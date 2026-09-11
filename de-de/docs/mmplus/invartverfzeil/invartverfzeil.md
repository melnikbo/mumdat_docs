---
title: Anwenderhandbuch m+m Physical Inventory Item Tracking
---

# Anwenderhandbuch m+m Physical Inventory Item Tracking

## Einleitung

Die Erweiterung **m+m Physical Inventory Item Tracking** erweitert die Inventur in Microsoft Dynamics 365 Business Central um eine zusätzliche Funktion beim Erstellen der Inventurerfassung. Sie richtet sich in erster Linie an **operative Anwender im Lager und in der Inventur**, die einen **Inventurauftrag** bearbeiten und daraus die **Inventurerfassung** erzeugen und zählen. Lagerleitung und Systemadministration sind nur nachrangig betroffen, da die App keine eigenen Einrichtungsseiten mitbringt.

Zweck des Moduls ist die **erhebliche Erleichterung der Zählung von Artikeln mit Artikelverfolgung** (Seriennummern, Chargennummern und Paketnummern). Ohne die Erweiterung erhält der Anwender pro Inventurauftragszeile in der Regel eine einzelne Erfassungszeile und muss die vorhandenen Serien- und Chargennummern von Hand nachtragen. Mit der Erweiterung kann Business Central beim Erstellen der Erfassung **je erwarteter Serien-, Chargen- oder Paketnummer eine eigene Erfassungszeile** anlegen, sodass der Anwender nur noch die tatsächlich gezählte Menge eintragen muss.

Der Prozess umfasst nur wenige Schritte: Der Anwender öffnet einen Inventurauftrag, startet die Aktion **Neue Erfassung erstellen**, aktiviert im Dialog die Option **Separate Zeile pro Artikelverfolgung erstellen** und erhält anschließend eine Inventurerfassung, in der die erwarteten Artikelverfolgungsnummern bereits als getrennte Zeilen vorliegen.

## Schnellstart für Anwender

Die App benötigt keine eigene Einrichtung; nach der Installation steht die zusätzliche Option unmittelbar im Dialog der Erfassungserstellung zur Verfügung. Der schnellste Weg zu getrennten Erfassungszeilen je Artikelverfolgung:

1. Öffnen Sie den gewünschten **Inventurauftrag** über die Inventurauftragsliste und wählen Sie die Auftragszeile mit dem verfolgungspflichtigen Artikel.
2. Wählen Sie im Inventurauftrag die Aktion **Neue Erfassung erstellen**. Es öffnet sich der Dialog zur Eingabe der Optionen und Parameter.
3. Aktivieren Sie im Bereich **Optionen** das Kontrollkästchen **Separate Zeile pro Artikelverfolgung erstellen**.
4. Bestätigen Sie den Dialog. Business Central ermittelt die zum **Buchungsdatum** des Auftrags vorhandenen Bestände mit Artikelverfolgung und legt in der Inventurerfassung **je Seriennummer, Chargennummer und Paketnummer eine eigene Erfassungszeile** an.
5. Öffnen Sie die erzeugte **Inventurerfassung**, zählen Sie die einzelnen Nummern und tragen Sie die gezählte **Menge** je Zeile ein.

Lassen Sie die Option in Schritt 3 deaktiviert, wenn Sie wie im Standard vorgehen möchten: In diesem Fall entsteht eine Erfassungszeile ohne vorbelegte Verfolgungsnummern, und die Serien- bzw. Chargennummern sind manuell zu erfassen.

## Einrichtung

Für den Einsatz im Webclient von Microsoft Dynamics 365 Business Central ist **keine zusätzliche Einrichtung erforderlich**. Voraussetzung ist lediglich, dass die App **m+m Physical Inventory Item Tracking** in der Erweiterungsverwaltung installiert und aktiviert ist. Die Erweiterung bringt keine eigenen Einrichtungsseiten, Nummernserien oder Stammdaten mit; sie ergänzt ausschließlich den bestehenden Standardablauf der Inventurerfassung.

Damit die automatische Zeilenerstellung fachlich sinnvoll ist, müssen die betroffenen Artikel im Standard über eine **Artikelverfolgung** (Serien-, Chargen- oder Paketnummernführung) verfügen und über entsprechende Lagerbestände zum Stichtag verfügen. Diese Voraussetzungen werden vollständig im Business-Central-Standard gepflegt (Artikelverfolgungscode am Artikel, Lager- bzw. Lagerplatzführung am Lagerort). Die Erweiterung wertet diese vorhandenen Daten nur aus; sie verändert die Standardeinrichtung nicht.

## Anwendung: Erfassung mit getrennten Verfolgungszeilen

Die gesamte Funktion der Erweiterung liegt im Ablauf **Inventurauftrag → Neue Erfassung erstellen → Inventurerfassung**. Dieser Abschnitt beschreibt die zusätzliche Option und ihre Wirkung im Detail.

### Einstieg und Aufruf

**Einstieg:** Inventurauftragsliste → **Inventurauftrag** öffnen → Aktion **Neue Erfassung erstellen**.

Öffnen Sie über die Aktion **Neue Erfassung erstellen** im Inventurauftrag den Dialog zur Erstellung der Inventurerfassung. Der Dialog entspricht dem Business-Central-Standard und wird durch die Erweiterung um genau eine Option ergänzt.

### Zusätzliche Option im Dialog

Die Erweiterung fügt im Bereich **Optionen** des Dialogs das folgende Kontrollkästchen hinzu:

| Option | Erläuterung |
|--------|-------------|
| **Separate Zeile pro Artikelverfolgung erstellen** | Wenn aktiviert, ermittelt Business Central beim Erstellen der Erfassung die zum **Buchungsdatum** des Inventurauftrags vorhandenen Bestände mit Artikelverfolgung und legt in der **Inventurerfassung** je erwarteter **Seriennummer**, **Chargennummer** und **Paketnummer** eine eigene Erfassungszeile an. Der Anwender muss anschließend nur noch die gezählte **Menge** je Nummer eintragen. Wenn nicht aktiviert, entsteht wie im Standard eine Erfassungszeile ohne vorbelegte Verfolgungsnummern; die Serien- bzw. Chargennummern sind dann manuell zu erfassen. |

Das Kontrollkästchen ist standardmäßig **nicht** gesetzt; der Standardablauf bleibt damit unverändert, solange der Anwender die Option nicht bewusst aktiviert. Die Einstellung gilt für den jeweiligen Aufruf der Erfassungserstellung und wird nach dem Lauf wieder zurückgesetzt.

### Welche Bestände ermittelt werden

Bei aktivierter Option ermittelt die Erweiterung die vorhandene Artikelverfolgung abhängig von der Lagerführung des Lagerorts der Auftragszeile:

- **Lagerplatzpflichtiger Lagerort mit Lagerplatzverfolgung:** Grundlage sind die **Lagerposten** zum passenden **Lagerortcode**, **Lagerplatzcode**, **Artikelnr.** und **Variantencode**, deren Registrierungsdatum bis zum **Buchungsdatum** des Inventurauftrags liegt. Berücksichtigt werden Posten mit einer **Seriennummer** oder **Chargennummer**.
- **Übrige Lagerorte:** Grundlage sind die **Artikelposten** zum passenden **Artikelnr.**, **Variantencode** und **Lagerortcode** bis zum **Buchungsdatum**. Berücksichtigt werden Posten mit einer **Seriennummer**, **Chargennummer** oder **Paketnummer**.

Die ermittelten Mengen werden je Kombination aus Serien-, Chargen- und Paketnummer aufsummiert. **Kombinationen mit einer erwarteten Menge von Null werden nicht als Erfassungszeile angelegt**, sodass in der Erfassung nur tatsächlich bestandsführende Verfolgungsnummern erscheinen.

### Ergebnis in der Inventurerfassung

In der erzeugten **Inventurerfassung** entsteht je ermittelter Verfolgungsnummer eine eigene Erfassungszeile mit vorbelegter **Seriennummer**, **Chargennummer** und **Paketnummer**. Die **Menge** wird dabei bewusst mit **0** vorbelegt und das Kennzeichen **Erfasst** bleibt zunächst leer, damit der Anwender die tatsächlich gezählte Menge je Nummer eintragen und die Zeile anschließend als erfasst kennzeichnen kann. Der weitere Ablauf der Inventur (Zählung, Erfassung, Buchung des Inventurauftrags) folgt unverändert dem Business-Central-Standard.

### Erweitertes Feld am Inventurauftrag

Die Erweiterung führt am **Inventurauftrag** ein zusätzliches, internes Steuerkennzeichen:

| Feld | Erläuterung |
|------|-------------|
| **Separate Zeile pro Artikelverfolgung erstellen** | Wenn gesetzt, verarbeitet Business Central beim Erstellen der Erfassung die getrennten Verfolgungszeilen für diesen Inventurauftrag. Das Feld wird durch die Option im Dialog automatisch gesetzt und nach dem Lauf wieder zurückgesetzt; es ist **nicht editierbar** und muss vom Anwender nicht gepflegt werden. Es dient ausschließlich der internen Steuerung und erfordert keine manuelle Bearbeitung. |

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Einsatz der Erweiterung im Alltag. Alle Schritte entsprechen dem geprüften Ablauf der App.

### Chargengeführte Artikel zur Stichtagsinventur zählen

**Auslöser:** Zum Inventurstichtag muss ein chargengeführter Artikel gezählt werden, zu dem im Lager mehrere Chargen mit Bestand liegen.

**Einstieg in BC:** Der Anwender öffnet den betreffenden **Inventurauftrag** aus der Inventurauftragsliste und wählt die Auftragszeile des Artikels.

**Kernablauf:** Über die Aktion **Neue Erfassung erstellen** öffnet der Anwender den Dialog, aktiviert **Separate Zeile pro Artikelverfolgung erstellen** und bestätigt. Business Central ermittelt aus den **Artikelposten** die zum **Buchungsdatum** vorhandenen Chargen und legt in der **Inventurerfassung** je Charge eine eigene Zeile mit vorbelegter **Chargennummer** an. Der Anwender zählt die einzelnen Chargen und trägt die jeweilige **Menge** ein.

**Abschluss:** Nach dem Erfassen der Mengen kennzeichnet der Anwender die Zeilen als **Erfasst**; die weitere Verarbeitung des Inventurauftrags erfolgt im Standard.

### Seriennummerngeführte Artikel im lagerplatzgeführten Lager

**Auslöser:** In einem lagerplatzpflichtigen Lager mit Lagerplatzverfolgung ist ein seriennummerngeführter Artikel zu inventarisieren.

**Einstieg in BC:** Der Anwender öffnet den **Inventurauftrag** und wählt die Auftragszeile mit dem passenden **Lagerortcode** und **Lagerplatzcode**.

**Kernablauf:** Über **Neue Erfassung erstellen** aktiviert der Anwender **Separate Zeile pro Artikelverfolgung erstellen**. Business Central wertet in diesem Fall die **Lagerposten** je **Lagerortcode**, **Lagerplatzcode**, **Artikelnr.** und **Variantencode** bis zum **Buchungsdatum** aus und legt je erwarteter **Seriennummer** eine Erfassungszeile an. Der Anwender prüft die physische Präsenz jeder Seriennummer und trägt die gezählte **Menge** ein.

**Abschluss:** Fehlende Seriennummern bleiben mit Menge 0 stehen und werden so als Fehlbestand sichtbar; die Zeilen werden als **Erfasst** gekennzeichnet und der Inventurauftrag im Standard weiterverarbeitet.

## FAQ und Troubleshooting

### Warum werden in der Inventurerfassung mehrere Zeilen pro Artikel angelegt?

Weil im Dialog **Neue Erfassung erstellen** die Option **Separate Zeile pro Artikelverfolgung erstellen** aktiviert war. Business Central legt dann je vorhandener Serien-, Chargen- oder Paketnummer eine eigene Erfassungszeile an, statt einer einzelnen Sammelzeile.

### Wie erhalte ich weiterhin nur eine Erfassungszeile pro Artikel?

Lassen Sie die Option **Separate Zeile pro Artikelverfolgung erstellen** im Dialog deaktiviert. Dann entsteht wie im Standard eine Erfassungszeile, und die Serien- bzw. Chargennummern sind manuell zu erfassen.

### Warum erscheint eine bestimmte Charge nicht als eigene Erfassungszeile?

Es werden nur Verfolgungsnummern angelegt, zu denen bis zum **Buchungsdatum** des Inventurauftrags ein Bestand ermittelt wird. Kombinationen mit einer erwarteten Menge von Null werden bewusst nicht als Zeile erzeugt.

### Warum steht in den erzeugten Zeilen zunächst die Menge 0?

Die Erweiterung belegt die erwartete Zählmenge bewusst mit 0 vor. So trägt ausschließlich der Anwender die tatsächlich gezählte **Menge** ein, und das Zählergebnis wird nicht durch den erwarteten Bestand vorweggenommen.

### Bis zu welchem Datum werden Bestände berücksichtigt?

Maßgeblich ist das **Buchungsdatum** des Inventurauftrags. Es werden Lager- bzw. Artikelposten bis einschließlich dieses Datums ausgewertet.

### Wovon hängt es ab, ob Lagerposten oder Artikelposten ausgewertet werden?

Bei einem **lagerplatzpflichtigen Lagerort mit Lagerplatzverfolgung** werden die **Lagerposten** je Lagerort und Lagerplatz herangezogen. Bei allen übrigen Lagerorten sind die **Artikelposten** die Grundlage.

### Werden Paketnummern ebenfalls berücksichtigt?

Ja. Bei der Auswertung der Artikelposten werden neben Serien- und Chargennummern auch **Paketnummern** ausgewertet und als eigene Erfassungszeilen berücksichtigt.

### Muss ich das Feld „Separate Zeile pro Artikelverfolgung erstellen" am Inventurauftrag selbst setzen?

Nein. Das gleichnamige Feld am Inventurauftrag ist nicht editierbar und wird durch die Option im Dialog automatisch gesetzt und nach dem Lauf wieder zurückgesetzt. Eine manuelle Pflege ist weder nötig noch möglich.

### Ist eine Einrichtung notwendig, bevor ich die Option nutzen kann?

Nein. Für die Nutzung im Webclient ist keine zusätzliche Einrichtung erforderlich; die App muss lediglich installiert sein. Die betroffenen Artikel müssen im Standard über eine Artikelverfolgung verfügen.

### Warum ist eine Seriennummer trotz Bestand nicht in der Erfassung enthalten?

Prüfen Sie **Lagerortcode**, **Lagerplatzcode**, **Artikelnr.** und **Variantencode** der Auftragszeile sowie das **Buchungsdatum**. Es werden nur Posten berücksichtigt, die exakt zu diesen Werten passen und deren Datum innerhalb des Stichtags liegt; ohne passende Bewegung entsteht keine Zeile.
