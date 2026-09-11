---
title: Anwenderhandbuch m+m Production Order Job Overview
---

# Anwenderhandbuch m+m Production Order Job Overview

Dieses Handbuch beschreibt die Bedienung der App **m+m Production Order Job Overview** (in der Oberfläche durchgängig als **FA-Arbeitsvorrat** bezeichnet) in Microsoft Dynamics 365 Business Central. Es richtet sich an Anwenderinnen und Anwender, die täglich am Arbeitsvorrat arbeiten, sowie an Key User und Administratoren, die die App einrichten. Alle Seiten-, Feld- und Aktionsbezeichnungen entsprechen der deutschen Oberfläche.

## Einleitung

Die App **FA-Arbeitsvorrat** erweitert die Fertigungsabwicklung um einen arbeitsplatzgruppenbezogenen Arbeitsvorrat für freigegebene Fertigungsaufträge. Sie bündelt die offenen und laufenden Arbeitsgänge einer **Arbeitsplatzgruppe** (bzw. eines **Arbeitsplatzes**) in einer einzigen Arbeitsliste und erlaubt es, den Bearbeitungsstatus direkt aus dieser Liste zu steuern: **Rüsten**, **Starten**, **Unterbrechen**, **Teilbeenden**, **Beenden** und **Erneut öffnen**. Zeit- und Mengenrückmeldungen werden über die Buchungsseite gebucht, Materialbewegungen können als **Umlagerung** vorbereitet werden, und alle Aktionen werden im Ereignisverlauf protokolliert.

**Zielgruppe.** Primäre Zielgruppe sind **operative Fertigungsanwender** – Werkerinnen und Werker, Schichtführerinnen und Schichtführer sowie Arbeitsvorbereiter, die Arbeitsgänge starten, rückmelden und beenden. Sekundär richtet sich das Handbuch an Key User und Administratoren, die die globale **FA-Arbeitsvorrat Einrichtung** und die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** pflegen.

**Typischer Prozessablauf.** Der Einstieg folgt einer festen Kette: **Arbeitsplatzgruppe wählen** (Pflichtfilter) → optional **Arbeitsplatz**, **Fertigungsauftrag** oder **Datum** eingrenzen → **Zeile auswählen** → **Prozessaktion ausführen** (Rüsten/Starten/Unterbrechen/Teilbeenden/Beenden) → bei Zeit- oder Mengenbuchung die Seite **FA-Arbeitsvorrat Buchung** abschließen. Vor der ersten Nutzung pflegen Administratoren die globale Einrichtung, je Arbeitsplatzgruppe die Arbeitsplatzgruppeneinrichtung sowie die Stammdaten **FA-Arbeitsvorrat Unterbrechungsgründe** und optional das Beschreibungsschema.

## Schnellstart für Anwender

Reihenfolge: zuerst die **Einrichtung** (durch Administrator/Key User), danach die Arbeitsliste, danach die Prozessaktionen.

### Einrichtung sicherstellen (einmalig, Voraussetzung)

1. Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorrat Einrichtung** und prüfen Sie die Vorgaben zu Reihenfolge, Aktualisierung nach Aktionen, Archivierung sowie die Ampelfarben.
2. Öffnen Sie die **Arbeitsplatzgruppenkarte** der betreffenden Arbeitsplatzgruppe und wählen Sie die Aktion **FA-Arbeitsvorrat Einrichtung**, um die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** zu pflegen (Zeitbuchung, Rüstaktivität, Umlagerung, Sortierung).
3. Legen Sie unter **FA-Arbeitsvorrat Unterbrechungsgründe** die benötigten Gründe an.

### Arbeitsvorrat aufrufen und Arbeitsgang bearbeiten

1. Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorrat**.
2. Wählen Sie im Feld **Arbeitsplatzgruppennr.** die Arbeitsplatzgruppe, für die Sie arbeiten. (Der **Arbeitsplatzgruppenname** wird automatisch angezeigt.)
3. Grenzen Sie optional über **Arbeitsplatznr.**, **FA-Nr.** und **Datum** weiter ein.
4. Führen Sie bei Bedarf **Daten aktualisieren** aus, damit die Zeilen neu zusammengestellt werden.
5. Prüfen Sie die markierte Zeile (Beschreibung, **Status**, **Vorheriger Arbeitsgang Status**, **Arbeitsgangnr.**, Mengen).
6. Falls für die Arbeitsplatzgruppe **Rüsten** aktiv ist: Aktion **Rüsten** ausführen (Status **Rüsten**).
7. Aktion **Starten** ausführen (Status **Gestartet**).
8. Falls unterbrochen werden muss: Aktion **Unterbrechen** ausführen und einen Eintrag aus **FA-Arbeitsvorrat Unterbrechungsgründe** wählen (Status **Unterbrochen**).
9. Für eine Teilmenge: Aktion **Teilbeenden** (Status **Teilbeendet**). Für den Abschluss: Aktion **Beenden** (Status **Beendet**).
10. Löst die Aktion eine Zeit- oder Mengenbuchung aus, schließen Sie die Seite **FA-Arbeitsvorrat Buchung** mit **OK** ab. Ist die **Zeitbuchung** auf **Keine** oder **Mengenabhängige Sollzeit** gesetzt, ist dabei zwingend eine **Menge** einzutragen.

> Die Schritte 6–10 entsprechen exakt dem Buchungs- und Meldeablauf (siehe **Rückmeldung und Buchung**) und werden in den **Typischen Anwendungsfällen** wiederholt.

### Einstieg in Auftragsmonitor und Historie

1. Über **Suchen** die Seite **Auftragsmonitor FA-Arbeitsvorrat** öffnen, um je Arbeitsplatzgruppe den letzten Zustand als Ampel zu sehen.
2. Aus der Zeile im **FA-Arbeitsvorrat** die Aktion **Ereignisverlauf** öffnen, um Rückmeldungen und Unterbrechungen nachzuvollziehen.

## Einrichtung

Die Einrichtung ist die Voraussetzung für die tägliche Arbeit und der umfangreichste Konfigurationsbereich der App. Sie besteht aus einer **globalen** Einrichtungskarte und einer **je Arbeitsplatzgruppe** gepflegten Einrichtung; darauf setzen mehrere Freischaltketten auf, die weiter unten als eigene Unterabschnitte („… einrichten") beschrieben sind.

### Globale Einrichtung (FA-Arbeitsvorrat Einrichtung)

**Einstieg:** über **Suchen** → **FA-Arbeitsvorrat Einrichtung**. Es handelt sich um eine unternehmensweite Einrichtungskarte (ein Datensatz je Mandant). Die Karte wird beim ersten Öffnen automatisch angelegt; ein Datensatz muss nicht manuell erzeugt werden. Konfiguriert wird sie durch den Administrator/Key User **vor** der ersten Nutzung des Arbeitsvorrats. Die hier hinterlegten Vorgaben steuern die Reihenfolgeplanung, das Neuladen der Zeilen nach Aktionen (siehe **Tägliche Arbeit**), das Umlagerungsverhalten sowie den **Auftragsmonitor FA-Arbeitsvorrat**.

Bereich **Allgemein**:

| Einrichtung | Erläuterung |
|---|---|
| Auftragsvorr.-Reihenfolge beachten | Wenn aktiviert, wird beim Sammeln der Zeilen die im Fertigungsauftrag hinterlegte Reihenfolge der Arbeitsgänge berücksichtigt; ohne Kennzeichen richtet sich die Anzeige allein nach der gewählten **Sortierung**. |
| Automatische Reihenfolgeanpassung | Wenn aktiviert, verschiebt die App bei Vergabe einer bereits belegten **Reihenfolge** die betroffenen Zeilen automatisch um eine Position nach hinten, sodass keine doppelten Reihenfolgenummern entstehen; ohne Kennzeichen bleibt die manuelle Vergabe unverändert. |
| Automatische Reihenfolge beim Beenden | Wenn aktiviert, werden beim **Beenden** eines Arbeitsgangs die verbleibenden offenen Zeilen automatisch neu von 1 aufwärts durchnummeriert; ohne Kennzeichen bleibt die bisherige Reihenfolge erhalten. |
| Zwangsfolge bei Arbeitsplänen | Wenn aktiviert, prüft die App beim **Starten**, ob der vorherige Arbeitsgang bereits rückgemeldet ist; fehlt die Rückmeldung, wird der Start mit der Meldung „Es befindet sich keine Rückmeldung zum vorherigen Arbeitsgang." verhindert. Ohne Kennzeichen darf ohne diese Prüfung gestartet werden. |
| FA-Arbeitsvorratzeilen aktualisieren nach Aktion | Wenn aktiviert, werden die Zeilen nach einer Prozessaktion sofort neu zusammengestellt, sodass der Anwender den aktuellen Stand sieht; ohne Kennzeichen bleibt die Liste bis zur nächsten Aktion **Daten aktualisieren** unverändert. Steuert, welche der folgenden Aktionsfelder überhaupt greifen. |
| FA-Arbeitsvorratzeilen für alle Aktionen aktualisieren | Wenn aktiviert, werden die Zeilen nach **jeder** Aktion neu geladen; ohne Kennzeichen greifen die einzelnen Aktionsfelder darunter selektiv. Nur bearbeitbar, wenn „aktualisieren nach Aktion" gesetzt ist. |
| FA-Arbeitsvorratzeilen nach Aktion rüsten aktualisieren | Wenn aktiviert, werden die Zeilen gezielt nach der Aktion **Rüsten** neu geladen. |
| FA-Arbeitsvorratzeilen nach Aktion starten (Bearbeitung) aktualisieren | Wenn aktiviert, werden die Zeilen gezielt nach der Aktion **Starten** neu geladen. |
| FA-Arbeitsvorratzeilen nach Aktion unterbrechen aktualisieren | Wenn aktiviert, werden die Zeilen gezielt nach der Aktion **Unterbrechen** neu geladen. |
| FA-Arbeitsvorratzeilen nach Aktion teilbeenden aktualisieren | Wenn aktiviert, werden die Zeilen gezielt nach der Aktion **Teilbeenden** neu geladen. |
| FA-Arbeitsvorratzeilen nach Aktion beenden aktualisieren | Wenn aktiviert, werden die Zeilen gezielt nach der Aktion **Beenden** neu geladen. |
| FA-Arbeitsvorratzeilen nach Aktion neu öffnen aktualisieren | Wenn aktiviert, werden die Zeilen gezielt nach der Aktion **Erneut öffnen** / **Auf Offen setzen** neu geladen. |
| Menge durch Restmenge in Umlagerung setzen | Wenn aktiviert, übernimmt die App beim Ermitteln der **Umlagerungszeilen** die noch offene Restmenge der Komponente als Mengenvorschlag; ohne Kennzeichen bleibt die Menge zunächst leer und muss manuell erfasst werden. |
| Arbeitsvorratszeilen durch Query sammeln | Wenn aktiviert, werden die Arbeitsvorratszeilen über die interne Abfrage der vorhandenen Zeilen ermittelt (schnellere Zusammenstellung); ohne Kennzeichen erfolgt die Sammlung über die vollständige Durchlaufmethode. |
| Beendete Zeilen archivieren | Legt fest, ob und wann beendete Zeilen archiviert werden. **Nie:** keine Archivierung; beendete Zeilen bleiben in den aktiven Listen. **Beim Beenden des Fertigungsauftrags:** sobald der Fertigungsauftrag den Status „Beendet" erhält, werden die zugehörigen Arbeitsvorratszeilen samt Ereignissen und Umlagerungszeilen ins Archiv verschoben (siehe **Historie und Archiv**). |

Bereich **Statusampel Add-In** (steuert den **Auftragsmonitor FA-Arbeitsvorrat**):

| Einrichtung | Erläuterung |
|---|---|
| Aktualisierungsintervall (Sekunde) | Legt fest, nach wie vielen Sekunden der **Auftragsmonitor FA-Arbeitsvorrat** die Kacheln automatisch neu einliest; ein kleiner Wert hält die Ampeln aktueller, erzeugt aber häufigere Abfragen (Mindestwert 1, Vorgabe 10). |
| Ampelfarbe 1 | Farbwert (Hex) für die erste Ampelstufe. Wenn gesetzt, erscheint der Arbeitsplatz im Monitor in dieser Farbe, sobald ein unterbrochener Arbeitsgang den Folgeprozess **nicht** freigibt (Vorgabe Rot). |
| Ampelfarbe 2 | Farbwert (Hex) für die zweite Ampelstufe. Wenn gesetzt, erscheint der Arbeitsplatz in dieser Farbe, wenn kein kritischer Laufstatus vorliegt und nur der letzte Fertigungsauftrag angezeigt wird (Vorgabe Gelb). |
| Ampelfarbe 3 | Farbwert (Hex) für die dritte Ampelstufe. Wenn gesetzt, erscheint der Arbeitsplatz in dieser Farbe, wenn ein Arbeitsgang aktiv **Gestartet** ist (Vorgabe Grün). |

Über die Aktion **Unterbrechungsgründe** öffnen Sie aus dieser Karte direkt die Stammdatenliste **FA-Arbeitsvorrat Unterbrechungsgründe** (siehe **Stammdaten**).

### Arbeitsplatzgruppeneinrichtung (FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung)

**Einstieg:** Öffnen Sie die **Arbeitsplatzgruppenkarte** (oder die Liste **Arbeitsplatzgruppen**), markieren Sie die betreffende Arbeitsplatzgruppe und wählen Sie die Aktion **FA-Arbeitsvorrat Einrichtung**. Existiert für die Arbeitsplatzgruppe noch keine Einrichtung, fragt die App „Einrichtung für Arbeitsplatzgruppe %1 ist nicht vorhanden. Soll diese angelegt werden?" und legt sie auf Bestätigung an. Diese Seite wird **nicht** über **Suchen** aufgerufen; sie ist immer an eine konkrete Arbeitsplatzgruppe gebunden.

Diese Einrichtung wird je Arbeitsplatzgruppe durch den Key User gepflegt und steuert unmittelbar das Verhalten des **FA-Arbeitsvorrats** und der Seite **FA-Arbeitsvorrat Buchung** für diese Arbeitsplatzgruppe: welche Aktionen sichtbar sind, wie Zeiten gemeldet werden, ob Material umgelagert wird und wie die Liste sortiert und gefiltert erscheint.

| Einrichtung | Erläuterung |
|---|---|
| Arbeitsplatzgruppenname | Anzeige des Namens der ausgewählten Arbeitsplatzgruppe (nur Anzeige, aus dem Stammsatz gelesen). |
| Unproduktiv | Wenn aktiviert, wird die Arbeitsplatzgruppe als unproduktiv gekennzeichnet; dies dient der Abgrenzung von Arbeitsgängen, die nur zur Meldung oder Steuerung dienen und keine produktive Menge rückmelden. |
| Mehrere Aufträge starten | Wenn aktiviert, dürfen an dieser Arbeitsplatzgruppe mehrere Arbeitsgänge gleichzeitig im Status **Gestartet** sein; ohne Kennzeichen verhindert die App den Start eines weiteren Auftrags, solange am selben Arbeitsplatz noch ein Auftrag gestartet oder unterbrochen ist. |
| Start nicht erforderlich | Wenn aktiviert, darf ohne vorheriges **Starten** direkt teilbeendet oder beendet werden; ohne Kennzeichen verlangt die App vor dem Beenden einen gestarteten Auftrag. Kann nicht gesetzt werden, solange die **Zeitbuchung** auf **Standard** steht. |
| Sortierung | Legt die Standardsortierung des Arbeitsvorrats fest. **Reihenfolge:** nach der vergebenen Arbeitsreihenfolge; **Status:** gruppiert nach Bearbeitungsstand; **FA-Artikel:** nach dem gefertigten Artikel; **Datum:** nach Startdatum/-zeit. Die Anwenderin kann die Sortierung im Arbeitsvorrat temporär überschreiben. |
| Zeitbuchung | Steuert, welche Zeitangaben in der Seite **FA-Arbeitsvorrat Buchung** bearbeitbar sind und wie die Zeit ermittelt wird. **Standard:** Start-/Endzeit werden genutzt; Zeiten werden aus dem Ereignis übernommen. **Keine:** Zeitfelder sind gesperrt, dafür ist eine **Menge** zwingend. **Sollzeit:** Rüstzeit und Bearbeitungszeit werden direkt erfasst, Datum/Uhrzeit bleiben fest. **Mengenabhängige Sollzeit:** die Zeit ergibt sich aus der gemeldeten Menge, eine **Menge** ist zwingend. **Manuell:** Rüstzeit und Bearbeitungszeit werden manuell gesetzt; bei aktivem „Startdatum/-zeit änderbar" können auch die Startwerte angepasst werden. |
| Nur Zeit melden | Wenn aktiviert, wird die Seite **FA-Arbeitsvorrat Buchung** bei der Rückmeldung nicht geöffnet; die Zeit wird direkt aus dem Ereignis gebucht, ohne Detailerfassung von Start-/Endzeit und Menge. Kann nur zusammen mit **Zeitbuchung** = **Standard** oder **Sollzeit** gesetzt werden. |
| Rüsten | Wenn aktiviert, wird im Arbeitsvorrat die Aktion **Rüsten** eingeblendet und ein eigener Rüst-Statuswechsel ermöglicht; ohne Kennzeichen entfällt der separate Rüstschritt. |
| Umlagerung | Wenn aktiviert, wird im Arbeitsvorrat die Aktion **Umlagerung** eingeblendet und beim **Unterbrechen** bzw. beim Abschließen werden Umlagerungszeilen ermittelt; ohne Kennzeichen findet keine Materialumlagerung statt (siehe **Materialumlagerung einrichten**). |
| Startdatum/-zeit änderbar | Wenn aktiviert, darf der Anwender in der Seite **FA-Arbeitsvorrat Buchung** Startdatum und Startzeit ändern; ohne Kennzeichen sind diese Felder gesperrt. |
| Direkte Suche deaktivieren | Wenn aktiviert, werden die Zeilen nach Auswahl der Arbeitsplatzgruppe **nicht** automatisch gesammelt; der Anwender muss bewusst **Daten aktualisieren** ausführen. Sinnvoll bei sehr großen Arbeitsvorräten, um unnötige Ladevorgänge zu vermeiden. |
| Verkaufsauftragsnr. anzeigen | Wenn aktiviert, blendet der Arbeitsvorrat die Felder zum Vertriebsbezug ein (**Verkaufsauftragsnr.**, **Verkaufsauftragszeilennr.**, **Zusteller**, **Zustellertransportart**); ohne Kennzeichen bleiben diese Spalten ausgeblendet. |
| Zeiten anzeigen | Wenn aktiviert, blendet der Arbeitsvorrat die Zeitfelder **Sollzeit**, **Gemeldete Zeit**, **Offene Zeit** und **Zeit inkl. Rüsten** ein; ohne Kennzeichen bleiben diese Spalten ausgeblendet. |

Zusätzlich vorhanden, in der Oberfläche jedoch ausgeblendet und ohne Wirkung auf die Kern-App: **Vorbelegung fertiggestellte Menge** (Optionswerte **(leer)** und **Vorheriger Arbeitsgang**). Dieses Feld ist als nicht sichtbares Vorbelegungskennzeichen angelegt und wird im Standardablauf nicht bearbeitet.

**Zeitbuchung-Verriegelungen (Validierung):** Die App erzwingt widerspruchsfreie Einstellungen: **Start nicht erforderlich** ist bei **Zeitbuchung = Standard** nicht zulässig, und **Nur Zeit melden** ist nur bei **Zeitbuchung = Standard** oder **Sollzeit** erlaubt.

#### Zeitbuchung und Rückmeldung einrichten

**Wer/wann.** Der Key User legt je Arbeitsplatzgruppe fest, wie Zeiten und Mengen gemeldet werden – **vor** der ersten Rückmeldung an diesem Arbeitsplatz. Konsumiert wird die Einstellung in der täglichen Arbeit beim **Starten**/**Teilbeenden**/**Beenden** und in der Seite **FA-Arbeitsvorrat Buchung** (siehe **Rückmeldung und Buchung**).

Freischaltschritte in Abhängigkeitsreihenfolge:

1. Öffnen Sie über die **Arbeitsplatzgruppenkarte** → Aktion **FA-Arbeitsvorrat Einrichtung** die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**.
2. Setzen Sie **Zeitbuchung** passend zum Arbeitsplatz: Wenn **Standard** gewählt ist, arbeitet der Anwender mit Start-/Endzeiten; wenn **Keine** oder **Mengenabhängige Sollzeit** gewählt ist, muss bei der Rückmeldung zwingend eine **Menge** erfasst werden.
3. Setzen Sie bei Bedarf **Rüsten**: Wenn aktiviert, erscheint im Arbeitsvorrat der zusätzliche Rüstschritt vor dem Starten.
4. Setzen Sie bei Bedarf **Nur Zeit melden**: Wenn aktiviert, entfällt die Buchungsseite; ohne Kennzeichen bestätigt der Anwender jede Rückmeldung über **FA-Arbeitsvorrat Buchung**.
5. Setzen Sie bei Bedarf **Startdatum/-zeit änderbar** und **Start nicht erforderlich** gemäß Arbeitsweise des Arbeitsplatzes.

**Operativer Abschluss:** In der täglichen Arbeit lösen **Starten** (nach vorherigem **Rüsten**), **Teilbeenden** und **Beenden** die Buchung aus; die Anwenderin schließt sie über **FA-Arbeitsvorrat Buchung** mit **OK** ab (siehe **Rückmeldung und Buchung**).

#### Materialumlagerung einrichten

**Wer/wann.** Der Key User aktiviert die Materialumlagerung je Arbeitsplatzgruppe, wenn an diesem Arbeitsplatz Komponenten zwischen Lagerorten/Lagerplätzen bewegt werden sollen, bevor oder während eine Rückmeldung erfolgt. Angewendet wird die Funktion in der täglichen Arbeit über die Aktion **Umlagerung** und die Seite **FA-Arbeitsvorrat Umlagerungszeilen** (siehe **Materialumlagerung**).

1. Prüfen Sie in der globalen **FA-Arbeitsvorrat Einrichtung** das Kennzeichen **Menge durch Restmenge in Umlagerung setzen**: Wenn aktiviert, schlägt die App bei der Ermittlung der Umlagerungszeilen die offene Restmenge der Komponente als Menge vor.
2. Aktivieren Sie in der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** das Feld **Umlagerung**: Wenn aktiviert, erscheint im Arbeitsvorrat die Aktion **Umlagerung**, und beim **Unterbrechen** werden – falls noch nicht vorhanden – die Umlagerungszeilen automatisch gesammelt.
3. Stellen Sie sicher, dass die betroffenen Artikel, Lagerorte und Lagerplätze in Business Central gepflegt sind (Voraussetzung für die Verfügbarkeitsprüfung in den Umlagerungszeilen).

**Operativer Abschluss:** Über die Aktion **Umlagerung** öffnet der Anwender die **FA-Arbeitsvorrat Umlagerungszeilen**, kontrolliert Lagerort, Lagerplatz, Chargennr./Seriennr. und Menge und schließt die Materialbewegung mit der Rückmeldung ab (die Umlagerung wird beim Beenden gebucht, siehe **Rückmeldung und Buchung**).

#### Reihenfolgesteuerung einrichten

**Wer/wann.** Der Administrator legt in der globalen **FA-Arbeitsvorrat Einrichtung** fest, wie stark die Reihenfolge der Arbeitsgänge vorgegeben wird. Angewendet wird dies beim Sammeln und Sortieren der Zeilen sowie beim **Starten**.

1. **Auftragsvorr.-Reihenfolge beachten:** Wenn aktiviert, übernimmt die App die Reihenfolge aus dem Fertigungsauftrag; ohne Kennzeichen steuert die manuelle **Reihenfolge** je Zeile.
2. **Zwangsfolge bei Arbeitsplänen:** Wenn aktiviert, verhindert die App den **Start** eines Arbeitsgangs, solange der vorherige Arbeitsgang keine Rückmeldung hat.
3. **Automatische Reihenfolgeanpassung** und **Automatische Reihenfolge beim Beenden:** Wenn aktiviert, hält die App die Reihenfolgenummern automatisch lückenlos bzw. renummeriert beim Beenden.

**Operativer Abschluss:** In der täglichen Arbeit vergibt bzw. ändert die Anwenderin die **Reihenfolge** direkt in der Zeile; die konfigurierten Regeln greifen dann beim Sortieren, Starten und Beenden.

#### Personalpflicht einrichten

**Wer/wann.** Der Key User bestimmt je Arbeitsplatzgruppe, ob beim Starten eine Personalnummer angegeben werden muss. Der Schalter liegt auf der **Arbeitsplatzgruppenkarte** (siehe **Stammdaten – Arbeitsplatzgruppe**), die Wirkung tritt beim **Starten** ein.

1. Öffnen Sie die **Arbeitsplatzgruppenkarte** und setzen Sie **Personalnummer notwendig**: Wenn aktiviert, verlangt die App beim **Starten** eine gültige **Personalnummer**; fehlt sie, wird mit „Die Personalnummer muss für die Arbeitsplatzgruppe %1 angegeben werden." abgebrochen.
2. Stellen Sie sicher, dass die betreffenden Mitarbeitenden als aktive Mitarbeiter (ohne abgelaufenes Austrittsdatum) gepflegt sind; nur solche lassen sich in der Zeile als **Personalnummer** auswählen.

**Operativer Abschluss:** In der täglichen Arbeit trägt die Anwenderin die **Personalnummer** direkt in der Zeile ein (nur möglich, solange der Auftrag nicht **Gestartet** ist); beim Starten prüft die App die Pflicht.

## Stammdaten

Die Stammdaten der Kern-App sind bewusst schlank gehalten; sie steuern jedoch unmittelbar die tägliche Arbeit.

### Arbeitsplatzgruppe (Personalpflicht)

**Wer/wann.** Der Administrator pflegt je Arbeitsplatzgruppe auf der **Arbeitsplatzgruppenkarte**, ob Personalpflicht besteht. Die App erweitert die Standardkarte um genau ein Kennzeichen; alle übrigen Felder der Arbeitsplatzgruppenkarte sind Business-Central-Standard.

| Feld | Erläuterung |
|---|---|
| Personalnummer notwendig | Wenn aktiviert, muss beim **Starten** eines Arbeitsgangs dieser Arbeitsplatzgruppe eine gültige **Personalnummer** in der Zeile stehen; andernfalls wird der Start abgebrochen. Ohne Kennzeichen ist die Personalangabe freiwillig. |

Die Karte enthält außerdem die Aktion **FA-Arbeitsvorrat Einrichtung**, über die die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** geöffnet wird (siehe **Einrichtung**). Der Wert **Personalnummer notwendig** wirkt sich in der täglichen Arbeit über die Prüfung beim Starten und über die Bearbeitbarkeit des Feldes **Personalnummer** in der Zeile aus (Querverweis: **Personalpflicht einrichten**).

### FA-Arbeitsvorrat Unterbrechungsgründe

**Wer/wann.** Der Key User pflegt die Gründe, bevor Anwender Arbeitsgänge unterbrechen. Die Liste wird aus der globalen **FA-Arbeitsvorrat Einrichtung** über die Aktion **Unterbrechungsgründe** geöffnet und im Arbeitsvorrat bei der Aktion **Unterbrechen** ausgewählt. Der wichtigste Effekt liegt im Kennzeichen **Nächster Auftrag kann starten**, das steuert, ob ein Folgeschritt trotz Unterbrechung bereits beginnen darf, und die Ampelfarbe im **Auftragsmonitor FA-Arbeitsvorrat** bestimmt.

| Feld | Erläuterung |
|---|---|
| Code | Eindeutiger Kurzschlüssel des Unterbrechungsgrundes; erscheint in der Zeile und im Ereignisverlauf. |
| Beschreibung | Klartext des Grundes; wird dem Fertigungsmitarbeiter bei der Auswahl angezeigt. |
| Nächster Auftrag kann starten | Wenn aktiviert, darf trotz der Unterbrechung der nächste Arbeitsgang bereits starten, und der Arbeitsplatz erscheint im Auftragsmonitor in der zweiten Ampelstufe (Vorgabe Gelb); ohne Kennzeichen blockiert der Grund den Folgeprozess, und der Monitor zeigt die erste Ampelstufe (Vorgabe Rot). |

**Prozessschritte:** Zuerst je fachlichem Störgrund einen eigenen **Code** anlegen, danach die **Beschreibung** eindeutig formulieren und schließlich **Nächster Auftrag kann starten** nur bei bewusst freigegebenen Gründen aktivieren.

### FA-Arbeitsvorrat Beschreibung (Beschreibungsschema)

**Wer/wann.** Der Key User hinterlegt je Arbeitsplatzgruppe optional ein Schema, aus dem die App die **Beschreibung** einer Arbeitsvorratszeile zusammensetzt. Die Seite wird aus der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** über die Aktion **FA-Arbeitsvorrat Beschreibung** geöffnet. Ist kein Schema hinterlegt, bildet die App die Beschreibung standardmäßig aus FA-Nr., FA-Zeilennr. und Arbeitsgangnr.

| Feld | Erläuterung |
|---|---|
| Reihenfolge | Bestimmt, in welcher Reihenfolge die Bestandteile zur Beschreibung zusammengesetzt werden; die Zeilen werden aufsteigend verarbeitet. |
| Präfix | Wenn gefüllt, wird dieser Text dem Feldinhalt vorangestellt (z. B. ein Kennbuchstabe). |
| Feldbeschreibung | Wenn aktiviert, wird zusätzlich die Bezeichnung des Quellfeldes vor den Wert gesetzt (z. B. „FA-Nr. 100123"); ohne Kennzeichen erscheint nur der Wert. |
| Feld | Legt fest, welcher Quellwert eingesetzt wird. Werte: **FA-Nr.**, **FA-Zeilennr.**, **Arbeitsgangnr.**, **Arbeitsgangbeschreibung**, **FA-Artikelbeschreibung**, **FA-Artikelbeschreibung 2**. Je Wert wird der entsprechende Inhalt des Arbeitsgangs bzw. Fertigungsauftrags übernommen. |
| Suffix | Wenn gefüllt, wird dieser Text hinter dem Feldinhalt angefügt. |

**Prozessschritte:** Zuerst je gewünschtem Bestandteil eine Zeile mit **Reihenfolge** anlegen, danach **Feld** wählen (und bei Bedarf **Feldbeschreibung** setzen), schließlich **Präfix**/**Suffix** ergänzen. Das Ergebnis erscheint anschließend im Arbeitsvorrat in der Spalte **Beschreibung** der betroffenen Arbeitsplatzgruppe.

## Tägliche Arbeit im FA-Arbeitsvorrat

Die Seite **FA-Arbeitsvorrat** ist die zentrale Arbeitsliste. Ihr Verhalten wird durch die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** (Sichtbarkeit von **Rüsten**, **Umlagerung**, Zeitfeldern und Vertriebsfeldern, Standardsortierung, Zeitbuchung) und durch die globale **FA-Arbeitsvorrat Einrichtung** (Reihenfolge, Aktualisierung nach Aktionen) gesteuert. Ohne Auswahl einer **Arbeitsplatzgruppe** kann die App keine Zeilen sammeln.

### Filter

Der Filterbereich oberhalb der Zeilenliste bestimmt, welche Arbeitsgänge zusammengestellt und angezeigt werden.

| Filterfeld | Erläuterung |
|---|---|
| Arbeitsplatzgruppennr. | Pflichtfilter. Wenn gesetzt, sammelt die App die offenen und laufenden Arbeitsgänge dieser Arbeitsplatzgruppe; ohne Angabe erscheint die Meldung „Keine Arbeitsplatzgruppe angegeben." und es werden keine Zeilen geladen. |
| Arbeitsplatzgruppenname | Wenn eine Arbeitsplatzgruppe gewählt ist, wird deren Name automatisch angezeigt (nur Anzeige). |
| Arbeitsplatznr. | Wenn gesetzt, werden die Zeilen zusätzlich auf diesen Arbeitsplatz eingegrenzt. |
| Arbeitsplatzname | Wenn ein Arbeitsplatz gewählt ist, wird dessen Name angezeigt (nur Anzeige). |
| FA-Nr. | Wenn gesetzt, werden nur Zeilen des angegebenen freigegebenen Fertigungsauftrags angezeigt. |
| Datum | Wenn gesetzt, werden die Zeilen nach dem Startdatum des Arbeitsgangs eingegrenzt. |
| Sortierung | Wenn gesetzt, überschreibt der Wert die Standardsortierung der Arbeitsplatzgruppeneinrichtung (**Reihenfolge**, **Status**, **FA-Artikel**, **Datum**). |
| Beendete ausblenden | Wenn aktiviert, werden Zeilen mit **Status = Beendet** ausgeblendet (beim Öffnen der Seite standardmäßig aktiv). |
| Offene ausblenden | Wenn aktiviert, werden Zeilen mit **Status = Offen** ausgeblendet. |
| Rückmeldung in Vorarbeitsgang | Wenn aktiviert, werden nur Zeilen angezeigt, deren vorheriger Arbeitsgang bereits eine Rückmeldung hat; ohne Kennzeichen werden auch Zeilen ohne Rückmeldung im Vorarbeitsgang gezeigt. |

**Parent-vor-Child.** Wählen Sie in der täglichen Arbeit stets **zuerst** die **Arbeitsplatzgruppennr.** und **anschließend** – optional – die **Arbeitsplatznr.**. Der Arbeitsplatz ist keine Pflichtangabe.

### Zeilenliste lesen

Die Zeilen enthalten deutlich mehr als Arbeitsgang und Menge. Zentrale Spalten:

| Feld | Erläuterung |
|---|---|
| Beschreibung / Beschreibung 2 | Zusammengesetzte Bezeichnung des Arbeitsgangs (siehe Beschreibungsschema) bzw. Zusatzzeile. |
| Reihenfolge | Arbeitsreihenfolge im Arbeitsvorrat; der interne Leerwert 999999 wird ausgeblendet. Eine Änderung setzt den Auftrag auf **Geplant** und passt – je Einrichtung – die übrigen Reihenfolgen automatisch an. |
| Status | Bearbeitungsstand des Arbeitsgangs (siehe Statuswerte unten). |
| Vorheriger Arbeitsgang Status | Zeigt den Rückmeldestand des vorherigen Arbeitsgangs. **keine Rückmeldung:** der Vorarbeitsgang wurde noch nicht rückgemeldet; **Rückmeldung vorhanden:** es existiert bereits eine Rückmeldung; **Beendet:** der Vorarbeitsgang ist abgeschlossen; **1. Arbeitsgang:** es gibt keinen vorherigen Arbeitsgang. |
| Arbeitsgangnr. | Arbeitsgang aus dem Arbeitsplan des Fertigungsauftrags. |
| Personalnummer | Zugeordnete Person; nur bearbeitbar, solange der Auftrag nicht **Gestartet** ist. Bei Personalpflicht (siehe Stammdaten) zwingend beim Starten. |
| Arbeitsplatznr. | Zugeordneter Arbeitsplatz; eine Änderung setzt den Auftrag auf **Geplant**. |
| Unterbrechungsgrundcode / Unterbrechungsgrundbeschreibung | Bei unterbrochenen Zeilen der gewählte Grund und dessen Beschreibung. |
| Startdatum / Startzeit | Geplanter bzw. gemeldeter Beginn des Arbeitsgangs. |
| Fertiggestellte Menge | Summe der bereits gebuchten Mengen (aus den Ereignissen berechnet). |
| FA Menge | Fertigungsmenge des Fertigungsauftrags (nur Anzeige). |
| Einheitencode | Mengeneinheit des Fertigungsartikels. |

Über **Zeiten anzeigen** (Einrichtung) erscheinen zusätzlich **Sollzeit**, **Gemeldete Zeit**, **Offene Zeit** und **Zeit inkl. Rüsten**; über **Verkaufsauftragsnr. anzeigen** die Vertriebsfelder **Verkaufsauftragsnr.**, **Verkaufsauftragszeilennr.**, **Zusteller** und **Zustellertransportart**. Weitere optionale, standardmäßig ausgeblendete Spalten sind die FA-Kopfdaten (**FA-Status**, **FA-Nr.**, **FA-Zeilennr.**, **FA-Artikelnr.**, **FA-Variantencode**, **FA-Artikelbeschreibung**/**2**, **Letzter Arbeitsgang**) sowie die Vor-/Nachgangsfelder (**Vorh. Arbeitsgang Art/Nr./Beschr.**, **Nächster Arbeitsgang Art/Nr./Beschr.**).

**Statuswerte (Spalte Status):**

- **Offen:** Arbeitsgang zusammengestellt, noch nicht geplant oder gestartet – keine Zeit- oder Mengenbuchung.
- **Geplant:** einer Person, einem Arbeitsplatz oder einer Reihenfolge zugeordnet, aber noch nicht in Arbeit.
- **Rüsten:** Rüstschritt läuft (nur bei aktiver Rüstaktivität); die anschließende Bearbeitung kann gestartet werden.
- **Gestartet:** Bearbeitung läuft; Folgebuchungen sind möglich; ein weiterer Start am selben Arbeitsplatz ist gesperrt, sofern „Mehrere Aufträge starten" nicht gesetzt ist.
- **Unterbrochen:** Bearbeitung pausiert mit hinterlegtem Unterbrechungsgrund; ein Abschluss ist bis zum Fortsetzen bzw. Beenden nicht möglich.
- **Teilbeendet:** eine Teilmenge wurde rückgemeldet; der Arbeitsgang bleibt zur weiteren Bearbeitung offen.
- **Beendet:** Arbeitsgang abgeschlossen; keine weiteren Mengen- oder Zeitänderungen; wird optional archiviert.

### Prozessaktionen

Die Aktionen in der Menüleiste (Bereich **Verarbeiten**) steuern den Statuswechsel und lösen bei Bedarf Buchungen aus:

- **Rüsten:** Nur sichtbar, wenn für die Arbeitsplatzgruppe die Rüstaktivität aktiv ist. Setzt den Arbeitsgang auf **Rüsten**.
- **Starten:** Setzt den Arbeitsgang auf **Gestartet**. Bei aktiver **Zwangsfolge bei Arbeitsplänen** wird geprüft, ob der Vorarbeitsgang rückgemeldet ist; bei Personalpflicht wird die **Personalnummer** geprüft; wird ein Arbeitsplatz mit Arbeitsplätzen genutzt, ist die **Arbeitsplatznr.** anzugeben.
- **Unterbrechen:** Öffnet – bei aktiver Umlagerung – zunächst die Sammlung der Umlagerungszeilen, verlangt die Auswahl eines **Unterbrechungsgrundes** und setzt den Arbeitsgang auf **Unterbrochen**; die Personalnummer wird dabei entfernt.
- **Teilbeenden:** Meldet eine Teilmenge zurück (Status **Teilbeendet**); der Arbeitsgang bleibt bearbeitbar.
- **Beenden:** Schließt den Arbeitsgang fachlich ab (Status **Beendet**). Wechsel aus **Offen**/**Geplant** (ohne „Start nicht erforderlich"), **Unterbrochen** oder **Teilbeendet** werden mit einer Rückfrage „Vorgang fortsetzen?" bestätigt.
- **Umlagerung:** Nur sichtbar bei aktiver Umlagerung. Öffnet die **FA-Arbeitsvorrat Umlagerungszeilen** des markierten Arbeitsgangs.
- **Auf Offen setzen:** Setzt den Arbeitsgang nach Rückfrage „FA-Arbeitsvorratzeile wieder auf Status ‚Offen' setzen?" zurück auf **Offen**.
- **Beleg anzeigen:** Öffnet den zugrunde liegenden Fertigungsauftrag passend zu dessen Status (simuliert, geplant, langfristig geplant, freigegeben oder beendet).
- **Ereignisverlauf:** Öffnet die Historie des markierten Arbeitsgangs (**FA-Arbeitsvorratereignisse**).
- **Daten aktualisieren:** Stellt die Zeilen neu zusammen und setzt die Standardsortierung.

**Statusregeln (Auszug).** Aus **Gestartet** kann nicht erneut gestartet werden („Auftrag wurde bereits gestartet!"); ein **Unterbrochener** Auftrag kann nicht ohne Fortsetzen beendet werden; ein bereits **Beendeter** Auftrag löst beim erneuten Beenden die Meldung „Auftrag wurde bereits beendet!" aus. Ohne „Start nicht erforderlich" ist ein Beenden aus **Offen**/**Geplant** nur nach Bestätigung „Auftrag wurde noch nicht gestartet! Vorgang fortsetzen?" möglich.

### FactBox Vorheriger & Nächster Arbeitsgang

Rechts neben der Zeilenliste zeigt die FactBox **Vorh. & Nächster Arbeitsgang** den direkt vorhergehenden und nachfolgenden Schritt zum markierten Datensatz. Sie hilft bei der Entscheidung, ob ein Arbeitsgang bereits gestartet werden darf oder ob Folgeprozesse vorzubereiten sind.

| Feld | Erläuterung |
|---|---|
| Vorh. Arbeitsgang Beschr. | Kurztext des direkt vorhergehenden Arbeitsgangs. |
| Nächster Arbeitsgang Beschr. | Kurztext des direkt folgenden Arbeitsgangs. |

## Rückmeldung und Buchung

Löst eine Aktion (**Starten** nach vorherigem **Rüsten**, **Teilbeenden**, **Beenden** oder **Unterbrechen**) eine Zeit- oder Mengenbuchung aus, öffnet die App – sofern in der Arbeitsplatzgruppeneinrichtung **Nur Zeit melden** nicht gesetzt ist – die Seite **FA-Arbeitsvorrat Buchung** als modalen Dialog. Die App prüft dabei die zeitliche Konsistenz: Das **Startdatum** darf nicht nach dem **Enddatum** liegen, und bei gleichem Datum darf die **Startzeit** nicht nach der **Endzeit** liegen. Welche Felder bearbeitbar sind, richtet sich nach der **Zeitbuchung** der Arbeitsplatzgruppe (siehe **Zeitbuchung und Rückmeldung einrichten**).

Bereich **Buchungszeitraum**:

| Feld | Erläuterung |
|---|---|
| Startdatum | Beginn des Arbeitsgangs; bearbeitbar nur, wenn „Startdatum/-zeit änderbar" gesetzt ist. |
| Startzeit | Beginnzeit; bearbeitbar nur bei „Startdatum/-zeit änderbar". |
| Enddatum | Abschlussdatum; bei Zeitbuchung **Standard** aus dem Ereignis, sonst gesperrt. |
| Endzeit | Abschlusszeit; Bearbeitbarkeit analog Enddatum. |
| Rüstzeit | Gerüstete Zeit; bearbeitbar bei Zeitbuchung **Sollzeit** und **Manuell**. |
| Bearbeitungszeit | Laufzeit; bearbeitbar bei Zeitbuchung **Sollzeit** und **Manuell**. |

Bereich **Mengen**:

| Feld | Erläuterung |
|---|---|
| Menge | Rückgemeldete Menge des Arbeitsgangs. Bei Zeitbuchung **Keine** und **Mengenabhängige Sollzeit** ist die Angabe zwingend; wird beim Schließen keine Menge erkannt, erscheint „Es wurde keine Menge angegeben." und die Buchung wird nicht abgeschlossen. |
| Gebuchte Menge | Bereits insgesamt gebuchte Menge des Arbeitsgangs (nur Anzeige). |

Bereich **Lagerort** (relevant vor allem beim **letzten Arbeitsgang**):

| Feld | Erläuterung |
|---|---|
| Lagerort | Ziel-Lagerort der Rückmeldung; bearbeitbar nur beim letzten Arbeitsgang. |
| Lagerplatzcode | Ziel-Lagerplatz der Rückmeldung; bearbeitbar nur beim letzten Arbeitsgang. |

Bereich **Informationen** (nur Anzeige, zum Gegenprüfen): **FA-Nr.**, **Artikelnr.**, **Variantencode**, **Beschreibung**, **Beschreibung 2**. Über die Aktion **Artikelverfolgungszeilen** öffnen Sie bei verfolgungspflichtigen Artikeln die Artikelverfolgung; danach wird die gemeldete **Menge** mit der erfassten Menge abgeglichen.

**Wirkung der Zeitbuchung (Zusammenfassung):**

1. **Standard:** Start-/Endzeit werden gemäß Einrichtung genutzt; Zeiten stammen aus dem Ereignis.
2. **Keine:** Zeitfelder gesperrt; **Menge** zwingend.
3. **Sollzeit:** **Rüstzeit** und **Bearbeitungszeit** werden direkt erfasst, Datum/Zeit fest.
4. **Mengenabhängige Sollzeit:** Zeit ergibt sich aus der Menge; **Menge** zwingend.
5. **Manuell:** **Rüstzeit** und **Bearbeitungszeit** manuell; bei „Startdatum/-zeit änderbar" auch Startwerte anpassbar.

### Buchungsablauf (Reihenfolge der Schritte)

Der Meldeablauf folgt einer festen Schrittfolge, die in **Schnellstart** und in den **Typischen Anwendungsfällen** wiederholt wird:

1. Zeile auf **FA-Arbeitsvorrat** markieren.
2. Optional **Rüsten** (Status **Rüsten**).
3. **Starten** (Status **Gestartet**). Bei aktiver Zwangsfolge wird die Rückmeldung des Vorarbeitsgangs geprüft.
4. Bei ausgelöster Buchung und deaktiviertem **Nur Zeit melden**: Seite **FA-Arbeitsvorrat Buchung** ausfüllen und mit **OK** schließen.
5. **Teilbeenden** (Teilmenge) und/oder **Beenden** (Abschluss).
6. Beim Beenden mit aktiver **Umlagerung** und vorherigem Status **Gestartet** wird zunächst die Materialumlagerung gebucht, danach die gemeldete Menge und Zeit.
7. Die App bucht das Istmeldungs-/Kapazitätsposten-Buch.-Blatt; es entstehen **Kapazitätsposten**, **Artikelposten** und – bei Umlagerung – **Lagerplatzposten**. Das Ereignis wird als **Gebucht** markiert.

**Ausgeblendete Buchungsseite (Nur Zeit melden).** Ist **Nur Zeit melden** aktiv, wird die Seite **FA-Arbeitsvorrat Buchung** übersprungen; ausgelöst durch dieselben Aktionen (Starten/Teilbeenden/Beenden) bucht die App die Zeit direkt aus den Ereigniswerten. Der Anwender bestätigt weiterhin die Aktion selbst; eine Mengen- oder Zeitkorrektur im Dialog entfällt.

**Teilmengen.** Teilrückmeldungen sind zulässig: Über **Teilbeenden** kann wiederholt eine Teilmenge gemeldet werden, ohne den Arbeitsgang abzuschließen. Ein vollständiger Mengenausgleich ist für den Abschluss nicht erforderlich.

### Rückmeldung ohne Start (Sonderfall)

Ist in der Arbeitsplatzgruppeneinrichtung **Start nicht erforderlich** gesetzt, kann direkt teilbeendet oder beendet werden, ohne zuvor zu starten. Die App bucht dann die gemeldete Menge beim Abschluss.

## Materialumlagerung

Bei aktiver **Umlagerung** (siehe **Materialumlagerung einrichten**) bereitet der Anwender über die Aktion **Umlagerung** oder beim **Unterbrechen** die Bewegung der Komponenten vor. Die Seite **FA-Arbeitsvorrat Umlagerungszeilen** listet je Komponente eine Zeile mit Ausgangs- und Zielort. Die Zeilen sind bearbeitbar, solange der Arbeitsgang im Status **Rüsten** oder **Gestartet** ist (bzw. in **Offen**/**Geplant**, wenn „Start nicht erforderlich" gesetzt ist).

| Feld | Erläuterung |
|---|---|
| Artikelnr. | Umzulagernder Artikel; standardmäßig aus der Fertigungsauftragskomponente vorbelegt. |
| Chargennr. | Wenn der Artikel chargenpflichtig ist, wird hier die Charge erfasst; über die Assist-Schaltfläche kann sie aus dem Bestand gewählt werden. |
| Seriennr. | Bei seriennummernpflichtigen Artikeln die zu bewegende Seriennummer. |
| Beschreibung | Bezeichnung der Komponente (nur Anzeige, aus der Komponente gelesen). |
| Restmenge | Aus Komponentenmenge abzüglich bereits erfasster und gebuchter Umlagerungen berechnete offene Menge; ändert sich, wenn die **Menge** einer Zeile angepasst wird. |
| Menge | Zu bewegende Menge; eine Änderung aktualisiert die Restmengen aller zugehörigen Zeilen. |
| Gebuchte Menge | Bereits gebuchte Umlagerungsmenge (nur Anzeige). |
| Einheitencode | Mengeneinheit der Komponente (nur Anzeige). |
| Von Lagerortcode / Von Lagerplatzcode | Ausgangs-Lagerort und -Lagerplatz; die Lagerplatzauswahl berücksichtigt Charge/Seriennummer und verfügbaren Bestand. |
| Verfügbar | Wenn grün, ist die benötigte Menge am Ausgangsort verfügbar; wenn rot, reicht der Bestand für die erfasste Menge nicht aus. |
| Nach Lagerortcode / Nach Lagerplatzcode | Ziel-Lagerort und -Lagerplatz der Bewegung. |

**Aktionen:** **Zeile teilen** erzeugt aus einer Zeile eine neue, um dieselbe Komponente auf mehrere Chargen, Seriennummern oder Lagerplätze aufzuteilen. **Lagerplatzinhalt** öffnet den Lagerplatzinhalt zum Artikel für die Bestandskontrolle. Die FactBoxen **Von Lagerort – Lagerplatzinhalt** und **Nach Lagerort – Lagerplatzinhalt** zeigen die Chargenbestände je Lagerplatz für Ausgangs- und Zielort.

Die vorbereiteten Umlagerungen werden beim **Beenden** des gestarteten Arbeitsgangs zusammen mit der Rückmeldung gebucht (siehe **Buchungsablauf**, Schritt 6/7).

## Auftragsmonitor und Ereignisverlauf

### Auftragsmonitor FA-Arbeitsvorrat

**Einstieg:** über **Suchen** → **Auftragsmonitor FA-Arbeitsvorrat**. Die Seite zeigt je Arbeitsplatzgruppe eine Ampelkachel und liest dafür die zuletzt geänderte Arbeitsvorratszeile der Gruppe. Die Ampel richtet sich nach deren Status und – bei Unterbrechung – nach dem Kennzeichen **Nächster Auftrag kann starten** des Grundes:

1. Ampelfarbe 3 (Vorgabe Grün): ein Arbeitsgang ist aktiv **Gestartet**; angezeigt werden FA-Nr. und **Fertiggestellte Menge**.
2. Ampelfarbe 1 (Vorgabe Rot): der letzte Arbeitsgang ist **Unterbrochen** und der Grund gibt den Folgeprozess **nicht** frei; angezeigt wird der **Unterbrechungsgrundcode**.
3. Ampelfarbe 2 (Vorgabe Gelb): kein kritischer Laufstatus; angezeigt wird der letzte Fertigungsauftrag.

Ein Klick auf die Werte einer Kachel öffnet direkt den zugehörigen **Freigegebenen FA**. Das **Aktualisierungsintervall** aus der globalen Einrichtung steuert die automatische Neueinlesung.

### Ereignisverlauf (FA-Arbeitsvorratereignisse)

**Einstieg:** aus dem **FA-Arbeitsvorrat** über die Aktion **Ereignisverlauf** (oder aus der Liste **FA-Arbeitsvorrat** über **Ereignisverlauf** je Fertigungsauftrag). Die schreibgeschützte Liste dokumentiert jede Aktion auf einer Arbeitsvorratszeile und dient der Rückverfolgung.

| Feld | Erläuterung |
|---|---|
| Erstellt von | Benutzerkennung des Auslösers der Aktion. |
| Datum / Zeit | Datum und Uhrzeit des Ereignisses. |
| Status | Status, der durch das Ereignis dokumentiert wurde (Rüsten/Gestartet/Unterbrochen/Teilbeendet/Beendet). |
| Unterbrechungsgrundcode / Unterbrechungsgrundbeschreibung | Bei Unterbrechungen der gewählte Grund und dessen Beschreibung. |
| Menge | Gebuchte bzw. rückgemeldete Menge dieses Ereignisses. |
| Bearbeitungszeit / Rüstzeit | Gebuchte Lauf- bzw. Rüstzeit des Ereignisses. |
| Arbeitsplatznr. / Arbeitsplatzgruppennr. | Zugeordneter Arbeitsplatz bzw. Arbeitsplatzgruppe. |

Ausgeblendet, aber für die Detailprüfung verfügbar: **Datum-Zeit geändert**, **Gebucht** (ob aus dem Ereignis bereits Buchungen entstanden sind), **Zeitbuchung**, die Vorstart-Zeitpunkte und die „geändert"-Kennzeichen der Zeiten. Über die Aktionen **Artikelposten**, **Lagerplatzposten** und **Kapazitätsposten** öffnen Sie die aus dem Ereignis entstandenen Posten zur Nachverfolgung. Die App verknüpft dazu jeden Posten über die Ereignisverbindung mit dem auslösenden Ereignis (Feld **FA-Arbeitsvorrat Ereignis** in den erweiterten Posten- und Buch.-Blatt-Tabellen).

## Fertigungsauftrag für den Arbeitsvorrat sperren

Über das erweiterte Feld **Gesperrt für FA-Arbeitsvorrat** am Fertigungsauftrag kann ein Auftrag von der Zusammenstellung im Arbeitsvorrat ausgeschlossen werden.

| Feld | Erläuterung |
|---|---|
| Gesperrt für FA-Arbeitsvorrat | Wenn aktiviert, werden die Arbeitsgänge dieses Fertigungsauftrags **nicht** in den **FA-Arbeitsvorrat** aufgenommen; ohne Kennzeichen erscheint der Auftrag normal in der Arbeitsliste. |

Die App verhindert das Setzen dieses Kennzeichens, solange zum Fertigungsauftrag noch mindestens eine Arbeitsvorratszeile den Status **Gestartet** oder **Unterbrochen** hat; in diesem Fall erscheint „Mindestens eine zugehörige Zeile im FA-Arbeitsvorrat befindet sich noch im Status ‚%1'!".

## Personalnummer in Buch.-Blättern und Posten

Für die Nachverfolgung, wer eine Rückmeldung erzeugt hat, ergänzt die App das Feld **Personalnummer** in den zugehörigen Buch.-Blättern und Posten:

| Feld | Erläuterung |
|---|---|
| Personalnummer (im Istmeldungs-Buch.-Blatt und Produktions-Buch.-Blatt) | Wenn gesetzt, wird die rückmeldende Person in der Buchungszeile geführt; nur gültige, aktive Mitarbeitende sind erlaubt, andernfalls erscheint „Diese Personalnummer existiert nicht." |
| Personalnummer (in den Kapazitätsposten) | Zeigt an, welche Person die gebuchte Kapazität rückgemeldet hat (nur Anzeige, aus der Buchung übernommen). |

## Historie und Archiv

Ist in der globalen **FA-Arbeitsvorrat Einrichtung** die Archivierung auf **Beim Beenden des Fertigungsauftrags** gestellt und erhält ein Fertigungsauftrag den Status „Beendet", verschiebt die App die zugehörigen Arbeitsvorratszeilen samt Ereignissen und Umlagerungszeilen ins Archiv. Die Seite **Arch. FA-Arbeitsvorratzeilen** dient dann als Nachweis abgeschlossener Vorgänge.

| Feld | Erläuterung |
|---|---|
| FA-Status / FA-Nr. / FA-Zeilennr. | Bezug zum archivierten Fertigungsauftrag. |
| Status | Archivierter Arbeitsstatus. |
| Arbeitsgangnr. / Arbeitsplatzgruppennr. / Arbeitsplatznr. | Arbeitsgang, Arbeitsplatzgruppe und Arbeitsplatz des Vorgangs. |
| Unterbrechungsgrundcode / Unterbrechungsgrundbeschreibung | Hinterlegter Unterbrechungsgrund. |
| Startdatum / Startzeit | Beginn des archivierten Vorgangs. |
| Reihenfolge | Reihenfolge im Arbeitsvorrat. |
| FA Menge / Fertiggestellte Menge | Ursprüngliche Fertigungsmenge und fertiggemeldete Menge. |
| Personalnummer | Beteiligte Person. |

Zur Detailprüfung stehen zusätzlich die Seiten **Arch. FA-Arbeitsvorratereignisse** und **Arch. FA-Arbeitsvorratsumlagerungszeilen** zur Verfügung; sie entsprechen inhaltlich den aktiven Listen, dienen aber nur der Nachverfolgung. Nutzen Sie diese Seiten, um zu klären, wer einen Arbeitsgang gestartet, unterbrochen oder beendet hat, welche Mengen und Zeiten gebucht wurden und welche Materialumlagerung vor der Rückmeldung vorbereitet oder verbucht wurde.

## Berechtigungen

Die App liefert einen Berechtigungssatz **MuM PJ Permission** aus. Er bestimmt die Berechtigungen für die Objekte der App und legt fest, welche Aktionen Anwenderinnen und Anwender im FA-Arbeitsvorrat sowie in dessen Einrichtung ausführen dürfen. Weisen Sie diesen Satz den Rollen zu, die mit dem Arbeitsvorrat arbeiten oder ihn administrieren.

## FAQ und Troubleshooting

### Warum sehe ich nach dem Öffnen des Arbeitsvorrats keine Zeilen?
Ohne **Arbeitsplatzgruppennr.** kann die App keine Zeilen sammeln (Meldung „Keine Arbeitsplatzgruppe angegeben."). Wählen Sie zuerst eine Arbeitsplatzgruppe. Ist in der Arbeitsplatzgruppeneinrichtung **Direkte Suche deaktivieren** aktiv, führen Sie zusätzlich **Daten aktualisieren** aus.

### Warum sind die Aktionen Rüsten oder Umlagerung nicht sichtbar?
Beide Aktionen hängen von der Arbeitsplatzgruppeneinrichtung ab: **Rüsten** wird durch das Feld **Rüsten** eingeblendet, **Umlagerung** durch das Feld **Umlagerung**. Ist das jeweilige Kennzeichen nicht gesetzt, bleibt die Aktion verborgen.

### Warum verlangt die Buchungsseite zwingend eine Menge?
Bei **Zeitbuchung = Keine** oder **Mengenabhängige Sollzeit** prüft die App beim Schließen der Seite **FA-Arbeitsvorrat Buchung**, dass eine Rückmeldemenge eingetragen wurde. Fehlt sie, erscheint „Es wurde keine Menge angegeben." und die Buchung wird nicht abgeschlossen.

### Warum kann ich einen Arbeitsgang nicht starten, obwohl der Auftrag ausgewählt ist?
Bei aktiver **Zwangsfolge bei Arbeitsplänen** verhindert die App den Start, solange der vorherige Arbeitsgang keine Rückmeldung hat („Es befindet sich keine Rückmeldung zum vorherigen Arbeitsgang."). Melden Sie zunächst den Vorarbeitsgang zurück. Ist außerdem **Personalnummer notwendig** gesetzt, muss zuvor eine gültige **Personalnummer** in der Zeile stehen.

### Warum lässt sich kein zweiter Auftrag am selben Arbeitsplatz starten?
Ist **Mehrere Aufträge starten** in der Arbeitsplatzgruppeneinrichtung nicht gesetzt, sperrt die App den Start eines weiteren Auftrags, solange am selben Arbeitsplatz noch ein Auftrag **Gestartet** oder **Unterbrochen** ist. Beenden oder unterbrechen Sie den laufenden Auftrag oder aktivieren Sie das Kennzeichen.

### Warum kann ich einen unterbrochenen Auftrag nicht direkt beenden?
Ein **Unterbrochener** Auftrag muss zunächst bestätigt fortgesetzt werden; erst nach der Rückfrage „Auftrag wurde unterbrochen! Vorgang fortsetzen?" ist der Abschluss möglich. Ebenso meldet ein bereits beendeter Auftrag „Auftrag wurde bereits beendet!".

### Warum kann ich den Fertigungsauftrag nicht für den FA-Arbeitsvorrat sperren?
Die App blockiert das Setzen von **Gesperrt für FA-Arbeitsvorrat**, wenn zum Auftrag noch mindestens eine Arbeitsvorratszeile den Status **Gestartet** oder **Unterbrochen** hat. Beenden Sie diese Zeilen zuerst.

### Warum zeigt der Auftragsmonitor rot?
Die erste Ampelstufe (Vorgabe Rot) erscheint, wenn der letzte relevante Arbeitsgang **Unterbrochen** ist und der zugehörige Unterbrechungsgrund **Nächster Auftrag kann starten** nicht freigibt. Wählen Sie bei Bedarf einen Grund mit gesetztem Freigabekennzeichen oder beenden Sie die Unterbrechung.

### Warum bleibt die Restmenge in den Umlagerungszeilen auf null oder ändert sich sofort?
Die App berechnet die **Restmenge** aus der Komponentenmenge abzüglich bereits erfasster und gebuchter Umlagerungen neu. Sobald Sie die **Menge** einer Zeile ändern, werden die Restmengen aller zugehörigen Zeilen aktualisiert. Ist zusätzlich **Menge durch Restmenge in Umlagerung setzen** aktiv, wird die offene Restmenge automatisch als Menge vorgeschlagen.

### Warum ist die Personalnummer in einer Zeile nicht mehr änderbar?
Die **Personalnummer** ist nur bearbeitbar, solange der Auftrag nicht **Gestartet** ist. Nach dem Start wird das Feld gesperrt; beim **Unterbrechen** wird die Personalnummer wieder entfernt und kann anschließend neu gesetzt werden.

## Typische Anwendungsfälle

### Schichtstart an einer Arbeitsplatzgruppe

**Auslöser.** Die Frühschicht beginnt, und der Schichtführer möchte sehen, welche Arbeitsgänge an einer Arbeitsplatzgruppe heute anstehen.

**Einstieg in BC.** Der Anwender öffnet über **Suchen** die Seite **FA-Arbeitsvorrat** und wählt die passende **Arbeitsplatzgruppennr.**.

**Kernablauf.**
1. Filter für **Arbeitsplatzgruppennr.** und optional **Datum** setzen; bei Bedarf **Arbeitsplatznr.** ergänzen.
2. **Daten aktualisieren**, damit die aktuellen Zeilen gesammelt werden.
3. Nach **Reihenfolge** oder **Datum** sortieren.
4. In der Zeile **Status**, **Vorheriger Arbeitsgang Status**, **Arbeitsgangnr.**, **FA-Nr.** und **Fertiggestellte Menge** prüfen.
5. Den ersten freigegebenen Arbeitsgang mit **Starten** in Arbeit nehmen (Status **Gestartet**).

**Abschluss.** Bei Rückfragen öffnet der Anwender mit **Beleg anzeigen** direkt den freigegebenen Fertigungsauftrag.

### Maschinenstörung mit Unterbrechung und Materialentscheidung

**Auslöser.** Während der Bearbeitung tritt eine Störung auf; der Mitarbeitende muss den Arbeitsgang stoppen und Material für den nächsten Schritt sichern.

**Einstieg in BC.** Der Anwender arbeitet bereits im **FA-Arbeitsvorrat** auf der Zeile des laufenden Arbeitsgangs (Status **Gestartet**).

**Kernablauf.**
1. In der Zeile prüfen, dass der **Status** = **Gestartet** ist.
2. Aktion **Unterbrechen** ausführen.
3. Bei aktiver **Umlagerung** werden die Umlagerungszeilen automatisch gesammelt bzw. geöffnet.
4. Einen Eintrag aus **FA-Arbeitsvorrat Unterbrechungsgründe** wählen (Status wechselt auf **Unterbrochen**).
5. In den **FA-Arbeitsvorrat Umlagerungszeilen** **Von Lagerortcode**, **Von Lagerplatzcode**, **Chargennr.** und **Menge** kontrollieren; das Feld **Verfügbar** muss grün sein.
6. Bei Bedarf mit **Zeile teilen** mehrere Chargen oder Lagerplätze vorbereiten.

**Abschluss.** Der Vorgang bleibt im **Ereignisverlauf** sichtbar. Im **Auftragsmonitor FA-Arbeitsvorrat** wechselt die Anzeige je nach Unterbrechungsgrund auf die erste (Rot) oder zweite (Gelb) Ampelstufe.

### Teilrückmeldung und Abschluss eines Arbeitsgangs

**Auslöser.** Es wurde zunächst nur ein Teil der Menge gefertigt; die Rückmeldung soll bereits im System erfolgen, der Arbeitsgang später abgeschlossen werden.

**Einstieg in BC.** Der Anwender arbeitet im **FA-Arbeitsvorrat** auf der gestarteten Zeile.

**Kernablauf.**
1. Zeile mit **Status = Gestartet** markieren.
2. Aktion **Teilbeenden** ausführen (Status **Teilbeendet**).
3. In der Seite **FA-Arbeitsvorrat Buchung** die **Menge** (und je nach **Zeitbuchung** die Zeiten) erfassen und mit **OK** schließen; bei **Zeitbuchung = Keine**/**Mengenabhängige Sollzeit** ist die **Menge** zwingend.
4. Später den restlichen Arbeitsgang mit **Beenden** abschließen (Status **Beendet**); erneut die **FA-Arbeitsvorrat Buchung** mit **OK** abschließen.
5. Ist es der **letzte Arbeitsgang**, im Bereich **Lagerort** der Buchungsseite **Lagerort** und **Lagerplatzcode** für die Einlagerung setzen.

**Abschluss.** Die gebuchten Mengen und Zeiten erscheinen im **Ereignisverlauf**; über **Kapazitätsposten**, **Artikelposten** und ggf. **Lagerplatzposten** lassen sich die entstandenen Posten prüfen.
