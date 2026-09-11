---
title: Anwenderhandbuch m+m Drop- and Special Shipment
---

# Anwenderhandbuch m+m Drop- and Special Shipment

## Einleitung

Die App **m+m Drop- and Special Shipment** erweitert Microsoft Dynamics 365 Business Central um eine weitgehend automatisierte Abwicklung von **Direktgeschäft**, **Spezialauftrag** und **Release Geschäft**. Sie verbindet den **Verkaufsauftrag** mit der daraus erzeugten **Bestellung**, damit Verkauf und Einkauf denselben Vorgang gemeinsam bearbeiten, ohne die Belege manuell aneinander koppeln zu müssen.

Die drei Geschäftstypen unterscheiden sich im Warenweg und in der Buchungslogik:

- **Direktgeschäft (Direktlieferung):** Der Kreditor liefert den Artikel unmittelbar an den Debitor; die Ware läuft nicht über das eigene Lager. Verkaufsauftrag und Bestellung sind verknüpft. Sobald der Einkauf die Einkaufslieferung bucht, wird die Lieferung des Verkaufsauftrags automatisch im Hintergrund mitgebucht.
- **Spezialauftrag:** Die bestellte Ware kommt zunächst ins eigene Unternehmen (z. B. zum Umpacken oder zur weiteren Bearbeitung) und wird erst danach an den Debitor geliefert. Die Verkaufslieferung wird hier **nicht** automatisch, sondern manuell vom Verkauf gebucht.
- **Release Geschäft:** Eine Erweiterung des Spezialauftrags. Zusätzlich werden die Lieferadressfelder („Lieferung an") aus dem Verkaufsauftrag in die Bestellung übernommen, sodass der Kreditor direkt an die im Auftrag hinterlegte Zieladresse liefern kann. Beim Setzen von **Release Geschäft** wird **Spezialauftrag** automatisch mitgesetzt.

### Zielgruppe

Primäre Zielgruppe sind die **operativen Anwender im Verkauf und im Einkauf**, die täglich Aufträge und Bestellungen erfassen, freigeben und buchen: Der Verkauf legt den Verkaufsauftrag an, kennzeichnet die Zeile über den **Einkaufscode**, wählt die **Kreditor-Nr.** und stößt die Bestellung an; der Einkauf bearbeitet die erzeugte Bestellung und bucht Wareneingang und Rechnung. Sekundär richtet sich das Handbuch an **Administratoren und Key-User**, die die **Einkaufscodes** und die **Lagerorte** einmalig einrichten (siehe Kapitel *Einrichtung*).

### Kurzer Prozessüberblick

Der Anwender kennzeichnet eine Verkaufszeile über einen entsprechend eingerichteten **Einkaufscode** und einen dafür freigegebenen **Lagerort**, gibt den Verkaufsauftrag frei und erzeugt über eine Aktion automatisch die zugehörige **Bestellung**. Anschließend wird der Vorgang je nach Geschäftstyp im Einkauf und Verkauf gebucht. Die Einrichtung der Einkaufscodes und Lagerorte ist damit die Voraussetzung für die tägliche Arbeit und wird zuerst beschrieben.

## Schnellstart für Anwender

Der Schnellstart zeigt den kürzesten Weg vom eingerichteten System bis zur erzeugten Bestellung. Die Einrichtung (Schritte 1–2) führt der Administrator einmalig durch; die tägliche Arbeit (ab Schritt 3) erfolgt im Verkauf.

1. **Einkaufscode einrichten** (einmalig, Administrator): In **Einkaufscodes** einen Code anlegen und je nach Geschäftstyp **Direktlieferung**, **Spezialauftrag** oder **Release Geschäft** aktivieren (siehe *Einrichtung › Einkaufscodes*).
2. **Lagerort freigeben** (einmalig, Administrator): Im gewünschten **Lagerort** (Seite Lagerortkarte) die passenden Kennzeichen **Direktgeschäft**, **Spezialauftrag** und/oder **Release Geschäft** setzen (siehe *Einrichtung › Lagerorte*).
3. **Verkaufsauftrag anlegen:** Öffnen Sie einen neuen **Verkaufsauftrag** und erfassen Sie den Debitor sowie die Artikelzeile mit **Lagerortcode** (Lagerort mit passendem Kennzeichen).
4. **Einkaufscode in der Verkaufszeile setzen:** Wählen Sie in der Verkaufszeile den eingerichteten **Einkaufscode**. Damit wird die Zeile automatisch als **Selektiert für Bestellung** markiert; bei falsch eingerichtetem Lagerort lässt sich der Einkaufscode nicht auswählen.
5. **Kreditor-Nr. prüfen/erfassen:** Kontrollieren Sie in der Verkaufszeile die **Kreditor-Nr.** Fehlt sie und ist auch am Artikel bzw. an der Lagerhaltungsdaten kein Kreditor hinterlegt, kann keine Bestellung erzeugt werden.
6. **Verkaufsauftrag freigeben:** Geben Sie den Verkaufsauftrag über die Standardfunktion **Freigeben** frei. Ohne Freigabe (Status **Freigegeben**) bricht die Erzeugung mit Fehlermeldung ab.
7. **Bestellung erzeugen:** Wählen Sie im Verkaufsauftrag die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen**. Bestätigen Sie die Abfrage **„Soll(en) die Bestellung(en) angezeigt werden?"** mit **Ja**, um die automatisch erzeugte **Bestellung** direkt zu öffnen.
8. **Buchen:** Direktgeschäft – der Einkauf bucht Wareneingang und die Verkaufslieferung wird automatisch mitgebucht. Spezialauftrag/Release Geschäft – der Verkauf bucht die Verkaufslieferung manuell (siehe *Lager und Folgebelege*).

## Einrichtung

Die Einrichtung erfolgt vollständig in Microsoft Dynamics 365 Business Central. Sie besteht aus zwei aufeinander abgestimmten Bereichen: den **Einkaufscodes**, die den Geschäftstyp einer Verkaufszeile bestimmen, und den **Lagerorten**, die festlegen, welcher Lagerort für welchen Geschäftstyp verwendet werden darf. Beide greifen zusammen: Ein Einkaufscode lässt sich in der Verkaufszeile nur auswählen, wenn der dort gewählte Lagerort passend eingerichtet ist. Deshalb richten Administratoren zuerst die Lagerorte und die Einkaufscodes ein, bevor die Anwender im Tagesgeschäft damit arbeiten.

### Einkaufscodes einrichten

**Einstieg:** Öffnen Sie über die BC-Funktion **Suchen** die Seite **Einkaufscodes**. Die Einkaufscodes sind eine unternehmensweite Stammdatenliste ohne eigene übergeordnete Einstiegsseite; der Aufruf über **Suchen** ist hier der vorgesehene Weg.

**Prozesskontext:** Der Administrator bzw. Key-User legt die Einkaufscodes einmalig vor der ersten Nutzung an. Ein Einkaufscode entscheidet, ob eine Verkaufszeile als Direktgeschäft, Spezialauftrag oder Release Geschäft behandelt wird. Der Verkauf wählt diesen Code später in der Verkaufszeile aus (siehe *Tägliche Arbeit im Verkaufsauftrag*). Über die Aktion **Neu** legen Sie einen neuen Code an oder bearbeiten einen bestehenden.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Code | Eindeutiger Schlüssel der Einkaufsaktivität. Wenn gesetzt, steht der Code in der Verkaufszeile im Feld **Einkaufscode** zur Auswahl und bestimmt dort den Geschäftstyp. |
| Beschreibung | Klartext zur Einkaufsaktivität. Wenn gepflegt, sehen die Anwender in der Auswahlliste eine sprechende Bezeichnung statt nur des Codes und wählen den richtigen Code sicherer aus. |
| Direktlieferung | Wenn aktiviert, wird eine Verkaufszeile mit diesem Einkaufscode als **Direktgeschäft** verarbeitet: Die Zeile wird als **Selektiert für Bestellung** markiert, der gewählte Lagerort muss das Kennzeichen **Direktgeschäft** tragen, und bei der späteren Buchung des Wareneingangs wird die Verkaufslieferung automatisch mitgebucht. |
| Spezialauftrag | Wenn aktiviert, wird die Verkaufszeile als **Spezialauftrag** verarbeitet: Die Ware läuft zunächst über das eigene Lager, die Zeile wird als **Selektiert für Bestellung** markiert, und der Lagerort muss das Kennzeichen **Spezialauftrag** tragen. Die Verkaufslieferung wird später manuell gebucht. |
| Release Geschäft | Wenn aktiviert, wird die Verkaufszeile als **Release Geschäft** verarbeitet; zusätzlich werden die Lieferadressfelder aus dem Verkaufsauftrag in die erzeugte Bestellung übernommen. Beim Aktivieren setzt das System zwingend auch **Spezialauftrag**; ohne gesetzten Spezialauftrag lässt sich Release Geschäft nicht speichern. |

**Abhängigkeit (aus AL):** Für einen Release-Einkaufscode müssen **Spezialauftrag** und **Release Geschäft** gemeinsam gesetzt sein – das System erzwingt dies beim Speichern. Wird **Release Geschäft** wieder entfernt, prüft das System die Kombination erneut.

Der Einkaufscode ist außerdem als Spalte in der Liste **Einkaufscodes (Übersicht)** verfügbar; dort erscheint das Kennzeichen **Release Geschäft** ebenfalls als zusätzliche Spalte, sodass Anwender die Release-fähigen Codes direkt in der Übersicht erkennen.

### Lagerorte einrichten

**Einstieg:** Öffnen Sie über **Suchen** die **Lagerorte** und dort per Aktion **Bearbeiten** die **Lagerortkarte**; alternativ Lagerorteliste → Zeile → Karte öffnen. Die drei Kennzeichen liegen im Register **Allgemein** der Lagerortkarte.

**Prozesskontext:** Je Lagerort legt der Administrator fest, für welche Geschäftstypen dieser Lagerort im Rahmen der App genutzt werden darf. Diese Kennzeichen wirken als Schranke in der Verkaufszeile: Nur wenn der in der Zeile gewählte Lagerort das zum Einkaufscode passende Kennzeichen trägt, lässt sich der Einkaufscode setzen; andernfalls bricht das System mit einer Fehlermeldung ab (z. B. „Der Lagerort … ist nicht für eine Direktlieferung vorgesehen." bzw. „… nicht für ein Spezialgeschäft vorgesehen.").

| Einrichtung | Erläuterung |
|-------------|-------------|
| Direktgeschäft | Wenn aktiviert, darf dieser Lagerort in Verkaufszeilen mit einem Direktlieferungs-Einkaufscode verwendet werden. Ohne dieses Kennzeichen wird die Auswahl eines Direktlieferungs-Einkaufscodes mit dem Lagerort abgelehnt. |
| Spezialauftrag | Wenn aktiviert, darf dieser Lagerort für Verkaufszeilen mit einem Spezialauftrags-Einkaufscode verwendet werden. Ohne dieses Kennzeichen wird die Auswahl eines Spezialauftrags-Einkaufscodes mit dem Lagerort abgelehnt. |
| Release Geschäft | Wenn aktiviert, ist der Lagerort zusätzlich für Release Geschäfte freigegeben. Beim Aktivieren setzt das System automatisch auch **Spezialauftrag**, weil das Release Geschäft technisch auf dem Spezialauftrag aufsetzt; ein reiner Release-Lagerort ohne Spezialauftrag ist damit nicht möglich. |

**Abhängigkeit (aus AL):** Das Setzen von **Release Geschäft** validiert automatisch **Spezialauftrag** = Ja. Für die Auswahl eines Spezialauftrags- oder Release-Einkaufscodes prüft das System zusätzlich, dass die Verkaufszeile einen **Lagerortcode** trägt (Pflichtfeld) und dass der Lagerort das Kennzeichen **Spezialauftrag** besitzt.

> Die Lagerortkarte ist eine Standardseite von Business Central mit zahlreichen weiteren Feldern (Adresse, Lagerlogistik, Behälter usw.). Für diese App sind ausschließlich die drei oben genannten Kennzeichen im Register **Allgemein** relevant; die übrigen Felder der Lagerortkarte behalten ihr Standardverhalten und werden hier nicht verändert.

### Geschäftstyp end-to-end einrichten (Zusammenspiel Einkaufscode und Lagerort)

Damit ein Anwender im Tagesgeschäft eine Direkt-, Spezial- oder Releasebestellung erzeugen kann, müssen mehrere Einstellungen über zwei Seiten hinweg zusammenpassen. Der Administrator richtet sie in folgender Reihenfolge ein:

1. **Lagerort freigeben (Stammdaten):** Öffnen Sie die **Lagerortkarte** des Lagerorts, über den der Geschäftstyp abgewickelt werden soll, und setzen Sie das passende Kennzeichen (**Direktgeschäft**, **Spezialauftrag** oder **Release Geschäft**). Wenn dieses Kennzeichen fehlt, kann der zugehörige Einkaufscode in Verkaufszeilen mit diesem Lagerort nicht ausgewählt werden.
2. **Einkaufscode anlegen (globale Einrichtung):** Legen Sie in **Einkaufscodes** einen Code an und aktivieren Sie dieselbe Ausprägung (**Direktlieferung**, **Spezialauftrag** oder **Release Geschäft**; für Release zusätzlich Spezialauftrag). Wenn gesetzt, steht der Code in der Verkaufszeile zur Auswahl und markiert die Zeile automatisch als **Selektiert für Bestellung**.
3. **Kreditor bereitstellen (Voraussetzung):** Stellen Sie sicher, dass am Artikel oder an den Lagerhaltungsdaten (Lagerort/Variante) eine **Kreditor-Nr.** hinterlegt ist, oder erfassen Sie sie später direkt in der Verkaufszeile. Ohne Kreditor bricht die Erzeugung der Bestellung ab.
4. **Operativer Abschluss (Tagesablauf):** Der Verkauf setzt den Einkaufscode in der Verkaufszeile, gibt den Auftrag frei und startet die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** (siehe *Tägliche Arbeit im Verkaufsauftrag*).

## Stammdaten

Die App bringt keine eigenen Stammdatentabellen mit, sondern erweitert bestehende Standard-Stammdaten von Business Central um steuernde Kennzeichen. Fachlich relevant sind zwei Stammdatenflächen: der **Einkaufscode** (Klassifizierung der Einkaufsaktivität) und der **Lagerort** (zulässige Geschäftstypen). Beide sind oben unter *Einrichtung* mit vollständiger Feldtabelle beschrieben, weil sie zugleich die zentrale Konfiguration der App bilden.

### Einkaufscode als Stammsatz

Der **Einkaufscode** ist der Stammsatz, den der Verkauf in der Verkaufszeile auswählt. Über das Kennzeichen **Release Geschäft** (zusätzliche Spalte in **Einkaufscodes** und in der Übersichtsliste) erkennt der Anwender, welche Codes ein Release Geschäft auslösen. Wann gepflegt: einmalig bei der Einrichtung und bei neuen Geschäftstypen. Wo wirksam: als Feld **Einkaufscode** in der Verkaufszeile; die Auswahl steuert direkt die weitere Verarbeitung (siehe *Tägliche Arbeit im Verkaufsauftrag*). Details und alle Felder: *Einrichtung › Einkaufscodes*.

### Lagerort als Stammsatz

Der **Lagerort** trägt die drei Freigabekennzeichen **Direktgeschäft**, **Spezialauftrag** und **Release Geschäft**. Wann gepflegt: bei Einrichtung der Lager und immer dann, wenn ein Lagerort für einen weiteren Geschäftstyp freigegeben werden soll. Wo wirksam: bei der Auswahl des Einkaufscodes in der Verkaufszeile – der Lagerort entscheidet, ob der Geschäftstyp zulässig ist. Details und alle Felder: *Einrichtung › Lagerorte*.

## Tägliche Arbeit im Verkaufsauftrag

Die tägliche Arbeit findet im **Verkaufsauftrag** statt. Voraussetzung sind die unter *Einrichtung* beschriebenen Einkaufscodes und Lagerorte: Der Einkaufscode bestimmt den Geschäftstyp, der Lagerort gibt den Geschäftstyp frei, und die Kreditor-Nr. steuert, bei welchem Kreditor bestellt wird. Ohne diese Konfiguration lässt sich der Einkaufscode nicht setzen und die Bestellung nicht erzeugen.

### Felder in der Verkaufszeile

Die App ergänzt die Verkaufszeile (Unterseite **Zeilen** des Verkaufsauftrags) um drei Felder. Die übrigen Spalten der Verkaufszeile (z. B. **Nr.**, **Beschreibung**, **Menge**, **Lagerortcode**, **Einkaufscode**) sind Standardfelder von Business Central und behalten ihr Standardverhalten.

| Feld | Erläuterung |
|------|-------------|
| Kreditor-Nr. | Kreditor, bei dem die Ware bestellt wird. Wenn beim Setzen des Einkaufscodes am Artikel oder an den Lagerhaltungsdaten ein Kreditor hinterlegt ist, füllt das System dieses Feld automatisch; andernfalls tragen Sie den Kreditor manuell ein. Das Feld lässt sich nur pflegen, wenn die Zeile als **Selektiert für Bestellung** markiert ist. Ist keine Kreditor-Nr. ermittelbar, bricht die Erzeugung der Bestellung mit einer Meldung ab. |
| Selektiert für Bestellung | Steuert, ob die Zeile bei der Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** berücksichtigt wird. Wenn aktiviert, fließt die Zeile in die zu erzeugende Bestellung ein. Das System setzt das Kennzeichen automatisch beim Auswählen eines Direkt-/Spezial-/Release-Einkaufscodes und entfernt es, wenn der Einkaufscode entfernt oder auf einen neutralen Code geändert wird. Ein manuelles Setzen ohne **Direktgeschäft** bzw. **Spezialauftrag** in der Zeile lehnt das System mit einer Fehlermeldung ab. |
| Release Geschäft | Kennzeichnet die Zeile als Release Geschäft. Das Feld ist nicht editierbar und wird vom System aus dem gewählten Einkaufscode abgeleitet. Wenn gesetzt, überträgt die Bestellerzeugung zusätzlich die Lieferadressfelder aus dem Verkaufsauftrag in die Bestellung, und in der erzeugten Bestellung steht ebenfalls das Kennzeichen **Release Geschäft**. |

### Vorgehen: Bestellung aus dem Verkaufsauftrag erzeugen

Die Reihenfolge ist im Code fest vorgegeben; halten Sie sie ein, sonst bricht der Vorgang ab.

1. **Verkaufsauftrag öffnen** und die Artikelzeile mit dem gewünschten **Lagerortcode** erfassen.
2. **Einkaufscode wählen:** Setzen Sie in der Verkaufszeile den passenden **Einkaufscode**. Ist die Spalte nicht sichtbar, blenden Sie sie über die Personalisierung ein. Das System markiert die Zeile daraufhin als **Selektiert für Bestellung** und übernimmt – sofern vorhanden – die **Kreditor-Nr.** aus Artikel oder Lagerhaltungsdaten. Passt der Lagerort nicht zum Geschäftstyp, wird die Auswahl mit einer Fehlermeldung abgelehnt.
3. **Kreditor-Nr. sicherstellen:** Ergänzen Sie die **Kreditor-Nr.** in der Zeile, falls sie nicht automatisch gefüllt wurde.
4. **Verkaufsauftrag freigeben:** Geben Sie den Auftrag über die Standardaktion **Freigeben** frei (Status **Freigegeben**). Ohne Freigabe verweigert das System die Bestellerzeugung.
5. **Bestellung erzeugen:** Wählen Sie im Menüband die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen**. Das System sammelt alle Zeilen des Auftrags, die als **Selektiert für Bestellung** markiert und noch keiner Bestellung zugeordnet sind, und erzeugt daraus je Kreditor eine **Bestellung** (bzw. hängt die Zeile an eine bereits im selben Lauf erzeugte Bestellung desselben Kreditors an).
6. **Bestellung anzeigen:** Bestätigen Sie die Abfrage **„Soll(en) die Bestellung(en) angezeigt werden?"** mit **Ja**. Bei genau einer erzeugten Bestellung öffnet sich die **Bestellung**, bei mehreren die Liste der Bestellungen.

**Was das System dabei überträgt:** Direktgeschäft-Zeilen erhalten in der Bestellung das Standardkennzeichen **Direktlieferung** und die Verknüpfung zum Verkaufsauftrag; die Lieferadresse des Debitors wird als Debitor in den Bestellkopf übernommen. Spezialauftrags-Zeilen werden als **Spezialauftrag** in der Bestellung geführt. Release-Zeilen werden ebenfalls als Spezialauftrag geführt, zusätzlich werden die Felder „Lieferung an" (Code, Name, Adresse, Ort, Land) aus dem Verkaufsauftrag in den Bestellkopf kopiert.

### Wechsel zwischen Verkaufsauftrag und Bestellung

Bei Release Geschäften können Anwender jederzeit zwischen den verknüpften Belegen wechseln:

- **Aus der Bestellung zum Verkaufsauftrag:** Wählen Sie in der Einkaufszeile die Aktion **Release Geschäft › Auftrag**. Das System öffnet den zugehörigen Verkaufsauftrag (schreibgeschützt), sofern die Einkaufszeile das Kennzeichen **Release Geschäft** trägt und eine Spezialauftrags-Verknüpfung besitzt.
- **Aus dem Verkaufsauftrag zur Bestellung:** Wählen Sie in der Verkaufszeile die Aktion **Release Geschäft › Bestellung**. Das System öffnet die verknüpfte Bestellung; ist die Bestellung bereits gebucht, wird stattdessen die gebuchte Einkaufslieferung angezeigt (bei genau einem Beleg die Karte, sonst die Übersicht).

## Lager, Buchung und Folgebelege

Nach dem Freigeben und Buchen der Bestellung entscheidet der Geschäftstyp über den weiteren Buchungsablauf. Die App greift dabei in die Standardbuchung ein und verknüpft Einkaufs- und Verkaufsbeleg über Reservierungen.

### Buchungsablauf je Geschäftstyp

- **Direktgeschäft:** Der Einkauf gibt die Bestellung frei und bucht den **Wareneingang** (Einkaufslieferung). Da die Ware direkt vom Kreditor zum Debitor geht, wird die **Verkaufslieferung** des verknüpften Verkaufsauftrags automatisch im Hintergrund mitgebucht. Der Einkauf kann die Einkaufsrechnung erst buchen, nachdem der Verkauf die Verkaufsrechnung gebucht hat.
- **Spezialauftrag:** Der Einkauf bucht den Wareneingang ins eigene Lager. Die **Verkaufslieferung** wird **nicht** automatisch gebucht, sondern muss anschließend manuell vom Verkauf gebucht werden. Die Einkaufsrechnung kann der Einkauf unabhängig davon bereits vor der Verkaufsrechnung buchen.
- **Release Geschäft:** Verhält sich in der Buchung wie der Spezialauftrag (manuelle Verkaufslieferung), liefert aber physisch an die aus dem Verkaufsauftrag übernommene Adresse.

### Reservierung und Verknüpfung

Beim Kopieren einer Einkaufszeile in die Artikelposten (Buchung des Wareneingangs) stellt die App bei Spezialauftrag und Release Geschäft eine Reservierungsverknüpfung zwischen der Einkaufsbestellzeile und der zugehörigen Verkaufszeile her. Dadurch wird die eingehende Menge der richtigen Verkaufszeile zugeordnet; offene Restmengen werden anteilig verteilt, bis die Verkaufszeile gedeckt ist. Steht die Verkaufszeile in Verbindung mit einer Fertigungsauftragskomponente, überträgt die App die Reservierung stattdessen auf die passende Fertigungsauftragskomponente. Diese Verknüpfung läuft ohne Anwendereingriff im Hintergrund.

### Gebuchte Belege und Nachverfolgung

Auf der **Gebuchten Einkaufslieferung** trägt die App das Kennzeichen **Release-Geschäft** mit, sodass Release-Vorgänge auch nach der Buchung erkennbar bleiben. Aus dem Verkaufsauftrag heraus lässt sich über **Release Geschäft › Bestellung** die zugehörige gebuchte Einkaufslieferung aufrufen, wenn die Bestellung bereits gebucht ist. Die Artikelposten des Vorgangs zeigen nach den Lieferbuchungen den erwarteten Bestand (bei Direktgeschäft ohne Lagerzugang).

## Berechtigungen

Die App liefert den Berechtigungssatz **„All permissions"** (Objektname MuM DS Permission). Er ist zuweisbar und bestimmt die Berechtigungen für die App-eigenen Objekte: Er gewährt Lese- und Schreibrechte auf die interne Puffertabelle sowie die Ausführungsrechte für die beiden Codeunits der App. Der Berechtigungssatz legt damit fest, welche Aktionen Anwender im Zusammenhang mit der Bestellerzeugung ausführen können. Weisen Sie diesen Satz den Anwendern zu, die Direkt-, Spezial- und Releasebestellungen erzeugen. Für die eigentliche Belegbearbeitung (Verkaufsauftrag, Bestellung, Buchung) gelten zusätzlich die Standard-Berechtigungen von Business Central.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die drei Geschäftstypen im Arbeitsalltag ausgelöst und in Business Central abgewickelt werden. Alle Schritte entsprechen dem im Code hinterlegten Ablauf.

### Direktgeschäft: Kunde bestellt Lagerartikel ohne eigenen Bestand

**Auslöser:** Ein Debitor bestellt telefonisch einen Artikel, den das Unternehmen nicht bevorratet. Der Artikel soll direkt vom Kreditor an den Debitor geliefert werden.

**Einstieg in BC:** Der Verkauf legt einen neuen **Verkaufsauftrag** an und erfasst die Artikelzeile mit einem Lagerort, der das Kennzeichen **Direktgeschäft** trägt.

**Kernablauf:**
1. In der Verkaufszeile den **Einkaufscode** mit Kennzeichen **Direktlieferung** wählen – die Zeile wird **Selektiert für Bestellung**, die **Kreditor-Nr.** wird aus dem Artikel übernommen.
2. **Kreditor-Nr.** kontrollieren.
3. Verkaufsauftrag **Freigeben**.
4. Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** starten.
5. Abfrage **„Soll(en) die Bestellung(en) angezeigt werden?"** mit **Ja** bestätigen – die erzeugte **Bestellung** öffnet sich.

**Abschluss:** Der Einkauf gibt die Bestellung frei und bucht den Wareneingang; die Verkaufslieferung wird automatisch mitgebucht. Anschließend bucht der Verkauf die Verkaufsrechnung, danach der Einkauf die Einkaufsrechnung.

### Spezialauftrag: Ware wird vor der Auslieferung im Haus bearbeitet

**Auslöser:** Ein Debitor bestellt einen Artikel, der vor der Auslieferung im eigenen Haus umgepackt bzw. bearbeitet werden muss. Die Ware soll also zunächst ins eigene Lager kommen.

**Einstieg in BC:** Neuer **Verkaufsauftrag**; Artikelzeile mit einem Lagerort, der das Kennzeichen **Spezialauftrag** trägt.

**Kernablauf:**
1. In der Verkaufszeile den **Einkaufscode** mit Kennzeichen **Spezialauftrag** wählen (Lagerortcode ist Pflicht) – die Zeile wird **Selektiert für Bestellung**.
2. **Kreditor-Nr.** prüfen bzw. eintragen.
3. Verkaufsauftrag **Freigeben**.
4. Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** ausführen und die Abfrage mit **Ja** bestätigen.

**Abschluss:** Der Einkauf bucht den Wareneingang ins Lager. Nach der internen Bearbeitung bucht der Verkauf die **Verkaufslieferung manuell** und anschließend die Verkaufsrechnung.

### Release Geschäft: Direktlieferung an eine abweichende Lieferadresse

**Auslöser:** Ein Debitor bestellt Ware, die der Kreditor direkt an eine im Verkaufsauftrag hinterlegte, vom Debitor abweichende Lieferadresse senden soll.

**Einstieg in BC:** Neuer **Verkaufsauftrag** mit gepflegten Feldern „Lieferung an"; Artikelzeile mit einem Lagerort, der das Kennzeichen **Release Geschäft** (und damit **Spezialauftrag**) trägt.

**Kernablauf:**
1. **Einkaufscode** mit Kennzeichen **Release Geschäft** in der Verkaufszeile wählen – die Zeile wird **Selektiert für Bestellung** und als **Release Geschäft** markiert.
2. **Kreditor-Nr.** sicherstellen.
3. Verkaufsauftrag **Freigeben**.
4. Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** starten und mit **Ja** bestätigen.
5. In der geöffneten **Bestellung** prüfen, dass die Felder „Lieferung an" aus dem Verkaufsauftrag übernommen wurden.

**Abschluss:** Der Einkauf gibt die Bestellung frei und bucht die Lieferung an die übernommene Adresse; der Verkauf bucht die Verkaufslieferung manuell. Über **Release Geschäft › Auftrag** (in der Bestellung) bzw. **Release Geschäft › Bestellung** (im Verkaufsauftrag) wechseln die Anwender jederzeit zwischen den Belegen.

## FAQ und Troubleshooting

### 1. Warum lässt sich der Einkaufscode in der Verkaufszeile nicht auswählen?
Der gewählte Lagerort ist nicht für den Geschäftstyp freigegeben. Setzen Sie auf der **Lagerortkarte** das passende Kennzeichen (**Direktgeschäft**, **Spezialauftrag** oder **Release Geschäft**). Ohne dieses Kennzeichen lehnt das System die Auswahl ab.

### 2. Was passiert, wenn ich einen Direktlieferungs-Einkaufscode ohne passenden Lagerort setze?
Das System bricht mit der Meldung „Der Lagerort … ist nicht für eine Direktlieferung vorgesehen." ab. Aktivieren Sie zuerst **Direktgeschäft** auf der Lagerortkarte.

### 3. Warum verlangt das System bei Spezialauftrag und Release Geschäft einen Lagerortcode?
Für Spezialauftrag und Release Geschäft ist der **Lagerortcode** in der Verkaufszeile Pflicht, weil die Ware physisch über das eigene Lager läuft und der Lagerort das zugehörige Kennzeichen **Spezialauftrag** tragen muss. Ohne Lagerortcode bricht die Auswahl des Einkaufscodes ab.

### 4. Warum wird beim Aktivieren von „Release Geschäft" automatisch „Spezialauftrag" gesetzt?
Das Release Geschäft baut technisch auf dem Spezialauftrag auf. Deshalb erzwingt das System beim Setzen von **Release Geschäft** – sowohl im Einkaufscode als auch auf der Lagerortkarte – automatisch **Spezialauftrag**.

### 5. Warum kann ich die Bestellung nicht erzeugen, obwohl die Zeile korrekt aussieht?
Der Verkaufsauftrag ist nicht freigegeben. Die Erzeugung setzt den Status **Freigegeben** voraus; geben Sie den Auftrag zuerst über **Freigeben** frei.

### 6. Was passiert, wenn keine Kreditor-Nr. gefunden wird?
Findet das System weder in der Verkaufszeile noch an Artikel oder Lagerhaltungsdaten eine **Kreditor-Nr.**, bricht es mit der Meldung „Es kann kein Geschäft für die Verkaufszeile … erstellt werden. Es wurde keine Kreditor-Nr. ausgewählt für Artikel …" ab. Tragen Sie die Kreditor-Nr. in der Zeile ein.

### 7. Wie werden mehrere Zeilen mit demselben Kreditor verarbeitet?
Zeilen desselben Kreditors bündelt das System im selben Lauf in **eine** Bestellung; weitere Zeilen werden an die bereits erzeugte Bestellung dieses Kreditors angehängt. Für unterschiedliche Kreditoren entstehen mehrere Bestellungen.

### 8. Warum werden einige Zeilen bei der Erzeugung übersprungen?
Berücksichtigt werden nur Zeilen mit gesetztem Kennzeichen **Selektiert für Bestellung**, mit Typ **Artikel**, mit gesetztem **Einkaufscode** und ohne bereits zugeordnete Bestellnummer. Zeilen, die diese Bedingungen nicht erfüllen, bleiben unberücksichtigt.

### 9. Warum wird beim Direktgeschäft meine Verkaufslieferung automatisch gebucht?
Beim Direktgeschäft geht die Ware unmittelbar vom Kreditor zum Debitor. Deshalb bucht das System bei der Buchung des Wareneingangs die zugehörige **Verkaufslieferung** automatisch mit. Beim Spezialauftrag und Release Geschäft geschieht dies bewusst nicht – hier buchen Sie die Verkaufslieferung manuell.

### 10. Wie gelange ich vom Verkaufsauftrag zur erzeugten Bestellung (und zurück)?
Nutzen Sie im Verkaufsauftrag die Aktion **Release Geschäft › Bestellung** und in der Bestellung die Aktion **Release Geschäft › Auftrag**. Ist die Bestellung bereits gebucht, öffnet der Aufruf aus dem Verkaufsauftrag stattdessen die gebuchte Einkaufslieferung.
