

Niezwykle popularny, wszechstronny i mocny moduł sterownika oparty na układzie **L298N**. Pozwala na niezależne kontrolowanie kierunku oraz prędkości obrotowej **dwóch silników prądu stałego (DC)** lub **jednego dwufazowego silnika krokowego**. 

Dzięki konstrukcji typu **Mostek H (H-Bridge)**, układ idealnie nadaje się do budowy robotów mobilnych (w tym platform 2WD i 4WD), pojazdów RC oraz systemów automatyki DIY opartych na Arduino, ESP32, Raspberry Pi czy AVR.

![[20260602_194313.jpg|200]]

---

### Główne cechy i zalety
* **Podwójny Mostek H:** Pozwala na niezależne sterowanie dwoma silnikami DC (ruch w przód, w tył, hamowanie) lub jednym silnikiem krokowym.
* **Wbudowany stabilizator 5V (78M05):** Moduł potrafi wygenerować napięcie 5V do zasilania mikrokontrolera (np. Arduino), jeśli napięcie zasilania silników mieści się w przedmiarze 7V - 12V.
* **Obsługa sygnału PWM:** Umożliwia płynną regulację prędkości obrotowej silników DC za pomocą modulacji szerokości impulsu.
* **Masywny radiator:** Duży aluminiowy radiator skutecznie odprowadza ciepło z układu L298N, zapewniając stabilną pracę pod obciążeniem.
* **Diody zabezpieczające:** Płytka posiada wbudowane diody tłumiące przepięcia (szpilki prądowe) generowane przez cewki silników.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Układ sterujący** | L298N (podwójny mostek H) |
| **Napięcie zasilania silników (VMS)** | DC 5V - 35V |
| **Maksymalny prąd wyjściowy (na kanał)** | 2A (chwilowy do 3A) |
| **Napięcie części logicznej** | 5V |
| **Prąd części logicznej** | 0mA - 36mA |
| **Maksymalny pobór mocy** | 20W (przy temperaturze T = 75°C) |
| **Wymiary płytki** | 43 mm x 43 mm x 27 mm |

---

### Opis wyprowadzeń i złączy śrubowych (Terminal Block)

#### Sekcja Zasilania (Złącze 3-pinowe):
* **VCC (lub VMS):** Plus zasilania silników (5V - 35V).
* **GND:** Masa układu (musi być wspólna z masą mikrokontrolera!).
* **+5V:** Wyjście napięcia 5V (gdy zworka *5V_EN* jest założona) lub wejście zasilania logiki (gdy zworka jest zdjęta).

#### Sekcja Wyjściowa (Złącza 2-pinowe):
* **OUT1 / OUT2:** Wyjście dla Silnika A (lub pierwszej cewki silnika krokowego).
* **OUT3 / OUT4:** Wyjście dla Silnika B (lub drugiej cewki silnika krokowego).

#### Sekcja Sterowania (Piny sygnałowe):
* **ENA:** Załączenie Silnika A (zdjęcie zworki i podanie sygnału PWM pozwala na regulację prędkości).
* **IN1 / IN2:** Kierunek obrotów Silnika A.
* **IN3 / IN4:** Kierunek obrotów Silnika B.
* **ENB:** Załączenie Silnika B (analogicznie jak ENA).

---

### ⚠️ Ważne zworki (Jumpers) na płytce

1. **Zworka 5V_EN (Stabilizator 5V):**
   * **ZAŁOŻONA:** Jeśli zasilasz silniki napięciem od **7V do 12V**, wbudowany stabilizator obniża je do 5V. Możesz wtedy z pinu "+5V" zasilić np. Arduino.
   * **ZDJĘTA:** Jeśli napięcie zasilania silników przekracza **12V** (lub jest niższe niż 7V), zworkę należy zdjąć, aby nie uszkodzić stabilizatora. Wtedy na pin "+5V" musisz podać zewnętrzne zasil