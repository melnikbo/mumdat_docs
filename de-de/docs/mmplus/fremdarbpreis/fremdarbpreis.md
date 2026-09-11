---
title: Anwenderhandbuch m+m Subcontracting Prices
---

# Anwenderhandbuch m+m Subcontracting Prices

## Einleitung

Die App **m+m Subcontracting Prices** erweitert die Fertigung in Microsoft Dynamics 365 Business Central um eine eigene Preisliste für Fremdarbeiten. In dieser Liste hinterlegen Sie **Fremdarbeitspreise** je Kombination aus **Arbeitsplatzgruppe**, **Kreditor**, **Standardkatalogcode** und **Artikel**. Sobald ein Fertigungsauftrag mit einem fremdvergebenen Arbeitsgang berechnet wird, ermittelt das Modul aus dieser Liste den passenden Preis und schreibt ihn automatisch als **EK-Preis (direkt)** in die betroffene Arbeitsgangzeile, die Bestellzeile oder die Planungszeile.

**Zielgruppe.** Primäre Anwender sind **operative Rollen in Fertigung und Einkauf**, die täglich mit Fertigungsaufträgen, dem **Fremdarbeitsarbeitsblatt** und **Einkaufsbestellungen** arbeiten und dort die Preise für vergebene Lohnarbeit benötigen. **Sekundär** richtet sich das Handbuch an **Administratoren und Stammdatenverantwortliche**, die die Arbeitsplatzgruppen vorbereiten und die Fremdarbeitspreise pflegen.

**Kurzer Prozessüberblick.** Der Ablauf folgt einer festen Kette:

1. Ein Administrator hinterlegt auf der **Arbeitsplatzgruppenkarte** einen Kreditor als Unterlieferant und aktiviert damit die Verwendung spezifischer Fremdarbeitspreise.
2. Ein Stammdatenverantwortlicher pflegt in der Liste **Fremdarbeitspreise** die gültigen Preise, Mindestpreise, Mindestmengen und Gültigkeitszeiträume.
3. Im Tagesgeschäft berechnet das System beim Aufbau bzw. Aktualisieren eines Fertigungsauftrags den Arbeitsgangpreis und überträgt ihn in den Arbeitsgang, das Fremdarbeitsarbeitsblatt und die daraus erzeugte Einkaufsbestellung.

Alle drei Schritte werden in diesem Handbuch in dieser Reihenfolge beschrieben: zuerst der **Schnellstart**, dann die **Einrichtung** der Arbeitsplatzgruppe, danach die **Stammdatenpflege** der Preise und schließlich die **tägliche Arbeit** im Fertigungsauftrag und Einkauf.

---

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg von der Einrichtung bis zum automatisch gesetzten Preis. Führen Sie die Schritte in dieser Reihenfolge aus; jeder Schritt setzt den vorherigen voraus.

**A. Einrichtung (einmalig, durch den Administrator)**

1. Öffnen Sie die betreffende **Arbeitsplatzgruppe** über die Suchfunktion (**Suchen**) und wählen Sie die **Arbeitsplatzgruppenkarte**.
2. Tragen Sie im Feld **Unterlieferantennr.** den Kreditor ein, der die Fremdarbeit ausführt. Mit dem Eintrag setzt das System den Schalter **Spez. EK-Preis** automatisch auf aktiv.
3. Prüfen Sie, dass **Spez. EK-Preis** aktiviert ist. Nur dann greift die Preisermittlung dieses Moduls.

**B. Stammdaten (Preise hinterlegen)**

4. Öffnen Sie die Liste **Fremdarbeitspreise**. Sie erreichen die Liste über die Suche (**Suchen**) oder komfortabler über die **Kreditorkarte** bzw. **Artikelkarte** im Menü **Zugehörig** über die Aktion **Fremdarbeitspreise**.
5. Erfassen Sie je Zeile die **Einkaufsart**, die **Arbeitsplatzgruppennr.**, die **Referenz-Art**, ggf. den **Standardkatalogcode**, die **Definitionsart**, ggf. den **Artikel**, den **Preis**, die **Mindestmenge**, den **Mindestpreis** sowie **Gültig ab** und **Gültig bis**.

**C. Tägliche Arbeit (Preis wird automatisch gesetzt)**

6. Legen Sie einen **freigegebenen Fertigungsauftrag** für den Artikel mit fremdvergebenem Arbeitsgang an.
7. Aktualisieren Sie den Auftrag über **Prozess** > **Fertigungsauftrag aktualisieren**. Beim Aufbau der Arbeitsgänge ermittelt das System den Fremdarbeitspreis und schreibt ihn als **EK-Preis (direkt)** in die Arbeitsgangzeile.
8. Öffnen Sie den **Arbeitsplan** des Auftrags (Register **Zeilen** > **Arbeitsplan**). Der ermittelte Preis steht in der Arbeitsgangzeile; im Infobereich **Fremdarbeitspreise** sehen Sie die zugrunde liegenden gültigen Preiszeilen.
9. Erzeugen Sie aus dem **Fremdarbeitsarbeitsblatt** über **Prozess** > **Fremdarbeit berechnen** und anschließend über **Prozess** > **Ereignismeldung durchführen** die **Einkaufsbestellung**. Der Fremdarbeitspreis wird dabei in die Bestellzeile übernommen.

> Die vollständige Feldbeschreibung der Einrichtung finden Sie unter [Einrichtung](#einrichtung), die Preispflege unter [Stammdaten: Fremdarbeitspreise pflegen](#stammdaten-fremdarbeitspreise-pflegen).

---

## Einrichtung

Die Einrichtung dieses Moduls besteht aus **einer** zwingenden Konfiguration: der Verknüpfung einer **Arbeitsplatzgruppe** mit einem Unterlieferanten und der Aktivierung des spezifischen Einstandspreises. Erst diese Einstellung schaltet die gesamte Preisermittlung des Moduls frei. Die Preiszeilen selbst sind Stammdaten und werden im Kapitel [Stammdaten](#stammdaten-fremdarbeitspreise-pflegen) beschrieben.

### Fremdarbeitspreise je Arbeitsplatzgruppe einrichten

**Prozesseinführung.** Diese Einrichtung nimmt der **Administrator** bzw. der Fertigungsverantwortliche **vor der ersten Nutzung** je fremdvergebener Arbeitsplatzgruppe vor. Sie legt fest, für welche Arbeitsplatzgruppen überhaupt Fremdarbeitspreise gezogen werden. Die Einstellung wird später in der [täglichen Arbeit am Fertigungsauftrag](#tägliche-arbeit-am-fertigungsauftrag) ausgewertet: Nur für Arbeitsplatzgruppen mit aktiviertem **Spez. EK-Preis** ersetzt das Modul den regulären Einkaufspreis durch den hinterlegten Fremdarbeitspreis.

**Einstieg:** Öffnen Sie über die Suche (**Suchen**) die **Arbeitsplatzgruppen**, wählen Sie die betreffende Zeile und öffnen Sie die **Arbeitsplatzgruppenkarte**. Die relevanten Felder liegen im Bereich der Buchungs- bzw. Kostendaten der Karte.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Unterlieferantennr.** | Wenn Sie hier einen Kreditor eintragen, kennzeichnen Sie die Arbeitsplatzgruppe als fremdvergeben und setzen zugleich automatisch den Schalter **Spez. EK-Preis** auf aktiv. Dadurch werden Arbeitsgänge dieser Arbeitsplatzgruppe über eine Einkaufsbestellung an diesen Kreditor beschafft, und die Preisermittlung dieses Moduls wird für diese Arbeitsplatzgruppe eingeschaltet. |
| **Spez. EK-Preis** | Wenn aktiviert, verwendet das System bei der Auftragsberechnung **nicht** den regulären Einkaufs- bzw. Einstandspreis, sondern den in den **Fremdarbeitspreisen** hinterlegten Preis für diese Arbeitsplatzgruppe. Ist der Schalter nicht gesetzt, bleibt der Standard-Einstandspreis wirksam und das Modul greift nicht ein. Der Schalter wird beim Eintragen einer **Unterlieferantennr.** automatisch aktiviert, kann jedoch durch den Administrator geprüft und angepasst werden. |

**Prozessschritte (Abhängigkeitsreihenfolge):**

1. **Zuerst** tragen Sie die **Unterlieferantennr.** ein. Dadurch wird der Schalter **Spez. EK-Preis** automatisch gesetzt.
2. **Danach** prüfen Sie, dass **Spez. EK-Preis** aktiviert ist. Ohne diesen Schalter zieht das Modul in der täglichen Arbeit keinen Fremdarbeitspreis.
3. **Schließlich** pflegen Sie für diese Arbeitsplatzgruppe die Preiszeilen in der Liste **Fremdarbeitspreise** (siehe [Stammdaten](#stammdaten-fremdarbeitspreise-pflegen)).

**Abhängigkeit / Validierung.** Die Preisermittlung greift ausschließlich für Arbeitsgänge vom Typ **Arbeitsplatzgruppe** und nur, wenn die Arbeitsplatzgruppe **Spez. EK-Preis** = aktiv trägt. Der auf der Arbeitsplatzgruppe hinterlegte Unterlieferant wird bei der Preisermittlung als Kreditor herangezogen; fehlt der Kreditor oder der Schalter, bleibt der reguläre Preis stehen.

---

## Stammdaten: Fremdarbeitspreise pflegen

Die Liste **Fremdarbeitspreise** ist das zentrale Stammdatenobjekt dieses Moduls. Hier definieren Stammdatenverantwortliche, welcher Preis für welche Kombination aus Arbeitsplatzgruppe, Kreditor, Standardkatalogcode und Artikel gilt, in welcher Menge und in welchem Zeitraum.

**Prozesseinführung.** Die Preise pflegt der **Stammdatenverantwortliche** oder Einkäufer **nach** der Einrichtung der Arbeitsplatzgruppe und **vor** dem ersten Fertigungsauftrag mit Fremdarbeit. Die gepflegten Zeilen werden in der täglichen Arbeit ausgewertet, sobald ein Fertigungsauftrag berechnet oder ein Fremdarbeitsarbeitsblatt bzw. eine Einkaufsbestellung erzeugt wird.

### Navigation zur Liste Fremdarbeitspreise

Sie erreichen die Liste **Fremdarbeitspreise** auf drei Wegen:

- Über die Suche (**Suchen**) direkt als Listenseite **Fremdarbeitspreise**.
- Über die **Kreditorkarte**: Menü **Zugehörig** > **Fremdarbeitspreise**. Die Liste ist dann auf den geöffneten Kreditor vorgefiltert.
- Über die **Artikelkarte**: Menü **Zugehörig** > **Fremdarbeitspreise**. Die Liste ist dann auf den geöffneten Artikel vorgefiltert.

Die Navigation über **Kreditorkarte** oder **Artikelkarte** wird für die tägliche Pflege empfohlen, weil die Liste bereits auf den relevanten Datensatz eingegrenzt ist.

### Felder der Liste Fremdarbeitspreise

Erfassen Sie je Preiszeile die folgenden Felder. Die Editierbarkeit einzelner Felder steuert das System über die jeweilige Art (siehe Optionswerte unten): Setzen Sie eine Art auf „Alle …“, wird das zugehörige Detailfeld gesperrt und geleert.

| Feld | Erläuterung |
|------|-------------|
| **Einkaufsart** | Legt fest, für welchen Beschaffungsbezug die Zeile gilt. Bei **Kreditoren** gilt der Preis nur für den in **Kreditornr.** genannten Kreditor; bei **Alle Kreditoren** gilt er kreditorübergreifend. Wenn Sie **Alle Kreditoren** wählen, wird **Kreditornr.** gesperrt und geleert. |
| **Kreditornr.** | Der Kreditor, für den der Preis gilt. Nur bei **Einkaufsart** = **Kreditoren** editierbar und dann gegen die Kreditorenstammdaten geprüft. Wenn Sie hier trotz **Alle Kreditoren** einen Wert eintragen, bricht das System mit der Meldung „%1 muss leer sein.“ ab. |
| **Kreditorname** | Zeigt den Namen des in **Kreditornr.** hinterlegten Kreditors an (nur Anzeige, wird aus den Kreditorenstammdaten gelesen). |
| **Arbeitsplatzgruppennr.** | Die Arbeitsplatzgruppe, für die der Preis gilt. Wenn **Einkaufsart** = **Kreditoren** gesetzt ist, sind nur Arbeitsplatzgruppen wählbar, deren Unterlieferant dem gewählten Kreditor entspricht; andernfalls sind alle Arbeitsplatzgruppen wählbar. Dieses Feld verknüpft die Preiszeile mit dem Arbeitsgang im Fertigungsauftrag. |
| **Arbeitsplatzgruppenname** | Zeigt den Namen der in **Arbeitsplatzgruppennr.** hinterlegten Arbeitsplatzgruppe an (nur Anzeige). |
| **Referenz-Art** | Legt fest, ob der Preis für einen bestimmten oder für jeden Standardkatalogcode gilt. Bei **Standardkatalogcode** gilt der Preis nur für den genannten Code; bei **Alle Standardkatalogcodes** kreditor- und arbeitsplatzgruppenweit unabhängig vom Code. Wenn Sie **Alle Standardkatalogcodes** wählen, wird **Standardkatalogcode** gesperrt und geleert. |
| **Standardkatalogcode** | Der Standardkatalogcode (die Tätigkeit/der Arbeitsgangtyp), für den der Preis gilt. Nur bei **Referenz-Art** = **Standardkatalogcode** editierbar und gegen die Standardkatalogcodes geprüft. Ein Eintrag bei **Alle Standardkatalogcodes** führt zur Fehlermeldung „%1 muss leer sein.“ |
| **Definitionsart** | Legt fest, ob der Preis für einen bestimmten oder für jeden Artikel gilt. Bei **Artikel** gilt der Preis nur für den genannten Artikel; bei **Alle Artikel** artikelübergreifend. Wenn Sie **Alle Artikel** wählen, wird **Artikel** gesperrt und geleert. |
| **Artikel** | Der Artikel, für den der Preis gilt. Nur bei **Definitionsart** = **Artikel** editierbar und gegen die Artikelstammdaten geprüft. Ein Eintrag bei **Alle Artikel** führt zur Fehlermeldung „%1 muss leer sein.“ |
| **Einheit** | Die Maßeinheit, auf die sich der Preis bezieht. Wird gegen die Einheiten geprüft und dient als Bezugsgröße der Preisangabe. |
| **Mindestpreis** | Wenn gesetzt, greift dieser Betrag als Untergrenze: Liegt der aus **Preis** × Menge errechnete Zeilenbetrag unter dem Mindestpreis, verwendet das System pauschal den Mindestpreis. So stellen Sie sicher, dass eine Fremdarbeit einen Sockelbetrag nicht unterschreitet. Der Mindestpreis darf pro Arbeitsplatzgruppe und Standardkatalogcode **nur einmal** vergeben werden; ein zweiter Mindestpreis für dieselbe Kombination wird mit der Meldung „Für diese Kombination aus Arbeitsplatzgruppe und Standardkatalogcode ist bereits ein Mindestpreis gepflegt.“ abgewiesen. |
| **Mindestmenge** | Wenn gesetzt, gilt der Preis dieser Zeile erst ab der angegebenen Menge. Über mehrere Zeilen mit unterschiedlicher Mindestmenge bilden Sie **Preisstaffeln** ab: Bei der Berechnung werden nur Zeilen berücksichtigt, deren Mindestmenge kleiner oder gleich der Auftragsmenge ist. Die Mindestmenge darf pro Kombination mehrfach vergeben werden. |
| **Preis** | Der Preis je **Einheit** für die Kombination aus Arbeitsplatzgruppe, Standardkatalogcode und Menge. Aus diesem Preis errechnet das System den Zeilenbetrag und daraus den **EK-Preis (direkt)** der Arbeitsgang- bzw. Bestellzeile. |
| **Gültig ab** | Wenn gesetzt, gilt der Preis erst ab diesem Datum. Bei der Berechnung werden nur Zeilen berücksichtigt, deren **Gültig ab** leer oder kleiner/gleich dem Arbeitsdatum ist. |
| **Gültig bis** | Wenn gesetzt, gilt der Preis nur bis zu diesem Datum. Bei der Berechnung werden nur Zeilen berücksichtigt, deren **Gültig bis** leer oder größer/gleich dem Arbeitsdatum ist. So planen Sie Preiswechsel vor. |

#### Optionswerte im Detail

**Einkaufsart**

- **Kreditoren:** Die Zeile gilt ausschließlich für den in **Kreditornr.** genannten Kreditor. Das Feld **Kreditornr.** ist editierbar und muss gefüllt werden.
- **Alle Kreditoren:** Die Zeile gilt für jeden Kreditor. **Kreditornr.** wird gesperrt und geleert; ein manuell eingetragener Kreditor wird abgewiesen.
- **Kreditorengruppe:** Vorgesehener Wert für eine Bündelung mehrerer Kreditoren zu einer Gruppe. In der aktuellen Preisermittlung werden bei der Auswahl der gültigen Zeilen die Ausprägungen **Kreditoren** und **Alle Kreditoren** ausgewertet; dokumentieren Sie den geplanten Einsatz von **Kreditorengruppe** mit Ihrem Betreuer.

**Referenz-Art**

- **Standardkatalogcode:** Die Zeile gilt nur für den genannten Standardkatalogcode. **Standardkatalogcode** ist editierbar und muss gefüllt werden.
- **Alle Standardkatalogcodes:** Die Zeile gilt für jeden Standardkatalogcode. **Standardkatalogcode** wird gesperrt und geleert.

**Definitionsart**

- **Artikel:** Die Zeile gilt nur für den genannten Artikel. **Artikel** ist editierbar und muss gefüllt werden.
- **Alle Artikel:** Die Zeile gilt für jeden Artikel. **Artikel** wird gesperrt und geleert.

**Prozessschritte für eine Preisstaffel (Beispiel):**

1. **Zuerst** legen Sie eine Zeile mit **Mindestmenge** 0 (oder leer) und dem Grundpreis an.
2. **Danach** legen Sie weitere Zeilen mit steigender **Mindestmenge** und dem jeweils gestaffelten **Preis** an.
3. **Optional** hinterlegen Sie in **einer** Zeile je Kombination aus Arbeitsplatzgruppe und Standardkatalogcode einen **Mindestpreis** als Sockelbetrag.
4. **Schließlich** grenzen Sie über **Gültig ab** / **Gültig bis** den Zeitraum ein, wenn Preise befristet gelten sollen.

**Abhängigkeit / Validierung.** Der **Mindestpreis** ist pro Arbeitsplatzgruppe und Standardkatalogcode eindeutig. Bei einem zweiten Mindestpreis für dieselbe Kombination bricht das System ab. Die Ermittlung des maßgeblichen Preises in der täglichen Arbeit ist unter [Preisermittlung](#preisermittlung-logik) beschrieben.

---

## Tägliche Arbeit am Fertigungsauftrag

Dieses Kapitel beschreibt, wie und wann der Fremdarbeitspreis im laufenden Betrieb gezogen wird. Alle beschriebenen Automatismen setzen voraus, dass die Arbeitsplatzgruppe gemäß [Einrichtung](#einrichtung) den Schalter **Spez. EK-Preis** trägt und dass für die Kombination gültige [Fremdarbeitspreise](#stammdaten-fremdarbeitspreise-pflegen) gepflegt sind.

**Bezug zur Einrichtung.** Die tägliche Preisermittlung wird durch zwei vorgelagerte Konfigurationen gesteuert: durch den Schalter **Spez. EK-Preis** und den Unterlieferanten auf der **Arbeitsplatzgruppenkarte** (Einrichtung) sowie durch die Zeilen in der Liste **Fremdarbeitspreise** (Stammdaten). Fehlt eine dieser Voraussetzungen, bleibt der reguläre Preis stehen.

### Preis im Arbeitsgang des Fertigungsauftrags

Das Modul setzt den **EK-Preis (direkt)** des fremdvergebenen Arbeitsgangs an mehreren Stellen automatisch:

1. **Beim Aufbau der Arbeitsgänge** (Aktion **Prozess** > **Fertigungsauftrag aktualisieren**): Sobald ein Arbeitsgang zum Fertigungsauftrag hinzugefügt wird, ermittelt das System den Fremdarbeitspreis und trägt den **EK-Preis (direkt)** ein.
2. **Beim Ändern der Arbeitsgangzeile:** Wenn Sie im **Arbeitsplan** die **Arbeitsplatzgruppennr.** oder den **Standardkatalogcode** einer Arbeitsgangzeile ändern, berechnet das System den Preis unmittelbar neu.
3. **Beim Umsetzen von Planungsvorschlägen** in einen Fertigungsauftrag wird der Preis ebenfalls beim Anlegen der Arbeitsgangzeile gesetzt.

**Einstieg:** Öffnen Sie den **freigegebenen Fertigungsauftrag** und darin das Register **Zeilen** > **Arbeitsplan**. Die betroffene Arbeitsgangzeile zeigt den ermittelten Preis im Feld **EK-Preis (direkt)**.

### Infobereich Fremdarbeitspreise

Auf den Seiten **Arbeitsplan** (Prod.-Auftrags-Arbeitsplan), **Fremdarbeitsarbeitsblatt** und **Einkaufsbestellung** blendet das Modul den Infobereich **Fremdarbeitspreise** ein. Er zeigt für die aktuell markierte Zeile die zutreffenden, **aktuell gültigen** Preiszeilen (gefiltert auf **Gültig ab** ≤ Arbeitsdatum und **Gültig bis** ≥ Arbeitsdatum). So prüfen Anwender direkt am Beleg, welche hinterlegten Preise die Berechnung speisen.

| Feld (Infobereich) | Erläuterung |
|--------------------|-------------|
| **Arbeitsplatzgruppenname** | Zeigt die Arbeitsplatzgruppe der jeweils gültigen Preiszeile an. |
| **Standardkatalogcode** | Zeigt den Standardkatalogcode der gültigen Preiszeile an. |
| **Mindestpreis** | Zeigt den hinterlegten Sockelbetrag der Zeile an. |
| **Mindestmenge** | Zeigt die Mengenschwelle der Preisstaffel an. |
| **Preis** | Zeigt den je Einheit hinterlegten Preis an. |
| **Gültig ab** / **Gültig bis** | Zeigt den Gültigkeitszeitraum der angezeigten Preiszeile an. |

Der Infobereich ist nicht editierbar; er dient ausschließlich der Kontrolle. Die **Kreditornr.** wird im Infobereich nicht als Spalte geführt, weil der Bezug bereits über Arbeitsplatzgruppe und Beleg gegeben ist.

### Einkaufsbestellung aus dem Fremdarbeitsarbeitsblatt

Der reguläre Weg zur Beschaffung der Fremdarbeit führt über das **Fremdarbeitsarbeitsblatt**:

1. Öffnen Sie über die Suche (**Suchen**) das **Fremdarbeitsarbeitsblatt**.
2. Wählen Sie **Prozess** > **Fremdarbeit berechnen**, um die offenen Fremdarbeiten anzuzeigen. Dabei wird der Fremdarbeitspreis in die Planungszeile übernommen.
3. Setzen Sie ggf. einen Filter auf die zu bearbeitenden Zeilen und wählen Sie **Prozess** > **Ereignismeldung durchführen**. Das System erzeugt daraus die **Einkaufsbestellung**; die verarbeitete Zeile verschwindet aus dem Arbeitsblatt.
4. Öffnen Sie die erzeugte **Einkaufsbestellung**. In der Bestellzeile steht der aus den Fremdarbeitspreisen übernommene **EK-Preis (direkt)**.

### Preis in der Einkaufsbestellung neu berechnen

Auf den **Zeilen der Einkaufsbestellung** steht zusätzlich die Aktion **Fremdarbeitspreise berechnen** zur Verfügung. Sie berechnet den Preis der markierten Bestellzeile erneut auf Basis der aktuell gültigen Fremdarbeitspreise und des zugehörigen Fertigungsauftrags-Arbeitsgangs.

**Einstieg:** Öffnen Sie die **Einkaufsbestellung**, markieren Sie in den Zeilen die betreffende Bestellzeile und wählen Sie über **Funktionen** die Aktion **Fremdarbeitspreise berechnen**.

Verwenden Sie diese Aktion, wenn sich nach dem Erzeugen der Bestellung Menge, Arbeitsgang oder Preisstaffel geändert haben und Sie den **EK-Preis (direkt)** an den aktuellen Fremdarbeitspreis angleichen möchten. Voraussetzung ist, dass die Bestellzeile über Fertigungsauftrag, Arbeitsplan und Arbeitsgang einem berechenbaren Arbeitsgang zugeordnet ist und die Menge größer als null ist.

<a id="preisermittlung-logik"></a>
### Preisermittlung – so bestimmt das System den Preis

Bei jeder Berechnung wählt das Modul aus den gepflegten Zeilen die zutreffenden Preise aus und ermittelt daraus den maßgeblichen Preis:

1. **Vorbedingung:** Der Arbeitsgang ist vom Typ **Arbeitsplatzgruppe** und die Arbeitsplatzgruppe trägt **Spez. EK-Preis** = aktiv. Andernfalls greift das Modul nicht ein.
2. **Grundfilter:** Es werden nur Preiszeilen betrachtet, deren **Arbeitsplatzgruppennr.** passt, deren **Artikel** leer ist oder dem Auftragsartikel entspricht, deren Gültigkeitszeitraum das Arbeitsdatum einschließt und deren **Mindestmenge** kleiner oder gleich der Auftragsmenge ist.
3. **Kombinationen:** Aus diesen Zeilen berücksichtigt das System vier Ausprägungen — **Alle Kreditoren + Alle Standardkatalogcodes**, **Kreditoren (Unterlieferant) + Alle Standardkatalogcodes**, **Kreditoren (Unterlieferant) + Standardkatalogcode** und **Alle Kreditoren + Standardkatalogcode**.
4. **Betragsermittlung je Zeile:** Für jede berücksichtigte Zeile gilt: Zeilenbetrag = **Preis** × Auftragsmenge. Liegt der Zeilenbetrag über dem **Mindestpreis**, wird der Zeilenbetrag verwendet, sonst der **Mindestpreis**.
5. **Bestwert:** Aus allen so ermittelten Beträgen wählt das System den **niedrigsten** Betrag. Dieser Betrag geteilt durch die Menge ergibt den **EK-Preis (direkt)** der Zeile.

Der ermittelte Preis wird je nach Auslöser in die **Arbeitsgangzeile**, die **Bestellzeile** oder die **Planungszeile** geschrieben; bei der Umsetzung aus dem Arbeitsblatt in die Bestellung wird der berechnete Preis zusätzlich in den Arbeitsgang des Fertigungsauftrags zurückgeschrieben.

---

## FAQ und Troubleshooting

### 1. Warum wird kein Fremdarbeitspreis in den Arbeitsgang übernommen?

Prüfen Sie zuerst die **Arbeitsplatzgruppenkarte**: Ohne aktivierten Schalter **Spez. EK-Preis** greift die Preisermittlung nicht. Der Schalter wird automatisch gesetzt, sobald eine **Unterlieferantennr.** eingetragen ist. Zusätzlich muss der Arbeitsgang vom Typ **Arbeitsplatzgruppe** sein.

### 2. Warum bleibt der Preis null, obwohl eine passende Preiszeile existiert?

Die Preisermittlung berücksichtigt nur Zeilen, deren **Mindestmenge** kleiner oder gleich der Auftragsmenge ist und deren Gültigkeitszeitraum (**Gültig ab** / **Gültig bis**) das Arbeitsdatum einschließt. Ist die Auftragsmenge kleiner als jede hinterlegte **Mindestmenge** oder liegt das Arbeitsdatum außerhalb der Gültigkeit, wird die Zeile ignoriert. Auch bei Auftragsmenge null erfolgt keine Berechnung.

### 3. Warum meldet das System „Für diese Kombination aus Arbeitsplatzgruppe und Standardkatalogcode ist bereits ein Mindestpreis gepflegt.“?

Der **Mindestpreis** darf je Kombination aus **Arbeitsplatzgruppennr.** und **Standardkatalogcode** nur **einmal** vergeben werden. Für dieselbe Kombination existiert bereits eine Zeile mit einem Mindestpreis größer null. Verwenden Sie die bestehende Zeile oder setzen Sie den doppelten Mindestpreis auf null.

### 4. Warum kann ich die Kreditornr. nicht ausfüllen?

Die **Kreditornr.** ist nur bei **Einkaufsart** = **Kreditoren** editierbar. Bei **Alle Kreditoren** sperrt und leert das System das Feld. Ein trotzdem eingetragener Kreditor wird mit „%1 muss leer sein.“ abgewiesen. Dasselbe Prinzip gilt für **Standardkatalogcode** bei **Referenz-Art** und **Artikel** bei **Definitionsart**.

### 5. Wie bilde ich Mengenrabatte für Fremdarbeiten ab?

Legen Sie mehrere Preiszeilen mit gleicher Arbeitsplatzgruppe und steigender **Mindestmenge** an und hinterlegen Sie je Zeile den gestaffelten **Preis**. Bei der Berechnung werden alle Zeilen bis zur Auftragsmenge berücksichtigt; das System wählt daraus den günstigsten maßgeblichen Betrag.

### 6. Wie wirkt sich der Mindestpreis auf kleine Mengen aus?

Liegt der aus **Preis** × Auftragsmenge errechnete Zeilenbetrag unter dem **Mindestpreis**, verrechnet das System pauschal den Mindestpreis. Bei sehr kleinen Mengen wird also nicht der proportionale Betrag, sondern der Sockelbetrag angesetzt.

### 7. Wo sehe ich, welche Preise gerade herangezogen werden?

Im Infobereich **Fremdarbeitspreise** auf dem **Arbeitsplan**, im **Fremdarbeitsarbeitsblatt** und in der **Einkaufsbestellung**. Er zeigt die aktuell gültigen Preiszeilen zur markierten Zeile, gefiltert auf das Arbeitsdatum.

### 8. Warum unterscheidet sich der Preis in der Einkaufsbestellung vom Arbeitsgang?

Nach dem Erzeugen der Bestellung können sich Menge oder Arbeitsgang geändert haben. Verwenden Sie in den Bestellzeilen über **Funktionen** die Aktion **Fremdarbeitspreise berechnen**, um den **EK-Preis (direkt)** neu auf Basis der aktuell gültigen Fremdarbeitspreise zu ermitteln.

### 9. Gilt eine Preiszeile ohne Kreditor für jeden Lieferanten?

Ja. Bei **Einkaufsart** = **Alle Kreditoren** und **Referenz-Art** = **Alle Standardkatalogcodes** wirkt die Zeile als allgemeine Grundlage. Spezifischere Zeilen (mit Kreditor bzw. Standardkatalogcode) werden zusätzlich berücksichtigt; maßgeblich ist am Ende der günstigste ermittelte Betrag.

### 10. Muss ich den Preis manuell in die Bestellung eintragen?

Nein. Der reguläre Weg erzeugt die **Einkaufsbestellung** über das **Fremdarbeitsarbeitsblatt** (**Prozess** > **Fremdarbeit berechnen**, dann **Prozess** > **Ereignismeldung durchführen**); der Preis wird automatisch übernommen. Manuelle Nacharbeit ist nur bei nachträglichen Änderungen über **Fremdarbeitspreise berechnen** nötig.

---

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Ablauf aus Sicht der operativen Anwender. Jede angesprochene Seite und Aktion ist in den vorherigen Kapiteln beschrieben.

### Szenario 1: Neuer Fremdarbeitspreis für einen Unterlieferanten

**Auslöser.** Ein neuer Unterlieferant übernimmt das Beschichten eines Bauteils; der Einkauf hat einen Staffelpreis verhandelt und per E-Mail bestätigt bekommen.

**Einstieg in BC.** Der Administrator öffnet über die Suche (**Suchen**) die **Arbeitsplatzgruppen**, wählt die Arbeitsplatzgruppe „Beschichten“ und darin die **Arbeitsplatzgruppenkarte**.

**Kernablauf.**
1. Der Administrator trägt im Feld **Unterlieferantennr.** den neuen Kreditor ein; **Spez. EK-Preis** wird automatisch aktiviert.
2. Der Stammdatenverantwortliche öffnet über die **Kreditorkarte** im Menü **Zugehörig** die **Fremdarbeitspreise**.
3. Er legt eine erste Zeile mit **Einkaufsart** = **Kreditoren**, der Arbeitsplatzgruppe, **Referenz-Art** = **Alle Standardkatalogcodes**, **Definitionsart** = **Alle Artikel**, **Mindestmenge** 0 und dem Grundpreis an.
4. Für die höhere Staffel legt er eine zweite Zeile mit größerer **Mindestmenge** und niedrigerem **Preis** an und hinterlegt in einer Zeile einen **Mindestpreis** als Sockelbetrag.

**Abschluss.** Die Preise sind sofort wirksam und werden ab dem nächsten Fertigungsauftrag automatisch gezogen.

### Szenario 2: Fertigungsauftrag mit Fremdarbeit bis zur Einkaufsbestellung

**Auslöser.** Die Fertigungssteuerung gibt einen Fertigungsauftrag für ein Bauteil frei, dessen Arbeitsplan einen fremdvergebenen Arbeitsgang enthält.

**Einstieg in BC.** Der Fertigungsplaner öffnet den **freigegebenen Fertigungsauftrag**.

**Kernablauf.**
1. Er aktualisiert den Auftrag über **Prozess** > **Fertigungsauftrag aktualisieren**; das System trägt den **EK-Preis (direkt)** in den fremdvergebenen Arbeitsgang ein.
2. Über das Register **Zeilen** > **Arbeitsplan** kontrolliert er den ermittelten Preis und prüft im Infobereich **Fremdarbeitspreise** die zugrunde liegenden Zeilen.
3. Im **Fremdarbeitsarbeitsblatt** ruft er **Prozess** > **Fremdarbeit berechnen** auf und anschließend **Prozess** > **Ereignismeldung durchführen**.

**Abschluss.** Das System erzeugt die **Einkaufsbestellung** mit dem übernommenen Fremdarbeitspreis; die verarbeitete Zeile verschwindet aus dem Arbeitsblatt. Bei nachträglichen Mengenänderungen gleicht der Einkäufer den Preis über **Funktionen** > **Fremdarbeitspreise berechnen** in den Bestellzeilen an.

### Szenario 3: Befristeter Sonderpreis

**Auslöser.** Ein Unterlieferant gewährt für ein Quartal einen reduzierten Preis.

**Einstieg in BC.** Der Stammdatenverantwortliche öffnet über die **Artikelkarte** im Menü **Zugehörig** die **Fremdarbeitspreise**.

**Kernablauf.**
1. Er legt eine Preiszeile für die betroffene Kombination an und trägt den reduzierten **Preis** ein.
2. Über **Gültig ab** und **Gültig bis** grenzt er den Zeitraum auf das Quartal ein.

**Abschluss.** Innerhalb des Zeitraums zieht das System den Sonderpreis; danach greifen automatisch wieder die regulären Preiszeilen, weil abgelaufene Zeilen bei der Berechnung übergangen werden.
