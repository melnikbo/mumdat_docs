---
title: Anwenderhandbuch m+m Unit Conversion
---

# Anwenderhandbuch m+m Unit Conversion

## Einleitung

Die m+m-App **Einheitenumrechnung** (App-Titel: *m+m Unit Conversion*) ergänzt Microsoft Dynamics 365 Business Central um eine parallele Mengendarstellung in den drei Einheiten **KG**, **Meter** und **Stück** – zusätzlich zur Standardmenge (**Menge**). Auf nahezu jedem artikelführenden Beleg, Buchblatt und Posten stehen dadurch neben der gewohnten Menge auch die zugehörigen Werte in KG, Meter und Stück zur Verfügung. Erfasst der Anwender einen Wert in einer der drei Einheiten, berechnet die App die Standardmenge sowie die beiden übrigen Einheiten automatisch anhand hinterlegter Umrechnungsfaktoren.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender**, die täglich Belege und Buchblätter bearbeiten: Einkaufssachbearbeiter, Verkaufssachbearbeiter, Lager- und Produktionsmitarbeiter, die Mengen erfassen, Chargen zuweisen sowie Wareneingänge, Warenausgänge, Verbräuche und Ist-Meldungen buchen. Sekundäre Zielgruppe sind **Administratoren und Stammdatenverantwortliche**, welche die globale **KG Meter Stück Einrichtung** vornehmen und je Artikel die Umrechnungsfaktoren, die **Mengenkonsistenzabfrage** und die Rundung pflegen.

**Kurzer Prozessüberblick.** Der administrative Einstieg erfolgt einmalig über die globale **KG Meter Stück Einrichtung** (welche Einheitencodes für KG, Meter und Stück stehen). Anschließend pflegt der Stammdatenverantwortliche je Artikel auf der **Artikelkarte** die theoretischen Umrechnungsfaktoren, die **Mengenkonsistenzabfrage** und optional die Rundung. Im Tagesgeschäft erfasst der Anwender auf Belegzeilen und Buchblattzeilen Mengen wahlweise in **Menge**, **KG**, **Meter** oder **Stück**; die übrigen Werte werden automatisch berechnet. Verfügt ein Artikel über eine aktive **Artikelverfolgung** (Chargen oder Seriennummern), kann der Anwender bewusst von den theoretischen Faktoren abweichen – dies wird als **Inkonsistenz** bezeichnet und über alle Folgebelege und Posten mitgeführt.

## Schnellstart für Anwender

Die folgende Reihenfolge bildet die Abhängigkeiten aus dem Code ab: zuerst die globale Einrichtung, dann die Stammdaten je Artikel, danach die tägliche Belegarbeit.

1. **Globale Einrichtung (einmalig, Administrator).** Öffnen Sie über **Suchen** die Seite **KG Meter Stück Einrichtung** und tragen Sie die **Einheitencode für KG**, **Einheitencode für Meter** und **Einheitencode für Stück** ein. Ohne diese drei Codes bleibt die gesamte Umrechnung wirkungslos.
2. **Artikel vorbereiten (Stammdatenverantwortliche).** Öffnen Sie aus der Artikelliste die **Artikelkarte** des betreffenden Artikels. Prüfen Sie den **Basiseinheitencode** und tragen Sie im Bereich **Faktoren** die **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** ein. Setzen Sie bei Bedarf die **Mengenkonsistenzabfrage** und die Werte im Bereich **KG:/Meter:/Stück:** (**Rundungspräzision** und **Rundungsregel**).
3. **Artikelverfolgung aktivieren (nur wenn Inkonsistenzen gewünscht).** Soll der Anwender von den theoretischen Faktoren abweichen können, hinterlegen Sie auf der Artikelkarte einen **Artikelverfolgungscode** und wählen Sie in der **Mengenkonsistenzabfrage** *Mengen niemals ändern* oder *Mengenänderung durch Nachfrage*.
4. **Belegzeile erfassen (operativer Anwender).** Legen Sie z. B. einen Verkaufsauftrag oder eine Einkaufsbestellung an. Sobald Sie den Artikel in der Zeile hinterlegen, werden die Felder **KG**, **Meter** und **Stück** automatisch berechnet. Sie können den Wert wahlweise direkt in **KG**, **Meter** oder **Stück** überschreiben – die **Menge** und die übrigen Einheiten rechnen sich neu.
5. **Charge/Serie zuweisen und ggf. Inkonsistenz erzeugen.** Öffnen Sie die Artikelverfolgungszeilen, weisen Sie eine Charge zu und passen Sie bei Bedarf KG, Meter oder Stück an. Je nach **Mengenkonsistenzabfrage** erscheint die Rückfrage **„Möchten Sie alle Mengenfelder neu berechnen?"**.
6. **Beleg buchen (Standard).** Buchen Sie den Beleg wie gewohnt (Wareneingang/Warenausgang, Einkaufs-/Verkaufsrechnung, Ist-Meldung, Verbrauch). Die Werte KG, Meter und Stück – einschließlich etwaiger Inkonsistenzen – werden in die gebuchten Belege sowie in Artikel-, Wert-, Kapazitäts- und Lagerplatzposten übernommen.

## Einrichtung

Die Einrichtung der Einheitenumrechnung gliedert sich in eine **globale** Grundeinrichtung (eine Seite je Mandant) und die **artikelbezogene** Einrichtung auf der Artikelkarte (siehe Kapitel *Stammdaten*). Beide bauen aufeinander auf: Ohne die globale Zuordnung der Einheitencodes greifen die artikelbezogenen Faktoren nicht.

### KG Meter Stück Einrichtung

**Prozessintro.** Diese Seite konfiguriert der **Administrator einmalig je Mandant**, bevor die App erstmals genutzt wird. Sie legt fest, welche in Business Central angelegten **Einheitencodes** von der App als KG, als Meter und als Stück interpretiert werden. Erst wenn alle drei Codes gesetzt sind, führt die App auf Artikeln und Belegen eine Umrechnung durch (im Code prüft `GetAndTestSetup` alle drei Felder; fehlt einer, bricht die Umrechnung stillschweigend ab). Die auf der Artikelkarte gepflegten Faktoren (siehe *Stammdaten*) setzen diese Einrichtung voraus.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **KG Meter Stück Einrichtung** und klicken Sie den gleichlautenden Link an. Die Seite ist ein Einzelsatz (Karte) und wird beim Öffnen automatisch angelegt.

| Einrichtung | Erläuterung |
|---|---|
| **Einheitencode für KG** | Wenn gesetzt, behandelt die App den ausgewählten Einheitencode systemweit als Gewichtseinheit KG. Nur Artikel, deren **Basiseinheitencode** einem der drei hier gepflegten Codes entspricht, werden umgerechnet; ohne diesen Eintrag findet keine KG-Umrechnung statt und die KG-Felder bleiben leer. |
| **Einheitencode für Meter** | Wenn gesetzt, gilt der ausgewählte Einheitencode systemweit als Längeneinheit Meter. Dadurch stehen auf Belegen und Buchblättern die Meter-Felder zur Verfügung und werden aus den theoretischen Faktoren berechnet; fehlt der Eintrag, bleibt die Meter-Spalte ohne Wert. |
| **Einheitencode für Stück** | Wenn gesetzt, gilt der ausgewählte Einheitencode systemweit als Stückeinheit. Erst damit werden die Stück-Felder gefüllt und in Folgebelege übernommen; ohne Eintrag entfällt die Stück-Umrechnung. |

Der Bereich **Einheiten** fasst die drei Zuordnungen zusammen. Das technische Feld **Primärschlüssel** ist ein systeminternes Schlüsselfeld und für den Anwender ohne Bedeutung.

> **Voraussetzung/Abhängigkeit.** Die drei Einheitencodes müssen zuvor in der Standard-Einrichtung der **Einheiten** von Business Central existieren. Solange nicht alle drei Felder gefüllt sind, unterbleibt jede Umrechnung – auch auf bereits vorbereiteten Artikeln. Die eigentliche Aktivierung je Artikel erfolgt anschließend über die theoretischen Faktoren auf der Artikelkarte (siehe *Stammdaten → Artikelkarte*).

### Berechtigungen

Die App liefert den Berechtigungssatz **KG Mtr. Piece** mit. Der Administrator weist diesen Berechtigungssatz den Benutzern oder Benutzergruppen zu; er bestimmt die Berechtigungen für die von der App bereitgestellten Objekte (Einrichtungstabelle, Umrechnungslogik und die zusätzlichen Felder) und legt fest, welche Aktionen die Anwender im Rahmen der Einheitenumrechnung ausführen dürfen. Die Zuweisung erfolgt über die Standardverwaltung der Berechtigungssätze in Business Central.

## Stammdaten

Nach der globalen Einrichtung wird die Umrechnung je Artikel aktiviert und gesteuert. Die Stammdatenpflege entscheidet, **ob** ein Artikel umgerechnet wird (theoretische Faktoren), **wie** mit manuellen Abweichungen umgegangen wird (Mengenkonsistenzabfrage) und **wie genau** gerundet wird (Rundungspräzision/-regel). Ergänzend steuern Charge/Serie die tatsächlichen Faktoren und der Arbeitsplatz die Zeitenberechnung.

### Einheitenumrechnung je Artikel einrichten (Artikelkarte)

**Prozessintro.** Diese Einrichtung nimmt der **Stammdatenverantwortliche** vor, sobald ein Artikel in KG, Meter und Stück geführt werden soll – in der Regel bei Neuanlage oder Umstellung des Artikels. Die hier gepflegten **theoretischen Faktoren** benötigt das System, um die Werte KG, Meter und Stück in allen Prozessen (siehe *Nutzungsbeispiele*) zu berechnen. Ist nur einer der beiden Faktoren gefüllt, ist nur die Umrechnung zwischen diesen beiden Einheiten möglich; die jeweils andere Einheit bleibt leer. Sind beide Faktoren leer, bleiben alle drei Mengenfelder leer.

**Einstieg:** Öffnen Sie aus der **Artikelliste** die **Artikelkarte** des Artikels. Die App ergänzt dort die Bereiche **Faktoren:**, **Mengenkonsistenz:** sowie **KG:**, **Meter:** und **Stück:**.

#### Faktoren und Rundung

| Einrichtung | Erläuterung |
|---|---|
| **Theoretische KG pro Meter** | Wenn gefüllt, dann rechnet die App auf allen Belegen und Buchblättern zwischen KG und Meter um (Meter = KG ÷ Faktor bzw. KG = Meter × Faktor). Zusätzlich legt die App bei aktiver Standardumrechnung automatisch die passende **Artikeleinheit** an. Voraussetzung: Der **Basiseinheitencode** des Artikels ist einer der drei in der globalen Einrichtung hinterlegten Codes, sonst wird die Eingabe mit einer Feldmeldung abgewiesen. Bereits gebuchte Posten verhindern eine Änderung des Faktors. |
| **Theoretische KG pro Stück** | Wenn gefüllt, dann rechnet die App zwischen KG und Stück um. Bei Basiseinheit Stück und leerem Faktor wird auch der Faktor „KG pro Meter" zurückgesetzt und die zugehörige Artikeleinheit entfernt. Gleiche Voraussetzung und Sperre bei gebuchten Posten wie bei „Theoretische KG pro Meter". |
| **Rundungspräzision KG** | Wenn größer als 0, dann wird jede automatisch berechnete KG-Menge auf diese Präzision gerundet (z. B. 0,001). Bei 0 findet keine Rundung statt und die Rundungsregel wird auf **Keine Rundung** gesetzt; ein negativer Wert wird mit einer Feldmeldung abgewiesen. |
| **Rundungsregel KG** | Legt fest, in welche Richtung berechnete KG-Werte gerundet werden. Nur editierbar, wenn eine Rundungspräzision > 0 hinterlegt ist. Werte siehe unten. |
| **Rundungspräzision Meter** | Wenn größer als 0, dann werden berechnete Meter-Werte auf diese Präzision gerundet; bei 0 keine Rundung. |
| **Rundungsregel Meter** | Legt die Rundungsrichtung für berechnete Meter-Werte fest; nur editierbar bei Präzision > 0. Werte siehe unten. |
| **Rundungspräzision Stück** | Wenn größer als 0, dann werden berechnete Stück-Werte auf diese Präzision gerundet; bei 0 keine Rundung. |
| **Rundungsregel Stück** | Legt die Rundungsrichtung für berechnete Stück-Werte fest; nur editierbar bei Präzision > 0. Werte siehe unten. |

**Werte der Rundungsregel (KG, Meter, Stück gleichermaßen):**

- **Keine Rundung:** Der berechnete Wert wird auf die Präzision abgeschnitten, ohne auf- oder abzurunden.
- **Aufrunden:** Der berechnete Wert wird stets auf die nächste Präzisionsstufe aufgerundet.
- **Abrunden:** Der berechnete Wert wird stets auf die nächste Präzisionsstufe abgerundet.
- **Kaufmännisches Runden:** Der berechnete Wert wird kaufmännisch gerundet (ab 5 wird aufgerundet, bis 4 wird abgerundet). Dieser Wert wird automatisch voreingestellt, sobald erstmals eine Präzision > 0 gesetzt wird.

> Wird eine Rundungspräzision auf 0 gesetzt, dann setzt die App die zugehörige Rundungsregel automatisch auf **Keine Rundung**; umgekehrt wird beim Setzen einer Rundungsregel auf **Keine Rundung** die Präzision auf 0 zurückgesetzt.

#### Mengenkonsistenzabfrage und Inkonsistenzen

| Einrichtung | Erläuterung |
|---|---|
| **Mengenkonsistenzabfrage** | Legt fest, wie das System reagiert, wenn ein Anwender in einer Artikelverfolgungszeile einen abweichenden Wert in eines der drei Mengenfelder KG, Meter oder Stück einträgt. Der gewählte Wert entscheidet darüber, ob überhaupt **Inkonsistenzen** (Abweichungen von den theoretischen Faktoren) entstehen dürfen. Werte siehe unten. |

**Werte der Mengenkonsistenzabfrage:**

- **Mengen immer ändern:** Ein manuell geänderter Wert überschreibt stets die über die theoretischen Faktoren berechneten Werte; die übrigen Mengenfelder werden automatisch neu berechnet. Inkonsistenzen sind **nicht** möglich. In diesem Modus übernimmt die Umrechnung die Standardfunktion von Business Central; beim Eintragen der theoretischen Faktoren werden automatisch die entsprechenden **Artikeleinheiten** gebildet.
- **Mengen niemals ändern:** Nicht manuell geänderte Werte werden bei Eingabe in KG, Meter oder Stück **niemals** automatisch neu berechnet. Trägt der Anwender einen manuellen Wert ein, entsteht immer eine Inkonsistenz. In diesem Modus verlangt das System einen gesetzten **Artikelverfolgungscode**; die Umrechnung erfolgt über die App statt über die Standard-Artikeleinheiten. Alle vorhandenen Artikeleinheiten außer der Basiseinheit werden entfernt, und der Versuch, eine neue Artikeleinheit anzulegen, wird mit einer Fehlermeldung abgewiesen.
- **Mengenänderung durch Nachfrage:** Bei manueller Änderung eines Wertes erscheint der Dialog **„Möchten Sie alle Mengenfelder neu berechnen?"**. Bestätigt der Anwender mit *Ja*, werden die übrigen Felder automatisch über die theoretischen Faktoren berechnet; bei *Nein* bleibt der abweichende Wert bestehen und es entsteht eine Inkonsistenz. Auch dieser Modus verlangt einen **Artikelverfolgungscode** und entfernt die Zusatz-Artikeleinheiten wie bei „Mengen niemals ändern".

**Prozessschritte zur Freischaltung von Inkonsistenzen (in Abhängigkeitsreihenfolge):**

1. **Zuerst** globale Einrichtung sicherstellen: Die drei Einheitencodes sind in der **KG Meter Stück Einrichtung** gesetzt.
2. **Danach** auf der Artikelkarte einen **Artikelverfolgungscode** hinterlegen (bei „Mengen niemals ändern" und „Mengenänderung durch Nachfrage" zwingend erforderlich).
3. **Anschließend** die theoretischen Faktoren **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** eintragen.
4. **Schließlich** die **Mengenkonsistenzabfrage** auf *Mengen niemals ändern* oder *Mengenänderung durch Nachfrage* setzen.
5. **Im Tagesgeschäft** kann der Anwender dann in den Artikelverfolgungszeilen eines Belegs KG, Meter oder Stück abweichend erfassen (siehe *Nutzungsbeispiele*).

> **Zusammenhang zur täglichen Arbeit.** Bei aktiver Umrechnung werden auf den Belegzeilen die Felder KG, Meter und Stück automatisch gefüllt; die Mengenkonsistenzabfrage steuert, ob die Zuweisung einer Charge oder eine manuelle Eingabe eine Inkonsistenz erzeugt. Prozesse, die eine **neue** Charge buchen (z. B. Einkaufsbestellung, Ist-Meldung in der Produktion, Zubuchung über das Artikelbuchblatt), erlauben das Anlegen von Inkonsistenzen. Prozesse, die eine **bestehende** Charge nutzen (z. B. Chargenauswahl im Verkaufsauftrag, Verbrauchscharge in der Produktion), rechnen mit den bereits vorhandenen Faktoren und lassen keine Änderung mehr zu.

#### Artikel-Übersichtsspalten (Lagerbestand)

Die App ergänzt die **Artikelkarte** und die **Artikelliste** um schreibgeschützte Kennzahlen in KG, Meter und Stück. Diese spiegeln vorhandene Standard-Mengenfelder von Business Central in den drei Einheiten wider und aktualisieren sich automatisch aus den Posten und offenen Belegen. Sie werden hier als Gruppe dokumentiert, da sie keine pflegbare Einrichtung darstellen:

- **Lagerbestand** in KG, Meter und Stück (Summe der Artikelposten) – auf Artikelkarte und Artikelliste sichtbar.
- **In Auftrag**-Kennzahlen (Beschaffung, Verkauf, Fertigung, Komponenten, Service, Projekt, Montage, Montagekomponente) jeweils in KG, Meter und Stück – informativer Spiegel der jeweiligen Standard-„Menge in …"-Felder.
- **Reservierte** Mengen in KG, Meter und Stück (Lager sowie Einkaufs-/Verkaufsaufträge).

### Zeitenberechnung je Arbeitsplatz einrichten (Arbeitsplatzkarte)

**Prozessintro.** Diese Einstellung pflegt der Stammdatenverantwortliche je **Arbeitsplatz** in der Fertigung. Sie bestimmt, welche der Einheiten für die Zeitenberechnung des Arbeitsplatzes herangezogen wird, und ergänzt damit die Einheitenumrechnung um den Kapazitätsbezug.

**Einstieg:** Öffnen Sie aus der Arbeitsplatzliste die **Arbeitsplatzkarte** und wählen Sie das Feld **Zeitenberechnungseinheit** (im Bereich der Einheitenkosten-Berechnung).

| Einrichtung | Erläuterung |
|---|---|
| **Zeitenberechnungseinheit** | Legt fest, auf welche Einheit sich die Zeitenberechnung dieses Arbeitsplatzes bezieht. Wenn ein bestimmter Wert gewählt ist, wird die Kapazitäts- bzw. Zeitermittlung auf Basis dieser Einheit durchgeführt. Werte siehe unten. |

**Werte der Zeitenberechnungseinheit:**

- **Menge:** Die Zeitenberechnung erfolgt auf Basis der Standardmenge.
- **KG:** Die Zeitenberechnung erfolgt auf Basis der KG-Menge.
- **Meter:** Die Zeitenberechnung erfolgt auf Basis der Meter-Menge.
- **Stück:** Die Zeitenberechnung erfolgt auf Basis der Stück-Menge.

### Tatsächliche Faktoren je Charge/Serie (Chargennr.-/Seriennr.-Informationskarte)

**Prozessintro.** Während die Artikelkarte die **theoretischen** Faktoren vorgibt, kann je einzelner Charge oder Seriennummer ein **tatsächlicher** (gemessener) Faktor hinterlegt werden. Dies pflegt der Lager- oder Qualitätsverantwortliche, wenn eine konkrete Charge vom theoretischen Wert abweicht. Bei der Umrechnung eines Belegs gilt die Vorrangregel: Ist auf der **Seriennr.-Informationskarte** ein tatsächlicher Faktor gepflegt, wird dieser verwendet; sonst der Faktor der **Chargennr.-Informationskarte**; sonst der theoretische Faktor der Artikelkarte (im Code: `GetActualKGPer`).

**Einstieg:** Die Informationskarte öffnen Sie aus den **Artikelverfolgungszeilen** eines Belegs oder aus der Chargen-/Seriennummernübersicht des Artikels, indem Sie die betreffende Charge bzw. Seriennummer auswählen.

| Feld | Erläuterung |
|---|---|
| **Theoretische KG pro Meter** / **Theoretische KG pro Stück** | Übernahme der theoretischen Faktoren aus der Artikelkarte als Ausgangswert für diese Charge/Serie. |
| **Tatsächliche KG pro Meter** | Wenn gefüllt, dann verwendet die App für alle Umrechnungen dieser Charge diesen gemessenen Faktor anstelle des theoretischen Wertes – dadurch bilden die Belege die reale Beschaffenheit der Charge ab. |
| **Tatsächliche KG pro Stück** | Wenn gefüllt, dann gilt dieser gemessene Wert für die Umrechnung zwischen KG und Stück dieser Charge/Serie und hat Vorrang vor dem theoretischen Faktor. |
| **Lagerbestand KG / Meter / Stück** | Schreibgeschützter Lagerbestand der Charge/Serie in den drei Einheiten. |
| **Abgelaufene KG / Meter / Stück am Lager** | Schreibgeschützter Anteil des Bestands, dessen Ablaufdatum überschritten ist, in den drei Einheiten. |

> Die **Seriennr.-Informationskarte** trägt dieselben Felder mit identischer Bedeutung; sie wird hier nicht gesondert aufgeführt. Löschversuche einer Chargen- oder Seriennummern-Informationskarte, zu der bereits Artikelposten bestehen, weist das System mit einer Fehlermeldung ab (z. B. „Sie können die Chargennr.-Informationskarte nicht löschen, da ein oder mehrere Artikelposten vorhanden sind.").

## Inkonsistenzen – das zentrale Konzept

Eine **Inkonsistenz** liegt vor, wenn die Werte KG, Meter und Stück einer Zeile **nicht** dem in der Artikelkarte hinterlegten theoretischen Verhältnis entsprechen. Inkonsistenzen sind gewollt und bilden reale Abweichungen ab (z. B. eine Charge, die pro Meter mehr wiegt als der theoretische Durchschnitt).

- Inkonsistenzen sind **nur** möglich, wenn der Artikel über eine **aktive Artikelverfolgung** (Chargen oder Seriennummern) verfügt und die **Mengenkonsistenzabfrage** auf *Mengen niemals ändern* oder *Mengenänderung durch Nachfrage* steht.
- Bei **Mengen immer ändern** sind Inkonsistenzen ausgeschlossen; die Umrechnung läuft über die Standard-Artikeleinheiten von Business Central.
- Erzeugt werden Inkonsistenzen in Prozessen mit **neuer** Charge (Einkaufsbestellung, Ist-Meldung, Artikelbuchblatt). In Prozessen mit **bestehender** Charge sind die Faktoren fixiert.
- Einmal erfasste Inkonsistenzen werden über die gesamte Belegkette und in die Artikel-, Wert-, Kapazitäts- und Lagerplatzposten mitgeführt.

## Tägliche Arbeit auf Belegen und Buchblättern

Die App fügt die Einheiten KG, Meter und Stück auf allen relevanten Belegen und Buchblättern hinzu – im Einkauf, Verkauf, in der Umlagerung, im Service, in Projekten, in der Montage, in der Produktion sowie in Lager- und Artikelbuchblättern. Das Bedienprinzip ist überall gleich; stellvertretend wird es an der Verkaufszeile beschrieben.

### Mengenerfassung auf der Belegzeile

Sobald in einer Zeile ein Artikel (mit gepflegten Faktoren) hinterlegt wird, füllt die App die zugehörigen Felder **KG**, **Meter** und **Stück**. Der Anwender kann die Menge in jeder der Einheiten erfassen:

| Feld | Erläuterung |
|---|---|
| **KG** | Wenn der Anwender hier einen Wert erfasst, dann berechnet die App aus dem hinterlegten Faktor die **Menge**, die **Meter** und die **Stück** neu und merkt sich, dass zuletzt in KG erfasst wurde. Die Standardmenge der Zeile wird entsprechend validiert. |
| **Meter** | Wenn der Anwender hier einen Wert erfasst, dann werden Menge, KG und Stück aus dem Faktor abgeleitet; die Zeile führt Meter als führende Erfassungseinheit. |
| **Stück** | Wenn der Anwender hier einen Wert erfasst, dann werden Menge, KG und Meter aus dem Faktor abgeleitet; die Zeile führt Stück als führende Erfassungseinheit. |
| **Menge** (Standard) | Wenn der Anwender die Standardmenge ändert, dann berechnet die App KG, Meter und Stück neu aus den theoretischen Faktoren. |

> Ändert der Anwender den **Einheitencode** oder die **Artikelnr.** der Zeile, ermittelt die App die gültigen Faktoren neu und rechnet die Einheiten erneut durch. Ändert er den **Lagerortcode**, wird die Menge zur Lieferung in den drei Einheiten aktualisiert.

Die Umrechnung greift für alle mengenführenden Felder der Zeile – neben der Menge auch für die zu liefernde, gelieferte, zu fakturierende und fakturierte Menge, die Restmenge sowie die reservierte Menge; jeweils in KG, Meter und Stück. Auf der Verkaufszeilenübersicht sind standardmäßig die Spalten **KG**, **Meter** und **Stück** eingeblendet; weitere Einheiten-Varianten (z. B. zur Lieferung) lassen sich über die Spaltenauswahl einblenden.

### Übersichten und Drilldowns

- **Beschaffungsplanung:** Die Zeilen der Auftragsbezogenen Planung zeigen zusätzlich **Beschaffung KG**, **Beschaffung Meter** und **Beschaffung Stück** – die zu beschaffende Menge je Einheit.
- **Ausgeglichene Artikelposten:** Die Postenausgleichs-Übersicht zeigt **Ausgeglichene KG**, **Ausgeglichene Meter** und **Ausgeglichene Stück** – den in den drei Einheiten ausgeglichenen Anteil.
- **Produktion Buchungs-Blatt:** Die Zeilen zeigen zusätzlich **Verbrauch KG**, **Verbrauch Meter** und **Verbrauch Stück**.
- **Artikel-, Wert-, Kapazitäts- und Lagerplatzposten** führen die gebuchten KG-, Meter- und Stück-Werte je Buchung mit, sodass die drei Einheiten in der gesamten Nachverfolgung sichtbar bleiben.

## Nutzungsbeispiele (typische Anwendungsfälle)

Die folgenden Abläufe entsprechen der im Code hinterlegten Berechnungs- und Buchungslogik sowie den geführten Prozessen der Einheitenumrechnung. Alle Beispiele setzen voraus, dass die globale **KG Meter Stück Einrichtung** vorgenommen wurde und der Artikel theoretische Faktoren sowie – für Inkonsistenzen – einen Artikelverfolgungscode besitzt.

### Einkaufsbestellung mit Wareneingang

1. **Auslöser.** Ein Lieferant liefert Material, das im Haus in KG, Meter und Stück geführt wird; der Einkauf legt dazu eine Bestellung an.
2. **Einstieg in BC.** Öffnen Sie die **Einkaufsbestellung** und erfassen Sie in der Zeile die Artikelnr. Die Felder **KG**, **Meter** und **Stück** werden automatisch berechnet, ebenso die zugehörigen Werte für die aktuelle Lieferung, die bereits gelieferte Menge, die reservierte Menge, die aktuelle Rechnung und die Eingangsüberschussmenge.
3. **Kernablauf.** Öffnen Sie die **Artikelverfolgungszeilen** und hinterlegen Sie eine **Charge**. Die Charge wird zunächst mit den theoretischen Faktoren der Artikelkarte angelegt. Ändern Sie nun z. B. die **Meter**, während KG und Stück konstant bleiben sollen: Bei **Mengenänderung durch Nachfrage** erscheint der Dialog **„Möchten Sie alle Mengenfelder neu berechnen?"** – bestätigen Sie mit *Nein*, um eine **Inkonsistenz** zu erzeugen. Beim Verlassen der Artikelverfolgungszeilen werden die Inkonsistenzen auf die buchungsrelevanten Mengenfelder der Bestellzeile übertragen.
4. **Abschluss.** Erstellen und buchen Sie den **Wareneingang** und anschließend die **Einkaufsrechnung**. Sämtliche Mengenfelder samt Inkonsistenz werden in die gebuchte Einkaufslieferung, die Artikel- und Wertposten sowie – bei Lagerorten mit Lagerplätzen – die Lagerplatzposten übernommen.

### Fertigung inklusive Verbrauch

1. **Auslöser.** Ein Fertigungsauftrag soll produziert und der Materialverbrauch in den drei Einheiten gebucht werden.
2. **Einstieg in BC.** Legen Sie einen **Fertigungsauftrag** an (Status beliebig; gebucht wird auf freigegebene Aufträge). Die Felder der Einheitenumrechnung sind auf allen Status vorhanden und werden bei Anlage mit den theoretischen Faktoren berechnet – auch in den Fertigungsauftragskomponenten.
3. **Kernablauf.** Öffnen Sie das **Produktion Buchungs-Blatt**; je nach Fertigungseinrichtung erscheinen Verbrauchs- und Ist-Meldungszeilen mit den Feldern **Verbrauch KG/Meter/Stück**. Wählen Sie in der Artikelverfolgung der Verbrauchszeile eine **bestehende Charge**; deren Inkonsistenzen werden übernommen – die Umrechnungsfaktoren lassen sich hier nicht mehr ändern. Für die Ist-Meldung kann über die Artikelverfolgung eine **neue Charge** erzeugt werden, bei der Sie – z. B. bei *Mengenänderung durch Nachfrage* – durch Bestätigung mit *Nein* gezielt neue Inkonsistenzen anlegen.
4. **Abschluss.** Führen Sie die Funktion **Buchen** im Produktion Buchungs-Blatt aus. Durch die Ist-Meldung aktualisieren sich die Felder auf dem Fertigungsauftrag; es entstehen Artikel-, Wert- und Kapazitätsposten (sowie ggf. Lagerplatzposten) mit den jeweiligen Inkonsistenzen. Die für den Arbeitsplatz gepflegte **Zeitenberechnungseinheit** bestimmt dabei, auf welche Einheit sich die Zeitenberechnung stützt.

### Verkaufsauftrag mit Warenausgang und Kommissionierung

1. **Auslöser.** Ein Kunde bestellt Material, das in KG, Meter und Stück geführt wird.
2. **Einstieg in BC.** Öffnen Sie den **Verkaufsauftrag** und erfassen Sie die Artikelnr. Die Felder **KG**, **Meter** und **Stück** werden für Menge, zu liefernde und gelieferte Menge, reservierte Menge, zu fakturierende und fakturierte Menge berechnet.
3. **Kernablauf.** Hinterlegen Sie in den **Artikelverfolgungszeilen** eine **bestehende Charge**. Deren Inkonsistenzen werden in die Verkaufszeile übernommen; die Umrechnungsfaktoren sind bei bestehender Charge fixiert. Erstellen Sie aus dem Beleg heraus den **Warenausgang** und daraus die **Kommissionierung**; die Mengenfelder der Kommissionierzeilen spiegeln die Charge und ihre Inkonsistenzen.
4. **Abschluss.** **Registrieren** Sie die Kommissionierung und **buchen** Sie den Warenausgang; die Werte inklusive Inkonsistenzen gehen an die registrierte Kommissionierung, die gebuchte Verkaufslieferung, die Artikel- und Wertposten sowie ggf. die Lagerplatzposten. Buchen Sie abschließend die **Verkaufsrechnung**, deren Zeilen die Inkonsistenzen der Lieferung übernehmen.

## FAQ und Troubleshooting

### 1. Warum werden auf meinen Belegzeilen keine KG-, Meter- oder Stück-Werte berechnet?
Weil eine Voraussetzung fehlt. Die App rechnet nur, wenn in der **KG Meter Stück Einrichtung** alle drei Einheitencodes gesetzt sind, der **Basiseinheitencode** des Artikels einem dieser Codes entspricht und auf der Artikelkarte mindestens ein theoretischer Faktor gepflegt ist. Fehlt eines davon, bleiben die Einheitenfelder leer.

### 2. Warum kann ich auf der Artikelkarte keinen theoretischen Faktor eintragen?
Weil der **Basiseinheitencode** des Artikels keiner der drei in der globalen Einrichtung hinterlegten Einheiten (KG, Meter, Stück) entspricht. In diesem Fall weist das System die Eingabe mit einer Feldmeldung auf den Basiseinheitencode ab. Prüfen Sie zuerst die globale Einrichtung und die Basiseinheit des Artikels.

### 3. Warum lässt sich der theoretische Faktor eines Artikels nicht mehr ändern?
Weil zu diesem Artikel bereits **Posten oder offene Belege/Buchblätter** existieren. Die App prüft dies (`TestNoOpenEntriesExist`) und verhindert eine nachträgliche Faktoränderung, damit bereits berechnete Mengen nicht inkonsistent werden.

### 4. Wann entsteht eine Inkonsistenz und wann nicht?
Eine Inkonsistenz entsteht nur, wenn der Artikel eine aktive **Artikelverfolgung** besitzt und die **Mengenkonsistenzabfrage** auf *Mengen niemals ändern* oder *Mengenänderung durch Nachfrage* steht und der Anwender einen Einheitenwert abweichend von den Faktoren erfasst. Bei *Mengen immer ändern* werden die Werte stets neu berechnet – Inkonsistenzen sind dann ausgeschlossen.

### 5. Warum erscheint die Rückfrage „Möchten Sie alle Mengenfelder neu berechnen?"?
Weil für den Artikel die **Mengenkonsistenzabfrage** = *Mengenänderung durch Nachfrage* eingestellt ist. Bestätigen Sie mit *Ja*, um die übrigen Einheiten aus den Faktoren neu zu berechnen, oder mit *Nein*, um Ihren abweichenden Wert (eine Inkonsistenz) beizubehalten.

### 6. Warum wurden beim Umstellen auf „Mengen niemals ändern" meine zusätzlichen Artikeleinheiten gelöscht?
Weil in den Modi *Mengen niemals ändern* und *Mengenänderung durch Nachfrage* die Umrechnung über die App statt über die Standard-Artikeleinheiten erfolgt. Die App entfernt daher alle Artikeleinheiten außer der Basiseinheit und verhindert das Anlegen neuer Artikeleinheiten mit einer Fehlermeldung. In diesen Modi ist zudem ein **Artikelverfolgungscode** zwingend erforderlich.

### 7. Warum weichen berechnete KG/Meter/Stück geringfügig voneinander ab?
Weil je Einheit eine **Rundungspräzision** und eine **Rundungsregel** greifen. Je nach Einstellung (Keine Rundung, Aufrunden, Abrunden, Kaufmännisches Runden) wird das Rechenergebnis unterschiedlich gerundet. Prüfen Sie die Rundungsfelder im Bereich KG:/Meter:/Stück: der Artikelkarte.

### 8. Warum kann ich die Rundungsregel nicht auswählen?
Weil die zugehörige **Rundungspräzision** noch 0 ist. Das Feld Rundungsregel ist nur editierbar, wenn eine Präzision > 0 hinterlegt ist. Tragen Sie zuerst eine Präzision ein.

### 9. Warum kann ich die Umrechnungsfaktoren beim Verbrauch einer vorhandenen Charge nicht ändern?
Weil bei Prozessen mit **bestehender** Charge (z. B. Verbrauchscharge in der Produktion, Chargenauswahl im Verkaufsauftrag) die Faktoren der Charge fixiert sind. Neue Inkonsistenzen entstehen nur bei Prozessen, die eine **neue** Charge buchen (Einkaufsbestellung, Ist-Meldung, Artikelbuchblatt).

### 10. Warum lässt sich eine Chargennr.- oder Seriennr.-Informationskarte nicht löschen?
Weil zu dieser Charge bzw. Seriennummer bereits **Artikelposten** existieren. Das System weist den Löschversuch mit einer Fehlermeldung ab, um die Nachvollziehbarkeit der gebuchten Mengen zu erhalten.
