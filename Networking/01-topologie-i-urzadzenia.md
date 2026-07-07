## Topologie Sieci

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

| Topologia                                  | Opis                                                        | Zalety                                       | Wady                                                                             |
|--------------------------------------------|-------------------------------------------------------------|----------------------------------------------|----------------------------------------------------------------------------------|
| <span class="hl">Gwiazda ★</span>          | Wszystkie urządzenia podłączone do centralnego switcha/huba | Niezawodna, łatwo dodać nowe urządzenia      | Droga (dużo kabli + sprzęt), jak padnie switch — pada cała sieć                  |
| <span class="hl-y">Magistrala (Bus)</span> | Wszystkie urządzenia na jednym kablu szkieletowym           | Tania i prosta w konfiguracji                | Wąskie gardło przy dużym ruchu, jeden zerwany kabel = koniec sieci               |
| <span class="hl-p">Pierścień</span>        | Urządzenia połączone w pętlę, dane krążą w jednym kierunku  | Mało okablowania, łatwe diagnozowanie błędów | Nieefektywna (dane odwiedzają każde urządzenie), jeden uszkodzony kabel = koniec |

### Switch i Router — różnica

| Urządzenie                            | Co robi                                                                                                                   | Gdzie stosowane                        |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| <span class="b b-cyan">Switch</span>  | Agreguje urządzenia w jednej sieci — inteligentny, wie który port to które urządzenie, wysyła dane tylko tam gdzie trzeba | Sieci firmowe, szkoły                  |
| <span class="b b-green">Router</span> | Łączy *różne sieci* ze sobą i przekazuje dane między nimi — tworzy ścieżkę dla danych żeby dotarły do celu                | Połączenie sieci lokalnej z internetem |

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**Dlaczego ważne w SOC?**Rozumiejąc topologię wiesz gdzie szukać problemu i jak interpretować ruch sieciowy (np. w tcpdump). Switche i routery można łączyć = większa redundancja (jak jedna ścieżka padnie, jest inna).

</div>

</div>

</div>

<div id="shub" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>


---

## Switch vs Hub — analogia

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

| Urządzenie                                            | Jak działa                                                                                                                                  | Problem                                            |
|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------|
| <span class="hl-r">Hub (stary, głupi)</span>          | Dostajesz paczkę dla Marka → hub wysyła ją do **każdego** w biurze i pyta "czy to dla ciebie?". Wszyscy muszą sprawdzić.                    | Chaos i wolno — zaśmieca sieć niepotrzebnym ruchem |
| <span class="hl-g">Switch (nowy, inteligentny)</span> | Dostajesz paczkę dla Marka → switch wie że Marek siedzi przy porcie nr 4 → wysyła **tylko do Marka**. Reszta nawet nie wie że coś przyszło. | Brak — efektywny                                   |

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Jak switch "uczy się"?**Switch zapamiętuje adresy MAC urządzeń podłączonych do każdego portu w tzw. tablicy MAC. Dzięki temu nie zaśmieca sieci niepotrzebnym ruchem — wysyła ramkę tylko na właściwy port.

</div>

</div>

</div>

<div id="s02" class="section section">

<div class="section-header">

<span class="section-num-badge">02</span>


---

## Router, Switch i VLAN

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

### 🔀 Router

Router to urządzenie które **łączy różne sieci** i przesyła dane między nimi. Działa na <span class="hl">warstwie 3</span> modelu OSI. Ma interfejs (stronę WWW lub konsolę) przez który administrator może konfigurować reguły takie jak port forwarding czy firewall.

<span class="hl-y">Routing</span> to **proces** (nie tylko urządzenie) — polega na tworzeniu ścieżki między sieciami żeby dane dotarły do celu. O wyborze trasy decydują <span class="hl-g">protokoły routingu</span> (np. OSPF, RIP) — nie robi tego router sam z siebie.

### Jak router wybiera trasę?

| Czynnik                                    | Opis                              |
|--------------------------------------------|-----------------------------------|
| <span class="hl-g">Najkrótsza droga</span> | Mniej urządzeń po drodze = lepiej |
| <span class="hl">Niezawodność</span>       | Która ścieżka rzadziej pada       |
| <span class="hl-y">Szybkość medium</span>  | Światłowód \> miedź               |

<div class="callout tip">

<span class="callout-icon">⚠️</span>

<div class="callout-body">

**Router ≠ Switch** — to różne urządzenia które nie zastępują się nawzajem. Router łączy różne sieci, switch łączy urządzenia w tej samej sieci.

</div>

</div>

### 🔌 Switch (Przełącznik)

Switch to urządzenie które **łączy wiele urządzeń w tej samej sieci** (od 3 do 63 urządzeń) za pomocą kabli Ethernet. Pakiety IP są opakowane w <span class="hl">ramki</span> (hermetyzacja) — switch operuje właśnie na ramkach.

|                  | Warstwa 2                                                             | Warstwa 3                                                          |
|------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------|
| **Jak działa**   | Wysyła ramki na podstawie <span class="hl">adresu MAC</span>          | Wysyła ramki na podstawie <span class="hl">MAC i IP</span>         |
| **Czy routuje?** | <span class="hl-r">❌ Nie</span> — wyłącznie wysyła ramki, nic więcej | <span class="hl-g">✅ Tak</span> — częściowo pełni funkcję routera |

⚠️ Switch warstwy 2 <span class="hl-r">nie może</span> działać jak warstwa 3 — to jednostronne! Switch warstwy 3 obsługuje wiele sieci jednocześnie (np. `192.168.1.1` i `192.168.2.1`).

### 🏢 VLAN — Virtual Local Area Network

VLAN to technologia która pozwala **wirtualnie rozdzielić** urządzenia w sieci — nawet jeśli są podłączone do tego samego switcha fizycznie. Nie trzeba kupować osobnego sprzętu — wystarczy konfiguracja.

Wszyscy w sieci z VLANem mogą korzystać z internetu, ale są <span class="hl-y">traktowani oddzielnie</span> — obowiązują reguły które kontrolują kto z kim może się komunikować.

<div class="cards">

<div class="card">

<div class="card-label">

Przykład z życia

</div>

Dział Sprzedaży i Dział Księgowości podłączone do **tego samego switcha**:  
✅ Obydwa mają internet  
❌ Nie mogą się ze sobą komunikować — dla bezpieczeństwa

</div>

<div class="card">

<div class="card-label">

Analogia

</div>

Mieszkańcy tego samego bloku — wszyscy używają tej samej bramy wejściowej, ale każdy ma zamknięte swoje mieszkanie. 🏠

</div>

</div>

</div>

<div id="shttpsession" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
