---
title: Anwenderhandbuch m+m HTML Editor
---

# Anwenderhandbuch m+m HTML Editor

## Einleitung

Der **m+m HTML Editor** stellt in Microsoft Dynamics 365 Business Central einen komfortablen
Rich-Text-Editor bereit, mit dem Anwender lange Textfelder (Langtextfelder) formatiert erfassen
und pflegen können. Statt reinen Fließtext einzugeben, bearbeiten Sie den Inhalt in einer
Symbolleiste mit Formatierungsfunktionen wie Schriftgröße, Fett, Aufzählungen, Tabellen und
Bildern; der Editor speichert das Ergebnis als HTML in das zugrunde liegende Langtextfeld zurück.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender**, die im Tagesgeschäft
Langtexte pflegen — etwa Beschreibungen, Hinweise oder Belegtexte auf Seiten, in die das
Editor-Steuerelement eingebettet ist. Sekundär angesprochen sind **Administratoren und Key User**,
die die App installieren, die Lizenz sicherstellen und Berechtigungen vergeben.

**Kurzer Prozessüberblick:** Der Anwender öffnet eine Seite, auf der ein Langtextfeld über den
HTML-Editor bereitgestellt wird → er bearbeitet und formatiert den Text in der Symbolleiste → die
Eingaben werden automatisch bzw. beim Speichern der Seite in das Feld übernommen. Der Editor
erscheint entweder als **großflächiges Bearbeitungsfeld** oder als kompakter **Faktenbox-Editor**
am Seitenrand.

Dieses Modul ist eine technische Erweiterung: Es liefert das Editor-Steuerelement, das andere
Business-Central-Seiten für ihre Langtextfelder verwenden. Es bringt selbst keine eigenen Listen,
Belege, Stammdaten oder Einrichtungsseiten mit; die konkrete Seite, auf der Sie den Editor
antreffen, wird durch die jeweils aufrufende Funktion bestimmt.

## Schnellstart für Anwender

Der schnellste Weg vom Öffnen bis zum gespeicherten, formatierten Text:

1. **Seite mit Langtextfeld öffnen.** Rufen Sie die Seite auf, deren Langtextfeld über den
   HTML-Editor bereitgestellt wird (z. B. ein Bemerkungs- oder Beschreibungsfeld). Der Editor wird
   als Bearbeitungsbereich mit einer Symbolleiste angezeigt.
2. **Text eingeben oder einfügen.** Klicken Sie in den Bearbeitungsbereich und schreiben oder fügen
   Sie Ihren Text ein.
3. **Formatieren.** Nutzen Sie die Symbolleiste — etwa **[[en:Bold]]**, **[[en:Font Size]]**,
   **[[en:Bulleted List]]** oder **[[en:Insert table]]** — um den Text zu gestalten.
4. **Speichern.** Der Editor übernimmt Änderungen automatisch (automatisches Speichern); zusätzlich
   werden die Inhalte gesichert, wenn die aufrufende Seite die Speicherung anfordert. Verlassen bzw.
   schließen Sie die Seite wie gewohnt, um den Datensatz festzuschreiben.

Wenn das Feld **schreibgeschützt** angezeigt wird, blendet der Editor die Symbolleiste aus und lässt
nur das Lesen zu — das ist kein Fehler, sondern spiegelt den Bearbeitungsstatus des Datensatzes
wider.

## Einrichtung

Der m+m HTML Editor bringt **keine eigene Einrichtungsseite, keine Nummernserien und keine Report-
oder Mailparameter** mit. Die Einrichtung beschränkt sich auf die technische Bereitstellung der App,
eine gültige Lizenz und die Berechtigungsvergabe. Diese Schritte führt der Administrator einmalig
vor der ersten Nutzung durch; danach steht das Editor-Steuerelement überall dort zur Verfügung, wo
eine aufrufende Seite es einbindet.

### Installation und Abhängigkeit einrichten

**Prozess:** Der Administrator installiert die App in der Business-Central-Umgebung. Der m+m HTML
Editor setzt die Basis-App **m+m Cloud Base** voraus (Abhängigkeit in `app.json`); ohne diese Basis
lässt sich das Modul nicht installieren.

Gehen Sie in dependency-order vor:

1. **Zuerst** stellen Sie sicher, dass **m+m Cloud Base** in der Zielumgebung installiert ist.
2. **Danach** installieren Sie den **m+m HTML Editor** (App-Version 27.0.0.0, kompatibel mit
   Plattform und Anwendung 27.0.0.0).
3. **Schließlich** melden sich die Anwender an; ab diesem Zeitpunkt ist das Editor-Steuerelement für
   aufrufende Seiten verfügbar.

Nach der Installation ist keine weitere feldbezogene Konfiguration nötig — der Editor konfiguriert
seine Symbolleiste und sein Verhalten selbst.

### Lizenzprüfung verstehen

**Prozess:** Bei jeder Benutzeranmeldung prüft das Modul automatisch die Lizenz. Diese Prüfung ist
nicht sichtbar konfigurierbar; sie läuft im Hintergrund und bindet den HTML-Editor an eine gültige
Lizenz der m+m-Produktlinie.

| Vorgang | Erläuterung |
|---------|-------------|
| Lizenzprüfung bei Anmeldung | Wenn sich ein Anwender anmeldet, ermittelt das Modul die eigene App-Registrierung und ruft die Lizenzprüfung der Basis auf; dadurch wird sichergestellt, dass der HTML-Editor nur in lizenzierten Umgebungen aktiv ist. Ohne gültige Lizenz stehen die Funktionen des Moduls nicht bereit — der Administrator muss die Lizenz der m+m-Produktlinie prüfen lassen. |

Die Prüfung erfolgt gegen die aktuelle Modul-Registrierung (installierte App) und den angemeldeten
Benutzer im aktuellen Mandanten. Für den operativen Anwender ist hier nichts einzustellen; relevant
ist nur, dass bei fehlender Lizenz der Editor nicht wie erwartet arbeitet und der Administrator zu
informieren ist.

### Berechtigungen vergeben

**Prozess:** Damit Anwender die Funktionen des Moduls nutzen können, weist der Administrator den
mitgelieferten Berechtigungssatz zu. Das Modul liefert einen zuweisbaren Berechtigungssatz mit der
Bezeichnung **[[en:All permissions]]**.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Berechtigungssatz **[[en:All permissions]]** | Wenn dieser Berechtigungssatz einem Benutzer oder einer Benutzergruppe zugewiesen ist, erhält der Anwender Zugriff auf die Funktionsbausteine des HTML-Editors; ohne diese Zuweisung kann das Modul seine Objekte für den Benutzer nicht ausführen. Der Satz bestimmt damit, welche Benutzer den Editor nutzen dürfen. |

Weisen Sie den Berechtigungssatz den Benutzern zu, die Langtexte über den Editor pflegen sollen.
Eine feldweise Steuerung ist nicht vorgesehen; der Zugriff wird auf Modulebene geregelt.

## Der HTML-Editor im Alltag

Sobald eine aufrufende Seite ein Langtextfeld über den HTML-Editor bereitstellt, arbeiten Sie
direkt im Bearbeitungsbereich. Der Editor lädt den vorhandenen Feldinhalt beim Öffnen und
übernimmt Ihre Änderungen automatisch zurück in das Feld.

### Bearbeiten, Laden und Speichern

**Ablauf beim Öffnen und Bearbeiten:**

1. **Zuerst** öffnet die Seite den Editor und lädt den bestehenden Inhalt des Langtextfelds in den
   Bearbeitungsbereich.
2. **Danach** bearbeiten Sie den Text. Der Editor speichert Ihre Eingaben mit **automatischem
   Speichern** kurz nach der letzten Änderung selbstständig zwischen.
3. **Schließlich** übernimmt der Editor die Inhalte, wenn die aufrufende Seite eine Speicherung
   anfordert oder Sie die Seite schließen; der formatierte HTML-Inhalt wird in das Feld
   geschrieben.

| Funktion | Erläuterung |
|----------|-------------|
| Automatisches Speichern | Wenn Sie den Text ändern, meldet der Editor die Änderung nach kurzer Wartezeit selbstständig zurück; dadurch geht Ihr Zwischenstand nicht verloren, auch wenn Sie nicht manuell speichern. |
| Laden des Feldinhalts | Beim Öffnen wird der aktuelle Feldinhalt in den Editor geladen, sodass Sie stets auf dem zuletzt gespeicherten Stand weiterarbeiten. |
| Speicherung anfordern | Wenn die aufrufende Seite die Speicherung auslöst, übergibt der Editor den aktuellen HTML-Inhalt an das Feld; damit ist sichergestellt, dass Ihre Formatierungen mit dem Datensatz festgeschrieben werden. |

### Symbolleiste und Formatierungsfunktionen

Die Symbolleiste des großflächigen Editors stellt folgende Funktionen bereit. Die Bezeichnungen der
Schaltflächen erscheinen in Business Central in englischer Sprache.

| Funktion | Erläuterung |
|----------|-------------|
| **[[en:Heading]]** | Wenn Sie einen Absatz als Überschrift auszeichnen, wird der Text als strukturierte Überschrift dargestellt; das gliedert längere Inhalte lesbar. |
| **[[en:Font Size]]** | Wenn Sie eine Schriftgröße wählen (verfügbar: 9, 11, 13, Standard, 17, 19, 21), wird der markierte Text in dieser Größe dargestellt; ohne Auswahl bleibt die Standardgröße erhalten. |
| **[[en:Font Family]]** | Wenn Sie eine Schriftart auswählen, wird der markierte Text in dieser Schriftart gesetzt. |
| **[[en:Font Color]]** | Wenn Sie eine Vordergrundfarbe aus der Farbpalette wählen, wird der markierte Text in dieser Farbe eingefärbt. Verfügbare Farben u. a. **[[en:Black]]**, **[[en:Dim grey]]**, **[[en:Grey]]**, **[[en:Light grey]]**, **[[en:White]]**, **[[en:Red]]**, **[[en:Orange]]**, **[[en:Yellow]]**, **[[en:Light green]]**, **[[en:Green]]**, **[[en:Aquamarine]]**, **[[en:Turquoise]]**, **[[en:Light blue]]**, **[[en:Blue]]**, **[[en:Purple]]**. |
| **[[en:Font Background Color]]** | Wenn Sie eine Hintergrundfarbe wählen, wird der markierte Text farbig hinterlegt (z. B. zur Hervorhebung); es steht dieselbe Farbpalette wie bei der Schriftfarbe zur Verfügung. |
| **[[en:Bold]]** | Wenn Sie diese Funktion anwenden, wird der markierte Text fett dargestellt. |
| **[[en:Italic]]** | Wenn Sie diese Funktion anwenden, wird der markierte Text kursiv dargestellt. |
| **[[en:Underline]]** | Wenn Sie diese Funktion anwenden, wird der markierte Text unterstrichen. |
| **[[en:Remove Format]]** | Wenn Sie diese Funktion anwenden, werden alle Zeichenformatierungen des markierten Texts entfernt und der Text auf die Grunddarstellung zurückgesetzt. |
| **[[en:Link]]** | Wenn Sie einen Link einfügen, wird der markierte Text mit einer Zieladresse verknüpft; der Leser kann dem Verweis später folgen. |
| **[[en:Bulleted List]]** | Wenn Sie diese Funktion anwenden, werden die gewählten Zeilen als unnummerierte Aufzählung mit Punkten formatiert. |
| **[[en:Numbered List]]** | Wenn Sie diese Funktion anwenden, werden die gewählten Zeilen als nummerierte Liste formatiert; die Nummerierung wird automatisch fortgeführt. |
| **[[en:Alignment]]** | Wenn Sie eine Ausrichtung wählen, wird der Absatz entsprechend (links, zentriert, rechts, Blocksatz) ausgerichtet. |
| **[[en:Increase Indent]]** | Wenn Sie diese Funktion anwenden, wird der Absatz eine Ebene weiter eingerückt; das eignet sich für Verschachtelungen in Listen. |
| **[[en:Decrease Indent]]** | Wenn Sie diese Funktion anwenden, wird die Einrückung des Absatzes um eine Ebene verringert. |
| **[[en:Insert image]]** | Wenn Sie ein Bild einfügen, wird eine Grafik in den Text übernommen; anschließend stehen Bildwerkzeuge zur Verfügung (siehe unten). |
| **[[en:Block quote]]** | Wenn Sie diese Funktion anwenden, wird der markierte Absatz als abgesetztes Zitat dargestellt und optisch vom übrigen Text hervorgehoben. |
| **[[en:Insert table]]** | Wenn Sie eine Tabelle einfügen, wird ein Zeilen-/Spaltenraster in den Text übernommen; danach stehen Tabellenwerkzeuge zum Bearbeiten bereit (siehe unten). |
| **[[en:Undo]]** | Wenn Sie diese Funktion anwenden, wird der letzte Bearbeitungsschritt rückgängig gemacht. |
| **[[en:Redo]]** | Wenn Sie diese Funktion anwenden, wird ein zuvor rückgängig gemachter Schritt wiederhergestellt. |

**Bildwerkzeuge (nach dem Einfügen eines Bildes):** Nach **[[en:Insert image]]** können Sie über
**[[en:Image text alternative]]** einen Alternativtext hinterlegen und über **[[en:Toggle caption]]**
eine Bildunterschrift ein- oder ausblenden. Zusätzlich stehen die Platzierungsvarianten
**[[en:In line]]**, **[[en:Wrap text]]** und **[[en:Break text]]** zur Verfügung, mit denen das Bild
im Text bzw. neben dem Text positioniert wird.

**Tabellenwerkzeuge (nach dem Einfügen einer Tabelle):** Über **[[en:Column]]** bearbeiten Sie
Spalten, über **[[en:Row]]** Zeilen und über **[[en:Merge cells]]** verbinden Sie ausgewählte
Zellen zu einer.

### HTML-Quelltext ansehen und bearbeiten

Der großflächige Editor bietet zusätzlich eine Schaltfläche am Ende der Symbolleiste, mit der Sie
zwischen der gerenderten Ansicht und dem **HTML-Quelltext** umschalten. Damit lassen sich
unerwünschte Formatierungen (z. B. aus eingefügten Inhalten) direkt im Quelltext korrigieren.

| Zustand | Erläuterung |
|---------|-------------|
| Gerenderte Ansicht (Standard) | Der Editor zeigt den formatierten Text an. Wenn Sie die Schaltfläche **[[en:Show HTML (edit raw)]]** betätigen, wechselt der Editor in die Quelltextansicht. |
| Quelltextansicht | Wenn Sie umgeschaltet haben, sehen und bearbeiten Sie das rohe HTML in einem Textbereich; das eignet sich für gezielte Korrekturen am Markup. Über **[[en:Show rendered]]** kehren Sie zur gerenderten Ansicht zurück, wobei Ihre Quelltextänderungen in die formatierte Darstellung übernommen werden. |

### Schreibgeschützte und vergrößerte Darstellung

| Verhalten | Erläuterung |
|-----------|-------------|
| Schreibgeschützter Modus | Wenn die aufrufende Seite das Feld schreibgeschützt setzt, blendet der Editor die Symbolleiste aus und lässt nur das Lesen zu; so erkennen Sie sofort, dass der Datensatz in seinem aktuellen Status nicht bearbeitet werden darf. |
| Symbolleiste ausblenden | Wenn die aufrufende Seite die Symbolleiste ausblendet, wird der Inhalt ohne Formatierungswerkzeuge angezeigt; der Text bleibt lesbar, ist aber nicht über die Leiste formatierbar. |
| Vergrößerte Ansicht | Wenn die vergrößerte Darstellung aktiv ist, füllt der Editor den verfügbaren Bereich vollständig aus; dadurch steht beim Bearbeiten langer Texte mehr Platz zur Verfügung. |

## Faktenbox-Editor

Neben dem großflächigen Editor stellt das Modul eine kompakte Variante für die **Faktenbox** am
Seitenrand bereit. Sie eignet sich, um Langtexte begleitend zu einem Beleg oder Datensatz
anzuzeigen und zu pflegen, ohne die Hauptansicht zu verlassen.

Der Faktenbox-Editor verhält sich weitgehend wie der große Editor — er lädt den Feldinhalt, bietet
dieselbe Formatierungs-Symbolleiste (**[[en:Bold]]**, **[[en:Font Size]]**, **[[en:Insert table]]**
usw.), unterstützt automatisches Speichern und kann schreibgeschützt geschaltet werden. Zwei
Unterschiede sind zu beachten:

- Der Faktenbox-Editor wird in **geringerer Höhe** dargestellt, passend für die schmalere
  Faktenbox-Spalte.
- Die Umschaltung in den **HTML-Quelltext** (Schaltfläche **[[en:Show HTML (edit raw)]]**) steht in
  der Faktenbox-Variante **nicht** zur Verfügung; für Quelltextkorrekturen nutzen Sie den
  großflächigen Editor.

## Typische Anwendungsfälle

### Langtext formatiert erfassen

**Auslöser:** Ein Sachbearbeiter erhält den Auftrag, zu einem Datensatz einen aussagekräftigen,
gegliederten Langtext zu hinterlegen — etwa als interne Notiz oder als Belegtext, der später gedruckt
oder versendet wird.

**Einstieg in BC:** Der Anwender öffnet die betreffende Seite mit dem Langtextfeld; dort erscheint der
HTML-Editor mit seiner Symbolleiste.

**Kernablauf:**

1. In den Bearbeitungsbereich klicken und den Text eingeben.
2. Wichtige Passagen mit **[[en:Bold]]** hervorheben, Aufzählungen über **[[en:Bulleted List]]**
   strukturieren und bei Bedarf eine Übersicht über **[[en:Insert table]]** einfügen.
3. Farbliche Hervorhebungen über **[[en:Font Color]]** oder **[[en:Font Background Color]]** setzen.
4. Der Editor speichert die Änderungen automatisch; beim Schließen der Seite wird der Inhalt in das
   Feld übernommen.

**Abschluss:** Der formatierte HTML-Inhalt ist im Feld gespeichert und steht der weiterverarbeitenden
Funktion (z. B. Anzeige, Druck) auf der aufrufenden Seite zur Verfügung.

### Eingefügten Inhalt über den Quelltext bereinigen

**Auslöser:** Ein Anwender kopiert Text aus einer anderen Anwendung in das Langtextfeld und stellt
fest, dass dabei unerwünschte Formatierungen übernommen wurden.

**Einstieg in BC:** Der Anwender arbeitet im großflächigen HTML-Editor der betreffenden Seite.

**Kernablauf:**

1. Zunächst über **[[en:Remove Format]]** die Zeichenformatierung des markierten Bereichs entfernen.
2. Reichen die verbleibenden Auszeichnungen (z. B. Absätze, Tabellen) noch nicht aus, über die
   Schaltfläche **[[en:Show HTML (edit raw)]]** in die Quelltextansicht wechseln.
3. Im Quelltext die störenden HTML-Elemente entfernen oder korrigieren.
4. Über **[[en:Show rendered]]** zurück in die gerenderte Ansicht wechseln; die Korrekturen werden
   übernommen.

**Abschluss:** Der bereinigte Text wird automatisch gespeichert und beim Schließen der Seite in das
Feld festgeschrieben. In der Faktenbox-Variante steht die Quelltextansicht nicht zur Verfügung;
dieser Fall wird daher im großflächigen Editor bearbeitet.

## FAQ und Troubleshooting

### Warum sehe ich keine Symbolleiste, sondern nur den Text?

Das Feld wird schreibgeschützt angezeigt. Der Editor blendet in diesem Fall die Symbolleiste aus und
lässt nur das Lesen zu. Ob ein Feld bearbeitbar ist, richtet sich nach dem Status des Datensatzes auf
der aufrufenden Seite — nicht nach dem Editor selbst.

### Muss ich meine Änderungen manuell speichern?

Nein. Der Editor übernimmt Ihre Eingaben mit automatischem Speichern kurz nach der letzten Änderung.
Zusätzlich wird der Inhalt festgeschrieben, wenn die aufrufende Seite eine Speicherung anfordert oder
Sie die Seite schließen.

### Warum stehen mir die Editor-Funktionen gar nicht zur Verfügung?

Möglicherweise fehlt die Lizenz oder die Berechtigung. Das Modul prüft bei jeder Anmeldung die Lizenz
der m+m-Produktlinie; ist keine gültige Lizenz vorhanden, arbeitet der Editor nicht wie erwartet.
Zudem benötigen Sie den Berechtigungssatz **[[en:All permissions]]**. Wenden Sie sich in diesem Fall
an Ihren Administrator.

### Welche Basis-App wird benötigt?

Der m+m HTML Editor setzt die App **m+m Cloud Base** voraus. Ohne diese Basis lässt sich das Modul
nicht installieren; die Basis wird daher zuerst bereitgestellt.

### Wie füge ich ein Bild in den Text ein?

Nutzen Sie **[[en:Insert image]]** in der Symbolleiste. Danach können Sie über
**[[en:Image text alternative]]** einen Alternativtext und über **[[en:Toggle caption]]** eine
Bildunterschrift hinzufügen sowie das Bild im oder neben dem Text positionieren.

### Wie erstelle ich eine Tabelle und bearbeite sie?

Fügen Sie über **[[en:Insert table]]** eine Tabelle ein. Anschließend bearbeiten Sie über
**[[en:Column]]** die Spalten, über **[[en:Row]]** die Zeilen und verbinden Zellen über
**[[en:Merge cells]]**.

### Wie entferne ich eine versehentliche Formatierung?

Markieren Sie den betroffenen Text und wählen Sie **[[en:Remove Format]]**. Damit werden die
Zeichenformatierungen entfernt und der Text auf die Grunddarstellung zurückgesetzt. Für Korrekturen
am zugrunde liegenden HTML nutzen Sie zusätzlich die Quelltextansicht.

### Wie kann ich das rohe HTML sehen und korrigieren?

Im großflächigen Editor betätigen Sie am Ende der Symbolleiste **[[en:Show HTML (edit raw)]]**, um in
die Quelltextansicht zu wechseln. Nach der Korrektur kehren Sie über **[[en:Show rendered]]** zur
formatierten Ansicht zurück. In der Faktenbox-Variante ist diese Umschaltung nicht verfügbar.

### Warum fehlt der HTML-Quelltext-Umschalter in der Faktenbox?

Die Faktenbox-Variante des Editors bietet die Umschaltung in den HTML-Quelltext bewusst nicht an; sie
ist auf die kompakte Darstellung ausgelegt. Verwenden Sie für Quelltextarbeiten den großflächigen
Editor auf der Hauptseite.

### Warum nutzt der Editor eine geringere Höhe in der Faktenbox?

Die Faktenbox-Variante ist für die schmalere Faktenbox-Spalte am Seitenrand ausgelegt und wird daher
in geringerer Höhe dargestellt. Für längere Texte mit viel Bearbeitungsfläche verwenden Sie den
großflächigen Editor bzw. die vergrößerte Ansicht.
