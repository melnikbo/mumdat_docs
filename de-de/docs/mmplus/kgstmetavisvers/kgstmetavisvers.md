---
title: Anwenderhandbuch m+m Unit Conversion with Logistic Management
---

# Anwenderhandbuch m+m Unit Conversion with Logistic Management

## Einleitung

Die App m+m „Unit Conversion with Logistic Management“ verbindet die
**Einheitenumrechnung** (KG / Meter / Stück) mit den Belegen der Avisierung und
der Versandplanung in „Microsoft Dynamics 365 Business Central“. Sobald ein
Artikel in **KG**, **Meter** und **Stück** geführt wird, stehen diese drei
Mengengrößen auch in der **Avisierung**, in der **Versandplanung** und in der
**Artikelverfolgungszuordnung** zur Verfügung. Gibt der Anwender eine dieser
Größen ein, berechnet die App die beiden übrigen automatisch und übernimmt die
zugewiesenen Mengen in die logistischen Folgebelege (Einkaufszeile,
Verkaufszeile, Umlagerungszeile, Wareneingangszeile, Warenausgangszeile).

Die App bringt **keine eigenen Seiten, keine eigenen Aktionen und keine eigenen
Einrichtungsseiten** mit. Sie ergänzt bestehende Seiten der Basismodule um
zusätzliche Mengenspalten und rechnet im Hintergrund. Die Bedienoberfläche
bleibt daher die gewohnte Oberfläche der Avisierung und Versandplanung; neu sind
die Spalten **KG**, **Meter**, **Stück** und ihre abgeleiteten Werte.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender** in Einkauf, Verkauf und Logistik,
die täglich mit der Avisierung und der Versandplanung arbeiten: Sie erfassen
Belege, weisen Mengen zu und stoßen das **Registrieren** an. Sekundäre Zielgruppe
sind **Administratoren**, die die Voraussetzungen einrichten (siehe
[Einrichtung](#einrichtung)).

### Voraussetzungen

Die App ist eine Erweiterung und setzt voraus, dass die folgenden m+m Apps
installiert und eingerichtet sind:

- m+m Cloud Base
- m+m Unit Conversion (Einheitenumrechnung)
- m+m Logistic Management (Avisierung und Versandplanung)

Ohne diese Basismodule stehen die erweiterten Mengenfelder nicht zur Verfügung.

### Kurzer Prozessüberblick

1. Ein Artikel wird in der **Einheitenumrechnung** mit KG-, Meter- und
   Stück-Werten geführt.
2. Der Anwender erfasst einen Beleg (**Einkaufsbestellung**,
   **Verkaufsauftrag** oder **Umlagerungsauftrag**).
3. Aus dem Beleg entsteht eine **Avisierung** (Zugang) bzw. eine
   **Versandplanung** (Abgang). Die Felder **KG**, **Meter** und **Stück**
   werden mit übernommen; die zusätzlichen Felder werden gefüllt.
4. Der Anwender weist die gewünschte Menge in einer der drei Einheiten zu; die
   App rechnet die anderen beiden Einheiten um.
5. Mit **Registrieren** übernimmt das Basismodul die zugewiesenen Mengen in die
   Folgebelege.

---

## Schnellstart für Anwender

Der Schnellstart beschreibt die kürzesten Wege. Voraussetzung ist immer die
abgeschlossene [Einrichtung](#einrichtung).

### Schnellstart A — Zugang über die Avisierung

1. Öffnen Sie über **Suchen** die **Einkaufsbestellung** und erfassen Sie eine
   Zeile mit einem Artikel, der in KG/Meter/Stück geführt wird.
2. Erstellen Sie über die Aktion **Avisierung erstellen** die **Avisierung**.
   Die Felder **KG**, **Meter** und **Stück** werden aus der Bestellung
   übernommen.
3. Erfassen Sie in der **Avisierung**-Zeile in genau **einer** Einheit die
   Menge — z. B. **KG für Zuweisung**. Die App füllt **Meter für Zuweisung** und
   **Stück für Zuweisung** automatisch.
4. Führen Sie den **Registrieren**-Schritt der Avisierung aus. Die zugewiesenen
   Mengen werden in die Wareneingangs- bzw. Einkaufszeile übernommen.

### Schnellstart B — Abgang über die Versandplanung

1. Öffnen Sie über **Suchen** den **Verkaufsauftrag** und erfassen Sie eine
   Zeile mit einem KG/Meter/Stück-Artikel.
2. Öffnen Sie über **Suchen** die **Versandplanung** und legen Sie aus dem
   Auftrag eine Versandplanungszeile an. Die Felder **KG**, **Meter** und
   **Stück** erscheinen.
3. Erfassen Sie in der **Versandplanung**-Zeile in genau **einer** Einheit die
   Menge — z. B. **Meter für Zuweisung**. Die App füllt **KG für Zuweisung** und
   **Stück für Zuweisung** automatisch und aktualisiert **Bruttogewicht** und
   **Nettogewicht**, sofern der Artikel eine KG-Einheit besitzt.
4. Wählen Sie in der Liste **Versandplanung** die Aktion **Registrieren**. Die
   zugewiesenen Mengen werden in die Warenausgangs-, Verkaufs- bzw.
   Umlagerungszeile übernommen.

> Reihenfolge: Zuerst **Einrichtung**, dann Beleg (Bestellung/Auftrag), dann
> **Avisierung** bzw. **Versandplanung**, dann **Registrieren**.

---

## Einrichtung

Die App selbst besitzt **keine eigene Einrichtungsseite**. Zur Nutzung genügt
es, die Voraussetzungen der Basismodule zu erfüllen und zwei bestehende
Einrichtungsfelder korrekt zu setzen. Diese Einrichtung nimmt der Administrator
einmalig je Mandant vor, bevor die operativen Anwender mit der Avisierung und
Versandplanung arbeiten.

### Einheitenumrechnung für Avisierung und Versandplanung einrichten

**Wer und wann:** Der Administrator richtet dies einmalig je Mandant ein, bevor
die erste Avisierung oder Versandplanung mit KG/Meter/Stück erstellt wird. Die
Einstellungen wirken anschließend in der täglichen Arbeit in
[Avisierung](#tägliche-arbeit-avisierung) und
[Versandplanung](#tägliche-arbeit-versandplanung).

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Basis-Apps installieren.** Stellen Sie sicher, dass m+m Cloud Base, m+m
   Unit Conversion und m+m Logistic Management installiert sind. Wenn diese Apps
   fehlen, dann werden die zusätzlichen KG/Meter/Stück-Felder auf den logistischen
   Belegen nicht angezeigt und es findet keine Umrechnung statt.
2. **Artikelstamm in der Einheitenumrechnung pflegen.** Hinterlegen Sie je
   Artikel die theoretischen Werte für KG pro Meter und KG pro Stück in der
   Einheitenumrechnung. Wenn diese Werte gepflegt sind, dann kann die App aus
   einer eingegebenen Einheit die beiden anderen berechnen; ohne diese Werte
   bleiben die abgeleiteten Mengen leer.
3. **Einheitencode für KG festlegen.** Öffnen Sie über **Suchen** die
   **KG Meter Stück Einrichtung** und tragen Sie den **Einheitencode für KG**
   ein. Wenn ein Einheitencode für KG gesetzt ist, dann verwendet die
   Versandplanung die zugewiesenen KG als **Bruttogewicht** und **Nettogewicht**
   der Versandplanungszeile; ist er leer, unterbleibt diese Gewichtsermittlung.
4. **Standardmenge der Versandplanung festlegen.** Öffnen Sie über **Suchen** die
   **Versandplanung Einrichtung** und setzen Sie den **Standardwert Menge für
   Zuweisung** (siehe Wertetabelle unten). Wenn ein Standardwert gesetzt ist,
   dann schlägt die Versandplanung beim Anlegen einer Zeile automatisch die
   entsprechende KG-, Meter- und Stück-Menge vor.

**Operativer Abschluss:** In der täglichen Arbeit erfasst der Anwender die
zugewiesene Menge auf der Avisierungs- bzw. Versandplanungszeile und stößt
**Registrieren** an; siehe [Tägliche Arbeit — Versandplanung](#tägliche-arbeit-versandplanung).

#### Einrichtungsfelder

| Einrichtung | Erläuterung |
|---|---|
| **Einheitencode für KG** (KG Meter Stück Einrichtung) | Wenn hier ein Einheitencode hinterlegt ist und der Artikel diese KG-Einheit oder theoretische KG-Werte besitzt, dann übernimmt die Versandplanung die zugewiesenen KG als **Bruttogewicht** und **Nettogewicht** der Zeile; ist das Feld leer, werden Gewichte nicht aus den KG abgeleitet. |
| **Standardwert Menge für Zuweisung** (Versandplanung Einrichtung) | Legt fest, welche Menge beim Anlegen einer Versandplanungszeile automatisch als KG/Meter/Stück für Zuweisung vorgeschlagen wird. Siehe Wertetabelle. |

**Werte von „Standardwert Menge für Zuweisung“:**

- **Fertig gestellte Menge:** Beim Anlegen der Versandplanungszeile wird die
  bereits fertig gestellte Menge des zugeordneten Fertigungsauftrags (abzüglich
  bereits verplanter Mengen) als KG/Meter/Stück für Zuweisung vorgeschlagen.
  Geeignet, wenn nur tatsächlich produzierte Mengen versandt werden sollen.
- **Restmenge:** Beim Anlegen der Versandplanungszeile wird die offene Menge des
  Belegs (abzüglich bereits verplanter Mengen) als KG/Meter/Stück für Zuweisung
  vorgeschlagen. Geeignet, wenn die gesamte noch offene Belegmenge verplant
  werden soll.

### Berechtigungen

Die App liefert den Berechtigungssatz **MuM ASUC Permission** mit. Dieser
Berechtigungssatz bestimmt die Berechtigungen für die Ausführung der drei
Berechnungs-Codeunits der App. Er legt fest, dass ein Anwender die automatische
KG/Meter/Stück-Umrechnung in Avisierung, Versandplanung und
Artikelverfolgungszuordnung ausführen darf. Weisen Sie ihn den Anwendern zu, die
mit diesen Belegen arbeiten.

---

## Tägliche Arbeit — Avisierung

Die **Avisierung** wird über **Suchen** aufgerufen oder über die Aktion
**Avisierungen** bzw. **Avisierung erstellen** aus einem Beleg heraus. Wird ein
KG/Meter/Stück-Artikel aus einer **Einkaufsbestellung** in eine Avisierung
überführt, übernimmt die App die Felder **KG**, **Meter** und **Stück** und füllt
die weiteren Felder. Die hier gepflegten Zuweisungsmengen steuern anschließend,
welche Mengen der **Registrieren**-Schritt in Wareneingang bzw. Einkaufszeile
übernimmt (siehe [Einrichtung](#einrichtung)).

### Felder im Avisierungs-Unterformular und in den Avisierungszeilen

Die folgenden Spalten fügt die App den Avisierungszeilen und dem
Unterformular hinzu.

| Feld | Erläuterung |
|---|---|
| **KG** | Zeigt die Gesamt-KG der Zeile aus der Einheitenumrechnung. Wenn der Artikel KG-Werte besitzt, dann dient dieser Wert als Ausgangsbasis für die Umrechnung der Zuweisungsmengen. |
| **Stück** | Zeigt die Gesamtmenge der Zeile in Stück. |
| **Meter** | Zeigt die Gesamtmenge der Zeile in Meter. |
| **KG für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App daraus **Meter für Zuweisung** und **Stück für Zuweisung** sowie die zugewiesene **Menge für Zuweisung** und aktualisiert die Zeile sofort. |
| **Meter für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App daraus **KG für Zuweisung** und **Stück für Zuweisung** und aktualisiert die zugewiesene Menge. |
| **Stück für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App daraus **KG für Zuweisung** und **Meter für Zuweisung** und aktualisiert die zugewiesene Menge. |
| **Rest-KG** | Zeigt die noch nicht avisierten KG. Wenn Zuweisungen erfasst werden, dann verringert sich der Restwert entsprechend. |
| **Reststück** | Zeigt die noch nicht avisierten Stück. |
| **Restmeter** | Zeigt die noch nicht avisierten Meter. |

> Sie müssen die drei Einheiten nicht widerspruchsfrei selbst rechnen: Es genügt,
> **eine** Einheit einzugeben. Eine Teilzuweisung ist zulässig — es ist nicht
> erforderlich, dass alle drei Einheiten vollständig ausgeglichen sind, bevor Sie
> die Zeile verlassen.

### Zusatzfelder auf der Einkaufsbestellung und in den Avisierungs-Einkaufszeilen

Auf dem **Unterformular der Einkaufsbestellung** und in den
Avisierungs-Einkaufszeilen stehen zusätzlich diese Mengenspalten zur Verfügung.

| Feld | Erläuterung |
|---|---|
| **KG für Zuweisung** / **Meter für Zuweisung** / **Stück für Zuweisung** | Wenn Sie eine dieser Größen (bzw. die Menge für Avisierung) auf der Einkaufszeile erfassen, dann berechnet die App die jeweils anderen beiden Einheiten und stellt sie für die Avisierungserstellung bereit. |
| **KG in Avisierung** / **Meter in Avisierung** / **Stück in Avisierung** | Zeigt summiert an, welche KG/Meter/Stück dieser Einkaufszeile bereits in offenen Avisierungen zugewiesen sind. Wenn eine Avisierung angelegt oder geändert wird, dann aktualisiert sich der Wert. |
| **KG in reg. Avisierung** / **Meter in reg. Avisierung** / **Stück in reg. Avisierung** | Zeigt summiert an, welche KG/Meter/Stück dieser Einkaufszeile bereits in **registrierten** Avisierungen verbucht sind. |

---

## Tägliche Arbeit — Versandplanung

Die **Versandplanung** wird über **Suchen** aufgerufen oder über die Aktion
**Versandplanung** aus einem Beleg heraus. Wird ein KG/Meter/Stück-Artikel aus
einem **Verkaufsauftrag** oder **Umlagerungsauftrag** in die Versandplanung
überführt, erscheinen die Felder **KG**, **Meter** und **Stück** auch in der
Versandplanung. Welche Menge beim Anlegen vorgeschlagen wird, steuert der
**Standardwert Menge für Zuweisung** aus der [Einrichtung](#einrichtung).

### Felder im Versandplanungs-Unterformular und in den Versandplanungszeilen

| Feld | Erläuterung |
|---|---|
| **KG für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App **Meter für Zuweisung** und **Stück für Zuweisung**, aktualisiert die **Menge für Zuweisung** und leitet bei gesetztem Einheitencode für KG **Bruttogewicht** und **Nettogewicht** ab. |
| **Meter für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App **KG für Zuweisung** und **Stück für Zuweisung** und aktualisiert die zugewiesene Menge. |
| **Stück für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App **KG für Zuweisung** und **Meter für Zuweisung** und aktualisiert die zugewiesene Menge. |

### Versandplanungszuordnung mit Bestand

In der Versandplanungszuordnung mit Bestand zeigt die App zusätzlich die
Ausgangs- und Planungsmengen je Einheit an. Diese Spalten dienen der Übersicht,
welche Mengen offen, fertig gestellt und für die Versandplanung vorgesehen sind.

| Feld | Erläuterung |
|---|---|
| **KG** / **Meter** / **Stück** | Zeigt die Gesamtmenge der Belegzeile in der jeweiligen Einheit. |
| **Rest-KG** / **Restmeter** / **Reststück** | Zeigt die offene, noch nicht versandte Menge je Einheit. |
| **Fertig gestellte KG** / **Fertig gestellte Meter** / **Fertig gestellte Stück** | Zeigt die aus zugeordneten Fertigungsaufträgen fertig gestellte Menge je Einheit. Wenn der Standardwert „Fertig gestellte Menge“ eingestellt ist, dann bildet dieser Wert die Grundlage für den Zuweisungsvorschlag. |
| **KG für Versandplanung** / **Meter für Versandplanung** / **Stück für Versandplanung** | Zeigt die für die Versandplanung vorgeschlagene Menge je Einheit (Standardwert abzüglich bereits verplanter Mengen). Wenn Sie diese Zuordnung übernehmen, dann werden die Werte als Zuweisungsmengen in die Versandplanungszeile geschrieben. |

### Umlagerung und Folgebelege

Die Versandplanung deckt neben dem Verkauf auch die **Umlagerung** ab. Beim
Anlegen einer Versandplanungszeile aus einer Umlagerungszeile schlägt die App die
offenen KG/Meter/Stück als Zuweisungsmengen vor. Nach dem **Registrieren**
überträgt die App die zugewiesenen Einheiten in die Folgebelege:

- **Verkauf:** in die Verkaufszeile bzw. in die **Warenausgang**-Zeile.
- **Umlagerung:** in die **Umlagerungsauftrag**-Zeile bzw. in die
  **Warenausgang**-Zeile.
- **Zugang (Avisierung):** in die Einkaufszeile bzw. in die **Wareneingang**-Zeile.

### Registrieren

Der Abschluss der Versandplanung erfolgt über die Aktion **Registrieren** in der
Liste **Versandplanung**. Diese Aktion gehört zum Basismodul; die App sorgt
dafür, dass die zugewiesenen KG/Meter/Stück-Mengen vollständig in die
Folgebelege übernommen werden. Nach dem Registrieren stehen die Mengen in der
**Registrierten Versandplanung** zur Nachverfolgung bereit.

---

## Artikelverfolgungszuordnung

Wenn ein Artikel mit **Chargennr.** oder **Seriennr.** geführt wird, ordnet der
Anwender die Verfolgung in der **Artikelverfolgungszuordnung** zu. Auch hier
ergänzt die App die drei Einheiten, sodass die Zuweisung nicht nur in der
Basismenge, sondern auch in KG, Meter und Stück erfolgen kann.

| Feld | Erläuterung |
|---|---|
| **KG für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App **Meter für Zuweisung** und **Stück für Zuweisung** und aktualisiert die **Menge für Zuweisung** der Zuordnungszeile. |
| **Meter für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App **KG für Zuweisung** und **Stück für Zuweisung**. |
| **Stück für Zuweisung** | Wenn Sie hier einen Wert erfassen, dann berechnet die App **KG für Zuweisung** und **Meter für Zuweisung**. |

Bei der Auswahl mehrerer Chargen bzw. Seriennummern summiert die App die
ausgewählten Mengen. In der Auswahlübersicht stehen dafür zusätzlich zur
Verfügung:

| Feld | Erläuterung |
|---|---|
| **Ausgewählte KG für Zuweisung** / **Ausgewählte Meter für Zuweisung** / **Ausgewähltes Stück für Zuweisung** | Wenn Sie in der Auswahlzeile eine dieser Größen erfassen, dann rechnet die App die beiden anderen um und bildet die Basismenge. |
| **Gesamt-KG für Zuweisung** / **Gesamt-Meter für Zuweisung** / **Gesamt-Stück für Zuweisung** | Zeigt die Summe der ausgewählten Mengen je Einheit über alle ausgewählten Chargen bzw. Seriennummern. |

Die in der Artikelverfolgungszuordnung zugewiesenen KG/Meter/Stück werden an die
zugehörige Avisierungs- bzw. Versandplanungszeile zurückgeschrieben, damit die
Mengen über den gesamten Prozess konsistent bleiben.

---

## Historie, Archiv und Nachverfolgung

Nach dem **Registrieren** sind die Mengen in den registrierten Belegen und im
Archiv nachvollziehbar. Die App zeigt dort dieselben Zuweisungsspalten wie in den
aktiven Listen.

| Bereich | Erläuterung |
|---|---|
| **Registrierte Avisierung** | Zeigt in den Zeilen **KG für Zuweisung**, **Meter für Zuweisung** und **Stück für Zuweisung** der registrierten Avisierung. Dient der Nachverfolgung, welche Mengen je Einheit tatsächlich avisiert wurden. |
| **Registrierte Versandplanung** | Zeigt in den Zeilen und im Unterformular **KG für Zuweisung**, **Meter für Zuweisung** und **Stück für Zuweisung** der registrierten Versandplanung. |
| **Avisierung — Archiv** | Zeigt im archivierten Unterformular **KG**, **Meter**, **Stück** sowie die zugewiesenen Mengen der archivierten Avisierungsversion. |
| **Registrierte Artikelverfolgungszuordnung** | Zeigt **KG für Zuweisung**, **Meter für Zuweisung** und **Stück für Zuweisung** der registrierten Zuordnung. |

---

## FAQ und Troubleshooting

### 1. Warum erscheinen in der Avisierung keine KG/Meter/Stück-Felder?

Die Felder werden nur gefüllt, wenn der Artikel in der **Einheitenumrechnung**
mit KG-, Meter- oder Stück-Werten geführt wird und die Basismodule installiert
sind. Prüfen Sie die theoretischen KG-Werte des Artikels und die
[Einrichtung](#einrichtung).

### 2. Muss ich alle drei Einheiten selbst eintragen?

Nein. Es genügt, **eine** Einheit (KG, Meter oder Stück) für Zuweisung
einzugeben. Die App berechnet die beiden anderen Einheiten und die Menge für
Zuweisung automatisch.

### 3. Was passiert, wenn ich „KG für Zuweisung“ ändere?

Die App rechnet aus dem neuen KG-Wert die zugehörigen **Meter für Zuweisung**
und **Stück für Zuweisung** neu, aktualisiert die **Menge für Zuweisung** und
aktualisiert die Zeilenanzeige sofort.

### 4. Warum weicht die berechnete Menge geringfügig ab?

Die Umrechnung basiert auf den KG pro Meter bzw. KG pro Stück des Artikels.
Liegt ein **tatsächlicher** KG-Wert (z. B. je Charge) vor, verwendet die App
diesen; andernfalls den **theoretischen** Wert. Unterschiedliche Bezugswerte
führen zu unterschiedlichen Ergebnissen.

### 5. Wie wird das Gewicht der Versandplanung ermittelt?

Ist in der **KG Meter Stück Einrichtung** ein **Einheitencode für KG**
hinterlegt und besitzt der Artikel KG-Werte, setzt die App **Bruttogewicht** und
**Nettogewicht** der Versandplanungszeile gleich den zugewiesenen KG. Ohne
Einheitencode für KG unterbleibt diese Ableitung.

### 6. Welche Menge schlägt die Versandplanung beim Anlegen vor?

Das steuert der **Standardwert Menge für Zuweisung** in der **Versandplanung
Einrichtung**: **Fertig gestellte Menge** schlägt die fertig gestellte Menge
vor, **Restmenge** die offene Belegmenge — jeweils abzüglich bereits verplanter
Mengen.

### 7. Warum ist die vorgeschlagene Menge kleiner als erwartet?

Von der fertig gestellten bzw. offenen Menge zieht die App die bereits in
anderen, noch nicht abgeschlossenen Versandplanungszeilen verplanten Mengen ab,
damit keine Menge doppelt verplant wird.

### 8. Kann ich Teilmengen zuweisen?

Ja. Sie können in der Avisierung und der Versandplanung Teilmengen zuweisen; es
ist nicht erforderlich, dass alle Einheiten vollständig ausgeglichen sind, bevor
Sie die Zeile verlassen oder **Registrieren** ausführen.

### 9. Wie ordne ich Mengen einer Charge oder Seriennummer zu?

Nutzen Sie die **Artikelverfolgungszuordnung**. Dort erfassen Sie je **Chargennr.**
bzw. **Seriennr.** die KG/Meter/Stück für Zuweisung; die App summiert die
Auswahl und schreibt die Mengen an die Avisierungs- bzw. Versandplanungszeile
zurück.

### 10. Wo sehe ich, welche Mengen bereits registriert wurden?

Auf der Einkaufs- bzw. Verkaufszeile zeigen die Felder **KG/Meter/Stück in
Avisierung** die offen zugewiesenen und **KG/Meter/Stück in reg. Avisierung** die
bereits registrierten Mengen. Die registrierten Belege selbst führen dieselben
Zuweisungsspalten (siehe [Historie](#historie-archiv-und-nachverfolgung)).

---

## Typische Anwendungsfälle

### Nutzungsbeispiel 1 — Wareneingang eines Coils (Avisierung)

**Auslöser:** Ein Lieferant kündigt telefonisch die Anlieferung von Coils an,
die in **KG**, **Meter** und **Stück** geführt werden.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** die **Einkaufsbestellung**
und erstellt über **Avisierung erstellen** die **Avisierung**.

**Kernablauf:** In der **Avisierung**-Zeile trägt der Anwender die avisierte
Menge in **KG für Zuweisung** ein. Die App berechnet **Meter für Zuweisung** und
**Stück für Zuweisung** und aktualisiert die Zeile. Anschließend stößt der
Anwender den **Registrieren**-Schritt an.

**Abschluss:** Die zugewiesenen Mengen werden in die Wareneingangs- bzw.
Einkaufszeile übernommen; die registrierte Avisierung zeigt die verbuchten
KG/Meter/Stück.

### Nutzungsbeispiel 2 — Kundenabruf (Versandplanung)

**Auslöser:** Ein Kunde ruft eine Teilmenge zu einem Liefertermin ab.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** den **Verkaufsauftrag**
und danach über **Suchen** die **Versandplanung**.

**Kernablauf:**

1. Der Anwender legt aus dem Auftrag eine **Versandplanung**-Zeile an; je nach
   **Standardwert Menge für Zuweisung** wird eine Menge vorgeschlagen.
2. Der Anwender überschreibt bei Bedarf **Meter für Zuweisung**; die App
   berechnet **KG für Zuweisung** und **Stück für Zuweisung** und aktualisiert
   **Bruttogewicht**/**Nettogewicht**.
3. Der Anwender wählt in der Liste **Versandplanung** die Aktion **Registrieren**.

**Abschluss:** Die Mengen werden in die Verkaufs- bzw. **Warenausgang**-Zeile
übernommen; die **Registrierte Versandplanung** dokumentiert den Vorgang.

### Nutzungsbeispiel 3 — Umlagerung zwischen Lagerorten

**Auslöser:** Für einen internen Bestandsausgleich soll Material zwischen zwei
Lagerorten umgelagert werden.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** den
**Umlagerungsauftrag** und danach über **Suchen** die **Versandplanung**.

**Kernablauf:** Beim Anlegen der Versandplanungszeile aus der Umlagerungszeile
schlägt die App die offenen **KG/Meter/Stück für Zuweisung** vor. Der Anwender
passt eine Einheit an; die App rechnet die übrigen um. Danach wählt der Anwender
**Registrieren**.

**Abschluss:** Die zugewiesenen Mengen werden in die **Umlagerungsauftrag**- bzw.
**Warenausgang**-Zeile übernommen und stehen in der **Registrierten
Versandplanung** zur Nachverfolgung bereit.
