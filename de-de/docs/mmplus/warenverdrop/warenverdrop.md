---
title: Anwenderhandbuch m+m Goods Receipt with Dropzone
---

# Anwenderhandbuch m+m Goods Receipt with Dropzone

## Einleitung

Die m+m Erweiterung **Goods Receipt with Dropzone** ergänzt die Warenannahme in „Microsoft Dynamics 365 Business Central“ um eine **Dokumentenablage direkt am Wareneingangsbeleg**. Anwender können Dateien (Lieferscheine, Zertifikate, Fotos, PDF) per Ziehen und Ablegen an der **Warenannahme** hinterlegen oder direkt ein **Bild** über die Gerätekamera aufnehmen. Beim Verarbeiten der Warenannahme werden diese Belege automatisch an den entstehenden **gebuchten Wareneingang** (Quellart **Geb. Wareneingang**) übertragen, sodass die Dokumentation dauerhaft mit dem Vorgang verbunden bleibt.

**Zielgruppe:** Primär die **operativen Anwender in der Wareneingangs- und Lagerbearbeitung**, die täglich Warenannahmen erfassen, freigeben und verarbeiten und dabei Belege bzw. Fotos zum Vorgang festhalten. Sekundär betrifft die Erweiterung Administratoren, die lediglich die Installation der abhängigen Apps sicherstellen — eine fachliche Einrichtung ist nicht erforderlich.

**Kurzer Prozessüberblick:** Die Erweiterung fügt der Ansicht **Warenannahme** und der Ansicht des gebuchten Wareneingangs jeweils die Faktenbox **DropZone** hinzu. An der Warenannahme steht zusätzlich die Aktion **Bild aufnehmen** zur Verfügung. Legt der Anwender an der Warenannahme Dateien ab und verarbeitet den Beleg anschließend über die Standardfunktionen des Moduls Warenvereinnahmung (**Freigeben**, **Verarbeitung**), so wandern die abgelegten Belege automatisch an den gebuchten Wareneingang mit. Wird eine noch offene Warenannahme gelöscht, werden die zugehörigen Belege ebenfalls entfernt.

> Diese Erweiterung baut auf den m+m Apps **m+m Goods Receipt** (Warenvereinnahmung), **m+m Dropzone**, **m+m Media Storage** und **m+m Cloud Base** auf. Die eigentlichen Wareneingangsbelege, ihre Kopf- und Zeilenfelder sowie die Aktionen **Freigeben**, **Avisieren** und **Verarbeitung** stammen aus dem Modul Warenvereinnahmung; dieses Handbuch beschreibt die durch die DropZone-Erweiterung ergänzten Funktionen und ihren Platz im Ablauf.

## Schnellstart für Anwender

Der schnellste Weg von der Warenannahme bis zum dokumentierten, verarbeiteten Wareneingang:

1. **Warenannahme öffnen.** Wählen Sie im Modul Warenvereinnahmung in der Liste der Warenannahmen die gewünschte Zeile und öffnen Sie die Ansicht **Warenannahme**.
2. **Belege ablegen.** Ziehen Sie die gewünschten Dateien mit gedrückter Maustaste aus dem Windows-Explorer in die Faktenbox **DropZone** und lassen Sie sie dort los (Ziehen und Ablegen). Die Datei wird gespeichert und unterhalb des Ablagebereichs unter **Dateiname** aufgelistet.
3. **Optional: Bild aufnehmen.** Nutzen Sie die Aktion **Bild aufnehmen**, um über die Kamera des Geräts direkt ein Foto der Ware zu erstellen. Das Foto wird automatisch als Beleg zur Warenannahme abgelegt.
4. **Freigeben.** Lösen Sie die Aktion **Freigeben** aus, um die Warenannahme freizugeben (Status **In Bearbeitung** bzw. freigegeben).
5. **Verarbeiten.** Starten Sie über die Kategorie **Verarbeitung** die Verarbeitung der Warenannahme. Dabei entsteht der **gebuchte Wareneingang** (Geb. Wareneingang).
6. **Ergebnis prüfen.** Öffnen Sie den gebuchten Wareneingang: In dessen Faktenbox **DropZone** finden Sie dieselben Belege wieder — sie wurden automatisch mit übertragen.

Für die Nutzung ist **keine gesonderte Einrichtung** notwendig (siehe folgendes Kapitel).

## Einrichtung

Für die Erweiterung **Goods Receipt with Dropzone** ist **keine fachliche Einrichtung** erforderlich. Es gibt keine eigenen Einrichtungsseiten, keine Nummernserien und keine zu pflegenden Parameter. Die Funktion steht unmittelbar an der Warenannahme und am gebuchten Wareneingang zur Verfügung, sobald die erforderlichen Apps installiert sind.

**Voraussetzungen (durch den Administrator sicherzustellen):**

| Einrichtung | Erläuterung |
|---|---|
| App **m+m Goods Receipt with Dropzone** installiert | Wenn die Erweiterung in der Erweiterungsverwaltung installiert ist, erscheinen die Faktenbox **DropZone** und die Aktion **Bild aufnehmen** an der Warenannahme sowie die Faktenbox **DropZone** am gebuchten Wareneingang; ohne Installation stehen diese Funktionen nicht bereit. |
| Abhängige App **m+m Goods Receipt** installiert | Wenn das Modul Warenvereinnahmung vorhanden ist, existieren die Belege **Warenannahme** und **Geb. Wareneingang**, an die die DropZone andockt; fehlt es, gibt es keine Zielbelege für die Dokumentenablage. |
| Abhängige App **m+m Dropzone** installiert | Wenn die Dropzone-Basis vorhanden ist, funktioniert die Ablage per Ziehen und Ablegen samt Liste (**Dateiname**) und der Aktion **Datei herunterladen**; ohne sie fehlt der Ablagebereich. |
| Abhängige App **m+m Media Storage** installiert | Wenn die Medienspeicherung vorhanden ist, werden die abgelegten Dateien und aufgenommenen Bilder dauerhaft in der Datenbank (bzw. im eingerichteten Speicher) gehalten und sind später abrufbar; ohne sie können keine Belege gespeichert werden. |

> Hinweis: Wo und wie der Medienspeicher physisch abgelegt wird (z. B. Datenbank oder Azure-Speicher), regelt die App **m+m Media Storage** über ihre eigene Einrichtung. Für die DropZone an der Warenannahme sind dort keine zusätzlichen Einstellungen speziell für diese Erweiterung vorzunehmen.

## Tägliche Arbeit an der Warenannahme

Die eigentliche Arbeit findet an zwei Belegen des Moduls Warenvereinnahmung statt: an der **Warenannahme** (offener Wareneingangsbeleg) und am **gebuchten Wareneingang** (Geb. Wareneingang). Beide erhalten durch diese Erweiterung die Faktenbox **DropZone**; die Warenannahme zusätzlich die Aktion **Bild aufnehmen**.

Die folgenden Kopffelder der **Warenannahme** stammen aus dem Modul Warenvereinnahmung und dienen hier nur der Orientierung, an welchem Vorgang die Belege hängen:

| Feld | Erläuterung |
|---|---|
| **Nr.** | Eindeutige Belegnummer der Warenannahme; die DropZone ordnet alle abgelegten Belege genau dieser Nummer zu. |
| **Lagerortcode** | Lagerort, für den die Ware angenommen wird; steuert die weitere Lagerlogik des Basismoduls. |
| **Eingangsdatum** | Datum des Wareneingangs; dokumentiert, wann die Ware angenommen wurde. |
| **Verk. an Deb.-Nr.** / **Verk. an Name** | Debitor, sofern die Annahme mit einem Verkaufsvorgang verknüpft ist; relevant für Folgeschritte wie **Verkaufsauftrag erstellen**. |
| **Buchungsdatum** | Datum, mit dem die Verarbeitung gebucht wird. |
| **Status** | Bearbeitungsstand des Belegs; **In Bearbeitung** kennzeichnet einen freigegebenen, noch nicht abgeschlossenen Beleg. |

### DropZone-Faktenbox

Die Faktenbox **DropZone** ist der zentrale Ablagebereich für Belege am Wareneingang. Sie wird an der Warenannahme und am gebuchten Wareneingang jeweils oben in den Faktenboxen angezeigt und ist stets mit der Belegnummer (**Nr.**) des aktuellen Belegs verknüpft.

**So legen Sie einen Beleg ab:** Öffnen Sie den Windows-Explorer, markieren Sie die gewünschte Datei und ziehen Sie sie mit gedrückter Maustaste in den Bereich **DropZone**. Lassen Sie die Datei dort los. Der Beleg wird gespeichert und unterhalb des Ablagebereichs in der Liste angezeigt.

| Feld / Aktion | Erläuterung |
|---|---|
| **DropZone** (Ablagebereich) | Wenn Sie eine Datei in diesen Bereich ziehen und ablegen, wird sie gespeichert und fest der aktuellen Warenannahme (über deren **Nr.** und die Quellart **Wareneingang**) zugeordnet; die Datei steht damit jederzeit wieder am Beleg zur Verfügung. |
| **Dateiname** | Zeigt je Zeile den Namen der abgelegten Datei an; wählen Sie eine Zeile aus, um die Aktion für genau diesen Beleg auszuführen. |
| **Datei herunterladen** | Wenn Sie eine Zeile markieren und diese Aktion ausführen, wird die zugehörige Datei auf Ihr Gerät heruntergeladen; so rufen Sie einen zuvor abgelegten Beleg (z. B. den Lieferschein) wieder ab. |

> Die abgelegten Belege lassen sich in der DropZone anzeigen und wieder herunterladen. Nicht mehr benötigte Belege können am offenen Beleg wieder entfernt werden; beim Löschen der offenen Warenannahme werden die zugehörigen Belege automatisch mitgelöscht (siehe **Verarbeitungs- und Buchungsablauf**).

### Aktion „Bild aufnehmen“

An der **Warenannahme** steht in der Menüband-Kategorie **Verarbeitung** die angeheftete (promoted) Aktion **Bild aufnehmen** zur Verfügung.

| Aktion | Erläuterung |
|---|---|
| **Bild aufnehmen** | Wenn Sie diese Aktion ausführen, öffnet sich die Kamerafunktion des Geräts; nach dem Aufnehmen wird das Foto automatisch als Beleg zur aktuellen Warenannahme gespeichert und erscheint in der Faktenbox **DropZone** in der Liste (**Dateiname**). So dokumentieren Sie z. B. den Zustand der angelieferten Ware ohne separaten Upload. |

**Ablauf im Detail:** Nach dem Auslösen der Aktion nehmen Sie im Kameradialog das Bild auf und bestätigen es. Das System vergibt automatisch einen Dateinamen aus Belegnummer und laufender Nummer (Beispiel: `WA00012_3.jpg`) und legt das Bild als weiteren Beleg der Warenannahme ab. Diese Aktion ist besonders für die Erfassung über Tablet oder Smartphone in der Webanwendung geeignet.

### Verarbeitungs- und Buchungsablauf

Die Belegdokumentation folgt dem Verarbeitungsweg des Moduls Warenvereinnahmung. Die Erweiterung greift dabei automatisch ein — sie besitzt keine eigene Buchungsaktion, sondern reagiert auf die Verarbeitung des Basismoduls:

1. **Warenannahme öffnen** und Belege bzw. Fotos in die **DropZone** ablegen (Aktionen **Bild aufnehmen**, Ziehen und Ablegen).
2. **Freigeben** (Aktion **Freigeben**): Der Beleg wird freigegeben und für die weitere Verarbeitung vorbereitet.
3. **Verarbeitung** (Kategorie **Verarbeitung**): Über die Verarbeitungsfunktionen des Basismoduls wird die Warenannahme verarbeitet; dabei entsteht der **gebuchte Wareneingang** (Geb. Wareneingang).
4. **Automatische Belegübertragung:** In dem Moment, in dem der gebuchte Wareneingang entsteht bzw. aktualisiert wird, überträgt die Erweiterung alle in der DropZone abgelegten Belege der offenen Warenannahme (Quellart **Wareneingang**) auf den gebuchten Wareneingang (Quellart **Geb. Wareneingang**). Die Zuordnung erfolgt über die **Herkunftsbelegnr.** des gebuchten Belegs.
5. **Ergebnis am gebuchten Wareneingang:** Öffnen Sie den gebuchten Wareneingang; in dessen Faktenbox **DropZone** sind dieselben Belege sichtbar und über **Datei herunterladen** abrufbar. Die Kopffelder **Verarbeitet von Benutzer-ID** und **Verarbeitet am** dokumentieren, wer wann verarbeitet hat; das Feld **Storno** kennzeichnet Korrekturbelege.
6. **Löschen einer offenen Warenannahme:** Wird eine noch offene Warenannahme gelöscht, entfernt die Erweiterung automatisch die zugehörigen abgelegten Belege (Quellart **Wareneingang**), damit keine verwaisten Dokumente zurückbleiben.

> Es gibt keine Vorgabe, dass alle Belege abgelegt sein müssen, bevor verarbeitet werden darf — die Dokumentenablage ist unabhängig vom Buchungsstatus. Bereits abgelegte Belege bleiben nach der Verarbeitung am gebuchten Wareneingang erhalten.

## Quellarten der Belegablage

Die Erweiterung unterscheidet, an welchem Belegtyp ein Beleg hängt. Dazu ergänzt sie die Quellart der Medienspeicherung um zwei Werte. Jeder abgelegte Beleg trägt genau eine dieser Quellarten:

| Wert | Erläuterung |
|---|---|
| **Wareneingang** | Wenn ein Beleg diese Quellart trägt, ist er einer **offenen Warenannahme** zugeordnet. Solche Belege werden bei der Verarbeitung auf den gebuchten Wareneingang übertragen und beim Löschen der offenen Warenannahme entfernt. |
| **Geb. Wareneingang** | Wenn ein Beleg diese Quellart trägt, ist er dem **gebuchten Wareneingang** zugeordnet. Diese Belege entstehen automatisch bei der Verarbeitung aus den Belegen der Quellart **Wareneingang** und bleiben dauerhaft am gebuchten Beleg erhalten. |

> Diese Quellarten steuern die automatische Zuordnung im Hintergrund; der Anwender wählt sie nicht manuell aus. Sie erklären, warum ein an der Warenannahme abgelegter Beleg nach der Verarbeitung am gebuchten Wareneingang wieder auftaucht.

## Typische Anwendungsfälle

### Lieferschein beim Wareneingang ablegen

**Auslöser:** Mit der Ware trifft ein Lieferschein in Papierform ein, der digital am Vorgang hinterlegt werden soll.

**Einstieg in BC:** Der Anwender öffnet im Modul Warenvereinnahmung die betreffende **Warenannahme**.

**Kernablauf:** Der Lieferschein wird eingescannt und die Datei per Ziehen und Ablegen in die Faktenbox **DropZone** gezogen. Sie erscheint sofort unter **Dateiname**. Anschließend gibt der Anwender die Warenannahme über **Freigeben** frei und startet die **Verarbeitung**.

**Abschluss:** Am automatisch entstehenden **gebuchten Wareneingang** ist der Lieferschein in der DropZone weiterhin vorhanden und kann jederzeit über **Datei herunterladen** aufgerufen werden.

### Foto der Ware direkt am Wareneingang aufnehmen

**Auslöser:** Beim Entladen fällt eine Transportbeschädigung auf, die fotografisch festgehalten werden soll.

**Einstieg in BC:** Der Anwender öffnet an einem Tablet oder Smartphone in der Webanwendung die **Warenannahme** des Vorgangs.

**Kernablauf:** Über die angeheftete Aktion **Bild aufnehmen** öffnet der Anwender die Kamera, nimmt ein Foto der beschädigten Ware auf und bestätigt es. Das Bild wird automatisch als Beleg gespeichert und erscheint in der DropZone unter **Dateiname**. Bei Bedarf werden weitere Fotos ergänzt.

**Abschluss:** Nach **Freigeben** und **Verarbeitung** liegen die Fotos am gebuchten Wareneingang und stehen für spätere Reklamations- oder Prüfvorgänge zur Verfügung.

### Belege wandern automatisch zum gebuchten Beleg

**Auslöser:** Ein Kollege hat an der Warenannahme bereits Zertifikate und Fotos abgelegt; der Vorgang soll nun abgeschlossen werden.

**Einstieg in BC:** Der Anwender öffnet die vorbereitete **Warenannahme**.

**Kernablauf:** Der Anwender prüft die in der DropZone gelisteten Belege, gibt den Beleg mit **Freigeben** frei und löst die **Verarbeitung** aus. Es ist kein manuelles Kopieren der Belege nötig.

**Abschluss:** Die Erweiterung überträgt alle Belege automatisch auf den **gebuchten Wareneingang** (Quellart **Geb. Wareneingang**). Der Anwender öffnet den gebuchten Beleg und findet dort dieselbe Dokumentation wieder — verknüpft über die **Herkunftsbelegnr.**

## FAQ und Troubleshooting

### 1. Warum sehe ich an der Warenannahme keine DropZone?
Die Faktenbox erscheint nur, wenn die App **m+m Goods Receipt with Dropzone** und ihre abhängigen Apps (**m+m Dropzone**, **m+m Media Storage**, **m+m Goods Receipt**) installiert sind. Prüfen Sie außerdem, ob die Faktenboxen im Seitenbereich eingeblendet sind.

### 2. Wie füge ich einen Beleg hinzu?
Ziehen Sie die Datei mit gedrückter Maustaste aus dem Windows-Explorer in den Bereich **DropZone** und lassen Sie sie los. Alternativ nutzen Sie an der Warenannahme die Aktion **Bild aufnehmen**, um ein Foto über die Kamera aufzunehmen.

### 3. Was passiert mit meinen Belegen, wenn ich die Warenannahme verarbeite?
Bei der Verarbeitung entsteht der **gebuchte Wareneingang**. Alle an der Warenannahme abgelegten Belege werden dabei automatisch auf diesen gebuchten Beleg übertragen und bleiben dort erhalten.

### 4. Muss ich die Belege nach dem Verarbeiten manuell übertragen?
Nein. Die Übertragung erfolgt automatisch, sobald der gebuchte Wareneingang entsteht oder aktualisiert wird. Ein manuelles Kopieren ist nicht vorgesehen.

### 5. Warum finde ich einen abgelegten Beleg nach dem Löschen der Warenannahme nicht mehr?
Wird eine noch **offene** Warenannahme gelöscht, entfernt die Erweiterung automatisch die zu diesem Beleg abgelegten Dateien, damit keine verwaisten Dokumente zurückbleiben. Nach der Verarbeitung liegen die Belege am gebuchten Wareneingang und sind vom Löschen der offenen Warenannahme nicht betroffen.

### 6. Wie rufe ich einen abgelegten Beleg wieder ab?
Markieren Sie in der DropZone die gewünschte Zeile (**Dateiname**) und führen Sie die Aktion **Datei herunterladen** aus. Die Datei wird auf Ihr Gerät heruntergeladen.

### 7. Wo finde ich die mit „Bild aufnehmen“ erstellten Fotos wieder?
Die aufgenommenen Fotos erscheinen unmittelbar in der Faktenbox **DropZone** der Warenannahme (Liste **Dateiname**) und werden bei der Verarbeitung an den gebuchten Wareneingang übertragen.

### 8. Muss ich zunächst etwas einrichten, bevor ich Belege ablegen kann?
Nein. Für diese Erweiterung ist keine fachliche Einrichtung erforderlich. Es genügt, dass die App und ihre abhängigen Apps installiert sind.

### 9. Kann ich mehrere Belege zu einer Warenannahme ablegen?
Ja. Sie können beliebig viele Dateien ablegen und mehrere Fotos aufnehmen; jeder Beleg wird als eigene Zeile mit eigenem **Dateinamen** geführt.

### 10. Warum unterscheidet das System zwischen „Wareneingang“ und „Geb. Wareneingang“?
Diese beiden Quellarten kennzeichnen, ob ein Beleg an einer **offenen** Warenannahme (**Wareneingang**) oder am **gebuchten** Wareneingang (**Geb. Wareneingang**) hängt. Die Unterscheidung steuert die automatische Übertragung bei der Verarbeitung und das Aufräumen beim Löschen offener Belege.
