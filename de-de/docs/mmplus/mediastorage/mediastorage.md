---
title: Anwenderhandbuch m+m Media Storage
---

# Anwenderhandbuch m+m Media Storage

## Einleitung

Die App **m+m Media Storage** legt fest, **wo** die in Business Central abgelegten medialen
Dateien (Bilder, PDF-Dokumente) tatsächlich gespeichert werden. Sie ist die **Speicherablage im
Hintergrund** für die m+m **DropZone**: Zieht ein Anwender eine Datei in eine DropZone – zum
Beispiel auf einer Artikelkarte –, so entsteht daraus ein Eintrag im **Medienspeicher**, den
diese App verwaltet. Media Storage entscheidet dabei, ob die Datei in der Datenbank oder in der
Cloud liegt, und stellt die Liste sowie die Download-Funktion für diese Dateien bereit.

Es stehen drei Ablageorte zur Auswahl (Feld **Speicherungsart**):

- **Datenbank** – die Datei wird direkt in der Datenbank von Business Central gespeichert
  (zentrale Ablage, keine weitere Einrichtung nötig).
- **Azure Blob Storage** – die Datei wird dezentral in der Microsoft Cloud in einem eigenen
  Azure-Speicherkonto abgelegt.
- **OneDrive** – die Datei wird über Microsoft Graph in OneDrive gespeichert.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender**, die im
Tagesgeschäft Dateien über die DropZone ablegen, in der **Medienspeicherliste** verwalten und
einzelne Dateien wieder herunterladen. Sekundär angesprochen sind **Administratoren**, die in
der **Medienspeicher-Einrichtung** den Ablageort und – bei Cloud-Nutzung – die Zugangsdaten
konfigurieren.

**Voraussetzungen:**

- Die App **m+m Media Storage** ist nur zusammen mit der m+m **DropZone**-App sinnvoll nutzbar;
  die DropZone erzeugt die Einträge, die der Medienspeicher aufnimmt.
- Media Storage setzt die Basis-App **m+m Cloud Base** voraus. Nach der Anmeldung prüft das Modul
  in Cloud-Umgebungen automatisch die Lizenz. Ist der Mandant oder Benutzer dem Modul nicht
  zugeordnet oder eine Zahlung überfällig, erhält der Anwender einen Hinweis; bei mehrfacher
  Überfälligkeit kann die App gesperrt werden. In On-Premises- und Sandbox-Umgebungen entfällt
  diese Prüfung.

Kurzer Prozessüberblick: **Speicherungsart wählen → (bei Cloud) Zugangsdaten hinterlegen und
Verbindung testen → Datei per DropZone ablegen → Eintrag in der Medienspeicherliste bearbeiten →
Datei bei Bedarf herunterladen**.

## Schnellstart für Anwender

Die folgenden Schritte führen in der von Business Central erzwungenen Reihenfolge zum Ergebnis –
zuerst die Einrichtung, dann die tägliche Nutzung.

1. **Ablageort festlegen.** Öffnen Sie über **Suchen** die Seite **Medienspeicher-Einrichtung**
   und setzen Sie im Bereich **Speicherort** das Feld **Speicherungsart** auf **Datenbank**,
   **Azure Blob Storage** oder **OneDrive**.
2. **Nur bei Azure Blob Storage:** Füllen Sie im Bereich **Azure Blob Storage** die Felder
   **Access Key**, **Storage Account** und **Storage Container** und wählen Sie anschließend die
   Aktion **Verbindung testen**.
3. **Nur bei OneDrive:** Füllen Sie im Bereich **OneDrive** die Felder **Anwendungs-ID
   (Client)**, **Geheimschlüssel**, **Verzeichnis-ID (Mandant)**, **E-Mail** sowie bei Bedarf
   **Delegierte Genehmigungen** und wählen Sie **Verbindung testen**.
4. **Datei ablegen.** Ziehen Sie im Tagesgeschäft eine Datei in die m+m DropZone des jeweiligen
   Belegs oder Stammsatzes (z. B. auf der Artikelkarte). Die Datei wird sofort im Medienspeicher
   gespeichert – je nach **Speicherungsart** in der Datenbank, im Azure Blob Storage oder in
   OneDrive.
5. **Datei wiederfinden.** Öffnen Sie über **Suchen** die **Medienspeicherliste**. Dort sehen Sie
   die abgelegte Datei mit **Code**, **Herkunftsart** und **Dateiname** wieder.
6. **Datei herunterladen.** Markieren Sie in der Datei-Übersicht **Medienspeicherdateien** den
   Eintrag und wählen Sie **Datei herunterladen**.

Die Speicherungsart und die Zugangsdaten sind Voraussetzung für die Schritte 4 bis 6; Details
dazu stehen im Kapitel **Einrichtung**.

## Einrichtung

Die gesamte Einrichtung des Moduls erfolgt auf einer einzigen Karte, der
**Medienspeicher-Einrichtung**. Sie ist ein unternehmensweiter Einzeldatensatz (ein Datensatz je
Mandant) und wird beim ersten Öffnen automatisch angelegt.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Medienspeicher-Einrichtung**
(Kategorie *Verwaltung*). Ein übergeordneter Aufruf über eine Stammdatenliste besteht nicht; die
DropZone-App kann die Einrichtung im Hintergrund vorbelegen, für die manuelle Pflege ist
**Suchen** der vorgesehene Einstieg.

**Wer richtet ein und wann:** Der Administrator legt die Speicherungsart **einmalig vor der
ersten Dateiablage** fest. Solange keine Cloud-Ablage gewählt ist, sind keine weiteren Angaben
nötig. Die hier gewählte **Speicherungsart** steuert unmittelbar, wohin jede über die DropZone
abgelegte Datei geschrieben wird (siehe Kapitel **Medienspeicherliste** und **Typische
Anwendungsfälle**).

### Speicherort

In diesem Bereich wird der grundsätzliche Ablageort gewählt. Er ist der einzige Pflichtwert der
Einrichtung und schaltet die weiteren Eingabebereiche frei.

| Einrichtung | Erläuterung |
|---|---|
| **Speicherungsart** | Legt fest, wohin jede neue Datei geschrieben wird. **Datenbank:** Wenn ausgewählt, wird die Datei direkt in der Business-Central-Datenbank gespeichert; es sind keine weiteren Zugangsdaten erforderlich, und die Datei ist ohne externe Dienste sofort verfügbar. **Azure Blob Storage:** Wenn ausgewählt, wird die Datei beim Ablegen in das hinterlegte Azure-Speicherkonto hochgeladen, das Feld **Im Blob Speicher** wird gesetzt und das datenbankinterne Bild entfernt; dadurch wird die Datenbank entlastet, es entstehen jedoch Kosten seitens Microsoft. **OneDrive:** Wenn ausgewählt, wird die Datei über Microsoft Graph in OneDrive abgelegt und das Feld **In OneDrive** gesetzt; die Ablage erfolgt im hinterlegten OneDrive-Konto. |

Hinweis zu **Herkunftsart** (Enum, Wert **(leer)**): Der Medienspeicher kennzeichnet jede Datei
mit einer Herkunftsart. In dieser App ist zunächst nur der Wert **(leer)** definiert; die
verwendenden Module (z. B. die DropZone auf Artikeln oder Belegen) erweitern diese Auswahl um
ihre eigenen Herkunftsarten. Für den Anwender bedeutet das: Die Herkunftsart zeigt an, aus
welchem Kontext eine Datei stammt, und wird automatisch beim Ablegen gesetzt.

### Azure Blob Storage einrichten

**Prozess:** Diese Einrichtung führt der Administrator durch, **bevor** erstmals mit der
Speicherungsart **Azure Blob Storage** gearbeitet wird. Sie verbindet Business Central mit einem
Azure-Speicherkonto, in das anschließend jede über die DropZone abgelegte Datei automatisch
hochgeladen wird (die eigentliche Ablage geschieht im Tagesgeschäft, siehe **Typische
Anwendungsfälle**). Der Eingabebereich ist nur bearbeitbar, wenn die **Speicherungsart** auf
**Azure Blob Storage** steht.

| Einrichtung | Erläuterung |
|---|---|
| **Access Key** | Wenn hinterlegt, authentifiziert sich Business Central mit diesem Schlüssel (Shared Key) am Speicherkonto; ohne gültigen Access Key schlägt jeder Upload-, Download- und Löschvorgang fehl und der Anwender erhält eine Fehlermeldung mit dem Hinweis, die Medienspeicher-Einrichtung zu prüfen. Das Feld wird maskiert angezeigt. |
| **Storage Account** | Wenn gesetzt, bestimmt dieser Wert das Ziel-Speicherkonto in Azure; die Eingabe wird automatisch in Kleinbuchstaben umgewandelt und bildet zusammen mit dem Container die Download-URL der Datei. |
| **Storage Container** | Wenn gesetzt, legt dieser Wert den Container innerhalb des Speicherkontos fest, in dem die Dateien liegen; die Eingabe wird automatisch in Kleinbuchstaben umgewandelt. Fehlt der Container, kann keine Verbindung aufgebaut werden. |

**Schritte in Abhängigkeitsreihenfolge:**

1. **Zuerst** setzen Sie im Bereich **Speicherort** die **Speicherungsart** auf **Azure Blob
   Storage** – dadurch werden die Felder im Bereich **Azure Blob Storage** bearbeitbar.
2. **Danach** tragen Sie **Access Key**, **Storage Account** und **Storage Container** aus Ihrem
   Azure-Portal ein.
3. **Schließlich** wählen Sie die Aktion **Verbindung testen**. Bei Erfolg meldet das System
   „Verbindung zum Azure Blob Storage erfolgreich hergestellt“; andernfalls prüfen Sie die
   Angaben und wiederholen den Test.

**Operativer Abschluss:** Sobald die Verbindung steht, wird jede weitere per DropZone abgelegte
Datei automatisch in den Container hochgeladen (Feld **Im Blob Speicher** = ja). Die tägliche
Nutzung ist im Kapitel **Medienspeicherliste** und im Anwendungsfall *Cloud-Ablage aktivieren*
beschrieben.

**Abhängigkeit:** Bei jedem Verbindungsaufbau werden **Storage Container**, **Access Key** und
**Storage Account** geprüft; fehlt einer der Werte, bricht der Vorgang mit einer Meldung ab.

### OneDrive-Speicher einrichten

**Prozess:** Diese Einrichtung ist eine eigenständige Alternative zum Azure Blob Storage und wird
vom Administrator durchgeführt, **bevor** erstmals mit der Speicherungsart **OneDrive**
gearbeitet wird. Sie hinterlegt eine registrierte Azure-Anwendung (App-Registrierung), über die
Business Central per OAuth 2.0 auf OneDrive zugreift. Der Eingabebereich ist nur bearbeitbar,
wenn die **Speicherungsart** auf **OneDrive** steht.

| Einrichtung | Erläuterung |
|---|---|
| **Anwendungs-ID (Client)** | Wenn gesetzt, identifiziert dieser Wert die registrierte Azure-Anwendung, mit der das Zugriffstoken angefordert wird; ohne gültige Anwendungs-ID kann kein Token abgerufen werden und Uploads nach OneDrive schlagen fehl. |
| **Geheimschlüssel** | Wenn hinterlegt, dient dieser Wert zusammen mit der Anwendungs-ID zur Anmeldung der Anwendung; ohne gültigen Geheimschlüssel scheitert die Tokenanforderung. Das Feld wird maskiert angezeigt. |
| **Verzeichnis-ID (Mandant)** | Wenn gesetzt, bestimmt dieser Wert den Azure-Mandanten, gegen den die Anmeldung erfolgt; die ID wird in die Login-URL eingesetzt, über die das Zugriffstoken bezogen wird. |
| **E-Mail** | Wenn gesetzt und **Delegierte Genehmigungen** nicht aktiviert ist, wird die Datei in das OneDrive des hier angegebenen Benutzerkontos hochgeladen (Ablagepfad des angegebenen Postfachs). |
| **Delegierte Genehmigungen** | Wenn aktiviert, wird die Datei in das OneDrive des angemeldeten Benutzers selbst hochgeladen (Pfad „…/me/drive“); wenn nicht aktiviert, wird stattdessen das unter **E-Mail** angegebene Konto verwendet. So steuern Sie, ob die Ablage im eigenen oder in einem zentralen OneDrive erfolgt. |

**Schritte in Abhängigkeitsreihenfolge:**

1. **Zuerst** setzen Sie im Bereich **Speicherort** die **Speicherungsart** auf **OneDrive** –
   dadurch werden die OneDrive-Felder bearbeitbar.
2. **Danach** tragen Sie **Anwendungs-ID (Client)**, **Geheimschlüssel** und **Verzeichnis-ID
   (Mandant)** aus der Azure-App-Registrierung ein.
3. **Anschließend** legen Sie über **Delegierte Genehmigungen** und ggf. **E-Mail** fest, in
   welches OneDrive abgelegt wird (eigenes Konto oder zentrales Postfach).
4. **Schließlich** wählen Sie die Aktion **Verbindung testen**. Bei Erfolg meldet das System
   „Erfolgreich mit Onedrive verbunden.“; andernfalls prüfen Sie die Angaben.

**Operativer Abschluss:** Nach erfolgreichem Test werden neu abgelegte Dateien nach OneDrive
hochgeladen (Feld **In OneDrive** = ja). Diese Einrichtung und die Azure-Blob-Storage-Einrichtung
schließen einander aus, da beide über dieselbe **Speicherungsart** gesteuert werden.

### Verbindung testen

Die Aktion **Verbindung testen** ist nur aktiv, wenn als **Speicherungsart** **Azure Blob
Storage** oder **OneDrive** gewählt ist. Sie prüft mit den hinterlegten Zugangsdaten, ob eine
Verbindung zum jeweiligen Dienst aufgebaut werden kann, und gibt eine Erfolgs- oder
Fehlermeldung aus, ohne Daten zu verändern. Bei der Speicherungsart **Datenbank** ist kein Test
erforderlich, da keine externe Verbindung besteht.

## Medienspeicherliste

Die **Medienspeicherliste** ist die zentrale Übersicht aller im Medienspeicher abgelegten
Dateien. Sie zeigt sowohl in der Datenbank als auch in der Cloud abgelegte Einträge und dient
dem Anwender zum Sichten und Verwalten der Dateien.

**Einstieg:** Öffnen Sie über **Suchen** die **Medienspeicherliste**. Sie ist außerdem als
Absprung aus dem Medienspeicher hinterlegt.

Die Einträge entstehen automatisch, wenn ein Anwender eine Datei in die DropZone eines Belegs
oder Stammsatzes zieht. Legt ein Anwender – wie im Beispiel des Artikels „EK1701595“ – ein Bild
in der DropZone ab, findet er dieses Bild anschließend in der Medienspeicherliste wieder.

| Feld | Erläuterung |
|---|---|
| **Lfd. Nr.** | Fortlaufende Nummer der Datei innerhalb desselben Herkunftskontexts. Wird beim Ablegen automatisch vergeben (die erste Datei zu einer Herkunft erhält 1, jede weitere die nächste Nummer) und ist nicht editierbar. |
| **Code** | Ordnet die Datei ihrem Herkunftsobjekt zu; wird beim Ablegen aus der DropZone übernommen. Anhand des Codes erkennt der Anwender, zu welchem Datensatz die Datei gehört. |
| **Herkunftsart** | Zeigt an, aus welchem Modul bzw. Kontext die Datei stammt. In dieser App ist nur der Wert **(leer)** definiert; verwendende Module ergänzen weitere Herkunftsarten. Wird beim Ablegen gesetzt. |
| **Dateiname** | Der ursprüngliche Name der abgelegten Datei (technisches Feld *Description*). Dient dem Anwender zur Identifikation der Datei in Liste und Download. |
| **Bild** | Vorschau bzw. Inhalt der Datei, solange sie in der Datenbank liegt. Bei Ablage in Azure Blob Storage wird dieses Feld nach dem Upload geleert, da die Datei dann extern liegt. |
| **Ist Bildtitel** | Wenn aktiviert, gilt diese Datei als Titelbild der Herkunft. Die **erste** zu einer Herkunft abgelegte Datei wird automatisch als Titelbild gesetzt; so weiß das verwendende Modul, welches Bild bevorzugt anzuzeigen ist. |
| **Position** | Sortierreihenfolge der Datei innerhalb der Herkunft. Steuert, in welcher Reihenfolge die Dateien angezeigt werden. |
| **Im Blob Speicher** | Wenn aktiviert (ja), liegt die Datei im Azure Blob Storage und nicht in der Datenbank; der Download erfolgt dann direkt aus der Cloud. Das Feld wird beim erfolgreichen Upload automatisch gesetzt und ist nicht editierbar. |
| **In OneDrive** | Wenn aktiviert (ja), liegt die Datei in OneDrive. Das Feld wird beim OneDrive-Upload gesetzt und ist nicht editierbar. |

**Löschen:** Löscht der Anwender einen Eintrag in der Medienspeicherliste, wird die zugehörige
Datei automatisch am jeweiligen Ablageort mitentfernt – bei **Im Blob Speicher** = ja aus dem
Azure Blob Storage, andernfalls aus der internen Medienablage der Datenbank. Es bleibt also keine
verwaiste Datei zurück.

**Herkunftsfelder (technischer Hintergrund):** Neben den sichtbaren Spalten führt der
Medienspeicher je Datei zusätzliche Herkunftsangaben – **Herkunftsunterart**, **Herkunftsnr.**
und **Herkunftszeilennr.** –, mit denen eine Datei eindeutig einem Beleg, einer Zeile oder einem
Stammsatz zugeordnet wird. Diese Werte setzt die DropZone beim Ablegen automatisch; der Anwender
muss sie nicht pflegen. Für Cloud-Ablagen speichert das System außerdem **Externe
Bild-URL-Referenz**, **Blob Storage Dateiname** und **Blob Speicher-Referenz** zur Wiederauffindung
der Datei.

## Medienspeicherdateien und Datei herunterladen

Die Datei-Übersicht **Medienspeicherdateien** ist ein eingebettetes Teilbild (Infobox), das neben
der DropZone die zu einem Datensatz abgelegten Dateien auflistet. Sie zeigt je Zeile den
**Dateiname** und stellt die Aktion **Datei herunterladen** bereit.

| Feld | Erläuterung |
|---|---|
| **Dateiname** | Name der abgelegten Datei; identifiziert den herunterzuladenden Eintrag. |

**Aktion Datei herunterladen:** Markieren Sie die gewünschte Zeile und wählen Sie **Datei
herunterladen**. Das System liefert die Datei aus dem korrekten Ablageort aus: Liegt die Datei im
Azure Blob Storage (**Im Blob Speicher** = ja), wird sie direkt aus der Cloud gelesen; andernfalls
wird sie aus der Datenbank bereitgestellt. Der Anwender erhält die Datei anschließend als
Download; PDF-Dateien werden dabei entsprechend benannt.

## Berechtigungen

Zum Modul gehört der Berechtigungssatz **m+m Media Storage** (interne Kennung „All permissions“).
Er legt fest, welche Aktionen ein Anwender im Medienspeicher ausführen darf, und bündelt die
Lese-, Schreib-, Änderungs- und Löschrechte auf die Tabellen **Medienspeicher** und
**Medienspeicher-Einrichtung** sowie die Ausführungsrechte auf die zugehörigen Seiten und
Verarbeitungslogiken. Weisen Sie diesen Berechtigungssatz allen Anwendern zu, die Dateien ablegen,
in der Medienspeicherliste verwalten oder herunterladen sollen; ohne diese Berechtigungen bleibt
der Medienspeicher für den Benutzer nicht bedienbar.

## FAQ und Troubleshooting

### 1. Wo lege ich fest, ob meine Dateien in der Datenbank oder in der Cloud gespeichert werden?
In der **Medienspeicher-Einrichtung** über das Feld **Speicherungsart** im Bereich
**Speicherort**. Die dort gewählte Ablage gilt für alle danach neu abgelegten Dateien.

### 2. Warum ist der Bereich „Azure Blob Storage“ (oder „OneDrive“) ausgegraut?
Der jeweilige Bereich ist nur bearbeitbar, wenn die **Speicherungsart** auf denselben Wert steht.
Setzen Sie zuerst die Speicherungsart auf **Azure Blob Storage** bzw. **OneDrive**, dann werden
die zugehörigen Felder freigeschaltet.

### 3. Warum kann ich die Aktion „Verbindung testen“ nicht auswählen?
Die Aktion ist nur aktiv, wenn als **Speicherungsart** **Azure Blob Storage** oder **OneDrive**
gewählt ist. Bei der Ablage **Datenbank** entfällt der Test, da keine externe Verbindung besteht.

### 4. Was passiert, wenn beim Ablegen die Verbindung zu Azure fehlschlägt?
Der Upload wird abgebrochen und es erscheint die Meldung, dass die Datei nicht hochgeladen werden
konnte und die Medienspeicher-Einrichtung geprüft werden soll. Kontrollieren Sie **Access Key**,
**Storage Account** und **Storage Container** und testen Sie die Verbindung erneut.

### 5. Warum ist das Feld „Bild“ bei einigen Einträgen leer, obwohl eine Datei existiert?
Bei Ablage im **Azure Blob Storage** wird die Datei nach dem Upload aus der Datenbank entfernt und
das Feld **Bild** geleert (Feld **Im Blob Speicher** = ja). Die Datei ist nicht verloren – sie
liegt in der Cloud und wird beim **Datei herunterladen** direkt von dort geladen.

### 6. Wie kommt eine Datei überhaupt in den Medienspeicher?
Nicht durch manuelles Anlegen: Der Anwender zieht eine Datei in die m+m **DropZone** eines Belegs
oder Stammsatzes. Daraus erzeugt das System automatisch einen Eintrag im Medienspeicher mit
**Code**, **Herkunftsart**, **Dateiname** und Inhalt.

### 7. Warum wird meine erste abgelegte Datei automatisch als Titelbild markiert?
Ist zu einer Herkunft noch kein Titelbild vorhanden, setzt das System bei der ersten Datei
automatisch **Ist Bildtitel** = ja. So steht dem verwendenden Modul sofort ein bevorzugtes Bild
zur Verfügung. Weitere Dateien erhalten diese Markierung nicht automatisch.

### 8. Was geschieht mit der Datei, wenn ich einen Eintrag aus der Medienspeicherliste lösche?
Die Datei wird am jeweiligen Ablageort mitgelöscht – aus dem **Azure Blob Storage**, wenn **Im
Blob Speicher** gesetzt ist, sonst aus der internen Medienablage der Datenbank. Es bleibt keine
verwaiste Datei zurück.

### 9. Bestimmt die „Delegierte Genehmigungen“-Option, in welches OneDrive gespeichert wird?
Ja. Ist **Delegierte Genehmigungen** aktiviert, landet die Datei im OneDrive des angemeldeten
Benutzers. Ist die Option nicht aktiviert, wird das unter **E-Mail** hinterlegte Konto verwendet.

### 10. Ich erhalte nach der Anmeldung einen Lizenz- oder Zahlungshinweis – was bedeutet das?
Media Storage prüft in Cloud-Umgebungen über die Basis-App **m+m Cloud Base** die Lizenz. Ist der
Mandant oder Benutzer dem Modul nicht zugeordnet oder eine Zahlung überfällig, erscheint ein
Hinweis; bei mehrfacher Überfälligkeit kann die App gesperrt werden. Wenden Sie sich zur Klärung
an Ihren Administrator bzw. an Markmann + Müller. In On-Premises- und Sandbox-Umgebungen entfällt
diese Prüfung.

## Typische Anwendungsfälle

### Anwendungsfall 1: Produktbild zu einem Artikel ablegen

**Auslöser:** Ein Kollege sendet per E-Mail ein Produktfoto zu einem Artikel und bittet darum, es
im System zu hinterlegen.

**Einstieg in BC:** Der Anwender öffnet den betreffenden Artikel; auf der Karte steht die m+m
DropZone samt der Infobox **Medienspeicherdateien** zur Verfügung.

**Kernablauf:** Der Anwender zieht die Bilddatei in die DropZone. Das System erzeugt automatisch
einen Medienspeicher-Eintrag: **Code** und **Herkunftsart** werden aus dem Artikelkontext
übernommen, **Dateiname** aus dem Dateinamen gesetzt und – da es die erste Datei zu diesem Artikel
ist – **Ist Bildtitel** = ja gesetzt. Je nach eingestellter **Speicherungsart** liegt die Datei
nun in der Datenbank, im Azure Blob Storage oder in OneDrive. In der **Medienspeicherliste** (über
**Suchen**) findet der Anwender das Bild anschließend wieder.

**Abschluss:** Bei Bedarf lädt der Anwender die Datei über die Infobox **Medienspeicherdateien**
und die Aktion **Datei herunterladen** wieder herunter.

### Anwendungsfall 2: Cloud-Ablage über Azure Blob Storage aktivieren

**Auslöser:** Die Datenbank soll entlastet werden; der Administrator entscheidet, künftig alle
Dateien in Azure abzulegen.

**Einstieg in BC:** Der Administrator öffnet über **Suchen** die **Medienspeicher-Einrichtung**.

**Kernablauf (Reihenfolge zwingend):**
1. Im Bereich **Speicherort** die **Speicherungsart** auf **Azure Blob Storage** setzen.
2. Im Bereich **Azure Blob Storage** die Felder **Access Key**, **Storage Account** und
   **Storage Container** aus dem Azure-Portal eintragen.
3. Die Aktion **Verbindung testen** wählen und die Erfolgsmeldung abwarten.

**Abschluss:** Ab sofort wird jede über die DropZone abgelegte Datei automatisch in den Container
hochgeladen; in der **Medienspeicherliste** ist bei diesen Einträgen **Im Blob Speicher** = ja,
und das Feld **Bild** ist geleert. Der Download erfolgt weiterhin über **Datei herunterladen**,
nun direkt aus der Cloud.

### Anwendungsfall 3: Nicht mehr benötigte Datei entfernen

**Auslöser:** Ein Dokument ist veraltet und soll aus dem System verschwinden.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** die **Medienspeicherliste** und sucht den
Eintrag anhand von **Code** und **Dateiname**.

**Kernablauf:** Der Anwender markiert den Eintrag und löscht ihn. Das System entfernt die Datei
zugleich am Ablageort: bei **Im Blob Speicher** = ja aus dem Azure Blob Storage, sonst aus der
Datenbank.

**Abschluss:** Der Eintrag verschwindet aus der Medienspeicherliste; es verbleibt keine verwaiste
Datei am Speicherort. Wird vorher noch eine Kopie benötigt, lädt der Anwender die Datei zuvor über
**Datei herunterladen** herunter.
