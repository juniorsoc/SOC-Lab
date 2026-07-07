## Operatory Bash — Przekierowania i Łączenie Komend

<span class="section-tag tag-linux">Linux</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">ℹ️</span>

<div class="callout-body">

**Dlaczego to ważne w SOC?**Operatory pozwalają zapisywać wyniki analiz do plików, budować złożone pipeline'y komend i automatyzować pracę z logami — kluczowe umiejętności każdego SOC Analityka.

</div>

</div>

### Operatory przekierowania wyjścia

| Operator                                                   | Zachowanie                                                                           | Przykład użycia                        | Zastosowanie w SOC                               |
|------------------------------------------------------------|--------------------------------------------------------------------------------------|----------------------------------------|--------------------------------------------------|
| <span class="b b-red" style="font-size:15px">\></span>     | <span class="hl-r">NISZCZY</span> poprzednią zawartość pliku i zapisuje nową         | `grep "ERROR" access.log > wyniki.txt` | Tworzenie czystego raportu od nowa               |
| <span class="b b-green" style="font-size:15px">\>\></span> | <span class="hl-g">ZACHOWUJE</span> poprzednią zawartość i dodaje nowe dane na końcu | `grep "FAILED" auth.log >> wyniki.txt` | Zbieranie wyników z wielu logów do jednego pliku |

<div class="code">

<span class="cm">\# \> NISZCZY — plik zaczyna od zera za każdym razem</span> <span class="ck">echo</span> <span class="cv">"Linia 1"</span> <span class="cr">\></span> raport.txt <span class="cm">\# raport.txt: "Linia 1"</span> <span class="ck">echo</span> <span class="cv">"Linia 2"</span> <span class="cr">\></span> raport.txt <span class="cm">\# raport.txt: TYLKO "Linia 2" — Linia 1 zniknęła!</span> <span class="cm">\# \>\> ZACHOWUJE — dane są dopisywane na końcu</span> <span class="ck">echo</span> <span class="cv">"Linia 1"</span> <span class="cg">\>\></span> raport.txt <span class="cm">\# raport.txt: "Linia 1"</span> <span class="ck">echo</span> <span class="cv">"Linia 2"</span> <span class="cg">\>\></span> raport.txt <span class="cm">\# raport.txt: "Linia 1" i "Linia 2"</span>

</div>

### Operatory łączenia komend

| Operator                                                 | Zachowanie                                                                                   | Przykład użycia             | Zastosowanie w SOC                                           |
|----------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------|--------------------------------------------------------------|
| <span class="b b-green" style="font-size:15px">&&</span> | Uruchom komendę 2 <span class="hl-g">TYLKO jeśli</span> komenda 1 się powiodła (exit code 0) | `mkdir raport && cd raport` | Bezpieczne sekwencje — nie kontynuuj jeśli coś się nie udało |
| <span class="b b-yellow" style="font-size:15px">&</span> | Uruchom komendę <span class="hl-y">W TLE</span> — wróć do terminala od razu                  | `tcpdump -w capture.pcap &` | Uruchamianie długich skanów/snifferów podczas dalszej pracy  |

<div class="code">

<span class="cm">\# && — command2 NIE uruchomi się jeśli command1 się nie powiódł</span> <span class="ck">mkdir</span> /tmp/analiza <span class="cg">&&</span> <span class="ck">cd</span> /tmp/analiza <span class="cm">\# Jeśli mkdir się nie powiedzie → cd NIE zostanie wykonane</span> <span class="ck">grep</span> <span class="cv">"CRITICAL"</span> /var/log/syslog <span class="cg">&&</span> <span class="ck">echo</span> <span class="cv">"⚠ Znaleziono incydenty!"</span> <span class="cm">\# Echo pojawi się TYLKO jeśli grep znalazł pasujące linie</span> <span class="cm">\# & — NIE czeka na zakończenie, działa w tle</span> <span class="ck">tcpdump</span> -i eth0 -w /tmp/ruch.pcap <span class="cv">&</span> <span class="ck">jobs</span> <span class="cm">\# pokaż procesy działające w tle</span> <span class="ck">fg</span> <span class="cm">\# przywróć ostatni proces z tła na pierwszy plan</span>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Praktyczny przykład łączenia operatorów** `grep "81.143.211.90" access.log > podejrzane_ip.txt && wc -l podejrzane_ip.txt`  
Zapisz wszystkie wpisy dla IP → jeśli się udało → policz ile ich jest

</div>

</div>

### Porównanie — szybka ściąga

| Operator                            | Pamięć podręczna                                          | Kiedy używać                                        |
|-------------------------------------|-----------------------------------------------------------|-----------------------------------------------------|
| <span class="b b-red">\></span>     | <span class="hl-r">Nadpisuję</span> — czysty start        | Tworzysz nowy raport, stare dane niepotrzebne       |
| <span class="b b-green">\>\></span> | <span class="hl-g">Dopisuję</span> — zachowuję historię   | Zbierasz dane z wielu źródeł do jednego pliku       |
| <span class="b b-green">&&</span>   | <span class="hl-g">Warunkowo</span> — tylko przy sukcesie | Sekwencja kroków gdzie każdy zależy od poprzedniego |
| <span class="b b-yellow">&</span>   | <span class="hl-y">W tle</span> — nie blokuję terminala   | Długie skany, sniffery, monitorowanie w tle         |

</div>

<div id="swincmd" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
