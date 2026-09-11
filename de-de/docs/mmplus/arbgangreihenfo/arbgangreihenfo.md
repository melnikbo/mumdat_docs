---
title: Anwenderhandbuch m+m Routing Sequence
---

# Anwenderhandbuch m+m Routing Sequence

## Einleitung

Das Modul **m+m Routing Sequence** verwaltet für jede **Arbeitsplatzgruppe** die
**Reihenfolge**, in der die Arbeitsgänge freigegebener Fertigungsaufträge dort
abgearbeitet werden. Aus den Arbeitsgängen der freigegebenen Fertigungsaufträge
entsteht automatisch eine je Arbeitsplatzgruppe geführte Arbeitsliste. Auf der
Seite **Produktionsplanung** ordnet der Anwender diese Arbeitsgänge in die
gewünschte Bearbeitungsreihenfolge, ohne den Arbeitsplan des Fertigungsauftrags
selbst zu ändern.

Das Modul erzeugt **keine** eigenen Belege und bucht **nicht**. Es liefert eine
zusätzliche Steuerungssicht: Welcher Arbeitsgang wird an einer Arbeitsplatzgruppe
als Nächstes bearbeitet, welcher folgt danach. Die Liste wird vom System
automatisch gepflegt; sie wächst, verschiebt sich und leert sich in Abhängigkeit
davon, wie Arbeitsgänge in den Fertigungsaufträgen angelegt, geändert oder
erledigt werden.

**Zielgruppe:** Primär sind dies **operative** Anwender in Fertigungssteuerung
und Produktionsplanung, die täglich die Bearbeitungsreihenfolge an den
Arbeitsplatzgruppen festlegen und pflegen. Sekundär betrifft das Modul
Administratoren, die die Lizenzierung und die Berechtigungen einrichten. Ein
eigener Einrichtungsdialog ist nicht erforderlich; nach Installation, Lizenz und
Berechtigung steht die Funktion unmittelbar zur Verfügung.

**Kurzer Prozessüberblick:**

1. In einem **Freigegebenen Fertigungsauftrag** werden Arbeitsgänge angelegt, die
   auf eine **Arbeitsplatzgruppe** verweisen.
2. Für jeden solchen Arbeitsgang legt das System automatisch eine Zeile in der
   **Produktionsplanung** an und vergibt fortlaufend die nächste **Reihenfolge**
   innerhalb der Arbeitsplatzgruppe.
3. Der Anwender öffnet die Seite **Produktionsplanung** und passt bei Bedarf die
   **Reihenfolge** einzelner Zeilen an; das System sortiert die übrigen Zeilen der
   Arbeitsplatzgruppe automatisch nach.
4. Wird ein Arbeitsgang erledigt, geändert oder gelöscht, entfernt oder verschiebt
   das System die zugehörige Zeile automatisch und schließt entstehende Lücken in
   der Reihenfolge.

## Schnellstart für Anwender

Der schnellste Weg zu einer gepflegten Bearbeitungsreihenfolge:

1. **Voraussetzung Einrichtung:** Stellen Sie sicher, dass das Modul lizenziert
   ist und dass Ihr Benutzer die Berechtigung **Produktionsplanung** besitzt
   (siehe Kapitel **Einrichtung**). Ohne gültige Lizenz und Berechtigung ist die
   Seite nicht nutzbar.
2. **Arbeitsgänge erzeugen:** Legen Sie im **Freigegebenen Fertigungsauftrag**
   Arbeitsgänge an, die auf eine **Arbeitsplatzgruppe** verweisen. Für jeden
   dieser Arbeitsgänge entsteht automatisch eine Zeile in der Produktionsplanung.
3. **Liste öffnen:** Rufen Sie über **Suchen** die Seite **Produktionsplanung**
   auf. Die Seite ist eine eigenständige Liste und wird über die BC-Suche
   gefunden.
4. **Reihenfolge festlegen:** Wählen Sie die zu verschiebende Zeile und tragen Sie
   im Feld **Reihenfolge** die gewünschte Position ein. Das System verschiebt die
   dazwischenliegenden Zeilen der Arbeitsplatzgruppe automatisch und aktualisiert
   die Anzeige.
5. **Kontrolle:** Prüfen Sie die Sortierung: Die Liste ist je Arbeitsplatzgruppe
   nach **Reihenfolge** aufsteigend geordnet. Erledigte Arbeitsgänge sind nicht
   mehr enthalten.

Ein Buchungs- oder Freigabeschritt ist im Modul selbst nicht vorgesehen; die
Reihenfolgepflege ist der einzige Anwenderschritt. Alle weiteren Änderungen ergeben
sich automatisch aus der Arbeit am Fertigungsauftrag.

## Einrichtung

Das Modul benötigt **keine** eigene Einrichtungsseite und keine Nummernserie. Die
für den Betrieb erforderlichen Schritte betreffen ausschließlich **Lizenzierung**
und **Berechtigungen**. Beide werden vom Administrator vor der ersten Nutzung
erledigt und sind Voraussetzung für die tägliche Arbeit auf der Seite
**Produktionsplanung** (Kapitel **Tägliche Arbeit: Produktionsplanung**).

### Modul lizenzieren

**Prozessintro:** Die Lizenzprüfung wird vom Administrator eingerichtet und läuft
danach ohne weiteres Zutun. Sie stellt sicher, dass das Modul im aktuellen
Mandanten und für den jeweiligen Benutzer freigeschaltet ist. Die Prüfung erfolgt
über das Basismodul **m+m Cloud Base** und wird bei jeder Anmeldung ausgelöst. Ohne
gültige Zuordnung erhält der Anwender bei der Anmeldung einen Hinweis, und die
Nutzung des Moduls kann eingeschränkt werden.

Die Lizenzprüfung wertet je Modul einen **Lizenztyp** aus. Für jeden Wert ergibt
sich ein anderes Verhalten:

- **Pauschal (Flat-Rate):** Wenn dieser Lizenztyp gesetzt ist, gilt das Modul
  ohne weitere Zuordnung als freigeschaltet; es findet keine Prüfung je Mandant
  oder Benutzer statt.
- **Je Mandant (per Company):** Wenn dieser Lizenztyp gesetzt ist, muss der
  aktuelle Mandant dem Modul zugeordnet sein; fehlt die Zuordnung, meldet das
  System bei der Anmeldung, dass der Mandant dem Modul nicht zugewiesen ist.
- **Je Benutzer (per User):** Wenn dieser Lizenztyp gesetzt ist, muss der
  angemeldete Benutzer dem Modul zugeordnet sein; fehlt die Zuordnung, meldet das
  System, dass der Benutzer dem Modul nicht zugewiesen ist.

**Einstieg:** Die Lizenzverwaltung ist Bestandteil des Basismoduls **m+m Cloud
Base**; die Zuordnung von Mandanten und Benutzern erfolgt dort. Für dieses Modul
ist keine zusätzliche Seite einzurichten.

**Enablement-Schritte (in Abhängigkeitsreihenfolge):**

1. **Zuerst** installieren Sie das Modul zusammen mit seiner Abhängigkeit **m+m
   Cloud Base** im Mandanten. Wenn beide Apps installiert sind, kann die
   Lizenzprüfung bei der Anmeldung ausgeführt werden.
2. **Danach** ordnen Sie im Basismodul je nach Lizenztyp den **Mandanten** und/oder
   die **Benutzer** dem Modul zu. Wenn die Zuordnung vorhanden ist, meldet die
   Anmeldung keinen Lizenzhinweis mehr, und die Funktion steht bereit.
3. **Schließlich** meldet sich der Anwender an. Wenn Lizenz und Zuordnung gültig
   sind, kann er die Seite **Produktionsplanung** öffnen und die Reihenfolge
   pflegen (Kapitel **Tägliche Arbeit: Produktionsplanung**).

**Hinweis zur Betriebsart:** In On-Premises-Umgebungen wird die Lizenzprüfung
übersprungen; die Zuordnung ist dort nicht erforderlich. In der Cloud ist die
Zuordnung Voraussetzung für den ungestörten Betrieb.

### Berechtigungen vergeben

**Prozessintro:** Die Berechtigungsvergabe erfolgt durch den Administrator vor der
ersten Nutzung. Sie legt fest, welche Anwender die Produktionsplanung öffnen und
die Reihenfolge ändern dürfen. Ohne diese Berechtigung ist die Seite für den
Anwender nicht zugänglich, und die automatische Pflege im Hintergrund kann die
Planungsdaten nicht schreiben.

Das Modul liefert einen Berechtigungssatz mit, der alle für den Betrieb nötigen
Objekte abdeckt.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Berechtigungssatz **Produktionsplanung** | Wenn dieser Berechtigungssatz einem Benutzer oder einer Benutzergruppe zugewiesen ist, erhält dieser Vollzugriff (Lesen, Einfügen, Ändern, Löschen) auf die Planungsdaten sowie das Ausführungsrecht auf die Seite und die Verwaltungslogik des Moduls. Der Berechtigungssatz bestimmt damit, wer die Seite **Produktionsplanung** öffnen und die **Reihenfolge** pflegen darf und dass die automatische Pflege im Hintergrund die Zeilen anlegen, ändern und löschen kann. |

**Enablement-Schritte:**

1. **Zuerst** öffnet der Administrator die Berechtigungsverwaltung von Business
   Central.
2. **Danach** weist er den Berechtigungssatz **Produktionsplanung** den
   zuständigen Benutzern oder Benutzergruppen zu. Wenn die Zuweisung erfolgt ist,
   können diese Anwender die Seite öffnen und die Reihenfolge bearbeiten.
3. **Schließlich** kann der Anwender die tägliche Arbeit aufnehmen (Kapitel
   **Tägliche Arbeit: Produktionsplanung**).

## Tägliche Arbeit: Produktionsplanung

Die eigentliche Anwenderarbeit findet auf der Seite **Produktionsplanung** statt.
Sie zeigt je **Arbeitsplatzgruppe** die dort anstehenden Arbeitsgänge der
freigegebenen Fertigungsaufträge in der aktuellen Bearbeitungsreihenfolge. Der
Inhalt der Liste ist eine Folge der Arbeit im **Freigegebenen Fertigungsauftrag**:
Ob eine Zeile erscheint, verschwindet oder an eine andere Arbeitsplatzgruppe
wandert, steuert der Anwender über die Arbeitsgänge im Fertigungsauftrag. Die
**Reihenfolge** innerhalb einer Arbeitsplatzgruppe hingegen bestimmt der Anwender
direkt auf dieser Seite.

**Einstieg:** Rufen Sie die Seite **Produktionsplanung** über **Suchen** auf. Es
handelt sich um eine eigenständige Liste; ein übergeordneter Beleg oder eine
Einrichtungsseite als Einstieg ist nicht erforderlich.

Die Seite ist eine reine Bearbeitungsliste: Neue Zeilen können **nicht** manuell
angelegt und vorhandene Zeilen **nicht** manuell gelöscht werden. Diese
Änderungen ergeben sich ausschließlich aus der Arbeit am Fertigungsauftrag.
Änderbar ist ausschließlich die **Reihenfolge**.

### Felder der Liste

Die Liste ist je **Arbeitsplatzgruppe** aufsteigend nach **Reihenfolge** sortiert.

| Feld | Erläuterung |
|------|-------------|
| **Arbeitsplatzgruppennr.** | Wenn ein Arbeitsgang eines freigegebenen Fertigungsauftrags auf eine Arbeitsplatzgruppe verweist, wird deren Nummer hier geführt; sie gruppiert die Zeilen und ist der Bezug, innerhalb dessen die Reihenfolge gilt. Das Feld ist nicht editierbar und wird vom System aus dem Arbeitsgang übernommen. |
| **Reihenfolge** | Bestimmt die Bearbeitungsposition des Arbeitsgangs innerhalb der Arbeitsplatzgruppe. Wenn der Anwender diesen Wert ändert, verschiebt das System die dazwischenliegenden Zeilen der Arbeitsplatzgruppe automatisch und hält die Nummerierung lückenlos. Dies ist das einzige vom Anwender editierbare Feld. |
| **Zeilennr.** | Interne, lückenlos vergebene Ordnungsnummer des Datensatzes je Arbeitsplatzgruppe. Wenn eine neue Zeile entsteht, vergibt das System die nächste freie Zeilennr.; sie dient der eindeutigen Identifikation und ist nicht editierbar. |
| **Artikelnr.** | Zeigt den Artikel, der über den Fertigungsauftrag an diesem Arbeitsgang gefertigt wird. Wenn die Zeile angelegt wird, übernimmt das System die Artikelnr. aus der Fertigungsauftragszeile; so erkennt der Anwender, welches Erzeugnis hinter dem Arbeitsgang steht. Das Feld ist nicht editierbar. |
| **FA-Nr.** | Zeigt die Nummer des freigegebenen Fertigungsauftrags, aus dem der Arbeitsgang stammt. Wenn die Zeile angelegt wird, übernimmt das System die FA-Nr. aus dem Arbeitsgang; darüber navigiert der Anwender gedanklich zurück zum Auftrag. Das Feld ist nicht editierbar. |

Die Liste enthält keine weiteren, benutzerdefinierten Filterfelder über die
Standard-BC-Listenfilterung hinaus. Eine Filterung ist über die
Standard-Spaltenfilter möglich, insbesondere nach **Arbeitsplatzgruppennr.**, um
die Sicht auf eine einzelne Arbeitsplatzgruppe einzugrenzen.

### Reihenfolge ändern

Das Ändern der **Reihenfolge** ist der zentrale Anwenderschritt.

1. Wählen Sie in der Liste **Produktionsplanung** die Zeile, deren Position Sie
   ändern möchten.
2. Tragen Sie im Feld **Reihenfolge** die gewünschte Zielposition ein.
3. Das System prüft und begrenzt den Wert automatisch auf den gültigen Bereich der
   Arbeitsplatzgruppe: Liegt der eingegebene Wert unterhalb der kleinsten
   vorhandenen Reihenfolge, wird die Zeile an den Anfang gesetzt; liegt er oberhalb
   der größten vorhandenen Reihenfolge, an das Ende.
4. Das System verschiebt die dazwischenliegenden Zeilen der Arbeitsplatzgruppe um
   eine Position und aktualisiert die Anzeige. Verschieben Sie eine Zeile nach
   hinten, rücken die übersprungenen Zeilen um eine Position nach vorn; verschieben
   Sie sie nach vorn, rücken die übersprungenen Zeilen um eine Position nach hinten.

Auf diese Weise bleibt die Nummerierung innerhalb der Arbeitsplatzgruppe stets
lückenlos, und keine zwei Arbeitsgänge belegen dieselbe Position.

### Automatische Pflege der Liste (Hintergrundverhalten)

Der Anwender legt Zeilen nicht selbst an; das System pflegt die Liste anhand der
Arbeitsgänge im **Freigegebenen Fertigungsauftrag**. Nur Arbeitsgänge vom Typ
Arbeitsplatzgruppe werden berücksichtigt. Das Verständnis dieses Verhaltens
erleichtert die tägliche Arbeit:

- **Neuer Arbeitsgang:** Wenn im freigegebenen Fertigungsauftrag ein Arbeitsgang
  mit Bezug auf eine Arbeitsplatzgruppe angelegt wird, erzeugt das System eine
  neue Zeile und hängt sie mit der nächsthöheren **Reihenfolge** an das Ende der
  Arbeitsplatzgruppe an. Artikelnr. und FA-Nr. werden dabei aus dem Auftrag
  übernommen.
- **Arbeitsplatzgruppe gewechselt:** Wenn an einem bestehenden Arbeitsgang die
  Arbeitsplatzgruppe geändert wird, verschiebt das System die zugehörigen Zeilen
  in die neue Arbeitsplatzgruppe, vergibt dort neue, an das Ende angehängte
  Reihenfolgen und schließt die entstandene Lücke in der bisherigen
  Arbeitsplatzgruppe.
- **Arbeitsgang erledigt:** Wenn der Arbeitsplanstatus des Arbeitsgangs auf
  **erledigt** wechselt, entfernt das System die zugehörige Zeile aus der
  Produktionsplanung und schließt die Lücke in der Reihenfolge der
  Arbeitsplatzgruppe.
- **Arbeitsgang gelöscht:** Wenn ein Arbeitsgang gelöscht wird, entfernt das System
  die zugehörige Zeile und schließt ebenfalls die Lücke in der Reihenfolge.

In allen Fällen bleibt die Reihenfolge je Arbeitsplatzgruppe lückenlos und
konsistent, ohne dass der Anwender manuell eingreifen muss.

## FAQ und Troubleshooting

### 1. Warum kann ich in der Produktionsplanung keine neue Zeile anlegen?

Die Seite erlaubt kein manuelles Einfügen. Zeilen entstehen ausschließlich
automatisch, sobald im **Freigegebenen Fertigungsauftrag** ein Arbeitsgang mit
Bezug auf eine **Arbeitsplatzgruppe** angelegt wird. Legen Sie den Arbeitsgang im
Fertigungsauftrag an; die passende Zeile erscheint dann von selbst.

### 2. Warum kann ich eine Zeile nicht löschen?

Das Löschen ist auf der Seite gesperrt. Eine Zeile verschwindet erst, wenn der
zugehörige Arbeitsgang erledigt oder im Fertigungsauftrag gelöscht wird. So bleibt
die Planung immer im Einklang mit den tatsächlich vorhandenen Arbeitsgängen.

### 3. Welche Felder kann ich überhaupt bearbeiten?

Nur das Feld **Reihenfolge**. Alle übrigen Felder — **Arbeitsplatzgruppennr.**,
**Zeilennr.**, **Artikelnr.** und **FA-Nr.** — werden vom System gefüllt und sind
nicht editierbar.

### 4. Was passiert, wenn ich eine sehr hohe oder sehr niedrige Reihenfolge eintrage?

Das System begrenzt den Wert automatisch auf den gültigen Bereich der
Arbeitsplatzgruppe. Ein Wert unterhalb der kleinsten vorhandenen Reihenfolge setzt
die Zeile an den Anfang, ein Wert oberhalb der größten vorhandenen Reihenfolge an
das Ende. Ungültige Positionen außerhalb der Liste können so nicht entstehen.

### 5. Warum verschieben sich beim Ändern einer Reihenfolge auch andere Zeilen?

Weil die Reihenfolge innerhalb einer Arbeitsplatzgruppe lückenlos bleiben muss.
Wenn Sie eine Zeile an eine andere Position setzen, rücken die dazwischenliegenden
Zeilen automatisch um eine Position nach, damit keine Doppelbelegung und keine
Lücke entsteht.

### 6. Warum taucht ein Arbeitsgang nicht in der Produktionsplanung auf?

Berücksichtigt werden ausschließlich Arbeitsgänge, die auf eine
**Arbeitsplatzgruppe** verweisen. Arbeitsgänge anderer Art werden nicht in die
Produktionsplanung übernommen. Prüfen Sie den betreffenden Arbeitsgang im
Fertigungsauftrag.

### 7. Warum ist ein zuvor sichtbarer Arbeitsgang plötzlich aus der Liste verschwunden?

Das geschieht, wenn der Arbeitsplanstatus des Arbeitsgangs auf **erledigt**
gesetzt oder der Arbeitsgang gelöscht wurde. In beiden Fällen entfernt das System
die Zeile und schließt die Lücke in der Reihenfolge.

### 8. Was passiert mit der Reihenfolge, wenn ich einen Arbeitsgang auf eine andere Arbeitsplatzgruppe umstelle?

Das System entfernt die Zeile aus der bisherigen Arbeitsplatzgruppe, schließt dort
die Lücke und legt sie in der neuen Arbeitsplatzgruppe mit einer an das Ende
angehängten **Reihenfolge** neu an. Eine zuvor gesetzte Position in der alten
Arbeitsplatzgruppe geht dabei verloren.

### 9. Warum erhalte ich bei der Anmeldung einen Lizenzhinweis, und was bedeutet er?

Das Modul prüft bei jeder Anmeldung über das Basismodul **m+m Cloud Base** die
Lizenz. Ein Hinweis erscheint, wenn der Mandant oder der Benutzer dem Modul nicht
zugeordnet ist oder eine Zahlung offen ist. Lassen Sie die Zuordnung durch den
Administrator im Basismodul prüfen und ergänzen.

### 10. Warum kann ein Anwender die Seite Produktionsplanung nicht öffnen?

In der Regel fehlt die Berechtigung. Weisen Sie dem Benutzer den
Berechtigungssatz **Produktionsplanung** zu. Ohne diese Berechtigung ist die Seite
nicht zugänglich, und die automatische Pflege im Hintergrund kann keine Zeilen
schreiben.

## Typische Anwendungsfälle

### Anwendungsfall 1: Reihenfolge an einer Arbeitsplatzgruppe umstellen

**Auslöser:** Ein Meister der Fertigung meldet telefonisch, dass ein eiliger
Auftrag an einer Arbeitsplatzgruppe vorgezogen werden soll.

**Einstieg in BC:** Der Planer öffnet über **Suchen** die Seite
**Produktionsplanung** und filtert über den Spaltenfilter auf die betreffende
**Arbeitsplatzgruppennr.**, um nur deren Arbeitsgänge zu sehen.

**Kernablauf:**

1. Der Planer sucht in der gefilterten Liste die Zeile des vorzuziehenden
   Arbeitsgangs (Orientierung über **Artikelnr.** und **FA-Nr.**).
2. Er trägt im Feld **Reihenfolge** die gewünschte vordere Position ein.
3. Das System begrenzt den Wert auf den gültigen Bereich, verschiebt die
   dazwischenliegenden Zeilen automatisch nach hinten und aktualisiert die
   Anzeige.

**Abschluss:** Die Arbeitsplatzgruppe zeigt nun die neue Bearbeitungsreihenfolge;
der vorgezogene Arbeitsgang steht an der gewünschten Position, alle übrigen bleiben
lückenlos einsortiert. Ein Buchungsschritt ist nicht erforderlich.

### Anwendungsfall 2: Neuer Fertigungsauftrag reiht sich automatisch ein

**Auslöser:** Die Fertigungssteuerung gibt aufgrund einer neuen Bedarfsmeldung
einen weiteren Fertigungsauftrag frei.

**Einstieg in BC:** Der Sachbearbeiter arbeitet im **Freigegebenen
Fertigungsauftrag** und legt die Arbeitsgänge des Auftrags an; jeder Arbeitsgang
verweist auf eine **Arbeitsplatzgruppe**.

**Kernablauf:**

1. Mit dem Anlegen jedes Arbeitsgangs erzeugt das System automatisch eine Zeile in
   der **Produktionsplanung** und hängt sie mit der nächsten **Reihenfolge** an das
   Ende der jeweiligen Arbeitsplatzgruppe an; **Artikelnr.** und **FA-Nr.** werden
   aus dem Auftrag übernommen.
2. Der Planer öffnet über **Suchen** die **Produktionsplanung** und prüft, an
   welche Position die neuen Arbeitsgänge eingereiht wurden.
3. Bei Bedarf passt er einzelne **Reihenfolge**-Werte an, um den neuen Auftrag vor-
   oder zurückzustellen; das System sortiert automatisch nach.

**Abschluss:** Der neue Auftrag ist ohne manuelle Zeilenanlage in die
Bearbeitungsreihenfolge der betroffenen Arbeitsplatzgruppen eingegliedert. Werden
seine Arbeitsgänge später erledigt, entfernt das System die zugehörigen Zeilen
automatisch.
