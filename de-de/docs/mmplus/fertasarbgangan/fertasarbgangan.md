---
title: Anwenderhandbuch m+m Production Order Assistant with Routing Status View
---

# Anwenderhandbuch m+m Production Order Assistant with Routing Status View

## Einleitung

Die App **m+m Production Order Assistant with Routing Status View** ist eine Erweiterung für **Microsoft Dynamics 365 Business Central**. Sie verbindet zwei bestehende m+m-Funktionen miteinander: den **Fertigungsassistenten**, mit dem aus einer Verkaufszeile heraus ein Fertigungsauftrag erzeugt wird, und die grafische **Arbeitsgangstatusanzeige**, die im Verkaufsauftrag den Fortschritt der zugehörigen Fertigung darstellt.

Ohne diese Erweiterung speist die Arbeitsgangstatusanzeige ihre Daten ausschließlich aus **Reservierungsposten** und **Artikelposten**, die mit der Verkaufszeile verknüpft sind. In vielen auftragsbezogenen Fertigungen besteht diese Reservierungsverknüpfung jedoch nicht (der Fertigungsauftrag wurde direkt aus der Verkaufszeile über den Fertigungsassistenten erzeugt, aber nicht gegen die Verkaufszeile reserviert). In diesem Fall bliebe die Anzeige leer.

Diese App schließt genau diese Lücke: Sie sorgt dafür, dass die Arbeitsgangstatusanzeige zusätzlich **alle Fertigungsaufträge** berücksichtigt, die der Fertigungsassistent aus der jeweiligen Verkaufszeile erstellt hat. Die Zuordnung erfolgt nicht über Reservierungen, sondern über die Zielfelder, die der Fertigungsassistent beim Anlegen des Fertigungsauftrags setzt (Zieltyp **Verkaufsauftrag**, Zielbelegnummer und Zielzeilennummer). Dadurch wird der **Arbeitsplanstatus** dieser Fertigungsaufträge direkt im Verkaufsauftrag sichtbar.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender im Verkauf und in der Fertigung**, die aus Kundenaufträgen heraus Fertigungsaufträge anstoßen und deren Fortschritt am Verkaufsauftrag verfolgen: Auftragssachbearbeiter, Fertigungssteuerung und Vertriebsinnendienst. Administratoren sind sekundäre Zielgruppe; ihre Aufgabe beschränkt sich auf die einmalige Installation und die Berechtigungsvergabe (siehe **Voraussetzungen und Einrichtung**), da die App bewusst **keine eigenen Einrichtungsseiten** besitzt.

### Einordnung und Abhängigkeiten

Die App ist eine reine Verbindungs-Erweiterung. Sie enthält keine eigenen Seiten, Tabellen oder Einrichtungsfelder. Ihre gesamte Wirkung entfaltet sie über die folgenden Basismodule, die installiert sein müssen:

- **m+m Production Order Assistant** — stellt in der Verkaufszeile die Aktion **Fertigungsassistent** bereit und markiert die erzeugten Fertigungsaufträge mit den Zielfeldern (Zieltyp, Zielbelegnr., Zielzeilennr.).
- **m+m Routing Status Overview** — stellt die grafische **Arbeitsgangstatusanzeige** im Verkaufsauftrag bereit und liefert die Basislogik, welche Fertigungsauftragszeilen angezeigt werden.
- **m+m Cloud Base** — technisches Basismodul.

Diese App ergänzt lediglich die Auswahllogik der Arbeitsgangstatusanzeige um die vom Fertigungsassistenten verknüpften Fertigungsaufträge.

## Schnellstart für Anwender

Der schnellste Weg vom Kundenauftrag zur Statusverfolgung:

1. Öffnen Sie den **Verkaufsauftrag** und erfassen Sie die Verkaufszeile mit dem zu fertigenden Artikel (Typ **Artikel**, Artikelnummer und Menge).
2. Markieren Sie die Verkaufszeile und wählen Sie im Zeilenmenü **Zeile** die Aktion **Fertigungsassistent**.
3. Bestätigen Sie die Ansicht **Fertigungsassistent** mit **OK**. Business Central legt daraufhin den Fertigungsauftrag an und verknüpft ihn über die Zielfelder mit dieser Verkaufszeile.
4. Kehren Sie in den **Verkaufsauftrag** zurück. Der Bereich **Arbeitsgangstatusanzeige** unterhalb der Verkaufszeilen aktualisiert sich beim Wechsel auf die Verkaufszeile automatisch und zeigt den Arbeitsplan-Fortschritt der verknüpften Fertigungsaufträge — grafisch und als Zeilenliste.
5. Beurteilen Sie den Fortschritt anhand der Farbe (siehe Farblegende unter **Tägliche Arbeit**) und öffnen Sie bei Bedarf per Klick den zugehörigen **FA-Arbeitsplan** oder den Fertigungsauftrag.

Ein separater Einrichtungsschritt im Tagesgeschäft entfällt: Sobald der Fertigungsassistent den Fertigungsauftrag erzeugt hat, ist die Verknüpfung gesetzt und die Anzeige gefüllt.

## Voraussetzungen und Einrichtung

Diese Erweiterung besitzt **keine eigene Einrichtungsseite, keine Einrichtungstabelle und keinen Einrichtungsschalter**. Es gibt daher keine modulspezifischen Felder zu pflegen. Die Einrichtung beschränkt sich auf zwei administrative Schritte, die einmalig vor der ersten Nutzung durchzuführen sind.

### App-Voraussetzungen bereitstellen

Wer richtet ein: Administrator. Wann: einmalig vor der ersten Nutzung. Wozu: Die Anzeigelogik dieser App greift nur, wenn die drei Basismodule vorhanden sind.

Stellen Sie die folgende Abhängigkeitskette in Reihenfolge sicher:

1. **m+m Cloud Base** ist installiert (technische Grundlage).
2. **m+m Production Order Assistant** ist installiert. Wenn dieses Modul aktiv ist, dann steht in der Verkaufszeile die Aktion **Fertigungsassistent** zur Verfügung, und erzeugte Fertigungsaufträge tragen die Zielfelder, über die diese App verknüpft.
3. **m+m Routing Status Overview** ist installiert. Wenn dieses Modul aktiv ist, dann erscheint im Verkaufsauftrag der Bereich **Arbeitsgangstatusanzeige**, den diese App mit zusätzlichen Fertigungsauftragszeilen versorgt.
4. **m+m Production Order Assistant with Routing Status View** (diese App) ist installiert. Wenn diese App aktiv ist, dann werden in der Arbeitsgangstatusanzeige auch die vom Fertigungsassistenten verknüpften, nicht reservierten Fertigungsaufträge angezeigt.

Ist eine der ersten drei Apps nicht vorhanden, bleibt die Zusatzlogik ohne Wirkung; die Basisanzeige richtet sich dann allein nach Reservierungs- und Artikelposten.

### Berechtigung zuweisen

Wer richtet ein: Administrator. Wann: bei der Rollenvergabe. Wozu: Der Berechtigungssatz legt fest, welche Aktionen die Anwender mit der Funktion ausführen dürfen.

Weisen Sie den betroffenen Anwendern den Berechtigungssatz **MuM PARO Permission** zu. Wenn dieser Berechtigungssatz einer Rolle zugeordnet ist, dann darf die Anzeigelogik dieser App für diese Anwender ausgeführt werden; die zusätzlichen Fertigungsauftragszeilen erscheinen in der Arbeitsgangstatusanzeige. Ohne diese Berechtigung bleibt die Ergänzung dieser App inaktiv, während die Basisanzeige weiterhin funktioniert. Der Berechtigungssatz umfasst ausschließlich die Ausführung der internen Anzeigelogik dieser App und vergibt keine weitergehenden Rechte auf Fertigungs- oder Verkaufsdaten; diese Rechte stammen aus den Berechtigungssätzen der Basismodule.

## Tägliche Arbeit am Verkaufsauftrag

Der zentrale Arbeitsplatz dieser Funktion ist der **Verkaufsauftrag**. Unterhalb der Verkaufszeilen zeigt der Bereich **Arbeitsgangstatusanzeige** den Fertigungsfortschritt zur jeweils markierten Verkaufszeile an. Die Anzeige besteht aus zwei Teilen: einer **grafischen Darstellung** (Statusgrafik) und einer **Zeilenliste** der zugehörigen Fertigungsauftragszeilen.

Voraussetzung dafür, dass hier Daten erscheinen, sind die im Kapitel **Voraussetzungen und Einrichtung** genannten Basismodule sowie ein Fertigungsauftrag, der über den **Fertigungsassistenten** aus der Verkaufszeile erzeugt wurde. Der Inhalt der Anzeige wird bei jedem Wechsel der Verkaufszeile automatisch neu ermittelt; eine manuelle Aktualisierung ist nicht erforderlich.

### Fertigungsauftrag aus der Verkaufszeile erzeugen

Wer arbeitet hier: Auftragssachbearbeiter oder Fertigungssteuerung. Wann: sobald ein zu fertigender Artikel im Kundenauftrag steht.

1. Öffnen Sie den **Verkaufsauftrag** und markieren Sie die Verkaufszeile.
2. Wählen Sie **Zeile** und dann **Fertigungsassistent**. Die Ansicht **Fertigungsassistent** öffnet sich.
3. Bestätigen Sie mit **OK**. Wenn Sie bestätigen, dann erzeugt Business Central den Fertigungsauftrag und setzt an der Fertigungsauftragszeile die Zielfelder (Zieltyp **Verkaufsauftrag**, Zielbelegnummer und Zielzeilennummer der Verkaufszeile). Genau über diese Zielfelder findet diese App den Fertigungsauftrag später wieder und blendet ihn in der Arbeitsgangstatusanzeige ein.

Der Status, in dem der Fertigungsauftrag angelegt wird (zum Beispiel geplant, fest geplant oder freigegeben), richtet sich nach der Einrichtung des Fertigungsassistenten und ist nicht Bestandteil dieser App.

### Die Arbeitsgangstatusanzeige lesen

Die Zeilenliste der Arbeitsgangstatusanzeige enthält zu jeder angezeigten Fertigungsauftragszeile die folgenden Spalten. Alle Spalten sind schreibgeschützt; sie dienen der Information und dem Einstieg in die Details.

| Feld | Erläuterung |
|---|---|
| **Ebene** | Zeigt die Struktureinrückung der Zeile in der Baumdarstellung. Wenn eine mehrstufige Fertigung dargestellt wird, dann macht die Ebene sichtbar, welche Zeile über- und welche untergeordnet ist. |
| **Status** | Gibt den Auftragsstatus des Fertigungsauftrags an, aus dem die Zeile stammt. Die zulässigen Werte werden unten je Bedeutung erläutert. |
| **Fertigungsauftragsnr.** | Nummer des Fertigungsauftrags. Wenn Sie diese Nummer anklicken, dann öffnet sich der zugehörige Fertigungsauftrag (bzw. der FA-Arbeitsplan), sodass Sie die Details ohne Umweg prüfen können. |
| **Beschreibung** | Beschreibung der Fertigungsauftragszeile (in der Regel der zu fertigende Artikel). Dient der schnellen Identifikation der Zeile. |
| **Menge** | Zu fertigende Menge der Fertigungsauftragszeile. Wenn Sie Soll- und Fertigstellungsmenge vergleichen, dann erkennen Sie den offenen Rest. |
| **Startdatum** | Geplanter Beginn der Fertigung. Wenn das Startdatum in der Zukunft liegt, dann hat die Bearbeitung planmäßig noch nicht begonnen. |
| **Startzeit** | Geplante Startuhrzeit ergänzend zum Startdatum bei feiner terminierter Fertigung. |
| **Enddatum** | Geplantes Ende der Fertigung. Wenn das Enddatum überschritten ist und der Auftrag noch nicht beendet wurde, dann liegt ein Terminverzug vor. |
| **Endzeit** | Geplante Enduhrzeit ergänzend zum Enddatum. |
| **Fertiggestellte Menge** | Bereits fertiggemeldete Menge der Zeile. Wenn die fertiggestellte Menge die Menge erreicht, dann ist die Fertigung dieser Zeile abgeschlossen; solange sie kleiner ist, steht noch eine Restmenge aus. |

**Werte der Spalte Status** (Auftragsstatus des Fertigungsauftrags):

- **Simuliert:** Der Fertigungsauftrag ist eine Simulation und noch nicht produktionswirksam; er dient der Vorkalkulation.
- **Geplant:** Der Fertigungsauftrag ist geplant, aber noch nicht fest eingeplant; Termine und Mengen können sich noch verschieben.
- **Fest geplant:** Der Fertigungsauftrag ist fest eingeplant; er ist für die Fertigung vorgesehen, aber noch nicht freigegeben.
- **Freigegeben:** Der Fertigungsauftrag ist zur Fertigung freigegeben; Rückmeldungen und Buchungen sind möglich, die fertiggestellte Menge kann wachsen.
- **Beendet:** Der Fertigungsauftrag ist beendet; die Fertigung ist abgeschlossen und es sind keine weiteren Rückmeldungen zu erwarten.

Die Basisanzeige berücksichtigt in der Regel freigegebene und beendete Fertigungsaufträge aus Reservierungs- und Artikelposten. Durch diese App kommen zusätzlich die vom Fertigungsassistenten verknüpften Fertigungsaufträge hinzu, unabhängig von einer Reservierung.

### Farbliche Statusdarstellung

Die grafische Darstellung färbt jeden Arbeitsgang nach seinem **Arbeitsplanstatus** im FA-Arbeitsplan ein. So erkennen Sie den Fortschritt auf einen Blick, ohne die Zeilenliste zu lesen. Die Färbung selbst wird vom Basismodul **m+m Routing Status Overview** bestimmt; diese App entscheidet lediglich, **welche** Fertigungsaufträge in die Grafik einfließen.

| Arbeitsplanstatus | Farbe | Bedeutung für den Anwender |
|---|---|---|
| **Leer** | grau | Für den Arbeitsgang ist noch kein Arbeitsplanstatus gesetzt; die Bearbeitung ist noch nicht eingeplant. |
| **Geplant** | grün | Der Arbeitsgang ist eingeplant; die Bearbeitung steht bevor. |
| **In Bearbeitung** | rot | Der Arbeitsgang wird gerade bearbeitet; er ist begonnen, aber noch nicht abgeschlossen. |
| **Fertig** | blau | Der Arbeitsgang ist abgeschlossen. |

### In die Details wechseln

Aus der Arbeitsgangstatusanzeige gelangen Sie ohne Suchen direkt in die zugrunde liegenden Belege:

- Ein Klick auf einen Eintrag in der Grafik bzw. auf die **Fertigungsauftragsnr.** öffnet den **FA-Arbeitsplan** des betreffenden Fertigungsauftrags. Dort sehen Sie die einzelnen Arbeitsgänge und deren Status im Detail.
- Über die Fertigungsauftragszeile erreichen Sie den Fertigungsauftrag selbst in dem Status, in dem er sich befindet (zum Beispiel den freigegebenen oder den beendeten Fertigungsauftrag).

Diese Absprünge sind schreibgeschützt geöffnet, damit die Statusanzeige nicht versehentlich verändert wird.

## FAQ und Troubleshooting

### 1. Warum erscheint in der Arbeitsgangstatusanzeige nichts, obwohl ein Fertigungsauftrag existiert?

Die Anzeige wird pro **Verkaufszeile** ermittelt. Prüfen Sie, ob der Fertigungsauftrag tatsächlich über den **Fertigungsassistenten** aus genau dieser Verkaufszeile erzeugt wurde und die Zielfelder gesetzt sind. Ist der Fertigungsauftrag manuell und ohne Reservierungsbezug angelegt worden, kennt weder die Basisanzeige noch diese App die Verknüpfung.

### 2. Was ist der Unterschied zwischen dieser App und der reinen Arbeitsgangstatusanzeige?

Die Basisanzeige (Modul m+m Routing Status Overview) füllt sich aus **Reservierungsposten** und **Artikelposten**. Diese App ergänzt sie um Fertigungsaufträge, die der **Fertigungsassistent** über die Zielfelder mit der Verkaufszeile verknüpft hat — auch dann, wenn keine Reservierung besteht.

### 3. Warum sehe ich einen Fertigungsauftrag hier, obwohl er nicht gegen die Verkaufszeile reserviert ist?

Genau das ist der Zweck dieser App. Sie wertet die Zielfelder des Fertigungsassistenten aus (Zieltyp **Verkaufsauftrag**, Zielbelegnummer, Zielzeilennummer) und blendet die passenden Fertigungsauftragszeilen ein, unabhängig von Reservierungsposten.

### 4. Welche Verkaufsbelege werden berücksichtigt?

Die Zusatzlogik dieser App greift für den Zieltyp **Verkaufsauftrag**. Der Fertigungsassistent kann Fertigungsaufträge zwar auch mit dem Zieltyp **Verkaufsangebot** oder ohne Zieltyp (**leer**) markieren; die Arbeitsgangstatusanzeige dieser App ist jedoch auf den Verkaufsauftrag ausgerichtet.

### 5. Muss ich die Anzeige manuell aktualisieren?

Nein. Die Anzeige aktualisiert sich automatisch, sobald Sie im Verkaufsauftrag die Zeile wechseln. Es gibt keine gesonderte Aktualisieren-Aktion für diesen Bereich.

### 6. Was bedeuten die Farben grau, grün, rot und blau?

Sie geben den **Arbeitsplanstatus** des jeweiligen Arbeitsgangs wieder: grau = **Leer** (noch nicht eingeplant), grün = **Geplant**, rot = **In Bearbeitung**, blau = **Fertig**. Die Farbregel stammt aus dem Basismodul.

### 7. Wie komme ich vom Statusbereich zu den Arbeitsgängen im Detail?

Klicken Sie auf den Eintrag in der Grafik oder auf die **Fertigungsauftragsnr.** in der Zeilenliste. Es öffnet sich der **FA-Arbeitsplan** des Fertigungsauftrags mit allen Arbeitsgängen.

### 8. Warum ist der Statusbereich leer, obwohl die Farben früher angezeigt wurden?

Prüfen Sie, ob alle drei Basismodule sowie diese App aktiv sind und ob den Anwendern der Berechtigungssatz **MuM PARO Permission** zugewiesen ist. Fehlt eine Voraussetzung, füllt sich die Anzeige nur noch über die Basislogik (Reservierungs-/Artikelposten) oder bleibt leer.

### 9. Kann ich Werte im Statusbereich ändern?

Nein. Alle Spalten und die Grafik sind schreibgeschützt. Änderungen nehmen Sie im Fertigungsauftrag bzw. im FA-Arbeitsplan vor, den Sie per Klick erreichen.

### 10. Woran erkenne ich, dass ein Fertigungsauftrag über den Fertigungsassistenten erzeugt wurde?

Am Fertigungsauftrag bzw. an der Fertigungsauftragszeile sind die Zielfelder gesetzt (Zieltyp, Zielbelegnummer, Zielzeilennummer). Diese Felder werden vom Fertigungsassistenten beim Anlegen gefüllt und sind zugleich der Schlüssel, über den diese App die Zeile in die Arbeitsgangstatusanzeige aufnimmt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Auftragsbezogene Fertigung anstoßen und verfolgen

**Auslöser:** Ein Kunde bestellt telefonisch einen Artikel, der eigens gefertigt werden muss.

**Einstieg in BC:** Der Auftragssachbearbeiter erfasst den **Verkaufsauftrag** mit der Verkaufszeile (Artikel und Menge). In der Verkaufszeile wählt er **Zeile** und dann **Fertigungsassistent**.

**Kernablauf:** In der Ansicht **Fertigungsassistent** bestätigt er mit **OK**. Business Central legt den Fertigungsauftrag an und setzt die Zielfelder auf Zieltyp **Verkaufsauftrag** sowie auf Belegnummer und Zeilennummer der Verkaufszeile. Zurück im Verkaufsauftrag wechselt der Sachbearbeiter auf die Verkaufszeile; der Bereich **Arbeitsgangstatusanzeige** aktualisiert sich und zeigt die Fertigungsauftragszeile mit Spalten wie **Status**, **Menge** und **Fertiggestellte Menge** sowie die farbige Statusgrafik.

**Abschluss:** Im weiteren Verlauf verfolgt der Sachbearbeiter die Farbe der Arbeitsgänge (grün → rot → blau) und die wachsende **Fertiggestellte Menge**. Sobald die Arbeitsgänge blau (**Fertig**) sind und die fertiggestellte Menge die Menge erreicht, ist die Fertigung abgeschlossen. Für Details öffnet er per Klick auf die **Fertigungsauftragsnr.** den **FA-Arbeitsplan**.

### Anwendungsfall 2: Fortschritt eines nicht reservierten Fertigungsauftrags sehen

**Auslöser:** Die Fertigungssteuerung hat einen Fertigungsauftrag über den Fertigungsassistenten erzeugt, ihn aber nicht gegen die Verkaufszeile reserviert. Der Vertrieb fragt nach dem Stand.

**Einstieg in BC:** Der Anwender öffnet den betreffenden **Verkaufsauftrag** und markiert die Verkaufszeile.

**Kernablauf:** Ohne diese App bliebe die Arbeitsgangstatusanzeige hier leer, weil kein Reservierungsposten existiert. Mit dieser App erkennt Business Central den Fertigungsauftrag über die Zielfelder des Fertigungsassistenten und zeigt seine Fertigungsauftragszeilen samt Arbeitsplanstatus an. Der Anwender liest den Fortschritt aus Farbe und Spalten ab.

**Abschluss:** Bei Rückfragen springt der Anwender über die **Fertigungsauftragsnr.** in den **FA-Arbeitsplan** und meldet dem Vertrieb den aktuellen Arbeitsgangstatus zurück. Ein Buchungs- oder Freigabeschritt ist in diesem Bereich nicht erforderlich; die Anzeige dient ausschließlich der Information.
