---
title: Anwenderhandbuch m+m Certificate Of Supply with Report Dispatch
---

# Anwenderhandbuch m+m Certificate Of Supply with Report Dispatch

## Einleitung

Dieses Modul verbindet die m+m **Gelangensbestätigung** mit dem m+m **Belegversand**. Es sorgt dafür, dass eine **Gelangensbestätigung** und die zugehörige **Gelangensbestätigungsmahnung** nicht nur gedruckt, sondern über den Belegversand als **E-Mail** oder als **Druckanhang** an den richtigen Empfänger versendet werden können. Das Modul selbst besitzt keine eigenen Seiten oder Felder; es wirkt im Hintergrund und schaltet den Versandweg für diese beiden Belege frei.

Fachlich löst das Modul beim Versand drei Aufgaben automatisch: Es ermittelt zur ausgewählten Gelangensbestätigung den zugehörigen Beleg (die **Verkaufslieferung**), es bestimmt anhand des Debitors bzw. Kreditors den passenden Empfänger samt **Sprachcode**, und es wählt das zutreffende **Belegversandprofil** für den jeweiligen Beleg aus. Der Anwender muss diese Zuordnung nicht manuell vornehmen.

**Zielgruppe.** Primäre Zielgruppe sind **operative Anwender** im Vertrieb und in der Versand-/Exportabwicklung, die im Tagesgeschäft Gelangensbestätigungen erhalten, nachverfolgen, drucken und versenden. Sekundäre Zielgruppe sind **Administratoren und Key-User**, die einmalig die Gelangensbestätigungseinrichtung und die Belegversandprofile hinterlegen.

**Kurzer Prozessüberblick.** Zuerst richtet der Administrator die **Gelangensbestätigungseinrichtung** (Nummernserie, Fälligkeitsberechnung) und je Debitor bzw. Kreditor ein **Belegversandprofil** ein. Danach arbeitet der Anwender in der Liste **Gelangensbestätigungen**: Er wählt einen Datensatz aus und löst über eine Aktion den Druck oder den Mailversand der Bestätigung oder der Mahnung aus. Beim Mailversand greift dieses Modul ein und stellt Empfänger, Sprache und Anhänge gemäß Belegversandprofil bereit.

## Schnellstart für Anwender

Der schnellste Weg vom eingerichteten System bis zur versendeten Gelangensbestätigung. Die Einrichtung (Schritte 1–2) ist Voraussetzung und wird nur einmal je Debitor bzw. Kreditor durchgeführt.

1. **Einrichtung prüfen (einmalig):** Öffnen Sie über **Suchen** die **Gelangensbestätigungseinrichtung** und stellen Sie sicher, dass eine Nummernserie hinterlegt ist.
2. **Belegversandprofil anlegen (einmalig je Empfänger):** Öffnen Sie über **Suchen** die Seite **m+m Belegversandprofile**, legen Sie eine Zeile mit der **Herkunftsart** Debitor bzw. Kreditor, der passenden **Herkunftsnr.**, der **Art** E-Mail und der **Belegart** für die Gelangensbestätigung an und füllen Sie die Empfängerfelder.
3. **Liste öffnen:** Öffnen Sie die Liste **Gelangensbestätigungen** (aus dem Modul m+m Gelangensbestätigung).
4. **Datensatz wählen:** Markieren Sie die zu versendende Zeile.
5. **Versenden:** Wählen Sie **Gelangensbestätigung per Mail senden** (oder **Gelangensbestätigung drucken** für den reinen Druck).
6. **E-Mail kontrollieren und senden:** Empfänger und Anhänge sind gemäß Belegversandprofil vorbelegt; prüfen Sie Empfänger, Betreff und Anhänge und senden Sie die E-Mail.
7. **Nachverfolgen:** Ist die Bestätigung bis zum **Fälligkeitsdatum** nicht **erhalten**, versenden Sie über **Mahnung per Mail senden** eine Mahnung.

## Einrichtung

Die Einrichtung ist die Voraussetzung für den gesamten Versand. Sie besteht aus zwei aufeinander aufbauenden Bereichen: der modulweiten **Gelangensbestätigungseinrichtung** und – je Debitor bzw. Kreditor – dem **Belegversandprofil**. Beide werden vom Administrator bzw. Key-User vor der ersten Nutzung gepflegt.

### Gelangensbestätigungseinrichtung

**Wer und wann.** Diese Seite ist eine unternehmensweite Einrichtungskarte und wird einmalig vom Administrator eingerichtet, bevor die erste Gelangensbestätigung entsteht. **Einstieg:** Öffnen Sie die **Gelangensbestätigungseinrichtung** über **Suchen** (unternehmensweite Einrichtung, kein übergeordneter Aufrufpfad).

| Einrichtung | Erläuterung |
|---|---|
| **Nummernserie Gelangensbestätigungen** | Wenn hier eine Nummernserie gesetzt ist, dann erhält jede neue Gelangensbestätigung automatisch eine fortlaufende **Nr.**; ohne Nummernserie können keine Gelangensbestätigungen nummeriert und damit nicht eindeutig versendet und nachverfolgt werden. |
| **Standard Fälligkeitsberechnungsformel** | Wenn hier eine Datumsformel gesetzt ist, dann wird bei jeder neuen Gelangensbestätigung aus dem Liefer-/Buchungsdatum automatisch das **Fälligkeitsdatum** berechnet; ist das Feld leer, bleibt das Fälligkeitsdatum offen und die Mahnstufenlogik hat keinen Bezugstermin. |

### Gelangensbestätigungsversand einrichten

**Prozesseinführung.** Diese Einrichtung schaltet den E-Mail- und Druckversand der Gelangensbestätigung frei. Konfiguriert wird sie vom Administrator bzw. Key-User, und zwar **je Debitor bzw. Kreditor**, für den Bestätigungen versendet werden. Sie wird im Tagesgeschäft im Abschnitt **Gelangensbestätigung senden und drucken** verwendet. Ohne passendes Belegversandprofil findet der Mailversand keinen Empfänger und kann nicht ausgeführt werden.

**Einstieg:** Öffnen Sie die Seite **m+m Belegversandprofile** über **Suchen** und führen Sie **Liste bearbeiten** aus.

Ablauf in Abhängigkeitsreihenfolge:

1. **Zuerst** die Gelangensbestätigungseinrichtung (Nummernserie, Fälligkeitsformel) hinterlegen – siehe oben.
2. **Danach** für jeden Debitor bzw. Kreditor eine Zeile in **m+m Belegversandprofile** anlegen: **Herkunftsart** wählen, **Herkunftsnr.** eintragen, **Art** und **Belegart** setzen, Empfänger und Anhänge pflegen.
3. **Schließlich** im Tagesgeschäft in der Liste **Gelangensbestätigungen** über **Gelangensbestätigung per Mail senden** den Versand auslösen; das Modul zieht das hier angelegte Profil automatisch.

Die Belege, für die dieses Modul den Versand freischaltet, sind die **Gelangensbestätigung** und die **Gelangensbestätigungsmahnung**. Legen Sie die **Belegart** im Profil entsprechend auf den jeweiligen Gelangensbestätigungsbeleg fest, damit das richtige Profil gezogen wird.

#### Felder der Seite m+m Belegversandprofile

Die folgende Tabelle dokumentiert alle Felder der Belegversandprofil-Zeile. Für die Gelangensbestätigung sind vor allem **Herkunftsart**, **Herkunftsnr.**, **Art**, **Belegart** sowie die Empfänger- und Anhangsfelder maßgeblich.

| Einrichtung | Erläuterung |
|---|---|
| **Herkunftsart** | Legt fest, für welchen Geschäftspartnerkreis das Profil gilt. **Allgemein:** Das Profil greift unabhängig von einem konkreten Partner. **Debitor:** Wenn gewählt, dann gilt das Profil für einen einzelnen Debitor und die **Herkunftsnr.** ist zwingend anzugeben. **Kreditor:** Wenn gewählt, dann gilt das Profil für einen einzelnen Kreditor und die **Herkunftsnr.** ist zwingend anzugeben. Für jeden Debitor bzw. Kreditor ist eine eigene Zeile anzulegen. |
| **Herkunftsnr.** | Wenn als Herkunftsart Debitor oder Kreditor gewählt ist, dann bestimmt die hier eingetragene Nummer den konkreten Geschäftspartner, für den das Profil beim Versand gezogen wird; mit der Auswahl wird der **Herkunftsname** automatisch gefüllt. |
| **Herkunftsname** | Zeigt den Namen zum gewählten Debitor bzw. Kreditor an, damit die Zeile ohne Nachschlagen eindeutig zugeordnet werden kann. |
| **Referenzart** | Optionale Verfeinerung des Geltungsbereichs. **(leer):** Wenn leer, dann gilt das Profil ohne zusätzliche Referenz. **Zusteller:** Wenn gewählt, dann wird das Profil zusätzlich auf einen Zusteller bezogen und die **Referenznr.** ist anzugeben. |
| **Referenznr.** | Wenn eine Referenzart gesetzt ist, dann konkretisiert diese Nummer die Referenz (z. B. den Zusteller), auf die das Profil zusätzlich eingegrenzt wird. |
| **Art** | Steuert den Versandkanal. **E-Mail:** Wenn gewählt, dann wird der Beleg als E-Mail versendet. **Drucken:** Wenn gewählt, dann wird der Beleg gedruckt. **Drucken und E-Mail:** Wenn gewählt, dann erfolgen Druck und E-Mail-Versand zusammen. |
| **Belegart** | Bestimmt, für welchen Beleg das Profil greift. Für dieses Modul ist die Belegart auf den Gelangensbestätigungsbeleg zu setzen, damit beim Versand aus der Liste **Gelangensbestätigungen** genau dieses Profil gezogen wird. |
| **Verantwortlichkeitscode** | Wenn ein Code gesetzt ist, dann werden alle Kontakte dieser Verantwortlichkeit als **An**-Empfänger vorbelegt; so lässt sich eine Personengruppe adressieren, ohne einzelne Adressen zu pflegen. |
| **Verantwortlichkeitsbeschreibung** | Zeigt die Beschreibung des gewählten Verantwortlichkeitscodes an. |
| **CC** | Wenn hier eine Verantwortlichkeit gesetzt ist, dann werden deren Kontakte als **CC**-Empfänger der E-Mail vorbelegt. |
| **BCC** | Wenn hier eine Verantwortlichkeit gesetzt ist, dann werden deren Kontakte als **BCC**-Empfänger der E-Mail vorbelegt. |
| **Zus. Empfänger** | Wenn hier Adressen hinterlegt sind, dann werden diese zusätzlich in das **An**-Feld übernommen; so lassen sich Empfänger adressieren, die nicht als Kontakt zum Debitor bzw. Kreditor gepflegt sind. |
| **Zus. CC** | Wie **Zus. Empfänger**, jedoch werden die Adressen in das **CC**-Feld übernommen. |
| **Zus. BCC** | Wie **Zus. Empfänger**, jedoch werden die Adressen in das **BCC**-Feld übernommen. |
| **Anzahl Anhänge** | Zeigt die Anzahl der zusätzlich hinterlegten Anhänge an. Wenn Sie in das Feld klicken, dann öffnet sich die Anhangsliste, in der zusätzliche Belege oder Dateien für den Versand ausgewählt werden; der eigentliche Beleg wird stets angehängt und hier nicht mitgezählt. |
| **Zusätzlich zum Standard** | Steuert, welche Empfänger im **An**-Feld vorbelegt werden. **Standard:** Wenn gewählt, dann werden nur die Adressen aus dem Belegversandprofil gesetzt. **Ja:** Wenn gewählt, dann werden die Adressen aus dem Profil und zusätzlich die aus der BC-Standardlogik gesetzt. **Nachfrage:** Wenn gewählt, dann fragt ein Dialog beim Versand nach; die Bestätigung wirkt wie **Ja**, die Ablehnung wie **Standard**. **Nur Standard:** Wenn gewählt, dann werden ausschließlich die Adressen der BC-Standardlogik gesetzt. Die Einstellung wirkt nur auf das **An**-Feld, nicht auf CC und BCC. |
| **ZIP-Option** | Steuert die Bündelung der Anhänge. **Keine:** Wenn gewählt, dann wird kein ZIP-Ordner erzeugt. **Alle:** Wenn gewählt, dann werden alle Belege und Dateien in einen ZIP-Ordner gepackt. **Nur Anhänge:** Wenn gewählt, dann werden nur die zusätzlichen Dateien (nicht der Beleg selbst) in einen ZIP-Ordner gepackt. |
| **Max. MB** | Wenn hier ein Wert gesetzt ist, dann wird eine E-Mail, deren Anhänge diese Grenze überschreiten, automatisch in mehrere nummerierte Teil-E-Mails aufgeteilt; überschreitet bereits eine einzelne Datei die Grenze, dann erscheint eine Fehlermeldung. So wird verhindert, dass E-Mails wegen zu großer Anhänge unzustellbar bleiben. |
| **Zus. Empfänger** / **Zus. CC** / **Zus. BCC** (Anzeige) | Die drei Anzeigefelder fassen die zusätzlich hinterlegten Adressen je Verteilerfeld zusammen und machen sie in der Liste direkt sichtbar. |

**Abhängigkeitshinweis.** Das Modul wählt beim Mailversand das Profil nach Priorität anhand von Herkunftsart, Herkunftsnr. und Belegart aus (im Hintergrund über den Belegversand). Fehlt für den Debitor bzw. Kreditor ein Profil zur passenden Belegart, findet der Mailversand keinen Empfänger. Der **Sprachcode** für die E-Mail wird automatisch aus dem Debitor bzw. Kreditor gezogen.

## Gelangensbestätigung senden und drucken

Dieser Abschnitt beschreibt das Tagesgeschäft. Er setzt die im Kapitel **Einrichtung** angelegten Profile voraus (Querverweis: **Gelangensbestätigungsversand einrichten**).

**Einstieg.** Öffnen Sie die Liste **Gelangensbestätigungen** (aus dem Modul m+m Gelangensbestätigung). Jede Zeile ist eine Gelangensbestätigung zu einer Verkaufslieferung.

### Felder der Liste Gelangensbestätigungen

Die wichtigsten Felder für Versand und Nachverfolgung:

| Feld | Erläuterung |
|---|---|
| **Belegart** | Herkunftsbelegart der Bestätigung. **Verkaufslieferung:** Bestätigung zu einer gebuchten Verkaufslieferung (der von diesem Modul unterstützte Fall). **Servicelieferung:** Bestätigung zu einer Servicelieferung. **Rücklieferung:** Bestätigung zu einer Rücklieferung. |
| **Belegnr.** | Wenn gesetzt, dann verweist die Nummer auf den zugrunde liegenden Liefer­beleg; darüber ermittelt das Modul beim Versand den zugehörigen Belegdatensatz. |
| **Status** | Zeigt den Bearbeitungsstand der Bestätigung an (nicht relevant, angefordert, erhalten, nicht erhalten). Der Status wird durch die Aktionen **Gelangensbestätigung erhalten** und **… zurücksetzen** sowie durch die Fälligkeits-/Mahnlogik gesteuert und ist schreibgeschützt. |
| **Nr.** | Fortlaufende Nummer aus der Nummernserie der Gelangensbestätigungseinrichtung; identifiziert die Bestätigung eindeutig. |
| **Gedruckt** | Wenn gesetzt, dann wurde die Bestätigung bereits gedruckt; dient der Kontrolle, ob der Nachweis den Empfänger erreicht hat. |
| **Debitoren-/Kreditorennr.** | Nummer des Geschäftspartners; darüber zieht das Modul beim Mailversand das passende Belegversandprofil und den Sprachcode. |
| **Debitoren-/Kreditorenname** | Name des Geschäftspartners zur schnellen Identifikation der Zeile. |
| **Lieferbedingungscode** | Lieferbedingung der zugrunde liegenden Lieferung; fachlicher Bestandteil des Nachweises. |
| **Liefer-/Buchungsdatum** | Datum der Lieferung/Buchung; Ausgangspunkt für die Fälligkeitsberechnung. |
| **Fälligkeitsdatum** | Termin, bis zu dem die Bestätigung erhalten sein soll; wird aus dem Liefer-/Buchungsdatum und der Standard-Fälligkeitsformel berechnet. Nach Ablauf ist eine **Mahnung** angezeigt. |
| **Mahnstufe** | Zeigt an, wie oft bereits gemahnt wurde; steuert die Eskalation über die Mahnaktionen. |
| **Steuernummer des Fahrzeugs** | Kennzeichen bzw. Steuernummer des Transportfahrzeugs; fachliches Nachweisfeld. |
| **Zertifikatsnr.** | Wenn gesetzt, dann bündelt diese Nummer mehrere zusammengefasste Bestätigungen; Grundlage für Sammeldruck und Sammelmahnung. |
| **Zertifikatsdatum** / **Empfangsdatum** / **Wareneingangsdatum** | Datumsangaben zum Zertifikat, zum bestätigten Empfang und zum Wareneingang; dokumentieren den zeitlichen Ablauf des Nachweises. |
| **Rechnungsnr.** / **Liefer-/Buchungsdatum** | Verweis auf die zugehörige Rechnung bzw. das Belegdatum. |
| **Art** | Gibt an, ob es sich um einen **Debitor** oder einen **Kreditor** handelt; bestimmt, ob beim Versand ein Debitoren- oder Kreditorenprofil gezogen wird. |
| Adressfelder **Lief. an Name/Adresse/Ort/PLZ/Land**, **Rech. an Name/Adresse/Ort/PLZ/Land**, Kontakt und Code | Diese schreibgeschützten Adressfelder spiegeln die Liefer- und Rechnungsanschrift aus dem zugrunde liegenden Beleg wider und erscheinen auf dem gedruckten Nachweis. Sie werden hier zu einer Gruppe zusammengefasst, da sie nur der Anzeige dienen und von diesem Modul nicht gesteuert werden. |

### Aktionen zum Versenden und Drucken

Die folgenden Aktionen der Liste lösen Druck bzw. Versand aus. Der Mailversand nutzt den m+m Belegversand; dieses Modul stellt dabei Empfänger, Sprache und Anhänge bereit.

| Aktion | Erläuterung |
|---|---|
| **Gelangensbestätigung drucken** | Druckt die Bestätigung der markierten Zeile. Setzt anschließend das Feld **Gedruckt**. |
| **Gelangensbestätigung per Mail senden** | Versendet die Bestätigung der markierten Zeile als E-Mail über den Belegversand; Empfänger, Sprache und Anhänge werden aus dem Belegversandprofil des Debitors bzw. Kreditors vorbelegt. |
| **Gelangensbestätigungen zusammenfassen** | Fasst mehrere markierte Bestätigungen unter einer gemeinsamen **Zertifikatsnr.** zusammen, sodass sie gebündelt gedruckt oder versendet werden können. |
| **Sammeldruck Gelangensbestätigung** | Druckt alle unter einer **Zertifikatsnr.** zusammengefassten Bestätigungen in einem Vorgang. |
| **Sammelgelangensbestätigung per Mail senden** | Versendet die zusammengefassten Bestätigungen einer **Zertifikatsnr.** in einer E-Mail. |
| **Mahnung** | Druckt eine Gelangensbestätigungsmahnung für die überfälligen markierten Zeilen und erhöht die Mahnstufe. |
| **Mahnung per Mail senden** | Versendet die Gelangensbestätigungsmahnung als E-Mail über den Belegversand. |
| **Sammelmahnung** | Druckt eine zusammengefasste Mahnung über mehrere Bestätigungen. |
| **Sammelmahnung per Mail senden** | Versendet die zusammengefasste Mahnung als E-Mail. |
| **Gelangensbestätigung erhalten** | Markiert die Bestätigung als erhalten und setzt den zugehörigen Status; das **Empfangsdatum** wird gesetzt. Danach ist keine Mahnung mehr nötig. |
| **Gelangensbestätigung erhalten zurücksetzen** | Nimmt die Kennzeichnung „erhalten“ zurück, falsch bestätigte Zeilen werden wieder in die Nachverfolgung aufgenommen. |

### Ablauf beim Mailversand

Wenn Sie **Gelangensbestätigung per Mail senden** wählen, läuft im Hintergrund folgende Kette:

1. Das Modul ermittelt zur Gelangensbestätigung den zugehörigen Beleg (die **Verkaufslieferung**) für den Anhang.
2. Anhand von **Art** (Debitor/Kreditor) und **Debitoren-/Kreditorennr.** wird das passende **Belegversandprofil** nach Priorität ausgewählt.
3. Empfänger (**An**, **CC**, **BCC**, zusätzliche Empfänger) und der **Sprachcode** werden aus Profil und Geschäftspartner vorbelegt.
4. Der Belegversand erstellt die E-Mail mit den Anhängen gemäß Profil (**Anzahl Anhänge**, **ZIP-Option**, **Max. MB**).
5. Vor dem Senden können Sie Empfänger, Betreff, Nachrichtentext und Anhänge kontrollieren und bei Bedarf anpassen; anschließend versenden Sie die E-Mail.

## Berechtigungen

Für das Modul steht der Berechtigungssatz **MuM CSRD All** bereit. Er bestimmt die Berechtigungen für die Ausführung der modulinternen Logik, die den Versand der Gelangensbestätigung über den Belegversand freischaltet. Weisen Sie diesen Berechtigungssatz allen Benutzern zu, die Gelangensbestätigungen versenden oder drucken sollen. Zusätzlich benötigen die Anwender die Berechtigungen der Module m+m Gelangensbestätigung und m+m Belegversand für die dort liegenden Seiten und Belegversandprofile.

## FAQ und Troubleshooting

### Warum wird beim Mailversand kein Empfänger vorgeschlagen?
Weil für den betreffenden Debitor bzw. Kreditor kein **Belegversandprofil** mit passender **Belegart** angelegt ist. Das Modul wählt das Profil nach Herkunftsart, Herkunftsnr. und Belegart aus; ohne passende Zeile findet es keinen Empfänger. Legen Sie das Profil in **m+m Belegversandprofile** an.

### Was passiert, wenn ich statt „per Mail senden“ die Aktion „drucken“ wähle?
Dann wird die Gelangensbestätigung nur gedruckt und das Feld **Gedruckt** gesetzt. Der Belegversand und die Empfängerermittlung dieses Moduls werden dabei nicht aktiviert.

### In welcher Sprache wird die E-Mail erstellt?
In der Sprache des Empfängers: Das Modul zieht den **Sprachcode** automatisch aus dem Debitor bzw. Kreditor der Gelangensbestätigung.

### Warum kann ich für „alle Debitoren“ kein Sammelprofil anlegen?
Weil je Debitor bzw. Kreditor eine eigene Profilzeile erforderlich ist. Wählen Sie als **Herkunftsart** Debitor oder Kreditor und tragen Sie die konkrete **Herkunftsnr.** ein; ein Profil „für alle Debitoren“ ist nicht vorgesehen.

### Wie stelle ich sicher, dass zusätzliche Dokumente mitgesendet werden?
Über das Feld **Anzahl Anhänge** im Belegversandprofil. Klicken Sie in das Feld und hinterlegen Sie die zusätzlichen Belege oder Dateien; der eigentliche Nachweis wird ohnehin angehängt.

### Was bewirkt die Einstellung „Zusätzlich zum Standard“?
Sie steuert nur das **An**-Feld: **Standard** nutzt allein die Profiladressen, **Nur Standard** allein die BC-Standardadressen, **Ja** beide zusammen und **Nachfrage** fragt beim Versand nach. Auf CC und BCC hat die Einstellung keine Wirkung.

### Warum wird meine E-Mail in mehrere Teile aufgeteilt?
Weil die Summe der Anhänge den Wert **Max. MB** überschreitet. Der Belegversand teilt die E-Mail dann in nummerierte Teil-E-Mails auf. Überschreitet bereits eine einzelne Datei die Grenze, erscheint eine Fehlermeldung.

### Wann wird eine Mahnung fällig?
Wenn das **Fälligkeitsdatum** überschritten ist und die Bestätigung noch nicht als **erhalten** markiert wurde. Das Fälligkeitsdatum ergibt sich aus dem Liefer-/Buchungsdatum und der **Standard Fälligkeitsberechnungsformel** aus der Gelangensbestätigungseinrichtung.

### Wie fasse ich mehrere Bestätigungen für einen Empfänger zusammen?
Markieren Sie die Zeilen und wählen Sie **Gelangensbestätigungen zusammenfassen**. Die Bestätigungen erhalten eine gemeinsame **Zertifikatsnr.** und können danach über **Sammeldruck Gelangensbestätigung** oder **Sammelgelangensbestätigung per Mail senden** gebündelt versendet werden.

### Ich habe eine Bestätigung versehentlich als erhalten markiert – wie korrigiere ich das?
Wählen Sie **Gelangensbestätigung erhalten zurücksetzen**. Die Kennzeichnung wird entfernt und die Zeile kehrt in die Nachverfolgung zurück.

## Typische Anwendungsfälle

### Anwendungsfall 1: Gelangensbestätigung per E-Mail an einen Debitor senden

**Auslöser.** Eine Lieferung an einen Debitor im EU-Ausland wurde gebucht; der steuerliche Nachweis (Gelangensbestätigung) soll dem Debitor per E-Mail zugestellt werden.

**Einstieg in BC.** Der Administrator hat vorab in **m+m Belegversandprofile** eine Zeile mit **Herkunftsart** Debitor, der **Herkunftsnr.** des Kunden, **Art** E-Mail und der passenden **Belegart** angelegt. Der Anwender öffnet die Liste **Gelangensbestätigungen**.

**Kernablauf.**
1. Der Anwender markiert die Zeile mit der **Belegart** Verkaufslieferung und der passenden **Debitoren-/Kreditorennr.**.
2. Er wählt **Gelangensbestätigung per Mail senden**.
3. Das Modul ermittelt die zugehörige Verkaufslieferung, zieht das Belegversandprofil des Debitors und belegt Empfänger und **Sprachcode** vor.
4. Der Anwender kontrolliert Empfänger, Betreff und Anhänge und versendet die E-Mail.

**Abschluss.** Sobald der Debitor den Nachweis bestätigt, markiert der Anwender die Zeile über **Gelangensbestätigung erhalten**; das **Empfangsdatum** wird gesetzt und eine Mahnung entfällt.

### Anwendungsfall 2: Überfällige Bestätigung anmahnen

**Auslöser.** Das **Fälligkeitsdatum** einer Gelangensbestätigung ist überschritten und der **Status** zeigt weiterhin an, dass der Nachweis nicht erhalten wurde.

**Einstieg in BC.** Der Anwender öffnet die Liste **Gelangensbestätigungen** und filtert bzw. sortiert nach **Fälligkeitsdatum** und **Mahnstufe**.

**Kernablauf.**
1. Der Anwender markiert die überfällige Zeile.
2. Er wählt **Mahnung per Mail senden** (oder **Mahnung** für den reinen Druck).
3. Das Modul versendet die **Gelangensbestätigungsmahnung** über den Belegversand an den Empfänger aus dem Belegversandprofil; die **Mahnstufe** wird erhöht.

**Abschluss.** Trifft der Nachweis daraufhin ein, markiert der Anwender die Zeile über **Gelangensbestätigung erhalten**. Bei mehreren überfälligen Bestätigungen desselben Empfängers kann zuvor über **Gelangensbestätigungen zusammenfassen** und **Sammelmahnung per Mail senden** gebündelt gemahnt werden.
