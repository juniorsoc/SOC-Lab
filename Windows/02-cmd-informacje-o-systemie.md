## Windows CMD — Zbieranie Informacji o Systemie

<span class="section-tag tag-os">Systemy</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Dlaczego to robimy?**Przed naprawą problemu lub badaniem incydentu specjaliści IT/SOC zawsze najpierw sprawdzają podstawowe informacje o systemie. To pierwsze komendy jakie każdy analityk uruchamia na nieznanym systemie Windows.

</div>

</div>

| Komenda      | Co sprawdza                                                | Linux odpowiednik   |
|--------------|------------------------------------------------------------|---------------------|
| `whoami`     | Na jakim koncie użytkownika jesteś zalogowany              | `whoami`            |
| `hostname`   | Nazwa komputera w sieci                                    | `hostname`          |
| `systeminfo` | Szczegóły systemu operacyjnego (wersja, architektura, RAM) | `uname -a`          |
| `ipconfig`   | Konfiguracja sieci (IP, maska, brama)                      | `ip a` / `ifconfig` |

### Co szukać w wynikach

| Komenda      | Skup się na                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------|
| `whoami`     | Ważne — różni użytkownicy mają różne uprawnienia. <span class="hl-r">SYSTEM / Administrator</span> = pełna kontrola! |
| `hostname`   | Identyfikacja maszyny w sieci firmowej — `DC01` to Domain Controller!                                                |
| `systeminfo` | Nazwa i wersja OS · Typ systemu (32/64-bit) · Data ostatniego patch'a (stary = podatny!)                             |
| `ipconfig`   | Adres IPv4 · Brama domyślna (Default Gateway) · Czy jest VPN adapter?                                                |

<div class="code">

<span class="cm">\# Kolejność na nieznanym systemie Windows:</span> <span class="ck">whoami</span> <span class="cm">← kim jestem i jakie mam uprawnienia?</span> <span class="ck">hostname</span> <span class="cm">← jaka to maszyna?</span> <span class="ck">systeminfo</span> <span class="cm">← jaki Windows, jaki sprzęt, kiedy patchowany?</span> <span class="ck">ipconfig</span> <span class="cm">← jak podłączona do sieci?</span>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Dlaczego te komendy są ważne?**`whoami` = czy atakujący eskalował uprawnienia do SYSTEM? · `systeminfo` = czy system ma stare, podatne wersje? · `ipconfig` = czy maszyna ma podejrzane adaptery sieciowe (np. tunel VPN atakującego)?

</div>

</div>

</div>

<div id="s01" class="section section">

<div class="section-header">

<span class="section-num-badge">01</span>
