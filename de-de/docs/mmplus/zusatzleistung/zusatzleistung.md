---
title: Anwenderhandbuch m+m Ext. Production Information
---

# Anwenderhandbuch m+m Ext. Production Information

## Einleitung

Die App **m+m Ext. Production Information** erweitert Microsoft Dynamics 365 Business Central um **erweiterte Fertigungseigenschaften** und um eine **Materialverfolgung** in der Fertigungskette. Fertigungsbezogene Zusatzinformationen — etwa Temperaturen, Zeiten, Programme, Prüfwerte oder Texte — werden an **Arbeitsplatzgruppen** und **Arbeitsplänen** hinterlegt und begleiten den Artikel anschließend durch **Verkaufsangebot**, **Verkaufsauftrag**, **Bestellung**, **Fertigungsauftrag** und **Produktionsbuchblatt** bis in die **Kapazitätsposten**.

**Zielgruppe:** Primär richtet sich das Modul an **operative Anwender** in Verkauf, Einkauf und Fertigung, die täglich Belegzeilen erfassen, Fertigungsaufträge kalkulieren und im **Produktionsbuchblatt** buchen. Sekundär richtet es sich an **Administratoren und Fertigungsplaner**, die die Stammdaten (Arbeitsplatzgruppen, Arbeitspläne, Materialarten) und die automatische Arbeitsplanermittlung einrichten.

**Kurzer Prozessüberblick:** Der Administrator hinterlegt je **Arbeitsplatzgruppe** und je **Arbeitsplan**-Arbeitsgang die gewünschten Eigenschaften und ihre **Standardwerte**. Über die **Materialart** wird ein **Masterarbeitsplannr.** zugeordnet, sodass Business Central beim Erfassen einer Verkaufs- oder Einkaufszeile automatisch den passenden **Arbeitsplan** und dessen Eigenschaften ermitteln kann. Der Anwender im Verkauf ruft über die Belegzeile die **Erw. Fertigungseigenschaften** auf und passt Werte an. Wird aus dem Auftrag ein **Fertigungsauftrag** erstellt, übernimmt Business Central Arbeitsplan und Eigenschaften; beim Buchen im **Produktionsbuchblatt** werden die Werte in die **Kapazitätsposten** übertragen und dort dauerhaft dokumentiert.

> Hinweis zur Terminologie: In diesem Handbuch bezeichnet **Arbeitsplatzgruppe** die kapazitätsführende Gruppe, **Arbeitsplatz** die einzelne Maschinenkapazität, **Charge** die chargengeführte Losverfolgung und **Übertragen** das Kennzeichen einer bereits an die Fertigung weitergegebenen Materialverfolgungszeile.

---

## Schnellstart für Anwender

Der Schnellstart folgt der vom Code erzwungenen Reihenfolge: zuerst Einrichtung und Stammdaten, dann die Belegarbeit, zuletzt das Buchen.

1. **Einrichtung/Stammdaten (einmalig, Administrator).**
   1. Öffnen Sie die **Materialart** und tragen Sie in der Gruppe **Erw. Fertigungseigenschaften** die **Masterarbeitsplannr.** ein; aktivieren Sie bei Bedarf **Materialverfolgung im Verkauf verwenden**.
   2. Öffnen Sie eine **Arbeitsplatzgruppe** und erfassen Sie über die Factbox **Erw. Eigenschaften** mit **Bearbeiten** die Eigenschaften und deren **Standardwert**.
   3. Kennzeichnen Sie Eigenschaften, deren Ergebnis vor dem Buchen zwingend erfasst werden muss, mit **Obligatorischer Istwert**.
2. **Verkaufszeile erfassen (Anwender Verkauf).** Legen Sie im **Verkaufsauftrag** eine Artikelzeile an. Business Central setzt die **Arbeitsplannr.** automatisch (aus Artikel, Artikelreferenz oder Masterarbeitsplan). Über die Zeilen­aktion **Erw. Fertigungseigenschaften** öffnen Sie den Editor und passen Werte an.
3. *(optional)* **Charge zuweisen.** Ist an der Materialart **Materialverfolgung im Verkauf verwenden** aktiv, weisen Sie über die Materialsuche Chargen zu; die Zuweisung erscheint in **Materialverfolgungsposten** (Zeilen­aktion).
4. **Fertigungsauftrag erstellen.** Geben Sie den Verkaufsauftrag frei und erstellen Sie den **Fertigungsauftrag**. Beim Berechnen des Fertigungsauftrags übernimmt Business Central den **Arbeitsplan**, die **Erw. Fertigungseigenschaften** und — falls vorhanden — die Materialverfolgung als Komponenten.
5. **Buchen im Produktionsbuchblatt.** Öffnen Sie das **Produktionsbuchblatt** zum Fertigungsauftrag und buchen Sie über **Buchung → Buchen**. Fehlt zu einer mit **Obligatorischer Istwert** gekennzeichneten Eigenschaft der **Istwert**, bricht Business Central mit einer Meldung ab.
6. **Ergebnis prüfen.** Nach dem Buchen finden Sie die übernommenen Eigenschaften als **Erw. Fertigungseigenschaften** in der Factbox der **Kapazitätsposten**.

---

## Einrichtung

Die Einrichtung dieses Moduls besteht weniger aus einer klassischen Einrichtungsseite als aus einer **mehrstufigen Stammdaten- und Aktivierungskette**. Die eigentliche Steuerung liegt in den Stammdaten (Materialart, Arbeitsplatzgruppe, Arbeitsplan, Artikelreferenz). Dieses Kapitel beschreibt zunächst die Einrichtungsseite und dann die beiden Aktivierungsketten.

### Erw. Fertigungseigenschaften Einrichtung

**Einstieg:** über die globale **Suchen**-Funktion (Kategorie Verwaltung).

Die Seite **Erw. Fertigungseigenschaften Einrichtung** ist eine unternehmensweite Einrichtungsseite (ein Datensatz je Mandant). In der ausgelieferten Version enthält sie **keine konfigurierbaren Felder**; sie legt lediglich den technischen Einrichtungsdatensatz an, sobald sie erstmals geöffnet wird. Es sind daher keine Feldwerte zu pflegen. Die gesamte fachliche Konfiguration erfolgt über die Stammdaten der folgenden Abschnitte.

> Berechtigungen: Der mitgelieferte Berechtigungssatz **MuM AP Permission** bestimmt die Berechtigungen für alle Tabellen, Seiten und Codeunits des Moduls. Er legt fest, welche Aktionen Anwender auf den Materialverfolgungsposten, den Eigenschaftsdaten und dem Verkaufs-Fertigungs-Bezug ausführen können. Weisen Sie ihn den Rollen zu, die mit erweiterten Fertigungseigenschaften arbeiten.

### Automatische Arbeitsplanermittlung einrichten

**Prozessintro.** Diese Kette richtet der **Administrator/Fertigungsplaner** einmalig vor der ersten Belegerfassung ein. Sie sorgt dafür, dass beim Anlegen einer Verkaufs- oder Einkaufszeile automatisch der richtige **Arbeitsplan** gezogen wird, ohne dass der Anwender ihn manuell wählen muss. Die Kette wird in der **täglichen Arbeit im Verkauf und Einkauf** konsumiert (siehe dortiger Abschnitt zur **Arbeitsplannr.**).

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Materialart pflegen.** Öffnen Sie die **Materialart** und tragen Sie in der Gruppe **Erw. Fertigungseigenschaften** die **Masterarbeitsplannr.** ein. Wenn gesetzt, verwendet Business Central diesen Arbeitsplan als Rückfall­wert, sobald zu einem Artikel weder am Artikel noch an einer Artikelreferenz ein Arbeitsplan hinterlegt ist. Ohne Eintrag und ohne Arbeitsplan am Artikel meldet der Aufruf der Eigenschaften **Kein Arbeitsplan gefunden/gesetzt!**.
2. **Artikel der Materialart zuordnen.** Ordnen Sie dem Artikel die **Materialart** zu (Feld der Artikelkarte aus dem Modul m+m Material Properties) und hinterlegen Sie ggf. am Artikel selbst einen **Arbeitsplan**. Wenn am Artikel ein Arbeitsplan gesetzt ist, hat dieser Vorrang vor dem Masterarbeitsplan.
3. *(optional)* **Kundenspezifische Artikelreferenz.** Hinterlegen Sie in der **Artikelreferenz** (Referenzart Debitor) eine abweichende **Arbeitsplannr.**. Wenn gesetzt, wird für Belege dieses Debitors dieser Arbeitsplan bevorzugt (Reihenfolge: Artikelreferenz → Artikel → Masterarbeitsplan).
4. **Ergebnis in der Belegzeile.** In **Verkaufsauftrag**, **Verkaufsangebot** und **Bestellung** wird die **Arbeitsplannr.** beim Erfassen der Artikelzeile automatisch gesetzt. Der Arbeitsplan muss den Status **Zertifiziert** haben; andernfalls kann keine Eigenschaftsstruktur erzeugt werden.

**Validierungs-/Abhängigkeitshinweis:** Die Materialart erzwingt die **Masterarbeitsplannr.** nur, wenn tatsächlich kein anderer Arbeitsplan ermittelt werden kann. Die Artikelreferenz erlaubt eine abweichende Arbeitsplannr. nur bei **Referenzart Debitor**.

### Erweiterte Fertigungseigenschaften pflegen (Stammdaten) einrichten

**Prozessintro.** Der **Administrator/Fertigungsplaner** definiert einmalig, welche Eigenschaften an welcher Kapazität geführt werden und mit welchen **Standardwerten**. Diese Werte werden in der täglichen Arbeit an Verkaufs-/Fertigungszeilen vererbt und dort ggf. angepasst (Cross-Link: **Tägliche Arbeit** und **Fertigungsauftrag und Produktionsbuchblatt**).

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Zuerst** die Standardwerte an der **Arbeitsplatzgruppe** hinterlegen (siehe Stammdaten → *Arbeitsplatzgruppe*). Wenn hier ein **Standardwert** gesetzt ist, wird er automatisch in **Wert** übernommen und dient allen Arbeitsgängen dieser Kapazität als Vorbelegung.
2. **Danach** je **Arbeitsplan**-Arbeitsgang prüfen (siehe Stammdaten → *Arbeitsplan*): Business Central übernimmt die Eigenschaften des Arbeitsgangs bevorzugt aus dem Arbeitsplan; findet es dort keine, erbt es sie von der zugeordneten **Arbeitsplatzgruppe**.
3. **Schließlich** die Eigenschaften kennzeichnen, deren Ergebnis der Werker vor dem Buchen zwingend erfassen muss: Feld **Obligatorischer Istwert** setzen. Wenn aktiviert, prüft Business Central beim Buchen im Produktionsbuchblatt, dass zu jeder solchen Eigenschaft ein **Istwert** vorliegt.

**Operativer Abschluss:** Der Werker trägt im **Produktionsbuchblatt** die **Istwerte** ein und bucht; ohne Istwert zu einer obligatorischen Eigenschaft wird die Buchung abgewiesen (Cross-Link: **Fertigungsauftrag und Produktionsbuchblatt**).

### Materialverfolgung im Verkauf einrichten

**Prozessintro.** Diese optionale Kette aktiviert die chargengenaue Reservierung von Vormaterial im Verkauf und deren Übergabe an den Fertigungsauftrag. Sie wird vor allem im Stahl-/Chargenumfeld genutzt und in der täglichen Arbeit über die **Materialverfolgungsposten** konsumiert.

**Nummerierte Einrichtungsschritte:**

1. **Materialart aktivieren.** Setzen Sie an der **Materialart** das Kennzeichen **Materialverfolgung im Verkauf verwenden**. Wenn aktiviert, ersetzt Business Central beim Zuweisen von Chargen über die Materialsuche im Verkauf die Standard-Chargenzuordnung durch die Materialverfolgung dieses Moduls; die zugewiesenen Chargen werden als **Materialverfolgungsposten** an der Verkaufszeile gespeichert. Ohne Kennzeichen bleibt die Standard-Chargenzuordnung von Business Central aktiv.
2. **Charge im Verkauf zuweisen.** Der Anwender weist in der Verkaufszeile über die Materialsuche Chargen zu (siehe **Tägliche Arbeit**). Die Zuweisung landet mengengenau — bei lagerplatzpflichtigen Lagerorten je **Lagerplatzcode** — in den **Materialverfolgungsposten**.
3. **Übergabe an den Fertigungsauftrag.** Beim Berechnen des aus dem Verkaufsauftrag erzeugten Fertigungsauftrags werden die noch nicht **übertragenen** Materialverfolgungsposten als **Fertigungsauftragskomponenten** angelegt und, sofern keine Bestellzuordnung vorliegt, mit **Chargennr./Seriennr.** reserviert. Danach ist der Posten als **Übertragen** gekennzeichnet.

---

## Stammdaten

### Arbeitsplatzgruppe: Erw. Eigenschaften und Standardwerte

**Prozessintro.** Der Administrator legt hier fest, welche Eigenschaften eine **Arbeitsplatzgruppe** grundsätzlich mitbringt und mit welchem **Standardwert**. Diese Standardwerte sind die Grundlage für alle Arbeitspläne, die diese Kapazität nutzen, und werden bis in Verkauf und Fertigung vererbt.

**Einstieg:** Öffnen Sie über die globale **Suchen**-Funktion die **Arbeitsplatzgruppen**. Sie können die Eigenschaften auf zwei Wegen pflegen: in der Liste **Arbeitsplatzgruppen** über die Factbox **Erw. Eigenschaften**, oder in der einzelnen Arbeitsplatzgruppe. Wählen Sie in der Factbox **Bearbeiten**, um den Editor zu öffnen, in dem Eigenschaften erfasst, geändert oder gelöscht werden.

Der Editor (**Erw. Fertigungseigenschaften**) zeigt für die Arbeitsplatzgruppe folgende Felder:

| Feld | Erläuterung |
|---|---|
| **Eigenschaftscode** | Wenn gesetzt, ordnet dieser Code der Kapazität eine definierte Eigenschaft aus dem Eigenschaftenstamm zu; nur auf Stammdatenebene (Arbeitsplatzgruppe) editierbar. |
| **Standardwert** | Wenn ein Wert gesetzt ist, wird er automatisch in **Wert** übernommen und dient allen Arbeitsgängen und Belegen, die diese Eigenschaft erben, als Vorbelegung. |
| **Eigenschaftswertname** | Zeigt den Klartextnamen des aktuell hinterlegten Werts (z. B. bei wertelistengeführten Eigenschaften); dient der Kontrolle, wird nicht manuell erfasst. |
| **Obligatorischer Istwert** | Wenn aktiviert, muss der zugehörige **Istwert** im Produktionsbuchblatt vor dem Buchen ausgefüllt sein; fehlt er, wird die Buchung abgewiesen. Ohne Kennzeichen ist der Istwert optional. |
| **Wert zulässig von** | Wenn gesetzt (nur bei numerischen Eigenschaften), begrenzt dieser Wert die zulässige Untergrenze; erfasste Werte darunter werden abgewiesen. |
| **Wert zulässig bis** | Wenn gesetzt (nur bei numerischen Eigenschaften), begrenzt dieser Wert die zulässige Obergrenze. |
| **Einheit** | Zeigt die Maßeinheit der Eigenschaft; sorgt für eindeutige Interpretation numerischer Werte in Beleg und Posten. |
| **Berechnungsformel** | Wenn hinterlegt (nur bei numerischen Eigenschaften), wird der Wert automatisch berechnet und das Feld **Wert** gesperrt. Über die Bearbeitungshilfe öffnen Sie den Formelgenerator. |
| **Anzeigereihenfolge** | Steuert die Sortierung der Eigenschaften in allen Ansichten; niedrigere Werte erscheinen zuerst. |
| **Nr.** / **Beschreibung** / **Art** | Zeigen die zugeordnete Kapazität (Nummer, Bezeichnung und **Art** — Arbeitsplatzgruppe oder Arbeitsplatz); nicht editierbar, dienen der Zuordnung des Werts zum Arbeitsgang. |
| *(ausgeblendete Hilfsfelder)* **Datentyp**, **Eigenschaftswerte verwenden** | Steuern intern die Feldeigenschaften (numerisch/Text, Werteliste) und werden nicht direkt gepflegt; sie bestimmen, ob **Wert zulässig von/bis** und die Berechnungsformel editierbar sind. |

**Prozessschritt:** Erfassen Sie je Kapazität die benötigten Eigenschaften und deren **Standardwert**; setzen Sie **Obligatorischer Istwert** dort, wo das Ergebnis später zwingend gebucht werden muss. Diese Werte werden anschließend in Arbeitsplan, Verkauf und Fertigung vererbt (Cross-Link: **Arbeitsplan**, **Tägliche Arbeit**, **Fertigungsauftrag und Produktionsbuchblatt**).

### Arbeitsplan und Arbeitsplanversion: Eigenschaften je Arbeitsgang

**Prozessintro.** Am **Arbeitsplan** (und je **Arbeitsplanversion**) werden die geerbten Eigenschaften je Arbeitsgang sichtbar und können arbeitsgangspezifisch überschrieben werden. Damit lassen sich abweichende Vorgaben je Fertigungsschritt hinterlegen, ohne die Stammwerte der Kapazität zu ändern.

**Einstieg:** Öffnen Sie über die globale **Suchen**-Funktion die **Arbeitspläne**, rufen Sie einen Arbeitsplan über die **Nr.** auf. Auf der rechten Seite zeigt die Factbox **Erw. Eigenschaften** die Eigenschaften des markierten Arbeitsgangs. Für versionierte Arbeitspläne gilt dies analog in der **Arbeitsplanversion**.

Die Factbox **Erw. Eigenschaften** zeigt (lesend) je Arbeitsgang:

| Feld | Erläuterung |
|---|---|
| **Eigenschaftsname** | Zeigt den Namen der Eigenschaft, die für diesen Arbeitsgang gilt. |
| **Standardwert** | Zeigt den aus der Arbeitsplatzgruppe geerbten Standardwert (nur bei Kapazitätseigenschaften sichtbar). |
| **Wert** | Zeigt den aktuell gültigen Wert; weicht er vom **Standardwert** ab, wird er farblich hervorgehoben, sodass angepasste Werte sofort erkennbar sind. |
| **Obligatorischer Istwert** | Zeigt an, ob zu dieser Eigenschaft im Produktionsbuchblatt ein Istwert Pflicht ist. |
| **Istwert** | Zeigt den erfassten Istwert (nur in den buchungsnahen Ansichten sichtbar). |
| **Einheit** | Zeigt die Maßeinheit der Eigenschaft. |

**Vererbungslogik (aus dem Code):** Beim Anlegen/Ändern eines Arbeitsgangs übernimmt Business Central die Eigenschaften bevorzugt aus dem **Arbeitsplan**; findet es dort keine, erbt es sie von der zugeordneten **Arbeitsplatzgruppe** bzw. dem **Arbeitsplatz**. Beim Kopieren von Arbeitsplanzeilen werden die Eigenschaften des Quellarbeitsplans mitgeführt. Wird eine Arbeitsplanzeile gelöscht, werden die zugehörigen Eigenschaften entfernt.

### Materialart: Masterarbeitsplan und Materialverfolgung

**Prozessintro.** Die **Materialart** (Stammdaten aus m+m Material Properties) steuert zwei Verhaltensweisen dieses Moduls: die automatische Arbeitsplanermittlung und die chargengenaue Materialverfolgung im Verkauf. Der Administrator pflegt sie je Materialart, bevor Artikel dieser Art in Belegen verwendet werden.

**Einstieg:** Öffnen Sie die **Materialarten** und dort die Karte einer Materialart; die Zusatzfelder stehen in der Gruppe **Erw. Fertigungseigenschaften**.

| Feld | Erläuterung |
|---|---|
| **Masterarbeitsplannr.** | Wenn gesetzt, verwendet Business Central diesen Arbeitsplan als Rückfallwert, sobald für einen Artikel dieser Materialart weder am Artikel noch an einer Artikelreferenz ein Arbeitsplan hinterlegt ist; erst dadurch können in Verkauf/Fertigung überhaupt erweiterte Fertigungseigenschaften erzeugt werden. Ohne Eintrag und ohne Arbeitsplan am Artikel bleibt der Aufruf der Eigenschaften ohne Struktur (Meldung **Kein Arbeitsplan gefunden/gesetzt!**). |
| **Materialverfolgung im Verkauf verwenden** | Wenn aktiviert, übernimmt dieses Modul die Chargenzuweisung im Verkauf: über die Materialsuche zugewiesene Chargen werden als **Materialverfolgungsposten** an der Verkaufszeile gespeichert und später an die Fertigungsauftragskomponenten übergeben. Ohne Kennzeichen bleibt die Standard-Chargenzuordnung von Business Central wirksam. |

> Die übrigen Felder der Materialart-Karte (z. B. **Materialartencode**, **Beschreibung**) gehören zum Grundmodul m+m Material Properties und dienen hier nur der Identifikation der Materialart; sie sind für die beiden oben genannten Steuerungen nicht relevant.

### Artikelreferenz: kundenspezifische Arbeitsplannr.

**Prozessintro.** Über die **Artikelreferenz** hinterlegt der Administrator je **Debitor** einen abweichenden Arbeitsplan, wenn ein Kunde denselben Artikel mit einem anderen Fertigungsablauf bestellt.

**Einstieg:** Öffnen Sie zum Artikel die **Artikelreferenzen** (Liste bzw. Posten); die Zusatzspalte steht am Ende der Zeile.

| Feld | Erläuterung |
|---|---|
| **Arbeitsplannr.** | Wenn gesetzt, wird für Belegzeilen dieses Debitors dieser Arbeitsplan bevorzugt vor dem Arbeitsplan des Artikels und dem Masterarbeitsplan ermittelt. Der Wert ist nur bei **Referenzart Debitor** zulässig; zulässig sind ausschließlich **zertifizierte** Arbeitspläne. |

---

## Tägliche Arbeit im Verkauf und Einkauf

Die tägliche Arbeit findet in den Standardbelegen statt; dieses Modul ergänzt dort eine Spalte und Zeilenaktionen. Welche Werte erscheinen, ist über die **Stammdaten** (Arbeitsplatzgruppe, Arbeitsplan, Materialart) und die **Einrichtung** (automatische Arbeitsplanermittlung) vorkonfiguriert — siehe die entsprechenden Abschnitte oben.

### Verkaufsangebot und Verkaufsauftrag

**Einstieg:** Öffnen Sie über die globale **Suchen**-Funktion den **Verkaufsauftrag** (bzw. das **Verkaufsangebot**) und erfassen Sie eine Artikelzeile.

In der Belegzeile ergänzt das Modul die Spalte **Arbeitsplannr.** und in der Zeilen-Menüleiste zwei Aktionen:

| Feld/Aktion | Erläuterung |
|---|---|
| **Arbeitsplannr.** (Spalte) | Wenn Sie eine Artikelzeile anlegen, setzt Business Central die Arbeitsplannr. automatisch (Artikelreferenz → Artikel → Masterarbeitsplan der Materialart). Ändern Sie die Arbeitsplannr. manuell und bestehen bereits erweiterte Fertigungseigenschaften zur Zeile, fragt Business Central **Bestehende erw. Fertigungseigenschaften werden gelöscht. Fortfahren?**; bestätigen Sie, werden die alten Eigenschaften verworfen und die Arbeitsplanversion neu gezogen. |
| **Erw. Fertigungseigenschaften** (Aktion) | Öffnen Sie über die Aktion den **Erw. Fertigungseigenschaften Editor**. Beim ersten Aufruf erzeugt Business Central die Eigenschaftsstruktur aus dem Arbeitsplan (je Arbeitsgang, mit geerbten Standardwerten). Sie passen die **Werte** an; abweichende Werte werden hervorgehoben. Voraussetzung: Zeilentyp **Artikel** und eine gesetzte **Nr.**; die Aktion ist nur in **Angebot** und **Auftrag** verfügbar. |
| **Materialverfolgungsposten** (Aktion) | Öffnen Sie über die Aktion die **Materialverfolgungsposten** der Zeile (siehe Kapitel *Historie*). Hier sehen Sie die den Chargen zugewiesenen Mengen. |

**Statusabhängigkeit:** Ist die Zeile über eine Streckenlieferung oder einen Sonderbestellbezug an eine Bestellung gekoppelt, öffnet der Editor **schreibgeschützt**, da die Eigenschaften dann vom Einkauf gesteuert werden.

### Bestellung

**Einstieg:** Öffnen Sie die **Bestellung** und erfassen Sie eine Artikelzeile.

| Feld/Aktion | Erläuterung |
|---|---|
| **Arbeitsplannr.** (Spalte) | Wird beim Erfassen der Artikelzeile automatisch ermittelt (Artikelreferenz → Artikel). Bei Streckenlieferung/Sonderbestellung wird die Arbeitsplannr. stattdessen aus der zugehörigen Verkaufszeile übernommen. |
| **Erw. Fertigungseigenschaften** (Aktion) | Öffnet den Editor für die Bestellzeile. Voraussetzung: Belegart **Anfrage** oder **Bestellung**, Zeilentyp **Artikel**, gesetzte **Nr.**, und die Zeile darf keine Streckenlieferung/Sonderbestellung sein (sonst schreibgeschützt, außer der zwischenbetriebliche Status ist **Neu**). |

> Bei **Streckenlieferung** oder **Sonderbestellung** überträgt Business Central beim Einfügen/Ändern der Bestellzeile die erweiterten Fertigungseigenschaften automatisch aus der verknüpften Verkaufszeile in die Bestellzeile; die Bestellzeile selbst erlaubt dann keine manuelle Arbeitsplanänderung.

### Erw. Fertigungseigenschaften Editor (Belegzeile)

Der aus der Belegzeile geöffnete Editor stellt die Eigenschaften **baumartig** je Arbeitsgang dar. Er enthält dieselben Felder wie der Stammdaten-Editor, mit folgenden Besonderheiten für die Belegarbeit:

| Feld | Erläuterung |
|---|---|
| **Arbeitsgangnr.** | Zeigt den Arbeitsgang, zu dem die darunter eingerückten Eigenschaften gehören; die Hauptzeile je Arbeitsgang ist hervorgehoben. |
| **Beschreibung** | Zeigt die Bezeichnung des Arbeitsgangs bzw. der Eigenschaft. |
| **Reihenfolge** | Wenn editierbar, bestimmt sie die spätere Reihenfolge der Arbeitsgänge im Fertigungsauftrag; nur auf der Arbeitsgang-Hauptzeile und nur solange noch keine Fertigungsauftrags-Arbeitsgänge existieren, änderbar. |
| **Wert** | Der vom Anwender erfassbare Wert der Eigenschaft; gesperrt, wenn eine **Berechnungsformel** hinterlegt ist. Abweichungen vom **Standardwert** werden hervorgehoben. |
| **Herkunft** | Zeigt, woher die Eigenschaft stammt. **Einkauf:** aus einer Einkaufszeile übernommen. **Verkauf:** aus einer Verkaufszeile übernommen. **Arbeitsplan:** direkt aus dem Arbeitsplan-Arbeitsgang. **Arbeitsplatzgruppe:** von der Kapazität geerbt. |

**Bearbeitbarkeit:** Für einen **beendeten** Fertigungsauftrag sowie für schreibgeschützt geöffnete Belege ist der Editor nicht editierbar.

---

## Fertigungsauftrag und Produktionsbuchblatt

### Vom Verkaufsauftrag zum Fertigungsauftrag

Wird aus einem freigegebenen **Verkaufsauftrag** ein **Fertigungsauftrag** erstellt und dieser berechnet, führt Business Central automatisch mehrere Schritte dieses Moduls aus (verifiziert im Code):

1. **Arbeitsplan übernehmen.** Ist an der Verkaufszeile eine **Arbeitsplannr.** gesetzt, wird sie samt **Arbeitsplanversionscode** an die Fertigungsauftragszeile übertragen.
2. **Arbeitsgänge aus der Reihenfolge aufbauen.** Existieren zur Fertigungsauftragszeile noch keine Arbeitsgänge, erzeugt Business Central sie aus der in den Eigenschaften hinterlegten **Reihenfolge** (Sequenz) und berechnet die Arbeitsgangkosten.
3. **Eigenschaften vererben.** Die erweiterten Fertigungseigenschaften der Verkaufszeile werden in die Fertigungsauftragszeile übernommen.
4. **Materialverfolgung übergeben.** Nicht **übertragene** Materialverfolgungsposten der Verkaufszeile werden als **Fertigungsauftragskomponenten** angelegt; ohne Bestellzuordnung erfolgt eine Reservierung je **Chargennr./Seriennr.**. Anschließend ist der Materialverfolgungsposten als **Übertragen** gekennzeichnet.

Beim Umstufen des Fertigungsauftrags (z. B. von *Geplant* nach *Freigegeben*) werden Eigenschaften und der Verkaufs-Fertigungs-Bezug mit umgezogen; beim Löschen einer Fertigungsauftragszeile werden die zugehörigen Eigenschaften entfernt und übergebene Materialverfolgungsposten wieder freigegeben.

Über die Zeilen der **Fertigungsauftragszeilen** (in allen Status: *Geplant*, *Fest geplant*, *Freigegeben*, *Beendet*) steht die Aktion **Erw. Fertigungseigenschaften** bereit, um die Eigenschaften der Zeile einzusehen bzw. — außer bei *Beendet* — anzupassen.

### Erw. Eigenschaften am Fertigungsauftrags-Arbeitsplan

Auf der Seite **Fertigungsauftrags-Arbeitsplan** zeigt die Factbox **Erw. Fertigungseigenschaften** je markiertem Arbeitsgang dessen Eigenschaften und Werte (lesend). Damit kann der Fertigungsplaner vor der Freigabe kontrollieren, welche Vorgaben je Arbeitsgang gelten.

### Buchen im Produktionsbuchblatt

**Einstieg:** Öffnen Sie zum **Freigegebenen Fertigungsauftrag** das **Produktionsbuchblatt** (bzw. das entsprechende Istmeldungs-Buchblatt). In der Factbox **Erw. Eigenschaften** sehen und erfassen Sie je Arbeitsgang die Eigenschaften; das Feld **Istwert** ist hier editierbar.

**Buchungsablauf:**

1. Erfassen Sie zu jedem Arbeitsgang die **Istwerte** der Eigenschaften.
2. Buchen Sie über **Buchung → Buchen**.
3. **Pflichtprüfung:** Für Zeilen vom Typ **Arbeitsplatzgruppe** prüft Business Central vor dem Buchen jede Eigenschaft mit **Obligatorischer Istwert**. Fehlt der **Istwert**, wird die Buchung mit einer Meldung abgewiesen (sinngemäß: *„Istwert in Erw. Fertigungseigenschaften darf nicht leer sein“* mit Angabe des betroffenen **Eigenschaftsnamens**).
4. Nach erfolgreicher Buchung werden die Eigenschaften und ihre **Istwerte** in die **Kapazitätsposten** übernommen (siehe *Historie*).

> Hinweis: Dieses Modul stellt keine eigenen Aktionen wie „Teilbeenden“ oder „Beenden“ bereit; es nutzt die Standard-Buchungslogik von Business Central. Teilbuchungen sind zulässig, soweit Business Central sie erlaubt; die erweiterten Eigenschaften werden bei jeder Buchung mitgeführt.

---

## Historie: Kapazitätsposten und Materialverfolgungsposten

### Kapazitätsposten

**Einstieg:** Öffnen Sie zum **Freigegebenen Fertigungsauftrag** über **Zugehörig → Auftrag → Posten → Kapazitätsposten** die **Kapazitätsposten**. In der Factbox **Erw. Fertigungseigenschaften** sehen Sie je gebuchtem Kapazitätsposten die dokumentierten Eigenschaften und **Istwerte**. Damit ist nach der Buchung dauerhaft nachvollziehbar, mit welchen Werten ein Arbeitsgang tatsächlich ausgeführt wurde.

### Materialverfolgungsposten

**Einstieg:** Öffnen Sie die **Materialverfolgungsposten** über die gleichnamige Zeilen­aktion einer Verkaufszeile (die Seite besitzt keinen eigenen Sucheintrag).

| Feld | Erläuterung |
|---|---|
| **Artikelnr.** | Zeigt den verfolgten Artikel. |
| **Variantencode** | Zeigt die Variante, sofern der Artikel variantengeführt ist. |
| **Chargennr.** | Zeigt die zugewiesene Charge des Vormaterials. |
| **Seriennr.** | Zeigt die zugewiesene Seriennummer, sofern seriengeführt. |
| **Menge** | Zeigt die der Charge zugewiesene Menge (bei lagerplatzpflichtigen Lagerorten je Lagerplatz aufgeteilt). |
| **Übertragen** | Wenn aktiviert, wurde der Posten bereits als Fertigungsauftragskomponente übergeben und wird bei der nächsten Fertigungsauftragsberechnung nicht erneut angelegt. |
| *(bei Bedarf einblendbar)* **Lagerortcode**, **Lagerplatzcode**, **Einheitencode**, **Bestellungsnr.**, **Bestellzeilennr.** | Zeigen Herkunfts- und Lagerdetails der Zuweisung; die Bestellangaben verweisen auf die Herkunftsbestellung der Charge. |
| *(technisch, standardmäßig ausgeblendet)* **Lfd. Nr.** und die **Herkunfts**felder (Herkunftsart/-unterart/-nr./-zeilennr. usw.) | Identifizieren die Belegzeile, zu der die Verfolgung gehört; bei Aufruf aus der Verkaufszeile ausgeblendet, da durch den Kontext bereits eindeutig. |

---

## Typische Anwendungsfälle

### Anwendungsfall 1: Kundenauftrag mit erweiterten Fertigungseigenschaften

**Auslöser:** Ein Kunde bestellt per E-Mail einen gefertigten Artikel mit besonderen Vorgaben (z. B. eine bestimmte Länge oder Temperatur).

**Einstieg in BC:** Der Verkäufer öffnet über **Suchen** den **Verkaufsauftrag** und erfasst die Artikelzeile. Business Central setzt die **Arbeitsplannr.** automatisch.

**Kernablauf:**
1. Über die Zeilen­aktion **Erw. Fertigungseigenschaften** öffnet der Verkäufer den Editor; Business Central erzeugt die Eigenschaftsstruktur aus dem Arbeitsplan.
2. Der Verkäufer trägt die Kundenvorgabe im Feld **Wert** ein; der abweichende Wert wird hervorgehoben.
3. Der Auftrag wird freigegeben und ein **Fertigungsauftrag** erstellt und berechnet — Arbeitsplan, Arbeitsgänge und Eigenschaften werden übernommen.
4. Der Werker öffnet das **Produktionsbuchblatt**, trägt die **Istwerte** ein und bucht über **Buchung → Buchen**. Ist eine Eigenschaft als **Obligatorischer Istwert** gekennzeichnet und der Istwert fehlt, verhindert Business Central die Buchung.

**Abschluss:** In den **Kapazitätsposten** dokumentiert die Factbox **Erw. Fertigungseigenschaften** dauerhaft die tatsächlich gebuchten Werte.

### Anwendungsfall 2: Chargengenaue Materialzuweisung im Verkauf

**Auslöser:** Für einen Auftrag im Chargenumfeld soll bereits im Verkauf festgelegt werden, welche konkrete **Charge** Vormaterial verwendet wird.

**Einstieg in BC:** Der Sachbearbeiter öffnet den **Verkaufsauftrag** und die betreffende Artikelzeile. Voraussetzung: An der **Materialart** des Artikels ist **Materialverfolgung im Verkauf verwenden** aktiviert.

**Kernablauf:**
1. Über die Materialsuche weist der Sachbearbeiter dem Artikel eine oder mehrere **Chargen** zu; die Zuweisung wird mengengenau (bei lagerplatzpflichtigem Lagerort je **Lagerplatzcode**) als **Materialverfolgungsposten** gespeichert.
2. Über die Zeilen­aktion **Materialverfolgungsposten** kontrolliert er **Chargennr.** und **Menge**.
3. Bei der Erstellung/Berechnung des **Fertigungsauftrags** werden die noch nicht **übertragenen** Posten als **Fertigungsauftragskomponenten** angelegt und je **Chargennr./Seriennr.** reserviert.

**Abschluss:** Die Materialverfolgungsposten sind als **Übertragen** gekennzeichnet; die reservierten Chargen stehen in den Fertigungsauftragskomponenten.

---

## FAQ und Troubleshooting

### 1. Warum erscheint beim Aufruf der Erw. Fertigungseigenschaften die Meldung „Kein Arbeitsplan gefunden/gesetzt!“?
Weil zur Zeile kein Arbeitsplan ermittelt werden konnte. Business Central sucht in der Reihenfolge **Artikelreferenz (Debitor) → Artikel → Masterarbeitsplannr. der Materialart**. Hinterlegen Sie einen **zertifizierten** Arbeitsplan an einer dieser Stellen.

### 2. Warum kann ich einen Arbeitsplan nicht verwenden, obwohl er existiert?
Beim Erzeugen der Eigenschaftsstruktur wird der Arbeitsplanstatus geprüft; nur **zertifizierte** Arbeitspläne werden akzeptiert. Setzen Sie den Arbeitsplan auf **Zertifiziert**.

### 3. Warum werde ich beim Ändern der Arbeitsplannr. gefragt, ob bestehende Eigenschaften gelöscht werden?
Weil zur Zeile bereits erweiterte Fertigungseigenschaften existieren. Ein neuer Arbeitsplan bedeutet eine andere Arbeitsgang-/Eigenschaftsstruktur; bestätigen Sie mit **Fortfahren**, werden die alten Eigenschaften verworfen und neu aufgebaut. Brechen Sie ab, bleibt die alte Arbeitsplannr. erhalten.

### 4. Warum kann ich die Buchung im Produktionsbuchblatt nicht abschließen?
Weil zu mindestens einer Eigenschaft mit Kennzeichen **Obligatorischer Istwert** der **Istwert** fehlt. Business Central prüft dies für Zeilen vom Typ **Arbeitsplatzgruppe** vor dem Buchen. Tragen Sie die fehlenden **Istwerte** in der Factbox **Erw. Eigenschaften** ein.

### 5. Warum lässt sich das Feld „Wert“ einer Eigenschaft nicht bearbeiten?
Weil zu dieser Eigenschaft eine **Berechnungsformel** hinterlegt ist; der Wert wird dann automatisch berechnet und das Feld gesperrt. Entfernen Sie die Formel im Stammdaten-Editor, wenn Sie den Wert manuell erfassen möchten.

### 6. Warum ist der Editor der Erw. Fertigungseigenschaften manchmal schreibgeschützt?
Bei **beendeten** Fertigungsaufträgen sowie bei Verkaufs-/Einkaufszeilen, die über **Streckenlieferung** oder **Sonderbestellung** gekoppelt sind. In diesen Fällen werden die Eigenschaften vom verknüpften Beleg gesteuert und dürfen an dieser Stelle nicht geändert werden.

### 7. Warum werden meine zugewiesenen Chargen nicht als normale Artikelverfolgung, sondern als Materialverfolgungsposten geführt?
Weil an der **Materialart** das Kennzeichen **Materialverfolgung im Verkauf verwenden** aktiviert ist. Dann übernimmt dieses Modul die Zuweisung und speichert sie als **Materialverfolgungsposten**, damit die Chargen später an die Fertigungsauftragskomponenten übergeben werden können.

### 8. Warum taucht ein Materialverfolgungsposten nicht erneut als Komponente auf?
Weil er beim Berechnen des Fertigungsauftrags bereits als Komponente angelegt und dabei als **Übertragen** gekennzeichnet wurde. Übertragene Posten werden nicht doppelt übergeben. Wird die Fertigungsauftragszeile gelöscht, wird das Kennzeichen zurückgesetzt.

### 9. Warum kann ich an einer Artikelreferenz keine Arbeitsplannr. eintragen?
Weil die Arbeitsplannr. nur für Artikelreferenzen der **Referenzart Debitor** zulässig ist. Für andere Referenzarten wird das Feld beim Speichern abgewiesen.

### 10. Wo sehe ich nach der Produktion, mit welchen Werten tatsächlich gefertigt wurde?
In den **Kapazitätsposten** des Fertigungsauftrags. Öffnen Sie die Kapazitätsposten und blenden Sie die Factbox **Erw. Fertigungseigenschaften** ein; dort stehen die gebuchten Eigenschaften mit ihren **Istwerten**.
