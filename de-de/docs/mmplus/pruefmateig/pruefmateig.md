---
title: Anwenderhandbuch m+m Test Certificate Management with Material Properties
---

# Anwenderhandbuch m+m Test Certificate Management with Material Properties

## Einleitung

Die App **m+m Test Certificate Management with Material Properties** verbindet zwei bestehende m+m-Module: die regelbasierte Prüfungssteuerung aus **m+m Test Certificate Management** und die Eigenschaftsverwaltung aus **m+m Material Properties**. Sie ermöglicht es, in der Prüfungssteuerung nicht nur nach klassischen Belegfeldern zu filtern, sondern nach den **Eigenschaften** der Artikel — abhängig von der **Materialart** oder materialartübergreifend.

Der zentrale Baustein ist ein wiederverwendbarer **Eigenschaftenregelfilter**: eine benannte Zusammenstellung von Bedingungen auf Materialeigenschaften. Dieser Filter wird anschließend in einer **Prüfdatenregel** als Regelfilter hinterlegt. Trifft ein Beleg (z. B. eine Verkaufs-, Einkaufs-, Fertigungs- oder Lagerzeile) auf die dort geforderten Eigenschaftswerte zu, greift die Prüfdatenregel — andernfalls bleibt sie wirkungslos.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwenderinnen und Anwender der Qualitätssicherung** sowie an **Sachbearbeiter im Einkauf, Verkauf und in der Fertigung**, deren Belege durch die Prüfungssteuerung bewertet werden. Sekundär angesprochen sind **Administratoren und Key-User**, die die Nummernserie einrichten, die Eigenschaftenregelfilter pflegen und die Regelbindung in der Prüfdatenregel vornehmen.

**Kurzer Prozessüberblick:**

1. Der Administrator vergibt in der **Prüfdaten Einrichtung** eine Nummernserie für Eigenschaftenregelfilter.
2. Der Key-User legt in der **Eigenschaftenregelfilter-Liste** einen Filter an und definiert in den **Zeilen** je Eigenschaft einen Filterwert.
3. Der Key-User verknüpft den Filter in einer **Prüfdatenregel** über den **Regelfilter** (Feld **Feldfilter**).
4. Im Tagesgeschäft prüft das System bei den betroffenen Belegzeilen automatisch, ob die Eigenschaften des Artikels zum hinterlegten Filter passen, und steuert darüber, ob die Prüfdatenregel ausgelöst wird.

**Abhängigkeiten:** Die App setzt **m+m Test Certificate Management**, **m+m Material Properties** und **m+m Cloud Base** voraus. Die Materialarten und Eigenschaften selbst werden im Modul **m+m Material Properties** gepflegt (**Materialarten**, **Eigenschaftskarte**); dieses Handbuch beschreibt den Zusatznutzen der Verknüpfung, nicht die Grundpflege dieser Stammdaten.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zur wirksamen Regel. Die Reihenfolge folgt der technischen Abhängigkeit: erst die Einrichtung, dann die Stammdaten, zuletzt die Regelbindung.

1. **Nummernserie einrichten.** Öffnen Sie über **Suchen** die **Prüfdaten Einrichtung**. Tragen Sie im Register **Nummerierung** im Feld **Eigenschaftenregelfilternummern** eine Nummernserie ein. Ohne diesen Eintrag lässt sich kein Eigenschaftenregelfilter automatisch nummerieren.
2. **Eigenschaftenregelfilter anlegen.** Öffnen Sie über **Suchen** die **Eigenschaftenregelfilter-Liste** und wählen Sie **Neu**. In der **Eigenschaftenregelfilter Karte** vergeben Sie eine **Beschreibung**, wählen die **Art** und — falls der Filter nur für eine Materialart gelten soll — im Feld **Code** die zugehörige Materialart.
3. **Filterzeilen definieren.** Erfassen Sie im Bereich **Zeilen** je Bedingung eine Zeile: Wählen Sie den **Eigenschaftencode** und hinterlegen Sie im Feld **Filterwert** die geforderte Ausprägung (per AssistEdit unterstützt).
4. **Filter an eine Prüfdatenregel binden.** Öffnen Sie über **Suchen** die **Prüfregeln**, öffnen Sie die gewünschte **Prüfdatenregel** und tragen Sie im **Regelfilter** eine Zeile ein, deren **Tabellen-ID** auf den Eigenschaftsregelfilterkopf verweist; im Feld **Feldfilter** wählen Sie die **Nr.** des angelegten Eigenschaftenregelfilters.

Ab jetzt bewertet das System die betroffenen Belege automatisch. Ein eigener Buchungs- oder Freigabeschritt ist in dieser App nicht erforderlich.

## Einrichtung

Die Einrichtung dieser App ist bewusst schlank: Sie benötigen genau **eine** Nummernserie, die passenden **Berechtigungen** und anschließend die Pflege der Eigenschaftenregelfilter (siehe Abschnitt **Stammdaten**). Alle weiteren Steuerungen erfolgen über die einzelnen Filter und deren Bindung in der Prüfdatenregel.

### Prüfdaten Einrichtung — Register Nummerierung

**Prozessintro.** Diese Einrichtung nimmt der **Administrator** einmalig **vor der ersten Nutzung** vor. Die **Prüfdaten Einrichtung** ist eine unternehmensweite Einrichtungskarte (ein Datensatz je Mandant). Das durch diese App ergänzte Feld steht im vorhandenen Register **Nummerierung**, gemeinsam mit den übrigen Nummernserien der Prüfungssteuerung. Anwender greifen die hier vergebene Nummernserie später beim Anlegen jedes Eigenschaftenregelfilters auf (Cross-Link: Abschnitt **Stammdaten**).

**Einstieg:** Öffnen Sie über **Suchen** die **Prüfdaten Einrichtung** und wechseln Sie in das Register **Nummerierung**.

Die BC-Anwenderin sieht in diesem Register alle Nummernserien der Prüfungssteuerung auf einer Seite. Die folgende Tabelle dokumentiert das gesamte Register **Nummerierung** (Basisfelder des Grundmoduls und das durch diese App ergänzte Feld):

| Einrichtung | Erläuterung |
|---|---|
| **Prüfvorlagennummernserie** | Wenn hier eine Nummernserie gesetzt ist, dann erhalten neu angelegte Prüfvorlagen automatisch eine fortlaufende Nummer aus dieser Serie; ohne Eintrag muss die Nummer manuell vergeben werden. |
| **Prüfungsnummernserie** | Wenn gesetzt, dann werden neu erzeugte Prüfungen automatisch aus dieser Serie nummeriert — Voraussetzung dafür, dass die Prüfungssteuerung Prüfungen ohne manuelle Nummernvergabe erzeugen kann. |
| **Probennummern** | Wenn gesetzt, dann erhalten Proben zu einer Prüfung automatisch eine eindeutige Nummer aus dieser Serie; das sichert die Rückverfolgbarkeit einzelner Proben. |
| **Prüfungsregelnummern** | Wenn gesetzt, dann werden neue Prüfdatenregeln automatisch aus dieser Serie nummeriert; die Regeln bleiben dadurch eindeutig referenzierbar. |
| **Eigenschaftenregelfilternummern** | Wenn hier eine Nummernserie hinterlegt ist, dann vergibt das System beim Anlegen eines neuen Eigenschaftenregelfilters automatisch die nächste Nummer dieser Serie. Ist das Feld leer, dann verweigert das System das Anlegen und fordert eine manuelle Nummer bzw. eine gültige Serie an — die Pflege von Eigenschaftenregelfiltern (Abschnitt **Stammdaten**) ist also erst nach diesem Eintrag möglich. |

> Hinweis zum Umfang: Die **Prüfdaten Einrichtung** enthält weitere Register, die zum Grundmodul **m+m Test Certificate Management** gehören und dort dokumentiert sind. Für diese App ist ausschließlich das Feld **Eigenschaftenregelfilternummern** im Register **Nummerierung** relevant; es wird hier vollständig im Kontext des Registers erläutert.

### Berechtigungen

**Prozessintro.** Bevor Anwender Eigenschaftenregelfilter anlegen oder bearbeiten dürfen, weist der Administrator die passende Berechtigung zu. Die App liefert dafür einen zuweisbaren Berechtigungssatz mit.

Der Berechtigungssatz **MuM TCMP All** legt fest, welche Aktionen Anwenderinnen und Anwender auf den Objekten dieser App ausführen dürfen: Er umfasst das vollständige Lesen und Bearbeiten (Anlegen, Ändern, Löschen) des Eigenschaftsregelfilterkopfes und der Eigenschaftsregelfilterzeilen sowie die Ausführungsrechte für die zugehörigen Seiten und die Regelauswertung. Wenn Sie diesen Satz einem Anwender zuweisen, dann kann dieser Eigenschaftenregelfilter pflegen und die App-Funktionen nutzen; ohne diese Zuweisung bleiben die Seiten und die regelbasierte Auswertung für den Anwender gesperrt.

### Eigenschaftenregelfilter einrichten

**Prozessintro.** Dies ist die durchgängige Freischaltung der einzigen fachlichen Fähigkeit dieser App. Sie betrifft mehrere Seiten und wird deshalb hier als zusammenhängender Ablauf beschrieben. Konfiguriert wird durch **Administrator** (Nummernserie, Berechtigung) und **Key-User** (Filterpflege, Regelbindung), einmalig vor der produktiven Nutzung und danach bei Bedarf. Verwendet wird die Einstellung anschließend im Tagesgeschäft durch die automatische Bewertung der Belegzeilen (Cross-Link: Abschnitt **Regelbindung in der Prüfdatenregel**).

**Enablement-Schritte in Abhängigkeitsreihenfolge:**

1. **Nummernserie hinterlegen.** Tragen Sie in der **Prüfdaten Einrichtung** im Register **Nummerierung** das Feld **Eigenschaftenregelfilternummern** ein. Wenn dieser Schritt fehlt, dann lässt sich in Schritt 3 kein Filter anlegen.
2. **Berechtigung zuweisen.** Weisen Sie den Berechtigungssatz **MuM TCMP All** zu. Wenn die Berechtigung fehlt, dann sind die folgenden Seiten für den Anwender nicht bearbeitbar.
3. **Eigenschaftenregelfilter anlegen und Zeilen pflegen.** Legen Sie in der **Eigenschaftenregelfilter-Liste** den Filter an und definieren Sie in den **Zeilen** die Eigenschaftsbedingungen (Details im Abschnitt **Stammdaten**). Wenn mindestens eine Zeile einen **Filterwert** trägt, dann ist der Filter auswertbar.
4. **Filter in der Prüfdatenregel binden.** Verknüpfen Sie den Filter im **Regelfilter** einer **Prüfdatenregel** (Feld **Feldfilter**). Erst mit dieser Bindung wirkt der Filter im Tagesgeschäft.

**Operative Abschluss-Aktion:** Es ist keine gesonderte Buchungs- oder Freigabeaktion nötig. Sobald die Bindung in Schritt 4 gespeichert ist, wertet die Prüfungssteuerung die betroffenen Belegzeilen automatisch aus (Cross-Link: Abschnitt **Regelbindung in der Prüfdatenregel**).

## Stammdaten

Die einzige eigene Stammdatenkategorie dieser App ist der **Eigenschaftenregelfilter**. Er besteht aus einem Kopf (Eigenschaftsregelfilterkopf) und beliebig vielen Zeilen (Eigenschaftsregelfilterzeile).

### Eigenschaftenregelfilter — Liste und Karte

**Prozessintro.** Diese Stammdaten pflegt der **Key-User** nach der Grundeinrichtung, laufend bei neuen Anforderungen der Qualitätssicherung. Ein Filter bündelt die Eigenschaftsbedingungen, die später eine Prüfdatenregel auslösen sollen. Die Werte erscheinen im Tagesgeschäft nicht auf dem Beleg, sondern wirken im Hintergrund über die Regelbindung (Cross-Link: Abschnitt **Regelbindung in der Prüfdatenregel**).

**Einstieg:** Öffnen Sie über **Suchen** die **Eigenschaftenregelfilter-Liste**. Über **Neu** legen Sie einen neuen Datensatz an; ein vorhandener Eintrag öffnet sich per Doppelklick in der **Eigenschaftenregelfilter Karte**. Die Liste selbst ist nicht editierbar und dient der Übersicht; die Pflege erfolgt auf der Karte.

Die **Eigenschaftenregelfilter-Liste** zeigt je Zeile die Kopfdaten eines Filters. Sie enthält keine gesonderten Filterfelder in der Anfragezeile; die Übersicht wird über die Standard-Suche und -Sortierung von Business Central eingegrenzt.

**Kopffelder (Liste und Register Allgemein der Karte):**

| Feld | Erläuterung |
|---|---|
| **Nr.** | Eindeutige Nummer des Eigenschaftenregelfilters. Wenn das Feld beim Anlegen leer bleibt, dann zieht das System automatisch die nächste Nummer aus der in **Eigenschaftenregelfilternummern** hinterlegten Serie; diese Nr. ist der Wert, den Sie später in der Prüfdatenregel im **Feldfilter** referenzieren. |
| **Art** | Legt fest, worauf sich die Filterbedingungen beziehen. Zulässige Werte: <br>**Eigenschaft:** Der Filter bewertet Materialeigenschaften des Artikels. Wenn diese Art gewählt ist, dann werden die in den **Zeilen** hinterlegten Eigenschaftswerte gegen die Eigenschaften des Artikels der Belegzeile geprüft. (Die Art ist erweiterbar; in dieser App steht ausschließlich der Wert **Eigenschaft** zur Verfügung.) |
| **Code** | Grenzt den Filter optional auf eine **Materialart** ein (Auswahl aus den Materialarten). Wenn hier eine Materialart gesetzt ist, dann greift der Filter nur für Artikel dieser Materialart und die erfassbaren Eigenschaften beschränken sich auf die dieser Materialart zugewiesenen; bleibt das Feld leer, dann gilt der Filter materialartübergreifend für alle Artikel, denen die jeweilige Eigenschaft zugewiesen ist. |
| **Beschreibung** | Freitext zur Benennung des Filters. Wenn eine sprechende Beschreibung gepflegt ist, dann finden Key-User den passenden Filter bei der Regelbindung schneller wieder; der Wert hat keine steuernde Wirkung. |

> Zum Feld **Code**: Das System prüft die Zuordnung erst inhaltlich, wenn Sie eine Zeile erfassen (siehe unten). Eine leere **Nr.** verhindert das Speichern des Codes, da der Filterkopf zuerst eine gültige Nummer benötigt.

### Zeilen des Eigenschaftenregelfilters

**Prozessintro.** In den **Zeilen** hinterlegt der Key-User die eigentlichen Bedingungen — je Zeile eine Eigenschaft mit dem geforderten Filterwert. Alle Zeilen eines Filters wirken zusammen: Ein Artikel erfüllt den Filter nur, wenn er **jede** Zeile erfüllt (Und-Verknüpfung).

Der Bereich **Zeilen** wird direkt auf der **Eigenschaftenregelfilter Karte** unterhalb der Kopfdaten angezeigt.

| Feld | Erläuterung |
|---|---|
| **Eigenschaftencode** | Wählt die zu prüfende Eigenschaft (Auswahl aus den Eigenschaften des Moduls m+m Material Properties). Wenn ein Code gewählt wird, dann prüft das System sofort, ob diese Eigenschaft überhaupt zugewiesen ist: Ist am Kopf eine **Materialart** (Feld **Code**) gesetzt, muss die Eigenschaft dieser Materialart zugewiesen sein; ist keine Materialart gesetzt, muss die Eigenschaft mindestens einer Materialart zugewiesen sein. Andernfalls meldet das System „Die Eigenschaft … ist nicht zugewiesen." und verweigert die Zeile. |
| **Eigenschaftenname** | Zeigt den Namen zur gewählten Eigenschaft an (wird automatisch nachgeschlagen). Wenn Sie den Eigenschaftencode ändern, dann aktualisiert sich der Name entsprechend; das Feld ist nicht bearbeitbar und dient der Lesbarkeit. |
| **Filterwert** | Die geforderte Ausprägung der Eigenschaft, gegen die der Artikel geprüft wird. Wenn ein Filterwert gesetzt ist, dann muss die betreffende Eigenschaft des Artikels diesen Wert (bzw. Wertebereich) erfüllen, damit der Filter zutrifft. Über die AssistEdit-Funktion öffnet sich eine Auswahlhilfe: Nutzt die Eigenschaft feste **Eigenschaftswerte**, dann wählen Sie aus diesen Werten; andernfalls stellen Sie einen Filterausdruck zusammen. Das Feld darf nicht leer bleiben — leere Zeilen werden bei der Auswertung nicht berücksichtigt und beim Verlassen der Zeilen erzwingt das System einen Wert. Ändern Sie den **Eigenschaftencode** einer Zeile, dann wird der bisherige **Filterwert** zurückgesetzt. |

**Validierung und Abhängigkeiten:** Beim Verlassen der Zeilen prüft das System, dass jede Zeile einen **Filterwert** trägt. Ein **Filterwert** ohne **Eigenschaftencode** ist nicht möglich; das System verlangt zuerst die Eigenschaft. Wird der Filterkopf gelöscht, dann werden alle zugehörigen Zeilen automatisch mitgelöscht.

## Regelbindung in der Prüfdatenregel

Dieser Abschnitt beschreibt, **wie** der eingerichtete Eigenschaftenregelfilter im Tagesgeschäft wirkt. Die Wirkung entsteht nicht auf einer eigenen Seite dieser App, sondern über die **Prüfdatenregel** des Grundmoduls, die durch diese App um die Auswertung von Materialeigenschaften erweitert wird.

**Steuernde Seiten:** Die Auswertung wird durch die **Eigenschaftenregelfilter** (Stammdaten dieser App, Abschnitt **Stammdaten**) und durch die **Prüfdaten Einrichtung** (Nummernserie, Abschnitt **Einrichtung**) vorbereitet und in der **Prüfdatenregel** über den **Regelfilter** aktiviert. Der Administrator/Key-User konfiguriert dort die Bindung; die operative Auswertung läuft danach ohne Anwendereingriff.

### Filter in einer Prüfdatenregel hinterlegen

**Einstieg:** Öffnen Sie über **Suchen** die **Prüfregeln**, öffnen Sie die gewünschte **Prüfdatenregel** und wechseln Sie in den Bereich **Regelfilter**.

Erfassen Sie im **Regelfilter** eine Zeile und setzen Sie im Feld **Tabellen-ID** die Tabelle des Eigenschaftsregelfilterkopfes. Das Feld **Verbundene Tabellen-ID** zeigt daraufhin die verknüpfte Tabelle an. Im Feld **Feldfilter** hinterlegen Sie die **Nr.** des zuvor angelegten Eigenschaftenregelfilters. Wenn diese Bindung gespeichert ist, dann bezieht die Prüfdatenregel bei ihrer Auswertung die Eigenschaftsbedingungen des Filters mit ein.

| Feld (Regelfilter) | Erläuterung |
|---|---|
| **Tabellen-ID** | Bestimmt, worauf sich die Filterzeile bezieht. Wenn Sie hier den Eigenschaftsregelfilterkopf wählen, dann aktivieren Sie für diese Regel die eigenschaftsbasierte Auswertung dieser App. |
| **Verbundene Tabellen-ID** | Zeigt die zur Tabellen-ID gehörende verbundene Tabelle. Wenn diese auf den Eigenschaftsregelfilterkopf verweist, dann erkennt die Auswertung, dass ein Eigenschaftenregelfilter anzuwenden ist (das Feld ist nicht bearbeitbar). |
| **Feldfilter** | Nimmt die **Nr.** des anzuwendenden Eigenschaftenregelfilters auf. Wenn hier eine Filternummer steht, dann prüft das System für jeden betroffenen Beleg genau die in diesem Filter definierten Eigenschaftsbedingungen. |

### Welche Belege ausgewertet werden

Die App klinkt sich in die Auswertung der Prüfdatenregel ein und bewertet den Artikel der jeweiligen Belegzeile. Bei der Installation registriert die App automatisch die folgenden Belegarten als auswertbare Quellen; für den Anwender bedeutet das, dass die eigenschaftsbasierte Regel auf diesen Zeilen greifen kann:

- Verkaufszeilen und Einkaufszeilen (jeweils nur bei Zeilen des Typs Artikel),
- Fertigungsauftragszeilen, Fertigungsauftragskomponenten und Fertigungsauftrags-Arbeitsgangzeilen,
- Kommissionierzeilen (Lageraktivitätszeilen),
- Wareneingangszeilen und Warenausgangszeilen,
- Umlagerungszeilen.

Für jede dieser Zeilen ermittelt das System die **Materialart** des Artikels und vergleicht die Eigenschaften des Artikels mit den Zeilen des Eigenschaftenregelfilters.

### Wie die Auswertung entscheidet

Die Entscheidung folgt einer klaren Logik, die der Anwender kennen sollte, um Filter richtig aufzubauen:

1. Das System liest alle Zeilen des im **Feldfilter** referenzierten Eigenschaftenregelfilters, die einen **Filterwert** tragen.
2. Ist am Filterkopf eine **Materialart** (Feld **Code**) gesetzt, dann greift der Filter nur, wenn der Artikel der Belegzeile genau dieser Materialart angehört; ist keine Materialart gesetzt, dann gilt der Filter unabhängig von der Materialart.
3. Für jede Filterzeile prüft das System, ob die entsprechende Eigenschaft des Artikels den geforderten **Filterwert** erfüllt.
4. Nur wenn **alle** Filterzeilen erfüllt sind, gilt der Filter als zutreffend und die Prüfdatenregel wird ausgelöst; scheitert auch nur eine Zeile, dann bleibt die Regel für diesen Beleg wirkungslos.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Einsatz der App entlang realistischer Auslöser. Alle Schritte beziehen sich auf die in diesem Handbuch beschriebenen, im Code hinterlegten Seiten und Abläufe.

### Anwendungsfall 1: Neue Prüfvorgabe für eine Materialart

**Auslöser:** Die Qualitätssicherung meldet intern, dass Artikel einer bestimmten Materialart künftig nur dann eine Prüfung erhalten sollen, wenn eine bestimmte Materialeigenschaft einen definierten Wert aufweist.

**Einstieg in BC:** Der Key-User öffnet über **Suchen** die **Eigenschaftenregelfilter-Liste** und legt über **Neu** einen Filter an.

**Kernablauf:** In der **Eigenschaftenregelfilter Karte** vergibt der Key-User eine **Beschreibung**, belässt die **Art** auf **Eigenschaft** und wählt im Feld **Code** die betroffene Materialart. Im Bereich **Zeilen** erfasst er eine Zeile mit dem passenden **Eigenschaftencode** und trägt im **Filterwert** die geforderte Ausprägung ein (per AssistEdit). Danach öffnet er über **Suchen** die **Prüfregeln**, wählt die zuständige **Prüfdatenregel** und hinterlegt im **Regelfilter** eine Zeile mit der **Tabellen-ID** des Eigenschaftsregelfilterkopfes und der **Nr.** des neuen Filters im **Feldfilter**.

**Abschluss:** Es ist kein Buchungsschritt nötig. Ab sofort löst die Prüfdatenregel bei Artikeln dieser Materialart nur dann aus, wenn die geforderte Eigenschaft den Filterwert erfüllt.

### Anwendungsfall 2: Prüfung nur bei passender Eigenschaft im Einkauf

**Auslöser:** Beim Wareneingang zu einer Bestellung soll für einen Artikel nur dann eine Prüfung angestoßen werden, wenn eine sicherheitsrelevante Eigenschaft einen bestimmten Wert hat.

**Einstieg in BC:** Der Key-User verwendet einen bestehenden oder neuen Eigenschaftenregelfilter (Abschnitt **Stammdaten**) und bindet ihn wie in Anwendungsfall 1 an die zuständige **Prüfdatenregel**.

**Kernablauf:** Der Einkaufssachbearbeiter erfasst wie gewohnt die Bestellung mit einer Einkaufszeile des Typs Artikel. Beim Wareneingang bewertet die Prüfungssteuerung die Wareneingangszeile bzw. die zugrunde liegende Einkaufszeile: Das System ermittelt die **Materialart** des Artikels und vergleicht dessen Eigenschaften mit dem gebundenen Eigenschaftenregelfilter. Erfüllt der Artikel den Filter, greift die Prüfdatenregel; andernfalls bleibt der Wareneingang ohne zusätzliche Prüfung.

**Abschluss:** Der Sachbearbeiter bucht den Wareneingang mit dem BC-Standardprozess. Die eigenschaftsbasierte Steuerung erfolgt automatisch im Hintergrund; ein eigener Bedienschritt der App entfällt.

### Anwendungsfall 3: Filterwert komfortabel über die Auswahlhilfe pflegen

**Auslöser:** Ein Key-User möchte einen bestehenden Eigenschaftenregelfilter verfeinern und ist sich beim korrekten Wert einer Eigenschaft unsicher.

**Einstieg in BC:** Über **Suchen** öffnet der Key-User die **Eigenschaftenregelfilter-Liste** und darin den betreffenden Filter.

**Kernablauf:** Im Bereich **Zeilen** wählt er die Zeile der gewünschten Eigenschaft und ruft im Feld **Filterwert** die AssistEdit-Funktion auf. Nutzt die Eigenschaft feste **Eigenschaftswerte**, dann wählt er den Wert aus der angebotenen Liste; andernfalls stellt er über die Auswahlhilfe einen Filterausdruck zusammen. Das System übernimmt das Ergebnis als **Filterwert**.

**Abschluss:** Beim Verlassen der Zeilen prüft das System, dass jede Zeile einen **Filterwert** trägt. Der angepasste Filter wirkt ohne weiteren Schritt in allen Prüfdatenregeln, in denen seine **Nr.** hinterlegt ist.

## FAQ und Troubleshooting

### Warum kann ich keinen neuen Eigenschaftenregelfilter anlegen?

Weil in der **Prüfdaten Einrichtung** im Register **Nummerierung** das Feld **Eigenschaftenregelfilternummern** leer ist. Das System benötigt beim Anlegen entweder eine gültige Nummernserie oder eine manuell eingegebene Nummer. Tragen Sie die Nummernserie ein, dann lassen sich neue Filter automatisch nummerieren.

### Warum erscheint die Meldung „Die Eigenschaft … ist nicht zugewiesen."?

Weil der in der Zeile gewählte **Eigenschaftencode** der ausgewählten Konstellation nicht zugewiesen ist. Ist am Kopf im Feld **Code** eine **Materialart** gesetzt, muss die Eigenschaft dieser Materialart zugewiesen sein; ist keine Materialart gesetzt, muss die Eigenschaft mindestens einer Materialart zugewiesen sein. Weisen Sie die Eigenschaft in m+m Material Properties zu oder wählen Sie eine passende Eigenschaft.

### Warum lässt sich die Karte nicht über die Suche öffnen?

Die **Eigenschaftenregelfilter Karte** ist bewusst nicht direkt über **Suchen** erreichbar. Öffnen Sie stattdessen die **Eigenschaftenregelfilter-Liste** über **Suchen** und darin den gewünschten Datensatz; die Karte öffnet sich aus der Liste heraus.

### Warum kann ich in der Eigenschaftenregelfilter-Liste keine Werte ändern?

Weil die Liste nicht editierbar ist und nur der Übersicht dient. Alle Änderungen nehmen Sie in der **Eigenschaftenregelfilter Karte** vor, die Sie per Doppelklick aus der Liste öffnen.

### Warum wird meine Prüfdatenregel trotz passendem Artikel nicht ausgelöst?

Prüfen Sie drei Punkte: Erstens muss in der **Prüfdatenregel** im **Regelfilter** die **Nr.** des Filters korrekt im **Feldfilter** stehen. Zweitens muss die **Materialart** am Filterkopf (Feld **Code**) zum Artikel passen — oder leer sein. Drittens müssen **alle** Filterzeilen erfüllt sein; scheitert eine Zeile, greift die Regel nicht.

### Warum genügt es nicht, wenn nur eine von mehreren Filterzeilen zutrifft?

Weil die Zeilen eines Eigenschaftenregelfilters mit „Und" verknüpft sind. Der Artikel muss jede Zeile erfüllen. Möchten Sie eine „Oder"-Logik, dann verteilen Sie die Bedingungen auf mehrere Filter und binden Sie diese an separate Prüfdatenregeln.

### Warum wird mein Filterwert beim Ändern der Eigenschaft geleert?

Weil der **Filterwert** immer zu einem bestimmten **Eigenschaftencode** gehört. Ändern Sie den Eigenschaftencode einer Zeile, dann setzt das System den bisherigen Filterwert zurück, damit kein zur alten Eigenschaft passender Wert versehentlich stehen bleibt. Erfassen Sie den Filterwert danach neu.

### Warum kann ich die Zeilen nicht verlassen?

Weil mindestens eine Zeile keinen **Filterwert** enthält. Das System erzwingt beim Verlassen der Zeilen, dass jede erfasste Zeile einen Filterwert trägt. Ergänzen Sie den Wert oder löschen Sie die leere Zeile.

### Warum wirkt der Filter materialartübergreifend, obwohl ich das nicht wollte?

Weil am Filterkopf das Feld **Code** (Materialart) leer geblieben ist. Ohne Materialart gilt der Filter für alle Artikel, denen die jeweilige Eigenschaft zugewiesen ist. Tragen Sie im Feld **Code** die gewünschte **Materialart** ein, dann beschränkt sich der Filter auf diese.

### Auf welchen Belegen wirkt die eigenschaftsbasierte Auswertung überhaupt?

Auf den bei der Installation registrierten Belegarten: Verkaufs- und Einkaufszeilen (Typ Artikel), Fertigungsauftragszeilen, Fertigungsauftragskomponenten und Arbeitsgangzeilen, Kommissionierzeilen, Wareneingangs- und Warenausgangszeilen sowie Umlagerungszeilen. Auf anderen Belegen wird der Eigenschaftenregelfilter nicht ausgewertet.
