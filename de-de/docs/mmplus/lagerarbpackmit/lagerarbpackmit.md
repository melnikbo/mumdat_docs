---
title: Anwenderhandbuch m+m Warehouse Job Overview with Package Mgt.
---

# Anwenderhandbuch m+m Warehouse Job Overview with Package Mgt.

## Einleitung

Das Modul **m+m Warehouse Job Overview with Package Mgt.** verbindet die Handheld-Masken des **Lagerarbeitsvorrats**
mit der Packmittelverwaltung. Es erweitert die Scanner-Oberfläche des Lagerarbeitsvorrats um drei neue **Ansichtsarten**
für Packmittel und um zwei neue Aktionen, mit denen der Anwender direkt an der Maske Packmittel anlegt, einem Beleg
zuordnet, deren Bewegungsmenge bearbeitet oder Packmittelzuordnungen wieder entfernt.

Das Modul stellt selbst **keine eigene Seite** in der Business-Central-Oberfläche bereit. Es fügt seine Funktionen in
die bereits vorhandene Maskenkonfiguration des Lagerarbeitsvorrats ein und greift auf die Stammdaten der
Packmittelverwaltung zu. Die eigentliche Bedienung findet daher auf zwei Ebenen statt: der Administrator konfiguriert
die Masken in Business Central, der Lagermitarbeiter arbeitet mit dem Handheld-Gerät.

**Zielgruppe.** Primäre Zielgruppe sind die **operativen Lagermitarbeiter**, die am Handheld-Gerät kommissionieren,
umlagern und dabei Packmittel erfassen. Sekundäre Zielgruppe sind **Administratoren und Key-User**, die einmalig die
Ansichtsarten, Aktionen und Feldzuordnungen einrichten und die Masken den Geräten und Benutzern zuweisen.

**Kurzer Prozessüberblick.** Der typische Weg vom Einstieg bis zum Ergebnis lautet:

**Lagerarbeitsvorratseinrichtung → Maskenkonfiguration (Ansichtsart + Aktion) → Feldzuordnung je Ansichtsbereich →
Lagermaske Benutzer → Handheld: Lagerarbeitsvorratszeile → Ansicht Packmittel → Aktion Packmittel zuordnen**

Voraussetzung für den operativen Einsatz ist, dass in der **m+m Package Management** die Packmittel-Stammdaten
(Packmittel, Packmittelkategorie, Packmittelgruppe) gepflegt sind. Diese Stammdaten werden nicht in diesem Modul,
sondern in der Packmittelverwaltung angelegt.

## Schnellstart für Anwender

Der Schnellstart folgt der Reihenfolge, die der Programmablauf erzwingt: **zuerst die Einrichtung**, danach die
Zuweisung an die Benutzer, erst dann die Arbeit am Gerät.

**A. Einrichtung (Administrator, einmalig)**

1. Stellen Sie sicher, dass in der **m+m Package Management** Packmittel, Packmittelkategorien und Packmittelgruppen
   angelegt sind. Ohne Packmittelbestand kann an der Maske kein Packmittel zugeordnet werden.
2. Öffnen Sie über **Suchen** die **Lagerarbeitsvorratseinrichtung** und prüfen Sie die Maskensteuerung
   (siehe Abschnitt *Einrichtung*).
3. Öffnen Sie die Maskenkonfiguration des Lagerarbeitsvorrats und legen Sie eine neue **Ansichtsart** an — je nach
   Bedarf **Packmittel**, **Bestehendes Packmittel** oder **Menge. Vorhandene Verpackung**.
4. Ordnen Sie der Ansichtsart je **Ansichtsbereich** (**Kopfinformation**, **Zeileninformation**) die anzuzeigenden
   Felder zu (**Feldname** / **Feldnr.**).
5. Legen Sie zu der Ansichtsart die benötigten Aktionen an: **Packmittel zuordnen** und/oder **Bestehendes Packmittel
   zuweisen**, ergänzt um Standardaktionen wie **Löschen**, **OK** und **Schließen**.
6. Weisen Sie die Maske über **Lagermaske Benutzer** dem jeweiligen **Gerät** bzw. Benutzer zu.

**B. Tägliche Arbeit (Lagermitarbeiter, am Gerät)**

1. Öffnen Sie am Handheld-Gerät die zu bearbeitende **Lagerarbeitsvorratszeile**.
2. Wechseln Sie in die Ansicht **Packmittel**.
3. Wählen Sie die Aktion **Packmittel zuordnen**. Es öffnet sich der Dialog **Packmittel erstellen**.
4. Erfassen Sie **Anzahl Packmittel**, **Lagerort** und **Lagerplatz** und bestätigen Sie mit **OK**.
5. Für ein bereits physisch vorhandenes Packmittel wählen Sie stattdessen die Ansicht **Bestehendes Packmittel** und
   die Aktion **Bestehendes Packmittel zuweisen**.
6. Zum Korrigieren einer Menge wechseln Sie in die Ansicht **Menge. Vorhandene Verpackung** und bearbeiten das Feld
   **Bewegungsmenge**. Zum Entfernen einer Zuordnung wählen Sie **Löschen**.

Reicht der Packmittelbestand am Lagerplatz nicht aus, bricht die Aktion mit der Meldung *„Es gibt keinen ausreichenden
Packmittelbestand auf dem Lagerplatz.“* ab (siehe *FAQ und Troubleshooting*).

## Einrichtung

Die Einrichtung dieses Moduls besteht nicht aus einer eigenen Einrichtungsseite, sondern aus **Erweiterungen der
bestehenden Maskensteuerung des Lagerarbeitsvorrats**. Der Administrator legt die neuen Ansichtsarten und Aktionen an,
ordnet die Felder zu und verteilt die Masken an die Geräte. Alle in diesem Kapitel genannten Seiten gehören zum
Basismodul **Lagerarbeitsvorrat**; dieses Modul fügt dort ausschließlich neue **Ansichtsart**- und **Aktionsart**-Werte
hinzu.

**Einstieg:** **Suchen → Lagerarbeitsvorratseinrichtung** bzw. die Maskenkonfiguration des Lagerarbeitsvorrats.

**Berechtigungen.** Das Modul liefert den Berechtigungssatz **MuM WJPM All** (Bezeichnung *All Warehouse Job
permissions*). Dieser Berechtigungssatz bestimmt die Berechtigungen für die Zwischentabelle **Packmittel** sowie für
die genutzten Lagerarbeitsvorrats- und Packmittelobjekte und legt fest, welche Aktionen die Anwender an der Maske
ausführen dürfen. Weisen Sie den Berechtigungssatz den Benutzern zu, die mit den Packmittel-Ansichten arbeiten sollen.

### Ansichtsarten und Aktionen für Packmittel einrichten

**Wer und wann.** Diese Einrichtung führt der Administrator bzw. Key-User **einmalig vor dem ersten Einsatz** durch —
und erneut, wenn eine weitere Maske oder ein weiteres Gerät hinzukommt. Sie schaltet das Packmittel-Handling auf der
Handheld-Maske frei. Die hier konfigurierten Ansichten und Aktionen konsumiert der Lagermitarbeiter später im Kapitel
*Tägliche Arbeit an der Lagermaske*.

**Was diese Einrichtung bewirkt.** Erst wenn eine Ansichtsart und die zugehörigen Aktionen angelegt und einem Gerät
zugewiesen sind, erscheinen die Packmittel-Funktionen überhaupt am Handheld. Ohne diese Einrichtung bleibt die Maske
auf die Standard-Lagerfunktionen beschränkt und der Anwender sieht keine Packmittel-Ansicht.

**Enablement-Schritte (in Abhängigkeitsreihenfolge):**

1. **Zuerst** die Packmittel-Stammdaten sicherstellen: In der **m+m Package Management** müssen Packmittel,
   Packmittelkategorie und Packmittelgruppe existieren. Wenn keine Packmittel mit Bestand vorhanden sind, dann schlägt
   die spätere Aktion **Packmittel zuordnen** am Gerät fehl.
2. **Danach** in der Maskenkonfiguration eine neue **Ansichtsart** anlegen. Wählen Sie den passenden Wert:
   - **Packmittel** — Wenn gesetzt, dann zeigt die Maske die für die Belegzeile anzulegenden bzw. zuzuordnenden
     Packmittel an; über diese Ansicht wird ein neues Packmittel erstellt.
   - **Bestehendes Packmittel** — Wenn gesetzt, dann arbeitet die Maske mit bereits physisch vorhandenen Packmitteln
     der Belegzuordnung; der Anwender weist ein vorhandenes Packmittel zu, statt ein neues anzulegen.
   - **Menge. Vorhandene Verpackung** — Wenn gesetzt, dann ist an dieser Ansicht die Mengeneingabe aktiv; der Anwender
     kann die **Bewegungsmenge** eines vorhandenen Packmittels direkt bearbeiten.
3. **Danach** die **Aktionsart** je Ansicht festlegen:
   - **Packmittel zuordnen** — Wenn diese Aktion ausgelöst wird, dann wird für die aktuelle Belegzeile ein Packmittel
     angelegt und dem Beleg zugeordnet; dabei öffnet sich der Dialog **Packmittel erstellen**.
   - **Bestehendes Packmittel zuweisen** — Wenn diese Aktion ausgelöst wird, dann wird ein bereits vorhandenes
     Packmittel der Belegzeile zugewiesen, ohne ein neues Packmittel zu erzeugen.
   - Ergänzend stehen die Standardaktionen des Lagerarbeitsvorrats zur Verfügung: **Löschen** (entfernt die
     Packmittelzuordnung der Belegzeile), **OK** (schließt die Eingabe erfolgreich ab) und **Schließen** (beendet die
     Ansicht ohne weitere Verarbeitung).
4. **Schließlich** die Feldzuordnung je Ansichtsbereich vornehmen (siehe nächste H3) und die Maske über **Lagermaske
   Benutzer** zuweisen (übernächste H3).

**Operativer Abschluss.** Die Kette endet am Gerät: Der Lagermitarbeiter öffnet die Belegzeile, wechselt in die
konfigurierte Ansicht und löst die Aktion aus. Der genaue Ablauf ist im Kapitel *Tägliche Arbeit an der Lagermaske*
beschrieben.

### Feldzuordnung je Ansichtsbereich

**Wer und wann.** Ebenfalls Teil der einmaligen Einrichtung. Der Administrator legt fest, welche Felder in welchem
Bereich der Maske erscheinen.

Jede Ansichtsart wird pro **Ansichtsbereich** befüllt. Es gibt zwei Bereiche:

- **Kopfinformation** — Wenn Felder diesem Bereich zugeordnet sind, dann erscheinen sie im Kopfteil der Maske und
  liefern dem Anwender den Kontext der Belegzeile (z. B. Artikel, Charge, Lagerort).
- **Zeileninformation** — Wenn Felder diesem Bereich zugeordnet sind, dann erscheinen sie im Zeilenteil der Maske, in
  dem der Anwender die einzelnen Packmittel sieht und bearbeitet.

Für jede Zeile der Feldzuordnung sind folgende Angaben relevant:

| Feld | Erläuterung |
|---|---|
| **Art** | Wenn ausgewählt, dann bestimmt dieser Wert, für welche Ansichtsart (**Packmittel**, **Bestehendes Packmittel**, **Menge. Vorhandene Verpackung**) die Feldzuordnung gilt. |
| **Ansichtsbereich** | Wenn auf **Kopfinformation** gesetzt, erscheint das Feld im Kopfteil; bei **Zeileninformation** im Zeilenteil der Maske. |
| **Feldname** | Zeigt die Bezeichnung des zugeordneten Feldes; wird beim Auswählen der **Feldnr.** automatisch aus der Feldbezeichnung der Quelltabelle übernommen. |
| **Feldnr.** | Wenn gesetzt, dann wird genau dieses Feld der zugrunde liegenden Tabelle an der Maske dargestellt; die Auswahl erfolgt über eine Feldliste, die nur anzeigbare Felder zulässt. |
| **Tabellennr.** | Wird durch die Ansichtsart vorgegeben: für **Packmittel** die Packmitteltabelle, für **Bestehendes Packmittel** und **Menge. Vorhandene Verpackung** die Belegpackmitteltabelle (**Packmittelbelege**). Der Anwender muss sie nicht selbst wählen. |
| **Editierbar** | Wenn aktiviert, dann darf der Anwender das Feld an der Maske ändern; für die Ansicht **Menge. Vorhandene Verpackung** ist die Eingabe systemseitig freigeschaltet, damit die **Bewegungsmenge** bearbeitet werden kann. Für die übrigen Packmittel-Felder ist ausschließlich die **Bewegungsmenge** eingabefähig. |

**Validierungshinweis.** Wählt der Administrator eine **Feldnr.** aus, prüft das System, ob das Feld in der Quelltabelle
zulässig ist; Felder technischer Typen (z. B. BLOB, Medien, RecordID, Tabellenfilter) werden ausgeschlossen. Ist die
gewählte Feldnummer ungültig, meldet das System einen Fehler auf dem Feld **Feldnr.**

### Masken den Benutzern zuweisen

**Wer und wann.** Nach dem Anlegen der Ansichtsarten, Aktionen und Feldzuordnungen weist der Administrator die Maske
den Geräten bzw. Benutzern zu. Ohne diese Zuweisung erreicht die konfigurierte Maske das Handheld nicht.

**Einstieg:** **Suchen → Lagermaske Benutzer**.

Auf der Seite **Lagermaske Benutzer** ordnen Sie je Eintrag zu:

| Feld | Erläuterung |
|---|---|
| **Art** | Wenn auf **Gerät** (bzw. Benutzer) gesetzt, dann legt dieser Wert fest, ob die Zuweisung für ein physisches Handheld-Gerät oder einen benannten Benutzer gilt. |
| **Code** | Wenn gesetzt, dann identifiziert dieser Wert das konkrete Gerät bzw. den Benutzer, für den die Maske gilt. |
| **Sprachcode** | Wenn gesetzt, dann werden die Maskentexte in der hinterlegten Sprache angezeigt; ohne Sprachcode gilt die Standardsprache. |

**Prozessschritt.** Zuerst die Maskenkonfiguration abschließen, danach hier das Gerät bzw. den Benutzer mit der Maske
verknüpfen; erst dann stehen die Packmittel-Ansichten am Handheld zur Verfügung. Diese Zuweisung ist die letzte
Voraussetzung für das Kapitel *Tägliche Arbeit an der Lagermaske*.

## Datenmodell: Zwischentabelle „Packmittel“

Dieses Modul führt eine einzige eigene Tabelle: die Zwischentabelle mit der Bezeichnung **Packmittel** (technisch
*MuM WJPM Whse Doc. Assignment*). Sie speichert die Packmittelzuordnung einer Belegzeile, während die Belegzeile an der
Maske bearbeitet wird, und liefert die Felder, die der Administrator den Ansichten zuordnen kann. Der Anwender pflegt
diese Tabelle nicht direkt; er sieht ausgewählte Felder daraus an der Handheld-Maske. Die folgende Übersicht erläutert
die anwenderrelevanten Felder.

| Feld | Erläuterung |
|---|---|
| **Belegart** | Wenn gesetzt, dann ordnet dieser Wert die Zeile einem Packmittelbelegtyp der Packmittelverwaltung zu (z. B. **Artikel Buch.-Blatt Umlagerung**); daraus leitet sich ab, in welchem Beleg das Packmittel entsteht. |
| **Belegnr.** | Wenn gefüllt, dann verweist die Zeile auf den konkreten Beleg, zu dem das Packmittel gehört. |
| **Zeilenart** | Wenn auf Artikel, Partition oder Packmittel gesetzt, dann steuert dieser Wert, ob die Zeile einen Artikel, eine Teilmenge (Partition) oder ein Packmittel beschreibt; bei Artikel/Partition wird das Ziel-Packmittel als übergeordnetes Paket verwendet, bei Packmittel das Paket selbst. |
| **Paketkategorie** | Wenn gesetzt, dann schränkt dieser Wert die zulässigen Paketcodes ein; nur Packmittel der gewählten Kategorie sind erlaubt. |
| **Paketcode** | Wenn gesetzt, dann bestimmt dieser Wert die Packmittelart (Vorlage) des zugeordneten Packmittels. |
| **Paketnr.** | Wenn gefüllt, dann identifiziert dieser Wert das konkrete physische Packmittel. |
| **Paketgruppennr.** / **Paketgruppencode-Nr.** | Wenn gefüllt, dann fassen diese Werte zusammengehörige Packmittel zu einer Packmittelgruppe zusammen; sie verknüpfen die Maskenzeile mit der Gruppierung der Packmittelverwaltung. |
| **Artikelnr.** | Wenn gefüllt, dann benennt dieser Wert den Artikel, dessen Menge im Packmittel liegt. |
| **Variantencode** | Wenn gefüllt, dann konkretisiert dieser Wert die Artikelvariante. |
| **Chargennr.** | Wenn gefüllt, dann ordnet dieser Wert die im Packmittel enthaltene Menge einer Charge zu; erforderlich für die Chargenverfolgung. |
| **Seriennr.** | Wenn gefüllt, dann ordnet dieser Wert die Menge einer Seriennummer zu. |
| **Lagerortcode** | Wenn gesetzt, dann bestimmt dieser Wert den Lagerort, aus dem das Packmittelmaterial entnommen und auf dem der Bestand geprüft wird. |
| **Lagerplatzcode** | Wenn gesetzt, dann bestimmt dieser Wert den Lagerplatz innerhalb des Lagerorts; die Bestandsprüfung des Packmittels erfolgt gegen diesen Lagerplatz. |
| **Bewegungsmenge** | Wenn der Anwender diesen Wert in der Ansicht **Menge. Vorhandene Verpackung** ändert, dann wird die zu bewegende Menge des Packmittels neu gesetzt und validiert; dies ist das einzige an der Maske frei eingabefähige Mengenfeld. |
| **Paket nicht verbrauchen** | Wenn aktiviert, dann bleibt das Packmittel bei der Weiterverarbeitung erhalten und wird nicht als verbraucht gebucht; ohne Kennzeichen wird das Packmittel im Folgeprozess verbraucht. |
| **Nettogewicht** | Zeigt das errechnete Nettogewicht des Packmittelinhalts; das Feld ist nicht editierbar und dient der Information. |
| **Physische Menge.** / **Verbleibende physische Menge.** | Zeigen die tatsächlich vorhandene bzw. noch offene physische Menge des Packmittels; sie unterstützen den Anwender bei der Kontrolle, wie viel bereits behandelt wurde. |
| **Dokumentzeilenmenge** | Zeigt die Menge der zugehörigen Belegzeile als Bezugsgröße für die Packmittelbefüllung. |
| **Beschreibung** / **Beschreibung 2** | Wenn gefüllt, dann liefern diese Freitexte eine Bezeichnung des Packmittels für die Anzeige an der Maske. |
| **Paketbuch gebucht** / **Paketlager gebucht** | Zeigen an, ob das Packmittel bereits in das Paketbuch bzw. das Paketlager gebucht wurde; die Buchung selbst führt die Packmittelverwaltung durch, nicht dieses Modul. |
| *Technische Schlüssel- und Statusfelder* | Nicht durch den Anwender gepflegt: **FA-Zeilennr.**, **Buch.-Blattvorlagenname**, **Buch.-Blattname**, **Lfd. Nr.**, **Belegzeilennr.**, **Sortiernr.**, **Sequenzzeilen-Nr.**, **Ebene**, **Partitionstyp**, **Partitionscode**, **Physische Datensatz-ID**, **Herkunftsbelegart**, **Herkunftsbelegnr.**, **Herkunftszeilennr.**, **Quelle Prod. Bestellzeilennr.**, **Physisch behandelt**, **Lager-Job-Beziehung**, **Paket-Parent-Code-Nr.**, **Paket-Eltern-Nr.**. Diese Felder verknüpfen die Maskenzeile technisch mit Beleg, Buchungsblatt und Packmittelstruktur und werden vom System gefüllt. |

## Tägliche Arbeit an der Lagermaske

**Steuernde Einrichtung.** Welche Ansichten und Aktionen dem Lagermitarbeiter am Handheld angeboten werden, ergibt sich
vollständig aus der Maskenkonfiguration und der Zuweisung unter **Lagermaske Benutzer** (siehe Kapitel *Einrichtung*).
Sieht ein Anwender eine hier beschriebene Ansicht nicht, ist die entsprechende Ansichtsart, Aktion oder
Gerätezuweisung noch nicht eingerichtet.

Der Lagermitarbeiter öffnet am Handheld-Gerät die **Lagerarbeitsvorratszeile**, die er bearbeiten möchte, und wechselt
in eine der drei Packmittel-Ansichten. Die verfügbaren Ansichten und Aktionen sind:

### Ansicht Packmittel — neues Packmittel anlegen und zuordnen

Wählt der Anwender die Ansicht **Packmittel** und die Aktion **Packmittel zuordnen**, prüft das System zunächst den
Packmittelbestand am Lagerplatz. Ist Bestand vorhanden, öffnet sich der Dialog **Packmittel erstellen**. Dort erfasst
der Anwender:

| Feld | Erläuterung |
|---|---|
| **Anzahl Packmittel** | Wenn gesetzt, dann wird die angegebene Anzahl gleichartiger Packmittel angelegt und der Belegzeile zugeordnet. |
| **Lagerort** | Wenn gesetzt, dann wird das Packmittelmaterial aus diesem Lagerort entnommen und der Bestand dort geprüft. |
| **Lagerplatz** | Wenn gesetzt, dann erfolgt Entnahme und Bestandsprüfung gegen diesen Lagerplatz. |

Nach der Bestätigung mit **OK** legt das System die Packmittel an, ordnet sie der Belegzeile zu und befüllt sie mit den
Artikel-/Mengendaten der Zeile. Anschließend steht das Packmittel im Beleg der Packmittelverwaltung zur weiteren
Verarbeitung bereit.

### Ansicht Bestehendes Packmittel — vorhandenes Packmittel zuweisen

Wählt der Anwender die Ansicht **Bestehendes Packmittel** und die Aktion **Bestehendes Packmittel zuweisen**, ordnet das
System der Belegzeile ein bereits physisch vorhandenes Packmittel zu, ohne ein neues zu erzeugen. Diese Ansicht nutzt
der Anwender, wenn das Packmittel bereits existiert und lediglich mit der aktuellen Belegzeile verknüpft werden soll.

### Ansicht Menge. Vorhandene Verpackung — Bewegungsmenge bearbeiten

In der Ansicht **Menge. Vorhandene Verpackung** ist die Mengeneingabe freigeschaltet. Der Anwender bearbeitet hier das
Feld **Bewegungsmenge**, um die zu bewegende Menge eines bereits vorhandenen Packmittels zu korrigieren. Das System
validiert die eingegebene Menge; andere Felder dieser Ansicht sind schreibgeschützt.

### Packmittelzuordnung entfernen

Über die Aktion **Löschen** entfernt der Anwender die Packmittelzuordnung der aktuellen Belegzeile aus der
Zwischentabelle **Packmittel**. Die zugrunde liegende Belegzeile bleibt bestehen; nur die Packmittelzuordnung wird
gelöscht.

**Lager- und Buchungsbezug.** Dieses Modul erzeugt die Packmittelzuordnung und setzt die **Bewegungsmenge**; die
eigentliche Buchung der Packmittel in **Paketbuch** und **Paketlager** (Felder **Paketbuch gebucht** / **Paketlager
gebucht**) sowie die Erzeugung der Artikelposten übernimmt die **m+m Package Management** im weiteren Verlauf des
Umlagerungs- bzw. Buchungsprozesses.

## FAQ und Troubleshooting

### 1. Warum sehe ich am Handheld keine Packmittel-Ansicht?

Die Ansicht erscheint nur, wenn eine passende **Ansichtsart** (Packmittel, Bestehendes Packmittel oder Menge. Vorhandene
Verpackung) in der Maskenkonfiguration angelegt und die Maske über **Lagermaske Benutzer** dem Gerät bzw. Benutzer
zugewiesen ist. Prüfen Sie beide Einrichtungsschritte.

### 2. Was bedeutet die Meldung „Es gibt keinen ausreichenden Packmittelbestand auf dem Lagerplatz“?

Beim Anlegen eines Packmittels prüft das System den Packmittelbestand am angegebenen Lagerplatz. Ist der Bestand des
Packmittelmaterials null bzw. nicht ausreichend, bricht die Aktion **Packmittel zuordnen** mit dieser Meldung ab. Sorgen
Sie für ausreichenden Packmittelbestand am Lagerort/Lagerplatz oder wählen Sie einen anderen Lagerplatz.

### 3. Warum kann ich nur die Bewegungsmenge bearbeiten?

An den Packmittel-Ansichten ist ausschließlich das Feld **Bewegungsmenge** eingabefähig; alle anderen Felder sind
schreibgeschützt. In der Ansicht **Menge. Vorhandene Verpackung** ist die Mengeneingabe zusätzlich systemseitig
freigeschaltet. So bleibt die Packmittelstruktur konsistent, während der Anwender die Menge anpasst.

### 4. Wie ordne ich ein bereits vorhandenes Packmittel zu, ohne ein neues zu erzeugen?

Wechseln Sie in die Ansicht **Bestehendes Packmittel** und wählen Sie **Bestehendes Packmittel zuweisen**. Damit wird
das vorhandene Packmittel der Belegzeile zugewiesen, ohne dass der Dialog **Packmittel erstellen** und eine
Neuanlage erfolgen.

### 5. Was passiert genau, wenn ich „Packmittel zuordnen“ auslöse?

Das System prüft den Packmittelbestand, öffnet den Dialog **Packmittel erstellen**, legt nach Bestätigung mit **OK** die
angegebene **Anzahl Packmittel** an, ordnet sie der Belegzeile zu und befüllt sie mit den Artikel- und Mengendaten der
Zeile. Anschließend steht das Packmittel im Packmittelbeleg zur Verfügung.

### 6. Warum wird mein Feld in der Maske nicht angezeigt?

Ein Feld erscheint nur, wenn es in der **Feldzuordnung** dem passenden **Ansichtsbereich** (**Kopfinformation** oder
**Zeileninformation**) mit gültiger **Feldnr.** zugeordnet ist. Technische Feldtypen (z. B. BLOB, Medien) sind nicht
auswählbar und können nicht angezeigt werden.

### 7. Was bedeutet das Kennzeichen „Paket nicht verbrauchen“?

Wenn **Paket nicht verbrauchen** aktiviert ist, bleibt das Packmittel im Folgeprozess erhalten und wird nicht als
verbraucht gebucht. Ohne dieses Kennzeichen wird das Packmittel im weiteren Verlauf verbraucht.

### 8. Warum ist das Nettogewicht nicht editierbar?

Das **Nettogewicht** wird aus dem Packmittelinhalt errechnet und dient nur der Information. Es lässt sich an der Maske
nicht ändern; ändern Sie stattdessen die zugrunde liegenden Mengen- bzw. Artikeldaten.

### 9. Woran erkenne ich, ob ein Packmittel bereits gebucht wurde?

Die Felder **Paketbuch gebucht** und **Paketlager gebucht** zeigen an, ob das Packmittel in das Paketbuch bzw. das
Paketlager gebucht wurde. Die Buchung selbst führt die **m+m Package Management** durch, nicht dieses Modul.

### 10. Wie entferne ich eine falsche Packmittelzuordnung?

Wählen Sie an der Maske die Aktion **Löschen**. Damit werden die Packmittelzeilen der aktuellen Belegzeile aus der
Zwischentabelle **Packmittel** entfernt; die Belegzeile selbst bleibt erhalten.

## Typische Anwendungsfälle

### Anwendungsfall 1: Neues Packmittel bei der Kommissionierung anlegen

**Auslöser.** Ein Lagermitarbeiter kommissioniert eine Umlagerung und benötigt für die entnommene Ware ein neues
Packmittel, um die Menge sauber zu verpacken und weiterzuleiten.

**Einstieg in BC.** Am Handheld-Gerät öffnet der Mitarbeiter die betreffende **Lagerarbeitsvorratszeile** und wechselt
in die Ansicht **Packmittel**.

**Kernablauf.**
1. Der Mitarbeiter wählt die Aktion **Packmittel zuordnen**.
2. Das System prüft den Packmittelbestand am Lagerplatz; ist Bestand vorhanden, öffnet sich der Dialog **Packmittel
   erstellen**.
3. Der Mitarbeiter erfasst **Anzahl Packmittel**, **Lagerort** und **Lagerplatz** und bestätigt mit **OK**.
4. Das System legt die Packmittel an, ordnet sie der Belegzeile zu und befüllt sie mit den Artikel-, Chargen- und
   Mengendaten der Zeile.

**Abschluss.** Das Packmittel steht im Packmittelbeleg der Packmittelverwaltung bereit. Die spätere Buchung von
Paketbuch und Paketlager erfolgt im nachgelagerten Umlagerungsprozess durch die Packmittelverwaltung.

### Anwendungsfall 2: Bereits verpackte Ware zuordnen

**Auslöser.** Die Ware ist bereits in einem physisch vorhandenen Packmittel verpackt; der Mitarbeiter muss dieses
Packmittel nur noch der aktuellen Belegzeile zuordnen.

**Einstieg in BC.** Der Mitarbeiter öffnet die **Lagerarbeitsvorratszeile** und wechselt in die Ansicht **Bestehendes
Packmittel**.

**Kernablauf.**
1. Der Mitarbeiter wählt die Aktion **Bestehendes Packmittel zuweisen**.
2. Das System verknüpft das vorhandene Packmittel mit der Belegzeile, ohne ein neues Packmittel anzulegen.

**Abschluss.** Die Zuordnung ist gesetzt; ein Dialog **Packmittel erstellen** erscheint in diesem Fall nicht.

### Anwendungsfall 3: Menge korrigieren oder Zuordnung entfernen

**Auslöser.** Beim Verpacken stellt der Mitarbeiter fest, dass die erfasste Menge nicht stimmt, oder ein Packmittel
wurde versehentlich der falschen Zeile zugeordnet.

**Einstieg in BC.** Der Mitarbeiter öffnet die **Lagerarbeitsvorratszeile**.

**Kernablauf.**
1. Zum Korrigieren der Menge wechselt der Mitarbeiter in die Ansicht **Menge. Vorhandene Verpackung** und bearbeitet
   das Feld **Bewegungsmenge**; das System validiert die neue Menge.
2. Zum Entfernen einer falschen Zuordnung wählt der Mitarbeiter die Aktion **Löschen**; die Packmittelzuordnung der
   Zeile wird aus der Zwischentabelle **Packmittel** entfernt.

**Abschluss.** Nach der Korrektur kann der Mitarbeiter die Zeile erneut über **Packmittel zuordnen** bzw. **Bestehendes
Packmittel zuweisen** bearbeiten und den Vorgang mit **OK** abschließen.
