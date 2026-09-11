---
title: Anwenderhandbuch m+m Production Order Assistant with Package Management
---

# Anwenderhandbuch m+m Production Order Assistant with Package Management

## Einleitung

Die App **m+m Production Order Assistant with Package Management** verbindet zwei m+m-Apps auf der **Verkaufszeile**: den **m+m Production Order Assistant** (Feld **FA erstellen**) und das **m+m Package Management** (Feld **Packmittelstatus**). Sie sorgt dafür, dass Verkaufszeilen, die ein Packmittel abbilden, automatisch von der Fertigungsauftragserstellung ausgenommen werden.

Ohne diese Verbindung würde der Fertigungsassistent auch für eine Packmittelzeile versuchen, einen **Fertigungsauftrag** anzulegen, obwohl diese Zeile kein zu fertigender Artikel, sondern ein Verpackungsobjekt ist. Diese App verhindert das: Sobald eine Verkaufszeile den **Packmittelstatus** **Packmittel** erhält, wird auf derselben Zeile das Kennzeichen **FA erstellen** zurückgesetzt.

Die App arbeitet **regelbasiert im Hintergrund**. Sie bringt **keine eigenen Seiten, Aktionen, Einrichtungs- oder Stammdatentabellen** mit. Alle sichtbaren Felder gehören zu den beiden verbundenen Apps und erscheinen dort, wo diese Apps sie einblenden — auf der Verkaufszeile im **Verkaufsauftrag**.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender im Verkauf**, die täglich **Verkaufsaufträge** erfassen und **Verkaufszeilen** bearbeiten — insbesondere dort, wo dieselbe Verkaufszeile sowohl als Fertigungsauslöser (**FA erstellen**) als auch als Packmittel (**Packmittelstatus**) auftreten kann. Sekundäre Zielgruppe sind **Administratoren**, die die Voraussetzungen schaffen: Installation der beiden Basis-Apps und Zuweisung der Berechtigungen.

### Kurzer Prozessüberblick

1. Der Anwender legt im **Verkaufsauftrag** eine **Verkaufszeile** an oder ändert sie.
2. Das **m+m Package Management** ermittelt für diese Zeile den **Packmittelstatus** (**(leer)**, **Teilweise**, **Voll** oder **Packmittel**).
3. Diese App prüft bei jedem Einfügen und Ändern der Verkaufszeile: Ist der **Packmittelstatus** = **Packmittel**, wird **FA erstellen** auf der Zeile automatisch deaktiviert.
4. Beim **Freigeben** des Verkaufsauftrags erstellt der **m+m Production Order Assistant** nur noch für Zeilen mit gesetztem **FA erstellen** einen **Fertigungsauftrag** — Packmittelzeilen bleiben dabei außen vor.

## Schnellstart für Anwender

Die App benötigt im Tagesgeschäft **keine Bedienung**. Die folgenden Schritte zeigen, wie sich ihr Verhalten im gewohnten Ablauf des Verkaufsauftrags äußert.

1. **Voraussetzung (einmalig durch den Administrator):** Die Apps **m+m Production Order Assistant** und **m+m Package Management** sind installiert, und der Berechtigungssatz **MuM PAPM All** ist den betroffenen Anwendern zugewiesen (siehe **Einrichtung**).
2. Öffnen Sie den **Verkaufsauftrag** und erfassen Sie in der Unterseite **Zeilen** eine **Verkaufszeile** (Feld **Art** = **Artikel**, **Nr.**, **Menge**).
3. Setzen Sie bei zu fertigenden Artikeln das Kennzeichen **FA erstellen** auf der Zeile.
4. Weisen Sie Packmittel wie gewohnt über das **m+m Package Management** zu. Erhält die Zeile dadurch den **Packmittelstatus** **Packmittel**, wird **FA erstellen** auf dieser Zeile automatisch entfernt — ein Eingreifen ist nicht nötig.
5. Wählen Sie im Verkaufsauftrag **Freigeben**. Der **m+m Production Order Assistant** legt **Fertigungsaufträge** nur für Zeilen mit gesetztem **FA erstellen** an; Packmittelzeilen werden nicht als Fertigungsauftrag angelegt.

## Einrichtung

Diese App hat **keine eigene Einrichtungsseite** und **keine eigenen Einrichtungsfelder**. Es gibt in dieser App weder eine Nummernserie noch Report- oder Mailparameter. Die gesamte Einrichtung besteht aus zwei administrativen Voraussetzungen und der Berechtigungsvergabe. Die fachlichen Einrichtungsseiten liegen in den verbundenen Apps und werden in deren Handbüchern gepflegt; die für das Zusammenspiel wesentlichen Felder sind hier beschrieben.

### Voraussetzungen und Aktivierung einrichten

**Wer richtet ein:** Der Administrator. **Wann:** Vor der ersten Nutzung, bevor Verkaufszeilen mit Packmitteln und Fertigungsauftragskennzeichen bearbeitet werden. **Welcher Prozess wird ermöglicht:** Das automatische Ausschließen von Packmittelzeilen aus der Fertigungsauftragserstellung im Verkaufsauftrag (siehe **Tägliche Arbeit im Verkaufsauftrag**).

Die App ist eine Brücke zwischen zwei Apps. Sie greift nur, wenn beide vorhanden sind und die auslösenden Felder auf der Verkaufszeile bestehen. Richten Sie die Voraussetzungen in Abhängigkeitsreihenfolge ein:

1. **m+m Package Management installieren.** Wenn diese App installiert ist, existiert auf der Verkaufszeile das Feld **Packmittelstatus**; erst dadurch kann eine Zeile den Wert **Packmittel** annehmen, den diese Brücke auswertet. Ohne diese App gibt es keinen **Packmittelstatus** und die Brücke bleibt wirkungslos.
2. **m+m Production Order Assistant installieren.** Wenn diese App installiert ist, existiert auf der Verkaufszeile das Feld **FA erstellen**; erst dadurch entscheidet ein Kennzeichen pro Zeile, ob beim Freigeben ein **Fertigungsauftrag** entsteht. Ohne dieses Feld gibt es nichts, das die Brücke zurücksetzen könnte.
3. **Diese App (m+m Production Order Assistant with Package Management) installieren.** Wenn beide Voraussetzungen erfüllt sind und diese App installiert ist, dann wird die Regel aktiv: Bei jedem Einfügen oder Ändern einer Verkaufszeile mit **Packmittelstatus** = **Packmittel** wird **FA erstellen** deaktiviert.
4. **Fertigungsauftragserstellung im Verkauf konfigurieren.** Legen Sie in der Seite **Fertigungsassistent Einrichtung** fest, wie und in welchem Status der **m+m Production Order Assistant** beim Freigeben Fertigungsaufträge erzeugt. Diese Einrichtung steuert den nachgelagerten Schritt, aus dem die Brücke die Packmittelzeilen heraushält.

**Operativer Abschluss der Kette:** Die Regel benötigt im Tagesgeschäft keine gesonderte Aktion. Sie wird jedes Mal automatisch ausgeführt, wenn der Anwender im Verkaufsauftrag eine Verkaufszeile mit **Packmittelstatus** = **Packmittel** einfügt oder ändert (siehe **Tägliche Arbeit im Verkaufsauftrag**).

### Berechtigungen einrichten

**Wer richtet ein:** Der Administrator. **Wann:** Nach der Installation, vor der Nutzung. **Zweck:** Der Berechtigungssatz bestimmt, welche Anwender die von dieser App bereitgestellten Objekte ausführen dürfen.

Weisen Sie den Anwendern den mitgelieferten Berechtigungssatz zu. Der Satz **MuM PAPM All** legt die Ausführungsrechte für die beiden Verarbeitungsobjekte dieser App fest.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Berechtigungssatz **MuM PAPM All** | Wenn dieser Satz einem Anwender oder einer Rolle zugewiesen ist, dann darf dieser Anwender die Hintergrundverarbeitung dieser App ausführen; ohne die Zuweisung greift die automatische Regel für diesen Anwender nicht, weil die zugehörigen Objekte nicht ausgeführt werden dürfen. Der Satz ist zuweisbar und umfasst ausschließlich die beiden Verarbeitungs-Codeunits dieser App. |

Die App enthält keine weiteren berechtigungsrelevanten Einrichtungsfelder. Die Berechtigungen auf **Verkaufszeile**, **Packmittelstatus** und **FA erstellen** selbst werden über die Basis-App und die beiden verbundenen Apps gesteuert.

## Tägliche Arbeit im Verkaufsauftrag

Diese App wirkt ausschließlich auf der **Verkaufszeile** im **Verkaufsauftrag**. Sie stellt keine eigene Seite dar; die beiden relevanten Felder werden durch die verbundenen Apps in die Unterseite **Zeilen** des Verkaufsauftrags eingeblendet. Steuernde Vorbedingungen liegen in der Einrichtung der verbundenen Apps: Das Feld **Packmittelstatus** wird durch das **m+m Package Management** aus der Packmittelzuweisung abgeleitet, das Feld **FA erstellen** und die Erzeugung von Fertigungsaufträgen werden über die **Fertigungsassistent Einrichtung** gesteuert (siehe **Voraussetzungen und Aktivierung einrichten**).

**Einstieg:** Öffnen Sie über die Aktion **Freigeben** bzw. über die Liste **Verkaufsaufträge** den gewünschten **Verkaufsauftrag** und arbeiten Sie in der Unterseite **Zeilen**.

### Felder auf der Verkaufszeile

Die folgenden Felder steuern das Zusammenspiel. Beide erscheinen auf derselben Verkaufszeile.

| Feld | Erläuterung |
|------|-------------|
| **FA erstellen** | Wenn dieses Kennzeichen auf einer Verkaufszeile gesetzt ist, dann legt der **m+m Production Order Assistant** beim Freigeben des Verkaufsauftrags für diese Zeile einen **Fertigungsauftrag** an. Ist es nicht gesetzt, entsteht für diese Zeile kein Fertigungsauftrag. Diese App setzt das Kennzeichen automatisch zurück, sobald die Zeile den **Packmittelstatus** **Packmittel** trägt. |
| **Packmittelstatus** | Wenn dieses Feld auf einer Verkaufszeile einen Wert trägt, dann zeigt es an, in welchem Umfang der Zeile Packmittel zugeordnet sind. Das Feld ist nicht direkt editierbar; das **m+m Package Management** setzt den Wert automatisch aus der Packmittelzuweisung. Erreicht der Wert **Packmittel**, deaktiviert diese App auf derselben Zeile das Kennzeichen **FA erstellen**. |
| **Packmittelreferenz Nr.** | Wenn hier eine Referenz eingetragen ist, dann verknüpft das **m+m Package Management** die Verkaufszeile mit dem zugehörigen Packmittelbeleg; die Zuordnung wird bei Eingabe und über die Auswahl geprüft. Das Feld gehört zum **m+m Package Management** und beeinflusst, welchen **Packmittelstatus** die Zeile erhält. |

Die Werte des Feldes **Art** und die weiteren Standardfelder der Verkaufszeile (**Nr.**, **Beschreibung**, **Menge**) gehören zur Standard-Verkaufszeile von Business Central und werden hier nur genannt, soweit sie für den Ablauf nötig sind: Ein **Fertigungsauftrag** entsteht durch den **m+m Production Order Assistant** nur für Zeilen mit **Art** = **Artikel** und gesetztem **FA erstellen**.

### Bedeutung der Werte im Feld Packmittelstatus

Das Feld **Packmittelstatus** ist ein Optionsfeld des **m+m Package Management**. Für diese App ist entscheidend, dass nur der Wert **Packmittel** die automatische Deaktivierung von **FA erstellen** auslöst. Alle Werte:

- **(leer):** Der Zeile sind keine Packmittel zugeordnet. Die Zeile wird von dieser App **nicht** verändert; ein gesetztes **FA erstellen** bleibt erhalten.
- **Teilweise:** Der Zeile sind Packmittel nur für einen Teil der Menge zugeordnet. Die Zeile gilt nicht als reine Packmittelzeile; diese App verändert **FA erstellen** **nicht**.
- **Voll:** Der Zeile sind Packmittel für die gesamte Menge zugeordnet, sie bleibt jedoch eine Artikelzeile. Diese App verändert **FA erstellen** **nicht**.
- **Packmittel:** Die Zeile bildet selbst ein Packmittel ab. In diesem Fall setzt diese App beim Einfügen und Ändern der Zeile das Kennzeichen **FA erstellen** auf **Nein**, damit für diese Zeile kein Fertigungsauftrag erzeugt wird.

### Buchungs- bzw. Freigabeablauf

Der Fertigungsauftrag entsteht nicht durch diese App, sondern durch den **m+m Production Order Assistant** beim Freigeben des Verkaufsauftrags. Diese App greift ausschließlich vorbereitend in die Verkaufszeile ein. Der Ablauf im Zusammenspiel:

1. Wählen Sie die Zeile im **Verkaufsauftrag** (Unterseite **Zeilen**).
2. Ordnen Sie über das **m+m Package Management** Packmittel zu bzw. tragen Sie eine **Packmittelreferenz Nr.** ein. Wird die Zeile dadurch zur Packmittelzeile, erhält sie den **Packmittelstatus** **Packmittel**.
3. Beim Einfügen und Ändern der Zeile setzt diese App bei **Packmittelstatus** = **Packmittel** das Kennzeichen **FA erstellen** automatisch auf **Nein**.
4. Wählen Sie die Aktion **Freigeben** im Verkaufsauftrag.
5. Der **m+m Production Order Assistant** legt für alle Zeilen mit gesetztem **FA erstellen** einen **Fertigungsauftrag** an. Packmittelzeilen sind durch Schritt 3 ausgenommen.

Diese App zeigt bei diesem Ablauf **keine Meldung** und **keinen Bestätigungsdialog** an; die Deaktivierung von **FA erstellen** erfolgt unbemerkt im Hintergrund. Ob die Fertigungsauftragserstellung beim Freigeben mit oder ohne Rückfrage erfolgt und in welchem Status der Fertigungsauftrag angelegt wird, steuert die **Fertigungsassistent Einrichtung** des **m+m Production Order Assistant**.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie sich die App im gewohnten Verkaufsablauf auswirkt. Alle Schritte beziehen sich auf Standard-Business-Central-Seiten und die Felder der verbundenen Apps.

### Verkaufsauftrag mit Fertigungsartikel und Packmittel

**Auslöser:** Ein Kunde bestellt telefonisch einen zu fertigenden Artikel; zusätzlich soll eine Verpackung als eigene Position erfasst werden.

**Einstieg in BC:** Der Anwender öffnet die Liste **Verkaufsaufträge**, legt einen neuen **Verkaufsauftrag** an und wechselt in die Unterseite **Zeilen**.

**Kernablauf:**
1. Der Anwender erfasst die erste Zeile mit dem zu fertigenden **Artikel** (**Art** = **Artikel**, **Nr.**, **Menge**) und setzt **FA erstellen**.
2. Er erfasst eine zweite Zeile für die Verpackung und ordnet ihr über das **m+m Package Management** Packmittel zu; diese Zeile erhält dadurch den **Packmittelstatus** **Packmittel**.
3. Beim Speichern dieser zweiten Zeile entfernt diese App automatisch ein etwaig gesetztes **FA erstellen** auf der Packmittelzeile.
4. Der Anwender wählt **Freigeben**.

**Abschluss:** Der **m+m Production Order Assistant** erstellt ausschließlich für die Artikelzeile einen **Fertigungsauftrag**. Für die Packmittelzeile entsteht kein Fertigungsauftrag.

### Nachträgliche Packmittelzuweisung auf einer bereits gekennzeichneten Zeile

**Auslöser:** Eine Verkaufszeile war zunächst als Fertigungsartikel mit **FA erstellen** vorgesehen; im Nachgang wird die Zeile per Packmittelzuweisung als Packmittel eingestuft.

**Einstieg in BC:** Der Anwender öffnet den betroffenen **Verkaufsauftrag** aus der Liste **Verkaufsaufträge** und die Unterseite **Zeilen**.

**Kernablauf:**
1. Auf der Zeile ist **FA erstellen** bereits gesetzt.
2. Der Anwender ordnet über das **m+m Package Management** Packmittel zu bzw. trägt die **Packmittelreferenz Nr.** ein; die Zeile wechselt auf **Packmittelstatus** **Packmittel**.
3. Da die Zeile beim Speichern geändert wird, greift die Regel dieser App: **FA erstellen** wird auf **Nein** gesetzt.

**Abschluss:** Beim späteren **Freigeben** wird für diese Zeile kein **Fertigungsauftrag** mehr angelegt, obwohl das Kennzeichen ursprünglich gesetzt war.

## FAQ und Troubleshooting

### 1. Warum wird für eine Verkaufszeile kein Fertigungsauftrag angelegt?

Prüfen Sie den **Packmittelstatus** der Zeile. Steht dort **Packmittel**, hat diese App das Kennzeichen **FA erstellen** automatisch deaktiviert; für Packmittelzeilen entsteht bewusst kein **Fertigungsauftrag**.

### 2. Warum lässt sich das Kennzeichen FA erstellen auf einer Packmittelzeile nicht dauerhaft setzen?

Sobald die Zeile mit **Packmittelstatus** = **Packmittel** eingefügt oder geändert wird, setzt diese App **FA erstellen** wieder auf **Nein**. Das ist beabsichtigt: Eine Packmittelzeile soll keinen Fertigungsauftrag auslösen.

### 3. Was passiert, wenn eine Zeile den Packmittelstatus Voll oder Teilweise hat?

In diesen Fällen greift die Regel dieser App **nicht**. Nur der Wert **Packmittel** löst die Deaktivierung von **FA erstellen** aus. Bei **Voll** oder **Teilweise** bleibt ein gesetztes **FA erstellen** erhalten.

### 4. Muss ich die App im Tagesgeschäft bedienen?

Nein. Die App hat keine eigene Seite und keine Aktion. Sie prüft bei jedem Einfügen und Ändern einer Verkaufszeile automatisch den **Packmittelstatus**.

### 5. Warum sehe ich keine eigene Einrichtungsseite der App?

Die App bringt bewusst keine Einrichtung mit. Sie steuert sich vollständig über den **Packmittelstatus** der Verkaufszeile. Konfiguriert wird ausschließlich in den verbundenen Apps (**m+m Package Management** und **m+m Production Order Assistant**).

### 6. Wann genau wird FA erstellen zurückgesetzt?

Beim **Einfügen** einer neuen Verkaufszeile und beim **Ändern** einer bestehenden Verkaufszeile — jeweils genau dann, wenn der **Packmittelstatus** der Zeile den Wert **Packmittel** hat.

### 7. Kann ich das automatische Zurücksetzen für einzelne Zeilen abschalten?

Nein. Die Regel gilt einheitlich für alle Verkaufszeilen mit **Packmittelstatus** = **Packmittel**. Eine zeilenweise Ausnahme ist nicht vorgesehen.

### 8. Warum passiert nichts, obwohl ich Packmittel zugewiesen habe?

Prüfen Sie, ob die Zeile tatsächlich den **Packmittelstatus** **Packmittel** erreicht hat. Bei nur teilweiser Zuordnung steht dort **Teilweise** oder **Voll**, und die Regel greift nicht. Der **Packmittelstatus** wird vom **m+m Package Management** aus der Zuordnung abgeleitet.

### 9. Welche Berechtigung wird für die App benötigt?

Weisen Sie den Anwendern den Berechtigungssatz **MuM PAPM All** zu. Ohne diese Berechtigung darf die Verarbeitung dieser App nicht ausgeführt werden und die Regel greift für den betroffenen Anwender nicht.

### 10. Funktioniert die App ohne die beiden verbundenen Apps?

Nein. Ohne **m+m Package Management** existiert kein **Packmittelstatus**, und ohne **m+m Production Order Assistant** existiert kein Feld **FA erstellen**. Beide Apps sind Voraussetzung; erst mit ihnen wird die Brücke wirksam.
