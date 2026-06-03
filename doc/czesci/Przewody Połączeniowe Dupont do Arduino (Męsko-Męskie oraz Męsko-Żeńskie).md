
Niezbędny element wyposażenia każdego warsztatu elektronicznego i pracowni DIY. Elastyczne przewody połączeniowe (tzw. **kable Dupont**) zakończone standardowymi pinami o skoku **2.54 mm** (0.1"). Umożliwiają błyskawiczne, bezlutowe łączenie komponentów, mikrokontrolerów, czujników oraz płytek stykowych (breadboard).

Przewody dostarczane są zazwyczaj w formie wygodnej taśmy 40-pinowej, z której można pojedynczo odrywać potrzebną liczbę kabli. Każda żyła posiada inny kolor izolacji (taśma wielokolorowa/tęczowa), co ogromnie ułatwia identyfikację sygnałów w złożonych projektach.
![[20260602_193538.jpg|200]]

---

### Rodzaje przewodów w zestawach i ich zastosowanie

#### 1. Przewody Męsko-Męskie (M-M / Male-Male)
Zakończone sztywnymi pinami (wtykami) z obu stron.
* **Główne zastosowanie:** Łączenie otworów w płytce stykowej między sobą, mostkowanie zasilania oraz łączenie pinów żeńskich mikrokontrolera (np. Arduino UNO R4, sterownik L298N) bezpośrednio z płytką stykową.

#### 2. Przewody Męsko-Żeńskie (M-Ż / Male-Female)
Zakończone wtykiem z jednej strony oraz gniazdem z drugiej.
* **Główne zastosowanie:** Przedłużanie połączeń. Idealne do podłączania modułów z wyprowadzonymi pinami męskimi (np. czujnik ultradźwiękowy HC-SR04, żyroskop MPU-6050, serwo SG90) bezpośrednio do gniazd w mikrokontrolerze (Arduino UNO) lub do wpięcia ich w płytkę stykową.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Typ złącza** | Dupont (standardowe złącze kołkowe) |
| **Raster pinów (skok)** | 2.54 mm (0.1") |
| **Długość przewodów** | Zazwyczaj 10 cm, 20 cm lub 30 cm (w zależności od zestawu) |
| **Ilość żył w taśmie** | 40 sztuk |
| **Kolorystyka** | Wielokolorowe (10 powtarzających się kolorów) |
| **Materiał przewodnika**| Miedź platerowana (OFC lub CCA) |
| **Izolacja** | Elastyczne PVC |

---

### 💡 Praktyczne porady warsztatowe

1. **Zarządzanie kolorami (Dobra praktyka):** Aby uniknąć pomyłek i przypadkowego zwarcia, staraj się zawsze trzymać standardu kolorystycznego:
   * **Czerwony** – Zasilanie dodatnie (+5V, +3.3V, VCC).
   * **Czarny (lub brązowy)** – Masa (GND).
   * **Inne kolory** – Linie sygnałowe (np. żółty dla SDA, zielony dla SCL, nie