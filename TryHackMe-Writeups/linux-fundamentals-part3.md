# TryHackMe — Linux Fundamentals: Part 3

Writeup z trzeciej części serii Linux Fundamentals na TryHackMe. Notatki obejmują pobieranie/serwowanie plików, zarządzanie procesami, edytory tekstu, crontab oraz repozytoria pakietów.

---

## Task 1-2 — Pobieranie i serwowanie plików

### `wget` — pobieranie plików przez HTTP

```bash
wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
```

Pobiera plik z podanego adresu URL, tak jakbyśmy otwierali go w przeglądarce.

### `scp` — bezpieczne kopiowanie plików (SSH)

Format: `scp ŹRÓDŁO CEL`

**Wysyłanie pliku na zdalny host:**
```bash
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

**Pobieranie pliku ze zdalnego hosta:**
```bash
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```

`scp` korzysta z protokołu SSH, więc transfer jest szyfrowany i uwierzytelniony — w przeciwieństwie do zwykłego `cp`, które działa tylko lokalnie.

### Serwowanie plików — Python `http.server`

Ubuntu ma domyślnie zainstalowany Python3, który udostępnia prosty moduł do serwowania plików z bieżącego katalogu:

```bash
python3 -m http.server
```
```
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Serwer działa w bieżącym terminalu — trzeba **otworzyć drugi terminal**, żeby pobrać plik za pomocą `wget`:

```bash
wget http://10.113.149.98:8000/myfile
```

Wada tego rozwiązania: brak indeksowania katalogu — trzeba znać dokładną nazwę pliku. Alternatywa z większą funkcjonalnością: **Updog**.

**Flaga:**
```bash
wget http://10.113.149.98:8000/.flag.txt
```
> `THM{WGET_WEBSERVER}`

---

## Task 3 — Procesy

Procesy to uruchomione programy zarządzane przez kernel. Każdy proces ma **PID** (Process ID), który rośnie w kolejności uruchamiania — proces uruchomiony jako 60. w kolejności ma PID 60.

### Podgląd procesów

```bash
ps          # procesy w bieżącej sesji
ps aux      # wszystkie procesy w systemie (też inne użytkowniki, procesy systemowe)
top         # widok procesów w czasie rzeczywistym
```

### Zarządzanie procesami — sygnały

| Sygnał | Działanie |
|---|---|
| `SIGTERM` | zabija proces, ale pozwala mu wcześniej "posprzątać" |
| `SIGKILL` | zabija proces natychmiast, bez sprzątania |
| `SIGSTOP` | zatrzymuje/zawiesza proces |

```bash
kill 1337          # wysyła domyślnie SIGTERM do PID 1337
```

### Jak startują procesy — namespace'y i PID 0

System dzieli zasoby (CPU, RAM) między procesy za pomocą **namespace'ów** — izolują one procesy od siebie nawzajem (procesy widzą tylko te w tym samym namespace).

Proces o **PID 0** to proces startujący przy uruchomieniu systemu — na Ubuntu jest to `systemd`. Wszystkie inne programy startują jako **procesy potomne (child processes)** systemd.

### Uruchamianie usług na starcie systemu — `systemctl`

Format: `systemctl [opcja] [usługa]`

| Opcja | Znaczenie |
|---|---|
| `start` | uruchamia usługę teraz |
| `stop` | zatrzymuje usługę teraz |
| `enable` | usługa wystartuje automatycznie przy każdym boocie |
| `disable` | usługa nie wystartuje automatycznie przy boocie |
| `status` | pokazuje aktualny stan usługi |

```bash
systemctl start apache2      # uruchamia apache2 od razu
systemctl enable apache2     # sprawia, że apache2 startuje przy boocie
```

### Backgrounding / foregrounding procesów

**Operator `&`** — uruchamia komendę w tle, zwracając od razu PID zamiast oczekiwać na wynik:
```bash
echo "Hi THM" &
```

**`Ctrl + Z`** — zawiesza (suspenduje) proces działający na pierwszym planie, zwalniając terminal.

**`fg`** — przywraca zawieszony/tłowy proces z powrotem na pierwszy plan, żeby móc z nim wchodzić w interakcję.

**`jobs`** — lista procesów w tle/zawieszonych w bieżącej sesji.

### Pytania i odpowiedzi

| Pytanie | Odpowiedź |
|---|---|
| Poprzedni PID to 300, jaki będzie PID nowego procesu? | `301` |
| Jaki sygnał wysłać, żeby "czysto" zabić proces? | `SIGTERM` |
| Flaga po zlokalizowaniu procesu na deployed instance | `THM{PROCESSES}` |
| Komenda zatrzymująca usługę "myservice" | `systemctl stop myservice` |
| Komenda uruchamiająca usługę na boot-cie | `systemctl enable myservice` |
| Komenda przywracająca proces na pierwszy plan | `fg` |

---

## Task 4-5 — Edytory tekstu (Nano/VIM) i Crontab

### Nano

```bash
nano nazwa_pliku
```

Podstawowe skróty (Ctrl = `^`):
- `^X` — wyjście
- `^O` — zapis (Write Out)
- `^W` — szukaj (Where Is)
- `^K` / `^U` — wytnij / wklej

### VIM

Bardziej zaawansowany edytor: konfigurowalne skróty, podświetlanie składni, dostępny praktycznie na każdym terminalu (w przeciwieństwie do nano, które nie zawsze jest zainstalowane). TryHackMe ma dedykowany pokój: [VIM room](https://tryhackme.com/room/toolboxvim), ściągawka: [vim.rtorr.com](https://vim.rtorr.com/).

### Crontab — planowanie zadań

Cron to proces uruchamiany przy boocie, odpowiedzialny za wykonywanie zaplanowanych zadań (cron jobs) na podstawie pliku **crontab**.

Format crontab (6 pól):

| Pole | Znaczenie |
|---|---|
| MIN | minuta |
| HOUR | godzina |
| DOM | dzień miesiąca |
| MON | miesiąc |
| DOW | dzień tygodnia |
| CMD | komenda do wykonania |

Przykład — backup katalogu co 12 godzin:
```
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

Gwiazdka (`*`) = wildcard, oznacza "dowolna wartość" dla danego pola.

Edycja crontaba:
```bash
crontab -e
```

**Odpowiedź:** crontab na deployed instance uruchamia się przy `@reboot`.

---

## Task 7 — Pakiety i repozytoria (APT)

### Czym jest repozytorium APT?

To **serwer z gotowym, skompilowanym oprogramowaniem** (pliki `.deb`), skąd `apt` pobiera programy — to **nie to samo co repozytorium Git/GitHub**, które służy do przechowywania i wersjonowania kodu źródłowego. Analogia: repo APT ≈ sklep z aplikacjami (jak App Store), repo Git ≈ miejsce pracy nad kodem.

Podobny koncept na macOS to **Homebrew (`brew`)** — inny menedżer pakietów, inna platforma, ta sama filozofia.

### Zarządzanie repozytoriami

Dodanie repozytorium (przykład: Sublime Text):

1. Dodaj i zaufaj kluczowi GPG (potwierdza integralność/pochodzenie oprogramowania):
```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

2. Utwórz osobny plik dla repozytorium w `/etc/apt/sources.list.d/` (np. `sublime-text.list`) i wpisz w nim adres repozytorium.

3. Zaktualizuj listę pakietów:
```bash
sudo apt update
```

4. Zainstaluj oprogramowanie:
```bash
sudo apt install sublime-text
```

### Usuwanie repozytorium/pakietu

```bash
add-apt-repository --remove ppa:PPA_Name/ppa   # usunięcie repo
apt remove sublime-text                         # usunięcie pakietu
```

> Uwaga: instancje TryHackMe nie mają dostępu do internetu — to zadanie jest wyłącznie teoretyczne.

---

## Task 8 — Logi systemowe

Logi znajdują się w katalogu `/var/log`. System automatycznie zarządza logami w procesie zwanym **rotacją (rotating)**.

Przykładowe usługi z logami:
- **Apache2** — serwer WWW (logi `access.log` i `error.log`)
- **fail2ban** — monitoruje próby brute-force
- **UFW** — firewall

Logi serwera WWW zawierają informacje o każdym requeście — przydatne do diagnozowania wydajności lub śledzenia aktywności intruza.

Typowa lokalizacja logów Apache:
```bash
cat /var/log/apache2/access.log
```

---

## Podsumowanie kluczowych komend

```bash
# Pobieranie / transfer plików
wget <url>
scp plik user@ip:/ścieżka/
scp user@ip:/ścieżka/plik .
python3 -m http.server

# Procesy
ps aux
top
kill <pid>
systemctl [start|stop|enable|disable|status] <usługa>

# Backgrounding
komenda &
Ctrl + Z
fg
jobs

# Edytory
nano plik
vim plik

# Crontab
crontab -e

# APT
apt update
apt install <pakiet>
apt remove <pakiet>
add-apt-repository <repo>
```
