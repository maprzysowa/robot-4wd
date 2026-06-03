
Niezwykle popularne, lekkie i kompaktowe mikroserwo o wadze zaledwie **9 gramów**. Jest to absolutny standard w świecie modelarstwa RC oraz edukacyjnej robotyki DIY. Pozwala na precyzyjne kontrolowanie pozycji wału w zakresie **od 0° do 180°**.

Dzięki sterowaniu sygnałem PWM, serwo SG90 jest banalnie proste w obsłudze i współpracuje bezpośrednio z praktycznie każdym mikrokontrolerem, takim jak Arduino, ESP32, Raspberry Pi czy układy STM32.
![TowerPro SG90](20260602_194804.jpg)

---

### Główne cechy i zalety
* **Kompaktowe wymiary i niska waga:** Przy wadze 9g idealnie nadaje się do projektów lotniczych (samoloty, drony) oraz miniaturowych robotów.
* **Wysoki moment obrotowy:** Mimo małych gabarytów, serwo oferuje moment rzędu 1.6 kg/cm (przy zasilaniu 4.8V).
* **Komplet akcesoriów w zestawie:** Zazwyczaj dostarczane z zestawem 3 różnych orczyków (dźwigni) oraz śrubek montażowych.
* **Szeroka kompatybilność:** Standardowy rozstaw pinów wtyczki typu "Dupont" (grafitowy/czarny, czerwony, pomarańczowy).

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Model** | TowerPro SG90 (Micro Servo) |
| **Wymiary** | 22.2 mm x 11.8 mm x 22.7 mm |
| **Waga** | 9 g (samo serwo bez kabla) |
| **Moment obrotowy (Torque)** | 1.6 kg/cm (4.8V) |
| **Prędkość ruchu** | 0.12 s / 60° (4.8V) |
| **Napięcie pracy** | 4.8V - 6.0V |
| **Zakres obrotu** | 180° (odpowiedź na szerokość impulsu) |
| **Typ zębatek** | Tworzywo sztuczne (plastikowe) |
| **Temperatura pracy** | -30°C do +60°C |
| **Długość przewodu** | ok. 25 cm |

---

### Opis wyprowadzeń (Pinout przewodu)

Serwo posiada standardowy 3-żyłowy przewód zakończony żeńskim złączem. Kolory kabli odpowiadają następującym funkcjom:

* **Brązowy (lub czarny):** GND – Masa układu.
* **Czerwony:** VCC – Zasilanie (4.8V - 6V).
* **Pomarańczowy (lub żółty):** PWM / Signal – Sygnał sterujący z mikrokontrolera.

---

### ⚙️ Sterowanie (Sygnał PWM)

Pozycja serwa jest kontrolowana za pomocą impulsu o częstotliwości **50 Hz** (okres 20 ms). Czas trwania stanu wysokiego (szerokość impulsu) definiuje kąt wychylenia orczyka:

* Impuls **1.0 ms** (1000 µs) – ustawia serwo w pozycji **0°**
* Impuls **1.5 ms** (1500 µs) – ustawia serwo w pozycji **90°** (środek)
* Impuls **2.0 ms** (2000 µs) – ustawia serwo w pozycji **180°**

*Uwaga: W zależności od producenta i partii, skrajne wartości impulsów mogą się nieznacznie różnić (np. od 5