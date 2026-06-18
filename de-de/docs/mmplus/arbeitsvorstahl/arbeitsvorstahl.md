---
title: FA-Arbeitsvorrat Stahlhandel mit Zusatzleistungen
---

# Anwenderhandbuch FA-Arbeitsvorrat Stahl

---

## Einleitung

Dieses Modul erweitert den **FA-Arbeitsvorrat** für die Stahlfertigung in Microsoft Dynamics 365 Business Central. Es ergänzt die Fertigungsrückmeldung um die Stahleinheiten **KG**, **Meter** und **Stück**, führt **Chargen** für Vormaterial und produzierte Mengen, erlaubt das Weiterführen von nutzbarem Restmaterial als **Restecharge**, erfasst **Schrott** und stellt die **Erw. Rückmeldung** bereit, die der Anwender direkt aus der Übersicht **FA-Arbeitsvorrat** öffnet.

**Zielgruppe** sind in erster Linie die **operativen Anwenderinnen und Anwender** an den Stahlarbeitsplätzen: Sie melden täglich Arbeitsgänge zurück, verbrauchen Vormaterial, führen Chargen und Restechargen, erfassen Schrott und buchen die Mengen. Administratorinnen, Administratoren und Key User sind sekundäre Zielgruppe: Sie richten die globalen Regeln sowie die Optionen je **Arbeitsplatzgruppe** ein und pflegen die Stahlstammdaten an der **Artikelkarte**. Alle arbeiten ausschließlich über die BC-Suche (**Suchen**), Listen- und Belegseiten, Einrichtungsseiten und Aktionen — nicht über AL, Visual Studio oder Git.

**Typischer Einstieg (Anwenderreise):** Der Anwender öffnet die übergeordnete Übersicht **FA-Arbeitsvorrat**, grenzt die Zeilen über die **Arbeitsplatzgruppe** und ggf. den **Status** ein, sortiert nach dem am Arbeitsplatz vorgegebenen Muster, wählt die Zeile für Auftrag, Arbeitsgang und Arbeitsplatzgruppe aus und startet daraus die Aktion **Erw. Rückmeldung**. Diese öffnet die Arbeitsfläche **FA-Arbeitsvorrat Vormaterialien** mit ihren Unterbereichen **FA-Arbeitsvorrat Chargen**, **FA-Arbeitsvorrat Restechargen** und **Schrotte**.

Der Prozess gliedert sich in drei Phasen:

1. **Einrichten** — globale Regeln auf der Seite **FA-Arbeitsvorrat Einrichtung**, arbeitsplatzbezogene Optionen je Arbeitsplatzgruppe auf der Seite **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** sowie die Stahlstammdaten an der **Artikelkarte**.
2. **Zurückmelden** — auf der Seite **FA-Arbeitsvorrat** den Arbeitsgang wählen und über **Erw. Rückmeldung** Vormaterial, Chargen, Restechargen, Schrott und Zeiten erfassen.
3. **Buchen und Abschließen** — über **FA-Arbeitsvorrat Buchung** kontrollieren und buchen, mit **Teilbeenden** oder **Beenden** abschließen; die Ergebnisse erscheinen in den **FA-Arbeitsvorratereignissen** und den **FA-Schrottposten**.

---

## Schnellstart für Anwender

Der folgende Pfad führt mit minimalem Aufwand zur Rückmeldung eines Stahl-Arbeitsgangs. Voraussetzung ist die abgeschlossene **Einrichtung** (siehe nächstes Kapitel). Im Tagesgeschäft genügen diese Schritte:

1. **Einmalige Prüfung der Einrichtung:** Öffnen Sie in der Liste **Arbeitsplatzgruppen** die betroffene Zeile und wählen Sie die Aktion **FA-Arbeitsvorrat Einrichtung**, um die **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** zu prüfen — sind **Erw. Rückmeldung**, **Vormaterialorientiert** und (bei Restmaterial) **Erw. Rückmeldung Restechargen** aktiviert?
2. Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorrat**.
3. Grenzen Sie die Liste auf Ihre **Arbeitsplatzgruppe** ein (übergeordnete Eingrenzung) und ggf. zusätzlich auf den **Status**; sortieren Sie nach dem vorgegebenen Muster.
4. Wählen Sie die Zeile für den passenden Auftrag und Arbeitsgang und prüfen Sie den **Status** — für die Rückmeldung muss er **Gestartet** sein — sowie die Stahlfelder **Fertig-KG**, **Fertig-Meter** und **Fertig-Stück**.
5. Öffnen Sie über die Aktion **Erw. Rückmeldung** die Seite **FA-Arbeitsvorrat Vormaterialien**.
6. Kontrollieren oder ergänzen Sie die Vormaterialzeile. Wählen Sie eine vorhandene Charge über **Chargenauswahl** oder bauen Sie die Zeilen über **Materialbestandssuche starten** auf; legen Sie über **Charge erstellen** die produzierte Charge an.
7. Legen Sie bei nutzbarem Restmaterial über **Restecharge erstellen** eine **Restecharge** an, sofern der Arbeitsplatz dies vorsieht.
8. Prüfen Sie in der Factbox **Geb. Mengenbilanz**, ob Vormaterial, Chargen, Restechargen und Schrott zusammenpassen (Wert **= Mengenbilanz** möglichst 0).
9. Buchen Sie die Rückmeldung mit **OK**. Ist am Arbeitsplatz **Buchungsseite ausblenden** nicht gesetzt, kontrollieren Sie zuvor auf der Seite **FA-Arbeitsvorrat Buchung** Menge, KG, Meter, Stück, Lagerortcode und Lagerplatzcode.
10. Schließen Sie den Arbeitsgang über die Aktionen **Teilbeenden** (Teilrückmeldung, Status wird **Teilbeendet**) oder **Beenden** (Status wird **Beendet**) auf der Übersicht **FA-Arbeitsvorrat** ab.

Eine **Teilrückmeldung** ist zulässig: Über **Teilbeenden** wechselt die Zeile in den Status **Teilbeendet** und kann weitere Teilrückmeldungen aufnehmen, bis Sie sie mit **Beenden** abschließen. Es gibt keine Regel, die das Abschließen erst bei ausgeglichener Bilanz zulässt; die **Geb. Mengenbilanz** dient nur der Kontrolle.

---

## Einrichtung

Die Einrichtung gliedert sich in eine **globale Ebene** auf der Seite **FA-Arbeitsvorrat Einrichtung** und eine **arbeitsplatzbezogene Ebene** je Arbeitsplatzgruppe auf der Seite **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**. Richten Sie zuerst die globalen Regeln ein und verfeinern Sie danach die Optionen je Arbeitsplatzgruppe; die Schrottlogistik konfigurieren Sie ebenfalls je Arbeitsplatzgruppe. Beide Seiten zeigen die zusammengeführte Oberfläche aus Basismodul und Stahlerweiterung — dieses Handbuch dokumentiert jeweils die gesamte Seite, damit Sie keinen weiteren Leitfaden benötigen.

### Globale Einrichtung — FA-Arbeitsvorrat Einrichtung

**Einstieg:** Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorrat Einrichtung** (firmenweite Einrichtungskarte, ein Datensatz je Mandant).

**Wer und wann:** Die Administratorin oder der Key User richtet diese Regeln einmalig vor der ersten Stahlrückmeldung ein. Die ersten Felder steuern Reihenfolgenlogik, Fortschreibung der Arbeitsvorratszeilen und Anzeige des Basismoduls; die Stahlerweiterung ergänzt im Bereich **Allgemein** die letzten fünf Felder. Die Stahlregeln greifen später in der Seite **FA-Arbeitsvorrat Vormaterialien** (siehe *Tägliche Arbeit am FA-Arbeitsvorrat*).

| Einrichtung | Erläuterung |
|---|---|
| Auftragsvorr.-Reihenfolge beachten | Wenn aktiviert, dann arbeitet der Arbeitsvorrat die Arbeitsgänge in der über die Reihenfolge gesteuerten Abfolge ab; dadurch wird in der Rückmeldung die geplante Auftragsfolge eingehalten. |
| Automatische Reihenfolgeanpassung | Wenn aktiviert, dann passt das System die Reihenfolgenummern beim Verschieben von Zeilen automatisch an; dadurch entfällt das manuelle Nachnummerieren. |
| Automatische Reihenfolge beim Beenden | Wenn aktiviert, dann wird die Reihenfolge beim **Beenden** eines Arbeitsgangs fortgeschrieben; dadurch rückt der nächste Arbeitsgang ohne Eingriff nach. |
| Zwangsfolge bei Arbeitsplänen | Wenn aktiviert, dann erzwingt das Modul die Rückmeldung in der vom Arbeitsplan vorgegebenen Arbeitsgangfolge; dadurch wird das Überspringen von Arbeitsgängen verhindert. |
| FA-Zeile nach Aktion aktualisieren | Wenn aktiviert, dann schreibt das Modul nach einer Job-Aktion die Fertigungsauftragszeile fort; dadurch stimmen Auftragsmengen und Rückmeldung überein. |
| FA-Zeile bei jeder Aktion / bei Rüsten / bei Bearbeitung / bei Unterbrechen / bei Teilbeenden / bei Beenden / bei Erneut öffnen aktualisieren | Wenn die jeweilige Option aktiviert ist, dann erfolgt die Fortschreibung der Fertigungsauftragszeile genau bei dieser Aktion; dadurch steuern Sie, zu welchem Zeitpunkt die Auftragszeile aktualisiert wird (sieben einzeln schaltbare Aktionskennzeichen). |
| Menge aus Restmenge für Umlagerung setzen | Wenn aktiviert, dann übernimmt das Modul beim Anlegen einer Umlagerung die noch offene Restmenge als Vorschlagsmenge; dadurch entfällt die manuelle Mengeneingabe in den **FA-Arbeitsvorrat Umlagerungszeilen**. |
| Arbeitsvorratszeile per Abfrage sammeln | Wenn aktiviert, dann ermittelt das Modul die Arbeitsvorratszeilen über eine performante Abfrage; dadurch werden große Übersichten schneller aufgebaut. |
| Beendete Zeilen archivieren | Steuert die Archivierung beendeter Arbeitsvorratszeilen. **Nie:** keine Archivierung. **Beim Beenden des Fertigungsauftrags:** beim Beenden des Fertigungsauftrags werden die zugehörigen Rückmeldedaten (Chargen, Restechargen, Schrott) in die Archivtabellen geschrieben (siehe *Historie, Archiv und Nachverfolgung*). |
| Aktualisierungsintervall (Sek.) | Legt fest, in welchem Sekundentakt sich die Übersicht **FA-Arbeitsvorrat** selbst aktualisiert; dadurch sehen Anwender am Arbeitsplatz Statuswechsel ohne manuelles Neuladen. |
| Ampel 1 / Ampel 2 / Ampel 3 | Legen die Schwellwerte für die farbliche Statusanzeige (Ampellogik) in der Übersicht fest; dadurch erkennt der Anwender kritische Zeilen auf einen Blick. |
| Resteartikel erforderlich | Wenn aktiviert, dann erzwingt das Modul beim Anlegen einer **Restecharge** in der erweiterten Rückmeldung einen am Ausgangsartikel hinterlegten Resteartikel; ohne Eintrag meldet das Modul „Resteartikel muss in den Artikelstammdaten definiert sein!". Ohne das Kennzeichen ist die Restecharge auch ohne Resteartikel möglich. (Siehe *Erweiterte Rückmeldung einrichten* und *Stammdaten*.) |
| Chargennr. in Erw. Rückmeldung zuweisen | Wenn aktiviert, dann vergibt das Modul beim Erfassen einer Charge in der erweiterten Rückmeldung automatisch die Chargennummer; dadurch entfällt die manuelle Nummernzuweisung über **Chargennr. zuweisen**. |
| Lagerort/Lagerplatz automatisch für Fertigungschargen ändern | Wenn aktiviert, dann übernimmt das Modul beim Buchen Lagerort und Lagerplatz der Vormaterialzeile automatisch in die Fertigungscharge; ohne das Kennzeichen bleiben die in der Charge erfassten Lagerwerte stehen. |
| Materialangleichfaktor in Charge der erw. Rückmeldung | Wenn aktiviert, dann berücksichtigt das Modul den Materialangleichfaktor (KG pro Meter bzw. pro Stück) bei den **Chargen** der erweiterten Rückmeldung; dadurch werden die umgerechneten Stahleinheiten an den theoretischen Materialwerten angeglichen. |
| Materialangleichfaktor in Restecharge der erw. Rückmeldung | Wenn aktiviert, dann wird der Materialangleichfaktor zusätzlich auf die **Restechargen** angewendet; dadurch sind auch weitergeführte Restmengen einheitlich angeglichen. |

> **Berechtigungen:** Der mitgelieferte Berechtigungssatz **Prod. Order Job Steel Permissions** bestimmt die Berechtigungen für die Stahltabellen, -seiten und -codeunits dieser Erweiterung. Weisen Sie ihn den Anwendern zu, die mit der erweiterten Rückmeldung arbeiten sollen.

### Arbeitsplatzbezogene Einrichtung — FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung

**Einstieg:** Öffnen Sie in der Liste **Arbeitsplatzgruppen** die betreffende Zeile und wählen Sie die Aktion **FA-Arbeitsvorrat Einrichtung**; es öffnet sich die Seite **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** für diese Arbeitsplatzgruppe. (Die Seite ist nicht über **Suchen** erreichbar; der Einstieg führt immer über die Arbeitsplatzgruppe.)

**Wer und wann:** Die Administratorin oder der Key User pflegt je Arbeitsplatzgruppe, wie zurückgemeldet, gebucht und Schrott behandelt wird. Diese Optionen steuern unmittelbar, welche Bereiche und Aktionen der Anwender später in der **FA-Arbeitsvorrat Vormaterialien** sieht (Cross-Link: *Tägliche Arbeit am FA-Arbeitsvorrat*).

#### Allgemeine Arbeitsplatzoptionen (Basismodul)

| Einrichtung | Erläuterung |
|---|---|
| Arbeitsplatzgruppenname | Zeigt den Namen der Arbeitsplatzgruppe (nicht editierbar); dadurch ordnen Sie die Einrichtungszeile eindeutig zu. |
| Unproduktiv | Wenn aktiviert, dann gilt die Arbeitsplatzgruppe als unproduktiv und wird in Auswertungen entsprechend behandelt; dadurch trennen Sie Hilfs- von Wertschöpfungsplätzen. |
| Mehrere Aufträge starten | Wenn aktiviert, dann dürfen an dieser Gruppe mehrere Aufträge gleichzeitig im Status **Gestartet** stehen; dadurch lassen sich parallele Bearbeitungen abbilden. |
| Start nicht erforderlich | Wenn aktiviert, dann kann ohne vorherige Startaktion zurückgemeldet werden; dadurch ist die Rückmeldung auch ohne expliziten **Starten**-Schritt möglich. |
| Sortierung | Legt die Anzeigereihenfolge der Zeilen in der Übersicht fest. **Reihenfolge:** nach der Reihenfolgenummer. **Status:** nach dem aktuellen Status. **Prod. Artikel:** nach dem Fertigungsartikel. **Datum:** nach dem Startdatum. |
| Zeitbuchung | Steuert, wie Zeiten in der Rückmeldung erfasst werden. **Standard:** manuelle Zeiterfassung mit Start-/Endzeitpunkt. **Keine:** keine Zeiterfassung; alle Zeitfelder bleiben gesperrt. **Sollzeit:** Soll-Rüst- und -Bearbeitungszeit werden vorgeschlagen, nur **Rüstzeit** und **Bearbeitungszeit** sind frei. **Mengenabhängige Sollzeit:** die Zeit wird aus der Menge berechnet; alle Zeitfelder bleiben gesperrt. **Manuell:** freie Erfassung von Rüst- und Bearbeitungszeit. |
| Nur Dauer melden | Wenn aktiviert, dann wird nur die Dauer ohne Start-/Endzeitpunkt gebucht; dadurch genügt die Angabe der Zeitspanne. |
| Rüstaktivität | Wenn aktiviert, dann steht das **Rüsten** als eigene Aktion bereit; dadurch lässt sich Rüstzeit getrennt von der Bearbeitungszeit melden. |
| Umlagerung | Wenn aktiviert, dann stehen für diese Arbeitsplatzgruppe die Seite **FA-Arbeitsvorrat Umlagerungszeilen** und die zugehörige Aktion zur Verfügung; dadurch kann Vormaterial vor dem Verbrauch umgelagert werden (siehe *Lager, Umlagerung und Folgebuchungen*). |
| Startdatum/-zeit änderbar | Wenn aktiviert, dann darf der Anwender Start- und Endzeit in der erweiterten Rückmeldung ändern; ohne das Kennzeichen bleiben diese Felder gesperrt. |
| Fertigmenge initialisieren | Steuert die Vorbelegung der Fertigmenge. **(leer):** keine Vorbelegung. **Vorheriger Arbeitsgang:** das Modul übernimmt die im vorherigen Arbeitsgang gebuchte Menge als Startwert; dadurch entfällt die erneute Erfassung bei der Mengenübergabe. |
| Direktsuche FA deaktivieren | Wenn aktiviert, dann wird die direkte Sprungsuche in den Arbeitsvorrat unterdrückt; dadurch steuern Sie an Touch-Arbeitsplätzen das Navigationsverhalten. |
| Verkaufsauftragsnr. anzeigen | Wenn aktiviert, dann blendet die Übersicht die zugehörige Verkaufsauftragsnummer ein; dadurch sieht der Anwender den Auftragsbezug der Fertigung. |
| Zeiten anzeigen | Wenn aktiviert, dann zeigt die erweiterte Rückmeldung den Bereich **Buchungszeitraum** mit Start-/Endzeit, Rüst- und Bearbeitungszeit; dadurch werden Zeiten je Rückmeldung sichtbar. |

#### Bereich Vormaterial (Stahlerweiterung)

| Einrichtung | Erläuterung |
|---|---|
| Vormaterialorientiert | Wenn aktiviert, dann führt das Modul die Rückmeldung dieser Arbeitsplatzgruppe vormaterialorientiert: in der **FA-Arbeitsvorrat Vormaterialien** werden Vormaterialzeilen und ihre Chargen geführt und beim Buchen an den Materialverbrauch gekoppelt. Ohne das Kennzeichen bleibt der Arbeitsgang rein mengen-/zeitbezogen ohne Vormaterialbezug. |
| Rückmeldung ohne Vormaterial | Wenn aktiviert, dann lässt das Modul eine Rückmeldung auch ohne erfasstes Vormaterial zu; dadurch sind reine Mengen-/Zeitrückmeldungen an einem sonst vormaterialorientierten Arbeitsplatz möglich. |
| Vormaterialverbrauch buchen | Wenn aktiviert, dann bucht das Modul beim Rückmelden den Vormaterialverbrauch als Verbrauchsbuchung; zugleich wird in den **FA-Arbeitsvorrat Umlagerungszeilen** das Ziel-Lager gesperrt, da der Verbrauch direkt erfolgt. Ohne das Kennzeichen wird kein Verbrauch gebucht und das Umlagerungsziel bleibt editierbar. |
| Restmenge ohne Charge ignorieren | Wenn aktiviert, dann ergänzt das Modul fehlende Vormaterialmengen ohne zugeordnete Charge **nicht** automatisch; ohne das Kennzeichen füllt es die Differenz zur erwarteten Komponentenmenge als chargenlose Restzeile auf. Dadurch steuern Sie, ob nicht chargengeführte Restmengen in die Rückmeldung einfließen. |

#### Bereich Erweiterte Rückmeldung (Stahlerweiterung)

| Einrichtung | Erläuterung |
|---|---|
| Erw. Rückmeldung | Wenn aktiviert, dann erscheint in der Übersicht **FA-Arbeitsvorrat** für Zeilen dieser Arbeitsplatzgruppe die Aktion **Erw. Rückmeldung**, und die erweiterte Rückmeldung wird beim Buchen verarbeitet. Ohne das Kennzeichen ist die Aktion nicht sichtbar. |
| Erw. Rückmeldung Vormaterial | Wenn aktiviert, dann blendet die Seite **FA-Arbeitsvorrat Vormaterialien** den Vormaterialbereich ein und macht ihn editierbar; dadurch erfasst der Anwender Vormaterial mengen- und chargengenau. |
| Erw. Rückmeldung Chargen | Wenn aktiviert, dann wird die Unterseite **FA-Arbeitsvorrat Chargen** eingeblendet; dadurch erfasst der Anwender die produzierten Chargen je Vormaterial. Diese Option ist Voraussetzung für die **Automatische Schrottdifferenzermittlung**. |
| Erw. Rückmeldung Restechargen | Wenn aktiviert, dann wird die Unterseite **FA-Arbeitsvorrat Restechargen** eingeblendet und die Aktion **Restecharge erstellen** verfügbar; dadurch kann nutzbares Restmaterial als **Restecharge** weitergeführt werden. |
| Menge in Erw. Rückmeldung übertragen | Wenn aktiviert, dann übernimmt das Modul die im vorherigen Arbeitsgang gebuchten Chargenmengen als Vorschlag in den neuen Arbeitsgang; dadurch entfällt die erneute Erfassung bei der Mengenübergabe zwischen Arbeitsgängen. |
| Buchungsseite ausblenden | Wenn aktiviert, dann erscheint beim Buchen aus der Rückmeldung **keine** Seite **FA-Arbeitsvorrat Buchung**; der Buchungsschritt läuft mit den erfassten Werten im Hintergrund, der Anwender bestätigt nur die erweiterte Rückmeldung mit **OK**. Ohne das Kennzeichen prüft der Anwender Menge, KG, Meter, Stück, Lagerort und Lagerplatz auf der Buchungsseite, bevor er bestätigt. |

#### Bereich Schrott (Stahlerweiterung)

| Einrichtung | Erläuterung |
|---|---|
| Schrott Lagerortcode | Legt den Lagerort fest, auf den Schrottbuchungen dieser Arbeitsplatzgruppe laufen; dadurch wird Schrott vom Normalbestand getrennt geführt. Beim Ändern des Lagerorts leert das Modul automatisch den **Schrott Lagerplatzcode** (siehe FAQ 5). |
| Schrott Lagerplatzcode | Legt den Lagerplatz innerhalb des Schrottlagerorts fest; dadurch wird der Schrott am Zielplatz eingelagert. Nur in Kombination mit einem gesetzten Schrott Lagerortcode sinnvoll. |
| Automatische Schrottdifferenzermittlung | Wenn aktiviert, dann ermittelt das Modul den Schrott beim Beenden als Gewichtsdifferenz (Vormaterial minus Chargen minus Restechargen minus bereits gebuchter Schrott) automatisch; das Feld **Schrottmenge** in der Rückmeldung ist dann gesperrt, der Anwender arbeitet über die Aktion **Schrotte**. Voraussetzung ist **Erw. Rückmeldung Chargen**. Ohne das Kennzeichen gibt der Anwender die Schrottmenge manuell ein. |
| Direkte Schrottbuchung | Wenn aktiviert, dann wird der Schrottartikel sofort beim Buchen bestandswirksam (gebuchte Schrottmenge fortgeschrieben); ohne das Kennzeichen bleibt der Schrott zunächst als registrierte Menge offen. |

### Erweiterte Rückmeldung einrichten

**Prozess-Intro:** Die erweiterte Stahlrückmeldung ist eine Kapazität, die der Administrator über **mehrere Seiten** freischaltet, bevor der Anwender sie im Tagesablauf nutzt. Konfigurieren Sie in Abhängigkeitsreihenfolge; die operative Nutzung erfolgt anschließend in der **FA-Arbeitsvorrat Vormaterialien** (Cross-Link: *Tägliche Arbeit am FA-Arbeitsvorrat*).

1. **Stammdaten zuerst:** Pflegen Sie an der **Artikelkarte** die Stahl- und Resteartikelangaben (**Resteartikel**, **Resteartikelnr.**), damit Restechargen ein gültiges Ziel haben (siehe *Stammdaten*). Wenn an der **FA-Arbeitsvorrat Einrichtung** das globale Kennzeichen **Resteartikel erforderlich** gesetzt ist, dann ist dieser Schritt verpflichtend, sonst bricht das Anlegen einer Restecharge mit Fehlermeldung ab.
2. **Globale Stahlregeln:** Setzen Sie auf **FA-Arbeitsvorrat Einrichtung** die Stahlkennzeichen (**Chargennr. in Erw. Rückmeldung zuweisen**, **Lagerort/Lagerplatz automatisch für Fertigungschargen ändern**, **Materialangleichfaktor in Charge / in Restecharge der erw. Rückmeldung**, **Resteartikel erforderlich**). Wenn gesetzt, dann gelten diese Regeln mandantenweit für alle Stahlrückmeldungen.
3. **Arbeitsplatzbezogene Freischaltung:** Aktivieren Sie auf **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** im Bereich **Erweiterte Rückmeldung** zuerst **Erw. Rückmeldung**, danach die Teilschalter **Erw. Rückmeldung Vormaterial**, **Erw. Rückmeldung Chargen** und — bei Restmaterial — **Erw. Rückmeldung Restechargen**. Wenn aktiviert, dann erscheint die Aktion **Erw. Rückmeldung** in der Übersicht und die passenden Bereiche werden in der Arbeitsfläche eingeblendet.
4. **Operativer Abschluss:** Der Anwender markiert auf **FA-Arbeitsvorrat** eine Zeile mit Status **Gestartet** und startet die Aktion **Erw. Rückmeldung**; damit ist die Kette geschlossen (Cross-Link: *Tägliche Arbeit am FA-Arbeitsvorrat*).

### Schrottbehandlung einrichten

**Prozess-Intro:** Die Schrottlogistik ist eine zweite, eigenständige Kapazität mit eigener Konfigurationskette über Stahl-Basiseinrichtung und Arbeitsplatzgruppe; sie endet mit der Schrotterfassung in der täglichen Rückmeldung.

1. **Voraussetzung in der Stahl-Basis:** Aktivieren Sie in der Stahl-Basiseinrichtung die Option **Schrott je Lagerort**. Ohne diese Einstellung lehnt das Modul das Setzen von **Schrott Lagerortcode**, **Automatische Schrottdifferenzermittlung** und **Direkte Schrottbuchung** ab.
2. **Lagerziel je Arbeitsplatzgruppe:** Hinterlegen Sie auf **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung** im Bereich **Schrott** den **Schrott Lagerortcode** und optional den **Schrott Lagerplatzcode**. Wenn ein Schrottlagerort gesetzt ist, dann werden Schrottmengen dieser Gruppe getrennt vom Normalbestand geführt.
3. **Ermittlungsart:** Setzen Sie **Automatische Schrottdifferenzermittlung**, wenn der Schrott als Gewichtsdifferenz berechnet werden soll (Voraussetzung **Erw. Rückmeldung Chargen**). Wenn gesetzt, dann ist das Feld **Schrottmenge** in der Rückmeldung gesperrt und der Anwender arbeitet über die Aktion **Schrotte**.
4. **Buchungszeitpunkt:** Setzen Sie **Direkte Schrottbuchung**, wenn der Schrottartikel sofort beim Buchen bestandswirksam werden soll; ohne diese Option bleibt der Schrott zunächst als registrierte Menge offen.
5. **Operativer Abschluss:** Der Anwender erfasst Schrott in der Rückmeldung (Feld **Schrottmenge** oder Aktion **Schrotte**); beim Buchen mit Status **Beendet** schreibt das Modul die Schrottmengen fort und kennzeichnet die Schrottposten mit **Von FA-Arbeitsvorrat** (Cross-Link: *Historie, Archiv und Nachverfolgung*).

---

## Stammdaten

Die Stahlrückmeldung greift auf wenige, aber zentrale Stammsätze am Artikel sowie auf die Chargen- und Restechargeneigenschaften zu. Pflegen Sie diese, bevor Restechargen und Schrottartikel in der Rückmeldung genutzt werden.

### Artikel und Resteartikel — Artikelkarte

**Einstieg:** Artikel (Liste) → **Artikelkarte** des betreffenden Artikels.

**Wer und wann:** Der Key User pflegt diese Felder beim Anlegen oder Überarbeiten von Stahlartikeln. Sie steuern, ob ein Artikel selbst als Ziel für Restmengen dient und auf welchen Resteartikel seine Restmengen laufen. Sie wirken später beim Anlegen von Restechargen in der erweiterten Rückmeldung und werden über die globale Option **Resteartikel erforderlich** erzwungen (Cross-Link: *Erweiterte Rückmeldung einrichten*).

| Feld | Erläuterung |
|---|---|
| Resteartikel | Wenn aktiviert, dann wird der Artikel selbst als Resteartikel geführt; das Feld **Resteartikelnr.** wird gesperrt und geleert, und der Artikel kann von anderen Artikeln als Ziel für Restmengen verwendet werden. Das Kennzeichen lässt sich nicht entfernen, solange andere Artikel ihn noch nutzen — das Modul meldet dann „Artikel wird als Resteartikel in anderen Artikeln verwendet!". |
| Resteartikelnr. | Wenn Sie hier einen Resteartikel hinterlegen, dann laufen Restmengen dieses Artikels auf den angegebenen Resteartikel; dabei muss die Materialart übereinstimmen, damit Restmaterial ohne Bruch in Folgeprozesse übernommen werden kann. Das Feld ist nur editierbar, solange der Artikel selbst kein Resteartikel ist. Beim Ändern der Materialart prüft das Modul, dass kein Artikel mit abweichender Materialart denselben Resteartikel nutzt; andernfalls erscheint „Artikel mit anderer Materialart verwenden diesen Resteartikel!". |

**Abhängigkeit:** Wenn die globale Option **Resteartikel erforderlich** gesetzt ist, dann erzwingt das Modul beim Anlegen einer Restecharge in der erweiterten Rückmeldung einen hinterlegten Resteartikel. Ohne diesen Eintrag erscheint „Resteartikel muss in den Artikelstammdaten definiert sein!" (siehe FAQ 3).

### Artikelvorlage — Resteartikel/Schrottartikel

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Artikelvorlage** (m+m Create Item Template) und wählen Sie die Vorlage.

**Wer und wann:** Der Key User legt die Vorlagen vor der Serienanlage von Stahlartikeln an. Wenn die hier gesetzten Kennzeichen aktiv sind, dann erhalten neu aus der Vorlage erzeugte Artikel die entsprechende Stahlrolle automatisch.

| Feld | Erläuterung |
|---|---|
| Resteartikel | Wenn aktiviert, dann werden aus dieser Vorlage erzeugte Artikel sofort als **Resteartikel** angelegt; dadurch entfällt die manuelle Nachpflege an der Artikelkarte. |
| Schrottartikel | Wenn aktiviert, dann werden aus dieser Vorlage erzeugte Artikel als **Schrottartikel** angelegt; dadurch stehen sie unmittelbar für Schrottbuchungen aus der Rückmeldung bereit. |

### Chargen- und Restechargeneigenschaften — Eigenschaften

**Einstieg:** In der **FA-Arbeitsvorrat Vormaterialien** über die Factboxen **Chargeneigenschaften** und **Restechargeneigenschaften**, oder über die Seite **Eigenschaften** (Record Properties).

**Wer und wann:** Die Eigenschaften entstehen mit der Charge bzw. Restecharge in der Rückmeldung; der Anwender ergänzt sie bei Bedarf. Die Stahlerweiterung kennzeichnet hier, ob eine Eigenschaftszeile zu einer Restecharge gehört.

| Feld | Erläuterung |
|---|---|
| Restecharge | Wenn gesetzt, dann gehört die Eigenschaftszeile zu einer **Restecharge** (nicht zu einer regulären Charge); dadurch unterscheiden Sie die Eigenschaften weitergeführten Restmaterials von denen der produzierten Charge. |

---

## Tägliche Arbeit am FA-Arbeitsvorrat

**Einrichtungsbezug:** Welche Zeilen der Anwender hier sieht und ob die Aktion **Erw. Rückmeldung** erscheint, steuern die Optionen aus dem Kapitel *Einrichtung* (**Erw. Rückmeldung**, **Vormaterialorientiert**, **Rückmeldung ohne Vormaterial**, **Sortierung**). Die Stahlmengen entstehen aus den Stammdaten am Artikel. Welche Unterbereiche und Aktionen in der erweiterten Rückmeldung sichtbar sind, ergibt sich aus den Teilschaltern der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**.

### Einstieg über die Übersicht FA-Arbeitsvorrat

**Einstieg:** Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorrat**.

Hier sehen Sie Auftrag, Arbeitsgang, **Arbeitsplatzgruppe**, **Status** und die zusätzlichen Stahlspalten. Für den Tagesablauf gilt:

1. Grenzen Sie die Liste zuerst auf die **Arbeitsplatzgruppe** ein (übergeordnete Eingrenzung) und ggf. zusätzlich auf den **Status**.
2. Sortieren Sie nach dem an der Arbeitsplatzgruppe vorgegebenen Muster (**Sortierung**).
3. Kontrollieren Sie **Status** und Artikelbezug der Zeile.
4. Öffnen Sie über die Aktion **Erw. Rückmeldung** die erweiterte Rückmeldung direkt aus der markierten Zeile. Die Aktion ist nur sichtbar, wenn an der Arbeitsplatzgruppe **Erw. Rückmeldung** aktiv ist.

#### Filter

Die Übersicht **FA-Arbeitsvorrat** ist die zusammengeführte Oberfläche aus Basisliste und Stahlerweiterung. Für den Tagesablauf grenzen Sie über folgende Filterfelder ein:

| Filterfeld | Erläuterung |
|---|---|
| Arbeitsplatzgruppennr. | Wenn gesetzt, dann werden die Zeilen auf die gewählte Arbeitsplatzgruppe gefiltert; dies ist die übergeordnete Eingrenzung für den Arbeitsplatz und sollte zuerst gesetzt werden. |
| Status | Wenn gesetzt, dann werden die Zeilen nach dem Arbeitsgangstatus gefiltert (z. B. nur **Gestartet**); dadurch sieht der Anwender nur rückmeldebereite Zeilen. Diese Eingrenzung ist optional und folgt der Arbeitsplatzgruppe. |

#### Status-Werte

Der **Status** der Arbeitsvorratszeile steuert, welche Rückmeldungen möglich sind:

| Wert | Bedeutung |
|---|---|
| Offen | Zeile angelegt, noch nicht gestartet — keine Rückmeldung möglich. |
| Geplant | Arbeitsgang eingeplant, aber noch nicht begonnen — erscheint zur Vorbereitung in der Übersicht. |
| Gestartet | Bearbeitung läuft; **Erw. Rückmeldung** und Buchungsaktionen sind möglich. |
| Unterbrochen | Arbeitsgang pausiert; vor erneuter Rückmeldung muss die Zeile über **Starten** wieder gestartet werden. |
| Teilbeendet | Erste Teilrückmeldung gebucht; der Arbeitsgang kann weitere Teilrückmeldungen aufnehmen, bis er mit **Beenden** abgeschlossen wird. |
| Beendet | Arbeitsgang abgeschlossen; keine weiteren Mengen- oder Zeitrückmeldungen. |
| Rüsten | Der Arbeitsgang befindet sich in der Rüstphase; Rüstzeit wird getrennt von der Bearbeitung erfasst. |

#### Stahlspalten in der Übersicht

| Feld | Erläuterung |
|---|---|
| Fertig-KG / Fertig-Meter / Fertig-Stück | Zeigen die produzierte (zurückgemeldete) Menge der Zeile in KG, Metern bzw. Stück; dadurch beurteilt der Anwender den Produktionsfortschritt in der Stahleinheit, nicht nur in der Basismenge. |
| Fertiggestellte KG / Fertiggestellte Meter / Fertiggestellte Stück | Zeigen die bereits gebuchte, fertiggestellte Menge in KG, Metern bzw. Stück (schreibgeschützt, je Buchung fortgeschrieben); dadurch ist der gebuchte Fortschritt je Stahleinheit sichtbar. |
| Vormaterialartikelnr. *(ausgeblendet)* | Zeigt den eingesetzten Vormaterialartikel der Zeile; dadurch ist der Materialbezug ohne Öffnen der Rückmeldung erkennbar. |
| Vormaterialvariantencode / Vormaterialchargennr. *(ausgeblendet)* | Zeigen Variante und Charge des Vormaterials; dadurch ist die Materialherkunft chargengenau nachvollziehbar. |
| Vormaterialmenge / Vormaterial-KG / Vormaterial-Meter / Vormaterial-Stück *(ausgeblendet)* | Zeigen die eingesetzte Vormaterialmenge je Einheit; dadurch erkennt der Anwender den Materialeinsatz der Zeile. |
| Vormaterialorientiert *(ausgeblendet)* | Zeigt, ob die Zeile vormaterialorientiert geführt wird (aus der Arbeitsplatzgruppe übernommen); dadurch ist die Rückmeldeart je Zeile transparent. |
| Einzelarbeitsgang *(ausgeblendet)* | Wenn gesetzt, dann wird der Arbeitsgang als Einzelarbeitsgang behandelt; dadurch steuert das Modul die getrennte Rückmeldung dieses Arbeitsgangs. |
| Buchungsseite ausblenden *(ausgeblendet)* | Zeigt je Zeile, ob beim Buchen die Seite **FA-Arbeitsvorrat Buchung** unterdrückt wird (aus der Arbeitsplatzgruppe); dadurch ist das Buchungsverhalten je Zeile erkennbar. |
| Arbeitsplanbeschreibung *(ausgeblendet)* | Zeigt die Beschreibung des Arbeitsplans der Zeile; dadurch ist der Fertigungskontext ohne Wechsel sichtbar. |

> Die zahlreichen schreibgeschützten Basisspalten der Übersicht (u. a. Reihenfolge, Beschreibung, Verkaufsauftragsnr., vorheriger/nächster Arbeitsgang, Zeitkennzahlen, Spediteur) stammen aus dem Basismodul und bleiben unverändert verfügbar; sie dienen der Orientierung im Auftrag, ohne durch die Stahlerweiterung verändert zu werden.

### Erweiterte Rückmeldung — FA-Arbeitsvorrat Vormaterialien

**Einstieg:** Markieren Sie auf **FA-Arbeitsvorrat** eine Zeile mit Status **Gestartet** und wählen Sie die Aktion **Erw. Rückmeldung**. Es öffnet sich die Arbeitsfläche **FA-Arbeitsvorrat Vormaterialien** mit dem Bereich **Buchungszeitraum**, der Vormaterialliste und den Unterseiten **FA-Arbeitsvorrat Chargen**, **FA-Arbeitsvorrat Restechargen** sowie der Aktion **Schrotte**. Welche Bereiche sichtbar und editierbar sind, hängt von den Teilschaltern der Arbeitsplatzgruppe ab.

#### Bereich Buchungszeitraum

Dieser Bereich erscheint, wenn an der Arbeitsplatzgruppe **Zeiten anzeigen** gesetzt ist. Die Editierbarkeit der Felder ergibt sich aus der Option **Zeitbuchung** und dem Kennzeichen **Startdatum/-zeit änderbar** (siehe FAQ 2).

| Feld | Erläuterung |
|---|---|
| Startdatum / Startzeit | Wenn editierbar, dann erfassen Sie hier Beginn der Bearbeitung; das Modul prüft, dass das Startdatum nicht nach dem Enddatum und die Startzeit am gleichen Tag nicht nach der Endzeit liegt, sonst erscheint „Startdatum … liegt nach dem Enddatum …!" bzw. „Startzeit … liegt nach der Endzeit …!". |
| Enddatum / Endzeit | Wenn editierbar, dann erfassen Sie hier das Ende der Bearbeitung; dieselbe Reihenfolgenprüfung wie bei Start gilt. |
| Rüstzeit | Wenn editierbar (z. B. bei **Zeitbuchung** = **Sollzeit** oder **Manuell**), dann erfassen Sie die Rüstzeit; dadurch wird die Rüstzeit getrennt gebucht. |
| Bearbeitungszeit | Wenn editierbar, dann erfassen Sie die reine Bearbeitungszeit; bei reiner Rüstbuchung wird dieses Feld gesperrt. |

#### Vormaterialzeilen

| Feld | Erläuterung |
|---|---|
| Vormaterial FA-Komponentenzeilennr. | Verknüpft die Vormaterialzeile mit der Komponente des Fertigungsauftrags; dadurch ist die Materialherkunft eindeutig. |
| Neue Vormaterial-FA-Komponente | Wenn gesetzt, dann legt das Modul beim Buchen für diese Zeile eine zusätzliche FA-Komponentenzeile an; dadurch lässt sich neu eingesetztes Vormaterial in den Auftrag aufnehmen. |
| Artikelnr. | Zeigt den eingesetzten Vormaterialartikel; dadurch ist eindeutig, welches Material verbraucht wird. |
| Variantencode *(ausgeblendet)* | Bezeichnet die Variante des Vormaterials; dadurch wird die richtige Ausprägung verbraucht. |
| Chargennr. | Zeigt die zugeordnete Vormaterialcharge; dadurch ist die Materialherkunft chargengenau nachvollziehbar. |
| Lieferantenchargennr. *(ausgeblendet)* | Zeigt die Chargennummer des Lieferanten; dadurch bleibt die Herkunft bis zur Anlieferung verfolgbar. |
| Beschreibung / Beschreibung 2 *(ausgeblendet)* | Zeigen die Artikelbeschreibung des Vormaterials. |
| Lagerortcode / Lagerplatzcode | Zeigen, wo das Vormaterial liegt; beim Buchen übernimmt das Modul den Lagerort in die FA-Komponente. |
| Lagerbestand | Zeigt den verfügbaren Lagerbestand der Charge in der Basiseinheit; dadurch erkennt der Anwender, ob die geplante Menge gedeckt ist. |
| Lagerbestand KG / Lagerbestand Meter / Lagerbestand Stück *(ausgeblendet)* | Zeigen den Lagerbestand in KG, Metern bzw. Stück. |
| Menge | Wenn Sie die Menge ändern, dann speichert die Seite den Satz sofort und aktualisiert die Bilanzfactboxen; dadurch sehen Sie die Auswirkung auf den Verbrauch unmittelbar. |
| Basiseinheitencode | Zeigt die Basiseinheit der Zeile; dadurch sind die Mengen eindeutig zugeordnet. |
| KG / Meter / Stück *(ausgeblendet)* | Wenn Sie hier eine Stahleinheit pflegen, dann steuern Sie die Vormaterialmenge gewichts-, längen- bzw. stückbezogen; die Felder lösen ebenfalls ein sofortiges Speichern aus. |
| Primäres Mengenfeld *(ausgeblendet)* | Zeigt das führende Mengenfeld der Zeile; dadurch ist erkennbar, welche Stahleinheit die Menge bestimmt. |
| Gebuchte Menge / Gebuchte KG / Gebuchte Meter / Gebuchte Stück *(KG/Meter/Stück ausgeblendet)* | Zeigen den bereits gebuchten Anteil je Einheit (schreibgeschützt); dadurch ist der bisherige Verbrauch sichtbar. |
| Restmenge / Rest-KG / Rest-Meter / Rest-Stück *(KG/Meter/Stück ausgeblendet)* | Zeigen die noch offene Menge der Zeile je Einheit. |
| Geb. Restmenge / Geb. Rest-KG / Geb. Rest-Meter / Geb. Rest-Stück *(KG/Meter/Stück ausgeblendet)* | Zeigen den als Restecharge gebuchten Anteil je Einheit (schreibgeschützt). |
| Schrottmenge | Wenn editierbar (nur ohne **Automatische Schrottdifferenzermittlung**), dann erfassen Sie hier die Schrottmenge dieser Vormaterialzeile; das Speichern erfolgt sofort. Bei aktivierter automatischer Ermittlung ist das Feld gesperrt (siehe FAQ 4). |
| Reg. Schrottmenge | Zeigt die bereits registrierte Schrottmenge (schreibgeschützt); dadurch ist der erfasste Schrott der Zeile nachvollziehbar. |
| Gebuchte Schrottmenge *(ausgeblendet)* | Zeigt den bei **Direkter Schrottbuchung** bereits bestandswirksam gebuchten Schrott. |
| Rest. Lagerbestand / Rest. Lagerbestand KG/Meter/Stück *(KG/Meter/Stück ausgeblendet)* | Zeigen den verbleibenden Lagerbestand nach der geplanten Rückmeldung; dadurch erkennt der Anwender, was nach Verbrauch und Restecharge übrig bleibt. |
| Neuer Lagerortcode / Neuer Lagerplatzcode *(ausgeblendet)* | Zeigen das Ziel-Lager für umgelagertes Material; dadurch wird beim Buchen das richtige Folgelager gesetzt. |
| Gebucht *(ausgeblendet)* | Zeigt, ob die Vormaterialzeile bereits gebucht wurde. |

**Promotete Aktionen der Vormaterialfläche:** **Materialbestandssuche starten** (öffnet die Materialbestandssuche und baut die Vormaterialzeilen daraus auf), **Chargenauswahl** (übernimmt eine Charge aus den Chargennummerninformationen), **Charge erstellen** (legt eine produzierte Charge an), **Restecharge erstellen** (legt eine Restecharge an, nur bei aktivierter **Erw. Rückmeldung Restechargen**) und **Schrotte** (öffnet die Schrottzeilen).

#### Unterseite FA-Arbeitsvorrat Chargen

Dieser Bereich erscheint, wenn an der Arbeitsplatzgruppe **Erw. Rückmeldung Chargen** gesetzt ist. Hier erfasst der Anwender die je Vormaterial produzierten Chargen.

| Feld | Erläuterung |
|---|---|
| Vormaterial FA-Komponentenzeilennr. | Verknüpft die Charge mit der Vormaterialkomponente; dadurch ist die Materialherkunft der Charge eindeutig. |
| Int. Chargennr. | Enthält die interne Chargennummer der Zeile; dadurch wird dieselbe fachliche Charge technisch eindeutig geführt. |
| Beschreibung / Beschreibung 2 *(ausgeblendet)* | Zeigen die Artikelbeschreibung der Charge. |
| Menge | Wenn Sie die Chargenmenge ändern, dann aktualisiert die Seite die Ansicht sofort; dadurch sehen Sie unmittelbar die Auswirkung auf die Rückmeldung. |
| Basiseinheitencode | Zeigt die Basiseinheit der Charge. |
| KG / Meter / Stück *(ausgeblendet)* | Wenn Sie hier Mengen pflegen, dann steuern Sie die Chargenmenge gewichts-, längen- bzw. stückbezogen. |
| Primäres Mengenfeld *(ausgeblendet)* | Zeigt das führende Mengenfeld der Charge. |
| Gebuchte Menge / Gebuchte KG / Gebuchte Meter / Gebuchte Stück *(KG/Meter/Stück ausgeblendet)* | Zeigen den bereits gebuchten Chargenanteil je Einheit (schreibgeschützt). |
| Vorh. Arbeitsgangnr. *(ausgeblendet)* | Zeigt den vorherigen Arbeitsgang, aus dem die Charge übernommen wurde; dadurch ist die Mengenübergabe zwischen Arbeitsgängen nachvollziehbar. |
| Vorh. AG Gebuchte Menge / Vorh. AG Gebuchte KG / Vorh. AG Gebuchte Meter / Vorh. AG Gebuchte Stück *(ausgeblendet)* | Zeigen die im vorherigen Arbeitsgang gebuchten Mengen; bei aktiviertem **Menge in Erw. Rückmeldung übertragen** werden sie als Vorschlag übernommen. |
| Lagerortcode / Lagerplatzcode | Zeigen das Lager der Charge; beim Buchen ggf. automatisch aus der Vormaterialzeile übernommen, wenn **Lagerort/Lagerplatz automatisch für Fertigungschargen ändern** gesetzt ist. |
| Chargennr. | Zeigt die vergebene Chargennummer; per Absprung gelangen Sie auf die Chargennummerninformationen. |
| Fertigungschargennr. | Zeigt die Fertigungschargennummer der produzierten Charge. |
| Gebucht | Zeigt, ob die Charge bereits gebucht wurde. |
| Ausgleich mit Lfd. Nr. *(ausgeblendet)* | Zeigt den Bezug zum ausgleichenden Artikelposten; dadurch ist die buchhalterische Verbindung nachvollziehbar. |
| Lieferantenchargennr. *(ausgeblendet)* | Zeigt die Lieferantenchargennummer des Materials der Charge. |

**Aktionen:** **Chargennr. zuweisen** (vergibt bzw. wählt die Chargennummer) und **Chargenbemerkung** (öffnet die Bemerkungen zur Charge).

#### Unterseite FA-Arbeitsvorrat Restechargen

Dieser Bereich erscheint, wenn an der Arbeitsplatzgruppe **Erw. Rückmeldung Restechargen** gesetzt ist. Er führt nutzbares Restmaterial als **Restecharge** weiter und enthält dieselben Mengen- und Lagerfelder wie die Charge sowie zusätzlich die Materialangleichfelder (**Tatsächliche KG pro Meter**, **Tatsächliche KG pro Stück**, **Materialangleichfaktor KG pro Meter/Stück**). Die Aktionen **Chargennr. zuweisen** und **Chargenbemerkung** stehen ebenfalls bereit. Die Eigenschaften der markierten Restecharge zeigt die Factbox **Restechargeneigenschaften**.

#### Schrotte

**Einstieg:** Aktion **Schrotte** in der **FA-Arbeitsvorrat Vormaterialien**. Die Aktion ist aktiv, wenn zu Vormaterial mindestens ein Schrottartikel existiert und — bei **Automatischer Schrottdifferenzermittlung** und mehreren Schrottzeilen — die Seite editierbar ist.

| Feld | Erläuterung |
|---|---|
| Schrottartikelnr. | Zeigt den Schrottartikel; dadurch ist eindeutig, als welcher Artikel der Schrott gebucht wird. |
| Menge / Reg. Menge | Zeigen die erfasste bzw. registrierte Schrottmenge; dadurch ist der gemeldete Schrott der Zeile nachvollziehbar. |
| Beschreibung | Zeigt die Beschreibung des Schrottartikels. |

#### Factboxen

| Factbox | Erläuterung |
|---|---|
| Geb. Mengenbilanz | Bilanziert je gewählter Einheit (über **Menge als**: Basiseinheit, KG, Stück, Meter) **Vormaterialmenge** minus **Chargenmenge** minus **Rest. Chargenmenge** minus **Schrottmenge** und zeigt das Ergebnis als **= Mengenbilanz**. Ein Wert von 0 bestätigt eine ausgeglichene Rückmeldung; eine Abweichung wird hervorgehoben. Über **Anzeigen als** wechseln Sie die Einheit. |
| Mengen | Zeigt je Charge die Stahlmengen (**Fertig-KG**, **Fertig-Meter**, **Fertig-Stück**, **Fertigmenge**), die Rest- und gebuchten Mengen sowie die aktuellen Werte; dadurch behält der Anwender den Mengenüberblick beim Erfassen. |
| Chargen | Zeigt je Charge **Int. Chargennr.**, Menge und gebuchte Menge; dadurch ist der Chargenüberblick beim Erfassen sichtbar. |
| Chargeneigenschaften / Restechargeneigenschaften | Zeigen die Materialeigenschaften der jeweils markierten Charge bzw. Restecharge (siehe *Stammdaten*). |

---

## Buchung, Umlagerung und Schrott

**Einrichtungsbezug:** Ob die Buchungsseite erscheint, steuert **Buchungsseite ausblenden** an der Arbeitsplatzgruppe; ob das Umlagerungsziel editierbar ist, steuert **Vormaterialverbrauch buchen**; wie Schrott gebucht wird, steuern **Automatische Schrottdifferenzermittlung** und **Direkte Schrottbuchung** (siehe *Einrichtung*).

### Buchungsablauf

1. Markieren Sie auf **FA-Arbeitsvorrat** die Zeile (Status **Gestartet**) und öffnen Sie über **Erw. Rückmeldung** die Seite **FA-Arbeitsvorrat Vormaterialien**.
2. Füllen Sie die Bereiche (**Buchungszeitraum**, Vormaterial, **FA-Arbeitsvorrat Chargen**, **FA-Arbeitsvorrat Restechargen**, **Schrotte**) und schließen Sie mit **OK**.
3. Beim Buchen prüft das Modul, ob Mengen vorhanden sind. Sind Chargen-, Vormaterial- oder Restechargenmengen erfasst, erscheint — sofern **Buchungsseite ausblenden** nicht gesetzt ist — die Seite **FA-Arbeitsvorrat Buchung** zur Kontrolle.
4. Sind keine Ringe/Teile mit Menge erfasst, fragt das Modul „Keine Ringe/Teile mit Menge gefunden. Nur Zeit wird gebucht! Fortsetzen?". Bestätigen Sie, wenn nur die Zeit gebucht werden soll.
5. Bestätigen Sie auf **FA-Arbeitsvorrat Buchung** mit **OK**. Das Modul schreibt in fester Reihenfolge fort: **zuerst** den Vormaterialverbrauch, **danach** die Chargen (fertiggestellte Menge, am letzten Arbeitsgang), **schließlich** die Restechargen als neue Anarbeitung. Schrott wird bei Status **Beendet** mitgebucht.
6. Schließen Sie den Arbeitsgang über die Aktion **Teilbeenden** (Status **Teilbeendet**, weitere Teilrückmeldungen möglich) oder **Beenden** (Status **Beendet**) auf der Übersicht ab.

Eine Teilrückmeldung ist zulässig: Über **Teilbeenden** erhält der Arbeitsgang den Status **Teilbeendet** und kann weitere Teilmengen aufnehmen, bis er mit **Beenden** abgeschlossen wird. Es gibt **keine** Regel, die das Abschließen erst bei ausgeglichener Bilanz zulässt; die **Geb. Mengenbilanz** dient ausschließlich der Kontrolle.

### Buchungsseite — FA-Arbeitsvorrat Buchung

**Einstieg:** Erscheint beim Buchen aus der erweiterten Rückmeldung, sofern **Buchungsseite ausblenden** nicht gesetzt ist. Brechen Sie die Seite ab, bereinigt das Modul den angefangenen Buchungssatz. Die Stahlerweiterung ergänzt die Basis-Buchungsseite um die Stahleinheiten und die bereits fertiggestellten Mengen.

| Feld | Erläuterung |
|---|---|
| KG / Meter / Stück | Zeigen die zu buchende Fertigmenge je Stahleinheit zusätzlich zur Basismenge; dadurch kontrolliert der Anwender vor der Buchung Gewicht, Länge und Stückzahl. |
| Gebuchte KG / Gebuchte Meter / Gebuchte Stück | Zeigen die bereits fertiggestellten Mengen je Stahleinheit (schreibgeschützt, je Arbeitsgang berechnet); dadurch ist der gebuchte Fortschritt vor der weiteren Buchung sichtbar. |

> **Bypass:** Ist **Buchungsseite ausblenden** an der Arbeitsplatzgruppe (bzw. der Zeile) gesetzt, dann wird die Seite **FA-Arbeitsvorrat Buchung** übersprungen; das Modul bucht mit den in der erweiterten Rückmeldung erfassten Werten im Hintergrund. Der Anwender bestätigt dann nur die erweiterte Rückmeldung mit **OK** (und ggf. die Rückfrage „Keine Ringe/Teile mit Menge …").

### Umlagerung — FA-Arbeitsvorrat Umlagerungszeilen

**Einrichtungsbezug:** Diese Seite und ihre Aktion stehen nur bereit, wenn an der Arbeitsplatzgruppe die Option **Umlagerung** gesetzt ist. Ob das Zielfeld **Nach Lagerortcode** editierbar ist, hängt von **Vormaterialverbrauch buchen** ab: ist der Verbrauch gesetzt, sind **Nach Lagerortcode** und **Nach Lagerplatzcode** gesperrt.

**Einstieg:** Markieren Sie auf **FA-Arbeitsvorrat** die Zeile und öffnen Sie über die Aktion **Umlagerung** die Seite **FA-Arbeitsvorrat Umlagerungszeilen**.

| Feld | Erläuterung |
|---|---|
| Artikelnr. / Chargennr. / Variantencode | Bestimmen das umzulagernde Vormaterial chargengenau. |
| Von Lagerortcode / Nach Lagerortcode | Legen Quell- und Ziel-Lagerort der Umlagerung fest; **Nach Lagerortcode** ist bei aktiviertem **Vormaterialverbrauch buchen** gesperrt, da das Material direkt verbraucht wird. |
| Menge | Erfasst die umzulagernde Basismenge; bei aktiviertem **Menge aus Restmenge für Umlagerung setzen** wird die offene Restmenge vorgeschlagen. |
| KG / Meter / Stück | Erfassen die Umlagerungsmenge in der jeweiligen Stahleinheit; dadurch wird auch chargengeführtes Stahlmaterial einheitengenau umgelagert. |
| KG pro Meter / KG per Stück *(ausgeblendet)* | Zeigen die Umrechnungsfaktoren der Zeile; dadurch bleiben die Stahleinheiten konsistent. |
| Restmenge / Rest-KG / Rest-Meter / Rest-Stück | Zeigen die noch nicht umgelagerte Menge je Einheit; dadurch erkennt der Anwender den offenen Umlagerungsbedarf. |
| Gebuchte KG / Gebuchte Meter / Gebuchte Stück | Zeigen die bereits umgelagerte Menge je Einheit (schreibgeschützt). |
| Verbrauchsmenge / Verbrauch KG / Verbrauch Meter / Verbrauch Stück *(ausgeblendet)* | Zeigen den im Zuge der Umlagerung gebuchten Verbrauch je Einheit, wenn **Vormaterialverbrauch buchen** aktiv ist. |
| Arbeitsplatzgruppennr. | Zeigt die Arbeitsplatzgruppe der Umlagerungszeile; dadurch ist der Arbeitsplatzbezug eindeutig. |

**Aktionen:** **Materialbestandssuche starten** (baut die Umlagerungszeilen aus der Materialbestandssuche auf; bestätigt mit der Rückfrage „… Einträge übertragen?") und **Chargenauswahl** (übernimmt eine Charge aus den Chargennummerninformationen).

### Schrott

Schrott entsteht in der erweiterten Rückmeldung über das Feld **Schrottmenge** oder die Aktion **Schrotte** und wird beim Buchen mit Status **Beendet** fortgeschrieben. Bei **Automatischer Schrottdifferenzermittlung** berechnet das Modul den Schrott als Gewichtsdifferenz; bei **Direkter Schrottbuchung** wird der Schrottartikel sofort bestandswirksam. Die entstehenden Schrottposten sind mit **Von FA-Arbeitsvorrat** gekennzeichnet (siehe *Historie, Archiv und Nachverfolgung*).

---

## Historie, Archiv und Nachverfolgung

Das Modul nutzt mehrere Nachverfolgungspunkte, um die gebuchten Stahlmengen und Chargen dauerhaft sichtbar zu machen.

### FA-Arbeitsvorratereignisse

**Einstieg:** Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorratereignisse**. Sie zeigt je Arbeitsereignis die Zeitdaten, den Status und — durch die Stahlerweiterung — die gemeldeten Stahleinheiten und den gebuchten Vormaterialverbrauch.

| Feld | Erläuterung |
|---|---|
| KG / Meter / Stück | Zeigen die im Ereignis gemeldete Menge in KG, Metern bzw. Stück; dadurch ist je Rückmeldung der Stahlbezug nachvollziehbar. |
| Verbrauchsmenge | Zeigt den im Ereignis gebuchten Vormaterialverbrauch in der Basiseinheit; dadurch ist je Rückmeldung sichtbar, wie viel Material verbraucht wurde. |
| Verbrauchs-KG / Verbrauchs-Meter / Verbrauchs-Stück | Zeigen den gebuchten Verbrauch in KG, Metern bzw. Stück; dadurch ist der Materialverbrauch einheitengenau dokumentiert. |

Die Basisspalten dieser Seite (Erstellt von, Datum/Uhrzeit, Status, Rüstzeit, Bearbeitungszeit, Zeitbuchung) stehen unverändert zur Verfügung.

### FA-Schrottposten

**Einstieg:** Öffnen Sie über **Suchen** die Seite **FA-Schrottposten**. Sie zeigt die gebuchten Schrottmengen. Die Stahlerweiterung ergänzt das Kennzeichen:

| Feld | Erläuterung |
|---|---|
| Von FA-Arbeitsvorrat | Wenn gesetzt, dann stammt der Schrottposten aus einer Rückmeldung im FA-Arbeitsvorrat; dadurch unterscheiden Sie aus der Stahlrückmeldung entstandenen Schrott von anderweitig erfasstem Schrott. |

### Archiv beendeter Zeilen

Ist auf **FA-Arbeitsvorrat Einrichtung** das Feld **Beendete Zeilen archivieren** auf **Beim Beenden des Fertigungsauftrags** gesetzt, dann archiviert das Modul beim Beenden des Fertigungsauftrags die zugehörigen Rückmeldedaten in die Archivtabellen **Arch. Fertigungschargen**, **Arch. Fertigungsmaterial** sowie die Archivsätze für Restechargen und Schrott. Dadurch bleiben die Stahlmengen und Chargen auch nach dem Auftragsabschluss nachvollziehbar.

---

## FAQ und Troubleshooting

### 1. Warum sehe ich die Aktion Erw. Rückmeldung im FA-Arbeitsvorrat nicht?
Die Aktion wird nur eingeblendet, wenn an der zugehörigen Arbeitsplatzgruppe **Erw. Rückmeldung** aktiviert ist. Prüfen Sie die Zeile auf der Seite **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**. Außerdem muss der Arbeitsgang den Status **Gestartet** haben.

### 2. Warum kann ich Start- und Endzeit nicht ändern?
Die Bearbeitbarkeit hängt von der Basisoption **Zeitbuchung** und vom Kennzeichen **Startdatum/-zeit änderbar** ab. Bei **Keine** bleiben alle Zeitfelder gesperrt; bei **Sollzeit** und **Mengenabhängige Sollzeit** sind die Datums-/Uhrzeitfelder gesperrt, bei **Sollzeit** sind nur **Rüstzeit** und **Bearbeitungszeit** frei. Prüfen Sie die Konfiguration auf der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**.

### 3. Warum erscheint eine Fehlermeldung zum Resteartikel?
Das Modul meldet „Resteartikel muss in den Artikelstammdaten definiert sein!", wenn die globale Option **Resteartikel erforderlich** gesetzt ist und am Ausgangsartikel keine **Resteartikelnr.** hinterlegt wurde. Pflegen Sie zunächst den Resteartikel an der **Artikelkarte** (siehe *Stammdaten*), bevor Sie eine **Restecharge** anlegen.

### 4. Warum ist das Feld Schrottmenge nicht bearbeitbar?
Bei aktivierter **Automatische Schrottdifferenzermittlung** wird die direkte Eingabe gesperrt, weil der Schrott automatisch als Gewichtsdifferenz ermittelt wird. Arbeiten Sie dann über die Aktion **Schrotte** oder prüfen Sie die Optionen auf der **FA-Arbeitsvorrat Arbeitsplatzgruppeneinrichtung**.

### 5. Warum wurde mein Schrott Lagerplatzcode zurückgesetzt?
Wenn Sie den **Schrott Lagerortcode** ändern, leert das Modul automatisch den **Schrott Lagerplatzcode**, damit keine ungültige Lagerortkombination entsteht. Setzen Sie den Lagerplatz nach dem Wechsel des Lagerorts neu.

### 6. Warum erscheint beim Buchen die Meldung „Keine Ringe/Teile mit Menge"?
Das Modul stellt diese Frage, wenn beim Buchen aus der erweiterten Rückmeldung keine Chargen-, Vormaterial- oder Restechargenmengen erfasst sind. Bestätigen Sie, wenn nur die Zeit gebucht werden soll; andernfalls brechen Sie ab und erfassen die Mengen.

### 7. Warum sehe ich beim Buchen keine Seite FA-Arbeitsvorrat Buchung?
An der Arbeitsplatzgruppe ist **Buchungsseite ausblenden** gesetzt. Dann läuft der Buchungsschritt mit den erfassten Werten im Hintergrund; Sie bestätigen nur die erweiterte Rückmeldung mit **OK**. Entfernen Sie das Kennzeichen, wenn Sie vor jeder Buchung Menge, KG, Meter, Stück, Lagerort und Lagerplatz kontrollieren möchten.

### 8. Warum ist das Zielfeld Nach Lagerortcode in den Umlagerungszeilen gesperrt?
An der Arbeitsplatzgruppe ist **Vormaterialverbrauch buchen** aktiviert. Dann wird das Material direkt verbraucht statt umgelagert, und das Umlagerungsziel (**Nach Lagerortcode**, **Nach Lagerplatzcode**) ist nicht editierbar. Ohne dieses Kennzeichen können Sie das Ziel-Lager wählen.

### 9. Warum kann ich das Kennzeichen Resteartikel an der Artikelkarte nicht entfernen?
Das Modul meldet „Artikel wird als Resteartikel in anderen Artikeln verwendet!", solange andere Artikel diesen Artikel als **Resteartikelnr.** referenzieren. Entfernen Sie zuerst die Verweise an den nutzenden Artikeln, danach lässt sich das Kennzeichen abschalten.

### 10. Warum übernimmt der neue Arbeitsgang die Chargenmengen des vorherigen nicht?
Die Mengenübergabe zwischen Arbeitsgängen erfolgt nur, wenn an der Arbeitsplatzgruppe **Menge in Erw. Rückmeldung übertragen** gesetzt ist. Dann werden die im vorherigen Arbeitsgang gebuchten Chargenmengen als Vorschlag übernommen (Felder **Vorh. AG Gebuchte …**); ohne das Kennzeichen erfassen Sie die Mengen erneut.

---

## Typische Anwendungsfälle

### 1. Rückmeldung eines vormaterialgeführten Arbeitsgangs

**Auslöser:** An einem Stahlarbeitsplatz wird ein Arbeitsgang abgeschlossen; die Rückmeldung muss Vormaterial und Chargen berücksichtigen.

**Einstieg in BC:** Öffnen Sie über **Suchen** die Seite **FA-Arbeitsvorrat**.

**Kernablauf:**
1. Grenzen Sie die Liste auf Ihre **Arbeitsplatzgruppe** ein, wählen Sie die passende Zeile und prüfen Sie **Status** (muss **Gestartet** sein) sowie den Artikelbezug.
2. Prüfen Sie **Fertig-KG**, **Fertig-Meter** und **Fertig-Stück**, um den Produktionsfortschritt zu bewerten.
3. Öffnen Sie über die Aktion **Erw. Rückmeldung** die Seite **FA-Arbeitsvorrat Vormaterialien**.
4. Kontrollieren Sie die Vormaterialzeile; wählen Sie die Charge über **Chargenauswahl** oder bauen Sie die Zeilen über **Materialbestandssuche starten** auf.
5. Ergänzen Sie die Mengen in **Menge**, **KG**, **Meter** oder **Stück**; legen Sie über **Charge erstellen** die produzierte Charge an.
6. Prüfen Sie in der Factbox **Geb. Mengenbilanz**, ob Vormaterial, Chargen und Schrott zur **= Mengenbilanz** passen.
7. Buchen Sie mit **OK**. Ist **Buchungsseite ausblenden** nicht gesetzt, kontrollieren Sie auf **FA-Arbeitsvorrat Buchung** Menge, KG, Meter, Stück, Lagerort und Lagerplatz und bestätigen mit **OK**.
8. Schließen Sie über **Teilbeenden** (weitere Teilmengen möglich) oder **Beenden** ab.

**Abschluss:** Prüfen Sie in der Übersicht **FA-Arbeitsvorrat** die aktualisierten Felder **Fertiggestellte KG**, **Fertiggestellte Meter** und **Fertiggestellte Stück**. Die Buchung ist in den **FA-Arbeitsvorratereignissen** nachvollziehbar. Bei Teilrückmeldung steht die Zeile auf **Teilbeendet** und kann weitere Teilmengen aufnehmen, bis Sie mit **Beenden** abschließen.

### 2. Restmaterial als Restecharge weiterführen

**Auslöser:** Nach der Bearbeitung bleibt nutzbares Vormaterial übrig, das nicht als Schrott enden soll.

**Einstieg in BC:** Öffnen Sie **FA-Arbeitsvorrat**, markieren Sie die Zeile (Status **Gestartet**) und starten Sie die Aktion **Erw. Rückmeldung**.

**Kernablauf:**
1. Erfassen Sie in der **FA-Arbeitsvorrat Vormaterialien** das verbrauchte Vormaterial und die produzierte Charge wie in Fall 1.
2. Legen Sie über **Restecharge erstellen** die **Restecharge** für die verbleibende Menge an; die Unterseite **FA-Arbeitsvorrat Restechargen** wird eingeblendet (Voraussetzung: **Erw. Rückmeldung Restechargen** an der Arbeitsplatzgruppe).
3. Pflegen Sie die Mengen der Restecharge und prüfen Sie in **Geb. Mengenbilanz**, dass Vormaterial = Charge + Restecharge + Schrott aufgeht.
4. Buchen Sie und schließen Sie ggf. mit **Teilbeenden** oder **Beenden** ab.

**Abschluss:** Ist am Ausgangsartikel die **Resteartikelnr.** gepflegt (bzw. **Resteartikel erforderlich** erfüllt), läuft die Restecharge auf den Resteartikel. Die Restecharge steht im Folgeprozess als Vormaterial bereit; ihre Eigenschaften sehen Sie in der Factbox **Restechargeneigenschaften**.

### 3. Vormaterial vor dem Verbrauch umlagern

**Auslöser:** Das benötigte Vormaterial liegt an einem anderen Lagerort/Lagerplatz und muss vor dem Verbrauch umgelagert werden.

**Einstieg in BC:** Öffnen Sie **FA-Arbeitsvorrat**, markieren Sie die Zeile und starten Sie die Aktion **Umlagerung** (nur sichtbar, wenn an der Arbeitsplatzgruppe **Umlagerung** gesetzt ist).

**Kernablauf:**
1. Bauen Sie in den **FA-Arbeitsvorrat Umlagerungszeilen** die Zeilen über **Materialbestandssuche starten** auf und bestätigen Sie „… Einträge übertragen?", oder wählen Sie über **Chargenauswahl** eine Charge.
2. Prüfen Sie **Von Lagerortcode** und **Nach Lagerortcode**; ist **Vormaterialverbrauch buchen** aktiv, ist das Ziel-Lager gesperrt und das Material wird direkt verbraucht.
3. Erfassen Sie **Menge**, **KG**, **Meter** oder **Stück**; bei aktiviertem **Menge aus Restmenge für Umlagerung setzen** wird die offene Restmenge vorgeschlagen.

**Abschluss:** Die umgelagerten bzw. verbrauchten Mengen erscheinen als **Gebuchte KG/Meter/Stück**; das Vormaterial steht anschließend für die Rückmeldung am Ziel-Lager bereit.
