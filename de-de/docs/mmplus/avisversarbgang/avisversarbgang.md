---
title: Anwenderhandbuch m+m Logistic Management with Routing Status Overview
---

# Anwenderhandbuch m+m Logistic Management with Routing Status Overview

## Einleitung

Die App **m+m Logistic Management with Routing Status Overview** verbindet zwei bestehende m+m Erweiterungen miteinander: die **Versandplanung** (aus *m+m Logistic Management*) und die **Arbeitsgangstatusanzeige** (aus *m+m Routing Status Overview*). Sie ergänzt die Seite **Versandplanungszuordnung und Lagersteuerung** um einen zusätzlichen Bereich **Arbeitsgangstatusanzeige**. Damit sehen Anwenderinnen und Anwender direkt in der Versandplanung, in welchem Fertigungszustand sich die Ware einer ausgewählten Versandzeile befindet, ohne die Seite verlassen zu müssen.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender im Versand und in der Lagersteuerung**, die täglich mit der Seite **Versandplanungszuordnung und Lagersteuerung** arbeiten: Sie ordnen Verkaufszeilen der Versandplanung zu, erstellen Lagerbelege und müssen dabei erkennen, ob die zugehörigen **Fertigungsaufträge** bereits fertiggestellt sind. Sekundär profitieren **Fertigungssteuerung und Disposition**, die Rückfragen zum Fertigungsfortschritt einer Versandzeile schnell beantworten möchten.

**Kurzer Prozessüberblick.** Die App bringt selbst **keine** eigenen Einrichtungs-, Stammdaten- oder Belegseiten mit. Ihr gesamter Funktionsbeitrag besteht darin, im unteren Bereich der Seite **Versandplanungszuordnung und Lagersteuerung** die **Arbeitsgangstatusanzeige** einzublenden. Wählt der Anwender in der Liste **Zeilen** eine Zeile aus, aktualisiert sich die **Arbeitsgangstatusanzeige** und zeigt den Arbeitsgang- und Fertigungsstatus des Fertigungsauftrags, der hinter der Verkaufszeile dieser Versandzeile liegt. Eine gesonderte Dokumentation der App m+m **Arbeitsgangstatus** beschreibt die Anzeige selbst im Detail; dieses Handbuch beschreibt die **Zusammenführung** beider Funktionen in der Versandplanung.

## Schnellstart für Anwender

Die App benötigt **keine** Einrichtung. Nach der Installation steht die **Arbeitsgangstatusanzeige** auf der Seite **Versandplanungszuordnung und Lagersteuerung** unmittelbar zur Verfügung. Der schnellste Weg zum Ergebnis:

1. Öffnen Sie über die Suche in Business Central die Seite **Versandplanungszuordnung und Lagersteuerung**. (Die Seite ist eine unternehmensweite Arbeitsseite und wird über **Suchen** aufgerufen.)
2. Grenzen Sie die anzuzeigenden Positionen bei Bedarf über die Filter im Bereich **Allgemein** ein — mindestens sinnvoll sind **Lagerortfilter** und **Datumsfilter** — und wählen Sie **Daten aktualisieren**.
3. Wählen Sie in der Liste **Zeilen** die gewünschte **Zeile** (eine Positionszeile, nicht eine Gruppierungszeile) aus.
4. Lesen Sie im unteren Bereich **Arbeitsgangstatusanzeige** den Fertigungsstatus ab: Die Anzeige gibt farblich und in der Liste wieder, ob der Fertigungsauftrag **fest geplant**, **freigegeben**, **in Bearbeitung** oder **beendet** ist.
5. Zum Detail springen: Klicken Sie in der Liste der **Arbeitsgangstatusanzeige** auf die **FA-Nr.**, um den zugehörigen **Fertigungsauftrag** zu öffnen, bzw. auf eine Kachel, um den **FA-Arbeitsplan** einzusehen.

Die weiteren Aktionen der Seite (**Lagerbelege erstellen/registrieren**, **Lagerbelege buchen**) gehören zum Basismodul *m+m Logistic Management* und werden hier nur als Umgebung beschrieben — siehe Abschnitt **Tägliche Arbeit**.

## Einrichtung

Diese Erweiterung erfordert **keine gesonderte Einrichtung**. Sie enthält keine Einrichtungsseite, keine Nummernserie und keine steuernden Kennzeichen. Sobald die App installiert ist, erscheint die **Arbeitsgangstatusanzeige** automatisch auf der Seite **Versandplanungszuordnung und Lagersteuerung**.

Damit die Anzeige jedoch **Inhalte** zeigt, müssen die fachlichen Voraussetzungen aus den zugrunde liegenden Modulen erfüllt sein:

- Die **Versandplanung** aus *m+m Logistic Management* muss eingerichtet sein, damit die Seite **Versandplanungszuordnung und Lagersteuerung** mit Versandzeilen gefüllt werden kann. Die Einrichtung dieser Seite (Filtervorlagen, Lagerorte, Liefertouren) ist Bestandteil des Basismoduls.
- Zur ausgewählten Versandzeile muss ein **Fertigungsauftrag** existieren. Nur dann kann die App über die Verkaufszeile den Fertigungsauftrag ermitteln und den Arbeitsgangstatus anzeigen. Ist kein Fertigungsauftrag vorhanden, bleibt der Bereich **Arbeitsgangstatusanzeige** leer.
- Die App **m+m Routing Status Overview** (Arbeitsgangstatus) liefert die eigentliche Anzeige. Deren Verhalten (Grafik, Farben, Rückmeldungen) ist in der separaten m+m Dokumentation zu **Arbeitsgangstatus** beschrieben.

## Tägliche Arbeit: Versandplanungszuordnung und Arbeitsgangstatusanzeige

Diese Erweiterung wirkt ausschließlich auf der Seite **Versandplanungszuordnung und Lagersteuerung**. Der Anwender arbeitet dort wie gewohnt mit der Versandplanung; zusätzlich beobachtet er im eingeblendeten Bereich **Arbeitsgangstatusanzeige** den Fertigungsfortschritt der jeweils markierten Zeile.

Die Seite wird über die zentralen Einrichtungen des Basismoduls gesteuert (Filtervorlagen, Lagerorte, Liefertouren aus *m+m Logistic Management*). Die App **Logistic Management with Routing Status Overview** selbst steuert nichts davon; sie ergänzt lediglich die Anzeige. Der folgende Aufbau beschreibt die **zusammengeführte Oberfläche**, die der Anwender tatsächlich sieht.

### Einstieg und Seitenaufbau

**Einstieg:** Öffnen Sie über die Suche in Business Central die Seite **Versandplanungszuordnung und Lagersteuerung**. Sie ist eine unternehmensweite Arbeitsseite (kein belegbezogener Aufruf über eine übergeordnete Liste) und daher über **Suchen** zu erreichen.

Die Seite gliedert sich von oben nach unten in:

1. den Filterbereich **Allgemein**,
2. die Liste **Zeilen** mit den Versandpositionen,
3. die Summenzeilen **Ausgewähltes Gesamt-Nettogewicht** / **Ausgewähltes Gesamt-Bruttogewicht**,
4. den durch diese App ergänzten Bereich **Arbeitsgangstatusanzeige**.

### Filter (Bereich Allgemein)

Über die Filter im Bereich **Allgemein** schränken Sie ein, welche Versandpositionen in der Liste **Zeilen** erscheinen. Wird ein Filter gesetzt, werden die Zeilen nach dem jeweiligen Kriterium eingegrenzt; nach jeder Änderung aktualisiert sich die Liste.

| Filterfeld | Erläuterung |
|------------|-------------|
| **Letzte Datenaktualisierung** | Zeigt an, wann die angezeigten Zeilen zuletzt neu berechnet wurden; dient der Kontrolle, ob die Liste aktuell ist. Wenn der Wert veraltet wirkt, wählen Sie **Daten aktualisieren**. |
| **Benutzerfiltervorlagencode** | Wenn gesetzt, werden die gespeicherten Filterwerte der ausgewählten Vorlage geladen und auf die Liste angewendet; so rufen Sie eine wiederkehrende Filterkombination mit einem Griff auf, ohne alle Einzelfilter erneut zu setzen. |
| **Gruppieren nach** | Wenn gesetzt, werden die Zeilen zu Gruppen zusammengefasst (z. B. nach Datum oder Lieferdatum); die Liste zeigt dann Gruppierungszeilen als Baum, unter denen die Positionszeilen einsortiert sind. |
| **Datumsfilter** | Wenn gesetzt, werden nur Zeilen im angegebenen Zeitraum angezeigt; damit blenden Sie z. B. nur die für den heutigen Versand relevanten Positionen ein. |
| **Lagerortfilter** | Wenn gesetzt, werden nur Zeilen des gewählten Lagerorts angezeigt; so bearbeiten Sie gezielt den Versand eines Standorts. |
| **Debitorenfilter** | Wenn gesetzt, werden nur Zeilen der gewählten Debitoren angezeigt; nützlich, wenn Sie eine bestimmte Kundenlieferung vorbereiten. |
| **Liefertourenfilter** | Wenn gesetzt, werden nur Zeilen der gewählten Liefertour angezeigt; damit stellen Sie eine Tour zusammen. |
| **PLZ-Code Filter** | Wenn gesetzt, werden nur Zeilen mit passender Postleitzahl angezeigt; hilfreich bei regionaler Tourenplanung. |
| **Länder-/Regionscode Filter** | Wenn gesetzt, werden nur Zeilen des gewählten Landes bzw. der Region angezeigt. |
| **Mengenfilter** | Wenn gesetzt, werden nur Zeilen angezeigt, deren Menge dem Filterausdruck entspricht; damit trennen Sie z. B. Teil- von Vollmengen. |
| **Verkaufsauftragsfilter** | Wenn gesetzt, werden nur Zeilen der gewählten Verkaufsaufträge angezeigt; so verfolgen Sie einen konkreten Auftrag. |
| **Artikelkategorienfilter** | Wenn gesetzt, werden nur Zeilen der gewählten Artikelkategorie angezeigt. |
| **Filter für EK-Reklamationen** | Wenn gesetzt, werden nur Zeilen der gewählten Einkaufsreklamationen (Rückgabebestellungen) angezeigt; damit planen Sie Rücksendungen im selben Bild. |
| **Lieferbedingungscodefilter** | Wenn gesetzt, werden nur Zeilen der gewählten Lieferbedingung angezeigt. |

Mit der Aktion **Filter für Zuordnung löschen** setzen Sie alle oben genannten Filter zurück; die Liste zeigt danach wieder den ungefilterten Umfang.

### Liste Zeilen

Die Liste **Zeilen** ist als Baum aufgebaut (Gruppierungs- und Positionszeilen). Alle Spalten sind rein informativ (nicht editierbar). Die **Arbeitsgangstatusanzeige** darunter bezieht sich immer auf die aktuell markierte **Positionszeile** (Zeilen vom Typ Line); auf einer reinen Gruppierungszeile bleibt die Anzeige leer.

| Feld | Erläuterung |
|------|-------------|
| **Gruppierungsname** | Bezeichnung der Gruppierungszeile, wenn **Gruppieren nach** aktiv ist; benennt die Sammelzeile im Baum. |
| **Ausgewählt** | Wenn markiert, ist die Zeile für die weiteren Funktionen (z. B. Lagerbelege erstellen) vorgemerkt; die Markierung setzen bzw. entfernen Sie über die Aktionen **Zeilen auswählen** / **Zeilen abwählen**. |
| **Herkunftsnr.** | Nummer des Herkunftsbelegs (z. B. Verkaufsauftrag), aus dem die Versandzeile stammt; stellt den Bezug zum Ursprungsbeleg her. |
| **Artikelnr.** | Artikel der Position; identifiziert die zu versendende Ware. |
| **Variantencode** | Variante des Artikels, sofern geführt. |
| **Artikelkategoriencode** | Artikelkategorie der Position; unterstützt Gruppierung und Filterung. |
| **Lagerortcode** | Lagerort, aus dem versendet wird; bestimmt, welcher Bestand herangezogen wird. |
| **Beschreibung** | Artikelbezeichnung. |
| **Beschreibung 2** | Ergänzende Artikelbezeichnung. |
| **Menge** | Positionsmenge der Versandzeile. |
| **Restmenge** | Noch offene Menge der Position; zeigt, wie viel noch zu versenden ist. |
| **Einheitencode** | Mengeneinheit der Position. |
| **Referenznr.** | Referenznummer (z. B. Artikelreferenz/EAN), sofern hinterlegt. |
| **Bruttogewicht** | Bruttogewicht der Position; fließt in die Summenzeilen ein. |
| **Nettogewicht** | Nettogewicht der Position; fließt in die Summenzeilen ein. |
| **Warenausg.-Datum** | Datum des geplanten Warenausgangs der Position. |
| **Geplantes Lieferdatum** | Geplantes Lieferdatum. |
| **Geplantes Warenausgangsdatum** | Geplantes Warenausgangsdatum. |
| **Gewünschtes Lieferdatum** | Vom Kunden gewünschtes Lieferdatum. |
| **Zugesagtes Lieferdatum** | Dem Kunden zugesagtes Lieferdatum. |
| **Liefertourcode** | Zugeordnete Liefertour der Position. |
| **Lief. an Art** | Art der Lieferadresse (z. B. Standardadresse oder abweichende Adresse). |
| **Lief. an Nr.** | Nummer der abweichenden Lieferadresse, sofern verwendet. |
| **Lief. an Name** | Name der Lieferanschrift. |
| **Lief. an Name 2** | Namenszusatz der Lieferanschrift. |
| **Lief. an Adresse** | Straße/Adresse der Lieferanschrift. |
| **Lief. an Adresse 2** | Adresszusatz der Lieferanschrift. |
| **Lief. an Ort** | Ort der Lieferanschrift. |
| **Lief. an PLZ-Code** | Postleitzahl der Lieferanschrift. |
| **Lief. an Länder-/Regionscode** | Land/Region der Lieferanschrift. |
| **Lagerprozess** | Kennzeichnet den vorgesehenen Lagerprozess der Position (z. B. Warenausgang/Kommissionierung); bestimmt, welche Folgebelege erzeugt werden. |
| **Warenausgang erstellt** | Wenn gesetzt, wurde für die Position bereits ein Warenausgang erzeugt; verhindert doppelte Belegerstellung und zeigt den Bearbeitungsstand. |
| **Warenausgangsnr.** | Nummer des erzeugten Warenausgangs; verweist auf den Folgebeleg. |
| **Warenausgangszeilennr.** | Zeilennummer im Warenausgang. |
| **Kommissionierung erstellt** | Wenn gesetzt, wurde bereits eine Kommissionierung erzeugt; zeigt, dass die Position im Lager in Bearbeitung ist. |
| **Kommissionierungsnr.** | Nummer der erzeugten Kommissionierung. |
| **Kommissionierungszeilennr.** | Zeilennummer in der Kommissionierung. |
| **Fertigungsauftrag erstellt** | Wenn gesetzt, existiert zur Position ein Fertigungsauftrag; nur dann kann die **Arbeitsgangstatusanzeige** einen Status zeigen. |
| **FA-Status** | Fertigungsauftragsstatus der Position (siehe Statuswerte unten); zeigt, wie weit die Fertigung fortgeschritten ist. |
| **FA-Nr.** | Nummer des zugehörigen Fertigungsauftrags. |
| **Fertig gestellte Menge** | Bereits fertiggestellte Menge des Fertigungsauftrags; zeigt, wie viel der bestellten Menge bereits produziert ist. |
| **Menge für Versandplanung** | Für die Versandplanung verfügbare Menge der Position; Grundlage der Zuordnung zum Versand. |
| **Lieferbedingungscode** | Lieferbedingung der Position. |

**FA-Status — Bedeutung der Werte.** Das Feld **FA-Status** spiegelt den Status des zugehörigen Fertigungsauftrags. Dieselben Werte bestimmen die Farbe der **Arbeitsgangstatusanzeige**:

- **Simuliert:** Der Fertigungsauftrag dient nur der Vorschau/Kalkulation; es wird nicht produziert.
- **Geplant:** Der Fertigungsauftrag ist geplant, aber noch nicht fest eingeplant; noch keine Freigabe zur Fertigung.
- **Fest geplant:** Der Fertigungsauftrag ist fest eingeplant, aber noch nicht freigegeben — es kann noch nicht gefertigt werden.
- **Freigegeben:** Der Fertigungsauftrag ist zur Fertigung freigegeben; Rückmeldungen/Buchungen auf die Arbeitsgänge sind möglich.
- **Beendet:** Der Fertigungsauftrag ist abgeschlossen; die Ware gilt als fertiggestellt und ist versandbereit.

### Summen

Unter der Liste fasst die Seite die Gewichte der **ausgewählten** Zeilen zusammen:

| Feld | Erläuterung |
|------|-------------|
| **Ausgewähltes Gesamt-Nettogewicht** | Summe des Nettogewichts aller markierten Zeilen; unterstützt die Beladungs- und Tourenplanung. |
| **Ausgewähltes Gesamt-Bruttogewicht** | Summe des Bruttogewichts aller markierten Zeilen. |

### Arbeitsgangstatusanzeige (durch diese App ergänzt)

Der Bereich **Arbeitsgangstatusanzeige** ist der eigentliche Beitrag dieser Erweiterung. Er erscheint unterhalb der Zeilen und zeigt zur aktuell markierten **Positionszeile** den Fertigungsstatus des dahinterliegenden **Fertigungsauftrags**. Grundlage ist die Verkaufszeile der Versandzeile: Die App ermittelt zu **Herkunftsnr.** und Zeile die Verkaufszeile und übergibt sie an die Anzeige.

Die Anzeige besteht aus zwei zusammengehörigen Teilen:

- **Grafische Anzeige:** Kacheln stellen die Arbeitsgänge des Fertigungsauftrags dar. Ihre Farbe richtet sich nach dem Zustand:
  - **Grau** — Fertigungsauftrag **fest geplant**: noch nicht fertigbar.
  - **Grün** — Fertigungsauftrag **freigegeben**: bereit für die Fertigung.
  - **Rot** — Arbeitsgang **gestartet / in Bearbeitung**: der Auftragsstatus selbst ändert sich dadurch nicht.
  - **Blau** — Arbeitsgang bzw. Fertigungsauftrag **beendet**: Fertigung abgeschlossen.
- **Listenanzeige:** Eine tabellarische Zusammenfassung des Fertigungsauftrags, u. a. **Ebene**, **Status**, **FA-Nr.** und Mengen. Über die **Ebene** werden mehrstufige Fertigungsaufträge als Baum dargestellt.

**Navigation aus der Anzeige heraus.** Ein Klick auf die **FA-Nr.** in der Liste öffnet den zugehörigen Fertigungsauftrag — je nach Status die Karte **Simulierter FA**, **Geplanter FA**, **Fest geplanter FA**, **Freigegebener FA** oder **Beendeter FA**. Ein Klick auf eine Kachel öffnet den **FA-Arbeitsplan** des Fertigungsauftrags. So gelangen Sie ohne Umweg von der Versandzeile direkt in den Fertigungsauftrag, um dort weiterzuarbeiten.

> Hinweis: Sind zu einem Verkaufsauftrag mehrere Verkaufszeilen vorhanden, wechselt die **Arbeitsgangstatusanzeige** entsprechend, sobald Sie eine andere **Zeile** markieren. Die vollständige Beschreibung der Anzeige (Grafik, Rückmeldungen, Bearbeitung des Fertigungsauftrags) finden Sie in der separaten m+m Dokumentation **Arbeitsgangstatus**.

### Umgebung: Lagerbelege und weitere Aktionen (Basismodul)

Die folgenden Aktionen befinden sich auf derselben Seite, gehören jedoch zum Basismodul *m+m Logistic Management* und werden hier nur als Umgebung genannt, damit die Oberfläche vollständig verständlich ist. Sie werden nicht durch diese Erweiterung bereitgestellt:

- **Auswahl:** **Zeilen auswählen**, **Zeilen abwählen**, **Alle Zeilen anzeigen**, **Ausgewählte Zeilen anzeigen** — steuern, welche Zeilen markiert bzw. sichtbar sind.
- **Funktionen:** **Daten aktualisieren**, **Zeilen zur Versandplanung hinzufügen**, **Filter für Zuordnung löschen**, **Lagerbelege erstellen/registrieren**.
- **Lagerbelege buchen** und **Lagerbelege buchen und senden** — buchen die erzeugten Lagerbelege; vor dem Buchen erscheint eine Bestätigungsabfrage.
- **Zeile:** **Belege anzeigen**, **Lagerplatzinhaltsübersicht**.
- **Belege:** **Versandplanung** (öffnet die Liste der Versandplanungen).

Für die Arbeit mit der **Arbeitsgangstatusanzeige** sind diese Aktionen nicht erforderlich; die Anzeige aktualisiert sich allein durch die Auswahl einer Zeile.

## FAQ und Troubleshooting

### 1. Warum sehe ich in der Arbeitsgangstatusanzeige nichts?
Die Anzeige füllt sich nur, wenn zur markierten **Positionszeile** ein **Fertigungsauftrag** existiert. Prüfen Sie in der Zeile das Feld **Fertigungsauftrag erstellt** bzw. die **FA-Nr.**. Ist kein Fertigungsauftrag vorhanden, bleibt der Bereich leer.

### 2. Warum bleibt die Anzeige leer, obwohl eine Zeile markiert ist?
Die App wertet nur Zeilen vom Typ **Positionszeile** aus. Auf einer **Gruppierungszeile** (bei aktivem **Gruppieren nach**) wird nichts angezeigt. Klappen Sie die Gruppe auf und markieren Sie eine Einzelposition.

### 3. Muss ich die App einrichten, bevor ich sie nutzen kann?
Nein. Die Erweiterung benötigt keine eigene Einrichtung. Voraussetzung ist lediglich, dass die Versandplanung des Basismoduls genutzt wird und zur Zeile ein Fertigungsauftrag besteht.

### 4. Woher weiß ich, ob die Ware fertig ist?
Steht der **FA-Status** auf **Beendet** und erscheinen die Kacheln der Arbeitsgangstatusanzeige **blau**, ist der Fertigungsauftrag abgeschlossen und die Ware fertiggestellt. Das Feld **Fertig gestellte Menge** zeigt zusätzlich die produzierte Menge.

### 5. Was bedeuten die Farben Grau, Grün, Rot und Blau?
**Grau** = Fertigungsauftrag fest geplant (noch nicht fertigbar), **Grün** = freigegeben (fertigbar), **Rot** = Arbeitsgang gestartet/in Bearbeitung, **Blau** = Arbeitsgang bzw. Fertigungsauftrag beendet.

### 6. Ändert die Farbe Rot den Status des Fertigungsauftrags?
Nein. Rot zeigt nur an, dass mindestens ein Arbeitsgang gestartet bzw. in Bearbeitung ist. Der übergeordnete **FA-Status** (z. B. **Freigegeben**) bleibt davon unberührt.

### 7. Wie öffne ich den Fertigungsauftrag zu einer Versandzeile?
Klicken Sie in der Liste der **Arbeitsgangstatusanzeige** auf die **FA-Nr.**. Je nach Status öffnet sich die passende Fertigungsauftragskarte (**Fest geplanter FA**, **Freigegebener FA**, **Beendeter FA** usw.).

### 8. Wie sehe ich die einzelnen Arbeitsgänge?
Klicken Sie in der grafischen Anzeige auf eine Kachel. Es öffnet sich der **FA-Arbeitsplan** des Fertigungsauftrags mit den Arbeitsgängen.

### 9. Ich habe mehrere Verkaufszeilen — welche wird angezeigt?
Immer die zur aktuell markierten **Zeile** gehörende. Markieren Sie eine andere Zeile, wechselt die Anzeige entsprechend.

### 10. Wo finde ich die vollständige Beschreibung der Anzeige selbst?
In der separaten m+m Dokumentation zur App **Arbeitsgangstatus** (*m+m Routing Status Overview*). Dieses Handbuch beschreibt die Einbindung der Anzeige in die **Versandplanungszuordnung und Lagersteuerung**.

## Typische Anwendungsfälle

### Anwendungsfall 1: Versandfreigabe erst nach Fertigstellung prüfen

**Auslöser.** Der Sachbearbeiter Versand möchte vor dem Erstellen der Lagerbelege sicherstellen, dass die Ware einer Kundenposition bereits gefertigt ist.

**Einstieg in BC.** Er öffnet über die Suche die Seite **Versandplanungszuordnung und Lagersteuerung** und grenzt die Positionen über **Lagerortfilter** und **Datumsfilter** ein; anschließend wählt er **Daten aktualisieren**.

**Kernablauf.** In der Liste **Zeilen** markiert er die betreffende Positionszeile. Im Bereich **Arbeitsgangstatusanzeige** erkennt er den Zustand: Sind die Kacheln **blau** und steht der **FA-Status** auf **Beendet**, ist die Ware fertig. Zur Kontrolle prüft er zusätzlich **Fertig gestellte Menge**.

**Abschluss.** Ist die Position fertig, markiert er die Zeile über **Zeilen auswählen** und stößt die weitere Versandbearbeitung des Basismoduls an (**Lagerbelege erstellen/registrieren**). Ist die Anzeige noch **rot** (in Bearbeitung) oder **grau** (fest geplant), verschiebt er die Position und wendet sich der nächsten zu.

### Anwendungsfall 2: Rückfrage zum Fertigungsfortschritt einer Versandzeile

**Auslöser.** Die Disposition erhält telefonisch die Frage, wie weit der Fertigungsauftrag zu einer bestimmten Versandposition fortgeschritten ist.

**Einstieg in BC.** Die Mitarbeiterin öffnet die Seite **Versandplanungszuordnung und Lagersteuerung** und setzt den **Verkaufsauftragsfilter** auf den genannten Auftrag.

**Kernablauf.** Sie markiert die betreffende **Zeile**. Die **Arbeitsgangstatusanzeige** zeigt Grafik und Liste des Fertigungsauftrags. Über die Farbe der Kacheln liest sie ab, welche Arbeitsgänge bereits gestartet (**rot**) oder beendet (**blau**) sind.

**Abschluss.** Für Details klickt sie in der Liste auf die **FA-Nr.** und öffnet den **Freigegebenen FA**; über eine Kachel ruft sie bei Bedarf den **FA-Arbeitsplan** auf und beantwortet die Rückfrage anhand des konkreten Arbeitsgangfortschritts.
