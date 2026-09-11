---
title: Anwenderhandbuch m+m Report Package
---

# Anwenderhandbuch m+m Report Package

## Einleitung

Das Modul **m+m Report Package** erweitert Microsoft Dynamics 365 Business Central um umfangreiche Möglichkeiten zur Individualisierung der **gedruckten und per E-Mail versendeten Belege** (Angebote, Aufträge, Rechnungen, Lieferungen, Bestellungen, Mahnungen, Servicebelege, Warenbegleitscheine und die zugehörigen gebuchten Belege). Das Modul steuert **nicht** die Buchung selbst, sondern legt fest, **welche Inhalte in welcher Form** auf den Belegen erscheinen: Kopf- und Fußinformationen, Firmenangaben, Bankverbindungen, Anreden, Barcodes, Positionsnummern, Reklamationslegenden sowie Sachbearbeiter- und Außendienstangaben.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwenderinnen und Anwender**, die täglich mit Belegen arbeiten – Verkauf, Einkauf, Service und Versand –, die Belege erfassen, Zeilen pflegen und Belege drucken oder per E-Mail versenden. Die **Berichtseinrichtung** und die Pflege der Stammdaten (Debitoren, Kreditoren, Kontakte, Verkäufer, Bankkonten) obliegen sekundär den Administratorinnen und Administratoren bzw. Key-Usern.

**Prozessüberblick.** Der typische Weg durch das Modul verläuft in drei Stufen: Zuerst legt die Administration in der **Berichtseinrichtung** unternehmensweit fest, welche Angaben angedruckt werden. Anschließend werden die **Stammdaten** so gepflegt, dass belegsteuernde Werte (Factoringbank, Anrede, Sachbearbeiter, Kopienanzahl) automatisch in die Belege übernommen werden. Im **Tagesablauf** öffnen die Anwender die Belege, prüfen bzw. ergänzen die vom Modul zugefügten Kopf- und Zeilenfelder und drucken den Beleg – der Andruck folgt dann exakt der hinterlegten Einrichtung.

## Schnellstart für Anwender

Der schnellste Weg zu einem korrekt individualisierten Beleg:

1. **Berichtseinrichtung öffnen.** Geben Sie in der Business-Central-Suche (**Suchen**) den Begriff **Berichtseinrichtung** ein und öffnen Sie die gleichnamige Seite. Legen Sie die unternehmensweiten Andruckoptionen fest (Firmeninformationen, Bankandruck, Chargen-/Seriennr., Positionsnummern-Verhalten der Legenden usw.).
2. **Positionsnummern einrichten.** Öffnen Sie über **Suchen** die **Positionsnummern Einrichtung** und legen Sie je Belegbereich (Verkauf, Einkauf, Umlagerung) die Schrittweite fest. Wählen Sie danach die Aktion **Offene Belege aktualisieren**, um bestehende offene Belege zu nummerieren.
3. **Stammdaten vorbereiten.** Kennzeichnen Sie auf der **Bankkontokarte** die Factoringbanken, hinterlegen Sie auf der **Debitorenkarte** und **Kreditorenkarte** die gewünschte Kopienanzahl sowie **Sachbearbeitercode** und **Außendienstmitarbeitercode**, und pflegen Sie am **Kontakt** den **Beleganredecode**.
4. **Beleg bearbeiten.** Öffnen Sie den gewünschten Beleg (z. B. **Verkaufsauftrag**). Im Inforegister **Berichte** stehen **Factoringbankcode**, **Sachbearbeitercode** und **Außendienstmitarbeitercode**; in den Zeilen wird automatisch die **Positionsnr.** vergeben.
5. **Drucken/Senden.** Drucken oder versenden Sie den Beleg wie gewohnt. Der Andruck übernimmt alle Einstellungen aus Berichtseinrichtung und Stammdaten.

Die Reihenfolge folgt der Abhängigkeit im Code: Ohne **Berichtseinrichtung** und passende **Stammdaten** greifen die belegseitigen Automatismen nicht.

## Einrichtung

Die Einrichtung ist der umfangreichste Teil dieses Moduls. Sie erfolgt zum Großteil einmalig durch die Administration und steuert danach dauerhaft den Belegandruck aller Anwender.

### Berichtseinrichtung

**Einstieg:** Über **Suchen** den Begriff **Berichtseinrichtung** eingeben und die Seite **Berichtseinrichtung** öffnen (unternehmensweite Einzelsatz-Einrichtung, Typ Administration).

**Prozess.** Die **Berichtseinrichtung** wird von der Administration bzw. einem Key-User **vor dem ersten Belegdruck** gepflegt. Sie ist unternehmensweit gültig (ein Datensatz je Mandant) und bestimmt, welche Felder, Zusatztexte, Bankverbindungen und Formatierungen auf allen Belegen erscheinen. Alle nachfolgenden Kapitel (Stammdaten, Tägliche Arbeit) setzen diese Einrichtung voraus. Die Seite ist in die Register **Allgemein**, **Verkauf**, **Einkauf** und **Service** gegliedert; sie zeigt genau die Felder, die der Andruck auswertet.

#### Register Allgemein

| Einrichtung | Erläuterung |
|---|---|
| **Logoposition auf Fax/E-Mail** | Bestimmt die Logoausrichtung auf Fax-/E-Mail-Belegen. Wenn ein Wert gesetzt ist, wird das Logo entsprechend positioniert; das Feld ist nur editierbar, wenn in der Debitoren- & Verkaufseinrichtung die Logoposition auf Dokumenten auf **Kein Logo** steht. Werte: **Kein Logo** (kein Logoandruck), **Links** (linksbündig), **Zentriert** (mittig), **Rechts** (rechtsbündig). |
| **Währungszeichen (MW)** | Legt das Symbol fest, das für die Mandantenwährung angedruckt wird. Wenn gefüllt, erscheint dieses Zeichen auf den Belegen statt des ISO-Codes. |
| **Firmeninformationen im Kopf/Fuß** | Steuert, wo die Firmenangaben erscheinen. Wenn **Kopf** gewählt ist, werden die Firmendaten im Belegkopf angedruckt; bei **Fuß** im Belegfuß; bei **(leer)** erfolgt kein gesonderter Andruck an dieser Stelle. |
| **Firmeninformationen in Zeilen** | Wenn aktiviert, werden die Firmendaten zusätzlich im Zeilenbereich des Belegs wiederholt; ohne Kennzeichen bleibt der Zeilenbereich frei von Firmenangaben. |
| **Firmeninformationen mehrsprachig** | Wenn aktiviert, werden die Firmenangaben in der Belegsprache (mehrsprachig) angedruckt; ohne Kennzeichen erfolgt der Andruck nur in der Mandantensprache. |
| **Anrede aus Kontakt verwenden** | Wenn aktiviert, zieht der Beleg die Anrede aus dem am Beleg verknüpften Kontakt (über den **Beleganredecode**) und baut daraus die persönliche Anrede; ohne Kennzeichen wird keine kontaktbezogene Anrede gebildet. |
| **Lieferungs- und Zahlungsbedingung** | Wenn aktiviert, werden Liefer- und Zahlungsbedingungen im Belegtext angedruckt; ohne Kennzeichen entfallen diese Angaben. |
| **Beleg-Nr. als Barcode** | Wenn aktiviert, wird die Belegnummer zusätzlich als Barcode angedruckt (siehe Kapitel **Barcode-Einrichtung**); ohne Kennzeichen erscheint nur der Klartext. |
| **Barcode Trennzeichen** | Legt das Trennzeichen fest, mit dem zusammengesetzte Barcode-Inhalte getrennt werden. Wenn gefüllt, verwendet der Barcodegenerator dieses Zeichen zur Segmentierung. |
| **Jahreszahl vierstellig** | Wenn aktiviert, werden Datumsangaben mit vierstelliger Jahreszahl angedruckt; ohne Kennzeichen erfolgt der Andruck zweistellig. |
| **Externe Belegnummer** | Wenn aktiviert, wird die externe Belegnummer auf dem Beleg angedruckt. Erst wenn dieses Feld aktiv ist, wird das Folgefeld **Externe Beleg-Nr. in Ihre Bestell-Nr. ändern** editierbar. |
| **Externe Beleg-Nr. in Ihre Bestell-Nr. ändern** | Wenn aktiviert, wird die externe Belegnummer unter der Bezeichnung „Ihre Bestell-Nr." statt „Ext. Beleg-Nr." angedruckt; ohne Kennzeichen bleibt die Standardbezeichnung. |
| **Ihre Referenz in Ihr Zeichen ändern** | Wenn aktiviert, wird das Feld „Ihre Referenz" unter der Bezeichnung „Ihr Zeichen" angedruckt; ohne Kennzeichen bleibt „Ihre Referenz". |
| **Lieferung/Rechnung an Adresse komprimieren** | Wenn aktiviert, werden Liefer- und Rechnungsadresse platzsparend zusammengefasst; ohne Kennzeichen werden sie in voller Länge angedruckt. |
| **Zolltarifnr. drucken** | Wenn aktiviert, wird die Zolltarifnummer der Artikel in den Zeilen angedruckt; relevant für Auslandsbelege. |
| **Chargen-/Seriennr. drucken** | Wenn aktiviert, werden Chargen- und Seriennummern der Artikel angedruckt. Erst wenn dieses Feld aktiv ist, werden die Anhang-Felder **Chargennr./Seriennr. als Anhang (Verkauf/Einkauf)** editierbar. |
| **Zeichnungsnr. drucken** | Wenn aktiviert, wird die Zeichnungsnummer je Artikel in den Zeilen angedruckt; ohne Kennzeichen entfällt sie. |
| **Externe Bemerkungszeilen drucken** | Wenn aktiviert, werden als extern gekennzeichnete Bemerkungszeilen auf dem Beleg angedruckt; ohne Kennzeichen bleiben sie belegintern. |
| **Bank (Währung) im Fuß andrucken, wenn es ein Auslandskunde ist** | Wenn aktiviert, wird bei abweichender Kundenwährung die passende Bankverbindung im Belegfuß angedruckt. Erst wenn dieses Feld aktiv ist, wird **Zusätzliche Bank bei abweichender Währung andrucken** verfügbar. |
| **Zusätzliche Bank bei abweichender Währung andrucken** | Wenn aktiviert, wird bei abweichender Währung eine zusätzliche Bank angedruckt. Erst wenn dieses Feld aktiv ist, kann im Folgefeld eine konkrete Bank ausgewählt werden. |
| **Zusätzliche Bank, die bei abweichender Währung im Footer angedruckt werden soll** | Legt die konkrete Bankverbindung fest, die bei abweichender Währung zusätzlich im Fuß erscheint. Wenn gefüllt, wird genau diese Bank herangezogen. |
| **Montagekomponenten andrucken** | Wenn aktiviert, werden zu Montageartikeln die enthaltenen Komponenten in den Belegzeilen angedruckt; ohne Kennzeichen erscheint nur der Montageartikel. |
| **Barcode Server URL** | Legt die URL des Dienstes fest, der die Barcodes erzeugt. Wenn gefüllt, werden Barcodes über diesen Server generiert; ohne Eintrag unterbleibt der Barcodeandruck. |
| **Firmenname im Briefkopf** | Wenn aktiviert, wird der Firmenname im Briefkopf angedruckt; ohne Kennzeichen entfällt der Firmenname an dieser Stelle. |
| **Gerichtsstand** | Freitext für den Gerichtsstand. Wenn gefüllt, wird dieser Text in den Fuß-/Rechtsangaben des Belegs angedruckt. |
| **Geschäftsführung** | Freitext für die Geschäftsführung. Wenn gefüllt, erscheint diese Angabe in den Fußangaben. |
| **Handelsregister** | Freitext für das Handelsregister. Wenn gefüllt, wird die Registerangabe in den Fußangaben angedruckt. |
| **Postfach** | Legt die Postfachangabe fest. Wenn gefüllt, wird bei Belegen mit Postfachadresse diese anstelle der Hausanschrift verwendet. |
| **PLZ-Code (Postfach)** | Legt die Postleitzahl des Postfachs fest; wird gemeinsam mit **Postfach** und **Ort (Postfach)** angedruckt. |
| **Ort (Postfach)** | Legt den Ort des Postfachs fest; ergänzt die Postfachadresse im Andruck. |

#### Register Verkauf

| Einrichtung | Erläuterung |
|---|---|
| **Zusteller andrucken** | Wenn aktiviert, wird der Zusteller (Versanddienstleister) auf Verkaufsbelegen angedruckt; ohne Kennzeichen entfällt die Angabe. |
| **Chargennr./Seriennr. als Anhang (Verkauf)** | Wenn aktiviert, werden Chargen-/Seriennummern im Verkauf als separater Anhang statt in den Zeilen angedruckt. Editierbar nur bei aktivem **Chargen-/Seriennr. drucken**. |
| **Rabatt % immer andrucken** | Wenn aktiviert, wird der Zeilenrabatt in Prozent auf Verkaufsbelegen stets angedruckt – auch bei 0 %; ohne Kennzeichen nur bei tatsächlichem Rabatt. |
| **Gewünschter Liefertermin** | Wenn aktiviert, wird der gewünschte Liefertermin auf der Auftragsbestätigung angedruckt. |
| **Zugesagter Liefertermin** | Wenn aktiviert, wird der zugesagte Liefertermin auf der Auftragsbestätigung angedruckt. |
| **Geplantes Warenausgangsdatum** | Wenn aktiviert, wird das geplante Warenausgangsdatum auf der Auftragsbestätigung angedruckt. |
| **Geplantes Lieferdatum** | Wenn aktiviert, wird das geplante Lieferdatum auf der Auftragsbestätigung angedruckt. |
| **Liefertermin als KW** (Auftragsbestätigung) | Wenn aktiviert, wird der Liefertermin auf der Auftragsbestätigung als Kalenderwoche statt als Datum angedruckt. |
| **Ausfuhrbestimmung** | Wenn aktiviert, werden Ausfuhrbestimmungen auf Rechnung/Gutschrift angedruckt. Beim Deaktivieren werden die abhängigen Felder **Ausfuhrbestimmungen in Zeilen drucken** und **Mwst. Satz ohne Positionsnummern-Zusammenfassung andrucken** automatisch zurückgesetzt. |
| **Ausfuhrbestimmungen in Zeilen drucken** | Wenn aktiviert, werden Ausfuhrbestimmungen je Zeile angedruckt; nur verfügbar bei aktiver **Ausfuhrbestimmung**. |
| **Mwst. Satz ohne Positionsnummern-Zusammenfassung andrucken** | Wenn aktiviert, wird der MwSt.-Hinweis ohne die Positionsnummern-Zusammenfassung angedruckt. Setzt aktive **Ausfuhrbestimmung** voraus (wird beim Speichern geprüft). |
| **Gutschrift entspricht Rechnungskorrektur** | Wenn aktiviert, werden Gutschriften ab dem Stichtag **Rechnungskorrektur ab** als „Rechnungskorrektur" bezeichnet und angedruckt; ohne Kennzeichen als „Gutschrift". |
| **Rechnungskorrektur ab** | Legt das Datum fest, ab dem Gutschriften als Rechnungskorrektur behandelt werden. Editierbar nur bei aktivem **Gutschrift entspricht Rechnungskorrektur**. |
| **Auftragsnr.-Bemerkung einfügen** | Wenn aktiviert, fügt das Modul beim Erzeugen der Verkaufsrechnung aus Lieferung automatisch eine Bemerkungszeile mit der Auftragsnummer ein. |
| **Externe Belegnr.-Bemerkung einfügen** | Wenn aktiviert, wird beim Erzeugen der Verkaufsrechnung eine Bemerkungszeile mit der externen Belegnummer eingefügt; abhängig von **Externe Beleg-Nr. in Ihre Bestell-Nr. ändern** wird der Text als „Ihre Bestell-Nr." oder „Ext. Beleg-Nr." formuliert. |
| **Ihre Referenz-Bemerkung einfügen** | Wenn aktiviert, wird eine Bemerkungszeile mit „Ihre Referenz" (bzw. „Ihr Zeichen") eingefügt; die Bezeichnung folgt **Ihre Referenz in Ihr Zeichen ändern**. |
| **Liefertermin als KW** (Lieferung) | Wenn aktiviert, wird das Lieferdatum auf dem Lieferschein als Kalenderwoche angedruckt. |
| **Null-Mengen unterdrücken** | Wenn aktiviert, werden Zeilen mit Menge 0 nicht angedruckt; ohne Kennzeichen erscheinen auch Null-Mengen-Zeilen. |
| **Nicht fällige Posten** | Wenn aktiviert, werden auf der Mahnung auch noch nicht fällige Posten angedruckt; ohne Kennzeichen nur fällige. |
| **Erste Mahnung entspricht Zahlungserinnerung** | Wenn aktiviert, wird die erste Mahnstufe als „Zahlungserinnerung" bezeichnet und angedruckt; ohne Kennzeichen als „Mahnung". |
| **Reklamationslegende drucken** (Rücksendung/Reklamation) | Wenn aktiviert, wird auf Rücksendung/Reklamation die Legende der Reklamationsgründe angedruckt; ohne Kennzeichen entfällt die Legende. |

#### Register Einkauf

| Einrichtung | Erläuterung |
|---|---|
| **Chargennr./Seriennr. als Anhang (Einkauf)** | Wenn aktiviert, werden Chargen-/Seriennummern im Einkauf als separater Anhang angedruckt. Editierbar nur bei aktivem **Chargen-/Seriennr. drucken**. |
| **Rabatt % immer andrucken** | Wenn aktiviert, wird der Zeilenrabatt in Prozent auf Einkaufsbelegen stets angedruckt; ohne Kennzeichen nur bei tatsächlichem Rabatt. |
| **EK-Gutschrift entspricht Belastungsanzeige** | Wenn aktiviert, werden Einkaufsgutschriften als „Belastungsanzeige" bezeichnet und angedruckt; ohne Kennzeichen als „Gutschrift". |
| **Reklamationslegende drucken** (Reklamation) | Wenn aktiviert, wird auf der Einkaufsreklamation die Legende der Reklamationsgründe angedruckt. |

#### Register Service

| Einrichtung | Erläuterung |
|---|---|
| **Rabatt % immer andrucken** | Wenn aktiviert, wird der Zeilenrabatt in Prozent auf Servicebelegen stets angedruckt; ohne Kennzeichen nur bei tatsächlichem Rabatt. |

#### Weitere Aufrufe der Berichtseinrichtung

Über das Menü **Aktionen** der Berichtseinrichtung erreichen Sie unterstützende Karten: **Firmendaten** (Firmenstammdaten), **Zuständigkeitseinheit** und **Bankkonten**. Diese Verknüpfungen erleichtern die Pflege der Daten, die der Andruck heranzieht (z. B. Bankverbindungen für den Fußandruck).

### Barcode-Einrichtung

**Einstieg:** Über **Suchen** die Seite **Standard Berichtsbarcode Einrichtung** öffnen (unternehmensweite Einzelsatz-Einrichtung, Typ Administration).

**Prozess.** Die Barcode-Einrichtung wird von der Administration festgelegt, damit Belege einheitliche Barcodes tragen. Sie greift zusammen mit den Feldern **Beleg-Nr. als Barcode**, **Barcode Trennzeichen** und **Barcode Server URL** der Berichtseinrichtung: Erst wenn dort der Barcodeandruck aktiviert und ein Barcode-Server hinterlegt ist, werden die hier definierten Standardwerte für die Barcode-Erzeugung wirksam. Je gewählter **Barcodeart** blendet die Seite nur die passende Parametergruppe ein.

| Einrichtung | Erläuterung |
|---|---|
| **Barcodeart** | Legt die zu erzeugende Symbologie fest. Je nach Auswahl wird die zugehörige Parametergruppe (Aztec, Code128, DataMatrix, PDF417, QRCode) eingeblendet. Zulässige Werte sind die Symbologien **Aztec, Codabar, Code128, Code39, DataMatrix, EAN13, EAN8, ITF, MSI, PDF417, Plessey, QRCode, UPCA** (technische Symbologiebezeichnungen). Nur für Aztec, Code128, DataMatrix, PDF417 und QRCode existieren zusätzliche Parameter (siehe unten); die übrigen Symbologien werden ohne weitere Parameter erzeugt. |
| **Barcodehöhe in Pixel** | Legt die Höhe des erzeugten Barcodes in Pixel fest. Wenn gesetzt, wird der Barcode in dieser Höhe gerendert. |
| **Barcodebreite in Pixel** | Legt die Breite des erzeugten Barcodes in Pixel fest. |
| **Barcoderand in Pixel** | Legt den Rand (Ruhezone) um den Barcode in Pixel fest; ein ausreichender Rand sichert die Lesbarkeit durch Scanner. |
| **Barcode zusätzlich als Text anzeigen** | Wenn aktiviert, wird der Barcode-Inhalt zusätzlich im Klartext unter dem Barcode angedruckt; ohne Kennzeichen erscheint nur der Barcode. |
| **Barcode Bildformat** | Legt das Bildformat des erzeugten Barcodes fest. Werte: **bmp**, **jpeg**, **png** (technische Bildformate). |

Symbologiespezifische Parameter (nur bei entsprechender Barcodeart sichtbar):

- **Aztec:** **Aztec Schichten** (Anzahl der Layer) und **Aztec Fehlerkorrektur in %** (Höhe der Fehlerkorrektur; je höher, desto robuster gegen Beschädigung).
- **Code128:** **Code128 Zeichensatz B** – wenn aktiviert, wird Zeichensatz B erzwungen (relevant für alphanumerische Inhalte).
- **DataMatrix:** **DataMatrix Encodierungstyp** (Werte: **Standard, C40, Text, X12, Edifact, Base256**) und **DataMatrix Formfaktor** (**Standard**, **Rechteck erzwingen**, **Quadrat erzwingen**) – legen Codierung und Form des Codes fest.
- **PDF417:** **PDF417 Zeichensatz UTF8**, **PDF417 verdichten**, **PDF417 Verdichtung** (**Standard, Byte, Numerisch, Text**), **PDF417 Spalten/Zeilen (Minimum/Maximum)**, **PDF417 ECI unterdrücken**, **PDF417 Fehlerkorrekturlevel** (**Standard, L1–L8**) – steuern Größe, Codierung und Fehlerkorrektur.
- **QRCode:** **QRCode Zeichensatz UTF8**, **QRCode ECI unterdrücken**, **QRCode Fehlerkorrekturlevel** (**Standard, L, M, Q, H** – von niedriger zu hoher Fehlerkorrektur).

**Abschluss/Übergang.** Über die Aktion **Berichtsbarcodeauswahl** öffnen Sie die **Berichtsbarcodeauswahlliste**. Dort können Sie je Bericht (**Berichts-ID**, **Belegname**) von den Standardwerten abweichende Barcode-Einstellungen hinterlegen; die Detailwerte pflegen Sie über die **Berichtsbarcodeauswahlkarte**. So erhalten einzelne Belege abweichende Barcodes, während alle übrigen die Standardwerte nutzen.

### Positionsnummern einrichten

**Einstieg:** Über **Suchen** die Seite **Positionsnummern Einrichtung** öffnen (unternehmensweite Einzelsatz-Einrichtung, Typ Administration).

**Prozess.** Diese Einrichtung wird von der Administration **vor der ersten Belegerfassung** vorgenommen. Sie bewirkt, dass Zeilen in Verkaufs-, Einkaufs- und Umlagerungsbelegen automatisch eine durchgängige **Positionsnr.** erhalten, die auch in die gebuchten Belege übernommen und auf den Belegen angedruckt wird. Die Nummerierung wird je neuer oder geänderter Zeile automatisch neu berechnet.

| Einrichtung | Erläuterung |
|---|---|
| **Verkauf Schrittweite** | Legt fest, mit welcher Schrittweite die Positionsnummern in Verkaufsbelegen hochgezählt werden. Wenn z. B. 10 gesetzt ist, erhalten die Zeilen die Nummern 10, 20, 30 …; so bleibt Platz für spätere Einschübe. |
| **VK-Position für Zu-/Abschläge deaktivieren** | Wenn aktiviert, erhalten Verkaufszeilen der Art **Artikel Zu-/Abschlag** **keine** Positionsnummer; ohne Kennzeichen werden auch diese Zeilen nummeriert (und dabei ans Zeilenende sortiert). |
| **Einkauf Schrittweite** | Legt die Schrittweite der Positionsnummern in Einkaufsbelegen fest (z. B. 100 → 100, 200, 300 …). |
| **EK-Position für Zu-/Abschläge deaktivieren** | Wenn aktiviert, erhalten Einkaufszeilen der Art **Artikel Zu-/Abschlag** keine Positionsnummer; ohne Kennzeichen werden sie nummeriert. |
| **Umlagerung Schrittweite** | Legt die Schrittweite der Positionsnummern in Umlagerungsaufträgen fest (z. B. 1000). |
| **Clientsortierung verwenden** | Wenn aktiviert, wird die Zeilenreihenfolge in der Belegmaske nach Positionsnummer sortiert; so sieht der Anwender die Zeilen bereits im Client in Andruckreihenfolge. |
| **Belegsortierung verwenden** | Wenn aktiviert, wird der Andruck der Zeilen nach Positionsnummer sortiert; ohne Kennzeichen folgt der Andruck der internen Zeilennummer. |

*Hinweis:* Die zugrunde liegende Tabelle enthält zusätzlich eine **Service Schrittweite**; diese ist auf der Einrichtungsseite nicht als eigenes Feld eingeblendet, wird aber über die Aktion **Offene Servicebelege aktualisieren** wirksam.

**Aktionen (Prozessabschluss).** Nach der Ersteinrichtung nummerieren Sie bestehende offene Belege über die Aktionen im Menüband:

| Aktion | Erläuterung |
|---|---|
| **Offene Belege aktualisieren** | Aktualisiert die Positionsnummern **aller** offenen Verkaufs-, Einkaufs- und Umlagerungsbelege. Vor der Ausführung erscheint die Rückfrage „Möchten Sie die Positionsnummern aller offenen Belege aktualisieren?"; nach dem Lauf wird die Anzahl aktualisierter Belege je Belegart gemeldet. |
| **Offene Verkaufsbelege aktualisieren** | Aktualisiert nur die offenen Verkaufsbelege. Es erscheint die Rückfrage „Möchten Sie alle Positionsnummern der zugehörigen offenen Belege aktualisieren?". |
| **Offene Einkaufsbelege aktualisieren** | Aktualisiert nur die offenen Einkaufsbelege (gleiche Rückfrage). |
| **Offene Umlagerungsbelege aktualisieren** | Aktualisiert nur die offenen Umlagerungsbelege (gleiche Rückfrage). |
| **Offene Servicebelege aktualisieren** | Aktualisiert nur die offenen Servicebelege (gleiche Rückfrage). |

**Übergang zum Tagesablauf.** Ab jetzt vergibt jede neu erfasste Zeile automatisch ihre **Positionsnr.** – siehe Kapitel **Tägliche Arbeit am Beleg**.

### Beleganreden einrichten

**Einstieg:** Über **Suchen** die Liste **Beleganreden** öffnen; die Formeln je Anrede öffnen Sie über die Aktion **Formeln** (Seite **Beleganredeformeln**, geöffnet für die markierte Anrede).

**Prozess.** Die Beleganreden werden vom Key-User gepflegt, damit Belege eine **persönliche, mehrsprachige Anrede** aus den Kontaktdaten bilden können. Die Kette greift, wenn in der **Berichtseinrichtung** das Feld **Anrede aus Kontakt verwenden** aktiviert und am **Kontakt** ein **Beleganredecode** hinterlegt ist (siehe Kapitel Stammdaten).

Numerierte Einrichtungsschritte in Abhängigkeitsreihenfolge:

1. **Anrede anlegen.** Legen Sie in **Beleganreden** je Anredetyp einen Datensatz mit **Code** und **Beschreibung** an. Wenn eine Anrede gelöscht wird, werden automatisch alle zugehörigen Formeln entfernt.
2. **Formel je Sprache hinterlegen.** Öffnen Sie über **Formeln** die **Beleganredeformeln** und pflegen Sie je **Sprachcode** eine **Anrede**-Vorlage mit Platzhaltern sowie die Bausteine **Name 1** bis **Name 4**. Jeder Namensbaustein wird aus dem Kontakt gefüllt; zulässige Werte je Baustein: **Titel** (Job Title), **Vorname**, **Vorname 2** (Middle Name), **Nachname**. Leere Namensbausteine werden beim Andruck samt Platzhalter entfernt, sodass keine Lücken entstehen.
3. **Operativer Abschluss.** Weisen Sie den Anredecode am **Kontakt** zu (Feld **Beleganredecode**) und aktivieren Sie **Anrede aus Kontakt verwenden** in der Berichtseinrichtung. Beim Belegdruck wird die Anrede in der Belegsprache aus Formel und Kontaktdaten zusammengesetzt.

### Factoringbank-Zusatztexte einrichten

**Einstieg:** Auf der **Bankkontokarte** (Bankkonto) im Inforegister **MuM Reports** das Kennzeichen **Factoringbank** setzen; die Zusatztexte pflegen Sie über die Aktion **Factoringbank - Zusatztexte** (öffnet die Seite **Factoringbank - Zusatztexte** gefiltert auf das aktuelle Bankkonto).

**Prozess.** Diese Kette ermöglicht, dass bei Factoringabwicklung ein **sprachabhängiger Zusatztext** einer Factoringbank auf den Belegen (Fuß) erscheint. Konfiguriert wird sie durch die Administration; im Tagesablauf greift sie über den **Factoringbankcode** am Beleg bzw. Debitor.

1. **Bank als Factoringbank kennzeichnen.** Setzen Sie auf der **Bankkontokarte** das Feld **Factoringbank**. Wenn Sie das Kennzeichen später wieder deaktivieren und bereits Zusatztexte hinterlegt sind, fragt das System: „Sie beabsichtigen, die Bank '…' als Factoringbank zu deaktivieren. Dabei werden die zugeordneten Zusatztexte gelöscht. Möchten Sie fortfahren?" – bei Bestätigung werden die Zusatztexte gelöscht.
2. **Druckreihenfolge festlegen.** Setzen Sie **Reihenfolge Belegdruck**, wenn mehrere Banken angedruckt werden: Wenn gefüllt, bestimmt der Wert, in welcher Reihenfolge die Bankverbindungen beim Druck erscheinen.
3. **Zusatztexte pflegen.** Öffnen Sie über die Aktion **Factoringbank - Zusatztexte** die gleichnamige Seite und erfassen Sie je **Sprachcode** einen **Zusatztext**. Der Text wird bei Belegen in der jeweiligen Sprache angedruckt.
4. **Operativer Abschluss.** Hinterlegen Sie den **Factoringbankcode** am Debitor bzw. direkt am Beleg (Inforegister **Berichte**). Zusammen mit den Report-Setup-Feldern **Bank (Währung) im Fuß andrucken …** und **Zusätzliche Bank …** wird der Zusatztext beim Druck ausgegeben.

### Übersetzungen einrichten (Länder/Reklamationsgründe)

**Einstieg:** **Länder/Regionen Übersetzungen** über die Liste **Länder/Regionen** (Aktion **Länder/Regionen Übersetzungen**); **Reklamationsgrund-Übersetzung** über die Liste **Reklamationsgründe** (Aktion **Übersetzungen**). Beide Zielseiten sind zusätzlich als eigene Listen auffindbar.

**Prozess.** Diese Stammübersetzungen sorgen dafür, dass Ländernamen und Reklamationsgründe auf fremdsprachigen Belegen in der Belegsprache erscheinen. Sie werden vom Key-User gepflegt und im Andruck automatisch nach **Sprachcode** ausgewertet (u. a. für die **Reklamationslegende**, siehe Berichtseinrichtung).

- **Länder/Regionen Übersetzungen:** je **Länder-/Regionscode** und **Sprachcode** ein übersetzter **Name**. Wenn gefüllt, wird der übersetzte Ländername in der Belegsprache angedruckt.
- **Reklamationsgrund-Übersetzung:** je Reklamationsgrund-**Code** und **Sprachcode** eine übersetzte **Beschreibung**. Wenn gefüllt, erscheint die übersetzte Reklamationsbeschreibung in der Reklamationslegende.

## Stammdaten

Neben den Einrichtungsseiten fügt das Modul belegsteuernde Felder auf zentralen Stammdatenkarten hinzu. Diese Werte werden beim Erfassen von Belegen automatisch übernommen und steuern Andruck und Kopienanzahl.

### Debitor

**Einstieg:** **Debitoren** (Liste) → Debitor öffnen → Inforegister **Berichte**.

**Prozess.** Die Administration bzw. der Vertrieb pflegt hier die debitorenspezifischen Andruck- und Kopiervorgaben. Beim Anlegen eines Verkaufsbelegs werden **Sachbearbeitercode** und **Außendienstmitarbeitercode** automatisch aus dem Debitor in den Belegkopf übernommen (ergänzt ggf. durch Kontakt und Benutzereinrichtung).

| Feld | Erläuterung |
|---|---|
| **Factoringbankcode** | Legt die Factoringbank des Debitors fest (Verweis auf ein Bankkonto). Wenn gefüllt, wird der zugehörige Factoringbank-Zusatztext beim Belegdruck herangezogen. |
| **Sachbearbeitercode** | Legt den zuständigen Sachbearbeiter (Verkäufer/Einkäufer) fest. Wenn gefüllt, wird der Code beim Anlegen von Verkaufsbelegen automatisch in den Belegkopf übernommen und angedruckt. |
| **Außendienstmitarbeitercode** | Legt den zuständigen Außendienstmitarbeiter fest. Wenn gefüllt, wird er beim Anlegen von Verkaufsbelegen automatisch in den Beleg übernommen und angedruckt. |
| **Anzahl Kopien (Verkaufsrechnung)** | Legt fest, wie viele Kopien einer Verkaufsrechnung für diesen Debitor gedruckt werden. Wenn > 0, wird der Druck entsprechend vervielfacht. |
| **Anzahl Kopien (Verkaufslieferschein)** | Legt die Kopienanzahl des Verkaufslieferscheins für diesen Debitor fest. |
| **Anzahl Kopien (Verkaufsauftragsbestätigung)** | Legt die Kopienanzahl der Auftragsbestätigung für diesen Debitor fest. |

### Kreditor

**Einstieg:** **Kreditoren** (Liste) → Kreditor öffnen → Inforegister **Berichte**.

**Prozess.** Der Einkauf pflegt hier die kreditorenspezifischen Vorgaben; beim Anlegen von Einkaufsbelegen werden **Sachbearbeitercode** und **Außendienstmitarbeitercode** analog zum Debitor in den Belegkopf übernommen.

| Feld | Erläuterung |
|---|---|
| **Sachbearbeitercode** | Legt den zuständigen Sachbearbeiter fest. Wenn gefüllt, wird er beim Anlegen von Einkaufsbelegen in den Belegkopf übernommen und angedruckt. |
| **Außendienstmitarbeitercode** | Legt den zuständigen Außendienstmitarbeiter fest. Wenn gefüllt, wird er beim Anlegen von Einkaufsbelegen übernommen und angedruckt. |
| **Anzahl Kopien (Bestellung)** | Legt die Kopienanzahl der Bestellung für diesen Kreditor fest. Wenn > 0, wird der Druck entsprechend vervielfacht. |

### Kontakt

**Einstieg:** **Kontakte** (Liste) → Kontakt öffnen → Inforegister **Berichte**.

**Prozess.** Am Kontakt werden die für die persönliche Anrede und Zuständigkeit relevanten Werte gepflegt. Der **Beleganredecode** verknüpft den Kontakt mit einer **Beleganrede**/Formel; zusammen mit **Anrede aus Kontakt verwenden** (Berichtseinrichtung) bildet der Beleg daraus die Anrede in der Belegsprache.

| Feld | Erläuterung |
|---|---|
| **Beleganredecode** | Legt die zu verwendende Beleganrede fest (Verweis auf **Beleganreden**). Wenn gefüllt und **Anrede aus Kontakt verwenden** aktiv ist, baut der Beleg die persönliche Anrede aus der zugehörigen Formel und den Kontaktnamen. |
| **Sachbearbeitercode** | Legt den Sachbearbeiter fest. Wenn gefüllt, wird er beim Anlegen von Belegen für diesen Kontakt in den Belegkopf übernommen (hat Vorrang vor dem Debitorwert, wenn der Kontakt am Beleg gesetzt ist). |
| **Außendienstmitarbeitercode** | Legt den Außendienstmitarbeiter fest. Wenn gefüllt, wird er beim Anlegen von Belegen für diesen Kontakt übernommen. |

### Verkäufer/Einkäufer

**Einstieg:** **Verkäufer/Einkäufer** (Liste) → Karte öffnen → Inforegister **Berichte**.

**Prozess.** Hier werden Angaben gepflegt, die auf Belegen die verantwortliche Person kennzeichnen.

| Feld | Erläuterung |
|---|---|
| **Signatur** | Hinterlegt ein Unterschriftsbild. Wenn gefüllt, wird die Signatur des Sachbearbeiters/Verkäufers auf den Belegen angedruckt. |
| **Firmenbevollmächtigung** | Kennzeichnet, ob bzw. mit welcher Bevollmächtigung die Person zeichnet. Wenn gefüllt, wird die Angabe im Signaturbereich des Belegs berücksichtigt. |

### Benutzereinrichtung

**Einstieg:** Über **Suchen** die **Benutzereinrichtung** öffnen.

**Prozess.** In der Benutzereinrichtung werden je Anwender Vorgabewerte hinterlegt, die beim Anlegen von Belegen greifen, wenn Debitor/Kontakt keinen eigenen Wert liefern.

| Feld | Erläuterung |
|---|---|
| **Sachbearbeitercode** | Legt den Standard-Sachbearbeiter des angemeldeten Benutzers fest. Wenn gefüllt und am Beleg noch kein Sachbearbeiter gesetzt ist, wird dieser Wert beim Anlegen automatisch übernommen. |
| **Außendienstmitarbeitercode** | Legt den Standard-Außendienstmitarbeiter des Benutzers fest. Wenn gefüllt und am Beleg noch nicht gesetzt, wird er beim Anlegen automatisch übernommen. |

### MwSt.-Buchungsgruppen (Reverse-Charge)

**Einstieg:** Über **Suchen** die **MwSt.-Buchungsgruppen** öffnen und die betreffende Karte wählen.

| Feld | Erläuterung |
|---|---|
| **Reverse-Charge-Verfahren andrucken** | Wenn aktiviert, wird für Belege mit dieser MwSt.-Buchungsgruppenkombination der Reverse-Charge-Hinweis (Steuerumkehr) je Position auf dem Beleg angedruckt; ohne Kennzeichen entfällt der Hinweis. |

### Bankkonto

Siehe Kapitel **Factoringbank-Zusatztexte einrichten**. Auf der Bankkontokarte kennzeichnen Sie im Inforegister **MuM Reports** eine Bank als **Factoringbank** und legen die **Reihenfolge Belegdruck** fest; die sprachabhängigen Zusatztexte pflegen Sie über die zugehörige Aktion.

## Tägliche Arbeit am Beleg

Im Tagesablauf arbeiten die Anwender mit den Standard-Belegen von Business Central (Verkaufsangebot/-auftrag/-rechnung/-gutschrift/-reklamation, Einkaufsanfrage/-bestellung/-rechnung usw.). Das Modul fügt dort einheitliche **Kopf-** und **Zeilenfelder** hinzu, die die Berichtseinrichtung und die Stammdaten voraussetzen.

### Belegkopf

Auf den Belegkarten steht das Inforegister **Berichte** mit folgenden Feldern:

| Feld | Erläuterung |
|---|---|
| **Factoringbankcode** | Legt die für diesen Beleg zu druckende Factoringbank fest. Wird beim Anlegen aus dem Debitor vorbelegt und kann am Beleg überschrieben werden. Wenn gefüllt, erscheint der zugehörige Zusatztext im Fuß. |
| **Sachbearbeitercode** | Zeigt/setzt den zuständigen Sachbearbeiter. Wird beim Setzen von **Verkauf an Kunde**/**Verkauf an Kontakt** (bzw. den Einkaufspendants) automatisch aus Kontakt, Debitor bzw. Benutzereinrichtung übernommen und auf dem Beleg angedruckt. |
| **Außendienstmitarbeitercode** | Zeigt/setzt den zuständigen Außendienstmitarbeiter; wird analog automatisch vorbelegt und angedruckt. |

Diese Vorbelegung ist im Code hinterlegt: Beim Ändern von Debitor oder Kontakt am Verkaufsbeleg zieht das Modul Sachbearbeiter, Außendienstmitarbeiter und Verkäufer aus dem Kontakt, ersatzweise aus dem Debitor und ergänzend aus der Benutzereinrichtung, sofern die Felder am Beleg noch leer sind.

Auf gebuchten Belegen (gebuchte Verkaufsrechnung, gebuchte Lieferung, gebuchte Einkaufsrechnung, gebuchte Rücksendung usw.) sowie auf Mahnungen und ausgegebenen Mahnungen werden **Factoringbankcode**, **Sachbearbeitercode**, **Außendienstmitarbeitercode** und – bei Mahnungen – der **Verkäufercode** ebenfalls angezeigt, sodass die Angaben nach der Buchung nachvollziehbar bleiben.

### Belegzeilen (Positionsnummern)

In den Zeilensubformularen aller Verkaufs-, Einkaufs-, Service- und Umlagerungsbelege ergänzt das Modul die Spalte **Positionsnr.**; auf einigen (gebuchten/archivierten) Belegen zusätzlich **Sortierpositionsnr.**:

| Feld | Erläuterung |
|---|---|
| **Positionsnr.** | Zeigt die automatisch vergebene Positionsnummer der Zeile. Zeilen der Art **Sachkonto, Artikel, Ressource, Anlage** und **Artikel Zu-/Abschlag** erhalten eine Nummer gemäß der eingerichteten Schrittweite; Leerzeilen erhalten keine. Die Nummer wird beim Erfassen/Ändern automatisch neu berechnet und in den gebuchten Beleg übernommen. |
| **Sortierpositionsnr.** | Interner Sortierwert für die Andruck-/Anzeigereihenfolge. Wenn gesetzt, steuert er die Reihenfolge der Zeilen unabhängig von der internen Zeilennummer (z. B. Zu-/Abschlagszeilen ans Zeilenende). |

Ob die Positionsnummern in der Belegmaske und/oder im Andruck nach Positionsnr. sortiert werden, steuern die Felder **Clientsortierung verwenden** und **Belegsortierung verwenden** der Positionsnummern-Einrichtung.

### Bemerkungszeilen und Andruck je Belegart

Auf den **Verkaufs-** und **Einkaufsbemerkungsblättern** (Comment Sheets) ergänzt das Modul je Bemerkungszeile Kennzeichen, die festlegen, **auf welchen Belegarten** die jeweilige Bemerkung angedruckt wird – z. B. **Extern**, **Angebot/Anfrage**, **Auftrag/Bestellung**, **Rahmenbestellung**, **Rechnung**, **Gutschrift**, **Lieferung**, **Rücksendung/Rücklieferung**, **Reklamation**, **Kommissionierliste** und **Gebuchte Rücksendung**. Wenn ein Kennzeichen gesetzt ist, erscheint die Bemerkung genau auf der entsprechenden Belegart; ohne Kennzeichen bleibt sie auf dieser Belegart unsichtbar. So lassen sich Bemerkungen gezielt je Belegtyp steuern.

## Belege und Berichte

Nach Einrichtung und Berichtsauswahl drucken die m+m-Belege die individualisierten Layouts. Die zentralen Belegberichte des Moduls sind:

| Bericht | Berichts-ID | Abgedeckte Belegarten |
|---|---|---|
| **Verkaufsbericht** | 5400420 | Angebot, Rahmenauftrag, Auftrag, Angebot/Auftrag Archiv, Lieferung, Rechnung, Reklamation, Gutschrift, Rücksendung, Mahnung, Warenbegleitschein, Proformarechnung |
| **Einkaufsbericht** | 5400427 | Anfrage, Rahmenbestellung, Bestellung, Gutschrift, Rücksendung, Rechnung, Anfrage/Bestellung Archiv |
| **Servicebericht** | 5400432 | Serviceauftrag, Serviceangebot, Servicerechnung, Servicevertrag, Servicelieferung, Servicegutschrift |
| **FA-Arbeitsschein** | 5400411 | Fertigungsauftrags-Arbeitsschein |
| **Proformarechnung** | 5400430 | Verkauf – Proformarechnung |

Die **Berichtsart** (Angebot, Auftrag, Rechnung, Gutschrift, Reklamation, Rücksendung, Lieferung, Warenbegleitschein, Umlagerungsausgang, Rahmenbestellung, Vertrag, Versandplanung, Proformarechnung, gebuchte Rechnung, gebuchte Gutschrift) steuert, welche Aufbereitung der Bericht wählt. Die **Anzahl gedruckter Kopien** ergibt sich aus den Debitoren- bzw. Kreditorenfeldern (**Anzahl Kopien …**).

Auf **archivierten** und **gebuchten** Belegen werden die zusätzlichen Kopf- und Zeilenfelder (Factoringbankcode, Sachbearbeiter-/Außendienstmitarbeitercode, Positionsnr.) mitgeführt und mitgedruckt, sodass die Belege auch nach Buchung und Archivierung vollständig nachvollziehbar bleiben.

**Berechtigungen.** Für den Zugriff auf die Modulseiten und -daten wird der mitgelieferte Berechtigungssatz **MuM RP Permission** verwendet; er bestimmt, welche Aktionen die Anwender in den Modulseiten ausführen können.

## FAQ und Troubleshooting

### Warum erscheinen keine Positionsnummern in meinen Belegzeilen?
Die Positionsnummern werden nur vergeben, wenn in der **Positionsnummern Einrichtung** für den jeweiligen Bereich eine **Schrittweite** hinterlegt ist. Ist keine Schrittweite gepflegt, bleibt die **Positionsnr.** leer. Prüfen Sie außerdem, ob die Zeilenart eine Nummer erhält (Leerzeilen werden nie nummeriert).

### Warum haben meine Zu-/Abschlagszeilen keine Positionsnummer?
Vermutlich ist **VK-Position für Zu-/Abschläge deaktivieren** bzw. **EK-Position für Zu-/Abschläge deaktivieren** aktiviert. In diesem Zustand erhalten Zeilen der Art **Artikel Zu-/Abschlag** bewusst keine Nummer. Deaktivieren Sie das Kennzeichen, wenn diese Zeilen nummeriert werden sollen.

### Wie aktualisiere ich Positionsnummern in bereits vorhandenen Belegen?
Öffnen Sie die **Positionsnummern Einrichtung** und wählen Sie **Offene Belege aktualisieren** (alle Bereiche) oder eine der bereichsbezogenen Aktionen (**Offene Verkaufs-/Einkaufs-/Umlagerungs-/Servicebelege aktualisieren**). Bestätigen Sie die Rückfrage; anschließend meldet das System die Anzahl aktualisierter Belege.

### Warum wird die persönliche Anrede auf dem Beleg nicht gebildet?
Für die Anrede müssen drei Dinge zusammenpassen: In der **Berichtseinrichtung** muss **Anrede aus Kontakt verwenden** aktiv sein, am **Kontakt** muss ein **Beleganredecode** hinterlegt sein, und in den **Beleganredeformeln** muss für die Belegsprache eine **Anrede**-Formel existieren. Fehlt eines davon, bleibt die Anrede leer.

### Warum wird eine Factoringbank nicht im Belegfuß angedruckt?
Der Fußandruck der Bank hängt an mehreren Stellen zusammen: Die Bank muss auf der **Bankkontokarte** als **Factoringbank** gekennzeichnet sein, am Beleg (oder Debitor) muss der **Factoringbankcode** gesetzt sein, und in der **Berichtseinrichtung** müssen die Felder **Bank (Währung) im Fuß andrucken …** bzw. **Zusätzliche Bank …** entsprechend gesetzt sein.

### Was passiert mit den Zusatztexten, wenn ich das Kennzeichen „Factoringbank" entferne?
Enthält die Bank bereits Zusatztexte und deaktivieren Sie das Kennzeichen **Factoringbank**, warnt das System: „…Dabei werden die zugeordneten Zusatztexte gelöscht. Möchten Sie fortfahren?" Bestätigen Sie, werden die Zusatztexte unwiderruflich gelöscht; brechen Sie ab, bleibt das Kennzeichen gesetzt.

### Warum kann ich „Ausfuhrbestimmungen in Zeilen drucken" nicht setzen?
Dieses Feld ist nur bei aktiver **Ausfuhrbestimmung** verfügbar. Wird **Ausfuhrbestimmung** deaktiviert, setzt das System **Ausfuhrbestimmungen in Zeilen drucken** und **Mwst. Satz ohne Positionsnummern-Zusammenfassung andrucken** automatisch zurück.

### Warum ändern sich die Bezeichnungen „Gutschrift" bzw. „Ihre Referenz" auf dem Beleg?
Das ist gewollt und wird über die Berichtseinrichtung gesteuert: **Gutschrift entspricht Rechnungskorrektur** (ab **Rechnungskorrektur ab**) druckt „Rechnungskorrektur", **EK-Gutschrift entspricht Belastungsanzeige** druckt „Belastungsanzeige", **Ihre Referenz in Ihr Zeichen ändern** druckt „Ihr Zeichen", und **Externe Beleg-Nr. in Ihre Bestell-Nr. ändern** druckt „Ihre Bestell-Nr.".

### Warum stimmt die gedruckte Kopienanzahl nicht?
Die Kopienanzahl je Belegart wird auf der **Debitorenkarte** (Verkaufsrechnung, Verkaufslieferschein, Verkaufsauftragsbestätigung) bzw. **Kreditorenkarte** (Bestellung) gepflegt. Prüfen Sie dort die Felder **Anzahl Kopien (…)** für den betroffenen Geschäftspartner.

### Warum ist mein Barcode auf dem Beleg leer oder wird nicht erzeugt?
Für den Barcodeandruck müssen in der **Berichtseinrichtung** **Beleg-Nr. als Barcode** aktiviert und eine **Barcode Server URL** hinterlegt sein; zusätzlich müssen in der **Standard Berichtsbarcode Einrichtung** eine gültige **Barcodeart** und passende Maße gepflegt sein. Fehlt der Barcode-Server, unterbleibt die Erzeugung.

## Typische Anwendungsfälle

### Anwendungsfall 1: Factoringbank mit fremdsprachigem Fußtext einrichten und drucken

**Auslöser.** Die Buchhaltung meldet, dass bei ausländischen Debitoren die abtretende Factoringbank samt Hinweistext im Rechnungsfuß erscheinen soll.

**Einstieg in BC.** Öffnen Sie die **Bankkonten**, wählen Sie die betreffende Bank und öffnen Sie die **Bankkontokarte**. Im Inforegister **MuM Reports** setzen Sie das Kennzeichen **Factoringbank** und legen die **Reihenfolge Belegdruck** fest.

**Kernablauf.** Über die Aktion **Factoringbank - Zusatztexte** öffnen Sie die gleichnamige Seite (auf das Bankkonto gefiltert) und erfassen je **Sprachcode** einen **Zusatztext**. Anschließend hinterlegen Sie am Debitor (Inforegister **Berichte**) den **Factoringbankcode** und setzen in der **Berichtseinrichtung** die Felder **Bank (Währung) im Fuß andrucken, wenn es ein Auslandskunde ist** sowie ggf. **Zusätzliche Bank bei abweichender Währung andrucken** samt konkreter Bank.

**Abschluss.** Beim Druck der Verkaufsrechnung erscheint die Factoringbank mit dem sprachabhängigen Zusatztext im Fuß. Deaktivieren Sie später das Kennzeichen **Factoringbank**, weist das System auf die Löschung der Zusatztexte hin.

### Anwendungsfall 2: Durchgängige Positionsnummern im Verkaufsauftrag

**Auslöser.** Der Vertrieb wünscht auf der Auftragsbestätigung eine durchgängige, gut lesbare Positionsnummerierung der Zeilen.

**Einstieg in BC.** Öffnen Sie über **Suchen** die **Positionsnummern Einrichtung** und tragen Sie unter **Verkauf Schrittweite** z. B. 10 ein. Entscheiden Sie über **VK-Position für Zu-/Abschläge deaktivieren**, ob Zu-/Abschlagszeilen nummeriert werden. Aktivieren Sie bei Bedarf **Clientsortierung verwenden** und **Belegsortierung verwenden**.

**Kernablauf.** Wählen Sie die Aktion **Offene Verkaufsbelege aktualisieren** und bestätigen Sie die Rückfrage, um bestehende offene Aufträge zu nummerieren. Öffnen Sie danach einen **Verkaufsauftrag**: In den Zeilen wird die **Positionsnr.** automatisch gemäß Schrittweite vergeben; neue Zeilen erhalten fortlaufend die nächste Nummer.

**Abschluss.** Beim Druck der Auftragsbestätigung erscheinen die Positionsnummern in den Zeilen; nach dem Buchen werden sie in den gebuchten Beleg übernommen.

### Anwendungsfall 3: Mehrsprachige persönliche Anrede aus dem Kontakt

**Auslöser.** Für einen englischsprachigen Kunden soll die Rechnung eine korrekte, personalisierte Anrede tragen.

**Einstieg in BC.** Öffnen Sie über **Suchen** die **Beleganreden** und legen Sie eine Anrede mit **Code** und **Beschreibung** an. Über die Aktion **Formeln** öffnen Sie die **Beleganredeformeln** und hinterlegen je **Sprachcode** eine **Anrede**-Vorlage sowie die Bausteine **Name 1**–**Name 4** (z. B. **Titel**, **Vorname**, **Nachname**).

**Kernablauf.** Weisen Sie am **Kontakt** (Inforegister **Berichte**) den **Beleganredecode** zu und aktivieren Sie in der **Berichtseinrichtung** das Feld **Anrede aus Kontakt verwenden**. Erfassen Sie den Verkaufsbeleg mit dem betreffenden Kontakt/Debitor.

**Abschluss.** Beim Druck bildet der Beleg die Anrede in der Belegsprache aus Formel und Kontaktdaten; fehlende Namensbausteine werden samt Platzhalter automatisch entfernt, sodass keine Lücken entstehen.
