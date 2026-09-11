---
title: Anwenderhandbuch m+m Material Planning with Unit Conversion
---

# Anwenderhandbuch m+m Material Planning with Unit Conversion

## Einleitung

Die App **m+m Material Planning with Unit Conversion** verbindet die Materialdisposition von m+m mit der Einheitenumrechnung KG / Meter / Stück. Sie ergänzt die **Dispositionszeilen** um vier zusätzliche Spalten – **Akt. geplante Einheit**, **Akt. geplante KG**, **Akt. geplante Meter** und **Akt. geplante Stück** – und rechnet diese Werte automatisch aus der bereits erfassten **Akt. Dispositionsmenge** um. Beim Erstellen der Bestellvorschläge übergibt die App die gewählte Einheit an die Bestellvorschlagszeile.

Die App besitzt **keine eigenen Seiten, Einrichtungsseiten oder Berichte**. Sie erweitert ausschließlich die Dispositionszeilen der App **m+m Material Planning** und nutzt die Umrechnungslogik und die Einrichtung der App **m+m Unit Conversion**. Ohne diese beiden Apps ist die Funktion nicht verwendbar.

**Zielgruppe.** Primäre Anwender sind **operative Disponenten und Einkäufer**, die in der Materialdisposition täglich Bestellmengen festlegen und in den Bestellvorschlag übergeben. Für sie ist entscheidend, eine Bestellmenge in der Einheit erfassen zu können, in der sie denkt (z. B. Meter eines Coils), während das System die restlichen Einheiten und die eigentliche Bestellmenge daraus ableitet. Sekundäre Zielgruppe sind **Administratoren und Stammdatenverantwortliche**, die einmalig die Einheitencodes und die Umrechnungsfaktoren je Artikel hinterlegen.

**Prozessüberblick und typischer Einstieg.** Der Anwender öffnet die **Materialdispositionsliste**, wählt eine Disposition und öffnet die **Materialdisposition**. Dort kalkuliert er die Disposition, wodurch sich die **Dispositionszeilen** öffnen. In den Zeilen erfasst er auf Artikelebene die gewünschte Menge – wahlweise als **Akt. Dispositionsmenge** oder über eine der Einheitenspalten **Akt. geplante KG / Meter / Stück** – und erstellt anschließend die **Bestellvorschlagszeilen**. Voraussetzung für die Umrechnung sind die einmalige Einrichtung der Einheitencodes (**KG Meter Stück Einrichtung**) und die Umrechnungsfaktoren auf der **Artikelkarte**.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zum fertigen Bestellvorschlag. Die Reihenfolge folgt der technischen Abhängigkeit: zuerst die Einrichtung, dann die Stammdaten, dann die tägliche Arbeit.

1. **Einheitencodes einrichten (einmalig, Administrator).** Öffnen Sie über **Suchen** die Seite **KG Meter Stück Einrichtung** und tragen Sie **Einheitencode für KG**, **Einheitencode für Meter** und **Einheitencode für Stück** ein. Erst dadurch weiß das System, welche Einheiten der Basiseinheit KG, Meter oder Stück entsprechen.
2. **Umrechnungsfaktoren am Artikel hinterlegen (Stammdaten).** Öffnen Sie die **Artikelkarte** des betreffenden Artikels und erfassen Sie im Bereich **Faktoren:** die Werte **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück**. Ohne diese Faktoren kann das System zwischen den Einheiten nicht umrechnen.
3. **Disposition öffnen.** Öffnen Sie über **Suchen** die **Materialdispositionsliste** und öffnen Sie durch Auswahl einer Zeile die **Materialdisposition**.
4. **Disposition kalkulieren.** Wählen Sie die Aktion **Disposition kalkulieren**. Das System füllt die **Dispositionsmenge** und öffnet die **Dispositionszeilen**.
5. **Menge erfassen.** Erfassen Sie in den Dispositionszeilen auf Artikelebene die Bestellmenge – entweder in **Akt. Dispositionsmenge** oder in einer der Spalten **Akt. geplante KG**, **Akt. geplante Meter** oder **Akt. geplante Stück**. Bei Bedarf stellen Sie die **Akt. geplante Einheit** um. Alle Werte werden gegenseitig umgerechnet.
6. **Bestellvorschlag erzeugen.** Wählen Sie **Bestellvorschlagszeilen erstellen**. Für jede Zeile mit einer Menge größer null entsteht eine Bestellvorschlagszeile; als **Einheitencode** wird die **Akt. geplante Einheit** übernommen. Mit **Bestellvorschlagszeilen anzeigen** prüfen Sie das Ergebnis.

## Einrichtung

Die App selbst bringt keine Einrichtungsseite mit. Die für die Umrechnung notwendige Konfiguration erfolgt vollständig in der App **m+m Unit Conversion** und muss vor der ersten Nutzung in der Disposition abgeschlossen sein.

### KG Meter Stück Einrichtung

**Prozessintro.** Diese unternehmensweite Einrichtung legt der Administrator einmalig fest, bevor die Umrechnung produktiv genutzt wird. Sie ordnet den drei logischen Bezugsgrößen KG, Meter und Stück jeweils einen konkreten Einheitencode aus Business Central zu. Erst diese Zuordnung ermöglicht es der Materialdisposition, eine erfasste Menge der richtigen Bezugsgröße zuzuordnen und umzurechnen. Die hier gesetzten Werte greifen später in den **Dispositionszeilen** (Abschnitt *Tägliche Arbeit*).

**Einstieg:** Öffnen Sie über **Suchen** die Seite **KG Meter Stück Einrichtung**.

| Einrichtung | Erläuterung |
|---|---|
| **Einheitencode für KG** | Wenn Sie hier den Einheitencode für Kilogramm hinterlegen, erkennt das System Artikel mit dieser Basiseinheit als gewichtsgeführt; nur dann werden in den Dispositionszeilen die KG-Werte umgerechnet und in **Akt. geplante KG** gefüllt. Ohne Eintrag findet keine KG-Umrechnung statt. |
| **Einheitencode für Meter** | Wenn Sie den Einheitencode für Meter hinterlegen, behandelt das System Artikel mit dieser Basiseinheit als längengeführt und rechnet die **Akt. geplante Meter** aus der Menge und dem Faktor **Theoretische KG pro Meter** um. Ohne Eintrag bleibt die Meter-Spalte ohne Umrechnung. |
| **Einheitencode für Stück** | Wenn Sie den Einheitencode für Stück hinterlegen, behandelt das System Artikel mit dieser Basiseinheit als stückgeführt und rechnet **Akt. geplante Stück** über den Faktor **Theoretische KG pro Stück** um. Ohne Eintrag entfällt die Stück-Umrechnung. |

**Abhängigkeitshinweis.** Die Umrechnung greift für einen Artikel nur, wenn dessen **Basiseinheitencode** einem der drei hier hinterlegten Einheitencodes entspricht. Ist die Basiseinheit eines Artikels keiner dieser drei Größen zugeordnet, füllt die App die Einheitenspalten in den Dispositionszeilen nicht.

### Einheitenumrechnung für die Materialdisposition einrichten

Diese Funktion – Bestellmengen in KG, Meter oder Stück erfassen und automatisch in die Dispositions- und Bestellmenge umrechnen – erfordert mehrere aufeinander aufbauende Schritte über verschiedene Seiten. Sie werden nachfolgend in Abhängigkeitsreihenfolge beschrieben.

**Prozessintro.** Verantwortlich ist der Administrator (globale Einrichtung) gemeinsam mit dem Stammdatenverantwortlichen (Artikelfaktoren). Die Einrichtung ist vor der ersten Disposition abzuschließen. Angewendet wird das Ergebnis in den **Dispositionszeilen** (Abschnitt *Tägliche Arbeit*), wo der Disponent die umgerechneten Werte nutzt.

1. **Einheitencodes zuordnen.** Zuerst hinterlegen Sie in der **KG Meter Stück Einrichtung** die **Einheitencode für KG / Meter / Stück** (siehe oben). Wenn diese Zuordnung gesetzt ist, erkennt das System, welche Artikel überhaupt umgerechnet werden.
2. **Umrechnungsfaktoren je Artikel pflegen.** Danach erfassen Sie auf der **Artikelkarte** im Bereich **Faktoren:** die Werte **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** (siehe Kapitel *Stammdaten*). Wenn ein Faktor hinterlegt ist, kann das System zwischen KG und Meter bzw. KG und Stück rechnen; fehlt er, bleibt die betroffene Umrechnung wirkungslos.
3. **Mengenverhalten je Artikel festlegen.** Legen Sie auf der Artikelkarte im Bereich **Mengenkonsistenz:** über das Feld **Mengenkonsistenz** fest, ob und wie Mengen automatisch angepasst werden dürfen (siehe *Stammdaten*).
4. **Umrechnung im Tagesablauf nutzen.** Schließlich erfasst der Disponent in den **Dispositionszeilen** die Menge in einer der Einheitenspalten und erstellt mit **Bestellvorschlagszeilen erstellen** den Bestellvorschlag – damit ist die Kette geschlossen (siehe *Tägliche Arbeit*).

**Operativer Abschluss.** Die Konfigurationskette endet in der Aktion **Bestellvorschlagszeilen erstellen** in den Dispositionszeilen: Dort wird die gewählte **Akt. geplante Einheit** als **Einheitencode** in die Bestellvorschlagszeile übernommen.

## Stammdaten

### Artikelkarte: Umrechnungsfaktoren und Mengenkonsistenz

**Prozessintro.** Der Stammdatenverantwortliche pflegt diese Werte je Artikel, sobald ein Artikel gewichts-, längen- oder stückbezogen disponiert werden soll – idealerweise bei der Artikelanlage, spätestens vor der ersten Disposition. Die Faktoren sind die rechnerische Grundlage, ohne die die Einheitenspalten in den **Dispositionszeilen** leer bleiben. Sie werden in der Materialdisposition (Kapitel *Tägliche Arbeit*) ausgewertet.

**Einstieg:** Öffnen Sie die **Artikelkarte** des Artikels (aus der Artikelübersicht die Zeile öffnen) und wechseln Sie in die Bereiche **Faktoren:** und **Mengenkonsistenz:**.

| Feld | Erläuterung |
|---|---|
| **Theoretische KG pro Meter** | Wenn Sie hier das Gewicht je Meter hinterlegen, kann das System in den Dispositionszeilen aus einer in **Akt. geplante Meter** erfassten Länge die zugehörigen **Akt. geplante KG** berechnen und umgekehrt. Ist der Wert null, unterbleibt die KG/Meter-Umrechnung für diesen Artikel. |
| **Theoretische KG pro Stück** | Wenn Sie das Gewicht je Stück hinterlegen, rechnet das System zwischen **Akt. geplante Stück** und **Akt. geplante KG** um. Ist der Wert null, unterbleibt die KG/Stück-Umrechnung. |
| **Mengenkonsistenz** | Legt fest, wie das System die Mengen bei einer Umrechnung anpasst. Die Wirkung je Auswahl: siehe folgende Aufstellung. |

Bedeutung der Werte von **Mengenkonsistenz**:

- **Mengen immer ändern:** Wenn dieser Wert gesetzt ist, passt das System bei jeder Umrechnung die abhängigen Mengen ohne Rückfrage an – der Disponent erhält sofort konsistente KG-, Meter- und Stückwerte.
- **Mengen niemals ändern:** Wenn dieser Wert gesetzt ist, verändert das System bestehende Mengen nicht automatisch; Abweichungen zwischen den Einheiten bleiben bestehen, bis der Anwender sie selbst korrigiert.
- **Mengenänderung durch Nachfrage:** Wenn dieser Wert gesetzt ist, fragt das System vor einer automatischen Mengenanpassung nach und ändert die Menge nur nach Bestätigung durch den Anwender.

**Hinweis zu tatsächlichen Faktoren.** Für die Umrechnung verwendet das System vorrangig einen hinterlegten tatsächlichen Faktor (**Tatsächliche KG pro Meter** bzw. **Tatsächliche KG pro Stück**), sofern dieser für den Datensatz größer null ist; andernfalls greift der theoretische Faktor der Artikelkarte. In den Dispositionszeilen werden diese tatsächlichen und theoretischen Faktoren mitgeführt, aber nicht editierbar angezeigt.

## Tägliche Arbeit in den Dispositionszeilen

In den **Dispositionszeilen** erfasst der Disponent die tatsächlich zu bestellende Menge. Die App ergänzt hier die Umrechnung in KG, Meter und Stück. Die Zeilen werden nicht über **Suchen** geöffnet, sondern aus der Disposition heraus.

**Steuernde Einrichtung.** Die in diesem Abschnitt beschriebenen Spalten werden durch die **KG Meter Stück Einrichtung** (welche Einheiten gelten als KG/Meter/Stück) und durch die Faktoren der **Artikelkarte** (Umrechnungsfaktoren, Mengenkonsistenz) gesteuert. Ist eine dieser Voraussetzungen nicht erfüllt, bleiben die Einheitenspalten ohne Werte (siehe Kapitel *Einrichtung* und *Stammdaten*).

**Einstieg:** Öffnen Sie die **Materialdisposition** (aus der **Materialdispositionsliste**) und wählen Sie **Disposition kalkulieren**; im Anschluss öffnen sich die **Dispositionszeilen**. Alternativ öffnen Sie die Zeilen über die entsprechende Aktion in der Materialdisposition.

Die App fügt die folgenden Spalten hinter **Akt. Dispositionsmenge** ein:

| Feld | Erläuterung |
|---|---|
| **Akt. geplante Einheit** | Wenn Sie hier eine Einheit des Artikels wählen, legt sie fest, in welcher Einheit die Bestellmenge geführt wird; genau diese Einheit übergibt das System später als **Einheitencode** an die Bestellvorschlagszeile. Beim Anlegen einer neuen Zeile wird die Einkaufseinheit des Artikels vorbelegt. |
| **Akt. geplante KG** | Wenn Sie hier ein Gewicht erfassen, rechnet das System auf Basis der hinterlegten Faktoren die **Akt. geplante Meter**, **Akt. geplante Stück** und die **Akt. Dispositionsmenge** neu und bestimmt damit die tatsächliche Bestellmenge. |
| **Akt. geplante Meter** | Wenn Sie hier eine Länge erfassen, ermittelt das System über **Theoretische KG pro Meter** die zugehörigen KG und über die Basiseinheit die **Akt. Dispositionsmenge**; der Disponent kann so in Metern denken, obwohl der Artikel z. B. in KG geführt wird. |
| **Akt. geplante Stück** | Wenn Sie hier eine Stückzahl erfassen, rechnet das System über **Theoretische KG pro Stück** in KG und in die **Akt. Dispositionsmenge** um; die Bestellung entsteht damit aus einer Stückvorgabe. |

**Zusammenspiel mit der Basisspalte.** Die App ist eng mit der Basisspalte **Akt. Dispositionsmenge** verzahnt: Jede Änderung an **Akt. Dispositionsmenge**, an einer der drei Einheitenmengen oder an der **Akt. geplante Einheit** löst eine Neuberechnung der jeweils anderen Werte aus. Maßgeblich für die anschließende Bestellung bleibt die **Akt. Dispositionsmenge** in der gewählten **Akt. geplante Einheit**.

**Standardvorbelegung beim Anlegen.** Beim automatischen Anlegen einer Dispositionszeile setzt die App die **Akt. geplante Einheit** auf die im Artikel als Einkaufseinheit hinterlegte Einheit. Dadurch entsteht der Bestellvorschlag ohne weiteres Zutun in der üblichen Einkaufseinheit.

### Bestellvorschlag erstellen und Übergabe der Einheit

Aus den Dispositionszeilen erzeugt der Disponent die Bestellvorschlagszeilen. Dieser Ablauf entspricht dem Standard der Materialdisposition; die App greift ausschließlich bei der Einheit ein.

1. Wählen Sie eine oder mehrere Zeilen auf Artikelebene in den **Dispositionszeilen**.
2. Erfassen Sie die Bestellmenge über **Akt. Dispositionsmenge** oder eine der Einheitenspalten.
3. Wählen Sie die Aktion **Bestellvorschlagszeilen erstellen**. Für jede Zeile mit einer Menge größer null entsteht eine Bestellvorschlagszeile; als **Einheitencode** wird die **Akt. geplante Einheit** übernommen.
4. Prüfen Sie das Ergebnis über **Bestellvorschlagszeilen anzeigen**.

## Typische Anwendungsfälle

### Anwendungsfall 1: Coil-Bestellung in Metern erfassen

1. **Auslöser.** Der Einkauf meldet, dass ein Aluminium-Coil nachbestellt werden muss. Der Artikel wird im Lager in KG geführt, der Disponent denkt jedoch in laufenden Metern.
2. **Einstieg in BC.** Der Disponent öffnet über **Suchen** die **Materialdispositionsliste**, öffnet die betreffende **Materialdisposition** und wählt **Disposition kalkulieren**. Die **Dispositionszeilen** öffnen sich.
3. **Kernablauf.** In der Artikelzeile prüft der Disponent, dass die **Akt. geplante Einheit** korrekt gesetzt ist. Er trägt die benötigte Länge in **Akt. geplante Meter** ein. Das System berechnet über **Theoretische KG pro Meter** die **Akt. geplante KG**, die **Akt. geplante Stück** sowie die **Akt. Dispositionsmenge**. Voraussetzung ist, dass die Meter-Einheit in der **KG Meter Stück Einrichtung** hinterlegt und der Faktor auf der **Artikelkarte** gepflegt ist.
4. **Abschluss.** Der Disponent wählt **Bestellvorschlagszeilen erstellen**; die Bestellvorschlagszeile entsteht mit der übernommenen **Akt. geplante Einheit** als **Einheitencode**. Mit **Bestellvorschlagszeilen anzeigen** kontrolliert er die erzeugten Zeilen.

### Anwendungsfall 2: Regelmäßige Disposition mit vorbelegter Einkaufseinheit

1. **Auslöser.** Im wöchentlichen Dispositionslauf werden für mehrere Artikel neue Dispositionszeilen erzeugt.
2. **Einstieg in BC.** Nach **Disposition kalkulieren** öffnen sich die **Dispositionszeilen** mit den neu ermittelten Artikeln.
3. **Kernablauf.** Für jede neu angelegte Zeile ist die **Akt. geplante Einheit** bereits mit der Einkaufseinheit des Artikels vorbelegt. Der Disponent trägt in **Akt. Dispositionsmenge** die gewünschte Menge ein; die Einheitenspalten **Akt. geplante KG / Meter / Stück** werden – soweit Faktoren vorhanden sind – automatisch mitgeführt.
4. **Abschluss.** Über **Bestellvorschlagszeilen erstellen** werden alle Zeilen mit einer Menge größer null in Bestellvorschlagszeilen überführt, jeweils in der vorbelegten Einheit.

## FAQ und Troubleshooting

### 1. Warum bleiben die Spalten Akt. geplante KG / Meter / Stück leer?
Die Umrechnung greift nur, wenn der **Basiseinheitencode** des Artikels einem der in der **KG Meter Stück Einrichtung** hinterlegten Einheitencodes (KG, Meter oder Stück) entspricht. Ist die Basiseinheit keiner dieser Größen zugeordnet, füllt die App die Spalten nicht.

### 2. Was passiert, wenn auf der Artikelkarte kein Umrechnungsfaktor hinterlegt ist?
Ohne **Theoretische KG pro Meter** bzw. **Theoretische KG pro Stück** fehlt die rechnerische Grundlage. Die betroffene Umrechnung unterbleibt, und die zugehörige Einheitenspalte bleibt ohne Wert.

### 3. Welche Einheit landet in der Bestellvorschlagszeile?
Beim **Bestellvorschlagszeilen erstellen** übernimmt die App die **Akt. geplante Einheit** der Dispositionszeile als **Einheitencode** der Bestellvorschlagszeile. Ändern Sie die Einheit also bereits in den Dispositionszeilen, nicht erst im Bestellvorschlag.

### 4. Warum ist die Akt. geplante Einheit beim Anlegen schon gefüllt?
Beim automatischen Anlegen einer Dispositionszeile setzt die App die **Akt. geplante Einheit** auf die im Artikel als Einkaufseinheit hinterlegte Einheit, damit der Bestellvorschlag ohne weiteres Zutun in der üblichen Einkaufseinheit entsteht.

### 5. Wie hängen Akt. Dispositionsmenge und die Einheitenspalten zusammen?
Alle Werte sind gekoppelt: Eine Änderung an **Akt. Dispositionsmenge** oder an **Akt. geplante KG / Meter / Stück** oder an der **Akt. geplante Einheit** löst eine Neuberechnung der jeweils anderen Werte aus. Maßgeblich für die Bestellung ist die daraus ermittelte **Akt. Dispositionsmenge**.

### 6. Kann ich die Menge weiterhin klassisch in Akt. Dispositionsmenge erfassen?
Ja. Sie können die Menge unverändert in **Akt. Dispositionsmenge** eintragen; die Einheitenspalten werden dann – soweit Faktoren vorhanden sind – automatisch daraus abgeleitet. Die App erzwingt keine Eingabe in KG, Meter oder Stück.

### 7. Warum ändern sich Mengen manchmal automatisch, manchmal erst nach Rückfrage?
Das steuert das Feld **Mengenkonsistenz** auf der Artikelkarte: **Mengen immer ändern** passt Mengen ohne Rückfrage an, **Mengen niemals ändern** verändert nichts automatisch, **Mengenänderung durch Nachfrage** fragt vor jeder Anpassung nach.

### 8. Warum kann ich die Felder Theoretische/Tatsächliche KG pro Meter in den Dispositionszeilen nicht bearbeiten?
Diese Faktoren werden aus den Stammdaten (Artikel bzw. Artikelverfolgungsinformationen) übernommen und nur zur Nachvollziehbarkeit mitgeführt. Sie sind in den Zeilen nicht editierbar; ändern Sie die theoretischen Werte auf der **Artikelkarte**.

### 9. Auf welche Zeilen wirkt die Mengeneingabe?
Die Bestellmenge wird auf Artikel- bzw. Artikelvariantenebene erfasst. Nur auf dieser untersten Ebene sind die Mengen bearbeitbar; übergeordnete Ebenen (Materialart, Eigenschaft) zeigen kumulierte Werte.

### 10. Es werden keine Bestellvorschlagszeilen erzeugt – woran liegt das?
**Bestellvorschlagszeilen erstellen** berücksichtigt nur Zeilen mit einer **Akt. Dispositionsmenge** größer null. Ist keine Menge erfasst – auch nicht mittelbar über eine Einheitenspalte –, entsteht keine Bestellvorschlagszeile.
