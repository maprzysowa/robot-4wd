Kultowa nakładka silnikowa (**Motor Shield**) stworzona specjalnie dla płytek kompatybilnych z **Arduino UNO** (w tym UNO R3 oraz nowszych wersji, jak UNO R4). Moduł oparty jest na dwóch dwukanałowych mostkach H typu **L293D** oraz jednym rejestrze przesuwnym **74HC595**, który pozwala zaoszczędzić piny Arduino poprzez szeregowe sterowanie kierunkiem obrotów.

Ta nakładka to idealne rozwiązanie "wszystko w jednym" do budowy pojazdów gąsienicowych, ramion robotycznych oraz zaawansowanych platform jezdnych (np. robotów z kołami Mecanum), ponieważ eliminuje potrzebę stosowania płytek stykowych i plątaniny kabli.
![L293D](20260602_193515.jpg)

---

### Główne cechy i możliwości sterowania

Shield cechuje się ogromną wszechstronnością i pozwala na jednoczesne podłączenie:
* Do **4 silników prądu stałego (DC)** z niezależną regulacją kierunku oraz prędkości (poprzez PWM).
* LUB do **2 silników krokowych** (bipolarnych lub unipolarnych) ze sterowaniem jedno- lub dwufazowym.
* Dodatkowo płytka wyprowadza linie zasilania i sygnałowe dla **2 serwomechanizmów 5V** (np. SG90), podłączonych bezpośrednio do dedykowanych timerów Arduino (piny 9 i 10).

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Układy wykonawcze** | 2x L293D (Mostek H) + 1x 74HC595 (Rejestr przesuwny) |
| **Napięcie zasilania silników (EXT_PWR)**| DC 4.5V - 25V (zewnętrzne źródło) |
| **Napięcie zasilania logiki** | 5V (pobierane bezpośrednio z Arduino) |
| **Prąd wyjściowy na kanał** | 600 mA (ciągły) |
| **Prąd szczytowy na kanał** | 1.2 A (chwilowy, impulsowy) |
| **Zabezpieczenia** | Wbudowane diody zabezpieczające przed prądami wstrotnymi oraz zabezpieczenie termiczne |
| **Złącza wyjściowe** | Terminale śrubowe (ARK) dla silników i zasilania |
| **Przycisk RESET** | Wbudowany na nakładce (powielenie przycisku z Arduino) |

---

### Opis złączy i wyprowadzeń (Pinout)



1. **Złącza silników DC / Krokowych:**
   * **M1 i M2:** Bloki śrubowe po lewej stronie (obsługiwane przez pierwszy układ L293D).
   * **M3 i M4:** Bloki śrubowe po prawej stronie (obsługiwane przez drugi układ L293D).
   * Do sterowania silnikiem krokowym wykorzystuje się parę złączy (np. M1+M2 dla pierwszego silnika i M3+M4 dla drugiego).
2. **Złącze zasilania zewnętrznego (EXT_PWR):**
   * Dwupinowy zacisk śrubowy opisany jako **GND** i **M_PWR** (lub VIN). Służy do doprowadzenia prądu dla silników z zewnętrznego źródła (np. koszyka 2S z ogniwami 18650).
3. **Zworka zasilania (PWR Jumper):**
   * Gdy zworka jest włożona, zasilanie silników jest połączone z zasilaniem Arduino.
   * Gdy zworka jest wyciągnięta, zasilanie silników (EXT_PWR) jest **całkowicie odseparowane** od elektroniki Arduino.

---

### ⚠️ Bardzo ważne wskazówki dotyczące użytkowania i bezpieczeństwa

1. **Zworka zasilania a bezpiecznik (Złota Zasada):** Podczas korzystania z silników DC lub krokowych **zawsze wyciąg