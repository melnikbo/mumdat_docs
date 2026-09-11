---
title: Anwenderhandbuch m+m Calculation with Aided Data Management
---

# Anwenderhandbuch m+m Calculation with Aided Data Management

## Einleitung

Das Modul **m+m Calculation with Aided Data Management** verbindet die m+m Kalkulation mit der regelbasierten Datenverwaltung (Regeln und Regelabläufe). Es erlaubt, einzelne Werte in einer **Kalkulation** nicht mehr nur manuell oder über eine **Formel** zu bestimmen, sondern automatisch durch einen hinterlegten **Regelablauf** setzen zu lassen. Damit lassen sich Zu- und Abschläge, Basiswerte und alternative Werte einer Kalkulationszeile abhängig von Artikel, Materialart, Eigenschaften oder anderen Bedingungen ermitteln, ohne dass der Anwender die Werte bei jeder Kalkulation von Hand pflegt.

**Zielgruppe:** Primär richtet sich das Modul an **operative Anwender im Vertrieb und in der Kalkulation**, die im Tagesgeschäft eine **Kalkulation** zu einem Verkaufsangebot oder Verkaufsauftrag erzeugen und neu berechnen. Für sie läuft die Regelverarbeitung im Hintergrund; sie sehen das Ergebnis als automatisch gesetzten **Wert** in der Kalkulationszeile. Sekundär angesprochen sind **Key-User und Administratoren**, die die **Kalkulationsvorlage** und die **Regeln** einrichten: Sie legen fest, welche Zeile durch welche Regel gefüllt wird.

**Kurzer Prozessüberblick:** Ein Administrator markiert in der **Kalkulationsvorlage** eine Zeile mit der **Feldart** **Regel** und hinterlegt zur Vorlage einen **Regelablauf**. In der regelbasierten Datenverwaltung definiert er eine **Regel** der **Regelart** **Kalk.-Zeilenwert setzen**, verknüpft sie mit der Vorlagenzeile und legt fest, welche Wertfelder gesetzt werden. Erzeugt der Anwender später eine **Kalkulation** mit dieser Vorlage und berechnet sie neu, verarbeitet das Modul den **Regelablauf** automatisch und schreibt die Ergebnisse in die betreffende Kalkulationszeile.

Dieses Modul liefert **keine** eigene Einrichtungsseite, keine eigenen Listen und keine eigenen Berichte. Es erweitert ausschließlich die **Kalkulationsvorlage** aus der m+m Kalkulation und die **Regel** aus der regelbasierten Datenverwaltung um die zur Kopplung nötigen Felder und Aktionen. Alle Screens, die dieses Handbuch beschreibt, sind erweiterte Basis-Seiten dieser beiden Module.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zum automatisch berechneten Wert. Die Einrichtungsschritte (1–4) führt ein Administrator oder Key-User einmalig durch; die Schritte im Tagesgeschäft (5–7) betreffen den operativen Anwender.

1. **Kalkulationsvorlage vorbereiten:** Öffnen Sie über **Suchen** die Liste **Kalkulationsvorlagen** und öffnen Sie die gewünschte **Kalkulationsvorlage**. Setzen Sie in der Zeile, deren Wert automatisch bestimmt werden soll, die **Feldart** auf **Regel**. Dadurch werden **Wert** und **Alt. Wert 1** bis **Alt. Wert 4** dieser Zeile auf 0 gesetzt und für die manuelle Eingabe gesperrt — die Zeile wird künftig durch die Regelverarbeitung gefüllt.
2. **Regelablauf zur Vorlage anlegen:** Wählen Sie auf der **Kalkulationsvorlage** die Aktion **Regelablauf**. Beim ersten Aufruf wird der Vorlage automatisch ein leerer **Regelablauf** zugeordnet und geöffnet.
3. **Regel definieren:** Öffnen Sie über **Suchen** die Liste **Regeln** und legen Sie eine **Regel** an. Setzen Sie die **Regelart** auf **Kalk.-Zeilenwert setzen**. Es erscheint die Gruppe **Kalkulation**: Tragen Sie dort den **Kalkulationsvorlagencode** und die **Kalkulationsvorlagenzeile** ein und wählen Sie über **Wert setzen** / **Alt. Wert 1 setzen** … die Zielfelder. Pflegen Sie das Ergebnis der Regel bei Bedarf über die Aktion **Matrix**.
4. **Regel in den Regelablauf aufnehmen:** Nehmen Sie die Regel als Schritt in den in Schritt 2 geöffneten **Regelablauf** auf (Zeilenart **Regel**, Feld **Regelcode**). Optional steuern Sie die Ausführung über **Wenn (Wahr)** / **Wenn (Falsch)** / **Wenn (Vergleich)**, **Sonst** und **Ende**.
5. **Kalkulation erzeugen:** Erstellen Sie im Tagesgeschäft aus der Verkaufszeile eine **Kalkulation** und wählen Sie dieselbe **Kalkulationsvorlage**.
6. **Neu berechnen:** Lösen Sie die Neuberechnung der Kalkulation aus (Status **In Entwicklung**). Vor der Zeilenberechnung verarbeitet das Modul den **Regelablauf** der Vorlage automatisch.
7. **Ergebnis prüfen:** Kontrollieren Sie in der Kalkulationszeile mit **Feldart** **Regel** den gesetzten **Wert** (bzw. **Alt. Wert 1**–**4**). Er wurde durch die Regel bestimmt und ist nicht manuell editierbar.

> Es gibt in diesem Modul keinen eigenen Buchungs- oder Freigabelauf. Der einzige auslösende Vorgang ist die **Neuberechnung** der Kalkulation.

## Einrichtung

Die Einrichtung dieses Moduls besteht nicht aus einer eigenen Einrichtungskarte, sondern aus zwei zusammenwirkenden Konfigurationsflächen der Basismodule: der **Kalkulationsvorlage** (m+m Kalkulation) und der **Regel** (regelbasierte Datenverwaltung). Beide werden hier vollständig für den in diesem Modul relevanten Teil beschrieben, damit der Screen ohne ein weiteres Handbuch konfiguriert werden kann.

### Kalkulationsvorlage: Zeile als Regel-Ziel kennzeichnen

**Wer/wann:** Ein Administrator oder Key-User bereitet die **Kalkulationsvorlage** einmalig vor, bevor Anwender Kalkulationen mit dieser Vorlage rechnen. Die hier gesetzten Kennzeichen entscheiden, welche Zeilen der späteren Kalkulation durch die Regelverarbeitung gefüllt werden statt durch manuelle Eingabe oder Formel.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Kalkulationsvorlagen** und öffnen Sie die gewünschte **Kalkulationsvorlage** (Karte). Die Vorlagenzeilen bearbeiten Sie im Unterformular der Karte.

Die folgende Tabelle beschreibt die für dieses Modul steuernden Felder der Vorlagenzeile. Die **Feldart** ist das zentrale Feld dieses Moduls; die übrigen Felder gehören zur Basis-Kalkulationsvorlage und bestimmen, wie die Zeile ohne Regel gerechnet würde.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Beschreibung** | Wenn Sie einen Text erfassen, erscheint er als Bezeichnung der Zeile in der späteren Kalkulation; er erleichtert dem Anwender das Wiedererkennen der regelgesteuerten Zeile. |
| **Feldart** | Wenn Sie den Wert **Regel** wählen, wird diese Zeile nicht mehr manuell oder per Formel bewertet, sondern durch die Regelverarbeitung gesetzt; **Wert** und **Alt. Wert 1**–**4** werden dabei sofort auf 0 gesetzt und gesperrt. Bei den übrigen Feldarten bleibt die Standard-Kalkulationslogik aktiv. Werte siehe Aufstellung unter der Tabelle. |
| **Berechneter Wert** | Wenn Sie einen berechneten Wert zuordnen, fließt das Zeilenergebnis in die entsprechende Kostenkategorie der Kalkulation (z. B. Materialkosten) ein; steuert, in welchen Summenblock der ermittelte Betrag eingeht. |
| **Berechnungsbasis** | Wenn Sie eine Basiszeile angeben, wird der Zeilenwert prozentual auf das Ergebnis dieser Basiszeile bezogen; ohne Basis wirkt der Wert absolut. |
| **Formel** | Wenn Sie eine Formel hinterlegen, berechnet die Zeile ihren Wert aus anderen Zeilennummern; dieses Feld ist nur bei einer Formel-Feldart aktiv und steht in Konkurrenz zur Regelsteuerung — für regelgesteuerte Zeilen verwenden Sie die **Feldart** **Regel** statt einer Formel. |
| **Wert** | Wenn Sie hier bei einer manuellen Feldart einen Betrag eintragen, wird er direkt als Zeilenwert verwendet. Bei **Feldart** **Regel** wird das Feld auf 0 gesetzt und durch die Regel überschrieben. |
| **Alt. Wert 1** … **Alt. Wert 4** | Wenn Sie alternative Werte pflegen, stehen der Kalkulation zusätzliche Wertspalten (z. B. für Varianten oder Staffeln) zur Verfügung. Bei **Feldart** **Regel** werden auch diese Felder auf 0 gesetzt und können durch die Regel gefüllt werden. |
| **Fixer Wert** | Wenn aktiviert, bleibt der Zeilenwert bei einer Neuberechnung unverändert erhalten; ohne das Kennzeichen wird der Wert bei jeder Berechnung neu ermittelt. |
| **Im Hundert** | Wenn aktiviert, wird der Prozentsatz „im Hundert“ (auf den Bruttobetrag) statt „vom Hundert“ gerechnet; beeinflusst die Höhe des ermittelten Zuschlags. |
| **Verwendungsart** | Wenn Sie einer Zeile eine Verwendungsart zuweisen, kennzeichnet sie deren besondere Rolle in der Kalkulation; eine Verwendungsart ist je Vorlage nur einmal vergeben und wird beim erneuten Setzen automatisch von der bisherigen Zeile entfernt. |

**Werte der Feldart (Auszug — für dieses Modul relevant):**

- **Regel:** Der durch dieses Modul ergänzte Wert. Wenn gewählt, wird die Zeile zur Zielzeile eines Regelablaufs; **Wert** und **Alt. Wert 1**–**4** werden auf 0 gesetzt und gesperrt und ausschließlich durch die verknüpfte Regel gefüllt.
- Alle weiteren Feldarten der Basis-Kalkulationsvorlage (z. B. **Berechneter Wert**) bleiben unverändert verfügbar und rechnen nach der Standardlogik der m+m Kalkulation. Für die regelgesteuerte Automatik ist ausschließlich der Wert **Regel** maßgeblich.

> Die vollständige fachliche Bedeutung aller Kalkulationsfelder (Kostenkategorien, mehrstufige Kalkulation, Zertifizierung) ist Bestandteil der m+m Kalkulation. Für dieses Modul ist entscheidend: Nur Zeilen mit **Feldart** **Regel** werden durch den Regelablauf bedient.

**Prozessschritt:** Zuerst legen Sie in der **Kalkulationsvorlage** fest, *welche* Zeile regelgesteuert ist (**Feldart** **Regel**); danach ordnen Sie der Vorlage über die Aktion **Regelablauf** einen Ablauf zu (siehe nächste Abschnitte). Die Regel, die den Wert liefert, definieren Sie unter **Stammdaten**.

### Regelablauf zur Kalkulationsvorlage einrichten

Diese dedizierte Einrichtung beschreibt die Aktivierung der Automatik über mehrere Seiten hinweg (Kalkulationsvorlage → Regelablauf → Regel) und schließt mit dem auslösenden Vorgang im Tagesgeschäft ab.

**Prozessintro:** Der **Regelablauf** ist die Klammer, die eine oder mehrere Regeln zu einer ausführbaren Reihenfolge verbindet. Er wird pro **Kalkulationsvorlage** geführt und über die Aktion **Regelablauf** auf der Vorlagenkarte angelegt und bearbeitet. Konfiguriert wird er von einem Key-User vor der ersten Nutzung der Vorlage; ausgeführt wird er automatisch bei jeder Neuberechnung einer Kalkulation, die diese Vorlage verwendet (siehe **Tägliche Arbeit**).

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Kalkulationsvorlagen**, öffnen Sie die **Kalkulationsvorlage** und wählen Sie die Aktion **Regelablauf** (im Menüband unter der Navigation, zusätzlich als geförderte Aktion im Prozessbereich).

**Nummerierte Aktivierungsschritte (in Abhängigkeitsreihenfolge):**

1. **Zielzeile kennzeichnen (Stammdaten der Vorlage):** Setzen Sie in der Vorlagenzeile die **Feldart** auf **Regel**. Wenn gesetzt, wird diese Zeile leer initialisiert und für die Regelbefüllung freigegeben — ohne dieses Kennzeichen greift keine Regel auf die Zeile zu.
2. **Regelablauf öffnen (globale Kopplung):** Wählen Sie auf der Vorlage die Aktion **Regelablauf**. Wenn die Vorlage noch keinen Ablauf besitzt, wird beim ersten Aufruf automatisch ein neuer, leerer **Regelablauf** vom Typ **Kalkulation** erzeugt, der Vorlage zugeordnet (über die **Regelablauf-ID**) und geöffnet. Bei jedem weiteren Aufruf wird derselbe Ablauf geöffnet.
3. **Regel bereitstellen (Stammdaten):** Legen Sie in der Liste **Regeln** die benötigte **Regel** der **Regelart** **Kalk.-Zeilenwert setzen** an (siehe **Stammdaten**). Wenn gesetzt, kann diese Regel einen Zielwert in der Kalkulationszeile schreiben.
4. **Regel in den Ablauf aufnehmen (scoped Kopplung):** Erfassen Sie im **Regelablauf** eine Zeile der **Zeilenart** **Regel** und tragen Sie im Feld **Regelcode** die zuvor angelegte Regel ein. Wenn gesetzt, wird die Regel bei der Verarbeitung des Ablaufs ausgeführt. Über **Wenn (Wahr)**, **Wenn (Falsch)**, **Wenn (Vergleich)**, **Sonst** und **Ende** steuern Sie, unter welchen Bedingungen der Schritt greift.

**Felder des Regelablaufs (Zeile):**

| Feld | Erläuterung |
|------|-------------|
| **Ablauf** | Zeigt den aus Zeilenart, Regel und Vergleich generierten Ablauftext der Zeile an (nur Anzeige); wenn eine Zeile eingerückt dargestellt ist, liegt sie innerhalb einer Bedingung. |
| **Zeilenart** | Wenn Sie eine Zeilenart wählen, bestimmt sie die Funktion der Ablaufzeile. Werte siehe Aufstellung unter der Tabelle. |
| **Regelcode** | Wenn Sie bei Zeilenart **Regel** einen Regelcode wählen, wird genau diese Regel an dieser Stelle des Ablaufs ausgeführt. |
| **Variable** | Wenn Sie eine Ablaufvariable angeben, wird der ausgewertete Wert dieser Variable im Vergleich oder als Zwischenergebnis genutzt. |
| **Vergleichszeichen** | Wenn Sie bei einer Wenn-Zeile ein Vergleichszeichen setzen, legt es die Vergleichsoperation fest (z. B. gleich, größer, kleiner) zwischen den beiden Vergleichsseiten. |
| **Vergleichsregelcode** | Wenn Sie eine Vergleichsregel angeben, wird deren Ergebnis als rechte Seite des Vergleichs herangezogen. |
| **Vergleichsvariable** | Wenn Sie eine Vergleichsvariable angeben, wird deren Wert als rechte Seite des Vergleichs herangezogen. |
| **Wertart** | Zeigt die Wertart der Zeile an und stellt sicher, dass Regeln und Vergleiche typkonform (z. B. dezimal) ausgewertet werden. |

**Werte der Zeilenart (für dieses Modul relevant):**

- **Regel:** Wenn gewählt, wird die im **Regelcode** hinterlegte Regel an dieser Stelle ausgeführt — hier binden Sie die Regel **Kalk.-Zeilenwert setzen** ein.
- **Wenn (Wahr):** Wenn gewählt, werden die folgenden, eingerückten Zeilen nur ausgeführt, wenn die Bedingungsregel den Wahrheitswert *wahr* liefert.
- **Wenn (Falsch):** Wenn gewählt, werden die folgenden Zeilen nur ausgeführt, wenn die Bedingungsregel *falsch* liefert.
- **Wenn (Vergleich):** Wenn gewählt, werden die folgenden Zeilen nur ausgeführt, wenn der Vergleich aus **Vergleichszeichen**, **Vergleichsregelcode**/**Vergleichsvariable** zutrifft.
- **Sonst:** Wenn gewählt, kehrt sich die Bedingung des zugehörigen Wenn-Blocks für die folgenden Zeilen um.
- **Ende:** Wenn gewählt, schließt sie einen Bedingungsblock ab; nachfolgende Zeilen werden wieder unabhängig von der Bedingung ausgeführt.

**Operativer Abschluss:** Die Kette ist wirksam, sobald der Anwender im Tagesgeschäft die Kalkulation neu berechnet — dann verarbeitet das Modul den Ablauf und füllt die Zielzeile. Siehe **Tägliche Arbeit: Kalkulation neu berechnen**.

> Alternativ zur zeilenbasierten Bearbeitung steht in der regelbasierten Datenverwaltung ein grafischer Ablauf-Editor zur Verfügung. Die fachliche Wirkung ist identisch; für dieses Modul genügt die zeilenbasierte Pflege des **Regelablaufs**.

## Stammdaten

### Regel „Kalk.-Zeilenwert setzen" pflegen

**Prozessintro:** Die **Regel** ist der Stammsatz, der einen konkreten Wert ermittelt und in eine Kalkulationszeile schreibt. Sie wird von einem Key-User in der regelbasierten Datenverwaltung gepflegt, bevor der zugehörige **Regelablauf** genutzt wird. Die hier gepflegten Werte erscheinen später als automatisch gesetzter **Wert** in der Kalkulation (siehe **Tägliche Arbeit**). Dieses Modul ergänzt die **Regel** um die **Regelart** **Kalk.-Zeilenwert setzen** und um die Gruppe **Kalkulation**, in der Sie Zielvorlage, Zielzeile und Zielfelder festlegen.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Regeln** und öffnen Sie über eine Zeile die Karte **Regel**. Die Liste **Regeln** ist über die Suche auffindbar; die Karte **Regel** öffnen Sie aus der Liste heraus.

**Allgemeine Felder der Regel (Basis, für dieses Modul relevant):**

| Feld | Erläuterung |
|------|-------------|
| **Code** | Wenn Sie einen Code vergeben, identifiziert er die Regel eindeutig; unter diesem Code binden Sie die Regel später im **Regelablauf** über den **Regelcode** ein. |
| **Beschreibung** | Wenn Sie eine Beschreibung erfassen, erleichtert sie das Wiederfinden der Regel in Listen und im Regelablauf. |
| **Regelart** | Wenn Sie die Regelart wählen, bestimmt sie, welche Aktion die Regel ausführt. Für dieses Modul ist der Wert **Kalk.-Zeilenwert setzen** maßgeblich; erst dann erscheint die Gruppe **Kalkulation**. Weitere Regelarten der Basis (z. B. **Wert zurückgeben**, **Eigenschaft setzen**) bleiben verfügbar, füllen aber keine Kalkulationszeile. |
| **Wertart** | Wenn Sie **Kalk.-Zeilenwert setzen** wählen, wird die Wertart automatisch auf **Dezimal** gesetzt, da Kalkulationswerte dezimale Beträge sind; eine abweichende Wertart ist für diese Regelart nicht sinnvoll. |
| **Direkt** | Wenn aktiviert, wird die Regel direkt (ohne Umweg über einen Ablauf) ausgewertet; für die Kalkulationsbefüllung wird die Regel jedoch über den **Regelablauf** der Vorlage angesteuert. |
| **Materialart** / **Materialartencode** | Wenn Sie eine Materialart hinterlegen, kann die Regel materialartabhängige Werte über die **Matrix** ermitteln; ohne Materialart wirkt die Regel materialartunabhängig. |
| **Eigenschaft** / **Merkmalcode** | Wenn Sie eine Eigenschaft hinterlegen, bezieht die Regel deren Wert (z. B. eine Materialeigenschaft des kalkulierten Artikels) in die Ermittlung ein. |
| **Standardwerte verwenden** | Wenn aktiviert, greift die Regel bei fehlendem Matrixtreffer auf hinterlegte Konstantwerte zurück; ohne das Kennzeichen liefert ein fehlender Treffer keinen Wert. |
| **Ausgabetext** | Wenn Sie einen Ausgabetext hinterlegen, wird er bei Regelarten mit Meldung ausgegeben; für **Kalk.-Zeilenwert setzen** ohne Bedeutung. |

> Die Regel-Basisseite enthält je nach **Regelart** weitere Felder (Konstanten, **Formel**, **Ausdruck zurückgeben**, Arbeitsplan-/Stücklistenbezug). Diese sind nur bei den jeweiligen Basis-Regelarten sichtbar und bearbeitbar. Für die Regelart **Kalk.-Zeilenwert setzen** sind die Felder der Gruppe **Kalkulation** entscheidend.

**Gruppe „Kalkulation" (durch dieses Modul ergänzt):** Diese Gruppe ist nur sichtbar, wenn die **Regelart** auf **Kalk.-Zeilenwert setzen** steht.

| Feld | Erläuterung |
|------|-------------|
| **Kalkulationsvorlagencode** | Wenn Sie hier eine Kalkulationsvorlage wählen, legen Sie fest, in welcher Vorlage die Zielzeile liegt; nur so kann die Regel die richtige Zeile ansprechen. Die Auswahl ist auf vorhandene Kalkulationsvorlagen beschränkt. |
| **Kalkulationsvorlagenzeile** | Wenn Sie eine Zeilennummer wählen, bestimmen Sie die konkrete Zielzeile innerhalb der Vorlage. Auswählbar sind ausschließlich Zeilen dieser Vorlage mit **Feldart** **Regel**. Beim Setzen dieses Feldes wird **Wert setzen** automatisch aktiviert, damit die Regel standardmäßig den Hauptwert füllt. |
| **Wert setzen** | Wenn aktiviert, schreibt die Regel ihr Ergebnis in das Feld **Wert** der Zielzeile; ohne das Kennzeichen bleibt **Wert** durch die Regel unberührt. |
| **Alt. Wert 1 setzen** | Wenn aktiviert, schreibt die Regel ihr Ergebnis zusätzlich in **Alt. Wert 1** der Zielzeile; nützlich für Varianten- oder Staffelwerte. |
| **Alt. Wert 2 setzen** | Wenn aktiviert, schreibt die Regel ihr Ergebnis zusätzlich in **Alt. Wert 2** der Zielzeile. |
| **Alt. Wert 3 setzen** | Wenn aktiviert, schreibt die Regel ihr Ergebnis zusätzlich in **Alt. Wert 3** der Zielzeile. |
| **Alt. Wert 4 setzen** | Wenn aktiviert, schreibt die Regel ihr Ergebnis zusätzlich in **Alt. Wert 4** der Zielzeile. |

**Prozessschritte (Reihenfolge):**

1. Zuerst legen Sie **Code**, **Beschreibung** und **Regelart** **Kalk.-Zeilenwert setzen** fest; danach erscheint die Gruppe **Kalkulation**.
2. Wählen Sie **Kalkulationsvorlagencode** und **Kalkulationsvorlagenzeile** (nur Zeilen mit **Feldart** **Regel** stehen zur Auswahl).
3. Aktivieren Sie die Zielfelder über **Wert setzen** / **Alt. Wert 1 setzen** bis **Alt. Wert 4 setzen**.
4. Pflegen Sie das eigentliche Rechenergebnis der Regel über die Aktion **Matrix** (bei dieser Regelart automatisch aktiv), ggf. materialart- oder eigenschaftsabhängig.

**Aktionen der Regel:** Die Aktion **Matrix** ist bei der Regelart **Kalk.-Zeilenwert setzen** aktiviert und öffnet die Wertematrix der Regel. Die Aktion **Eigenschaften** steht wie bei den übrigen Regelarten zur Verfügung.

**Validierungs- und Abhängigkeitshinweise:**

- Die **Kalkulationsvorlagenzeile** lässt sich nur auf Zeilen setzen, die in der gewählten Vorlage die **Feldart** **Regel** tragen — die Zielzeile muss also zuvor in der Vorlage entsprechend gekennzeichnet sein (siehe **Einrichtung**).
- Beim Auswählen der **Kalkulationsvorlagenzeile** wird **Wert setzen** automatisch aktiviert; passen Sie die Zielfelder danach bei Bedarf an.
- Die **Wertart** wird bei dieser Regelart fest auf **Dezimal** gestellt.

## Tägliche Arbeit: Kalkulation neu berechnen

**Setup-Bezug:** Dieser Ablauf setzt voraus, dass die genutzte **Kalkulationsvorlage** eine Zeile mit **Feldart** **Regel** besitzt, dass der Vorlage ein **Regelablauf** zugeordnet ist und dass eine **Regel** der **Regelart** **Kalk.-Zeilenwert setzen** die Zielzeile bedient (siehe **Einrichtung** und **Stammdaten**). Ohne diese Einrichtung verhält sich die Kalkulation wie im Standard der m+m Kalkulation.

Der operative Anwender arbeitet ausschließlich in der **Kalkulation**. Die Regelverarbeitung ist ein Hintergrundvorgang ohne eigene Maske.

**Ablauf:**

1. Erzeugen Sie zur Verkaufszeile eine **Kalkulation** und wählen Sie die vorbereitete **Kalkulationsvorlage**. Die Vorlagenzeilen werden als Kalkulationszeilen übernommen; die mit **Feldart** **Regel** gekennzeichnete Zeile bleibt zunächst mit **Wert** 0.
2. Stellen Sie sicher, dass die Kalkulation den Status **In Entwicklung** hat — nur dann ist eine Neuberechnung möglich.
3. Lösen Sie die **Neuberechnung** der Kalkulation aus. Unmittelbar vor der Zeilenberechnung verarbeitet dieses Modul automatisch den **Regelablauf** der Vorlage: Für jede Regel **Kalk.-Zeilenwert setzen** wird der ermittelte Dezimalwert in die als Ziel hinterlegten Felder (**Wert** bzw. **Alt. Wert 1**–**4**) der Kalkulationszeile geschrieben.
4. Zur Wertermittlung berücksichtigt das Modul den kalkulierten Artikel: Ist die Kalkulation einer Verkaufszeile zugeordnet und ist diese ein Artikel, wird dieser Artikel herangezogen; andernfalls die im Kalkulationskopf hinterlegte Artikelnr. Dadurch können material- und eigenschaftsabhängige Regeln den passenden Wert liefern.
5. Prüfen Sie in der regelgesteuerten Zeile den gesetzten **Wert**. Er ist nicht manuell editierbar und wird bei jeder erneuten Berechnung neu ermittelt (sofern die Zeile nicht als **Fixer Wert** gekennzeichnet ist).

> Es öffnet sich während der Regelverarbeitung kein zusätzliches Fenster. Ist der Vorlage kein Regelablauf zugeordnet oder ist der Ablauf leer, wird die Kalkulation ohne Regelbefüllung wie im Standard berechnet.

## FAQ und Troubleshooting

### Warum bleibt der Wert meiner Kalkulationszeile trotz Regel auf 0?

Prüfen Sie drei Bedingungen: (1) Die Vorlagenzeile trägt die **Feldart** **Regel**. (2) Der **Kalkulationsvorlage** ist ein **Regelablauf** zugeordnet und dieser enthält eine Zeile der **Zeilenart** **Regel** mit dem passenden **Regelcode**. (3) In der Regel ist unter **Kalkulation** die richtige **Kalkulationsvorlagenzeile** gewählt und mindestens **Wert setzen** aktiviert. Fehlt eine dieser Bedingungen, wird kein Wert geschrieben.

### Warum kann ich den Wert in der regelgesteuerten Zeile nicht von Hand ändern?

Sobald eine Vorlagenzeile die **Feldart** **Regel** hat, werden **Wert** und **Alt. Wert 1**–**4** auf 0 gesetzt und für die manuelle Eingabe gesperrt. Die Werte sind ausschließlich der Regelverarbeitung vorbehalten, damit manuelle und automatische Werte nicht in Konflikt geraten.

### Warum erscheint die Gruppe „Kalkulation" auf der Regel nicht?

Die Gruppe **Kalkulation** ist nur sichtbar, wenn die **Regelart** der Regel auf **Kalk.-Zeilenwert setzen** steht. Bei jeder anderen Regelart wird die Gruppe ausgeblendet, weil dann keine Kalkulationszeile bedient wird.

### Warum kann ich in der Regel keine bestimmte Kalkulationsvorlagenzeile auswählen?

Die Auswahl der **Kalkulationsvorlagenzeile** ist auf Zeilen der gewählten Vorlage beschränkt, die die **Feldart** **Regel** tragen. Kennzeichnen Sie die Zielzeile zuerst in der **Kalkulationsvorlage** entsprechend; danach steht sie in der Regel zur Auswahl.

### Warum wird beim Setzen der Zielzeile automatisch „Wert setzen" aktiviert?

Beim Auswählen der **Kalkulationsvorlagenzeile** aktiviert das System automatisch **Wert setzen**, damit die Regel standardmäßig den Hauptwert der Zeile füllt. Möchten Sie stattdessen (oder zusätzlich) alternative Werte setzen, aktivieren Sie **Alt. Wert 1 setzen** bis **Alt. Wert 4 setzen** und passen Sie **Wert setzen** bei Bedarf an.

### Warum ist die Wertart meiner Regel fest auf „Dezimal"?

Bei der **Regelart** **Kalk.-Zeilenwert setzen** setzt das Modul die **Wertart** automatisch auf **Dezimal**, weil Kalkulationswerte dezimale Beträge sind. Eine andere Wertart würde nicht typkonform in die Kalkulationszeile passen.

### Warum passiert beim Öffnen von „Regelablauf" auf der Vorlage zunächst nichts Sichtbares außer einer leeren Liste?

Beim ersten Aufruf der Aktion **Regelablauf** legt das Modul einen neuen, leeren **Regelablauf** vom Typ **Kalkulation** an und ordnet ihn der Vorlage zu (über die **Regelablauf-ID**). Der Ablauf ist zunächst leer; Sie erfassen die Ausführungsschritte anschließend als Zeilen.

### Muss ich die Kalkulation buchen oder freigeben, damit die Regel greift?

Nein. Dieses Modul kennt keinen Buchungs- oder Freigabeschritt. Der einzige Auslöser ist die **Neuberechnung** der Kalkulation im Status **In Entwicklung**. Die Regelverarbeitung läuft automatisch vor der Zeilenberechnung.

### Woher weiß die Regel, für welchen Artikel sie rechnet?

Das Modul ermittelt den Artikel aus der Kalkulation: Ist die Kalkulation einer Verkaufszeile vom Typ Artikel zugeordnet, wird dieser Artikel verwendet; sonst die Artikelnr. des Kalkulationskopfes. Auf dieser Basis können material- und eigenschaftsabhängige Regeln den korrekten Wert über die **Matrix** liefern.

### Kann ich mehrere Zeilen einer Vorlage regelgesteuert füllen?

Ja. Kennzeichnen Sie jede gewünschte Vorlagenzeile mit **Feldart** **Regel** und legen Sie je Zielzeile eine Regel **Kalk.-Zeilenwert setzen** an (mit passender **Kalkulationsvorlagenzeile**). Nehmen Sie alle Regeln als Schritte in den **Regelablauf** der Vorlage auf; über **Wenn**-/**Sonst**-/**Ende**-Zeilen steuern Sie, welche Regeln unter welchen Bedingungen greifen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Materialabhängiger Zuschlag automatisch in die Kalkulation

**Auslöser:** Der Vertrieb kalkuliert einen Verkaufsartikel, bei dem ein Zuschlag von der Materialart des Artikels abhängt. Bisher trug der Sachbearbeiter diesen Zuschlag in jeder Kalkulation manuell ein.

**Einstieg in BC:** Ein Key-User öffnet über **Suchen** die **Kalkulationsvorlagen**, öffnet die betreffende **Kalkulationsvorlage** und setzt in der Zuschlagszeile die **Feldart** auf **Regel**.

**Kernablauf:**
1. Auf der Vorlage wählt der Key-User die Aktion **Regelablauf**; es wird ein neuer, leerer Ablauf angelegt und geöffnet.
2. Über **Suchen** → **Regeln** legt er eine **Regel** mit **Regelart** **Kalk.-Zeilenwert setzen** an, wählt in der Gruppe **Kalkulation** den **Kalkulationsvorlagencode** und die Zuschlagszeile als **Kalkulationsvorlagenzeile** und belässt **Wert setzen** aktiv.
3. Über die Aktion **Matrix** hinterlegt er die materialartabhängigen Zuschlagswerte.
4. Im **Regelablauf** erfasst er eine Zeile der **Zeilenart** **Regel** mit dem **Regelcode** dieser Regel.
5. Der operative Anwender erstellt später eine **Kalkulation** mit dieser Vorlage und berechnet sie neu.

**Abschluss:** Der materialartabhängige Zuschlag steht nach der Neuberechnung automatisch im **Wert** der Zuschlagszeile; eine manuelle Erfassung entfällt.

### Anwendungsfall 2: Bedingter Wert über eine Wenn-Verzweigung

**Auslöser:** Ein Wert soll nur unter einer bestimmten Bedingung gesetzt werden (z. B. nur für eine bestimmte Materialart), sonst soll die Zeile 0 bleiben.

**Einstieg in BC:** Der Key-User öffnet die vorbereitete **Kalkulationsvorlage** und darüber den **Regelablauf**.

**Kernablauf:**
1. Er legt in der regelbasierten Datenverwaltung zwei Regeln an: eine Bedingungsregel (Basis-Regelart, die einen Wahrheitswert oder Vergleichswert liefert) und eine Regel **Kalk.-Zeilenwert setzen**, die den eigentlichen Wert schreibt.
2. Im **Regelablauf** erfasst er eine Zeile **Wenn (Wahr)** (bzw. **Wenn (Vergleich)** mit **Vergleichszeichen** und **Vergleichsregelcode**/**Vergleichsvariable**) mit der Bedingungsregel.
3. Darunter — eingerückt — erfasst er die Zeile **Zeilenart** **Regel** mit dem **Regelcode** der Wert-Regel.
4. Er schließt den Block mit einer Zeile **Ende** ab; optional ergänzt er einen **Sonst**-Zweig.
5. Der Anwender berechnet die Kalkulation neu.

**Abschluss:** Der Wert wird nur gesetzt, wenn die Bedingung zutrifft; andernfalls bleibt die Zeile bei 0. Die Verzweigung ist im **Ablauf**-Text des Regelablaufs an der Einrückung erkennbar.
