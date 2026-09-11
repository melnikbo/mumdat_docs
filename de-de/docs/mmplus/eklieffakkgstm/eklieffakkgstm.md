---
title: Anwenderhandbuch m+m Invoice Purchase Receipt with Unit Conversion
---

# Anwenderhandbuch m+m Invoice Purchase Receipt with Unit Conversion

## Einleitung

Dieses Modul erweitert den bestehenden Ablauf **Einkaufslieferung fakturieren** um die drei Umrechnungsmengen **KG**, **Meter** und **Stück**. Zusätzlich zur klassischen Menge in der Basiseinheit führt Business Central damit für jede Einkaufslieferzeile parallel mit, wie viel Gewicht (KG), Länge (Meter) und Stückzahl geliefert, bereits fakturiert, noch nicht fakturiert und verbraucht wurde. Beim Fakturieren werden diese Umrechnungsmengen automatisch mit der Einkaufsrechnung, den Reservierungsposten und dem Umlagerungsbuchblatt synchron gehalten.

Das Modul ist eine Brückenerweiterung: Es besitzt selbst keine eigene Einrichtungsseite und keine eigene Stammdatenkarte. Seine gesamte sichtbare Oberfläche besteht aus zusätzlichen Spalten in der Liste **Einkaufslieferung fakturieren** sowie aus drei erfassbaren Spalten (**zu fakturierende KG**, **Zu fakturierende Meter**, **Zu fakturierende Stück**), über die Sie eine Teilfakturierung mengengenau steuern.

**Zielgruppe:** Primär sind es die **operativen Anwender in der Rechnungsprüfung und im Wareneingang**, die täglich Einkaufslieferungen fakturieren und dabei Gewicht, Länge oder Stückzahl kontrollieren – zum Beispiel im Stahl- und Metallhandel, wo eine Coil-Lieferung in KG und Meter geführt wird. Sekundär richtet sich das Handbuch an Administratoren und Key-User, die die Voraussetzungen für die Mengenumrechnung einrichten (Abschnitt **Einrichtung**).

**Kurzer Prozessüberblick:** Der Anwender öffnet die Seite **Einkaufslieferung fakturieren**, wählt die noch nicht vollständig fakturierten Lieferzeilen aus, prüft bzw. begrenzt die zu fakturierenden Mengen (auch getrennt nach KG, Meter oder Stück) und stößt anschließend über die Aktion **Pflichtentnahme** die Fakturierung an. Die Umrechnungsmengen wandern dabei automatisch in die Folgebelege.

## Schnellstart für Anwender

Voraussetzung: Die Mengenumrechnung ist eingerichtet (siehe **Einrichtung**) und die Einkaufslieferung wurde bereits gebucht, sodass sie in der Liste erscheint.

1. Öffnen Sie über **Suchen** die Seite **Einkaufslieferung fakturieren**. Die Liste zeigt automatisch nur Zeilen mit einer offenen Menge (**Menge** größer als 0).
2. Suchen Sie die zu fakturierende Zeile anhand von **Belegnr.**, **Kreditorennr.** oder **Chargennr.**. Prüfen Sie in den Spalten **KG nicht fakturiert**, **Meter nicht fakturiert** und **Stück nicht fakturiert**, welche Umrechnungsmengen noch offen sind.
3. *(Optional bei Teilfakturierung)* Tragen Sie in **zu fakturierende KG**, **Zu fakturierende Meter** oder **Zu fakturierende Stück** die gewünschte Teilmenge ein. Der jeweilige Wert darf die zugehörige nicht fakturierte Menge nicht überschreiten; **Menge zu fakturieren** wird automatisch passend zurückgerechnet.
4. Führen Sie die Aktion **Pflichtentnahme** aus. Existiert zur Zeile bereits eine ungebuchte Einkaufsrechnung, bestätigen Sie zunächst die Sicherheitsabfrage.
5. Die Einkaufsrechnung wird mit den Umrechnungsmengen KG, Meter und Stück erzeugt bzw. ergänzt. Diese Werte werden zugleich in die Reservierungsposten und – bei Chargenführung – in das Umlagerungsbuchblatt übernommen.
6. *(Optional)* Setzen Sie mit der Aktion **Kred.-Rechnungsnr. setzen** die Kreditorenrechnungsnummer für die markierten Zeilen.

Diese Kurzfolge entspricht dem vollständigen Fakturierungsablauf; die Detailerläuterung finden Sie unter **Tägliche Arbeit: Einkaufslieferung fakturieren**.

## Einrichtung

Für das Modul selbst ist im Webclient **keine zusätzliche Einrichtung** erforderlich. In der Erweiterungsverwaltung müssen die App **m+m Invoice Purchase Receipt with Unit Conversion** und ihre Abhängigkeiten (m+m Cloud Base, m+m Invoice Purchase Receipt, m+m Unit Conversion) installiert sein.

Damit in den Spalten **KG**, **Meter** und **Stück** tatsächlich Werte erscheinen, müssen jedoch die fachlichen Voraussetzungen der Mengenumrechnung erfüllt sein. Diese Voraussetzungen werden in der Abhängigkeit **m+m Unit Conversion** gepflegt und wirken sich anschließend in der Liste **Einkaufslieferung fakturieren** aus. Der folgende Abschnitt beschreibt diese Kette in Abhängigkeitsreihenfolge.

### Voraussetzungen für die Mengenumrechnung einrichten

**Wer richtet ein und wann:** Der Administrator bzw. Key-User richtet die Mengenumrechnung einmalig je Artikel ein, bevor Einkaufslieferungen dieser Artikel fakturiert werden. Konsumiert werden die Einstellungen später in der täglichen Arbeit auf der Seite **Einkaufslieferung fakturieren** (siehe **Tägliche Arbeit**).

**Ablauf in Abhängigkeitsreihenfolge:**

1. **Zuerst** hinterlegen Sie im Modul **m+m Unit Conversion** je Artikel und Einheit die Umrechnungsfaktoren (z. B. KG je Meter und KG je Stück). Wenn diese Faktoren gesetzt sind, kann Business Central aus der erfassten Basismenge die Werte für KG, Meter und Stück berechnen; ohne Faktoren bleiben die Umrechnungsspalten 0.
2. **Danach** werden bei der Buchung des Wareneingangs die Umrechnungsmengen an der Einkaufslieferzeile geführt. Wenn die Einkaufslieferung gebucht ist, stehen die Mengen als Ausgangswerte für die Fakturierung bereit; die Liste **Einkaufslieferung fakturieren** liest sie aus der gebuchten Lieferzeile bzw. – bei Chargenführung – aus den Artikelposten.
3. **Schließlich** ruft der Anwender im Tagesgeschäft die Seite **Einkaufslieferung fakturieren** auf und stößt über **Pflichtentnahme** die Fakturierung an. Wenn dieser Schritt ausgeführt wird, überträgt das Modul die Umrechnungsmengen automatisch in die Einkaufsrechnung und die Reservierungsposten.

**Abhängigkeitshinweis:** Die tatsächlichen KG-je-Meter- bzw. KG-je-Stück-Faktoren werden pro Zeile aus der gebuchten Einkaufslieferzeile ermittelt; ist die Zeile chargengeführt, werden die Faktoren stattdessen aus dem passenden Artikelposten der Charge gelesen. Fehlt ein tatsächlicher Faktor, greift der theoretische Faktor. Pflegen Sie die Faktoren daher vollständig, damit die zurückgerechneten Mengen korrekt sind.

### Berechtigungen

Das Modul liefert den Berechtigungssatz **m+m PIUC Permission** (Anzeigename „All permissions“) mit. Er bestimmt die Berechtigungen für die beiden Verarbeitungs-Codeunits der Erweiterung und legt fest, welche Aktionen ein Anwender im Zusammenhang mit der Mengenumrechnung ausführen kann. Weisen Sie diesen Berechtigungssatz den Anwendern zu, die Einkaufslieferungen fakturieren; die eigentliche Fakturierungsberechtigung (Zugriff auf die Seite **Einkaufslieferung fakturieren** und die zugrunde liegenden Einkaufsbelege) wird zusätzlich über die Berechtigungssätze der Basismodule gesteuert.

## Tägliche Arbeit: Einkaufslieferung fakturieren

Die gesamte tägliche Arbeit findet auf der Seite **Einkaufslieferung fakturieren** statt. Diese Seite gehört zum Basismodul; die vorliegende Erweiterung ergänzt sie um die Umrechnungsspalten KG, Meter und Stück in jeweils fünf Ausprägungen (Menge, fakturiert, nicht fakturiert, verbraucht, zu fakturieren).

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Einkaufslieferung fakturieren**. Die Seite ist eine unternehmensweite Aufgabenliste und besitzt keine übergeordnete Stammdatenseite; der Einstieg über **Suchen** ist daher der vorgesehene Weg. Beim Öffnen filtert die Seite automatisch auf Zeilen mit **Menge** größer als 0, sodass ausschließlich noch zu fakturierende Lieferzeilen erscheinen.

**Steuernde Einrichtung:** Ob und mit welchen Werten die Umrechnungsspalten gefüllt sind, hängt vollständig von der Mengenumrechnung des Artikels ab (Modul **m+m Unit Conversion**, siehe **Voraussetzungen für die Mengenumrechnung einrichten**). Sind dort keine Umrechnungsfaktoren hinterlegt, bleiben KG, Meter und Stück auf 0, und es kann nur über die Basismenge fakturiert werden.

### Spalten der Zeilenliste

Business Central zeigt in der Zeilenliste sowohl die Felder des Basismoduls als auch die von dieser Erweiterung ergänzten Umrechnungsspalten auf einem Bildschirm. Die folgende Tabelle dokumentiert die gesamte sichtbare Zeile.

**Identifikations- und Kopfangaben (aus dem Basismodul, nicht erfassbar):**

| Feld | Erläuterung |
|------|-------------|
| Belegnr. | Nummer der gebuchten Einkaufslieferung. Wenn Sie eine Zeile auswählen, beziehen sich alle Aktionen auf genau diesen Beleg. |
| Buchungsdatum | Buchungsdatum der gebuchten Einkaufslieferung; dient zur zeitlichen Einordnung der offenen Fakturierung. |
| Kred.-Lieferungsnr. | Lieferscheinnummer des Kreditors. Wenn Sie mehrere Lieferungen desselben Kreditors sehen, unterscheiden Sie sie hierüber. |
| Kred.-Rechnungsnr. | Rechnungsnummer des Kreditors. Wenn sie noch leer ist, können Sie sie über die Aktion **Kred.-Rechnungsnr. setzen** nachtragen. |
| Kreditorennr. | Nummer des Kreditors der Lieferung. |
| Kreditorenname | Name des Kreditors; erleichtert das Auffinden der richtigen Zeile ohne Rückgriff auf die Nummer. |
| Kreditoradresse | Adresse des Kreditors (Kontrollinformation zur Zeile). |
| Lagerortcode | Lagerort der gebuchten Lieferzeile; relevant, wenn dieselbe Ware an mehreren Lagerorten liegt. |
| Lagerplatzcode | Lagerplatz innerhalb des Lagerorts. |
| Art | Zeilenart aus der Einkaufslieferung. Die Mengenumrechnung dieses Moduls wirkt ausschließlich bei der Art **Artikel**; bei anderen Arten (z. B. Sachkonto) bleiben KG, Meter und Stück ohne Funktion. |
| Nr. | Artikelnummer der Zeile. |
| Beschreibung | Artikelbezeichnung. |
| Beschreibung 2 | Ergänzende Artikelbezeichnung. |
| Chargennr. | Chargennummer der Zeile. Wenn eine Charge gesetzt ist, ermittelt das Modul verbrauchte und fakturierte Umrechnungsmengen chargengenau aus den Artikelposten. |
| Chargen-Beschreibung | Beschreibung der Charge (Kontrollinformation). |
| Einheit | Basiseinheit der Menge (Klartext). |
| Variantencode | Artikelvariante der Zeile, sofern geführt. |
| Einheitencode | Code der Basiseinheit; dient dem Modul als Ausgangseinheit für die Umrechnung nach KG, Meter und Stück. |

**Basismengen (aus dem Basismodul, nicht erfassbar außer „Menge zu fakturieren“):**

| Feld | Erläuterung |
|------|-------------|
| Menge | Gelieferte Gesamtmenge in Basiseinheit. Grundlage aller Umrechnungen. |
| Fakturierte Menge | Bereits fakturierter Anteil der Menge. |
| nicht fakturierte Menge | Noch offener, zu fakturierender Anteil der Menge. |
| Verbrauchte Menge | Bereits verbrauchter Anteil (Verbrauch/negative Regulierung) laut Artikelposten. |
| Menge zu fakturieren | Die Menge, die mit der nächsten Fakturierung verrechnet wird. Wenn Sie eine Umrechnungsmenge (KG, Meter oder Stück) erfassen, wird dieser Wert automatisch zurückgerechnet; erfassen Sie ihn direkt, dürfen Sie ihn nicht größer als die nicht fakturierte Menge setzen. |

### Umrechnungsspalten dieser Erweiterung

Die folgenden 15 Spalten fügt diese Erweiterung hinzu. KG, Meter und Stück treten jeweils in fünf Ausprägungen auf, die den Basismengen entsprechen. Alle Spalten außer den drei „zu fakturierenden“ sind Anzeigefelder und nicht erfassbar.

**Gelieferte Umrechnungsmengen (Anzeige):**

| Feld | Erläuterung |
|------|-------------|
| KG | Wenn der Artikel eine KG-Umrechnung besitzt, zeigt diese Spalte das gelieferte Gewicht der Zeile in KG. Sie ist die Bezugsgröße für „KG fakturiert“, „KG nicht fakturiert“ und „zu fakturierende KG“. |
| Meter | Wenn eine Meter-Umrechnung besteht, zeigt diese Spalte die gelieferte Länge der Zeile in Meter. |
| Stück | Wenn eine Stück-Umrechnung besteht, zeigt diese Spalte die gelieferte Stückzahl der Zeile. |

**Fakturierte Umrechnungsmengen (Anzeige):**

| Feld | Erläuterung |
|------|-------------|
| KG fakturiert | Wenn zu dieser Zeile bereits fakturiert wurde, steht hier das bereits fakturierte Gewicht in KG. Wenn Sie erneut fakturieren, verringert sich dadurch die noch offene Menge „KG nicht fakturiert“. |
| Meter fakturiert | Bereits fakturierte Länge in Meter; wirkt analog auf „Meter nicht fakturiert“. |
| Stück fakturiert | Bereits fakturierte Stückzahl; wirkt analog auf „Stück nicht fakturiert“. |

**Noch nicht fakturierte Umrechnungsmengen (Anzeige):**

| Feld | Erläuterung |
|------|-------------|
| KG nicht fakturiert | Ergibt sich aus „KG“ minus „KG fakturiert“. Wenn dieser Wert größer als 0 ist, steht noch Gewicht zur Fakturierung offen; er ist zugleich die Obergrenze für „zu fakturierende KG“. |
| Meter nicht fakturiert | Offene, noch nicht fakturierte Länge in Meter; Obergrenze für „Zu fakturierende Meter“. |
| Stück nicht fakturiert | Offene, noch nicht fakturierte Stückzahl; Obergrenze für „Zu fakturierende Stück“. |

**Verbrauchte Umrechnungsmengen (Anzeige):**

| Feld | Erläuterung |
|------|-------------|
| Verbrauchte KG | Wenn zur Charge des Artikels Verbrauchs- oder negative Regulierungsposten existieren, summiert dieses Feld deren Gewicht in KG. Der Wert wird von der offenen Menge abgezogen, sodass bereits verbrauchte Mengen nicht erneut zur Fakturierung vorgeschlagen werden. |
| Verbrauchte Meter | Summiert die verbrauchte bzw. negativ regulierte Länge in Meter (chargengenau) und mindert die vorgeschlagene zu fakturierende Menge entsprechend. |
| Verbrauchte Stück | Summiert die verbrauchte bzw. negativ regulierte Stückzahl (chargengenau) und mindert die vorgeschlagene zu fakturierende Menge entsprechend. |

**Zu fakturierende Umrechnungsmengen (erfassbar):**

| Feld | Erläuterung |
|------|-------------|
| zu fakturierende KG | Wenn Sie hier einen Wert eintragen, legen Sie fest, wie viel Gewicht mit der nächsten Fakturierung verrechnet wird; das Modul rechnet daraus automatisch „Menge zu fakturieren“ zurück. Der Wert darf „KG nicht fakturiert“ nicht überschreiten – andernfalls bricht Business Central mit der Meldung „Zu fakturierende KG darf nicht größer sein als KG nicht fakturiert“ ab. |
| Zu fakturierende Meter | Wenn Sie hier einen Wert eintragen, wird die Fakturierung längenbasiert gesteuert und „Menge zu fakturieren“ entsprechend zurückgerechnet. Der Wert darf „Meter nicht fakturiert“ nicht überschreiten (sonst Meldung „Zu fakturierende Meter darf nicht größer sein als Meter nicht fakturiert“). |
| Zu fakturierende Stück | Wenn Sie hier einen Wert eintragen, wird die Fakturierung stückbasiert gesteuert und „Menge zu fakturieren“ zurückgerechnet. Der Wert darf „Stück nicht fakturiert“ nicht überschreiten (sonst Meldung „Zu fakturierende Stück darf nicht größer sein als Stück nicht fakturiert“). |

**Zusammenspiel der erfassbaren Felder:** Sie steuern die Fakturierungsmenge wahlweise über die Basismenge **Menge zu fakturieren** oder über eine der drei Umrechnungsmengen. Sobald Sie eines dieser Felder ändern, gleicht das Modul die übrigen automatisch ab. So können Sie beispielsweise exakt 500 KG einer Coil fakturieren, ohne die entsprechende Basismenge selbst umrechnen zu müssen.

### Aktionen der Seite

Die für dieses Modul relevanten Aktionen der Liste **Einkaufslieferung fakturieren**:

| Aktion | Erläuterung |
|--------|-------------|
| Pflichtentnahme | Startet die Fakturierung der markierten Zeilen. Wenn zur Zeile bereits eine ungebuchte Einkaufsrechnung besteht, erscheint zuvor eine Bestätigungsabfrage. Die Aktion erzeugt bzw. ergänzt die Einkaufsrechnungszeile und überträgt dabei die Umrechnungsmengen KG, Meter und Stück in Rechnung, Reservierungsposten und – bei Chargenführung – in das Umlagerungsbuchblatt. |
| Kred.-Rechnungsnr. setzen | Öffnet einen Dialog, in dem Sie den markierten Zeilen die Kreditorenrechnungsnummer zuweisen. |
| Beleg anzeigen | Öffnet zur markierten Zeile die zugehörige gebuchte Einkaufslieferung. |
| Ungebuchte Einkaufsrechnungen anzeigen | Zeigt zur markierten Zeile die bereits vorhandene, noch nicht gebuchte Einkaufsrechnung. Die Aktion ist nur verfügbar, wenn eine passende ungebuchte Rechnungszeile existiert. |

### Automatische Mengenübernahme im Hintergrund

Beim Fakturieren übernimmt das Modul die Umrechnungsmengen ohne weiteres Zutun des Anwenders. Wenn die Zeile **keine** Charge trägt, werden KG, Meter und Stück direkt aus der Einkaufslieferzeile in die Einkaufsrechnungszeile geschrieben. Wenn die Zeile **chargengeführt** ist, summiert das Modul die fakturierten und verbrauchten Umrechnungsmengen chargengenau aus den Artikelposten und verteilt sie über die Reservierungsposten auf die Rechnungszeile. Zusätzlich werden bei der Umlagerungsbuchung dieselben KG-, Meter- und Stück-Werte in das Umlagerungsbuchblatt und die zugehörigen Reservierungsposten übernommen, damit Lagerbewegungen konsistent zur fakturierten Menge bleiben. Für den Anwender bedeutet das: Es genügt, die zu fakturierende Menge zu prüfen und **Pflichtentnahme** auszuführen – die Umrechnung erfolgt automatisch und posten-genau.

## FAQ und Troubleshooting

### 1. Warum stehen in den Spalten KG, Meter und Stück nur Nullen?

Weil für den Artikel keine Umrechnungsfaktoren im Modul **m+m Unit Conversion** hinterlegt sind. Ohne KG-je-Meter- bzw. KG-je-Stück-Faktoren kann Business Central die Basismenge nicht umrechnen; pflegen Sie die Faktoren, damit die Spalten gefüllt werden.

### 2. Warum wird eine Umrechnungsspalte für eine Zeile nicht berücksichtigt?

Die Umrechnungslogik läuft ausschließlich für Zeilen der **Art** „Artikel“. Bei anderen Zeilenarten (z. B. Sachkonto) bleiben KG, Meter und Stück wirkungslos, weil kein Artikel für die Umrechnung vorhanden ist.

### 3. Warum erhalte ich die Meldung „Zu fakturierende KG darf nicht größer sein als KG nicht fakturiert“?

Sie haben in **zu fakturierende KG** mehr eingetragen, als laut **KG nicht fakturiert** noch offen ist. Reduzieren Sie den Wert auf höchstens die offene Menge. Dieselbe Prüfung gilt sinngemäß für Meter und Stück.

### 4. Kann ich eine Lieferung teilweise fakturieren?

Ja. Tragen Sie in **Menge zu fakturieren** oder in eine der drei „zu fakturierenden“ Umrechnungsspalten weniger als die offene Menge ein. Das Modul erlaubt jede Teilmenge bis zur offenen Menge; ein vollständiger Ausgleich ist nicht erzwungen.

### 5. Warum ändert sich „Menge zu fakturieren“, wenn ich „Zu fakturierende Meter“ eingebe?

Weil beide Felder dieselbe Fakturierung beschreiben. Sobald Sie eine Umrechnungsmenge erfassen, rechnet das Modul über die Umrechnungsfaktoren die passende Basismenge zurück und aktualisiert **Menge zu fakturieren** automatisch – und umgekehrt.

### 6. Wonach richtet sich der verwendete Umrechnungsfaktor?

Das Modul nimmt bevorzugt den **tatsächlichen** Faktor der gebuchten Einkaufslieferzeile (KG je Meter bzw. KG je Stück). Ist dieser 0, greift der **theoretische** Faktor. Bei chargengeführten Zeilen werden die Faktoren stattdessen aus dem passenden Artikelposten der Charge gelesen.

### 7. Warum weichen die fakturierten Umrechnungsmengen bei Chargen von der einfachen Rechnung „KG minus KG fakturiert“ ab?

Bei chargengeführten Zeilen ermittelt das Modul die fakturierten Mengen posten-genau aus den Artikelposten der Charge (fakturierte KG/Meter/Stück) statt aus einem einfachen Differenzwert. So bleiben die Werte auch bei mehreren Teilfakturierungen und Chargen korrekt.

### 8. Was bedeuten die Spalten „Verbrauchte KG/Meter/Stück“?

Sie summieren – chargengenau – die bereits verbrauchten bzw. negativ regulierten Umrechnungsmengen aus den Artikelposten. Diese Mengen werden von der offenen Menge abgezogen, damit bereits verbrauchte Ware nicht erneut zur Fakturierung vorgeschlagen wird.

### 9. Warum sehe ich eine gebuchte Lieferung gar nicht in der Liste?

Die Seite blendet beim Öffnen automatisch alle Zeilen mit **Menge** gleich 0 aus. Ist eine Lieferzeile vollständig fakturiert oder trägt sie keine offene Menge, erscheint sie nicht mehr.

### 10. Muss ich die Umrechnungsmengen nach dem Fakturieren manuell in Rechnung und Lager nachtragen?

Nein. Beim Ausführen von **Pflichtentnahme** überträgt das Modul die Umrechnungsmengen automatisch in die Einkaufsrechnungszeile, die Reservierungsposten und – bei Chargenführung – in das Umlagerungsbuchblatt. Ein manuelles Nachtragen ist nicht erforderlich und nicht vorgesehen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Einkaufslieferung ohne Chargenführung fakturieren

**Auslöser:** Die Rechnung eines Lieferanten trifft per E-Mail ein. Sie bezieht sich auf eine bereits gebuchte Einkaufslieferung eines Artikels, der in KG geführt wird, aber keine Chargenpflicht hat.

**Einstieg in BC:** Öffnen Sie über **Suchen** die Seite **Einkaufslieferung fakturieren**. Die Liste zeigt die offenen Lieferzeilen.

**Kernablauf:**
1. Filtern bzw. suchen Sie die Zeile über **Kreditorennr.** und **Belegnr.**.
2. Prüfen Sie **KG nicht fakturiert**. Soll die volle offene Menge fakturiert werden, lassen Sie die zu fakturierenden Felder unverändert.
3. Führen Sie **Pflichtentnahme** aus und bestätigen Sie eine gegebenenfalls erscheinende Abfrage.
4. Das Modul schreibt die gelieferten KG (sowie Meter/Stück, falls vorhanden) direkt aus der Lieferzeile in die Einkaufsrechnungszeile und aktualisiert die Reservierungsposten.

**Abschluss:** Setzen Sie bei Bedarf über **Kred.-Rechnungsnr. setzen** die Kreditorenrechnungsnummer und prüfen Sie über **Ungebuchte Einkaufsrechnungen anzeigen**, dass die Rechnungszeile mit den korrekten KG-Werten angelegt wurde.

### Anwendungsfall 2: Teilfakturierung einer chargengeführten Coil in Meter

**Auslöser:** Von einer chargengeführten Coil (in KG und Meter geführt) soll aus abrechnungstechnischen Gründen zunächst nur ein Teil in Meter fakturiert werden; der Rest folgt später.

**Einstieg in BC:** Öffnen Sie über **Suchen** die Seite **Einkaufslieferung fakturieren** und wählen Sie die Zeile mit der betreffenden **Chargennr.**.

**Kernablauf:**
1. Prüfen Sie **Meter nicht fakturiert** und **Verbrauchte Meter**, um die tatsächlich noch fakturierbare Länge zu erkennen.
2. Tragen Sie in **Zu fakturierende Meter** die gewünschte Teilmenge ein (höchstens „Meter nicht fakturiert“). **Menge zu fakturieren** wird automatisch zurückgerechnet.
3. Führen Sie **Pflichtentnahme** aus und bestätigen Sie die Abfrage, falls bereits eine ungebuchte Rechnung existiert.
4. Das Modul ermittelt die fakturierten und verbrauchten Umrechnungsmengen chargengenau aus den Artikelposten, verteilt sie über die Reservierungsposten und überträgt die Werte zusätzlich in das Umlagerungsbuchblatt.

**Abschluss:** Die Zeile bleibt mit ihrer verbleibenden offenen Menge in der Liste sichtbar. Für die spätere Fakturierung des Rests wiederholen Sie den Ablauf; die bereits fakturierten Meter sind in **Meter fakturiert** berücksichtigt.
