---
title: Anwenderhandbuch m+m Undoing Production
---

# Anwenderhandbuch m+m Undoing Production

## Einleitung

Die Erweiterung **m+m Undoing Production** bietet innerhalb von Microsoft Dynamics 365 Business Central eine komfortable Möglichkeit, bereits gebuchte Produktionsrückmeldungen wieder zurückzunehmen. Über eine einzige Aktion im **Produktions Buch.-Blatt** eines freigegebenen **Fertigungsauftrags** lassen sich gebuchte **Verbrauchsbuchungen**, gebuchte **Ist-Meldungen** (Fertigmengen) und gebuchte **Zeiten** gezielt stornieren. Die Erweiterung erzeugt dabei keine Direktbuchung, sondern legt im Produktions Buch.-Blatt entsprechende **negative Gegenzeilen** an, die der Anwender anschließend selbst bucht.

**Zielgruppe:** Primär richtet sich die Erweiterung an **operative Anwender in der Fertigung** – Werker, Fertigungssteuerung und Rückmeldeplätze –, die im Tagesgeschäft Rückmeldungen erfassen und fehlerhafte Buchungen korrigieren müssen. Sekundär betrifft sie Administratoren, die die Erweiterung installieren und die Berechtigung zuweisen.

**Kurzer Prozessüberblick:** Der Anwender öffnet zu einem freigegebenen Fertigungsauftrag das **Produktions Buch.-Blatt**, wählt die Aktion **Buchung stornieren**, entscheidet über Optionen, *welche* Buchungsarten storniert werden sollen, wählt in den anschließend geöffneten Postenlisten die konkret zu stornierenden Posten aus und bucht abschließend das Produktions Buch.-Blatt. Die App richtet sich ausschließlich an noch nicht abgeschlossene Buchungen; für bereits abgeschlossene (beendete) Rückmeldungen ist sie nicht vorgesehen.

## Schnellstart für Anwender

Der schnellste Weg von einer fehlerhaften Rückmeldung zur Korrektur:

1. Öffnen Sie den betreffenden **freigegebenen Fertigungsauftrag** und rufen Sie zu der gewünschten Zeile das **Produktions Buch.-Blatt** auf.
2. Wählen Sie im Produktions Buch.-Blatt die Aktion **Buchung stornieren**.
3. Setzen Sie im Abschnitt **Allgemein** die gewünschten Optionen: **Verbrauchsbuchung stornieren** und/oder **Ist-Meldung stornieren**. Aktivieren Sie darunter je nach Bedarf **Menge stornieren** (im Abschnitt **Verbrauchsbuchung**) sowie **Menge stornieren** und/oder **Zeiten stornieren** (im Abschnitt **Ist-Meldung**). Bestätigen Sie mit **OK**.
4. Bestätigen Sie die Rückfrage, dass zunächst alle vorhandenen Buch.-Blattzeilen gelöscht werden.
5. Wählen Sie in den daraufhin geöffneten Listen **Artikelposten** bzw. **Kapazitätsposten** die konkret zu stornierenden Posten aus und bestätigen Sie jeweils mit **OK**. Es können einzelne, keine oder alle Zeilen ausgewählt werden.
6. Prüfen Sie die im Produktions Buch.-Blatt neu eingefügten negativen Zeilen.
7. Wählen Sie **Buchen**, damit die Stornobuchungen tatsächlich erzeugt werden.

Für die Nutzung ist keine zusätzliche Einrichtung erforderlich (siehe Kapitel **Einrichtung**). Der ausführliche Ablauf mit allen Optionen und Rückfragen ist im Kapitel **Buchung stornieren – Ablauf im Produktions Buch.-Blatt** beschrieben.

## Einrichtung

Für den Einsatz der Erweiterung im Webclient von Microsoft Dynamics 365 Business Central ist **keine zusätzliche fachliche Einrichtung** erforderlich. Es existieren weder eine eigene Einrichtungsseite noch Nummernserien oder Stammdaten, die vor der ersten Nutzung zu pflegen wären. Die Funktion **Buchung stornieren** steht unmittelbar zur Verfügung, sobald die Erweiterung installiert und die Berechtigung zugewiesen ist.

### Installation und Voraussetzungen

Voraussetzung für die Nutzung ist, dass die Erweiterung **m+m Undoing Production** in der **Erweiterungsverwaltung** installiert ist. Die Erweiterung setzt die Basiserweiterung **m+m Cloud Base** desselben Herstellers voraus; diese Abhängigkeit wird bei der Installation automatisch mit aufgelöst. Beim Anmelden führt die Erweiterung im Hintergrund eine Lizenzprüfung über das Bezahlmodul der Basiserweiterung aus; für den Anwender ist hierzu keine Aktion nötig.

Wenn die Erweiterung installiert und lizenziert ist, dann steht in jedem **Produktions Buch.-Blatt** die Aktion **Buchung stornieren** zur Verfügung – ohne weitere Konfiguration.

### Berechtigungen

Die Erweiterung liefert ein eigenes Berechtigungsset aus, das die Ausführung der Stornofunktion freischaltet. Weisen Sie dieses Berechtigungsset den Anwendern zu, die Produktionsbuchungen zurücknehmen dürfen.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Berechtigungsset **All permissions** (m+m Undoing Production) | Legt fest, welche Anwender die Stornofunktion ausführen dürfen. Wenn das Set einem Benutzer zugewiesen ist, dann kann dieser die Aktion **Buchung stornieren** aufrufen und den zugehörigen Korrekturlauf ausführen; ohne dieses Set bleibt die Funktion für den Benutzer wirkungslos. Das Set bestimmt die Berechtigungen für die Ausführung des internen Korrekturmoduls und des Korrekturlaufs. |

Die Zuweisung erfolgt über die Standard-Berechtigungsverwaltung von Business Central (Benutzer bzw. Berechtigungssätze). Es sind keine feldbezogenen Zusatzberechtigungen zu pflegen.

## Buchung stornieren – Ablauf im Produktions Buch.-Blatt

Dieses Kapitel beschreibt die zentrale und einzige transaktionale Funktion der Erweiterung. Die Funktion setzt an den Standardobjekten von Business Central an: Der Einstieg erfolgt über das **Produktions Buch.-Blatt** eines freigegebenen Fertigungsauftrags, die Auswahl der zu stornierenden Posten erfolgt in den Standardlisten **Artikelposten** und **Kapazitätsposten**. Die Erweiterung fügt dort keine zusätzlichen Felder oder Spalten hinzu; sie ergänzt ausschließlich die Aktion **Buchung stornieren** und den zugehörigen Auswahldialog.

### Einstieg

**Einstieg:** Öffnen Sie einen **freigegebenen Fertigungsauftrag**, rufen Sie zur gewünschten Fertigungsauftragszeile das **Produktions Buch.-Blatt** auf und wählen Sie dort die Aktion **Buchung stornieren**. Die Aktion ist im Menüband des Produktions Buch.-Blatts direkt nach der Standardaktion zum Buchen und Drucken angeordnet.

### Optionen der Aktion „Buchung stornieren“

Nach dem Aufruf der Aktion öffnet sich ein Dialog mit den folgenden Optionen. Alle Optionen sind Schalter (aktiviert/nicht aktiviert); ihre Erläuterung beschreibt, was bei Aktivierung im weiteren Ablauf geschieht.

| Feld | Erläuterung |
|------|-------------|
| **Verbrauchsbuchung stornieren** (Abschnitt **Allgemein**) | Wenn aktiviert, dann werden im weiteren Ablauf die gebuchten **Verbrauchsbuchungen** der Komponenten zur Stornierung angeboten. Erst mit dieser Option wird der untere Abschnitt **Verbrauchsbuchung** wirksam. Wird die Option wieder deaktiviert, dann wird die darunterliegende Option **Menge stornieren** automatisch zurückgesetzt. |
| **Ist-Meldung stornieren** (Abschnitt **Allgemein**) | Wenn aktiviert, dann werden im weiteren Ablauf die gebuchten **Ist-Meldungen** des Fertigartikels (gemeldete Mengen und/oder Zeiten) zur Stornierung angeboten. Erst mit dieser Option werden die Optionen im Abschnitt **Ist-Meldung** wirksam. Wird die Option wieder deaktiviert, dann werden die Optionen **Menge stornieren** und **Zeiten stornieren** automatisch zurückgesetzt. |
| **Menge stornieren** (Abschnitt **Verbrauchsbuchung**) | Wenn aktiviert, dann werden die gebuchten **Verbrauchsmengen** durch eine Gegenbuchung storniert; das System öffnet zur Auswahl die Liste der Verbrauchs-Artikelposten des Fertigungsauftrags. Die Option ist nur bearbeitbar, wenn zuvor **Verbrauchsbuchung stornieren** aktiviert wurde. |
| **Menge stornieren** (Abschnitt **Ist-Meldung**) | Wenn aktiviert, dann werden die gebuchten **Ist-Mengen** (gemeldete Fertigmengen) durch eine Gegenbuchung storniert; das System öffnet zur Auswahl die Liste der offenen Ist-Meldungs-Artikelposten des Fertigungsauftrags. Die Option ist nur bearbeitbar, wenn zuvor **Ist-Meldung stornieren** aktiviert wurde. |
| **Zeiten stornieren** (Abschnitt **Ist-Meldung**) | Wenn aktiviert, dann werden die gebuchten **Rüst-, Bearbeitungs- und Stoppzeiten** der Ist-Meldungen durch eine Gegenbuchung storniert; das System öffnet zur Auswahl die Liste der **Kapazitätsposten** des Fertigungsauftrags. Die Option ist nur bearbeitbar, wenn zuvor **Ist-Meldung stornieren** aktiviert wurde. |

Werden im Dialog weder **Verbrauchsbuchung stornieren** noch **Ist-Meldung stornieren** gesetzt – oder wird zwar eine übergeordnete Option, aber keine der untergeordneten Mengen-/Zeitoptionen gesetzt – so bricht der Korrekturlauf ohne Änderung ab. Wählen Sie daher mindestens eine übergeordnete Option **und** die zugehörige Mengen- oder Zeitoption.

### Ablauf nach Bestätigung mit OK

Nach Bestätigung des Dialogs mit **OK** durchläuft der Korrekturlauf die folgenden Schritte:

1. **Buch.-Blatt leeren:** Zunächst werden – nach Rückfrage – alle vorhandenen Zeilen des aktuellen Produktions Buch.-Blatts gelöscht, ebenso die zu diesem Buch.-Blatt gehörenden Reservierungen. Dadurch startet die Stornierung mit einem leeren Buch.-Blatt.
2. **Rückfragen je Option:** Für jede gesetzte Option erscheint eine Rückfrage:
   - bei aktivierter Mengenstornierung der Verbrauchsbuchung: *„Wollen Sie die zu stornierenden Verbrauchsmengen auswählen?“*
   - bei aktivierter Mengenstornierung der Ist-Meldung: *„Wollen Sie die zu stornierenden Istmeldungsmengen auswählen?“*
   - bei aktivierter Zeitenstornierung: *„Wollen Sie die zu stornierenden Istmeldungszeiten auswählen?“*
3. **Postenauswahl:** Bestätigen Sie eine Rückfrage, dann öffnet sich die zugehörige Standardliste im Auswahlmodus:
   - **Ist-Meldung – Menge:** die Liste **Artikelposten**, gefiltert auf offene Ist-Meldungsposten (Postenart Ist-Meldung) des Fertigungsauftrags.
   - **Zeiten:** die Liste **Kapazitätsposten** des Fertigungsauftrags (nur Posten mit einer Menge ungleich null).
   - **Verbrauchsbuchung – Menge:** die Liste **Artikelposten**, gefiltert auf Verbrauchsposten (Postenart Verbrauch) des Fertigungsauftrags.
   Markieren Sie die zu stornierenden Posten und bestätigen Sie mit **OK**. Es lassen sich einzelne, keine oder alle Posten markieren.
4. **Reservierungsprüfung (nur Ist-Menge):** Bestehen zu den ausgewählten Ist-Meldungsposten noch **Reservierungen** zu abhängigen Belegen, dann erscheint die Rückfrage *„Es existieren Reservierungen zu abhängigen Belegen. Wollen Sie fortfahren und die vorhandenen Reservierungen löschen?“*. Wird bestätigt, dann werden die betreffenden Reservierungen aufgehoben; wird abgelehnt, dann bleibt die Auswahl unverändert und es wird nicht storniert.
5. **Gegenzeilen erzeugen:** Entsprechend der Auswahl fügt das System in das Produktions Buch.-Blatt neue Zeilen mit **negativen Werten** ein (negative Fert.-Menge, negativer Verbrauch bzw. negative Rüst-/Bearbeitungs-/Stoppzeiten). Chargen- und Seriennummern der Ursprungsposten werden dabei über Reservierungseinträge übernommen; Zeilen zu bereits beendeten Arbeitsgängen werden intern als erledigt gekennzeichnet.
6. **Buchen:** Die erzeugten Gegenzeilen sind zunächst nur Vorschläge. Wählen Sie im Produktions Buch.-Blatt **Buchen**, damit die eigentlichen Stornobuchungen erzeugt und die Posten korrigiert werden.

### Auswirkungen der Stornierung

- **Artikelposten:** Für stornierte Verbrauchs- und Ist-Mengen entstehen mit dem Buchen ausgleichende Artikelposten mit umgekehrtem Vorzeichen. Bei Chargen- oder seriennummerngeführten Artikeln wird die Rückbuchung über die Artikelverfolgung mit den ursprünglichen **Chargennr.** bzw. **Seriennr.** verknüpft.
- **Kapazitätsposten:** Für stornierte Zeiten entstehen Kapazitätsposten mit negativen **Rüstzeit-**, **Bearbeitungszeit-** und Stoppzeitwerten, sodass die zurückgemeldeten Zeiten des Fertigungsauftrags entlastet werden.
- **Reservierungen:** Zu den betroffenen Ist-Meldungsposten bestehende Reservierungen werden – nach Bestätigung – aufgehoben, damit die Rücknahme durchgeführt werden kann.

## FAQ und Troubleshooting

### Warum steht die Aktion „Buchung stornieren“ nur im Produktions Buch.-Blatt zur Verfügung?
Die Erweiterung ergänzt ausschließlich das **Produktions Buch.-Blatt** um diese Aktion, weil die Stornierung als negative Gegenbuchung genau über dieses Buch.-Blatt läuft. Sie erreichen die Aktion daher immer über einen freigegebenen Fertigungsauftrag und dessen Produktions Buch.-Blatt, nicht über die Suchen-Funktion.

### Was passiert, wenn ich im Dialog keine Option setze?
Setzen Sie weder **Verbrauchsbuchung stornieren** noch **Ist-Meldung stornieren** – oder eine übergeordnete Option ohne zugehörige Mengen-/Zeitoption –, dann bricht der Korrekturlauf ohne jede Änderung ab. Es werden keine Zeilen erzeugt und nichts gebucht.

### Warum werden zuerst alle vorhandenen Buch.-Blattzeilen gelöscht?
Der Korrekturlauf benötigt ein leeres Produktions Buch.-Blatt, um ausschließlich die Storno-Gegenzeilen aufzunehmen. Deshalb werden nach Rückfrage zunächst alle bestehenden Zeilen des Buch.-Blatts und die zugehörigen Reservierungen entfernt. Erfassen Sie noch benötigte, ungebuchte Zeilen bitte erst nach der Stornierung.

### Warum erzeugt die Stornierung nur Vorschlagszeilen und bucht nicht sofort?
Die Erweiterung legt bewusst nur **negative Gegenzeilen** an. So können Sie die vorgeschlagene Rücknahme vor dem Buchen prüfen und gegebenenfalls verwerfen. Erst mit **Buchen** entstehen die tatsächlichen Stornobuchungen.

### Warum erscheint die Meldung zu Reservierungen zu abhängigen Belegen?
Sind ausgewählte Ist-Meldungsposten noch für abhängige Belege reserviert, dann muss diese Reservierung zuvor aufgelöst werden. Die Rückfrage *„Es existieren Reservierungen zu abhängigen Belegen …“* gibt Ihnen die Kontrolle: Bestätigen Sie, dann werden die Reservierungen gelöscht und die Stornierung fortgesetzt; lehnen Sie ab, dann bleibt alles unverändert.

### Kann ich einzelne Posten gezielt stornieren?
Ja. In den geöffneten Listen **Artikelposten** bzw. **Kapazitätsposten** wählen Sie genau die Posten aus, die zurückgenommen werden sollen. Sie können einzelne, mehrere oder alle Posten markieren; nicht markierte Posten bleiben unverändert.

### Warum finde ich bei der Ist-Mengen-Stornierung nicht alle Posten?
Für die Stornierung der Ist-Menge bietet das System nur **offene** Ist-Meldungsposten des Fertigungsauftrags an. Bereits ausgeglichene oder geschlossene Posten stehen nicht zur Auswahl, da sie nicht mehr zurückgenommen werden können.

### Werden Chargen- und Seriennummern bei der Rücknahme berücksichtigt?
Ja. Sind die Ursprungsposten chargen- oder seriennummerngeführt, dann übernimmt die Erweiterung die **Chargennr.** bzw. **Seriennr.** über die Artikelverfolgung in die Gegenzeilen und verknüpft die Rückbuchung mit dem Ursprungsposten.

### Warum werden getrennte Optionen für Menge und Zeiten angeboten?
Ist-Meldungen enthalten sowohl gemeldete Mengen (über Artikelposten) als auch gemeldete Zeiten (über Kapazitätsposten). Mit **Menge stornieren** nehmen Sie die gemeldete Fertigmenge zurück, mit **Zeiten stornieren** die gemeldeten Rüst-, Bearbeitungs- und Stoppzeiten. So lassen sich Mengen- und Zeitkorrekturen unabhängig voneinander durchführen.

### Kann ich bereits abgeschlossene Fertigungsauftragszeilen stornieren?
Die Erweiterung ist für die Rücknahme noch nicht abgeschlossener Rückmeldungen gedacht. Für die Stornierung wird die zugehörige, freigegebene Fertigungsauftragszeile herangezogen; für vollständig abgeschlossene (beendete) Rückmeldungen ist der Korrekturlauf nicht vorgesehen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Falsch gemeldete Ist-Menge korrigieren

**Auslöser:** Ein Werker meldet der Fertigungssteuerung telefonisch, dass er an einem freigegebenen Fertigungsauftrag versehentlich eine zu hohe Fertigmenge zurückgemeldet und bereits gebucht hat.

**Einstieg in BC:** Die Fertigungssteuerung öffnet den betreffenden **freigegebenen Fertigungsauftrag**, ruft zur Fertigungsauftragszeile das **Produktions Buch.-Blatt** auf und wählt die Aktion **Buchung stornieren**.

**Kernablauf:**
1. Im Abschnitt **Allgemein** wird **Ist-Meldung stornieren** aktiviert; im Abschnitt **Ist-Meldung** wird **Menge stornieren** gesetzt. Bestätigen mit **OK**.
2. Die Rückfrage zum Leeren des Buch.-Blatts wird bestätigt.
3. Auf die Rückfrage *„Wollen Sie die zu stornierenden Istmeldungsmengen auswählen?“* öffnet sich die Liste **Artikelposten** mit den offenen Ist-Meldungsposten des Auftrags. Die falsch gebuchte Position wird markiert und mit **OK** bestätigt.
4. Besteht zu dem Posten noch eine Reservierung, wird die Reservierungs-Rückfrage bestätigt.
5. Das System fügt eine negative Ist-Meldungszeile in das Produktions Buch.-Blatt ein.

**Abschluss:** Die Fertigungssteuerung prüft die eingefügte Gegenzeile und wählt **Buchen**. Die zu hohe Fertigmenge ist damit über einen ausgleichenden Artikelposten zurückgenommen; anschließend kann die korrekte Menge neu zurückgemeldet werden.

### Anwendungsfall 2: Verbrauch und Zeiten eines Auftrags gemeinsam zurücknehmen

**Auslöser:** Per E-Mail meldet die Arbeitsvorbereitung, dass zu einem Fertigungsauftrag Komponentenverbrauch und Bearbeitungszeiten mit falschem Datum gebucht wurden und komplett zurückgenommen werden sollen, bevor korrekt neu gemeldet wird.

**Einstieg in BC:** Der Sachbearbeiter öffnet den **freigegebenen Fertigungsauftrag**, ruft das **Produktions Buch.-Blatt** auf und wählt **Buchung stornieren**.

**Kernablauf:**
1. Im Abschnitt **Allgemein** werden **Verbrauchsbuchung stornieren** und **Ist-Meldung stornieren** aktiviert.
2. Im Abschnitt **Verbrauchsbuchung** wird **Menge stornieren** gesetzt; im Abschnitt **Ist-Meldung** werden **Menge stornieren** und **Zeiten stornieren** gesetzt. Bestätigen mit **OK**.
3. Die Rückfrage zum Leeren des Buch.-Blatts wird bestätigt.
4. Nacheinander erscheinen die Rückfragen zu Istmeldungsmengen, Istmeldungszeiten und Verbrauchsmengen. Für jede bestätigte Rückfrage öffnet sich die passende Liste – **Artikelposten** für Mengen, **Kapazitätsposten** für Zeiten –, in der die betreffenden Posten markiert und mit **OK** übernommen werden.
5. Etwaige Reservierungen zu den Ist-Meldungsposten werden nach Rückfrage aufgelöst.
6. Das System fügt für alle Auswahlen negative Gegenzeilen (Verbrauch, Ist-Menge, Zeiten) in das Produktions Buch.-Blatt ein.

**Abschluss:** Der Sachbearbeiter prüft die Gegenzeilen und wählt **Buchen**. Verbrauch, Ist-Menge und Zeiten des Auftrags sind damit über ausgleichende Artikel- und Kapazitätsposten zurückgenommen; die Rückmeldung kann anschließend mit korrektem Datum neu erfasst werden.
