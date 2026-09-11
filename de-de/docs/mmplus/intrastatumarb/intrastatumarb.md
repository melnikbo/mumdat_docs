---
title: "Anwenderhandbuch m+m Metal & Tolling with Intrastat"
---

# Anwenderhandbuch m+m Metal & Tolling with Intrastat

## Einleitung

Die App **m+m Metal & Tolling with Intrastat** verbindet die Umarbeitungs- und Metallwertdaten aus dem Modul **m+m Metal & Tolling** mit der Intrastatmeldung von Business Central. Bei Warenbewegungen mit Umarbeitung ist der reine Umarbeitungsanteil (die Dienstleistung am fremden Metall) statistisch anders zu bewerten als der volle Warenwert. Diese App sorgt dafür, dass die Intrastatmeldung diesen Unterschied automatisch berücksichtigt: Sie überträgt beim Vorschlagen der Meldungszeilen die Kennzeichnung **Umarbeitung** und den **Metallwert** von den gebuchten Beleg­zeilen in die Intrastat-Meldungszeile und berechnet daraus den statistischen Wert neu.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwenderinnen und Anwender**, die die monatliche Intrastatmeldung erstellen und prüfen — im Regelfall Mitarbeitende aus Buchhaltung, Zoll oder Export. Sie arbeiten direkt an den **Meldungszeilen** der Intrastatmeldung. Administratorinnen und Administratoren sind nur mittelbar betroffen: Sie stellen im vorgelagerten Modul **m+m Metal & Tolling** sicher, dass die betroffenen Belege überhaupt mit Umarbeitung und Metallwert gebucht werden.

**Kurzer Prozessüberblick:**

1. Waren werden im Verkauf oder Einkauf mit **Umarbeitung** und **Metallwert** gebucht (durch das Basismodul m+m Metal & Tolling).
2. Am Monatsende ruft der Anwender die Intrastatmeldung auf und lässt die Zeilen aus den Artikelposten vorschlagen.
3. Diese App überträgt beim Vorschlag automatisch **Umarbeitung** und **Metallwert** aus der jeweils gebuchten Belegzeile in die Meldungszeile und errechnet den **Metallbetrag**.
4. Der statistische Wert der Zeile wird um den reinen Metallanteil bereinigt, sodass nur der Umarbeitungsanteil gemeldet wird.
5. Der Anwender prüft die Zeilen, korrigiert bei Bedarf und übergibt die Meldung wie gewohnt an die Behörde.

## Schnellstart für Anwender

Der schnellste Weg zu einer korrekten Intrastatmeldung mit Umarbeitung besteht aus wenigen Schritten. Voraussetzung ist, dass die zugrundeliegenden Belege bereits mit **Umarbeitung** und **Metallwert** gebucht wurden (siehe **Einrichtung und Voraussetzungen**).

1. **Einrichtung prüfen (einmalig):** Stellen Sie sicher, dass im Modul **m+m Metal & Tolling** die betroffenen Verkaufs- und Einkaufsbelege mit **Umarbeitung** und **Metallwert** erfasst und gebucht werden. Ohne diese Daten auf den gebuchten Belegzeilen bleibt die Meldungszeile ohne Umarbeitungsanteil.
2. **Intrastatmeldung öffnen:** Öffnen Sie über **Suchen** die Intrastatmeldung und legen Sie die Meldung für den gewünschten Zeitraum an bzw. öffnen Sie eine bestehende.
3. **Zeilen vorschlagen lassen:** Rufen Sie die Standardfunktion zum Vorschlagen der Meldungszeilen (Abruf aus den Artikelposten) auf. Beim Erzeugen jeder Zeile überträgt die App automatisch **Umarbeitung** und **Metallwert** aus der gebuchten Belegzeile und berechnet den **Metallbetrag**.
4. **Zeilen prüfen:** Kontrollieren Sie in der Zeilenübersicht die Spalten **Umarbeitung**, **Metallwert** und **Metallbetrag** sowie den daraus resultierenden statistischen Wert.
5. **Bei Bedarf korrigieren:** Passen Sie **Umarbeitung**, **Metallwert**, **Nettogewicht** oder **Betrag** direkt in der Zeile an. Der **Metallbetrag** und der statistische Wert werden sofort neu berechnet.
6. **Meldung abschließen:** Übergeben Sie die geprüfte Intrastatmeldung wie im Standard von Business Central an die Behörde.

## Einrichtung und Voraussetzungen

Diese App bringt **keine eigene Einrichtungsseite** mit. Sie besitzt keine Nummernserien, Parameter oder Optionsschalter, die separat zu pflegen wären. Ihre Wirkung hängt ausschließlich davon ab, dass die vorgelagerten Belege die richtigen Daten tragen.

**Wer richtet ein und wann:** Die Einrichtung erfolgt einmalig durch die Administration bzw. den Key-User des Moduls **m+m Metal & Tolling** — vor der ersten Intrastatmeldung, in der Umarbeitungsvorgänge enthalten sein sollen. Die operative Anwendung (Schritt für Schritt beschrieben unter **Tägliche Arbeit an der Meldungszeile**) setzt diese Einrichtung voraus.

**Was einzurichten ist (Wirkungsprinzip):**

- **Umarbeitung und Metallwert auf den Belegen aktivieren.** Wenn im Modul m+m Metal & Tolling Verkaufs- und Einkaufsvorgänge mit **Umarbeitung** und **Metallwert** gebucht werden, dann stehen diese Werte anschließend auf den gebuchten Belegzeilen (Verkaufslieferung, Verkaufsrechnung, Verkaufsgutschrift, Verkaufsreklamation/Rücksendung sowie den entsprechenden Einkaufsbelegen) zur Verfügung. Nur dann kann diese App sie beim Zeilenvorschlag in die Intrastatmeldung übernehmen; ohne diese Daten bleibt die Meldungszeile ein normaler Warenwert ohne Umarbeitungsbereinigung.
- **Standardmäßige Art des Geschäftes prüfen.** Da Ein- und Ausgänge in der Intrastatmeldung je nach Ein- oder Verkaufsgeschäft unterschiedlich zu bewerten sind, sollte im vorgelagerten Modul die zutreffende **Art des Geschäftes** hinterlegt sein. Wenn sie korrekt gesetzt ist, dann werden die vorgeschlagenen Meldungszeilen mit der passenden Geschäftsart erzeugt und die Umarbeitungsbereinigung greift auf der richtigen Bewegungsart.

Eine mehrstufige, seitenübergreifende Aktivierungskette existiert innerhalb dieser App **nicht**; deshalb gibt es hier bewusst keine gesonderte „… einrichten“-Prozedur. Die einzige Voraussetzung ist die oben beschriebene Datenlage auf den gebuchten Belegen.

## Tägliche Arbeit an der Meldungszeile

Die gesamte sichtbare Funktion dieser App liegt in den **Meldungszeilen** der Intrastatmeldung. Dort ergänzt die App die Zeilenübersicht (das Unterformular der Intrastatmeldung) um drei Spalten und steuert die automatische Berechnung des statistischen Werts.

**Steuerung durch vorgelagerte Daten:** Die Inhalte der Spalten **Umarbeitung** und **Metallwert** stammen aus den gebuchten Belegzeilen des Moduls **m+m Metal & Tolling** (siehe **Einrichtung und Voraussetzungen**). Beim Vorschlagen der Meldungszeilen werden sie automatisch übernommen; in der Zeile selbst können sie anschließend noch verändert werden.

### Einstieg

Öffnen Sie über **Suchen** die Intrastatmeldung für den gewünschten Meldezeitraum. Die drei Zusatzspalten erscheinen in der **Zeilenübersicht** (dem Unterformular) der Meldung; sie sind dort am Ende der bestehenden Spalten eingefügt und stehen für jede Meldungszeile zur Verfügung.

### Zusätzliche Felder der Meldungszeile

Die folgenden Felder ergänzt diese App auf jeder Meldungszeile. Alle drei stehen sowohl in der Zeilenübersicht als auch in der Zeilenbearbeitung zur Verfügung.

| Feld | Erläuterung |
|---|---|
| **Umarbeitung** | Kennzeichen (Ja/Nein), ob die Zeile eine Umarbeitung betrifft. **Wenn aktiviert**, dann behandelt die App die Zeile als Umarbeitungsvorgang: Der reine Metallanteil wird über den **Metallbetrag** aus dem meldepflichtigen **Betrag** herausgerechnet, sodass nur der Umarbeitungsanteil in den statistischen Wert einfließt. **Wenn nicht aktiviert**, dann bleibt die Zeile ein gewöhnlicher Warenwert; der **Metallbetrag** wird auf 0 gesetzt und der statistische Wert wie im Standard ermittelt. Beim Zeilenvorschlag wird der Wert automatisch aus der gebuchten Belegzeile übernommen, lässt sich in der Meldungszeile aber manuell umsetzen. |
| **Metallwert** | Der spezifische Metallwert je Gewichts-/Mengeneinheit, der aus der gebuchten Belegzeile übernommen wird. **Wenn ein Wert gesetzt ist und Umarbeitung aktiviert ist**, dann berechnet die App daraus den **Metallbetrag** und passt **Betrag** und statistischen Wert entsprechend an. Eine Änderung dieses Feldes löst die Neuberechnung der Zeile sofort aus (siehe **Feldberechnung und Wirkungsweise**). Das Feld erlaubt bis zu fünf Nachkommastellen, damit auch feine Notierungen exakt abgebildet werden. |
| **Metallbetrag** | Der aus **Metallwert**, **Nettogewicht** und **Menge** errechnete reine Metallanteil der Zeile. Das Feld wird **automatisch berechnet und ist nicht direkt editierbar**. **Wenn Umarbeitung aktiviert ist**, dann enthält es den herausgerechneten Metallanteil, der vom meldepflichtigen **Betrag** abgezogen und im statistischen Wert wieder als reiner Statistikanteil berücksichtigt wird; **wenn Umarbeitung nicht aktiviert ist**, dann ist der **Metallbetrag** 0. |

**Option „Umarbeitung“ — Bedeutung der Werte:**

- **Aktiviert (Ja):** Die Zeile gilt als Umarbeitung. Der **Metallbetrag** wird aus dem **Metallwert** berechnet, vom **Betrag** abgezogen und in den statistischen Wert eingerechnet. So wird nur der Umarbeitungsanteil statistisch gemeldet, nicht der volle Metallwert.
- **Nicht aktiviert (Nein):** Die Zeile gilt als normaler Warenwert. Der **Metallbetrag** ist 0; **Betrag** und statistischer Wert entsprechen dem Standardverhalten der Intrastatmeldung. Wird die Kennzeichnung von Ja auf Nein zurückgesetzt, dann wird ein zuvor abgezogener **Metallbetrag** wieder auf den **Betrag** aufgeschlagen.

### Manuelle Korrektur einer Zeile

Sie können die berechneten Werte jederzeit auf der Zeile nachsteuern:

1. Öffnen Sie die betroffene Meldungszeile in der Zeilenübersicht.
2. Setzen oder entfernen Sie das Kennzeichen **Umarbeitung** bzw. tragen Sie einen korrigierten **Metallwert** ein.
3. Sobald Sie **Umarbeitung**, **Metallwert**, **Nettogewicht** oder **Betrag** ändern, berechnet die App den **Metallbetrag** und den statistischen Wert der Zeile automatisch neu — ein separater Berechnungsaufruf ist nicht nötig.
4. Kontrollieren Sie den neuen **Metallbetrag** und den statistischen Wert, bevor Sie die Meldung abschließen.

## Feldberechnung und Wirkungsweise

Der fachliche Kern dieser App ist die automatische Berechnung des statistischen Werts bei Umarbeitung. Die Berechnung läuft vollständig im Hintergrund und wird durch jede relevante Feldänderung ausgelöst.

**Auslöser der Neuberechnung:** Die Zeile wird immer dann neu berechnet, wenn eines der folgenden Felder geändert wird: **Betrag**, **Nettogewicht**, der (aus dem Basismodul stammende) Zuschlags-/Kostenanteil der Zeile, der indirekte Kostenanteil der Zeile oder die App-eigenen Felder **Umarbeitung** und **Metallwert**. In allen Fällen stößt die App intern die Neubewertung des **Metallwerts** an, sodass **Metallbetrag** und statistischer Wert konsistent bleiben.

**Rechenregel:**

1. **Metallbetrag ermitteln.** Ist **Umarbeitung** aktiviert, dann gilt: **Metallbetrag = Metallwert × (Nettogewicht × Menge)**, gerundet auf ganze Beträge. Ist **Umarbeitung** nicht aktiviert, dann ist der **Metallbetrag** 0.
2. **Betrag bereinigen.** Wird eine Zeile von „Umarbeitung“ auf „keine Umarbeitung“ zurückgesetzt, dann wird der zuvor abgezogene **Metallbetrag** wieder auf den **Betrag** aufgeschlagen. Ist **Umarbeitung** aktiviert, dann wird der frisch berechnete **Metallbetrag** vom **Betrag** abgezogen.
3. **Statistischen Wert bilden.** Der statistische Wert der Zeile wird aus dem bereinigten **Betrag** zuzüglich des indirekten Kostenanteils und des **Metallbetrags** gebildet und auf ganze Beträge gerundet. Auf diese Weise enthält der statistische Wert den Umarbeitungsanteil in der gesetzlich geforderten Bewertung.

**Automatische Übernahme beim Zeilenvorschlag:** Beim Vorschlagen der Meldungszeilen aus den Artikelposten ermittelt die App zu jeder Bewegung den zugehörigen gebuchten Beleg. Berücksichtigt werden ausschließlich Artikelposten der Herkunft **Einkauf** und **Verkauf**. Je nach Belegart wird die passende gebuchte Zeile herangezogen:

- Verkaufslieferung, Verkaufsreklamation (Rücksendung), Verkaufsrechnung und Verkaufsgutschrift,
- Einkaufslieferung (Wareneingang), Einkaufsreklamation (Rücksendung), Einkaufsrechnung und Einkaufsgutschrift.

Aus der gefundenen Belegzeile übernimmt die App **Umarbeitung** und **Metallwert** in die Meldungszeile. Findet sich zu einer Bewegung keine passende gebuchte Belegzeile mit diesen Daten, dann bleibt die Zeile ohne Umarbeitungsanteil und kann bei Bedarf manuell nachgepflegt werden.

## Typische Anwendungsfälle

### Anwendungsfall 1: Umarbeitungsware in der monatlichen Intrastatmeldung

**Auslöser:** Zum Monatsanfang steht die Intrastatmeldung des Vormonats an. Im Vormonat wurden mehrere Lieferungen mit Umarbeitung an Kunden im EU-Ausland ausgeführt.

**Einstieg in BC:** Die Sachbearbeiterin öffnet über **Suchen** die Intrastatmeldung und legt die Meldung für den Meldezeitraum an.

**Kernablauf:**

1. Sie ruft die Standardfunktion zum Vorschlagen der Meldungszeilen auf; die Zeilen werden aus den Artikelposten erzeugt.
2. Für jede Zeile, deren gebuchte Belegzeile eine Umarbeitung trägt, setzt die App automatisch das Kennzeichen **Umarbeitung** und übernimmt den **Metallwert**.
3. Die App berechnet den **Metallbetrag** und bereinigt **Betrag** sowie statistischen Wert, sodass nur der Umarbeitungsanteil gemeldet wird.
4. Die Sachbearbeiterin prüft in der Zeilenübersicht die Spalten **Umarbeitung**, **Metallwert** und **Metallbetrag** und vergleicht den statistischen Wert mit ihrer Erwartung.

**Abschluss:** Nach der Prüfung übergibt sie die Meldung wie im Standard von Business Central an die Behörde. Ein zusätzlicher App-Schritt ist nicht erforderlich.

### Anwendungsfall 2: Nachträgliche Korrektur eines Metallwerts

**Auslöser:** Bei der Kontrolle fällt auf, dass für eine Position ein veralteter Metallwert übernommen wurde, weil die Notierung erst nach der Buchung aktualisiert wurde.

**Einstieg in BC:** Der Anwender öffnet dieselbe Intrastatmeldung und wechselt in die betroffene Meldungszeile in der Zeilenübersicht.

**Kernablauf:**

1. Er kontrolliert das Kennzeichen **Umarbeitung** — es ist korrekt gesetzt.
2. Er trägt im Feld **Metallwert** den richtigen Wert ein.
3. Mit dem Verlassen des Feldes berechnet die App den **Metallbetrag** neu und passt **Betrag** und statistischen Wert der Zeile automatisch an.
4. Er prüft den neuen statistischen Wert der Zeile.

**Abschluss:** Die korrigierte Zeile ist sofort meldefertig; die Meldung kann ohne weitere Zwischenschritte abgeschlossen werden.

## FAQ und Troubleshooting

### 1. Warum erscheinen die Spalten Umarbeitung, Metallwert und Metallbetrag nur in der Intrastatmeldung?
Weil diese App ausschließlich die **Zeilenübersicht der Intrastatmeldung** erweitert. Die drei Felder werden am Ende der bestehenden Spalten der Meldungszeile eingefügt und stehen deshalb nur dort zur Verfügung — nicht auf anderen Seiten.

### 2. Warum ist eine Meldungszeile ohne Umarbeitung markiert, obwohl der Vorgang eine Umarbeitung war?
Das Kennzeichen **Umarbeitung** wird beim Zeilenvorschlag aus der **gebuchten Belegzeile** übernommen. Trug der ursprüngliche Beleg keine Umarbeitung, dann bleibt auch die Meldungszeile ohne Kennzeichen. Sie können die Kennzeichnung in der Zeile manuell setzen; der **Metallbetrag** wird dann neu berechnet.

### 3. Warum ändert sich der statistische Wert, sobald ich das Kennzeichen Umarbeitung setze?
Bei aktivierter **Umarbeitung** rechnet die App den **Metallbetrag** aus dem **Betrag** heraus und berücksichtigt ihn separat im statistischen Wert. Dadurch wird nur der Umarbeitungsanteil statistisch gemeldet, weshalb sich der statistische Wert gegenüber der reinen Warenwertmeldung verändert.

### 4. Warum kann ich den Metallbetrag nicht direkt eingeben?
Der **Metallbetrag** ist ein **berechnetes Feld** und deshalb nicht editierbar. Er ergibt sich aus **Metallwert × (Nettogewicht × Menge)**. Um ihn zu beeinflussen, ändern Sie **Metallwert**, **Nettogewicht** oder **Menge**.

### 5. Wie wird der Metallbetrag genau berechnet?
Bei aktivierter **Umarbeitung** gilt: **Metallbetrag = Metallwert × (Nettogewicht × Menge)**, gerundet auf ganze Beträge. Ohne Umarbeitung ist der **Metallbetrag** 0.

### 6. Warum wird der Betrag größer, wenn ich das Kennzeichen Umarbeitung wieder entferne?
Beim Deaktivieren der **Umarbeitung** schlägt die App den zuvor abgezogenen **Metallbetrag** wieder auf den **Betrag** auf. Damit entspricht die Zeile wieder dem vollen Warenwert ohne Umarbeitungsbereinigung.

### 7. Ich habe den Metallwert geändert, aber es passiert nichts. Woran liegt das?
Die Neuberechnung wird erst mit dem **Verlassen des Feldes** (Feldbestätigung) ausgelöst. Prüfen Sie außerdem, ob **Umarbeitung** aktiviert ist — bei nicht aktivierter Umarbeitung bleibt der **Metallbetrag** unabhängig vom **Metallwert** bei 0.

### 8. Für welche Belegarten übernimmt die App die Umarbeitungsdaten automatisch?
Für gebuchte Verkaufslieferungen, Verkaufsreklamationen (Rücksendungen), Verkaufsrechnungen und Verkaufsgutschriften sowie die entsprechenden Einkaufsbelege (Wareneingang, Einkaufsreklamation, Einkaufsrechnung, Einkaufsgutschrift). Nur Artikelposten der Herkunft Einkauf und Verkauf werden berücksichtigt.

### 9. Warum bleibt eine vorgeschlagene Zeile ohne Metallwert?
Findet die App zur Bewegung keine passende gebuchte Belegzeile mit **Umarbeitung** und **Metallwert** — etwa weil der Beleg ohne diese Daten gebucht wurde —, dann bleibt die Meldungszeile ohne Umarbeitungsanteil. Sie können die Werte in der Zeile manuell nachtragen.

### 10. Muss ich für diese App etwas einrichten?
Innerhalb dieser App ist **keine** eigene Einrichtung nötig. Voraussetzung ist allein, dass die vorgelagerten Belege im Modul **m+m Metal & Tolling** mit **Umarbeitung** und **Metallwert** gebucht werden. Sind diese Daten vorhanden, arbeitet die App beim Zeilenvorschlag und bei jeder Zeilenänderung automatisch.
