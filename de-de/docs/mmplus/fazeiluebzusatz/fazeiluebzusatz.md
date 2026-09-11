---
title: Anwenderhandbuch m+m Production Order Overview with Ext. Prod. Information
---

# Anwenderhandbuch m+m Production Order Overview with Ext. Prod. Information

## Einleitung

Die App **m+m Production Order Overview with Ext. Prod. Information** ergänzt die
Fertigungsauftrags-Zeilenübersicht Ihres Unternehmens um eine zusätzliche Infobox mit den
**Erweiterten Fertigungseigenschaften**. Wenn Sie eine Fertigungsauftragszeile in der Liste
**FA-Zeilenübersicht** markieren, blendet die App auf der rechten Seite die Infobox
**Erw. Fertigungseigenschaften** ein und zeigt dort die zur markierten Zeile gehörenden
Eigenschaften und deren Werte an.

Die App fügt der bestehenden Liste **keine** eigenen Spalten, Aktionen, Berichte oder
Einrichtungsseiten hinzu. Ihr einziger sichtbarer Beitrag ist diese Infobox. Die angezeigten
Eigenschaften selbst werden nicht in dieser App gepflegt, sondern stammen aus den erweiterten
Fertigungsinformationen, die zuvor an den Arbeitsplatzgruppen bzw. Arbeitsplänen hinterlegt und über
den Arbeitsplan in den Fertigungsauftrag übernommen wurden.

**Zielgruppe:** Primär die operativen Anwender in der Fertigungssteuerung und Arbeitsvorbereitung, die
täglich mit Fertigungsaufträgen arbeiten und beim Betrachten einer Auftragszeile sofort die zugehörigen
technischen Eigenschaften (Soll- und Istwerte) einsehen möchten. Sekundär betrifft es Administratoren,
die die zugrunde liegenden Eigenschaften in den vorgelagerten Modulen einrichten.

**Kurzer Prozessüberblick:**

1. Ein Administrator hinterlegt die erweiterten Fertigungseigenschaften an Arbeitsplatzgruppen bzw.
   Arbeitsplänen (in den vorgelagerten Modulen; siehe Abschnitt *Woher die angezeigten Eigenschaften
   stammen*).
2. Beim Anlegen bzw. Berechnen eines Fertigungsauftrags werden diese Informationen in den Arbeitsplan
   des Fertigungsauftrags übernommen.
3. Der Anwender öffnet die **FA-Zeilenübersicht**, markiert eine Zeile und liest die Werte in der
   Infobox **Erw. Fertigungseigenschaften** ab.

## Schnellstart für Anwender

Der schnellste Weg zu den erweiterten Fertigungseigenschaften einer Auftragszeile:

1. Öffnen Sie über **Suchen** die Seite **FA-Zeilenübersicht**.
2. Markieren Sie in der Liste die gewünschte Fertigungsauftragszeile (Zeilen sind an den Spalten
   **Status**, **FA-Nr.** und **Artikelnr.** erkennbar).
3. Lesen Sie rechts in der Infobox **Erw. Fertigungseigenschaften** die zur Zeile gehörenden
   Eigenschaften ab. Je markierter Zeile zeigt die Infobox automatisch die passenden Werte an; ein
   gesonderter Aufruf ist nicht nötig.
4. Vergleichen Sie bei Bedarf den vorgegebenen **Standardwert** mit dem tatsächlich erfassten **Wert**
   bzw. **Istwert** der Eigenschaft.

Da die App keine Buchungs-, Freigabe- oder Abschlussfunktion enthält, endet der Schnellstart mit dem
Ablesen der Werte. Es gibt keine weiteren Pflichtschritte in dieser App.

## Erw. Fertigungseigenschaften – die Infobox im Detail

Die Infobox **Erw. Fertigungseigenschaften** ist der eigentliche Funktionsumfang dieser App. Sie ist
eine reine Anzeige-Infobox: Die App bindet sie an die aktuell markierte Fertigungsauftragszeile und
filtert die zugehörigen Eigenschaften automatisch anhand von Fertigungsauftragsstatus,
Fertigungsauftragsnummer und Zeilennummer. Sie müssen dazu nichts eingeben.

Die folgende Tabelle beschreibt alle Felder, die die Infobox je Eigenschaftszeile ausweist.

| Feld | Erläuterung |
|------|-------------|
| **Arbeitsgangnr.** | Wenn die Eigenschaft einem bestimmten Arbeitsgang des Arbeitsplans zugeordnet ist, dann sehen Sie hier dessen Nummer; so erkennen Sie, an welcher Stelle der Fertigung die Eigenschaft gilt. Bei nicht arbeitsgangbezogenen Eigenschaften bleibt das Feld leer. |
| **Beschreibung** | Wenn ein Beschreibungstext hinterlegt ist, dann zeigt dieses Feld den Klartext zur Eigenschaft bzw. zum Arbeitsgang; der Anwender muss die Bedeutung nicht aus dem Code ableiten. |
| **Eigenschaftscode** | Der eindeutige Code der Eigenschaft. Wenn Sie eine Zeile lesen, dann identifiziert dieser Code, um welches technische Merkmal es sich handelt (z. B. eine Abmessung oder Materialangabe). |
| **Standardwert** | Wenn für die Eigenschaft ein Vorgabewert aus den Stammdaten übernommen wurde, dann steht er hier; er dient als Referenz, gegen die Sie den tatsächlichen Wert prüfen. |
| **Wert** | Wenn für diese Auftragszeile ein konkreter Wert der Eigenschaft ermittelt wurde, dann steht er hier. Weicht der **Wert** vom **Standardwert** ab, so wurde für diesen Auftrag bewusst ein anderer Wert gesetzt. |
| **Istwert** | Wenn während der Fertigung ein tatsächlich erreichter Wert erfasst wurde, dann sehen Sie ihn hier; dadurch können Sie Soll (Standardwert/Wert) und Ist unmittelbar vergleichen. Das Feld wird nur für die dafür vorgesehenen Herkunftsarten (z. B. Kapazitätsposten) angezeigt. |
| **Eigenschaftswertname** | Wenn die Eigenschaft aus einer Werteliste stammt, dann zeigt dieses Feld die sprechende Bezeichnung des gewählten Werts statt eines reinen Codes. |
| **Wert zulässig von** | Wenn für eine numerische Eigenschaft eine Untergrenze definiert ist, dann steht sie hier; Sie erkennen sofort, ab welchem Wert die Angabe gültig ist. |
| **Wert zulässig bis** | Wenn eine Obergrenze definiert ist, dann steht sie hier; zusammen mit *Wert zulässig von* ergibt sich der erlaubte Wertebereich der Eigenschaft. |
| **Einheit** | Wenn der Eigenschaftswert eine Maßeinheit besitzt, dann wird sie hier angezeigt; dadurch ist der Zahlenwert eindeutig interpretierbar. |
| **Berechnungsformel** | Wenn der Wert der Eigenschaft aus einer Formel abgeleitet wird, dann ist die Formel hier hinterlegt; Sie sehen, dass der Wert nicht manuell, sondern rechnerisch entsteht. |
| **Anzeigereihenfolge** | Bestimmt die Sortierung der Eigenschaften in der Infobox; wenn ein Wert vergeben ist, dann erscheinen die Zeilen in dieser Reihenfolge, sodass wichtige Eigenschaften oben stehen. |
| **Datentyp** | Legt fest, wie der Wert der Eigenschaft zu lesen und zu prüfen ist. Die möglichen Werte sind unten je Ausprägung erläutert. |

**Werte des Feldes „Datentyp" (Optionsfeld):**

- **Text:** Der Wert wird als Freitext geführt; es findet keine Zahlen- oder Datumsprüfung statt.
- **Integer:** Der Wert ist eine Ganzzahl; bei der Erfassung muss eine gültige ganze Zahl eingegeben
  werden, sonst wird die Eingabe abgewiesen.
- **Decimal:** Der Wert ist eine Dezimalzahl; nur gültige Dezimalwerte werden akzeptiert, was
  Bereichsgrenzen (*Wert zulässig von/bis*) auswertbar macht.
- **Date:** Der Wert ist ein Datum; es wird als Datum interpretiert und geprüft.

**Sichtbarkeitslogik (was Sie sehen und warum):** Die Infobox schaltet einzelne Bereiche abhängig von
der Herkunft der markierten Zeile:

- Bei einer Fertigungsauftragszeile werden die Eigenschaften mit ihrer Struktur (z. B. Arbeitsgangbezug)
  angezeigt.
- Bei einer arbeitsgangbezogenen Herkunft werden nur Zeilen mit gefülltem **Eigenschaftscode**
  eingeblendet, damit die Infobox nicht mit leeren Merkmalen überfrachtet wird.
- Für Herkünfte mit Ist-Erfassung (z. B. Kapazitätsposten) wird zusätzlich der **Istwert** sichtbar.

Diese Steuerung erfolgt automatisch; Sie müssen die Sichtbarkeit nicht selbst einstellen.

## Woher die angezeigten Eigenschaften stammen (Voraussetzung)

Damit die Infobox überhaupt Werte anzeigt, müssen die erweiterten Fertigungseigenschaften vorher
gepflegt worden sein. Diese Pflege findet **nicht** in dieser App statt, sondern in den vorgelagerten
Modulen für erweiterte Fertigungsinformationen und Materialeigenschaften. Für den Anwender ist wichtig
zu verstehen, wie die Daten den Weg in die Infobox finden:

1. **Zuerst** hinterlegt ein Administrator die Eigenschaften und ihre Vorgabewerte an den
   Arbeitsplatzgruppen bzw. an den Arbeitsplänen. Wenn dort ein **Standardwert** gesetzt ist, dann wird
   dieser später als Vorgabe in den Fertigungsauftrag übernommen.
2. **Danach** übernimmt Business Central beim Anlegen bzw. Berechnen eines Fertigungsauftrags diese
   Angaben in den Arbeitsplan des Fertigungsauftrags. Wenn der Fertigungsauftrag berechnet wird, dann
   entstehen die zeilen- und arbeitsgangbezogenen Eigenschaften, die die Infobox später filtert.
3. **Schließlich** liest der Anwender die übernommenen Werte in der **FA-Zeilenübersicht** über die
   Infobox **Erw. Fertigungseigenschaften** ab.

Wenn die Infobox für eine Zeile leer bleibt, dann wurden für den zugehörigen Artikel bzw. Arbeitsgang
keine erweiterten Fertigungseigenschaften gepflegt oder sie wurden noch nicht in den Fertigungsauftrag
übernommen. Die Behebung erfolgt in den vorgelagerten Modulen, nicht in dieser App.

## Die Host-Liste „FA-Zeilenübersicht" im Überblick

Die Infobox erscheint auf der Seite **FA-Zeilenübersicht**. Diese Liste ist Bestandteil des
vorgelagerten Moduls für die Fertigungsauftrags-Zeilenübersicht; die vorliegende App verändert ihre
Spalten nicht, sondern ergänzt lediglich die Infobox. Zur Orientierung sind hier die wichtigsten Spalten
beschrieben, die Sie zum Auffinden und Einordnen einer Zeile benötigen.

| Feld | Erläuterung |
|------|-------------|
| **Status** | Zeigt den Bearbeitungsstand des Fertigungsauftrags. Wenn Sie nach offenen Aufträgen suchen, dann filtern Sie über diese Spalte (z. B. auf *Freigegeben*). |
| **FA-Nr.** | Die Nummer des Fertigungsauftrags; sie stellt den Bezug zwischen Zeile und Auftrag her und ist Teil der Verknüpfung zur Infobox. |
| **Artikelnr.** | Der zu fertigende Artikel der Zeile; anhand dieser Spalte erkennen Sie, welches Erzeugnis die angezeigten Eigenschaften betrifft. |
| **Variantencode** | Wenn der Artikel in Varianten geführt wird, dann grenzt dieser Code die konkrete Variante ein. |
| **Beschreibung** | Klartextbezeichnung des Artikels; erleichtert das Auffinden der richtigen Zeile ohne Nummernkenntnis. |
| **Beschreibung 2** | Ergänzende zweite Bezeichnung, sofern gepflegt. |
| **Lagerortcode** | Wenn ein Lagerort zugeordnet ist, dann zeigt die Spalte, wo die Fertigung bzw. Einlagerung erfolgt. |
| **Menge** | Die geplante Fertigungsmenge der Zeile; Bezugsgröße für die Bewertung der Eigenschaften. |
| **Restmenge** | Wenn noch nicht die gesamte Menge fertiggestellt ist, dann sehen Sie hier die verbleibende Menge. |
| **Arbeitsplannr.** | Der Arbeitsplan der Zeile; er ist die Quelle der arbeitsgangbezogenen Eigenschaften, die die Infobox anzeigt. |
| **Fert.-Stücklistennr.** | Die zugeordnete Fertigungsstückliste der Zeile. |
| **Einstandspreis** | Der Einstandspreis der Zeile als betriebswirtschaftliche Bezugsgröße. |

Weitere Standardspalten des Basismoduls (u. a. Kosten in Berichtswährung, Basismengen,
Planungsflexibilität, Gemeinkosten, Dimensionen sowie Start- und Enddaten) sind ebenfalls verfügbar,
werden hier aber nicht einzeln erläutert, da sie zum Standardumfang der Fertigungsauftragszeile gehören
und von dieser App nicht verändert werden.

**Verknüpfte Bereiche derselben Liste:** Unterhalb der Zeilenliste zeigt die Seite die zugeordneten
Bereiche **Zugeordnete FA-Komponente** und **Verkaufszeilen**; rechts stehen neben der neuen Infobox
**Erw. Fertigungseigenschaften** noch die Standard-Infoboxen des Basismoduls für Arbeitsgänge und
Materialkomponenten. Diese Bereiche gehören zum Basismodul und dienen der Anwendung als zusätzlicher
Kontext beim Lesen der Eigenschaften.

## Berechtigungen

Die App liefert einen eigenen Berechtigungssatz **All permissions** aus. Er ist zuweisbar und bestimmt
die Berechtigungen für die von dieser App bereitgestellten Objekte. Da die App außer der Infobox keine
eigenen Datentabellen besitzt, umfasst der Satz im Wesentlichen das Ausführungsrecht auf das interne
App-Objekt.

Zum sichtbaren Anzeigen der Infoboxinhalte benötigen die Anwender darüber hinaus die Leseberechtigungen
der vorgelagerten Module (erweiterte Fertigungsinformationen bzw. Materialeigenschaften), da die
angezeigten Daten aus deren Tabellen stammen. Vergeben Sie den Berechtigungssatz an alle Anwender, die
mit der **FA-Zeilenübersicht** arbeiten und die erweiterten Fertigungseigenschaften einsehen sollen.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die Infobox im Arbeitsalltag genutzt wird. Beide Abläufe sind reine
Lese-/Prüfvorgänge, da die App keine Buchungs- oder Änderungsfunktionen enthält.

### Anwendungsfall 1: Fertigungsauftrag vor der Bearbeitung prüfen

1. **Auslöser:** Ein Mitarbeiter der Fertigungssteuerung erhält einen freigegebenen Fertigungsauftrag
   zur Kontrolle, telefonisch oder per interner Meldung.
2. **Einstieg in BC:** Er öffnet über **Suchen** die **FA-Zeilenübersicht** und markiert die betreffende
   Auftragszeile anhand von **FA-Nr.** und **Artikelnr.**
3. **Kernablauf:** Rechts erscheint automatisch die Infobox **Erw. Fertigungseigenschaften**. Der
   Mitarbeiter prüft je Eigenschaft den **Eigenschaftscode**, den **Standardwert** und den tatsächlich
   gesetzten **Wert** samt **Einheit**. Weicht der **Wert** vom **Standardwert** ab, klärt er die
   Ursache, bevor die Fertigung startet.
4. **Abschluss:** Der Vorgang endet mit der Sichtprüfung; es sind keine weiteren Schritte in dieser App
   erforderlich.

### Anwendungsfall 2: Soll-Ist-Abgleich einer Eigenschaft

1. **Auslöser:** Aus der Fertigung kommt die Rückfrage, ob ein erreichter Messwert innerhalb der Vorgabe
   liegt.
2. **Einstieg in BC:** Der Anwender öffnet die **FA-Zeilenübersicht** und markiert die passende Zeile.
3. **Kernablauf:** In der Infobox **Erw. Fertigungseigenschaften** liest er zur betreffenden Eigenschaft
   den **Standardwert** bzw. **Wert** (Soll) und den **Istwert** ab und vergleicht beide gegen
   **Wert zulässig von** und **Wert zulässig bis**. Anhand von **Datentyp** und **Einheit** ordnet er die
   Zahl korrekt ein.
4. **Abschluss:** Er meldet das Ergebnis des Abgleichs zurück; eine Erfassung des Istwerts erfolgt in dem
   Modul, das die Ist-Werte führt, nicht in dieser App.

## FAQ und Troubleshooting

### 1. Warum sehe ich in der FA-Zeilenübersicht plötzlich eine zusätzliche Infobox?
Weil diese App die Infobox **Erw. Fertigungseigenschaften** an die Liste anfügt. Sie erscheint rechts
neben den Standard-Infoboxen und zeigt die Eigenschaften der jeweils markierten Auftragszeile.

### 2. Wie hängt die Infobox mit der markierten Zeile zusammen?
Die App verknüpft die Infobox fest mit Fertigungsauftragsstatus, **FA-Nr.** und Zeilennummer der
markierten Zeile. Wenn Sie eine andere Zeile markieren, dann aktualisiert sich die Infobox automatisch.

### 3. Warum bleibt die Infobox für eine Zeile leer?
Weil für den zugehörigen Artikel bzw. Arbeitsgang keine erweiterten Fertigungseigenschaften gepflegt
oder noch nicht in den Fertigungsauftrag übernommen wurden. Die Pflege erfolgt in den vorgelagerten
Modulen an Arbeitsplatzgruppen bzw. Arbeitsplänen.

### 4. Kann ich in der Infobox Werte ändern?
In dieser App ist die Infobox als Anzeige ausgelegt. Änderungen an Eigenschaften und Werten nehmen Sie
dort vor, wo die Eigenschaften gepflegt werden (vorgelagerte Module), nicht in der
**FA-Zeilenübersicht**.

### 5. Was bedeutet der Unterschied zwischen Standardwert, Wert und Istwert?
Der **Standardwert** ist die Vorgabe aus den Stammdaten, der **Wert** der für diesen Auftrag ermittelte
Sollwert und der **Istwert** der tatsächlich erreichte Wert. Der Vergleich zeigt, ob ein Auftrag von der
Vorgabe abweicht.

### 6. Warum wird der Istwert nicht bei jeder Zeile angezeigt?
Weil der **Istwert** nur für Herkunftsarten mit Ist-Erfassung (z. B. Kapazitätsposten) sichtbar
geschaltet wird. Bei reinen Planzeilen ist keine Ist-Erfassung vorgesehen, daher bleibt das Feld
ausgeblendet.

### 7. Was sagt mir das Feld Datentyp?
Es legt fest, wie der Wert zu lesen ist: **Text** als Freitext, **Integer** als Ganzzahl, **Decimal** als
Dezimalzahl und **Date** als Datum. Bei numerischen Datentypen sind die Grenzen *Wert zulässig von/bis*
auswertbar.

### 8. Wozu dienen „Wert zulässig von" und „Wert zulässig bis"?
Sie geben den erlaubten Wertebereich einer numerischen Eigenschaft an. Liegt ein **Istwert** außerhalb
dieser Grenzen, dann ist das ein Hinweis auf eine Abweichung, die Sie prüfen sollten.

### 9. Nach welcher Reihenfolge werden die Eigenschaften angezeigt?
Nach der **Anzeigereihenfolge** der Eigenschaft. So stehen fachlich wichtige Merkmale oben und sind ohne
Scrollen sichtbar.

### 10. Welche Berechtigungen benötige ich, um die Infobox zu sehen?
Sie benötigen den Berechtigungssatz dieser App sowie die Leseberechtigungen der vorgelagerten Module, aus
deren Tabellen die angezeigten Eigenschaften stammen. Ohne diese Leserechte bleibt die Infobox leer,
obwohl Daten vorhanden sind.
