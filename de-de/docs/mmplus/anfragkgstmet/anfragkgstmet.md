---
title: Anwenderhandbuch m+m Purchase Quote Manager with Unit Conversion
---

# Anwenderhandbuch m+m Purchase Quote Manager with Unit Conversion

## Einleitung

Die App **m+m Purchase Quote Manager with Unit Conversion** verbindet zwei bestehende m+m-Erweiterungen: den **m+m Purchase Quote Manager** (Anfragen- und Kampagnenverwaltung im Einkauf) und die **m+m Einheitenumrechnung** (Umrechnung zwischen **KG**, **Meter** und **Stück**). Die App fügt den **Kampagnenartikeln** einer Anfrage-Kampagne drei zusätzliche Mengenfelder hinzu – **KG**, **Meter** und **Stück** – und hält diese Felder zusammen mit der Basismenge automatisch synchron.

Sobald ein Anwender in einer Kampagnenzeile die **Menge**, die Mengen in **KG**, **Meter** oder **Stück** oder den **Artikel** ändert, rechnet die App die übrigen Mengenfelder über die für den Artikel hinterlegten Umrechnungsfaktoren neu. So sieht der Einkäufer in einer Anfrage-Kampagne für einen Stahl- oder Coil-Artikel gleichzeitig, wie viel **Gewicht (KG)**, welche **Länge (Meter)** und welche **Stückzahl** einer erfassten Menge entsprechen, ohne selbst rechnen zu müssen.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Einkaufsanwender**, die täglich in Anfrage-Kampagnen Artikelmengen erfassen und Anfragen an Kreditoren vorbereiten. **Administratoren** und **Stammdatenverantwortliche** sind die sekundäre Zielgruppe: Sie richten die für die Umrechnung notwendigen Faktoren am Artikel ein, ohne die die drei neuen Felder leer bleiben.

**Kurzer Prozessüberblick:** Der Administrator hinterlegt einmalig am Artikel die Umrechnungsfaktoren **Theoretische KG pro Meter** und **Theoretische KG pro Stück** (in der App **m+m Einheitenumrechnung**). Danach ergänzt der Einkäufer im Tagesgeschäft die **Kampagnenartikel** einer Anfrage-Kampagne und trägt eine der Mengen **Menge**, **KG**, **Meter** oder **Stück** ein; die App berechnet die restlichen Werte automatisch.

Diese App ist eine **Verbindungs-App**: Sie hat keine eigenen Einrichtungsseiten und keine eigenen Listen- oder Kartenseiten. Ihr gesamter sichtbarer Funktionsumfang besteht aus den drei Feldern auf der Seite **Kampagnenartikel** des m+m Purchase Quote Manager. Die dafür nötige Einrichtung erfolgt vollständig in den beiden abhängigen Modulen.

## Schnellstart für Anwender

Der schnellste Weg von einem eingerichteten Artikel bis zu einer vollständig gefüllten Anfrage-Kampagnenzeile mit KG-, Meter- und Stück-Mengen:

1. **Einrichtung prüfen (Administrator, einmalig):** Stellen Sie sicher, dass am Artikel die Faktoren **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** hinterlegt sind (siehe Kapitel *Einrichtung: Umrechnungsfaktoren am Artikel einrichten*). Ohne diese Faktoren bleiben **KG**, **Meter** und **Stück** leer.
2. **Anfrage-Kampagne öffnen:** Öffnen Sie die gewünschte Kampagne des m+m Purchase Quote Manager und rufen Sie deren **Kampagnenartikel** auf.
3. **Artikel wählen:** Tragen Sie in einer neuen Zeile die **Artikelnr.** ein. Ist der Artikel für die Einheitenumrechnung eingerichtet, übernimmt die App die theoretischen Faktoren des Artikels.
4. **Eine Menge erfassen:** Tragen Sie **einen** der Werte **Menge**, **KG**, **Meter** oder **Stück** ein.
5. **Automatische Umrechnung abwarten:** Die App füllt die jeweils anderen der drei Felder **KG**, **Meter** und **Stück** über die theoretischen Faktoren des Artikels und aktualisiert die **Menge** in der Basiseinheit.
6. **Zeile prüfen und speichern:** Kontrollieren Sie die berechneten Werte und fahren Sie mit der Anfragebearbeitung im m+m Purchase Quote Manager fort.

Sind für den Artikel **keine** Umrechnungsfaktoren eingerichtet, verhält sich die Kampagnenzeile wie im Standard des m+m Purchase Quote Manager: Es findet keine Umrechnung statt, und die drei zusätzlichen Felder bleiben leer.

## Einrichtung

Die App **m+m Purchase Quote Manager with Unit Conversion** bringt **keine eigene Einrichtungsseite** mit. Damit die automatische Umrechnung greift, müssen die beiden abhängigen Module eingerichtet sein: die **m+m Einheitenumrechnung** (Umrechnungsfaktoren am Artikel und modulweite Einheitencodes) sowie der **m+m Purchase Quote Manager** (Anfrage-Kampagnen). Dieses Kapitel beschreibt die für die Umrechnung notwendigen Einstellungen in **Abhängigkeitsreihenfolge**: zuerst die modulweiten Einheitencodes, dann die Faktoren je Artikel.

### Einheitenumrechnung aktivieren und Umrechnungsfaktoren am Artikel einrichten

**Wer richtet das ein und wann:** Diese Einrichtung nimmt der **Administrator** bzw. der **Stammdatenverantwortliche** vor – einmalig vor der ersten Nutzung modulweit, danach je Artikel, für den KG/Meter/Stück in Anfrage-Kampagnen genutzt werden sollen. Die hier gepflegten Werte werden später im Tagesgeschäft auf der Seite **Kampagnenartikel** verbraucht (siehe Kapitel *Tägliche Arbeit: Kampagnenartikel mit KG, Meter und Stück*).

**Prozessschritte in Abhängigkeitsreihenfolge:**

1. **Zuerst – modulweite Einheitencodes hinterlegen:** Öffnen Sie die Seite **KG Meter Stück Einrichtung** der m+m Einheitenumrechnung. Legen Sie fest, welcher **Einheitencode** in Business Central jeweils für **KG**, für **Meter** und für **Stück** steht. Wenn diese Zuordnung gesetzt ist, kann das System erkennen, welche Basiseinheit eines Artikels welcher der drei Größen entspricht, und die Umrechnung überhaupt durchführen.
2. **Danach – theoretische Faktoren je Artikel eintragen:** Öffnen Sie die **Artikelkarte** des betreffenden Artikels und tragen Sie die Faktoren **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** ein. Wenn nur **einer** der beiden Faktoren gesetzt ist, dann ist auch nur die Umrechnung zwischen diesen beiden Einheiten möglich; die jeweils andere Einheit bleibt in der Kampagnenzeile leer. Sind **beide** Faktoren gesetzt, dann werden in der Kampagnenzeile alle drei Felder KG, Meter und Stück berechnet. Sind **keine** Faktoren gesetzt, dann bleiben in der Kampagnenzeile alle drei Felder leer und es findet keine Umrechnung statt.
3. **Schließlich – im Tagesgeschäft anwenden:** Sobald die Faktoren gepflegt sind, greift die Umrechnung automatisch, wenn ein Einkäufer den Artikel in einer Anfrage-Kampagne erfasst (siehe *Tägliche Arbeit: Kampagnenartikel mit KG, Meter und Stück*).

**Einstellungen für die theoretischen Faktoren:**

| Einrichtung | Erläuterung |
|-------------|-------------|
| Theoretische KG pro Meter | Gibt an, wie viele KG bei diesem Artikel theoretisch auf einen Meter entfallen. Wenn gesetzt, dann kann die App aus einer erfassten Meter-Menge das zugehörige Gewicht in KG (und umgekehrt) berechnen; ist der Faktor leer, dann bleibt in der Kampagnenzeile das Feld **Meter** ohne Bezug zum Gewicht und wird nicht befüllt. |
| Theoretische KG pro Stück | Gibt an, wie viele KG bei diesem Artikel theoretisch auf ein Stück entfallen. Wenn gesetzt, dann kann die App aus einer erfassten Stückzahl das zugehörige Gewicht in KG (und umgekehrt) berechnen; ist der Faktor leer, dann bleibt in der Kampagnenzeile das Feld **Stück** ohne Gewichtsbezug und wird nicht befüllt. |

**Abhängigkeitshinweis:** Die App führt eine Umrechnung nur durch, wenn der Artikel gemäß der m+m Einheitenumrechnung dafür eingerichtet ist. Ist der Artikel nicht eingerichtet, dann greift die App nicht ein und die Kampagnenzeile verhält sich wie im Standard des m+m Purchase Quote Manager. Es ist daher zwingend, zuerst die Einheitencodes und danach die Artikelfaktoren zu pflegen, bevor die drei Felder in der Anfrage-Kampagne verwendet werden.

## Stammdaten

Die App legt **keine eigenen Stammdaten** an und erweitert keine Stammdatenkarte um sichtbare Felder. Sie setzt vollständig auf den Stammdaten der abhängigen Module auf:

- **Artikel** (m+m Einheitenumrechnung): Träger der Umrechnungsfaktoren **Theoretische KG pro Meter** und **Theoretische KG pro Stück** sowie der **Basiseinheit**. Diese Faktoren sind die fachliche Grundlage jeder Berechnung in der Anfrage-Kampagne. Die Pflege ist im Kapitel *Einrichtung* beschrieben.
- **Anfrage-Kampagne und Kampagnenartikel** (m+m Purchase Quote Manager): Die Kampagne bündelt die Artikel, für die Anfragen an Kreditoren vorbereitet werden. Die App erweitert die **Kampagnenartikel** um die drei Mengenfelder; die Bearbeitung ist im folgenden Kapitel beschrieben.

Eine eigene Stammdaten-Pflegemaske entsteht durch diese App nicht.

## Tägliche Arbeit: Kampagnenartikel mit KG, Meter und Stück

Die einzige durch diese App veränderte Anwenderoberfläche ist die Seite **Kampagnenartikel** des m+m Purchase Quote Manager. Dort ergänzt die App im Bereich **Allgemein** die drei Felder **KG**, **Meter** und **Stück**. Diese drei Felder werden über die im Kapitel *Einrichtung* beschriebenen Umrechnungsfaktoren des Artikels gesteuert; ohne diese Faktoren bleiben sie leer.

**Einstieg:** Öffnen Sie die gewünschte Anfrage-Kampagne im m+m Purchase Quote Manager und rufen Sie deren **Kampagnenartikel** auf. Die drei Felder erscheinen auf derselben Zeile wie die Basisfelder der Kampagnenzeile (unter anderem **Artikelnr.**, **Menge** und **Beschreibung**).

### Felder der Kampagnenzeile (ergänzt durch diese App)

Die folgende Tabelle beschreibt die durch diese App **hinzugefügten** Mengenfelder auf der Seite **Kampagnenartikel**. Die übrigen Felder der Zeile (etwa **Artikelnr.**, **Menge**, **Beschreibung**, **Variantencode**) stammen aus dem m+m Purchase Quote Manager und behalten dort ihr Standardverhalten; für die Umrechnung sind die drei folgenden Felder sowie **Artikelnr.** und **Menge** maßgeblich.

| Feld | Erläuterung |
|------|-------------|
| KG | Gewichtsmenge der Zeile in Kilogramm. Wenn Sie hier einen Wert eintragen, dann berechnet die App über die theoretischen Faktoren des Artikels die zugehörigen **Meter** und **Stück** neu und passt anschließend die **Menge** in der Basiseinheit an. Ist der Artikel nicht für die Einheitenumrechnung eingerichtet, dann bleibt das Feld leer und ohne Wirkung. |
| Meter | Längenmenge der Zeile in Meter. Wenn Sie hier einen Wert eintragen, dann berechnet die App über den Faktor **Theoretische KG pro Meter** das zugehörige Gewicht in **KG** sowie – sofern der Stück-Faktor gesetzt ist – die **Stück** neu und passt die **Menge** an. Ist am Artikel kein Meter-Faktor hinterlegt, dann bleibt das Feld leer. |
| Stück | Stückmenge der Zeile. Wenn Sie hier einen Wert eintragen, dann berechnet die App über den Faktor **Theoretische KG pro Stück** das zugehörige Gewicht in **KG** sowie – sofern der Meter-Faktor gesetzt ist – die **Meter** neu und passt die **Menge** an. Ist am Artikel kein Stück-Faktor hinterlegt, dann bleibt das Feld leer. |

**Zusammenspiel mit den Basisfeldern:**

- **Artikelnr.:** Wenn Sie den Artikel in der Zeile setzen oder ändern und der Artikel für die Einheitenumrechnung eingerichtet ist, dann übernimmt die App die theoretischen Faktoren des Artikels, setzt die tatsächlichen Faktoren zurück und berechnet KG, Meter und Stück passend zur bereits erfassten **Menge**.
- **Menge:** Wenn Sie die **Menge** in der Basiseinheit ändern, dann berechnet die App die drei Felder KG, Meter und Stück aus dieser Menge neu (sofern der Artikel eingerichtet ist).

### Ablauf der automatischen Umrechnung

Die Umrechnung läuft ohne zusätzliche Schaltfläche direkt beim Verlassen des geänderten Feldes ab. Der Ablauf ist immer derselbe:

1. **Auslöser:** Sie ändern in der Kampagnenzeile eines der Felder **Artikelnr.**, **Menge**, **KG**, **Meter** oder **Stück**.
2. **Prüfung der Einrichtung:** Die App prüft, ob der Artikel gemäß m+m Einheitenumrechnung für die Umrechnung eingerichtet ist. Ist er es nicht, dann bricht die App ab und die Zeile bleibt unverändert im Standardverhalten.
3. **Faktoren ermitteln:** Die App liest die am Artikel hinterlegten theoretischen Faktoren (**Theoretische KG pro Meter**, **Theoretische KG pro Stück**). Ein am Datensatz gespeicherter tatsächlicher Faktor hat Vorrang vor dem theoretischen; ist kein tatsächlicher Faktor vorhanden, dann verwendet die App den theoretischen Wert.
4. **Berechnung:** Ausgehend vom geänderten Feld berechnet die App die jeweils anderen der drei Mengen KG, Meter und Stück.
5. **Menge anpassen:** Zum Abschluss aktualisiert die App die **Menge** in der Basiseinheit, damit Basismenge und die drei Zusatzfelder konsistent bleiben.

Da die Umrechnung feldbasiert ausgelöst wird, genügt es, **eine** der Mengen zu erfassen; die App füllt die übrigen. Tragen Sie mehrere Felder nacheinander ein, dann setzt jede Eingabe eine neue Berechnung ausgehend vom zuletzt geänderten Feld in Gang.

## FAQ und Troubleshooting

### 1. Warum bleiben die Felder KG, Meter und Stück in der Kampagnenzeile leer?
Weil der Artikel nicht für die Einheitenumrechnung eingerichtet ist. Die App führt nur dann eine Berechnung durch, wenn am Artikel die Faktoren der m+m Einheitenumrechnung hinterlegt sind. Prüfen Sie auf der **Artikelkarte** die Werte **Theoretische KG pro Meter** und **Theoretische KG pro Stück**.

### 2. Warum wird nur eine der drei Zusatzmengen gefüllt und die anderen bleiben leer?
Weil am Artikel nur **einer** der beiden Faktoren gesetzt ist. Ist nur **Theoretische KG pro Meter** hinterlegt, dann kann die App nur zwischen KG und Meter umrechnen; das Feld **Stück** bleibt leer. Ist nur **Theoretische KG pro Stück** hinterlegt, dann verhält es sich umgekehrt. Für alle drei Felder müssen beide Faktoren gepflegt sein.

### 3. Was passiert, wenn ich die Menge in der Basiseinheit ändere?
Die App berechnet aus der neuen **Menge** die Werte für **KG**, **Meter** und **Stück** über die theoretischen Faktoren des Artikels neu, sofern der Artikel eingerichtet ist. So bleiben Basismenge und Zusatzmengen konsistent.

### 4. Was passiert, wenn ich direkt einen KG-Wert eintrage?
Die App rechnet vom eingetragenen **KG**-Wert auf **Meter** und **Stück** zurück und passt anschließend die **Menge** in der Basiseinheit an. Damit können Sie eine Zeile auch gewichtsorientiert erfassen, ohne zuerst die Stückzahl zu kennen.

### 5. Muss ich eine Schaltfläche drücken, damit die Umrechnung startet?
Nein. Die Umrechnung wird automatisch beim Verlassen des geänderten Feldes (**Artikelnr.**, **Menge**, **KG**, **Meter** oder **Stück**) ausgeführt. Eine eigene Aktion oder ein Dialog dieser App existiert nicht.

### 6. Welches Feld hat Vorrang, wenn mehrere Mengenfelder Werte enthalten?
Maßgeblich ist immer das **zuletzt geänderte** Feld. Von diesem Feld aus berechnet die App die übrigen Mengen. Tragen Sie nacheinander Werte ein, dann überschreibt jede neue Eingabe die zuvor berechneten Werte.

### 7. Warum unterscheiden sich berechnete Werte gelegentlich geringfügig von einer Handrechnung?
Die App verwendet die am Artikel hinterlegten theoretischen Faktoren und die in der m+m Einheitenumrechnung eingestellten Rundungsregeln und Rundungspräzisionen. Kleine Abweichungen gegenüber einer ungerundeten Handrechnung ergeben sich aus diesen Rundungseinstellungen.

### 8. Warum sehe ich in der Kampagnenzeile keine Felder für die theoretischen oder tatsächlichen KG-Faktoren?
Diese Faktorenfelder werden datenseitig geführt, aber in der Kampagnenzeile **nicht** angezeigt. Auf der Seite **Kampagnenartikel** blendet die App ausschließlich die drei Mengenfelder **KG**, **Meter** und **Stück** ein. Die Faktoren pflegen Sie an der **Artikelkarte**.

### 9. Gilt die Umrechnung auch für Artikel ohne KG-Bezug?
Nein. Für Artikel ohne hinterlegte KG-Faktoren greift die App nicht ein. Solche Artikel verhalten sich in der Anfrage-Kampagne unverändert wie im Standard des m+m Purchase Quote Manager.

### 10. Was ist zu tun, wenn nach der Installation zunächst nichts berechnet wird?
Prüfen Sie in dieser Reihenfolge: erstens, ob in der **KG Meter Stück Einrichtung** die Einheitencodes für KG, Meter und Stück gesetzt sind; zweitens, ob am betreffenden Artikel die theoretischen Faktoren hinterlegt sind; drittens, ob der erfasste Artikel tatsächlich dieser eingerichtete Artikel ist. Erst wenn Einheitencodes und Artikelfaktoren vorhanden sind, füllt die App die drei Mengenfelder.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Einsatz der App im Kontext der Einkaufs-Anfragebearbeitung. Jeder Screen und jede Menge stammt aus der Seite **Kampagnenartikel** des m+m Purchase Quote Manager; die Berechnung erfolgt über die Faktoren der m+m Einheitenumrechnung.

### Anwendungsfall 1: Anfrage für Coil-Material nach Gewicht erfassen

1. **Auslöser:** Ein Lieferant meldet telefonisch verfügbare Coil-Mengen für einen Stahlartikel. Der Einkäufer soll dazu eine Anfrage-Kampagne vorbereiten und die Mengen gewichtsorientiert festhalten.
2. **Einstieg in BC:** Der Einkäufer öffnet die betreffende Anfrage-Kampagne im m+m Purchase Quote Manager und ruft die **Kampagnenartikel** auf.
3. **Kernablauf:** Er trägt in einer neuen Zeile die **Artikelnr.** des Coil-Artikels ein; die App übernimmt die theoretischen Faktoren des Artikels. Anschließend erfasst er im Feld **KG** das vom Lieferanten genannte Gewicht. Die App berechnet daraus die zugehörigen **Meter** und **Stück** und passt die **Menge** in der Basiseinheit an.
4. **Abschluss:** Der Einkäufer prüft die berechneten Werte und setzt die Anfragebearbeitung im m+m Purchase Quote Manager fort. Eine eigene Buchung oder ein eigener Beleg entsteht durch diese App nicht.

### Anwendungsfall 2: Bedarf in Stück melden, Gewicht automatisch ermitteln

1. **Auslöser:** Aus der Fertigung geht per E-Mail ein Bedarf über eine bestimmte **Stückzahl** eines Langgut-Artikels ein. Für die Anfrage an den Kreditor wird jedoch das Gewicht benötigt.
2. **Einstieg in BC:** Der Einkäufer öffnet die passende Anfrage-Kampagne und deren **Kampagnenartikel**.
3. **Kernablauf:** Er erfasst die **Artikelnr.** und trägt im Feld **Stück** die gemeldete Stückzahl ein. Über den Faktor **Theoretische KG pro Stück** berechnet die App das Gewicht in **KG** und – sofern der Meter-Faktor am Artikel gepflegt ist – die **Meter**; die **Menge** in der Basiseinheit wird ebenfalls aktualisiert.
4. **Abschluss:** Der Einkäufer verwendet die berechneten KG-Werte für die weitere Anfrage- und Preisklärung im m+m Purchase Quote Manager.

### Anwendungsfall 3: Fehlende Umrechnung auf einer Zeile klären

1. **Auslöser:** Ein Einkäufer bemerkt, dass bei einem neu erfassten Artikel die Felder **KG**, **Meter** und **Stück** leer bleiben, obwohl er eine Menge eingetragen hat.
2. **Einstieg in BC:** Er bleibt zunächst auf den **Kampagnenartikeln** und öffnet anschließend die **Artikelkarte** des betreffenden Artikels.
3. **Kernablauf:** Auf der Artikelkarte stellt er fest, dass die Faktoren **Theoretische KG pro Meter** und **Theoretische KG pro Stück** nicht gepflegt sind. Der Stammdatenverantwortliche trägt die Faktoren nach; zusätzlich wird geprüft, ob in der **KG Meter Stück Einrichtung** die Einheitencodes gesetzt sind (siehe Kapitel *Einrichtung*).
4. **Abschluss:** Zurück in den **Kampagnenartikeln** erfasst der Einkäufer die Menge erneut; die App füllt nun die drei Mengenfelder korrekt.
