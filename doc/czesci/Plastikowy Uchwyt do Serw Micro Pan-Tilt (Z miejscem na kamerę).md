
Lekki, uniwersalny mechanizm obrotowo-pochylny typu **Pan-Tilt (2-DOF)** wykonany z wytrzymałego tworzywa sztucznego (formowanego wtryskowo). Uchwyt został zaprojektowany specjalnie jako platforma montażowa dla miniaturowych kamer oraz czujników, umożliwiając im ruch w dwóch płaszczyznach: poziomej (Pan) oraz pionowej (Tilt).

Konstrukcja jest idealnie dopasowana do najpopularniejszych mikroserwomechanizmów na rynku, takich jak **TowerPro SG90** oraz ich mocniejszych odpowiedników z metalowymi zębatkami – **MG90S**.
![Pan-Tilt](20260602_194717.jpg)

---

### Główne cechy i zalety
* **Dwuosiowa swoboda ruchu:** Pozwala na obrót lewo/prawo (oś Pan) oraz pochylenie góra/dół (oś Tilt), co pozwala kamerze na pełne "rozglądanie się" wokół robota.
* **Dedykowana platforma na kamerę:** Górna płytka montażowa posiada fabryczne otwory i sloty ułatwiające stabilne przykręcenie lub przypięcie małych modułów kamer (np. kamer FPV, płytek ESP32-CAM czy dedykowanych kamer do Raspberry Pi).
* **Niska waga i opływowy kształt:** Wykonanie z plastiku sprawia, że konstrukcja nie obciąża serwomechanizmów, co przekłada się na szybszą reakcję, mniejszy pobór prądu i dłuższą żywotność silników.
* **Stabilność mechaniczna:** Precyzyjnie spasowane elementy wtryskowe minimalizują tak zwany "luz międzyzębny" (backlash) na łączeniach, co stabilizuje obraz z kamery podczas ruchu.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Typ konstrukcji** | Pan-Tilt (2 osie swobody / 2-DOF) |
| **Materiał** | Tworzywo sztuczne (Nylon / ABS) |
| **Kompatybilne serwa** | 2x Mikroserwo 9g (SG90, MG90S, HXT900 itp.) |
| **Wymiary podstawy** | ok. 35 mm x 30 mm |
| **Wymiary platformy kamery**| ok. 28 mm x 28 mm |
| **Waga (bez serw)** | ok. 15 g |
| **Kolor** | Czarny |

---

### 🧱 Budowa zestawu i elementy montażowe

Zestaw dostarczany jest zazwyczaj w częściach do samodzielnego montażu (jako miniaturowy kit). W skład plastikowych elementów wchodzą:
1. **Podstawa (Base):** Element mocowany bezpośrednio do ramy robota (np. za pomocą nylonowych śrubek M3). Mieści w sobie dolne serwo (oś pozioma).
2. **Ramię pośrednie (Yoke/Bracket):** Element łączący dolne serwo z górnym. Obraca się w poziomie i trzyma w pionie drugie serwo.
3. **Platforma czołowa (Camera Bed):** Płytka, do której przykręca się kamerę, połączona bezpośrednio z orczykiem górnego serwa (oś pionowa).

*Uwaga: Do zmontowania całości wykorzystuje się plastikowe orczyki oraz wkręty dostarczane w komplecie razem z serwami SG90/MG90S.*

---

### 💡 Ważne wskazówki przedmontażowe

* **Elektroniczne centrowanie (90°):** Zanim skręcisz plastikowe ramiona uchwytu z serwami, podłącz serwa do Arduino i ustaw je programowo dokładnie w pozycji środkowej (`servo.write(90);`). Dopiero przy