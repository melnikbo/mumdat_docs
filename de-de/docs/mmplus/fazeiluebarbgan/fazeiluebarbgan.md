---
title: Anwenderhandbuch m+m Production Order Overview with Routing Status Overview
---

# Anwenderhandbuch m+m Production Order Overview with Routing Status Overview

## Einleitung

Die App m+m „Production Order Overview with Routing Status Overview" verbindet zwei bestehende m+m-Module miteinander: die **FA-Zeilenübersicht** (Übersicht der Fertigungsauftragszeilen) und die **Arbeitsgangstatusanzeige**. Die App fügt der **FA-Zeilenübersicht** einen zusätzlichen Bereich hinzu, in dem für die aktuell markierte Fertigungsauftragszeile der Status aller Arbeitsgänge sowohl grafisch als auch als Liste dargestellt wird.

Der Anwender arbeitet dadurch auf **einer** Seite: Er wählt links in der Zeilenübersicht einen Fertigungsauftrag aus und sieht darunter sofort, in welchem Bearbeitungsstand sich die einzelnen Arbeitsgänge dieses Fertigungsauftrags befinden — ohne dass er den Fertigungsauftrag oder den zugehörigen Arbeitsplan separat öffnen muss.

**Zielgruppe:** Primäre Zielgruppe sind **operative Anwender in der Fertigungssteuerung** — Fertigungssteuerer, Arbeitsvorbereiter und Mitarbeiter, die den Fortschritt laufender Fertigungsaufträge überwachen und Folgeaktionen (Status ändern, Buchen im Buch.-Blatt, Arbeitsplan öffnen) auslösen. Planer und Auftragskoordinatoren nutzen die Übersicht sekundär zur Grob- und Terminkontrolle.

**Kurzer Prozessüberblick:** Fertigungsaufträge werden im BC-Standard bzw. in den vorgelagerten m+m-Modulen angelegt und terminiert. In der **FA-Zeilenübersicht** überwacht der Anwender die daraus entstandenen Fertigungsauftragszeilen. Die App ergänzt diese Zeilenübersicht um die **Arbeitsgangstatusanzeige**, die den Rückmeldestand jedes Arbeitsgangs in Echtzeit sichtbar macht. Von dort verzweigt der Anwender bei Bedarf in den **Arbeitsplan**, in den Fertigungsauftrag oder in die weiteren Aktionen der Zeilenübersicht.

**Einrichtung:** Für die Nutzung dieser App ist **keine gesonderte Einrichtung** erforderlich. Es gibt keine eigenen Einrichtungsseiten, Nummernserien oder Stammdaten. Nach der Installation steht die **Arbeitsgangstatusanzeige** in der **FA-Zeilenübersicht** automatisch zur Verfügung. Voraussetzung ist lediglich, dass die abhängigen Module (m+m Cloud Base, m+m Production Order Overview, m+m Routing Status Overview) installiert sind.

## Schnellstart für Anwender

Der schnellste Weg vom Öffnen der Übersicht bis zur Statuskontrolle eines Arbeitsgangs:

1. Öffnen Sie über **Suchen** die Seite **FA-Zeilenübersicht**. Die Seite ist als Listenseite discoverable und ohne übergeordnete Einstiegsseite erreichbar.
2. Markieren Sie in der Zeilenliste die gewünschte **Fertigungsauftragszeile** (Spalten **Status**, **Fertigungsauftragsnr.**, **Artikelnr.** helfen bei der Auswahl).
3. Lesen Sie im unteren Bereich **Arbeitsgangstatusanzeige** den Fortschritt ab: Jede Kachel steht für einen Arbeitsgang; die Farbe zeigt den Bearbeitungsstand (siehe Abschnitt *Farblogik*).
4. Klicken Sie auf eine **Kachel**, um den **Arbeitsplan** (Aktion **Arbeitsgänge**) des Fertigungsauftrags einzusehen.
5. Wechseln Sie bei Bedarf über die Listenform der Anzeige per Klick auf die **Fertigungsauftragsnr.** direkt in den passenden **Fertigungsauftrag**.
6. Lösen Sie Folgeaktionen aus der **FA-Zeilenübersicht** aus: **Status ändern**, **Prod. Buch. Blatt**, **Komponenten** oder **Arbeitsgänge** (siehe Abschnitt *Aktionen*).

Es sind keine vorbereitenden Einrichtungsschritte notwendig; der Schnellstart beginnt direkt mit dem Öffnen der Liste.

## Die FA-Zeilenübersicht

Die **FA-Zeilenübersicht** ist die zentrale Listenseite dieses Zusammenspiels. Sie zeigt die Zeilen aller Fertigungsaufträge ab dem Status **Geplant** aufwärts und ist nach **Status**, **Fertigungsauftragsnr.** und **Zeilennr.** sortiert. Die Seite selbst ist nicht editierbar (mit Ausnahme der **Arbeitsplannr.**, siehe unten); Anlegen und Löschen von Zeilen sind auf dieser Seite gesperrt. Über **Suchen** ist sie unmittelbar aufrufbar.

Die App erweitert diese Seite: Direkt oberhalb des Bereichs **Zugeordnete FA-Komponente** wird die **Arbeitsgangstatusanzeige** eingeblendet, die sich bei jedem Zeilenwechsel automatisch auf die markierte Fertigungsauftragszeile aktualisiert.

### Spalten der Zeilenliste

Die folgende Tabelle beschreibt die Spalten der **FA-Zeilenübersicht**. Alle Spalten sind schreibgeschützt und dienen der Information; einzige Ausnahme ist die **Arbeitsplannr.**

| Feld | Erläuterung |
|------|-------------|
| **Status** | Zeigt den Belegstatus des Fertigungsauftrags der Zeile (z. B. Geplant, Fest geplant, Freigegeben, Beendet). Wenn Sie eine Zeile auswählen, richtet sich hieran, welcher Fertigungsauftrag beim Öffnen bzw. beim Statuswechsel angesprochen wird. |
| **Fertigungsauftragsnr.** | Nummer des Fertigungsauftrags. Wenn Sie diese Nummer als Orientierung nutzen, erkennen Sie, zu welchem Auftrag die Zeile und die darunter angezeigten Arbeitsgänge gehören. |
| **Zeilennr.** | Laufende Nummer der Fertigungsauftragszeile. Wenn ein Auftrag mehrere Zeilen hat, unterscheidet die Zeilennr. die einzelnen zu fertigenden Positionen. |
| **Artikelnr.** | Zu fertigender Artikel der Zeile. Wenn Sie die Zeile wählen, bezieht sich die Arbeitsgangstatusanzeige auf die Fertigung genau dieses Artikels. |
| **Variantencode** | Variante des Artikels. Wenn eine Variante gesetzt ist, betrifft der Fertigungsfortschritt diese Ausprägung des Artikels. |
| **Beschreibung** | Bezeichnung des Artikels bzw. der Zeile zur schnellen Identifikation. |
| **Beschreibung 2** | Ergänzende zweite Bezeichnungszeile, sofern gepflegt. |
| **Lagerortcode** | Lagerort, für den die Zeile gefertigt wird. Wenn gesetzt, ordnet er den Fertigungsauftrag einem Lagerort zu. |
| **Shortcutdimensionscode 1** | Wert der ersten globalen Dimension der Zeile; dient der buchhalterischen Zuordnung. |
| **Shortcutdimensionscode 2** | Wert der zweiten globalen Dimension der Zeile; dient der buchhalterischen Zuordnung. |
| **Lagerplatzcode** | Lagerplatz innerhalb des Lagerorts, sofern der Lagerort platzgeführt ist. |
| **Menge** | Geplante Fertigungsmenge der Zeile. Sie bildet die Bezugsgröße für Fertiggestellte Menge und Restmenge. |
| **Fertiggestellte Menge** | Bereits gemeldete/gebuchte Gutmenge der Zeile. Wenn dieser Wert steigt, verringert sich entsprechend die Restmenge; er zeigt den erreichten Fertigungsfortschritt. |
| **Restmenge** | Noch offene Menge (Menge abzüglich Fertiggestellte Menge). Wenn die Restmenge 0 erreicht, ist die geplante Menge der Zeile vollständig gefertigt. |
| **Ausschuss %** | Geplanter Ausschussanteil der Zeile in Prozent. Wenn gesetzt, kalkuliert der Fertigungsauftrag einen Mengenaufschlag für erwarteten Ausschuss ein. |
| **Fälligkeitsdatum** | Termin, zu dem die Zeile fertiggestellt sein soll. Er dient der Termin- und Rückstandskontrolle. |
| **Startdatum** | Geplanter Beginn der Fertigung der Zeile. |
| **Startzeit** | Geplante Startuhrzeit der Fertigung der Zeile. |
| **Enddatum** | Geplantes Ende der Fertigung der Zeile. |
| **Endzeit** | Geplante Enduhrzeit der Fertigung der Zeile. |
| **Planungsebenencode** | Kennzeichnet die Planungsebene der Zeile in mehrstufigen Fertigungen. |
| **Priorität** | Priorität der Zeile; unterstützt die Reihenfolgebildung bei konkurrierenden Aufträgen. |
| **Fert.-Stücklistennr.** | Verwendete Fertigungsstückliste der Zeile; bestimmt, welche Komponenten benötigt werden. |
| **Arbeitsplannr.** | Verwendeter Arbeitsplan der Zeile. Dieses Feld ist editierbar: Wenn Sie es ändern und die Rückfrage bestätigen, übernimmt das System die neue Arbeitsplannr. in den Fertigungsauftrag und rechnet den Arbeitsplan rückwärts neu durch — die darunter angezeigten Arbeitsgänge ändern sich dadurch entsprechend. |
| **Lagerbuchungsgruppe** | Steuert die Sachkontenfindung bei lagerbezogenen Buchungen der Zeile. |
| **Arbeitsplanref.-Nr.** | Referenznummer, über die die Zeile mit den zugehörigen Arbeitsgängen des Arbeitsplans verknüpft ist. |
| **Einstandspreis** | Einstandspreis je Einheit der Zeile; Basis für die Wertermittlung. |
| **Kostenbetrag** | Kalkulierter Kostenbetrag der Zeile. |
| **Reservierte Menge** | Für die Zeile reservierte Menge; zeigt, wie viel Bedarf bereits durch Reservierungen gedeckt ist. |
| **Einheitencode** | Mengeneinheit der Zeile, in der Menge und Fertiggestellte Menge geführt werden. |
| **Menge (Basis)** | Menge in der Basiseinheit des Artikels. |
| **Fertiggestellte Menge (Basis)** | Fertiggestellte Menge in der Basiseinheit. |
| **Restmenge (Basis)** | Restmenge in der Basiseinheit. |
| **Reservierte Menge (Basis)** | Reservierte Menge in der Basiseinheit. |
| **Erwarteter Arbeitsgangkostenbetrag** | Erwarteter Kostenbetrag aus den Arbeitsgängen der Zeile. |
| **Erw. Arbeitsgangausgabe gesamt (Menge)** | Erwartete Gesamtmenge, die aus den Arbeitsgängen der Zeile hervorgeht. |
| **Erwarteter Komponentenkostenbetrag** | Erwarteter Kostenbetrag aus den Komponenten der Zeile. |
| **Startdatum/-zeit** | Zusammengesetzter Startzeitpunkt (Datum und Uhrzeit) der Zeile. |
| **Enddatum/-zeit** | Zusammengesetzter Endzeitpunkt (Datum und Uhrzeit) der Zeile. |
| **Kostenbetrag (BW)** | Kostenbetrag in der zusätzlichen Berichtswährung. |
| **Einstandspreis (BW)** | Einstandspreis in der zusätzlichen Berichtswährung. |
| **Fert.-Stücklistenversionscode** | Verwendete Version der Fertigungsstückliste. |
| **Arbeitsplanversionscode** | Verwendete Version des Arbeitsplans. |
| **Arbeitsplanart** | Art des Arbeitsplans (z. B. seriell oder parallel); beeinflusst die Terminierung der Arbeitsgänge. |
| **Menge pro Einheit** | Umrechnungsfaktor zwischen Einheiten- und Basiseinheit. |
| **MPS-Auftrag** | Kennzeichnet, ob die Zeile aus der Hauptproduktionsplanung stammt. |
| **Planungsflexibilität** | Steuert, ob die Zeile von der Planung verschoben werden darf; bei „Keine" bleibt der Termin fixiert. |
| **Indirekte Kosten %** | Aufschlag für indirekte Kosten je Einheit der Zeile. |
| **Gemeinkostensatz** | Fester Gemeinkostenzuschlag je Einheit der Zeile. |

> Hinweis zur **Arbeitsplannr.**: Diese Änderung wirkt direkt auf den Fertigungsauftrag. Bestätigen Sie die Sicherheitsabfrage nur, wenn der Arbeitsplan tatsächlich getauscht werden soll — das System terminiert die Arbeitsgänge anschließend neu.

### Weitere Bereiche der Seite

Neben der Zeilenliste und der **Arbeitsgangstatusanzeige** blendet die Seite mitlaufende Zusatzbereiche ein, die sich auf die markierte Zeile beziehen:

- **Zugeordnete FA-Komponente** — Unterseite mit den Komponenten der markierten Fertigungsauftragszeile (schreibgeschützt); zeigt, welches Material die Zeile verbraucht.
- **Verkaufszeilen** — Unterseite mit den Verkaufszeilen, die den Bedarf für den Fertigungsauftrag ausgelöst haben; stellt den Bezug zwischen Fertigung und Kundenauftrag her.
- Zusätzlich werden Infoboxen zu den **Arbeitsgängen** und zu den **Materialkomponenten** der markierten Zeile eingeblendet.

## Arbeitsgangstatusanzeige

Die **Arbeitsgangstatusanzeige** ist der Bereich, den diese App der **FA-Zeilenübersicht** hinzufügt. Sie besteht aus zwei aufeinander bezogenen Teilen: einer **grafischen Ansicht** (Kacheln) und einer **Listenansicht** (Tabelle). Beide beziehen sich immer auf die aktuell in der Zeilenliste markierte Fertigungsauftragszeile und aktualisieren sich bei jedem Zeilenwechsel automatisch.

### Grafische Ansicht

Die grafische Ansicht stellt die Arbeitsgänge des Fertigungsauftrags als Kacheln nebeneinander dar:

- Am linken Rand steht das **Startdatum/-zeit**, am rechten Rand das **Enddatum/-zeit** des Fertigungsauftrags — so ist die zeitliche Spanne der Fertigung ablesbar.
- Jede **Kachel** steht für einen Arbeitsgang. Auf der Kachel stehen die **Beschreibung** des Arbeitsgangs und in Klammern die **Arbeitsgangnummer**.
- Eine kleinere Kachel darunter zeigt die **Fertiggestellte Menge** des jeweiligen Arbeitsgangs an, sodass der erreichte Fortschritt je Arbeitsgang sichtbar ist.
- Der aktuell in Bearbeitung befindliche Arbeitsgang wird gesondert hervorgehoben. Grundlage ist die letzte Kapazitätsbuchung des Fertigungsauftrags: Der Arbeitsgang, auf den die jüngste Rückmeldung gebucht wurde, gilt als der aktive Arbeitsgang.
- Ein **Klick auf eine Kachel** öffnet den **Arbeitsplan** (Seite **Arbeitsgänge**) des Fertigungsauftrags in einer schreibgeschützten Ansicht. So gelangt der Anwender vom Statusüberblick mit einem Klick in die Detailsicht des Arbeitsplans.

#### Farblogik der Kacheln

Die Farbe einer Kachel bündelt den Belegstatus des Fertigungsauftrags und den Rückmeldestand des Arbeitsgangs. Die Anzeige leitet die Farbe aus dem Status des Fertigungsauftrags sowie aus dem Arbeitsgangstatus (Feld **Arbeitsgangstatus** der Arbeitsplanzeile) ab:

- **Grau — Fest geplant:** Der Fertigungsauftrag steht im Status **Fest geplant**. Wenn eine Kachel grau ist, ist der Arbeitsgang eingeplant, aber es kann noch nicht gefertigt werden.
- **Grün — Freigegeben:** Der Fertigungsauftrag wurde auf **Freigegeben** gesetzt. Wenn die Kachel grün ist, ist der Arbeitsgang zur Fertigung freigegeben und kann bearbeitet werden.
- **Rot — Gestartet/in Bearbeitung:** Der Arbeitsgang wurde gestartet bzw. befindet sich in Bearbeitung. Wenn die Kachel rot ist, laufen Rückmeldungen auf diesen Arbeitsgang; der Belegstatus des Fertigungsauftrags ändert sich dadurch nicht.
- **Blau — Beendet:** Der Arbeitsgang wurde durch eine entsprechende Meldung/Buchung auf **Beendet** gesetzt. Wenn der Fertigungsauftrag insgesamt auf **Beendet** gesetzt wird, erscheinen auch alle zugehörigen Arbeitsgänge blau.

> In der Praxis werden die Arbeitsgänge nacheinander gebucht bzw. gemeldet, sodass die Kacheln eines Fertigungsauftrags zeitgleich unterschiedliche Farben aufweisen — der Anwender erkennt daran auf einen Blick, welcher Arbeitsgang schon abgeschlossen ist, welcher gerade läuft und welcher noch aussteht.

### Listenansicht

Unterhalb der grafischen Kacheln zeigt die Listenansicht dieselben Fertigungsauftragszeilen als Tabelle. Sie ist schreibgeschützt und als Baumstruktur eingerückt (Feld **Ebene**), sodass mehrstufige Fertigungen (Fertigungsauftrag mit Unteraufträgen) hierarchisch erkennbar sind.

| Feld | Erläuterung |
|------|-------------|
| **Ebene** | Einrückungsebene der Zeile in mehrstufigen Fertigungen. Wenn die Ebene größer 0 ist, gehört die Zeile zu einem untergeordneten Fertigungsauftrag; die Baumstruktur macht die Fertigungshierarchie sichtbar. |
| **Status** | Belegstatus des Fertigungsauftrags der Zeile; ordnet die Zeile demselben Statusbereich zu wie in der oberen Zeilenliste. |
| **Fertigungsauftragsnr.** | Nummer des Fertigungsauftrags. Ein Klick auf die Nummer öffnet den zum Status passenden Fertigungsauftrag (Simuliert, Geplant, Fest geplant, Freigegeben oder Beendet), in dem der Anwender den Auftrag mit allen Funktionen bearbeiten kann. |
| **Beschreibung** | Bezeichnung der Fertigungsauftragszeile zur schnellen Identifikation. |
| **Menge** | Geplante Fertigungsmenge der Zeile; Bezugsgröße für die Fertiggestellte Menge. |
| **Startdatum** | Geplanter Beginn der Fertigung der Zeile. |
| **Startzeit** | Geplante Startuhrzeit der Fertigung der Zeile. |
| **Enddatum** | Geplantes Ende der Fertigung der Zeile. |
| **Endzeit** | Geplante Enduhrzeit der Fertigung der Zeile. |
| **Fertiggestellte Menge** | Bereits gefertigte Gutmenge der Zeile. Wenn dieser Wert die Menge erreicht, ist die Zeile mengenmäßig vollständig gefertigt. |

Über den Klick auf die **Fertigungsauftragsnr.** in dieser Liste gelangt der Anwender direkt in den Fertigungsauftrag; von dort kann er den Auftrag mit den Standardfunktionen (u. a. Statuswechsel, Zeilenpflege) weiterbearbeiten.

## Aktionen

Die Aktionen stehen im Menüband der **FA-Zeilenübersicht** bereit und beziehen sich auf die aktuell markierte Fertigungsauftragszeile. Sie sind zusätzlich als hervorgehobene Aktionen im Prozessbereich verfügbar.

| Aktion | Erläuterung |
|--------|-------------|
| **Beleg anzeigen** | Öffnet den Fertigungsauftrag der markierten Zeile im zum Status passenden Beleg (Simuliert, Geplant, Fest geplant, Freigegeben oder Beendet). Wenn Sie diese Aktion wählen, bearbeiten Sie den vollständigen Fertigungsauftrag statt nur die Zeile. |
| **Status ändern** | Startet den Statuswechsel des Fertigungsauftrags über die BC-Standardfunktion. Wenn Sie den Status ändern (z. B. von Fest geplant auf Freigegeben oder von Freigegeben auf Beendet), ändert sich anschließend auch die Farbe der Kacheln in der Arbeitsgangstatusanzeige. |
| **Komponenten** | Öffnet die Fertigungsauftragskomponenten der markierten Zeile. Wenn Sie diese Aktion wählen, prüfen und pflegen Sie den Materialbedarf der Zeile. (Tastenkürzel Alt+K.) |
| **Prod. Buch. Blatt** | Öffnet das Produktions-Buch.-Blatt für die markierte Zeile. Voraussetzung: Der Fertigungsauftrag hat den Status **Freigegeben** — andernfalls weist das System die Aktion ab. Wenn Sie hier Verbrauch und fertiggestellte Menge zurückmelden, steigt die Fertiggestellte Menge und die Farben/Mengen in der Arbeitsgangstatusanzeige aktualisieren sich. (Tastenkürzel Alt+P.) |
| **Arbeitsgänge** | Öffnet den Arbeitsplan (die Arbeitsgänge) des Fertigungsauftrags der markierten Zeile. Wenn Sie diese Aktion wählen, sehen und bearbeiten Sie die Arbeitsgänge im Detail — dieselbe Detailsicht, die auch der Klick auf eine Kachel öffnet. |

> Zum Anlegen und Löschen von Fertigungsauftragszeilen nutzt der Anwender die Standardfunktionen des jeweiligen Fertigungsauftrags (erreichbar über **Beleg anzeigen** bzw. den Klick auf die Fertigungsauftragsnr.). Dabei müssen die fachlichen Voraussetzungen erfüllt sein (z. B. keine bereits gebuchten Posten auf der Zeile).

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die App im Tagesablauf genutzt wird. Alle beschriebenen Seiten, Spalten und Aktionen entsprechen dem tatsächlichen Verhalten der **FA-Zeilenübersicht** mit **Arbeitsgangstatusanzeige**.

### Fortschrittskontrolle nach Nachfrage aus dem Vertrieb

**Auslöser:** Der Vertrieb ruft an und fragt, wie weit die Fertigung eines Kundenauftrags ist.

**Einstieg in BC:** Der Fertigungssteuerer öffnet über **Suchen** die **FA-Zeilenübersicht** und markiert die Zeile mit der passenden **Fertigungsauftragsnr.** bzw. **Artikelnr.**

**Kernablauf:** In der **Arbeitsgangstatusanzeige** liest er an den Kachelfarben ab, welche Arbeitsgänge bereits **blau** (beendet), welcher gerade **rot** (in Bearbeitung) und welche noch **grün** (freigegeben, aber nicht begonnen) sind. Die kleinen Kacheln zeigen ihm die **Fertiggestellte Menge** je Arbeitsgang. Über die Unterseite **Verkaufszeilen** verknüpft er die Fertigung mit der auslösenden Verkaufszeile.

**Abschluss:** Er gibt dem Vertrieb den aktuellen Stand durch. Bei Detailfragen klickt er auf eine Kachel und öffnet die **Arbeitsgänge**, um die Termine einzelner Arbeitsgänge zu nennen.

### Freigabe eines fest geplanten Fertigungsauftrags

**Auslöser:** Ein fest geplanter Auftrag soll in die Fertigung gehen.

**Einstieg in BC:** Der Anwender öffnet die **FA-Zeilenübersicht** und markiert die betreffende Zeile — die Kacheln der Arbeitsgänge sind zunächst **grau** (Status **Fest geplant**).

**Kernablauf:** Er wählt die Aktion **Status ändern** und setzt den Fertigungsauftrag über die BC-Standardfunktion auf **Freigegeben**. Nach der Aktualisierung erscheinen die Kacheln in der **Arbeitsgangstatusanzeige** **grün** — die Arbeitsgänge sind nun zur Fertigung bereit.

**Abschluss:** Anschließend kann der Anwender bei Fertigungsbeginn über **Prod. Buch. Blatt** die ersten Rückmeldungen buchen; die betroffenen Kacheln wechseln daraufhin auf **rot**.

### Rückmeldung eines Arbeitsgangs buchen

**Auslöser:** Aus der Fertigung kommt die Meldung, dass ein Arbeitsgang bearbeitet bzw. fertig ist.

**Einstieg in BC:** Der Anwender markiert in der **FA-Zeilenübersicht** die zugehörige Zeile (Status muss **Freigegeben** sein).

**Kernablauf:** Er öffnet über **Prod. Buch. Blatt** (Alt+P) das Produktions-Buch.-Blatt und meldet Verbrauch und fertiggestellte Menge des Arbeitsgangs zurück. Nach der Buchung aktualisiert sich die **Arbeitsgangstatusanzeige**: Die **Fertiggestellte Menge** der betroffenen Kachel steigt, und die Kachelfarbe zeigt den neuen Rückmeldestand (rot bei laufender, blau bei beendeter Bearbeitung).

**Abschluss:** Sind alle Arbeitsgänge blau, ist die Fertigung der Zeile abgeschlossen; der Anwender kann den Auftrag über **Status ändern** auf **Beendet** setzen.

## FAQ und Troubleshooting

### 1. Muss ich die App vor der Nutzung einrichten?
Nein. Die App benötigt keine gesonderte Einrichtung, keine Nummernserien und keine Stammdaten. Nach der Installation der App und ihrer abhängigen Module erscheint die **Arbeitsgangstatusanzeige** automatisch in der **FA-Zeilenübersicht**.

### 2. Wo finde ich die FA-Zeilenübersicht?
Sie öffnen die Seite über **Suchen**. Die **FA-Zeilenübersicht** ist als Listenseite direkt auffindbar und benötigt keinen Einstieg über eine übergeordnete Seite.

### 3. Warum sehe ich in der Übersicht keine simulierten Fertigungsaufträge?
Die **FA-Zeilenübersicht** zeigt Fertigungsauftragszeilen erst ab dem Status **Geplant** aufwärts. Zeilen im Status **Simuliert** werden bewusst nicht gelistet.

### 4. Was bedeuten die Farben der Kacheln?
**Grau** = Fertigungsauftrag **Fest geplant** (noch nicht fertigbar), **Grün** = **Freigegeben** (fertigungsbereit), **Rot** = Arbeitsgang **gestartet/in Bearbeitung**, **Blau** = Arbeitsgang **Beendet**. Ein rot markierter Arbeitsgang ändert den Belegstatus des Fertigungsauftrags nicht.

### 5. Warum sind alle Kacheln gleich gefärbt?
Das tritt auf, wenn alle Arbeitsgänge im selben Zustand sind. Im normalen Betrieb wird Arbeitsgang für Arbeitsgang gebucht/gemeldet, sodass die Kacheln je nach Fortschritt unterschiedliche Farben zeigen.

### 6. Wie öffne ich den Arbeitsplan eines Fertigungsauftrags?
Klicken Sie in der grafischen Ansicht auf eine **Kachel** oder wählen Sie in der **FA-Zeilenübersicht** die Aktion **Arbeitsgänge**. Beide öffnen den Arbeitsplan des Fertigungsauftrags in einer schreibgeschützten Ansicht.

### 7. Woran erkenne ich den aktuell laufenden Arbeitsgang?
Die Anzeige wertet die letzte Kapazitätsbuchung des Fertigungsauftrags aus und hebt den Arbeitsgang hervor, auf den zuletzt zurückgemeldet wurde. Dieser gilt als der aktive Arbeitsgang.

### 8. Warum lässt sich das Produktions-Buch.-Blatt nicht öffnen?
Die Aktion **Prod. Buch. Blatt** setzt den Status **Freigegeben** voraus. Ist der Fertigungsauftrag noch **Fest geplant** oder bereits **Beendet**, weist das System die Aktion ab. Setzen Sie den Auftrag zunächst über **Status ändern** auf **Freigegeben**.

### 9. Was passiert, wenn ich die Arbeitsplannr. in der Zeile ändere?
Nach einer Sicherheitsabfrage übernimmt das System die neue **Arbeitsplannr.** in den Fertigungsauftrag und terminiert den Arbeitsplan rückwärts neu. Danach zeigt die **Arbeitsgangstatusanzeige** die Arbeitsgänge des neuen Arbeitsplans. Bestätigen Sie die Abfrage nur bei einem gewollten Arbeitsplantausch.

### 10. Warum aktualisiert sich die Anzeige nach einer Buchung?
Die **Arbeitsgangstatusanzeige** ist an die markierte Zeile gebunden und wird bei jedem Zeilenwechsel sowie beim Aufruf der Seite neu aufgebaut. Nach einer Rückmeldung im Produktions-Buch.-Blatt spiegeln Kachelfarben und **Fertiggestellte Menge** unmittelbar den neuen Fertigungsfortschritt wider.
