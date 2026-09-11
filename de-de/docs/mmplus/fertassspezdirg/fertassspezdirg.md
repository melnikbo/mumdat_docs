---
title: Anwenderhandbuch m+m Production Order Assistant with Drop-/Special Shipment
---

# Anwenderhandbuch m+m Production Order Assistant with Drop-/Special Shipment

## Einleitung

Die App **m+m Production Order Assistant with Drop-/Special Shipment** ist eine Erweiterung für „Microsoft Dynamics 365 Business Central". Sie ist ein **Bindeglied** zwischen zwei m+m-Modulen: dem **m+m Production Order Assistant** (Fertigungsassistent) und dem **m+m Drop-/Special Shipment** (Direkt-/Spezialgeschäft). Die App fügt selbst keine eigenen Seiten hinzu, sondern sorgt dafür, dass beide Module in einem gemeinsamen Verkaufsprozess korrekt zusammenspielen.

Konkret regelt die App zwei Dinge:

- Für Verkaufszeilen, die als **Release Geschäft** gekennzeichnet sind, wird bei der Freigabe des Verkaufsauftrags **kein** automatischer Fertigungsauftrag erzeugt. Diese Zeilen werden stattdessen über die Bestellung des Direkt-/Spezialgeschäfts abgewickelt.
- Der **Fertigungsassistent** lässt sich – gesteuert über eine Einrichtungsoption – auch für Verkaufszeilen mit **Spezialauftrag** aufrufen, obwohl der Assistent solche Zeilen im Standard blockieren würde.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender im Verkauf und Einkauf**, die täglich mit Verkaufsaufträgen arbeiten – also Verkaufszeilen erfassen, Aufträge freigeben, Bestellungen aus dem Verkaufsauftrag erzeugen und den Fertigungsassistenten aus der Verkaufszeile starten. Sekundär angesprochen sind **Administratoren und Key-User**, welche die **Fertigungsassistent Einrichtung**, die **Einkaufscodes** und die **Lagerorte** vor der ersten Nutzung konfigurieren.

**Kurzer Prozessüberblick:** Der Anwender legt einen Verkaufsauftrag an und kennzeichnet eine Zeile über den **Einkaufscode** als Direktlieferung, Spezialauftrag oder Release Geschäft. Nach der Freigabe des Auftrags erzeugt der Anwender über eine Aktion im Verkaufsauftrag die zugehörige **Bestellung**. Für Zeilen mit Spezialauftrag kann zusätzlich über die Verkaufszeile der **Fertigungsassistent** gestartet werden, um einen Fertigungsauftrag zu erzeugen.

## Schnellstart für Anwender

Der Schnellstart zeigt den kürzesten Weg zum Ergebnis. Die Einrichtung ist Voraussetzung und steht deshalb am Anfang.

**Einmalig einrichten (Administrator/Key-User):**

1. **Fertigungsassistent Einrichtung** über **Suchen** öffnen und die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** aktivieren, wenn der Fertigungsassistent für Spezialauftrags-Zeilen genutzt werden soll. Zusätzlich **FA-Status für Verkaufsaufträge** festlegen.
2. **Einkaufscode** über **Suchen** öffnen und einen Code mit gesetztem **Spezialauftrag** und **Release Geschäft** anlegen (für ein Release-Geschäft müssen beide Haken gesetzt sein).
3. **Lagerorte** über **Suchen** öffnen, die betroffene **Lagerortkarte** aufrufen und **Release Geschäft** (bzw. **Direktgeschäft**/**Spezialauftrag**) aktivieren.

**Täglich arbeiten (Verkauf/Einkauf):**

4. **Verkaufsauftrag** anlegen, Artikelzeile erfassen und in der Zeile den in Schritt 2 angelegten **Einkaufscode** setzen. Dadurch werden **Spezialauftrag** und **Release Geschäft** in der Zeile gesetzt.
5. In der Verkaufszeile **Selektiert für Bestellung** aktivieren und bei Bedarf eine **Kreditor-Nr.** hinterlegen.
6. Den Verkaufsauftrag **freigeben** (Status **Freigegeben**).
7. Im Verkaufsauftrag die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** aufrufen.
8. Die Abfilterung „Soll die Bestellung geöffnet werden?" mit **Ja** bestätigen; die erzeugte **Bestellung** öffnet sich.
9. *(Optional, für Spezialauftrags-Zeilen ohne Release Geschäft)* In der Verkaufszeile über **Zeile → Fertigungsassistent** den Assistenten öffnen und mit **OK** einen Fertigungsauftrag erzeugen.

## Einrichtung

Die Einrichtung ist in „Microsoft Dynamics 365 Business Central" durchzuführen. Da diese App das Zusammenspiel von Fertigungsassistent und Direkt-/Spezialgeschäft steuert, sind drei Konfigurationsbereiche relevant: die zentrale **Fertigungsassistent Einrichtung**, die **Einkaufscodes** und die **Lagerorte**. Die letzten beiden bilden zusammen mit einer globalen Option die Freischaltkette für das Release-Geschäft.

### Fertigungsassistent Einrichtung

**Einstieg:** Über **Suchen** die Seite **Fertigungsassistent Einrichtung** öffnen.

**Wer/wann:** Diese Seite konfiguriert der Administrator bzw. Key-User **einmalig vor der ersten Nutzung**. Es handelt sich um eine unternehmensweite Einrichtung (ein Datensatz je Mandant). Die hier gesetzten Optionen steuern, mit welchem Status und unter welchen Bedingungen der Fertigungsassistent aus dem Verkaufsbeleg heraus Fertigungsaufträge erzeugt – und ob dies auch für Zeilen mit **Spezialauftrag** erlaubt ist. Die App **m+m Production Order Assistant with Drop-/Special Shipment** wertet die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** aus (siehe Abschnitt *Zusammenspiel der Module*).

| Einrichtung | Erläuterung |
|-------------|-------------|
| **FA-Status für Verkaufsangebote** | Wenn ein Fertigungsauftrag aus einem Verkaufsangebot erzeugt wird, dann erhält er den hier gewählten Status. Zulässig sind **Simuliert**, **Geplant**, **Fest geplant** und **Freigegeben**; der Status **Fertig** ist nicht erlaubt und wird abgewiesen. **Simuliert:** unverbindlicher Vorschlag ohne Reservierung/Buchung. **Geplant:** eingeplant, aber noch nicht fest terminiert. **Fest geplant:** fest terminiert, für die Fertigung vorgesehen. **Freigegeben:** zur Fertigung freigegeben, Rückmeldungen möglich. |
| **FA-Status für Verkaufsaufträge** | Wenn ein Fertigungsauftrag aus einem Verkaufsauftrag erzeugt wird, dann erhält er den hier gewählten Status. Werte wie oben: **Simuliert**, **Geplant**, **Fest geplant**, **Freigegeben** (nicht **Fertig**). Der Wert bestimmt, ob die erzeugten Aufträge nur simuliert sind oder bereits fest in der Fertigungsplanung erscheinen. |
| **Setze Bestätigt-Status nach Fertigungsassistentaufruf im VK-Beleg** | Wenn aktiviert, dann erhält der über den Fertigungsassistenten erzeugte Fertigungsauftrag (und die zugehörige Zeile) den Prüfstatus „Bestätigt"; ohne diese Option bleibt der Prüfstatus „Offen". Dadurch ist für nachgelagerte Prüfungen sofort erkennbar, dass der Auftrag über den Assistenten bestätigt wurde. |
| **Zeitformel, um FAs für Verkaufsangebote zu löschen** | Wenn eine Zeitformel hinterlegt ist, dann werden simulierte Fertigungsaufträge zu Verkaufsangeboten nach Ablauf dieser Frist automatisch bereinigt; bleibt das Feld leer, findet keine automatische Löschung statt. Verhindert das Anwachsen simulierter Aufträge zu nicht gewandelten Angeboten. |
| **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen** | Wenn aktiviert, dann wird bei der **Freigabe** des Verkaufsauftrags automatisch ein Fertigungsauftrag für die betroffenen Zeilen erzeugt; ohne die Option erzeugt der Anwender den Fertigungsauftrag manuell über die Aktion **Fertigungsassistent**. Für Zeilen mit **Release Geschäft** wird diese automatische Erzeugung durch die vorliegende App unterdrückt (siehe *Zusammenspiel der Module*). |
| **Abfrage zur Erstellung von Fertigungsaufträgen innerhalb Verkaufsaufträgen** | Wenn aktiviert, dann erscheint bei der Freigabe eine Rückfrage, bevor Fertigungsaufträge erzeugt werden; der Anwender entscheidet pro Freigabe. Diese Option setzt voraus, dass **Fertigungsauftrag bei Verkaufsauftragsfreigabe erstellen** aktiv ist (wird andernfalls beim Validieren abgewiesen). |
| **"FA erstellen" in der Verkaufszeile vorbelegen** | Legt fest, wie das Zeilenfeld **FA erstellen** in neuen Verkaufszeilen vorbelegt wird. **Keine:** keine Vorbelegung, der Anwender setzt den Haken je Zeile selbst. **Alle:** in allen neuen Zeilen wird **FA erstellen** vorbelegt, sodass ohne weitere Aktion ein Fertigungsauftrag vorgesehen ist. Auch diese Option setzt eine aktive Freigabe-Automatik voraus. |
| **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** | Wenn aktiviert, dann darf der Fertigungsassistent auch für Verkaufszeilen mit **Spezialauftrag** ausgeführt werden; ist die Option nicht gesetzt, blockiert der Assistent solche Zeilen und meldet, dass für Spezialauftrags-Zeilen kein Fertigungsauftrag erzeugt werden darf. **Dies ist die zentrale Steueroption dieser App** für den Assistenten-Pfad. |
| **Löschen von zugeh. FA beim Löschen des VK-Auftrags** | Wenn aktiviert, dann werden beim Löschen eines Verkaufsauftrags auch die daraus erzeugten, zugeordneten Fertigungsaufträge gelöscht; ohne die Option bleiben verwaiste Fertigungsaufträge bestehen und müssen manuell entfernt werden. |
| **Verkäufer bei Statuswechsel benachrichtigen** | Wenn aktiviert, dann erhält der zuständige Verkäufer eine Benachrichtigung, sobald sich der Status eines aus dem Verkauf erzeugten Fertigungsauftrags ändert; ohne die Option erfolgt keine automatische Information an den Verkauf. |

Hinweis: Das technische Feld für die Übernahme der Artikelverfolgung aus dem Fertigungsauftrag an den Verkaufsauftrag ist in der aktuellen Programmversion außer Funktion gesetzt und erscheint dem Anwender nicht mehr; es ist deshalb hier nicht aufgeführt.

### Release-Geschäft einrichten

Das Release-Geschäft benötigt eine Kette aus **Stammdaten** und **Einrichtung**, bevor es im Tagesgeschäft genutzt werden kann. Wer das Release-Geschäft konfiguriert, legt zuerst den Einkaufscode an, kennzeichnet dann die Lagerorte und ruft die Funktion anschließend im Verkaufsauftrag auf. Die Reihenfolge ergibt sich aus den Prüfungen im Programm.

**Zuerst – Einkaufscode für das Release-Geschäft anlegen**

**Einstieg:** Über **Suchen** die Seite **Einkaufscodes** öffnen. Über **Neu** einen neuen Code erfassen oder einen bestehenden bearbeiten.

Der **Einkaufscode** ist die Standard-Business-Central-Stammdatentabelle, über die eine Verkaufszeile als Direktlieferung oder Spezialauftrag gekennzeichnet wird. Das Modul Direkt-/Spezialgeschäft ergänzt hier das Kennzeichen **Release Geschäft**. Der Anwender im Verkauf wählt den Code später in der Verkaufszeile aus; über den Code werden die Kennzeichen automatisch in die Zeile übernommen.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Code** | Wenn ein Code vergeben ist, dann steht er im Verkauf zur Auswahl in der Verkaufszeile bereit; er ist der Schlüssel, über den die nachfolgenden Kennzeichen in die Zeile übertragen werden. |
| **Beschreibung** | Beschreibender Text zum Einkaufscode; erleichtert dem Verkauf die richtige Auswahl in der Verkaufszeile. |
| **Direktlieferung** | Wenn gesetzt, dann liefert der Kreditor die Artikel direkt an den Debitor; die Buchung der Verkaufslieferung erfolgt automatisch nach der Einkaufslieferung. |
| **Spezialauftrag** | Wenn gesetzt, dann wird der bestellte Artikel zunächst ins eigene Unternehmen geliefert (z. B. zum Umpacken oder Weiterbearbeiten) und erst danach an den Debitor; die Verkaufslieferung wird manuell gebucht. |
| **Release Geschäft** | Wenn gesetzt, dann arbeitet die Zeile wie ein Spezialgeschäft, jedoch werden zusätzlich die „Lieferung an"-Felder vom Verkaufsauftrag auf die erzeugte Bestellung übertragen. Voraussetzung: Im Einkaufscode müssen **Spezialauftrag** und **Release Geschäft** gemeinsam gesetzt sein. |

**Danach – Lagerorte für das Release-Geschäft kennzeichnen**

**Einstieg:** Über **Suchen** die Liste **Lagerorte** öffnen und die betroffene **Lagerortkarte** aufrufen.

Je Lagerort legt der Administrator fest, für welche Geschäftsarten dieser Lagerort innerhalb des Direkt-/Spezialgeschäfts genutzt werden darf. Beim Erzeugen der Bestellung prüft das Programm den Lagerort der Verkaufszeile: Ist die Zeile ein Release Geschäft, muss der Lagerort das Kennzeichen **Release Geschäft** tragen, sonst wird der Vorgang abgebrochen.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Direktgeschäft** | Wenn gesetzt, dann darf dieser Lagerort in Verkaufszeilen mit Direktlieferung verwendet werden; ohne das Kennzeichen wird eine Direktlieferung über diesen Lagerort beim Bestellvorgang abgewiesen. |
| **Spezialauftrag** | Wenn gesetzt, dann darf dieser Lagerort in Verkaufszeilen mit Spezialauftrag verwendet werden; andernfalls bricht der Bestellvorgang für Spezialauftrags-Zeilen an diesem Lagerort ab. |
| **Release Geschäft** | Wenn gesetzt, dann darf dieser Lagerort für Release-Geschäft-Zeilen genutzt werden. Beim Setzen dieses Hakens wird automatisch auch **Spezialauftrag** aktiviert, da das Release-Geschäft auf dem Spezialgeschäft aufsetzt. |

**Schließlich – operative Auslösung**

Nach dem Freigeben des Verkaufsauftrags erzeugt der Anwender die Bestellung über die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** (siehe *Tägliche Arbeit am Verkaufsauftrag*). Ist zusätzlich in der **Fertigungsassistent Einrichtung** die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** aktiv, kann für Spezialauftrags-Zeilen zusätzlich der Fertigungsassistent genutzt werden (siehe nächster Abschnitt).

### Fertigungsauftrag für Spezialauftrags-Zeilen aktivieren

Diese zweite, eigenständige Freischaltung betrifft den **Fertigungsassistenten**. Sie wird vom Administrator in der **Fertigungsassistent Einrichtung** gesetzt und im Tagesgeschäft über die Verkaufszeile genutzt.

1. **Prozessvoraussetzung:** In der **Fertigungsassistent Einrichtung** die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** aktivieren. Wenn diese Option nicht gesetzt ist, dann blockiert der Fertigungsassistent jede Verkaufszeile, die als **Spezialauftrag** gekennzeichnet ist.
2. **FA-Status** über **FA-Status für Verkaufsaufträge** festlegen, damit die erzeugten Fertigungsaufträge den gewünschten Planungsstatus erhalten.
3. **Operativer Abschluss:** Der Anwender startet in der Verkaufszeile über **Zeile → Fertigungsassistent** den Assistenten und erzeugt mit **OK** den Fertigungsauftrag (siehe *Tägliche Arbeit am Verkaufsauftrag*).

Hinweis zur Abgrenzung: Für Zeilen mit **Release Geschäft** wird kein Fertigungsauftrag über die Freigabe erzeugt (dies unterdrückt die vorliegende App). Solche Zeilen laufen ausschließlich über den Bestellweg des Release-Geschäfts.

### Berechtigungen

Die App liefert den Berechtigungssatz **All permissions** (interner Zugriff, zuweisbar) mit. Er bestimmt die Berechtigungen für die Ausführung der Integrationslogik dieser App (des Codeunits, das Fertigungsassistent und Direkt-/Spezialgeschäft verbindet). Der Administrator weist diesen Berechtigungssatz den Anwendern zu, die im Verkaufsauftrag mit Release-Geschäft und Fertigungsassistent arbeiten. Für die eigentlichen Verkaufs-, Einkaufs- und Fertigungsvorgänge gelten zusätzlich die Standard-Berechtigungen von Business Central sowie der beiden Basismodule.

## Tägliche Arbeit am Verkaufsauftrag

Der zentrale Beleg für den Anwender ist der **Verkaufsauftrag**. Die betroffenen Felder und Aktionen werden von den beiden Basismodulen zur Verkaufszeile hinzugefügt; die vorliegende App steuert im Hintergrund deren Zusammenspiel.

**Steuernde Einrichtung:** Das Verhalten in diesem Kapitel wird durch die **Fertigungsassistent Einrichtung** (Assistenten-Pfad und Freigabe-Automatik), die **Einkaufscodes** (Kennzeichnung der Zeile als Direktlieferung/Spezialauftrag/Release Geschäft) und die **Lagerorte** (Zulässigkeit je Geschäftsart) bestimmt. Diese Bereiche sind im Kapitel *Einrichtung* beschrieben.

### Felder in der Verkaufszeile

Diese Felder erscheinen in den Zeilen des Verkaufsauftrags und stammen aus den beiden Basismodulen.

| Feld | Erläuterung |
|------|-------------|
| **FA erstellen** | Wenn gesetzt, dann ist für diese Zeile die Erzeugung eines Fertigungsauftrags vorgesehen; der Assistent bzw. die Freigabe-Automatik verarbeitet nur Zeilen mit gesetztem Haken. Die Vorbelegung steuert die Option **"FA erstellen" in der Verkaufszeile vorbelegen** in der Einrichtung. |
| **Kreditor-Nr.** | Wenn gesetzt, dann wird die daraus erzeugte Bestellung an diesen Kreditor gerichtet; bleibt das Feld leer, ermittelt das Programm den Kreditor über die Lagerhaltungsdaten des Artikels bzw. den Artikel selbst. Das Feld darf nur gefüllt werden, wenn **Selektiert für Bestellung** gesetzt ist. |
| **Selektiert für Bestellung** | Wenn gesetzt, dann wird diese Zeile beim Aufruf der Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** in die Bestellung übernommen; nur selektierte Zeilen werden verarbeitet. Der Haken lässt sich nur setzen, wenn die Zeile als **Spezialauftrag** oder **Direktlieferung** gekennzeichnet ist, andernfalls erscheint eine Fehlermeldung. |
| **Release Geschäft** | Zeigt an, dass diese Zeile ein Release-Geschäft ist. Das Feld wird automatisch über den gewählten **Einkaufscode** gesetzt und ist nicht direkt editierbar. Wenn gesetzt, dann werden bei der Bestellerzeugung die „Lieferung an"-Felder des Verkaufsauftrags in die Bestellung übernommen, und bei der Auftragsfreigabe wird für diese Zeile **kein** automatischer Fertigungsauftrag erzeugt. |

### Aktion: Fertigungsassistent

**Öffnen Sie über die Aktion Fertigungsassistent den Assistenten:** In der Verkaufszeile über **Zeile → Fertigungsassistent**. Der Assistent berechnet die zu fertigende Menge und erzeugt mit **OK** einen Fertigungsauftrag für die Zeile (Status gemäß **FA-Status für Verkaufsaufträge**). Voraussetzung ist das gesetzte Zeilenfeld **FA erstellen**. Ist die Zeile ein **Spezialauftrag**, muss zusätzlich in der **Fertigungsassistent Einrichtung** die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** aktiv sein; andernfalls wird der Aufruf für diese Zeile abgewiesen. Bricht der Anwender den Assistenten ab, wird der zuvor erzeugte simulierte Fertigungsauftrag wieder gelöscht.

### Aktion: Direkt-/Spezial-/Releasebestellung erzeugen

**Öffnen Sie über die Aktion Direkt-/Spezial-/Releasebestellung erzeugen den Bestellvorgang:** im freigegebenen Verkaufsauftrag über die Belegaktionen. Die Aktion verarbeitet alle Zeilen mit gesetztem **Selektiert für Bestellung** und erzeugt daraus je Kreditor eine **Bestellung**. Der genaue Ablauf ist im Abschnitt *Buchungs- und Bestellablauf* beschrieben.

### Aufruf der verknüpften Belege

Nach der Bestellerzeugung sind Verkaufsauftrag und Bestellung miteinander verknüpft:

- In der Bestellzeile öffnet der Anwender über den entsprechenden Aufruf den zugehörigen **Auftrag** (Verkaufsauftrag).
- In der Verkaufszeile öffnet der Anwender über die Aktion **Bestellung** die verknüpfte Einkaufsbestellung.

### Buchungs- und Bestellablauf

Der Ablauf für ein Release-Geschäft ergibt sich aus dem Programm und ist in folgender Reihenfolge einzuhalten:

1. Im **Verkaufsauftrag** die Zeile erfassen: Artikel, Menge und **Einkaufscode** mit Release Geschäft. Dadurch werden **Spezialauftrag** und **Release Geschäft** in der Zeile gesetzt.
2. **Selektiert für Bestellung** in der Zeile aktivieren; bei Bedarf **Kreditor-Nr.** setzen.
3. Den Verkaufsauftrag **freigeben** (Status **Freigegeben**). Die Bestellerzeugung setzt einen freigegebenen Auftrag voraus. Für Release-Geschäft-Zeilen wird bei der Freigabe kein automatischer Fertigungsauftrag erzeugt.
4. Die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** aufrufen. Das Programm prüft den Lagerort (bei Release Geschäft muss der Lagerort das Kennzeichen **Release Geschäft** tragen), ermittelt den Kreditor (Zeilen-**Kreditor-Nr.**, sonst Lagerhaltungsdaten, sonst Artikel) und erzeugt je Kreditor eine **Bestellung**. Bei einem Release-Geschäft werden die „Lieferung an"-Felder des Verkaufsauftrags in die Bestellung übernommen.
5. Die Abfrage **„Soll die Bestellung geöffnet werden?"** mit **Ja** bestätigen. Bei einer einzelnen Bestellung öffnet sich die **Bestellung**; bei mehreren Bestellungen öffnet sich die Liste der Bestellungen.
6. Den weiteren Standardprozess in Business Central fortsetzen: die **Bestellung freigeben** und die Einkaufslieferung buchen. Über die Zeilenaufrufe lassen sich jederzeit der verknüpfte **Auftrag** aus der Bestellung bzw. die **Bestellung** aus dem Verkaufsauftrag anzeigen.

Teilmengen sind zulässig: Es müssen nicht alle Zeilen gleichzeitig selektiert und bestellt werden. Der Anwender kann selektierte Zeilen bestellen und weitere Zeilen später ergänzen; bereits mit einer Bestellung verknüpfte Zeilen werden nicht erneut verarbeitet.

## Zusammenspiel der Module (Steuerlogik)

Dieses Kapitel beschreibt, was die App **m+m Production Order Assistant with Drop-/Special Shipment** selbst beiträgt. Sie greift an zwei Stellen des Fertigungsassistenten ein – beide betreffen ausschließlich Verkaufszeilen mit gesetztem **Release Geschäft**:

- **Bei der Auftragsfreigabe:** Wenn eine Verkaufszeile als **Release Geschäft** gekennzeichnet ist, dann unterdrückt die App die automatische Erzeugung eines Fertigungsauftrags. Diese Zeilen werden über die **Bestellung** des Release-Geschäfts abgewickelt, nicht über einen Fertigungsauftrag.
- **Beim direkten Aufruf des Fertigungsassistenten:** Wenn eine Verkaufszeile als **Release Geschäft** gekennzeichnet ist, dann übersteuert die App die Standardprüfungen des Assistenten in Abhängigkeit von der Einrichtung. Ist die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** nicht gesetzt, bleibt die Sperre gegen Direktlieferungs-Zeilen wirksam. So bleibt sichergestellt, dass Release-Geschäft-Zeilen nicht versehentlich zusätzlich einen Fertigungsauftrag erzeugen.

Für Anwender bedeutet dies: **Release-Geschäft-Zeilen** durchlaufen den Bestellweg (Aktion **Direkt-/Spezial-/Releasebestellung erzeugen**); reine **Spezialauftrags-Zeilen** ohne Release Geschäft können zusätzlich den **Fertigungsassistenten** nutzen, sofern die Einrichtung dies erlaubt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Release-Geschäft an eine Lieferadresse des Kunden

**Auslöser:** Ein Kunde bestellt telefonisch einen Artikel, der nicht auf Lager ist und über einen Lieferanten beschafft wird; die Ware soll an eine bestimmte Lieferadresse des Kunden gehen.

**Einstieg in BC:** Der Anwender im Verkauf öffnet über **Suchen** die **Verkaufsaufträge** und legt einen neuen **Verkaufsauftrag** für den Debitor an.

**Kernablauf:**

1. In der Verkaufszeile Artikel und Menge erfassen und den **Einkaufscode** mit Release Geschäft wählen. Dadurch werden **Spezialauftrag** und **Release Geschäft** in der Zeile gesetzt.
2. **Selektiert für Bestellung** aktivieren und – falls ein bestimmter Lieferant gewünscht ist – die **Kreditor-Nr.** setzen. Sicherstellen, dass der Lagerort der Zeile das Kennzeichen **Release Geschäft** trägt.
3. Den Verkaufsauftrag **freigeben** (Status **Freigegeben**). Für die Release-Geschäft-Zeile wird dabei bewusst kein Fertigungsauftrag erzeugt.
4. Die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** aufrufen. Die „Lieferung an"-Felder des Verkaufsauftrags werden in die erzeugte **Bestellung** übernommen.
5. Die Abfrage mit **Ja** bestätigen; die **Bestellung** öffnet sich.

**Abschluss:** Der Einkauf gibt die **Bestellung** frei und bucht die Einkaufslieferung im Standardprozess. Über die Zeilenaufrufe kann jederzeit zwischen **Auftrag** und **Bestellung** gewechselt werden.

### Anwendungsfall 2: Fertigungsauftrag für einen Spezialauftrag

**Auslöser:** Ein Kunde bestellt einen Artikel, der erst gefertigt bzw. bearbeitet werden muss und dazu zunächst ins eigene Unternehmen kommt (Spezialauftrag).

**Einstieg in BC:** Der Anwender öffnet den betreffenden **Verkaufsauftrag** und geht in die Verkaufszeile.

**Kernablauf:**

1. Voraussetzung prüfen: In der **Fertigungsassistent Einrichtung** ist **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** aktiviert.
2. In der Verkaufszeile den **Einkaufscode** mit **Spezialauftrag** wählen und das Feld **FA erstellen** setzen.
3. In der Zeile über **Zeile → Fertigungsassistent** den Assistenten öffnen.
4. Im Assistenten die Berechnung prüfen und mit **OK** den Fertigungsauftrag erzeugen (Status gemäß **FA-Status für Verkaufsaufträge**).

**Abschluss:** Der erzeugte Fertigungsauftrag erscheint mit dem eingerichteten Status in der Fertigungsplanung. Ist in der Einrichtung **Setze Bestätigt-Status nach Fertigungsassistentaufruf im VK-Beleg** aktiv, trägt der Auftrag zusätzlich den Prüfstatus „Bestätigt".

## FAQ und Troubleshooting

### 1. Warum wird bei der Freigabe eines Verkaufsauftrags mit Release-Geschäft-Zeile kein Fertigungsauftrag erzeugt?

Das ist das gewollte Verhalten dieser App. Für Zeilen mit **Release Geschäft** unterdrückt die App die automatische Fertigungsauftrags-Erstellung bei der Auftragsfreigabe. Diese Zeilen werden über die Aktion **Direkt-/Spezial-/Releasebestellung erzeugen** als Bestellung abgewickelt.

### 2. Warum blockiert der Fertigungsassistent meine Spezialauftrags-Zeile?

Der Assistent weist Zeilen mit **Spezialauftrag** ab, solange in der **Fertigungsassistent Einrichtung** die Option **Fertigungsauftrag für einen Verkaufsauftrag mit Spezialgeschäft erstellen** nicht aktiviert ist. Aktivieren Sie diese Option, um den Assistenten für solche Zeilen freizuschalten.

### 3. Warum lässt sich das Feld Selektiert für Bestellung nicht setzen?

Der Haken lässt sich nur setzen, wenn die Verkaufszeile als **Spezialauftrag** oder **Direktlieferung** gekennzeichnet ist. Wählen Sie zunächst einen passenden **Einkaufscode** in der Zeile; erst danach ist **Selektiert für Bestellung** zulässig.

### 4. Warum kann ich keine Kreditor-Nr. in der Verkaufszeile eintragen?

Die **Kreditor-Nr.** darf nur gefüllt werden, wenn **Selektiert für Bestellung** in der Zeile gesetzt ist. Setzen Sie zuerst den Selektions-Haken und wählen Sie dann den Kreditor.

### 5. Warum bricht die Bestellerzeugung mit einem Hinweis auf den Lagerort ab?

Beim Erzeugen der Bestellung prüft das Programm den Lagerort der Zeile. Für ein **Release Geschäft** muss der Lagerort auf der **Lagerortkarte** das Kennzeichen **Release Geschäft** tragen (analog **Spezialauftrag** bzw. **Direktgeschäft** für die übrigen Geschäftsarten). Ergänzen Sie das fehlende Kennzeichen am Lagerort.

### 6. Warum verlangt die Aktion Direkt-/Spezial-/Releasebestellung erzeugen einen freigegebenen Auftrag?

Die Bestellerzeugung setzt den Verkaufsauftragsstatus **Freigegeben** voraus. Geben Sie den Verkaufsauftrag frei, bevor Sie die Aktion aufrufen.

### 7. Welcher Kreditor wird verwendet, wenn ich keine Kreditor-Nr. in der Zeile hinterlege?

Das Programm ermittelt den Kreditor in dieser Reihenfolge: zuerst die **Kreditor-Nr.** der Zeile, dann die Lagerhaltungsdaten des Artikels für den Lagerort, danach der am Artikel hinterlegte Kreditor. Ist keiner davon gefüllt, meldet das Programm, dass für den Artikel kein Kreditor ausgewählt wurde und für die Zeile keine Bestellung erzeugt werden kann.

### 8. Was bedeutet der FA-Status in der Fertigungsassistent Einrichtung?

Der über **FA-Status für Verkaufsaufträge** bzw. **FA-Status für Verkaufsangebote** gewählte Wert legt den Status neu erzeugter Fertigungsaufträge fest: **Simuliert** (unverbindlicher Vorschlag), **Geplant** (eingeplant), **Fest geplant** (fest terminiert) oder **Freigegeben** (zur Fertigung freigegeben). Der Status **Fertig** ist nicht zulässig.

### 9. Warum öffnet sich nach der Bestellerzeugung eine Liste statt einer einzelnen Bestellung?

Werden aus den selektierten Zeilen mehrere Bestellungen (z. B. für verschiedene Kreditoren) erzeugt, öffnet das Programm nach der Bestätigung mit **Ja** die Liste dieser Bestellungen. Bei genau einer Bestellung öffnet sich diese direkt.

### 10. Wie finde ich zu einer Bestellung den passenden Verkaufsauftrag – und umgekehrt?

Aus der Bestellzeile öffnen Sie über den entsprechenden Aufruf den verknüpften **Auftrag**. Aus der Verkaufszeile öffnen Sie über die Aktion **Bestellung** die zugehörige Einkaufsbestellung. Beide Belege sind nach der Bestellerzeugung dauerhaft miteinander verknüpft.
