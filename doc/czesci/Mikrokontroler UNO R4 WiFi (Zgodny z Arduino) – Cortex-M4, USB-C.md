

Rewolucyjna ewolucja kultowej płytki rozwojowej UNO. Wersja **UNO R4 WiFi** łączy w sobie klasyczny, uwielbiany przez twórców format (rozmieszczenie pinów) z potężną, nowoczesną architekturą 32-bitową oraz pełną łącznością bezprzewodową. 

Sercem płytki jest wydajny mikrokontroler **Renesas RA4M1 (ARM Cortex-M4)** taktowany zegarem 48 MHz, wspierany przez koprocesor **ESP32-S3**, który odpowiada za bezproblemową komunikację Wi-Fi oraz Bluetooth. To idealna platforma do projektów IoT (Internet of Things), zaawansowanej robotyki oraz automatyki domowej.
![Arduino R4](20260602_193403.jpg)

---

### Główne cechy i zalety
* **Potężna architektura 32-bitowa:** Przeskok z wysłużonego 8-bitowego układu na ARM Cortex-M4 zapewnia wielokrotnie większą moc obliczeniową i szybkość działania.
* **Zintegrowane Wi-Fi i Bluetooth LE:** Dzięki układowi ESP32-S3 płytka pozwala na łatwe łączenie się z siecią, wysyłanie danych do chmury (np. Arduino Cloud) oraz sterowanie przez smartfon.
* **Wbudowana matryca LED (12x8):** Wyjątkowy element płytki – jasnoczerwona matryca 96 diod LED pozwala na wyświetlanie prostych animacji, napisów czy danych z czujników bez podłączania zewnętrznego ekranu.
* **Nowoczesne złącze USB-C:** Służy do programowania oraz zasilania płytki, zastępując stary i duży port USB Typu B.
* **Złącze Qwiic / STEMMA QT:** Wbudowany port I2C kompatybilny z systemem Qwiic pozwala na błyskawiczne podłączanie kompatybilnych czujników i modułów za pomocą gotowych przewodów, bez lutowania.
* **Obsługa CAN Bus oraz przetwornik DAC:** Płytka wspiera przemysłowy standard komunikacji CAN oraz posiada prawdziwy 12-bitowy przetwornik cyfrowo-analogowy (DAC) do generowania sygnałów audio/analogowych.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Główny mikrokontroler** | Renesas RA4M1 (ARM Cortex-M4 32-bit) |
| **Taktowanie zegara** | 48 MHz |
| **Pamięć Flash** | 256 kB |
| **Pamięć SRAM** | 32 kB |
| **Pamięć EEPROM** | 8 kB |
| **Układ łączności bezprzewodowej**| ESP32-S3 (Wi-Fi 802.11 b/g/n + Bluetooth 5.0 / BLE) |
| **Napięcie pracy (logiki)** | 5V |
| **Napięcie wejściowe (rekomendowane)**| 6V - 24V (przez gniazdo DC Barrel) |
| **Piny cyfrowe I/O** | 14 (w tym 6 z obsługą PWM) |
| **Piny wejść analogowych (ADC)**| 6 |
| **Piny wyjść analogowych (DAC)**| 1 (prawdziwy 12-bitowy DAC) |
| **Interfejsy komunikacyjne** | UART, SPI, I2C, CAN Bus |
| **Złącze programowania** | USB-C |

---

### Nowości w architekturze UNO R4 w porównaniu do UNO R3

1. **Zwiększone napięcie zasilania:** Ulepszony obwód zasilania pozwala na bezpieczne podłączenie napięcia wejściowego aż do 24V przez gniazdo DC, co ułatwia integrację płytki np. w systemach automatyki przemysłowej czy robotach z pakietami Li-Po 4S/6S.
2. **Zaawansowane układy HID:** UNO R4 potrafi emulować myszkę lub klawiaturę (Human Interface Device) po podłączeniu do komputera przez USB-C, co otwiera drogę do tworzenia własnych kontrolerów gier czy paneli skrótów.
3. **Zabezpieczenie nadprądowe:** Płytka posiada ulepszone bezpieczniki chroniące port USB komputera oraz same piny mikrokontrolera przed skutkami przypadkowego zwarcia.

---

### Zastosowanie
* **Projekty Internetu Rzeczy (IoT):** Inteligentne stacje pogodowe, systemy monitoringu domowego wysyłające powiadomienia na telefon.
* **Inteligentny dom (Smart Home):** Sterowanie oświetleniem, integracja z systemami Home Assistant przez Wi-Fi.
* **Robotyka mobilna:** Znakomity mózg sterujący dla zaawansowanych platform (np. pojazdów 4WD z kołami Mecanum), dzięki natywnej obsłudze obliczeń zmiennoprzecinkowych.
* **Edukacja:** Nauka programowania nowoczesnych mikrokontrolerów 32-bitowych z zachowaniem pełnej kompatybilności z większością starych nakładek (Shieldów) projektowanych dla UNO R3.