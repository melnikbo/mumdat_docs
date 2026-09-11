---
title: Anwenderhandbuch m+m Sales Purchase History
---

# Anwenderhandbuch m+m Sales Purchase History

## Einleitung

Die Erweiterung **m+m Sales Purchase History** stellt Anwenderinnen und Anwendern in
**Microsoft Dynamics 365 Business Central** eine verdichtete Übersicht über alle Einkaufs- und
Verkaufsbelege bis auf **Belegzeilenebene** bereit. Sie beantwortet die tägliche Frage „Was
haben wir mit diesem Debitor bzw. Kreditor – und mit diesem Artikel – in der Vergangenheit
bewegt?“, ohne dass Sie jede Belegart einzeln aufrufen müssen.

Die Erweiterung sammelt offene, archivierte und gebuchte Belegzeilen (ausschließlich Zeilen der
Art **Artikel**) für einen Debitor bzw. Kreditor, wahlweise eingegrenzt auf einen Artikel und
eine Variante sowie auf eine Suchperiode, und gruppiert sie nach Belegarten. Das Ergebnis wird
in zwei eigenen Übersichtsseiten – **Verkaufshistorie** und **Einkaufshistorie** – als
temporäre, schreibgeschützte Liste angezeigt.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender** im Vertriebs- und Einkaufsalltag
– Innendienst, Auftragserfassung, Einkaufssachbearbeitung –, die während der Belegbearbeitung
schnell auf die Belegzeilenhistorie eines Geschäftspartners oder Artikels zugreifen möchten.
Sekundäre Zielgruppe sind Administratorinnen und Administratoren, die einmalig die Seite
**Historie Einrichtung** konfigurieren.

**Kurzer Prozessüberblick.**

1. Ein Administrator legt in **Historie Einrichtung** je Bereich (Verkauf/Einkauf) die
   Standard-Suchperiode und die standardmäßig vorausgewählten Belegarten fest.
2. Der Anwender öffnet **Verkaufshistorie** bzw. **Einkaufshistorie** – entweder direkt über die
   Suche oder aus einem Verkaufs-/Einkaufsbeleg heraus.
3. Der Anwender setzt Filter (Debitor/Kreditor, Artikel, Variante, Suchperiode), führt
   **Historie aufbereiten** aus und analysiert die Zeilen; über **Beleg anzeigen** springt er in
   den Originalbeleg.

Diese Erweiterung schreibt **keine** Buchungen und verändert **keine** Belege. Sie ist eine
reine Auswertungs- und Navigationshilfe.

## Schnellstart für Anwender

Der schnellste Weg zu einem Ergebnis. Die Einrichtung ist Voraussetzung und steht daher zuerst.

1. **Einmalig einrichten (Administrator):** Öffnen Sie über **Suchen** die Seite
   **Historie Einrichtung** und hinterlegen Sie im Register **Verkauf** und im Register
   **Einkauf** je eine Datumsformel (Feld **Verkaufshistorienperiode (Datumsformel)** bzw.
   **Einkaufshistorienperiode (Datumsformel)**) sowie die standardmäßig anzuzeigenden Bereiche.
2. **Historie öffnen:** Öffnen Sie über **Suchen** die Seite **Verkaufshistorie** (bzw.
   **Einkaufshistorie**). Alternativ öffnen Sie sie direkt aus einem Beleg – siehe Kapitel
   *Historie in Verkaufs- und Einkaufsbelegen*.
3. **Filter setzen:** Erfassen Sie im Bereich **Filter** die **Debitornr.** (bzw. **Kreditornr.**)
   und prüfen Sie die vorbelegte **Suchperiode**. Optional grenzen Sie auf **Artikelnr.** und
   **Variantencode** ein.
4. **Historie aufbereiten:** Wählen Sie die Aktion **Historie aufbereiten** (F9). Die Zeilen
   werden anhand der Filter und der Bereichsauswahl ermittelt und im Zeilenbereich angezeigt.
5. **Eingrenzen und öffnen:** Klicken Sie im **Bereichsfilter** auf eine Belegart, um nur deren
   Zeilen zu sehen; über **Gesamt** kehren Sie zur Gesamtansicht zurück. Markieren Sie eine
   Zeile und wählen Sie **Beleg anzeigen**, um den Originalbeleg zu öffnen.

Hinweis: Ohne mindestens ein Filterkriterium neben der Suchperiode meldet die Seite
**Kein Filter definiert!** und bricht die Aufbereitung ab.

## Einrichtung

Die Einrichtung dieser Erweiterung ist bewusst schlank: Es gibt **eine** unternehmensweite
Einrichtungsseite und **einen** Berechtigungssatz. Es werden **keine** Nummernserien und
**keine** Stammdaten benötigt.

### Historie Einrichtung

**Wer/wann/wofür.** Diese Seite konfiguriert eine Administratorin bzw. ein Administrator
**einmalig vor der ersten Nutzung** je Mandant. Sie ist ein unternehmensweiter Einzelsatz und
steuert zwei Dinge: die **Standard-Suchperiode** (als Datumsformel) und die **standardmäßig
vorausgewählten Belegarten** (Bereiche), die beim Öffnen der Verkaufs- bzw. Einkaufshistorie
bereits aktiviert sind. Beide Einstellungen konsumiert der Anwender später in den
Historienseiten (siehe *Verkaufshistorie und Einkaufshistorie*).

**Einstieg:** Öffnen Sie über **Suchen** den Eintrag **Historie Einrichtung** und klicken Sie
auf den gleichlautenden Link. Beim ersten Öffnen wird der Einrichtungssatz automatisch angelegt.
Die Seite gliedert sich in die beiden Register **Verkauf** und **Einkauf**, jeweils mit der
Gruppe **Datum** und der Gruppe **Bereiche**.

**Register Verkauf**

| Einrichtung | Erläuterung |
|---|---|
| **Verkaufshistorienperiode (Datumsformel)** | Legt den Betrachtungshorizont für die Verkaufshistorie fest. Wenn Sie z. B. `-1J` hinterlegen, dann wird beim Öffnen der Verkaufshistorie die **Suchperiode** automatisch auf „vor einem Jahr bis heute“ vorbelegt und die Belegzeilen werden auf dieses Zeitfenster gefiltert. Ohne Datumsformel meldet die Verkaufshistorie beim Öffnen einen Fehler zum Feld Verkaufshistorienperiode. |
| **Angebote** | Wenn aktiviert, dann ist der Bereich **Angebote** beim Öffnen der Verkaufshistorie vorausgewählt und offene Verkaufsangebotszeilen werden mit aufbereitet; ohne Kennzeichen bleibt dieser Bereich zunächst ausgeblendet und kann bei Bedarf über die Bereichsauswahl zugeschaltet werden. |
| **Archivierte Angebote** | Wenn aktiviert, dann werden zusätzlich archivierte Verkaufsangebotszeilen in die Aufbereitung einbezogen; so sehen Sie auch bereits gelöschte/archivierte Angebotsstände. |
| **Aufträge** | Wenn aktiviert, dann werden offene Verkaufsauftragszeilen standardmäßig mit aufbereitet – der häufigste Anwendungsfall für laufende Kundenvorgänge. |
| **Archivierte Aufträge** | Wenn aktiviert, dann werden archivierte Auftragsstände (frühere Versionen) mit angezeigt. |
| **Rahmenaufträge** | Wenn aktiviert, dann werden Verkaufsrahmenauftragszeilen mit einbezogen, z. B. um Abrufmengen gegen Rahmenvereinbarungen zu prüfen. |
| **Archivierte Rahmenaufträge** | Wenn aktiviert, dann werden archivierte Verkaufsrahmenaufträge zusätzlich berücksichtigt. |
| **Lieferungen** | Wenn aktiviert, dann werden gebuchte Verkaufslieferungszeilen mit aufbereitet – relevant für Liefernachweise und Mengenabgleiche. |
| **Rechnungen** | Wenn aktiviert, dann werden gebuchte Verkaufsrechnungszeilen mit angezeigt – die Grundlage für Umsatz- und Konditionsauskünfte. |
| **Gutschriften** | Wenn aktiviert, dann werden gebuchte Verkaufsgutschriftszeilen mit einbezogen, z. B. für Reklamations- und Retourenauswertungen. |
| **Reklamationen** | Wenn aktiviert, dann werden offene Verkaufsreklamationszeilen mit aufbereitet. |
| **Archivierte Reklamationen** | Wenn aktiviert, dann werden archivierte Verkaufsreklamationen zusätzlich berücksichtigt. |

**Register Einkauf**

| Einrichtung | Erläuterung |
|---|---|
| **Einkaufshistorienperiode (Datumsformel)** | Legt den Betrachtungshorizont für die Einkaufshistorie fest. Wenn Sie z. B. `-1J` hinterlegen, dann wird beim Öffnen der Einkaufshistorie die **Suchperiode** entsprechend vorbelegt und die Belegzeilen auf dieses Zeitfenster gefiltert. Ohne Datumsformel meldet die Einkaufshistorie beim Öffnen einen Fehler zum Feld Einkaufshistorienperiode. |
| **Anfragen** | Wenn aktiviert, dann ist der Bereich **Anfragen** beim Öffnen der Einkaufshistorie vorausgewählt und offene Einkaufsanfragezeilen werden mit aufbereitet. |
| **Archivierte Anfragen** | Wenn aktiviert, dann werden zusätzlich archivierte Einkaufsanfragezeilen einbezogen. |
| **Bestellungen** | Wenn aktiviert, dann werden offene Einkaufsbestellzeilen standardmäßig aufbereitet – der häufigste Anwendungsfall im Einkauf. |
| **Archivierte Bestellungen** | Wenn aktiviert, dann werden archivierte Bestellstände mit angezeigt. |
| **Rahmenbestellungen** | Wenn aktiviert, dann werden Einkaufsrahmenbestellzeilen mit einbezogen, z. B. zum Abgleich von Abrufen gegen Rahmenvereinbarungen. |
| **Archivierte Rahmenbestellungen** | Wenn aktiviert, dann werden archivierte Einkaufsrahmenbestellungen berücksichtigt. |
| **Lieferungen** | Wenn aktiviert, dann werden gebuchte Einkaufslieferungszeilen (Wareneingänge) mit aufbereitet – relevant für Eingangsnachweise. |
| **Rechnungen** | Wenn aktiviert, dann werden gebuchte Einkaufsrechnungszeilen angezeigt – Grundlage für Preis- und Konditionsauskünfte. |
| **Gutschriften** | Wenn aktiviert, dann werden gebuchte Einkaufsgutschriftszeilen einbezogen. |
| **Reklamationen** | Wenn aktiviert, dann werden offene Einkaufsreklamationszeilen aufbereitet. |
| **Archivierte Reklamationen** | Wenn aktiviert, dann werden archivierte Einkaufsreklamationen berücksichtigt. |

**Ablauf der Einrichtung.**

1. **Zuerst** hinterlegen Sie im Register **Verkauf** die **Verkaufshistorienperiode
   (Datumsformel)** und im Register **Einkauf** die **Einkaufshistorienperiode (Datumsformel)** –
   ohne Datumsformel lässt sich die jeweilige Historienseite nicht sinnvoll öffnen.
2. **Danach** aktivieren Sie in beiden Registern unter **Bereiche** die Belegarten, die für Ihre
   Anwender in der Regel sofort sichtbar sein sollen. Diese Vorauswahl ist eine
   Standardeinstellung und kann in der Historienseite jederzeit über die **Bereichsauswahl**
   angepasst werden.
3. **Schließlich** verweisen Sie Ihre Anwender auf die Historienseiten bzw. auf die Belegaktion
   (siehe *Historie in Verkaufs- und Einkaufsbelegen*).

Hinweis: Die Bereichs-Kennzeichen der Einrichtung sind reine **Voreinstellungen**. Der Anwender
kann sie pro Sitzung in der Historienseite abweichend setzen; die Einrichtung bestimmt lediglich
den Ausgangszustand.

### Berechtigungen

Mit dieser Erweiterung wird der Berechtigungssatz **All permissions** (Objekt „MuM SPH
Permission“) ausgeliefert. Er legt fest, welche Aktionen ein Anwender auf den Tabellen, Seiten,
Codeunits und Abfragen dieser Erweiterung ausführen darf, und gewährt Lese-/Schreibzugriff auf
die Einrichtungstabelle sowie Ausführungsrechte für die Historienseiten. Weisen Sie diesen
Berechtigungssatz den Anwenderinnen und Anwendern zu, die mit der Verkaufs- bzw.
Einkaufshistorie arbeiten sollen. Da die beiden Historienzeilentabellen **temporär** je Sitzung
aufgebaut werden, entstehen keine dauerhaften Datenbestände, die gesondert zu berechtigen wären.

## Verkaufshistorie und Einkaufshistorie

Die beiden Historienseiten sind funktional gleich aufgebaut; sie unterscheiden sich nur im
Geschäftspartner (**Debitor** in der Verkaufshistorie, **Kreditor** in der Einkaufshistorie) und
in einzelnen Preis-/Mengenspalten. Beide sind **schreibgeschützte** Arbeitsblattseiten: Sie
können hier keine Belege ändern, sondern ausschließlich auswerten und in den Originalbeleg
springen.

Jede Historienseite gliedert sich in **vier Bereiche**: **Filter**, **Zeilenbereich**,
**Bereichsfilter** und **Bereichsauswahl**. Der Betrachtungshorizont (Suchperiode) und die
vorausgewählten Belegarten stammen aus der Seite **Historie Einrichtung** (siehe *Einrichtung*).

### Filter

Im Bereich **Filter** grenzen Sie ein, welche Belegzeilen aufbereitet werden. Neben der
Suchperiode muss **mindestens ein weiteres** Kriterium gesetzt sein, sonst meldet die Seite
**Kein Filter definiert!**.

**Verkaufshistorie – Filter**

| Filterfeld | Erläuterung |
|---|---|
| **Debitornr.** | Wenn gesetzt, dann werden nur Zeilen des angegebenen Debitors aufbereitet. Dies ist das zentrale Filterkriterium der Verkaufshistorie. |
| **Artikelnr.** | Wenn gesetzt, dann werden die Zeilen zusätzlich auf diesen Artikel eingeschränkt; die Suche schaltet dabei vom Debitor- auf den Artikelbezug um, sodass Sie auch ohne Debitornr. artikelbezogen auswerten können. Beim Setzen einer Artikelnr. wird ein zuvor gesetzter Variantencode zurückgesetzt. |
| **Variantencode** | Wenn gesetzt, dann werden die Zeilen zusätzlich auf diese Artikelvariante gefiltert. Über die Auswahl öffnet sich die Seite **Artikelvarianten**, gefiltert auf die zuvor erfasste Artikelnr. |
| **Suchperiode** | Wenn gesetzt, dann werden nur Belegzeilen im angegebenen Datumsbereich aufbereitet. Der Wert wird beim Öffnen aus der **Verkaufshistorienperiode (Datumsformel)** der Einrichtung vorbelegt und kann überschrieben werden. |

**Einkaufshistorie – Filter**

| Filterfeld | Erläuterung |
|---|---|
| **Kreditornr.** | Wenn gesetzt, dann werden nur Zeilen des angegebenen Kreditors aufbereitet. Dies ist das zentrale Filterkriterium der Einkaufshistorie. |
| **Artikelnr.** | Wenn gesetzt, dann werden die Zeilen zusätzlich auf diesen Artikel eingeschränkt; die Suche schaltet dabei auf den Artikelbezug um. Beim Setzen einer Artikelnr. wird ein zuvor gesetzter Variantencode zurückgesetzt. |
| **Variantencode** | Wenn gesetzt, dann werden die Zeilen zusätzlich auf diese Artikelvariante gefiltert. Über die Auswahl öffnet sich die Seite **Artikelvarianten**, gefiltert auf die zuvor erfasste Artikelnr. |
| **Suchperiode** | Wenn gesetzt, dann werden nur Belegzeilen im angegebenen Datumsbereich aufbereitet. Der Wert wird beim Öffnen aus der **Einkaufshistorienperiode (Datumsformel)** der Einrichtung vorbelegt und kann überschrieben werden. |

### Zeilenbereich

Im **Zeilenbereich** werden alle Belegzeilen angezeigt, die zu den Filterkriterien und der
aktuellen Bereichsauswahl passen. Die Zeilen sind nicht editierbar. Die folgende Tabelle
beschreibt die standardmäßig eingeblendeten Spalten; weitere Spalten sind vorhanden, aber
zunächst ausgeblendet (siehe *Weitere, standardmäßig ausgeblendete Spalten*).

**Verkaufshistorie – Zeilenspalten (Standardanzeige)**

| Feld | Erläuterung |
|---|---|
| **Belegart** | Herkunft der Zeile. Werte: **(leer)** (Summenzeilen bzw. gebuchte Belege ohne Belegstatus), **Angebot**, **Archivangebot**, **Auftrag**, **Archivauftrag**, **Rahmenauftrag**, **Archivrahmenauftrag**, **Lieferung**, **Rechnung**, **Gutschrift**, **Reklamation**, **Archivreklamation**. Anhand dieses Werts erfolgt beim **Beleg anzeigen** der Sprung in den passenden Beleg. |
| **Belegnr.** | Nummer des Ursprungsbelegs, aus dem die Zeile stammt. |
| **Belegzeilennr.** | Zeilennummer innerhalb des Ursprungsbelegs. |
| **Verk. an Name** | Name des Debitors laut Belegkopf. |
| **Verk. an Ort** | Ort des Debitors laut Belegkopf. |
| **Verk. an Länder-/Regionscode** | Länder-/Regionscode des Debitors laut Belegkopf. |
| **Belegdatum** | Belegdatum des Ursprungsbelegs; wird u. a. durch die Suchperiode gefiltert. |
| **Auftragsdatum** | Auftragsdatum des Ursprungsbelegs (bei Gutschriften leer). |
| **Status** | Belegstatus der Zeile. Werte: **(leer)** – gebuchte Belege (Lieferung, Rechnung, Gutschrift) tragen keinen Belegstatus; **Offen** – Beleg in Bearbeitung, noch nicht freigegeben; **Freigegeben** – Beleg freigegeben; **Genehmigung ausstehend** – Beleg im Genehmigungsworkflow; **Vorauszahlung ausstehend** – Beleg wartet auf Vorauszahlung. |
| **Artikelnr.** | Artikel der Belegzeile (nur Zeilen der Art Artikel werden aufbereitet). |
| **Variantencode** | Artikelvariante der Belegzeile. |
| **Referenznr.** | Referenznummer (Artikelreferenz) der Belegzeile. |
| **Beschreibung** | Beschreibung der Belegzeile. |
| **Beschreibung 2** | Zusatzbeschreibung der Belegzeile. |
| **Lagerortcode** | Lagerort der Belegzeile. |
| **Lagerplatzcode** | Lagerplatz der Belegzeile. |
| **Einheitencode** | Mengeneinheit der Belegzeile. |
| **Menge** | Belegmenge der Zeile. |
| **Menge geliefert** | Bereits gelieferte Menge (bei offenen/archivierten Aufträgen). |
| **Menge fakturiert** | Bereits fakturierte Menge. |
| **VK-Preis** | Verkaufspreis (Einzelpreis) der Belegzeile. |
| **Zeilenrabatt %** | Zeilenrabatt in Prozent. |
| **Zeilenrabattbetrag** | Zeilenrabatt als Betrag. |
| **Zeilenbetrag** | Zeilenbetrag der Belegzeile. |
| **Einkaufscode** | Einkaufscode der Belegzeile (Standard-BC-Feld zur Einkaufssteuerung). |
| **Lieferung an Code** | Code der abweichenden Lieferadresse. |
| **Zu-/Abschläge** | Kennzeichen bzw. Wert für Artikel-Zu-/Abschläge der Belegzeile. |

**Einkaufshistorie – Zeilenspalten (Standardanzeige).** Der Aufbau entspricht der
Verkaufshistorie; abweichend sind der Geschäftspartnerbezug und einzelne Preis-/Mengenspalten:

| Feld | Erläuterung |
|---|---|
| **Belegart** | Wie Verkaufshistorie, jedoch mit einkaufsseitigen Werten: **(leer)**, **Anfrage**, **Archivanfrage**, **Bestellung**, **Archivbestellung**, **Rahmenbestellung**, **Archivrahmenbestellung**, **Lieferung**, **Rechnung**, **Gutschrift**, **Reklamation**, **Archivreklamation**. |
| **Belegnr.** / **Belegzeilennr.** | Nummer und Zeilennummer des Ursprungsbelegs. |
| **Eink. von Name** | Name des Kreditors laut Belegkopf. |
| **Eink. von Ort** | Ort des Kreditors laut Belegkopf. |
| **Eink. von Länder-/Regionscode** | Länder-/Regionscode des Kreditors. |
| **Belegdatum** / **Auftragsdatum** | Beleg- bzw. Auftragsdatum des Ursprungsbelegs. |
| **Status** | Wie Verkaufshistorie: **(leer)**, **Offen**, **Freigegeben**, **Genehmigung ausstehend**, **Vorauszahlung ausstehend**. |
| **Artikelnr.** / **Variantencode** / **Referenznr.** | Artikel, Variante und Referenznummer der Belegzeile. |
| **Beschreibung** / **Beschreibung 2** | Beschreibung und Zusatzbeschreibung der Belegzeile. |
| **Lagerortcode** / **Lagerplatzcode** / **Einheitencode** | Lagerort, Lagerplatz und Mengeneinheit. |
| **Menge** | Belegmenge der Zeile. |
| **Menge geliefert** | Bereits eingegangene (gelieferte) Menge. |
| **Menge fakturiert** | Bereits fakturierte Menge. |
| **EK-Preis** | Einkaufspreis (direkter Einzelpreis) der Belegzeile. |
| **Zeilenrabatt %** / **Zeilenrabattbetrag** / **Zeilenbetrag** | Rabatt und Betrag der Belegzeile. |
| **Einkaufscode** / **Lieferung an Code** / **Zu-/Abschläge** | Einkaufscode, Lieferadresscode und Artikel-Zu-/Abschläge. |

**Weitere, standardmäßig ausgeblendete Spalten.** Beide Historienseiten führen weitere Spalten,
die per Personalisierung eingeblendet werden können. Sie sind zur besseren Übersicht zunächst
verborgen: **Belegversionsnr.** und **Belegnr.-Häufigkeit** (nur bei Archivbelegen gefüllt),
**Verk. an Name 2 / Eink. von Name 2**, **Verk. an Adresse / Adresse 2** bzw. **Eink. von
Adresse / Adresse 2**, **Verk. an PLZ-Code / Eink. von PLZ-Code**, **Buchungsdatum**,
**Menge (Basis)**, **Restauftragsmenge**, **Restauftragsmenge (Basis)**, **Menge geliefert
(Basis)** und **Menge fakturiert (Basis)**. Diese Felder liefern denselben Datenbezug wie die
sichtbaren Spalten, jedoch in Basis-Mengeneinheit bzw. für Adress- und Archivdetails.

### Bereichsfilter

Der **Bereichsfilter** zeigt zu jeder Belegart in Klammern die Anzahl der gefundenen
Belegzeilen an (z. B. **Aufträge (12)**). Er dient als schnelle Ampel und als Sprungziel:

- Klicken Sie auf eine Belegart, dann werden im Zeilenbereich nur noch die Zeilen dieser Belegart
  angezeigt; die aktive Belegart wird hervorgehoben.
- Klicken Sie auf **Gesamt**, dann werden wieder alle aufbereiteten Zeilen angezeigt.

Der Bereichsfilter umfasst dieselben Belegarten wie die Bereichsauswahl: **Angebote**,
**Archivierte Angebote**, **Aufträge**, **Archivierte Aufträge**, **Rahmenaufträge**,
**Archivierte Rahmenaufträge**, **Lieferungen**, **Rechnungen**, **Gutschriften**,
**Reklamationen**, **Archivierte Reklamationen** sowie **Gesamt** (in der Einkaufshistorie
entsprechend **Anfragen**, **Bestellungen**, **Rahmenbestellungen** usw.).

### Bereichsauswahl

Die **Bereichsauswahl** ist zunächst ausgeblendet. Blenden Sie sie über die Aktion
**Bereichsauswahl ein-/ausblenden** ein. Hier setzen Sie pro Sitzung, **welche** Belegarten
überhaupt aufbereitet werden sollen. Die Vorbelegung stammt aus der Seite **Historie
Einrichtung**.

Wichtig: Wenn Sie die Bereichsauswahl ändern, dann müssen Sie anschließend erneut
**Historie aufbereiten** ausführen, damit die Zeilen mit der geänderten Auswahl neu ermittelt
werden.

### Aktionen

| Aktion | Erläuterung |
|---|---|
| **Historie aufbereiten** | Ermittelt anhand der Filterkriterien und der Bereichsauswahl die passenden Belegzeilen und zeigt sie im Zeilenbereich an. Vorherige Ergebnisse werden dabei verworfen und neu aufgebaut. Fehlt neben der Suchperiode jedes weitere Filterkriterium, wird **Kein Filter definiert!** gemeldet. (Tastenkürzel F9.) |
| **Beleg anzeigen** | Öffnet zur markierten Zeile den zugehörigen Originalbeleg. Je nach **Belegart** wird der passende Beleg geöffnet – z. B. **Verkaufsangebot**, **Verkaufsauftrag** oder eine gebuchte Verkaufslieferung/-rechnung/-gutschrift (in der Einkaufshistorie entsprechend **Einkaufsanfrage**, **Einkaufsbestellung** usw.). |
| **Bereichsauswahl ein-/ausblenden** | Blendet den Bereich **Bereichsauswahl** ein oder aus, damit Sie die anzuzeigenden Belegarten anpassen können. |

## Historie in Verkaufs- und Einkaufsbelegen

Anwender müssen die Historie nicht zwingend über die Suche öffnen. In den relevanten
Verkaufs- und Einkaufsbelegen ist die Historie direkt als Aktion hinterlegt und wird mit den
Filterkriterien des aktuellen Belegs vorbelegt. Das erspart die manuelle Eingabe von Debitor-/
Kreditornummer und Artikel.

**Verkaufsbelege.** In den Belegen **Verkaufsangebot** und **Verkaufsauftrag** finden Sie die
Aktion **Verkaufshistorie** an zwei Stellen:

- **Im Belegkopf** (auch als geförderte Aktion im Menüband): Öffnen Sie über die Aktion
  **Verkaufshistorie** die Seite **Verkaufshistorie**. Es wird die **Debitornr.** des Belegs als
  Filter übergeben; die Historie wird sofort aufbereitet.
- **In der Belegzeile** (Aktion auf der Zeilenunterseite): Markieren Sie eine Artikelzeile und
  wählen Sie **Verkaufshistorie**. Zusätzlich zur **Debitornr.** werden **Artikelnr.** und
  **Variantencode** der Zeile übergeben. Die Zeilenaktion setzt voraus, dass die Zeile vom Typ
  **Artikel** ist.

**Einkaufsbelege.** In den Belegen **Einkaufsanfrage** und **Einkaufsbestellung** finden Sie
analog die Aktion **Einkaufshistorie**:

- **Im Belegkopf** (auch geförderte Aktion): Öffnet die **Einkaufshistorie** mit der
  **Kreditornr.** des Belegs.
- **In der Belegzeile**: Öffnet die **Einkaufshistorie** mit **Kreditornr.**, **Artikelnr.** und
  **Variantencode** der markierten Artikelzeile; auch hier muss die Zeile vom Typ **Artikel**
  sein.

In beiden Fällen öffnet sich die Historienseite mit den vorbelegten Filtern. Sie können dort
weitere Filter anwenden, die **Bereichsauswahl** ändern und über **Historie aufbereiten** neu
laden sowie über **Beleg anzeigen** in andere Belege springen.

## FAQ und Troubleshooting

### Warum erscheint beim Aufbereiten die Meldung „Kein Filter definiert!“?
Weil neben der **Suchperiode** kein weiteres Filterkriterium gesetzt ist. Erfassen Sie
mindestens die **Debitornr.** (bzw. **Kreditornr.**) oder eine **Artikelnr.** und führen Sie
**Historie aufbereiten** erneut aus.

### Warum kann ich in der Historie keine Zeilen ändern?
Beide Historienseiten sind bewusst schreibgeschützt und arbeiten auf einer temporären
Ergebnisliste. Sie dienen ausschließlich der Auswertung und Navigation. Änderungen nehmen Sie
im Originalbeleg vor, den Sie über **Beleg anzeigen** öffnen.

### Warum fehlen manche Belegzeilen, die ich erwarte?
Prüfen Sie drei Dinge: Ist die passende **Belegart** in der **Bereichsauswahl** aktiviert? Liegt
das **Belegdatum** innerhalb der **Suchperiode**? Und handelt es sich um eine **Artikelzeile**?
Es werden ausschließlich Zeilen der Art **Artikel** aufbereitet – Sach-, Ressourcen- oder
Textzeilen erscheinen nicht.

### Warum sehe ich nach dem Ändern der Bereichsauswahl keine neuen Zeilen?
Die Bereichsauswahl wirkt erst nach erneutem Aufbereiten. Führen Sie nach jeder Änderung der
Bereichsauswahl die Aktion **Historie aufbereiten** noch einmal aus.

### Wie grenze ich auf einen bestimmten Artikel oder eine Variante ein?
Erfassen Sie im Filterbereich die **Artikelnr.**; die Suche schaltet dann auf den Artikelbezug
um. Für eine Variante setzen Sie zusätzlich den **Variantencode** – die Auswahl öffnet die Seite
**Artikelvarianten**, bereits gefiltert auf die Artikelnr. Achtung: Beim Erfassen einer neuen
**Artikelnr.** wird ein zuvor gesetzter **Variantencode** automatisch zurückgesetzt.

### Woher kommt die vorbelegte Suchperiode?
Aus der Seite **Historie Einrichtung**: Die dort hinterlegte **Verkaufshistorienperiode
(Datumsformel)** bzw. **Einkaufshistorienperiode (Datumsformel)** wird beim Öffnen der Historie
in eine konkrete Suchperiode „berechnet ab heute“ umgesetzt. Sie können den Wert danach
überschreiben.

### Was bedeutet die Zahl in Klammern im Bereichsfilter?
Sie zeigt die Anzahl der aufbereiteten Belegzeilen je Belegart an, z. B. **Rechnungen (8)**. Ein
Klick auf die Belegart filtert den Zeilenbereich auf genau diese Belegart; **Gesamt** hebt den
Filter wieder auf.

### Warum steht bei gebuchten Belegen im Feld „Status“ nichts?
Gebuchte Belege – **Lieferung**, **Rechnung** und **Gutschrift** – tragen keinen Belegstatus; ihr
**Status** bleibt daher **(leer)**. Ein Status wie **Offen** oder **Freigegeben** erscheint nur
bei offenen und archivierten Belegen (Angebot, Auftrag, Rahmenauftrag, Reklamation).

### Warum öffnet „Historie öffnen“ aus dem Beleg direkt eine gefüllte Liste?
Weil die Belegaktion die Filter des aktuellen Belegs übergibt (Debitor-/Kreditornr., aus der
Zeile zusätzlich Artikel und Variante) und die Historie sofort aufbereitet. So sehen Sie ohne
Zwischenschritt die passenden Vorgänge.

### Muss ich zum Öffnen der Historie besondere Rechte haben?
Ja. Weisen Sie den betreffenden Anwendern den mitgelieferten Berechtigungssatz der Erweiterung
zu (Objekt „MuM SPH Permission“). Er gewährt die nötigen Ausführungsrechte für die
Historienseiten und den Zugriff auf die Einrichtung.

## Typische Anwendungsfälle (Nutzungsbeispiele)

### Kundenrückfrage zu früheren Lieferungen und Rechnungen

**Auslöser.** Ein Debitor ruft an und fragt, welche Mengen eines Artikels er im letzten Jahr
erhalten und was er dafür berechnet bekommen hat.

**Einstieg in BC.** Öffnen Sie über **Suchen** die Seite **Verkaufshistorie**. (Alternativ,
falls Sie bereits einen Beleg dieses Debitors offen haben, über die Belegaktion
**Verkaufshistorie**.)

**Kernablauf.**
1. Erfassen Sie im Bereich **Filter** die **Debitornr.** des Anrufers.
2. Prüfen Sie die vorbelegte **Suchperiode** (z. B. das letzte Jahr) und passen Sie sie bei
   Bedarf an; optional setzen Sie die **Artikelnr.**.
3. Stellen Sie in der **Bereichsauswahl** sicher, dass **Lieferungen** und **Rechnungen**
   aktiviert sind, und führen Sie **Historie aufbereiten** aus.
4. Klicken Sie im **Bereichsfilter** auf **Lieferungen**, um nur die Liefermengen zu sehen,
   danach auf **Rechnungen** für die fakturierten Beträge.
5. Markieren Sie eine Zeile und wählen Sie **Beleg anzeigen**, um dem Kunden Details aus der
   gebuchten Verkaufslieferung bzw. -rechnung zu nennen.

**Abschluss.** Es entsteht keine Buchung; die Auskunft basiert vollständig auf den vorhandenen
Belegen. Über **Beleg anzeigen** können Sie den Originalbeleg bei Bedarf drucken oder versenden
(Standardfunktionen des jeweiligen Belegs).

### Preis- und Konditionsprüfung beim Erfassen einer Bestellung

**Auslöser.** Eine Einkaufssachbearbeiterin erfasst eine neue **Einkaufsbestellung** und möchte
prüfen, zu welchem Preis derselbe Artikel zuletzt bei diesem Kreditor beschafft wurde.

**Einstieg in BC.** Markieren Sie in der Einkaufsbestellung die Artikelzeile und wählen Sie in
der Zeile die Aktion **Einkaufshistorie**. Die Seite **Einkaufshistorie** öffnet sich mit
vorbelegter **Kreditornr.**, **Artikelnr.** und ggf. **Variantencode**.

**Kernablauf.**
1. Die Historie ist bereits aufbereitet; prüfen Sie die **Suchperiode** und erweitern Sie sie bei
   Bedarf.
2. Klicken Sie im **Bereichsfilter** auf **Rechnungen**, um die zuletzt fakturierten **EK-Preise**
   zu sehen; über **Bestellungen** erkennen Sie noch offene Beschaffungen.
3. Vergleichen Sie **EK-Preis**, **Zeilenrabatt %** und **Zeilenbetrag** der historischen Zeilen
   mit Ihrer aktuellen Bestellung.
4. Bei Rückfragen öffnen Sie über **Beleg anzeigen** die frühere **Einkaufsbestellung** bzw. die
   gebuchte Einkaufsrechnung.

**Abschluss.** Mit der so gewonnenen Preisinformation erfassen Sie die Bestellzeile fertig. Auch
hier verändert die Historie selbst nichts am Beleg.
