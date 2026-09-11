---
title: Anwenderhandbuch m+m Item Charge Management
---

# Anwenderhandbuch m+m Item Charge Management

## Einleitung

Das Modul **m+m Item Charge Management** erweitert die Zu-/Abschlagsverarbeitung von Microsoft Dynamics 365 Business Central. Es ermöglicht, **Zu-/Abschläge** (Frachten, Verpackungspauschalen, Mindermengenzuschläge und ähnliche Nebenkosten) regelbasiert aus Stammdaten heraus in Verkaufs- und Einkaufsbelege einzusteuern – automatisch bei der Freigabe, manuell auf Knopfdruck oder als vorgefilterte Auswahl. Damit entfällt das wiederholte manuelle Anlegen von Zu-/Abschlagszeilen, und die Verteilung der Kosten auf die Artikelzeilen erfolgt nach hinterlegten Regeln.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwenderinnen und Anwender im Vertrieb und Einkauf**, die täglich Verkaufsaufträge, Verkaufsrechnungen, Bestellungen und Einkaufsrechnungen bearbeiten, freigeben und buchen. Sie fügen in den Belegzeilen Zu-/Abschläge hinzu oder lassen diese bei der Freigabe automatisch erzeugen. **Administratorinnen und Administratoren sowie Key-User** sind sekundäre Zielgruppe: Sie pflegen die zentrale **Artikel Zu-/Abschlagseinrichtung**, die einzelnen **Artikel Zu-/Abschläge** und deren **Zu-/Abschlagszuweisungen**.

**Prozessüberblick.** Bevor Zu-/Abschläge in Belegen wirken, konfiguriert der Administrator drei aufeinander aufbauende Ebenen: die globale **Artikel Zu-/Abschlagseinrichtung**, die einzelnen **Artikel Zu-/Abschläge** (Stammkarte mit Bezugsgröße, Berechnungszeitpunkt und Übernahmeregel) und je Zu-/Abschlag eine oder mehrere **Zu-/Abschlagszuweisungen** (Preis und Gültigkeit je Debitor/Kreditor und Artikel). Optional grenzen **Spezifische Zuweisungen** eine Zuweisung auf bestimmte Belegklassen (z. B. nur Verkaufsrechnung) ein. In der täglichen Arbeit wählt der Anwender im Beleg die Aktion **Freigeben**, **Zu-/Abschläge hinzufügen** oder **Vorgeschlagene Zu-/Abschläge**; das Modul erzeugt daraufhin die passenden Zu-/Abschlagszeilen und ordnet sie den Artikelzeilen zu.

Der typische Einstiegspfad lautet: **Artikel Zu-/Abschläge** (Stammkarte) öffnen → Aktion **Zu-/Abschlagsmanagement → Zu-/Abschlagszuweisungen** → Zuweisung pflegen; anschließend im **Verkaufsauftrag** bzw. in der **Bestellung** die Belegzeile bearbeiten und über **Freigeben** oder die Zeilenaktionen den Zu-/Abschlag einsteuern.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg vom leeren System zum wirksamen Zu-/Abschlag. Die Einrichtung ist Voraussetzung und steht daher zuerst.

1. **Einmalig einrichten (Administrator):** Öffnen Sie über **Suchen** die **Artikel Zu-/Abschlagseinrichtung** und legen Sie fest, wie Belegzuschläge verteilt werden und zu welchem Lieferzeitpunkt Menge-/Pauschal-Zu-/Abschläge berechnet werden.
2. **Artikel Zu-/Abschlag anlegen:** Öffnen Sie über **Suchen** die **Artikel Zu-/Abschläge**, legen Sie einen Datensatz an und setzen Sie **Bezugsgröße**, **Automatisch in Beleg übernehmen**, **In Belegzeile auswählbar** und **Berechnungszeitpunkt**.
3. **Preis zuweisen:** Wählen Sie auf der Karte **Artikel Zu-/Abschläge** die Aktion **Zu-/Abschlagsmanagement → Zu-/Abschlagszuweisungen** und erfassen Sie je Debitor/Kreditor (oder „Alle Debitoren“/„Alle Kreditoren“) den **Preis**, die **Preisart**, den Gültigkeitszeitraum und – bei Bedarf – **Mindestbezugsart**, **Mindestwert** und **Differenz auffüllen**.
4. **Im Beleg anwenden:** Legen Sie einen **Verkaufsauftrag** (oder eine **Bestellung**) mit einer Artikelzeile an.
   - Bei **Automatisch in Beleg übernehmen = Bei Freigabe** wählen Sie **Freigeben** – der Zu-/Abschlag wird als eigene Zeile erzeugt.
   - Bei Bedarf ergänzen Sie in der Belegzeile über **Zeile → Funktionen → Zu-/Abschläge hinzufügen** oder **Vorgeschlagene Zu-/Abschläge** weitere Zu-/Abschläge.
5. **Liefern und buchen:** Verarbeiten Sie den Beleg im Business-Central-Standard weiter (ggf. Warenausgang buchen) und wählen Sie **Buchen**. Über **Status zurücksetzen** entfernt das System automatisch erzeugte Zu-/Abschlagszeilen wieder, sodass eine erneute Freigabe die aktuelle Konfiguration anwendet.

## Einrichtung

Die Einrichtung ist die Grundlage des Moduls. Sie besteht aus einer globalen Einrichtungskarte, den Stammkarten der einzelnen Zu-/Abschläge (im Kapitel **Stammdaten** beschrieben) und der Berechtigungsvergabe.

### Artikel Zu-/Abschlagseinrichtung

**Wer und wann.** Diese Karte pflegt der Administrator **einmalig vor der ersten Nutzung**. Sie ist ein unternehmensweiter Einzeldatensatz (Singleton): Beim ersten Öffnen wird der Datensatz automatisch angelegt. Die hier gesetzten Werte gelten als Vorbelegung für **jeden** Artikel Zu-/Abschlag mit Bezugsgröße **Beleg**, **Menge** oder **Pauschal** und wirken damit indirekt in allen Verkaufs- und Einkaufsbelegen.

**Einstieg:** Öffnen Sie über **Suchen** die **Artikel Zu-/Abschlagseinrichtung**. Es handelt sich um eine globale Einrichtungsseite ohne übergeordnete Stammdaten; der Aufruf über **Suchen** ist hier der vorgesehene Weg.

Die Seite ist in die Bereiche **Allgemein**, **Verkauf** und **Einkauf** gegliedert.

| Einrichtung | Erläuterung |
|---|---|
| **Zu-/Abschlagsverteilung bei Bezugsgröße Beleg** (Allgemein) | Wenn ein Zu-/Abschlag die Bezugsgröße **Beleg** hat, dann wird der Belegbetrag mit dieser Regel auf alle Artikelzeilen verteilt. **Volumen:** Verteilung nach Volumen × Menge (Gesamtvolumen) der Zeilen. **Wert:** Verteilung anhand des Zeilenbetrags. **zu gleichen Teilen:** prozentual gleichmäßig nach Anzahl der Zeilen (z. B. 4 Zeilen je 25 %). **Gewicht:** Verteilung anhand des Nettogewichts der Zeilen. Die Auswahl bestimmt, welchen Betrag jede Artikelzeile aus dem Belegzuschlag erhält. |
| **Menge/Pauschal zu liefern (VK)** (Verkauf) | Legt fest, zu welchem Lieferzeitpunkt ein Verkaufs-Zu-/Abschlag mit Bezugsgröße **Menge** oder **Pauschal** berechnet wird. Wirkt als Vorbelegung für neue Verkaufs-Zu-/Abschläge. Werte siehe unten. |
| **Bezugsgröße Beleg zu liefern (VK)** (Verkauf) | Legt fest, zu welchem Lieferzeitpunkt ein Verkaufs-Zu-/Abschlag mit Bezugsgröße **Beleg** berechnet wird. Vorbelegung für neue Verkaufs-Zu-/Abschläge. Werte siehe unten. |
| **Menge/Pauschal zu liefern (EK)** (Einkauf) | Legt fest, zu welchem Lieferzeitpunkt ein Einkaufs-Zu-/Abschlag mit Bezugsgröße **Menge** oder **Pauschal** berechnet wird. Vorbelegung für neue Einkaufs-Zu-/Abschläge. Werte siehe unten. |
| **Bezugsgröße Beleg zu liefern (EK)** (Einkauf) | Legt fest, zu welchem Lieferzeitpunkt ein Einkaufs-Zu-/Abschlag mit Bezugsgröße **Beleg** berechnet wird. Vorbelegung für neue Einkaufs-Zu-/Abschläge. Werte siehe unten. |

Werte für **Menge/Pauschal zu liefern (VK)** und **(EK)**:
- **Standard:** Wenn ausgewählt, verhält sich das System wie der Business-Central-Standard; der Zu-/Abschlag folgt der normalen Mengenlogik.
- **Erste Lieferung (komplett):** Wenn ausgewählt, wird der Zu-/Abschlag vollständig bei der ersten Lieferung berechnet.
- **Letzte Lieferung (komplett):** Wenn ausgewählt, wird der Zu-/Abschlag bei der letzten Lieferung berechnet; er greift, sobald die Restmenge 0 erreicht.
- **Jede Lieferung:** Wenn ausgewählt, wird der Zu-/Abschlag anteilig zur jeweils gelieferten Menge berechnet.

Werte für **Bezugsgröße Beleg zu liefern (VK)** und **(EK)**:
- **Standard:** Wenn ausgewählt, gilt das Standardverhalten von Business Central.
- **Erste Lieferung:** Wenn ausgewählt, wird der belegbezogene Zu-/Abschlag bei der ersten Lieferung berechnet.
- **Letzte Lieferung:** Wenn ausgewählt, wird der belegbezogene Zu-/Abschlag bei der letzten Lieferung berechnet, sobald die Restmenge 0 erreicht.

**Zusammenhang mit der täglichen Arbeit.** Diese Vorbelegungen greifen, sobald auf einer Zu-/Abschlagskarte die **Bezugsgröße** gesetzt wird (siehe Stammdaten): Für Bezugsgröße **Beleg** übernimmt das System die Werte **Bezugsgröße Beleg zu liefern (VK/EK)**, für Bezugsgröße **Menge**/**Pauschal** die Werte **Menge/Pauschal zu liefern (VK/EK)**. Der Lieferzeitpunkt entscheidet später beim Buchen, welcher Mengenanteil des Zu-/Abschlags wirksam wird.

### Berechtigungen einrichten

**Wer und wann.** Der Administrator ordnet den Anwendern vor der ersten Nutzung den Berechtigungssatz des Moduls zu. Der Berechtigungssatz **„All permissions“** (interner Berechtigungssatz des Moduls) legt fest, welche Aktionen die Anwender auf den Zu-/Abschlagsdaten ausführen dürfen: Er gewährt Vollzugriff (Lesen, Einfügen, Ändern, Löschen) auf die Tabellen **Zu-/Abschlagszuweisung**, **Spezifische Zuweisung**, **Artikel Zu-/Abschlagseinrichtung**, **Zu-/Abschlagsübersetzung** sowie den zugehörigen Seiten und Verarbeitungscodeeinheiten. Ohne diesen Berechtigungssatz können Anwender die Zu-/Abschlagsstammdaten weder einsehen noch pflegen und die Belegaktionen nicht ausführen. Vergeben Sie den Satz über die Standard-Berechtigungsverwaltung von Business Central an die betreffenden Benutzergruppen.

## Stammdaten

Auf den Stammdaten baut die gesamte Automatik auf. Sie umfasst die **Artikel Zu-/Abschläge** (die eigentlichen Zu-/Abschlagsarten), deren **Zu-/Abschlagszuweisungen** (Preise und Gültigkeiten), die optionalen **Spezifischen Zuweisungen** (Belegklassen-Steuerung) und die **Übersetzungen**.

### Artikel Zu-/Abschläge (Stammkarte)

**Wer und wann.** Key-User oder Administrator pflegen die Zu-/Abschlagsarten, bevor sie in Belegen eingesteuert werden. Jeder Datensatz beschreibt genau eine Zu-/Abschlagsart (z. B. „Fracht“, „Mindermengenzuschlag“) und steuert, **wie** und **wann** sie in Belege gelangt.

**Einstieg:** Öffnen Sie über **Suchen** die **Artikel Zu-/Abschläge**. Die Seite ist die zentrale Stammliste; sie erweitert die Business-Central-Standardseite um die folgenden Felder und um die Aktionsgruppe **Zu-/Abschlagsmanagement**.

| Feld | Erläuterung |
|---|---|
| **Nr.** | Eindeutige Nummer des Zu-/Abschlags; dient als Referenz in Zuweisungen und Belegzeilen. |
| **Beschreibung** | Sprechende Bezeichnung des Zu-/Abschlags; erscheint als Text der erzeugten Belegzeile. |
| **Produktbuchungsgruppe** | Wenn gesetzt, dann verknüpft sie die Buchungen des Zu-/Abschlags über die Buchungsmatrix mit dem passenden Sachkonto; ohne korrekte Gruppe schlägt das Buchen der Zu-/Abschlagszeile fehl. |
| **MwSt.-Produktbuchungsgruppe** | Wenn gesetzt, dann steuert sie die Umsatzsteuer der Zu-/Abschlagszeile über die MwSt.-Buchungsmatrix; bestimmt den ausgewiesenen Steuerbetrag. |
| **Bezugsgröße** | Bestimmt, worauf sich der Zu-/Abschlag bezieht und steuert damit die gesamte Folgeverarbeitung. Werte siehe unten. |
| **In Belegzeile auswählbar** | Wenn aktiviert, dann kann der Anwender diesen Zu-/Abschlag in der Belegzeile über **Zu-/Abschläge hinzufügen** manuell auswählen; ist das Kennzeichen nicht gesetzt, erscheint der Zu-/Abschlag nicht in der Auswahlliste. |
| **Automatisch in Beleg übernehmen** | Steuert, ob und wann der Zu-/Abschlag ohne Zutun in den Beleg gelangt. Werte siehe unten. |
| **Einheitencode** | Wenn gesetzt, dann wird die erzeugte Zu-/Abschlagszeile mit dieser Einheit angelegt; ohne Eintrag verwendet die Zeile keine gesonderte Einheit. |
| **Berechnungszeitpunkt** | Legt fest, welches Datum der Preisfindung des Zu-/Abschlags bei der Rechnungserstellung zugrunde liegt. Werte siehe unten. Vorbelegung ist **Auftrags-/Bestelldatum**. |
| **Bezugsgröße Beleg zu liefern (EK)** | Wenn die Bezugsgröße **Beleg** ist, dann bestimmt dieser Wert den Lieferzeitpunkt im Einkauf; er wird aus der Einrichtung vorbelegt und ist nur bei Bezugsgröße **Beleg** editierbar. |
| **Menge/Pauschal zu liefern (EK)** | Wenn die Bezugsgröße **Menge**/**Pauschal** ist, dann bestimmt dieser Wert den Lieferzeitpunkt im Einkauf; wird aus der Einrichtung vorbelegt. |
| **Bezugsgröße Beleg zu liefern (VK)** | Wie zuvor, jedoch für den Verkauf und nur bei Bezugsgröße **Beleg** editierbar. |
| **Menge/Pauschal zu liefern (VK)** | Wie zuvor, jedoch für den Verkauf und nur bei Bezugsgröße **Menge**/**Pauschal** editierbar. |
| **Suchbegriff** | Wenn gesetzt, dann findet der Anwender den Zu-/Abschlag über diesen Text, auch wenn die Nummer unbekannt ist. |

Werte für **Bezugsgröße**:
- **(leer):** Es gilt der Business-Central-Standard; der Zu-/Abschlag wird nicht durch das Modul eingesteuert.
- **Pauschal Teilweise:** Zeilenbezogen mit Menge = 1; der Zu-/Abschlag bezieht sich anteilig auf die einzelne Artikelzeile.
- **Beleg:** Der Zu-/Abschlag bezieht sich auf sämtliche Zeilen des Belegs (Menge = 1) und wird nach der Regel **Zu-/Abschlagsverteilung bei Bezugsgröße Beleg** verteilt.
- **Menge:** Zeilenbezogen mit Menge = Menge der Artikelzeile; der Zu-/Abschlag skaliert mit der Artikelmenge.
- **Pauschal Gesamt:** Pauschal auf den gesamten Zeilenbetrag bezogen.

Werte für **Automatisch in Beleg übernehmen**:
- **(leer):** Keine automatische Übernahme; der Zu-/Abschlag steht nur zur manuellen Auswahl bereit (sofern **In Belegzeile auswählbar**).
- **Ja:** Wenn ausgewählt, dann legt das System die Zu-/Abschlagszeile bereits beim Einfügen und Validieren der Artikelzeile automatisch an. Dieser Wert ist nicht mit Bezugsgröße **Beleg** kombinierbar (das System weist die Kombination mit einer Fehlermeldung ab).
- **Manuell:** Wenn ausgewählt, dann bleibt die Übernahme dem Anwender überlassen; er ergänzt die Zeile über **Zu-/Abschläge hinzufügen** oder **Vorgeschlagene Zu-/Abschläge**.
- **Bei Freigabe:** Wenn ausgewählt, dann erzeugt das System die Zu-/Abschlagszeile automatisch, sobald der Anwender den Beleg **freigibt**; beim **Status zurücksetzen** wird sie wieder entfernt.

Werte für **Berechnungszeitpunkt**:
- **(leer):** Kein gesonderter Zeitpunkt hinterlegt.
- **Arbeitsdatum:** Die Preisfindung bei Rechnungserstellung legt das Arbeitsdatum zugrunde.
- **Buchungsdatum:** Die Preisfindung legt das Buchungsdatum zugrunde.
- **Auftrags-/Bestelldatum:** Die Preisfindung legt das Auftrags- bzw. Bestelldatum zugrunde (Vorbelegung).
- **Lieferdatum/Erw. Wareneingangsdatum:** Die Preisfindung legt das Liefer- bzw. erwartete Wareneingangsdatum zugrunde.

**Aktionen der Aktionsgruppe „Zu-/Abschlagsmanagement“:**
- **Zu-/Abschlagszuweisungen** – öffnet gefiltert auf den aktuellen Zu-/Abschlag die **Zu-/Abschlagszuweisung** (siehe unten).
- **Übersetzungen** – öffnet die **Zu-/Abschlagsübersetzungen** (siehe unten).

#### Artikel Zu-/Abschlag einrichten

**Prozess.** Diese Kette macht einen Zu-/Abschlag in Belegen wirksam. Sie konfiguriert der Administrator einmalig je Zu-/Abschlagsart; die Verkaufs- und Einkaufsabteilung nutzt das Ergebnis später in der täglichen Arbeit (siehe Kapitel **Tägliche Arbeit**).

1. **Globale Einrichtung prüfen:** Legen Sie in der **Artikel Zu-/Abschlagseinrichtung** die Verteilungsregel und die Lieferzeitpunkte fest. Wenn diese Werte gesetzt sind, dann werden sie auf jeder neuen Zu-/Abschlagskarte automatisch vorbelegt.
2. **Zu-/Abschlagskarte anlegen:** Erfassen Sie auf **Artikel Zu-/Abschläge** die **Bezugsgröße**. Wenn Sie **Beleg** wählen, dann steuert die Verteilungsregel der Einrichtung die Aufteilung auf die Zeilen; wenn Sie **Menge**/**Pauschal** wählen, dann skaliert der Zu-/Abschlag mit der Zeile.
3. **Übernahmeverhalten festlegen:** Setzen Sie **Automatisch in Beleg übernehmen** (Ja / Manuell / Bei Freigabe) und – für die manuelle Auswahl – **In Belegzeile auswählbar**. Wenn **Bei Freigabe** gesetzt ist, dann entsteht die Belegzeile erst beim Freigeben.
4. **Preis zuweisen:** Wechseln Sie über **Zu-/Abschlagsmanagement → Zu-/Abschlagszuweisungen** und hinterlegen Sie den Preis je Debitor/Kreditor (nächster Abschnitt).
5. **Operativer Abschluss:** In der täglichen Arbeit greift der Anwender über **Freigeben** bzw. **Zu-/Abschläge hinzufügen**/**Vorgeschlagene Zu-/Abschläge** auf die konfigurierte Kette zu (siehe **Tägliche Arbeit im Verkauf**).

### Zu-/Abschlagszuweisung (Preistabelle)

**Wer und wann.** Der Key-User pflegt zu jedem Zu-/Abschlag die **Zu-/Abschlagszuweisungen**, bevor der Zu-/Abschlag preislich in Belegen wirkt. Hier werden Preise und Gültigkeiten je Debitor bzw. Kreditor und je Artikel definiert.

**Einstieg:** Öffnen Sie die Karte **Artikel Zu-/Abschläge** und wählen Sie die Aktion **Zu-/Abschlagsmanagement → Zu-/Abschlagszuweisungen**. Die Liste öffnet gefiltert auf den ausgewählten Zu-/Abschlag (**Nr.**).

| Feld | Erläuterung |
|---|---|
| **Nr.** | Verweist auf den Artikel Zu-/Abschlag, zu dem die Zuweisung gehört. |
| **Referenzart** | Legt fest, für welchen Geschäftspartnerkreis die Zuweisung gilt, und steuert die Auswahl der **Referenznummer**. Werte siehe unten. |
| **Referenznummer** | Wenn die Referenzart **Debitor** oder **Kreditor** ist, dann gibt dieses Feld den konkreten Debitor bzw. Kreditor an; bei **Alle Debitoren**/**Alle Kreditoren** bleibt es leer (das System weist einen Eintrag dort ab). |
| **Art** | Legt fest, ob die Zuweisung für einen bestimmten Artikel oder für alle Artikel gilt, und steuert das Feld **Code**. Werte siehe unten. |
| **Code** | Wenn die Art **Artikel** ist, dann enthält dieses Feld die Artikelnummer; bei **Alle Artikel** bleibt es leer. |
| **Preis** | Wenn gesetzt, dann bildet dieser Wert den Preis des Zu-/Abschlags; die Auslegung richtet sich nach der **Preisart**. |
| **Preisart** | Bestimmt, wie der **Preis** interpretiert wird. **Gesamt:** fester Betrag. **Prozentsatz:** prozentualer Wert, der je nach Bezugsgröße auf Belegbetrag, Zeilenbetrag oder Einzelpreis angewendet wird. |
| **Startdatum** | Wenn gesetzt, dann gilt die Zuweisung ab diesem Datum; leer bedeutet keine Untergrenze. |
| **Enddatum** | Wenn gesetzt, dann gilt die Zuweisung bis zu diesem Datum; das Startdatum darf nicht nach dem Enddatum liegen (das System weist dies ab). |
| **Mindestbezugsart** | Legt fest, gegen welche Bezugsgröße der **Mindestwert** geprüft wird. Werte siehe unten. |
| **Mindestwert** | Wenn gesetzt, dann greift der Zu-/Abschlag nur, solange der jeweilige Betrag (Zeile bzw. Beleg) den Mindestwert unterschreitet; setzt eine **Mindestbezugsart** voraus. |
| **Differenz auffüllen** | Wenn aktiviert, dann füllt der Zu-/Abschlag den Betrag bis zum **Mindestwert** auf, statt einen festen Betrag hinzuzufügen; nur mit Bezugsgröße **Beleg** und Mindestbezugsart **Zeilenbetrag** oder **Belegbetrag** zulässig. |
| **Spezifische Zuweisung** | Wenn auf **Spezifische Zuweisung** gesetzt, dann wird die Zuweisung zusätzlich über die **Spezifischen Zuweisungen** auf bestimmte Belegklassen eingegrenzt (siehe nächster Abschnitt); bei **(leer)** gilt die Zuweisung für Angebot und Auftrag ohne weitere Einschränkung. |
| **Anzahl spez. Zuweisungen** | Zeigt an, wie viele **Spezifische Zuweisungen** zu dieser Zeile hinterlegt sind (gefiltert nach dem gesetzten **Spezifischer Zuweisungsfilter**). Ein Klick auf die Zahl öffnet direkt die gefilterte Liste der Spezifischen Zuweisungen. |

Werte für **Referenzart**:
- **Alle Debitoren:** Die Zuweisung gilt für sämtliche Debitoren; die Referenznummer bleibt leer.
- **Debitor:** Die Zuweisung gilt für den in **Referenznummer** genannten Debitor.
- **Alle Kreditoren:** Die Zuweisung gilt für sämtliche Kreditoren; die Referenznummer bleibt leer.
- **Kreditor:** Die Zuweisung gilt für den in **Referenznummer** genannten Kreditor.

Werte für **Art**:
- **Alle Artikel:** Die Zuweisung gilt für alle Artikel; **Code** bleibt leer.
- **Artikel:** Die Zuweisung gilt für den in **Code** genannten Artikel.

Werte für **Mindestbezugsart**:
- **(leer):** Keine Mindestprüfung; der Zu-/Abschlag greift unabhängig vom Betrag.
- **Zeilenbetrag:** Der Mindestwert wird gegen den Betrag der einzelnen Artikelzeile geprüft.
- **Belegbetrag:** Der Mindestwert wird gegen den Gesamtbetrag des Belegs geprüft.

**Ermittlungslogik.** Bei der Anwendung sucht das Modul die passende Zuweisung in dieser Reihenfolge: zuerst **Artikel + Debitor/Kreditor**, dann **Alle Artikel + Debitor/Kreditor**, dann **Artikel + Alle Debitoren/Alle Kreditoren**, zuletzt **Alle Artikel + Alle Debitoren/Alle Kreditoren**. Zusätzlich muss der **Berechnungszeitpunkt** in den Gültigkeitszeitraum (Start-/Enddatum) fallen. Damit lassen sich allgemeine und speziell ausgehandelte Konditionen kombinieren.

#### Filter

Die Liste **Zu-/Abschlagszuweisung** stellt einen Belegklassen-Filter bereit, der das Zählfeld steuert.

| Filterfeld | Erläuterung |
|---|---|
| **Spezifischer Zuweisungsfilter** | Wenn gesetzt (VK-Angebot & Auftrag / VK-Rechnung / EK-Anfrage & Bestellung / EK-Rechnung), dann zählt das Feld **Anzahl spez. Zuweisungen** nur die Spezifischen Zuweisungen dieser Belegklasse; ohne Filter bezieht sich die Zählung auf alle hinterlegten Spezifischen Zuweisungen der Zeile. |

### Spezifische Zuweisung

**Wer und wann.** Der Key-User grenzt eine Zu-/Abschlagszuweisung auf bestimmte Belegklassen ein, wenn ein Zu-/Abschlag nur in bestimmten Belegen (z. B. erst in der Verkaufsrechnung) wirken soll. Diese Funktion adressiert Fälle, in denen der Verkaufspreis erst spät – etwa durch Kalkulation in der Rechnung – feststeht.

**Einstieg:** Öffnen Sie in der Liste **Zu-/Abschlagszuweisung** die betreffende Zeile, setzen Sie **Spezifische Zuweisung** auf **Spezifische Zuweisung** und wählen Sie anschließend die Aktion **Spezifische Zuweisungen**, oder klicken Sie in der Spalte **Anzahl spez. Zuweisungen** auf die Zahl. Die Seite **Spezifische Zuweisungen** ist nur über diesen Weg erreichbar (kein Aufruf über **Suchen**).

| Feld | Erläuterung |
|---|---|
| **Spezifische Zuweisung** | Legt fest, in welcher Belegklasse die übergeordnete Zuweisung wirken darf. Werte siehe unten. Die übrigen Spalten (Nr., Referenzart, Referenznummer, Art, Code, Start-/Enddatum) sind schreibgeschützt und werden aus der ausgewählten Zuweisungszeile übernommen. |

Werte für **Spezifische Zuweisung**:
- **VK-Angebot & Auftrag:** Wenn hinterlegt, dann greift der Zu-/Abschlag im Verkaufsangebot und im Verkaufsauftrag.
- **VK-Rechnung:** Wenn hinterlegt, dann greift der Zu-/Abschlag in der Verkaufsrechnung.
- **EK-Anfrage & Bestellung:** Wenn hinterlegt, dann greift der Zu-/Abschlag in Einkaufsanfrage und Bestellung.
- **EK-Rechnung:** Wenn hinterlegt, dann greift der Zu-/Abschlag in der Einkaufsrechnung.

#### Spezifische Zuweisung einrichten

**Prozess.** Diese Kette schaltet die belegklassen-genaue Steuerung frei. Sie ist die zweite, eigenständige Konfigurationskette des Moduls neben der allgemeinen Zu-/Abschlagseinrichtung.

1. **Zuweisung vorbereiten:** Legen Sie in der **Zu-/Abschlagszuweisung** die gewünschte Zeile (Preis, Referenzart, Gültigkeit) an.
2. **Spezifische Zuweisung aktivieren:** Setzen Sie in der Zeile das Feld **Spezifische Zuweisung** auf **Spezifische Zuweisung**. Wenn aktiviert, dann wird die Schaltfläche **Spezifische Zuweisungen** wirksam und die Zeile wird nur noch über hinterlegte Belegklassen ausgesteuert.
3. **Belegklassen hinterlegen:** Öffnen Sie über **Spezifische Zuweisungen** die Liste und erfassen Sie je Belegklasse (VK-Angebot & Auftrag, VK-Rechnung, EK-Anfrage & Bestellung, EK-Rechnung) einen Eintrag. Wenn eine Belegklasse hinterlegt ist, dann greift der Zu-/Abschlag genau dort.
4. **Prüfung im Beleg:** Über den **Spezifischer Zuweisungsfilter** und die Spalte **Anzahl spez. Zuweisungen** kontrollieren Sie, für welche Belegklasse Einträge bestehen.
5. **Operativer Abschluss:** In der Verkaufsrechnung bzw. Einkaufsrechnung ergänzt der Anwender die so gesteuerten Zu-/Abschläge über **Zu-/Abschläge hinzufügen** / **Vorgeschlagene Zu-/Abschläge** (siehe **Tägliche Arbeit**). Ohne passende Spezifische Zuweisung erscheint der Zu-/Abschlag in Rechnungen nicht.

### Übersetzungen

**Wer und wann.** Der Key-User pflegt Übersetzungen der Zu-/Abschlagsbeschreibung, wenn Belege in mehreren Sprachen erzeugt werden.

**Einstieg:** Öffnen Sie die Karte **Artikel Zu-/Abschläge** und wählen Sie **Zu-/Abschlagsmanagement → Übersetzungen**. Die Liste **Zu-/Abschlagsübersetzungen** ist ausschließlich über diese Aktion erreichbar.

| Feld | Erläuterung |
|---|---|
| **Sprachcode** | Wenn gesetzt, dann gilt die Übersetzung für diesen Sprachcode; das System wählt beim Belegdruck die zur Belegsprache passende Beschreibung. |
| **Beschreibung** | Übersetzter Text des Zu-/Abschlags, der anstelle der Standardbeschreibung erscheint. |

## Tägliche Arbeit im Verkauf

**Zusammenhang mit der Einrichtung.** Die im Verkauf sichtbaren Aktionen werden durch die Stammdaten gesteuert: **Artikel Zu-/Abschläge** (Bezugsgröße, Automatisch in Beleg übernehmen, In Belegzeile auswählbar, Berechnungszeitpunkt), **Zu-/Abschlagszuweisung** (Preis, Mindestwert, Differenz auffüllen) und – wo gepflegt – **Spezifische Zuweisung** (Belegklasse). Anpassungen an diesen Konditionen wirken unmittelbar in den nächsten Belegen.

Das Modul erweitert die Zeilenmenübänder folgender Verkaufsbelege um die Aktionen **Zu-/Abschläge hinzufügen** und **Vorgeschlagene Zu-/Abschläge** (jeweils unter **Zeile → Funktionen**):

- Verkaufsangebot
- Verkaufsauftrag
- Verkaufsrechnung

Zusätzlich hakt das Modul in die Standardfreigabe des **Verkaufsauftrags** (und weiterer Verkaufsbelege einschließlich des Rahmenauftrags) ein.

### Aktionen in der Verkaufsbelegzeile

- **Zu-/Abschläge hinzufügen** (Tastenkürzel Alt+Z): Öffnet die Liste der **Zu-/Abschläge**, gefiltert auf die im Beleg auswählbaren Zu-/Abschläge. Voraussetzung ist, dass der Zu-/Abschlag **In Belegzeile auswählbar** gesetzt hat; die aktive Zeile muss vom Typ **Artikel** sein. Nach Auswahl mit **OK** legt das System die passenden Zu-/Abschlagszeilen an und ordnet sie der Artikelzeile zu. In der Verkaufsrechnung sind zusätzlich nur Zu-/Abschläge mit passender **Spezifischer Zuweisung** (VK-Rechnung) auswählbar.
- **Vorgeschlagene Zu-/Abschläge**: Ermittelt für die markierte(n) Artikelzeile(n) die laut Stammdaten passenden manuellen Zu-/Abschläge und ergänzt sie, sofern noch nicht vorhanden. Bereits vorhandene Zuordnungen werden nicht doppelt erzeugt.

### Automatischer Zu-/Abschlag bei Freigabe (Buchungsablauf)

Der Buchungsablauf im Verkauf folgt dem Business-Central-Standard; das Modul ergänzt lediglich die automatische Zu-/Abschlagszeile:

1. **Verkaufsauftrag** öffnen und Artikelzeile (Typ **Artikel**, Menge) erfassen.
2. Optional in der Zeile über **Zeile → Funktionen** **Vorgeschlagene Zu-/Abschläge** oder **Zu-/Abschläge hinzufügen** ergänzen.
3. **Freigeben** wählen. Wenn der zugehörige Zu-/Abschlag **Automatisch in Beleg übernehmen = Bei Freigabe** hat, dann erzeugt das System jetzt die Zu-/Abschlagszeile und ordnet sie der Artikelzeile zu. Zu-/Abschläge mit **= Ja** entstehen bereits beim Erfassen der Artikelzeile.
4. Bei Bedarf **Status zurücksetzen** – automatisch erzeugte Zu-/Abschlagszeilen (Bei Freigabe) werden entfernt, sodass eine erneute Freigabe die aktuelle Konfiguration anwendet.
5. Beleg weiterverarbeiten (ggf. Warenausgang buchen) und **Buchen**. Der Zu-/Abschlag wird beim Buchen entsprechend **Menge/Pauschal zu liefern (VK)** bzw. **Bezugsgröße Beleg zu liefern (VK)** der jeweils gelieferten Menge zugeordnet.

**Belegkette.** Wird ein Verkaufsauftrag aus einem Angebot mit Zu-/Abschlägen erzeugt, werden die Zu-/Abschläge mitübernommen; dasselbe gilt beim Erzeugen einer Verkaufsrechnung aus einem Auftrag. Ein Zu-/Abschlag mit **Bei Freigabe** wird dabei nicht erneut erstellt, sofern für die Artikelzeile bereits eine Zuordnung besteht.

**Belegzuschlag mit Differenz auffüllen.** Ist ein Belegzuschlag auf **Differenz auffüllen** gesetzt, dann wird zuerst der Zeilenzuschlag den Artikelzeilen zugewiesen und anschließend der Belegzuschlag als letzte Zeile hinter allen Artikel- und Zu-/Abschlagszeilen verteilt. Der bereits vorhandene Zeilen- und Belegzeilenbetrag reduziert dabei den aufzufüllenden Belegbetrag, sodass der konfigurierte Gesamtbetrag (Mindestwert) exakt erreicht wird.

## Tägliche Arbeit im Einkauf

**Zusammenhang mit der Einrichtung.** Analog zum Verkauf steuern **Artikel Zu-/Abschläge**, **Zu-/Abschlagszuweisung** und **Spezifische Zuweisung** das Verhalten; im Einkauf gelten die EK-Varianten der Lieferzeitpunkte (**Menge/Pauschal zu liefern (EK)**, **Bezugsgröße Beleg zu liefern (EK)**) und die Referenzart **Kreditor**/**Alle Kreditoren**.

Das Modul erweitert die Zeilenmenübänder folgender Einkaufsbelege um **Zu-/Abschläge hinzufügen** und **Vorgeschlagene Zu-/Abschläge**:

- Einkaufsanfrage
- Bestellung
- Einkaufsrechnung

Zusätzlich hakt das Modul in die Freigabe der **Bestellung** (und des Rahmenbestellungsbelegs) ein.

### Aktionen in der Einkaufsbelegzeile und Buchungsablauf

- **Zu-/Abschläge hinzufügen** und **Vorgeschlagene Zu-/Abschläge** wirken wie im Verkauf: manuelle bzw. vorgefilterte Auswahl der laut Stammdaten passenden Zu-/Abschläge; Voraussetzung **In Belegzeile auswählbar** und Zeilentyp **Artikel**.
- **Freigeben** der Bestellung erzeugt automatisch die Zu-/Abschlagszeilen für alle Zu-/Abschläge mit **Automatisch in Beleg übernehmen = Bei Freigabe**; **Status zurücksetzen** entfernt sie wieder. Wurden zwischenzeitlich die Konditionen geändert, wird bei erneuter Freigabe die aktuelle Konfiguration angewendet.
- **Buchen** ordnet den Zu-/Abschlag entsprechend der EK-Lieferzeitpunkte der Wareneingangs- bzw. Rechnungsmenge zu.

**Historie und Archiv.** Werden Belege archiviert, übernehmen die Belegzeilenarchive die Steuerfelder des Zu-/Abschlags (u. a. **Zu-/Abschlag automatisch erstellt**, **Zu-/Abschlagsbezugsgröße**, **Mindestbezugsart**), sodass archivierte Belege die ursprüngliche Zu-/Abschlagslogik nachvollziehbar bewahren. Eine gesonderte Historienliste stellt das Modul nicht bereit; die Nachverfolgung erfolgt über die Standard-Belegarchive und die Wertposten von Business Central.

## FAQ und Troubleshooting

### 1. Warum erscheint mein Zu-/Abschlag nicht automatisch im Beleg?
Prüfen Sie auf der Karte **Artikel Zu-/Abschläge** das Feld **Automatisch in Beleg übernehmen**. Nur bei **Ja** (beim Erfassen der Artikelzeile) oder **Bei Freigabe** (beim Freigeben) entsteht die Zeile automatisch. Bei **Manuell** oder **(leer)** müssen Sie den Zu-/Abschlag über **Zu-/Abschläge hinzufügen** ergänzen.

### 2. Warum kann ich einen Zu-/Abschlag nicht über „Zu-/Abschläge hinzufügen“ auswählen?
Die Auswahl zeigt nur Zu-/Abschläge, bei denen **In Belegzeile auswählbar** aktiviert ist. Ist das Kennzeichen nicht gesetzt, blendet das System den Zu-/Abschlag in der Auswahlliste aus. Zudem muss die aktive Belegzeile vom Typ **Artikel** sein.

### 3. Warum meldet das System einen Fehler, wenn ich „Automatisch in Beleg übernehmen = Ja“ mit Bezugsgröße „Beleg“ kombiniere?
Diese Kombination ist unzulässig. Ein Belegzuschlag (**Bezugsgröße = Beleg**) kann nicht bereits beim Erfassen der Artikelzeile (**Ja**) gebildet werden, da er sich auf alle Zeilen bezieht. Wählen Sie stattdessen **Bei Freigabe** oder **Manuell**.

### 4. Wozu dient „Differenz auffüllen“?
Wenn **Differenz auffüllen** aktiviert ist, füllt der Zu-/Abschlag den Beleg- bzw. Zeilenbetrag bis zum **Mindestwert** auf, statt einen festen Betrag zu addieren. Das ist nur mit Bezugsgröße **Beleg** und Mindestbezugsart **Zeilenbetrag** oder **Belegbetrag** möglich und wird zum Erreichen von Mindestbeträgen genutzt.

### 5. Warum greift ein Zu-/Abschlag in der Verkaufsrechnung, nicht aber im Auftrag (oder umgekehrt)?
Verantwortlich ist die **Spezifische Zuweisung**. Ist sie auf **Spezifische Zuweisung** gesetzt, wirkt der Zu-/Abschlag nur in den unter **Spezifische Zuweisungen** hinterlegten Belegklassen (z. B. nur **VK-Rechnung**). Ohne passenden Eintrag erscheint der Zu-/Abschlag in der betreffenden Belegklasse nicht.

### 6. Wie prüfe ich, für welche Belege eine Zuweisung gilt?
Öffnen Sie die **Zu-/Abschlagszuweisung**, setzen Sie den **Spezifischer Zuweisungsfilter** auf die gewünschte Belegklasse und lesen Sie die Spalte **Anzahl spez. Zuweisungen** ab. Ein Klick auf die Zahl öffnet die gefilterte Liste der **Spezifischen Zuweisungen**.

### 7. Warum verschwindet meine automatische Zu-/Abschlagszeile beim Status zurücksetzen?
Zu-/Abschläge mit **Bei Freigabe** sind an die Freigabe gekoppelt. Beim **Status zurücksetzen** entfernt das System die automatisch erzeugten Zeilen wieder, damit eine erneute Freigabe die dann gültige Konfiguration (z. B. geänderte Preise) anwendet. Bereits gelieferte oder fakturierte Zeilen bleiben erhalten.

### 8. Welche Zuweisung wird gewählt, wenn mehrere passen?
Das Modul sucht in fester Reihenfolge: **Artikel + Debitor/Kreditor**, dann **Alle Artikel + Debitor/Kreditor**, dann **Artikel + Alle Debitoren/Alle Kreditoren**, zuletzt **Alle Artikel + Alle Debitoren/Alle Kreditoren**. Zusätzlich muss der **Berechnungszeitpunkt** in den Gültigkeitszeitraum (Start-/Enddatum) fallen. So haben speziellere Konditionen Vorrang.

### 9. Warum unterscheidet sich der berechnete Betrag zwischen Auftrag und Rechnung?
Der **Berechnungszeitpunkt** legt fest, welches Datum die Preisfindung heranzieht (Arbeits-, Buchungs-, Auftrags-/Bestell- oder Lieferdatum). Bei **Preisart = Prozentsatz** hängt der Betrag zudem von der Bezugsgröße ab (Belegbetrag, Zeilenbetrag oder Einzelpreis), die sich zwischen den Belegen ändern kann.

### 10. Warum wird der Zu-/Abschlag nur anteilig gebucht?
Maßgeblich sind **Menge/Pauschal zu liefern** bzw. **Bezugsgröße Beleg zu liefern**. Bei **Jede Lieferung** wird der Zu-/Abschlag anteilig zur gelieferten Menge berechnet; bei **Erste/Letzte Lieferung (komplett)** vollständig zur ersten bzw. letzten Lieferung. Der volle Betrag entsteht daher erst, wenn die maßgebliche Lieferung gebucht ist.

## Typische Anwendungsfälle

### Anwendungsfall 1 – Frachtpauschale automatisch bei Auftragsfreigabe

**Auslöser.** Der Vertrieb erfasst einen Standardauftrag; laut Konditionsvereinbarung fällt pro Auftrag eine Frachtpauschale an, die nicht vergessen werden darf.

**Einstieg in BC.** Der Administrator hat den Zu-/Abschlag „Fracht“ auf **Artikel Zu-/Abschläge** mit **Bezugsgröße = Pauschal Gesamt** und **Automatisch in Beleg übernehmen = Bei Freigabe** angelegt und über **Zu-/Abschlagsmanagement → Zu-/Abschlagszuweisungen** einen Preis für den Debitor hinterlegt.

**Kernablauf.**
1. Anwender öffnet den **Verkaufsauftrag** und erfasst die Artikelzeile.
2. Anwender wählt **Freigeben**.
3. Das System erzeugt automatisch die Zu-/Abschlagszeile „Fracht“ und ordnet sie der Artikelzeile zu.

**Abschluss.** Der Auftrag wird im Standard weiterverarbeitet und **gebucht**. Setzt der Anwender den **Status zurück**, wird die Frachtzeile entfernt und bei erneuter Freigabe neu gebildet.

### Anwendungsfall 2 – Mindermengenzuschlag erst in der Verkaufsrechnung (Spezifische Zuweisung)

**Auslöser.** Der Verkaufspreis steht erst in der Verkaufsrechnung fest (Kalkulation). Ein Mindermengenzuschlag soll die Restbeträge bis zu einem Mindestwert auffüllen – jedoch ausschließlich in der Rechnung, nicht im Angebot oder Auftrag.

**Einstieg in BC.** Der Key-User pflegt in der **Zu-/Abschlagszuweisung** eine Zeile mit **Mindestbezugsart = Belegbetrag**, **Mindestwert** und **Differenz auffüllen = aktiv**, setzt **Spezifische Zuweisung** auf **Spezifische Zuweisung** und hinterlegt unter **Spezifische Zuweisungen** die Belegklasse **VK-Rechnung**.

**Kernablauf.**
1. Anwender erstellt die **Verkaufsrechnung** (ggf. über Lieferzeilen aus einem gebuchten Warenausgang).
2. In der Rechnungszeile wählt der Anwender **Zeile → Funktionen → Vorgeschlagene Zu-/Abschläge** bzw. **Zu-/Abschläge hinzufügen**.
3. Das System bietet den Zuschlag an, da eine **Spezifische Zuweisung** für **VK-Rechnung** existiert, und füllt den Belegbetrag bis zum **Mindestwert** auf.

**Abschluss.** Der Anwender wählt **Freigeben** und **Buchen**; die aufgefüllte Zu-/Abschlagszeile erscheint in der gebuchten Verkaufsrechnung.

### Anwendungsfall 3 – Zusatzkosten manuell in einer Bestellung ergänzen

**Auslöser.** Ein Lieferant kündigt telefonisch einen einmaligen Verpackungszuschlag an, der in der laufenden Bestellung berücksichtigt werden soll.

**Einstieg in BC.** Der Zu-/Abschlag ist auf **Artikel Zu-/Abschläge** mit **In Belegzeile auswählbar = aktiv** und einer **Zu-/Abschlagszuweisung** für den Kreditor angelegt.

**Kernablauf.**
1. Anwender öffnet die **Bestellung** und markiert die Artikelzeile (Typ **Artikel**).
2. Anwender wählt **Zeile → Funktionen → Zu-/Abschläge hinzufügen** (Alt+Z).
3. In der Liste **Zu-/Abschläge** wählt der Anwender den Verpackungszuschlag und bestätigt mit **OK**; das System legt die Zu-/Abschlagszeile an und ordnet sie der Artikelzeile zu.

**Abschluss.** Die Bestellung wird **freigegeben** und nach Wareneingang **gebucht**; der manuell ergänzte Zu-/Abschlag wird entsprechend der EK-Lieferzeitpunkte zugeordnet.
