---
title: Anwenderhandbuch m+m Component Planning
---

# Anwenderhandbuch m+m Component Planning

## Einleitung

Die **Vormaterial Orientierte Planung (VOP)** unterstützt die vormaterialgetriebene Fertigungsplanung im Stahl- und Coilumfeld in Microsoft Dynamics 365 Business Central. Ausgangspunkt ist eine vorhandene Vormaterialcharge (z. B. ein Coil oder ein Block), die auf einen oder mehrere Aufträge (Verkaufsauftrag, Fertigungsauftrag) aufgeteilt (eingeteilt) werden soll. Aus diesen Zuordnungen erzeugt das Modul die passenden Fertigungsaufträge samt FA-Komponentenzeilen, Artikelverfolgung und Trenninformationen.

**Primäre Zielgruppe** sind operative Anwender in der Fertigungsplanung, die täglich Vormaterial suchen, Aufträge zuordnen, Trenneinheiten erfassen und Fertigungsaufträge erstellen. **Sekundäre Zielgruppe** sind Administratoren und Schlüsselanwender, die die **VOP Einrichtung** sowie die Stammdaten (Materialart, Arbeitsplatzgruppe, Trennvorgabewerte) pflegen.

Das Modul erweitert Stammdaten und Belege des Basismoduls. Auf der **Materialart** (Verwaltung durch den Administrator) wird die maßgebende **Trenndimension** festgelegt; auf der **Arbeitsplatzgruppe** wird die **Trennarbeitsplatzgruppe** gekennzeichnet. In den **Fertigungsauftragszeilen** und im **Verkaufsauftrag** wird die Planung über die Aktion **Vormaterial Orientierte Planung** gestartet. Der zentrale Arbeitsplatz ist die Seite **Vormaterial Orientierte Planung**, in der Vormaterial, Aufträge und Zuordnungen gemeinsam bearbeitet werden.

Der typische Ablauf: **Vormaterial suchen** → **Auftragssuche** → Zeilen markieren → **Zuordnen** → **Trenneinheiten** erfassen → **Fehler vorhanden** prüfen → **Fertigungsaufträge erstellen** → **Protokoll anzeigen**.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg von der Vormaterialcharge zum fertigen Fertigungsauftrag. Voraussetzung ist eine abgeschlossene **VOP Einrichtung** sowie gepflegte Stammdaten (siehe **Einrichtung** und **Stammdaten**).

**Voraussetzung (einmalig, durch den Administrator):**

1. **VOP Einrichtung** öffnen (über **Suchen**, Begriff *VOP Einrichtung*) und mindestens **FA-Anlagestatus**, **FA-Erstellungsmethode** sowie eine Option der **Auftragssuche** setzen. Details siehe **Einrichtung**.
2. Auf der **Materialartenkarte** des Vormaterials die **Trenndimension** setzen und die passenden **Eigenschaften** mit der Verwendung Breite/Länge/Dicke pflegen (siehe **Stammdaten**).
3. In den Arbeitsplänen der zu fertigenden Artikel mindestens eine **Trennarbeitsplatzgruppe** hinterlegen (siehe **Stammdaten**).

**Täglicher Ablauf:**

1. Seite **Vormaterial Orientierte Planung** öffnen — entweder über **Suchen** (Begriff *VOP*) oder aus einer Fertigungsauftragszeile bzw. einem freigegebenen Verkaufsauftrag über die Aktion **Vormaterial Orientierte Planung**.
2. Im oberen Bereich das Vormaterial suchen: Feld **Artikelnr.** oder **Matchcode** füllen, oder Aktion **Vormaterialsuche** verwenden. Optional zuvor die **Ansichtsart** wählen.
3. Im Bereich **Vormaterialsuchergebnisse** eine oder mehrere Vormaterialchargen auswählen.
4. Aktion **Auftragssuche** (Bereich **Vormaterial**) ausführen und im Bereich **Auftragssuchergebnisse** die passenden Auftragszeilen über **Markieren** kennzeichnen.
5. Aktion **Zuordnen** (Bereich **Aufträge**) ausführen. Je Kombination aus Vormaterial und Auftrag entsteht im Bereich **Zuordnungen** eine Zeile.
6. In der Zuordnungszeile **Zugew. Trenneinheiten** erfassen. **Zugew. Menge** und **Fert. Menge** werden automatisch berechnet; bei Bedarf **Zugew. Segment** und **Trenneinheitenfaktor** anpassen.
7. Einteilung in der Infobox **Trennüberwachung** grafisch prüfen und über die Spalte **Fehler vorhanden** kontrollieren, ob alle Pflichtangaben gesetzt sind.
8. Fehlerfreie Zuordnungszeilen über **Markieren** kennzeichnen und über **Fertigungsaufträge erstellen** (Bereich **Zuordnungen**) die Fertigungsaufträge anlegen.
9. In der Rückfrage **Protokoll anzeigen?** bestätigen, um die **Protokolleinträge** mit den erstellten Fertigungsaufträgen zu sehen.

## Einrichtung

Die Einrichtung ist Voraussetzung für die tägliche Arbeit. Sie umfasst die zentrale **VOP Einrichtung** sowie die Stammdaten in **Materialart** und **Arbeitsplatzgruppe** (siehe **Stammdaten**). Die Reihenfolge folgt der technischen Abhängigkeit: zuerst die globale **VOP Einrichtung**, danach die materialart- und arbeitsplatzgruppenbezogene Konfiguration.

### VOP Einrichtung

**Einstieg:** Über **Suchen** den Begriff *VOP Einrichtung* (bzw. *Vormaterial Orientierte Planung Einrichtung*) eingeben und die Seite **VOP Einrichtung** öffnen. Diese Seite ist eine unternehmensweite Einzeleinrichtung (ein Datensatz je Mandant) und wird beim ersten Öffnen automatisch angelegt.

**Prozess:** Der Administrator legt hier einmalig fest, **wie** Fertigungsaufträge aus den Zuordnungszeilen entstehen, welchen Status neue Fertigungsaufträge erhalten, ob Restmengen und Schrott automatisch verarbeitet werden und welche Auftragsarten die **Auftragssuche** liefert. Alle Werte wirken direkt im täglichen Ablauf auf der Seite **Vormaterial Orientierte Planung** (siehe **Tägliche Arbeit** und **Fertigungsaufträge erstellen**).

Register **Allgemein**:

| Einrichtung | Erläuterung |
|-------------|-------------|
| **FA-Erstellungsmethode** | Bestimmt, wie die Zuordnungszeilen bei **Fertigungsaufträge erstellen** zusammengefasst werden. Wirkt unmittelbar auf Anzahl und Aufbau der erzeugten Fertigungsaufträge. Werte: **Je Zuordnung:** Für jede Zuordnungszeile entsteht ein eigener Fertigungsauftrag mit einer FA-Zeile. **Je Vormaterial:** Zuordnungszeilen mit gleicher Vormaterialcharge werden in einem Fertigungsauftrag als je eigene FA-Zeile zusammengefasst. **Je Verkaufsauftragszeile:** Zuordnungszeilen mit gleicher Auftragszeile werden in einem Fertigungsauftrag zusammengefasst. **Abfrage der Methode:** Bei jeder FA-Erstellung wird die Methode zur Laufzeit abgefragt, sodass situativ entschieden werden kann. |
| **Erw. FA-Erstellung je Vormaterial** | Wenn aktiviert, versucht das System bei der Methode **Je Vormaterial**, die Zuordnungszeilen auch bestehenden, noch nicht beendeten Fertigungsaufträgen mit gleicher Vormaterialcharge zuzuordnen; damit existiert je Vormaterialcharge nur ein aktiver Fertigungsauftrag. Das Kennzeichen lässt sich nur setzen, wenn als **FA-Erstellungsmethode** *Je Vormaterial* gewählt ist; andernfalls wird die Einstellung automatisch auf *Je Vormaterial* umgesetzt bzw. abgewiesen. |
| **FA-Anlagestatus** | Legt fest, welchen Status (z. B. **Simuliert**, **Geplant**, **Fest geplant**, **Freigegeben**) die bei **Fertigungsaufträge erstellen** neu angelegten Fertigungsaufträge erhalten. Wenn ein bereits vorhandener Fertigungsauftrag einen niedrigeren Status hat als hier gewählt, wird er beim Zuordnen auf den hier festgelegten Status hochgesetzt. Das Feld ist Pflicht; ohne Wert bricht die FA-Erstellung mit einer Meldung ab. |
| **Restmengeneinschränkung** | Wenn aktiviert, prüft das System bei der Restmengenverteilung, dass am Vormaterial keine zu große Restmenge verbleibt, die auf die FA-Zeilen verteilt werden soll; der zulässige Prozentsatz wird an der Einsatzmaterialart gepflegt. Ohne Kennzeichen erfolgt keine Restmengenprüfung. |
| **FA-Zeilenartikelverfolgung für Chargeneinteilung erstellen** | Wenn aktiviert, werden bei der FA-Erstellung für die Trenneinheiten (Chargeneinteilungen) bereits Chargennummern vergeben und in die Artikelverfolgung der FA-Zeile eingetragen; ohne Kennzeichen erfolgt keine automatische Chargenvergabe für die Trenneinheiten. |
| **Chargen in Erw. Rückmeldung für Trenneinheiten hinzufügen** | Wenn aktiviert, wird in der erweiterten Rückmeldung im Bereich Chargen je Trenneinheit eine eigene Zeile erzeugt. Ohne Kennzeichen bleibt die erweiterte Rückmeldung ohne trenneinheitenbezogene Chargenzeilen. Die Einstellung ist nur bei Einsatz der erweiterten Rückmeldung wirksam. |
| **FA-Schrott durch Saumschrott & Trennverlust** | Wenn aktiviert, erzeugt das System bei der FA-Erstellung automatisch FA-Schrottposten aus **Saumschrott** und **Trennverlust** (auf Basis der Einteilungen und der Trennvorgabewerte). Das Kennzeichen lässt sich nur setzen, wenn **Erw. FA-Erstellung je Vormaterial** aktiv ist; andernfalls wird die Eingabe abgewiesen. Ohne Kennzeichen entsteht kein automatischer Trennschrott. Siehe **Lager, Schrott und Folgebelege**. |

Register **Auftragssuche**:

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Auftragssuche inkl. Fertigungsaufträge** | Wenn aktiviert, liefert die **Auftragssuche** auch offene Fertigungsauftragszeilen als Bedarf. Ist weder diese noch **Auftragssuche inkl. Verkaufsaufträge** gesetzt, bricht die Einrichtung mit dem Hinweis ab, dass mindestens eine Option der Auftragssuche aktiviert sein muss. |
| **Auftragssuche inkl. Verkaufsaufträge** | Wenn aktiviert, liefert die **Auftragssuche** auch offene Verkaufsauftragszeilen als Bedarf. Zusammen mit der vorstehenden Option steuert dieses Kennzeichen, welche Belegarten im Bereich **Auftragssuchergebnisse** erscheinen. |

**Validierung/Abhängigkeit:** Die beiden Kennzeichen der Auftragssuche sind miteinander verknüpft — mindestens eines muss gesetzt sein. **FA-Schrott durch Saumschrott & Trennverlust** setzt **Erw. FA-Erstellung je Vormaterial** voraus, und dieses wiederum die **FA-Erstellungsmethode** *Je Vormaterial*.

### Automatische FA-Schrotterzeugung einrichten

**Prozessvorstellung:** Diese Fähigkeit sorgt dafür, dass bei der FA-Erstellung der beim Trennen anfallende **Saumschrott** (jeweils erste und letzte Einteilung auf dem Vormaterial) und der **Trennverlust** (zwischen den Einteilungen) automatisch als FA-Schrottposten gebucht werden. Konfiguriert wird sie durch den Administrator vor der ersten Nutzung; angewendet wird sie im Tagesablauf über **Fertigungsaufträge erstellen** (siehe **Fertigungsaufträge erstellen**).

**Einrichtungsschritte in Abhängigkeitsreihenfolge:**

1. **Zuerst** auf der **Arbeitsplatzgruppenkarte** die relevanten Arbeitsplatzgruppen als **Trennarbeitsplatzgruppe** kennzeichnen und über die Aktion **Trennvorgabewerte** je Materialart den **Trennverlust** hinterlegen (Vorgabeart **Trennverlust**). Wenn gesetzt, fällt der hinterlegte Wert zwischen jeder Einteilung an und verringert den einteilbaren Wert (siehe **Stammdaten**).
2. **Danach** auf der **Materialartenkarte** über die Aktion **Trennvorgabewerte** je Arbeitsplatzgruppe den **Saumschrott** hinterlegen (Vorgabeart **Saumschrott**). Wenn gesetzt, wird der Wert als erste und letzte Einteilung platziert.
3. **Danach** in der **VOP Einrichtung** die **FA-Erstellungsmethode** auf *Je Vormaterial* stellen und **Erw. FA-Erstellung je Vormaterial** aktivieren.
4. **Schließlich** in der **VOP Einrichtung** das Kennzeichen **FA-Schrott durch Saumschrott & Trennverlust** aktivieren. Wenn aktiviert, erzeugt die FA-Erstellung für jede beendete Zuordnung mit Vormaterialcharge FA-Schrottposten für **Saumschrott** und **Trennschrott** anteilig zum Einteilungswert.

**Operativer Abschluss:** Der Anwender löst die Schrotterzeugung im Tagesablauf über **Fertigungsaufträge erstellen** aus; die erzeugten Posten sind im **FA-Schrott** und in den **FA-Schrottposten** sichtbar (Kennzeichen **Von VOP**).

## Stammdaten

Die Stammdaten steuern, wie Vormaterial und zu fertigende Artikel in der Planung behandelt werden. Die Pflege erfolgt durch Administratoren bzw. Schlüsselanwender vor der ersten Nutzung und bei Bedarf laufend.

### Materialartenkarte — Trenndimension und primäre Eigenschaften

**Einstieg:** Aus der Materialartenliste die gewünschte Materialart öffnen (**Materialartenkarte**). Die Materialartenkarte gehört zum Basismodul; die VOP ergänzt Felder im Register **Allgemein** und eine Gruppe **Primäre Eigenschaften**.

**Prozessvorstellung:** Der Administrator legt hier fest, welche Dimension eines Vormaterials verteilt wird und welche Eigenschaften die Vormaterial- und Fertigmaterialsuche steuern. Die **Trenndimension** ist die zentrale Steuergröße für die Einteilung; sie bestimmt, welches Maß (Breite, Länge, Dicke) in der Zuordnungszeile als **Zugew.**-Wert erfasst und in der Infobox **Trennüberwachung** überwacht wird.

| Feld | Erläuterung |
|------|-------------|
| **Trenndimension** | Legt fest, welche Dimension bei diesem (Vormaterial-)Materialtyp eingeteilt und verteilt wird. Werte: **(leer):** Keine Trenndimension festgelegt — die Einteilung ist nicht möglich, solange kein Maß gesetzt ist. **Breite:** Das Vormaterial wird nach Breite eingeteilt (z. B. Längsteilung von Coils in Spaltbänder). **Länge:** Das Vormaterial wird nach Länge eingeteilt. **Dicke:** Das Vormaterial wird nach Dicke/Höhe eingeteilt (z. B. Blöcke). Wenn ein Wert gesetzt ist, erscheint in der Zuordnung das zugehörige **Zugew.**-Maß, und die passende Eigenschaftsverwendung muss gepflegt sein. |
| **Trennzuschlag Zwischenlagerfertigung** | Wenn ein Wert > 0 gesetzt ist, wird bei der Zuordnung automatisch zunächst eine **Zwischenlagerfertigung** mit dem um diesen Wert erhöhten Maß der Trenndimension gebildet; über eine Artikelsuche wird der passende Zwischenartikel ermittelt oder automatisch angelegt, und die FA-Erstellung bildet eine mehrstufige FA-Kette. Der Wert wird in jede darauf basierende Zuordnungszeile übernommen und kann dort überschrieben werden (was zu einer erneuten Artikelsuche führt). Bei Wert 0 entsteht keine Zwischenstufe. |
| **Primäre Eigenschaft 1 … 10** | Wenn eine primäre Eigenschaft gesetzt ist, wird ihr Wert als Spalte im Vormaterialsuchergebnis der Seite **Vormaterial Orientierte Planung** eingeblendet (je nach Datentyp als Text- oder Dezimalspalte). Damit legt der Administrator fest, welche Merkmale der Anwender beim Suchen und Einteilen unmittelbar sieht. Ohne gesetzte Eigenschaft bleibt die zugehörige Spalte ausgeblendet. Es können bis zu zehn primäre Eigenschaften definiert werden. |

**Abhängigkeit:** Für die gewählte **Trenndimension** muss in den Eigenschaften der Materialart mindestens eine Eigenschaft mit gleichlautender **Verwendung** (Breite/Länge/Dicke) gepflegt sein. Ohne passende Verwendung findet die Restmengen- und Zwischenartikelsuche keine Eigenschaft und meldet, dass keine Eigenschaft für die Trenndimension in der Materialart definiert ist. Angewendet werden diese Stammdaten im täglichen Ablauf (siehe **Tägliche Arbeit**).

### Arbeitsplatzgruppenkarte — Trennarbeitsplatzgruppe

**Einstieg:** Aus der Arbeitsplatzgruppenliste die gewünschte Arbeitsplatzgruppe öffnen (**Arbeitsplatzgruppenkarte**). Die Karte gehört zum Basismodul; die VOP ergänzt im Register **Allgemein** ein Kennzeichen.

**Prozessvorstellung:** Der Administrator kennzeichnet hier, welche Arbeitsplatzgruppen für den Trennvorgang zuständig sind. Jeder Arbeitsplan, der in einer VOP-Zuordnung verwendet werden soll, muss mindestens eine **Trennarbeitsplatzgruppe** enthalten; aus der ersten gefundenen Trennarbeitsplatzgruppe werden die Trenneinrichtungen übernommen.

| Feld | Erläuterung |
|------|-------------|
| **Trennarbeitsplatzgruppe** | Wenn aktiviert, gilt diese Arbeitsplatzgruppe als Trennarbeitsplatzgruppe; ihre Trennvorgabewerte werden in der Zuordnung herangezogen, und der Arbeitsplan des Fertigartikels ist für die VOP verwendbar. Ohne Kennzeichen wird die Arbeitsplatzgruppe bei der Trennplanung nicht berücksichtigt. |

**Prozessschritte:** Zuerst die Arbeitsplatzgruppe als **Trennarbeitsplatzgruppe** kennzeichnen, danach über die Aktion **Trennvorgabewerte** den **Trennverlust** je Materialart hinterlegen (siehe unten). Angewendet wird die Trennarbeitsplatzgruppe in der Zuordnungszeile über das Feld **Trennarbeitsplatzgruppennr.** und den **Arbeitsplan** (siehe **Felder der Zuordnungszeile**).

### Trennvorgabewerte pflegen

**Einstieg:** Auf der **Arbeitsplatzgruppenkarte** bzw. der **Materialartenkarte** die Aktion **Trennvorgabewerte** wählen. Die Liste **Trennvorgabewerte** ist nicht über **Suchen** erreichbar; sie wird ausschließlich über diese Aktionen geöffnet (kontextabhängig gefiltert).

**Prozessvorstellung:** Der Administrator hinterlegt hier die Verlust- und Saumwerte, die der einteilbare Wert eines Vormaterials verliert. Von der **Arbeitsplatzgruppe** aus wird der **Trennverlust** je Materialart gepflegt (fällt zwischen jeder Einteilung an); von der **Materialart** aus wird der **Saumschrott** je Arbeitsplatzgruppe gepflegt (wird als erste und letzte Einteilung platziert).

| Feld | Erläuterung |
|------|-------------|
| **Materialartencode** | Bezeichnet die Materialart, für die der Vorgabewert gilt. Beim Öffnen von der Materialartenkarte ist die Spalte in der Regel ausgeblendet und vorbelegt; beim Öffnen von der Arbeitsplatzgruppe wird sie eingeblendet, um den Wert je Materialart zu pflegen. |
| **Arbeitsplatzgruppennr.** | Bezeichnet die Arbeitsplatzgruppe, für die der Vorgabewert gilt. Beim Öffnen von der Arbeitsplatzgruppenkarte ist die Spalte in der Regel ausgeblendet und vorbelegt; beim Öffnen von der Materialart wird sie eingeblendet, um den Saumschrott je Arbeitsplatzgruppe zu pflegen. |
| **Vorgabeart** | Bestimmt, welche Art von Trennwert der Datensatz beschreibt. Werte: **Saumschrott:** Der Wert wird als erste und letzte Einteilung auf dem Vormaterial platziert und verringert den einteilbaren Wert. **Trennverlust:** Der Wert fällt zwischen jeder Einteilung (Trennung) an. |
| **Wert** | Enthält den Betrag des Trennwerts in der Einheit der Trenndimension. Wenn gesetzt, reduziert dieser Wert bei der Einteilung den verfügbaren Trenndimensionswert entsprechend der **Vorgabeart**. |

### Artikel-Schrottart

**Einstieg:** Aus der Liste **Artikel Schrotte** (Basismodul m+m Steel Base) die Schrottzuordnung eines Artikels öffnen. Die VOP ergänzt hier ein Feld.

**Prozessvorstellung:** Der Administrator ordnet je Schrottartikel eine VOP-**Schrottart** zu, damit die automatische FA-Schrotterzeugung (siehe **Automatische FA-Schrotterzeugung einrichten**) den richtigen Schrottartikel für Saum- bzw. Trennschrott verwendet.

| Feld | Erläuterung |
|------|-------------|
| **Schrottart** | Ordnet dem Artikel-Schrott eine VOP-Schrottart zu. Werte: **(leer):** Keine VOP-Schrottart — der Artikel-Schrott wird von der automatischen FA-Schrotterzeugung nicht herangezogen. **Trennschrott:** Der Schrottartikel wird für den zwischen den Einteilungen anfallenden Trennverlust verwendet. **Saumschrott:** Der Schrottartikel wird für den an Anfang und Ende platzierten Saumschrott verwendet. Wenn gesetzt, wählt die FA-Schrotterzeugung anhand dieser Art den passenden Schrottposten. |

## Der Arbeitsbereich Vormaterial Orientierte Planung

**Einstieg:** Die Seite **Vormaterial Orientierte Planung** wird auf drei Wegen geöffnet:

- über **Suchen** (Begriff *VOP* bzw. *Vormaterial Orientierte Planung*),
- aus einer Fertigungsauftragszeile (fest geplant, geplant oder freigegeben) über die Aktion **Vormaterial Orientierte Planung**,
- aus einem **freigegebenen** Verkaufsauftrag über die Aktion **Vormaterial Orientierte Planung** in den Auftragszeilen (nur für Zeilen der Art Artikel; der Verkaufsauftrag muss den Status *Freigegeben* haben).

Wird die Seite aus einem Beleg geöffnet, ist die zugehörige Beleg-/Auftragszeile im Auftragssuchergebnis hervorgehoben.

Die Seite ist dreigeteilt: oben das **Vormaterial** (Suchergebnis), in der Mitte die **Auftragssuchergebnisse**, unten die **Zuordnungen**. Zusätzlich stehen die Infoboxen **Vormaterialeigenschaften**, **Auftragseigenschaften** und **Trennüberwachung** zur Verfügung.

### Suchoptionen und Vormaterialsuche

Im Register **Suchoptionen** steuert der Anwender, wie das Vormaterial ermittelt und dargestellt wird.

| Feld | Erläuterung |
|------|-------------|
| **Artikelnr.** | Wenn eine Artikelnummer eingegeben (oder über die Auswahl gewählt) wird, ermittelt das System beim Verlassen des Feldes alle verfügbaren Chargen und Seriennummern dieses Artikels in ihren Lagerorten und Lagerplätzen und stellt sie als Ergebniszeilen dar. |
| **Matchcode** | Wenn ein vollständiger Matchcode oder ein Teil davon (ergänzt durch `*`) eingegeben wird, ermittelt das System alle passenden Artikel und dazu die verfügbaren Chargen/Seriennummern als Ergebniszeilen. |
| **Ansichtsart** | Bestimmt die Gruppierung der Ergebniszeilen. Wenn auf Artikel- und Lagerortebene gestellt, werden die Zeilen hierarchisch nach Artikel und Lagerort dargestellt; auf Artikelebene nach Artikeln gruppiert; auf Charge-/Seriennummernebene ohne Hierarchie je Charge/Seriennummer. Die verfügbaren Werte stammen aus dem Basismodul; die Vorbelegung wird aus der Standard-Ansichtsart der Materialeigenschaften-Einrichtung übernommen. |

Über die Aktion **Vormaterialsuche** (Bereich **Vormaterial**) öffnet der Anwender eine eigenschaftsbasierte Suche: Zunächst wird eine Materialart gewählt, danach werden zu deren Eigenschaften Werte, Filter oder `*` eingegeben. Das Ergebnis erscheint ebenfalls im Vormaterialsuchergebnis.

### Vormaterialsuchergebnisse — Spalten

Der Bereich **Vormaterialsuchergebnisse** zeigt je Zeile Bestandsinformationen und die konfigurierten Eigenschaften. Die wesentlichen Spalten:

| Feld | Erläuterung |
|------|-------------|
| **Beschreibung** | Zeigt die hierarchische Bezeichnung (Artikel, Lagerort, Charge) gemäß **Ansichtsart**; die Formatierung kennzeichnet die Ebene der Zeile. |
| **Gesperrt** | Zeigt an, ob der Artikel gesperrt ist; gesperrtes Vormaterial ist als solches erkennbar und sollte nicht eingeplant werden. |
| **Lagerbestand** | Zeigt den verfügbaren Lagerbestand der Zeile als Grundlage für die Einteilung. |
| **Menge in Bestellung** | Zeigt die noch zugehende Menge aus Einkaufsbestellungen, um zukünftige Verfügbarkeit einzuschätzen. |
| **Menge in Fertigungsauftrag** | Zeigt die Menge, die in Fertigungsaufträgen als Zugang erwartet wird. |
| **Menge in Komponentenzeilen** | Zeigt die bereits als FA-Komponente reservierte/geplante Menge des Vormaterials. |
| **Menge in Verkaufsauftrag** | Zeigt die aus Verkaufsaufträgen bereits gebundene Menge. |
| **Matchcode** | Zeigt den Matchcode des Artikels für die schnelle Identifikation. |
| **Eigenschaftswert 1 … 10** | Zeigt je nach Materialart und Datentyp die konfigurierten primären Eigenschaften (Text- oder Dezimalwert). Nur die auf der Materialart als **Primäre Eigenschaft** gepflegten Merkmale werden eingeblendet. |

### Auftragssuchergebnisse — Spalten

Der Bereich **Auftragssuchergebnisse** zeigt die über **Auftragssuche** ermittelten Verkaufs- und Fertigungsauftragszeilen, die noch nicht vollständig durch Vormaterial gedeckt sind.

| Feld | Erläuterung |
|------|-------------|
| **Markiert** | Zeigt, ob die Zeile für **Zuordnen** markiert ist; nur markierte Zeilen werden zugeordnet. |
| **Zeilenart** | Kennzeichnet die Herkunft der Bedarfszeile. Werte: **VK-Auftrag:** offene Verkaufsauftragszeile. **Fertigungsauftrag:** offene Fertigungsauftragszeile. |
| **Belegnr.** | Zeigt die Nummer des Verkaufs- bzw. Fertigungsauftrags. |
| **Belegzeilennr.** | Zeigt die Zeilennummer im Beleg. |
| **Beleg FA-Status** | Zeigt bei Fertigungsauftragszeilen den Status des Fertigungsauftrags (z. B. **Simuliert**, **Geplant**, **Fest geplant**, **Freigegeben**). |
| **Artikelnr.** | Zeigt den zu fertigenden Artikel der Bedarfszeile. |
| **Beschreibung / Beschreibung 2** | Zeigen die Artikelbeschreibung der Bedarfszeile. |
| **Menge / KG / Meter / Stück** | Zeigen die Bedarfsmenge in Basiseinheit und in den steel-typischen Einheiten. |
| **Trennbreite** | Zeigt die für die Zeile relevante Trennbreite (Bandbreite) als Planungshilfe. |
| **Auftragsmenge / Auftrag KG / Auftrags Meter / Auftrag Stück** | Zeigen die ursprüngliche Auftragsmenge in den jeweiligen Einheiten. |
| **Restauftragsmenge / Restauftrag KG / Restauftrag Meter / Restauftrag Stück** | Zeigen die noch offene Auftragsmenge, die durch Vormaterial gedeckt werden soll. |
| **FA Menge / FA KG / FA Meter / FA Stück** | Zeigen bei Fertigungsauftragszeilen die zu produzierende Menge. |
| **FA Fertiggestellte Menge / FA Fertiggestellte Kg / … Meter / … Stück** | Zeigen den bereits fertiggestellten Anteil des Fertigungsauftrags. |
| **Arbeitsplan Nr.** | Zeigt den Arbeitsplan der Bedarfszeile. |
| **Warenausg.-Datum / Fälligkeitsdatum** | Zeigen Liefer- und Fälligkeitstermin der Bedarfszeile. |

Aktionen im Bereich: **Markieren**, **Alles markieren**, **Markierungen löschen**, **Artikelkarte** und **Belegkarte** (öffnet den zugehörigen Verkaufs- oder Fertigungsauftrag).

### Zuordnungen — Bereich und Aktionen

Der Bereich **Zuordnungen** zeigt das Ergebnis der Verheiratung von Vormaterial und Auftrag. Über **Zuordnen** (Bereich **Aufträge**) entsteht je Kombination eine Zeile. Zuordnungszeilen der Art **Anarbeitung** oder **Lagerfertigung** dürfen auch manuell eingefügt werden; das Einfügen anderer Zeilenarten wird mit einem Hinweis abgewiesen.

Aktionen im Untermenü **Zuordnungen**: **Markieren**, **Alles markieren**, **Markierungen löschen**, **Vormaterialkarte**, **Belegkarte**, **Einteilungen** (öffnet die **Chargennr. Einteilungen** des Vormaterials), **Vormaterial filtern** (Filter auf das Vormaterial der aktuellen Zeile) und **Filter aufheben**.

#### Felder der Zuordnungszeile

Die folgende Tabelle dokumentiert die Felder der Zuordnungszeile. Ein Teil der Felder (Zwischen- und Detailmaße) ist standardmäßig ausgeblendet und kann bei Bedarf eingeblendet werden.

| Feld | Erläuterung |
|------|-------------|
| **Markiert** | Kennzeichnet, ob die Zeile für Aktionen wie **Fertigungsaufträge erstellen** oder **Zwischenlagerfertigung erstellen** ausgewählt ist. |
| **Zeilenart** | Bestimmt, wofür die Zuordnung produziert wird. Werte: **VK-Auftrag:** Fertigung für eine Verkaufsauftragszeile. **Fert.-Auftrag:** Zuordnung zu einem bestehenden Fertigungsauftrag. **Anarbeitung:** Zuordnung zu einem vorgelagerten Fertigungsauftrag (Anarbeitung). **Lagerfertigung:** Fertigung ans Lager. Für **VK-Auftrag** und **Fert.-Auftrag** sind Kopf- und Vormaterialfelder gesperrt (aus dem Beleg übernommen); **Anarbeitung** und **Lagerfertigung** sind editierbar. |
| **Belegnr. / Belegzeilennr. / Beleg FA-Status** | Enthalten den zugeordneten Beleg (Verkaufs- oder Fertigungsauftrag) samt Zeile und FA-Status. Bei Änderung der Belegzeile wird die Zeile neu berechnet. |
| **Fehler vorhanden** | Zeigt an, ob die Zeile noch logische Fehler enthält (z. B. fehlende Trenneinheit, fehlende Menge, unvollständiges Vormaterial). Über die Detailanzeige wird der **Protokolleintrag** mit dem konkreten Fehlertext angezeigt. Nur fehlerfreie Zeilen lassen sich in Fertigungsaufträge überführen. |
| **Artikelnr. / Variantencode / Matchcode** | Enthalten den zu fertigenden Artikel. Bei editierbaren Zeilenarten löst eine Änderung eine Neuberechnung der Zeile aus. |
| **Beschreibung / Beschreibung 2** | Enthalten die Bezeichnung des zu fertigenden Artikels. |
| **Zugew. Segment** | Bestimmt den Ort auf dem Vormaterial, an dem die Einteilung platziert wird (z. B. die Messereinteilung/den Längsabschnitt bei Coils). Zeilen im selben Segment müssen dieselbe Trennarbeitsplatzgruppe verwenden. |
| **Zugew. Breite / Zugew. Länge / Zugewiesene Dicke** | Enthalten den Wert der Trenndimension des Fertigartikels gemäß der **Trenndimension** der Vormaterialart; nur das der Trenndimension entsprechende Maß ist standardmäßig sichtbar. Editierbar, solange keine manuellen Einteilungen verwendet werden. |
| **Zugew. Trenneinheiten** | Legt fest, wie viele Einheiten der Trenndimension auf dem Vormaterial platziert werden. Wenn ein Wert erfasst wird, berechnet das System automatisch **Zugew. Menge** (Vormaterialverbrauch) und **Fert. Menge** (Fertigungsmenge). Solange keine Trenneinheit gesetzt ist, werden keine Einsatz- und Fertigungsmengen berechnet. |
| **Zugew. Trenneinheitenfaktor** | Bestimmt, welcher Anteil des Vormaterials im Segment belegt wird; der Wert 1 entspricht dem vollständigen Vormaterial. Ein kleinerer Wert belegt nur einen Teil des Segments. |
| **Zugew. Menge (Stück / Meter / KG)** | Enthält die für die Zuordnung verbrauchte Vormaterialmenge (die erwartete Menge der FA-Komponentenzeile). Wird aus Trenneinheiten und Trennwert berechnet, kann aber manuell angepasst werden. |
| **Fert. Menge (Stück / Meter / KG)** | Enthält die für die Zuordnung zu produzierende Fertigmenge (die Menge der FA-Zeile). Wird automatisch berechnet und kann manuell angepasst werden. |
| **Offene Menge (Stück / Meter / KG)** | Zeigt die noch zu verplanende Menge des zugeordneten Belegs. |
| **Vormaterial Artikelnr. / Vormaterial Variantencode / Vormaterial Chargennr.** | Enthalten die zugeordnete Vormaterialcharge. |
| **Vormaterial Chargeneinteilungsnr.** | Verweist auf die konkrete Chargeneinteilung des Vormaterials, die dieser Zuordnung zugewiesen ist. |
| **Vormaterial Lagerortcode / Vormaterial Lagerplatzcode** | Enthalten den aktuellen Lagerort und Lagerplatz des Vormaterials; werden aus dem Bestand des Vormaterials ermittelt. |
| **Vormaterialbreite / Vormateriallänge / Vormaterialdicke** | Enthalten die Maße des zugeordneten Vormaterials als Basis für die Einteilung. |
| **Anarbeitung Zugeordneter FA-Status / Anarbeitung Zugeordneter FA-Nr. / Anarbeitung Zugeordnete FA Zeile** | Enthalten bei der Zeilenart **Anarbeitung** den vorgelagerten Fertigungsauftrag, in den die Anarbeitung als Komponente eingeht. Editierbar nur bei Anarbeitungszeilen. |
| **Bemerkung** | Enthält eine Bemerkung zur Zuordnungszeile; sie wird an die FA-Komponentenzeile (**Trennbemerkung**) weitergegeben. |
| **Zugew. Querteilungen** | Bestimmt bei Spaltbändern die Querteilungen innerhalb des Segments (z. B. um den Außendurchmesser zu begrenzen). |
| **Trenndimension** | Enthält die aus der Vormaterialart übernommene Trenndimension der Zeile. |
| **Zugewiesener Trenndimensionswert / Vormaterialtrenndimensionswert** | Enthalten den zugewiesenen bzw. den insgesamt verfügbaren Trenndimensionswert; die Differenz ergibt den noch verfügbaren Wert (siehe **Trennüberwachung**). |
| **Zwischentrennartikelnr. / Zwischenvariantencode** | Enthalten den zu fertigenden Zwischenartikel; er entsteht, wenn die Vormaterialart einen **Trennzuschlag Zwischenlagerfertigung** hat. |
| **Zwischenbreite / Zwischenlänge / Zwischendicke / Zwischentrenndimmensionswert** | Enthalten die Maße des Zwischenartikels gemäß Trenndimension. |
| **Arbeitsplannr. / Arbeitsplanversionscode** | Enthalten den Arbeitsplan des zu fertigenden Fertigartikels. |
| **Zwischenfertigungsarbeitsplannr. / Zwischenfertigungsarbeitsplanversionscode** | Enthalten den Arbeitsplan des zu fertigenden Zwischenartikels. |
| **Trennarbeitsplatzgruppennr.** | Enthält die erste Trennarbeitsplatzgruppe im Arbeitsplan des Fertigartikels; alle Zeilen desselben Segments müssen dieselbe Trennarbeitsplatzgruppe verwenden, andernfalls wird die Eingabe mit einem Hinweis abgewiesen. |

### Trennüberwachung (Infobox)

Die Infobox **Trennüberwachung** stellt die Einteilung des aktuellen Vormaterials grafisch dar und zeigt die Deckung der Trenndimension und der Menge.

| Feld | Erläuterung |
|------|-------------|
| **Für Zuweisung** | Zeigt den insgesamt einteilbaren Trenndimensionswert des Vormaterials (Vormaterialtrenndimensionswert). |
| **Zugewiesen** | Zeigt den bereits über Einteilungen zugewiesenen Trenndimensionswert. |
| **Verfügbar** | Zeigt den noch freien Trenndimensionswert (Für Zuweisung minus Zugewiesen); wird der Wert überschritten, erscheint eine entsprechende Warnung. |
| **Vormaterialmenge** | Zeigt die Gesamtmenge des Vormaterials. |
| **Zugewiesene Menge** | Zeigt die bereits zugewiesene Menge. |
| **Verfügbare Menge** | Zeigt die noch verfügbare Menge (Vormaterialmenge minus zugewiesene Menge). |
| **Artikelnr. / Chargennr. / Variantencode** | Zeigen das Vormaterial, auf das sich die Überwachung bezieht. |

Dieselbe grafische Darstellung erscheint als Infobox **Trennüberwachung** in der FA-Zeilenübersicht (siehe **Historie und Nachverfolgung**).

## Fertigungsaufträge erstellen (FA-Erstellung)

Die FA-Erstellung ist der zentrale Abschlussschritt: Aus den fehlerfreien, markierten Zuordnungszeilen entstehen die Fertigungsaufträge. Die Reihenfolge und die Aktionsbezeichnungen entsprechen dem Ablauf auf der Seite **Vormaterial Orientierte Planung**.

**Ablauf:**

1. Zeile(n) im Bereich **Vormaterialsuchergebnisse** auswählen.
2. Aktion **Auftragssuche** (Bereich **Vormaterial**) ausführen und im Bereich **Auftragssuchergebnisse** über **Markieren** die Bedarfszeilen kennzeichnen.
3. Aktion **Zuordnen** (Bereich **Aufträge**) ausführen — je Kombination entsteht eine Zuordnungszeile.
4. In den Zuordnungszeilen **Zugew. Trenneinheiten** (und ggf. **Zugew. Segment**, **Trenneinheitenfaktor**) erfassen; **Zugew. Menge** und **Fert. Menge** werden berechnet.
5. Über die Spalte **Fehler vorhanden** die Zeilen prüfen (Detailanzeige zeigt den Protokolleintrag).
6. Fehlerfreie Zuordnungszeilen über **Markieren** kennzeichnen.
7. Aktion **Fertigungsaufträge erstellen** (Bereich **Zuordnungen**) ausführen. Ist als **FA-Erstellungsmethode** *Abfrage der Methode* eingerichtet, erscheint die Auswahl **FA-Erstellungsmethode auswählen** (Je Zuordnung / Je Vormaterial / Je Verkaufsauftragszeile).
8. Rückfrage **Fertigungsaufträge geändert oder erstellt. Protokoll anzeigen?** — bei Bestätigung öffnen sich die **Protokolleinträge**.

**Prüfungen vor der Erstellung:** Das System prüft alle nicht beendeten Zuordnungszeilen auf Fehler; bestehen Fehler, bricht der Vorgang mit dem Hinweis ab, dass Zuordnungszeilen mit Fehlern vorhanden sind. Zeilen ohne zugewiesene Menge werden mit einer entsprechenden Meldung abgewiesen. Bei der Zeilenart **Anarbeitung** müssen der zugeordnete Anarbeitungs-Fertigungsauftrag samt Zeile gesetzt sein.

**Statusanhebung:** Ist der Zielstatus (**FA-Anlagestatus** aus der VOP Einrichtung) höher als der Status eines vorhandenen Fertigungsauftrags der Zeilenart **Fert.-Auftrag**, hebt das System den Fertigungsauftrag automatisch auf den Zielstatus an.

**Mehrstufige Fertigung:** Enthält die Zuordnung einen Zwischenartikel (aus **Trennzuschlag Zwischenlagerfertigung**) oder eine geplante Lageranarbeitung, erzeugt die FA-Erstellung eine mehrstufige FA-Kette und trägt die Charge der Zwischenstufe automatisch als FA-Komponente (Vormaterial) der nächsten Fertigungsstufe ein.

**Kein separater Buchungslauf:** Das Modul bucht nicht selbst; die eigentliche Rückmeldung/Buchung erfolgt anschließend im Standard-Fertigungsauftrag. Es gibt daher keine Teilbeenden-/Beenden-Aktion in der VOP; der Abschluss der Planung ist die FA-Erstellung.

### Sonderaktionen der Zuordnungen

| Aktion | Erläuterung |
|--------|-------------|
| **Vormaterial zuordnen** | Weist den markierten Zuordnungszeilen das erste markierte Vormaterial aus dem Vormaterialsuchergebnis zu. |
| **Auftrag zuordnen** | Weist den markierten Zuordnungszeilen den ersten markierten Auftrag aus dem Auftragssuchergebnis zu. |
| **Chargeneinteilung zuweisen** | Weist der ersten markierten Zuordnungszeile eine bereits vorhandene Chargeneinteilung zu, sodass auf einer Chargeneinteilung mehrere Aufträge produziert werden. |
| **Einteilung auf Vormaterial kopieren** | Kopiert die Einteilung der markierten Zuordnungszeilen auf die im Vormaterialsuchergebnis markierten Chargen; hilfreich, wenn dieselbe Einteilung für mehrere gleiche Vormaterialchargen gelten soll. Voraussetzung ist, dass die Zielcharge keine aktiven (noch nicht verbrauchten) Einteilungen besitzt und alle Ausgangszeilen dasselbe Vormaterial verwenden. |
| **Zwischenlagerfertigung erstellen** | Erstellt aus den summierten Trennwerten der markierten Zuordnungszeilen eine Zuordnungszeile für ein zu fertigendes Zwischenprodukt; bei der FA-Erstellung entsteht daraus eine mehrstufige Fertigung. |
| **Lagerfertigung erstellen** | Erstellt mit dem verbleibenden Trennwert (Vormaterialtrennwert minus eingeteilte Trennwerte) einen Artikel für eine Fertigung ans Lager als Zuordnungszeile. Ist das Vormaterial im Segment bereits vollständig eingeteilt, erscheint ein entsprechender Hinweis. |
| **Protokoll anzeigen** | Ruft das Protokoll der letzten FA-Erstellung auf, solange die Seite nicht geschlossen wurde. |

## Lager, Schrott und Folgebelege

Bei der FA-Erstellung schreibt das Modul mehrere Folgeinformationen in die Fertigungsaufträge und den Lagerbezug:

- **FA-Komponenten:** Für jede Zuordnung wird eine FA-Komponentenzeile mit dem Vormaterial angelegt und – bei vorhandener Vormaterialcharge und Menge – eine **Artikelverfolgung** (Reservierung) für die Charge erzeugt. Die Trenninformationen werden in die Komponente übernommen: **Trenndimension**, **Trenneinheiten**, **Trenneinheitenfaktor**, **Querteilungen**, **Segment**, Maße **Breite/Länge/Dicke** sowie die **Trennbemerkung**. Über **Herkunfts FA-Nr./-Zeilennr./-Status** wird bei mehrstufiger Fertigung die Herkunft festgehalten.
- **Chargeneinteilungen:** Ist **FA-Zeilenartikelverfolgung für Chargeneinteilung erstellen** aktiv, vergibt das System je Trenneinheit eine Chargennummer für die FA-Zeile und legt die zugehörige Artikelverfolgung an.
- **FA-Schrott:** Ist **FA-Schrott durch Saumschrott & Trennverlust** aktiv, erzeugt das Modul FA-Schrottposten aus **Saumschrott** und **Trennschrott** anteilig zum Einteilungswert. Die erzeugten **FA-Schrottposten** tragen das Kennzeichen **Von VOP**; auf **FA-Schrott** und **Artikel Schrotte** ist die **Schrottart** sichtbar.

### FA-Arbeitsplan und Arbeitsgangzeilen

Der Arbeitsplan des Fertigartikels muss mindestens eine **Trennarbeitsplatzgruppe** enthalten. In den **Arbeitsgangzeilen** des Arbeitsplans sowie in den **Arbeitsplanversionszeilen** wird je Zeile das Kennzeichen **Trennarbeitsplatzgruppe** angezeigt, sodass der Planer erkennt, welcher Arbeitsgang den Trennvorgang abbildet. Aus der ersten Trennarbeitsplatzgruppe werden die Trennvorgabewerte für die Einteilung übernommen.

## Historie und Nachverfolgung

### Protokolleinträge

**Einstieg:** Über die Aktion **Protokoll anzeigen** auf der Seite **Vormaterial Orientierte Planung** oder automatisch nach der FA-Erstellung (Rückfrage). Die Seite **Protokolleinträge** zeigt die beendeten Zuordnungszeilen des aktuellen Benutzers.

| Feld | Erläuterung |
|------|-------------|
| **Zeilenart** | Zeigt, ob die Zeile für einen VK-Auftrag, Fertigungsauftrag, eine Anarbeitung oder Lagerfertigung erstellt wurde. |
| **Artikelnr. / Variantencode** | Zeigen den gefertigten Artikel. |
| **Protokolleintrag** | Zeigt den Ergebnistext der FA-Erstellung (z. B. neuer Fertigungsauftrag erstellt, zu Fertigungsauftrag hinzugefügt, als Lagerauftrag erstellt). |
| **FA-Status / FA-Nr.** | Zeigen den Status und die Nummer des erzeugten bzw. geänderten Fertigungsauftrags. |

Aktionen: **Fertigungsauftrag** (öffnet den Fertigungsauftrag), **FA-Arbeitsplan** (öffnet die zugehörigen Arbeitsgänge) und **Lageranarbeitung verplanen (VOP)** (öffnet die Planung für eine erzeugte Lagerfertigung erneut).

### Chargennr. Einteilungen

**Einstieg:** Über die Aktion **Einteilungen** im Bereich **Vormaterial** oder im Untermenü **Zuordnungen** der Seite **Vormaterial Orientierte Planung**. Die Liste **Chargennr. Einteilungen** zeigt die auf einem Vormaterial platzierten Einteilungen – sowohl die bereits in Fertigungsaufträgen befindlichen als auch die noch nicht überführten aus VOP-Zuordnungen.

| Feld | Erläuterung |
|------|-------------|
| **Einteilungsnr.** | Zeigt die laufende Nummer der Einteilung auf dem Vormaterial. |
| **Einteilungsposition** | Zeigt die Position der Einteilung; bestimmt die Reihenfolge der Einteilungen. |
| **Art** | Kennzeichnet die Art der Einteilung. Werte: **Einteilung:** reguläre nutzbare Einteilung. **Trennverlust:** zwischen den Einteilungen anfallender Verlust. **Saumschrott:** an Anfang und Ende platzierter Saum. Editierbar nur, solange die Einteilung keiner Zuordnung zugewiesen ist. |
| **Einteilungswert** | Enthält den Wert der Einteilung in der Trenndimension. Editierbar nur, solange die Einteilung keiner Zuordnung zugewiesen ist. |
| **Verbraucht** | Zeigt an, ob die Einteilung bereits verbraucht ist; verbrauchte Einteilungen können nicht gelöscht werden. |
| **Zugewiesen zu FA-Komponente** | Zeigt an, ob die Einteilung bereits einer FA-Komponente zugewiesen wurde. |
| **Gep. Einteilung** | Zeigt an, ob es sich um eine geplante (noch nicht in einen Fertigungsauftrag überführte) Einteilung handelt. |
| **Gehört zu Einteilungsnr.** | Verweist auf die übergeordnete Einteilung, zu der Saumschrott- oder Trennverlusteinteilungen gehören. |

Zusätzlich pflegt das Modul auf der **Chargennr.-Information** den **Einteilungswert** je Charge; er ist dort als Kennzahl der Charge sichtbar.

## FAQ und Troubleshooting

### Warum kann ich in einer Zuordnungszeile keine Menge sehen, obwohl ich Vormaterial zugeordnet habe?
Solange in der Zuordnungszeile keine **Zugew. Trenneinheiten** erfasst sind, berechnet das System weder **Zugew. Menge** noch **Fert. Menge**. Erfassen Sie zunächst die Trenneinheiten; danach werden beide Mengen automatisch ermittelt und können bei Bedarf angepasst werden.

### Warum meldet die Spalte „Fehler vorhanden“ einen Fehler, obwohl die Zeile fast vollständig aussieht?
Die Zeile wird auf mehrere Pflichtangaben geprüft: fehlendes oder unvollständiges Vormaterial (Charge/Lagerort), **Zugew. Menge** gleich 0, **Fert. Menge** gleich 0, fehlender Anarbeitungs-Fertigungsauftrag bei Zeilenart **Anarbeitung** sowie eine noch nicht zugewiesene **Vormaterial Chargeneinteilungsnr.** Öffnen Sie die Detailanzeige der Spalte **Fehler vorhanden**, um den konkreten **Protokolleintrag** zu sehen.

### Warum lässt sich das Kennzeichen „FA-Schrott durch Saumschrott & Trennverlust“ nicht setzen?
Dieses Kennzeichen setzt **Erw. FA-Erstellung je Vormaterial** voraus, und dieses wiederum die **FA-Erstellungsmethode** *Je Vormaterial*. Stellen Sie in der **VOP Einrichtung** zuerst die Methode auf *Je Vormaterial*, aktivieren Sie **Erw. FA-Erstellung je Vormaterial** und setzen Sie danach das Schrottkennzeichen.

### Warum verlangt die Einrichtung, dass ich eine Option der Auftragssuche aktiviere?
Die **Auftragssuche** benötigt mindestens eine Bedarfsquelle. Ist weder **Auftragssuche inkl. Fertigungsaufträge** noch **Auftragssuche inkl. Verkaufsaufträge** aktiv, bricht die Einrichtung mit dem Hinweis ab, dass mindestens eine Option gesetzt sein muss. Aktivieren Sie mindestens eine der beiden Optionen.

### Warum finde ich einen bestimmten Verkaufsauftrag nicht in den Auftragssuchergebnissen?
Eine Verkaufsauftragszeile erscheint nur, wenn sie mengenmäßig noch nicht vollständig durch einen Fertigungsauftrag als Bedarfsdecker abgedeckt ist. Vollständig gedeckte Zeilen werden nicht mehr angezeigt. Prüfen Sie außerdem, ob **Auftragssuche inkl. Verkaufsaufträge** in der **VOP Einrichtung** aktiv ist.

### Warum kann ich die Seite „Vormaterial Orientierte Planung“ nicht aus jedem Verkaufsauftrag öffnen?
Die Aktion **Vormaterial Orientierte Planung** ist in den Verkaufsauftragszeilen nur für Zeilen der Art Artikel wirksam und setzt voraus, dass der Verkaufsauftrag den Status **Freigegeben** hat. Geben Sie den Auftrag frei und wählen Sie eine Artikelzeile.

### Warum entstehen bei der FA-Erstellung mehrere Fertigungsaufträge statt einem?
Das hängt von der **FA-Erstellungsmethode** ab. Bei **Je Zuordnung** entsteht je Zuordnungszeile ein eigener Fertigungsauftrag; bei **Je Vormaterial** bzw. **Je Verkaufsauftragszeile** werden Zeilen mit gleichem Vormaterial bzw. gleicher Auftragszeile zusammengefasst. Bei **Abfrage der Methode** wählen Sie die Methode bei jeder Erstellung selbst.

### Was passiert, wenn ich „Lagerfertigung erstellen“ verwende, obwohl das Vormaterial bereits voll eingeteilt ist?
Ist der verbleibende Trennwert im Segment gleich 0, ist das Vormaterial vollständig eingeteilt und es kann keine Lagerfertigung mehr gebildet werden. Das System weist dies mit dem Hinweis ab, dass das Vormaterial im Segment komplett eingeteilt ist.

### Warum verwenden zwei Zuordnungszeilen im selben Segment plötzlich unterschiedliche Ergebnisse?
Alle Zeilen desselben Segments müssen dieselbe **Trennarbeitsplatzgruppe** verwenden. Weicht eine Zeile ab, weist das System die Eingabe mit dem Hinweis ab, dass die Verwendung der Arbeitsplatzgruppe nicht möglich ist, weil andere Zeilen im gleichen Segment eine andere Arbeitsplatzgruppe verwenden. Vereinheitlichen Sie die Trennarbeitsplatzgruppe je Segment.

### Wie plane ich eine erzeugte Lagerfertigung weiter?
Nach der FA-Erstellung erscheint die Lagerfertigung im Protokoll. Über die Aktion **Lageranarbeitung verplanen (VOP)** in den **Protokolleinträgen** wird die Lageranarbeitung erneut im oberen Vormaterialbereich der Planung eingefügt und kann wie eine normale Vormaterialcharge weiter eingeteilt werden.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Ablauf entlang realistischer Auslöser. Alle Schritte und Bezeichnungen entsprechen der Seite **Vormaterial Orientierte Planung** und den zuvor beschriebenen Aktionen.

### Coil auf mehrere Verkaufsaufträge einteilen

1. **Auslöser:** Ein Kunde ruft an und benötigt kurzfristig mehrere Spaltbänder aus einem vorhandenen Coil; die entsprechenden Verkaufsaufträge sind bereits freigegeben.
2. **Einstieg in BC:** Der Planer öffnet die Seite **Vormaterial Orientierte Planung** über **Suchen** (Begriff *VOP*).
3. **Kernablauf:** Im Feld **Artikelnr.** die Coil-Artikelnummer eingeben; im Vormaterialsuchergebnis die passende **Chargennr.** wählen. Aktion **Auftragssuche** (Bereich **Vormaterial**) ausführen und im Bereich **Auftragssuchergebnisse** die offenen Verkaufsauftragszeilen über **Markieren** kennzeichnen. Aktion **Zuordnen** (Bereich **Aufträge**) ausführen. In jeder Zuordnungszeile **Zugew. Trenneinheiten** je Spaltband erfassen und – falls verschiedene Messereinteilungen – **Zugew. Segment** anpassen. Einteilung in der Infobox **Trennüberwachung** prüfen, **Verfügbar** darf nicht überschritten werden.
4. **Abschluss:** Fehlerfreie Zeilen über **Markieren** kennzeichnen und **Fertigungsaufträge erstellen** ausführen. Rückfrage **Protokoll anzeigen?** bestätigen und im **Protokolleintrag** die je Auftrag erzeugten Fertigungsaufträge prüfen.

### Block mit Zwischenlagerfertigung planen

1. **Auslöser:** Eine interne Fertigungsmeldung fordert einen Fertigartikel, der zunächst aus einem Block mit Übermaß vorgeschnitten werden muss.
2. **Einstieg in BC:** Der Planer öffnet aus der fest geplanten Fertigungsauftragszeile die Aktion **Vormaterial Orientierte Planung**; die zugehörige FA-Zeile ist im Auftragssuchergebnis hervorgehoben.
3. **Kernablauf:** Vormaterial (Block) über **Artikelnr.** oder **Vormaterialsuche** ermitteln und die **Chargennr.** wählen. Ist auf der Vormaterialart ein **Trennzuschlag Zwischenlagerfertigung** hinterlegt, füllt das System in der Zuordnungszeile automatisch den **Zwischentrennartikel** samt Maßen. **Zugew. Trenneinheiten** (nach Dicke) erfassen; **Zugew. Menge** und **Fert. Menge** prüfen. Bei Bedarf über **Zwischenlagerfertigung erstellen** eine gesonderte Zwischenstufe bilden.
4. **Abschluss:** Zeilen **Markieren** und **Fertigungsaufträge erstellen**. Das Modul bildet eine mehrstufige FA-Kette; die Charge der Zwischenstufe wird automatisch als FA-Komponente der nächsten Stufe eingetragen. Ergebnis im **Protokolleintrag** kontrollieren.

### Restmenge eines Vormaterials ans Lager fertigen

1. **Auslöser:** Nach der Einteilung eines Coils auf Kundenaufträge bleibt ein nutzbarer Restwert übrig, der nicht verfallen soll.
2. **Einstieg in BC:** Der Planer arbeitet in der bereits geöffneten Seite **Vormaterial Orientierte Planung** weiter.
3. **Kernablauf:** Die Zuordnungszeilen des betreffenden Vormaterials **Markieren**. Über **Lagerfertigung erstellen** (Bereich **Zuordnungen**) wird mit dem verbleibenden Trennwert ein Artikel für eine Fertigung ans Lager als neue Zuordnungszeile (Zeilenart **Lagerfertigung**) gebildet. In der neuen Zeile Trenneinheiten und Mengen prüfen.
4. **Abschluss:** Alle Zeilen **Markieren** und **Fertigungsaufträge erstellen**. Die Lagerfertigung erscheint im Protokoll und kann über **Lageranarbeitung verplanen (VOP)** bei Bedarf weiter eingeteilt werden.
