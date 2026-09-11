---
title: Anwenderhandbuch m+m Production Order Assistant with Ext. Prod. Information
---

# Anwenderhandbuch m+m Production Order Assistant with Ext. Prod. Information

## Einleitung

Dieses Handbuch beschreibt die Funktionen der App **m+m Production Order Assistant with Ext. Prod. Information** in Microsoft Dynamics 365 Business Central. Die App ist eine schlanke Erweiterung, die die **erweiterten Fertigungseigenschaften** eines Fertigungsauftrags direkt im **Fertigungsassistenten** sichtbar und bearbeitbar macht.

Die App bringt keine eigenen Einrichtungs- oder Stammdatenseiten mit. Sie setzt auf drei m+m-Basismodulen auf und verbindet deren Daten mit dem Fertigungsassistenten:

- **m+m Production Order Assistant** – stellt die Seite **Fertigungsassistent** mit den Unterseiten **Arbeitsplan** und Komponenten bereit.
- **m+m Ext. Production Information** – liefert den **Istwert** und den **Obligatorischen Istwert** je Eigenschaft (Vorgangs- bzw. Kapazitätsbezug).
- **m+m Material Properties** – liefert die eigentliche Datenstruktur der Eigenschaften (Eigenschaftscode, Standardwert, Wert, Berechnungsformel usw.).

**Was die App leistet:** Wählt der Anwender im Fertigungsassistenten im **Arbeitsplan** einen Arbeitsgang aus, zeigt der Faktenkasten **Erw. Fertigungseigenschaften** rechts die zu diesem Arbeitsgang hinterlegten Eigenschaften an. Über die Aktion **Bearbeiten** öffnet der Anwender eine Maske, in der er die Werte des Arbeitsgangs erfassen und ändern kann. Zusätzlich sorgt die App im Hintergrund dafür, dass beim Kopieren von Arbeitsgangzeilen aus einem simulierten Fertigungsauftrag die erweiterten Fertigungseigenschaften mitkopiert werden.

**Zielgruppe:** Primäre Zielgruppe sind **operative Anwender in der Fertigungssteuerung und Arbeitsvorbereitung**, die einen Fertigungsauftrag über den Fertigungsassistenten aufbereiten und je Arbeitsgang die technischen Eigenschaften prüfen oder den **Istwert** erfassen. Planer und Administratoren sind nur mittelbar betroffen: Die zugrunde liegenden Eigenschaften werden in den Basismodulen (Material Properties bzw. Ext. Production Information) gepflegt; diese App fügt dort keine eigene Konfiguration hinzu.

**Kurzer Prozessüberblick:** Fertigungsauftrag im Fertigungsassistenten öffnen → im **Arbeitsplan** den Arbeitsgang markieren → Faktenkasten **Erw. Fertigungseigenschaften** lesen → bei Bedarf über **Bearbeiten** die Werte anpassen → Maske schließen; der Faktenkasten aktualisiert sich.

## Schnellstart für Anwender

Der schnellste Weg zu den erweiterten Fertigungseigenschaften eines Arbeitsgangs:

1. Öffnen Sie den **Fertigungsassistenten** zu dem gewünschten Fertigungsauftrag (der Aufruf erfolgt über das Basismodul m+m Production Order Assistant, üblicherweise aus der Verkaufszeile heraus).
2. Markieren Sie in der Unterseite **Arbeitsplan** die Zeile des Arbeitsgangs, dessen Eigenschaften Sie sehen möchten.
3. Lesen Sie rechts im Faktenkasten **Erw. Fertigungseigenschaften** die Eigenschaften dieses Arbeitsgangs (Eigenschaftscode, Standardwert, **Wert**, ggf. **Istwert**).
4. Möchten Sie einen Wert erfassen oder ändern, wählen Sie im Faktenkasten die Aktion **Bearbeiten**. Es öffnet sich die Maske **Erw. Fertigungseigenschaften**.
5. Erfassen Sie in der Maske den gewünschten **Wert** bzw. **Istwert** und schließen Sie die Maske. Der Faktenkasten zeigt die geänderten Werte anschließend aktualisiert an.

> Hinweis: Diese App enthält keine Einrichtung. Welche Eigenschaften ein Arbeitsgang überhaupt besitzt, ergibt sich aus dem hinterlegten Arbeitsplan und den Eigenschaftsdefinitionen der Basismodule. Sind für einen Arbeitsgang keine Eigenschaften definiert, bleibt der Faktenkasten leer.

## Der Faktenkasten „Erw. Fertigungseigenschaften“ im Fertigungsassistenten

Der Faktenkasten ist der zentrale Anzeigebereich dieser App. Er wird durch die App automatisch als erster Faktenkasten in den Fertigungsassistenten eingefügt und ist an die Unterseite **Arbeitsplan** gekoppelt: Angezeigt werden immer die Eigenschaften des im Arbeitsplan **aktuell markierten Arbeitsgangs**. Wechselt der Anwender im Arbeitsplan die Zeile, wechselt auch der Inhalt des Faktenkastens.

**Einstieg:** Fertigungsassistent öffnen → Unterseite **Arbeitsplan** → Arbeitsgangzeile markieren → Faktenkasten **Erw. Fertigungseigenschaften** rechts. Ein separater Aufruf über **Suchen** existiert nicht; der Faktenkasten erscheint ausschließlich im Fertigungsassistenten.

Der Faktenkasten ist **schreibgeschützt** – er dient dem schnellen Überblick. Zum Ändern von Werten dient die Aktion **Bearbeiten** (siehe nächster Abschnitt).

### Felder des Faktenkastens

Standardmäßig sichtbar sind die Felder, die dem Anwender den Arbeitsgang und dessen Werte auf einen Blick zeigen. Weitere Felder sind vorhanden, aber ausgeblendet und können bei Bedarf über die Spaltenauswahl eingeblendet werden.

| Feld | Erläuterung |
|---|---|
| **Eigenschaftscode** | Technischer Code der Eigenschaft. Wenn ein Code gesetzt ist, kennzeichnet die Zeile eine konkrete Eigenschaft des Arbeitsgangs; im Faktenkasten werden nur Zeilen mit gesetztem Eigenschaftscode angezeigt, damit der Anwender keine Struktur-Leerzeilen sieht. |
| **Beschreibung** | Sprechende Bezeichnung des Arbeitsgangs bzw. der Struktur. Wenn eine Strukturzeile vorliegt, dient dieses Feld dem Anwender zur Orientierung, welchem Arbeitsgang die darunterliegenden Eigenschaften zugeordnet sind. |
| **Standardwert** | Der aus der Eigenschaftsdefinition vorgegebene Standardwert. Wenn kein individueller **Wert** erfasst wurde, arbeitet die Fertigung mit diesem Standardwert weiter; erfasst der Anwender einen abweichenden **Wert**, tritt dieser an die Stelle des Standardwerts. |
| **Wert** | Der für diesen Arbeitsgang gültige Eigenschaftswert. Wenn hier ein Wert steht, ist dies der maßgebliche Sollwert der Eigenschaft für den Arbeitsgang; er wird beim späteren Verbuchen des Fertigungsauftrags durch die Basismodule weiterverarbeitet. |
| **Istwert** | Der tatsächlich erreichte Wert (aus dem Modul m+m Ext. Production Information). Dieses Feld ist nur sichtbar, wenn der Faktenkasten einen Kapazitätsbezug anzeigt; wenn ein Istwert erfasst ist, dokumentiert er das tatsächliche Ergebnis des Arbeitsgangs gegenüber dem geplanten **Wert**. |
| **Eigenschaftswertname** | Ausgeschriebener Name des ausgewählten Eigenschaftswerts (bei Eigenschaften mit hinterlegten Wertelisten). Wenn die Eigenschaft mit Wertelisten arbeitet, sieht der Anwender hier den Klartext statt des internen Werts. Standardmäßig ausgeblendet. |
| **Wert zulässig von** | Untere Grenze des zulässigen Wertebereichs. Wenn eine Untergrenze gesetzt ist, erkennt der Anwender sofort, ab welchem Wert die Eigenschaft gültig ist; die Prüfung dieser Grenze erfolgt bei der Erfassung in der Bearbeiten-Maske. Standardmäßig ausgeblendet. |
| **Wert zulässig bis** | Obere Grenze des zulässigen Wertebereichs. Analog zu „Wert zulässig von“ zeigt dieses Feld an, bis zu welchem Wert die Eigenschaft gültig ist. Standardmäßig ausgeblendet. |
| **Einheit** | Maßeinheit der Eigenschaft. Wenn eine Einheit hinterlegt ist, weiß der Anwender, in welcher Größe der **Wert** bzw. **Istwert** anzugeben ist (z. B. mm, kg). Standardmäßig ausgeblendet. |
| **Berechnungsformel** | Formel, mit der der Wert automatisch berechnet wird. Wenn eine Berechnungsformel hinterlegt ist, wird der **Wert** aus der Formel ermittelt und ist nicht frei eingebbar; ohne Formel gibt der Anwender den Wert manuell ein. Standardmäßig ausgeblendet. |
| **Vorgangsnr.** | Nummer des Arbeitsgangs (Vorgang), zu dem die Eigenschaft gehört. Dieses Feld ist standardmäßig ausgeblendet und wird nur in Strukturzeilen ausgewertet; es stellt die Zuordnung der Eigenschaft zum richtigen Arbeitsgang sicher. |
| **Anzeigereihenfolge** | Steuert die Reihenfolge, in der die Eigenschaften untereinander erscheinen. Wenn die Anzeigereihenfolge gepflegt ist, sieht der Anwender die Eigenschaften in der fachlich gewünschten Sortierung. Standardmäßig ausgeblendet. |
| **Datentyp** | Datenart der Eigenschaft. Der Datentyp bestimmt, wie der **Wert** einzugeben und zu interpretieren ist. Standardmäßig ausgeblendet; die zulässigen Werte sind im Abschnitt **Datentyp** beschrieben. |

> Sichtbarkeitslogik: Die Spalten **Beschreibung**/**Eigenschaftscode** wechseln je nach Kontext (Strukturansicht vs. Arbeitsgangansicht); im Fertigungsassistenten ist die Arbeitsgangansicht aktiv, sodass der **Eigenschaftscode** im Vordergrund steht. Das Feld **Istwert** wird nur bei Kapazitätsbezug eingeblendet.

## Die Bearbeiten-Maske „Erw. Fertigungseigenschaften“

Über die Aktion **Bearbeiten** im Faktenkasten öffnet der Anwender die gleichnamige Maske **Erw. Fertigungseigenschaften** als eigenes Fenster. Hier werden die Eigenschaften desselben Arbeitsgangs angezeigt – im Unterschied zum Faktenkasten jedoch **bearbeitbar**. Nach dem Schließen der Maske werden die zuvor gesetzten Filter des Faktenkastens erneut angewendet, sodass die Anzeige konsistent bleibt.

**Einstieg:** Faktenkasten **Erw. Fertigungseigenschaften** → Aktion **Bearbeiten**.

**Bearbeitbarkeit:** Ob Felder tatsächlich änderbar sind, hängt vom Kontext des Datensatzes ab. Im Arbeitsgangkontext des Fertigungsassistenten sind die Wert- und Definitionsfelder editierbar; reine Anzeigefelder (z. B. **Eigenschaftswertname**, **Einheit**) bleiben schreibgeschützt.

### Felder der Bearbeiten-Maske

| Feld | Erläuterung |
|---|---|
| **Eigenschaftscode** | Auswahl der Eigenschaft. Wenn der Anwender im editierbaren Kontext einen Eigenschaftscode wählt, ordnet er dem Arbeitsgang eine Eigenschaft zu; das Feld ist nur im Stammdatenkontext änderbar, sonst gesperrt. |
| **Standardwert** | Vorgabewert der Eigenschaft. Wenn der Anwender den Standardwert setzt, gilt dieser als Rückfallwert, solange kein individueller **Wert** erfasst ist; das Feld ist nur im Stammdatenkontext und nur ohne **Berechnungsformel** editierbar. |
| **Wert** | Maßgeblicher Eigenschaftswert des Arbeitsgangs. Wenn der Anwender hier einen Wert einträgt, wird dieser als Sollwert übernommen und später von den Basismodulen weiterverarbeitet; das Feld ist gesperrt, sobald eine **Berechnungsformel** hinterlegt ist (dann wird der Wert berechnet). |
| **Istwert** | Tatsächlich erreichter Wert. Wenn der Anwender einen Istwert erfasst, dokumentiert er das reale Ergebnis des Arbeitsgangs; das Feld ist nur sichtbar und nur editierbar, wenn der Kontext einen Istwert zulässt (Kapazitäts-/Rückmeldebezug). |
| **Eigenschaftswertname** | Klartextname des gewählten Eigenschaftswerts. Dieses Feld ist immer schreibgeschützt und dient nur der Kontrolle, welcher Wert ausgewählt wurde. |
| **Obligatorischer Istwert** | Kennzeichen aus dem Modul m+m Ext. Production Information. Wenn dieses Kennzeichen gesetzt ist, muss für die Eigenschaft ein **Istwert** erfasst werden, bevor der Arbeitsgang als vollständig gilt; ist es nicht gesetzt, ist die Istwert-Erfassung optional. Nur im Stammdatenkontext änderbar. |
| **Wert zulässig von** | Untergrenze des zulässigen Wertebereichs. Wenn der Anwender eine Untergrenze setzt, werden spätere Werteingaben gegen diese Grenze geprüft; das Feld ist nur im Stammdatenkontext und nur bei numerischem **Datentyp** (Dezimal/Ganzzahl) editierbar. |
| **Wert zulässig bis** | Obergrenze des zulässigen Wertebereichs. Analog zu „Wert zulässig von“; ebenfalls nur im Stammdatenkontext und nur bei numerischem Datentyp editierbar. |
| **Einheit** | Maßeinheit der Eigenschaft. Dieses Feld ist schreibgeschützt und übernimmt die in der Eigenschaftsdefinition hinterlegte Einheit; es zeigt dem Anwender, in welcher Größe der Wert anzugeben ist. |
| **Berechnungsformel** | Formel zur automatischen Wertermittlung. Wenn eine Berechnungsformel hinterlegt ist, wird der **Wert** aus ihr berechnet und ist nicht mehr manuell eingebbar. Das Feld selbst ist nicht direkt eingebbar; über die Hilfefunktion (AssistEdit) öffnet der Anwender die Maske **Berechnungsformel erstellen**, wählt dort die Formel und übernimmt sie mit **OK**. Verfügbar nur im Stammdatenkontext und nur bei numerischem Datentyp. |
| **Anzeigereihenfolge** | Sortierposition der Eigenschaft. Wenn der Anwender die Anzeigereihenfolge ändert, verschiebt sich die Position der Eigenschaft in Faktenkasten und Maske; nur im Stammdatenkontext editierbar. |
| **Eigenschaftswerte verwenden** | Kennzeichen, ob die Eigenschaft mit einer festen Werteliste arbeitet. Wenn aktiviert, wählt der Anwender den **Wert** aus einer hinterlegten Liste statt ihn frei einzugeben; ohne Kennzeichen ist die freie Eingabe möglich. Standardmäßig ausgeblendet. |
| **Datentyp** | Datenart der Eigenschaft (siehe Abschnitt **Datentyp**). Schreibgeschützt und standardmäßig ausgeblendet; steuert Eingabeprüfung und die Verfügbarkeit numerischer Zusatzfelder. |

### Feld „Datentyp“ – zulässige Werte

Das Feld **Datentyp** legt fest, wie der **Wert** einer Eigenschaft erfasst und geprüft wird. Es ist ein Optionsfeld mit einem festen Wertebereich. Die zulässigen Werte und ihre Wirkung für den Anwender:

- **Text:** Die Eigenschaft nimmt einen freien Text auf; es findet keine numerische Bereichsprüfung statt, und die Felder **Wert zulässig von/bis** sowie **Berechnungsformel** sind nicht anwendbar.
- **Ganzzahl:** Die Eigenschaft nimmt eine ganze Zahl auf; die Bereichsfelder **Wert zulässig von/bis** und die **Berechnungsformel** stehen zur Verfügung, und der Anwender kann nur ganzzahlige Werte erfassen.
- **Dezimal:** Die Eigenschaft nimmt eine Dezimalzahl auf; wie bei Ganzzahl sind Bereichsprüfung und **Berechnungsformel** verfügbar, jedoch mit Nachkommastellen.
- **Datum:** Die Eigenschaft nimmt ein Datum auf; die numerische Bereichsprüfung und die Berechnungsformel entfallen, die Erfassung erfolgt als Datumswert.

> Der Wertebereich dieses Datentyps umfasst genau diese vier Werte. Ein Kennzeichen für Ja/Nein (Boolean) ist in diesem Feld **nicht** enthalten.

### Neuanlage und Löschen in der Maske

Das Anlegen und Löschen von Eigenschaftszeilen ist geschützt und nur im **Stammdatenkontext** erlaubt:

- Versucht der Anwender, eine Zeile anzulegen, obwohl der Kontext dies nicht zulässt, bricht Business Central mit der Meldung **„Einfügen nicht erlaubt!“** ab.
- Versucht der Anwender, eine Zeile zu löschen, obwohl der Kontext dies nicht zulässt, erscheint die Meldung **„Löschen nicht erlaubt!“**.

Dadurch wird verhindert, dass in einem reinen Arbeitsgang-/Rückmeldekontext versehentlich Eigenschaftsdefinitionen entstehen oder entfernt werden, die eigentlich zur Stammdatenpflege gehören.

## Automatische Übernahme der Eigenschaften beim Kopieren von Arbeitsgangzeilen

Neben der Anzeige und Bearbeitung enthält die App eine Hintergrundfunktion, die dem Anwender Nacharbeit erspart: Werden im Basismodul m+m Production Order Assistant Arbeitsgangzeilen **aus einem simulierten Fertigungsauftrag** in einen Ziel-Fertigungsauftrag kopiert, so werden die erweiterten Fertigungseigenschaften der Quell-Arbeitsgangzeile **automatisch mitkopiert**.

Konkret bedeutet das für den Anwender:

- Beim Kopieren einer Arbeitsgangzeile werden zunächst bereits vorhandene erweiterte Fertigungseigenschaften der Zielzeile entfernt, damit keine Dubletten entstehen.
- Anschließend werden alle Eigenschaften mit gesetztem **Eigenschaftscode** aus der Quellzeile in die Zielzeile übertragen (inklusive **Standardwert**, **Wert** und den Definitionsfeldern).
- Der Anwender muss die Eigenschaften des kopierten Arbeitsgangs also nicht erneut manuell pflegen; sie stehen unmittelbar im Faktenkasten des Zielauftrags zur Verfügung.

Diese Funktion läuft ohne eigene Schaltfläche ab; sie wird durch den Kopiervorgang des Basismoduls ausgelöst.

## Zusammenspiel mit den Basismodulen und den Kapazitätsposten

Diese App zeigt und bearbeitet Daten, deren Verarbeitung in den Basismodulen stattfindet. Für das Verständnis des Gesamtprozesses ist folgender Zusammenhang wichtig (die eigentliche Buchung erfolgt in den Basismodulen, nicht in dieser App):

- Die **Definition**, welche Eigenschaften ein Arbeitsgang besitzt, stammt aus dem Arbeitsplan und den Eigenschaftsdefinitionen von m+m Material Properties.
- Der **Istwert** und der **Obligatorische Istwert** stammen aus m+m Ext. Production Information.
- Bei der Verbuchung des Fertigungsauftrags (über das Produktionsbuchblatt der Basismodule) werden die erweiterten Fertigungseigenschaften an die **Kapazitätsposten** weitergegeben, sodass die Werte dort später eingesehen werden können.

Diese App liefert dafür die komfortable Sicht und Erfassung direkt im Fertigungsassistenten; die Weiterverarbeitung in Posten und Buchungen bleibt Aufgabe der Basismodule.

## Typische Anwendungsfälle

### Anwendungsfall 1: Fertigungseigenschaften eines Arbeitsgangs prüfen

1. **Auslöser:** Ein Mitarbeiter der Arbeitsvorbereitung möchte vor Freigabe eines Fertigungsauftrags kontrollieren, welche technischen Eigenschaften der zweite Arbeitsgang mitführt.
2. **Einstieg in BC:** Er öffnet den **Fertigungsassistenten** zum Fertigungsauftrag und markiert in der Unterseite **Arbeitsplan** die Zeile des betreffenden Arbeitsgangs.
3. **Kernablauf:** Rechts im Faktenkasten **Erw. Fertigungseigenschaften** liest er die Eigenschaften des markierten Arbeitsgangs ab: **Eigenschaftscode**, **Standardwert** und den maßgeblichen **Wert**. Bei Bedarf blendet er über die Spaltenauswahl **Einheit** und **Wert zulässig von/bis** ein, um die Vorgaben vollständig zu sehen. Der Faktenkasten ist schreibgeschützt, sodass er beim Prüfen nichts versehentlich ändert.
4. **Abschluss:** Sind alle Werte korrekt, wechselt er zur nächsten Arbeitsgangzeile; der Faktenkasten aktualisiert sich automatisch.

### Anwendungsfall 2: Istwert eines Arbeitsgangs erfassen

1. **Auslöser:** Nach der Bearbeitung eines Arbeitsgangs meldet die Fertigung einen gemessenen Wert zurück, der dokumentiert werden soll.
2. **Einstieg in BC:** Der Anwender öffnet den **Fertigungsassistenten**, markiert im **Arbeitsplan** den Arbeitsgang und wählt im Faktenkasten **Erw. Fertigungseigenschaften** die Aktion **Bearbeiten**.
3. **Kernablauf:** In der geöffneten Maske **Erw. Fertigungseigenschaften** trägt er in der betreffenden Eigenschaftszeile den **Istwert** ein. Ist die Eigenschaft als **Obligatorischer Istwert** gekennzeichnet, ist diese Erfassung erforderlich. Enthält die Eigenschaft eine **Berechnungsformel**, ist der **Wert** gesperrt und ergibt sich automatisch – der Anwender erfasst dann nur den Istwert. Ein Anlegen zusätzlicher Zeilen ist im Arbeitsgangkontext nicht möglich (Meldung **„Einfügen nicht erlaubt!“**).
4. **Abschluss:** Er schließt die Maske. Die erfassten Werte erscheinen aktualisiert im Faktenkasten; die Weiterverarbeitung in die Kapazitätsposten übernimmt bei der Verbuchung das Basismodul.

## FAQ und Troubleshooting

### 1. Warum ist der Faktenkasten „Erw. Fertigungseigenschaften“ leer?
Der Faktenkasten zeigt nur Eigenschaften mit gesetztem **Eigenschaftscode** für den aktuell markierten Arbeitsgang. Sind dem Arbeitsgang keine Eigenschaften zugeordnet, bleibt er leer. Prüfen Sie, ob der Arbeitsplan des Artikels erweiterte Fertigungseigenschaften enthält.

### 2. Warum ändert sich der Inhalt des Faktenkastens, wenn ich im Arbeitsplan eine andere Zeile anklicke?
Der Faktenkasten ist an die Unterseite **Arbeitsplan** gekoppelt und zeigt immer die Eigenschaften des markierten Arbeitsgangs. Der Wechsel der Anzeige ist beabsichtigt.

### 3. Warum kann ich im Faktenkasten keine Werte ändern?
Der Faktenkasten ist bewusst schreibgeschützt und dient nur der Ansicht. Zum Ändern nutzen Sie im Faktenkasten die Aktion **Bearbeiten** und arbeiten in der geöffneten Maske.

### 4. Warum ist das Feld „Wert“ in der Bearbeiten-Maske gesperrt?
Das Feld **Wert** ist gesperrt, sobald für die Eigenschaft eine **Berechnungsformel** hinterlegt ist. Der Wert wird dann automatisch aus der Formel berechnet und darf nicht manuell überschrieben werden.

### 5. Wie hinterlege ich eine Berechnungsformel?
Wählen Sie in der Zeile das Feld **Berechnungsformel** und öffnen Sie über die Hilfefunktion (AssistEdit) die Maske **Berechnungsformel erstellen**. Wählen Sie dort die Formel und bestätigen Sie mit **OK**. Dies ist nur im Stammdatenkontext und nur bei numerischem **Datentyp** (Ganzzahl/Dezimal) möglich.

### 6. Warum sehe ich das Feld „Istwert“ nicht?
Der **Istwert** wird nur eingeblendet, wenn der Kontext einen Kapazitäts- bzw. Rückmeldebezug hat. In der reinen Struktur- oder Sollwertansicht ist das Feld ausgeblendet.

### 7. Warum erhalte ich die Meldung „Einfügen nicht erlaubt!“?
Das Anlegen neuer Eigenschaftszeilen ist nur im **Stammdatenkontext** erlaubt. Im Arbeitsgang-/Rückmeldekontext des Fertigungsassistenten ist das Einfügen gesperrt, um versehentliche Definitionen zu verhindern.

### 8. Warum erhalte ich die Meldung „Löschen nicht erlaubt!“?
Analog zum Einfügen ist das Löschen von Eigenschaftszeilen nur im Stammdatenkontext möglich. Im Arbeitsgangkontext ist es gesperrt.

### 9. Muss ich zu jeder Eigenschaft einen Istwert erfassen?
Nur wenn die Eigenschaft als **Obligatorischer Istwert** gekennzeichnet ist. Ist das Kennzeichen nicht gesetzt, ist die Istwert-Erfassung optional.

### 10. Warum stehen beim kopierten Fertigungsauftrag die Eigenschaften schon fertig da?
Beim Kopieren von Arbeitsgangzeilen aus einem simulierten Fertigungsauftrag überträgt die App die erweiterten Fertigungseigenschaften automatisch in den Zielauftrag. Sie müssen sie daher nicht erneut manuell erfassen; vorhandene Zieldaten werden zuvor bereinigt, damit keine Dubletten entstehen.
