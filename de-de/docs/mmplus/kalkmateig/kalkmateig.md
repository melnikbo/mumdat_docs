---
title: Anwenderhandbuch m+m Calculation with Material Properties
---

# Anwenderhandbuch m+m Calculation with Material Properties

## Einleitung

Die App **m+m Calculation with Material Properties** erweitert die m+m App **Kalkulation** in Microsoft Dynamics 365 Business Central um die Bewertung von **Materialeigenschaften** innerhalb einer Kalkulation. Sie ermöglicht es, den Kalkulationspreis eines Artikels nicht nur aus festen Zeilenwerten zu bilden, sondern zusätzlich aus den **Eigenschaften** des Materials abzuleiten: Je nach hinterlegter **Materialart**, **Eigenschaft** und deren **Wert** fließen definierte **Kosten** in die Kalkulationszeile ein.

Zusätzlich stellt die App zwei weitere Herleitungsarten für Kalkulationszeilen bereit: die direkte Übernahme eines numerischen **Belegeigenschaftswerts** in die Zeile sowie eine frei definierbare **Berechnungsformel**, die Eigenschaftswerte und Rechenoperatoren kombiniert. Schließlich kann ein **Artikel** so gekennzeichnet werden, dass beim Erfassen einer Verkaufszeile automatisch eine Kalkulation erzeugt, zertifiziert und deren **Verkaufspreis** in die Zeile geschrieben wird.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender im Verkauf und in der Kalkulation**, die Verkaufsbelege erfassen, Kalkulationen öffnen und deren Eigenschaften pflegen. Sekundär angesprochen sind **Administratoren und Key-User**, die die Kalkulationsvorlagen, die Materialeigenschaftskosten und die Artikelkennzeichnung einrichten.

**Kurzer Prozessüberblick:** Der Administrator hinterlegt zunächst die **Materialeigenschaftskosten** und erweitert eine **Kalkulationsvorlage** um die neue **Feldart**. Im Tagesgeschäft entsteht die Kalkulation entweder automatisch beim Erfassen einer Verkaufszeile (wenn der Artikel entsprechend gekennzeichnet ist) oder manuell über die Aktion **Erstelle/Öffne Kalkulation** auf der Belegzeile. Der Anwender kann die **Eigenschaften** einer Kalkulation nachträglich über die Aktion **Eigenschaften bearbeiten** anpassen und neu berechnen lassen.

Voraussetzung ist, dass die abhängigen Apps **m+m Kalkulation** und **m+m Material Properties** installiert und eingerichtet sind: Die **Materialarten** und **Eigenschaften** stammen aus der App m+m Material Properties, die **Kalkulationsvorlage** und der Kalkulationsbeleg aus der App m+m Kalkulation.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zum kalkulierten Preis. Die Einrichtungsschritte sind Voraussetzung und müssen in dieser Reihenfolge erfolgen; erst danach folgt die tägliche Arbeit.

1. **Eigenschaften und Materialarten prüfen (Voraussetzung, App m+m Material Properties).** Stellen Sie sicher, dass die benötigten **Materialarten** und **Eigenschaften** samt Datentyp bereits gepflegt sind, denn die Materialeigenschaftskosten verweisen darauf.
2. **Materialeigenschaftskosten hinterlegen.** Öffnen Sie über die Suche die Liste **Materialeigenschaftskosten** und erfassen Sie je Kombination aus **Materialartencode**, **Eigenschaftscode** und **Wert** (bzw. **Wert**/**Bis Wert** als Bereich) die zugehörigen **Kosten**. Siehe *Einrichtung → Materialeigenschaftskosten einrichten*.
3. **Kalkulationsvorlage erweitern.** Öffnen Sie in **Kalkulationsvorlagen** die gewünschte Vorlage und setzen Sie in einer Zeile die **Feldart** auf **Materialeigenschaftskosten** (oder auf **Belegeigenschaftswert nutzen** bzw. **Berechnungsformel verwenden**). Siehe *Einrichtung*.
4. **(Optional) Artikel für automatische Kalkulation kennzeichnen.** Setzen Sie auf der **Artikelkarte** in der Infobox **Preise & Verkauf** das Kennzeichen **Automatisch kalkulieren**. Siehe *Einrichtung → Automatische Kalkulation einrichten*.
5. **Kalkulation im Beleg erzeugen.**
   - *Automatisch:* Erfassen Sie im **Verkaufsauftrag** eine Zeile mit dem gekennzeichneten **Artikel** und einer **Menge**. Beim Bestätigen der Menge wird die Kalkulation erstellt, auf **zertifiziert** gesetzt und der **Verkaufspreis** als Einheitspreis in die Zeile geschrieben.
   - *Manuell:* Wählen Sie auf der Belegzeile **Zeile → Funktion → Erstelle/Öffne Kalkulation** und die gewünschte **Kalkulationsvorlage**.
6. **(Bei Bedarf) Eigenschaften anpassen.** Öffnen Sie die **Kalkulation** und wählen Sie die Aktion **Eigenschaften bearbeiten**, um die Eigenschaftswerte zu ändern und die Kalkulation neu berechnen zu lassen.

## Einrichtung

Die Einrichtung ist der umfangreichste Teil dieser App und in Business Central vorzunehmen. Sie umfasst drei aufeinander aufbauende Bereiche: die **Materialeigenschaftskosten** (Kostenmatrix), die **Kalkulationsvorlage** (welche Herleitungsart eine Zeile verwendet) und die **automatische Kalkulation** am Artikel. Zusätzlich beschreibt dieser Abschnitt die mitgelieferte **Berechtigung**.

Alle drei fachlichen Herleitungsarten dieser App werden über **eine** neue Ausprägung des Feldes **Feldart** in der **Kalkulationsvorlage** gesteuert. Die App fügt der Feldart drei Werte hinzu:

| Feldart (Wert) | Erläuterung |
|---|---|
| **Materialeigenschaftskosten** | Wenn eine Vorlagenzeile diese Feldart erhält, dann ermittelt die Kalkulation den Zeilenwert aus den hinterlegten **Materialeigenschaftskosten**: Für jede Eigenschaft der zugeordneten **Materialart** wird der passende Kostensatz gesucht und aufsummiert. Ohne diese Feldart bleibt die Zeile bei ihrer bisherigen Herleitung. |
| **Belegeigenschaftswert nutzen** | Wenn gesetzt, dann übernimmt die Kalkulation den **numerischen** Wert einer im Beleg (Kalkulationskopf) hinterlegten Eigenschaft direkt als Zeilenwert. Es sind nur Eigenschaften vom Datentyp **Dezimal** oder **Ganzzahlig** zulässig; andernfalls bricht die Berechnung mit einer Meldung ab. |
| **Berechnungsformel verwenden** | Wenn gesetzt, dann berechnet die Kalkulation den Zeilenwert aus einer frei definierten **Berechnungsformel**, in der numerische Belegeigenschaften, Zahlen und die Operatoren `+ - * / ^` sowie Klammern kombiniert werden. Ist die Formel ungültig, wird die Berechnung mit einer Meldung abgebrochen. |

> Hinweis: Das Feld **Feldart** enthält daneben die bereits durch die Basis-App m+m Kalkulation definierten Ausprägungen. Nur die drei oben genannten Werte werden von dieser App ergänzt und gesteuert.

### Materialeigenschaftskosten einrichten

**Wer/wann:** Der Administrator oder Key-User richtet die Materialeigenschaftskosten **vor der ersten Kalkulation** ein. Sie sind die Kostenbasis, aus der die Feldart **Materialeigenschaftskosten** in der Kalkulationsvorlage (siehe unten sowie *Tägliche Arbeit*) ihren Zeilenwert bezieht.

**Einstieg:** Über die Suche die Liste **Materialeigenschaftskosten** öffnen (die Liste ist unter *Verwaltung* verfügbar und über die Suche auffindbar).

Die Liste bildet eine Matrix: Zu einer **Materialart** und einer ihrer **Eigenschaften** wird für einen konkreten **Wert** – oder für einen Wertebereich von **Wert** bis **Bis Wert** – ein **Kostensatz** hinterlegt.

| Feld | Erläuterung |
|---|---|
| **Materialartencode** | Wenn gesetzt, dann gilt der Kostensatz nur für Kalkulationen von Artikeln dieser **Materialart**; die Auswahl erfolgt aus den in m+m Material Properties gepflegten Materialarten. Bleibt das Feld leer, greift der Satz materialartenübergreifend für die angegebene Eigenschaft. |
| **Eigenschaftscode** | Wenn gesetzt, dann bezieht sich der Kostensatz auf diese **Eigenschaft** der Materialart (Pflichtfeld). Die Auswahl erfolgt aus den im System hinterlegten Eigenschaften. Damit wird festgelegt, welche Eigenschaft den Kostenbeitrag steuert. |
| **Wert** | Wenn gesetzt, dann greift der Kostensatz für genau diesen Eigenschaftswert. Bei Eigenschaften mit hinterlegter Wertliste (**Verwende Eigenschaftswerte** = Ja) kann nur aus den gültigen Eigenschaftswerten gewählt werden. Bei numerischen oder Datums-Eigenschaften bildet **Wert** die Untergrenze eines Bereichs. |
| **Bis Wert** | Wenn gesetzt, dann definiert **Wert** bis **Bis Wert** einen **Bereich**: Der Kostensatz greift, wenn der Eigenschaftswert des Belegs innerhalb dieses Bereichs liegt. **Bis Wert** muss größer als **Wert** sein, sonst erscheint die Meldung „Kann nicht kleiner oder gleich dem ersten Wert sein.“ Bleibt **Bis Wert** leer, gilt der Satz nur für den exakten **Wert**. |
| **Kosten** | Wenn gesetzt, dann ist dies der Betrag, der bei einem Treffer in die Kalkulationszeile der Feldart **Materialeigenschaftskosten** einfließt. Mehrere zutreffende Eigenschaften werden addiert. |
| **Verwende Eigenschaftswerte** | Anzeigefeld: Wenn Ja, dann besitzt die zugehörige Eigenschaft eine feste Wertliste, und die Felder **Wert**/**Bis Wert** lassen nur diese gültigen Eigenschaftswerte zu; wenn Nein, sind freie numerische oder Datumsangaben und Bereiche möglich. Das Feld wird aus der Eigenschaft ermittelt und ist nicht editierbar. |

**Datentyp-abhängige Wertermittlung (aus dem Code):** Der Datentyp der Eigenschaft (**Datentyp**: Text, Dezimal, Ganzzahlig, Datum – definiert in m+m Material Properties) bestimmt, wie **Wert**/**Bis Wert** interpretiert werden:

- **Dezimal / Ganzzahlig:** Die Eingabe wird in einen **Numerischen Wert** konvertiert (bei Ganzzahlig gerundet). Bei der Kalkulation greift der Bereich **Wert ≤ Belegwert ≤ Bis Wert**.
- **Datum:** Die Eingabe wird als **Datumswert** interpretiert; die Kalkulation prüft **Wert ≤ Belegdatum ≤ Bis Wert**.
- **Text / Wertliste:** Es wird auf **Gleichheit** des Werts geprüft.

Lässt sich eine Eingabe nicht in den Datentyp der Eigenschaft konvertieren, erscheint die Meldung „(Wert) kann nicht konvertiert werden zu (Datentyp).“

**Prozessschritte (Aktivierung der Materialeigenschaftskosten in der Kalkulation):**

1. **Zuerst** in m+m Material Properties sicherstellen, dass **Materialart** und **Eigenschaft** (mit passendem **Datentyp**) existieren – ohne diese Stammdaten lassen sich keine Kostensätze anlegen.
2. **Danach** in **Materialeigenschaftskosten** je Kombination aus **Materialartencode**, **Eigenschaftscode** und **Wert**/**Bis Wert** die **Kosten** hinterlegen.
3. **Anschließend** in der **Kalkulationsvorlage** eine Zeile auf die **Feldart** **Materialeigenschaftskosten** setzen (siehe *Kalkulationsvorlage einrichten*).
4. **Schließlich** entsteht der Kostenbeitrag im Tagesgeschäft automatisch, sobald eine Kalkulation für einen Artikel dieser Materialart berechnet wird (siehe *Tägliche Arbeit → Kalkulation und Eigenschaften*).

Cross-Link: Die so hinterlegten Kosten werden wirksam über die Feldart **Materialeigenschaftskosten** in *Kalkulationsvorlage einrichten* und erscheinen im Ergebnis unter *Tägliche Arbeit*.

### Kalkulationsvorlage einrichten (Feldart)

**Wer/wann:** Der Administrator erweitert die vorhandene **Kalkulationsvorlage** der App m+m Kalkulation, bevor die Vorlage im Tagesgeschäft verwendet wird. Die Anlage einer Kalkulationsvorlage selbst ist in der Dokumentation der App m+m Kalkulation beschrieben; diese App fügt lediglich die Steuerung über die **Feldart** und drei zusätzliche Felder auf der Vorlagenzeile hinzu.

**Einstieg:** In **Kalkulationsvorlagen** die gewünschte Vorlage öffnen; die Zeilen werden im Unterformular der Vorlage bearbeitet. (Erreichbar über die Kalkulationsvorlagen der App m+m Kalkulation, nicht über eine eigene Seite dieser App.)

Auf der Vorlagenzeile stehen neben den Basisfeldern (u. a. **Feldart**, **Beschreibung**, **Wert**) die folgenden, durch diese App ergänzten Felder zur Verfügung. Sie sind jeweils nur editierbar, wenn die passende **Feldart** gewählt ist:

| Feld | Erläuterung |
|---|---|
| **Materialart** | Nur editierbar, wenn die Feldart **Materialeigenschaftskosten** ist. Wenn gesetzt, dann werden bei der Berechnung nur die Materialeigenschaftskosten dieser **Materialart** herangezogen; die Auswahl erfolgt aus den Materialarten aus m+m Material Properties. Wird die Feldart wieder von **Materialeigenschaftskosten** weggeschaltet, leert das System diesen Eintrag automatisch. |
| **Belegeigenschaftscode** | Nur editierbar, wenn die Feldart **Belegeigenschaftswert nutzen** ist. Wenn gesetzt, dann übernimmt die Zeile den numerischen Wert dieser Belegeigenschaft direkt. Auswählbar sind ausschließlich Eigenschaften vom Datentyp **Dezimal** oder **Ganzzahlig**. Beim Wegschalten der Feldart wird der Eintrag automatisch geleert. |
| **Berechnungsformel** | Nur editierbar, wenn die Feldart **Berechnungsformel verwenden** ist. Wenn gesetzt, dann berechnet die Zeile ihren Wert aus dieser Formel. Über die Assistenzfunktion (AssistEdit) am Feld öffnet sich der Formeleditor der App m+m Material Properties, in dem Eigenschaftscodes, Zahlen, Klammern und die Operatoren `+ - * / ^` zusammengestellt werden. Beim Wegschalten der Feldart wird die Formel automatisch geleert. |

**Wichtig – abhängige Feldpflege (aus dem Code):** Ändert der Anwender die **Feldart** einer Zeile weg von einer der drei App-Ausprägungen, dann setzt das System das jeweils zugehörige Detailfeld (**Materialart**, **Belegeigenschaftscode** oder **Berechnungsformel**) automatisch zurück, damit keine widersprüchlichen Angaben stehen bleiben.

**Prozessschritte:**

1. **Zuerst** die Zeile in der Kalkulationsvorlage anlegen und die **Feldart** wählen.
2. **Danach** – je nach Feldart – die **Materialart**, den **Belegeigenschaftscode** oder die **Berechnungsformel** pflegen.
3. **Anschließend** die Vorlage im Beleg verwenden; die gewählte Feldart bestimmt, woher der Zeilenwert bei der Berechnung kommt (siehe *Tägliche Arbeit*).

### Automatische Kalkulation einrichten

**Wer/wann:** Der Administrator kennzeichnet einzelne **Artikel** dafür, dass ihr **Verkaufspreis** beim Erfassen einer Verkaufszeile automatisch aus einer Kalkulation ermittelt wird. Dies setzt voraus, dass für den Artikel bzw. die Debitor-/Artikelkonstellation eine **Standard-Kalkulationsvorlage** in der App m+m Kalkulation eingerichtet ist.

**Einstieg:** **Artikel** (Liste) → **Artikelkarte** öffnen → Infobox **Preise & Verkauf**.

| Feld | Erläuterung |
|---|---|
| **Automatisch kalkulieren** | Wenn aktiviert, dann wird beim Erfassen einer Verkaufszeile mit diesem Artikel automatisch eine Kalkulation erstellt bzw. wiederverwendet, zertifiziert und der resultierende **Verkaufspreis** als Einheitspreis in die Belegzeile geschrieben. Wenn deaktiviert, verhält sich der Artikel wie im Standard – der Preis wird nicht automatisch kalkuliert. |

**Prozessschritte (Ende-zu-Ende-Aktivierung):**

1. **Zuerst** in m+m Kalkulation eine **Standard-Kalkulationsvorlage** einrichten, die für den Artikel greift. Fehlt sie, meldet das System beim automatischen Lauf „Für Artikel (Nr.) konnte keine Kalkulationsvorlage ermittelt werden. Richten Sie eine Standard-Kalkulationsvorlage ein.“
2. **Danach** die Vorlage – falls Materialeigenschaftskosten einfließen sollen – gemäß *Kalkulationsvorlage einrichten* um die passende **Feldart** erweitern.
3. **Anschließend** auf der **Artikelkarte** das Kennzeichen **Automatisch kalkulieren** setzen.
4. **Schließlich** entsteht der Preis im Tagesgeschäft automatisch beim Erfassen der Belegzeile (siehe *Tägliche Arbeit → Automatische Kalkulation im Verkaufsbeleg*).

Cross-Link: Die operative Auslösung ist in *Tägliche Arbeit* und in *Typische Anwendungsfälle → Auto-Kalkulation im Verkaufsauftrag* beschrieben.

### Berechtigungen

Die App liefert den Berechtigungssatz **m+m Kalkulation mit Materialeigenschaften** mit. Er legt fest, welche Aktionen die Anwender in dieser App ausführen können: Er umfasst den Vollzugriff (Lesen, Ändern, Einfügen, Löschen) auf die Tabelle **Materialeigenschaftskosten** sowie die Ausführungsrechte für die Seite **Materialeigenschaftskosten**, den Dialog **Eigenschaften bearbeiten** und die zugehörigen Verarbeitungs-Codeunits. Ordnen Sie diesen Berechtigungssatz den Benutzern zu, die Materialeigenschaftskosten pflegen oder Eigenschaften einer Kalkulation bearbeiten sollen.

## Stammdaten

### Materialeigenschaftskosten

Die zentrale, von dieser App eingeführte Stammdatentabelle ist die Liste **Materialeigenschaftskosten**. Sie ist zugleich Einrichtungs- und Stammdatenobjekt: Sie beschreibt dauerhaft, welcher **Kostenbeitrag** aus welcher Kombination von **Materialart**, **Eigenschaft** und **Wert**(-bereich) entsteht. Die vollständige Feldbeschreibung, die Datentyp-Logik und der Anlageprozess sind in *Einrichtung → Materialeigenschaftskosten einrichten* dokumentiert.

**Wo die Werte wirken:** Die Datensätze werden bei jeder Kalkulation ausgewertet, deren Vorlagenzeile die **Feldart Materialeigenschaftskosten** trägt und deren Artikel eine passende **Materialart** besitzt. Der Kostenbeitrag erscheint dann als Zeilenwert in der **Kalkulation** (siehe *Tägliche Arbeit*).

### Artikel für Auto-Kalkulation kennzeichnen

Der Artikel ist der Stammsatz, an dem die automatische Kalkulation aktiviert wird. Das dafür ergänzte Feld **Automatisch kalkulieren** auf der **Artikelkarte** ist in *Einrichtung → Automatische Kalkulation einrichten* vollständig beschrieben. Administratoren pflegen dieses Kennzeichen pro Artikel; im Verkaufsbeleg entscheidet es darüber, ob der Preis automatisch kalkuliert wird.

> Die Materialarten und Eigenschaften selbst sind Stammdaten der App **m+m Material Properties** und werden dort gepflegt. Diese App verweist nur darauf.

## Tägliche Arbeit: Kalkulation und Eigenschaften

Diese Abschnitte werden durch die Einrichtung gesteuert: Die **Feldart** der verwendeten **Kalkulationsvorlage** (siehe *Einrichtung*) bestimmt, woher jede Zeile ihren Wert bezieht, die **Materialeigenschaftskosten** liefern die Kostenbeiträge, und das Artikelkennzeichen **Automatisch kalkulieren** entscheidet über den automatischen Ablauf. Die folgenden Bereiche beschreiben die Belegoberflächen, die diese App erweitert.

### Kalkulationskopf: Eigenschaften bearbeiten

Auf der **Kalkulation** (Kalkulationskopf) ergänzt die App die Aktion **Eigenschaften bearbeiten** (im Menüband unter den Prozess-Aktionen, zusätzlich als hervorgehobene Aktion) sowie eine Infobox, die die aktuellen **Eigenschaften** des Kalkulationskopfs anzeigt.

**Einstieg:** **Kalkulationen** (Liste) → **Kalkulation** öffnen → Aktion **Eigenschaften bearbeiten**.

Ablauf der Aktion **Eigenschaften bearbeiten** (aus dem Code):

1. Ist die Kalkulation **zertifiziert**, fragt das System: „Die Kalkulation (Nr.) ist zertifiziert. Möchten Sie sie auf ‚In Entwicklung‘ setzen, um die Eigenschaften zu bearbeiten?“ Nur nach Bestätigung wird der Status auf **In Entwicklung** gesetzt; andernfalls bricht die Aktion ab. Eine Kalkulation, die weder **zertifiziert** noch **In Entwicklung** ist, kann auf diesem Weg nicht bearbeitet werden (Meldung: „Nur zertifizierte Kalkulationen können auf diese Weise bearbeitet werden …“).
2. Besteht eine Verknüpfung zu einer **Verkaufszeile**, fragt das System: „Wollen Sie die Eigenschaftswerte der Kalkulation mit den aktuellen Eigenschaften der verbundenen Verkaufszeile aktualisieren?“ Bei Bestätigung werden die Eigenschaften der Verkaufszeile in den Kalkulationskopf übernommen.
3. Der Eigenschaften-Editor öffnet sich als Dialog **Eigenschaften bearbeiten**. Änderungen wirken direkt auf die Eigenschaften des Kalkulationskopfs.
4. Beim Schließen mit **OK** wird die Kalkulation **neu berechnet**. Beim Schließen mit **Abbrechen** (oder über das Fenster-Schließen-Symbol) werden alle Änderungen verworfen und der vorherige Stand wiederhergestellt.

Das Bearbeiten ist nur im Status **In Entwicklung** möglich; deshalb wird eine zertifizierte Kalkulation vor dem Editieren nach Rückfrage zurückgesetzt.

### Kalkulationszeilen: Belegeigenschaftscode und Berechnungsformel

Im Unterformular der **Kalkulation** (Kalkulationszeilen) ergänzt die App zwei Felder, die – analog zur Vorlage – abhängig von der **Feldart** der Zeile editierbar sind:

| Feld | Erläuterung |
|---|---|
| **Belegeigenschaftscode** | Nur editierbar, wenn die Zeile die Feldart **Belegeigenschaftswert nutzen** hat. Wenn gesetzt, dann liest die Zeile den numerischen Wert dieser Belegeigenschaft aus dem Kalkulationskopf und verwendet ihn als Zeilenwert. |
| **Berechnungsformel** | Nur editierbar, wenn die Zeile die Feldart **Berechnungsformel verwenden** hat. Wenn gesetzt, dann berechnet die Zeile ihren Wert aus der Formel. Über die Assistenzfunktion am Feld öffnet sich der Formeleditor, der Eigenschaftscodes des Kalkulationskopfs, Zahlen, Klammern und Operatoren anbietet. |

Das Feld **Materialart** der Zeile wird bei der Feldart **Materialeigenschaftskosten** gefüllt und ist in den Zeilen nicht editierbar; es dokumentiert, für welche Materialart der Kostenbeitrag ermittelt wurde.

**Wertermittlung bei der Berechnung (aus dem Code):** Beim Berechnen einer Zeile prüft die App die **Feldart** und ermittelt den Wert entsprechend:

- **Materialeigenschaftskosten:** Für jede Eigenschaft des Kalkulationskopfs, die zur **Materialart** der Zeile passt, wird der Kostensatz aus **Materialeigenschaftskosten** gesucht (exakter **Wert**, sonst numerischer Bereich **Wert ≤ x ≤ Bis Wert**, sonst Datumsbereich) und aufsummiert.
- **Belegeigenschaftswert nutzen:** Der **numerische** Wert der Belegeigenschaft wird direkt übernommen (nur Datentyp Dezimal/Ganzzahlig zulässig).
- **Berechnungsformel verwenden:** Die Formel wird ausgewertet, wobei Eigenschaftscodes durch ihre numerischen Werte ersetzt werden; unbekannte Codes werden als 0 eingesetzt.

Bevor die Zeilen berechnet werden, stellt die App sicher, dass der Kalkulationskopf die Belegeigenschaften seiner **primären Quelle** (der verknüpften Verkaufszeile) trägt, damit Zeilen der Feldart **Belegeigenschaftswert nutzen** und **Berechnungsformel verwenden** nicht 0 ergeben.

### Automatische Kalkulation im Verkaufsbeleg

Ist ein **Artikel** mit **Automatisch kalkulieren** gekennzeichnet (siehe *Einrichtung*), läuft beim Erfassen der Verkaufszeile automatisch folgender Ablauf – ohne dass der Anwender die Kalkulation manuell öffnet:

1. Der Anwender erfasst im **Verkaufsauftrag** (oder einem anderen Verkaufsbeleg) eine Zeile vom Typ **Artikel** und bestätigt die **Menge**.
2. Nur solange der Belegstatus **offen** ist, erzeugt bzw. verwendet die App eine **Kalkulation** für diese Zeile und ermittelt die zugehörige **Standard-Kalkulationsvorlage**.
3. Die Kalkulation wird berechnet und auf **zertifiziert** gesetzt.
4. Der resultierende **Verkaufspreis** wird – gerundet gemäß der Rundungsgenauigkeit aus der Finanzbuchhaltungseinrichtung – als **Einheitspreis** in die Verkaufszeile geschrieben.

Fehlt eine passende Standard-Kalkulationsvorlage, meldet das System dies (siehe *Einrichtung → Automatische Kalkulation einrichten*). Der automatische Lauf ist gegen Wiedereintritt gesichert und wird nur bei nicht-temporären Artikelzeilen ausgelöst.

## FAQ und Troubleshooting

### 1. Warum fließen keine Materialeigenschaftskosten in meine Kalkulation ein?
Prüfen Sie drei Punkte: Die Vorlagenzeile muss die **Feldart Materialeigenschaftskosten** haben, der Artikel muss eine **Materialart** besitzen, und es muss ein passender Datensatz in **Materialeigenschaftskosten** existieren (gleicher **Materialartencode**, **Eigenschaftscode** und ein passender **Wert** oder Bereich). Fehlt einer dieser Punkte, bleibt der Kostenbeitrag 0.

### 2. Warum kann ich das Feld „Materialart“ / „Belegeigenschaftscode“ / „Berechnungsformel“ in der Vorlage nicht ausfüllen?
Diese Felder sind jeweils nur editierbar, wenn die passende **Feldart** gewählt ist: **Materialart** bei **Materialeigenschaftskosten**, **Belegeigenschaftscode** bei **Belegeigenschaftswert nutzen** und **Berechnungsformel** bei **Berechnungsformel verwenden**. Setzen Sie zuerst die **Feldart**.

### 3. Was passiert, wenn ich die Feldart einer Zeile nachträglich ändere?
Das System leert automatisch das zur alten Feldart gehörende Detailfeld (**Materialart**, **Belegeigenschaftscode** oder **Berechnungsformel**), damit keine widersprüchlichen Angaben zurückbleiben. Sie müssen das Detailfeld für die neue Feldart neu pflegen.

### 4. Warum erhalte ich die Meldung „Bis Wert kann nicht kleiner oder gleich dem ersten Wert sein“?
Bei einem numerischen Bereich in **Materialeigenschaftskosten** muss **Bis Wert** echt größer als **Wert** sein. Korrigieren Sie den oberen Bereichswert oder lassen Sie **Bis Wert** leer, wenn der Satz nur für den exakten **Wert** gelten soll.

### 5. Warum erscheint „(Wert) kann nicht konvertiert werden zu (Datentyp)“?
Der eingegebene **Wert** oder **Bis Wert** passt nicht zum **Datentyp** der Eigenschaft (z. B. Text statt Zahl bei einer numerischen Eigenschaft). Geben Sie einen Wert im richtigen Datentyp ein.

### 6. Warum meldet das System, dass für eine Berechnungsformel nur numerische Belegeigenschaften erlaubt sind?
In einer **Berechnungsformel** und bei **Belegeigenschaftswert nutzen** dürfen nur Belegeigenschaften vom Datentyp **Dezimal** oder **Ganzzahlig** verwendet werden. Verweist die Formel auf eine Text- oder Datumseigenschaft, bricht die Berechnung mit dieser Meldung ab. Verwenden Sie ausschließlich numerische Eigenschaften.

### 7. Warum wird meine Berechnungsformel als ungültig gemeldet?
Die Formel enthält einen Ausdruck, der sich nicht auswerten lässt (z. B. fehlende Klammer oder unzulässige Zeichenfolge). Erlaubt sind Zahlen, Eigenschaftscodes und die Operatoren `+ - * / ^` mit Klammern. Nutzen Sie den Formeleditor über die Assistenzfunktion am Feld **Berechnungsformel**, um gültige Ausdrücke zusammenzustellen.

### 8. Warum kann ich die Eigenschaften einer Kalkulation nicht bearbeiten?
Das Bearbeiten über **Eigenschaften bearbeiten** ist nur im Status **In Entwicklung** möglich. Eine **zertifizierte** Kalkulation wird nach Rückfrage automatisch auf **In Entwicklung** gesetzt. Eine Kalkulation, die weder zertifiziert noch in Entwicklung ist, lässt sich auf diesem Weg nicht bearbeiten.

### 9. Warum wird beim Erfassen einer Verkaufszeile kein Preis automatisch kalkuliert?
Die automatische Kalkulation läuft nur, wenn der **Artikel** das Kennzeichen **Automatisch kalkulieren** trägt, die Zeile vom Typ **Artikel** ist und der Belegstatus **offen** ist. Ausgelöst wird der Lauf beim Bestätigen der **Menge**. Fehlt das Kennzeichen oder ist der Beleg bereits freigegeben, unterbleibt die automatische Kalkulation.

### 10. Warum erhalte ich „Für Artikel (Nr.) konnte keine Kalkulationsvorlage ermittelt werden“?
Für die automatische Kalkulation muss eine **Standard-Kalkulationsvorlage** für den Artikel (bzw. die Debitor-/Artikelkonstellation) in der App m+m Kalkulation eingerichtet sein. Richten Sie eine passende Standardvorlage ein, damit die automatische Kalkulation eine Vorlage findet.

## Typische Anwendungsfälle

### Auto-Kalkulation im Verkaufsauftrag

1. **Auslöser:** Der Innendienst erhält telefonisch eine Bestellung für einen Artikel, dessen Preis sich aus Materialeigenschaften ergibt (z. B. abhängig von einer Kundennummer oder einer Materialkennzahl).
2. **Einstieg in BC:** Der Anwender öffnet einen **Verkaufsauftrag** und erfasst eine Zeile vom Typ **Artikel** mit dem betreffenden **Artikel** und der **Menge**. Der Artikel ist über die **Artikelkarte** mit **Automatisch kalkulieren** gekennzeichnet.
3. **Kernablauf:** Beim Bestätigen der **Menge** erzeugt die App im Hintergrund eine **Kalkulation**, ermittelt die **Standard-Kalkulationsvorlage**, berechnet die Kalkulation, setzt sie auf **zertifiziert** und schreibt den ermittelten **Verkaufspreis** als Einheitspreis in die Zeile. Fließen Materialeigenschaftskosten ein, sind zuvor die Schritte aus *Einrichtung → Materialeigenschaftskosten einrichten* erforderlich.
4. **Abschluss:** Der Anwender sieht den automatisch gesetzten Preis in der Belegzeile und führt den Verkaufsauftrag im Standard weiter. Eine Nachbearbeitung der zugrundeliegenden Kalkulation ist bei Bedarf über *Eigenschaften einer Kalkulation anpassen* möglich.

### Eigenschaften einer zertifizierten Kalkulation anpassen

1. **Auslöser:** Nach Rückmeldung aus dem Vertrieb muss der Kalkulationspreis eines bereits kalkulierten Auftrags angepasst werden, weil sich eine Materialeigenschaft geändert hat.
2. **Einstieg in BC:** Der Anwender öffnet über **Kalkulationen** die betreffende **Kalkulation** und wählt die Aktion **Eigenschaften bearbeiten**.
3. **Kernablauf:** Da die Kalkulation **zertifiziert** ist, bestätigt der Anwender die Rückfrage, sie auf **In Entwicklung** zu setzen. Optional übernimmt er die aktuellen Eigenschaften der verknüpften **Verkaufszeile**. Im Dialog **Eigenschaften bearbeiten** passt er die Eigenschaftswerte an. Mit **OK** wird die Kalkulation **neu berechnet**; mit **Abbrechen** bleibt der bisherige Stand erhalten.
4. **Abschluss:** Der neu berechnete Wert steht in der Kalkulation zur Verfügung und – bei verknüpften Belegen – als Grundlage für den weiteren Verkaufsprozess.
