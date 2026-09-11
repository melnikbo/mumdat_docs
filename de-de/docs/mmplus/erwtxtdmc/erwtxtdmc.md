---
title: Anwenderhandbuch m+m Ext. Text Module with Digital Metal Code
---

# Anwenderhandbuch m+m Ext. Text Module with Digital Metal Code

## Einleitung

Das Modul **m+m Ext. Text Module with Digital Metal Code** erweitert das Basismodul *m+m Ext. Text Module* um zwei zusätzliche **Systemprozeduren**, mit denen Sie **IDMC-Barcodes** direkt in erweiterte Texte einbetten. Ein **Platzhalter** in einem erweiterten Text wird beim Andruck bzw. Versand nicht durch einen einfachen Feldwert, sondern durch ein **Barcodebild** ersetzt: entweder einen **QR Code** (zweidimensionaler Matrixcode) oder einen **Code 39** (linearer Strichcode). Grundlage des Barcodes ist der **IDMC Code**, den das Modul *m+m Digital Metal Code* am Artikel, an der Artikelvariante, an der Charge oder an den zugehörigen Beleg­zeilen führt.

Der Ablauf ist bewusst schlank: Sie legen im Basismodul einen Platzhalter an, wählen als **Systemprozeduren** den Wert **IDMC QR-Code** oder **IDMC Code39** und setzen bei Bedarf **Breite** und **Größe ändern %**. Beim Andruck sucht das Modul zuerst ein bereits gespeichertes Barcodebild zum IDMC Code; ist keines vorhanden, erzeugt es den Barcode über den Barcodedienst neu. So erscheint auf Ihren Belegen, in Ihren Berichten und E-Mail-Texten an der Platzhalterstelle automatisch der passende, scannbare Code.

**Zielgruppe:** Primär richtet sich dieses Handbuch an die **operativen Anwender im Tagesgeschäft**, die erweiterte Texte auf Verkaufs- und Einkaufsbelegen nutzen und dort einen Barcode benötigen. Sekundär sind **Administratorinnen und Administratoren bzw. Key-User** angesprochen, die die **Platzhalter** und die **Erweiterte Texteinstellungen** des Basismoduls pflegen sowie sicherstellen, dass die Artikel, Varianten oder Chargen einen **IDMC Code** tragen.

**Kurzer Prozessüberblick:**

1. Ein Administrator stellt in den **Erweiterte Texteinstellungen** sicher, dass ein **Platzhalter-Startzeichen** und ein **Platzhalter-Endzeichen** hinterlegt sind (Voraussetzung, damit Platzhalter überhaupt verarbeitet werden).
2. Ein Key-User legt in der Liste **Platzhalter** einen neuen Platzhalter an, wählt die Zieltabelle und als **Systemprozeduren** den Wert **IDMC QR-Code** oder **IDMC Code39** und setzt **Breite** bzw. **Größe ändern %**.
3. Der Platzhalter wird im erweiterten Textbaustein zwischen Start- und Endzeichen eingefügt.
4. Voraussetzung ist, dass der zugehörige Datensatz einen **IDMC Code** besitzt (aus dem Modul *m+m Digital Metal Code*).
5. Beim Andruck bzw. E-Mail-Versand ersetzt das Modul den Platzhalter durch das Barcodebild — aus dem Cache oder neu erzeugt.

> ☞ Dieses Modul enthält **keinen** eigenen Buchungs-, Freigabe- oder Berichtslauf. Es fügt ausschließlich Barcodebilder in bereits vorhandene erweiterte Texte ein; die eigentliche Beleg­verarbeitung bleibt unverändert Standard.

## Schnellstart für Anwender

Der Schnellstart nennt den kürzesten Weg zum Ergebnis. Die Reihenfolge folgt der technischen Abhängigkeit: **zuerst Einrichtung, dann Platzhalter, dann Tagesarbeit**.

### A. Einmalige Voraussetzung (Administrator)

1. Öffnen Sie über **Suchen** die **Erweiterte Texteinstellungen**.
2. Prüfen Sie, dass ein **Platzhalter-Startzeichen** und ein **Platzhalter-Endzeichen** hinterlegt sind. Ohne beide Zeichen verarbeitet das Basismodul keine Platzhalter, und es wird kein Barcode eingesetzt.

### B. Barcode-Platzhalter anlegen (Key-User)

3. Öffnen Sie in den **Erweiterte Texteinstellungen** über die Aktion **Platzhalter** die Liste der Platzhalter.
4. Legen Sie einen neuen **Platzhalter** an und vergeben Sie einen eindeutigen Platzhalter-Code.
5. Wählen Sie die **Tabellen-ID** der Zieltabelle (z. B. Verkaufszeile) und — falls das Zielfeld benötigt wird — die **Feld Nr.**
6. Setzen Sie das Feld **Systemprozeduren** auf **IDMC QR-Code** (zweidimensionaler Code) oder **IDMC Code39** (linearer Strichcode).
7. Hinterlegen Sie bei **IDMC QR-Code** die gewünschte **Breite** und bei Bedarf die **Größe ändern %**.

### C. Platzhalter im Text verwenden und drucken (Anwender)

8. Fügen Sie den Platzhalter-Code — umschlossen von Start- und Endzeichen — an der gewünschten Stelle in den erweiterten Textbaustein ein.
9. Stellen Sie sicher, dass der Datensatz (Artikel, Variante, Charge oder Beleg­zeile) einen **IDMC Code** trägt.
10. Drucken oder versenden Sie den Beleg wie gewohnt. An der Platzhalterstelle erscheint automatisch das Barcodebild.

> ☞ Ist zum IDMC Code bereits ein Barcodebild gespeichert, verwendet das Modul dieses; andernfalls erzeugt es den Barcode beim Andruck neu (Neuerzeugung nur in der Cloud/SaaS-Umgebung).

## Einrichtung

Die Einrichtung dieses Moduls ist bewusst minimal: Das Modul bringt **keine eigene Einrichtungsseite** mit. Alle Einstellungen werden auf zwei Seiten des Basismoduls vorgenommen — den **Erweiterte Texteinstellungen** (globale Voraussetzung) und der Liste **Platzhalter** (eigentliche Konfiguration des Barcode-Platzhalters). Beide Seiten steuern gemeinsam, ob und wie der Barcode an der Platzhalterstelle erscheint.

### Voraussetzung: Platzhalterzeichen in den Erweiterte Texteinstellungen

**Wer/wann:** Ein Administrator nimmt diese Einstellung **einmalig pro Mandant** vor, bevor Platzhalter zum ersten Mal genutzt werden. Es handelt sich um eine unternehmensweite Einrichtung mit genau einem Datensatz pro Mandant. **Einstieg:** Öffnen Sie über **Suchen** die **Erweiterte Texteinstellungen**. Die hier gesetzten Zeichen sind Voraussetzung dafür, dass die Platzhalter-Verarbeitung — und damit die Barcode-Ersetzung dieses Moduls — überhaupt anläuft (Querverweis: Abschnitt **Tägliche Arbeit**).

| Einrichtung | Erläuterung |
|---|---|
| **Platzhalter-Startzeichen** | Wenn gesetzt, erkennt das Basismodul ab diesem Zeichen den Beginn eines Platzhalters im erweiterten Text; ist das Zeichen leer, wird kein Platzhalter — und damit auch kein Barcode — verarbeitet, der Text bleibt unverändert. |
| **Platzhalter-Endzeichen** | Wenn gesetzt, markiert dieses Zeichen das Ende des Platzhalters; erst mit gültigem Start- **und** Endzeichen ersetzt das Modul den eingeschlossenen Code durch das Barcodebild. Fehlt eines der beiden, unterbleibt jede Ersetzung. |
| **Vorlagennummern** | Wenn gesetzt, zieht das Basismodul die Nummern neuer Textvorlagen aus dieser Nummernserie; betrifft die Anlage von Textbausteinen, in denen Sie den Barcode-Platzhalter später einfügen. |
| **Vorschautexte in Herkunftsbelegen** | Wenn aktiviert, zeigt das Basismodul die erweiterten Texte bereits im Herkunftsbeleg zur Vorschau an; so erkennen Sie vor dem Andruck, an welcher Stelle der Barcode-Platzhalter greift. |

> ☞ Die weiteren Felder der **Erweiterte Texteinstellungen** (z. B. automatische Textzuweisung beim Buchen, E-Mail-Platzhalter, Hintergrund-Texterzeugung) gehören zum Funktionsumfang des Basismoduls *m+m Ext. Text Module* und haben **keinen** Einfluss auf die Barcode-Erzeugung dieses Moduls. Sie werden dort konfiguriert, wo das Basismodul sie beschreibt.

### Barcode-Platzhalter einrichten

**Prozesseinstieg:** Dies ist die zentrale Konfiguration des Moduls. Ein Key-User legt je Barcode-Anwendung einen **Platzhalter** an und verknüpft ihn über die **Systemprozeduren** mit der Barcode-Erzeugung. Die Einrichtung greift später in der **Tägliche Arbeit**, sobald ein erweiterter Text mit diesem Platzhalter angedruckt oder versendet wird. **Einstieg:** Öffnen Sie in der **Erweiterte Texteinstellungen** die Aktion **Platzhalter**; es öffnet sich die Liste **Platzhalter**.

Die folgende Tabelle beschreibt die Felder des Platzhalters, die für die Barcode-Erzeugung relevant sind. Das Modul fügt diesen Feldern keine neuen hinzu; es ergänzt lediglich die Auswahl im Feld **Systemprozeduren**.

| Feld | Erläuterung |
|---|---|
| **Platzhalter** | Wenn gesetzt, ist dies der eindeutige Code, den Sie zwischen Start- und Endzeichen in den erweiterten Text einfügen; genau an dieser Stelle erscheint später das Barcodebild. Ohne Platzhalter-Code lässt sich der Datensatz nicht speichern. |
| **Tabellen-ID** | Wenn gesetzt, bindet der Platzhalter an diese Zieltabelle (z. B. Verkaufszeile, Einkaufszeile, Artikel); daraus liest das Modul beim Andruck den Datensatz, dessen IDMC Code den Barcode liefert. Zulässig sind nur die vom Basismodul freigegebenen Tabellen. |
| **Tabellenname** | Zeigt den Namen der gewählten Tabelle an (nur Anzeige); dient der Kontrolle, dass die richtige Zieltabelle gewählt wurde. |
| **Feld Nr.** | Wenn gesetzt, verweist der Platzhalter auf dieses Feld der Zieltabelle; für die Barcode-Systemprozeduren ist dies der Ausgangswert, aus dem heraus das Modul das zugehörige IDMC-Feld ermittelt. |
| **Feld Name** | Zeigt die Bezeichnung des gewählten Feldes an (nur Anzeige). |
| **Systemprozeduren** | Steuert, wodurch der Platzhalter ersetzt wird. Für dieses Modul wählen Sie **IDMC QR-Code** oder **IDMC Code39** — dann wird der Platzhalter durch das jeweilige Barcodebild ersetzt (die einzelnen Werte werden unten erläutert). |
| **Freitext** | Wenn gesetzt, ersetzt das Basismodul den Platzhalter durch diesen festen Text; das Setzen eines Freitextes leert Tabellen- und Feldbezug. Für Barcode-Platzhalter bleibt dieses Feld leer, da der Wert aus dem Datensatz stammt. |
| **Verwandte Tabelle** | Zeigt an, auf welche verknüpfte Tabelle sich der Platzhalter zusätzlich bezieht (wird beim Setzen der Feld Nr. automatisch ermittelt, nur Anzeige). |
| **Zugehöriges Tabellenfeld** | Wenn gesetzt, liest das Basismodul den Wert aus diesem Feld der verwandten Tabelle; relevant, wenn der IDMC nicht direkt in der Zieltabelle, sondern in einer verknüpften Tabelle steht. |
| **Zugehöriges Feld Name** | Zeigt die Bezeichnung des zugehörigen Feldes an (nur Anzeige). |
| **Drucktyp** | Wenn auf **Bericht** gesetzt, steht der Platzhalter für den Andruck in einem Bericht zur Verfügung; damit legen Sie fest, in welchem Ausgabekanal der Barcode erscheint. |
| **Breite** | Wenn gesetzt, erzeugt das Modul den **IDMC QR-Code** mit dieser Breite; über die Breite steuern Sie die Kantenlänge des QR-Bildes im Beleg. Bleibt sie leer, wird die Vorgabegröße des Barcodedienstes verwendet. |
| **Größe ändern %** | Wenn gesetzt (zulässig −99 bis 99), skaliert das Modul das erzeugte Barcodebild um diesen Prozentsatz: ein positiver Wert vergrößert, ein negativer verkleinert das Bild; bei 0 bleibt die Originalgröße erhalten. So passen Sie den Barcode an den verfügbaren Platz im Beleg an, ohne den Code neu zu erzeugen. |
| **Höhe** | Wenn gesetzt, wird das Bild auf diese Höhe gebracht; zusammen mit **Breite** bestimmt die Höhe die Darstellung des Barcodes. Eine Änderung löst eine erneute Skalierung des Bildes aus. |
| **Bild / Bild Name** | Enthält ein manuell hinterlegtes Bild bzw. dessen Namen; für die Barcode-Systemprozeduren bleibt diese Bildablage in der Regel leer, da das Barcodebild aus dem IDMC-Cache stammt oder neu erzeugt wird. |

#### Werte des Feldes Systemprozeduren (Task-relevante Optionswerte)

Das Feld **Systemprozeduren** ist ein Auswahlfeld mit festem Wertevorrat. Das Basismodul liefert die ersten Werte; dieses Modul ergänzt die beiden IDMC-Werte. Bedeutung je Wert:

- **(leer):** Es wird keine Systemprozedur ausgeführt; der Platzhalter wird — sofern gefüllt — über Freitext oder Feldbezug ersetzt, es entsteht **kein** Barcode.
- **Benutzer-ID:** Der Platzhalter wird durch die Benutzer-ID ersetzt (Basisfunktion, kein Barcode).
- **Heute:** Der Platzhalter wird durch das aktuelle Tagesdatum ersetzt (Basisfunktion, kein Barcode).
- **Arbeitsdatum:** Der Platzhalter wird durch das in Business Central eingestellte Arbeitsdatum ersetzt (Basisfunktion, kein Barcode).
- **Aktuelle Zeit:** Der Platzhalter wird durch die aktuelle Uhrzeit ersetzt (Basisfunktion, kein Barcode).
- **IDMC QR-Code:** Wenn ausgewählt, ermittelt das Modul zum Datensatz das Feld mit dem IDMC Code, sucht ein gespeichertes **QR Code**-Bild und setzt es an die Platzhalterstelle; ist keines vorhanden, erzeugt es den QR Code über den Barcodedienst neu (mit der eingestellten **Breite**) und bettet ihn als Bild ein.
- **IDMC Code39:** Wenn ausgewählt, verfährt das Modul ebenso, erzeugt jedoch einen linearen **Code 39**-Barcode; liegt kein gespeichertes Bild vor, wird der Code 39 neu erzeugt und als Barcode eingesetzt.

> ☞ Die beiden Werte **IDMC QR-Code** und **IDMC Code39** erscheinen im Auswahlfeld sprachunabhängig mit dieser Schreibweise, da es sich um festgelegte Produktkennungen handelt.

#### Prozessschritte: Barcode-Platzhalter vollständig einrichten

1. **Zuerst** in den **Erweiterte Texteinstellungen** das **Platzhalter-Startzeichen** und **Platzhalter-Endzeichen** prüfen bzw. setzen — ohne diese Zeichen greift kein Platzhalter.
2. **Danach** über die Aktion **Platzhalter** einen neuen Platzhalter anlegen, Platzhalter-Code vergeben und die **Tabellen-ID** (sowie ggf. **Feld Nr.**) der Zieltabelle wählen.
3. **Anschließend** das Feld **Systemprozeduren** auf **IDMC QR-Code** oder **IDMC Code39** setzen und — bei QR — die **Breite** sowie bei Bedarf **Größe ändern %** hinterlegen.
4. **Schließlich** den Platzhalter-Code, umschlossen vom Start- und Endzeichen, in den erweiterten Textbaustein einfügen (Querverweis: **Tägliche Arbeit**).

**Voraussetzung/Abhängigkeit:** Der Barcode wird nur dann erzeugt, wenn der Datensatz der Zieltabelle über ein Feld verfügt, dessen Name auf **IDMC Code** endet und das gefüllt ist. Dieses Feld stammt aus dem Modul *m+m Digital Metal Code* (siehe **Tägliche Arbeit** und **Voraussetzung IDMC Code**). Ist das IDMC-Feld leer, bleibt die Platzhalterstelle ohne Barcode.

## Tägliche Arbeit

Im Tagesgeschäft berührt dieses Modul keine eigene Seite und keine eigene Aktion. Es wirkt **im Hintergrund** beim Andruck oder E-Mail-Versand eines Belegs, sobald ein erweiterter Text einen Barcode-Platzhalter enthält. Für den Anwender bleibt der Ablauf der gewohnte: Beleg erfassen, erweiterten Text zuordnen, drucken oder senden.

**Bezug zur Einrichtung:** Damit an der Platzhalterstelle ein Barcode erscheint, müssen drei Bedingungen erfüllt sein — sie werden in **Einrichtung** gesetzt bzw. vorausgesetzt:

1. In den **Erweiterte Texteinstellungen** sind **Platzhalter-Startzeichen** und **Platzhalter-Endzeichen** hinterlegt.
2. Auf der Liste **Platzhalter** existiert ein Platzhalter mit **Systemprozeduren** = **IDMC QR-Code** oder **IDMC Code39**, der im Textbaustein verwendet wird.
3. Der gedruckte Datensatz besitzt einen gefüllten **IDMC Code** (aus *m+m Digital Metal Code*).

### Voraussetzung IDMC Code

Der Barcode bildet stets einen **IDMC Code** ab. Diesen Code führt das Modul *m+m Digital Metal Code* am Artikel, an der Artikelvariante, an der Charge sowie auf den zugehörigen Verkaufs- und Einkaufsbelegzeilen. Beim Andruck sucht dieses Modul auf der Zieltabelle automatisch das Feld, dessen Bezeichnung auf **IDMC Code** endet, und verwendet dessen Inhalt als Barcodeinhalt.

- Ist das IDMC-Feld **leer**, bleibt die Platzhalterstelle ohne Barcode (der Beleg wird dennoch fertig gedruckt).
- Ist das IDMC-Feld **gefüllt**, prüft das Modul zunächst den Barcode-Cache **IDMC Barcode** (Tabelle des Moduls *m+m Digital Metal Code*).

### Ablauf der Barcode-Ersetzung (aus dem Code abgeleitet)

1. Das Basismodul verarbeitet beim Andruck den erweiterten Text und trifft auf einen Platzhalter mit **Systemprozeduren** = **IDMC QR-Code** bzw. **IDMC Code39**.
2. Dieses Modul ermittelt auf der Zieltabelle das Feld, dessen Name auf **IDMC Code** endet, und liest dessen Wert.
3. Es sucht im **IDMC Barcode**-Cache ein Bild zum Schlüssel aus **IDMC Code** und **Barcodeart** (**QR Code** bzw. **Code 39**).
4. **Ist ein Bild vorhanden**, wird es an die Platzhalterstelle gesetzt — bei Bedarf zuvor gemäß **Größe ändern %** skaliert.
5. **Ist kein Bild vorhanden**, erzeugt das Modul den Barcode neu: den **QR Code** mit der eingestellten **Breite**, den **Code 39** als linearen Strichcode. Die Neuerzeugung erfolgt über den Barcodedienst und ist der Cloud/SaaS-Umgebung vorbehalten.
6. Das erzeugte oder gelesene Barcodebild ersetzt den Platzhalter im ausgegebenen Text.

### Der Barcode-Cache: IDMC Barcode

Zu jedem **IDMC Code** legt das Modul *m+m Digital Metal Code* je **Barcodeart** genau ein Bild ab. Die Seite **IDMC Barcodes** zeigt diese Bilder an. Für dieses Modul ist der Cache die bevorzugte Quelle, da das gespeicherte Bild ohne erneuten Dienstaufruf verwendet werden kann.

| Feld | Erläuterung |
|---|---|
| **IDMC Code** | Der Code, zu dem der Barcode gehört; er verbindet den gedruckten Datensatz mit dem gespeicherten Barcodebild. |
| **Barcodeart** | Art des Barcodes. **Code 39:** ein linearer Strichcode — verwendet, wenn der Platzhalter auf **IDMC Code39** steht. **QR Code:** ein zweidimensionaler Matrixcode — verwendet, wenn der Platzhalter auf **IDMC QR-Code** steht. Je IDMC Code wird je Barcodeart genau ein Bild vorgehalten. |
| **Bild** | Das gespeicherte Barcodebild; dieses Modul bettet es unverändert (bzw. gemäß **Größe ändern %** skaliert) in den erweiterten Text ein. |

## Typische Anwendungsfälle

Die folgenden Szenarien sind aus dem geprüften Verhalten des Moduls abgeleitet.

### Anwendungsfall 1: QR Code auf der Auftragsbestätigung

- **Auslöser:** Ein Kunde verlangt auf der gedruckten Auftragsbestätigung einen scannbaren QR Code je Position, damit sein Wareneingang die Ware eindeutig zuordnen kann.
- **Einstieg in BC:** Öffnen Sie über **Suchen** die **Erweiterte Texteinstellungen** und stellen Sie sicher, dass **Platzhalter-Startzeichen** und **Platzhalter-Endzeichen** gesetzt sind. Öffnen Sie dann über die Aktion **Platzhalter** die Platzhalterliste.
- **Kernablauf:** Legen Sie einen Platzhalter an, wählen Sie als **Tabellen-ID** die Verkaufszeile und setzen Sie **Systemprozeduren** = **IDMC QR-Code**. Hinterlegen Sie die gewünschte **Breite** und passen Sie bei Bedarf über **Größe ändern %** die Darstellung an. Fügen Sie den Platzhalter-Code in den erweiterten Textbaustein der Auftragsbestätigung ein. Erfassen Sie den Verkaufsauftrag wie gewohnt; die Positionen tragen bereits ihren **IDMC Code**.
- **Abschluss:** Beim Andruck ersetzt das Modul den Platzhalter durch das QR-Bild aus dem **IDMC Barcode**-Cache. Der Beleg wird über die Standardfunktion gedruckt oder als E-Mail versendet.

### Anwendungsfall 2: Code39-Barcode für einen frisch codierten Artikel

- **Auslöser:** Ein neu angelegter Artikel hat gerade erst seinen **IDMC Code** erhalten; zu diesem Code liegt noch **kein** gespeichertes Barcodebild vor, dennoch soll der Beleg sofort einen linearen Barcode zeigen.
- **Einstieg in BC:** Rufen Sie in der **Erweiterte Texteinstellungen** über die Aktion **Platzhalter** die Platzhalterliste auf.
- **Kernablauf:** Verwenden Sie einen Platzhalter mit **Systemprozeduren** = **IDMC Code39** im erweiterten Text des betreffenden Belegs. Beim Andruck findet das Modul im Cache kein Bild und erzeugt den **Code 39** über den Barcodedienst neu.
- **Abschluss:** Der neu erzeugte Barcode erscheint an der Platzhalterstelle. (Die Neuerzeugung ist der Cloud/SaaS-Umgebung vorbehalten; siehe FAQ.)

## FAQ und Troubleshooting

### 1. Warum erscheint an der Platzhalterstelle kein Barcode, sondern nichts?

Das zugehörige **IDMC Code**-Feld des Datensatzes ist leer. Das Modul erkennt zwar den Platzhalter, findet aber keinen Codeinhalt und lässt die Stelle ohne Barcode. Versehen Sie den Artikel, die Variante, die Charge oder die Beleg­zeile zuvor mit einem IDMC Code (Modul *m+m Digital Metal Code*).

### 2. Warum wird der Platzhalter im Text gar nicht ersetzt?

In den **Erweiterte Texteinstellungen** fehlt das **Platzhalter-Startzeichen** oder das **Platzhalter-Endzeichen**. Ohne beide Zeichen verarbeitet das Basismodul keine Platzhalter, und es wird kein Barcode eingesetzt. Hinterlegen Sie beide Zeichen.

### 3. Wann verwendet das Modul ein gespeichertes Bild und wann erzeugt es neu?

Zuerst sucht das Modul im **IDMC Barcode**-Cache ein Bild zum **IDMC Code** und zur **Barcodeart** (**QR Code** bzw. **Code 39**). Ist ein Bild vorhanden, wird es verwendet; fehlt es, wird der Barcode über den Barcodedienst neu erzeugt.

### 4. Warum wird in meiner lokalen Installation kein Barcode neu erzeugt?

Die **Neuerzeugung** eines Barcodes über den Barcodedienst erfolgt ausschließlich in der Cloud/SaaS-Umgebung. Liegt kein zwischengespeichertes Bild vor, bleibt die Stelle in einer On-Premises-Installation ohne neu erzeugten Code. Sorgen Sie in diesem Fall dafür, dass zum IDMC Code bereits ein Barcodebild gespeichert ist.

### 5. Worin unterscheiden sich IDMC QR-Code und IDMC Code39?

**IDMC QR-Code** erzeugt einen zweidimensionalen **QR Code** (kompakt, viel Inhalt, per Kamera scannbar) und berücksichtigt die eingestellte **Breite**. **IDMC Code39** erzeugt einen linearen **Code 39**-Strichcode (klassischer Barcodescanner). Je Anwendung wählen Sie im Feld **Systemprozeduren** den passenden Wert.

### 6. Wie stelle ich die Größe des Barcodes ein?

Bei **IDMC QR-Code** steuern Sie die Kantenlänge über die **Breite**. Zusätzlich skaliert **Größe ändern %** das fertige Bild: positive Werte vergrößern, negative verkleinern (zulässig −99 bis 99); bei 0 bleibt die Originalgröße. So passen Sie den Barcode an den Platz im Beleg an.

### 7. An welche Tabelle muss ich den Platzhalter binden?

Wählen Sie in der **Tabellen-ID** die Tabelle, aus der beim Andruck der Datensatz mit dem IDMC Code stammt (z. B. Verkaufszeile oder Einkaufszeile). Zulässig sind nur die vom Basismodul für Platzhalter freigegebenen Tabellen; eine unzulässige Tabelle weist das Basismodul mit einer Meldung ab.

### 8. Muss ich das Feld Freitext füllen?

Nein. Für Barcode-Platzhalter bleibt **Freitext** leer, da der Codeinhalt aus dem Datensatz gelesen wird. Das Setzen eines Freitextes würde den Tabellen- und Feldbezug entfernen und den Platzhalter durch festen Text statt durch den Barcode ersetzen.

### 9. Wo sehe ich die vorhandenen Barcodebilder?

Auf der Seite **IDMC Barcodes** des Moduls *m+m Digital Metal Code*. Dort ist zu jedem **IDMC Code** je **Barcodeart** das gespeicherte **Bild** hinterlegt, das dieses Modul in die erweiterten Texte einbettet.

### 10. Warum funktioniert das Modul nicht, obwohl alles eingerichtet ist?

Beim Anmelden prüft das Modul die Lizenz. Fehlt eine gültige Lizenz für die Erweiterung, stehen die Barcode-Systemprozeduren nicht zur Verfügung. Wenden Sie sich in diesem Fall an Ihren Administrator bzw. an m+m, um die Lizenzierung zu klären.
