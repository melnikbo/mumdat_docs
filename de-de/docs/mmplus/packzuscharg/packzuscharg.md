---
title: Anwenderhandbuch m+m Additional Lot Information with Package Management
---

# Anwenderhandbuch m+m Additional Lot Information with Package Management

## Einleitung

Die App **m+m Additional Lot Information with Package Management** verbindet zwei bereits vorhandene m+m-Apps miteinander: **m+m Additional Lot Information** (zusätzliche Chargeninformationen) und **m+m Package Management** (Packmittelverwaltung). Sie sorgt dafür, dass die zu einer Charge hinterlegte **Lieferantenchargennr.** direkt in der Packmittelübersicht **Physische Packmittel** sichtbar wird.

Fachlich löst die App eine einfache, aber im Wareneingang und in der Logistik wichtige Aufgabe: Wer ein physisches Packmittel bearbeitet, sieht auf einen Blick, welche **Lieferantenchargennr.** der darin enthaltenen Charge zugeordnet ist – ohne die Chargennr.-Information des Artikels separat öffnen zu müssen. Die App fügt dazu genau ein zusätzliches, schreibgeschütztes Feld in die Übersicht **Physische Packmittel** ein und liest dessen Wert automatisch aus der Charge.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender** in Wareneingang, Lager und Logistik, die täglich mit physischen Packmitteln und Chargen arbeiten und die Lieferantenchargennr. bei der Bearbeitung benötigen. Sekundär betrifft es Anwender, die im Rahmen der Chargenpflege die **Lieferantenchargennr.** auf der **Chargennr.-Information** erfassen, damit dieser Wert später in der Packmittelübersicht erscheint.

**Kurzer Prozessüberblick:**

1. Beim Wareneingang bzw. bei der Chargenpflege wird auf der **Chargennr.-Information** der Charge die **Lieferantenchargennr.** hinterlegt (dieser Wert stammt aus der App m+m Additional Lot Information).
2. In der Übersicht **Physische Packmittel** zeigt die App diesen Wert je Zeile automatisch in der neuen Spalte **Lieferantenchargennr.** an – passend zu Artikelnr., Variantencode und Chargennr. der Zeile.

**Voraussetzungen:** Die App ist eine Erweiterung (Bridge) und benötigt die installierten Basis-Apps **m+m Package Management** (liefert die Seite **Physische Packmittel**), **m+m Additional Lot Information** (liefert die **Lieferantenchargennr.** auf der Charge) sowie **m+m Cloud Base**. Ohne diese Apps gibt es weder die anzuzeigende Übersicht noch den auszulesenden Wert. Für die Nutzung ist zudem eine gültige **Lizenz** erforderlich: Die App prüft bei der Anmeldung des Anwenders automatisch die Lizenz; ist keine gültige Lizenz vorhanden, steht die Zusatzspalte nicht zur Verfügung. Die vollständige Chargen- und Packmittelpflege ist in den Handbüchern der beiden Basis-Apps beschrieben; dieses Handbuch beschränkt sich auf die Zusatzfunktion, die diese App beisteuert.

## Schnellstart für Anwender

Der schnellste Weg zum Ergebnis – die Lieferantenchargennr. eines Packmittels sehen:

1. **Lieferantenchargennr. an der Charge hinterlegen (Voraussetzung).** Öffnen Sie die **Chargennr.-Information** der betreffenden Charge (über die Artikelkarte bzw. die Artikelverfolgung des Artikels) und tragen Sie im Feld **Lieferantenchargennr.** die Chargennummer des Lieferanten ein. Dieser Schritt ist nur nötig, solange der Wert noch nicht gepflegt ist.
2. **Übersicht öffnen.** Öffnen Sie über die **Suche** in Microsoft Dynamics 365 Business Central die Ansicht **Physische Packmittel**.
3. **Zeile finden.** Suchen bzw. sortieren Sie die gewünschte Packmittelzeile (z. B. über **Artikelnr.**, **Chargennr.** oder **Packmittel Nr.**).
4. **Lieferantenchargennr. ablesen.** In der Spalte **Lieferantenchargennr.** wird der zur Charge hinterlegte Wert automatisch angezeigt. Das Feld ist schreibgeschützt; eine Änderung erfolgt ausschließlich über die **Chargennr.-Information** (siehe Schritt 1).

> Hinweis: Diese App fügt keine eigenen Aktionen oder Buchungen hinzu. Alle Aktionen der Übersicht **Physische Packmittel** (z. B. **Packmittel füllen**, **Artikel umlagern**) stammen aus der Basis-App m+m Package Management und sind dort dokumentiert.

## Datenquelle und Voraussetzungen

Die App zeigt die **Lieferantenchargennr.** nur an – erzeugt oder speichert sie aber nicht selbst. Der Wert entsteht an einer anderen Stelle und wird von dort ausgelesen. Damit die Spalte gefüllt ist, müssen zwei Voraussetzungen erfüllt sein: die Charge muss eine **Lieferantenchargennr.** tragen, und die App-Lizenz muss gültig sein.

### Herkunft des Wertes: Chargennr.-Information

Die **Lieferantenchargennr.** wird auf der **Chargennr.-Information** der jeweiligen Charge gepflegt. Dieses Feld wird von der App **m+m Additional Lot Information** bereitgestellt. Wer die Chargen pflegt (typischerweise im Wareneingang oder in der Qualitätssicherung), trägt dort die vom Lieferanten vergebene Chargennummer ein. Erst danach kann die Packmittelübersicht diesen Wert anzeigen.

Beim Erfassen bzw. Ändern der **Lieferantenchargennr.** auf der Charge gilt:

- Wird ein Wert eingetragen, dann wird dieser als Lieferantencharge zur Charge gespeichert und steht anschließend allen auswertenden Ansichten – auch der Übersicht **Physische Packmittel** – zur Verfügung.
- Wird die **Lieferantenchargennr.** nachträglich geändert und existieren bereits Artikelposten zu dieser Charge, dann erscheint eine Sicherheitsabfrage. Bestätigt der Anwender, wird die geänderte Lieferantenchargennr. konsistent in die betroffenen Posten übernommen; lehnt er ab, bleibt der bisherige Wert erhalten. So bleibt die Rückverfolgbarkeit der Lieferantencharge über alle Buchungen hinweg gewährleistet.

Weitere zur Charge gehörende Angaben aus m+m Additional Lot Information (nur zur Einordnung, wo die Lieferantenchargennr. steht):

| Feld | Erläuterung |
|------|-------------|
| **Lieferantenchargennr.** | Wenn hier die Chargennummer des Lieferanten hinterlegt ist, dann wird genau dieser Wert in der Übersicht **Physische Packmittel** in der gleichnamigen Spalte angezeigt; ohne Eintrag bleibt die Spalte dort leer. |
| **Lieferanten interne Chargennr.** | Wenn gesetzt, dann steht die lieferantenintern verwendete Chargennummer für Rückfragen und Auswertungen zur Verfügung; sie ergänzt die offizielle Lieferantenchargennr., wird von dieser App aber nicht in der Packmittelübersicht angezeigt. |
| **Ursprungsland/-regionscode** | Wenn gepflegt, dann ist die Herkunft der Charge dokumentiert; relevant für Herkunftsnachweise, nicht Teil der Packmittelanzeige dieser App. |
| **Herstellercode** | Wenn gesetzt, dann ist der Hersteller der Charge hinterlegt; dient der Rückverfolgung, unabhängig von der Packmittelanzeige. |
| **Bund** | Wenn aktiviert, dann ist die Charge als Bund gekennzeichnet; steuert Auswertungen in m+m Additional Lot Information, nicht die Anzeige dieser Bridge-App. |

### Voraussetzung Lizenz

Die App prüft die Lizenz automatisch bei der Anmeldung des Anwenders. Ist die App installiert und lizenziert, dann steht die Zusatzspalte **Lieferantenchargennr.** in der Übersicht **Physische Packmittel** bereit. Ist keine gültige Lizenz vorhanden, dann wird die Zusatzfunktion nicht aktiviert. Es sind keine manuellen Einrichtungsschritte für diese Prüfung erforderlich; der Anwender muss nichts konfigurieren.

## Die Liste „Physische Packmittel"

Die Übersicht **Physische Packmittel** ist über die **Suche** in Microsoft Dynamics 365 Business Central zu erreichen. Sie stammt aus der App m+m Package Management und listet die aktuell vorhandenen physischen Packmittel je Zeile auf (Packmittel, enthaltene Artikel und Innenverpackungen). Neue Zeilen werden hier nicht direkt angelegt; die Pflege erfolgt über die Aktionen der Basis-App. Diese App ergänzt die Liste um genau eine schreibgeschützte Spalte: **Lieferantenchargennr.**

### Spalten der Übersicht

Die folgende Tabelle beschreibt die in der Übersicht sichtbaren Spalten (Basis-App und die von dieser App ergänzte Spalte gemeinsam, da der Anwender eine einzige Liste sieht):

| Feld | Erläuterung |
|------|-------------|
| **Packmittel Nr.** | Zeigt die Nummer des physischen Packmittels; damit identifiziert der Anwender das konkrete Packstück in der Liste. |
| **Packmittelcode** | Zeigt den Code der zugrunde liegenden Packmitteldefinition; damit erkennt der Anwender die Art des Packmittels. |
| **Reserviert** | Zeigt die reservierte Menge zu dieser Zeile; ist der Wert größer null, dann ist der Bestand bereits einem Vorgang zugeordnet und steht nicht frei zur Verfügung. |
| **Artikelnr.** | Zeigt den im Packmittel enthaltenen Artikel; zusammen mit Variantencode und Chargennr. bestimmt dieser Wert, welche **Lieferantenchargennr.** angezeigt wird. |
| **Variantencode** | Zeigt die Artikelvariante der Zeile; er geht in die Ermittlung der Lieferantenchargennr. ein. |
| **Seriennr.** | Zeigt die Seriennummer, sofern der Artikel seriennummernpflichtig ist. |
| **Chargennr.** | Zeigt die Chargennummer des enthaltenen Artikels; über diese Chargennr. (mit Artikelnr. und Variantencode) wird die **Lieferantenchargennr.** aus der Chargennr.-Information ermittelt. |
| **Zeilenart** | Gibt an, welchen Inhalt die Zeile beschreibt. Werte siehe Erläuterung unmittelbar unter dieser Tabelle. |
| **Innenverpackungsart** | Gibt die Ausrichtung einer Innenverpackung an. Werte siehe Erläuterung unter dieser Tabelle. |
| **Innenverpackungscode** | Zeigt den Code der Innenverpackung; relevant, wenn die Zeile eine Innenverpackung beschreibt. |
| **Packmittelgruppennr.** | Zeigt die Nummer der Packmittelgruppe, zu der die Zeile gehört; damit erkennt der Anwender zusammengehörende Packstücke. |
| **Packmittelgruppencodenr.** | Zeigt den Gruppencode der Packmittelgruppe; dient der Zuordnung mehrerer Packmittel zu einer Gruppe. |
| **Posten Nr.** | Zeigt die interne laufende Nummer des Eintrags; dient der eindeutigen technischen Identifikation der Zeile. |
| **Sortierung Nr.** | Steuert die Reihenfolge der Anzeige; damit bleibt die Baumdarstellung der Packmittel stabil sortiert. |
| **Reihenfolgenzeilennr.** | Zeigt die Zeilennummer innerhalb der Sortierreihenfolge; ergänzt die Sortierung Nr. für eine eindeutige Reihenfolge. |
| **Stufe** | Zeigt die Ebene der Zeile in der Packmittelstruktur; damit erkennt der Anwender die Verschachtelung (z. B. Packmittel über Innenverpackung über Artikel). |
| **Packmittelgruppencode** | Zeigt den übergeordneten Gruppencode der Zeile; ordnet die Zeile ihrer übergeordneten Packmittelstruktur zu. |
| **Übergeordnete Packmittel Nr.** | Zeigt das übergeordnete Packmittel; damit ist die Eltern-Kind-Beziehung in der Struktur nachvollziehbar. |
| **Beschreibung** | Zeigt die Bezeichnung des Packmittels oder Artikels der Zeile. |
| **Beschreibung 2** | Zeigt eine ergänzende Bezeichnung, sofern gepflegt. |
| **Menge** | Zeigt die Menge des Inhalts der Zeile; damit sieht der Anwender, wie viel im Packmittel enthalten ist. |
| **Lagerort** | Zeigt den Lagerort des Packmittels; damit ist der physische Standort erkennbar. |
| **Lagerplatz** | Zeigt den Lagerplatz innerhalb des Lagerorts; ergänzt den Lagerort um die genaue Ablage. |
| **NVE Code** | Zeigt die NVE (Nummer der Versandeinheit) des Packmittels, sofern vergeben; dient der Versand- und Sendungsidentifikation. |
| **Lieferantenchargennr.** *(von dieser App ergänzt)* | Wenn zur Charge der Zeile (Artikelnr. + Variantencode + Chargennr.) auf der **Chargennr.-Information** eine Lieferantenchargennr. hinterlegt ist, dann zeigt diese Spalte automatisch genau diesen Wert an. So sieht der Anwender die Lieferantencharge direkt am Packmittel, ohne die Chargennr.-Information gesondert zu öffnen. Das Feld ist schreibgeschützt und wird laufend aus der Charge berechnet; eine Änderung erfolgt ausschließlich an der **Chargennr.-Information**. |

**Werte des Feldes Zeilenart** (gibt an, was die Zeile darstellt – alle möglichen Werte):

- **(leer):** Zeile ohne bestimmte Einordnung – die Zeile ist keinem der folgenden Typen zugeordnet.
- **Packmittel:** Die Zeile beschreibt das Packmittel selbst (das äußere Packstück).
- **Artikel:** Die Zeile beschreibt einen im Packmittel enthaltenen Artikel; nur bei diesen Zeilen ist die **Lieferantenchargennr.** fachlich relevant, da hier Artikelnr. und Chargennr. vorliegen.
- **Innenverpackung:** Die Zeile beschreibt eine Innenverpackung innerhalb des Packmittels.

**Werte des Feldes Innenverpackungsart** (nur bei Zeilen der Zeilenart Innenverpackung relevant – alle möglichen Werte):

- **Horizontal:** Die Innenverpackung ist horizontal angeordnet.
- **Vertikal:** Die Innenverpackung ist vertikal angeordnet.

### Aktionen der Übersicht (Kontext)

Die Übersicht **Physische Packmittel** stellt Aktionen der Basis-App m+m Package Management bereit, u. a. **Packmittel füllen**, **Packmittel erstellen**, **Aus Packmittelstückliste erstellen**, **Packmittelzusätze erstellen**, **Packmittelreferenzen**, **Packmittel in ein anderes Packmittel umlagern**, **Lagerort/-platz der Packmittelgruppe ändern**, **Artikel umlagern** und **Packmittelgruppe löschen**. Diese Aktionen werden **nicht** von dieser App verändert oder erweitert; ihre Bedienung ist im Handbuch zu m+m Package Management beschrieben. Für die Zusatzspalte **Lieferantenchargennr.** sind keine eigenen Aktionen erforderlich – der Wert wird automatisch angezeigt.

## FAQ und Troubleshooting

### Warum sehe ich in „Physische Packmittel" keine Spalte „Lieferantenchargennr."?
Die Spalte wird nur bereitgestellt, wenn die App installiert und lizenziert ist. Prüfen Sie, ob die App **m+m Additional Lot Information with Package Management** aktiv ist. Möglicherweise ist die Spalte auch nur in der Personalisierung ausgeblendet; blenden Sie sie über **Personalisieren** wieder ein.

### Warum ist die Spalte „Lieferantenchargennr." bei einer Zeile leer?
Die App zeigt den Wert nur an, wenn zur Charge der Zeile eine **Lieferantenchargennr.** gepflegt ist. Fehlt der Eintrag auf der **Chargennr.-Information** (Kombination aus Artikelnr., Variantencode und Chargennr.), dann bleibt die Spalte leer. Tragen Sie den Wert auf der Chargennr.-Information nach.

### Warum kann ich die „Lieferantenchargennr." in der Packmittelübersicht nicht ändern?
Das Feld ist bewusst schreibgeschützt, weil es den Wert aus der Charge nur anzeigt. Die Lieferantenchargennr. wird ausschließlich auf der **Chargennr.-Information** gepflegt; von dort übernimmt die Übersicht den Wert automatisch.

### Wo pflege ich die „Lieferantenchargennr." korrekt?
Auf der **Chargennr.-Information** der betreffenden Charge, im Feld **Lieferantenchargennr.**. Diesen Zugang erreichen Sie über den Artikel bzw. dessen Artikelverfolgung. Nach dem Speichern erscheint der Wert automatisch in der Packmittelübersicht.

### Was passiert, wenn ich die „Lieferantenchargennr." nachträglich ändere, obwohl schon gebucht wurde?
Existieren bereits Artikelposten zur Charge, dann erscheint beim Ändern eine Sicherheitsabfrage. Bestätigen Sie, wird der neue Wert konsistent in die betroffenen Posten übernommen; brechen Sie ab, bleibt der bisherige Wert bestehen. Dadurch bleibt die Rückverfolgbarkeit erhalten.

### Warum weicht die angezeigte „Lieferantenchargennr." von der erwarteten Charge ab?
Die Zuordnung erfolgt über **Artikelnr.**, **Variantencode** und **Chargennr.** der Packmittelzeile. Stimmt eine dieser Angaben nicht mit der gepflegten Charge überein, dann wird ein anderer oder kein Wert angezeigt. Prüfen Sie die drei Schlüsselfelder der Zeile gegen die Chargennr.-Information.

### Muss ich für diese App etwas einrichten?
Nein. Die App hat keine eigene Einrichtungsseite und keine Kennzeichen. Voraussetzung sind lediglich die installierten Basis-Apps, eine gültige Lizenz und eine gepflegte Lieferantenchargennr. an der Charge.

### Welche Berechtigungen benötige ich?
Sie benötigen die Berechtigungen, die auch für die Übersicht **Physische Packmittel** (m+m Package Management) und für die **Chargennr.-Information** (m+m Additional Lot Information) gelten. Die Zusatzspalte selbst erfordert keine gesonderte Freischaltung über die Lizenzprüfung hinaus.

### Warum steht die Spalte nach der Installation nicht sofort bereit?
Die Lizenz wird bei der **Anmeldung** geprüft. Melden Sie sich nach der Installation neu an, damit die Prüfung erneut durchläuft und die Zusatzspalte aktiviert wird.

### Ändert diese App etwas an den Buchungen oder Aktionen der Packmittel?
Nein. Die App fügt ausschließlich eine schreibgeschützte Anzeigespalte hinzu. Sie verändert keine Buchungen, keine Aktionen (z. B. **Packmittel füllen**, **Artikel umlagern**) und keine Mengen. Alle diese Funktionen bleiben unverändert Bestandteil der Basis-App m+m Package Management.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen realistische Auslöser und den chronologischen Ablauf in Business Central. Alle genannten Seiten, Felder und Verhaltensweisen sind im Code der beteiligten Apps hinterlegt.

### Anwendungsfall 1: Lieferantencharge beim Wareneingang erfassen und am Packmittel sichtbar machen

**Auslöser:** Eine Lieferung trifft ein; auf den Gebinden ist die Chargennummer des Lieferanten aufgedruckt. Diese soll in Business Central so hinterlegt werden, dass sie später am Packmittel ersichtlich ist.

**Einstieg in BC:** Der Anwender öffnet zum betroffenen Artikel die **Chargennr.-Information** der neu vereinnahmten Charge (über die Artikelverfolgung des Artikels).

**Kernablauf:**
1. Der Anwender trägt im Feld **Lieferantenchargennr.** die vom Lieferanten vergebene Chargennummer ein.
2. Beim Speichern wird der Wert zur Charge hinterlegt und steht auswertenden Ansichten zur Verfügung.
3. Anschließend öffnet der Anwender über die **Suche** die Übersicht **Physische Packmittel**.
4. In der Zeile des entsprechenden Packmittels (passend zu **Artikelnr.**, **Variantencode** und **Chargennr.**) erscheint der Wert nun automatisch in der Spalte **Lieferantenchargennr.**

**Abschluss:** Die Lieferantencharge ist am Packmittel sichtbar; ein separates Öffnen der Chargennr.-Information ist für die tägliche Packmittelarbeit nicht mehr nötig.

### Anwendungsfall 2: Lieferantencharge während der Packmittelbearbeitung nachschlagen

**Auslöser:** Ein Mitarbeiter in Lager/Logistik bearbeitet ein Packmittel und muss gegenüber Kunde oder Qualitätssicherung die **Lieferantenchargennr.** der enthaltenen Charge nennen.

**Einstieg in BC:** Der Anwender öffnet über die **Suche** die Ansicht **Physische Packmittel**.

**Kernablauf:**
1. Der Anwender filtert bzw. sortiert die Liste nach **Packmittel Nr.**, **Artikelnr.** oder **Chargennr.**, um die richtige Zeile zu finden.
2. In der Spalte **Lieferantenchargennr.** liest er den zur Charge hinterlegten Wert direkt ab.
3. Ist die Spalte leer, erkennt der Anwender, dass die Lieferantenchargennr. an der Charge noch nicht gepflegt ist (siehe Anwendungsfall 1).

**Abschluss:** Die benötigte Information liegt unmittelbar in der Packmittelübersicht vor; die Auskunft kann ohne Wechsel in andere Ansichten gegeben werden.

### Anwendungsfall 3: Falsch erfasste Lieferantencharge korrigieren

**Auslöser:** Es fällt auf, dass an einer Charge eine falsche **Lieferantenchargennr.** hinterlegt wurde, obwohl bereits Buchungen (Artikelposten) zu dieser Charge existieren.

**Einstieg in BC:** Der Anwender öffnet die **Chargennr.-Information** der betroffenen Charge.

**Kernablauf:**
1. Der Anwender ändert im Feld **Lieferantenchargennr.** den Wert auf die korrekte Lieferantencharge.
2. Da bereits Artikelposten zur Charge bestehen, erscheint eine Sicherheitsabfrage, ob die Änderung in die vorhandenen Posten übernommen werden soll.
3. Bestätigt der Anwender, wird die korrigierte Lieferantenchargennr. konsistent in die betroffenen Posten übernommen; lehnt er ab, bleibt der ursprüngliche Wert bestehen.
4. Nach der Übernahme zeigt die Übersicht **Physische Packmittel** in der Spalte **Lieferantenchargennr.** automatisch den korrigierten Wert an.

**Abschluss:** Die Lieferantencharge ist über alle Buchungen hinweg korrekt und am Packmittel korrekt sichtbar; die Rückverfolgbarkeit bleibt gewahrt.
