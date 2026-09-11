---
title: Anwenderhandbuch m+m Semifinished Items with Prod. Order Job Steel
---

# Anwenderhandbuch m+m Semifinished Items with Prod. Order Job Steel

## Einleitung

Die App m+m „Semifinished Items with Prod. Order Job Steel“ verbindet zwei bestehende m+m Erweiterungen für die Stahlfertigung: die Halbfertigteil-Logik aus m+m „Semifinished Items“ und den **FA-Arbeitsvorrat** aus m+m „Production Order Job Overview“. Sie sorgt dafür, dass beim Abschluss des letzten Arbeitsgangs eines Halbfertigartikels der zugehörige Auftrag im **FA-Arbeitsvorrat** automatisch mitgeführt und – je nach Einstellung – automatisch oder manuell zurückgemeldet wird.

Die App fügt dazu genau **einen** neuen Wert **Vom FA-Arbeitsvorrat** in die Option **Halbfertigteil letzter AG Option** am Arbeitsgang ein und reagiert im Hintergrund auf die Meldeereignisse des Halbfertigteil-Moduls. Eigene Seiten oder Karten bringt die App nicht mit; sie steuert das Zusammenspiel der beiden Basismodule. Alle im Handbuch genannten Seiten und Aktionen stammen daher aus den mitgelieferten Basismodulen, werden hier aber vollständig in dem Umfang beschrieben, den ein Anwender für diese Funktion benötigt.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender** in der Stahlfertigung, die am Arbeitsplatz Aufträge starten, unterbrechen, teilbeenden und beenden sowie Zeiten und Mengen zurückmelden. Sekundär angesprochen sind **Administratoren und Fertigungsleiter**, die die Arbeitsplatzgruppen und den letzten Arbeitsgang für den FA-Arbeitsvorrat einrichten.

**Kurzer Prozessüberblick:** Der Administrator kennzeichnet den letzten Arbeitsgang eines Halbfertigartikels und wählt für diesen Arbeitsgang die Rückmeldeart. Bei laufender Fertigung startet die App den Auftrag im FA-Arbeitsvorrat automatisch, sobald das Halbfertigteil in Bearbeitung geht. Der Abschluss erfolgt anschließend entweder **automatisch beim Buchen des Umlagerungseingangs** oder **manuell durch den Anwender im FA-Arbeitsvorrat**. Jede Statusänderung wird als Ereignis protokolliert.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zur ersten Rückmeldung – in der vom Programm erzwungenen Reihenfolge (zuerst Einrichtung, dann tägliche Arbeit):

1. **Einrichtung – Arbeitsgang kennzeichnen:** Öffnen Sie den **FA-Arbeitsplan** des freigegebenen Fertigungsauftrags (im freigegebenen Fertigungsauftrag über **Zeile → Arbeitsplan**). Setzen Sie im letzten Arbeitsgang das Kennzeichen **Halbfertigartikel** und wählen Sie unter **Halbfertigteil letzter AG Option** den Wert **Vom FA-Arbeitsvorrat**.
2. **Einrichtung – Arbeitsplatzgruppe:** Öffnen Sie die betreffende **Arbeitsplatzgruppe** (Arbeitsplatzgruppenkarte) und darüber die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**. Legen Sie die **Zeitbuchung** und das Startverhalten fest (siehe Einrichtung).
3. **FA-Arbeitsvorrat öffnen:** Rufen Sie über **Suchen** den **FA-Arbeitsvorrat** auf und wählen Sie die **Arbeitsplatzgruppennr.** – optional zusätzlich die **Arbeitsplatznr.** Es erscheinen alle zugehörigen Aufträge.
4. **Starten:** Die App startet den Auftrag beim Wechsel des Halbfertigteils in die Bearbeitung automatisch. Falls noch nicht gestartet, wählen Sie die Zeile und die Aktion **Starten**.
5. **Teilbeenden:** Für eine Teilmenge wählen Sie die Zeile und die Aktion **Teilbeenden**; der Status wechselt auf **Teilbeendet**.
6. **Beenden:** Ist der Arbeitsgang vollständig fertig, wählen Sie **Beenden**; der Status wechselt auf **Beendet**.
7. **Nachvollziehen:** Über **Ereignisverlauf** prüfen Sie die protokollierten Statuswechsel.

☞ Wenn Sie stattdessen die vollautomatische Rückmeldung wünschen, wählen Sie in Schritt 1 unter **Halbfertigteil letzter AG Option** den Wert **Beim Buchen des Umlagerungseingangs**. Dann übernimmt das System das Teilbeenden bzw. Beenden ohne manuelle Aktion (siehe „Wirkungsweise der Rückmeldung“).

## Einrichtung

Die Einrichtung umfasst zwei Ebenen: die **Kennzeichnung des letzten Arbeitsgangs** am Fertigungsauftrag (steuert, ob und wie der FA-Arbeitsvorrat einbezogen wird) und die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** je Arbeitsplatzgruppe (steuert Startverhalten und Zeitbuchung). Beide Ebenen greifen zusammen; die folgende H3 „Rückmeldung über den FA-Arbeitsvorrat einrichten“ beschreibt die vollständige Kette in Abhängigkeitsreihenfolge.

### Rückmeldung über den FA-Arbeitsvorrat einrichten

**Wer richtet ein und wann:** Diese Kette richtet der Administrator bzw. Fertigungsleiter **vor der ersten Rückmeldung** ein – die Arbeitsplatzgruppeneinrichtung einmalig je Arbeitsplatzgruppe, das Arbeitsgangkennzeichen je Fertigungsauftrags-Arbeitsplan. Angewendet wird die Einstellung später im Kapitel **Tägliche Arbeit am FA-Arbeitsvorrat**.

**Ablauf in Abhängigkeitsreihenfolge:**

1. **Zuerst – Halbfertigartikel kennzeichnen:** Setzen Sie im **FA-Arbeitsplan** des Fertigungsauftrags am letzten Arbeitsgang das Kennzeichen **Halbfertigartikel**. Wenn dieses Kennzeichen gesetzt ist, dann ist die Auswahl der **Halbfertigteil letzter AG Option** überhaupt erst möglich; ohne das Kennzeichen bleibt die Option gesperrt und der Arbeitsgang wird wie ein normaler Arbeitsgang ohne FA-Arbeitsvorrat-Anbindung behandelt.
2. **Danach – Rückmeldeart wählen:** Wählen Sie unter **Halbfertigteil letzter AG Option** den passenden Wert. Wenn Sie **Vom FA-Arbeitsvorrat** wählen, dann erfolgt der Abschluss ausschließlich manuell durch den Anwender im **FA-Arbeitsvorrat**; wenn Sie **Beim Buchen des Umlagerungseingangs** wählen, dann teilbeendet bzw. beendet das System den Auftrag automatisch beim Buchen des Umlagerungseingangs (siehe „Wirkungsweise der Rückmeldung“).
3. **Prüfregel Lagerort:** Beim Setzen der Option prüft das System, dass sich der **Lagerort** des Arbeitsgangs vom Lagerort der Arbeitsplatzgruppe unterscheidet. Wenn beide Lagerorte identisch sind, dann bricht das System die Auswahl mit einer Meldung ab; ist der Arbeitsplatzgruppe kein Lagerort zugeordnet, wird die Option automatisch zurückgesetzt. Ordnen Sie der Arbeitsplatzgruppe also einen von der Arbeitsgangzeile abweichenden Lagerort zu, bevor Sie die Rückmeldung über den FA-Arbeitsvorrat einrichten.
4. **Schließlich – Arbeitsplatzgruppe einrichten:** Legen Sie in der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** das Startverhalten und die **Zeitbuchung** fest (Felder siehe nächste H3). Diese Werte bestimmen, ob der Auftrag ausdrücklich gestartet werden muss und welche Zeiten beim Beenden gemeldet werden.

**Operativer Abschluss der Kette:** Nach dieser Einrichtung startet die App den betroffenen Auftrag im FA-Arbeitsvorrat automatisch, sobald das Halbfertigteil in Bearbeitung geht; der Anwender schließt ihn anschließend über die Aktionen **Teilbeenden** und **Beenden** im **FA-Arbeitsvorrat** ab (siehe Kapitel **Tägliche Arbeit am FA-Arbeitsvorrat**).

**Feld | Erläuterung** (letzter Arbeitsgang im **FA-Arbeitsplan**):

| Feld | Erläuterung |
|------|-------------|
| **Halbfertigartikel** | Wenn aktiviert, wird dieser Arbeitsgang als letzter Arbeitsgang eines Halbfertigartikels behandelt und die App bezieht ihn in den FA-Arbeitsvorrat ein; erst dann lässt sich die **Halbfertigteil letzter AG Option** setzen. Ohne das Kennzeichen bleibt der Arbeitsgang ohne FA-Arbeitsvorrat-Anbindung. |
| **Halbfertigteil letzter AG Option** | Legt fest, wie der letzte Arbeitsgang zurückgemeldet wird. **(leer):** Es greift das Standardverhalten des Basismoduls ohne automatische FA-Arbeitsvorrat-Rückmeldung. **Beim Buchen des Umlagerungseingangs:** Beim Buchen des Umlagerungseingangs teilbeendet bzw. beendet das System den zugehörigen Auftrag im FA-Arbeitsvorrat automatisch – ohne Aktion des Anwenders. **Vom FA-Arbeitsvorrat:** Das System meldet nicht automatisch zurück; der Anwender beendet den Auftrag manuell im FA-Arbeitsvorrat über **Teilbeenden**/**Beenden**. Diese App fügt genau diesen Wert hinzu. |

☞ Die Option ist nur wählbar, wenn zuvor **Halbfertigartikel** aktiviert wurde.

### FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung

**Wer richtet ein und wann:** Der Administrator richtet die Seite **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** je Arbeitsplatzgruppe **einmalig vor der ersten Meldung** ein. Sie steuert, wie sich Aufträge dieser Arbeitsplatzgruppe im **FA-Arbeitsvorrat** starten und melden lassen und wie Zeiten beim Beenden verbucht werden – also genau das Verhalten, das der Anwender in **Tägliche Arbeit am FA-Arbeitsvorrat** vorfindet.

**Einstieg:** Öffnen Sie in der **Arbeitsplatzgruppe** (Arbeitsplatzgruppenkarte) die Zeile bzw. Karte der gewünschten Arbeitsplatzgruppe und wählen Sie darüber den Aufruf zur **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**. Diese Seite ist bewusst nicht über **Suchen** erreichbar; sie wird immer aus der Arbeitsplatzgruppe heraus geöffnet.

**Einrichtung | Erläuterung** (Register „Allgemein“):

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Arbeitsplatzgruppenname** | Zeigt den Namen der Arbeitsplatzgruppe an, für die diese Einrichtung gilt; wird aus der Arbeitsplatzgruppe übernommen und dient der eindeutigen Zuordnung der Einrichtungswerte. |
| **Unproduktiv** | Wenn aktiviert, gilt die Arbeitsplatzgruppe als unproduktiv; ihre Zeiten fließen nicht als produktive Fertigungszeit in die Auswertung ein, wodurch die Rückmeldung sauber zwischen Wert schöpfender und nicht wertschöpfender Zeit trennt. |
| **Mehrere Aufträge starten** | Wenn aktiviert, kann der Anwender im FA-Arbeitsvorrat mehrere Aufträge dieser Arbeitsplatzgruppe gleichzeitig starten; ohne das Kennzeichen ist jeweils nur ein aktiv gestarteter Auftrag zulässig, was Fehlbuchungen bei paralleler Arbeit verhindert. |
| **Start nicht erforderlich** | Wenn aktiviert, kann der Anwender einen Auftrag direkt teilbeenden oder beenden, ohne ihn vorher zu starten; das beschleunigt die Meldung an Arbeitsplätzen ohne separate Startzeiterfassung. Dieses Kennzeichen ist mit der Zeitbuchung **Standard** nicht kombinierbar. |
| **Sortierung** | Legt die Standardsortierung der Auftragszeilen im FA-Arbeitsvorrat fest; eine passende Sortierung reduziert Suchaufwand am Arbeitsplatz. |
| **Zeitbuchung** | Legt fest, welche Zeiten beim Beenden in den Kapazitätsposten gebucht werden. **Standard:** Es werden die tatsächlich gemeldeten Start-/Endzeiten gebucht. **Keine:** Es wird keine Zeit gebucht; nur der Status wird fortgeschrieben. **Sollzeit:** Statt Ist-Zeiten werden die im Arbeitsplan hinterlegte Rüst- und Bearbeitungszeit gebucht. **Mengenabhängige Sollzeit:** Die Sollzeit wird anhand der gemeldeten Menge verteilt. **Manuell:** Der Anwender gibt die Zeiten selbst ein. Damit steuert dieses Feld unmittelbar, wie präzise und wie aufwandsarm die Rückmeldung erfolgt. |
| **Nur Zeit melden** | Wenn aktiviert, wird beim Beenden nur die Zeit, aber keine fertiggestellte Menge gebucht; sinnvoll an reinen Zeit-Arbeitsplätzen. Zulässig nur bei Zeitbuchung **Standard** oder **Sollzeit** – bei anderen Zeitbuchungsarten weist das System das Kennzeichen ab. |
| **Rüsten** (Rüstaktivität) | Wenn aktiviert, wird für diese Arbeitsplatzgruppe eine eigene Rüstphase geführt; der Anwender kann den Auftrag zunächst auf **Rüsten** setzen, bevor er startet, sodass Rüst- und Bearbeitungszeit getrennt erfasst werden. |
| **Startdatum/-zeit änderbar** | Wenn aktiviert, darf der Anwender beim Melden Startdatum und -zeit nachträglich ändern; das erlaubt die korrekte Nacherfassung, wenn die Rückmeldung zeitversetzt zur tatsächlichen Bearbeitung erfolgt. |
| **Vorbelegung fertiggestellte Menge** | Steuert die Vorbelegung der fertiggestellten Menge beim Beenden. **(leer):** Keine Vorbelegung. **Vorheriger Arbeitsgang:** Die Menge wird aus dem vorherigen Arbeitsgang übernommen, was Tippaufwand und Übertragungsfehler bei durchlaufenden Mengen vermeidet. (Feld standardmäßig ausgeblendet; bei Bedarf über die Seitenpersonalisierung einblenden.) |
| **Direkte Suche deaktivieren** | Wenn aktiviert, wird der direkte Sprung in den FA-Arbeitsvorrat für diese Arbeitsplatzgruppe unterbunden; der Anwender ruft die Ansicht dann ausschließlich über den regulären Weg auf, was in Umgebungen mit fester Arbeitsplatzsteuerung Fehlbedienungen verhindert. |
| **Verkaufsauftragsnr. anzeigen** | Wenn aktiviert, blendet der FA-Arbeitsvorrat die zugehörige Verkaufsauftragsnr. ein; der Anwender erkennt so direkt, für welchen Kundenauftrag er meldet. |
| **Zeiten anzeigen** | Wenn aktiviert, werden im FA-Arbeitsvorrat die Zeitfelder eingeblendet; ohne das Kennzeichen bleibt die Ansicht auf Status und Menge reduziert. |

☞ Die Kombinationsregeln (z. B. **Start nicht erforderlich** nicht mit **Zeitbuchung Standard**, **Nur Zeit melden** nur mit **Standard**/**Sollzeit**) werden vom System beim Speichern geprüft; eine unzulässige Kombination wird mit einer Feldmeldung abgewiesen.

## Wirkungsweise der Rückmeldung

Diese App verändert keine Seite sichtbar, sondern reagiert auf die Meldeereignisse des Halbfertigteil-Moduls. Je nach gewählter **Halbfertigteil letzter AG Option** ergeben sich zwei Abläufe. Beide werden durch die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** (Startverhalten, Zeitbuchung) mitgesteuert.

### Automatische Rückmeldung – Beim Buchen des Umlagerungseingangs

Ist am letzten Arbeitsgang die Option **Beim Buchen des Umlagerungseingangs** gewählt, läuft die Rückmeldung ohne Zutun des Anwenders:

1. Der Anwender bucht den **Umlagerungseingang** des Halbfertigteils.
2. Das System ermittelt die zugehörige **FA-Arbeitsvorratszeile**. Ist noch keine gestartete Zeile vorhanden, wird der Auftrag zunächst automatisch **gestartet**.
3. Ist der Arbeitsgang noch **in Bearbeitung**, wird der Auftrag auf **Teilbeendet** gesetzt; ist er vollständig abgeschlossen, auf **Beendet**.
4. Der Statuswechsel wird als Ereignis protokolliert (siehe **Ereignisprotokoll**).

☞ Bei dieser Option ist keine Aktion im FA-Arbeitsvorrat nötig; der Anwender kann das Ergebnis dort nur nachvollziehen.

### Manuelle Rückmeldung – Vom FA-Arbeitsvorrat

Ist die von dieser App bereitgestellte Option **Vom FA-Arbeitsvorrat** gewählt, meldet das System **nicht** automatisch zurück:

1. Geht das Halbfertigteil in Bearbeitung, **startet** die App den zugehörigen Auftrag im FA-Arbeitsvorrat automatisch, sofern er noch nicht **Gestartet** ist. Der Anwender findet ihn dadurch bereits als laufenden Auftrag vor.
2. Beim Buchen des Umlagerungseingangs unternimmt das System **bewusst nichts** – es überlässt Teilbeenden und Beenden dem Anwender.
3. Der Anwender meldet den Fortschritt selbst im **FA-Arbeitsvorrat** über die Aktionen **Teilbeenden** und **Beenden** (siehe **Tägliche Arbeit am FA-Arbeitsvorrat**).

☞ Wählen Sie **Vom FA-Arbeitsvorrat** immer dann, wenn der Bediener am Arbeitsplatz selbst über den Meldezeitpunkt und die Teilmengen entscheiden soll – etwa wenn der Umlagerungseingang und die tatsächliche Fertigstellung zeitlich auseinanderfallen.

## Tägliche Arbeit am FA-Arbeitsvorrat

Der **FA-Arbeitsvorrat** ist die zentrale Arbeitsansicht des operativen Anwenders. Er wird über settings der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** gesteuert (Startverhalten, Zeitbuchung, eingeblendete Spalten – siehe Einrichtung).

**Einstieg:** Rufen Sie den **FA-Arbeitsvorrat** über **Suchen** auf. Wählen Sie zunächst die **Arbeitsplatzgruppennr.** (übergeordneter Bereich); optional grenzen Sie zusätzlich über die **Arbeitsplatznr.** ein. Es erscheinen alle Aufträge der gewählten Arbeitsplatzgruppe.

**Aktionen im Menüband:**

| Aktion | Erläuterung |
|--------|-------------|
| **Rüsten** | Setzt den markierten Auftrag auf den Status **Rüsten**; nutzbar, wenn für die Arbeitsplatzgruppe die Rüstaktivität eingerichtet ist, um Rüstzeit vor der Bearbeitung getrennt zu erfassen. |
| **Starten** | Setzt den Auftrag auf **Gestartet** und beginnt die Zeiterfassung. Bei der Option **Vom FA-Arbeitsvorrat** wird dieser Schritt in der Regel bereits automatisch ausgeführt, sobald das Halbfertigteil in Bearbeitung geht. |
| **Unterbrechen** | Setzt den Auftrag auf **Unterbrochen**. Das System verlangt die Auswahl eines **Unterbrechungsgrundcode**; ohne Grund wird die Aktion abgebrochen. So bleibt jede Pause nachvollziehbar begründet. |
| **Teilbeenden** | Meldet eine Teilmenge zurück und setzt den Auftrag auf **Teilbeendet**; der Auftrag bleibt für weitere Meldungen offen. Teilmengen sind ausdrücklich zulässig – Sie müssen nicht bis zum Mengenausgleich warten. |
| **Beenden** | Schließt den Auftrag ab und setzt ihn auf **Beendet**; abhängig von der **Zeitbuchung** werden dabei Zeiten und ggf. die fertiggestellte Menge gebucht. |
| **Erneut öffnen** | Setzt einen bereits gemeldeten Auftrag wieder auf **Offen** zurück, um eine Korrektur zu ermöglichen. |
| **Umlagerung** | Öffnet die zugehörigen Umlagerungszeilen des Auftrags, sofern für die Arbeitsplatzgruppe die Umlagerung aktiv ist. |
| **Beleg anzeigen** | Öffnet den zugehörigen Fertigungsauftrag (je nach Status simuliert, geplant, fest geplant, freigegeben oder beendet) zur Einsicht. |
| **Daten aktualisieren** | Liest die Auftragsliste neu ein und wendet Sortierung und Anzeigeoptionen erneut an. |
| **Ereignisverlauf** | Öffnet die Ereignisliste des markierten Auftrags (siehe **Ereignisprotokoll**). |

**Statuswerte der Auftragszeile:**

| Status | Bedeutung |
|--------|-----------|
| **Offen** | Auftrag angelegt, noch nicht gestartet – keine Zeit- oder Mengenmeldung. |
| **Geplant** | Auftrag ist eingeplant, aber noch nicht in Bearbeitung. |
| **Gestartet** | Bearbeitung läuft; Folgemeldungen (Unterbrechen, Teilbeenden, Beenden) sind möglich. |
| **Rüsten** | Rüstphase läuft; die Rüstzeit wird getrennt erfasst, bevor der Auftrag gestartet wird. |
| **Unterbrochen** | Bearbeitung pausiert mit hinterlegtem Grund; ein Abschluss ist erst nach erneutem Starten möglich. |
| **Teilbeendet** | Eine Teilmenge ist gemeldet; der Auftrag bleibt für weitere Meldungen offen. |
| **Beendet** | Auftrag abgeschlossen; es sind keine weiteren Mengen- oder Zeitänderungen vorgesehen. |

☞ Diese App wirkt vor allem auf die Statuswechsel **Gestartet**, **Teilbeendet** und **Beendet** der Halbfertigteil-Arbeitsgänge; die übrigen Statuswerte gehören zum allgemeinen Verhalten des FA-Arbeitsvorrats.

## Ereignisprotokoll

Jeder von dieser App ausgelöste Statuswechsel (Starten, Teilbeenden, Beenden) wird als **Ereignis** zur FA-Arbeitsvorratszeile gespeichert. So lässt sich lückenlos nachvollziehen, wann und durch wen der letzte Arbeitsgang gemeldet wurde.

**Einstieg:** Markieren Sie im **FA-Arbeitsvorrat** die Auftragszeile und wählen Sie **Ereignisverlauf**. Es öffnen sich die **FA-Arbeitsvorratereignisse** zur gewählten Zeile.

Je Ereignis werden unter anderem der erreichte **Status**, **FA-Nr.**, **Arbeitsgangnr.**, **Arbeitsplatzgruppennr.**, **Arbeitsplatznr.**, die übernommene **Zeitbuchung**, Datum und Uhrzeit sowie der anlegende Benutzer festgehalten. Bei einer **Unterbrechung** wird zusätzlich der **Unterbrechungsgrundcode** protokolliert, bei einem Übergang aus dem Rüsten heraus auch der vorherige Startzeitpunkt.

☞ Das Ereignisprotokoll ist eine reine Nachweisansicht; es wird automatisch geschrieben und erfordert keine manuelle Pflege.

## Typische Anwendungsfälle

Die folgenden Nutzungsbeispiele zeigen die beiden verifizierten Rückmeldewege im Zusammenhang. Alle genannten Seiten und Aktionen entsprechen dem geprüften Programmverhalten.

### Anwendungsfall 1 – Automatische Rückmeldung beim Umlagerungseingang

**Auslöser:** Am Wareneingang wird ein Halbfertigteil aus der vorgelagerten Fertigungsstufe umgelagert und der **Umlagerungseingang** gebucht. Der letzte Arbeitsgang ist mit der Option **Beim Buchen des Umlagerungseingangs** eingerichtet.

**Einstieg in BC:** Der Lagermitarbeiter bucht wie gewohnt den Umlagerungseingang; ein Öffnen des FA-Arbeitsvorrats ist nicht erforderlich.

**Kernablauf:**
1. Mit dem Buchen des Umlagerungseingangs ermittelt das System die zugehörige **FA-Arbeitsvorratszeile**.
2. Ist noch keine gestartete Zeile vorhanden, wird der Auftrag automatisch **gestartet**.
3. Ist der Arbeitsgang noch in Bearbeitung, setzt das System den Auftrag auf **Teilbeendet**; ist er vollständig fertig, auf **Beendet**.
4. Der Statuswechsel wird als Ereignis protokolliert.

**Abschluss:** Der Fertigungsleiter öffnet später über **Suchen** den **FA-Arbeitsvorrat**, filtert die **Arbeitsplatzgruppennr.** und kontrolliert über **Ereignisverlauf**, dass der Auftrag korrekt teilbeendet bzw. beendet wurde.

### Anwendungsfall 2 – Manuelle Meldung über den FA-Arbeitsvorrat

**Auslöser:** Ein Bediener an der letzten Bearbeitungsstation soll den Fertigungsfortschritt selbst und in Teilmengen melden, weil Umlagerungseingang und tatsächliche Fertigstellung zeitlich auseinanderfallen. Der letzte Arbeitsgang ist mit der Option **Vom FA-Arbeitsvorrat** eingerichtet.

**Einstieg in BC:** Der Bediener öffnet über **Suchen** den **FA-Arbeitsvorrat** und wählt die **Arbeitsplatzgruppennr.** – bei Bedarf zusätzlich die **Arbeitsplatznr.**

**Kernablauf:**
1. Der Auftrag ist bereits **Gestartet**, weil die App ihn beim Übergang des Halbfertigteils in die Bearbeitung automatisch gestartet hat. Andernfalls wählt der Bediener **Starten**.
2. Für eine gefertigte Teilmenge wählt der Bediener **Teilbeenden**; der Status wechselt auf **Teilbeendet** und der Auftrag bleibt offen.
3. Muss die Arbeit pausiert werden, wählt der Bediener **Unterbrechen** und gibt einen **Unterbrechungsgrundcode** an; der Status wird **Unterbrochen**.
4. Ist der Arbeitsgang vollständig fertig, wählt der Bediener **Beenden**; abhängig von der **Zeitbuchung** werden Zeiten und ggf. Menge gebucht und der Status wird **Beendet**.

**Abschluss:** Über **Ereignisverlauf** prüft der Bediener die protokollierten Meldungen; über **Beleg anzeigen** kann er bei Bedarf den zugehörigen Fertigungsauftrag öffnen.

## FAQ und Troubleshooting

### Warum erscheint die Option „Vom FA-Arbeitsvorrat“ nicht im letzten Arbeitsgang?
Die **Halbfertigteil letzter AG Option** lässt sich erst wählen, wenn am selben Arbeitsgang das Kennzeichen **Halbfertigartikel** aktiviert ist. Setzen Sie zuerst das Kennzeichen; danach steht die Option zur Verfügung.

### Warum wird beim Setzen der Option eine Lagerort-Meldung angezeigt?
Das System verlangt, dass sich der **Lagerort** des Arbeitsgangs vom Lagerort der Arbeitsplatzgruppe unterscheidet. Sind beide gleich, wird die Auswahl mit einer Meldung abgebrochen. Ordnen Sie der Arbeitsplatzgruppe einen abweichenden Lagerort zu.

### Warum passiert nach dem Buchen des Umlagerungseingangs nichts im FA-Arbeitsvorrat?
Das ist bei der Option **Vom FA-Arbeitsvorrat** so vorgesehen: Das System meldet dann bewusst nicht automatisch zurück. Der Abschluss erfolgt manuell über **Teilbeenden**/**Beenden**. Für die automatische Rückmeldung wählen Sie **Beim Buchen des Umlagerungseingangs**.

### Warum ist mein Auftrag bereits „Gestartet“, obwohl ich nichts getan habe?
Bei der Option **Vom FA-Arbeitsvorrat** startet die App den Auftrag automatisch, sobald das Halbfertigteil in Bearbeitung geht – vorausgesetzt, er ist noch nicht **Gestartet**. Sie können direkt mit **Teilbeenden** oder **Beenden** fortfahren.

### Warum verlangt „Unterbrechen“ eine zusätzliche Eingabe?
Beim **Unterbrechen** ist ein **Unterbrechungsgrundcode** verpflichtend. Wird kein Grund ausgewählt, bricht die Aktion ab und der Status bleibt unverändert. So ist jede Pause begründet dokumentiert.

### Warum lässt sich „Nur Zeit melden“ nicht aktivieren?
**Nur Zeit melden** ist nur mit der Zeitbuchung **Standard** oder **Sollzeit** zulässig. Bei anderen Zeitbuchungsarten weist das System das Kennzeichen mit einer Feldmeldung ab. Stellen Sie zuerst die passende **Zeitbuchung** ein.

### Warum kann ich einen Auftrag nicht direkt beenden, ohne ihn zu starten?
Das direkte Teilbeenden/Beenden ohne vorheriges Starten ist nur möglich, wenn in der Arbeitsplatzgruppeneinrichtung **Start nicht erforderlich** aktiviert ist. Dieses Kennzeichen ist mit der Zeitbuchung **Standard** nicht kombinierbar.

### Muss ich einen Auftrag komplett fertigstellen oder darf ich Teilmengen melden?
Teilmengen sind ausdrücklich zulässig. Über **Teilbeenden** setzen Sie den Auftrag auf **Teilbeendet**; er bleibt für weitere Meldungen offen. Ein Warten auf den vollständigen Mengenausgleich ist nicht erforderlich.

### Wo sehe ich, wann und wie ein Arbeitsgang gemeldet wurde?
Markieren Sie die Auftragszeile im **FA-Arbeitsvorrat** und wählen Sie **Ereignisverlauf**. In den **FA-Arbeitsvorratereignissen** finden Sie Status, Datum, Uhrzeit, Benutzer, Arbeitsplatzgruppe/Arbeitsplatz und – bei Unterbrechungen – den Unterbrechungsgrundcode.

### Warum werden beim Beenden andere Zeiten gebucht als tatsächlich gearbeitet?
Das hängt von der **Zeitbuchung** der Arbeitsplatzgruppe ab: Bei **Sollzeit** oder **Mengenabhängige Sollzeit** werden nicht die Ist-Zeiten, sondern die im Arbeitsplan hinterlegten bzw. mengenabhängig verteilten Sollzeiten gebucht. Für Ist-Zeiten wählen Sie **Standard** oder **Manuell**.
