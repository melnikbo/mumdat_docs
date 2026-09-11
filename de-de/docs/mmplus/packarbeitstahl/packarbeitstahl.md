---
title: Anwenderhandbuch FA-Arbeitsvorrat Stahl
---

# Anwenderhandbuch FA-Arbeitsvorrat Stahl

Dieses Handbuch beschreibt die Erweiterung **m+m Production Order Job Overview Steel with Package Mgt.** Die App verbindet den **FA-Arbeitsvorrat** der Stahlfertigung mit der **Packmittelverwaltung**: Beim Beenden bzw. Teilbeenden eines Fertigungsauftrags weisen die Anwender den zurückgemeldeten **Chargen** die passenden **Packmittel** zu, bauen die Packmittelstruktur (Packmittel, Innenverpackungen, Artikel) auf und buchen die zurückgemeldete Menge samt Packmitteln in einem Zug. Alle Bezeichnungen in diesem Handbuch entsprechen den in Business Central angezeigten deutschen Beschriftungen.

## Einleitung

### Zweck des Moduls

Die Erweiterung integriert die Packmittelzuordnung in die **erweiterte Rückmeldung** des FA-Arbeitsvorrats der Stahlbranche. Sie stellt sicher, dass jede zurückgemeldete Charge eines Fertigungsauftrags einem Packmittel zugeordnet wird, bevor der Arbeitsgang gebucht wird, und dass die entstandene Packmittelstruktur beim Buchen der letzten Rückmeldung als **physisches Packmittel** in den Lager- und Artikelposten fortgeschrieben wird. Zusätzlich rechnet das Modul die Mengen durchgängig in **KG**, **Meter** und **Stück** um (Bewegungsmengen), wie es in der Stahlverarbeitung üblich ist.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender**, die täglich am FA-Arbeitsvorrat zurückmelden und buchen: Werker und Rückmeldepersonal an den Arbeitsplätzen sowie Lagerpersonal, das Chargen verpackt und die Packmittelstruktur pflegt. Sekundäre Zielgruppe sind **Administratoren und Key-User**, die die Arbeitsplatz-Einrichtung und die Packmittel-Stammdaten vorbereiten (Kapitel *Einrichtung*).

### Kurzer Prozessüberblick

1. Der Administrator aktiviert je Arbeitsplatz die erweiterte Ausgabe-Rückmeldung und hinterlegt über die **Rückmeldepage-Nr.** die packmittelbasierte Rückmeldeseite.
2. Der Anwender öffnet den **FA-Arbeitsvorrat**, filtert nach **Arbeitsplatznr.** (und ggf. **Maschinenplatznr.**) und wählt eine gestartete Zeile.
3. Über **Teilbeenden** bzw. **Beenden** startet die erweiterte Rückmeldung. Ist die packmittelbasierte Rückmeldeseite eingerichtet, öffnet sich **Erw. Packmittel Rückmeldung**.
4. Der Anwender ordnet die **Verfügbaren Chargen** den Packmitteln zu (**Chargen zuweisen** / **Alle Chargen zuweisen**), baut bei Bedarf die Packmittelstruktur auf und bestätigt mit **OK**.
5. Beim Buchen der letzten Rückmeldung werden die Packmittel zu physischen Packmitteln, es entstehen Artikel- und Lagerposten; optional werden die Packmittel automatisch dem reservierten Verkaufsauftrag zugewiesen.

---

## Schnellstart für Anwender

Die folgende Reihenfolge entspricht der Abhängigkeit im Code: zuerst Einrichtung, dann die Liste, dann die transaktionalen Aktionen.

1. **Einrichtung prüfen (einmalig, Administrator):** Öffnen Sie in der **Arbeitsplatzkarte** die Aktion für die Arbeitsplatz-Einrichtung des FA-Arbeitsvorrats. Aktivieren Sie im Bereich **Extended Output Response** die erweiterte Ausgabe-Rückmeldung und tragen Sie im Feld **Rückmeldepage-Nr.** die packmittelbasierte Rückmeldeseite (**Erw. Packmittel Rückmeldung**) ein. Siehe *Packmittelbasierte erweiterte Rückmeldung einrichten*.
2. **FA-Arbeitsvorrat öffnen:** Öffnen Sie über **Suchen** den **FA-Arbeitsvorrat**. Wählen Sie die **Arbeitsplatznr.** (und ggf. **Maschinenplatznr.**); es erscheinen die zugehörigen Fertigungsaufträge.
3. **Zeile wählen und Rückmeldung starten:** Markieren Sie eine gestartete Zeile und wählen Sie **Teilbeenden** (Teilmenge) oder **Beenden** (Abschluss des Arbeitsgangs).
4. **Chargen den Packmitteln zuweisen:** In **Erw. Packmittel Rückmeldung** markieren Sie im Bereich **Verfügbare Chargen** die Chargen und ordnen sie über **Chargen zuweisen** dem gewählten Packmittel zu, oder verwenden Sie **Alle Chargen zuweisen**.
5. **Packmittel bei Bedarf aufbauen:** Legen Sie mit **Packmittel erstellen**, **Innenverpackung erstellen** oder **Aus Packmittel Stückliste erstellen** die Struktur an und füllen Sie sie mit **Fülle Packmittel**.
6. **Bestätigen:** Schließen Sie die Seite mit **OK**. Fehlen Zuordnungen, meldet das System dies (siehe FAQ).
7. **Buchen:** Beim **Beenden** der letzten Rückmeldung werden die Packmittel gebucht; es entstehen Artikel- und Lagerposten, und die Packmittel werden als physische Packmittel fortgeschrieben.

Der Schnellstart nennt nur den kürzesten Weg. Auslöser, Rollen und Sonderfälle beschreibt das Kapitel *Typische Anwendungsfälle*.

---

## Einrichtung

Die Einrichtung dieses Moduls ist bewusst schlank: Die App fügt der Arbeitsplatz-Einrichtung des FA-Arbeitsvorrats **ein** steuerndes Feld hinzu (**Rückmeldepage-Nr.**), das die gesamte packmittelbasierte Rückmeldung freischaltet. Die eigentlichen Packmittel-Stammdaten (Packmittelcodes, Nummernserien, Packmittel-Stücklisten) werden in der App **m+m Packmittelverwaltung** gepflegt und sind Voraussetzung; sie werden hier als Voraussetzung benannt und mit den Aktionen verknüpft, die sie verwenden.

### Arbeitsplatz-Einrichtung des FA-Arbeitsvorrats

**Wer richtet ein und wann:** Der Administrator oder Key-User richtet die Arbeitsplatz-Einrichtung einmalig je Arbeitsplatz vor der ersten Rückmeldung ein. Die Einrichtung steuert, welche Rückmeldeseite die operativen Anwender im Kapitel *Tägliche Arbeit* sehen.

**Einstieg:** Öffnen Sie in der **Arbeitsplatzkarte** (Standard-BC-Arbeitsplatzstammdaten) die zugehörige Aktion für die Arbeitsplatz-Einrichtung des FA-Arbeitsvorrats (Objekt: `Prod. Order Job Work Center Setup`). Existiert noch keine Einrichtung für diesen Arbeitsplatz, bietet das System an, sie anzulegen, und öffnet anschließend die Karte. Die Einrichtungsseite ist nicht über **Suchen** erreichbar; sie wird ausschließlich über die Arbeitsplatzkarte aufgerufen.

Die Einrichtungsseite ist eine gemeinsame Oberfläche aus dem Basismodul, dem Stahl-Modul und dieser Erweiterung. Der Anwender sieht eine Seite; deshalb dokumentiert die folgende Tabelle die gesamte relevante Seite und hebt das von dieser App ergänzte Feld hervor.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Allgemeine Arbeitsplatzfelder** (Arbeitsplatzname, „Unproductive", „Start Multiple Jobs", „No Start-Action required", „Sort By", „Time Posting", „Post Only Duration", „Setup Activity", „Transfer", „Start Date-Time Editable", „Deactivate Direct Search POJ", „Show Sales Order No.", „Show Times") | Wenn diese Felder gesetzt sind, bestimmen sie das allgemeine Verhalten des FA-Arbeitsvorrats für diesen Arbeitsplatz (Anzeige, Sortierung, Zeiterfassung, Direktsuche). Sie stammen aus dem Basismodul FA-Arbeitsvorrat und beeinflussen die Packmittelzuordnung nicht direkt; sie werden hier als eine Gruppe zusammengefasst, weil nur die folgenden Felder das Packmittel-Verhalten steuern. |
| **Extended Output Response** (erw. Ausgabe-Rückmeldung aktiv) | Wenn aktiviert, verwendet der Arbeitsplatz die erweiterte Ausgabe-Rückmeldung statt der einfachen Mengenrückmeldung; erst dann kann eine packmittelbasierte Rückmeldeseite hinterlegt werden. Ohne dieses Kennzeichen ist das Feld **Rückmeldepage-Nr.** wirkungslos. (Feld aus dem Stahl-Basismodul.) |
| **Ext. O. R. Tr. Qty.** (mengenbasierte erw. Rückmeldung) | Wenn aktiviert, arbeitet die erweiterte Rückmeldung rein mengenbasiert. Für die packmittelbasierte Rückmeldung muss dieses Kennzeichen **deaktiviert** sein — andernfalls verweigert das System das Setzen der **Rückmeldepage-Nr.** (Prüfung im Code). |
| **Hide Posting Page** (Buchungsseite ausblenden) | Wenn aktiviert, überspringt das System beim Buchen die interaktive Rückmeldeseite und bucht direkt; der Anwender bestätigt dann keine Packmittelzuordnung mehr im Buchungsschritt. Ohne das Kennzeichen öffnet sich die Rückmeldeseite vor dem Buchen. (Feld aus dem Stahl-Basismodul; steuert den Buchungsablauf, siehe *Buchung und Folgebelege*.) |
| **Rückmeldepage-Nr.** | Wenn hier die Seite **Erw. Packmittel Rückmeldung** eingetragen ist, öffnet das Beenden/Teilbeenden am FA-Arbeitsvorrat die packmittelbasierte Rückmeldung: Der Anwender ordnet Chargen Packmitteln zu, bevor gebucht wird. Bleibt das Feld leer oder verweist es auf die materialbasierte Standard-Rückmeldeseite, läuft die klassische Rückmeldung ohne Packmittelzuordnung. Beim Setzen prüft das System, dass **Extended Output Response** aktiv und **Ext. O. R. Tr. Qty.** deaktiviert ist. (Feld dieser Erweiterung.) |
| **Material- und Ausschuss-Felder** (Materialorientiert, Rückmeldung ohne Material, Materialverbrauch buchen, Ausschuss-Lagerort/-Lagerplatz u. a.) | Wenn gesetzt, steuern diese Stahl-Basisfelder Materialverbrauch und Ausschussbuchung des Arbeitsgangs. Sie beeinflussen die Packmittelzuordnung nur indirekt (z. B. ob **Verbrauch anzeigen** in der Rückmeldung sichtbar ist) und sind hier als Gruppe zusammengefasst; ihre vollständige Erläuterung enthält das Handbuch des Stahl-FA-Arbeitsvorrats. |

#### Packmittelbasierte erweiterte Rückmeldung einrichten

Diese Fähigkeit setzt mehrere Konfigurationsschritte in Abhängigkeitsreihenfolge voraus. Wer sie einrichtet: Administrator/Key-User, vor der ersten Rückmeldung, je Arbeitsplatz. Wo sie greift: im Kapitel *Tägliche Arbeit* bei **Beenden**/**Teilbeenden**.

1. **Packmittel-Stammdaten bereitstellen (Voraussetzung):** Sorgen Sie in der **m+m Packmittelverwaltung** dafür, dass Packmittelcodes, die zugehörige **Nummernserie** für Packmittelnummern und – falls verwendet – **Packmittel-Stücklisten** vorhanden sind. Wenn diese fehlen, kann der Anwender später keine Packmittel erstellen (das System meldet z. B., dass keine Nummernserie gesetzt ist).
2. **Erweiterte Ausgabe-Rückmeldung aktivieren:** Aktivieren Sie in der Arbeitsplatz-Einrichtung **Extended Output Response**. Wenn aktiviert, schaltet der Arbeitsplatz von der einfachen Mengenrückmeldung auf die erweiterte Rückmeldung um; erst dann ist Schritt 4 möglich.
3. **Mengenmodus ausschließen:** Stellen Sie sicher, dass **Ext. O. R. Tr. Qty.** deaktiviert ist. Wenn dieses Kennzeichen gesetzt bliebe, würde das System die Rückmeldepage-Nr. abweisen und die packmittelbasierte Rückmeldung wäre nicht möglich.
4. **Rückmeldepage-Nr. setzen:** Tragen Sie im Feld **Rückmeldepage-Nr.** die Seite **Erw. Packmittel Rückmeldung** ein. Wenn gesetzt, öffnet das Beenden/Teilbeenden am FA-Arbeitsvorrat genau diese Seite und der Anwender ordnet Chargen Packmitteln zu.
5. **Optional Buchungsseite steuern:** Aktivieren Sie **Hide Posting Page**, wenn beim Buchen keine interaktive Rückmeldeseite erscheinen soll; der Anwender bestätigt dann Packmittel bereits im Rückmeldeschritt und nicht erneut beim Buchen.

**Operativer Abschluss:** Der Anwender löst die Kette später über **Beenden**/**Teilbeenden** am FA-Arbeitsvorrat aus (siehe *Tägliche Arbeit → Erw. Packmittel Rückmeldung*).

#### Packmittelreferenz-gestützte Packmittelerstellung einrichten

Diese zweite Fähigkeit ermöglicht es, aus einer am Fertigungsauftrag hinterlegten **Packmittelreferenz Nr.** die Packmittelstruktur automatisch zu erzeugen, statt sie manuell aufzubauen. Wer richtet ein: Administrator/Key-User gemeinsam mit den für Verpackungsvorschriften Verantwortlichen; wo greift es: in der **Erw. Rückmeldung Material** über die Aktion **Aus Packmittelreferenz erstellen**.

1. **Packmittelreferenzen pflegen (Voraussetzung):** Legen Sie in der **m+m Packmittelverwaltung** die Packmittelreferenzen (Verpackungsvorschriften) an, die als Vorlage dienen sollen. Wenn vorhanden, kann der Anwender sie am Fertigungsauftrag auswählen.
2. **Referenz am Beleg hinterlegen:** Der Anwender wählt in der **Erw. Rückmeldung Material** im Feld **Packmittelreferenz Nr.** die passende Referenz. Wenn gesetzt, prüft das System die Referenz gegen die Fertigungsauftragszeile und übernimmt sie als Vorgabe.
3. **Struktur erzeugen:** Über **Aus Packmittelreferenz erstellen** baut das System die Packmittelstruktur gemäß Referenz auf und verteilt die zurückgemeldeten Chargenmengen auf die Packmittel. Sind bereits Packmittel vorhanden, fragt das System zur Sicherheit nach, ob fortgefahren werden soll.

Beide Einrichtungswege überschneiden sich auf der Rückmeldeseite: Ist die Rückmeldepage-Nr. auf **Erw. Packmittel Rückmeldung** gesetzt, stehen sowohl die manuelle Chargenzuweisung als auch – bei gepflegter Referenz – die Referenzerzeugung zur Verfügung.

### Berechtigungen

Die App liefert den Berechtigungssatz **MuM PSP Permission**. Er legt fest, welche Aktionen die Anwender in den Packmittel-Rückmelde- und Buchungsobjekten dieser Erweiterung ausführen dürfen. Weisen Sie ihn den Rollen zu, die am FA-Arbeitsvorrat zurückmelden und buchen, zusätzlich zu den Berechtigungen der Basis- und Packmittelmodule.

---

## Stammdaten und Listen

Dieses Modul führt keine eigenen Stammdatenkarten (Packmittelcodes und Packmittel-Stücklisten liegen in der m+m Packmittelverwaltung). Es erweitert jedoch zwei zentrale Listen um Mengen- und Bezugsinformationen und stellt die FA-Arbeitsvorrat-Liste als Einstieg bereit.

### FA-Arbeitsvorrat (Einstiegsliste)

Der **FA-Arbeitsvorrat** ist die Übersicht aller Fertigungsaufträge je Arbeitsplatz und der Ausgangspunkt der täglichen Arbeit. Er wird über **Suchen** geöffnet. Diese Erweiterung fügt der Liste keine Spalten hinzu, sondern klinkt sich in die Aktionen **Beenden** und **Teilbeenden** ein (siehe *Tägliche Arbeit*).

#### Filter

Die Liste filtert man über die Kopffelder. Der Einstieg erfolgt **arbeitsplatzorientiert**: zuerst der Arbeitsplatz, danach optional der Maschinenplatz.

| Filterfeld | Erläuterung |
|------------|-------------|
| **Arbeitsplatznr.** | Wenn gesetzt, werden die Zeilen auf die Fertigungsaufträge dieses Arbeitsplatzes gefiltert; dies ist der erste, führende Filter. |
| **Maschinenplatznr.** | Wenn gesetzt, werden die Zeilen zusätzlich auf diesen Maschinenplatz eingeschränkt. Optional — bei reiner Arbeitsplatzsteuerung bleibt das Feld leer. |
| **FA Nr.** | Wenn gesetzt, wird auf einen bestimmten freigegebenen Fertigungsauftrag gefiltert. |
| **Datum** | Wenn gesetzt, werden die Zeilen nach Datum gefiltert. |
| **Sortieren nach** | Wenn gesetzt, bestimmt die Sortierreihenfolge der Zeilen. |
| **Fertige ausblenden** | Wenn aktiviert, werden bereits beendete Zeilen ausgeblendet, sodass nur offene Arbeit erscheint. |
| **Offene ausblenden** | Wenn aktiviert, werden offene Zeilen ausgeblendet (z. B. zur Kontrolle bereits erledigter Rückmeldungen). |
| **Buchungen im vorherigen Arbeitsgang** | Wenn aktiviert, werden nur Zeilen angezeigt, bei denen der vorherige Arbeitsgang bereits Buchungen aufweist. |

### Erw. Packmittel-Belege Liste (erweiterte Spalten)

Diese Erweiterung ergänzt die Belegpackmittel-Liste der Packmittelverwaltung um die branchenüblichen Bewegungsmengen. So sieht der Anwender je Packmittelzeile nicht nur die Stückmenge, sondern auch KG und Meter.

| Feld | Erläuterung |
|------|-------------|
| **Bewegungsmenge KG** | Wenn ein Wert vorhanden ist, zeigt er die dieser Packmittelzeile zugeordnete Menge in Kilogramm; er wird bei der Chargenzuweisung aus der Umrechnung (KG pro Meter/Stück) fortgeschrieben. |
| **Bewegungsmenge Meter** | Wenn ein Wert vorhanden ist, zeigt er die zugeordnete Menge in Metern; bei Längenmaterial die führende Steuergröße der Zuordnung. |
| **Bewegungsmenge Stück** | Wenn ein Wert vorhanden ist, zeigt er die zugeordnete Stückzahl; bei stückbezogenem Material die führende Steuergröße. |

### Physische Packmittel (erweiterte Spalten und Bezug)

Nach dem Buchen werden Beleg-Packmittel zu **physischen Packmitteln**. Diese Erweiterung ergänzt die Liste der physischen Packmittel um Bewegungsmengen und einen Bezug zurück auf den FA-Arbeitsvorrat.

| Feld | Erläuterung |
|------|-------------|
| **Bewegungsmenge KG** | Wenn ein Wert vorhanden ist, zeigt er die im physischen Packmittel enthaltene Menge in Kilogramm; sie wird beim Buchen aus dem Beleg-Packmittel übernommen. |
| **Bewegungsmenge Meter** | Wenn ein Wert vorhanden ist, zeigt er die enthaltene Menge in Metern. |
| **Bewegungsmenge Stück** | Wenn ein Wert vorhanden ist, zeigt er die enthaltene Stückzahl. |
| **Anzahl WIP Prod. Packmittel** | Wenn der Wert größer als null ist, gibt es noch nicht gebuchte Beleg-Packmittel (WIP) zu dieser Packmittelgruppe. Ein Aufruf des Feldes öffnet die Liste **WIP Prod. Belegpackmittel-Liste** mit genau diesen offenen Belegpackmitteln. |

---

## Tägliche Arbeit am FA-Arbeitsvorrat

Die tägliche Arbeit wird durch die Arbeitsplatz-Einrichtung gesteuert (Kapitel *Einrichtung*): Nur wenn dort **Extended Output Response** aktiv ist und die **Rückmeldepage-Nr.** auf **Erw. Packmittel Rückmeldung** verweist, erscheinen die hier beschriebenen Packmittelseiten. Andernfalls läuft die klassische materialbasierte Rückmeldung.

### Erw. Rückmeldung Material (Belegzeile)

Die **Erw. Rückmeldung Material** ist die zentrale Rückmeldeseite je Fertigungsauftragszeile. Sie stammt aus dem Stahl-Basismodul (Kopfbereich mit Buchungsdaten/-zeiten, Materialzeilen mit Mengen in Menge/KG/Meter/Stück, Rest- und gebuchten Mengen sowie den Unterseiten **Chargen** und **Rest-Chargen**). Diese Erweiterung ergänzt den Kopf, eine Aktion und eine Infobox.

**Vom Modul ergänzte Elemente:**

| Feld / Aktion | Erläuterung |
|---------------|-------------|
| **Packmittelreferenz Nr.** (Kopf) | Wenn gesetzt, wird die gewählte Verpackungsvorschrift gegen die Fertigungsauftragszeile geprüft und als Vorgabe für die Packmittelerstellung übernommen; wurde bereits am Fertigungsauftrag oder Verkaufsauftrag eine Referenz gewählt, erscheint sie hier vorbelegt. Ohne Referenz baut der Anwender die Packmittel manuell auf. |
| **Packmittelzuweisung Chargen** (Aktion) | Öffnet die Seite **Beleg Packmittel** für die aktuelle Zeile. Dort weist der Anwender den zurückgemeldeten Chargen die Packmittel zu und baut die Packmittelstruktur auf. Die Aktion ist nur bei bearbeitbarer (gestarteter) Rückmeldung aktiv. |
| **Aus Packmittelreferenz erstellen** (Aktion) | Wenn eine **Packmittelreferenz Nr.** gepflegt ist, erzeugt die Aktion die Packmittelstruktur automatisch gemäß Referenz und verteilt die Chargenmengen darauf. Sind bereits Packmittel vorhanden, erscheint zunächst die Rückfrage **„Es sind bereits Packmittel erstellt worden. Sind Sie sich sicher, dass Sie fortfahren möchten?"**. |
| **Beleg Packmittelstruktur** (Infobox) | Zeigt zur aktuellen Zeile die aufgebaute Packmittelstruktur des Produktionsbelegs an, damit der Anwender die Zuordnung ohne Seitenwechsel kontrollieren kann. |

Ändert der Anwender in dieser Seite die **Menge**, prüft das Modul sofort, ob Packmittelmenge und Rückmeldemenge noch zusammenpassen, und weist auf Abweichungen hin (siehe *Buchung und Folgebelege*).

### Erw. Packmittel Rückmeldung (Rückmeldeseite mit Chargenzuweisung)

Ist die **Rückmeldepage-Nr.** entsprechend eingerichtet, öffnet **Beenden**/**Teilbeenden** am FA-Arbeitsvorrat die Seite **Erw. Packmittel Rückmeldung**. Sie ist eine zusammengesetzte Seite mit zwei Bereichen. Der Kopf enthält das Feld **Packmittelreferenz Nr.** (Vorbelegung wie oben).

#### Bereich „Packmittelliste"

Zeigt die Packmittelstruktur des Belegs als Baum (Packmittel, Innenverpackungen, Artikel). Wichtige Spalten:

| Feld | Erläuterung |
|------|-------------|
| **Packmittel Nr.** / **Packmittel Code** | Identifizieren das einzelne Packmittel bzw. seinen Packmitteltyp. |
| **Zeilenart** | Bestimmt die Art der Zeile im Baum. **Packmittel:** ein Packmittel als Behälter. **Innenverpackung:** eine Unterteilung innerhalb eines Packmittels. **Artikel:** ein verpackter Artikel (Charge) innerhalb eines Packmittels oder einer Innenverpackung. |
| **Stufe** / **Übergeordnete Packmittel Nr.** | Bilden die Verschachtelung des Baums ab; die übergeordnete Nummer verweist auf das umschließende Packmittel. |
| **Belegzeilennr.** | Wenn gesetzt, verknüpft die Artikelzeile mit der Rückmelde-/Belegzeile; bei aus Chargen erzeugten Zeilen nicht editierbar. |
| **Bewegungsmenge / KG / Meter / Stück** | Die dem Packmittel zugeordnete Menge; bei Längen-/Gewichtsmaterial führen KG/Meter, bei Stückmaterial die Stückzahl. |
| **Restmenge physisch** / **Physische Menge** / **Belegmenge** | Zeigen offene physische Menge, bereits physisch erfasste Menge und die Belegmenge zur Kontrolle der Zuordnung. |
| **Von verfügbaren Chargen** | Wenn aktiviert, wurde die Zeile aus der Chargenzuweisung erzeugt; solche Zeilen sind gegen manuelle Mengenänderung geschützt. |
| **Packmittel nicht verbrauchen** | Wenn aktiviert, wird dieses Packmittel beim Buchen nicht als verbraucht gebucht (z. B. Mehrwegbehälter). |

Aktionen im Bereich Packmittelliste: **Packmittel erstellen**, **Innenverpackung erstellen**, **Aus Packmittel Stückliste erstellen**, **Fülle Packmittel**, **Packmittel auswählen**, **vorh. Artikel aus Packmittel auswählen**, **Packmittelgruppe löschen** sowie **Oben/Unten/Links/Rechts** zum Verschieben von Zeilen im Baum.

#### Bereich „Verfügbare Chargen"

Zeigt die zurückgemeldeten, noch nicht vollständig verpackten Chargen. Hier trägt der Anwender die zu verpackenden Mengen ein.

| Feld | Erläuterung |
|------|-------------|
| **Artikel Nr.** / **Varianten Code** / **Chargennr.** / **Seriennr.** | Identifizieren die verfügbare Charge. |
| **Lagerort Code** / **Lagerplatzcode** | Herkunftslager/-platz der Charge; steuert, welchem Packmittel sie zugeordnet werden darf (Lager/Platz müssen zusammenpassen). |
| **Menge gesamt / KG / Meter / Stück** | Die insgesamt verfügbare Chargenmenge in den vier Größen (nicht editierbar). |
| **Menge zu verpacken / KG / Meter / Stück** | Die Menge, die der Anwender aktuell verpacken will. Wenn ein Wert eingetragen wird, rechnet das Modul die übrigen Größen um; der Wert darf die noch nicht verpackte Restmenge nicht übersteigen, sonst erscheint die Meldung **„… muss kleiner oder gleich … sein"**. |
| **Menge verpackt / KG / Meter / Stück** | Die bereits verpackte Menge (Summe aus den zugeordneten Packmittelzeilen). |
| **Komplett verpackt** | Wenn aktiviert, ist die Charge vollständig einem Packmittel zugeordnet; nur dann lässt sich der Arbeitsgang beenden. |

**Aktionen (Menüband):**

| Aktion | Erläuterung |
|--------|-------------|
| **Chargen zuweisen** | Ordnet die im Bereich Verfügbare Chargen markierten Chargen dem im Bereich Packmittelliste markierten **einen** Packmittel zu (es darf nur ein Packmittel markiert sein, sonst Meldung **„Sie können nur ein Packmittel auswählen"**). Die zugewiesene Menge wird als Artikelzeile unter dem Packmittel angelegt. |
| **Alle Chargen zuweisen** | Weist alle passenden verfügbaren Chargen dem markierten Packmittel zu, ohne dass der Anwender jede Charge einzeln markieren muss. |
| **Aus Packmittel entfernen** | Entfernt zuvor aus Chargen erzeugte, noch nicht gebuchte Artikelzeilen wieder aus den Packmitteln, sodass die Chargen erneut zugewiesen werden können. |
| **Verbrauch anzeigen** | Zeigt den Materialverbrauch zur erweiterten Ausgabe-Rückmeldung an. Sichtbar nur, wenn der Arbeitsplatz Materialverbrauch bucht. |

Bestätigen mit **OK** übernimmt die Zuordnung; **Abbrechen** verwirft sie.

### Beleg Packmittel (Packmittel-Arbeitsblatt)

Die Aktion **Packmittelzuweisung Chargen** in der Erw. Rückmeldung Material öffnet das Arbeitsblatt **Beleg Packmittel**. Es dient dem Aufbau der Packmittelstruktur zu genau einer Rückmeldezeile und zeigt oben die Kennzahl **Menge zur Anpassung anstehend** (offene, noch zu verteilende Menge). Solange dieser Wert kleiner als null wäre, lässt sich die Seite nicht schließen (Meldung **„Die Menge, die angepasst werden muss, ist kleiner als null…"**).

Die Zeilen bilden denselben Packmittelbaum wie oben (Zeilenart Packmittel/Innenverpackung/Artikel, Stufe, Beschreibung, Menge, Lagerort/Lagerplatz, Physisch, Bewegungsmengen KG/Meter/Stück). Technische Spalten (Postennr., Reihenfolge, Stufe, Innenverpackungsdetails, Herkunftsdatensatz) sind standardmäßig ausgeblendet.

**Aktionen:**

| Aktion | Erläuterung |
|--------|-------------|
| **Packmittel erstellen** | Öffnet den Dialog *Packmittel erstellen* zum Anlegen eines oder mehrerer Packmittel. |
| **Aus Packmittel Stückliste erstellen** | Erzeugt die Packmittelstruktur aus einer hinterlegten Packmittel-Stückliste der Packmittelverwaltung. |
| **Fülle Packmittel** | Füllt ein bestehendes Packmittel mit den zurückgemeldeten Artikeln/Chargen (Dialog *Fülle Beleg Packmittel*). |
| **Packmittel auswählen** | Übernimmt ein vorhandenes physisches Packmittel als Vorlage in den Beleg. |
| **Packmittelgruppe löschen** | Löscht die markierte Packmittelgruppe nach Rückfrage **„Wollen Sie wirklich die ausgewählten Packmittelgruppen löschen?"**. |
| **Oben / Unten / Links / Rechts** | Verschieben eine Zeile im Baum: Links/Rechts ändern die Verschachtelungsstufe, Oben/Unten die Reihenfolge. |

### Dialoge zur Packmittelerstellung

Beim Aufbau der Struktur unterstützen drei Dialoge:

#### Packmittel erstellen

| Feld | Erläuterung |
|------|-------------|
| **Packmittel Code** | Wenn gewählt, wird bei genau einem Packmittel automatisch die nächste **Packmittel Nr.** aus der Nummernserie vorgeschlagen und Beschreibung/Beschreibung 2 aus dem Packmittelcode übernommen. |
| **Packmittel Nr.** | Die eindeutige Nummer des zu erstellenden Packmittels; bei mehreren Packmitteln vergibt das System sie automatisch. |
| **Beschreibung** / **Beschreibung 2** | Werden aus dem Packmittelcode übernommen und dienen der Kennzeichnung. |
| **Lagerort Code** / **Lagerplatzcode** | Bestimmen, wo das Packmittel geführt wird; bei lagerplatzpflichtigen Lagerorten ist der Lagerplatz Pflicht. |
| **Anzahl der Packmittel** | Wenn größer als eins, erstellt das System mehrere gleichartige Packmittel mit automatisch vergebenen Nummern. |
| **Erstelle Packmittel in einem anderen Packmittel** | Wenn aktiviert, wird das neue Packmittel innerhalb eines vorhandenen Packmittels angelegt; die Felder **Zu Packmittel Nr.** / **Zu Packmittel Code** legen das Ziel fest. |

#### Innenverpackung erstellen

| Feld | Erläuterung |
|------|-------------|
| **Packmittel Code** (Innenverpackung) | Wenn gewählt, werden Innenverpackungsart und Beschreibung aus dem gewählten Innenverpackungscode übernommen. |
| **Innenverpackungsart** | Zeigt die aus dem Code abgeleitete Art der Innenverpackung (nicht editierbar). |
| **Beschreibung** | Kennzeichnet die Innenverpackung. |
| **Zu Packmittel Nr.** | Das Packmittel, in dem die Innenverpackung angelegt wird. Ist es leer, meldet das System beim Schließen **„Ein Packmittel in einem Packmittel kann nicht mit einer leeren Packmittelnr. erstellt werden"**. |

#### Fülle Beleg Packmittel

| Feld | Erläuterung |
|------|-------------|
| **Zu Packmittel Nr.** / **Zu Packmittel Code** | Bestimmen das Zielpackmittel, in das die markierten Artikel/Chargen gefüllt werden. |
| **Zeilen (Artikel, Charge, Menge, KG/Meter/Stück, Lagerort/Lagerplatz)** | Zeigen die füllbaren Rückmeldezeilen; die Bewegungsmengen KG/Meter/Stück können vor dem Füllen angepasst werden. |

### WIP Prod. Belegpackmittel-Liste und Packmittel auswählen

- **WIP Prod. Belegpackmittel-Liste** (über **Suchen** oder aus der Kennzahl **Anzahl WIP Prod. Packmittel** der physischen Packmittel): zeigt alle noch nicht gebuchten Beleg-Packmittel als Baum, damit der Anwender offene Verpackungsarbeit erkennt.
- **Packmittel auswählen** (über **Suchen** oder aus der Aktion **Packmittel auswählen**): listet die physischen Packmittel je Lagerort/Lagerplatz. Über **Packmittelgruppe auswählen** markiert der Anwender eine ganze Packmittelgruppe zur Übernahme.

---

## Buchung und Folgebelege

Der Buchungsablauf ist im Code fest verdrahtet und knüpft an die Rückmeldung an. Die folgende Reihenfolge gilt für die packmittelbasierte Rückmeldung (Rückmeldepage-Nr. = **Erw. Packmittel Rückmeldung**):

1. Auf dem **FA-Arbeitsvorrat** eine gestartete Zeile markieren.
2. **Teilbeenden** (Teilmenge) oder **Beenden** (Abschluss) wählen.
3. Es öffnet sich **Erw. Packmittel Rückmeldung**; Chargen den Packmitteln zuweisen (**Chargen zuweisen** / **Alle Chargen zuweisen**), Struktur bei Bedarf ergänzen, mit **OK** bestätigen.
4. Beim **Beenden** prüft das System, dass **alle** verfügbaren Chargen komplett verpackt sind. Ist eine Charge nicht **Komplett verpackt**, bricht es mit **„Es wurden nicht allen Chargen Packmittel zugewiesen."** ab.
5. Anschließend prüft das System, ob Packmittelmenge und zurückgemeldete Menge übereinstimmen:
   - Beim **letzten Arbeitsgang** und **Beenden** ist eine Abweichung nicht zulässig: **„Die Abweichung zwischen Verpackungsmaterial und Ausbringungsmenge muss vor Abschluss des letzten Vorgangs des Produktionsauftrags behoben werden."**
   - Sonst erscheint die Rückfrage **„Die zugewiesenen Packmittel weisen eine Differenz zu den eingetragenen Mengen auf, möchten sie die arbeit beenden?"** bzw. das Angebot, die Packmittel anzupassen (**„… möchten Sie die Packmittel anpassen?"**), was die Belegpackmittel-Liste öffnet.
6. Das Modul überträgt die zugewiesenen Packmittel in die Belegpackmittelstruktur der FA-Zeile.
7. Ist **Hide Posting Page** gesetzt, entfällt die interaktive Rückmeldeseite beim Buchen; das System bucht direkt.
8. Beim Buchen der **Ausgabe des letzten Arbeitsgangs** werden die Beleg-Packmittel zu **physischen Packmitteln**: Es entstehen Artikel- und (bei lagerplatzpflichtigem Lager) Lagerposten, die Zeilen werden als **Posten gebucht** bzw. **Lager gebucht** markiert und als **Gebucht vom FA-Arbeitsvorrat** gekennzeichnet.
9. Ist in der Packmittelverwaltung die automatische Verkaufszuweisung aktiv und ist die gebuchte Menge für eine Verkaufsauftragszeile reserviert, werden die entstandenen Packmittel automatisch dieser Verkaufszeile zugewiesen.

**Teilmengen:** **Teilbeenden** ist ausdrücklich erlaubt; das Modul überträgt die Packmittel auch bei Teilrückmeldung. Ein Zwang, „erst bei vollständigem Mengenausgleich zu schließen", besteht **nur** für den letzten Arbeitsgang beim vollständigen **Beenden** (Schritt 5). Bei früheren Arbeitsgängen kann der Anwender die Abweichung bestätigen und fortfahren.

---

## Historie, Archiv und Nachverfolgung

- **WIP Prod. Belegpackmittel-Liste:** Offene, noch nicht gebuchte Beleg-Packmittel je Fertigungsauftrag; dient der Verfolgung offener Verpackungsarbeit vor dem Buchen.
- **Physische Packmittel:** Nach dem Buchen entstandene Packmittel mit Bewegungsmengen KG/Meter/Stück; über **Anzahl WIP Prod. Packmittel** ist der Rücksprung zu noch offenen Belegpackmitteln möglich.
- **Archiv (Arch. Erw. Packmittel Rückmeldung):** Wird ein Fertigungsauftrag archiviert, überträgt das Modul die Packmittelstruktur in die archivierten Rückmeldeansichten. So bleibt nachvollziehbar, welche Chargen in welchen Packmitteln zurückgemeldet wurden. Die archivierten Ansichten sind nicht editierbar.

---

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Ablauf ausgehend von realistischen Auslösern. Alle genannten Seiten und Aktionen sind im Code hinterlegt.

### Szenario 1 — Stahllängen aus der Fertigung verpacken und zurückmelden

1. **Auslöser:** Ein Werker meldet am Arbeitsplatz, dass ein gestarteter Fertigungsauftrag für Stabstahl fertig zum Rückmelden ist.
2. **Einstieg in BC:** Der Rückmelder öffnet über **Suchen** den **FA-Arbeitsvorrat**, wählt die **Arbeitsplatznr.** und markiert die gestartete Zeile.
3. **Kernablauf:** Er wählt **Beenden**. Da für den Arbeitsplatz die **Rückmeldepage-Nr.** auf **Erw. Packmittel Rückmeldung** gesetzt ist, öffnet sich diese Seite. Im Bereich **Verfügbare Chargen** trägt er je Charge die **Menge zu verpacken** (bzw. **… Meter/KG**) ein, markiert im Bereich **Packmittelliste** das Zielpackmittel und wählt **Chargen zuweisen**. Fehlt noch ein Behälter, legt er ihn über **Packmittel erstellen** an. Sind alle Chargen **Komplett verpackt**, bestätigt er mit **OK**.
4. **Abschluss:** Beim Buchen prüft das System die vollständige Zuordnung und die Mengenübereinstimmung, schreibt die Packmittel als physische Packmittel fort und erzeugt Artikel- und Lagerposten. Die gebuchten Zeilen erscheinen als **Gebucht vom FA-Arbeitsvorrat**.

### Szenario 2 — Verpacken nach Verpackungsvorschrift (Packmittelreferenz)

1. **Auslöser:** Für einen Kundenauftrag gilt eine feste Verpackungsvorschrift; der Vertrieb hat am Fertigungsauftrag eine Packmittelreferenz hinterlegt.
2. **Einstieg in BC:** Der Rückmelder öffnet den **FA-Arbeitsvorrat**, wählt die Zeile und startet die Rückmeldung; alternativ arbeitet er in der **Erw. Rückmeldung Material**.
3. **Kernablauf:** Im Feld **Packmittelreferenz Nr.** erscheint die vorbelegte Referenz. Er wählt **Aus Packmittelreferenz erstellen**; das System baut die Packmittelstruktur gemäß Referenz auf und verteilt die Chargenmengen. Gibt es Chargen ohne zugeordnete Menge, fragt das System **„Es gibt einige Chargen ohne zugeordnete Menge. Möchten Sie fortfahren?"**. Nach Bestätigung meldet es **„Beleg Packmittel erfolgreich erstellt."**.
4. **Abschluss:** Er beendet den Arbeitsgang; die Buchung erfolgt wie in Szenario 1. Ist die automatische Verkaufszuweisung aktiv und die gebuchte Menge reserviert, ordnet das System die Packmittel direkt dem Verkaufsauftrag zu.

### Szenario 3 — Teilrückmeldung mit späterer Restverpackung

1. **Auslöser:** Nur ein Teil der Charge ist verpackt; der Rest folgt in einer späteren Schicht.
2. **Einstieg in BC:** Der Rückmelder öffnet den **FA-Arbeitsvorrat** und markiert die gestartete Zeile.
3. **Kernablauf:** Er wählt **Teilbeenden**, trägt in **Erw. Packmittel Rückmeldung** nur die bereits verpackte **Menge zu verpacken** ein, weist sie über **Chargen zuweisen** zu und bestätigt mit **OK**. Da es sich nicht um den letzten Arbeitsgang bzw. um eine Teilmenge handelt, ist ein vollständiger Mengenausgleich nicht erzwungen; eine Restmenge bleibt offen.
4. **Abschluss:** In einer späteren Schicht öffnet er die Zeile erneut, verpackt den Rest und **beendet** den Arbeitsgang. Erst dann verlangt das System die vollständige Zuordnung aller Chargen.

---

## FAQ und Troubleshooting

### Warum öffnet sich beim Beenden keine Packmittelseite, sondern die normale Rückmeldung?
Weil in der Arbeitsplatz-Einrichtung die **Rückmeldepage-Nr.** nicht auf **Erw. Packmittel Rückmeldung** gesetzt ist oder **Extended Output Response** nicht aktiviert wurde. Ohne diese Einrichtung läuft die klassische, materialbasierte Rückmeldung.

### Warum lässt sich die Rückmeldepage-Nr. nicht setzen?
Das System verlangt beim Setzen, dass **Extended Output Response** aktiv und **Ext. O. R. Tr. Qty.** deaktiviert ist. Ist der Mengenmodus (Ext. O. R. Tr. Qty.) aktiv, wird die Eingabe abgewiesen. Aktivieren Sie zuerst die erweiterte Ausgabe-Rückmeldung und deaktivieren Sie den Mengenmodus.

### Was passiert, wenn nicht allen Chargen ein Packmittel zugewiesen ist?
Beim **Beenden** bricht das System mit **„Es wurden nicht allen Chargen Packmittel zugewiesen."** ab. Weisen Sie im Bereich **Verfügbare Chargen** die offenen Chargen zu, bis das Kennzeichen **Komplett verpackt** überall gesetzt ist.

### Warum meldet das System „Sie können nur ein Packmittel auswählen"?
**Chargen zuweisen** ordnet Chargen immer genau **einem** Packmittel zu. Markieren Sie im Bereich **Packmittelliste** nur ein einziges Packmittel und lösen Sie die Aktion erneut aus.

### Was bedeutet die Abweichungsmeldung beim letzten Arbeitsgang?
Stimmen Packmittelmenge und zurückgemeldete Menge beim letzten Arbeitsgang nicht überein, verlangt das System die Korrektur vor dem Abschluss: **„Die Abweichung zwischen Verpackungsmaterial und Ausbringungsmenge muss vor Abschluss des letzten Vorgangs des Produktionsauftrags behoben werden."** Passen Sie die zu verpackenden Mengen oder die Packmittel an, bis die Mengen übereinstimmen.

### Kann ich einen Arbeitsgang teilweise zurückmelden?
Ja. Über **Teilbeenden** melden Sie eine Teilmenge zurück; das Modul überträgt die zugewiesenen Packmittel auch bei Teilrückmeldung. Der vollständige Mengenausgleich wird erst beim **Beenden** des letzten Arbeitsgangs erzwungen.

### Warum kann ich die Seite „Beleg Packmittel" nicht schließen?
Wenn die noch anzupassende Menge kleiner als null wäre, meldet das System **„Die Menge, die angepasst werden muss, ist kleiner als null. Bitte passen Sie die Mengen an, bevor Sie die Seite schließen."**. Korrigieren Sie die Artikelmengen in der Struktur, sodass die anstehende Menge nicht negativ ist.

### Warum kann ich eine aus Chargen erzeugte Zeile nicht in der Menge ändern?
Zeilen mit dem Kennzeichen **Von verfügbaren Chargen** entstehen aus der Chargenzuweisung und sind gegen manuelle Mengenänderung geschützt. Nutzen Sie **Aus Packmittel entfernen** und weisen Sie die Charge mit der gewünschten Menge neu zu.

### Warum schlägt „Packmittel erstellen" mit einem Nummernserien-Hinweis fehl?
Für den gewählten **Packmittel Code** ist keine Packmittel-Nummernserie hinterlegt bzw. die zentrale Serie in der Packmittelverwaltung fehlt. Hinterlegen Sie die Nummernserie in der m+m Packmittelverwaltung.

### Wo sehe ich, was bereits gebucht ist und was noch offen ist?
Offene, noch nicht gebuchte Beleg-Packmittel zeigt die **WIP Prod. Belegpackmittel-Liste** (auch erreichbar über die Kennzahl **Anzahl WIP Prod. Packmittel** an den physischen Packmitteln). Gebuchte Packmittel erscheinen als **physische Packmittel** und tragen an der Belegzeile die Kennzeichen **Posten gebucht** / **Lager gebucht** sowie **Gebucht vom FA-Arbeitsvorrat**.
