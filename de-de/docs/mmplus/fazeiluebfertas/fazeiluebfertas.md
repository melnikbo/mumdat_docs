---
title: Anwenderhandbuch m+m Production Order Overview with Production Order Assistant
---

# Anwenderhandbuch m+m Production Order Overview with Production Order Assistant

## Einleitung

Die m+m App „FA-Zeilenübersicht mit Fertigungsassistent" ist eine Erweiterung für Microsoft Dynamics 365 Business Central. Sie verbindet zwei bereits vorhandene m+m Module miteinander: die **FA-Zeilenübersicht** (Anzeige der Fertigungsauftragszeilen mit den zugehörigen Verkaufszeilen) und den **Fertigungsassistenten** (Erstellung von Fertigungsaufträgen direkt aus dem Verkaufsbeleg).

Der Zweck dieser App ist eng umrissen: Sie sorgt dafür, dass in der **FA-Zeilenübersicht** auch diejenigen Verkaufszeilen sichtbar werden, aus denen ein Fertigungsauftrag über den **Fertigungsassistenten** entstanden ist. Der Fertigungsassistent berechnet die zu fertigende Menge anhand der Angaben aus dem **Verkaufsauftrag** beziehungsweise **Verkaufsangebot** und nicht – wie in Business Central sonst üblich – über die **Reservierungsposten**. Ohne diese App würde die Übersicht solche Fertigungsaufträge nicht mit ihrer Ursprungszeile verknüpfen, weil kein Reservierungsposten die Verbindung herstellt.

**Zielgruppe:** Primär richtet sich das Modul an operative Anwenderinnen und Anwender in der Fertigungssteuerung und im Vertrieb, die täglich mit Fertigungsaufträgen und den auslösenden Verkaufsbelegen arbeiten und in der Übersicht nachvollziehen müssen, welcher Verkaufsvorgang hinter einer Fertigungsauftragszeile steht. Sekundär betrifft es die Administration, die die App und ihre Voraussetzungen einmalig bereitstellt.

**Kurzer Prozessüberblick:** Ein Verkaufsvorgang (Auftrag oder Angebot) löst über den **Fertigungsassistenten** einen Fertigungsauftrag aus. Auf der Fertigungsauftragszeile hinterlegt der Assistent die Verweisfelder **Fert. Verwendungsart**, **Fert. Verwendungsnr.** und **Fert. Verwendungszeilennr.**. In der **FA-Zeilenübersicht** wählt der Anwender eine Fertigungsauftragszeile aus; die untergeordnete Ansicht **Verkaufszeilen** zeigt daraufhin die verknüpfte Verkaufszeile an – auch dann, wenn keine Reservierung besteht. Über **Beleg anzeigen** gelangt man von dort in den jeweiligen Beleg.

## Schnellstart für Anwender

Der kürzeste Weg, um zu einer Fertigungsauftragszeile den auslösenden Verkaufsvorgang zu finden:

1. Öffnen Sie über **Suchen** die Liste **FA-Zeilenübersicht**.
2. Markieren Sie die gewünschte Fertigungsauftragszeile in der Liste.
3. Lesen Sie im unteren Bereich die Ansicht **Verkaufszeilen** ab. Dort erscheint die Verkaufszeile, aus der der Fertigungsauftrag entstanden ist – bei über den **Fertigungsassistenten** angelegten Aufträgen auch ohne Reservierungsposten.
4. Wählen Sie in **Verkaufszeilen** die Aktion **Beleg anzeigen**, um den zugehörigen **Verkaufsauftrag** oder das **Verkaufsangebot** zu öffnen.
5. Alternativ öffnen Sie mit **Beleg anzeigen** auf der Fertigungsauftragszeile den zugehörigen **Fertigungsauftrag** und prüfen dort in den Zeilen die Felder **Fert. Verwendungsart**, **Fert. Verwendungsnr.** und **Fert. Verwendungszeilennr.**.

Voraussetzung ist, dass der Fertigungsauftrag zuvor über den **Fertigungsassistenten** aus einem Verkaufsbeleg erzeugt wurde (siehe **Typische Anwendungsfälle**). Für diese App selbst sind keine weiteren Einstellungen erforderlich.

## Voraussetzungen und Einrichtung

Diese App ist eine reine Kopplung und bringt selbst keine Einrichtungsseite, keine Nummernserie und keine Stammdaten mit. Sie ist erst wirksam, wenn ihre Bausteine vorhanden und einsatzbereit sind.

### Abhängige Module bereitstellen

Die App setzt drei m+m Module voraus, die vor der Nutzung installiert und lizenziert sein müssen:

1. Zuerst muss **m+m Production Order Overview** vorhanden sein. Wenn dieses Modul installiert ist, steht die Liste **FA-Zeilenübersicht** mit der untergeordneten Ansicht **Verkaufszeilen** zur Verfügung.
2. Danach muss **m+m Production Order Assistant** installiert sein. Wenn dieses Modul aktiv ist, kann der **Fertigungsassistent** aus dem Verkaufsbeleg heraus Fertigungsaufträge erzeugen und die Verweisfelder **Fert. Verwendungsart**, **Fert. Verwendungsnr.** und **Fert. Verwendungszeilennr.** auf der Fertigungsauftragszeile setzen.
3. Zusätzlich wird das Basismodul **m+m Cloud Base** vorausgesetzt. Es stellt technische Grundfunktionen bereit und hat keine eigene Bedienoberfläche in diesem Ablauf.

Sind alle drei Module vorhanden, greift die vorliegende Kopplungs-App automatisch – ohne weitere Aktivierung. Es gibt keinen Schalter, den ein Anwender oder Administrator setzen müsste.

### Fertigungsassistent Einrichtung (im vorgelagerten Modul)

Damit überhaupt Fertigungsaufträge mit Verweisfeldern entstehen, die diese App auswerten kann, konfiguriert die Administration einmalig den Fertigungsassistenten. Diese Einrichtung gehört zum Modul **m+m Production Order Assistant** und wird dort ausführlich beschrieben; für den vorliegenden Ablauf sind daraus vor allem folgende Kategorien relevant:

- der Fertigungsauftragsstatus, in den ein aus einem **Verkaufsauftrag** beziehungsweise **Verkaufsangebot** erzeugter Fertigungsauftrag überführt wird,
- die Vorbelegung des Kennzeichens **FA erstellen** in der Verkaufszeile,
- ob bei der Freigabe eines Verkaufsauftrags automatisch ein Fertigungsauftrag entsteht.

Wenn diese Einstellungen gesetzt sind, dann erzeugt der Fertigungsassistent Fertigungsaufträge mit gefüllten Verweisfeldern; genau diese Verweisfelder wertet die vorliegende App aus, um die Verkaufszeile in der Übersicht anzuzeigen. Öffnen Sie die zugehörige Einrichtungsseite **Fertigungsassistent Einrichtung** über **Suchen**.

### Berechtigungen

Die App liefert den Berechtigungssatz **All permissions** (Objektname `MuM PLPA Permission`) mit. Wenn Sie diesen Berechtigungssatz einem Benutzer oder einer Benutzergruppe zuweisen, dann erhält die betreffende Person die Ausführungsrechte für die Kopplungslogik dieser App. Der Berechtigungssatz legt fest, welche Aktionen ein Anwender im Rahmen dieser Erweiterung ausführen darf, und bestimmt damit den technischen Zugriff auf die Kopplungsfunktion. Für die reine Anzeige der **Verkaufszeilen** in der **FA-Zeilenübersicht** sind zusätzlich die Berechtigungen der vorgelagerten Module sowie die Standardberechtigungen für Fertigungs- und Verkaufsbelege erforderlich.

## Funktionsweise der Kopplung

Dieser Abschnitt erläutert, was die App im Hintergrund bewirkt, damit Anwender die Anzeige in der **FA-Zeilenübersicht** richtig einordnen können. Die Steuerung erfolgt vollständig automatisch; es gibt keine zusätzliche Bedienoberfläche.

### Ausgangslage in der FA-Zeilenübersicht

Die Liste **FA-Zeilenübersicht** zeigt Fertigungsauftragszeilen. Zu jeder markierten Zeile blendet die untergeordnete Ansicht **Verkaufszeilen** die zugehörigen Verkaufszeilen ein. In der Standardlogik der Übersicht ermittelt Business Central diese Verkaufszeilen über die **Reservierungsposten** beziehungsweise die Artikelposten – also über eine mengenmäßige Reservierung zwischen Verkaufsbedarf und Fertigung.

Fertigungsaufträge, die der **Fertigungsassistent** direkt aus einem Verkaufsbeleg erzeugt, berechnen ihre Menge jedoch aus den Angaben des Verkaufsvorgangs und nicht über Reservierungsposten. Für solche Aufträge existiert daher nicht zwingend ein Reservierungsposten, der die Verkaufszeile mit der Fertigung verbindet. Ohne die vorliegende App bliebe die Ansicht **Verkaufszeilen** in diesem Fall leer.

### Was die App ergänzt

Die App erkennt die vom Fertigungsassistenten gesetzten Verweisfelder auf der Fertigungsauftragszeile und markiert die genannte Verkaufszeile zusätzlich zur Standardlogik. Ausschlaggebend sind drei Felder der Fertigungsauftragszeile:

| Feld | Erläuterung |
|------|-------------|
| **Fert. Verwendungsart** | Wenn dieses Feld gefüllt ist, dann stammt der Fertigungsauftrag aus einem Verkaufsvorgang und die App zeigt die zugehörige Verkaufszeile an. Der Wert bestimmt, in welchem Belegtyp die App die Zeile sucht: **Verkaufsauftrag** – die App sucht die Zeile im Verkaufsauftrag; **Verkaufsangebot** – die App sucht die Zeile im Verkaufsangebot. Ist das Feld leer, dann liegt kein Verweis aus dem Fertigungsassistenten vor und die Anzeige folgt allein der Standardlogik über Reservierungsposten. |
| **Fert. Verwendungsnr.** | Wenn dieses Feld gefüllt ist, dann verweist es auf die Belegnummer des auslösenden **Verkaufsauftrags** beziehungsweise **Verkaufsangebots**; die App verwendet diese Nummer, um in der Ansicht **Verkaufszeilen** genau den richtigen Beleg auszuwählen. |
| **Fert. Verwendungszeilennr.** | Wenn dieses Feld gefüllt ist, dann verweist es auf die konkrete Zeilennummer innerhalb des Verkaufsbelegs; erst dadurch wird in **Verkaufszeilen** die exakte Ursprungszeile und nicht nur der Beleg angezeigt. |

Die drei Felder werden vom Fertigungsassistenten gesetzt und sind auf der Fertigungsauftragszeile nicht manuell editierbar. Sind alle drei gefüllt, dann markiert die App die passende Verkaufszeile und stellt sie in der Übersicht dar. Ist die **Fert. Verwendungsart** leer, dann greift ausschließlich die reservierungsbasierte Standardlogik.

### Ansicht „Verkaufszeilen"

Die untergeordnete Ansicht **Verkaufszeilen** ist schreibgeschützt und dient der Information. Sie zeigt die kaufmännischen Eckdaten der verknüpften Verkaufszeile – insbesondere den zugehörigen Debitor, den Belegbezug (Belegart und Belegnummer), die Mengen sowie die offene Menge als Standarddaten der Verkaufszeile. Aus dem vorgelagerten Modul ergänzt wird folgende Spalte:

| Feld | Erläuterung |
|------|-------------|
| **Verk. an Deb.- Name** | Zeigt den Namen des Debitors der Verkaufszeile an. Wenn Sie mehrere Fertigungsauftragszeilen durchgehen, dann erkennen Sie so ohne zusätzlichen Belegaufruf, für welchen Kunden die jeweilige Fertigung bestimmt ist. |

Über die Ansicht stehen Aktionen zur Verfügung, um von der Verkaufszeile aus weiterzuarbeiten:

- **Beleg anzeigen** – öffnet den zugehörigen Verkaufsbeleg (**Verkaufsauftrag** oder **Verkaufsangebot**).
- **Reservierungsposten** – zeigt die Reservierungsposten zur Verkaufszeile.
- **Artikelverfolgungszeilen** – öffnet die Artikelverfolgung der Verkaufszeile.

### Aktionen der FA-Zeilenübersicht

Auf der Ebene der Fertigungsauftragszeile bietet die **FA-Zeilenübersicht** die folgenden Aktionen (aus dem vorgelagerten Modul), die den Übergang in die weitere Bearbeitung erleichtern:

- **Beleg anzeigen** – öffnet den Fertigungsauftrag im passenden Status.
- **Status ändern** – startet den Statuswechsel des Fertigungsauftrags.
- **Komponenten** – öffnet die Fertigungsauftragskomponenten der Zeile.
- **Prod. Buch. Blatt** – öffnet das Produktionsbuchungsblatt (nur bei freigegebenem Fertigungsauftrag).
- **Arbeitsgänge** – öffnet die Arbeitsgänge des Fertigungsauftrags.

## Typische Anwendungsfälle

Die folgenden Beispiele zeigen den durchgängigen Ablauf vom auslösenden Ereignis bis zur Auswertung in der **FA-Zeilenübersicht**. Alle Bildschirme und Aktionen entsprechen den vorhandenen Modulen; die vorliegende App sorgt jeweils dafür, dass die Verkaufszeile in der Übersicht sichtbar wird.

### Anwendungsfall 1: Fertigungsauftrag aus einem Verkaufsauftrag nachvollziehen

**Auslöser:** Ein Kunde ruft an und fragt nach dem Liefertermin für einen bestellten, gefertigten Artikel. Die Fertigungssteuerung möchte schnell prüfen, welcher Fertigungsauftrag zu diesem Verkaufsauftrag gehört.

**Einstieg in BC:** Zuvor wurde der Fertigungsauftrag angelegt: Im **Verkaufsauftrag** wurde in der betreffenden Zeile das Kennzeichen **FA erstellen** gesetzt und über die Aktion **Fertigungsassistent** ein Fertigungsauftrag erzeugt. Im **Fertigungsassistenten** wurden Menge, Arbeitsplan, **Fälligkeitsdatum** und **Komponenten** geprüft und mit **OK** bestätigt. Dabei setzte der Assistent auf der Fertigungsauftragszeile **Fert. Verwendungsart** = **Verkaufsauftrag** sowie die zugehörige **Fert. Verwendungsnr.** und **Fert. Verwendungszeilennr.**.

**Kernablauf:**

1. Öffnen Sie über **Suchen** die **FA-Zeilenübersicht**.
2. Markieren Sie die betreffende Fertigungsauftragszeile.
3. Lesen Sie in der Ansicht **Verkaufszeilen** die verknüpfte Auftragszeile mit Debitor (**Verk. an Deb.- Name**), Belegbezug und Mengen ab.
4. Wählen Sie **Beleg anzeigen**, um den **Verkaufsauftrag** direkt zu öffnen und dem Kunden den Stand zu nennen.

**Abschluss:** Der Zusammenhang zwischen Fertigung und Verkaufsauftrag ist ohne manuelle Suche belegt; es sind keine weiteren Buchungen in dieser App erforderlich.

### Anwendungsfall 2: Fertigungsauftrag aus einem Verkaufsangebot prüfen

**Auslöser:** Eine interne Notiz bittet um Prüfung eines Fertigungsauftrags, der bereits auf Basis eines noch offenen **Verkaufsangebots** vorbereitet wurde. Weil noch kein Auftrag besteht, existiert typischerweise kein Reservierungsposten.

**Einstieg in BC:** Der Fertigungsauftrag wurde zuvor aus der Angebotszeile über die Aktion **Fertigungsassistent** angelegt. Der Assistent setzte **Fert. Verwendungsart** = **Verkaufsangebot** sowie **Fert. Verwendungsnr.** und **Fert. Verwendungszeilennr.**.

**Kernablauf:**

1. Öffnen Sie über **Suchen** die **FA-Zeilenübersicht**.
2. Markieren Sie die Fertigungsauftragszeile zum Angebot.
3. In der Ansicht **Verkaufszeilen** erscheint die Angebotszeile – obwohl kein Reservierungsposten vorliegt, weil die App die Verweisfelder auswertet.
4. Öffnen Sie bei Bedarf mit **Beleg anzeigen** das **Verkaufsangebot**.

**Abschluss:** Die Prüfung ist abgeschlossen; die Herkunft des Fertigungsauftrags aus dem Angebot ist eindeutig dokumentiert.

## FAQ und Troubleshooting

### 1. Warum sehe ich in der Ansicht „Verkaufszeilen" keine Zeile, obwohl ein Fertigungsauftrag existiert?

Die Verkaufszeile wird nur angezeigt, wenn entweder ein Reservierungsposten die Verbindung herstellt oder die Fertigungsauftragszeile die Verweisfelder des Fertigungsassistenten enthält. Prüfen Sie, ob **Fert. Verwendungsart**, **Fert. Verwendungsnr.** und **Fert. Verwendungszeilennr.** gefüllt sind. Sind sie leer, wurde der Fertigungsauftrag nicht über den **Fertigungsassistenten** aus einem Verkaufsbeleg erzeugt.

### 2. Was bedeutet ein Eintrag in „Fert. Verwendungsart"?

Ein gefüllter Wert zeigt an, dass der Fertigungsauftrag über den **Fertigungsassistenten** aus einem Verkaufsvorgang stammt und die Mengenberechnung aus dem Verkaufsbeleg erfolgte – nicht über Reservierungsposten. Der Wert **Verkaufsauftrag** verweist auf einen Auftrag, der Wert **Verkaufsangebot** auf ein Angebot als Ursprung.

### 3. Warum wird die Verkaufszeile angezeigt, obwohl es keinen Reservierungsposten gibt?

Genau das ist die Aufgabe dieser App: Sie ergänzt die reservierungsbasierte Standardlogik um die Verweisfelder des Fertigungsassistenten. Dadurch erscheint die auslösende Verkaufszeile auch dann, wenn keine Reservierung vorliegt.

### 4. Muss ich die App aktivieren oder einrichten?

Nein. Es gibt keine eigene Einrichtungsseite und keinen Aktivierungsschalter. Sobald die drei vorausgesetzten Module installiert sind, greift die Kopplung automatisch.

### 5. Warum finde ich für diese App keine eigene Einrichtungsseite über „Suchen"?

Diese App bringt selbst keine Einrichtung mit. Konfiguriert wird ausschließlich der vorgelagerte Fertigungsassistent auf der Seite **Fertigungsassistent Einrichtung**. Von deren Einstellungen hängt ab, ob und in welchem Status Fertigungsaufträge mit Verweisfeldern entstehen.

### 6. Kann ich die Felder „Fert. Verwendungsnr." oder „Fert. Verwendungszeilennr." selbst ändern?

Nein. Diese Felder werden vom **Fertigungsassistenten** gesetzt und sind auf der Fertigungsauftragszeile schreibgeschützt. Sie dienen ausschließlich der Nachverfolgung des Ursprungs.

### 7. Ich habe einen Fertigungsauftrag manuell angelegt – warum erscheint keine Verkaufszeile?

Manuell oder über die Planung angelegte Fertigungsaufträge tragen keine Verweisfelder des Fertigungsassistenten. Für sie greift nur die Standardlogik über Reservierungsposten. Besteht kein Reservierungsposten, bleibt die Ansicht **Verkaufszeilen** entsprechend leer.

### 8. Welche Rolle spielt der „Check-Status" des Fertigungsassistenten für die Anzeige?

Der **Check-Status** dokumentiert den Prüfstand des vom Assistenten erzeugten Fertigungsauftrags mit den Werten **Offen** (angelegt, noch nicht geprüft), **In Bearbeitung** (Prüfung läuft), **Bestätigt** (freigegeben) und **Abgelehnt** (verworfen). Für die Anzeige der Verkaufszeile in der Übersicht ist allein das Vorhandensein der Verweisfelder maßgeblich; der **Check-Status** steuert die Anzeige nicht, gibt aber Auskunft über den Bearbeitungsstand.

### 9. Wie komme ich von der Übersicht schnell in den auslösenden Beleg?

Wählen Sie in der Ansicht **Verkaufszeilen** die Aktion **Beleg anzeigen**. Sie öffnet je nach Ursprung den **Verkaufsauftrag** oder das **Verkaufsangebot**. Auf Ebene der Fertigungsauftragszeile öffnet **Beleg anzeigen** hingegen den Fertigungsauftrag.

### 10. Der erwartete Kundenname fehlt in der Spalte „Verk. an Deb.- Name" – woran liegt das?

Die Spalte zeigt den Debitornamen der verknüpften Verkaufszeile. Fehlt der Name, ist entweder keine Verkaufszeile verknüpft (siehe Frage 1) oder der zugrunde liegende Debitor ist im Verkaufsbeleg nicht gesetzt. Prüfen Sie über **Beleg anzeigen** den Ursprungsbeleg.
