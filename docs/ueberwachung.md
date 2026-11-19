# Überwachung

CT M365 Connect meldet seinen Zustand über **feste Ereignis-IDs** im Windows-Anwendungsprotokoll, Quelle
**«CT M365 Connect»**. Jedes RMM-Werkzeug, das die Ereignisanzeige überwacht, kann darauf reagieren – ohne Skript und
ohne Zugriff auf das Programm.

## Ereignis-IDs

| ID | Stufe | Bedeutung |
|---|---|---|
| **2001** | Warnung | **Freigabe nötig** – der Löschschutz hält Löschungen zurück |
| 2002 | Warnung | Postfächer mit Fehlern beim letzten Abgleich |
| 2003 | Warnung | Sync überfällig – kein Lauf seit dem Dreifachen des Intervalls (mindestens 60 Minuten) |
| 3001 | Fehler | Letzter Sync fehlgeschlagen |
| 3002 | Fehler | Cobra-Anmeldung gesperrt, keine automatischen Läufe mehr |
| 1000 | Information | Wieder in Ordnung, keine offenen Probleme |
| 100 / 101 | Warnung / Fehler | allgemeine Log-Einträge, nicht als Alarm gedacht |

- Der Dienst prüft alle 5 Minuten.
- Gemeldet wird nur bei einer Änderung: ein neues Problem, ein neuer Löschplan oder «wieder in Ordnung».
  Besteht ein Problem weiter, kommt alle 24 Stunden eine Erinnerung.
- Nach einem Neustart des Dienstes werden bestehende Probleme einmal erneut gemeldet.
- Vor abgeschlossener Einrichtung gibt es keine Meldungen.
- Die Meldungen enthalten nur Zahlen und Zeitpunkte, keine Namen oder Adressen.

Zusätzlich empfiehlt sich eine Überwachung des Windows-Dienstes **«CTM365Connect»** (läuft nicht, z. B. nach
5 Minuten). Ein Update stoppt den Dienst für etwa eine Minute.

Letzte Meldungen auf dem Server anzeigen:

```powershell
Get-WinEvent -FilterHashtable @{ LogName = 'Application'; ProviderName = 'CT M365 Connect'; Id = 1000,2001,2002,2003,3001,3002 } -MaxEvents 20
```

Test-Alarm ohne Eingriff in den Sync (PowerShell als Administrator):

```powershell
Write-EventLog -LogName Application -Source 'CT M365 Connect' -EventId 2001 -EntryType Warning -Message 'Test Überwachung'
```

## Beispiel: NinjaOne

| Bedingung | Einstellung | Schweregrad |
|---|---|---|
| Windows-Dienst | `CTM365Connect` inaktiv, 5 Minuten Verzögerung | hoch |
| Windows-Ereignis | Quelle `CT M365 Connect`, ID **2001** | hoch |
| Windows-Ereignis | Quelle `CT M365 Connect`, IDs 3001, 3002 | hoch |
| Windows-Ereignis | Quelle `CT M365 Connect`, IDs 2002, 2003 | mittel |

Wird ein Ticketsystem angebunden, die Bedingungen nur «zurücksetzen, wenn nicht mehr erfüllt» und **nicht** nach
einer festen Zeitspanne – sonst entsteht bei jeder Erinnerung ein neues Ticket.

Die Bedingungen lassen sich gezielt nur den Servern zuweisen, auf denen der Dienst installiert ist, z. B. über einen
Gerätetag, den ein kleines Erkennungsskript setzt, wenn der Dienst `CTM365Connect` vorhanden ist.
