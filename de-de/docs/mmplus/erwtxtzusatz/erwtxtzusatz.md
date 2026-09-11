---
title: Anwenderhandbuch m+m Ext. Text Module with Ext. Production Information
---

# Anwenderhandbuch m+m Ext. Text Module with Ext. Production Information

## Einleitung

Die App **m+m Ext. Text Module with Ext. Production Information** ist eine Verbindungs-App: Sie koppelt die materialartbezogene Textzuweisung des **Erweiterten Textmoduls** an die **Arbeitsgänge (Vorgänge) von Fertigungsaufträgen**. Das Ziel ist, dass ein **Erweiterter Text**, der über eine **Materialart** zugewiesen wurde, nicht nur an Verkaufs- und Fertigungsauftragszeilen erscheint, sondern zusätzlich an den **Arbeitsgangzeilen des Fertigungsauftrags** und von dort auf Belege, Factboxen und E-Mails gedruckt bzw. übernommen wird.

Die App bringt selbst **keine eigenen Seiten, Listen oder Aktionen** mit. Sie ergänzt ausschließlich die Verarbeitungslogik im Hintergrund. Alle Bildschirmmasken, in denen der Anwender arbeitet, stammen aus den vorausgesetzten m+m-Apps:

- **m+m Ext. Text Module** — Textvorlagen, Zuweisung (Subtyp), Belegtexte, Arbeitsgangtexte, Druck- und Mailsteuerung.
- **m+m Material Properties** — Materialarten und deren Zuordnung zum Artikel.
- **m+m Ext. Text Module with Material Properties** — verbindet Materialart und Erweiterten Text (Subtyp **Materialart** / **Alle Materialarten**).
- **m+m Ext. Production Information** — erweiterte Fertigungsinformationen an Vorgängen.

Ohne diese Basis-Apps ist die Funktion nicht nutzbar; sie sind als Abhängigkeit installiert.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender in der Fertigung und im Verkauf**, die Fertigungsaufträge und deren Arbeitsgänge bearbeiten sowie Belege und E-Mails erzeugen und dort den erweiterten Text sehen und prüfen. Sekundär angesprochen sind **Administratoren und Stammdatenverantwortliche**, die die Materialarten pflegen, die Erweiterten Texteinstellungen konfigurieren und die Textzuweisung über die Materialart einrichten.

**Kurzer Prozessüberblick.** Der Administrator pflegt die **Materialarten** und ordnet sie dem **Artikel** zu. In den **Erweiterten Texteinstellungen** legt er fest, welche Felder der Materialeigenschaft in Formeln verwendet werden. Anschließend erstellt er eine **Textvorlage** und weist sie über den **Subtyp Materialart** bzw. **Alle Materialarten** zu. Sobald ein Fertigungsauftrag Arbeitsgänge für einen Artikel dieser Materialart enthält, verknüpft diese App den passenden **Erweiterten Text** mit der jeweiligen **Arbeitsgangzeile** und stellt ihn für **Bericht**, **Factbox** und **Mail** bereit.

**Typischer Anwenderweg.** Materialart pflegen (**Materialarten** → **Materialartenkarte**) → Materialart am **Artikel** hinterlegen → Textvorlage über **Subtyp = Materialart / Alle Materialarten** zuweisen → Fertigungsauftrag und Arbeitsgang öffnen → **Erweiterter Text** am Vorgang prüfen → Beleg drucken oder als Mail versenden.

## Schnellstart für Anwender

Der Schnellstart nennt den kürzesten Weg zum Ergebnis „materialartbezogener Erweiterter Text an einer Arbeitsgangzeile des Fertigungsauftrags". Die Reihenfolge folgt der Abhängigkeit im Code: zuerst Einrichtung und Stammdaten, dann die tägliche Arbeit am Fertigungsauftrag.

1. **Materialart anlegen.** Öffnen Sie **Materialarten** und legen Sie über **+ Neu** eine Materialart an; erfassen Sie in der **Materialartenkarte** die Eigenschaften und heben Sie den Schalter **Gesperrt** auf, damit die Materialart in Zeilen verwendbar ist.
2. **Materialart am Artikel hinterlegen.** Weisen Sie dem betreffenden **Artikel** die Materialart zu (über die Materialliste des Artikels der App **m+m Material Properties**).
3. **Erweiterte Texteinstellungen prüfen.** Öffnen Sie **Erweiterte Texteinstellungen** und stellen Sie im Register **Materialtext** über die Aktion **Materialeigenschaftseinrichtung** ein, welche Felder der Materialeigenschaft im Erweiterten Text verwendet werden.
4. **Textvorlage über die Materialart zuweisen.** Legen Sie eine **Textvorlage** an, erfassen Sie den Text (mit optionaler Formel) und weisen Sie sie über den **Subtyp Materialart** (für eine bestimmte Materialart) oder **Alle Materialarten** (für jede Materialart) mit **Prozessobjekttyp = Seite** dem gewünschten Fertigungsbeleg zu.
5. **Fertigungsauftrag öffnen.** Öffnen Sie den Fertigungsauftrag mit Arbeitsgängen für einen Artikel der zugewiesenen Materialart.
6. **Erweiterten Text am Vorgang prüfen.** Öffnen Sie über die Aktion **Erweiterter Text** den Text zur betreffenden **Arbeitsgangzeile** (**Vorgangsnr.**) und kontrollieren Sie Inhalt und Anzeige für **Bericht**, **Factbox** und **Mail**.
7. **Beleg ausgeben.** Drucken Sie den Fertigungsbeleg bzw. versenden Sie ihn als E-Mail; der zugewiesene Text erscheint an der jeweiligen Arbeitsgangzeile.

> Diese App liefert keine eigene Seite. Alle genannten Masken gehören zu den verbundenen m+m-Apps (siehe **Einrichtung** und **Stammdaten**).

## Einrichtung

Die App selbst hat **keine Einrichtungsseite**. Damit die materialartbezogene Textzuweisung an Arbeitsgängen wirkt, müssen jedoch die Einrichtungen der verbundenen Module vorhanden sein. Dieser Abschnitt beschreibt den Aufbau in Abhängigkeitsreihenfolge. Alle Seiten stammen aus den Basis-Apps; die Bezeichnungen sind aus deren Übersetzungen übernommen.

### Erweiterte Texteinstellungen einrichten

**Wer und wann.** Der Administrator richtet die **Erweiterten Texteinstellungen** einmalig vor der ersten Nutzung ein. Diese Einstellungen steuern, wie Formelausdrücke im Erweiterten Text erkannt werden und welche Felder der Materialeigenschaft als Platzhalter eingesetzt werden können. Der Anwender nutzt das Ergebnis später beim Erfassen von Textvorlagen (siehe **Textvorlage über die Materialart zuweisen**).

**Einstieg:** Öffnen Sie die Seite **Erweiterte Texteinstellungen** (Basis-App m+m Ext. Text Module) und wechseln Sie in das Register **Materialtext**.

Felder im Register **Materialtext**:

| Einrichtung | Erläuterung |
|-------------|-------------|
| Formel Start/Ende | Wenn Sie hier ein Zeichen (Standard `^`) festlegen, erkennt der Erweiterte Text ab diesem Zeichen den Beginn und das Ende eines Formelausdrucks; dadurch können Sie in Textvorlagen bedingte Materialtexte formulieren, die beim Zusammensetzen des Belegtextes ausgewertet werden. |
| Teilformel Beginn | Wenn Sie dieses Zeichen (Standard `{`) setzen, markiert es den Anfang des Textblocks, der bei erfüllter Bedingung ausgegeben wird; ohne das Zeichen wird der bedingte Textblock nicht abgegrenzt. |
| Teilformel Ende | Wenn Sie dieses Zeichen (Standard `}`) setzen, markiert es das Ende des bedingten Textblocks; damit weiß die Verarbeitung, bis wohin der Text bei erfüllter Bedingung reicht. |
| Ext.Text automatisch aktualisieren | Wenn aktiviert, wird der Erweiterte Text automatisch neu zusammengesetzt, sobald sich der Wert der Materialeigenschaft ändert; ohne den Schalter bleibt ein bereits erzeugter Text unverändert, bis er manuell neu aufgebaut wird. |

**Prozessschritt.** Starten Sie in den **Erweiterten Texteinstellungen** die Aktion **Materialeigenschaftseinrichtung**. Dort legen Sie fest, welche Feldwerte der Materialeigenschaft im Erweiterten Text verwendet werden.

Felder in der **Materialeigenschaftseinrichtung**:

| Einrichtung | Erläuterung |
|-------------|-------------|
| Tabellen-ID | Wenn Sie hier die Tabelle der Materialeigenschaft angeben, wird festgelegt, aus welcher Tabelle die Feldwerte für den Erweiterten Text gelesen werden; erst danach stehen deren Felder für Platzhalter zur Verfügung. |
| Feld Nr. | Wenn Sie eine Feldnummer aus der angegebenen Tabellen-ID auswählen, wird genau dieser Feldwert als möglicher Platzhalter im Erweiterten Text verfügbar. |
| Feld Name | Zeigt den Namen zur ausgewählten Feld Nr.; er dient der eindeutigen Zuordnung des Platzhalters in der Textvorlage. |
| Start Merkmal | Wenn Sie dieses Anfangszeichen (Länge 1) setzen, erkennt die Verarbeitung ab diesem Zeichen den Beginn des einzusetzenden Feldwerts im Text. |
| End Merkmal | Wenn Sie dieses Endzeichen (Länge 1) setzen, erkennt die Verarbeitung das Ende des einzusetzenden Feldwerts; erst mit Start- und End-Merkmal wird der Platzhalter korrekt durch den Materialeigenschaftswert ersetzt. |

**Abschluss / Bezug zur täglichen Arbeit.** Nach dieser Einrichtung können Textvorlagen Formeln und Materialeigenschaftswerte enthalten, die beim Zusammensetzen des Belegtextes am Fertigungsauftrag und an dessen Arbeitsgängen ausgewertet werden (siehe **Tägliche Arbeit am Fertigungsauftrag**).

### Materialartbezogenen Arbeitsgangtext einrichten

Dies ist die zentrale Einrichtung, die genau diese Verbindungs-App wirksam macht. Sie verbindet drei Ebenen: **Materialart (Stammdaten)** → **Textvorlage mit Subtyp Materialart / Alle Materialarten** → **Wirkung an der Arbeitsgangzeile des Fertigungsauftrags**.

**Wer und wann.** Der Administrator oder Key-User richtet die Zuweisung einmalig ein, bevor Fertigungsaufträge mit materialartbezogenen Texten gedruckt werden. Der operative Anwender konsumiert das Ergebnis in der **Tagesarbeit am Fertigungsauftrag**.

**Numerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Materialart als Stammdatum anlegen.** Öffnen Sie **Materialarten** und legen Sie die benötigte Materialart an. Wenn die Materialart nicht **Gesperrt** ist, kann sie in Belegzeilen und in der Textzuweisung verwendet werden; solange sie gesperrt ist, greift die Zuweisung nicht (siehe **Stammdaten – Materialarten**).
2. **Materialart dem Artikel zuordnen.** Hinterlegen Sie die Materialart am **Artikel**. Wenn ein Artikel eine Materialart trägt, kann die Verarbeitung beim Fertigungsauftrag über die Fertigungsauftragszeile die passende Materialart ermitteln und den zugehörigen Text an den Arbeitsgang koppeln.
3. **Textvorlage anlegen und zuweisen.** Erstellen Sie eine **Textvorlage** mit dem gewünschten Text bzw. Formelausdruck. Setzen Sie den **Subtyp** auf **Materialart**, wenn der Text nur für eine bestimmte Materialart gelten soll, oder auf **Alle Materialarten**, wenn er für jede Materialart gelten soll. Wählen Sie als **Prozessobjekttyp** den Wert **Seite** und als **Prozess-Objekt-ID** die Fertigungsbeleg-Seite, für die der Text gelten soll. Damit wird gesteuert, auf welchem Fertigungsbeleg der Text am Arbeitsgang erscheint.
4. **Feldwerte der Materialeigenschaft prüfen.** Stellen Sie sicher, dass die in der Textvorlage verwendeten Platzhalter in der **Materialeigenschaftseinrichtung** (siehe oben) hinterlegt sind; ohne diese Zuordnung bleiben Platzhalter im Text unaufgelöst.

**Operativer Abschluss.** Sobald ein Fertigungsauftrag Arbeitsgänge für einen Artikel der eingerichteten Materialart enthält, verknüpft die App den passenden Erweiterten Text automatisch mit der **Arbeitsgangzeile** (**Vorgangsnr.**). Der Anwender kontrolliert und druckt ihn in der **Tagesarbeit am Fertigungsauftrag**.

**Subtyp – Bedeutung der relevanten Werte** (Enum **Subtyp**, für diese App maßgeblich):

- **Materialart:** Der Text greift nur, wenn die Materialart des Artikels der Arbeitsgangzeile mit der in der Zuweisung hinterlegten Materialart übereinstimmt. So steuern Sie materialartspezifische Hinweise (z. B. Bearbeitungs- oder Sicherheitshinweise je Werkstoff).
- **Alle Materialarten:** Der Text greift für jede Materialart, sofern am Artikel der Arbeitsgangzeile überhaupt eine Materialeigenschaft vorhanden ist. So verteilen Sie einen allgemeingültigen Materialtext über alle Werkstoffe.

> Weitere Subtyp-Werte des Erweiterten Textmoduls (z. B. **Arbeitsplatzgruppe**) gehören zum Basismodul und werden durch diese Verbindungs-App nicht verändert; für die materialartbezogene Arbeitsgang-Verarbeitung sind ausschließlich **Materialart** und **Alle Materialarten** relevant.

## Stammdaten

### Materialarten

**Wer und wann.** Der Stammdatenverantwortliche pflegt die **Materialarten**, bevor materialartbezogene Texte zugewiesen und an Fertigungsaufträgen ausgegeben werden. Die gepflegten Werte erscheinen später als Auswahl in der Textzuweisung (**Subtyp Materialart**) und bestimmen, welcher Text an welche Arbeitsgangzeile gekoppelt wird.

**Einstieg:** Öffnen Sie die Liste **Materialarten**; über **+ Neu** legen Sie eine Materialart an, über **Verwalten → Bearbeiten** öffnen Sie die **Materialartenkarte**.

In der Übersicht **Materialarten** sehen Sie alle verfügbaren Materialarten sowie die Anzahl der Artikel, die eine Materialart verwenden. Über das Flowfield der Artikelanzahl öffnen Sie eine gefilterte **Artikelliste** zur jeweiligen Materialart.

Zentrale Felder der Materialart:

| Feld | Erläuterung |
|------|-------------|
| Materialart (Code/Bezeichnung) | Wenn Sie hier den Code und die Bezeichnung erfassen, steht die Materialart als Stammdatum zur Zuordnung an Artikeln und zur Textzuweisung bereit; ohne Code kann die Materialart nicht referenziert werden. |
| Gesperrt | Wenn aktiviert, ist die Materialart gesperrt und kann nicht in Belegzeilen verwendet und nicht zugewiesen werden; heben Sie den Schalter auf, damit die Materialart am Artikel und in der Textzuweisung greift. |

**Bezug zur täglichen Arbeit.** Nur eine entsperrte, dem Artikel zugeordnete Materialart führt dazu, dass diese App an den Arbeitsgangzeilen des Fertigungsauftrags den passenden Erweiterten Text ermittelt (siehe **Tägliche Arbeit am Fertigungsauftrag**).

> Die vollständige Feld- und Aktionsvielfalt der **Materialartenkarte** (z. B. Vorlagen für Artikelbeschreibungen, Kopiervorlagen) gehört zur App **m+m Material Properties** und ist dort dokumentiert. Für die vorliegende Verbindungs-App sind die Existenz einer entsperrten Materialart und deren Zuordnung zum Artikel die einzige stammdatenseitige Voraussetzung.

## Tägliche Arbeit am Fertigungsauftrag

Dieser Abschnitt beschreibt, was der operative Anwender im Fertigungsauftrag sieht und tut, sobald die Einrichtung steht. Die Verbindungs-App arbeitet hier im Hintergrund: Beim Zusammensetzen des Belegtextes für eine **Arbeitsgangzeile** eines Fertigungsauftrags prüft sie die vorhandenen Textzuweisungen mit **Subtyp Materialart** oder **Alle Materialarten** und markiert die passenden Textvorlagen.

**Voraussetzungen (Verweis auf Einrichtung).** Die Wirkung setzt eine entsperrte, dem Artikel zugeordnete Materialart (siehe **Stammdaten – Materialarten**) sowie eine Textzuweisung mit **Subtyp Materialart / Alle Materialarten** und **Prozessobjekttyp = Seite** voraus (siehe **Materialartbezogenen Arbeitsgangtext einrichten**).

**Kernablauf:**

1. **Fertigungsauftrag öffnen.** Öffnen Sie den Fertigungsauftrag, dessen Arbeitsgänge Artikel mit einer eingerichteten Materialart betreffen.
2. **Arbeitsgangzeile wählen.** Wählen Sie die betreffende **Arbeitsgangzeile** (**Vorgangsnr.**). Die App ordnet die Textzuweisung anhand des Arbeitsgangs dem richtigen Vorgang zu (Ermittlung über die zum Vorgang gehörende Fertigungsauftragszeile und deren Materialart).
3. **Erweiterten Text öffnen.** Öffnen Sie über die Aktion **Erweiterter Text** den zusammengesetzten Text zur Arbeitsgangzeile. Der Text enthält die über die Materialart zugewiesenen Inhalte; enthaltene Platzhalter wurden anhand der Materialeigenschaftswerte des Artikels ersetzt.
4. **Anzeigearten prüfen.** Kontrollieren Sie den Text getrennt nach Verwendungszweck:
   - **Bericht:** Der Text wird auf dem Beleg gedruckt (mit optionalen Teilbereichen wie Kopf, Fuß, vor/nach Position).
   - **Factbox:** Der Text wird in der Infobox zur Zeile angezeigt.
   - **Mail:** Der Text wird in eine E-Mail übernommen.

**Reihenfolge- und Prioritätslogik.** Wurde der Text an der Arbeitsgangzeile bereits **manuell geändert**, hat dieser geänderte Text Vorrang und wird nicht durch die materialartbezogene Zuweisung überschrieben. Andernfalls setzt die App den Text aus den zutreffenden Vorlagen zusammen. So bleiben individuelle Anpassungen am einzelnen Fertigungsauftrag erhalten.

## Belege und E-Mail

Der über die Materialart zugewiesene Arbeitsgangtext ist nicht nur am Bildschirm sichtbar, sondern fließt in die **Belegausgabe** und den **Mailversand** des Erweiterten Textmoduls ein.

- **Bericht (Druck).** Beim Drucken des Fertigungsbelegs wird der zusammengesetzte Text der Arbeitsgangzeile ausgegeben. Über die Untertypen des Berichtstexts (Kopf, Fuß, vor Position, nach Position) steuern Sie, an welcher Stelle des Belegs der Text erscheint.
- **Factbox.** In der Infobox zur Arbeitsgangzeile wird der Text zur Sichtprüfung angezeigt, ohne dass gedruckt werden muss.
- **Mail.** Der Text wird in die E-Mail-Ausgabe übernommen, sodass materialartbezogene Hinweise auch bei elektronischem Versand mitgeführt werden.

Welche Belegart betroffen ist, ergibt sich aus der **Prozess-Objekt-ID** (der Fertigungsbeleg-Seite) der Textzuweisung. Damit steuern Sie gezielt, auf welchem Fertigungsbeleg der materialartbezogene Arbeitsgangtext erscheint.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen realistische Auslöser und den chronologischen Ablauf in Business Central. Jeder Schritt ist über die verbundenen Module abgesichert; die Verbindungs-App sorgt dafür, dass der materialartbezogene Text an den Arbeitsgängen des Fertigungsauftrags landet.

### Szenario 1: Werkstoffspezifischer Bearbeitungshinweis auf dem Fertigungsbeleg

1. **Auslöser.** Die Fertigung meldet, dass für einen bestimmten Werkstoff ein zusätzlicher Bearbeitungshinweis auf jeder Arbeitsgangzeile stehen soll.
2. **Einstieg in BC.** Der Administrator öffnet **Materialarten**, stellt sicher, dass die betreffende Materialart existiert und nicht **Gesperrt** ist, und prüft, dass die relevanten Artikel diese Materialart tragen.
3. **Kernablauf.** Er legt eine **Textvorlage** mit dem Hinweistext an und weist sie über den **Subtyp Materialart** (für genau diesen Werkstoff), **Prozessobjekttyp = Seite** und die passende **Prozess-Objekt-ID** der Fertigungsbeleg-Seite zu. Anschließend öffnet der Fertigungsanwender einen Fertigungsauftrag mit Arbeitsgängen für einen Artikel dieser Materialart, wählt die **Arbeitsgangzeile** (**Vorgangsnr.**) und prüft über **Erweiterter Text** die Anzeige für **Bericht**.
4. **Abschluss.** Der Fertigungsbeleg wird gedruckt; der werkstoffspezifische Hinweis erscheint an der jeweiligen Arbeitsgangzeile.

### Szenario 2: Allgemeiner Materialhinweis per E-Mail an die Fertigung

1. **Auslöser.** Ein allgemein gültiger Materialhinweis soll unabhängig vom konkreten Werkstoff bei jedem materialbezogenen Arbeitsgang mitversandt werden.
2. **Einstieg in BC.** Der Key-User öffnet die **Erweiterten Texteinstellungen**, kontrolliert im Register **Materialtext** die Formelzeichen und die **Materialeigenschaftseinrichtung**.
3. **Kernablauf.** Er erstellt eine **Textvorlage** mit dem allgemeinen Hinweis und weist sie über den **Subtyp Alle Materialarten** zu. Beim Aufbau des Belegtextes für einen Fertigungsauftrag markiert die Verbindungs-App diese Vorlage für jeden Arbeitsgang, dessen Artikel eine Materialeigenschaft besitzt. Der Anwender kontrolliert an der **Arbeitsgangzeile** über **Erweiterter Text** die Anzeige für **Mail**.
4. **Abschluss.** Der Fertigungsbeleg wird als E-Mail versendet; der allgemeine Materialhinweis ist am Arbeitsgang enthalten.

## FAQ und Troubleshooting

### 1. Warum bringt diese App keine eigene Seite mit?
Die App ist eine reine Verbindungs-App. Sie ergänzt im Hintergrund die Verarbeitung des Erweiterten Textmoduls, damit materialartbezogene Texte auch an den Arbeitsgangzeilen von Fertigungsaufträgen greifen. Sämtliche Bedienoberflächen stammen aus den verbundenen m+m-Apps.

### 2. Welche Apps müssen installiert sein, damit die Funktion arbeitet?
Vorausgesetzt sind **m+m Ext. Text Module**, **m+m Material Properties**, **m+m Ext. Text Module with Material Properties**, **m+m Ext. Production Information** sowie **m+m Cloud Base**. Ohne diese Basis stehen weder Materialarten noch Textzuweisung noch die Arbeitsgangtexte zur Verfügung.

### 3. Warum erscheint an der Arbeitsgangzeile kein materialartbezogener Text?
Prüfen Sie in dieser Reihenfolge: Ist die **Materialart** entsperrt und dem Artikel zugeordnet? Existiert eine Textzuweisung mit **Subtyp Materialart / Alle Materialarten**? Ist der **Prozessobjekttyp = Seite** und die **Prozess-Objekt-ID** die richtige Fertigungsbeleg-Seite? Fehlt eine dieser Voraussetzungen, findet die Verarbeitung keine passende Vorlage und beendet sich ohne Text.

### 4. Was ist der Unterschied zwischen den Subtypen Materialart und Alle Materialarten?
**Materialart** greift nur, wenn die Materialart des Artikels der Arbeitsgangzeile mit der in der Zuweisung hinterlegten Materialart übereinstimmt. **Alle Materialarten** greift für jede Materialart, sofern am Artikel überhaupt eine Materialeigenschaft vorhanden ist.

### 5. Warum wird mein manuell geänderter Arbeitsgangtext nicht durch die Zuweisung überschrieben?
Ein an der Arbeitsgangzeile bereits manuell geänderter Text hat Vorrang. Die Verarbeitung erkennt die manuelle Änderung und übernimmt den geänderten Text, statt ihn durch die materialartbezogene Vorlage zu ersetzen. So bleiben individuelle Anpassungen erhalten.

### 6. Wie ordnet die App den Text dem richtigen Arbeitsgang zu?
Die App ermittelt zur **Arbeitsgangzeile** (über **Vorgangsnr.** und Arbeitsplan) die zugehörige Fertigungsauftragszeile und deren Materialart und vergleicht sie mit der Textzuweisung. Nur bei Übereinstimmung wird die Vorlage markiert und der Text übernommen.

### 7. Warum bleiben Platzhalter im Text unaufgelöst?
Platzhalter werden nur ersetzt, wenn die verwendeten Felder in der **Materialeigenschaftseinrichtung** hinterlegt sind und die Formelzeichen in den **Erweiterten Texteinstellungen** korrekt gesetzt sind. Fehlt die Feldzuordnung oder das Start-/End-Merkmal, bleibt der Platzhalter stehen.

### 8. Auf welchen Belegen erscheint der materialartbezogene Arbeitsgangtext?
Auf der Fertigungsbeleg-Seite, die Sie über die **Prozess-Objekt-ID** der Textzuweisung festgelegt haben. Über die Anzeigearten **Bericht**, **Factbox** und **Mail** steuern Sie zusätzlich, wo der Text sichtbar wird.

### 9. Wirkt die App auch auf Verkaufs- und Fertigungsauftragszeilen?
Die materialartbezogene Zuweisung an **Verkaufszeilen** und **Fertigungsauftragszeilen** erledigt bereits das Modul **m+m Ext. Text Module with Material Properties**. Diese Verbindungs-App ergänzt gezielt die **Arbeitsgangzeilen (Vorgänge)** des Fertigungsauftrags.

### 10. Muss ich den Erweiterten Text nach einer Änderung der Materialeigenschaft neu aufbauen?
Nur, wenn der Schalter **Ext.Text automatisch aktualisieren** in den **Erweiterten Texteinstellungen** nicht aktiviert ist. Ist er aktiviert, wird der Text bei einer Wertänderung der Materialeigenschaft automatisch neu zusammengesetzt.
