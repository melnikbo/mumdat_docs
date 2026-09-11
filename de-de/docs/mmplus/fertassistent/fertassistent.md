---
title: Anwenderhandbuch m+m Production Order Assistant
---

# Anwenderhandbuch m+m Production Order Assistant

Der **m+m Production Order Assistant** (in der Oberfläche: **Fertigungsassistent**) verbindet den Verkauf mit der Fertigung in Microsoft Dynamics 365 Business Central. Aus einer Verkaufszeile im **Verkaufsangebot** oder **Verkaufsauftrag** entsteht mit wenigen Schritten ein passender **Fertigungsauftrag** – wahlweise manuell über einen geführten Dialog oder automatisch bei der Auftragsfreigabe. Zusätzlich hält das Modul die Verbindung zwischen Verkaufsbeleg und Fertigungsauftrag über einen **Auftragsbezug** und einen **Check-Status** transparent.

Dieses Handbuch beschreibt die Einrichtung, die tägliche Arbeit und die typischen Abläufe. Alle Feld-, Aktions- und Seitenbezeichnungen entsprechen der deutschen Oberfläche.

## Einleitung

### Zweck des Moduls

Der Fertigungsassistent automatisiert und vereinfacht die Erstellung von Fertigungsaufträgen aus dem Verkauf. Er stellt sicher, dass ein Fertigungsauftrag denselben Bezug behält wie die auslösende Verkaufszeile (**Fert. Verwendungsart**, **Fert. Verwendungsnr.**, **Fert. Verwendungszeilennr.**), dass der zuständige Verkäufer über neue Fertigungsaufträge informiert wird und dass die Umwandlung eines Angebots in einen Auftrag nur dann möglich ist, wenn die verbundenen Fertigungsaufträge fachlich geprüft wurden.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender im Verkauf und in der Arbeitsvorbereitung**, die täglich Verkaufsbelege erfassen, freigeben und daraus Fertigungsaufträge anstoßen sowie deren **Check-Status** pflegen. Sekundär richtet sich das Kapitel **Einrichtung** an **Administratoren und Key-User**, die die unternehmensweiten Vorgaben einmalig festlegen.

### Kurzer Prozessüberblick

Der typische Weg verläuft entlang des Verkaufsbelegs bis zum Fertigungsauftrag:

1. Der Anwender erfasst im **Verkaufsangebot** oder **Verkaufsauftrag** eine Artikelzeile.
2. In der Verkaufszeile steuert das Kennzeichen **FA erstellen**, ob für diese Zeile ein Fertigungsauftrag entstehen soll.
3. Über die Aktion **Fertigungsassistent** in der Verkaufszeile öffnet der Anwender einen geführten Dialog und legt den Fertigungsauftrag mit **Arbeitsplan** und **Komponenten** an – oder der Fertigungsauftrag entsteht automatisch bei der **Freigabe** des Verkaufsauftrags.
4. Der erzeugte Fertigungsauftrag trägt einen **Check-Status** und einen **Auftragsbezug** zur Verkaufszeile; der Verkäufer wird bei Bedarf benachrichtigt.
5. Beim Umwandeln eines Angebots in einen Auftrag wandert der Fertigungsauftrag mit und erhält den für Aufträge vorgesehenen Status.

## Schnellstart für Anwender

Die folgende Reihenfolge folgt der technischen Abhängigkeit: zuerst die **Einrichtung**, dann die tägliche Arbeit am Verkaufsbeleg.

**A. Einmalige Einrichtung (Administrator).** Öffnen Sie über **Suchen** die Seite **Fertigungsassistent Einrichtung** und legen Sie mindestens fest: **FA-Status für Verkaufsangebote** und **FA-Status für Verkaufsaufträge**, ob **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen** aktiv sein soll und wie **"FA erstellen" in der Verkaufszeile vorbelegen** wirkt.

**B. Manuelle Erstellung im Verkaufsbeleg (Anwender).**

1. Öffnen Sie den **Verkaufsauftrag** (oder das **Verkaufsangebot**) und erfassen Sie eine Artikelzeile.
2. Prüfen Sie in der Zeile das Kennzeichen **FA erstellen** (standardmäßig gemäß Einrichtung vorbelegt).
3. Wählen Sie in der Verkaufszeile die Aktion **Fertigungsassistent**.
4. Prüfen und ergänzen Sie im Dialog **Menge**, **Arbeitsplannr.**, **Fälligkeitsdatum** sowie die Register **Arbeitsplan** und **Komponenten**.
5. Bestätigen Sie den Dialog mit **OK**. Der Fertigungsauftrag wird angelegt, erhält den in der Einrichtung vorgesehenen **FA-Status** sowie einen **Check-Status**, und der Verkäufer wird – falls aktiviert – benachrichtigt.

**C. Automatische Erstellung bei Freigabe (Anwender).**

1. Aktivieren Sie in der Einrichtung **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen**.
2. Geben Sie den **Verkaufsauftrag** frei.
3. Beantworten Sie – falls **Abfrage zur Erstellung von Fertigungsaufträgen innerhalb Verkaufsaufträgen** aktiv ist – die Rückfrage **"Fertigungsauftrag erstellen?"** mit **Ja**.
4. Für jede Artikelzeile mit **FA erstellen** = aktiviert entsteht ein Fertigungsauftrag im **FA-Status für Verkaufsaufträge**.

## Einrichtung

Die Einrichtung erfolgt zentral auf der Seite **Fertigungsassistent Einrichtung**. Sie ist eine unternehmensweite Einzelsatz-Einrichtung: Business Central legt den Satz beim ersten Öffnen automatisch an.

**Einstieg:** Öffnen Sie die Seite **Fertigungsassistent Einrichtung** über **Suchen**. Diese Seite ist unter **Verwaltung** eingeordnet und besitzt keine übergeordnete Stammdatenseite, die sie aufruft; der Einstieg über **Suchen** ist daher der vorgesehene Weg.

Alle Felder der Seite liegen im Register **Allgemein**. Da es sich um eine reine Einrichtungstabelle des Moduls handelt, sind sämtliche sichtbaren Felder unten dokumentiert – es gibt keine zusätzlichen Basisfelder auf diesem Bildschirm.

### Grundeinstellungen der Fertigungsassistent Einrichtung

**Wer richtet ein und wann:** Ein Administrator oder Key-User legt diese Werte einmalig vor der ersten Nutzung fest. Sie steuern sowohl die manuelle Erstellung über den **Fertigungsassistent** (siehe *Tägliche Arbeit*) als auch die automatische Erstellung bei der Freigabe.

| Einrichtung | Erläuterung |
|---|---|
| **FA-Status für Verkaufsangebote** | Wenn gesetzt, erhält ein aus einem **Verkaufsangebot** erstellter Fertigungsauftrag genau diesen Status. Zulässig sind **Simuliert**, **Geplant**, **Fest geplant** und **Freigegeben**; **Beendet** ist nicht erlaubt und wird abgewiesen. Der Wert darf nicht höher sein als **FA-Status für Verkaufsaufträge**, sonst erscheint eine Fehlermeldung. Damit stellt der Administrator sicher, dass Angebote nur eine unverbindlichere Fertigungsstufe auslösen als bestätigte Aufträge. |
| **FA-Status für Verkaufsaufträge** | Wenn gesetzt, erhält ein aus einem **Verkaufsauftrag** erstellter Fertigungsauftrag diesen Status – auch bei automatischer Erstellung während der Freigabe und beim Umwandeln eines Angebots in einen Auftrag. Zulässig sind **Simuliert**, **Geplant**, **Fest geplant**, **Freigegeben** (nicht **Beendet**). Der Wert muss mindestens so hoch sein wie **FA-Status für Verkaufsangebote**. |
| **Setze Bestätigt-Status nach Fertigungsassistentaufruf im VK-Beleg** | Wenn aktiviert, erhält der neu erzeugte Fertigungsauftrag nach dem Bestätigen des Dialogs sofort den **Check-Status "Bestätigt"**; ist das Kennzeichen nicht gesetzt, startet der Fertigungsauftrag mit **Check-Status "Offen"** und muss später manuell geprüft werden. Dies entscheidet, ob ein Angebot ohne weitere Prüfung in einen Auftrag umgewandelt werden kann (siehe *Check-Status-Prüfung*). |
| **Zeitformel, um FAs für Verkaufsangebote zu löschen** | Wenn eine Zeitformel hinterlegt ist, dient sie als Vorgabe dafür, nach welcher Frist Fertigungsaufträge aus abgelaufenen **Verkaufsangeboten** zurückgesetzt bzw. bereinigt werden sollen; ohne Zeitformel gibt es keine solche zeitbasierte Vorgabe. |
| **Verkäufer bei Statuswechsel benachrichtigen** | Wenn aktiviert, erhält der zuständige Anwender beim Anlegen eines Fertigungsauftrags aus dem Verkaufsbeleg die Benachrichtigung **"Fertigungsauftrag anzeigen"** mit dem Hinweis, dass der Check-Status noch zu setzen ist; ist das Kennzeichen nicht gesetzt, unterbleibt diese Meldung und der Anwender muss neue Fertigungsaufträge selbst nachverfolgen. |
| **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen** | Wenn aktiviert, erzeugt Business Central bei der **Freigabe** eines Verkaufsauftrags automatisch für jede Artikelzeile mit **FA erstellen** = aktiviert einen Fertigungsauftrag; ist das Kennzeichen nicht gesetzt, entstehen Fertigungsaufträge ausschließlich manuell über die Aktion **Fertigungsassistent**. |
| **Abfrage zur Erstellung von Fertigungsaufträgen innerhalb Verkaufsaufträgen** | Wenn aktiviert, erscheint bei der Auftragsfreigabe zuerst die Rückfrage **"Fertigungsauftrag erstellen?"**; erst nach Bestätigung mit **Ja** werden die Fertigungsaufträge erzeugt. So kann der Anwender die automatische Erstellung im Einzelfall überspringen. Dieses Kennzeichen setzt voraus, dass **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen** aktiviert ist. |
| **"FA erstellen" in der Verkaufszeile vorbelegen** | Steuert die Vorbelegung des Zeilenkennzeichens **FA erstellen** bei neuen Artikelzeilen. Bei **Alle** wird **FA erstellen** in neuen Artikelzeilen automatisch aktiviert; bei **Keine** bleibt es deaktiviert und der Anwender aktiviert es gezielt pro Zeile. Nicht lagerhaltige Artikeltypen werden dabei stets ausgenommen. |
| **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** | Wenn aktiviert, dürfen auch Verkaufszeilen mit Kennzeichen **Spezialgeschäft** einen Fertigungsauftrag auslösen; ist das Kennzeichen nicht gesetzt, blockiert der Fertigungsassistent solche Zeilen (Prüfung auf **Spezialgeschäft** = Nein) und bei der automatischen Erstellung werden Spezialgeschäft-Zeilen übersprungen. |
| **Löschen von zugeh. FA beim Löschen des VK-Auftrags** | Wenn aktiviert, werden beim Löschen einer Verkaufszeile die zugeordneten Fertigungsaufträge mitbehandelt: Ohne vorhandene Artikel- oder Kapazitätsposten wird der Fertigungsauftrag gelöscht, mit vorhandenen Posten erscheint stattdessen die Rückfrage, ob nur die **Verknüpfung** aufgehoben werden soll. Ist das Kennzeichen nicht gesetzt, bleiben Fertigungsaufträge beim Löschen der Verkaufszeile unverändert bestehen. |

#### Wertebereich "FA-Status" (Option)

Die beiden Statusfelder verwenden die Standard-Fertigungsauftragsstatus, jedoch ohne **Beendet**:

- **Simuliert:** Der Fertigungsauftrag entsteht als unverbindliche Simulation – geeignet für Angebote und Kalkulationen, ohne feste Einplanung.
- **Geplant:** Der Fertigungsauftrag wird geplant angelegt; er fließt in die Bedarfsplanung ein, ist aber noch nicht fest eingeplant.
- **Fest geplant:** Der Fertigungsauftrag ist fest eingeplant und reserviert Kapazität; Fertigung ist noch nicht freigegeben.
- **Freigegeben:** Der Fertigungsauftrag ist zur Fertigung freigegeben; Buchungen in der Produktion sind möglich.
- **Beendet:** nicht zulässig – die Auswahl wird mit einer Fehlermeldung abgewiesen, da der Assistent keinen bereits abgeschlossenen Auftrag erzeugen darf.

### Automatische FA-Erstellung bei Auftragsfreigabe einrichten

**Prozessintro:** Diese Fähigkeit erlaubt es, dass bei der Freigabe eines Verkaufsauftrags ohne weiteren Klick alle benötigten Fertigungsaufträge entstehen. Sie wird vom Administrator vor dem ersten Einsatz eingerichtet und in der täglichen Arbeit beim Freigeben von Aufträgen wirksam (siehe *Tägliche Arbeit im Verkaufsbeleg*).

Richten Sie die Kette in Abhängigkeitsreihenfolge ein:

1. **Stammdaten prüfen:** Zuerst müssen die betroffenen Artikel fertigungsfähig sein (Artikel mit **Arbeitsplannr.** und Fertigungsstückliste). Wenn diese Stammdaten fehlen, kann kein Fertigungsauftrag berechnet werden.
2. **Globales Kennzeichen setzen:** Aktivieren Sie **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen**. Wenn aktiviert, prüft Business Central bei jeder Freigabe die Auftragszeilen.
3. **Optional Rückfrage aktivieren:** Aktivieren Sie **Abfrage zur Erstellung von Fertigungsaufträgen innerhalb Verkaufsaufträgen**, wenn der Anwender die automatische Erstellung pro Freigabe bestätigen soll. Wenn aktiviert, erscheint **"Fertigungsauftrag erstellen?"**.
4. **Zielstatus festlegen:** Setzen Sie **FA-Status für Verkaufsaufträge**. Wenn gesetzt, entstehen alle automatisch erzeugten Fertigungsaufträge in genau diesem Status.
5. **Sonderfall Spezialgeschäft:** Aktivieren Sie **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen**, wenn auch Spezialgeschäft-Zeilen berücksichtigt werden sollen; andernfalls werden diese bei der Freigabe übersprungen.
6. **Vorbelegung abstimmen:** Stellen Sie **"FA erstellen" in der Verkaufszeile vorbelegen** so ein, dass nur die gewünschten Zeilen ein aktives **FA erstellen** tragen – nur diese lösen bei der Freigabe einen Fertigungsauftrag aus.

**Operativer Abschluss:** Der Anwender gibt den Verkaufsauftrag frei; für jede Zeile mit **FA erstellen** = aktiviert entsteht ein Fertigungsauftrag. Bereits verknüpfte Zeilen werden nicht doppelt bedient.

### Manuelle FA-Erstellung über den Fertigungsassistenten einrichten

**Prozessintro:** Für die manuelle, geführte Erstellung im Verkaufsbeleg legt der Administrator fest, in welchem Status der Fertigungsauftrag entsteht und wie der Check-Status vorbelegt wird. Der Anwender löst die Erstellung später über die Aktion **Fertigungsassistent** in der Verkaufszeile aus (siehe *Tägliche Arbeit im Verkaufsbeleg*).

1. **Zielstatus je Belegart festlegen:** Setzen Sie **FA-Status für Verkaufsangebote** und **FA-Status für Verkaufsaufträge**. Wenn gesetzt, erhält der über den Dialog erzeugte Fertigungsauftrag den zur Belegart passenden Status.
2. **Prüfvorgabe wählen:** Aktivieren Sie **Setze Bestätigt-Status nach Fertigungsassistentaufruf im VK-Beleg**, wenn der Fertigungsauftrag sofort als **Bestätigt** gelten soll; andernfalls startet er als **Offen** und muss vor der Angebot-in-Auftrag-Umwandlung noch geprüft werden.
3. **Benachrichtigung aktivieren:** Aktivieren Sie **Verkäufer bei Statuswechsel benachrichtigen**, damit der Anwender nach der Erstellung die Meldung **"Fertigungsauftrag anzeigen"** erhält.

**Operativer Abschluss:** Der Anwender wählt in der Verkaufszeile **Fertigungsassistent**, prüft im Dialog **Menge**, **Arbeitsplannr.** und **Fälligkeitsdatum** und bestätigt mit **OK**.

### Aufräumen von Fertigungsaufträgen einrichten

**Prozessintro:** Diese Einstellungen bestimmen, wie mit Fertigungsaufträgen verfahren wird, deren auslösende Verkaufszeile gelöscht wird oder deren Angebot abläuft. Sie schützen vor verwaisten Fertigungsaufträgen und vor dem Löschen bereits gebuchter Aufträge.

1. **Löschverhalten aktivieren:** Aktivieren Sie **Löschen von zugeh. FA beim Löschen des VK-Auftrags**. Wenn aktiviert, werden zugeordnete Fertigungsaufträge beim Löschen der Verkaufszeile mitbehandelt.
2. **Postenschutz beachten:** Bestehen für den Fertigungsauftrag bereits Artikel- oder Kapazitätsposten, wird er nicht gelöscht; stattdessen erscheint die Rückfrage **"Es existieren bereits Posten … Verknüpfung … aufheben?"**. Wenn der Anwender bestätigt, bleibt der Fertigungsauftrag bestehen und nur der **Auftragsbezug** wird entfernt; lehnt er ab, wird der Löschvorgang abgebrochen.
3. **Angebotsfrist hinterlegen:** Pflegen Sie **Zeitformel, um FAs für Verkaufsangebote zu löschen**, um eine Frist für das Bereinigen von Fertigungsaufträgen aus abgelaufenen Angeboten vorzugeben.

**Operativer Abschluss:** Der Anwender löscht eine Verkaufszeile bzw. das Angebot – die Fertigungsaufträge werden entsprechend gelöscht, entkoppelt oder bereinigt.

## Tägliche Arbeit im Verkaufsbeleg

Die eigentliche Nutzung findet in den **Verkaufszeilen** von **Verkaufsauftrag** und **Verkaufsangebot** statt. Diese Bereiche werden durch die zentrale **Fertigungsassistent Einrichtung** gesteuert: Dort legt der Administrator die Vorbelegung von **FA erstellen**, die Zielstatus, die Check-Status-Vorgabe, die Benachrichtigung sowie die automatische Erstellung bei Freigabe fest (siehe *Einrichtung*). Prüfen Sie bei unerwartetem Verhalten immer zuerst diese Einrichtung.

### Verkaufszeile: Kennzeichen und Aktion

In den Verkaufszeilen (Kopf über Standard-Verkaufsbeleg, Zeilen über das Unterformular) ergänzt das Modul ein Kennzeichen und eine Aktion.

| Feld / Aktion | Erläuterung |
|---|---|
| **FA erstellen** (Feld) | Wenn aktiviert, wird diese Artikelzeile bei der Auftragsfreigabe für die automatische Fertigungsauftragserstellung berücksichtigt; ist es deaktiviert, entsteht für die Zeile bei der Freigabe kein Fertigungsauftrag. Das Feld wird bei neuen Zeilen gemäß **"FA erstellen" in der Verkaufszeile vorbelegen** vorbelegt und ist nur bei lagerhaltigen Artikelzeilen bearbeitbar (bei anderen Typen automatisch deaktiviert). |
| **Fertigungsassistent** (Aktion) | Öffnen Sie über die Aktion **Fertigungsassistent** den geführten Dialog für die aktuelle Verkaufszeile. Wenn ausgeführt, prüft das Modul Artikeltyp, Artikelnr., Menge und Direktlieferung, legt einen simulierten Fertigungsauftrag an und zeigt ihn zur Kontrolle. Voraussetzung: Die Zeilenmenge ist noch nicht vollständig anderen Fertigungsaufträgen zugewiesen – andernfalls erscheint der Hinweis, dass die Verkaufszeilenmenge bereits komplett zugewiesen ist. |

### Dialog "Fertigungsassistent"

Der Dialog **Fertigungsassistent** ist die geführte Maske zum Prüfen und Anlegen des Fertigungsauftrags. Er wird ausschließlich über die gleichnamige Aktion in der Verkaufszeile geöffnet.

Im Kopfbereich (Register **Allgemein**) prüfen und ändern Sie die zentralen Werte:

| Feld | Erläuterung |
|---|---|
| **Artikelnr.** | Zeigt den zu fertigenden Artikel (nicht änderbar); dient der Kontrolle, dass der richtige Artikel gefertigt wird. |
| **Beschreibung** / **Beschreibung 2** | Zeigen den Artikeltext des Fertigungsauftrags (nicht änderbar). |
| **Menge** | Wenn Sie die Menge ändern, wird der Fertigungsauftrag neu berechnet: Der zugrunde liegende Fertigungsauftrag übernimmt die Menge und die Komponenten werden neu ermittelt. So passt die Fertigungsmenge zur benötigten Verkaufsmenge. |
| **Arbeitsplannr.** | Wenn Sie den Arbeitsplan ändern, wird der Fertigungsauftrag mit den Arbeitsgängen des neuen Arbeitsplans neu berechnet; damit steuern Sie den Fertigungsweg direkt aus dem Dialog. |
| **Arbeitsplanversionscode** | Wenn Sie eine andere Arbeitsplanversion wählen, wird der Fertigungsauftrag anhand dieser Version neu berechnet. |
| **Fälligkeitsdatum** | Wenn Sie das Fälligkeitsdatum ändern, wird das Enddatum aus der Durchlaufzeit des Artikels neu ermittelt und der Fertigungsauftrag terminlich neu gerechnet; so richten Sie den Fertigungstermin am Liefertermin aus. |

Der Dialog enthält zwei Unterregister sowie eine Infobox. Sie werden nachfolgend jeweils in einem eigenen Abschnitt beschrieben.

#### Register "Arbeitsplan"

Das Register **Arbeitsplan** zeigt die Arbeitsgänge des Fertigungsauftrags (Fertigungsauftrags-Arbeitsplanzeilen). Der Anwender kann Termine und Zeiten je Arbeitsgang prüfen und anpassen; Änderungen aktualisieren die Anzeige sofort.

| Feld | Erläuterung |
|---|---|
| **Arbeitsgangnr.** | Nummer des Arbeitsgangs; bestimmt die Reihenfolge in der Fertigung. |
| **Art** / **Nr.** | Legen die Kapazität des Arbeitsgangs fest (Arbeitsplatz oder Arbeitsplatzgruppe und deren Nummer); daraus ergibt sich, wo der Arbeitsgang gefertigt wird. |
| **Beschreibung** | Text des Arbeitsgangs. |
| **Startdatum/-zeit** / **Enddatum/-zeit** | Wenn Sie Start- oder Endzeit ändern, wird die Terminierung des Arbeitsgangs aktualisiert und die Anzeige neu berechnet. |
| **Rüstzeit** / **Bearbeitungszeit** / **Wartezeit** / **Transportzeit** | Wenn Sie eine dieser Zeiten ändern, wird der Kapazitätsbedarf und die Terminierung des Arbeitsgangs neu berechnet. |
| **Erw. Kapazitätsbedarf** | Zeigt den erwarteten Kapazitätsbedarf des Arbeitsgangs, umgerechnet auf die Einheit des Arbeitsplatzes – zur Kontrolle der Auslastung. |
| *Weitere, standardmäßig ausgeblendete Felder* | Der Arbeitsplan enthält zusätzlich ausgeblendete Detailfelder (u. a. Vorheriger/Nächster Arbeitsgang, Ablaufcode, Fester Ausschuss, Ausschussfaktor %, Vorlaufmenge, Parallele Kapazitäten, Stückkosten pro, Losgröße, erwartete Kosten, Arbeitsgangstatus, Lagerort sowie Lagerplätze für Fertigung). Sie dienen der Feinsteuerung und werden bei Bedarf eingeblendet. |

Über die Arbeitsgänge stehen zusätzliche Aktionen bereit: **Bemerkungen**, **Werkzeuge**, **Personal**, **Prüfmaßnahmen**, **Zugewiesene Kapazität** sowie **Bedarfsverursacher**. Mit **Zugewiesene Kapazität** sehen Sie die eingeplanten Kapazitätsbedarfe des Arbeitsgangs; **Bedarfsverursacher** zeigt die auslösenden Bedarfe.

#### Register "Komponenten"

Das Register **Komponenten** zeigt die Fertigungsauftrags-Komponenten. Hier prüft und pflegt der Anwender das benötigte Material. Änderungen an mengen- oder lagerrelevanten Feldern lösen bei entsprechend eingestellten Artikeln automatisch eine Reservierung aus.

| Feld | Erläuterung |
|---|---|
| **Artikelnr.** | Komponentenartikel; bei Änderung wird – abhängig vom Artikel – automatisch reserviert. |
| **Fälligkeitsdatum** | Bedarfstermin der Komponente. |
| **Beschreibung** | Text der Komponente. |
| **Komponentenmenge** (Menge pro) | Wenn Sie die Menge pro ändern, wird der Materialbedarf neu ermittelt und ggf. neu reserviert. |
| **Erwartete Menge** | Zeigt die insgesamt erwartete Komponentenmenge für den Fertigungsauftrag. |
| **Restmenge** | Zeigt die noch offene, nicht verbrauchte Komponentenmenge. |
| **Einheitencode** | Mengeneinheit der Komponente; bei Änderung wird neu reserviert. |
| **Ablaufmethode** | Steuert, wie die Komponente verbraucht/gebucht wird (z. B. manuell oder automatisch beim Buchen). |
| **Lagerplatz** | Entnahme-Lagerplatz der Komponente. |
| **Ersatz verfügbar** | Zeigt an, ob für die Komponente ein Ersatzartikel hinterlegt ist. |
| *Weitere, standardmäßig ausgeblendete Felder* | Zusätzlich vorhanden (ausgeblendet): Variantencode, Fälligkeitsdatum/-zeit, Ausschuss %, Berechnungsformel, Länge/Breite/Gewicht/Tiefe, Reservierte Menge, Kostenfelder, Positionsfelder, Vorlaufzeitversatz, kommissionierte Menge, Dimensionscodes, Ablaufcode. Sie dienen der Detailkalkulation und werden bei Bedarf eingeblendet. |

Aktionen im Register **Komponenten**:

- **Reservieren** – reserviert Bestand für die Komponente. Bei den Status **Simuliert** und **Geplant** ist keine Reservierung möglich; es erscheint der Hinweis, dass Komponenten mit diesem Status nicht reserviert werden können.
- **Ersatzartikel auswählen** – wählt einen Ersatzartikel und reserviert anschließend automatisch.
- **Artikelverfolgungszeilen** – erfasst Chargen- und Seriennummern der Komponente.
- **Artikelverfügbarkeit nach** (Ereignis, Periode, Variante, Lagerort, Charge, Stücklistenebene) – prüft die Verfügbarkeit des Komponentenartikels.
- **Lagerplatzinhalt**, **Einlagerungs-/Kommissionierzeilen/Umlagerungszeilen** – zeigen Lagerbestand und Lageraktivitäten zur Komponente.
- **Dimensionen**, **Bemerkungen**, **Bedarfsverursacher**, **Drucken** (Kommissionierliste).

#### Infobox "Komponenten Chargen & Seriennummern"

Die Infobox **Komponenten Chargen & Seriennummern** zeigt zur markierten Komponente die reservierten Artikelverfolgungsangaben, verdichtet je Charge/Seriennummer.

| Feld | Erläuterung |
|---|---|
| **Chargennr.** | Reservierte Chargennummer der Komponente. |
| **Seriennr.** | Reservierte Seriennummer der Komponente. |
| **Menge** | Insgesamt für diese Charge/Seriennummer reservierte Menge. |

## Fertigungsaufträge über alle Status

Der erzeugte Fertigungsauftrag ist ein **Standard-Fertigungsauftrag**; das Modul ergänzt ihn um Bezugs- und Statusinformationen. Diese Ergänzungen erscheinen einheitlich in allen vier Statusausprägungen – **Simulierter Fertigungsauftrag**, **Geplanter Fertigungsauftrag**, **Fest geplanter Fertigungsauftrag** und **Freigegebener Fertigungsauftrag** – jeweils auf der **Karte**, in der **Übersicht** (Liste) und in den **FA-Zeilen**.

### Zusätzliche Felder auf Karte und Liste

| Feld | Erläuterung |
|---|---|
| **Check-Status** | Zeigt den fachlichen Prüfstatus des Fertigungsauftrags. Er steuert insbesondere, ob ein Angebot in einen Auftrag umgewandelt werden darf (siehe *Check-Status-Prüfung*). Die Werte werden unten erläutert. |
| **Verk. an Deb.-Nr.** | Zeigt die Debitorennummer des über den **Auftragsbezug** verknüpften Verkaufsauftrags (abgeleitetes Feld). So erkennt der Fertigungsanwender, für welchen Kunden gefertigt wird. |
| **Verk. an Deb.-Name** | Zeigt den zugehörigen Debitorennamen (abgeleitet). |

### Zusätzliche Felder in den FA-Zeilen

Zusätzlich zu **Check-Status**, **Verk. an Deb.-Nr.** und **Verk. an Deb.-Name** zeigen die **FA-Zeilen** den vollständigen Auftragsbezug:

| Feld | Erläuterung |
|---|---|
| **Fert. Verwendungsart** | Zeigt, ob der Bezug zu einem **Verkaufsangebot** oder **Verkaufsauftrag** besteht (oder **(leer)**, wenn kein Bezug vorhanden ist). Daraus leitet das Modul die Prüf- und Umwandlungslogik ab. |
| **Fert. Verwendungsnr.** | Zeigt die Belegnummer des verknüpften Verkaufsbelegs (nicht änderbar). |
| **Fert. Verwendungszeilennr.** | Zeigt die Zeilennummer der verknüpften Verkaufszeile (nicht änderbar). |
| **Verk. an Deb.-Nr.** / **Verk. an Deb.-Name** | Abgeleitete Debitorinformation zur verknüpften Verkaufszeile. |

#### Wertebereich "Check-Status" (Option)

- **(leer):** Es ist noch kein Prüfstatus gesetzt (Ausgangszustand ohne Bezug).
- **Offen:** Der Fertigungsauftrag ist angelegt, aber fachlich noch nicht geprüft; eine Angebot-in-Auftrag-Umwandlung ist noch nicht erlaubt.
- **In Bearbeitung:** Die Prüfung läuft; die Umwandlung ist weiterhin nicht erlaubt.
- **Bestätigt:** Der Fertigungsauftrag ist geprüft und freigegeben; nur mit diesem Status dürfen die zugehörigen Verkaufsangebote in Aufträge umgewandelt werden.
- **Abgelehnt:** Der Fertigungsauftrag wurde abgelehnt; eine Umwandlung ist nicht erlaubt.

### Aktion "Auftragsbezug löschen" (FA-Zeilen)

In den **FA-Zeilen** der Status **Simuliert**, **Geplant**, **Fest geplant** und **Freigegeben** steht die Aktion **Auftragsbezug löschen** zur Verfügung.

Wenn Sie **Auftragsbezug löschen** ausführen, wird der Bezug der FA-Zeile zum Verkaufsbeleg entfernt (**Fert. Verwendungsart** wird auf **(leer)** gesetzt, Nummer und Zeilennummer werden geleert) und bestehende Reservierungen der FA-Zeile werden aufgehoben. Anschließend erscheint die Meldung, dass der Auftragsbezug entfernt wurde. Besteht kein Bezug, meldet das System, dass kein Auftragsbezug existiert. Nutzen Sie die Aktion, wenn ein Fertigungsauftrag bestehen bleiben, aber vom Verkaufsbeleg entkoppelt werden soll.

## Benachrichtigung und Check-Status-Workflow

### Benachrichtigung "Fertigungsauftrag anzeigen"

Ist **Verkäufer bei Statuswechsel benachrichtigen** aktiviert, erhält der Anwender nach dem Anlegen eines Fertigungsauftrags aus dem Verkaufsbeleg eine Benachrichtigung mit dem Hinweis, dass der Fertigungsauftrag erstellt wurde und der **Check-Status** noch zu setzen ist. Über die Aktion **Fertigungsauftrag anzeigen** in der Benachrichtigung öffnet der Anwender den Fertigungsauftrag direkt in der zum Status passenden Seite.

### Check-Status-Prüfung bei Angebot → Auftrag

Beim Umwandeln eines **Verkaufsangebots** in einen **Verkaufsauftrag** prüft das Modul alle Artikelzeilen: Existiert zu einer Zeile ein verknüpfter Fertigungsauftrag mit **Check-Status** **Offen**, **In Bearbeitung** oder **Abgelehnt**, wird die Umwandlung mit dem Hinweis abgebrochen, dass alle Zeilen einen **"Bestätigten"** Check-Status aufweisen müssen. Nur wenn alle verknüpften Fertigungsaufträge **Bestätigt** sind, läuft die Umwandlung durch; die Fertigungsaufträge werden anschließend auf den **Auftrag** umgehängt und auf den **FA-Status für Verkaufsaufträge** angehoben.

## Löschen und Verknüpfung aufheben

Beim Löschen einer Verkaufszeile greift – sofern **Löschen von zugeh. FA beim Löschen des VK-Auftrags** aktiviert ist – die automatische Behandlung der verknüpften Fertigungsaufträge:

- **Ohne** vorhandene Artikel- oder Kapazitätsposten wird der Fertigungsauftrag (bzw. die FA-Zeile) gelöscht; wird der Fertigungsauftrag dadurch leer, wird er komplett entfernt.
- **Mit** vorhandenen Posten erscheint die Rückfrage, ob die Verknüpfung zwischen Fertigungsauftrag und Verkaufsauftrag aufgehoben werden soll. Bei Bestätigung bleibt der Fertigungsauftrag erhalten und nur der **Auftragsbezug** wird entfernt; bei Ablehnung wird der Löschvorgang abgebrochen.

Unabhängig davon können Sie den Bezug jederzeit gezielt über die FA-Zeilen-Aktion **Auftragsbezug löschen** entfernen.

## Berechtigungen

Das Modul liefert den Berechtigungssatz **All permissions** (Objektname der Berechtigung: intern) mit. Er bestimmt, welche Aktionen Anwender im Fertigungsassistenten ausführen dürfen, und umfasst Lese-/Schreibrechte auf die Einrichtungstabelle sowie Ausführungsrechte auf die Modulseiten und -codeunits. Weisen Sie diesen Berechtigungssatz den Anwendern zu, die Fertigungsaufträge aus dem Verkauf erzeugen und pflegen sollen.

## FAQ und Troubleshooting

### 1. Warum kann ich ein Verkaufsangebot nicht in einen Auftrag umwandeln?

Weil mindestens ein verknüpfter Fertigungsauftrag noch nicht den **Check-Status** **Bestätigt** hat. Solange eine Zeile einen Fertigungsauftrag mit **Offen**, **In Bearbeitung** oder **Abgelehnt** besitzt, wird die Umwandlung abgebrochen. Setzen Sie den **Check-Status** aller verknüpften Fertigungsaufträge auf **Bestätigt**.

### 2. Warum entsteht bei der Auftragsfreigabe kein Fertigungsauftrag?

Prüfen Sie drei Punkte: In der Einrichtung muss **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen** aktiviert sein, die Verkaufszeile muss **FA erstellen** = aktiviert und Typ **Artikel** haben, und für die Zeile darf noch kein Fertigungsauftrag existieren. Ist **Abfrage zur Erstellung …** aktiv, müssen Sie zudem die Rückfrage mit **Ja** beantworten.

### 3. Was passiert, wenn ich im Dialog "Fertigungsassistent" auf Abbrechen klicke?

Der zuvor als Simulation angelegte Fertigungsauftrag wird wieder gelöscht. Es bleibt kein halbfertiger Fertigungsauftrag zurück.

### 4. Warum meldet das System, dass die Verkaufszeilenmenge bereits komplett zugewiesen ist?

Weil zu dieser Verkaufszeile bereits Fertigungsaufträge existieren, deren Menge die Zeilenmenge erreicht oder übersteigt. Es kann kein weiterer Fertigungsauftrag für die Zeile erzeugt werden, bis die zugewiesene Menge unter die Zeilenmenge fällt.

### 5. Warum lässt sich für eine Verkaufszeile das Kennzeichen "FA erstellen" nicht bearbeiten?

Weil die Zeile keinen lagerhaltigen Artikel enthält. Für nicht lagerhaltige Artikeltypen und für Nicht-Artikelzeilen wird **FA erstellen** automatisch deaktiviert und ist nicht editierbar.

### 6. Warum kann ich für eine Spezialgeschäft-Zeile keinen Fertigungsauftrag erstellen?

Weil **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** in der Einrichtung nicht aktiviert ist. Ohne dieses Kennzeichen blockiert der Assistent Spezialgeschäft-Zeilen und die automatische Erstellung überspringt sie.

### 7. Warum kann ich im Dialog Komponenten nicht reservieren?

Weil der Fertigungsauftrag den Status **Simuliert** oder **Geplant** hat. In diesen Status ist keine Reservierung möglich; das System weist mit einem Hinweis auf den Status hin. Reservieren ist erst ab **Fest geplant** möglich.

### 8. Warum kann ich den "FA-Status für Verkaufsangebote" nicht auf "Beendet" setzen?

Weil der Assistent keinen bereits abgeschlossenen Fertigungsauftrag erzeugen darf. **Beendet** wird abgewiesen. Zudem darf der Angebotsstatus nie höher sein als der **FA-Status für Verkaufsaufträge**.

### 9. Was passiert beim Löschen einer Verkaufszeile mit einem bereits gebuchten Fertigungsauftrag?

Existieren für den Fertigungsauftrag Artikel- oder Kapazitätsposten, wird er nicht gelöscht. Sie werden gefragt, ob die Verknüpfung aufgehoben werden soll: Bei **Ja** bleibt der Fertigungsauftrag ohne Auftragsbezug bestehen, bei **Nein** wird der Löschvorgang abgebrochen.

### 10. Wie erkenne ich im Fertigungsauftrag, für welchen Kunden gefertigt wird?

Über die Felder **Verk. an Deb.-Nr.** und **Verk. an Deb.-Name** auf der Karte, in der Übersicht und in den FA-Zeilen sowie über **Fert. Verwendungsart/-nr./-zeilennr.**, die den verknüpften Verkaufsbeleg anzeigen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Kundenanfrage mit Fertigungsvorschau im Angebot

**Auslöser:** Ein Interessent fragt telefonisch einen Fertigungsartikel an; der Vertrieb soll ein belastbares Angebot mit realistischem Fertigungstermin erstellen.

**Einstieg in BC:** Der Anwender legt ein **Verkaufsangebot** an, erfasst die Artikelzeile und wählt in der Verkaufszeile die Aktion **Fertigungsassistent**.

**Kernablauf:** Im Dialog prüft der Anwender **Menge**, **Arbeitsplannr.** und **Fälligkeitsdatum**; über die Register **Arbeitsplan** und **Komponenten** kontrolliert er Arbeitsgänge und Material. Mit **OK** entsteht ein Fertigungsauftrag im **FA-Status für Verkaufsangebote**. Je nach Einrichtung erhält der Fertigungsauftrag den **Check-Status** **Bestätigt** oder **Offen**, und der Verkäufer wird über **Fertigungsauftrag anzeigen** benachrichtigt.

**Abschluss:** Das Angebot geht mit hinterlegter Fertigungsvorschau an den Kunden. Der Fertigungsauftrag bleibt über den **Auftragsbezug** mit der Angebotszeile verknüpft.

### Anwendungsfall 2: Bestätigter Auftrag mit automatischer Fertigungsauftragserstellung

**Auslöser:** Eine schriftliche Bestellung trifft ein; der Auftrag soll erfasst, freigegeben und die Fertigung soll ohne manuelle Nacharbeit angestoßen werden.

**Einstieg in BC:** Voraussetzung ist die aktivierte Einrichtung **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen**. Der Anwender erfasst den **Verkaufsauftrag** mit Artikelzeilen; **FA erstellen** ist gemäß Vorbelegung gesetzt.

**Kernablauf:** Der Anwender gibt den Auftrag frei. Ist **Abfrage zur Erstellung von Fertigungsaufträgen innerhalb Verkaufsaufträgen** aktiv, bestätigt er die Rückfrage **"Fertigungsauftrag erstellen?"** mit **Ja**. Für jede Artikelzeile mit **FA erstellen** = aktiviert entsteht ein Fertigungsauftrag im **FA-Status für Verkaufsaufträge**; Spezialgeschäft-Zeilen werden nur berücksichtigt, wenn dies eingerichtet ist.

**Abschluss:** Die Fertigungsaufträge sind angelegt und tragen **Verk. an Deb.-Nr.**/**-Name** sowie den Auftragsbezug; die Fertigung kann direkt weiterarbeiten.

### Anwendungsfall 3: Angebot in Auftrag umwandeln mit Prüfsicherung

**Auslöser:** Der Kunde erteilt zu einem bestehenden Angebot den Zuschlag; das Angebot soll in einen Auftrag überführt werden.

**Einstieg in BC:** Der Anwender öffnet das **Verkaufsangebot** und startet die Standardfunktion zum Umwandeln in einen **Verkaufsauftrag**.

**Kernablauf:** Das Modul prüft alle Artikelzeilen: Nur wenn alle verknüpften Fertigungsaufträge den **Check-Status** **Bestätigt** haben, läuft die Umwandlung durch. Andernfalls bricht sie mit dem Hinweis ab, dass alle Zeilen einen **"Bestätigten"** Check-Status benötigen. Nach erfolgreicher Umwandlung werden die Fertigungsaufträge automatisch vom Angebot auf den Auftrag umgehängt und auf den **FA-Status für Verkaufsaufträge** angehoben.

**Abschluss:** Der neue Auftrag ist mit denselben Fertigungsaufträgen verknüpft wie zuvor das Angebot; der Fertigungsbezug bleibt lückenlos erhalten.
