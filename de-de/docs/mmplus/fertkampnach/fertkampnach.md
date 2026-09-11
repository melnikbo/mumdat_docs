---
title: Anwenderhandbuch m+m Production Campaign with Rework
---

# Anwenderhandbuch m+m Production Campaign with Rework

## Einleitung

Das Modul **m+m Production Campaign with Rework** verbindet die Produktionskampagne mit der Nacharbeitslogik von Business Central. Es ergänzt die Seite **Produktionskampagne** um die Aktion **Nacharbeiten**: Anwender markieren betroffene Kampagnenzeilen und lösen daraus einen Nacharbeitsvorgang aus. Je nach gewähltem **Nacharbeitsprozess** wird die betroffene Menge entweder in einen neuen **Fertigungsauftrag** übernommen (Prozess **Fertigung**) oder als Ausschuss behandelt (Prozess **Schrott**). Ist dieselbe Fertigungsauftragsmenge auf mehrere Kampagnen oder Arbeitsgänge verteilt, verlangt das Modul zusätzlich eine manuelle Verteilung der Mengenreduzierung im Assistenten **Kampagnenzeilen aktualisieren**.

Die Erweiterung besitzt **keine eigene Einrichtungsseite** und keine eigene Übersichtsliste. Sie setzt vollständig auf den drei Basis-Apps auf: der Produktionskampagne (Kampagnen, Kampagnenzeilen, verknüpfte Fertigungsaufträge), der Nacharbeitslogik (Nummernserien, Fertigungsstatus, Fehlerarten und Fehlergründe, Schrottlager) und der Cloud-Base-Lizenzprüfung.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender in der Fertigungssteuerung** – Arbeitsvorbereitung, Produktionsplanung und Fertigungssteuerung –, die im Tagesgeschäft an der Produktionskampagne arbeiten und dort Qualitäts- und Ausschussfälle bearbeiten. Administratoren und Key-User sind die sekundäre Zielgruppe: Sie richten in der **Fertigungseinrichtung** die Nummernserien und den Fertigungsstatus für die Nacharbeit ein und geben auf der **Lagerortkarte** Schrottlager frei.

### Prozessüberblick

Voraussetzungen prüfen (Kampagne, Kampagnenzeile, verknüpfter Fertigungsauftrag) → Zeile(n) markieren → Aktion **Nacharbeiten** → **Überarbeitungsdialog** ausfüllen (Fehlertyp, Fehlerursache, Menge, bei Schrott zusätzlich Schrottlager) → bei verteilten Mengen den Assistenten **Kampagnenzeilen aktualisieren** ausfüllen → **Abschließen**. Das Modul verbucht die Nacharbeit direkt und passt Kampagnen- und Fertigungsauftragsmengen automatisch an.

## Schnellstart für Anwender

Der schnellste Weg von einem Qualitäts- oder Ausschussfall bis zur verbuchten Nacharbeit. Die Einrichtung (siehe Kapitel **Einrichtung**) muss einmalig durch einen Administrator erfolgt sein, bevor der erste Vorgang gebucht werden kann.

1. **Voraussetzung (einmalig, Administrator):** In der **Fertigungseinrichtung** sind **Fertigungsstatus**, **Schrottnummernserie** und **Fertigungsnummernserie** gepflegt; für Schrott ist mindestens ein Lagerort mit **Schrott erlauben** vorhanden.
2. Öffnen Sie die Seite **Produktionskampagne** und wählen Sie die betroffene Kampagne. Im Kopf zeigt das Kennzeichen **Nacharbeiten** an, ob für diese Kampagne bereits ein Nacharbeitsbezug besteht.
3. Wechseln Sie in die Kampagnenzeilen und markieren Sie die betroffene Zeile (oder mehrere Zeilen).
4. Wählen Sie in den Zeilen die Aktion **Nacharbeiten**. Der **Überarbeitungsdialog** öffnet sich.
5. Erfassen Sie je Zeile mindestens **Nacharbeitsfehlertypcode**, **Ursachencode für Nacharbeitsfehler** und **Menge**. Der **Nacharbeitsprozess** wird automatisch aus dem Fehlertyp abgeleitet:
   - Bei **Fertigung** können Sie optional eine **Alternative Routenführung** angeben.
   - Bei **Schrott** füllen Sie zusätzlich den **Junk-Standortcode** und – bei lagerplatzpflichtigen Lagerorten – den **Junk-Bin-Code**.
6. Schließen Sie den Dialog mit **OK**. Das Modul prüft alle Pflichtfelder und Mengen.
7. Erscheint der Assistent **Kampagnenzeilen aktualisieren**, tragen Sie in **Neue Menge** je betroffener Zeile die künftige Restmenge ein, bis die **Reduzierte Menge** insgesamt der **Erforderlichen Menge zur Senkung** entspricht. Schließen Sie den Assistenten mit **Abschließen** ab.
8. Das Modul verbucht die Nacharbeit direkt: Es reduziert die betroffenen Kampagnen- und Fertigungsauftragsmengen, kennzeichnet die Ursprungszeile als **Überarbeitet** und legt bei **Fertigung** einen neuen **Fertigungsauftrag** für die Nacharbeitsmenge an.

## Einrichtung

Diese Erweiterung bringt **keine eigene Einrichtungsseite** mit. Alle Voraussetzungen werden in bestehenden Standard- bzw. Basismodul-Seiten gepflegt. Ein Administrator richtet sie einmalig ein, bevor der erste Nacharbeitsvorgang aus einer Produktionskampagne gebucht werden kann. Werden diese Werte nicht gepflegt, lässt sich beim Speichern einer Nacharbeitszeile keine Belegnummer vergeben, und der Vorgang bricht mit einer Fehlermeldung ab.

### Fertigungseinrichtung für die Nacharbeit einrichten

**Prozesseinstieg:** Diese Werte legt der Administrator vor der ersten Nutzung fest. Sie steuern, mit welchem Fertigungsauftragsstatus und aus welchen Nummernserien die Nacharbeit ihre Belege erzeugt. Der **Überarbeitungsdialog** (Kapitel **Tägliche Arbeit**) greift bei jeder Buchung auf diese Werte zu.

**Einstieg:** Die **Fertigungseinrichtung** ist eine firmenweite Einrichtungsseite (ein Datensatz je Mandant). Öffnen Sie sie über **Suchen** und geben Sie **Fertigungseinrichtung** ein.

| Einrichtung | Erläuterung |
|---|---|
| **Fertigungsstatus** | Wenn gesetzt, wird ein bei **Fertigung** neu erzeugter Fertigungsauftrag mit genau diesem Status angelegt (z. B. geplant, planfixiert oder freigegeben). Ohne gesetzten Status bricht das Speichern der Nacharbeitszeile ab, da das Modul den Zielstatus des neuen Auftrags nicht kennt. |
| **Schrottnummernserie** | Wenn gesetzt, vergibt das Modul beim Speichern einer Nacharbeitszeile mit Prozess **Schrott** aus dieser Serie automatisch eine Belegnummer. Fehlt die Serie, lässt sich kein Schrottvorgang speichern. |
| **Fertigungsnummernserie** | Wenn gesetzt, vergibt das Modul beim Speichern einer Nacharbeitszeile mit Prozess **Fertigung** aus dieser Serie automatisch eine Belegnummer. Fehlt die Serie, lässt sich kein Fertigungs-Nacharbeitsvorgang speichern. |

> Hinweis: Der Fertigungsstatus wird zusätzlich beim Auslesen des Zielstatus für den neuen Fertigungsauftrag verwendet. Er ist daher für den Prozess **Fertigung** immer erforderlich, unabhängig davon, ob im konkreten Fall ein Schrott- oder ein Fertigungsvorgang gebucht wird.

### Schrottlager freigeben (Lagerort und Lagerplatz)

**Prozesseinstieg:** Damit der Prozess **Schrott** im **Überarbeitungsdialog** einen Lagerort anbieten kann, muss der Administrator den betreffenden Lagerort (und bei Lagerplatzpflicht auch die Lagerplätze) ausdrücklich für den Schrottprozess freigeben. Ohne diese Freigabe erscheint der Lagerort nicht in der Auswahl **Junk-Standortcode**, und ein Schrottvorgang lässt sich nicht abschließen.

**Einstieg:** Öffnen Sie die **Lagerorte** (Übersicht), wählen Sie den gewünschten Lagerort und öffnen Sie die **Lagerortkarte**. Für lagerplatzpflichtige Lagerorte öffnen Sie zusätzlich die zugehörigen **Lagerplätze**.

| Einrichtung | Erläuterung |
|---|---|
| **Schrott erlauben** (Lagerort) | Wenn aktiviert, kann dieser Lagerort im Dialogfeld **Junk-Standortcode** ausgewählt werden. Ohne die Aktivierung steht der Lagerort für Schrott nicht zur Verfügung, und der Anwender kann den Schrottvorgang nicht speichern. |
| **Schrott erlauben** (Lagerplatz) | Wenn aktiviert, kann dieser Lagerplatz im Dialogfeld **Junk-Bin-Code** ausgewählt werden. Ist der gewählte Lagerort lagerplatzpflichtig, ist ein freigegebener Lagerplatz zwingend erforderlich, damit der Dialog geschlossen werden kann. |

### Berechtigungen

Die Erweiterung liefert den Berechtigungssatz **MuM PCRW All** („All permissions“). Er legt fest, welche Aktionen Anwender in der Nacharbeit der Produktionskampagne ausführen dürfen: Lese- und Schreibzugriff auf die Nacharbeitslinie sowie die Ausführung der zugehörigen Codeunits und Seiten (Überarbeitungsdialog und Assistent **Kampagnenzeilen aktualisieren**). Weisen Sie diesen Berechtigungssatz den Anwendern zu, die aus Produktionskampagnen Nacharbeit buchen sollen; ohne diese Berechtigungen bleibt die Aktion **Nacharbeiten** wirkungslos.

## Tägliche Arbeit in der Produktionskampagne

Die gesamte tägliche Arbeit dieser Erweiterung findet auf der bestehenden Seite **Produktionskampagne** statt. Die Erweiterung ändert die Grundlogik der Kampagne nicht, sondern ergänzt ein Kennzeichen im Kopf und eine Aktion in den Zeilen. Die eigentliche Erfassung erfolgt anschließend im **Überarbeitungsdialog**.

Voraussetzung ist, dass die Kampagnenzeile bereits mit einem Fertigungsauftrag verknüpft ist. Das Modul liest beim Start der Aktion die Zeile, den zugehörigen Fertigungsauftrag, den Arbeitsgang und die verfügbare Kampagnenmenge aus. Prüfen Sie vor dem Start deshalb mindestens: Kampagnennr., FA-Status, FA-Nr., Arbeitsgang und die aktuelle Kampagnenmenge der Zeile.

### Kennzeichen im Kampagnenkopf

Die Erweiterung fügt im Kopf der **Produktionskampagne** ein einziges Feld hinzu.

| Feld | Erläuterung |
|---|---|
| **Nacharbeiten** | Wenn gesetzt, existiert für diese Kampagne bereits mindestens ein verbuchter Nacharbeitsvorgang mit Kampagnenbezug. Das Feld wird automatisch berechnet und ist nicht editierbar; es dient als schnelle Sichtprüfung, ob an der Kampagne schon nachgearbeitet wurde. Ist es leer, wurde für diese Kampagne noch keine Nacharbeit mit Kampagnenverbindung gebucht. |

### Aktion Nacharbeiten in den Kampagnenzeilen

In den Kampagnenzeilen ergänzt die Erweiterung die Aktion **Nacharbeiten**. Sie ist die einzige benutzergesteuerte Aktion dieses Moduls im Tagesablauf.

Öffnen Sie über die Aktion **Nacharbeiten** den **Überarbeitungsdialog**: Markieren Sie eine oder mehrere Kampagnenzeilen und wählen Sie **Nacharbeiten**. Das Modul erzeugt daraufhin je markierter Zeile eine temporäre Nacharbeitslinie und übernimmt Artikel, Variante, Einheit, Beschreibung, verfügbare Menge sowie die Herkunft (Kampagnennr. und Zeilennr.) automatisch in den Dialog. Erst nach dem Bestätigen des Dialogs entstehen daraus echte Nacharbeitsbelege, die unmittelbar verbucht werden.

### Der Überarbeitungsdialog

Der **Überarbeitungsdialog** ist die zentrale Erfassungsmaske der Nacharbeit. Beim Öffnen wird die **Art der Produktionsüberarbeitung** standardmäßig auf **Artikel** gesetzt, und das System zeigt einen Hinweis: Wird die Nacharbeit als **Schrott** aus einer Produktionskampagne ausgeführt, verschiebt das Modul den Artikel **nicht** automatisch an den Schrottlagerort. Stattdessen wird die Menge der Fertigungsauftragszeile reduziert und der Vorgang in der Nacharbeitslogik protokolliert.

Der Dialog ist in drei Bereiche gegliedert: den Kopfbereich **Allgemein**, den Bereich **Informationen zum Ursprungsdokument** und den Zeilenbereich **Zeilen**.

#### Kopf- und Herkunftsfelder (Allgemein, Informationen zum Ursprungsdokument)

| Feld | Erläuterung |
|---|---|
| **Beschreibung** | Beschreibung des betroffenen Artikels bzw. Vorgangs. Nur Anzeige; wird aus der Kampagnenzeile übernommen. |
| **Variantencode** | Variante des Artikels. Nur Anzeige; stammt aus der verknüpften Fertigungsauftragszeile. |
| **Maßeinheitscode** | Verwendete Mengeneinheit. Nur Anzeige; stammt aus der Fertigungsauftragszeile und bestimmt die Umrechnung auf die Basismenge. |
| **Ursprungsprozess** | Nur Anzeige. Zeigt, aus welchem Prozess die Nacharbeit stammt. Beim Einstieg aus der Produktionskampagne steht hier **In der Fertigung**. Weitere Werte der zugrunde liegenden Nacharbeitslogik sind **Im Verkauf** und **Nach der Fertigung**. |
| **Ursprungsdokumenttyp** | Nur Anzeige. Kennzeichnet die Herkunft des Datensatzes. Für die Kampagnennacharbeit steht hier **Produktionskampagne**; die zugrunde liegende Logik kennt außerdem **Verkauf** und **Fertigung**. |
| **Ursprungsdokumentnr.** | Nur Anzeige. Nummer des Ursprungsdokuments – hier die Kampagnennr. der markierten Zeile. |

Zur Bedeutung der Optionswerte im Kopfbereich:

- **Ursprungsprozess** – **In der Fertigung:** Die Nacharbeit stammt aus einem laufenden Fertigungsvorgang; dies ist der Fall beim Einstieg über die Produktionskampagne. **Im Verkauf:** Die Nacharbeit wäre aus dem Verkauf ausgelöst worden. **Nach der Fertigung:** Die Nacharbeit bezieht sich auf bereits fertig gemeldete Ware.
- **Ursprungsdokumenttyp** – **Produktionskampagne:** von dieser Erweiterung ergänzter Wert; kennzeichnet Nacharbeit mit Kampagnenbezug und steuert, dass die kampagnenspezifische Buchungslogik greift. **Verkauf** / **Fertigung:** Herkunft aus dem Verkaufs- bzw. Fertigungsumfeld der Basislogik.

#### Zeilenfelder (Zeilen)

Im Bereich **Zeilen** erfassen Sie je nachzuarbeitendem Vorgang eine Zeile. Pflichtfelder sind gekennzeichnet und werden beim Schließen des Dialogs geprüft.

| Feld | Erläuterung |
|---|---|
| **Ursprungszeilennr.** | Nur Anzeige. Verweist auf die ursprüngliche Kampagnenzeile, aus der die Nacharbeitsmenge stammt. |
| **Artikelnr.** | Nur Anzeige. Betroffener Artikel der Kampagnenzeile. |
| **Nacharbeitsfehlertypcode** | Pflichtfeld. Wenn Sie einen Fehlertyp aus den gepflegten Nacharbeitsarten wählen, übernimmt das Modul automatisch den im Fehlertyp hinterlegten **Nacharbeitsprozess** (Schrott oder Fertigung) in die Zeile und steuert damit, welche weiteren Felder verpflichtend werden. |
| **Beschreibung des Nacharbeitsfehlertyps** | Nur Anzeige. Klartext zum gewählten Fehlertyp; wird beim Setzen des Fehlertyps berechnet. |
| **Ursachencode für Nacharbeitsfehler** | Pflichtfeld. Wenn Sie eine Fehlerursache aus den gepflegten Gründen wählen, wird der Vorgang dieser Ursache zugeordnet; ohne Ursache lässt sich der Dialog nicht schließen. |
| **Beschreibung des Nacharbeitsfehlergrunds** | Nur Anzeige. Klartext zur gewählten Fehlerursache; wird beim Setzen der Ursache berechnet. |
| **Nacharbeitsprozess** | Nur Anzeige, wird aus dem Fehlertyp abgeleitet. Bestimmt den gesamten weiteren Ablauf (siehe Optionswerte unten). |
| **Nacharbeitsursache** | Gibt an, wer oder was die Nacharbeit ausgelöst hat. Wenn Sie hier den Verursacher setzen, dokumentieren Sie die Verantwortlichkeit für Auswertungen (siehe Optionswerte unten). |
| **Art der Produktionsüberarbeitung** | Nur Anzeige. Beim Öffnen aus der Kampagne immer **Artikel**. Die zugrunde liegende Logik kennt außerdem **Komponente**; in diesem Einstieg bleibt es beim Artikelbezug, sodass die Nacharbeit auf den Produktionsartikel wirkt. |
| **Junk-Standortcode** | Nur bei Prozess **Schrott** editierbar und dann Pflichtfeld. Wenn Sie einen für Schrott freigegebenen Lagerort wählen, wird dieser für die Nacharbeitsdaten hinterlegt; ändert sich der Lagerort, wird ein zuvor gewählter Lagerplatz zurückgesetzt. |
| **Junk-Bin-Code** | Nur bei Prozess **Schrott** editierbar. Wenn der gewählte Schrottlagerort lagerplatzpflichtig ist, wird dieses Feld zum Pflichtfeld; nur ein für Schrott freigegebener Lagerplatz des gewählten Lagerorts ist zulässig. |
| **Menge** | Pflichtfeld. Wenn Sie die nachzuarbeitende Menge erfassen, berechnet das Modul daraus die Basismenge. Die Menge darf nicht kleiner als 0 und nicht größer als die verbleibende zulässige Maximalmenge der Zeile sein; andernfalls erscheint ein Fehler. |
| **Menge (Basis)** | Basismenge des Vorgangs. Nur bei einem Einheitenfaktor größer 1 editierbar; sonst wird sie automatisch aus **Menge** berechnet. |
| **Alternative Routenführung** | Nur bei Prozess **Fertigung** editierbar. Wenn Sie hier einen zertifizierten Arbeitsplan angeben, erhält der neu erzeugte Nacharbeits-Fertigungsauftrag diesen Arbeitsplan statt der Routing-Daten des Ursprungsauftrags. Bei **Schrott** wird der Wert automatisch geleert. |

Optionswerte im Zeilenbereich:

- **Nacharbeitsprozess** – **Schrott:** Es wird **kein** neuer Fertigungsauftrag erzeugt. Das Modul reduziert die verbundenen Kampagnen- und Fertigungsmengen und protokolliert den Vorgang; **Junk-Standortcode** (und ggf. **Junk-Bin-Code**) sind Pflicht, **Alternative Routenführung** wird geleert. **Fertigung:** Das Modul legt einen neuen Fertigungsauftrag mit der Nacharbeitsmenge an; **Alternative Routenführung** ist optional wählbar, die Schrott-Lagerfelder werden geleert.
- **Nacharbeitsursache** – **Intern:** Der Fehler wurde intern verursacht. **Debitor:** Der Auslöser liegt beim Kunden. **Kreditor:** Der Auslöser liegt beim Lieferanten. Der Wert dient der Auswertung und Zuordnung der Verantwortlichkeit.
- **Art der Produktionsüberarbeitung** – **Artikel:** Die Nacharbeit bezieht sich auf den Produktionsartikel selbst (Standard in diesem Einstieg). **Komponente:** In der Basislogik möglicher, komponentenbezogener Fall; aus der Kampagne wird er nicht gesetzt.

#### Prüfungen beim Schließen des Dialogs

Beim Schließen mit **OK** prüft das Modul jede Zeile in fester Reihenfolge und verhindert das Schließen, bis alle Angaben vollständig und plausibel sind:

1. **Nacharbeitsfehlertypcode** muss gefüllt sein.
2. **Ursachencode für Nacharbeitsfehler** muss gefüllt sein.
3. **Artikelnr.** muss vorhanden sein.
4. **Menge** muss gefüllt sein.
5. Bei Prozess **Schrott** muss ein **Junk-Standortcode** vorhanden sein.
6. Ist der Schrottlagerort lagerplatzpflichtig, muss zusätzlich der **Junk-Bin-Code** gefüllt sein.
7. Arbeiten mehrere Zeilen mit demselben zugeordneten Artikelposten, darf deren Gesamtmenge die verbleibende Menge des Postens nicht übersteigen; andernfalls fordert das System, die Zeile zu löschen und den Posten erneut zuzuordnen.

Brechen Sie den Dialog ab, werden alle temporären Zeilen verworfen und keine Nacharbeit gebucht.

## Kampagnenzeilen aktualisieren (Assistent)

Der Assistent **Kampagnenzeilen aktualisieren** ist kein eigener Menüeinstieg, sondern öffnet sich automatisch während der Buchung, wenn die Nacharbeitsmenge nicht allein von der markierten Kampagnenzeile abgezogen werden kann.

### Wann der Assistent erscheint

Das Modul sucht nach weiteren Kampagnenzeilen, die zur selben Fertigungsauftragszeile und zum selben Arbeitsplan gehören. Betrifft dieselbe Fertigungsmenge mehrere Kampagnenzeilen desselben Arbeitsgangs und reicht die verbleibende Menge für die Nacharbeit nicht aus, muss die Reduzierung manuell auf die betroffenen Zeilen verteilt werden. In diesem Fall öffnet sich der Assistent. Ist keine manuelle Verteilung nötig, wird er übersprungen und die Nacharbeit direkt gebucht.

### Ablauf im Assistenten

Der Assistent führt in drei Schritten durch die Verteilung. Die Navigation erfolgt über **Rückwärts**, **Weiter** und **Abschließen**.

1. **Einführungsseite** mit dem Hinweis, dass die Menge zugehöriger Kampagnen manuell zu senken ist.
2. **Zeilenansicht** mit allen betroffenen Kampagnenzeilen zur Verteilung.
3. **Abschlussseite:** Mit **Abschließen** werden die Werte gespeichert und die Nacharbeit anschließend direkt verbucht.

### Felder in der Zeilenansicht

Die Zeilenansicht zeigt die betroffenen Kampagnenzeilen in einer dichten Tabelle. Bearbeitbar ist ausschließlich die Spalte **Neue Menge**; alle übrigen Spalten dienen der Kontrolle. Die beiden Summenfelder oberhalb der Tabelle steuern den Abschluss:

| Feld | Erläuterung |
|---|---|
| **Erforderliche Menge zur Senkung** | Nur Anzeige. Zielsumme, um die alle betroffenen Zeilen zusammen reduziert werden müssen. Der Assistent lässt sich nur abschließen, wenn dieser Wert exakt erreicht wird. |
| **Reduzierte Menge** (Kopf) | Nur Anzeige. Summiert die bereits erfassten Reduzierungen über alle betroffenen Zeilen. Der Wert wird farblich bewertet: passend bei exakter Übereinstimmung mit der erforderlichen Menge, abweichend bei Unter- oder Überdeckung. |
| **Neue Menge** | Einzige bearbeitbare Spalte. Wenn Sie hier die künftige Restmenge einer Zeile eintragen, berechnet das Modul die zugehörige **Reduzierte Menge** und aktualisiert die Gesamtsumme. Der Wert darf nicht kleiner als 0 und nicht größer als die bisherige Kampagnenmenge sein; andernfalls erscheint ein Fehler. |
| **Reduzierte Menge** (Zeile) | Nur Anzeige. Automatisch berechnete Absenkung der einzelnen Zeile (bisherige Kampagnenmenge minus **Neue Menge**). |
| **Kampagnennr.** | Nur Anzeige. Betroffene Kampagne. |
| **FA-Status**, **FA-Nr.**, **FA-Zeilennr.** | Nur Anzeige. Verknüpfter Fertigungsauftrag mit Status und Zeile. |
| **Arbeitsplan- bzw. Arbeitsgangbezug** | Nur Anzeige. Zeigt den zugeordneten Arbeitsplan und Arbeitsgang der Zeile, damit die Verteilung dem richtigen Vorgang zugeordnet werden kann. |
| **Artikelnr.**, **Artikelbeschreibung** | Nur Anzeige. Artikel und Beschreibung der Zeile. |
| **Kampagnenmenge** und **Fertigungsauftragsmenge** | Nur Anzeige. Bisherige Menge der Kampagnenzeile sowie die Gesamtmenge des zugehörigen Fertigungsauftrags als Vergleichsbasis. |
| **Weitere Kontrollspalten** (Art, Nr., Beschreibung, Arbeitsplatz, Startdatum/-zeit, Rüstzeit, Bearbeitungszeit, Wartezeit, Transportzeit) | Nur Anzeige. Übernommene Kennzahlen der Kampagnenzeile zur Orientierung bei der Verteilung. |

Der Abschluss ist nur möglich, wenn die Summe aller **Reduzierten Mengen** exakt der **Erforderlichen Menge zur Senkung** entspricht. Ist die Summe zu klein oder zu groß, zeigt das System eine Meldung und beendet den Vorgang nicht.

## Wirkung der Verbuchung

Nach dem Schließen des Dialogs bzw. dem Abschließen des Assistenten verbucht das Modul die Nacharbeit direkt. Die Wirkung hängt vom **Nacharbeitsprozess** ab.

### Nacharbeit in Fertigung

Bei Prozess **Fertigung** führt das Modul folgende Schritte aus:

1. Die ursprüngliche Kampagnenzeile und die verknüpfte Fertigungsauftragszeile werden gelesen.
2. Falls nötig, werden weitere Kampagnenzeilen über den Assistenten **Kampagnenzeilen aktualisieren** manuell reduziert.
3. Ein neuer **Fertigungsauftrag** wird mit der Nacharbeitsmenge und dem in der **Fertigungseinrichtung** hinterlegten **Fertigungsstatus** angelegt.
4. Die neue Fertigungsauftragszeile erhält dieselben Basisdaten wie die ursprüngliche Zeile; die fertig gemeldete Menge wird auf 0 gesetzt.
5. Ist eine **Alternative Routenführung** angegeben, wird deren Arbeitsplan für den neuen Auftrag verwendet und aus den zertifizierten Arbeitsplanzeilen aufgebaut. Andernfalls werden die Routing-Daten aus dem bestehenden Fertigungsauftrag übernommen.
6. Die Mengen der betroffenen Kampagnenzeilen und der ursprünglichen Fertigungsauftragszeile werden um die Nacharbeitsmenge reduziert.
7. Die ursprüngliche Kampagnenzeile wird zusätzlich als **Überarbeitet** gekennzeichnet.

### Nacharbeit zu Schrott

Bei Prozess **Schrott** wird **kein** neuer Fertigungsauftrag erzeugt. Das Modul reduziert die verbundenen Kampagnen- und Fertigungsmengen und protokolliert den Vorgang über die Nacharbeitslogik. Wie im Dialoghinweis angekündigt, erfolgt beim Einstieg aus der Produktionskampagne **keine** automatische Umlagerung des Materials in einen Schrottlagerort. Der Schrottlagerort wird für die Vollständigkeit der Nacharbeitsdaten benötigt; die eigentliche Wirkung besteht in der Mengenreduzierung und der Protokollierung.

### Automatische Mengenanpassung

Nach erfolgreicher Verbuchung passt die Erweiterung die Mengen systematisch an:

| Schritt | Erläuterung |
|---|---|
| Manuell reduzierte Nebenzeilen | Zeilen aus dem Assistenten werden auf ihre **Neue Menge** gesetzt. Ergibt sich dabei eine Menge von 0 oder kleiner, wird die Zeile gelöscht. |
| Weitere Zeilen derselben Kampagne | Betroffene verwandte Kampagnenzeilen werden um die Nacharbeitsmenge reduziert; bei Menge 0 oder kleiner wird die Zeile gelöscht. |
| Ursprüngliche Kampagnenzeile | Wird um die Nacharbeitsmenge reduziert und mit dem Kennzeichen **Überarbeitet** versehen; bei Menge 0 oder kleiner wird die Zeile gelöscht. |
| Fertigungsauftragszeile | Ihre Basismenge wird um die Nacharbeitsmenge reduziert. |
| Verknüpfte Kampagnenzeilen des Fertigungsauftrags | Erhalten die aktualisierte Fertigungsauftragsmenge als neue Bezugsmenge. |

## Historie und Nachverfolgung

Die Erweiterung besitzt **keine eigene Historienliste** und keinen eigenen Bericht. Die Nachverfolgung eines Nacharbeitsvorgangs erfolgt über die vorhandenen Stellen:

| Bereich | Erläuterung |
|---|---|
| **Produktionskampagne** | Das Kopfkennzeichen **Nacharbeiten** zeigt an, dass mindestens ein Nacharbeitsvorgang mit der Kampagne verbunden wurde; die reduzierten Mengen und das Zeilenkennzeichen **Überarbeitet** dokumentieren die betroffenen Zeilen. |
| **Nacharbeitsbeleg der Basislogik** | Bei der Verbuchung speichert das Modul die Verbindung zwischen Nacharbeitsvorgang und Produktionskampagne (Verbindungstyp und Verbindungsnr. = Kampagnennr.). Darüber erkennt die Nacharbeitslogik den kampagnenbezogenen Ursprung. |
| **Fertigungsauftrag** | Bei Nacharbeit in **Fertigung** bildet der neu angelegte Fertigungsauftrag die Nacharbeitsmenge ab und ist über den zugeordneten Ursprung nachvollziehbar. |

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Ablauf anhand realistischer Auslöser. Alle Bildschirme und Aktionen sind im Code der Erweiterung belegt.

### Nacharbeit wegen internem Fertigungsfehler

**Auslöser:** In der laufenden Fertigung meldet ein Mitarbeiter ein Qualitätsproblem an einem Artikel; die betroffene Menge soll erneut durch die Fertigung laufen.

**Einstieg in BC:** Die Fertigungssteuerung öffnet die Seite **Produktionskampagne**, springt in die betroffene Kampagne und wechselt in die Zeilen.

**Kernablauf:** Der Anwender markiert die betroffene Kampagnenzeile und wählt **Nacharbeiten**. Im **Überarbeitungsdialog** setzt er **Nacharbeitsfehlertypcode** (mit Prozess **Fertigung**) und **Ursachencode für Nacharbeitsfehler**, belässt den **Nacharbeitsprozess** auf **Fertigung**, erfasst die **Menge** und gibt bei Bedarf eine **Alternative Routenführung** an. Als **Nacharbeitsursache** wählt er **Intern**. Beim Schließen mit **OK** prüft das Modul die Pflichtfelder. Ist dieselbe Fertigungsmenge auf mehrere Kampagnen verteilt, öffnet sich **Kampagnenzeilen aktualisieren**; dort trägt der Anwender je Zeile die **Neue Menge** ein, bis die **Reduzierte Menge** der **Erforderlichen Menge zur Senkung** entspricht, und wählt **Abschließen**.

**Abschluss:** Das System legt einen neuen **Fertigungsauftrag** für die Nacharbeitsmenge an, reduziert die ursprüngliche Kampagnen- und Fertigungsmenge und kennzeichnet die Ursprungszeile als **Überarbeitet**. Das Kopfkennzeichen **Nacharbeiten** der Kampagne ist nun gesetzt.

### Ausschuss in einer Produktionskampagne buchen

**Auslöser:** Ein Teil der geplanten Menge ist unbrauchbar und kann nicht nachgearbeitet werden; er soll als Ausschuss behandelt werden.

**Einstieg in BC:** Der Anwender öffnet die betroffene **Produktionskampagne** und wählt in den Zeilen die passende Zeile.

**Kernablauf:** Über **Nacharbeiten** öffnet sich der **Überarbeitungsdialog**. Der Anwender wählt einen **Nacharbeitsfehlertypcode**, dessen hinterlegter **Nacharbeitsprozess** **Schrott** ist, sowie die Fehlerursache. Er füllt **Junk-Standortcode** und – bei lagerplatzpflichtigem Lagerort – **Junk-Bin-Code** sowie die **Menge**. Der Hinweis beim Öffnen erinnert daran, dass aus der Kampagne keine automatische Umlagerung in das Schrottlager erfolgt. Betrifft der Vorgang mehrere zusammenhängende Kampagnenzeilen, verteilt der Anwender die Senkung im Assistenten **Kampagnenzeilen aktualisieren**.

**Abschluss:** Das Modul reduziert die Kampagnen- und Fertigungsmengen und protokolliert den Schrottvorgang in der Nacharbeitslogik. Ein neuer Fertigungsauftrag entsteht nicht, und es wird kein Lagerzugang im Schrottlager gebucht.

### Nacharbeit über mehrere verteilte Kampagnenzeilen

**Auslöser:** Eine Produktionsmenge wurde auf mehrere Kampagnen bzw. Arbeitsgänge aufgeteilt; die Nacharbeit betrifft den gemeinsamen Ursprung.

**Einstieg in BC:** Einstieg über **Produktionskampagne**, danach Wechsel in die Zeilen und Start von **Nacharbeiten**.

**Kernablauf:** Im **Überarbeitungsdialog** erfasst der Anwender die Nacharbeitsmenge. Das Modul erkennt, dass die verbleibende Menge der markierten Zeile nicht ausreicht und weitere Kampagnenzeilen desselben Fertigungsauftrags manuell abgesenkt werden müssen, und öffnet **Kampagnenzeilen aktualisieren**. Der Anwender prüft je Zeile Kampagnennr., FA-Bezug, Arbeitsgang und bisherige Kampagnenmenge und trägt in **Neue Menge** die künftige Restmenge ein.

**Abschluss:** Erst wenn die **Reduzierte Menge** exakt der **Erforderlichen Menge zur Senkung** entspricht, lässt sich der Vorgang mit **Abschließen** beenden und die Nacharbeit verbuchen. Zeilen, deren Menge dadurch auf 0 sinkt, werden gelöscht.

## FAQ und Troubleshooting

### 1. Warum lässt sich der Überarbeitungsdialog nicht schließen?

Der Dialog prüft die Pflichtfelder strikt. In der Regel fehlen **Nacharbeitsfehlertypcode**, **Ursachencode für Nacharbeitsfehler**, **Artikelnr.** oder **Menge**; bei Prozess **Schrott** zusätzlich der **Junk-Standortcode** bzw. – bei lagerplatzpflichtigem Lagerort – der **Junk-Bin-Code**. Vervollständigen Sie die betreffende Zeile.

### 2. Warum ist das Feld Alternative Routenführung nicht editierbar?

Die **Alternative Routenführung** ist nur bei Prozess **Fertigung** freigeschaltet. Bei **Schrott** wird der Wert automatisch geleert, weil kein Fertigungsauftrag und damit kein Arbeitsplan erzeugt wird.

### 3. Warum wird bei Schrott kein Lagerzugang im Schrottlager erzeugt?

Der Dialog weist beim Öffnen ausdrücklich darauf hin: Beim Einstieg aus der Produktionskampagne führt der Schrottprozess **keine** automatische Umlagerung in einen Schrottlagerort aus. Das Modul reduziert stattdessen Produktions- und Kampagnenmengen und protokolliert den Vorgang in der Nacharbeitslogik. Der **Junk-Standortcode** wird nur für die Vollständigkeit der Nacharbeitsdaten benötigt.

### 4. Warum erscheint der Assistent Kampagnenzeilen aktualisieren nicht immer?

Der Assistent öffnet sich nur, wenn dieselbe Fertigungsauftragsmenge auf mehrere Kampagnenzeilen oder Arbeitsgänge verteilt ist und die Nacharbeitsmenge nicht allein von der markierten Zeile abgezogen werden kann. Ist keine manuelle Verteilung nötig, wird die Nacharbeit direkt verbucht.

### 5. Warum kann ich im Assistenten nicht einfach eine beliebige Neue Menge eintragen?

Die **Neue Menge** darf nicht kleiner als 0 und nicht größer als die bisherige Kampagnenmenge der Zeile sein. Zusätzlich muss die Summe aller **Reduzierten Mengen** exakt der **Erforderlichen Menge zur Senkung** entsprechen. Erst dann lässt sich **Abschließen** ausführen.

### 6. Warum meldet das System, die reduzierte Menge stimme nicht?

Beim Abschließen vergleicht das Modul die Summe der reduzierten Mengen mit der erforderlichen Senkungsmenge. Weicht die Summe ab (Unter- oder Überdeckung), erscheint eine Meldung mit beiden Werten, und der Vorgang wird nicht beendet. Passen Sie die **Neue Menge** in den betroffenen Zeilen an, bis die Kopfanzeige **Reduzierte Menge** als passend bewertet wird.

### 7. Warum wurde eine Kampagnenzeile nach der Verbuchung gelöscht?

Sinkt die verbleibende Kampagnenmenge einer Zeile durch die Nacharbeit auf 0 oder darunter, löscht das Modul diese Zeile automatisch. Das betrifft sowohl die Ursprungszeile als auch verwandte Zeilen derselben Fertigungsstruktur.

### 8. Warum kann ich keine größere Menge als angezeigt nacharbeiten?

Die **Menge** je Zeile ist auf die verbleibende zulässige Maximalmenge begrenzt, die aus der Kampagnenzeile abgeleitet wird. Zusätzlich prüft das Modul beim Schließen, ob die Gesamtmenge aller Zeilen mit demselben zugeordneten Artikelposten dessen verbleibende Menge nicht übersteigt. Ist das der Fall, löschen Sie die betreffende Zeile und ordnen Sie den Posten erneut zu, um die verfügbare Menge zu erhalten.

### 9. Warum lässt sich beim Speichern keine Nacharbeitszeile anlegen?

Beim Speichern vergibt das Modul eine Belegnummer aus der passenden Nummernserie und liest den Fertigungsstatus aus der **Fertigungseinrichtung**. Fehlt der **Fertigungsstatus**, die **Schrottnummernserie** (bei Schrott) oder die **Fertigungsnummernserie** (bei Fertigung), bricht der Vorgang mit einer Fehlermeldung ab. Ergänzen Sie die fehlenden Werte in der Fertigungseinrichtung.

### 10. Woran erkenne ich, dass eine Kampagne bereits nachgearbeitet wurde?

Das Kopffeld **Nacharbeiten** der Produktionskampagne ist gesetzt, sobald mindestens ein Nacharbeitsvorgang mit Kampagnenbezug gebucht wurde. Auf Zeilenebene ist die betroffene Zeile mit **Überarbeitet** gekennzeichnet und in ihrer Menge reduziert.
