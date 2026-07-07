## Rekordy DNS

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

| Rekord                              | Do czego służy                |
|-------------------------------------|-------------------------------|
| <span class="b b-cyan">A</span>     | Adres IPv4 strony             |
| <span class="b b-cyan">AAAA</span>  | Adres IPv6 strony             |
| <span class="b b-cyan">CNAME</span> | Przekierowanie na inną domenę |
| <span class="b b-cyan">MX</span>    | Serwer obsługujący e-maile    |
| <span class="b b-cyan">TXT</span>   | Weryfikacja i antyspam        |

</div>

<div id="s06" class="section section">

<div class="section-header">

<span class="section-num-badge">06</span>


---

## Jak Działa DNS — Krok po Kroku

<span class="section-tag tag-net">Sieci</span>

</div>

<div class="section-divider">

</div>

<div class="flow">

<div class="fs">

Ty

</div>

<span class="fa">→</span>

<div class="fs">

Pamięć komputera

</div>

<span class="fa">→</span>

<div class="fs">

Serwer DNS ISP

</div>

<span class="fa">→</span>

<div class="fs">

Root DNS

</div>

<span class="fa">→</span>

<div class="fs">

Serwer TLD

</div>

<span class="fa">→</span>

<div class="fs">

Serwer domeny

</div>

<span class="fa">→</span>

<div class="fs ok">

✓ Odpowiedź

</div>

</div>

### Szczegóły kroków

| Krok                             | Co się dzieje                                                                                                                                      |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="b b-cyan">1</span>  | **Twój komputer sprawdza pamięć podręczną** — pyta siebie: "Czy już byłem na tej stronie?". Jeśli tak — od razu zna adres. Jeśli nie — pyta dalej. |
| <span class="b b-cyan">2</span>  | **Pyta serwer DNS twojego dostawcy** (np. Orange, Play). On też ma swoją pamięć podręczną. Jeśli zna — odsyła. Jeśli nie — szuka dalej.            |
| <span class="b b-cyan">3</span>  | **Pyta Root DNS** — "szef wszystkich serwerów". Nie zna adresu, ale wie gdzie szukać. Mówi: "Chcesz .com? Idź do serwera TLD dla .com".            |
| <span class="b b-cyan">4</span>  | **Pyta serwer TLD** — obsługuje konkretną końcówkę, np. .com. Mówi: "tryhackme.com? Zapytaj serwer Cloudflare".                                    |
| <span class="b b-green">5</span> | **Odpowiedź wraca do Ciebie** — serwer autorytatywny podaje prawdziwy IP. Odpowiedź jest zapamiętywana na czas TTL.                                |

### Rekurencyjny vs Autorytatywny DNS

| Typ                                         | Analogia                           | Rola                                                                                        |
|---------------------------------------------|------------------------------------|---------------------------------------------------------------------------------------------|
| <span class="hl-y">Rekurencyjny DNS</span>  | Asystent który biega i pyta        | Szuka odpowiedzi w Twoim imieniu                                                            |
| <span class="hl-g">Autorytatywny DNS</span> | Właściciel książki z odpowiedziami | Zna oficjalną prawdziwą odpowiedź — właściciel strony wpisał tu rekordy (A, MX, CNAME itp.) |

</div>

<div id="ssub" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
