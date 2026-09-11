---
title: Anwenderhandbuch m+m Ext. Text Module with Report Dispatch
---

# Anwenderhandbuch m+m Ext. Text Module with Report Dispatch

## Einleitung

Das Modul **m+m Ext. Text Module with Report Dispatch** verbindet zwei bestehende m+m-Module
miteinander: das **erweiterte Textmodul** (Platzhalterverwaltung) und den **Belegversand**
(E-Mail- und Anhangsversand). Es stellt keine eigenen Seiten bereit, sondern ergänzt die vorhandene
Platzhalterverwaltung um zwei neue **Systemprozeduren** — **Anhänge** und **Anhangsliste** — und
sorgt dafür, dass diese Platzhalter beim E-Mail-Versand über den Belegversand automatisch durch die
Namen der tatsächlich angehängten Dateien ersetzt werden.

Der Nutzen für den Anwender: Wenn eine E-Mail über ein **m+m Belegversandprofile** verschickt wird,
kann im **Betreff** oder im **Nachrichtentext** ein Platzhalter stehen, der zum Sendezeitpunkt durch
die konkrete Liste der Anhänge ersetzt wird. Der Empfänger sieht damit direkt in der E-Mail, welche
Dateien beigefügt sind — bei Bedarf sogar als aufbereitete Liste mit der jeweiligen Dateigröße.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender**, die im Tagesgeschäft Belege per
E-Mail versenden (Vertriebs- und Einkaufssachbearbeitung, die über **Drucken/senden** arbeitet).
Sekundäre Zielgruppe sind **Administratoren bzw. Key-User**, die einmalig die Platzhalter und die
Startzeichen/Endzeichen der Platzhalter einrichten.

**Kurzer Prozessüberblick.** Der Ablauf gliedert sich in drei Abschnitte, die in dieser Reihenfolge
aufeinander aufbauen:

1. **Einrichtung** — der Administrator legt in den **Erweiterte Texteinstellungen** die
   **Platzhalter Startzeichen** und **Platzhalter Endzeichen** fest und definiert in der **Liste der
   Platzhalter** einen Platzhalter mit der Systemprozedur **Anhänge** oder **Anhangsliste**.
2. **Anwendung** — der Anwender fügt diesen Platzhalter in den E-Mail-Text ein (bzw. in eine
   Textvorlage, die als E-Mail-Text genutzt wird) und versendet den Beleg über ein **m+m
   Belegversandprofile** mit der **Art** **E-Mail**.
3. **Ergebnis** — beim Senden ersetzt das Modul den Platzhalter durch die Namen der Anhänge.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg vom leeren Zustand bis zur fertigen E-Mail, in der die
Anhänge automatisch benannt werden. Die Einrichtung ist Voraussetzung und steht daher zuerst.

1. **Startzeichen und Endzeichen prüfen.** Öffnen Sie über **Suchen** die Seite **Erweiterte
   Texteinstellungen** und stellen Sie sicher, dass **Platzhalter Startzeichen** und **Platzhalter
   Endzeichen** gefüllt sind (z. B. `{` und `}`). Ohne diese beiden Zeichen findet keine Ersetzung
   statt.
2. **Platzhalter anlegen.** Öffnen Sie in den **Erweiterte Texteinstellungen** über die Aktion
   **Platzhalter** die Seite **Liste der Platzhalter**. Legen Sie eine neue Zeile an, tragen Sie im
   Feld **Platzhalter** einen sprechenden Namen ein (z. B. `Anhaenge`) und wählen Sie in der Spalte
   **Systemprozeduren** den Wert **Anhänge** oder **Anhangsliste**.
3. **Platzhalter in den E-Mail-Text einfügen.** Schreiben Sie den Platzhalter — eingerahmt von
   Startzeichen und Endzeichen (z. B. `{Anhaenge}`) — in den **Betreff** oder den **Nachrichtentext**
   der E-Mail bzw. in die genutzte Textvorlage.
4. **Belegversandprofil vorbereiten.** Legen Sie über **Suchen** in **m+m Belegversandprofile** (oder
   über die Debitoren-/Kreditorenkarte, Aktion **m+m Belegversandprofile**) ein Profil mit **Art** =
   **E-Mail** und der passenden **Belegart** an. Über **Anzahl Anhänge** hinterlegen Sie die
   zusätzlichen Dateien.
5. **Beleg versenden.** Rufen Sie den Beleg auf und starten Sie **Drucken/senden**. Beim Erzeugen der
   E-Mail ersetzt das Modul den Platzhalter durch die Namen der Anhänge; kontrollieren Sie Betreff
   und Nachrichtentext vor dem Absenden.

## Einrichtung

Die Einrichtung erfolgt in „Microsoft Dynamics 365 Business Central“. Sie besteht aus zwei
aufeinander aufbauenden Schritten: dem Festlegen der Platzhalterzeichen auf der zentralen Setup-Seite
und dem Anlegen der eigentlichen Platzhalter. Da das Modul selbst keine eigene Einrichtungsseite
mitbringt, verwenden Sie die Seiten des erweiterten Textmoduls; die beiden neuen Werte **Anhänge**
und **Anhangsliste** erscheinen dort automatisch, sobald dieses Modul installiert ist.

### Erweiterte Texteinstellungen

**Prozessintro.** Die **Erweiterte Texteinstellungen** sind eine unternehmensweite Einrichtung
(genau ein Datensatz je Mandant). Sie werden vom Administrator einmalig vor der ersten Nutzung
gepflegt. Für dieses Modul sind vor allem die Felder **Platzhalter Startzeichen** und **Platzhalter
Endzeichen** entscheidend, denn sie definieren, an welchen Zeichen das Modul einen Platzhalter im
Text erkennt. Die übrigen Felder steuern das erweiterte Textmodul insgesamt und werden hier
vollständig beschrieben, weil der Anwender genau diese eine Seite vor sich sieht.

**Einstieg:** Öffnen Sie die Seite über **Suchen** und den Seitentitel **Erweiterte
Texteinstellungen** (unternehmensweite Einrichtung ohne übergeordnete Liste).

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Vorlagennummern** | Wenn Sie hier eine Nummernserie hinterlegen, dann werden neue Textvorlagen automatisch mit einer Nummer aus dieser Serie versehen; ohne Eintrag müssen Nummern manuell vergeben werden. |
| **Sprachcode** | Wenn Sie einen Sprachcode setzen, dann werden Texte in der zugehörigen Sprache erzeugt bzw. bevorzugt; ohne Eintrag greift die Standardsprache des Mandanten. |
| **Platzhalter Startzeichen** | Legt das einleitende Zeichen eines Platzhalters fest (Länge 1). Wenn dieses Zeichen leer ist, dann findet **keine** Platzhalterersetzung statt — auch die Systemprozeduren **Anhänge** und **Anhangsliste** werden dann nicht aufgelöst. |
| **Platzhalter Endzeichen** | Legt das abschließende Zeichen eines Platzhalters fest (Länge 1). Wenn dieses Zeichen leer ist, dann werden Platzhalter nicht erkannt und nicht ersetzt. Erst wenn Start- **und** Endzeichen gefüllt sind, ersetzt das Modul einen Text der Form Startzeichen + Platzhaltername + Endzeichen. |
| **E-Mail Platzhalter** | Steuert, wann Platzhalter in E-Mail-Texten verarbeitet werden. **(leer):** keine automatische E-Mail-Platzhalterverarbeitung. **Beim Senden:** Wenn gesetzt, dann werden Platzhalter beim Senden der E-Mail ersetzt, der gespeicherte Text bleibt unverändert. **Beim Senden ersetzen und speichern:** Wenn gesetzt, dann wird der ersetzte Text zusätzlich am Beleg gespeichert. |
| **E-Mail-Text bevorzugen** | Bestimmt, welcher Text als E-Mail-Text herangezogen wird. **E-Mail-Text verwenden:** Wenn gesetzt, dann wird der reguläre E-Mail-Text verwendet. **Factbox-Text anstelle von E-Mail-Text verwenden:** Wenn gesetzt, dann wird der Infobox-Text der erweiterten Texte als E-Mail-Text herangezogen. |
| **Vorschautexte in Herkunftsbelegen** | Wenn aktiviert, dann werden die erweiterten Texte bereits im Herkunftsbeleg als Vorschau angezeigt, sodass der Anwender das Ergebnis vor dem Buchen bzw. Versand sieht. |
| **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** | Wenn aktiviert, dann werden Infobox-Texte auch dann im Bericht gedruckt, wenn kein Druck-Untertyp gesetzt ist; andernfalls bleiben diese Texte auf den Bericht ohne Untertyp beschränkt. |
| **Text kopieren** (Gruppe **Dokumente kopieren**) | Wenn aktiviert, dann werden erweiterte Texte beim Kopieren eines Belegs mit in den Zielbeleg übernommen; andernfalls beginnt der Zielbeleg ohne diese Texte. |
| **Ext.Text bei Buchungsroutinen automatisch zuweisen** | Wenn aktiviert, dann werden erweiterte Texte während der Buchung automatisch dem gebuchten Beleg zugeordnet, ohne dass der Anwender manuell eingreifen muss. |
| **Arbeitsgangtext an Bestellung übertragen** | Wenn aktiviert, dann wird der Arbeitsgangtext beim Erzeugen einer Bestellung an diese übertragen; andernfalls bleibt der Text auf dem Ursprungsbeleg. |
| **FA-Texte beim Statuswechsel übernehmen** | Wenn aktiviert, dann werden Fertigungsauftragstexte beim Statuswechsel automatisch übernommen; andernfalls müssen sie erneut zugeordnet werden. |

> Hinweis: Die Gruppe **Hintergrundaufgaben** (Erstellen von Kopf- und Zeilentexten im Hintergrund
> für Einkauf und Verkauf) ist in der Standardansicht ausgeblendet und für den täglichen Umgang mit
> diesem Modul nicht relevant; sie wird daher hier nicht als Bedienfeld aufgeführt.

### Platzhalter für Anhänge einrichten

**Prozessintro.** Damit die E-Mail beim Versand die Anhangsnamen anzeigt, muss der Administrator
einen Platzhalter anlegen und ihm die richtige Systemprozedur zuweisen. Wer konfiguriert: der
Administrator bzw. Key-User. Wann: einmalig vor der ersten Nutzung, nach dem Setzen der
Start-/Endzeichen. Wo wird es angewendet: im Tagesgeschäft beim Versand über ein **m+m
Belegversandprofile** (siehe **Tägliche Arbeit: Belege per E-Mail versenden**).

Führen Sie die Schritte in dieser Reihenfolge aus:

1. **Zeichen sicherstellen.** Prüfen Sie in den **Erweiterte Texteinstellungen**, dass **Platzhalter
   Startzeichen** und **Platzhalter Endzeichen** gefüllt sind. Wenn eines der beiden Zeichen leer
   ist, dann wird der Platzhalter später nicht ersetzt.
2. **Liste der Platzhalter öffnen.** Öffnen Sie in den **Erweiterte Texteinstellungen** über die
   Aktion **Platzhalter** die Seite **Liste der Platzhalter**.
3. **Platzhalter anlegen.** Legen Sie eine neue Zeile an und vergeben Sie im Feld **Platzhalter**
   einen Namen. Dieser Name ist der Text, den Sie später — eingerahmt von Start- und Endzeichen — in
   den E-Mail-Text schreiben.
4. **Systemprozedur wählen.** Setzen Sie die Spalte **Systemprozeduren** auf **Anhänge** (einfache
   Aufzählung der Dateinamen) oder auf **Anhangsliste** (aufbereitete Liste mit Dateigröße). Wenn Sie
   eine dieser beiden Systemprozeduren wählen, dann werden die Felder für Tabelle/Feld nicht
   benötigt; die Ersetzung liefert das Modul beim Versand.
5. **Operativer Abschluss.** Fügen Sie den Platzhalter in den E-Mail-Text ein und versenden Sie einen
   Beleg über **Drucken/senden** mit einem Belegversandprofil der **Art** **E-Mail** — siehe
   **Tägliche Arbeit: Belege per E-Mail versenden**.

## Stammdaten

### Liste der Platzhalter

**Prozessintro.** Die **Liste der Platzhalter** ist der zentrale Stammdatensatz des erweiterten
Textmoduls. Hier definiert der Administrator, welche Platzhalter im Text erlaubt sind und wodurch
sie ersetzt werden. Dieses Modul ergänzt die Auswahl der Spalte **Systemprozeduren** um die Werte
**Anhänge** und **Anhangsliste**. Die Liste wird über die Aktion **Platzhalter** aus den
**Erweiterte Texteinstellungen** geöffnet.

**Einstieg:** **Erweiterte Texteinstellungen** → Aktion **Platzhalter** → Seite **Liste der
Platzhalter**.

| Feld | Erläuterung |
|------|-------------|
| **Platzhalter** | Der Name des Platzhalters. Wenn Sie diesen Namen — eingerahmt von Start- und Endzeichen — in einen Text schreiben, dann ersetzt das Modul die Zeichenfolge durch den ermittelten Wert. Der Name ist Pflichtfeld. |
| **Systemprozeduren** | Bestimmt, wodurch der Platzhalter ersetzt wird. Werte: **(leer):** keine Systemprozedur — die Ersetzung richtet sich nach Tabelle/Feld bzw. Freitext. **Benutzer-ID:** Wenn gewählt, dann wird der Platzhalter durch die Benutzer-ID des angemeldeten Anwenders ersetzt. **Heute:** Wenn gewählt, dann wird das aktuelle Tagesdatum eingesetzt. **Arbeitsdatum:** Wenn gewählt, dann wird das in BC eingestellte Arbeitsdatum eingesetzt. **Aktuelle Zeit:** Wenn gewählt, dann wird die aktuelle Uhrzeit eingesetzt. **Anhänge:** Wenn gewählt, dann wird der Platzhalter beim E-Mail-Versand durch die durch Komma getrennten Namen aller Anhänge ersetzt. **Anhangsliste:** Wenn gewählt, dann wird der Platzhalter durch eine aufbereitete Liste der Anhänge ersetzt, in der zu jeder Datei zusätzlich die Größe in MB angezeigt wird. |
| **Tabellen-ID** | Wenn keine Systemprozedur gewählt ist, dann bestimmt dieses Feld die Quelltabelle, aus der der Ersetzungswert gelesen wird. Bei den Systemprozeduren **Anhänge** und **Anhangsliste** wird es nicht benötigt. |
| **Tabellenname** | Zeigt den Namen der über **Tabellen-ID** gewählten Tabelle an (nicht editierbar). |
| **Feld Nr.** | Wenn keine Systemprozedur gewählt ist, dann bestimmt dieses Feld die Feldnummer in der Quelltabelle, deren Wert eingesetzt wird. |
| **Feld Name** | Zeigt den Namen des über **Feld Nr.** gewählten Feldes an (nicht editierbar). |
| **Verwandte Tabelle** | Wenn eine Systemprozedur ungleich (leer) gewählt ist, dann kann hier eine verknüpfte Tabelle angegeben werden, deren Wert stattdessen herangezogen wird. |
| **Zugehöriges Tabellenfeld** | Bestimmt die Feldnummer in der verwandten Tabelle, deren Wert eingesetzt wird. |
| **Zugehöriges Feld Name** | Zeigt den Namen des zugehörigen Feldes an (nicht editierbar). |
| **Freitext** | Wenn Sie hier einen Text eintragen, dann wird der Platzhalter durch diesen festen Text ersetzt; die Angaben zu Tabelle, Feld und Bild werden dabei zurückgesetzt. |
| **Bild** | Wenn Sie ein Bild hinterlegen, dann wird der Platzhalter durch dieses Bild ersetzt (z. B. für Berichte). |
| **Größe ändern %** | Wenn Sie einen Prozentwert setzen, dann wird das hinterlegte Bild proportional skaliert (Wertebereich −99 bis 99). |
| **Höhe** | Wenn Sie einen Wert setzen, dann wird das Bild auf die angegebene Höhe skaliert. |
| **Breite** | Wenn Sie einen Wert setzen, dann wird das Bild auf die angegebene Breite skaliert. |
| **Bild** (Infobox) | Zeigt in der Infobox eine Vorschau des zum Platzhalter hinterlegten Bildes an. |

> Für dieses Modul sind ausschließlich die Werte **Anhänge** und **Anhangsliste** der Spalte
> **Systemprozeduren** relevant. Bei diesen beiden Werten liefert das Modul den Ersetzungstext beim
> Versand selbst; die Felder für Tabelle, Feld, Freitext und Bild bleiben leer.

## Tägliche Arbeit: Belege per E-Mail versenden

**Setup-Bezug (Bridge-Absatz).** Der tägliche Ablauf wird durch zwei Einrichtungsbereiche gesteuert:
durch die **Erweiterte Texteinstellungen** und die **Liste der Platzhalter** (welcher Platzhalter
existiert und dass Start-/Endzeichen gesetzt sind) sowie durch das **m+m Belegversandprofile** des
Belegversands (ob überhaupt per **E-Mail** versendet und ob und wie **gezippt** wird). Ist die
Einrichtung wie unter **Einrichtung** und **Stammdaten** beschrieben erfolgt, muss der Anwender im
Tagesgeschäft nur noch den Platzhalter in den Text einfügen und den Beleg versenden.

**Ablauf.** Das Modul greift nicht als Schaltfläche in die Oberfläche ein, sondern arbeitet
automatisch im Moment des E-Mail-Versands. Der Ablauf ist:

1. Der Anwender ruft den Beleg auf (z. B. **Verkaufsauftrag** oder einen gebuchten Beleg) und startet
   den Versand über **Drucken/senden**. Voraussetzung ist ein passendes **m+m Belegversandprofile**
   mit der **Art** **E-Mail** oder **Drucken und E-Mail**.
2. Der Belegversand erstellt die E-Mail, hängt Beleg und zusätzliche Dateien an und bildet — je nach
   **ZIP-Option** (**Alle**, **Nur Anhänge** oder ohne ZIP) — gegebenenfalls einen ZIP-Ordner.
3. Unmittelbar vor dem Senden verarbeitet dieses Modul den E-Mail-Betreff und den Nachrichtentext:
   Es sammelt die Namen aller Anhänge. Handelt es sich um einen ZIP-Anhang, werden zusätzlich die
   Namen der Dateien **innerhalb** des ZIP-Ordners ermittelt.
4. Jeder Platzhalter mit der Systemprozedur **Anhänge** wird durch die durch Komma getrennte Liste
   der Dateinamen ersetzt. Jeder Platzhalter mit der Systemprozedur **Anhangsliste** wird durch eine
   HTML-Aufzählung ersetzt, in der zu jeder Datei — sofern größer als 0 MB — die auf zwei
   Nachkommastellen gerundete Größe in MB in Klammern angezeigt wird.
5. Der Belegversand versendet die E-Mail mit dem so aufbereiteten Betreff und Nachrichtentext. Vor
   dem Absenden kann der Anwender Empfänger, **Betreff**, **Nachrichtentext** und Anhänge noch prüfen
   und manuell anpassen.

> Voraussetzung für die Ersetzung: In den **Erweiterte Texteinstellungen** müssen **Platzhalter
> Startzeichen** und **Platzhalter Endzeichen** gefüllt sein. Sind sie leer, versendet der
> Belegversand die E-Mail unverändert — der Platzhalter bliebe als Text stehen.

### Anhänge und Anhangsliste im Vergleich

Beide Systemprozeduren beziehen sich auf dieselben Anhänge, unterscheiden sich aber in der
Darstellung im E-Mail-Text:

| Systemprozedur | Ergebnis im Text |
|----------------|------------------|
| **Anhänge** | Eine einzeilige, durch Komma getrennte Aufzählung der Dateinamen (z. B. `Angebot.pdf, AGB.pdf`). Geeignet für den **Betreff** oder einen kurzen Satz im **Nachrichtentext**. |
| **Anhangsliste** | Eine formatierte Aufzählung (HTML-Liste). Zu jeder Datei größer als 0 MB wird zusätzlich die Größe in MB angezeigt (z. B. `AGB.pdf (0,12 MB)`); Dateien ohne ermittelbare Größe erscheinen ohne MB-Angabe. Geeignet für den **Nachrichtentext**, wenn der Empfänger die Anhänge übersichtlich aufgelistet sehen soll. |

## Typische Anwendungsfälle

### Anwendungsfall 1: Anhänge im E-Mail-Text benennen

- **Auslöser.** Eine Sachbearbeiterin verschickt eine Auftragsbestätigung, der neben dem Beleg noch
  die allgemeinen Geschäftsbedingungen als zusätzliche Datei beiliegen. Der Empfänger soll bereits
  im E-Mail-Text sehen, welche Dateien angehängt sind.
- **Vorbereitung (einmalig).** In den **Erweiterte Texteinstellungen** sind **Platzhalter
  Startzeichen** und **Platzhalter Endzeichen** gesetzt. In der **Liste der Platzhalter** existiert
  ein Platzhalter (z. B. `Anhaenge`) mit **Systemprozeduren** = **Anhänge**. Der Platzhalter
  `{Anhaenge}` steht im Nachrichtentext bzw. in der genutzten Textvorlage.
- **Einstieg in BC.** Die Sachbearbeiterin öffnet den **Verkaufsauftrag** und wählt **Drucken/senden**.
  Das zugehörige **m+m Belegversandprofile** hat die **Art** **E-Mail** und die passende **Belegart**;
  über **Anzahl Anhänge** ist die zusätzliche Datei hinterlegt.
- **Kernablauf.** Beim Erstellen der E-Mail ersetzt das Modul `{Anhaenge}` durch die Dateinamen der
  Anhänge (Beleg und zusätzliche Datei). Die Sachbearbeiterin kontrolliert Betreff und
  Nachrichtentext.
- **Abschluss.** Die E-Mail wird versendet; der Nachrichtentext nennt die angehängten Dateien
  namentlich.

### Anwendungsfall 2: Anhangsliste mit Größenangabe bei ZIP-Versand

- **Auslöser.** Für einen Kunden werden regelmäßig mehrere Dateien gebündelt versendet. Damit die
  E-Mail nicht zu groß wird, sollen die Anhänge als ZIP-Ordner verschickt werden, und der Empfänger
  soll im Text sehen, was er erhält.
- **Vorbereitung (einmalig).** In der **Liste der Platzhalter** existiert ein Platzhalter (z. B.
  `Anhangsliste`) mit **Systemprozeduren** = **Anhangsliste**. Der Platzhalter steht im
  Nachrichtentext. Das **m+m Belegversandprofile** hat **Art** = **E-Mail** und **ZIP-Option** =
  **Alle**; optional begrenzt **Max. MB** die Gesamtgröße.
- **Einstieg in BC.** Der Anwender ruft den Beleg auf und startet **Drucken/senden**.
- **Kernablauf.** Der Belegversand packt die Anhänge gemäß **ZIP-Option** in einen ZIP-Ordner. Das
  Modul liest die Namen der Dateien innerhalb des ZIP-Ordners und ersetzt den Platzhalter durch eine
  aufbereitete Liste, in der zu jeder Datei größer als 0 MB die Größe in MB steht.
- **Abschluss.** Die E-Mail wird mit dem ZIP-Anhang und der lesbaren Anhangsliste im Nachrichtentext
  versendet.

## FAQ und Troubleshooting

### Warum wird mein Platzhalter im E-Mail-Text nicht ersetzt?

Wahrscheinlich fehlen die Platzhalterzeichen. Prüfen Sie in den **Erweiterte Texteinstellungen**, ob
**Platzhalter Startzeichen** und **Platzhalter Endzeichen** gefüllt sind. Ist eines der beiden Zeichen
leer, verarbeitet das Modul keinen Platzhalter und der Text bleibt unverändert.

### Wie muss ich den Platzhalter im Text schreiben?

Schreiben Sie den in der **Liste der Platzhalter** vergebenen Namen und rahmen Sie ihn genau mit dem
**Platzhalter Startzeichen** und dem **Platzhalter Endzeichen** ein (z. B. `{Anhaenge}`). Nur diese
exakte Zeichenfolge wird erkannt und ersetzt.

### Was ist der Unterschied zwischen Anhänge und Anhangsliste?

**Anhänge** ersetzt den Platzhalter durch eine einzeilige, durch Komma getrennte Aufzählung der
Dateinamen. **Anhangsliste** ersetzt ihn durch eine formatierte Aufzählung, in der zu jeder Datei
größer als 0 MB zusätzlich die Größe in MB angezeigt wird.

### Warum erscheint bei manchen Dateien keine MB-Angabe in der Anhangsliste?

Die Größe wird nur angezeigt, wenn sie größer als 0 MB ist. Ist die ermittelte Größe 0 (bzw. nicht
verfügbar), führt die **Anhangsliste** die Datei nur mit dem Namen und ohne Größenangabe auf.

### Funktioniert die Ersetzung auch im Betreff der E-Mail?

Ja. Das Modul verarbeitet sowohl den **Betreff** als auch den **Nachrichtentext**. Für den Betreff
eignet sich die Systemprozedur **Anhänge** (kompakte Aufzählung) besser als die **Anhangsliste**, die
für den Textkörper gedacht ist.

### Werden auch die Dateien innerhalb eines ZIP-Ordners aufgelistet?

Ja. Ist ein Anhang ein ZIP-Ordner, liest das Modul die Namen der darin enthaltenen Dateien und nimmt
diese in die Ersetzung auf. So sieht der Empfänger die einzelnen Dateien und nicht nur den Namen des
ZIP-Ordners.

### Muss ich zum Versenden eine besondere Schaltfläche des Moduls betätigen?

Nein. Das Modul arbeitet automatisch im Moment des E-Mail-Versands über den Belegversand. Sie
versenden den Beleg wie gewohnt über **Drucken/senden** mit einem **m+m Belegversandprofile** der
**Art** **E-Mail**; die Ersetzung geschieht im Hintergrund.

### Warum passiert nichts, obwohl ich einen Platzhalter angelegt habe?

Die Ersetzung greift nur beim **E-Mail-Versand**. Steht die **Art** des Belegversandprofils auf
**Drucken**, wird keine E-Mail erzeugt und der Platzhalter nicht verarbeitet. Wählen Sie **E-Mail**
oder **Drucken und E-Mail**.

### Wo lege ich fest, welche zusätzlichen Dateien überhaupt angehängt werden?

Die Anhänge selbst werden nicht in diesem Modul, sondern im **m+m Belegversandprofile** über
**Anzahl Anhänge** festgelegt. Das Modul benennt anschließend nur die Dateien, die der Belegversand
tatsächlich an die E-Mail gehängt hat.

### Kann ich den ersetzten Text vor dem Absenden noch kontrollieren?

Ja. Vor dem Versenden können Sie in der E-Mail Empfänger, **Betreff**, **Nachrichtentext** und
Anhänge prüfen und bei Bedarf manuell anpassen. Die Platzhalter sind zu diesem Zeitpunkt bereits
durch die Anhangsnamen ersetzt.
