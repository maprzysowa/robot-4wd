
Niezwykle praktyczny kabel zasilający, który pozwala na zasilanie urządzeń elektronicznych wyposażonych w standardowe gniazdo **DC 5.5/2.1 mm** bezpośrednio z dowolnego portu USB. 

Przewód ten stanowi idealne uzupełnienie opisanego wcześniej *Modułu Zasilania Płytki Stykowej MB-102* oraz płytek Arduino (takich jak *UNO R4*), umożliwiając ich wygodne zasilanie z powerbanku, ładowarki do telefonu lub portu USB w komputerze bez konieczności używania dedykowanych, stacjonarnych zasilaczy sieciowych.
![Kabel](20260602_195124.jpg)

---

### Główne cechy i zalety
* **Uniwersalne źródło energii:** Możliwość uruchomienia urządzeń DC w warunkach polowych przy użyciu ogólnodostępnych powerbanków.
* **Standardowe złącza:** Najpopularniejszy na rynku wtyk DC 5.5/2.1 mm pasuje do większości routerów, modemów, mikrokontrolerów oraz zabawek.
* **Polaryzacja standardowa:** Plus w środku (center positive), co jest fabrycznym standardem w 95% urządzeń elektronicznych.
* **Optymalna długość:** Elastyczny przewód o długości zazwyczaj ok. 80-100 cm zapewnia wygodę podczas prototypowania na biurku lub wewnątrz ramy robota.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Złącze wejściowe** | USB Typ A (męskie) |
| **Złącze wyjściowe** | DC 5.5 mm / 2.1 mm (wtyk męski, baryłkowy) |
| **Napięcie wyjściowe** | DC 5V (dokładnie takie, jakie podaje port USB) |
| **Maksymalny prąd** | ok. 1A - 2A (zależny od wydajności prądowej portu źródłowego USB) |
| **Polaryzacja wtyku DC** | Plus (+) w środku, Minus (-) na zewnątrz |
| **Długość przewodu** | zazwyczaj ok. 80 cm - 1 m |
| **Kolor** | Czarny |

---

### ⚠️ Ważne uwagi dotyczące napięcia i wydajności

1. **Brak przetwornicy (Napięcie to zawsze 5V):** Jest to kabel bezpośredni (pasywny). Nie posiada wbudowanej przetwornicy podwyższającej napięcie. Jeśli podłączysz go do ładowarki USB (5V), na wtyku DC otrzymasz **dokładnie 5V**. 
   * *Uwaga:* Nie podłączaj tego kabla do urządzeń, które bezwzględnie wymagają zasilania 9V lub 12V (np. niektóre routery), ponieważ urządzenie nie uruchomi się lub będzie działać niestabilnie.
2. **Ograniczenia prądowe:** Maksymalny prąd, jaki można przesłać tym kablem, zależy od źródła. Tradycyjny port USB w komputerze (USB 2.0) dostarcza tylko 500mA (0.5A). Nowoczesne ładowarki sieciowe lub powerbanki potrafią podać od 2A do 3A, co w zupełności wystarczy do zasilenia logiki robota, ekranu LCD1602 oraz kilku czujników.

---

### Zastosowanie
* Zasilanie mikrokontrolerów Arduino (Uno, Mega) oraz kompatybilnych płytek bezpośrednio z powerbanku.
* Dostarczanie stabilnego zasilania 5V do modułu zasilacza płytki stykowej MB-102 przez dedykowane gniazdo DC.
* Zasilanie domowego sprzętu sieciowego (switche, niektóre modemy/routery 5V) podczas awarii prądu z wykorzystaniem powerbanku.
* Zasilanie taśm LED 5V, wentylatorów komputerowych (będą kręcić się wolniej niż przy 12V) oraz innych akcesoriów DIY.