---
title: Anwenderhandbuch m+m Package Management with Material Properties
---

# Anwenderhandbuch m+m Package Management with Material Properties

## Einleitung

Die App **m+m Package Management with Material Properties** verbindet zwei bestehende m+m Anwendungen: die Packmittelverwaltung (**Packmittel Einrichtung**, **Packmittelreferenzen**) und die Materialeigenschaften (**Materialarten**, **Eigenschaften**). Sie ermöglicht es, eine Packmittelstruktur nicht mehr nur einem einzelnen Artikel zuzuordnen, sondern ganzen **Materialarten** oder einer über Eigenschaften definierten Auswahl von Artikeln – dem **Eigenschaftenfilter**. Dadurch pflegen Sie eine Packmittelvorschrift einmal zentral, statt sie an jedem betroffenen Artikel einzeln zu hinterlegen.

**Zielgruppe.** Primäre Anwender sind operative Mitarbeiter, die im Tagesgeschäft **Packmittelreferenzen** pflegen und einer Materialart oder einem Eigenschaftenfilter das passende Packmittel zuweisen (Verpackungsplanung, Arbeitsvorbereitung, Lager). Sekundäre Zielgruppe sind Administratoren und Key-User, die in der **Packmittel Einrichtung** die Nummernserie hinterlegen und in den Stammdaten die **Materialarten** und **Eigenschaften** vorbereiten.

**Kurzer Prozessüberblick.** Zuerst richtet der Administrator in der **Packmittel Einrichtung** die **Eigenschaftsnummernserie** ein. In den Stammdaten pflegt der Anwender die **Materialarten** und deren **Eigenschaften** (Basismodul Materialeigenschaften). Anschließend legt er – wenn eine über Eigenschaften eingegrenzte Auswahl benötigt wird – eine **Packmittelreferenz Eigenschaftsfilterkarte** an und definiert dort die **Zeilen** mit **Eigenschaftscode** und **Filterwert**. Zuletzt öffnet er über die Aktion **Packmittelreferenz** die Seite **Packmittelreferenzen** und ordnet dem gewählten **Produkttyp** (Materialart oder Eigenschaftenfilter) das konkrete Packmittel zu.

## Schnellstart für Anwender

Die folgende Reihenfolge entspricht der Abhängigkeitskette im Code: erst Einrichtung, dann Stammdaten, dann die Zuordnung.

1. **Einrichtung (einmalig):** Öffnen Sie über **Suchen** die Seite **Packmittel Einrichtung** und tragen Sie im Register **Allgemein** unter **Eigenschaftsnummernserie** eine Nummernserie ein. Ohne diesen Eintrag lässt sich keine Eigenschaftsfilterkarte anlegen.
2. **Materialart wählen:** Öffnen Sie über **Suchen** die Liste **Materialarten** und wählen Sie die Zeile der gewünschten Materialart.
3. **Direkte Zuordnung (Produkttyp Materialart):** Wählen Sie in der Zeile die Aktion **Packmittelreferenz**. Es öffnet sich die Seite **Packmittelreferenzen**, vorgefiltert auf diese Materialart. Legen Sie eine Zeile an, füllen Sie **Packmittelreferenz Nr.**, **Packmittelart** und **Packmittel Nr.** und schließen Sie mit **OK**.
4. **Eigenschaftsbasierte Zuordnung (Produkttyp Eigenschaftenfilter):** Öffnen Sie über **Suchen** die **Packmittelreferenz Eigenschaftsfilterliste**, legen Sie mit einer neuen Zeile eine **Packmittelreferenz Eigenschaftsfilterkarte** an, wählen Sie den **Materialartencode** und erfassen Sie im Unterregister **Zeilen** je Merkmal einen **Eigenschaftscode** und einen **Filterwert**.
5. **Packmittel zum Eigenschaftenfilter zuordnen:** Wählen Sie auf der Eigenschaftsfilterkarte die Aktion **Packmittelreferenz**. Auf der Seite **Packmittelreferenzen** (vorgefiltert auf den Produkttyp Eigenschaftenfilter) legen Sie das Packmittel wie in Schritt 3 an.

Dieses Modul kennt **keinen** Buchungs- oder Freigabelauf. Die Arbeit endet mit dem Speichern der Packmittelreferenz; es gibt keine Meldung, keinen Beleg und keine Buchung.

## Einrichtung

Die Einrichtung dieses Moduls ist bewusst schlank, weil die App nur einen einzigen Konfigurationswert ergänzt: die **Eigenschaftsnummernserie**. Diese steuert jedoch die gesamte eigenschaftsbasierte Kette und wird daher hier vollständig und im Prozesskontext beschrieben.

### Packmittel Einrichtung – ergänzte Felder

**Wer/wann/wozu.** Der Administrator hinterlegt diesen Wert einmalig vor der ersten Nutzung, unternehmensweit. Die **Packmittel Einrichtung** ist eine unternehmensweite Einrichtungsseite (ein Datensatz je Mandant) des Basismoduls und wird über **Suchen** geöffnet. Die App fügt der Seite im Register **Allgemein** ein Feld hinzu.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Packmittel Einrichtung**, Register **Allgemein**.

| Einrichtung | Erläuterung |
|---|---|
| **Eigenschaftsnummernserie** | Wenn hier eine Nummernserie hinterlegt ist, vergibt das System beim Anlegen einer neuen **Packmittelreferenz Eigenschaftsfilterkarte** automatisch die nächste freie Nummer aus dieser Serie in das Feld **Nr.**; ist das Feld leer, bricht das Anlegen einer Eigenschaftsfilterkarte mit einer Fehlermeldung ab. Ohne diese Einrichtung kann die eigenschaftsbasierte Packmittelzuordnung also nicht genutzt werden. |

Ergänzend sichtbar sind auf derselben Seite die Felder des Basismoduls **Packmittel**. Für die eigenschaftsbasierte Zuordnung ist davon nur die **Eigenschaftsnummernserie** relevant; die weiteren im Register **Allgemein** verfügbaren Steuerungen des Basismoduls betreffen die allgemeine Packmittelverwaltung:

| Einrichtung (Basismodul, Kontext) | Erläuterung |
|---|---|
| **Vertikales Innenverpackungsymbol** / **Horizontales Innenverpackungssymbol** | Wenn ein Symbol gesetzt ist, verwendet die Packmittelverwaltung dieses Zeichen zur Darstellung vertikaler bzw. horizontaler Unterteilungen innerhalb einer Packmittelstruktur; dies wirkt sich nicht auf die Eigenschaftsfilter aus. |
| **Packmittelzuweisung** | Steuert im Basismodul, wie Packmittel Belegen zugewiesen werden; für die eigenschaftsbasierte Referenz ohne Bedeutung. |
| **Artikelumlagerungsbuchblattvorlagenname** / **Artikelumlagerungsbuchblattname** | Wenn gesetzt, verwendet das Basismodul diese Buch.-Blattvorlage bzw. dieses Buch.-Blatt für artikelbezogene Umlagerungen der Packmittelverwaltung; für die Eigenschaftsfilter nicht erforderlich. |

> Hinweis: Weitere Felder der **Packmittel Einrichtung** gehören ausschließlich zum Basismodul Packmittel und beeinflussen die eigenschaftsbasierte Zuordnung nicht. Für die Nutzung dieser App genügt die **Eigenschaftsnummernserie**.

### Eigenschaftsbasierte Packmittelreferenzen einrichten

Diese Kette verbindet vier Ebenen: Stammdaten der Materialeigenschaften → globale Nummernserie → Eigenschaftsfilterkarte → operative Zuordnung. Sie wird hier als zusammenhängender Prozess beschrieben; die einzelnen Seiten sind in den folgenden Kapiteln im Detail dokumentiert.

**Prozesseinstieg.** Konfiguriert wird die Kette von einem Key-User der Verpackungsplanung, bevor eigenschaftsbasierte Packmittelreferenzen erstmals im Tagesgeschäft genutzt werden. Das Ergebnis verwendet der Anwender später auf der Seite **Packmittelreferenzen** (siehe Kapitel **Tägliche Arbeit**).

**Enablement-Schritte in Abhängigkeitsreihenfolge:**

1. **Zuerst** pflegen Sie im Basismodul Materialeigenschaften die **Materialarten** und je Materialart die zugehörigen **Eigenschaften**. Damit im Filterwert eine Auswahlliste erscheint, aktivieren Sie an der jeweiligen Eigenschaft das Kennzeichen **Eigenschaftswerte verwenden**: Wenn aktiviert, kann der Anwender den **Filterwert** später aus den hinterlegten Eigenschaftswerten auswählen; ist es nicht aktiviert, gibt er den Filter frei ein.
2. **Danach** hinterlegen Sie in der **Packmittel Einrichtung** die **Eigenschaftsnummernserie** (siehe oben). Wenn dieser Wert fehlt, lässt sich im nächsten Schritt keine Eigenschaftsfilterkarte anlegen.
3. **Anschließend** legen Sie eine **Packmittelreferenz Eigenschaftsfilterkarte** an, wählen den **Materialartencode** und definieren im Unterregister **Zeilen** die Kombination aus **Eigenschaftscode** und **Filterwert** (siehe Kapitel **Stammdaten**). Wenn eine Zeile gefüllt ist, grenzt sie die Auswahl der Artikel auf jene ein, die dieser Eigenschaftsausprägung entsprechen.
4. **Schließlich** öffnen Sie auf der Eigenschaftsfilterkarte die Aktion **Packmittelreferenz** und ordnen dem Filter das konkrete Packmittel zu. Damit ist die Kette abgeschlossen; die Zuordnung greift, sobald für einen passenden Artikel eine Packmittelstruktur benötigt wird (siehe Kapitel **Tägliche Arbeit**).

**Abhängigkeits- und Validierungshinweise.** Der **Materialartencode** auf der Eigenschaftsfilterkarte muss gesetzt sein, bevor eine Zeile mit einem **Eigenschaftscode** erfasst werden kann; das System prüft beim Erfassen der Zeile, dass die gewählte Eigenschaft tatsächlich zur Materialart der Karte gehört. Wird die Materialart geändert oder der **Eigenschaftscode** einer Zeile geleert bzw. gewechselt, setzt das System den zugehörigen **Filterwert** automatisch zurück, damit kein unpassender Filter zurückbleibt.

## Stammdaten

Die App bringt eine eigene Stammdatenseite mit – die **Packmittelreferenz Eigenschaftsfilterkarte** – und ergänzt die bestehenden Materialarten-Seiten um eine Navigationsaktion.

### Materialarten und die Aktion Packmittelreferenz

**Wer/wann/wozu.** Materialarten werden von der Stammdatenpflege im Basismodul Materialeigenschaften angelegt und gepflegt. Die App ergänzt sowohl die Liste **Materialarten** als auch die **Materialartenkarte** um die Aktion **Packmittelreferenz**, mit der eine Packmittelstruktur direkt einer ganzen Materialart zugeordnet wird. Anwender setzen diese Aktion ein, wenn für alle Artikel einer Materialart dieselbe Verpackung gilt.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Materialarten** und wählen Sie die betreffende Zeile; alternativ öffnen Sie über die Zeile die **Materialartenkarte**.

Die App fügt hier **kein** eigenes Feld hinzu; die Materialart selbst (Code, Beschreibung, Eigenschaften) wird im Basismodul Materialeigenschaften gepflegt. Ergänzt wird ausschließlich die folgende Aktion:

| Aktion | Erläuterung |
|---|---|
| **Packmittelreferenz** | Wenn Sie diese Aktion auf einer Materialart auswählen, öffnet sich die Seite **Packmittelreferenzen**, vorgefiltert auf den **Produkttyp** Materialart und den Code dieser Materialart. Dort ordnen Sie der Materialart ein oder mehrere Packmittel zu; die Produkt- und Referenzspalten sind dabei ausgeblendet, weil der Bezug bereits durch die gewählte Materialart feststeht. |

Cross-Link: Die Pflege der Packmittelzeilen selbst ist im Kapitel **Tägliche Arbeit** beschrieben; die eigenschaftsbasierte Alternative im nächsten Abschnitt.

### Packmittelreferenz Eigenschaftsfilter (Eigenschaftsfilterkarte und Zeilen)

**Wer/wann/wozu.** Diese Stammdaten legt der Key-User an, wenn eine Packmittelvorschrift nicht für eine ganze Materialart, sondern nur für die Artikel einer Materialart mit bestimmten Eigenschaftsausprägungen gelten soll (z. B. nur eine bestimmte Abmessung oder Qualität). Die Karte definiert also einen benannten **Eigenschaftenfilter**, dem später ein Packmittel zugeordnet wird.

**Einstieg:** Öffnen Sie über **Suchen** die **Packmittelreferenz Eigenschaftsfilterliste** und legen Sie mit einer neuen Zeile eine **Packmittelreferenz Eigenschaftsfilterkarte** an; eine bestehende öffnen Sie durch Auswahl der Listenzeile.

Kopffelder der **Packmittelreferenz Eigenschaftsfilterkarte** (Register **Allgemein**):

| Feld | Erläuterung |
|---|---|
| **Nr.** | Eindeutige Nummer des Eigenschaftenfilters. Wenn Sie das Feld beim Anlegen leer lassen, vergibt das System die nächste Nummer aus der **Eigenschaftsnummernserie** der **Packmittel Einrichtung**; ist keine Serie hinterlegt, wird das Anlegen abgebrochen. |
| **Materialartencode** | Wenn Sie eine Materialart auswählen, legt das System fest, aus welcher Materialart die in den Zeilen erlaubten Eigenschaften stammen; erst danach lassen sich Zeilen mit einem **Eigenschaftscode** erfassen. Das Feld ist zwingend zu füllen, bevor eine Zeile angelegt wird. |
| **Beschreibung** | Wenn Sie hier einen Text eintragen, erscheint dieser als sprechende Bezeichnung des Filters in der **Packmittelreferenz Eigenschaftsfilterliste** und erleichtert das Wiederfinden. |

Zeilen im Unterregister **Zeilen** (jede Zeile grenzt die Artikelauswahl um ein Merkmal ein):

| Feld | Erläuterung |
|---|---|
| **Eigenschaftscode** | Wenn Sie einen Eigenschaftscode wählen, bestimmen Sie, nach welchem Merkmal der Materialart gefiltert wird. Das System lässt nur Eigenschaften zu, die zur Materialart des Kopfes gehören; passt der Code nicht, wird die Eingabe abgewiesen. |
| **Eigenschaftsname** | Zeigt den Namen der gewählten Eigenschaft an. Das Feld wird automatisch aus dem **Eigenschaftscode** ermittelt und ist nicht editierbar. |
| **Filterwert** | Wenn Sie einen Wert setzen, filtert das System die Artikel auf jene, deren Eigenschaftsausprägung diesem Wert entspricht. Über die Auswahlfunktion (AssistEdit) im Feld gilt: Ist an der Eigenschaft **Eigenschaftswerte verwenden** aktiviert, wählen Sie einen oder mehrere hinterlegte Werte aus einer Liste (Mehrfachauswahl wird als Oder-Verknüpfung übernommen); andernfalls öffnet sich der Materialsuche-Dialog, in dem Sie den Filterausdruck zusammenstellen. Leeren Sie den **Eigenschaftscode**, wird der **Filterwert** automatisch zurückgesetzt. |

**Prozessschritte.** Zuerst **Materialartencode** wählen, danach je gewünschtem Merkmal eine Zeile mit **Eigenschaftscode** und **Filterwert** anlegen, schließlich über die Aktion **Packmittelreferenz** (siehe unten) das Packmittel zuordnen.

| Aktion | Erläuterung |
|---|---|
| **Packmittelreferenz** | Wenn Sie diese Aktion auf der Eigenschaftsfilterkarte auswählen, öffnet sich die Seite **Packmittelreferenzen**, vorgefiltert auf den **Produkttyp** Eigenschaftenfilter und die **Nr.** dieses Filters. Dort hinterlegen Sie das Packmittel für genau diesen Eigenschaftenfilter. |

**Löschverhalten.** Beim Löschen einer Eigenschaftsfilterkarte prüft das System, ob zu diesem Filter bereits eine Packmittelreferenz existiert; ist das der Fall, wird das Löschen mit dem Hinweis „Eine Packmittelreferenz existiert." verhindert. Die zugehörigen **Zeilen** werden beim Löschen der Karte automatisch mit entfernt. Ebenso verhindert das System das Löschen einer **Materialart** oder einer **Eigenschaft**, solange diese noch in einer Packmittelreferenz bzw. in einer Eigenschaftsfilterzeile verwendet wird.

## Tägliche Arbeit: Packmittelreferenzen

Die eigentliche Zuordnung eines Packmittels erfolgt auf der Seite **Packmittelreferenzen** des Basismoduls. Diese Seite wird von der App um die Spalte **Materialartencode** erweitert und wird über die Aktion **Packmittelreferenz** vorgefiltert geöffnet – aus der Materialart, aus der Materialartenkarte oder aus der Eigenschaftsfilterkarte.

**Setup-/Stammdaten-Bezug.** Diese transaktionale Seite wird durch die zuvor gepflegten Stammdaten gesteuert: die **Packmittel Einrichtung** (Eigenschaftsnummernserie), die **Materialarten**/**Eigenschaften** (Basismodul Materialeigenschaften) sowie die **Packmittelreferenz Eigenschaftsfilterkarte**. Ist einer dieser Bausteine nicht gepflegt, steht die entsprechende Zuordnung nicht zur Verfügung (siehe Kapitel **Einrichtung** und **Stammdaten**).

**Einstieg:** Öffnen Sie die Seite **Packmittelreferenzen** über die Aktion **Packmittelreferenz** – auf einer Materialart, auf der Materialartenkarte oder auf einer Packmittelreferenz Eigenschaftsfilterkarte. Ein direkter Aufruf über **Suchen** ist für die eigenschaftsbasierten Fälle nicht vorgesehen, weil die Seite stets vorgefiltert auf den jeweiligen **Produkttyp** geöffnet wird.

Beim Öffnen über eine dieser Aktionen sind die Produkt- und Referenzspalten ausgeblendet; sichtbar und zu pflegen sind insbesondere:

| Feld | Erläuterung |
|---|---|
| **Packmittelreferenz Nr.** | Wenn Sie hier eine Nummer vergeben, identifizieren Sie die einzelne Packmittelzuordnung eindeutig; das Feld ist ein Pflichtfeld. |
| **Packmittelart** | Bestimmt, welche Art von Packmittel zugeordnet wird. Wenn Sie die Packmittelart ändern, setzt das System **Menge pro Packmittel** und **Packmittel Nr.** zurück, damit keine unpassende Kombination bestehen bleibt. |
| **Packmittel Nr.** | Wenn Sie ein Packmittel wählen, legen Sie fest, welches konkrete Packmittel (bzw. welche Packmittelstückliste oder -kategorie) für den gefilterten Umfang gilt; Pflichtfeld. |
| **Menge pro Packmittel** | Wenn Sie eine Menge eintragen, bestimmt sie, wie viele Einheiten je Packmittel angesetzt werden. Bei der Packmittelart Packmittelkategorie ist das Feld gesperrt, weil dort keine feste Menge zulässig ist. |
| **Einheitencode** | Legt die Maßeinheit fest, auf die sich die Menge pro Packmittel bezieht. |
| **Variante** | Grenzt die Zuordnung optional auf eine bestimmte Artikelvariante ein. |
| **Beschreibung** | Freitext zur Erläuterung der Zuordnung. |
| **Artikelverfolgung separat belassen** | Wenn aktiviert, hält das Basismodul die Artikelverfolgung dieser Packmittelzuordnung getrennt; dies steuert das Verhalten der nachgelagerten Packmittelprozesse im Basismodul. |
| **Materialartencode** (von dieser App ergänzte Spalte) | Zeigt zu jeder Packmittelreferenz die Materialart des zugeordneten Artikels an. Der Wert wird automatisch aus dem Artikel ermittelt und ist nicht editierbar; er dient dazu, eigenschaftsbasierte und materialartbezogene Zuordnungen in der Liste unmittelbar zu erkennen. |

### Produkttyp – die von dieser App ergänzten Werte

Der **Produkttyp** einer Packmittelreferenz entscheidet, worauf sich die Zuordnung bezieht. Die App ergänzt die Auswahl um drei Werte. Die beiden Aktionen dieser App setzen den Produkttyp jeweils automatisch, sodass der Anwender ihn nicht manuell wählen muss:

- **Materialart:** Die Packmittelreferenz gilt für **eine** Materialart. Diesen Wert setzt die Aktion **Packmittelreferenz** auf der Materialart bzw. der Materialartenkarte automatisch; als **Artikelnr.** wird der Materialartencode geführt.
- **Alle Materialarten:** Die Zuordnung gilt materialartübergreifend als Vorgabewert. Dieser Wert steht als Auswahl zur Verfügung, wenn eine übergreifende Regel ohne Einschränkung auf eine einzelne Materialart gewünscht ist.
- **Eigenschaftenfilter:** Die Packmittelreferenz gilt für alle Artikel, die dem auf der **Packmittelreferenz Eigenschaftsfilterkarte** definierten Filter entsprechen. Diesen Wert setzt die Aktion **Packmittelreferenz** auf der Eigenschaftsfilterkarte automatisch; als Bezug wird die **Nr.** des Eigenschaftenfilters geführt.

## FAQ und Troubleshooting

### 1. Warum lässt sich keine Eigenschaftsfilterkarte anlegen?
Weil in der **Packmittel Einrichtung** keine **Eigenschaftsnummernserie** hinterlegt ist. Das System vergibt die **Nr.** aus dieser Serie; fehlt sie, wird das Anlegen abgebrochen. Tragen Sie die Nummernserie zuerst in der Einrichtung ein.

### 2. Wie ordne ich einer ganzen Materialart ein Packmittel zu, ohne einzelne Artikel zu pflegen?
Öffnen Sie die **Materialarten**, wählen Sie die Zeile und dann die Aktion **Packmittelreferenz**. Auf der Seite **Packmittelreferenzen** legen Sie das Packmittel an; der **Produkttyp** Materialart wird automatisch gesetzt.

### 3. Warum kann ich in einer Filterzeile keinen Eigenschaftscode auswählen?
Weil auf der Eigenschaftsfilterkarte noch kein **Materialartencode** gesetzt ist oder der gewählte **Eigenschaftscode** nicht zu dieser Materialart gehört. Setzen Sie zuerst den Materialartencode; danach sind nur die Eigenschaften dieser Materialart zulässig.

### 4. Warum verschwindet mein Filterwert, wenn ich den Eigenschaftscode ändere?
Das ist beabsichtigt: Beim Wechseln oder Leeren des **Eigenschaftscodes** setzt das System den **Filterwert** automatisch zurück, damit kein Wert stehen bleibt, der nicht mehr zur Eigenschaft passt. Erfassen Sie den Filterwert nach dem Wechsel neu.

### 5. Wann erhalte ich beim Filterwert eine Auswahlliste, wann muss ich frei eingeben?
Das hängt am Kennzeichen **Eigenschaftswerte verwenden** der jeweiligen Eigenschaft. Ist es aktiviert, wählen Sie den **Filterwert** aus den hinterlegten Eigenschaftswerten (auch mehrere, als Oder-Verknüpfung); ist es nicht aktiviert, stellen Sie den Filter im Materialsuche-Dialog zusammen.

### 6. Kann ich mehrere Eigenschaftswerte in einer Filterzeile zulassen?
Ja. Wählen Sie im Auswahldialog mehrere Werte aus; das System übernimmt sie als Oder-Verknüpfung in den **Filterwert**. Damit greift die Packmittelreferenz für Artikel, die einen der gewählten Werte tragen.

### 7. Warum kann ich eine Eigenschaftsfilterkarte nicht löschen?
Weil zu diesem Filter bereits eine **Packmittelreferenz** existiert. Entfernen Sie zuerst die zugehörige Packmittelreferenz; danach lässt sich die Karte löschen. Die **Zeilen** der Karte werden beim Löschen automatisch mit entfernt.

### 8. Warum lässt sich eine Materialart oder eine Eigenschaft nicht löschen?
Weil sie noch in einer Packmittelreferenz bzw. in einer Eigenschaftsfilterzeile verwendet wird. Das System verhindert das Löschen mit dem Hinweis, dass ein Eintrag existiert. Lösen Sie zuerst die Zuordnung, dann ist das Löschen möglich.

### 9. Muss ich den Produkttyp der Packmittelreferenz manuell setzen?
Nein. Öffnen Sie die Seite **Packmittelreferenzen** immer über die Aktion **Packmittelreferenz** – auf der Materialart wird der Produkttyp **Materialart**, auf der Eigenschaftsfilterkarte der Produkttyp **Eigenschaftenfilter** automatisch vorbelegt und die Seite entsprechend vorgefiltert.

### 10. Muss ich nach dem Zuordnen etwas buchen oder freigeben?
Nein. Dieses Modul kennt keinen Buchungs-, Freigabe- oder Meldelauf. Die Zuordnung ist mit dem Speichern der Packmittelreferenz wirksam.

## Typische Anwendungsfälle

### Anwendungsfall 1: Packmittel für eine über Eigenschaften eingegrenzte Auswahl

**Auslöser.** Die Verpackungsplanung erhält die Vorgabe, dass Artikel einer Materialart mit einer bestimmten Eigenschaftsausprägung (z. B. einer bestimmten Abmessung) künftig ein spezielles Packmittel erhalten sollen.

**Einstieg in BC.** Der Anwender stellt zunächst sicher, dass in der **Packmittel Einrichtung** die **Eigenschaftsnummernserie** hinterlegt ist. Danach öffnet er über **Suchen** die **Packmittelreferenz Eigenschaftsfilterliste**.

**Kernablauf.** Er legt mit einer neuen Zeile eine **Packmittelreferenz Eigenschaftsfilterkarte** an, wählt den **Materialartencode** und erfasst im Unterregister **Zeilen** einen **Eigenschaftscode**. Im **Filterwert** wählt er – da an der Eigenschaft **Eigenschaftswerte verwenden** aktiv ist – den gewünschten Wert aus der Liste. Anschließend wählt er die Aktion **Packmittelreferenz**; auf der Seite **Packmittelreferenzen** (Produkttyp Eigenschaftenfilter, vorgefiltert auf die Filternummer) trägt er **Packmittelreferenz Nr.**, **Packmittelart**, **Packmittel Nr.** und **Menge pro Packmittel** ein.

**Abschluss.** Mit dem Speichern der Packmittelreferenz ist der Vorgang abgeschlossen; ein Buchen oder Freigeben ist nicht erforderlich. In der Liste **Packmittelreferenzen** erkennt der Anwender die Zuordnung an der Spalte **Materialartencode**.

### Anwendungsfall 2: Packmittel für eine ganze Materialart

**Auslöser.** Für alle Artikel einer Materialart gilt einheitlich dasselbe Packmittel; eine Einschränkung über Eigenschaften ist nicht nötig.

**Einstieg in BC.** Der Anwender öffnet über **Suchen** die Liste **Materialarten** und wählt die betreffende Zeile (alternativ die **Materialartenkarte**).

**Kernablauf.** Er wählt die Aktion **Packmittelreferenz**. Die Seite **Packmittelreferenzen** öffnet sich vorgefiltert auf den **Produkttyp** Materialart und den Materialartencode. Er legt eine Zeile an und füllt **Packmittelreferenz Nr.**, **Packmittelart**, **Packmittel Nr.** sowie **Menge pro Packmittel** und **Einheitencode**.

**Abschluss.** Nach dem Speichern gilt die Packmittelvorschrift für die gesamte Materialart. Auch hier gibt es keinen nachgelagerten Buchungs- oder Freigabeschritt.
