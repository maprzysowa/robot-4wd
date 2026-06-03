

Kompaktowa, wytrzymała i zaawansowana platforma jezdna przeznaczona do budowy robotów mobilnych, pojazdów autonomicznych oraz projektów DIY. Dzięki zastosowaniu **dwóch poziomów z anodowanego aluminium** konstrukcja jest wyjątkowo sztywna, lekka i odporna na uszkodzenia mechaniczne.

Kluczowym elementem platformy są **koła Mecanum**, które w połączeniu z niezależnym napędem **4WD** zapewniają robotowi **wielokierunkowość (omnidirectional)**. Pojazd potrafi poruszać się w dowolnym kierunku – w przód, w tył, na boki (jazda krabem) oraz po skosie, a także obracać się w miejscu, co pozwala na genialną zwrotność w ciasnych przestrzeniach.
![[20260602_194158.jpg|200]]

---

### Główne cechy i zalety
* **Poruszanie wielokierunkowe (Omni):** Specjalna konstrukcja rolek na kołach Mecanum (ustawionych pod kątem 45°) pozwala na ruchy lateralne (boczne) bez konieczności obracania całego podwozia.
* **Solidna aluminiowa konstrukcja:** Dwa poziomy wykonane z aluminium zapewniają dużą przestrzeń montażową przy zachowaniu niskiej wagi i wysokiej trwałości.
* **Niezależny napęd 4WD:** Każde koło napędzane jest osobnym silnikiem DC z przekładnią. Sterując prędkością i kierunkiem obrotu każdego silnika z osobna, uzyskujemy pełny wektor ruchu.
* **Uniwersalna siatka otworów:** Płyty montażowe posiadają liczne otwory i fasolki, co ułatwia montaż mikrokontrolerów (Arduino, Raspberry Pi, ESP32), sterowników silników, sensorów (LiDAR, ultradźwięki) oraz akumulatorów.
* **Separacja poziomów:** Dwuwarstwowa konstrukcja pozwala na odseparowanie ciężkiej sekcji zasilania i napędu (dolny poziom) od delikatnej elektroniki sterującej (górny poziom).

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Typ podwozia** | 4WD Wielokierunkowe (Omnidirectional) |
| **Typ kół** | Koła Mecanum (zestaw zawiera 2 koła lewe i 2 koła prawe) |
| **Materiał ramy** | Aluminium (anodowane) |
| **Napięcie zasilania silników** | 3V - 6V DC (zalecane 6V) |
| **Przełożenie przekładni** | 1:48 (standardowe żółte silniki typu TT) |
| **Pobór prądu silnika** | ok. 70mA (bez obciążenia), do 250mA (przy zablokowanym wale dla 6V) |
| **Średnica kół Mecanum** | zazwyczaj ok. 60 mm - 65 mm |
| **Sposób skrętu** | Zmiana wektorów sił poprzez indywidualne sterowanie obrotami kół |

---

### ⚠️ Ważne wskazówki konstrukcyjne i programistyczne

1. **Układ kół (Kształt "X" lub "O"):** Koła Mecanum występują w wersjach Lewej (L) i Prawej (R). Aby robot poruszał się prawidłowo, rolki stykające się z podłożem muszą tworzyć określony wzór. Patrząc na robota **od góry**, osie rolek powinny tworzyć **kształt litery X** (skierowane do środka robota). Błędne założenie kół uniemożliwi jazdę na boki!
2. **Wymagania sterownika:** Ponieważ każde koło musi kręcić się niezależnie (często w różnych kierunkach w tym samym czasie), platforma wymaga sterownika zdolnego obsłużyć **4 niezależne silniki DC** (np. dwa podwójne mostki H L298N, dedykowany Motor Shield lub nowoczesny poczwórny sterownik oparty na układach TB6612).

---

### Zawartość typowego zestawu (BOM)
* 2 x Aluminiowa płyta podwozia (poziom dolny i górny)
* 4 x Koło Mecanum (2x Lewe, 2x Prawe)
* 4 x Silnik DC z przekładnią (typ TT) wraz z osadzeniem
* Zestaw dystansów do połączenia poziomów ramy
* Śruby i nakrętki montażowe

---

### Sugerowane komponenty do dokupienia
* **Zasilanie:** Koszyk na 2x ogniwo 18650 (7.4V) lub pakiet Li-Po 2S wraz z ładowarką USB-C 2S.
* **Kontroler:** Arduino Uno/Mega, ESP32 lub Raspberry Pi (do zaawansowanych algorytmów jazdy Omni wymagana jest biblioteka obsługująca kinematykę Mecanum).
* **Czujniki:** LiDAR, kamera mapująca (ROS), sensory ultradźwiękowe HC-SR04.