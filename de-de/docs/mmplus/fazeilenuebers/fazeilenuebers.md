---
title: Anwenderhandbuch m+m Production Order Overview
---

# Anwenderhandbuch m+m Production Order Overview

## Einleitung

Die App **m+m Production Order Overview** erweitert Microsoft Dynamics 365 Business Central um eine zentrale Übersicht aller Fertigungsauftragszeilen (FA-Zeilen). Standardmäßig verteilt Business Central diese Informationen über mehrere Belegarten (Simuliert, Geplant, Fest geplant, Freigegeben, Beendet) und über den jeweiligen Fertigungsauftragskopf. Die **FA-Zeilenübersicht** führt alle FA-Zeilen dieser Statuswerte auf **einer** Seite zusammen und macht die zu einer Zeile gehörenden **FA-Komponenten**, **Arbeitsgänge** und **Verkaufszeilen** sofort sichtbar.

**Zielgruppe:** Primär richtet sich die App an **operative Anwender in der Fertigung** – Fertigungssteuerung, Arbeitsvorbereitung und Werker, die täglich mit offenen und freigegebenen Fertigungsaufträgen arbeiten, Mengen prüfen, Status ändern und aus der Übersicht heraus in das Produktionsbuchungsblatt und die Arbeitsgänge springen. Sekundär profitieren Planer und Disponenten, die sich einen gefilterten Gesamtüberblick über den Bestand an Fertigungsauftragszeilen verschaffen.

**Kurzer Prozessüberblick:** Der Anwender öffnet die **FA-Zeilenübersicht**, wählt in der oberen Tabelle eine FA-Zeile aus und sieht darunter automatisch die zugeordneten Komponenten und Verkaufszeilen sowie – im Infobereich rechts – die Arbeitsgänge der Zeile. Aus derselben Seite heraus ruft er ohne Umweg über den Belegkopf die wichtigsten Funktionen eines Fertigungsauftrags auf: Beleg anzeigen, Status ändern, Komponenten öffnen, Produktionsbuchungsblatt starten und Arbeitsgänge öffnen. Über das Filtersymbol filtert er die Ansicht nach eigenen Kriterien und speichert diese Ansichten als persönliche Ansichten.

Diese App bringt **keine eigenen Einrichtungsseiten, keine eigenen Stammdaten und keine eigene Buchungsroutine** mit. Sie ist eine reine Auswertungs- und Steuerungsoberfläche auf den Standardtabellen von Business Central. Alle aufgerufenen Funktionen (Statusänderung, Buchungsblatt, Arbeitsgänge, Beleganzeige) sind Standardfunktionen von Business Central, die lediglich aus der Übersicht heraus zugänglich gemacht werden.

## Schnellstart für Anwender

Der schnellste Weg zu den wichtigsten Ergebnissen:

1. **FA-Zeilenübersicht öffnen.** Rufen Sie die Seite **FA-Zeilenübersicht** über die Business-Central-Suche (**Suche**) auf. Die Seite ist als Listenseite unter der Nutzungskategorie *Listen* auffindbar und benötigt keine vorherige Einrichtung.
2. **FA-Zeile auswählen.** Markieren Sie in der oberen Tabelle die gewünschte Fertigungsauftragszeile. Die Ansicht zeigt standardmäßig alle Zeilen ab Status **Geplant** aufwärts (**Geplant**, **Fest geplant**, **Freigegeben**, **Beendet**), sortiert nach Status, **FA-Nr.** und **Zeilennr.**.
3. **Zugeordnete Daten lesen.** Sobald Sie eine FA-Zeile markieren, füllen sich der mittlere Bereich **FA-Komponenten** und der untere Bereich **Verkaufszeilen** automatisch mit den zur Zeile gehörenden Daten. Rechts zeigt der Infobereich **Arbeitsgänge zur FA-Zeile** die Arbeitsgänge der markierten Zeile.
4. **Funktion ausführen.** Rufen Sie bei Bedarf über die Menüband-Aktionen eine der folgenden Standardfunktionen auf: **Beleg anzeigen**, **Status ändern**, **Komponenten**, **Prod. Buch. Blatt** oder **Arbeitsgänge**.
5. **Ansicht filtern und speichern.** Setzen Sie über das Filtersymbol einen Filter (zum Beispiel **Status** = **Freigegeben**) und speichern Sie das Ergebnis als persönliche Ansicht, um es später erneut aufzurufen.

> Die App erzwingt keine feste Reihenfolge von Einrichtungsschritten. Da sie ausschließlich auf Standardtabellen aufsetzt, sind Fertigungsaufträge und deren Zeilen die einzige Voraussetzung; diese entstehen im Standardprozess von Business Central.

## Aufbau der FA-Zeilenübersicht

Die Seite **FA-Zeilenübersicht** (Seitentyp Liste, Quelltabelle *Fertigungsauftragszeile*) ist in drei übereinander liegende Bereiche gegliedert und um einen Infobereich rechts ergänzt. Der obere Bereich ist die eigentliche Liste der FA-Zeilen; die beiden unteren Bereiche und der Infobereich sind Unterseiten, die sich beim Wechsel der markierten FA-Zeile automatisch aktualisieren.

Die Datensatzauswahl der oberen Liste ist über die Quelltabellenansicht fest auf FA-Zeilen ab Status **Geplant** eingegrenzt (`where(Status = filter(Planned ..))`); simulierte Zeilen erscheinen daher nur, wenn deren Status entsprechend gesetzt ist. Neuanlage und Löschen sind in der Übersicht gesperrt; Bearbeiten ist grundsätzlich zugelassen, in den Feldern jedoch überwiegend deaktiviert (siehe Abschnitt **FA-Zeilen bearbeiten**).

### Oberer Bereich – FA-Zeilen

Der obere Bereich listet die Fertigungsauftragszeilen tabellarisch auf. Die folgende Tabelle beschreibt die fachlich wichtigsten Spalten; die vollständige Spaltenmenge entspricht den Feldern der Standardtabelle *Fertigungsauftragszeile* und lässt sich über die Personalisierung ein- und ausblenden.

| Feld | Erläuterung |
|------|-------------|
| **Status** | Zeigt den Fertigungsauftragsstatus der Zeile. Der Wert steuert, welche Funktionen erlaubt sind und ob die Zeile im **Prod. Buch. Blatt** bebucht werden kann. Mögliche Werte: **Simuliert:** unverbindliche Simulation, keine Buchung; **Geplant:** aus der Planung erzeugt, noch nicht bestätigt; **Fest geplant:** verbindlich eingeplant, noch nicht freigegeben; **Freigegeben:** zur Fertigung freigegeben – erst in diesem Status ist das **Prod. Buch. Blatt** möglich; **Beendet:** abgeschlossen, keine weiteren Buchungen. |
| **FA-Nr.** | Nummer des Fertigungsauftrags, zu dem die Zeile gehört. Dient als Sprungziel für **Beleg anzeigen** und als Filterkriterium für die zugeordneten Komponenten und Verkaufszeilen. |
| **Zeilennr.** | Laufende Nummer der Zeile innerhalb des Fertigungsauftrags. Bestimmt zusammen mit **FA-Nr.** und **Status**, welche Komponenten und Arbeitsgänge im unteren Bereich und im Infobereich angezeigt werden. |
| **Artikelnr.** | Der zu fertigende Artikel der Zeile. |
| **Variante** | Artikelvariante der Zeile, sofern der Artikel mit Varianten geführt wird. |
| **Beschreibung** / **Beschreibung 2** | Bezeichnung des Artikels aus der Zeile. |
| **Lagerortcode** | Lagerort, dem die Fertigung der Zeile zugeordnet ist. |
| **Menge** | Sollmenge der Fertigungsauftragszeile. |
| **Gebuchte Menge** | Bereits als Ausbringung zurückgemeldete Menge. Steigt mit jeder Ausgabebuchung; wenn sie die **Menge** erreicht, ist die Zeile mengenmäßig fertiggestellt. |
| **Restmenge** | Noch offene Menge (Sollmenge abzüglich gebuchter Menge). Sinkt mit jeder Rückmeldung; bei Null ist nichts mehr zu fertigen. |
| **Rüstprozentsatz** | Ausschussaufschlag in Prozent, der bei der Mengenberechnung berücksichtigt wird. |
| **Fälligkeitsdatum**, **Startdatum**/**Startzeit**, **Endedatum**/**Endezeit** | Terminfelder der Zeile aus der Feinplanung. |
| **Arbeitsplannr.** | Zugeordneter Arbeitsplan. Dieses Feld ist in den Status **Simuliert**, **Geplant** und **Fest geplant** editierbar; siehe **FA-Zeilen bearbeiten**. |
| **Prod.-Stücklistennr.** | Zugeordnete Fertigungsstückliste der Zeile. |
| **Einstandspreis**, **Kostenbetrag**, **Erwartete Arbeitsgangkosten**, **Erwartete Komponentenkosten** | Wert- und Kostenfelder der Zeile zur Kostenkontrolle. |

Alle Felder des oberen Bereichs sind standardmäßig **nicht editierbar** und dienen der Anzeige. Einzige Ausnahme ist die **Arbeitsplannr.** in den planbaren Status (siehe unten).

#### FA-Zeilen bearbeiten

Die Übersicht lässt in den Status **Simuliert**, **Geplant** und **Fest geplant** die Bearbeitung der **Arbeitsplannr.** direkt in der Zeile zu; in den Status **Freigegeben** und **Beendet** ist dieses Feld gesperrt. Wenn Sie die **Arbeitsplannr.** in einem planbaren Status ändern, erscheint die Rückfrage **„Möchten Sie den FA neu berechnen?“**:

- Bestätigen Sie die Rückfrage, dann übernimmt die App die neue **Arbeitsplannr.** in den Fertigungsauftrag und berechnet den Auftrag rückwärts neu (Arbeitsplan wird neu ermittelt; Komponenten und Fälligkeit bleiben unverändert). Die Ansicht wird anschließend aktualisiert.
- Lehnen Sie die Rückfrage ab, dann wird die Änderung nicht ausgeführt.

### Mittlerer Bereich – FA-Komponenten

Der mittlere Bereich **Zugeordnete FA-Komponente** (Unterseite auf der Standardtabelle *Fertigungsauftragskomponente*) zeigt die Materialkomponenten der oben markierten FA-Zeile. Der Bereich ist nur zur Anzeige bestimmt und filtert automatisch auf **Status**, **FA-Nr.** und **Zeilennr.** der markierten Zeile.

| Feld | Erläuterung |
|------|-------------|
| **Artikelnr.** | Komponentenartikel, der für die Fertigung der Zeile benötigt wird. |
| **Beschreibung** / **Beschreibung 2** | Bezeichnung der Komponente. **Beschreibung 2** wird zur Anzeige aus dem Artikel bzw. – bei gesetzter Variante – aus der Artikelvariante nachgeladen. |
| **Variante** | Variantencode der Komponente. |
| **Position**, **Position 2**, **Position 3** | Positionsangaben der Komponente aus der Fertigungsstückliste. |
| **Einheitencode** | Maßeinheit der Komponente. |
| **Menge** / **Menge pro** | Benötigte Menge bzw. Menge je Einheit des Endartikels. |
| **Erwartete Menge** | Aus Sollmenge und Stücklistenmenge errechneter Materialbedarf. |
| **Restmenge** | Noch nicht verbrauchte Menge der Komponente. |
| **Ist-Verbrauch (Menge)** | Bereits als Verbrauch gebuchte Menge der Komponente. |
| **Buchungsmethode** | Steuert, wie der Verbrauch gebucht wird: manuelle Buchung, Buchung mit Vorwärtsverbuchung bei Fertigungsstart oder Rückwärtsverbuchung bei Fertigmeldung. |
| **Lagerortcode**, **Lagerplatzcode** | Lagerzuordnung der Komponente. |
| **Fälligkeitsdatum** / **Fälligkeitszeit** | Bereitstellungstermin der Komponente. |
| **Ausschussprozentsatz** | Ausschussaufschlag der Komponente. |
| **Kommissioniermenge**, **Kommissionierte Menge**, **Vollständig kommissioniert** | Kommissionierstatus der Komponente für die Materialbereitstellung. |
| **Einstandspreis**, **Kostenbetrag**, **Direkte Kosten (Betrag)**, **Gemeinkostensatz**, **Indirekte Kosten %** | Wert- und Kostenfelder der Komponente. |

### Unterer Bereich – Verkaufszeilen

Der untere Bereich **Verkaufszeilen** (Unterseite auf der Standardtabelle *Verkaufszeile*) zeigt die Verkaufszeilen, die mit der oben markierten FA-Zeile in Verbindung stehen. Der Bereich ist schreibgeschützt.

Die Verknüpfung wird nicht über einen einfachen Schlüssel hergestellt, sondern über die Reservierungslogik von Business Central: Die App ermittelt zunächst über die **Reservierungsposten** der FA-Zeile die reservierten Verkaufszeilen. Findet sie keine Reservierung, wertet sie ersatzweise die **Artikelposten** vom Typ Ausgabe der Fertigung aus und ermittelt darüber die zugehörige Verkaufszeile. So sieht der Anwender, welche Kundenaufträge an der gewählten Fertigung hängen.

| Feld | Erläuterung |
|------|-------------|
| **Belegart** | Art des Verkaufsbelegs (z. B. Auftrag) der Zeile. |
| **Belegnr.** | Nummer des Verkaufsbelegs. |
| **Verk. an Deb.-Nr.** | Nummer des Debitors, an den verkauft wird. |
| **Verk. an Deb.- Name** | Name des Debitors. Dieses Feld ergänzt die App als abgeleitetes Feld (siehe Abschnitt **Erweiterung der Verkaufszeile**) und blendet den Debitorennamen direkt neben der Debitorennummer ein, sodass der Anwender den Kunden erkennt, ohne den Beleg zu öffnen. |
| **Art** | Zeilenart der Verkaufszeile (z. B. Artikel). |
| **Nr.** | Artikel- bzw. Sachnummer der Verkaufszeile. |
| **Beschreibung** | Bezeichnung der Verkaufszeile. |
| **Lagerortcode** | Lagerort der Verkaufszeile. |
| **Reservieren** | Reservierungsmethode der Verkaufszeile. |
| **Menge** | Verkaufte Menge. |
| **Reservierte Menge (Basis)** | Bereits reservierte Menge in Basiseinheiten. |
| **Einheitencode** | Maßeinheit der Verkaufszeile. |
| **Zeilenbetrag** | Betrag der Verkaufszeile (Nullwerte werden ausgeblendet). |
| **Warenausg.-Datum** | Geplantes Warenausgangsdatum der Verkaufszeile. |
| **Restmenge** | Noch nicht ausgelieferte Menge der Verkaufszeile. |

Über die Zeilenaktionen des unteren Bereichs (Gruppe **Zeile**) stehen zur markierten Verkaufszeile bereit:

- **Beleg anzeigen** – öffnet den zugehörigen Verkaufsbeleg.
- **Reservierungsposten** – zeigt die Reservierungsposten der Zeile.
- **Artikelverfolgungszeilen** – öffnet die Artikelverfolgung (Chargen-/Seriennummern) der Zeile.

### Infobereich – Arbeitsgänge und Komponenten

Rechts blendet die Seite zwei Infoboxen ein:

- **Arbeitsgänge zur FA-Zeile** (Standardtabelle *Fertigungsauftrags-Arbeitsgang*): zeigt zur markierten FA-Zeile die Arbeitsgänge mit **Vorgangsnr.**, **Nr.** (Arbeitsplatz/Arbeitsplatzgruppe), **Beschreibung**, **Rüstzeit** und **Bearbeitungszeit**. Die Box ist schreibgeschützt und filtert auf **Arbeitsplannr.**, **Arbeitsplanreferenznr.**, **FA-Nr.** und **Status** der markierten Zeile.
- **Komponenten** (Standardtabelle *Fertigungsauftragskomponente*): kompakte Materialansicht mit **Artikelnr.** und **Variante**. Diese Box ist standardmäßig ausgeblendet und kann über die Personalisierung eingeblendet werden.

## Funktionen im Menüband

Aus der FA-Zeilenübersicht heraus ruft der Anwender Funktionen auf, die im Standard nur über den Fertigungsauftragskopf verfügbar wären. Alle Funktionen sind als geförderte Aktionen im Menüband erreichbar und beziehen sich auf die oben markierte FA-Zeile bzw. deren Fertigungsauftrag.

| Aktion | Erläuterung |
|--------|-------------|
| **Beleg anzeigen** | Öffnet den Fertigungsauftrag der markierten Zeile in der passenden Belegansicht. Die App wählt die Ansicht anhand des Status: **Simulierter FA**, **Geplanter FA**, **Fest geplanter FA**, **Freigegebener FA** oder **Beendeter FA**. Dort stehen dem Anwender – entsprechend seiner Berechtigungen – alle üblichen Funktionen des Belegs zur Verfügung. |
| **Status ändern** | Startet die Standardfunktion zur Statusänderung des Fertigungsauftrags. Der Anwender kann den Auftrag so beispielsweise von **Fest geplant** auf **Freigegeben** setzen; erst danach ist eine Rückmeldung über das **Prod. Buch. Blatt** möglich. |
| **Komponenten** | Öffnet die Standardansicht **FA-Komponenten** zur markierten Zeile. Verknüpfung: **Status**, **FA-Nr.** und **Zeilennr.** der Zeile. Tastenkürzel Alt+K. |
| **Prod. Buch. Blatt** | Erzeugt die Buchungsdaten und öffnet das Produktionsbuchungsblatt, in dem der Anwender – mit den entsprechenden Berechtigungen – Verbrauch und Ausbringung der Zeile bucht. Die Aktion ist nur im Status **Freigegeben** zulässig; in anderen Status weist die App die Ausführung ab. Tastenkürzel Alt+P. |
| **Arbeitsgänge** | Öffnet die Standardansicht der Arbeitsgänge des Fertigungsauftrags. Verknüpfung: **Status**, **FA-Nr.**, **Arbeitsplannr.** und **Arbeitsplanreferenznr.** der Zeile. |

## Filter und persönliche Ansichten

Die FA-Zeilenübersicht bietet dem Anwender die Möglichkeit, die Ansicht mit den Standard-Filterfunktionen von Business Central einzugrenzen und das Ergebnis als **persönliche Ansicht** zu speichern.

So gehen Sie vor:

1. Klicken Sie oben rechts auf das **Filtersymbol**. Am linken Rand der Seite öffnet sich der Filterbereich.
2. Setzen Sie einen Filter auf eine oder mehrere Spalten – beispielsweise **Status** = **Freigegeben**. Die Liste zeigt daraufhin nur noch die passenden FA-Zeilen.
3. Speichern Sie die gefilterte Ansicht über das Menü der drei Punkte mit **Speichern unter…** unter einem eigenen Namen.
4. Wiederholen Sie den Vorgang für weitere Kriterien, etwa für **Fest geplant**e Fertigungsaufträge.

Beim erneuten Aufruf der FA-Zeilenübersicht wählen Sie eine der gespeicherten Ansichten per Klick aus und arbeiten sofort mit der gewünschten Eingrenzung weiter. Die Filterung nutzt den Business-Central-Standardmechanismus für Ansichten; die App bringt keine eigenen Filterfelder mit.

## Erweiterung der Verkaufszeile

Die App ergänzt die Standardtabelle *Verkaufszeile* um ein einziges, abgeleitetes Feld, das ausschließlich der Anzeige im unteren Bereich der Übersicht dient:

| Feld | Erläuterung |
|------|-------------|
| **Verk. an Deb.- Name** | Abgeleitetes Feld (Flowfield), das den Namen des Debitors aus der Debitorentabelle anhand der **Verk. an Deb.-Nr.** nachschlägt. Wenn dieses Feld im Bereich **Verkaufszeilen** eingeblendet ist, erkennt der Anwender den Kunden direkt in der Zeile, ohne den Verkaufsbeleg oder den Debitorenstamm öffnen zu müssen. Das Feld ist schreibgeschützt und verändert keine Daten. |

Das Feld ist für Personalisierungen als Lese-/Schreibfeld freigegeben, wird von der App selbst jedoch nur lesend verwendet.

## Berechtigungen

Die App liefert den Berechtigungssatz **Alle Berechtigungen** (AL-Objekt `MuM PL Permission`) mit. Dieser Satz legt fest, welche Aktionen die Anwender innerhalb der App ausführen dürfen: Er umfasst die ausführbare Berechtigung auf die Seiten der FA-Zeilenübersicht (obere Liste, Unterseiten für Komponenten und Verkaufszeilen, beide Infoboxen) sowie auf die interne Lizenzprüfung.

Da die App auf Standardtabellen zugreift, bestimmen für die eigentliche Datenanzeige und -bearbeitung zusätzlich die **Standardberechtigungen** von Business Central auf Fertigung, Verkauf und Lager, welche Felder ein Anwender sehen und ändern kann. Das Bearbeiten in der Übersicht (etwa der **Arbeitsplannr.**) und das Buchen über das **Prod. Buch. Blatt** setzen die entsprechenden Standardberechtigungen voraus.

## Lizenzprüfung

Beim Anmelden prüft die App über das m+m-Basismodul, ob eine gültige Lizenz für die App vorliegt. Diese Prüfung läuft technisch im Hintergrund und erfordert keine Anwenderaktion. Ohne gültige Lizenz stehen die Funktionen der App nicht zur Verfügung; wenden Sie sich in diesem Fall an Ihren Systemverantwortlichen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Freigegebene Fertigung zurückmelden

**Auslöser:** Ein Werker meldet der Fertigungssteuerung, dass ein Fertigungsauftrag fertiggestellt ist und gebucht werden soll.

**Einstieg in BC:** Die Fertigungssteuerung öffnet über die **Suche** die **FA-Zeilenübersicht**.

**Kernablauf:**
1. In der oberen Liste die betreffende FA-Zeile auswählen; zur schnellen Eingrenzung zuvor die gespeicherte Ansicht **Status = Freigegeben** aktivieren oder das **Filtersymbol** nutzen.
2. Im mittleren Bereich die **FA-Komponenten** und deren **Restmenge** prüfen; im Infobereich **Arbeitsgänge zur FA-Zeile** die Arbeitsgänge kontrollieren.
3. Über die Aktion **Prod. Buch. Blatt** das Produktionsbuchungsblatt öffnen. Voraussetzung ist der Status **Freigegeben**; die App erzeugt die Buchungsdaten und öffnet das Blatt.
4. Im Standard-Buchungsblatt Verbrauch und Ausbringung buchen.

**Abschluss:** Nach der Buchung steigt die **Gebuchte Menge** der Zeile, die **Restmenge** sinkt. Ist die Fertigung vollständig, ändert die Fertigungssteuerung über **Status ändern** den Auftrag auf **Beendet**.

### Anwendungsfall 2: Kundenbezug einer Fertigung prüfen

**Auslöser:** Der Vertrieb fragt telefonisch nach, für welchen Kundenauftrag eine bestimmte Fertigung läuft und wann geliefert werden kann.

**Einstieg in BC:** Die Fertigungssteuerung öffnet die **FA-Zeilenübersicht** und sucht die FA-Zeile über einen Filter auf **FA-Nr.** oder **Artikelnr.**.

**Kernablauf:**
1. Die betreffende FA-Zeile in der oberen Liste markieren.
2. Im unteren Bereich **Verkaufszeilen** die zugeordneten Kundenaufträge ablesen: **Belegnr.**, **Verk. an Deb.- Name**, **Menge**, **Restmenge** und **Warenausg.-Datum**.
3. Bei Bedarf über die Zeilenaktion **Beleg anzeigen** den Verkaufsbeleg öffnen oder über **Artikelverfolgungszeilen** bzw. **Reservierungsposten** die Zuordnung im Detail nachvollziehen.

**Abschluss:** Der Anwender nennt dem Vertrieb Kunde, Menge und geplantes Warenausgangsdatum – ohne zwischen Fertigungsauftrag, Reservierung und Verkaufsauftrag wechseln zu müssen.

### Anwendungsfall 3: Arbeitsplan einer geplanten Zeile anpassen

**Auslöser:** In der Arbeitsvorbereitung stellt sich heraus, dass ein noch nicht freigegebener Fertigungsauftrag über einen anderen Arbeitsplan gefertigt werden soll.

**Einstieg in BC:** Die Arbeitsvorbereitung öffnet die **FA-Zeilenübersicht** und filtert auf **Status = Fest geplant** (oder **Geplant**).

**Kernablauf:**
1. Die zu ändernde FA-Zeile markieren.
2. In der Spalte **Arbeitsplannr.** den neuen Arbeitsplan eintragen. Da die Zeile planbar ist, ist das Feld editierbar.
3. Die Rückfrage **„Möchten Sie den FA neu berechnen?“** bestätigen. Die App übernimmt den neuen Arbeitsplan in den Fertigungsauftrag und berechnet ihn rückwärts neu.

**Abschluss:** Im Infobereich **Arbeitsgänge zur FA-Zeile** erscheinen die Arbeitsgänge des neuen Arbeitsplans. Bei Bedarf öffnet die Aktion **Arbeitsgänge** die vollständige Standardansicht zur Kontrolle.

## FAQ und Troubleshooting

### 1. Warum sehe ich in der FA-Zeilenübersicht keine simulierten Fertigungsaufträge?
Die obere Liste ist über die Quelltabellenansicht fest auf Zeilen ab Status **Geplant** eingegrenzt (`Status = filter(Planned ..)`). Zeilen mit rein simuliertem Charakter erscheinen nur, wenn ihr Status innerhalb dieses Bereichs liegt. Prüfen Sie den **Status** der Zeile.

### 2. Warum kann ich die meisten Felder in der oberen Liste nicht bearbeiten?
Die Übersicht ist bewusst überwiegend schreibgeschützt und dient der Auswertung und Steuerung. Editierbar ist ausschließlich die **Arbeitsplannr.**, und auch diese nur in den Status **Simuliert**, **Geplant** und **Fest geplant**. Feldänderungen an Mengen, Terminen und Kosten nehmen Sie im jeweiligen Standardbeleg vor, den Sie über **Beleg anzeigen** öffnen.

### 3. Warum erscheint beim Ändern der Arbeitsplannr. die Rückfrage „Möchten Sie den FA neu berechnen?“
Eine geänderte **Arbeitsplannr.** wirkt sich auf die Arbeitsgänge und Termine des Fertigungsauftrags aus. Nur wenn Sie die Rückfrage bestätigen, übernimmt die App den neuen Arbeitsplan in den Auftrag und rechnet ihn rückwärts neu. Lehnen Sie ab, bleibt der bisherige Arbeitsplan bestehen.

### 4. Warum ist das Feld Arbeitsplannr. bei freigegebenen und beendeten Zeilen gesperrt?
Ab dem Status **Freigegeben** ist der Auftrag in Fertigung; eine nachträgliche Arbeitsplanänderung über die Übersicht ist deshalb unterbunden. In den planbaren Status **Simuliert**, **Geplant** und **Fest geplant** ist das Feld dagegen editierbar.

### 5. Warum lässt sich das Prod. Buch. Blatt nicht starten?
Die Aktion **Prod. Buch. Blatt** ist nur im Status **Freigegeben** zulässig. Bei einem Auftrag in einem anderen Status weist die App die Ausführung ab. Setzen Sie den Auftrag zunächst über **Status ändern** auf **Freigegeben**.

### 6. Warum werden im mittleren und unteren Bereich keine Daten angezeigt?
Beide Bereiche filtern auf die oben markierte FA-Zeile. Markieren Sie eine Zeile in der oberen Liste; erst dann füllen sich **FA-Komponenten** und **Verkaufszeilen**. Zeigt eine Zeile keine Komponenten, besitzt der Auftrag für diese Zeile keine; zeigt sie keine Verkaufszeilen, besteht keine Reservierung oder Ausgabezuordnung zu einem Verkaufsbeleg.

### 7. Warum sehe ich Verkaufszeilen zu einer FA-Zeile, obwohl ich keine direkte Verknüpfung erwartet hätte?
Der untere Bereich ermittelt die Verkaufszeilen über die **Reservierungsposten** der FA-Zeile. Fehlt eine Reservierung, wertet die App ersatzweise die **Artikelposten** vom Typ Ausgabe der Fertigung aus. So werden auch Verkaufszeilen angezeigt, die nur über die tatsächliche Ausbringung mit der Fertigung verbunden sind.

### 8. Warum steht neben der Debitorennummer der Kundenname?
Die App ergänzt die Verkaufszeile um das abgeleitete Feld **Verk. an Deb.- Name**, das den Namen anhand der **Verk. an Deb.-Nr.** nachschlägt. So erkennen Sie den Kunden direkt in der Zeile, ohne den Beleg zu öffnen.

### 9. Wie rufe ich schnell wiederkehrende Auswertungen auf?
Setzen Sie über das **Filtersymbol** die gewünschten Kriterien und speichern Sie das Ergebnis über **Speichern unter…** als persönliche Ansicht. Beim nächsten Aufruf der FA-Zeilenübersicht aktivieren Sie diese Ansicht per Klick. Die Ansichten sind persönlich und stehen Ihnen dauerhaft zur Verfügung.

### 10. Muss ich die App einrichten, bevor ich sie nutzen kann?
Nein. Die App bringt keine eigenen Einrichtungsseiten und keine eigenen Stammdaten mit. Voraussetzung sind lediglich vorhandene Fertigungsaufträge aus dem Standardprozess sowie die passenden Standardberechtigungen für Fertigung, Verkauf und Lager. Für den vollen Funktionsumfang muss zudem eine gültige Lizenz vorliegen.
