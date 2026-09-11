---
title: Anwenderhandbuch m+m Label Management with Package Management
---

# Anwenderhandbuch m+m Label Management with Package Management

## Einleitung

Die App **m+m Label Management with Package Management** verbindet die beiden Module **m+m Label Management** (Etiketten- und Barcodedruck) und **m+m Package Management** (Packmittelverwaltung) in Microsoft Dynamics 365 Business Central. Sie ist eine reine Integrations-Erweiterung: Sie fügt keine eigenen Karten, Listen oder Belege hinzu, sondern erweitert bestehende Seiten der beiden Basismodule um einige wenige Felder und sorgt dafür, dass **Packmittel-Informationen automatisch auf Etiketten und in Barcodes** übernommen werden.

Der Nutzen für den Anwender: Beim Etikettendruck aus einem Lager- oder Belegprozess müssen die Packmittelangaben (z. B. **Paketnr.**, **Paketcode**, **Paketgruppennr** oder die **Menge im Paket**) nicht mehr manuell erfasst werden. Sie werden aus den Packmitteldaten des Belegs ermittelt und an der im Etikettenlayout hinterlegten Position ausgegeben. Zusätzlich lässt sich pro Packmittel ein **Etikettentypcode** festlegen, der beim Erzeugen der Belegpackmittel weitervererbt wird.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender**, die im Tagesgeschäft Packmittel erzeugen und Etiketten drucken – etwa im Wareneingang, Warenausgang, in der Kommissionierung oder Verpackung. Sekundär angesprochen sind **Administratoren und Key-User**, die im Modul **m+m Label Management** die Etikettentypen und deren Felder einrichten sowie in **m+m Package Management** die Packmittelstammdaten (Packmittelreferenzen und Packmittelstücklisten) pflegen.

**Voraussetzung.** Diese App setzt die installierten und eingerichteten Basismodule **m+m Label Management** und **m+m Package Management** sowie **m+m Cloud Base** voraus. Die Einrichtung der Etikettentypen, Berichte, Barcodes und Standardwerte erfolgt vollständig im Modul **m+m Label Management**; die Anlage von Packmitteln, Packmittelreferenzen und Packmittelstücklisten im Modul **m+m Package Management**. Dieses Handbuch beschreibt ausschließlich die **zusätzlichen Felder und die automatische Verknüpfung**, die durch die Integrations-App entstehen.

### Prozessüberblick

1. **Einrichtung (Administrator):** In den Feldern eines Etikettentyps bzw. eines Barcodefelds wird über das neue Feld **Paketfeld** festgelegt, welche Packmittelinformation gedruckt werden soll.
2. **Stammdaten (Key-User):** In der **Packmittelstückliste** und in den **Packmittelreferenzen** wird je Packmittel ein **Etikettentypcode** hinterlegt.
3. **Tägliche Arbeit (Anwender):** Beim Erzeugen der Belegpackmittel (z. B. aus einer Packmittelstückliste oder einer Packmittelreferenz) wird der **Etikettentypcode** automatisch auf das Belegpackmittel übernommen.
4. **Ausgabe:** Beim Etikettendruck zu einem Lager- oder Verkaufs-/Einkaufsbeleg werden die eingestellten **Paketfeld**-Werte je Packmittel ermittelt und auf Etikett bzw. Barcode ausgegeben.

## Schnellstart für Anwender

Der schnellste Weg zum bedruckten Etikett mit Packmittelangaben – in Reihenfolge der Abhängigkeiten:

1. **Einrichtung prüfen (einmalig, Administrator).** Öffnen Sie über die Suchfunktion (**Suchen**) die Seite **Labelart-Felder**. Setzen Sie in der gewünschten Zeile das Feld **Paketfeld** auf die Packmittelinformation, die gedruckt werden soll (z. B. **Paketnr.**). Für ein Feld vom Typ **Barcode** verwenden Sie stattdessen die Seite **Label Barcodefelder** und dort ebenfalls das Feld **Paketfeld**.
2. **Etikettentyp am Packmittel hinterlegen (Key-User).** Tragen Sie in der **Packmittelstückliste** (bzw. in den **Packmittelreferenzen**) im Feld **Etikettentypcode** den passenden Etikettentyp ein.
3. **Belegpackmittel erzeugen (Anwender).** Erzeugen Sie im Belegprozess die Packmittel wie gewohnt aus der Packmittelstückliste bzw. Packmittelreferenz. Der **Etikettentypcode** wird dabei automatisch auf das jeweilige Belegpackmittel übernommen.
4. **Etikett drucken (Anwender).** Stoßen Sie den Etikettendruck im gewohnten Lager-/Belegprozess an. Die App ermittelt je Packmittel die unter **Paketfeld** eingestellten Werte und gibt sie auf Etikett bzw. Barcode aus. Prüfen Sie das Ergebnis in der Etikettenvorschau des Basismoduls.

**Wichtig:** Es werden nur dann Packmittelwerte gedruckt, wenn im Prozess auch die entsprechenden Packmittelfelder gepflegt sind. Fehlen die Packmitteldaten, bleibt die Etikettenposition leer.

## Einrichtung

Die eigentliche Etiketten-Einrichtung (Etikettentypen, Berichte, Barcodes, Standardwerte, Barcode-Trennzeichen) erfolgt vollständig im Basismodul **m+m Label Management** und ist dort dokumentiert. Die Integrations-App ergänzt an **zwei** Einrichtungsseiten jeweils **ein** Feld: **Paketfeld**. Über dieses Feld steuert der Administrator, welche Packmittelinformation beim Druck an der jeweiligen Feldposition erscheint.

Beide Seiten sind unternehmensweite Einrichtungsseiten des Etikettenmoduls und werden – wie im Basismodul üblich – über die Business-Central-Suchfunktion (**Suchen**) geöffnet. Sie sind einem Etikettentyp zugeordnet; die dort gepflegten Zeilen bestimmen, welche Felder in welcher Reihenfolge auf das Etikett bzw. in den Barcode geschrieben werden.

### Paketfeld auf einem Etikettentyp einrichten

**Prozesseinstieg.** Diese Einrichtung nimmt der **Administrator** einmalig vor, bevor Anwender Etiketten mit Packmittelangaben drucken. Sie ergänzt die Feldliste eines Etikettentyps um eine Packmittelquelle. Die hier getroffene Auswahl wird später im Tagesablauf beim Etikettendruck (Abschnitt **Lager, Belege und Etikettendruck**) automatisch ausgewertet.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Labelart-Felder**.

Auf der Seite **Labelart-Felder** pflegt der Administrator je Etikettentyp und Label-Prozess eine oder mehrere Feldzeilen. Diese Zeilen stammen aus dem Basismodul; die Integrations-App fügt in derselben Zeile das Feld **Paketfeld** hinzu. Der Anwender sieht eine einzige Seite mit Basis- und Erweiterungsfeldern.

| Feld | Erläuterung |
|------|-------------|
| **Etikettentypcode** | Ordnet die Zeile einem Etikettentyp zu. Wenn gesetzt, gilt die Feldbelegung für alle Etiketten dieses Typs. |
| **Label Prozess** | Ordnet die Zeile einem Etikettenprozess zu (z. B. Warenannahme, Warenausgang). Wenn gesetzt, wird die Zeile nur in diesem Prozess ausgewertet. |
| **Berichtsfeldart** | Legt fest, ob es sich um ein Textfeld oder ein **Barcode**-Feld handelt. Wenn **Barcode** gewählt ist, wird das Feld **Paketfeld** an dieser Stelle deaktiviert; die Packmittelquelle für Barcodes wird stattdessen auf der Seite **Label Barcodefelder** gepflegt. |
| **Tabellennr.** / **Feldnr.** | Quelltabelle und -feld, aus dem der Standardwert gelesen wird. Wenn eine Tabelle/Feld gesetzt ist, druckt das Basismodul diesen Feldwert. |
| **Benutz. Wert** | Fester Textwert, der anstelle eines Tabellenfelds gedruckt wird. Wenn gefüllt, hat er Vorrang: Beim Setzen von **Paketfeld** wird ein vorhandener **Benutz. Wert** entfernt, damit sich Packmittelquelle und Freitext nicht überlagern. |
| **Paketfeld** | Steuert, welche Packmittelinformation auf das Etikett gedruckt wird. Wenn ein Wert außer **(leer)** gesetzt wird, ermittelt die App beim Druck den entsprechenden Packmittelwert je Packmittel und schreibt ihn an diese Feldposition. Beim Wechsel des Werts werden abhängige Tabellen-/Feldbezüge bzw. ein vorhandener **Benutz. Wert** nach Rückfrage geleert, damit pro Zeile genau eine Quelle aktiv ist. |

**Werte des Feldes „Paketfeld" (Task-relevant):**

- **(leer):** Es wird kein Packmittelwert ausgegeben; die Zeile verhält sich wie im Basismodul (Tabellenfeld oder **Benutz. Wert**).
- **Paketnr.:** Beim Druck wird die Paketnummer des jeweiligen Belegpackmittels ausgegeben.
- **Paketcode:** Beim Druck wird der Paketcode des Belegpackmittels ausgegeben.
- **Menge im Paket:** Beim Druck wird die zu bearbeitende Menge des Belegpackmittels (Feld **Zu bearbeitende Menge**) als Mengenangabe ausgegeben.
- **Paketgruppennr:** Beim Druck wird die Paketgruppennummer des Belegpackmittels ausgegeben (Zusammenfassung mehrerer Pakete zu einer Gruppe).

**Ablauf.**
1. **Zuerst** wählen Sie die Zeile des gewünschten Etikettentyps und Prozesses (Feld **Etikettentypcode** / **Label Prozess**).
2. **Danach** setzen Sie in dieser Zeile **Paketfeld** auf die gewünschte Packmittelquelle.
3. **Schließlich** prüft der Anwender in der Etikettenvorschau des Basismoduls, an welcher Position der Packmittelwert erscheint.

**Abhängigkeitshinweis.** Das Feld **Paketfeld** ist gesperrt, sobald die **Berichtsfeldart** den Wert **Barcode** hat – für Barcodes verwenden Sie die Seite **Label Barcodefelder** (siehe unten). Wird ein **Benutz. Wert** erfasst, entfernt das System nach Rückfrage einen zuvor gesetzten **Paketfeld**-Wert und umgekehrt; so bleibt pro Feldzeile genau eine Wertquelle wirksam.

### Paketfeld in einem Barcodefeld einrichten

**Prozesseinstieg.** Diese Einrichtung nimmt der **Administrator** vor, wenn eine Packmittelinformation nicht als Klartext, sondern **innerhalb eines Barcodes** gedruckt werden soll. Ein Barcode setzt sich aus mehreren Barcodefeldern zusammen; jedes Feld kann eine eigene Quelle haben. Die hier getroffene Auswahl wird beim Etikettendruck (Abschnitt **Lager, Belege und Etikettendruck**) in den zusammengesetzten Barcode-Inhalt eingefügt.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Label Barcodefelder**.

Auch diese Seite stammt aus dem Basismodul; die Integrations-App ergänzt das Feld **Paketfeld** in derselben Zeile.

| Feld | Erläuterung |
|------|-------------|
| **Etikettentypcode** | Ordnet das Barcodefeld einem Etikettentyp zu. Wenn gesetzt, wird der Barcode für Etiketten dieses Typs erzeugt. |
| **Label Prozess** | Ordnet das Barcodefeld einem Etikettenprozess zu. Wenn gesetzt, wird das Feld nur in diesem Prozess ausgewertet. |
| **Tabellennr.** / **Feldnr.** | Quelltabelle und -feld für den Barcode-Bestandteil. Wenn gesetzt, fließt dieser Feldwert in den Barcode ein. |
| **Benutz. Wert** | Fester Textbestandteil des Barcodes. Wenn gefüllt, wird beim Setzen von **Paketfeld** der zuvor eingestellte Packmittelwert entfernt, damit der Barcode-Bestandteil eindeutig ist. |
| **Paketfeld** | Steuert, welche Packmittelinformation als Bestandteil in den Barcode geschrieben wird. Wenn ein Wert außer **(leer)** gesetzt wird, hängt die App beim Druck den ermittelten Packmittelwert an den Barcode-Inhalt an; die Bestandteile werden mit dem Trennzeichen des Barcodetyps verbunden und anschließend als Barcode codiert. |

**Werte des Feldes „Paketfeld" im Barcode:**

- **(leer):** Es wird kein Packmittelwert in den Barcode aufgenommen.
- **Paketnr.:** Die Paketnummer wird als Barcode-Bestandteil aufgenommen.
- **Paketcode:** Der Paketcode wird als Barcode-Bestandteil aufgenommen.
- **Menge im Paket:** Die zu bearbeitende Menge (**Zu bearbeitende Menge**) wird als Barcode-Bestandteil aufgenommen.
- **Paketgruppennr:** Die Paketgruppennummer wird als Barcode-Bestandteil aufgenommen.

**Abhängigkeitshinweis.** Wird in der Zeile die Quelltabelle (**Tabellennr.**) oder der **Benutz. Wert** geändert, setzt das System den zuvor eingestellten **Paketfeld**-Wert automatisch zurück. So ist je Barcode-Bestandteil immer eindeutig, ob er aus einem Tabellenfeld, einem Freitext oder einer Packmittelquelle stammt.

## Stammdaten

Neben den Einrichtungsfeldern ergänzt die Integrations-App das Feld **Etikettentypcode** auf zwei **Packmittel-Stammdatenseiten** des Moduls m+m Package Management. Über dieses Feld wird festgelegt, welcher Etikettentyp später für die aus diesem Packmittel erzeugten Belegpackmittel gilt. Der **Etikettentypcode** verweist jeweils auf einen im Modul m+m Label Management gepflegten Etikettentyp (Seite **Labelarten**).

### Etikettentyp in der Packmittelstückliste hinterlegen

**Prozesseinstieg.** Diese Stammdaten pflegt der **Key-User** beim Aufbau der Packmittelstücklisten – also bevor im Tagesgeschäft Packmittel aus einer Stückliste erzeugt werden. Der hier gepflegte **Etikettentypcode** bestimmt, welcher Etikettentyp beim Erzeugen der Belegpackmittel aus dieser Stückliste übernommen wird (siehe **Tägliche Arbeit**).

**Einstieg:** Öffnen Sie über **Suchen** die **Packmittelstückliste** und wählen Sie die gewünschte Stückliste; die Positionen werden im Unterformular **Packmittelstücklistenzeilen** angezeigt.

Die Packmittelstückliste (Seite **Packmittelstückliste**) besitzt einen Kopf mit **Status** und ein Zeilen-Unterformular. Die Integrations-App ergänzt in den Zeilen die Spalte **Etikettentypcode**.

| Feld | Erläuterung |
|------|-------------|
| **Packmittelcode** | Kennzeichnet die Packmittelposition der Zeile (aus dem Basismodul). |
| **Zeilenart** | Unterscheidet Packmittel- und Artikelzeilen. **Packmittel:** die Zeile beschreibt ein Packmittel – nur hier ist der **Etikettentypcode** pflegbar. **Artikel:** die Zeile beschreibt einen im Packmittel enthaltenen Artikel – der **Etikettentypcode** wird hier nicht direkt erfasst, sondern automatisch vom übergeordneten Packmittel abgeleitet. |
| **Beschreibung** / **Menge** | Bezeichnung und Menge der Zeile (aus dem Basismodul). |
| **Etikettentypcode** | Wenn in einer Packmittelzeile ein Etikettentyp gesetzt wird, dann übernehmen alle **Artikelzeilen** desselben Packmittels automatisch denselben **Etikettentypcode**; beim späteren Erzeugen der Belegpackmittel wird dieser Etikettentyp mitgeführt. Das Feld ist nur editierbar, wenn die **Zeilenart** den Wert **Packmittel** hat. |

**Ablauf.**
1. **Zuerst** öffnen Sie die gewünschte **Packmittelstückliste**. Solange ihr **Status** den Wert **Offen** hat, sind die Zeilen editierbar.
2. **Danach** tragen Sie in der Packmittelzeile (**Zeilenart** = **Packmittel**) den **Etikettentypcode** ein. Die enthaltenen Artikelzeilen erhalten den Code automatisch.
3. **Schließlich** setzen Sie den **Status** der Stückliste bei Bedarf auf **Freigegeben**; freigegebene Stücklisten sind nicht mehr editierbar.

**Validierungshinweis.** Der **Etikettentypcode** ist gegen die Etikettentypen (Seite **Labelarten**) geprüft; nur dort angelegte Codes sind zulässig.

### Etikettentyp in den Packmittelreferenzen hinterlegen

**Prozesseinstieg.** Diese Stammdaten pflegt der **Key-User** in den **Packmittelreferenzen** – den Regeln, die einem Artikel, Debitor oder Kreditor ein Standardpackmittel zuordnen. Der hier gepflegte **Etikettentypcode** wird beim Erzeugen der Belegpackmittel aus einer Referenz übernommen (siehe **Tägliche Arbeit**). Die Packmittelreferenzen werden im Modul m+m Package Management über die Aktion **Packmittelreferenzen** auf den jeweiligen Stammkarten (z. B. Artikel- oder Kreditorkarte) geöffnet.

**Einstieg:** Öffnen Sie auf der jeweiligen Stammkarte die Aktion **Packmittelreferenzen**; es öffnet sich die Seite **Packmittelreferenzen**.

Die Integrations-App ergänzt in dieser Seite die Spalte **Etikettentypcode**.

| Feld | Erläuterung |
|------|-------------|
| **Packmittelreferenznr.** | Eindeutige Nummer der Referenzregel (aus dem Basismodul). |
| **Produkttyp** / **Artikelnr.** | Legen fest, für welchen Artikel bzw. welche Artikelgruppe die Referenz gilt. |
| **Referenzart** / **Referenznr.** | Legen fest, für welchen Geschäftspartner (z. B. Debitor, Kreditor) die Referenz gilt. |
| **Packmittelart** | Art der Referenzquelle. Wenn der Wert **Packmittelstückliste** ist, darf hier **kein** **Etikettentypcode** gesetzt werden – der Etikettentyp wird in diesem Fall in der **Packmittelstückliste** gepflegt (siehe Validierungshinweis). Bei anderen Werten (z. B. **Packmittelkategorie**) ist die direkte Pflege des Etikettentyps zulässig. |
| **Packmittelnr.** / **Menge pro Packmittel** | Konkretes Packmittel und Umrechnungsmenge der Referenz (aus dem Basismodul). |
| **Etikettentypcode** | Wenn gesetzt, wird der hinterlegte Etikettentyp beim Erzeugen der Belegpackmittel aus dieser Referenz auf das Belegpackmittel übernommen. |

**Ablauf.**
1. **Zuerst** öffnen Sie über die Aktion **Packmittelreferenzen** die gewünschte Referenz.
2. **Danach** prüfen Sie die **Packmittelart**: Bei **Packmittelstückliste** pflegen Sie den Etikettentyp in der Stückliste, sonst tragen Sie den **Etikettentypcode** direkt in der Referenzzeile ein.
3. **Schließlich** steht der Etikettentyp beim nächsten Erzeugen von Belegpackmitteln aus dieser Referenz automatisch zur Verfügung.

**Validierungshinweis.** Setzt der Anwender in einer Referenz mit **Packmittelart** = **Packmittelstückliste** einen **Etikettentypcode**, meldet das System: *„Sie müssen den Etikettentypcode in der Paketstückliste definieren!"* und verhindert die Eingabe. Der Etikettentyp gehört in diesem Fall in die **Packmittelstückliste**, damit er beim Auflösen der Stückliste je Packmittelposition korrekt vererbt wird.

## Tägliche Arbeit: Packmittel erzeugen und Etikettentyp vererben

Im Tagesgeschäft erzeugt der Anwender **Belegpackmittel** aus den Stammdaten – entweder aus einer **Packmittelstückliste** oder aus einer **Packmittelreferenz**. Die Integrations-App greift dabei automatisch ein und überträgt den in den Stammdaten gepflegten **Etikettentypcode** auf das jeweilige Belegpackmittel. Der Anwender muss den Etikettentyp im Beleg **nicht** erneut erfassen.

Gesteuert wird dieses Verhalten durch die Einrichtung und die Stammdaten aus den vorigen Kapiteln: Der **Etikettentypcode** stammt aus **Packmittelstückliste** bzw. **Packmittelreferenzen** (siehe **Stammdaten**), und **was** später gedruckt wird, bestimmt das Feld **Paketfeld** auf **Labelart-Felder** bzw. **Label Barcodefelder** (siehe **Einrichtung**).

**Vererbungswege (automatisch, ohne zusätzliche Aktion des Anwenders):**

- **Aus der Packmittelstückliste:** Beim Erzeugen der Belegpackmittel aus einer Packmittelstückliste wird der in der Packmittelzeile gepflegte **Etikettentypcode** auf das erzeugte Belegpackmittel übernommen.
- **Aus einer Packmittelreferenz:** Beim Erzeugen der Belegpackmittel aus einer Packmittelreferenz wird der dort gepflegte **Etikettentypcode** auf das Belegpackmittel übernommen.
- **Aus der Verkaufszeile:** Beim Befüllen der Belegpackmittel aus einer Verkaufszeile wird ein an der Verkaufszeile geführter **Etikettentypcode** mitgeführt und auf das Belegpackmittel übernommen.

**Zeilenaktualisierung.** In den **Packmittelstücklistenzeilen** (Seite **Packmittelstückliste**) aktualisiert das System die Anzeige unmittelbar, sobald ein **Etikettentypcode** in einer Packmittelzeile geändert wird, damit die vererbten Werte in den Artikelzeilen sofort sichtbar sind.

## Lager, Belege und Etikettendruck

Der eigentliche **Etikettendruck** wird im gewohnten Lager- oder Belegprozess des Basismoduls angestoßen. Die Integrations-App stellt beim Druck automatisch den Bezug zwischen dem Beleg, seinen Packmitteln und den Etikettenfeldern her und ermittelt je Packmittel die unter **Paketfeld** eingestellten Werte.

### Unterstützte Belege und Prozesse

Beim Auflösen der Packmittel zum Druck ermittelt die App den Quellbeleg anhand der Belegart des Belegpackmittels. Unterstützt werden:

| Belegart des Belegpackmittels | Ermittelter Quellbeleg |
|-------------------------------|------------------------|
| **Warenannahme** (Label-Prozess) | Warenannahmekopf und -zeile – bei Einkaufsbestellung, Verkaufsrücklieferung und eingehender Umlagerung. |
| **Warenausgang** (Label-Prozess) | Warenausgangskopf und -zeile – bei Verkaufsauftrag, Einkaufsrücklieferung und ausgehender Umlagerung. |
| **Verkaufsauftrag** | Verkaufskopf und -zeile (Auftrag). |
| **Verkaufsreklamation** | Verkaufskopf und -zeile (Rücklieferung). |
| **Einkaufsbestellung** | Einkaufskopf und -zeile (Bestellung). |
| **Einkaufsreklamation** | Einkaufskopf und -zeile (Rücklieferung). |
| **Umlagerung (Eingang/Ausgang)** | Umlagerungskopf und -zeile. |
| **Artikel Buch.-Blatt** | Artikelbuchungsblattzeile. |

Wird kein passender Quellbeleg gefunden, überspringt die App das Packmittel; es werden dann keine Packmittelwerte auf das Etikett geschrieben.

### Ablauf des Etikettendrucks mit Packmittelwerten

1. **Zuerst** ermittelt die App zum gedruckten Beleg alle zugeordneten Belegpackmittel.
2. **Danach** bestimmt sie je Packmittel den Quellbeleg (siehe Tabelle oben).
3. **Anschließend** werden für jede Etikettenfeldzeile die Werte gesetzt: Tabellenfeld, **Benutz. Wert** oder – bei gesetztem **Paketfeld** – der ermittelte Packmittelwert (**Paketnr.**, **Paketcode**, **Menge im Paket** oder **Paketgruppennr**).
4. **Für Barcodefelder** werden die Bestandteile – inklusive gesetzter **Paketfeld**-Werte – mit dem Trennzeichen des Barcodetyps verbunden und als Barcode codiert.
5. **Schließlich** wird das Etikett wie im Basismodul erzeugt bzw. in der Vorschau angezeigt.

**Voraussetzung für die Ausgabe:** Die Packmittelfelder müssen im Prozess gepflegt sein. Fehlen sie, bleibt die entsprechende Etiketten- bzw. Barcodeposition leer.

## FAQ und Troubleshooting

### 1. Warum erscheint auf dem Etikett keine Packmittelinformation, obwohl ich ein Paketfeld eingestellt habe?

Es werden nur Werte ausgegeben, wenn im Prozess auch die Packmitteldaten gepflegt sind und dem Beleg Belegpackmittel zugeordnet sind. Fehlen die Packmittelangaben oder findet die App keinen passenden Quellbeleg zur Belegart, bleibt die Etikettenposition leer.

### 2. Warum kann ich das Feld Paketfeld in einer Zeile nicht auswählen?

Auf der Seite **Labelart-Felder** ist das Feld **Paketfeld** deaktiviert, sobald die **Berichtsfeldart** den Wert **Barcode** hat. Für Barcodes pflegen Sie die Packmittelquelle auf der Seite **Label Barcodefelder**.

### 3. Warum wird mein Benutz. Wert gelöscht, wenn ich ein Paketfeld setze?

Pro Feldzeile darf nur eine Wertquelle aktiv sein. Setzen Sie ein **Paketfeld**, entfernt das System nach Rückfrage einen vorhandenen **Benutz. Wert** (und umgekehrt), damit sich Freitext und Packmittelquelle nicht überlagern.

### 4. Warum erhalte ich die Meldung „Sie müssen den Etikettentypcode in der Paketstückliste definieren!"?

Diese Meldung erscheint, wenn Sie in einer **Packmittelreferenz** mit **Packmittelart** = **Packmittelstückliste** einen **Etikettentypcode** eintragen. In diesem Fall gehört der Etikettentyp in die **Packmittelstückliste**, nicht in die Referenz, damit er je Packmittelposition korrekt vererbt wird.

### 5. Warum kann ich in einer Artikelzeile der Packmittelstückliste keinen Etikettentypcode eintragen?

Der **Etikettentypcode** ist nur in Zeilen mit **Zeilenart** = **Packmittel** editierbar. Artikelzeilen erhalten den Code automatisch von ihrem übergeordneten Packmittel.

### 6. Woher kommt der Etikettentyp auf meinem Belegpackmittel?

Er wird beim Erzeugen der Belegpackmittel automatisch vererbt: aus der **Packmittelstückliste**, aus einer **Packmittelreferenz** oder aus einer Verkaufszeile. Eine manuelle Erfassung am Belegpackmittel ist nicht erforderlich.

### 7. Welche Packmittelwerte kann ich auf ein Etikett drucken?

Über **Paketfeld** stehen **Paketnr.**, **Paketcode**, **Menge im Paket** und **Paketgruppennr** zur Verfügung. **Menge im Paket** gibt dabei die zu bearbeitende Menge (**Zu bearbeitende Menge**) des Belegpackmittels aus.

### 8. Warum ändert sich mein Etikettentypcode in der Packmittelstückliste nicht sofort in den Artikelzeilen?

Die Vererbung auf die Artikelzeilen erfolgt beim Validieren des **Etikettentypcodes** in der Packmittelzeile; die Zeilenanzeige wird dabei unmittelbar aktualisiert. Prüfen Sie, ob Sie den Wert in einer Packmittelzeile (nicht in einer Artikelzeile) eingetragen haben.

### 9. Kann ich Packmittelinformationen in einen Barcode aufnehmen?

Ja. Setzen Sie in der gewünschten Zeile auf der Seite **Label Barcodefelder** das Feld **Paketfeld**. Der Wert wird beim Druck als Bestandteil in den Barcode aufgenommen und mit dem Trennzeichen des Barcodetyps mit den übrigen Bestandteilen verbunden.

### 10. Muss ich die App separat einrichten, oder reichen die Basismodule?

Die App benötigt die eingerichteten Basismodule **m+m Label Management** und **m+m Package Management**. Zusätzlich pflegen Sie nur die neuen Felder: **Paketfeld** auf **Labelart-Felder** bzw. **Label Barcodefelder** und **Etikettentypcode** in **Packmittelstückliste** bzw. **Packmittelreferenzen**. Weitere Einrichtungsschritte entstehen durch diese App nicht.

## Typische Anwendungsfälle

### Anwendungsfall 1: Paketnummer auf dem Versandetikett drucken

**Auslöser.** Ein Verkaufsauftrag soll versandt werden; auf dem Packmitteletikett soll die Paketnummer sichtbar sein, damit der Versand jedes Paket eindeutig zuordnen kann.

**Einstieg in BC.** Der Administrator öffnet einmalig über **Suchen** die Seite **Labelart-Felder** und setzt in der Zeile des Versand-Etikettentyps (Label-Prozess **Warenausgang**) das Feld **Paketfeld** auf **Paketnr.**.

**Kernablauf.**
1. Der Key-User hinterlegt in der zutreffenden **Packmittelreferenz** bzw. **Packmittelstückliste** den passenden **Etikettentypcode**.
2. Im Warenausgangsprozess zum Verkaufsauftrag erzeugt der Anwender die Belegpackmittel; der **Etikettentypcode** wird automatisch übernommen.
3. Beim Etikettendruck ermittelt die App je Packmittel die **Paketnr.** und druckt sie an der eingestellten Position.

**Abschluss.** Der Anwender prüft die Etikettenvorschau des Basismoduls und druckt die Etiketten; jedes Paket trägt seine Paketnummer.

### Anwendungsfall 2: Packmittelmenge im Wareneingang als Barcode

**Auslöser.** Bei der Warenannahme einer Einkaufsbestellung soll die Menge je Paket als Barcode erfasst werden, um die spätere Einlagerung zu beschleunigen.

**Einstieg in BC.** Der Administrator öffnet über **Suchen** die Seite **Label Barcodefelder** und setzt in der Zeile des Wareneingangs-Etikettentyps (Label-Prozess **Warenannahme**) das Feld **Paketfeld** auf **Menge im Paket**.

**Kernablauf.**
1. Der Key-User stellt sicher, dass die betroffenen Packmittel über **Packmittelstückliste** oder **Packmittelreferenz** einen gültigen **Etikettentypcode** besitzen.
2. Im Warenannahmeprozess zur Einkaufsbestellung werden die Belegpackmittel erzeugt; der Etikettentyp wird vererbt.
3. Beim Druck fügt die App die **Menge im Paket** (Wert aus **Zu bearbeitende Menge**) als Bestandteil in den Barcode ein und codiert diesen.

**Abschluss.** Der gedruckte Barcode enthält die Packmittelmenge und kann bei der Einlagerung gescannt werden.

### Anwendungsfall 3: Etikettentyp über die Packmittelstückliste zentral steuern

**Auslöser.** Für eine mehrstufige Packmittelstückliste (Palette mit Kartons) soll je Packmittelebene automatisch der richtige Etikettentyp gelten, ohne dass die Artikelzeilen einzeln gepflegt werden.

**Einstieg in BC.** Der Key-User öffnet über **Suchen** die **Packmittelstückliste** und wählt die betreffende Stückliste (**Status** = **Offen**).

**Kernablauf.**
1. In der Packmittelzeile (**Zeilenart** = **Packmittel**) trägt der Key-User den **Etikettentypcode** ein.
2. Alle Artikelzeilen dieses Packmittels übernehmen den Code automatisch; die Anzeige wird sofort aktualisiert.
3. Der Key-User setzt den **Status** der Stückliste bei Bedarf auf **Freigegeben**.

**Abschluss.** Beim Erzeugen der Belegpackmittel aus dieser Stückliste tragen alle Ebenen den korrekten Etikettentyp; der anschließende Etikettendruck nutzt die je Etikettentyp eingestellten **Paketfeld**-Werte.
