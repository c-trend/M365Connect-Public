# Änderungen

Ab 0.3.4 sind Versionen regulär; Beta sind nur noch Versionen mit Zusatz (z. B. `1.2.0-beta.1`). Frühere 0.x-Versionen waren Beta. Pakete und Prüfdateien: [Releases](https://github.com/c-trend/M365Connect-Public/releases).

## 0.5.1 – 22.11.2026

- **Oberfläche:** Kachelraster fest zweispaltig mit gleich hohen Kacheln – auf breiten Bildschirmen keine leere dritte Spalte mehr (Dashboard, Cobra CRM, Microsoft 365, Einstellungen). Unter 900 px eine Spalte.
- **Sync → Einstellungen** neu angeordnet: Zeitplan | Schutz, Sync-Kontakte | Übrige Kontakte (eigene Kachel), Rufnummern über die ganze Breite.
- Formularfelder in Cobra CRM → Feldzuordnung ohne leere Spalten; die Log-Tabelle lässt sich auf schmalen Bildschirmen seitlich scrollen.
- **Texte:** «Trockenlauf» statt «Dry Run», Meldungen bei Verbindungsabbruch auf Deutsch, einheitliche Begriffe (Einmal-Setup-Token, Zertifikatsspeicher, Prüfung) und korrekte Menüpfade («Einstellungen → …»).
- Dokumentation: Menüpfade nachgeführt, Sicherheitsgrundsätze um den Opt-in-Schalter «Übrige Kontakte kategorisieren» ergänzt, Screenshot Sync-Einstellungen neu.

## 0.5.0 – 22.11.2026

- **Neuer Anzeigename «CT 365 Connect».** Dienst, Programm- und Datenordner, Firewall-Regel und Zertifikate behalten ihre bisherigen Namen; ein Update ändert an der Installation nichts.
- **Übrige Kontakte kategorisieren (Opt-in):** Unter Sync → Einstellungen → «Kontakte im Postfach» lassen sich die übrigen, nicht synchronisierten Kontakte mit einer eigenen Kategorie (Standard «Eigene Kontakte») versehen. Geändert wird ausschliesslich die Kategorie; standardmässig aus. Fehler beim Kategorisieren markieren das Postfach als «Teilweise».
- **Microsoft 365 → App überschreiben / Zertifikat erneuern:** Eine vorhandene App-Registrierung kann mit neuem Zertifikat übernommen werden. Dabei werden früher zusätzlich erteilte Anwendungsberechtigungen widerrufen; scheitert das, bleibt das bisherige Zertifikat aktiv.
- **⚙ Einstellungen** oben rechts fasst Einrichtung und System zusammen.
- **Port der Weboberfläche änderbar** (Einstellungen → Allgemein, Standard 8443). Wirkt nach dem Neustart des Dienstes; die Firewall-Regel des Fernzugriffs folgt erst, wenn der neue Port tatsächlich gebunden ist. Updates prüfen den neu gespeicherten Port.
- Beim Start gleicht der Dienst die Firewall-Regel ab: fehlende oder deaktivierte Regel bei eingeschaltetem Fernzugriff wird neu gesetzt, eine verbliebene Regel bei ausgeschaltetem Fernzugriff entfernt.

## 0.4.1 – 22.11.2026

- **Cobra-Leselogin:** Scheitert die Einrichtung, entfernt der Assistent wieder, was er selbst angelegt hat (neue Leserechte, neuer Datenbankbenutzer, neues Login). Lässt sich das nicht sicher feststellen, nennt die Meldung die Befehle zum manuellen Entfernen.
- Die SQL-Server-Hilfsobjekte für Datenbankdiagramme (`sp_helpdiagrams` u. ä.), die über `public` ausführbar sein können, werden für das Leselogin gesperrt. Bisher brach die Einrichtung in diesem Fall ab.
- **Einrichtung → Cobra CRM** umfasst nur noch Verbindung und Leselogin (vier Schritte) und verweist am Ende auf **Cobra CRM → Feldzuordnung & Filter**. Feldzuordnung, Adressfilter und Vorschau gibt es nur noch dort.

## 0.4.0 – 21.11.2026

- **Anruferkennung (Cobra):** Felder werden mit ihren Cobra-Bezeichnungen im Klartext angezeigt.
- Neue Seite **«Feldzuordnung & Filter»**: Felder und Filter lassen sich ohne erneute Einrichtung anpassen; der Filter zeigt die echte Gesamtzahl der Adressen und kennzeichnet, wenn nur die häufigsten Werte aufgeführt sind.
- Einrichtung des Cobra-Leselogins und der M365-App gehärtet: Rückbau bei Fehlern, klare Meldung, wenn der Ausgang unklar ist.
- Schutz vor Kontosperre: höchstens ein Cobra-Anmeldeversuch gleichzeitig, auch zwischen Dienst und Kommandozeile. Nach einer abgelehnten Anmeldung bleiben automatische Läufe gesperrt, bis neue Zugangsdaten gespeichert sind.

## 0.3.4 – 19.11.2026

- Erste reguläre Version (nicht mehr Beta). Neue Installationen beziehen standardmässig nur reguläre Versionen.
- Lizenzbedingungen und Hinweise zu Komponenten Dritter liegen dem Paket bei.
- Neutrale Beispiele für Netze und Server in Oberfläche und Setup-Skript.

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
