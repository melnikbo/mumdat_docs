---
title: Anwenderhandbuch m+m Prod. Order Job Overview with Ext. Prod. Information
---

# Anwenderhandbuch m+m Prod. Order Job Overview with Ext. Prod. Information

## Einleitung

Die App **m+m Prod. Order Job Overview with Ext. Prod. Information** erweitert den **FA-Arbeitsvorrat** in Microsoft Dynamics 365 Business Central um eine zusätzliche Infobox (Factbox) mit der Bezeichnung **Erw. Fertigungseigenschaften**. In dieser Factbox werden zu dem gerade markierten Arbeitsgang die hinterlegten erweiterten Fertigungseigenschaften angezeigt – zum Beispiel Eigenschaftscode, Standardwert, Istwert, zulässiger Wertebereich, Einheit, Berechnungsformel und Datentyp.

Der praktische Nutzen: Der Anwender sieht die für einen Arbeitsgang relevanten Fertigungseigenschaften direkt neben der Arbeitsvorratszeile und muss nicht mehr zwischen der Übersicht und den Eigenschaftsseiten der Arbeitsplatzgruppe wechseln. Die Factbox folgt automatisch der markierten Zeile.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender in der Fertigungssteuerung** – Werker, Schichtmeister und Fertigungssteuerer, die im FA-Arbeitsvorrat die anstehenden Arbeitsgänge einer Arbeitsplatzgruppe abarbeiten und dabei die Sollvorgaben je Arbeitsgang benötigen. Sekundär profitieren Fertigungsplaner, die die Eigenschaften zuvor an der Arbeitsplatzgruppe bzw. am Arbeitsplan pflegen.

**Kurzer Prozessüberblick.** Ein Fertigungsplaner hinterlegt die erweiterten Fertigungseigenschaften an der Arbeitsplatzgruppe bzw. im Arbeitsplan (dies erfolgt in den zugrunde liegenden m+m-Modulen und ist Voraussetzung, siehe Abschnitt **Voraussetzungen**). Anschließend öffnet der operative Anwender den **FA-Arbeitsvorrat**, wählt seine **Arbeitsplatzgruppe** und liest zu jeder Arbeitsvorratszeile in der Factbox **Erw. Fertigungseigenschaften** die zugehörigen Werte ab.

Diese App fügt selbst keine Einrichtungsseiten, keine Stammdatenkarten, keine Belege, keine Buchungen und keine Berichte hinzu. Sie stellt ausschließlich die genannte Factbox im FA-Arbeitsvorrat bereit und verknüpft sie mit dem passenden Arbeitsgang.

## Schnellstart für Anwender

Der schnellste Weg zu den erweiterten Fertigungseigenschaften eines Arbeitsgangs:

1. Öffnen Sie über die **Suche** den **FA-Arbeitsvorrat**. Der FA-Arbeitsvorrat ist eine zentrale Übersichtsseite und wird direkt über die Suche aufgerufen; es gibt keine vorgelagerte Stammdatenzeile, über die er geöffnet würde.
2. Tragen Sie im Filterbereich unter **Arbeitsplatzgruppennr.** die gewünschte Arbeitsplatzgruppe ein. Die Übersicht zeigt daraufhin die Arbeitsgänge dieser Arbeitsplatzgruppe an; der Name erscheint schreibgeschützt unter **Arbeitsplatzgruppenname**.
3. Grenzen Sie die Liste bei Bedarf weiter ein: **Arbeitsplatznr.** (einzelner Arbeitsplatz innerhalb der Gruppe – optional), **FA-Nr.** (einzelner Fertigungsauftrag – optional) sowie **Datum**, **Sortierung**, **Beendete ausblenden** und **Offene ausblenden**.
4. Markieren Sie in der Zeilenliste den gewünschten **Arbeitsgang**.
5. Lesen Sie rechts in der Factbox **Erw. Fertigungseigenschaften** die zum markierten Arbeitsgang hinterlegten Eigenschaften ab. Wechseln Sie die markierte Zeile, aktualisiert sich die Factbox automatisch.

Sind zu einem Arbeitsgang keine Eigenschaften gepflegt, bleibt die Factbox leer – dann ist zunächst die Pflege gemäß Abschnitt **Voraussetzungen** erforderlich.

## Voraussetzungen

Damit die Factbox **Erw. Fertigungseigenschaften** Werte anzeigt, müssen zwei Bedingungen erfüllt sein:

- **App-Installation.** Diese App muss installiert sein. Eine gesonderte Einrichtung innerhalb der App ist nicht erforderlich: Nach der Installation erscheint die Factbox automatisch im FA-Arbeitsvorrat. Es gibt keine Einrichtungsseite und keine zu aktivierenden Schalter in dieser App.
- **Gepflegte Fertigungseigenschaften.** Die angezeigten Werte stammen aus den erweiterten Fertigungseigenschaften, die zuvor an der **Arbeitsplatzgruppe** bzw. im **Arbeitsplan** hinterlegt wurden. Diese Pflege erfolgt in den zugrunde liegenden m+m-Modulen (Materialeigenschaften und Erw. Fertigungsinformationen) und ist damit die eigentliche fachliche Voraussetzung. Wenn zu einem Arbeitsgang ein **Eigenschaftscode** mit Werten gepflegt ist, zeigt die Factbox diese Eigenschaft an; ist kein Eigenschaftscode hinterlegt, bleibt die Zeile in der Factbox aus.

Wenn also die Factbox bei einem Arbeitsgang leer bleibt, obwohl dort Eigenschaften erwartet werden, prüfen Sie zuerst, ob an der zugehörigen Arbeitsplatzgruppe bzw. im Arbeitsplan die erweiterten Fertigungseigenschaften gepflegt sind.

## Der FA-Arbeitsvorrat als Einstieg

Der FA-Arbeitsvorrat ist die Arbeitsoberfläche, an der diese App ansetzt. Er zeigt die Arbeitsgänge einer Arbeitsplatzgruppe als Liste. Die App verändert diese Liste selbst nicht – sie ergänzt lediglich rechts eine weitere Factbox. Damit Sie die richtige Zeile markieren und die Factbox die passenden Eigenschaften anzeigt, sind vor allem die folgenden Filter des FA-Arbeitsvorrats relevant.

### So folgt die Factbox der ausgewählten Zeile

Die Factbox **Erw. Fertigungseigenschaften** ist an die jeweils markierte Arbeitsvorratszeile gekoppelt. Intern verknüpft die App die Factbox über den **FA-Status**, die **FA-Nr.**, den **Arbeitsgang** und die Fertigungsauftragszeile der markierten Zeile mit den passenden erweiterten Fertigungseigenschaften. Für Sie als Anwender bedeutet das: Sie steuern die Anzeige allein durch die Zeilenauswahl – ein separates Öffnen oder Nachladen ist nicht nötig.

Die folgenden Filter des FA-Arbeitsvorrats bestimmen, welche Zeilen überhaupt angezeigt werden und damit, zu welchen Arbeitsgängen Sie die Factbox einsehen können. Sie gehören zur Basisübersicht; diese App verändert sie nicht, sie werden hier zur Orientierung beschrieben.

| Filterfeld | Erläuterung |
|---|---|
| **Arbeitsplatzgruppennr.** | Wenn gesetzt, werden die Arbeitsgänge auf die gewählte Arbeitsplatzgruppe eingegrenzt; die Übersicht lädt daraufhin deren Zeilen. Dies ist der übergeordnete Einstieg – ohne Arbeitsplatzgruppe bleibt die Liste leer. |
| **Arbeitsplatzgruppenname** | Wird schreibgeschützt aus der gewählten Arbeitsplatzgruppe übernommen; dient nur der Kontrolle, dass die richtige Gruppe eingestellt ist. |
| **Arbeitsplatznr.** | Wenn gesetzt, werden die Zeilen zusätzlich auf einen einzelnen Arbeitsplatz innerhalb der Gruppe eingegrenzt. Optional – die Auswahl auf Ebene der Arbeitsplatzgruppe genügt, wenn Sie alle Arbeitsplätze der Gruppe sehen möchten. |
| **Arbeitsplatzname** | Wird schreibgeschützt aus dem gewählten Arbeitsplatz übernommen; dient der Kontrolle. |
| **FA-Nr.** | Wenn gesetzt, werden nur die Arbeitsgänge des angegebenen (freigegebenen) Fertigungsauftrags angezeigt. Optional; ohne Angabe erscheinen alle passenden Fertigungsaufträge. |
| **Datum** | Wenn gesetzt, filtert die Übersicht auf das eingestellte Datum; damit blenden Sie z. B. tagesbezogen die relevanten Arbeitsgänge ein. |
| **Sortierung** | Legt fest, in welcher Reihenfolge die Arbeitsgänge angezeigt werden; ändert die Reihenfolge der Liste, nicht deren Inhalt. |
| **Beendete ausblenden** | Wenn aktiviert, werden bereits beendete Arbeitsgänge ausgeblendet, sodass Sie sich auf noch offene Arbeit konzentrieren. |
| **Offene ausblenden** | Wenn aktiviert, werden offene Arbeitsgänge ausgeblendet; nützlich, wenn Sie gezielt bereits erledigte Arbeitsgänge nachschlagen möchten. |

## Die Factbox „Erw. Fertigungseigenschaften"

Dies ist die einzige Oberfläche, die diese App hinzufügt, und zugleich ihr Kern. Die Factbox erscheint am rechten Rand des FA-Arbeitsvorrats. Sie zeigt je markiertem Arbeitsgang die zugehörigen erweiterten Fertigungseigenschaften als Liste. Die Felder sind Anzeigefelder – Sie lesen darin die Sollvorgaben und den erreichten Istwert ab; die Pflege der Werte erfolgt an der Arbeitsplatzgruppe bzw. im Arbeitsplan (siehe **Voraussetzungen**).

Die Factbox enthält folgende Spalten:

| Feld | Erläuterung |
|---|---|
| **Arbeitsgangnr.** | Zeigt den Arbeitsgang, zu dem die Eigenschaftszeile gehört. Wenn Sie im FA-Arbeitsvorrat eine Zeile markieren, sehen Sie hier, welchem Arbeitsgang die darunter aufgeführten Eigenschaften zugeordnet sind – so ordnen Sie die Werte eindeutig einem Arbeitsschritt zu. |
| **Beschreibung** | Zeigt den Klartext zur Eigenschaftszeile bzw. zum Arbeitsgang. Damit erkennen Sie ohne Rückgriff auf Codes, worum es bei der Eigenschaft geht. |
| **Eigenschaftscode** | Zeigt den Code der Fertigungseigenschaft. Wenn ein Eigenschaftscode gesetzt ist, gilt die Zeile als tatsächlich gepflegte Eigenschaft; Zeilen ohne Eigenschaftscode werden in dieser Factbox nicht angezeigt, sodass Sie nur relevante Eigenschaften sehen. |
| **Standardwert** | Zeigt den vorgegebenen Sollwert der Eigenschaft. An diesem Wert orientieren Sie sich, wenn Sie den Arbeitsgang ausführen; weicht der Istwert davon ab, ist das ein Hinweis auf eine Abweichung von der Vorgabe. |
| **Wert** | Zeigt den für diese konkrete Fertigung gültigen Wert der Eigenschaft. Wenn dieser Wert vom **Standardwert** abweicht, ist das die auftragsspezifische Vorgabe, die Vorrang vor dem allgemeinen Standard hat. |
| **Istwert** | Zeigt den tatsächlich erfassten Wert der Eigenschaft. Wenn ein Istwert vorliegt, können Sie ihn unmittelbar gegen **Standardwert** bzw. **Wert** vergleichen und so den Fertigungsstand des Arbeitsgangs beurteilen. |
| **Eigenschaftswertname** | Zeigt den Klarnamen zum eingestellten Wert, wenn die Eigenschaft mit einer Werteliste arbeitet. Damit lesen Sie einen kodierten Wert als verständliche Bezeichnung. |
| **Wert zulässig von** | Zeigt die untere Grenze des zulässigen Wertebereichs. Wenn der Istwert diese Grenze unterschreitet, liegt die Eigenschaft außerhalb der Vorgabe – ein direkter Prüfhinweis am Arbeitsplatz. |
| **Wert zulässig bis** | Zeigt die obere Grenze des zulässigen Wertebereichs. Wenn der Istwert diese Grenze überschreitet, liegt die Eigenschaft außerhalb der Vorgabe. |
| **Einheit** | Zeigt die Maßeinheit der Eigenschaft (z. B. für Länge, Gewicht oder Temperatur). Damit interpretieren Sie Standardwert, Wert und Istwert korrekt und vermeiden Verwechslungen der Größenordnung. |
| **Berechnungsformel** | Zeigt die hinterlegte Formel, mit der ein numerischer Wert der Eigenschaft berechnet wird. Wenn eine Formel gesetzt ist, ergibt sich der Wert rechnerisch und wird nicht frei eingetragen; das erklärt, warum ein Wert automatisch entsteht. |
| **Anzeigereihenfolge** | Bestimmt die Reihenfolge, in der die Eigenschaften in der Factbox erscheinen. Wenn die Reihenfolge gepflegt ist, stehen die für den Arbeitsgang wichtigsten Eigenschaften oben, sodass Sie das Wesentliche zuerst sehen. |
| **Datentyp** | Zeigt an, welche Art von Wert die Eigenschaft trägt. Der Datentyp bestimmt, wie **Wert**, **Standardwert** und **Istwert** zu lesen sind und ob ein zulässiger Wertebereich sinnvoll ist. Die Ausprägungen sind: |

Die möglichen Ausprägungen des Feldes **Datentyp**:

- **Text:** Die Eigenschaft trägt einen freien Textwert. Ein zulässiger Wertebereich (von/bis) und eine Berechnungsformel greifen hier nicht; Sie lesen den Wert als Zeichenfolge.
- **Dezimal:** Die Eigenschaft trägt einen Dezimalwert. Ein zulässiger Wertebereich **Wert zulässig von** / **Wert zulässig bis** ist auswertbar, und es kann eine **Berechnungsformel** hinterlegt sein.
- **Ganzzahl:** Die Eigenschaft trägt einen ganzzahligen Wert. Wie bei **Dezimal** sind Wertebereich und Berechnungsformel auswertbar, jedoch ohne Nachkommastellen.
- **Datum:** Die Eigenschaft trägt einen Datumswert. Der Wert ist als Datum zu lesen; ein numerischer Von-/Bis-Bereich mit Berechnungsformel ist hierfür nicht vorgesehen.

## Berechtigungen

Die App liefert den Berechtigungssatz **MuM PJAP Perm** mit. Er ist zuweisbar und bestimmt die Berechtigungen für die Ausführung der App-Logik, die die Factbox mit dem passenden Arbeitsgang verknüpft. Ordnen Sie diesen Berechtigungssatz den Benutzern zu, die im FA-Arbeitsvorrat mit den erweiterten Fertigungseigenschaften arbeiten. Der Berechtigungssatz legt fest, dass die zugehörige App-Funktion ausgeführt werden darf; die Sichtbarkeit der einzelnen Eigenschaftswerte selbst richtet sich nach den Berechtigungen der zugrunde liegenden Fertigungs- und Eigenschaftsdaten.

## FAQ und Troubleshooting

### 1. Warum sehe ich im FA-Arbeitsvorrat keine Factbox „Erw. Fertigungseigenschaften"?
Prüfen Sie, ob die App installiert ist und ob der Factbox-Bereich rechts eingeblendet ist. Die Factbox wird nach der Installation automatisch als zusätzliche Factbox im FA-Arbeitsvorrat angezeigt; ist der Factbox-Bereich zugeklappt, blenden Sie ihn über die Personalisierung wieder ein.

### 2. Warum bleibt die Factbox leer, obwohl ich eine Zeile markiert habe?
Zu dem markierten Arbeitsgang sind keine erweiterten Fertigungseigenschaften mit **Eigenschaftscode** gepflegt. Die Factbox zeigt nur Zeilen mit gesetztem Eigenschaftscode an. Pflegen Sie die Eigenschaften an der zugehörigen Arbeitsplatzgruppe bzw. im Arbeitsplan (siehe **Voraussetzungen**).

### 3. Muss ich in dieser App etwas einrichten, bevor ich sie nutzen kann?
Nein. Diese App besitzt keine Einrichtungsseite und keine zu setzenden Schalter. Nach der Installation ist die Factbox sofort verfügbar. Die fachliche Vorarbeit besteht ausschließlich in der Pflege der Fertigungseigenschaften an Arbeitsplatzgruppe bzw. Arbeitsplan.

### 4. Wie sorge ich dafür, dass die Factbox zum richtigen Arbeitsgang passt?
Markieren Sie im FA-Arbeitsvorrat die gewünschte Zeile. Die Factbox koppelt sich automatisch an **FA-Status**, **FA-Nr.**, **Arbeitsgang** und Fertigungsauftragszeile der markierten Zeile und zeigt genau die dazu passenden Eigenschaften. Ein manuelles Nachladen ist nicht nötig.

### 5. Warum weicht der Istwert vom Standardwert ab?
Der **Standardwert** ist die allgemeine Vorgabe, der **Wert** die auftragsspezifische Vorgabe und der **Istwert** der tatsächlich erfasste Wert. Eine Abweichung zwischen **Istwert** und **Standardwert**/**Wert** ist ein Hinweis darauf, dass die Fertigung von der Vorgabe abweicht – nutzen Sie diesen Vergleich zur Beurteilung des Arbeitsgangs.

### 6. Was bedeutet ein Eintrag unter „Wert zulässig von" und „Wert zulässig bis"?
Diese Felder geben den zulässigen Wertebereich der Eigenschaft an. Liegt der **Istwert** außerhalb dieses Bereichs, ist die Vorgabe nicht eingehalten. Der Bereich ist vor allem bei den Datentypen **Dezimal** und **Ganzzahl** auswertbar.

### 7. Warum kann ich einen Wert nicht direkt eintragen – er scheint berechnet zu werden?
Zu der Eigenschaft ist eine **Berechnungsformel** hinterlegt. In diesem Fall ergibt sich der Wert rechnerisch und wird nicht frei erfasst. Die Formel ist Bestandteil der Eigenschaftsdefinition und wird an der Arbeitsplatzgruppe bzw. im Arbeitsplan gepflegt.

### 8. In welcher Reihenfolge erscheinen die Eigenschaften in der Factbox?
Die Reihenfolge richtet sich nach dem Feld **Anzeigereihenfolge** der jeweiligen Eigenschaft. Ist die Anzeigereihenfolge gepflegt, stehen die wichtigsten Eigenschaften oben; andernfalls erscheinen sie in der Standardsortierung.

### 9. Woran erkenne ich, wie ein Wert zu lesen ist – als Zahl, Text oder Datum?
Am Feld **Datentyp**: **Text** kennzeichnet einen freien Textwert, **Dezimal** und **Ganzzahl** numerische Werte (mit bzw. ohne Nachkommastellen), **Datum** einen Datumswert. Der Datentyp bestimmt zugleich, ob ein zulässiger Wertebereich und eine Berechnungsformel sinnvoll sind.

### 10. Kann ich in der Factbox die Fertigungseigenschaften ändern?
Die Factbox im FA-Arbeitsvorrat dient der Anzeige der Sollvorgaben und des Istwerts zum Arbeitsgang. Die Pflege der Eigenschaften (Standardwerte, Wertebereiche, Formeln) erfolgt an der Arbeitsplatzgruppe bzw. im Arbeitsplan in den zugrunde liegenden Modulen, nicht in dieser Factbox.

## Typische Anwendungsfälle

Die folgenden Beispiele zeigen, wie die Factbox im Arbeitsalltag hilft. Alle beschriebenen Schritte beziehen sich ausschließlich auf den FA-Arbeitsvorrat und die Factbox **Erw. Fertigungseigenschaften**.

### Anwendungsfall 1: Sollwerte am Arbeitsgang prüfen

**Auslöser.** Ein Werker fragt beim Schichtmeister nach, welche Vorgaben für den nächsten Arbeitsgang an seiner Arbeitsplatzgruppe gelten.

**Einstieg in BC.** Der Schichtmeister öffnet über die **Suche** den **FA-Arbeitsvorrat** und trägt unter **Arbeitsplatzgruppennr.** die betreffende Arbeitsplatzgruppe ein. Optional grenzt er über **Arbeitsplatznr.** oder **FA-Nr.** weiter ein.

**Kernablauf.** In der Zeilenliste markiert er den fraglichen **Arbeitsgang**. Rechts in der Factbox **Erw. Fertigungseigenschaften** liest er zu diesem Arbeitsgang die Eigenschaften ab: **Eigenschaftscode**, **Standardwert** bzw. **Wert** als Vorgabe, **Einheit** zur richtigen Interpretation der Größenordnung sowie **Wert zulässig von** und **Wert zulässig bis** als zulässigen Bereich. Am **Datentyp** erkennt er, ob es sich um einen numerischen, einen Text- oder einen Datumswert handelt.

**Abschluss.** Der Schichtmeister gibt dem Werker die abgelesenen Sollvorgaben durch. Ein separater Buchungs- oder Druckschritt ist nicht erforderlich; die Factbox dient der Information.

### Anwendungsfall 2: Standard- und Istwert vor der Freigabe eines Arbeitsgangs vergleichen

**Auslöser.** Vor der internen Freigabe eines Arbeitsgangs soll geprüft werden, ob die erfassten Werte innerhalb der Vorgaben liegen.

**Einstieg in BC.** Der Fertigungssteuerer öffnet über die **Suche** den **FA-Arbeitsvorrat**, stellt die **Arbeitsplatzgruppennr.** ein und blendet mit **Beendete ausblenden** bereits abgeschlossene Arbeitsgänge aus, um sich auf die noch offenen zu konzentrieren.

**Kernablauf.** Er markiert den zu prüfenden **Arbeitsgang**. In der Factbox **Erw. Fertigungseigenschaften** vergleicht er zeilenweise den **Istwert** mit **Standardwert** bzw. **Wert** und prüft, ob der Istwert innerhalb von **Wert zulässig von** und **Wert zulässig bis** liegt. Wechselt er die markierte Zeile, aktualisiert sich die Factbox automatisch, sodass er mehrere Arbeitsgänge nacheinander prüfen kann.

**Abschluss.** Liegen alle Istwerte im zulässigen Bereich, gibt der Fertigungssteuerer den Arbeitsgang im gewohnten Ablauf frei. Bei Abweichungen veranlasst er die Klärung an der Arbeitsplatzgruppe bzw. im Arbeitsplan, wo die Eigenschaften gepflegt werden. Auch hier erfolgt in dieser App kein eigener Buchungsschritt – der Nutzen liegt im unmittelbaren Soll-Ist-Vergleich an der Arbeitsvorratszeile.
