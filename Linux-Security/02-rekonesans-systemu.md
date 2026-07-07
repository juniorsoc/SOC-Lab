## Linux — Rekonesans Systemu (whoami, uname, df)

<span class="section-tag tag-linux">Linux</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Po co to robimy?**Przed analizą incydentu analityk zawsze najpierw sprawdza podstawowe informacje o systemie — kim jest, jaki system, ile miejsca. To samo co na Windows, tylko inne komendy.

</div>

</div>

| Komenda               | Co sprawdza                                | Przykładowy wynik                            |
|-----------------------|--------------------------------------------|----------------------------------------------|
| `whoami`              | Twoja aktualna nazwa użytkownika           | `ubuntu`                                     |
| `uname -a`            | Pełne info o systemie i jądrze             | `Linux tryhackme 6.x.x-aws x86_64 GNU/Linux` |
| `uname`               | Tylko nazwa systemu                        | `Linux`                                      |
| `df -h`               | Stan dysków czytelnie (h = human readable) | Rozmiary jako 2G, 500M zamiast bajtów        |
| `cat /etc/os-release` | Info o dystrybucji Linuxa                  | `PRETTY_NAME="Ubuntu 24.04.1 LTS"`           |

### Rozkład wyniku uname -a

<div class="code">

<span class="ck">uname</span> -a <span class="cg">Linux</span> <span class="cv">tryhackme</span> <span class="ck">6.x.x-aws</span> \#17-Ubuntu <span class="cv">x86_64</span> GNU/Linux │ │ │ │ │ │ │ └── architektura (64-bit) │ │ └── wersja jądra │ └── hostname (nazwa komputera w sieci) └── system działa na jądrze Linux

</div>

### Rozkład wyniku df -h

| Kolumna                            | Co oznacza                                            |
|------------------------------------|-------------------------------------------------------|
| <span class="hl">Filesystem</span> | Nazwa systemu plików / dysku                          |
| <span class="hl">Size</span>       | Całkowity rozmiar                                     |
| <span class="hl">Used</span>       | Ile zajęte                                            |
| <span class="hl">Avail</span>      | Ile wolnego miejsca                                   |
| <span class="hl">Use%</span>       | Procent zajętości                                     |
| <span class="hl">Mounted on</span> | Gdzie dysk jest zamontowany (/ = główny dysk systemu) |

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**/etc — katalog konfiguracyjny**Katalog `/etc` przechowuje pliki konfiguracyjne całego systemu. Prawie każdy program trzyma tu swoje ustawienia. Klucz `cd /etc && ls` — zobaczysz dziesiątki plików jak `hosts`, `fstab`, `resolv.conf`.

</div>

</div>

### Ukryte pliki w Linux

Pliki i foldery zaczynające się od <span class="hl">.</span> (kropki) są ukryte. `ls` ich nie pokaże — musisz użyć `ls -al`.

<div class="code">

<span class="ck">ls</span> <span class="cm">\# nie pokaże .research/ ani .bashrc</span> <span class="ck">ls</span> -al <span class="cm">\# pokaże WSZYSTKIE pliki i foldery, też ukryte</span> <span class="cm">\# Jak wejść do ukrytego folderu:</span> <span class="ck">find</span> ~ -name plik.txt <span class="cm">\# zwraca pełną ścieżkę: /home/ubuntu/Documents/.research/plik.txt</span> <span class="ck">cd</span> /home/ubuntu/Documents/.research/ <span class="cm">\# cd do FOLDERU (bez nazwy pliku!)</span> <span class="ck">cat</span> plik.txt <span class="cm">\# cat czyta PLIK — nigdy nie rób cd na .txt</span>

</div>

### Szukanie plików bez błędów uprawnień

<div class="code">

<span class="ck">find</span> / -name plik.txt <span class="cv">2\>/dev/null</span> <span class="cm">\# 2\>/dev/null = wyrzuć błędy uprawnień (Permission denied) do kosza</span> <span class="cm">\# Dzięki temu widzisz tylko wyniki, a nie masa czerwonych błędów</span>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Kolejność rekonesansu na nieznanym systemie Linux**`whoami` → kim jestem · `uname -a` → jaki system · `df -h` → stan dysków · `cat /etc/os-release` → dystrybucja · `ls -al /tmp/` → podejrzane pliki

</div>

</div>

</div>

<div id="sfind" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
