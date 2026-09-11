---
title: Anwenderhandbuch m+m Price Calculation
---

# Anwenderhandbuch m+m Price Calculation

## Einleitung

Das Modul **m+m - Preisfindung** ergänzt Microsoft Dynamics 365 Business Central um eine zusätzliche Preisberechnungsmethode, mit der Verkaufs- und Einkaufspreise nicht je Verkaufs- bzw. Einkaufseinheit, sondern je frei definierbarer **Berechnungseinheit** ermittelt werden. Typischer Anwendungsfall: Ein Artikel wird in „Stück" oder „kg" verkauft, der Preis soll aber pro Liter, pro Meter oder in einer Staffel wie „100/Liter" angegeben und automatisch in den Stückpreis der Belegzeile umgerechnet werden.

Das Modul stellt dazu zwei Stammdatenlisten bereit — die **VK-Preisberechnungsliste** und die **EK-Preisberechnungsliste** — in denen je Kombination aus Debitor bzw. Kreditor, Art (Artikel, Artikelgruppe, Sachkonto, Zu-/Abschlag), Einheit und Berechnungseinheit festgelegt wird, wie umgerechnet wird. In den Verkaufs- und Einkaufsbelegen sowie in den Preislisten erscheinen dann die zusätzlichen Felder **Berechnungseinheit**, **Berechnete Menge** und **Berechnungspreis**.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender** im Verkauf und Einkauf, die täglich Belegzeilen erfassen und Preise pflegen — sie wählen in Angebot, Auftrag, Bestellung, Rechnung und Preisliste die passende Berechnungseinheit und arbeiten mit dem daraus ermittelten Berechnungspreis. **Sekundär** ist das Handbuch für Administratoren und Schlüsselanwender relevant, die die Preisberechnungsmethode aktivieren, den **Fixen Berechnungspreis** einrichten und die Preisberechnungslisten als Stammdaten pflegen.

**Kurzer Prozessüberblick:** Zuerst aktiviert der Administrator die Preisberechnungsmethode **m+m - Preisfindung** und legt fest, ob der Berechnungspreis fixiert wird. Anschließend pflegt ein Schlüsselanwender die VK-/EK-Preisberechnungslisten. Im Tagesgeschäft wählt der Anwender in der Belegzeile eine Berechnungseinheit; das System ermittelt die passende Preisberechnung, berechnet die berechnete Menge und den Berechnungspreis und schreibt den umgerechneten Stückpreis bzw. Einkaufspreis in die Zeile zurück.

## Schnellstart für Anwender

Der schnellste Weg zu einem berechneten Preis — in der Reihenfolge, in der die Einrichtung dies voraussetzt:

1. **Einrichtung (einmalig, Administrator):** Öffnen Sie über **Suchen** die **Debitoren & Verkauf Einrichtung** und setzen Sie die **Preisberechnungsmethode** auf **m+m - Preisfindung**. Wiederholen Sie dies für den Einkauf in der **Kreditoren & Einkauf Einrichtung**. Entscheiden Sie je Bereich, ob der **Fixer Berechnungspreis** aktiviert wird.
2. **Stammdaten (Schlüsselanwender):** Öffnen Sie über **Suchen** die **VK-Preisberechnungsliste** und legen Sie je Kombination aus **Verkaufsart**, **Art**, **Verkaufseinheit**, **Verkaufsberechnungseinheit** und ggf. **Faktor** eine Zeile an. Für den Einkauf nutzen Sie die **EK-Preisberechnungsliste**.
3. **Belegzeile erfassen (Anwender):** Erfassen Sie im **Verkaufsauftrag** (oder Angebot, Rechnung, Bestellung usw.) eine Zeile mit Artikel und **Menge**.
4. **Berechnungseinheit wählen:** Öffnen Sie im Feld **Berechnungseinheit** der Zeile die Auswahl. Gibt es genau eine passende Preisberechnung, wird sie automatisch übernommen; gibt es mehrere, wählen Sie die gewünschte in der eingeblendeten **VK-Preisberechnungsliste** aus.
5. **Ergebnis prüfen:** Das System füllt **Berechnete Menge** und **Berechnungspreis** und rechnet daraus den **VK-Preis** bzw. **EK-Preis (Direkte Stückkosten)** der Zeile. Sie können den **Berechnungspreis** direkt überschreiben — der Stückpreis wird dann rückwärts neu berechnet.

Es gibt in diesem Modul **keinen eigenen Buchungs- oder Freigabeschritt**: Die Preisfindung wirkt auf die Belegzeile; gebucht und freigegeben wird der Beleg anschließend wie gewohnt über die Standardaktionen von Business Central.

## Einrichtung

Die Einrichtung erfolgt in zwei bestehenden, unternehmensweiten Standard-Einrichtungsseiten von Business Central, die dieses Modul jeweils um ein Feld erweitert. Beide Seiten sind **globale Einzelsätze** (ein Datensatz je Mandant) und werden über **Suchen** geöffnet — für den Verkauf über **Debitoren & Verkauf Einrichtung**, für den Einkauf über **Kreditoren & Einkauf Einrichtung**.

### Preisberechnungsmethode aktivieren

**Einstieg:** Öffnen Sie über **Suchen** die **Debitoren & Verkauf Einrichtung** bzw. die **Kreditoren & Einkauf Einrichtung**.

**Prozess:** Diese Einrichtung nimmt der Administrator einmalig vor der ersten Nutzung vor. Sie entscheidet, ob Business Central beim Ermitteln von Verkaufs- bzw. Einkaufspreisen die Standard-Preisfindung oder die Methode **m+m - Preisfindung** verwendet. Erst mit dieser Methode werden die Berechnungsfelder in Belegen und Preislisten wirksam; sie ist die Voraussetzung für sämtliche Stammdaten und Tagesabläufe in diesem Handbuch (siehe **Stammdaten** und **Tägliche Arbeit in Belegen**).

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Preisberechnungsmethode** | Wenn hier **m+m - Preisfindung** ausgewählt ist, ermittelt Business Central Verkaufs- bzw. Einkaufspreise über die VK-/EK-Preisberechnungsliste dieses Moduls; die Belegzeilen und Preislistenzeilen zeigen dann die Felder **Berechnungseinheit**, **Berechnete Menge** und **Berechnungspreis** und rechnen den Preis je Berechnungseinheit in den Stückpreis um. Bleibt ein anderer Wert eingestellt, arbeitet Business Central mit seiner Standard-Preisfindung und die Zusatzfelder bleiben ohne Wirkung. |

Der Wert **m+m - Preisfindung** ist die durch dieses Modul ergänzte Methode; die übrigen auswählbaren Methoden sind Standard von Business Central und werden hier nicht verändert.

### Fixer Berechnungspreis einrichten

**Einstieg:** Öffnen Sie über **Suchen** die **Debitoren & Verkauf Einrichtung** bzw. die **Kreditoren & Einkauf Einrichtung**. Das Feld **Fixer Berechnungspreis** steht direkt hinter dem Feld **Preisberechnungsmethode**.

**Prozess:** Dieses Kennzeichen setzt der Administrator einmalig je Bereich (Verkauf, Einkauf). Es steuert das Verhalten, wenn ein Anwender in einer Belegzeile die **Berechnungseinheit** wechselt (siehe **Tägliche Arbeit in Belegen**). Die Einrichtung wirkt also nicht auf der Einrichtungsseite selbst, sondern greift später beim Umschalten der Berechnungseinheit in jeder Verkaufs- bzw. Einkaufszeile.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Fixer Berechnungspreis** | Wenn aktiviert, bleibt der zuvor erfasste **Berechnungspreis** einer Belegzeile erhalten, wenn der Anwender die **Berechnungseinheit** der Zeile ändert: Der gemerkte Berechnungspreis wird auf die neue Berechnungseinheit erneut angewendet und der Stückpreis daraus neu bestimmt. Wenn nicht aktiviert, wird der Berechnungspreis beim Wechsel der Berechnungseinheit verworfen und aus dem aktuellen Stückpreis der Zeile neu abgeleitet. Der administrative Vorteil: Bei aktiviertem Kennzeichen behalten manuell festgelegte Berechnungspreise ihren Wert über einen Einheitenwechsel hinweg und müssen nicht erneut eingegeben werden. |

**Abhängigkeit:** Der Fixe Berechnungspreis ist nur relevant, wenn zuvor die **Preisberechnungsmethode** auf **m+m - Preisfindung** gesetzt wurde. Für Verkauf und Einkauf wird das Kennzeichen getrennt gepflegt.

## Stammdaten

Die eigentlichen Berechnungsregeln pflegt ein Schlüsselanwender in zwei Listen, die zugleich Stammdaten und Pflegeoberfläche sind: der **VK-Preisberechnungsliste** und der **EK-Preisberechnungsliste**. Beide werden über **Suchen** geöffnet. Ohne mindestens eine passende Zeile in diesen Listen kann in einer Belegzeile weder eine Berechnungseinheit ausgewählt noch ein Berechnungspreis angezeigt werden.

### VK-Preisberechnungsliste

**Einstieg:** Öffnen Sie über **Suchen** die **VK-Preisberechnungsliste**.

**Prozess:** Diese Stammdaten pflegt der Schlüsselanwender vor der ersten Preisermittlung im Verkauf und danach laufend. Je Zeile wird festgelegt, für welche **Verkaufsart** (Referenzpunkt Debitor/Debitorengruppe), für welche **Art** von Position (Artikel, Sachkonto, Zu-/Abschlag …) und für welche Einheitenkombination eine Preisberechnung gilt. Die hier gepflegten Zeilen werden im Tagesgeschäft über das Feld **Berechnungseinheit** der Verkaufszeile abgerufen (siehe **Tägliche Arbeit in Belegen**) und dienen auch als Grundlage für die Berechnungsspalten in den VK-Preislisten (siehe **Berechnung in Preislisten**).

| Feld | Erläuterung |
|------|-------------|
| **Verkaufsart** | Bestimmt den Bezugspunkt der Berechnung. **Debitor:** Wenn ausgewählt, gilt die Zeile für einen bestimmten Kunden; das Feld **Debitoren Nr.** wird pflichtig. **Alle Debitoren:** Wenn ausgewählt, gilt die Zeile kundenübergreifend und **Debitoren Nr.** entfällt. **Debitorenpreisgruppe:** Wenn ausgewählt, gilt die Zeile für eine Preisgruppe; das Feld **Debitorenpreisgruppe** wird pflichtig. |
| **Debitoren Nr.** | Wenn die Verkaufsart **Debitor** ist, legt dieses Feld den konkreten Kunden fest, für den die Berechnung greift; nur dann ist das Feld bearbeitbar. Bei anderen Verkaufsarten wird es beim Wechsel geleert. |
| **Debitorenpreisgruppe** | Wenn die Verkaufsart **Debitorenpreisgruppe** ist, legt dieses Feld die Preisgruppe fest, für deren Kunden die Berechnung gilt; nur dann ist das Feld bearbeitbar. |
| **Art** | Bestimmt, auf welche Positionsart die Berechnung angewendet wird und welche Positionskennung (**Nr.** oder **Artikelgruppe**) pflichtig ist. **Artikel:** gilt für einen konkreten Artikel (**Nr.** pflichtig). **Artikelgruppe:** gilt für eine Serviceartikelgruppe (**Artikelgruppe** pflichtig). **Alle Artikel:** gilt für alle Artikel ohne weitere Kennung. **Zu-/Abschlag (Artikel):** gilt für einen bestimmten Artikel-Zu-/Abschlag (**Nr.** pflichtig, **Faktor** pflichtig). **Alle Zu-/Abschläge:** gilt für alle Artikel-Zu-/Abschläge (**Faktor** pflichtig). **Sachkonto:** gilt für ein bestimmtes Sachkonto (**Nr.** pflichtig, **Faktor** pflichtig). **Alle Sachkonten:** gilt für alle Sachkonten (**Faktor** pflichtig). |
| **Artikelgruppe** | Wenn die **Art** auf **Artikelgruppe** steht, legt dieses Feld die Serviceartikelgruppe fest, für die die Berechnung gilt. Bei anderen Arten wird es beim Wechsel geleert. |
| **Nr.** | Kennung der Position gemäß gewählter **Art**: bei **Artikel** die Artikelnummer, bei **Zu-/Abschlag (Artikel)** die Nummer des Artikel-Zu-/Abschlags, bei **Sachkonto** die Sachkontonummer. Wird beim Wechsel der Art geleert, sofern die neue Art keine Positionsnummer verlangt. |
| **Variantencode** | Schränkt die Berechnung optional auf eine bestimmte Artikelvariante ein. Bleibt das Feld leer, gilt die Zeile variantenübergreifend; wird bei der Suche in der Belegzeile keine variantengenaue Zeile gefunden, greift die variantenneutrale Zeile. |
| **Verkaufseinheit** | Basismengeneinheit der Verkaufszeile, für die die Berechnung gilt (Pflichtfeld). Nur wenn diese Einheit mit der Einheit der Belegzeile übereinstimmt, wird die Zeile als passend erkannt. |
| **Verkaufsberechnungseinheit** | Einheit, in der der Preis angegeben und berechnet wird (Pflichtfeld) — z. B. „L" (Liter), wenn der Preis pro Liter geführt wird, obwohl in Stück verkauft wird. Wird der Anwender in der Belegzeile diese Berechnungseinheit auswählt, rechnet das System zwischen Verkaufseinheit und Berechnungseinheit um. |
| **Faktor** | Zusätzlicher Teiler zur Darstellung von Staffeln wie „100/Liter". Wenn gesetzt, wird die berechnete Menge zusätzlich durch den Faktor geteilt; für **Zu-/Abschlag** und **Sachkonto** ist der Faktor pflichtig. Das Setzen des Faktors leert die **Berechnungseinheit (Basis)** und umgekehrt: Es wird entweder mit Faktor **oder** mit Berechnungseinheit (Basis) gerechnet. |
| **Berechnungseinheit (Basis)** | Basiskennzahl, auf die bei artikel- bzw. gruppenbezogenen Zeilen ohne Faktor umgerechnet wird. Wenn gefüllt, wird die berechnete Menge über die Mengeneinheiten-Umrechnung dieser Basis-Einheit bestimmt; das Feld ist pflichtig, sobald ein **Faktor** ungleich 0 fehlt und die Art nicht Zu-/Abschlag/Sachkonto ist. Faktor und Berechnungseinheit (Basis) schließen sich gegenseitig aus. |
| **Standard** | Wenn aktiviert, wird diese Zeile in der Belegzeile automatisch herangezogen, sobald zur Kombination genau eine Standardzeile existiert — der Anwender muss die Berechnungseinheit dann nicht manuell wählen. Pro Kombination aus Artikel und Kunde ist nur **eine** Standardzeile zulässig; beim Versuch, eine zweite als Standard zu markieren, meldet das System **„Für diese Kombination von Artikel und Kunde ist nur ein Standard zulässig"** und setzt das Kennzeichen zurück. |

**Validierungen (aus dem Programmablauf):** Beim Anlegen werden **Verkaufseinheit** und **Verkaufsberechnungseinheit** geprüft; je nach **Verkaufsart** ist **Debitoren Nr.** oder **Debitorenpreisgruppe** pflichtig; je nach **Art** ist **Nr.** oder **Artikelgruppe** pflichtig. Eine Zeile lässt sich nicht löschen, solange sie in einer Preislistenzeile verwendet wird — das System meldet dann, dass ein abhängiger Preislisteneintrag existiert.

### EK-Preisberechnungsliste

**Einstieg:** Öffnen Sie über **Suchen** die **EK-Preisberechnungsliste**.

**Prozess:** Analog zur Verkaufsseite pflegt der Schlüsselanwender hier die Berechnungsregeln für den Einkauf, bezogen auf Kreditoren. Die Zeilen werden im Tagesgeschäft über das Feld **Berechnungseinheit** der Einkaufszeile abgerufen und liefern die Berechnungsspalten der EK-Preislisten.

| Feld | Erläuterung |
|------|-------------|
| **Einkaufsart** | Bestimmt den Bezugspunkt der Berechnung. **Kreditor:** Wenn ausgewählt, gilt die Zeile für einen bestimmten Lieferanten; **Kreditoren Nr.** wird pflichtig. **Alle Kreditoren:** Wenn ausgewählt, gilt die Zeile lieferantenübergreifend und **Kreditoren Nr.** entfällt. |
| **Kreditoren Nr.** | Wenn die Einkaufsart **Kreditor** ist, legt dieses Feld den konkreten Lieferanten fest; nur dann bearbeitbar. Beim Wechsel auf eine andere Einkaufsart wird es geleert. |
| **Art** | Wie in der VK-Preisberechnungsliste: **Artikel** (Nr. pflichtig), **Artikelgruppe** (Artikelgruppe pflichtig), **Alle Artikel**, **Zu-/Abschlag (Artikel)** (Nr. + Faktor pflichtig), **Alle Zu-/Abschläge** (Faktor pflichtig), **Sachkonto** (Nr. + Faktor pflichtig), **Alle Sachkonten** (Faktor pflichtig). Die Auswahl steuert, welche Positionskennung erfasst werden muss. |
| **Artikelgruppe** | Serviceartikelgruppe, für die die Berechnung gilt, wenn die **Art** auf **Artikelgruppe** steht. |
| **Nr.** | Positionskennung gemäß **Art**: Artikelnummer, Nummer des Artikel-Zu-/Abschlags oder Sachkontonummer. |
| **Variantencode** | Optionale Einschränkung auf eine Artikelvariante; leer = variantenübergreifend. |
| **Einkaufseinheit** | Basismengeneinheit der Einkaufszeile, für die die Berechnung gilt (Pflichtfeld). |
| **Einkaufsberechnungseinheit** | Einheit, in der der Einkaufspreis angegeben und berechnet wird (Pflichtfeld). |
| **Faktor** | Zusätzlicher Teiler für Staffeln (z. B. „100/Liter"); für **Zu-/Abschlag** und **Sachkonto** pflichtig. Schließt sich mit **Berechnungseinheit (Basis)** gegenseitig aus. |
| **Berechnungseinheit (Basis)** | Basiskennzahl für die Umrechnung ohne Faktor bei artikel-/gruppenbezogenen Zeilen; pflichtig, wenn kein Faktor gesetzt ist und die Art nicht Zu-/Abschlag/Sachkonto ist. |
| **Standard** | Wenn aktiviert, wird die Zeile in der Einkaufszeile automatisch herangezogen, sofern genau eine Standardzeile zur Kombination existiert. Pro Kombination aus Artikel und Lieferant ist nur eine Standardzeile zulässig; andernfalls meldet das System **„Für diese Kombination von Artikel und Lieferant ist nur ein Standard zulässig"**. |

Die berechnete Menge und der Berechnungspreis entstehen erst in der Belegzeile bzw. Preislistenzeile — die Preisberechnungslisten legen ausschließlich die Regeln fest.

### Erläuterung der Berechnungsschritte

Damit die Stammdaten korrekt gepflegt werden, hier der vom System angewandte Rechenweg (aus dem Programmablauf) am Verkaufsbeispiel; für den Einkauf gilt er sinngemäß mit Direkten Stückkosten statt Stückpreis:

- **Berechnete Menge ohne Faktor:** Die **Menge** der Zeile (umgerechnet in Basiseinheiten) wird durch die Menge pro Mengeneinheit der **Verkaufsberechnungseinheit** bzw. der **Berechnungseinheit (Basis)** geteilt. Beispiel: Menge 10 bei einer Umrechnung von 100 je Einheit ergibt eine berechnete Menge von 0,1.
- **Berechnungspreis:** Er wird ermittelt, indem der Stückpreis mit der Menge multipliziert und durch die berechnete Menge geteilt wird. Beispiel: Stückpreis 500 und Menge 10 ergeben bei berechneter Menge 0,1 einen Berechnungspreis von (500 × 10) / 0,1 = 50.000 je Berechnungseinheit.
- **Berechnete Menge mit Faktor:** Ist ein **Faktor** gesetzt, wird die zuvor ermittelte berechnete Menge zusätzlich durch den Faktor geteilt. Beispiel: 0,1 geteilt durch Faktor 100 ergibt eine endgültige berechnete Menge von 0,001.
- **Rückrechnung:** Überschreibt der Anwender den **Berechnungspreis** direkt, wird umgekehrt der **Stückpreis** aus Berechnungspreis und berechneter Menge neu bestimmt.

## Berechnung in Preislisten

Zusätzlich zur direkten Erfassung in Belegen lässt sich die Preisberechnung bereits in den **Preislisten** hinterlegen. Dieses Modul erweitert die Zeilen der Verkaufs- und Einkaufspreislisten um Berechnungsspalten und blendet die Standardfelder **Arbeitstypencode**, **Mindestmenge** und (im Verkauf) **Kostenfaktor** aus, da sie mit der Berechnung nicht kombiniert werden.

**Einstieg:** Öffnen Sie die gewünschte **Preisliste** und arbeiten Sie in den **Zeilen**. Die Berechnungsspalten stehen sowohl in den bearbeitbaren Preislistenzeilen als auch in der Übersicht der Preislistenzeilen zur Verfügung.

**Prozess:** Der Schlüsselanwender pflegt die Berechnung einmalig in der Preisliste; die Zeilen wirken anschließend automatisch, wenn ein Beleg über die Standard-Preisfindung mit einer solchen Preislistenzeile bepreist wird. Voraussetzung ist auch hier die aktivierte Methode **m+m - Preisfindung** (siehe **Einrichtung**).

| Feld | Erläuterung |
|------|-------------|
| **Verkaufsart** / **Einkaufsart** | Bestimmt den Bezugspunkt der Berechnungszeile (Debitor/Alle Debitoren/Debitorenpreisgruppe bzw. Kreditor/Alle Kreditoren). Wenn gesetzt, sucht das System die passende VK-/EK-Preisberechnung anhand dieses Referenzpunkts. |
| **Debitoren Nr.** / **Kreditoren Nr.** | Konkreter Kunde bzw. Lieferant, wenn die Verkaufs-/Einkaufsart auf **Debitor** bzw. **Kreditor** steht. Beim Wechsel der Art wird das Feld geleert. |
| **Debitorenname** / **Kreditorenname** | Anzeigefeld: zeigt den Namen des in der Zeile hinterlegten Debitors bzw. Kreditors zur Kontrolle an; nicht bearbeitbar. |
| **Debitorenpreisgruppe** | Preisgruppe, wenn die Verkaufsart auf **Debitorenpreisgruppe** steht. |
| **Artikelgruppe** | Schränkt die Berechnungszeile auf eine Serviceartikelgruppe ein. |
| **Berechnungseinheit** | Einheit, in der der Preis der Preislistenzeile berechnet wird. Über die Auswahl (Aufriss) im Feld sucht das System passende Preisberechnungen; existiert keine, meldet es **„Es sind keine passenden VK-Preisberechnungen für die aktuelle Zeile vorhanden."** (bzw. die EK-Variante). Nach Auswahl wird der Bezug zur Preisberechnung gesetzt und der Preis daraus abgeleitet. |
| **Berechnungspreis** | Preis je Berechnungseinheit für die Preislistenzeile. Wenn gefüllt, wird der **VK-Preis** bzw. die **Direkten Stückkosten** der Preislistenzeile daraus umgerechnet; umgekehrt wird bei Änderung des VK-Preises der Berechnungspreis nachgeführt. |
| **Preisberechnung** | Interner Bezug der Preislistenzeile auf die verwendete VK-/EK-Preisberechnung; wird durch die Auswahl der Berechnungseinheit gesetzt und dient der Rückverfolgung. |

Die Berechnungseinheit lässt sich nur auswählen und ein Preis nur anzeigen, wenn in der VK-/EK-Preisberechnungsliste eine Einrichtung für die Kombination vorhanden ist.

## Tägliche Arbeit in Belegen

Im Tagesgeschäft erweitert das Modul die Zeilen der Verkaufs- und Einkaufsbelege um die Felder **Berechnungseinheit**, **Berechnete Menge** und **Berechnungspreis**. Betroffen sind auf der Verkaufsseite Angebot, Auftrag, Rechnung, Gutschrift, Rücksendung und Rahmenauftrag, auf der Einkaufsseite Anfrage/Angebot, Bestellung, Rechnung, Gutschrift, Reklamation und Rahmenbestellung. Alle Berechnungsfelder liegen auf der **Zeile** (nicht im Kopf) und stehen nur bei aktivierter Methode **m+m - Preisfindung** zur Verfügung (siehe **Einrichtung**).

### Berechnungseinheit auswählen und Preis ermitteln

1. Erfassen Sie die Belegzeile mit **Art**, **Nr.** und **Menge** wie gewohnt.
2. **Automatische Übernahme:** Existiert in der VK-/EK-Preisberechnungsliste genau eine als **Standard** markierte, passende Zeile, füllt das System die **Berechnungseinheit** automatisch, sobald die Zeile bewertet wird.
3. **Manuelle Auswahl:** Andernfalls öffnen Sie im Feld **Berechnungseinheit** die Auswahl. Gibt es mehrere passende Preisberechnungen, blendet das System die **VK-Preisberechnungsliste** (bzw. **EK-Preisberechnungsliste**) zur Auswahl ein; bei genau einer Zeile wird diese direkt übernommen. Findet das System keine passende Zeile, erscheint die Meldung **„Es sind keine passenden VK-Preisberechnungen für die aktuelle Zeile vorhanden."**
4. Das System füllt daraufhin **Berechnete Menge** und **Berechnungspreis** und rechnet den **VK-Preis** bzw. die **Direkten Stückkosten** der Zeile um.
5. **Berechnungspreis übersteuern:** Sie können den **Berechnungspreis** direkt eingeben (das setzt eine gefüllte Berechnungseinheit voraus, sonst meldet das System **„Geben Sie eine Berechnungseinheit ein, um das Feld Berechnungspreis ausfüllen zu können."**). Der Stückpreis wird dann rückwärts aus Ihrem Berechnungspreis neu bestimmt.

**Zusammenspiel mit dem Fixen Berechnungspreis:** Wechseln Sie die **Berechnungseinheit** einer Zeile erneut, hängt das Verhalten vom Einrichtungskennzeichen **Fixer Berechnungspreis** ab (siehe **Einrichtung**): Ist es aktiviert, wird der bisher erfasste Berechnungspreis gemerkt und auf die neue Berechnungseinheit angewendet; ist es nicht aktiviert, wird der Berechnungspreis verworfen und aus dem aktuellen Stückpreis neu abgeleitet.

| Feld (Belegzeile) | Erläuterung |
|-------------------|-------------|
| **Berechnungseinheit** | Einheit, in der der Preis dieser Zeile berechnet wird. Über die Auswahl wählen Sie die zutreffende Preisberechnung; die Änderung setzt **Berechnete Menge** und **Berechnungspreis** zurück und ermittelt sie neu. Das Ändern ist nur möglich, solange der Beleg den Status **Offen** hat. |
| **Berechnete Menge** | Aus der Belegmenge und der Umrechnung ermittelte Menge in der Berechnungseinheit; Anzeigefeld, nicht direkt editierbar. Sie ist die Bezugsgröße für den Berechnungspreis. |
| **Berechnungspreis** | Preis je Berechnungseinheit. Wenn Sie ihn eingeben, wird der Stückpreis der Zeile daraus neu berechnet; er ist nur bearbeitbar, wenn eine Berechnungseinheit gesetzt ist, und nur bei Belegstatus **Offen**. |

### Artikelverfolgung und Neuberechnung

Öffnen und schließen Sie in Verkaufs- oder Einkaufsauftragszeilen die **Artikelverfolgungszeilen**, aktualisiert das Modul anschließend automatisch die berechnete Menge und den Preis der Zeile, damit die Preisberechnung zur verfolgten Menge passt. Es ist kein zusätzlicher Schritt durch den Anwender nötig.

## Archiv und gebuchte Belege

Die Berechnungsfelder werden mit dem Beleg archiviert und gebucht und stehen zur Nachverfolgung zur Verfügung — jedoch **schreibgeschützt**, da an einem archivierten oder gebuchten Beleg keine Preise mehr geändert werden.

- **Archivierte Belege:** In den archivierten Verkaufs- und Einkaufsaufträgen sowie -angeboten zeigen die Zeilen **Berechnungseinheit**, **Berechnete Menge** und **Berechnungspreis** in dem Stand, in dem der Beleg archiviert wurde.
- **Gebuchte Belege:** In den gebuchten Verkaufs- und Einkaufsrechnungen sowie -gutschriften zeigen die Zeilen ebenfalls **Berechnungseinheit**, **Berechnete Menge** und **Berechnungspreis** — als Beleg, wie zum Buchungszeitpunkt kalkuliert wurde.

## Berechtigungen

Für die Nutzung des Moduls stellt die Anwendung den Berechtigungssatz **MuM Price Calc. Per** bereit. Er legt fest, welche Aktionen Anwender in der Preisfindung ausführen dürfen: Er gewährt Lese- und Schreibzugriff (Anzeigen, Anlegen, Ändern, Löschen) auf die Tabellen der **VK-Preisberechnung** und **EK-Preisberechnung** sowie die Ausführungsrechte auf die zugehörigen Verarbeitungsobjekte und die beiden Preisberechnungslisten. Der Administrator weist diesen Berechtigungssatz den Anwendern zu, die Preisberechnungslisten pflegen oder in Belegen mit den Berechnungsfeldern arbeiten sollen.

## FAQ und Troubleshooting

### 1. Warum erscheinen die Felder Berechnungseinheit und Berechnungspreis in meinen Belegzeilen nicht?
Die Zusatzfelder wirken nur, wenn in der **Debitoren & Verkauf Einrichtung** bzw. **Kreditoren & Einkauf Einrichtung** die **Preisberechnungsmethode** auf **m+m - Preisfindung** gesetzt ist. Ohne diese Methode arbeitet Business Central mit der Standard-Preisfindung und die Berechnung bleibt ohne Wirkung.

### 2. Warum meldet das System „Es sind keine passenden VK-Preisberechnungen für die aktuelle Zeile vorhanden"?
Für die Kombination aus Debitor/Debitorengruppe, Art, Artikel/Sachkonto, Einheit und ggf. Variante gibt es in der **VK-Preisberechnungsliste** keine passende Zeile. Legen Sie dort eine entsprechende Zeile an oder erweitern Sie eine bestehende über **Alle Debitoren** bzw. **Alle Artikel**, damit die Suche einen Treffer findet.

### 3. Warum kann ich den Berechnungspreis nicht eingeben?
Der **Berechnungspreis** lässt sich nur füllen, wenn zuvor eine **Berechnungseinheit** ausgewählt wurde. Andernfalls meldet das System **„Geben Sie eine Berechnungseinheit ein, um das Feld Berechnungspreis ausfüllen zu können."** Wählen Sie zuerst die Berechnungseinheit.

### 4. Warum ändert sich der Stückpreis, wenn ich den Berechnungspreis überschreibe?
Das ist beabsichtigt: Der **VK-Preis** bzw. die **Direkten Stückkosten** werden aus dem Berechnungspreis und der berechneten Menge rückgerechnet. So können Sie mit dem Preis je Berechnungseinheit arbeiten, ohne den Stückpreis manuell umzurechnen.

### 5. Warum wird beim Wechsel der Berechnungseinheit mal der Berechnungspreis behalten und mal nicht?
Das steuert das Einrichtungskennzeichen **Fixer Berechnungspreis**. Ist es aktiviert, wird der bisherige Berechnungspreis auf die neue Berechnungseinheit angewendet; ist es deaktiviert, wird er verworfen und aus dem aktuellen Stückpreis neu abgeleitet.

### 6. Warum lässt sich eine Zeile in der Preisberechnungsliste nicht löschen?
Eine Preisberechnungszeile kann nicht gelöscht werden, solange sie in einer **Preislistenzeile** verwendet wird. Das System weist auf den abhängigen Preislisteneintrag hin. Entfernen oder ändern Sie zuerst die betreffende Preislistenzeile.

### 7. Warum meldet das System „Für diese Kombination von Artikel und Kunde ist nur ein Standard zulässig"?
Pro Kombination aus Verkaufsart, Kunde, Art, Artikel/Gruppe, Variante und Einheit darf nur **eine** Zeile als **Standard** markiert sein, damit die automatische Übernahme eindeutig ist. Das Kennzeichen wird bei einem zweiten Standard automatisch zurückgesetzt. Im Einkauf gilt dies für die Kombination aus Artikel und Lieferant.

### 8. Wozu dient der Faktor, und warum darf ich Faktor und Berechnungseinheit (Basis) nicht zusammen setzen?
Der **Faktor** stellt Staffeln wie „100/Liter" dar, indem die berechnete Menge zusätzlich durch ihn geteilt wird. **Berechnungseinheit (Basis)** definiert stattdessen eine Basis-Mengeneinheit für die Umrechnung. Beide Wege schließen sich aus: Das Setzen des Faktors leert die Berechnungseinheit (Basis) und umgekehrt.

### 9. Warum wird bei mehreren passenden Berechnungen eine Liste eingeblendet?
Gibt es mehr als eine passende Preisberechnung, kann das System nicht selbst entscheiden und blendet die **VK-**/**EK-Preisberechnungsliste** zur Auswahl ein. Markieren Sie die gewünschte Zeile als **Standard**, wenn sie künftig automatisch übernommen werden soll.

### 10. Warum ändern sich Berechnungsfelder, nachdem ich die Artikelverfolgungszeilen geöffnet habe?
Nach dem Bearbeiten der **Artikelverfolgungszeilen** rechnet das Modul die berechnete Menge und den Preis der Zeile automatisch neu, damit die Preisberechnung zur verfolgten Menge passt. Das ist ein gewollter Abgleich und erfordert keinen weiteren Schritt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Verkauf mit Preis je Liter, obwohl in Stück verkauft wird

**Auslöser:** Ein Kunde bestellt telefonisch 10 Gebinde eines Artikels, der intern in Stück geführt, aber pro Liter kalkuliert wird.

**Einstieg in BC:** Der Anwender öffnet den **Verkaufsauftrag** und erfasst in den **Zeilen** den Artikel mit **Menge** 10.

**Kernablauf:** Existiert eine als **Standard** markierte VK-Preisberechnung, füllt das System die **Berechnungseinheit** (z. B. „L") automatisch. Andernfalls öffnet der Anwender im Feld **Berechnungseinheit** die Auswahl und wählt die passende Zeile aus der eingeblendeten **VK-Preisberechnungsliste**. Das System ermittelt die **Berechnete Menge** über die Mengeneinheiten-Umrechnung und setzt den **Berechnungspreis** je Liter; daraus wird der **VK-Preis** der Zeile bestimmt. Der Anwender kann den Berechnungspreis je Liter direkt anpassen — der Stückpreis wird dann neu berechnet.

**Abschluss:** Der Auftrag wird anschließend wie gewohnt über die Standardaktionen von Business Central weiterverarbeitet und gebucht; die Berechnungsfelder erscheinen schreibgeschützt in der gebuchten Rechnung.

### Anwendungsfall 2: Verkaufspreis erst in der Rechnung festlegen

**Auslöser:** Der endgültige Verkaufspreis steht erst bei Rechnungsstellung fest und soll nicht bereits im Auftrag fixiert werden.

**Einstieg in BC:** Der Anwender öffnet die **Verkaufsrechnung** und arbeitet in den **Zeilen**.

**Kernablauf:** In der Rechnungszeile wählt der Anwender im Feld **Berechnungseinheit** die zutreffende Preisberechnung und gibt den **Berechnungspreis** je Berechnungseinheit ein. Das System rechnet daraus den **VK-Preis** der Zeile. Ist in der **Debitoren & Verkauf Einrichtung** der **Fixer Berechnungspreis** aktiviert, bleibt ein einmal erfasster Berechnungspreis auch dann erhalten, wenn die Berechnungseinheit später noch einmal gewechselt wird.

**Abschluss:** Die Rechnung wird über die Standardaktionen gebucht; **Berechnungseinheit**, **Berechnete Menge** und **Berechnungspreis** werden mit der gebuchten Rechnung dokumentiert.

### Anwendungsfall 3: Einkaufspreis in Staffel „100/Liter"

**Auslöser:** Ein Lieferant nennt seinen Preis je 100 Liter, während der Artikel in einer anderen Einheit bestellt wird.

**Einstieg in BC:** Der Schlüsselanwender hinterlegt in der **EK-Preisberechnungsliste** eine Zeile mit **Einkaufsart** = **Kreditor**, der passenden **Einkaufseinheit**, der **Einkaufsberechnungseinheit** und einem **Faktor** von 100 (in Kombination mit der **Berechnungseinheit (Basis)** „L"). Anschließend öffnet der Einkäufer die **Einkaufsbestellung**.

**Kernablauf:** In der Bestellzeile wählt der Einkäufer die **Berechnungseinheit**; das System teilt die berechnete Menge zusätzlich durch den Faktor 100 und ermittelt so den Preis je 100 Liter. Aus **Berechnungspreis** und **Berechneter Menge** entstehen die **Direkten Stückkosten** der Zeile.

**Abschluss:** Die Bestellung wird über die Standardaktionen von Business Central weiterverarbeitet; die Berechnungsfelder stehen in gebuchten und archivierten Einkaufsbelegen zur Nachvollziehbarkeit bereit.
