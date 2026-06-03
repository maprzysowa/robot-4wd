
Klasyczny, niezwykle popularny alfanumeryczny wyświetlacz LCD zdolny do wyświetlania tekstu w **2 liniach po 16 znaków w każdej**. Prezentowana wersja posiada niebieskie tło oraz kontrastowe, białe znaki, co zapewnia doskonałą czytelność wyświetlanych komunikatów.

Głównym atutem modułu jest **fabrycznie przylutowany konwerter magistrali I2C** (oparty na układzie PCF8574). Dzięki niemu, zamiast tradycyjnego, skomplikowanego podłączania aż 16 przewodów do mikrokontrolera, do pełnej obsługi ekranu wymagane są **tylko 2 piny sygnałowe** (SDA i SCL). To drastycznie oszczędza piny w Arduino czy ESP32.
![LCD](20260602_193428.jpg)

---

### Główne cechy i zalety
* **Oszczędność pinów (Interfejs I2C):** Cały ekran obsługiwany jest za pomocą zaledwie 4 przewodów (zasilanie VCC, GND oraz linie danych I2C).
* **Regulacja kontrastu:** Na płytce konwertera I2C znajduje się wbudowany potencjometr (niebieski), którym można idealnie dostroić widoczność znaków.
* **Sterowanie podświetleniem:** Konwerter posiada dedykowaną zworkę (jumper). Jej zdjęcie pozwala programowo lub fizycznie wyłączyć podświetlenie ekranu w celu oszczędzania energii.
* **Szeroka kompatybilność:** Standard oparty na kultowym sterowniku HD44780, wspierany przez gotowe biblioteki (np. *LiquidCrystal_I2C*) na Arduino, Raspberry Pi, ESP32 i STM32.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Rozdzielczość tekstu** | 16 znaków x 2 linie |
| **Sterownik wyświetlacza** | HD44780 (lub zgodny) |
| **Konwerter magistrali** | I2C (układ PCF8574) |
| **Napięcie zasilania** | 5V DC |
| **Kolor podświetlenia** | Niebieski |
| **Kolor znaków** | Biały |
| **Adres magistrali I2C** | 0x27 lub 0x3F (w zależności od partii układowej) |
| **Wymiary modułu** | 80 mm x 36 mm x 19 mm |

---

### Opis wyprowadzeń złącza I2C (Pinout)

Konwerter wyprowadza standardowe złącze męskie (goldpin) z 4 pinami:

* **GND** – Masa układu (wspólna z mikrokontrolerem).
* **VCC** – Zasilanie +5V DC.
* **SDA** – Linia danych magistrali I2C (Serial Data).
* **SCL** – Linia zegarowa magistrali I2C (Serial Clock).

---

### ⚠️ Wskazówki programistyczne i rozwiązywanie problemów

1. **"Ekran świeci, ale nie widzę tekstu":** To najczęstszy problem przy pierwszym uruchomieniu. W 99% przypadków kontrast jest ustawiony fabrycznie na zero. Weź mały śrubokręt i delikatnie **pokręć niebieskim potencjometrem** na plecach wyświetlacza, aż na ekranie pojawią się białe prostokąty lub tekst.
2. **Problem z adresem I2C:** Jeśli wgrałeś poprawny kod, a ekran nie reaguje, biblioteka może odwoływać się do złego adresu I2C. Najpopularniejsze adresy dla tego modułu to `0x27` lub `0x3F`. Jeśli nie jesteś pewien, jaki masz układ, wgraj do Arduino darmowy szkic o nazwie **I2C Scanner** – wyświetli on dokładny adres Twojego ekranu w Monitorze Portu Szeregowego.
3. **Zmiana adresu sprzętowego:** Na płytce konwertera znajdują się trzy sekcje zworkowe opisane jako `A0, A1, A2`. Poprzez zlutowanie tych padów możesz zmienić adres I2C modułu. Pozwala to na podłączenie do jednej magistrali Arduino nawet kilku wyświetlaczy LCD jednocześnie.

---

### Zastosowanie
* **Interfejsy użytkownika (UI):** Wyświetlanie menu, statusu urządzenia, komunikatów powitalnych.
* **Stacje pogodowe i pomiarowe:** Prezentacja aktualnej temperatury, wilgotności, ciśnienia lub odległości (np. pobranej z czujnika HC-SR04).
* **Robotyka mobilna:** Wyświetlanie aktualnego trybu pracy robota (np. "Line Follower", "Manual"), poziomu naładowania baterii z koszyka 18650 czy wykrytych błędów.
* **Liczniki i zegary:** Budowa stoperów, liczników produkcyjnych czy zegarów szachowych.