## Model OSI — 7 Warstw Sieci

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Model OSI (*Open Systems Interconnection*) to niezbędny model stosowany w sieciach — zapewnia ramy określające, w jaki sposób urządzenia sieciowe wysyłają, odbierają i interpretują dane. Dzięki niemu urządzenia różnych producentów mogą się ze sobą komunikować.

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**Enkapsulacja**Dane idą od warstwy 7 *w dół* do warstwy 1 przy wysyłaniu — każda warstwa dokłada swój nagłówek. Przy odbieraniu działa odwrotnie (dekapsulacja).

</div>

</div>

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Mnemonik 7→1**`All People Seem To Need Data Processing` — Application · Presentation · Session · Transport · Network · Data Link · Physical

</div>

</div>

### Warstwy — przegląd

| \#                                | Nazwa                                  | Co robi                                                                                                                                      | Przykłady                                  | SOC — ataki                         |
|-----------------------------------|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-------------------------------------|
| <span class="b b-purple">7</span> | <span class="hl-p">Aplikacji</span>    | Interfejs użytkownika — protokoły i reguły interakcji z danymi. Codzienne aplikacje: przeglądarki, klienci e-mail.                           | HTTP, HTTPS, DNS, FTP, GUI                 | XSS, SQLi, exploity aplikacji       |
| <span class="b b-yellow">6</span> | <span class="hl-y">Prezentacji</span>  | Tłumacz + ochroniarz. Tłumaczy formaty danych, szyfruje (TLS/SSL), kompresuje.                                                               | SSL/TLS, szyfrowanie, kompresja, kodowanie | Analiza certyfikatów, TLS downgrade |
| <span class="b b-cyan">5</span>   | <span class="hl">Sesji</span>          | Tworzy, utrzymuje i zamyka sesje. Sesje są unikalne. Zawiera punkty kontrolne przy utracie danych.                                           | NetBIOS, RPC, SMB sesje                    | Session hijacking, analiza sesji    |
| <span class="b b-green">4</span>  | <span class="hl-g">Transportu</span>   | TCP lub UDP — decyduje jak i z jaką gwarancją dane są przesyłane między urządzeniami.                                                        | TCP (niezawodny), UDP (szybki)             | Port scanning, DoS/flood            |
| <span class="b b-cyan">3</span>   | <span class="hl">Sieciowa</span>       | Routing pakietów — GPS dla danych. Wybiera optymalną trasę. Używa adresów IP. Routery = urządzenia warstwy 3.                                | IP, OSPF, RIP, routery                     | IP spoofing, TTL manipulation       |
| <span class="b b-orange">2</span> | <span class="hl-o">Łącza Danych</span> | Fizyczne adresowanie — dodaje adres MAC do pakietu. Każda karta sieciowa (NIC) ma unikalny MAC wypalony przez producenta (można sfałszować). | MAC, Ethernet, switche, NIC                | ARP spoofing, MAC flooding, MITM    |
| <span class="b b-red">1</span>    | <span class="hl-r">Fizyczna</span>     | Kable i sygnały — rzeczywista transmisja bitów przez medium fizyczne.                                                                        | Ethernet, WiFi, światłowód, miedź          | Fizyczny dostęp, podsłuch kabla     |

### Warstwa 4 — TCP vs UDP

|                  | <span class="hl-g">TCP</span>                         | <span class="hl-y">UDP</span>               |
|------------------|-------------------------------------------------------|---------------------------------------------|
| **Niezawodność** | ✅ Gwarantuje dostarczenie, sprawdza błędy, kolejność | ❌ Brak gwarancji — pakiet może nie dotrzeć |
| **Szybkość**     | Wolniejszy (więcej procesów)                          | ✅ Znacznie szybszy                         |
| **Połączenie**   | Stałe (3-way handshake)                               | Brak — wysyła i zapomina                    |
| **Zastosowanie** | WWW, e-mail, pobieranie plików                        | Streaming, gry online, DNS, ARP, DHCP       |

### Warstwa 3 — jak działa routing

<div class="flow">

<div class="fs">

Dane → pakiety

</div>

<span class="fa">→</span>

<div class="fs">

Naklejony IP odbiorcy

</div>

<span class="fa">→</span>

<div class="fs">

Router sprawdza IP

</div>

<span class="fa">→</span>

<div class="fs">

Wybiera trasę

</div>

<span class="fa">→</span>

<div class="fs ok">

Pakiety złożone u celu

</div>

</div>

Router wybiera trasę wg: 🔢 liczby urządzeń po drodze (mniej = lepiej) · ✅ niezawodności · ⚡ szybkości łącza (światłowód \> miedź). Protokoły routingu: `OSPF` i `RIP`.

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Warstwy a ataki**Warstwy 1–4 (dolne) = ataki sieciowe: skanowanie portów, ARP spoofing, IP spoofing, DoS/flood. Warstwy 5–7 (górne) = ataki aplikacyjne: XSS, SQLi, session hijacking, exploity na poziomie aplikacji.

</div>

</div>

</div>

<div id="spackets" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## Pakiety i Ramki w Sieci Komputerowej

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

To małe kawałki danych, które razem tworzą większą wiadomość — jak puzzle składające się w obrazek.

### Pakiet vs Ramka — jaka różnica?

| Typ                             | Warstwa OSI                                           | Co zawiera                                                               | Analogia                           |
|---------------------------------|-------------------------------------------------------|--------------------------------------------------------------------------|------------------------------------|
| <span class="hl">Pakiet</span>  | <span class="b b-cyan">Layer 3</span> — Sieciowa      | Adres IP nadawcy i odbiorcy — właściwa "treść" przesyłanych danych       | 📄 List w środku koperty           |
| <span class="hl-g">Ramka</span> | <span class="b b-green">Layer 2</span> — Łącza danych | "Opakowanie" dla pakietu — zawiera adresy MAC (fizyczne adresy urządzeń) | ✉️ Koperta — mówi gdzie dostarczyć |

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Prosta zasada** Mówimy o adresach IP → mówimy o **pakietach**  
Mówimy o adresach MAC → mówimy o **ramkach**

</div>

</div>

### Dlaczego małe kawałki, a nie całość?

Wyobraź sobie że pobierasz zdjęcie kota — nie przychodzi ono w całości, tylko w małych kawałkach, które komputer składa z powrotem w całość. Zaleta: mniejsze ryzyko "zakorkowania" sieci.

### Ważne nagłówki pakietu IP

| Nagłówek                                 | Co robi po ludzku                                                                       |
|------------------------------------------|-----------------------------------------------------------------------------------------|
| <span class="hl-y">Time to Live</span>   | "Termin ważności" pakietu — jeśli błądzi za długo, jest usuwany żeby nie zapychał sieci |
| <span class="hl">Checksum</span>         | Sprawdza czy dane nie zostały uszkodzone po drodze                                      |
| <span class="hl-g">Adres źródłowy</span> | Skąd pakiet pochodzi (żeby odpowiedź wróciła)                                           |
| <span class="hl-g">Adres docelowy</span> | Dokąd pakiet ma trafić                                                                  |

</div>

<div id="sarp" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
