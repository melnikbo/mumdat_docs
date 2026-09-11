---
title: Cloud Base
---

# m+m Cloud Base

## Einleitung
m+m Cloud Base steuert die Lizenzierung der installierten m+m Apps in Microsoft Dynamics 365 Business Central. Anwender in der Administration pflegen Lizenzschlüssel, prüfen den Lizenzstatus einzelner Module und ordnen Benutzer oder Mandanten zu, wenn die Lizenzart dies verlangt.

Der typische Ablauf ist kurz: Zuerst hinterlegen Sie einen Lizenzschlüssel, danach aktualisiert das System die lizenzierten Module. Anschließend prüfen Sie je Modul die Lizenzart, die Gültigkeit und die zulässige Anzahl an Zuweisungen. Bei benutzer- oder mandantenbezogenen Lizenzen ergänzen Sie die erforderlichen Zuweisungen.

## Schnellstart für Anwender
1. Öffnen Sie über **Suchen** die Seite **m+m Module**.
2. Wählen Sie die Aktion **Eintrag aktualisieren/einfügen**.
3. Erfassen oder ersetzen Sie den **Lizenzschlüssel** und bestätigen Sie den Dialog.
4. Prüfen Sie in der Liste die Felder **Lizenzart**, **Lizenzierte Werte**, **Zugewiesene Lizenzwerte** und **Gültig bis**.
5. Wenn die Lizenzart benutzer- oder mandantenbezogen ist, öffnen Sie über **Wertzuweisung** die zugehörigen Zuweisungen und ergänzen die benötigten Einträge.
6. Kontrollieren Sie abschließend, ob das Modul als gültig nutzbar ist und keine überfällige Zahlung oder abgelaufene Gültigkeit vorliegt.

## Einrichtung
### Lizenzschlüssel hinterlegen
Die eigentliche Einrichtung erfolgt auf den Listen **m+m Module** und **m+m Produkte**. Beide Seiten stellen eine Aktion bereit, mit der Sie einen Lizenzschlüssel erfassen oder ersetzen. Nach der Bestätigung ruft die App die zugehörigen Lizenzdaten ab und aktualisiert die gespeicherten Produkt- und Modulinformationen.

Auf der Seite **m+m Module** verwalten Sie die eigentlichen lizenzierten Module. Diese Seite ist der wichtigste Einstiegspunkt für die laufende Arbeit.

| Einrichtung | Erläuterung |
|---|---|
| Modul-GUID | Eindeutige technische Kennung des Moduls. Das Feld ist schreibgeschützt und dient der internen Zuordnung. |
| Name | Bezeichnung des Moduls. Darüber erkennen Sie, für welche App der Eintrag gilt. |
| Lizenzschlüssel | Hinterlegter Lizenzschlüssel für das Modul. Über die Aktualisierungsaktion können Sie den Wert neu einlesen oder ersetzen. |
| Als Bundle gekauft | Kennzeichnet, ob das Modul als Teil eines Produktpakets geliefert wurde. |
| Zugehöriger Produktname | Zeigt den Namen des verknüpften Produkts an, aus dem das Modul stammt. |
| Lizenzart | Gibt an, ob das Modul als **pro Benutzer**, **pro Mandant** oder **pauschal** lizenziert ist. Davon hängt ab, ob Sie Wertzuweisungen pflegen müssen. |
| Zugewiesene Lizenzwerte | Zeigt an, wie viele Benutzer- oder Mandantenzuweisungen bereits aktiv hinterlegt sind. |
| Lizenzierte Werte | Gibt die maximal zulässige Anzahl von Zuweisungen an. |
| Gültig bis | Enddatum einer zeitlich begrenzten Lizenz, zum Beispiel bei einer Testlizenz. Nach Ablauf ist das Modul nicht mehr gültig. |
| Letzte Zahlung | Datum der zuletzt erfassten Zahlung laut Lizenzdaten. |
| Nächster Zahlungstag | Datum, zu dem die nächste Zahlung erwartet wird. |
| Überfällig | Kennzeichnet, ob das Modul zahlungsseitig im Rückstand ist. |
| Überfällig seit | Zeigt, seit wann der Zahlungsrückstand besteht. |
| Mahnstufe | Zeigt die aktuelle Mahnstufe des Moduls an. Mit steigender Mahnstufe wird aus dem Hinweis später eine Sperre. |

### Produkte mit Lizenzschlüssel pflegen
Die Seite **m+m Produkte** dient als weiterer Einstieg für die Schlüsselpflege. Sie ist besonders dann sinnvoll, wenn Sie die lizenzierten Module aus einem Produktkontext heraus aktualisieren möchten.

| Einrichtung | Erläuterung |
|---|---|
| Produkt-GUID | Eindeutige technische Kennung des Produkts. |
| Produktname | Bezeichnung des Produkts, dem der Lizenzschlüssel zugeordnet ist. |
| Lizenzschlüssel | Schlüssel des Produkts. Über **Eintrag aktualisieren/einfügen** lesen Sie die zugehörigen Moduldaten erneut ein. |

### Installierte m+m Apps prüfen
Auf der Seite **m+m Module** steht zusätzlich die Aktion **Installierte m+m Module anzeigen** zur Verfügung. Damit erhalten Sie eine Übersicht über die aktuell installierten Apps desselben Herausgebers. Die aktuelle App wird dabei ausgeblendet, damit Sie sich auf die übrigen installierten Module konzentrieren können.

Die Übersicht eignet sich für zwei Prüfungen:

1. Sie sehen, welche Apps technisch installiert sind.
2. Sie erkennen, für welche dieser Apps bereits ein Lizenzschlüssel hinterlegt ist.

| Feld | Erläuterung |
|---|---|
| App-ID | Technische Kennung der installierten App. |
| Lizenzschlüssel | Hinterlegter Schlüssel, sofern für die App bereits eine Lizenz gespeichert ist. |
| Lizenziert | Kennzeichnet, ob für die App bereits eine Lizenz in der Cloud Base hinterlegt ist. |
| Name | Anzeigename der installierten App. |

## Stammdaten
### Wertzuweisungen für Benutzer und Mandanten
Benutzer- und mandantenbezogene Lizenzen benötigen Einträge auf der Seite **m+m Lizenzwertzuweisung**. Die Seite wird in der Regel direkt aus einem Modul über die Aktion **Wertzuweisung** geöffnet. Dabei filtert das System bereits auf die passende **Lizenzart** und die **Modul-GUID**.

Für pauschale Lizenzen sind keine Zuweisungen vorgesehen. Das System lässt dafür keine sinnvolle Wertzuweisung zu.

| Feld | Erläuterung |
|---|---|
| Art | Lizenzart der Zuweisung. Zulässig sind **pro Benutzer** und **pro Mandant**. Die Option **pauschal** ist für Zuweisungen nicht erlaubt. |
| Nr. | Enthält den Bezug zur Zuweisung. Bei **pro Mandant** wählen Sie den Mandantennamen, bei **pro Benutzer** den Benutzernamen. Beim Ändern setzt das System die Zuweisung automatisch auf aktiv. |
| Zugeordnete Modul-GUID | Verknüpft die Zuweisung mit einem konkreten Modul. Das Feld ist Pflicht und darf nur Module zulassen, deren Lizenzart nicht **pauschal** ist. |
| Modulname | Zeigt den Namen des zugeordneten Moduls als Nachschlagewert an. |
| Aktiviert | Legt fest, ob die Zuweisung für die Lizenzprüfung berücksichtigt wird. Bei deaktivierter Zuweisung darf der betreffende Benutzer oder Mandant das Modul nicht verwenden. |

### Zulässige Werte und automatische Prüfungen
Bei der Pflege der Wertzuweisungen gelten feste Regeln:

1. Wenn Sie eine **Modul-GUID** auswählen, übernimmt das System automatisch die passende Lizenzart des Moduls.
2. Die Lizenzart **pauschal** darf nicht manuell als Zuweisung verwendet werden.
3. Die Anzahl aktiver Zuweisungen darf die im Modul hinterlegte Anzahl **Lizenzierte Werte** nicht überschreiten.
4. Für die Auswahl in **Nr.** verwendet das System je nach Lizenzart Benutzer oder Mandanten.

Damit bleibt die Zuweisung konsistent mit der Lizenzdefinition des jeweiligen Moduls.

## Profile und Zuordnungen
Ein eigenes Profilkonzept mit zusätzlichen Karten oder Ableitungsregeln enthält dieses Modul nicht. Die entscheidende Zuordnung erfolgt direkt über die Wertzuweisungen je Modul. Dadurch ist der fachliche Zusammenhang klar:

1. Das Modul bestimmt über **Lizenzart**, ob eine Zuordnung erforderlich ist.
2. Die Seite **m+m Lizenzwertzuweisung** bildet die erforderlichen Benutzer- oder Mandantenzuordnungen ab.
3. Die Lizenzprüfung verwendet nur aktivierte Zuweisungen.

## Tägliche Arbeit
### Module überwachen und nachpflegen
Die tägliche Arbeit findet überwiegend auf der Seite **m+m Module** statt. Dort prüfen Sie Lizenzstatus, Zahlungshinweise und Auslastung der verfügbaren Zuweisungen.

Gehen Sie in dieser Reihenfolge vor:

1. Öffnen Sie **m+m Module**.
2. Prüfen Sie, ob das gewünschte Modul bereits vorhanden ist.
3. Hinterlegen oder aktualisieren Sie bei Bedarf über **Eintrag aktualisieren/einfügen** den Lizenzschlüssel.
4. Kontrollieren Sie anschließend **Lizenzart**, **Lizenzierte Werte**, **Zugewiesene Lizenzwerte**, **Gültig bis** und **Mahnstufe**.
5. Öffnen Sie bei benutzer- oder mandantenbezogenen Lizenzen die Aktion **Wertzuweisung** und ergänzen oder korrigieren Sie die Zuweisungen.

### Wichtige Aktionen auf der Modulliste
| Aktion | Erläuterung |
|---|---|
| Eintrag aktualisieren/einfügen | Öffnet einen Dialog zur Eingabe des Lizenzschlüssels. Nach Bestätigung aktualisiert die App die Moduldaten aus dem Lizenzdienst. |
| Wertzuweisung | Öffnet die gefilterte Liste der Wertzuweisungen für das aktuelle Modul. |
| Installierte m+m Module anzeigen | Zeigt eine Übersicht der installierten m+m Apps desselben Herausgebers und markiert, ob bereits eine Lizenz hinterlegt ist. |

### Dialog zur Schlüsseleingabe
Bei der Aktion **Eintrag aktualisieren/einfügen** öffnet sich eine Eingabeseite. Dort übernimmt das System die Feldbezeichnung des Lizenzschlüssels als Beschriftung und zeigt den bisherigen Wert zur Bearbeitung an.

| Feld | Erläuterung |
|---|---|
| Eingabeaufforderung | Zeigt an, welcher Wert zu erfassen ist. Im Lizenzprozess ist dies der Lizenzschlüssel. |
| Eingabewert | Hier erfassen oder ersetzen Sie den Lizenzschlüssel. |

### Was das System nach der Aktualisierung prüft
Nach der Aktualisierung oder bei der Verwendung eines lizenzierten Moduls führt die App mehrere Prüfungen aus:

1. Die Lizenzdaten werden höchstens einmal pro Tag je Modul erneut geladen, sofern sich der Stand bereits für den aktuellen Tag im Speicher befindet.
2. Bei überfälligen Zahlungen zeigt das System Warnungen an. Ab einer höheren Mahnstufe wird daraus eine Sperre.
3. Wenn **Gültig bis** überschritten ist, gilt das Modul als nicht mehr gültig.
4. Bei **pro Benutzer** muss für den angemeldeten Benutzer eine aktive Zuweisung bestehen.
5. Bei **pro Mandant** muss für den aktuellen Mandanten eine aktive Zuweisung bestehen.
6. Bei **pauschal** ist keine zusätzliche Zuweisung nötig.

## Historie und Nachverfolgung
Dieses Modul enthält keine eigene Historienliste, kein Archiv und kein Versand- oder Druckprotokoll. Die Nachverfolgung erfolgt direkt über die aktuellen Felder in den Lizenzlisten:

1. **Letzte Zahlung**, **Nächster Zahlungstag**, **Überfällig**, **Überfällig seit** und **Mahnstufe** zeigen den aktuellen Zahlungs- und Erinnerungsstatus.
2. **Gültig bis** zeigt das Ende einer befristeten Lizenz.
3. **Zugewiesene Lizenzwerte** im Verhältnis zu **Lizenzierte Werte** zeigt die aktuelle Auslastung.

## FAQ und Troubleshooting
### 1. Warum kann ein Benutzer ein Modul trotz vorhandener Lizenz nicht verwenden?
Wenn die Lizenzart **pro Benutzer** ist, muss auf der Wertzuweisung eine aktive Zeile für diesen Benutzer vorhanden sein. Fehlt die Zeile oder ist **Aktiviert** ausgeschaltet, schlägt die Lizenzprüfung fehl.

### 2. Warum kann ein Mandant ein Modul nicht nutzen?
Bei der Lizenzart **pro Mandant** muss der Mandantenname als aktive Wertzuweisung hinterlegt sein. Ohne diesen Eintrag wird der Mandant als nicht zugeordnet behandelt.

### 3. Warum lässt sich keine Wertzuweisung für eine pauschale Lizenz anlegen?
Die App verbietet Wertzuweisungen für die Lizenzart **pauschal**. Diese Lizenzform gilt ohne Benutzer- oder Mandantenzuordnung.

### 4. Warum erscheint beim Zuweisen eine Meldung zur maximalen Anzahl?
Die Zahl aktiver Zuweisungen darf den Wert in **Lizenzierte Werte** nicht überschreiten. Sobald mehr Benutzer oder Mandanten zugewiesen werden sollen als erlaubt, blockiert das System den Vorgang.

### 5. Warum wird die Zuweisung beim Erfassen der Nr. sofort aktiviert?
Beim Validieren der **Nr.** setzt die App das Feld **Aktiviert** automatisch auf eingeschaltet. So wird der neue Eintrag direkt in der Lizenzprüfung berücksichtigt.

### 6. Warum ändert sich die Art der Wertzuweisung automatisch?
Beim Eintragen der **Zugeordneten Modul-GUID** liest das System die Lizenzart des Moduls und übernimmt diesen Wert. Dadurch kann keine unpassende Art gespeichert werden.

### 7. Warum wird ein Modul trotz Lizenz mit Warnhinweisen angezeigt?
Warnhinweise entstehen bei Zahlungsrückständen. Die Felder **Überfällig** und **Mahnstufe** zeigen an, dass das Modul zwar noch vorhanden ist, aber eine Zahlung offen ist.

### 8. Was passiert, wenn das Datum in Gültig bis überschritten ist?
Dann gilt das Modul als nicht mehr gültig. Die Lizenzprüfung bewertet das Modul als abgelaufen.

### 9. Warum aktualisieren sich die Lizenzdaten nicht bei jedem Aufruf erneut?
Die App merkt sich, ob die Lizenzdaten für ein Modul bereits am aktuellen Tag geladen wurden. Dadurch werden unnötige Mehrfachabfragen vermieden.

### 10. Was passiert mit Zuweisungen, wenn ein Benutzer oder ein Mandant gelöscht wird?
Benutzer- und Mandantenzuweisungen werden automatisch bereinigt. Bei geänderten Benutzern aktualisiert das System außerdem den Aktivstatus entsprechend dem Benutzerstatus.

## Typische Anwendungsfälle
### Lizenz für ein neu erworbenes Modul aktivieren
**Auslöser:** Ihr Unternehmen hat ein zusätzliches m+m Modul erworben und den Lizenzschlüssel erhalten.

**Einstieg in BC:** Öffnen Sie über **Suchen** die Seite **m+m Module** oder **m+m Produkte**.

**Kernablauf:** Wählen Sie **Eintrag aktualisieren/einfügen**, erfassen Sie den Lizenzschlüssel und bestätigen Sie den Dialog. Das System lädt die Moduldaten nach. Prüfen Sie danach auf der Modulliste die Felder **Lizenzart**, **Lizenzierte Werte**, **Gültig bis** und gegebenenfalls **Mahnstufe**.

**Abschluss:** Falls die Lizenzart **pro Benutzer** oder **pro Mandant** lautet, öffnen Sie anschließend **Wertzuweisung** und ergänzen die erforderlichen Zuordnungen.

### Benutzer für eine benutzerbezogene Lizenz freischalten
**Auslöser:** Ein weiterer Mitarbeiter soll ein bereits lizenziertes Modul verwenden.

**Einstieg in BC:** Öffnen Sie **m+m Module**, markieren Sie das Modul und rufen Sie **Wertzuweisung** auf.

**Kernablauf:** Legen Sie eine neue Zeile an, wählen Sie in **Nr.** den Benutzernamen und prüfen Sie, ob **Aktiviert** gesetzt ist. Die App übernimmt die Lizenzart aus dem Modul und verhindert unzulässige Kombinationen.

**Abschluss:** Kontrollieren Sie auf der Modulliste, ob **Zugewiesene Lizenzwerte** noch innerhalb von **Lizenzierte Werte** liegt.

### Mandant für eine mandantenbezogene Lizenz freischalten
**Auslöser:** Ein zusätzliches Unternehmen im System soll ein vorhandenes Modul nutzen.

**Einstieg in BC:** Öffnen Sie **m+m Module** und wechseln Sie über **Wertzuweisung** in die Zuweisungsliste des Moduls.

**Kernablauf:** Erfassen Sie eine neue Zeile mit dem Mandantennamen in **Nr.**. Die App verwendet dafür automatisch die Lizenzart **pro Mandant** des Moduls. Aktivieren Sie die Zeile, falls dies nicht bereits geschehen ist.

**Abschluss:** Testen Sie die Nutzung im betreffenden Mandanten. Bei fehlender Zuweisung würde die Lizenzprüfung den Zugriff ablehnen.

### Lizenzstatus installierter Apps prüfen
**Auslöser:** Sie möchten nachvollziehen, welche installierten m+m Apps bereits lizenziert sind.

**Einstieg in BC:** Öffnen Sie **m+m Module** und wählen Sie **Installierte m+m Module anzeigen**.

**Kernablauf:** Vergleichen Sie in der Übersicht die Felder **Lizenziert**, **Lizenzschlüssel** und **Name**. So erkennen Sie schnell, für welche installierten Apps bereits ein gültiger Eintrag vorhanden ist.

**Abschluss:** Wechseln Sie bei Bedarf zurück in **m+m Module**, um fehlende Lizenzschlüssel nachzutragen oder vorhandene Einträge zu aktualisieren.
