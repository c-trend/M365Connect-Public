# Sicherheit

## Grundsätze

- **Quellen werden nur gelesen.** Im CRM ändert CT M365 Connect nichts. Die einzige Ausnahme ist der
  Einrichtungsassistent, der auf Klick ein eigenes Leselogin anlegt.
- **In Microsoft 365 nur eigene Daten.** Geschrieben werden ausschliesslich persönliche Kontakte mit der eigenen
  Kategorie, in den gewählten Postfächern. Andere Kontakte werden nie verändert oder gelöscht.
- **Kein stilles Löschen.** Ist der Abruf aus der Quelle unvollständig, wird nichts gelöscht. Grosse Löschmengen
  brauchen eine ausdrückliche Freigabe genau dieses Plans.

## Berechtigungen in Microsoft 365

Der Einrichtungsassistent legt eine App-Registrierung mit diesen **Anwendungsberechtigungen** an:

| Berechtigung | Zweck |
|---|---|
| `Contacts.ReadWrite` | persönliche Kontakte in den Postfächern lesen und schreiben |
| `User.Read.All` | Liste der Benutzerpostfächer für die Auswahl |

Die Anmeldung der App erfolgt mit einem **Zertifikat** im Zertifikatsspeicher des Computers, nicht mit einem
Client-Secret. `Contacts.ReadWrite` gilt technisch für alle Postfächer des Tenants; das Programm schreibt aber nur in
die gewählten. Das sollte mit dem Kunden besprochen sein. Wer die App auf bestimmte Postfächer beschränken möchte,
kann dies in Exchange Online über RBAC für Anwendungen tun.

## Cobra CRM

- Für den Betrieb wird ein eigenes SQL-Login mit **Leserecht auf genau eine Tabelle** verwendet.
- Die Admin-Anmeldung für die Einrichtung (`sa` oder Windows-Konto) wird nicht gespeichert.
- Pro Lauf gibt es genau einen Anmeldeversuch. Nach einem Fehler stoppen die automatischen Läufe, damit das Konto
  nicht gesperrt wird.

## Zugang zur Oberfläche

- HTTPS auf Port 8443, standardmässig **nur direkt auf dem Server** erreichbar.
- Anmeldung über das **Windows-Konto** (Negotiate); zugelassen sind nur Mitglieder der Gruppe
  «CTM365Connect Admins». Die erste Freischaltung erfolgt mit einem einmaligen, befristeten Token.
- Sitzungen enden nach 30 Minuten Inaktivität. Wird ein Konto aus der Gruppe entfernt, müssen sich alle offenen
  Sitzungen neu anmelden.
- Optionaler **Fernzugriff** nur aus freigegebenen privaten Netzen, doppelt abgesichert über Firewall-Regel und
  Prüfung im Programm. Aus dem Netz standardmässig nur Kerberos.
- Passworteingaben und die Einrichtung von Microsoft 365 sind nur direkt auf dem Server möglich, solange kein
  Zertifikat einer vertrauenswürdigen Zertifizierungsstelle eingerichtet ist.
- Alle Änderungen stehen im Auditlog unter **System → Systemstatus**.

## Schutz gespeicherter Daten

- Zugangsdaten sind mit Windows DPAPI an den Computer gebunden verschlüsselt.
- Das Datenverzeichnis `C:\ProgramData\CT M365 Connect` ist nur für SYSTEM und Administratoren zugänglich.
- Logs, Ereignisse und Diagnoseberichte enthalten keine Passwörter, Tokens oder Schlüssel.

## Updates

- Pakete sind mit **ECDSA P-256** signiert. Geprüft werden Prüfsumme und Signatur gegen den im Programm eingebauten
  öffentlichen Schlüssel; der private Schlüssel liegt nie beim Kunden.
- Es werden nur Pakete aus diesem Repository angenommen, und nie eine ältere als die installierte Version.
- Vor jedem Update werden Programm und Datenbank gesichert; bei einem Fehlstart wird beides zurückgespielt.

## Schwachstellen melden

Siehe [SECURITY.md](../SECURITY.md).
