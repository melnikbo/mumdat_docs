---
title: Anwenderhandbuch m+m PDF Merge
---

# Anwenderhandbuch m+m PDF Merge

## Einleitung

Die App **m+m PDF Merge** erweitert die **DropZone** von m+m innerhalb von Microsoft
Dynamics 365 Business Central um die Möglichkeit, mehrere in der DropZone abgelegte
PDF-Dokumente zu einem einzigen neuen PDF-Dokument zusammenzuführen. Das zusammengeführte
Dokument können Sie anschließend direkt herunterladen oder als neuen Beleg wieder in der
DropZone speichern. Optional lassen sich zusätzlich Standardberichte aus Business Central in
die Zusammenführung aufnehmen.

Da die App Bestandteil der m+m DropZone ist, steht sie überall dort zur Verfügung, wo Sie
auch auf die DropZone zugreifen können – also in Stammdaten- und Belegseiten, in denen die
DropZone als Infobox eingeblendet wird. Eine eigene Einrichtungs- oder Stammdatenpflege
benötigt die App nicht.

**Zielgruppe:** Primär richtet sich die App an **operative Anwenderinnen und Anwender**, die
im Tagesgeschäft Dokumente an Belegen und Stammdaten ablegen und diese zu einem gemeinsamen
PDF-Dokument zusammenstellen möchten (z. B. Auftragsbestätigung und Zeichnung in einem
Dokument). Administratorinnen und Administratoren sind nur insofern betroffen, als sie die
erforderlichen Berechtigungen vergeben (siehe **Voraussetzungen und Berechtigungen**).

**Kurzer Prozessüberblick:**

1. In der DropZone einer Seite die gewünschten PDF-Dateien markieren.
2. Über das Assist-Edit-Menü der DropZone die Aktion **PDF zusammenführen und anzeigen**
   oder **PDF zusammenführen und herunterladen** wählen.
3. Beim Anzeigen öffnet sich der **PDF Editor**; hier können optional weitere Berichte
   ergänzt und das Ergebnis über **Als neuen Beleg speichern** in der DropZone abgelegt
   werden.
4. Das zusammengeführte Dokument erscheint in der DropZone bzw. wird als Datei
   heruntergeladen.

## Schnellstart für Anwender

Voraussetzung: In der DropZone der aktuellen Seite liegen **mindestens zwei PDF-Dateien**.

1. Öffnen Sie die Seite (Stammsatz oder Beleg), auf der die DropZone als Infobox angezeigt
   wird. Unterhalb des DropZone-Bereichs sehen Sie die abgelegten Dateien mit ihrem
   **Dateiname**.
2. Markieren Sie die zusammenzuführenden Dateien. Nutzen Sie dazu im Assist-Edit-Menü die
   Standardfunktion **Weitere auswählen** und wählen Sie die gewünschten Zeilen aus.
3. Rufen Sie erneut das Assist-Edit-Menü auf und wählen Sie **PDF zusammenführen und
   anzeigen**. Es öffnet sich der **PDF Editor** mit der Vorschau des zusammengeführten
   Dokuments.
4. *(Optional)* Ergänzen Sie im PDF Editor über **Beleg hinzufügen** oder **Mehrere Berichte
   hinzufügen** zusätzliche Standardberichte (siehe **Berichte in die Zusammenführung
   aufnehmen**).
5. Wählen Sie **Als neuen Beleg speichern**, vergeben Sie in der **Belegdateieingabe** einen
   **Dateiname** und bestätigen Sie mit **OK**. Das zusammengeführte PDF wird in der DropZone
   abgelegt.

Wenn Sie das Dokument nur benötigen, ohne es in der DropZone zu speichern, wählen Sie in
Schritt 3 stattdessen **PDF zusammenführen und herunterladen**. Das zusammengeführte
Dokument wird dann direkt als Datei in Ihrem Browser heruntergeladen, ohne dass der PDF
Editor geöffnet wird.

## Voraussetzungen und Berechtigungen

Diese App enthält bewusst **keine** eigenen Einrichtungsseiten, Nummernserien oder
Stammdatentabellen. Sie setzt vollständig auf den vorhandenen Funktionen der m+m DropZone
auf. Bevor Anwender die Zusammenführung nutzen können, müssen die folgenden Voraussetzungen
erfüllt sein.

**Abhängige Module (Prerequisites):** m+m PDF Merge benötigt die m+m **DropZone**, den
m+m **Medienspeicher** (dort werden die abgelegten Dokumente gespeichert) sowie
m+m **Cloud Base**. Wenn diese Module installiert und lizenziert sind, erscheinen die
Aktionen der App automatisch in der DropZone-Infobox – eine gesonderte Aktivierung ist nicht
erforderlich.

**Ablage von Dokumenten:** Damit eine Zusammenführung möglich ist, müssen in der DropZone
bereits PDF-Dateien abgelegt sein. Das Ablegen erfolgt über die Standardfunktion der
DropZone (Dokumente per Drag-and-drop in den DropZone-Bereich ziehen); die abgelegten Dateien
werden im Medienspeicher gespeichert und unterhalb der DropZone mit ihrem **Dateiname**
aufgelistet. m+m PDF Merge verarbeitet dabei ausschließlich Dateien mit der Endung `.pdf`;
andere Dateitypen in der DropZone werden bei der Zusammenführung übergangen.

**Berechtigungen:** Für die Nutzung liefert die App den Berechtigungssatz
**All permissions** (m+m PDF Merge) mit. Dieser Satz umfasst die Ausführungsrechte für die
Seiten und den Verarbeitungscodeunit der App. Ordnen Sie den Berechtigungssatz den
Benutzergruppen zu, deren Mitglieder die Zusammenführung ausführen dürfen. Der Satz legt
fest, welche Anwender die App-Seiten (PDF Editor, Berichts-Lookup, Belegdateieingabe) öffnen
und die Zusammenführung ausführen können; darüber hinausgehende Rechte an den Dokumenten
selbst (Ablegen, Herunterladen, Löschen) werden über die Berechtigungen der DropZone bzw.
des Medienspeichers gesteuert.

## Arbeiten mit dem PDF-Merge in der DropZone

Der gesamte Ablauf beginnt in der **DropZone**-Infobox einer beliebigen Seite. Die App
ergänzt diese Infobox um eine PDF-Vorschau sowie um zwei Aktionen im Verarbeitungsmenü der
Infobox.

**Aktionen in der DropZone-Infobox:**

| Aktion | Erläuterung |
|---|---|
| **PDF zusammenführen und anzeigen** | Wenn Sie diese Aktion für die markierten Dateien wählen, werden alle markierten PDF-Dateien zu einem Dokument zusammengeführt und der **PDF Editor** wird als Dialog geöffnet. Dort sehen Sie die Vorschau des Ergebnisses und können weitere Berichte ergänzen sowie das Dokument speichern. Sind keine markierten PDF-Dateien vorhanden, erscheint der Hinweis „Sie müssen mindestens ein PDF-Dokument auswählen." |
| **PDF zusammenführen und herunterladen** | Wenn Sie diese Aktion wählen, werden die markierten PDF-Dateien im Hintergrund zusammengeführt und das Ergebnis wird sofort als Datei heruntergeladen, ohne dass der PDF Editor geöffnet wird. Nutzen Sie diese Aktion, wenn Sie das zusammengeführte Dokument nur außerhalb von Business Central benötigen und es **nicht** in der DropZone ablegen möchten. |
| **Datei herunterladen** | Standardaktion der DropZone: Wenn Sie eine einzelne Datei markieren und diese Aktion wählen, wird die markierte Datei unverändert heruntergeladen. Diese Aktion führt keine Zusammenführung durch. |

**Felder und Bereiche der Infobox:**

| Feld / Bereich | Erläuterung |
|---|---|
| **Dateiname** | Zeigt je abgelegtem Dokument den Namen der Datei an. Anhand der Endung `.pdf` erkennt die App, welche Dateien zusammengeführt werden können. Über dieses Listenfeld markieren Sie die Dateien für die Zusammenführung. |
| DropZone-Bereich | Der Ablagebereich der DropZone. Wenn Sie hier ein Dokument per Drag-and-drop ablegen, wird es im Medienspeicher gespeichert und anschließend in der Dateiliste angezeigt; erst danach steht es für die Zusammenführung zur Verfügung. |
| PDF-Vorschau | Wenn eine Zusammenführung erfolgt ist, zeigt dieser Bereich das erzeugte PDF-Dokument an. Solange keine Zusammenführung vorliegt, bleibt der Bereich leer. |

Nach der Auswahl von **PDF zusammenführen und anzeigen** öffnet sich der **PDF Editor**. In
diesem Dialog stehen Ihnen die folgenden Bereiche und Aktionen zur Verfügung.

**Bereiche und Felder im PDF Editor:**

| Feld / Bereich | Erläuterung |
|---|---|
| **PDF** (Vorschau) | Zeigt das aktuell zusammengeführte Dokument an. Jede weitere aufgenommene Datei bzw. jeder ergänzte Bericht wird an das bestehende Dokument angehängt und die Vorschau anschließend neu aufgebaut. |
| **Fehler** (Hinweisbereich) | Dieser Bereich wird nur eingeblendet, wenn beim Zusammenführen ein Problem auftritt. Wenn eine Datei nicht verarbeitet werden kann (z. B. ein verschlüsseltes PDF), erscheint hier der Hinweis „Es ist ein Fehler beim Verbinden der PDFs aufgetreten. Bitte Beleg überprüfen." – prüfen Sie in diesem Fall die betroffene Datei und starten Sie den Vorgang erneut. |

**Aktionen im PDF Editor:**

| Aktion | Erläuterung |
|---|---|
| **Beleg hinzufügen** | Wenn Sie diese Aktion wählen, öffnet sich der **Berichts-Lookup**. Nach Auswahl **eines** Berichts wird dessen Anfrageseite (Request Page) angezeigt; der fertig gedruckte Bericht wird anschließend als PDF an das zusammengeführte Dokument angehängt. |
| **Mehrere Berichte hinzufügen** | Wenn Sie diese Aktion wählen, öffnet sich ebenfalls der **Berichts-Lookup**, hier können Sie jedoch **mehrere** Berichte gleichzeitig markieren. Für jeden markierten Bericht wird eine Anfrageseite durchlaufen und das Ergebnis an das Dokument angehängt. |
| **Als neuen Beleg speichern** | Wenn Sie diese Aktion wählen, wird das aktuell in der Vorschau angezeigte, zusammengeführte PDF gespeichert. Zuvor werden Sie in der **Belegdateieingabe** nach einem **Dateiname** gefragt. Nach Bestätigung wird das Dokument als neuer Eintrag im Medienspeicher der aktuellen DropZone abgelegt und erscheint nach dem Schließen des PDF Editors in der Dateiliste der DropZone. |

### Berichte in die Zusammenführung aufnehmen

Zusätzlich zu den in der DropZone abgelegten PDF-Dateien können Sie im PDF Editor
**Standardberichte** aus Business Central in das zusammengeführte Dokument aufnehmen. Dies
ist hilfreich, wenn ein aktueller Beleg (z. B. eine Auftragsbestätigung) gemeinsam mit
bereits abgelegten Dokumenten in einem einzigen PDF ausgegeben werden soll.

So gehen Sie vor:

1. Öffnen Sie über **PDF zusammenführen und anzeigen** den PDF Editor.
2. Wählen Sie **Beleg hinzufügen** (ein Bericht) oder **Mehrere Berichte hinzufügen**
   (mehrere Berichte). Es öffnet sich der **Berichts-Lookup**.
3. Markieren Sie im Berichts-Lookup den bzw. die gewünschten Berichte und bestätigen Sie die
   Auswahl.
4. Füllen Sie die eingeblendete Anfrageseite (Request Page) je Bericht aus. Der Bericht wird
   danach als PDF erzeugt und an das zusammengeführte Dokument angehängt; die Vorschau wird
   aktualisiert.

Der **Berichts-Lookup** zeigt die auswählbaren Berichte in einer Liste an. Es werden nur
Berichte angeboten, die tatsächlich ausgegeben werden können (reine Verarbeitungsberichte
ohne Ausgabe werden ausgeblendet).

**Spalten im Berichts-Lookup:**

| Feld | Erläuterung |
|---|---|
| **ID** | Zeigt die Objektnummer des Berichts an. Anhand dieser Nummer wird der Bericht beim Zusammenführen aufgerufen. |
| **Name** | Zeigt den internen Namen des Berichtsobjekts an und hilft bei der eindeutigen Zuordnung, wenn mehrere Berichte ähnliche Bezeichnungen haben. |
| **Bezeichnung** | Zeigt die sprechende Bezeichnung des Berichts an, wie sie auch bei der normalen Berichtsausgabe erscheint. Nutzen Sie diese Spalte, um den fachlich passenden Bericht zu finden. |

### Zusammengeführtes PDF speichern

Möchten Sie das zusammengeführte Dokument dauerhaft in der DropZone behalten, speichern Sie
es als neuen Beleg. Dieser Schritt schließt den Zusammenführungsvorgang ab.

1. Wählen Sie im PDF Editor **Als neuen Beleg speichern**.
2. Es öffnet sich die **Belegdateieingabe**. Erfassen Sie im Feld **Dateiname** den
   gewünschten Namen für das zusammengeführte Dokument (ohne Endung – die Endung `.pdf` wird
   automatisch ergänzt).
3. Bestätigen Sie mit **OK**.

**Feld in der Belegdateieingabe:**

| Feld | Erläuterung |
|---|---|
| **Dateiname** | Wenn Sie hier einen Namen erfassen und mit **OK** bestätigen, wird das zusammengeführte PDF unter diesem Namen (ergänzt um `.pdf`) im Medienspeicher der aktuellen DropZone gespeichert. Lassen Sie das Feld leer und bestätigen Sie ohne Eingabe, erscheint der Hinweis „Der Dateiname muss angegeben werden." und es wird nichts gespeichert. |

Nach dem Speichern erscheint das neue Dokument in der Dateiliste der DropZone, sobald Sie
den PDF Editor geschlossen haben. Ist bislang kein Titelbild für die DropZone hinterlegt,
wird das gespeicherte Dokument automatisch als Titelbild (**Ist Bildtitel**) gekennzeichnet.

> **Technischer Hinweis (Verarbeitungsmodus):** Intern unterscheidet die App beim
> Zusammenführen, woher ein Dokument stammt. Der Modus **(leer)** bedeutet, dass keine
> automatische Zusammenführung angestoßen wird und die vorhandenen Dateien angehängt werden.
> Beim Modus **Beleg drucken** wird ein Business-Central-Bericht ausgegeben und das Ergebnis
> angehängt (dieser Modus greift bei **Beleg hinzufügen** / **Mehrere Berichte hinzufügen**).
> Beim Modus **URL** wird ein Dokument über eine Adresse geladen und angehängt. Diese
> Unterscheidung steuert die App automatisch; Sie müssen den Modus nicht manuell auswählen.

## Typische Anwendungsfälle (Nutzungsbeispiele)

### Auftragsbestätigung und Zeichnung als ein PDF an eine Kundin senden

**Auslöser:** Eine Kundin bittet per E-Mail um die Auftragsbestätigung zusammen mit der
technischen Zeichnung – möglichst in einem einzigen PDF-Dokument.

**Einstieg in BC:** Öffnen Sie den betreffenden Beleg (bzw. den Stammsatz), auf dem die
**DropZone** als Infobox eingeblendet ist. Sowohl die Auftragsbestätigung als auch die
Zeichnung liegen dort bereits als PDF-Dateien.

**Kernablauf:**

1. Markieren Sie in der DropZone die beiden PDF-Dateien (über **Weitere auswählen**).
2. Wählen Sie im Assist-Edit-Menü **PDF zusammenführen und anzeigen**. Der **PDF Editor**
   öffnet sich und zeigt beide Dokumente hintereinander in einem PDF an.
3. Prüfen Sie die Vorschau. Ist alles korrekt, wählen Sie **Als neuen Beleg speichern**.
4. Vergeben Sie in der **Belegdateieingabe** einen aussagekräftigen **Dateiname** und
   bestätigen Sie mit **OK**.

**Abschluss:** Das zusammengeführte Dokument liegt nun als neue Datei in der DropZone und
kann von dort mit **Datei herunterladen** heruntergeladen und der Kundin übermittelt werden.

### Mehrere Standardberichte und abgelegte Dokumente in einem Dokument bündeln

**Auslöser:** Für eine interne Zusammenstellung sollen mehrere Business-Central-Berichte
gemeinsam mit bereits abgelegten PDF-Dateien in einem Dokument gebündelt werden.

**Einstieg in BC:** Öffnen Sie die Seite mit der **DropZone**, in der die vorbereiteten
PDF-Dateien liegen.

**Kernablauf:**

1. Markieren Sie die vorhandenen PDF-Dateien und wählen Sie **PDF zusammenführen und
   anzeigen**.
2. Wählen Sie im **PDF Editor** die Aktion **Mehrere Berichte hinzufügen**.
3. Markieren Sie im **Berichts-Lookup** die benötigten Berichte und bestätigen Sie die
   Auswahl.
4. Durchlaufen Sie je Bericht die Anfrageseite. Die Berichte werden nacheinander an das
   Dokument angehängt; die Vorschau wird jeweils aktualisiert.
5. Wählen Sie **Als neuen Beleg speichern**, vergeben Sie einen **Dateiname** und bestätigen
   Sie mit **OK**.

**Abschluss:** Das gebündelte Dokument steht in der DropZone bereit. Wird es nur temporär
benötigt, können Sie in Schritt 1 alternativ **PDF zusammenführen und herunterladen** wählen
und auf das Speichern verzichten.

## FAQ und Troubleshooting

### 1. Warum erscheinen die Aktionen zum Zusammenführen nicht?

Die Aktionen **PDF zusammenführen und anzeigen** und **PDF zusammenführen und herunterladen**
gehören zur **DropZone**-Infobox. Sie erscheinen nur auf Seiten, auf denen die DropZone
eingeblendet ist, und nur, wenn die App m+m PDF Merge samt der abhängigen Module (DropZone,
Medienspeicher, m+m Cloud Base) installiert und lizenziert ist sowie der Berechtigungssatz
zugeordnet wurde.

### 2. Was passiert, wenn ich keine Datei markiert habe?

Wenn Sie **PDF zusammenführen und anzeigen** oder **PDF zusammenführen und herunterladen**
ohne markierte PDF-Datei ausführen, erscheint der Hinweis „Sie müssen mindestens ein
PDF-Dokument auswählen." Es wird kein Dokument erzeugt. Markieren Sie mindestens eine
PDF-Datei und wiederholen Sie den Vorgang.

### 3. Warum werden manche Dateien beim Zusammenführen nicht berücksichtigt?

Die App verarbeitet ausschließlich Dateien mit der Endung `.pdf`. Andere Dateitypen (z. B.
Bilder oder Office-Dokumente) in der DropZone werden beim Zusammenführen übergangen. Prüfen
Sie, ob die gewünschte Datei tatsächlich ein PDF-Dokument ist.

### 4. Was bedeutet der Hinweis „Es ist ein Fehler beim Verbinden der PDFs aufgetreten"?

Dieser Hinweis erscheint im Bereich **Fehler** des PDF Editors, wenn eine der Dateien nicht
zusammengeführt werden konnte – häufig bei **verschlüsselten** PDF-Dokumenten oder bei
beschädigten Dateien. Entfernen Sie die betroffene Datei aus der Auswahl bzw. legen Sie eine
unverschlüsselte Fassung in der DropZone ab und starten Sie den Vorgang erneut.

### 5. Wie speichere ich das Ergebnis dauerhaft in Business Central?

Öffnen Sie das Ergebnis über **PDF zusammenführen und anzeigen** und wählen Sie im PDF
Editor **Als neuen Beleg speichern**. Nach Eingabe eines **Dateiname** und Bestätigung mit
**OK** wird das zusammengeführte PDF im Medienspeicher der aktuellen DropZone abgelegt.

### 6. Warum muss ich einen Dateinamen eingeben?

Der Dateiname ist erforderlich, damit das Dokument eindeutig gespeichert werden kann. Lassen
Sie das Feld **Dateiname** leer, erscheint der Hinweis „Der Dateiname muss angegeben werden."
und es wird nichts gespeichert. Die Endung `.pdf` wird automatisch ergänzt.

### 7. Wie unterscheiden sich „anzeigen" und „herunterladen"?

Bei **PDF zusammenführen und anzeigen** öffnet sich der **PDF Editor** mit der Vorschau; dort
können Sie Berichte ergänzen und das Ergebnis in der DropZone speichern. Bei **PDF
zusammenführen und herunterladen** wird das Ergebnis ohne Editor sofort als Datei
heruntergeladen und **nicht** in der DropZone gespeichert.

### 8. Wo finde ich das zusammengeführte Dokument nach dem Speichern?

Das gespeicherte Dokument erscheint in der Dateiliste der DropZone, sobald Sie den PDF
Editor geschlossen haben. Von dort können Sie es wie jede andere abgelegte Datei über
**Datei herunterladen** herunterladen.

### 9. Kann ich zusätzlich zu den DropZone-Dateien Berichte aufnehmen?

Ja. Öffnen Sie den PDF Editor über **PDF zusammenführen und anzeigen** und wählen Sie
**Beleg hinzufügen** (ein Bericht) oder **Mehrere Berichte hinzufügen** (mehrere Berichte).
Die Auswahl erfolgt im **Berichts-Lookup**; je Bericht durchlaufen Sie eine Anfrageseite.

### 10. Warum wird mein gespeichertes Dokument als Titelbild markiert?

Wenn für die aktuelle DropZone noch **kein** Titelbild hinterlegt ist, kennzeichnet die App
das gerade gespeicherte Dokument automatisch als Titelbild (**Ist Bildtitel**). Existiert
bereits ein Titelbild, bleibt dieses unverändert und das neue Dokument wird ohne
Titelbild-Kennzeichnung abgelegt.
