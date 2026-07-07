## Model Klient-Serwer

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Analogia: Pizza**Ty (Alice) dzwonisz do pizzerii (Luigi's) przez telefon (sieć). Ty = klient, pizzeria = serwer. <span class="hl-g">Klient zawsze inicjuje żądanie — serwer tylko odpowiada.</span>

</div>

</div>

| Pojęcie                          | Co to jest                                                                                                                                 | Przykład                           |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
| <span class="hl">Klient</span>   | Urządzenie/aplikacja inicjująca żądanie                                                                                                    | Przeglądarka, aplikacja mobilna    |
| <span class="hl">Serwer</span>   | System obsługujący żądania i zwracający odpowiedzi                                                                                         | Serwer WWW, serwer poczty          |
| <span class="hl">Protokół</span> | Zestaw zasad komunikacji — wspólny język obu stron. Określa jakie polecenia są rozumiane, jak zbudować żądanie i jakie odpowiedzi zwracać. | HTTP, FTP, SSH, SMTP               |
| <span class="hl">Port</span>     | "Drzwi wejściowe" do konkretnej usługi na serwerze. Jeden serwer może mieć wiele usług — każda słucha na innym porcie.                     | HTTP=80, HTTPS=443, SSH=22, DNS=53 |
| <span class="hl">DNS</span>      | Tłumaczy nazwę domeny na adres IP — jak GPS zamieniający nazwę miejsca na współrzędne.                                                     | google.com → 142.250.74.46         |
| <span class="hl">Adres IP</span> | Unikalny adres serwera w sieci — "adres domowy" serwera                                                                                    | `192.168.1.1`, `8.8.8.8`           |

<div class="flow">

<div class="fs">

Klient

</div>

<span class="fa">→ protokół →</span>

<div class="fs">

żądanie na port

</div>

<span class="fa">→</span>

<div class="fs">

Serwer

</div>

<span class="fa">→</span>

<div class="fs ok">

odpowiedź

</div>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: To zawsze klient inicjuje połączenie, nigdy serwer.**Jeśli widzisz w logach że serwer nagle sam "nawiązuje połączenie" do zewnętrznego IP — to sygnał reverse shell lub Command & Control (C2) złośliwego oprogramowania!

</div>

</div>

</div>

<div id="srouterswitch" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
