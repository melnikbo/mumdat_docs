---
title: Anwenderhandbuch m+m Logistic Differences with Unit Conversion
---

# Anwenderhandbuch m+m Logistic Differences with Unit Conversion

## Einleitung

Die Erweiterung **m+m Logistic Differences with Unit Conversion** ist eine reine Verbindungs-App. Sie besitzt selbst keine eigenen Seiten, Karten, Einrichtungsseiten oder Felder, sondern verbindet im Hintergrund die beiden bereits vorhandenen Module **Über- und Unterlieferung** (Logistic Differences) und **Einheitenumrechnung (KG/Meter/Stück)** (Unit Conversion). Ihre gesamte Wirkung entsteht automatisch beim Buchen von Warenein- und Warenausgängen.

Fachlich löst die App folgendes Problem: Wenn beim Buchen eines Wareneingangs oder Warenausgangs die tatsächlich gelieferte oder empfangene Menge von der ursprünglich bestellten oder beauftragten Menge abweicht (Über- oder Unterlieferung), muss die Einheitenumrechnung nach **KG**, **Meter** und **Stück** auf die real gebuchte Menge neu gerechnet werden. Ohne diese Verbindung würden die umgerechneten Werte auf der ursprünglichen Menge stehen bleiben und nicht zur gebuchten Menge passen. Die App sorgt dafür, dass die Einheitenumrechnung bei jeder Über- oder Unterlieferungsbuchung im Lager konsistent auf Basis der Menge nachgezogen wird.

**Zielgruppe:** Primär richtet sich dieses Handbuch an operativ tätige Anwender im Lager, die **Wareneingänge** und **Warenausgänge** buchen — insbesondere in Prozessen, in denen Über- oder Unterlieferungen zugelassen sind und in denen Artikel zusätzlich in KG, Meter und Stück geführt werden. Sekundär betrifft es Administratoren, die die zugrunde liegenden Module einrichten; die App selbst benötigt keine eigene Einrichtung.

**Kurzer Prozessüberblick:** Der Anwender bucht einen Warenein- oder Warenausgang mit einer von der Ursprungsmenge abweichenden Menge. Das Modul **Über- und Unterlieferung** prüft diese Abweichung anhand der eingerichteten Kontrollmethode. Beim Buchen setzt diese App das Steuerfeld **Einheitenfeld modifiziert** der betroffenen Beleg­zeile auf **Menge** zurück, damit das Modul **Einheitenumrechnung** die Werte **KG**, **Meter** und **Stück** aus der gebuchten Menge neu berechnet.

## Schnellstart für Anwender

Die App arbeitet vollautomatisch. Es gibt keine Aktion, keinen Button und keine Seite, die der Anwender für diese App aufrufen müsste. Der Nutzen tritt ein, sobald die beiden Basismodule eingerichtet und die App installiert ist.

Voraussetzung (einmalig, durch den Administrator):

1. Richten Sie zuerst die **Einheitenumrechnung** je Artikel ein: Hinterlegen Sie auf der **Artikelkarte** die Umrechnungsfaktoren **Theoretische KG pro Meter** und **Theoretische KG pro Stück**. Wenn diese Faktoren gefüllt sind, dann berechnet das System die Größen KG, Meter und Stück aus der Menge; ohne Faktoren bleiben diese Felder leer.
2. Richten Sie danach die **Über- und Unterlieferung** ein: Legen Sie auf der Seite **Über-/Unterlieferung Einrichtung** je Vorgang (Einkauf, Verkauf, Umlagerung) fest, ob Über- und Unterlieferungen kontrolliert werden, und definieren Sie über die **Kontrollmethode** und den **Kontrollwert**, in welchem Rahmen Mengenabweichungen zulässig sind.
3. Stellen Sie sicher, dass die App **m+m Logistic Differences with Unit Conversion** installiert ist. Danach ist keine weitere Konfiguration erforderlich.

Ablauf im Tagesgeschäft (durch den Anwender):

1. Öffnen Sie den **Warenausgang** bzw. den **Wareneingang** zum Auftrag oder zur Bestellung.
2. Erfassen Sie in der Zeile die tatsächlich zu liefernde bzw. zu empfangende Menge — auch dann, wenn diese von der **Ursprünglichen Menge** abweicht.
3. Buchen Sie den Beleg. Wird die Abweichung durch die Einrichtung als Über- oder Unterlieferung erkannt und akzeptiert, dann werden die umgerechneten Werte KG, Meter und Stück der Zeile automatisch aus der gebuchten Menge neu berechnet.
4. Kontrollieren Sie nach dem Buchen die Mengen und die umgerechneten Werte KG/Meter/Stück auf der Belegzeile bzw. auf dem gebuchten Beleg. Sie entsprechen jetzt der real gebuchten Menge.

## Voraussetzungen und Einrichtung

Diese App bringt **keine eigenen Einrichtungsseiten und keine eigenen Felder** mit. Sie wird ausschließlich über die Einrichtung der drei Abhängigkeiten gesteuert. Nehmen Sie die Einrichtung in der folgenden Reihenfolge vor, weil die Einheitenumrechnung die Datengrundlage für die spätere Neuberechnung liefert und die Über-/Unterlieferung erst die abweichende Menge zulässt.

### Einheitenumrechnung je Artikel einrichten

Wer richtet ein: Administrator oder Stammdatenverantwortlicher, vor der ersten Nutzung, je Artikel. Diese Einrichtung liefert die Umrechnungsfaktoren, mit denen die App später beim Buchen die Werte KG/Meter/Stück nachzieht. Sie wird im Tagesgeschäft in den Lagerbuchungen (siehe Abschnitt **Tägliche Arbeit**) wirksam.

Die Umrechnung wird auf der **Artikelkarte** hinterlegt. Wenn Sie in den Prozessen die automatische Umrechnung zwischen den Einheiten KG, Meter und Stück nutzen möchten, dann sind je Artikel Einrichtungen notwendig.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Theoretische KG pro Meter** | Wenn Sie hier einen Faktor eintragen, dann rechnet das System aus der Menge den Wert in KG und Meter um; ohne diesen Faktor bleibt bei laufenmeterbasierten Artikeln die Umrechnung zwischen KG und Meter leer. |
| **Theoretische KG pro Stück** | Wenn Sie hier einen Faktor eintragen, dann rechnet das System aus der Menge den Wert in KG und Stück um; ohne diesen Faktor bleibt die Umrechnung zwischen KG und Stück leer. |

Numerierte Schritte:

1. Rufen Sie über die BC-Suche (**Suchen**) die Artikelliste auf und öffnen Sie die **Artikelkarte** des betroffenen Artikels.
2. Tragen Sie die Umrechnungsfaktoren **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** ein. Ist nur einer der beiden Faktoren gefüllt, dann ist nur die Umrechnung zwischen diesen beiden Einheiten möglich; die jeweils andere Einheit bleibt leer. Sind gar keine Faktoren gefüllt, dann bleiben KG, Meter und Stück leer.
3. Wiederholen Sie dies für alle Artikel, die im Lager mit abweichenden Liefermengen und Einheitenumrechnung geführt werden.

Abschluss der Kette: Der eigentliche Nutzen — die Neuberechnung von KG/Meter/Stück auf die gebuchte Menge — tritt später automatisch beim Buchen des Warenein- bzw. Warenausgangs ein (siehe **Tägliche Arbeit**).

### Über- und Unterlieferung einrichten

Wer richtet ein: Administrator oder Einkaufs-/Verkaufsverantwortlicher, vor der ersten Nutzung, unternehmensweit sowie optional artikelbezogen. Diese Einrichtung entscheidet darüber, ob beim Buchen überhaupt eine von der Ursprungsmenge abweichende Menge zugelassen wird — und damit, wann die Neuberechnung durch diese App überhaupt ausgelöst wird. Sie wird im Abschnitt **Tägliche Arbeit** wirksam.

Auf der Seite **Über-/Unterlieferung Einrichtung** definieren Sie allgemeine Regeln je Vorgang. Auf der Registerkarte **Allgemein** schalten boolesche Felder die Kontrolle je Prozess vollständig ein oder aus; auf der Registerkarte **Vorgaben** legen Sie das Standardverhalten für Über- und Unterlieferung fest.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Einkauf** | Wenn aktiviert, dann greifen die Kontrollen für Über- und Unterlieferung im gesamten Einkaufsprozess; ist der Schalter aus, dann finden im Einkauf keine Prüfungen statt. |
| **Verkauf** | Wenn aktiviert, dann greifen die Kontrollen für Über- und Unterlieferung im gesamten Verkaufsprozess; ohne Aktivierung bleibt der Verkauf ungeprüft. |
| **Umlagerung** | Wenn aktiviert, dann greifen die Kontrollen im Umlagerungsprozess; ohne Aktivierung werden Mengenabweichungen bei Umlagerungen nicht kontrolliert. |
| **Kontrollmethode** | Legt fest, wie eine zulässige Abweichung berechnet wird. **Vorgabe:** Es gilt das Standardverhalten von Business Central, es greift keine zusätzliche Regel. **Prozentsatz:** Die zulässige Über- oder Unterlieferung wird als prozentualer Anteil der ursprünglichen Menge berechnet. **Absoluter Wert:** Die zulässige Abweichung wird als fester Betrag zur bzw. von der ursprünglichen Menge berechnet. |
| **Kontrollwert** | Wenn die Kontrollmethode **Prozentsatz** oder **Absoluter Wert** gewählt ist, dann definiert dieser Wert die zulässige Höhe der Abweichung; bei der Methode **Vorgabe** ist er ohne Wirkung. |
| **Warnung** | Wenn aktiviert, dann kann der Anwender die Mengenbegrenzung durch Bestätigung überschreiten und die Buchung trotzdem durchführen; ist die Warnung nicht aktiviert, dann verhindert eine Fehlermeldung die unzulässige Menge. Jede bestätigte Überschreitung wird protokolliert. |

Numerierte Schritte in Abhängigkeitsreihenfolge:

1. Öffnen Sie über die BC-Suche (**Suchen**) die Seite **Über-/Unterlieferung Einrichtung**.
2. Aktivieren Sie auf der Registerkarte **Allgemein** die Vorgänge (**Einkauf**, **Verkauf**, **Umlagerung**), für die Mengenabweichungen kontrolliert werden sollen. Wenn ein Vorgang aktiviert ist, dann werden dort Über- und Unterlieferungen geprüft.
3. Legen Sie auf der Registerkarte **Vorgaben** die **Kontrollmethode** und den **Kontrollwert** fest. Damit bestimmen Sie, welche Abweichung von der **Ursprünglichen Menge** überhaupt gebucht werden darf.
4. Entscheiden Sie über das Feld **Warnung**, ob eine Abweichung per Bestätigung erlaubt (Warnung aktiv) oder per Fehlermeldung unterbunden (Warnung inaktiv) wird.
5. Optional: Hinterlegen Sie über die **Über-/Unterlieferung Artikeleinrichtung** artikelbezogene Sonderregeln, wenn einzelne Artikel abweichende Toleranzen benötigen.

Abschluss der Kette: Erst wenn hier eine Abweichung zugelassen ist und der Anwender im Lager eine abweichende Menge bucht, wird das Steuerfeld **Einheitenfeld modifiziert** durch diese App auf **Menge** gesetzt und die Umrechnung neu berechnet (siehe **Tägliche Arbeit**).

## Tägliche Arbeit: Buchen von Warenein- und Warenausgang mit Mengenabweichung

Die tägliche Wirkung dieser App wird durch die im Abschnitt **Voraussetzungen und Einrichtung** beschriebenen Seiten gesteuert: Die **Artikelkarte** liefert über die Umrechnungsfaktoren die Datengrundlage, und die **Über-/Unterlieferung Einrichtung** entscheidet, ob eine abweichende Menge zulässig ist. Die App selbst besitzt in diesen Belegen keine eigenen Felder und keine eigenen Aktionen; sie greift ausschließlich im Moment des Buchens ein.

### Was die App beim Buchen automatisch tut

Beim Buchen eines Warenausgangs bzw. eines Wareneingangs mit abweichender Menge setzt die App das Feld **Einheitenfeld modifiziert** der Belegzeile auf den Wert **Menge**. Dadurch weiß das Modul Einheitenumrechnung, dass es die abgeleiteten Werte aus der Menge herzuleiten hat, und rechnet **KG**, **Meter** und **Stück** anhand der theoretischen Faktoren des Artikels neu — passend zur real gebuchten Menge statt zur ursprünglichen.

Dies geschieht in zwei Buchungswegen:

1. **Standard-Lagerbuchung:** beim Buchen von Wareneingang und Warenausgang über die Standard-Lagerbelege.
2. **Über-/Unterlieferungs-Buchung:** wenn das Modul Über- und Unterlieferung beim Buchen die abweichende Menge in die zugehörige Einkaufs- bzw. Verkaufszeile übernimmt.

In beiden Fällen ist das Verhalten für den Anwender identisch: Er erfasst und bucht die tatsächliche Menge; die umgerechneten Werte folgen automatisch.

### Ablauf am Warenausgang (Verkauf/Umlagerung)

| Feld | Erläuterung |
|------|-------------|
| **Ursprüngliche Menge** | Zeigt die ursprünglich beauftragte Menge der Zeile. Wenn die tatsächlich gelieferte Menge davon abweicht, dann dient dieser Wert dem Modul Über-/Unterlieferung als Bezug für die Toleranzprüfung. |
| **Zu liefern** | Erfassen Sie hier die tatsächlich zu liefernde Menge. Wenn dieser Wert von der Ursprünglichen Menge abweicht, dann wird die Abweichung gegen die Einrichtung geprüft und beim Buchen die Einheitenumrechnung neu gerechnet. |
| **Beleg komplett** | Wenn gesetzt, dann behandelt das System die Zeile mit der reduzierten Menge als vollständig geliefert und lässt keine weitere Lieferung mehr zu; das Feld kann nur gesetzt werden, wenn die Unterlieferungsregeln dies erlauben. |
| **Einheitenfeld modifiziert** | Steuerfeld für die Einheitenumrechnung. Diese App setzt es beim Buchen automatisch auf **Menge**, damit KG, Meter und Stück aus der gebuchten Menge abgeleitet werden. Der Anwender muss dieses Feld nicht selbst pflegen. |

Schritte:

1. Öffnen Sie den **Warenausgang** zum betreffenden Beleg.
2. Erfassen Sie in der Zeile die tatsächlich zu liefernde Menge im Feld **Zu liefern**.
3. Weicht die Menge ab, dann bestätigen oder verhindern Sie die Über-/Unterlieferung entsprechend der Einrichtung (Warnung bzw. Fehler).
4. Setzen Sie bei Bedarf **Beleg komplett**, wenn die Zeile mit der reduzierten Menge endgültig geliefert ist.
5. Buchen Sie den Warenausgang. Die App setzt **Einheitenfeld modifiziert** auf **Menge**; die Werte KG, Meter und Stück werden aus der gebuchten Menge neu berechnet.

### Ablauf am Wareneingang (Einkauf)

Der Wareneingang verhält sich spiegelbildlich zum Warenausgang.

| Feld | Erläuterung |
|------|-------------|
| **Ursprüngliche Menge** | Zeigt die ursprünglich bestellte Menge der Zeile als Bezug für die Toleranzprüfung bei Über- oder Unterlieferung. |
| **Menge geliefert** | Erfassen Sie hier die tatsächlich empfangene Menge. Weicht sie von der Ursprünglichen Menge ab, dann prüft das System die Abweichung gegen die Einrichtung und rechnet beim Buchen die Einheitenumrechnung neu. |
| **Beleg komplett** | Wenn gesetzt, dann gilt die Bestellzeile mit der empfangenen Menge als vollständig erledigt; weitere Wareneingänge auf diese Zeile sind dann nicht mehr möglich. |
| **Einheitenfeld modifiziert** | Wird von der App beim Buchen automatisch auf **Menge** gesetzt, damit KG, Meter und Stück aus der empfangenen Menge abgeleitet werden. |

Schritte:

1. Öffnen Sie den **Wareneingang** zur betreffenden Bestellung.
2. Erfassen Sie die tatsächlich empfangene Menge.
3. Bestätigen oder verhindern Sie eine Mengenabweichung gemäß Einrichtung.
4. Buchen Sie den Wareneingang. Die App setzt **Einheitenfeld modifiziert** auf **Menge**; die umgerechneten Werte werden aus der empfangenen Menge neu berechnet.

## Typische Anwendungsfälle

### Unterlieferung im Verkauf mit Einheitenumrechnung

**Auslöser:** Ein Lagermitarbeiter kommissioniert einen Verkaufsauftrag über einen Stahlartikel, der in Stück geführt und zugleich in KG und Meter umgerechnet wird. Beim Kommissionieren stellt sich heraus, dass nur eine geringere Menge lieferbar ist; der Kunde akzeptiert die Teilmenge als vollständige Lieferung.

**Einstieg in BC:** Der Mitarbeiter öffnet den zum Verkaufsauftrag gehörenden **Warenausgang**.

**Kernablauf:** In der Zeile trägt er im Feld **Zu liefern** die tatsächlich lieferbare Menge ein, die unter der **Ursprünglichen Menge** liegt. Da im Modul **Über-/Unterlieferung Einrichtung** der **Verkauf** aktiviert und die **Warnung** eingeschaltet ist, bestätigt er die Unterlieferung. Er setzt **Beleg komplett**, weil keine Restlieferung mehr erfolgen soll. Anschließend bucht er den Warenausgang.

**Abschluss:** Beim Buchen setzt die App **Einheitenfeld modifiziert** auf **Menge**. Die Einheitenumrechnung berechnet KG und Meter aus der tatsächlich gelieferten Stückzahl neu. Auf dem gebuchten Beleg stimmen Menge, KG und Meter überein.

### Überlieferung im Einkauf mit Einheitenumrechnung

**Auslöser:** Beim Wareneingang einer Coil-Lieferung liefert der Lieferant etwas mehr als bestellt. Die Mehrmenge ist im Rahmen der vereinbarten Toleranz zulässig.

**Einstieg in BC:** Der Mitarbeiter der Warenannahme öffnet den **Wareneingang** zur Bestellung.

**Kernablauf:** Er erfasst die tatsächlich empfangene, höhere Menge. Da im Modul **Über-/Unterlieferung Einrichtung** der **Einkauf** aktiviert und für Überlieferungen eine **Kontrollmethode** mit **Kontrollwert** hinterlegt ist, prüft das System die Mehrmenge. Liegt sie innerhalb der Toleranz, wird sie akzeptiert; andernfalls erscheint je nach Einstellung eine **Warnung** oder eine Fehlermeldung. Er bucht den Wareneingang.

**Abschluss:** Die App setzt beim Buchen **Einheitenfeld modifiziert** auf **Menge**; KG, Meter und Stück werden aus der empfangenen Mehrmenge neu berechnet und stehen konsistent auf der Zeile.

## FAQ und Troubleshooting

### Muss ich für diese App etwas einrichten?
Nein. Die App **m+m Logistic Differences with Unit Conversion** hat keine eigene Einrichtungsseite und keine eigenen Felder. Eingerichtet werden ausschließlich die Basismodule **Einheitenumrechnung** (auf der **Artikelkarte**) und **Über- und Unterlieferung** (auf der Seite **Über-/Unterlieferung Einrichtung**).

### Warum ändern sich meine KG-/Meter-/Stück-Werte erst nach dem Buchen?
Weil die App genau im Moment des Buchens des Warenein- bzw. Warenausgangs eingreift. Sie setzt dann das Feld **Einheitenfeld modifiziert** auf **Menge**, worauf die Einheitenumrechnung die Werte aus der gebuchten Menge ableitet.

### Warum bleiben KG, Meter und Stück leer, obwohl eine Menge gebucht wurde?
Weil auf der **Artikelkarte** keine Umrechnungsfaktoren hinterlegt sind. Ohne **Theoretische KG pro Meter** und/oder **Theoretische KG pro Stück** kann das System die abgeleiteten Werte nicht berechnen und lässt sie leer.

### Warum wird nur eine der Einheiten KG/Meter/Stück berechnet?
Weil auf der **Artikelkarte** nur einer der beiden theoretischen Faktoren gefüllt ist. Dann ist ausschließlich die Umrechnung zwischen den beiden verbundenen Einheiten möglich; die jeweils andere Einheit bleibt leer.

### Warum lässt das System eine abweichende Liefer- oder Empfangsmenge gar nicht zu?
Weil im Modul **Über-/Unterlieferung Einrichtung** für den betreffenden Vorgang keine Abweichung erlaubt ist. Steht die **Kontrollmethode** auf **Vorgabe** oder ist der Vorgang (**Einkauf**, **Verkauf**, **Umlagerung**) nicht aktiviert, dann greift keine erweiterte Toleranz und die Einheitenumrechnung wird durch diese App nicht neu ausgelöst.

### Warum bekomme ich beim Buchen eine Fehlermeldung statt einer Rückfrage?
Weil in der Einrichtung das Feld **Warnung** nicht aktiviert ist. Ist die **Warnung** ausgeschaltet, dann verhindert eine Fehlermeldung die unzulässige Menge; erst mit aktivierter **Warnung** kann der Anwender die Abweichung per Bestätigung überschreiben.

### Wird protokolliert, wenn ich eine Über- oder Unterlieferung bestätige?
Ja. Jede per **Warnung** bestätigte Über- oder Unterlieferung wird durch das Basismodul in den Über-/Unterlieferungsprotokollen festgehalten. Diese App fügt dem nichts hinzu und ändert das Protokollverhalten nicht.

### Muss ich das Feld Einheitenfeld modifiziert selbst setzen?
Nein. Dieses Steuerfeld wird von der App beim Buchen automatisch auf **Menge** gesetzt. Ein manuelles Eingreifen ist im Zusammenspiel dieser Buchungswege nicht erforderlich.

### Gilt die Neuberechnung auch bei Umlagerungen?
Die App greift bei den Buchungswegen für Wareneingang und Warenausgang ein. Für Umlagerungen ist im Modul **Über-/Unterlieferung Einrichtung** der Vorgang **Umlagerung** separat zu aktivieren, damit dort eine abweichende Menge überhaupt zugelassen wird.

### Was passiert, wenn ich Beleg komplett setze, aber weniger geliefert habe?
Dann behandelt das System die Zeile mit der reduzierten Menge als vollständig erledigt und lässt keine Restlieferung mehr zu. Das Feld **Beleg komplett** kann nur gesetzt werden, wenn die Unterlieferungsregeln dies zulassen; die Einheitenumrechnung wird beim Buchen auf die reduzierte Menge neu gerechnet.
