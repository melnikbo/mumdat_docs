---
title: Anwenderhandbuch m+m Test Certificate Management with Aided Data Management
---

# Anwenderhandbuch m+m Test Certificate Management with Aided Data Management

## Einleitung

Das Modul **m+m Test Certificate Management with Aided Data Management** verbindet zwei bestehende m+m-Apps in Microsoft Dynamics 365 Business Central: die **regelbasierte Datenverwaltung** (Regeln und Regelabläufe) und die **Prüfungsverwaltung** (Prüfungen und Prüfvorlagen). Ziel ist, dass **Prüfungen** und **Prüfvorlagen** nicht mehr manuell erfasst, sondern anhand hinterlegter **Regeln** automatisch erzeugt und mit Werten vorbelegt werden, sobald ein auslösendes Ereignis im Tagesgeschäft eintritt.

**Zielgruppe:** Primär sind dies **operative Anwender** in Qualitätssicherung und Wareneingang, die im Tagesgeschäft Prüfungen anlegen (etwa beim Buchen eines Wareneingangs) und deren Prüfungen und Prüfvorlagen durch das Modul automatisch vorbereitet werden. Sekundär richtet sich das Handbuch an **Administratoren und Key-User**, die in der **Regel Einrichtung**, in den **Regeln** und auf der **Materialartenkarte** die Regelabläufe konfigurieren.

**Kurzer Prozessüberblick:** Der Administrator legt in den **Regeln** einzelne Prüf-Regeln an (z. B. „Prüfvorlage nutzen", „Prüfungszeilenfeld setzen"). Diese Regeln werden je **Materialart** zu einem **Regelablauf** zusammengesetzt — getrennt nach **Prüfvorlagen-Regelablauf** und **Prüfregelablauf**. Sobald ein Artikel dieser Materialart entsperrt wird bzw. eine Prüfung angelegt wird, führt das System den passenden Regelablauf automatisch aus und erzeugt bzw. füllt die zugehörige Prüfvorlage oder Prüfung.

Alle in diesem Handbuch genannten Aufrufe erfolgen in „Microsoft Dynamics 365 Business Central". Wo eine Seite über die **Suche** erreichbar ist, ist dies angegeben; Seiten ohne eigene Suchkategorie werden ausschließlich über die genannte übergeordnete Liste oder Aktion geöffnet.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg von der Einrichtung bis zum automatisch erzeugten Prüfergebnis. Die Reihenfolge folgt der technischen Abhängigkeit (zuerst Einrichtung, dann Stammdaten, dann Ausführung).

1. **Nummernvergabe festlegen (einmalig):** Öffnen Sie über die **Suche** die Seite **Regel Einrichtung** und setzen Sie im Register „Allgemein" das Feld **Prüfnummernserie von** auf **Nummerserie** oder **Artikelnr.** (siehe Kapitel *Einrichtung*). Dieses Feld steuert, wie automatisch erzeugte Prüfvorlagen ihre Nummer erhalten.
2. **Regeln anlegen:** Öffnen Sie über die **Suche** die Seite **Regeln** und legen Sie die benötigten Prüf-Regeln an. Wählen Sie je Regel die passende **Regelart** (z. B. **Prüfvorlage nutzen**, **Prüfungszeile nutzen**, **Prüfungszeilenfeld setzen**) und füllen Sie die dann eingeblendeten Felder (siehe Kapitel *Regeln und Regelarten*).
3. **Regelablauf an die Materialart hängen:** Öffnen Sie über die **Suche** die Liste **Materialarten**, öffnen Sie die betreffende Zeile (**Materialartenkarte**) und wählen Sie die Aktion **Prüfvorlagen-Regelablauf** bzw. **Prüfregelablauf**. Setzen Sie im geöffneten **Regelablauf** je Zeile die **Zeilenart** und den **Regelcode** zusammen (siehe Kapitel *Materialarten und Regelabläufe*).
4. **Auslösen im Tagesgeschäft:** Der Ablauf wird anschließend **automatisch** ausgeführt:
   - Der **Prüfvorlagen-Regelablauf** startet, wenn ein **Artikel** dieser Materialart **entsperrt** wird.
   - Der **Prüfregelablauf** startet, wenn eine **Prüfung** angelegt wird (z. B. beim Wareneingang).
5. **Ergebnis prüfen:** Öffnen Sie über die **Suche** die **Prüfvorlagen** bzw. rufen Sie über den Prüfstatus die erzeugte **Prüfung** auf und kontrollieren Sie die automatisch gefüllten Werte.

> Hinweis: Dieses Modul enthält **keinen** manuellen Buchungs- oder Freigabeschritt. Die „Ausführung" ist die **automatische** Verarbeitung des Regelablaufs durch das System (siehe Kapitel *Automatische Ausführung des Regelablaufs*). Der Anwender löst sie indirekt über das Entsperren eines Artikels bzw. das Anlegen einer Prüfung aus.

## Einrichtung

Die Einrichtung dieses Moduls ist bewusst schlank: Das Modul erweitert die bestehende **Regel Einrichtung** der regelbasierten Datenverwaltung um genau ein steuerndes Feld. Alle übrigen Grundeinstellungen (Regeln, Regelabläufe) sind fachliche Stammdaten und stehen in den nachfolgenden Kapiteln.

### Regel Einrichtung

**Einstieg:** Öffnen Sie die Seite **Regel Einrichtung** über die **Suche** in Business Central. Diese Seite ist ein unternehmensweiter Einrichtungsdatensatz (ein Datensatz je Mandant) und über die Suchkategorie „Verwaltung" auffindbar.

**Prozess:** Diese Seite wird vom **Administrator** einmalig **vor der ersten Nutzung** gepflegt. Sie legt fest, wie die regelbasierte Datenverwaltung Nummern für automatisch erzeugte Objekte vergibt. Das durch dieses Modul ergänzte Feld **Prüfnummernserie von** wird später beim **Prüfvorlagen-Regelablauf** ausgewertet, wenn das System eine neue Prüfvorlage anlegt (siehe *Prüfvorlagen-Regelablauf einrichten*).

Die Seite zeigt dem Anwender **eine** zusammengeführte Maske aus Basisfeldern der regelbasierten Datenverwaltung und dem Feld dieses Moduls. Alle sichtbaren Felder des Registers „Allgemein":

| Einrichtung Regel Einrichtung | Erläuterung |
|---|---|
| **Arbeitsplannummern von** | Wenn **Nummerserie** gewählt ist, erhält ein durch einen Regelablauf erzeugter Arbeitsplan seine Nummer aus der hinterlegten Nummernserie; wenn **Artikelnr.** gewählt ist, wird stattdessen die Artikelnummer als Arbeitsplannummer verwendet. Steuert die Nachvollziehbarkeit erzeugter Arbeitspläne (Basisfeld der regelbasierten Datenverwaltung). |
| **Fertigungsstücklistenummern von** | Wenn **Nummerserie** gewählt ist, erhält eine erzeugte Fertigungsstückliste ihre Nummer aus der Nummernserie; wenn **Artikelnr.** gewählt ist, wird die Artikelnummer verwendet. Bestimmt die Nummernvergabe erzeugter Fertigungsstücklisten (Basisfeld der regelbasierten Datenverwaltung). |
| **Prüfnummernserie von** | Steuert die Nummernvergabe automatisch erzeugter **Prüfvorlagen** im Prüfvorlagen-Regelablauf. **Nummerserie:** Wenn gesetzt, legt das System bei der Entsperrung eines Artikels eine **neue** Prüfvorlage mit einer laufenden Nummer aus der Nummernserie an. **Artikelnr.:** Wenn gesetzt, verwendet das System die **Artikelnummer** als Prüfvorlagennummer; existiert bereits eine Prüfvorlage mit dieser Artikelnummer, wird sie **überschrieben** statt eine zusätzliche anzulegen. |

**Optionswerte von „Prüfnummernserie von" (jeder Wert und seine Wirkung):**
- **Nummerserie:** Jede Artikelentsperrung erzeugt eine eigenständige, fortlaufend nummerierte Prüfvorlage; frühere Prüfvorlagen bleiben unverändert bestehen.
- **Artikelnr.:** Es entsteht je Artikel höchstens **eine** Prüfvorlage (Nummer = Artikelnummer). Eine erneute Entsperrung **überschreibt** die vorhandene Prüfvorlage dieses Artikels mit dem aktuellen Regelablaufergebnis.

#### Prüfnummernserie einrichten

**Prozess:** Diese Einrichtung nimmt der **Administrator** einmalig vor der ersten Nutzung vor. Sie ist Voraussetzung dafür, dass der **Prüfvorlagen-Regelablauf** (Kapitel *Materialarten und Regelabläufe*) die erzeugte Prüfvorlage korrekt nummerieren kann.

1. Öffnen Sie über die **Suche** die Seite **Regel Einrichtung**.
2. Setzen Sie das Feld **Prüfnummernserie von**. Wenn Sie **Nummerserie** wählen, entstehen bei jeder Entsperrung neue, fortlaufend nummerierte Prüfvorlagen; wenn Sie **Artikelnr.** wählen, wird je Artikel eine Prüfvorlage geführt und bei erneuter Entsperrung überschrieben.
3. **Operativer Abschluss:** Die Einstellung greift automatisch, sobald ein Artikel der betroffenen Materialart entsperrt wird und der Prüfvorlagen-Regelablauf durchläuft (siehe *Nutzungsbeispiel 1*).

## Regeln und Regelarten

Die eigentliche Fachlogik dieses Moduls liegt in den **Regeln** der regelbasierten Datenverwaltung. Dieses Modul ergänzt die vorhandenen Regelarten um Prüf-spezifische Varianten und blendet je nach gewählter **Regelart** zusätzliche Felder ein. Eine einzelne Regel ist ein Baustein; mehrere Regeln werden später in einem **Regelablauf** je Materialart zu einer Verarbeitungslogik verkettet.

**Einstieg:** Öffnen Sie über die **Suche** die Seite **Regeln**. Öffnen Sie eine Zeile, um die einzelne **Regel** zu bearbeiten. Prüf-spezifische Regeln sind üblicherweise am Namensbestandteil „Prüf" erkennbar.

### Grundfelder einer Regel

Diese Basisfelder legt der Anwender bei jeder Regel fest, bevor die prüf-spezifischen Felder relevant werden:

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger Schlüssel der Regel. Über diesen Code wird die Regel später im Regelablauf als **Regelcode** referenziert; ohne eindeutigen Code kann die Regel nicht in einen Ablauf eingebunden werden. |
| **Beschreibung** | Klartextbezeichnung der Regel. Wenn gepflegt, erleichtert sie die Auswahl im Regelablauf, weil die Zeile dort verständlich benannt ist. |
| **Regelart** | Bestimmt, **was** die Regel tut, und blendet die dazu passenden Felder ein. Die prüf-spezifischen Werte sind unten einzeln erläutert. Wenn eine der „Setzen"-Regelarten gewählt ist, wird zusätzlich die Matrixfunktion aktiviert, sodass der Rückgabewert über die Matrix bestimmt werden kann. |
| **Wertart** | Legt den Datentyp des Rückgabewerts fest (Text, Dezimal, Ganzzahl, Boolean, Datum, Uhrzeit, Datum-Uhrzeit). Wenn gesetzt, prüft und validiert das System den in ein Ziel­feld geschriebenen Wert gegen diesen Typ. |
| **Direkt** | Wenn aktiviert, liefert die Regel ihren Wert unmittelbar (direkte Regel), ohne einen weiteren Zwischenschritt; wenn nicht aktiviert, wird der Wert über die nachgelagerte Ablauflogik bzw. Matrix ermittelt. |

### Regelarten dieses Moduls (Regelart)

Die folgenden **sieben** Regelarten fügt dieses Modul hinzu. Je nach Auswahl wird auf der Regelkarte eine eigene Feldgruppe eingeblendet. Für jede Regelart ist erläutert, **was sie bewirkt**, wenn der Anwender sie auswählt.

| Regelart | Erläuterung |
|---|---|
| **Prüfvorlage nutzen** | Wenn gewählt, verwendet die Regel eine **bestehende Prüfvorlage** als Basis. Es werden die Felder **Prüfvorlagen Nummer** und **Prüfvorlagen Versionscode** eingeblendet. Beim Ablauf legt das System aus dieser Vorlage eine neue Prüfvorlage für den verarbeiteten Artikel an (mit Beschreibung „Erstellt für Artikel …"). |
| **Prüfvorlagenzeile nutzen** | Wenn gewählt, stellt die Regel sicher, dass in der Ziel-Prüfvorlage eine Zeile für die angegebene **Prüfgruppe** und **Prüfeigenschaft** vorhanden ist. Es werden **Prüfgruppencode** und **Prüfeigenschaftsnummer** eingeblendet. Existiert die Zeile nicht, wird sie angelegt; danach ist sie Ziel nachfolgender „Feld setzen"-Regeln. |
| **Prüfvorlagenfeld setzen** | Wenn gewählt, schreibt die Regel einen berechneten Wert in ein Feld des **Prüfvorlagenkopfs**. Es wird das Feld **Feldname** eingeblendet (Auswahl des Zielfelds über die Aktion am Feld). Der Rückgabewert wird typgerecht in das gewählte Kopffeld validiert. |
| **Prüfvorlagenzeilenfeld setzen** | Wenn gewählt, schreibt die Regel einen Wert in ein Feld der zuvor bestimmten **Prüfvorlagenzeile**. Es wird **Feldname** eingeblendet. Voraussetzung ist, dass vorher per „Prüfvorlagenzeile nutzen" die Zielzeile festgelegt wurde. |
| **Prüfungsfeld setzen** | Wenn gewählt, schreibt die Regel einen Wert in ein Feld des **Prüfungskopfs** (nicht der Vorlage, sondern der konkreten Prüfung). Es wird **Feldname** eingeblendet. Wird im **Prüfregelablauf** verwendet, der beim Anlegen einer Prüfung greift. |
| **Prüfungszeile nutzen** | Wenn gewählt, stellt die Regel eine **Prüfungszeile** für die angegebene **Prüfgruppe** und **Prüfeigenschaft** in der aktuellen Prüfung sicher. Es werden **Prüfgruppencode** und **Prüfeigenschaftsnummer** eingeblendet. Fehlt die Zeile, wird sie angelegt und dient als Ziel folgender „Feld setzen"-Regeln. |
| **Prüfungszeilenfeld setzen** | Wenn gewählt, schreibt die Regel einen Wert in ein Feld der zuvor bestimmten **Prüfungszeile**. Es wird **Feldname** eingeblendet. Voraussetzung ist eine vorher per „Prüfungszeile nutzen" bestimmte Zielzeile. |

> Reihenfolge beachten: Bei zeilenbezogenen Regelarten gilt durchgängig — **zuerst** die Zeile bestimmen (Prüfvorlagenzeile/Prüfungszeile nutzen), **dann** die einzelnen Felder setzen. Diese Reihenfolge ist im Regelablauf einzuhalten, sonst fehlt das Ziel für die „Feld setzen"-Regeln.

### Prüf-spezifische Felder der Regel (Feld | Erläuterung)

Diese Felder blendet das Modul abhängig von der gewählten **Regelart** ein. Sie sind die von diesem Modul zur Regelkarte hinzugefügten Steuerfelder.

| Feld | Erläuterung |
|---|---|
| **Prüfvorlagen Nummer** | Wenn gesetzt (bei Regelart **Prüfvorlage nutzen**), bestimmt es die Basis-Prüfvorlage, aus der der Ablauf eine neue Prüfvorlage kopiert. Auswahl nur aus vorhandenen Prüfvorlagen; wirkt zusammen mit dem Versionscode als Schlüssel. |
| **Prüfvorlagen Versionscode** | Wenn gesetzt (bei Regelart **Prüfvorlage nutzen**), wählt es die konkrete **Version** der Basis-Prüfvorlage. Ohne passenden Versionscode findet der Ablauf die Basisvorlage nicht und legt nichts an. |
| **Prüfgruppencode** | Wenn gesetzt (bei „…zeile nutzen"-Regelarten), bestimmt es, für welche **Prüfgruppe** eine Zeile in Prüfvorlage bzw. Prüfung sichergestellt wird. Zusammen mit der Prüfeigenschaftsnummer identifiziert es die Zielzeile eindeutig. |
| **Prüfeigenschaftsnummer** | Wenn gesetzt (bei „…zeile nutzen"-Regelarten), bestimmt es die konkrete **Prüfeigenschaft** innerhalb der Prüfgruppe. Ist der Wert 0/leer, wird keine spezifische Eigenschaft gefiltert. |
| **Feldname** | Wenn eine „Feld setzen"-Regelart gewählt ist, zeigt dieses Feld das aktuell gewählte **Zielfeld**. Über die Aktion am Feld wählt der Anwender Tabelle und Feld; das System merkt sich Feldnummer und Feldname für die spätere Wertzuweisung. |

## Materialarten und Regelabläufe

Damit die einzelnen Regeln wirken, werden sie je **Materialart** zu einem **Regelablauf** zusammengesetzt. Dieses Modul ergänzt die **Materialartenkarte** um zwei Aktionen, mit denen der jeweilige Regelablauf geöffnet und gepflegt wird. Jede Materialart trägt intern zwei systemverwaltete Verknüpfungen (je eine GUID für den Prüfvorlagen- und den Prüfregelablauf); diese werden beim erstmaligen Öffnen der jeweiligen Aktion automatisch angelegt und sind für den Anwender nicht direkt sichtbar.

**Einstieg:** Öffnen Sie über die **Suche** die Liste **Materialarten** und öffnen Sie die gewünschte Zeile. Auf der **Materialartenkarte** stehen im Menüband die beiden Aktionen bereit.

### Regelabläufe von der Materialartenkarte öffnen

| Aktion (Materialartenkarte) | Erläuterung |
|---|---|
| **Prüfvorlagen-Regelablauf** | Öffnet den Regelablauf vom Typ **Prüfvorlage** für diese Materialart. Wenn für die Materialart noch kein Ablauf existiert, legt das System ihn beim ersten Aufruf an. Dieser Ablauf wird später beim **Entsperren eines Artikels** dieser Materialart ausgeführt. |
| **Prüfregelablauf** | Öffnet den Regelablauf vom Typ **Prüfung** für diese Materialart. Auch dieser wird beim ersten Aufruf angelegt, falls noch nicht vorhanden. Er wird später beim **Anlegen einer Prüfung** ausgeführt. |

### Der Regelablauf (Regelablauf-Seite)

Beide Aktionen öffnen dieselbe Seite **Regelablauf** — gefiltert auf den jeweiligen Ablauftyp (**Prüfvorlage** bzw. **Prüfung**). Hier setzt der Anwender die Verarbeitung Zeile für Zeile zusammen.

| Feld / Aktion | Erläuterung |
|---|---|
| **Zeilenart** | Legt fest, wie die Zeile im Ablauf wirkt (z. B. eine **Regel** ausführen, eine Bedingung „Wenn (Wahr)/(Falsch)/(Vergleich)", eine Variable setzen oder eine Meldung ausgeben). Wenn **Regel** gewählt ist, wird das Feld **Regelcode** bearbeitbar. |
| **Ablauf** | Zeigt die aus Zeilenart und Regel zusammengesetzte, eingerückte Klartextdarstellung des Ablaufs. Dient der Übersicht und wird bei jeder Änderung aktualisiert. |
| **Regelcode** | Verweist auf den **Code** einer zuvor angelegten Regel (Kapitel *Regeln und Regelarten*). Wenn gesetzt, wird beim Ablauf genau diese Regel ausgeführt. |
| Aktion **Flow Editor** | Öffnet die grafische bzw. strukturierte Bearbeitung desselben Ablaufs zur komfortableren Pflege verzweigter Abläufe. |
| Aktion **Variablen** | Öffnet die Liste der **Variablen** dieses Ablaufs. Variablen nehmen Zwischenergebnisse auf, die spätere Zeilen weiterverwenden. |

> Empfehlung aus der Praxis: Bauen Sie in jeden Ablauf am Ende eine Zeile mit einer Meldungsregel ein. Sie zeigt dem Anwender nach der automatischen Ausführung, dass der Ablauf tatsächlich durchlaufen wurde.

#### Prüfvorlagen-Regelablauf einrichten

**Prozess:** Diese Konfiguration nimmt der **Administrator/Key-User** je Materialart vor, **bevor** Artikel dieser Materialart produktiv entsperrt werden. Der eingerichtete Ablauf wird später im Tagesgeschäft automatisch ausgeführt (siehe *Automatische Ausführung* und *Nutzungsbeispiel 1*).

1. **Voraussetzung Nummernvergabe:** Stellen Sie sicher, dass **Prüfnummernserie von** in der **Regel Einrichtung** gesetzt ist (siehe *Prüfnummernserie einrichten*). Sie entscheidet, ob je Entsperrung eine neue Prüfvorlage entsteht (**Nummerserie**) oder die Prüfvorlage des Artikels überschrieben wird (**Artikelnr.**).
2. **Regeln bereitstellen:** Legen Sie in den **Regeln** die benötigten Bausteine an, typischerweise **Prüfvorlage nutzen** (Basisvorlage), **Prüfvorlagenzeile nutzen** (Zielzeile je Prüfgruppe/Prüfeigenschaft) und **Prüfvorlagenzeilenfeld setzen** bzw. **Prüfvorlagenfeld setzen** (Wertzuweisung). Wenn diese Regeln vorhanden sind, können sie im Ablauf referenziert werden.
3. **Ablauf zusammensetzen:** Öffnen Sie **Materialarten → Materialartenkarte → Prüfvorlagen-Regelablauf** und setzen Sie je Zeile die **Zeilenart** und — bei Zeilenart **Regel** — den **Regelcode**. Beachten Sie: zuerst „Prüfvorlagenzeile nutzen", dann die zugehörigen „…feld setzen"-Regeln.
4. **Operativer Abschluss:** Sobald ein **Artikel** dieser Materialart **entsperrt** wird, führt das System den Ablauf aus und legt die Prüfvorlage an bzw. überschreibt sie (siehe *Nutzungsbeispiel 1*).

#### Prüfregelablauf einrichten

**Prozess:** Diese Konfiguration ist eine **eigenständige** Fähigkeit neben dem Prüfvorlagen-Regelablauf und wird ebenfalls je Materialart durch den **Administrator/Key-User** vorgenommen. Sie steuert, was beim **Anlegen einer Prüfung** automatisch geschieht.

1. **Regeln bereitstellen:** Legen Sie die für Prüfungen passenden Regelarten an — typischerweise **Prüfungsfeld setzen** (z. B. Anzahl Proben im Prüfungskopf), **Prüfungszeile nutzen** (Zielzeile je Prüfgruppe/Prüfeigenschaft) und **Prüfungszeilenfeld setzen** (Werte in der Zeile, z. B. von/bis).
2. **Ablauf zusammensetzen:** Öffnen Sie **Materialarten → Materialartenkarte → Prüfregelablauf** und ordnen Sie die Regeln über **Zeilenart** und **Regelcode**. Halten Sie auch hier die Reihenfolge Zeile-vor-Feld ein.
3. **Operativer Abschluss:** Beim **Anlegen einer Prüfung** (z. B. beim Wareneingang eines Artikels dieser Materialart) startet der Ablauf automatisch und füllt Prüfungskopf und -zeilen (siehe *Nutzungsbeispiel 2*).

## Automatische Ausführung des Regelablaufs

Dieses Modul kennt keinen manuellen Buchungs- oder Freigabeknopf. Die Regelabläufe werden **ereignisgesteuert** ausgeführt. Der Anwender stößt sie mittelbar an; das System erledigt die Verarbeitung im Hintergrund.

| Auslösendes Ereignis | Ausgeführter Ablauf | Wirkung |
|---|---|---|
| **Artikel wird entsperrt** | **Prüfvorlagen-Regelablauf** der Materialart des Artikels | Das System legt gemäß **Prüfnummernserie von** eine neue Prüfvorlage an (Nummerserie) oder überschreibt die vorhandene Prüfvorlage des Artikels (Artikelnr.) und füllt Zeilen und Felder gemäß den Regeln. Ein leerer Ablauf löst nichts aus. |
| **Prüfung wird angelegt** (Kopf eingefügt oder Objektbezug geändert) | **Prüfregelablauf** der Materialart des im Prüfungskopf referenzierten Artikels | Das System füllt Prüfungskopf und -zeilen gemäß den Regeln (z. B. Anzahl Proben, von/bis-Werte). Betrifft nur Prüfungen mit Objektart **Artikel**; ohne hinterlegte Materialart oder bei leerem Ablauf geschieht nichts. |

Voraussetzung in beiden Fällen: Der jeweilige Regelablauf der Materialart ist **nicht leer**. Ist kein Ablauf hinterlegt oder enthält er keine Zeilen, überspringt das System die Verarbeitung ohne Meldung.

## Typische Anwendungsfälle (Nutzungsbeispiele)

Die folgenden Szenarien zeigen den durchgängigen Weg vom Auslöser bis zum Ergebnis. Jeder Schritt entspricht einer im Code bzw. per MCP bestätigten Seite oder Aktion dieses Moduls.

### Nutzungsbeispiel 1: Prüfvorlage automatisch aus Regeln erzeugen

1. **Auslöser:** Die Qualitätssicherung legt für eine bestimmte Materialart fest, dass zu jedem neuen Artikel automatisch eine Prüfvorlage mit definierten Prüfzeilen entstehen soll. Ein Sachbearbeiter erhält einen neuen Artikel zur Anlage.
2. **Einstieg in BC (Einrichtung, einmalig):** Der Administrator setzt in der **Regel Einrichtung** das Feld **Prüfnummernserie von** (z. B. auf **Artikelnr.**, damit je Artikel genau eine Prüfvorlage geführt wird). Anschließend legt er in den **Regeln** die Bausteine an (**Prüfvorlage nutzen**, **Prüfvorlagenzeile nutzen**, **Prüfvorlagenzeilenfeld setzen**) und verkettet sie über **Materialarten → Materialartenkarte → Prüfvorlagen-Regelablauf** zu einem Ablauf.
3. **Kernablauf:** Der Sachbearbeiter legt den neuen **Artikel** an, trägt **Materialartencode**, **Basiseinheitencode** ein und setzt den Artikel zunächst auf **Gesperrt**. Nach Pflege der Eigenschaftswerte entsperrt er den Artikel wieder. Mit dem Entsperren startet das System den **Prüfvorlagen-Regelablauf** automatisch; eine Meldungsregel bestätigt am Ende den Durchlauf.
4. **Abschluss:** Der Anwender öffnet über die **Suche** die **Prüfvorlagen** und findet die für den Artikel automatisch erzeugte Prüfvorlage; Zeilen und von/bis-Werte sind gemäß den Regeln vorbelegt. Bei Einstellung **Artikelnr.** trägt die Prüfvorlage die Artikelnummer und wird bei erneuter Entsperrung überschrieben.

### Nutzungsbeispiel 2: Prüfung beim Wareneingang automatisch vorbelegen

1. **Auslöser:** Für einen Einkaufsartikel soll bei jedem Wareneingang automatisch eine Prüfung mit passender Probenanzahl und vorbelegten Grenzwerten entstehen, ohne dass der Wareneingangsmitarbeiter Werte manuell erfasst.
2. **Einstieg in BC (Einrichtung, einmalig):** Der Administrator legt Regeln vom Typ **Prüfungsfeld setzen** (z. B. Anzahl Proben), **Prüfungszeile nutzen** und **Prüfungszeilenfeld setzen** (Grenzwerte) an und verkettet sie über **Materialarten → Materialartenkarte → Prüfregelablauf**.
3. **Kernablauf:** Der Einkauf legt eine Einkaufsbestellung an und gibt sie frei. Beim Anlegen des Wareneingangs entsteht für den Artikel eine **Prüfung**. Mit dem Einfügen des Prüfungskopfs startet das System den **Prüfregelablauf** automatisch; es setzt die Felder im Prüfungskopf (z. B. Anzahl Proben) und füllt in den Zeilen die von/bis-Werte aus den Artikeleigenschaften.
4. **Abschluss:** Der Wareneingangsmitarbeiter ruft über den Prüfstatus die erzeugte **Prüfung** auf und kontrolliert die automatisch gesetzten Werte. Eine abschließende Meldungsregel signalisiert, dass der Ablauf vollständig durchlaufen wurde.

## FAQ und Troubleshooting

### 1. Warum passiert beim Entsperren eines Artikels nichts?
Der **Prüfvorlagen-Regelablauf** wird nur ausgeführt, wenn die **Materialart** des Artikels einen **nicht leeren** Ablauf besitzt. Fehlt der Materialartencode am Artikel, ist der Materialart kein Ablauf zugeordnet oder ist der Ablauf leer, überspringt das System die Verarbeitung ohne Meldung. Prüfen Sie den Materialartencode und öffnen Sie über die **Materialartenkarte** den **Prüfvorlagen-Regelablauf**.

### 2. Warum wird meine Prüfvorlage bei jedem Entsperren überschrieben statt neu angelegt?
Das steuert das Feld **Prüfnummernserie von** in der **Regel Einrichtung**. Bei **Artikelnr.** führt das System je Artikel genau eine Prüfvorlage (Nummer = Artikelnummer) und **überschreibt** sie bei erneuter Entsperrung. Wenn Sie stattdessen bei jedem Durchlauf eine neue Prüfvorlage möchten, wählen Sie **Nummerserie**.

### 3. Warum bleibt eine Prüfungszeile nach „Prüfungszeilenfeld setzen" leer?
Die Regelart **Prüfungszeilenfeld setzen** schreibt nur in eine bereits bestimmte Zeile. Fehlt zuvor eine Regel **Prüfungszeile nutzen** mit passendem **Prüfgruppencode** und passender **Prüfeigenschaftsnummer**, gibt es kein Ziel für das Feld. Setzen Sie im Ablauf zuerst „Prüfungszeile nutzen" und danach „Prüfungszeilenfeld setzen".

### 4. Wie wähle ich das Zielfeld für eine „Feld setzen"-Regelart aus?
Wählen Sie zunächst die Regelart (z. B. **Prüfungsfeld setzen**). Danach erscheint das Feld **Feldname**. Über dessen Aktion wählen Sie Tabelle und Feld; das System merkt sich intern Feldnummer und Feldname und zeigt den Feldnamen an.

### 5. Warum stehen bei der Regelart „Prüfvorlage nutzen" die Zeilenfelder nicht zur Verfügung?
Jede Regelart blendet nur ihre eigenen Felder ein. **Prüfvorlage nutzen** zeigt **Prüfvorlagen Nummer** und **Prüfvorlagen Versionscode**. Für zeilenbezogene Angaben (Prüfgruppencode, Prüfeigenschaftsnummer) benötigen Sie eine eigene Regel mit einer „…zeile nutzen"-Regelart.

### 6. Warum findet der Ablauf die Basis-Prüfvorlage nicht?
Bei **Prüfvorlage nutzen** identifizieren **Prüfvorlagen Nummer** und **Prüfvorlagen Versionscode** gemeinsam die Basisvorlage. Ist der Versionscode falsch oder leer, kann das System die Vorlage nicht laden und legt nichts an. Kontrollieren Sie beide Werte.

### 7. Warum wird der Prüfregelablauf beim Ändern einer bestehenden Prüfung nicht erneut ausgeführt?
Der Prüfregelablauf startet beim **Anlegen** einer Prüfung und beim Ändern nur dann, wenn sich der **Objektbezug** (Objektart/Objektnummer) ändert. Reine Wertänderungen an einer bestehenden Prüfung lösen keinen erneuten Durchlauf aus.

### 8. Gibt es in diesem Modul einen Buchungs- oder Freigabeschritt?
Nein. Die Verarbeitung ist **automatisch** und ereignisgesteuert (Artikel entsperren bzw. Prüfung anlegen). Es gibt keine gesonderte Buchungs- oder Freigabeaktion dieses Moduls.

### 9. Wie erkenne ich, dass ein Ablauf tatsächlich durchgelaufen ist?
Bauen Sie in den Ablauf eine Zeile mit einer **Meldungsregel** ein (Zeilenart Meldung). Sie zeigt nach der automatischen Verarbeitung eine Bestätigung an und ist der zuverlässigste Weg, den Durchlauf im Tagesgeschäft sichtbar zu machen.

### 10. Der Prüfvorlagen-Regelablauf und der Prüfregelablauf verwenden dieselbe Materialart — beeinflussen sie sich?
Nein. Jede Materialart führt zwei getrennte Abläufe: einen für **Prüfvorlagen** (Auslöser: Artikel entsperren) und einen für **Prüfungen** (Auslöser: Prüfung anlegen). Sie werden zu unterschiedlichen Zeitpunkten und über unterschiedliche Aktionen der **Materialartenkarte** gepflegt und ausgeführt.

## Berechtigungen

Das Modul liefert den Berechtigungssatz **MuM TCNO Permission** mit. Er bestimmt die Ausführungsberechtigungen für die Verarbeitungslogik dieses Moduls und legt fest, welche Aktionen die zugeordneten Anwender im Regelablauf ausführen können. Der Berechtigungssatz umfasst die vier Codeunits des Moduls (Ereignis-Abonnenten sowie die Verarbeitungs-Codeunits für Prüfungen und Prüfvorlagen) und ist zuweisbar. Die eigentliche Sichtbarkeit von Regeln, Materialarten und Prüfungen richtet sich zusätzlich nach den Berechtigungen der zugrunde liegenden Basismodule (regelbasierte Datenverwaltung, Materialeigenschaften, Prüfungsverwaltung).
