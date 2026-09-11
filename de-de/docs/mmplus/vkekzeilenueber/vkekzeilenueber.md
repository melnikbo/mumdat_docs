---
title: Anwenderhandbuch m+m Sales Purchase Line Overview
---

# Anwenderhandbuch m+m Sales Purchase Line Overview

## Einleitung

Die Erweiterung **m+m Sales Purchase Line Overview** ergänzt Microsoft Dynamics 365 Business Central um zwei zeilenorientierte Übersichtsseiten: **Verkaufsauftragszeilen** und **Einkaufsbestellzeilen**. Beide Seiten fassen die offenen Auftrags- bzw. Bestellzeilen aller Belege in einer einzigen Liste zusammen, stellen dazu einen Filterbereich sowie mehrere Infoboxen bereit und bieten Aktionen, mit denen Sie aus einer Zeilenselektion heraus einen **Warenausgang** bzw. **Wareneingang** erzeugen.

Zielgruppe sind in erster Linie **operative Anwender** im Vertrieb und im Einkauf, die täglich mit offenen Auftrags- und Bestellzeilen arbeiten: Sachbearbeiter, die zu einem Kunden oder Lieferanten schnell Auskunft geben, Mengen und Termine prüfen, den Belegstatus verfolgen und die Lieferung bzw. den Wareneingang anstoßen. Disponenten und Lagerverantwortliche nutzen die Seiten sekundär, etwa für die Verfügbarkeitsprüfung und die Reservierung.

Der typische Ablauf ist auf beiden Seiten gleich: Sie öffnen die Übersicht, grenzen die Zeilen über den Filterbereich ein (z. B. auf einen Debitor bzw. Kreditor, einen Artikel oder auf Zeilen mit Restmenge), springen bei Bedarf über eine Aufriss-Aktion in den zugehörigen Beleg oder die Stammdatenkarte und lösen anschließend die gewünschte Folgeaktion aus.

Die Erweiterung setzt auf der App **m+m Cloud Base** auf und benötigt darüber hinaus keine eigenen Einrichtungs- oder Stammdatenseiten.

## Schnellstart für Anwender

Die beiden Übersichtsseiten sind eigenständige Listenseiten (**Ablage = Listen**) und werden über die Business-Central-Suche geöffnet. Eine gesonderte Einrichtung ist nicht erforderlich; es genügt, dass die Erweiterung installiert ist.

**Offene Verkaufsauftragszeilen prüfen und Warenausgang erstellen:**

1. Öffnen Sie über die Suche (**Suchen**) mit dem Begriff **Verkaufsauftragszeilen** die gleichnamige Seite. Beim Öffnen ist der Filter **Restmenge** bereits auf **Restmenge > 0** gesetzt, sodass nur noch offene Zeilen erscheinen.
2. Grenzen Sie die Liste im Filterbereich weiter ein, z. B. über **Debitornr.**, **Artikelnr.** oder **Verkäufer**.
3. Markieren Sie die gewünschten Zeilen und wählen Sie **Zeilen auswählen**. Die Aktion prüft je Zeile, dass der zugehörige Verkaufsauftrag den **Status** *Freigegeben* hat und ein **Lagerortcode** eingetragen ist; nur dann wird die Zeile als **Ausgewählt** markiert.
4. Über **Ausgewählte Zeilen anzeigen** blenden Sie die Liste auf die markierten Zeilen ein.
5. Wählen Sie **Warenausgang erstellen**. Für die ausgewählten Zeilen wird je Lagerort ein Warenausgang gebildet; anschließend öffnet sich die Liste der erzeugten Warenausgänge.

**Offene Einkaufsbestellzeilen prüfen und Wareneingang erstellen:**

1. Öffnen Sie über die Suche (**Suchen**) mit dem Begriff **Einkaufsbestellzeilen** die gleichnamige Seite. Auch hier ist der Filter **Restmenge** beim Öffnen auf **Restmenge > 0** voreingestellt.
2. Grenzen Sie über **Kreditornr.**, **Artikelnr.** oder **Einkäufer** ein.
3. Wählen Sie **Zeilen auswählen** (nur bei Status *Freigegeben* und gesetztem **Lagerortcode**), danach **Ausgewählte Zeilen anzeigen**.
4. Wählen Sie **Wareneingang für Zeilen erstellen**. Für die ausgewählten Zeilen wird je Lagerort ein Wareneingang gebildet; anschließend öffnet sich die Liste der erzeugten Wareneingänge.

## Einrichtung

Für den Betrieb im Webclient von Microsoft Dynamics 365 Business Central ist **keine modulspezifische Einrichtung** erforderlich. Es gibt in dieser Erweiterung keine eigene Einrichtungsseite, keine Nummernserien und keine modulspezifischen Setup-Optionen. Voraussetzung ist lediglich, dass die Erweiterung **m+m Sales Purchase Line Overview** in der Erweiterungsverwaltung installiert und die Basis-App **m+m Cloud Base** vorhanden ist.

Damit die Folgeaktionen der beiden Übersichtsseiten funktionieren, greifen die Seiten auf die **Standard-Einrichtung von Business Central** zurück. Diese Voraussetzungen richtet der Administrator im Standard ein, nicht in dieser Erweiterung:

1. **Lagerorte mit Ausgangs- bzw. Eingangslogistik:** Für die Aktion **Warenausgang erstellen** wertet die Seite alle Lagerorte aus, bei denen **Warenausgang erf.** aktiviert und **Als Umlagerungslager verw.** nicht gesetzt ist. Wenn diese Kennzeichen am Lagerort gesetzt sind, entstehen bei der Aktion Warenausgangsbelege für genau diese Lagerorte; ohne die Kennzeichen wird für den betreffenden Lagerort kein Warenausgang gebildet. Für die Aktion **Wareneingang für Zeilen erstellen** gilt sinngemäß das Kennzeichen **Wareneingang erf.**.
2. **Freigabe der Belege:** Die Zeilenselektion lässt nur Zeilen aus **freigegebenen** Aufträgen bzw. Bestellungen zu. Wenn ein Beleg noch den Status *Offen* hat, kann seine Zeile nicht ausgewählt werden; der Anwender muss den Auftrag bzw. die Bestellung zuvor im Standard freigeben.
3. **Berechtigungen:** Die mitgelieferte Berechtigungsgruppe **All permissions** (Objektname der Berechtigungsgruppe, in der Berechtigungsverwaltung sichtbar) legt fest, welche Objekte dieser Erweiterung ein Anwender aufrufen darf. Sie umfasst die beiden Übersichtsseiten, die Infoboxen und die interne Verwaltungscodeunit. Weisen Sie diese Gruppe den Anwendern zu, die mit den Übersichten arbeiten sollen.

> Hinweis: Die genannten Lagerort-Kennzeichen und die Belegfreigabe sind Bestandteil der Business-Central-Standardeinrichtung. Sie werden hier nur aufgeführt, weil die Folgeaktionen der Übersichtsseiten (siehe Kapitel **Lager und Folgebelege**) davon abhängen.

## Verkaufsauftragszeilen (Tägliche Arbeit)

Die Seite **Verkaufsauftragszeilen** zeigt die Auftragszeilen vom Typ *Artikel* aus Verkaufsaufträgen (Belegart *Auftrag*). Sie ist in einen **Filterbereich**, die **Listenansicht** (Zeilen) und mehrere **Infoboxen** gegliedert. Die Seite ist schreibgeschützt; sie dient der Auskunft, der Navigation in die Belege sowie dem Anstoßen des Warenausgangs.

Die Steuerung der angezeigten Zeilen erfolgt ausschließlich über den Filterbereich dieser Seite; es gibt keine gesonderte Einrichtungsseite, die das Verhalten vorkonfiguriert. Der Filter **Verkäufer** wertet dabei das per Erweiterung ergänzte Feld **Verkäufercode** der Auftragszeile aus (siehe Kapitel **Ergänzte Felder in den Belegzeilen**).

### Filter

Der Filterbereich schränkt die angezeigten Zeilen sofort ein; jede Eingabe aktualisiert die Liste unmittelbar.

| Filterfeld | Erläuterung |
|------------|-------------|
| Externe Belegnummer | Wenn Sie eine externe Belegnummer eintragen, werden die Zeilen auf Aufträge mit dieser externen Belegnummer eingegrenzt. So finden Sie bei einer Rückfrage schnell die passenden Auftragszeilen. |
| Restmenge | Wenn *Restmenge > 0* ausgewählt ist, werden nur Zeilen mit offener Restauftragsmenge angezeigt; bei *Alle* erscheinen auch bereits vollständig gelieferte Zeilen. Beim Öffnen der Seite ist *Restmenge > 0* voreingestellt. **Alle:** alle Auftragszeilen unabhängig von der Restmenge. **Restmenge > 0:** nur Zeilen, deren offene Restmenge größer als null ist. |
| Debitornr. | Wenn Sie einen Debitor auswählen, werden nur die Auftragszeilen dieses Debitors angezeigt; der zugehörige **Debitorname** wird darunter zur Kontrolle eingeblendet. |
| Debitorname | Zeigt den Namen zum gewählten Debitor an. Das Feld ist nicht bearbeitbar und dient nur der Kontrolle der Filterauswahl. |
| Artikelnr. | Wenn Sie einen Artikel auswählen, werden nur Zeilen zu diesem Artikel angezeigt. Beim Setzen der Artikelnr. werden ein zuvor gewählter **Variantencode** und die **Artikelreferenz** zurückgesetzt, damit sich die Filter nicht widersprechen. |
| Variantencode | Wenn Sie einen Variantencode setzen, werden die Zeilen zusätzlich auf diese Variante eingegrenzt. Die Variantenauswahl ist nur möglich, wenn zuvor eine Artikelnr. gewählt wurde; das Setzen der Variante setzt eine gesetzte **Artikelreferenz** zurück. |
| Artikelreferenz | Wenn Sie eine Artikelreferenz (z. B. eine Kundenartikelnummer) eintragen, werden die Zeilen darüber gefiltert. Das Setzen der Artikelreferenz setzt **Artikelnr.** und **Variantencode** zurück, da diese Filter alternativ wirken. |
| Verkäufer | Wenn Sie einen Verkäufer auswählen, werden nur die Auftragszeilen der Aufträge dieses Verkäufers angezeigt. Ausgewertet wird der aus dem Auftragskopf ermittelte Verkäufercode der Zeile. |

### Listenspalten

Die Listenansicht zeigt je Auftragszeile die kaufmännisch relevanten Daten. Die folgenden Spalten sind modul- bzw. auskunftsspezifisch und werden aus dem Auftragskopf oder aus verknüpften Belegen ermittelt:

| Feld | Erläuterung |
|------|-------------|
| Ausgewählt | Kennzeichnet, ob die Zeile über **Zeilen auswählen** in die aktuelle Auswahl aufgenommen wurde. Nur ausgewählte Zeilen fließen in die Erstellung des Warenausgangs ein. |
| Verk. an Deb.-Name | Zeigt den Namen des Auftragsdebitors aus dem Auftragskopf. Dient der schnellen Zuordnung der Zeile zum Kunden. |
| Status | Zeigt den Status des zugehörigen Verkaufsauftrags. **Offen:** Auftrag noch nicht freigegeben; die Zeile kann nicht für den Warenausgang ausgewählt werden. **Freigegeben:** Auftrag freigegeben; die Zeile ist für die Zeilenselektion und den Warenausgang zugelassen. |
| Belegdatum | Zeigt das Belegdatum des Auftragskopfs. |
| Auftragsdatum | Zeigt das Auftragsdatum des Auftragskopfs. |
| Externe Belegnr. | Zeigt die externe Belegnummer des Auftragskopfs, z. B. die Bestellnummer des Kunden. |
| Zugeordnete FA-Menge | Zeigt die über eine Reservierung zugeordnete Fertigungsauftragsmenge (Menge des reservierten Fertigungsauftrags). Ein Aufriss öffnet die zugeordneten FA-Zeilen. |
| Zugeordnete Fertigmenge | Zeigt die bereits fertig gemeldete Menge des zugeordneten Fertigungsauftrags. Ein Aufriss öffnet die zugeordneten FA-Zeilen mit fertig gemeldeter Menge. |
| Nicht zugeordnete FA-Menge | Zeigt die Differenz aus Basismenge der Zeile und der zugeordneten FA-Menge, also den noch nicht über einen Fertigungsauftrag gedeckten Anteil. |
| Zugeordnete Artikelverfolgungsmenge | Zeigt die über die Artikelverfolgung reservierte Menge zur Zeile (standardmäßig ausgeblendet). |
| Letztes WA-Datum | Zeigt das Buchungsdatum der letzten Warenausgangszeile (gebuchte Lieferung) zu dieser Auftragszeile. |
| Verkäufercode | Zeigt den aus dem Auftragskopf ermittelten Verkäufercode. |

Zusätzlich zeigt die Liste die kaufmännischen Standardfelder der Verkaufsauftragszeile mit ihren gewohnten Business-Central-Bezeichnungen. Diese Spalten stammen aus der Standardtabelle und werden hier gruppiert genannt, da sie unverändert übernommen werden:

- Identifikation und Artikel: **Belegnr.** (Aufriss öffnet den Verkaufsauftrag), **Verk. an Deb.-Nr.** (Aufriss öffnet die Debitorenkarte), **Artikelnr.** (Aufriss öffnet die Artikelkarte), **Variantencode** (Aufriss öffnet die Artikelvarianten), **Artikelreferenznr.**, **Beschreibung**, **Beschreibung 2**, **Einheitencode**.
- Mengen und Preise: **Menge**, **Restauftragsmenge** (offene Menge der Zeile), **VK-Preis**, **Zeilenbetrag**, **Menge geliefert** (Aufriss öffnet die gebuchten Lieferzeilen), **Zu liefern**, **Menge fakturiert** (Aufriss öffnet die gebuchten Rechnungszeilen), **Geliefert, nicht fakt. Menge**.
- Logistik und Termine: **Lagerortcode**, **Zust.-Methodencode**, **Zust.-Serviceartcode**, **Warenausgangsdatum**, **gewünschtes Lieferdatum**, **zugesagtes Lieferdatum**, **geplantes Lieferdatum**, **geplantes Warenausgangsdatum**.
- Verknüpfte Beschaffung: **Einkaufscode**, **Bestellnr. Spezialauftrag** und **Bestellnr.** (Aufriss öffnet die zugehörige Bestellung), **Rahmenauftragsnr.** samt Zeilennummer.

Die Aufriss-Spalten führen jeweils direkt in den passenden Standardbeleg (Auftrag, gebuchte Lieferung, gebuchte Rechnung, Bestellung, Debitoren- bzw. Artikelkarte), sodass Sie zur Detailprüfung nicht die Übersicht verlassen müssen.

### Aktionen

Die Seite stellt Aktionen zur **Zeilenselektion**, zum **Warenausgang** sowie Navigations- und Zeilenaktionen bereit.

**Zeilenselektion**

| Aktion | Erläuterung |
|--------|-------------|
| Zeilen auswählen | Nimmt die markierten Zeilen in die Auswahl auf. Die Aktion prüft je Zeile, dass der Auftrag den **Status** *Freigegeben* besitzt und ein **Lagerortcode** eingetragen ist; nur dann wird die Zeile als **Ausgewählt** gesetzt. Die Aktion kann mehrfach ausgeführt werden. |
| Zeilen entfernen | Hebt die Auswahl der markierten Zeilen wieder auf; das Kennzeichen **Ausgewählt** wird zurückgesetzt. |
| Ausgewählte Zeilen anzeigen | Blendet die Liste auf die zuvor ausgewählten Zeilen ein, sodass Sie vor der Warenausgangserstellung nur die relevanten Zeilen sehen. |
| Alle Zeilen anzeigen | Hebt die Einblendung auf und zeigt wieder alle gefilterten Zeilen. |

**Warenausgang**

| Aktion | Erläuterung |
|--------|-------------|
| Warenausgang erstellen | Bildet für die ausgewählten Zeilen je Lagerort einen Warenausgang. Berücksichtigt werden nur Lagerorte mit aktiviertem **Warenausgang erf.**, die nicht als Umlagerungslager gekennzeichnet sind. Existieren zu einer Zeile bereits Warenausgangszeilen, bricht die Aktion mit dem Hinweis *Es existieren Warenausgangszeilen.* ab; lässt sich keine Warenausgangszeile erzeugen, meldet sie *Es wurden keine Warenausgangszeilen erstellt.* Nach dem Lauf öffnet sich die Liste der erzeugten Warenausgänge. |

**Zugehörig – Bestellung**

| Aktion | Erläuterung |
|--------|-------------|
| Karte | Öffnet den Verkaufsauftrag der aktuell markierten Zeile. |
| Debitorkarte | Öffnet die Debitorenkarte zum Auftragsdebitor der markierten Zeile. |
| Bemerkungen | Öffnet die Belegbemerkungen zum Auftrag der markierten Zeile. |
| Dimensionen | Öffnet die Dimensionen des Auftragskopfs. |
| Genehmigungen | Öffnet die Genehmigungsposten zum Verkaufsauftrag der markierten Zeile. |
| Warenausgangszeilen | Öffnet die Warenausgangszeilen zum Auftrag der markierten Zeile. |
| Lagerbelegzeilen | Öffnet die Kommissionier-/Einlagerungszeilen (Lageraktivität) zum Auftrag. |
| Planung | Öffnet die Auftragsplanung zum Verkaufsauftrag der markierten Zeile. |
| Lieferterminzusagen | Öffnet die Lieferterminzusagen (Order Promising) zur markierten Zeile. |
| Direktlieferung – Bestellung | Öffnet die zur Zeile gehörende Direktlieferungsbestellung. |
| Spezialauftrag – Bestellung | Öffnet die zur Zeile gehörende Spezialauftragsbestellung. |

**Zugehörig – Zeile**

| Aktion | Erläuterung |
|--------|-------------|
| Artikelkarte | Öffnet die Artikelkarte zum Artikel der markierten Zeile. |
| Varianten | Öffnet die Artikelvarianten zum Artikel der markierten Zeile. |
| Artikelverfügbarkeit nach – Periode / Variante / Lagerort | Öffnet die Artikelverfügbarkeit der Zeile nach der jeweils gewählten Sicht (Periode, Variante oder Lagerort). |
| Reservierungsposten | Öffnet die Reservierungsposten zur markierten Zeile. |
| Artikelverfolgungszeilen | Öffnet die Artikelverfolgungszeilen zur markierten Zeile. |
| Dimensionen | Öffnet die Dimensionen der markierten Auftragszeile. |
| Bemerkungen | Öffnet die Zeilenbemerkungen der markierten Zeile. |

### Infoboxen der Verkaufsauftragszeilen

Rechts neben der Liste unterstützen mehrere Infoboxen die Beurteilung der aktuell markierten Zeile:

- **Durchschnittlicher Verkauf (Artikel)** und **Durchschnittlicher Verkauf (Artikelvariante)** – durchschnittliche Verkaufsmengen zum Artikel bzw. zur Artikelvariante (siehe Kapitel **Infoboxen im Detail**).
- **Durchschnittlicher Einkauf (Artikel)** und **Durchschnittlicher Einkauf (Artikelvariante)** – die entsprechenden Einkaufsdurchschnitte.
- **Fertigungsaufträge** – die der Zeile zugeordneten Fertigungsauftragszeilen mit dem zuletzt gebuchten Arbeitsgang.
- **Verkaufszeileninfo** – Anzahl zugeordneter FA-Zeilen und zugeordnete Fertigmenge zur Zeile.
- **Verknüpfte Einkaufszeilen** – Anzahl der über Spezial- oder Direktbestellung verknüpften Einkaufszeilen.

## Einkaufsbestellzeilen (Tägliche Arbeit)

Die Seite **Einkaufsbestellzeilen** zeigt die Bestellzeilen vom Typ *Artikel* aus Einkaufsbestellungen (Belegart *Bestellung*), sofern sie nicht aus einem Fertigungsauftrag stammen. Aufbau und Bedienung entsprechen der Verkaufsseite: **Filterbereich**, **Listenansicht** und **Infoboxen**. Die Seite ist schreibgeschützt und dient der Auskunft, der Navigation und dem Anstoßen des Wareneingangs.

Wie auf der Verkaufsseite steuert allein der Filterbereich die Anzeige; eine gesonderte Einrichtungsseite gibt es nicht. Der Filter **Einkäufer** wertet das per Erweiterung ergänzte Feld **Einkäufercode** der Bestellzeile aus (siehe Kapitel **Ergänzte Felder in den Belegzeilen**).

### Filter

| Filterfeld | Erläuterung |
|------------|-------------|
| Restmenge | Wenn *Restmenge > 0* ausgewählt ist, werden nur Bestellzeilen mit offener Restmenge angezeigt; bei *Alle* erscheinen auch vollständig gelieferte Zeilen. Beim Öffnen ist *Restmenge > 0* voreingestellt. **Alle:** alle Bestellzeilen unabhängig von der Restmenge. **Restmenge > 0:** nur Zeilen mit offener Restmenge größer null. |
| Kreditornr. | Wenn Sie einen Kreditor auswählen, werden nur dessen Bestellzeilen angezeigt; der zugehörige **Kreditorname** wird zur Kontrolle darunter eingeblendet. |
| Kreditorname | Zeigt den Namen zum gewählten Kreditor an. Das Feld ist nicht bearbeitbar und dient nur der Kontrolle der Filterauswahl. |
| Artikelnr. | Wenn Sie einen Artikel auswählen, werden nur Zeilen zu diesem Artikel angezeigt. Das Setzen der Artikelnr. setzt einen zuvor gewählten **Variantencode** und die **Artikelreferenz** zurück. |
| Variantencode | Wenn Sie einen Variantencode setzen, werden die Zeilen zusätzlich auf diese Variante eingegrenzt. Die Auswahl ist nur nach zuvor gewählter Artikelnr. möglich und setzt eine gesetzte **Artikelreferenz** zurück. |
| Artikelreferenz | Wenn Sie eine Artikelreferenz eintragen, werden die Zeilen darüber gefiltert. Das Setzen setzt **Artikelnr.** und **Variantencode** zurück, da die Filter alternativ wirken. |
| Einkäufer | Wenn Sie einen Einkäufer auswählen, werden nur die Bestellzeilen der Bestellungen dieses Einkäufers angezeigt. Ausgewertet wird der aus dem Bestellkopf ermittelte Einkäufercode der Zeile. |

### Listenspalten

Die folgenden Spalten sind auskunfts- bzw. modulspezifisch und werden aus dem Bestellkopf oder aus verknüpften Belegen ermittelt:

| Feld | Erläuterung |
|------|-------------|
| Ausgewählt | Kennzeichnet, ob die Zeile über **Zeilen auswählen** in die aktuelle Auswahl aufgenommen wurde. Nur ausgewählte Zeilen fließen in die Erstellung des Wareneingangs ein. |
| Einkauf von Kred.-Name | Zeigt den Namen des Bestellkreditors aus dem Bestellkopf zur schnellen Zuordnung der Zeile. |
| Status | Zeigt den Status der zugehörigen Bestellung. **Offen:** Bestellung noch nicht freigegeben; die Zeile kann nicht für den Wareneingang ausgewählt werden. **Freigegeben:** Bestellung freigegeben; die Zeile ist für die Zeilenselektion und den Wareneingang zugelassen. |
| Belegdatum | Zeigt das Belegdatum des Bestellkopfs. |
| Ihre Referenz | Zeigt die Referenz aus dem Bestellkopf (z. B. interner Bezug des Bestellers). |
| Lieferbedingungscode | Zeigt den Lieferbedingungscode (Zustellmethode) aus dem Bestellkopf. |
| Einkäufercode | Zeigt den aus dem Bestellkopf ermittelten Einkäufercode. |
| Wareneingangszeile vorhanden | Zeigt an, ob zu der Bestellzeile bereits eine Wareneingangszeile existiert. Wenn gesetzt, würde die erneute Erstellung eines Wareneingangs für diese Zeile abgewiesen; die Spalte hilft, Doppelerfassungen zu vermeiden. |

Zusätzlich zeigt die Liste die kaufmännischen Standardfelder der Einkaufsbestellzeile mit ihren gewohnten Business-Central-Bezeichnungen. Diese Spalten stammen aus der Standardtabelle und werden hier gruppiert genannt:

- Identifikation und Artikel: **Belegnr.** (Aufriss öffnet die Bestellung), **Eink. von Kred.-Nr.** (Aufriss öffnet die Kreditorenkarte), **Artikelnr.** (Aufriss öffnet die Artikelkarte), **Variantencode** (Aufriss öffnet die Artikelvarianten), **Artikelreferenznr.**, **Beschreibung**, **Beschreibung 2**, **Einheitencode**.
- Mengen und Preise: **Menge**, **Restauftragsmenge** (offene Menge der Zeile), **EK-Preis**, **Zeilenbetrag**, **Menge geliefert** (Aufriss öffnet die gebuchten Wareneingangszeilen), **Menge fakturiert** (Aufriss öffnet die gebuchten Rechnungszeilen), **Geliefert, nicht fakt. Menge**.
- Logistik und Termine: **Lagerortcode**, **erwartetes Wareneingangsdatum**, **zugesagtes Wareneingangsdatum**.
- Verknüpfte Belege: **Rahmenbestellnr.** samt Zeilennummer (Aufriss öffnet die Rahmenbestellung), **Einkaufscode**, **Verkaufsauftragsnr.** samt Zeilennummer, **Bestellnr. Spezialauftrag** samt Zeilennummer, **Fertigungsauftragsnr.** samt Zeilennummer (Aufriss öffnet den Fertigungsauftrag im jeweiligen Status).

### Aktionen

**Zeilenselektion**

| Aktion | Erläuterung |
|--------|-------------|
| Zeilen auswählen | Nimmt die markierten Zeilen in die Auswahl auf. Die Aktion prüft je Zeile, dass die Bestellung den **Status** *Freigegeben* besitzt und ein **Lagerortcode** eingetragen ist; nur dann wird die Zeile als **Ausgewählt** gesetzt. Die Aktion kann mehrfach ausgeführt werden. |
| Zeilen entfernen | Hebt die Auswahl der markierten Zeilen wieder auf; das Kennzeichen **Ausgewählt** wird zurückgesetzt. |
| Ausgewählte Zeilen anzeigen | Blendet die Liste auf die zuvor ausgewählten Zeilen ein. |
| Alle Zeilen anzeigen | Hebt die Einblendung auf und zeigt wieder alle gefilterten Zeilen. |

**Wareneingang**

| Aktion | Erläuterung |
|--------|-------------|
| Wareneingang für Zeilen erstellen | Bildet für die ausgewählten Zeilen je Lagerort einen Wareneingang. Berücksichtigt werden nur Lagerorte mit aktiviertem **Wareneingang erf.**, die nicht als Umlagerungslager gekennzeichnet sind. Existieren zu einer Zeile bereits Wareneingangszeilen, bricht die Aktion mit dem Hinweis *Es existieren bereits Wareneingangszeilen.* ab; lässt sich keine Wareneingangszeile erzeugen, meldet sie *Es wurden keine Wareneingangszeilen erstellt.* Nach dem Lauf öffnet sich die Liste der erzeugten Wareneingänge. |
| Wareneingangszeilen | Öffnet die Wareneingangszeilen zur aktuell markierten Bestellzeile. Ist bereits eine Wareneingangszeile vorhanden, kann sie hier bearbeitet werden; die Zeile muss dafür nicht über die Zeilenselektion ausgewählt sein. |

**Zugehörig – Bestellung**

| Aktion | Erläuterung |
|--------|-------------|
| Karte | Öffnet die Bestellung der aktuell markierten Zeile. |
| Kreditorkarte | Öffnet die Kreditorenkarte zum Bestellkreditor der markierten Zeile. |
| Bemerkungen | Öffnet die Belegbemerkungen zur Bestellung der markierten Zeile. |

**Zugehörig – Zeile**

| Aktion | Erläuterung |
|--------|-------------|
| Artikelkarte | Öffnet die Artikelkarte zum Artikel der markierten Zeile. |
| Artikelverfügbarkeit nach – Periode / Variante / Lagerort | Öffnet die Artikelverfügbarkeit der Zeile nach der jeweils gewählten Sicht. |
| Reservierungsposten | Öffnet die Reservierungsposten zur markierten Zeile. |
| Artikelverfolgungszeilen | Öffnet die Artikelverfolgungszeilen zur markierten Zeile. |
| Dimensionen | Öffnet die Dimensionen der markierten Bestellzeile. |
| Bemerkungen | Öffnet die Zeilenbemerkungen der markierten Zeile. |
| Artikel Zu-/Abschlagszuweisung | Öffnet die Zu-/Abschlagszuweisung zur markierten Bestellzeile. |

### Infoboxen der Einkaufsbestellzeilen

Zur Beurteilung der markierten Bestellzeile stehen folgende Infoboxen bereit:

- **Durchschnittlicher Einkauf (Artikel)** und **Durchschnittlicher Einkauf (Artikelvariante)** – durchschnittliche Einkaufsmengen zum Artikel bzw. zur Variante beim gewählten Kreditor.
- **Durchschnittlicher Verkauf (Artikel)** und **Durchschnittlicher Verkauf (Artikelvariante)** – die entsprechenden Verkaufsdurchschnitte.

## Infoboxen im Detail

Die Durchschnittsinfoboxen **Durchschnittlicher Verkauf** bzw. **Durchschnittlicher Einkauf** werten die Artikelposten des Artikels der markierten Zeile aus und stellen Mengen über mehrere Zeiträume dar.

| Feld | Erläuterung |
|------|-------------|
| Kreditornr. / Debitornr. | Zeigt den Quellfilter der Infobox: bei der Einkaufsbox die Kreditornr., bei der Verkaufsbox die Debitornr. der markierten Zeile. Ist ein Quellfilter gesetzt, werden nur Artikelposten mit dieser Quelle einbezogen. |
| Verw. Durchschnitt | Legt die Bezugsgröße der Durchschnittswerte fest. **Tag:** Umrechnung der Perioden­menge auf einen Tageswert (Basis 30 Tage je Monat). **Monat:** Umrechnung auf einen Monatswert. **Gesamt:** keine Umrechnung, es wird die Summenmenge angezeigt. |
| 6 Monate | Zeigt die Menge der letzten 6 Monate (bzw. den daraus umgerechneten Durchschnitt). |
| 12 Monate | Zeigt die Menge der letzten 12 Monate (bzw. den daraus umgerechneten Durchschnitt). |
| 13-24 Monate | Zeigt die Menge des Zeitraums von 13 bis 24 Monaten vor dem Arbeitsdatum. |
| Verkaufsmenge / Einkaufsmenge (Gesamt) | Zeigt die Gesamtmenge über alle Perioden. |

Über die Aktion **Durchschnittswert je** wählen Sie zwischen *Tag*, *Monat* und *Gesamt*; der Aufriss auf einen Mengenwert öffnet die zugrunde liegenden **Artikelposten**.

Die Infobox **Fertigungsaufträge** zeigt zu einer Auftragszeile mit reservierter Fertigung den zuletzt gebuchten Arbeitsgang:

| Feld | Erläuterung |
|------|-------------|
| Nr. (Fertigungsauftragsnr.) | Zeigt die Nummer des zugeordneten Fertigungsauftrags. Der Aufriss öffnet die Fertigungsauftragsliste im jeweiligen Status. |
| Letzter bebuchter AG.: | Zeigt die Nummer des zuletzt mit einer gebuchten Menge belegten Arbeitsgangs. |
| Art | Zeigt die Art (z. B. Arbeitsplatz oder Arbeitsplatzgruppe) des zuletzt gebuchten Arbeitsgangs. |
| Nr. | Zeigt die Nummer des Arbeitsplatzes bzw. der Arbeitsplatzgruppe des gebuchten Arbeitsgangs. |
| Beschreibung | Zeigt die Beschreibung des zuletzt gebuchten Arbeitsgangs. |
| Status | Zeigt an, ob zum freigegebenen Fertigungsauftrag bereits eine Kapazitätsbuchung erfolgt ist. **Bebucht:** es liegt mindestens eine Kapazitätsbuchung mit gebuchter Menge vor. **Nicht bebucht:** es liegt noch keine solche Buchung vor. |

Die Infobox **Verkaufszeileninfo** zeigt zwei Werte:

| Feld | Erläuterung |
|------|-------------|
| FA-Zeilen | Zeigt die Anzahl der über Reservierung zugeordneten Fertigungsauftragszeilen. Der Aufriss öffnet die Liste dieser FA-Zeilen. |
| Zugeordnete Fertigmenge | Zeigt die über die Artikelverfolgung zugeordnete Fertigmenge. Der Aufriss öffnet die zugehörigen Reservierungsposten. |

Die Infobox **Verknüpfte Einkaufszeilen** zeigt, wie eine Verkaufsauftragszeile mit Einkaufszeilen verknüpft ist:

| Feld | Erläuterung |
|------|-------------|
| Spezialbestellungen | Zeigt die Anzahl der über einen Spezialauftrag verknüpften Einkaufszeilen. Der Aufriss öffnet diese Einkaufszeilen. |
| Direktbestellungen | Zeigt die Anzahl der über eine Direktbestellung (Sales Order-Verknüpfung) verknüpften Einkaufszeilen. Der Aufriss öffnet diese Einkaufszeilen. |

## Ergänzte Felder in den Belegzeilen

Die Erweiterung fügt der Verkaufs- und der Einkaufszeile jeweils genau ein zusätzliches Feld hinzu. Beide Felder werden aus dem jeweiligen Belegkopf ermittelt (berechnete Felder) und sind nicht bearbeitbar. Sie dienen als Grundlage für die Filter **Verkäufer** bzw. **Einkäufer** der Übersichtsseiten.

| Feld | Erläuterung |
|------|-------------|
| Verkäufercode (Verkaufszeile) | Übernimmt den Verkäufercode aus dem Verkaufsauftragskopf zur zugehörigen Zeile. Dadurch lassen sich die Verkaufsauftragszeilen in der Übersicht direkt nach Verkäufer filtern, ohne den Auftragskopf zu öffnen. |
| Einkäufercode (Einkaufszeile) | Übernimmt den Einkäufercode aus dem Bestellkopf zur zugehörigen Zeile. Dadurch lassen sich die Einkaufsbestellzeilen in der Übersicht direkt nach Einkäufer filtern. |

## Lager und Folgebelege

Die einzige belegerzeugende Verarbeitung dieser Erweiterung ist die Erstellung von **Warenausgang** (Verkauf) bzw. **Wareneingang** (Einkauf) aus einer Zeilenselektion. Der Ablauf ist in beiden Fällen identisch aufgebaut und folgt einer festen Schrittfolge.

**Ablauf Warenausgang (Verkaufsauftragszeilen):**

1. Zeile(n) in der Liste **Verkaufsauftragszeilen** markieren.
2. **Zeilen auswählen** – prüft je Zeile **Status** *Freigegeben* und gesetzten **Lagerortcode** und markiert die Zeile als **Ausgewählt**.
3. Optional **Ausgewählte Zeilen anzeigen**, um vor der Erzeugung nur die Auswahl zu sehen.
4. **Warenausgang erstellen** – bildet je Lagerort (nur bei **Warenausgang erf.** und kein Umlagerungslager) einen Warenausgang und überträgt die ausgewählten Zeilen. Bereits vorhandene Warenausgangszeilen führen zum Abbruch mit entsprechendem Hinweis.
5. Nach dem Lauf öffnet sich die Liste der erzeugten Warenausgänge zur weiteren Bearbeitung.

**Ablauf Wareneingang (Einkaufsbestellzeilen):**

1. Zeile(n) in der Liste **Einkaufsbestellzeilen** markieren.
2. **Zeilen auswählen** – prüft je Zeile **Status** *Freigegeben* und gesetzten **Lagerortcode**.
3. Optional **Ausgewählte Zeilen anzeigen**.
4. **Wareneingang für Zeilen erstellen** – bildet je Lagerort (nur bei **Wareneingang erf.** und kein Umlagerungslager) einen Wareneingang. Bereits vorhandene Wareneingangszeilen führen zum Abbruch.
5. Nach dem Lauf öffnet sich die Liste der erzeugten Wareneingänge.

Die Übersichtsseiten buchen **nichts** selbst. Die eigentliche Buchung des Warenausgangs bzw. Wareneingangs erfolgt anschließend im Standard-Lagerbeleg von Business Central. Über die Aufriss-Spalten **Menge geliefert** und **Menge fakturiert** sowie die Zeilenaktionen **Warenausgangszeilen**, **Wareneingangszeilen** und **Lagerbelegzeilen** gelangen Sie in die zugehörigen Lager- und Folgebelege.

## Typische Anwendungsfälle

### Kundenrückfrage zu einem offenen Auftrag beantworten

**Auslöser:** Ein Kunde meldet sich telefonisch und fragt nach dem Status seiner offenen Bestellung und dem voraussichtlichen Liefertermin.

**Einstieg in BC:** Öffnen Sie über die Suche (**Suchen**) die Seite **Verkaufsauftragszeilen**. Tragen Sie im Filter die **Externe Belegnr.** des Kunden oder die **Debitornr.** ein. Die Liste zeigt sofort die offenen Zeilen.

**Kernablauf:** Prüfen Sie je Zeile den **Status**, das **gewünschte Lieferdatum**, das **zugesagte Lieferdatum** sowie **Restauftragsmenge** und **Menge geliefert**. Über den Aufriss auf **Menge geliefert** sehen Sie die bereits gebuchten Lieferzeilen. Benötigen Sie eine Verfügbarkeitsaussage, öffnen Sie über **Zugehörig – Zeile** die **Artikelverfügbarkeit nach – Periode**. Springen Sie bei Bedarf über **Karte** in den Verkaufsauftrag.

**Abschluss:** Die Auskunft erfolgt direkt aus der Übersicht; eine Buchung ist nicht erforderlich.

### Warenausgang für freigegebene Auftragszeilen anstoßen

**Auslöser:** Für mehrere freigegebene Aufträge eines Lagerorts soll der Warenausgang gestartet werden.

**Einstieg in BC:** Öffnen Sie **Verkaufsauftragszeilen** und filtern Sie über **Restmenge > 0** und ggf. **Debitornr.** oder **Artikelnr.** auf die relevanten Zeilen.

**Kernablauf:** Markieren Sie die gewünschten Zeilen und wählen Sie **Zeilen auswählen**. Nur Zeilen mit **Status** *Freigegeben* und gesetztem **Lagerortcode** werden übernommen; andere werden abgewiesen. Kontrollieren Sie die Auswahl über **Ausgewählte Zeilen anzeigen**. Lösen Sie dann **Warenausgang erstellen** aus.

**Abschluss:** Business Central bildet je Lagerort einen Warenausgang und öffnet die Liste der erzeugten Warenausgänge. Die weitere Kommissionierung und Buchung erfolgt im Standard-Lagerbeleg.

### Wareneingang für eintreffende Bestellungen vorbereiten

**Auslöser:** Eine Lieferavis-Mitteilung eines Lieferanten kündigt den Eingang mehrerer Bestellpositionen an.

**Einstieg in BC:** Öffnen Sie **Einkaufsbestellzeilen** und filtern Sie über **Kreditornr.** und **Restmenge > 0**.

**Kernablauf:** Kontrollieren Sie über die Spalte **Wareneingangszeile vorhanden**, ob für Zeilen bereits ein Wareneingang existiert. Markieren Sie die einzulagernden Zeilen, wählen Sie **Zeilen auswählen** (Status *Freigegeben* und **Lagerortcode** vorausgesetzt) und danach **Wareneingang für Zeilen erstellen**.

**Abschluss:** Je Lagerort entsteht ein Wareneingang; die Liste der erzeugten Wareneingänge öffnet sich zur weiteren Bearbeitung.

### Beschaffung zu einer Auftragszeile nachverfolgen

**Auslöser:** Zu einer Auftragszeile ist unklar, ob die Ware über eine Spezial-, Direkt- oder Fertigungsbeschaffung gedeckt ist.

**Einstieg in BC:** Öffnen Sie **Verkaufsauftragszeilen** und suchen Sie die betreffende Zeile über **Artikelnr.** oder **Debitornr.**.

**Kernablauf:** Werten Sie die Infobox **Verknüpfte Einkaufszeilen** aus (Anzahl **Spezialbestellungen** und **Direktbestellungen**) und öffnen Sie per Aufriss die verknüpften Einkaufszeilen. Für eine Fertigungsdeckung nutzen Sie die Spalten **Zugeordnete FA-Menge** und **Zugeordnete Fertigmenge** sowie die Infobox **Fertigungsaufträge** mit dem zuletzt gebuchten Arbeitsgang. Über die Spalten **Bestellnr.** bzw. **Bestellnr. Spezialauftrag** springen Sie direkt in die zugehörige Bestellung.

**Abschluss:** Die Nachverfolgung erfolgt vollständig aus der Übersicht heraus; Buchungen sind nicht nötig.

## FAQ und Troubleshooting

### Warum kann ich eine Zeile nicht über „Zeilen auswählen“ auswählen?
Die Aktion **Zeilen auswählen** übernimmt eine Zeile nur, wenn der zugehörige Beleg den **Status** *Freigegeben* hat und in der Zeile ein **Lagerortcode** gesetzt ist. Ist der Auftrag bzw. die Bestellung noch *Offen* oder fehlt der Lagerortcode, wird die Zeile abgewiesen. Geben Sie den Beleg zuvor im Standard frei bzw. tragen Sie den Lagerortcode ein.

### Warum sehe ich beim Öffnen nur einen Teil der Zeilen?
Beim Öffnen setzen beide Seiten den Filter **Restmenge** automatisch auf **Restmenge > 0**. Dadurch erscheinen nur Zeilen mit offener Menge. Wählen Sie im Filter **Alle**, um auch vollständig gelieferte Zeilen zu sehen.

### Warum werden nur Artikelzeilen angezeigt?
Beide Übersichten filtern fest auf Zeilen vom Typ *Artikel* und auf die Belegart *Auftrag* bzw. *Bestellung*. Sach-, Ressourcen- oder Textzeilen sowie andere Belegarten erscheinen deshalb nicht. Einkaufsbestellzeilen aus Fertigungsaufträgen werden ebenfalls ausgeblendet.

### Warum bricht „Warenausgang erstellen“ mit einem Hinweis ab?
Existieren zu einer ausgewählten Zeile bereits Warenausgangszeilen, bricht die Aktion mit *Es existieren Warenausgangszeilen.* ab. Prüfen Sie über **Warenausgangszeilen**, ob für die Zeile bereits ein Warenausgang besteht, und entfernen Sie die Zeile ggf. aus der Auswahl.

### Warum wird für einen Lagerort kein Warenausgang bzw. Wareneingang gebildet?
Berücksichtigt werden nur Lagerorte, bei denen **Warenausgang erf.** bzw. **Wareneingang erf.** aktiviert ist und die nicht als Umlagerungslager gekennzeichnet sind. Ist eines dieser Kennzeichen am Lagerort nicht gesetzt, bleibt der Lagerort bei der Erstellung außen vor.

### Was bedeutet die Spalte „Wareneingangszeile vorhanden“ in den Einkaufsbestellzeilen?
Die Spalte zeigt an, dass zu der Bestellzeile bereits eine Wareneingangszeile existiert. In diesem Fall würde die erneute Erstellung eines Wareneingangs für diese Zeile abgewiesen. Nutzen Sie stattdessen die Aktion **Wareneingangszeilen**, um den vorhandenen Wareneingang zu bearbeiten.

### Wie filtere ich die Zeilen nach Verkäufer bzw. Einkäufer?
Nutzen Sie im Filterbereich das Feld **Verkäufer** (Verkaufsauftragszeilen) bzw. **Einkäufer** (Einkaufsbestellzeilen). Ausgewertet werden die ergänzten Zeilenfelder **Verkäufercode** bzw. **Einkäufercode**, die den jeweiligen Code aus dem Belegkopf übernehmen.

### Warum lassen sich Artikelnr. und Artikelreferenz nicht gleichzeitig setzen?
Die Filter **Artikelnr.**/**Variantencode** und **Artikelreferenz** wirken alternativ. Setzen Sie die **Artikelnr.**, werden **Variantencode** und **Artikelreferenz** zurückgesetzt; setzen Sie die **Artikelreferenz**, werden **Artikelnr.** und **Variantencode** zurückgesetzt. So bleibt der Filter eindeutig.

### Kann ich die Zeilen in den Übersichten direkt ändern?
Nein. Beide Seiten sind schreibgeschützt und dienen der Auskunft und Navigation. Änderungen nehmen Sie im jeweiligen Standardbeleg vor, den Sie über die Aktion **Karte** oder den Aufriss auf die **Belegnr.** öffnen.

### Was zeigen die Durchschnittsinfoboxen an?
Die Infoboxen **Durchschnittlicher Verkauf** bzw. **Durchschnittlicher Einkauf** werten die Artikelposten des Artikels der markierten Zeile aus und zeigen Mengen für 6 Monate, 12 Monate und 13-24 Monate sowie die Gesamtmenge. Über **Verw. Durchschnitt** stellen Sie zwischen Tages-, Monats- und Gesamtwert um; der Aufriss öffnet die zugrunde liegenden Artikelposten.
