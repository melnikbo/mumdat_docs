---
title: Anwenderhandbuch m+m Own Delivery Rating
---

# Anwenderhandbuch m+m Own Delivery Rating

## Einleitung

Die Erweiterung **Eigene Liefertreue** ermöglicht es Ihnen, die eigene Lieferleistung gegenüber Ihren Debitoren systematisch zu überwachen und in einer nachvollziehbaren Bewertung abzubilden. Grundlage sind zwei Faktoren, die Sie frei aktivieren und gewichten können: die **Lieferverzögerung** (Abweichung des Buchungsdatums vom vereinbarten Lieferdatum) und die **Reklamationen** (gebuchte Verkaufsreklamationen). Aus den bei jeder Belegbuchung automatisch erfassten **Eigene Liefertreue Posten** berechnet das Modul je Debitor und Zeitraum eine Punktzahl und wandelt diese über ein frei definiertes Bewertungssystem in eine **Bewertung** um.

Primäre Zielgruppe sind **operative Anwender**, die täglich Verkaufsaufträge, Warenausgänge und Verkaufsreklamationen erfassen und buchen: Sie sehen unmittelbar in der Belegzeile den **Lieferstatus** (Pünktlich, Verzögerung, Zu früh) und lösen mit dem Buchen die Datenerfassung aus. Sekundäre Zielgruppe sind Administratoren und Auswertende, die das Bewertungssystem einrichten (Einrichtung, Bewertungssystem, Verzögerungskriterien) sowie im Arbeitsblatt periodisch berechnen und buchen.

Kurzer Prozessüberblick: Der Administrator legt in der **Eigene Liefertreue Einrichtung** fest, welche Faktoren einfließen, definiert das **Eigene Liefertreue System** (Punktebänder) und – bei aktiver Lieferverzögerung – die **Kriterien für die Lieferverzögerung**. Auf der **Debitorenkarte** markiert er die zu bewertenden Debitoren. Im Tagesgeschäft entstehen beim Buchen der Belege automatisch Posten. Periodisch berechnet und bucht der Anwender die Bewertungen im **Arbeitsblatt Bewertung der eigenen Liefertreue**; die Ergebnisse stehen anschließend auf der Debitorenkarte und in den Historienlisten zur Verfügung. Optional lässt sich zusätzlich eine **Externe Lieferantenbewertung** hinterlegen, um interne und externe Sicht zu vergleichen.

## Schnellstart für Anwender

Der folgende Ablauf führt in der vom Code erzwungenen Reihenfolge (Einrichtung vor Nutzung) zum ersten Bewertungsergebnis.

1. **Eigene Liefertreue Einrichtung** öffnen (über **Suchen**): Aktivieren Sie unter **Faktoren für die Berechnung der eigenen Liefertreue** mindestens einen Faktor – **Lieferverzögerung** und/oder **Reklamationen**. Bei aktiver **Lieferverzögerung** wählen Sie ein **Lieferdatum**; bei aktiven **Reklamationen** tragen Sie die **Reklamationspunkte** ein (Wert größer 0).
2. Über die Aktion **Liefertreue Bewertungssystem** die Punktebänder anlegen: je Zeile **Bewertungscode**, **Beschreibung**, **Punkte von**, **Punkte bis** – lückenlos und überschneidungsfrei.
3. Nur bei aktiver Lieferverzögerung: über die Aktion **Kriterien für die Lieferverzögerung** die Verzögerungsklassen anlegen (**Code**, **Verspätungstage von**, **Verspätungstage bis**, **Punkte**).
4. Auf der **Debitorenkarte** der zu bewertenden Debitoren das Feld **Im Bewertungssystem enthalten** auf **Ja** setzen.
5. Belege wie gewohnt buchen (**Verkaufsauftrag**, **Warenausgang**, **Verkaufsreklamation**). Beim Buchen entstehen automatisch **Eigene Liefertreue Posten**.
6. **Arbeitsblatt Bewertung der eigenen Liefertreue** öffnen (über **Suchen**), optional **Debitorenfilter** und **Zeitraum Filter** setzen.
7. Aktion **Eigene Liefertreue berechnen** ausführen: das Arbeitsblatt füllt sich mit den einbezogenen Debitoren und ermittelt **Gesamtpunktzahl** und **Errechnete Bewertung**.
8. Aktion **Buchen** ausführen und die Rückfrage *„Möchten Sie die Bewertungen buchen?“* mit **Ja** bestätigen. Die Bewertungen werden je Debitor als **Eigene Liefertreue** archiviert und sind auf der Debitorenkarte sichtbar.

## Einrichtung

Die **Eigene Liefertreue Einrichtung** ist die zentrale, unternehmensweite Einrichtungsseite (ein Datensatz je Mandant). Sie wird beim ersten Öffnen automatisch angelegt. Da die Seite die Kategorie *Administration* trägt, ist sie über **Suchen** auffindbar; ein übergeordnetes Listenblatt existiert nicht.

**Einstieg:** über **Suchen** die Seite **Eigene Liefertreue Einrichtung** öffnen.

Die Einrichtung steuert das gesamte Modul: Sie legt fest, **welche** Faktoren in die Bewertung einfließen, **welches** Lieferdatum für die Verzögerungsberechnung herangezogen wird und **wie** Reklamationen bepunktet werden. Von hier aus erreichen Sie über Aktionen die beiden abhängigen Einrichtungsseiten (Bewertungssystem, Verzögerungskriterien). Erst danach zeigt das Tagesgeschäft den **Lieferstatus** an und erzeugt beim Buchen Posten (siehe **Tägliche Arbeit** und **Bewertung berechnen und buchen**).

### Faktoren für die Berechnung der eigenen Liefertreue

Wer richtet das ein: Administrator/Key-User, einmalig vor der ersten Nutzung. Diese Seite entscheidet, ob das Modul überhaupt Daten sammelt und welche Zusatzfelder in den Belegen erscheinen.

| Einrichtung | Erläuterung |
|---|---|
| **Lieferverzögerung** | Wenn auf **Ja** gesetzt, bezieht das Modul Lieferverzögerungen in die Bewertung ein: In Verkaufsauftrags- und Warenausgangszeilen erscheint das Feld **Lieferstatus**, beim Buchen entstehen Posten vom Typ **Verspätungen**, und das Feld **Lieferdatum** sowie die **Kriterien für die Lieferverzögerung** werden aktiv. Ohne dieses Kennzeichen wird keine Verzögerung erfasst und die zugehörigen Aktionen/Spalten bleiben ausgeblendet. |
| **Lieferdatum** | Legt fest, gegen welches Datum das Buchungsdatum verglichen wird, wenn in der Verkaufszeile **kein** zugesagtes Lieferdatum hinterlegt ist. Wenn Sie hier einen Wert wählen, bestimmt dieser die Verzögerungsberechnung für alle betroffenen Zeilen. Nur sichtbar/relevant bei aktiver Lieferverzögerung (Pflichtangabe). Werte siehe unten. |
| **Reklamationen** | Wenn auf **Ja** gesetzt, wird bei jeder Buchung einer **Verkaufsreklamation** eines bewerteten Debitoren ein Posten vom Typ **Reklamation** erzeugt und die dabei abgezogenen **Reklamationspunkte** fließen in die Bewertung ein. Ohne dieses Kennzeichen bleiben Reklamationen bewertungsneutral. |
| **Reklamationspunkte** | Wenn ein Wert (> 0) gesetzt ist, wird dieser je gebuchter Verkaufsreklamation als **Abzug** verwendet (im Posten mit negativem Vorzeichen) – unabhängig von der Anzahl der Belegzeilen. Der Wert muss größer als 0 sein; andernfalls erscheint die Meldung *„Der Wert der Reklamationspunkte muss größer als 0 sein.“* Nur sichtbar/relevant bei aktiven Reklamationen. |

**Lieferdatum – mögliche Werte** (nur bei aktiver Lieferverzögerung, herangezogen wenn kein zugesagtes Lieferdatum vorliegt):

- **Geplante Lieferung:** Verzögerung wird gegen das geplante Lieferdatum der Verkaufszeile berechnet.
- **Geplanter Warenausgang:** Verzögerung wird gegen das geplante Warenausgangsdatum berechnet.
- **Warenausgang:** Verzögerung wird gegen das Warenausgangsdatum berechnet.
- **Gewünschte Lieferung:** Verzögerung wird gegen das gewünschte Lieferdatum berechnet.

Ist in der Verkaufszeile ein **zugesagtes Lieferdatum** gepflegt, hat dieses immer Vorrang; die Einstellung **Lieferdatum** greift dann nicht.

**Prozessschritte der Grundeinrichtung:** Zuerst aktivieren Sie die gewünschten Faktoren; danach legen Sie – abhängig von der Auswahl – das **Bewertungssystem** und (bei Lieferverzögerung) die **Verzögerungskriterien** an; schließlich markieren Sie die Debitoren auf der **Debitorenkarte**. Nicht ausgefüllte abhängige Einstellungen verfälschen die Berechnungsergebnisse.

### Lieferverzögerungsbewertung einrichten

Diese durchgehende Konfigurationskette aktiviert die Bewertung nach Liefertreue. Sie wird vom Administrator vor der ersten Nutzung angelegt und im Tagesgeschäft durch die automatische Posten-Erfassung beim Buchen von Verkaufsaufträgen und Warenausgängen konsumiert (siehe **Tägliche Arbeit**).

1. In der **Eigene Liefertreue Einrichtung** das Feld **Lieferverzögerung** auf **Ja** setzen. Wenn aktiviert, werden das Feld **Lieferdatum** und die Aktion **Kriterien für die Lieferverzögerung** freigeschaltet und in den Belegzeilen erscheint der **Lieferstatus**.
2. Das **Lieferdatum** wählen. Wenn gesetzt, bestimmt dieses die Referenz für die Verzögerungsberechnung, sofern in der Zeile kein zugesagtes Lieferdatum vorliegt.
3. Über die Aktion **Liefertreue Bewertungssystem** die Punktebänder definieren (siehe **Eigenes Bewertungssystem**). Wenn angelegt, kann aus der Gesamtpunktzahl eine **Bewertung** abgeleitet werden.
4. Über die Aktion **Kriterien für die Lieferverzögerung** die Verzögerungsklassen anlegen (siehe **Kriterien für die Lieferverzögerung**). Wenn angelegt, erhält jede Verzögerungsspanne die zugehörigen Punkte.
5. Auf der **Debitorenkarte** je Debitor **Im Bewertungssystem enthalten** auf **Ja** setzen. Wenn aktiviert, werden für diesen Debitor beim Buchen Verzögerungsposten erfasst.

Operativer Abschluss der Kette: Beim Buchen eines Verkaufsauftrags bzw. Warenausgangs für einen bewerteten Debitoren entsteht automatisch ein **Eigene Liefertreue Posten** (Typ **Verspätungen**); die Auswertung erfolgt im **Arbeitsblatt Bewertung der eigenen Liefertreue**.

#### Eigenes Bewertungssystem

**Einstieg:** in der **Eigene Liefertreue Einrichtung** die Aktion **Liefertreue Bewertungssystem** wählen (die Seite **Eigene Liefertreue System** ist nicht über **Suchen** auffindbar).

Wer richtet das ein: Administrator/Key-User, vor der ersten Bewertung. Das Bewertungssystem übersetzt die gesammelte **Gesamtpunktzahl** eines Debitoren in eine sprechende **Bewertung**. Es gilt für beide Faktoren gemeinsam und wird sowohl von der Lieferverzögerungs- als auch von der Reklamationsbewertung genutzt.

| Feld | Erläuterung |
|---|---|
| **Bewertungscode** | Eindeutiger Code der Bewertung (z. B. eine Note oder Stufe). Wenn gesetzt, wird dieser Code als Ergebnis in den Bewertungsseiten und auf der Debitorenkarte geführt. Darf nicht leer sein. |
| **Beschreibung** | Klartext zur Bewertung. Wenn gepflegt, hilft er dem Anwender, den Bewertungswert einzuordnen. |
| **Punkte von** | Untere Grenze des Punktebandes. Wenn gesetzt, gilt die Bewertung ab dieser Punktzahl. Darf nicht kleiner als 0 und nicht größer als **Punkte bis** sein; andernfalls erscheinen die Meldungen *„Die Anzahl der Punkte darf nicht unter 0 liegen.“* bzw. *„Der minimale Punktwert kann nicht höher sein als der maximale Punktwert.“* |
| **Punkte bis** | Obere Grenze des Punktebandes. Wenn gesetzt, gilt die Bewertung bis zu dieser Punktzahl. Muss gefüllt sein (Pflichtangabe beim Anlegen) und darf nicht kleiner als **Punkte von** sein. |

Dependency-Hinweis: Beim Anlegen und Ändern prüft das System, dass sich die Bänder **nicht überschneiden** und **lückenlos** aneinander anschließen; andernfalls erscheint *„Die Punktwerte müssen außerhalb der bestehenden Bereiche liegen.“* bzw. *„Die Bewertungen sollten der Reihe nach angegeben werden.“* Liegt eine Gesamtpunktzahl außerhalb aller Bänder, wird das nächstgelegene Randband verwendet.

#### Kriterien für die Lieferverzögerung

**Einstieg:** in der **Eigene Liefertreue Einrichtung** die Aktion **Kriterien für die Lieferverzögerung** wählen (die Seite **Eigene Liefertreue Kriterien** ist nicht über **Suchen** auffindbar und nur bei aktiver **Lieferverzögerung** verfügbar).

Wer richtet das ein: Administrator/Key-User, vor der ersten Nutzung, sobald die Lieferverzögerung aktiv ist. Hier ordnen Sie jeder Spanne von Verzögerungstagen einen Punktwert zu. Auf Basis dieser Kriterien erhält jeder beim Buchen erzeugte Verzögerungsposten seine **Bewertungspunkte** und seinen Kriteriencode.

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger Code der Verzögerungsklasse. Wenn gesetzt, wird dieser Code am erzeugten Posten und in der **Statistik der Lieferverzögerung** geführt. Darf nicht leer sein. |
| **Beschreibung** | Klartext zur Verzögerungsklasse. Wenn gepflegt, erleichtert er die Einordnung in Auswertungen. |
| **Verspätungstage von** | Untere Grenze der Verzögerungsspanne in Tagen. Wenn gesetzt, gilt die Klasse ab dieser Tagesanzahl. Negative Werte bedeuten „zu früh“, 0 bedeutet „pünktlich“, positive Werte bedeuten „Verspätung“. Darf nicht größer als **Verspätungstage bis** sein. |
| **Verspätungstage bis** | Obere Grenze der Verzögerungsspanne in Tagen. Wenn gesetzt, gilt die Klasse bis zu dieser Tagesanzahl. Darf nicht kleiner als **Verspätungstage von** sein; andernfalls erscheint *„Der Wert für die minimalen Verspätungstage darf nicht höher sein als der Wert für die maximalen Verspätungstage.“* |
| **Punkte** | Punktwert, der dem Debitor für Posten dieser Verzögerungsklasse gutgeschrieben oder abgezogen wird. Wenn gesetzt, fließt er in die Durchschnittsbildung der Lieferverzögerungspunkte ein (frühe/pünktliche Lieferungen können positiv, Verspätungen negativ gewertet werden – je nach Ihrer Punktvergabe). |

Dependency-Hinweis: Wie beim Bewertungssystem müssen die Tagesspannen **überschneidungsfrei** und **lückenlos** sein (gleiche Prüfmeldungen). Fällt die berechnete Verzögerung außerhalb aller Spannen, wird das nächstgelegene Randkriterium verwendet.

### Reklamationsbewertung einrichten

Diese Konfigurationskette aktiviert den zweiten Bewertungsfaktor. Sie wird vom Administrator vor der ersten Nutzung angelegt und im Tagesgeschäft durch das Buchen von **Verkaufsreklamationen** bewerteter Debitoren konsumiert.

1. In der **Eigene Liefertreue Einrichtung** das Feld **Reklamationen** auf **Ja** setzen. Wenn aktiviert, wird das Feld **Reklamationspunkte** eingeblendet und beim Buchen von Verkaufsreklamationen entstehen Posten vom Typ **Reklamation**.
2. Die **Reklamationspunkte** (> 0) eintragen. Wenn gesetzt, wird dieser Betrag je gebuchter Verkaufsreklamation vom Punktekonto des Debitoren abgezogen.
3. Über die Aktion **Liefertreue Bewertungssystem** die Punktebänder anlegen (gemeinsame Nutzung mit der Lieferverzögerungsbewertung, siehe **Eigenes Bewertungssystem**).
4. Auf der **Debitorenkarte** je Debitor **Im Bewertungssystem enthalten** auf **Ja** setzen. Wenn aktiviert, werden für diesen Debitor Reklamationsposten erfasst.

Operativer Abschluss der Kette: Beim Buchen einer Verkaufsreklamation eines bewerteten Debitoren entsteht ein **Eigene Liefertreue Posten** (Typ **Reklamation**) mit dem negativen Reklamationspunktwert; die Auswertung erfolgt im Arbeitsblatt.

### Berechtigungen

Das Modul liefert einen zuweisbaren Berechtigungssatz für die eigene Liefertreue (technische Kennung `MuM OR Own Deliv Rat`). Dieser bestimmt die Berechtigungen für die Modultabellen und -seiten (Lese-/Schreibrechte auf Einrichtung, Bewertungssystem, Kriterien, Posten, Arbeitsblatt, Bewertungen und externe Lieferantenbewertungen sowie Ausführungsrecht auf die zugehörigen Codeunits). Weisen Sie ihn allen Anwendern zu, die Belege bewerteter Debitoren buchen oder Bewertungen berechnen. Voraussetzung für den Betrieb ist eine gültige Lizenz der Grundlösung **m+m Cloud Base**; die Lizenzprüfung erfolgt automatisch bei der Anmeldung.

## Stammdaten

### Debitorenkarte: Debitor in die Bewertung aufnehmen

**Einstieg:** über die **Debitorenliste** den Debitor öffnen und die **Debitorenkarte** aufrufen; die Felder der eigenen Liefertreue befinden sich in der Gruppe **Eigene Liefertreue** unterhalb der Statistik.

Wer pflegt das: Administrator/Key-User, je Debitor. Die Debitorenkarte ist die Stammdatenstelle, an der Sie **auswählen**, welche Debitoren überhaupt bewertet werden – nicht jeder Debitor muss in das System aufgenommen werden. Von diesem Kennzeichen hängt ab, ob in den Belegen der **Lieferstatus** erscheint, ob beim Buchen Posten entstehen und ob der Debitor im Arbeitsblatt einbezogen wird.

| Feld | Erläuterung |
|---|---|
| **Im Bewertungssystem enthalten** | Wenn auf **Ja** gesetzt, wird der Debitor in die eigene Liefertreue aufgenommen: In seinen Verkaufsauftrags- und Warenausgangszeilen erscheint der **Lieferstatus**, beim Buchen seiner Belege entstehen Posten, und er wird im Arbeitsblatt berücksichtigt. Bei **Nein** werden keine Bewertungsdaten mehr für ihn erfasst und die Zusatzfelder/Aktionen bleiben inaktiv. |
| **Bewertung** | Zeigt die zuletzt berechnete und gebuchte eigene Liefertreue des Debitoren (nicht editierbar). Nur sichtbar, wenn der Debitor im Bewertungssystem enthalten ist. |
| **Bewertungszeitraum** | Zeigt den Zeitraum der zuletzt gebuchten Bewertung (nicht editierbar). |
| **Externe Lieferantenbewertung** | Zeigt die zuletzt erfasste externe Bewertung des Debitoren (nicht editierbar) – zum Vergleich der internen mit der externen Sicht. |
| **Externer Lieferantenbewertungszeitraum** | Zeigt den Zeitraum der zuletzt erfassten externen Bewertung (nicht editierbar). |

Über die Debitorenkarte erreichen Sie zudem die Historien- und Vergleichsseiten des Debitoren (Aktionen **Eigene Liefertreuen** und **Externe Lieferantenbewertungen**, beide nur aktiv, wenn **Im Bewertungssystem enthalten = Ja**). Diese sind unter **Historie und Vergleich** beschrieben. Das Kennzeichen ist die gemeinsame Voraussetzung beider Einrichtungsketten (**Lieferverzögerungsbewertung einrichten**, **Reklamationsbewertung einrichten**).

## Tägliche Arbeit an den Verkaufsbelegen

Im Tagesgeschäft müssen Anwender nichts zusätzlich erfassen: Die eigene Liefertreue ist eng mit der Verkaufsabwicklung verbunden. Für bewertete Debitoren blendet das Modul in den Belegzeilen den **Lieferstatus** ein und erzeugt beim Buchen automatisch die **Eigene Liefertreue Posten**. Welche Faktoren erfasst werden, steuert die **Eigene Liefertreue Einrichtung** (Lieferverzögerung, Reklamationen); wer bewertet wird, steuert die **Debitorenkarte** (Im Bewertungssystem enthalten).

### Lieferstatus in der Verkaufsauftragszeile

Ist der Debitor im Bewertungssystem enthalten und ist die **Lieferverzögerung** aktiv, zeigt die Verkaufsauftragszeile die zusätzliche Spalte **Lieferstatus**. Sie wird automatisch beim Öffnen und beim Ändern der relevanten Datumsfelder (**Geplantes Lieferdatum**, **Geplantes Warenausgangsdatum**, **Warenausgangsdatum**, **Zugesagtes Lieferdatum**, **Gewünschtes Lieferdatum**) sowie des **Lagerortcodes** neu ermittelt.

| Feld | Erläuterung |
|---|---|
| **Lieferstatus** | Wenn das Buchungsdatum voraussichtlich später als das maßgebliche Lieferdatum ist, zeigt die Zeile **Verzögerung**; ist es früher, zeigt sie **Zu früh**; stimmen beide überein, zeigt sie **Pünktlich**. Maßgeblich ist das **Zugesagte Lieferdatum**, ersatzweise das in der Einrichtung gewählte **Lieferdatum**. Erfordert der Lagerort einen Warenausgang, bleibt das Feld leer, weil der Status dann am Warenausgang ermittelt wird. |

Werte des Lieferstatus:

- **Pünktlich:** Buchungsdatum entspricht dem maßgeblichen Lieferdatum – keine Verzögerung.
- **Verzögerung:** Buchungsdatum liegt nach dem maßgeblichen Lieferdatum – die Lieferung ist verspätet.
- **Zu früh:** Buchungsdatum liegt vor dem maßgeblichen Lieferdatum – die Lieferung erfolgt vor Termin.

### Lieferstatus im Warenausgang

Erfordert der Lagerort einen Warenausgang, bleibt der Lieferstatus in der Verkaufsauftragszeile leer und wird stattdessen in der **Warenausgang**-Zeile angezeigt (Spalte **Lieferstatus**, gleiche Werte **Pünktlich**, **Verzögerung**, **Zu früh**). Maßgeblich ist hier das **Buchungsdatum des Warenausgangs** im Verhältnis zum maßgeblichen Lieferdatum der zugehörigen Verkaufsauftragszeile. Wird das **Buchungsdatum** im Warenausgangskopf geändert, aktualisiert sich die Anzeige.

### Automatische Erfassung der Posten beim Buchen

Beim Buchen von Verkaufsbelegen bewerteter Debitoren erzeugt das Modul die **Eigene Liefertreue Posten** – ohne weitere Eingabe:

1. **Verkaufsauftrag buchen** (ohne Warenausgangspflicht am Lagerort): Ist **Lieferverzögerung = Ja**, wird je Verkaufszeile die Verzögerung berechnet und ein Posten vom Typ **Verspätungen** geschrieben.
2. **Warenausgang buchen** (bei warenausgangspflichtigem Lagerort): Der Verzögerungsposten wird stattdessen beim Warenausgang erzeugt (auf Basis des Warenausgang-Buchungsdatums). Wird anschließend die zugehörige Verkaufsauftragszeile gebucht, entsteht **kein** zweiter Posten – so wird eine doppelte Erfassung vermieden.
3. **Verkaufsreklamation buchen**: Ist **Reklamationen = Ja**, wird je Beleg ein Posten vom Typ **Reklamation** mit den negativen **Reklamationspunkten** geschrieben (unabhängig von der Zeilenanzahl; die Herkunftsbelegzeilennummer ist hier immer 0).

Alle so erfassten Daten sind in **Eigene Liefertreue Posten** einsehbar und bilden die Grundlage der Berechnung im Arbeitsblatt.

### Eigene Liefertreue Posten

**Einstieg:** über **Suchen** die Seite **Eigene Liefertreue Posten** öffnen; oder per DrillDown aus dem Arbeitsblatt und der Debitorenkarte. Die Seite ist nicht editierbar und dient der Nachverfolgung der erfassten Daten.

| Feld | Erläuterung |
|---|---|
| **Debitorennr.** | Debitor, zu dem der Posten gehört. |
| **Dokumententyp** | Herkunftsbelegart des Postens. Werte siehe unten. |
| **Dokumentennr.** | Nummer des Herkunftsbelegs (Verkaufsauftrag, Warenausgang oder Verkaufsreklamation). |
| **Herkunftsbelegzeilennummer** | Zeile des Herkunftsbelegs. Bei Verkaufsauftrag/Warenausgang je Zeile gefüllt; bei Verkaufsreklamation immer 0, da pro Beleg berechnet wird. |
| **Buchungsdatum** | Buchungsdatum des Herkunftsbelegs. |
| **Bewertungskriterien Typ** | Art des Bewertungskriteriums. Werte siehe unten. |
| **Verzögerungstage** | Anzahl der Verzögerungstage (nur bei Typ **Verspätungen**): negativer Wert = zu früh, 0 = pünktlich, positiver Wert = Verspätung. |
| **Bewertungspunkte** | Punkte, die bei der Berechnung hinzugefügt oder abgezogen werden. |
| **Postennr.** | Fortlaufende, eindeutige Postennummer (technische Sortierung, standardmäßig ausgeblendet). |

**Dokumententyp – mögliche Werte:**

- **(leer):** kein Herkunftstyp gesetzt (technischer Ausgangswert; bei erzeugten Posten nicht verwendet).
- **Verkaufsauftrag:** Posten stammt aus einem gebuchten Verkaufsauftrag.
- **Verkaufsreklamation:** Posten stammt aus einer gebuchten Verkaufsreklamation.
- **Warenausgang:** Posten stammt aus einem gebuchten Warenausgang.

**Bewertungskriterien Typ – mögliche Werte:**

- **Verspätungen:** Posten bewertet eine Lieferverzögerung; **Verzögerungstage** und die Verzögerungsklasse (**Lieferverzögerung**) sind gefüllt.
- **Reklamation:** Posten bewertet eine Verkaufsreklamation; die **Bewertungspunkte** enthalten den negativen Reklamationsabzug.

## Bewertung berechnen und buchen

Die periodische Bewertung erfolgt im **Arbeitsblatt Bewertung der eigenen Liefertreue**. Es liest die **Eigene Liefertreue Posten**, verdichtet sie je Debitor und Zeitraum zu einer **Gesamtpunktzahl**, leitet daraus die **Errechnete Bewertung** ab und archiviert die Ergebnisse beim Buchen als **Eigene Liefertreue**. Welche Faktoren einfließen und welche Spalten sichtbar sind, richtet sich nach der **Eigene Liefertreue Einrichtung**.

**Einstieg:** über **Suchen** die Seite **Arbeitsblatt Bewertung der eigenen Liefertreue** öffnen.

### Filter

Vor der Berechnung grenzen Sie die einbezogenen Debitoren und den Auswertungszeitraum ein.

| Filterfeld | Erläuterung |
|---|---|
| **Debitorenfilter** | Wenn gesetzt, werden nur die ausgewählten, im Bewertungssystem enthaltenen Debitoren in das Arbeitsblatt aufgenommen. Über die AssistEdit-Schaltfläche (drei Punkte) lassen sich Debitoren aus der Debitorenliste wählen (nur bewertete Debitoren). Ohne Debitorenfilter werden bei der Berechnung alle enthaltenen Debitoren einbezogen. |
| **Zeitraum Filter** | Wenn gesetzt, werden nur Posten mit Buchungsdatum in diesem Zeitraum in die Durchschnitts- und Summenbildung sowie in die Factbox einbezogen. Der Zeitraum bestimmt außerdem **Bewertungszeitraum von/bis** der gebuchten Bewertung. |

### Arbeitsblattzeilen

| Feld | Erläuterung |
|---|---|
| **Debitorennr.** | Debitor der Arbeitsblattzeile (nur bewertete Debitoren wählbar). |
| **Debitorenname** | Name des Debitoren (wird automatisch übernommen). |
| **Letzte Bewertung** | Zuletzt gebuchte Bewertung des Debitoren (nicht editierbar) – zum Vergleich mit dem neuen Ergebnis. |
| **Errechnete Bewertung** | Für den gewählten Zeitraum neu ermittelte Bewertung (nicht editierbar); wird durch **Eigene Liefertreue berechnen** gesetzt. |
| **Durchschnittliche Punkte (Lieferverzögerungen)** | Durchschnitt der Bewertungspunkte aus Verzögerungsposten im Zeitraum. Nur sichtbar, wenn **Lieferverzögerung = Ja**. Per DrillDown lassen sich die zugrunde liegenden Posten anzeigen. |
| **Summe der Punkte (Reklamationen)** | Summe der Bewertungspunkte aus Reklamationsposten im Zeitraum (stets negativer Wert). Nur sichtbar, wenn **Reklamationen = Ja**. Per DrillDown lassen sich die zugrunde liegenden Posten anzeigen. |
| **Gesamtpunktzahl** | Ergebnis **Durchschnittliche Punkte (Lieferverzögerungen) + Summe der Punkte (Reklamationen)** (jeder Summand nur bei aktivem Faktor). Aus diesem Wert wird über das Bewertungssystem die **Errechnete Bewertung** bestimmt. |

### Factbox „Statistik der Lieferverzögerung“

Rechts neben den Arbeitsblattzeilen zeigt die Factbox **Statistik der Lieferverzögerung** für den markierten Debitoren, wie sich seine Verzögerungsposten im gewählten Zeitraum auf die Kriterien verteilen.

| Feld | Erläuterung |
|---|---|
| **Lieferverzögerung** | Verzögerungsklasse (Code aus **Kriterien für die Lieferverzögerung**). |
| **Anzahl von Posten** | Anzahl der Verzögerungsposten dieser Klasse im Zeitraum. Per DrillDown werden die zugehörigen **Eigene Liefertreue Posten** angezeigt. |

### Buchungsablauf

Der Berechnungs- und Buchungsablauf entspricht dem Schnellstart und wird hier vertieft (die Schnellstartschritte 6–8 spiegeln diese Nummerierung):

1. **Arbeitsblatt Bewertung der eigenen Liefertreue** öffnen.
2. **Debitorenfilter** und/oder **Zeitraum Filter** setzen (optional; ohne Debitorenfilter werden bei der Berechnung alle enthaltenen Debitoren aufgenommen).
3. Aktion **Eigene Liefertreue berechnen** ausführen: Sind noch keine Zeilen vorhanden, werden alle enthaltenen Debitoren eingefügt; anschließend werden **Gesamtpunktzahl** und **Errechnete Bewertung** je Zeile ermittelt.
4. Aktion **Buchen** ausführen. Es erscheint die Rückfrage *„Möchten Sie die Bewertungen buchen?“*. Bei **Ja** wird je Zeile mit Posten im Zeitraum ein **Eigene Liefertreue**-Datensatz (Bewertungszeitraum von/bis, Bewertung) archiviert und die Arbeitsblattzeile entfernt. Zeilen ohne Posten im Zeitraum werden nicht gebucht und mit *„Für den Kunden %1 gibt es nichts zu buchen.“* protokolliert. Nach erfolgreicher Buchung erscheint *„Eig. Liefertreuenbewertungen sind gebucht“*.

Es gibt keinen zwischengeschalteten Buchungsbeleg und keine Teilbuchung: Das Buchen überträgt alle vorhandenen Arbeitsblattzeilen unmittelbar in das Bewertungsarchiv. Ein Debitor kann für einen identischen Zeitraum nicht mehrfach bewertet werden.

## Historie und Vergleich

Die gebuchten Bewertungen und die erfassten Rohdaten stehen dauerhaft zur Nachverfolgung bereit; zusätzlich lassen sich externe Bewertungen zum Vergleich hinterlegen.

### Eigene Liefertreuen (gebuchte Bewertungen)

**Einstieg:** auf der **Debitorenkarte** eines bewerteten Debitoren die Aktion **Eigene Liefertreuen** wählen (nur aktiv, wenn **Im Bewertungssystem enthalten = Ja**).

| Feld | Erläuterung |
|---|---|
| **Bewertungszeitraum von** | Beginn des Zeitraums, für den die Bewertung gebucht wurde. |
| **Bewertungszeitraum bis** | Ende des Zeitraums, für den die Bewertung gebucht wurde. |
| **Bewertung** | Die für diesen Zeitraum ermittelte eigene Liefertreue. |

Über die Aktion **Eigene Liefertreue Posten** springen Sie von einer Bewertung in die zugrunde liegenden Posten des jeweiligen Zeitraums (nur aktiv, wenn Datensätze vorhanden sind).

### Externe Lieferantenbewertungen

**Einstieg:** auf der **Debitorenkarte** eines bewerteten Debitoren die Aktion **Externe Lieferantenbewertungen** wählen (nur aktiv, wenn **Im Bewertungssystem enthalten = Ja**).

Hier erfassen Sie extern ermittelte Bewertungen desselben Debitoren, um die intern berechnete eigene Liefertreue mit der externen Sicht zu vergleichen. Die Felder entsprechen denen der gebuchten Bewertungen.

| Feld | Erläuterung |
|---|---|
| **Bewertungszeitraum von** | Beginn des Zeitraums der externen Bewertung. |
| **Bewertungszeitraum bis** | Ende des Zeitraums der externen Bewertung. |
| **Bewertung** | Extern vergebene Bewertung (Bewertungscode aus dem eigenen Bewertungssystem). |

Die zuletzt erfasste externe Bewertung erscheint zusätzlich auf der Debitorenkarte in den Feldern **Externe Lieferantenbewertung** und **Externer Lieferantenbewertungszeitraum**.

## FAQ und Troubleshooting

### Warum erscheint in der Verkaufsauftragszeile kein Lieferstatus?

Der **Lieferstatus** wird nur angezeigt, wenn der Debitor auf der Debitorenkarte **Im Bewertungssystem enthalten = Ja** hat **und** in der **Eigene Liefertreue Einrichtung** die **Lieferverzögerung** aktiv ist. Erfordert der Lagerort der Zeile zusätzlich einen Warenausgang, bleibt das Feld in der Auftragszeile leer – der Status erscheint dann in der Warenausgangszeile.

### Warum entstehen beim Buchen keine Eigene Liefertreue Posten?

Posten werden nur für Debitoren mit **Im Bewertungssystem enthalten = Ja** erzeugt und nur für aktive Faktoren: Verzögerungsposten setzen **Lieferverzögerung = Ja** voraus, Reklamationsposten setzen **Reklamationen = Ja** voraus. Ist keiner der Faktoren aktiv oder der Debitor nicht aufgenommen, bleibt die Buchung bewertungsneutral.

### Warum wird ein Verzögerungsposten nicht beim Verkaufsauftrag, sondern erst beim Warenausgang erzeugt?

Erfordert der Lagerort der Verkaufszeile einen Warenausgang, überspringt das Modul die Erfassung beim Auftragsbuchen und erzeugt den Posten beim Buchen des Warenausgangs (mit dem Warenausgang-Buchungsdatum). Das verhindert eine doppelte Erfassung, wenn anschließend die Auftragszeile gebucht wird.

### Welches Datum wird für die Verzögerungsberechnung herangezogen?

Vorrang hat das **Zugesagte Lieferdatum** der Verkaufszeile. Ist es leer, verwendet das Modul das in der **Eigene Liefertreue Einrichtung** unter **Lieferdatum** gewählte Datum: **Geplante Lieferung**, **Geplanter Warenausgang**, **Warenausgang** oder **Gewünschte Lieferung**. Die Verzögerung ist die Differenz zwischen Buchungsdatum und diesem Datum.

### Was bedeuten negative Verzögerungstage?

Die **Verzögerungstage** ergeben sich aus Buchungsdatum minus maßgeblichem Lieferdatum. Ein **negativer** Wert bedeutet „zu früh“, **0** bedeutet „pünktlich“, ein **positiver** Wert bedeutet „Verspätung“. Über die **Kriterien für die Lieferverzögerung** ordnen Sie jeder Spanne Punkte zu.

### Warum lässt sich das Bewertungssystem nicht speichern („Bereiche“ / „der Reihe nach“)?

Die Punktebänder im **Eigene Liefertreue System** müssen überschneidungsfrei und lückenlos sein. Überschneiden sich Bänder, erscheint *„Die Punktwerte müssen außerhalb der bestehenden Bereiche liegen.“*; entsteht eine Lücke, erscheint *„Die Bewertungen sollten der Reihe nach angegeben werden.“* Passen Sie **Punkte von/bis** so an, dass die Bänder direkt aneinander anschließen.

### Warum darf ich negative oder zu große Punktgrenzen nicht eingeben?

Im Bewertungssystem darf **Punkte von** nicht kleiner als 0 sein (*„Die Anzahl der Punkte darf nicht unter 0 liegen.“*) und nicht größer als **Punkte bis** (*„Der minimale Punktwert kann nicht höher sein als der maximale Punktwert.“*). **Punkte bis** ist zudem beim Anlegen eine Pflichtangabe. Diese Regeln sichern eine konsistente Zuordnung der Gesamtpunktzahl.

### Warum meldet das Buchen „Für den Kunden … gibt es nichts zu buchen“?

Eine Arbeitsblattzeile wird nur gebucht, wenn im gewählten **Zeitraum Filter** tatsächlich **Eigene Liefertreue Posten** für den Debitoren existieren. Fehlen Posten (z. B. falscher Zeitraum oder keine gebuchten Belege), wird die Zeile übersprungen und der Hinweis protokolliert. Prüfen Sie Zeitraum und vorhandene Posten.

### Warum kann ich für denselben Zeitraum keine zweite Bewertung buchen?

Der Schlüssel der gebuchten **Eigene Liefertreue** besteht aus Debitor und Bewertungszeitraum. Ein Debitor kann daher für einen identischen Zeitraum nicht mehrfach bewertet werden. Wählen Sie einen anderen Zeitraum oder bereinigen Sie die vorhandene Bewertung.

### Warum sind die Spalten „Durchschnittliche Punkte (Lieferverzögerungen)“ oder „Summe der Punkte (Reklamationen)“ nicht sichtbar?

Diese Spalten und ihr Beitrag zur **Gesamtpunktzahl** hängen an den Faktoren der Einrichtung: Die Verzögerungsspalte erscheint nur bei **Lieferverzögerung = Ja**, die Reklamationsspalte nur bei **Reklamationen = Ja**. Aktivieren Sie den jeweiligen Faktor in der **Eigene Liefertreue Einrichtung**.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen realistische Auslöser und den chronologischen Ablauf in Business Central. Alle Schritte sind durch die Modullogik abgedeckt.

### Szenario 1: Quartalsbewertung eines Debitoren

**Auslöser:** Zum Quartalsende soll die Liefertreue gegenüber einem Schlüsselkunden ausgewertet und dokumentiert werden.

**Einstieg in BC:** Über **Suchen** das **Arbeitsblatt Bewertung der eigenen Liefertreue** öffnen.

**Kernablauf:**
1. **Debitorenfilter** auf den betreffenden Debitoren und **Zeitraum Filter** auf das Quartal setzen.
2. Aktion **Eigene Liefertreue berechnen** ausführen. Das Arbeitsblatt zeigt **Durchschnittliche Punkte (Lieferverzögerungen)**, **Summe der Punkte (Reklamationen)**, **Gesamtpunktzahl** und **Errechnete Bewertung**; die Factbox **Statistik der Lieferverzögerung** schlüsselt die Verzögerungsklassen auf (DrillDown über **Anzahl von Posten**).
3. Aktion **Buchen** ausführen und *„Möchten Sie die Bewertungen buchen?“* mit **Ja** bestätigen.

**Abschluss:** Die Bewertung erscheint unter **Eigene Liefertreuen** und auf der **Debitorenkarte** (Felder **Bewertung**, **Bewertungszeitraum**).

### Szenario 2: Verspäteter Warenausgang bei lagerortpflichtiger Abwicklung

**Auslöser:** Die Logistik meldet, dass eine Lieferung an einen bewerteten Debitoren erst nach dem zugesagten Termin das Lager verlassen hat.

**Einstieg in BC:** Den **Verkaufsauftrag** des Debitoren öffnen; da der Lagerort einen Warenausgang erfordert, ist der **Lieferstatus** in der Auftragszeile leer und wird im **Warenausgang** geführt.

**Kernablauf:**
1. Im **Warenausgang** die Zeile prüfen: Der **Lieferstatus** zeigt **Verzögerung**, wenn das Warenausgang-Buchungsdatum nach dem maßgeblichen Lieferdatum liegt.
2. Den Warenausgang buchen. Dabei entsteht automatisch ein **Eigene Liefertreue Posten** vom Typ **Verspätungen** mit den ermittelten **Verzögerungstagen** und den Punkten der passenden Verzögerungsklasse.

**Abschluss:** Der Posten ist in **Eigene Liefertreue Posten** sichtbar und fließt in die nächste Quartalsberechnung ein. Eine spätere Buchung der zugehörigen Auftragszeile erzeugt keinen zweiten Posten.

### Szenario 3: Reklamation eines bewerteten Debitoren

**Auslöser:** Ein Debitor meldet fehlerhafte Ware; es wird eine Verkaufsreklamation erfasst.

**Einstieg in BC:** Die **Verkaufsreklamation** des Debitoren erfassen und buchen (Voraussetzung: **Reklamationen = Ja** und **Reklamationspunkte** gepflegt).

**Kernablauf:**
1. Die Verkaufsreklamation buchen. Es entsteht genau ein **Eigene Liefertreue Posten** vom Typ **Reklamation** mit den negativen **Reklamationspunkten** – unabhängig von der Zeilenanzahl.
2. Bei der nächsten Berechnung im Arbeitsblatt mindert dieser Posten über **Summe der Punkte (Reklamationen)** die **Gesamtpunktzahl** des Debitoren.

**Abschluss:** Die verschlechterte Bewertung wird beim nächsten **Buchen** archiviert und ist auf der Debitorenkarte nachvollziehbar; per DrillDown im Arbeitsblatt lässt sich der auslösende Reklamationsposten anzeigen.
