---
title: Anwenderhandbuch m+m Unit Conversion with DACH
---

# Anwenderhandbuch m+m Unit Conversion with DACH

## Einleitung

Die Erweiterung **m+m Unit Conversion with DACH** ergänzt die DACH-Belege des Liefermahnwesens
(**Lieferanmahnung** und **Reg. Lieferanmahnung**) sowie die **Lieferanmahnungsposten** um Mengen in den
zusätzlichen Einheiten **KG**, **Meter** und **Stück**. Sie überträgt damit die Mengenumrechnung des Moduls
*m+m Unit Conversion* in die österreichisch/schweizerisch/deutsch lokalisierten Liefermahnbelege.

**Zielgruppe.** Primär richtet sich das Modul an **operative Anwender im Einkauf**, die im Tagesgeschäft
Lieferanmahnungen bearbeiten und die angemahnten Mengen zusätzlich in KG, Meter oder Stück sehen möchten – etwa im
Stahl- oder Metallhandel, wo eine Bestellzeile in Basiseinheiten geführt, das Gewicht oder die Länge aber
mitgeführt werden soll. Sekundär betrifft es **Administratoren und Key-User**, die einmalig die fachlichen
Voraussetzungen der Mengenumrechnung im abhängigen Modul hinterlegen (siehe **Einrichtung**).

**Kurzer Prozessüberblick.** Sobald in einer Lieferanmahnungszeile eine **Menge** erfasst oder geändert wird,
berechnet das Modul im Hintergrund die Werte für **KG**, **Meter** und **Stück** sowie deren Rest- und
Bestellmengen und zeigt sie als zusätzliche, nicht erfassbare Spalten an. Beim **Registrieren** der
Lieferanmahnung werden die Umrechnungswerte und die zugrunde liegenden Umrechnungsfaktoren in die
**Reg. Lieferanmahnung** und die **Lieferanmahnungsposten** übernommen. Das Modul liefert **keine eigene
Einrichtungsseite und keine eigenen Stammdaten**; die Umrechnung stützt sich vollständig auf die Faktoren des
Moduls *m+m Unit Conversion*.

> **Grundprinzip:** Alle KG-, Meter- und Stück-Spalten dieses Moduls sind **reine Anzeigefelder**. Sie werden
> automatisch berechnet und können in den Belegen **nicht direkt bearbeitet** werden. Erfasst wird ausschließlich die
> **Menge** in der Basiseinheit.

---

## Schnellstart für Anwender

Die folgenden Schritte führen in Abhängigkeitsreihenfolge (zuerst die einmalige Einrichtung, dann der Beleg, dann das
Registrieren) zum Ergebnis. Details stehen in den jeweiligen Kapiteln.

1. **Voraussetzungen prüfen (einmalig, Administrator/Key-User).** Stellen Sie sicher, dass die Apps
   *m+m Cloud Base*, *m+m Unit Conversion* und *m+m Unit Conversion with DACH* installiert sind und dass im Modul
   *m+m Unit Conversion* die **Umrechnungsfaktoren** (KG je Meter, KG je Stück) für die betroffenen Artikel gepflegt
   sind. Ohne diese Faktoren bleiben **KG**, **Meter** und **Stück** auf 0 (siehe Kapitel **Einrichtung**).
2. **Lieferanmahnung öffnen.** Öffnen Sie die Liste **Lieferanmahnungen** und öffnen bzw. erstellen Sie die
   betreffende **Lieferanmahnung**.
3. **Menge erfassen.** Tragen Sie in der Belegzeile die **Menge** in der Basiseinheit ein. Die Spalten **KG**,
   **Meter** und **Stück** – sowie **Rest KG/Meter/Stück** und **Bestell KG/Meter/Stück** – werden daraufhin
   automatisch berechnet und angezeigt.
4. **Werte kontrollieren.** Prüfen Sie in der Zeile die berechneten Umrechnungsmengen. Weichen sie von der Erwartung
   ab, liegt dies an den Umrechnungsfaktoren des Artikels (siehe **Einrichtung**), nicht an einer Eingabe in diesen
   Spalten.
5. **Registrieren.** Lösen Sie am Beleg die Aktion **Registrieren** aus. Es entsteht eine **Reg. Lieferanmahnung**;
   die Umrechnungswerte und -faktoren werden dabei in die registrierte Zeile und in die **Lieferanmahnungsposten**
   übernommen.

> Der Schnellstart ist der minimale Weg. Die ausführlichen Abläufe mit Auslöser und Zuständigkeiten finden Sie im
> Kapitel **Typische Anwendungsfälle**.

---

## Einrichtung

Für die Erweiterung selbst ist im Web Client **keine zusätzliche Einrichtung** erforderlich: Sie enthält weder eine
Einrichtungsseite noch Stammdaten. Damit in den Spalten **KG**, **Meter** und **Stück** überhaupt Werte erscheinen,
müssen jedoch die **fachlichen Voraussetzungen der Mengenumrechnung** erfüllt sein. Diese werden im abhängigen Modul
*m+m Unit Conversion* gepflegt und wirken sich anschließend in den Liefermahnbelegen aus. Der folgende Abschnitt
beschreibt diese Kette in Abhängigkeitsreihenfolge.

### Mengenumrechnung für Lieferanmahnungen einrichten

**Wer richtet ein und wann.** Der **Administrator** bzw. **Key-User** hinterlegt die Umrechnung einmalig je Artikel,
**bevor** Lieferanmahnungen für diese Artikel bearbeitet werden. Angewendet werden die Einstellungen später in der
täglichen Arbeit an der **Lieferanmahnung** (siehe **Tägliche Arbeit an der Lieferanmahnung**) sowie in der
**Reg. Lieferanmahnung** und den **Lieferanmahnungsposten** (siehe **Historie und Nachverfolgung**).

**Ablauf in Abhängigkeitsreihenfolge:**

1. **Zuerst – Apps bereitstellen.** Stellen Sie in der Erweiterungsverwaltung sicher, dass *m+m Cloud Base*,
   *m+m Unit Conversion* und *m+m Unit Conversion with DACH* installiert sind. Wenn die Abhängigkeit
   *m+m Unit Conversion* fehlt, dann stehen die Umrechnungsspalten in den Liefermahnbelegen nicht zur Verfügung, weil
   dieses Modul deren Berechnung übernimmt.
2. **Danach – Umrechnungsfaktoren am Artikel pflegen.** Hinterlegen Sie im Modul *m+m Unit Conversion* je Artikel die
   **theoretischen** Umrechnungsfaktoren (KG je Meter, KG je Stück). Wenn diese Faktoren gepflegt sind, dann kann
   Business Central aus einer erfassten **Menge** automatisch **KG**, **Meter** und **Stück** ableiten; fehlen sie,
   dann bleiben die Umrechnungsspalten 0.
3. **Schließlich – im Tagesablauf anwenden.** Sobald ein Anwender in der Lieferanmahnungszeile die **Menge** erfasst
   oder ändert, rechnet das System die Umrechnungsspalten automatisch nach (siehe **Tägliche Arbeit an der
   Lieferanmahnung**). Damit ist die Kette geschlossen: Die Umrechnung greift ohne weiteres Zutun des Anwenders in den
   Belegen.

**Herkunft der Faktoren je Zeile (Abhängigkeitshinweis).** Bezieht sich die Lieferanmahnungszeile auf eine
**Bestellung** (Bestellnummer und -zeilennummer sind gesetzt), dann übernimmt das Modul die **theoretischen** und
**tatsächlichen** Faktoren aus der zugehörigen Bestellzeile. Existiert keine passende Bestellzeile, dann werden die
theoretischen Faktoren aus den Artikelstammdaten der Mengenumrechnung gelesen und die tatsächlichen Faktoren mit 0
angesetzt. Pflegen Sie die Faktoren daher vollständig, damit die angezeigten Umrechnungsmengen belastbar sind.

> **Lizenzhinweis.** Beim Anmelden prüft das Modul die Lizenz der App über die zentrale Lizenzverwaltung der
> m+m-Module. Ist die App nicht ordnungsgemäß lizenziert, dann können die Umrechnungsfunktionen eingeschränkt sein.
> Dies ist eine technische Prüfung im Hintergrund und erfordert keine Aktion des Anwenders.

### Berechtigungen

Das Modul liefert den Berechtigungssatz **m+m UC Permission** (Anzeigename „All permissions“) mit. Er bestimmt die
Berechtigungen für die drei Verarbeitungs-Codeunits der Erweiterung und legt fest, welche Aktionen ein Anwender im
Zusammenhang mit der Mengenumrechnung der Liefermahnbelege ausführen kann. Weisen Sie diesen Berechtigungssatz den
Anwendern zu, die Lieferanmahnungen bearbeiten und registrieren. Die eigentliche Berechtigung für die Belege selbst
(Zugriff auf **Lieferanmahnung**, **Reg. Lieferanmahnung** und **Lieferanmahnungsposten**) wird zusätzlich über die
Berechtigungssätze der Basis- und DACH-Module gesteuert.

---

## Tägliche Arbeit an der Lieferanmahnung

Die tägliche Arbeit findet an der **Lieferanmahnung** statt. Der Beleg selbst gehört zum DACH-Liefermahnwesen; diese
Erweiterung ergänzt die **Zeilen** um die Umrechnungsspalten KG, Meter und Stück in jeweils mehreren Ausprägungen
(Menge, Rest, Bestell) sowie um die zugrunde liegenden Umrechnungsfaktoren.

**Einstieg:** Öffnen Sie die Liste **Lieferanmahnungen** und öffnen bzw. erstellen Sie die betreffende
**Lieferanmahnung**. Die zusätzlichen Spalten erscheinen im Zeilenbereich des Belegs neben der jeweiligen
Basismenge.

**Steuernde Einrichtung.** Ob und mit welchen Werten die Umrechnungsspalten gefüllt sind, hängt vollständig von der
**Mengenumrechnung** des Artikels ab (Modul *m+m Unit Conversion*, siehe **Mengenumrechnung für Lieferanmahnungen
einrichten**). Sind dort keine Umrechnungsfaktoren hinterlegt, dann bleiben KG, Meter und Stück auf 0.

### Spalten der Lieferanmahnungszeile

Business Central zeigt in der Zeile die Felder des DACH-Belegs und die von dieser Erweiterung ergänzten
Umrechnungsspalten gemeinsam auf einem Bildschirm. Die folgende Tabelle dokumentiert die von dieser Erweiterung
hinzugefügten Spalten. Alle Spalten sind **Anzeigefelder** und nicht erfassbar; erfasst wird ausschließlich die
Basismenge.

**Bezugsgröße aus dem Basisbeleg:**

| Feld | Erläuterung |
|------|-------------|
| Menge | Basismenge der angemahnten Zeile in der Basiseinheit. Wenn Sie diese Menge erfassen oder ändern, dann berechnet das Modul daraus alle KG-, Meter- und Stück-Spalten neu. Sie ist damit die einzige erfassbare Bezugsgröße der Umrechnung. |

**Umgerechnete Belegmenge (Anzeige):**

| Feld | Erläuterung |
|------|-------------|
| KG | Wenn der Artikel eine KG-Umrechnung besitzt, dann zeigt diese Spalte das Gewicht der angemahnten Menge in Kilogramm. Sie ist die Bezugsgröße für **Rest KG** und **Bestell KG**. |
| Meter | Wenn eine Meter-Umrechnung besteht, dann zeigt diese Spalte die Länge der angemahnten Menge in Meter. |
| Stück | Wenn eine Stück-Umrechnung besteht, dann zeigt diese Spalte die Stückzahl der angemahnten Menge. |

**Bestellmengen umgerechnet (Anzeige):** Diese Spalten spiegeln die Nachbestellmenge der Zeile in den drei Einheiten.

| Feld | Erläuterung |
|------|-------------|
| Bestell KG | Wenn zur Zeile eine Nachbestellmenge geführt wird, dann zeigt diese Spalte deren Gewicht in Kilogramm. So erkennen Sie das nachzubestellende Gewicht, ohne die Basismenge selbst umrechnen zu müssen. |
| Bestell Meter | Zeigt die Nachbestellmenge der Zeile umgerechnet in Meter. |
| Bestell Stück | Zeigt die Nachbestellmenge der Zeile umgerechnet in Stück. |

**Restmengen umgerechnet (Anzeige):** Diese Spalten spiegeln die Restmenge der Zeile in den drei Einheiten.

| Feld | Erläuterung |
|------|-------------|
| Rest KG | Wenn die Zeile eine offene Restmenge hat, dann zeigt diese Spalte das noch offene Gewicht in Kilogramm. So sehen Sie den offenen Anteil der Mahnung gewichtsbezogen. |
| Rest Meter | Zeigt die offene Restmenge der Zeile umgerechnet in Meter. |
| Rest Stück | Zeigt die offene Restmenge der Zeile umgerechnet in Stück. |

**Umrechnungsfaktoren (standardmäßig ausgeblendet).** Die folgenden vier Faktorspalten sind in der Standardansicht
**ausgeblendet** und können bei Bedarf über die Personalisierung eingeblendet werden. Sie dienen der Nachvollziehbarkeit,
mit welchen Faktoren die obigen Mengen berechnet wurden, und werden – wie alle Spalten dieses Moduls – nicht erfasst,
sondern aus der Bestellzeile bzw. den Artikelstammdaten übernommen.

| Feld | Erläuterung |
|------|-------------|
| Theoretische KG pro Meter | Wenn kein tatsächlicher Faktor vorliegt, dann rechnet das Modul mit diesem theoretischen Gewicht je Meter aus den Artikelstammdaten. So bleibt die Umrechnung auch ohne bestellbezogenen Istwert nachvollziehbar. |
| Theoretische KG pro Stück | Theoretisches Gewicht je Stück aus den Artikelstammdaten; wird verwendet, wenn kein tatsächlicher Faktor je Stück vorliegt. |
| Tatsächliche KG pro Meter | Wenn die Zeile auf eine Bestellung verweist und dort ein Istgewicht je Meter geführt wird, dann verwendet das Modul diesen tatsächlichen Faktor anstelle des theoretischen. Dadurch entsprechen KG und Meter dem real bestellten Material. |
| Tatsächliche KG pro Stück | Tatsächliches Gewicht je Stück aus der zugehörigen Bestellzeile; hat Vorrang vor dem theoretischen Faktor je Stück. |

**Berechnungslogik (Validierung/Abhängigkeit).** Das Modul berechnet die Umrechnungsspalten automatisch beim Anlegen
und Ändern einer Zeile. Für jede Einheit gilt: Liegt ein **tatsächlicher** Faktor (aus der Bestellzeile) vor, dann wird
dieser verwendet; andernfalls greift der **theoretische** Faktor aus den Artikelstammdaten. Die Umrechnung wirkt nur
bei Zeilen der Art **Artikel**; bei anderen Zeilenarten bleiben KG, Meter und Stück ohne Wert.

---

## Historie und Nachverfolgung

Die Umrechnungsspalten sind nicht nur im aktiven Beleg sichtbar, sondern werden auch in den nachgelagerten
Datenbeständen geführt, damit die angemahnten Mengen in KG, Meter und Stück dauerhaft nachvollziehbar bleiben.

### Reg. Lieferanmahnung – Zeilen

Beim **Registrieren** einer Lieferanmahnung entsteht eine **Reg. Lieferanmahnung**. Deren Zeilen tragen dieselben
Umrechnungsspalten wie der aktive Beleg: **KG**, **Meter**, **Stück**, die zugehörigen **Bestell**- und **Rest**-Spalten
sowie die vier ausgeblendeten Faktorspalten. Die Bedeutung der einzelnen Spalten entspricht der Tabelle unter
**Spalten der Lieferanmahnungszeile**; sie werden hier nicht erneut erfasst, sondern zeigen den zum Zeitpunkt des
Registrierens gültigen Zustand.

**Einstieg:** Öffnen Sie die Liste **Reg. Lieferanmahnungen**, wählen Sie den Beleg und wechseln Sie in die Zeilen.

**Fortschreibung beim Registrieren.** Beim Registrieren übernimmt das Modul die Umrechnungswerte und die
**theoretischen** wie **tatsächlichen** Faktoren aus der Lieferanmahnungszeile in die registrierte Zeile. Anschließend
werden die Umrechnungsmengen in der registrierten Zeile auf Basis dieser übernommenen Faktoren erneut berechnet, sodass
sie dem Basiswert der Zeile entsprechen.

### Lieferanmahnungsposten

Die **Lieferanmahnungsposten** protokollieren die angemahnten Mengen als Posten. Diese Erweiterung ergänzt die
Postenliste um dieselben Umrechnungsspalten (**KG**, **Meter**, **Stück** sowie **Bestell**- und **Rest**-Varianten und
die ausgeblendeten Faktorspalten). Die Werte werden beim Erzeugen der Posten aus der Lieferanmahnungszeile übernommen
bzw. auf Basis der übernommenen Faktoren berechnet.

**Einstieg:** Öffnen Sie die **Lieferanmahnungsposten** über **Suchen** oder über die Postenansicht des zugehörigen
Belegs. Die Liste hat keine übergeordnete Stammdatenseite; der Einstieg über **Suchen** bzw. den Belegaufriss ist daher
der vorgesehene Weg.

**Nutzen.** So lässt sich später gewichts-, längen- oder stückbezogen auswerten, welche Mengen in welchem Umfang
angemahnt wurden – auch dann, wenn der ursprüngliche Beleg bereits registriert ist.

---

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie das Modul im Arbeitsalltag ausgelöst und in Business Central abgewickelt wird. Alle
Schritte entsprechen dem im Programmcode dieser Erweiterung hinterlegten Ablauf.

### Anwendungsfall 1: Überfällige Lieferung anmahnen und Mengen in KG/Meter prüfen

**Auslöser.** Eine Bestellung über Stahlprofile ist überfällig. Der Einkauf beschließt, den Lieferanten schriftlich zu
mahnen, und möchte im Mahnbeleg neben der Basismenge auch das angemahnte **Gewicht** und die **Länge** sehen.

**Einstieg in BC.** Der Anwender öffnet die Liste **Lieferanmahnungen** und öffnet bzw. erstellt die betreffende
**Lieferanmahnung** zum Lieferanten.

**Kernablauf.**
1. In der Belegzeile erfasst der Anwender die angemahnte **Menge** in der Basiseinheit.
2. Das Modul füllt daraufhin automatisch **KG**, **Meter** und **Stück** sowie die zugehörigen **Rest**- und
   **Bestell**-Spalten. Bezieht sich die Zeile auf eine Bestellung, dann werden die **tatsächlichen** Faktoren aus der
   Bestellzeile herangezogen, andernfalls die **theoretischen** Faktoren aus den Artikelstammdaten.
3. Der Anwender kontrolliert die berechneten Umrechnungsmengen. Sind sie 0, prüft er die Umrechnungsfaktoren im Modul
   *m+m Unit Conversion* (siehe **Einrichtung**).
4. Der Anwender löst die Aktion **Registrieren** aus.

**Abschluss.** Es entsteht eine **Reg. Lieferanmahnung**; die Umrechnungswerte und -faktoren stehen in der
registrierten Zeile und in den **Lieferanmahnungsposten** dauerhaft zur Verfügung.

### Anwendungsfall 2: Rückfrage zu bereits angemahnten Mengen anhand der Posten

**Auslöser.** Ein Lieferant oder eine interne Stelle fragt nach, in welchem Umfang eine Position bereits angemahnt
wurde – bezogen auf Gewicht bzw. Länge, nicht nur auf die Basismenge.

**Einstieg in BC.** Der Anwender öffnet über **Suchen** die **Lieferanmahnungsposten**.

**Kernablauf.**
1. Der Anwender filtert die Posten auf den betreffenden Artikel bzw. Beleg.
2. In den Spalten **KG**, **Meter** und **Stück** liest er die angemahnten Mengen in den zusätzlichen Einheiten ab;
   über **Rest KG/Meter/Stück** erkennt er den seinerzeit offenen Anteil.

**Abschluss.** Die Auskunft erfolgt vollständig aus der Postenliste; eine Buchung oder Änderung ist nicht erforderlich,
da alle Spalten reine Anzeigefelder sind.

---

## FAQ und Troubleshooting

### 1. Warum kann ich die Felder KG, Meter und Stück nicht ausfüllen?
Weil alle Umrechnungsspalten dieses Moduls **reine Anzeigefelder** sind (im Belegzeilen- und Postenlayout nicht
erfassbar). Erfasst wird ausschließlich die **Menge** in der Basiseinheit; daraus berechnet das Modul KG, Meter und
Stück automatisch.

### 2. Warum bleiben KG, Meter und Stück auf 0?
Weil für den Artikel keine **Umrechnungsfaktoren** hinterlegt sind. Diese werden im abhängigen Modul
*m+m Unit Conversion* gepflegt (KG je Meter, KG je Stück). Ohne Faktoren kann das System die Basismenge nicht
umrechnen, und die Spalten bleiben 0 (siehe **Einrichtung**).

### 3. Wann werden die Werte berechnet?
Immer beim **Anlegen** und **Ändern** einer Zeile. Sobald Sie die **Menge** erfassen oder ändern, rechnet das Modul die
Umrechnungsspalten neu. Ein manuelles Anstoßen ist nicht nötig.

### 4. Woher stammen die Umrechnungsfaktoren einer Zeile?
Bezieht sich die Zeile auf eine **Bestellung** (Bestellnummer und -zeilennummer gesetzt), dann werden die theoretischen
und tatsächlichen Faktoren aus der zugehörigen Bestellzeile übernommen. Andernfalls liest das Modul die theoretischen
Faktoren aus den Artikelstammdaten der Mengenumrechnung; die tatsächlichen Faktoren sind dann 0.

### 5. Was ist der Unterschied zwischen „theoretisch“ und „tatsächlich“?
Der **tatsächliche** Faktor stammt aus der konkreten Bestellzeile (real bestelltes Material) und hat Vorrang. Liegt kein
tatsächlicher Faktor vor, dann rechnet das Modul mit dem **theoretischen** Faktor aus den Artikelstammdaten.

### 6. Für welche Zeilenarten wirkt die Umrechnung?
Nur für Zeilen der Art **Artikel**. Bei anderen Zeilenarten (z. B. Sachkonto) bleiben KG, Meter und Stück ohne Wert, da
die Umrechnung artikelbezogen ist.

### 7. Warum sehe ich die Faktorspalten (theoretisch/tatsächlich) nicht?
Weil die vier Faktorspalten in der Standardansicht **ausgeblendet** sind. Über die Personalisierung der Zeile können Sie
sie bei Bedarf einblenden, um die Berechnungsgrundlage nachzuvollziehen.

### 8. Bleiben die Umrechnungswerte nach dem Registrieren erhalten?
Ja. Beim **Registrieren** werden die Werte und Faktoren in die **Reg. Lieferanmahnung** und die
**Lieferanmahnungsposten** übernommen, sodass der angemahnte Mengenstand in KG, Meter und Stück dauerhaft
nachvollziehbar bleibt.

### 9. Wo finde ich die angemahnten Mengen nach dem Registrieren wieder?
In den Zeilen der **Reg. Lieferanmahnung** und in den **Lieferanmahnungsposten**. Beide tragen dieselben
Umrechnungsspalten wie der aktive Beleg.

### 10. Welche Berechtigung benötige ich?
Für die Verarbeitungsfunktionen des Moduls den Berechtigungssatz **m+m UC Permission**. Der Zugriff auf die Belege
selbst (Lieferanmahnung, Reg. Lieferanmahnung, Lieferanmahnungsposten) wird zusätzlich über die Berechtigungssätze der
Basis- und DACH-Module gesteuert.
