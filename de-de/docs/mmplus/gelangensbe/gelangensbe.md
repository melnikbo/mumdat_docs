---
title: Anwenderhandbuch m+m Certificate of Supply
---

# Anwenderhandbuch m+m Certificate of Supply

## Einleitung

Die Erweiterung **m+m Certificate of Supply** ergänzt Microsoft Dynamics 365 Business Central um die vollständige Bearbeitung der **Gelangensbestätigung**. Eine Gelangensbestätigung weist bei innergemeinschaftlichen Lieferungen nach, dass die Ware tatsächlich in einen anderen EU‑Mitgliedstaat gelangt ist. Dieser Nachweis ist Voraussetzung für die Steuerfreiheit der Lieferung.

Die Erweiterung erzeugt Gelangensbestätigungen **automatisch beim Buchen** von Lieferbelegen und stellt eine eigene Liste **Gelangensbestätigungen** bereit, in der die Belege zusammengefasst, gedruckt, per Mail versendet, angemahnt und auf **Empfangen** gesetzt werden. Betroffen sind drei Belegarten:

- **Verkaufslieferung** (Debitor)
- **Servicelieferung** (Debitor)
- **Rücklieferung** aus dem Einkauf (Kreditor)

**Zielgruppe.** Primäre Anwender sind die **operativen Sachbearbeiter** in Vertrieb, Versand und Debitoren‑/Kreditorenbuchhaltung, die täglich Gelangensbestätigungen drucken, versenden, auf Empfangen setzen und offene Bestätigungen anmahnen. **Administratoren** und Key‑User sind sekundäre Zielgruppe; sie richten Nummernserie, Fälligkeitsformeln und die auslösende MwSt.‑Kennzeichnung ein.

**Kurzer Prozessüberblick.** Der Anwender bucht wie gewohnt eine Lieferung. Ist für die MwSt.‑Kombination der Zeile die Kennzeichnung **Gelangensbestätigung erforderlich** gesetzt, legt die Erweiterung automatisch eine Gelangensbestätigung mit Status **Erforderlich** an. In der Liste **Gelangensbestätigungen** fasst der Anwender die Belege je Empfänger optional zu einer **Zertifikatsnr.** zusammen, druckt sie oder versendet sie per Mail und setzt sie nach Rücklauf auf **Empfangen**. Nicht zurückgekehrte Bestätigungen werden über **Mahnung** und **Sammelmahnung** nachverfolgt.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg vom eingerichteten System bis zur empfangenen Gelangensbestätigung. Die Einrichtung ist Voraussetzung und steht daher zuerst (siehe Kapitel **Einrichtung**).

1. **Einrichtung prüfen (einmalig, Administrator).** In der **Gelangensbestätigungseinrichtung** sind eine **Nummernserie Gelangensbestätigungen** und eine **Standard Fälligkeitsberechnungsformel** hinterlegt; in der **MwSt.‑Buchungsmatrix Einrichtung** ist für die betroffenen Kombinationen **Gelangensbestätigung erforderlich** aktiviert.
2. **Lieferung buchen.** Buchen Sie eine **Verkaufslieferung**, **Servicelieferung** oder **Rücklieferung** im Standard von Business Central. Für Zeilen mit der Kennzeichnung **Gelangensbestätigung erforderlich** entsteht automatisch eine Gelangensbestätigung mit Status **Erforderlich**.
3. **Liste öffnen.** Geben Sie über **Suchen** den Begriff `Gelangensbestätigungen` ein und öffnen Sie den gleichnamigen Link. Es erscheint die Liste **Gelangensbestätigungen**.
4. **Zusammenfassen (optional).** Markieren Sie mehrere Zeilen desselben Empfängers und wählen Sie **Gelangensbestätigungen zusammenfassen**. Alle markierten Belege erhalten dieselbe **Zertifikatsnr.** und können gemeinsam gedruckt werden.
5. **Drucken.** Wählen Sie **Gelangensbestätigung drucken** (Einzelbeleg) oder **Sammeldruck Gelangensbestätigung** (zusammengefasste Belege). Der Druck setzt den Status auf **Nicht empfangen**, vermerkt das **Zertifikatsdatum** und ermittelt das **Fälligkeitsdatum**.
6. **Versenden (alternativ zum Druck).** Wählen Sie **Gelangensbestätigung per Mail senden** oder **Sammelgelangensbestätigung per Mail senden**.
7. **Empfang buchen.** Kommt die unterschriebene Bestätigung zurück, markieren Sie die Zeile(n) und wählen **Gelangensbestätigung erhalten**. Der Status wechselt auf **Empfangen** und das **Empfangsdatum** wird gesetzt.
8. **Anmahnen (bei Verzug).** Für überfällige Belege wählen Sie **Mahnung** bzw. **Sammelmahnung** oder deren Mail‑Varianten.

## Einrichtung

Die Einrichtung erfolgt vor der ersten Nutzung und in Abhängigkeitsreihenfolge: zuerst die **Gelangensbestätigungseinrichtung** (Nummernserie, Standardfälligkeit), danach je Bedarf die **Fälligkeitsformel an der Lieferbedingung**, anschließend die auslösende Kennzeichnung in der **MwSt.‑Buchungsmatrix Einrichtung**. Die Druck‑ und Mailberichte werden bei der Installation automatisch zugeordnet.

### Gelangensbestätigungseinrichtung

**Einstieg:** Geben Sie über **Suchen** den Begriff `Gelangensbestätigungseinrichtung` ein und öffnen Sie den gleichnamigen Link. Es handelt sich um eine unternehmensweite Einrichtungskarte (ein Datensatz je Mandant); sie wird beim ersten Öffnen automatisch angelegt.

**Prozess.** Der Administrator richtet hier einmalig die zentralen Vorgaben ein, die für **alle** Gelangensbestätigungen gelten: die Nummernserie für Sammelbelege und die Standardvorgabe für die Fälligkeit. Diese Werte greifen später beim Zusammenfassen (Kapitel **Anwendung**) und beim Ermitteln des Fälligkeitsdatums (Kapitel **Fälligkeit und Mahnwesen einrichten**).

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Nummernserie Gelangensbestätigungen** | Wenn eine Nummernserie hinterlegt ist, wird beim **Zusammenfassen** mehrerer Gelangensbestätigungen automatisch eine fortlaufende **Zertifikatsnr.** je Empfängergruppe vergeben; ohne Nummernserie kann nicht zusammengefasst werden, und der Aufruf **Gelangensbestätigungen zusammenfassen** bricht mit einer Fehlermeldung ab. |
| **Standard Fälligkeitsberechnungsformel** | Wenn eine Datumsformel (z. B. `14T`) gesetzt ist, wird beim Druck einer Gelangensbestätigung das **Fälligkeitsdatum** als Arbeitsdatum plus Formel berechnet; ab diesem Datum gilt die Bestätigung als überfällig und geht in den Mahnlauf ein. Ist an der jeweiligen **Lieferbedingung** eine eigene Fälligkeitsformel hinterlegt, hat diese Vorrang. Ist gar keine Formel hinterlegt, wird das Arbeitsdatum als Fälligkeitsdatum verwendet. |

### Fälligkeitsformel an der Lieferbedingung

**Einstieg:** Geben Sie über **Suchen** den Begriff `Lieferbedingungen` ein und öffnen Sie den gleichnamigen Link. Bearbeiten Sie die gewünschte **Lieferbedingung** direkt in der Zeile.

**Prozess.** Der Administrator legt hier fest, ob eine bestimmte Lieferbedingung eine **abweichende** Fälligkeit erhalten soll. Die Erweiterung fügt der Lieferbedingung dazu ein zusätzliches Feld hinzu. Diese pro‑Lieferbedingung gepflegte Formel übersteuert die zentrale **Standard Fälligkeitsberechnungsformel** aus der Gelangensbestätigungseinrichtung und wirkt beim Druck (Kapitel **Anwendung**).

| Feld | Erläuterung |
|------|-------------|
| **Code** | Identifiziert die Lieferbedingung (Standardfeld). Wird als **Lieferbedingungscode** auf die Gelangensbestätigung übernommen und steuert, welche Fälligkeitsformel greift. |
| **Beschreibung** | Klartextbezeichnung der Lieferbedingung (Standardfeld). |
| **Fälligkeitsformel (Gelangensbestätigung)** | Wenn hier eine Datumsformel gesetzt ist, wird das **Fälligkeitsdatum** von Gelangensbestätigungen mit dieser Lieferbedingung über diese Formel berechnet und die zentrale Standardformel übersteuert; ist das Feld leer, greift die **Standard Fälligkeitsberechnungsformel** der Gelangensbestätigungseinrichtung. Ist das Feld in der Ansicht nicht sichtbar, blenden Sie es über **Personalisieren** ein. |

### Automatische Erstellung von Gelangensbestätigungen einrichten

Damit überhaupt Gelangensbestätigungen entstehen, muss der Administrator die auslösende Kennzeichnung in der MwSt.‑Buchungsmatrix setzen. Ohne diesen Schritt bucht der Anwender zwar Lieferungen, es werden aber keine Bestätigungen erzeugt.

1. **MwSt.‑Buchungsmatrix Einrichtung öffnen.** Geben Sie über **Suchen** den Begriff `MwSt.-Buchungsmatrix Einr.` ein und öffnen Sie den gleichnamigen Link. Die Matrix enthält je Zeile eine Kombination aus **MwSt.‑Geschäftsbuchungsgruppe** und **MwSt.‑Produktbuchungsgruppe**.
2. **Auslösekennzeichen setzen.** Aktivieren Sie für jede betroffene Kombination das Feld **Gelangensbestätigung erforderlich**.

   | Einrichtung | Erläuterung |
   |-------------|-------------|
   | **MwSt.‑Geschäftsbuchungsgruppe** | Bestimmt zusammen mit der Produktbuchungsgruppe, für welche Geschäftsvorfälle die Regel gilt (Standardfeld). |
   | **MwSt.‑Produktbuchungsgruppe** | Ergänzt die Geschäftsbuchungsgruppe zur eindeutigen Kombination (Standardfeld). |
   | **Gelangensbestätigung erforderlich** | Wenn aktiviert, erzeugt Business Central beim Buchen einer Lieferung für Zeilen dieser MwSt.‑Kombination automatisch eine Gelangensbestätigung mit Status **Erforderlich**; ist das Kennzeichen nicht gesetzt, entsteht keine Bestätigung. Zusätzlich verhindert die Erweiterung bei aktivem Kennzeichen das **direkte Fakturieren** ohne separate Lieferung (siehe Prozesshinweis unten). Ist das Feld nicht sichtbar, blenden Sie es über **Personalisieren** ein. |
3. **Wirkung im Tagesablauf.** Nach dem Setzen des Kennzeichens entsteht bei jeder gebuchten **Verkaufslieferung**, **Servicelieferung** oder **Rücklieferung** mit passender MwSt.‑Kombination automatisch eine Zeile in der Liste **Gelangensbestätigungen** (Kapitel **Anwendung**).

**Prozesshinweis (Validierung aus dem Code).** Ist für eine Zeile **Gelangensbestätigung erforderlich** gesetzt, lässt Business Central das **direkte Fakturieren** (Buchen mit Fakturieren ohne getrennte Lieferung) nicht zu; der Beleg muss zuerst **geliefert** und danach fakturiert werden. Andernfalls erscheint eine Fehlermeldung mit dem Hinweis, den Weg über die Verkaufsrechnung zu nutzen. So ist sichergestellt, dass zu jeder steuerfreien Lieferung eine Gelangensbestätigung angelegt wird.

### Fälligkeit und Mahnwesen einrichten

Diese Einrichtung steuert, **wann** eine Gelangensbestätigung als überfällig gilt und in Mahnungen erscheint. Sie wird vom Administrator vor der ersten Nutzung vorgenommen und wirkt in der täglichen Arbeit beim Druck und bei den Mahnaktionen (Kapitel **Anwendung**).

1. **Zentrale Fälligkeit festlegen.** Hinterlegen Sie in der **Gelangensbestätigungseinrichtung** die **Standard Fälligkeitsberechnungsformel** (z. B. `14T`). Wenn gesetzt, wird daraus beim Druck das **Fälligkeitsdatum** berechnet.
2. **Abweichende Fälligkeit je Lieferbedingung (optional).** Hinterlegen Sie an einzelnen **Lieferbedingungen** die **Fälligkeitsformel (Gelangensbestätigung)**. Wenn gesetzt, übersteuert sie für Belege mit dieser Lieferbedingung die zentrale Formel.
3. **Nummernserie für Sammelbelege.** Hinterlegen Sie in der Gelangensbestätigungseinrichtung die **Nummernserie Gelangensbestätigungen**, damit beim **Zusammenfassen** eine **Zertifikatsnr.** vergeben werden kann.
4. **Abschluss im Tagesablauf.** Der Anwender druckt Bestätigungen (setzt Status **Nicht empfangen** und **Fälligkeitsdatum**) und mahnt überfällige Belege über **Mahnung**/**Sammelmahnung** an; das Feld **Mahnstufe erhöhen** auf dem Anforderungsdialog erhöht die **Mahnstufe** (Querverweis: Kapitel **Anwendung**).

### Berichte zuordnen

Für den Druck und den Mailversand nutzt die Erweiterung zwei eigene m+m‑Berichte: einen für die **Gelangensbestätigung** und einen für die **Gelangensbestätigungsmahnung**. Diese Berichtszuordnung wird bei der **Installation** der Erweiterung automatisch angelegt; ein manueller Einrichtungsschritt ist im Normalfall nicht erforderlich. Sollen abweichende oder mehrsprachige Layouts (die Gelangensbestätigung ist zusätzlich in französischer Sprache verfügbar) verwendet werden, passt der Administrator die Zuordnung in der Standard‑Berichtsauswahl von Business Central an.

## Anwendung — tägliche Arbeit mit Gelangensbestätigungen

Sind über gebuchte Geschäftsvorfälle Gelangensbestätigungen entstanden, bearbeitet der Anwender sie in der Liste **Gelangensbestätigungen**.

**Einstieg:** Geben Sie über **Suchen** den Begriff `Gelangensbestätigungen` ein und öffnen Sie den gleichnamigen Link. Business Central zeigt die von der Erweiterung bereitgestellte Liste **Gelangensbestätigungen** mit allen erzeugten Bestätigungen an.

**Bezug zur Einrichtung.** Welche Zeilen hier erscheinen, steuert die Kennzeichnung **Gelangensbestätigung erforderlich** in der **MwSt.‑Buchungsmatrix Einrichtung**; das **Fälligkeitsdatum** ergibt sich aus den Fälligkeitsformeln der **Gelangensbestätigungseinrichtung** bzw. der **Lieferbedingung**; die **Zertifikatsnr.** stammt aus der **Nummernserie Gelangensbestätigungen** (Kapitel **Einrichtung**).

### Felder der Liste Gelangensbestätigungen

Die Liste ist schreibgeschützt; alle Werte werden aus dem gebuchten Lieferbeleg übernommen bzw. durch die Aktionen gesetzt.

| Feld | Erläuterung |
|------|-------------|
| **Belegart** | Herkunftsbelegart der Bestätigung. **Verkaufslieferung:** aus einer gebuchten Verkaufslieferung (Debitor). **Servicelieferung:** aus einer gebuchten Servicelieferung (Debitor). **Rücklieferung:** aus einer gebuchten Rücklieferung im Einkauf (Kreditor). Die Belegart bestimmt, aus welchem Quellbeleg Adress- und Mengendaten stammen. |
| **Belegnr.** | Nummer des gebuchten Lieferbelegs, zu dem die Bestätigung gehört. Zusammen mit der Belegart identifiziert sie die Bestätigung eindeutig. |
| **Status** | Steuert den Bearbeitungsstand und die erlaubten Folgeaktionen. **Nicht zutreffend:** keine Gelangensbestätigung erforderlich; das Feld **Nr.** und die **Zertifikatsnr.** bleiben leer. **Erforderlich:** Bestätigung ist angelegt, aber noch nicht gedruckt; sie kann zusammengefasst und gedruckt werden. **Empfangen:** die unterschriebene Bestätigung liegt vor; **Empfangsdatum** und **Wareneingangsdatum** sind gesetzt, weitere Änderungen sind gesperrt. **Nicht empfangen:** Bestätigung wurde gedruckt bzw. versendet, ist aber noch nicht zurückgekehrt; nur dieser Status geht in Mahnungen ein. Wird der Status manuell von **Empfangen** zurückgesetzt, erscheint eine Sicherheitsabfrage. |
| **Nr.** | Belegnummer der Gelangensbestätigung. Bei Status **Nicht zutreffend** muss das Feld leer sein; bei **Erforderlich**, **Empfangen** oder **Nicht empfangen** darf es nicht leer sein (Validierung aus dem Code). |
| **Wareneingangsdatum** | Datum, an dem die Bestätigung auf **Empfangen** gesetzt wurde. Beim Setzen auf **Empfangen** übernimmt die Aktion das **Liefer‑/Buchungsdatum**; das Wareneingangsdatum darf nicht vor dem Liefer‑/Buchungsdatum liegen. |
| **Gedruckt** | Wenn gesetzt, wurde die Bestätigung bereits gedruckt oder per Mail versendet; erst danach lässt sich der Empfang buchen. |
| **Debitoren‑/Kreditorenname** | Name des Empfängers, übernommen aus dem Quellbeleg. |
| **Lieferbedingungscode** | Lieferbedingung des Quellbelegs; steuert, welche **Fälligkeitsformel (Gelangensbestätigung)** beim Druck greift. |
| **Liefer‑/Buchungsdatum** | Buchungsdatum der zugrunde liegenden Lieferung; dient als Untergrenze für das Wareneingangsdatum. |
| **Lief. an Länder‑/Regionscode** | Zielland der Lieferung; bei innergemeinschaftlichen Lieferungen der EU‑Mitgliedstaat, in den die Ware gelangt. |
| **Debitoren‑/Kreditorennr.** | Nummer des Empfängers; zusammen mit dem **Lief. an Code** bildet sie die Gruppe für das Zusammenfassen zu einer **Zertifikatsnr.** |
| **Steuernummer des Fahrzeugs** | Erfassbare Fahrzeugkennung für den Nachweis. Bei Status **Empfangen** kann dieses Feld nicht mehr geändert werden (Validierung aus dem Code). |
| **Herkunftsnr.** | Belegnummer des auslösenden Geschäftsvorfalls, z. B. Verkaufsauftrag oder Bestellung. |
| **Fälligkeitsdatum** | Wird beim Druck aus der greifenden Fälligkeitsformel ermittelt; ab diesem Datum ist die Bestätigung überfällig. |
| **Mahnstufe** | Zählt, wie oft die Bestätigung angemahnt wurde; wird über den Mahnbericht bei Bedarf erhöht. |
| **Rechnungsnr.** | Zugehörige Rechnungsnummer des Geschäftsvorfalls; wird beim Fakturieren nachgetragen. |
| **Rechnungs‑/Buchungsdatum** | Rechnungs- bzw. Buchungsdatum des Rechnungsbelegs. |
| **Zertifikatsnr.** | Wird beim Zusammenfassen mehrerer Bestätigungen vergeben und in alle zusammengehörigen Zeilen eingetragen; ermöglicht den Sammeldruck und den Sammelversand. |
| **Zertifikatsdatum** | Datum, an dem der Sammelbeleg erstellt bzw. gedruckt wurde. |
| **Empfangsdatum** | Datum der Empfangsbestätigung; wird beim Setzen auf **Empfangen** gefüllt und beim Zurücksetzen wieder geleert. |
| **Art** | Empfängerart der Bestätigung. **Debitor:** aus Verkaufs- oder Servicelieferung; Adress- und Kontaktdaten stammen von Rechnungs‑/Lieferadresse des Debitors. **Kreditor:** aus einer Rücklieferung; Daten stammen vom Kreditor. Die Art steuert, an wen gedruckt und gemailt wird und welcher Sprachcode für den Bericht gilt. |
| **Lieferadresse** (Lief. an Name, Name 2, Kontakt, Code, Adresse, Adresse 2, Ort, PLZ‑Code, Land) | Read‑only übernommene Lieferanschrift des Quellbelegs; erscheint im Nachweis als Empfangsort. Wird als Feldgruppe geführt, da alle Werte gemeinsam aus dem Beleg stammen. |
| **Rechnungsadresse** (Rech. an Name, Name 2, Kontakt, Adresse, Adresse 2, Ort, PLZ‑Code, Land, Länder‑/Regionscode) | Read‑only übernommene Rechnungs‑/Zahlungsanschrift des Quellbelegs; benennt den bestätigenden Abnehmer. Wird als Feldgruppe geführt. |

Die Liste stellt keine eigenen Anforderungs- oder Tabellenfilter bereit; zum Eingrenzen nutzen Anwender die Standard‑Spaltenfilter von Business Central (z. B. nach **Status** = `Nicht empfangen` für offene Belege).

### Aktionen der Gelangensbestätigungen

Die folgenden Aktionen stehen im Menüband; die wichtigsten sind unter **Prozess** bzw. **Bericht** angeheftet.

| Aktion | Erläuterung |
|--------|-------------|
| **Gelangensbestätigungen zusammenfassen** | Fasst die markierten Bestätigungen mit Status **Nicht zutreffend** oder **Erforderlich** je Gruppe aus **Art**, **Debitoren‑/Kreditorennr.** und **Lief. an Code** zusammen und vergibt aus der **Nummernserie Gelangensbestätigungen** eine gemeinsame **Zertifikatsnr.** Anschließend kann direkt gedruckt oder per Mail versendet werden. Voraussetzung ist eine hinterlegte Nummernserie. |
| **Gelangensbestätigung drucken** | Druckt die markierte Einzelbestätigung. Der Druck setzt den Status von **Erforderlich**/**Nicht zutreffend** auf **Nicht empfangen**, vermerkt **Gedruckt**, das **Zertifikatsdatum** und ermittelt das **Fälligkeitsdatum**. |
| **Sammeldruck Gelangensbestätigung** | Druckt alle zu einer **Zertifikatsnr.** zusammengefassten Bestätigungen in einem Sammelbeleg. |
| **Gelangensbestätigung per Mail senden** | Versendet die Einzelbestätigung als Anhang per E‑Mail an den Empfänger (Debitor oder Kreditor). |
| **Sammelgelangensbestätigung per Mail senden** | Versendet die zu einer **Zertifikatsnr.** zusammengefassten Bestätigungen gemeinsam per E‑Mail. |
| **Gelangensbestätigung erhalten** | Setzt die markierten Bestätigungen auf Status **Empfangen**, füllt **Empfangsdatum** und übernimmt das **Liefer‑/Buchungsdatum** als **Wareneingangsdatum**. Gehören die Zeilen zu einer **Zertifikatsnr.**, fragt eine Sicherheitsabfrage, ob **alle** Belege dieses Sammelbelegs geändert werden sollen. |
| **Gelangensbestätigung erhalten zurücksetzen** | Setzt die markierten Bestätigungen von **Empfangen** wieder auf **Nicht empfangen**, leert **Empfangsdatum** und **Wareneingangsdatum**. Bei Sammelbelegen gilt dieselbe Sicherheitsabfrage wie beim Empfang. |
| **Mahnung** | Druckt eine Mahnung zu den markierten, noch nicht empfangenen Bestätigungen. |
| **Sammelmahnung** | Druckt eine Sammelmahnung zu den zu einer **Zertifikatsnr.** zusammengefassten, noch nicht empfangenen Bestätigungen. |
| **Mahnung per Mail senden** | Versendet die Mahnung zu einer Einzelbestätigung per E‑Mail. |
| **Sammelmahnung per Mail senden** | Versendet die Sammelmahnung per E‑Mail. |

### Buchungs- und Statusablauf

Dieser Ablauf spiegelt den im Code hinterlegten Ablauf und wird im **Schnellstart** sowie in **Nutzungsbeispiel 1** mit denselben Aktionsnamen wiederholt.

1. **Lieferung buchen** (Standard‑Business‑Central): Verkaufslieferung, Servicelieferung oder Rücklieferung. Für Zeilen mit **Gelangensbestätigung erforderlich** entsteht automatisch eine Bestätigung mit Status **Erforderlich**.
2. **Gelangensbestätigungen zusammenfassen** (optional): vergibt die **Zertifikatsnr.**
3. **Gelangensbestätigung drucken** oder **Sammeldruck Gelangensbestätigung**: Status wird **Nicht empfangen**, **Fälligkeitsdatum** und **Zertifikatsdatum** werden gesetzt, **Gedruckt** wird vermerkt.
4. Alternativ oder zusätzlich **Gelangensbestätigung per Mail senden** / **Sammelgelangensbestätigung per Mail senden**.
5. **Gelangensbestätigung erhalten**: Status **Empfangen**, **Empfangsdatum** und **Wareneingangsdatum** werden gesetzt; bei Sammelbelegen erscheint die Sicherheitsabfrage.
6. Bei Verzug: **Mahnung** / **Sammelmahnung**; das Feld **Mahnstufe erhöhen** im Anforderungsdialog erhöht die **Mahnstufe**.

Ein fester Mengenabgleich („nicht schließen, bis Menge stimmt“) existiert nicht; jede Bestätigung wird einzeln bzw. je Zertifikatsnr. auf Empfangen gesetzt.

## Bericht Gelangensbestätigung und Mahnung

### Bericht Gelangensbestätigung

Der Bericht **Gelangensbestätigung** erzeugt das amtliche Nachweisformular. Er ist nach **Debitoren‑/Kreditornr.** bzw. Lieferadresse und **Sprachcode** gruppiert und dient zugleich dem Sammelausdruck. Der Bericht wird über die Aktionen **Gelangensbestätigung drucken** und **Sammeldruck Gelangensbestätigung** aufgerufen.

Beim Aufruf stehen zwei Anforderungsoptionen zur Verfügung:

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Zeilendetails andrucken** | Wenn aktiviert, druckt der Bericht zusätzlich die Lieferscheinzeilen (Artikelnr., Beschreibung, Menge, Einheit); Zeilen mit Null‑Menge werden automatisch unterdrückt. Ohne Aktivierung erscheint nur die Kopfbestätigung. Bei Sammelbelegen (Aufruf mit **Zertifikatsnr.**) wird der Detaildruck automatisch eingeschaltet. |
| **Als gedruckt markieren** | Wenn aktiviert, wird die Bestätigung auch in der Seitenansicht als **Gedruckt** gekennzeichnet und auf **Nicht empfangen** gesetzt; ohne Aktivierung erfolgt diese Statusfortschreibung in der Vorschau nicht. |

Der Bericht ermittelt beim Druck über die greifende Fälligkeitsformel das **Fälligkeitsdatum**, setzt **Zertifikatsdatum** und **Gedruckt** und schreibt den Status auf **Nicht empfangen** fort. Der Ausdruck erfolgt in der Sprache des Empfängers (Sprachcode aus Debitor bzw. Kreditor).

### Bericht Gelangensbestätigungsmahnung

Der Bericht **Gelangensbestätigungsmahnung** erinnert Empfänger an noch nicht zurückgesandte Bestätigungen. Er berücksichtigt ausschließlich Bestätigungen mit Status **Nicht empfangen** und wird über **Mahnung**, **Sammelmahnung** und deren Mail‑Varianten aufgerufen.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Mahnstufe erhöhen** | Wenn aktiviert, erhöht der Mahnlauf beim tatsächlichen Druck (nicht in der Vorschau) die **Mahnstufe** der betroffenen Bestätigungen um eins; ohne Aktivierung wird die Mahnung gedruckt, die Mahnstufe bleibt jedoch unverändert. |

### Bericht Erstelle Gelangensbestätigungen

Der Bericht **Erstelle Gelangensbestätigungen** erzeugt nachträglich Bestätigungen für bereits gebuchte Lieferungen, für die noch keine Bestätigung existiert (z. B. bei Ersteinführung der Erweiterung im Altbestand). Er prüft je Beleg, ob für die MwSt.‑Kombination **Gelangensbestätigung erforderlich** gesetzt ist, und legt nur dann eine Bestätigung an.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Erstelle Bestätigungen für Lieferungen** | Wenn aktiviert, werden gebuchte Verkaufslieferungen berücksichtigt. |
| **Erstelle Bestätigungen für Rücklieferungen** | Wenn aktiviert, werden gebuchte Rücklieferungen (Einkauf) berücksichtigt. |
| **Erstelle Bestätigungen für Service‑Lieferungen** | Wenn aktiviert, werden gebuchte Servicelieferungen berücksichtigt. |

### Inhalt des Nachweisformulars

Das gedruckte Formular enthält den amtlichen Bestätigungstext (Einzahl bzw. Mehrzahl je nach Anzahl der Gegenstände), Name und Anschrift des Abnehmers, die Referenzbelege sowie – bei aktivem **Zeilendetails andrucken** – eine Zeilentabelle mit **Beschreibung**, **Artikelnr.**, **Menge** und **Einheit**. Musterausdrucke der Gelangensbestätigung und der Mahnung stehen in der offiziellen mumdat‑Handbuchseite zur Verfügung.

## FAQ und Troubleshooting

### Warum entsteht nach dem Buchen einer Lieferung keine Gelangensbestätigung?
Weil für die MwSt.‑Kombination der Lieferzeile die Kennzeichnung **Gelangensbestätigung erforderlich** in der **MwSt.‑Buchungsmatrix Einrichtung** nicht gesetzt ist. Nur für gekennzeichnete Kombinationen legt die Erweiterung automatisch eine Bestätigung an.

### Warum meldet Business Central beim direkten Fakturieren einen Fehler?
Ist **Gelangensbestätigung erforderlich** gesetzt, ist das Buchen mit Fakturieren ohne getrennte Lieferung gesperrt, weil der Vorgang eine Gelangensbestätigung erzeugen muss. Buchen Sie zuerst die Lieferung und fakturieren Sie anschließend über die Verkaufsrechnung.

### Warum lässt sich der Aufruf Gelangensbestätigungen zusammenfassen nicht ausführen?
Weil in der **Gelangensbestätigungseinrichtung** keine **Nummernserie Gelangensbestätigungen** hinterlegt ist. Ohne Nummernserie kann keine **Zertifikatsnr.** vergeben werden, und die Aktion bricht mit einer Fehlermeldung ab.

### Wie wird das Fälligkeitsdatum ermittelt?
Beim Druck: Ist an der **Lieferbedingung** eine **Fälligkeitsformel (Gelangensbestätigung)** hinterlegt, gilt diese. Andernfalls greift die **Standard Fälligkeitsberechnungsformel** aus der Gelangensbestätigungseinrichtung. Ist keine Formel hinterlegt, wird das Arbeitsdatum verwendet.

### Warum kann ich das Wareneingangsdatum nicht erfassen?
Das **Wareneingangsdatum** ist nur bei Status **Empfangen** erlaubt. Es wird beim Setzen auf **Empfangen** automatisch aus dem **Liefer‑/Buchungsdatum** übernommen und darf nicht vor diesem liegen. Bei anderen Status muss es leer bleiben.

### Was bedeuten die vier Status einer Gelangensbestätigung?
**Nicht zutreffend:** kein Nachweis nötig. **Erforderlich:** angelegt, noch nicht gedruckt. **Nicht empfangen:** gedruckt bzw. versendet, aber noch nicht zurückgekehrt. **Empfangen:** unterschriebene Bestätigung liegt vor. Nur **Nicht empfangen** geht in Mahnungen ein.

### Warum erscheint beim Setzen auf Empfangen eine Sicherheitsabfrage?
Gehört die Bestätigung zu einem Sammelbeleg (gemeinsame **Zertifikatsnr.**), fragt die Erweiterung, ob **alle** Belege dieser Zertifikatsnr. gemeinsam auf **Empfangen** gesetzt werden sollen. Bestätigen Sie, wenn der komplette Sammelbeleg zurückgekommen ist.

### Warum werden meine gebuchten Altlieferungen nicht in der Liste angezeigt?
Für Lieferungen, die vor Aktivierung der Kennzeichnung gebucht wurden, entstehen keine Bestätigungen automatisch. Nutzen Sie den Bericht **Erstelle Gelangensbestätigungen**, um sie für den Altbestand nachträglich anzulegen.

### Warum erhöht sich die Mahnstufe nach dem Mahnungsdruck nicht?
Nur wenn im Anforderungsdialog das Feld **Mahnstufe erhöhen** aktiviert ist und der Bericht **tatsächlich gedruckt** (nicht nur in der Vorschau angezeigt) wird, erhöht sich die **Mahnstufe**.

### In welcher Sprache wird die Gelangensbestätigung gedruckt?
Der Bericht verwendet den **Sprachcode** des Empfängers (Debitor bzw. Kreditor). Die Gelangensbestätigung steht zusätzlich in französischer Sprache zur Verfügung.

## Typische Anwendungsfälle

### Anwendungsfall 1: EU‑Verkaufslieferung nachweisen

**Auslöser.** Der Vertrieb liefert Waren an einen Kunden in einem anderen EU‑Mitgliedstaat; die Lieferung ist steuerfrei und muss durch eine Gelangensbestätigung belegt werden.

**Einstieg in BC.** Der Sachbearbeiter bucht die **Verkaufslieferung** im Standard. Da für die MwSt.‑Kombination **Gelangensbestätigung erforderlich** gesetzt ist, entsteht automatisch eine Bestätigung mit Status **Erforderlich**. Über **Suchen** öffnet er die Liste **Gelangensbestätigungen**.

**Kernablauf.** Der Sachbearbeiter markiert die zusammengehörigen Belege des Kunden und wählt **Gelangensbestätigungen zusammenfassen** (gemeinsame **Zertifikatsnr.**). Anschließend wählt er **Gelangensbestätigung drucken** bzw. **Sammeldruck Gelangensbestätigung** — der Status wechselt auf **Nicht empfangen**, **Fälligkeitsdatum** und **Zertifikatsdatum** werden gesetzt. Alternativ versendet er das Formular über **Gelangensbestätigung per Mail senden** direkt an den Kunden.

**Abschluss.** Kommt die unterschriebene Bestätigung zurück, markiert er die Zeile und wählt **Gelangensbestätigung erhalten**; der Status wird **Empfangen**, **Empfangsdatum** und **Wareneingangsdatum** werden gesetzt. Der Nachweis ist damit dokumentiert.

### Anwendungsfall 2: Offene Bestätigungen anmahnen

**Auslöser.** Beim wöchentlichen Prüflauf stellt die Buchhaltung fest, dass mehrere gedruckte Gelangensbestätigungen nach Ablauf des **Fälligkeitsdatums** noch nicht zurückgekommen sind.

**Einstieg in BC.** Über **Suchen** öffnet die Sachbearbeiterin die Liste **Gelangensbestätigungen** und filtert die Spalte **Status** auf `Nicht empfangen`.

**Kernablauf.** Sie markiert die überfälligen Belege und wählt **Mahnung** (Einzelbeleg) bzw. **Sammelmahnung** (zu einer **Zertifikatsnr.** zusammengefasst). Im Anforderungsdialog lässt sie **Mahnstufe erhöhen** aktiviert, damit die **Mahnstufe** je Mahnlauf steigt. Für den elektronischen Versand nutzt sie **Mahnung per Mail senden** bzw. **Sammelmahnung per Mail senden**.

**Abschluss.** Die Mahnung wird gedruckt bzw. gemailt, die **Mahnstufe** ist erhöht. Trifft die Bestätigung ein, setzt sie den Beleg über **Gelangensbestätigung erhalten** auf **Empfangen**.

### Anwendungsfall 3: Rücklieferung an einen Lieferanten belegen

**Auslöser.** Aus dem Einkauf wird Ware an einen Lieferanten in einem anderen EU‑Mitgliedstaat zurückgesandt; auch hierfür ist ein Gelangensnachweis erforderlich.

**Einstieg in BC.** Der Einkaufssachbearbeiter bucht die **Rücklieferung** im Standard. Für gekennzeichnete MwSt.‑Kombinationen entsteht automatisch eine Bestätigung mit **Art** = **Kreditor**. Über **Suchen** öffnet er die Liste **Gelangensbestätigungen**.

**Kernablauf.** Er prüft die aus der Rücklieferung übernommenen Adressdaten, fasst bei Bedarf mehrere Belege desselben Lieferanten über **Gelangensbestätigungen zusammenfassen** zusammen und versendet den Nachweis über **Gelangensbestätigung per Mail senden** an den Lieferanten.

**Abschluss.** Nach Rücklauf setzt er die Bestätigung über **Gelangensbestätigung erhalten** auf **Empfangen**. Bleibt der Rücklauf aus, mahnt er über **Mahnung** nach.

## Berechtigungen

Die Erweiterung liefert einen eigenen Berechtigungssatz aus, der Lese‑ und Schreibrechte auf die Tabellen und Seiten der Gelangensbestätigung sowie Ausführungsrechte auf die Codeunits und Berichte bündelt. Der Administrator weist diesen Berechtigungssatz den Anwendern zu; er bestimmt die Berechtigungen für das Bearbeiten, Drucken, Versenden und Nachverfolgen von Gelangensbestätigungen.
