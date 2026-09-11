---
title: Anwenderhandbuch m+m Product Configurator with Item Charge Management
---

# Anwenderhandbuch m+m Product Configurator with Item Charge Management

## Einleitung

Dieses Modul ist eine **Brücke** zwischen zwei m+m-Erweiterungen: dem **Produktkonfigurator** und dem **Zu-/Abschlagsmanagement**. Es sorgt dafür, dass ein Artikel, der über den **Produktkonfigurator** konfiguriert wird und dabei mit dem Kennzeichen **Zu-/Abschläge erzeugen** versehen ist, im Verkaufs- oder Einkaufsbeleg **automatisch** eine passende **Zu-/Abschlag (Artikel)**-Zeile erhält. Das Modul selbst besitzt keine eigenen Seiten oder Einrichtungsfelder; es verbindet ausschließlich die vorhandenen Funktionen der beiden Basismodule miteinander.

**Zielgruppe:** Primär richtet sich dieses Handbuch an **operative Anwender**, die täglich mit Verkaufsaufträgen und Einkaufsbestellungen arbeiten — Vertriebsinnendienst und Einkaufssachbearbeitung, die konfigurierte Artikel erfassen, Belege **freigeben** und **buchen**. Sekundär angesprochen sind **Administratoren** und **Key-User**, die die notwendige Einrichtung im Zu-/Abschlagsmanagement und im Produktkonfigurator vornehmen.

**Kurzer Prozessüberblick:** Der Anwender erfasst eine Artikelzeile in einem Beleg und ruft den **Produktkonfigurator** auf. Setzt die Konfiguration das Kennzeichen **Zu-/Abschläge erzeugen** auf der Zeile, erkennt das Zu-/Abschlagsmanagement die Zeile bei jeder Änderung als geändert und legt — gesteuert durch dieses Modul — automatisch die zugehörige **Zu-/Abschlag (Artikel)**-Zeile an oder legt sie neu an. Spätestens bei der **Freigabe** des Belegs ist die Zeile vorhanden; beim **Zurücksetzen des Status** wird sie wieder entfernt. Die Höhe und Verteilung des Zu-/Abschlags richten sich nach der Einrichtung des jeweiligen **Artikel Zu-/Abschlags**.

## Schnellstart für Anwender

Der schnellste Weg von der Konfiguration bis zum gebuchten Beleg mit automatischem Zu-/Abschlag. Die Einrichtung (siehe Kapitel **Einrichtung**) muss einmalig durch einen Administrator erfolgen, bevor Sie diesen Ablauf nutzen können.

1. **Einrichtung sicherstellen (einmalig, Voraussetzung):** Im **Artikel Zu-/Abschlag** ist die **Bezugsgröße** gesetzt und **Automatisch in Beleg übernehmen** auf **Ja** oder **Bei Freigabe** eingestellt; der zugehörige Produktkonfigurator-Eintrag setzt das Kennzeichen **Zu-/Abschläge erzeugen**.
2. **Beleg anlegen:** Legen Sie einen **Verkaufsauftrag** (oder eine **Einkaufsbestellung**) an und erfassen Sie eine Artikelzeile vom Typ Artikel.
3. **Konfigurieren:** Öffnen Sie über die Aktion **Produktkonfigurator** in der Belegzeile die Konfiguration und schließen Sie diese ab. Dadurch wird auf der Zeile das Kennzeichen **Zu-/Abschläge erzeugen** gesetzt.
4. **Automatische Zeile prüfen:** Nach dem Speichern der Zeile erzeugt das System automatisch eine Zeile vom Typ **Zu-/Abschlag (Artikel)** im selben Beleg. Prüfen Sie Menge und Betrag.
5. **Freigeben:** Geben Sie den Beleg über **Freigeben** frei. Ist **Automatisch in Beleg übernehmen** auf **Bei Freigabe** gesetzt, entsteht die **Zu-/Abschlag (Artikel)**-Zeile spätestens jetzt.
6. **Buchen:** Buchen Sie den Beleg über **Buchen**. Die Mengenverteilung der Zu-/Abschlagszeile folgt den Feldern **Menge/Pauschal zu liefern (VK)** bzw. **Bezugsgröße Beleg zu liefern (VK)** aus der Einrichtung.
7. **Bei Bedarf korrigieren:** Über **Status zurücksetzen** öffnen Sie den Beleg erneut; die automatisch erzeugte **Zu-/Abschlag (Artikel)**-Zeile wird dabei entfernt und bei erneuter Freigabe mit den aktuellen Einrichtungswerten neu angelegt.

## Einrichtung

Dieses Brückenmodul besitzt **keine eigene Einrichtungsseite**. Damit der automatische Ablauf funktioniert, müssen die Einstellungen in den beiden Basismodulen zusammenpassen. Dieses Kapitel beschreibt die Einrichtung **in Abhängigkeitsreihenfolge**: zuerst die globale Grundeinrichtung, dann der einzelne **Artikel Zu-/Abschlag** als Stammsatz, schließlich das auslösende Kennzeichen aus dem Produktkonfigurator.

### Artikel Zu-/Abschlagseinrichtung (globale Grundeinrichtung)

**Prozesseinstieg:** Diese Einrichtung ist eine **unternehmensweite Grundeinrichtung** (ein Datensatz je Mandant). Sie öffnen die Seite **Artikel Zu-/Abschlagseinrichtung** über **Suchen**. Sie wird einmalig durch den Administrator vor der ersten Nutzung gepflegt und legt das Standardverhalten für die Berechnung der Zu-/Abschläge bei Lieferung fest. Die konkreten Zu-/Abschläge selbst pflegen Sie anschließend als Stammdaten (siehe **Stammdaten**).

| Einrichtung | Erläuterung |
|---|---|
| Bezugsgröße (Berechnung) | Wenn hier eine Bezugsgröße hinterlegt ist, bestimmt sie, worauf sich die Standardberechnung des Zu-/Abschlags bezieht; ohne Vorgabe verhält sich das System wie der Business-Central-Standard. |
| Menge/Pauschal zu liefern (VK) | Wenn gesetzt, legt der Wert für den **Verkauf** fest, zu welchem Lieferzeitpunkt der Zu-/Abschlag mengenmäßig übernommen wird. **(leer)/Standard:** BC-Standardverhalten. **Erste Lieferung (komplett):** Der Zu-/Abschlag wird bei der ersten Lieferung berechnet. **Letzte Lieferung (komplett):** Er wird erst bei der letzten Lieferung berechnet, wenn die Restmenge 0 ist. **Jede Lieferung:** Je gelieferten Anteil wird der entsprechende Anteil des Zu-/Abschlags berechnet. |
| Bezugsgröße Beleg zu liefern (VK) | Wenn gesetzt, steuert der Wert im **Verkauf** die belegbezogene Berechnung. **(leer)/Standard:** BC-Standard. **Erste Lieferung:** Berechnung bei der ersten Lieferung, abhängig vom Beleg. **Letzte Lieferung:** Berechnung bei der letzten Lieferung, wenn die Restmenge 0 ist. |
| Menge/Pauschal zu liefern (EK) | Wie **Menge/Pauschal zu liefern (VK)**, jedoch für den **Einkauf**; steuert den Lieferzeitpunkt der Zu-/Abschlagsberechnung in Einkaufsbelegen mit denselben Werten. |
| Bezugsgröße Beleg zu liefern (EK) | Wie **Bezugsgröße Beleg zu liefern (VK)**, jedoch für den **Einkauf**. |

> Diese Grundeinrichtung gehört fachlich zum Zu-/Abschlagsmanagement und wird von diesem Brückenmodul nur vorausgesetzt. Die einzelnen Zeitpunktwerte werden je **Artikel Zu-/Abschlag** feiner eingestellt (siehe unten).

### Automatische Zu-/Abschläge aus der Konfiguration einrichten

Damit ein konfigurierter Artikel im Beleg automatisch einen Zu-/Abschlag erhält, ist eine mehrstufige Einrichtung über mehrere Seiten notwendig. Dieses Brückenmodul verbindet die letzten beiden Stufen automatisch.

**Prozessintro:** Diese Kette richtet der Administrator gemeinsam mit dem Key-User **vor der ersten Nutzung** ein. Sie wird im Tagesgeschäft durch die Aktion **Produktkonfigurator** in der Belegzeile ausgelöst (siehe **Tägliche Arbeit im Beleg**).

**Einrichtungsschritte in Abhängigkeitsreihenfolge:**

1. **Artikel Zu-/Abschlag als Stammsatz anlegen** (Seite **Artikel Zu-/Abschläge**): Legen Sie den Zu-/Abschlag mit **Nr.**, **Beschreibung** und **Produktbuchungsgruppe** an. Wenn diese Felder gefüllt sind, kann der Zu-/Abschlag in Belegen verwendet und korrekt auf das passende Sachkonto gebucht werden.
2. **Bezugsgröße festlegen:** Setzen Sie die **Bezugsgröße** des Zu-/Abschlags. Wenn hier z. B. **Menge** gewählt ist, wird der Zu-/Abschlag zeilen- und mengenbezogen berechnet; bei **Beleg** bezieht er sich auf sämtliche Zeilen des Belegs.
3. **Übernahme steuern:** Setzen Sie **Automatisch in Beleg übernehmen** auf **Ja** (sofortige automatische Zeile bei Anlage) oder **Bei Freigabe** (Zeile entsteht bei Belegfreigabe). Wenn **Ja** gewählt wird, darf die **Bezugsgröße** nicht **Beleg** sein — diese Kombination wird vom System mit einer Fehlermeldung verhindert.
4. **Auswählbarkeit setzen (optional):** Aktivieren Sie **In Belegzeile auswählbar**, wenn der Anwender den Zu-/Abschlag zusätzlich manuell in der Belegzeile auswählen können soll. Wenn aktiviert, erscheint der Zu-/Abschlag in der manuellen Auswahl der Belegzeile.
5. **Kennzeichen im Produktkonfigurator hinterlegen:** Sorgen Sie dafür, dass die Konfiguration des betreffenden Artikels das Kennzeichen **Zu-/Abschläge erzeugen** auf der Belegzeile setzt. Wenn dieses Kennzeichen gesetzt ist, behandelt das Zu-/Abschlagsmanagement die Zeile bei jeder Änderung als geändert und legt die **Zu-/Abschlag (Artikel)**-Zeile automatisch an — genau dies ist die Aufgabe dieses Brückenmoduls.

**Operativer Abschluss:** Im Tagesgeschäft ruft der Anwender die Aktion **Produktkonfigurator** in der Belegzeile auf; anschließend entsteht die Zu-/Abschlagszeile automatisch (siehe **Tägliche Arbeit im Beleg** und **Typische Anwendungsfälle**).

## Stammdaten

### Artikel Zu-/Abschläge (Stammdaten) pflegen

**Prozessintro:** Der **Artikel Zu-/Abschlag** ist der zentrale Stammsatz, aus dem die automatisch erzeugte Belegzeile ihre Werte bezieht. Er wird durch den Administrator/Key-User gepflegt und über **Suchen** geöffnet (Liste **Artikel Zu-/Abschläge** → Karte). Die hier gepflegten Werte fließen im Tagesgeschäft in jede automatisch generierte **Zu-/Abschlag (Artikel)**-Zeile ein (siehe **Tägliche Arbeit im Beleg**).

| Feld | Erläuterung |
|---|---|
| Nr. | Wenn gefüllt, identifiziert die Nummer den Artikel Zu-/Abschlag gemäß der festgelegten Nummernserie; sie wird auf der automatisch erzeugten Belegzeile als Artikelzuschlag verwendet. |
| Beschreibung | Wenn gefüllt, erscheint dieser Text als Zeilenbeschreibung des Zu-/Abschlags im Beleg; so erkennt der Anwender den Zweck der automatisch angelegten Zeile. |
| Produktbuchungsgruppe | Wenn gesetzt, verknüpft die Produktbuchungsgruppe den Zu-/Abschlag beim Buchen mit dem passenden Sachkonto gemäß Buchungsmatrix-Einrichtung; ohne sie kann der Zu-/Abschlag nicht korrekt gebucht werden. |
| Einheitencode | Wenn gesetzt, bestimmt der Einheitencode die Einheit des Zu-/Abschlags auf Basis der Einheitentabelle. |
| Bezugsgröße | Wenn gesetzt, steuert die Bezugsgröße, wie der Zu-/Abschlag berechnet wird. **(leer)/Standard:** BC-Standard. **Pauschal Teilweise:** zeilenbezogen mit Menge 1. **Beleg:** bezogen auf sämtliche Zeilen des Belegs mit Menge 1. **Menge:** zeilenbezogen, Menge = Menge der Artikelzeile. **Pauschal Gesamt:** pauschaler Gesamtbetrag über den Beleg. |
| In Belegzeile auswählbar | Wenn aktiviert, kann der Anwender den Zu-/Abschlag manuell in der Belegzeile auswählen bzw. übersteuern; das Kennzeichen dient zugleich als Filtermarkierung für die vorgefilterte Auswahl. |
| Automatisch in Beleg übernehmen | Wenn gesetzt, legt der Wert fest, wann die Zu-/Abschlagszeile automatisch entsteht. **(leer):** BC-Standardverhalten ohne automatische Anlage. **Ja:** Bei Anlage einer Artikelzeile wird der Zu-/Abschlag automatisch als nächste Zeile erzeugt. **Manuell:** Der Anwender kann zu jeder Verkaufs-/Einkaufszeile eine Zu-/Abschlagszeile manuell hinzufügen. **Bei Freigabe:** Wird der Beleg freigegeben, legt das System die Zu-/Abschlagszeile automatisch an. Für den automatischen Ablauf dieses Brückenmoduls sind **Ja** oder **Bei Freigabe** relevant. |
| Berechnungszeitpunkt | Wenn gesetzt, bestimmt der Berechnungszeitpunkt, welches Datum die Preisfindung bei Rechnungserstellung heranzieht: **Arbeitsdatum**, **Buchungsdatum**, **Auftrags-/Bestelldatum** oder **Lieferdatum**. |
| Bezugsgröße Beleg zu liefern (VK) | Wenn gesetzt, steuert der Wert im Verkauf, zu welchem Lieferzeitpunkt der belegbezogene Zu-/Abschlag berechnet wird: **(leer)/Standard**, **Erste Lieferung**, **Letzte Lieferung** (Restmenge 0). |
| Menge/Pauschal zu liefern (VK) | Wenn gesetzt, steuert der Wert im Verkauf den mengenbezogenen Lieferzeitpunkt: **(leer)/Standard**, **Erste Lieferung (komplett)**, **Letzte Lieferung (komplett)**, **Jede Lieferung**. |
| Bezugsgröße Beleg zu liefern (EK) | Wie **Bezugsgröße Beleg zu liefern (VK)**, jedoch für den Einkauf. |
| Menge/Pauschal zu liefern (EK) | Wie **Menge/Pauschal zu liefern (VK)**, jedoch für den Einkauf. |

> Der **Berechnungszeitpunkt** ist besonders in dem vom zugehörigen Prozess beschriebenen Fall relevant, in dem der Verkaufspreis erst in der Rechnung über die Kalkulation gesetzt wird: Dann liefert das gewählte Datum die Grundlage für die Zu-/Abschlagsberechnung bei Rechnungserstellung.

### Zu-/Abschlagszuweisung

**Prozessintro:** Die **Zu-/Abschlagszuweisung** verknüpft einen Zu-/Abschlag mit den Belegzeilen, auf die er sich bezieht. Sie wird im Zu-/Abschlagsmanagement gepflegt und ist die Grundlage dafür, dass die automatisch erzeugte **Zu-/Abschlag (Artikel)**-Zeile korrekt auf die Artikelzeile verweist. Für den automatischen Ablauf dieses Brückenmoduls muss der Anwender die Zuweisung in der Regel nicht manuell bearbeiten — sie entsteht zusammen mit der automatischen Zeile. Über die Aktion **Zu-/Abschlagszuweisungen** in der Belegzeile kann der Anwender die Zuweisung bei Bedarf einsehen und anpassen.

## Tägliche Arbeit im Beleg (Verkauf und Einkauf)

Dieses Kapitel beschreibt, wie das Brückenmodul im Beleg wirkt. Die steuernden Einstellungen liegen auf den Seiten **Artikel Zu-/Abschläge** und **Artikel Zu-/Abschlagseinrichtung** (siehe **Einrichtung**) sowie in der Konfiguration des **Produktkonfigurators**; dort legt der Administrator fest, welche Bezugsgröße gilt, ob die Übernahme automatisch oder bei Freigabe erfolgt und welcher Artikel das Kennzeichen **Zu-/Abschläge erzeugen** setzt.

### Konfiguration in der Belegzeile

**Einstieg:** Öffnen Sie in der Verkaufs- bzw. Einkaufsbelegzeile über die Aktion **Produktkonfigurator** die Konfiguration. Nach Abschluss der Konfiguration trägt das System auf der Zeile das Kennzeichen **Zu-/Abschläge erzeugen** ein.

| Feld/Aktion | Erläuterung |
|---|---|
| Produktkonfigurator (Aktion) | Wenn aufgerufen, öffnet sich die Konfigurationsmaske zur Zeile; nach Abschluss werden die Konfigurationswerte und — abhängig von der Konfiguration — das Kennzeichen **Zu-/Abschläge erzeugen** auf die Zeile geschrieben. |
| Zu-/Abschläge erzeugen | Wenn auf der Zeile gesetzt, behandelt das Zu-/Abschlagsmanagement die Zeile bei jeder Änderung als geändert und legt automatisch die zugehörige **Zu-/Abschlag (Artikel)**-Zeile an bzw. neu an; ist das Kennzeichen nicht gesetzt, bleibt die Zeile eine normale Artikelzeile ohne automatischen Zu-/Abschlag. |

### Automatische Zu-/Abschlagszeile

Sobald das Kennzeichen **Zu-/Abschläge erzeugen** gesetzt ist, greift die Brücke:

- Bei jeder Änderung der Belegzeile prüft das Zu-/Abschlagsmanagement auf Unterschiede. Dieses Modul meldet die Zeile in diesem Fall stets als geändert, damit die **Zu-/Abschlag (Artikel)**-Zeile korrekt neu bewertet wird.
- Wird beim Speichern keine bestehende automatische Zeile gelöscht, stößt das Modul die (Neu-)Anlage der **Zu-/Abschlag (Artikel)**-Zeile mit **Automatisch in Beleg übernehmen = Ja** an. So erhält eine Zeile, deren Betrag zwischenzeitlich wieder unter den Mindestwert gefallen war, ihren Zu-/Abschlag ohne Dubletten erneut.
- Die neue Zeile übernimmt Bezugsgröße, Übernahmezeitpunkt und die Liefermengen-Steuerung aus dem hinterlegten **Artikel Zu-/Abschlag**.

### Freigeben, Buchen und Status zurücksetzen

1. **Freigeben:** Über **Freigeben** geben Sie den Beleg frei. Ist im Artikel Zu-/Abschlag **Automatisch in Beleg übernehmen = Bei Freigabe** gesetzt, entsteht die **Zu-/Abschlag (Artikel)**-Zeile spätestens jetzt.
2. **Buchen:** Über **Buchen** buchen Sie den Beleg. Die Mengen der Zu-/Abschlagszeile werden anhand von **Menge/Pauschal zu liefern (VK)** bzw. **Bezugsgröße Beleg zu liefern (VK)** (im Einkauf entsprechend die EK-Felder) verteilt.
3. **Status zurücksetzen:** Über **Status zurücksetzen** öffnen Sie den Beleg erneut. Die automatisch erzeugte **Zu-/Abschlag (Artikel)**-Zeile wird entfernt; bei erneuter Freigabe wird sie mit den dann aktuellen Einrichtungswerten neu angelegt.

## Berechtigungen

Das Modul liefert den Berechtigungssatz **MuM PKCM All** aus. Er ist zuweisbar und bestimmt die Berechtigungen für die Ausführung des Brücken-Codeunits dieses Moduls. Weisen Sie diesen Berechtigungssatz allen Anwendern zu, die mit konfigurierten Artikeln und automatischen Zu-/Abschlägen in Verkaufs- und Einkaufsbelegen arbeiten. Er legt fest, dass die automatische Erzeugung der Zu-/Abschlagszeilen für diese Anwender ausgeführt werden darf; die Berechtigungen für die eigentlichen Zu-/Abschlags- und Belegdaten werden über die Berechtigungssätze der Basismodule gesteuert.

Beim Anmelden führt das Modul zusätzlich eine **Lizenzprüfung** aus. Wenn die Lizenz für diese Erweiterung nicht gültig ist, steht die automatische Zu-/Abschlagserzeugung nicht zur Verfügung; wenden Sie sich in diesem Fall an Ihren Administrator.

## Typische Anwendungsfälle

### Anwendungsfall 1 — Konfigurierter Verkaufsauftrag mit automatischem Zu-/Abschlag

1. **Auslöser:** Ein Kunde ruft an und bestellt einen konfigurierbaren Artikel; der Vertriebsinnendienst legt dazu einen Verkaufsauftrag an.
2. **Einstieg in BC:** Der Anwender legt den **Verkaufsauftrag** an, erfasst die Artikelzeile und öffnet über die Aktion **Produktkonfigurator** die Konfiguration.
3. **Kernablauf:** Nach Abschluss der Konfiguration trägt das System das Kennzeichen **Zu-/Abschläge erzeugen** auf der Zeile ein. Beim Speichern legt das Zu-/Abschlagsmanagement — gesteuert durch dieses Modul — automatisch eine Zeile vom Typ **Zu-/Abschlag (Artikel)** an. Der Anwender gibt den Auftrag über **Freigeben** frei; die Zu-/Abschlagszeile wird gemäß Einrichtung berücksichtigt.
4. **Abschluss:** Der Anwender bucht den Auftrag über **Buchen**. Muss er die Konfiguration nachträglich ändern, setzt er den Status über **Status zurücksetzen** zurück, passt die Zeile an und gibt erneut frei; die Zu-/Abschlagszeile wird mit den aktuellen Werten neu erzeugt.

### Anwendungsfall 2 — Einkaufsbestellung mit automatischem Zu-/Abschlag

1. **Auslöser:** Für einen konfigurierten Artikel fallen beim Lieferanten zusätzliche Kosten (z. B. Fracht) an, die als Zu-/Abschlag in der Bestellung abgebildet werden sollen.
2. **Einstieg in BC:** Der Einkauf legt eine **Einkaufsbestellung** für den Kreditor an und erfasst die Artikelzeile.
3. **Kernablauf:** Über die Aktion **Produktkonfigurator** wird die Zeile konfiguriert und das Kennzeichen **Zu-/Abschläge erzeugen** gesetzt. Beim Speichern bzw. spätestens bei **Freigeben** legt das System automatisch eine **Zu-/Abschlag (Artikel)**-Zeile an. Wurden zwischenzeitlich die Rahmenbedingungen des Zu-/Abschlags geändert, wird bei Löschung und Neuanlage die aktuelle Einrichtung angewendet.
4. **Abschluss:** Die Bestellung wird über **Buchen** gebucht. Über **Status zurücksetzen** kann der Anwender die automatische Zu-/Abschlagszeile entfernen und nach Anpassung erneut erzeugen lassen.

## FAQ und Troubleshooting

### 1. Wozu dient dieses Modul überhaupt?
Es verbindet den **Produktkonfigurator** mit dem **Zu-/Abschlagsmanagement**: Trägt eine Konfiguration das Kennzeichen **Zu-/Abschläge erzeugen** auf der Belegzeile ein, sorgt dieses Modul dafür, dass automatisch die passende **Zu-/Abschlag (Artikel)**-Zeile im Beleg entsteht.

### 2. Wo stelle ich ein, dass ein Artikel automatisch einen Zu-/Abschlag erhält?
In drei Schritten: Legen Sie den **Artikel Zu-/Abschlag** an, setzen Sie dort **Bezugsgröße** und **Automatisch in Beleg übernehmen** (**Ja** oder **Bei Freigabe**), und sorgen Sie dafür, dass die Konfiguration des Artikels das Kennzeichen **Zu-/Abschläge erzeugen** setzt.

### 3. Warum entsteht keine automatische Zu-/Abschlagszeile?
Prüfen Sie, ob auf der Belegzeile das Kennzeichen **Zu-/Abschläge erzeugen** gesetzt ist. Ist es nicht gesetzt, behandelt das System die Zeile als normale Artikelzeile und legt keinen Zu-/Abschlag an. Prüfen Sie zusätzlich, ob **Automatisch in Beleg übernehmen** im Artikel Zu-/Abschlag auf **Ja** oder **Bei Freigabe** steht.

### 4. Warum erhalte ich eine Fehlermeldung, wenn ich „Automatisch in Beleg übernehmen“ auf „Ja“ setze?
Die Kombination **Automatisch in Beleg übernehmen = Ja** mit **Bezugsgröße = Beleg** ist nicht zulässig und wird vom System mit einer Fehlermeldung verhindert. Wählen Sie für die automatische Übernahme eine andere Bezugsgröße (z. B. **Menge** oder **Pauschal Teilweise**).

### 5. Was bedeutet „Bei Freigabe“ gegenüber „Ja“?
Bei **Ja** entsteht die Zu-/Abschlagszeile bereits bei Anlage der Artikelzeile. Bei **Bei Freigabe** entsteht sie erst, wenn der Beleg über **Freigeben** freigegeben wird. In beiden Fällen berücksichtigt das System die hinterlegten Parameter.

### 6. Warum verschwindet die Zu-/Abschlagszeile, wenn ich den Beleg zurücksetze?
Beim **Status zurücksetzen** entfernt das System die automatisch erzeugte **Zu-/Abschlag (Artikel)**-Zeile. Bei erneuter Freigabe wird sie mit den dann gültigen Einrichtungswerten neu angelegt — so werden zwischenzeitliche Änderungen der Rahmenbedingungen berücksichtigt.

### 7. Ich habe die Menge der Artikelzeile geändert — wird der Zu-/Abschlag neu berechnet?
Ja. Bei jeder relevanten Änderung der Zeile meldet dieses Modul die Zeile als geändert, sodass das Zu-/Abschlagsmanagement die zugehörige Zu-/Abschlagszeile neu bewertet und bei Bedarf neu anlegt.

### 8. Entstehen doppelte Zu-/Abschlagszeilen, wenn ich die Zeile mehrfach ändere?
Nein. Das Modul legt die Zeile nur dann neu an, wenn keine automatisch erzeugte Zu-/Abschlagszeile mehr vorhanden ist. Existiert bereits eine, wird keine Dublette erzeugt.

### 9. Kann ich einen Zu-/Abschlag auch manuell hinzufügen?
Ja. Setzen Sie im Artikel Zu-/Abschlag **Automatisch in Beleg übernehmen = Manuell** und aktivieren Sie **In Belegzeile auswählbar**. Dann kann der Anwender den Zu-/Abschlag über die Belegzeile manuell auswählen und hinzufügen.

### 10. Warum funktioniert die automatische Erzeugung gar nicht, obwohl alles eingerichtet ist?
Das Modul führt beim Anmelden eine **Lizenzprüfung** durch. Ist die Lizenz für diese Erweiterung nicht gültig, wird die automatische Zu-/Abschlagserzeugung nicht ausgeführt. Prüfen Sie außerdem, ob der Berechtigungssatz **MuM PKCM All** zugewiesen ist, und wenden Sie sich bei Lizenzfragen an Ihren Administrator.
