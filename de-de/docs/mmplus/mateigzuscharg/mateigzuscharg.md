---
title: Anwenderhandbuch m+m Material Properties with Additional Lot Information
---

# Anwenderhandbuch m+m Material Properties with Additional Lot Information

## Einleitung

Die App **m+m Material Properties with Additional Lot Information** erweitert Microsoft Dynamics 365 Business Central um zusätzliche Chargeninformationen an den Stellen, an denen Anwender im Tagesgeschäft Chargen auswählen und Bestände beurteilen. Die App fügt **keine** eigenen Karten, Belege oder Berichte hinzu. Sie ergänzt bestehende Masken um Herkunfts- und Lieferantenangaben zur Charge und steuert zusätzlich die Reihenfolge der Chargenvorschläge in der erweiterten Suche.

Konkret bewirkt die App dreierlei:

1. Sie zeigt in den **Materialbeständen** und im **Chargensuchergebnis** zusätzliche Chargenfelder an: Lieferantencharge, interne Lieferantencharge, Zugangsdatum, eingekaufter Kreditor, Ursprungsland/Region, Hersteller und die Kennzeichnung als Bund.
2. Sie ergänzt die Maske **Einkaufsbestellchargen** um die Spalten Artikel-Matchcode und Chargen-Matchcode.
3. Sie fügt der Verteilungslogik der Materialeigenschaften-Einrichtung den Wert **FiFo** hinzu. Ist dieser Wert gesetzt, schlägt die erweiterte Chargensuche die Chargen nach Zugangsdatum aufsteigend vor (älteste Charge zuerst).

**Zielgruppe.** Primär richtet sich die App an **operative Anwender**, die im Verkauf und Einkauf an Belegzeilen Chargen zuweisen sowie an Lagerpersonal, das Bestände nach Charge beurteilt. Sekundär betrifft sie **Administratoren und Key-User**, die in der Materialeigenschaften-Einrichtung die erweiterte Matchcodesuche und die Verteilungslogik festlegen.

**Voraussetzungen.** Die App setzt die Basis-Apps **m+m Cloud Base**, **m+m Material Properties** und **m+m Additional Lot Information** voraus. Die Chargeninformationen selbst (Lieferantencharge, Hersteller, Ursprungsland, Zugangsdatum usw.) werden auf der **Chargennr.-Informationskarte** aus **m+m Additional Lot Information** gepflegt; diese App macht diese Werte an den genannten Masken sichtbar und nutzt sie für die Reihenfolge.

**Prozessüberblick.** Der Administrator aktiviert einmalig die erweiterte Matchcodesuche und setzt die Verteilungslogik. Danach sehen die Anwender die zusätzlichen Chargenspalten in den Materialbeständen, im Chargensuchergebnis und in den Einkaufsbestellchargen und erhalten bei aktivem FiFo die Chargenvorschläge in der gewünschten Reihenfolge.

## Schnellstart für Anwender

Die Einrichtung geht dem Tagesgeschäft voran. Führen Sie die Schritte in dieser Reihenfolge aus.

1. **Erw. Matchcodesuche verwenden** aktivieren. Öffnen Sie über **Suchen** die **Materialeigenschaften Einrichtung** und setzen Sie das Kontrollkästchen **Erw. Matchcodesuche verwenden**. Dieses Kennzeichen ist die Voraussetzung für die Verteilungslogik.
2. **Verteilungslogik** setzen. Wählen Sie im Feld **Verteilungslogik** den Wert **FiFo**, wenn die Chargensuche die älteste Charge zuerst vorschlagen soll; belassen Sie den Wert auf **Manuell**, wenn keine automatische Reihenfolge gewünscht ist.
3. **Bestände prüfen.** Öffnen Sie die **Materialbestände** und lesen Sie in den zusätzlichen Spalten Zugangsdatum, Lieferantencharge, Hersteller und Ursprungsland/Regionscode der jeweiligen Charge.
4. **Charge in der Belegzeile wählen.** Starten Sie aus einer Verkaufs- oder Einkaufszeile die erweiterte Suche. Im **Chargensuchergebnis** sind bei aktivem FiFo die Chargen nach Zugangsdatum aufsteigend sortiert; die zusätzlichen Spalten zeigen Herkunft und Lieferant zur Charge.
5. **Einkaufsbestellchargen** prüfen. In der Maske **Einkaufsbestellchargen** stehen zusätzlich die Spalten **Artikel-Matchcode** und **Chargen-Matchcode** zur Verfügung.

Es gibt in dieser App keinen Buchungs- oder Freigabeschritt; sie stellt ausschließlich zusätzliche Anzeigefelder und die Chargenreihenfolge bereit.

## Einrichtung

Die Einrichtung erfolgt zentral auf der Seite **Materialeigenschaften Einrichtung**. Diese Seite ist eine unternehmensweite Einrichtung (ein Datensatz pro Mandant) aus der Basis-App **m+m Material Properties**. Diese App fügt der Seite **kein** eigenes Feld hinzu; sie erweitert lediglich das Feld **Verteilungslogik** um den Wert **FiFo**. Dokumentiert werden hier die Felder, die die von dieser App gesteuerte Chargenreihenfolge freischalten und beeinflussen.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Materialeigenschaften Einrichtung** (unternehmensweite Einrichtung).

### FiFo-Chargenreihenfolge einrichten

**Wer und wann.** Diese Einrichtung nimmt der Administrator oder Key-User einmalig vor der ersten Nutzung vor. Die Einstellung wirkt anschließend in der täglichen Arbeit im **Chargensuchergebnis** (siehe Abschnitt **Anwendung im Tagesablauf → Chargensuchergebnis**).

**Ablauf in Abhängigkeitsreihenfolge.**

1. **Erw. Matchcodesuche verwenden** aktivieren. Wenn dieses Kennzeichen gesetzt ist, wird die erweiterte Matchcode- und Chargensuche insgesamt aktiviert und die abhängigen Felder (unter anderem **Verteilungslogik**) werden bearbeitbar. Ohne dieses Kennzeichen lässt sich die Verteilungslogik nicht ändern: Das System prüft bei jeder Änderung der Verteilungslogik, dass die erweiterte Matchcodesuche aktiv ist, und weist die Eingabe andernfalls zurück.
2. **Verteilungslogik** auf **FiFo** setzen. Wenn die Verteilungslogik auf **FiFo** gesetzt ist, sortiert die erweiterte Chargensuche die Trefferliste im **Chargensuchergebnis** automatisch nach dem **Zugangsdatum** aufsteigend, sodass die älteste Charge zuerst vorgeschlagen und zugewiesen wird. Bleibt der Wert auf **Manuell**, bestimmt der Anwender die Reihenfolge selbst und es erfolgt keine automatische Sortierung nach Zugangsdatum durch diese App.
3. **Operativer Abschluss.** Die Kette schließt sich in der Belegzeile: Sobald ein Anwender aus einer Verkaufs- oder Einkaufszeile die erweiterte Suche startet, greift die eingestellte Verteilungslogik und ordnet die Chargen im **Chargensuchergebnis** entsprechend an.

**Relevante Einrichtungsfelder**

| Einrichtung | Erläuterung |
|---|---|
| Erw. Matchcodesuche verwenden | Wenn aktiviert, wird die erweiterte Matchcode- und Chargensuche eingeschaltet und Folgeeinstellungen wie **Verteilungslogik**, **Chargensuche**, **Artikelsuche**, **In Bestellung** und **Alle anzeigen** werden bearbeitbar. Ist das Kennzeichen nicht gesetzt, sind diese Einstellungen gesperrt und die von dieser App gelieferte FiFo-Reihenfolge kommt nicht zum Tragen. |
| Verteilungslogik | Steuert die Reihenfolge, in der Chargen in der erweiterten Suche vorgeschlagen werden. **Manuell:** Es erfolgt keine automatische Sortierung durch diese App; der Anwender wählt die Charge frei. **FiFo:** Die Trefferliste wird nach Zugangsdatum aufsteigend sortiert; die zuerst zugegangene (älteste) Charge steht oben und wird zuerst zugewiesen. Die Änderung dieses Feldes setzt ein aktiviertes Kennzeichen **Erw. Matchcodesuche verwenden** voraus. |
| Chargensuche | Wenn aktiviert, bezieht die erweiterte Suche Chargen als Suchergebnis ein, sodass das **Chargensuchergebnis** überhaupt gefüllt wird. Ohne dieses Kennzeichen liefert die Suche keine Chargenzeilen und die FiFo-Reihenfolge dieser App ist gegenstandslos. |
| Artikelsuche | Wenn aktiviert, liefert die erweiterte Suche Artikel als Suchergebnis; in Kombination mit der Chargensuche entscheidet dies, welche Trefferart der Anwender in der Zeile erhält. |
| In Bestellung | Wenn aktiviert, bezieht die Suche zusätzlich noch nicht zugegangene, in Bestellung befindliche Chargen ein (ohne Zugangsdatum). Bei aktiver Verteilungslogik **FiFo** trennt diese App die in Bestellung befindlichen von den bereits zugegangenen Chargen anhand des Zugangsdatums, sodass die Sortierung eindeutig bleibt. |
| Alle anzeigen | Wenn aktiviert, zeigt die Suche alle Treffer ohne Einschränkung auf Artikel- oder Chargensuche; das Kennzeichen schließt sich mit der Chargensuche gegenseitig aus und ist daher nur relevant, wenn keine reine Chargensuche gewünscht ist. |

Weitere Felder der Seite **Materialeigenschaften Einrichtung** gehören zum Basisumfang der App **m+m Material Properties** und steuern nicht das Verhalten dieser Erweiterung; sie sind daher hier nicht Gegenstand.

### Berechtigungen

Die App liefert einen internen Berechtigungssatz mit, der ausschließlich die zur Chargenreihenfolge notwendige Verarbeitung freigibt. Er bestimmt die Berechtigungen für die interne Verarbeitung dieser Erweiterung und legt fest, welche technischen Aktionen im Hintergrund ausgeführt werden dürfen; ein eigenständiger, dem Anwender zugewiesener Funktionsumfang ist damit nicht verbunden. Die eigentlichen Chargen- und Bestandsberechtigungen ergeben sich aus den Basis-Apps und dem Standard von Business Central.

## Anwendung im Tagesablauf

Die App wirkt an drei bestehenden Masken. Alle Felder sind Anzeigefelder zur Charge; sie werden auf der **Chargennr.-Informationskarte** (aus **m+m Additional Lot Information**) gepflegt und hier sichtbar gemacht.

### Materialbestände

Die **Materialbestände** zeigen den Bestand je Charge. Diese App ergänzt die Liste um Herkunfts- und Lieferantenangaben zur jeweiligen Charge, sodass der Anwender die Charge ohne Wechsel auf die Chargennr.-Informationskarte beurteilen kann.

**Einstieg:** Öffnen Sie die **Materialbestände** aus der Artikel- bzw. Bestandsübersicht.

#### Zusätzliche Chargenspalten

| Feld | Erläuterung |
|---|---|
| Lieferanten-Chargennr. | Zeigt die vom Lieferanten vergebene Chargennummer. Wenn gefüllt, erkennt der Anwender im Bestand sofort, unter welcher Chargennummer der Lieferant die Ware geführt hat, ohne die Chargennr.-Informationskarte zu öffnen. |
| Lieferanteninterne Chargennr. | Zeigt die interne Chargenkennung des Lieferanten. Wenn gefüllt, lässt sich die Charge auch bei abweichender externer Nummerierung eindeutig dem Lieferantenlos zuordnen. |
| Zugangsdatum | Zeigt das Datum des Chargenzugangs. Wenn gefüllt, kann der Anwender das Alter der Charge beurteilen; dieses Datum ist zugleich das Sortierkriterium der FiFo-Reihenfolge in der erweiterten Suche. |
| Eingekauft von Kreditor (Nr.) | Zeigt die Kreditorennummer, von der die Charge eingekauft wurde. Wenn gefüllt, ist die Bezugsquelle der Charge direkt im Bestand ersichtlich. |
| Eingekauft von Kreditor (Name) | Zeigt den Namen des einkaufenden Kreditors zur Chargenherkunft. Der Wert wird aus dem Kreditor ermittelt und dient der schnellen Klartextzuordnung ohne Nummernauflösung. |
| Ursprungsland/-regionscode | Zeigt das Ursprungsland bzw. die Ursprungsregion der Charge. Wenn gefüllt, kann der Anwender Herkunftsanforderungen bereits im Bestand prüfen. |
| Herstellercode | Zeigt den Hersteller der Charge als Code. Wenn gefüllt, ist der Hersteller der Charge unmittelbar erkennbar. |
| Herstellername | Zeigt den Herstellernamen im Klartext. Diese Spalte ist standardmäßig ausgeblendet und kann bei Bedarf über die Personalisierung eingeblendet werden; sie ergänzt den Herstellercode um die lesbare Bezeichnung. |
| Bund | Kennzeichnet die Charge als Bund. Wenn gesetzt, weiß der Anwender, dass es sich um eine gebündelte Wareneinheit handelt, was bei Entnahme und Kommissionierung zu berücksichtigen ist. |

#### Filter

Die **Materialbestände** lassen sich nach Lagerort einschränken. Der Filter gehört zur Basisseite und bleibt auch mit den zusätzlichen Chargenspalten wirksam.

| Filterfeld | Erläuterung |
|---|---|
| Lagerortcode | Wenn gesetzt, werden die Bestandszeilen nach dem angegebenen Lagerort gefiltert, sodass nur Chargen dieses Lagerorts mit ihren Herkunftsangaben angezeigt werden. |

### Chargensuchergebnis

Das **Chargensuchergebnis** ist die Trefferliste der erweiterten Chargensuche. Es wird nicht über **Suchen** geöffnet, sondern erscheint, wenn der Anwender aus einer Verkaufs- oder Einkaufszeile die erweiterte Suche startet. Diese App ergänzt die Trefferliste um dieselben Herkunftsspalten wie in den Materialbeständen und steuert – abhängig von der Verteilungslogik – die Reihenfolge der Treffer.

**Einstieg:** Starten Sie aus der Belegzeile die erweiterte Matchcode-/Chargensuche; das **Chargensuchergebnis** öffnet sich mit den gefundenen Chargen.

**Reihenfolge.** Ist die **Verteilungslogik** auf **FiFo** gesetzt, sortiert die App die Treffer beim Öffnen der Seite, beim Aufbau der Datensätze und vor der Mengenzuweisung nach dem **Zugangsdatum** aufsteigend, sodass die älteste Charge oben steht. Ist die Verteilungslogik auf **Manuell**, bleibt die Standardreihenfolge erhalten.

#### Zusätzliche Chargenspalten

| Feld | Erläuterung |
|---|---|
| Zugangsdatum | Zeigt das Zugangsdatum der Charge. Wenn gefüllt, erkennt der Anwender das Chargenalter unmittelbar in der Trefferliste; bei aktivem FiFo bestimmt dieses Datum die Sortierung. |
| Lieferantencharge | Zeigt die Lieferantenchargennummer zur Trefferzeile. Wenn gefüllt, lässt sich der Vorschlag der Suche einer Lieferantencharge zuordnen. |
| Interne Lieferantencharge | Zeigt die interne Chargenkennung des Lieferanten zur Trefferzeile. Wenn gefüllt, ist die Charge auch bei abweichender externer Nummer eindeutig. |
| Herstellercode | Zeigt den Hersteller der Charge als Code, damit die Herkunft schon bei der Auswahl berücksichtigt werden kann. |
| Herstellername | Zeigt den Herstellernamen im Klartext zur Trefferzeile. |
| Ursprungsland/Regionscode | Zeigt das Ursprungsland/die Region der vorgeschlagenen Charge, sodass Herkunftsanforderungen vor der Zuweisung geprüft werden können. |
| Bund | Kennzeichnet die vorgeschlagene Charge als Bund; wenn gesetzt, ist die Verpackungseinheit bei der Auswahl zu beachten. |
| Eingekauft von Kreditor Nr. | Zeigt die Kreditorennummer der Bezugsquelle zur Trefferzeile. |
| Eingekauft von Kreditor Name | Zeigt den Namen des einkaufenden Kreditors im Klartext zur Trefferzeile. |

Neben diesen zusätzlichen Spalten enthält das Chargensuchergebnis die Standardfelder der Basissuche, unter anderem **Artikelnr.**, **Chargennr.**, **Verfügbare Menge** und die Belegangaben **Bestellungsnr.** und **Bestellzeilennr.** Die zusätzlichen Herkunftsspalten dieser App sind schreibgeschützt.

### Einkaufsbestellchargen

Die Maske **Einkaufsbestellchargen** stellt die Chargen einer Einkaufsbestellung dar. Diese App ergänzt sie um zwei Matchcode-Spalten, damit Artikel und Charge anhand ihres Matchcodes zugeordnet werden können.

**Einstieg:** Öffnen Sie die **Einkaufsbestellchargen** aus dem Chargen- bzw. Artikelverfolgungskontext der Einkaufsbestellung.

#### Zusätzliche Spalten

| Feld | Erläuterung |
|---|---|
| Artikel-Matchcode | Zeigt den Matchcode des Artikels zur Chargenzeile. Wenn gefüllt, kann der Anwender die Zeile anhand des Artikel-Matchcodes zuordnen, ohne die vollständige Artikelnummer zu vergleichen. Der Wert wird aus dem Artikel ermittelt und ist schreibgeschützt. |
| Chargen-Matchcode | Zeigt den Matchcode der Charge zur Zeile. Wenn gefüllt, lässt sich die Charge über ihren Matchcode identifizieren; der Wert wird aus der Chargennr.-Information ermittelt und ist schreibgeschützt. |

Die übrigen Spalten der Maske – unter anderem **Einkaufsbestellnr.**, **Artikelnr.**, Artikelbeschreibung, **Chargennr.**, Lieferantencharge und **Menge** sowie die Kennzeichnung der ausgewählten Zeile – gehören zur Basismaske aus **m+m Additional Lot Information**.

## FAQ und Troubleshooting

### 1. Warum lässt sich die Verteilungslogik nicht ändern?
Die Änderung der **Verteilungslogik** setzt das aktivierte Kennzeichen **Erw. Matchcodesuche verwenden** voraus. Solange dieses Kennzeichen nicht gesetzt ist, weist das System die Eingabe im Feld Verteilungslogik zurück. Aktivieren Sie zuerst die erweiterte Matchcodesuche.

### 2. Was bewirkt der Wert FiFo in der Verteilungslogik?
Ist **FiFo** gesetzt, sortiert die erweiterte Chargensuche die Trefferliste im **Chargensuchergebnis** nach dem **Zugangsdatum** aufsteigend. Die zuerst zugegangene (älteste) Charge steht oben und wird zuerst vorgeschlagen. Bei **Manuell** entfällt diese automatische Sortierung.

### 3. Warum werden die Chargen trotz FiFo nicht sortiert?
Die Sortierung greift nur, wenn die Verteilungslogik tatsächlich auf **FiFo** steht und die erweiterte Chargensuche aktiv ist (**Erw. Matchcodesuche verwenden** und **Chargensuche**). Steht die Verteilungslogik auf **Manuell**, bleibt die Standardreihenfolge erhalten.

### 4. Warum sehe ich die Spalte Herstellername in den Materialbeständen nicht?
Die Spalte **Herstellername** ist in den Materialbeständen standardmäßig ausgeblendet. Blenden Sie sie bei Bedarf über die Personalisierung der Seite ein. Der zugehörige **Herstellercode** ist standardmäßig sichtbar.

### 5. Woher stammen die zusätzlichen Chargenangaben?
Alle Herkunfts- und Lieferantenangaben (Lieferantencharge, interne Lieferantencharge, Zugangsdatum, eingekaufter Kreditor, Ursprungsland/Region, Hersteller, Bund) werden auf der **Chargennr.-Informationskarte** aus **m+m Additional Lot Information** gepflegt. Diese App zeigt sie an den genannten Masken an, ändert sie aber nicht.

### 6. Kann ich die zusätzlichen Chargenspalten bearbeiten?
Nein. Die durch diese App ergänzten Herkunftsspalten in den **Materialbeständen** und im **Chargensuchergebnis** sowie die Matchcode-Spalten in den **Einkaufsbestellchargen** sind schreibgeschützt. Änderungen nehmen Sie auf der Chargennr.-Informationskarte vor.

### 7. Was bedeutet die Kennzeichnung Bund?
**Bund** kennzeichnet die Charge als gebündelte Wareneinheit. Wenn das Kennzeichen gesetzt ist, ist die Charge als Bund geführt; berücksichtigen Sie dies bei Entnahme und Kommissionierung.

### 8. Wozu dienen Artikel-Matchcode und Chargen-Matchcode in den Einkaufsbestellchargen?
Beide Spalten erleichtern die Zuordnung: Der **Artikel-Matchcode** stammt aus dem Artikel, der **Chargen-Matchcode** aus der Chargennr.-Information. Über den Matchcode lassen sich Artikel und Charge schneller identifizieren als über die vollständigen Nummern. Beide Werte sind schreibgeschützt.

### 9. Warum unterscheiden sich die deutschen Feldbezeichnungen zwischen den Masken?
Dieselbe Chargenangabe kann je nach zugrunde liegender Maske eine leicht abweichende Bezeichnung tragen: Im **Chargensuchergebnis** heißt die Lieferantencharge **Lieferantencharge**, in der Materialsuche der **Materialbestände** **Lieferanten-Chargennr.** Inhaltlich handelt es sich um dieselbe Herkunftsangabe zur Charge.

### 10. Muss ich für in Bestellung befindliche Chargen etwas beachten?
Wenn die Einstellung **In Bestellung** aktiv ist, bezieht die Suche auch noch nicht zugegangene Chargen ohne Zugangsdatum ein. Bei aktivem **FiFo** trennt die App diese von den bereits zugegangenen Chargen anhand des Zugangsdatums, damit die Reihenfolge eindeutig bleibt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Älteste Charge in der Verkaufszeile zuweisen

1. **Auslöser.** Ein Kunde bestellt telefonisch Ware, für die nach dem Prinzip „älteste Charge zuerst“ ausgeliefert werden soll.
2. **Einstieg in BC.** Der Anwender öffnet den Verkaufsauftrag, erfasst die Zeile mit Artikel und Menge und startet aus der Zeile die erweiterte Matchcode-/Chargensuche.
3. **Kernablauf.** Das **Chargensuchergebnis** öffnet sich. Da die **Verteilungslogik** auf **FiFo** steht, sind die Chargen nach **Zugangsdatum** aufsteigend sortiert; die älteste Charge steht oben. Der Anwender prüft zusätzlich **Lieferantencharge**, **Herstellercode** und **Ursprungsland/Regionscode** direkt in der Trefferliste und weist die Menge der obersten Charge zu.
4. **Abschluss.** Die zugewiesene Charge übernimmt Business Central in die Artikelverfolgung der Zeile. Ein eigener Buchungsschritt dieser App entsteht nicht; der weitere Belegablauf folgt dem Standard.

### Anwendungsfall 2: Chargen einer Einkaufsbestellung über Matchcode zuordnen

1. **Auslöser.** Beim Wareneingang liegen mehrere Chargen zu einer Einkaufsbestellung vor, die anhand ihres Matchcodes abgeglichen werden sollen.
2. **Einstieg in BC.** Der Anwender öffnet aus dem Chargen- bzw. Artikelverfolgungskontext der Einkaufsbestellung die Maske **Einkaufsbestellchargen**.
3. **Kernablauf.** In der Liste stehen je Chargenzeile die Standardangaben (**Einkaufsbestellnr.**, **Artikelnr.**, **Chargennr.**, **Menge**) sowie die durch diese App ergänzten Spalten **Artikel-Matchcode** und **Chargen-Matchcode**. Über den Chargen-Matchcode ordnet der Anwender die eingegangene Charge der richtigen Bestellzeile zu.
4. **Abschluss.** Die Zuordnung erfolgt im Rahmen der Standard-Artikelverfolgung. Diese App liefert dazu die zusätzlichen Matchcode-Spalten; einen eigenen Buchungs- oder Abschlussschritt gibt es nicht.
