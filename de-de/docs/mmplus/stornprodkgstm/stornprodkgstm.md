---
title: Anwenderhandbuch m+m Undoing Production with Unit Conversion
---

# Anwenderhandbuch m+m Undoing Production with Unit Conversion

## Einleitung

Die App **m+m Undoing Production with Unit Conversion** ist eine Verbindungs-App für **Microsoft Dynamics 365 Business Central**. Sie verbindet die Stornierung von Produktionsbuchungen mit der Einheitenumrechnung KG/Meter/Stück. Storniert ein Anwender im **Produktions Buch.-Blatt** eine bereits gebuchte Ist-Meldung oder Verbrauchsbuchung, sorgt diese App dafür, dass die Umrechnungswerte KG, Meter und Stück des ursprünglichen **Artikelpostens** auf die neu erzeugte Stornozeile im Buch.-Blatt übernommen werden. So bleibt die KG/Meter/Stück-Information auch nach der Stornierung konsistent und wird ordnungsgemäß zurück abgewickelt.

Die App fügt selbst **keine** eigenen Seiten, Einrichtungsseiten oder Stammdaten hinzu. Sie arbeitet vollständig im Hintergrund und greift in den bestehenden Stornierungsvorgang der App **m+m Undoing Production** ein, indem sie zusätzliche Mengenfelder der App **m+m Unit Conversion** mitführt.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender in der Fertigung** — Fertigungssteuerung und Lagerpersonal, die im **Produktions Buch.-Blatt** eines freigegebenen Fertigungsauftrags täglich Ist-Meldungen und Verbrauchsbuchungen erfassen und bei Bedarf stornieren. Administratoren sind nur sekundär betroffen, da die App keine eigene Einrichtung erfordert; ihre Aufgabe beschränkt sich auf die Installation der erforderlichen Apps (siehe **Voraussetzungen**).

### Kurzer Prozessüberblick

1. Ein Anwender hat in der Fertigung eine Ist-Meldung und/oder Verbrauchsbuchung gebucht. Zu dieser Buchung wurden über die App **m+m Unit Conversion** die Werte **KG**, **Meter** und **Stück** sowie die Umrechnungsfaktoren im **Artikelposten** festgehalten.
2. Stellt der Anwender fest, dass die Buchung falsch war, storniert er sie im **Produktions Buch.-Blatt** über die Aktion **Buchung stornieren**.
3. Business Central erzeugt für die Stornierung neue Zeilen im **Produktions Buch.-Blatt** (Gegenbuchungen). Diese App überträgt dabei die Umrechnungswerte des ursprünglichen **Artikelpostens** auf die Stornozeilen.
4. Der Anwender bucht die Stornozeilen. Die KG/Meter/Stück-Werte werden dadurch korrekt zurück abgewickelt.

## Voraussetzungen

Damit diese App wirken kann, müssen die folgenden Apps installiert sein. Ohne diese Apps stehen weder die Stornierungsaktion noch die Umrechnungsfelder im **Produktions Buch.-Blatt** zur Verfügung.

| Voraussetzung | Erläuterung |
|---------------|-------------|
| **m+m Undoing Production** | Stellt die Aktion **Buchung stornieren** im **Produktions Buch.-Blatt** und den zugrunde liegenden Stornierungslauf bereit. Wenn diese App fehlt, kann keine Produktionsbuchung storniert werden und diese Verbindungs-App hat keinen Anknüpfungspunkt. |
| **m+m Unit Conversion** | Stellt die Umrechnungsfelder **KG**, **Meter**, **Stück** sowie die tatsächlichen und theoretischen KG-pro-Meter/Stück-Faktoren im **Artikelposten** und in der **Artikelbuchblattzeile** bereit. Wenn diese App fehlt, existieren die zu übertragenden Felder nicht. |
| **m+m Cloud Base** | Basis-App der m+m-Anwendungen; technische Grundlage, keine anwenderseitige Bedienung. |

Eine eigene Einrichtung dieser Verbindungs-App ist nicht erforderlich. Es gibt keine Nummernserien, keine Einrichtungsseite und keine Stammdaten, die der Anwender pflegen muss. Die Aktivierung erfolgt allein durch die Installation der oben genannten Apps.

## Schnellstart für Anwender

Der schnellste Weg, eine fehlerhafte Produktionsbuchung inklusive KG/Meter/Stück-Werten zurück abzuwickeln:

1. Öffnen Sie den freigegebenen **Fertigungsauftrag**, dessen Buchung storniert werden soll, und rufen Sie das **Produktions Buch.-Blatt** auf.
2. Wählen Sie im **Produktions Buch.-Blatt** die Aktion **Buchung stornieren**.
3. Setzen Sie im Abfragedialog die gewünschten Optionen: **Verbrauchsbuchung stornieren** und/oder **Ist-Meldung stornieren**, dazu je Bereich **Menge stornieren** bzw. bei der Ist-Meldung zusätzlich **Zeiten stornieren**.
4. Bestätigen Sie den Dialog mit **OK**. Business Central löscht zunächst nach Rückfrage vorhandene Buch.-Blattzeilen und öffnet anschließend Auswahlfenster mit den stornierbaren **Artikelposten** bzw. Kapazitätsposten. Wählen Sie die zu stornierenden Zeilen aus und bestätigen Sie mit **OK**.
5. Business Central erzeugt neue Stornozeilen im **Produktions Buch.-Blatt**. Dabei überträgt die App die Werte **KG**, **Meter**, **Stück** sowie die tatsächlichen und theoretischen KG-pro-Meter/Stück-Faktoren aus dem ausgewählten **Artikelposten** auf die neue **Artikelbuchblattzeile**.
6. Prüfen Sie die erzeugten Zeilen und führen Sie die Funktion **Buchen** aus. Mit der Buchung sind die KG/Meter/Stück-Werte korrekt zurück abgewickelt.

Für die Verbrauchsstornierung mit **Chargennr.** oder Seriennr. wird die Artikelverfolgung der ursprünglichen Buchung automatisch mitgeführt; eine manuelle Nacherfassung der Charge ist nicht erforderlich.

## Umrechnungsfelder in der Stornierung

Diese App überträgt bei jeder Stornierung — sowohl bei der **Ist-Meldung** (Fertigmeldung) als auch bei der **Verbrauchsbuchung** — genau die folgenden Felder aus dem ursprünglichen **Artikelposten** auf die neu erzeugte **Artikelbuchblattzeile**. Die Werte werden gesetzt, bevor Business Central die Menge der Stornozeile validiert, damit die Gegenbuchung dieselben Umrechnungswerte trägt wie die Ursprungsbuchung.

| Feld | Erläuterung |
|------|-------------|
| **KG** | Wenn im ursprünglichen Artikelposten ein KG-Wert hinterlegt war, wird dieser auf die Stornozeile übernommen; dadurch bucht die Gegenbuchung dieselbe KG-Menge zurück und der KG-Bestand bleibt nach der Stornierung konsistent. |
| **Meter** | Wenn im ursprünglichen Artikelposten ein Meter-Wert hinterlegt war, wird dieser auf die Stornozeile übernommen; die Gegenbuchung wickelt damit die gebuchten Meter vollständig zurück. |
| **Stück** | Wenn im ursprünglichen Artikelposten ein Stück-Wert hinterlegt war, wird dieser auf die Stornozeile übernommen; die Gegenbuchung storniert damit die gebuchte Stückzahl passend zur KG- und Meter-Menge. |
| **Tatsächliche KG pro Meter** | Wenn im ursprünglichen Artikelposten ein tatsächlicher Faktor KG pro Meter hinterlegt war, wird dieser auf die Stornozeile übernommen; dadurch verwendet die Gegenbuchung denselben tatsächlichen Umrechnungsfaktor wie die Ursprungsbuchung und erzeugt keine abweichende KG-/Meter-Relation. |
| **Tatsächliche KG pro Stück** | Wenn im ursprünglichen Artikelposten ein tatsächlicher Faktor KG pro Stück hinterlegt war, wird dieser auf die Stornozeile übernommen; die Gegenbuchung rechnet damit KG und Stück mit demselben tatsächlichen Faktor zurück. |
| **Theoretische KG pro Meter** | Wenn im ursprünglichen Artikelposten ein theoretischer Faktor KG pro Meter hinterlegt war, wird dieser auf die Stornozeile übernommen; damit bleibt der theoretische Referenzfaktor der Gegenbuchung identisch zur Ursprungsbuchung und Abweichungen zwischen tatsächlichem und theoretischem Wert bleiben nachvollziehbar. |
| **Theoretische KG pro Stück** | Wenn im ursprünglichen Artikelposten ein theoretischer Faktor KG pro Stück hinterlegt war, wird dieser auf die Stornozeile übernommen; die Gegenbuchung führt damit denselben theoretischen KG-pro-Stück-Faktor mit. |

Diese Felderübertragung ist der gesamte fachliche Funktionsumfang der App. Sie greift ausschließlich im Stornierungslauf der App **m+m Undoing Production** und nur dann, wenn die App **m+m Unit Conversion** die genannten Felder bereitstellt.

## Tägliche Arbeit im Produktions Buch.-Blatt

Die App hat keine eigene Bedienoberfläche. Der Anwender arbeitet vollständig in den Standard- und m+m-Seiten der Fertigung. Der relevante Einstieg ist der freigegebene **Fertigungsauftrag** und das daraus geöffnete **Produktions Buch.-Blatt**.

### Einstieg: Produktions Buch.-Blatt öffnen

**Einstieg:** Öffnen Sie in der Liste bzw. Karte des freigegebenen **Fertigungsauftrags** über die zugehörige Aktion das **Produktions Buch.-Blatt**. Damit alle KG/Meter/Stück-Felder in den Buch.-Blattzeilen vorhanden sind, müssen die unter **Voraussetzungen** genannten Apps installiert sein.

Im **Produktions Buch.-Blatt** erfasst der Anwender wie gewohnt Verbrauchs- und Ist-Meldungszeilen und bucht diese über die Funktion **Buchen**. Erst wenn eine bereits gebuchte Buchung zurückgenommen werden soll, kommt der Stornierungsvorgang zum Tragen, in den diese App eingreift.

### Aktion Buchung stornieren

**Einstieg:** Wählen Sie im **Produktions Buch.-Blatt** die Aktion **Buchung stornieren**. Diese Aktion stammt aus der App **m+m Undoing Production** und ist der einzige Einstiegspunkt, über den die Umrechnungsfelder dieser Verbindungs-App wirksam werden.

Nach Aufruf der Aktion öffnet sich ein Abfragedialog mit den folgenden Optionen. Die Angaben bestimmen, welche Buchungsart storniert wird und ob Mengen bzw. Zeiten durch Gegenbuchung zurückgenommen werden.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Verbrauchsbuchung stornieren** | Wenn gesetzt, werden die Verbrauchsbuchungen der Komponenten zur Stornierung angeboten; anschließend erzeugt Business Central Gegenbuchungszeilen für den Verbrauch und diese App überträgt die KG/Meter/Stück-Werte der ursprünglichen Verbrauchs-Artikelposten auf diese Zeilen. |
| **Menge stornieren** (Bereich **Verbrauchsbuchung**) | Wenn gesetzt, werden die gebuchten Verbrauchsmengen durch eine Gegenbuchung storniert; ohne diese Option bleibt die Verbrauchsmenge unverändert und es entsteht keine Verbrauchs-Stornozeile. |
| **Ist-Meldung stornieren** | Wenn gesetzt, wird die Ist-Meldung (Fertigmeldung) des Fertigartikels zur Stornierung angeboten; die daraus entstehenden Gegenbuchungszeilen erhalten über diese App die KG/Meter/Stück-Werte des ursprünglichen Ist-Meldungs-Artikelpostens. |
| **Menge stornieren** (Bereich **Ist-Meldung**) | Wenn gesetzt, werden die gebuchten Mengen der Ist-Meldung durch Gegenbuchung storniert; die App führt dabei die Umrechnungswerte der zugehörigen Artikelposten mit. |
| **Zeiten stornieren** (Bereich **Ist-Meldung**) | Wenn gesetzt, werden die gebuchten Zeiten der Ist-Meldung durch Gegenbuchung aus den Kapazitätsposten storniert; diese Zeitstornierung betrifft keine KG/Meter/Stück-Werte, sondern ausschließlich die gebuchten Kapazitätszeiten. |

Bestätigt der Anwender den Dialog mit **OK**, werden in Abhängigkeit der gesetzten Optionen weitere Auswahlfenster geöffnet:

1. Business Central löscht auf Nachfrage zunächst alle vorhandenen Buch.-Blattzeilen im betroffenen Buchblatt.
2. Bei aktivierter Mengenstornierung der **Ist-Meldung** öffnet sich die Auswahl der **Artikelposten** (Ist-Meldungen); der Anwender wählt einzelne, keine oder alle Zeilen. Für jede gewählte Zeile erzeugt Business Central eine Ist-Meldungs-Gegenbuchung und diese App überträgt deren KG/Meter/Stück-Werte.
3. Bei aktivierter Zeitenstornierung öffnet sich die Auswahl der Kapazitätsposten; hier werden nur Zeiten storniert.
4. Bei aktivierter Mengenstornierung der **Verbrauchsbuchung** öffnet sich die Auswahl der Verbrauchs-**Artikelposten**; für jede gewählte Zeile erzeugt Business Central eine Verbrauchs-Gegenbuchung und diese App überträgt deren KG/Meter/Stück-Werte.
5. Bestehen zu den ausgewählten Ist-Meldungen Reservierungen, fragt Business Central vor der Übernahme, ob fortgefahren werden soll; bei Bestätigung werden die betroffenen Reservierungen aufgelöst.

Im Anschluss stehen die Stornozeilen im **Produktions Buch.-Blatt**. Der Anwender prüft sie und führt die Funktion **Buchen** aus, um die Stornierung abzuschließen.

### Artikelverfolgung bei der Stornierung

Trägt der ursprüngliche **Artikelposten** eine **Chargennr.** oder Seriennr., übernimmt der Stornierungslauf diese Artikelverfolgung automatisch in die Stornozeile und stellt die Anwendung zum ursprünglichen Posten her. Der Anwender muss die Charge nicht erneut erfassen. Die KG/Meter/Stück-Werte dieser App werden unabhängig von der Artikelverfolgung immer aus demselben ausgewählten Artikelposten übernommen.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die App im Arbeitsalltag der Fertigung wirkt. Alle Schritte entsprechen dem tatsächlichen Ablauf im **Produktions Buch.-Blatt** und dem Stornierungslauf.

### Anwendungsfall 1: Falsche Ist-Meldung einer Coil-Fertigung zurücknehmen

**Auslöser:** Ein Mitarbeiter der Fertigung meldet der Fertigungssteuerung, dass eine Ist-Meldung für einen Fertigungsauftrag mit falscher Menge gebucht wurde. Der betroffene Artikel wird in KG geführt, aber auch in Meter und Stück umgerechnet.

**Einstieg in BC:** Die Fertigungssteuerung öffnet den freigegebenen **Fertigungsauftrag** und ruft daraus das **Produktions Buch.-Blatt** auf.

**Kernablauf:**
1. Aktion **Buchung stornieren** wählen.
2. Im Dialog **Ist-Meldung stornieren** und darunter **Menge stornieren** setzen; **Zeiten stornieren** bleibt aus, da nur die Menge falsch war.
3. Dialog mit **OK** bestätigen und die zu löschenden Buch.-Blattzeilen bestätigen.
4. In der Auswahl der **Artikelposten** die falsch gebuchte Ist-Meldung markieren und mit **OK** übernehmen.
5. Business Central erzeugt die Ist-Meldungs-Gegenbuchung; die App überträgt **KG**, **Meter**, **Stück** sowie die tatsächlichen und theoretischen KG-pro-Meter/Stück-Faktoren aus dem ausgewählten Artikelposten auf die Stornozeile.

**Abschluss:** Die Fertigungssteuerung prüft die Stornozeile und führt **Buchen** aus. Die KG/Meter/Stück-Werte des Fertigungsauftrags sind damit zurück abgewickelt und können anschließend korrekt neu gemeldet werden.

### Anwendungsfall 2: Fehlerhafte Verbrauchsbuchung einer chargengeführten Komponente stornieren

**Auslöser:** Bei der Nachkalkulation fällt auf, dass für einen Fertigungsauftrag eine Komponente mit falscher Charge verbraucht gebucht wurde. Die Komponente ist chargengeführt und wird in KG/Meter/Stück umgerechnet.

**Einstieg in BC:** Der Anwender öffnet den freigegebenen **Fertigungsauftrag** und daraus das **Produktions Buch.-Blatt**.

**Kernablauf:**
1. Aktion **Buchung stornieren** wählen.
2. Im Dialog **Verbrauchsbuchung stornieren** und darunter **Menge stornieren** setzen.
3. Dialog mit **OK** bestätigen und die Rückfrage zum Löschen der Buch.-Blattzeilen bestätigen.
4. In der Auswahl der Verbrauchs-**Artikelposten** die betroffene Zeile mit der falschen **Chargennr.** markieren und mit **OK** übernehmen.
5. Business Central erzeugt die Verbrauchs-Gegenbuchung, übernimmt die ursprüngliche **Chargennr.** über die **Artikelverfolgung** und stellt die Anwendung zum Ursprungsposten her; die App überträgt zusätzlich die KG/Meter/Stück-Werte des Artikelpostens auf die Stornozeile.

**Abschluss:** Der Anwender bucht die Stornozeile über **Buchen**. Der Verbrauch ist inklusive Charge und Umrechnungswerten zurückgenommen; anschließend kann die korrekte Charge neu verbraucht gebucht werden.

## FAQ und Troubleshooting

### 1. Warum brauche ich neben dieser App noch weitere Apps?
Diese App ist eine reine Verbindungs-App. Die Aktion **Buchung stornieren** stammt aus **m+m Undoing Production**, die Felder **KG**, **Meter** und **Stück** aus **m+m Unit Conversion**. Ohne diese beiden Apps gibt es weder die Stornierung noch die zu übertragenden Umrechnungsfelder.

### 2. Muss ich die App einrichten, bevor ich sie nutzen kann?
Nein. Die App hat keine Einrichtungsseite, keine Nummernserien und keine Stammdaten. Sie wirkt automatisch, sobald sie zusammen mit den erforderlichen Apps installiert ist.

### 3. Wo finde ich die Funktion, um eine Produktionsbuchung zu stornieren?
Im **Produktions Buch.-Blatt** eines freigegebenen Fertigungsauftrags über die Aktion **Buchung stornieren**. Eine eigene Seite dieser Verbindungs-App gibt es nicht.

### 4. Welche Felder überträgt die App genau?
Sie überträgt aus dem ursprünglichen **Artikelposten** die Felder **KG**, **Meter**, **Stück**, **Tatsächliche KG pro Meter**, **Tatsächliche KG pro Stück**, **Theoretische KG pro Meter** und **Theoretische KG pro Stück** auf die neu erzeugte **Artikelbuchblattzeile**.

### 5. Wann genau werden die Werte gesetzt?
Die Werte werden gesetzt, unmittelbar bevor Business Central die Menge der Stornozeile validiert. Dadurch trägt die Gegenbuchung dieselben Umrechnungswerte wie die ursprüngliche Buchung.

### 6. Gilt die Übertragung für Ist-Meldungen und für Verbrauchsbuchungen?
Ja. Sowohl beim Stornieren einer **Ist-Meldung** als auch beim Stornieren einer **Verbrauchsbuchung** werden dieselben KG/Meter/Stück-Werte des jeweiligen Ursprungspostens übernommen.

### 7. Werden bei der Zeitenstornierung ebenfalls KG/Meter/Stück-Werte übertragen?
Nein. Die Option **Zeiten stornieren** wirkt nur auf die gebuchten Kapazitätszeiten aus den Kapazitätsposten. Die KG/Meter/Stück-Werte werden ausschließlich für die Mengenstornierung aus den Artikelposten übertragen.

### 8. Was passiert mit einer Charge oder Seriennr. bei der Stornierung?
Trägt der Ursprungsposten eine **Chargennr.** oder Seriennr., wird die **Artikelverfolgung** automatisch in die Stornozeile übernommen und die Anwendung zum Ursprungsposten hergestellt. Die Umrechnungswerte werden davon unabhängig aus demselben Posten übernommen.

### 9. Warum fragt Business Central beim Stornieren nach dem Löschen von Buch.-Blattzeilen?
Der Stornierungslauf löscht zunächst vorhandene Zeilen im betroffenen Buchblatt, um saubere Stornozeilen erzeugen zu können. Bestätigen Sie diese Rückfrage nur, wenn die vorhandenen Zeilen tatsächlich verworfen werden dürfen.

### 10. Ich sehe nach der Stornierung keine KG/Meter/Stück-Werte auf der Stornozeile — woran liegt das?
Die App überträgt nur Werte, die im ursprünglichen **Artikelposten** vorhanden waren. War dort kein KG/Meter/Stück-Wert bzw. kein Umrechnungsfaktor hinterlegt, bleibt auch die Stornozeile in diesen Feldern leer. Prüfen Sie außerdem, ob die App **m+m Unit Conversion** installiert ist, da sonst die Felder gar nicht existieren.
