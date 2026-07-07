## Adresy IP — Publiczny vs Prywatny

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

| Typ                                 | Do czego służy                           | Przykład      |
|-------------------------------------|------------------------------------------|---------------|
| <span class="hl-g">Publiczny</span> | Identyfikuje urządzenie w Internecie     | `89.64.12.44` |
| <span class="hl">Prywatny</span>    | Identyfikuje urządzenie w sieci lokalnej | `192.168.1.1` |

</div>

<div id="s03" class="section section">

<div class="section-header">

<span class="section-num-badge">03</span>


---

## Adres MAC

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Adres MAC to <span class="hl">unikalny identyfikator karty sieciowej</span> urządzenia.

<div class="code">

<span class="cm">Przykład adresu MAC:</span> <span class="ck">a4:c3:f0</span>:<span class="cv">85:ac:2d</span> └──────┘ └──────┘ <span class="cm">Pierwsze 6 znaków Ostatnie 6 znaków</span> <span class="cm">= firma producenta = unikalny numer urządzenia</span>

</div>

</div>

<div id="s04" class="section section">

<div class="section-header">

<span class="section-num-badge">04</span>


---

## Ping — ICMP

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Ping używa pakietów <span class="hl">ICMP (Internet Control Message Protocol)</span> do sprawdzenia wydajności połączenia między urządzeniami.

<div class="code">

<span class="cm">Pingowanie urządzenia 192.168.1.254:</span> <span class="cg">Wysłano: </span> 6 pakietów ICMP <span class="cg">Odebrano: </span> 6 pakietów <span class="cg">Utracono: </span> 0 pakietów <span class="ck">Średni czas:</span> <span class="cv">4.16 ms</span>

</div>

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**Do czego służy**Sprawdzenie czy połączenie z urządzeniem istnieje i czy jest niezawodne.

</div>

</div>

</div>

<div id="sosi" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## ARP — Address Resolution Protocol

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

ARP umożliwia urządzeniu <span class="hl">powiązanie adresu MAC z adresem IP</span> w sieci. Każde urządzenie przechowuje dziennik adresów MAC powiązanych z innymi urządzeniami — tzw. <span class="hl">pamięć podręczną ARP (ARP cache)</span>.

### Jak działa ARP?

<div class="flow">

<div class="fs">

Urządzenie A chce znaleźć MAC dla IP

</div>

<span class="fa">→</span>

<div class="fs">

ARP Request (broadcast do wszystkich)

</div>

<span class="fa">→</span>

<div class="fs">

Urządzenie z tym IP odpowiada

</div>

<span class="fa">→</span>

<div class="fs ok">

ARP Reply (zwraca swój MAC)

</div>

</div>

| Wiadomość                                   | Co robi                                                                             |
|---------------------------------------------|-------------------------------------------------------------------------------------|
| <span class="b b-yellow">ARP Request</span> | Broadcast do całej sieci: *"Jaki jest adres MAC właściciela tego IP?"*              |
| <span class="b b-green">ARP Reply</span>    | Odpowiedź od urządzenia z tym IP: *"To ja, mój MAC to..."* — zapisywany w ARP cache |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: ARP Spoofing / Poisoning**Atakujący może wysyłać fałszywe ARP Reply — podszywać się pod inny adres IP (np. bramę domyślną). To pozwala na atak MITM (Man-in-the-Middle). Warto znać ten protokół bo pojawia się w logach IDS.

</div>

</div>

</div>

<div id="sdhcp" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## DHCP — Dynamiczne Przydzielanie Adresów IP

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Adresy IP można przypisywać ręcznie (statycznie) lub automatycznie przez serwer <span class="hl">DHCP (Dynamic Host Configuration Protocol)</span>.

### Proces DHCP — 4 kroki (DORA)

<div class="flow">

<div class="fs">

DHCP Discover

</div>

<span class="fa">→</span>

<div class="fs">

DHCP Offer

</div>

<span class="fa">→</span>

<div class="fs">

DHCP Request

</div>

<span class="fa">→</span>

<div class="fs ok">

DHCP ACK

</div>

</div>

| Krok                                        | Kto wysyła  | Co się dzieje                                                               |
|---------------------------------------------|-------------|-----------------------------------------------------------------------------|
| <span class="b b-cyan">1 · Discover</span>  | Urządzenie  | Wysyła broadcast: "Czy jest jakiś serwer DHCP w sieci?"                     |
| <span class="b b-green">2 · Offer</span>    | Serwer DHCP | Odpowiada z propozycją adresu IP: "Możesz użyć 192.168.1.50"                |
| <span class="b b-yellow">3 · Request</span> | Urządzenie  | Potwierdza: "Chcę ten adres IP"                                             |
| <span class="b b-green">4 · ACK</span>      | Serwer DHCP | Finalnie potwierdza przydzielenie adresu — urządzenie może zacząć go używać |

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**Skrót: DORA**Discover → Offer → Request → ACK. Łatwy sposób żeby zapamiętać kolejność kroków.

</div>

</div>

</div>

<div id="stcp" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## Podsieciowanie (Subnetting)

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

Podsieciowanie = dzielenie jednej dużej sieci na mniejsze podsieci. <span class="dim">Analogia: kroisz ciasto — każdy dział firmy dostaje swój kawałek.</span>

### Trzy typy adresów w podsieci

| Typ adresu                               | Przykład                 | Analogia                                  | Co identyfikuje                      |
|------------------------------------------|--------------------------|-------------------------------------------|--------------------------------------|
| <span class="hl">Adres sieciowy</span>   | `192.168.1.0`            | "Adres bloku mieszkalnego"                | Całą sieć — nie konkretne urządzenie |
| <span class="hl-g">Adres hosta</span>    | `192.168.1.100`          | "Numer mieszkania"                        | Konkretne urządzenie w sieci         |
| <span class="hl-y">Domyślna brama</span> | `192.168.1.1` lub `.254` | "Portier przekazujący paczki na zewnątrz" | Router — wysyła ruch do innych sieci |

### Twoja sieć domowa jako przykład

<div class="code">

<span class="cm">192.168.1.0</span> → adres sieci <span class="cg">192.168.1.1</span> → router (domyślna brama = Twój Funbox Orange) <span class="ck">192.168.1.26</span> → Twój MacBook (adres hosta) <span class="cr">192.168.1.255</span> → broadcast (do wszystkich)

</div>

### Po co podsieciowanie?

| Powód                                    | Co daje                         |
|------------------------------------------|---------------------------------|
| <span class="hl-g">Efektywność</span>    | Mniejszy ruch w każdej podsieci |
| <span class="hl-g">Bezpieczeństwo</span> | Oddzielasz sieci od siebie      |
| <span class="hl-g">Kontrola</span>       | Wiesz co jest gdzie             |

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Przykład z życia — kawiarnia**Sieć 1 → pracownicy + kasy (prywatna) \| Sieć 2 → WiFi dla klientów (publiczna). Podsieciowanie = te dwie sieci są oddzielone, ale obie mają dostęp do internetu.

</div>

</div>

</div>

<div id="sfirewall" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
