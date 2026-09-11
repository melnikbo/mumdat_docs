---
title: Anwenderhandbuch m+m Goods Receipt with Ext. Production Information
---

# Anwenderhandbuch m+m Goods Receipt with Ext. Production Information

## Einleitung

Die Erweiterung **m+m Goods Receipt with Ext. Production Information** ist eine Verbindungskomponente zwischen der m+m **Warenvereinnahmung** und der m+m Erweiterung für erweiterte Fertigungsinformationen. Sie übernimmt automatisch die **Arbeitsplannr.** aus dem Artikel oder aus der Artikelreferenz auf die Zeile eines Warenannahme-Belegs. Der Anwender muss die Arbeitsplannr. auf der Belegzeile also nicht mehr von Hand nachtragen.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender in der Warenannahme** – also Mitarbeiter, die Wareneingänge erfassen und in der **Warenvereinnahmung** täglich Belegzeilen anlegen. Sekundär betrifft die Erweiterung Administratoren und Stammdatenverantwortliche, die die Arbeitsplannr. an den beiden Datenquellen (Artikelkarte und Artikelreferenz) pflegen sowie die Berechtigungen vergeben.

**Kurzer Prozessüberblick.** Der Anwender erfasst in der **Warenannahme** eine Belegzeile im Zeilenbereich **Fertigmaterial** und trägt dort einen **Artikelnr.** oder eine **Artikelreferenznr.** ein. Sobald dieses Feld geprüft (validiert) wird, ermittelt die Erweiterung im Hintergrund die passende **Arbeitsplannr.** und schreibt sie in die Belegzeile:

1. Ist auf der Zeile eine **Artikelreferenznr.** hinterlegt und trägt die zugehörige **Artikelreferenz** eine Arbeitsplannr., dann wird diese verwendet.
2. Ist keine Artikelreferenznr. hinterlegt (oder die Artikelreferenz führt keine Arbeitsplannr.), dann wird die **Arbeitsplannr.** aus der **Artikelkarte** übernommen.

Die Erweiterung besitzt **keine eigenen Seiten, Aktionen oder Einrichtungsfelder**. Sie wirkt ausschließlich als Automatik auf der bestehenden Warenannahme-Zeile. Alle nachfolgend genannten Seiten und Felder gehören zur **Warenvereinnahmung**, zur Erweiterung für Fertigungsinformationen oder zum Standard von Microsoft Dynamics 365 Business Central; dieses Handbuch beschreibt nur den Ausschnitt, den die Automatik betrifft.

## Schnellstart für Anwender

Der schnellste Weg zum Ergebnis – die automatisch gefüllte **Arbeitsplannr.** auf der Warenannahme-Zeile:

1. **Voraussetzung (einmalig, durch Administrator/Stammdaten):** Hinterlegen Sie an der Datenquelle eine Arbeitsplannr. – entweder auf der **Artikelkarte** im Feld **Arbeitsplannr.** oder auf der **Artikelreferenz** im Feld **Arbeitsplannr.** (siehe *Stammdaten*). Ohne gepflegte Arbeitsplannr. bleibt das Feld auf der Zeile leer.
2. Öffnen Sie die **Warenannahme** über die **Suche** von Business Central (bzw. über **Warenvereinnahmung erstellen**, wenn Sie einen neuen Beleg anlegen).
3. Wechseln Sie in den Zeilenbereich **Fertigmaterial** (Unterseite **Zeilen**) und legen Sie eine Zeile an.
4. Tragen Sie die **Artikelnr.** ein und bestätigen Sie das Feld. Wenn der Artikel eine Arbeitsplannr. führt und keine Artikelreferenznr. gesetzt ist, dann erscheint die **Arbeitsplannr.** sofort in der Zeile.
5. *Optional:* Tragen Sie stattdessen oder zusätzlich eine **Artikelreferenznr.** ein und bestätigen Sie das Feld. Führt die Artikelreferenz eine Arbeitsplannr., dann überschreibt diese die zuvor ermittelte Arbeitsplannr.
6. Prüfen Sie die **Arbeitsplannr.** in der Zeile und bearbeiten Sie den Warenannahme-Beleg wie gewohnt weiter.

> Die Reihenfolge ist bewusst: **Einrichtung/Stammdaten zuerst**, danach die Belegzeile. Ist die Arbeitsplannr. an der Quelle nicht gepflegt, kann die Automatik nichts übernehmen.

## Einrichtung

Die Erweiterung bringt **keine eigene Einrichtungsseite und keine eigenen Einrichtungsfelder** mit. Die Automatik ist nach der Installation ohne Konfiguration aktiv. „Einrichten“ bedeutet für diese Erweiterung daher: die **fachlichen Voraussetzungen** schaffen, damit eine Arbeitsplannr. überhaupt übernommen werden kann, sowie die **Berechtigungen** vergeben.

### Berechtigungen

Die Erweiterung liefert einen zuweisbaren Berechtigungssatz mit, der die Ausführungsrechte für die beiden Automatik-Codeunits bündelt.

| Einrichtung | Erläuterung |
|---|---|
| Berechtigungssatz **MuM GRAP All** | Legt fest, welche Anwender die Automatik der Erweiterung ausführen dürfen. Wenn Sie diesen Berechtigungssatz einem Benutzer oder einer Benutzergruppe zuweisen, dann darf dieser Benutzer die Ausführungslogik der Erweiterung nutzen; die Arbeitsplannr. wird beim Erfassen der Warenannahme-Zeile automatisch übernommen. Ohne diese Berechtigung kann die im Hintergrund laufende Übernahme nicht ausgeführt werden. Der Berechtigungssatz bestimmt ausschließlich die Ausführungsrechte der beiden Automatikbausteine und enthält keine Datenrechte auf Belege oder Stammdaten. |

### Arbeitsplan-Übernahme einrichten

Die automatische Übernahme der Arbeitsplannr. auf die Warenannahme-Zeile ist die einzige fachliche Fähigkeit dieser Erweiterung. Sie wird nicht über einen Schalter aktiviert, sondern durch eine **Kette von Voraussetzungen** über mehrere Bereiche hinweg wirksam. Diese Kette richtet der Administrator bzw. Stammdatenverantwortliche **vor dem ersten produktiven Einsatz** ein.

**Wer richtet ein und wann.** Der Administrator stellt vor dem ersten Wareneingang sicher, dass die abhängigen Module vorhanden sind und die Berechtigungen vergeben wurden. Der Stammdatenverantwortliche pflegt die Arbeitsplannr. an den Artikeln und Artikelreferenzen. Angewendet wird das Ergebnis später vom operativen Anwender in der *Täglichen Arbeit* (siehe dort).

**Einrichtungsschritte in Abhängigkeitsreihenfolge:**

1. **Abhängige Module bereitstellen.** Wenn die Erweiterung installiert ist, dann müssen auch die vorausgesetzten Module **m+m Cloud Base**, **m+m Goods Receipt** (Warenvereinnahmung) und **m+m Ext. Production Information** installiert und lizenziert sein; erst dann existieren die Warenannahme-Zeile mit dem Feld **Arbeitsplannr.** und das Feld **Arbeitsplannr.** auf der Artikelreferenz, auf die die Automatik zugreift. Die Erweiterung prüft die Lizenz beim Anmelden automatisch mit.
2. **Berechtigungen vergeben.** Wenn Sie den Berechtigungssatz **MuM GRAP All** den betroffenen Anwendern zuweisen, dann dürfen diese die Übernahme ausführen (siehe *Berechtigungen*).
3. **Datenquelle pflegen (Stammdaten).** Wenn Sie an der **Artikelkarte** und/oder an der **Artikelreferenz** eine **Arbeitsplannr.** hinterlegen, dann steht der Automatik ein Wert zur Übernahme zur Verfügung (siehe *Stammdaten*). Ohne gepflegte Arbeitsplannr. bleibt die Zeile leer – das ist kein Fehler, sondern das erwartete Verhalten.
4. **Operativer Abschluss der Kette.** Wenn der Anwender in der Warenannahme-Zeile die **Artikelnr.** oder die **Artikelreferenznr.** bestätigt, dann übernimmt die Automatik die passende Arbeitsplannr. in das Feld **Arbeitsplannr.** der Zeile (siehe *Tägliche Arbeit*).

Damit greift die Kette ineinander: Modul- und Berechtigungsvoraussetzung → gepflegte Stammdaten → Aktion des Anwenders auf der Belegzeile.

## Stammdaten

Die Arbeitsplannr., die auf die Warenannahme-Zeile übernommen wird, stammt aus **einer von zwei** Stammdatenquellen. Beide werden vom Stammdatenverantwortlichen gepflegt, bevor die Warenannahme-Zeilen erfasst werden. Die Automatik wertet sie mit klarer Priorität aus: **Artikelreferenz vor Artikel.**

### Arbeitsplannr. auf der Artikelkarte

**Prozess.** Der Stammdatenverantwortliche hinterlegt je Fertigungsartikel den Standard-Arbeitsplan auf der **Artikelkarte**. Dieser Wert dient als **Fallback**: Er wird übernommen, wenn die Zeile keine Artikelreferenznr. trägt oder die Artikelreferenz keinen eigenen Arbeitsplan führt. Angewendet wird der Wert in der *Täglichen Arbeit* beim Bestätigen der Artikelnr.

**Einstieg:** Öffnen Sie über die **Suche** die Artikelübersicht, öffnen Sie die **Artikelkarte** des betreffenden Artikels und pflegen Sie das Feld **Arbeitsplannr.**

| Feld | Erläuterung |
|---|---|
| **Arbeitsplannr.** (Artikelkarte) | Wenn Sie hier einen Arbeitsplan hinterlegen, dann wird genau diese Arbeitsplannr. auf die Warenannahme-Zeile übernommen, sobald der Anwender die Artikelnr. bestätigt und keine (arbeitsplanführende) Artikelreferenznr. auf der Zeile steht. Ist das Feld leer, dann bleibt die Arbeitsplannr. auf der Zeile leer und muss – falls benötigt – manuell erfasst werden. |

### Arbeitsplannr. auf der Artikelreferenz

**Prozess.** Für kundenspezifische Fälle pflegt der Stammdatenverantwortliche die **Arbeitsplannr.** direkt auf der **Artikelreferenz** (Feld aus der Erweiterung für Fertigungsinformationen). Dieser Wert hat **Vorrang** vor dem Arbeitsplan der Artikelkarte. Angewendet wird er in der *Täglichen Arbeit* beim Bestätigen der Artikelreferenznr.

**Einstieg:** Öffnen Sie die **Artikelkarte**, rufen Sie die zugehörigen **Artikelreferenzen** auf und pflegen Sie dort das Feld **Arbeitsplannr.**

| Feld | Erläuterung |
|---|---|
| **Arbeitsplannr.** (Artikelreferenz) | Wenn Sie auf einer Artikelreferenz einen Arbeitsplan hinterlegen, dann übernimmt die Automatik diese Arbeitsplannr. bevorzugt auf die Warenannahme-Zeile, sobald der Anwender die passende Artikelreferenznr. bestätigt. Der Standard-Arbeitsplan der Artikelkarte wird in diesem Fall nicht herangezogen. Ist das Feld leer, dann fällt die Automatik auf den Arbeitsplan der Artikelkarte zurück. |
| **Referenzart** (Voraussetzung) | Die Arbeitsplannr. lässt sich auf der Artikelreferenz nur pflegen, **wenn** die **Referenzart** den Wert **Debitor** hat. Wenn Sie versuchen, die Arbeitsplannr. bei einer anderen Referenzart zu erfassen, dann verhindert Business Central die Eingabe mit einer Feldprüfung. Praktisch bedeutet das: kundenspezifische Arbeitspläne über die Artikelreferenz sind ausschließlich für **debitorenbezogene** Referenzen vorgesehen. |

> **Prioritätsregel (wichtig für die Pflege):** Trägt sowohl die Artikelreferenz als auch die Artikelkarte einen Arbeitsplan, dann gewinnt die **Artikelreferenz**. Pflegen Sie die Artikelkarte als allgemeinen Standard und die Artikelreferenz nur dort, wo ein Debitor einen abweichenden Arbeitsplan benötigt.

## Tägliche Arbeit an der Warenannahme-Zeile

Die tägliche Arbeit findet im Beleg der **Warenannahme** statt. Der für diese Erweiterung relevante Bereich ist der Zeilenbereich **Fertigmaterial** (Unterseite **Zeilen**). Dieser Abschnitt wird durch die Stammdaten aus dem vorigen Kapitel gesteuert: die **Arbeitsplannr.** auf der **Artikelkarte** und auf der **Artikelreferenz** bestimmen, welcher Wert automatisch in die Zeile geschrieben wird. Legen Sie diese Stammdaten daher vor der Belegerfassung an (Querverweis: *Stammdaten*, *Arbeitsplan-Übernahme einrichten*).

**Einstieg:** Öffnen Sie die **Warenannahme** über die **Suche** bzw. über **Warenvereinnahmung erstellen** und wechseln Sie in den Zeilenbereich **Fertigmaterial**.

Auf der Zeile sind für die Automatik die folgenden Felder maßgeblich (weitere Spalten der Warenannahme-Zeile gehören zur Warenvereinnahmung und sind dort beschrieben):

| Feld | Erläuterung |
|---|---|
| **Artikelnr.** | Wenn Sie die Artikelnr. eintragen und bestätigen und die Zeile führt **keine** Artikelreferenznr., dann übernimmt die Automatik die **Arbeitsplannr.** aus der Artikelkarte dieses Artikels (sofern dort gepflegt). Führt der Artikel keinen Arbeitsplan, dann bleibt das Feld leer. |
| **Artikelreferenznr.** | Wenn Sie eine Artikelreferenznr. eintragen und bestätigen und die zugehörige Artikelreferenz führt eine **Arbeitsplannr.**, dann wird diese bevorzugt in die Zeile übernommen. Führt die Artikelreferenz keinen Arbeitsplan, dann greift die Automatik ersatzweise auf die Arbeitsplannr. der Artikelkarte zurück. |
| **Arbeitsplannr.** | Zielfeld der Automatik. Wenn eine der beiden Quellen einen Arbeitsplan liefert, dann steht die Arbeitsplannr. nach dem Bestätigen ohne weitere Eingabe in der Zeile. Der Wert wird über die reguläre Feldprüfung gesetzt, sodass abhängige Prüfungen der Zeile ausgelöst werden. Sie können den Wert bei Bedarf manuell überschreiben. |
| **Beschreibung**, **Menge**, **Einheitencode**, **Lagerortcode** | Übliche Zeilenfelder der Warenannahme (kein Einfluss der Automatik). Sie erfassen sie wie gewohnt; sie werden hier nur als Kontext der Zeile genannt. |

**Ablauf der Automatik (aus dem Code abgeleitet):**

1. Sie bestätigen auf der Zeile die **Artikelnr.** → ist keine Artikelreferenznr. gesetzt, wird die **Arbeitsplannr.** aus der Artikelkarte übernommen (nur wenn dort nicht leer).
2. Sie bestätigen auf der Zeile die **Artikelreferenznr.** → führt die Artikelreferenz eine **Arbeitsplannr.**, wird diese übernommen; andernfalls wird die Arbeitsplannr. der Artikelkarte übernommen.

Die Erweiterung stellt **keine eigenen Schaltflächen** bereit; es gibt keine gesonderte Aktion zum Auslösen der Übernahme. Sie geschieht allein durch die Feldbestätigung.

## Typische Anwendungsfälle

Die folgenden Abläufe zeigen die zwei realistischen Auslöser für die Automatik. Alle genannten Felder und Seiten sind über den Code der Erweiterung und die abhängigen Module belegt.

### Anwendungsfall 1 – Arbeitsplan aus dem Artikel

**Auslöser.** Im Wareneingang trifft Fertigmaterial ein, für das ein Standard-Arbeitsplan am Artikel hinterlegt ist; eine kundenspezifische Referenz ist nicht im Spiel.

**Einstieg in BC.** Der Anwender öffnet die **Warenannahme** über die **Suche** und wechselt in den Zeilenbereich **Fertigmaterial**.

**Kernablauf.**
1. Der Anwender legt eine Zeile an und trägt die **Artikelnr.** ein.
2. Beim Bestätigen prüft die Automatik: keine **Artikelreferenznr.** gesetzt → sie liest die **Arbeitsplannr.** aus der **Artikelkarte**.
3. Ist dort ein Arbeitsplan hinterlegt, dann erscheint die **Arbeitsplannr.** sofort in der Zeile.

**Abschluss.** Der Anwender vervollständigt die Zeile (Menge, Lagerortcode) und bearbeitet den Warenannahme-Beleg im gewohnten Prozess weiter. Eine manuelle Erfassung der Arbeitsplannr. entfällt.

### Anwendungsfall 2 – Arbeitsplan aus der Artikelreferenz (debitorenspezifisch)

**Auslöser.** Für einen bestimmten Debitor gilt ein abweichender Arbeitsplan. Dieser ist als **Arbeitsplannr.** auf der **Artikelreferenz** (Referenzart **Debitor**) hinterlegt.

**Einstieg in BC.** Der Anwender öffnet die **Warenannahme** über die **Suche** und wechselt in den Zeilenbereich **Fertigmaterial**.

**Kernablauf.**
1. Der Anwender trägt auf der Zeile die **Artikelreferenznr.** ein und bestätigt sie.
2. Die Automatik liest die **Arbeitsplannr.** von der Artikelreferenz und schreibt sie in die Zeile – **vorrangig** vor einem etwaigen Arbeitsplan der Artikelkarte.
3. Führt die Artikelreferenz ausnahmsweise keinen Arbeitsplan, dann übernimmt die Automatik ersatzweise die **Arbeitsplannr.** aus der Artikelkarte.

**Abschluss.** Der Anwender prüft die übernommene **Arbeitsplannr.** und setzt die Belegbearbeitung fort. So erhält der debitorenspezifische Wareneingang automatisch den richtigen Arbeitsplan.

## FAQ und Troubleshooting

### 1. Warum erscheint die Arbeitsplannr. automatisch auf meiner Warenannahme-Zeile?
Weil die Erweiterung beim Bestätigen der **Artikelnr.** oder der **Artikelreferenznr.** die passende **Arbeitsplannr.** aus dem Artikel bzw. der Artikelreferenz übernimmt. Das ist der gesamte Zweck der Erweiterung.

### 2. Woher stammt die übernommene Arbeitsplannr. – vom Artikel oder von der Artikelreferenz?
Trägt die Zeile eine **Artikelreferenznr.** und führt diese Referenz einen Arbeitsplan, dann stammt der Wert von der **Artikelreferenz**. Andernfalls stammt er aus der **Arbeitsplannr.** der **Artikelkarte**.

### 3. Was passiert, wenn sowohl der Artikel als auch die Artikelreferenz einen Arbeitsplan haben?
Dann gewinnt die **Artikelreferenz**. Ihr Arbeitsplan wird bevorzugt übernommen; der Arbeitsplan der Artikelkarte wird in diesem Fall nicht verwendet.

### 4. Warum bleibt das Feld Arbeitsplannr. auf der Zeile leer?
Weil an keiner der beiden Quellen ein Arbeitsplan gepflegt ist: Die **Artikelkarte** führt keine **Arbeitsplannr.**, und es ist keine (arbeitsplanführende) **Artikelreferenznr.** gesetzt. Pflegen Sie die Arbeitsplannr. an der gewünschten Quelle, dann wird sie beim nächsten Bestätigen übernommen.

### 5. Warum kann ich die Arbeitsplannr. auf der Artikelreferenz nicht speichern?
Weil die **Referenzart** nicht **Debitor** ist. Die Arbeitsplannr. auf der Artikelreferenz ist nur für debitorenbezogene Referenzen vorgesehen; bei anderer Referenzart verhindert eine Feldprüfung die Eingabe.

### 6. Muss ich eine Schaltfläche drücken, damit die Arbeitsplannr. übernommen wird?
Nein. Es gibt **keine** eigene Aktion. Die Übernahme läuft automatisch beim Bestätigen der **Artikelnr.** bzw. der **Artikelreferenznr.** auf der Zeile.

### 7. Was passiert, wenn ich die Artikelnr. ändere, nachdem eine Artikelreferenznr. gesetzt ist?
Solange eine **Artikelreferenznr.** auf der Zeile steht, übernimmt die Automatik beim Bestätigen der Artikelnr. **nicht** den Arbeitsplan der Artikelkarte. Der Weg über die Artikelkarte greift nur, wenn keine Artikelreferenznr. gesetzt ist.

### 8. Kann ich die automatisch gesetzte Arbeitsplannr. überschreiben?
Ja. Die Arbeitsplannr. ist ein reguläres Feld der Warenannahme-Zeile. Sie können den übernommenen Wert manuell ändern; die Erweiterung setzt ihn nur zum Zeitpunkt der Feldbestätigung.

### 9. Warum werde ich beim Anmelden auf eine Lizenz geprüft?
Die Erweiterung führt beim Anmelden eine **Lizenzprüfung** über das m+m Zahlungsmodul durch. Ist die Lizenz gültig, dann bemerken Sie davon nichts; die Prüfung stellt sicher, dass die Automatik ausgeführt werden darf.

### 10. Ich habe die Arbeitsplannr. am Artikel gepflegt, trotzdem bleibt die Zeile leer – woran liegt das?
Prüfen Sie drei Punkte: (a) Steht auf der Zeile eine **Artikelreferenznr.** ohne eigenen Arbeitsplan? Dann sollte der Artikel-Arbeitsplan greifen – ist die Artikelkarte wirklich befüllt? (b) Wurde die **Artikelnr.** nach dem Pflegen erneut **bestätigt**? Die Übernahme geschieht nur bei der Feldbestätigung. (c) Besitzt der Anwender den Berechtigungssatz **MuM GRAP All**? Ohne Ausführungsrecht kann die Automatik nicht laufen.
