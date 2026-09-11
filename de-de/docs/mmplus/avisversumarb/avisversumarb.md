---
title: Anwenderhandbuch m+m Logistic Mgt. with Metal Tolling
---

# Anwenderhandbuch m+m Logistic Mgt. with Metal Tolling

## Einleitung

Die Erweiterung **m+m Logistic Mgt. with Metal Tolling** verbindet zwei bestehende m+m-Module miteinander: die **Metallaufträge** aus *m+m Metal & Tolling* und die **Versandplanung** aus *m+m Logistic Management*. Ohne diese Erweiterung werden Metallaufträge und die Versandplanung getrennt geführt. Mit ihr können freigegebene Metallaufträge direkt in der **Versandplanung** aufgerufen, den Versandplanungszeilen zugewiesen und über den normalen Warenausgang gebucht werden.

Der Nutzen für den Betrieb: Ein Metallauftrag, der einen Warenein- oder -ausgang auslöst, muss nicht mehr als separater Beleg zur Tourenplanung erfasst werden. Er erscheint in derselben **Versandplanung**, in der auch Verkaufs- und Umlagerungsaufträge zusammengestellt werden, und lässt sich zusammen mit diesen zu einer Liefertour gruppieren.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender in der Logistik und im Versand**, die täglich mit der **Versandplanung** arbeiten: Sie wählen Metallaufträge aus, weisen sie einer Versandplanung zu und stoßen den Warenausgang an. **Sekundär** angesprochen sind Administratorinnen und Administratoren, die einmalig die Adressquelle für die Versandplanung in der **Metall & Umarbeitung Einrichtung** festlegen, sowie Sachbearbeiter, die am **Metallauftrag** die Liefertour hinterlegen.

**Kurzer Prozessüberblick.** Der typische Weg verläuft in dieser Reihenfolge:

1. Einmalige **Einrichtung**: In der **Metall & Umarbeitung Einrichtung** legt der Administrator im Register **Avisierung & Versandplanung** fest, welche Adresse des Metallauftrags in die Versandplanung übernommen wird.
2. **Stammdaten am Beleg**: Am **Metallauftrag** wird bei Bedarf ein **Liefertourcode** hinterlegt; das Feld **Verfügbar für Versandplanung** steuert, ob der Auftrag zur Zuweisung angeboten wird.
3. **Tägliche Arbeit**: In der **Versandplanung** öffnet der Anwender den Bereich **Metallaufträge für Zuordnung**, wählt Aufträge aus und übernimmt sie mit **Zeilen zur Versandplanung hinzufügen**.
4. **Abschluss**: Die Versandplanung wird im Basismodul freigegeben, der **Warenausgang** wird erzeugt und gebucht. Wird die Lieferung zum Metallauftrag gebucht (**Geliefert**), setzt das System die zugehörigen Versandplanungszeilen automatisch auf **Beendet**.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg von einem freigegebenen Metallauftrag bis zum gebuchten Warenausgang. Die Einrichtung (Schritt 0) erfolgt nur einmalig; die Schritte 1 bis 6 sind der tägliche Ablauf.

0. **Einrichtung (einmalig, Administrator).** Öffnen Sie über **Suchen** die **Metall & Umarbeitung Einrichtung** und setzen Sie im Register **Avisierung & Versandplanung** das Feld **Metallauftragadresse für Versandplanung** auf den gewünschten Wert (**Standard**, **Lieferung an** oder **Abholung**). Ohne diese Auswahl greift der Standard.
1. **Metallauftrag vorbereiten.** Stellen Sie sicher, dass der Metallauftrag den **Status** **Freigegeben** (oder **Geprüft**) hat und dass **Verfügbar für Versandplanung** = Ja gesetzt ist. Hinterlegen Sie bei Bedarf am Metallauftrag den **Liefertourcode**.
2. **Versandplanung öffnen.** Öffnen Sie die **Versandplanung** und wählen Sie den Versandplanungssatz aus, dem die Metallaufträge zugewiesen werden sollen. Der Bereich **Metallaufträge für Zuordnung** ist sichtbar, solange die Liefertour **nicht** als **Interne Logistik** gekennzeichnet ist.
3. **Metallaufträge auswählen.** Markieren Sie im Bereich **Metallaufträge für Zuordnung** die gewünschten Zeilen und wählen Sie **Zeilen auswählen** (Strg+1). Falsch markierte Zeilen entfernen Sie mit **Zeilen entfernen** (Strg+2). Mit **Ausgewählte Zeilen anzeigen** (Strg+4) und **Alle Zeilen anzeigen** (Strg+3) schalten Sie die Ansicht um.
4. **Übernahme in die Versandplanung.** Wählen Sie **Zeilen zur Versandplanung hinzufügen** (Strg+I). Für jeden ausgewählten Metallauftrag wird eine Versandplanungszeile erzeugt; der Auftrag wird anschließend nicht mehr zur Zuweisung angeboten (**Verfügbar für Versandplanung** = Nein).
5. **Freigeben und Warenausgang buchen.** Vervollständigen Sie die Versandplanung im Basismodul, geben Sie sie über **Freigeben** frei und erzeugen bzw. buchen Sie den **Warenausgang**.
6. **Abschluss.** Buchen Sie die Lieferung zum Metallauftrag. Sobald der Metallauftrag den **Status** **Geliefert** erreicht, setzt das System die zugehörigen Versandplanungszeilen automatisch auf **Beendet**; ein manuelles Schließen ist nicht nötig.

## Einrichtung

Die Einrichtung dieser Erweiterung ist bewusst schlank: Sie fügt der bestehenden **Metall & Umarbeitung Einrichtung** genau **ein** Feld hinzu. Alle übrigen Felder dieser Karte gehören zum Basismodul *m+m Metal & Tolling* und werden dort gepflegt. Der folgende Abschnitt beschreibt vollständig, was diese Erweiterung an der Einrichtung ergänzt und wie diese Einstellung in die tägliche Versandplanung einfließt.

### Adressquelle für die Versandplanung einrichten

**Prozess.** Diese Einstellung nimmt der Administrator oder Key-User **einmalig vor der ersten Nutzung** vor. Sie legt fest, welche der am Metallauftrag geführten Adressen (Debitor/Kreditor, Anlieferung oder Abholung) beim Zusammenstellen der Versandplanung als **Lieferadresse** herangezogen wird. Die Auswahl wirkt sich unmittelbar auf die **Metallaufträge für Zuordnung** und auf die erzeugten Versandplanungszeilen aus (Querverweis: Abschnitt *Metallaufträge für Zuordnung* und *Versandplanung-Integration*).

**Einstieg:** Öffnen Sie über **Suchen** die **Metall & Umarbeitung Einrichtung** und wählen Sie das Register **Avisierung & Versandplanung**. Es handelt sich um eine unternehmensweite Einrichtung (ein Datensatz je Mandant); es gibt keine übergeordnete Liste, daher ist der Zugriff über **Suchen** der vorgesehene Weg.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Metallauftragadresse für Versandplanung** | Legt die Adressquelle fest, die beim Abruf der Metallaufträge in die Versandplanung übernommen wird. Der ausgewählte Wert steuert, welche Anschriftsfelder des Metallauftrags in die Versandplanungszeile (Lief.-an-Daten) geschrieben werden und nach welcher Anschrift bei der Gruppierung nach **Lief. an Adresse** zusammengefasst wird. **Wenn** hier ein Wert gesetzt ist, **dann** verwendet das System bei jeder Übernahme genau diese Adressquelle für alle Metallaufträge einheitlich. |

**Werte des Feldes Metallauftragadresse für Versandplanung** (Optionsfeld — jeder Wert im Detail):

- **Standard:** Es wird die Anlieferadresse des Metallauftrags (Lief.-an-Daten) übernommen. **Wenn** gewählt, **dann** schreibt das System **Lief. an Code**, **Anlieferung Name**, **Anlieferadresse**, **Anlieferung Ort** usw. in die Versandplanungszeile und gruppiert danach.
- **Lieferung an:** Verhält sich wie **Standard** und übernimmt ebenfalls die Anlieferadresse (Lief.-an-Daten) des Metallauftrags. **Wenn** gewählt, **dann** werden dieselben Anlieferfelder wie bei **Standard** herangezogen.
- **Abholung:** Es wird die **Abhol**adresse des Metallauftrags übernommen. **Wenn** gewählt, **dann** schreibt das System **Abholung Nr.**, **Abholung Name**, **Abholung Ort** usw. in die Versandplanungszeile und gruppiert nach der Abholanschrift — sinnvoll, wenn die Ware beim Lieferanten bzw. am Abholort disponiert wird und nicht an der Anlieferadresse.

**Numerierte Freischaltung (Reihenfolge aus dem Code):**

1. **Zuerst** setzen Sie in der **Metall & Umarbeitung Einrichtung** das Feld **Metallauftragadresse für Versandplanung**. **Wenn** gesetzt, **dann** steht die Adresslogik für alle folgenden Übernahmen bereit.
2. **Danach** stellen die Sachbearbeiter am **Metallauftrag** sicher, dass **Verfügbar für Versandplanung** = Ja und der **Status** **Freigegeben** oder **Geprüft** ist (siehe Abschnitt *Stammdaten und Belegdaten am Metallauftrag*).
3. **Schließlich** übernehmen die Anwender die Aufträge im Tagesablauf über **Zeilen zur Versandplanung hinzufügen** in der **Versandplanung** (Querverweis: *Metallaufträge für Zuordnung*).

**Abhängigkeit.** Die Adressauswahl greift bei jeder Übernahme automatisch; sie muss nicht je Auftrag wiederholt werden. Eine Änderung wirkt erst auf **künftige** Übernahmen — bereits erzeugte Versandplanungszeilen behalten ihre übernommene Adresse.

## Stammdaten und Belegdaten am Metallauftrag

Der **Metallauftrag** ist der führende Beleg, aus dem die Versandplanung gespeist wird. Diese Erweiterung ergänzt die Metallauftragskarte um vier Felder: eines steuert die Liefertour, drei zeigen den Bezug zur Versandplanung an.

**Prozess.** Diese Felder pflegen bzw. beobachten die Sachbearbeiter im Tagesgeschäft am Metallauftrag, **bevor** und **nachdem** der Auftrag in die Versandplanung übernommen wird. Der **Liefertourcode** wird aktiv gesetzt; die drei übrigen Felder werden vom System geführt und dienen der Kontrolle. Die Werte erscheinen anschließend in der Liste **Metallaufträge für Zuordnung** und steuern, ob und wie der Auftrag dort angeboten wird (Querverweis: *Metallaufträge für Zuordnung*, *Adressquelle für die Versandplanung einrichten*).

**Einstieg:** Öffnen Sie die Liste **Metallaufträge** und wählen Sie den gewünschten **Metallauftrag** aus, um die Karte zu öffnen. Der **Liefertourcode** liegt im Register mit den Anlieferdaten (Anlieferadresse); die drei Versandplanungsfelder liegen im Bereich der zugehörigen Belege.

| Feld | Erläuterung |
|------|-------------|
| **Liefertourcode** | Ordnet den Metallauftrag einer Liefertour zu. **Wenn** ein Liefertourcode gesetzt wird, **dann** übernimmt das System — sofern an der Liefertour ein **Zusteller** hinterlegt ist — diesen Zusteller in den Metallauftrag; außerdem wird der Auftrag in der Versandplanung nach dieser Liefertour filter- und gruppierbar. Ohne Liefertourcode bleibt der Auftrag ohne Tourbezug und muss in der Versandplanung ohne Tourfilter gesucht werden. |
| **Versandplanungszeilen** | Zeigt die Anzahl der offenen Versandplanungszeilen, die auf diesen Metallauftrag verweisen (berechnetes Feld). **Wenn** dieser Wert größer als 0 ist, **dann** wurde der Auftrag bereits mindestens einer Versandplanung zugewiesen und wird nicht erneut zur Zuordnung angeboten. |
| **Reg. Versandplanungszeilen** | Zeigt die Anzahl der bereits **registrierten** Versandplanungszeilen zu diesem Metallauftrag (berechnetes Feld). **Wenn** dieser Wert größer als 0 ist, **dann** ist die Versandplanung für diesen Auftrag bereits registriert (weiter verarbeitet) und der Auftrag bleibt für die Zuordnung gesperrt, bis keine registrierte Zeile mehr besteht. |
| **Verfügbar für Versandplanung** | Kennzeichnet, ob der Metallauftrag im Bereich **Metallaufträge für Zuordnung** angeboten wird (nicht manuell editierbar, Vorgabewert Ja). **Wenn** = Ja, **dann** erscheint der Auftrag zur Auswahl; sobald er einer Versandplanung hinzugefügt wird, setzt das System das Feld automatisch auf Nein. **Wenn** die zugehörige Versandplanungszeile später gelöscht wird und keine registrierte Zeile mehr besteht, **dann** setzt das System das Feld wieder auf Ja, und der Auftrag steht erneut zur Zuordnung bereit. |

**Statusabhängigkeit.** Zur Zuordnung angeboten werden ausschließlich Metallaufträge mit **Status** **Freigegeben** oder **Geprüft** (und **Verfügbar für Versandplanung** = Ja). Die Statuswerte des Metallauftrags bedeuten:

- **Offen:** Eingaben am Auftrag sind möglich; der Auftrag erscheint **nicht** zur Zuordnung.
- **Freigegeben:** Der Auftrag ist geprüft/freigegeben und wird zur Versandplanung angeboten.
- **Geprüft:** Optionaler Status; der Auftrag wird ebenfalls zur Versandplanung angeboten.
- **Geliefert:** Wird vom System gesetzt, sobald die Lieferung zum Metallauftrag gebucht ist; dann werden die zugehörigen Versandplanungszeilen automatisch **beendet** (siehe *Buchungs- und Abschlussverhalten*).

## Metallaufträge für Zuordnung

Die Seite **Metallaufträge für Zuordnung** ist der zentrale Arbeitsbereich dieser Erweiterung. Sie erscheint **eingebettet** in der **Versandplanung** (nicht als eigenständige Seite) und listet die zur Zuweisung verfügbaren Metallaufträge. Der Anwender markiert hier Aufträge und übernimmt sie in die Versandplanung.

**Einstieg:** Öffnen Sie die **Versandplanung**, wählen Sie den Versandplanungssatz und ggf. optional die gewünschte Liefertour; der Bereich **Metallaufträge für Zuordnung** wird darunter angezeigt. Die Liste ist nicht editierbar; gearbeitet wird ausschließlich über die Aktionen.

**Sichtbare Spalten.** Die Liste zeigt zu jedem Metallauftrag die folgenden Spalten:

| Feld | Erläuterung |
|------|-------------|
| **Ausgewählt** | Markierung, ob die Zeile für die Übernahme ausgewählt ist. **Wenn** markiert, **dann** wird der Auftrag bei **Zeilen zur Versandplanung hinzufügen** berücksichtigt. |
| **Nr.** | Nummer des Metallauftrags; identifiziert den Beleg eindeutig. |
| **Vorlage** | Zeigt die Vorlagenart des Metallauftrags (z. B. Ein- oder Verkaufsvorgang) und hilft, gleichartige Aufträge in der Liste zu unterscheiden. |
| **Debitor-/Kreditorart** | Gibt an, ob der Auftrag einem Debitor oder einem Kreditor zugeordnet ist; bestimmt zusammen mit der **Lieferrichtung** die spätere Lief.-an-Art der Versandplanungszeile. |
| **Debitor-/Kreditor Nr.** | Nummer des zugeordneten Debitors bzw. Kreditors. |
| **Debitor-/Kreditor Name** | Name des zugeordneten Debitors bzw. Kreditors zur schnellen Identifikation in der Liste. |
| **Debitor-/Kreditor Ort** | Ort des Debitors bzw. Kreditors; unterstützt die Orientierung nach Region. |
| **Lieferrichtung** | Gibt die Richtung der Bewegung an (Lagerortcode oder Debitor/Kreditor). **Wenn** Lagerortcode, **dann** wird die Versandplanungszeile als Lagerlieferung geführt; **wenn** Debitor/Kreditor, **dann** richtet sich die Lief.-an-Art nach der **Debitor-/Kreditorart**. |
| **Anliefer-/Abholdatum** | Termin der Anlieferung bzw. Abholung; dient als Datumsfilter beim Zusammenstellen der Tour und wird als Warenausgangsdatum in die Planung übernommen. |
| **Liefertourcode** | Zeigt die am Metallauftrag hinterlegte Liefertour; erlaubt die Gruppierung mehrerer Aufträge zu einer Tour. |
| **Abholung Name** | Name der Abholanschrift des Metallauftrags zur Kontrolle des Abholorts vor der Übernahme. |
| **Anlieferung Name** | Name der Anlieferanschrift des Metallauftrags zur Kontrolle des Lieferziels vor der Übernahme. |
| **Anlieferung Ort** | Ort der Anlieferanschrift zur schnellen Orientierung nach Zielregion. |
| **Abholung Ort** | Ort der Abholanschrift zur schnellen Orientierung nach Abholregion. |

Weitere Adress- und Detailspalten (z. B. vollständige Anschrift, Postleitzahl, Länder-/Regionscode, Lieferbedingungs- und Zustellerdaten sowie die einzelnen Anlieferungs- und Abhol-Detailfelder) sind standardmäßig **ausgeblendet** und können bei Bedarf über die Personalisierung eingeblendet werden; sie enthalten die vollständigen Anschriftsdaten aus dem Metallauftrag.

**Aktionen.** Alle Arbeitsschritte erfolgen über zwei Aktionsgruppen:

Gruppe **Auswahl**:

| Aktion | Erläuterung |
|--------|-------------|
| **Zeilen auswählen** (Strg+1) | Markiert die aktuell ausgewählten Zeilen für die Übernahme. **Wenn** ausgeführt, **dann** werden die betroffenen Aufträge in der Spalte **Ausgewählt** gekennzeichnet. |
| **Zeilen entfernen** (Strg+2) | Hebt die Markierung der ausgewählten Zeilen wieder auf. |
| **Alle Zeilen anzeigen** (Strg+3) | Zeigt alle verfügbaren Metallaufträge, unabhängig von der Markierung. |
| **Ausgewählte Zeilen anzeigen** (Strg+4) | Blendet die Liste auf die markierten Zeilen ein, um die Auswahl vor der Übernahme zu prüfen. |

Gruppe **Funktionen**:

| Aktion | Erläuterung |
|--------|-------------|
| **Zeilen zur Versandplanung hinzufügen** (Strg+I) | Übernimmt alle markierten Metallaufträge als Versandplanungszeilen. **Wenn** ausgeführt, **dann** erzeugt das System je Auftrag eine Zeile mit Artikel, **Menge für Zuweisung** (aus dem **Gesamtnettogewicht**), Gewichten, Lagerort und der gemäß Einrichtung gewählten Lief.-an-Adresse; anschließend wird jeder übernommene Auftrag auf **Verfügbar für Versandplanung** = Nein gesetzt und die Liste aktualisiert. |

Gruppe **Zeile**:

| Aktion | Erläuterung |
|--------|-------------|
| **Beleg anzeigen** (Umschalt+F7) | Öffnet den zur markierten Zeile gehörenden Metallauftrag, um den Quellbeleg vor der Übernahme zu prüfen. |

## Versandplanung-Integration

Diese Erweiterung ergänzt die **Versandplanung** des Basismoduls um den eingebetteten Bereich **Metallaufträge für Zuordnung** sowie um eine Aktion, mit der die zugewiesenen Metallaufträge aufgerufen werden. Damit reihen sich Metallaufträge nahtlos neben Verkaufs- und Umlagerungsaufträgen in denselben Planungsablauf ein.

**Prozess.** Der Anwender arbeitet weiterhin in der gewohnten **Versandplanung**; die Metallaufträge werden dort mitgeführt. Ob der Zuordnungsbereich sichtbar ist, hängt von der Liefertour ab.

| Feld/Aktion | Erläuterung |
|-------------|-------------|
| Bereich **Metallaufträge für Zuordnung** (eingebettet) | Zeigt die zur Zuweisung verfügbaren Metallaufträge zum aktuellen Versandplanungssatz. **Wenn** die zugeordnete Liefertour **nicht** als **Interne Logistik** gekennzeichnet ist, **dann** wird der Bereich eingeblendet; bei interner Logistik bleibt er ausgeblendet, da hier keine externe Tourenzusammenstellung erfolgt. |
| Aktion **Metallaufträge** | Öffnet die Liste der Metallaufträge, die dem aktuellen Versandplanungssatz bereits zugewiesen sind. **Wenn** ausgeführt, **dann** zeigt das System genau die Metallaufträge, zu denen Versandplanungszeilen dieses Satzes bestehen — nützlich, um vom Planungssatz zurück auf die Quellbelege zu springen. |

**Adressherkunft.** Welche Anschrift beim Hinzufügen in die Versandplanungszeile geschrieben wird, bestimmt die Einrichtung **Metallauftragadresse für Versandplanung** (Querverweis: *Adressquelle für die Versandplanung einrichten*). Bei **Standard**/**Lieferung an** werden die Anlieferdaten, bei **Abholung** die Abholdaten übernommen.

## Buchungs- und Abschlussverhalten

Diese Erweiterung bucht selbst keinen Beleg. Der Warenausgang wird über die **Versandplanung** und den Warenausgang des Basismoduls gebucht (Freigeben → Warenausgang erzeugen → buchen). Die Erweiterung reagiert jedoch automatisch auf zwei Ereignisse und hält Metallauftrag und Versandplanung konsistent.

- **Nach dem Buchen der Lieferung zum Metallauftrag:** Erreicht der Metallauftrag den **Status** **Geliefert**, setzt das System alle zugehörigen Versandplanungszeilen dieses Auftrags automatisch auf **Beendet** und **Offen** = Nein. Der Anwender muss die Zeilen nicht manuell schließen.
- **Beim Löschen einer Versandplanungszeile:** Wird eine Versandplanungszeile zu einem Metallauftrag gelöscht und besteht keine registrierte Versandplanungszeile mehr zu diesem Auftrag, setzt das System **Verfügbar für Versandplanung** wieder auf Ja. Der Auftrag erscheint dann erneut im Bereich **Metallaufträge für Zuordnung**.

**Teilmengen.** Jeder Metallauftrag wird als Ganzes über sein **Gesamtnettogewicht** als eine Versandplanungszeile übernommen; eine Sperre gegen unvollständige Mengen besteht nicht. Ein Auftrag kann jederzeit entfernt und — nach Freigabe der Verfügbarkeit — erneut zugewiesen werden.

## Berechtigungen

Für den Betrieb der Erweiterung liefert m+m den Berechtigungssatz **MuM ASMT ALL** mit. Er ist zuweisbar und bestimmt die Berechtigungen für die Objekte dieser Erweiterung: die beiden Verarbeitungscodeunits sowie die Seite **Metallaufträge für Zuordnung**. Weisen Sie diesen Berechtigungssatz allen Anwendern zu, die in der Versandplanung mit Metallaufträgen arbeiten sollen. Der Satz legt fest, welche Aktionen die Anwender in diesem Bereich ausführen können; für die eigentliche Versandplanung und die Metallaufträge gelten zusätzlich die Berechtigungen der beiden Basismodule.

## FAQ und Troubleshooting

### 1. Warum erscheint ein Metallauftrag nicht im Bereich Metallaufträge für Zuordnung?
Der Auftrag wird nur angeboten, wenn sein **Status** **Freigegeben** oder **Geprüft** ist **und** **Verfügbar für Versandplanung** = Ja gesetzt ist. Ein Auftrag im Status **Offen** oder ein bereits zugewiesener Auftrag (Verfügbar = Nein) erscheint nicht.

### 2. Warum ist der Bereich Metallaufträge für Zuordnung gar nicht sichtbar?
Der Bereich wird ausgeblendet, wenn die Liefertour des Versandplanungssatzes als **Interne Logistik** gekennzeichnet ist. Wählen Sie einen Versandplanungssatz bzw. eine Liefertour ohne interne Logistik, damit der Bereich erscheint.

### 3. Was passiert, wenn ich Zeilen zur Versandplanung hinzufügen wähle?
Für jeden markierten Metallauftrag wird eine Versandplanungszeile mit Artikel, **Menge für Zuweisung** (aus dem Gesamtnettogewicht), Gewichten, Lagerort und der eingerichteten Lief.-an-Adresse erzeugt. Anschließend wird der Auftrag auf **Verfügbar für Versandplanung** = Nein gesetzt und verschwindet aus der Auswahlliste.

### 4. Warum kann ich denselben Metallauftrag nicht zweimal zuweisen?
Sobald ein Auftrag hinzugefügt wurde, steht **Verfügbar für Versandplanung** auf Nein und der Zähler **Versandplanungszeilen** ist größer als 0. Damit wird eine doppelte Zuweisung verhindert. Erst wenn die zugehörige Zeile gelöscht wird und keine registrierte Zeile mehr besteht, wird der Auftrag wieder freigegeben.

### 5. Wie mache ich eine falsche Zuweisung rückgängig?
Löschen Sie die betreffende Versandplanungszeile. Besteht danach keine registrierte Versandplanungszeile mehr zu diesem Metallauftrag, setzt das System **Verfügbar für Versandplanung** automatisch wieder auf Ja, und der Auftrag erscheint erneut zur Zuordnung.

### 6. Welche Adresse wird in die Versandplanungszeile übernommen?
Das steuert die Einrichtung **Metallauftragadresse für Versandplanung** in der **Metall & Umarbeitung Einrichtung**. Bei **Standard** und **Lieferung an** werden die Anlieferdaten, bei **Abholung** die Abholdaten des Metallauftrags übernommen.

### 7. Warum wird meine geänderte Adresseinrichtung bei alten Zeilen nicht wirksam?
Die Einstellung greift nur bei **neuen** Übernahmen. Bereits erzeugte Versandplanungszeilen behalten die Adresse, die zum Zeitpunkt der Übernahme gültig war. Entfernen und wiederholen Sie die Übernahme, wenn eine bestehende Zeile die neue Adressquelle nutzen soll.

### 8. Warum wurde die Versandplanungszeile automatisch auf Beendet gesetzt?
Sobald die Lieferung zum Metallauftrag gebucht wurde und der Auftrag den **Status** **Geliefert** erreicht, setzt das System alle zugehörigen Versandplanungszeilen automatisch auf **Beendet** und **Offen** = Nein. Das ist gewolltes Verhalten und erspart das manuelle Schließen.

### 9. Wie gelange ich von der Versandplanung zurück zu den zugewiesenen Metallaufträgen?
Verwenden Sie in der **Versandplanung** die Aktion **Metallaufträge**. Sie öffnet die Liste genau der Metallaufträge, zu denen Versandplanungszeilen des aktuellen Satzes bestehen.

### 10. Warum wird beim Setzen des Liefertourcodes ein Zusteller im Metallauftrag eingetragen?
Ist an der gewählten Liefertour ein **Zusteller** hinterlegt, übernimmt das System diesen beim Setzen des **Liefertourcodes** in den Metallauftrag. Dadurch ist der Auftrag konsistent einer Tour und deren Zusteller zugeordnet; die Angabe kann am Auftrag bei Bedarf überschrieben werden.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Ablauf aus Sicht der operativen Anwender. Alle Schritte und Bezeichnungen entsprechen den in dieser Erweiterung vorhandenen Seiten und Aktionen.

### Anwendungsfall 1: Freigegebenen Metallauftrag in die Tagesplanung übernehmen

**Auslöser.** Die Disposition meldet, dass ein freigegebener Metallauftrag heute ausgeliefert werden soll.

**Einstieg in BC.** Der Anwender prüft zunächst auf der **Metallauftrag**-Karte, dass der **Status** **Freigegeben** ist, **Verfügbar für Versandplanung** = Ja steht und ein passender **Liefertourcode** hinterlegt ist. Anschließend öffnet er die **Versandplanung** und wählt den Versandplanungssatz der Tour.

**Kernablauf.** Im eingeblendeten Bereich **Metallaufträge für Zuordnung** markiert der Anwender den Auftrag und wählt **Zeilen auswählen**. Mit **Ausgewählte Zeilen anzeigen** kontrolliert er die Auswahl und übernimmt sie über **Zeilen zur Versandplanung hinzufügen**. Das System erzeugt die Versandplanungszeile und sperrt den Auftrag gegen erneute Zuweisung.

**Abschluss.** Der Anwender gibt die Versandplanung im Basismodul über **Freigeben** frei, erzeugt und bucht den **Warenausgang**. Nach dem Buchen der Lieferung erreicht der Metallauftrag den Status **Geliefert**, und die Versandplanungszeile wird automatisch **beendet**.

### Anwendungsfall 2: Versehentlich zugewiesenen Auftrag korrigieren

**Auslöser.** Beim Zusammenstellen der Tour fällt auf, dass ein Metallauftrag der falschen Versandplanung zugeordnet wurde.

**Einstieg in BC.** Der Anwender öffnet die betroffene **Versandplanung** und ruft über die Aktion **Metallaufträge** die zugewiesenen Aufträge auf, um den falschen Beleg zu identifizieren.

**Kernablauf.** Er löscht die zugehörige Versandplanungszeile. Da keine registrierte Versandplanungszeile mehr zu diesem Metallauftrag besteht, setzt das System **Verfügbar für Versandplanung** automatisch wieder auf Ja.

**Abschluss.** Der Auftrag erscheint erneut im Bereich **Metallaufträge für Zuordnung** und kann der richtigen Versandplanung zugewiesen werden.

### Anwendungsfall 3: Abholung beim Lieferanten disponieren

**Auslöser.** Rohmetall soll beim Lieferanten abgeholt und in die Tourenplanung aufgenommen werden.

**Einstieg in BC.** Der Administrator hat in der **Metall & Umarbeitung Einrichtung** das Feld **Metallauftragadresse für Versandplanung** auf **Abholung** gesetzt, damit die Abholanschrift maßgeblich ist. Der Anwender öffnet die **Versandplanung** und den passenden Versandplanungssatz.

**Kernablauf.** Im Bereich **Metallaufträge für Zuordnung** markiert der Anwender den betreffenden Metallauftrag und übernimmt ihn mit **Zeilen zur Versandplanung hinzufügen**. In die Versandplanungszeile werden die **Abholung**-Daten (Abholung Name, Abholung Ort usw.) des Metallauftrags geschrieben.

**Abschluss.** Die Versandplanung wird freigegeben und der **Warenausgang** gebucht; die Abholung ist damit in der Tour berücksichtigt.
