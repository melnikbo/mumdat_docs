---
title: Anwenderhandbuch m+m Aided Data Management
---

# Anwenderhandbuch m+m Aided Data Management

Die App **m+m Aided Data Management** stellt in Microsoft Dynamics 365 Business Central eine **regelbasierte Datenverwaltung** bereit: Sie definieren einmalig **Regeln** und ordnen sie in **Regelabläufen** einer **Materialart** zu. Sobald ein Artikel dieser Materialart entsperrt wird, prüft und setzt das System die Artikelstammdaten – Eigenschaften, Materialfilter, Arbeitspläne und Fertigungsstücklisten – automatisch nach Ihren Regeln. Das Modul ersetzt manuelle, fehleranfällige Pflegeschritte durch nachvollziehbare, wiederverwendbare Automatik.

## Einleitung

### Zweck des Moduls

Das Modul automatisiert den Aufbau von Artikelstammdaten. Statt jeden neuen Artikel von Hand mit Eigenschaftswerten, Arbeitsplan-Arbeitsgängen und Stücklistenkomponenten zu füllen, hinterlegen Sie **Regeln**, die Werte berechnen, vergleichen, suchen oder in Zielfelder schreiben. Mehrere Regeln werden in einem **Regelablauf** logisch verknüpft (mit **Wenn/Sonst/Ende**-Verzweigungen) und je Bereich an einer **Materialart** hinterlegt. Die Ausführung erfolgt automatisch beim **Entsperren** des Artikels.

### Zielgruppe

- **Operative Anwenderinnen und Anwender in der Artikelanlage und Arbeitsvorbereitung** sind die primäre Zielgruppe: Sie legen Artikel an, setzen die **Materialart**, pflegen Eigenschaftswerte und **entsperren** den Artikel, damit die Regelabläufe ihre Stammdaten aufbauen.
- **Key-User und Administratoren** sind die sekundäre Zielgruppe: Sie richten die **Regel Einrichtung** ein und definieren **Regeln** und **Regelabläufe**.

### Kurzer Prozessüberblick

Der typische Weg durch das Modul folgt dieser Kette:

1. **Regel Einrichtung** vornehmen (Nummernvergabe für Arbeitspläne und Fertigungsstücklisten).
2. **Regeln** definieren (je **Regelart** ein Verhalten, ggf. mit **Regelmatrix** und **Regeleigenschaften**).
3. Regeln in einem **Regelablauf** an der **Materialartenkarte** verketten (Eigenschaften-, Vormaterialsuchfilter-, Arbeitsplan-, Fertigungsstückliste- und FA-Arbeitsplan-Regelablauf).
4. Im Tagesgeschäft einen Artikel mit passender **Materialart** anlegen; der Artikel wird automatisch **Gesperrt**.
5. Den Artikel **entsperren** – die Regelabläufe laufen der Reihe nach und bauen die Stammdaten auf.

## Schnellstart für Anwender

Dieser Schnellstart beschreibt den kürzesten Weg vom leeren System bis zum automatisch aufgebauten Artikel. Die Einrichtungsschritte sind Voraussetzung und stehen deshalb zuerst.

1. **Regel Einrichtung öffnen** (über **Suchen**) und festlegen, wie **Arbeitsplannummern von** und **Fertigungsstücklistenummern von** vergeben werden (**Nummernserie** oder **Artikelnr.**).
2. **Regeln** definieren: Öffnen Sie die Liste **Regeln** (über **Suchen**), wählen Sie **Neu** und legen Sie je Automatisierungsschritt eine Regel mit passender **Regelart** an. Für Nachschlagelogik pflegen Sie **Regeleigenschaften** und die **Regelmatrix**.
3. **Regelablauf hinterlegen:** Öffnen Sie in der Materialarten-Übersicht die gewünschte Zeile, rufen Sie die **Materialartenkarte** auf und wählen Sie in der Aktionsgruppe **Regelablauf** den passenden Ablauf, z. B. **Eigenschaften-Regelablauf**. Verketten Sie im **Regelablauf** die Regeln über die Spalte **Zeilenart**.
4. **Artikel anlegen** und die **Materialart** setzen. Der Artikel wird automatisch **Gesperrt**, sobald die Materialart einen Regelablauf besitzt.
5. **Artikel entsperren.** Beim Entsperren laufen die Regelabläufe in fester Reihenfolge (Eigenschaften → Vormaterialsuchfilter → Arbeitsplan → Fertigungsstückliste) und bauen die Stammdaten auf.

> Hinweis: Die eigentliche „Buchung“ dieses Moduls ist das **Entsperren** des Artikels. Es gibt keinen eigenen Buchungs- oder Freigabebeleg; der Regelablauf ist die einzige vom Anwender ausgelöste Aktion.

## Einrichtung

Die Einrichtung besteht aus einer zentralen Einrichtungsseite und der anschließenden Definition der Regeln. Sie ist Grundlage für die gesamte Automatik und wird vom Key-User bzw. Administrator vor der ersten Nutzung vorgenommen.

### Regel Einrichtung

**Prozesseinstieg:** Der Administrator richtet einmalig je Mandant fest, wie das Modul neue Arbeitsplan- und Fertigungsstücklistennummern vergibt, wenn eine Regel einen Arbeitsplan oder eine Fertigungsstückliste anlegt. Diese Vorgabe steuert später die Regelarten **Arbeitsgang verwenden** und **Fertigungsstücklistekomponente verwenden**.

**Einstieg:** Öffnen Sie die Seite **Regel Einrichtung** über **Suchen**. Es handelt sich um eine mandantenweite Einzelseite; beim ersten Öffnen wird der Datensatz automatisch angelegt.

| Einrichtung | Erläuterung |
|---|---|
| **Arbeitsplannummern von** | Legt fest, woher die Nummer eines durch eine Regel neu erzeugten Arbeitsplans stammt. Wenn **Nummernserie** gewählt ist, erhält der neue Arbeitsplan eine fortlaufende Nummer aus der Nummernserie; wenn **Artikelnr.** gewählt ist, wird die Artikelnummer als Arbeitsplannummer verwendet, sodass Artikel und Arbeitsplan dieselbe Nummer tragen. |
| **Fertigungsstücklistenummern von** | Legt fest, woher die Nummer einer durch eine Regel neu erzeugten Fertigungsstückliste stammt. Wenn **Nummernserie** gewählt ist, wird die Nummer fortlaufend vergeben; wenn **Artikelnr.** gewählt ist, trägt die Fertigungsstückliste die Artikelnummer, was die Zuordnung von Artikel und Stückliste vereinfacht. |

**Werte des Optionsfelds (für beide Felder identisch):**

- **Nummernserie:** Die Nummer wird beim Anlegen aus einer Nummernserie gezogen; Artikel und Arbeitsplan bzw. Fertigungsstückliste haben unterschiedliche Nummern.
- **Artikelnr.:** Die Nummer entspricht der Artikelnummer; für jeden Artikel entsteht ein gleichnamiger Arbeitsplan bzw. eine gleichnamige Fertigungsstückliste.

## Stammdaten

Die Stammdaten dieses Moduls sind die **Regeln** selbst, ihre **Regelmatrix** und **Regeleigenschaften**, sowie die Zuordnung der Regeln zu **Materialarten** über Regelabläufe. Zusätzlich lassen sich Regeln als **direkte Regeln** unmittelbar an einer Datensatzeigenschaft hinterlegen.

### Regeln definieren

**Prozesseinstieg:** Der Key-User legt je Automatisierungsschritt genau eine Regel an. Die **Regelart** bestimmt das Verhalten und blendet auf der Karte nur die dafür nötigen Felder ein. Regeln werden später in Regelabläufen verwendet oder als direkte Regel an einer Eigenschaft hinterlegt.

**Einstieg:** Öffnen Sie die Liste **Regeln** über **Suchen** und wählen Sie **Neu**; die Liste öffnet die **Regel**-Karte. Eine Regel kann nicht umbenannt werden, und im **Code** sind Sonderzeichen wie `. ; # $` nicht zulässig.

#### Allgemeine Felder der Regel

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutige Kennung der Regel. Wenn gesetzt, kann die Regel in Regelabläufen und als direkter Regelcode ausgewählt werden; ein nachträgliches Umbenennen ist nicht möglich. |
| **Beschreibung** | Klartextbezeichnung. Wenn gesetzt, erscheint sie in Listen und im **Regel Flow Editor** als Knotentitel und erleichtert die Auswahl der Regel. |
| **Regelart** | Bestimmt das Verhalten der Regel und steuert, welche Feldgruppen auf der Karte sichtbar und editierbar sind. Wenn Sie die Regelart ändern, werden nicht mehr passende Werte automatisch geleert. Die einzelnen Werte sind unten beschrieben. |
| **Wertart** | Legt den Datentyp des Ergebnisses fest (**Ja/Nein, Datum, Datum/Zeit, Dezimal, Ganzzahl, Text, Zeit**). Wenn die Regelart oder eine gewählte Eigenschaft den Typ vorgibt, wird die Wertart automatisch gesetzt; bei **Wert zurückgeben** und **Konstante zurückgeben** wählen Sie sie selbst. Sie steuert, welches Konstantenfeld und welche Rückgabespalte der Regelmatrix verwendet werden. |
| **Direkt** | Wenn aktiviert, kann die Regel direkt an einer Datensatzeigenschaft (**Direkter Regelcode**) hinterlegt und ohne Regelablauf ausgeführt werden. Nur für die Regelarten **Eigenschaft setzen, Eigenschaftattribut setzen, Wertfilter setzen** und **Wertgruppenfilter setzen** zulässig; bei anderen Regelarten wird das Setzen verhindert. |
| **Materialart in Matrix** | Wenn aktiviert, wird die **Materialartencode**-Spalte in der Regelmatrix eingeblendet, sodass dieselbe Regel je Materialart unterschiedliche Rückgabewerte liefern kann. Beim Umschalten wird die vorhandene Matrix nach Rückfrage gelöscht. |
| **Standardwerte verwenden** | Wenn aktiviert (nur bei **Eigenschaft setzen**), blendet die Karte die Gruppe **Standardwerte** ein; findet die Regelmatrix keinen Treffer, wird der dort hinterlegte Standardwert zurückgegeben, statt kein Ergebnis zu liefern. |
| **Ausgabetext** | Text für die Regelarten **Meldung, Bestätigung** und **Fehler**. Wenn gesetzt, wird er dem Anwender angezeigt; ein Platzhalter `%1` wird durch den Wert der zugeordneten Variablen ersetzt. Fehlt der Text, bricht die Ausführung mit einer Fehlermeldung ab. |

#### Werte der Regelart

Die **Regelart** hat einen leeren Anfangswert und die folgenden Ausprägungen; jede beschreibt, was beim Ausführen der Regel geschieht:

- **(leer):** Regel ohne Verhalten – dient nur als Platzhalter, bis eine Regelart gewählt wird.
- **Eigenschaft zurückgeben:** Liest den Eigenschaftswert (**Eigenschaft** über **Materialartencode** und **Eigenschaftencode**) des Artikels und gibt ihn als Ergebnis zurück; typisch als Eingang für Vergleiche oder weitere Regeln.
- **Eigenschaft setzen:** Ermittelt einen Wert (aus Variable, Formel oder Regelmatrix) und schreibt ihn in die Datensatzeigenschaft des Artikels; kann per **Matrix** je Eigenschaftskombination gesteuert werden.
- **Eigenschaftattribut setzen:** Setzt ein **Eigenschaftattribut** (siehe unten) der Datensatzeigenschaft, z. B. macht die Eigenschaft erforderlich oder unsichtbar, statt einen Wert zu schreiben.
- **Wertfilter zurückgeben / Wertfilter setzen:** Liest bzw. schreibt den **Wertfilter** einer Datensatzeigenschaft; steuert, welche Werte für die Eigenschaft zulässig sind.
- **Wertgruppenfilter zurückgeben / Wertgruppenfilter setzen:** Liest bzw. schreibt den **Wertgruppenfilter** einer Datensatzeigenschaft.
- **Wert zurückgeben:** Ermittelt einen Wert über Variable, Formel oder **Regelmatrix** und gibt ihn zurück, ohne ihn zu schreiben.
- **Konstante zurückgeben:** Gibt einen fest hinterlegten Konstantenwert des in der **Wertart** gewählten Typs zurück.
- **Formel:** Berechnet einen Ausdruck; Eigenschaftswerte werden mit `#Code#`, Variablen mit `$Variable$` in die **Formel** eingesetzt. Ist **Ausdruck zurückgeben** aktiv, wird der Text zurückgegeben, sonst das Rechenergebnis als Dezimalwert.
- **Meldung / Bestätigung / Fehler:** Zeigt dem Anwender den **Ausgabetext** als Meldung an, stellt eine Ja/Nein-**Bestätigung** (Ergebnis Ja/Nein) oder bricht mit einer **Fehler**-Meldung ab.
- **Artikelfeld setzen:** Schreibt den ermittelten Wert in ein wählbares Feld des **Artikels** (über **Feldname**/**Feldnr.**).
- **Artikelvorlage anwenden:** Wendet eine **Artikelvorlage** (über **Artikelvorlagencode** oder ermittelten Wert) auf den Artikel an.
- **Arbeitsgang verwenden:** Kopiert einen Arbeitsgang aus einem Quell-**Arbeitsplan** in den Arbeitsplan des Artikels; die Zielnummer richtet sich nach der **Regel Einrichtung**.
- **Arbeitsgangfeld setzen:** Schreibt den ermittelten Wert in ein Feld einer Arbeitsgangzeile.
- **Fertigungsstücklistekomponente verwenden:** Kopiert eine Komponentenzeile aus einer Quell-**Fertigungsstückliste** in die Fertigungsstückliste des Artikels.
- **Fertigungsstücklistenkomponentenfeld setzen:** Schreibt den ermittelten Wert in ein Feld einer Fertigungsstücklistenkomponentenzeile.
- **Fertigungsauftragsarbeitsgang verwenden:** Fügt beim Neuberechnen des Fertigungsauftrags einen Arbeitsgang in den **FA-Arbeitsplan** ein.
- **Fertigungsauftragsarbeitsgangfeld setzen:** Schreibt den ermittelten Wert in ein Feld einer FA-Arbeitsgangzeile.
- **Materialfilter zurückgeben / Materialfilter setzen:** Liest bzw. setzt einen **Materialfilter** des Artikels; über **Materialfilterart** wird zwischen Materialart- und Eigenschaftsfilter unterschieden.
- **Runden:** Rundet einen Dezimalwert gemäß **Rundungspräzision** und **Rundungsrichtung**.
- **Ersetzen:** Ersetzt im ermittelten Text den **Suchwert** durch den **Ersetzungswert**.
- **Enthält:** Prüft, ob der ermittelte Text den **Suchwert** enthält (Ergebnis Ja/Nein); **Gross-/Kleinschreibung beachten** steuert die Genauigkeit.

#### Regelart-abhängige Feldgruppen

Je nach **Regelart** blendet die **Regel**-Karte zusätzliche Gruppen ein. Die folgende Tabelle beschreibt die dann sichtbaren Felder.

| Gruppe / Feld | Erläuterung |
|---|---|
| **Materialfilter** – **Materialfilterart** | Sichtbar bei **Materialfilter zurückgeben/setzen**. Wenn auf Materialart gestellt, arbeitet die Regel mit einem Materialart-Filter und blendet die **Konstante** ein; bei Eigenschaftsfilter blendet sie **Eigenschaft** ein. |
| **Eigenschaft** – **Materialartencode**, **Eigenschaftencode**, **Eigenschaftenname**, **Eigenschaftswerte verwenden** | Sichtbar bei allen Eigenschafts-Regelarten. Wenn **Eigenschaftencode** gesetzt ist, wird der Datentyp aus der Eigenschaft in die **Wertart** übernommen; **Eigenschaftenname** und **Eigenschaftswerte verwenden** werden aus der Eigenschaft nachgeladen. |
| **Eigenschaftattribut** – **Eigenschaftattribut** | Sichtbar bei **Eigenschaftattribut setzen**. Bestimmt, welches Attribut der Eigenschaft gesetzt wird; die Wertart wird automatisch auf Ja/Nein gestellt. |
| **Konstante** – **Textkonstante, Dezimalkonstante, Ganzzahlkonstante, Ja/Nein-Konstante, Datumskonstante, Zeitkonstante, Datum/Zeit-Konstante** | Sichtbar bei **Konstante zurückgeben** (und bei Materialfilter mit Materialart). Nur das zur **Wertart** passende Feld ist editierbar; sein Inhalt wird als fester Wert zurückgegeben. |
| **Standardwerte** – dieselben Konstantenfelder als **Standardtext/-dezimal/-ganzzahl** usw. | Sichtbar bei **Eigenschaft setzen** mit aktivem **Standardwerte verwenden**. Wenn die Regelmatrix keinen Treffer liefert, wird der hier hinterlegte Standardwert geschrieben. |
| **Formel** – **Formel**, **Ausdruck zurückgeben** | Sichtbar bei **Formel**. Wenn **Ausdruck zurückgeben** aktiv ist, gibt die Regel den zusammengesetzten Text zurück; sonst das berechnete Dezimalergebnis. |
| **Ausgabetext** – **Ausgabetext** | Sichtbar bei **Meldung/Bestätigung/Fehler**; der angezeigte Text mit optionalem Platzhalter `%1`. |
| **Artikel** / **Arbeitsplan** / **Fertigungsstückliste** (Feldvariante) – **Feldnr.**, **Feldname** | Sichtbar bei den „…feld setzen“-Regelarten. Über den AssistEdit wählen Sie das Zielfeld; nur unterstützte Feldtypen sind zulässig, andernfalls erscheint „Feldart nicht zugelassen!“. |
| **Artikelvorlage** – **Artikelvorlagencode** | Sichtbar bei **Artikelvorlage anwenden**. |
| **Arbeitsplan** – **Arbeitsplannr.**, **Arbeitsplanversionscode**, **Arbeitsgangsnr.** | Sichtbar bei **Arbeitsgang verwenden**. Wenn keine Matrix gepflegt ist, ist **Arbeitsgangsnr.** direkt editierbar; mit Matrix wird der Arbeitsgang je Kombination ermittelt. |
| **Fertigungsstückliste** – **Fertigungsstückliste**, **Fertigungsstücklistenversion**, **Fertigungsstücklistenzeile** | Sichtbar bei **Fertigungsstücklistekomponente verwenden**; analog zum Arbeitsplan mit optionaler Matrixsteuerung. |
| **Runden** – **Rundungspräzision**, **Rundungsrichtung** | Sichtbar bei **Runden**. **Rundungsrichtung** kann **Kaufmännisch**, **Aufrunden** oder **Abrunden** sein. |
| **Suchen/Ersetzen** – **Suchwert**, **Ersetzungswert** | Sichtbar bei **Ersetzen**. |
| **Enthält** – **Suchwert**, **Gross-/Kleinschreibung beachten** | Sichtbar bei **Enthält**. |

**Werte der Rundungsrichtung:**

- **Kaufmännisch:** Rundet zum nächstliegenden Wert (auf oder ab).
- **Aufrunden:** Rundet stets zur größeren Zahl.
- **Abrunden:** Rundet stets zur kleineren Zahl.

**Werte des Eigenschaftattributs:**

- **(leer):** Kein Attribut – die Regel setzt keinen Attributwert.
- **Erforderlich:** Wenn gesetzt, wird die Datensatzeigenschaft als Pflichtfeld markiert.
- **Nicht editierbar:** Wenn gesetzt, kann der Anwender den Eigenschaftswert nicht mehr ändern.
- **Nicht sichtbar:** Wenn gesetzt, wird die Eigenschaft in der Erfassung ausgeblendet.
- **Null ist Wert:** Wenn gesetzt, gilt der Wert 0 als gültiger Wert und nicht als „leer“.

### Regeleigenschaften

**Prozesseinstieg:** Sobald eine Regel ihr Ergebnis aus einer **Regelmatrix** ermittelt, legen Sie hier fest, welche Eigenschaften an welcher **Position** die Matrix aufspannen und wie verglichen wird. Ohne mindestens eine Regeleigenschaft mit Position kann die Matrix nicht geöffnet werden („Keine Eigenschaften oder Positionen für Regelmatrix definiert!“).

**Einstieg:** Öffnen Sie in der **Regel**-Karte die Aktion **Eigenschaften**; die Seite **Regeleigenschaften** ist nach **Position** sortiert.

| Feld | Erläuterung |
|---|---|
| **Eigenschaftencode** | Wählt die Eigenschaft, die eine Spaltengruppe der Matrix bildet. Wenn gesetzt, wird der **Datentyp** aus der Eigenschaft übernommen und – falls noch keine Position vergeben – die nächste freie Position gesetzt. |
| **Eigenschaftenname** | Zeigt den Namen der gewählten Eigenschaft an; dient der Kontrolle. |
| **Datentyp** | Zeigt den Datentyp der Eigenschaft (Text, Ganzzahl, Dezimal, Datum). Er steuert, welche Matrixspalte (Text/Ganzzahl/Dezimal) verwendet und welche Filtermethode zulässig ist. |
| **Position** | Legt die Reihenfolge der Eigenschaft in der Matrix fest (1–10). Wenn eine Position bereits belegt ist, erscheint „Position … wird bereits für Eigenschaftencode … verwendet!“. |
| **Filtermethode** | Bestimmt, wie der Eigenschaftswert gegen die Matrixwerte geprüft wird. Für Zahlen und Datum muss die Methode in allen Positionen gleich sein, sonst erscheint „Filtermethode für Ganzzahl/Dezimal muss in allen Positionen gleich sein!“. |
| **Zusätzliche Suche mit Leer** | Wenn aktiviert, wird zusätzlich zur Wertsuche eine Suche mit leerem Wert durchgeführt, sodass auch Matrixzeilen ohne konkreten Wert als Treffer gelten. |

**Werte der Filtermethode:**

- **gleich (=):** Trifft Matrixzeilen mit exakt gleichem Wert.
- **von (>=):** Trifft Zeilen, deren Grenzwert kleiner oder gleich dem Eigenschaftswert ist (untere Schranke).
- **bis (<=):** Trifft Zeilen mit oberer Schranke.
- **über (>):** Trifft Zeilen echt oberhalb.
- **unter (<):** Trifft Zeilen echt unterhalb.
- **ungleich (<>):** Trifft Zeilen mit abweichendem Wert.
- **von/bis:** Wertebereich; die Matrix erhält zusätzlich eine zweite (Sekundär-)Spalte für die obere Grenze.

### Regelmatrix

**Prozesseinstieg:** Die **Regelmatrix** ist die Nachschlagetabelle einer Regel: Je Kombination der in den **Regeleigenschaften** definierten Positionen hinterlegen Sie den Rückgabewert. So liefert dieselbe Regel je nach Eigenschaftswerten (und optional je **Materialart**) unterschiedliche Ergebnisse.

**Einstieg:** Öffnen Sie in der **Regel**-Karte die Aktion **Matrix**. Beim Verlassen bereinigt das System nicht mehr benötigte Direktwerte der Regel.

Die Spalten werden dynamisch nach den Regeleigenschaften eingeblendet:

| Feldgruppe | Erläuterung |
|---|---|
| **Zeilennr.** | Laufende Nummer der Matrixzeile. |
| **Materialartencode** | Nur sichtbar, wenn an der Regel **Materialart in Matrix** aktiv ist. Wenn gesetzt, gilt die Zeile nur für Artikel dieser Materialart. |
| **Text 1**–**Text 10** | Suchspalten für Eigenschaften vom Datentyp Text; eingeblendet werden nur die Spalten der belegten Positionen. |
| **Dezimal 1**–**Dezimal 10** und **Sek. Dezimal 1**–**Sek. Dezimal 10** | Suchspalten für Dezimal-Eigenschaften; die Sekundärspalte wird bei der Filtermethode **von/bis** als obere Grenze verwendet. |
| **Ganzzahl 1**–**Ganzzahl 10** und **Zweite Ganzzahl 1**–**Zweite Ganzzahl 10** | Suchspalten für Ganzzahl-Eigenschaften; die zweite Spalte dient wieder der oberen Grenze bei **von/bis**. |
| **Rückgabewert Text/Dezimal/Ganzzahl/Ja-Nein/Datum/Zeit/Datum/Zeit** | Ergebnisspalte; eingeblendet wird die zur **Wertart** der Regel passende Spalte. Ihr Wert wird zurückgegeben, wenn die Zeile über die Positionen getroffen wird. |

> Grundprinzip der Auswertung: Das System filtert die Matrix Position für Position nach den aktuellen Eigenschaftswerten des Artikels. Bleibt am Ende ein Treffer, wird dessen Rückgabewert verwendet; bleibt keiner und ist **Standardwerte verwenden** aktiv, greift der Standardwert.

### Materialart und Regelabläufe

**Prozesseinstieg:** An der **Materialartenkarte** verbinden Sie die zuvor definierten Regeln zu **Regelabläufen**. Je Bereich (Eigenschaften, Vormaterialsuchfilter, Arbeitsplan, Fertigungsstückliste, FA-Arbeitsplan) gibt es einen eigenen Regelablauf, der beim Entsperren eines Artikels dieser Materialart ausgeführt wird. Die zugehörigen Regelablauf-IDs werden an der Materialart gespeichert.

**Einstieg:** Öffnen Sie in der Materialarten-Übersicht die gewünschte Zeile und rufen Sie die **Materialartenkarte** auf. In der Aktionsgruppe **Regelablauf** stehen die folgenden Aktionen bereit; jede öffnet (und legt beim ersten Aufruf an) den passenden Regelablauf.

| Aktion | Erläuterung |
|---|---|
| **Eigenschaften-Regelablauf** | Öffnet den Regelablauf, der beim Entsperren die **Eigenschaften** des Artikels ermittelt und setzt. |
| **Vormaterialsuchfilter-Regelablauf** | Öffnet den Regelablauf, der den **Materialfilter** des Artikels für die Vormaterialsuche aufbaut. |
| **Arbeitsplan-Regelablauf** | Öffnet den Regelablauf, der den **Arbeitsplan** des Artikels mit Arbeitsgängen füllt. |
| **Fertigungsstückliste-Regelablauf** | Öffnet den Regelablauf, der die **Fertigungsstückliste** des Artikels mit Komponenten füllt. |
| **FA-Arbeitsplan-Regelablauf** | Öffnet den Regelablauf, der beim Neuberechnen eines Fertigungsauftrags den **FA-Arbeitsplan** aufbaut. |

**Grundfelder der Materialartenkarte (zur Navigation):**

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger Code der Materialart; über ihn wird der Regelablauf zugeordnet. |
| **Beschreibung** | Klartextname der Materialart. |

**Wichtige Automatik:** Wird an einem Artikel eine Materialart gesetzt, die einen oder mehrere Regelabläufe besitzt, so wird der Artikel automatisch **Gesperrt**. Erst beim **Entsperren** laufen die Regelabläufe. Dieses Verhalten ist im Kapitel **Automatik im Tagesablauf** beschrieben.

### Direkte Regeln an Datensatzeigenschaften

**Prozesseinstieg:** Nicht jede Automatik braucht einen Regelablauf. Für einfache, sofort wirkende Logik hinterlegen Sie eine als **Direkt** markierte Regel unmittelbar an einer Datensatzeigenschaft. Sie wird ausgeführt, sobald der Anwender den **Wert** dieser Eigenschaft ändert.

**Einstieg:** Öffnen Sie am Artikel bzw. an der Materialart die **Datensatzeigenschaften** (Eigenschaftszeilen). Die App ergänzt dort die Spalte **Direkter Regelcode**.

| Feld | Erläuterung |
|---|---|
| **Direkter Regelcode** | Nimmt einen oder mehrere (mit Semikolon getrennte) direkte Regelcodes auf. Wenn gesetzt, wird beim Ändern des Eigenschaftswerts jede hinterlegte Regel ausgeführt. Über die Auswahl werden nur als **Direkt** markierte Regeln angeboten, deren **Materialartencode** zur Zeile passt; unpassende Regelarten oder ein abweichender **Eigenschaftencode** werden abgewiesen. |

Zur Orientierung werden in dieser Zeile die verifizierten Basisfelder der Datensatzeigenschaft mitgeführt: **Eigenschaftsname**, **Wert**, **Wertfilter**, **Wertgruppenfilter** sowie die Attribute **Erforderlich**, **Nicht editierbar**, **Nicht sichtbar** und **Null ist Wert**. Eine direkte Regel kann genau diese Werte bzw. Attribute setzen.

## Regelabläufe erstellen und bearbeiten

Ein **Regelablauf** ist ein geordnetes, eingerücktes Programm aus Regeln, Verzweigungen und Variablen. Er wird je Bereich an einer Materialart hinterlegt (siehe **Materialart und Regelabläufe**) und beim Entsperren des Artikels abgearbeitet.

### Regelablauf (Zeilenansicht)

**Einstieg:** über eine der Regelablauf-Aktionen der **Materialartenkarte**. Die Seite **Regelablauf** zeigt die Zeilen des Ablaufs; die Einrückung bildet die **Wenn/Sonst/Ende**-Ebenen ab.

| Feld | Erläuterung |
|---|---|
| **Ablauf** | Zeigt den lesbaren Text der Zeile (z. B. „Wenn (…) dann“, „Regel …“, „Meldung …“). Dient der Kontrolle des Ablaufs und ist nicht editierbar. |
| **Zeilenart** | Bestimmt die Art der Zeile. Beim Ändern werden die Ebenen neu berechnet und nicht mehr passende Felder geleert. Die Werte sind unten beschrieben. |
| **Regelcode** | Wählt die auszuführende **Regel**. Wenn gesetzt, wird die Variable geleert und die **Wertart** aus der Regel übernommen. Bei **Meldung/Bestätigung/Fehler** stehen nur Regeln der entsprechenden Regelart zur Auswahl. |
| **Variable** | Alternative zum Regelcode: verweist auf eine **Regelablaufvariable** desselben Ablaufs. Wenn gesetzt, wird der Regelcode geleert. |
| **Vergleichszeichen** | Nur bei **Wenn (Vergleich)**: Operator (=, <>, >, >=, <, <=) für den Vergleich der linken mit der rechten Seite. |
| **Vergleichsregelcode** | Rechte Seite eines Vergleichs, wenn sie aus einer Regel stammt. |
| **Vergleichsvariable** | Rechte Seite eines Vergleichs, wenn sie aus einer Variablen stammt; schließt den Vergleichsregelcode aus. |
| **Wertart** | Zeigt die Wertart der Zeile (aus Regel oder Variable) und steuert den Datentyp des Vergleichs. |

**Werte der Zeilenart:**

- **(leer):** Noch nicht bestimmte Zeile.
- **Regel:** Führt die unter **Regelcode** gewählte Regel aus.
- **Wenn (Wahr):** Beginn eines Blocks, der nur ausgeführt wird, wenn die Regel/Variable Ja/Nein = wahr liefert.
- **Wenn (Falsch):** Beginn eines Blocks, der nur bei Ergebnis „falsch“ ausgeführt wird.
- **Wenn (Vergleich):** Beginn eines Blocks, der ausgeführt wird, wenn der Vergleich (linke Seite **Vergleichszeichen** rechte Seite) zutrifft.
- **Sonst:** Kehrt die Bedingung des zugehörigen Wenn-Blocks um.
- **Ende:** Schließt einen Wenn-/Sonst-Block; die Verarbeitung kehrt auf die vorige Ebene zurück.
- **Meldung:** Zeigt dem Anwender den Ausgabetext der Regel als Hinweis an.
- **Bestätigung:** Stellt eine Ja/Nein-Rückfrage; das Ergebnis kann eine Verzweigung steuern.
- **Fehler:** Bricht den Ablauf mit einer Fehlermeldung ab.
- **Variable setzen:** Schreibt das Regelergebnis in die zugeordnete **Variable**, damit spätere Zeilen darauf zugreifen.

### Regel Flow Editor

**Prozesseinstieg:** Der **Regel Flow Editor** ist die grafische Alternative zur Zeilenansicht: Sie ziehen Regel- und Verzweigungsknoten und verbinden sie zu einem Ablauf. Er eignet sich, um komplexe Abläufe übersichtlich zu modellieren.

**Einstieg:** Öffnen Sie im **Regelablauf** die Aktion **Flow Editor**. Nach dem Speichern erscheint die Zeilenansicht mit der Rückfrage **„Ist der Flow korrekt?“**; bestätigen Sie mit Ok, wird der Ablauf übernommen, andernfalls der vorherige Stand wiederhergestellt.

### Regelablaufvariablen

**Prozesseinstieg:** **Regelablaufvariablen** halten Zwischenergebnisse eines Ablaufs oder liefern Kontextwerte (z. B. das Arbeitsdatum). Sie werden in Zeilen als linke oder rechte Vergleichsseite oder als Ziel von **Variable setzen** verwendet.

**Einstieg:** Öffnen Sie im **Regelablauf** die Aktion **Variablen**.

| Feld | Erläuterung |
|---|---|
| **Variable** | Eindeutiger Name der Variablen innerhalb des Ablaufs. Wird eine benutzte Variable gelöscht, erscheint „Die Regelablaufvariable ist in Gebrauch.“. |
| **Variablenart** | Legt fest, woher der Variablenwert stammt (siehe Werte unten). Beim Ändern werden die passenden Wertfelder editierbar. |
| **Eigenschaftencode** | Nur bei Variablenart **Artikeleigenschaft**: die Eigenschaft, deren Wert die Variable liefert. |
| **Wertart** | Datentyp der Variablen (**Ja/Nein, Datum, Datum/Zeit, Dezimal, Ganzzahl, Text, Zeit**); steuert, welches Wertfeld editierbar ist. |
| **Textwert / Dezimalwert / Ganzzahlwert / Ja-Nein-Wert / Datumswert / Zeitwert / Datum/Zeit-Wert** | Fester Startwert bei Variablenart **Normal**; nur das zur **Wertart** passende Feld ist editierbar. |

**Werte der Variablenart:**

- **Normal:** Freier, fest eingegebener Wert im passenden Wertfeld.
- **Mandantenname:** Liefert den Namen des aktuellen Mandanten.
- **Arbeitsdatum:** Liefert das Arbeitsdatum von Business Central.
- **Aktuelles Datum:** Liefert das heutige Datum.
- **Aktuelle Zeit:** Liefert die aktuelle Uhrzeit.
- **Aktuelles Datum/Zeit:** Liefert den aktuellen Zeitstempel.
- **Artikelmaterialart:** Liefert die Materialart des verarbeiteten Artikels.
- **Artikeleigenschaft:** Liefert den Wert der unter **Eigenschaftencode** gewählten Eigenschaft.
- **Artikelfeld - Basisartikel:** Liefert einen Feldwert des Basisartikels.

## Automatik im Tagesablauf

In diesem Kapitel wird beschrieben, wann und wie die eingerichteten Regelabläufe im Tagesgeschäft automatisch wirken. Alle Auslöser sind Standardvorgänge am Artikel bzw. am Fertigungsauftrag; einen eigenen Beleg gibt es nicht.

### Materialart setzen sperrt den Artikel

Setzen Sie an einem Artikel die **Materialart** und besitzt diese Materialart mindestens einen Regelablauf, so wird der Artikel automatisch auf **Gesperrt** gesetzt. Damit wird verhindert, dass ein Artikel mit unvollständigen, noch nicht durch die Regeln aufgebauten Stammdaten in Belegen verwendet wird. Pflegen Sie nun in Ruhe die Eingangsdaten (z. B. Eigenschaftswerte), während der Artikel gesperrt ist.

### Artikel entsperren führt die Regelabläufe aus

Beim **Entsperren** des Artikels (Kennzeichen **Gesperrt** wird zurückgenommen) laufen die Regelabläufe der Materialart in fester Reihenfolge:

1. **Eigenschaften-Regelablauf** – ermittelt und setzt die Eigenschaftswerte.
2. **Vormaterialsuchfilter-Regelablauf** – baut den Materialfilter auf.
3. **Arbeitsplan-Regelablauf** – füllt den Arbeitsplan.
4. **Fertigungsstückliste-Regelablauf** – füllt die Fertigungsstückliste.

Danach steht der Artikel mit vollständig aufgebauten Stammdaten zur Verfügung.

### Direkte Regel bei Wertänderung

Ändert der Anwender an einer **Datensatzeigenschaft** den **Wert** und ist ein **Direkter Regelcode** hinterlegt, wird die Regel sofort ausgeführt – ohne Entsperren und ohne Regelablauf. So lassen sich abhängige Eigenschaftswerte unmittelbar nachziehen.

### FA-Arbeitsplan beim Fertigungsauftrag

Beim Neuberechnen des Arbeitsplans eines Fertigungsauftrags – sowie beim Erzeugen eines Fertigungsauftrags aus einer Verkaufszeile – wird der **FA-Arbeitsplan-Regelablauf** der Materialart ausgeführt und baut den Arbeitsplan des Fertigungsauftrags auf.

## Berechtigungen

Für den Betrieb stellt das Modul den Berechtigungssatz **Regel Allgemein** bereit. Er bestimmt die Berechtigungen für die Objekte der regelbasierten Datenverwaltung und legt fest, welche Aktionen Anwenderinnen und Anwender mit diesem Satz an Regeln, Regelmatrizen, Regeleigenschaften und Regelabläufen ausführen können. Weisen Sie den Berechtigungssatz den Rollen zu, die Regeln pflegen oder Artikel entsperren.

## FAQ und Troubleshooting

### Warum wird mein Artikel beim Setzen der Materialart automatisch gesperrt?

Weil die gewählte **Materialart** mindestens einen Regelablauf besitzt. Das System sperrt den Artikel, damit er nicht mit unvollständigen Stammdaten verwendet wird; die Regeln bauen die Daten erst beim **Entsperren** auf.

### Wie starte ich die Automatik – wo ist der „Buchen“-Knopf?

Es gibt keinen Buchungs- oder Freigabebeleg. Die Automatik wird ausgelöst, indem Sie den Artikel **entsperren**. Beim Entsperren laufen die Regelabläufe automatisch.

### In welcher Reihenfolge laufen die Regelabläufe?

Beim Entsperren werden **Eigenschaften-Regelablauf**, dann **Vormaterialsuchfilter-Regelablauf**, dann **Arbeitsplan-Regelablauf** und zuletzt **Fertigungsstückliste-Regelablauf** ausgeführt. Der **FA-Arbeitsplan-Regelablauf** läuft separat beim Berechnen des Fertigungsauftrags.

### Warum kann ich eine Regel nicht löschen?

Weil sie noch verwendet wird. Ist die Regel in einer **Regelablaufzeile** (als **Regelcode** oder **Vergleichsregelcode**) oder als **Direkter Regelcode** einer Eigenschaft eingebunden, meldet das System „Regel … wird verwendet. Löschen nicht möglich!“ bzw. „… wird als direkte Regel verwendet!“. Entfernen Sie zuerst die Verwendungen.

### Warum kann ich den Code einer Regel nicht umbenennen und keine Sonderzeichen verwenden?

Das Umbenennen ist gesperrt („Ein Umbenennen ist nicht erlaubt!“), damit bestehende Verweise gültig bleiben. Sonderzeichen wie `. ; # $` sind im **Code** nicht zulässig, weil sie in Formeln und Filtern als Steuerzeichen dienen würden.

### Warum kann ich die Matrix nicht öffnen?

Die **Regelmatrix** benötigt mindestens eine **Regeleigenschaft** mit einer **Position**. Fehlt sie, erscheint „Keine Eigenschaften oder Positionen für Regelmatrix definiert!“. Pflegen Sie zuerst die Regeleigenschaften.

### Warum meldet das System „Filtermethode … muss in allen Positionen gleich sein“?

Für Eigenschaften vom Datentyp **Ganzzahl**, **Dezimal** oder **Datum** muss dieselbe **Filtermethode** über alle Positionen verwendet werden, damit die Matrix eindeutig auswertet. Stellen Sie alle numerischen Positionen auf dieselbe Methode.

### Warum liefert eine Regel keinen Wert, obwohl die Matrix gepflegt ist?

Vermutlich trifft keine Matrixzeile auf die aktuellen Eigenschaftswerte des Artikels. Aktivieren Sie an der Regel **Standardwerte verwenden** und hinterlegen Sie einen Standardwert, oder ergänzen Sie mit **Zusätzliche Suche mit Leer**, damit auch Zeilen ohne konkreten Wert getroffen werden.

### Wann verwende ich eine direkte Regel statt eines Regelablaufs?

Nutzen Sie eine **Direkt** markierte Regel an der **Datensatzeigenschaft**, wenn eine Automatik sofort bei jeder **Wert**-Änderung greifen soll, ohne den Artikel zu entsperren. Für mehrstufige, verzweigte Logik verwenden Sie einen **Regelablauf**.

### Warum kann ich eine Eigenschaft nicht löschen?

Weil sie in einer Regel oder Regeleigenschaft verwendet wird. Das System meldet „Die Eigenschaft … wird in Regel … verwendet!“, wenn die Eigenschaft in einer Regel, einer Regeleigenschaft, als **Direkter Regelcode** oder in einer Regelablaufzeile der Materialart eingebunden ist. Entfernen Sie zuerst diese Verwendungen.

## Typische Anwendungsfälle

### Neuer Artikel wird per Materialart automatisch aufgebaut

- **Auslöser:** Die Arbeitsvorbereitung erhält den internen Auftrag, für eine bekannte Produktgruppe (Materialart) einen neuen Artikel anzulegen, dessen Eigenschaften, Arbeitsplan und Stückliste dem Standard dieser Gruppe folgen sollen.
- **Einstieg in BC:** Öffnen Sie die Artikelübersicht und legen Sie über **Neu** einen Artikel an. Setzen Sie im Artikel die **Materialart**. Besitzt die Materialart Regelabläufe, wird der Artikel sofort **Gesperrt**.
- **Kernablauf:** Pflegen Sie die notwendigen Eingangswerte an den **Datensatzeigenschaften** des Artikels (Voraussetzung: die Regeln und Regelabläufe der Materialart sind gemäß Kapitel **Stammdaten** eingerichtet). Nehmen Sie anschließend das Kennzeichen **Gesperrt** zurück (**entsperren**). Nun laufen nacheinander **Eigenschaften-Regelablauf**, **Vormaterialsuchfilter-Regelablauf**, **Arbeitsplan-Regelablauf** und **Fertigungsstückliste-Regelablauf**.
- **Abschluss:** Der Artikel ist entsperrt und trägt die von den Regeln gesetzten Eigenschaften sowie – falls konfiguriert – einen automatisch gefüllten Arbeitsplan und eine Fertigungsstückliste. Er kann jetzt in Belegen verwendet werden.

### Eigenschaftswert ändern löst eine direkte Regel aus

- **Auslöser:** Eine Anwenderin passt an einem bestehenden Artikel einen Eigenschaftswert an (z. B. eine Abmessung), von dem weitere Eigenschaften abhängen.
- **Einstieg in BC:** Öffnen Sie am Artikel die **Datensatzeigenschaften**. In der Zeile der betreffenden Eigenschaft ist ein **Direkter Regelcode** hinterlegt (Voraussetzung: eine als **Direkt** markierte Regel wurde gemäß Kapitel **Direkte Regeln an Datensatzeigenschaften** zugeordnet).
- **Kernablauf:** Ändern Sie den **Wert** der Eigenschaft. Unmittelbar nach der Eingabe führt das System die hinterlegte(n) Regel(n) aus – z. B. **Eigenschaft setzen**, **Formel** oder **Wertfilter setzen** – und aktualisiert die abhängigen Eigenschaften.
- **Abschluss:** Die abgeleiteten Eigenschaftswerte bzw. Attribute sind gesetzt, ohne dass der Artikel gesperrt und wieder entsperrt werden musste.
