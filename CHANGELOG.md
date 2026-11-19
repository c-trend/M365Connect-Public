# Änderungen

Alle Versionen 0.x sind Beta-Versionen. Pakete und Prüfdateien: [Releases](https://github.com/c-trend/M365Connect-Public/releases).

## 0.3.3 – 19.11.2026

- **Benutzerverwaltung** unter System → Benutzer: Konten und AD-Gruppen in die Admin-Gruppe aufnehmen und entfernen.
- **Überwachung** über feste Ereignis-IDs im Anwendungsprotokoll (z. B. 2001 «Freigabe nötig»), siehe [Überwachung](docs/ueberwachung.md).
- Systemstatus zeigt die aufrufbaren Adressen (Servername und localhost).
- Schaltfläche «Dry Run».

## 0.3.2 – 19.11.2026

- Cobra-Leselogin: Bricht die Einrichtung nach dem Passwortwechsel ab, wird das bisherige Passwort wiederhergestellt.

## 0.3.1 – 19.11.2026

- Fernzugriff in der Oberfläche (System → Fernzugriff) mit Firewall-Regel.
- Gehärtet: aus dem Netz nur Kerberos, Passworteingaben nur lokal, laufende Prüfung offener Sitzungen.
- Updates: Schutz vor dem Einspielen älterer Versionen.
- Setup-Skript ist im Paket enthalten.

## 0.3.0 – 18.11.2026

- Optionaler Zugriff aus dem lokalen Netz.
- Geschäftsadresse (Strasse, PLZ, Ort, Land) im Kontakt.
- Updates: «Beta» statt «Vorabversionen».

## 0.2.4 – 18.11.2026

- Cobra-Einrichtung: Sortierungskonflikt bei einem bestehenden Leselogin behoben.

## 0.2.3 – 18.11.2026

- Cobra-Einrichtung: Windows-Anmeldung mit einem anderen Konto (z. B. Domänen-Admin).

## 0.2.0 – 18.11.2026

- Updates direkt aus der Oberfläche über signierte Pakete, mit automatischem Rückroll.
