## Linux — Find, Grep, WC — Przeszukiwanie Logów

<span class="section-tag tag-linux">Linux</span>

</div>

<div class="section-divider">

</div>

### Polecenie FIND — szukanie plików

<div class="code">

<span class="ck">find</span> -name passwords.txt <span class="cm">\# szukaj pliku po dokładnej nazwie</span> <span class="ck">find</span> -name <span class="cv">\*.txt</span> <span class="cm">\# szukaj wszystkich plików .txt</span>

</div>

### Polecenie GREP — przeszukiwanie zawartości

| Komenda                              | Co robi                                                                         |
|--------------------------------------|---------------------------------------------------------------------------------|
| `grep "81.143.211.90" access.log`    | Szukaj konkretnego IP w logu                                                    |
| `grep "THM" access.log`              | Szukaj słowa / flagi THM                                                        |
| `grep -o "THM{.*}" access.log`       | Wyświetl <span class="hl-g">TYLKO</span> dopasowany fragment (np. samą flagę)   |
| `grep -c "81.143.211.90" access.log` | <span class="hl-y">Policz</span> liczbę wystąpień                               |
| `grep -n "81.143.211.90" access.log` | Pokaż <span class="hl-y">numery linii</span> gdzie znaleziono                   |
| `grep -R "PRETTY_NAME" /etc/`        | Szukaj <span class="hl-g">rekurencyjnie</span> we wszystkich plikach w katalogu |

### Polecenie WC — liczenie wpisów

<div class="code">

<span class="ck">wc</span> -l access.log <span class="cm">\# policz liczbę linii w pliku (= ile wpisów ma log)</span>

</div>

### Zastosowanie w SOC — przykłady z życia

<div class="code">

<span class="cm">\# Ile wpisów ma log?</span> <span class="ck">wc</span> -l access.log <span class="cm">\# Aktywność konkretnego IP</span> <span class="ck">grep</span> <span class="cv">"81.143.211.90"</span> access.log <span class="cm">\# Jakie strony odwiedzał atakujący? (7. kolumna = URL)</span> <span class="ck">grep</span> <span class="cv">"81.143.211.90"</span> access.log \| <span class="ck">awk</span> <span class="cv">'{print \$7}'</span> <span class="cm">\# Szukaj rekurencyjnie</span> <span class="ck">grep</span> -R <span class="cv">"szukana_wartość"</span> /ścieżka/do/katalogu/

</div>

### Format wpisu w access.log — jak czytać log serwera

<div class="code">

<span class="cr">81.143.211.90</span> - - \[<span class="cv">25/Mar/2021:11:17 +0000</span>\] "<span class="ck">GET / HTTP/1.1</span>" <span class="cg">200</span> 417

</div>

| Pole                                   | Przykład            | Co oznacza                                               |
|----------------------------------------|---------------------|----------------------------------------------------------|
| <span class="hl">Adres IP</span>       | `81.143.211.90`     | IP użytkownika lub atakującego                           |
| <span class="hl">Data i godzina</span> | `25/Mar/2021:11:17` | Kiedy nastąpiło zdarzenie                                |
| <span class="hl">Metoda + URL</span>   | `GET /strona`       | Co i skąd pobrał                                         |
| <span class="b b-green">200</span>     | Kod 200             | OK — strona zwrócona poprawnie                           |
| <span class="b b-yellow">404</span>    | Kod 404             | Nie znaleziono — atakujący szuka nieistniejących zasobów |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC Tip: Wykrywanie skanowania** Dużo żądań 404 z jednego IP w krótkim czasie = prawdopodobne skanowanie (directory brute-force). Sprawdź:  
`grep "81.143.211.90" access.log | grep " 404 " | wc -l`

</div>

</div>

</div>

<div id="sbash" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
