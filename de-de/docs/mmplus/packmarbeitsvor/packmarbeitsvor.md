---
title: Anwenderhandbuch m+m Prod. Order Job Overview with Package Mgt.
---

# Anwenderhandbuch m+m Prod. Order Job Overview with Package Mgt.

Dieses Handbuch beschreibt die Funktionen, die die App **m+m Prod. Order Job Overview with Package Mgt.**
in Microsoft Dynamics 365 Business Central bereitstellt. Die App erweitert den bestehenden **FA-Arbeitsvorrat**
um die Möglichkeit, bei der Rückmeldung eines Fertigungsauftrags **Packmittel** zuzuordnen und mitzubuchen.

Alle in diesem Handbuch genannten Seiten, Felder, Aktionen und Statuswerte sind die deutschen Bezeichnungen,
die Sie in Business Central sehen.

## 1. Einleitung

### Zweck des Moduls

Die App fügt dem **FA-Arbeitsvorrat** einen **Packmittel**-Bereich hinzu. Wenn ein Anwender einen gestarteten
Fertigungsauftrag im FA-Arbeitsvorrat zurückmeldet, öffnet sich die Buchungsmaske **FA-Arbeitsvorrat Buchung**.
Genau dort ergänzt diese App:

- eine **Packmittel Factbox**, die die Packmittelstruktur zum Fertigungsauftrag anzeigt,
- im Register **Packmittel** die Felder **Packmittelstatus** und **Packmittelreferenz Nr.**,
- die Aktionen **Packmittelzuweisung** und **Aus Paketreferenz erstellen**.

Dadurch ordnet der Anwender das verbrauchte oder erzeugte Material direkt bei der Rückmeldebuchung einem
Packmittel zu, ohne die Buchungsmaske verlassen zu müssen. Zusätzlich erhält die Liste **FA-Arbeitsvorrat**
dieselbe **Packmittel Factbox** zur schnellen Ansicht der Packmittelstruktur.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender** in der Fertigung, die Fertigungsaufträge am FA-Arbeitsvorrat
**zurückmelden** (Zeiten und Mengen buchen) und dabei Packmittel zuordnen. Administratoren und Planer sind nur
sekundär betroffen, da diese App **keine eigenen Einrichtungsseiten** mitbringt (siehe Kapitel Einrichtung).

### Voraussetzungen

Die App ist eine Integrationskomponente und setzt zwei andere Apps voraus:

- **m+m Packmittel** (Packmittel-Stammdaten und Packmittellogik),
- **m+m FA-Arbeitsvorrat** (FA-Arbeitsvorrat-Liste und Buchungsmaske).

Ohne diese beiden Apps stehen weder die Packmittel noch der FA-Arbeitsvorrat zur Verfügung.

### Kurzer Prozessüberblick

Der Anwender ruft den **FA-Arbeitsvorrat** über die **Suchen**-Funktion auf, wählt eine
**Arbeitsplatzgruppennr.** (und optional eine **Arbeitsplatznr.**) und erhält die zugehörigen
Fertigungsaufträge. Er startet einen Auftrag über **Starten** und schließt ihn mit **Teilbeenden** oder
**Beenden** ab. Dabei öffnet sich die **FA-Arbeitsvorrat Buchung**. Dort erfasst er Zeiten und Mengen und ordnet
im Register **Packmittel** ein Packmittel zu – entweder über die **Packmittelreferenz Nr.**, über
**Packmittelzuweisung** oder über **Aus Paketreferenz erstellen**. Mit **OK** wird die Rückmeldung gebucht.

## 2. Schnellstart für Anwender

Der schnellste Weg, eine Rückmeldung mit Packmittelzuordnung zu buchen:

1. Öffnen Sie über **Suchen** die Liste **FA-Arbeitsvorrat**.
2. Tragen Sie im Kopf die **Arbeitsplatzgruppennr.** ein (und bei Bedarf die **Arbeitsplatznr.**). Die
   passenden Fertigungsaufträge werden geladen.
3. Markieren Sie die gewünschte Zeile und wählen Sie **Starten**, sofern der Arbeitsgang noch nicht läuft.
4. Wählen Sie **Teilbeenden** (Teilmenge) oder **Beenden** (Restmenge). Die Maske
   **FA-Arbeitsvorrat Buchung** öffnet sich.
5. Erfassen Sie im Bereich **Mengen** die **Menge** sowie im Bereich **Buchungszeitraum** die Zeiten.
6. Ordnen Sie im Register **Packmittel** ein Packmittel zu – wählen Sie dazu **Packmittelzuweisung**
   (öffnet die **Beleg Packmittel Liste**) oder tragen Sie eine **Packmittelreferenz Nr.** ein.
7. Bestätigen Sie mit **OK**. Die Rückmeldung wird gebucht und der **Packmittelstatus** zeigt an, ob das
   Material dem Packmittel vollständig (**Voll**) oder teilweise (**Teilweise**) zugeordnet ist.

Die Reihenfolge **zuerst** Auftrag starten, **danach** teilbeenden/beenden und **schließlich** buchen ist durch
den FA-Arbeitsvorrat vorgegeben. Die Packmittelzuordnung erfolgt **innerhalb** von Schritt 5–6, bevor Sie mit
**OK** buchen.

## 3. Einrichtung

Diese App bringt **keine eigenen Einrichtungsseiten, Nummernserien, Report- oder Mailparameter** mit. Sie
aktiviert ihre Funktionen allein dadurch, dass sie zusammen mit ihren beiden Voraussetzungs-Apps installiert
ist. Die eigentliche Konfiguration liegt vollständig in den beiden Voraussetzungsmodulen und wird in deren
Handbüchern beschrieben:

- **m+m Packmittel:** Anlage und Pflege der Packmittel-Stammdaten, Packmittelreferenzen und der Packmittellogik.
  Diese Stammdaten bestimmen, welche Packmittel und Referenzen bei der Rückmeldebuchung zur Auswahl stehen.
- **m+m FA-Arbeitsvorrat:** Einrichtung des FA-Arbeitsvorrats (unter anderem Sortierung, Sequenzführung und die
  Aktualisierung der Fertigungsauftragszeilen nach einer Arbeitsgangaktion). Diese Einstellungen steuern, wie
  Aufträge in der Liste **FA-Arbeitsvorrat** erscheinen und zurückgemeldet werden.

### Voraussetzung aktivieren

Damit der Packmittel-Bereich in der **FA-Arbeitsvorrat Buchung** erscheint, gehen Sie in folgender
Reihenfolge vor:

1. **Zuerst** installieren Sie **m+m Packmittel** und pflegen dort die Packmittel-Stammdaten. Wenn Packmittel
   angelegt und – wo gewünscht – Packmittelreferenzen hinterlegt sind, dann stehen diese später in der
   Rückmeldebuchung zur Zuordnung bereit.
2. **Danach** installieren Sie **m+m FA-Arbeitsvorrat** und richten den FA-Arbeitsvorrat ein. Wenn der
   FA-Arbeitsvorrat eingerichtet ist, dann können Anwender Fertigungsaufträge über **Suchen** aufrufen,
   starten und zurückmelden.
3. **Schließlich** installieren Sie **m+m Prod. Order Job Overview with Package Mgt.**. Wenn diese App aktiv
   ist, dann erscheinen in der **FA-Arbeitsvorrat Buchung** das Register **Packmittel**, die Aktionen
   **Packmittelzuweisung** und **Aus Paketreferenz erstellen** sowie die **Packmittel Factbox**.

### Berechtigungen

Die App liefert die Berechtigungsgruppe **All permissions** (`MuM PJPM All`) mit. Diese Berechtigungsgruppe
legt fest, welche Objekte dieser App ein Anwender ausführen darf; sie umfasst die interne Programmlogik der App.
Ergänzend benötigen Anwender die Berechtigungen der beiden Voraussetzungsmodule, um Packmittel und den
FA-Arbeitsvorrat nutzen zu können. Weisen Sie die Berechtigungsgruppe den Benutzern zu, die im FA-Arbeitsvorrat
Packmittel zuordnen sollen.

## 4. Stammdaten

Diese App führt **keine eigenen Stammdaten** und erweitert **keine** Stammdatenkarte (Artikel, Debitor,
Kreditor). Alle für die Packmittelzuordnung nötigen Stammdaten – insbesondere die Packmittel selbst und die
Packmittelreferenzen – werden im Modul **m+m Packmittel** gepflegt und dort dokumentiert. In der
Rückmeldebuchung greifen Sie ausschließlich auf diese bestehenden Packmittel-Stammdaten zu.

## 5. Tägliche Arbeit: Rückmeldung mit Packmittel

Die tägliche Arbeit mit dieser App findet in der Buchungsmaske **FA-Arbeitsvorrat Buchung** statt. Diese Maske
wird durch die Einstellungen im Modul **m+m FA-Arbeitsvorrat** gesteuert (Sortierung und Anzeige der Aufträge
in der Liste **FA-Arbeitsvorrat**) und greift auf die im Modul **m+m Packmittel** gepflegten Packmittel-Stammdaten
zu. Öffnen Sie zunächst die Liste, melden Sie einen Auftrag zurück und ordnen Sie in der Buchungsmaske das
Packmittel zu.

### 5.1 Liste FA-Arbeitsvorrat

**Einstieg:** Öffnen Sie über **Suchen** die Liste **FA-Arbeitsvorrat**.

In der Liste filtern Sie zuerst nach der Arbeitsplatzstruktur und wählen dann den zurückzumeldenden Auftrag.
Diese App ergänzt die Liste um die **Packmittel Factbox** (siehe Abschnitt 5.4). Die Filter und Aktionen der
Liste stammen aus dem Modul **m+m FA-Arbeitsvorrat**; sie sind hier zur Orientierung beschrieben, weil die
Packmittelzuordnung von dieser Liste aus beginnt.

#### Filter der Liste

Setzen Sie **zuerst** die übergeordnete Arbeitsplatzstruktur, **danach** – falls nötig – die feinere Ebene.

| Filterfeld | Erläuterung |
|------------|-------------|
| **Arbeitsplatzgruppennr.** | Wenn gesetzt, dann werden alle Fertigungsaufträge dieser Arbeitsplatzgruppe geladen und angezeigt. Dies ist der übergeordnete Einstieg und in der Regel das erste Feld, das Sie füllen. |
| **Arbeitsplatznr.** | Wenn gesetzt, dann werden die Zeilen zusätzlich auf diesen einzelnen Arbeitsplatz innerhalb der Arbeitsplatzgruppe eingegrenzt. Optional; ohne diesen Filter sehen Sie alle Arbeitsplätze der Gruppe. |
| **FA-Nr.** | Wenn gesetzt, dann werden nur die Zeilen des angegebenen freigegebenen Fertigungsauftrags angezeigt. |
| **Datum** | Wenn gesetzt, dann werden die Zeilen nach diesem Datum gefiltert. |
| **Sortierung** | Bestimmt die Sortierreihenfolge der Zeilen (z. B. nach Reihenfolge, Status oder Datum). Wenn geändert, dann wird die Liste unmittelbar neu sortiert. |
| **Beendete ausblenden** | Wenn aktiviert, dann werden bereits beendete Arbeitsgänge ausgeblendet, sodass nur noch offene Arbeit sichtbar ist. |
| **Offene ausblenden** | Wenn aktiviert, dann werden offene Arbeitsgänge ausgeblendet; dies hilft, gezielt bereits gemeldete Zeilen zu prüfen. |
| **Rückmeldung in Vorarbeitsgang** | Wenn aktiviert, dann werden Zeilen berücksichtigt, für die im vorhergehenden Arbeitsgang bereits eine Rückmeldung erfolgt ist; so erkennen Sie, welche Aufträge zur Weiterbearbeitung bereitstehen. |

#### Aktionen der Liste

Diese Aktionen steuern den Rückmeldeprozess. Sie stammen aus dem FA-Arbeitsvorrat und leiten in die
Buchungsmaske über, in der diese App die Packmittelzuordnung ergänzt.

| Aktion | Erläuterung |
|--------|-------------|
| **Rüsten** | Meldet den Rüstvorgang des markierten Arbeitsgangs. Wenn ausgelöst, dann wird der Auftrag in den Rüstzustand versetzt. |
| **Starten** | Startet den markierten Arbeitsgang. Wenn ausgelöst, dann läuft der Auftrag und kann anschließend teilbeendet oder beendet werden. |
| **Unterbrechen** | Unterbricht einen laufenden Arbeitsgang. Wenn ausgelöst, dann wird die Bearbeitung pausiert, bis erneut gestartet wird. |
| **Teilbeenden** | Meldet eine **Teilmenge** zurück. Wenn ausgelöst, dann öffnet sich die **FA-Arbeitsvorrat Buchung** für die Teilmenge; der Auftrag bleibt für die Restmenge offen. |
| **Beenden** | Meldet die **Restmenge** zurück und schließt den Arbeitsgang ab. Wenn ausgelöst, dann öffnet sich die **FA-Arbeitsvorrat Buchung** für die abschließende Buchung. |
| **Umlagerung** | Öffnet die Umlagerungszeilen zum Arbeitsgang. Wenn ausgelöst, dann bearbeiten Sie die zugehörigen Lagerumlagerungen (sofern für den Arbeitsgang aktiviert). |
| **Auf Offen setzen** | Setzt einen gemeldeten Arbeitsgang wieder auf offen. Wenn ausgelöst, dann kann der Auftrag erneut bearbeitet und zurückgemeldet werden. |
| **Daten aktualisieren** | Lädt die Liste anhand der aktuellen Filter neu. Wenn ausgelöst, dann werden zwischenzeitliche Änderungen sichtbar. |
| **Beleg anzeigen** | Öffnet den zugehörigen Fertigungsauftrag. Wenn ausgelöst, dann wechseln Sie zum vollständigen Beleg des markierten Arbeitsgangs. |
| **Ereignisverlauf** | Öffnet den Ereignisverlauf des Arbeitsgangs. Wenn ausgelöst, dann sehen Sie die protokollierten Rückmeldeereignisse zur Zeile. |

### 5.2 Buchungsmaske FA-Arbeitsvorrat Buchung

**Einstieg:** Wählen Sie in der Liste **FA-Arbeitsvorrat** eine gestartete Zeile und dann **Teilbeenden**
oder **Beenden**. Die Maske **FA-Arbeitsvorrat Buchung** öffnet sich. Sie ist nicht über **Suchen**
erreichbar, sondern nur über diesen Weg aus der Liste.

In dieser Maske erfassen Sie Zeiten und Mengen der Rückmeldung. Die folgenden Felder stammen aus dem
FA-Arbeitsvorrat und bilden den Rahmen, in dem Sie anschließend das Packmittel zuordnen.

| Feld | Erläuterung |
|------|-------------|
| **Startdatum** | Wenn gesetzt, dann wird dieser Tag als Beginn der Rückmeldung gebucht. Muss vor oder gleich dem Enddatum liegen, sonst wird die Buchung mit einer Meldung abgewiesen. |
| **Startzeit** | Wenn gesetzt, dann wird diese Uhrzeit als Beginn gebucht. Bei gleichem Start- und Enddatum muss sie vor der Endzeit liegen. |
| **Enddatum** | Wenn gesetzt, dann wird dieser Tag als Ende der Rückmeldung gebucht. |
| **Endzeit** | Wenn gesetzt, dann wird diese Uhrzeit als Ende gebucht; sie begrenzt zusammen mit der Startzeit die gemeldete Dauer. |
| **Rüstzeit** | Wenn erfasst, dann wird diese Zeit als Rüstanteil der Rückmeldung gebucht und fließt in die Kapazitätsrückmeldung ein. |
| **Bearbeitungszeit** | Wenn erfasst, dann wird diese Zeit als Bearbeitungsanteil gebucht; sie bestimmt den zeitbezogenen Teil der Rückmeldung. |
| **Menge** | Wenn erfasst, dann wird diese Menge als Rückmeldemenge des Arbeitsgangs gebucht. Ist die Menge **0**, kann keine Packmittelreferenz gesetzt werden (siehe Register Packmittel). |
| **Gebuchte Menge** | Zeigt die bereits gebuchte Menge des Arbeitsgangs an (nicht editierbar). So erkennen Sie, wie viel bei einer Teilbeendung bereits gemeldet wurde und welche Restmenge noch offen ist. |
| **Lagerort** | Wenn gesetzt, dann wird gegen diesen Lagerort gebucht. Der Lagerort ist Pflicht für die **Packmittelzuweisung** (siehe Register Packmittel). |
| **Lagerplatz** | Wenn gesetzt, dann wird gegen diesen Lagerplatz innerhalb des Lagerorts gebucht. |
| **FA-Nr.** | Zeigt den zugehörigen Fertigungsauftrag an (nicht editierbar). |
| **Artikelnr.** | Zeigt den Artikel des Fertigungsauftrags an (nicht editierbar). Dieser Artikel ist Bezug für die Packmittelzuordnung. |
| **Variantencode** | Zeigt die Variante des Artikels an (nicht editierbar). |
| **Beschreibung** | Zeigt die Artikelbeschreibung an (nicht editierbar). |
| **Beschreibung 2** | Zeigt die ergänzende Artikelbeschreibung an (nicht editierbar). |

### 5.3 Register Packmittel (durch diese App ergänzt)

Dieses Register fügt die App der Buchungsmaske hinzu. Hier ordnen Sie das Packmittel zur Rückmeldung zu,
bevor Sie mit **OK** buchen.

| Feld | Erläuterung |
|------|-------------|
| **Packmittelstatus** | Zeigt an, wie weit die gemeldete Menge einem Packmittel zugeordnet ist. Das Feld ist nicht editierbar; es wird bei jeder Änderung automatisch neu berechnet. Die Farbmarkierung unterstützt die schnelle Erkennung (siehe Werte unten). |
| **Packmittelreferenz Nr.** | Wenn Sie hier eine Packmittelreferenz auswählen, dann wird die zugehörige Verpackungsvorschrift auf die Rückmeldezeile angewendet und das Material entsprechend zugeordnet. Auswahl über die Nachschlagefunktion. War bereits am Fertigungs- oder Verkaufsauftrag eine Packmittelreferenz hinterlegt, dann erscheint diese hier als Vorgabe. Die Auswahl ist **nur möglich**, wenn der **Packmittelstatus (leer)** ist und die **Menge** größer als **0** ist; andernfalls erscheint die Meldung, dass die Referenz nicht ausgewählt werden kann, weil die Position null ist oder bereits einem Packmittel zugeordnet ist. |

**Werte des Feldes Packmittelstatus** (alle möglichen Werte):

- **(leer):** Der Rückmeldezeile ist **kein** Packmittel zugeordnet. In diesem Zustand können Sie eine
  **Packmittelreferenz Nr.** setzen oder über **Packmittelzuweisung** ein Packmittel zuordnen.
- **Teilweise:** Es ist **weniger** als die gesamte gemeldete Menge einem Packmittel zugeordnet. Das Feld wird
  gelb hervorgehoben. Sie können weitere Menge zuordnen, bis der Status auf **Voll** wechselt.
- **Voll:** Die **gesamte** gemeldete Menge ist einem Packmittel zugeordnet. Das Feld wird grün hervorgehoben;
  die Zuordnung ist vollständig.
- **Packmittel:** Die Zeile ist **selbst ein Packmittel** (Packmittelartikel). Das Feld wird fett hervorgehoben.
  In diesem Zustand ist **Aus Paketreferenz erstellen** nicht verfügbar, da die Zeile bereits ein Packmittel
  darstellt.

#### Aktionen im Register Packmittel

| Aktion | Erläuterung |
|--------|-------------|
| **Packmittelzuweisung** | Öffnet die **Beleg Packmittel Liste**, in der Sie der Rückmeldezeile Packmittel zuordnen. Wenn ausgelöst, dann prüft die App zunächst, dass ein **Lagerort** gesetzt ist; anschließend öffnet sich die Liste mit den Aktionen **Packmittel erstellen** (neues Packmittel anlegen) und **Packmittel füllen** (vorhandenes Packmittel befüllen). Nach der Zuordnung wird der **Packmittelstatus** aktualisiert. Diese Aktion ist zusätzlich als angeheftete Aktion im Prozessmenü verfügbar. |
| **Aus Paketreferenz erstellen** | Erstellt die Packmittelzuordnung automatisch aus der hinterlegten Packmittelreferenz der Zeile. Wenn ausgelöst, dann werden die Packmittel gemäß Referenz für die Rückmeldezeile erzeugt und zugeordnet. Verfügbar nur, solange der **Packmittelstatus** nicht **Packmittel** ist. |

### 5.4 Packmittel Factbox

Die **Packmittel Factbox** wird durch diese App sowohl in der Liste **FA-Arbeitsvorrat** als auch in der
**FA-Arbeitsvorrat Buchung** eingeblendet. Sie zeigt die Packmittelstruktur zum jeweiligen Fertigungsauftrag als
Baum (übergeordnete Packmittel mit ihren untergeordneten Positionen) und dient der Kontrolle der Zuordnung,
ohne die Maske zu wechseln.

| Feld | Erläuterung |
|------|-------------|
| **Packmittel Nr.** | Nummer des Packmittels in der Struktur. Wird als Wurzelknoten des Baums fett dargestellt, wenn die Zeile ein Packmittel ist. |
| **Packmittelcode** | Code (Art) des Packmittels; beschreibt, um welches Packmittel es sich handelt. |
| **Artikelnr.** | Artikel, der im Packmittel enthalten ist. |
| **Chargennr.** | Charge des enthaltenen Artikels, sofern chargengeführt. |
| **Seriennr.** | Seriennummer des enthaltenen Artikels, sofern seriengeführt. |
| **Variante** | Variante des enthaltenen Artikels. |
| **Zeilenart** | Art der Strukturzeile (z. B. Packmittel oder enthaltene Position). Bestimmt, wie die Zeile im Baum interpretiert wird. |
| **Packmittelgruppennr.** | Zuordnung der Zeile zu einer Packmittelgruppe. |
| **Übergeordnete Packmittel Nr.** | Verweis auf das übergeordnete Packmittel; bildet die Hierarchie des Baums ab. |
| **Menge** | Enthaltene bzw. zu handhabende Menge der Strukturzeile. |
| **Beschreibung** | Beschreibung der Strukturzeile. |
| **Beschreibung 2** | Ergänzende Beschreibung der Strukturzeile. |
| **Lagerort** | Lagerort der Strukturzeile. |
| **Lagerplatz** | Lagerplatz der Strukturzeile innerhalb des Lagerorts. |
| Technische bzw. Hierarchiespalten (Level, Lfd.-Nr., Reihenfolgenzeilennr.) | Interne Sortier- und Hierarchiefelder der Struktur; für die tägliche Zuordnung nicht relevant und daher zusammengefasst. |

## 6. FAQ und Troubleshooting

### 1. Warum finde ich die FA-Arbeitsvorrat Buchung nicht über die Suche?

Die **FA-Arbeitsvorrat Buchung** ist bewusst nicht über **Suchen** erreichbar. Sie öffnet sich nur, wenn Sie in
der Liste **FA-Arbeitsvorrat** einen gestarteten Auftrag mit **Teilbeenden** oder **Beenden** zurückmelden.
Rufen Sie daher zuerst die Liste über **Suchen** auf.

### 2. Warum erscheint das Register Packmittel bei mir nicht?

Das Register **Packmittel**, die Aktionen und die **Packmittel Factbox** werden nur eingeblendet, wenn alle drei
Apps installiert sind: **m+m Packmittel**, **m+m FA-Arbeitsvorrat** und **m+m Prod. Order Job Overview with
Package Mgt.**. Fehlt eine Voraussetzung, fehlt auch der Packmittel-Bereich.

### 3. Warum kann ich keine Packmittelreferenz Nr. auswählen?

Eine **Packmittelreferenz Nr.** lässt sich nur setzen, wenn der **Packmittelstatus (leer)** ist **und** die
**Menge** größer als **0** ist. Ist die Zeile bereits einem Packmittel zugeordnet oder ist die Menge null,
erscheint eine Meldung und die Auswahl wird abgewiesen. Erfassen Sie zuerst eine Menge und heben Sie eine
bestehende Zuordnung auf, bevor Sie die Referenz wählen.

### 4. Warum verlangt die Packmittelzuweisung einen Lagerort?

Die Aktion **Packmittelzuweisung** prüft vor dem Öffnen der **Beleg Packmittel Liste**, dass ein **Lagerort**
gesetzt ist. Ohne Lagerort kann das Packmittel keinem Bestand zugeordnet werden. Tragen Sie deshalb in der
Buchungsmaske zuerst den **Lagerort** ein.

### 5. Was bedeutet der Packmittelstatus Teilweise?

**Teilweise** bedeutet, dass nur ein Teil der gemeldeten **Menge** einem Packmittel zugeordnet ist. Der Status
wird gelb hervorgehoben. Ordnen Sie weitere Menge zu, bis der Status auf **Voll** wechselt, wenn die vollständige
Zuordnung gewünscht ist.

### 6. Was bedeutet der Packmittelstatus Voll?

**Voll** bedeutet, dass die **gesamte** gemeldete Menge einem Packmittel zugeordnet ist. Der Status wird grün
hervorgehoben. Eine weitere Zuordnung ist nicht erforderlich.

### 7. Wann ist Aus Paketreferenz erstellen verfügbar?

Die Aktion **Aus Paketreferenz erstellen** ist verfügbar, solange der **Packmittelstatus** nicht **Packmittel**
ist. Ist die Zeile selbst ein Packmittel, entfällt die Aktion, da bereits ein Packmittel vorliegt.

### 8. Muss ich einen Auftrag vollständig beenden, oder darf ich teilweise zurückmelden?

Sie dürfen mit **Teilbeenden** eine Teilmenge zurückmelden; der Auftrag bleibt für die Restmenge offen. Es ist
**nicht** erforderlich, auf einen ausgeglichenen Restbestand zu warten. Erst **Beenden** meldet die Restmenge
zurück und schließt den Arbeitsgang ab.

### 9. Wie sehe ich die Packmittelstruktur zu einem Auftrag, ohne zu buchen?

Nutzen Sie die **Packmittel Factbox**. Sie wird in der Liste **FA-Arbeitsvorrat** und in der Buchungsmaske
angezeigt und stellt die zugeordneten Packmittel als Baum dar – auch ohne dass Sie eine Buchung auslösen.

### 10. Ich habe mich vertan – wie mache ich eine Rückmeldung rückgängig?

Setzen Sie den betroffenen Arbeitsgang in der Liste **FA-Arbeitsvorrat** über **Auf Offen setzen** wieder auf
offen. Anschließend können Sie den Auftrag erneut starten und korrekt mit der gewünschten Packmittelzuordnung
zurückmelden.

## 7. Typische Anwendungsfälle (Nutzungsbeispiele)

### Anwendungsfall 1: Rückmeldung mit einem neuen Packmittel

- **Auslöser:** Ein Mitarbeiter in der Fertigung hat einen Arbeitsgang abgeschlossen und muss die gefertigte Menge
  zurückmelden sowie ein neu gepacktes Packmittel erfassen.
- **Einstieg in BC:** Über **Suchen** die Liste **FA-Arbeitsvorrat** öffnen, **Arbeitsplatzgruppennr.**
  auswählen, die Auftragszeile markieren.
- **Kernablauf:** **Starten** (falls noch nicht laufend), dann **Beenden**. In der **FA-Arbeitsvorrat Buchung**
  Zeiten und **Menge** erfassen, **Lagerort** setzen. Im Register **Packmittel** die Aktion
  **Packmittelzuweisung** wählen; in der **Beleg Packmittel Liste** über **Packmittel erstellen** ein neues
  Packmittel anlegen und der Zeile zuordnen. Der **Packmittelstatus** wechselt auf **Teilweise** oder **Voll**.
- **Abschluss:** Mit **OK** bestätigen. Die Rückmeldung wird gebucht.

### Anwendungsfall 2: Rückmeldung mit einem vorhandenen Packmittel

- **Auslöser:** Das benötigte Packmittel wurde bereits physisch gepackt und existiert im System.
- **Einstieg in BC:** Wie Anwendungsfall 1 bis zur **FA-Arbeitsvorrat Buchung**.
- **Kernablauf:** Im Register **Packmittel** **Packmittelzuweisung** wählen. In der **Beleg Packmittel Liste**
  über **Packmittel füllen** das vorhandene Packmittel auswählen und die gemeldete Menge zuordnen. Übernehmen
  Sie das ausgewählte Packmittel in die Buchungsmaske; ist die Menge vollständig zugeordnet, zeigt der
  **Packmittelstatus** den Wert **Voll**.
- **Abschluss:** Mit **OK** bestätigen. Die Rückmeldung wird gebucht.

### Anwendungsfall 3: Rückmeldung über eine Packmittelreferenz

- **Auslöser:** Für den Auftrag gilt eine Verpackungsvorschrift, die bereits am Fertigungs- oder Verkaufsauftrag
  als Packmittelreferenz hinterlegt wurde.
- **Einstieg in BC:** Wie Anwendungsfall 1 bis zur **FA-Arbeitsvorrat Buchung**.
- **Kernablauf:** Im Register **Packmittel** ist die **Packmittelreferenz Nr.** häufig bereits als Vorgabe
  gefüllt. Andernfalls wählen Sie sie über die Nachschlagefunktion (nur bei **Packmittelstatus (leer)** und
  **Menge** größer **0**). Alternativ erzeugen Sie die Zuordnung automatisch über **Aus Paketreferenz
  erstellen**. Die Packmittel werden gemäß Referenz zugeordnet und der **Packmittelstatus** aktualisiert.
- **Abschluss:** Mit **OK** bestätigen. Die Buchung wird durchgeführt und die Rückmeldung des
  Fertigungsauftrags abgeschlossen.
