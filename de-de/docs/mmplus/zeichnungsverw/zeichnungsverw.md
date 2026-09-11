---
title: Anwenderhandbuch m+m Drawing Management
---

# Anwenderhandbuch m+m Drawing Management

## 1. Einleitung

Die App **m+m Drawing Management** (Zeichnungsverwaltung) verwaltet **Zeichnungen** und
**Zeichnungsmappen** zentral in Microsoft Dynamics 365 Business Central und verknüpft sie mit
Artikeln, Artikelvarianten sowie mit Verkaufs-, Einkaufs-, Service-, Montage-, Fertigungs- und
Projektbelegen. Jede Zeichnung wird versioniert geführt: Zu einer **Interne Nr.** existieren
mehrere **Versionen**, von denen genau eine als **Aktiv** gekennzeichnet ist. Belege übernehmen
beim Anlegen eine unveränderliche Referenz auf die zum Zeitpunkt gültige aktive Version, sodass
jederzeit nachvollziehbar bleibt, welche Zeichnung in welcher Ausgabe an einem Vorgang beteiligt war.

**Zielgruppe.** Primäre Anwender sind **operative Fachkräfte**, die im Tagesgeschäft mit Artikeln
und Belegen arbeiten – Arbeitsvorbereitung, Konstruktionsbüro, Verkauf, Einkauf, Fertigung und
Service. Sie legen Zeichnungen an, pflegen Versionen, weisen Zeichnungen Artikeln zu, öffnen die
hinterlegte Zeichnung direkt aus der Belegzeile und laden hinterlegte Dateien herunter.
**Sekundär** sind Administratoren und Key-User, die einmalig die **Nummernserien** sowie die
Stammdaten **Zeichnungsarten** und **Zeichnungsverbindungen** einrichten.

**Kurzer Prozessüberblick.** Der Administrator hinterlegt die Nummernserien in der
**Zeichnungsverwaltung Einrichtung**. Danach pflegen Anwender die Stammdaten **Zeichnungen** und
**Zeichnungsmappen**, versehen sie mit **Versionen** und **Bemerkungen** und weisen sie über
**Artikel zuweisen** oder direkt auf der **Artikelkarte** einem oder mehreren Artikeln zu. Sobald ein
Artikel mit einer Zeichnungsreferenz in einem Beleg verwendet wird, erscheint die Referenz in der
Belegzeile, die zugehörigen Dateien werden in der Infobox **Zeichnung - Dokumente** angezeigt, und
über die Aktionsgruppe **Zeichnungsverwaltung** lässt sich die Zeichnung öffnen oder eine neue
anlegen.

## 2. Schnellstart für Anwender

Reihenfolge in Abhängigkeit der technischen Voraussetzungen (Einrichtung zuerst):

1. **Einrichtung prüfen.** Öffnen Sie über **Suchen** die Seite **Zeichnungsverwaltung Einrichtung**
   und hinterlegen Sie im Inforegister **Nummerierung** die Felder **Interne Zeichnungsnummern** und
   **Interne Zeichnungsmappennummern**. Ohne diese Nummernserien lässt sich keine Zeichnung anlegen.
2. **Stammdaten anlegen (optional, aber empfohlen).** Pflegen Sie über **Suchen** die Listen
   **Zeichnungsarten** und **Zeichnungsverbindungen**, damit Zeichnungen klassifiziert werden können.
3. **Zeichnung anlegen.** Öffnen Sie über **Suchen** die Liste **Zeichnungen** und legen Sie mit
   *Neu* eine Zeichnung an. Die **Interne Nr.** wird aus der Nummernserie vergeben. Tragen Sie
   **Zeichnungsnr.**, **Beschreibung** und ggf. **Zeichnungsartencode** und
   **Zeichnungsverbindungscode** ein.
4. **Version erzeugen und aktiv setzen.** Wählen Sie im Inforegister **Versionen** die Aktion
   **Neue Version erstellen**, tragen Sie **Revisionsnr.** und **Zeichnungs-URL** ein und setzen Sie
   den Haken **Aktiv**. Erst eine aktive Version wird in Belegen als Referenz herangezogen.
5. **Artikel zuweisen.** Wählen Sie auf der Zeichnung die Aktion **Artikel zuweisen** und markieren
   Sie im Fenster **Artikelzuweisung** die betroffenen Artikel bzw. Artikelvarianten über das
   Kennzeichen **Zugewiesen**. Alternativ setzen Sie die Referenz direkt auf der **Artikelkarte**
   (Gruppe **Zeichnungsverwaltung**).
6. **Im Beleg nutzen.** Verwenden Sie den Artikel in einer Beleg-/Fertigungszeile. Die Infobox
   **Zeichnung - Dokumente** zeigt die hinterlegten Dateien; über die Zeilenaktion **Zeichnung öffnen**
   gelangen Sie zur Zeichnung, über **Datei herunterladen** laden Sie die Datei herunter.

Die Zeichnungsmappe (**Zeichnungsmappen** → **Zeichnungsmappe**) fasst mehrere Zeichnungen zu einer
Sammlung zusammen und wird analog versioniert und zugewiesen (siehe §4.2).

## 3. Einrichtung

### 3.1 Nummerierung einrichten

**Wer und wann.** Der Administrator richtet die Nummernserien **einmalig vor der ersten Nutzung** ein.
Ohne sie schlägt das Anlegen einer Zeichnung oder Zeichnungsmappe fehl, weil beim Einfügen eine
Nummer aus der Serie gezogen wird (`TestField` auf die jeweilige Nummernserie).

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Zeichnungsverwaltung Einrichtung**. Es handelt
sich um eine unternehmensweite Einrichtungsseite mit genau einem Datensatz; beim Öffnen wird der
Datensatz automatisch initialisiert.

**Voraussetzung.** Legen Sie zuvor in der Standard-**Nr.-Serie**-Einrichtung von Business Central
zwei Nummernserien an (eine für Zeichnungen, eine für Zeichnungsmappen).

| Einrichtung | Erläuterung |
|---|---|
| **Interne Zeichnungsnummern** | Wenn hier eine **Nr.-Serie** gesetzt ist, erhält jede neue Zeichnung beim Anlegen automatisch eine fortlaufende **Interne Nr.** aus dieser Serie; ist das Feld leer, lässt sich keine Zeichnung anlegen. Diese interne Nummer ist der dauerhafte, systeminterne Schlüssel der Zeichnung (unabhängig von der frei vergebbaren **Zeichnungsnr.**). |
| **Interne Zeichnungsmappennummern** | Wenn hier eine **Nr.-Serie** gesetzt ist, erhält jede neue **Zeichnungsmappe** beim Anlegen automatisch eine fortlaufende **Interne Nr.**; ist das Feld leer, lässt sich keine Zeichnungsmappe anlegen. |

**Prozessschritte (Reihenfolge).** Zuerst die beiden Nummernserien in der **Nr.-Serie**-Einrichtung
von Business Central anlegen; danach diese Serien in der **Zeichnungsverwaltung Einrichtung** in den
Feldern **Interne Zeichnungsnummern** und **Interne Zeichnungsmappennummern** hinterlegen;
schließlich stehen die Aktionen **Neue Zeichnung erstellen** / **Neue Zeichnungsmappe erstellen** in
den Stammdaten und in den Belegzeilen (§6) zur Verfügung. Diese Einrichtung ist die Voraussetzung für
alle in §4 und §6 beschriebenen Vorgänge.

Weitere Einrichtungsfelder besitzt diese App nicht; die Einrichtung beschränkt sich bewusst auf die
Nummernvergabe. Die inhaltliche Klassifizierung erfolgt über die Stammdaten in §4.3.

## 4. Stammdaten

Die Stammdaten sind der Kern der Zeichnungsverwaltung. Sie werden von Anwendern gepflegt und steuern,
welche Zeichnung in welcher Version an Artikeln und Belegen erscheint.

### 4.1 Zeichnungen

**Wer und wann.** Konstruktion/Arbeitsvorbereitung legt Zeichnungen an, sobald ein neues
Dokument (z. B. eine CAD-Zeichnung als Datei oder Link) im Unternehmen geführt werden soll. Die hier
aktiv gesetzte Version wird später in Artikeln (§5) und Belegen (§6) verwendet.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Zeichnungen** und öffnen Sie mit *Neu* oder per
Klick auf eine Zeile die Karte **Zeichnung**.

Die Liste **Zeichnungen** zeigt je Zeichnung eine Zeile (nur die Basissätze, interne Versionsnr. 0):

| Feld | Erläuterung |
|---|---|
| **Interne Nr.** | Systeminterner, eindeutiger Schlüssel der Zeichnung aus der Nummernserie; kann nicht umbenannt werden. |
| **Zeichnungsnr.** | Frei vergebbare, sprechende Zeichnungsnummer (z. B. die Nummer laut Konstruktion). Wenn gesetzt, dient sie der Wiedererkennung; sie ist nur auf der Basisversion (Version 0) pflegbar. |
| **Beschreibung** | Klartextbezeichnung der Zeichnung; erscheint in Nachschlagelisten und Infoboxen. |
| **Zeichnungsartencode** | Wenn gesetzt, ordnet er die Zeichnung einer **Zeichnungsart** zu (§4.3) und ermöglicht Filterung/Auswertung nach Art. |
| **Zeichnungsverbindungscode** | Wenn gesetzt, verknüpft er die Zeichnung mit einer **Zeichnungsverbindung** (§4.3); dieselbe Verbindung kann u. a. an Arbeitsgangzeilen verwendet werden, um zusammengehörige Zeichnungen zu bündeln. |
| **Aktive interne Versionsnr.** | Zeigt an, welche Version aktuell **Aktiv** ist; nur diese Version wird in Belegen referenziert. Wird automatisch gepflegt, wenn Sie eine Version aktiv setzen. |
| **Aktive Revisionsnr.** | Zeigt die **Revisionsnr.** der aktiven Version an (abgeleitet, nicht direkt editierbar). |

Auf der Karte **Zeichnung** stehen im Inforegister **Allgemein** dieselben Kopf-Felder
(**Interne Nr.**, **Zeichnungsnr.**, **Beschreibung**, **Zeichnungsartencode**,
**Zeichnungsverbindungscode**, **Aktive interne Versionsnr.**, **Aktive Revisionsnr.**). Über das
Feld **Interne Nr.** kann per AssistEdit eine verwandte Nummernserie ausgewählt werden.

**Versionen pflegen.** Der Unterbereich **Versionen** listet alle Versionen (interne Versionsnr. ≠ 0):

| Feld | Erläuterung |
|---|---|
| **Interne Versionsnr.** | Fortlaufende Versionsnummer innerhalb der Zeichnung; wird automatisch vergeben, nicht editierbar. |
| **Revisionsnr.** | Frei vergebbarer Revisionsstand dieser Version (z. B. „A", „B", Index). |
| **Zeichnungs-URL** | Wenn gesetzt, verweist sie auf die abgelegte Zeichnungsdatei/den Speicherort; Standardmäßig ausgeblendet, kann eingeblendet werden. |
| **Aktiv** | Wenn Sie den Haken setzen, wird diese Version zur gültigen Version: jede zuvor aktive Version derselben Zeichnung wird automatisch deaktiviert und die **Aktive interne Versionsnr.** auf diese Version gesetzt. Ohne aktive Version wird die Zeichnung in Belegen nicht als Referenz herangezogen. |
| **Bemerkungen vorhanden** | Wenn markiert, existieren zu dieser Version bereits **Bemerkungen**; ein Klick führt zum Bemerkungsblatt. |
| **Erstellt von** / **Geändert von** | Anzeige des anlegenden bzw. zuletzt ändernden Benutzers (Klarname); dient der Nachvollziehbarkeit. |
| **SystemCreatedAt** / **SystemModifiedAt** | Zeitstempel der Anlage bzw. letzten Änderung dieser Version. |

Aktionen im Unterbereich **Versionen**:

1. **Neue Version erstellen** – Legt eine leere Folgeversion an (nächste **Interne Versionsnr.**).
   Wenn Sie damit arbeiten, dokumentieren Sie einen neuen Stand, ohne die bisherige Version zu
   verändern.
2. **In neue Version kopieren** – Legt eine Folgeversion an und übernimmt **Revisionsnr.**,
   **Zeichnungs-URL** und die vorhandenen **Bemerkungen** der aktuellen Version. Nutzen Sie dies bei
   einer Revision, bei der der bisherige Inhalt Ausgangspunkt bleibt. Die neue Version wird zunächst
   **nicht** aktiv gesetzt.
3. **Bemerkungen** – Öffnet das Bemerkungsblatt der Version zum Erfassen datierter Kommentare
   (Felder **Datum** und **Bemerkung**; das **Datum** wird beim ersten Kommentar eines Tages
   automatisch auf heute vorbelegt).

**Artikel zuweisen.** Über die Aktion **Artikel zuweisen** auf der Karte **Zeichnung** öffnen Sie die
Seite **Artikelzuweisung** (siehe §5).

**Dateien.** In der Infobox **Zeichnung - Dokumente** (bereitgestellt über die abhängige App-Funktion
DropZone/Media Storage) legen Sie Dateien per Drag-and-drop zur jeweiligen Version ab und laden sie
über **Datei herunterladen** wieder herunter.

**Löschregel.** Eine Zeichnung kann nicht gelöscht werden, solange mindestens ein Element (z. B. eine
Zeichnungsmappe) sie enthält; das System weist dies mit einer Meldung ab.

### 4.2 Zeichnungsmappen

Eine **Zeichnungsmappe** bündelt mehrere **Zeichnungen** zu einer benannten Sammlung – etwa alle
Zeichnungen einer Baugruppe. Auch die Mappe wird versioniert; jede Mappenversion enthält ihre eigene
Zusammenstellung von Zeichnungen.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Zeichnungsmappen** und öffnen Sie die Karte
**Zeichnungsmappe**.

Kopf-Felder der Karte (Inforegister **Allgemein**):

| Feld | Erläuterung |
|---|---|
| **Interne Nr.** | Systeminterner Schlüssel der Mappe aus der Nummernserie **Interne Zeichnungsmappennummern**. |
| **Zeichnungsmappennr.** | Frei vergebbare, sprechende Mappennummer. |
| **Beschreibung** | Bezeichnung der Mappe. |
| **Aktive interne Versionsnr.** | Zeigt die aktive Mappenversion; nur diese wird in Belegen referenziert. |
| **Aktive Revisionsnr.** | Revisionsstand der aktiven Mappenversion (abgeleitet). |

Unterbereich **Versionen** der Mappe (Felder wie bei der Zeichnung: **Interne Versionsnr.**,
**Revisionsnr.**, **Aktiv**, **Bemerkungen vorhanden**, **Erstellt von**/**Geändert von**,
**SystemCreatedAt**/**SystemModifiedAt**) mit den Aktionen **Neue Version erstellen**,
**In neue Version kopieren** (übernimmt zusätzlich die zugeordneten Zeichnungen der Version) und
**Bemerkungen**.

Unterbereich **Zeichnungen** der Mappe (Seite „Zeichnungen" der Mappe) – die zur gewählten
Mappenversion gehörenden Zeichnungen:

| Feld | Erläuterung |
|---|---|
| **Interne Zeichnungsnr.** | Interner Schlüssel der eingebundenen Zeichnung (nicht editierbar). |
| **Interne Zeichnungsversionsnr.** | Version der eingebundenen Zeichnung (nicht editierbar). |
| **Zeichnungsnr.** | Sprechende Nummer der Zeichnung (abgeleitet). |
| **Zeichnungsrevisionsnr.** | Revisionsstand der eingebundenen Zeichnungsversion (abgeleitet). |
| **Zeichnungsbeschreibung** | Beschreibung der Zeichnung (abgeleitet). |
| **Zeichnungsartencode** / **Zeichnungsverbindungscode** | Klassifizierung der Zeichnung (abgeleitet). |
| **Bemerkungen vorhanden** | Zeigt an, ob zur eingebundenen Zeichnungsversion Bemerkungen bestehen. |
| **Zeichnung erstellt von/am**, **Zeichnung geändert von/am** | Audit-Angaben der Zeichnungsversion (Sammelinformation; als Gruppe dokumentiert, dienen nur der Nachvollziehbarkeit). |

Aktionen im Unterbereich **Zeichnungen** (nur aktiv, wenn die Mappe mindestens eine Version besitzt):

1. **Vorhandene Zeichnung hinzufügen** – Öffnet die Auswahl **Zeichnungsversionen**; die gewählte
   Zeichnungsversion wird als neue Zeile in die Mappe aufgenommen.
2. **Neue Zeichnung erstellen** – Legt eine neue Zeichnung an, nimmt sie in die Mappe auf und öffnet
   sie sofort zur Bearbeitung.

Die Infoboxen der Mappenkarte (**Zeichnungsmappe - Informationen**, **Zeichnungsmappe - Bemerkungen**,
**Zeichnung - Informationen**, **Zeichnung - Versionen**, **Zeichnung - Bemerkungen**,
**Zeichnung - Dokumente**) zeigen kontextbezogen die Verwendungszähler und Dateien zur jeweils
markierten Mappe bzw. eingebundenen Zeichnung an.

### 4.3 Zeichnungsarten und Zeichnungsverbindungen

Beide Listen sind einfache Klassifizierungsstammdaten, die Zeichnungen strukturieren.

**Wer und wann.** Ein Key-User legt sie **vor** der breiten Nutzung an, damit Zeichnungen einheitlich
klassifiziert werden. Sie werden anschließend in den Feldern **Zeichnungsartencode** bzw.
**Zeichnungsverbindungscode** der Zeichnung (§4.1) verwendet.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Zeichnungsarten** bzw. **Zeichnungsverbindungen**.

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger, nicht leerer Schlüssel der Art bzw. Verbindung; wird an der Zeichnung als **Zeichnungsartencode** / **Zeichnungsverbindungscode** ausgewählt. |
| **Beschreibung** | Klartextbezeichnung. |

**Löschverhalten (Wenn …, dann …).** Wenn Sie eine **Zeichnungsart** löschen, dann wird der
**Zeichnungsartencode** aus allen Zeichnungen entfernt, die ihn verwendet haben – die Zeichnungen
bleiben bestehen, sind danach aber ohne Art. Wenn Sie eine **Zeichnungsverbindung** löschen, dann
wird der **Zeichnungsverbindungscode** sowohl aus allen betroffenen Zeichnungen als auch aus den
verknüpften **Arbeitsgangzeilen** entfernt.

## 5. Zuordnung an Artikel und Varianten

Die einzige Zuordnungslogik dieses Moduls verknüpft **Zeichnungen/Zeichnungsmappen mit Artikeln und
Artikelvarianten**. Über diese Zuordnung „wandert" die aktive Zeichnungsversion später automatisch in
die Belege, in denen der Artikel verwendet wird (§6). Es gibt keine Debitoren- oder
Profilzuordnungen; die vorliegende Zuordnung ersetzt das Kapitel „Profile und Zuordnungen".

**Zwei Wege der Zuordnung.**

- **Aus der Zeichnung heraus:** Aktion **Artikel zuweisen** auf der Karte **Zeichnung** bzw.
  **Zeichnungsmappe** öffnet die Seite **Artikelzuweisung**.
- **Aus dem Artikel heraus:** Gruppe **Zeichnungsverwaltung** auf der **Artikelkarte** bzw.
  **Artikelvariantenkarte**.

**Seite Artikelzuweisung.** Die Worksheet-Seite zeigt oben die Referenz und darunter eine
Baumstruktur aus Artikeln (obere Ebene) und deren Artikelvarianten (untere Ebene):

| Feld | Erläuterung |
|---|---|
| **Zeichnungsreferenzart** | Zeigt an, ob die Zuweisung eine **Zeichnung** oder eine **Zeichnungsmappe** betrifft (vorbelegt durch die aufrufende Aktion, nicht änderbar). |
| **Zeichnungsreferenznr.** | Interne Nr. der zuzuweisenden Zeichnung/Mappe (nicht änderbar). |
| **Artikelnr.** | Artikel der jeweiligen Baumzeile. |
| **Variantencode** | Variante des Artikels (untergeordnete Baumzeile). |
| **Beschreibung** / **Beschreibung 2** | Bezeichnung des Artikels bzw. der Variante. |
| **Zugewiesen** | Wenn Sie den Haken setzen, wird die aktuelle Zeichnung/Mappe als Referenz in den Artikel bzw. die Variante geschrieben; wenn Sie ihn entfernen, wird die Referenz dort wieder gelöscht. So steuern Sie zeilenweise, welche Artikel diese Zeichnung führen. |

**Felder der Gruppe Zeichnungsverwaltung auf Artikelkarte/Artikelvariantenkarte.**

| Feld | Erläuterung |
|---|---|
| **Zeichnungsreferenzart** | Bestimmt, ob dem Artikel eine einzelne **Zeichnung** oder eine **Zeichnungsmappe** zugeordnet ist. **(leer):** keine Zeichnungsreferenz – der Artikel führt keine Zeichnung, die Folgefelder und Infoboxen bleiben ausgeblendet. **Zeichnung:** eine einzelne Zeichnung wird referenziert; das Feld **Zeichnung aktive Versionsnr.** und die Zeichnungs-Infobox werden eingeblendet. **Zeichnungsmappe:** eine Zeichnungsmappe wird referenziert; das Feld **Zeichnungsmappe aktive Versionsnr.** und die Mappen-Infobox werden eingeblendet. Wenn Sie die Art ändern, wird die **Zeichnungsreferenznr.** automatisch geleert, damit keine unpassende Nummer stehen bleibt. |
| **Zeichnungsreferenznr.** | Interne Nr. der zugeordneten Zeichnung bzw. Zeichnungsmappe (Auswahl per Nachschlagen; die Auswahlliste richtet sich nach der gewählten **Zeichnungsreferenzart**). Nach dem Setzen wird die Karte aktualisiert, sodass aktive Versionsnr. und Infobox passen. |
| **Zeichnung aktive Versionsnr.** | Zeigt (bei Art **Zeichnung**) die aktuell aktive Version der referenzierten Zeichnung an; nicht editierbar. |
| **Zeichnungsmappe aktive Versionsnr.** | Zeigt (bei Art **Zeichnungsmappe**) die aktive Version der referenzierten Mappe an; nicht editierbar. |

**Vorrangregel (Wenn …, dann …).** Wenn eine **Artikelvariante** eine eigene Zeichnungsreferenz
besitzt, dann gilt diese; ist die Variante ohne eigene Referenz, dann fällt die Zuordnung auf die
Referenz des **Artikels** zurück. So können Sie eine allgemeine Artikelzeichnung führen und für
einzelne Varianten abweichende Zeichnungen hinterlegen.

## 6. Zeichnungen in Belegen und Fertigung

Dieses Modul besitzt keinen eigenen Hauptbeleg. Es erweitert stattdessen die Standardbelege von
Business Central – **Verkaufsauftrag**, **Einkaufsbestellung**, **Serviceauftrag**,
**Montageauftrag**, Angebote, Reklamationen, Gutschriften und deren Archive, Fertigungsaufträge
(simuliert, geplant, fest geplant, freigegeben, beendet) mit Zeilen, Komponenten und
Arbeitsgängen, Projektplanungszeilen, das **Artikel Buch.-Blatt** sowie Stücklisten. In all diesen
Belegen wird pro Zeile automatisch die aktive Zeichnungsreferenz des verwendeten Artikels/der Variante
mitgeführt und in den gebuchten Belegen sowie Artikelposten festgehalten.

**Voraussetzung/Steuerung.** Welche Zeichnung erscheint, wird ausschließlich über die Stammdaten
gesteuert: die aktive Version der Zeichnung (§4.1/§4.2) und die Artikel-/Variantenzuordnung (§5). In
den Belegzeilen selbst sind die Referenzfelder schreibgeschützt und standardmäßig ausgeblendet.

**Referenzfelder in der Belegzeile (schreibgeschützt, bei Bedarf einblendbar).**

| Feld | Erläuterung |
|---|---|
| **Zeichnungsreferenzart** | Zeigt, ob die Zeile auf eine **Zeichnung** oder **Zeichnungsmappe** verweist – übernommen aus Artikel/Variante beim Anlegen der Zeile. |
| **Zeichnungsreferenznr.** | Interne Nr. der referenzierten Zeichnung/Mappe (Momentaufnahme). |
| **Zeichnungsreferenz Versionsnr.** | Die zum Zeitpunkt der Zeilenanlage aktive Version – dokumentiert unveränderlich, welche Ausgabe gültig war. |

**Aktionsgruppe Zeichnungsverwaltung in der Belegzeile.** In den Zeilenbereichen (z. B.
**Verkaufsauftrag** → Zeilen) stehen unter **Zeichnungsverwaltung** je nach Zeilenzustand folgende
Aktionen bereit (nur bei Zeilen vom Typ Artikel mit gefüllter **Nr.**):

1. **Zeichnung öffnen** – sichtbar, wenn die Zeile auf eine **Zeichnung** verweist; öffnet die
   zugehörige Zeichnung.
2. **Zeichnungsmappe öffnen** – sichtbar, wenn die Zeile auf eine **Zeichnungsmappe** verweist;
   öffnet die zugehörige Mappe.
3. **Neue Zeichnung erstellen** – sichtbar, wenn der Artikel/die Variante noch keine
   Zeichnungsreferenz hat; legt eine neue Zeichnung an, verknüpft sie mit Artikel/Variante und öffnet
   sie sofort.
4. **Neue Zeichnungsmappe erstellen** – analog für eine neue Zeichnungsmappe.

**Dateivorschau.** Zu jeder Belegzeile zeigt die Infobox **Zeichnung - Dokumente** die hinterlegten
Dateien der referenzierten (aktiven) Zeichnungsversion; über **Datei herunterladen** öffnen/speichern
Sie die Datei.

**Übernahme beim Kopieren.** Beim Kopieren eines Fertigungsauftrags (Standardbericht *Fertigungsauftrag
kopieren*) werden **Zeichnungsreferenzart**, **Zeichnungsreferenznr.** und **Zeichnungsreferenz
Versionsnr.** von Kopf und Zeilen auf den neuen Auftrag übernommen; hat der Ausgangsauftrag keine
Referenz, wird nichts kopiert.

## 7. Verwendung nachverfolgen

Zu jeder Zeichnung (und Zeichnungsmappe) protokolliert das System, in welchen Stamm- und Belegdaten
sie verwendet wird. Die Infobox **Zeichnung - Informationen** (bzw. **Zeichnungsmappe - Informationen**)
zeigt gruppierte Zähler:

- **Verwendung in Stammdaten:** Anzahl **Artikel**, **Artikelvarianten**, Fert.-Stücklistenzeilen und
  Montagestücklistenzeilen, die diese Zeichnung führen.
- **Verwendung in Belegen:** getrennt nach **Verkauf**, **Einkauf**, **Produktion**, **Montage**,
  **Service**, **Projekt** und **Buch.-Blatt** – jeweils die Anzahl offener, archivierter und
  gebuchter Zeilen bzw. Belege sowie Artikelposten, in denen die Zeichnung referenziert ist.

Jeder Zähler bezieht sich auf die jeweilige Zeichnungsversion und aktualisiert sich automatisch, wenn
Belege mit dem zugeordneten Artikel entstehen oder gebucht werden. So erkennen Sie vor einer Revision
oder Löschung sofort, wo eine Zeichnung überall im Einsatz ist. Eine separate Historienliste führt das
Modul nicht; die Nachverfolgung erfolgt über diese Zähler und die Drill-down-Navigation in die
gezählten Datensätze.

## 8. FAQ und Troubleshooting

### 1. Warum lässt sich keine neue Zeichnung anlegen?
Weil in der **Zeichnungsverwaltung Einrichtung** das Feld **Interne Zeichnungsnummern** noch leer ist.
Beim Anlegen zieht das System die **Interne Nr.** aus dieser Serie und prüft sie per Pflichtfeld.
Hinterlegen Sie zuerst die Nummernserie (§3.1).

### 2. Warum erscheint meine Zeichnung nicht im Beleg, obwohl sie dem Artikel zugeordnet ist?
Weil keine Version der Zeichnung **Aktiv** gesetzt ist. In Belege wandert ausschließlich die aktive
Version. Setzen Sie im Unterbereich **Versionen** den Haken **Aktiv** (§4.1).

### 3. Was passiert, wenn ich eine andere Version aktiv setze?
Die bisher aktive Version wird automatisch deaktiviert und die **Aktive interne Versionsnr.** auf die
neue Version umgestellt. Bereits gebuchte Belege behalten ihre ursprünglich referenzierte Version, da
diese unveränderlich in der Zeile gespeichert ist.

### 4. Worin unterscheiden sich „Neue Version erstellen" und „In neue Version kopieren"?
**Neue Version erstellen** legt eine leere Folgeversion an. **In neue Version kopieren** übernimmt
zusätzlich **Revisionsnr.**, **Zeichnungs-URL** und die Bemerkungen der aktuellen Version. Für eine
Revision auf Basis des bisherigen Stands nutzen Sie das Kopieren (§4.1).

### 5. Warum ist die neu kopierte Version nicht sofort gültig?
Weil eine kopierte Version bewusst **nicht** automatisch **Aktiv** gesetzt wird. Prüfen Sie den neuen
Stand und setzen Sie den Haken **Aktiv** erst danach.

### 6. Warum lässt sich meine Zeichnung nicht löschen?
Weil sie noch in mindestens einer **Zeichnungsmappe** enthalten ist. Das System weist das Löschen mit
einer Meldung ab. Entfernen Sie die Zeichnung zuerst aus allen Mappen.

### 7. Ich habe die Zeichnungsreferenzart auf der Artikelkarte geändert – warum ist die Nummer weg?
Beim Wechsel der **Zeichnungsreferenzart** wird die **Zeichnungsreferenznr.** automatisch geleert,
damit keine Nummer aus dem falschen Bereich (Zeichnung vs. Zeichnungsmappe) stehen bleibt. Wählen Sie
die passende Nummer neu aus (§5).

### 8. Variante und Artikel haben unterschiedliche Zeichnungen – welche gilt?
Die eigene Referenz der **Artikelvariante** hat Vorrang. Nur wenn die Variante keine eigene Referenz
besitzt, gilt die Referenz des **Artikels** (§5).

### 9. Wie hinterlege und öffne ich die eigentliche Zeichnungsdatei?
Über die Infobox **Zeichnung - Dokumente** legen Sie Dateien zur Version ab; mit **Datei
herunterladen** rufen Sie sie wieder ab. Alternativ kann in der Version eine **Zeichnungs-URL** auf
den Ablageort verweisen.

### 10. Wie sehe ich, wo eine Zeichnung überall verwendet wird, bevor ich sie ändere?
In der Infobox **Zeichnung - Informationen** unter **Verwendung in Stammdaten:** und **Verwendung in
Belegen:**. Die Zähler zeigen pro Bereich die Anzahl der Verwendungen und lassen sich zur Detailliste
aufklappen (§7).

## 9. Typische Anwendungsfälle

### 9.1 Neue Zeichnung anlegen und einem Artikel zuweisen
**Auslöser:** Die Konstruktion liefert eine neue Fertigungszeichnung für einen Artikel per E-Mail.
**Einstieg in BC:** Öffnen Sie über **Suchen** die Liste **Zeichnungen** und legen Sie mit *Neu* eine
Zeichnung an. **Kernablauf:** Tragen Sie **Zeichnungsnr.**, **Beschreibung** und **Zeichnungsartencode**
ein. Wählen Sie im Unterbereich **Versionen** die Aktion **Neue Version erstellen**, erfassen Sie
**Revisionsnr.** und die Datei (Ablage über **Zeichnung - Dokumente** oder **Zeichnungs-URL**) und
setzen Sie **Aktiv**. Wählen Sie danach **Artikel zuweisen**, markieren Sie in der **Artikelzuweisung**
den betreffenden Artikel über **Zugewiesen**. **Abschluss:** Ab sofort erscheint die Zeichnung an allen
Belegzeilen dieses Artikels; die Verwendungszähler in **Zeichnung - Informationen** steigen entsprechend.

### 9.2 Zeichnungsmappe für eine Baugruppe zusammenstellen
**Auslöser:** Für eine Baugruppe sollen mehrere zusammengehörige Zeichnungen gemeinsam geführt und
einem Baugruppenartikel zugeordnet werden. **Einstieg in BC:** Öffnen Sie über **Suchen** die Liste
**Zeichnungsmappen** und legen Sie eine Mappe an. **Kernablauf:** Erzeugen Sie im Unterbereich
**Versionen** mit **Neue Version erstellen** eine Version. Fügen Sie im Unterbereich **Zeichnungen**
über **Vorhandene Zeichnung hinzufügen** bestehende Zeichnungen hinzu oder erstellen Sie mit **Neue
Zeichnung erstellen** direkt neue. Setzen Sie die Mappenversion **Aktiv** und weisen Sie die Mappe über
**Artikel zuweisen** dem Baugruppenartikel zu (Referenzart **Zeichnungsmappe**). **Abschluss:** In
Belegen des Baugruppenartikels wird die Mappe referenziert; die eingebundenen Zeichnungen sind über die
Infoboxen der Mappe einsehbar.

### 9.3 Revision einer Zeichnung im laufenden Betrieb
**Auslöser:** Für eine im Einsatz befindliche Zeichnung erscheint eine neue Revision; die alte muss für
bereits gebuchte Vorgänge erhalten bleiben. **Einstieg in BC:** Öffnen Sie die betroffene **Zeichnung**
aus der Liste **Zeichnungen**. **Kernablauf:** Wählen Sie im Unterbereich **Versionen** die Aktion
**In neue Version kopieren**, passen Sie in der neuen Version die **Revisionsnr.** und die Datei/
**Zeichnungs-URL** an und setzen Sie erst nach Prüfung **Aktiv**. Die bisher aktive Version wird dabei
automatisch deaktiviert. **Abschluss:** Neue Belege referenzieren die neue Version; bereits gebuchte
Belege behalten unverändert ihre ursprünglich referenzierte **Zeichnungsreferenz Versionsnr.**. Prüfen
Sie vorab über **Verwendung in Belegen:**, welche offenen Vorgänge betroffen sind.
