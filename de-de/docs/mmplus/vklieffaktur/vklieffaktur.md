---
title: Anwenderhandbuch m+m Invoice Sales Shipment
---

# Anwenderhandbuch m+m Invoice Sales Shipment

Dieses Handbuch beschreibt die Erweiterung **m+m Invoice Sales Shipment** für Microsoft Dynamics 365 Business Central. Das Modul stellt die Seite **Verkaufslieferungen fakturieren** bereit: eine Übersicht aller gebuchten Verkaufslieferzeilen, die noch eine offene, nicht fakturierte Liefermenge enthalten. Aus dieser Übersicht heraus erzeugen, buchen, drucken und versenden Sie Verkaufsrechnungen — einzeln, je Beleg oder als Sammelrechnung je Debitor.

## Einleitung

### Zweck des Moduls

In Business Central bleibt eine Verkaufslieferung nach dem Warenausgang so lange offen fakturierbar, bis die gelieferte Menge vollständig in Rechnung gestellt wurde. Ohne zusätzliche Hilfsmittel muss der Anwender diese offenen Lieferungen einzeln über die Verkaufsrechnung und die Funktion zum Holen von Lieferzeilen zusammensuchen. Das Modul **Verkaufslieferungen fakturieren** bündelt genau diesen Vorgang: Es zeigt sämtliche Verkaufslieferzeilen mit einer offenen Menge in einer Liste und fakturiert die markierten Zeilen mit einem Klick.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender in Verkauf und Fakturierung**, die täglich gebuchte Lieferungen in Rechnungen überführen und diese Rechnungen buchen, drucken oder per E‑Mail versenden. Sekundär richtet sich das Handbuch an **Administratoren und Key‑User**, die die Berechtigungen vergeben und die automatische Sammelfakturierung über die Aufgabenwarteschlange einrichten.

### Kurzer Prozessüberblick

1. Der Warenausgang zu einem Verkaufsauftrag wird wie gewohnt gebucht; dadurch entsteht eine gebuchte Verkaufslieferung mit offener, noch nicht fakturierter Menge.
2. Der Anwender öffnet die Seite **Verkaufslieferungen fakturieren**. Sie listet alle Lieferzeilen mit einer offenen Menge (**Lief. nicht fakt. Menge** ungleich 0).
3. Der Anwender markiert eine oder mehrere Zeilen und startet die Aktion **Fakturieren**. Im Dialog **Optionen** legt er Buchungsdatum, Buchung, Druck und Versand fest.
4. Das Modul erzeugt je Beleg eine Verkaufsrechnung, bucht sie auf Wunsch und druckt bzw. versendet den gebuchten Beleg.
5. Alternativ läuft derselbe Vorgang vollautomatisch als Sammelfakturierung über die Aufgabenwarteschlange.

## Schnellstart für Anwender

Der schnellste Weg von einer offenen Lieferung zur gebuchten Rechnung:

1. Öffnen Sie über **Suchen** die Seite **Verkaufslieferungen fakturieren**. (Die Seite ist als Aufgabenseite hinterlegt und daher direkt über die Suche erreichbar.)
2. Die Liste zeigt alle Verkaufslieferzeilen mit offener Menge. Zeilen, zu denen bereits eine ungebuchte Verkaufsrechnung existiert, werden in Signalfarbe hervorgehoben.
3. Markieren Sie die zu fakturierende(n) Zeile(n).
4. Wählen Sie die Aktion **Fakturieren**.
5. Bestätigen Sie – falls zu einer markierten Zeile bereits eine ungebuchte Rechnung besteht – die Rückfrage *„Es gibt ungebuchte Rechnungszeilen für diese Zeile. Wollen Sie fortfahren?“* mit **Ja**, wenn Sie zusätzlich eine weitere Rechnung erzeugen möchten.
6. Erfassen Sie im Dialog **Optionen** das **Buchungsdatum** und aktivieren Sie **Rechnung buchen**, wenn die erzeugte Rechnung sofort gebucht werden soll. Aktivieren Sie **Geb. Belege drucken** oder **Geb. Belege senden**, wenn der gebuchte Beleg zusätzlich gedruckt bzw. versendet werden soll.
7. Bestätigen Sie den Dialog. Das Modul erzeugt je Liefer­beleg eine Rechnung und führt Buchung, Druck bzw. Versand gemäß Ihren Optionen aus.

Für die wiederkehrende Massenfakturierung richten Sie stattdessen die **automatische Sammelfakturierung** ein (siehe Abschnitt *Einrichtung*); sie durchläuft die Schritte 3 bis 7 ohne Benutzerdialog.

## Einrichtung

Das Modul benötigt **keine eigene Einrichtungsseite** und keine Stammdaten. Für den produktiven Einsatz sind lediglich die Installation der Erweiterung, die Berechtigungsvergabe und – optional – die Einrichtung der automatischen Sammelfakturierung erforderlich.

### Erweiterung und Berechtigungen

Voraussetzung ist, dass die Erweiterung **m+m Invoice Sales Shipment** in der Erweiterungsverwaltung installiert und aktiviert ist. Eine weitergehende Konfiguration im Webclient ist nicht notwendig.

Für den Zugriff liefert das Modul einen Berechtigungssatz mit. Er legt fest, welche Aktionen die Anwender im Modul ausführen dürfen, und umfasst die Ausführungsrechte für die Fakturierungsseite, die beiden Fakturierungsberichte sowie die Codeunits für Ereignisbehandlung und Sammelfakturierung.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Berechtigungssatz zuweisen | Wenn Sie den mitgelieferten Berechtigungssatz einem Benutzer bzw. einer Benutzergruppe zuweisen, dann erhält dieser die Ausführungsrechte für die Seite **Verkaufslieferungen fakturieren**, die Berichte zum einzelnen und stapelweisen Fakturieren sowie die zugehörigen Verarbeitungs‑Codeunits. Ohne diese Zuweisung ist die Seite für den Anwender nicht bedienbar. |

### Automatische Sammelfakturierung einrichten

Wer den Standardfall Tag für Tag ausführt, sollte die Fakturierung nicht manuell anstoßen, sondern über die **Aufgabenwarteschlange** automatisieren. Das Modul stellt hierfür eine Codeunit bereit, die den stapelweisen Fakturierungslauf ohne Benutzerdialog durchführt.

**Wer richtet ein:** Administrator oder Key‑User. **Wann:** einmalig vor dem ersten automatisierten Lauf, danach über die Wiederholung des Aufgabenwarteschlangenpostens gesteuert. **Wohin fließt die Einstellung:** in den täglichen Fakturierungslauf, der ansonsten manuell über die Aktion **Fakturieren** ausgelöst würde (siehe *Tägliche Arbeit*).

Gehen Sie in Abhängigkeitsreihenfolge vor:

1. **Zuerst** stellen Sie sicher, dass die Erweiterung installiert und der Berechtigungssatz dem ausführenden Benutzer zugewiesen ist. Wenn diese Voraussetzung fehlt, dann bricht der automatische Lauf mit einem Berechtigungsfehler ab.
2. **Danach** legen Sie einen Aufgabenwarteschlangenposten an, der die mitgelieferte Sammelfakturierungs‑Codeunit (Objekt‑Nr. 5399952) ausführt. Wenn dieser Posten aktiviert und eingeplant ist, dann verarbeitet er bei jedem Lauf alle Verkaufslieferzeilen mit offener Menge automatisch.
3. **Schließlich** ist keine weitere Aktion im Tagesablauf nötig: Der Lauf bucht die erzeugten Rechnungen und druckt die gebuchten Belege eigenständig. Fehlerhafte Belege werden nicht gebucht, sondern mit einem Fehlertext gekennzeichnet (siehe *Historie und Fehlernachverfolgung*).

Der automatische Lauf verwendet feste Vorgaben: Er filtert die Verkaufslieferzeilen auf offene Menge, verwendet das **Arbeitsdatum** als Buchungsdatum, bucht die Rechnungen (**Rechnung buchen** aktiv) und druckt die gebuchten Belege (**Geb. Belege drucken** aktiv). Ob eine erzeugte Rechnung als Einzel- oder als Sammelrechnung entsteht, steuert das Kennzeichen **Sammelrechnung** je Lieferzeile (siehe *Sammelrechnung je Debitor*).

## Tägliche Arbeit: Verkaufslieferungen fakturieren

Die Seite **Verkaufslieferungen fakturieren** ist der zentrale Arbeitsplatz des Moduls. Sie ist schreibgeschützt und zeigt ausschließlich Verkaufslieferzeilen, deren gelieferte Menge noch nicht vollständig fakturiert ist (interner Listenfilter: **Lief. nicht fakt. Menge** ungleich 0). Die Sortierung erfolgt nach **Belegnr.** und Zeilennummer.

### Einstieg

Öffnen Sie die Seite über **Suchen** mit dem Begriff *Verkaufslieferungen fakturieren*. Die Seite ist als Aufgabenseite eingerichtet und dadurch unmittelbar über die Suche erreichbar; ein übergeordneter Beleg oder eine Stammdatenkarte muss nicht geöffnet werden.

### Spalten der Übersicht

Die folgende Tabelle beschreibt die in der Übersicht sichtbaren und die zusätzlich einblendbaren Spalten. Alle Spalten stammen aus der Verkaufslieferzeile und sind nicht editierbar.

| Feld | Erläuterung |
|------|-------------|
| Belegnr. | Nummer der gebuchten Verkaufslieferung, aus der die Zeile stammt. Dient als führendes Gruppierungsmerkmal: Zeilen mit derselben **Belegnr.** werden zu einer Rechnung je Beleg zusammengefasst. Die Spalte ist zur besseren Lesbarkeit hervorgehoben. |
| Rech. an Deb.-Nr. | Rechnungsempfänger der Lieferzeile. Wenn dieser vom Verkaufsdebitor abweicht, dann wird die Rechnung an diesen abweichenden Rechnungsdebitor gestellt; bei der Sammelrechnung werden Zeilen nach diesem Debitor gebündelt. Zeilen mit bereits vorhandener ungebuchter Rechnung werden in dieser Spalte farblich hervorgehoben. |
| Verk. an Deb.-Nr. | Verkaufsdebitor der Lieferzeile. Standardmäßig ausgeblendet; einblendbar, wenn Sie zwischen Verkaufs- und Rechnungsdebitor unterscheiden müssen. |
| Art | Zeilenart der Verkaufslieferzeile (z. B. Artikel, Sachkonto). Bestimmt, welche Ergebniszeile beim Fakturieren erzeugt wird. |
| Nr. | Nummer des Artikels bzw. Kontos der Zeile. |
| Variantencode | Variante des Artikels; standardmäßig ausgeblendet, relevant bei variantengeführten Artikeln. |
| Beschreibung | Bezeichnung der Zeile, wie sie in die Rechnung übernommen wird. |
| Beschreibung 2 | Ergänzende Bezeichnung der Zeile. |
| Währungscode | Währung der Lieferzeile; standardmäßig ausgeblendet. Wenn gesetzt, dann wird die erzeugte Rechnung in dieser Währung angelegt. |
| Shortcutdimensionscode 1 | Wert der ersten Shortcut-Dimension; standardmäßig ausgeblendet. Wird beim Fakturieren in die Rechnung übernommen. |
| Shortcutdimensionscode 2 | Wert der zweiten Shortcut-Dimension; standardmäßig ausgeblendet. Wird beim Fakturieren in die Rechnung übernommen. |
| Lagerortcode | Lagerort der Lieferung; standardmäßig ausgeblendet. |
| Einheitencode | Verkaufseinheit der Zeile. |
| Menge | Gelieferte Menge der Zeile. |
| Einheit | Basiseinheit der Zeile; standardmäßig ausgeblendet. |
| Ausgleich mit Artikelposten | Verweis auf den auszugleichenden Artikelposten; standardmäßig ausgeblendet, relevant für die Artikelverfolgung. |
| Projektnr. | Projektbezug der Lieferzeile; standardmäßig ausgeblendet. |
| Warenausg.-Datum | Datum des Warenausgangs der Zeile; standardmäßig ausgeblendet. |
| Fakturierte Menge | Bereits in Rechnung gestellte Menge der Zeile. Zeigt, wie viel der gelieferten Menge schon fakturiert wurde. |
| Lief. nicht fakt. Menge | Noch offene, nicht fakturierte Liefermenge. Nur Zeilen mit einem Wert ungleich 0 erscheinen in der Liste; dieser Wert wird beim Fakturieren in Rechnung gestellt. |

Zeilen, zu denen bereits eine **ungebuchte** Verkaufsrechnung existiert, werden farblich als Hinweis dargestellt. So erkennt der Anwender vor dem Fakturieren, dass für diese Lieferzeile schon eine offene Rechnung angelegt wurde, und vermeidet Doppelfakturierungen.

### Aktionen der Übersicht

Alle nachstehenden Aktionen sind zusätzlich in der Menüleiste als hervorgehobene Aktionen verfügbar.

| Aktion | Erläuterung |
|--------|-------------|
| Fakturieren | Fakturiert die markierten Lieferzeilen. Wenn Sie die Aktion auslösen, dann öffnet sich der Dialog **Optionen**; anschließend erzeugt das Modul je Belegnr. eine Verkaufsrechnung und bucht, druckt bzw. versendet sie gemäß den gewählten Optionen. |
| Beleg anzeigen | Öffnet zur markierten Zeile die zugehörige **Geb. Verkaufslieferung**, damit Sie den Ursprungsbeleg prüfen können. |
| Ungebuchte Verkaufsrechnungen anzeigen | Öffnet zur markierten Zeile die **Verkaufszeilen** der bereits vorhandenen ungebuchten Rechnung. Wenn keine passende ungebuchte Rechnungszeile existiert, dann ist die Aktion deaktiviert. |
| Dimensionen | Öffnet die Dimensionen der markierten Zeile zur Ansicht der Dimensionswerte. |
| Artikelverfolgungsposten | Öffnet die **Artikelverfolgungszeilen** der markierten Zeile (Serien-/Chargeninformationen der Lieferung). |

### Der Dialog „Optionen" beim Fakturieren

Nachdem Sie eine oder mehrere Zeilen markiert und **Fakturieren** gewählt haben, erscheint zunächst – sofern zu einer markierten Zeile bereits eine ungebuchte Rechnung besteht – die Rückfrage *„Es gibt ungebuchte Rechnungszeilen für diese Zeile. Wollen Sie fortfahren?“*. Bestätigen Sie mit **Ja**, wird zusätzlich zur bestehenden eine weitere Verkaufsrechnung erzeugt.

Anschließend öffnet sich der Dialog **Optionen** mit folgenden Feldern:

| Einrichtung | Erläuterung |
|-------------|-------------|
| Buchungsdatum | Datum, das für die Buchung der erzeugten Rechnung verwendet wird. Wenn eines der Ersetzen-Kennzeichen aktiv ist und hier kein Datum eingetragen wurde, dann bricht die Verarbeitung mit der Meldung *„Ein Buchungsdatum muss eingegeben werden.“* ab. Vorbelegt ist das Arbeitsdatum. |
| Buchungsdatum ersetzen | Wenn aktiviert, dann wird das Buchungsdatum der erzeugten Rechnung durch das oben erfasste **Buchungsdatum** ersetzt; andernfalls bleibt das aus dem Standardablauf ermittelte Buchungsdatum bestehen. |
| Belegdatum ersetzen | Wenn aktiviert, dann wird das Belegdatum der erzeugten Rechnung durch das oben erfasste **Buchungsdatum** ersetzt; andernfalls bleibt das ermittelte Belegdatum bestehen. |
| Rechnungsrabatt kalkulieren | Wenn aktiviert, dann durchläuft das Modul vor dem Buchen die Rechnungsrabattberechnung, sodass ein zeilenübergreifender Rabatt ermittelt wird. Voraussetzung: In der Einrichtung Verkauf & Forderungen darf die automatische Rechnungsrabattberechnung nicht aktiv sein; andernfalls verhindert eine Prüfung die Verwendung dieser Option. |
| Rechnung buchen | Zunächst wird stets eine ungebuchte Rechnung erzeugt. Wenn diese Option aktiviert ist, dann wird die Rechnung im selben Lauf gebucht; andernfalls verbleibt sie als ungebuchte Verkaufsrechnung zur späteren Prüfung. |
| Geb. Belege drucken | Wenn aktiviert, dann wird nach erfolgreicher Buchung der gebuchte Rechnungsbeleg über die eingerichtete Berichtsauswahl gedruckt. Das Aktivieren schaltet **Rechnung buchen** zwingend mit ein und **Geb. Belege senden** aus, da nur ein gebuchter Beleg gedruckt werden kann. |
| Geb. Belege senden | Wenn aktiviert, dann wird der gebuchte Beleg gemäß dem Beleg-Sendeprofil des Debitors versendet (z. B. per E‑Mail). Das Aktivieren schaltet **Rechnung buchen** zwingend mit ein und **Geb. Belege drucken** aus. |

Zusammenspiel der Optionen: Deaktivieren Sie **Rechnung buchen**, so werden auch **Geb. Belege drucken** und **Geb. Belege senden** automatisch deaktiviert, weil ohne Buchung kein gebuchter Beleg entsteht. **Geb. Belege drucken** und **Geb. Belege senden** schließen sich gegenseitig aus.

### Was beim Fakturieren im Hintergrund geschieht

Damit Sie das Ergebnis richtig einordnen, hier der von Business Central ausgeführte Ablauf: Das Modul gruppiert die markierten Lieferzeilen nach **Belegnr.** und legt je Beleg eine Verkaufsrechnung an. In den Rechnungskopf übernimmt es Verkaufs- bzw. Rechnungsdebitor, gegebenenfalls das ersetzte Buchungs- und Belegdatum, den **Lieferung-an-Code**, den **Währungscode**, die Shortcut-Dimensionen sowie – aus dem zugehörigen Verkaufsauftrag – Zahlungsbedingung und Lieferbedingung. Anschließend werden die Lieferzeilen über die Standardfunktion zum Holen von Lieferzeilen als Rechnungszeilen eingelesen. Ist **Rechnungsrabatt kalkulieren** aktiv, folgt die Rabattberechnung; ist **Rechnung buchen** aktiv, wird die Rechnung gebucht und – je nach Option – gedruckt oder versendet.

## Sammelrechnung je Debitor

Über das Kennzeichen **Sammelrechnung** je Verkaufslieferzeile steuert das Modul, ob Lieferungen eines Debitors zu **einer** Rechnung zusammengefasst werden.

| Feld | Erläuterung |
|------|-------------|
| Sammelrechnung | Kennzeichen der Verkaufslieferzeile. Wenn gesetzt, dann werden im stapelweisen Lauf alle betroffenen Lieferzeilen desselben Rechnungsdebitors zu einer gemeinsamen Verkaufsrechnung zusammengeführt; ist es nicht gesetzt, dann entsteht je Lieferbeleg eine eigene Rechnung. |

Das Kennzeichen wird **nicht** manuell auf der Fakturierungsseite gepflegt, sondern automatisch beim Buchen der Verkaufslieferung gesetzt: Das Modul übernimmt dabei den Wert des Standardfelds **Sammelrechnung** aus dem Verkaufsbeleg auf die entstehende Lieferzeile. Wenn ein Verkaufsauftrag mit aktiver Sammelrechnung geliefert wird, dann trägt die zugehörige Lieferzeile das Kennzeichen und wird im automatischen Lauf mit den übrigen Sammelrechnungszeilen desselben Debitors gebündelt.

Der stapelweise Bericht **VK-Lieferungen stapelweise fakturieren** wertet dieses Kennzeichen aus: Zeilen mit Sammelrechnung werden je Rechnungsdebitor gesammelt und in einer Rechnung zusammengeführt; alle übrigen Zeilen werden je Lieferbeleg einzeln fakturiert. Vor dem Anlegen prüft der Lauf über die Standardsperrprüfung, ob der Debitor für Verkaufsrechnungen gesperrt ist.

## Historie und Fehlernachverfolgung

Das Modul führt keine eigene Historienliste. Für die Nachverfolgung fehlgeschlagener Läufe erweitert es jedoch die Standardliste der Verkaufsrechnungen um eine Fehlerspalte.

### Fehlertext auf der Verkaufsrechnungsliste

Beim automatischen bzw. stapelweisen Fakturieren kann das Erzeugen oder Buchen einer einzelnen Rechnung fehlschlagen (z. B. gesperrter Debitor, fehlende Angaben). Damit ein Fehler den gesamten Lauf nicht abbricht, fängt das Modul ihn je Beleg ab, verwirft leere Rechnungsköpfe und vermerkt die Ursache.

| Feld | Erläuterung |
|------|-------------|
| Fehlertext | Wird im stapelweisen Lauf auf dem Verkaufsrechnungskopf gefüllt, wenn das Erzeugen oder Buchen dieser Rechnung fehlgeschlagen ist. Wenn ein Wert vorhanden ist, dann enthält das Feld die zuletzt aufgetretene Fehlermeldung und weist den Sachbearbeiter auf die zu prüfende Rechnung hin; bei erfolgreicher Verarbeitung bleibt das Feld leer. |

Die Spalte **Fehlertext** wird am Ende der Liste **Verkaufsrechnungen** eingeblendet. Über sie erkennt der Anwender nach einem automatischen Lauf auf einen Blick, welche Rechnungen nicht gebucht werden konnten und aus welchem Grund, und kann sie gezielt nacharbeiten.

## FAQ und Troubleshooting

### 1. Warum erscheint eine Verkaufslieferzeile nicht in der Übersicht?

Die Seite **Verkaufslieferungen fakturieren** zeigt ausschließlich Zeilen mit einer offenen Menge (**Lief. nicht fakt. Menge** ungleich 0). Wenn die gelieferte Menge bereits vollständig fakturiert wurde, dann verschwindet die Zeile aus der Liste.

### 2. Warum ist eine Zeile farblich hervorgehoben?

Die farbliche Hervorhebung kennzeichnet Lieferzeilen, zu denen bereits eine **ungebuchte** Verkaufsrechnung existiert. Das ist ein Hinweis, um versehentliche Doppelfakturierungen zu vermeiden.

### 3. Was passiert, wenn ich eine hervorgehobene Zeile trotzdem fakturiere?

Beim Auslösen von **Fakturieren** erscheint die Rückfrage *„Es gibt ungebuchte Rechnungszeilen für diese Zeile. Wollen Sie fortfahren?“*. Bestätigen Sie mit **Ja**, wird zusätzlich zur bestehenden eine weitere Verkaufsrechnung erzeugt.

### 4. Warum verlangt der Dialog ein Buchungsdatum?

Wenn Sie **Buchungsdatum ersetzen** oder **Belegdatum ersetzen** aktivieren, aber kein Datum eintragen, dann bricht die Verarbeitung mit der Meldung *„Ein Buchungsdatum muss eingegeben werden.“* ab. Tragen Sie in diesem Fall ein gültiges **Buchungsdatum** ein.

### 5. Warum lässt sich „Rechnungsrabatt kalkulieren" nicht verwenden?

Die Option prüft, dass in der Einrichtung Verkauf & Forderungen die automatische Rechnungsrabattberechnung deaktiviert ist. Wenn diese Einstellung aktiv ist, dann verhindert die Prüfung die Verwendung der Option, um eine doppelte Rabattberechnung auszuschließen.

### 6. Warum wird die Rechnung nicht gebucht, obwohl ich sie fakturiert habe?

Das Modul erzeugt zunächst immer eine **ungebuchte** Rechnung. Nur wenn Sie im Dialog **Rechnung buchen** aktivieren, wird sie im selben Lauf gebucht. Ohne dieses Kennzeichen bleibt die Rechnung als ungebuchte Verkaufsrechnung bestehen.

### 7. Warum sind „Geb. Belege drucken" und „Geb. Belege senden" ausgegraut?

Beide Optionen setzen eine Buchung voraus. Solange **Rechnung buchen** nicht aktiv ist, stehen sie nicht zur Verfügung; das Aktivieren einer der beiden Optionen schaltet **Rechnung buchen** automatisch mit ein. Zudem schließen sich Drucken und Senden gegenseitig aus.

### 8. Warum entstehen mehrere Rechnungen statt einer Sammelrechnung?

Eine Sammelrechnung je Debitor entsteht nur für Lieferzeilen mit gesetztem Kennzeichen **Sammelrechnung**. Dieses Kennzeichen wird beim Buchen der Lieferung aus dem Feld **Sammelrechnung** des Verkaufsbelegs übernommen. Fehlt es, dann wird je Lieferbeleg eine eigene Rechnung erzeugt.

### 9. Wo sehe ich, warum ein automatischer Lauf eine Rechnung nicht buchen konnte?

Der stapelweise Lauf schreibt die Fehlerursache je Beleg in das Feld **Fehlertext**. Blenden Sie die Spalte **Fehlertext** in der Liste **Verkaufsrechnungen** ein, um die betroffenen Rechnungen und die jeweilige Meldung zu sehen.

### 10. Warum wird eine Rechnung im automatischen Lauf übersprungen?

Vor dem Anlegen prüft der Lauf, ob der Debitor für Verkaufsrechnungen gesperrt ist, und ob zur Lieferzeile bereits eine Rechnungszeile existiert. Wenn der Debitor gesperrt ist oder bereits eine Rechnungszeile vorliegt, dann wird die betroffene Zeile nicht erneut fakturiert; bei einem echten Fehler wird der leere Rechnungskopf verworfen und der **Fehlertext** gefüllt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Einzelne Lieferung nach Kundenanfrage fakturieren

**Auslöser:** Ein Kunde ruft an und bittet um die Rechnung zu einer bereits erhaltenen Lieferung.

**Einstieg in BC:** Der Sachbearbeiter öffnet über **Suchen** die Seite **Verkaufslieferungen fakturieren**.

**Kernablauf:**
1. Er sucht die Zeile(n) des Kunden anhand von **Rech. an Deb.-Nr.** und **Belegnr.** und markiert sie.
2. Über **Beleg anzeigen** prüft er bei Bedarf die zugehörige **Geb. Verkaufslieferung**.
3. Er wählt **Fakturieren**.
4. Im Dialog **Optionen** trägt er das **Buchungsdatum** ein, aktiviert **Rechnung buchen** und **Geb. Belege senden** und bestätigt.

**Abschluss:** Die Rechnung wird gebucht und gemäß dem Beleg-Sendeprofil des Debitors versendet. Die fakturierte Zeile verschwindet aus der Übersicht, sobald ihre offene Menge vollständig abgerechnet ist.

### Anwendungsfall 2: Tägliche Sammelfakturierung über die Aufgabenwarteschlange

**Auslöser:** Am Tagesende sollen alle offenen Lieferungen automatisch abgerechnet werden, Kunden mit aktiver Sammelrechnung erhalten je eine gebündelte Rechnung.

**Einstieg in BC:** Kein manueller Einstieg — der eingerichtete Aufgabenwarteschlangenposten startet die Sammelfakturierungs‑Codeunit (siehe *Automatische Sammelfakturierung einrichten*).

**Kernablauf:**
1. Der Lauf filtert alle Verkaufslieferzeilen mit offener Menge.
2. Zeilen mit Kennzeichen **Sammelrechnung** werden je **Rech. an Deb.-Nr.** zu einer Rechnung zusammengeführt; übrige Zeilen werden je **Belegnr.** einzeln fakturiert.
3. Für jeden Beleg prüft der Lauf die Debitorsperre und erzeugt die Rechnung; anschließend wird sie gebucht (**Rechnung buchen**) und gedruckt (**Geb. Belege drucken**).

**Abschluss:** Alle erfolgreichen Rechnungen sind gebucht und gedruckt. Fehlgeschlagene Belege sind über den **Fehlertext** in der Liste **Verkaufsrechnungen** nachvollziehbar.

### Anwendungsfall 3: Fehlgeschlagene Rechnung aus einem automatischen Lauf nacharbeiten

**Auslöser:** Nach dem automatischen Lauf meldet die Buchhaltung, dass für einen Kunden keine Rechnung angekommen ist.

**Einstieg in BC:** Der Key‑User öffnet die Liste **Verkaufsrechnungen** und blendet die Spalte **Fehlertext** ein.

**Kernablauf:**
1. Er filtert auf gefüllte **Fehlertext**-Einträge und liest die Fehlerursache (z. B. gesperrter Debitor).
2. Er behebt die Ursache im jeweiligen Stammsatz.
3. Er öffnet erneut **Verkaufslieferungen fakturieren**; da die betroffene Lieferzeile weiterhin eine offene Menge trägt, erscheint sie wieder in der Liste.
4. Er markiert die Zeile, wählt **Fakturieren**, aktiviert **Rechnung buchen** und bestätigt.

**Abschluss:** Die zuvor fehlgeschlagene Rechnung ist nun gebucht; die offene Menge der Lieferzeile ist abgerechnet.
