---
title: Anwenderhandbuch m+m Digital Metal Code
---

# Anwenderhandbuch m+m Digital Metal Code

## Einleitung

Das Modul **m+m Digital Metal Code** (kurz DMC) verbindet Microsoft Dynamics 365 Business Central mit einem externen DMC-Webdienst und übersetzt die Materialklassifizierung des Metallhandels in verwertbare Codes. Aus den in Business Central gepflegten **Datensatzeigenschaften** eines Datensatzes (Materialart, Artikel, Artikelvariante, Charge) erzeugt das Modul einen **DMC Code** (den vollständigen Code) und einen **IDMC Code** (den kompakten Kurzcode) und legt zu jedem IDMC die passenden **Barcodes** (Code 39 und QR Code) als Bild ab.

Umgekehrt genügt in den Belegzeilen die Eingabe eines **IDMC Code**, damit das Modul den passenden Artikel, die Artikelvariante oder die Charge findet und die Zeile automatisch füllt. So arbeiten Ihre Anwenderinnen und Anwender mit einem einzigen gescannten oder eingetippten Code statt mit Artikelnummern.

**Zielgruppe:** Primär sind es die **operativen Anwender im Tagesgeschäft** — die Personen im Verkauf und Einkauf, die Belegzeilen erfassen und einen IDMC Code eintippen oder scannen, sowie die Personen in der Wareneingangs- und Chargenverwaltung, die Chargen mit Eigenschaften anreichern. Sekundär richtet sich das Handbuch an **Administratorinnen und Administratoren bzw. Key-User**, die das Modul in der Materialeigenschaften Einrichtung, an den Materialarten und an den Eigenschaften konfigurieren.

**Kurzer Prozessüberblick:**

1. Ein Administrator aktiviert die DMC-Verbindung in der **Materialeigenschaften Einrichtung** und hinterlegt Zugangsdaten, Präfix und Trennzeichen.
2. Ein Key-User verbindet jede **Materialart** mit einer **DMC-Klasse** und ordnet den **Eigenschaften** und **Eigenschaftswerten** die DMC-Kennungen zu.
3. Über die Matching-Aktionen erhalten **Artikel**, **Artikelvarianten** und **Chargen** ihren IDMC/DMC Code.
4. Im Tagesgeschäft geben Anwender in **Verkaufs-** und **Einkaufszeilen** einen IDMC Code ein; die Zeile wird automatisch aufgelöst.
5. Zu jedem IDMC stehen **Barcodes** zur Verfügung.

Das Modul setzt das Basismodul **Materialeigenschaften** (m+m Material Properties) voraus. Materialart, Eigenschaft, Eigenschaftswert und Datensatzeigenschaft stammen aus diesem Basismodul; DMC erweitert diese Seiten um seine eigenen Felder und Aktionen. Felder, die ausschließlich zum Basismodul gehören, sind in dessen eigenem Handbuch beschrieben; hier ist der vollständige DMC-Anteil dokumentiert.

## Schnellstart für Anwender

Der Schnellstart nennt den kürzesten Weg zum Ergebnis. Die Reihenfolge folgt der technischen Abhängigkeit: **zuerst Einrichtung, dann Stammdaten, dann Tagesarbeit**.

### A. Einmalige Einrichtung (Administrator)

1. Öffnen Sie die **Materialeigenschaften Einrichtung** und wechseln Sie in das Register **DMC**.
2. Aktivieren Sie **DMC aktiviert** und tragen Sie **DMC Url**, **DMC Benutzer** und **DMC Passwort** ein.
3. Prüfen Sie **DMC-Präfix** und **DMC Werttrennzeichen** (Vorgabe `DMC` bzw. `$`).
4. Wählen Sie in der Aktionsgruppe **DMC** die Aktion **Verbindung testen**.
5. Aktivieren Sie im Register **Matching** die Kennzeichen **DMC Matching aktivieren** sowie je nach Bedarf **DMC Artikel-Matching**, **DMC Artikevarianten-Matching** und **DMC Chargen-Matching**.

### B. Stammdaten vorbereiten (Key-User)

6. Öffnen Sie die **Materialartenkarte** der Materialart und wählen Sie im Register **DMC** über **DMC Klassen anzeigen** die passende DMC-Klasse; **DMC Klassen-ID** und **DMC Klassen-Identifizierer** werden gesetzt.
7. Wählen Sie **DMC Eigenschaftenvorschlag** und danach **Fehlende Pflicht-Merkmale zuordnen**, damit alle notwendigen Eigenschaften eine **DMC Eigenschafts-ID** erhalten.

### C. Codes erzeugen (Key-User)

8. Wählen Sie auf der **Materialartenkarte** die Aktion **DMC mit Artikel matchen** (und bei Bedarf **DMC mit Artikelvariante matchen**, **DMC mit Charge matchen**). Die Datensätze erhalten **IDMC Code** und **DMC Code**.

### D. Tägliche Arbeit (Verkauf/Einkauf)

9. Legen Sie im **Verkaufsauftrag** eine neue Zeile an und tragen Sie in das Feld **IDMC Code** den gescannten oder erhaltenen Code ein.
10. Bestätigen Sie die eingeblendeten Rückfragen (z. B. Suche nur mit MUSS-Eigenschaften, Bestandsrückfrage). Die Zeile wird mit dem passenden **Artikel** bzw. der **Artikelvariante** und dem IDMC Code gefüllt.

> ☞ Das Modul enthält keinen eigenen Buchungs- oder Freigabelauf. Die eigentliche Belegbuchung erfolgt unverändert über die Standard-Buchungsaktionen von Business Central. DMC wirkt nur bis zum Füllen der Zeile.

## Einrichtung

Die Einrichtung ist der umfangreichste Konfigurationsteil. Sie umfasst die zentrale DMC-Verbindung, das Lizenzkontingent, die Matching-Optionen, die Benutzer-Benachrichtigung sowie zwei eigenständige Konfigurationsketten (Dummy-Merkmale und optionale Gruppensuche).

### DMC-Verbindung und Optionen (Materialeigenschaften Einrichtung, Register DMC)

**Wer/wann:** Ein Administrator konfiguriert diese Seite **einmalig pro Mandant**, bevor Materialarten, Artikel und Chargen erstmals mit DMC-Codes versehen werden. Es handelt sich um eine unternehmensweite Einrichtungsseite (ein Datensatz pro Mandant). **Einstieg:** Öffnen Sie über **Suchen** die **Materialeigenschaften Einrichtung** (unternehmensweite Einrichtung ohne übergeordnete Liste) und wechseln Sie in das Register **DMC**. Die hier gesetzten Werte steuern alle DMC-Funktionen der Materialarten-, Artikel- und Chargen-Seiten (Querverweis: Abschnitt **Stammdaten** und **Tägliche Arbeit**).

Felder des Registers **DMC**:

| Einrichtung | Erläuterung |
|---|---|
| **DMC aktiviert** | Wenn aktiviert, sind der DMC-Webdienst und alle DMC-Aktionen der Aktionsgruppe **DMC** freigeschaltet; ist das Kennzeichen nicht gesetzt, bleiben Verbindung und Codeerzeugung gesperrt und die Aktionen sind nicht ausführbar. |
| **DMC Url** | Wenn gesetzt, richtet das Modul alle Webdienstaufrufe (Klassen, Eigenschaften, Barcodes, IDMC) an diese Adresse; ohne gültige Url schlägt **Verbindung testen** fehl. |
| **DMC Benutzer** | Wenn gesetzt, meldet sich das Modul mit diesem Benutzer am DMC-Webdienst an; ohne Benutzer wird keine Verbindung aufgebaut. |
| **DMC Passwort** | Wenn gesetzt, wird dieses (maskierte) Passwort für die Anmeldung verwendet; es ergänzt den DMC Benutzer und ist Voraussetzung für den Abruf von Klassen und Codes. |
| **DMC-Präfix** | Wenn gesetzt (Vorgabe `DMC`), beginnt jeder erzeugte DMC Code mit diesem Präfix; beim Zerlegen eines eingegebenen Codes prüft das Modul auf genau dieses Präfix — stimmt es nicht, gilt die Eingabe als kein gültiger IDMC. |
| **DMC Werttrennzeichen** | Wenn gesetzt (Vorgabe `$`), trennt dieses Zeichen Klasse, Eigenschafts-IDs und Werte im DMC Code; ohne gültiges Trennzeichen können Codes weder erzeugt noch zerlegt werden. |
| **DMC Überprüfungszeichen** | Wenn gesetzt (Vorgabe `!`), hängt das Modul dieses Zeichen an Codes an, die einer Prüfung bedürfen; beim Einlesen erkennt das Modul das Zeichen, entfernt es und meldet „Der DMC muss überprüft werden!“ — so werden zu prüfende Codes im Beleg sichtbar. Ist das Feld leer, findet keine Überprüfungskennzeichnung statt. |

Felder der Untergruppe **DMC Lizenz**:

| Einrichtung | Erläuterung |
|---|---|
| **DMC gekaufte Lizenzanzahl** | Wenn gesetzt, legt dieser Wert das erworbene Kontingent an DMC-Abrufen fest; beim Nähern an dieses Kontingent warnt das Modul, beim Erreichen verweigert es weitere Abrufe mit dem Hinweis, eine neue Lizenz zu kaufen. |
| **DMC Lizenzwarnung bei** | Wenn gesetzt, erscheint ab diesem Restwert eine Fortfahren-Rückfrage vor dem nächsten Abruf; so bemerken die Anwender rechtzeitig ein knapp werdendes Kontingent. |
| **DMC verbrauchte Lizenzanzahl** | Zeigt die bereits verbrauchte Menge an Abrufen an; das Feld ist nicht editierbar und dient der Kontrolle des Verbrauchs. |
| **DMC Restlizenzanzahl** | Zeigt die verbleibende Menge an Abrufen an; das Feld ist nicht editierbar und ergibt sich aus gekaufter minus verbrauchter Anzahl. |

Felder der Untergruppe **Matching**:

| Einrichtung | Erläuterung |
|---|---|
| **DMC Matching aktivieren** | Wenn aktiviert, ermittelt das Modul aus den Datensatzeigenschaften den passenden IDMC/DMC Code (das eigentliche Matching); ist es nicht gesetzt, bleiben alle Matching-Aktionen und die automatische Codeermittlung wirkungslos. |
| **DMC Artikel-Matching** | Wenn aktiviert, wird für Artikel ein IDMC/DMC ermittelt (beim Entsperren des Artikels und über **DMC mit Artikel matchen**); ohne dieses Kennzeichen bleiben Artikel ohne automatischen Code. |
| **DMC Artikevarianten-Matching** | Wenn aktiviert, wird auch für Artikelvarianten gematcht; dieses Kennzeichen ist nur bei aktivem Artikelvarianten-Feature des Basismoduls bedienbar. Ohne das Kennzeichen erhalten Varianten keinen Code. |
| **DMC Chargen-Matching** | Wenn aktiviert, wird für Chargen (Chargennr.-Informationen) ein IDMC/DMC ermittelt; ohne das Kennzeichen bleiben Chargen ohne automatischen Code. |
| **DMC Hintergrund Matching** | Wenn aktiviert, läuft das Matching als Hintergrundaufgabe statt im Vordergrund; das Modul verlangt dann mindestens einen Benutzer mit **Benachrichtigung bei DMC Warnungen** in der Benutzer Einrichtung — andernfalls wird das Aktivieren mit einer Fehlermeldung verhindert. So bleibt die Erfassung flüssig und Warnungen erreichen die zuständigen Personen per Mail. |

> ☞ **Suche nur mit MUSS-Eigenschaften (Hintergrund-Matching)** ist ein weiteres Matching-Kennzeichen der Einrichtungstabelle: Wenn aktiviert, sucht das Hintergrund-Matching bei fehlender Volltrefferlage nur mit den notwendigen (MUSS-)Eigenschaften weiter; ohne das Kennzeichen bricht das Hintergrund-Matching bei fehlendem Volltreffer ab, ohne einen Teiltreffer zu übernehmen.

Aktionen der Aktionsgruppe **DMC** (Register Aktionen / Menüband):

| Aktion | Erläuterung |
|---|---|
| **Verbindung testen** | Prüft die hinterlegten Zugangsdaten gegen den DMC-Webdienst; die Aktion ist auch als angeheftete Aktion verfügbar und sollte nach jeder Änderung der Verbindungsdaten ausgeführt werden. |
| **DMC Klassen anzeigen** | Ruft die Klassen des Webdienstes ab und zeigt sie im **DMC Puffer** zur Ansicht an; dient dem Überblick über die verfügbaren Klassen. |
| **Materialart von DMC Klassen anlegen** | Legt Materialarten aus den DMC-Klassen an; die Aktion ist standardmäßig ausgeblendet und für die Ersteinrichtung großer Klassenbestände vorgesehen. |
| **IDMC vom Hashwert holen.** | Öffnet einen Eingabedialog für einen Hashwert und ermittelt daraus IDMC und DMC zur Kontrolle; nur bei aktivem Matching verfügbar. |
| **Für alle Materialarten vorschlagen** | Schlägt für alle Materialarten das Eigenschaften-Matching vor; nur bei aktivem Matching verfügbar. |
| **Für alle Eigenschaftswerte vorschlagen** | Schlägt für alle Eigenschaften die Wertzuordnung (Wert-ID) vor; nur bei aktivem Matching verfügbar. |
| **Materialart und Eigenschaft in Hintergrund vorschlagen** | Plant den kombinierten Vorschlaglauf als Hintergrundaufgabe (Job Queue) ein; nur bei aktivem Matching verfügbar. |
| **IDMC Matching initialisieren** | Startet die IDMC-Ermittlung; über einen Auswahldialog wählen Sie **Direkt ausführen** oder **Im Hintergrund ausführen**. Nur bei aktivem Matching verfügbar. |
| **DMC-Felder mit Datensatz-Eigenschaften synchronisieren** | Überträgt DMC Eigenschafts-ID und DMC Kategorie von der Materialart-Zuordnung auf alle abgeleiteten Datensatzeigenschaften der Artikel, Varianten und Chargen; nur bei aktivem Matching verfügbar. |
| **IDMC-Dummy-Merkmale** | Öffnet die Einrichtung der Merkmale, die beim Matching durch Dummywerte ersetzt werden dürfen (siehe **DMC-Dummy-Merkmale einrichten**). |

### Benutzer-Benachrichtigung (Benutzer Einrichtung)

**Wer/wann:** Ein Administrator legt fest, welche Personen bei DMC-Warnungen aus dem Hintergrund-Matching informiert werden. **Einstieg:** Öffnen Sie über **Suchen** die **Benutzer Einrichtung** (unternehmensweite Standard-Einrichtung) und ergänzen Sie je Benutzerzeile das Feld unten.

| Einrichtung | Erläuterung |
|---|---|
| **Benachrichtigung bei DMC Warnungen** | Wenn aktiviert, erhält dieser Benutzer bei Fehlern des Hintergrund-Matchings eine Benachrichtigung per Mail (Betreff „DMC Fehler!“); ist für **DMC Hintergrund Matching** kein einziger Benutzer mit diesem Kennzeichen gesetzt, verweigert das Modul das Aktivieren des Hintergrund-Matchings. |

### DMC-Matching einrichten

**Prozesseinstieg:** Diese Kette verbindet Stammdaten, globale Einrichtung und die operative Codeerzeugung. Ein Administrator und ein Key-User richten sie gemeinsam **vor der ersten Codeerzeugung** ein. Verbraucht wird die Einrichtung im Abschnitt **Tägliche Arbeit** (IDMC-Eingabe im Beleg) und bei den Matching-Aktionen der Materialart.

**Nummerierte Schritte in Abhängigkeitsreihenfolge:**

1. **Materialart mit DMC-Klasse verbinden (Stammdaten):** Setzen Sie auf der **Materialartenkarte** über **DMC Klassen anzeigen** die **DMC Klassen-ID** und den **DMC Klassen-Identifizierer**. Wenn diese Werte gesetzt sind, kennt das Modul die Zielklasse; ohne sie sind alle Matching-Aktionen der Materialart gesperrt.
2. **Eigenschaften kennzeichnen (Stammdaten):** Vergeben Sie über **DMC Eigenschaftenvorschlag** und **Fehlende Pflicht-Merkmale zuordnen** je Eigenschaft die **DMC Eigenschafts-ID** und die **DMC Kategorie** (Notwendig/Optional). Wenn eine Eigenschaft als **Notwendig** gekennzeichnet ist, geht sie zwingend in den DMC Code ein; **Optional** gekennzeichnete Eigenschaften ergänzen den Code nur, wenn sie einen Wert haben.
3. **Eigenschaftswerte zuordnen (Stammdaten):** Vergeben Sie in den **Eigenschaftswerten** über **DMC Eigenschaftwertvorschlag** die **DMC Wert-ID**. Wenn eine Wert-ID gesetzt ist, verwendet das Modul beim Matching den codierten Wert statt des Klartexts.
4. **Matching global aktivieren (globale Einrichtung):** Setzen Sie in der **Materialeigenschaften Einrichtung** **DMC aktiviert** und **DMC Matching aktivieren** sowie die gewünschten Ebenen **DMC Artikel-Matching**, **DMC Artikevarianten-Matching**, **DMC Chargen-Matching**. Wenn eine Ebene nicht aktiviert ist, bleibt das Matching für diese Datensatzart wirkungslos.
5. **(Optional) Hintergrund-Matching (globale + benutzerbezogene Einrichtung):** Aktivieren Sie **DMC Hintergrund Matching** und setzen Sie zuvor bei mindestens einem Benutzer **Benachrichtigung bei DMC Warnungen**. Wenn aktiviert, läuft die Codeermittlung asynchron und Fehler gehen per Mail an die gekennzeichneten Benutzer.
6. **Operativer Abschluss:** Erzeugen Sie die Codes über **DMC mit Artikel matchen** / **DMC mit Artikelvariante matchen** / **DMC mit Charge matchen** auf der Materialartenkarte, oder lassen Sie die Codes im Tagesgeschäft beim Entsperren des Artikels bzw. bei der IDMC-Eingabe im Beleg automatisch ermitteln (Querverweis: **Tägliche Arbeit**).

### DMC-Dummy-Merkmale einrichten

**Prozesseinstieg:** Findet das Matching für eine Eigenschaftskombination keinen Treffer, kann das Modul bestimmte Merkmale durch einen **Dummywert** ersetzen und erneut suchen. Ein Key-User richtet ein, welche Merkmale je Materialart als Dummy zulässig sind. Die Einrichtung greift automatisch beim Matching (siehe **Tägliche Arbeit**), das Ergebnis erkennt man am Kennzeichen **IDMC ist Dummy**.

**Nummerierte Schritte:**

1. **Einstieg:** Öffnen Sie auf der **Materialartenkarte** die Aktion **IDMC-Dummy-Merkmale** (alternativ dieselbe Aktion in der Materialeigenschaften Einrichtung). Die Seite ist auf die gewählte Materialart gefiltert.
2. **Merkmale festlegen:** Erfassen Sie je Zeile das Merkmal, das ersetzt werden darf.

| Feld | Erläuterung |
|---|---|
| **Materialartencode** | Wenn gesetzt, gilt das Dummy-Merkmal für diese Materialart; auswählbar sind nur Materialarten mit einer DMC Klassen-ID. |
| **Materialartbeschreibung** | Zeigt die Beschreibung der gewählten Materialart an (nur Anzeige). |
| **Eigenschaftencode** | Wenn gesetzt, darf dieses Merkmal beim IDMC-Matching durch einen Dummywert ersetzt werden; auswählbar sind nur Merkmale der Materialart mit vergebener DMC Eigenschafts-ID. |
| **Eigenschaftenname** | Zeigt den Namen des gewählten Merkmals an (nur Anzeige). |

3. **Operativer Abschluss:** Beim automatischen Matching versucht das Modul zuerst den Treffer mit echten Werten; scheitert dieser, wird mit den hinterlegten Dummy-Merkmalen erneut gesucht. Wird so ein IDMC gefunden, setzt das Modul auf dem Datensatz das Kennzeichen **IDMC ist Dummy** (Querverweis: **Stammdaten – Artikel/Charge**).

### DMC optionale Gruppensuche einrichten

**Prozesseinstieg:** Optionale Merkmale lassen sich zu **Suchgruppen** bündeln, damit das Matching auch dann greift, wenn nicht alle optionalen Werte vorliegen. Ein Key-User definiert die Gruppen je Materialart. Die Gruppen werden beim Ermitteln des Hashwerts verwendet (siehe **Tägliche Arbeit**).

**Nummerierte Schritte:**

1. **Einstieg:** Öffnen Sie auf der **Materialartenkarte** die Aktion **DMC optionale Gruppensuche**. Die Seite **DMC optionale Suchgruppen** ist auf die Materialart gefiltert und nach Materialartencode und Gruppennr. sortiert.
2. **Gruppen bilden:** Erfassen Sie je optionalem Merkmal eine Gruppennummer.

| Feld | Erläuterung |
|---|---|
| **Materialartencode** | Wenn gesetzt, gehört die Gruppenzeile zu dieser Materialart; auswählbar sind nur Materialarten mit DMC Klassen-ID. |
| **Materialartbeschreibung** | Zeigt die Beschreibung der Materialart an (nur Anzeige). |
| **Eigenschaftencode** | Wenn gesetzt, wird dieses (optionale oder nicht kategorisierte) Merkmal in die Suchgruppe aufgenommen; auswählbar sind nur Merkmale der Materialart mit vergebener DMC Eigenschafts-ID. |
| **Eigenschaftenname** | Zeigt den Namen des Merkmals an (nur Anzeige). |
| **Gruppennr.** | Wenn gesetzt, fasst diese Nummer mehrere Merkmale zu einer Suchgruppe zusammen; findet das Matching keinen Volltreffer, probiert es die Gruppen der Reihe nach, bis ein Hashwert gefunden wird. |

3. **Operativer Abschluss:** Beim Matching bildet das Modul aus den Pflichtmerkmalen plus jeweils einer Gruppe einen Filter und ruft den Hashwert ab; die erste treffende Gruppe liefert den IDMC.

### Berechtigungen

Das Modul liefert den Berechtigungssatz **MuM DM All** mit. Dieser bestimmt die Berechtigungen für sämtliche DMC-Objekte und legt fest, welche Aktionen die Anwenderinnen und Anwender im Modul ausführen dürfen. Weisen Sie ihn den Personen zu, die DMC einrichten oder nutzen. Zusätzlich prüft das Modul beim Anmelden über das hinterlegte Bezahlmodul die Lizenz der App; ist keine gültige Lizenz vorhanden, stehen die DMC-Funktionen nicht zur Verfügung.

## Stammdaten

Die Stammdaten sind die Grundlage jeder Codeerzeugung. DMC erweitert die Karten und Übersichten des Basismoduls Materialeigenschaften sowie die Standard-Artikel- und Chargenseiten um seine Felder und Aktionen.

### Materialart (Materialartenkarte)

**Prozesseinstieg:** Die Materialart ist die zentrale Klassifizierungsstufe. Ein Key-User verbindet sie mit einer DMC-Klasse und pflegt hier die Zuordnung der Eigenschaften; alle Codeerzeugungen für Artikel, Varianten und Chargen dieser Materialart hängen davon ab. **Einstieg:** Öffnen Sie die Materialart aus der Materialarten-Übersicht des Basismoduls und rufen Sie die **Materialartenkarte** auf; die DMC-Felder liegen im Register **DMC**.

| Feld | Erläuterung |
|---|---|
| **DMC Klassen-ID** | Wenn gesetzt, ist die Materialart mit dieser DMC-Klasse des Webdienstes verbunden; erst dann sind die Matching-Aktionen bedienbar und Codes können erzeugt werden. |
| **DMC Klassen-Identifizierer** | Wenn gesetzt, enthält dieses Feld die textuelle Kennung der Klasse; sie wird in den DMC Code geschrieben und beim Zerlegen eines Codes zur Ermittlung der Materialart verwendet. |
| **Letztes Auto-Matching** | Zeigt den Zeitpunkt des letzten automatischen Matchings an; dient der Kontrolle, wann zuletzt Codes für diese Materialart ermittelt wurden. |

Aktionen der Materialartenkarte (Aktionsgruppe **DMC**):

| Aktion | Erläuterung |
|---|---|
| **DMC Eigenschaften abrufen** | Ruft die Eigenschaften der verbundenen Klasse ab und zeigt sie im **DMC Puffer** an. |
| **DMC Eigenschaftenvorschlag** | Schlägt die Zuordnung der Klasseneigenschaften zu den Eigenschaften der Materialart vor; nur bei gesetzter DMC Klassen-ID verfügbar. |
| **Fehlende Pflicht-Merkmale zuordnen** | Ordnet die noch fehlenden notwendigen Klasseneigenschaften der Materialart zu; nur bei gesetzter DMC Klassen-ID verfügbar. |
| **DMC optionale Gruppensuche** | Öffnet die **DMC optionalen Suchgruppen** für diese Materialart (siehe **DMC optionale Gruppensuche einrichten**). |
| **IDMC-Dummy-Merkmale** | Öffnet die **IDMC-Dummy-Merkmale** für diese Materialart (siehe **DMC-Dummy-Merkmale einrichten**). |
| **DMC mit Artikel matchen** | Ermittelt für alle Artikel dieser Materialart ohne IDMC Code den passenden IDMC/DMC; nur bei gesetzter DMC Klassen-ID verfügbar. |
| **DMC mit Artikelvariante matchen** | Ermittelt den IDMC/DMC für die Artikelvarianten dieser Materialart; nur bei gesetzter DMC Klassen-ID verfügbar. |
| **DMC mit Charge matchen** | Ermittelt den IDMC/DMC für die Chargen dieser Materialart; nur bei gesetzter DMC Klassen-ID verfügbar. |

> ☞ Die Matching-Aktionen setzen voraus, dass in der **Materialeigenschaften Einrichtung** **DMC Matching aktivieren** und die jeweilige Ebene (Artikel/Variante/Charge) aktiviert sind; andernfalls bricht der Lauf mit einem Feldprüf-Hinweis ab.

### Eigenschaft (Eigenschaftskarte)

**Prozesseinstieg:** Jede Eigenschaft erhält eine DMC-Kennung, damit ihr Wert in den Code einfließen kann. Ein Key-User pflegt die Kennung, sobald die Eigenschaft einer Materialart mit DMC-Klasse zugeordnet ist. **Einstieg:** Öffnen Sie die **Eigenschaftskarte** aus der Eigenschaftsübersicht des Basismoduls.

| Feld | Erläuterung |
|---|---|
| **DMC Eigenschafts-ID** | Wenn gesetzt, wird der Wert dieser Eigenschaft unter dieser Kennung in den DMC Code aufgenommen; ohne Kennung kann die Eigenschaft nicht gematcht werden. |
| **Letztes Auto-Matching** | Zeigt den Zeitpunkt der letzten automatischen Wertzuordnung an. |

Aktionen der Eigenschaftskarte:

| Aktion | Erläuterung |
|---|---|
| **DMC Eigenschaftswerte abrufen** | Ruft die möglichen Werte der Eigenschaft aus der DMC-Klasse ab; nur bei gesetzter DMC Eigenschafts-ID verfügbar. |
| **DMC Eigenschaftwertvorschlag** | Schlägt je Eigenschaftswert die passende DMC Wert-ID vor; nur bei gesetzter DMC Eigenschafts-ID verfügbar. |

### Eigenschaftswerte

**Prozesseinstieg:** Für Eigenschaften mit fester Wertetabelle ordnet ein Key-User jedem Wert eine DMC-Wertkennung zu, damit der codierte Wert statt des Klartexts in den Code geschrieben wird. **Einstieg:** Öffnen Sie von der **Eigenschaftskarte** die **Eigenschaftswerte**.

| Feld | Erläuterung |
|---|---|
| **DMC Wert-ID** | Wenn gesetzt, verwendet das Matching für diesen Eigenschaftswert die codierte Wertkennung; ohne Wert-ID geht der Klartextwert in den Filter ein. |

Aktion: **DMC Eigenschaftwertvorschlag** — schlägt die DMC Wert-IDs für die Werte der gewählten Eigenschaft vor und aktualisiert die Zeilen.

### Datensatzeigenschaften

**Prozesseinstieg:** Die **Datensatzeigenschaften** sind die konkreten Eigenschaftszeilen eines Datensatzes (Materialart, Artikel, Variante, Charge). DMC ergänzt hier die codebildenden Kennungen, die aus der Materialart-Zuordnung übernommen werden. Ein Key-User kontrolliert diese Werte; im Regelfall werden sie über **DMC-Felder mit Datensatz-Eigenschaften synchronisieren** aus der Materialart gesetzt. **Einstieg:** Öffnen Sie die **Datensatzeigenschaften** über die Eigenschaftserfassung des jeweiligen Datensatzes.

| Feld | Erläuterung |
|---|---|
| **DMC Eigenschafts-ID** | Wenn gesetzt, geht der Wert dieser Datensatzeigenschaft unter dieser Kennung in den DMC Code ein. |
| **DMC Kategorie** | Legt fest, wie das Merkmal in den Code eingeht. **(leer):** keine DMC-Zuordnung, das Merkmal fließt nicht in den Code ein. **Optional:** das Merkmal wird nur aufgenommen, wenn es einen Wert hat, und kann bei der Gruppensuche entfallen. **Notwendig:** das Merkmal ist Pflicht und muss beim Matching übereinstimmen. |

### Artikel und Artikelvariante (Artikelkarte, Artikelvariantenkarte)

**Prozesseinstieg:** Am Artikel und an der Artikelvariante speichert DMC die erzeugten Codes und steuert das Überprüfungszeichen. Ein Key-User pflegt bzw. prüft diese Felder; die Codes entstehen automatisch beim Entsperren des Artikels oder über die Matching-Aktionen der Materialart. **Einstieg:** Öffnen Sie die **Artikelkarte** aus der **Artikelübersicht** bzw. die **Artikelvariantenkarte** aus den **Artikelvarianten**.

| Feld | Erläuterung |
|---|---|
| **IDMC Code** | Wenn gesetzt, ist dem Datensatz dieser Kurzcode zugeordnet; er wird in Belegzeilen zur automatischen Auflösung genutzt und ist die Grundlage der Barcodeerzeugung. Ein doppelt vergebener IDMC an Artikel oder Variante wird beim Speichern mit einem Fehler verhindert. |
| **DMC Code** | Wenn gesetzt, enthält der Datensatz den vollständigen DMC Code; er wird aus den Datensatzeigenschaften bzw. vom Webdienst ermittelt. |
| **DMC Überprüfungszeichen verwenden** | Wenn aktiviert, hängt das Modul dem erzeugten IDMC/DMC das in der Einrichtung hinterlegte Überprüfungszeichen an; so werden Zeilen mit diesem Code später als überprüfungspflichtig erkannt. Ohne das Kennzeichen bleibt der Code ohne Zusatzzeichen. |
| **IDMC ist Dummy** | Wenn gesetzt, wurde der IDMC nur mithilfe konfigurierter Dummywerte gefunden (siehe **DMC-Dummy-Merkmale einrichten**); dies signalisiert, dass der Code nicht aus echten, sondern aus ersatzweisen Werten stammt. |

> ☞ Auf der **Artikelkarte** zeigt die Infobox **IDMC Barcodes** das zum IDMC Code gehörende Barcodebild an (siehe **Barcodes**). Die **Artikelvariantenkarte** trägt dieselben vier DMC-Felder wie die Artikelkarte.

### Charge (Chargennr.-Informationskarte)

**Prozesseinstieg:** An der Charge speichert DMC die chargenspezifischen Codes; sie entstehen beim Chargen-Matching oder durch Eingabe eines IDMC Code auf der Chargennr.-Informationskarte. **Einstieg:** Öffnen Sie die **Chargennr.-Informationskarte** aus der **Chargennr.-Informationsübersicht**.

| Feld | Erläuterung |
|---|---|
| **IDMC Code** | Wenn Sie hier einen IDMC Code eintragen, ermittelt das Modul die zugehörigen Eigenschaftswerte vom Webdienst, prüft die Materialart des Artikels und schreibt die Werte in die Datensatzeigenschaften der Charge (nur solange kein offener Artikelposten die Charge sperrt); die Beschreibung wird ergänzt und die Barcodes werden erzeugt. |
| **DMC Code** | Wenn gesetzt, enthält die Charge den vollständigen DMC Code. |
| **DMC Überprüfungszeichen verwenden** | Wenn aktiviert, erhält der erzeugte Code der Charge das Überprüfungszeichen (siehe Einrichtung). |
| **IDMC ist Dummy** | Wenn gesetzt, wurde der IDMC der Charge über Dummywerte ermittelt. |

> ☞ Eine Chargeneigenschaft kann nicht als reine Verkaufseigenschaft gesetzt werden; das Modul verhindert dies mit einem Hinweis. Ebenso lässt sich eine nicht als Chargeneigenschaft gekennzeichnete Eigenschaft nicht aus der Charge heraus ändern.

## Überblicks- und Listenseiten

Für die schnelle Orientierung ergänzt DMC die wichtigsten Übersichten um Spalten. Die Erweiterung fügt ausschließlich **Spalten** hinzu; sie führt keine zusätzlichen Filterfelder in den Anfragebereich der Listen ein.

### Artikelübersicht, Artikelvarianten, Chargennr.-Informationsübersicht

Jede dieser Übersichten zeigt zusätzlich dieselben vier Spalten:

| Feld | Erläuterung |
|---|---|
| **IDMC Code** | Zeigt den zugeordneten Kurzcode je Zeile; aktualisiert sich, sobald ein Matching oder eine manuelle Eingabe den Code setzt. |
| **DMC Code** | Zeigt den vollständigen Code je Zeile. |
| **DMC Überprüfungszeichen verwenden** | Zeigt an, ob für diesen Datensatz das Überprüfungszeichen an den Code angehängt wird. |
| **IDMC ist Dummy** | Zeigt an, ob der IDMC über Dummywerte gefunden wurde. |

### IDMC Liste

Die **IDMC Liste** ist eine technische Übersicht der ermittelten IDMC-Puffereinträge mit den Spalten **Hashwert**, **Name**, **Artikelnr.**, **Variantencode**, **Chargennr.** und **Verknüpfte Datensatz-ID**. Sie ist nicht über **Suchen** auffindbar (interne Diagnoseansicht) und dient der Kontrolle der Zuordnungen.

## Tägliche Arbeit

Im Tagesgeschäft berührt DMC vor allem die **Belegzeilen** des Verkaufs und Einkaufs sowie die Ermittlungsdialoge. Das Modul hat keinen eigenen Buchungs- oder Freigabelauf; es füllt die Zeile und übergibt danach an die Standardverarbeitung.

**Bezug zur Einrichtung:** Damit die IDMC-Eingabe wirkt, müssen in der **Materialeigenschaften Einrichtung** **DMC aktiviert** und **DMC Matching aktivieren** gesetzt sein, die Materialart eine **DMC Klassen-ID** besitzen und die Eigenschaften/Werte ihre **DMC Eigenschafts-ID** bzw. **DMC Wert-ID** tragen (Querverweis: **Einrichtung – DMC-Matching einrichten**).

### Verkaufszeilen (Verkaufsauftrag, Verkaufsangebot, Rahmenauftrag)

DMC ergänzt die Zeilen des **Verkaufsauftrags**, des **Verkaufsangebots** und des **Rahmenauftrags** um:

| Feld | Erläuterung |
|---|---|
| **IDMC Code** | Wenn Sie in eine offene, noch nicht gelieferte Zeile einen IDMC Code eingeben, sucht das Modul der Reihe nach nach passenden Chargen mit Bestand, dann nach Artikelvarianten und Artikeln, und setzt **Art**, **Nr.** und ggf. **Variantencode** automatisch. Gibt es mehrere Treffer, öffnet sich die Artikel- bzw. Variantenauswahl zur Übernahme. |
| **DMC-Überprüfung erforderlich** | Wenn gesetzt, endete der eingegebene Code auf das Überprüfungszeichen; das Modul entfernt das Zeichen, kennzeichnet die Zeile als überprüfungspflichtig und meldet „Der DMC muss überprüft werden!“. |

Ablauf der IDMC-Eingabe in der Verkaufszeile (aus dem Code abgeleitet):

1. Öffnen Sie den **Verkaufsauftrag** und legen Sie eine neue Zeile an.
2. Tragen Sie in das Feld **IDMC Code** den gescannten oder erhaltenen Code ein (die Zeile muss offen und darf noch nicht geliefert sein).
3. Findet das Modul **Chargen mit Bestand** zum IDMC, wird die Zeile mit deren Artikel/Variante gefüllt.
4. Findet es keine Charge mit Bestand, prüft es Chargen ohne Bestand, dann eindeutige Artikelvarianten, dann Artikel; bei Mehrdeutigkeit erscheint die **Artikelvarianten-** bzw. **Artikelauswahl**.
5. Führt keine Zuordnung zum Ziel, zerlegt das Modul den DMC (bzw. holt ihn per Webdienst) und startet die Eigenschaftssuche. Bei fehlendem Volltreffer erscheint die Rückfrage **„Kein Match für alle Eigenschaften gefunden. Soll die Suche nur mit den MUSS-Eigenschaften durchgeführt werden?“**.
6. Reicht der gefundene Bestand nicht oder liegt er nicht am Lagerort, erscheint die Rückfrage **„Es wurde nicht genug Bestand oder auf dem gewählten Lagerort gefunden.“**; bei Bestätigung wird ohne Lager-/Mengenfilter erneut gesucht.
7. Die Zeile ist mit **Artikel**/**Variante** und dem IDMC Code gefüllt; die eigentliche Buchung erfolgt anschließend über die Standardaktionen von Business Central.

### Einkaufszeilen (Bestellung, Einkaufsanfrage, Rahmenbestellung)

DMC ergänzt die Zeilen der **Bestellung**, der **Einkaufsanfrage** und der **Rahmenbestellung** um dieselben zwei Felder **IDMC Code** und **DMC-Überprüfung erforderlich**. Wählen Sie in einer Einkaufszeile einen **Artikel** (Feld **Nr.**) oder einen **Variantencode**, übernimmt das Modul automatisch den **IDMC Code** und das Kennzeichen **DMC-Überprüfung erforderlich** aus dem Artikel bzw. der Variante. So ist der Code bereits bei der Beschaffung an der Zeile sichtbar.

### Ermittlungs- und Auswahldialoge

Beim Abrufen und Übernehmen von Klassen, Eigenschaften und Werten öffnen sich mehrere Dialogseiten:

#### DMC Puffer

Der **DMC Puffer** zeigt Klassen, Eigenschaften, Werte und Übersetzungen als aufklappbaren Baum (eingerückt nach Ebene, farblich abgestuft). Er dient der Auswahl und Übernahme der gewünschten Zeilen.

| Feld | Erläuterung |
|---|---|
| **Ausgewählt** | Zeigt an, ob die Zeile markiert ist (nur Anzeige). |
| **Name** | Bezeichnung der Klasse, Eigenschaft oder des Werts. |
| **Wert** | Der zugehörige Wert. |
| **Art** | Art der Zeile im Baum. **(leer):** keine Zuordnung. **Klasse:** eine DMC-Klasse. **Klassengruppe / Klassensubstanzgruppe:** Gruppierungen der Klasse. **Klasseneigenschaft:** eine Eigenschaft der Klasse. **Eigenschaftswert:** ein möglicher Wert. **Klassenübersetzung / Klasseneigenschaftsübersetzung / Eigenschaftswert-Übersetzung:** sprachliche Übersetzungen der jeweiligen Ebene. |
| **Sprache** | Sprachkennung bei Übersetzungszeilen. |
| **Eigenschaftskategorie** | Kategorie der Eigenschaft (Notwendig/Optional). |
| **Verknüpfter Datensatz** | Zeigt den bereits verknüpften Business-Central-Datensatz; über **Bearbeiten** springen Sie in die zugehörige Datensatzeigenschaftenseite. |

Aktionen des DMC Puffers:

| Aktion | Erläuterung |
|---|---|
| **Eigenschaften abrufen** | Lädt die Eigenschaften der markierten Klasse nach. |
| **Von Auswahl erstellen** | Legt aus den markierten Zeilen die Materialart, Eigenschaften, Werte bzw. Übersetzungen in Business Central an oder ändert sie; anschließend werden vorgeschlagene Änderungen in **Geänderte Werte** zur Bestätigung angezeigt. |
| **Zeilen auswählen** | Markiert die aktuelle Auswahl (Tastenkürzel Strg+1). |
| **Auswahl aufheben** | Hebt die Markierung auf (Strg+2). |
| **Alle Zeilen anzeigen** | Zeigt alle Zeilen (Strg+3). |
| **Auswahl anzeigen** | Zeigt nur markierte Zeilen (Strg+4). |

#### DMC Vorschlag

Der **DMC Vorschlag** listet die vom Webdienst vorgeschlagenen Zuordnungen (Eigenschafts-ID, Wert-ID, Name, Eigenschaftencode/-name und **Trefferanzahl**). Anhand der Trefferanzahl erkennen Sie, wie sicher ein Vorschlag ist, bevor Sie ihn übernehmen.

#### Geänderte Werte

Nach **Von Auswahl erstellen** zeigt die Seite **Geänderte Werte** die anstehenden Änderungen mit **Alter Wert**, **Neuer Wert**, **Herkunftstabelle** und **Herkunftsdatensatz**. Über die **Änderungsoption** entscheiden Sie je Zeile:

| Feld | Erläuterung |
|---|---|
| **Änderungsoption** | **(leer):** die Änderung wird nicht übernommen. **Akzeptieren:** der neue Wert wird beim Verlassen der Seite in den Herkunftsdatensatz geschrieben. |

## Barcodes

Zu jedem **IDMC Code** legt das Modul automatisch Barcodebilder an, sobald der Code erzeugt oder ergänzt wird. Die Seite **IDMC Barcodes** und die gleichnamige Infobox auf der Artikelkarte zeigen die Bilder an.

| Feld | Erläuterung |
|---|---|
| **IDMC Code** | Der Code, zu dem der Barcode gehört. |
| **Barcodeart** | Art des Barcodes. **Code 39:** ein linearer Strichcode. **QR Code:** ein zweidimensionaler Matrixcode. Zu jedem IDMC wird je Barcodeart genau ein Bild erzeugt. |
| **Bild** | Das gerenderte Barcodebild (vom Webdienst geliefert und als Bild gespeichert). |

## Gebuchte Belege und Historie

Die IDMC-Kennzeichnung bleibt über die Buchung erhalten. DMC ergänzt die Zeilen der **gebuchten** Verkaufs- und Einkaufsbelege — gebuchte Verkaufslieferung, -rechnung und -gutschrift, gebuchter Wareneingang, gebuchte Einkaufsrechnung und -gutschrift, gebuchte Verkaufs- und Einkaufsretouren — sowie die Belegarchive um die Spalten **IDMC Code** und **DMC-Überprüfung erforderlich** (nur Anzeige). So ist auch im Nachhinein nachvollziehbar, mit welchem Code eine Zeile erfasst wurde und ob sie überprüfungspflichtig war.

## FAQ und Troubleshooting

### 1. Warum sind die DMC-Aktionen auf der Materialeigenschaften Einrichtung ausgegraut?

Die Aktionsgruppe **DMC** ist nur bei gesetztem Kennzeichen **DMC aktiviert** bedienbar. Aktivieren Sie das Kennzeichen und hinterlegen Sie Url, Benutzer und Passwort.

### 2. Warum meldet die Eingabe eines Codes „Die Eingabe ist kein gültiger IDMC“?

Der eingegebene Code beginnt nicht mit dem in der Einrichtung hinterlegten **DMC-Präfix** oder konnte vom Webdienst nicht aufgelöst werden. Prüfen Sie Präfix und Trennzeichen in der **Materialeigenschaften Einrichtung**.

### 3. Was passiert, wenn das Matching keinen vollständigen Treffer findet?

Das Modul fragt „Soll die Suche nur mit den MUSS-Eigenschaften durchgeführt werden?“. Bestätigen Sie, um mit den notwendigen Eigenschaften weiterzusuchen; alternativ hinterlegen Sie **DMC-Dummy-Merkmale** oder eine **DMC optionale Gruppensuche**.

### 4. Warum lässt sich das DMC Hintergrund Matching nicht aktivieren?

Für das Hintergrund-Matching muss mindestens ein Benutzer in der **Benutzer Einrichtung** das Kennzeichen **Benachrichtigung bei DMC Warnungen** tragen. Ohne einen solchen Benutzer verhindert das Modul das Aktivieren mit einem Hinweis.

### 5. Warum erhält ein Artikel keinen IDMC/DMC Code?

Prüfen Sie, ob **DMC Matching aktivieren** und die passende Ebene (**DMC Artikel-Matching**) gesetzt sind, ob die Materialart eine **DMC Klassen-ID** besitzt und ob die notwendigen Eigenschaften eine **DMC Eigenschafts-ID** und einen Wert haben.

### 6. Was bedeutet das Kennzeichen „IDMC ist Dummy“ am Datensatz?

Der IDMC wurde nicht mit den echten Werten, sondern über konfigurierte **Dummy-Merkmale** gefunden. Der Code ist damit ein Ersatztreffer; prüfen Sie die Werte, wenn die Zuordnung eindeutig sein muss.

### 7. Warum erscheint der Hinweis „Der DMC muss überprüft werden!“?

Der eingegebene bzw. erzeugte Code endete auf das **DMC Überprüfungszeichen**. Das Modul entfernt das Zeichen und markiert die Zeile mit **DMC-Überprüfung erforderlich**. Prüfen Sie die betroffene Zeile.

### 8. Warum meldet das System „Es gibt einen Eintrag mit demselben IDMC“?

Ein IDMC Code darf je Artikel bzw. Artikelvariante nur einmal vergeben sein. Das Modul verhindert Duplikate beim Speichern. Suchen Sie den bereits vorhandenen Datensatz und bereinigen Sie die doppelte Vergabe.

### 9. Warum lässt sich eine Chargeneigenschaft nicht ändern oder als Verkaufseigenschaft setzen?

Eine nicht als Chargeneigenschaft gekennzeichnete Eigenschaft kann nicht aus der Charge heraus geändert werden, und eine Chargeneigenschaft kann nicht als reine Verkaufseigenschaft gesetzt werden. Passen Sie die Kennzeichen der Eigenschaft in der Materialart-Zuordnung an.

### 10. Warum verweigert das Modul weitere Abrufe („keine DMC Lizenzwerte mehr“)?

Die **DMC gekaufte Lizenzanzahl** ist aufgebraucht (**DMC Restlizenzanzahl** = 0). Erhöhen Sie das Kontingent bzw. erwerben Sie eine neue Lizenz; über **DMC Lizenzwarnung bei** lässt sich rechtzeitig vor dem Aufbrauchen warnen.

## Typische Anwendungsfälle

Die folgenden Szenarien sind aus dem geprüften Verhalten des Moduls abgeleitet.

### Anwendungsfall 1: Neue Materialart mit DMC-Klasse verbinden und Artikel codieren

- **Auslöser:** Der Metalldatendienst hat eine neue Werkstoffklasse; ein Key-User soll die zugehörigen Artikel mit DMC-Codes versehen.
- **Einstieg in BC:** Materialart aus der Materialarten-Übersicht öffnen → **Materialartenkarte**, Register **DMC**.
- **Kernablauf:** Über **DMC Klassen anzeigen** die Klasse wählen (**DMC Klassen-ID**/**-Identifizierer** werden gesetzt) → **DMC Eigenschaftenvorschlag** → **Fehlende Pflicht-Merkmale zuordnen** → in den **Eigenschaftswerten** über **DMC Eigenschaftwertvorschlag** die **DMC Wert-ID** vergeben → **DMC mit Artikel matchen**. Die Artikel erhalten **IDMC Code** und **DMC Code**.
- **Abschluss:** Auf der **Artikelkarte** zeigt die Infobox **IDMC Barcodes** den erzeugten Barcode; in der **Artikelübersicht** sind die neuen Codespalten gefüllt.

### Anwendungsfall 2: Charge im Wareneingang per IDMC anreichern

- **Auslöser:** Zu einer eingehenden Charge liegt ein IDMC (Etikett/Scan) vor; die Chargeneigenschaften sollen automatisch gesetzt werden.
- **Einstieg in BC:** **Chargennr.-Informationskarte** der Charge öffnen.
- **Kernablauf:** In das Feld **IDMC Code** den Code eingeben. Das Modul holt den DMC vom Webdienst, prüft die Materialart des Artikels, schreibt die Werte in die **Datensatzeigenschaften** der Charge (solange kein offener Artikelposten die Charge sperrt) und ergänzt die Beschreibung.
- **Abschluss:** Die Charge trägt **IDMC Code**/**DMC Code**; die Barcodes stehen bereit. Weicht die Materialart des Artikels von der Klasse des Codes ab, bricht der Vorgang mit einem Hinweis ab.

### Anwendungsfall 3: Verkaufszeile per gescanntem IDMC füllen

- **Auslöser:** Ein Kunde übermittelt einen IDMC/Barcode statt einer Artikelnummer.
- **Einstieg in BC:** **Verkaufsauftrag** öffnen, neue Zeile.
- **Kernablauf:** In das Feld **IDMC Code** den Code eingeben. Das Modul sucht zuerst Chargen mit Bestand, dann Varianten und Artikel; bei Mehrdeutigkeit erscheint die Auswahlseite. Rückfragen zu MUSS-Eigenschaften und Bestand/Lagerort werden bei Bedarf eingeblendet. Endet der Code auf das Überprüfungszeichen, wird die Zeile als **DMC-Überprüfung erforderlich** markiert.
- **Abschluss:** Die Zeile ist mit **Artikel**/**Variante** und **IDMC Code** gefüllt; die Buchung erfolgt über die Standardaktionen von Business Central.
