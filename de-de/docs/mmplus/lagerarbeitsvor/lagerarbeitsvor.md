---
title: Anwenderhandbuch m+m Warehouse Job Overview
---

# Anwenderhandbuch m+m Warehouse Job Overview

## Einleitung

Der **Lagerarbeitsvorrat** bündelt alle offenen Lageraufträge eines Unternehmens in einer einzigen Liste. Immer wenn im Standard von Microsoft Dynamics 365 Business Central ein **Wareneingang**, ein **Warenausgang**, eine **Lageraktivität** (Kommissionierung oder Einlagerung) oder eine **Umlagerung** über ein Artikel-Umlagerungsbuch.-Blatt entsteht, legt das Modul automatisch eine Zeile im Lagerarbeitsvorrat an. Der Anwender sieht dadurch an einer Stelle, welche Lagerbelege noch offen sind, welche Restmengen bestehen und in welchem Bearbeitungsstatus sich jede Zeile befindet. Das Buchen der Herkunftsbelege wird aus dieser Liste heraus angestoßen und vereinfacht.

**Zielgruppe:** Primär richtet sich das Modul an **operative Lagermitarbeiter**, die täglich kommissionieren, einlagern, Wareneingänge und Warenausgänge bearbeiten sowie Umlagerungen buchen. Diese Anwender arbeiten überwiegend auf der Seite **Lagerarbeitsvorrat** und den daraus geöffneten Zeilen. Sekundär betrifft das Modul **Administratoren und Lagerleiter**, die einmalig die **Lagerarbeitsvorratseinrichtung**, die **Lagergruppen**, die **Lagerkapazität** und die **Lagermaske** konfigurieren.

**Prozessüberblick:** Herkunftsbeleg entsteht (Verkaufsauftrag → Warenausgang, Einkaufsbestellung → Wareneingang, Lageraktivität, Artikel-Umlagerungsbuch.-Blatt) ⇒ Zeile im **Lagerarbeitsvorrat** wird automatisch erzeugt ⇒ Anwender filtert die Liste (Lagergruppe, Filtervorlage) ⇒ Zeile auswählen ⇒ **Starten** ⇒ **Teilbeenden** bzw. **Beenden** ⇒ Herkunftsbeleg wird gebucht ⇒ Kontrolle über die **Ereignishistorie**.

## Schnellstart für Anwender

Der schnellste Weg vom offenen Lagerbeleg bis zur Buchung. Die Einrichtung (Schritte A–C) ist Voraussetzung und wird in der Regel einmalig vom Administrator erledigt; die tägliche Arbeit beginnt bei Schritt 1.

**Voraussetzung (Administrator, einmalig):**

- **A.** Öffnen Sie über **Suchen** die **Lagerarbeitsvorratseinrichtung** und legen Sie die globalen Grundwerte fest (siehe Abschnitt *Einrichtung*).
- **B.** Pflegen Sie unter **Lagergruppen** mindestens eine **Lagergruppe** und aktivieren Sie darin die benötigten Lagerprozesse (Kommissionierung, Einlagerung, Wareneingang, Warenausgang, Umlagerung).
- **C.** Legen Sie unter **Lagerarbeitsvorratsfiltervorlagen** je Arbeitsbereich eine **Lagerarbeitsvorratsfiltervorlage** an, damit die Anwender die Liste schnell auf ihren Bereich einschränken können.

**Tägliche Arbeit (Lagermitarbeiter):**

1. Öffnen Sie über **Suchen** die Seite **Lagerarbeitsvorrat**.
2. Schränken Sie im Bereich **Filter** die Liste über **Vorlagenfiltercode** und/oder **Lagergruppencodefilter** ein und blenden Sie bei Bedarf über **Beendete ausblenden** die abgeschlossenen Zeilen aus.
3. Markieren Sie die zu bearbeitende Zeile (oder mehrere Zeilen) in der Liste **Zeilen**.
4. Wählen Sie **Starten**. Die Zeile wechselt in den Status **Gestartet**; ein Eintrag wird in der Ereignishistorie festgehalten.
5. Nach Abschluss der physischen Arbeit wählen Sie **Beenden** (vollständig) oder **Teilbeenden** (Restmenge bleibt offen). Der zugehörige Herkunftsbeleg wird dabei gebucht.
6. Prüfen Sie bei Bedarf über **Ereignishistorie** den zeitlichen Verlauf der Zeile.

## Einrichtung

Die Einrichtung ist die Grundlage des Moduls. Sie legt fest, welche Lagerbelege im Lagerarbeitsvorrat erscheinen, wie die Buchung erfolgt und ob zusätzliche Funktionen (Lagerkapazität, Lagermaske) genutzt werden. Führen Sie die Schritte in der genannten Reihenfolge aus: zuerst die globale Einrichtung, danach die Stammdaten der Lagergruppen, anschließend die scoped Filtervorlagen und optionalen Funktionen.

### Lagerarbeitsvorratseinrichtung

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Lagerarbeitsvorratseinrichtung** (Karte, unternehmensweit ein Datensatz). Diese Seite wird beim ersten Öffnen automatisch angelegt.

**Prozess:** Der Administrator legt hier einmalig die unternehmensweit gültigen Grundwerte fest, bevor die erste Lagergruppe gepflegt wird. Die Felder steuern die Anzeige-Nummerierung, die Übernahme des kompletten Lagerplatzinhalts und die Nutzung der Lagerkapazität.

| Einrichtung | Erläuterung |
|---|---|
| **Globales Trennzeichen** | Wenn Sie ein Zeichen (Vorgabewert `%`) hinterlegen, dann verwendet das Modul dieses Zeichen als Trennzeichen bei der Zusammensetzung interner Bezeichner und Filter. Ändern Sie den Wert nur, wenn ein hinterlegtes Trennzeichen mit Ihren Codewerten kollidiert. |
| **Anzeigenreihenfolgezähler** | Wenn Sie hier einen Schrittwert (z. B. 10) eintragen, dann vergibt das System die **Anzeigenreihenfolge** neuer Lagergruppen- und Ansichtszeilen automatisch in diesem Abstand. Dadurch lassen sich später Zeilen dazwischenschieben, ohne alle Nummern neu vergeben zu müssen. |
| **Kompletten Lagerplatzinhalt verwenden** | Wenn aktiviert, dann wird dieser Vorgabewert beim Anlegen neuer Artikel in das gleichnamige Artikelfeld übernommen; die Umlagerung schlägt dann den vollständigen Bestand eines Lagerplatzes zur Bewegung vor, statt nur die Auftragsmenge. Ohne Kennzeichen wird ausschließlich die benötigte Menge vorgeschlagen. |
| **Lagerkapazität verwenden** | Wenn aktiviert, dann wird die Funktion **Lagerkapazitäten** freigeschaltet: Nur dann lässt sich die Seite Lagerkapazitäten öffnen und es können Höchstmengen je Lagerplatz gepflegt werden. Ohne Kennzeichen ist die Kapazitätsprüfung inaktiv. |

**Aktion auf dieser Seite:**

- **Webdienst initialisieren** — Wenn Sie diese Aktion ausführen, dann veröffentlicht das System den für die **Lagermaske** benötigten Webdienst (Tablet-/Scanner-Oberfläche). Führen Sie die Aktion aus, bevor Sie die Lagermaske in Betrieb nehmen; das System bestätigt die erfolgreiche Initialisierung mit einer Meldung.

Hinweis zur Berechtigung: Die im Modul mitgelieferte Berechtigungsgruppe bestimmt, welche Anwender die Einrichtungs-, Stammdaten- und Buchungsfunktionen des Lagerarbeitsvorrats ausführen dürfen. Vergeben Sie diese Gruppe an alle operativen Lagerbenutzer sowie an die Administratoren.

### Lagerarbeitsvorrat einrichten

Diese Kernfunktion — offene Lagerbelege sammeln, starten und beenden/buchen — setzt eine mehrstufige Konfiguration voraus. Wer sie einrichtet: der Administrator, vor der ersten produktiven Nutzung. Wo sie im Tagesablauf wirkt: auf der Seite **Lagerarbeitsvorrat** (Abschnitt *Tägliche Arbeit am Lagerarbeitsvorrat*).

1. **Zuerst** legen Sie in der **Lagerarbeitsvorratseinrichtung** die globalen Grundwerte fest (siehe oben). Wenn dies erfolgt ist, dann greifen die Vorgabewerte für alle nachgelagerten Schritte.
2. **Danach** pflegen Sie unter **Lagergruppen** die Stammdaten der Lagergruppen und aktivieren je Gruppe die Lagerprozesse (Kommissionierung, Einlagerung, Wareneingang, Warenausgang, Umlagerung). Wenn ein Lagerprozess in einer Gruppe aktiviert ist, dann erscheinen die zugehörigen Herkunftsbelege im Lagerarbeitsvorrat, sobald der Filter auf diese Gruppe gesetzt wird (siehe *Stammdaten → Lagergruppen*).
3. **Anschließend** erstellen Sie je Arbeitsbereich eine **Lagerarbeitsvorratsfiltervorlage** (nächster Abschnitt). Wenn eine Vorlage hinterlegt ist, dann kann der Anwender die Liste mit einem Klick auf seinen Bereich einschränken.
4. **Schließlich** arbeitet der Lagermitarbeiter im Tagesablauf mit den Aktionen **Starten**, **Teilbeenden** und **Beenden** (Operative Umsetzung, siehe *Tägliche Arbeit*).

#### Lagerarbeitsvorratsfiltervorlage

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Lagerarbeitsvorratsfiltervorlagen** und legen Sie mit *Neu* eine Vorlage an; die Karte **Lagerarbeitsvorratsfiltervorlage** öffnet sich.

**Prozess:** Der Administrator oder Key-User definiert je Arbeitsbereich (z. B. Wareneingangszone, Versandzone) eine Vorlage. Der Lagermitarbeiter wählt diese Vorlage später im Filterbereich der Seite Lagerarbeitsvorrat aus und sieht sofort nur die für ihn relevanten Zeilen.

| Feld | Erläuterung |
|---|---|
| **Code** | Wenn Sie einen eindeutigen Code vergeben, dann kann die Vorlage über **Vorlagenfiltercode** im Filterbereich des Lagerarbeitsvorrats ausgewählt werden. |
| **Beschreibung** | Wenn Sie eine sprechende Beschreibung erfassen, dann erkennt der Anwender in der Auswahl sofort, für welchen Arbeitsbereich die Vorlage gedacht ist. |
| **Lagergruppenfilter** | Wenn Sie hier eine oder mehrere **Lagergruppen** hinterlegen, dann zeigt die Liste beim Anwenden der Vorlage nur Zeilen dieser Gruppen. So wird die Sicht auf den zuständigen Lagerbereich eingeschränkt. |
| **Beendete ausblenden** | Wenn aktiviert, dann blendet die Liste beim Anwenden der Vorlage alle bereits beendeten Zeilen aus und zeigt nur die noch offene Arbeit. Ohne Kennzeichen bleiben auch abgeschlossene Zeilen sichtbar. |

### Umlagerung im Lagerarbeitsvorrat einrichten

Damit Umlagerungen (Bestandsverschiebungen zwischen Lagerorten/Lagerplätzen) über den Lagerarbeitsvorrat abgewickelt und gebucht werden können, ist eine eigene Konfigurationskette nötig. Wer sie einrichtet: der Administrator. Wo sie im Tagesablauf wirkt: über die Umlagerungszeilen im Lagerarbeitsvorrat (siehe *Tägliche Arbeit*) und das Artikel-Umlagerungsbuch.-Blatt.

1. **Zuerst** öffnen Sie über **Suchen** die **Artikel Buch.-Blattvorlagen** und aktivieren bei der gewünschten Vorlage das Feld **Lagerarbeitsvorrat benötigt**. Wenn aktiviert, dann prüft das System, dass die Vorlage die Art **Umlagerung** besitzt, und erzeugt für jede Buchblattzeile automatisch eine Zeile im Lagerarbeitsvorrat.

   | Feld | Erläuterung |
   |---|---|
   | **Lagerarbeitsvorrat benötigt** | Wenn aktiviert, dann werden alle über diese Buch.-Blattvorlage erfassten Umlagerungszeilen automatisch als Zeilen in den Lagerarbeitsvorrat übernommen und lassen sich dort starten und beenden/buchen. Die Aktivierung ist nur zulässig, wenn die Vorlage die Art **Umlagerung** hat (das System erzwingt dies). Ohne Kennzeichen bleibt die Umlagerung ein reiner Standard-Buchblattvorgang ohne Eintrag im Lagerarbeitsvorrat. |

   Dasselbe Feld steht auch in der Liste **Artikel Buch.-Blattvorlagen** zur Verfügung; die Wirkung ist identisch.

2. **Danach** hinterlegen Sie in der betreffenden **Lagergruppe** (siehe *Stammdaten → Lagergruppen*) das Kennzeichen **Umlagerung** sowie den **Buch.-Blattvorlagenname** und den **Buch.-Blattname**. Wenn diese Werte gesetzt sind, dann weiß das System, in welches Umlagerungsbuchblatt die Bewegungen der Gruppe gebucht werden.
3. **Optional** aktivieren Sie am Artikel das Feld **Kompletten Lagerplatzinhalt verwenden** (siehe *Stammdaten → Artikel*). Wenn aktiviert, dann schlägt die Umlagerung den vollständigen Lagerplatzbestand des Artikels zur Bewegung vor.
4. **Schließlich** bucht der Anwender die Umlagerungszeile im Lagerarbeitsvorrat über **Beenden** (Operative Umsetzung, siehe *Tägliche Arbeit → Umlagerungszeilen*).

### Lagerkapazität einrichten

Mit der Lagerkapazität lassen sich Höchstmengen je Lagerplatz hinterlegen. Wer sie einrichtet: der Administrator. Wo sie wirkt: bei Einlagerungs-/Umlagerungsvorschlägen, die den Lagerplatzinhalt berücksichtigen.

1. **Zuerst** aktivieren Sie in der **Lagerarbeitsvorratseinrichtung** das Feld **Lagerkapazität verwenden**. Wenn aktiviert, dann wird die Aktion **Lagerkapazitäten** freigeschaltet; ohne dieses Kennzeichen lässt sich die Kapazitätsseite nicht öffnen (das System prüft dies beim Öffnen).
2. **Danach** öffnen Sie die **Lagerortkarte** des betreffenden Lagerorts und wählen dort die Aktion **Lagerkapazitäten** (im Menüband unter *Zugehörig/Navigation*). Alternativ öffnen Sie **Lagerkapazitäten** direkt aus der Liste **Lagerplätze** bzw. der **Lagerplatzübersicht** über die gleichnamige Aktion; dann ist der Lagerplatz bereits vorbelegt.

**Felder der Seite Lagerkapazitäten:**

| Feld | Erläuterung |
|---|---|
| **Lagerortcode** | Wenn Sie den Lagerort hinterlegen, dann gilt die Kapazitätszeile für diesen Lagerort. Beim Einstieg über die Lagerortkarte oder Lagerplatzliste ist der Wert bereits vorbelegt. |
| **Lagerplatzcode** | Wenn Sie den Lagerplatz hinterlegen, dann begrenzt die Zeile die Kapazität dieses konkreten Lagerplatzes. |
| **Prozessart** | Legt fest, für welche Bewegungsrichtung die Höchstmenge gilt. **Alle:** Kapazität gilt für ein- und ausgehende Bewegungen. **Eingehend:** Kapazität wird nur bei Zugängen (Einlagerung/Wareneingang) geprüft. **Ausgehend:** Kapazität wird nur bei Abgängen (Kommissionierung/Warenausgang) geprüft. |
| **Art** | Bestimmt, worauf sich die Kapazität bezieht (z. B. artikel- oder einheitenbezogen). Beim Wechsel der Art wird das Feld **Nr.** geleert. Bei leerer Art meldet das System beim Setzen von **Nr.** einen Fehler. |
| **Nr.** | Wenn Sie hier den zur **Art** passenden Wert (z. B. eine Artikelnr.) hinterlegen, dann gilt die Kapazität nur für diesen Bezug. Voraussetzung ist eine gültige **Art**. |
| **Einheitencode** | Wenn Sie den Einheitencode setzen, dann wird die **Max. Menge** in dieser Einheit interpretiert. |
| **Max. Menge** | Wenn Sie eine Höchstmenge eintragen, dann darf der Lagerplatz für den angegebenen Bezug diese Menge nicht überschreiten; das Modul berücksichtigt den Wert bei den kapazitätsabhängigen Vorschlägen. |

### Lagermaske einrichten

Die **Lagermaske** ist die konfigurierbare Tablet-/Scanner-Oberfläche des Moduls für die Arbeit direkt am Lager. Sie besteht aus **Ansichten** (welche Felder und Aktionen je Prozess angezeigt werden) und der **Benutzer-/Gerätezuordnung**. Wer sie einrichtet: der Administrator. Wo sie wirkt: auf dem mobilen Endgerät des Lagermitarbeiters.

1. **Zuerst** führen Sie in der **Lagerarbeitsvorratseinrichtung** die Aktion **Webdienst initialisieren** aus. Wenn dies erfolgt ist, dann steht der Webdienst bereit, über den die mobile Oberfläche mit Business Central kommuniziert.
2. **Danach** definieren Sie unter **Lagermaskenansichten** je Prozessart eine **Lagermaskenansicht**.
3. **Schließlich** ordnen Sie unter **Lagermaske Benutzer** die Benutzer bzw. Geräte zu.

#### Lagermaskenansicht

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Lagermaskenansichten** und öffnen Sie eine Zeile; die Karte **Lagermaskenansicht** erscheint.

Die Karte gliedert sich in mehrere Bereiche, die je nach **Art** der Ansicht sichtbar sind. Jeder Bereich ist ein eigener Unterbereich mit eigenen Zeilen.

**Allgemein:**

| Feld | Erläuterung |
|---|---|
| **Art** | Bestimmt, für welchen Lagerprozess die Ansicht gilt und welche Bereiche eingeblendet werden. **Umlagerung:** Ansicht für Bestandsverschiebungen. **Lageraktivität:** Ansicht für Kommissionierung/Einlagerung (blendet zusätzlich die Bereiche Wareneingang und Warenausgang ein). **Wareneingang / Warenausgang:** Ansicht für den jeweiligen Beleg. **Mengeneingabe Umlagerung / Mengeneingabe Lageraktivität / Mengeneingabe Wareneingang / Mengeneingabe Warenausgang:** Ansichten, in denen der Mitarbeiter am Gerät ausschließlich Mengen erfasst. Nur bei den mengen- und aktivitätsbezogenen Arten ist die Spalte **Editierbar** in den Zeilen relevant. |
| **Beschreibung** | Wenn Sie eine Beschreibung erfassen, dann erkennt der Administrator in der Übersicht, wofür die Ansicht verwendet wird. |

**Bereiche (Unterseiten) der Ansicht:** **Kopfinformation**, **Zeileninformation** sowie – bei der Art **Lageraktivität** – **Wareneingang** und **Warenausgang**. Jeder Bereich enthält dieselben Felder für die Feldsteuerung.

**Zeilen der Bereiche (Lagermaske Zeilen):**

| Feld | Erläuterung |
|---|---|
| **Feldnr.** | Wenn Sie die Feldnummer wählen, dann wird das zugehörige Datenfeld in diesem Bereich der Maske angezeigt. |
| **Feldname** | Zeigt den Namen des ausgewählten Feldes zur Kontrolle an. |
| **Anzeigenreihenfolge** | Wenn Sie eine Reihenfolge vergeben, dann erscheinen die Felder am Gerät in dieser Sortierung. Der Vorgabewert ergibt sich aus dem **Anzeigenreihenfolgezähler** der Einrichtung. |
| **Editierbar** | Wenn aktiviert, dann darf der Mitarbeiter das Feld am Gerät ändern (nur bei mengen-/aktivitätsbezogenen Ansichtsarten sichtbar). Ohne Kennzeichen wird das Feld nur angezeigt. |
| **Editierbarkeit umschalten** | Wenn aktiviert, dann kann die Editierbarkeit des Feldes am Gerät situativ umgeschaltet werden; das System fragt in diesem Fall vor der Eingabe einer Teilmenge nach. Nur relevant, wenn **Editierbar** gesetzt ist. |

Über die Aktion **Übersetzungen** hinterlegen Sie je Feldzeile bzw. Aktion sprachabhängige Bezeichnungen; über den Bereich **Aktionen** legen Sie fest, welche Schaltflächen (z. B. Buchen, Schließen) am Gerät verfügbar sind.

#### Lagermaske Benutzer

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Lagermaske Benutzer**. Über die Kartenansicht **Benutzer/Gerät** pflegen Sie die Details eines Eintrags.

**Prozess:** Der Administrator ordnet jedem Lagerbenutzer bzw. jedem Gerät eine Filtervorlage und eine Sprache zu und aktiviert den Zugang. Der so eingerichtete Benutzer sieht am Gerät genau die für ihn vorgesehene Auswahl an Lagerarbeitsvorratszeilen.

| Einrichtung | Erläuterung |
|---|---|
| **Art** | Bestimmt, ob der Eintrag einen **Benutzer** oder ein **Gerät** betrifft. **Benutzer:** Der **Code** verweist auf einen Business-Central-Benutzernamen. **Gerät:** Der Eintrag gilt für ein Endgerät unabhängig vom angemeldeten Benutzer. |
| **Code** | Wenn Sie den Code hinterlegen, dann gilt die Zuordnung für diesen Benutzer bzw. dieses Gerät. Bei der Art **Benutzer** wird auf die Benutzertabelle verwiesen. |
| **Sprachcode** | Wenn Sie eine Sprache hinterlegen, dann erscheint die Lagermaske am Gerät in dieser Sprache. |
| **Status** | Legt fest, ob der Zugang aktiv ist. **Aktiviert:** Der Benutzer/das Gerät kann die Lagermaske verwenden. **Deaktiviert:** Der Zugang ist gesperrt; die Maske ist für diesen Eintrag nicht nutzbar. |

Im Unterbereich **Benutzerfilterzeilen** (Arbeitsbereichszeilen) hinterlegen Sie je Eintrag die anzuzeigenden Filter mit **Beschreibung** und **Anzeigenreihenfolge**, sodass der Benutzer am Gerät seine Arbeitsbereiche in der gewünschten Reihenfolge vorfindet.

## Stammdaten

### Lagergruppen

**Einstieg:** Die **Lagergruppen** bilden die zentrale Stammdatentabelle des Moduls. Öffnen Sie die Liste **Lagergruppen** und öffnen Sie eine Zeile, um die Karte **Lagergruppe** zu bearbeiten; die Lagergruppe wird außerdem als Nachschlage- und DrillDown-Seite dort geöffnet, wo eine Lagergruppe referenziert wird (z. B. im **Lagergruppenfilter** der Filtervorlage).

**Prozess:** Der Administrator legt je organisatorischem Lagerbereich eine Lagergruppe an und bestimmt darüber, **welche Lagerprozesse** in dieser Gruppe im Lagerarbeitsvorrat auftauchen. Anschließend wird die Gruppe in den Filtervorlagen und im Filterbereich der Liste Lagerarbeitsvorrat verwendet, um die Sicht der Anwender zu steuern.

| Feld | Erläuterung |
|---|---|
| **Code** | Wenn Sie einen eindeutigen Code vergeben, dann kann die Gruppe in Filtervorlagen und im **Lagergruppencodefilter** referenziert werden. |
| **Beschreibung** | Wenn Sie eine Beschreibung erfassen, dann ist die Gruppe in Auswahllisten eindeutig erkennbar. |
| **Einlagerung** | Wenn aktiviert, dann erscheinen Einlagerungs-Lageraktivitäten (mit Lagerlogistik) dieser Gruppe im Lagerarbeitsvorrat. Beim Zuordnen von Lagerorten werden nur Lagerorte akzeptiert, die Einlagerung erfordern. |
| **Kommissionierung** | Wenn aktiviert, dann erscheinen Kommissionierungs-Lageraktivitäten (mit Lagerlogistik) dieser Gruppe im Lagerarbeitsvorrat; die Lagerortzuordnung ist auf Lagerorte mit Kommissionierpflicht beschränkt. |
| **Lagereinlagerung** | Wenn aktiviert, dann werden Bestandseinlagerungen (Invt. Put-away, ohne erweiterte Lagerlogistik) dieser Gruppe berücksichtigt. |
| **Lagerkommissionierung** | Wenn aktiviert, dann werden Bestandskommissionierungen (Invt. Pick, ohne erweiterte Lagerlogistik) dieser Gruppe berücksichtigt. |
| **Wareneingang** | Wenn aktiviert, dann erscheinen offene Wareneingänge der zugeordneten Lagerorte im Lagerarbeitsvorrat und lassen sich von dort buchen. |
| **Warenausgang** | Wenn aktiviert, dann erscheinen offene Warenausgänge der zugeordneten Lagerorte im Lagerarbeitsvorrat und lassen sich von dort buchen. |
| **Umlagerung** | Wenn aktiviert, dann werden Umlagerungen dieser Gruppe im Lagerarbeitsvorrat geführt. Erst mit diesem Kennzeichen sind die Felder **Buch.-Blattvorlagenname** und **Buch.-Blattname** editierbar; beim Zurücksetzen werden beide geleert. Setzt die **Lagerplatzverwendung** auf **Von** oder **Nach**, ist die Umlagerung zwingend aktiv (das System prüft dies). |
| **Lagerplatzverwendung** | Steuert, wie Lagerplätze der Gruppe bei der Umlagerung verwendet werden. **Alle:** keine Einschränkung. **Von:** Lagerplätze dienen als Herkunft. **Nach:** Lagerplätze dienen als Ziel. Die Werte **Von** und **Nach** setzen voraus, dass **Umlagerung** aktiv ist. |
| **Buch.-Blattvorlagenname** | Wenn Sie die Umlagerungs-Buchblattvorlage hinterlegen, dann werden die Umlagerungen der Gruppe in diese Vorlage gebucht. Auswählbar sind nur Vorlagen der Art **Umlagerung** mit **Lagerarbeitsvorrat benötigt**. Editierbar nur bei aktiver **Umlagerung**. |
| **Buch.-Blattname** | Wenn Sie das konkrete Buch.-Blatt hinterlegen, dann werden die Umlagerungen in dieses Blatt der gewählten Vorlage geschrieben. Editierbar nur bei aktiver **Umlagerung**. |

**Abhängigkeit (Prüfung im Code):** Beim Speichern prüft das System, dass bei **Lagerplatzverwendung** = Von/Nach das Kennzeichen **Umlagerung** gesetzt ist und dass bei inaktiver Umlagerung die beiden Buchblattfelder leer sind. Ordnen Sie im Unterbereich **Lagergruppenzeilen** die konkreten Lagerorte und Lagerplätze zu; die dort erlaubten Lagerorte richten sich nach den in der Gruppe aktivierten Lagerprozessen.

#### Lagergruppenzeilen

Im Unterbereich **Lagergruppenzeilen** der Lagergruppe hinterlegen Sie, für welche Lagerorte und Lagerplätze die Gruppe gilt.

| Feld | Erläuterung |
|---|---|
| **Lagerortcode** | Wenn Sie einen Lagerort wählen, dann gilt die Gruppe für diesen Lagerort. Die Auswahl ist auf Lagerorte beschränkt, deren Logistikkennzeichen zu den in der Gruppe aktivierten Prozessen passen (z. B. Kommissionierpflicht bei aktiver Kommissionierung). |
| **Lagerplatzcode** | Wenn Sie einen Lagerplatz wählen, dann wird die Gruppe zusätzlich auf diesen Lagerplatz eingegrenzt. |
| **Beschreibung** | Zeigt automatisch die Beschreibung des gewählten Lagerplatzes an, damit die Zuordnung eindeutig ist. |

### Artikel: Kompletten Lagerplatzinhalt verwenden

**Einstieg:** Öffnen Sie über **Artikel** die **Artikelkarte** und wechseln Sie in das Inforegister **Lager**.

**Prozess:** Der Administrator oder Disponent entscheidet je Artikel, ob bei Umlagerungen der komplette Lagerplatzinhalt bewegt werden soll. Der Vorgabewert stammt aus der **Lagerarbeitsvorratseinrichtung** und wird beim Anlegen neuer Artikel übernommen; er kann je Artikel überschrieben werden.

| Feld | Erläuterung |
|---|---|
| **Kompletten Lagerplatzinhalt verwenden** | Wenn aktiviert, dann schlägt die Umlagerung für diesen Artikel den vollständigen am Lagerplatz vorhandenen Bestand zur Bewegung vor, statt nur die für den Auftrag benötigte Menge. Das ist sinnvoll, wenn ein Lagerplatz vollständig geräumt werden soll. Ohne Kennzeichen wird nur die benötigte Menge vorgeschlagen. |

Dieses Kennzeichen wirkt zusammen mit der Einrichtung *Umlagerung im Lagerarbeitsvorrat* (siehe dort).

## Tägliche Arbeit am Lagerarbeitsvorrat

Die Seite **Lagerarbeitsvorrat** ist der zentrale Arbeitsplatz der operativen Lagermitarbeiter. Sie zeigt alle offenen Lagerbelege als Zeilen und stellt die Aktionen zum Starten, Teilbeenden, Beenden, Wiedereröffnen sowie den Zugriff auf die Ereignishistorie bereit. Welche Zeilen erscheinen, steuert der Administrator über die **Lagergruppen** und die **Lagerarbeitsvorratseinrichtung** (siehe *Einrichtung*).

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Lagerarbeitsvorrat**.

### Filter

Der Filterbereich am Kopf der Seite schränkt die angezeigten Zeilen ein. Da bei aktiven Filtervorlagen und Lagergruppen die Trefferzahl deutlich sinkt, sollte jeder Anwender zuerst hier seinen Bereich einstellen.

| Filterfeld | Erläuterung |
|---|---|
| **Vorlagenfiltercode** | Wenn gesetzt, dann werden die Zeilen anhand der ausgewählten **Lagerarbeitsvorratsfiltervorlage** gefiltert; die in der Vorlage hinterlegten Lagergruppen und die Einstellung **Beendete ausblenden** werden übernommen. |
| **Lagergruppencodefilter** | Wenn gesetzt, dann werden nur Zeilen der angegebenen **Lagergruppen** angezeigt. Über das Nachschlagen lässt sich der Filterausdruck bequem aus den vorhandenen Gruppen zusammenstellen; das System prüft die Gültigkeit des eingegebenen Filters. |
| **Beendete ausblenden** | Wenn gesetzt, dann werden alle Zeilen mit Status **Beendet** ausgeblendet und nur die noch offene Arbeit angezeigt. Ohne Kennzeichen bleiben beendete Zeilen sichtbar (z. B. zur Nachschau). |

### Zeilen und Spalten

Die Liste **Zeilen** zeigt je offenem Lagerbeleg eine Zeile. Die Zeilen sind nach **Lieferdatum** sortiert; beendete Zeilen werden optisch abgesetzt dargestellt, der Status ist zusätzlich farblich hervorgehoben.

| Feld | Erläuterung |
|---|---|
| **Projektbeschreibung** | Zeigt die Kennung des Herkunftsbelegs (Belegnr. und Zeilennr.), damit der Anwender die Zeile eindeutig einem Beleg zuordnen kann. |
| **Status** | Zeigt den Bearbeitungsstand der Zeile. **Offen:** Zeile angelegt, noch nicht gestartet — nur **Starten** ist möglich. **Geplant:** vorgemerkter Zustand (farblich hervorgehoben), noch keine Bearbeitung. **Gestartet:** Bearbeitung läuft — **Teilbeenden** und **Beenden** sind möglich. **Unterbrochen:** Bearbeitung pausiert (farblich als kritisch markiert). **Teilbeendet:** ein Teil ist gebucht, eine Restmenge bleibt offen — kann erneut **gestartet** werden. **Beendet:** Zeile vollständig gebucht/abgeschlossen — wird abgesetzt dargestellt; kann bei Bedarf über **Erneut öffnen** wieder geöffnet werden. |
| **Lieferdatum** | Zeigt das Liefer-/Fälligkeitsdatum des Herkunftsbelegs; steuert die Sortierung und Dringlichkeit der Abarbeitung. |
| **Herkunfts-ID** | Zeigt die Belegnummer des Herkunftsbelegs (Warenausgang, Wareneingang, Lageraktivität oder Buch.-Blattvorlage). |
| **Lagerortcode** | Zeigt den Lagerort, an dem die Bewegung stattfindet. |
| **Lagerplatzcode** | Zeigt den Quell-Lagerplatz der Bewegung. |
| **Neuer Lagerortcode** | Zeigt bei Umlagerungen den Ziel-Lagerort. |
| **Neuer Lagerplatzcode** | Zeigt bei Umlagerungen den Ziel-Lagerplatz. |
| **Debitorname** | Zeigt bei Warenausgängen aus Verkaufsaufträgen den Namen des Debitors. |
| **Verkaufsauftragsnr.** | Zeigt bei Warenausgängen die zugrunde liegende Verkaufsauftragsnummer. |
| **Artikelnr.** | Zeigt den zu bewegenden Artikel. |
| **Artikelbeschreibung** | Zeigt die Bezeichnung des Artikels. |
| **Artikelbeschreibung 2** | Zeigt die zweite Bezeichnungszeile des Artikels. |
| **Menge** | Zeigt die zu bearbeitende (offene) Menge der Zeile. |

Je nach Herkunftsart blendet die Seite unterhalb der Liste einen passenden Detailbereich ein — z. B. die **Warenausgangszeilen**, die **Wareneingangszeilen**, die Kommissionier-/Einlagerungszeilen oder bei Umlagerungen die **Umlagerungszeilen** (Artikel-Umlagerungsbuchblatt). So sieht der Anwender die Details des Herkunftsbelegs direkt in derselben Ansicht.

### Aktionen und Buchungsablauf

Die folgenden Aktionen stehen im Menüband bereit; sie sind je nach Status der markierten Zeile aktiv oder inaktiv.

| Aktion | Erläuterung |
|---|---|
| **Starten** | Wenn Sie eine Zeile mit Status **Offen** (oder erneut nach Teilbeenden/Beenden) starten, dann wechselt die Zeile in den Status **Gestartet** und es wird ein Eintrag in der **Ereignishistorie** geschrieben. Erst danach sind Teilbeenden und Beenden möglich. Bei Zeilen ohne gültige Herkunft ist die Aktion nicht verfügbar. |
| **Teilbeenden** | Wenn Sie eine gestartete Zeile teilbeenden, dann setzt das System den Status auf **Teilbeendet**, schreibt einen Ereigniseintrag und bucht die bearbeitete Teilmenge des Herkunftsbelegs. Die Restmenge bleibt offen und kann später erneut gestartet werden. |
| **Beenden** | Wenn Sie eine gestartete Zeile beenden, dann setzt das System den Status auf **Beendet**, schreibt einen Ereigniseintrag und bucht den Herkunftsbeleg. Bei einer Restmenge kennzeichnet das System den Beleg zusätzlich als vollständig abgeschlossen, sodass keine weitere Lieferung/Zugang erwartet wird. |
| **Erneut öffnen** | Wenn Sie eine noch nicht beendete Zeile erneut öffnen, dann wird ihr Status auf **Offen** zurückgesetzt. So lässt sich eine versehentlich gestartete Zeile zurückstellen. |
| **Ereignishistorie** | Wenn Sie diese Aktion wählen, dann öffnet sich die **Lagervorratsereigniszeile** mit dem chronologischen Verlauf der markierten Zeile. |

**Buchungsablauf (Schritt für Schritt):**

1. Zeile auf **Lagerarbeitsvorrat** markieren.
2. **Starten** — Status wechselt auf **Gestartet**, Ereigniseintrag entsteht.
3. Physische Lagerarbeit ausführen (kommissionieren, einlagern, Ware annehmen/ausgeben, umlagern).
4. **Teilbeenden** (Restmenge bleibt offen) **oder** **Beenden** (vollständig).
5. Das Modul bucht den passenden Herkunftsbeleg automatisch: Warenausgang über den Warenausgang-Buchungslauf, Wareneingang über den Wareneingang-Buchungslauf, Kommissionierung/Einlagerung über die Lageraktivitäts-Registrierung, Umlagerung über die Artikel-Umlagerungsbuchung.
6. Ergebnis über **Ereignishistorie** kontrollieren.

**Automatischer Abschluss vom Beleg aus:** Wird ein Herkunftsbeleg direkt im Standard gebucht bzw. registriert (Warenausgang, Wareneingang, Lageraktivität oder Umlagerungsbuchblatt), dann setzt das Modul die zugehörige Lagerarbeitsvorratszeile automatisch auf **Beendet**, ohne erneut zu buchen. So bleibt der Lagerarbeitsvorrat auch dann aktuell, wenn außerhalb der Liste gebucht wurde.

### Umlagerungszeilen

Bei Zeilen mit der Herkunft **Umlagerung** (Artikel-Umlagerungsbuch.-Blatt) wird unterhalb der Liste der Bereich **Umlagerungszeilen** eingeblendet. Dort sehen Sie die Buch.-Blattzeilen mit Herkunfts- und Ziel-Lagerplatz. Über die zugehörigen Aktionen erreichen Sie den **Lagerplatzinhalt**, die **Dimensionen** und die **Artikelverfolgungszeilen** der Zeile. Der Abschluss erfolgt wie bei allen anderen Herkunftsarten über **Beenden**; dabei wird die Umlagerung im hinterlegten Buch.-Blatt gebucht (Voraussetzung: Neuer Lagerplatzcode ist gefüllt).

## Historie und Nachverfolgung

Jede Statusänderung einer Lagerarbeitsvorratszeile (Starten, Teilbeenden, Beenden) wird protokolliert. So lässt sich nachvollziehen, wann und durch wen eine Zeile bearbeitet wurde.

**Einstieg:** Markieren Sie auf der Seite **Lagerarbeitsvorrat** die gewünschte Zeile und wählen Sie die Aktion **Ereignishistorie**. Es öffnet sich die **Lagervorratsereigniszeile**.

| Feld | Erläuterung |
|---|---|
| **Status** | Zeigt, in welchen Status die Zeile mit diesem Ereignis gewechselt ist (z. B. Gestartet, Teilbeendet, Beendet). |
| **Datum** | Zeigt das Datum der Statusänderung. |
| **Zeit** | Zeigt die Uhrzeit der Statusänderung. |
| **Menge** | Zeigt die zum Zeitpunkt des Ereignisses relevante Menge. |
| **Lagerortcode** | Zeigt den Lagerort der bearbeiteten Zeile. |
| **Lagerplatzcode** | Zeigt den Lagerplatz der bearbeiteten Zeile. |

Zu jedem Ereignis speichert das System zusätzlich den erstellenden Benutzer sowie das vorherige Startdatum, sodass sich die Bearbeitungsdauer je Zeile nachvollziehen lässt.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen typische Auslöser und den vollständigen Ablauf in Business Central. Alle Seiten und Aktionen sind im Modul vorhanden und verhalten sich wie beschrieben.

### Warenausgang für einen Verkaufsauftrag kommissionieren

- **Auslöser:** Ein freigegebener Verkaufsauftrag ist versandbereit; aus ihm wurde ein Warenausgang erstellt.
- **Einstieg in BC:** Der Lagermitarbeiter öffnet über **Suchen** die Seite **Lagerarbeitsvorrat**. Im Bereich **Filter** wählt er über **Vorlagenfiltercode** seine Versand-Filtervorlage; die Liste zeigt nur die Warenausgänge seiner **Lagergruppe**.
- **Kernablauf:** Er markiert die Zeile (Herkunft Warenausgang, Debitorname und Verkaufsauftragsnr. sichtbar) und wählt **Starten** — der Status wechselt auf **Gestartet**. Nach dem Kommissionieren wählt er **Beenden**. Das Modul bucht den Warenausgang. Ist nur eine Teilmenge versandfertig, wählt er stattdessen **Teilbeenden**; die Restmenge bleibt als offene Zeile stehen.
- **Abschluss:** Über **Ereignishistorie** prüft er, dass die Zeile mit Datum und Uhrzeit auf **Beendet** gesetzt wurde.

### Interne Umlagerung zwischen Lagerplätzen buchen

- **Auslöser:** Bestand soll von einem Lagerplatz auf einen anderen verschoben werden; die Bewegung wurde in einem Artikel-Umlagerungsbuch.-Blatt erfasst (Buch.-Blattvorlage mit **Lagerarbeitsvorrat benötigt**).
- **Einstieg in BC:** Für jede Buch.-Blattzeile ist automatisch eine Zeile im **Lagerarbeitsvorrat** entstanden. Der Mitarbeiter filtert die Liste auf die Umlagerungs-**Lagergruppe**.
- **Kernablauf:** Er markiert die Umlagerungszeile; im eingeblendeten Bereich **Umlagerungszeilen** sieht er Herkunfts- und **Neuer Lagerplatzcode**. Er wählt **Starten**, führt die Umlagerung physisch aus und wählt **Beenden**. Das Modul bucht die Umlagerung in das in der Lagergruppe hinterlegte **Buch.-Blatt**.
- **Abschluss:** Die Zeile steht auf **Beendet**; der Bestand ist auf dem neuen Lagerplatz gebucht.

### Wareneingang einer Einkaufsbestellung abschließen

- **Auslöser:** Zu einer Einkaufsbestellung ist ein Wareneingangsbeleg angelegt worden; die Ware ist eingetroffen.
- **Einstieg in BC:** Die Wareneingangszeile erscheint automatisch im **Lagerarbeitsvorrat**. Der Mitarbeiter filtert auf seine Wareneingangs-**Lagergruppe**.
- **Kernablauf:** Er markiert die Zeile, wählt **Starten**, kontrolliert die Ware und wählt **Beenden**; das Modul bucht den Wareneingang. Alternativ kann der Beleg auch direkt im Standard gebucht werden — dann setzt das Modul die Lagerarbeitsvorratszeile automatisch auf **Beendet**.
- **Abschluss:** Kontrolle über **Ereignishistorie**.

## FAQ und Troubleshooting

### Warum erscheint mein Lagerbeleg nicht im Lagerarbeitsvorrat?

Eine Zeile entsteht nur, wenn der Herkunftsprozess in einer **Lagergruppe** aktiviert ist und der betroffene Lagerort dieser Gruppe zugeordnet ist. Prüfen Sie in den **Lagergruppen**, ob z. B. **Wareneingang**, **Warenausgang**, **Kommissionierung** oder **Umlagerung** gesetzt ist und ob der Lagerort in den **Lagergruppenzeilen** hinterlegt wurde.

### Warum ist die Aktion Starten ausgegraut?

**Starten** ist nur bei Zeilen mit Status **Offen**, **Teilbeendet** oder **Beendet** und einer gültigen Herkunft verfügbar. Bei einer bereits gestarteten Zeile ist stattdessen **Teilbeenden** oder **Beenden** aktiv. Zeilen ohne gültige Herkunftsart lassen sich nicht starten.

### Was ist der Unterschied zwischen Teilbeenden und Beenden?

**Beenden** bucht den Herkunftsbeleg vollständig und setzt die Zeile auf **Beendet**. **Teilbeenden** bucht nur die bearbeitete Teilmenge und setzt den Status auf **Teilbeendet**; die Restmenge bleibt als offene Arbeit erhalten und kann erneut gestartet werden. Eine offene Restmenge ist ausdrücklich zulässig — Sie müssen nicht auf den vollständigen Ausgleich warten.

### Was passiert, wenn ich eine Zeile beende, die nur teilweise geliefert wird?

Ist die zu buchende Menge kleiner als die Belegmenge und Sie wählen **Beenden**, dann kennzeichnet das Modul den Herkunftsbeleg zusätzlich als vollständig abgeschlossen. Dadurch wird für die Restmenge keine weitere Lieferung bzw. kein weiterer Zugang mehr erwartet.

### Warum kann ich in der Lagergruppe die Buch.-Blattfelder nicht ausfüllen?

Der **Buch.-Blattvorlagenname** und der **Buch.-Blattname** sind nur editierbar, wenn in der Lagergruppe das Kennzeichen **Umlagerung** aktiv ist. Aktivieren Sie zuerst **Umlagerung**; deaktivieren Sie es wieder, werden beide Felder automatisch geleert.

### Warum lässt sich die Buch.-Blattvorlage nicht auswählen?

Auswählbar sind nur Artikel-Buch.-Blattvorlagen der Art **Umlagerung**, bei denen das Feld **Lagerarbeitsvorrat benötigt** aktiviert ist. Setzen Sie dieses Kennzeichen zuerst in den **Artikel Buch.-Blattvorlagen**; das System erzwingt dabei die Art **Umlagerung**.

### Warum kann ich die Seite Lagerkapazitäten nicht öffnen?

Die Lagerkapazität ist nur verfügbar, wenn in der **Lagerarbeitsvorratseinrichtung** das Feld **Lagerkapazität verwenden** aktiviert ist. Ohne dieses Kennzeichen meldet das System beim Öffnen einen Fehler. Aktivieren Sie die Einrichtung und öffnen Sie **Lagerkapazitäten** anschließend über die Lagerortkarte oder die Lagerplatzliste.

### Wie ändere ich die Reihenfolge der Zeilen in der Lagermaske?

Vergeben Sie in den **Lagergruppenzeilen** bzw. in den **Lagermaske Zeilen** eine **Anzeigenreihenfolge**. Der Vorgabeabstand ergibt sich aus dem **Anzeigenreihenfolgezähler** der Einrichtung. Eine bereits vergebene Anzeigenreihenfolge darf innerhalb derselben Gruppe nicht doppelt vorkommen — sonst meldet das System einen Fehler.

### Warum funktioniert die Lagermaske auf dem Gerät nicht?

Die Lagermaske benötigt einen veröffentlichten Webdienst. Führen Sie in der **Lagerarbeitsvorratseinrichtung** die Aktion **Webdienst initialisieren** aus und stellen Sie sicher, dass der betreffende Eintrag unter **Lagermaske Benutzer** den Status **Aktiviert** besitzt.

### Kann ich eine versehentlich beendete Zeile rückgängig machen?

Solange die Zeile nicht bereits beendet ist, setzt **Erneut öffnen** den Status auf **Offen** zurück. Eine bereits über **Beenden** gebuchte Zeile ist abgeschlossen; wurde sie automatisch vom Beleg aus beendet, steuern Sie Korrekturen über den Standard-Belegprozess des Herkunftsbelegs.
