---
title: Anwenderhandbuch m+m Semifinished Items with Routing Status Overview
---

# Anwenderhandbuch m+m Semifinished Items with Routing Status Overview

## Einleitung

Die App **m+m Semifinished Items with Routing Status Overview** verbindet zwei bestehende m+m-Erweiterungen in Microsoft Dynamics 365 Business Central: die **Arbeitsgangstatusanzeige** (Modul *m+m Routing Status Overview*) und die Halbfertigartikel-Verarbeitung (Modul *m+m Semifinished Items*). Die App fügt selbst keine eigenen Seiten, Einrichtungsmasken oder Stammdaten hinzu. Ihre gesamte Wirkung entfaltet sich in einer bereits vorhandenen Ansicht: der **Arbeitsgangstatusanzeige** im **Verkaufsauftrag**.

Ohne diese App zeigt die Arbeitsgangstatusanzeige nur die Arbeitsgänge des unmittelbar zum Verkaufsauftrag gehörenden **Fertigungsauftrags**. Enthält ein Fertigungsauftrag jedoch **Halbfertigartikel** – also Fertigungsauftragszeilen, die aus vorgelagerten Bearbeitungsschritten an einem als Halbfertigartikel gekennzeichneten **Arbeitsplatz** entstehen –, dann fehlen deren Arbeitsgänge in der Standardanzeige. Genau diese Lücke schließt die App: Sie ergänzt die Arbeitsgänge der Halbfertigartikel-Zeilen in der grafischen Ansicht **und** in der Listenansicht, sodass der Anwender den Fortschritt des gesamten Fertigungsprozesses – Hauptartikel und alle Halbfertigstufen – an einer Stelle im Verkaufsauftrag verfolgen kann.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender**, die täglich mit Verkaufsaufträgen und der zugehörigen Fertigung arbeiten: Innendienst, Auftragssachbearbeitung, Fertigungssteuerung und Vertrieb. Sie nutzen die Arbeitsgangstatusanzeige, um Kunden Auskunft über den Fertigungsfortschritt zu geben und die eigene Terminplanung abzustimmen. Sekundär betrifft die App **Administratoren**, die die Voraussetzungen (installierte Abhängigkeiten, Lizenz, als Halbfertigartikel gekennzeichnete Arbeitsplätze) einmalig sicherstellen.

### Kurzer Prozessüberblick

1. Der Anwender legt einen **Verkaufsauftrag** an und erzeugt daraus einen **Fertigungsauftrag**.
2. Enthält der Fertigungsauftrag Arbeitsgänge an einem Halbfertigartikel-Arbeitsplatz, entstehen beim Aufteilen zusätzliche Fertigungsauftragszeilen für die **Halbfertigartikel** (Modul *m+m Semifinished Items*).
3. Im Verkaufsauftrag zeigt die **Arbeitsgangstatusanzeige** den Status aller Arbeitsgänge. Durch diese App erscheinen dort auch die Arbeitsgänge der Halbfertigartikel-Zeilen – eingerückt als zusätzliche **Ebene** in der Listenansicht und als weitere Kacheln in der grafischen Ansicht.
4. Der Anwender liest Status, Mengen und Termine ab und springt bei Bedarf per Klick in den **FA-Arbeitsplan** oder in den **Fertigungsauftrag**.

## Schnellstart für Anwender

Die App benötigt keine eigene Einrichtung. Sobald die Voraussetzungen erfüllt sind (siehe **Voraussetzungen und Berechtigungen**), ist der schnellste Weg zum Ergebnis:

1. Öffnen Sie den betreffenden **Verkaufsauftrag**. Nutzen Sie zum Auffinden die BC-Funktion **Suchen** oder die Auftragsliste Ihres Rollencenters.
2. Wählen Sie im Verkaufsauftrag die **Verkaufszeile**, deren Fertigungsfortschritt Sie sehen möchten. Unterhalb der Verkaufszeilen wird der Bereich **Arbeitsgangstatusanzeige** angezeigt und automatisch auf die gewählte Zeile aktualisiert.
3. Lesen Sie in der **grafischen Ansicht** den Fortschritt farblich ab (grau, grün, rot, blau – siehe **Farbliche Statusdarstellung**). Die Kacheln der Halbfertigartikel-Arbeitsgänge werden durch diese App zusätzlich eingeblendet.
4. Nutzen Sie die **Listenansicht** darunter für die Detailwerte je Arbeitsgang (**Ebene**, **Status**, **Fertigungsauftragsnr.**, **Beschreibung**, **Menge**, **Startdatum/Startzeit**, **Enddatum/Endzeit**, **Fertiggestellte Menge**).
5. Klicken Sie auf eine **Kachel**, um den **FA-Arbeitsplan** des Arbeitsgangs zu öffnen, oder auf die **Fertigungsauftragsnr.** in der Liste, um den **Fertigungsauftrag** zu öffnen.

Es gibt in dieser App keinen Buchungs-, Freigabe- oder Beenden-Schritt. Die angezeigten Status entstehen aus den regulären Rückmeldungen der Fertigung.

## Voraussetzungen und Berechtigungen

Diese App ist eine reine Verbindungs-App und stellt selbst **keine** Einrichtungsseiten, Nummernserien oder Stammdatenmasken bereit. Damit die zusätzliche Anzeige funktioniert, müssen jedoch die folgenden Voraussetzungen aus den Basismodulen erfüllt sein. Diese Voraussetzungen richtet der **Administrator** einmalig vor der ersten Nutzung ein; angewendet werden sie anschließend im Tagesgeschäft im **Verkaufsauftrag**.

### Abhängige Module

Die App setzt drei installierte m+m-Module voraus (aus `app.json`):

| Voraussetzung | Erläuterung |
|---------------|-------------|
| **m+m Cloud Base** | Wenn installiert, dann stehen die gemeinsamen Basisfunktionen und die Lizenzprüfung zur Verfügung, ohne die die App beim Anmelden ihre Nutzung nicht freischalten kann. |
| **m+m Routing Status Overview** | Wenn installiert, dann existiert der Bereich **Arbeitsgangstatusanzeige** im Verkaufsauftrag überhaupt; diese App erweitert genau diesen Bereich um die Halbfertigartikel-Arbeitsgänge. Ohne dieses Modul gibt es keine Anzeige, die ergänzt werden könnte. |
| **m+m Semifinished Items** | Wenn installiert, dann werden Fertigungsauftragszeilen als **Halbfertigartikel** gekennzeichnet und mit einer **Halbfertigartikelherkunftszeilennr.** auf ihre Ursprungszeile verknüpft; erst diese Kennzeichnung liefert die Daten, die diese App in die Anzeige einspeist. |

### Halbfertigartikel-Arbeitsplätze (im Basismodul gepflegt)

Damit Halbfertigartikel-Zeilen entstehen, muss im Modul *m+m Semifinished Items* mindestens ein **Arbeitsplatz** als **Halbfertigartikel** gekennzeichnet sein. Beim Erzeugen und Aufteilen des Fertigungsauftrags werden die Arbeitsgänge dieses Arbeitsplatzes in eigene Fertigungsauftragszeilen mit dem Kennzeichen **Halbfertigartikel** überführt. Diese Konfiguration wird **nicht** in dieser App, sondern im Basismodul vorgenommen; sie ist hier nur als fachliche Voraussetzung genannt, damit der Anwender versteht, warum zusätzliche Zeilen und Kacheln erscheinen.

### Berechtigungen

Die App liefert den zuweisbaren Berechtigungssatz **MuM SFRO All** (`permissionset 5613851`). Dieser Berechtigungssatz legt fest, welche Aktionen ein Anwender im Rahmen dieser App ausführen darf: Er erteilt die Ausführungsberechtigung für die Verbindungs-Codeunit **MuM SFRO Routing Status Mgt.** Ordnen Sie diesen Berechtigungssatz allen Anwendern zu, die die erweiterte Arbeitsgangstatusanzeige im Verkaufsauftrag nutzen sollen. Ohne diesen Berechtigungssatz kann die ergänzende Anzeigelogik für den Anwender nicht ausgeführt werden. Die Lizenzprüfung erfolgt zusätzlich automatisch bei der Anmeldung über das Modul m+m Cloud Base; ist keine gültige Lizenz vorhanden, bleibt die Zusatzfunktion inaktiv.

## Arbeitsgangstatusanzeige im Verkaufsauftrag

Der Bereich **Arbeitsgangstatusanzeige** wird im **Verkaufsauftrag** unterhalb der Verkaufszeilen angezeigt. Er besteht aus zwei aufeinander abgestimmten Teilen: einer **grafischen Ansicht** (Kacheln je Arbeitsgang) und einer **Listenansicht** (tabellarische Detailzeilen). Beide Teile werden auf die aktuell markierte **Verkaufszeile** bezogen und aktualisiert; wechselt der Anwender die Verkaufszeile, aktualisieren sich beide Ansichten entsprechend.

Der eigentliche Beitrag dieser App: In beiden Teilen erscheinen zusätzlich die Arbeitsgänge der **Halbfertigartikel**-Fertigungsauftragszeilen. In der Listenansicht werden diese Zeilen über das Feld **Ebene** eingerückt (Baumdarstellung), sodass die Zugehörigkeit zur übergeordneten Fertigungsauftragszeile sichtbar bleibt.

### Grafische Ansicht

Die grafische Ansicht stellt die Arbeitsgänge des Fertigungsauftrags als Kacheln dar. Links wird das **Startdatum**, rechts das **Enddatum** des Fertigungsauftrags eingeblendet. Jede Kachel enthält die **Arbeitsgangnr.** und die **Beschreibung** des Arbeitsgangs; für Halbfertigartikel-Arbeitsgänge wird der zugehörige **Artikelnr.** ergänzt, damit der Anwender die Halbfertigstufe eindeutig erkennt. Zusätzlich zeigt die Kachel die **Fertiggestellte Menge** des jeweiligen Arbeitsgangs.

Ein Klick auf eine Kachel öffnet den **FA-Arbeitsplan** des betreffenden Fertigungsauftrags. So gelangt der Anwender von der Übersicht direkt in die Detailbearbeitung des Arbeitsplans.

#### Farbliche Statusdarstellung

Die Farbe einer Kachel richtet sich nach dem Feld **Arbeitsplanstatus** des jeweiligen Arbeitsgangs im **FA-Arbeitsplan**. Der Arbeitsplanstatus ist ein Feld mit einem festen Wertevorrat; für jeden Wert bedeutet die Anzeige Folgendes:

| Arbeitsplanstatus | Farbe und Bedeutung |
|-------------------|---------------------|
| **(leer)** | Wenn der Arbeitsplanstatus leer ist, dann erscheint die Kachel **grau**: Der Arbeitsgang ist angelegt, aber noch nicht begonnen; es liegen keine Rückmeldungen vor. |
| **geplant** | Wenn der Arbeitsplanstatus auf *geplant* steht, dann erscheint die Kachel **grün**: Der Arbeitsgang ist eingeplant und für die Bearbeitung vorgesehen. |
| **in Bearbeitung** | Wenn der Arbeitsplanstatus auf *in Bearbeitung* steht, dann erscheint die Kachel **rot**: Am Arbeitsgang wird gerade gearbeitet bzw. es sind Teilrückmeldungen erfolgt. |
| **fertig** | Wenn der Arbeitsplanstatus auf *fertig* steht, dann erscheint die Kachel **blau**: Der Arbeitsgang ist abgeschlossen. |

Auf diese Weise erhält der Anwender in Echtzeit einen farblichen Überblick über den Fortschritt – für die Arbeitsgänge des Hauptartikels ebenso wie für die durch diese App ergänzten Arbeitsgänge der Halbfertigartikel. In der Praxis wird Arbeitsgang für Arbeitsgang zurückgemeldet, sodass die Kacheln eines Fertigungsauftrags unterschiedliche Farben annehmen.

### Listenansicht

Unter der grafischen Ansicht listet die Listenansicht die Arbeitsgänge und Fertigungsauftragszeilen als Detailzeilen auf. Die Halbfertigartikel-Zeilen werden von dieser App mit **Ebene = 1** eingefügt und dadurch unter ihrer Ursprungszeile eingerückt dargestellt. Alle Felder sind schreibgeschützt (reine Anzeige).

| Feld | Erläuterung |
|------|-------------|
| **Ebene** | Wenn die Ebene größer als 0 ist, dann handelt es sich um eine durch diese App ergänzte **Halbfertigartikel**-Zeile; sie wird eingerückt unter der übergeordneten Fertigungsauftragszeile angezeigt. Ebene 0 kennzeichnet die Hauptzeile. |
| **Status** | Zeigt den Fertigungsauftragsstatus der Zeile (z. B. freigegeben, beendet). Er steuert, welche Fertigungsauftrags-Maske sich beim Aufruf öffnet. |
| **Fertigungsauftragsnr.** | Wenn der Anwender diese Nummer anklickt, dann öffnet sich der zugehörige **Fertigungsauftrag** in der zum Status passenden Maske (z. B. **Freigegebener FA** oder **Beendeter FA**). |
| **Beschreibung** | Bezeichnung der Fertigungsauftragszeile bzw. des Arbeitsgangs; dient der eindeutigen Identifikation in der Baumstruktur. |
| **Menge** | Geplante Menge der Fertigungsauftragszeile. Sie bildet die Bezugsgröße, gegen die die fertiggestellte Menge gelesen wird. |
| **Startdatum** | Geplanter Beginn der Fertigungsauftragszeile; unterstützt die Terminauskunft gegenüber dem Kunden. |
| **Startzeit** | Geplante Startuhrzeit ergänzend zum Startdatum für die Feinterminierung. |
| **Enddatum** | Geplantes Ende der Fertigungsauftragszeile; Grundlage für die Liefertermin-Einschätzung. |
| **Endzeit** | Geplante Enduhrzeit ergänzend zum Enddatum. |
| **Fertiggestellte Menge** | Wenn Rückmeldungen gebucht wurden, dann zeigt dieses Feld die bereits fertiggestellte Menge des Arbeitsgangs; der Vergleich mit **Menge** zeigt dem Anwender den Restfortschritt. Der Wert wird aus den Kapazitätsposten des Arbeitsgangs ermittelt. |

### Navigation aus der Anzeige

Aus der Arbeitsgangstatusanzeige stehen dem Anwender zwei Absprünge zur Verfügung:

- **Kachel anklicken** öffnet den **FA-Arbeitsplan** des Fertigungsauftrags. Dort sieht der Anwender die Arbeitsgänge im Detail (schreibgeschützt geöffnet).
- **Fertigungsauftragsnr. in der Liste anklicken** öffnet den **Fertigungsauftrag** selbst. Je nach **Status** der Zeile öffnet sich die passende Maske, etwa **Freigegebener FA** oder **Beendeter FA**.

Beide Absprünge sind Anzeige- bzw. Bearbeitungssprünge in Standardmasken; diese App führt dabei keine Buchung und keine Statusänderung aus.

## FAQ und Troubleshooting

### 1. Warum sehe ich im Verkaufsauftrag plötzlich zusätzliche, eingerückte Zeilen in der Arbeitsgangstatusanzeige?

Weil der Fertigungsauftrag **Halbfertigartikel**-Zeilen enthält. Diese App fügt deren Arbeitsgänge mit **Ebene = 1** in die Anzeige ein, sodass sie eingerückt unter der jeweiligen Hauptzeile erscheinen. Ohne die App wären nur die Arbeitsgänge des Hauptartikels sichtbar.

### 2. Was bedeuten die Farben der Kacheln?

Die Farbe folgt dem Feld **Arbeitsplanstatus** im **FA-Arbeitsplan**: leer = grau, *geplant* = grün, *in Bearbeitung* = rot, *fertig* = blau. Damit ist der Bearbeitungsstand jedes Arbeitsgangs auf einen Blick erkennbar.

### 3. Warum bleibt eine Kachel grau, obwohl der Arbeitsgang existiert?

Weil der **Arbeitsplanstatus** dieses Arbeitsgangs noch leer ist. Sobald der Arbeitsgang eingeplant oder zurückgemeldet wird, wechselt die Farbe auf grün, rot bzw. blau. Grau bedeutet: angelegt, aber noch keine Rückmeldung.

### 4. Warum erscheinen keine Halbfertigartikel-Arbeitsgänge, obwohl der Fertigungsauftrag welche haben sollte?

Die Zeilen werden nur ergänzt, wenn die Fertigungsauftragszeilen tatsächlich als **Halbfertigartikel** gekennzeichnet sind (Kennzeichen **Halbfertigartikel = ja** und gesetzte **Halbfertigartikelherkunftszeilennr.**). Diese Kennzeichnung entsteht im Modul *m+m Semifinished Items* beim Aufteilen des Fertigungsauftrags. Prüfen Sie, ob der betreffende **Arbeitsplatz** als Halbfertigartikel gekennzeichnet und der Fertigungsauftrag aufgeteilt wurde.

### 5. Woher kommt die angezeigte fertiggestellte Menge?

Die **Fertiggestellte Menge** eines Arbeitsgangs wird aus den Kapazitätsposten des Fertigungsauftrags summiert (Ausgabemenge des jeweiligen Arbeitsgangs). Sie steigt, sobald Rückmeldungen zum Arbeitsgang gebucht werden.

### 6. Welche Seite öffnet sich, wenn ich auf eine Kachel klicke?

Der **FA-Arbeitsplan** des zugehörigen Fertigungsauftrags. Er wird schreibgeschützt geöffnet und zeigt die Arbeitsgänge der Zeile im Detail.

### 7. Welche Seite öffnet sich, wenn ich auf die Fertigungsauftragsnr. klicke?

Der **Fertigungsauftrag** in der zum **Status** passenden Maske, zum Beispiel **Freigegebener FA** bei freigegebenen oder **Beendeter FA** bei beendeten Aufträgen.

### 8. Muss ich für diese App etwas einrichten?

Nein. Die App benötigt keine eigene Einrichtung. Es müssen lediglich die abhängigen Module installiert, eine gültige Lizenz vorhanden und der Berechtigungssatz **MuM SFRO All** zugewiesen sein. Die Halbfertigartikel-Kennzeichnung der Arbeitsplätze erfolgt im Basismodul *m+m Semifinished Items*.

### 9. Warum ändert sich die Anzeige, wenn ich eine andere Verkaufszeile markiere?

Die Arbeitsgangstatusanzeige bezieht sich immer auf die aktuell markierte **Verkaufszeile**. Bei mehreren Verkaufszeilen aktualisieren sich grafische und Listenansicht entsprechend der gewählten Zeile.

### 10. Kann ich in der Arbeitsgangstatusanzeige Mengen oder Status ändern?

Nein. Die Anzeige ist schreibgeschützt. Änderungen an Arbeitsgängen, Mengen oder Status nehmen Sie im **FA-Arbeitsplan** bzw. im **Fertigungsauftrag** vor; die Anzeige spiegelt diese Werte anschließend wider.

## Typische Anwendungsfälle

Die folgenden Szenarien beruhen auf dem tatsächlichen, im Code nachvollziehbaren Ablauf dieser App (Verknüpfung von Halbfertigartikel-Fertigungszeilen mit der Arbeitsgangstatusanzeige im Verkaufsauftrag). Sie sind bewusst knapp gehalten.

### Anwendungsfall 1: Kundenanruf zum Lieferstatus eines mehrstufigen Auftrags

- **Auslöser:** Ein Kunde ruft im Innendienst an und fragt nach dem Fertigungsfortschritt seines Auftrags, dessen Artikel über eine Halbfertigstufe gefertigt wird.
- **Einstieg in BC:** Der Anwender öffnet den **Verkaufsauftrag** (über **Suchen** oder die Auftragsliste) und markiert die betreffende **Verkaufszeile**. Unterhalb der Verkaufszeilen erscheint die **Arbeitsgangstatusanzeige**.
- **Kernablauf:** In der **grafischen Ansicht** liest der Anwender den Fortschritt farblich ab. Neben den Arbeitsgängen des Hauptartikels sind – dank dieser App – die Kacheln der **Halbfertigartikel**-Arbeitsgänge sichtbar (mit **Arbeitsgangnr.**, **Beschreibung** und **Artikelnr.** der Halbfertigstufe). Blaue Kacheln zeigen abgeschlossene, rote Kacheln laufende, grüne geplante und graue noch nicht begonnene Arbeitsgänge. In der **Listenansicht** prüft der Anwender bei Bedarf **Fertiggestellte Menge** gegen **Menge** sowie **Enddatum/Endzeit**.
- **Abschluss:** Der Anwender gibt dem Kunden anhand der Farben und Termine eine belastbare Auskunft. Für Detailfragen klickt er eine Kachel an und öffnet den **FA-Arbeitsplan**.

### Anwendungsfall 2: Interne Fortschrittskontrolle vor der Feinterminierung

- **Auslöser:** Die Fertigungssteuerung möchte vor der Wochenplanung prüfen, welche Halbfertigstufen eines Verkaufsauftrags bereits fertiggestellt sind.
- **Einstieg in BC:** Öffnen des **Verkaufsauftrags** und Auswahl der relevanten **Verkaufszeile**; die **Arbeitsgangstatusanzeige** wird auf diese Zeile aktualisiert.
- **Kernablauf:** In der **Listenansicht** erkennt der Anwender über die **Ebene**-Einrückung, welche Zeilen Halbfertigartikel-Arbeitsgänge sind. Er vergleicht je Arbeitsgang **Fertiggestellte Menge** mit **Menge** und liest **Startdatum/Enddatum**. Über die **Fertigungsauftragsnr.** springt er bei Bedarf in den **Fertigungsauftrag** (**Freigegebener FA**), um Kapazitäten zu prüfen.
- **Abschluss:** Auf Basis des sichtbaren Fortschritts entscheidet die Fertigungssteuerung über die Reihenfolge der nächsten Arbeitsgänge. Diese App nimmt dabei keine Buchung vor; sie liefert ausschließlich die zusammengeführte Statusübersicht.
