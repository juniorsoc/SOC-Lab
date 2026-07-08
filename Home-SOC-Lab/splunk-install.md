# Instalacja i konfiguracja Splunk (Ubuntu)

## Cel
Splunk jako centralny SIEM zbierający logi z Windows i Suricata.

## Instalacja
(uzupełnij: wersja, komenda instalacji, porty)

## Konfiguracja źródeł danych
- Windows Event Logs → Splunk Universal Forwarder
- Suricata alerts (eve.json) → Splunk

## Przydatne zapytania SPL
```
index=main sourcetype=WinEventLog:Security EventCode=4625
```
