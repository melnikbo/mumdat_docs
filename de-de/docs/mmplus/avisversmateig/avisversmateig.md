---
title: Anwenderhandbuch m+m Logistic Management with Material Properties
---

# Anwenderhandbuch m+m Logistic Management with Material Properties

## Einleitung

Die Erweiterung **m+m Logistic Management with Material Properties** verbindet zwei bestehende m+m-Module miteinander: die logistische **Avisierung** (Versand- und Wareneingangsplanung) und die **Materialeigenschaften** (Eigenschaften je Charge, Artikel und Materialart). Sie fügt der Maske **Artikelverfolgungszuordnungszeilen** eine InfoBox hinzu, in der die **Materialeigenschaften der ausgewählten Charge** angezeigt und – sofern gewünscht – direkt bearbeitet werden können.

Der fachliche Nutzen: Während ein Anwender einer Avisierungszeile Chargen zuordnet, sieht er ohne Seitenwechsel, welche Eigenschaften (z. B. Prüfwerte, Abmessungen, Qualitätsmerkmale) an der jeweiligen Charge hinterlegt sind. So lässt sich die richtige Charge anhand ihrer Materialeigenschaften auswählen, statt die Chargennr. isoliert zu betrachten.

**Zielgruppe:** Primär **operative Anwender** in Wareneingang, Versand und Logistik, die täglich Avisierungen bearbeiten und den Zeilen Chargen zuordnen. Sekundär **Administratoren und Stammdatenverantwortliche**, welche die Materialeigenschaften einrichten und den Artikeln eine Materialart zuweisen, damit an den Chargen überhaupt Eigenschaften zur Verfügung stehen.

**Kurzer Prozessüberblick:** Der Administrator aktiviert die **Materialeigenschaften Einrichtung**, legt **Materialarten** mit **Eigenschaften** an und weist den Artikeln über den **Materialartencode** eine Materialart zu. Erhalten Chargen dadurch Eigenschaften, zeigt die InfoBox diese anschließend im Dialog **Artikelverfolgungszuordnungszeilen** an, sobald ein Anwender dort eine Charge auswählt.

Diese Erweiterung besitzt selbst **keine eigene Einrichtungs- oder Stammdatenseite**. Sie nutzt die Seiten der Module m+m Logistic Management und m+m Material Properties. Damit der Anwender die Maske vollständig konfigurieren und bedienen kann, sind die zugehörigen Voraussetzungen in diesem Handbuch mitdokumentiert.

## Schnellstart für Anwender

Der Schnellstart folgt der Abhängigkeitsreihenfolge: zuerst die einmalige Einrichtung, dann die Stammdaten, danach die tägliche Arbeit im Beleg.

1. **Voraussetzung prüfen (einmalig, Administrator):** In der Seite **Materialeigenschaften Einrichtung** ist die Materialeigenschaftsverwaltung aktiviert. Wenn die Einrichtung fehlt, stehen an den Chargen keine Eigenschaften bereit und die InfoBox bleibt leer.
2. **Materialart und Eigenschaften anlegen (Stammdaten, Administrator):** In **Materialarten** eine Materialart anlegen und ihr über die **Materialartenkarte** die gewünschten **Eigenschaften** zuordnen.
3. **Materialart am Artikel setzen (Stammdaten):** Auf der **Artikelkarte** im Feld **Materialartencode** die Materialart hinterlegen. Wenn gesetzt, erben die Chargen dieses Artikels die Eigenschaften der Materialart.
4. **Beleg öffnen (tägliche Arbeit):** Die **Avisierung** öffnen und in der Zeile über die Aktion **Zeile → Artikelverfolgungszuordnungszeilen** den Zuordnungsdialog aufrufen.
5. **Charge zuordnen:** Über **&Einträge auswählen** oder **Charge-Nr. zuordnen** die **Chargennr.** setzen und **Menge für Zuweisung** eintragen.
6. **Eigenschaften lesen/bearbeiten:** Die InfoBox **Eigenschaften** zeigt zur markierten Zeile die Materialeigenschaften der Charge. Bei Bedarf den **Wert** direkt in der InfoBox ändern.
7. **Abschließen:** Den Dialog mit **OK** schließen. Die Zuordnung wird gespeichert; geänderte Eigenschaftswerte werden an der Charge (Chargennr.-Information) übernommen.

## Einrichtung

Da die Erweiterung selbst keine Einrichtungsseite mitbringt, beschränkt sich die Einrichtung auf **eine Voraussetzung** aus dem Modul m+m Material Properties, die aktiv sein muss, damit die InfoBox Daten anzeigt.

### Materialeigenschaften für die Artikelverfolgung einrichten

**Prozessintro:** Diese Einrichtung nimmt der **Administrator** einmalig **vor der ersten Nutzung** vor. Sie ist die Grundlage dafür, dass die InfoBox in der Maske **Artikelverfolgungszuordnungszeilen** (siehe Kapitel *Tägliche Arbeit*) überhaupt Eigenschaften zur Charge anzeigt. Die Kette verläuft von der zentralen Einrichtung über die Stammdaten bis zur Aktion des Anwenders im Beleg.

**Einstieg:** Öffnen Sie die Seite **Materialeigenschaften Einrichtung** über **Suchen** (es handelt sich um eine unternehmensweite Einrichtungsseite ohne übergeordnete Belegseite).

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Zuerst** aktivieren Sie in der Seite **Materialeigenschaften Einrichtung** die Materialeigenschaftsverwaltung. Wenn die Einrichtung vorhanden und aktiv ist, dann werden beim Anlegen und Fortschreiben von Chargen deren Eigenschaften geführt und stehen später in der InfoBox zur Verfügung; ohne aktive Einrichtung bleibt die InfoBox leer.
2. **Danach** legen Sie die **Materialarten** an und ordnen jeder Materialart über die **Materialartenkarte** ihre **Eigenschaften** zu (siehe Kapitel *Stammdaten*). Wenn eine Materialart Eigenschaften besitzt, dann erben Artikel und Chargen dieser Materialart genau diese Eigenschaften.
3. **Anschließend** setzen Sie auf der **Artikelkarte** den **Materialartencode** (siehe Kapitel *Stammdaten*). Wenn ein Artikel eine Materialart trägt, dann werden für seine Chargen die passenden Eigenschaftszeilen erzeugt.
4. **Schließlich** öffnet der Anwender im Tagesablauf die **Artikelverfolgungszuordnungszeilen** und wählt eine Chargenzeile aus. Wenn eine Charge markiert ist, dann zeigt die InfoBox **Eigenschaften** die Materialeigenschaften genau dieser Charge an (operative Schließung der Kette; siehe Kapitel *Tägliche Arbeit*).

| Einrichtung | Erläuterung |
|---|---|
| **Materialeigenschaften Einrichtung** (unternehmensweit, einmalig) | Wenn diese Einrichtung aktiv ist, dann werden Materialeigenschaften unternehmensweit geführt und in nachgelagerten Masken – darunter die InfoBox der Artikelverfolgungszuordnung – angezeigt; fehlt sie, dann stehen dem Anwender in der Zuordnungsmaske keine Eigenschaften zur Verfügung. |

**Abhängigkeitshinweis:** Die InfoBox zeigt nur dann Eigenschaften, wenn die Charge über die obige Kette Eigenschaften erhalten hat. Fehlt an einem Artikel der **Materialartencode**, bleibt die InfoBox für dessen Chargen leer.

Für diese Erweiterung ist allein die **Aktivierung** der Materialeigenschaftsverwaltung als Voraussetzung maßgeblich. Die detaillierte Feldpflege der Materialarten und Eigenschaften nehmen Sie in den Stammdaten vor (siehe folgendes Kapitel).

## Stammdaten

Die für die InfoBox relevanten Stammdaten werden im Modul m+m Material Properties gepflegt. Zwei Stammdatensurfaces steuern, welche Eigenschaften der Anwender später in der Zuordnungsmaske sieht.

### Materialarten und Eigenschaften

**Prozessintro:** Der **Stammdatenverantwortliche** legt Materialarten **vor der ersten Nutzung** an und ordnet ihnen Eigenschaften zu. Die hier gepflegten Eigenschaften bilden die Vorlage, die später an Artikel und Chargen vererbt wird und in der InfoBox der Maske **Artikelverfolgungszuordnungszeilen** erscheint.

**Einstieg:** Öffnen Sie die Liste **Materialarten**; wählen Sie eine Zeile und öffnen Sie über die Aktion die **Materialartenkarte**. Dort pflegen Sie die zugeordneten **Eigenschaften**.

| Feld | Erläuterung |
|---|---|
| **Eigenschaftscode** | Wenn Sie einer Materialart einen Eigenschaftscode zuordnen, dann steht diese Eigenschaft anschließend an allen Artikeln und Chargen dieser Materialart zur Verfügung und wird in der InfoBox als Zeile angezeigt. |
| **Eigenschaftsname** | Wenn ein Eigenschaftsname gepflegt ist, dann erscheint dieser Klartext als Bezeichnung der Eigenschaftszeile in der InfoBox, sodass der Anwender die Eigenschaft ohne Codekenntnis erkennt. |
| **Standardwert** | Wenn Sie einen Standardwert hinterlegen, dann wird dieser Wert als Vorschlag übernommen, solange an der konkreten Charge kein abweichender Wert erfasst ist; weicht der Wert der Charge vom Standardwert ab, hebt die InfoBox den Wert farblich hervor. |
| **Einheit** | Wenn eine Einheit gepflegt ist, dann wird der Eigenschaftswert in der InfoBox mit dieser Maßeinheit interpretiert und angezeigt, sodass der Anwender Werte fachlich richtig einordnet. |
| **Anzeigereihenfolge** | Wenn Sie eine Anzeigereihenfolge vergeben, dann werden die Eigenschaften in der InfoBox genau in dieser Reihenfolge sortiert; so stehen die wichtigsten Merkmale oben. |

**Validierungshinweis:** Nur Eigenschaften, die einer Materialart zugeordnet sind, werden an deren Artikel und Chargen vererbt. Ohne Zuordnung erzeugt das System für die Charge keine Eigenschaftszeile.

### Materialart am Artikel (Artikelkarte)

**Prozessintro:** Der **Stammdatenverantwortliche** verknüpft jeden relevanten Artikel mit einer Materialart. Erst diese Verknüpfung sorgt dafür, dass die Chargen des Artikels Eigenschaften erhalten, die der Anwender in der Zuordnungsmaske sieht.

**Einstieg:** Öffnen Sie die Artikelliste und darin die **Artikelkarte** des Artikels.

| Feld | Erläuterung |
|---|---|
| **Materialartencode** | Wenn Sie am Artikel einen Materialartencode setzen, dann übernehmen die Chargen dieses Artikels die Eigenschaften der zugeordneten Materialart und die InfoBox der Artikelverfolgungszuordnung zeigt diese an; bleibt das Feld leer, dann besitzt der Artikel keine Materialeigenschaften und die InfoBox bleibt für seine Chargen leer. |

**Querverweis:** Die hier gesetzte Materialart konsumiert der Anwender im Kapitel *Tägliche Arbeit* – die InfoBox in der Maske **Artikelverfolgungszuordnungszeilen** greift auf genau diese Eigenschaften zu.

## Tägliche Arbeit: Chargenzuordnung mit Materialeigenschaften

Dies ist die Kernfunktion der Erweiterung. Die Maske **Artikelverfolgungszuordnungszeilen** ist ein modaler Dialog, den der Anwender aus einem Logistikbeleg heraus öffnet, um den Belegzeilen Chargen bzw. Seriennummern zuzuordnen. Die Erweiterung ergänzt diesen Dialog um die InfoBox **Eigenschaften**.

**Steuernde Einrichtung/Stammdaten:** Welche Eigenschaften die InfoBox anzeigt, wird nicht in diesem Dialog konfiguriert, sondern über die Seiten **Materialeigenschaften Einrichtung**, **Materialarten**/**Materialartenkarte** und das Feld **Materialartencode** auf der **Artikelkarte** (siehe Kapitel *Einrichtung* und *Stammdaten*). Ist an der Charge keine Eigenschaft hinterlegt, bleibt die InfoBox leer.

### Einstieg in die Maske

**Einstieg:** Öffnen Sie die **Avisierung** (Beleg). Markieren Sie in den Belegzeilen die betreffende Zeile und öffnen Sie über die Aktion **Zeile → Artikelverfolgungszuordnungszeilen** den modalen Zuordnungsdialog. Die Maske ist kein über **Suchen** aufrufbarer Menüpunkt; sie wird ausschließlich aus der Belegzeile heraus geöffnet.

### Kopfbereich der Maske

| Feld | Erläuterung |
|---|---|
| **Menge für Zuweisung:** | Zeigt die Gesamtmenge, die der Belegzeile zugeordnet werden muss. Wenn dieser Wert größer als die bereits zugewiesene Menge ist, dann sind noch Chargen zu erfassen. |
| **Bereits zugewiesene Menge:** | Zeigt die Summe der bereits über Chargenzeilen zugeordneten Mengen. Wenn dieser Wert der Menge für Zuweisung entspricht, dann ist die Zeile vollständig zugeordnet. |
| **Undefinierte Menge:** | Zeigt die noch nicht zugeordnete Restmenge (Menge für Zuweisung abzüglich bereits zugewiesener Menge). Wenn hier ein Wert ungleich null steht, dann fehlt noch eine Chargenzuordnung; das System lässt keine Zuordnung über die undefinierte Menge hinaus zu. |

### Zeilenbereich der Maske

| Feld | Erläuterung |
|---|---|
| **Chargennr.** | Wenn Sie eine Chargennr. eintragen oder über die Auswahl zuordnen, dann wird die Menge dieser Zeile dieser Charge zugeordnet und die InfoBox zeigt die Eigenschaften genau dieser Charge; das Feld ist nur editierbar, wenn der Artikel chargenpflichtig ist. |
| **Seriennr.** | Wenn Sie eine Seriennr. erfassen, dann wird die Zuordnung auf diese Seriennummer bezogen; das Feld ist nur editierbar, wenn der Artikel seriennummernpflichtig ist. |
| **Menge für Zuweisung** | Wenn Sie hier eine Menge eintragen, dann wird die bereits zugewiesene und die undefinierte Menge im Kopf sofort neu berechnet; die Eingabe darf die undefinierte Menge nicht überschreiten. |

### Aktionen der Maske

| Aktionsname | Erläuterung |
|---|---|
| **&Einträge auswählen** | Wenn Sie diese Aktion ausführen, dann öffnet sich eine Übersicht der verfügbaren Chargen bzw. Seriennummern mit ihren zuweisbaren Mengen; die dort gewählten Einträge werden als Zeilen in die Zuordnung übernommen. |
| **Charge-Nr. zuordnen** | Wenn Sie diese Aktion ausführen, dann vergibt das System der aktuellen bzw. den ausgewählten Zeilen eine Chargennr. anhand der Chargennummernserie des Artikels; anschließend zeigt die InfoBox die Eigenschaften der neu zugeordneten Charge. |
| **Zeile → Chargennr.-Informationskarte** | Wenn Sie diese Aktion ausführen, dann öffnet sich die Chargennr.-Informationskarte zur markierten Charge; dort sehen und pflegen Sie zentrale Chargeninformationen. Die Aktion setzt eine erfasste Chargennr. voraus. |
| **Zeile → Seriennr.-Informationskarte** | Wenn Sie diese Aktion ausführen, dann öffnet sich die Seriennr.-Informationskarte zur markierten Seriennummer. Die Aktion setzt eine erfasste Seriennr. voraus. |

### InfoBox „Eigenschaften“ (Materialeigenschaften der Charge)

Die InfoBox ist der eigentliche Zusatz dieser Erweiterung. Sie steht links bzw. rechts neben den Zuordnungszeilen und aktualisiert sich, sobald der Anwender eine andere Chargenzeile markiert. Sie zeigt die Materialeigenschaften der Charge, die in der markierten Zuordnungszeile ausgewählt ist, und ist bearbeitbar.

| Feld | Erläuterung |
|---|---|
| **Eigenschaftsname** | Zeigt die Bezeichnung der Eigenschaft (z. B. ein Qualitäts- oder Maßmerkmal) der Charge. Wenn mehrere Eigenschaften gepflegt sind, dann erscheint je Eigenschaft eine Zeile. |
| **Wert** | Zeigt den konkreten Eigenschaftswert der Charge. Wenn Sie den Wert ändern, dann wird die Änderung unmittelbar an der Charge (Chargennr.-Information) gespeichert; weicht der Wert vom Standardwert ab, hebt die InfoBox ihn farblich hervor. Das Feld ist bearbeitbar, weil die Erweiterung die InfoBox als editierbar einbindet. |
| **Standardwert** | Zeigt den in der Materialart hinterlegten Vorgabewert. Wenn an der Charge kein eigener Wert erfasst ist, dann dient der Standardwert als Orientierung; dieses Feld erscheint, wenn die Quelle eine Materialart ist. |
| **Einheit** | Zeigt die Maßeinheit der Eigenschaft. Wenn eine Einheit gepflegt ist, dann ordnet der Anwender den Wert fachlich korrekt ein (z. B. mm, kg, Prozent). |
| **Anzeigereihenfolge** | Zeigt bzw. steuert die Sortierung der Eigenschaftszeilen. Wenn eine Anzeigereihenfolge vergeben ist, dann erscheinen die Eigenschaften in dieser Reihenfolge. |

**Ausgeblendete Felder:** Die InfoBox führt technisch weitere Felder mit (**Eigenschaftswertname**, **Kategoriencode** sowie eine Kategoriebeschreibung), die standardmäßig **nicht sichtbar** sind. Sie dienen der internen Verknüpfung von Eigenschaftswerten und Kategorien und sind für die tägliche Zuordnung nicht erforderlich; der Anwender muss sie nicht pflegen.

**Abschluss:** Sind alle Zeilen zugeordnet (undefinierte Menge = 0) und die Eigenschaften geprüft bzw. korrigiert, schließen Sie den Dialog mit **OK**. Die Zuordnung wird gespeichert und steht der Avisierung zur weiteren Bearbeitung zur Verfügung.

## FAQ und Troubleshooting

### 1. Warum ist die InfoBox „Eigenschaften“ leer, obwohl eine Charge zugeordnet ist?

Weil an der Charge keine Materialeigenschaften hinterlegt sind. Das ist der Fall, wenn am Artikel der **Materialartencode** fehlt oder die zugeordnete Materialart keine Eigenschaften besitzt. Setzen Sie auf der **Artikelkarte** den Materialartencode und ordnen Sie der **Materialart** über die **Materialartenkarte** Eigenschaften zu.

### 2. Wie öffne ich die Maske „Artikelverfolgungszuordnungszeilen“?

Nicht über **Suchen**. Öffnen Sie die **Avisierung**, markieren Sie die Belegzeile und wählen Sie **Zeile → Artikelverfolgungszuordnungszeilen**. Der Dialog ist ein modaler Zuordnungsdialog und nur aus der Belegzeile erreichbar.

### 3. Kann ich einen Eigenschaftswert direkt im Zuordnungsdialog ändern?

Ja. Die Erweiterung bindet die InfoBox **bearbeitbar** ein. Ändern Sie den **Wert** in der InfoBox; die Änderung wird sofort an der Charge (Chargennr.-Information) gespeichert und gilt danach überall, wo diese Charge verwendet wird.

### 4. Was bedeutet die farbliche Hervorhebung eines Werts in der InfoBox?

Der Wert weicht vom **Standardwert** der Materialart ab. So erkennen Sie sofort, welche Chargen einen vom Vorgabewert abweichenden Eigenschaftswert tragen.

### 5. Warum kann ich das Feld „Chargennr.“ nicht bearbeiten?

Weil der Artikel nicht chargenpflichtig ist. Das Feld ist nur aktiv, wenn der Artikelverfolgungscode des Artikels chargenspezifische Verfolgung vorsieht. Analog ist **Seriennr.** nur bei seriennummernpflichtigen Artikeln aktiv.

### 6. Warum lässt das System keine weitere Menge zu?

Weil die **Undefinierte Menge** bereits null ist. Sie können insgesamt nur so viel zuordnen, wie in **Menge für Zuweisung** vorgegeben ist. Prüfen Sie den Kopfbereich: Ist die undefinierte Menge null, ist die Zeile vollständig zugeordnet.

### 7. Wie ordne ich mehrere Chargen in einem Schritt zu?

Verwenden Sie die Aktion **&Einträge auswählen**. Dort markieren Sie mehrere verfügbare Chargen mit ihren Mengen und übernehmen sie gemeinsam in die Zuordnung.

### 8. Wodurch erhält eine neu angelegte Charge ihre Eigenschaften?

Über die Materialart des Artikels. Sobald der Artikel einen **Materialartencode** trägt, werden für seine Chargen die Eigenschaftszeilen der Materialart erzeugt; abweichende Werte lassen sich anschließend je Charge erfassen – auch direkt in der InfoBox.

### 9. In welcher Reihenfolge erscheinen die Eigenschaften in der InfoBox?

In der **Anzeigereihenfolge**, die in der Materialart je Eigenschaft gepflegt ist. Passen Sie die Anzeigereihenfolge in den Stammdaten an, um die wichtigsten Merkmale oben anzuzeigen.

### 10. Welche Voraussetzungen müssen vor der ersten Nutzung erfüllt sein?

Drei Schritte in Abhängigkeitsreihenfolge: **Materialeigenschaften Einrichtung** aktivieren, **Materialarten** mit **Eigenschaften** anlegen und den Artikeln den **Materialartencode** zuweisen. Erst danach zeigt die InfoBox in der Zuordnungsmaske Eigenschaften an.

## Typische Anwendungsfälle

### Anwendungsfall 1: Charge beim Avisieren anhand ihrer Materialeigenschaften prüfen

**Auslöser:** Ein Lieferant kündigt per E-Mail eine Lieferung an; der Anwender in der Logistik legt bzw. bearbeitet die passende **Avisierung** und muss den Zeilen die richtigen Chargen zuordnen.

**Einstieg in BC:** Der Anwender öffnet die **Avisierung**, markiert die betreffende Belegzeile und ruft über **Zeile → Artikelverfolgungszuordnungszeilen** den Zuordnungsdialog auf.

**Kernablauf:**
1. In der Zuordnungszeile über **&Einträge auswählen** eine verfügbare **Chargennr.** wählen und die **Menge für Zuweisung** eintragen.
2. Der Kopf aktualisiert **Bereits zugewiesene Menge:** und **Undefinierte Menge:**.
3. Der Anwender markiert die Chargenzeile; die InfoBox **Eigenschaften** zeigt **Eigenschaftsname**, **Wert** und **Einheit** der Charge.
4. Anhand der angezeigten Eigenschaften prüft der Anwender, ob die Charge zur Anforderung passt; passt sie nicht, wählt er über **&Einträge auswählen** eine andere Charge.
5. Sind alle Mengen zugeordnet (undefinierte Menge = 0), schließt der Anwender den Dialog mit **OK**.

**Abschluss:** Die Chargenzuordnung ist gespeichert und steht der Avisierung zur weiteren Bearbeitung bereit.

### Anwendungsfall 2: Eigenschaftswert einer Charge direkt im Zuordnungsdialog korrigieren

**Auslöser:** Eine interne Meldung besagt, dass ein Prüfwert einer bestimmten Charge nachgetragen oder korrigiert werden muss, während die Charge gerade avisiert wird.

**Einstieg in BC:** Wie in Anwendungsfall 1 öffnet der Anwender aus der **Avisierung** heraus die **Artikelverfolgungszuordnungszeilen**.

**Kernablauf:**
1. Der Anwender markiert die Zeile mit der betreffenden **Chargennr.**
2. In der InfoBox **Eigenschaften** ändert er im Feld **Wert** den betreffenden Eigenschaftswert.
3. Weicht der neue Wert vom **Standardwert** der Materialart ab, hebt die InfoBox ihn farblich hervor.
4. Bei Bedarf öffnet der Anwender über **Zeile → Chargennr.-Informationskarte** die Chargennr.-Informationskarte, um weitere Chargeninformationen zu prüfen.

**Abschluss:** Der Anwender schließt den Dialog mit **OK**. Der korrigierte Eigenschaftswert ist an der Charge gespeichert und gilt fortan überall dort, wo diese Charge verwendet wird.
