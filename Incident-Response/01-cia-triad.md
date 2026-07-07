## CIA Triad — Co chronimy w cyberbezpieczeństwie

<span class="section-tag tag-soc">SOC</span>

</div>

<div class="section-divider">

</div>

<div class="callout info">

<span class="callout-icon">💡</span>

<div class="callout-body">

**Dlaczego CIA Triad jest kluczowy w SOC?**Każdy incydent bezpieczeństwa tłumaczy się przez CIA Triad. Analityk SOC zawsze pyta: co zostało naruszone — poufność, integralność czy dostępność? To fundament całego cybersecurity.

</div>

</div>

<div class="cia-cards">

<div class="cia-card cia-c">

<div class="cia-letter">

C

</div>

<div class="cia-name">

Confidentiality

</div>

<div class="cia-desc">

Poufność — dane dostępne tylko dla uprawnionych osób

</div>

</div>

<div class="cia-card cia-i">

<div class="cia-letter">

I

</div>

<div class="cia-name">

Integrity

</div>

<div class="cia-desc">

Integralność — dane nie są modyfikowane bez zgody

</div>

</div>

<div class="cia-card cia-a">

<div class="cia-letter">

A

</div>

<div class="cia-name">

Availability

</div>

<div class="cia-desc">

Dostępność — dane i usługi dostępne gdy są potrzebne

</div>

</div>

</div>

------------------------------------------------------------------------

### 🔐 Confidentiality — Poufność

Zapewnia że dane wrażliwe są dostępne wyłącznie dla uprawnionych osób. Naruszenie może prowadzić do strat finansowych i konsekwencji prawnych.

| Sytuacja                                                            | Poufność?                        | Dlaczego?                                  |
|---------------------------------------------------------------------|----------------------------------|--------------------------------------------|
| Hasło do Gmail napisane na kartce na biurku                         | <span class="hl-r">❌ NIE</span> | Każdy fizycznie w pobliżu może je odczytać |
| Dokumenty wewnętrzne dostępne tylko dla pracowników z uprawnieniami | <span class="hl-g">✅ TAK</span> | Dostęp kontrolowany — tylko uprawnieni     |
| Twój prywatny dokument jest publiczny w internecie                  | <span class="hl-r">❌ NIE</span> | Dostęp nieograniczony — każdy może czytać  |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Naruszenia poufności = data breach**Narzędzia: `szyfrowanie`, `access control`, `VPN`, `MFA`. W SOC — szukasz nieautoryzowanego dostępu do danych w logach.

</div>

</div>

------------------------------------------------------------------------

### ✅ Integrity — Integralność

Zapewnia że dane nie są modyfikowane przez nieuprawnione osoby. Bez integralności danych nie można im ufać.

| Sytuacja                                                             | Integralność?                    | Dlaczego?                                   |
|----------------------------------------------------------------------|----------------------------------|---------------------------------------------|
| Dane zmienione przez zatwierdzoną procedurę autoryzacji              | <span class="hl-g">✅ TAK</span> | Modyfikacja uprawniona i zaplanowana        |
| Dziennik obecności uczniów zmieniony po zamknięciu przez nauczyciela | <span class="hl-r">❌ NIE</span> | Zmiana po zamknięciu = naruszenie bez zgody |
| Cena zamówienia zmodyfikowana przed finalizacją zakupu               | <span class="hl-r">❌ NIE</span> | Nieuprawniona zmiana danych transakcji      |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Naruszenia integralności = data tampering**Narzędzia: `hashe (MD5, SHA-256)`, `podpisy cyfrowe`, `logi audytowe`. W SOC — szukasz nieautoryzowanych modyfikacji plików w logach.

</div>

</div>

------------------------------------------------------------------------

### ⚡ Availability — Dostępność

Zapewnia że dane i usługi są dostępne dla uprawnionych użytkowników kiedy ich potrzebują. Nawet krótki przestój może mieć poważne konsekwencje finansowe.

| Sytuacja                                                     | Dostępność?                      | Dlaczego?                                             |
|--------------------------------------------------------------|----------------------------------|-------------------------------------------------------|
| Krytyczne usługi zakłócone przez instalację oprogramowania   | <span class="hl-r">❌ NIE</span> | Usługi niedostępne — instalacja powinna być planowana |
| Strona firmy offline podczas godzin pracy                    | <span class="hl-r">❌ NIE</span> | Niedostępność = strata finansowa i reputacji          |
| Wszystkie systemy dostępne dla pracowników w godzinach pracy | <span class="hl-g">✅ TAK</span> | Pełna dostępność dla uprawnionych                     |

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**SOC: Naruszenia dostępności = DoS / DDoS / ransomware**Narzędzia: `load balancery`, `backupy`, `CDN`, `rate limiting`. W SOC — monitorujesz uptime i alerty o niedostępności usług.

</div>

</div>

------------------------------------------------------------------------

### 🧠 Mindset analityka SOC — 3 pytania na każdy incydent

<div class="flow">

<div class="fs" style="color:var(--cyan);border-color:rgba(56,189,248,.4)">

🔐 Dane do nieuprawnionych?

</div>

<span class="fa">→ C</span>

<div class="fs" style="color:var(--green);border-color:rgba(74,222,128,.4)">

✅ Dane zmodyfikowane?

</div>

<span class="fa">→ I</span>

<div class="fs" style="color:var(--yellow);border-color:rgba(251,191,36,.4)">

⚡ Systemy niedostępne?

</div>

<span class="fa">→ A</span>

</div>

| Filar CIA                                     | Pytanie analityka SOC                 | Przykładowy atak                    | Narzędzia obrony                                  |
|-----------------------------------------------|---------------------------------------|-------------------------------------|---------------------------------------------------|
| <span class="b b-cyan">Confidentiality</span> | Czy dane wyciekły do nieuprawnionych? | Phishing, MITM, sniffing            | Encryption, MFA, Access Control                   |
| <span class="b b-green">Integrity</span>      | Czy dane zostały zmienione bez zgody? | SQL Injection, MITM, file tampering | Hashing (SHA-256), digital signatures, audit logs |
| <span class="b b-yellow">Availability</span>  | Czy usługi były niedostępne?          | DoS, DDoS, ransomware               | Load balancer, CDN, backups, rate limiting        |

<div class="code">

<span class="cm">// CIA TRIAD — ŚCIĄGAWKA</span> <span class="ck">C</span> = <span class="cv">Confidentiality</span> = <span class="cg">POUFNOŚĆ</span> <span class="cm"> Dane tylko dla uprawnionych</span> <span class="cm"> Atak: phishing, sniffing, credential theft</span> <span class="cm"> Obrona: encryption, MFA, access control</span> <span class="ck">I</span> = <span class="cv">Integrity</span> = <span class="cg">INTEGRALNOŚĆ</span> <span class="cm"> Dane nie mogą być zmieniane bez zgody</span> <span class="cm"> Atak: MITM, SQL injection, file tampering</span> <span class="cm"> Obrona: hashing (SHA-256), digital signatures, audit logs</span> <span class="ck">A</span> = <span class="cv">Availability</span> = <span class="cg">DOSTĘPNOŚĆ</span> <span class="cm"> Usługi dostępne gdy potrzebne</span> <span class="cm"> Atak: DoS, DDoS, ransomware</span> <span class="cm"> Obrona: load balancer, CDN, backups, rate limiting</span> <span class="cr">Breach</span> = naruszenie C <span class="cm">← data leak, unauthorized access</span> <span class="cr">Tampering</span> = naruszenie I <span class="cm">← modified data, forged records</span> <span class="cr">Outage</span> = naruszenie A <span class="cm">← DDoS, service down, ransomware</span>

</div>

</div>

<div id="stools" class="section section">

<div class="section-header">

<span class="section-num-badge">★</span>
