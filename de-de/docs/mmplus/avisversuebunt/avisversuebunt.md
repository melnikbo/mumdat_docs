---
title: Anwenderhandbuch m+m Logistic Management with Logistic Differences
---

# Anwenderhandbuch m+m Logistic Management with Logistic Differences

## Einleitung

Diese Erweiterung ist ein Bindeglied zwischen zwei bereits vorhandenen m+m Apps: **m+m Logistic Management** (Avisierung und Versandplanung) und **m+m Logistic Differences** (Über- und Unterlieferungskontrolle). Sie sorgt dafür, dass die Regeln für Über- und Unterlieferung nicht nur beim Buchen von Standardbelegen, sondern bereits **während der Avisierung und der Versandplanung** greifen, wenn dort Mengen auf Beleg­zeilen zugewiesen werden.

Fachlich fügt die Erweiterung eine zusätzliche Steuerung in die Planungszeilen ein: das Kennzeichen **Bestellung komplett** (in der Avisierung) bzw. **Auftrag komplett** (in der Versandplanung). Mit diesem Kennzeichen meldet der Anwender, dass für die betroffene Herkunftszeile trotz einer Mengendifferenz keine weiteren Lieferungen oder Eingänge mehr folgen. Ohne dieses Kennzeichen prüft die Erweiterung beim Erfassen der **Menge für Zuweisung**, ob die geplante Menge nach den in **m+m Logistic Differences** hinterlegten Regeln zulässig ist, und blockiert oder bestätigt sie entsprechend.

**Zielgruppe.** Primär richtet sich dieses Handbuch an die **operativen Anwender** in Wareneingang, Versand und Logistik, die täglich Avisierungen und Versandplanungen bearbeiten und dabei Mengen zuweisen. Sekundär betrifft es **Administratoren und Key-User**, die die Über- und Unterlieferungsregeln in **m+m Logistic Differences** einrichten – ohne diese Einrichtung ist die Zusatzsteuerung wirkungslos.

**Kurzer Prozessüberblick.** Der Administrator legt in der **m+m Logistic Differences**-Einrichtung fest, ob und wie stark Über- und Unterlieferungen im Einkauf und im Verkauf erlaubt sind. Der operative Anwender erfasst anschließend in der **Avisierung** bzw. in der **Versandplanung** die zuzuweisende Menge; die Erweiterung prüft diese Menge gegen die Regeln. Weicht die Summe aus bereits gebuchter, bereits zugewiesener und neu zugewiesener Menge von der ursprünglichen Menge ab, setzt der Anwender bei Bedarf das Kennzeichen **Bestellung komplett** bzw. **Auftrag komplett**, um die Zeile bewusst abzuschließen.

## Schnellstart für Anwender

Der schnellste Weg zur korrekt geprüften Mengenzuweisung. Die Einrichtung (Schritt 1) ist einmalige Voraussetzung und wird vom Administrator vorgenommen; die Schritte 2 bis 5 gehören zur täglichen Arbeit.

1. **Einrichtung prüfen (Voraussetzung, Administrator).** Stellen Sie in der Seite **Über-/Unterlieferung Einrichtung** (App **m+m Logistic Differences**) sicher, dass **Einkauf** bzw. **Verkauf** aktiviert ist und dass in den Vorgaben bzw. in der Artikeleinrichtung eine passende **Kontrollmethode** hinterlegt ist. Ohne aktive Einrichtung findet keine zusätzliche Prüfung statt (siehe Kapitel **Einrichtung**).
2. **Planungszeile öffnen.** Öffnen Sie die betreffende **Avisierung** oder **Versandplanung** und markieren Sie in den Zeilen die Herkunftszeile, für die Sie eine Menge zuweisen möchten.
3. **Menge für Zuweisung erfassen.** Tragen Sie im Feld **Menge für Zuweisung** die Menge ein, die Sie dieser Zeile zuordnen. Beim Verlassen des Feldes prüft die Erweiterung die zulässige Über-/Unterlieferung. Bei Verstoß gegen die Regel erhalten Sie – je nach Einrichtung – eine Warnung mit Bestätigungsmöglichkeit oder eine Fehlermeldung.
4. **Bei Unterlieferung: Kennzeichen setzen.** Soll die Zeile trotz geringerer Menge abgeschlossen werden, setzen Sie den Haken **Bestellung komplett** (Avisierung) bzw. **Auftrag komplett** (Versandplanung) in der Zeile. Das Kennzeichen lässt sich nur setzen, wenn die Unterlieferungsregeln dies zulassen (siehe Kapitel **Tägliche Arbeit**).
5. **Registrieren bzw. buchen.** Setzen Sie den gewohnten Prozess der App **m+m Logistic Management** fort: Freigeben und **Registrieren** der Avisierung bzw. der Versandplanung. Das Kennzeichen wird dabei in die Folgebelege (Wareneingang, Warenausgang, Einkaufs-/Verkaufszeile) und in die registrierten Zeilen übernommen.

## Einrichtung

Diese Erweiterung besitzt **keine eigene Einrichtungsseite**. Ihr Verhalten wird vollständig durch die Einrichtung der abhängigen App **m+m Logistic Differences** gesteuert. Der folgende Abschnitt beschreibt daher, welche dortigen Einstellungen die zusätzliche Prüfung in Avisierung und Versandplanung aktivieren und wie sie zusammenwirken. Die Feldwerte werden vom Programmcode dieser Erweiterung ausgewertet (u. a. die Kennzeichen für aktive Über-/Unterlieferung sowie die Kontrollmethode).

### Über- und Unterlieferung einrichten

**Prozessintro.** Diese Einrichtung nimmt der **Administrator oder Key-User einmalig vor der ersten Nutzung** vor. Sie entscheidet, ob die Mengenzuweisung in Avisierung und Versandplanung überhaupt zusätzlich geprüft wird und wie streng. Ist keine Über-/Unterlieferung aktiv, verhält sich die Zuweisung wie im Standard, und das Kennzeichen **Bestellung komplett** / **Auftrag komplett** bleibt ohne Wirkung. Die hier gesetzten Werte konsumieren die täglichen Arbeitsbereiche **Avisierung** und **Versandplanung** (Querverweis: Kapitel **Tägliche Arbeit in der Avisierung** und **Tägliche Arbeit in der Versandplanung**).

**Einstieg:** Öffnen Sie über die Aktion **Suchen** die Seite **Über-/Unterlieferung Einrichtung**. Diese unternehmensweite Einrichtung (ein Datensatz pro Mandant) besitzt keine übergeordnete Belegzeile und wird deshalb – wie in der App **m+m Logistic Differences** vorgesehen – über die Suche geöffnet.

Die folgenden Einstellungen der Seite **Über-/Unterlieferung Einrichtung** und der zugehörigen Artikeleinrichtung steuern das Verhalten dieser Erweiterung:

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Einkauf** | Wenn aktiviert, greifen die Über-/Unterlieferungskontrollen im gesamten Einkaufsprozess. Erst dadurch prüft diese Erweiterung die **Menge für Zuweisung** in Avisierungen zu Einkaufsbestellungen; ist es deaktiviert, wird die Menge ohne zusätzliche Prüfung übernommen. |
| **Verkauf** | Wenn aktiviert, greifen die Kontrollen im gesamten Verkaufsprozess. Erst dadurch prüft diese Erweiterung die **Menge für Zuweisung** in Versandplanungen zu Verkaufs- und Umlagerungszeilen; ohne Aktivierung entfällt die zusätzliche Prüfung. |
| **Kontrollmethode** | Legt fest, wie eine Abweichung bewertet wird. **Vorgabe:** Es gilt das Standardverhalten von Business Central ohne zusätzliche Grenze. **Prozentsatz:** Die zulässige Über- bzw. Unterlieferung wird als Prozentsatz der ursprünglichen Menge berechnet. **Absoluter Wert:** Die zulässige Abweichung ergibt sich aus einem festen Mengenwert. Weicht die Zuweisung außerhalb der so bestimmten Grenze ab, wird sie – abhängig von **Warnung** – blockiert oder zur Bestätigung vorgelegt. |
| **Kontrollwert** | Wenn gesetzt, definiert dieser Wert die konkrete Grenze zur gewählten **Kontrollmethode** (Prozentsatz oder absolute Menge). Er wird zur ursprünglichen Menge ins Verhältnis gesetzt, um die maximal zulässige Über- bzw. Unterliefermenge zu ermitteln, gegen die die **Menge für Zuweisung** geprüft wird. |
| **Warnung** | Wenn aktiviert, erhält der Anwender bei einer Regelverletzung eine Warnung, die er bestätigen oder ablehnen kann; bei Ablehnung wird die zulässige Menge übernommen. Wenn deaktiviert, wird eine unzulässige **Menge für Zuweisung** mit einer Fehlermeldung abgewiesen und muss korrigiert werden. |

**Kontrolltypen in der Vorgaben-/Artikeleinrichtung (Feld „Definiert“).** Für jede Regel wird festgelegt, ob sie eine Über- oder eine Unterlieferung betrifft:

- **Überlieferung:** Die Regel greift, wenn im Kauf-, Verkaufs- oder Umlagerungsprozess mehr geliefert bzw. zugewiesen wird als ursprünglich vorgesehen. In dieser Erweiterung wird sie ausgewertet, wenn die Summe aus gebuchter, zugewiesener und neu zugewiesener Menge die ursprüngliche Menge **überschreitet**.
- **Unterlieferung:** Die Regel greift, wenn weniger geliefert bzw. zugewiesen wird. In dieser Erweiterung wird sie ausgewertet, wenn die Summe die ursprüngliche Menge **unterschreitet**. Nur bei einer erlaubten Unterlieferung lässt sich das Kennzeichen **Bestellung komplett** / **Auftrag komplett** setzen.

**Ausgleich mit Art (Regelgeltung).** In der Artikeleinrichtung bestimmt die **Ausgleich mit Art**, für welchen Geschäftspartner- bzw. Belegkreis eine spezifische Regel gilt. Diese Erweiterung wertet die Regel je Herkunft der Planungszeile aus:

- **Kreditor** / **Alle Kreditoren:** Für Avisierungen aus Einkaufsbestellungen. Die Prüfung erfolgt gegen den Kreditor der zugrunde liegenden Einkaufszeile.
- **Debitor** / **Alle Debitoren:** Für Versandplanungen aus Verkaufsaufträgen. Die Prüfung erfolgt gegen den Debitor der zugrunde liegenden Verkaufszeile.
- **Umlagerung:** Für Versandplanungen aus Umlagerungsaufträgen. Die Prüfung erfolgt gegen den Ausgangs-Lagerort der Umlagerungszeile.

Über die Felder **Ausgleich mit Art** und **Ausgleich mit Nummer** wird die Regel bei Bedarf auf einen konkreten Kreditor, Debitor oder eine konkrete Umlagerung eingegrenzt.

**Numerierte Aktivierungsschritte (Abhängigkeitsreihenfolge).** So aktiviert ein Administrator die zusätzliche Mengenprüfung in Avisierung und Versandplanung Ende zu Ende:

1. **Zuerst** öffnen Sie **Über-/Unterlieferung Einrichtung** und aktivieren Sie **Einkauf** (für die Avisierung) bzw. **Verkauf** (für die Versandplanung). Wenn aktiviert, werden die Kontrollen im jeweiligen Prozess grundsätzlich eingeschaltet.
2. **Danach** legen Sie in den **Vorgaben** oder in der **Artikeleinrichtung** die **Kontrolltypen** (**Definiert** = Überlieferung/Unterlieferung), die **Kontrollmethode** und den **Kontrollwert** fest. Wenn gesetzt, bestimmt dies die zulässige Bandbreite der Mengenabweichung.
3. **Danach** entscheiden Sie über das Feld **Warnung**, ob eine Regelverletzung als bestätigbare Warnung oder als harte Fehlermeldung erscheint.
4. **Schließlich** nutzt der operative Anwender die Einstellungen im Tagesablauf: Er erfasst die **Menge für Zuweisung** in der Avisierung bzw. Versandplanung und setzt bei zulässiger Unterlieferung das Kennzeichen **Bestellung komplett** / **Auftrag komplett** (Querverweis: Kapitel **Tägliche Arbeit**).

**Abhängigkeitshinweis.** Der Programmcode dieser Erweiterung liest die aktiven Einkaufs-/Verkaufskennzeichen und die Kontrollmethode aus der Einrichtung von **m+m Logistic Differences**. Sind diese nicht vorhanden oder nicht aktiv, unterbleibt jede zusätzliche Prüfung, und das Kennzeichen **Bestellung komplett** / **Auftrag komplett** hat keine Steuerungswirkung.

## Tägliche Arbeit in der Avisierung

Die Avisierung stammt aus der App **m+m Logistic Management** und dient dazu, avisierte Mengen zu einer Einkaufsbestellung zu planen und später zu registrieren. Diese Erweiterung ergänzt die **Avisierungszeilen** um das Kennzeichen **Bestellung komplett** und schaltet die Über-/Unterlieferungsprüfung bei der Mengenzuweisung ein.

**Steuernde Einrichtung.** Ob und wie geprüft wird, ergibt sich aus der Seite **Über-/Unterlieferung Einrichtung** (Kennzeichen **Einkauf**, **Kontrollmethode**, **Kontrollwert**, **Warnung**; siehe Kapitel **Über- und Unterlieferung einrichten**). Ist der Einkauf dort nicht aktiviert, entfällt die zusätzliche Prüfung.

**Einstieg:** Öffnen Sie die **Avisierung** aus der Einkaufsbestellung heraus oder über die Avisierungsliste der App **m+m Logistic Management** und wechseln Sie in die **Avisierungszeilen**.

### Felder der Avisierungszeile (durch diese Erweiterung ergänzt)

Die Avisierungszeile zeigt neben den Standardspalten der App **m+m Logistic Management** (u. a. **Artikelnr.**, **Beschreibung**, **Lagerortcode**, **Variantencode**, **Einheitencode**, **Menge**, **Restmenge**, **Menge für Zuweisung**) das folgende, durch diese Erweiterung hinzugefügte Feld:

| Feld | Erläuterung |
|------|-------------|
| **Bestellung komplett** | Wenn aktiviert, meldet der Anwender, dass die Herkunftszeile trotz einer unterschrittenen Menge abgeschlossen ist und keine weiteren Eingänge mehr erwartet werden. Das Kennzeichen lässt sich nur setzen, wenn die Unterlieferungsregeln der Einrichtung dies zulassen; ist keine Unterlieferung erlaubt, wird der Haken automatisch zurückgesetzt. Beim Registrieren wird der Wert in die Einkaufszeile bzw. den Wareneingang übernommen, sodass die Restmenge nicht weiter verplant wird. |

**Zusammenspiel mit der Menge für Zuweisung.** Tragen Sie in der Zeile die **Menge für Zuweisung** ein, prüft die Erweiterung beim Verlassen des Feldes die Summe aus bereits gebuchter Menge (**Menge geliefert**), bereits zugewiesener Menge und der neuen Menge gegen die **ursprüngliche Menge**:

- Liegt die Summe **über** der ursprünglichen Menge und ist keine Überlieferung erlaubt, wird die Menge abgewiesen bzw. zur Bestätigung vorgelegt.
- Liegt die Summe **unter** der ursprünglichen Menge und ist keine Unterlieferung erlaubt, gilt dies als Teil-Eingang; die Zeile bleibt offen. Erst wenn Unterlieferung erlaubt ist und das Kennzeichen **Bestellung komplett** gesetzt wird, wird die Zeile abgeschlossen.

## Tägliche Arbeit in der Versandplanung

Die Versandplanung stammt ebenfalls aus der App **m+m Logistic Management** und plant Versandmengen zu Verkaufsaufträgen und Umlagerungsaufträgen. Diese Erweiterung ergänzt die **Versandplanungszeilen** um das Kennzeichen **Auftrag komplett** und schaltet die Über-/Unterlieferungsprüfung bei der Mengenzuweisung ein.

**Steuernde Einrichtung.** Ob und wie geprüft wird, ergibt sich aus der Seite **Über-/Unterlieferung Einrichtung** (Kennzeichen **Verkauf**, **Kontrollmethode**, **Kontrollwert**, **Warnung**; siehe Kapitel **Über- und Unterlieferung einrichten**). Ist der Verkauf dort nicht aktiviert, entfällt die zusätzliche Prüfung.

**Einstieg:** Öffnen Sie in der **Versandplanungszuordnung und Lagersteuerung** (App **m+m Logistic Management**, über **Suchen** erreichbar) die gewünschte Zeile, setzen Sie zunächst einen **Debitorenfilter**, wählen Sie über die Aktion **Zeilen auswählen** die zu bearbeitenden Aufträge und wechseln Sie anschließend in die **Versandplanungszeilen**.

### Felder der Versandplanungszeile (durch diese Erweiterung ergänzt)

Die Versandplanungszeile zeigt neben den Standardspalten der App **m+m Logistic Management** (u. a. **Ausgewählt**, **Artikelnr.**, **Beschreibung**, **Lagerortcode**, **Variantencode**, **Einheitencode**, **Menge**, **Restmenge**, **Menge für Zuweisung**, **Offen**) das folgende, durch diese Erweiterung hinzugefügte Feld:

| Feld | Erläuterung |
|------|-------------|
| **Auftrag komplett** | Wenn aktiviert, meldet der Anwender, dass die Herkunftszeile (Verkaufs- oder Umlagerungszeile) trotz einer unterschrittenen Menge abgeschlossen ist und keine weiteren Lieferungen mehr erfolgen. Das Kennzeichen lässt sich nur setzen, wenn die Unterlieferungsregeln der Einrichtung dies zulassen; andernfalls wird der Haken automatisch zurückgesetzt. Beim Registrieren wird der Wert in die Verkaufszeile bzw. den Warenausgang übernommen, sodass die Restmenge nicht weiter verplant wird. |

**Herkunft der Zeile (Debitor oder Umlagerung).** Die Erweiterung erkennt anhand der Herkunft, welche Regel gilt: Bei einer Verkaufszeile prüft sie gegen die Regeln für **Debitor** / **Alle Debitoren**, bei einer Umlagerungszeile gegen die Regel für **Umlagerung**. Der Prüfmechanismus über die **Menge für Zuweisung** entspricht dem der Avisierung (siehe oben).

## Buchungs- und Registrierablauf

Diese Erweiterung führt keinen eigenen Buchungslauf ein; sie schaltet sich in die bestehenden Prüfpunkte der App **m+m Logistic Management** ein. Der Ablauf, in dem das Kennzeichen und die Mengenprüfung wirken, ist:

1. **Zeile auswählen** in der **Avisierung** bzw. in der **Versandplanungszuordnung und Lagersteuerung**.
2. **Menge für Zuweisung erfassen** in der Zeile. Die Erweiterung prüft die zulässige Über-/Unterlieferung. Bei **Warnung** = aktiv erscheint eine Bestätigungsabfrage, bei **Warnung** = inaktiv eine Fehlermeldung.
3. **Bei zulässiger Unterlieferung** das Kennzeichen **Bestellung komplett** (Avisierung) bzw. **Auftrag komplett** (Versandplanung) in der Zeile setzen, um die Herkunftszeile bewusst abzuschließen.
4. **Freigeben** der Avisierung bzw. Versandplanung im gewohnten Prozess der App **m+m Logistic Management**.
5. **Registrieren** der Avisierung bzw. Versandplanung. Dabei überträgt die Erweiterung das Kennzeichen in die Folgebelege: in die **Einkaufszeile** bzw. **Verkaufszeile**, in den **Wareneingang** bzw. **Warenausgang** und in die **registrierte** Avisierungs- bzw. Versandplanungszeile.
6. **Buchen** des Wareneingangs bzw. Warenausgangs im Standardprozess von Business Central. Ist das Kennzeichen gesetzt, wird die verbleibende Restmenge nicht als offene Unterlieferung weitergeführt.

**Hinweis zu Teilmengen.** Solange Unterlieferung erlaubt ist, dürfen Zeilen bewusst mit einer geringeren Menge abgeschlossen werden; ein Ausgleich der Restmenge ist nicht erzwungen. Ohne gesetztes Kennzeichen bleibt eine unterschrittene Zeile offen und kann in weiteren Lieferungen ergänzt werden.

## Historie, registrierte Belege und Archiv

Das Kennzeichen wird nicht nur in den aktiven Planungszeilen, sondern auch in den nachgelagerten Datenbeständen geführt, damit die getroffene Entscheidung nachvollziehbar bleibt:

| Bereich | Erläuterung |
|---------|-------------|
| **Registrierte Avisierung** (registrierte Avisierungszeile) | Beim Registrieren wird der Wert des Kennzeichens **Bestellung komplett** aus der Avisierungszeile in die registrierte Zeile übernommen und bleibt dort als abgeschlossene Entscheidung sichtbar. |
| **Registrierte Versandplanung** (registrierte Versandplanungszeile) | Beim Registrieren wird der Wert des Kennzeichens **Auftrag komplett** aus der Versandplanungszeile in die registrierte Zeile übernommen. |
| **Avisierungszeile (Archiv)** | Auch die archivierte Avisierungszeile führt das Kennzeichen **Bestellung komplett** mit, sodass archivierte Vorgänge den seinerzeit gesetzten Zustand widerspiegeln. |

Diese Datenbestände enthalten das Kennzeichen als Feld; eigene Aktionen oder Listenfilter fügt die Erweiterung hier nicht hinzu.

## FAQ und Troubleshooting

### 1. Warum wird meine Menge für Zuweisung mit einer Fehlermeldung abgewiesen?
Die eingetragene Menge verletzt eine Über- oder Unterlieferungsregel, und in der **Über-/Unterlieferung Einrichtung** ist das Feld **Warnung** für diesen Fall nicht aktiviert. Ohne Warnung wird eine unzulässige Menge hart abgewiesen. Korrigieren Sie die Menge oder passen Sie – falls fachlich gewünscht – die Einrichtung an.

### 2. Warum erscheint stattdessen nur eine Warnung, die ich bestätigen kann?
Weil in der Einrichtung das Feld **Warnung** aktiviert ist. Dann dürfen Sie eine Abweichung bewusst bestätigen; lehnen Sie ab, wird die zulässige Menge übernommen.

### 3. Warum lässt sich das Kennzeichen „Bestellung komplett“ bzw. „Auftrag komplett“ nicht setzen?
Das Kennzeichen ist nur bei einer **zulässigen Unterlieferung** setzbar. Ist im aktuellen Fall keine Unterlieferung erlaubt oder liegt gar keine Unterlieferung vor, wird der Haken beim Speichern automatisch wieder entfernt.

### 4. Was bewirkt das Kennzeichen konkret?
Es meldet, dass die Herkunftszeile trotz geringerer Menge abgeschlossen ist. Die Restmenge wird nicht weiter als offene Unterlieferung verplant, und der Wert wird beim Registrieren in Einkaufs-/Verkaufszeile, Wareneingang/Warenausgang und die registrierte Zeile übernommen.

### 5. Warum passiert bei der Mengenzuweisung gar keine zusätzliche Prüfung?
Weil in der **Über-/Unterlieferung Einrichtung** weder **Einkauf** (für die Avisierung) noch **Verkauf** (für die Versandplanung) aktiviert ist oder keine Kontrollregel hinterlegt wurde. Diese Erweiterung wertet nur eine vorhandene, aktive Einrichtung aus.

### 6. Gilt die Prüfung auch für Umlagerungen in der Versandplanung?
Ja. Stammt die Versandplanungszeile aus einem Umlagerungsauftrag, prüft die Erweiterung gegen die Regel mit **Ausgleich mit Art** = **Umlagerung** und den Ausgangs-Lagerort der Umlagerungszeile.

### 7. Nach welcher Menge richtet sich die Prüfung – nach der Belegmenge oder einer anderen Menge?
Maßgeblich ist die **ursprüngliche Menge** der Herkunftszeile. Ihr werden die bereits gebuchte Menge, die bereits zugewiesene Menge und die neu erfasste **Menge für Zuweisung** gegenübergestellt.

### 8. Warum verschwindet mein Haken, nachdem ich in der Einkaufsbestellung die Menge geändert habe?
Wird die Menge der Herkunftszeile geändert, sind wieder weitere Eingänge oder Lieferungen möglich; ein zuvor gesetztes Kennzeichen „komplett“ wird deshalb zurückgesetzt. Setzen Sie es nach der letzten Zuweisung erneut.

### 9. Warum heißt das Feld in der Avisierung „Bestellung komplett“ und in der Versandplanung „Auftrag komplett“?
Die Bezeichnungen entsprechen dem jeweiligen Beleg­kontext: Die Avisierung bezieht sich auf Einkaufsbestellungen, die Versandplanung auf Verkaufs- bzw. Umlagerungsaufträge. Fachlich hat das Kennzeichen in beiden Fällen dieselbe Wirkung.

### 10. Muss ich die Restmenge exakt ausgleichen, bevor ich abschließen darf?
Nein. Bei erlaubter Unterlieferung dürfen Sie die Zeile bewusst mit geringerer Menge über das Kennzeichen abschließen. Ein erzwungener Ausgleich der Restmenge auf null besteht nur, wenn Ihre Einrichtung Unterlieferungen nicht zulässt.

## Typische Anwendungsfälle

### Anwendungsfall 1: Einkaufsbestellung wird unterliefert und bewusst abgeschlossen

1. **Auslöser.** Ein Lieferant meldet telefonisch, dass er von der bestellten Menge nur einen Teil liefern kann und keine Restlieferung folgt.
2. **Einstieg in BC.** Der Anwender öffnet aus der Einkaufsbestellung heraus die **Avisierung** und wechselt in die **Avisierungszeilen**.
3. **Kernablauf.** Er trägt im Feld **Menge für Zuweisung** die tatsächlich avisierte Teilmenge ein. Da Unterlieferung im Einkauf erlaubt ist, meldet die Erweiterung – abhängig von **Warnung** – eine bestätigbare Warnung. Um die Zeile endgültig abzuschließen, setzt der Anwender den Haken **Bestellung komplett**. Anschließend gibt er die Avisierung frei.
4. **Abschluss.** Beim **Registrieren** der Avisierung wird **Bestellung komplett** in die Einkaufszeile und den Wareneingang übernommen. Nach dem Buchen des Wareneingangs bleibt keine offene Restmenge zur weiteren Verplanung.

### Anwendungsfall 2: Verkaufsauftrag wird in der Versandplanung überliefert

1. **Auslöser.** Der Versand meldet intern, dass für einen Kunden eine geringfügig höhere Menge versendet werden soll als im Auftrag vorgesehen.
2. **Einstieg in BC.** Der Anwender öffnet die **Versandplanungszuordnung und Lagersteuerung**, filtert über den **Debitorenfilter** auf den Kunden, wählt über **Zeilen auswählen** die Auftragszeile und öffnet die **Versandplanungszeilen**.
3. **Kernablauf.** Er trägt im Feld **Menge für Zuweisung** die höhere Menge ein. Ist im Verkauf eine Überlieferung mit **Kontrollmethode** und **Kontrollwert** hinterlegt und liegt die Menge innerhalb der Grenze, wird sie – je nach **Warnung** – akzeptiert oder zur Bestätigung vorgelegt; überschreitet sie die Grenze, erscheint eine Fehlermeldung.
4. **Abschluss.** Nach **Freigeben** und **Registrieren** der Versandplanung fließt die geprüfte Menge in den Warenausgang und die gebuchte Verkaufslieferung ein.

### Anwendungsfall 3: Umlagerung mit Teilmenge abschließen

1. **Auslöser.** Bei einer Umlagerung zwischen zwei Lagerorten steht weniger Bestand zur Verfügung als geplant; der Rest wird nicht mehr umgelagert.
2. **Einstieg in BC.** Der Anwender öffnet die **Versandplanung** zur Umlagerung und wechselt in die **Versandplanungszeilen**.
3. **Kernablauf.** Er erfasst die verfügbare **Menge für Zuweisung**. Die Erweiterung prüft gegen die Regel mit **Ausgleich mit Art** = **Umlagerung**. Ist die Unterlieferung zulässig, setzt der Anwender **Auftrag komplett**, um die Umlagerungszeile abzuschließen.
4. **Abschluss.** Nach dem **Registrieren** wird das Kennzeichen in den Warenausgang der Umlagerung übernommen; die nicht umgelagerte Restmenge bleibt nicht als offene Unterlieferung stehen.
