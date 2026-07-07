## Zapora Ogniowa (Firewall)

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Firewall to urządzenie w sieci które decyduje **co może wejść i wyjść z sieci**. Jak ochroniarz przy wejściu do klubu. Działa na <span class="hl">warstwie 3</span> (adresy IP) i <span class="hl">warstwie 4</span> (porty i protokoły TCP/UDP) modelu OSI.

### Na podstawie czego firewall przepuszcza lub blokuje ruch?

| Pytanie             | Co sprawdza                   |
|---------------------|-------------------------------|
| Skąd pochodzi ruch? | Adres IP źródłowy — warstwa 3 |
| Dokąd idzie ruch?   | Adres IP docelowy — warstwa 3 |
| Na jaki port?       | Nr portu (np. 80) — warstwa 4 |
| Jaki protokół?      | TCP czy UDP — warstwa 4       |

Firewall wykonuje <span class="hl-y">inspekcję pakietów</span> żeby odpowiedzieć na te pytania.

### Dwa rodzaje firewalli

<div class="cards">

<div class="card">

<div class="card-label">

🧠 Stateful (Stanowy)

</div>

Patrzy na **całe połączenie**, nie pojedynczy pakiet. Jest mądrzejszy, ale zużywa więcej zasobów. Jeśli jedno urządzenie zachowuje się źle → blokuje je **całkowicie**.

Analogia: ochroniarz który obserwuje całe Twoje zachowanie w klubie.

</div>

<div class="card">

<div class="card-label">

📋 Stateless (Bezstanowy)

</div>

Patrzy na **każdy pakiet osobno** według sztywnych reguł. Zużywa mniej zasobów, ale jest "głupszy" — jeśli reguła nie pasuje, pakiet przechodzi. Dobry przy atakach <span class="hl-r">DDoS</span>.

Analogia: bramkarz który sprawdza tylko dowód, nic więcej.

</div>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC Tip**Firewalle mogą być dedykowanym sprzętem (duże firmy) lub oprogramowaniem jak `Snort`. Kategoryzuje się je w 2 do 5 kategorii — najważniejsze to Stateful i Stateless.

</div>

</div>

</div>

<div id="sportfwd" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## Port Forwarding — Przekierowanie Portów

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Port forwarding to **niezbędny element łączenia usług z Internetem**. Bez niego aplikacje (np. serwer WWW) są dostępne <span class="hl-r">tylko w sieci lokalnej</span> (intranet).

### Jak to działa?

| Bez port forwardingu                             | Z port forwardingiem                                     |
|--------------------------------------------------|----------------------------------------------------------|
| Serwer `192.168.1.10:80` widoczny tylko lokalnie | Cały internet może dostać się przez publiczny IP routera |
| Nikt z zewnątrz nie może się dostać              | Router przekazuje ruch do właściwego urządzenia          |

### Przepływ danych

<div class="flow">

<span class="fs">Internet</span><span class="fa">→</span> <span class="fs">Router  
<span class="small">82.62.51.70:80</span></span><span class="fa">→</span> <span class="fs ok">Serwer  
<span class="small">192.168.1.10:80</span></span>

</div>

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Ważna różnica — Port Forwarding vs Firewall**  
**Port forwarding** = <span class="hl-g">otwiera</span> konkretny port (jak otwarcie drzwi)  
**Firewall** = <span class="hl-y">decyduje czy ruch może przejść</span> przez ten port (jak ochroniarz przy drzwiach)  
Port forwarding otwiera drzwi — firewall kontroluje kto przez nie przechodzi.

</div>

</div>

Port forwarding konfiguruje się na <span class="hl">routerze</span> sieci. Z zewnątrz nigdy nie widzisz prywatnego IP urządzenia — widzisz tylko publiczny IP routera.

</div>

<div id="svpn" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## VPN — Virtual Private Network

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

VPN to technologia która tworzy <span class="hl-g">szyfrowany tunel</span> między urządzeniami przez internet. Jakbyś miał prywatny, niewidoczny korytarz między dwoma miejscami. Urządzenia połączone tunelem tworzą własną sieć prywatną — mogą być częścią różnych sieci fizycznych ale razem tworzą jedną sieć VPN.

### Do czego służy VPN?

| Korzyść                                  | Opis                                                                                                                                     |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="hl-g">🏢 Łączy biura</span> | Pracownicy w różnych miastach mogą korzystać z tych samych zasobów firmowych (serwery, infrastruktura)                                   |
| <span class="hl">🔒 Prywatność</span>    | Dane są szyfrowane — można je zrozumieć tylko między nadawcą a odbiorcą. Przydatne na publicznym WiFi.                                   |
| <span class="hl-p">🕵️ Anonimowość</span> | Ukrywa ruch przed dostawcą internetu (ISP). Używają go dziennikarze i aktywiści. Uwaga: VPN który loguje Twoje dane = brak anonimowości! |

### Trzy technologie VPN

| Technologia                          | Co robi                                                                                                                                                                     | Wady                                        |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------|
| <span class="b b-yellow">PPP</span>  | Podstawa — uwierzytelnienie i szyfrowanie (klucz prywatny + certyfikat publiczny jak SSH). Nie może samodzielnie wyjść poza sieć — <span class="hl-r">nieroutowalny</span>. | Nie działa samodzielnie w internecie        |
| <span class="b b-orange">PPTP</span> | Rozbudowuje PPP — pozwala wyjść do internetu. Łatwy w konfiguracji, obsługiwany przez większość urządzeń.                                                                   | <span class="hl-r">Słabe szyfrowanie</span> |
| <span class="b b-green">IPSec</span> | Szyfruje dane używając istniejącego protokołu IP. Silne szyfrowanie, obsługiwany na wielu urządzeniach.                                                                     | Trudny w konfiguracji                       |

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**TryHackMe używa VPN**Dlatego możesz ćwiczyć hakowanie ich maszyn bezpiecznie — maszyny nie są wystawione na publiczny internet, a Twój ISP nie widzi że "atakujesz" inne maszyny.

</div>

</div>

</div>

<div id="sclientsrv" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
