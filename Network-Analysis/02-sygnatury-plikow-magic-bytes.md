## Sygnatury Plików — Magic Bytes

<span class="section-tag tag-soc">SOC</span>

</div>

<div class="section-divider">

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Atak: zmiana rozszerzenia pliku** Atakujący wysyła plik `zdjecie.jpg` → sprawdzasz pierwsze bajty HEX → widzisz <span class="hl-r" style="font-family:var(--mono)">4D 5A</span> → to ukryty <span class="hl-r" style="font-family:var(--mono)">.EXE</span> — ALARM!

</div>

</div>

| Sygnatura HEX                                                                  | Typ pliku                            | Znaczenie w SOC                                            |
|--------------------------------------------------------------------------------|--------------------------------------|------------------------------------------------------------|
| <span class="hl-r" style="font-family:var(--mono);font-size:13px">4D 5A</span> | <span class="b b-red">.EXE</span>    | ⚠️ Plik wykonywalny — najczęściej złośliwe oprogramowanie! |
| `FF D8 FF`                                                                     | <span class="b b-cyan">.JPG</span>   | Malware ukryty w zdjęciu? Sprawdź!                         |
| `89 50 4E 47`                                                                  | <span class="b b-cyan">.PNG</span>   | Zweryfikuj czy to naprawdę obrazek                         |
| `25 50 44 46`                                                                  | <span class="b b-yellow">.PDF</span> | Złośliwe PDF zdarzają się często                           |
| `50 4B 03 04`                                                                  | <span class="b b-green">.ZIP</span>  | Archiwum może zawierać ukryty malware                      |

### Narzędzia do pracy z HEX

| Narzędzie                         | Do czego                                 | Jak użyć                               |
|-----------------------------------|------------------------------------------|----------------------------------------|
| <span class="hl">CyberChef</span> | Dekoduje wszystko — HEX, Base64, binarny | [cyberchef.org](https://cyberchef.org) |
| `xxd` (Linux)                     | Podgląd pliku w HEX w terminalu          | `xxd nazwa_pliku`                      |
| `file` (Linux)                    | Sprawdza typ pliku po magic bytes        | `file nazwa_pliku`                     |

### Ściągawka — zapamiętaj na pamięć

<div class="code">

<span class="cm">// JEDNOSTKI:</span> <span class="ck">1 bit</span> = <span class="cv">0 lub 1</span> <span class="ck">4 bity</span> = <span class="cv">1 cyfra HEX</span> <span class="ck">8 bitów</span> = <span class="cv">1 bajt = 2 cyfry HEX = 256 wartości</span> <span class="ck">1 kolor RGB</span> = <span class="cv">3 bajty = 24 bity = 6 cyfr HEX</span> <span class="cm">// WAŻNE WARTOŚCI:</span> <span class="cg">FF</span> = <span class="cv">255</span> = <span class="cv">11111111</span> <span class="cm">← maksimum, pełny bajt</span> <span class="cg">00</span> = <span class="cv">0</span> = <span class="cv">00000000</span> <span class="cm">← minimum, pusty bajt</span> <span class="cm">// SYGNATURY — ZAPAMIĘTAJ:</span> <span class="cr">4D 5A</span> = <span class="cr">.EXE</span> <span class="cm">← NAJWAŻNIEJSZE W SOC!</span> <span class="ck">FF D8 FF</span> = <span class="ck">.JPG</span> <span class="ck">89 50 4E 47</span> = <span class="ck">.PNG</span> <span class="ck">25 50 44 46</span> = <span class="ck">.PDF</span> <span class="ck">50 4B 03 04</span> = <span class="ck">.ZIP</span>

</div>

</div>

<div id="s25" class="section section">

<div class="section-header">

<span class="section-num-badge">25</span>
