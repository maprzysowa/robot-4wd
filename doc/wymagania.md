# Wymagania Projektowe: Robot 4WD (Mecanum)

Projekt zakłada budowę wielokierunkowego (Omnidirectional) pojazdu robotycznego klasy 4WD w ekosystemie Arduino, rozwijanego w sposób przyrostowy (inkrementalny).

---

## 1. Architektura Sprzętowo-Systemowa (Hardware Blueprint)

Projekt bazuje na architekturze dwuprocesorowej z podziałem zadań (Master/Slave):
*   **Jednostka Główna (Master):** Mikrokontroler **Arduino UNO R4 WiFi** (Cortex-M4). Odpowiada za pętlę sterowania ruchem, kinematykę kół Mecanum, odczyt czujników bezpieczeństwa (HC-SR04, MPU-6050) oraz komunikację z aplikacją mobilną.
*   **Kompaniom Wizyjny (Slave):** Moduł **ESP32-S3 AI Camera (DFRobot)**. Odpowiada autonomicznie za generowanie strumienia wideo oraz pokładowe algorytmy rozpoznawania obiektów (Edge-AI). Komunikacja z jednostką główną odbywa się przez interfejs UART/I2C.
*   **Układ Wykonawczy:** Nakładka **L293D Motor Shield** zamontowana na Arduino UNO R4, sterująca niezależnie 4 silnikami DC (wymóg konieczny dla kół Mecanum).
*   **Zasilanie:** Pakiet 2x Akumulator Li-Ion 18650 w konfiguracji 2S (nominalnie ~7.4V), stabilizowany przez przetwornicę Step-Down LM2596s do zasilania logiki (5V) oraz bezpośrednio zasilający sekcję wysokoprądową silników.

---

## 2. Wymagania Funkcjonalne (Tryby Pracy)

Robot musi realizować ruch w trzech sekwencyjnie implementowanych trybach. Sterowanie i podgląd realizowane są za pomocą **dostępnych na rynku aplikacji mobilnych** obsługujących komunikację Wi-Fi (np. Blynk, RemoteXY, Dabble):

### 2.a. Tryb Manualny LOS (Line of Sight)
*   **Sterowanie:** Ruch we wszystkich kierunkach za pomocą wirtualnego joysticka w aplikacji mobilnej (komunikacja przez Wi-Fi / protokół TCP/UDP).
*   **Kinematyka:** Algorytm sterowania musi w pełni wykorzystywać koła Mecanum, umożliwiając:
    *   Ruch progresywny (przód/tył).
    *   Ruch translacyjny / krabowy (jazda bezpośrednio w bok lewo/prawo bez zmiany orientacji).
    *   Ruch rotacyjny (obrót w miejscu).
*   **Stabilizacja:** Wykorzystanie danych z żyroskopu/akcelerometru **MPU-6050** do aktywnej korekcji kursu (jazda po prostej i eliminacja poślizgu kół).

### 2.b. Tryb Manualny FPV (First Person View)
*   **Wideo:** Moduł ESP32-S3 generuje strumień wideo MJPEG/RTSP przez Wi-Fi, który jest osadzony w dedykowanym widżecie (Video Streaming Widget) w aplikacji mobilnej.
*   **Manipulator Kamery:** Operator ma możliwość zdalnego obracania kamery w osi poziomej lub pionowej za pomocą mikro-serwa **SG90** zamontowanego w uchwycie Pan-Tilt, sterowanego z poziomu suwaka (Slider) w aplikacji.

### 2.c. Tryb Autonomiczny (Edge-AI Object Tracking)
*   **Detekcja:** Moduł ESP32-S3 przetwarza obraz z kamery OV3660 w czasie rzeczywistym i lokalizuje wyuczony obiekt (np. twarz lub kolorowa piłka).
*   **Algorytm Śledzenia:** Po wykryciu obiektu, ESP32-S3 wysyła komendy do UNO R4, które steruje napędem tak, aby utrzymać obiekt w centrum kadru i w stałej odległości (np. 50 cm).
*   **Status systemu:** Aktualny tryb pracy oraz dystans do obiektu wyświetlane są na pokładowym ekranie **LCD 1602 (I2C)**.

---

## 3. System Bezpieczeństwa (Unikanie Kolizji)

W pętli głównej Arduino UNO R4 stale procesowane są dane z cyfrowego czujnika odległości **HC-SR04** zamontowanego na froncie robota.

*   **W trybach manualnych (2.a, 2.b):** Zbliżenie się do przeszkody na odległość **< 20 cm** aktywuje wymuszone zatrzymanie silników (Override). Aplikacja mobilna blokuje wektor ruchu w stronę przeszkody, zezwalając jedynie na wycofanie pojazdu lub odskok w bok (strafe).
*   **W trybie autonomicznym (2.c):** Wykrycie przeszkody na dystansie **< 40 cm** przerywa procedurę śledzenia. Robot wykonuje autonomiczny manewr ominięcia: wykorzystując koła Mecanum, wykonuje płynny ruch translacyjny w bok (omijanie bez obracania kamery), mija przeszkodę, po czym wraca do procedury poszukiwania i śledzenia obiektu.
*   **Failsafe (Utrata Sygnału):** Brak odebrania ramki danych z aplikacji mobilnej przez czas dłuższy niż 1000 ms w trybie manualnym skutkuje natychmiastowym zatrzymaniem wszystkich silników.

---

## 4. Harmonogram i Kamienie Milowe (Plan Inkrementalny)

Rozwój projektu musi przebiegać ściśle według poniższych kroków. Przejście do kolejnego kroku wymaga pełnego zaliczenia testów stabilności kroku poprzedniego.

### Krok 1: Inkrement Bazy Napędowej (Tryb 2.a)
*   **Hardware:** Montaż podwozia, kół Mecanum, Arduino UNO R4, L293D Shield, MPU-6050, HC-SR04 oraz zasilania.
*   **Software:** Implementacja matematyki kół Mecanum. Integracja z wybraną aplikacją mobilną po Wi-Fi (np. konfiguracja dashboardu z joystickem). Implementacja awaryjnego zatrzymania przed ścianą.

### Krok 2: Inkrement Strumieniowania Wideo (Tryb 2.b)
*   **Hardware:** Montaż uchwytu Pan-Tilt, serwa SG90 oraz modułu ESP32-S3.
*   **Software:** Uruchomienie serwera wideo na ESP32-S3. Konfiguracja odbierania obrazu w aplikacji mobilnej. Spięcie sterowania serwem z interfejsem aplikacji.

### Krok 3: Inkrement Inteligencji Brzegowej (Tryb 2.c)
*   **Hardware:** Integracja wyświetlacza LCD 1602 oraz czujnika AHT10 (jako telemetryczna stacja pogodowa na robocie).
*   **Software:** Uruchomienie modelu detekcji obiektów na ESP32-S3. Ustanowienie komunikacji UART/I2C między ESP32-S3 a UNO R4 w celu przesyłania koordynatów celu. Implementacja autonomicznego omijania przeszkód "w bok".
