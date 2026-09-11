---
title: Anwenderhandbuch m+m Subcontracting
---

# Anwenderhandbuch m+m Subcontracting

## Einleitung

Das Modul **m+m Subcontracting** bildet die **Fremdarbeit** (Fremdbearbeitung/Lohnbearbeitung) in Microsoft Dynamics 365 Business Central als eigenständigen Beleg ab: den **Fremdarbeitenauftrag**. Der Anwender steuert damit den kompletten Ablauf, wenn ein Arbeitsgang oder ein Artikel an einen externen Kreditor (Lohnbearbeiter) vergeben wird — vom Warenausgang an den Kreditor über den Wareneingang der bearbeiteten Ware bis zur Abrechnung der Bearbeitungsleistung.

Ein Fremdarbeitenauftrag besteht aus einem **Kopf** (Kreditor, Adressen, Termine, Lagerorte, Status), den **Auftragszeilen** (die zu bearbeitenden Herkunftsbelege wie Fertigungsauftrag oder Verkaufsauftrag samt Chargen/Seriennummern) und den **Gruppierungen** (die mengen- und wertmäßig gebündelten Positionen, die aus- und eingehen und abgerechnet werden). Jede Gruppierung kann zusätzlich **Zu-/Abschläge**, eine **Erw. Beschreibung** und zugewiesene **Chargen/Seriennummern** tragen. Buchungen erzeugen **Fremdarbeitenauftragsposten** und — über die im Hintergrund verwaltete **Einkaufsbestellung** — gebuchte Wareneingänge und Einkaufsrechnungen.

**Zielgruppe:** Primär **operative Anwender**, die täglich mit Fremdarbeit arbeiten — Fertigungssteuerung, Arbeitsvorbereitung, Einkauf/Disposition und Lager, die Fremdarbeitenaufträge anlegen, freigeben, Aus- und Eingang buchen und abrechnen. **Sekundär** wenden sich die Kapitel **Einrichtung** und die Vorbereitung der Stammdaten an **Administratoren bzw. Key-User**, die das Modul einmalig konfigurieren.

**Typischer Einstieg:** Ein Fremdarbeitenauftrag entsteht in der Regel nicht auf der leeren Seite, sondern **aus einem vorhandenen Beleg**: aus einer **Verkaufsauftragszeile** (Aktion **Fremdarbeitenauftrag erstellen** im Verkaufsauftrag) oder aus einem **freigegebenen Fertigungsauftrag** mit einem Arbeitsgang an einer als Fremdarbeit gekennzeichneten **Arbeitsplatzgruppe**. Anschließend arbeitet der Anwender in der Liste **Fremdarbeitenaufträge** und auf der Belegseite **Fremdarbeitenauftrag** weiter.

## Schnellstart für Anwender

Der Schnellstart zeigt den kürzesten durchgängigen Weg. Er setzt eine **einmalige Einrichtung** durch den Administrator voraus (siehe Kapitel **Einrichtung**); danach folgt die tägliche Arbeit in fester Reihenfolge.

**Voraussetzung (einmalig, Administrator):**

1. **Suche** öffnen, Seite **Fremdarbeitenauftrag Einrichtung** aufrufen und die **Nummernserie** im Feld **Fremdarbeitenauftragsnummern** hinterlegen (Pflichtfeld für die Belegnummer).
2. Auf derselben Seite die Berichts-IDs für **Fremdarbeitenauftrag**, **Fremdarbeitslieferschein** und **Fremdarbeitabholschein** eintragen, wenn gedruckt werden soll.
3. Sicherstellen, dass mindestens eine **Arbeitsplatzgruppe** mit gefülltem Feld **Kreditor** (Subcontractor No.) als Fremdarbeitsplatz vorhanden ist.

**Täglicher Ablauf (operativer Anwender):**

1. Fremdarbeitenauftrag anlegen — aus der **Verkaufsauftragszeile** über **Fremdarbeitenauftrag erstellen**, aus dem **Fertigungsauftrag** über den Fremdarbeitsgang, oder manuell in **Fremdarbeitenaufträge** (Aktion Neu). Status ist **Offen**.
2. Auf der Seite **Fremdarbeitenauftrag** die **Auftragszeilen** und **Gruppierungen** prüfen/ergänzen (Artikel, Menge, Preis, ggf. Zu-/Abschläge).
3. Aktion **Freigeben** wählen (Status wird **Freigegeben**).
4. Aktion **Ausgang buchen** — Rückfrage **Ausgang buchen?** bestätigen; die ausgehende Menge wird gebucht (Status wird **In Bearbeitung**).
5. Nach Rücklieferung: Aktion **Eingang buchen** — Rückfrage **Eingang buchen?** bestätigen; der Wareneingang wird gebucht.
6. Aktion **Abrechnung buchen** — Rückfrage **Abrechnung buchen?** bestätigen; die Einkaufsrechnung entsteht und der Beleg kann auf **Abgerechnet** gesetzt werden.

Diese Schrittfolge (**Freigeben → Ausgang buchen → Eingang buchen → Abrechnung buchen**) ist die verbindliche Buchungsreihenfolge; sie wird im Kapitel **Buchungsablauf** und in den **Typischen Anwendungsfällen** mit denselben Aktionsbezeichnungen wiederholt.

## Einrichtung

Die Einrichtung erfolgt **einmalig** durch den **Administrator** bzw. **Key-User** vor dem ersten Einsatz. Alle Einstellungen liegen zentral auf **einer** Seite: **Fremdarbeitenauftrag Einrichtung**.

**Einstieg:** **Suche** öffnen und **Fremdarbeitenauftrag Einrichtung** aufrufen. Es handelt sich um eine unternehmensweite Einzelsatz-Einrichtung (`UsageCategory = Administration`); beim ersten Öffnen legt das System den Einrichtungssatz automatisch an. Da es keine übergeordnete Liste gibt, ist die **Suche** hier der vorgesehene Einstieg.

Die Seite gliedert sich in die Register **Nummernserie**, **Berichte** und **Produktion**. Die folgende Tabelle dokumentiert alle vom Administrator pflegbaren Felder.

| Einrichtung | Erläuterung |
|---|---|
| **Fremdarbeitenauftragsnummern** (Register Nummernserie) | Wenn hier eine Nummernserie hinterlegt ist, dann vergibt das System beim Anlegen jedes neuen Fremdarbeitenauftrags automatisch die nächste **Nr.** aus dieser Serie. Ohne Eintrag lässt sich kein Beleg anlegen — die Belegerstellung bricht mit einem Hinweis auf das fehlende Feld ab. |
| **Fremdarbeitenauftrag** (Register Berichte) | Wenn hier eine Berichts-ID eingetragen ist, dann kann der Anwender auf dem Beleg die Aktion **Fremdarbeitenauftrag** (Bereich Berichte) ausführen und den Auftrag als Dokument für den Kreditor drucken. Ohne Eintrag ist der Druck nicht möglich (das System prüft das Feld beim Aufruf). |
| **Fremdarbeitslieferschein** (Register Berichte) | Wenn hier eine Berichts-ID eingetragen ist, dann kann der Anwender über die Aktion **Fremdarbeitslieferschein** den Lieferschein für die an den Kreditor ausgehende Ware drucken. Ohne Eintrag steht der Druck nicht zur Verfügung. |
| **Fremdarbeitabholschein** (Register Berichte) | Wenn hier eine Berichts-ID eingetragen ist, dann kann der Anwender über die Aktion **Abholschein** das Abholdokument drucken. Ohne Eintrag bricht der Aufruf mit Feldprüfung ab. |
| **FA nicht berechnen für Gruppierungen** (Register Produktion) | Steuert die Art der Fertigungsauftrags-Erstellung aus einer Gruppierung. Wenn aktiviert, dann legt das System bei **Fertigungsauftrag erstellen** direkt eine Fertigungsauftragszeile ohne Durchlauf des Berichts „Fertigungsauftrag aktualisieren“ an — schneller, aber ohne automatische Komponenten-/Arbeitsplanauflösung. Wenn nicht aktiviert, dann wird der Fertigungsauftrag über „Fertigungsauftrag aktualisieren“ vollständig berechnet (Komponenten und Arbeitsplan werden aufgelöst). |

Systemfeld **Primärschlüssel** (technischer Einzelsatzschlüssel) ist nicht sichtbar zu pflegen und daher nicht dokumentiert.

### Nummernserie einrichten

**Prozesseinstieg:** Der Administrator konfiguriert die Belegnummerierung vor der ersten Auftragsanlage. Der operative Anwender verbraucht diese Einstellung später in **Fremdarbeitenaufträge → Neu** bzw. **Fremdarbeitenauftrag erstellen** (siehe **Tägliche Arbeit**).

1. **Suche** → **Fremdarbeitenauftrag Einrichtung** öffnen.
2. Im Register **Nummernserie** im Feld **Fremdarbeitenauftragsnummern** eine Nummernserie auswählen. Wenn gesetzt, dann zieht jeder neue Beleg seine **Nr.** automatisch aus dieser Serie; die Serie muss zur manuellen oder automatischen Vergabe passen.
3. Ergebnis im Tagesablauf: Beim Anlegen eines Fremdarbeitenauftrags erhält der Beleg sofort eine eindeutige **Nr.**; ein zugehöriges Feld **Nummernserie** wird schreibgeschützt am Beleg protokolliert.

### Berichte einrichten

**Prozesseinstieg:** Der Administrator hinterlegt die Druckberichte, bevor Belege an Kreditoren versendet werden. Konsumiert werden die Einstellungen im Bereich **Berichte** auf der Belegseite (siehe **Tägliche Arbeit → Berichte drucken**).

1. **Suche** → **Fremdarbeitenauftrag Einrichtung** → Register **Berichte**.
2. Für **Fremdarbeitenauftrag**, **Fremdarbeitslieferschein** und **Fremdarbeitabholschein** je eine Berichts-ID eintragen. Wenn ein Feld gefüllt ist, dann wird die zugehörige Druckaktion auf dem Beleg aktiv; ist es leer, prüft das System das Feld beim Aufruf und verhindert den Druck.
3. Ergebnis im Tagesablauf: Der Anwender kann den Auftrag, den Lieferschein und den Abholschein direkt vom Fremdarbeitenauftrag drucken.

### Berechtigungen

Der Berechtigungssatz **All permissions** (Objekt „MuM FO Permission“) bündelt Lese-/Schreibrechte auf alle Tabellen (Fremdarbeitenauftragkopf, -zeile, -gruppenzeile, -gruppe Zu-/Abschlag, -gruppenbeschreibung, -posten, Einrichtung) sowie die Ausführungsrechte auf die Seiten und Codeunits des Moduls. Der Administrator weist diesen Satz den Benutzern zu; er legt fest, welche Aktionen die Anwender im Modul ausführen dürfen (Anlegen, Buchen, Abrechnen). Ohne diesen Satz kann ein Benutzer die Fremdarbeitenauftrags-Seiten nicht öffnen.

**Lizenz:** Das Modul prüft bei der Anmeldung über **m+m Cloud Base** die Lizenz. Ist keine gültige Lizenz vorhanden, stehen die Funktionen nicht bereit; dies betrifft ausschließlich den Administrator bei der Bereitstellung.

## Stammdaten und Voraussetzungen

Das Modul bringt **keine** eigenen Stammdatenkarten mit; es baut auf **Standard-Stammdaten** von Business Central auf. Der Administrator bzw. Key-User bereitet vor dem ersten Einsatz die folgenden Daten vor, weil der Fremdarbeitenauftrag sie beim Anlegen und Buchen prüft.

**Arbeitsplatzgruppe mit Kreditor:** Eine Fremdarbeit setzt mindestens eine **Arbeitsplatzgruppe** voraus, deren Feld **Kreditor** (Subcontractor No.) gefüllt ist. Wenn das Feld gefüllt ist, dann erkennt das Modul die Arbeitsplatzgruppe als Fremdarbeitsplatz: Bei der Erstellung aus der Verkaufsauftragszeile bietet das System nur solche Arbeitsplatzgruppen zur Auswahl an, und bei der Anlage eines Fertigungsarbeitsgangs an dieser Arbeitsplatzgruppe wird automatisch die passende Auftragszeile im Fremdarbeitenauftrag ergänzt. Das Feld **Arbeitsplatzgruppennr.** im Kopf verweist auf diese Arbeitsplatzgruppe.

**Kreditor:** Der im Kopf hinterlegte **Kreditor Nr.** ist der Lohnbearbeiter. Beim Setzen des Kreditors übernimmt der Beleg Name, Adresse, Kontakt, **Sprachcode** und **Zlg.-Bedingungscode** aus dem Kreditorenstamm und schlägt die **Anlieferadresse** vor.

**Artikel und Fertigungsauftrag/Arbeitsplan:** Für materialbezogene Gruppierungen und Auftragszeilen sind gepflegte **Artikel** (mit Basiseinheit) und — bei fertigungsbasierten Vorgängen — ein **Fertigungsauftrag** mit **Arbeitsplan** erforderlich, dessen Arbeitsgang auf die Fremdarbeitsplatzgruppe verweist. Fehlt der Arbeitsgang, meldet das System beim Ausgang „Eine oder mehrere Auftragszeilen haben keinen zugeordneten FA-Arbeitsgang!“.

## Übersicht: Fremdarbeitenaufträge

**Einstieg:** **Suche** → **Fremdarbeitenaufträge**. Die Liste ist die zentrale Arbeitsübersicht (`UsageCategory = Lists`); ein Doppelklick öffnet den Beleg **Fremdarbeitenauftrag**.

Die Liste ist schreibgeschützt und zeigt je Zeile einen Fremdarbeitenauftrag. Die Spalten geben schnellen Überblick über Kreditor, Termine und Status.

| Feld | Erläuterung |
|---|---|
| **Nr.** | Eindeutige Belegnummer des Fremdarbeitenauftrags aus der Nummernserie. |
| **Kreditor Nr.** | Nummer des Lohnbearbeiters, an den die Bearbeitung vergeben ist. |
| **Kreditor Name** / **Kreditor Name 2** | Name des Kreditors; aktualisiert sich mit der Kreditorauswahl im Kopf. |
| **Kreditor Adresse** / **Kreditor Adresse 2** | Straße/Adresszusatz des Kreditors. |
| **Kreditor Ort** | Ort des Kreditors. |
| **Kreditor Postleitzahl** | Postleitzahl des Kreditors. |
| **Kreditor Land/Regionscode** | Land/Region des Kreditors. |
| **Belegdatum** | Erstellungsdatum des Belegs (Vorschlag: Arbeitsdatum). |
| **Status** | Bearbeitungsstand des Auftrags (siehe Werte unten). |
| **Ziellagerortcode Ausgang** | Lagerort, von dem die Ware an den Kreditor ausgeht. |
| **Ausgangsdatum** | Geplantes/verwendetes Datum des Warenausgangs an den Kreditor. |
| **Eingangsdatum** | Geplantes/verwendetes Datum des Wareneingangs vom Kreditor. |
| **Ihre Referenz** | Freies Referenzfeld des Anwenders. |
| **Externe Belegnummer** | Belegnummer des Kreditors zum Auftrag. |
| **FA-Arbeitsvorratstatus** | Fertigungsfortschritt des zugrunde liegenden Fertigungsauftrags (siehe Werte unten). |

**Status** (Option, jeder Wert steuert die erlaubten Folgeaktionen):

- **Offen:** Beleg in Bearbeitung; Zeilen, Gruppierungen und Zu-/Abschläge sind editierbar; Buchen ist noch nicht möglich. Nur aus **Offen** ist **Freigeben** erlaubt.
- **Freigegeben:** Beleg festgeschrieben; Zeilen sind gesperrt. Aus diesem Status ist **Ausgang buchen** möglich.
- **In Bearbeitung:** Der Ausgang wurde (teilweise) gebucht; der Beleg befindet sich im laufenden Aus-/Eingang und in der Abrechnung. **Eingang buchen** und **Abrechnung buchen** sind nur in diesem Status möglich.
- **Abgerechnet:** Alle abzurechnenden Mengen/Beträge sind gebucht; der Vorgang ist abgeschlossen.
- **Storniert:** Der Auftrag wurde storniert. (Die zugehörige Aktion ist standardmäßig ausgeblendet.)

**FA-Arbeitsvorratstatus** (Option, schreibgeschützt; spiegelt den Fertigungsfortschritt):

- **Nicht begonnen:** Der zugehörige Fertigungsarbeitsgang wurde noch nicht gestartet.
- **Gestartet:** Die Fertigung des Arbeitsgangs läuft.
- **Unterbrochen:** Die Fertigung ist unterbrochen.
- **Teilbeendet:** Der Arbeitsgang ist teilweise fertig gemeldet.
- **Beendet:** Der Arbeitsgang ist vollständig fertig gemeldet.

## Tägliche Arbeit am Fremdarbeitenauftrag

Die Belegseite **Fremdarbeitenauftrag** ist die zentrale Arbeitsfläche. Sie steuert das Verhalten über die auf **Fremdarbeitenauftrag Einrichtung** gepflegten Einstellungen (Nummernserie für die **Nr.**, Berichts-IDs für die Druckaktionen). Der Beleg gliedert sich in den **Kopf** (Register **Allgemein**, **Aus- & Eingang**, **Anlieferadresse**, **Informationen**), die Unterseite **Zeilen** (Auftragszeilen) und die Unterseite **Gruppierungen**.

**Einstieg:** aus **Fremdarbeitenaufträge** per Zeilenaufruf, oder aus dem **Verkaufsauftrag** über die Verkaufsauftragszeile mit Aktion **Fremdarbeitenauftrag anzeigen** / **Fremdarbeitenauftrag erstellen**. Die Belegseite selbst ist nicht über die **Suche** erreichbar (`UsageCategory = None`).

### Kopf (Register Allgemein)

| Feld | Erläuterung |
|---|---|
| **Nr.** | Belegnummer; wird beim Anlegen aus der Nummernserie gezogen. Über die Auswahlhilfe lässt sich vor der Erstvergabe eine verbundene Nummernserie wählen. |
| **Kreditor Nr.** | Lohnbearbeiter. Wenn gesetzt, dann füllt das System Name, Adresse, Kontakt, **Sprachcode**, **Zlg.-Bedingungscode** und die **Anlieferadresse** aus dem Kreditorenstamm. |
| **Kreditor Name** / **Kreditor Name 2** | Name des Kreditors (aus dem Stamm übernommen, überschreibbar). |
| **Kreditor Kontaktnr.** | Kontakt des Kreditors; über die Auswahl werden nur Kontakte des Kreditors angeboten. |
| **Kreditor Kontaktnr.** (Name) | Anzeigename des ausgewählten Kontakts. |
| **Kreditor Adresse** / **Kreditor Adresse 2** | Straße und Zusatz des Kreditors. |
| **Kreditor Ort** / **Kreditor Postleitzahl** / **Kreditor Land/Regionscode** / **Kreditor Bundesregion** | Anschriftbestandteile des Kreditors; Ort und Postleitzahl werden gegen die Postleitzahltabelle geprüft. |
| **Belegdatum** | Erstellungsdatum; Vorschlag ist das Arbeitsdatum. |
| **Ausgangsdatum** | Datum des Warenausgangs an den Kreditor. Wenn gesetzt, dann wird zugleich **Buchungsdatum (Ausgang)** vorbelegt. |
| **Eingangsdatum** | Datum des Wareneingangs. Wenn gesetzt, dann wird zugleich **Buchungsdatum (Eingang)** vorbelegt. |
| **Zugesagtes Eingangsdatum** | Vom Kreditor zugesagtes Rücklieferdatum. |
| **Auftragsbestätigungsdatum** | Datum der Auftragsbestätigung des Kreditors. |
| **Auftragsbest. Bemerkung** | Freitextbemerkung zur Auftragsbestätigung. |
| **Buchungsdatum (Ausgang)** | Buchungsdatum für den Warenausgang; Pflichtangabe beim **Ausgang buchen**. |
| **Buchungsdatum (Eingang)** | Buchungsdatum für den Wareneingang; Pflichtangabe beim **Eingang buchen**. |
| **Buchungsdatum (Abrechnung)** | Buchungsdatum für die Abrechnung; Pflichtangabe beim **Abrechnung buchen**. |
| **Zlg.-Bedingungscode** | Zahlungsbedingung für die entstehende Einkaufsrechnung. |
| **Status** | Bearbeitungsstand (schreibgeschützt; wird über die Aktionen gesetzt; Werte siehe Kapitel Übersicht). |
| **Sprachcode** | Sprache des Kreditors für Belegdruck/Kommunikation. |
| **Ihre Referenz** | Freie Referenz des Anwenders. |
| **Externe Belegnummer** | Belegnummer des Kreditors. |
| **Externe Rechnungsnr.** | Externe Rechnungsnummer; steuert bei der Abrechnung die Zusammenfassung der Zu-/Abschläge je Rechnung. |

### Kopf: Aus- & Eingang

| Feld | Erläuterung |
|---|---|
| **Ziellagerortcode Ausgang** | Lagerort, aus dem die Ware an den Kreditor ausgeht. Wenn gesetzt, dann verwendet die erzeugte Einkaufsbestellung diesen Lagerort. |
| **Ausg. Zustellercode** | Zusteller (Spediteur) für den Ausgang. Wenn geändert, dann wird die Ausg. Transportart zurückgesetzt. |
| **Ausg. Zustellertransportartencode** | Transportart des Ausgangs-Zustellers (abhängig vom Ausg. Zustellercode). |
| **Ausg. Lieferbedingungscode** | Lieferbedingung des Ausgangs. |
| **Ziellagerortcode Eingang** | Lagerort, auf dem die zurückgelieferte Ware eingeht. |
| **Eing. Zustellercode** | Zusteller für den Eingang. Wenn geändert, dann wird die Eing. Transportart zurückgesetzt. |
| **Eing. Zustellertransportartencode** | Transportart des Eingangs-Zustellers (abhängig vom Eing. Zustellercode). |
| **Eing. Lieferbedingungscode** | Lieferbedingung des Eingangs. |

### Kopf: Anlieferadresse

| Feld | Erläuterung |
|---|---|
| **Anlieferung Nr.** | Referenz auf eine abweichende Lieferadresse. |
| **Anlieferung Name** / **Anlieferung Name 2** | Name der Anlieferstelle beim Kreditor. |
| **Anlieferung Adresse** / **Anlieferung Adresse 2** | Straße und Zusatz der Anlieferstelle. |
| **Anlieferung Ort** / **Anlieferung Postleitzahl** / **Anlieferung Land/Regionscode** / **Anlieferung Bundesregion** | Anschrift der Anlieferstelle; Ort/Postleitzahl werden gegen die Postleitzahltabelle geprüft. |

### Kopf: Informationen

| Feld | Erläuterung |
|---|---|
| **Einkaufsbestellnr.** | Nummer der im Hintergrund geführten Einkaufsbestellung (schreibgeschützt); entsteht beim Erzeugen der Bestellung und trägt Wareneingang und Rechnung. |
| **Ausgang gebucht** | Kennzeichen (schreibgeschützt). Wenn gesetzt, dann ist der Warenausgang bereits gebucht; ein erneutes Freigeben führt direkt in den Status **In Bearbeitung**. |
| **Eingang gebucht** | Kennzeichen (schreibgeschützt). Wenn gesetzt, dann ist der Wareneingang gebucht. |
| **Abgerechnet** | Kennzeichen (schreibgeschützt). Wenn gesetzt, dann sind alle abzurechnenden Positionen fakturiert. |

### Auftragszeilen

Die Unterseite **Zeilen** zeigt die Auftragszeilen vom **Zeilenart Auftrag** — die konkreten Herkunftspositionen (Fertigungsauftrag/Verkaufsauftrag), die fremdbearbeitet werden.

| Feld | Erläuterung |
|---|---|
| **Gruppenzeilennr.** | Ordnet die Auftragszeile einer **Gruppierung** zu. Wenn geändert, dann wird die Zeile mengen- und wertmäßig in die betreffende Gruppierung eingerechnet. |
| **FA-Status** | Status des Herkunfts-Fertigungsauftrags (Werte: **(leer)**, **Geplant**, **Fest geplant**, **Freigegeben**, **Beendet**). Nur bei **Freigegeben** sind ausgangs-/fertigungsrelevante Folgeaktionen möglich. |
| **FA-Nr.** | Nummer des Herkunfts-Fertigungsauftrags. |
| **FA-Zeilennr.** | Zeilennummer im Herkunfts-Fertigungsauftrag. Wenn gesetzt, dann wird die passende Arbeitsgangnummer automatisch ermittelt. |
| **FA-Arbeitsgangnr.** | Arbeitsgang des Fertigungsauftrags an der Fremdarbeitsplatzgruppe; steuert das spätere Fertigmelden des Arbeitsgangs. |
| **Arbeitsplatzgruppennr.** | Fremdarbeitsplatzgruppe (Kreditor) der Zeile. |
| **Verkaufsauftragsnr.** | Herkunfts-Verkaufsauftrag (falls die Fremdarbeit aus dem Verkauf stammt). |
| **Verkaufsauftragszeilennr.** | Zeilennummer im Herkunfts-Verkaufsauftrag. |
| **Artikelnr.** | Zu bearbeitender Artikel. |
| **Variantencode** | Artikelvariante (standardmäßig ausgeblendet). |
| **Beschreibung** / **Beschreibung 2** | Artikelbeschreibung. |
| **Menge** | Zu bearbeitende Menge der Zeile. Wenn geändert, dann wird der Datensatz sofort gespeichert und in die Gruppierung eingerechnet. |
| **Zugesagtes Lieferdatum** | Vom Kreditor zugesagtes Datum (standardmäßig ausgeblendet). |
| **Einkaufsbestellnr.** / **Einkaufsbestellungszeilennr.** | Verknüpfung zur Einkaufsbestellzeile (standardmäßig ausgeblendet). |

Zeilenaktionen:

- **Fertigungsauftrag erstellen:** Erzeugt aus der Auftragszeile einen Fertigungsauftrag (Statusauswahl **Geplant**/**Fest geplant**/**Freigegeben**); setzt anschließend die Herkunftsangaben in der Zeile.
- **Fertigungsauftrag anzeigen:** Öffnet den verknüpften Fertigungsauftrag im passenden Status.
- **Verkaufsauftrag anzeigen:** Öffnet den verknüpften Verkaufsauftrag.
- **Zeile splitten:** Teilt eine Zeile mengenmäßig auf (Rückfrage **Soll die Zeile gesplittet werden?**; Aktion standardmäßig ausgeblendet).

### Gruppierungen

Die Unterseite **Gruppierungen** bündelt die auszulagernden Positionen mengen- und wertmäßig. Hier steuert der Anwender die auszugebenden, einzugehenden und abzurechnenden Mengen sowie Preise und Zu-/Abschläge.

| Feld | Erläuterung |
|---|---|
| **Zeilennr.** | Interne Nummer der Gruppierung. |
| **Artikelnr.** | Artikel der Gruppierung. Wenn gesetzt, dann werden Beschreibung und Basiseinheit aus dem Artikel übernommen. |
| **Variantencode** | Artikelvariante (standardmäßig ausgeblendet). |
| **Beschreibung** / **Beschreibung 2** | Artikelbeschreibung der Gruppierung. |
| **Menge** | Gesamtmenge der Gruppierung. Wenn gesetzt, dann werden **Betrag** (= Menge × Preis) und die Zu-/Abschläge neu berechnet. |
| **Ausgangsmenge** | Menge, die beim nächsten **Ausgang buchen** an den Kreditor ausgeht. |
| **Geb. Ausgangsmenge** | Bereits gebuchte Ausgangsmenge (schreibgeschützt). Wenn erhöht, dann wird die offene **Eingangsmenge** automatisch nachgeführt. |
| **Eingangsmenge** | Menge, die beim nächsten **Eingang buchen** zurückgebucht wird. |
| **Geb. Eingangsmenge** | Bereits gebuchte Eingangsmenge (schreibgeschützt). Wenn erhöht, dann wird die offene **Menge zu fakturieren** automatisch nachgeführt. |
| **Menge zu fakturieren** | Menge, die beim nächsten **Abrechnung buchen** berechnet wird. Wenn gesetzt, dann wird **Betrag zu fakturieren** (= Menge zu fakturieren × Preis) berechnet. |
| **Fakturierte Menge** | Bereits abgerechnete Menge (schreibgeschützt). |
| **Preis** | Bearbeitungspreis je Einheit. Wenn geändert, dann werden Betrag und Betrag zu fakturieren neu berechnet. |
| **Betrag** | Gesamtbetrag der Gruppierung (Menge × Preis). |
| **Betrag zu fakturieren** | Abzurechnender Betrag. Wenn manuell gesetzt, dann wird **Fixer Betrag zu fakturieren** aktiviert und der Betrag bleibt bei Mengenänderungen unverändert. |
| **Fixer Betrag zu fakturieren** | Kennzeichen. Wenn gesetzt, dann bleibt der eingegebene Abrechnungsbetrag fixiert und wird nicht aus Menge × Preis überschrieben. |
| **Fakturierter Betrag** | Bereits fakturierter Betrag (schreibgeschützt). |
| **Zu-/Abschläge** | Kennzeichen (schreibgeschützt). Wenn gesetzt, dann existieren zu dieser Gruppierung Zu-/Abschlagszeilen. |
| **Zu-/Abschlagsbetrag** | Summe der Zu-/Abschläge der Gruppierung (schreibgeschützt, standardmäßig ausgeblendet). |
| **Gesamtbetrag** | Betrag zzgl. Zu-/Abschlagsbetrag (schreibgeschützt). |
| **Fakturierter Gesamtbetrag** | Fakturierter Betrag inkl. Zu-/Abschläge (schreibgeschützt). |
| **Herkunftsart** | Quelle der Gruppierung (Werte: **(leer)**, **Fertigungsauftrag**, **Einkaufsbestellung**, **EK-Bestellung & FA**). Wird automatisch aus den gesetzten Herkunftsbelegen ermittelt. |
| **Herkunft Kreditornr.** | Kreditor der Herkunfts-Einkaufsbestellung (für materialbezogene Beschaffung). |
| **Herkunft Bestellnr.** / **Herkunft Bestellzeilennr.** | Verknüpfte Herkunfts-Einkaufsbestellung. |
| **Herkunft Bestell-Prozessstatus** | Beschaffungsfortschritt der Herkunftsbestellung (**(leer)**, **In Bearbeitung**, **Teilweise geliefert**, **Geliefert**). |
| **Herkunft FA-Status** | Status des Herkunfts-Fertigungsauftrags (**(leer)**, **Geplant**, **Fest geplant**, **Freigegeben**, **Beendet**). |
| **Herkunft FA-Nr.** / **Herkunft FA-Zeilennr.** | Verknüpfter Herkunfts-Fertigungsauftrag. |
| **Herkunft FA-Prozessstatus** | Fertigungsfortschritt der Herkunft (**(leer)**, **In Bearbeitung**, **Teilweise gefertigt**, **Gefertigt**). |
| **Zugew. Chargen/Seriennr.** | Anzahl der zugeordneten Chargen/Seriennummern (schreibgeschützt). Über den Drilldown öffnet sich die Liste **Chargen/Seriennummernzeilen**. |

Gruppierungsaktionen:

- **Zu-/Abschläge:** Öffnet die Zu-/Abschlagszeilen der Gruppierung (siehe H3 unten).
- **Erw. Beschreibung:** Öffnet den erweiterten Beschreibungstext der Gruppierung (siehe H3 unten).
- **Einkaufsbestellung erstellen:** Legt für die Materialbeschaffung eine Herkunfts-Einkaufsbestellung beim **Herkunft Kreditornr.** an (Pflichtfelder Herkunft Kreditornr. und Artikelnr.).
- **Einkaufsbestellung anzeigen:** Öffnet die verknüpfte Herkunfts-Einkaufsbestellung.
- **Fertigungsauftrag erstellen:** Legt für die Gruppierung einen Fertigungsauftrag an (Statusauswahl **Geplant**/**Fest geplant**/**Freigegeben**); je nach Einrichtung **FA nicht berechnen für Gruppierungen** mit oder ohne Berechnungslauf.
- **Fertigungsauftrag anzeigen:** Öffnet den verknüpften Fertigungsauftrag.

#### Zu-/Abschläge

**Prozesseinstieg:** Der operative Anwender pflegt Zu-/Abschläge (z. B. Rüst-, Transport- oder Mindermengenzuschläge) je Gruppierung, damit sie in der Abrechnung als zusätzliche Rechnungspositionen entstehen. Aufruf: In **Gruppierungen** die Zeile markieren und Aktion **Zu-/Abschläge** wählen.

| Feld | Erläuterung |
|---|---|
| **Zu-/Abschlagnr.** | Artikel-/Sachreferenz des Zu-/Abschlags (Item Charge). |
| **Beschreibung** | Bezeichnung des Zu-/Abschlags. |
| **Preis** | Preis je Einheit des Zu-/Abschlags. |
| **Zu/Abschlag Einheit** | Einheit des Zu-/Abschlags (standardmäßig ausgeblendet). |
| **Menge pro Artikeleinheit** | Umrechnungsmenge je Artikeleinheit (standardmäßig ausgeblendet). |
| **Bezugsgröße** | Grundlage der Betragsermittlung. Werte: **(leer)**, **Menge**, **Menge (KG)**, **Menge (Stk.)**, **Menge (Meter)**, **Pauschal**. **(leer)/Menge:** Betrag = Menge × Preis; **Menge (KG)/Menge (Stk.)/Menge (Meter):** Bezug auf die jeweilige physische Menge; **Pauschal:** fester Betrag unabhängig von der Menge (standardmäßig ausgeblendet). |
| **Betrag** | Errechneter Zu-/Abschlagsbetrag. |
| **Betrag zu fakturieren** | Abzurechnender Anteil des Zu-/Abschlags. |
| **Fakturierter Betrag** | Bereits abgerechneter Anteil (schreibgeschützt). |
| **Zlg.-Bedingungscode** | Zahlungsbedingung des Zu-/Abschlags; steuert die Zusammenfassung je Rechnung (standardmäßig ausgeblendet). |
| **Externe Rechnungsnr.** | Externe Rechnungsnummer des Zu-/Abschlags; steuert die Rechnungszusammenfassung (standardmäßig ausgeblendet). |
| **Produktbuchungsgruppe** | Gen.-Produktbuchungsgruppe für die Buchung (standardmäßig ausgeblendet). |
| **MwSt.-Produktbuchungsgruppe** | MwSt.-Produktbuchungsgruppe (standardmäßig ausgeblendet). |
| **Steuergruppencode** | Steuergruppe (standardmäßig ausgeblendet). |

Hinweis: Das System lässt für dieselbe Referenz keine unterschiedlichen **Zlg.-Bedingungscodes** oder **Buchungsgruppen** zu und meldet dies bei der Erfassung.

#### Erw. Beschreibung

**Prozesseinstieg:** Der Anwender hinterlegt längere Beschreibungstexte zur Gruppierung (z. B. Bearbeitungshinweise für den Kreditor). Aufruf: In **Gruppierungen** die Aktion **Erw. Beschreibung**.

| Feld | Erläuterung |
|---|---|
| **Text** | Freitextzeile(n) der erweiterten Beschreibung; erscheint auf den zugehörigen Belegen/Drucken. Ist mindestens ein Text erfasst, wird in der Gruppierung das Kennzeichen **Erw. Beschreibung** gesetzt. |

#### Chargen/Seriennummernzeilen

**Prozesseinstieg:** Zeigt die der Gruppierung zugeordneten Chargen bzw. Seriennummern an. Diese Zeilen (Zeilenart **Charge/Seriennr.**) entstehen automatisch aus den Artikelposten der Fertigung bzw. der Wareneingänge; der Anwender ruft sie über den Drilldown im Feld **Zugew. Chargen/Seriennr.** in der Gruppierung auf. Die Liste ist schreibgeschützt.

| Feld | Erläuterung |
|---|---|
| **Artikelnr.** | Artikel der Charge/Seriennummer. |
| **Variantencode** | Variante des Artikels. |
| **Beschreibung** / **Beschreibung 2** | Artikelbeschreibung. |
| **Chargennr.** | Zugeordnete Charge. |
| **Seriennr.** | Zugeordnete Seriennummer. |
| **Menge** | Menge der zugeordneten Charge/Seriennummer. |

### Berichte drucken

Aus dem Bereich **Berichte** des Belegs druckt der Anwender die eingerichteten Dokumente:

- **Fremdarbeitenauftrag** — der Auftrag als Dokument für den Kreditor.
- **Fremdarbeitslieferschein** — der Lieferschein zur ausgehenden Ware.
- **Abholschein** — das Abholdokument.

Jede Aktion prüft, ob die zugehörige Berichts-ID in der Einrichtung hinterlegt ist; fehlt sie, ist der Druck nicht möglich (siehe **Berichte einrichten**).

## Buchungsablauf

Der Fremdarbeitenauftrag durchläuft eine feste Reihenfolge von Status- und Buchungsaktionen. Der Anwender findet diese Aktionen im Bereich **Status** und **Buchen** des Belegs.

1. **Anlegen und erfassen (Status Offen):** Kopf, Auftragszeilen und Gruppierungen erfassen; Mengen (**Ausgangsmenge**), Preise und ggf. Zu-/Abschläge setzen.
2. **Freigeben:** Aktion **Freigeben**. Setzt den Status von **Offen** auf **Freigegeben** (nur aus **Offen** möglich). Die Zeilen sind danach gesperrt. Wurde bereits ein Ausgang gebucht, führt das erneute Freigeben direkt nach **In Bearbeitung**.
3. **Ausgang buchen:** Aktion **Ausgang buchen**. Rückfrage **Ausgang buchen?** bestätigen. Voraussetzung: Status **Freigegeben** oder **In Bearbeitung**, gefülltes **Buchungsdatum (Ausgang)** und mindestens eine Gruppierung mit **Ausgangsmenge** ungleich null (sonst „Es gibt nichts zu buchen!“). Das System bucht die Ausgangsmenge, erzeugt einen Fremdarbeitenauftragsposten der **Postenart Ausgang**, setzt **Geb. Ausgangsmenge** hoch und den Status auf **In Bearbeitung** sowie **Ausgang gebucht** = ja.
4. **Eingang buchen:** Aktion **Eingang buchen**. Rückfrage **Eingang buchen?** bestätigen. Voraussetzung: Status **In Bearbeitung**, gefülltes **Buchungsdatum (Eingang)** und mindestens eine Gruppierung mit **Eingangsmenge** ungleich null. Das System bucht den Wareneingang der im Hintergrund geführten **Einkaufsbestellung**, erzeugt einen Posten der **Postenart Eingang** (Geb. Belegart **Lieferung**) und führt **Geb. Eingangsmenge** nach. Ist eine Gruppierung vollständig eingegangen, wird der zugehörige **FA-Arbeitsgang** automatisch **Beendet** gemeldet.
5. **Abrechnung buchen:** Aktion **Abrechnung buchen**. Rückfrage **Abrechnung buchen?** bestätigen. Voraussetzung: gefülltes **Buchungsdatum (Abrechnung)** und offene **Menge zu fakturieren** oder offener **Betrag zu fakturieren** (bei Zu-/Abschlägen). Das System bucht je **Externe Rechnungsnr.** und **Zlg.-Bedingungscode** eine Einkaufsrechnung, erzeugt Posten der **Postenart Abrechnung** und stellt anschließend die Frage **Fremdarbeitenauftrag auf Status „Abgerechnet“ setzen?**. Bei bereits abgerechneten Belegen erscheint zusätzlich **Fremdarbeitenauftrag bereits abgerechnet. Abrechnung fortsetzen?**.
6. **Abschluss/Korrektur:** Über **Abgerechnet** wird der Beleg manuell auf **Abgerechnet** gesetzt; über **Status zurücksetzen** gelangt er zurück nach **Offen** (nur aus **Freigegeben**, **In Bearbeitung** oder **Abgerechnet**). Die Aktion **Stornieren** (Status **Storniert**) ist standardmäßig ausgeblendet.

**Teilmengen:** Aus- und Eingang sowie Abrechnung sind **teilmengenfähig**. Der Anwender kann in mehreren Durchläufen buchen; das System führt die offenen Mengen (Eingangsmenge, Menge zu fakturieren) nach jeder Buchung automatisch nach. Ein Zwang, den Beleg erst bei vollständigem Mengenausgleich zu schließen, besteht nicht.

## Historie: Fremdarbeitenauftragsposten

**Einstieg:** Auf dem Beleg **Fremdarbeitenauftrag** die Aktion **Posten**. Die Liste **Fremdarbeitenauftragsposten** protokolliert schreibgeschützt jeden Aus-, Eingangs- und Abrechnungsvorgang.

| Feld | Erläuterung |
|---|---|
| **Lfd. Nr.** | Fortlaufende Postennummer. |
| **Belegnr.** | Fremdarbeitenauftrag, zu dem der Posten gehört. |
| **Beleggruppenzeilennr.** | Betroffene Gruppierung. |
| **Postenart** | Vorgangsart. **Ausgang:** Warenausgang an den Kreditor; **Eingang:** Wareneingang vom Kreditor; **Abrechnung:** Fakturierung. |
| **Buchungsdatum** | Buchungsdatum des Vorgangs. |
| **Menge** | Gebuchte Menge. |
| **Geb. Belegart** | Art des erzeugten gebuchten Belegs. **(leer):** kein gebuchter Beleg; **Lieferung:** gebuchter Wareneingang; **Rechnung:** gebuchte Einkaufsrechnung. |
| **Geb. Belegnr.** | Nummer des erzeugten gebuchten Belegs. |
| **Einkaufsbestellnr.** | Zugehörige Einkaufsbestellung. |
| **Buchungsnr.** | Interne Buchungslaufnummer (fasst zusammengehörige Posten zusammen). |
| **Berechnungsart** | Art der Abrechnungsposition. **(leer):** keine Abrechnung; **Gruppierungszeile:** Abrechnung einer Gruppierungsmenge; **Zu-/Abschlag:** Abrechnung eines Zu-/Abschlags. |
| **Fakturierter Betrag** | Fakturierter Betrag des Postens. |
| **Rechnungsbetrag fixiert** | Wenn gesetzt, dann wurde der Rechnungsbetrag manuell fixiert und nicht aus Menge × Preis abgeleitet. |
| **Fakturiert Zu-/Abschlagsbetrag** | Fakturierter Zu-/Abschlagsanteil. |
| **Externe Rechnungsnr.** | Externe Rechnungsnummer des Kreditors. |
| **Zlg.-Bedingungscode** | Zahlungsbedingung des Abrechnungspostens. |

Aktion **Geb. Beleg anzeigen:** Öffnet je nach **Geb. Belegart** die **Gebuchte Einkaufslieferung** (Lieferung) oder die **Gebuchte Einkaufsrechnung** (Rechnung).

## Typische Anwendungsfälle

### Fall 1: Fremdbearbeitung aus einem Verkaufsauftrag

**Auslöser:** Ein Kunde bestellt einen Artikel, dessen Bearbeitung (z. B. Beschichten, Härten) an einen externen Lohnbearbeiter vergeben werden soll. Der Vertrieb hat den Verkaufsauftrag bereits erfasst.

**Einstieg in BC:** Der Anwender öffnet den **Verkaufsauftrag**, markiert in den Verkaufsauftragszeilen die betreffende Zeile und wählt die Aktion **Fremdarbeitenauftrag erstellen**. Ist noch keine Fremdarbeitsplatzgruppe vorgegeben, bietet das System die Arbeitsplatzgruppen mit hinterlegtem Kreditor zur Auswahl an.

**Kernablauf:**

1. Das System legt einen **Fremdarbeitenauftrag** (Status **Offen**) an, übernimmt Kreditor (aus der Arbeitsplatzgruppe), Artikel, Menge und die Verknüpfung zum Verkaufsauftrag in die **Auftragszeile**.
2. Der Anwender ergänzt auf dem Beleg die **Gruppierungen** (Menge, Preis, ggf. **Zu-/Abschläge**) sowie **Ausgangsdatum**/**Eingangsdatum** und Lagerorte.
3. Aktion **Freigeben** (Status **Freigegeben**).
4. Aktion **Ausgang buchen** → Rückfrage **Ausgang buchen?** bestätigen (Status **In Bearbeitung**).
5. Nach Rücklieferung Aktion **Eingang buchen** → Rückfrage **Eingang buchen?** bestätigen.
6. Aktion **Abrechnung buchen** → Rückfrage **Abrechnung buchen?** bestätigen; anschließend **Fremdarbeitenauftrag auf Status „Abgerechnet“ setzen?** bejahen.

**Abschluss:** Über **Posten** kontrolliert der Anwender die entstandenen Fremdarbeitenauftragsposten (Ausgang, Eingang, Abrechnung) und öffnet über **Geb. Beleg anzeigen** die gebuchte Einkaufsrechnung. Optional druckt er zuvor **Fremdarbeitslieferschein** und **Abholschein**.

### Fall 2: Fremdarbeitsgang aus einem freigegebenen Fertigungsauftrag

**Auslöser:** In einem freigegebenen Fertigungsauftrag ist ein Arbeitsgang an einer Arbeitsplatzgruppe hinterlegt, deren Feld **Kreditor** gefüllt ist — dieser Arbeitsgang wird extern ausgeführt.

**Einstieg in BC:** Beim Anlegen bzw. Ändern des Fertigungsarbeitsgangs an der Fremdarbeitsplatzgruppe ergänzt das Modul automatisch die passende **Auftragszeile** im Fremdarbeitenauftrag (bzw. legt bei Bedarf einen neuen Fremdarbeitenauftrag an). Der Anwender öffnet den Beleg über **Fremdarbeitenaufträge** oder aus der Fertigungsauftragszeile.

**Kernablauf:**

1. In den **Gruppierungen** prüft der Anwender die Menge und den **Preis** der Bearbeitung; bei Materialbeistellung erzeugt er über **Einkaufsbestellung erstellen** oder **Fertigungsauftrag erstellen** die Herkunftsbelege.
2. Der Anwender setzt die **Ausgangsmenge**, gibt den Beleg über **Freigeben** frei und bucht mit **Ausgang buchen** den Warenausgang an den Kreditor.
3. Nach Fertigmeldung und Rücklieferung bucht er mit **Eingang buchen** den Wareneingang; das Modul meldet den zugehörigen **FA-Arbeitsgang** bei vollständigem Eingang automatisch **Beendet** (sichtbar am **FA-Arbeitsvorratstatus**).
4. Mit **Abrechnung buchen** entsteht die Einkaufsrechnung für die Bearbeitungsleistung.

**Abschluss:** Der Fortschritt ist an **Herkunft FA-Prozessstatus** (Teilweise gefertigt/Gefertigt) und am **Status** des Belegs ablesbar; die Posten liegen in **Fremdarbeitenauftragsposten**.

## FAQ und Troubleshooting

### Warum lässt sich kein neuer Fremdarbeitenauftrag anlegen?
In der **Fremdarbeitenauftrag Einrichtung** ist keine Nummernserie im Feld **Fremdarbeitenauftragsnummern** hinterlegt. Ohne diese Serie kann die **Nr.** nicht vergeben werden und die Anlage bricht ab. Der Administrator trägt die Serie ein (siehe **Nummernserie einrichten**).

### Warum kann ich die Zeilen nicht mehr ändern?
Sobald der Beleg über **Freigeben** den Status **Freigegeben** (oder **In Bearbeitung**) hat, sind Kopf, Auftragszeilen und Gruppierungen gesperrt; das System meldet „Status muss ‚Offen‘ sein!“. Über **Status zurücksetzen** gelangt der Beleg zurück nach **Offen**, danach ist die Bearbeitung wieder möglich.

### Warum erscheint beim Buchen „Es gibt nichts zu buchen!“?
Für den gewählten Vorgang gibt es keine offene Menge: Beim **Ausgang buchen** ist in keiner Gruppierung eine **Ausgangsmenge** gesetzt, beim **Eingang buchen** keine **Eingangsmenge** und beim **Abrechnung buchen** weder **Menge zu fakturieren** noch **Betrag zu fakturieren**. Der Anwender trägt die entsprechende Menge in der Gruppierung ein.

### Warum kann ich den Eingang nicht buchen?
**Eingang buchen** setzt den Status **In Bearbeitung** voraus, der erst durch das vorherige **Ausgang buchen** entsteht. Zusätzlich muss das **Buchungsdatum (Eingang)** gefüllt sein. Ist der Status noch **Freigegeben**, zuerst den Ausgang buchen.

### Was passiert, wenn ein Arbeitsgang für die Bearbeitung fehlt?
Beim Ausgang prüft das System, ob jede Auftragszeile einem freigegebenen FA-Arbeitsgang zugeordnet ist. Fehlt die Zuordnung, erscheint „Eine oder mehrere Auftragszeilen haben keinen zugeordneten FA-Arbeitsgang!“ bzw. „Keine passende FA-Arbeitsgangzeile gefunden!“. Der Anwender ordnet in der Auftragszeile **FA-Nr.**, **FA-Zeilennr.** und **FA-Arbeitsgangnr.** korrekt zu.

### Warum wird eine Gruppierung als „Gefertigt“ oder „Geliefert“ angezeigt, obwohl ich nichts gebucht habe?
Die Felder **Herkunft FA-Prozessstatus** und **Herkunft Bestell-Prozessstatus** spiegeln automatisch den Fortschritt der Herkunftsbelege: Bei Fertigungsausgabe (Artikelposten „Ist-Meldung“) wechselt der Status auf **Teilweise gefertigt**/**Gefertigt**, bei Wareneingang der Herkunftsbestellung auf **Teilweise geliefert**/**Geliefert**. Diese Werte sind Anzeigefelder und werden vom System gepflegt.

### Warum ändert sich mein eingegebener Abrechnungsbetrag nicht mehr automatisch?
Sobald **Betrag zu fakturieren** manuell erfasst wird, aktiviert das System **Fixer Betrag zu fakturieren**. Wenn dieses Kennzeichen gesetzt ist, dann bleibt der eingegebene Betrag fixiert und wird bei Änderungen von Menge oder Preis nicht überschrieben. Zum Zurücksetzen das Kennzeichen entfernen bzw. die Menge zu fakturieren neu validieren.

### Wie werden mehrere Rechnungen eines Kreditors getrennt abgerechnet?
Bei der Abrechnung fasst das System die Positionen je **Externe Rechnungsnr.** und **Zlg.-Bedingungscode** zu getrennten Einkaufsrechnungen zusammen. Trägt der Anwender in den Gruppierungen bzw. Zu-/Abschlägen unterschiedliche externe Rechnungsnummern oder Zahlungsbedingungen ein, entstehen entsprechend mehrere Rechnungen. Für dieselbe Zu-/Abschlagsreferenz sind abweichende Zahlungsbedingungen oder Buchungsgruppen nicht zulässig.

### Warum finde ich die zugewiesenen Chargen/Seriennummern nur teilweise?
Die **Chargen/Seriennummernzeilen** entstehen automatisch aus den Artikelposten der Fertigung (Ausgabe) und der Wareneingänge. Erst nach den entsprechenden Buchungen erhöht sich der Zähler **Zugew. Chargen/Seriennr.** in der Gruppierung; über dessen Drilldown öffnet sich die vollständige Liste. Vor der Buchung sind noch keine Zeilen vorhanden.

### Warum steht auf dem Beleg eine Einkaufsbestellnummer, die ich nicht angelegt habe?
Das Modul führt für den Wareneingang und die Abrechnung im Hintergrund eine **Einkaufsbestellung**; ihre Nummer erscheint schreibgeschützt im Feld **Einkaufsbestellnr.**. Diese Bestellung wird beim Buchen automatisch bewirtschaftet und beim Löschen des Fremdarbeitenauftrags wieder entfernt. Über **Einkaufsbestellung anzeigen** kann der Anwender sie einsehen.
