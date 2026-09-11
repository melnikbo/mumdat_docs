---
title: Anwenderhandbuch m+m Item Status
---

# Anwenderhandbuch m+m Item Status

## Einleitung

Die App m+m Item Status (**Artikelstatus**) erweitert Microsoft Dynamics 365 Business Central um eine Funktion, mit der ein Artikel gezielt für einzelne Geschäftsvorfälle gesperrt werden kann. Über einen **Artikelstatus** legen Sie fest, welche Belege, Buchblattbuchungen und Lagervorgänge für einen Artikel noch zulässig sind und welche das System blockiert.

Anders als die einfache Standardsperre in Business Central, die einen Artikel entweder vollständig oder gar nicht sperrt, arbeitet der Artikelstatus **feingranular**: Sie können denselben Artikel beispielsweise für den Einkauf sperren, während der Verkauf des noch vorhandenen Bestands weiterhin möglich bleibt. Innerhalb einer Regel (eines Artikelstatus) sind beliebige Kombinationen der Sperroptionen möglich; jeder Artikel wird jedoch immer nur **einem** Artikelstatus zugeordnet.

Ergänzend stellt die App eine **Requalifizierung** bereit: eine zeitgesteuerte Strategie, die Artikel nach einer definierten Frist automatisch auf einen anderen Artikelstatus umsetzt und die dort hinterlegten Sperren damit selbsttätig aktiviert.

**Zielgruppe:** Primäre Anwender sind die operativen Rollen, die täglich mit Artikeln arbeiten — Einkauf, Verkauf, Lager, Fertigung und Service. Sie erleben den Artikelstatus vor allem in Form von Prüfungen und Sperrmeldungen beim Erfassen von Belegzeilen und Buchblattzeilen. Sekundäre Zielgruppe sind Administratoren und Stammdatenverantwortliche, die die Artikelstatus und Requalifizierungen einrichten und den Artikeln zuweisen.

**Typischer Ablauf:** Zuerst definiert ein Administrator in der **Artikelstatusliste** die Sperrregeln und legt optional in den **Artikelstatus-Requalifizierungen** eine zeitgesteuerte Umsetzung fest. Anschließend weist ein Stammdatenverantwortlicher den betroffenen Artikeln über die **Artikelkarte** (Aktion **Artikelstatus setzen**) den passenden Status zu. Ab diesem Zeitpunkt greifen die Sperren sofort: Erfasst ein Anwender eine gesperrte Belegzeile, verhindert das System die Eingabe mit einer Fehlermeldung. Jede Statusänderung wird in den **Artikelstatusposten** protokolliert.

## Schnellstart für Anwender

Der schnellste Weg von der leeren Installation bis zur wirksamen Sperre folgt der Abhängigkeitsreihenfolge im Code (erst Einrichtung, dann Stammdatenzuweisung, dann Tagesgeschäft):

1. **Artikelstatus anlegen.** Geben Sie in der Suche (**Suchen**) `Artikelstatusliste` ein und öffnen Sie die **Artikelstatusliste**. Legen Sie mit einem sprechenden **Code** und einer **Beschreibung** eine neue Regel an.
2. **Sperroptionen setzen.** Öffnen Sie die Zeile per Doppelklick; es öffnet sich der Artikelstatus (**Artikelstatus**-Karte). Aktivieren Sie in den Registern **Einkauf sperren**, **Verkauf sperren**, **Lager sperren**, **Artikelbuchblatt sperren**, **Produktion sperren** und **Service sperren** die gewünschten Kontrollkästchen — einzeln oder gebündelt über die Aktionen **Alles aktivieren** / **Alles deaktivieren** je Geschäftsbereich.
3. *(Optional)* **Requalifizierung einrichten.** Geben Sie in der Suche `Artikelstatus-Requalifizierungen` ein, legen Sie eine Regel mit **Code**, **Zeitraum** (Datumsformel) und **zu setzender Artikelstatus** an und tragen Sie diesen **Requalifizierungscode** im Artikelstatus ein.
4. **Artikelstatus zuweisen.** Öffnen Sie die **Artikelkarte** des betroffenen Artikels und wählen Sie die Aktion **Artikelstatus setzen**. Wählen Sie den Status aus und bestätigen Sie die Sicherheitsabfrage. Die Felder **Artikelstatuscode** und **Artikelstatus gesetzt am** zeigen anschließend den aktiven Status.
5. **Wirkung im Tagesgeschäft.** Ab sofort blockiert das System die im Status gesperrten Vorgänge, sobald ein Anwender die entsprechende Belegzeile, Buchblattzeile oder Lagerzeile erfasst.

Die Einrichtung (Schritte 1–3) ist Voraussetzung für das Tagesgeschäft (Schritte 4–5) und wird daher zuerst ausgeführt.

## Einrichtung

Die Einrichtung des Artikelstatus umfasst zwei Bereiche: die **Artikelstatusliste** mit den Sperrregeln selbst und — bei zeitgesteuerter Sperre — die **Artikelstatus-Requalifizierungen**. Beide Seiten sind eigenständige Listenseiten dieser App und werden über die Suche geöffnet.

### Artikelstatus einrichten

**Einstieg:** Geben Sie in der Suche (**Suchen**) `Artikelstatusliste` ein und öffnen Sie die **Artikelstatusliste**. Über die Zeile gelangen Sie per Doppelklick auf die zugehörige **Artikelstatus**-Karte.

**Prozess:** Ein Administrator oder Stammdatenverantwortlicher richtet die Artikelstatus **vor** der ersten Zuweisung an Artikel ein. Jeder Artikelstatus ist eine wiederverwendbare Regel: Sie bündelt die gewünschten Sperren und wird später auf der **Artikelkarte** (siehe Kapitel *Tägliche Arbeit an der Artikelkarte*) einem oder mehreren Artikeln zugewiesen. Die Sperren wirken erst, sobald ein Artikel mit dem Status verknüpft ist.

Die **Artikelstatusliste** zeigt die vorhandenen Regeln im Überblick:

| Feld | Erläuterung |
|------|-------------|
| **Code** | Eindeutige Benennung der Regel (Pflichtfeld). Wenn Sie einen Code vergeben, kann dieser Artikelstatus anschließend Artikeln zugewiesen und in Requalifizierungen referenziert werden. |
| **Beschreibung** | Klartextbezeichnung der Regel. Wenn gepflegt, erscheint dieser Text in Auswahllisten und in der Sperrmeldung, sodass der Anwender im Fehlerfall sofort erkennt, welche Regel greift. |
| **Requalifizierungscode** | Verknüpfung zu einer **Artikelstatus-Requalifizierung**. Wenn gesetzt, prüft der tägliche Hintergrundlauf, ob Artikel mit diesem Status nach Ablauf der hinterlegten Frist automatisch auf einen anderen Status umgesetzt werden; ohne Eintrag bleibt der Status zeitlich unbefristet bestehen. |

Auf der **Artikelstatus**-Karte gliedern sich die Sperroptionen in sechs fachliche Register. Jede Option ist ein Kontrollkästchen: **Wenn aktiviert, dann** verhindert das System den jeweiligen Vorgang für alle Artikel, die diesen Status tragen; ist das Kennzeichen nicht gesetzt, bleibt der Vorgang uneingeschränkt möglich.

#### Register „Einkauf sperren“

Steuert die Einkaufsseite. Die Prüfung greift beim Validieren der Einkaufszeile (Feld **Nr.**) sowie beim Umwandeln einer Anfrage in eine Bestellung.

| Feld | Erläuterung |
|------|-------------|
| **Anfrage sperren** | Wenn aktiviert, kann der Artikel nicht mehr in eine Einkaufsanfrage (Belegart Anfrage) aufgenommen werden; die Zeilenerfassung bricht mit einer Sperrmeldung ab. |
| **Bestellung sperren** | Wenn aktiviert, wird der Artikel in Einkaufsbestellungen blockiert — auch beim Erzeugen der Bestellung aus einer Anfrage. So verhindern Sie Nachbestellungen eines auslaufenden Artikels. |
| **Rahmenbestellung sperren** | Wenn aktiviert, ist der Artikel in Einkaufsrahmenbestellungen nicht mehr zulässig; bestehende Abrufe müssen über einen anderen Artikel laufen. |
| **Einkaufsrechnung sperren** | Wenn aktiviert, kann der Artikel nicht mehr in Einkaufsrechnungen erfasst werden; die Rechnungsprüfung stoppt vor der Buchung. |
| **Einkaufsgutschrift sperren** | Wenn aktiviert, ist der Artikel in Einkaufsgutschriften gesperrt; Rücksendungen an den Lieferanten über diesen Artikel sind nicht möglich. |

#### Register „Verkauf sperren“

Steuert die Verkaufsseite. Die Prüfung greift beim Validieren der Verkaufszeile (Felder **Nr.** und **Menge**) sowie beim Umwandeln eines Angebots in einen Auftrag.

| Feld | Erläuterung |
|------|-------------|
| **Angebot sperren** | Wenn aktiviert, kann der Artikel nicht mehr in Verkaufsangebote aufgenommen werden; der Vertrieb kann den Artikel Kunden nicht mehr anbieten. |
| **Auftrag sperren** | Wenn aktiviert, wird der Artikel in Verkaufsaufträgen blockiert — auch beim Erzeugen des Auftrags aus einem Angebot. Neue Verkäufe werden dadurch unterbunden. |
| **Rahmenauftrag sperren** | Wenn aktiviert, ist der Artikel in Verkaufsrahmenaufträgen nicht mehr zulässig. |
| **Verkaufsrechnung sperren** | Wenn aktiviert, kann der Artikel nicht mehr in Verkaufsrechnungen erfasst werden; die Fakturierung stoppt vor der Buchung. |
| **Verkaufsgutschrift sperren** | Wenn aktiviert, ist der Artikel in Verkaufsgutschriften gesperrt; Kundenrücknahmen über diesen Artikel sind nicht möglich. |
| **Verkauf bis verfügbarer Bestand erlauben** | Sonderfall für Auslaufartikel. Wenn aktiviert, prüft das System beim Erfassen der Verkaufszeile die Verfügbarkeit: Ist noch Bestand vorhanden, bleibt der Verkauf erlaubt; ist kein Bestand mehr verfügbar, bricht die Erfassung mit dem Hinweis ab, dass der Artikel ein Auslaufteil ist und nur der noch verfügbare Bestand verkauft werden kann. So verkaufen Sie Restbestände ab, ohne Überverkäufe zuzulassen. |

> Hinweis: Das Kennzeichen **Verkauf bis verfügbarer Bestand erlauben** wirkt unabhängig von den übrigen Verkaufssperren als eigenständige Verfügbarkeitsprüfung. Ist es gesetzt, entscheidet die Bestandslage über die Zulässigkeit der Verkaufszeile.

#### Register „Lager sperren“

Steuert Lagervorgänge. Die Prüfung greift beim Einfügen von Wareneingangs-, Warenausgangs- und Lageraktivitätszeilen sowie beim Validieren von Artikelbuchblatt- und Umlagerungszeilen.

| Feld | Erläuterung |
|------|-------------|
| **Wareneingang sperren** | Wenn aktiviert, kann der Artikel nicht in einen Wareneingang aufgenommen werden; die Wareneingangszeile wird beim Einfügen abgewiesen. |
| **Warenausgang sperren** | Wenn aktiviert, wird der Artikel im Warenausgang blockiert; ein Versand über diesen Artikel ist nicht möglich. |
| **Kommissionierung sperren** | Wenn aktiviert, ist der Artikel in Kommissionierzeilen (Lager- und Bestandskommissionierung) gesperrt; der Artikel kann nicht für den Versand entnommen werden. |
| **Einlagerung sperren** | Wenn aktiviert, ist der Artikel in Einlagerungszeilen (Lager- und Bestandseinlagerung) gesperrt; ein Einlagern in Lagerplätze wird verhindert. |
| **Umlagerungsauftrag sperren** | Wenn aktiviert, kann der Artikel nicht in Umlagerungsauftragszeilen erfasst werden; Umlagerungen zwischen Lagerorten über diesen Artikel sind gesperrt. |
| **Umlagerungsbuchblatt sperren** | Wenn aktiviert, wird der Artikel im Umlagerungsbuchblatt sowie bei Artikelbuchblattzeilen mit neuem Lagerort oder neuem Lagerplatz blockiert; interne Umlagerungen werden dadurch unterbunden. |

#### Register „Artikelbuchblatt sperren“

Steuert die direkten Buchblattbuchungen. Die Prüfung greift beim Einfügen und beim Validieren der Artikelnummer in der Artikelbuchblattzeile und richtet sich nach der Buchungsart (Postenart) der Zeile.

| Feld | Erläuterung |
|------|-------------|
| **Artikelbuchblatt (Einkauf) sperren** | Wenn aktiviert, wird eine Artikelbuchblattzeile der Postenart Einkauf für diesen Artikel abgewiesen. |
| **Artikelbuchblatt (Verkauf) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Verkauf blockiert. |
| **Artikelbuchblatt (Verbrauch) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Verbrauch blockiert; ein manueller Verbrauch außerhalb eines Fertigungsauftrags ist nicht möglich. |
| **Artikelbuchblatt (Istmeldung) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Istmeldung blockiert; eine manuelle Fertigmeldung des Artikels wird verhindert. |
| **Artikelbuchblatt (Montageverbrauch) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Montageverbrauch blockiert. |
| **Artikelbuchblatt (Montage-Istmeldung) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Montage-Istmeldung blockiert. |
| **Artikelbuchblatt (Zugang) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Zugang (positive Regulierung) blockiert; manuelle Bestandszugänge werden verhindert. |
| **Artikelbuchblatt (Abgang) sperren** | Wenn aktiviert, wird eine Buchblattzeile der Postenart Abgang (negative Regulierung) blockiert; manuelle Bestandsabgänge werden verhindert. |

> Hinweis: Trägt die Artikelbuchblattzeile einen neuen Lagerort oder neuen Lagerplatz (Umlagerungsbuchung), greift statt der Postenart-Prüfung das Kennzeichen **Umlagerungsbuchblatt sperren** aus dem Register „Lager sperren“.

#### Register „Produktion sperren“

Steuert die Fertigung. Die Prüfung greift beim Validieren der Artikelnummer in Fertigungsauftragszeilen, Fertigungsstücklistenzeilen und FA-Komponenten und richtet sich bei Fertigungsaufträgen nach deren Status.

| Feld | Erläuterung |
|------|-------------|
| **Simulierten Fertigungsauftrag sperren** | Wenn aktiviert, kann der Artikel nicht in einer Fertigungsauftragszeile mit Status Simuliert verwendet werden. |
| **Geplanten Fertigungsauftrag sperren** | Wenn aktiviert, ist der Artikel in Fertigungsauftragszeilen mit Status Geplant gesperrt. |
| **Fest geplanten Fertigungsauftrag sperren** | Wenn aktiviert, ist der Artikel in Fertigungsauftragszeilen mit Status Fest geplant gesperrt. |
| **Freigegebenen Fertigungsauftrag sperren** | Wenn aktiviert, ist der Artikel in freigegebenen Fertigungsauftragszeilen gesperrt; die Produktion des Artikels wird verhindert. Bei bereits beendeten Aufträgen erfolgt keine Prüfung. |
| **Fertigungsstückliste sperren** | Wenn aktiviert, kann der Artikel nicht als Artikelposition in einer Fertigungsstücklistenzeile hinterlegt werden. |
| **FA-Komponente sperren** | Wenn aktiviert, ist der Artikel als Komponente eines Fertigungsauftrags gesperrt; er kann dem Fertigungsauftrag nicht als Verbrauchsmaterial zugeordnet werden. |

#### Register „Service sperren“

Steuert das Servicemodul. Die Prüfung greift beim Validieren der Artikelnummer in Servicezeilen, Serviceartikeln, Serviceartikelzeilen und Servicevertragszeilen und richtet sich nach der jeweiligen Belegart bzw. Vertragsart.

| Feld | Erläuterung |
|------|-------------|
| **Serviceartikel sperren** | Wenn aktiviert, kann der Artikel keinem Serviceartikel zugeordnet werden. |
| **Serviceangebot sperren** | Wenn aktiviert, ist der Artikel in Servicezeilen und Serviceartikelzeilen der Belegart Angebot gesperrt. |
| **Serviceauftrag sperren** | Wenn aktiviert, ist der Artikel in Servicezeilen und Serviceartikelzeilen der Belegart Auftrag gesperrt. |
| **Servicevertragsangebot sperren** | Wenn aktiviert, ist der Artikel in Servicevertragszeilen der Vertragsart Angebot gesperrt. |
| **Servicevertrag sperren** | Wenn aktiviert, ist der Artikel in Servicevertragszeilen der Vertragsart Vertrag gesperrt. |
| **Servicerechnung sperren** | Wenn aktiviert, ist der Artikel in Servicezeilen der Belegart Rechnung gesperrt. |
| **Servicegutschrift sperren** | Wenn aktiviert, ist der Artikel in Servicezeilen der Belegart Gutschrift gesperrt. |

#### Sammelaktionen je Register

Damit Sie nicht jedes Kontrollkästchen einzeln setzen müssen, bietet jedes Register zwei Aktionen. Sie wirken ausschließlich auf die Felder des jeweiligen Geschäftsbereichs:

| Aktion | Erläuterung |
|--------|-------------|
| **Alles aktivieren** | Setzt alle Sperren des jeweiligen Registers (z. B. **Verkauf**) auf aktiv. Im Register **Verkauf** wird dabei auch **Verkauf bis verfügbarer Bestand erlauben** mitgesetzt. |
| **Alles deaktivieren** | Entfernt alle Sperren des jeweiligen Registers wieder. |

Die Sammelaktionen sind je Bereich als Gruppe verfügbar: **Verkauf**, **Einkauf**, **Lager**, **Artikel Buch.-Blatt**, **Produktion** und **Service**.

### Requalifizierung einrichten

**Einstieg:** Geben Sie in der Suche (**Suchen**) `Artikelstatus-Requalifizierungen` ein und öffnen Sie die Seite **Artikelstatus-Requalifizierungen**. Die Verknüpfung zum Artikelstatus erfolgt anschließend über das Feld **Requalifizierungscode** auf der **Artikelstatus**-Karte.

**Prozess:** Die Requalifizierung ist ein optionaler, zeitgesteuerter Baustein und wird von einem Administrator eingerichtet, **nachdem** die Artikelstatus angelegt sind (die Requalifizierung verweist auf einen zu setzenden Artikelstatus). „Requalifizierung“ bedeutet die automatische Umsetzung eines Artikels auf einen anderen Artikelstatus, nachdem eine definierte Frist seit dem Setzen des aktuellen Status abgelaufen ist. Die dort hinterlegten Sperren wirken danach sofort. Der Baustein greift im Tagesgeschäft nicht über eine Anwenderaktion, sondern über einen Hintergrundlauf (siehe unten).

Erläuterungen zu den Feldern der Seite **Artikelstatus-Requalifizierungen**:

| Feld | Erläuterung |
|------|-------------|
| **Code** | Eindeutige Benennung der Requalifizierung (Pflichtfeld). Wenn vergeben, kann die Regel im Feld **Requalifizierungscode** eines Artikelstatus referenziert werden. |
| **Beschreibung** | Klartextbezeichnung der Requalifizierung zur besseren Auffindbarkeit in Auswahllisten. |
| **Zeitraum** | Datumsformel, nach der die Frist berechnet wird (Pflichtfeld, sobald ein zu setzender Artikelstatus hinterlegt ist). Wenn gesetzt, ermittelt der Hintergrundlauf aus dem Feld **Artikelstatus gesetzt am** des Artikels zzgl. dieser Formel den Ablaufzeitpunkt; ist er überschritten, wird der Artikel automatisch auf den zu setzenden Status umgesetzt. Es sind alle in Business Central üblichen Datumsformeln zulässig. |
| **zu setzender Artikelstatus** | Der Artikelstatus, auf den der Artikel bei Ablauf der Frist umgesetzt wird. Wenn gefüllt, ist das Feld **Zeitraum** verpflichtend; wird ein Zeitraum ohne diesen Wert erfasst, weist das System die Erfassung ab. |
| **Artikelstatusbeschreibung** | Zeigt automatisch die **Beschreibung** des zu setzenden Artikelstatus an (berechnetes Feld, nicht editierbar). Dient der Kontrolle, dass die richtige Folgeregel hinterlegt wurde. |

**Prozessschritte (Einrichtung der zeitgesteuerten Sperre):**

1. **Zuerst** legen Sie in der **Artikelstatusliste** den Zielstatus an, den der Artikel nach Fristablauf tragen soll (mit den gewünschten Sperren).
2. **Danach** erfassen Sie in den **Artikelstatus-Requalifizierungen** eine Regel mit **Code**, **Zeitraum** und **zu setzender Artikelstatus**.
3. **Anschließend** hinterlegen Sie diesen **Requalifizierungscode** im ausgehenden Artikelstatus (**Artikelstatus**-Karte).
4. **Zum Schluss** weisen Sie den Artikeln den ausgehenden Status über die Artikelkarte zu (siehe *Tägliche Arbeit an der Artikelkarte*). Ab dann übernimmt der Hintergrundlauf die Umsetzung.

**Kaskadierende Requalifizierung:** Verweist der zu setzende Artikelstatus seinerseits wieder auf eine Requalifizierung, lässt sich die Sperre stufenweise in zeitlicher Abfolge verschärfen. Beispiel: Nach sechs Monaten wird ein Artikel in der ersten Stufe für die Produktion gesperrt; 30 Tage später in der zweiten Stufe zusätzlich für den Einkauf; nach einem weiteren Tag in der dritten Stufe vollständig.

#### Automatischer Hintergrundlauf (Aufgabenwarteschlange)

Die Requalifizierung wird nicht manuell ausgelöst, sondern durch einen Aufgabenwarteschlangenposten überwacht. **Wenn Sie den ersten Artikelstatus anlegen**, erzeugt das System automatisch einen wiederkehrenden Aufgabenwarteschlangenposten mit der Beschreibung **Artikelstatus aktualisieren** (Codeunit *MuM IS Item Status Management*). Er startet standardmäßig täglich (Intervall 1440 Minuten, erste Ausführung um 23:00 Uhr). Direkt nach dem Anlegen fragt das System, ob die zugehörige Aufgabenwarteschlangenposten-Karte geöffnet werden soll, damit Sie den Zeitplan bei Bedarf anpassen können.

Bei jedem Lauf prüft der Hintergrundprozess alle Artikel mit gesetztem Status: Ist die aus **Artikelstatus gesetzt am** und dem **Zeitraum** der Requalifizierung berechnete Frist überschritten, wird der Artikel auf den **zu setzenden Artikelstatus** umgesetzt und das Feld **Artikelstatus gesetzt am** auf das aktuelle Arbeitsdatum aktualisiert. Jede automatische Umsetzung erzeugt ebenfalls einen Eintrag in den **Artikelstatusposten**.

## Stammdaten: Artikel mit Artikelstatus

Die App erweitert die Standard-Stammdaten des Artikels (**Artikelkarte** und die Artikelübersicht) um zwei Felder, mit denen der aktuell zugewiesene Artikelstatus sichtbar wird. Diese Felder werden nicht direkt getippt, sondern durch die Aktion **Artikelstatus setzen** bzw. durch den Requalifizierungslauf gefüllt.

**Prozess:** Der Stammdatenverantwortliche pflegt die Zuordnung je Artikel. Die beiden Felder sind schreibgeschützt und dienen der Anzeige; ihre Werte steuern anschließend im gesamten Tagesgeschäft, welche Vorgänge das System für diesen Artikel zulässt (siehe Kapitel *Tägliche Arbeit* und *Wirkung im Tagesgeschäft*).

| Feld | Erläuterung |
|------|-------------|
| **Artikelstatuscode** | Zeigt den aktuell zugewiesenen Artikelstatus des Artikels an (schreibgeschützt). Wenn gefüllt, greifen die im zugehörigen Artikelstatus gesetzten Sperren für diesen Artikel; ist das Feld leer, gelten keine Artikelstatus-Sperren. Gesetzt wird der Wert über die Aktion **Artikelstatus setzen** oder durch die Requalifizierung. |
| **Artikelstatus gesetzt am** | Zeigt das Datum, seit dem der aktuelle Status gilt (schreibgeschützt). Wenn gefüllt, dient dieser Wert als Startpunkt für die Fristberechnung der Requalifizierung; er wird beim Setzen des Status und bei jeder automatischen Umsetzung auf das Arbeitsdatum aktualisiert. |

Beide Felder erscheinen sowohl auf der **Artikelkarte** (im Inforegister zu den Artikeldaten) als auch als zusätzliche Spalten in der Artikelübersicht, sodass Sie den Status eines Artikels bereits in der Liste erkennen, ohne die Karte zu öffnen.

## Tägliche Arbeit an der Artikelkarte

Die **Artikelkarte** ist der zentrale Einstieg für die operative Arbeit mit dem Artikelstatus. Die App fügt dort zwei Aktionen hinzu: **Artikelstatus setzen** und **Artikelstatushistorie**.

**Einstieg:** Öffnen Sie die Artikelübersicht oder die **Artikelkarte** des Artikels (Standardnavigation über die Artikelstammdaten). Die beiden Aktionen finden Sie im Aktionsmenü der Karte.

### Artikelstatus setzen

Über die Aktion **Artikelstatus setzen** weisen Sie dem Artikel einen zuvor definierten Artikelstatus zu. Die Zuweisung lässt sich beliebig oft wiederholen und ändern.

Ablauf:

1. Öffnen Sie die **Artikelkarte** des Artikels.
2. Wählen Sie die Aktion **Artikelstatus setzen**. Es öffnet sich die Auswahl der vorhandenen Artikelstatus.
3. Wählen Sie den gewünschten Status und bestätigen Sie mit **OK**.
4. Weicht der neue Status vom bisherigen ab, erscheint eine Sicherheitsabfrage: *„Der aktuelle Artikelstatus ist … Der ausgewählte ist … Wollen Sie wirklich den ausgewählten Artikelstatus … verwenden?“* Bestätigen Sie, um die Änderung zu übernehmen, oder brechen Sie ab.
5. Der Artikel erhält den neuen Status; die Felder **Artikelstatuscode** und **Artikelstatus gesetzt am** werden aktualisiert. Das Datum wird dabei auf das aktuelle Arbeitsdatum gesetzt.

Sämtliche im gewählten Artikelstatus hinterlegten Sperren wirken **sofort** für diesen Artikel. Ist für den gesetzten Status eine Requalifizierung eingerichtet, bildet **Artikelstatus gesetzt am** zusammen mit dem **Zeitraum** die Grundlage für die spätere automatische Umsetzung.

### Artikelstatushistorie

Über die Aktion **Artikelstatushistorie** öffnen Sie die **Artikelstatusposten** — die lückenlose Protokollierung aller jemals für den Artikel gesetzten Status. So verfolgen Sie nach, wann welcher Status durch wen gesetzt wurde. Ein Posten entsteht bei jeder Änderung des Artikelstatuscodes, sowohl bei manueller Zuweisung als auch bei automatischer Requalifizierung; eine Umsetzung auf denselben Status erzeugt keinen Eintrag.

Die Seite **Artikelstatusposten** ist rein anzeigend (kein Anlegen, Ändern oder Löschen möglich):

| Feld | Erläuterung |
|------|-------------|
| **Lfd. Nr.** | Laufende Zählnummer des Postens (fortlaufend vergeben). |
| **Artikelnr.** | Die Artikelnummer, für die der Status geändert wurde. |
| **Alter Artikelstatuscode** | Der Status, den der Artikel vor der Änderung hatte. Bei der ersten Zuweisung ist dieses Feld leer. |
| **Neuer Artikelstatuscode** | Der Status, den der Artikel mit der Änderung erhalten hat. |
| **Gesetzt von** | Benutzername des Anwenders, der die Änderung ausgelöst hat. Bei automatischer Requalifizierung entspricht dies dem ausführenden Kontext des Hintergrundlaufs. |
| **Gesetzt am** | Datum und Uhrzeit der Statusänderung. |

Dieselbe Historie ist auch außerhalb der Artikelkarte über die Suche (**Suchen**, Eingabe `Artikelstatusposten`) erreichbar.

## Wirkung im Tagesgeschäft (Sperrprüfungen)

Die eigentliche Sperrwirkung erleben die operativen Anwender nicht auf den Einrichtungsseiten, sondern beim Erfassen ihrer Belege und Buchblätter. Die App prüft den Artikelstatus automatisch an folgenden Stellen; ist die betreffende Sperre gesetzt, bricht der Vorgang mit der Meldung *„Der Artikel … ist von dem Artikelstatus … gesperrt.“* ab:

| Bereich | Auslösende Stelle |
|---------|-------------------|
| **Verkauf** | beim Ändern von **Nr.** oder **Menge** in der Verkaufszeile und beim Erzeugen des Auftrags aus dem Angebot |
| **Einkauf** | beim Ändern der **Nr.** in der Einkaufszeile und beim Erzeugen der Bestellung aus der Anfrage |
| **Lager** | beim Einfügen von Wareneingangs-, Warenausgangs- und Lageraktivitätszeilen |
| **Artikelbuchblatt** | beim Einfügen der Buchblattzeile und beim Ändern der Artikelnummer |
| **Umlagerung** | beim Ändern der Artikelnummer in der Umlagerungszeile |
| **Produktion** | beim Ändern der Artikelnummer in Fertigungsauftragszeile, FA-Komponente und Fertigungsstücklistenzeile |
| **Service** | beim Ändern der Artikelnummer in Servicezeile, Serviceartikel, Serviceartikelzeile und Servicevertragszeile |

Die Prüfung erfolgt nur, wenn der Artikel überhaupt einen **Artikelstatuscode** trägt und die dem Vorgang entsprechende Sperre im Status aktiv ist. Trägt der Artikel keinen Status oder ist die passende Sperre nicht gesetzt, läuft der Vorgang unverändert weiter.

Sonderfall Auslaufartikel: Ist im Status **Verkauf bis verfügbarer Bestand erlauben** aktiv, ersetzt eine Verfügbarkeitsprüfung die harte Sperre. Ist noch Bestand vorhanden, bleibt der Verkauf erlaubt; andernfalls erscheint der Hinweis, dass der Artikel ein Auslaufteil ist und nur der verfügbare Bestand verkauft werden kann.

## Berechtigungen

Die App liefert die Berechtigungssammlung **All permissions** (Objektname *MuM IS All*) mit. Sie bestimmt die Berechtigungen für sämtliche Tabellen, Seiten und Codeunits des Artikelstatus (Lesen, Einfügen, Ändern, Löschen auf den Datentabellen) und legt fest, welche Aktionen Anwender im Modul ausführen können. Weisen Sie diese Sammlung den Benutzern oder Benutzergruppen zu, die Artikelstatus einrichten und zuweisen sollen. Die Zuweisung erfolgt über die Standard-Berechtigungsverwaltung von Business Central.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Artikelstatus im realen Arbeitsablauf. Alle Schritte und Meldungen sind durch den Programmcode dieser App belegt.

### Auslaufartikel – Restbestand noch verkaufen, aber nicht mehr beschaffen

**Auslöser:** Der Vertrieb meldet, dass ein Artikel künftig durch ein Nachfolgeprodukt ersetzt wird. Der vorhandene Lagerbestand soll noch abverkauft, aber nichts mehr nachbestellt oder produziert werden.

**Einstieg in BC:** Der Stammdatenverantwortliche legt in der **Artikelstatusliste** eine Regel „Auslauf“ an. Auf der **Artikelstatus**-Karte aktiviert er im Register **Einkauf sperren** alle Optionen sowie im Register **Produktion sperren** die Fertigungssperren; im Register **Verkauf sperren** setzt er ausschließlich **Verkauf bis verfügbarer Bestand erlauben**.

**Kernablauf:**
1. Über die **Artikelkarte** des betroffenen Artikels wählt er **Artikelstatus setzen** und ordnet den Status „Auslauf“ zu; die Sicherheitsabfrage bestätigt er.
2. Ab sofort meldet das System beim Erfassen einer Einkaufsbestellung oder eines Fertigungsauftrags mit diesem Artikel, dass der Artikel gesperrt ist.
3. Erfasst der Vertrieb eine Verkaufszeile, prüft das System die Verfügbarkeit: Solange Bestand vorhanden ist, bleibt der Verkauf möglich; ist der Bestand aufgebraucht, erscheint der Hinweis auf das Auslaufteil.

**Abschluss:** Jede Statusänderung ist in der **Artikelstatushistorie** des Artikels nachvollziehbar.

### Qualitätssperre mit automatischer Verschärfung

**Auslöser:** Die Qualitätssicherung stellt bei einem Zukaufteil einen Mangel fest. Der Artikel soll sofort für die Produktion gesperrt und – falls der Mangel nicht innerhalb einer Frist behoben ist – anschließend vollständig gesperrt werden.

**Einstieg in BC:** Der Administrator legt zwei Artikelstatus an: „QS-Prod-Sperre“ (nur Produktion gesperrt) und „QS-Vollsperre“ (alle Bereiche gesperrt). In den **Artikelstatus-Requalifizierungen** erfasst er eine Regel mit **Zeitraum** (z. B. `14T`) und **zu setzender Artikelstatus** = „QS-Vollsperre“ und hinterlegt deren **Code** als **Requalifizierungscode** im Status „QS-Prod-Sperre“.

**Kernablauf:**
1. Über die **Artikelkarte** setzt die QS den Status „QS-Prod-Sperre“; **Artikelstatus gesetzt am** wird auf das Arbeitsdatum gesetzt.
2. Ab sofort blockiert das System den Artikel in Fertigungsaufträgen.
3. Der automatisch angelegte Aufgabenwarteschlangenposten **Artikelstatus aktualisieren** prüft täglich die Frist. Ist der aus **Artikelstatus gesetzt am** plus **Zeitraum** berechnete Termin überschritten, setzt er den Artikel automatisch auf „QS-Vollsperre“.

**Abschluss:** Die automatische Umsetzung erzeugt einen weiteren **Artikelstatusposten**, sodass die Eskalation lückenlos dokumentiert ist.

### Lager- und Umlagerungssperre für einen gesperrten Artikel

**Auslöser:** Ein Artikel darf ein bestimmtes Lager weder verlassen noch intern umgelagert werden, bis eine Klärung erfolgt ist.

**Einstieg in BC:** Der Administrator aktiviert auf der **Artikelstatus**-Karte im Register **Lager sperren** unter anderem **Warenausgang sperren**, **Kommissionierung sperren**, **Umlagerungsauftrag sperren** und **Umlagerungsbuchblatt sperren** und weist den Status dem Artikel zu.

**Kernablauf:**
1. Beim Erfassen einer Umlagerungsauftragszeile mit diesem Artikel bricht das System mit der Sperrmeldung ab.
2. Ebenso werden Warenausgangs- und Kommissionierzeilen beim Einfügen abgewiesen.

**Abschluss:** Nach Klärung entfernt der Administrator die Sperren über **Alles deaktivieren** im Register **Lager** oder setzt den Artikel über **Artikelstatus setzen** auf einen freigebenden Status zurück.

## FAQ und Troubleshooting

### Warum kann ich einen Artikel nicht mehr in eine Bestellung aufnehmen?
Der Artikel trägt einen **Artikelstatuscode**, in dem **Bestellung sperren** aktiv ist. Prüfen Sie über die **Artikelkarte** (Feld **Artikelstatuscode**) den zugewiesenen Status und auf der zugehörigen **Artikelstatus**-Karte das Register **Einkauf sperren**.

### Was bedeutet die Meldung „Der Artikel … ist von dem Artikelstatus … gesperrt.“?
Der Vorgang, den Sie gerade erfassen (z. B. eine Auftrags- oder Buchblattzeile), ist im zugewiesenen Artikelstatus des Artikels gesperrt. Die Meldung nennt Artikel, Beschreibung und Code des Status, damit Sie die verantwortliche Regel finden.

### Warum lässt das System den Verkauf zu, obwohl der Artikel gesperrt sein soll?
Im Status ist vermutlich **Verkauf bis verfügbarer Bestand erlauben** aktiv. Dann ersetzt eine Verfügbarkeitsprüfung die harte Sperre: Solange Bestand vorhanden ist, bleibt der Verkauf möglich.

### Was passiert, wenn kein Bestand mehr verfügbar ist und „Verkauf bis verfügbarer Bestand erlauben“ gesetzt ist?
Die Verkaufszeile wird mit dem Hinweis abgewiesen, dass der Artikel ein Auslaufteil ist und nur der noch verfügbare Bestand verkauft werden kann.

### Warum ändert sich der Artikelstatus eines Artikels von selbst?
Für den Status ist eine **Requalifizierung** hinterlegt. Der tägliche Aufgabenwarteschlangenposten **Artikelstatus aktualisieren** setzt den Artikel nach Ablauf des im **Zeitraum** definierten Zeitraums automatisch auf den **zu setzenden Artikelstatus**.

### Warum wurde nach dem ersten Artikelstatus eine Aufgabenwarteschlange angelegt?
Das Anlegen des ersten Artikelstatus erzeugt automatisch den wiederkehrenden Aufgabenwarteschlangenposten **Artikelstatus aktualisieren**, der die Requalifizierungen überwacht. Standardmäßig läuft er täglich um 23:00 Uhr; den Zeitplan können Sie auf der Aufgabenwarteschlangenposten-Karte anpassen.

### Warum kann ich einen Artikelstatus nicht löschen?
Dem Artikelstatus sind noch Artikel zugewiesen. Das System weist das Löschen mit dem Hinweis ab, dass zunächst der Artikelstatus aus den betroffenen Artikeln entfernt werden muss.

### Warum kann ich eine Requalifizierung nicht löschen?
Der Requalifizierungscode ist noch in mindestens einem Artikelstatus hinterlegt. Entfernen Sie den **Requalifizierungscode** zuerst aus dem betreffenden Artikelstatus, dann lässt sich die Requalifizierung löschen.

### Warum verlangt die Requalifizierung einen Zeitraum, sobald ich einen zu setzenden Artikelstatus eintrage?
Ohne **Zeitraum** kann der Ablauftermin nicht berechnet werden. Sobald ein **zu setzender Artikelstatus** hinterlegt ist, ist das Feld **Zeitraum** daher Pflicht; andernfalls weist das System das Speichern ab.

### Wie sehe ich, wer den Artikelstatus wann geändert hat?
Öffnen Sie über die **Artikelkarte** die Aktion **Artikelstatushistorie** oder rufen Sie die **Artikelstatusposten** über die Suche auf. Dort sind **Alter Artikelstatuscode**, **Neuer Artikelstatuscode**, **Gesetzt von** und **Gesetzt am** je Änderung protokolliert.
