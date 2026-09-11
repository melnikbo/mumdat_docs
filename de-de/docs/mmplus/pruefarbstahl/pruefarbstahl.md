---
title: Anwenderhandbuch m+m Test Certificate Mgt. Prod. Order Job Steel
---

# Anwenderhandbuch m+m Test Certificate Mgt. Prod. Order Job Steel

## Einleitung

Diese Erweiterung verbindet die **Erw. Rückmeldung** des FA-Arbeitsvorrats im
Stahlumfeld mit der Prüfungsverwaltung (Modul **Prüfung** / **Prüfdaten
Einrichtung**). Sie sorgt dafür, dass zu den in der Rückmeldung erfassten **Chargen**
und **Restechargen** eines Vormaterials passende **Proben** in der zugehörigen
**Prüfung** entstehen – entweder automatisch bei der Chargenanlage oder auf Knopfdruck
durch den Anwender.

Fachlich schließt die App die Lücke zwischen zwei Prozessen: In der **Erw.
Rückmeldung** meldet der Anwender die gefertigten und aus dem **Vormaterial**
entstandenen Chargen zurück; parallel dazu muss jede relevante Charge qualitativ
dokumentiert werden. Ohne diese App müsste der Anwender die Probe manuell in der
**Prüfung** anlegen und die **Chargennr.** von Hand eintragen. Mit der App wird die
Probe direkt aus der zurückgemeldeten Chargenzeile erzeugt und mit deren **Chargennr.**
gefüllt.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender** in Fertigung und
Qualitätssicherung, die täglich am FA-Arbeitsvorrat und in der **Erw. Rückmeldung**
arbeiten: Sie melden Chargen zurück und dokumentieren sie über Proben. Sekundäre
Zielgruppe sind **Administratoren/Key-User**, die einmalig die **Prüfdaten
Einrichtung** vornehmen (insbesondere den Schalter **autom. Probenanlage**).

**Kurzer Prozessüberblick.**
1. Der Administrator hinterlegt in der **Prüfdaten Einrichtung** die Grundlagen der
   Prüfungsverwaltung (Nummernserien, automatische Probenerstellung) und aktiviert im
   Bereich **Erw. Rückmeldung** den Schalter **autom. Probenanlage**.
2. Voraussetzung im Beleg: Die FA-Arbeitsvorratszeile trägt eine **Prüfung Nr.** – nur
   dann besteht der Bezug zwischen Rückmeldung und Prüfung.
3. Der Anwender öffnet aus dem **FA-Arbeitsvorrat** die **Erw. Rückmeldung**, meldet
   das **Vormaterial** und die entstandenen **Chargen** bzw. **Restechargen** zurück.
4. Zu einer Chargenzeile entsteht eine **Probe** – automatisch (bei aktivem Schalter)
   oder über die Aktionen **Chargenprüfung erstellen** bzw. **Reste-Chargenprüfung
   erstellen**.
5. Der Anwender prüft und gibt die Proben in der **Prüfungskarte** frei (**Freigeben**);
   dieser Abschluss erfolgt im Basismodul **Prüfung**.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg von der leeren Einrichtung bis zur
ersten dokumentierten Charge. **Zuerst** die Einrichtung, **danach** die tägliche
Arbeit.

**A – Einrichtung (einmalig, durch den Administrator)**

1. **Prüfdaten Einrichtung** öffnen (über **Suchen** → „Prüfdaten Einrichtung").
2. Sicherstellen, dass die **Prüfungsnummernserie** hinterlegt ist und der Schalter
   **automatische Probenerstellung** den gewünschten Automatisierungsgrad vorgibt.
3. Im Bereich **Erw. Rückmeldung** den Schalter **autom. Probenanlage** setzen, wenn
   Proben ohne Zutun des Anwenders aus zurückgemeldeten Chargen entstehen sollen.
4. Prüfen, dass die betroffene FA-Arbeitsvorratszeile eine **Prüfung Nr.** trägt (wird
   über das Basismodul zwischen FA-Arbeitsvorrat und Prüfung gesetzt).

**B – Tägliche Arbeit (durch den operativen Anwender)**

5. **FA-Arbeitsvorrat** öffnen und die betreffende Zeile markieren.
6. Über die Aktion **Erw. Rückmeldung** die Rückmeldeseite zum **Vormaterial** öffnen.
7. Im Unterbereich **Chargen** die zurückgemeldete Chargenzeile wählen (**Chargennr.**
   muss gesetzt sein).
8. In der Aktionsgruppe **Prüfung** die Aktion **Chargenprüfung erstellen** wählen –
   die App legt die **Probe** in der verknüpften **Prüfung** an und füllt deren
   **Chargennr.** Bei aktivem Schalter **autom. Probenanlage** entfällt dieser Schritt,
   die Probe entsteht automatisch.
9. Die entstandenen Proben erscheinen in den Infoboxen **Chargenproben** bzw.
   **Restchargenproben** sowie in der **Prüfungskarte** unter **Proben**; dort füllt und
   gibt der Anwender sie über **Freigeben** frei.

## Einrichtung

Die zentrale Einrichtungsseite dieser Erweiterung ist die **Prüfdaten Einrichtung**.
Die App ergänzt diese Seite (ohne eine eigene Einrichtungsseite anzulegen) um den
Bereich **Erw. Rückmeldung** mit dem Schalter **autom. Probenanlage**. Da der Anwender in
Business Central **eine** zusammenhängende Seite sieht, dokumentiert dieses Kapitel die
gesamte **Prüfdaten Einrichtung** – Basisfelder und das Zusatzfeld dieser App
gemeinsam.

**Einstieg:** **Suchen** → „Prüfdaten Einrichtung". Die **Prüfdaten Einrichtung** ist
eine unternehmensweite Einrichtung (ein Datensatz je Mandant); ein übergeordneter
Stammbeleg existiert nicht, daher ist der Einstieg über **Suchen** korrekt.

**Wer richtet ein und wann.** Die **Prüfdaten Einrichtung** wird einmalig vor der
ersten produktiven Nutzung durch einen Administrator bzw. Key-User der
Qualitätssicherung vorgenommen und danach nur bei Prozessänderungen angepasst. Der für
diese App entscheidende Schalter **autom. Probenanlage** steuert unmittelbar, ob in der
**täglichen Arbeit** (Kapitel *Tägliche Arbeit am FA-Arbeitsvorrat*) Proben automatisch
entstehen.

### Prüfdaten Einrichtung – Bereich „Erw. Rückmeldung" (diese App)

Dieser Bereich wird durch die vorliegende Erweiterung hinzugefügt.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **autom. Probenanlage** | Wenn aktiviert, erzeugt das System beim Anlegen bzw. Ändern einer Chargen- oder Restechargenzeile in der **Erw. Rückmeldung** automatisch eine **Probe** in der zugehörigen **Prüfung** und übernimmt die **Chargennr.** der Zeile. Der Anwender muss die Aktionen **Chargenprüfung erstellen** / **Reste-Chargenprüfung erstellen** dann nicht mehr manuell auslösen. Ist der Schalter nicht gesetzt, entstehen Proben nur auf ausdrücklichen Klick des Anwenders. Voraussetzung in beiden Fällen: Die FA-Arbeitsvorratszeile trägt eine **Prüfung Nr.** und die Chargenzeile eine **Chargennr.** |

### Prüfdaten Einrichtung – Basisbereiche

Die folgenden Bereiche gehören zur Prüfungsverwaltung und erscheinen auf derselben
Seite. Sie werden hier mitdokumentiert, damit der Anwender die gesamte Seite ohne ein
weiteres Handbuch einrichten kann. Für die vorliegende App sind vor allem die Felder
**automatische Probenerstellung** und **Prüfungsnummernserie** relevant.

**Bereich „Allgemein"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **automatische Probenerstellung** | Wenn aktiviert, erzeugt das System beim Anlegen einer **Prüfung** bereits Proben in der aus der Vorlage vorgegebenen Anzahl; der Anwender muss die Proben nicht einzeln anlegen. Diese Basiseinstellung wirkt zusammen mit **autom. Probenanlage**: Ist Letzterer gesetzt, werden die automatisch angelegten Proben zusätzlich mit der **Chargennr.** aus der Rückmeldung gefüllt. |
| **Nur QS Benutzer können die Prüfung wieder öffnen** | Wenn aktiviert, dürfen ausschließlich als Qualitätssicherung gekennzeichnete Benutzer eine bereits abgeschlossene **Prüfung** erneut öffnen; andere Anwender können den Abschluss dann nicht rückgängig machen. |
| **Regel ignorieren, wenn eine manuelle Prüfung erstellt wird** | Wenn aktiviert, überspringt das System die automatische Regelbefüllung, sobald eine Prüfung manuell (aus Arbeitsgang oder Komponente) angelegt wird; der Anwender erhält dann eine leere Prüfung statt einer regelbasiert vorbefüllten. |
| **Warnen bevor der Status des FA geändert wird** | Wenn aktiviert, warnt das System vor einer Statusänderung des Fertigungsauftrags, falls noch Prüfungen mit einem anderen Prüfstatus als „Bestanden" offen sind; der Anwender kann so vor dem Weiterschalten reagieren. |
| **Beschriftung Vorgabewert 1** | Legt die frei wählbare Bezeichnung der ersten Vorgabewert-Spalte fest; die eingetragene Beschriftung erscheint anschließend in Prüfungen und im Prüfzeugnis. |
| **Beschriftung Vorgabewert 2** | Legt die Bezeichnung der zweiten Vorgabewert-Spalte fest; wirkt analog zu Vorgabewert 1 auf Prüfungen und Ausdruck. |
| **Chargennummer blockieren** | Wenn aktiviert, sperrt das System eine neu angelegte **Chargennr.** automatisch, bis die zugehörige Prüfung ein positives Ergebnis liefert; nicht geprüfte Chargen können damit nicht ungeprüft weiterverwendet werden. |
| **Probenwerte von Lieferantenchargenvorlage übertragen** | Wenn aktiviert, übernimmt das System vorhandene Probenwerte aus der Lieferantenchargenvorlage in die neue Probe; der Anwender spart die erneute Erfassung bereits bekannter Werte. |

**Bereich „Quarantäne Einrichtung"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Quarantäne-Lagerort** | Legt den Lagerort fest, auf den Artikel bei Auslösen der Quarantäne umgebucht werden; ohne Eintrag kann keine Quarantänebuchung erfolgen. |
| **Quarantäne Lagerplatzcode** | Bestimmt den Lagerplatz innerhalb des Quarantäne-Lagerorts, auf den quarantänebehaftete Artikel gebucht werden. |

**Bereich „Buchen"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **autom. Quarantänebuchung von Artikeln** | Wenn aktiviert, öffnet das System bei Auslösen von „Artikel in die Quarantäne verschieben" das Umlagerungsbuchblatt mit einer vorgeschlagenen Zeile, die der Anwender direkt buchen kann. |
| **Meldung bevor Quarantänebuchung** | Wenn aktiviert, fragt das System vor dem Verschieben in die Quarantäne beim Anwender nach; ohne den Schalter wird ohne Rückfrage gebucht. |
| **Quarantäne-Buchungszeilen sperren** | Wenn aktiviert, sperrt das System die erzeugten Quarantäne-Buchungszeilen gegen weitere Änderungen. |
| **Aktivieren Sie die Quarantänewarnung, bevor Sie den Probenwert validieren** | Wenn aktiviert, weist das System den Anwender darauf hin, dass der Prüfstatus der Herkunftszeile auf „Quarantäne" wechselt, bevor der Vorgabewert validiert wird. |

**Bereich „Erweiterte Lagerhaltung"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Quarantäne Zonencode** | Legt die Lagerzone für Quarantänebestände in Lagern mit erweiterter Lagerhaltung fest. |
| **Quarantäne-Lagerplatzartencode** | Bestimmt die Lagerplatzart für die Quarantäne in der erweiterten Lagerhaltung. |
| **Quarantäne-Lagerplatzartencode WE** | Legt die Lagerplatzart für den Wareneingang in die Quarantäne fest. |
| **Quarantäne-Lagerplatzart WA** | Legt die Lagerplatzart für den Warenausgang aus der Quarantäne fest. |
| **Quarantäne-Lagerplatzart Einlagerung** | Legt die Lagerplatzart für die Einlagerung in die Quarantäne fest. |
| **Quarantäne-Lagerplatzart Kommissionierung** | Legt die Lagerplatzart für die Kommissionierung aus der Quarantäne fest. |

**Bereich „Nummerierung"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Prüfvorlagennummernserie** | Bestimmt die Nummernserie für Prüfvorlagen; ohne Serie können keine Prüfvorlagen fortlaufend angelegt werden. |
| **Prüfungsnummernserie** | Bestimmt die Nummernserie für **Prüfungen**. Sie muss gesetzt sein, damit eine Prüfung mit **Prüfungsnr.** entsteht – und damit die aus der Rückmeldung erzeugten Proben überhaupt einer Prüfung zugeordnet werden können. |
| **Probennummern** | Bestimmt die Nummernserie für die einzelnen **Proben** innerhalb einer Prüfung. |
| **Prüfungsregelnummern** | Bestimmt die Nummernserie für Prüfungsregeln. |

**Bereich „Bericht"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Prüfzeugnis Nummernserie** | Bestimmt die Nummernserie für Prüfzeugnisbelege. |
| **Logoposition auf Belegen** | Legt fest, an welcher Position das Logo auf dem Prüfzeugnis erscheint. |
| **Bild-Referenzsymbol** | Definiert ein Symbol (bis zu 5 Zeichen), das im Bericht anzeigt, dass zu einem Probenwert Bilder hinterlegt sind; Vorgabewert ist „*". |
| **autom. Prüfzeugniserstellung** | Wenn aktiviert, erstellt das System den Prüfzeugnisbeleg automatisch, sobald die Voraussetzungen erfüllt sind. |

**Bereich „Aufgabenwarteschlange"**

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Aufgabenwarteschlange bei Fehlerfall neu starten** | Wenn aktiviert, startet das System die zugehörige Aufgabenwarteschlange nach einem Fehler automatisch neu. |
| **Aufgabenwarteschlange nach Nr. an Minuten neu starten** | Legt die Wartezeit bis zum Neustart in Minuten fest (z. B. 60 = eine Stunde; 1440 = ein Tag). |

### Automatische Probenanlage aus der Erw. Rückmeldung einrichten

Diese Erweiterung stellt genau eine Fähigkeit bereit, die mehrere Seiten
zusammenspielt: die **automatische Anlage von Proben** aus zurückgemeldeten Chargen.
Der Administrator richtet sie in der unten genannten Reihenfolge ein; der Nutzen
entsteht in der **täglichen Arbeit** (Kapitel *Tägliche Arbeit am FA-Arbeitsvorrat*).

**Prozessintro.** Konfiguriert wird die Fähigkeit vom Administrator/Key-User der
Qualitätssicherung, einmalig vor der ersten Rückmeldung. Sie greift, sobald der
operative Anwender Chargen in der **Erw. Rückmeldung** zurückmeldet.

**Einstieg:** **Suchen** → „Prüfdaten Einrichtung".

**Einrichtungsschritte in Abhängigkeitsreihenfolge:**

1. **Prüfung Nr. an der FA-Arbeitsvorratszeile sicherstellen (Voraussetzung).** Wenn
   die FA-Arbeitsvorratszeile eine **Prüfung Nr.** trägt, besteht der Bezug zwischen
   Rückmeldung und Prüfung; ohne diese Nummer wird keine Probe erzeugt (die
   Verarbeitung bricht ohne Meldung ab). Die **Prüfung Nr.** wird über das Basismodul
   zwischen FA-Arbeitsvorrat und Prüfung gesetzt.
2. **Prüfungsnummernserie hinterlegen.** Wenn in der **Prüfdaten Einrichtung** die
   **Prüfungsnummernserie** gesetzt ist, kann überhaupt eine Prüfung mit **Prüfungsnr.**
   entstehen, der die Proben zugeordnet werden; fehlt sie, schlägt die Zuordnung fehl.
3. **automatische Probenerstellung freigeben.** Wenn der Basisschalter **automatische
   Probenerstellung** aktiviert ist, legt das System zur Prüfung Proben in der
   vorgegebenen Anzahl an; auf diese Proben setzt die Chargenzuordnung dieser App auf.
4. **autom. Probenanlage aktivieren (diese App).** Wenn im Bereich **Erw. Rückmeldung**
   der Schalter **autom. Probenanlage** gesetzt ist, erzeugt das System die Probe
   automatisch beim Anlegen/Ändern der Chargen- bzw. Restechargenzeile und füllt deren
   **Chargennr.** – der Anwender muss keine Aktion mehr auslösen.

**Operativer Abschluss.** In der täglichen Arbeit entstehen die Proben nun automatisch
beim Rückmelden der Chargen. Ist der Schalter **autom. Probenanlage** bewusst nicht
gesetzt, löst der Anwender die Anlage manuell über **Chargenprüfung erstellen** bzw.
**Reste-Chargenprüfung erstellen** aus (siehe Kapitel *Tägliche Arbeit am
FA-Arbeitsvorrat*). Anschließend werden die Proben in der **Prüfungskarte** über
**Freigeben** abgeschlossen.

## Tägliche Arbeit am FA-Arbeitsvorrat

Die tägliche Arbeit findet in der **Erw. Rückmeldung** des FA-Arbeitsvorrats statt.
Diese Rückmeldeseite und ihre Unterbereiche gehören zum Stahl-Basismodul; die
vorliegende App ergänzt sie um die Spalte **Prüfungsnr.**, um Infoboxen mit Proben und
um die Aktionsgruppe **Prüfung**.

**Steuernde Einrichtung (Brücke zur Einrichtung).** Das Verhalten dieses Kapitels wird
in der **Prüfdaten Einrichtung** gesteuert: Der Schalter **autom. Probenanlage**
entscheidet, ob Proben automatisch beim Rückmelden entstehen; die **Prüfungsnummernserie**
und **automatische Probenerstellung** bestimmen, ob und wie die Prüfung samt Proben
angelegt wird. Details siehe Kapitel *Einrichtung* → *Automatische Probenanlage aus der
Erw. Rückmeldung einrichten*.

**Einstieg:** Öffnen Sie in **FA-Arbeitsvorrat** die betreffende Zeile und wählen Sie
die Aktion **Erw. Rückmeldung**. Es öffnet sich die Rückmeldeseite zum **Vormaterial**
mit den Unterbereichen **Chargen** und **Restechargen**.

### Erw. Rückmeldung – Spalte „Prüfungsnr."

Auf den drei Rückmeldebereichen (**Vormaterial**, **Chargen**, **Restechargen**)
ergänzt die App je eine schreibgeschützte Spalte.

| Feld | Erläuterung |
|------|-------------|
| **Prüfungsnr.** | Zeigt an, welcher **Prüfung** die Zeile über die FA-Arbeitsvorratszeile zugeordnet ist. Der Wert wird berechnet aus der **Prüfung Nr.** der zugehörigen FA-Arbeitsvorratszeile und ist nicht editierbar. Wenn hier eine Nummer steht, besteht der Bezug zur Prüfung und es können Proben zur Zeile erzeugt werden; ist die Spalte leer, fehlt die Zuordnung und die Aktionen zur Probenanlage bleiben wirkungslos. |

### Erw. Rückmeldung – Aktionsgruppe „Prüfung"

Die App fügt am Vormaterial-Rückmeldebereich die Aktionsgruppe **Prüfung** mit zwei
Aktionen hinzu.

| Aktion | Wirkung |
|--------|---------|
| **Chargenprüfung erstellen** | Erzeugt zur aktuell im Unterbereich **Chargen** markierten Chargenzeile eine **Probe** in der verknüpften **Prüfung** und füllt deren **Chargennr.** mit der **Chargennr.** der Zeile. Voraussetzung: Die Chargenzeile trägt eine **Chargennr.** und die FA-Arbeitsvorratszeile eine **Prüfung Nr.**; andernfalls passiert nichts. |
| **Reste-Chargenprüfung erstellen** | Erzeugt zur aktuell im Unterbereich **Restechargen** markierten Restechargenzeile eine **Probe** in der verknüpften **Prüfung** und füllt deren **Chargennr.** mit der **Chargennr.** der Restechargenzeile. Voraussetzungen wie bei **Chargenprüfung erstellen**. |

**Ablauf.** Öffnen Sie über die Aktion **Erw. Rückmeldung** die Rückmeldeseite,
markieren Sie im Unterbereich **Chargen** (bzw. **Restechargen**) die gewünschte Zeile
und wählen Sie in der Gruppe **Prüfung** die passende Aktion. Die App legt die Probe an
und stempelt die **Chargennr.** ein. Anschließend prüfen und dokumentieren Sie die
Probe in der **Prüfungskarte** (Aufruf über die Spalte **Prüfungsnr.** bzw. das
Basismodul **Prüfung**) und geben sie über **Freigeben** frei.

### Erw. Rückmeldung – Infoboxen

Die App zeigt am Vormaterial-Rückmeldebereich drei Infoboxen mit den vorhandenen
Proben. Sie dienen der Kontrolle, ob zu einer Charge bereits Proben existieren.

| Infobox | Erläuterung |
|---------|-------------|
| **Alle Einsatzmaterialproben** | Zeigt alle Proben zur **Chargennr.** des aktuellen Vormaterials – unabhängig von einer bestimmten Prüfung. Damit erkennt der Anwender, ob zu dieser Charge bereits an anderer Stelle Proben angelegt wurden. |
| **Chargenproben** | Zeigt die Proben, die zur **Chargennr.** der markierten Chargenzeile und zur zugeordneten **Prüfung** gehören. Aktualisiert sich, sobald über **Chargenprüfung erstellen** oder automatisch eine Probe entsteht. |
| **Restchargenproben** | Zeigt die Proben, die zur **Chargennr.** der markierten Restechargenzeile und zur zugeordneten **Prüfung** gehören. Aktualisiert sich analog bei **Reste-Chargenprüfung erstellen**. |

### Prüfung abschließen (Ausblick ins Basismodul)

Das Ausfüllen der Probenwerte, das Freigeben der einzelnen Proben und der Prüfung sowie
Ausdruck bzw. Versand eines Prüfzeugnisses erfolgen im Basismodul **Prüfung**
(Prüfungskarte, **Proben**, **Freigeben**). Diese Erweiterung erzeugt und verknüpft die
Proben; die weitere Bearbeitung nutzt die dortigen Funktionen. Öffnen Sie dazu die
**Prüfungskarte** über die berechnete **Prüfungsnr.** oder über die Suche nach der
Prüfung.

## FAQ und Troubleshooting

### 1. Warum entsteht beim Rückmelden einer Charge keine Probe?
Automatisch entstehen Proben nur, wenn in der **Prüfdaten Einrichtung** im Bereich
**Erw. Rückmeldung** der Schalter **autom. Probenanlage** gesetzt ist. Ohne den
Schalter müssen Sie die Aktion **Chargenprüfung erstellen** manuell auslösen.

### 2. Warum passiert nichts, wenn ich „Chargenprüfung erstellen" wähle?
Die Aktion bricht ohne Meldung ab, wenn die Chargenzeile keine **Chargennr.** hat oder
die zugehörige FA-Arbeitsvorratszeile keine **Prüfung Nr.** trägt. Prüfen Sie zuerst
diese beiden Werte.

### 3. Warum ist die Spalte „Prüfungsnr." in der Rückmeldung leer?
Die **Prüfungsnr.** wird aus der **Prüfung Nr.** der FA-Arbeitsvorratszeile berechnet.
Ist der Zeile keine Prüfung zugeordnet, bleibt die Spalte leer und es können keine
Proben erzeugt werden.

### 4. Kann ich die „Prüfungsnr." in der Rückmeldung ändern?
Nein. Die Spalte ist schreibgeschützt, weil sie ein berechneter Wert aus der
FA-Arbeitsvorratszeile ist. Die Zuordnung ändern Sie über die Prüfung Nr. der Zeile im
Basismodul.

### 5. Was ist der Unterschied zwischen „Chargenprüfung erstellen" und „Reste-Chargenprüfung erstellen"?
**Chargenprüfung erstellen** legt eine Probe zur markierten Zeile im Unterbereich
**Chargen** an, **Reste-Chargenprüfung erstellen** zur markierten Zeile im Unterbereich
**Restechargen** (Restecharge = verbliebene Restmenge einer Charge).

### 6. Welche Nummer bekommt die neue Probe?
Die Probe wird der **Prüfung** zugeordnet, die über die **Prüfung Nr.** der Zeile
ermittelt wird; die Probennummer stammt aus der in der **Prüfdaten Einrichtung**
hinterlegten Probennummernserie. Die **Chargennr.** der Rückmeldezeile wird in die
Probe übernommen.

### 7. Warum entstehen mehrere Proben statt einer?
Die App ruft die Standard-Probenerzeugung der Prüfung auf. Wie viele Proben dabei
entstehen, bestimmt die Prüfvorlage bzw. die Einstellung **automatische
Probenerstellung**. Die App füllt anschließend die zuletzt erzeugte Probe mit der
**Chargennr.**

### 8. Muss die Prüfung schon existieren, bevor ich zurückmelde?
Die FA-Arbeitsvorratszeile muss eine **Prüfung Nr.** tragen. Die eigentliche Prüfung
und ihre Proben werden beim Auslösen der Aktion bzw. bei automatischer Anlage über die
Standardfunktion der Prüfung erzeugt.

### 9. Ich sehe die neue Probe nicht sofort – woran liegt das?
Die Proben erscheinen in den Infoboxen **Chargenproben** / **Restchargenproben** und in
der **Prüfungskarte** unter **Proben**. Prüfen Sie, ob Sie die richtige Chargenzeile
markiert haben, da die Infoboxen nach **Chargennr.** und **Prüfung** filtern.

### 10. Wo gebe ich die Probe frei und drucke das Prüfzeugnis?
Freigabe der Proben und der Prüfung (**Freigeben**) sowie Ausdruck/Versand des
Prüfzeugnisses erfolgen in der **Prüfungskarte** des Basismoduls **Prüfung**. Diese
Erweiterung erzeugt nur die Proben und verknüpft sie mit der Charge.

## Typische Anwendungsfälle

### Anwendungsfall 1 – Charge nach der Rückmeldung dokumentieren (manuell)

**Auslöser.** Ein Fertigungsmitarbeiter hat eine Stahlcharge produziert und im
FA-Arbeitsvorrat zurückgemeldet; die Qualitätssicherung soll die Charge dokumentieren.

**Einstieg in BC.** Der Anwender öffnet den **FA-Arbeitsvorrat**, markiert die Zeile und
wählt die Aktion **Erw. Rückmeldung**. Die Rückmeldeseite zum **Vormaterial** öffnet
sich mit den Unterbereichen **Chargen** und **Restechargen**.

**Kernablauf.**
1. Im Unterbereich **Chargen** die zurückgemeldete Zeile mit gesetzter **Chargennr.**
   markieren.
2. In der Aktionsgruppe **Prüfung** die Aktion **Chargenprüfung erstellen** wählen.
3. Die App legt in der über **Prüfungsnr.** ermittelten **Prüfung** eine **Probe** an
   und übernimmt die **Chargennr.**
4. Die neue Probe erscheint in der Infobox **Chargenproben**.

**Abschluss.** Der Anwender öffnet die **Prüfungskarte**, füllt die Probenwerte und gibt
die Probe sowie die Prüfung über **Freigeben** frei. Ausdruck bzw. Versand des
Prüfzeugnisses erfolgen im Basismodul **Prüfung**.

### Anwendungsfall 2 – Durchgängige automatische Probenanlage

**Auslöser.** Die Qualitätssicherung möchte, dass zu jeder zurückgemeldeten Charge ohne
zusätzlichen Klick eine Probe entsteht.

**Einstieg in BC.** Einmalige Einrichtung über **Suchen** → „Prüfdaten Einrichtung".

**Kernablauf.**
1. In der **Prüfdaten Einrichtung** die **Prüfungsnummernserie** und **automatische
   Probenerstellung** sicherstellen.
2. Im Bereich **Erw. Rückmeldung** den Schalter **autom. Probenanlage** setzen.
3. Ab sofort erzeugt das System beim Anlegen bzw. Ändern einer Chargen- oder
   Restechargenzeile in der **Erw. Rückmeldung** automatisch eine **Probe** und füllt
   die **Chargennr.** – ohne die Aktionen manuell auszulösen.
4. Der operative Anwender meldet wie gewohnt im **FA-Arbeitsvorrat** über **Erw.
   Rückmeldung** zurück; die Proben erscheinen automatisch in **Chargenproben** bzw.
   **Restchargenproben**.

**Abschluss.** Die automatisch erzeugten Proben werden in der **Prüfungskarte** geprüft
und über **Freigeben** freigegeben.
