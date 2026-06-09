# Dokumentacja Projektowa: Robot Mobilny 4WD Omni (Mecanum)

Niniejszy dokument zawiera skorygowane wymagania projektowe, analizę architektury systemowej oraz wytyczne implementacyjne dla wielokierunkowego pojazdu robotycznego budowanego w ekosystemie Arduino.

---

## 1. Wstęp i Założenia Architektoniczne

Projekt bazuje na zaawansowanej architekturze dwuprocesorowej z podziałem zadań (Master/Slave). Wybór komponentów pozwala na pełne odciążenie jednostki sterującej ruchem od ciężkich zadań przetwarzania obrazu.

* **Jednostka Główna (Master):** Mikrokontroler **Arduino UNO R4 WiFi** (Cortex-M4). Odpowiada za pętlę sterowania ruchem, kinematykę kół Mecanum, odczyt czujników bezpieczeństwa oraz komunikację z gotową aplikacją mobilną (poprzez wbudowany moduł Wi-Fi).
* **Kompan Wizyjny (Slave):** Moduł **ESP32-S3 AI Camera (DFRobot)**. Działa autonomicznie jako jednostka Edge-AI, generując strumień wideo oraz realizując pokładowe algorytmy wizyjne (detekcja obiektów). Komunikuje się z UNO R4 przez sprzętowy port UART (`Serial1`).
* **Układ Wykonawczy:** Nakładka **L293D Motor Shield**. Konieczna do niezależnego wysterowania 4 silników DC (wymóg krytyczny dla kół Mecanum).
* **Sterowanie:** Wykorzystanie dostępnych na rynku aplikacji mobilnych wspierających Wi-Fi/TCP/UDP (np. Blynk, RemoteXY, Dabble).

---

## 2. Zredefiniowane Wymagania Funkcjonalne (Tryby Pracy)

Pojazd realizuje ruch w trzech sekwencyjnie implementowanych trybach (zgodnie z planem inkrementalnym):

### 2.a. Tryb Manualny LOS (Line of Sight)
* **Sterowanie:** Ruch we wszystkich kierunkach za pomocą wirtualnego joysticka w aplikacji mobilnej za pośrednictwem Wi-Fi.
* **Kinematyka:** Algorytm sterowania w pełni implementuje matematykę kół Mecanum, umożliwiając:
    * Ruch progresywny (przód/tył).
    * Ruch translacyjny / krabowy (jazda bezpośrednio w bok lewo/prawo bez zmiany orientacji frontu robota).
    * Ruch rotacyjny (obrót w miejscu).
* **Stabilizacja:** Aktywna korekcja kursu na podstawie odczytów z 3-osiowego żyroskopu/akcelerometru **MPU-6050** w celu eliminacji poślizgu kół na gładkich nawierzchniach.

### 2.b. Tryb Manualny FPV (First Person View)
* **Wizja FPV:** Moduł ESP32-S3 generuje niezależny strumień wideo (MJPEG/RTSP) przez Wi-Fi, osadzony bezpośrednio w widżecie podglądu w aplikacji mobilnej.
* **Manipulator Kamery:** Operator steruje pozycją kamery w osi poziomej (Pan) za pomocą mikro-serwa **SG90** zamontowanego w uchwycie Pan-Tilt. Sterowanie odbywa się przez suwak (Slider) w aplikacji mobilnej.

### 2.c. Tryb Autonomiczny (Edge-AI Object Tracking)
* **Detekcja Obiektu:** Moduł ESP32-S3 przetwarza obraz z kamery OV3660 w czasie rzeczywistym (wykorzystując akcelerację sprzętową sieci neuronowych) i lokalizuje zdefiniowany obiekt (np. kolorową piłkę lub twarz).
* **Algorytm Śledzenia:** ESP32-S3 przesyła współrzędne środka obiektu przez UART do Arduino UNO R4. UNO R4 steruje napędem tak, aby utrzymać obiekt w centrum kadru i w zadanej odległości (np. 50 cm).
* **Telemetria:** Bieżący tryb pracy, dystans od przeszkody oraz dane z czujnika temperatury **AHT10** są wyświetlane na pokładowym ekranie **LCD 1602 (I2C)**.

---

## 3. System Bezpieczeństwa (Unikanie Kolizji i Detekcja Zderzeń)

W pętli głównej Arduino UNO R4 stale procesowane są dane z czujników w celu aktywnej ochrony konstrukcji robota przed uszkodzeniem.

* **Proaktywne unikanie kolizji (HC-SR04):**
    * **W trybach manualnych (2.a, 2.b):** Zbliżenie się do przeszkody na odległość **< 20 cm** aktywuje wymuszone zatrzymanie silników (Override). Algorytm blokuje wektor ruchu w stronę przeszkody, zezwalając operatorowi jedynie na wycofanie pojazdu lub odskok w bok (strafe).
    * **W trybie autonomicznym (2.c):** Wykrycie przeszkody na dystansie **< 40 cm** przerywa procedurę śledzenia. Robot wykonuje autonomiczny manewr ominięcia: wykorzystując zalety kół Mecanum, wykonuje płynny ruch translacyjny w bok (omijanie bez obracania kamery i utraty obiektu z kadru), mija przeszkodę, a następnie wraca do procedury śledzenia.
* **Reaktywna detekcja kolizji / Pasywne bezpieczeństwo (MPU-6050):**
    * Algorytm monitoruje w czasie rzeczywistym wypadkowe przyspieszenie liniowe na osiach X i Y (płaszczyzna ruchu pojazdu). 
    * W przypadku wykrycia nagłego skoku przeciążenia (szpilka akcelerometru przekraczająca zdefiniowany próg programowy, np. **$|a| > 2g$** wywołany fizycznym uderzeniem w przeszkodę), system natychmiast odcina zasilanie silników (Emergency Brake).
    * Robot przechodzi w stan błędu, wysyła alert telemetryczny o kolizji do aplikacji mobilnej oraz na ekran LCD 1602 i ignoruje dalsze komendy ruchu do momentu manualnego zresetowania/potwierdzenia błędu przez operatora w aplikacji.
* **Failsafe (Utrata Sygnału):** Brak odebrania ramki danych z aplikacji mobilnej przez czas dłuższy niż 1000 ms w trybie manualnym skutkuje natychmiastowym zatrzymaniem wszystkich silników w celu uniknięcia "ucieczki" robota po zerwaniu połączenia Wi-Fi.

---

## 4. Architektura Sprzętowa i Dystrybucja Zasilania

Aby zapobiec zakłóceniom generowanym przez silniki DC oraz restartom (brown-out) mikrokontrolerów, zastosowano pełną izolację szyn zasilania:

1.  **Linia Wysokoprądowa (Silniki):** Napięcie z pakietu akumulatorów 18650 (~7.4V - 8.4V) zasila bezpośrednio złącze `EXT_PWR` na nakładce L293D. **Zworka PWR na shieldzie musi być zdjęta!**
2.  **Linia Logiczna (5V):** Przetwornica LM2596s obniża napięcie z pakietu do stabilnego **5.0V**, zasilając szynę na płytce stykowej MB-102. Z tej szyny zasilane jest Arduino (pin 5V), moduł ESP32-S3, serwo SG90, ekran LCD oraz czujniki.

### 4.1. Diagram Blokowy Połączeń (Mermaid)

```mermaid
graph TD
    %% --- PODSYSTEM ZASILANIA ---
    subgraph ZASILANIE [Podsystem Zasilania]
        Aku[Pakiet 2x 18650 Li-Ion ~7.4V] -->|Główne zasilanie| Sw[Przełącznik ON/OFF]
        Sw -->|Napięcie surowe V_MOTOR| L293D[L293D Motor Shield]
        Sw -->|Wejście IN| LM2596[Przetwornica Step-Down LM2596s]
        LM2596 -->|Stabilizowane 5V| Bus5V[Szyna 5V - Płytka Stykowa]
    end

    %% --- PODSYSTEM STEROWANIA ---
    subgraph STEROWANIE [Podsystem Logiki]
        Uno[Arduino UNO R4 WiFi <br> Mózg Główny]
        ESP32[ESP32-S3 AI Camera <br> Koprocesor Wizyjny]
        Uno <-->|Protokół UART <br> RX1 / TX1| ESP32
    end

    %% --- PERYFERIA WYKONAWCZE ---
    subgraph NAPED [Sekcja Wykonawcza]
        L293D --> M1[Silnik Front-Left]
        L293D --> M2[Silnik Front-Right]
        L293D --> M3[Silnik Back-Left]
        L293D --> M4[Silnik Back-Right]
        L293D --> Servo[Serwo SG90 Pan/Tilt]
    end

    %% --- SENSORY I TELEMETRIA ---
    subgraph SENSORY [Podsystem Sensoryczny]
        HC[Czujnik Odległości <br> HC-SR04]
        MPU[Żyroskop / Akcelerometr <br> MPU-6050]
        LCD[Wyświetlacz <br> LCD 1602 I2C]
        AHT[Czujnik Pogodowy <br> AHT10]
    end

    %% --- DYSTRYBUCJA ZASILANIA LOGICZNEGO ---
    Bus5V -->|Zasilanie 5V| Uno
    Bus5V -->|Zasilanie 5V| ESP32
    Bus5V -->|Zasilanie 5V| HC
    Bus5V -->|Zasilanie 5V| MPU
    Bus5V -->|Zasilanie 5V| LCD
    Bus5V -->|Zasilanie 5V| AHT

    %% --- LINIE SYGNAŁOWE ---
    Uno ===|Bezpośrednie wpięcie mechaniczne| L293D
    Uno -->|Sygnały Cyfrowe <br> Trigger: A0 / Echo: A1| HC
    Uno <-->|Magistrala I2C <br> Współdzielone SDA / SCL| MPU
    Uno <-->|Magistrala I2C <br> Współdzielone SDA / SCL| LCD
    Uno <-->|Magistrala I2C <br> Współdzielone SDA / SCL| AHT

    %% --- KOMUNIKACJA BEZPRZEWODOWA ---
    ESP32 -.->|Strumień Wideo Wi-Fi| App((Aplikacja Mobilna))
    Uno -.->|Komendy Ruchu Wi-Fi| App
```
---

### 4.2. Szczegółowe Mapowanie Pinów (Pinout)

Poniższa tabela przedstawia fizyczną i logiczną alokację pinów mikrokontrolera Arduino UNO R4 WiFi. Z uwagi na fakt, że nakładka L293D Motor Shield rezerwuje większość pinów cyfrowych, do obsługi czujników wykorzystano piny analogowe (A0, A1) działające w trybie cyfrowym oraz dedykowaną magistralę I2C.

| Komponent | Pin Komponentu | Pin Arduino UNO R4 | Kierunek (I/O) | Typ Sygnału | Opis Funkcjonalny |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **L293D Shield** | M1_PWM / M1_DIR | D11 / D4 | Output | PWM / Digital | Sterowanie silnikiem Front-Left (Silnik 1) |
| **L293D Shield** | M2_PWM / M2_DIR | D3 / D5 | Output | PWM / Digital | Sterowanie silnikiem Front-Right (Silnik 2) |
| **L293D Shield** | M3_PWM / M3_DIR | D6 / D7 | Output | PWM / Digital | Sterowanie silnikiem Back-Left (Silnik 3) |
| **L293D Shield** | M4_PWM / M4_DIR | D9 / D8 | Output | PWM / Digital | Sterowanie silnikiem Back-Right (Silnik 4) |
| **Serwo SG90** | PWM (Pomarańczowy) | D10 | Output | PWM | Sterowanie osią Pan/Tilt (Złącze SERVO_1 na Shieldzie) |
| **ESP32-S3 Cam** | TX | D0 (RX1) | Input | UART Hardware | Odbiór danych/koordynatów z koprocesora wizyjnego |
| **ESP32-S3 Cam** | RX | D1 (TX1) | Output | UART Hardware | Wysyłanie komend konfiguracyjnych do kamery |
| **HC-SR04** | Trigger | A0 | Output | Digital | Wyzwolenie pomiaru odległości (impuls 10 µs) |
| **HC-SR04** | Echo | A1 | Input | Digital | Odczyt czasu powrotu fali (pomiar odległości) |
| **MPU-6050** | SDA | Dedykowany SDA | In/Out | I2C Data | Współdzielona szyna danych (Adres: `0x68`) |
| **MPU-6050** | SCL | Dedykowany SCL | Output | I2C Clock | Współdzielona szyna zegarowa |
| **LCD 1602** | SDA | Dedykowany SDA | In/Out | I2C Data | Współdzielona szyna danych (Adres: `0x27` lub `0x3F`) |
| **LCD 1602** | SCL | Dedykowany SCL | Output | I2C Clock | Współdzielona szyna zegarowa |
| **AHT10** | SDA | Dedykowany SDA | In/Out | I2C Data | Współdzielona szyna danych (Adres: `0x38`) |
| **AHT10** | SCL | Dedykowany SCL | Output | I2C Clock | Współdzielona szyna zegarowa |

---

### 4.3. Krytyczne Konfiguracje Zworkowe i Zasilające

Podczas montażu elektroniki należy bezwzględnie przestrzegać poniższej konfiguracji, aby zapobiec przeciążeniom prądowym:

* **Zworka PWR (Power Jumper) na L293D Shield:** **WYCIĄGNIĘTA (ZDJĘTA)**. 
  * *Uzasadnienie:* Pakiet akumulatorów Li-Ion 2S (do 8.4V) podłączony do złącza śrubowego `EXT_PWR` na shieldzie nie może zasilać stabilizatora Arduino bezpośrednio przez pin Vin. Arduino UNO R4 WiFi posiada delikatniejszą sekcję zasilania niż wersja R3.
* **Zasilanie Logiki (Arduino, ESP32-S3, Sensory):** Realizowane centralnie z szyny 5V płytki stykowej MB-102, która otrzymuje stabilne, odfiltrowane napięcie z przetwornicy LM2596s.
* **Separacja Mas (GND):** Wszystkie punkty masy (GND akumulatora, GND przetwornicy, GND Arduino, GND L293D oraz GND płytki stykowej) **muszą być ze sobą fizycznie połączone** w jednym punkcie (wspólna masa odniesienia dla sygnałów logicznych).
