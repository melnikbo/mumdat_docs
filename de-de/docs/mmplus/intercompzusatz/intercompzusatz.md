---
title: Anwenderhandbuch m+m Ext. Production Information with Intercompany
---

# Anwenderhandbuch m+m Ext. Production Information with Intercompany

## Einleitung

Die Erweiterung **m+m Ext. Production Information with Intercompany** verbindet die Materialverfolgung aus der Fertigungsinformation mit dem mandantenübergreifenden Belegaustausch von **m+m Intercompany**. Sie sorgt dafür, dass die einem Einkaufsbeleg zugeordneten Chargen- und Serieninformationen (die **Materialverfolgungsposten**) beim automatischen Erzeugen eines Verkaufsauftrags im Partnermandanten mit übertragen werden. Zusätzlich ermöglicht sie dem Einkäufer, eine **Charge** direkt aus den Beständen des **IC-Partners** auszuwählen.

**Zielgruppe:** Primär sind das **operativ tätige Anwenderinnen und Anwender im Einkauf**, die Einkaufsbestellungen mit Intercompany-Bezug bearbeiten und dabei die Materialverfolgung pflegen. Sekundär betrifft die Erweiterung Anwender im **Verkauf** des Partnermandanten, in dessen Verkaufsauftrag die übertragenen Materialverfolgungsposten erscheinen, sowie Administratorinnen und Administratoren, die den Intercompany-Belegaustausch einrichten.

**Kurzer Prozessüberblick:** In einer **Einkaufsbestellung**, die für den Intercompany-Versand vorgesehen ist, öffnet der Anwender aus der Artikelzeile heraus die **Materialverfolgungsposten**. Ist der Beleg für den IC-Versand markiert (**IC-Beleg senden**) und befindet er sich im **IC-Status** **Neu**, kann der Anwender über die Aktion **Charge von IC-Partner auswählen** eine Charge aus dem Partnermandanten zuordnen. Erstellt der Intercompany-Prozess anschließend im Partnermandanten den zugehörigen **Verkaufsauftrag**, werden die erfassten Materialverfolgungsposten automatisch in die passende **Verkaufszeile** kopiert. So bleibt die Chargen- und Serienzuordnung über beide Mandanten hinweg konsistent, ohne dass sie doppelt erfasst werden muss.

Diese Erweiterung liefert **keine** eigenen Einrichtungsseiten, Stammdaten oder Berichte. Sie ergänzt bestehende Belege um zwei Aktionen und um eine automatische, im Hintergrund laufende Übertragung. Die notwendigen Grundeinstellungen stammen aus den zugrunde liegenden Modulen **m+m Intercompany** und **m+m Ext. Production Information**.

## Schnellstart für Anwender

Der schnelle Weg von der Einkaufsbestellung bis zur mandantenübergreifend konsistenten Materialverfolgung:

1. **Voraussetzungen prüfen (einmalig, durch die Administration):** Der **IC-Partner** ist in **m+m Intercompany** eingerichtet, und der Belegaustausch ist aktiv. Siehe Abschnitt **Voraussetzungen und Einrichtung**.
2. **Einkaufsbestellung öffnen:** Öffnen Sie die betreffende **Einkaufsbestellung** und stellen Sie sicher, dass der Kopf für den Intercompany-Versand vorgesehen ist (**IC-Beleg senden** aktiviert) und den **IC-Status** **Neu** hat.
3. **Artikelzeile wählen:** Markieren Sie in den **Zeilen** die gewünschte **Einkaufszeile** vom Typ Artikel.
4. **Materialverfolgungsposten öffnen:** Wählen Sie in den Zeilenaktionen **Materialverfolgungsposten**. Die Seite ist bearbeitbar, solange der Beleg im **IC-Status** **Neu** ist.
5. **Charge vom IC-Partner auswählen:** Wählen Sie auf der Seite **Materialverfolgungsposten** die Aktion **Charge von IC-Partner auswählen** und ordnen Sie im folgenden Auswahldialog die **Charge** (und ggf. **Seriennr.**) bis zur offenen Menge der Zeile zu.
6. **Intercompany-Prozess ausführen (durch m+m Intercompany):** Sobald der Intercompany-Prozess im Partnermandanten den **Verkaufsauftrag** erzeugt, werden die zugeordneten **Materialverfolgungsposten** automatisch in die passende **Verkaufszeile** kopiert — es ist kein weiterer Erfassungsschritt nötig.

Es gibt in dieser Erweiterung **keine** Buchungs-, Freigabe- oder Beenden-Aktion. Der einzige aktiv ausgelöste Schritt ist die Chargenzuweisung (Schritt 5); die Übertragung in den Partnermandanten (Schritt 6) läuft automatisch.

## Voraussetzungen und Einrichtung

Diese Erweiterung besitzt **keine eigene Einrichtungsseite**. Die Funktion wird ausschließlich über bereits vorhandene Kennzeichen der Basis- und Abhängigkeitsmodule aktiviert. Die folgende Übersicht beschreibt formal, welche Vorbedingungen erfüllt sein müssen, damit die beiden Aktionen zur Verfügung stehen und die automatische Übertragung greift.

### Voraussetzungen für die Chargenauswahl vom IC-Partner einrichten

**Prozessintro:** Diese Vorbereitung führt die **Administration** bzw. der Key-User **vor der ersten Nutzung** durch. Sie legt fest, unter welchen Bedingungen ein Anwender im Einkauf eine **Charge** aus dem **IC-Partner** zuordnen darf und wann die zugeordneten Posten in den Partner-**Verkaufsauftrag** übernommen werden. Angewendet wird die Einstellung später im Abschnitt **Materialverfolgungsposten am Einkaufsbeleg**.

Führen Sie die Schritte in Abhängigkeitsreihenfolge aus:

1. **IC-Partner im Modul m+m Intercompany einrichten.** Zuerst richten Sie den **IC-Partner** und den Intercompany-Belegaustausch im Modul **m+m Intercompany** ein. Wenn der IC-Partner samt Postausgangs-/Posteingangsangaben hinterlegt ist, dann kann die Erweiterung den zugehörigen Partnermandanten ermitteln und beim Anlegen des Verkaufsauftrags auf dessen Daten zugreifen. Ohne eingerichteten IC-Partner findet keine Übertragung statt.
2. **Einkaufsbestellung für den IC-Versand kennzeichnen (IC-Beleg senden).** Setzen Sie im Kopf der **Einkaufsbestellung** das Kennzeichen **IC-Beleg senden**. Wenn **IC-Beleg senden** aktiviert ist, dann wird die Aktion **Charge von IC-Partner auswählen** auf der Seite **Materialverfolgungsposten** freigeschaltet; ist das Kennzeichen nicht gesetzt, bleibt die Aktion deaktiviert, weil ohne IC-Versand keine Partner-Charge zugeordnet werden kann.
3. **IC-Status Neu beibehalten.** Achten Sie darauf, dass der Beleg den **IC-Status** **Neu** hat, während die Materialverfolgung gepflegt wird. Wenn der **IC-Status** **Neu** ist, dann ist die Seite **Materialverfolgungsposten** bearbeitbar und Zuordnungen sind möglich; verlässt der Beleg diesen Status, wird die Seite schreibgeschützt, damit bereits übertragene oder in Verarbeitung befindliche Zuordnungen nicht nachträglich verändert werden.
4. **Operativer Abschluss im Tagesablauf.** Die Kette endet mit der Anwenderaktion **Charge von IC-Partner auswählen** in den **Materialverfolgungsposten** (siehe Abschnitt **Materialverfolgungsposten am Einkaufsbeleg**). Die anschließende Übernahme in den Partner-Verkaufsauftrag erfolgt automatisch (siehe **Intercompany-Übertragung der Materialverfolgung**).

Diese eine Konfigurationskette steuert beide Fähigkeiten der Erweiterung — die manuelle Chargenauswahl und die automatische Übertragung. Beide beruhen auf demselben eingerichteten IC-Partner und demselben IC-Beleg; eine getrennte zweite Einrichtung ist nicht erforderlich.

### Berechtigungen

**Prozessintro:** Die Administration ordnet den Anwendern **vor der ersten Nutzung** das Berechtigungsset der Erweiterung zu, damit die hinterlegte Logik ausgeführt werden darf.

Das Berechtigungsset **MuM INAP Permission** bestimmt die Ausführungsberechtigungen für die Programmlogik der Erweiterung. Es legt fest, welche Aktionen die Anwender im Zusammenhang mit der Intercompany-Materialverfolgung ausführen können, indem es die Ausführung der beiden zugehörigen Codeunits gestattet. Wenn einem Benutzer dieses Set zugewiesen ist, dann kann er die Aktion **Charge von IC-Partner auswählen** nutzen, und die automatische Übertragung in den Partnermandanten wird für seine Vorgänge ausgeführt; ohne dieses Set steht die Logik der Erweiterung nicht zur Verfügung.

## Materialverfolgungsposten am Einkaufsbeleg

**Steuernde Einstellungen:** Dieser transaktionale Bereich wird durch Kennzeichen im Kopf der **Einkaufsbestellung** gesteuert, die in **m+m Intercompany** gepflegt werden: **IC-Beleg senden** (schaltet die Chargenauswahl frei) und **IC-Status** (steuert die Bearbeitbarkeit). Wie diese Kennzeichen gesetzt werden, beschreibt der Abschnitt **Voraussetzungen für die Chargenauswahl vom IC-Partner einrichten**.

Die Erweiterung fügt der **Einkaufszeile** einer **Einkaufsbestellung** eine Aktion hinzu, mit der die Materialverfolgungsposten der Zeile geöffnet werden. Von dort erfolgt die Chargenzuordnung aus dem Partnermandanten.

### Materialverfolgungsposten öffnen

**Einstieg:** Öffnen Sie die **Einkaufsbestellung** → markieren Sie in den **Zeilen** die gewünschte **Einkaufszeile** → wählen Sie die Aktion **Materialverfolgungsposten**.

Die Aktion **Materialverfolgungsposten** steht in den Zeilenaktionen der Einkaufszeile zur Verfügung, wenn die Zeile eine Artikelzeile mit einem gültigen IC-Partner-Artikelbezug ist (gemeinsame Artikelnr., Artikel, Artikelreferenz oder Lieferanten-Artikelnr.). Beim Öffnen prüft die Erweiterung, dass die Zeile vom Typ Artikel ist. Die geöffnete Seite ist **bearbeitbar**, wenn der Belegkopf den **IC-Status** **Neu** trägt; andernfalls wird sie nur zur Ansicht geöffnet.

Die Seite **Materialverfolgungsposten** zeigt je Zuordnung die folgenden Informationen:

| Feld | Erläuterung |
|---|---|
| **Lfd. Nr.** | Fortlaufende Nummer des Materialverfolgungspostens. Wenn ein neuer Posten angelegt wird, dann vergibt das System die Nummer automatisch; sie dient der eindeutigen Identifikation der einzelnen Chargen-/Serienzuordnung. |
| **Herkunftsart** | Art des Belegs, aus dem der Posten stammt. Wenn die Materialverfolgung aus einer Einkaufszeile geöffnet wurde, dann steht hier die Einkaufszeile als Herkunft; nach der Übertragung in den Partnermandanten verweist der Zielposten entsprechend auf die Verkaufszeile. |
| **Herkunftsnr.** | Belegnummer der Herkunft (Nummer der Einkaufsbestellung bzw. des Verkaufsauftrags). Wenn dieser Wert gesetzt ist, dann ordnet er den Posten eindeutig dem konkreten Beleg zu. |
| **Herkunftszeilennr.** | Zeilennummer innerhalb des Herkunftsbelegs. Wenn dieser Wert gesetzt ist, dann verknüpft er den Posten mit genau der Beleg­zeile, für die die Charge erfasst wurde. |
| **Artikelnr.** | Artikel, für den die Charge zugeordnet wird. Wenn eine Zuordnung erfolgt, dann übernimmt der Posten die Artikelnr. der Einkaufszeile, sodass die Verfolgung eindeutig dem richtigen Artikel gilt. |
| **Variantencode** | Variante des Artikels. Wenn der Artikel mit Varianten geführt wird, dann stellt dieses Feld sicher, dass die Charge der zutreffenden Variante zugeordnet und nicht mit einer anderen Variante verwechselt wird. |
| **Chargennr.** | Zugeordnete Charge aus dem IC-Partner. Wenn hier eine Chargennr. eingetragen ist, dann ist damit festgelegt, welche Partner-Charge die Zeile beliefert; dieser Wert wird bei der Intercompany-Übertragung in den Verkaufsauftrag übernommen. |
| **Seriennr.** | Zugeordnete Seriennummer, falls der Artikel seriennummernpflichtig ist. Wenn eine Seriennr. gesetzt ist, dann wird die Verfolgung auf Einzelstückebene geführt und ebenfalls mit übertragen. |
| **Menge** | Der Charge bzw. Serie zugeordnete Menge. Wenn eine Menge erfasst wird, dann verringert sich die noch offene, zuzuordnende Menge der Zeile entsprechend; die Summe der Zuordnungen darf die offene Menge der Einkaufszeile nicht überschreiten. |
| **Lagerortcode** | Lagerort, auf den sich die Zuordnung bezieht. Wenn ein Lagerortcode gesetzt ist, dann grenzt er die Chargenzuordnung auf den betreffenden Lagerort ein, damit Bestände korrekt unterschieden werden. |

### Charge von IC-Partner auswählen

**Einstieg:** Wählen Sie auf der geöffneten Seite **Materialverfolgungsposten** die Aktion **Charge von IC-Partner auswählen**.

Die Aktion **Charge von IC-Partner auswählen** ist nur aktiv, wenn der zugrunde liegende Einkaufsbeleg das Kennzeichen **IC-Beleg senden** trägt. Wenn die Aktion ausgeführt wird, dann öffnet die Erweiterung den Chargen-Auswahldialog der Artikelverfolgung und bietet die noch offene Menge der Einkaufszeile zur Zuordnung an. Die angebotene Restmenge ergibt sich aus der offenen Menge der Zeile abzüglich der bereits zugeordneten Menge.

Ablauf der Zuordnung:

1. Die Erweiterung ermittelt die offene, noch nicht zugeordnete Menge der **Einkaufszeile**.
2. Sie öffnet den Auswahldialog für die **Charge** (bei seriennummernpflichtigen Artikeln zusätzlich für die **Seriennr.**).
3. Der Anwender wählt die gewünschte **Charge** aus dem Partnerbestand aus.
4. Bricht der Anwender ohne Auswahl ab (weder **Charge** noch **Seriennr.** gesetzt), dann wird kein Posten angelegt.
5. Ist die gewählte **Charge** für dieselbe Herkunft, denselben Artikel, dieselbe Variante und denselben Lagerort bereits vorhanden, dann erscheint die Meldung **„Die Charge %1 ist bereits zugewiesen"**, und es wird kein doppelter Posten angelegt.
6. Andernfalls legt die Erweiterung einen neuen **Materialverfolgungsposten** mit der gewählten **Chargennr.**, der **Menge** und den zugehörigen Herkunfts-, Artikel-, Varianten- und Lagerortangaben an.

Diese Prüfung stellt sicher, dass jede Partner-Charge je Zeile und Lagerort nur einmal erfasst wird und die zugeordnete Gesamtmenge die offene Menge der Bestellung nicht übersteigt.

## Intercompany-Übertragung der Materialverfolgung

**Steuernde Einstellungen:** Die Übertragung setzt einen in **m+m Intercompany** eingerichteten **IC-Partner** und einen für den IC-Versand vorgesehenen Einkaufsbeleg voraus (siehe **Voraussetzungen für die Chargenauswahl vom IC-Partner einrichten**).

Dieser Vorgang läuft **automatisch** und erfordert keine gesonderte Anwenderaktion. Er greift in dem Moment, in dem der Intercompany-Prozess im Partnermandanten aus der Einkaufsbestellung heraus die zugehörigen **Verkaufszeilen** erzeugt.

Ablauf:

1. Der Intercompany-Prozess von **m+m Intercompany** erzeugt im Partnermandanten den **Verkaufsauftrag** und dessen **Verkaufszeilen**.
2. Die Erweiterung erkennt dieses Ereignis und ermittelt über die **Externe Belegnummer** des Verkaufsauftrags sowie die Zeilennummer die passende **Einkaufszeile** im Quellmandanten.
3. Sie liest im Quellmandanten alle **Materialverfolgungsposten** der Einkaufszeile.
4. Für jeden gefundenen Posten legt sie im Partnermandanten einen entsprechenden Posten an und verweist ihn auf die neue **Verkaufszeile** (**Herkunftsart** Verkaufszeile, mit **Herkunftsnr.** und **Herkunftszeilennr.** des Verkaufsauftrags).

Die Übertragung wird nur für Belege des Typs Auftrag ausgeführt und nur, wenn im Quellmandanten eine passende Einkaufszeile ermittelt werden kann. Findet sich keine passende Einkaufszeile oder ist die Belegnummer leer, dann wird kein Posten kopiert. So erscheinen die im Einkauf erfassten Chargen- und Seriendaten ohne erneute Erfassung im Verkaufsauftrag des Partnermandanten.

## Typische Anwendungsfälle

### Anwendungsfall 1: Charge des Lieferanten für eine Intercompany-Bestellung zuordnen

**Auslöser:** Ein Einkäufer erhält vom liefernden Partnermandanten die Angabe, aus welcher **Charge** ein bestellter Artikel stammt, und soll diese Information am Beleg festhalten.

**Einstieg in BC:** Der Einkäufer öffnet die betreffende **Einkaufsbestellung**. Der Belegkopf ist für den Intercompany-Versand vorgesehen (**IC-Beleg senden** aktiviert) und steht im **IC-Status** **Neu**. In den **Zeilen** markiert er die Artikelzeile und wählt die Aktion **Materialverfolgungsposten**.

**Kernablauf:** Auf der bearbeitbaren Seite **Materialverfolgungsposten** wählt der Einkäufer die Aktion **Charge von IC-Partner auswählen**. Im Auswahldialog ordnet er die vom Partner genannte **Charge** mit der zu belegenden **Menge** bis zur offenen Menge der Zeile zu. Versucht er, dieselbe Charge für dieselbe Zeile ein zweites Mal zu erfassen, weist ihn die Meldung **„Die Charge %1 ist bereits zugewiesen"** darauf hin. Nach erfolgreicher Auswahl erscheint ein neuer **Materialverfolgungsposten** mit **Chargennr.**, **Artikelnr.**, **Menge** und **Lagerortcode**.

**Abschluss:** Der Posten bleibt bearbeitbar, solange der Beleg den **IC-Status** **Neu** hat. Weitere Buchungs- oder Freigabeschritte sind in dieser Erweiterung nicht erforderlich.

### Anwendungsfall 2: Chargeninformation gelangt automatisch in den Partner-Verkaufsauftrag

**Auslöser:** Nachdem die Einkaufsseite die Materialverfolgung gepflegt hat, stößt die Sachbearbeitung den Intercompany-Prozess an, um im liefernden Mandanten den passenden **Verkaufsauftrag** zu erzeugen.

**Einstieg in BC:** Der Vorgang benötigt keine manuelle Navigation in dieser Erweiterung. Sobald **m+m Intercompany** im Partnermandanten den **Verkaufsauftrag** und die **Verkaufszeilen** anlegt, wird die Übertragung ausgelöst.

**Kernablauf:** Die Erweiterung ordnet die neu erzeugte **Verkaufszeile** über die **Externe Belegnummer** und die Zeilennummer der ursprünglichen **Einkaufszeile** zu und kopiert deren **Materialverfolgungsposten** in den Partnermandanten. Die Zielposten verweisen mit **Herkunftsart**, **Herkunftsnr.** und **Herkunftszeilennr.** auf den neuen Verkaufsauftrag.

**Abschluss:** Im Partnermandanten kann die Verkaufssachbearbeitung die übernommenen **Materialverfolgungsposten** an der **Verkaufszeile** einsehen. Chargen und Seriennummern sind damit über beide Mandanten hinweg konsistent, ohne dass sie erneut erfasst werden mussten.

## FAQ und Troubleshooting

### 1. Warum ist die Aktion „Charge von IC-Partner auswählen" ausgegraut?
Die Aktion ist nur aktiv, wenn der Kopf der Einkaufsbestellung das Kennzeichen **IC-Beleg senden** trägt. Ist der Beleg nicht für den Intercompany-Versand vorgesehen, bleibt die Aktion deaktiviert. Setzen Sie das Kennzeichen im Belegkopf, damit die Chargenauswahl freigeschaltet wird.

### 2. Warum kann ich die Materialverfolgungsposten nicht bearbeiten?
Die Seite **Materialverfolgungsposten** ist nur bearbeitbar, wenn der Beleg den **IC-Status** **Neu** hat. Sobald der Beleg diesen Status verlassen hat, wird die Seite schreibgeschützt geöffnet, damit bereits übertragene Zuordnungen nicht nachträglich verändert werden.

### 3. Was bedeutet die Meldung „Die Charge %1 ist bereits zugewiesen"?
Für dieselbe Herkunft (Einkaufszeile), denselben Artikel, dieselbe Variante und denselben Lagerort ist die gewählte **Chargennr.** bereits als Materialverfolgungsposten erfasst. Es wird kein doppelter Posten angelegt. Wählen Sie eine andere Charge oder korrigieren Sie den vorhandenen Posten.

### 4. Warum wird beim Öffnen der Materialverfolgungsposten geprüft, ob die Zeile ein Artikel ist?
Die Materialverfolgung bezieht sich immer auf einen Artikel mit Chargen- oder Seriennummernführung. Handelt es sich nicht um eine Artikelzeile, kann keine Charge zugeordnet werden, und die Aktion bricht mit einem Hinweis auf den erforderlichen Zeilentyp ab.

### 5. Wie viel Menge kann ich einer Charge zuordnen?
Angeboten wird die noch **offene Menge** der Einkaufszeile abzüglich der bereits zugeordneten **Menge**. Die Summe aller Zuordnungen kann damit die offene Menge der Zeile nicht überschreiten. Teilmengen sind zulässig; Sie können mehrere Chargen bis zur vollständigen Belegung der Zeile erfassen.

### 6. Muss ich die Charge im Verkaufsauftrag des Partnermandanten erneut erfassen?
Nein. Sobald der Intercompany-Prozess den **Verkaufsauftrag** im Partnermandanten anlegt, werden die im Einkauf erfassten **Materialverfolgungsposten** automatisch in die passende **Verkaufszeile** kopiert. Eine erneute Erfassung ist nicht nötig.

### 7. Warum sind im Verkaufsauftrag keine Materialverfolgungsposten angekommen?
Die Übertragung findet nur statt, wenn im Quellmandanten eine passende **Einkaufszeile** ermittelt werden kann. Die Zuordnung erfolgt über die **Externe Belegnummer** des Verkaufsauftrags und die Zeilennummer. Fehlt die externe Belegnummer oder existiert keine passende Einkaufszeile, werden keine Posten kopiert.

### 8. Für welche Belegart wird die Übertragung ausgeführt?
Die automatische Übertragung greift für Belege des Typs Auftrag. Bei anderen Belegarten wird der Vorgang nicht ausgeführt, sodass keine unerwarteten Posten entstehen.

### 9. Muss ich nach der Chargenzuweisung buchen oder freigeben?
Nein. Diese Erweiterung enthält keine Buchungs-, Freigabe- oder Beenden-Aktion. Der einzige aktive Schritt ist die Zuordnung der **Charge**; die Übernahme in den Partnermandanten läuft automatisch.

### 10. Welche Berechtigung benötige ich für die Funktion?
Sie benötigen das Berechtigungsset **MuM INAP Permission**. Es bestimmt die Ausführungsberechtigungen für die Programmlogik der Erweiterung und legt fest, welche Aktionen Sie im Zusammenhang mit der Intercompany-Materialverfolgung ausführen können. Ohne dieses Set steht die Funktion nicht zur Verfügung.
