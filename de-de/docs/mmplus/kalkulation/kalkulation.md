---
title: Anwenderhandbuch m+m Calculation
---

# Anwenderhandbuch m+m Calculation

## Einleitung

Das Modul **m+m Calculation** berechnet in Microsoft Dynamics 365 Business Central den
**Einstandspreis** und den **Verkaufspreis** eines Artikels auf Basis eines frei definierbaren
Kalkulationsschemas. Grundlage jeder Berechnung ist eine **Kalkulationsvorlage**, die Zeile für
Zeile festlegt, welche Kostenbestandteile (Materialkosten, Kapazitätskosten, Gemeinkosten,
Fremdarbeitskosten, Werkzeugkosten, Zu- und Abschläge) in welcher Reihenfolge zusammengeführt
werden. Aus den Kostenwerten eines simulierten Fertigungsauftrags ermittelt das Modul die
Einzelwerte und verdichtet sie über **Zwischensummen** und **Summen** bis zum Einstands- und
Verkaufspreis.

**Zielgruppe:** Primär sind es **operativ tätige Anwender im Verkauf und in der
Arbeitsvorbereitung**, die im Tagesgeschäft aus einem **Verkaufsauftrag**, einem
**Verkaufsangebot**, einer **Verkaufsrechnung** oder einer **Verkaufschance** heraus eine
Kalkulation erstellen, kalkulieren, **zertifizieren** und den ermittelten Preis in den Beleg
übernehmen. Sekundäre Zielgruppe sind **Administratoren und Key-User**, die einmalig die
**Kalkulation Einrichtung**, die **Kalkulationsvorlagen** und die
**Kalkulationsvorlagevorgaben** aufbauen.

**Kurzer Prozessüberblick:** Der Anwender öffnet aus der Verkaufsbelegzeile über
**Zeile → Funktionen → Erstelle/Öffne Kalkulation** eine neue **Kalkulation**. Anhand von
**Kontaktnr.** (Debitor bzw. Debitorenpreisgruppe) und **Artikelnr.** wählt das System über die
**Kalkulationsvorlagevorgaben** automatisch die passende **Kalkulationsvorlage** vor. Der Anwender
pflegt Werte und Prozentsätze in den Kalkulationszeilen, lässt neu berechnen, **zertifiziert** die
Kalkulation und übernimmt den **Verkaufspreis** in den Beleg bzw. den **Einstandspreis** in den
Artikel.

Die typische Einstiegskette lautet: **übergeordneter Beleg (Verkaufsauftrag/-angebot/-rechnung)
oder Verkaufschance → Zeile → Funktionen → Erstelle/Öffne Kalkulation → Kalkulation bearbeiten →
zertifizieren → Preisübernahme**.

---

## Schnellstart für Anwender

Die Schritte folgen der Abhängigkeitsreihenfolge: zuerst **Einrichtung**, dann **Stammdaten**,
dann die tägliche Arbeit am Beleg.

1. **Einrichtung prüfen (einmalig, Administrator).** Öffnen Sie über **Suchen** die Seite
   **Kalkulation Einrichtung** und hinterlegen Sie **Kalkulations-Nr.** (Nummernserie),
   **Dummy Artikel-Nr.**, **Dummy Arbeitsplannr.**, **Vorlage für neuen Artikel** sowie
   **Bericht Kalkulation**.
2. **Kalkulationsvorlage anlegen (Key-User).** Öffnen Sie über **Suchen** die Liste
   **Kalkulationsvorlagen**, legen Sie eine Vorlage an und definieren Sie in den **Zeilen** das
   Berechnungsschema (Feldart, Berechneter Wert, Formel, Verwendungsart).
3. **Standardvorgaben festlegen (optional).** Öffnen Sie in der **Kalkulation Einrichtung** über
   **Standardkalkulationsvorlagen** die Seite **Kalkulationsvorlagevorgaben** und ordnen Sie
   Debitoren/Artikel-Kombinationen eine Vorlage zu.
4. **Kalkulation aus dem Beleg starten (Anwender).** Öffnen Sie in der Zeile eines
   **Verkaufsauftrags**, **Verkaufsangebots** oder einer **Verkaufsrechnung** über
   **Zeile → Funktionen** die Aktion **Erstelle/Öffne Kalkulation**. Es öffnet sich die
   **Kalkulation** mit vorbelegter **Artikelnr.**, **Kontaktnr.** und ggf. **Kalkulationsvorlage**.
5. **Kalkulieren.** Pflegen Sie Werte/Prozentsätze in den Zeilen; das System berechnet Einstands-
   und Verkaufspreis fortlaufend neu. Bei Bedarf **Einstandspreis aktualisieren**.
6. **Kalkulation zertifizieren.** Wählen Sie **Kalkulation zertifizieren**. Der Status wechselt auf
   **Zertifiziert**; die Werte werden schreibgeschützt.
7. **Preis übernehmen.** Übernehmen Sie den Verkaufspreis mit **Verkaufspreis in Belege setzen**
   in den zugeordneten Beleg (bei Einrichtung **Beim Zertifizieren** geschieht dies automatisch),
   den Einstandspreis mit **Einstandspreis aktualisieren** in den Artikel und optional den
   Verkaufspreis mit **Preis in Artikelkarte setzen** in die Artikelkarte.

---

## Einrichtung

Die **Einrichtung** ist die Voraussetzung für jede Kalkulation und wird einmalig vom
Administrator vorgenommen. Ohne **Kalkulations-Nr.**, **Dummy Artikel-Nr.** und
**Dummy Arbeitsplannr.** lässt sich keine Kalkulation anlegen (das Modul erzeugt beim Anlegen
einer Kalkulation im Hintergrund einen **simulierten Fertigungsauftrag**, der eine Artikelnummer
und einen Arbeitsplan benötigt).

### Kalkulation Einrichtung

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Kalkulation Einrichtung**. Es handelt sich um
eine unternehmensweite Einrichtungsseite mit genau einem Datensatz (Typ A, kein übergeordneter
Beleg). Der Administrator hinterlegt hier alle grundlegenden Vorgaben für Nummernvergabe,
Berechnung, Preisübernahme und Berichte, bevor die erste Kalkulation entsteht. Die hier gesetzten
Werte steuern anschließend die **Kalkulation** (Nummernserie, Preisübernahme) und die
**Batch-Kalkulation** (Batch-Vorlage) im Tagesablauf.

#### Bereich Allgemein

| Einrichtung | Erläuterung |
|---|---|
| **Kalkulations-Nr.** | Legt die Nummernserie fest, aus der neue Kalkulationen ihre **Nr.** erhalten. Wenn hinterlegt, vergibt das System beim Anlegen automatisch die nächste freie Nummer; ist das Feld leer, kann keine Kalkulation angelegt werden (Pflichtprüfung beim Einfügen). |
| **Dummy Artikel-Nr.** | Legt den Platzhalter-Artikel fest, mit dem der simulierte Fertigungsauftrag initial angelegt wird. Wenn gesetzt, kann eine Kalkulation auch ohne bereits existierenden Zielartikel begonnen werden; ohne Eintrag bricht das Anlegen ab, da für jede Kalkulation eine Artikelnummer erforderlich ist. |
| **Dummy Arbeitsplannr.** | Legt den Platzhalter-Arbeitsplan fest, der dem simulierten Fertigungsauftrag zugewiesen wird, solange der Artikel keinen eigenen Arbeitsplan besitzt. Wenn gesetzt, können Kapazitätskosten über den simulierten Fertigungsauftrag ermittelt werden. |
| **Vorlage für neuen Artikel** | Legt die Artikelvorlage (Konfigurationsvorlage) fest, aus der beim **Artikel anlegen** die Stammdaten des neuen Artikels vorbelegt werden. Wenn gesetzt, erhält der aus der Kalkulation erzeugte Artikel automatisch die vordefinierten Eigenschaften; ist keine Vorlage hinterlegt, wird das Anlegen mit einer Meldung abgebrochen. |
| **Kalkulationen rekursiv aktualisieren** | Steuert, ob eine Änderung des Einstandspreises einer Kalkulation, die als Komponente in anderen Kalkulationen verwendet wird, an diese weitergereicht wird. Werte siehe Optionsliste unten. |
| **Mat.-Gemeinkosten für EK-Artikel berechnen** | Steuert, ob und wann auf zugekaufte Komponenten (Beschaffungsart Einkauf) zusätzliche Materialgemeinkosten aufgeschlagen werden. Werte siehe Optionsliste unten. |
| **Batch Kalkulationsvorlage** | Legt die Kalkulationsvorlage fest, die die **Batch-Kalkulation** (Massenkalkulation im **Kalkulation Batch Buch.-Blatt**) verwendet. Wenn gesetzt, werden beim Sammeln der Kalkulationen die Batchzeilen automatisch mit dieser Vorlage vorbelegt. |
| **Verkaufspreis im Beleg setzen** | Steuert, ob der ermittelte Verkaufspreis automatisch in den zugeordneten Verkaufsbeleg übernommen wird. Werte siehe Optionsliste unten. |

**Optionswerte:**

- **Kalkulationen rekursiv aktualisieren**
  - **Niemals:** Der neue Einstandspreis wird nicht an übergeordnete Kalkulationen weitergegeben;
    diese behalten ihren bisherigen Wert bis zur manuellen Neuberechnung.
  - **Immer:** Ändert sich der Einstandspreis, aktualisiert das System ohne Rückfrage automatisch
    alle in Entwicklung befindlichen Kalkulationen, in denen diese Kalkulation als Komponente
    verwendet wird.
  - **Bestätigung:** Vor der Weitergabe erscheint eine Rückfrage; der Anwender entscheidet, ob die
    abhängigen Kalkulationen aktualisiert werden.
- **Mat.-Gemeinkosten für EK-Artikel berechnen**
  - **Immer:** Auf zugekaufte Komponenten werden bei jeder Kalkulation Materialgemeinkosten
    aufgeschlagen und in **Mat.-Gemeinkosten EK-Artikel** ausgewiesen.
  - **Niemals:** Es werden keine gesonderten Materialgemeinkosten für Einkaufsartikel berechnet.
  - **Wenn verwendet:** Der Aufschlag erfolgt nur, wenn die Kalkulationsvorlage eine Zeile mit dem
    berechneten Wert **Materialgemeinkosten Einkaufsartikel** enthält.
- **Verkaufspreis im Beleg setzen**
  - **(leer):** Es erfolgt keine automatische Preisübernahme; der Anwender überträgt den
    Verkaufspreis bei Bedarf manuell über **Verkaufspreis in Belege setzen**.
  - **Beim Zertifizieren:** Beim **Zertifizieren** der Kalkulation wird der Verkaufspreis
    automatisch in die Zeilen der zugeordneten, noch offenen Verkaufsbelege geschrieben und ist
    danach fixiert.

#### Bereich Drucken

Dieser Bereich verknüpft die Kalkulation mit den auszugebenden Berichten. Wenn hier ein Bericht
hinterlegt ist, steht die Aktion **Drucken** in der Kalkulation und in der Liste **Kalkulationen**
zur Verfügung.

| Einrichtung | Erläuterung |
|---|---|
| **Bericht Kalkulation** | Legt die Berichts-ID fest, mit der eine Kalkulation ausgedruckt wird. Wenn gesetzt, druckt die Aktion **Drucken** genau diesen Bericht; ist das Feld leer, meldet das System beim Drucken einen fehlenden Bericht. |
| **Berichtsname** | Zeigt zur Kontrolle den Namen des unter **Bericht Kalkulation** gewählten Berichts an (nur Anzeige, nicht editierbar). |
| **Kalkulation Druckfilterseite anzeigen** | Wenn aktiviert, öffnet sich vor dem Druck der Kalkulation die Anfrageseite (Druckfilterseite), auf der der Anwender Filter und Optionen setzen kann; ohne Aktivierung wird direkt gedruckt. |
| **FA Bericht** | Legt die Berichts-ID des Fertigungsauftrag-Berichts fest, der zusätzlich zum Kalkulationsbericht für den simulierten Fertigungsauftrag gedruckt wird. Wenn gesetzt, wird beim Drucken auch dieser Bericht ausgegeben. |
| **Berichtsname** | Zeigt zur Kontrolle den Namen des unter **FA Bericht** gewählten Berichts an (nur Anzeige). |
| **FA Druckfilterseite anzeigen** | Wenn aktiviert, erscheint vor dem Druck des Fertigungsauftrag-Berichts dessen Anfrageseite; ohne Aktivierung wird direkt gedruckt. |

**Aktion in der Einrichtung:** Über **Standardkalkulationsvorlagen** öffnet der Anwender die Seite
**Kalkulationsvorlagevorgaben** (siehe Abschnitt *Kalkulationsvorlagevorgaben einrichten*).

### Berechtigungen

Für den Zugriff auf das Modul stellt die App das Berechtigungsset **MuM CA Permission** bereit. Es
legt fest, welche Aktionen die Anwender in den Kalkulationsobjekten ausführen dürfen (Anlegen,
Ändern, Zertifizieren, Löschen der Kalkulationen, Vorlagen und Einrichtung). Der Administrator
weist dieses Berechtigungsset den betreffenden Benutzern bzw. Benutzergruppen über die
Standard-Berechtigungsverwaltung von Business Central zu.

---

## Stammdaten

Die Stammdaten legen fest, **wie** kalkuliert wird (Kalkulationsvorlagen), **welche** Vorlage
automatisch vorgeschlagen wird (Kalkulationsvorlagevorgaben) und stellen den Bezug zu **Artikel**
und **Verkaufschance** her.

### Kalkulationsvorlagen

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Kalkulationsvorlagen** und öffnen Sie eine
Zeile, um die Karte **Kalkulationsvorlage** zu bearbeiten.

Die Kalkulationsvorlage ist der Kern des Moduls: In ihr definiert der Key-User **ein** Schema,
nach dem das System die Kalkulationspreise berechnet. Der Administrator/Key-User pflegt die
Vorlagen vor der ersten Kalkulation und passt sie an, wenn sich das Kalkulationsschema ändert. Die
Vorlage wird in der **Kalkulation** über das Feld **Kalkulationsvorlage** ausgewählt bzw. über die
**Kalkulationsvorlagevorgaben** automatisch vorbelegt.

**Ablauf:** Zuerst legen Sie den Vorlagenkopf an (Code, Beschreibung, Grundwerte), danach erfassen
Sie die Vorlagenzeilen von oben nach unten in der gewünschten Berechnungsreihenfolge.

#### Kopfdaten der Kalkulationsvorlage

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger Schlüssel der Vorlage. Wenn gesetzt, kann die Vorlage in Kalkulationen und Vorgaben ausgewählt werden. |
| **Beschreibung** | Sprechender Name der Vorlage; erleichtert die Auswahl in Kalkulation und Vorgaben. |
| **Mat.-Gemeinkosten % EK-Artikel** | Legt den Prozentsatz fest, mit dem Materialgemeinkosten auf zugekaufte Komponenten aufgeschlagen werden. Wenn gesetzt, wird dieser Wert beim Auswählen der Vorlage in die Kalkulation übernommen und dort für die Berechnung der **Mat.-Gemeinkosten EK-Artikel** herangezogen. |
| **Losgröße** | Legt die Auftragsmenge fest, auf die kalkuliert wird (Mindestwert 1). Wenn gesetzt, wird die Losgröße beim Auswählen der Vorlage in die Kalkulation übernommen; die ermittelten Kosten werden anschließend auf diese Menge bezogen (pro Stück). |

#### Zeilen der Kalkulationsvorlage

Die **Zeilen** bilden das Rechenschema. Die Abarbeitung erfolgt **immer von oben nach unten**;
Summen und Zwischensummen greifen über das Feld **Formel** auf die zu kumulierenden Zeilennummern
zu.

| Feld | Erläuterung |
|---|---|
| **Zeilennr.** | Legt die Position der Zeile im Schema fest und bestimmt damit die Abarbeitungsreihenfolge. |
| **Beschreibung** | Bezeichnung der Zeile (z. B. „Materialkosten“, „Verwaltungsgemeinkosten“); erscheint gleichlautend in der Kalkulation. |
| **Feldart** | Bestimmt, wie der Zeilenwert ermittelt wird. Werte siehe Optionsliste unten; von der Feldart hängt ab, welche weiteren Felder editierbar sind. |
| **Berechneter Wert** | Nur bei Feldart **Berechneter Wert** aktiv: legt fest, welcher Kostenbestandteil aus dem simulierten Fertigungsauftrag herangezogen wird. Werte siehe Optionsliste unten. |
| **Berechnungsbasis** | Verweist bei prozentualen Zeilen auf die Zeilennr., auf deren Wert der Prozentsatz angewandt wird. Wenn gesetzt, rechnet das System den Prozentwert genau auf diese Basiszeile. |
| **Formel** | Nur bei Feldart **Zwischensumme** oder **Summe** aktiv: gibt über Zeilennummern (mit „+“ verknüpft) an, welche Zeilen kumuliert werden. Eine ungültige Formel wird beim Erfassen mit einer Fehlermeldung abgewiesen. |
| **Wert** | Der manuell erfasste Betrag (bei **Manueller Wert**) bzw. der berechnete Zeilenwert; steuert unmittelbar das Kalkulationsergebnis der Folgezeilen. |
| **Alt. Wert 1** … **Alt. Wert 4** | Alternative Werte je Zeile für parallele Rechenvarianten (z. B. unterschiedliche Szenarien). Wenn gefüllt, werden die alternativen Spalten in der Kalkulation mitberechnet. |
| **Zugeordneter berechneter Wert** | Ordnet eine manuelle Zeile einem Kostenblock zu, damit die Summe der Einzelkosten dem ausgewiesenen Einstandspreis entspricht. Werte siehe Optionsliste unten. Für die Feldarten **Summe**, **Zwischensumme** und **Berechneter Wert** ist eine Zuordnung nicht zulässig (Fehlermeldung). |
| **Fixer Wert** | Wenn aktiviert, ist der erfasste Wert fixiert und kann in der Kalkulation nicht mehr geändert werden; ohne Kennzeichen bleibt die Zeile in der Kalkulation editierbar. |
| **Im Hundert** | Wenn aktiviert, wird der Prozentsatz „im Hundert“ gerechnet (Wert = Basis × Prozent/(100−Prozent)) statt „vom Hundert“; damit lassen sich Aufschläge auf einen Zielpreis rückwärts ermitteln. |
| **Verwendungsart** | Kennzeichnet, welche Zeile das Endergebnis liefert. Werte siehe Optionsliste unten. Wird eine Verwendungsart neu gesetzt, entzieht das System sie automatisch der bisherigen Zeile (Meldung), damit **Einstandspreis** und **Verkaufspreis** jeweils genau einer Zeile zugeordnet bleiben. |

**Optionswerte:**

- **Feldart**
  - **Berechneter Wert:** Der Zeilenwert wird aus dem simulierten Fertigungsauftrag übernommen; das
    Feld **Berechneter Wert** wird auswählbar.
  - **Manueller Wert:** Der Anwender gibt den Betrag im Feld **Wert** direkt ein.
  - **Manuelle Prozentangabe:** Der Anwender gibt einen Prozentsatz ein; der Zeilenwert ergibt sich
    aus der **Berechnungsbasis** multipliziert mit dem Prozentsatz.
  - **Zwischensumme:** Der Wert wird aus den in der **Formel** genannten Zeilen gebildet
    (Teilsumme).
  - **Summe:** Der Wert kumuliert die in der **Formel** genannten Zeilen zur Gesamtsumme.
  - **Werkzeugkosten pro Einheit:** Der Wert ergibt sich aus **Werkzeugkosten** geteilt durch
    **Werkzeug-Standzeit** der Kalkulation.
- **Berechneter Wert**
  - **Materialkosten:** Sämtliche Kosten der eingesetzten Roh-, Hilfs- und Betriebsstoffe.
  - **Materialkosten ohne Ausschuss:** Reine Materialkosten ohne die durch Ausschuss verursachten
    Anteile.
  - **Materialgemeinkosten Einkaufsartikel:** Gemeinkostenaufschlag auf zugekaufte Komponenten.
  - **Kapazitätskosten:** Kosten der eingesetzten Fertigungskapazität (Arbeitsgänge).
  - **Kap. Gemeinkosten:** Kapazitive Gemeinkosten.
  - **Prod. Gemeinkosten:** Gemeinkosten der Produktion.
  - **Fremdarbeitskosten:** Kosten für Arbeitsschritte, die von einem Lieferanten übernommen
    werden.
  - **Arbeitsplanausschuss:** Der im Arbeitsplan hinterlegte Ausschussanteil der Arbeitsgänge.
- **Zugeordneter berechneter Wert**
  - **(leer):** Keine Zuordnung; die Zeile fließt nicht in die Einstandspreis-Kontrollsumme ein.
  - **Materialkosten / Kapazitätskosten / Fremdarbeitskosten / Kap. Gemeinkosten /
    Prod. Gemeinkosten:** Die manuelle Zeile wird dem jeweiligen Kostenblock zugerechnet, sodass die
    Summe der Einzelkosten mit dem ausgewiesenen **Einstandspreis** übereinstimmt.
- **Verwendungsart**
  - **Einstandspreis:** Diese Zeile liefert den kalkulierten Einstandspreis und wird beim
    Aktualisieren in den Artikel geschrieben.
  - **Verkaufspreis:** Diese Zeile liefert den kalkulierten Verkaufspreis und wird in die Belege
    bzw. Preislisten übernommen.

Die Vorlagenzeilen lassen sich auch über die eigenständige Übersicht **Kalkulationsvorlagenzeilen**
(Drilldown der Vorlagenzeilen) einsehen.

### Kalkulationsvorlagevorgaben einrichten (Profilermittlung)

Diese dedizierte Einrichtung stellt sicher, dass beim Anlegen einer Kalkulation aus einem Beleg
**automatisch** die richtige Kalkulationsvorlage vorgeschlagen wird. Sie wird vom Key-User
gepflegt, nachdem die **Kalkulationsvorlagen** existieren, und greift später im Tagesablauf bei
**Erstelle/Öffne Kalkulation**.

**Einstieg:** Öffnen Sie in der **Kalkulation Einrichtung** die Aktion
**Standardkalkulationsvorlagen**. Es öffnet sich die Seite **Kalkulationsvorlagevorgaben**.

**Process intro:** Über Kombinationen aus **Vorlagenart** (Debitorebene) und **Vorlagenunterart**
(Artikelebene) ordnet der Key-User jeder Konstellation eine **Kalkulationsvorlage** zu. Beim Öffnen
einer Kalkulation ermittelt das System anhand von **Kontaktnr.** und **Artikelnr.** die
passendste Vorgabe.

| Feld | Erläuterung |
|---|---|
| **Vorlagenart** | Legt die Debitorebene der Vorgabe fest. Werte siehe Optionsliste unten. Wird auf **Alle Debitoren** gewechselt, entfernt das System eine ggf. erfasste Debitorennr. automatisch. |
| **Debitorennr.** | Legt bei **Debitor** die Debitorennr. bzw. bei **Debitorenpreisgruppe** den Gruppencode fest. Wenn gesetzt, gilt die Vorgabe nur für diesen Debitor bzw. diese Preisgruppe; bei anderer Vorlagenart ist eine Eingabe nicht zulässig. |
| **Vorlagenunterart** | Legt die Artikelebene der Vorgabe fest. Werte siehe Optionsliste unten. Wird auf **Alle Artikel** gewechselt, entfernt das System eine ggf. erfasste Artikelnr. automatisch. |
| **Artikelnr.** | Legt bei **Artikel** die Artikelnr. fest, für die die Vorgabe gilt. Eine Eingabe ist nur zulässig, wenn die Vorlagenunterart **Artikel** ist. |
| **Kalkulationsvorlage** | Legt die Kalkulationsvorlage fest, die bei der gewählten Kombination automatisch vorgeschlagen wird. |

**Optionswerte:**

- **Vorlagenart**
  - **Alle Debitoren:** Die Vorgabe gilt debitorenübergreifend als Auffangregel.
  - **Debitor:** Die Vorgabe gilt für genau einen Debitor (in **Debitorennr.**).
  - **Debitorenpreisgruppe:** Die Vorgabe gilt für alle Debitoren einer Preisgruppe.
- **Vorlagenunterart**
  - **Alle Artikel:** Die Vorgabe gilt für alle Artikel des gewählten Debitorbereichs.
  - **Artikel:** Die Vorgabe gilt für genau einen Artikel (in **Artikelnr.**).

**Numerierte Ermittlung (Ablauf laut Code):** Beim Anlegen einer Kalkulation aus einem Beleg
sucht das System die Vorlage in dieser Reihenfolge:

1. **Zuerst** wird geprüft, ob eine Vorgabe mit **Vorlagenart = Debitor** und der **Debitorennr.**
   des Belegs existiert.
2. **Danach**, falls nicht gefunden, wird die **Debitorenpreisgruppe** des Debitors herangezogen
   (**Vorlagenart = Debitorenpreisgruppe**).
3. **Schließlich**, falls weiterhin nicht gefunden, greift die Auffangregel
   **Vorlagenart = Alle Debitoren**.
4. Innerhalb der gefundenen Debitorebene wird bei vorhandener **Artikelnr.** zuerst die Vorgabe
   für **Artikel** und andernfalls für **Alle Artikel** verwendet.

Die so ermittelte **Kalkulationsvorlage** wird in die Kalkulation übernommen; der Anwender kann sie
weiterhin manuell ändern. Diese Vorgaben sparen im Tagesablauf Zeit und erhöhen die Sicherheit,
weil das Rechenschema nicht bei jeder Kalkulation neu ausgewählt werden muss (Bezug zum Abschnitt
*Tägliche Arbeit: Kalkulation*).

### Verkaufspreisübernahme einrichten

Diese Einrichtung verbindet die **Kalkulation Einrichtung** mit dem Tagesablauf am Beleg. Sie
legt fest, ob und wann der kalkulierte Verkaufspreis den Verkaufsbeleg erreicht.

1. **Zuerst** setzt der Administrator in der **Kalkulation Einrichtung** das Feld
   **Verkaufspreis im Beleg setzen** auf **Beim Zertifizieren**, wenn die Preisübernahme
   automatisch erfolgen soll (bei **(leer)** bleibt sie manuell).
2. **Danach** wird beim Anlegen der Kalkulation aus dem Beleg automatisch eine **Belegzuordnung**
   angelegt (siehe *Belegzuordnung*), die Kalkulation und Verkaufsbelegzeile verknüpft.
3. **Operativer Abschluss:** Beim **Zertifizieren** schreibt das System den **Verkaufspreis** in
   die Zeilen der zugeordneten, noch **offenen** Verkaufsbelege. Alternativ löst der Anwender die
   Übernahme jederzeit manuell über **Verkaufspreis in Belege setzen** aus (siehe *Tägliche
   Arbeit*).

### Artikelbezug (Stammdaten am Artikel)

Das Modul erweitert die **Artikelkarte** um das Feld **Kalkulation Einstandspreis**. Der Wert wird
gepflegt, wenn eine zertifizierte Kalkulation über **Einstandspreis aktualisieren** den
Einstandspreis in den Artikel schreibt. Wenn gefüllt, dokumentiert das Feld den zuletzt aus einer
Kalkulation übernommenen Einstandspreis des Artikels; der Administrator muss es nicht manuell
pflegen. Damit ist am Artikel jederzeit nachvollziehbar, welcher kalkulierte Einstandspreis
zuletzt gültig war.

### Verkaufschance (Stammdaten-Bezug)

Auf der **Verkaufschance** (Opportunity Card) ergänzt das Modul das Feld **Kalkulation Artikelnr.**
sowie die Aktion **Erstelle/Öffne Kalkulation**.

| Feld | Erläuterung |
|---|---|
| **Kalkulation Artikelnr.** | Legt den Artikel fest, für den aus der Verkaufschance heraus kalkuliert werden soll. Wenn gesetzt, verwendet die Aktion **Erstelle/Öffne Kalkulation** diesen Artikel als Zielartikel der neuen Kalkulation. |

Der Vertriebsmitarbeiter pflegt die **Kalkulation Artikelnr.** in der Angebotsphase. Über
**Zeile/Aktion → Funktionen → Erstelle/Öffne Kalkulation** startet er die Kalkulation direkt aus
der Verkaufschance; eine **Belegzuordnung** mit Herkunft „Verkaufschance“ wird automatisch angelegt
(Bezug zum Abschnitt *Tägliche Arbeit*).

---

## Tägliche Arbeit: Kalkulation

Die eigentliche Kalkulation entsteht im Tagesgeschäft, meist ausgelöst aus einem Verkaufsbeleg.
Die verwendeten Vorgaben stammen aus der **Kalkulation Einrichtung** (Nummernserie,
Preisübernahme, Berichte) und aus den **Stammdaten** (Kalkulationsvorlage, Vorlagevorgaben) —
siehe Kapitel *Einrichtung* und *Stammdaten*.

### Einstieg über den Verkaufsbeleg

**Einstieg (Typ C – Aktion auf Belegzeile):** Öffnen Sie in der Zeile eines **Verkaufsauftrags**,
**Verkaufsangebots**, einer **Verkaufsrechnung** oder eines Rahmen-Verkaufsauftrags die Gruppe
**Zeile → Funktionen** und wählen Sie **Erstelle/Öffne Kalkulation**. Existiert zur Zeile bereits
eine Kalkulation, wird deren letzte Version geöffnet; andernfalls legt das System eine neue
**Kalkulation** mit fortlaufender **Nr.** an, übernimmt **Artikelnr.** und **Kontaktnr.** aus dem
Beleg und wählt über die **Kalkulationsvorlagevorgaben** die passende **Kalkulationsvorlage** vor.

Alternativ startet der Anwender die Kalkulation aus einer **Verkaufschance** über die dortige
Aktion **Erstelle/Öffne Kalkulation** (siehe *Verkaufschance*).

### Kalkulation – Karte

Die Seite **Kalkulation** ist der Hauptbeleg des Moduls. Sie gliedert sich in die Bereiche
**Allgemein**, die Zeilen (**Zeilen**), **Erweitert**, **Kontakt**, **Werte**, **Info** und
**Nachkalkulation**. Alle Felder sind nur im Status **In Entwicklung** editierbar.

#### Bereich Allgemein

| Feld | Erläuterung |
|---|---|
| **Nr.** | Fortlaufende Kalkulationsnummer aus der Nummernserie. Nur im Status **In Entwicklung** editierbar; über die Bearbeitungshilfe kann eine verbundene Nummernserie gewählt werden. |
| **Version** | Zeigt die Versionsnummer der Kalkulation. Mit **Neue Version erstellen** entsteht eine höhere Version; ältere zertifizierte Versionen können auf **Abgelaufen** gesetzt werden. |
| **Gültig von** / **Gültig bis** | Legen den Gültigkeitszeitraum der Kalkulation fest. Wenn gesetzt, steuern sie beim **Aktualisiere Verkaufspreisliste** den Zeitraum der zu aktualisierenden Verkaufspreiszeilen. |
| **Beschreibung** | Freitextbeschreibung der Kalkulation; wird beim Setzen der **Artikelnr.** ggf. aus der Artikelbeschreibung vorbelegt. |
| **Projekt** | Freitextfeld zur Zuordnung eines Projekts. Auch im Status **Zertifiziert** änderbar. |
| **Angebot** | Freitextfeld zur Zuordnung eines Angebots. Auch im Status **Zertifiziert** änderbar. |
| **Kalkulationsvorlage** | Legt das Berechnungsschema fest. Beim Ändern werden bestehende Kalkulationszeilen nach Rückfrage gelöscht und aus der neuen Vorlage neu erzeugt; anschließend wird neu berechnet. |
| **Artikelnr.** | Legt den zu kalkulierenden Artikel fest. Wenn gesetzt (und ungleich Dummy-Artikel), wird **Artikel angelegt** aktiviert, Arbeitsplan und Fertigungsstückliste des Artikels werden in den simulierten Fertigungsauftrag übernommen und die Zeilen werden berechnet. |
| **Mehrstufige Kalkulation** | Wenn aktiviert, berechnet das System zunächst den Standard-Einstandspreis des Artikels (mehrstufig über die Stückliste) und verwendet diesen als Materialkosten der Kalkulation; ohne Kennzeichen werden die Materialkosten direkt aus dem simulierten Fertigungsauftrag übernommen. |
| **Artikel angelegt** | Zeigt an, ob aus der Kalkulation heraus bereits ein realer Artikel erzeugt wurde (nur Anzeige). |
| **Status** | Steuert den Lebenszyklus der Kalkulation. Werte siehe Optionsliste unten. Ein direktes Setzen auf **Zertifiziert** über das Feld ist gesperrt; hierfür ist die Aktion **Kalkulation zertifizieren** zu verwenden. |

**Optionswerte – Status:**

- **In Entwicklung:** Die Kalkulation ist in Bearbeitung; alle Werte sind editierbar, es kann neu
  berechnet werden.
- **Zertifiziert:** Die Kalkulation ist freigegeben und schreibgeschützt; Preise können nicht mehr
  geändert werden. Erst in diesem Status sind **Artikel anlegen**, **Einstandspreis
  aktualisieren** und **Aktualisiere Verkaufspreisliste** möglich.
- **Abgelaufen:** Die Kalkulation ist geschlossen und wird nur noch historisch geführt.

#### Bereich Zeilen (Kalkulationsschema)

Die Zeilen entsprechen dem Schema der gewählten Kalkulationsvorlage und werden **von oben nach
unten** abgearbeitet. Editierbar sind je nach **Feldart** nur die passenden Wert- oder
Prozentfelder; **Summen** und **Zwischensummen** werden vom System berechnet und fett dargestellt.

| Feld | Erläuterung |
|---|---|
| **Beschreibung** | Bezeichnung der Zeile aus der Vorlage; Summen-/Zwischensummenzeilen werden hervorgehoben. |
| **Feldart** | Zeigt die aus der Vorlage übernommene Art der Zeile (siehe Optionswerte im Abschnitt *Kalkulationsvorlagen*). |
| **Berechneter Wert** | Zeigt bei berechneten Zeilen den herangezogenen Kostenbestandteil. |
| **Prozent** | Bei **Manuelle Prozentangabe** editierbar: der Prozentsatz, der auf die Berechnungsbasis angewandt wird. Eine Änderung löst die Neuberechnung der Folgezeilen aus. |
| **Wert** | Bei **Manueller Wert** editierbar bzw. berechneter Zeilenwert; steuert das Ergebnis der Folgezeilen. |
| **Alt. Prozent 1** … **Alt. Prozent 4** | Alternative Prozentsätze für die parallelen Rechenvarianten (nur bei Prozentzeilen editierbar). |
| **Alt. Wert 1** … **Alt. Wert 4** | Alternative Werte der parallelen Rechenvarianten (nur bei Wertzeilen editierbar). |

Sind Werte oder Prozentsätze **fix** gesetzt (Vorlagenkennzeichen **Fixer Wert**), sind die
entsprechenden Felder in der Kalkulation gesperrt.

#### Bereich Erweitert

| Feld | Erläuterung |
|---|---|
| **Arbeitsplannr.** | Legt den Arbeitsplan fest, aus dem Kapazitätskosten und Arbeitsplanausschuss ermittelt werden. Beim Ändern wird der simulierte Fertigungsauftrag neu aufgebaut und neu berechnet. |
| **Fert.-Stücklistennr.** | Legt die Fertigungsstückliste fest, aus der die Materialkomponenten und -kosten stammen. Beim Ändern werden Komponenten und Kosten neu ermittelt. |
| **Losgröße** | Legt die Auftragsmenge fest (Mindestwert 1), auf die die Kosten bezogen werden. Beim Ändern werden der simulierte Fertigungsauftrag und die Zeilen neu berechnet (Kosten pro Stück). |
| **Mat.-Gemeinkosten % EK-Artikel** | Legt den Prozentsatz für Materialgemeinkosten auf zugekaufte Komponenten fest; steuert die Höhe der **Mat.-Gemeinkosten EK-Artikel**. |
| **Werkzeugkosten** | Legt die gesamten Werkzeugkosten fest; zusammen mit der **Werkzeug-Standzeit** ergibt sich der Wert einer Zeile vom Typ **Werkzeugkosten pro Einheit**. Eine Änderung erzwingt eine Neuberechnung. |
| **Werkzeug-Standzeit** | Legt fest, über wie viele Einheiten die Werkzeugkosten verteilt werden (Werkzeugkosten ÷ Standzeit = Werkzeugkosten pro Einheit). |
| **Interne Bemerkung** | Freitext für interne Hinweise; auch im Status **Zertifiziert** änderbar. |

#### Bereich Kontakt

| Feld | Erläuterung |
|---|---|
| **Kontaktart** | Legt fest, gegen welche Stammdaten die **Kontaktnr.** geprüft wird. Werte: **Debitor** (Prüfung/Herkunft aus der Debitorenübersicht) oder **Kontakt** (aus der Kontaktübersicht). Beim Wechsel wird eine bestehende Kontaktnr. zurückgesetzt. |
| **Kontaktnr.** | Legt den Debitor bzw. Kontakt der Kalkulation fest. Bei **Debitor** löst die Eingabe die automatische Ermittlung der Kalkulationsvorlage über die Vorgaben aus (siehe *Kalkulationsvorlagevorgaben einrichten*). |
| **Referenznr.** | Freitextfeld für eine externe Referenz; auch im Status **Zertifiziert** änderbar. |
| **Referenzdatum** | Datum der externen Referenz; auch im Status **Zertifiziert** änderbar. |

**Optionswerte – Kontaktart:** **Debitor:** Kontaktnr. wird aus der Debitorenübersicht gewählt und
löst die Vorlagenermittlung aus. **Kontakt:** Kontaktnr. wird aus der Kontaktübersicht gewählt.

#### Bereich Werte

Alle Wertfelder sind Ergebnisfelder (nur Anzeige) und werden bei jeder Neuberechnung aktualisiert.

| Feld | Erläuterung |
|---|---|
| **Materialkosten** | Ermittelte Materialkosten je Stück aus dem simulierten Fertigungsauftrag. |
| **Materialkosten ohne Ausschuss** | Materialkosten ohne den durch Ausschuss verursachten Anteil. |
| **Mat.-Gemeinkosten EK-Artikel** | Auf zugekaufte Komponenten aufgeschlagene Materialgemeinkosten (abhängig von Einrichtung und Vorlagenprozentsatz). |
| **Kapazitätskosten** | Kosten der eingesetzten Fertigungskapazität aus den Arbeitsgängen. |
| **Kap. Gemeinkosten** | Kapazitive Gemeinkosten. |
| **Prod. Gemeinkosten** | Produktionsgemeinkosten. |
| **Fremdarbeitskosten** | Kosten fremdvergebener Arbeitsschritte. |
| **Arbeitsplanausschuss** | Kostenanteil des im Arbeitsplan hinterlegten Ausschusses. |
| **Einstandspreis** | Kalkulierter Einstandspreis (aus der Zeile mit Verwendungsart **Einstandspreis**); wird beim Aktualisieren in den Artikel geschrieben. |
| **Verkaufspreis** | Kalkulierter Verkaufspreis (aus der Zeile mit Verwendungsart **Verkaufspreis**); wird in Belege bzw. Preislisten übernommen. |
| **Marge %** | Relative Marge in Prozent zwischen Einstands- und Verkaufspreis. |

#### Bereich Info

| Feld | Erläuterung |
|---|---|
| **Sim. Fertigungsauftrag** | Zeigt die Nummer des im Hintergrund geführten simulierten Fertigungsauftrags, aus dem die Kosten ermittelt werden (nur Anzeige). |
| **Zuletzt berechnet am** | Zeitpunkt der letzten Berechnung (nur Anzeige). |
| **Zuletzt berechnet von** | Benutzer der letzten Berechnung (nur Anzeige). |
| **Batch-Kalkulation** | Zeigt an, ob die Kalkulation im Rahmen einer **Batch-Kalkulation** erzeugt/aktualisiert wurde (nur Anzeige). |

#### Bereich Nachkalkulation

Die **Nachkalkulation** stellt die kalkulierten Werte den tatsächlichen Kosten eines
**abgeschlossenen (fertig gemeldeten) Fertigungsauftrags** gegenüber. Der Anwender wählt den
Fertigungsauftrag und die Auftragszeile; das System ermittelt die Istkosten und schreibt sie in
die Nachkalkulationsfelder.

| Feld | Erläuterung |
|---|---|
| **Nachkalkulation Fertigungsauftrag** | Legt den abgeschlossenen Fertigungsauftrag fest, gegen den nachkalkuliert wird. |
| **Nachkalkulation Fertigungsauftragszeile** | Legt die Auftragszeile fest; beim Setzen löst das System die Nachkalkulation aus. Stimmt die Artikelnr. der Zeile nicht mit der Kalkulation überein, erscheint eine Fehlermeldung. |
| **Nachkalkulation Materialkosten** | Tatsächliche Materialkosten je gefertigter Einheit. |
| **Nachkalkulation Materialkosten ohne Ausschuss** | Tatsächliche Materialkosten ohne Ausschussanteil. |
| **Nachkalkulation Materialgemeinkosten Einkaufsartikel** | Tatsächliche Materialgemeinkosten für zugekaufte Komponenten. |
| **Nachkalkulation Kapazitätskosten** | Tatsächliche Kapazitätskosten. |
| **Nachkalkulation Kapazitäts-Gemeinkosten** | Tatsächliche kapazitive Gemeinkosten. |
| **Nachkalkulation Fertigungsallgemeinkosten** | Tatsächliche Produktionsgemeinkosten. |
| **Nachkalkulation Fremdarbeitskosten** | Tatsächliche Fremdarbeitskosten. |
| **Nachkalkulation Arbeitplan Ausschuss** | Tatsächlicher Arbeitsplanausschuss (aus den Kapazitätsposten). |

### Aktionen der Kalkulation

Die folgenden Aktionen stehen in der Kalkulation zur Verfügung (Reihenfolge entspricht dem
typischen Ablauf).

| Aktion | Erläuterung |
|---|---|
| **Versionen** | Öffnet die Liste aller Versionen der Kalkulation. |
| **Komponenten** | Öffnet die Seite **Kalkulation Komponenten** mit den Materialkomponenten des simulierten Fertigungsauftrags (Reservierung, Artikelverfügbarkeit, Ersatzartikel u. a.). |
| **Arbeitsplanzeilen** | Öffnet die Arbeitsgänge des simulierten Fertigungsauftrags; nach dem Bearbeiten wird neu geplant und neu berechnet. |
| **Kalkulation zertifizieren** | Setzt den Status auf **Zertifiziert** und sperrt die Werte (siehe *Buchungs- bzw. Freigabeablauf*). |
| **Bearbeiten** | Öffnet die Seite **Kalkulation bearbeiten**, auf der auch bei zertifizierten Kalkulationen die zulässigen Felder (Beschreibung, Projekt, Angebot, Referenz, Interne Bemerkung) geändert werden können. |
| **Kalkulation schliessen** | Setzt eine zertifizierte Kalkulation auf **Abgelaufen**. |
| **Kalkulation kopieren** | Kopiert eine bestehende Kalkulation in eine neue Kalkulation (Auswahl aus der Übersicht). |
| **Neue Version erstellen** | Legt eine neue Version der aktuellen Kalkulation an. |
| **Artikel anlegen** | Erzeugt aus einer zertifizierten Kalkulation einen neuen Artikel (siehe *Artikel anlegen*). |
| **Preis in Artikelkarte setzen** | Schreibt den kalkulierten **Verkaufspreis** in das Feld **VK-Preis** der Artikelkarte. |
| **Einstandspreis aktualisieren** | Schreibt den kalkulierten **Einstandspreis** in den Artikel und die zugehörigen Lagerhaltungsdaten. |
| **Aktualisiere Verkaufspreisliste** | Überträgt den kalkulierten **Verkaufspreis** in die passenden Verkaufspreiszeilen (Preisliste) im Gültigkeitszeitraum. |
| **Belegzuweisung** | Öffnet die **Kalkulation Belegzuordnungen** mit den verknüpften Belegen. |
| **Verkaufspreis in Belege setzen** | Überträgt den kalkulierten **Verkaufspreis** in die Zeilen der zugeordneten, noch offenen Verkaufsbelege. |
| **Drucken** | Druckt den in der Einrichtung hinterlegten **Bericht Kalkulation** (und optional den **FA-Bericht**). |

### Buchungs- bzw. Freigabeablauf (Zertifizieren)

Das Modul kennt keine Beleg- oder Lagerbuchung. Der Freigabe- und Abschlussschritt ist das
**Zertifizieren**, das die Kalkulation sperrt und – je nach Einrichtung – den Verkaufspreis in die
Belege überträgt. Der Ablauf (aus dem Code abgeleitet):

1. Zeile auf **Kalkulationen** wählen oder Kalkulation aus dem Beleg öffnen.
2. Werte/Zeilen pflegen und ggf. **Einstandspreis aktualisieren**, bis die Kalkulation berechnet
   ist.
3. **Kalkulation zertifizieren** wählen. Prüfungen: Der Status muss **In Entwicklung** sein, die
   Kalkulation muss berechnet sein, und es dürfen keine Komponenten vom Typ **Kalkulation**
   vorhanden sein (andernfalls Abbruch mit Meldung). Existieren weitere zertifizierte Versionen,
   fragt das System, ob diese auf **Abgelaufen** gesetzt werden sollen.
4. Ist in der Einrichtung **Verkaufspreis im Beleg setzen = Beim Zertifizieren** gesetzt, überträgt
   das System den Verkaufspreis automatisch in die offenen zugeordneten Verkaufsbelege
   (versteckter Hintergrundprozess, kein Fenster).
5. Nach der Zertifizierung sind je nach Bedarf **Preis in Artikelkarte setzen**, **Einstandspreis
   aktualisieren**, **Aktualisiere Verkaufspreisliste**, **Verkaufspreis in Belege setzen** oder
   **Artikel anlegen** möglich.
6. Mit **Kalkulation schliessen** wird die zertifizierte Kalkulation auf **Abgelaufen** gesetzt.

### Artikel anlegen

Aus einer **zertifizierten** Kalkulation erzeugt der Anwender über **Artikel anlegen** einen realen
Artikel samt Arbeitsplan und Fertigungsstückliste. Es öffnet sich der Dialog **Artikel anlegen**.

| Feld | Erläuterung |
|---|---|
| **Nr.** | Nummer des neuen Artikels; über die Bearbeitungshilfe kann eine Nummernserie gezogen werden. Bei bereits vorhandenem Artikel gesperrt. |
| **Beschreibung** / **Beschreibung 2** | Bezeichnung des neuen Artikels; wird bei leerer Angabe aus der Kalkulation vorbelegt. |
| **Artikel anlegen** (Kennzeichen) | Wenn aktiviert, wird ein neuer Artikel aus der **Vorlage Artikel** erzeugt; existiert der Artikel bereits, ist das Kennzeichen gesperrt und der Hinweis **Artikel bereits angelegt** erscheint. |
| **Vorlage Artikel** | Legt die Artikelvorlage (Konfigurationsvorlage) fest, aus der die Stammdaten übernommen werden. Ohne Vorlage wird das Anlegen mit einer Meldung abgebrochen. |
| **Arbeitsplan anlegen** (Kennzeichen) | Wenn aktiviert, wird aus den Arbeitsgängen des simulierten Fertigungsauftrags ein Arbeitsplan erzeugt; besitzt der Artikel bereits einen Arbeitsplan, ist das Kennzeichen gesperrt (**Arbeitsplan bereits angelegt**). |
| **Stückliste anlegen** (Kennzeichen) | Wenn aktiviert, wird aus den Komponenten des simulierten Fertigungsauftrags eine Fertigungsstückliste erzeugt; existiert bereits eine, ist das Kennzeichen gesperrt (**Fertigungsstückliste bereits angelegt**). |

Nach Bestätigung mit **OK** legt das System den Artikel an, überträgt den Einstandspreis und
ersetzt – sofern die Kalkulation als Komponente in anderen Kalkulationen verwendet wird – dort die
Kalkulationskomponente durch den neuen Artikel.

---

## Batch-Kalkulation

Die **Batch-Kalkulation** dient der Massenermittlung bzw. Aktualisierung von Einstandspreisen über
das **Kalkulation Batch Buch.-Blatt**. Sie greift auf die in der **Kalkulation Einrichtung**
hinterlegte **Batch Kalkulationsvorlage** zurück.

**Einstieg:** Öffnen Sie über **Suchen** das **Kalkulation Batch Buch.-Blatt** (Aufgabenseite). Das
Buch.-Blatt ist je Benutzer gefiltert.

**Ablauf:**

1. **Kalkulationen sammeln** — sammelt die zu kalkulierenden Artikel in Batchzeilen (inklusive
   Stücklistenebene und Verwendungen).
2. Je Zeile die **Aktion** wählen (siehe Optionswerte) und ggf. **Neue Kalkulationsvorlage**,
   **Neue Losgröße** und weitere Vorgaben setzen.
3. **Zeile prüfen** — prüft eine fehlerhafte Zeile erneut; über **Fehler anzeigen** und
   **Verwendung anzeigen** lassen sich Details einsehen.
4. **Kalkulation/Einstandspreise setzen** — führt die Kalkulationen für die Batchzeilen durch und
   setzt die Einstandspreise.

Wichtige Felder der Batchzeile:

| Feld | Erläuterung |
|---|---|
| **Fehler** | Zeigt an, ob die Zeile einen Fehler enthält; eine Aktion ungleich **Keine** ist nur bei fehlerfreier Zeile zulässig. |
| **Aktion** | Legt fest, was mit der Zeile geschehen soll. Werte siehe Optionsliste unten. |
| **Artikelnr.** | Der zu kalkulierende Artikel (Anzeige). |
| **Aktuelle Kalkulationsnr.** / **Aktuelle Kalkulationsversion** | Verweisen auf die derzeit gültige Kalkulation des Artikels. |
| **Kalkulationsvorlage** / **Neue Kalkulationsvorlage** | Bisherige bzw. für die neue Kalkulation zu verwendende Vorlage. |
| **Neue Kalkulationsnr.** / **Neue Kalkulationsversion** | Ergebnis der Batchverarbeitung. |
| **Einstandspreis** / **Neuer Einstandspreis** / **Einstandspreisdifferenz** | Alter und neuer Einstandspreis sowie deren Differenz. |
| **Verwendungen vorhanden** | Zeigt an, ob der Artikel als Komponente in anderen Kalkulationen verwendet wird. |

**Optionswerte – Aktion:**

- **Keine:** Die Zeile wird nicht verarbeitet.
- **Neue Version:** Für den Artikel wird eine neue Version der bestehenden Kalkulation erstellt.
- **Neue Kalkulation:** Für den Artikel wird eine völlig neue Kalkulation angelegt.

Über **Fehler anzeigen** öffnet sich die Seite **Kalkulation Batch Fehler** mit der jeweiligen
**Fehlerart**:

- **Keine Fert.-Stückliste / Kein Arbeitsplan:** Dem Artikel ist keine Fertigungsstückliste bzw.
  kein Arbeitsplan zugeordnet.
- **Keine zert. Fert.-Stückliste / Kein zert. Arbeitsplan:** Es existiert keine zertifizierte
  Fertigungsstückliste bzw. kein zertifizierter Arbeitsplan.
- **Einstandspreisabweichung:** Die Summe der Einzelkosten entspricht nicht dem Einstandspreis.
- **Einstandspreis 0:** Der ermittelte Einstandspreis ist 0.
- **Lagerabgangsmethode (Artikelposten):** Die Lagerabgangsmethode ist nicht „Standard“ und es
  existieren Artikelposten.
- **Lagerabgangsmethode (Bestellungen):** Die Lagerabgangsmethode ist nicht „Standard“ und es
  existieren offene Bestellungen.

Über **Verwendung anzeigen** öffnet die Seite **Kalkulation Batch Verwendungen** die Zeilen, in
denen der Artikel als Komponente verwendet wird.

---

## Belegzuordnung

Die **Kalkulation Belegzuordnungen** verknüpfen eine Kalkulation mit den Belegen, aus denen sie
entstanden ist bzw. für die der Preis gesetzt werden soll. Sie werden beim **Erstelle/Öffne
Kalkulation** automatisch angelegt und sind Grundlage für **Verkaufspreis in Belege setzen**.

**Einstieg:** In der Kalkulation über die Aktion **Belegzuweisung**.

| Feld | Erläuterung |
|---|---|
| **Beleg** | Zeigt die Bezeichnung des zugeordneten Belegs (Anzeige). |
| **Belegart** | Zeigt die Art des zugeordneten Belegs (Anzeige). |
| **Belegnr.** | Nummer des zugeordneten Belegs. |
| **Belegzeilen-Nr.** | Zeilennummer der zugeordneten Belegzeile. |
| **Zuordnungsdatum** | Datum der Zuordnung. |
| **Abgelaufen** | Wenn gesetzt, wird die Zuordnung bei der Preisübernahme nicht mehr berücksichtigt. |
| **Primäre Herkunft** | Kennzeichnet die ursprüngliche Herkunftszeile der Kalkulation. |

Aktionen: **Beleg anzeigen** öffnet den zugeordneten Beleg; über **Funktionen** lassen sich mit
**Verkaufsangebotszeile zuordnen** bzw. **Verkaufsauftragszeile zuordnen** weitere Belegzeilen
manuell mit der Kalkulation verknüpfen.

---

## Bericht und Ausgaben

Über die Aktion **Drucken** (in der **Kalkulation** und in der Liste **Kalkulationen**) wird der in
der **Kalkulation Einrichtung** hinterlegte **Bericht Kalkulation** ausgegeben. Ist zusätzlich ein
**FA Bericht** hinterlegt, wird auch dieser für den simulierten Fertigungsauftrag gedruckt. Über
die Einrichtungskennzeichen **Kalkulation Druckfilterseite anzeigen** und **FA Druckfilterseite
anzeigen** steuert der Administrator, ob vor dem Druck die jeweilige Anfrageseite erscheint. Der
Kalkulationsbericht enthält die Kalkulationszeilen und – über die Option **Bemerkungen drucken** –
optional die erfassten Bemerkungen.

---

## FAQ und Troubleshooting

### Warum lässt sich keine Kalkulation anlegen?
Ohne hinterlegte **Kalkulations-Nr.** (Nummernserie) sowie **Dummy Artikel-Nr.** und
**Dummy Arbeitsplannr.** in der **Kalkulation Einrichtung** bricht das Anlegen ab, weil das Modul
im Hintergrund einen simulierten Fertigungsauftrag mit Artikel und Arbeitsplan erzeugt. Pflegen Sie
diese Felder zuerst.

### Warum wird beim Öffnen aus dem Beleg keine Kalkulationsvorlage vorgeschlagen?
Die automatische Vorbelegung greift nur, wenn in den **Kalkulationsvorlagevorgaben** eine passende
Kombination aus **Vorlagenart** (Debitor, Debitorenpreisgruppe oder Alle Debitoren) und
**Vorlagenunterart** (Artikel oder Alle Artikel) mit einer **Kalkulationsvorlage** hinterlegt ist.
Fehlt eine Vorgabe, wählen Sie die Vorlage in der Kalkulation manuell.

### Was passiert, wenn ich die Kalkulationsvorlage in einer bestehenden Kalkulation ändere?
Das System weist darauf hin, dass die vorhandenen Kalkulationszeilen gelöscht werden, und legt nach
Bestätigung die Zeilen aus der neuen Vorlage neu an. Bestätigen Sie nur, wenn Sie das bisherige
Schema verwerfen möchten.

### Warum kann ich die Kalkulation nicht zertifizieren?
Das Zertifizieren setzt voraus, dass der Status **In Entwicklung** ist und die Kalkulation
berechnet wurde. Enthält der simulierte Fertigungsauftrag Komponenten vom Typ **Kalkulation**,
bricht das System das Zertifizieren ab; lösen Sie diese Komponenten zuerst auf (z. B. über
**Artikel anlegen**).

### Warum meldet das System, dass die Summe nicht dem Einstandspreis entspricht?
Beim Aktualisieren des Einstandspreises prüft das System, ob die Summe der Einzelkosten (inklusive
der über **Zugeordneter berechneter Wert** zugeordneten Zeilen) dem ausgewiesenen **Einstandspreis**
entspricht. Weicht sie ab, korrigieren Sie die Zuordnung der manuellen Zeilen in der
Kalkulationsvorlage.

### Warum ist der Einstandspreis 0 und die Aktualisierung schlägt fehl?
Ist der kalkulierte **Einstandspreis** 0, bricht **Einstandspreis aktualisieren** mit einer Meldung
ab. Prüfen Sie, ob Arbeitsgänge und Komponenten vorhanden sind und die Zeile mit Verwendungsart
**Einstandspreis** korrekt gefüllt ist.

### Wie wird der Verkaufspreis automatisch in den Verkaufsauftrag gesetzt?
Setzen Sie in der **Kalkulation Einrichtung** das Feld **Verkaufspreis im Beleg setzen** auf
**Beim Zertifizieren**. Beim Zertifizieren schreibt das System den Verkaufspreis in die Zeilen der
zugeordneten, noch offenen Verkaufsbelege. Alternativ nutzen Sie jederzeit **Verkaufspreis in
Belege setzen**.

### Warum wird der Preis in einem bereits freigegebenen/gebuchten Beleg nicht aktualisiert?
Der Verkaufspreis wird nur in zugeordnete Verkaufsbelege übernommen, deren Status **offen** ist.
Ist der Beleg nicht mehr offen, bleibt der Preis unverändert.

### Was bewirkt „Mehrstufige Kalkulation“?
Bei aktivierter **Mehrstufiger Kalkulation** berechnet das System zunächst den mehrstufigen
Standard-Einstandspreis des Artikels über die Stückliste und verwendet diesen als Basis der
Materialkosten. Ohne das Kennzeichen stammen die Materialkosten direkt aus dem simulierten
Fertigungsauftrag.

### Kann ich den simulierten Fertigungsauftrag löschen?
Nein. Der simulierte Fertigungsauftrag kann nicht gelöscht werden, solange seine Basis eine
Kalkulation ist. Löschen Sie stattdessen die Kalkulation; der zugehörige simulierte
Fertigungsauftrag wird dabei mit entfernt. Eine zertifizierte Kalkulation lässt sich nicht löschen.

---

## Typische Anwendungsfälle

### 1. Kalkulation aus dem Verkaufsauftrag

**Auslöser:** Ein Kunde fragt einen zu fertigenden Artikel an; der Vertrieb hat bereits einen
Verkaufsauftrag mit Artikel und Menge erfasst und benötigt einen belastbaren Verkaufspreis.

**Einstieg in BC:** Der Anwender öffnet den **Verkaufsauftrag**, markiert die Zeile und wählt
**Zeile → Funktionen → Erstelle/Öffne Kalkulation**. Es öffnet sich eine neue **Kalkulation** mit
vorbelegter **Artikelnr.**, **Kontaktnr.** (Debitor des Auftrags) und – sofern eine Vorgabe
existiert – vorbelegter **Kalkulationsvorlage**.

**Kernablauf:**
1. Bei Bedarf **Kalkulationsvorlage**, **Losgröße** und **Werkzeugkosten** anpassen.
2. In den **Zeilen** die manuellen Werte/Prozentsätze pflegen; das System berechnet Einstands- und
   Verkaufspreis fortlaufend.
3. **Kalkulation zertifizieren**.
4. **Verkaufspreis in Belege setzen** (oder – bei Einrichtung **Beim Zertifizieren** – automatisch)
   überträgt den Verkaufspreis in die Auftragszeile.

**Abschluss:** Der Verkaufsauftrag enthält den kalkulierten Verkaufspreis; über **Drucken** kann
der Kalkulationsbericht ausgegeben werden.

### 2. Kalkulation aus der Verkaufsrechnung (Preis erst in der Rechnung)

**Auslöser:** Der Verkaufspreis soll erst in der Verkaufsrechnung endgültig gesetzt werden, weil er
sich aus der Kalkulation ergibt.

**Einstieg in BC:** In der Zeile der **Verkaufsrechnung** wählt der Anwender
**Zeile → Funktionen → Erstelle/Öffne Kalkulation**.

**Kernablauf:**
1. Kalkulation pflegen und berechnen lassen.
2. **Kalkulation zertifizieren**.
3. **Verkaufspreis in Belege setzen** überträgt den kalkulierten Verkaufspreis in die offene
   Rechnungszeile.

**Abschluss:** Die Verkaufsrechnung trägt den kalkulierten Verkaufspreis; die **Belegzuordnung**
dokumentiert die Verknüpfung zwischen Kalkulation und Rechnungszeile.

### 3. Massenaktualisierung über die Batch-Kalkulation

**Auslöser:** Nach geänderten Material- oder Kapazitätskosten sollen die Einstandspreise mehrerer
gefertigter Artikel neu ermittelt werden.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** das **Kalkulation Batch Buch.-Blatt**.

**Kernablauf:**
1. **Kalkulationen sammeln** füllt die Batchzeilen.
2. Je Zeile die **Aktion** (**Neue Version** oder **Neue Kalkulation**) und die **Neue
   Kalkulationsvorlage** setzen.
3. Über **Zeile prüfen**, **Fehler anzeigen** und **Verwendung anzeigen** Fehler bereinigen.
4. **Kalkulation/Einstandspreise setzen** führt die Kalkulationen durch und aktualisiert die
   Einstandspreise.

**Abschluss:** Die neuen Einstandspreise stehen an den Artikeln; die Spalte
**Einstandspreisdifferenz** dokumentiert die Veränderung je Zeile.
