---
title: Anwenderhandbuch m+m Goods Receipt with Item Configurator
---

# Anwenderhandbuch m+m Goods Receipt with Item Configurator

Dieses Handbuch beschreibt die Erweiterung **m+m Goods Receipt with Item Configurator**
für Microsoft Dynamics 365 Business Central. Die Erweiterung ist eine **Brücke** zwischen
den Modulen **m+m Warenvereinnahmung** (Warenannahme) und **m+m Artikelkonfigurator**.
Sie ergänzt den Warenannahme-Beleg um die Aktion **Artikelkonfigurator**, mit der ein
Anwender direkt aus dem Beleg heraus einen konfigurierten Artikel anlegt und automatisch
eine passende Belegzeile samt Komponenten in die Warenannahme einfügt.

## 1. Einleitung

### Zweck des Moduls

In vielen Wareneingangs- und Veredelungsprozessen steht der genaue, kundenspezifisch
konfigurierte Artikel erst beim Wareneingang fest. Ohne Unterstützung müsste der Anwender
den konfigurierten Artikel in einem getrennten Schritt im **Artikelkonfigurator** anlegen,
die entstandene Artikelnummer notieren und anschließend von Hand in die **Warenannahme**
übertragen.

Die Erweiterung schließt genau diese Lücke: Über eine einzige Aktion auf dem
Warenannahme-Beleg startet der Anwender den **Artikelkonfigurator**, legt dort das
**Fertigteil** an und erhält beim Zurückkehren in die Warenannahme automatisch eine
Belegzeile mit dem neuen Fertigteil sowie dessen **Komponenten**. Die manuelle Übertragung
entfällt, und Artikel und Beleg bleiben konsistent.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender** in der Warenannahme bzw. im Wareneingang,
die täglich Warenannahme-Belege erfassen und dabei konfigurierte Artikel benötigen.
Sekundär richtet sich das Kapitel **Voraussetzungen und Einrichtung** an
**Administratoren** und **Key-User**, die die beteiligten Module installieren und den
**Artikelkonfigurator** einmalig einrichten.

### Kurzer Prozessüberblick

1. Der Anwender öffnet einen **Warenannahme**-Beleg mit dem Status **Offen**.
2. Er startet die Aktion **Artikelkonfigurator**.
3. Im **Artikelkonfigurator** wählt er einen **Vorlagencode** und einen
   **Arbeitsplanvorlagencode** und führt die Aktion **Artikel und Arbeitsgänge erstellen**
   aus. Dabei entstehen das **Fertigteil** und das zugehörige **Beistellteil**.
4. Nach dem Schließen des Konfigurators fügt die Erweiterung in der **Warenannahme**
   automatisch eine Zeile mit dem neuen **Fertigteil** und dessen **Komponenten** ein.

Die eigentliche Weiterverarbeitung des Warenannahme-Belegs (Erstellen von
Verkaufs-, Fertigungs- oder Montageaufträgen, Buchen) übernimmt weiterhin das
Basismodul **m+m Warenvereinnahmung**; diese Erweiterung endet mit der eingefügten Zeile.

## 2. Schnellstart für Anwender

Der schnellste Weg von einem offenen Beleg zum konfigurierten Artikel:

1. **Einrichtung sicherstellen (einmalig, durch den Administrator):** Die Module
   **m+m Warenvereinnahmung** und **m+m Artikelkonfigurator** sind installiert, und die
   **Artikelkonfigurator Einrichtung** ist gepflegt (siehe Kapitel 3).
2. Öffnen Sie den gewünschten **Warenannahme**-Beleg. Der Beleg muss den Status
   **Offen** besitzen.
3. Wählen Sie im Menüband die Aktion **Artikelkonfigurator**.
4. Wählen Sie im **Artikelkonfigurator** den **Vorlagencode** und den
   **Arbeitsplanvorlagencode** aus.
5. Führen Sie die Aktion **Artikel und Arbeitsgänge erstellen** aus. Das **Fertigteil**
   und das **Beistellteil** werden angelegt; passen Sie bei Bedarf die Arbeitsplan- und
   Komponentenzeilen an.
6. Schließen Sie den **Artikelkonfigurator** mit **OK**. In der **Warenannahme** erscheint
   nun automatisch eine Zeile mit dem **Fertigteil** sowie den zugehörigen
   **Komponenten**.

> Ist der Beleg nicht **Offen**, bricht Business Central die Aktion mit einer
> Feldprüfung auf das Feld **Status** ab. Setzen Sie den Beleg zunächst wieder auf
> **Offen**, bevor Sie den **Artikelkonfigurator** starten.

## 3. Voraussetzungen und Einrichtung

Diese Erweiterung bringt selbst **keine eigene Einrichtungsseite** mit. Sie setzt jedoch
auf zwei vorgelagerte Module auf und benötigt deren korrekte Einrichtung. Die Reihenfolge
ergibt sich aus den Abhängigkeiten der App.

### 3.1 Abhängige Module und Installationsreihenfolge

Wer richtet dies ein: der **Administrator**, einmalig vor der ersten Nutzung.

Die Erweiterung ist von den folgenden Modulen abhängig und kann nur zusammen mit ihnen
genutzt werden:

| Modul | Erläuterung |
|-------|-------------|
| m+m Cloud Base | Basismodul; stellt die Lizenzprüfung bereit, die diese Erweiterung beim Anmelden aufruft. Wenn es fehlt, lässt sich die Erweiterung nicht ordnungsgemäß betreiben. |
| m+m Warenvereinnahmung | Stellt den **Warenannahme**-Beleg bereit, an den die Aktion **Artikelkonfigurator** angehängt wird, sowie die Zeilen- und Komponentenstruktur, in die die Erweiterung schreibt. |
| m+m Artikelkonfigurator | Stellt die Seite **Artikelkonfigurator** und deren Einrichtung bereit; hier entstehen **Fertigteil**, **Beistellteil**, Stückliste und Arbeitsplan. |

**Ablauf:** Zuerst installiert der Administrator die drei genannten Module (bzw. stellt
sicher, dass sie installiert sind), danach diese Brückenerweiterung. Erst danach steht die
Aktion **Artikelkonfigurator** auf dem Warenannahme-Beleg zur Verfügung.

### 3.2 Artikelkonfigurator einrichten

Wer richtet dies ein: der **Administrator** oder **Key-User**, einmalig, bevor der erste
konfigurierte Artikel aus einer Warenannahme heraus erstellt wird. Diese Einrichtung wird
später im Kapitel 5 (Ablauf im Detail) beim Ausführen der Aktion **Artikelkonfigurator**
wirksam.

**Einstieg:** Öffnen Sie die **Artikelkonfigurator Einrichtung** über **Suchen**, indem
Sie den Suchbegriff *Artikelkonfigurator Einrichtung* eingeben und den entsprechenden Link
wählen. (Diese Seite gehört zum Modul **m+m Artikelkonfigurator** und ist eine
unternehmensweite Einrichtung.)

Für das Zusammenspiel mit der Warenannahme sind vor allem die folgenden Felder relevant:

| Einrichtung | Erläuterung |
|-------------|-------------|
| Präfix Fertigteil | Wenn hier eine Zeichenkette hinterlegt ist (z. B. „FT"), dann wird sie jeder Artikelnummer eines **Fertigteils** vorangestellt; der Anwender erkennt an dieser Kennung, dass es sich um das konfigurierte Fertigteil handelt, das die Erweiterung in die Warenannahme-Zeile einfügt. |
| Fertigartikel-Nummernserie | Wenn hier eine Nummernserie hinterlegt ist, dann vergibt der **Artikelkonfigurator** die Artikelnummer des **Fertigteils** automatisch aus dieser Serie; ohne eingerichtete Serie kann kein Fertigteil erzeugt und damit auch keine Zeile in die Warenannahme eingefügt werden. |

> Über die genannten Felder hinaus besitzt die **Artikelkonfigurator Einrichtung** weitere
> Felder (z. B. Konfigurationsvorlage für Beistellteile, Standardkomponentenmenge). Diese
> gehören zum Modul **m+m Artikelkonfigurator** und werden dort ausführlich beschrieben;
> für den Brückenprozess genügen die beiden oben genannten Pflichteinstellungen.

**Voraussetzung/Abhängigkeit:** Es lassen sich im Konfigurator nur Vorlagen auswählen, die
für den Artikelkonfigurator freigegeben sind. Ist keine passende **Vorlage** und kein
**Arbeitsplanvorlagencode** vorhanden, kann der Anwender in Kapitel 5 kein Fertigteil
anlegen.

### 3.3 Berechtigungen

Wer richtet dies ein: der **Administrator**.

Die Erweiterung liefert den Berechtigungssatz **All permissions**
(`MuM GRIC Permission`). Er legt fest, welche Objekte ein Anwender ausführen darf, und
umfasst die Ausführungsberechtigung für die zentrale Verarbeitungslogik der Erweiterung
(Codeunit **MuM GRIC Item Config. Mgt.**). Weisen Sie diesen Berechtigungssatz den
Anwendern zu, die die Aktion **Artikelkonfigurator** in der Warenannahme nutzen sollen.
Die Berechtigungen für den Warenannahme-Beleg selbst und für den Artikelkonfigurator
werden über die Berechtigungssätze der jeweiligen Basismodule vergeben.

## 4. Die Aktion „Artikelkonfigurator" in der Warenannahme

Die einzige Bedienoberfläche, die diese Erweiterung selbst hinzufügt, ist die Aktion
**Artikelkonfigurator** auf dem Beleg **Warenannahme**. Damit der Anwender diese Aktion
sinnvoll einsetzen kann, werden nachfolgend zunächst die für den Brückenprozess relevanten
Felder des Belegs und anschließend die Aktion selbst beschrieben.

**Steuernde Einrichtung:** Ob und wie die eingefügte Zeile weiterverarbeitet wird, steuern
die Verarbeitungskennzeichen des Belegs (**Komponenten buchen**, **Verkaufsauftrag
erstellen**, **Fertigungsauftrag erstellen**, **Montageauftrag erstellen**). Deren
Standardwerte legt der Administrator in der **Warenvereinnahmung Einrichtung** des
Basismoduls fest; auf dem einzelnen Beleg kann der Anwender sie übersteuern (siehe
Kapitel 5).

### 4.1 Einstieg in den Beleg

**Einstieg:** Öffnen Sie die Liste der Warenannahme-Belege des Moduls
**m+m Warenvereinnahmung** und wählen Sie den gewünschten Beleg, oder legen Sie einen neuen
Beleg an. Achten Sie darauf, dass der Beleg den Status **Offen** besitzt.

### 4.2 Kopffelder des Belegs (für den Brückenprozess relevant)

Der Warenannahme-Beleg zeigt eine Reihe von Kopffeldern. Die folgenden sind für das
Zusammenspiel mit dem **Artikelkonfigurator** von Bedeutung:

| Feld | Erläuterung |
|------|-------------|
| Nummer | Eindeutige Belegnummer der Warenannahme. Wenn sie über die Nummernserie vergeben wird, dann ordnet Business Central den Beleg eindeutig zu; die eingefügte Fertigteil-Zeile referenziert genau diese Nummer. |
| Status | Steuert, ob der Beleg bearbeitet werden darf (siehe Werteliste unten). Nur bei **Offen** lässt sich die Aktion **Artikelkonfigurator** ausführen. |
| Eingangsdatum | Wenn gesetzt, dann dokumentiert es den tatsächlichen Wareneingangstag des Belegs; es steuert die zeitliche Einordnung der Warenannahme. |
| Belegdatum | Wenn gesetzt, dann hält es das Belegdatum fest, das für Auswertung und Nachverfolgung der Warenannahme herangezogen wird. |
| Komponenten buchen | Wenn aktiviert, dann werden für diese Warenannahme die Komponenten der eingefügten Fertigteil-Zeile mitgebucht; ohne das Kennzeichen bleiben die Komponenten unbebucht und dienen nur der Dokumentation. |
| Verkaufsauftrag erstellen | Wenn aktiviert, dann erzeugt das Basismodul aus dieser Warenannahme einen Verkaufsauftrag für den erfassten Kunden; ist es nicht gesetzt, entsteht kein Verkaufsbeleg. |
| Fertigungsauftrag erstellen | Wenn aktiviert, dann erzeugt das Basismodul aus der Fertigteil-Zeile einen Fertigungsauftrag zur Produktion des konfigurierten Artikels; ohne das Kennzeichen wird keine Fertigung angestoßen. |
| Montageauftrag erstellen | Wenn aktiviert, dann erzeugt das Basismodul aus der Zeile einen Montageauftrag; ohne das Kennzeichen unterbleibt die Montage. |
| Fertigungsauftragsart | Wenn gesetzt, dann verwendet das Basismodul beim Erstellen des Fertigungsauftrags genau diese Auftragsart; sie bestimmt Nummernkreis und Verhalten des erzeugten Fertigungsauftrags. |
| Verk. an Deb.-Nr. | Wenn gesetzt, dann ordnet es die Warenannahme einem Debitor zu; dieser Debitor wird bei aktivem **Verkaufsauftrag erstellen** in den erzeugten Verkaufsauftrag übernommen. |
| Verk. an Name | Zeigt den Namen des zugeordneten Debitors an; dient der Kontrolle des ausgewählten Kunden. |
| Wareneingangslagerortcode | Wenn gesetzt, dann werden die vereinnahmten Mengen auf diesen Lagerort gebucht; er bestimmt, wo die Ware zugeht. |
| Sperrlagerortcode | Wenn gesetzt, dann wird gesperrt zu vereinnahmende Ware auf diesen Sperrlagerort gebucht; er trennt freigegebene von gesperrter Ware. |
| Externe Lieferscheinnummer | Wenn gesetzt, dann hält es die Lieferscheinnummer des Lieferanten fest und ermöglicht die spätere Zuordnung des Wareneingangs zum externen Beleg. |
| Externe Bestellnummer | Wenn gesetzt, dann verweist es auf die Bestellnummer im Nummernsystem des Debitors und erleichtert die Kommunikation mit dem Kunden. |
| Gewünschtes Lieferdatum | Wenn gesetzt, dann dokumentiert es den vom Debitor gewünschten Liefertermin und fließt in einen erzeugten Verkaufsauftrag ein. |

Die weiteren Kopfbereiche des Belegs — **Lief. an**-Adresse (Lieferadresse und
Versandart) sowie die Bereiche **Beleginformation** (Anlage- und Änderungsdaten) — steuern
den Versand bzw. dienen der Protokollierung. Sie werden durch die Aktion
**Artikelkonfigurator** nicht verändert und gehören zum Standardumfang des Basismoduls
**m+m Warenvereinnahmung**.

#### Werteliste zum Feld „Status"

Das Feld **Status** steuert, welche Aktionen auf dem Beleg zulässig sind. Für die
Erweiterung ist entscheidend, dass die Aktion **Artikelkonfigurator** nur bei **Offen**
erlaubt ist:

- **Offen:** Der Beleg ist in Bearbeitung und darf geändert werden. Nur in diesem Status
  lässt sich die Aktion **Artikelkonfigurator** ausführen und eine Fertigteil-Zeile
  einfügen.
- **In Bearbeitung:** Der Beleg wird gerade verarbeitet. Die Aktion
  **Artikelkonfigurator** ist nicht möglich; setzen Sie den Beleg zunächst wieder auf
  **Offen**.
- **Freigegeben:** Der Beleg ist freigegeben und für die weitere Verarbeitung bzw. Buchung
  vorgesehen. Änderungen über den **Artikelkonfigurator** sind nicht mehr möglich.

> Die drei genannten Werte sind die über die Übersetzungsdateien bestätigten
> Statusausprägungen. Das Basismodul verwendet intern weitere Zwischenzustände für die
> Verarbeitungssteuerung; für die Nutzung der Aktion **Artikelkonfigurator** ist allein
> maßgeblich, dass der Beleg **Offen** ist.

### 4.3 Die Aktion „Artikelkonfigurator"

Die Aktion **Artikelkonfigurator** ist im Menüband des Belegs im Verarbeitungsbereich als
erste Aktion angeordnet.

**Öffnen Sie über die Aktion Artikelkonfigurator** die gleichnamige Konfiguratormaske.
Beim Aufruf prüft Business Central zunächst, ob der Beleg den Status **Offen** besitzt.

- Ist der Beleg **Offen**, dann öffnet sich der **Artikelkonfigurator** als modales
  Fenster (siehe Kapitel 5).
- Ist der Beleg nicht **Offen**, dann bricht Business Central mit einer Feldprüfung auf
  **Status** ab; es wird kein Konfigurator geöffnet und keine Zeile eingefügt.

## 5. Ablauf im Detail

Dieses Kapitel beschreibt den vollständigen Ablauf, den die Aktion **Artikelkonfigurator**
auslöst — von der Konfiguratormaske bis zur eingefügten Belegzeile.

### 5.1 Der Artikelkonfigurator

Nach dem Start der Aktion öffnet sich die Maske **Artikelkonfigurator**. Hier wählt der
Anwender die Vorlagen für den zu erzeugenden Artikel:

| Feld | Erläuterung |
|------|-------------|
| Vorlage | Zeigt die zugrunde liegende Artikelvorlage an; sie bestimmt, welche Stammdatenwerte in das erzeugte **Fertigteil** übernommen werden. |
| Vorlagencode | Wenn ausgewählt, dann wird diese Konfigurationsvorlage zur Anlage der Stammdaten des **Fertigteils** verwendet; die in der Vorlage vorbelegten Werte gehen in den neuen Artikel über. |
| Arbeitsplanvorlagencode | Wenn ausgewählt, dann dient der angegebene bestehende Arbeitsplan als Vorlage für den zu erzeugenden Arbeitsplan des Fertigteils; ohne Auswahl kann kein Arbeitsplan angelegt werden. |

Anschließend stehen folgende Aktionen zur Verfügung:

- **Artikel und Arbeitsgänge erstellen:** Wenn ausgeführt, dann werden auf Basis der
  ausgewählten Vorlagen das **Fertigteil** und das zugehörige **Beistellteil** angelegt,
  eine Komponentenzeile erstellt und die Arbeitsplanzeilen zur Bearbeitung angezeigt. Erst
  danach besitzt der Beleg einen Artikel, den die Erweiterung übernehmen kann.
- **Nicht abgeschlossene Konfiguration:** Wenn ausgeführt, dann wird die Konfiguration als
  nicht abgeschlossen gekennzeichnet; der Artikel bleibt in Bearbeitung und kann später
  vervollständigt werden.

Der Bereich der Komponenten- und Arbeitsplanzeilen gehört zum Modul
**m+m Artikelkonfigurator** und ist dort ausführlich beschrieben. Für den Brückenprozess
genügt es, das **Fertigteil** vollständig anzulegen und die Maske mit **OK** zu schließen.

### 5.2 Rückübernahme in die Warenannahme

Sobald der Anwender den **Artikelkonfigurator** schließt, ermittelt die Erweiterung das
angelegte **Fertigteil** und übernimmt es in den Warenannahme-Beleg. Bei Artikeln, die als
letzte Stufe eines mehrstufigen Arbeitsplans (ohne Folgearbeitsgang) angelegt wurden, wird
das erzeugte Fertigteil zusätzlich über einen internen Zwischenspeicher sicher übernommen,
sodass immer die zuletzt erzeugte Artikelnummer verwendet wird.

Die Erweiterung fügt daraufhin **automatisch** eine neue Zeile in die Warenannahme ein:

- Die Zeilennummer wird fortlaufend vergeben (jeweils um 10.000 erhöht gegenüber der
  letzten Zeile des Belegs).
- Das Feld **Artikelnr.** der Zeile wird mit dem neuen **Fertigteil** gefüllt.
- Zu dieser Zeile werden anschließend die zugehörigen **Komponenten** erzeugt.

Wird der Konfigurator ohne angelegtes Fertigteil geschlossen (leere Fertigteilnummer) oder
existiert der Artikel nicht, dann fügt die Erweiterung **keine** Zeile ein; der Beleg
bleibt unverändert.

### 5.3 Zeilenfelder der eingefügten Fertigteil-Zeile

Die eingefügte Zeile erscheint im Zeilenbereich der Warenannahme. Für die Kontrolle durch
den Anwender sind vor allem folgende Felder relevant:

| Feld | Erläuterung |
|------|-------------|
| Komponenten sperren | Wenn aktiviert, dann werden die zu diesem Fertigteil gehörenden Komponenten gesperrt und nicht zur Buchung freigegeben; ohne das Kennzeichen stehen die Komponenten zur Verarbeitung bereit. |
| Artikelnr. | Enthält die Nummer des angelegten **Fertigteils**; über sie ist die Warenannahme-Zeile eindeutig dem konfigurierten Artikel zugeordnet. |
| Beschreibung | Zeigt die Beschreibung des Fertigteils an; sie stammt aus den Stammdaten des Artikels und dient der Wiedererkennung im Beleg. |
| Menge | Wenn erfasst, dann legt sie fest, wie viele Einheiten des Fertigteils vereinnahmt bzw. weiterverarbeitet werden; auf dieser Menge basieren Folgeaufträge und Komponentenbedarfe. |
| Einheitencode | Wenn gesetzt, dann bestimmt er, in welcher Einheit die Menge geführt wird (z. B. Stück); er steuert die Mengenumrechnung in Folgebelegen. |
| Variantencode | Wenn gesetzt, dann konkretisiert er die Artikelvariante der Zeile; die Variante wird in Folgeaufträge übernommen. |
| Lagerortcode | Wenn gesetzt, dann bestimmt er den Lagerort, auf den die Zeile vereinnahmt wird; er steuert den Warenzugang der Zeile. |

Weitere Zeilenfelder (Zuordnung/Losgrößen-Angaben, Rundungspräzision, Arbeitsplannummer
der Zeile sowie die Herkunftsangaben zum Ursprungsbeleg) werden vom Basismodul für die
weitere Verarbeitung gepflegt und sind für die vom Konfigurator eingefügte Zeile in der
Regel nicht manuell zu erfassen.

### 5.4 Komponenten der Fertigteil-Zeile

Zu jeder eingefügten Fertigteil-Zeile erzeugt die Erweiterung die zugehörigen
**Komponenten**. Diese zeigt der Beleg im Komponentenbereich an:

| Feld | Erläuterung |
|------|-------------|
| Artikelnr. | Enthält die Nummer der Komponente; sie bezeichnet das Material, das in das Fertigteil eingeht. |
| Beschreibung | Zeigt die Beschreibung der Komponente an und dient der Kontrolle des richtigen Materials. |
| Komponentenmenge | Wenn gesetzt, dann gibt sie an, wie viele Einheiten der Komponente je Einheit Fertigteil benötigt werden; sie bestimmt den mengenabhängigen Materialbedarf. |
| Menge | Wenn gesetzt, dann zeigt sie die Gesamtmenge der Komponente für die Zeilenmenge des Fertigteils an; sie steuert den tatsächlichen Verbrauch. |
| Erwartete Menge | Wenn gesetzt, dann zeigt sie die erwartete Komponentenmenge an und dient dem Abgleich zwischen Planung und tatsächlichem Zugang. |
| Einheitencode | Wenn gesetzt, dann bestimmt er die Mengeneinheit der Komponente; er steuert die Mengenumrechnung. |
| Lagerortcode | Wenn gesetzt, dann bestimmt er den Lagerort, aus dem bzw. auf den die Komponente gebucht wird. |
| Lagerplatzcode | Wenn gesetzt, dann konkretisiert er den Lagerplatz innerhalb des Lagerorts für die Komponente. |
| Beistellteil | Wenn aktiviert, dann ist die Komponente als vom Kunden beigestelltes Teil gekennzeichnet; sie wird nicht als eigener Einkauf, sondern als Beistellung behandelt. |

Weitere, standardmäßig ausgeblendete Komponentenfelder (Geometrieangaben wie Länge,
Breite, Gewicht, Tiefe sowie die Berechnungsformel und die zweite Beschreibung) dienen
Sonderberechnungen des Basismoduls und werden dem Anwender im Standard nicht angezeigt.

### 5.5 Zusammenfassender Ablauf (Buchungs- bzw. Verarbeitungskette)

Diese Erweiterung führt **keine eigene Buchung oder Freigabe** durch. Ihr Beitrag endet mit
der eingefügten Zeile; die weitere Verarbeitung übernimmt das Basismodul. Der vollständige
Ablauf:

1. Beleg **Warenannahme** mit Status **Offen** auswählen.
2. Aktion **Artikelkonfigurator** ausführen (öffnet die modale Maske).
3. **Vorlagencode** und **Arbeitsplanvorlagencode** wählen und **Artikel und Arbeitsgänge
   erstellen** ausführen; mit **OK** schließen.
4. Die Erweiterung fügt automatisch die **Fertigteil**-Zeile samt **Komponenten** ein.
5. Die weitere Verarbeitung (Verkaufs-, Fertigungs- oder Montageauftrag erzeugen,
   Komponenten buchen, Beleg freigeben und buchen) erfolgt über die Standardfunktionen des
   Moduls **m+m Warenvereinnahmung**.

## 6. Systemverhalten und Ereignisse

Neben der sichtbaren Aktion enthält die Erweiterung Hintergrundlogik, die der Anwender
nicht direkt bedient, deren Wirkung er aber kennt:

- **Übernahme des Fertigteils bei mehrstufigen Arbeitsplänen:** Wird beim Anlegen im
  Artikelkonfigurator ein Halbfertigartikel als letzte Stufe (ohne Folgearbeitsgang)
  erzeugt, dann merkt sich die Erweiterung dessen Artikelnummer und verwendet genau diese
  beim Einfügen der Zeile. So wird immer das zuletzt erzeugte Fertigteil in die
  Warenannahme übernommen.
- **Lizenzprüfung beim Anmelden:** Beim Anmelden am Mandanten prüft die Erweiterung über
  das Modul **m+m Cloud Base** die Lizenz der Erweiterung. Damit wird sichergestellt, dass
  die Aktion **Artikelkonfigurator** nur bei gültiger Lizenz zur Verfügung steht.

## 7. FAQ und Troubleshooting

### 1. Warum ist die Aktion „Artikelkonfigurator" ausgegraut oder wirkungslos?

Die Aktion ist nur bei Belegstatus **Offen** ausführbar. Steht der Beleg auf **In
Bearbeitung** oder **Freigegeben**, bricht Business Central mit einer Feldprüfung auf
**Status** ab. Setzen Sie den Beleg wieder auf **Offen**.

### 2. Warum wurde nach dem Konfigurator keine Zeile eingefügt?

Die Erweiterung fügt nur dann eine Zeile ein, wenn im **Artikelkonfigurator** ein
**Fertigteil** tatsächlich angelegt wurde. Haben Sie die Maske ohne die Aktion **Artikel
und Arbeitsgänge erstellen** geschlossen, bleibt die Fertigteilnummer leer und es entsteht
keine Zeile.

### 3. Warum meldet das System, dass das Fertigteil nicht existiert?

Vor dem Einfügen prüft die Erweiterung, ob der Artikel zur ermittelten Fertigteilnummer
existiert. Wurde der Artikel im Konfigurator nicht vollständig angelegt oder zwischenzeitig
gelöscht, unterbleibt das Einfügen. Legen Sie das Fertigteil erneut über den Konfigurator
an.

### 4. Warum bekommt das Fertigteil keine Nummer?

Die Artikelnummer des Fertigteils wird aus der **Fertigartikel-Nummernserie** der
**Artikelkonfigurator Einrichtung** vergeben. Ist dort keine Nummernserie hinterlegt, kann
kein Fertigteil erzeugt werden. Pflegen Sie die Einrichtung (Kapitel 3.2).

### 5. Warum kann ich im Konfigurator keine Vorlage auswählen?

Es lassen sich nur Vorlagen wählen, die für den Artikelkonfigurator freigegeben sind.
Fehlen passende **Vorlagencode**- oder **Arbeitsplanvorlagencode**-Einträge, wenden Sie
sich an den Administrator; die Vorlagen werden im Modul **m+m Artikelkonfigurator**
gepflegt.

### 6. Warum werden die Komponenten meiner Zeile nicht gebucht?

Ob Komponenten mitgebucht werden, steuert das Kopf-Kennzeichen **Komponenten buchen**. Ist
es nicht aktiviert, dienen die Komponenten nur der Dokumentation. Aktivieren Sie das
Kennzeichen, wenn die Komponenten gebucht werden sollen.

### 7. Woran erkenne ich das erzeugte Fertigteil in der Zeile?

Am Feld **Artikelnr.** der eingefügten Zeile und am **Präfix Fertigteil** (z. B. „FT"),
das der Nummer vorangestellt ist. Über dieses Präfix unterscheiden Sie das Fertigteil vom
zugehörigen **Beistellteil**.

### 8. Was ist der Unterschied zwischen Fertigteil und Beistellteil?

Das **Fertigteil** ist der konfigurierte Endartikel, der in die Warenannahme-Zeile
eingefügt wird. Das **Beistellteil** ist das zugehörige beigestellte Teil (Rohteil) in der
Stückliste des Fertigteils. Beide werden vom Konfigurator gemeinsam angelegt.

### 9. Warum muss ich mich neu anmelden, damit die Erweiterung funktioniert?

Beim Anmelden prüft die Erweiterung die Lizenz über **m+m Cloud Base**. Ist die Lizenz erst
kürzlich aktiviert worden, kann eine erneute Anmeldung erforderlich sein, damit die Prüfung
greift und die Aktion verfügbar ist.

### 10. Bucht diese Erweiterung den Warenannahme-Beleg?

Nein. Die Erweiterung legt ausschließlich die Fertigteil-Zeile und deren Komponenten an.
Das Erstellen von Folgeaufträgen, das Buchen der Komponenten sowie das Freigeben und Buchen
des Belegs erfolgen über die Standardfunktionen des Moduls **m+m Warenvereinnahmung**.

## 8. Typische Anwendungsfälle

### 8.1 Konfigurierter Artikel zu einem Kundenauftrag beim Wareneingang

**Auslöser:** Für einen Kundenauftrag wird ein kundenspezifisch konfiguriertes Teil
erwartet. Beim Wareneingang steht die konkrete Ausprägung des Artikels fest und soll direkt
angelegt werden.

**Einstieg in BC:** Der Anwender öffnet aus der Warenannahme-Liste den betreffenden
**Warenannahme**-Beleg (Status **Offen**) und erfasst im Kopf den Debitor über
**Verk. an Deb.-Nr.** sowie die relevanten Kopfdaten (z. B. **Eingangsdatum**).

**Kernablauf:**
1. Aktion **Artikelkonfigurator** ausführen.
2. **Vorlagencode** und **Arbeitsplanvorlagencode** gemäß Kundenspezifikation wählen.
3. **Artikel und Arbeitsgänge erstellen**; **Fertigteil** und **Beistellteil** entstehen.
4. Maske mit **OK** schließen — die Erweiterung fügt die Zeile mit **Artikelnr.**
   (Fertigteil) und die **Komponenten** ein.
5. Bei Bedarf **Menge** und **Einheitencode** der Zeile anpassen.

**Abschluss:** Ist am Kopf **Verkaufsauftrag erstellen** aktiviert, erzeugt das Basismodul
im weiteren Verlauf den Verkaufsauftrag für den erfassten Debitor. Buchung und Freigabe des
Belegs erfolgen über die Standardfunktionen der Warenvereinnahmung.

### 8.2 Ad-hoc-Konfiguration auf einem offenen Warenannahme-Beleg

**Auslöser:** Während der Erfassung eines offenen Warenannahme-Belegs stellt der Anwender
fest, dass ein weiteres konfiguriertes Teil benötigt wird, das noch nicht als Artikel
existiert.

**Einstieg in BC:** Der Anwender befindet sich bereits auf dem offenen
**Warenannahme**-Beleg.

**Kernablauf:**
1. Aktion **Artikelkonfigurator** direkt aus dem Beleg starten.
2. Vorlagen wählen und **Artikel und Arbeitsgänge erstellen** ausführen.
3. Maske schließen — die Erweiterung ergänzt eine weitere **Fertigteil**-Zeile am Ende des
   Belegs (fortlaufende Zeilennummer) samt **Komponenten**.

**Abschluss:** Der Anwender prüft die neue Zeile und deren Komponenten (Feld **Beistellteil**
bei beigestellten Teilen) und setzt die Erfassung des Belegs fort. Eine gesonderte Buchung
durch die Erweiterung findet nicht statt.
