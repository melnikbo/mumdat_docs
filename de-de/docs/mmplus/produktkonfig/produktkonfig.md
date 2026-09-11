---
title: Anwenderhandbuch m+m Product Configurator
---

# Anwenderhandbuch m+m Product Configurator

## Einleitung

Der **Produktkonfigurator** ermöglicht es, in einem Verkaufs-, Einkaufs- oder Fertigungsbeleg einen
passenden Artikel anhand von Materialeigenschaften zu bestimmen oder – falls kein passender Artikel
existiert – automatisch anzulegen. Statt eine Artikelnummer aus dem Kopf zu kennen, wählt der Anwender in
der Belegzeile eine **Materialart** aus, gibt die gewünschten Eigenschaftswerte ein (z. B. Durchmesser,
Werkstoff, Länge) und erhält daraufhin den dazu passenden Artikel samt Variante zurück in die Zeile.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender**, die täglich Belegzeilen
erfassen – Innendienst im Verkauf und Einkauf sowie Anwender in der Fertigungsvorbereitung (Erfassung von
Fertigungsstücklistenzeilen). Sekundär angesprochen sind **Administratoren und Stammdatenverantwortliche**,
die die Materialarten, Eigenschaftskategorien, Sichtbarkeitsregeln und Textvorlagen einrichten, bevor der
Konfigurator genutzt werden kann.

**Kurzer Prozessüberblick.** Der Ablauf folgt einer festen Kette:

1. Eine **Materialart** wird auf der **Materialartenkarte** im Register **Produktkonfigurator** aktiviert
   und für bestimmte Belegarten freigegeben.
2. Den Eigenschaften der Materialart werden über **Produktkonfiguratorkategorien** Kategorien und eine
   Reihenfolge zugeordnet; genau eine Kategorie ist die **Hauptkategorie**.
3. Optional werden **Sichtbarkeitsregeln**, **erweiterte Texte** und ein **Regelablauf** eingerichtet.
4. Im Beleg füllt der Anwender in der Zeile das Feld **Produktkonfigurator-Materialart**; daraufhin öffnet
   sich der Dialog **Produktkonfigurator**, in dem die Eigenschaftswerte erfasst werden.
5. Beim Verlassen mit **OK** sucht das System einen passenden Artikel bzw. legt einen neuen Artikel über
   die hinterlegte Artikelvorlage an und schreibt Artikel und Variante in die Belegzeile zurück.

Dieses Modul bucht selbst nichts und erzeugt keine Historienbelege; es ergänzt die Belegerfassung um die
eigenschaftsbasierte Artikelfindung und -anlage.

---

## Schnellstart für Anwender

Die Reihenfolge folgt der technischen Abhängigkeit: erst Einrichtung, dann die tägliche Nutzung.

**Einrichtung (einmalig durch Administrator/Stammdatenverantwortliche):**

1. **Materialarten** öffnen (über **Suchen**), die gewünschte Materialart auswählen und die
   **Materialartenkarte** öffnen. Im Register **Produktkonfigurator** das Feld
   **Verwendet für Produktkonfigurator** aktivieren, einen **Artikelvorlagencode** hinterlegen, die
   **Suchoption** wählen und die Belegarten (**Verkaufsauftrag**, **Verkaufsangebot**, … ) ankreuzen, in
   denen der Konfigurator genutzt werden darf.
2. Auf der Materialartenkarte über **Zugehörig -> Produktkonfiguratorkategorien** die Ansicht
   **Materialeigenschaften-Kategorienzuordnungen** öffnen und mindestens eine Kategorie mit
   **Reihenfolge 0** (Hauptkategorie) anlegen sowie den Eigenschaften Kategorien zuordnen.
3. In der Eigenschaftentabelle der Materialartenkarte die benötigten Eigenschaften als **Erforderlich**
   kennzeichnen und ggf. **Darstellungsarten** setzen.

**Tägliche Nutzung (Anwender):**

1. Belegzeile erfassen (z. B. im **Verkaufsauftrag**) und in der Zeile das Feld
   **Produktkonfigurator-Materialart** auswählen.
2. Im geöffneten Dialog **Produktkonfigurator** die Eigenschaftswerte in der Hauptkategorie und in den
   weiteren **Kategorien** eingeben.
3. In der Infobox **Nicht gefüllte Pflichtfelder** prüfen, ob noch **Pflichtfelder** offen sind.
4. Mit **OK** bestätigen: Das System findet oder erstellt den Artikel und übernimmt Artikel und Variante
   in die Belegzeile. **Abbrechen** verwirft alle Eingaben.

---

## Einrichtung

Die Einrichtung ist der umfangreichste Teil dieses Moduls und die Voraussetzung für jede spätere Nutzung.
Alle folgenden Einrichtungsseiten werden über die **Materialartenkarte** (Basismodul m+m Materialarten)
erreicht, nicht über die globale **Suchen**-Funktion. Ist eine der zugehörigen Aktionen ausgegraut, ist in
der Regel auf der Materialartenkarte das Feld **Verwendet für Produktkonfigurator** noch nicht aktiviert.

### Produktkonfigurator für eine Materialart einrichten

**Einstieg:** **Materialarten** (über **Suchen**) -> Zeile auswählen -> **Materialartenkarte** ->
Register **Produktkonfigurator**.

**Prozessintro.** Diese Einrichtung führt der Administrator bzw. Stammdatenverantwortliche einmalig je
Materialart durch, bevor der Konfigurator zum ersten Mal in einem Beleg genutzt wird. Sie legt fest, ob
eine Materialart überhaupt konfigurierbar ist, mit welcher Vorlage neue Artikel entstehen, wie gesucht wird
und in welchen Belegarten der Konfigurator erscheint. Die hier gesetzten Kennzeichen steuern unmittelbar,
ob das Feld **Produktkonfigurator-Materialart** in der jeweiligen Belegzeile die Materialart überhaupt zur
Auswahl anbietet (siehe **Tägliche Arbeit im Produktkonfigurator**).

| Einrichtung | Erläuterung |
|---|---|
| **Verwendet für Produktkonfigurator** | Wenn aktiviert, ist die Materialart konfigurierbar: Erst dann lassen sich Belegarten, Artikelvorlage und Suchoption pflegen und die Aktionen **Produktkonfiguratorkategorien**, **Sichtbarkeit von Eigenschaften und Kategorien** sowie **Produktkonfigurator Regelwerk** aufrufen. Wenn deaktiviert, werden alle Belegkennzeichen zurückgesetzt; das Deaktivieren ist gesperrt, solange zu dieser Materialart Einträge unter **Sichtbarkeit von Eigenschaften und Kategorien** bestehen. |
| **Artikelvorlagencode** | Wenn gesetzt, verwendet der Konfigurator diese Konfigurationsvorlage, um einen neuen Artikel anzulegen, sobald zu den eingegebenen Eigenschaften kein Artikel gefunden wird. Ohne Artikelvorlage ist keine automatische Artikelanlage möglich – der Konfigurator kann dann nur bereits vorhandene Artikel finden. Die Vorlage muss aktiviert sein. |
| **Suchoption** | Legt fest, welche Eigenschaften bei der Artikelsuche geprüft werden. **Eindeutige Suche:** Es werden alle eingegebenen Eigenschaften geprüft; wird kein Treffer gefunden, legt das System direkt einen neuen Artikel über die Artikelvorlage an. **Nur fixe Merkmale suchen:** Es werden nur die Eigenschaften geprüft, die im Register **Allgemein** der Eigenschaftentabelle das Kennzeichen **Fix** gesetzt haben; **Verkaufseigenschaft** und **Einkaufseigenschaft** bleiben bei dieser Suche unberücksichtigt. Diese Option kann nicht gesetzt werden, wenn zu nicht-fixen Eigenschaften ein **Standardwert** hinterlegt ist. |
| **Verkaufsangebot** | Wenn aktiviert, steht der Konfigurator in Verkaufsangebotszeilen zur Verfügung; das Feld **Produktkonfigurator-Materialart** bietet die Materialart dort zur Auswahl an. Nur setzbar, wenn **Verwendet für Produktkonfigurator** aktiv ist. |
| **Rahmenauftrag** | Wenn aktiviert, ist der Konfigurator in Verkaufsrahmenauftragszeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |
| **Verkaufsauftrag** | Wenn aktiviert, ist der Konfigurator in Verkaufsauftragszeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |
| **Einkaufsanfrage** | Wenn aktiviert, ist der Konfigurator in Einkaufsanfragezeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |
| **Rahmenbestellung** | Wenn aktiviert, ist der Konfigurator in Einkaufsrahmenbestellungszeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |
| **Einkaufsbestellung** | Wenn aktiviert, ist der Konfigurator in Einkaufsbestellungszeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |
| **Fertigungsauftrag** | Wenn aktiviert, ist der Konfigurator in Fertigungsauftragszeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |
| **Fertigungsstückliste** | Wenn aktiviert, ist der Konfigurator in Fertigungsstücklistenzeilen nutzbar. Nur setzbar bei aktivem **Verwendet für Produktkonfigurator**. |

**Einrichtungsschritte in Abhängigkeitsreihenfolge:**

1. **Zuerst** **Verwendet für Produktkonfigurator** aktivieren – ohne dieses Kennzeichen sind alle
   weiteren Felder und Aktionen gesperrt.
2. **Danach** einen **Artikelvorlagencode** hinterlegen, damit bei fehlendem Treffer ein neuer Artikel
   entstehen kann.
3. **Anschließend** die **Suchoption** wählen und die benötigten Belegarten aktivieren.
4. **Schließlich** die Eigenschaften Kategorien zuordnen (siehe nächster Abschnitt) – dies ist zwingend,
   da im Konfigurator nur kategorisierte Eigenschaften erscheinen.

> Hinweis: Eine korrekt eingerichtete Materialart ist unerlässlich für die Funktion des Konfigurators. Es
> empfiehlt sich, alle Eigenschaften als **Erforderlich** zu kennzeichnen, deren Werte in der
> **Artikelbeschreibungsformel** oder in der Matchcodeformel verwendet werden.

### Kategorien und Reihenfolge einrichten

**Einstieg:** **Materialartenkarte** -> **Zugehörig -> Produktkonfiguratorkategorien** ->
**Materialeigenschaften-Kategorienzuordnungen**.

**Prozessintro.** Hier legt der Administrator fest, in welcher **Reihenfolge** und unter welchem
**Kategoriencode** die Eigenschaften einer Materialart im Konfigurator erscheinen. Genau eine Kategorie je
Materialart ist die **Hauptkategorie** (Reihenfolge 0); ihre Eigenschaften werden im Konfigurator im
oberen linken Bereich angezeigt. Die Reihenfolge ist besonders bei Regelverwendung wichtig, da abhängige
Eigenschaften zum richtigen Zeitpunkt bekannt sein müssen. Diese Einrichtung wird im Dialog
**Produktkonfigurator** (siehe **Tägliche Arbeit**) unmittelbar wirksam.

| Feld | Erläuterung |
|---|---|
| **Reihenfolge** | Wenn gesetzt, bestimmt der Wert die Anzeigeposition der Kategorie im Konfigurator. **Reihenfolge 0** definiert die **Hauptkategorie** und ist zwingend erforderlich; je Materialart darf die 0 nur einmal vergeben werden. |
| **Kategoriencode** | Wenn gewählt, ordnet der Wert die Zeile einer Eigenschaftskategorie zu; nur Eigenschaften mit Kategoriencode erscheinen im Konfigurator. Der Code wird aus den Eigenschaftskategorien ausgewählt oder über **+Neu** neu angelegt (sprechende Codes wie „ABMESSUNG" erleichtern die Zuordnung). |
| **Kategoriebeschreibung** | Zeigt die Beschreibung der gewählten Kategorie; wird automatisch aus dem Kategoriencode abgeleitet und dient der Orientierung in der Liste. |
| **Materialartencode** | Wenn gesetzt, ordnet der Wert die Zuordnung der jeweiligen Materialart zu; bei neuen Zeilen ist er aus dem Aufrufkontext bereits vorbelegt. |
| **Eigenschaftsname** | Zeigt die Bezeichnung der Materialart an und dient als Beschriftung in der Liste. |
| **Hauptkategorie** | Zeigt an, ob die Zeile die Hauptkategorie ist (Reihenfolge 0). Die Hauptkategorie wird im Konfigurator nicht als eigene Kategorie geführt; ihre Eigenschaften erscheinen direkt im ersten Bereich. |

**Aktionen auf dieser Seite:**

- **Hauptkategorie anlegen:** Wenn ausgeführt, legt die Aktion eine Zeile mit Reihenfolge 0 für die
  aktuelle Materialart an. Sie ist nur verfügbar, solange noch keine Hauptkategorie existiert.
- **Erweiterte Texte:** Öffnet das **Erw. Textzuordnungsarbeitsblatt** für die Materialart (siehe
  Abschnitt *Erweiterte Texte je Materialart und Kategorie einrichten*).

**Enablement-Schritte:** Zuerst mit **Hauptkategorie anlegen** die Reihenfolge 0 erzeugen, danach den
übrigen Eigenschaften über neue Zeilen Kategoriencodes und aufsteigende Reihenfolgen zuweisen. Beim
Verlassen der Seite prüft das System, dass eine Hauptkategorie vorhanden ist, und weist andernfalls darauf
hin. Massenzuordnungen sind über die Eigenschaftentabelle möglich (siehe **Stammdaten**).

### Sichtbarkeit von Eigenschaften und Kategorien einrichten

**Einstieg:** **Materialartenkarte** -> **Zugehörig -> Sichtbarkeit von Eigenschaften und Kategorien** ->
**Sichtbarkeit von Eigenschaften und Kategorien Liste** -> Zeile -> Karte
**Sichtbarkeit von Eigenschaften und Kategorien**.

**Prozessintro.** Mit dieser Einrichtung blendet der Administrator abhängig von einem im Konfigurator
eingegebenen Wert einzelne Eigenschaften oder ganze Kategorien aus. Beispiel: Wird für Stangenmaterial der
Wert „rund" erfasst, lassen sich „Dicke" und „Breite" ausblenden, weil nur „Durchmesser" relevant ist. Die
Regel greift ausschließlich, sobald der auslösende Wert tatsächlich gesetzt ist; bei leerem Auslösewert
wird nichts ausgeblendet. Wirksam wird die Einrichtung im Dialog **Produktkonfigurator**.

**Kopf – Auslöser:**

| Feld | Erläuterung |
|---|---|
| **Materialartencode** | Zeigt die Materialart, für die die Regel gilt; aus dem Aufrufkontext vorbelegt und nicht änderbar. Nur Materialarten mit aktivem **Verwendet für Produktkonfigurator** sind zulässig. |
| **Materialbeschreibung** | Zeigt die Beschreibung der Materialart zur Orientierung; wird automatisch abgeleitet. |
| **Eigenschaftscode** | Wenn gesetzt, bestimmt diese Eigenschaft den Auslöser der Ausblendung; auswählbar sind die Eigenschaften der Materialart. |
| **Eigenschaftsbeschreibung** | Zeigt den Namen der Auslöser-Eigenschaft; wird automatisch abgeleitet. |
| **Wert** | Wenn gesetzt, wird die Ausblendung genau dann aktiv, wenn im Konfigurator dieser Wert für die Auslöser-Eigenschaft erfasst wird. Bei Eigenschaften mit hinterlegten **Eigenschaftswerten** erfolgt die Auswahl aus dieser Liste; numerische bzw. Datumswerte werden gegen den **Datentyp** geprüft. |
| **Datentyp** | Zeigt den Datentyp der Auslöser-Eigenschaft (z. B. Text, Dezimal, Ganzzahl, Datum); steuert die Werteprüfung und wird automatisch abgeleitet. |
| **Eigenschaftswert verwenden** | Zeigt an, ob die Eigenschaft eine feste Werteliste nutzt. Wenn ja, wird der eingegebene **Wert** gegen die zulässigen **Eigenschaftswerte** geprüft. |

**Zeilen – auszublendende Objekte:**

| Feld | Erläuterung |
|---|---|
| **Ausblendungsart** | Legt fest, was ausgeblendet wird. **Eigenschaft:** Wenn gewählt, wird eine einzelne Eigenschaft ausgeblendet. **Kategorie:** Wenn gewählt, wird eine ganze Kategorie mit allen ihren Eigenschaften ausgeblendet. Bei Wechsel der Ausblendungsart wird der Code zurückgesetzt. |
| **Ausblendung von Code** | Wenn gesetzt, bezeichnet der Wert die konkret auszublendende Eigenschaft bzw. Kategorie. Die Hauptkategorie und Eigenschaften der Hauptkategorie können nicht ausgeblendet werden – der Versuch wird mit einer Meldung abgewiesen. |
| **Ausblendung von Beschreibung** | Zeigt die Bezeichnung des ausgeblendeten Objekts; wird automatisch aus dem Code abgeleitet. |

**Enablement-Schritte:** Zuerst im Kopf Eigenschaftscode und Wert als Auslöser festlegen, danach in den
Zeilen je Eintrag **Ausblendungsart** und **Ausblendung von Code** hinterlegen. Ein Auslöser kann mehrere
Ausblendungen bewirken. Für ausgeblendete Objekte übernimmt der Konfigurator automatisch den hinterlegten
Standardwert der Eigenschaft.

### Erweiterte Texte je Materialart und Kategorie einrichten

**Einstieg:** **Materialeigenschaften-Kategorienzuordnungen** -> Aktion **Erweiterte Texte** ->
**Erw. Textzuordnungsarbeitsblatt**.

**Prozessintro.** In diesem Arbeitsblatt ordnet der Administrator einer Materialart je Kategorie und
Prozess **Textvorlagen** des m+m Erw. Textmoduls zu. Beim Anlegen bzw. Finden eines Artikels über den
Konfigurator kombiniert das System diese Vorlagen und legt daraus die erweiterten Texte des neuen Artikels
an – getrennt nach Druckart (Infobox, Bericht, E-Mail). Dies verbindet die Konfiguration mit der
Belegtextausgabe des Erw. Textmoduls.

| Feld | Erläuterung |
|---|---|
| **Kategoriencode** | Wenn gesetzt, ordnet der Wert die Textzuweisung einer Eigenschaftskategorie zu. |
| **Kategoriebeschreibung** | Zeigt die Beschreibung der Kategorie; wird automatisch abgeleitet. |
| **Vorlagennr.** | Wenn gesetzt, verweist der Wert auf die zu verwendende Textvorlage; die **Druckart** wird daraus automatisch übernommen. Ein leerer Wert ist beim Speichern nicht zulässig. |
| **Vorlagenbeschreibung** | Zeigt die Beschreibung der Textvorlage; wird automatisch abgeleitet. |
| **Druckart** | Zeigt bzw. bestimmt, für welchen Ausgabekanal die Vorlage gilt (Infobox, Bericht oder E-Mail); wird aus der Vorlage übernommen und steuert die Prozessauswahl. |
| **Prozessgruppe** | Wenn gesetzt, ordnet der Wert die Zuweisung einer Prozessgruppe zu; das Setzen einer Prozessgruppe löscht einen ggf. gesetzten einzelnen Prozess. Die Auswahl ist auf Prozessgruppen der gewählten Druckart eingeschränkt. |
| **Prozess** | Wenn gesetzt, ordnet der Wert die Zuweisung einem einzelnen Prozess zu; das Setzen eines Prozesses löscht eine ggf. gesetzte Prozessgruppe. Die Auswahl ist auf Prozesse der gewählten Druckart eingeschränkt. |
| **Prozess-Objektname** | Zeigt das aus dem Prozess ermittelte Zielobjekt (z. B. eine Seite oder einen Bericht); nicht editierbar. |
| **Prozessobjekttyp** | Zeigt den Objekttyp des Prozessziels. **Bericht:** Das Prozessziel ist ein Bericht. **Seite:** Das Prozessziel ist eine Seite. **(leer):** Kein Objekttyp ermittelt (z. B. wenn eine Prozessgruppe statt eines Einzelprozesses verwendet wird). |
| **Reihenfolge** | Wenn gesetzt, bestimmt der Wert die Kombinationsreihenfolge der Vorlagen je Prozess/Prozessgruppe. **0 ist unzulässig**; je Prozess bzw. Prozessgruppe darf eine Reihenfolge nur einmal vergeben werden. |

Im Infobox-Bereich **Texte** wird die zur Vorlage gehörige Textvorschau angezeigt.

**Enablement-Schritte:** Zuerst je Kategorie eine Vorlagennr. und deren Druckart wählen, danach entweder
einen einzelnen **Prozess** oder eine **Prozessgruppe** zuordnen (nicht beides), schließlich eine
eindeutige **Reihenfolge > 0** vergeben. Beim späteren Konfigurieren erzeugt das System aus diesen
Zuweisungen die erweiterten Texte des Artikels.

### Beschreibungs- und Matchcodeformel um Textvorlagen erweitern

**Einstieg:** **Materialartenkarte** -> zugehörige Seite **Artikelbeschreibungsformel** (Basismodul
m+m Materialarten).

**Prozessintro.** Der Konfigurator nutzt die **Artikelbeschreibungsformel** der Materialart, um die
Beschreibung neu angelegter Artikel automatisch zu berechnen. Diese Erweiterung ergänzt die Formel-Eingabe
um die Möglichkeit, statt eines Eigenschaftscodes oder festen Textes eine **Erweiterte Textvorlage** in die
Formel aufzunehmen. Eine gleichartige Erweiterung (Feld **Erweiterte Textvorlage** und Aktion **Erw. Textvorlage hinzufügen**) steht auf der Seite **Chargen-/Seriennummernbeschreibungsformel erstellen** zur Verfügung.

| Feld | Erläuterung |
|---|---|
| **Erweiterte Textvorlage** | Wenn gesetzt, kann eine Textvorlage in die Beschreibungsformel aufgenommen werden. Das Feld ist nur editierbar, solange weder ein Eigenschaftscode noch ein fester Textwert gesetzt ist; umgekehrt sperren sich die drei Eingaben gegenseitig, damit je Formelbaustein genau eine Quelle greift. |

**Aktion:**

- **Erw. Textvorlage hinzufügen:** Wenn ausgeführt, fügt die Aktion die ausgewählte Textvorlage der
  Artikelbeschreibungsformel hinzu. Sie ist nur aktiv, wenn eine **Erweiterte Textvorlage** ausgewählt ist.

**Enablement-Schritt:** Erweiterte Textvorlage auswählen, mit **Erw. Textvorlage hinzufügen** in die Formel
übernehmen; anschließend berechnet der Konfigurator die Artikelbeschreibung daraus.

### Regelablauf des Produktkonfigurators einrichten

**Einstieg:** **Materialartenkarte** -> Aktion **Produktkonfigurator Regelwerk**.

**Prozessintro.** Über den **Regelablauf** (Modul m+m Normregelverwaltung) kann der Administrator festlegen,
dass bei der Eingabe von Eigenschaftswerten im Konfigurator automatisch Werte berechnet oder gesetzt
werden. Ergänzend kann je Eigenschaft ein **Direkter Regelcode** hinterlegt werden, der beim Ändern des
Wertes im Konfigurator direkt ausgeführt wird.

| Einrichtung | Erläuterung |
|---|---|
| **Produktkonfigurator Regelwerk** (Aktion) | Wenn ausgeführt, öffnet die Aktion den zur Materialart gehörenden Regelablauf; ist noch keiner vorhanden, wird automatisch ein neuer angelegt. Im Regelablauf definierte Regeln werden bei jeder Werteingabe im Konfigurator abgearbeitet und können abhängige Eigenschaften automatisch füllen. |
| **Direkter Regelcode** (Eigenschaft) | Wenn gesetzt, wird die hinterlegte Regel unmittelbar ausgeführt, sobald der Wert dieser Eigenschaft im Konfigurator geändert wird, und schreibt je nach Datentyp das berechnete Ergebnis in die Eigenschaft zurück. Andere Eigenschaften mit direktem Regelcode werden dabei ebenfalls neu ausgewertet. |

**Enablement-Schritte:** Zuerst mit **Produktkonfigurator Regelwerk** den Regelablauf öffnen und die
gewünschten Regeln anlegen; danach – bei Bedarf – einzelnen Eigenschaften einen **Direkten Regelcode**
zuweisen. Weiterführende Details zur Regeldefinition beschreibt die Dokumentation der m+m
Normregelverwaltung.

### Berechtigungen

Der Berechtigungssatz **Product Configurator all permissions** (m+m PK Permission) fasst alle Tabellen,
Seiten und Codeunits des Produktkonfigurators zusammen. Die Zuweisung dieses Satzes an eine Benutzergruppe
bestimmt, welche Aktionen die Anwender im Produktkonfigurator ausführen können – von der Pflege der
Kategorienzuordnungen und Sichtbarkeitsregeln bis zum Öffnen des Konfigurators in der Belegzeile. Ohne
diesen Berechtigungssatz stehen die zugehörigen Seiten und Aktionen nicht zur Verfügung.

---

## Stammdaten

### Eigenschaftentabelle – Darstellung und Kategorienzuweisung

**Einstieg:** **Materialartenkarte** -> Eigenschaftentabelle (Register **Allgemein**, Basismodul
m+m Materialarten).

**Prozessintro.** In der Eigenschaftentabelle der Materialart pflegen die Stammdatenverantwortlichen die
einzelnen Eigenschaften. Diese Erweiterung ergänzt die Tabelle um die **Darstellungsarten** und um eine
Aktion zur schnellen Kategorienzuweisung. Die hier gepflegten Werte – insbesondere **Erforderlich**,
**Fix**, **Standardwert** und **Darstellungsarten** – steuern unmittelbar, wie sich die Eigenschaft im
Dialog **Produktkonfigurator** verhält und darstellt.

| Feld | Erläuterung |
|---|---|
| **Darstellungsarten** | Wenn gesetzt, bestimmt der Wert die farbliche bzw. typografische Darstellung der Eigenschaft im Konfigurator. Zulässige Werte und ihre Wirkung: **(leer):** Standarddarstellung; nicht editierbare Eigenschaften werden abgeschwächt (grau) dargestellt. **Standard:** neutrale Standarddarstellung. **Blau** (StandardAccent): blaue Hervorhebung. **Fett** (Strong): fette Schrift. **Blau (Fett)** (StrongAccent): fett und blau. **Rot (Kursiv)** (Attention): rot-kursive Warndarstellung. **Blau (Kursiv)** (AttentionAccent): blau-kursiv. **Grün (Fett)** (Favorable): grün-fett als positive Kennzeichnung. **Rot (Fett & Kursiv)** (Unfavorable): rot-fett-kursiv als deutliche Warnung. **Gelb** (Ambiguous): gelbe Hervorhebung für uneindeutige Werte. **Grau** (Subordinate): abgeschwächte, untergeordnete Darstellung. |

Ergänzend steuern folgende Basisfelder der Eigenschaftentabelle das Verhalten im Konfigurator (Pflege im
Basismodul m+m Materialarten):

| Feld | Erläuterung |
|---|---|
| **Erforderlich** | Wenn aktiviert, muss die Eigenschaft im Konfigurator einen Wert erhalten; das Verlassen mit **OK** ist erst möglich, wenn kein Pflichtfeld mehr offen ist. Ist ein **Standardwert** hinterlegt, gilt das Pflichtfeld als vorbelegt. |
| **Fix** | Wenn aktiviert, wird die Eigenschaft bei der **Suchoption** „Nur fixe Merkmale suchen" in die Artikelsuche einbezogen; nicht-fixe Eigenschaften bleiben bei dieser Suchoption unberücksichtigt. |
| **Standardwert** | Wenn gesetzt, ist die Eigenschaft im Konfigurator bereits mit diesem Wert vorbelegt; bei ausgeblendeten Eigenschaften übernimmt der Konfigurator diesen Wert automatisch. |
| **Verkaufseigenschaft / Einkaufseigenschaft** | Wenn aktiviert, wird die Eigenschaft der Verkaufs- bzw. Einkaufsseite zugeordnet; bei der Suchoption „Nur fixe Merkmale suchen" werden diese Eigenschaften ignoriert. |
| **Wertfilter / Wertgruppenfilter** | Wenn gesetzt, schränken die Filter die im Konfigurator zur Auswahl stehenden **Eigenschaftswerte** ein. |

**Aktion:**

- **Kategorien von Produktkonfigurator zuweisen:** Wenn ausgeführt, ordnet die Aktion allen markierten
  Eigenschaften in einem Schritt einen zuvor gewählten **Kategoriencode** zu. Dies ist die Massenvariante
  der Zuordnung aus dem Abschnitt *Kategorien und Reihenfolge einrichten*.

### Textvorlagen als Produktkonfigurator-Kategorie kennzeichnen

**Einstieg:** Vorlagenliste des m+m Erw. Textmoduls (über **Suchen**) -> **Vorlagen**.

**Prozessintro.** Diese Erweiterung ergänzt die Textvorlagen des Erw. Textmoduls um ein Kennzeichen, das
signalisiert, dass eine Vorlage einer Produktkonfiguratorkategorie zugewiesen ist. Stammdatenverantwortliche
erkennen so in der Vorlagenpflege, welche Vorlagen im Kontext des Produktkonfigurators verwendet werden.

| Feld | Erläuterung |
|---|---|
| **Zugewiesen in Produktkonfiguratorkategorien** | Wenn gesetzt, zeigt das Feld an, dass die Textvorlage einer Produktkonfiguratorkategorie zugeordnet ist; es dient der Übersicht bei der Vorlagenpflege und weist auf die Verwendung im Konfigurator-Textablauf hin. |

---

## Tägliche Arbeit im Produktkonfigurator

Dieser Abschnitt beschreibt die tägliche Nutzung durch die operativen Anwender. Die Verfügbarkeit in einer
Belegzeile hängt direkt von der Einrichtung der Materialart ab (siehe **Produktkonfigurator für eine
Materialart einrichten**): Nur Materialarten mit aktivem **Verwendet für Produktkonfigurator** und
angehaktem Belegkennzeichen stehen zur Auswahl.

### Konfigurator aus einer Belegzeile öffnen

Der Einstieg ist in allen unterstützten Belegen identisch. In der Belegzeile wird das Feld
**Produktkonfigurator-Materialart** gefüllt:

1. Belegzeile öffnen und in der Zeile das Feld **Produktkonfigurator-Materialart** auswählen. Die Auswahl
   ist auf Materialarten eingeschränkt, die für die jeweilige Belegart freigegeben sind.
2. Nach Auswahl setzt das System den Zeilentyp auf Artikel, speichert die Zeile und öffnet den Dialog
   **Produktkonfigurator**.

Unterstützte Belegzeilen (jeweils Feld **Produktkonfigurator-Materialart**):

- **Verkauf:** Verkaufsangebot, Verkaufsauftrag, Rahmenauftrag.
- **Einkauf:** Einkaufsanfrage, Einkaufsbestellung, Rahmenbestellung.
- **Fertigung:** Fertigungsstücklistenzeilen sowie geplante, fest geplante, freigegebene und beendete
  Fertigungsauftragszeilen.

> In Fertigungsauftragszeilen ist der Konfigurator nur bearbeitbar, solange zur Zeile weder eine
> Reservierung noch ein Kapazitätsposten existiert. Andernfalls öffnet der Konfigurator nur zur Ansicht,
> und beim Öffnen weist das System auf die vorhandene Reservierung bzw. den Kapazitätsposten hin.

### Aufbau des Dialogs Produktkonfigurator

Der Dialog **Produktkonfigurator** ist in mehrere Bereiche gegliedert:

- **Oben links – Hauptkategorie:** Die Eigenschaften der Hauptkategorie (Reihenfolge 0) mit den Spalten
  **Eigenschaftswert**, **Eigenschaftswertname** und **Einheit**. Im Kopf werden Materialart, Belegnummer
  und Zeilennummer angezeigt.
- **Oben rechts – Kategorien:** Übersicht **Zugeordnete Kategorien** der Materialart (ohne Hauptkategorie).
  Ein Klick auf eine Kategorie zeigt deren Eigenschaften.
- **Unten – Zeilenbereich:** Die Eigenschaften der gewählten Kategorie mit **Beschreibung**,
  **Eigenschaftswert**, **Eigenschaftswertname** und **Einheit**.
- **Infoboxen – Pflichtfelder / Nicht gefüllte Pflichtfelder:** Alle als **Erforderlich** gekennzeichneten
  Eigenschaften. Sobald ein Pflichtfeld einen Wert erhält, verschwindet es aus **Nicht gefüllte
  Pflichtfelder**; die Darstellung wechselt von rot zu grün.
- **Druckart** und die Infobox der erweiterten Textbelegarten steuern bzw. zeigen die zugehörigen
  Textausgaben; über die Aktion **Vorschau** lässt sich der zusammengesetzte Text im Texteditor ansehen.

**Werteingabe.** Werte werden direkt eingegeben oder per Nachschlagen aus den hinterlegten
**Eigenschaftswerten** gewählt. Nach jeder Eingabe wird der Regelablauf ausgeführt und die
Sichtbarkeitsfilter werden neu aufgebaut – abhängige Eigenschaften oder Kategorien können dadurch
ein- oder ausgeblendet werden.

### Abschluss: Artikel finden oder anlegen

1. Alle **Pflichtfelder** füllen, bis der Bereich **Nicht gefüllte Pflichtfelder** leer ist.
2. Mit **OK** bestätigen. Das System prüft zunächst, ob alle Pflichtwerte der Hauptkategorie erfasst sind,
   und sucht dann einen passenden Artikel:
   - **Treffer gefunden:** Artikel und ggf. Variante werden in die Belegzeile übernommen.
   - **Kein Treffer, Suchoption „Eindeutige Suche":** Es wird direkt ein neuer Artikel über den
     **Artikelvorlagencode** angelegt und die erweiterten Texte werden aus den Textzuweisungen erzeugt.
   - **Kein Treffer, aber Basisartikel vorhanden:** Es wird eine Artikelvariante aus dem Basisartikel
     erzeugt und mit den eingegebenen Eigenschaftswerten belegt.
   Neu angelegte Artikel tragen das Kennzeichen **Erstellt von Produktkonfigurator** und werden während der
   Wertübernahme kurzzeitig gesperrt.
3. **Abbrechen** verwirft alle Eingaben; ein Zwischenspeichern und späteres Fortsetzen ist nicht möglich.

> Ist ein Erforderlich-Feld nicht gefüllt, verhindert das System das Verlassen mit **OK** und nennt die
> fehlende Eigenschaft samt Kategorie. Wird kein Artikel gefunden oder angelegt, fragt das System nach, ob
> die Seite dennoch geschlossen werden soll.

### Erweiterte Texte in der Fertigungsstückliste

In Fertigungsstücklistenzeilen steht neben dem Feld **Produktkonfigurator-Materialart** zusätzlich die
Aktion **Erweiterte Texte** zur Verfügung. Wenn ausgeführt, öffnet sie das Arbeitsblatt der erweiterten
Texte für den Artikel der Zeile, sodass die im Konfiguratorablauf erzeugten Texte eingesehen und gepflegt
werden können.

---

## Typische Anwendungsfälle

### Konfigurierten Artikel im Verkaufsauftrag erfassen

**Auslöser.** Ein Kunde ruft an und benötigt Stangenmaterial in einer bestimmten Abmessung, für die noch
kein Artikel existiert.

**Einstieg in BC.** Der Anwender öffnet den **Verkaufsauftrag** des Kunden und legt eine neue Zeile an. In
der Zeile wählt er im Feld **Produktkonfigurator-Materialart** die passende Materialart; der Dialog
**Produktkonfigurator** öffnet sich.

**Kernablauf.**
1. In der Hauptkategorie die Grundmerkmale (z. B. Werkstoff) erfassen.
2. Über die **Zugeordnete Kategorien** die weiteren Kategorien wählen und deren Eigenschaftswerte eingeben.
   Sichtbarkeitsregeln blenden nicht benötigte Eigenschaften automatisch aus.
3. Die Infobox **Nicht gefüllte Pflichtfelder** kontrollieren, bis sie leer und grün ist.
4. Mit **OK** bestätigen. Findet das System keinen passenden Artikel, legt es über den
   **Artikelvorlagencode** einen neuen Artikel samt Beschreibung (Artikelbeschreibungsformel) und
   erweiterten Texten an und übernimmt ihn in die Auftragszeile.

**Abschluss.** Die Auftragszeile enthält nun den konfigurierten Artikel; die weitere Auftragsbearbeitung
(Preise, Lieferung, Fakturierung) erfolgt im BC-Standard.

### Neue Materialart konfigurierbar machen

**Auslöser.** Ein neues Sortiment soll künftig über den Konfigurator abgewickelt werden.

**Einstieg in BC.** Der Administrator öffnet **Materialarten** (über **Suchen**), wählt die Materialart und
öffnet die **Materialartenkarte**.

**Kernablauf.**
1. Im Register **Produktkonfigurator** **Verwendet für Produktkonfigurator** aktivieren,
   **Artikelvorlagencode** und **Suchoption** setzen sowie die Belegarten ankreuzen.
2. Über **Zugehörig -> Produktkonfiguratorkategorien** die **Hauptkategorie** (Reihenfolge 0) anlegen und
   den Eigenschaften Kategorien zuordnen.
3. In der Eigenschaftentabelle die Pflichteigenschaften als **Erforderlich** kennzeichnen und
   **Darstellungsarten** setzen.
4. Optional über **Zugehörig -> Sichtbarkeit von Eigenschaften und Kategorien** Ausblendungsregeln
   hinterlegen und über **Produktkonfigurator Regelwerk** Regeln definieren.

**Abschluss.** Die Materialart steht ab sofort in den freigegebenen Belegarten im Feld
**Produktkonfigurator-Materialart** zur Verfügung.

### Konfiguration in der Fertigungsstückliste

**Auslöser.** Für einen Fertigungsartikel soll eine Komponente eigenschaftsbasiert bestimmt werden.

**Einstieg in BC.** Der Anwender öffnet die **Fertigungsstückliste** und legt eine Komponentenzeile an. In
der Zeile wählt er im Feld **Produktkonfigurator-Materialart** die Materialart.

**Kernablauf.**
1. Der Dialog **Produktkonfigurator** öffnet sich; die Eigenschaftswerte werden erfasst.
2. Mit **OK** wird die Komponente (Artikel/Variante) ermittelt oder angelegt und in die
   Stücklistenzeile übernommen.
3. Über die Aktion **Erweiterte Texte** lassen sich die zugehörigen Texte der Komponente einsehen.

**Abschluss.** Die Fertigungsstückliste enthält die konfigurierte Komponente für die weitere
Fertigungsplanung.

---

## FAQ und Troubleshooting

### 1. Warum kann ich die Aktion Produktkonfiguratorkategorien nicht anwählen?

Die Aktion ist nur aktiv, wenn auf der **Materialartenkarte** im Register **Produktkonfigurator** das Feld
**Verwendet für Produktkonfigurator** aktiviert ist. Ist das Kennzeichen nicht gesetzt, bleiben
**Produktkonfiguratorkategorien**, **Sichtbarkeit von Eigenschaften und Kategorien** und
**Produktkonfigurator Regelwerk** ausgegraut.

### 2. Warum lässt sich Verwendet für Produktkonfigurator nicht deaktivieren?

Das Deaktivieren ist gesperrt, solange zu dieser Materialart Einträge unter **Sichtbarkeit von
Eigenschaften und Kategorien** bestehen. Entfernen Sie zuerst diese Einträge; danach lässt sich das
Kennzeichen zurücknehmen, wobei alle Belegkennzeichen zurückgesetzt werden.

### 3. Warum erscheint eine Eigenschaft nicht im Produktkonfigurator?

Im Konfigurator werden nur Eigenschaften angezeigt, die einem **Kategoriencode** zugeordnet sind. Ordnen
Sie die Eigenschaft über **Produktkonfiguratorkategorien** bzw. über die Aktion **Kategorien von
Produktkonfigurator zuweisen** einer Kategorie zu. Zusätzlich kann die Eigenschaft durch eine
Sichtbarkeitsregel ausgeblendet sein.

### 4. Warum verlangt das System eine Hauptkategorie?

Je Materialart muss genau eine Kategorie die **Reihenfolge 0** (Hauptkategorie) tragen. Ihre Eigenschaften
erscheinen im Konfigurator im ersten Bereich. Fehlt die Hauptkategorie, weist das System beim Verlassen der
**Materialeigenschaften-Kategorienzuordnungen** darauf hin. Legen Sie sie über **Hauptkategorie anlegen** an.

### 5. Warum kann ich den Konfigurator mit OK nicht verlassen?

Solange in der Infobox **Nicht gefüllte Pflichtfelder** noch als **Erforderlich** gekennzeichnete
Eigenschaften ohne Wert stehen, wird das Verlassen mit **OK** verhindert. Das System nennt die fehlende
Eigenschaft samt Kategorie. Füllen Sie alle Pflichtfelder, bis der Bereich leer und grün ist.

### 6. Was passiert, wenn zu meinen Eingaben kein Artikel gefunden wird?

Bei der **Suchoption** „Eindeutige Suche" legt das System über den **Artikelvorlagencode** direkt einen
neuen Artikel an. Ist ein Basisartikel vorhanden, wird stattdessen eine Variante daraus erzeugt und mit den
Eigenschaftswerten belegt. Ohne hinterlegten **Artikelvorlagencode** ist keine Artikelanlage möglich.

### 7. Warum wird eine als erforderlich gekennzeichnete Eigenschaft nicht als nicht gefüllt angezeigt?

Ist zu einer Erforderlich-Eigenschaft ein **Standardwert** hinterlegt, gilt das Pflichtfeld als bereits
gefüllt. Die Eigenschaft erscheint dann zwar im Bereich **Pflichtfelder**, aber nicht in **Nicht gefüllte
Pflichtfelder**.

### 8. Was bewirkt die Suchoption „Nur fixe Merkmale suchen"?

Bei dieser Option prüft die Artikelsuche ausschließlich Eigenschaften mit gesetztem Kennzeichen **Fix** im
Register **Allgemein**; **Verkaufseigenschaft** und **Einkaufseigenschaft** werden ignoriert. Die Option
lässt sich nicht setzen, wenn zu nicht-fixen Eigenschaften ein **Standardwert** hinterlegt ist.

### 9. Warum verschwindet plötzlich eine Kategorie oder Eigenschaft während der Eingabe?

Über **Sichtbarkeit von Eigenschaften und Kategorien** kann eingerichtet sein, dass ein bestimmter Wert
weitere Eigenschaften oder ganze Kategorien ausblendet (z. B. Wert „rund" blendet „Dicke" und „Breite"
aus). Ausgeblendete Objekte übernehmen automatisch ihren **Standardwert**. Hauptkategorie und deren
Eigenschaften lassen sich nicht ausblenden.

### 10. Warum kann ich den Konfigurator in einer Fertigungsauftragszeile nur ansehen?

Sobald zur Fertigungsauftragszeile eine Reservierung oder ein Kapazitätsposten existiert, öffnet der
Konfigurator schreibgeschützt. Beim Öffnen weist das System auf die vorhandene Reservierung bzw. den
Kapazitätsposten hin. Lösen Sie die Reservierung, um die Konfiguration erneut bearbeiten zu können.
