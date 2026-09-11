---
title: Anwenderhandbuch m+m Ext. Text Module with Material Properties
---

# Anwenderhandbuch m+m Ext. Text Module with Material Properties

## Einleitung

Die App **m+m Ext. Text Module with Material Properties** verbindet zwei m+m-Anwendungen: das **Erweiterte Textmodul** (vorlagen- und platzhalterbasierte Erzeugung von Belegtexten) und die **Materialeigenschaften** (strukturierte Attribute und Werte zu Artikeln und Belegzeilen). Mit dieser Verbindung lassen sich Werte aus den Materialeigenschaften als **Platzhalter** und in **Formelausdrücken** direkt in den erweiterten Text einsetzen, der in Belegzeilen, FactBoxen, E-Mails und Berichten ausgegeben wird.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender**, die täglich mit Belegen arbeiten: Mitarbeitende in Verkauf und Einkauf, die in Angebots-, Auftrags-, Anfrage-, Bestell- und Rechnungszeilen mit erweitertem Text und Materialeigenschaften arbeiten, sowie Mitarbeitende in der Fertigung, die Arbeitsgangtexte an Fertigungsaufträgen nutzen. Sekundäre Zielgruppe sind **Administratoren und Key-User**, die die **Erweiterte Texteinstellungen** und die **Materialfeld Einrichtung** pflegen.

**Voraussetzungen.** Die App **m+m Ext. Text Module** und die App **m+m Material Properties** müssen installiert und eingerichtet sein. Materialarten und Eigenschaften werden in der Anwendung Materialeigenschaften gepflegt; die Vorlagen, Platzhalter und Zuordnungen werden im Erweiterten Textmodul gepflegt. Diese App ergänzt beide um die gemeinsame Auflösung von Materialwerten im Text.

**Kurzer Prozessüberblick.** Der Administrator legt in der **Materialfeld Einrichtung** fest, welche Felder der **Datensatzeigenschaft** über welche Start- und Endzeichen als Platzhalter im Text genutzt werden. In den **Erweiterte Texteinstellungen** bestimmt er die Zeichen für **Formel Start/Ende** und **Unterformel** sowie, ob bestehende Texte bei Wertänderungen automatisch neu zusammengesetzt werden. Im laufenden Betrieb pflegen die Anwender Materialeigenschaftswerte an Artikeln und Belegzeilen; der erweiterte Text wird beim Erzeugen, in der FactBox, beim E-Mail-Versand und im Bericht mit diesen Werten gefüllt, und bedingte Formelausdrücke werden ausgewertet.

> **Hinweis.** Diese App enthält keine eigenen Buchungs-, Lager- oder Umlagerungsvorgänge und keine eigene Historien- oder Archivseite. Sie verarbeitet ausschließlich Texte des Erweiterten Textmoduls anhand der Materialeigenschaften.

---

## Schnellstart für Anwender

Da kein Buchungslauf existiert, ist der schnellste Weg zum Ergebnis die **Einrichtungskette**, gefolgt von der täglichen Texterzeugung. Reihenfolge in Abhängigkeit der Voraussetzungen (zuerst Stammdaten, dann globale Einrichtung, dann Feldzuordnung, schließlich die Anwendung im Beleg):

1. **Materialarten und Eigenschaften bereitstellen.** Stellen Sie sicher, dass in der App Materialeigenschaften die benötigten **Materialarten** (Seite **Materialarten**) und Eigenschaften mit **Eigenschaftscode** angelegt sind und den Artikeln zugeordnet wurden.
2. **Erweiterte Texteinstellungen öffnen.** Öffnen Sie über **Suchen** die Seite **Erweiterte Texteinstellungen** und wechseln Sie in das Register **Materialtext**.
3. **Formelzeichen prüfen.** Kontrollieren Sie **Formel Start/Ende**, **Startzeichen Unterformel** und **Endzeichen Unterformel**. Bei der Installation werden die Standardwerte `^`, `{` und `}` gesetzt; passen Sie sie nur an, wenn diese Zeichen in Ihren Texten bereits verwendet werden.
4. **Automatische Aktualisierung festlegen.** Aktivieren Sie bei Bedarf **Autom. aktualisieren erw. Texte**, damit bestehende Texte bei Wertänderungen neu aus den Vorlagen zusammengesetzt werden.
5. **Materialfeld Einrichtung pflegen.** Wählen Sie auf der Seite **Erweiterte Texteinstellungen** die Aktion **Materialeigenschaftseinrichtung**. Legen Sie pro Zeile die **Tabellen-ID** (Datensatzeigenschaft), die **Feldnr.** sowie **Startzeichen** und **Endzeichen** fest, mit denen der Platzhalter im Text umschlossen wird.
6. **Vorlagen und Zuordnung vorbereiten.** Hinterlegen Sie in den Vorlagen des Erweiterten Textmoduls die Platzhalter und Formelausdrücke und ordnen Sie die Vorlagen auf dem **Arbeitsblatt erweiterte Textzuordnung** zu (für materialbezogene Zuordnungen über **Subtyp** = **Materialart** oder **Alle Materialarten**).
7. **Im Beleg anwenden.** Erfassen Sie eine Belegzeile mit Artikel, pflegen Sie die **Datensatzeigenschaft**-Werte und lassen Sie den erweiterten Text erzeugen; die Platzhalter werden durch die Werte ersetzt und Formelbedingungen ausgewertet.

> Die Einrichtungsschritte 2–6 werden im Kapitel **Einrichtung** vollständig erklärt; die Tagesarbeit in **Tägliche Arbeit: Materialtext in Belegen**.

---

## Einrichtung

Die Einrichtung ist der umfangreichste Teil dieser App. Sie besteht aus dem Register **Materialtext** auf der Seite **Erweiterte Texteinstellungen**, der Liste **Materialfeld Einrichtung** und der gemeinsamen Logik der Formelzeichen. Konfiguriert wird sie einmalig durch einen Administrator oder Key-User vor der ersten Nutzung; die Werte gelten mandantenweit.

### Erweiterte Texteinstellungen — Register Materialtext

**Prozess.** Diese Felder werden vom Administrator auf der mandantenweiten Seite **Erweiterte Texteinstellungen** gepflegt. Sie bestimmen, mit welchen Zeichen Formeln und Unterformeln im Text erkannt werden und ob Texte bei Materialänderungen automatisch neu erzeugt werden. Die Werte greifen anschließend überall dort, wo das Erweiterte Textmodul Material­platzhalter auflöst — siehe **Tägliche Arbeit: Materialtext in Belegen**.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Erweiterte Texteinstellungen** und wechseln Sie in das Register **Materialtext**.

| Einrichtung | Erläuterung |
|---|---|
| **Formel Start/Ende** | Wenn Sie hier ein Zeichen festlegen (Standard `^`), dann erkennt das Modul jeden Abschnitt, der von diesem Zeichen umschlossen ist, als **Bedingung** eines Formelausdrucks. Ist das Feld leer, wird keine Formelauswertung durchgeführt und nur einfache Platzhalter werden ersetzt. Das Feld ist auf ein Zeichen begrenzt. |
| **Startzeichen Unterformel** | Wenn Sie hier ein Zeichen festlegen (Standard `{`), dann beginnt damit der **bedingte Textblock**, der ausgegeben wird, sobald die zugehörige Bedingung wahr ist. Ohne dieses Zeichen kann das Modul den auszugebenden Block nicht abgrenzen und die Formel bleibt unaufgelöst. |
| **Endzeichen Unterformel** | Wenn Sie hier ein Zeichen festlegen (Standard `}`), dann endet damit der bedingte Textblock; das Modul nutzt es, um verschachtelte Blöcke korrekt zu zählen. Fehlt das Endzeichen, wird der Block nicht ersetzt. |
| **Autom. aktualisieren erw. Texte** | Wenn aktiviert, dann werden bei einer Änderung eines Materialeigenschaftswertes die bereits erzeugten erweiterten Texte der betroffenen Beleg­zeile automatisch neu aus den Vorlagen zusammengesetzt und aktualisiert. Existiert bereits ein passender Text, erscheint zuvor die Bestätigungsabfrage *„Es gibt bereits einen erweiterten Text … Möchten Sie aktualisieren?"*. Ist das Feld nicht aktiviert, bleibt bestehender Text unverändert, bis er manuell neu erzeugt wird. |
| **FA-Zeilen-Materialeigenschaften für Arbeitsgangstexte verwenden** | Wenn aktiviert, dann werden Platzhalter in den erweiterten Texten der **Arbeitsgänge** anhand der Materialeigenschaften der **FA-Zeile** aufgelöst (statt der erw. Fertigungseigenschaften der Arbeitsplatzgruppe). So erscheint im Arbeitsgangtext das Material des produzierten Artikels. Ist das Feld nicht aktiviert, gilt das ursprüngliche Verhalten und die Eigenschaften der Arbeitsplatzgruppe werden herangezogen. |

> **Aktion auf dieser Seite:** **Materialeigenschaftseinrichtung** — öffnet die Liste **Materialfeld Einrichtung** zur Pflege der Felder, die als Platzhalter im erweiterten Text genutzt werden (siehe nächste H3).

**Vollständige Seite Erweiterte Texteinstellungen (Basisfelder des Erweiterten Textmoduls).** Da BC dem Anwender eine einzige Seite anzeigt, sind hier auch die Basisfelder des Erweiterten Textmoduls dokumentiert. Sie steuern, wie Texte allgemein erzeugt und ausgegeben werden, und wirken damit auch auf die durch diese App eingesetzten Materialwerte.

| Einrichtung | Erläuterung |
|---|---|
| **Vorlagennummern** | Wenn Sie eine Nummernserie hinterlegen, dann werden neue Textvorlagen automatisch mit Nummern aus dieser Serie angelegt; ohne Serie vergeben Sie Vorlagennummern manuell. |
| **Sprachcode** | Wenn Sie einen Sprachcode hinterlegen, dann wird er als Standardsprache für die Texterzeugung verwendet, sofern der Beleg keine eigene Sprache vorgibt. |
| **Platzhalter Startzeichen** | Wenn Sie ein Zeichen festlegen, dann erkennt das Modul den Beginn eines allgemeinen Textplatzhalters daran; dieser Wert betrifft die Standardplatzhalter des Erweiterten Textmoduls. |
| **Platzhalter Endzeichen** | Wenn Sie ein Zeichen festlegen, dann erkennt das Modul daran das Ende eines allgemeinen Textplatzhalters. |
| **E-Mail Platzhalter** | Legt fest, ob und wann Platzhalter beim E-Mail-Versand ersetzt werden. **(leer):** keine besondere Ersetzung beim Senden. **Beim Senden:** Wenn gewählt, werden die Platzhalter erst beim Versand durch ihre Werte ersetzt. **Beim Senden ersetzen und speichern:** Wenn gewählt, werden die Platzhalter beim Versand ersetzt und der aufgelöste Text wird zusätzlich gespeichert. |
| **E-Mail-Text bevorzugen** | Bestimmt, welcher Text für die E-Mail herangezogen wird. **E-Mail-Text verwenden:** Wenn gewählt, wird der eigens für die E-Mail gepflegte Text genutzt. **Factbox-Text anstelle von E-Mail-Text verwenden:** Wenn gewählt, wird der FactBox-Text der Zeile anstelle des E-Mail-Textes versendet. |
| **Vorschautexte in Herkunftsbelegen** | Wenn aktiviert, dann werden die erweiterten Texte bereits im Herkunftsbeleg als Vorschau angezeigt, sodass der Anwender das Ergebnis vor dem Druck sieht. |
| **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** | Wenn aktiviert, dann werden FactBox-Texte ohne gesetzten Druck-Untertyp ebenfalls in den Bericht übernommen; ist es nicht gesetzt, bleiben diese Texte im Bericht aus. |
| **Text kopieren** | Wenn aktiviert, dann werden erweiterte Texte beim Kopieren von Belegen mit in den Zielbeleg übernommen. |
| **Ext.Text bei Buchungsroutinen automatisch zuweisen** | Wenn aktiviert, dann weist das Modul den erweiterten Text in den Buchungsroutinen des Belegs automatisch zu, sodass er auf dem gebuchten Beleg erscheint. |
| **Arbeitsgangtext an Bestellung übertragen** | Wenn aktiviert, dann wird der Text eines Arbeitsgangs bei der Beschaffung an die zugehörige Bestellung übertragen. |
| **FA-Texte beim Statuswechsel übernehmen** | Wenn aktiviert, dann werden die erweiterten Texte des Fertigungsauftrags beim Wechsel des Auftragsstatus mit übernommen, sodass sie auf der nächsten Statusstufe verfügbar bleiben. |
| **EK-Kopf-Texte im Hintergrund erstellen** | Wenn aktiviert, dann werden Kopf-Texte für Einkaufsbelege im Hintergrund erzeugt, was die Belegerfassung beschleunigt. |
| **Ek-Zeilen-Texte im Hintergrund erstellen** | Wenn aktiviert, dann werden Zeilen-Texte für Einkaufsbelege im Hintergrund erzeugt. |
| **VK-Kopf-Texte im Hintergrund erstellen** | Wenn aktiviert, dann werden Kopf-Texte für Verkaufsbelege im Hintergrund erzeugt. |
| **VK-Zeilen-Texte im Hintergrund erstellen** | Wenn aktiviert, dann werden Zeilen-Texte für Verkaufsbelege im Hintergrund erzeugt. |

> Die mandantenweite Seite besitzt einen verborgenen Primärschlüssel (Einzelsatz), der nicht erfasst wird.

### Materialfeld Einrichtung

**Prozess.** In dieser Liste legt der Administrator fest, **welche** Felder der **Datensatzeigenschaft** als Platzhalter im erweiterten Text auflösbar sind und mit **welchen Zeichen** ein Platzhalter im Text umschlossen wird. Erst diese Zuordnung macht aus einem Text wie `Werkstoff %BREITE%` einen Text, in dem `%BREITE%` durch den Eigenschaftswert ersetzt wird. Die Einrichtung erfolgt vor der ersten Nutzung; die Anwender verwenden die definierten Platzhalter später in den Vorlagen.

**Einstieg:** Öffnen Sie in den **Erweiterte Texteinstellungen** über die Aktion **Materialeigenschaftseinrichtung** die Liste **Materialfeld Einrichtung**.

| Einrichtung | Erläuterung |
|---|---|
| **Tabellen-ID** | Wenn Sie hier eine Tabelle wählen, dann liest das Modul den Platzhalterwert aus dieser Tabelle. Zulässig ist ausschließlich die Tabelle **Datensatzeigenschaft**; bei einer anderen Auswahl erscheint die Meldung *„Ausgewählte Tabellen-ID kann nicht verwendet werden."*. |
| **Tabellenname** | Zeigt den Namen der gewählten Tabelle an. Das Feld wird automatisch berechnet und ist nicht editierbar; es dient der Kontrolle der Auswahl. |
| **Feldnr.** | Wenn Sie eine Feldnummer wählen, dann darf der Wert dieses Feldes als Platzhalter im erweiterten Text verwendet werden. Auswählbar sind nur Felder der Typen Ganzzahl, BigInteger, Dezimal, Text, Code oder Option; andere Feldtypen lassen sich nicht zuordnen. |
| **Feldname** | Zeigt den Namen des gewählten Feldes an. Das Feld wird automatisch berechnet und ist nicht editierbar. |
| **Startzeichen** | Wenn Sie ein Zeichen festlegen, dann beginnt der Platzhalter im Text mit diesem Zeichen, unmittelbar vor dem **Eigenschaftscode**. Das Feld ist auf ein Zeichen begrenzt und darf nicht leer sein. |
| **Endzeichen** | Wenn Sie ein Zeichen festlegen, dann endet der Platzhalter im Text mit diesem Zeichen, unmittelbar nach dem **Eigenschaftscode**. Das Feld ist auf ein Zeichen begrenzt und darf nicht leer sein. |

> Ein Platzhalter setzt sich demnach zusammen aus **Startzeichen + Eigenschaftscode + Endzeichen** (z. B. `%BREITE%`, wenn Start- und Endzeichen `%` sind und der Eigenschaftscode `BREITE` lautet). Die Erkennung ist nicht groß-/kleinschreibungsabhängig.

### Materialeigenschaften im erweiterten Text einrichten

Dieser Abschnitt führt die mehrstufige Konfiguration zusammen, die nötig ist, damit Materialwerte im erweiterten Text erscheinen.

**Prozesseinführung.** Eingerichtet wird die Kette durch einen Administrator oder Key-User **vor der ersten Nutzung**. Sie verbindet die Stammdaten der Materialeigenschaften mit der globalen Texteinrichtung und der Feldzuordnung; angewendet werden die Einstellungen anschließend in der täglichen Belegarbeit (siehe **Tägliche Arbeit: Materialtext in Belegen**).

**Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Stammdaten der Materialeigenschaften bereitstellen.** Wenn in der App Materialeigenschaften eine **Materialart** und die zugehörigen Eigenschaften mit **Eigenschaftscode** angelegt und den Artikeln zugeordnet sind, dann stehen die Werte als **Datensatzeigenschaft** an den Belegzeilen zur Verfügung. Ohne diese Stammdaten findet das Modul keine Werte zum Ersetzen. (Pflege auf der Seite **Materialarten**, siehe **Stammdaten**.)
2. **Globale Formelzeichen festlegen.** Wenn auf der Seite **Erweiterte Texteinstellungen** im Register **Materialtext** die Felder **Formel Start/Ende**, **Startzeichen Unterformel** und **Endzeichen Unterformel** gesetzt sind, dann können bedingte Formelausdrücke ausgewertet werden; andernfalls erfolgt nur die einfache Platzhalterersetzung.
3. **Feldzuordnung pflegen.** Wenn in der **Materialfeld Einrichtung** je Eigenschaftsfeld eine Zeile mit **Tabellen-ID** (Datensatzeigenschaft), **Feldnr.** und **Startzeichen**/**Endzeichen** existiert, dann erkennt das Modul die zugehörigen Platzhalter im Text und ersetzt sie durch die Werte.
4. **Quelle für Arbeitsgangtexte wählen (optional).** Wenn **FA-Zeilen-Materialeigenschaften für Arbeitsgangstexte verwenden** aktiviert ist, dann nutzt das Modul für Arbeitsgangtexte die Materialeigenschaften der FA-Zeile; ist es deaktiviert, die der Arbeitsplatzgruppe.
5. **Automatische Aktualisierung wählen (optional).** Wenn **Autom. aktualisieren erw. Texte** aktiviert ist, dann werden vorhandene Texte bei Wertänderungen — nach Bestätigung — automatisch neu zusammengesetzt.

**Operativer Abschluss.** Die Kette wird im Tagesablauf abgeschlossen, indem der Anwender die **Datensatzeigenschaft**-Werte an der Belegzeile pflegt und den erweiterten Text erzeugen lässt (Vorschau, FactBox, E-Mail oder Bericht). Querverweis: **Tägliche Arbeit: Materialtext in Belegen**.

### Berechtigungen

Der Berechtigungssatz **All permissions** der App legt fest, welche Aktionen Anwender auf den Objekten dieser Erweiterung ausführen dürfen; er gewährt Lese- und Schreibzugriff auf die Tabelle **Materialfeld Einrichtung** sowie Ausführungsrechte auf die zugehörigen Seiten und Codeunits. Weisen Sie diesen Satz den Anwendern zu, die die Materialtext-Einrichtung pflegen oder Materialtexte in Belegen nutzen.

> **Installationshinweis (technisch).** Bei der Installation werden die Formelzeichen **Formel Start/Ende** = `^`, **Startzeichen Unterformel** = `{` und **Endzeichen Unterformel** = `}` als Standard gesetzt, sofern noch leer. Eine Benachrichtigung kann auffordern, die Anwendung neu zu starten, damit Änderungen sichtbar werden.

---

## Stammdaten

Diese App pflegt keine eigenen Stammdatenkarten; sie nutzt die Stammdaten der Apps Materialeigenschaften und Erweitertes Textmodul. Damit der Materialtext funktioniert, müssen die folgenden Stammdaten vorhanden sein.

### Materialart und Datensatzeigenschaft

**Prozess.** Materialarten und Eigenschaften werden in der App Materialeigenschaften gepflegt und den Artikeln zugeordnet; die App Ext. Text Module with Material Properties liest diese Werte nur. Der Administrator legt die **Materialart** an und ordnet sie über den **Eigenschaftscode** den Artikeln zu. An der Belegzeile entstehen daraus die **Datensatzeigenschaft**-Werte (**Eigenschaftswert**), die im Text ersetzt werden.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Materialarten** (App Materialeigenschaften). Die Pflege der Eigenschaftswerte erfolgt an den Artikeln bzw. Belegzeilen.

- **Materialart** — fasst Artikel mit gemeinsamen Eigenschaften zusammen. Wenn ein Artikel eine Materialart trägt, dann erbt die Belegzeile die zugehörigen Eigenschaften, und der Materialtext kann die Werte einsetzen.
- **Eigenschaftscode** — identifiziert die einzelne Eigenschaft (z. B. Breite, Werkstoff). Wenn ein Eigenschaftscode in der **Materialfeld Einrichtung** mit Start-/Endzeichen verknüpft ist, dann ist er als Platzhalter im Text verwendbar.
- **Eigenschaftswert** — der konkrete Wert der Eigenschaft an der Zeile. Wenn der Wert geändert wird und **Autom. aktualisieren erw. Texte** aktiv ist, dann wird der erweiterte Text neu zusammengesetzt.

> Querverweis: Die zu nutzenden Felder werden in der **Materialfeld Einrichtung** festgelegt; die Wirkung im Beleg beschreibt **Tägliche Arbeit: Materialtext in Belegen**.

### Materialzuordnung im Arbeitsblatt erweiterte Textzuordnung

**Prozess.** Auf dem **Arbeitsblatt erweiterte Textzuordnung** des Erweiterten Textmoduls ordnet der Administrator Textvorlagen den Bezugsobjekten zu. Diese App erweitert dabei den **Subtyp** um materialbezogene Werte, sodass Vorlagen gezielt anhand der Materialart einer Belegzeile herangezogen werden. Gepflegt wird die Zuordnung vor der Nutzung; angewendet wird sie automatisch bei der Texterzeugung in Verkaufs-, Einkaufs- und Fertigungszeilen.

**Einstieg:** Öffnen Sie über **Suchen** das **Arbeitsblatt erweiterte Textzuordnung**. Setzen Sie **Typ**/**Subtyp** und ordnen Sie die **Vorlage** zu.

Das Feld **Subtyp** ist ein Optionsfeld. Für die Materialtext-Verarbeitung sind die durch diese App ergänzten Werte maßgeblich:

- **Materialart:** Wenn gewählt, gilt die Zuordnung für genau die in **Subtyp Nummer** angegebene Materialart; das Modul zieht die Vorlage nur, wenn die Belegzeile dieselbe Materialart trägt.
- **Alle Materialarten:** Wenn gewählt, gilt die Zuordnung für jede Belegzeile, die überhaupt eine Materialeigenschaft besitzt, unabhängig von der konkreten Materialart.

Zur Einordnung umfasst der **Subtyp** zusätzlich die Basiswerte des Erweiterten Textmoduls: **(leer)**, **Alle Artikel**, **Artikelkategorie**, **Artikel**, **Alle Arbeitsplätze**, **Arbeitsplatz**, **Alle Arbeitsplatzgruppen**, **Arbeitsplatzgruppe** und **Lief.-an Code**. Diese werden vom Erweiterten Textmodul gesteuert; für den Materialtext sind **Materialart** und **Alle Materialarten** relevant.

> Das Feld **Subtyp Nummer** verweist bei **Subtyp** = **Materialart** auf eine konkrete Materialart. Bei **Alle Materialarten** bleibt es leer.

---

## Tägliche Arbeit: Materialtext in Belegen

Diese App besitzt keinen eigenen Beleg und keine eigene Belegzeilen-Maske. Die tägliche Arbeit findet in den Standard- bzw. m+m-Belegen statt (Verkauf, Einkauf, Fertigung). Dort sorgt die App dafür, dass Materialwerte im erweiterten Text erscheinen.

> **Voraussetzung.** Die Schritte setzen die im Kapitel **Einrichtung** beschriebene Kette voraus (Materialfeld Einrichtung, Formelzeichen, Zuordnung).

**Ablauf an einer Belegzeile:**

1. Erfassen Sie die Belegzeile mit einem Artikel, der eine **Materialart** trägt.
2. Pflegen Sie die **Datensatzeigenschaft**-Werte der Zeile (**Eigenschaftswert**).
3. Lassen Sie den erweiterten Text der Zeile erzeugen. Das Modul ersetzt jeden Platzhalter **Startzeichen + Eigenschaftscode + Endzeichen** durch den Eigenschaftswert.
4. Enthält der Text einen **Formelausdruck**, wird die Bedingung ausgewertet und der bedingte Block nur bei wahrer Bedingung ausgegeben (siehe **Formelausdrücke**).
5. Ändern Sie später einen Eigenschaftswert und ist **Autom. aktualisieren erw. Texte** aktiv, erscheint die Bestätigungsabfrage; nach Bestätigung wird der Text neu zusammengesetzt.

**Read-only-Kennzeichen.** Auf den erzeugten Textzeilen führt das Modul das Kennzeichen **Materialeigenschaft inbegriffen**. Wenn gesetzt, dann signalisiert es, dass die betreffende Textzeile mindestens einen aufgelösten Materialplatzhalter enthält; das Feld wird vom System gepflegt und ist nicht editierbar.

### Formelausdrücke

Formelausdrücke erlauben es, Textteile **bedingt** auszugeben. Sie verwenden die in **Erweiterte Texteinstellungen** gesetzten Zeichen.

- **Bedingung:** wird von **Formel Start/Ende** (Standard `^`) umschlossen.
- **Bedingter Block:** steht zwischen **Startzeichen Unterformel** (Standard `{`) und **Endzeichen Unterformel** (Standard `}`).

Aufbau: `^<Bedingung>^{<Text, wenn Bedingung wahr>}`

- **Wenn** die Bedingung wahr ist, **dann** wird der Block ausgegeben (zuvor werden enthaltene Platzhalter ersetzt).
- **Wenn** die Bedingung falsch ist, **dann** wird der gesamte Block entfernt.

Innerhalb der Bedingung dürfen Platzhalter und Vergleichs- bzw. Rechenoperatoren stehen (z. B. `>`, `<`, `>=`, `<=`, `=`, `<>`, sowie `+`, `-`, `*`, `/`, `^` und die logischen Verknüpfungen `|` und `&`). Blöcke lassen sich verschachteln; das Modul zählt die Unterformel-Zeichen, um den richtigen Endpunkt zu finden. Fehlen die Unterformel-Zeichen in der Einrichtung, bleibt die Formel unaufgelöst und reine Platzhalter werden weiterhin ersetzt.

### Wirkung auf FactBox, E-Mail und Bericht

Die Auflösung der Materialplatzhalter und Formeln wirkt überall dort, wo das Erweiterte Textmodul Texte ausgibt:

- **FactBox** der Belegzeile bzw. Arbeitsgangzeile,
- **E-Mail**-Text (abhängig von **E-Mail Platzhalter** und **E-Mail-Text bevorzugen**),
- **Bericht**-Ausgabe.

In allen drei Fällen werden vor der Ausgabe die Platzhalter durch die Werte der **Datensatzeigenschaft** ersetzt und die Formelbedingungen ausgewertet, sofern die Zeile Materialeigenschaften besitzt.

### Arbeitsgangtexte aus der FA-Zeile

Für Fertigungsaufträge bestimmt **FA-Zeilen-Materialeigenschaften für Arbeitsgangstexte verwenden**, woher die Werte für Arbeitsgangtexte stammen:

- **Wenn aktiviert,** dann werden die Materialeigenschaften der **FA-Zeile** (des produzierten Artikels) verwendet; der Arbeitsgangtext beschreibt damit das Material des Auftrags.
- **Wenn deaktiviert,** dann gelten die erw. Fertigungseigenschaften der **Arbeitsplatzgruppe** wie im ursprünglichen Verhalten.

---

## FAQ und Troubleshooting

### 1. Warum werden meine Platzhalter im Text nicht ersetzt?
Die Eigenschaft muss in der **Materialfeld Einrichtung** als Zeile mit **Tabellen-ID** = Datensatzeigenschaft, passender **Feldnr.** und gesetzten **Startzeichen**/**Endzeichen** hinterlegt sein. Der Platzhalter im Text muss exakt **Startzeichen + Eigenschaftscode + Endzeichen** lauten. Existiert keine passende Zeile, bleibt der Text unverändert.

### 2. Was passiert, wenn ich die Tabellen-ID auf eine andere Tabelle als Datensatzeigenschaft setze?
Das ist nicht zulässig. Das Modul gibt die Meldung *„Ausgewählte Tabellen-ID kann nicht verwendet werden."* aus. Es ist ausschließlich die Tabelle **Datensatzeigenschaft** erlaubt.

### 3. Warum kann ich ein bestimmtes Feld in der Feldnr. nicht auswählen?
Auswählbar sind nur Felder der Typen Ganzzahl, BigInteger, Dezimal, Text, Code oder Option. Felder anderer Typen werden in der Auswahl ausgeblendet, weil ihr Wert nicht als Textplatzhalter eingesetzt werden kann.

### 4. Warum erscheint beim Ändern eines Eigenschaftswerts die Frage, ob ich aktualisieren möchte?
Weil **Autom. aktualisieren erw. Texte** aktiviert ist und bereits erweiterte Texte existieren, die den Wert verwenden könnten. Bestätigen Sie, wird der Text aus den Vorlagen neu zusammengesetzt; lehnen Sie ab, bleibt der bestehende Text erhalten.

### 5. Wie verhindere ich, dass bestehende Texte automatisch überschrieben werden?
Deaktivieren Sie **Autom. aktualisieren erw. Texte** in den **Erweiterte Texteinstellungen**, Register **Materialtext**. Dann werden Texte nur dann neu zusammengesetzt, wenn Sie dies manuell auslösen.

### 6. Warum wird mein Formelausdruck nicht ausgewertet?
Die Felder **Formel Start/Ende**, **Startzeichen Unterformel** und **Endzeichen Unterformel** müssen alle gesetzt sein. Ist eines leer, führt das Modul keine Formelauswertung durch und gibt nur einfache Platzhalter aus.

### 7. Was bedeutet ein bedingter Block, der bei mir leer bleibt?
Das ist das erwartete Verhalten, wenn die Bedingung **falsch** ist: Der gesamte von `^…^{…}` umschlossene Block wird dann entfernt. Prüfen Sie die Werte in der Bedingung und die verwendeten Operatoren.

### 8. Woher nimmt der Arbeitsgangtext die Materialwerte?
Das steuert **FA-Zeilen-Materialeigenschaften für Arbeitsgangstexte verwenden**. Ist es aktiviert, stammen die Werte aus der **FA-Zeile**; ist es deaktiviert, aus der **Arbeitsplatzgruppe**.

### 9. Wie sorge ich dafür, dass eine Vorlage genau für eine bestimmte Materialart gilt?
Setzen Sie auf dem **Arbeitsblatt erweiterte Textzuordnung** den **Subtyp** auf **Materialart** und tragen Sie die Materialart in **Subtyp Nummer** ein. Soll die Vorlage für jede Zeile mit Materialeigenschaft gelten, wählen Sie **Alle Materialarten**.

### 10. Warum ist das Kennzeichen „Materialeigenschaft inbegriffen" nicht editierbar?
Es wird automatisch vom System gepflegt und zeigt an, dass die Textzeile mindestens einen aufgelösten Materialplatzhalter enthält. Es dient der Information und lässt sich nicht manuell ändern.

---

## Typische Anwendungsfälle

Die folgenden Beispiele zeigen realistische Auslöser und den Ablauf in BC. Alle Bildschirme und Aktionen sind im Code geprüft.

### Anwendungsfall 1: Materialtext im Verkaufsangebot

1. **Auslöser.** Ein Kunde fragt telefonisch ein Angebot für einen Stahlartikel an; der Angebotstext soll die Werkstoffdaten enthalten.
2. **Einstieg in BC.** Der Anwender öffnet das Verkaufsangebot und erfasst die Artikelzeile. Der Artikel trägt eine **Materialart**, sodass die **Datensatzeigenschaft**-Werte an der Zeile zur Verfügung stehen.
3. **Kernablauf.** Der Anwender pflegt die Eigenschaftswerte. Beim Erzeugen des erweiterten Textes ersetzt das Modul die Platzhalter (z. B. Breite, Werkstoff) durch die Werte; bedingte Formelausdrücke werden ausgewertet. Über das **Arbeitsblatt erweiterte Textzuordnung** wird — bei **Subtyp** = **Materialart** — die passende Vorlage gezogen.
4. **Abschluss.** Der aufgelöste Text erscheint in der FactBox und wird in den Angebotsausdruck übernommen.

### Anwendungsfall 2: Wertänderung in der Einkaufsbestellung

1. **Auslöser.** Beim Prüfen einer Bestellung stellt der Einkäufer fest, dass eine Materialeigenschaft (z. B. eine Abmessung) korrigiert werden muss.
2. **Einstieg in BC.** Der Einkäufer öffnet die Bestellzeile und ändert den **Eigenschaftswert** der **Datensatzeigenschaft**.
3. **Kernablauf.** Da **Autom. aktualisieren erw. Texte** aktiviert ist und bereits Text existiert, erscheint die Abfrage *„… Möchten Sie aktualisieren?"*. Der Einkäufer bestätigt; der erweiterte Text der Zeile wird aus den Vorlagen neu zusammengesetzt und enthält den neuen Wert.
4. **Abschluss.** Der aktualisierte Text steht für FactBox, E-Mail und Bericht der Bestellung bereit.

### Anwendungsfall 3: Arbeitsgangtext aus der FA-Zeile

1. **Auslöser.** In der Fertigung sollen die Arbeitsgangtexte das Material des produzierten Artikels statt der Eigenschaften der Arbeitsplatzgruppe zeigen.
2. **Einstieg in BC.** Der Administrator aktiviert in den **Erweiterte Texteinstellungen** (Register **Materialtext**) das Feld **FA-Zeilen-Materialeigenschaften für Arbeitsgangstexte verwenden**.
3. **Kernablauf.** Beim Erzeugen der Arbeitsgangtexte des Fertigungsauftrags löst das Modul die Platzhalter anhand der Materialeigenschaften der **FA-Zeile** auf. Werden Eigenschaftswerte der FA-Zeile angelegt oder geändert, werden die betroffenen Arbeitsgang- und Belegzeilentexte des Auftrags aktualisiert.
4. **Abschluss.** Die Arbeitsgangtexte enthalten die materialbezogenen Werte des produzierten Artikels und stehen in FactBox, E-Mail und Bericht zur Verfügung.
