---
title: Anwenderhandbuch m+m Report Package DACH
---

# Anwenderhandbuch m+m Report Package DACH

## Einleitung

Die App **m+m Report Package DACH** ergänzt das Beleg- und Berichtswesen von Microsoft Dynamics 365 Business Central um einen zusätzlichen, DACH-spezifischen Beleg: die gedruckte **Lieferanmahnung** an Ihre Lieferanten. Sie baut auf dem Basismodul **m+m Report Package** auf und schließt die Lücke, die im Standardumfang dieses Basismoduls fehlt – nämlich einen fertig gestalteten Einkaufs-Report für die **Reg. Lieferanmahnung**.

Konkret liefert die App zwei Dinge:

1. Den Report **Einkaufsbericht DACH** (Berichts-ID **5613062**), mit dem eine registrierte Lieferanmahnung an den Lieferanten gedruckt oder per E-Mail versendet werden kann.
2. Drei zusätzliche Codefelder am Kopf der Lieferanmahnung und der Reg. Lieferanmahnung – **Einkäufercode**, **Sachbearbeitercode** und **Außendienstmitarbeitercode** –, mit denen Sie festlegen, welche interne Person auf dem gedruckten Beleg als Ansprechpartner erscheint.

**Zielgruppe.** Dieses Handbuch richtet sich in erster Linie an **operative Anwender im Einkauf**, die Lieferanmahnungen bearbeiten, registrieren und an Lieferanten versenden. Für sie ist der Tagesablauf um die drei Codefelder am Belegkopf und um den Ausdruck des DACH-Berichts erweitert. Sekundär angesprochen sind **Administratoren bzw. Key-User**, die einmalig die Berichtsauswahl und die Berichtseinrichtung vornehmen, damit der Ausdruck überhaupt zur Verfügung steht.

**Umfang der App.** Die App erweitert ausschließlich das Belegwesen rund um die Lieferanmahnung. Sie enthält keine eigenen Einrichtungsseiten, keine Stammdatenkarten und keine Lager- oder Buchungslogik. Die Gestaltung der Belege (Kopf, Fußzeile, Logoposition und weitere Druckoptionen) wird zentral im Basismodul über die Seite **Berichtseinrichtung** gepflegt; die Zuordnung der Berichts-ID erfolgt in der **Berichtsauswahl – Komfort EK**.

## Schnellstart für Anwender

Der kürzeste Weg von der überfälligen Bestellung bis zur gedruckten Mahnung an den Lieferanten:

1. **Einrichtung prüfen (einmalig, durch Administrator).** Stellen Sie sicher, dass in der **Berichtsauswahl – Komfort EK** für den Einkaufsbereich DACH die Berichts-ID **5613062** hinterlegt ist. Ohne diese Zuordnung steht der Ausdruck **Einkaufsbericht DACH** nicht zur Verfügung. Layoutoptionen (z. B. Logoposition, Fußzeile) pflegen Sie in der **Berichtseinrichtung**.
2. **Lieferanmahnung öffnen.** Öffnen Sie die Liste **Lieferanmahnungen** und wählen Sie die betreffende **Lieferanmahnung** aus (oder erstellen Sie eine neue).
3. **Ansprechpartner setzen (optional).** Öffnen Sie am Belegkopf das Inforegister **m+m Belegpaket** und tragen Sie bei Bedarf **Einkäufercode**, **Sachbearbeitercode** und **Außendienstmitarbeitercode** ein.
4. **Registrieren.** Registrieren Sie die Lieferanmahnung über die Standardaktion. Aus der Lieferanmahnung wird dadurch eine **Reg. Lieferanmahnung**.
5. **Drucken oder versenden.** Öffnen Sie die **Reg. Lieferanmahnung** und drucken bzw. versenden Sie sie mit dem Layout **Einkaufsbericht DACH**. Der eingetragene **Einkäufercode** bestimmt dabei den Ansprechpartner im Kopf des Belegs.

Die Reihenfolge ist bewusst so gewählt: Die Einrichtung (Schritt 1) ist Voraussetzung, bevor der Ausdruck in Schritt 5 gelingt.

## Voraussetzungen und Einrichtung

Damit der DACH-Ausdruck einer Lieferanmahnung funktioniert, sind zwei zentrale Einrichtungsseiten des Basismoduls relevant. Beide sind Firmenweite Einrichtungen (je ein Datensatz pro Mandant) und werden vom Administrator bzw. Key-User gepflegt. Diese App selbst bringt keine eigenen Einrichtungsfelder mit; sie **nutzt** die Einrichtung des Basismoduls und stellt lediglich die zusätzliche Berichts-ID **5613062** bereit.

### Report-Bereitstellung einrichten

**Wer und wann.** Diese Einrichtung nimmt der Administrator einmalig vor der ersten Nutzung vor. Erst danach können Anwender im Tagesablauf (siehe **Codes am Belegkopf** und **Einkaufsbericht DACH**) eine Reg. Lieferanmahnung im DACH-Layout ausdrucken.

**Ablauf in Abhängigkeitsreihenfolge:**

1. **Berichtseinrichtung öffnen.** Öffnen Sie über **Suchen** die Seite **Berichtseinrichtung** (Basismodul m+m Report Package). Hier legen Sie die firmenweiten Gestaltungsoptionen für alle m+m-Belege fest – etwa Logoposition, Fußzeileninhalte, ob die Belegnummer als Barcode erscheint und ob Chargen-/Seriennummern gedruckt werden. Wenn Sie diese Optionen setzen, dann wirken sie auch auf den Ausdruck der Lieferanmahnung; ohne Pflege gelten die Standardeinstellungen des Basismoduls.
2. **Berichtsauswahl – Komfort EK öffnen.** Öffnen Sie über **Suchen** die Seite **Berichtsauswahl – Komfort EK**. Hinterlegen Sie für den Einkaufsbereich DACH die Berichts-ID **5613062**. Wenn diese ID gesetzt ist, dann wird beim Drucken einer Reg. Lieferanmahnung das DACH-Layout **Einkaufsbericht DACH** verwendet; fehlt die Zuordnung, dann kann der Beleg in diesem Layout nicht gedruckt werden.
3. **Codes am Belegkopf pflegen (optional, im Tagesablauf).** Der letzte Schritt liegt beim operativen Anwender: Er trägt auf der Lieferanmahnung die gewünschten Ansprechpartner-Codes ein (siehe nächstes Kapitel). Damit ist die Kette von der Einrichtung bis zur Nutzung geschlossen.

**Abschluss der Kette.** Die operative Aktion, die diese Einrichtung nutzbar macht, ist der **Druck** bzw. **E-Mail-Versand** der Reg. Lieferanmahnung im Kapitel **Einkaufsbericht DACH**.

### Berechtigungen

Die App liefert den zuweisbaren Berechtigungssatz **MuM RPD All** mit. Er bestimmt die Berechtigungen für die von dieser App bereitgestellten Objekte und legt fest, welche Aktionen die Anwender damit ausführen dürfen: den Report **Einkaufsbericht DACH** ausführen, den vorbereitenden Datenaufbereitungs-Report ausführen und die zugehörige Verarbeitungslogik nutzen.

| Einrichtung | Erläuterung |
|---|---|
| Berechtigungssatz **MuM RPD All** | Wenn dieser Berechtigungssatz einem Benutzer bzw. einer Benutzergruppe zugewiesen ist, dann darf dieser die DACH-Lieferanmahnung ausführen und drucken. Ohne Zuweisung stehen die von dieser App bereitgestellten Report-Objekte dem Benutzer nicht zur Verfügung, und der Ausdruck **Einkaufsbericht DACH** kann nicht gestartet werden. |

## Codes am Belegkopf

Die App fügt am Kopf der **Lieferanmahnung** und – identisch – am Kopf der **Reg. Lieferanmahnung** das Inforegister **m+m Belegpaket** mit drei Codefeldern hinzu. Über diese Felder steuern Sie, welche interne Person als Ansprechpartner im Kopf des gedruckten Belegs erscheint.

**Wer und wann.** Diese Felder pflegt der operative Anwender im Einkauf bei der Bearbeitung der Lieferanmahnung – vor dem Registrieren, damit die Angaben auf den registrierten Beleg übernommen und mitgedruckt werden. Alle drei Felder verweisen auf die Tabelle **Verkäufer/Einkäufer**; es sind also nur dort angelegte Codes wählbar.

**Einstieg:** Öffnen Sie die Liste **Lieferanmahnungen**, öffnen Sie die gewünschte **Lieferanmahnung** und wechseln Sie am Belegkopf auf das Inforegister **m+m Belegpaket**. Nach dem Registrieren finden Sie dieselben Felder auf der **Reg. Lieferanmahnung** wieder.

| Feld | Erläuterung |
|---|---|
| **Einkäufercode** | Wenn Sie hier einen Code aus **Verkäufer/Einkäufer** setzen, dann wird beim Druck der Reg. Lieferanmahnung genau dieser Einkäufer als Ansprechpartner in den Belegkopf übernommen: Name, Telefondurchwahl und Kontakt-E-Mail werden aus dem Datensatz gezogen und im Kopfbereich (**Ansprechpartner:**, **Telefondurchwahl:**, **Kontakt (E-Mail):**) angedruckt. Ohne Eintrag bleibt dieser Ansprechpartner-Block auf dem Beleg leer. |
| **Sachbearbeitercode** | Wenn Sie hier einen Code aus **Verkäufer/Einkäufer** hinterlegen, dann dokumentieren Sie den zuständigen internen Sachbearbeiter auf dem Belegkopf. Der Wert bleibt beim Registrieren erhalten und steht auf der Reg. Lieferanmahnung zur internen Nachverfolgung zur Verfügung. |
| **Außendienstmitarbeitercode** | Wenn Sie hier einen Code aus **Verkäufer/Einkäufer** eintragen, dann ordnen Sie den Beleg dem zuständigen Außendienstmitarbeiter zu. Der Wert wird auf die Reg. Lieferanmahnung übernommen und dient der internen Zuordnung des Vorgangs. |

**Zusammenspiel mit dem Ausdruck.** Von den drei Feldern steuert der **Einkäufercode** unmittelbar den Ansprechpartner-Block des Ausdrucks (siehe Kapitel **Einkaufsbericht DACH**). **Sachbearbeitercode** und **Außendienstmitarbeitercode** dienen der internen Zuordnung und Nachverfolgung. Die Werte werden beim Registrieren aus der Lieferanmahnung auf die Reg. Lieferanmahnung übertragen, sodass der historische, registrierte Beleg dieselben Angaben trägt.

## Einkaufsbericht DACH

Der **Einkaufsbericht DACH** (Berichts-ID 5613062) ist das druckbare Layout der Reg. Lieferanmahnung an den Lieferanten. Er wird nicht über **Suchen** gestartet, sondern beim Druck bzw. E-Mail-Versand einer **Reg. Lieferanmahnung** automatisch als Layout herangezogen, sobald die Berichts-ID in der **Berichtsauswahl – Komfort EK** hinterlegt ist (siehe **Report-Bereitstellung einrichten**).

**Einstieg:** Öffnen Sie die Liste **Reg. Lieferanmahnungen**, wählen Sie den Beleg aus und starten Sie den Druck bzw. E-Mail-Versand. Ist keine Selektion gesetzt, so werden nur die zuvor markierten Belege gedruckt.

### Inhalt des Belegkopfs

Der Report stellt im Kopf die für eine Lieferantenmahnung üblichen Angaben zusammen. Sie stammen aus der Reg. Lieferanmahnung, aus dem Lieferantenstamm und – für den Ansprechpartner – aus dem über **Einkäufercode** gewählten Datensatz.

| Feld auf dem Beleg | Erläuterung |
|---|---|
| **Ihre Lief.-Nr.:** | Die Nummer, unter der Sie beim Lieferanten geführt werden (aus dem Lieferantenstamm). Wird nur angedruckt, wenn hinterlegt. |
| **Belegdatum:** | Das Belegdatum der Reg. Lieferanmahnung, sprachabhängig formatiert. |
| **Buchungsdatum:** | Das Buchungsdatum der Reg. Lieferanmahnung. |
| **Ihre USt-IdNr.:** | Die Umsatzsteuer-Identifikationsnummer des Lieferanten, sofern vorhanden. |
| **Unsere Lief.-Nr.:** | Ihre eigene Kontonummer beim Lieferanten (aus dem Lieferantenstamm). |
| **Ihre Referenz:** | Die Referenz aus dem Beleg. Ist in der Berichtseinrichtung die Option „Ihre Referenz in Ihr Zeichen ändern" aktiv, dann erscheint stattdessen die Bezeichnung **Ihr Zeichen:**. |
| **Mahnstufe:** | Die Mahnstufe der Reg. Lieferanmahnung. |
| **Ansprechpartner:** | Der Name des über **Einkäufercode** gewählten Einkäufers. Nur gefüllt, wenn ein Einkäufercode gesetzt ist. |
| **Telefondurchwahl:** | Die Telefonnummer dieses Einkäufers. |
| **Kontakt (E-Mail):** | Die E-Mail-Adresse dieses Einkäufers. |
| **Nr.** (bzw. Barcode) | Die Belegnummer der Reg. Lieferanmahnung. Ist in der Berichtseinrichtung „Beleg-Nr. als Barcode" aktiv, dann wird die Nummer als Barcode dargestellt, andernfalls als Text unter der Bezeichnung **Nr.** |

### Inhalt der Belegzeilen

In den Zeilen listet der Bericht die angemahnten Positionen der zugrunde liegenden Reg. Lieferanmahnung auf. Je überfälliger Position werden u. a. folgende Spalten gedruckt:

| Spalte | Erläuterung |
|---|---|
| **Pos.** | Die fortlaufende Positionsnummer der angemahnten Zeile. |
| **Nr.** | Die Belegnummer, auf die sich die Mahnzeile bezieht (z. B. die Bestellnummer). |
| **Beschreibung** | Die Beschreibung der angemahnten Position; zusätzliche Beschreibungszeilen und Textbausteine werden mit angedruckt. |
| **Menge** | Die bestellte bzw. angemahnte Menge. |
| **Einheit** | Die Maßeinheit der Position. |
| **Restmenge** | Die noch offene Menge der Bestellzeile. |
| **Stufe** | Die Mahnstufe der jeweiligen Position. |
| **Lieferdatum** | Das für die Mahnung maßgebliche Lieferdatum. Je nach Einstellung der Zeile wird dafür das gewünschte, das zugesagte oder das erwartete Wareneingangsdatum herangezogen. |

Ist eine Position überfällig, so ergänzt der Bericht einen Hinweistext **fällig seit … Tagen**. Zusätzlich werden – sofern in der Bestellung vorhanden – Ihre Referenz, die Lieferantenauftragsnummer und die Lieferantenlieferscheinnummer als erläuternde Zeilen angedruckt. Vor- und Nachtexte der Mahnmethode (**Lieferanmahnungsmethode:**) werden ebenfalls übernommen.

### Anfrageseite des Berichts

Beim manuellen Aufruf des Berichts stehen im Bereich **Allgemein** drei Optionen zur Verfügung:

| Einrichtung | Erläuterung |
|---|---|
| **Anzahl Kopien** | Wenn Sie hier einen Wert größer als 0 eintragen, dann werden zusätzlich zum Original entsprechend viele als **KOPIE** gekennzeichnete Exemplare gedruckt; bei 0 wird nur das Original ausgegeben. |
| **Interne Informationen anzeigen** | Wenn aktiviert, dann werden zusätzliche interne Angaben (z. B. Dimensions- und MwSt.-Details) mitgedruckt; ist die Option nicht gesetzt, dann bleibt der Beleg auf die für den Lieferanten bestimmten Angaben beschränkt. |
| **Aktivität protokollieren** | Wenn aktiviert, dann wird der Ausdruck als Kontaktaktivität protokolliert; ohne die Option erfolgt keine Protokollierung des Vorgangs. |

## Typische Anwendungsfälle

### Fall 1 – Überfällige Lieferung anmahnen und DACH-Beleg versenden

1. **Auslöser.** Eine Bestellung ist überfällig; der Einkauf beschließt, den Lieferanten schriftlich zu mahnen.
2. **Einstieg in BC.** Öffnen Sie die Liste **Lieferanmahnungen** und öffnen bzw. erstellen Sie die betreffende **Lieferanmahnung**.
3. **Kernablauf.** Wechseln Sie am Belegkopf auf das Inforegister **m+m Belegpaket** und setzen Sie den **Einkäufercode** auf den zuständigen Einkäufer; bei Bedarf ergänzen Sie **Sachbearbeitercode** und **Außendienstmitarbeitercode**. Registrieren Sie anschließend die Lieferanmahnung – es entsteht eine **Reg. Lieferanmahnung**.
4. **Abschluss.** Öffnen Sie die **Reg. Lieferanmahnung** und drucken bzw. versenden Sie sie im Layout **Einkaufsbericht DACH**. Der gewählte Einkäufer erscheint im Kopf als **Ansprechpartner:** mit **Telefondurchwahl:** und **Kontakt (E-Mail):**; in den Zeilen stehen die überfälligen Positionen mit Hinweis **fällig seit … Tagen**. Voraussetzung ist die einmalige Einrichtung nach **Report-Bereitstellung einrichten**.

### Fall 2 – Klaren Ansprechpartner für Rückfragen ausweisen

1. **Auslöser.** Ein Lieferant meldet sich mit Rückfragen zu einer erhaltenen Mahnung und möchte wissen, an wen er sich wenden soll.
2. **Einstieg in BC.** Öffnen Sie die betreffende **Lieferanmahnung** (bzw. bei bereits registrierten Belegen die **Reg. Lieferanmahnung**).
3. **Kernablauf.** Prüfen bzw. setzen Sie auf dem Inforegister **m+m Belegpaket** den **Einkäufercode** so, dass der gewünschte interne Ansprechpartner hinterlegt ist. Dessen Name, Telefondurchwahl und E-Mail werden aus **Verkäufer/Einkäufer** gezogen.
4. **Abschluss.** Beim erneuten Druck der Reg. Lieferanmahnung im Layout **Einkaufsbericht DACH** erscheint der aktualisierte Ansprechpartner-Block im Belegkopf, sodass der Lieferant den richtigen Kontakt sieht.

## FAQ und Troubleshooting

### Warum steht der Ausdruck „Einkaufsbericht DACH" nicht zur Verfügung?
Weil in der **Berichtsauswahl – Komfort EK** für den Einkaufsbereich DACH die Berichts-ID **5613062** noch nicht hinterlegt ist. Ohne diese Zuordnung greift das DACH-Layout nicht. Tragen Sie die ID ein (siehe **Report-Bereitstellung einrichten**).

### Wozu dient die App überhaupt?
Sie ergänzt das Basismodul m+m Report Package um einen im Standard fehlenden Beleg: den gedruckten Einkaufs-Report zur **Reg. Lieferanmahnung**. Zusätzlich bringt sie drei Ansprechpartner-Codes am Belegkopf mit.

### Was passiert, wenn ich keinen Einkäufercode setze?
Dann bleibt der Ansprechpartner-Block im Kopf des gedruckten Belegs leer: Es werden weder **Ansprechpartner:** noch **Telefondurchwahl:** noch **Kontakt (E-Mail):** angedruckt. Der übrige Beleg wird trotzdem vollständig gedruckt.

### Woher stammen Name, Telefon und E-Mail des Ansprechpartners?
Aus dem Datensatz in **Verkäufer/Einkäufer**, der über den **Einkäufercode** ausgewählt ist. Der Bericht liest von dort Name, Telefonnummer und E-Mail-Adresse.

### Wo pflege ich Logo, Fußzeile und weitere Druckoptionen?
Nicht in dieser App, sondern zentral in der **Berichtseinrichtung** des Basismoduls. Die dort gesetzten Optionen wirken auch auf die Lieferanmahnung.

### Warum erscheint statt „Ihre Referenz:" die Bezeichnung „Ihr Zeichen:"?
Weil in der **Berichtseinrichtung** die Option „Ihre Referenz in Ihr Zeichen ändern" aktiviert ist. Dann druckt der Bericht die Referenz unter der Bezeichnung **Ihr Zeichen:**.

### Warum sehe ich die drei Codefelder auf der registrierten Mahnung wieder?
Weil die Werte beim Registrieren aus der Lieferanmahnung auf die **Reg. Lieferanmahnung** übernommen werden. So trägt der historische Beleg dieselben Angaben und kann unverändert nachgedruckt werden.

### Was bedeutet der Zusatz „fällig seit … Tagen" in den Zeilen?
Er wird für jede überfällige Position angedruckt und gibt an, wie viele Tage die Lieferung bereits überfällig ist. Ist eine Position nicht überfällig, erscheint der Hinweis nicht.

### Wie erzeuge ich zusätzliche Kopien des Belegs?
Tragen Sie auf der Anfrageseite des Berichts unter **Anzahl Kopien** die gewünschte Zahl ein. Die Kopien werden zusätzlich zum Original gedruckt und mit **KOPIE** gekennzeichnet.

### Welche Berechtigung benötige ich, um den Bericht zu drucken?
Sie benötigen den Berechtigungssatz **MuM RPD All** (oder eine ihn umfassende Zuweisung). Er stellt die von der App bereitgestellten Report-Objekte zur Ausführung bereit; ohne diese Berechtigung lässt sich der **Einkaufsbericht DACH** nicht starten.
