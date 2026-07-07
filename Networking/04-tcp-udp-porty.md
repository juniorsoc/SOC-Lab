## TCP — Transmission Control Protocol

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

TCP to zestaw zasad przesyłania danych w sieci. **Najważniejsza cecha:** TCP najpierw nawiązuje połączenie, a dopiero potem wysyła dane — dzięki temu <span class="hl-g">gwarantuje że dane dotrą do odbiorcy</span>.

### Zalety i wady TCP

| ✅ Zalety                              | ❌ Wady                                                       |
|----------------------------------------|---------------------------------------------------------------|
| Gwarantuje że dane dotrą w całości     | Jeśli jeden kawałek się zgubi, trzeba wysłać wszystko od nowa |
| Dane docierają we właściwej kolejności | Wolne połączenie spowalnia cały transfer                      |
| Sprawdza czy dane nie są uszkodzone    | Wolniejszy niż UDP — wykonuje więcej obliczeń                 |

### Nagłówki pakietu TCP

| Nagłówek                                      | Co to znaczy po ludzku                                                                         |
|-----------------------------------------------|------------------------------------------------------------------------------------------------|
| <span class="hl">Port źródłowy</span>         | Losowo wybrany "wyjazd" danych z urządzenia nadawcy (numer od 0 do 65535)                      |
| <span class="hl">Port docelowy</span>         | "Wejście" na urządzeniu odbiorcy — np. port 80 to strona internetowa, nie jest losowy          |
| <span class="hl-g">Numer sekwencji</span>     | Losowy numer nadany pierwszemu kawałkowi danych — żeby złożyć wszystko we właściwej kolejności |
| <span class="hl-g">Numer potwierdzenia</span> | Numer poprzedniego kawałka + 1 — odbiorca mówi "dostałem, czekam na następny"                  |
| <span class="hl-y">Suma kontrolna</span>      | Matematyczne sprawdzenie czy dane nie zostały uszkodzone po drodze                             |
| <span class="hl-p">Flaga</span>               | Mówi urządzeniu jak ma obsłużyć pakiet (SYN, ACK, FIN, RST — patrz niżej)                      |
| <span class="dim">Dane</span>                 | Właściwa treść — bajty przesyłanego pliku                                                      |

### Trójstronny uścisk dłoni — nawiązywanie połączenia

| Krok | Skrót                                  | Co to znaczy                                                               |
|------|----------------------------------------|----------------------------------------------------------------------------|
| 1    | <span class="b b-cyan">SYN</span>      | Klient mówi: "Hej, chcę się połączyć, oto mój numer startowy"              |
| 2    | <span class="b b-green">SYN/ACK</span> | Serwer odpowiada: "Słyszę cię, zgoda, oto mój numer startowy"              |
| 3    | <span class="b b-green">ACK</span>     | Klient potwierdza: "Dobra, zaczynamy wysyłać dane!"                        |
| 4    | <span class="b b-yellow">DANE</span>   | Właściwe dane lecą przez sieć                                              |
| 5    | <span class="b b-purple">FIN</span>    | Jedno urządzenie mówi: "Skończyłem, zamykam połączenie"                    |
| —    | <span class="b b-red">RST</span>       | Nagłe zerwanie połączenia — coś poszło bardzo nie tak (błąd, brak zasobów) |

<div class="flow">

<span class="fs">SYN</span><span class="fa">→</span> <span class="fs">SYN/ACK</span><span class="fa">→</span> <span class="fs">ACK</span><span class="fa">→</span> <span class="fs ok">DANE</span><span class="fa">→</span> <span class="fs">FIN</span>

</div>

### Numery sekwencji — jak działa kolejność?

<div class="code">

<span class="cm">\# Klient zaczyna od 0</span> Klient: <span class="cg">0</span> → <span class="cg">1</span> → <span class="cg">2</span> → ... <span class="cm">\# Serwer może zacząć od innego numeru</span> Serwer: <span class="ck">5000</span> → <span class="ck">5001</span> → <span class="ck">5002</span> → ...

</div>

Dzięki numerom sekwencji odbiorca zawsze składa dane we właściwej kolejności — nawet jeśli przychodziły w złej.

### Zamykanie połączenia (4 kroki)

| Krok                                                                               | Co się dzieje          |
|------------------------------------------------------------------------------------|------------------------|
| 1\. Alice → <span class="b b-purple">FIN</span>                                    | "Skończyłam wysyłać"   |
| 2\. Bob → <span class="b b-green">ACK</span> + <span class="b b-purple">FIN</span> | "Dobra, ja też kończę" |
| 3\. Alice → <span class="b b-green">ACK</span>                                     | "Zamknięte, pa!"       |

</div>

<div id="sudp" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## UDP — User Datagram Protocol

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

UDP to drugi sposób przesyłania danych w sieci, obok TCP. Główna różnica: <span class="hl-r">UDP nie nawiązuje połączenia</span> przed wysłaniem danych — po prostu je wysyła i tyle.

### UDP vs TCP — kluczowa różnica

<div class="cards">

<div class="card">

<div class="card-label">

TCP

</div>

📮 Jak **list polecony** — masz pewność że dotrze i jest potwierdzenie odbioru

</div>

<div class="card">

<div class="card-label">

UDP

</div>

🗞️ Jak **ulotka wrzucona do skrzynki** — może dojdzie, może nie, nieważne

</div>

</div>

### Zalety i wady UDP

| ✅ Zalety                                          | ❌ Wady                                    |
|----------------------------------------------------|--------------------------------------------|
| Znacznie szybszy niż TCP                           | Nie sprawdza czy dane dotarły              |
| Nie rezerwuje ciągłego połączenia                  | Niestabilne połączenie = fatalne działanie |
| Aplikacja sama decyduje jak szybko wysyłać pakiety | Brak zabezpieczeń takich jak w TCP         |

### Kiedy używa się UDP?

Tam gdzie <span class="hl-g">szybkość jest ważniejsza niż dokładność</span>: streaming wideo (YouTube, Netflix), gry online, rozmowy głosowe (Messenger, Teams). Jeśli zgubi się kilka klatek wideo — nie ma tragedii. Gdyby to był TCP, czekałbyś na ponowne wysłanie każdego zagubionego kawałka.

### Nagłówki pakietu UDP

| Nagłówek                                     | Co to znaczy po ludzku                                                                  |
|----------------------------------------------|-----------------------------------------------------------------------------------------|
| <span class="hl-y">Time to Live (TTL)</span> | "Termin ważności" pakietu — jeśli błądzi za długo, jest usuwany żeby nie zapychał sieci |
| <span class="hl-g">Źródło IP</span>          | Adres IP urządzenia które wysyła dane                                                   |
| <span class="hl-g">Cel IP</span>             | Adres IP urządzenia które ma odebrać dane                                               |
| <span class="hl">Port źródłowy</span>        | Losowo wybrany "wyjazd" danych z urządzenia nadawcy                                     |
| <span class="hl">Port docelowy</span>        | "Wejście" na urządzeniu odbiorcy — np. port 80 to strona internetowa                    |
| <span class="dim">Dane</span>                | Właściwa treść — bajty przesyłanego pliku                                               |

### Jak wygląda połączenie UDP vs TCP?

<div class="code">

<span class="cm">\# TCP — 3 kroki zanim cokolwiek poleci</span> <span class="ck">TCP:</span> SYN → SYN/ACK → ACK → <span class="cg">dane</span> <span class="cm">\# UDP — od razu, bez gadania 🚀</span> <span class="cv">UDP:</span> dane → dane → dane

</div>

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**Brak potwierdzenia w UDP**Nikt nie mówi "dostałem" — dane lecą i tyle. Brak trójstronnego uścisku dłoni oznacza zerowy narzut na nawiązywanie połączenia, co czyni UDP idealnym do zastosowań real-time.

</div>

</div>

</div>

<div id="sports" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## Porty Sieciowe

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Port to liczba od <span class="hl">0 do 65535</span>. Wyobraź sobie port morski — różne statki cumują przy różnych nabrzeżach. Każda aplikacja ma swoje "nabrzeże" przez które wymienia dane. Porty 0–1024 to <span class="hl-y">porty wspólne</span> — zarezerwowane dla najpopularniejszych protokołów.

### Najważniejsze porty

| Port                                 | Skrót | Pełna nazwa                 | Co robi po ludzku                                         |
|--------------------------------------|-------|-----------------------------|-----------------------------------------------------------|
| <span class="b b-cyan">21</span>     | FTP   | File Transfer Protocol      | Pobieranie i wysyłanie plików z serwera                   |
| <span class="b b-green">22</span>    | SSH   | Secure Shell                | Bezpieczne logowanie do systemu przez terminal            |
| <span class="b b-yellow">80</span>   | HTTP  | HyperText Transfer Protocol | Zwykłe strony internetowe (bez szyfrowania)               |
| <span class="b b-green">443</span>   | HTTPS | HTTP Secure                 | Strony internetowe z szyfrowaniem (kłódka w przeglądarce) |
| <span class="b b-orange">445</span>  | SMB   | Server Message Block        | Udostępnianie plików i drukarek w sieci lokalnej          |
| <span class="b b-purple">3389</span> | RDP   | Remote Desktop Protocol     | Zdalne sterowanie komputerem z graficznym pulpitem        |

### Czy można zmienić port?

Tak — technicznie możesz uruchomić stronę internetową na porcie `8080` zamiast standardowego `80`. Ale wtedy przeglądarka nie znajdzie jej automatycznie — trzeba podać port ręcznie:

<div class="code">

http://strona.pl:<span class="cv">8080</span>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC Tip: Niestandarowe porty**Usługi działające na niestandardowych portach (np. SSH na 2222, RDP na 3390) mogą być próbą ukrycia się przed prostymi skanerami. Warto monitorować ruch na nieoczekiwanych portach.

</div>

</div>

</div>

<div id="s05" class="section section">

<div class="section-header">

<span class="section-num-badge">05</span>
