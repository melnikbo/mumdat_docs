---
title: Anwenderhandbuch m+m Unit Conversion with Additional Lot Information
---

# Anwenderhandbuch m+m Unit Conversion with Additional Lot Information

## Einleitung

Die App **m+m Unit Conversion with Additional Lot Information** verbindet die beiden Module
**m+m Unit Conversion** und **m+m Additional Lot Information**. Sie sorgt dafür, dass bei der
**Phys. Bestandsaufnahme** die zusätzlichen Chargeninformationen einer bestehenden Charge automatisch auf eine neu
erzeugte Charge übertragen werden. Dadurch bleiben Herkunfts- und Zusatzangaben (z. B. Ursprungscharge, Hersteller,
Zugangsdatum) erhalten, wenn während der Bestandsaufnahme aus mengentechnischen Gründen eine neue Charge angelegt
wird.

Die App fügt selbst keine eigenen Seiten hinzu. Ihr Nutzen entsteht an zwei Stellen, die von den abhängigen Modulen
bereitgestellt werden:

- In der **Chargeninformationsübertragungseinrichtung** steht der neue **Prozess** **Phys. Bestandsaufnahme** zur
  Auswahl. Dort legt der Administrator fest, **welche** Felder bei diesem Prozess von der alten auf die neue Charge
  übertragen werden.
- In der **Phys. Bestandsaufnahme** übertragt die App bei der Aktion **Stornieren und neue Charge erstellen** die
  eingerichteten Felder sowie die Herkunftsangaben (**Ursprüngliche Artikel-Nr.**, **Ursprünglicher
  Variantencode**, **Ursprüngliche Chargennr.**) auf die neue **Chargennr.-Informationskarte**.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender im Lager**, die die
**Phys. Bestandsaufnahme** durchführen und dabei Chargen erfassen, stornieren und neu anlegen. Sekundär angesprochen
sind **Administratoren und Key-User**, die die **Chargeninformationsübertragungseinrichtung** einmalig vor der
ersten Nutzung konfigurieren.

**Voraussetzungen.** Für die Nutzung im Webclient „Microsoft Dynamics 365 Business Central" ist keine separate
Einrichtung dieser App erforderlich. In der Erweiterungsverwaltung müssen die App
**m+m Unit Conversion with Additional Lot Information** sowie ihre Basismodule **m+m Unit Conversion** und
**m+m Additional Lot Information** installiert sein. Damit neue Chargen automatisch eine **Chargennr.** erhalten
können, muss dem Artikel eine **Nummernserie** für Chargen zugeordnet sein.

**Prozessüberblick.** Der Ablauf besteht aus drei Schritten: Der Administrator richtet in der
**Chargeninformationsübertragungseinrichtung** den Prozess **Phys. Bestandsaufnahme** ein. Der Anwender führt die
**Phys. Bestandsaufnahme** durch und löst bei Bedarf die Aktion **Stornieren und neue Charge erstellen** aus.
Anschließend prüft der Anwender das Ergebnis auf der **Chargennr.-Informationskarte** der neuen Charge.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zum Ergebnis. Die Einrichtung ist Voraussetzung und steht daher am
Anfang.

1. **Einrichtung (einmalig, Administrator).** Öffnen Sie über **Suchen** die
   **Chargeninformationsübertragungseinrichtung**. Legen Sie eine oder mehrere Zeilen an, wählen Sie im Feld
   **Prozess** den Wert **Phys. Bestandsaufnahme** und wählen Sie im Feld **Feldnummer** die Chargenfelder aus, die
   übertragen werden sollen (z. B. eine Beschreibung oder eine Zertifikatsangabe). Details siehe
   **Einrichtung**.
2. **Phys. Bestandsaufnahme öffnen.** Öffnen Sie über **Suchen** die **Phys. Bestandsaufnahme** und wählen Sie die
   Erfassungszeile der betroffenen Charge.
3. **Neue Charge erzeugen.** Wählen Sie im Menüband unter **Funktionen** die Aktion **Stornieren und neue Charge
   erstellen**. Business Central erzeugt aus der **Nummernserie** des Artikels eine neue **Chargennr.**, überträgt
   die eingerichteten Felder von der alten auf die neue Charge und setzt zusätzlich die Herkunftsfelder
   (**Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode**, **Ursprüngliche Chargennr.**).
4. **Ergebnis prüfen.** Die neue Erfassungszeile enthält die neue **Chargennr.** und im Feld **Kopiert von
   Chargennr.** die Ausgangscharge; die alte Zeile ist als **Storniert** gekennzeichnet. Öffnen Sie die
   **Chargennr.-Informationskarte** der neuen Charge und prüfen Sie die übertragenen Felder und Herkunftsangaben.
5. **Korrektur (optional).** Wurde die neue Charge irrtümlich erzeugt, wählen Sie **Funktionen → Stornierung
   rückgängig machen**. Die neue Charge wird entfernt und die ursprüngliche Zeile wieder aktiviert.

## Einrichtung

Die zentrale und einzige Einrichtung dieser App erfolgt in der **Chargeninformationsübertragungseinrichtung**.
Diese Seite gehört zum Basismodul **m+m Additional Lot Information**; die vorliegende App ergänzt dort den Prozess
**Phys. Bestandsaufnahme**. Der Administrator legt hier fest, welche Chargenfelder bei einem Prozess von einer
bestehenden Charge auf eine neu erzeugte Charge übertragen werden.

### Feldübertragung für die Phys. Bestandsaufnahme einrichten

**Wer und wann.** Diese Einrichtung nimmt der **Administrator** oder ein **Key-User** einmalig vor der ersten
Nutzung vor. Sie steuert, welche Angaben bei der täglichen Arbeit in der **Phys. Bestandsaufnahme** automatisch
mitgeführt werden (siehe **Tägliche Arbeit an der Phys. Bestandsaufnahme**).

**Einstieg:** Öffnen Sie über **Suchen** die **Chargeninformationsübertragungseinrichtung**. Die Seite ist eine
Listenseite und wird nicht über eine übergeordnete Karte oder Liste geöffnet.

Die Seite enthält je Zeile die folgenden Felder:

| Feld | Erläuterung |
|---|---|
| **Prozess** | Legt fest, für welchen Geschäftsvorfall die Feldübertragung gilt. Wenn Sie **Phys. Bestandsaufnahme** wählen, greift die Zeile bei der Aktion **Stornieren und neue Charge erstellen** in der Phys. Bestandsaufnahme; wenn Sie **Fertigungsauftrag** wählen, greift die Zeile beim Buchen einer Istmeldung eines Fertigungsauftrags (Prozess des Basismoduls). Pro Prozess und Feld ist genau eine Zeile möglich. |
| **Feldnummer** | Legt fest, welches Feld der **Chargennr.-Information** übertragen wird. Wenn Sie über den Drilldown ein Feld auswählen, wird dieses Feld beim Erzeugen der neuen Charge von der Ausgangscharge auf die Zielcharge kopiert; ohne Zeile für dieses Feld bleibt das Feld auf der neuen Charge leer. Auswählbar sind die normalen (nicht systemeigenen) Felder der Chargennr.-Information. |
| **Feldname** | Zeigt den technischen Feldnamen zum gewählten Feld an. Das Feld wird automatisch gefüllt und dient der eindeutigen Zuordnung; eine Eingabe ist nicht erforderlich. |
| **Feldüberschrift** | Zeigt die Beschriftung des gewählten Feldes so an, wie der Anwender sie auf der **Chargennr.-Informationskarte** sieht. Das Feld wird automatisch gefüllt und erleichtert das Wiederfinden der eingerichteten Felder. |

**Prozess — Bedeutung je Wert (vollständig):**

- **Fertigungsauftrag:** Die Zeile gilt für die Chargenweitergabe im Fertigungsauftrag (Übergabe der
  Ursprungscharge an das Fertigprodukt). Dieser Wert wird vom Basismodul verwendet und ist hier nur der
  Vollständigkeit halber aufgeführt.
- **Phys. Bestandsaufnahme:** Die Zeile gilt für die Phys. Bestandsaufnahme. Wenn ein Anwender dort die Aktion
  **Stornieren und neue Charge erstellen** ausführt, werden genau die für diesen Prozess eingerichteten Felder auf
  die neue Charge übertragen. Dieser Wert wird durch die vorliegende App ergänzt.

**Ablauf der Einrichtung (in Abhängigkeitsreihenfolge):**

1. **Zuerst** öffnen Sie über **Suchen** die **Chargeninformationsübertragungseinrichtung**.
2. **Danach** legen Sie je zu übertragendem Feld eine Zeile an und setzen im Feld **Prozess** den Wert
   **Phys. Bestandsaufnahme**.
3. **Danach** wählen Sie im Feld **Feldnummer** über den Drilldown das gewünschte Feld der **Chargennr.-Information**
   aus. Wiederholen Sie dies für jedes Feld, das mitgeführt werden soll.
4. **Schließlich** stellen Sie sicher, dass dem betroffenen Artikel eine **Nummernserie** für Chargen zugeordnet
   ist, damit die neue **Chargennr.** automatisch vergeben werden kann. Die eingerichtete Feldübertragung wird
   anschließend im Tagesablauf durch die Aktion **Stornieren und neue Charge erstellen** ausgelöst (siehe
   **Tägliche Arbeit an der Phys. Bestandsaufnahme**).

☞ Legen Sie keine Zeile für ein Feld an, wird dieses Feld beim Erzeugen der neuen Charge **nicht** aus der
Ausgangscharge übernommen. Die Herkunftsfelder (**Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode**,
**Ursprüngliche Chargennr.**) werden hingegen **immer** gesetzt, unabhängig von der Einrichtung (siehe
**Stammdaten: Chargennr.-Informationskarte**).

## Stammdaten: Chargennr.-Informationskarte

Die **Chargennr.-Informationskarte** ist die zentrale Stammkarte einer Charge. Diese App pflegt keine eigenen
Stammdaten, schreibt aber auf der Karte der **neu erzeugten** Charge die Herkunfts- und Zusatzangaben, die sie aus
der Ausgangscharge übernimmt. Der Anwender liest diese Werte auf der Karte ab.

**Wer und wann.** Die Werte entstehen **automatisch** im Moment der Aktion **Stornieren und neue Charge erstellen**
in der **Phys. Bestandsaufnahme**. Ein manuelles Pflegen ist für die Herkunftsfelder nicht erforderlich; sie sind
auf der Karte nicht editierbar.

**Wo sichtbar.** Öffnen Sie die **Chargennr.-Informationskarte** der neuen Charge (aus der Chargenverfolgung des
Artikels bzw. aus der Chargennr.-Information). Dort finden Sie unter anderem die folgenden Felder, die diese App
befüllt:

| Feld | Erläuterung |
|---|---|
| **Ursprüngliche Artikel-Nr.** | Wenn eine neue Charge über **Stornieren und neue Charge erstellen** entsteht, wird hier die Artikelnr. der Ausgangscharge eingetragen; so ist nachvollziehbar, aus welchem Artikel die Charge hervorgegangen ist. Das Feld ist nicht editierbar. |
| **Ursprünglicher Variantencode** | Wenn die Ausgangscharge einen Variantencode besitzt, wird dieser auf die neue Charge übernommen; damit bleibt die Variantenzuordnung erhalten. |
| **Ursprüngliche Chargennr.** | Wenn eine neue Charge entsteht, wird hier die **Chargennr.** der Ausgangscharge (Ursprungscharge) eingetragen; die Herkunft der Charge ist damit lückenlos dokumentiert. |
| **Zugangsdatum** | Wird das Zugangsdatum der Ausgangscharge geführt, wird es auf die neue Charge übernommen; dadurch bleibt die zeitliche Einordnung des Bestands erhalten. |
| **Bund** | Ist die Ausgangscharge als **Bund** gekennzeichnet, wird diese Kennzeichnung auf die neue Charge übernommen; die neue Charge wird damit gleich behandelt wie die Ausgangscharge. |
| **Herstellercode** | Der Herstellercode der Ausgangscharge wird auf die neue Charge übernommen; die Herstellerzuordnung bleibt erhalten. |
| **Ursprungsland/-regionscode** | Das Ursprungsland bzw. die Ursprungsregion der Ausgangscharge wird auf die neue Charge übernommen; die Herkunftsangabe bleibt für Nachweise verfügbar. |
| **Einkaufsbelegnr.** | Ist die Ausgangscharge einem Einkaufsbeleg zugeordnet, wird die Einkaufsbelegnr. auf die neue Charge übernommen; der Bezug zum Wareneingang bleibt bestehen. |
| **Eingekauft von Kreditornr.** | Der einkaufende Kreditor der Ausgangscharge wird auf die neue Charge übernommen; die Lieferantenzuordnung bleibt erhalten. |
| **Lieferantenchargennr.** | Die Lieferantenchargennr. der Ausgangscharge wird auf die neue Charge übernommen; die externe Chargenreferenz bleibt nachvollziehbar. |
| **Lieferanten interne Chargennr.** | Die interne Chargennr. des Lieferanten wird auf die neue Charge übernommen; auch diese externe Referenz bleibt erhalten. |

☞ Zusätzlich zu diesen fest übernommenen Feldern werden **alle** Felder übertragen, die Sie in der
**Chargeninformationsübertragungseinrichtung** für den Prozess **Phys. Bestandsaufnahme** eingerichtet haben.

## Tägliche Arbeit an der Phys. Bestandsaufnahme

In der **Phys. Bestandsaufnahme** erfassen die Anwender die tatsächlich vorhandenen Bestände. Kann eine gezählte
Menge einer Charge nicht widerspruchsfrei fortgeschrieben werden, wird die betroffene Charge storniert und eine neue
Charge angelegt. Genau in diesem Moment greift die Feldübertragung dieser App (Einrichtung siehe
**Feldübertragung für die Phys. Bestandsaufnahme einrichten**).

**Einstieg:** Öffnen Sie über **Suchen** die **Phys. Bestandsaufnahme** und wählen Sie die Erfassungszeile. Die
Aktionen dieser Funktion liegen im Menüband in der Gruppe **Funktionen**.

Die folgenden Aktionen stehen auf den Erfassungszeilen zur Verfügung:

| Aktion | Erläuterung |
|---|---|
| **Charge erstellen** | Wenn Sie diese Aktion wählen, wird eine zusätzliche Erfassungszeile mit einer neuen, aus der **Nummernserie** des Artikels gezogenen **Chargennr.** angelegt. Es handelt sich um eine leere neue Charge; es werden **keine** Felder aus einer bestehenden Charge übernommen. |
| **Stornieren und neue Charge erstellen** | Wenn Sie diese Aktion für die markierten Zeilen wählen, wird je Zeile eine neue **Chargennr.** erzeugt, die eingerichteten Felder sowie die Herkunftsfelder werden von der bisherigen Charge auf die neue Charge übertragen, die neue Zeile erhält im Feld **Kopiert von Chargennr.** die Ausgangscharge und die bisherige Zeile wird mit Menge 0 als **Storniert** gekennzeichnet. Diese Aktion löst die Feldübertragung dieser App aus. |
| **Stornierung rückgängig machen** | Wenn Sie diese Aktion für stornierte Zeilen wählen, wird die zuvor erzeugte neue Charge wieder entfernt und die ursprüngliche Zeile reaktiviert (Kennzeichen **Storniert** zurückgesetzt). So korrigieren Sie eine versehentlich erzeugte neue Charge. |

**Ablauf beim Erzeugen einer neuen Charge (Reihenfolge aus dem Code):**

1. Sie wählen die Erfassungszeile in der **Phys. Bestandsaufnahme**.
2. Sie wählen **Funktionen → Stornieren und neue Charge erstellen**. Die Aktion ist nur ausführbar, wenn der Artikel
   nicht auf **Mengenkonsistenz** = *immer Menge ändern* eingestellt ist (siehe Hinweis unten).
3. Business Central zieht aus der **Nummernserie** des Artikels eine neue **Chargennr.**
4. Die für den Prozess **Phys. Bestandsaufnahme** eingerichteten Felder werden von der Ausgangscharge auf die neue
   Charge übertragen.
5. Die Herkunftsfelder (**Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode**, **Ursprüngliche
   Chargennr.**) sowie Zugangsdatum, Bund, Herstellercode, Ursprungsland/-regionscode, Einkaufsangaben, Kreditor-
   und Lieferantenchargenangaben werden auf die neue Charge gesetzt.
6. Die neue Erfassungszeile trägt die neue **Chargennr.** und **Kopiert von Chargennr.**; die alte Zeile ist
   **Storniert**. Das Ergebnis prüfen Sie auf der **Chargennr.-Informationskarte** der neuen Charge.

☞ **Interlock Mengenkonsistenz:** Ist der Artikel so eingestellt, dass die Menge immer direkt geändert wird
(**Mengenkonsistenz** = *immer Menge ändern*), ist die Aktion **Stornieren und neue Charge erstellen** deaktiviert.
In diesem Fall wird keine neue Charge erzeugt und es findet keine Feldübertragung statt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Bestandskorrektur mit neuer Charge während der Inventur

**Auslöser.** Bei der Inventur stellt ein Lagermitarbeiter fest, dass die gezählte Menge einer Charge nicht mit dem
erwarteten Bestand übereinstimmt und die Charge daher nicht unverändert fortgeschrieben werden kann.

**Einstieg in BC.** Der Mitarbeiter öffnet über **Suchen** die **Phys. Bestandsaufnahme** und wählt die
Erfassungszeile der betroffenen Charge aus.

**Kernablauf.**
1. Der Mitarbeiter wählt die Erfassungszeile.
2. Er wählt **Funktionen → Stornieren und neue Charge erstellen**.
3. Business Central vergibt eine neue **Chargennr.** aus der **Nummernserie** des Artikels.
4. Die eingerichteten Felder (Prozess **Phys. Bestandsaufnahme**) werden von der alten auf die neue Charge
   übertragen.
5. Die Herkunftsfelder **Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode** und **Ursprüngliche
   Chargennr.** werden gesetzt; die alte Zeile wird als **Storniert** markiert, die neue Zeile führt **Kopiert von
   Chargennr.**

**Abschluss.** Der Mitarbeiter öffnet die **Chargennr.-Informationskarte** der neuen Charge und bestätigt, dass die
Herkunfts- und Zusatzangaben korrekt übernommen wurden. Damit ist die Herkunft der neuen Charge lückenlos
dokumentiert.

### Anwendungsfall 2: Erstkonfiguration durch den Administrator

**Auslöser.** Vor der ersten Inventur mit diesem Modul soll festgelegt werden, welche Chargenangaben bei einer
Neuanlage automatisch mitgeführt werden.

**Einstieg in BC.** Der Administrator öffnet über **Suchen** die **Chargeninformationsübertragungseinrichtung**.

**Kernablauf.**
1. Der Administrator legt je zu übertragendem Feld eine Zeile an.
2. Im Feld **Prozess** wählt er **Phys. Bestandsaufnahme**.
3. Im Feld **Feldnummer** wählt er über den Drilldown die relevanten Felder der **Chargennr.-Information** aus;
   **Feldname** und **Feldüberschrift** werden automatisch angezeigt.
4. Er stellt sicher, dass den betroffenen Artikeln eine **Nummernserie** für Chargen zugeordnet ist.

**Abschluss.** Ab sofort werden bei jeder Aktion **Stornieren und neue Charge erstellen** in der
**Phys. Bestandsaufnahme** die eingerichteten Felder automatisch übertragen. Die Einrichtung wird im Tagesablauf
durch die Anwender genutzt (siehe **Tägliche Arbeit an der Phys. Bestandsaufnahme**).

## FAQ und Troubleshooting

### Warum stehen in der Chargeninformationsübertragungseinrichtung zwei Prozesse zur Auswahl?
Das Feld **Prozess** ist ein Optionsfeld mit den Werten **Fertigungsauftrag** und **Phys. Bestandsaufnahme**. Der
Wert **Fertigungsauftrag** stammt aus dem Basismodul und steuert die Chargenweitergabe im Fertigungsauftrag; der
Wert **Phys. Bestandsaufnahme** wird durch diese App ergänzt und steuert die Feldübertragung in der Inventur. Für
die vorliegende App richten Sie Zeilen mit dem Prozess **Phys. Bestandsaufnahme** ein.

### Warum werden bei der neuen Charge nicht alle Felder aus der alten Charge übernommen?
Übernommen werden nur die Felder, für die eine Zeile mit dem Prozess **Phys. Bestandsaufnahme** in der
**Chargeninformationsübertragungseinrichtung** existiert. Fehlt eine Zeile für ein Feld, bleibt dieses Feld auf der
neuen Charge leer. Ergänzen Sie die fehlende Zeile in der Einrichtung.

### Was passiert, wenn ich für ein Feld keine Zeile in der Einrichtung angelegt habe?
Das betreffende Feld wird beim Erzeugen der neuen Charge nicht aus der Ausgangscharge kopiert. Die
Herkunftsfelder **Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode** und **Ursprüngliche Chargennr.**
werden jedoch unabhängig von der Einrichtung immer gesetzt.

### Warum ist die Aktion „Stornieren und neue Charge erstellen" ausgegraut?
Die Aktion ist nur aktiv, wenn der Artikel nicht auf **Mengenkonsistenz** = *immer Menge ändern* eingestellt ist.
Bei dieser Einstellung wird die Menge direkt geändert, statt eine neue Charge anzulegen; deshalb ist die Aktion
deaktiviert.

### Warum erhalte ich beim Erstellen der neuen Charge keine Chargennr.?
Eine neue **Chargennr.** wird automatisch aus der dem Artikel zugeordneten **Nummernserie** für Chargen gezogen.
Fehlt diese Zuordnung am Artikel, kann keine neue Charge angelegt werden. Ordnen Sie dem Artikel eine Nummernserie
für Chargen zu.

### Wie unterscheiden sich „Charge erstellen" und „Stornieren und neue Charge erstellen"?
**Charge erstellen** legt eine zusätzliche, leere Erfassungszeile mit neuer **Chargennr.** an, ohne Felder aus einer
bestehenden Charge zu übernehmen. **Stornieren und neue Charge erstellen** storniert die bisherige Zeile, legt eine
neue Charge an und überträgt die eingerichteten Felder sowie die Herkunftsangaben von der alten Charge.

### Wie erkenne ich, aus welcher Charge eine neue Charge entstanden ist?
Auf der Erfassungszeile zeigt das Feld **Kopiert von Chargennr.** die Ausgangscharge. Auf der
**Chargennr.-Informationskarte** der neuen Charge steht die Ausgangscharge zusätzlich im Feld **Ursprüngliche
Chargennr.**

### Kann ich eine versehentlich erzeugte neue Charge wieder entfernen?
Ja. Wählen Sie in der **Phys. Bestandsaufnahme** die stornierte Zeile und danach **Funktionen → Stornierung
rückgängig machen**. Die neue Charge wird entfernt und die ursprüngliche Zeile wird reaktiviert.

### Werden die Herkunftsfelder auf der Chargennr.-Informationskarte automatisch gefüllt?
Ja. Die Felder **Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode** und **Ursprüngliche Chargennr.**
werden beim Erzeugen der neuen Charge automatisch aus der Ausgangscharge gesetzt und sind auf der Karte nicht
editierbar.

### Muss ich diese App gesondert einrichten?
Für die Nutzung im Webclient „Microsoft Dynamics 365 Business Central" ist keine separate Einrichtung dieser App
erforderlich. Es genügt, dass die App und ihre Basismodule installiert sind und dass in der
**Chargeninformationsübertragungseinrichtung** die gewünschten Felder für den Prozess **Phys. Bestandsaufnahme**
hinterlegt sind.
