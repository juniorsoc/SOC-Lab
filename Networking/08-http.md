## HTTP — Bezstanowość i Sesje

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Czym jest HTTP(S)?**HTTP(S) to protokół używany przez przeglądarkę do rozmowy z serwerem. Litera <span class="hl-g">S</span> = połączenie jest szyfrowane przez TLS. <span class="hl-y">Bezstanowy</span> = serwer traktuje każde żądanie jako nowe — nie pamięta że byłeś tu przed chwilą.

</div>

</div>

### Problem bezstanowości — jak go rozwiązano?

| Problem                                                 | Rozwiązanie                             | Jak działa                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Serwer nic nie pamięta — skąd wie że jesteś zalogowany? | <span class="hl">Sesje + Cookies</span> | Gdy się logujesz, serwer tworzy <span class="hl-g">identyfikator sesji</span> (unikalny kod), który zapisuje się w Twoim cookie. Przy każdym kolejnym żądaniu przeglądarka automatycznie wysyła ten kod — serwer "wie" kim jesteś. Bez tego musiałbyś logować się przy każdym kliknięciu. |

<div class="flow">

<div class="fs">

Login: user+hasło

</div>

<span class="fa">→</span>

<div class="fs">

Serwer tworzy Session ID

</div>

<span class="fa">→</span>

<div class="fs">

Cookie zapisane w przeglądarce

</div>

<span class="fa">→</span>

<div class="fs ok">

Każde kolejne żądanie wysyła cookie automatycznie

</div>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Session Hijacking**Atakujący kradnie Session ID z cookie ofiary — i uzyskuje dostęp do jej konta BEZ znajomości hasła. Szukaj w logach: jeden Session ID używany z dwóch różnych adresów IP w tym samym czasie = przejęcie sesji!

</div>

</div>

</div>

<div id="s07" class="section section">

<div class="section-header">

<span class="section-num-badge">07</span>


---

## Budowa URL

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

<div class="code">

<span class="cm">Przykład pełnego URL:</span> <span class="ck">http://</span><span class="cv">user:password</span>@<span class="cg">tryhackme.com</span><span class="ck">:80</span>/view-room<span class="cv">?id=1</span><span class="cr">\#task3</span>

</div>

| Część                                  | Przykład        | Co oznacza                                   |
|----------------------------------------|-----------------|----------------------------------------------|
| <span class="hl">Schemat</span>        | `http://`       | Język przeglądarki (HTTP, HTTPS, FTP)        |
| <span class="hl">Użytkownik</span>     | `user:password` | Login i hasło, jeśli strona tego wymaga      |
| <span class="hl">Host/Domena</span>    | `tryhackme.com` | Adres serwera                                |
| <span class="hl">Port</span>           | `:80`           | "Drzwi" serwera — HTTP=80, HTTPS=443         |
| <span class="hl">Ścieżka</span>        | `/view-room`    | Konkretna strona lub plik na serwerze        |
| <span class="hl">Ciąg zapytania</span> | `?id=1`         | Dodatkowe parametry (np. pokaż artykuł nr 1) |
| <span class="hl">Fragment</span>       | `#task3`        | Konkretne miejsce na stronie                 |

</div>

<div id="s08" class="section section">

<div class="section-header">

<span class="section-num-badge">08</span>


---

## Żądanie HTTP — Jak Wygląda

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

<div class="code">

<span class="ck">GET</span> / <span class="cv">HTTP/1.1</span> <span class="ck">Host:</span> tryhackme.com <span class="ck">User-Agent:</span> Mozilla/5.0 Firefox/87.0 <span class="ck">Referer:</span> https://tryhackme.com/

</div>

| Pole             | Co oznacza w SOC                                                         |
|------------------|--------------------------------------------------------------------------|
| `GET / HTTP/1.1` | Metoda + ścieżka + wersja protokołu                                      |
| `User-Agent`     | Jeśli to `python-requests` lub `curl` zamiast przeglądarki → podejrzane! |
| `Referer`        | Skąd przyszło żądanie — brak lub dziwna wartość może być sygnałem        |

</div>

<div id="s09" class="section section">

<div class="section-header">

<span class="section-num-badge">09</span>


---

## Odpowiedź HTTP — Jak Wygląda

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

<div class="code">

<span class="cv">HTTP/1.1</span> <span class="cg">200 OK</span> <span class="ck">Server:</span> nginx/1.15.8 <span class="ck">Content-Type:</span> text/html <span class="ck">Content-Length:</span> 98 <span class="cg">\<html\>...\</html\></span>

</div>

| Pole                   | Co oznacza w SOC                                              |
|------------------------|---------------------------------------------------------------|
| `HTTP/1.1 200 OK`      | Kod statusu — to co analizujesz najczęściej w logach          |
| `Server: nginx/1.15.8` | Wersja serwera — atakujący szuka przestarzałych wersji z CVE  |
| `Content-Type`         | Niezgodność typu (np. .jpg ale odpowiedź to exe) → podejrzane |

</div>

<div id="s10" class="section section">

<div class="section-header">

<span class="section-num-badge">10</span>


---

## Metody HTTP

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

| Metoda                              | Co robi                | Przykład z życia            | Analogia (biblioteka)            |
|-------------------------------------|------------------------|-----------------------------|----------------------------------|
| <span class="b b-cyan">GET</span>   | Pobiera dane z serwera | Wchodzisz na facebook.com   | "Pokaż mi tę książkę"            |
| <span class="b b-green">POST</span> | Wysyła nowe dane       | Logujesz się, rejestrujesz  | "Chcę dodać nową książkę"        |
| <span class="b b-yellow">PUT</span> | Aktualizuje dane       | Zmieniasz zdjęcie profilowe | "Chcę zmienić treść tej książki" |
| <span class="b b-red">DELETE</span> | Usuwa dane             | Usuwasz post lub konto      | "Usuń tę książkę"                |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Dlaczego ważne w SOC** Dużo `DELETE` od jednego IP → podejrzane!  ·  `POST` na logowanie 1000 razy → brute force!  ·  `PUT` na plik systemowy → ktoś próbuje nadpisać pliki! W logach widzisz metody i od razu wiesz co ktoś próbował zrobić.

</div>

</div>

</div>

<div id="s11" class="section section">

<div class="section-header">

<span class="section-num-badge">11</span>


---

## Kody Odpowiedzi HTTP

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

<div class="status-grid">

<div class="sc s2">

<div class="sc-num">

2xx

</div>

<div class="sc-title">

DOBRZE

</div>

<div class="dim" style="font-size:11px">

Żądanie wykonane pomyślnie

</div>

</div>

<div class="sc s3">

<div class="sc-num">

3xx

</div>

<div class="sc-title">

IDŹ TAM

</div>

<div class="dim" style="font-size:11px">

Zasób jest gdzie indziej

</div>

</div>

<div class="sc s4">

<div class="sc-num">

4xx

</div>

<div class="sc-title">

TWÓJ BŁĄD

</div>

<div class="dim" style="font-size:11px">

Coś nie tak po Twojej stronie

</div>

</div>

<div class="sc s5">

<div class="sc-num">

5xx

</div>

<div class="sc-title">

ICH BŁĄD

</div>

<div class="dim" style="font-size:11px">

Coś nie tak z serwerem

</div>

</div>

</div>

### Najważniejsze kody

| Kod                                 | Nazwa                 | Co oznacza                                         |
|-------------------------------------|-----------------------|----------------------------------------------------|
| <span class="b b-green">200</span>  | OK                    | Wszystko OK, strona działa                         |
| <span class="b b-green">201</span>  | Utworzono             | Coś nowego zostało stworzone (np. nowy użytkownik) |
| <span class="b b-cyan">301</span>   | Przeniesiony na stałe | Strona przeniesiona na nowy adres                  |
| <span class="b b-cyan">302</span>   | Znaleziono (tymcz.)   | Tymczasowe przekierowanie                          |
| <span class="b b-yellow">400</span> | Złe żądanie           | Coś brakuje w Twoim żądaniu                        |
| <span class="b b-yellow">401</span> | Nieautoryzowany       | Musisz się zalogować                               |
| <span class="b b-yellow">403</span> | Zabroniony            | Brak uprawnień nawet po logowaniu                  |
| <span class="b b-yellow">404</span> | Nie znaleziono        | Strona/plik nie istnieje                           |
| <span class="b b-yellow">405</span> | Metoda niedozwolona   | Zła metoda (np. GET zamiast POST)                  |
| <span class="b b-red">500</span>    | Błąd serwera          | Serwer nie poradził sobie z żądaniem               |
| <span class="b b-red">503</span>    | Usługa niedostępna    | Serwer przeciążony lub w konserwacji               |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Dlaczego ważne w SOC** Dużo `404` od jednego IP → ktoś skanuje stronę szukając plików!  ·  Dużo `401/403` → ktoś próbuje się włamać!  ·  Dużo `500` → może atak!

</div>

</div>

</div>

<div id="s12" class="section section">

<div class="section-header">

<span class="section-num-badge">12</span>


---

## Nagłówki HTTP

<span class="section-tag tag-web">Web</span>

</div>

<div class="section-divider">

</div>

### Nagłówki żądania (wysyłasz TY do serwera)

| Nagłówek                                | Co robi                                                                   |
|-----------------------------------------|---------------------------------------------------------------------------|
| <span class="hl">Host</span>            | Mówi której strony chcesz (jeden serwer hostuje wiele stron)              |
| <span class="hl">User-Agent</span>      | Mówi jaka przeglądarka/program wysyła żądanie (np. Firefox, curl, python) |
| <span class="hl">Content-Length</span>  | Ile danych wysyłasz (np. przy formularzu)                                 |
| <span class="hl">Accept-Encoding</span> | Jakie metody kompresji obsługuje Twoja przeglądarka                       |
| <span class="hl">Cookie</span>          | Dane które serwer wcześniej zapisał u Ciebie                              |

### Nagłówki odpowiedzi (serwer odsyła DO CIEBIE)

| Nagłówek                                   | Co robi                                         |
|--------------------------------------------|-------------------------------------------------|
| <span class="hl-g">Set-Cookie</span>       | Serwer zapisuje u Ciebie ciasteczko             |
| <span class="hl-g">Cache-Control</span>    | Jak długo przeglądarka ma pamiętać tę stronę    |
| <span class="hl-g">Content-Type</span>     | Co odsyła serwer (HTML, CSS, obrazek, PDF itp.) |
| <span class="hl-g">Content-Encoding</span> | Jaka kompresja została użyta na danych          |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Dlaczego ważne w SOC** `User-Agent: python-requests` → nie przeglądarka, może być skrypt/atak!  ·  Brak nagłówka `Host` → podejrzane  ·  Dziwne `Cookie` → może być kradzione ciasteczko (session hijack!)  ·  `Content-Type` niezgodny → ktoś może przesyłać złośliwe pliki!

</div>

</div>

</div>

<div id="s19" class="section section">

<div class="section-header">

<span class="section-num-badge">19</span>
