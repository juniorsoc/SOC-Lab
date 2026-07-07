## Narzędzia Online — Rekonesans i Analiza

<span class="section-tag tag-soc">SOC</span>

</div>

<div class="section-divider">

</div>

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Narzędzie</th>
<th>Co robi</th>
<th>Kiedy używasz w SOC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span class="hl">🔍 Shodan</span><br />
<span class="dim" style="font-family:var(--mono);font-size:11px">shodan.io</span></td>
<td>Wyszukiwarka urządzeń w internecie — otwarte porty, usługi, wersje</td>
<td>Sprawdzasz czy firma ma przypadkowo otwarte porty widoczne z zewnątrz</td>
</tr>
<tr class="even">
<td><span class="hl">🛡️ VirusTotal</span><br />
<span class="dim" style="font-family:var(--mono);font-size:11px">virustotal.com</span></td>
<td>Skanuje pliki, URL-e i hashe dziesiątkami silników AV jednocześnie</td>
<td>Podejrzany plik → sprawdzasz hash → 30/70 silników wykrywa = incydent</td>
</tr>
<tr class="odd">
<td><span class="hl">🗄️ NVD</span><br />
<span class="dim" style="font-family:var(--mono);font-size:11px">nvd.nist.gov</span></td>
<td>Oficjalna baza podatności z ocenami CVSS</td>
<td>Sprawdzasz szczegóły CVE i ocenę ryzyka</td>
</tr>
<tr class="even">
<td><span class="hl">💥 ExploitDB</span><br />
<span class="dim" style="font-family:var(--mono);font-size:11px">exploit-db.com</span></td>
<td>Baza kodów PoC do demonstracji luk</td>
<td>Czy dla danego CVE istnieje gotowy exploit → priorytyzacja patchy</td>
</tr>
<tr class="odd">
<td><span class="hl">🐙 GitHub</span></td>
<td>PoC, skanery i analizy CVE — często szybciej niż oficjalne kanały</td>
<td>Szukasz skanera dla konkretnego CVE</td>
</tr>
</tbody>
</table>

<div class="callout warn">

<span class="callout-icon">⚠️</span>

<div class="callout-body">

**Uwaga na PoC z GitHuba**Nie wszystkie PoC są wiarygodne. Niektóre są niekompletne, inne celowo zawierają błędy, a czasem samo repozytorium jest złośliwe. <span class="hl-r">Zawsze sprawdzaj kod przed uruchomieniem.</span> Nigdy nie uruchamiaj nieznanego skryptu na produkcji.

</div>

</div>

</div>

<div id="scve" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
