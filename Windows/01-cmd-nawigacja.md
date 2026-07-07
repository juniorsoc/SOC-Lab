## Terminal Windows — Nawigacja CMD

<span class="section-tag tag-os">Systemy</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Po co terminal na Windows?**Szybszy niż klikanie w foldery · Daje większą kontrolę · Wiele narzędzi security działa tylko z poziomu terminala · W SOC często pracujesz zdalnie przez CMD/PowerShell bez GUI.

</div>

</div>

### Podstawowe komendy CMD

| Komenda              | Co robi                                                        | Linux odpowiednik   |
|----------------------|----------------------------------------------------------------|---------------------|
| `cd`                 | Pokazuje aktualny folder                                       | `pwd`               |
| `cd nazwa_folderu`   | Wchodzi do podanego folderu                                    | `cd katalog/`       |
| `cd ..`              | Cofa się o jeden poziom wyżej                                  | `cd ..`             |
| `dir`                | Wyświetla zawartość bieżącego folderu                          | `ls`                |
| `dir /a`             | Wyświetla też <span class="hl-y">ukryte pliki i foldery</span> | `ls -al`            |
| `dir /s nazwa_pliku` | Szuka pliku we wszystkich podfolderach                         | `find / -name plik` |
| `type nazwa_pliku`   | Wyświetla zawartość pliku tekstowego                           | `cat plik.txt`      |

<div class="callout warn">

<span class="callout-icon">⚠️</span>

<div class="callout-body">

**Ukryty ≠ tajny**Windows domyślnie chowa niektóre pliki przed użytkownikiem, ale można je zobaczyć flagą `/a`. Atakujący często ukrywają złośliwe pliki — dlatego zawsze używaj `dir /a` podczas analizy.

</div>

</div>

### Jak znaleźć plik w CMD — krok po kroku

<div class="code">

<span class="cm">Krok 1 — Sprawdź gdzie jesteś:</span> <span class="ck">cd</span> <span class="cm">Krok 2 — Zobacz co jest w folderze:</span> <span class="ck">dir</span> <span class="cm">Krok 3 — Pokaż też ukryte pliki:</span> <span class="ck">dir</span> /a <span class="cm">Krok 4 — Wyszukaj plik na dysku:</span> <span class="ck">dir</span> /s task_brief.txt <span class="cm">Krok 5 — Przejdź do znalezionego folderu:</span> <span class="ck">cd</span> C:\Users\Administrator\Documents\Notes\\ <span class="cm">Krok 6 — Odczytaj plik:</span> <span class="ck">type</span> task_brief.txt

</div>

</div>

<div id="swininfo" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
