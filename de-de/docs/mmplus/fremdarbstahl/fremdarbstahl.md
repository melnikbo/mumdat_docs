---
title: Anwenderhandbuch m+m Subcontracting Steel
---

# Anwenderhandbuch m+m Subcontracting Steel

## Einleitung

Die Erweiterung **m+m Subcontracting Steel** ergänzt das Modul **m+m Subcontracting** (Fremdarbeitenauftrag) um Funktionen für die Stahlindustrie. Sie fügt dem bestehenden Fremdarbeitenauftrag drei Bausteine hinzu:

- die **mengengerechte Erfassung in KG, Meter und Stück** auf Gruppenzeilen, Auftragszeilen und Auftragsposten – parallel zur Standardmenge und in jeder Buchungsstufe (Ausgang, Eingang, zu fakturieren, fakturiert),
- die **Erfassung und Buchung von Schrottmengen** auf der Gruppenzeile, die beim Eingang anteilig auf die zugehörigen Fertigungsaufträge verteilt wird,
- die **Verzahnung mit dem FA-Arbeitsvorrat** (automatisches Beenden bei Eingang) und mit der **Versandplanung** (Liefertouren am Kopf, Fremdarbeitenaufträge in der Versandplanung).

Die Erweiterung bringt **keine eigenen Seiten** mit. Sämtliche Felder und Aktionen erscheinen auf den vorhandenen Seiten des Fremdarbeitenauftrags sowie auf der Versandplanung. Der Anwender arbeitet also weiter mit den gewohnten Belegen; dieses Handbuch beschreibt, **welche zusätzlichen Felder und Aktionen** dort hinzukommen und **wie sie den Tagesablauf steuern**.

**Zielgruppe.** Primär richtet sich das Handbuch an **operative Anwender**, die täglich mit dem Fremdarbeitenauftrag arbeiten: Sie erfassen Gruppen- und Auftragszeilen, buchen Ausgang und Eingang, tragen Schrottmengen ein, fakturieren und planen den Versand. Sekundär angesprochen sind **Administratoren und Key-User**, die die Einrichtung (globale Einrichtungskennzeichen, Mengenumrechnung, Liefertouren, Berechtigungen) vornehmen.

**Kurzer Prozessüberblick.** Der Anwender legt einen **Fremdarbeitenauftrag** an bzw. lässt ihn aus einem Fertigungs- oder Verkaufsprozess erzeugen. Auf den **Gruppenzeilen** erfasst er neben der Menge die Werte in **KG**, **Meter** und **Stück**, optional per **Matchcode**/**Materialsuche starten**. Er bucht den **Ausgang** an den Lohnbetrieb, später den **Eingang** zurück; beim Eingang werden **Schrottmengen** anteilig verbucht und – bei aktiver Einrichtung – die zugehörigen **FA-Arbeitsvorrat**-Zeilen automatisch beendet. Anschließend wird **fakturiert**. Für die physische Logistik lassen sich die offenen Fremdarbeitenaufträge in der **Versandplanung** einplanen.

---

## Schnellstart für Anwender

Die folgenden Schritte führen in Abhängigkeitsreihenfolge (zuerst Einrichtung, dann Beleg, dann Buchung) zum Ergebnis. Details stehen in den jeweiligen Kapiteln.

1. **Einrichtung prüfen (einmalig, Administrator).** Öffnen Sie **Fremdarbeitenauftrag Einrichtung** und legen Sie fest, ob **FA-Arbeitsvorrat beenden bei Eingang** aktiviert sein soll. Stellen Sie sicher, dass die Mengenumrechnung (KG/Meter/Stück) und – falls die Versandplanung genutzt wird – die **Liefertouren** eingerichtet sind (siehe Kapitel **Einrichtung**).
2. **Fremdarbeitenauftrag öffnen.** Wählen Sie den gewünschten **Fremdarbeitenauftrag** und wechseln Sie auf die **Fremdarbeitenauftraggruppenzeilen**.
3. **Menge und Einheiten erfassen.** Tragen Sie in der Gruppenzeile **Menge** ein; die Felder **KG**, **Meter** und **Stück** werden über die Mengenumrechnung des Artikels gefüllt bzw. können manuell überschrieben werden. Alternativ wählen Sie **Materialsuche starten** oder erfassen einen **Matchcode**, um Artikel und Erfassungsmengen zu übernehmen.
4. **Ausgang buchen.** Buchen Sie den Ausgang an den Lohnbetrieb. Die Werte in **Ausgang KG/Meter/Stück** fließen in **Geb. Ausgang KG/Meter/Stück**.
5. **Schrottmenge erfassen (falls Verschnitt anfällt).** Tragen Sie vor dem Eingang die **Schrottmenge** in der Gruppenzeile ein.
6. **Eingang buchen.** Buchen Sie den Rücklauf. Dabei werden **Eingang KG/Meter/Stück** in **Geb. Eingang KG/Meter/Stück** fortgeschrieben, die **Schrottmenge** anteilig auf die Fertigungsaufträge gebucht (**Geb. Schrottmenge**) und – bei aktiver Einrichtung – die passenden **FA-Arbeitsvorrat**-Zeilen automatisch beendet.
7. **Fakturieren.** Fakturieren Sie die Gruppenzeilen; **KG/Meter/Stück zu fakturieren** werden nach **KG/Meter/Stück fakturiert** übernommen.
8. **Versand planen (optional).** Öffnen Sie die **Versandplanung** und wählen Sie die Aktion **Fremdarbeitenaufträge**, um offene Aus- und Eingänge der Fremdarbeitenaufträge einzuplanen.

---

## Einrichtung

Die Einrichtung dieser Erweiterung umfasst ein globales Kennzeichen auf der Belegeinrichtung sowie mehrere **Voraussetzungen in abhängigen Modulen** (Mengenumrechnung, Materialsuche, Liefertouren), die aktiv sein müssen, damit die stahlspezifischen Felder und Aktionen im Tagesablauf greifen. Alle Angaben stammen aus dem Programmcode dieser Erweiterung.

### Fremdarbeitenauftrag Einrichtung – FA-Arbeitsvorrat

Diese Einrichtung wird vom **Administrator** einmalig je Mandant vorgenommen. Sie steuert, ob der Abschluss der externen Arbeitsgänge im **FA-Arbeitsvorrat** automatisch beim Rücklauf erfolgt.

**Einstieg:** Öffnen Sie die zentrale Seite **Fremdarbeitenauftrag Einrichtung** (mandantenweite Einrichtungskarte des Fremdarbeiten-Moduls). Da es sich um eine mandantenweite Einzelsatz-Einrichtung ohne übergeordnete Liste handelt, erfolgt der Zugriff über die Einrichtung des Fremdarbeiten-Moduls bzw. über **Suchen**.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **FA-Arbeitsvorrat beenden bei Eingang** | Wenn aktiviert, werden beim Buchen des **Eingangs** einer Gruppenzeile die zum Arbeitsgang gehörenden Zeilen im **FA-Arbeitsvorrat** automatisch auf **beendet** gesetzt. Der Anwender muss den Arbeitsgang also nicht zusätzlich im FA-Arbeitsvorrat manuell abschließen. Wenn deaktiviert, bleibt der FA-Arbeitsvorrat unverändert und der Abschluss der Arbeitsgänge muss dort separat erfolgen. Das automatische Beenden setzt das abhängige Modul *m+m Production Order Job Overview* voraus. |

#### FA-Arbeitsvorrat beenden bei Eingang einrichten

Diese Prozesskette verbindet eine globale Einstellung mit einer Aktion im Tagesablauf. Sie wird vom **Administrator** vor der ersten Nutzung konfiguriert und im Kapitel **Tägliche Arbeit** (Eingang buchen) wirksam.

1. **Voraussetzung schaffen.** Stellen Sie sicher, dass das Modul **FA-Arbeitsvorrat** (m+m Production Order Job Overview) installiert ist und die externen Arbeitsgänge der betroffenen Fertigungsaufträge dort geführt werden. Wenn diese Voraussetzung fehlt, kann beim Eingang kein Arbeitsgang beendet werden.
2. **Globales Kennzeichen setzen.** Aktivieren Sie in **Fremdarbeitenauftrag Einrichtung** das Kennzeichen **FA-Arbeitsvorrat beenden bei Eingang**. Wenn gesetzt, verbindet das System jede Eingangsbuchung mit dem passenden Arbeitsplatz, dem Fertigungsauftrag und dem Arbeitsgang und markiert die gefundenen FA-Arbeitsvorrat-Zeilen als beendet.
3. **Abschluss im Tagesablauf.** Der operative Anwender bucht später den **Eingang** der Gruppenzeile (siehe **Tägliche Arbeit**). Mit dieser Buchung ist die Kette geschlossen: Der externe Arbeitsgang gilt als abgeschlossen, ohne dass der Anwender den FA-Arbeitsvorrat gesondert öffnen muss.

### Mengenumrechnung für Fremdarbeitenaufträge einrichten

Die stahlspezifischen Mengenfelder **KG**, **Meter** und **Stück** werden nicht frei erfasst, sondern über die **Mengenumrechnung** aus den Artikelstammdaten abgeleitet. Diese Einrichtung liegt im abhängigen Modul *m+m Unit Conversion* und ist Voraussetzung dafür, dass die Felder in Gruppen- und Auftragszeilen automatisch gefüllt werden.

Konfiguriert wird dies durch den **Administrator/Key-User** vor der ersten Nutzung; angewendet werden die Werte im Kapitel **Tägliche Arbeit** bei der Zeilenerfassung.

1. **Einheiten der Umrechnung festlegen.** Hinterlegen Sie in der Einrichtung der Mengenumrechnung, welche Maßeinheiten als **KG-**, **Meter-** und **Stück-Einheit** gelten. Wenn diese Einheiten gesetzt sind, erkennt das System beim Artikelwechsel die passende Ausgangsgröße und rechnet die übrigen Größen um.
2. **Theoretische Umrechnungswerte am Artikel pflegen.** Tragen Sie am Artikel die theoretischen Umrechnungswerte (KG je Meter, KG je Stück) ein. Wenn gepflegt, werden aus einer erfassten **Menge** automatisch **KG**, **Meter** und **Stück** berechnet; fehlen die Werte, bleiben die abgeleiteten Größen leer und müssen manuell erfasst werden.
3. **Anwendung im Tagesablauf.** Sobald der Anwender in der Gruppenzeile **Menge**, **KG**, **Meter** oder **Stück** ändert oder den **Artikelnr.** wechselt, rechnet das System die übrigen Mengenfelder konsistent nach (siehe **Tägliche Arbeit**). So bleiben Menge und stahltypische Einheiten in allen Buchungsstufen synchron.

> Hinweis zur Materialsuche: Über den **Matchcode** und die Aktion **Materialsuche starten** in den Gruppenzeilen wird die **Artikelsuche** des Moduls *m+m Material Properties* aufgerufen. Deren Einrichtung erfolgt vollständig in diesem abhängigen Modul; diese Erweiterung bindet lediglich die Suche in die Gruppenzeile ein und übernimmt Artikel, Variante, Einheit sowie die **Erfassungsmenge** in KG/Meter/Stück.

### Versandplanung für Fremdarbeitenaufträge einrichten

Damit offene Fremdarbeitenaufträge in der **Versandplanung** erscheinen und Liefertouren zugeordnet werden können, müssen die Liefertouren des Moduls *m+m Logistic Management* eingerichtet sein.

Konfiguriert durch den **Administrator/Disponenten**; genutzt wird das Ergebnis in den Kapiteln **Tägliche Arbeit** (Kopffelder) und **Versandplanung**.

1. **Liefertouren anlegen.** Pflegen Sie die **Liefertour**-Stammdaten (mit Zusteller und Zustellerleistung). Wenn Liefertouren vorhanden sind, können sie am Fremdarbeitenauftrag als **Ausgeh. Liefertourcode** und **Eingeh. Liefertourcode** ausgewählt werden.
2. **Liefertouren am Beleg zuordnen.** Der Anwender wählt im Fremdarbeitenauftrag die Tourcodes (siehe **Tägliche Arbeit**). Wenn gesetzt, übernimmt das System aus der Tour den Zusteller und die Zustellerleistung in die entsprechenden Ausgangs- bzw. Eingangs-Zustellerfelder des Belegs.
3. **Einplanung in der Versandplanung.** In der **Versandplanung** ruft der Disponent die Aktion **Fremdarbeitenaufträge** auf. Wenn ausgeführt, sammelt das System alle freigegebenen bzw. in Bearbeitung befindlichen Fremdarbeitenaufträge mit offener Aus- bzw. Eingangsmenge und stellt sie zur Tourenplanung bereit (siehe Kapitel **Versandplanung**).

### Berechtigungen

Die Erweiterung liefert einen Berechtigungssatz (**MuM FOST Permission**), der die Zugriffsrechte auf die zusätzlichen Tabellenfelder und die neue Logik bündelt. Der Administrator ordnet diesen Berechtigungssatz den Benutzern oder Benutzergruppen zu, die mit Fremdarbeitenaufträgen arbeiten. Der Berechtigungssatz bestimmt die Berechtigungen für die stahlspezifischen Erweiterungsfelder und ergänzt die Berechtigungen des Basismoduls; er legt fest, welche Aktionen die Benutzer auf den erweiterten Feldern ausführen dürfen.

---

## Tägliche Arbeit am Fremdarbeitenauftrag

Der Fremdarbeitenauftrag ist der zentrale Beleg dieser Erweiterung. Die stahlspezifischen Felder verteilen sich auf **Belegkopf**, **Gruppenzeilen**, **Auftragszeilen** und die **Belegübersicht**. Die eigentliche Buchungslogik (Ausgang, Eingang, Fakturierung) stellt das Basismodul bereit; die Erweiterung ergänzt jede Stufe um die Werte in KG/Meter/Stück und um die Schrottmenge.

**Steuernde Einrichtung:** Das Verhalten dieses Belegs wird durch die Seite **Fremdarbeitenauftrag Einrichtung** (Kennzeichen **FA-Arbeitsvorrat beenden bei Eingang**), durch die **Mengenumrechnung** (KG/Meter/Stück-Ableitung, siehe Einrichtung) sowie durch die **Liefertour**-Stammdaten gesteuert. Bevor Sie hier arbeiten, sollten diese Einrichtungen abgeschlossen sein.

### Belegkopf – Liefertouren und Versandplanung

Der Belegkopf des Fremdarbeitenauftrags erhält Felder für die Tourensteuerung und Zähler zur Versandplanung. Fachlich schließen sie an die Standardfelder **Ziellagerortcode Ausgang/Eingang** an und liegen auf dem Register **Aus- & Eingang**.

| Feld | Erläuterung |
|------|-------------|
| **Ausgeh. Liefertourcode** | Wenn ein Liefertourcode für den Ausgang gesetzt wird, übernimmt das System aus der zugehörigen **Liefertour** den Zusteller und die Zustellerleistung in die Ausgangs-Zustellerfelder des Belegs; zudem wird der Beleg beim Sammeln in der Versandplanung dieser Tour zugeordnet. Ohne Eintrag bleibt der Ausgang tourneutral. |
| **Eingeh. Liefertourcode** | Wenn ein Liefertourcode für den Eingang gesetzt wird, übernimmt das System analog Zusteller und Zustellerleistung in die Eingangs-Zustellerfelder und ordnet den Eingang dieser Tour in der Versandplanung zu. Ohne Eintrag bleibt der Eingang tourneutral. |
| **Versandplanungszeilen** | Zeigt die Anzahl der noch offenen (nicht registrierten) Versandplanungszeilen zu diesem Fremdarbeitenauftrag an. Wenn der Wert größer als 0 ist, existiert bereits eine Einplanung, die noch nicht registriert wurde – ein Hinweis darauf, dass der Versand vorbereitet, aber noch nicht abgeschlossen ist. |
| **Reg. Versandplanungszeilen** | Zeigt die Anzahl der bereits **registrierten** Versandplanungszeilen zu diesem Fremdarbeitenauftrag an. Wenn der Wert größer als 0 ist, wurde der Versand für diesen Beleg bereits fest eingeplant. |

### Belegübersicht (Fremdarbeitenauftragsliste)

In der Übersicht der Fremdarbeitenaufträge stehen zusätzlich die Versandplanungs-Kennzahlen zur Verfügung, sodass der Disponent den Planungsstand je Beleg erkennt, ohne den Beleg zu öffnen.

| Feld | Erläuterung |
|------|-------------|
| **Ausgeh. Liefertourcode** | Ausgehender Liefertourcode des Belegs. Die Spalte wird standardmäßig ausgeblendet ausgeliefert und kann bei Bedarf über die Personalisierung eingeblendet werden; eingeblendet zeigt sie, welcher Tour der Ausgang zugeordnet ist. |
| **Eingeh. Liefertourcode** | Eingehender Liefertourcode des Belegs. Ebenfalls standardmäßig ausgeblendet; eingeblendet zeigt sie die Tourzuordnung des Eingangs. |
| **Versandplanungszeilen** | Anzahl offener Versandplanungszeilen des Belegs. Wenn größer als 0, ist eine Einplanung vorbereitet, aber noch nicht registriert. |
| **Reg. Versandplanungszeilen** | Anzahl registrierter Versandplanungszeilen des Belegs. Wenn größer als 0, ist der Versand fest eingeplant. |

### Fremdarbeitenauftraggruppenzeilen

Die Gruppenzeile ist die zentrale Arbeitsebene: Hier erfasst der Anwender Menge und Einheiten, startet die Materialsuche und trägt die Schrottmenge ein. Die stahlspezifischen Mengenfelder begleiten jede Buchungsstufe der Basismenge (Ausgang, Eingang, zu fakturieren, fakturiert) und werden – bis auf **Schrottmenge** und **Matchcode** – über die Mengenumrechnung konsistent gehalten.

#### Materialsuche und Matchcode

| Feld / Aktion | Erläuterung |
|---------------|-------------|
| **Matchcode** | Wenn ein Matchcode eingetragen wird, öffnet das System die **Artikelsuche** (Material Properties) mit diesem Matchcode als Filter und übernimmt den ausgewählten Artikel samt Variante, Einheit und Erfassungsmenge in die Zeile. Wird der **Artikelnr.** anschließend geleert, wird auch der Matchcode entfernt, damit Zeile und Matchcode konsistent bleiben. |
| **Materialsuche starten** (Aktion) | Öffnet die **Artikelsuche** ohne vorherigen Matchcode. Wenn der Anwender einen Treffer übernimmt, füllt das System Artikelnr., Variantencode, Einheitencode, Matchcode sowie **KG**, **Meter**, **Stück** aus der Erfassung und validiert die **Menge**. So lässt sich per Suche statt per Direkteingabe eine Gruppenzeile befüllen. |

#### Mengen in KG, Meter und Stück

Die folgenden Felder stehen für jede Buchungsstufe zur Verfügung. Sie sind über die Mengenumrechnung mit der jeweiligen Basismenge (Menge, Ausgangsmenge, Eingangsmenge, Menge zu fakturieren) verknüpft.

| Feld | Erläuterung |
|------|-------------|
| **KG** | Gewicht der geplanten Gruppenzeilenmenge in Kilogramm. Wenn der Anwender KG ändert, rechnet das System **Meter** und **Stück** sowie die Basis-**Menge** entsprechend der Artikel-Umrechnung nach; so ist die Zeile wahlweise gewichts-, längen- oder stückgeführt erfassbar. |
| **Meter** | Länge der Gruppenzeilenmenge in Metern. Wenn geändert, werden KG, Stück und Menge konsistent nachgerechnet. |
| **Stück** | Stückzahl der Gruppenzeilenmenge. Wenn geändert, werden KG, Meter und Menge konsistent nachgerechnet. |
| **Ausgang KG** / **Ausgang Meter** / **Ausgang Stück** | Noch zu buchende Ausgangsmenge in KG/Meter/Stück. Wenn die Basis-**Ausgangsmenge** geändert wird, werden diese Werte automatisch mitgeführt; sie geben an, welches Gewicht bzw. welche Länge/Stückzahl beim nächsten Ausgang an den Lohnbetrieb geht. |
| **Geb. Ausgang KG** / **Geb. Ausgang Meter** / **Geb. Ausgang Stück** | Bereits an den Lohnbetrieb ausgelieferte Menge in KG/Meter/Stück. Diese Werte werden mit jeder Ausgangsbuchung erhöht und sind nicht editierbar; sie dokumentieren den kumulierten Materialabgang. |
| **Eingang KG** / **Eingang Meter** / **Eingang Stück** | Noch zu buchende Eingangsmenge in KG/Meter/Stück (Rücklauf vom Lohnbetrieb). Wenn die Basis-**Eingangsmenge** geändert wird, werden diese Werte mitgeführt. Übersteigt der gebuchte Ausgang den gebuchten Eingang, schlägt das System die Differenz automatisch als offene Eingangsmenge vor. |
| **Geb. Eingang KG** / **Geb. Eingang Meter** / **Geb. Eingang Stück** | Bereits zurückgemeldete (gebuchte) Eingangsmenge in KG/Meter/Stück. Wird mit jeder Eingangsbuchung erhöht und ist nicht editierbar; dokumentiert den kumulierten Rücklauf. |
| **KG zu fakturieren** / **Meter zu fakturieren** / **Stück zu fakturieren** | Noch zu fakturierende Menge in KG/Meter/Stück. Wenn die Basis-**Menge zu fakturieren** geändert wird, werden diese Werte nachgerechnet; sie bestimmen, welches Gewicht/welche Länge in die nächste Fakturierung eingeht. |
| **KG fakturiert** / **Meter fakturiert** / **Stück fakturiert** | Bereits fakturierte Menge in KG/Meter/Stück. Wird mit jeder Fakturierung erhöht und ist nicht editierbar. |

#### Schrottmenge

| Feld | Erläuterung |
|------|-------------|
| **Schrottmenge** | Menge des beim externen Arbeitsgang angefallenen Verschnitts/Schrotts, die der Anwender vor dem Eingang erfasst. Wenn ein Wert erfasst und der **Eingang** gebucht wird, verteilt das System die noch nicht gebuchte Schrottmenge (**Schrottmenge − Geb. Schrottmenge**) anteilig nach Zeilenmenge auf die Fertigungsaufträge der zugehörigen Auftragszeilen und schreibt sie in **Geb. Schrottmenge** fort. Ist der Wert 0 oder bereits vollständig gebucht, erfolgt keine Schrottbuchung. |
| **Geb. Schrottmenge** | Bereits gebuchte Schrottmenge. Wird bei der Eingangsbuchung um die verteilte Schrottmenge erhöht und ist nicht editierbar; zeigt an, wie viel Schrott bereits den Fertigungsaufträgen zugerechnet wurde. |

> Buchungsreihenfolge (aus dem Programmcode): Beim **Ausgang buchen** werden die Ausgangs-Einheiten in die gebuchten Ausgangs-Einheiten übernommen. Beim **Eingang buchen** werden zuerst die Eingangs-Einheiten in die gebuchten Eingangs-Einheiten übernommen, anschließend die **Schrottmenge** anteilig gebucht und – bei aktiver Einrichtung **FA-Arbeitsvorrat beenden bei Eingang** – die passenden FA-Arbeitsvorrat-Zeilen beendet. Beim **Fakturieren** werden die Einheiten „zu fakturieren“ nach „fakturiert“ fortgeschrieben. Teilbuchungen sind zulässig; der Beleg muss nicht in einem Zug vollständig gebucht werden.

### Fremdarbeitenauftragsgruppenzeilen – Listenansicht (group list)

Die Listenansicht der Gruppenzeilen zeigt dieselben Mengenfelder in KG/Meter/Stück wie die Zeilenansicht (Menge, Ausgang, Geb. Ausgang, Eingang, Geb. Eingang, zu fakturieren, fakturiert) sowie **Schrottmenge** und **Geb. Schrottmenge**. Die Spalten dienen dem schnellen Überblick über den Bearbeitungsstand mehrerer Zeilen und aktualisieren sich mit den jeweiligen Buchungen. Matchcode und die Aktion **Materialsuche starten** stehen in dieser Listenansicht nicht zur Verfügung; sie sind der detaillierten Zeilenansicht vorbehalten.

### Auftragszeilen

Auf den **Auftragszeilen** des Fremdarbeitenauftrags werden ergänzend die Einheiten **KG**, **Meter** und **Stück** der Zeilenmenge geführt.

| Feld | Erläuterung |
|------|-------------|
| **KG** | Gewicht der Auftragszeilenmenge in Kilogramm. Wenn der Wert erfasst oder aus dem Herkunftsbeleg (Fertigungsauftrag, Verkaufszeile, Artikelposten) übernommen wird, rechnet das System Meter, Stück und Menge der Zeile konsistent nach. |
| **Meter** | Länge der Auftragszeilenmenge in Metern; konsistent mit KG, Stück und Menge. |
| **Stück** | Stückzahl der Auftragszeilenmenge; konsistent mit KG, Meter und Menge. |

Die Werte der Auftragszeilen werden beim Anlegen aus dem jeweiligen Herkunftsbeleg gefüllt und in die zugehörige Gruppenzeile summiert; so bleiben Kopf-, Gruppen- und Zeilenebene mengengerecht abgestimmt.

---

## Versandplanung

Die Versandplanung (Modul *m+m Logistic Management*) bündelt zu planende Aus- und Eingänge verschiedener Belegarten. Diese Erweiterung macht **Fremdarbeitenaufträge** als eigene Quellart in der Versandplanung verfügbar.

**Steuernde Einrichtung:** Voraussetzung sind eingerichtete **Liefertouren** und am Beleg gesetzte **Ausgeh./Eingeh. Liefertourcodes** (siehe **Einrichtung** und **Tägliche Arbeit**).

### Fremdarbeitenaufträge in die Planung übernehmen

**Einstieg:** Öffnen Sie die **Versandplanung** und wählen Sie die Aktion **Fremdarbeitenaufträge**.

Wenn die Aktion ausgeführt wird, sammelt das System alle Fremdarbeitenaufträge mit Status **Freigegeben** oder **In Bearbeitung** und stellt je Gruppenzeile eine Planungszeile bereit – sowohl für den **Ausgang** (Weg zum Lohnbetrieb) als auch für den **Eingang** (Rücklauf). Berücksichtigt werden nur Zeilen mit noch offener Menge:

- für den **Ausgang**, solange die Menge größer als die gebuchte Ausgangsmenge ist,
- für den **Eingang**, solange die Menge größer als die gebuchten Eingangsmenge ist,
- und nur, sofern noch keine Planungszeile zu dieser Quelle/Richtung existiert.

Die Planungszeilen tragen die offenen Mengen in **KG**, **Meter** und **Stück** sowie das Netto-/Bruttogewicht (aus den offenen KG). Als Lieferadresse wird beim Ausgang die Anlieferadresse des Belegs, beim Eingang die Adresse des Ziellagerorts (**Ziellagerortcode Eingang**) verwendet; als Termin dienen **Ausgangsdatum** bzw. **Eingangsdatum**, als Tour der jeweilige **Ausgeh./Eingeh. Liefertourcode**.

### Richtung der Planungszeile

Auf der Gruppenzeile steuert das (systemseitig gesetzte, nicht editierbare) Feld **Versandplanung Richtung**, für welche Transportrichtung eine Planungszeile erzeugt wird:

- **(leer):** Für die Zeile ist noch keine Richtung bestimmt; sie wird beim Sammeln je nach offener Aus-/Eingangsmenge einer Richtung zugeordnet.
- **Ausgehend:** Die Planungszeile betrifft den **Ausgang** an den Lohnbetrieb; als Menge dient die offene Ausgangsmenge, als Adresse die Anlieferadresse des Belegs.
- **Eingehend:** Die Planungszeile betrifft den **Eingang** (Rücklauf); als Menge dient die offene Eingangsmenge, als Adresse der Ziellagerort des Eingangs.

### Von der Versandplanung zum Beleg zurück

Aus der Versandplanung heraus lassen sich die zugrunde liegenden Fremdarbeitenaufträge direkt aufrufen: Über die Belegauswahl der Versandplanung wird für die Quellart **Fremdarbeitenauftrag** die **Belegübersicht der Fremdarbeitenaufträge** geöffnet; aus einer einzelnen Planungszeile wird der zugehörige **Fremdarbeitenauftrag** angezeigt. So wechselt der Disponent ohne Umweg zwischen Planung und Beleg.

---

## Historie: Fremdarbeitenauftragsposten

Gebuchte Vorgänge werden im Basismodul als **Fremdarbeitenauftragsposten** geführt. Diese Erweiterung ergänzt die Posten um die Einheiten der jeweiligen Buchung, damit der gebuchte Materialfluss auch mengengerecht nachvollziehbar ist.

| Feld | Erläuterung |
|------|-------------|
| **KG** | Gewicht der gebuchten Menge dieses Postens in Kilogramm. Der Wert wird bei Ausgang, Eingang bzw. Fakturierung aus der jeweils gebuchten Einheit der Gruppenzeile in den Posten übernommen und dokumentiert den mengengerechten Buchungsverlauf. |
| **Meter** | Länge der gebuchten Menge dieses Postens in Metern; analog aus der Buchung übernommen. |
| **Stück** | Stückzahl der gebuchten Menge dieses Postens; analog aus der Buchung übernommen. |

Über die Posten lässt sich je Buchung (Ausgang, Eingang, Fakturierung) nachvollziehen, welches Gewicht, welche Länge und welche Stückzahl bewegt wurden – ergänzend zur Standard-Postenmenge.

---

## FAQ und Troubleshooting

### 1. Warum werden KG, Meter und Stück nach dem Erfassen der Menge automatisch gefüllt?
Weil die stahlspezifischen Mengenfelder über die **Mengenumrechnung** (Modul *m+m Unit Conversion*) mit der Basismenge verknüpft sind. Ändern Sie **Menge**, **KG**, **Meter** oder **Stück**, rechnet das System die jeweils anderen Größen aus den Artikel-Umrechnungswerten (KG je Meter, KG je Stück) nach. Sie können jede der Größen als Leitgröße verwenden.

### 2. Was passiert, wenn am Artikel keine Umrechnungswerte hinterlegt sind?
Dann können KG/Meter/Stück nicht automatisch aus der Menge abgeleitet werden und bleiben leer bzw. müssen manuell erfasst werden. Pflegen Sie die theoretischen Umrechnungswerte am Artikel, damit die Ableitung funktioniert (siehe **Mengenumrechnung für Fremdarbeitenaufträge einrichten**).

### 3. Warum ändert sich der Matchcode, wenn ich den Artikel entferne?
Beim Leeren des Feldes **Artikelnr.** wird der **Matchcode** der Gruppenzeile automatisch zurückgesetzt. Das verhindert, dass ein Matchcode ohne zugehörigen Artikel stehen bleibt und bei der nächsten Suche irreführt.

### 4. Wie fülle ich eine Gruppenzeile schneller als per Direkteingabe?
Nutzen Sie die Aktion **Materialsuche starten** oder tragen Sie einen **Matchcode** ein. Beides öffnet die **Artikelsuche**; mit der Übernahme eines Treffers werden Artikelnr., Variantencode, Einheitencode, Matchcode sowie KG/Meter/Stück und die Menge in die Zeile übernommen.

### 5. Wann wird die Schrottmenge tatsächlich gebucht?
Erst beim **Eingang buchen**. Das System bucht die noch offene Schrottmenge (**Schrottmenge − Geb. Schrottmenge**) und verteilt sie anteilig nach Zeilenmenge auf die Fertigungsaufträge der Auftragszeilen. Vor der Eingangsbuchung ist die Schrottmenge nur erfasst, aber nicht gebucht.

### 6. Warum ist meine erfasste Schrottmenge beim Eingang nicht gebucht worden?
Weil die noch offene Schrottmenge 0 oder negativ ist – etwa wenn **Geb. Schrottmenge** bereits die erfasste **Schrottmenge** erreicht. Das System bucht nur eine positive Restmenge; ist keine offen, unterbleibt die Schrottbuchung.

### 7. Muss ich den externen Arbeitsgang im FA-Arbeitsvorrat noch manuell beenden?
Nur wenn das Kennzeichen **FA-Arbeitsvorrat beenden bei Eingang** in der **Fremdarbeitenauftrag Einrichtung** deaktiviert ist. Ist es aktiviert, beendet das System die passenden FA-Arbeitsvorrat-Zeilen automatisch mit der Eingangsbuchung.

### 8. Warum wird beim Eingang trotz aktiver Einrichtung kein Arbeitsgang beendet?
Der automatische Abschluss setzt das Modul **FA-Arbeitsvorrat** (m+m Production Order Job Overview) voraus und benötigt eine passende Zuordnung von Arbeitsplatz, Fertigungsauftrag, Fertigungsauftragszeile und Arbeitsgang. Findet das System keine passenden FA-Arbeitsvorrat-Zeilen, gibt es nichts zu beenden.

### 9. Warum erscheint ein Fremdarbeitenauftrag nicht in der Versandplanung?
Übernommen werden nur Fremdarbeitenaufträge mit Status **Freigegeben** oder **In Bearbeitung** und nur Gruppenzeilen mit **offener** Aus- bzw. Eingangsmenge, zu denen noch **keine** Planungszeile existiert. Ist die Menge bereits vollständig gebucht oder bereits eingeplant, wird keine neue Planungszeile erzeugt.

### 10. Kann ich Aus- und Eingang eines Fremdarbeitenauftrags getrennt planen und in Teilmengen buchen?
Ja. Ausgang und Eingang werden über das Feld **Versandplanung Richtung** als **Ausgehend** bzw. **Eingehend** getrennt geplant. Buchungen sind in Teilmengen zulässig; die gebuchten Einheiten (Geb. Ausgang/Eingang KG/Meter/Stück) werden dabei fortlaufend erhöht, bis die Menge vollständig ist.

---

## Typische Anwendungsfälle

### Anwendungsfall 1: Stahlprofile extern bearbeiten lassen mit KG-/Meter-Erfassung

**Auslöser.** Ein Fertigungsauftrag enthält einen externen Arbeitsgang; die Stahlprofile sollen zu einem Lohnbetrieb gebracht, dort bearbeitet und zurückgeholt werden. Der zuständige Anwender erhält den Hinweis aus der Fertigung.

**Einstieg in BC.** Der Anwender öffnet den zugehörigen **Fremdarbeitenauftrag** und wechselt auf die **Fremdarbeitenauftraggruppenzeilen**.

**Kernablauf.**
1. In der Gruppenzeile wählt er den Artikel per **Materialsuche starten** (Artikelsuche) oder per **Matchcode**; Artikel, Variante, Einheit und Erfassungsmenge werden übernommen. Alternativ erfasst er **Menge**; **KG**, **Meter** und **Stück** werden über die Mengenumrechnung gefüllt.
2. Er bucht den **Ausgang** an den Lohnbetrieb; **Ausgang KG/Meter/Stück** werden in **Geb. Ausgang KG/Meter/Stück** übernommen.
3. Nach Rücklauf bucht er den **Eingang**; **Eingang KG/Meter/Stück** werden in **Geb. Eingang KG/Meter/Stück** fortgeschrieben.
4. Er fakturiert; **KG/Meter/Stück zu fakturieren** gehen in **KG/Meter/Stück fakturiert** über.

**Abschluss.** Der gebuchte Materialfluss ist in den **Fremdarbeitenauftragsposten** mengengerecht (KG/Meter/Stück) nachvollziehbar.

### Anwendungsfall 2: Rücklauf mit Verschnitt und automatischem Abschluss des Arbeitsgangs

**Auslöser.** Der Lohnbetrieb meldet den Eingang der bearbeiteten Teile und teilt eine angefallene Verschnitt-/Schrottmenge mit.

**Einstieg in BC.** Der Anwender öffnet den **Fremdarbeitenauftrag** und die betreffende **Gruppenzeile**. Voraussetzung: In der **Fremdarbeitenauftrag Einrichtung** ist **FA-Arbeitsvorrat beenden bei Eingang** aktiviert (siehe **Einrichtung**).

**Kernablauf.**
1. Er trägt in der Gruppenzeile die gemeldete **Schrottmenge** ein.
2. Er bucht den **Eingang**. Das System schreibt zuerst die Eingangs-Einheiten fort, verteilt anschließend die offene **Schrottmenge** anteilig nach Zeilenmenge auf die Fertigungsaufträge der Auftragszeilen und erhöht **Geb. Schrottmenge**.
3. Mit derselben Eingangsbuchung setzt das System die passenden **FA-Arbeitsvorrat**-Zeilen automatisch auf **beendet**.

**Abschluss.** Der externe Arbeitsgang gilt als abgeschlossen, der Schrott ist den Fertigungsaufträgen zugerechnet, und der Rücklauf ist als **Fremdarbeitenauftragsposten** dokumentiert – ohne dass der Anwender den FA-Arbeitsvorrat gesondert öffnen musste.
