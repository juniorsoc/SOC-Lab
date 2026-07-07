## System Operacyjny — Co to jest i Co Robi

<span class="section-tag tag-os">Systemy</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Definicja**OS to niewidzialny menedżer komputera — działa między Tobą, aplikacjami a sprzętem. Bez niego komputer to kupka drogiego plastiku i metalu.

</div>

</div>

### Pięć głównych obowiązków OS

| \#                              | Obowiązek                                          | Przykład z życia                                                                                                    |
|---------------------------------|----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| <span class="b b-cyan">1</span> | <span class="hl">Zarządzanie procesami</span>      | Przeglądarka + Spotify + Discord naraz — OS przełącza między nimi tak szybko że wydaje się że działają jednocześnie |
| <span class="b b-cyan">2</span> | <span class="hl">Zarządzanie pamięcią (RAM)</span> | Każda aplikacja dostaje swoją "szufladę". Gdy brakuje miejsca — OS odkłada część do schowka (pamięć wirtualna)      |
| <span class="b b-cyan">3</span> | <span class="hl">Zarządzanie plikami</span>        | OS wie gdzie leży każdy plik i kto może go otworzyć                                                                 |
| <span class="b b-cyan">4</span> | <span class="hl">Zarządzanie użytkownikami</span>  | Logujesz się hasłem — Twoje pliki są niewidoczne dla innych kont na tym samym komputerze                            |
| <span class="b b-cyan">5</span> | <span class="hl">Zarządzanie urządzeniami</span>   | Podłączasz myszkę lub pendrive — OS automatycznie rozpoznaje urządzenie                                             |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Dlaczego ważne w SOC** Zarządzanie procesami → wykrywasz nieznane procesy (malware!)  ·  Zarządzanie plikami → uprawnienia "tylko do odczytu" chronią pliki systemowe  ·  Zarządzanie użytkownikami → nieautoryzowane konto = kompromitacja systemu!

</div>

</div>

</div>

<div id="s21" class="section section">

<div class="section-header">

<span class="section-num-badge">21</span>


---

## Przestrzeń Jądra vs Przestrzeń Użytkownika

<span class="section-tag tag-os">Systemy</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Dlaczego to istnieje?**Różne części systemu mają różne poziomy uprawnień — chroni przed atakami i błędami. Jedna wadliwa aplikacja nie może zniszczyć całego systemu.

</div>

</div>

### Analogia — Lotnisko

| Element                                | Lotnisko                        | Komputer            |
|----------------------------------------|---------------------------------|---------------------|
| Sprzęt                                 | 🛣️ Pasy, radar, paliwo          | Procesor, RAM, dysk |
| Aplikacje                              | ✈️ Linie lotnicze i pasażerowie | Przeglądarka, gry   |
| <span class="hl">Jądro (Kernel)</span> | 🗼 **Wieża kontrolna**          | **Kernel**          |

### Porównanie przestrzeni

|                                            | 🔐 Przestrzeń Jądra                             | 👤 Przestrzeń Użytkownika                                        |
|--------------------------------------------|-------------------------------------------------|------------------------------------------------------------------|
| <span class="hl">Analogia</span>           | Wieża kontrolna / maszynownia hotelu            | Pokój hotelowy                                                   |
| <span class="hl">Dostęp do sprzętu</span>  | <span class="hl-g">Pełny, nieograniczony</span> | <span class="hl-r">Brak — tylko przez wywołania systemowe</span> |
| <span class="hl">Kto działa</span>         | Tylko jądro i zaufane komponenty                | Wszystkie zwykłe aplikacje                                       |
| <span class="hl">Konsekwencja błędu</span> | Może zawiesić cały system                       | Tylko dana aplikacja pada                                        |

### Jak aplikacja prosi o dostęp do sprzętu?

<div class="flow">

<div class="fs">

Aplikacja (user space)

</div>

<span class="fa">→</span>

<div class="fs">

Wywołanie systemowe

</div>

<span class="fa">→</span>

<div class="fs">

Jądro sprawdza

</div>

<span class="fa">→</span>

<div class="fs">

Jądro wykonuje

</div>

<span class="fa">→</span>

<div class="fs ok">

✓ Wynik wraca

</div>

</div>

Jak dzwonienie do recepcji hotelowej — oni schodzą do maszynowni zamiast Ciebie.

### OS vs Jądro — jaka różnica?

| Pojęcie                                  | Analogia         | Co zawiera                                                      |
|------------------------------------------|------------------|-----------------------------------------------------------------|
| <span class="hl">OS</span>               | 🏛️ Cały rząd     | Jądro + GUI + narzędzia systemowe + sterowniki + wszystko razem |
| <span class="hl-g">Jądro (Kernel)</span> | 🔐 Tylko policja | Ta część która ma realną władzę i klucze do sprzętu             |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Dlaczego ważne w SOC** Atak na przestrzeń jądra (kernel exploit) = przejęcie pełnej kontroli nad maszyną — to najgroźniejszy typ ataku!  ·  Aplikacja próbująca bezpośrednio pisać do sprzętu bez wywołania systemowego = sygnał złośliwego oprogramowania.

</div>

</div>

</div>

<div id="s17" class="section section">

<div class="section-header">

<span class="section-num-badge">17</span>


---

## Wirtualizacja

<span class="section-tag tag-os">Systemy</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Dlaczego wirtualizacja?** Dawniej: 1 serwer = 1 aplikacja → dużo sprzętu, mało wykorzystania (5–20%). Hypervisor dzieli 1 fizyczny serwer na wiele VM-ów, każda działa niezależnie. Zamiast 3 serwerów (strona, baza, poczta) → 1 serwer z 3 VM-ami.

</div>

</div>

### Hypervisor — Typy

|                                   | Typ 1                  | Typ 2                           |
|-----------------------------------|------------------------|---------------------------------|
| <span class="hl">Działa na</span> | sprzęcie bezpośrednio  | systemie operacyjnym            |
| <span class="hl">Użycie</span>    | serwery, centra danych | nauka, testy (VirtualBox, Kali) |
| <span class="hl">Przykłady</span> | VMware ESXi, Hyper-V   | VirtualBox, VMware Workstation  |

### VM vs Kontener

|                                      | VM                           | Kontener          |
|--------------------------------------|------------------------------|-------------------|
| <span class="hl">System OS</span>    | własny, pełny                | dzieli z hostem   |
| <span class="hl">Czas startu</span>  | minuty                       | sekundy           |
| <span class="hl">Użycie w SOC</span> | testowanie malware, izolacja | szybkie wdrożenia |

</div>

<div id="s18" class="section section">

<div class="section-header">

<span class="section-num-badge">18</span>


---

## Linux — Podstawy dla SOC Analityka

<span class="section-tag tag-linux">Linux</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Czym jest Linux?**Rodzina systemów operacyjnych opartych na UNIX-ie. Open source. Jako SOC Analyst pracujesz z Linuxem CODZIENNIE — serwery, SIEM, narzędzia — wszystko chodzi na Linuxie.

</div>

</div>

### Gdzie spotykasz Linuxa na co dzień?

<div class="cards">

<div class="card">

<div class="card-label">

🌐 Internet

</div>

~96% serwerów WWW działa na Linuxie (Apache, Nginx)

</div>

<div class="card">

<div class="card-label">

🏦 Infrastruktura

</div>

Sygnalizacja świetlna, bankomaty, systemy przemysłowe

</div>

<div class="card">

<div class="card-label">

🛒 Sklepy

</div>

Kasy i systemy PoS często działają na Linuxie

</div>

<div class="card">

<div class="card-label">

📱 Android

</div>

Android = jądro Linux. Twój telefon to Linux.

</div>

</div>

### Dystrybucje — która do czego

| Dystrybucja                           | Zastosowanie                                               | Dlaczego ważna w SOC                                             |
|---------------------------------------|------------------------------------------------------------|------------------------------------------------------------------|
| <span class="hl">Ubuntu</span>        | Serwery www + pełny pulpit. Min. RAM: 512 MB.              | Najczęściej spotykana na serwerach firm — musisz umieć nawigować |
| <span class="hl">Debian</span>        | Stabilna baza dla serwerów i innych dystrybucji            | Podstawa wielu systemów serwerowych                              |
| <span class="hl">Kali Linux</span>    | Pentesting i cybersecurity — setki narzędzi out-of-the-box | Twoje główne narzędzie do nauki i testów                         |
| <span class="hl">CentOS / RHEL</span> | Korporacyjne serwery enterprise                            | Często spotykana w dużych firmach                                |

<div class="callout tip">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Kluczowa różnica vs Windows**Linux jest znacznie lżejszy. Ubuntu Server działa na zaledwie <span class="hl-g">512 MB RAM</span> — niemożliwe przy Windows Server (minimum 2 GB). Dlatego serwery = Linux.

</div>

</div>

### Terminal Linux — Twoje główne narzędzie pracy

<div class="code">

<span class="ck">tryhackme</span>@<span class="cv">linux1</span>:<span class="cg">~</span>\$ <span class="cm">\# użytkownik@hostname:katalog\$</span>

</div>

### Podstawowe komendy — zapamiętaj na pamięć

| Komenda                              | Pełna nazwa             | Co robi                                 | Przykład                  |
|--------------------------------------|-------------------------|-----------------------------------------|---------------------------|
| <span class="b b-cyan">echo</span>   | —                       | Wypisuje tekst na ekran                 | `echo "Witaj SOC"`        |
| <span class="b b-cyan">whoami</span> | —                       | Pokazuje nazwę zalogowanego użytkownika | `whoami → root`           |
| <span class="b b-cyan">ls</span>     | listing                 | Wylistuj zawartość katalogu             | `ls -la`                  |
| <span class="b b-cyan">cd</span>     | change directory        | Zmień katalog                           | `cd /var/log`             |
| <span class="b b-cyan">cat</span>    | concatenate             | Wyświetl zawartość pliku                | `cat /etc/passwd`         |
| <span class="b b-cyan">pwd</span>    | print working directory | Pokaż pełną ścieżkę obecnego katalogu   | `pwd → /home/ubuntu`      |
| <span class="b b-cyan">grep</span>   | —                       | Szukaj tekstu w pliku lub outputcie     | `grep "ERROR" system.log` |
| <span class="b b-cyan">find</span>   | —                       | Znajdź plik w systemie                  | `find / -name "*.log"`    |
| <span class="b b-cyan">ps aux</span> | process status          | Pokaż wszystkie działające procesy      | `ps aux | grep malware`   |
| <span class="b b-cyan">file</span>   | —                       | Sprawdź typ pliku (magic bytes)         | `file podejrzany.jpg`     |
| <span class="b b-cyan">xxd</span>    | —                       | Podgląd pliku w HEX                     | `xxd plik.exe | head`     |

### Przykłady z życia SOC

<div class="code">

<span class="cm">\# Sprawdź zawartość podejrzanego pliku</span> <span class="ck">cat</span> /tmp/podejrzany_skrypt.sh <span class="cm">\# Znajdź wszystkie logi z błędami</span> <span class="ck">grep</span> <span class="cv">"ERROR\\FAILED\\CRITICAL"</span> /var/log/syslog <span class="cm">\# Sprawdź co działa na porcie 4444 (popularny port malware)</span> <span class="ck">netstat</span> -an \| grep <span class="cv">4444</span> <span class="cm">\# Sprawdź typ pliku — czy .jpg to naprawdę zdjęcie?</span> <span class="ck">file</span> zdjecie.jpg <span class="cg">\# zdjecie.jpg: PE32 executable (GUI) Intel 80386 ← TO JEST .EXE!</span> <span class="cm">\# Szukaj ukrytych plików w katalogu</span> <span class="ck">ls</span> -la /tmp/ <span class="cr">\# -rwxr-xr-x 1 root root 45232 May 21 03:14 .hidden_backdoor</span>

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Najważniejsze lokalizacje w Linux** `/var/log/` — wszystkie logi systemowe (złoto dla SOC) · `/tmp/` — malware często tu ląduje (world-writable!) · `/etc/passwd` — lista użytkowników systemu · `/etc/crontab` — zaplanowane zadania (backdoor może tu być!) · `/proc/` — informacje o działających procesach

</div>

</div>

### Pro tipy — przydatne skróty

| Skrót / Trick             | Co robi                                 |
|---------------------------|-----------------------------------------|
| `ls Pictures`             | Listuj katalog bez wchodzenia do niego  |
| `cat plik | grep "haslo"` | Szukaj słowa w outputcie komendy (pipe) |
| `cd ..`                   | Wejdź katalog wyżej                     |
| `cd ~`                    | Wróć do katalogu domowego               |
| Strzałka ↑                | Poprzednia komenda w historii           |
| Tab                       | Autouzupełnianie nazwy pliku/komendy    |
| Ctrl+C                    | Przerwij działającą komendę             |

</div>

<div id="slinuxinfo" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
