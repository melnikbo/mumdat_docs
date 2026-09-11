---
title: Anwenderhandbuch m+m Original Length Management
---

# Anwenderhandbuch m+m Original Length Management

## Einleitung

Die Erweiterung **m+m Original Length Management** ergänzt die Artikelverfolgung von Microsoft
Dynamics 365 Business Central um die tatsächliche **Länge** und die **Ursprüngliche Länge** je
Charge sowie um eine **Gewichtsverteilung nach Länge**. Das Modul richtet sich an Betriebe der
Stahlverarbeitung, in denen chargenverfolgte Artikel (Stäbe, Rohre, Profile, Bunde) in Metern erfasst
und über eine KG-pro-Meter-Umrechnung gewogen werden.

**Zielgruppe:** Primär die **operativen Anwender** in Wareneingang, Lager und Fertigung, die täglich
mit der **Artikelverfolgung** arbeiten – also Chargen anlegen, Ist-Längen erfassen und das Gewicht je
Charge ermitteln. Sekundär sind **Administratoren und Stammdatenverantwortliche** angesprochen, die
einmalig die Längeneigenschaft je **Materialart** und die KG-/Meter-Umrechnung einrichten.

**Kurzer Prozessüberblick:**

1. Der Administrator hinterlegt je **Materialart** eine Datensatzeigenschaft mit der **Verwendung**
   *Länge* (und optional *Urspr. Länge*) und richtet in der **KG Meter Stück Einrichtung** die
   Einheiten für KG und Meter ein.
2. Beim Anlegen der Charge (Wareneingang) erfasst der Anwender in den **Artikelverfolgungszeilen**
   bzw. in **Artikelverfolgung erstellen** die tatsächliche **Länge**.
3. Über die Aktion **Gewichtsverteilung nach Länge** wird das Gesamtgewicht anhand der Längen auf die
   einzelnen Chargen verteilt und je Charge die **Menge (Basis)** gesetzt.
4. In der **Chargennr.-Information** und im **FA-Arbeitsvorrat** stehen **Länge** und
   **Ursprüngliche Länge** anschließend zur Ansicht und Weiterverarbeitung bereit.

## Schnellstart für Anwender

Die folgende Reihenfolge folgt der technischen Abhängigkeit: zuerst Einrichtung, dann Erfassung, dann
Gewichtsverteilung.

1. **Einrichtung prüfen (einmalig, Administrator).** Stellen Sie sicher, dass in der **KG Meter Stück
   Einrichtung** der **Einheitencode für KG** und der **Einheitencode für Meter** gesetzt sind und
   dass die betroffene **Materialart** eine Datensatzeigenschaft mit **Verwendung** = **Länge**
   besitzt. Ohne diese Eigenschaft bleibt die Längenlogik inaktiv.
2. **Charge mit Länge anlegen.** Öffnen Sie zur Belegzeile die **Artikelverfolgungszeilen** und tragen
   Sie je Charge die tatsächliche **Länge** ein – oder legen Sie die Chargen über
   **Artikelverfolgung erstellen** an und erfassen dort die **Länge**.
3. **Gewicht verteilen.** Wählen Sie in den **Artikelverfolgungszeilen** die Aktion
   **Gewichtsverteilung nach Länge**.
4. **Werte bestätigen.** Bestätigen Sie den Dialog *„Soll die Gewichtsverteilung der Chargen mit den
   folgenden Werten durchgeführt werden?“* (mit **Gesamtlänge**, **Gesamtgewicht** und
   **Tatsächliche KG pro Meter**) mit **Ja**. Das Modul berechnet je Charge das KG-Gewicht und setzt
   die **Menge (Basis)**.
5. **Ergebnis prüfen.** Kontrollieren Sie die verteilten Mengen in den Artikelverfolgungszeilen sowie
   **Länge** und **Ursprüngliche Länge** in der **Chargennr.-Information**.

## Einrichtung

Die Einrichtung dieses Moduls besteht aus Stammdaten und globalen Einstellungen, die in den
Basismodulen **m+m Material Properties** und **m+m Unit Conversion** liegen und von der
Längenverwaltung ausgewertet werden. Ohne diese Einrichtung sind die Längenfelder zwar sichtbar,
werden aber nicht automatisch gefüllt und die Gewichtsverteilung ist deaktiviert.

### Längeneigenschaften je Materialart einrichten

**Prozessintro.** Diese Einrichtung nimmt der **Administrator** oder ein **Stammdatenverantwortlicher**
einmalig vor, bevor die betroffenen Artikel produktiv chargenverfolgt gebucht werden. Sie legt fest,
für welche **Materialart** eine Länge geführt wird. Erst wenn eine Materialart eine Eigenschaft mit
der **Verwendung** *Länge* besitzt, aktiviert das Modul die Aktion **Gewichtsverteilung nach Länge**
in den Artikelverfolgungszeilen und füllt die Längenfelder automatisch. Die hier gepflegten Werte
wirken später in der täglichen Arbeit (Abschnitt **Tägliche Arbeit an der Artikelverfolgung**).

**Einstieg:** Öffnen Sie die **Materialart** in den Stammdaten der Materialeigenschaften und rufen Sie
dort den Eigenschafteneditor (**Datensatzeigenschaft**) der Materialart auf. Legen Sie je Materialart
eine Zeile mit der gewünschten **Verwendung** an.

Erläuterung der Felder der **Datensatzeigenschaft**, die dieses Modul auswertet:

| Feld | Erläuterung |
|---|---|
| Verwendung | Legt fest, wofür die Eigenschaft genutzt wird. Wenn Sie **Länge** auswählen, dann behandelt das Modul den numerischen Wert als tatsächliche Länge der Charge; er wird beim Buchen automatisch in die Chargeninformation und in die Artikelverfolgungszeilen übernommen und ist Grundlage der Gewichtsverteilung. Wenn Sie **Urspr. Länge** auswählen, dann wird zusätzlich die ursprüngliche Länge der Charge geführt (siehe eigener Absatz unten). |
| Chargeneigenschaft | Wenn aktiviert, dann gilt die Eigenschaft je Charge (Chargennr.-Ebene) und kann pro Charge unterschiedliche Werte annehmen; das Modul erzwingt diese Aktivierung für die Verwendungen **Länge** und **Urspr. Länge** – ohne gesetzte Chargeneigenschaft wird beim Speichern ein Fehler ausgegeben. |
| Datentyp | Bestimmt das erlaubte Werteformat. Für **Länge** und **Urspr. Länge** lässt das Modul ausschließlich **Dezimalzahl** oder **Ganzzahl** zu; andere Datentypen werden mit der Meldung *„Wenn Sie die Verwendung … verwenden, kann der Datentyp nur Dezimalzahl oder Ganzzahl sein.“* abgewiesen. |
| Numerischer Wert | Enthält den ausgewerteten Zahlenwert der Länge. Wenn hier ein Wert steht, dann liest das Modul ihn beim Zusammenstellen der Artikelverfolgung aus und schreibt ihn in das Feld **Länge** der Zeile. |
| Wert | Nimmt den erfassten Eigenschaftswert als Text auf. Wenn das Modul beim Buchen eine Länge zurückschreibt, dann aktualisiert es diesen Wert (per Validierung), sodass **Numerischer Wert** konsistent bleibt. |

**Datentyp – erlaubte Werte für Längeneigenschaften:**

- **Dezimalzahl:** Länge mit Nachkommastellen (z. B. 6,250 m). Empfohlen für metergenaue Erfassung.
- **Ganzzahl:** Länge ohne Nachkommastellen. Zulässig, wenn ganze Meter genügen.
- Alle übrigen Datentypen sind für die Verwendungen **Länge**/**Urspr. Länge** gesperrt und lösen die
  oben genannte Fehlermeldung aus.

**Verwendung – die von diesem Modul ergänzten Werte:**

- **Länge:** Die Charge führt eine tatsächliche Länge. Wenn gesetzt, dann wird der Wert beim Erzeugen
  der Artikelverfolgung, beim Anlegen der Chargeninformation und beim Buchen in das Feld **Länge**
  übernommen und dient als Basis der Gewichtsverteilung.
- **Urspr. Länge:** Die Charge führt zusätzlich die ursprüngliche Länge. Wenn gesetzt, dann schreibt
  das Modul beim erstmaligen Anlegen der Chargeninformation den Längenwert auch als ursprüngliche
  Länge – jedoch nur, solange für die Charge **noch kein Artikelposten** existiert. Dadurch bleibt die
  Ausgangslänge einer Charge nach der ersten Lagerbuchung unveränderlich erhalten.

> Hinweis: Die Verwendung **Länge**/**Urspr. Länge** darf je Materialart **nur einmal** vergeben
> werden. Legen Sie eine zweite Eigenschaft mit derselben Verwendung an, dann bricht das System mit
> *„Es ist bereits eine Verwendung mit dem Wert … zugewiesen.“* ab.

**Prozessschritte (Abhängigkeitsreihenfolge):**

1. Zuerst legen Sie die **Materialart** an bzw. wählen die bestehende Materialart aus.
2. Danach erfassen Sie in der **Datensatzeigenschaft** dieser Materialart eine Zeile mit
   **Verwendung** = **Länge**, aktivierter **Chargeneigenschaft** und **Datentyp** = **Dezimalzahl**
   (oder **Ganzzahl**).
3. Optional ergänzen Sie eine zweite Zeile mit **Verwendung** = **Urspr. Länge** (gleiche
   Chargeneigenschaft/Datentyp-Regeln).
4. Schließlich weisen Sie den betroffenen **Artikeln** diese **Materialart** zu (Feld
   **Materialartencode** am Artikel bzw. an der Artikelvariante) – erst dadurch greift die Logik im
   Tagesgeschäft.

**Validierung / Abhängigkeiten:** Das Modul prüft beim Speichern der Eigenschaft, dass
**Chargeneigenschaft** gesetzt ist, der **Datentyp** dezimal oder ganzzahlig ist und je Materialart
nur eine Eigenschaft der jeweiligen **Verwendung** existiert. Ist am Artikel keine Materialart mit
Längeneigenschaft hinterlegt, bleibt die Aktion **Gewichtsverteilung nach Länge** deaktiviert.

### KG-/Meter-Umrechnung einrichten

**Prozessintro.** Diese globale Einrichtung nimmt der **Administrator** einmalig je Mandant vor. Sie
bestimmt, welche Basiseinheiten für **KG** und **Meter** gelten und wie das aus der Länge errechnete
Gewicht gerundet wird. Die Gewichtsverteilung in den Artikelverfolgungszeilen greift zwingend auf
diese Einrichtung zu.

**Einstieg:** Öffnen Sie die **KG Meter Stück Einrichtung** über **Suchen**. Es handelt sich um eine
mandantenweite Einrichtung mit genau einem Datensatz; ein übergeordneter Aufruf über eine Liste
existiert nicht.

| Einrichtung | Erläuterung |
|---|---|
| Einheitencode für KG | Legt die Artikeleinheit fest, die als Gewicht in KG interpretiert wird. Wenn die **Basiseinheit** des Artikels diesem Code entspricht, dann übernimmt die Gewichtsverteilung das errechnete KG-Gewicht direkt als **Menge (Basis)**. Ist der Code leer, bricht die Gewichtsverteilung mit einer Feldprüfmeldung ab. |
| Einheitencode für Meter | Legt die Artikeleinheit fest, die als Länge in Meter interpretiert wird. Wenn die **Basiseinheit** des Artikels diesem Code entspricht, dann setzt die Gewichtsverteilung die Länge als zu bewegende Menge in Meter als **Menge (Basis)**. Ist der Code leer, bricht die Gewichtsverteilung mit einer Feldprüfmeldung ab. |
| Rundungsregel KG (am Artikel) | Bestimmt, wie das je Charge errechnete KG-Gewicht gerundet wird. Siehe Werteliste unten. |
| Rundungspräzision KG (am Artikel) | Legt die Rundungsschrittweite für das KG-Gewicht fest (z. B. 0,001 oder 1). Wenn gesetzt, dann rundet das Modul das errechnete Gewicht auf diese Genauigkeit gemäß der Rundungsregel. |

**Rundungsregel KG – erlaubte Werte:**

- **Aufrunden:** Das errechnete KG-Gewicht wird immer zur nächsthöheren Rundungsstufe aufgerundet.
  Wählen Sie dies, wenn Gewichte nie unterschätzt werden dürfen.
- **Abrunden:** Das Gewicht wird immer zur nächstniedrigeren Stufe abgerundet. Wählen Sie dies, wenn
  konservativ nach unten gerundet werden soll.
- **Kaufmännisches Runden:** Das Gewicht wird kaufmännisch (0,5 aufwärts) gerundet. Standardwahl für
  ausgeglichene Rundung.

**Prozessschritte:**

1. Zuerst setzen Sie in der **KG Meter Stück Einrichtung** den **Einheitencode für KG** und den
   **Einheitencode für Meter**.
2. Danach hinterlegen Sie am **Artikel** die **Rundungsregel KG** und die **Rundungspräzision KG**.
3. Schließlich steht die Aktion **Gewichtsverteilung nach Länge** im Tagesgeschäft zur Verfügung
   (siehe **Tägliche Arbeit an der Artikelverfolgung**).

### Berechtigungen

Die Erweiterung liefert den Berechtigungssatz **m+m Original Length Management** (Objektname
*MuM OL Permission*) aus. Er umfasst die Ausführungsberechtigung für die Längenlogik (Codeunit
*MuM OL Length Management*) und bestimmt damit die Berechtigungen für die automatische Längen- und
Gewichtsermittlung. Weisen Sie diesen Berechtigungssatz allen Anwendern zu, die mit der
Artikelverfolgung längenbasiert arbeiten.

## Stammdaten

### Chargennr.-Information: Länge und Ursprüngliche Länge

**Prozessintro.** Die **Chargennr.-Information** ist der Ort, an dem der Anwender die längenbezogenen
Werte einer Charge einsieht. Die beiden Felder werden nicht manuell erfasst, sondern als
berechnete Felder (FlowFields) aus der Datensatzeigenschaft der Charge gelesen. Die Stammdaten werden
im Zuge der Chargenanlage und der Buchungen gepflegt (siehe **Tägliche Arbeit**); hier prüft der
Anwender das Ergebnis.

**Einstieg:** Öffnen Sie die Übersicht der **Chargennr.-Information** (Chargenliste). Die beiden
Spalten erscheinen zusätzlich zu den Standardfeldern der Charge.

| Feld | Erläuterung |
|---|---|
| Länge | Zeigt die aktuelle tatsächliche Länge der Charge. Wenn für die Charge eine Datensatzeigenschaft mit **Verwendung** = **Länge** existiert, dann zeigt das Feld deren **Numerischen Wert**; ändert sich die Länge (z. B. durch Verbrauch in der Fertigung), aktualisiert sich der angezeigte Wert entsprechend. |
| Ursprüngliche Länge | Zeigt die ursprüngliche Länge der Charge zum Zeitpunkt der ersten Lagerbuchung. Wenn eine Eigenschaft mit **Verwendung** = **Urspr. Länge** existiert, dann zeigt das Feld deren **Numerischen Wert**; nach der ersten Lagerbuchung bleibt dieser Wert unverändert und dient als Referenz für die Ausgangslänge. |

Beide Felder sind **nicht editierbar** – sie spiegeln die zugrunde liegende Chargeneigenschaft wider.
Pflegen Sie Längenwerte daher über die Erfassung in der Artikelverfolgung, nicht in der Chargenliste.

## Tägliche Arbeit an der Artikelverfolgung

Die tägliche Arbeit findet in der Artikelverfolgung statt. Welche Felder und Aktionen aktiv sind, wird
durch die Einrichtung gesteuert: Die tatsächliche **Länge** wird nur dann automatisch gefüllt und die
Aktion **Gewichtsverteilung nach Länge** nur dann angeboten, wenn die zugehörige **Materialart** eine
Längeneigenschaft besitzt (Abschnitt **Längeneigenschaften je Materialart einrichten**) und die
**KG Meter Stück Einrichtung** vollständig ist (Abschnitt **KG-/Meter-Umrechnung einrichten**).

### Artikelverfolgungszeilen: Länge erfassen

**Einstieg:** Öffnen Sie über die Aktion **Artikelverfolgungszeilen** zu einer Beleg- oder
Buch.-Blattzeile die Seite **Artikelverfolgungszeilen**.

| Feld | Erläuterung |
|---|---|
| Länge | Erfasst bzw. zeigt die tatsächliche Länge je Charge. Wenn die Ist-Länge der Charge steuernd sein soll (Materialart mit Längeneigenschaft vorhanden), dann trägt das Modul die aus der Chargeneigenschaft bekannte Länge automatisch ein und Sie können sie anpassen; der Wert ist Grundlage der anschließenden Gewichtsverteilung. |

**Spaltenbeschriftung „Verbleibende Länge“:** Ist die Zufuhr-/Lieferansicht der Artikelverfolgung
nicht sichtbar, beschriftet das Modul dieselbe Spalte als **Verbleibende Länge**. Damit erkennt der
Anwender in der Verbrauchssicht, welche Restlänge der Charge noch zur Verfügung steht, statt der
ursprünglich zugeführten Länge.

### Aktion: Gewichtsverteilung nach Länge

**Einstieg:** Öffnen Sie über die Aktion **Gewichtsverteilung nach Länge** (in den
**Artikelverfolgungszeilen**, im Menüband gefördert) die Berechnung. Die Aktion ist nur aktiv, wenn
der Artikel einer **Materialart** mit Längeneigenschaft zugeordnet ist.

Ablauf der Aktion:

1. Wählen Sie in den **Artikelverfolgungszeilen** die betreffenden Chargenzeilen aus.
2. Wählen Sie **Gewichtsverteilung nach Länge**.
3. Bestätigen Sie den Dialog *„Soll die Gewichtsverteilung der Chargen mit den folgenden Werten
   durchgeführt werden?“*. Der Dialog zeigt **Gesamtlänge**, **Gesamtgewicht** und die daraus
   ermittelte **Tatsächliche KG pro Meter**. Mit **Ja** wird verteilt, mit **Nein** abgebrochen.
4. Das Modul berechnet je Charge das Gewicht aus **Länge × Tatsächliche KG pro Meter**, rundet gemäß
   **Rundungsregel KG**/**Rundungspräzision KG** des Artikels und setzt die **Menge (Basis)** je nach
   Basiseinheit des Artikels: entspricht sie dem **Einheitencode für KG**, wird das KG-Gewicht
   übernommen; entspricht sie dem **Einheitencode für Meter**, wird der Meterwert übernommen.
5. Zusätzlich schreibt das Modul die ermittelte **Tatsächliche KG pro Meter** in die Chargeninformation
   zurück und aktualisiert die Summen der Artikelverfolgungszeilen.

**Feldbezug im Bestätigungsdialog:**

- **Gesamtlänge:** Summe der Längen aller ausgewählten Chargenzeilen. Wenn 0, rechnet das Modul intern
  mit dem Faktor 1, um eine Division durch Null zu vermeiden.
- **Gesamtgewicht:** Summe der KG-Werte der ausgewählten Zeilen.
- **Tatsächliche KG pro Meter:** Gesamtgewicht geteilt durch Gesamtlänge – der Umrechnungsfaktor, mit
  dem jede Charge anschließend bewertet wird.

### Chargen anlegen mit Länge

**Einstieg:** Beim Erstellen mehrerer Chargen öffnen Sie die Seite **Artikelverfolgung erstellen**.

| Feld | Erläuterung |
|---|---|
| Länge | Erfasst die tatsächliche Länge je neu erzeugter Charge. Wenn Sie hier eine Länge eintragen, dann wird dieser Wert beim Anlegen der Artikelverfolgung in die erzeugte Chargenzeile übernommen und steht anschließend für die Gewichtsverteilung sowie in der Chargeninformation zur Verfügung. |

Legen Sie die Chargen wie gewohnt an; die erfasste **Länge** wird an die entstehenden
Artikelverfolgungszeilen weitergereicht.

### Längen im FA-Arbeitsvorrat

**Prozessintro.** Im **FA-Arbeitsvorrat** (Produktionsauftrags-Arbeitsvorrat des Stahlmoduls) ergänzt
die Erweiterung in den chargen- und materialbezogenen Ansichten jeweils das Feld **Länge**. So sieht
der Fertigungsanwender direkt am Auftrag, welche Länge je zugeordneter Charge bzw. je Vormaterial
geführt wird. Die Werte werden beim Zuordnen/Erfassen der Charge automatisch aus der Chargeneigenschaft
gezogen und bei Änderung der Chargennr. neu ermittelt.

**Einstieg:** Öffnen Sie den **FA-Arbeitsvorrat** und arbeiten Sie in den Teilansichten für Chargen,
Material und Restechargen.

| Ansicht | Feld | Erläuterung |
|---|---|---|
| Chargen (zugeordnete Chargen) | Länge | Zeigt/erfasst die Länge der dem Arbeitsgang zugeordneten Charge. Wenn Sie die **Chargennr.** wählen oder eine Zeile anlegen, dann ermittelt das Modul die Länge aus der Datensatzeigenschaft der Charge und schreibt einen geänderten Wert bei Bestätigung in die Chargeneigenschaft zurück. |
| Material (Vormaterial) | Länge | Zeigt die verbleibende Länge des zugeordneten Vormaterials. Wenn die Materialzeile geändert wird, dann aktualisiert das Modul den Längenwert der zugehörigen Charge (Zurückschreiben in die Chargeneigenschaft). Der Spaltentitel lautet in dieser Ansicht **Verbleibende Länge**. |
| Restechargen | Länge | Zeigt/erfasst die Länge einer Restecharge (Restlänge, die nach dem Fertigungsverbrauch verbleibt). Wenn Sie hier die **Chargennr.** wählen oder die Zeile anlegen, dann übernimmt das Modul die Länge aus der Eigenschaft und schreibt Änderungen zurück, sodass die Restlänge der Charge korrekt geführt wird. |

## Typische Anwendungsfälle

### Anwendungsfall 1 – Wareneingang: Ist-Längen erfassen und Gewicht verteilen

1. **Auslöser:** Eine Lieferung Stahlstäbe trifft am Wareneingang ein. Die tatsächlichen Meterlängen
   der einzelnen Bunde weichen von der Nennlänge ab und müssen exakt erfasst werden.
2. **Einstieg in BC:** Der Lagermitarbeiter öffnet die Einkaufs-/Wareneingangszeile und ruft die
   **Artikelverfolgungszeilen** auf. Voraussetzung: Die **Materialart** des Artikels besitzt die
   Längeneigenschaft (siehe **Längeneigenschaften je Materialart einrichten**).
3. **Kernablauf:** Je Charge trägt er die gemessene **Länge** ein. Anschließend wählt er
   **Gewichtsverteilung nach Länge**, bestätigt den Dialog mit **Gesamtlänge**, **Gesamtgewicht** und
   **Tatsächliche KG pro Meter** mit **Ja**. Das Modul verteilt das Gewicht, setzt je Charge die
   **Menge (Basis)** und schreibt die **Tatsächliche KG pro Meter** in die Chargeninformation.
4. **Abschluss:** Nach dem Buchen der Zeile stehen **Länge** und **Ursprüngliche Länge** in der
   **Chargennr.-Information** bereit; die ursprüngliche Länge bleibt ab der ersten Lagerbuchung
   unverändert.

### Anwendungsfall 2 – Mehrere Chargen mit Länge anlegen

1. **Auslöser:** Zu einer Wareneingangszeile sollen mehrere Chargen mit jeweils eigener Länge angelegt
   werden.
2. **Einstieg in BC:** Der Anwender öffnet aus der Artikelverfolgung heraus die Seite
   **Artikelverfolgung erstellen**.
3. **Kernablauf:** Er legt die gewünschte Anzahl Chargen an und erfasst je Charge die **Länge**. Die
   Werte werden an die entstehenden **Artikelverfolgungszeilen** übergeben.
4. **Abschluss:** In den Artikelverfolgungszeilen kann er direkt anschließend die
   **Gewichtsverteilung nach Länge** ausführen (siehe Anwendungsfall 1, Schritt 3).

### Anwendungsfall 3 – Restlänge in der Fertigung dokumentieren

1. **Auslöser:** In der Fertigung wird nur ein Teil einer Charge verbraucht; die verbleibende Restlänge
   ist am Fertigungsauftrag zu dokumentieren.
2. **Einstieg in BC:** Der Fertigungsanwender öffnet den **FA-Arbeitsvorrat** und wechselt in die
   Ansicht **Chargen** bzw. **Restechargen**.
3. **Kernablauf:** Er wählt die **Chargennr.** und prüft/erfasst die **Länge** der Restecharge. Das
   Modul zieht den Wert aus der Chargeneigenschaft und schreibt eine Änderung bei Bestätigung zurück.
   In der Ansicht **Material** zeigt die Spalte **Verbleibende Länge** die noch verfügbare Länge des
   Vormaterials.
4. **Abschluss:** Die aktualisierte Länge ist anschließend in der **Chargennr.-Information** sichtbar;
   die **Ursprüngliche Länge** bleibt als Ausgangswert erhalten.

## FAQ und Troubleshooting

### 1. Warum ist die Aktion „Gewichtsverteilung nach Länge“ ausgegraut?

Die Aktion ist nur aktiv, wenn der Artikel einer **Materialart** zugeordnet ist, die eine
Datensatzeigenschaft mit **Verwendung** = **Länge** besitzt. Fehlt die Längeneigenschaft der
Materialart oder ist dem Artikel kein **Materialartencode** zugewiesen, bleibt die Aktion deaktiviert.

### 2. Was passiert, wenn ich „Gewichtsverteilung nach Länge“ bestätige?

Das Modul summiert die Längen und Gewichte der ausgewählten Chargen, ermittelt die **Tatsächliche KG
pro Meter** und berechnet je Charge das Gewicht aus **Länge × Faktor**. Danach rundet es gemäß der
**Rundungsregel KG** und setzt die **Menge (Basis)** entsprechend der Basiseinheit (KG oder Meter).

### 3. Warum bricht die Gewichtsverteilung mit einer Feldprüfmeldung ab?

Die Berechnung setzt voraus, dass in der **KG Meter Stück Einrichtung** sowohl der **Einheitencode für
KG** als auch der **Einheitencode für Meter** gefüllt sind. Fehlt einer der beiden Codes, testet das
Modul das Feld und bricht mit einer Feldprüfmeldung ab.

### 4. Warum kann ich für eine Materialart keine zweite Längeneigenschaft anlegen?

Je Materialart ist die **Verwendung** **Länge** (bzw. **Urspr. Länge**) nur einmal zulässig. Ein
zweiter Eintrag derselben Verwendung wird mit *„Es ist bereits eine Verwendung mit dem Wert …
zugewiesen.“* abgewiesen, damit der Längenwert eindeutig bleibt.

### 5. Warum erhalte ich die Meldung, dass der Datentyp nur dezimal oder ganzzahlig sein darf?

Für die Verwendungen **Länge** und **Urspr. Länge** verlangt das Modul einen numerischen **Datentyp**.
Ist der Datentyp der Eigenschaft weder **Dezimalzahl** noch **Ganzzahl**, wird das Speichern mit der
Meldung *„Wenn Sie die Verwendung … verwenden, kann der Datentyp nur Dezimalzahl oder Ganzzahl sein.“*
verhindert.

### 6. Warum muss die Eigenschaft als Chargeneigenschaft gekennzeichnet sein?

Länge und ursprüngliche Länge werden je Charge geführt. Das Modul prüft daher beim Speichern, dass die
**Chargeneigenschaft** aktiviert ist; ist sie es nicht, schlägt die Feldprüfung fehl. Nur so kann jede
Chargennr. einen eigenen Längenwert erhalten.

### 7. Warum ändert sich die „Ursprüngliche Länge“ nach der ersten Buchung nicht mehr?

Die **Ursprüngliche Länge** wird beim erstmaligen Anlegen der Chargeninformation gesetzt und nur
zurückgeschrieben, solange für die Charge **noch kein Artikelposten** existiert. Nach der ersten
Lagerbuchung bleibt sie als Ausgangswert unveränderlich, während die **Länge** die aktuelle
(verbleibende) Länge widerspiegelt.

### 8. Warum heißt dieselbe Spalte einmal „Länge“ und einmal „Verbleibende Länge“?

In der Zufuhr-/Lieferansicht der Artikelverfolgung zeigt die Spalte die zugeführte **Länge**. Ist diese
Ansicht nicht sichtbar (Verbrauchssicht), beschriftet das Modul dieselbe Spalte als **Verbleibende
Länge**, damit der Anwender die noch verfügbare Restlänge der Charge erkennt.

### 9. Woher kommt der Wert „Länge“ in den Artikelverfolgungszeilen, wenn ich nichts eintrage?

Existiert für die Charge eine Datensatzeigenschaft mit **Verwendung** = **Länge**, liest das Modul beim
Zusammenstellen der Artikelverfolgung deren **Numerischen Wert** und trägt ihn automatisch in das Feld
**Länge** ein. Sie können den vorbelegten Wert anschließend anpassen.

### 10. Warum wird meine im FA-Arbeitsvorrat geänderte Länge in die Charge übernommen?

Ändern Sie im **FA-Arbeitsvorrat** in den Ansichten **Chargen**, **Material** oder **Restechargen** die
**Länge** bzw. die zugehörige **Chargennr.**, schreibt das Modul den neuen Wert in die
Datensatzeigenschaft (**Länge**) der Charge zurück. Dadurch bleiben Fertigungsansicht und
Chargeninformation konsistent.
