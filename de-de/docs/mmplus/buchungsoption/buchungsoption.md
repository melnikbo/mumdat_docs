---
title: Anwenderhandbuch m+m Posting Options
---

# Anwenderhandbuch m+m Posting Options

## Einleitung

Die Erweiterung **m+m Posting Options** steuert, welche **Buchungsoptionen** Anwenderinnen und Anwender beim Buchen eines Belegs überhaupt noch auswählen dürfen. Im Standard von Microsoft Dynamics 365 Business Central bietet BC beim Buchen eines Verkaufs- oder Einkaufsbelegs mehrere Optionen an (**Liefern**, **Fakturieren**, **Liefern und fakturieren**). Diese Erweiterung erlaubt es, dieses Angebot unternehmensweit einzuschränken, damit beim Buchen nur die betrieblich gewünschten Optionen erscheinen.

Die Steuerung erfolgt getrennt für drei Bereiche:

- **Auftragsbestätigung/Reklamation** — Verkaufsaufträge und Verkaufsreklamationen,
- **Bestellung/Reklamation** — Einkaufsbestellungen und Einkaufsreklamationen,
- **Warenausgang** — Warenausgänge aus dem Lager.

**Zielgruppe:** Primär richtet sich dieses Handbuch an die **operativen Anwender** im Verkauf, Einkauf und Lager, die täglich Belege buchen und beim Buchen die eingeschränkte Auswahl erleben. Sekundär betrifft es **Administratorinnen und Administratoren** bzw. Key-User, die die eine zentrale Einrichtungsseite einmalig pflegen.

**Kurzer Prozessüberblick:** Ein Administrator legt in der Seite **Buchungsoptionen Einrichtung** je Bereich fest, welche Buchungsoption gelten soll. Sobald eine Anwenderin danach in einem Verkaufsauftrag, einer Einkaufsbestellung oder einem Warenausgang die Aktion **Buchen** (bzw. **Buchen und neu** / **Buchen und senden**) auslöst, greift die hinterlegte Regel: Statt des vollständigen Standardmenüs erscheint nur noch die konfigurierte Auswahl, oder der Buchungsvorgang läuft direkt ohne Rückfrage durch.

Die Erweiterung fügt **keine** neuen Felder in Verkaufs-, Einkaufs- oder Warenausgangsbelege ein und legt **keine** eigenen Belege, Listen oder gebuchten Historien an. Sie besitzt genau **eine** Einrichtungsseite; die gesamte Wirkung entfaltet sich im vorhandenen Buchungsdialog der Standardbelege.

## Schnellstart für Anwender

Der schnellste Weg zum Ergebnis besteht aus einer einmaligen Einrichtung und der anschließenden täglichen Nutzung beim Buchen.

**Zuerst — Einrichtung (einmalig, durch Administrator):**

1. Öffnen Sie die Seite **Buchungsoptionen Einrichtung**. Geben Sie dazu in der BC-Suche (**Suchen**) den Begriff `Buchungsoptionen Einrichtung` ein und wählen Sie den gleichnamigen Link.
2. Setzen Sie im Feld **Auftragsbestätigung/Reklamation - Buchungsoptionen** die gewünschte Einschränkung für den Verkauf.
3. Setzen Sie im Feld **Bestellung/Reklamation - Buchungsoptionen** die gewünschte Einschränkung für den Einkauf.
4. Setzen Sie im Feld **Warenausgang - Buchungsoptionen** die gewünschte Einschränkung für den Lager-Warenausgang.
5. Belassen Sie ein Feld auf **Standard**, wenn im jeweiligen Bereich das unveränderte BC-Verhalten gelten soll. Die Einträge werden sofort gespeichert; es ist keine Freigabe- oder Aktivierungsaktion nötig.

**Danach — tägliche Nutzung (durch die operativen Anwender beim Buchen):**

1. Öffnen Sie den Beleg (z. B. **Verkaufsauftrag**, **Einkaufsbestellung** oder **Warenausgang**) und erfassen Sie die Zeilen wie gewohnt.
2. Lösen Sie die Buchung über **Buchen**, **Buchen und neu** oder **Buchen und senden** aus.
3. Statt des vollständigen Standardmenüs erscheint nur die in der Einrichtung hinterlegte Auswahl:
   - Bei einer Einzeloption wird die Buchung direkt mit dieser Option ausgeführt (nur eine Menüzeile).
   - Bei zwei zugelassenen Optionen wählen Sie zwischen den beiden angebotenen Zeilen.
   - Bei **Standard** verhält sich BC unverändert.
4. Bestätigen Sie die Auswahl; der Beleg wird entsprechend gebucht.

## Einrichtung

Die gesamte Konfiguration der Erweiterung findet auf **einer** unternehmensweiten Seite statt: **Buchungsoptionen Einrichtung**. Es gibt genau einen Datensatz je Mandant; die Seite legt diesen Datensatz beim ersten Öffnen automatisch an.

### Buchungsoptionen einrichten

**Wer und wann:** Diese Einrichtung nimmt der Administrator bzw. ein Key-User **einmalig vor der ersten produktiven Nutzung** vor und passt sie nur bei geänderten betrieblichen Vorgaben an. Sie gilt **mandantenweit** für alle Anwender und alle betroffenen Belege. Die hier gesetzten Optionen werden später beim Buchen in **Verkaufsaufträgen/-reklamationen**, **Einkaufsbestellungen/-reklamationen** und **Warenausgängen** wirksam (siehe Abschnitt **Tägliche Arbeit: Buchen mit eingeschränkten Optionen**).

**Voraussetzung:** Die Erweiterung **m+m Posting Options** muss in der **Erweiterungsverwaltung** installiert sein. Eine Nummernserie, ein Lagerort oder weitere Stammdaten sind **nicht** erforderlich — die Seite arbeitet mit einem einzigen, automatisch erzeugten Einrichtungsdatensatz.

**Einstieg:** Öffnen Sie die Seite über **Suchen** mit dem Begriff `Buchungsoptionen Einrichtung`. Die Seite ist als unternehmensweite Verwaltungsseite (Kategorie **Verwaltung**) angelegt und besitzt **keine** übergeordnete Liste oder Stammdatenkarte, von der aus sie geöffnet würde; der Einstieg über **Suchen** ist daher der vorgesehene und einzige Weg.

Im Bereich **Allgemein** stehen drei Felder zur Verfügung. Jedes Feld steuert **einen** Belegbereich unabhängig von den anderen.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Auftragsbestätigung/Reklamation - Buchungsoptionen** | Legt fest, welche Buchungsoptionen beim Buchen eines **Verkaufsauftrags** oder einer **Verkaufsreklamation** angeboten werden. Wenn ein anderer Wert als **Standard** gewählt ist, ersetzt die Erweiterung das Standardmenü beim Buchen durch die hier festgelegte, eingeschränkte Auswahl (Werte siehe unten). |
| **Bestellung/Reklamation - Buchungsoptionen** | Legt fest, welche Buchungsoptionen beim Buchen einer **Einkaufsbestellung** oder **Einkaufsreklamation** angeboten werden. Wenn ein anderer Wert als **Standard** gewählt ist, wird beim Buchen nur die konfigurierte Auswahl angezeigt; im Einkauf entspricht „Liefern“ dem Wareneingang der Bestellung (Werte siehe unten). |
| **Warenausgang - Buchungsoptionen** | Legt fest, welche Buchungsoptionen beim Buchen eines **Warenausgangs** angeboten werden. Wenn ein anderer Wert als **Standard** gewählt ist, wird der Warenausgang beim Buchen auf die konfigurierte Auswahl beschränkt (Werte siehe unten). |

#### Werte für Auftragsbestätigung/Reklamation und Bestellung/Reklamation

Beide Felder besitzen dieselbe Wertemenge. Die Wirkung greift ausschließlich bei den Belegarten **Auftrag** und **Reklamation** des jeweiligen Bereichs.

- **Standard:** Wenn gesetzt, bleibt das BC-Standardverhalten unverändert; beim Buchen erscheint das vollständige Standardmenü, und die Erweiterung greift nicht ein.
- **Nur Liefern:** Wenn gesetzt, wird beim Buchen ausschließlich **Liefern** angeboten (im Einkauf der Wareneingang, im Verkauf die Lieferung; bei Reklamationen die jeweils gegenläufige Warenbewegung). Es erscheint nur eine Menüzeile, sodass ohne weitere Wahl geliefert bzw. eingegangen wird — es wird nicht fakturiert.
- **Nur Fakturieren:** Wenn gesetzt, wird beim Buchen ausschließlich **Fakturieren** angeboten. Der Beleg wird nur fakturiert; eine Warenbewegung findet über diese Option nicht statt.
- **Nur Liefern und fakturieren:** Wenn gesetzt, wird beim Buchen ausschließlich die kombinierte Option **Liefern und fakturieren** angeboten. Warenbewegung und Faktura erfolgen in einem Schritt; eine reine Lieferung oder reine Faktura ist über diese Option nicht wählbar.
- **Fakturieren/Liefern und fakturieren:** Wenn gesetzt, erscheinen beim Buchen **zwei** Zeilen zur Auswahl: **Fakturieren** oder **Liefern und fakturieren**. Der Anwender entscheidet fallweise, ob nur fakturiert oder zusätzlich geliefert wird.
- **Liefern/Liefern und fakturieren:** Wenn gesetzt, erscheinen beim Buchen **zwei** Zeilen zur Auswahl: **Liefern** oder **Liefern und fakturieren**. Der Anwender entscheidet fallweise, ob nur geliefert oder zusätzlich fakturiert wird.

> Hinweis zu Reklamationen: Die Erweiterung berücksichtigt die Belegart automatisch. Im Verkauf entspricht „Liefern“ beim Auftrag der Lieferung und bei der Reklamation der Rücknahme (Wareneingang); im Einkauf entspricht „Liefern“ bei der Bestellung dem Wareneingang und bei der Reklamation der Rücklieferung (Warenausgang). Die Beschriftung der Menüzeile lautet in allen Fällen einheitlich **Liefern** bzw. **Fakturieren**.

#### Werte für Warenausgang

Das Feld **Warenausgang - Buchungsoptionen** besitzt eine reduzierte Wertemenge, da beim Warenausgang keine reine Faktura möglich ist.

- **Standard:** Wenn gesetzt, bleibt das BC-Standardverhalten des Warenausgangs unverändert; die Erweiterung greift nicht ein.
- **Nur Liefern:** Wenn gesetzt, wird der Warenausgang beim Buchen ausschließlich **geliefert** (Warenausgang ohne Faktura). Es erscheint nur eine Menüzeile.
- **Nur Liefern und fakturieren:** Wenn gesetzt, wird der Warenausgang beim Buchen zusammen mit der **Faktura** gebucht (Lieferung und Rechnung in einem Schritt).

**Ablauf der Einrichtung in Abhängigkeitsreihenfolge:**

1. **Zuerst** installieren Sie die Erweiterung in der **Erweiterungsverwaltung** (Voraussetzung).
2. **Danach** öffnen Sie **Buchungsoptionen Einrichtung** über **Suchen**; der Einrichtungsdatensatz wird beim ersten Öffnen automatisch angelegt.
3. **Anschließend** setzen Sie je Bereich (**Auftragsbestätigung/Reklamation**, **Bestellung/Reklamation**, **Warenausgang**) den gewünschten Wert; jedes Feld wirkt sofort und unabhängig.
4. **Zuletzt** prüfen die operativen Anwender die Wirkung beim Buchen im jeweiligen Beleg (siehe **Tägliche Arbeit** und **Typische Anwendungsfälle**).

## Tägliche Arbeit: Buchen mit eingeschränkten Optionen

Dieser Abschnitt beschreibt, wie sich die in **Buchungsoptionen Einrichtung** gesetzten Werte im Buchungsalltag auswirken. Gesteuert wird die tägliche Arbeit ausschließlich über die Einrichtungsseite (siehe **Buchungsoptionen einrichten**); an den Belegen selbst nimmt die Erweiterung keine sichtbaren Änderungen vor.

Die Erweiterung greift automatisch in den Buchungsvorgang folgender Belege ein:

- **Verkaufsauftrag** und **Verkaufsreklamation** — gesteuert durch **Auftragsbestätigung/Reklamation - Buchungsoptionen**,
- **Einkaufsbestellung** und **Einkaufsreklamation** — gesteuert durch **Bestellung/Reklamation - Buchungsoptionen**,
- **Warenausgang** — gesteuert durch **Warenausgang - Buchungsoptionen**.

### Buchungsablauf am Verkaufs- und Einkaufsbeleg

1. Wählen Sie den Beleg (**Verkaufsauftrag**, **Verkaufsreklamation**, **Einkaufsbestellung** oder **Einkaufsreklamation**) und erfassen bzw. prüfen Sie die Zeilen.
2. Lösen Sie die Buchung über eine der Standardaktionen **Buchen**, **Buchen und neu** oder **Buchen und senden** aus.
3. Vor der eigentlichen Buchung prüft die Erweiterung die hinterlegte Buchungsoption des Bereichs und ersetzt das Standard-Auswahlmenü:
   - **Standard** — es erscheint das unveränderte BC-Standardmenü.
   - Einzeloption (**Nur Liefern**, **Nur Fakturieren**, **Nur Liefern und fakturieren**) — es erscheint nur die eine zugelassene Menüzeile; die Buchung wird mit dieser Option ausgeführt.
   - Doppeloption (**Fakturieren/Liefern und fakturieren**, **Liefern/Liefern und fakturieren**) — es erscheinen zwei Zeilen; Sie wählen die gewünschte aus.
4. Wird die Auswahl abgebrochen (kein Eintrag gewählt), so wird der Buchungsvorgang **nicht** ausgeführt.
5. Bestätigen Sie die Auswahl; der Beleg wird entsprechend gebucht.

### Buchungsablauf am Warenausgang

1. Öffnen Sie den **Warenausgang** und wählen Sie die zu buchenden Zeilen.
2. Lösen Sie das Buchen des Warenausgangs aus.
3. Die Erweiterung ersetzt das Auswahlmenü gemäß **Warenausgang - Buchungsoptionen**:
   - **Standard** — unverändertes BC-Verhalten.
   - **Nur Liefern** — der Warenausgang wird nur geliefert.
   - **Nur Liefern und fakturieren** — der Warenausgang wird geliefert und fakturiert.
4. Bestätigen Sie die Auswahl; der Warenausgang wird entsprechend gebucht.

## Berechtigungen

Die Erweiterung liefert einen Berechtigungssatz mit, der den vollständigen Zugriff auf die Objekte der Erweiterung bündelt.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Alle Berechtigungen** (Berechtigungssatz **MuM PV All Perm.**) | Bestimmt die Berechtigungen für die Objekte der Erweiterung. Wenn dieser Satz einem Benutzer oder einer Benutzergruppe zugewiesen ist, kann dieser die Seite **Buchungsoptionen Einrichtung** öffnen und die Einrichtungsdaten lesen und bearbeiten. Der Berechtigungssatz legt fest, welche Aktionen die Anwender an den Einrichtungsdaten ausführen können; ohne diese Zuweisung ist die Einrichtung nicht bearbeitbar. |

Weisen Sie diesen Berechtigungssatz nur den Personen zu, die die Buchungsoptionen verwalten sollen (in der Regel Administratorinnen und Administratoren oder Key-User). Für die tägliche Buchung selbst genügen die Standard-Buchungsberechtigungen von Business Central; die Erweiterung greift bei jedem Buchungsvorgang automatisch, ohne dass die operativen Anwender einen eigenen Berechtigungssatz benötigen.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die Erweiterung im Arbeitsalltag wirkt. Jeder Ablauf beginnt mit einem Auslöser außerhalb von Business Central und endet mit dem gebuchten Beleg.

### Verkauf auf „Nur Liefern“ beschränken

1. **Auslöser:** Die Vertriebsleitung möchte verhindern, dass Verkaufsaufträge versehentlich sofort fakturiert werden, weil der Verkaufspreis erst später final feststeht. Die Fakturierung soll ausschließlich über einen separaten Prozess erfolgen.
2. **Einstieg in BC:** Der Administrator öffnet über **Suchen** die Seite **Buchungsoptionen Einrichtung** und setzt das Feld **Auftragsbestätigung/Reklamation - Buchungsoptionen** auf **Nur Liefern**.
3. **Kernablauf:** Eine Sachbearbeiterin erfasst einen **Verkaufsauftrag** und löst **Buchen** aus. Statt des vollständigen Standardmenüs erscheint nur die Zeile **Liefern**. Die Buchung liefert den Auftrag, ohne zu fakturieren.
4. **Abschluss:** Der Auftrag ist geliefert; eine spätere Faktura erfolgt über den regulären Rechnungsprozess. Eine versehentliche Sofortfaktura ist ausgeschlossen.

### Einkauf auf „Nur Liefern und fakturieren“ festlegen

1. **Auslöser:** Im Einkauf sollen Wareneingang und Rechnung stets gemeinsam gebucht werden, um getrennte Teilbuchungen und den damit verbundenen Abstimmungsaufwand zu vermeiden.
2. **Einstieg in BC:** Der Administrator öffnet **Buchungsoptionen Einrichtung** und setzt **Bestellung/Reklamation - Buchungsoptionen** auf **Nur Liefern und fakturieren**.
3. **Kernablauf:** Ein Einkaufssachbearbeiter bucht eine **Einkaufsbestellung** über **Buchen**. Es erscheint nur die Zeile **Liefern und fakturieren**; Wareneingang und Rechnung werden in einem Schritt gebucht.
4. **Abschluss:** Die Bestellung ist eingegangen und fakturiert. Reine Wareneingänge ohne Rechnung sind über diesen Beleg nicht mehr möglich.

### Anwender im Verkauf zwischen zwei Optionen wählen lassen

1. **Auslöser:** Der Verkauf soll flexibel bleiben: In manchen Fällen wird nur geliefert, in anderen sofort geliefert und fakturiert. Ein reines Fakturieren ohne Lieferung soll jedoch ausgeschlossen sein.
2. **Einstieg in BC:** Der Administrator setzt in **Buchungsoptionen Einrichtung** das Feld **Auftragsbestätigung/Reklamation - Buchungsoptionen** auf **Liefern/Liefern und fakturieren**.
3. **Kernablauf:** Beim Buchen eines **Verkaufsauftrags** erscheinen genau zwei Zeilen: **Liefern** und **Liefern und fakturieren**. Der Anwender wählt situativ die passende Option.
4. **Abschluss:** Der Auftrag wird je nach Auswahl geliefert oder geliefert und fakturiert; die unerwünschte Option „nur fakturieren“ steht nicht zur Verfügung.

## FAQ und Troubleshooting

### 1. Warum erscheint beim Buchen weiterhin das vollständige Standardmenü?

Der betreffende Bereich steht in **Buchungsoptionen Einrichtung** auf **Standard**. Bei **Standard** greift die Erweiterung bewusst nicht ein und überlässt das Buchen dem BC-Standard. Setzen Sie das passende Feld auf einen anderen Wert, um die Auswahl einzuschränken.

### 2. Wie öffne ich die Einrichtung, wenn ich keinen Menüeintrag finde?

Die Seite hat keine übergeordnete Liste oder Karte. Geben Sie in der BC-Suche (**Suchen**) den Begriff `Buchungsoptionen Einrichtung` ein und wählen Sie den gleichnamigen Link.

### 3. Muss ich die Einrichtung nach dem Setzen speichern oder freigeben?

Nein. Die Werte werden unmittelbar gespeichert. Es gibt keine Freigabe-, Aktivierungs- oder Buchungsaktion auf der Einrichtungsseite; die neue Regel gilt ab dem nächsten Buchungsvorgang.

### 4. Warum kann ich in der Einrichtung keinen zweiten Datensatz anlegen?

Die Einrichtung ist unternehmensweit und existiert genau **einmal** je Mandant. Das Anlegen weiterer Datensätze und das Löschen des vorhandenen sind gesperrt; der einzige Datensatz wird beim ersten Öffnen automatisch erzeugt.

### 5. Warum kann ich beim Warenausgang die Option „Nur Fakturieren“ nicht auswählen?

Das Feld **Warenausgang - Buchungsoptionen** kennt nur **Standard**, **Nur Liefern** und **Nur Liefern und fakturieren**. Eine reine Faktura ist beim Warenausgang fachlich nicht vorgesehen und daher nicht wählbar.

### 6. Warum verhält sich „Liefern“ bei einer Reklamation anders als beim Auftrag?

Die Erweiterung berücksichtigt die Belegart. Beim Auftrag steht „Liefern“ für die reguläre Warenbewegung (Verkauf: Lieferung, Einkauf: Wareneingang), bei der Reklamation für die gegenläufige Bewegung (Verkauf: Wareneingang der Rücknahme, Einkauf: Rücklieferung). Die Menüzeile heißt in beiden Fällen einheitlich **Liefern**.

### 7. Was passiert, wenn ich das Auswahlmenü beim Buchen abbreche?

Wird keine Zeile ausgewählt, bricht der Buchungsvorgang ab und es wird nicht gebucht. Der Beleg bleibt unverändert und kann erneut gebucht werden.

### 8. Gilt die Einschränkung auch für die Aktionen „Buchen und neu“ und „Buchen und senden“?

Ja. Die Erweiterung setzt am Buchungsvorgang selbst an. Unabhängig davon, ob Sie **Buchen**, **Buchen und neu** oder **Buchen und senden** wählen, erscheint die konfigurierte Auswahl.

### 9. Wirkt die Einrichtung nur für bestimmte Anwender oder für alle?

Die Einrichtung gilt **mandantenweit** für alle Anwender. Eine benutzer- oder gruppenbezogene Steuerung der Buchungsoptionen ist nicht vorgesehen.

### 10. Welche Belegarten sind von der Verkaufs- bzw. Einkaufseinstellung betroffen?

Betroffen sind ausschließlich die Belegarten **Auftrag** und **Reklamation** des jeweiligen Bereichs. Andere Belegarten (etwa Angebote oder Rechnungen als eigenständige Belege) werden von der Erweiterung nicht verändert.
