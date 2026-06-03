

Wydajny moduł impulsowej przetwornicy DC-DC (Step-Down) oparty na kultowym i niezawodnym układzie **LM2596s**. Urządzenie pozwala na precyzyjne obniżenie napięcia wejściowego z zakresu do 40V do pożądanego napięcia wyjściowego, które reguluje się za pomocą wbudowanego potencjometru wieloobrotowego.

Głównym atutem tej wersji modułu jest **zintegrowany cyfrowy woltomierz LED** (trzycyfrowy wyświetlacz siedmiosegmentowy). Pozwala on na bieżąco monitorować napięcie wejściowe lub wyjściowe bez konieczności używania zewnętrznego multimetru.
![[20260602_194908.jpg|200]]

---

### Główne cechy i zalety
* **Wbudowany woltomierz LED:** Czytelny wyświetlacz pozwala na natychmiastowy podgląd napięcia. Za pomocą fizycznego przycisku na płytce można przełączać tryb wyświetlania między napięciem wejściowym (dioda LED IN) a wyjściowym (dioda LED OUT).
* **Możliwość wyłączenia wyświetlacza:** Przytrzymanie przycisku pozwala całkowicie wyłączyć woltomierz, co zmniejsza pobór prądu przez sam moduł.
* **Możliwość kalibracji woltomierza:** Jeśli wskazania wyświetlacza minimalnie różnią się od wskazań profesjonalnego miernika, moduł umożliwia ręczną kalibrację błędu pomiarowego.
* **Wysoka sprawność (do 92%):** Dzięki pracy impulsowej przetwornica wydziela znacznie mniej ciepła niż tradycyjne stabilizatory liniowe (np. z serii 78xx).
* **Złącza śrubowe (Terminal Block):** Umożliwiają pewny i szybki montaż przewodów bez konieczności lutowania.

---

### Specyfikacja techniczna

| Parametr | Wartość / Opis |
| :--- | :--- |
| **Układ sterujący** | LM2596s (przetwornica impulsowa buck) |
| **Napięcie wejściowe (IN)** | DC 4.0V - 40V |
| **Napięcie wyjściowe (OUT)** | DC 1.25V - 37V (płynna regulacja) |
| **Maksymalny prąd wyjściowy** | 2A (do 3A przy zastosowaniu dodatkowego radiatora) |
| **Dokładność woltomierza** | ± 0.05V |
| **Zakres pomiarowy woltomierza**| 0V - 40V |
| **Częstotliwość kluczowania** | 150 kHz |
| **Zabezpieczenia** | Przeciwzwarciowe, przed przegrzaniem |
| **Wymiary płytki** | 61 mm x 34 mm x 12 mm |

---

### Opis wyprowadzeń i elementów płytki

#### Złącza śrubowe:
* **IN+** – Plus napięcia wejściowego (zasilanie źródłowe, np. akumulator, zasilacz sieciowy).
* **IN-** – Minus napięcia wejściowego (GND).
* **OUT+** – Plus stabilizowanego napięcia wyjściowego (zasilanie odbiornika, np. Arduino).
* **OUT-** – Minus napięcia wyjściowego (GND).

#### Diody sygnalizacyjne:
* **IN (LED)** – Świeci, gdy wyświetlacz pokazuje aktualne napięcie na wejściu przetwornicy.
* **OUT (LED)** – Świeci, gdy wyświetlacz pokazuje aktualne napięcie na wyjściu przetwornicy.

---

### ⚠️ Instrukcja obsługi i ważne uwagi

1. **Zasada działania Step-Down:** Jest to przetwornica obniżająca napięcie. Oznacza to, że napięcie wejściowe **musi być wyższe** od pożądanego napięcia wyjściowego o co najmniej 1.5V. Moduł nie podniesie napięcia (np. z 5V nie zrobi 12V).
2. **Pierwsze uruchomienie (Kręcenie potencjometrem):** Nowe moduły prosto z fabryki mają często potencjometr ustawiony na maksymalną wartość. Jeśli po podłączeniu zasilania kręcisz śrubą, a napięcie wyjściowe się nie zmienia, **wykonaj nawet 10-20 pełnych obrotów w kierunku przeciwnym do ruchu wskazówek zegara (w lewo)**, aż napięcie zacznie spadać.
3. **Chłodzenie przy dużym obciążeniu:** Przy ciągłym poborze prądu powyżej **2A** lub przy dużej różnicy między napięciem wejściowym a wyjściowym, układ LM2596s zacznie się mocno nagrzewać. Wymagane jest wtedy naklejenie na niego małego radiatora aluminiowego.

---

### Zastosowanie
* Zasilanie mikrokontrolerów (Arduino, ESP32, Raspberry Pi) z akumulatorów samochodowych 12V lub ciężarowych 24V.
* Budowa prostego, warsztatowego zasilacza laboratoryjnego z regulacją napięcia.
* Obniżanie napięcia w instalacjach solarnych, modelach RC oraz systemach oświetlenia LED.
* Bezpieczne zasilanie wymagających układów elektronicznych ze źródeł o niestabilnym napięciu.