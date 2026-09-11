---
title: Anwenderhandbuch m+m Invoice Purchase Receipt
---

# Anwenderhandbuch m+m Invoice Purchase Receipt

## Einleitung

Die App **m+m Invoice Purchase Receipt** erweitert Microsoft Dynamics 365 Business Central um eine zeilengenaue Übersicht aller gebuchten Einkaufslieferungen, die noch **nicht fakturiert** sind. Über die Seite **Einkaufslieferung fakturieren** erzeugen und buchen Sie zu diesen Lieferzeilen die zugehörige Einkaufsrechnung – wahlweise inklusive einer Pflichtentnahme (Umlagerung) aus dem Konsi-Lager in ein reguläres Lager.

Das Modul richtet sich an **operative Einkaufs- und Kreditorenbuchhaltungs-Anwender**, die im Tagesgeschäft Einkaufsrechnungen zu bereits gelieferter Ware buchen. Administratoren und Lagerverantwortliche sind sekundäre Zielgruppe: Sie kennzeichnen die betroffenen Lagerorte als Konsi-Lager und stellen die Buchhaltungs- und Lagerbewegungs-Voraussetzungen bereit (Einrichtung, Stammdaten).

**Fachlicher Hintergrund.** Für **Konsi-Lager** (Konsignationslager) wird die Ware zunächst geliefert und eingelagert, aber erst später fakturiert – häufig erst bei tatsächlichem Verbrauch. Das Modul sammelt daher genau die Lieferzeilen dieser Lagerorte, deren Menge noch offen (nicht fakturiert) ist, und stellt sie in einer Arbeitsliste bereit. Chargengeführte Artikel werden dabei **je Chargennr.** getrennt geführt, damit die Rechnung mengen- und chargengenau gebucht werden kann.

**Kurzer Prozessüberblick.**

1. Ein Lagerort wird als **Konsi-Lager** eingerichtet (Einrichtung).
2. Beim Buchen einer Einkaufslieferung bzw. Einkaufsrechnung auf einen solchen Lagerort füllt das Modul automatisch die Liste **Einkaufslieferung fakturieren** mit den offenen Zeilen.
3. Der Anwender öffnet die Liste, prüft die offenen Mengen, setzt bei Bedarf die **Kred.-Rechnungsnr.** und trägt die **Menge zu fakturieren** ein.
4. Über **Fakturieren** oder **Pflichtentnahme** wird die Einkaufsrechnung erzeugt und – je nach Option – direkt gebucht; bei der Pflichtentnahme wird zusätzlich eine **Umlagerung** aus dem Konsi-Lager gebucht.

## Schnellstart für Anwender

Die folgende Reihenfolge entspricht der Abhängigkeit im Code: erst die Einrichtung, dann die automatisch gefüllte Liste, dann die fakturierende Aktion.

1. **Einrichtung (einmalig, Administrator):** Öffnen Sie über die Aktion die **Lagerortkarte** des betreffenden Lagerorts (Suchen → **Lagerorte** → Zeile wählen → **Bearbeiten**) und setzen Sie im Inforegister **Allgemein** das Kennzeichen **Konsi-Lager**. Nur für so gekennzeichnete Lagerorte werden Fakturierungszeilen erzeugt.
2. **Ware buchen (Standard-Einkaufsprozess):** Buchen Sie die Einkaufslieferung bzw. Einkaufsrechnung wie gewohnt. Für Lieferzeilen auf einem Konsi-Lager legt das Modul im Hintergrund automatisch die offenen Zeilen in **Einkaufslieferung fakturieren** an.
3. **Liste öffnen:** Geben Sie in **Suchen** den Begriff **Einkaufslieferung fakturieren** ein und öffnen Sie den gleichnamigen Aufgaben-Link.
4. **Kred.-Rechnungsnr. vergeben (optional):** Markieren Sie die betreffenden Zeilen und wählen Sie **Kred.-Rechnungsnr. setzen**, um die Kreditoren-Rechnungsnummer für die spätere Rechnung zu hinterlegen. Die Rechnung wird je Kombination aus **Kred.-Rechnungsnr.** und **Kreditorennr.** zusammengefasst.
5. **Menge festlegen:** Tragen Sie in der Spalte **Menge zu fakturieren** die zu fakturierende Menge ein (höchstens die **nicht fakturierte Menge** – eine höhere Eingabe wird mit einer Fehlermeldung abgewiesen).
6. **Fakturieren:** Markieren Sie die Zeilen und wählen Sie
   - **Fakturieren**, wenn nur die Einkaufsrechnung erstellt/gebucht werden soll, oder
   - **Pflichtentnahme**, wenn zusätzlich die Ware per **Umlagerung** vom Konsi-Lager auf ein reguläres Lager gebucht werden soll (mit Angabe von **Lagerortcode** und **Lagerplatzcode**).
7. **Optionen im Dialog setzen:** Bestätigen Sie im Dialog **Buchungsdatum**, die Ersetzungs-Optionen sowie **Rechnungen buchen**, und schließen Sie mit **OK**.

## Einrichtung

Die Einrichtung ist bewusst schlank: Das Modul benötigt keine eigene Einrichtungsseite. Die einzige zwingende Konfiguration ist die Kennzeichnung der Konsi-Lager auf der Lagerortkarte. Ergänzend nutzt der Prozess ein automatisch angelegtes Umlagerungs-Buch.-Blatt sowie – bei der Pflichtentnahme – Lagerplatzsteuerung des Ziel­lagers.

### Konsi-Lager am Lagerort einrichten

**Prozess-Intro.** Diese Einrichtung nimmt der Administrator bzw. der Lagerverantwortliche **vor der ersten Nutzung** je Lagerort vor. Sie entscheidet, ob das Modul für Buchungen auf diesem Lagerort überhaupt Fakturierungszeilen erzeugt. Der so eingerichtete Lagerort wird später im Tagesgeschäft in der Liste **Einkaufslieferung fakturieren** (Kapitel „Tägliche Arbeit") sichtbar.

**Einstieg:** **Lagerorte** (Master-Liste) → Zeile des Lagerorts → **Bearbeiten** → **Lagerortkarte**, Inforegister **Allgemein**.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Konsi-Lager** | Wenn aktiviert, gilt der Lagerort als Konsignationslager: Beim Buchen einer Einkaufslieferung bzw. Einkaufsrechnung auf diesen Lagerort erzeugt das Modul automatisch je offener Lieferzeile (bei chargengeführten Artikeln je **Chargennr.**) einen Eintrag in **Einkaufslieferung fakturieren**. Ist das Kennzeichen nicht gesetzt, bleibt der Lagerort im Standardverhalten von Business Central; es werden **keine** Fakturierungszeilen gebildet und die Ware wird wie üblich direkt fakturiert. |

**Prozessschritte (Aktivierung).**

1. **Zuerst** öffnen Sie die **Lagerortkarte** des Lagerorts und setzen im Inforegister **Allgemein** das Kennzeichen **Konsi-Lager**.
2. **Danach** buchen Sie den Einkauf wie gewohnt; ab diesem Zeitpunkt werden für Lieferzeilen dieses Lagerorts automatisch offene Fakturierungszeilen gebildet.
3. **Schließlich** verarbeiten Anwender diese Zeilen in der Liste **Einkaufslieferung fakturieren** (siehe Kapitel „Tägliche Arbeit").

**Abhängigkeitshinweis.** Die Fakturierungszeilen entstehen nur für Belegzeilen des Typs **Artikel** oder **Zuschlag (Artikel)**. Zeilen ohne Lagerortbezug oder auf einem nicht als Konsi-Lager gekennzeichneten Lagerort werden übersprungen.

### Umlagerungs-Buch.-Blatt für die Pflichtentnahme

**Prozess-Intro.** Diese Konfiguration ist **nur** relevant, wenn Sie im Tagesgeschäft die Aktion **Pflichtentnahme** nutzen (Kapitel „Tägliche Arbeit"). Sie muss in der Regel nicht manuell erstellt werden: Das Modul legt das benötigte Buch.-Blatt automatisch an, sofern es noch nicht existiert. Die Erläuterung dient dem Verständnis der im Hintergrund gebuchten **Umlagerung**.

**Einstieg:** Kein direkter Anwender-Einstieg erforderlich; das Buch.-Blatt wird programmatisch bereitgestellt. Zur Kontrolle erreichbar über **Suchen** → **Artikel-Umlagerungs-Buch.-Blätter** (Buch.-Blattname **PRITRANS**).

Bei der **Pflichtentnahme** erzeugt das Modul im Umlagerungs-Buch.-Blatt eine Zeile vom **Buchungsart**-Typ **Umlagerung**:

1. **Zuerst** ermittelt das Modul die Quelle (Lagerort/Lagerplatz) aus dem Lagerplatzinhalt der ursprünglichen Einkaufslieferzeile bzw. – wenn kein Lagerplatzinhalt passt – aus den Lagerplatzinhalten des Artikels mit ausreichender Menge.
2. **Danach** setzt es den Ziel-Lagerort und -Lagerplatz auf die im Fakturier-Dialog angegebenen Werte **Lagerortcode** und **Lagerplatzcode**.
3. **Schließlich** wird diese Umlagerung gebucht (bei chargengeführten Artikeln mit übernommener **Chargennr.**), bevor die Einkaufsrechnung erstellt und gebucht wird.

**Validierung.** Bei aktiver Pflichtentnahme wird geprüft, ob der Ziel-Lagerort lagerplatzpflichtig ist; ist das der Fall, muss der angegebene **Lagerplatzcode** im Ziel-Lagerort existieren. Fehlt bei aktiven Ersetzungs-Optionen ein **Buchungsdatum**, bricht die Verarbeitung mit dem Hinweis „Ein Buchungsdatum muss eingegeben werden." ab.

## Stammdaten

Das Modul führt keine eigenen Stammdatentabellen (Teams, Gruppen, Kostenarten o. Ä.). Die fachlich relevante Stammdaten-Erweiterung betrifft die **Kred.-Lieferungsnr.**, die dieses Modul zusätzlich auf Einkaufsbelegen führt und bis in die gebuchte Einkaufslieferung durchreicht.

### Kred.-Lieferungsnr. auf Einkaufsbelegen (Bestellung)

**Prozess-Intro.** Die **Kred.-Lieferungsnr.** dokumentiert die Lieferschein-/Lieferungsnummer des Kreditors zur Ware. Anwender pflegen sie im **Kopf** der **Einkaufsbestellung**; das Modul verteilt den Wert automatisch auf die Bestellzeilen und überträgt ihn beim Buchen bis in die gebuchte Einkaufslieferung. In der Liste **Einkaufslieferung fakturieren** dient die Kred.-Lieferungsnr. später als Nachweis, zu welcher Lieferung eine offene Menge gehört.

**Einstieg (Kopf):** **Einkaufsbestellungen** → Beleg öffnen → Inforegister **Lieferung und Zahlung** → Feld **Kred.-Lieferungsnr.**
**Einstieg (Zeile):** **Einkaufsbestellung**, Zeilenbereich (Unterseite) → Spalte **Kred.-Lieferungsnr.**

| Feld | Erläuterung |
|------|-------------|
| **Kred.-Lieferungsnr.** (Kopf) | Wenn im Bestellkopf gesetzt, wird der Wert beim Ändern automatisch auf alle Bestellzeilen übernommen, bei denen noch keine Kred.-Lieferungsnr. hinterlegt ist; so muss der Anwender die Nummer nur einmal erfassen. |
| **Kred.-Lieferungsnr.** (Zeile) | Wenn je Zeile gesetzt bzw. übernommen, wird der Wert beim Buchen in die gebuchte Einkaufslieferzeile geschrieben und steht dort sowie in der Liste **Einkaufslieferung fakturieren** als Referenz zur Verfügung; neu angelegte Bestellzeilen erhalten den Kopfwert automatisch vorbelegt. |

**Prozessschritte.**

1. **Zuerst** erfassen Sie die **Kred.-Lieferungsnr.** im Kopf der **Einkaufsbestellung**; bestehende Zeilen ohne eigenen Wert werden aktualisiert, neue Zeilen werden beim Anlegen vorbelegt.
2. **Danach** buchen Sie die Lieferung; der Wert wandert in die gebuchte Einkaufslieferzeile.
3. **Schließlich** ist die **Kred.-Lieferungsnr.** in der gebuchten Einkaufslieferung und in der Liste **Einkaufslieferung fakturieren** sichtbar (Querverweis: Kapitel „Tägliche Arbeit").

### Kred.-Lieferungsnr. in der gebuchten Einkaufslieferung

**Prozess-Intro.** Diese Erweiterung macht die **Kred.-Lieferungsnr.** auch nach dem Buchen sichtbar. Sie wird nicht gepflegt, sondern nur angezeigt; die Pflege erfolgt im Bestellkopf/-zeile (siehe vorherige H3). Der Wert unterstützt Anwender beim Abgleich zwischen gebuchter Lieferung und offener Fakturierung.

**Einstieg:** **Gebuchte Einkaufslieferungen** → Beleg öffnen → Zeilenbereich (Unterseite) → Spalte **Kred.-Lieferungsnr.**

| Feld | Erläuterung |
|------|-------------|
| **Kred.-Lieferungsnr.** | Zeigt in der gebuchten Einkaufslieferzeile die beim Buchen übernommene Kreditoren-Lieferungsnummer an; damit ist nachvollziehbar, aus welcher Kreditorenlieferung eine offene, noch zu fakturierende Menge stammt. |

## Tägliche Arbeit: Seite „Einkaufslieferung fakturieren"

Dies ist die zentrale Arbeitsseite des Moduls. Sie ist eine **Liste** und zeigt alle offenen, noch nicht fakturierten Zeilen der Konsi-Lager (nur Zeilen mit **Menge** größer als 0). Zeilen, zu denen bereits eine **ungebuchte** Einkaufsrechnung existiert, werden zur Warnung farblich hervorgehoben.

**Setzt voraus (Bezug zur Einrichtung):** Die Zeilen dieser Liste entstehen ausschließlich für Lagerorte mit gesetztem Kennzeichen **Konsi-Lager** (siehe Kapitel „Einrichtung → Konsi-Lager am Lagerort einrichten"). Die Fakturierung erzeugt eine **Einkaufsrechnung** über die Standard-Funktion „Zugang abrufen"; die Pflichtentnahme nutzt zusätzlich das Umlagerungs-Buch.-Blatt (siehe „Umlagerungs-Buch.-Blatt für die Pflichtentnahme").

**Einstieg:** **Suchen** → **Einkaufslieferung fakturieren** (Aufgaben-Link). Die Seite ist als Aufgabenseite über **Suchen** erreichbar.

### Spalten der Liste

Alle Spalten sind schreibgeschützt – mit einer Ausnahme: **Menge zu fakturieren**. Die meisten Werte werden aus der gebuchten Einkaufslieferzeile ermittelt.

| Feld | Erläuterung |
|------|-------------|
| **Belegnr.** | Nummer der gebuchten Einkaufslieferung, aus der die Zeile stammt; bei vorhandener ungebuchter Einkaufsrechnung wird der Wert zur Warnung farblich hervorgehoben. |
| **Buchungsdatum** | Buchungsdatum der zugrunde liegenden Einkaufslieferzeile; dient der zeitlichen Einordnung der offenen Menge. |
| **Kred.-Lieferungsnr.** | Aus der Einkaufslieferzeile übernommene Kreditoren-Lieferungsnummer; ordnet die offene Menge der konkreten Kreditorenlieferung zu. |
| **Kred.-Rechnungsnr.** | Kreditoren-Rechnungsnummer für die zu erzeugende Einkaufsrechnung; steuert die Zusammenfassung: Zeilen mit gleicher Kred.-Rechnungsnr. und gleichem Kreditor werden in **eine** Rechnung gebucht. Setzbar über die Aktion **Kred.-Rechnungsnr. setzen**. |
| **Kreditorennr.** | Kreditor der Lieferung; zusammen mit der Kred.-Rechnungsnr. Gruppierungskriterium für die Rechnungserstellung. |
| **Kreditorenname** | Name des Kreditors (aus dem gebuchten Einkaufslieferungskopf); erleichtert die Identifikation ohne Nummernkenntnis. |
| **Kreditorenadresse** | Adresse des Kreditors (aus dem gebuchten Einkaufslieferungskopf) als zusätzliche Kontrollinformation. |
| **Lagerortcode** | Lagerort der Lieferzeile (das Konsi-Lager); zeigt, aus welchem Bestand die offene Menge stammt. |
| **Lagerplatzcode** | Lagerplatz der Lieferzeile; relevant für die Quellermittlung bei der Pflichtentnahme. |
| **Art** | Zeilentyp der Einkaufslieferzeile (z. B. **Artikel** oder **Zuschlag (Artikel)**); nur diese Typen werden in die Liste aufgenommen. |
| **Nr.** | Artikel- bzw. Sachnummer der Zeile; identifiziert den zu fakturierenden Posten. |
| **Beschreibung** | Beschreibung der Einkaufslieferzeile; Klartext zum Posten. |
| **Beschreibung 2** | Zusatzbeschreibung der Einkaufslieferzeile, sofern gepflegt. |
| **Chargennr.** | Chargennummer bei chargengeführten Artikeln; die offene Menge wird je Charge getrennt geführt, damit charg­engenau fakturiert werden kann. |
| **Chargen-Beschreibung** | Beschreibung der Charge aus der Chargeninformation; unterstützt die Identifikation der richtigen Charge. |
| **Einheit** | Einheit der Lieferzeile; Bezugsgröße der Mengen. |
| **Menge** | Ursprünglich gelieferte Menge der Zeile (bzw. Chargenmenge); Basis für die offenen Mengen. Die Liste zeigt nur Zeilen mit Menge größer 0. |
| **Fakturierte Menge** | Bereits fakturierte Menge der Zeile/Charge; sie mindert die noch offene Menge. |
| **nicht fakturierte Menge** | Noch nicht fakturierte Menge (Menge abzüglich fakturierte Menge); Obergrenze für die Eingabe in **Menge zu fakturieren**. |
| **Verbrauchte Menge** | Bereits verbrauchte Menge der Charge (aus Artikelposten der Buchungsarten Verbrauch, Negative Regulierung und Verkauf); bereits verbrauchte Mengen werden bei der Vorbelegung der zu fakturierenden Menge abgezogen. |
| **Menge zu fakturieren** | **Einziges editierbares Feld.** Wenn Sie hier einen Wert eintragen, wird beim Fakturieren genau diese Menge in die Einkaufsrechnung übernommen. Der Wert darf die **nicht fakturierte Menge** nicht überschreiten; andernfalls erscheint „Menge zu fakturieren kann nicht größer sein als Menge nicht fakturiert." Vorbelegt wird er mit der nicht fakturierten Menge abzüglich der verbrauchten Menge. |

### Aktionen

| Aktion | Erläuterung |
|--------|-------------|
| **Fakturieren** | Wenn ausgeführt, wird zu den markierten Zeilen eine Einkaufsrechnung erstellt (und je nach Dialogoption gebucht). Bereits vorhandene, noch ungebuchte Einkaufsrechnungen zu einer Zeile lösen zuvor eine Rückfrage aus (siehe unten). Es findet **keine** Lagerumlagerung statt. |
| **Pflichtentnahme** | Wenn ausgeführt, wird zusätzlich zur Rechnung eine **Umlagerung** der Ware aus dem Konsi-Lager auf ein anzugebendes Ziel (**Lagerortcode**/**Lagerplatzcode**) gebucht; der Fakturier-Dialog blendet dafür die Ziel-Felder ein. Nutzen Sie diese Aktion, wenn die Ware mit der Fakturierung physisch vom Konsi-Lager ins Eigenlager überführt werden soll. |
| **Kred.-Rechnungsnr. setzen** | Wenn ausgeführt, öffnet sich ein Dialog, in dem Sie eine **Kred.-Rechnungsnr.** für die markierten Zeilen vergeben; dadurch werden Zeilen für die spätere Fakturierung gruppiert. Über die Option **Kred.-Rechnungsnr. ersetzen** legen Sie fest, ob bereits vorhandene Nummern überschrieben werden. |
| **Beleg anzeigen** | Wenn ausgeführt, wird zur markierten Zeile die zugehörige **Gebuchte Einkaufslieferung** geöffnet; so prüfen Sie den Ursprungsbeleg. |
| **Ungebuchte Einkaufsrechnungen anzeigen** | Wenn ausgeführt, werden die zu dieser Lieferzeile bereits erzeugten, noch **ungebuchten** Einkaufsrechnungszeilen angezeigt. Die Aktion ist nur aktiv, wenn zu der Zeile eine ungebuchte Einkaufsrechnung existiert. |

**Rückfrage bei vorhandener ungebuchter Rechnung.** Führen Sie **Fakturieren** oder **Pflichtentnahme** auf einer Zeile aus, zu der bereits eine ungebuchte Einkaufsrechnung besteht, erscheint die Abfrage „Es gibt ungebuchte Einkaufsrechnungen für diese Zeile.\Wollen Sie fortfahren?". Bestätigen Sie mit **Ja**, wird eine **zusätzliche** Rechnung erzeugt; mit **Nein** brechen Sie ab.

### Dialog „Einkaufslieferungen fakturieren" (Fakturier-Optionen)

Nach **Fakturieren** oder **Pflichtentnahme** öffnet sich der Optionen-Dialog. Er steuert Datum, Buchung und – bei der Pflichtentnahme – das Ziel der Umlagerung.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Buchungsdatum** | Wenn gesetzt, wird dieses Datum für die Buchung verwendet (Vorbelegung: Arbeitsdatum). Bei aktiven Ersetzungs-Optionen ist die Angabe zwingend – fehlt sie, bricht die Verarbeitung mit einem Hinweis ab. |
| **Buchungsdatum ersetzen** | Wenn aktiviert, wird das Buchungsdatum der erzeugten Einkaufsrechnung durch das oben erfasste **Buchungsdatum** ersetzt; ohne Aktivierung bleibt das Standard-Buchungsdatum erhalten. |
| **Belegdatum ersetzen** | Wenn aktiviert, wird das Belegdatum der Rechnung durch das oben erfasste **Buchungsdatum** ersetzt; nutzen Sie dies, wenn Beleg- und Buchungsdatum übereinstimmen sollen. |
| **Rechnungen buchen** | Wenn aktiviert, wird die zunächst nur erstellte Einkaufsrechnung sofort gebucht; ohne Aktivierung bleibt eine ungebuchte Rechnung zur weiteren Bearbeitung stehen. |
| **Lagerortcode** | Nur bei **Pflichtentnahme** sichtbar. Wenn gesetzt, ist dies der Ziel-Lagerort der Umlagerung, auf den die Ware aus dem Konsi-Lager gebucht wird. |
| **Lagerplatzcode** | Nur bei **Pflichtentnahme** sichtbar. Wenn gesetzt, ist dies der Ziel-Lagerplatz im Ziel-Lagerort; ist der Ziel-Lagerort lagerplatzpflichtig, muss der Lagerplatz dort existieren. Über die Auswahlfunktion wählen Sie ihn aus den Lagerplätzen des Ziel-Lagerorts. |

### Dialog „Kred.-Rechnungsnr. setzen"

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Kred.-Rechnungsnr.** | Wenn gesetzt, wird diese Kreditoren-Rechnungsnummer auf die markierten Zeilen geschrieben und dient als Gruppierungskriterium für die Rechnungserstellung. |
| **Kred.-Rechnungsnr. ersetzen** | Wenn aktiviert (Vorbelegung), werden auch bereits vorhandene Kred.-Rechnungsnrn. überschrieben; ohne Aktivierung werden nur leere Felder gefüllt. |

## Buchungsablauf (Fakturieren und Pflichtentnahme)

Der folgende Ablauf spiegelt die im Code hinterlegte Reihenfolge wider und ist identisch mit den Schnellstart-Schritten.

1. Zeile(n) in der Liste **Einkaufslieferung fakturieren** markieren.
2. **Menge zu fakturieren** je Zeile prüfen bzw. eintragen (höchstens **nicht fakturierte Menge**).
3. Aktion **Fakturieren** (nur Rechnung) oder **Pflichtentnahme** (Rechnung + **Umlagerung**) wählen.
4. Bei bereits vorhandener ungebuchter Rechnung: Rückfrage mit **Ja** bestätigen oder mit **Nein** abbrechen.
5. Im Dialog **Buchungsdatum** sowie Ersetzungs- und Buchungsoptionen setzen; bei **Pflichtentnahme** zusätzlich **Lagerortcode** und **Lagerplatzcode** angeben.
6. Bei **Pflichtentnahme** wird zuerst die **Umlagerung** im Umlagerungs-Buch.-Blatt gebucht.
7. Die Einkaufsrechnung wird über „Zugang abrufen" erzeugt; die Mengen (**Menge zu fakturieren**, bei Chargen je Charge über die Artikelverfolgung) werden auf die Rechnungszeilen übernommen.
8. Ist **Rechnungen buchen** aktiv, wird die Einkaufsrechnung anschließend gebucht; andernfalls bleibt sie ungebucht stehen.

**Teilmengen sind zulässig.** Sie müssen eine Zeile **nicht** vollständig ausfaktu­rieren: Tragen Sie in **Menge zu fakturieren** eine Teilmenge ein, wird nur diese fakturiert; die verbleibende Menge bleibt als offene Zeile in der Liste bestehen und kann später weiterverarbeitet werden.

## Report „Einkaufslieferungen fakturieren"

Die eigentliche Verarbeitung erfolgt über den Verarbeitungs-Report **Einkaufslieferungen fakturieren**, der von den Aktionen **Fakturieren** und **Pflichtentnahme** aufgerufen wird. Er besitzt keine eigene Menüposition (Aufruf ausschließlich über die Aktionen der Liste) und stellt die im Abschnitt „Dialog … (Fakturier-Optionen)" beschriebenen Anfrage-Optionen bereit. Der Report gruppiert die markierten Zeilen je Kreditor und Kred.-Rechnungsnr., erstellt je Gruppe eine Einkaufsrechnung und bucht sie bei aktiver Option **Rechnungen buchen**. Zeilen mit **Menge zu fakturieren** = 0 werden übersprungen.

## FAQ und Troubleshooting

### 1. Warum erscheinen keine Zeilen in „Einkaufslieferung fakturieren"?
Zeilen entstehen nur für Lagerorte mit gesetztem Kennzeichen **Konsi-Lager** und nur beim Buchen einer Einkaufslieferung/-rechnung auf einen solchen Lagerort. Prüfen Sie zuerst die **Lagerortkarte** des betroffenen Lagerorts.

### 2. Warum werden bestimmte Belegzeilen nicht übernommen?
Es werden ausschließlich Zeilen der Art **Artikel** und **Zuschlag (Artikel)** aufgenommen. Andere Zeilentypen (z. B. Sachkonto, Anlage) erzeugen keine Fakturierungszeile.

### 3. Warum ist eine Zeile farblich hervorgehoben?
Die Hervorhebung signalisiert, dass zu dieser Zeile bereits eine **ungebuchte** Einkaufsrechnung existiert. Über **Ungebuchte Einkaufsrechnungen anzeigen** sehen Sie die betroffene Rechnung.

### 4. Was passiert, wenn ich trotz vorhandener ungebuchter Rechnung faktu­riere?
Nach Bestätigung der Rückfrage „…Wollen Sie fortfahren?" mit **Ja** wird eine **zusätzliche** Rechnung erzeugt. Prüfen Sie vorher über **Ungebuchte Einkaufsrechnungen anzeigen**, ob dies gewollt ist.

### 5. Warum kann ich in „Menge zu fakturieren" keinen höheren Wert eingeben?
Die eingegebene Menge darf die **nicht fakturierte Menge** nicht überschreiten. Andernfalls erscheint „Menge zu fakturieren kann nicht größer sein als Menge nicht fakturiert." Reduzieren Sie den Wert entsprechend.

### 6. Wodurch wird die Vorbelegung von „Menge zu fakturieren" bestimmt?
Sie ergibt sich aus der **nicht fakturierten Menge** abzüglich der **verbrauchten Menge** der Charge. Bereits verbrauchte Bestände sollen so nicht erneut zur Fakturierung angeboten werden.

### 7. Was ist der Unterschied zwischen „Fakturieren" und „Pflichtentnahme"?
**Fakturieren** erstellt/bucht nur die Einkaufsrechnung. **Pflichtentnahme** bucht zusätzlich eine **Umlagerung** der Ware aus dem Konsi-Lager auf ein anzugebendes Ziel-Lager und -Lagerplatz.

### 8. Warum verlangt der Dialog ein Buchungsdatum?
Sobald **Buchungsdatum ersetzen** oder **Belegdatum ersetzen** aktiviert ist, muss ein **Buchungsdatum** angegeben werden. Fehlt es, bricht die Verarbeitung mit „Ein Buchungsdatum muss eingegeben werden." ab.

### 9. Wie werden mehrere markierte Zeilen zu Rechnungen zusammengefasst?
Die Verarbeitung gruppiert je Kombination aus **Kreditornr.** und **Kred.-Rechnungsnr.**; pro Gruppe entsteht eine Einkaufsrechnung. Über **Kred.-Rechnungsnr. setzen** steuern Sie diese Gruppierung.

### 10. Wo finde ich nach dem Buchen die Kred.-Lieferungsnr. wieder?
Sie wird beim Buchen in die **gebuchte Einkaufslieferzeile** übernommen und dort sowie in der Liste **Einkaufslieferung fakturieren** angezeigt. Gepflegt wird sie im Kopf bzw. in den Zeilen der **Einkaufsbestellung**.

## Typische Anwendungsfälle

### Anwendungsfall 1: Konsignationsware bei Verbrauch fakturieren

**Auslöser.** Die Lagerabteilung meldet, dass eine Charge Konsignationsware verbraucht wurde und nun abgerechnet werden kann.

**Einstieg in BC.** Der Sachbearbeiter öffnet über **Suchen** die Liste **Einkaufslieferung fakturieren**. Die betreffenden Zeilen sind bereits vorhanden, weil die Ware zuvor auf ein als **Konsi-Lager** gekennzeichnetes Lager geliefert wurde.

**Kernablauf.**
1. Der Sachbearbeiter filtert bzw. sucht die Zeilen des betreffenden Kreditors und der Charge (Spalte **Chargennr.**).
2. Über **Kred.-Rechnungsnr. setzen** vergibt er die Kreditoren-Rechnungsnummer für die zu gruppierenden Zeilen.
3. In **Menge zu fakturieren** trägt er – falls nicht bereits passend vorbelegt – die zu fakturierende Menge ein (höchstens **nicht fakturierte Menge**).
4. Er wählt **Fakturieren**, bestätigt im Dialog das **Buchungsdatum**, aktiviert bei Bedarf **Rechnungen buchen** und schließt mit **OK**.

**Abschluss.** Die Einkaufsrechnung ist erstellt (und bei aktiver Option gebucht). Die fakturierte Menge erhöht die **Fakturierte Menge**; verbleibende Restmengen bleiben als offene Zeilen bestehen.

### Anwendungsfall 2: Fakturieren mit gleichzeitiger Umlagerung aus dem Konsi-Lager

**Auslöser.** Der Einkauf erhält die Kreditorenrechnung und möchte die Ware zugleich vom Konsignationslager in den Eigenbestand überführen.

**Einstieg in BC.** Öffnen der Liste **Einkaufslieferung fakturieren** über **Suchen**.

**Kernablauf.**
1. Der Anwender markiert die relevanten Zeilen und prüft **Menge zu fakturieren**.
2. Er wählt **Pflichtentnahme**.
3. Im Dialog gibt er **Lagerortcode** und **Lagerplatzcode** des Ziel-Lagers an, setzt **Buchungsdatum** und Optionen und schließt mit **OK**.
4. Das Modul bucht zuerst die **Umlagerung** (im Umlagerungs-Buch.-Blatt, bei Chargen mit übernommener **Chargennr.**) und erstellt anschließend die Einkaufsrechnung.

**Abschluss.** Die Ware liegt nun im Ziel-Lager; die Einkaufsrechnung ist erzeugt und – bei aktiver Option **Rechnungen buchen** – gebucht.

### Anwendungsfall 3: Kreditoren-Lieferungsnummer von der Bestellung durchreichen

**Auslöser.** Der Kreditor nennt auf seinem Lieferschein eine Lieferungsnummer, die im Wareneingangsprozess dokumentiert werden soll.

**Einstieg in BC.** Der Einkäufer öffnet die **Einkaufsbestellung**.

**Kernablauf.**
1. Im Bestellkopf (Inforegister **Lieferung und Zahlung**) trägt er die **Kred.-Lieferungsnr.** ein; der Wert wird automatisch auf die Bestellzeilen ohne eigenen Wert übertragen.
2. Er bucht die Lieferung; der Wert wandert in die **gebuchte Einkaufslieferzeile**.

**Abschluss.** Die **Kred.-Lieferungsnr.** ist in der gebuchten Einkaufslieferung und – sobald die Zeile ein Konsi-Lager betrifft – in der Liste **Einkaufslieferung fakturieren** als Referenz sichtbar.
