---
title: Anwenderhandbuch m+m Production Differences with Unit Conversion
---

# Anwenderhandbuch m+m Production Differences with Unit Conversion

## Einleitung

Die App **m+m Production Differences with Unit Conversion** verbindet zwei bereits vorhandene m+m-Apps miteinander: **m+m Production Differences** (Über- und Unterproduktion) und **m+m Unit Conversion** (Einheitenumrechnung KG/Meter/Stück). Sie ist eine reine Verbindungs-App und stellt selbst keine eigene Seite, keinen eigenen Menüpunkt und keine eigene Einrichtungsseite bereit. Ihre Wirkung entsteht ausschließlich im Hintergrund: Sie sorgt dafür, dass bei einer Fertigmeldung mit abweichender Menge (Über- oder Unterproduktion) die Werte **KG**, **Meter** und **Stück** korrekt neu umgerechnet und über alle beteiligten Belege hinweg konsistent gehalten werden.

**Voraussetzung** ist, dass die Apps **m+m Production Differences** und **m+m Unit Conversion** installiert und eingerichtet sind. Ohne diese beiden Apps hat die Verbindungs-App keine Funktion.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwenderinnen und Anwender in der Fertigung**, die freigegebene Fertigungsaufträge über das **Produktions-Buch.-Blatt** rückmelden (Ist-Meldung), Chargen in den **Artikelverfolgungszeilen** pflegen und mit den Mengen in **KG/Meter/Stück** arbeiten. Sekundär angesprochen sind **Administratorinnen und Administratoren**, die die Voraussetzungen in den beiden übergeordneten Apps konfigurieren und den Berechtigungssatz zuweisen.

**Kurzer Prozessüberblick:** Ein freigegebener Fertigungsauftrag wird über das Produktions-Buch.-Blatt mit einer tatsächlichen Menge zurückgemeldet, die von der geplanten Menge abweichen darf. In den Artikelverfolgungszeilen wird die produzierte **Charge** mit ihren Werten in **KG/Meter/Stück** erfasst. Beim Buchen werden die produzierten und die verbleibenden Einheitenwerte auf die Fertigungsauftragszeile zurückgeschrieben. Ist am Fertigungsauftrag das Kennzeichen **Update Herkunftsbeleg** gesetzt, aktualisiert die Verbindungs-App zusätzlich den zugehörigen **Verkaufsauftrag** und – bei Lieferung über Lager – den **Warenausgang**, jeweils inklusive der Einheitenwerte KG/Meter/Stück.

## Schnellstart für Anwender

Der Schnellstart folgt der vom Code erzwungenen Reihenfolge: zuerst die Einrichtung in den übergeordneten Apps, danach die tägliche Rückmeldung.

1. **Voraussetzungen sicherstellen (einmalig, Administration):** In der App **m+m Unit Conversion** sind auf der **Artikelkarte** des Artikels die theoretischen Umrechnungsfaktoren (theoretische KG pro Meter bzw. pro Stück) sowie die Mengenkonsistenzabfrage hinterlegt. In der App **m+m Production Differences** ist die Über-/Unterproduktion eingerichtet. Am **Freigegebenen Fertigungsauftrag** ist bei Bedarf das Kennzeichen **Update Herkunftsbeleg** gesetzt. Näheres unter *Voraussetzungen und Einrichtung*.
2. **Freigegebenen Fertigungsauftrag öffnen** und die betreffende Zeile wählen.
3. Über die Standardaktion das **Produktions-Buch.-Blatt** öffnen.
4. Die tatsächliche Menge als **Ist-Meldung** erfassen; diese darf gemäß den Regeln der Über-/Unterproduktion von der geplanten Menge abweichen.
5. Die **Artikelverfolgungszeilen** öffnen, die **Charge** zuweisen und die Werte **KG**, **Meter** und **Stück** für diese Charge prüfen bzw. erfassen. Das steuernde **Einheitenfeld** (Menge, KG, Meter oder Stück) bestimmt, welche Größe führend ist.
6. Bei Unterproduktion, wenn mit der geringeren Menge abgeschlossen werden soll: das Kennzeichen **Beendet** im Produktions-Buch.-Blatt setzen (ggf. Warnung bestätigen).
7. Das Produktions-Buch.-Blatt **Buchen**. Danach stehen auf der Fertigungsauftragszeile die **Fertig gestellte KG/Meter/Stück** und die **Rest KG/Meter/Stück** korrekt umgerechnet zur Verfügung.
8. Ist **Update Herkunftsbeleg** aktiv, werden **Verkaufsauftrag** (Menge, **Reservierte Menge**, KG/Meter/Stück) und – falls vorhanden – der **Warenausgang** automatisch aktualisiert; hierfür setzt die App im Hintergrund das Kennzeichen **Verknüpftes Dokument aktualisieren**.

## Voraussetzungen und Einrichtung

Diese App besitzt keine eigene Einrichtungsseite. Die gesamte fachliche Konfiguration liegt in den beiden übergeordneten Apps; die Verbindungs-App selbst muss lediglich installiert und über ihren Berechtigungssatz freigegeben werden. Dieses Kapitel beschreibt daher die **Voraussetzungskette**, die eine Administratorin oder ein Administrator in Abhängigkeitsreihenfolge herstellt, damit die automatische Einheitenumrechnung bei Produktionsdifferenzen greift.

### Einheitenumrechnung bei Produktionsdifferenzen einrichten

**Prozessintro:** Diese Konfiguration betrifft die Administration bzw. den Key-User und wird **vor der ersten Rückmeldung** eines betroffenen Artikels vorgenommen. Sie ist die Grundlage dafür, dass die tägliche Arbeit im Produktions-Buch.-Blatt (siehe *Tägliche Arbeit im Produktions-Buch.-Blatt*) korrekte KG/Meter/Stück-Werte liefert und dass der Verkaufsauftrag automatisch mitgezogen wird. Die einzelnen Schritte liegen in den übergeordneten Apps; die Verbindungs-App fügt keinen eigenen konfigurierbaren Schalter hinzu.

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Stammdaten zuerst – Artikelkarte (m+m Unit Conversion):** Zuerst hinterlegen Sie auf der **Artikelkarte** die theoretischen Umrechnungsfaktoren (theoretische KG pro Meter bzw. pro Stück) und die Mengenkonsistenzabfrage. Wenn diese Faktoren gepflegt sind, dann berechnet die Einheitenumrechnung beim Anlegen einer Charge automatisch die zusammengehörigen Werte in KG, Meter und Stück; fehlen die Faktoren, bleibt für den Artikel nur die Basismenge ohne Umrechnung verfügbar. Diese Seite wird über **Suchen** mit dem Begriff der Artikelkarte geöffnet.
2. **Globale Einrichtung – KG Meter Stück Einrichtung (m+m Unit Conversion):** Danach prüfen Sie in der Seite **KG Meter Stück Einrichtung** die unternehmensweiten Einstellungen (Einheitencodes für KG, Meter und Stück, Rundungsregeln). Wenn hier die Einheitencodes korrekt zugeordnet sind, dann werden die Einheitenfelder in Belegen und in der Artikelverfolgung mit den richtigen Maßeinheiten geführt. Diese Seite öffnen Sie über **Suchen** mit dem Begriff „KG Meter Stück Einrichtung“.
3. **Globale und artikelbezogene Einrichtung – Über-/Unterproduktion (m+m Production Differences):** Anschließend legen Sie in der Über-/Unterproduktions-Einrichtung fest, in welchem Rahmen die tatsächliche Menge von der geplanten Menge abweichen darf (Kontrollmethode Vorgabe, Prozentsatz oder absoluter Wert, mit Wert und optionaler Warnung). Wenn eine Warnung zugelassen ist, dann kann die Anwenderin oder der Anwender die Grenze durch Bestätigung überschreiten; ist nur ein Fehler zugelassen, dann wird die abweichende Menge blockiert. Diese Regeln bestimmen, welche Über- oder Unterproduktion im Produktions-Buch.-Blatt überhaupt gebucht werden kann.
4. **Belegbezogenes Kennzeichen – Update Herkunftsbeleg am Fertigungsauftrag (m+m Production Differences):** Setzen Sie am **Freigegebenen Fertigungsauftrag** das Kennzeichen **Update Herkunftsbeleg**, wenn der Ursprungsbeleg mitgezogen werden soll. Wenn dieses Kennzeichen aktiviert ist, dann aktualisiert das System nach der Rückmeldung den zugehörigen **Verkaufsauftrag** (Menge und **Reservierte Menge**) und – über die Verbindungs-App – auch dessen Einheitenwerte KG/Meter/Stück; ist es nicht gesetzt, bleibt der Verkaufsauftrag unverändert und nur der Fertigungsauftrag wird fortgeschrieben.
5. **Berechtigung – diese App (m+m Production Differences with Unit Conversion):** Weisen Sie den mitgelieferten Berechtigungssatz **MuM OPUC Gen. Perm** den betreffenden Benutzergruppen zu. Dieser Berechtigungssatz legt fest, welche Aktionen die Anwenderinnen und Anwender mit den beiden Verarbeitungs-Codeunits der App ausführen dürfen; ohne diese Berechtigung kann die automatische Umrechnung bei der Buchung nicht ausgeführt werden.

**Operativer Abschluss:** Sobald die Schritte 1 bis 5 vorliegen, greift die Verbindungs-App vollautomatisch beim Buchen des Produktions-Buch.-Blatts. Der Anwender löst die Kette durch die normale Rückmeldung aus; siehe *Tägliche Arbeit im Produktions-Buch.-Blatt*.

### Steuerndes Einheitenfeld

Das Verhalten der Umrechnung wird durch das **Einheitenfeld** (technische Bezeichnung des Feldes: **Einheitenfeld modifiziert**) gesteuert. Dieses Feld stammt aus der App m+m Unit Conversion und wird von der Verbindungs-App ausgewertet, um zu entscheiden, welche Größe bei einer Abweichung führend verglichen wird.

| Feld | Erläuterung |
|---|---|
| **Einheitenfeld** | Bestimmt, welche Mengengröße bei der Prüfung und Rückrechnung führend ist. Die zulässigen Werte und ihre Wirkung: **Menge:** Es wird mit der Standardmenge gerechnet; die Zusatzfelder KG/Meter/Stück wirken nicht führend. **KG:** Wenn ausgewählt, wird die produzierte bzw. abzuschließende Menge über die **Fertig gestellte KG** gegen die Charge geprüft und zurückgerechnet. **Meter:** Wenn ausgewählt, ist die **Fertig gestellte Meter** die führende Größe für Prüfung und Rückrechnung. **Stück:** Wenn ausgewählt, ist die **Fertig gestellte Stück** führend. |

### Zusammenspiel der Kennzeichen

Für die Anwenderin oder den Anwender sind diese Kennzeichen normalerweise nicht sichtbar bearbeitbar; sie werden vom System gesetzt und dokumentieren, wie die Umrechnung ablief. Ihre Kenntnis hilft beim Verständnis des Prozesses und bei der Fehlersuche.

| Feld | Erläuterung |
|---|---|
| **Update Herkunftsbeleg** | Kennzeichen am Freigegebenen Fertigungsauftrag (App m+m Production Differences). Wenn gesetzt, dann wird nach der Buchung des Produktions-Buch.-Blatts der verknüpfte Verkaufsauftrag inklusive **Reservierte Menge** und Einheitenwerte aktualisiert; wenn nicht gesetzt, bleibt der Verkaufsauftrag unverändert. |
| **Verknüpftes Dokument aktualisieren** | Technisches Kennzeichen, das diese App auf der **Verkaufszeile** und auf der **Warenausgang**-Zeile setzt. Wenn gesetzt, dann verwendet die Einheitenumrechnung für diese Zeile die aus der Produktion übernommenen tatsächlichen Faktoren (**Tatsächliche KG pro Meter** bzw. **Tatsächliche KG pro Stück**) statt der theoretischen Faktoren der Artikelkarte; dadurch stimmen die Einheitenwerte im Folgebeleg exakt mit der real produzierten Charge überein. Wird es nicht gesetzt, rechnet die Zeile weiterhin mit den theoretischen Faktoren. Dieses Feld wird ausschließlich vom System gesetzt. |
| **Nicht erneut umrechnen** | Kennzeichen aus der App m+m Unit Conversion. Wenn gesetzt, dann übernimmt das System die aus der Produktion ermittelten KG/Meter/Stück unverändert und rechnet sie nicht noch einmal über die theoretischen Faktoren neu; dadurch bleibt die tatsächlich produzierte Menge erhalten. Wenn nicht gesetzt, kann eine erneute automatische Umrechnung erfolgen. |
| **Einheitenfeld modifiziert** | Führt mit, welche Einheitengröße (Menge, KG, Meter oder Stück) bei der letzten Bearbeitung führend war. Wenn gesetzt, dann steuert dieser Wert, welches der Felder Fertig gestellte KG/Meter/Stück bei der Prüfung und Rückrechnung verwendet wird. |

## Tägliche Arbeit im Produktions-Buch.-Blatt

Die tägliche Arbeit findet vollständig auf den Standard- und m+m-Seiten der Produktion statt; diese App wirkt im Hintergrund. Die steuernden Einstellungen liegen in den unter *Voraussetzungen und Einrichtung* beschriebenen Seiten (Artikelkarte, KG Meter Stück Einrichtung, Über-/Unterproduktions-Einrichtung, Kennzeichen **Update Herkunftsbeleg**). Der folgende Ablauf beschreibt, wie die Anwenderin oder der Anwender eine Charge zurückmeldet.

### Rückmeldung mit abweichender Menge

**Einstieg:** Öffnen Sie den **Freigegebenen Fertigungsauftrag**, wählen Sie die Fertigungsauftragszeile und öffnen Sie über die Standardaktion das **Produktions-Buch.-Blatt**.

1. Erfassen Sie die tatsächlich produzierte Menge als **Ist-Meldung**. Über- oder Unterproduktion ist im Rahmen der eingerichteten Regeln zulässig.
2. Öffnen Sie die **Artikelverfolgungszeilen** und weisen Sie die **Charge** zu. Für die Charge werden die Werte **KG**, **Meter** und **Stück** geführt; bei gepflegten theoretischen Faktoren berechnet die Einheitenumrechnung diese Werte automatisch aus der Menge.
3. Ändern Sie bei Bedarf einen der Werte KG, Meter oder Stück. Wenn Sie einen Wert manuell abändern, dann entscheidet die auf der Artikelkarte hinterlegte Mengenkonsistenzabfrage, ob die übrigen Werte automatisch neu berechnet werden. Die Verbindungs-App prüft dabei, dass die zugewiesenen Einheitenwerte zur gemeldeten Menge passen.
4. Verlassen Sie die Artikelverfolgungszeilen. Die App gleicht die produzierten Einheitenwerte gegen die zu bearbeitende Menge ab.

### Fertig- und Teilrückmeldung

Wenn die produzierte Menge unter der geplanten Menge liegt und der Auftrag mit dieser geringeren Menge abgeschlossen werden soll, setzen Sie im Produktions-Buch.-Blatt das Kennzeichen **Beendet**. Liegt die Menge unter der eingerichteten Mindestmenge für Unterproduktion, dann erscheint – sofern die Regel eine Warnung zulässt – eine Warnung, die Sie bestätigen müssen; lehnen Sie ab, kann das Kennzeichen **Beendet** nicht gesetzt werden und die Buchung bleibt eine Teilrückmeldung. Eine Teilrückmeldung ist ausdrücklich zulässig; es ist nicht erforderlich, dass die produzierte Menge der geplanten Menge entspricht.

### Buchen und Rückschreibung

**Buchen** Sie anschließend das Produktions-Buch.-Blatt. Nach der Buchung schreibt die Verbindungs-App die Werte auf die Fertigungsauftragszeile zurück:

- **Fertig gestellte KG / Fertig gestellte Meter / Fertig gestellte Stück** werden um die gerade gebuchten Einheitenwerte erhöht.
- **Rest KG / Rest Meter / Rest Stück** werden als Differenz zwischen der Auftragsmenge und der fertig gestellten Menge in der jeweiligen Einheit fortgeschrieben.
- Das Kennzeichen **Nicht erneut umrechnen** wird gesetzt, damit die real produzierten Werte nicht über die theoretischen Faktoren überschrieben werden.
- Das **Einheitenfeld modifiziert** wird mit der zuletzt führenden Größe (Menge, KG, Meter oder Stück) fortgeschrieben.

So bleibt jederzeit nachvollziehbar, wie viel in KG, Meter und Stück bereits fertig gestellt ist und wie viel je Einheit noch offen ist.

## Verknüpfte Belege: Verkaufsauftrag und Warenausgang

Die Verbindungs-App erweitert zwei Belegtabellen um jeweils ein technisches Kennzeichen, damit die Einheitenwerte aus der Produktion in die Folgebelege übernommen werden. Diese Felder sind nicht zur manuellen Bearbeitung vorgesehen; sie werden ausschließlich vom System gesetzt.

### Verkaufsauftrag

Ist am Fertigungsauftrag **Update Herkunftsbeleg** aktiv, aktualisiert die App nach dem Buchen den verknüpften Verkaufsauftrag. Auf der **Verkaufszeile** werden dabei die Einheitenwerte aus der Produktion übernommen und das Kennzeichen **Verknüpftes Dokument aktualisieren** gesetzt.

| Feld | Erläuterung |
|---|---|
| **Verknüpftes Dokument aktualisieren** (Verkaufszeile) | Wenn gesetzt, dann rechnet die Einheitenumrechnung diese Verkaufszeile mit den tatsächlichen, aus der produzierten Charge stammenden Faktoren (**Tatsächliche KG pro Meter** / **Tatsächliche KG pro Stück**) und nicht mit den theoretischen Faktoren der Artikelkarte; dadurch entsprechen die Werte **KG/Meter/Stück** und **Restauftrag KG/Meter/Stück** auf der Verkaufszeile exakt der real produzierten Menge. Ist es nicht gesetzt, rechnet die Zeile mit den theoretischen Faktoren. Wird automatisch gesetzt. |

Zusätzlich werden auf der Verkaufszeile die aus der Produktion abgeleiteten Einheitenwerte fortgeschrieben (jeweils in KG, Meter und Stück): die aktuellen Mengen sowie die offenen Mengen (**Restauftrag KG/Meter/Stück**). Auch **Menge** und **Reservierte Menge** des Verkaufsauftrags werden entsprechend der gebuchten Produktionsmenge aktualisiert.

### Warenausgang

Wird der Verkaufsauftrag über einen **Warenausgang** geliefert, überträgt die App das Kennzeichen beim Anlegen der Warenausgangszeile.

| Feld | Erläuterung |
|---|---|
| **Verknüpftes Dokument aktualisieren** (Warenausgangszeile) | Wenn gesetzt, dann verwendet die Einheitenumrechnung für diese Warenausgangszeile die tatsächlichen Faktoren der produzierten Charge (**Tatsächliche KG pro Meter** / **Tatsächliche KG pro Stück**); dadurch werden im Warenausgang exakt die real produzierten KG/Meter/Stück ausgewiesen und nicht rechnerisch aus der theoretischen Umrechnung erzeugte Werte. Ist es nicht gesetzt, rechnet die Zeile mit den theoretischen Faktoren. Das Kennzeichen wird beim Erzeugen der Warenausgangszeile automatisch aus der zugehörigen Verkaufszeile übernommen. |

## FAQ und Troubleshooting

### 1. Warum brauche ich diese App zusätzlich zu m+m Production Differences und m+m Unit Conversion?
Beide Apps funktionieren jede für sich. Sobald Sie jedoch bei einem Artikel mit Einheitenumrechnung (KG/Meter/Stück) eine Über- oder Unterproduktion buchen, müssen die Einheitenwerte an die abweichende Menge angepasst und in die Folgebelege übernommen werden. Genau diese Kopplung stellt die Verbindungs-App her; ohne sie blieben die Einheitenwerte bei abweichender Menge unstimmig.

### 2. Wo finde ich die Einrichtungsseite dieser App?
Es gibt keine. Die App bringt keine eigene Seite mit. Die Konfiguration erfolgt in der **Artikelkarte** und der **KG Meter Stück Einrichtung** (m+m Unit Conversion) sowie in der Über-/Unterproduktions-Einrichtung und über **Update Herkunftsbeleg** am Fertigungsauftrag (m+m Production Differences). Siehe *Voraussetzungen und Einrichtung*.

### 3. Was passiert, wenn ich mehr produziere als geplant (Überproduktion)?
Innerhalb der eingerichteten Regeln ist die höhere Menge zulässig; bei Überschreiten der Grenze erscheint je nach Regel eine Warnung oder ein Fehler. Nach dem Buchen werden **Fertig gestellte KG/Meter/Stück** entsprechend erhöht. Ist **Update Herkunftsbeleg** aktiv, werden Menge und **Reservierte Menge** des Verkaufsauftrags über die ursprüngliche Menge hinaus angehoben.

### 4. Was passiert bei Unterproduktion, wenn ich den Auftrag abschließen möchte?
Setzen Sie im Produktions-Buch.-Blatt das Kennzeichen **Beendet**. Liegt die Menge unter der Mindestmenge für Unterproduktion, ist dies nur zulässig, wenn die Regel eine Warnung erlaubt; nach Bestätigung können Sie mit der geringeren Menge buchen. Lehnen Sie ab, bleibt die Buchung eine Teilrückmeldung.

### 5. Welche Größe ist bei der Prüfung führend – Menge, KG, Meter oder Stück?
Das steuert das **Einheitenfeld** (**Menge**, **KG**, **Meter**, **Stück**). Der gewählte Wert legt fest, welches der Felder **Fertig gestellte KG/Meter/Stück** beim Vergleich mit der Charge herangezogen wird.

### 6. Warum stimmen KG/Meter/Stück im Verkaufsauftrag nach der Produktion nicht mit der theoretischen Umrechnung überein?
Weil bei aktivem **Verknüpftes Dokument aktualisieren** die Zeile mit den **tatsächlichen** Faktoren der produzierten Charge rechnet (**Tatsächliche KG pro Meter** / **Tatsächliche KG pro Stück**) und nicht mit den theoretischen Faktoren der Artikelkarte. Das ist gewollt: Der Verkaufsauftrag soll die real produzierten Werte abbilden.

### 7. Warum wird mein Verkaufsauftrag nach dem Buchen der Produktion gar nicht aktualisiert?
Dann ist am Fertigungsauftrag das Kennzeichen **Update Herkunftsbeleg** nicht gesetzt. Ohne dieses Kennzeichen aktualisiert das System nur den Fertigungsauftrag, nicht aber den verknüpften Verkaufsauftrag.

### 8. Kann ich das Feld „Verknüpftes Dokument aktualisieren“ selbst setzen?
Nein. Es ist ein technisches, vom System gesetztes Kennzeichen auf der Verkaufszeile bzw. der Warenausgangszeile. Es dient der Steuerung der Umrechnung und ist nicht zur manuellen Pflege gedacht.

### 9. Warum werden meine manuell geänderten KG-, Meter- oder Stückwerte nicht neu berechnet?
Nach dem Rückschreiben aus der Produktion ist das Kennzeichen **Nicht erneut umrechnen** gesetzt, damit die real produzierten Werte erhalten bleiben. Zusätzlich entscheidet die Mengenkonsistenzabfrage der Artikelkarte, ob und wie manuelle Änderungen die übrigen Einheitenfelder neu berechnen.

### 10. Ich kann die automatische Umrechnung nicht auslösen – woran liegt das?
Prüfen Sie, ob der Berechtigungssatz **MuM OPUC Gen. Perm** zugewiesen ist. Er legt fest, welche Aktionen die Anwenderinnen und Anwender mit den Verarbeitungs-Codeunits der App ausführen dürfen; ohne diese Berechtigung wird die Umrechnung bei der Buchung nicht ausgeführt.

## Typische Anwendungsfälle

Die folgenden Beispiele zeigen den Ablauf in Business Central. Alle beschriebenen Seiten und Felder sind über die beiden übergeordneten Apps und die Verbindungs-App belegt; erfundene Firmen- oder Prüfszenarien werden nicht verwendet.

### Anwendungsfall 1: Unterproduktion einer Charge (Meterware)

**Auslöser:** Aus der Fertigung wird gemeldet, dass für einen Auftrag über Meterware weniger produziert wurde als geplant, und der Auftrag soll mit dieser geringeren Menge abgeschlossen werden.

**Einstieg in BC:** Öffnen Sie den **Freigegebenen Fertigungsauftrag** und wählen Sie die Zeile. Öffnen Sie über die Standardaktion das **Produktions-Buch.-Blatt**.

**Kernablauf:**
1. Erfassen Sie die tatsächlich produzierte Menge als **Ist-Meldung**.
2. Öffnen Sie die **Artikelverfolgungszeilen**, weisen Sie die **Charge** zu und prüfen Sie den Wert **Meter**; das **Einheitenfeld** steht auf **Meter**, sodass die Prüfung über die **Fertig gestellte Meter** erfolgt.
3. Da die Menge unter der geplanten liegt, setzen Sie das Kennzeichen **Beendet**. Erscheint eine Warnung zur Unterproduktion, bestätigen Sie diese.
4. **Buchen** Sie das Produktions-Buch.-Blatt.

**Abschluss:** Auf der Fertigungsauftragszeile stehen nun die **Fertig gestellte Meter** (und die daraus abgeleiteten KG und Stück) sowie die verbleibenden **Rest Meter**. Das Kennzeichen **Nicht erneut umrechnen** ist gesetzt, sodass die real produzierten Werte erhalten bleiben.

### Anwendungsfall 2: Überproduktion mit Aktualisierung des Verkaufsauftrags

**Auslöser:** Für einen kundenbezogenen Auftrag wird mehr produziert als bestellt. Am Fertigungsauftrag ist **Update Herkunftsbeleg** aktiv, damit der Verkauf die tatsächlichen Mengen sieht.

**Einstieg in BC:** Öffnen Sie den **Freigegebenen Fertigungsauftrag** und das zugehörige **Produktions-Buch.-Blatt**.

**Kernablauf:**
1. Erfassen Sie die höhere Menge als **Ist-Meldung**. Bei Überschreiten der Überproduktionsgrenze bestätigen Sie die Warnung, sofern die Regel dies zulässt.
2. Weisen Sie in den **Artikelverfolgungszeilen** die **Charge** mit ihren Werten **KG/Meter/Stück** zu.
3. **Buchen** Sie das Produktions-Buch.-Blatt.

**Abschluss:** Da **Update Herkunftsbeleg** aktiv ist, aktualisiert die Verbindungs-App den **Verkaufsauftrag**: Menge und **Reservierte Menge** werden angehoben, und auf der **Verkaufszeile** werden die Einheitenwerte KG/Meter/Stück sowie **Restauftrag KG/Meter/Stück** aus der Produktion übernommen; das Kennzeichen **Verknüpftes Dokument aktualisieren** wird gesetzt. Wird der Auftrag anschließend über einen **Warenausgang** geliefert, übernimmt die Warenausgangszeile dieses Kennzeichen und weist die tatsächlich produzierten KG/Meter/Stück aus.
