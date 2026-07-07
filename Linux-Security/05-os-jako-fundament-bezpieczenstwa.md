## OS jako Fundament Bezpieczeństwa

<span class="section-tag tag-soc">SOC</span>

</div>

<div class="section-divider">

</div>

<div class="callout soc">

<span class="callout-icon">🚨</span>

<div class="callout-body">

**Kluczowa zasada SOC** Antywirus i zapora sieciowa = dodatkowe zamki w drzwiach. OS = same drzwi z solidną ramą. 🏠🔒 OS pilnuje systemu od startu — zanim włączysz cokolwiek innego!

</div>

</div>

### 4 Mechanizmy bezpieczeństwa OS

| Mechanizm                                   | Co robi                                               | Przykład                                            | Znaczenie w SOC                                                     |
|---------------------------------------------|-------------------------------------------------------|-----------------------------------------------------|---------------------------------------------------------------------|
| 🪪 <span class="hl">Uwierzytelnianie</span> | Weryfikuje kim jesteś przed dostępem                  | Hasło, odcisk palca przy logowaniu                  | Wiele nieudanych logowań = brute force!                             |
| 🔑 <span class="hl">Uprawnienia</span>      | Kontroluje co każdy użytkownik i aplikacja mogą robić | Zwykły użytkownik nie zmienia ustawień systemowych  | Eskalacja uprawnień = klasyczny wektor ataku!                       |
| 📦 <span class="hl">Izolacja</span>         | Każdy program w swoim oddzielnym "pudełku"            | Zawieszenie jednej aplikacji nie zawiesza komputera | Wirus w przeglądarce nie sięga automatycznie do plików systemowych  |
| 🛡️ <span class="hl">Ochrona systemu</span>  | Blokuje zmiany w krytycznych plikach                  | Plik "tylko do odczytu" — nikt go nie nadpisze      | Złośliwe oprogramowanie ma utrudnione nadpisanie plików systemowych |

</div>

<div id="s23" class="section section">

<div class="section-header">

<span class="section-num-badge">23</span>
