---
title: Anwenderhandbuch m+m Production Order Job Overview with Test Certificate Mgt.
---

# Anwenderhandbuch m+m Production Order Job Overview with Test Certificate Mgt.

## Einleitung

Die App **m+m Production Order Job Overview with Test Certificate Mgt.** erweitert die Ansicht **FA-Arbeitsvorrat** in Microsoft Dynamics 365 Business Central um die Prüfdaten aus dem Prüfwesen. In der Zeilenliste des FA-Arbeitsvorrats sehen die Anwender pro Arbeitsgang direkt den **Prüfstatus** und die zugehörige **Prüfung Nr.**, ohne den Fertigungsauftrag oder die Prüfung separat öffnen zu müssen.

**Zielgruppe:** Primär richtet sich dieses Modul an die **operativen Anwender in der Fertigung** – Werker, Vorarbeiter und Fertigungssteuerung –, die im FA-Arbeitsvorrat Arbeitsgänge starten, teilbeenden und beenden. Für diese Anwender ist der Prüfstatus die entscheidende Zusatzinformation, bevor ein Arbeitsgang gemeldet wird. Sekundär betrifft das Modul die **Qualitätssicherung**, die die Prüfungen und Proben pflegt, sowie die **Administration**, die die Berechtigungen vergibt.

**Kurzer Prozessüberblick:** Der Anwender öffnet den **FA-Arbeitsvorrat** über die Suche, grenzt die Liste über **Arbeitsplatzgruppennr.** und optional **Arbeitsplatznr.** ein und erhält je Arbeitsgang eine Zeile. Zu jeder Zeile blendet das Modul den **Prüfstatus** und die **Prüfung Nr.** ein und stellt in der Infobox **Prüfdaten** die Prüfmerkmale der zugeordneten Prüfung dar. Über eine Absprung-Funktion gelangt der Anwender direkt in die **Prüfungskarte** bzw. in die **Proben**. Anschließend meldet er den Arbeitsgang im gewohnten Ablauf des FA-Arbeitsvorrats zurück (**Starten**, **Teilbeenden**, **Beenden**).

Die Prüfdaten werden dabei **automatisch** aus dem Arbeitsgang des Fertigungsauftrags in die Zeile des FA-Arbeitsvorrats übernommen; der Anwender muss den Prüfstatus nicht manuell erfassen.

## Schnellstart für Anwender

Der schnellste Weg vom Öffnen der Liste bis zur Meldung eines Arbeitsgangs mit geprüftem Prüfstatus:

1. **FA-Arbeitsvorrat** über **Suchen** aufrufen.
2. Im Feld **Arbeitsplatzgruppennr.** die zuständige Arbeitsplatzgruppe auswählen. Es erscheinen alle Arbeitsgänge dieser Gruppe.
3. Optional das Feld **Arbeitsplatznr.** setzen, um die Liste auf einen einzelnen Arbeitsplatz einzugrenzen (nicht zwingend).
4. Die gewünschte Arbeitsgangzeile auswählen. In der Zeile werden **Prüfstatus** (farblich hinterlegt) und **Prüfung Nr.** angezeigt.
5. Ist der **Prüfstatus** = **Gesperrt** (rot), zunächst die Prüfung klären: entweder in der Zeile auf **Prüfstatus** oder **Prüfung Nr.** klicken, um die **Prüfungskarte** zu öffnen, oder über die Aktion **Prüfzertifikatvorlagen öffnen** in die **Proben** wechseln und die Prüfdaten vervollständigen.
6. Den Arbeitsgang starten: Aktion **Starten**.
7. Bei einer Teilmenge: Aktion **Teilbeenden** – der Arbeitsgang bleibt für die Restmenge offen.
8. Bei vollständiger Erledigung: Aktion **Beenden** – der Arbeitsgang wird auf **Beendet** gesetzt.

> Voraussetzung ist, dass dem Arbeitsgang im Arbeitsplan des Fertigungsauftrags eine Prüfung zugeordnet ist. Ist keine Prüfung hinterlegt, bleiben **Prüfstatus** = **(leer)** und **Prüfung Nr.** leer; der Meldeablauf ist davon nicht betroffen.

## Voraussetzungen und Berechtigungen

Dieses Modul ist eine reine Integrationserweiterung und bringt keine eigenen Einrichtungsseiten, Nummernserien oder Stammdaten mit. Damit die Prüfdaten im FA-Arbeitsvorrat erscheinen, müssen die folgenden Bausteine vorhanden sein:

1. Die App **m+m Production Order Job Overview** stellt die Ansicht **FA-Arbeitsvorrat** und den Meldeablauf (**Starten**, **Teilbeenden**, **Beenden**) bereit. Sie ist Voraussetzung, weil dieses Modul deren Zeilenliste erweitert.
2. Die App **m+m Test Certificate Management** stellt die Prüfungen, die **Prüfungskarte** und die **Proben** bereit. Sie ist Voraussetzung, weil der Prüfstatus und die Prüfung Nr. aus dieser Quelle stammen.
3. Am Arbeitsgang (Arbeitsplan des Fertigungsauftrags) muss eine Prüfung zugeordnet sein. Nur dann füllt das Modul **Prüfstatus** und **Prüfung Nr.** in der Zeile des FA-Arbeitsvorrats.

**Berechtigungen:** Die Erweiterung liefert den Berechtigungssatz **MuM PJTC All**. Dieser legt fest, welche Aktionen die Anwender im Zusammenhang mit den Prüfdaten im FA-Arbeitsvorrat ausführen dürfen; er umfasst die Ausführung der beiden Verarbeitungscodeunits und den Zugriff auf die Infobox **Prüfdaten**. Die Administration weist diesen Berechtigungssatz zusätzlich zu den Berechtigungen der beiden Basismodule zu. Ohne die Berechtigungen der Basismodule ist der FA-Arbeitsvorrat selbst nicht nutzbar.

## Tägliche Arbeit im FA-Arbeitsvorrat

Der **FA-Arbeitsvorrat** ist die zentrale Arbeitsliste dieses Moduls. Die folgenden Abschnitte beschreiben die vom Modul ergänzten Bestandteile und wie sie sich in den bestehenden Meldeablauf einfügen. Der Anwender öffnet die Ansicht über **Suchen**; sie ist eine übergeordnete Arbeitsliste und wird nicht aus einer Stammdatenkarte heraus aufgerufen.

### Einstieg und Filter

**Einstieg:** **Suchen** → **FA-Arbeitsvorrat**. Danach grenzt der Anwender die Liste über die beiden Kopf-Filter ein. Der Filter für die Arbeitsplatzgruppe ist die übergeordnete Ebene, der Filter für den Arbeitsplatz die optionale untergeordnete Ebene.

| Filterfeld | Erläuterung |
|------------|-------------|
| **Arbeitsplatzgruppennr.** | Wenn gesetzt, werden nur die Arbeitsgänge der gewählten Arbeitsplatzgruppe angezeigt. Dieser Filter ist der übliche Einstieg: Der Anwender wählt zuerst seine Arbeitsplatzgruppe und sieht dann alle offenen Arbeitsgänge dazu. |
| **Arbeitsplatznr.** | Wenn zusätzlich gesetzt, wird die Liste innerhalb der Arbeitsplatzgruppe auf einen einzelnen Arbeitsplatz eingeschränkt. Dieser Filter ist optional; ohne ihn bleiben alle Arbeitsplätze der Gruppe sichtbar. |

Beide Filter sind Bestandteil der Basisansicht; die Erweiterung fügt keine weiteren Filter hinzu.

### Neue Spalten in der Zeilenliste

Zu jeder Arbeitsgangzeile des FA-Arbeitsvorrats blendet das Modul zwei zusätzliche Spalten ein. Sie stehen am Ende der Zeile und sind nicht editierbar – die Werte werden automatisch aus dem Arbeitsgang übernommen (siehe *Automatische Übernahme der Prüfdaten*).

| Feld | Erläuterung |
|------|-------------|
| **Prüfstatus** | Zeigt den Prüfzustand des Arbeitsgangs an und ist farblich hervorgehoben. Wenn der Wert gesetzt ist, erkennt der Anwender vor dem Melden auf einen Blick, ob die Prüfung offen, bestanden oder gesperrt ist. Ein Klick auf die Spalte öffnet die **Prüfungskarte** der zugeordneten Prüfung. Die einzelnen Werte sind unten erläutert. |
| **Prüfung Nr.** | Enthält die Nummer der dem Arbeitsgang zugeordneten Prüfung. Wenn gefüllt, verweist sie auf die konkrete Prüfung im Prüfwesen; ist keine Prüfung zugeordnet, bleibt das Feld leer. Ein Klick auf die Spalte öffnet ebenfalls die **Prüfungskarte** dieser Prüfung. |

**Werte des Feldes Prüfstatus** (jeder Wert steuert, was der Anwender vor dem Melden tun sollte):

- **(leer):** Dem Arbeitsgang ist keine Prüfung zugeordnet. Es ist keine Prüfhandlung erforderlich; der Arbeitsgang kann regulär gemeldet werden.
- **Prüfung:** Dem Arbeitsgang ist eine Prüfung zugeordnet, ein abschließendes Ergebnis liegt aber noch nicht vor. Der Anwender sollte die Prüfdaten vor dem Beenden prüfen bzw. vervollständigen. Die Zeile wird neutral hervorgehoben.
- **Bestanden:** Die Prüfung ist erfolgreich abgeschlossen. Der Arbeitsgang kann ohne weitere Prüfhandlung gemeldet werden. Die Zeile wird positiv (grün) hervorgehoben.
- **Gesperrt:** Die Prüfung ist nicht bestanden bzw. gesperrt. Der Anwender sollte den Arbeitsgang **nicht** ohne Klärung beenden; zunächst ist die Prüfung über die **Prüfungskarte** oder die **Proben** zu klären. Die Zeile wird negativ (rot) hervorgehoben.

> Die farbliche Hervorhebung dient der schnellen Orientierung in der Liste: grün für **Bestanden**, rot für **Gesperrt**, neutral für **Prüfung**. Der Prüfstatus ist eine Anzeige- und Entscheidungshilfe und ändert den technischen Meldeablauf des FA-Arbeitsvorrats nicht; er verhindert insbesondere nicht automatisch das Beenden. Die Bewertung, ob bei **Gesperrt** gemeldet werden darf, trifft der Anwender gemäß den betrieblichen Vorgaben.

Zur Orientierung zeigt die Basisansicht je Arbeitsgangzeile außerdem u. a. die **Fertigungsauftragsnr.**, die **Artikelnr.**, die **Arbeitsgangnr.** sowie **Menge** und **Restmenge**. Diese Spalten gehören zum Basismodul; **Prüfstatus** und **Prüfung Nr.** ergänzen sie am Zeilenende.

### Infobox Prüfdaten

Zusätzlich zu den Spalten blendet das Modul rechts die Infobox **Prüfdaten** ein. Sie ist an die **Prüfung Nr.** der aktuell markierten Zeile gekoppelt und zeigt die Prüfmerkmale (Zeilen) der zugeordneten Prüfung an. So sieht der Anwender die Merkmale und deren Vorgabewerte, ohne die Prüfung öffnen zu müssen.

| Feld | Erläuterung |
|------|-------------|
| **Prüfgruppencode** | Zeigt die Prüfgruppe des Merkmals. Wenn gefüllt, ordnet sie das Merkmal einer Gruppe im Prüfwesen zu und hilft dem Anwender, zusammengehörige Merkmale zu erkennen. |
| **Prüfmerkmalsbeschreibung** | Beschreibt das einzelne Prüfmerkmal im Klartext, sodass der Anwender ohne Rückgriff auf Codes erkennt, was geprüft wird. |
| **Vorgabe Wert 1** | Zeigt den ersten Vorgabewert des Merkmals. Wenn gesetzt, dient er dem Anwender als Soll-/Referenzwert für die Prüfung. |
| **Vorgabe Wert 2** | Zeigt den zweiten Vorgabewert des Merkmals (z. B. eine zweite Grenze oder Alternative). Wenn gesetzt, ergänzt er **Vorgabe Wert 1** als weitere Referenz. |

Die Infobox ist reine Anzeige (nicht editierbar). Die Merkmalszeilen ohne zugeordnete Prüfung bleiben leer. Technisch nicht sichtbare Steuerfelder der Infobox (die interne **Prüfung Nr.** der Zeile sowie eine Druckoption) sind ausgeblendet und für den Anwender nicht relevant.

### Aktion Prüfzertifikatvorlagen öffnen

Im Menüband des FA-Arbeitsvorrats ergänzt das Modul die (auch als Verarbeitungsaktion angeheftete) Aktion **Prüfzertifikatvorlagen öffnen**.

Öffnen Sie über die Aktion **Prüfzertifikatvorlagen öffnen** die Proben der zur markierten Zeile gehörenden Prüfung:

- Existiert genau **eine** Probe zur Prüfung, öffnet sich direkt die **Probe** (Einzelkarte).
- Existieren **mehrere** Proben, öffnet sich die Liste **Proben**, aus der der Anwender die gewünschte Probe auswählt.

Ist der markierten Zeile keine gültige **Prüfung Nr.** zugeordnet, geschieht nichts. So kann der Anwender die Probendaten direkt aus dem FA-Arbeitsvorrat heraus einsehen und – im Prüfwesen – vervollständigen, bevor er den Arbeitsgang beendet.

### Absprung in die Prüfungskarte

Über die Spalten **Prüfstatus** und **Prüfung Nr.** springt der Anwender per Klick in die **Prüfungskarte** der zugeordneten Prüfung. Öffnen Sie über den Klick auf eine dieser Spalten die **Prüfungskarte**, um die Prüfung im Detail einzusehen. Nach dem Schließen der Karte aktualisiert das Modul die Zeile automatisch: Der aktuelle **Prüfstatus** und die **Prüfung Nr.** werden erneut aus dem Arbeitsgang des Fertigungsauftrags gelesen und in der Zeile angezeigt. Änderungen an der Prüfung wirken sich damit unmittelbar auf die Anzeige im FA-Arbeitsvorrat aus.

### Automatische Übernahme der Prüfdaten

Der **Prüfstatus** und die **Prüfung Nr.** werden nicht manuell erfasst, sondern automatisch ermittelt. Beim Aufbau der Zeilenliste des FA-Arbeitsvorrats liest das Modul zu jeder Arbeitsgangzeile den zugehörigen Arbeitsgang des Fertigungsauftrags aus und übernimmt von dort den hinterlegten Prüfstatus und die Prüfung Nr. in die angezeigte Zeile. Die Zuordnung erfolgt über Fertigungsauftrag, Fertigungsauftragszeile und **Arbeitsgangnr.**.

Praktische Folge für den Anwender:

- Ändert sich am Arbeitsgang die Prüfung oder deren Status, erscheint die Änderung beim nächsten Aufbau der Liste bzw. nach dem Absprung in die **Prüfungskarte** automatisch in der Zeile.
- Da die Werte abgeleitet sind, sind die Spalten **Prüfstatus** und **Prüfung Nr.** im FA-Arbeitsvorrat nicht editierbar.

### Einordnung in den Meldeablauf

Die Prüfdaten sind eine Entscheidungshilfe innerhalb des bestehenden Meldeablaufs des FA-Arbeitsvorrats. Der vollständige Ablauf lautet:

1. **FA-Arbeitsvorrat** über **Suchen** öffnen.
2. **Arbeitsplatzgruppennr.** setzen (übergeordneter Filter).
3. Optional **Arbeitsplatznr.** setzen (untergeordneter Filter).
4. Arbeitsgangzeile auswählen und **Prüfstatus** prüfen; bei **Gesperrt** über **Prüfungskarte** oder **Prüfzertifikatvorlagen öffnen** klären.
5. **Starten** – der Arbeitsgang wird auf **Gestartet** gesetzt.
6. **Teilbeenden** – bei Teilmengen; der Status wechselt auf **Teilbeendet** und die Restmenge bleibt offen.
7. **Beenden** – bei vollständiger Erledigung; der Status wechselt auf **Beendet**.

Die Aktionen **Starten**, **Teilbeenden** und **Beenden** sowie die zugehörige Buchungsseite gehören zum Basismodul **m+m Production Order Job Overview**; dieses Modul blendet keinen Buchungsschritt aus und fügt keinen hinzu. Für die Details des Buchungsdialogs gilt die Dokumentation des Basismoduls.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die Prüfdaten im Tagesgeschäft genutzt werden. Alle Schritte entsprechen dem oben beschriebenen, im Code hinterlegten Ablauf.

### Anwendungsfall 1: Gesperrte Prüfung vor dem Beenden klären

**Auslöser:** Ein Werker möchte einen Arbeitsgang beenden und sieht in seiner Arbeitsliste eine rot hervorgehobene Zeile.

**Einstieg in BC:** Er öffnet über **Suchen** den **FA-Arbeitsvorrat** und wählt im Feld **Arbeitsplatzgruppennr.** seine Arbeitsplatzgruppe.

**Kernablauf:** In der Zeile des betreffenden Arbeitsgangs steht **Prüfstatus** = **Gesperrt**. Der Werker klickt auf die Spalte **Prüfstatus** und gelangt in die **Prüfungskarte**. Dort erkennt er, dass die Prüfung nicht bestanden wurde. Er klärt den Fall mit der Qualitätssicherung. Nach dem Schließen der Karte aktualisiert der FA-Arbeitsvorrat die Zeile automatisch. Erst wenn die Prüfung – im Prüfwesen – auf **Bestanden** gesetzt ist und die Zeile grün erscheint, meldet er den Arbeitsgang.

**Abschluss:** Der Werker wählt **Beenden**; der Arbeitsgang wird auf **Beendet** gesetzt.

### Anwendungsfall 2: Probendaten erfassen und Arbeitsgang teilbeenden

**Auslöser:** Zu einem laufenden Arbeitsgang liegt der Hinweis vor, dass vor der Teilmeldung Probenwerte zu dokumentieren sind.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** den **FA-Arbeitsvorrat**, setzt **Arbeitsplatzgruppennr.** und optional **Arbeitsplatznr.** und markiert die Arbeitsgangzeile.

**Kernablauf:** In der Infobox **Prüfdaten** sieht er die Prüfmerkmale mit **Prüfmerkmalsbeschreibung** und den **Vorgabe Wert 1**/**Vorgabe Wert 2**. Über die Aktion **Prüfzertifikatvorlagen öffnen** wechselt er in die **Proben** der Prüfung und trägt dort die Werte ein. Anschließend kehrt er in den FA-Arbeitsvorrat zurück; der **Prüfstatus** der Zeile ist aktualisiert.

**Abschluss:** Da nur eine Teilmenge fertig ist, wählt der Anwender **Teilbeenden**. Der Status wechselt auf **Teilbeendet**, die Restmenge bleibt für eine spätere Meldung offen. Nach Fertigstellung der Restmenge beendet er den Arbeitsgang später mit **Beenden**.

## FAQ und Troubleshooting

### 1. Warum ist bei einer Zeile im FA-Arbeitsvorrat der Prüfstatus leer?
Weil dem Arbeitsgang im Arbeitsplan des Fertigungsauftrags keine Prüfung zugeordnet ist. Das Modul übernimmt **Prüfstatus** und **Prüfung Nr.** nur dann, wenn am Arbeitsgang eine Prüfung hinterlegt ist. Ohne Zuordnung bleiben beide Felder leer, und es ist keine Prüfhandlung erforderlich.

### 2. Wie öffne ich die Prüfung zu einer Zeile?
Klicken Sie in der Zeile auf **Prüfstatus** oder **Prüfung Nr.**. Beide Spalten springen in die **Prüfungskarte** der zugeordneten Prüfung.

### 3. Was bedeuten die Farben in der Spalte Prüfstatus?
Grün steht für **Bestanden**, rot für **Gesperrt**, neutral für **Prüfung** (Prüfung zugeordnet, aber noch kein Ergebnis). **(leer)** bedeutet: keine Prüfung zugeordnet. Die Farbe ist eine Orientierungshilfe für die Entscheidung vor dem Melden.

### 4. Kann ich einen Arbeitsgang mit dem Prüfstatus Gesperrt beenden?
Das Modul verhindert das Beenden technisch nicht. **Gesperrt** ist ein Warnhinweis, dass die Prüfung nicht bestanden wurde. Ob gemeldet werden darf, richtet sich nach den betrieblichen Vorgaben; klären Sie den Fall zuvor über die **Prüfungskarte** oder die **Proben**.

### 5. Warum kann ich Prüfstatus und Prüfung Nr. nicht ändern?
Beide Spalten sind nicht editierbar, weil ihre Werte automatisch aus dem Arbeitsgang des Fertigungsauftrags abgeleitet werden. Änderungen nehmen Sie an der Prüfung im Prüfwesen vor; die Anzeige im FA-Arbeitsvorrat wird danach automatisch aktualisiert.

### 6. Die Prüfung wurde geändert – warum sehe ich den neuen Status nicht sofort?
Die Werte werden beim Aufbau der Zeilenliste bzw. nach dem Absprung in die **Prüfungskarte** neu ermittelt. Nach dem Schließen der **Prüfungskarte** aktualisiert das Modul die Zeile automatisch; alternativ genügt ein erneuter Aufbau der Liste.

### 7. Was zeigt die Infobox Prüfdaten an?
Sie zeigt die Prüfmerkmale (Zeilen) der Prüfung, die der aktuell markierten Zeile zugeordnet ist – mit **Prüfgruppencode**, **Prüfmerkmalsbeschreibung** sowie **Vorgabe Wert 1** und **Vorgabe Wert 2**. Die Infobox ist reine Anzeige.

### 8. Wozu dient die Aktion Prüfzertifikatvorlagen öffnen?
Sie öffnet die **Proben** der zur markierten Zeile gehörenden Prüfung. Gibt es genau eine Probe, öffnet sich direkt die **Probe**; gibt es mehrere, öffnet sich die Liste **Proben** zur Auswahl. So erreichen Sie die Probendaten direkt aus dem FA-Arbeitsvorrat.

### 9. Ich habe keine Berechtigung für die Prüfdaten – woran liegt das?
Für die Prüfdaten im FA-Arbeitsvorrat wird der Berechtigungssatz **MuM PJTC All** benötigt. Zusätzlich müssen die Berechtigungen der Basismodule **m+m Production Order Job Overview** und **m+m Test Certificate Management** vorhanden sein. Wenden Sie sich an Ihre Administration.

### 10. Ich sehe die neuen Spalten und die Infobox nicht – was tun?
Prüfen Sie, ob die App installiert und der Berechtigungssatz **MuM PJTC All** zugewiesen ist und ob die beiden Basismodule vorhanden sind. Sind die Spalten in Ihrer persönlichen Ansicht ausgeblendet, blenden Sie **Prüfstatus** und **Prüfung Nr.** über die Personalisierung wieder ein. Bleiben die Werte leer, ist dem Arbeitsgang keine Prüfung zugeordnet (siehe Frage 1).
