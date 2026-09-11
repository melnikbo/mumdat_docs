---
title: Anwenderhandbuch m+m Logistic Management with Additional Lot Information
---

# Anwenderhandbuch m+m Logistic Management with Additional Lot Information

## Einleitung

Die Erweiterung **m+m Logistic Management with Additional Lot Information** verbindet die zusätzlichen Chargeninformationen mit der Artikelverfolgung der Logistikbelege. Sie ergänzt die **Artikelverfolgungszeilen** um Zusatzangaben zur Charge (Lieferantenchargennr., Herkunft, Hersteller, Ursprungscharge) und stellt eine Aktion bereit, mit der aus einer offenen Zuweisungsmenge **mehrere Chargen auf einmal** erzeugt werden.

**Zielgruppe:** Primär **operative Anwender im Einkauf und in der Lagerlogistik**, die beim Wareneingang lot- bzw. chargenpflichtige Artikel erfassen und die Artikelverfolgung eines Einkaufsbelegs pflegen. Die Erweiterung hat **keine eigene Einrichtungsseite und keine eigenen Stammdaten**; nach der Installation stehen die Zusatzfelder und die Aktion unmittelbar in den Artikelverfolgungszeilen zur Verfügung. Eine gesonderte Konfiguration ist nicht erforderlich.

**Kurzer Prozessüberblick:** Der Anwender öffnet zu einer Einkaufsbelegzeile die **Artikelverfolgungszeilen**, erfasst eine oder – über die Aktion **Mehrere Artikelverfolgungen erstellen** – mehrere Chargen, ergänzt die chargenbezogenen Zusatzangaben und bucht anschließend den Beleg. Beim Buchen werden die erfassten Werte an die **Chargeninformationskarte** und die Reservierungsposten übergeben, sodass die Zusatzinformationen dauerhaft an der Charge hängen.

## Schnellstart für Anwender

Der schnellste Weg von der Belegzeile bis zur gebuchten Charge:

1. Öffnen Sie den **Einkaufsbeleg** (z. B. eine **Einkaufsbestellung**) mit einer Zeile für einen chargenpflichtigen Artikel.
2. Markieren Sie die Artikelzeile und öffnen Sie über **Zeile** die **Artikelverfolgungszeilen**.
3. Erfassen Sie die Charge:
   - **Einzelne Charge:** Tragen Sie in **Chargennr.** die Chargennummer ein und füllen Sie die Zusatzspalten (siehe unten).
   - **Mehrere Chargen automatisch:** Wählen Sie die Aktion **Mehrere Artikelverfolgungen erstellen**. Geben Sie im Dialog **Artikelverfolgung erstellen – Chargennr.** unter **Chargenanzahl** die gewünschte Anzahl an und füllen Sie die gemeinsamen Zusatzangaben. Bestätigen Sie mit **OK**.
4. Prüfen Sie, dass die Summe der zugewiesenen Mengen (**Menge für Zuweisung**) der zu verfolgenden Belegmenge entspricht.
5. **Buchen** Sie den Einkaufsbeleg (empfangen/liefern). Die Zusatzangaben werden dabei an die **Chargeninformationskarte** übergeben.

> Die Aktion **Mehrere Artikelverfolgungen erstellen** steht bei der **Artikelverfolgung im Einkauf** zur Verfügung. In Verkaufsbelegen wird sie nicht angeboten; dort sind die Zusatzspalten dennoch sichtbar und lesbar.

## Tägliche Arbeit: Artikelverfolgungszeilen mit Zusatzangaben

Diese Erweiterung wirkt ausschließlich in den **Artikelverfolgungszeilen** eines Belegs. Sie erweitert die vorhandene Artikelverfolgungszuordnung um chargenbezogene Zusatzspalten und um eine Aktion zum Anlegen mehrerer Chargen. Die Basis-Spalten der Artikelverfolgung (u. a. **Chargennr.**, **Menge für Zuweisung**, **Einheitencode**, **Artikelnr.**, **Variantencode**) bleiben unverändert bestehen; die folgenden Abschnitte beschreiben die von dieser App **zusätzlich** eingeblendeten Felder und Aktionen.

### Zusätzliche Spalten in den Artikelverfolgungszeilen

Die App blendet in der Zeilentabelle die folgenden Zusatzspalten ein. Ist einer Zeile eine **Chargennr.** zugewiesen, für die bereits eine **Chargeninformationskarte** existiert, werden diese Felder beim Bestätigen der Chargennr. **automatisch** aus der Karte gefüllt; wird die Chargennr. wieder geleert, werden sie automatisch zurückgesetzt.

| Feld | Erläuterung |
|------|-------------|
| **Lieferantenchargennr.** | Wenn gesetzt, wird die vom Lieferanten vergebene Chargennummer an der Zuordnungszeile geführt und beim Buchen an die Chargeninformationskarte übergeben; so bleibt die Rückverfolgung zur Lieferantencharge erhalten. Beim Buchen des Belegs wird zu dieser Nummer bei Bedarf eine Lieferantenchargen-Information angelegt. |
| **Lieferanten interne Chargennr.** | Wenn gesetzt, wird zusätzlich die interne Chargennummer des Lieferanten mitgeführt; dies ermöglicht den Abgleich mit Lieferpapieren, die eine hausinterne Chargenkennung des Lieferanten tragen. |
| **Bund** | Wenn aktiviert, wird die Charge als Bund gekennzeichnet (z. B. Stahlbund); die Kennzeichnung wird an die Chargeninformationskarte übergeben und steht dort für Auswertung und Weiterverarbeitung zur Verfügung. Ist die Option nicht gesetzt, gilt die Charge als Einzelmenge ohne Bundkennzeichen. |
| **Ursprungsland/-regionscode** | Wenn gesetzt, wird das Ursprungsland bzw. die Ursprungsregion der Charge festgehalten und beim Buchen an die Charge weitergegeben; dies unterstützt Herkunftsnachweise und länderbezogene Auswertungen. |
| **Eingekauft von Kreditor-Nr.** | Wird beim Anlegen mehrerer Chargen automatisch aus der Einkaufszeile (Kreditor der Bestellung) übernommen und ist nicht manuell editierbar. Dadurch ist jederzeit erkennbar, von welchem Lieferanten die Charge bezogen wurde. |
| **Herstellercode** | Wenn gesetzt, wird der Hersteller der Charge festgehalten und an die Chargeninformationskarte übergeben; dort steht ergänzend der zugehörige **Herstellername** zur Verfügung. So lässt sich die Charge dem Produzenten zuordnen. |
| **Ursprüngliche Artikel-Nr.** | Wird gefüllt, wenn die Charge aus einer Produktion mit einem Ursprungsartikel verknüpft wurde; zeigt die Artikelnummer der Ursprungscharge an. Das Feld ist nicht editierbar und dient der Rückverfolgung auf den eingesetzten Ursprungsartikel. |
| **Ursprünglicher Variantencode** | Wenn eine Ursprungscharge mit Variante verknüpft ist, wird hier die Variante des Ursprungsartikels angezeigt. Nicht editierbar. |
| **Ursprüngliche Chargennr.** | Wenn die Charge über einen Ursprungsartikel mit einer weiteren Charge verknüpft ist, wird hier die ursprüngliche Chargennummer angezeigt; damit ist die Herkunftscharge aus der Produktion nachvollziehbar. Nicht editierbar. |

Der ältere Wert **Herstellercode** aus einer früheren Version wird bei einem Upgrade automatisch in das oben genannte Feld **Herstellercode** übernommen; ein zusätzliches, technisch veraltetes Herstellercode-Feld ist ausgeblendet und für den Anwender ohne Bedeutung.

### Aktion: Mehrere Artikelverfolgungen erstellen

Muss eine zu verfolgende Menge auf mehrere Chargen aufgeteilt werden (typisch beim Wareneingang einer Lieferung, die in mehreren Bunden bzw. Chargen ankommt), erspart diese Aktion das manuelle Anlegen jeder einzelnen Zeile.

**Ablauf:**

1. Öffnen Sie die **Artikelverfolgungszeilen** zur Einkaufsbelegzeile.
2. Wählen Sie die Aktion **Mehrere Artikelverfolgungen erstellen** (auch über die Tastenkombination Alt+C erreichbar).
3. Der Dialog **Artikelverfolgung erstellen – Chargennr.** öffnet sich. Erfassen Sie die folgenden Angaben:

| Feld | Erläuterung |
|------|-------------|
| **Chargenanzahl** | Geben Sie an, wie viele Chargen erzeugt werden sollen. Wenn Sie einen Wert eintragen, wird die noch offene Zuweisungsmenge (**Menge für Zuweisung** abzüglich der bereits zugewiesenen Menge) gleichmäßig auf diese Anzahl aufgeteilt; die Aufteilung wird auf die Rundungspräzision des Artikels gerundet, ein verbleibender Rest wird der letzten Charge zugeschlagen. Die Aktion kann bei Bedarf mehrfach ausgeführt werden. |
| **Bund** | Wenn aktiviert, werden alle erzeugten Chargen als Bund gekennzeichnet (z. B. Stahl); der Wert wird auf jede neue Zeile übertragen. |
| **Ursprungsland/-regionscode** | Wenn gesetzt, erhalten alle erzeugten Chargen dieses Ursprungsland; die Angabe wird an jede neue Zeile übergeben. |
| **Lieferantenchargennr.** | Wenn gesetzt, wird die Lieferantenchargennummer auf die erzeugten Zeilen übertragen. |
| **Lieferanten interne Chargennr.** | Wenn gesetzt, wird die interne Chargennummer des Lieferanten auf die erzeugten Zeilen übertragen. |
| **Herstellercode** | Wenn gesetzt, wird der Herstellercode auf die erzeugten Zeilen übertragen. |

4. Bestätigen Sie mit **OK**. Das System erzeugt so viele Artikelverfolgungszeilen wie unter **Chargenanzahl** angegeben, vergibt je Zeile automatisch eine neue **Chargennr.** aus der am Artikel hinterlegten Nummernserie, verteilt die offene Menge auf die Zeilen und überträgt die im Dialog erfassten Zusatzangaben auf jede Zeile.

> **Hinweis:** Ist die noch offene Zuweisungsmenge null, ist keine Aufteilung möglich und es erscheint der Hinweis *„Die Menge ist 0. Aufteilung nicht möglich.“* – erfassen Sie zunächst die zu verfolgende Menge in der Belegzeile. Voraussetzung für die automatische Chargennummernvergabe ist, dass am Artikel eine Chargennummernserie hinterlegt ist; fehlt sie, weist das System darauf hin.

### Wie die Zusatzangaben mit der Charge verbunden werden

Die erfassten Werte sind nicht nur an der Belegzeile sichtbar, sondern werden dauerhaft mit der Charge verknüpft:

- Beim **Buchen** des Belegs werden die Angaben der Artikelverfolgungszeile (Lieferantenchargennr., interne Chargennr., Ursprungsland, Bund, Herstellercode, Ursprungsartikel/-charge) auf die **Chargeninformationskarte** übertragen; die Karte wird bei Bedarf angelegt.
- Wird eine bestehende **Chargeninformationskarte** nachträglich geändert, werden die zugehörigen, noch offenen Artikelverfolgungszeilen automatisch mit den neuen Werten abgeglichen. So bleiben Belegzeile und Chargenstammdaten konsistent.
- Wählen Sie in einer Zeile eine bereits bekannte **Chargennr.**, werden die Zusatzfelder aus der vorhandenen Chargeninformationskarte automatisch vorbelegt. Leeren Sie die Chargennr., werden die Zusatzfelder wieder geleert.

## Berechtigungen

Die Erweiterung liefert die zuweisbare Berechtigung **MuM ASAI Permission** mit. Sie legt fest, welche Aktionen die internen Funktionen dieser App (u. a. die Verwaltung der Artikelverfolgungs-Zusatzangaben sowie die Installations- und Upgrade-Routinen) ausführen dürfen. Weisen Sie diese Berechtigung den Benutzern zu, die mit Einkaufsbelegen und Artikelverfolgung arbeiten. Die eigentliche Sichtbarkeit der Belege und Artikelverfolgungszeilen wird darüber hinaus durch die Standard-Berechtigungen von Business Central und der Logistikmodule bestimmt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Wareneingang einer Lieferung mit mehreren Chargen

**Auslöser:** Der Einkauf erhält eine Lieferung eines chargenpflichtigen Artikels, die in mehreren Bunden bzw. Chargen ankommt; der Lieferschein weist mehrere Chargennummern aus.

**Einstieg in BC:** Der Anwender öffnet die zugehörige **Einkaufsbestellung**, markiert die Artikelzeile und ruft über **Zeile** die **Artikelverfolgungszeilen** auf.

**Kernablauf:**
1. Aktion **Mehrere Artikelverfolgungen erstellen** wählen.
2. Im Dialog **Artikelverfolgung erstellen – Chargennr.** die **Chargenanzahl** (z. B. Anzahl der gelieferten Bunde) eintragen, **Bund** aktivieren und die gemeinsamen Angaben (**Ursprungsland/-regionscode**, **Lieferantenchargennr.**, **Herstellercode**) füllen.
3. Mit **OK** bestätigen. BC legt die entsprechende Anzahl Zeilen an, vergibt je Zeile eine neue **Chargennr.** und teilt die Menge auf.
4. Bei Bedarf einzelne Mengen (**Menge für Zuweisung**) je Zeile nachjustieren, bis die Summe der Belegmenge entspricht.

**Abschluss:** Der Anwender bucht den Wareneingang (empfangen). Für jede Charge wird die **Chargeninformationskarte** mit den erfassten Zusatzangaben erzeugt.

### Anwendungsfall 2: Einzelne Charge mit Lieferanten- und Herstellerdaten erfassen

**Auslöser:** Zu einer gelieferten Charge liegt ein Werkszeugnis vor; die Lieferanten- und Herstellerangaben sollen revisionssicher an der Charge dokumentiert werden.

**Einstieg in BC:** Aus der Einkaufsbelegzeile über **Zeile → Artikelverfolgungszeilen**.

**Kernablauf:**
1. In der Zeile die **Chargennr.** eintragen. Ist die Charge bereits als Chargeninformationskarte bekannt, werden die Zusatzfelder automatisch vorbelegt.
2. Andernfalls **Lieferantenchargennr.**, **Lieferanten interne Chargennr.**, **Ursprungsland/-regionscode** und **Herstellercode** manuell erfassen. Die **Eingekauft von Kreditor-Nr.** wird automatisch aus dem Beleg abgeleitet.
3. **Menge für Zuweisung** so setzen, dass die Artikelverfolgung ausgeglichen ist.

**Abschluss:** Beim Buchen des Belegs werden die Angaben auf die **Chargeninformationskarte** übertragen und sind später für Rückverfolgung und Auswertung verfügbar.

## FAQ und Troubleshooting

### 1. Warum sehe ich die Aktion „Mehrere Artikelverfolgungen erstellen“ im Verkaufsbeleg nicht?
Die Aktion ist auf die **Artikelverfolgung im Einkauf** ausgelegt und wird dort in den Artikelverfolgungszeilen angeboten. In Verkaufsbelegen wird sie nicht bereitgestellt; die chargenbezogenen Zusatzspalten sind dort aber weiterhin sichtbar.

### 2. Warum erscheint die Meldung „Die Menge ist 0. Aufteilung nicht möglich.“?
Die Aktion teilt die **noch offene** Zuweisungsmenge auf. Ist diese null (keine oder bereits vollständig zugewiesene Menge), gibt es nichts zu verteilen. Erfassen Sie zuerst die zu verfolgende Menge in der Belegzeile und starten Sie die Aktion erneut.

### 3. Woher stammen die automatisch vergebenen Chargennummern?
Beim Anlegen mehrerer Chargen zieht das System je Zeile die nächste Nummer aus der **Chargennummernserie**, die am Artikel hinterlegt ist. Ist am Artikel keine Chargennummernserie eingerichtet, kann die Aktion keine Nummern vergeben und weist darauf hin.

### 4. Wie wird die Menge auf die einzelnen Chargen verteilt?
Die offene Menge wird gleichmäßig durch die **Chargenanzahl** geteilt und auf die Rundungspräzision des Artikels gerundet. Ein durch die Rundung verbleibender Rest wird der **letzten** erzeugten Charge zugeschlagen, damit die Summe exakt der Belegmenge entspricht.

### 5. Warum sind einige Zusatzfelder (z. B. „Ursprüngliche Chargennr.“) nicht editierbar?
Die Ursprungsfelder (**Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode**, **Ursprüngliche Chargennr.**) sowie **Eingekauft von Kreditor-Nr.** werden vom System aus der Chargeninformationskarte bzw. aus dem Beleg abgeleitet und dienen der Rückverfolgung. Sie werden daher nicht manuell erfasst.

### 6. Warum werden meine Zusatzfelder gefüllt, sobald ich eine Chargennr. eingebe?
Wenn zu der eingegebenen **Chargennr.** bereits eine **Chargeninformationskarte** existiert, übernimmt das System deren Werte automatisch in die Zeile. So müssen bekannte Chargen nicht erneut erfasst werden.

### 7. Was passiert mit den Zusatzfeldern, wenn ich die Chargennr. wieder lösche?
Wird die **Chargennr.** aus einer Zeile entfernt, werden alle chargenbezogenen Zusatzfelder (Lieferantenangaben, Ursprung, Bund, Herstellercode, Ursprungsartikel/-charge) automatisch geleert, damit keine unpassenden Werte an einer leeren Zeile verbleiben.

### 8. Ich habe eine Chargeninformationskarte nachträglich geändert – muss ich die Belegzeilen anpassen?
Nein. Änderungen an einer **Chargeninformationskarte** werden automatisch auf die zugehörigen Artikelverfolgungszeilen übertragen, sodass Beleg und Chargenstammdaten konsistent bleiben.

### 9. Wozu dient das Kennzeichen „Bund“?
**Bund** markiert eine Charge als Bund (z. B. Stahlbund). Ist es aktiviert, wird die Kennzeichnung an die Charge übergeben und steht für nachgelagerte Auswertung und Weiterverarbeitung zur Verfügung; ohne Kennzeichen gilt die Charge als Einzelmenge.

### 10. Muss ich für diese Erweiterung etwas einrichten?
Nein. Die App benötigt keine eigene Einrichtungsseite und keine Stammdaten. Nach der Installation stehen die Zusatzspalten und die Aktion **Mehrere Artikelverfolgungen erstellen** in den Artikelverfolgungszeilen automatisch bereit. Voraussetzung für die automatische Chargennummernvergabe ist lediglich eine am Artikel hinterlegte Chargennummernserie.
