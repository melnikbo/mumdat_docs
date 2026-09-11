---
title: Anwenderhandbuch m+m Prod. Order Job Overview Steel with Prod. Differences
---

# Anwenderhandbuch m+m Prod. Order Job Overview Steel with Prod. Differences

## Einleitung

Die App **m+m Prod. Order Job Overview Steel with Prod. Differences** verbindet die Über-/Unterproduktionskontrolle aus dem Modul **Über-/Unterproduktion** mit dem **FA-Arbeitsvorrat** für die Stahlfertigung. Die App bringt keine eigenen Seiten, Felder oder Stammdaten mit. Sie sorgt allein dafür, dass die im Produktionsauftrag hinterlegten Über-/Unterproduktionsregeln beim Abschluss der Meldung im **FA-Arbeitsvorrat** greifen – und zwar gezielt im **letzten Arbeitsgang**.

Konkret prüft die App im FA-Arbeitsvorrat, wenn der Anwender die erfasste Charge-Erfassung des verantwortlichen Materials abschließt, ob die gemeldete **Menge** die für den Artikel zulässige **Ursprüngliche Menge** unter Berücksichtigung der Über-/Unterproduktionsregeln überschreitet oder unterschreitet. Ist die gemeldete Menge außerhalb des erlaubten Bereichs, gibt das System – abhängig von der Einrichtung – eine Bestätigungsabfrage aus oder blockiert den Abschluss mit einer Benachrichtigung.

**Zielgruppe.** Primäre Zielgruppe sind **operative Fertigungsanwender**, die im FA-Arbeitsvorrat Rückmeldungen erfassen, Chargen zuordnen und den letzten Arbeitsgang eines Fertigungsauftrags abschließen. Sekundäre Zielgruppe sind **Administratoren und Fertigungsplaner**, welche die zugrunde liegenden Über-/Unterproduktionsregeln im Modul Über-/Unterproduktion einrichten.

**Kurzer Prozessüberblick.**

1. Der Administrator richtet im Modul Über-/Unterproduktion die zulässigen Abweichungen ein (global, je Artikel, mit Ausnahmen).
2. Im Produktionsauftrag wird die **Ursprüngliche Menge** je Zeile gesetzt; sie ist die Vergleichsbasis.
3. Der Anwender öffnet den **FA-Arbeitsvorrat**, filtert seine **Arbeitsplatzgruppennr.** und meldet den Fertigungsauftrag zurück.
4. Beim Abschluss der Charge-Erfassung des verantwortlichen Materials im letzten Arbeitsgang prüft diese App die gemeldete Menge gegen die Regeln.
5. Innerhalb der Grenzen wird der Abschluss durchgeführt; außerhalb der Grenzen folgt eine Bestätigungsabfrage oder eine blockierende Benachrichtigung.

> Diese App wirkt ausschließlich als Bindeglied. Die vollständige Einrichtung der Regeln erfolgt im Modul Über-/Unterproduktion; die Meldung selbst erfolgt im FA-Arbeitsvorrat. Beide Bereiche sind unten so beschrieben, dass Sie den Prozess ohne ein zweites Handbuch nachvollziehen können.

## Schnellstart für Anwender

Der Schnellstart folgt der erzwungenen Reihenfolge aus dem Code: zuerst Einrichtung, dann Meldung im FA-Arbeitsvorrat, dann die Prüfung beim Abschluss.

**A. Einrichtung (einmalig, durch den Administrator).**

1. Öffnen Sie über **Suchen** die **Über-/Unterproduktionseinrichtung** und legen Sie die Standardregeln je **Kontrollart** (**Überproduktion**/**Unterproduktion**) mit **Kontrollmethode**, **Wert** und **Warnung** fest.
2. Hinterlegen Sie bei Bedarf je Artikel abweichende Regeln in der **Über-/Unterproduktion Artikeleinrichtung** und Ausnahmen in der **Über-/Unterproduktion Ausnahmeeinrichtung**.
3. Stellen Sie sicher, dass im freigegebenen Fertigungsauftrag je Zeile die **Ursprüngliche Menge** gesetzt ist (Aktion **Ursprüngliche Menge setzen**).

**B. Meldung und Prüfung (täglich, durch den Anwender).**

1. Öffnen Sie über **Suchen** den **FA-Arbeitsvorrat**.
2. Filtern Sie zuerst die **Arbeitsplatzgruppennr.**; grenzen Sie optional zusätzlich die **Arbeitsplatznr.** ein.
3. Wählen Sie die Zeile des gestarteten Fertigungsauftrags und starten Sie den Abschluss; es öffnet sich die **FA-Arbeitsvorrat Buchung**.
4. Erfassen Sie im Schritt für das verantwortliche Material die Chargen: **Chargennr.** und **Menge**; teilen Sie bei Restmengen über **Restecharge erstellen** eine Restecharge ab.
5. Schließen Sie die Charge-Erfassung. Diese App prüft nun die Summe der gemeldeten Menge gegen die Über-/Unterproduktionsregeln des letzten Arbeitsgangs:
   - **Innerhalb der Grenzen:** Der Abschluss wird ohne Rückfrage durchgeführt.
   - **Außerhalb der Grenzen mit Warnung:** Es erscheint die Bestätigungsabfrage „Sie überschreiten die erlaubten Werte … Wollen Sie fortfahren?“. Bei **Ja** wird abgeschlossen, bei **Nein** bleiben Sie in der Erfassung.
   - **Außerhalb der Grenzen ohne Warnung:** Der Abschluss wird blockiert und eine Benachrichtigung verweist auf die Über-/Unterproduktionsregeln.

## Einrichtung

Die Über-/Unterproduktionskontrolle, die diese App im FA-Arbeitsvorrat auslöst, wird vollständig im Modul **Über-/Unterproduktion** konfiguriert. BC-Anwender sehen dort mehrere zusammenhängende Seiten; dieser Abschnitt beschreibt sie in der Reihenfolge, in der sie eingerichtet werden, und verknüpft sie mit der täglichen Arbeit im FA-Arbeitsvorrat.

### Grundlogik: was die App tatsächlich prüft

Diese App liest die Einrichtungswerte aus dem Modul Über-/Unterproduktion und wendet sie beim Abschluss der Charge-Erfassung an. Sie schreibt selbst keine Einrichtung. Für das Verständnis der folgenden Tabellen sind zwei Begriffe zentral:

- **Ursprüngliche Menge** – die zum Zeitpunkt der Zeilenerstellung festgehaltene Sollmenge des Fertigungsauftrags. Sie ist die Vergleichsbasis für jede Prüfung. Wird sie nicht gesetzt, kann die Kontrolle nicht sinnvoll greifen.
- **Gemeldete Menge** – die Summe der in der Charge-Erfassung gemeldeten **Menge** des Arbeitsgangs, ergänzt um bereits **Gebuchte Menge** aus vorgelagerten Vorgängen bzw. aus Artikelposten des letzten Arbeitsgangs. Diese Summe vergleicht die App mit der zulässigen Grenze.

### Über-/Unterproduktionseinrichtung (globale Standardregeln)

**Prozessintro.** Diese globale Einrichtungsseite konfiguriert der **Administrator einmalig vor der ersten Nutzung**. Sie legt die Standardregeln fest, die gelten, solange kein spezifischerer Artikel-Eintrag existiert. Die hier definierten Werte werden bei der Zeilenerstellung in den Fertigungsauftrag übernommen und von dieser App im FA-Arbeitsvorrat ausgewertet (siehe **Tägliche Arbeit**).

**Einstieg:** Öffnen Sie die **Über-/Unterproduktionseinrichtung** über **Suchen** (unternehmensweite Einzeleinrichtung).

Je **Kontrollart** wird eine Standardregel gepflegt:

| Einrichtung | Erläuterung |
|---|---|
| Kontrollart | Bestimmt, für welche Abweichungsrichtung die Regel gilt. **Überproduktion:** Regel greift, wenn die gemeldete Menge über der Ursprünglichen Menge liegt. **Unterproduktion:** Regel greift, wenn die gemeldete Menge unter der Ursprünglichen Menge liegt. |
| Kontrollmethode | Bestimmt, wie die zulässige Grenze berechnet wird. **Vorgabe:** Wenn gesetzt, gilt das Standardverhalten von Business Central und diese App greift nicht ein – es findet keine zusätzliche Prüfung statt. **Prozentsatz:** Wenn gesetzt, wird die Grenze als prozentualer Auf-/Abschlag auf die Ursprüngliche Menge berechnet. **Absoluter Wert:** Wenn gesetzt, wird die Grenze als fester Mengenbetrag über/unter der Ursprünglichen Menge berechnet. |
| Wert | Wenn ein Wert gesetzt ist, definiert er die zulässige Abweichung: bei **Prozentsatz** den Prozentanteil der Ursprünglichen Menge, bei **Absoluter Wert** die feste Zusatz- bzw. Fehlmenge. Bei **Vorgabe** ist das Feld ohne Wirkung und nicht änderbar. |
| Warnung | Wenn **aktiviert**, darf der Anwender eine Grenzüberschreitung im FA-Arbeitsvorrat nach einer Bestätigungsabfrage übersteuern und den Abschluss trotzdem durchführen; jede Bestätigung wird protokolliert. Wenn **deaktiviert**, wird der Abschluss bei Grenzüberschreitung blockiert und der Anwender erhält lediglich eine Benachrichtigung. |

Zusätzlich steuert auf der allgemeinen Registerkarte das Feld **Update Herkunftsbeleg** das Standardverhalten der Belegaktualisierung:

| Einrichtung | Erläuterung |
|---|---|
| Update Herkunftsbeleg | Wenn **aktiviert**, wird beim Buchen einer Überproduktion der auslösende Herkunftsbeleg (z. B. Verkaufsauftrag) in Menge und Reservierung nachgezogen; wenn **deaktiviert**, bleibt der Herkunftsbeleg unverändert. Der Wert ist ein Vorgabewert, der in den Fertigungsauftrag kopiert und dort je Auftrag noch geändert werden kann. |

> Standardwerte greifen nur, solange keine spezifische Artikeleinrichtung vorliegt. Von dieser Seite aus erreichen Sie über Funktionen die **Über-/Unterproduktion Artikeleinrichtung** und die **Über-/Unterproduktion Ausnahmeeinrichtung**.

### Über-/Unterproduktion Artikeleinrichtung (spezifische Regeln je Artikel)

**Prozessintro.** Der Administrator pflegt hier **feiner abgestufte Regeln**, sobald einzelne Artikel oder Debitoren von der Standardregel abweichen sollen. Diese Einträge haben Vorrang vor der globalen Standardregel und werden von dieser App im FA-Arbeitsvorrat berücksichtigt.

**Einstieg:** Öffnen Sie in der **Über-/Unterproduktionseinrichtung** die Funktion für die **Über-/Unterproduktion Artikeleinrichtung**.

| Einrichtung | Erläuterung |
|---|---|
| Kontrollart | Wenn gesetzt, entscheidet, ob die Zeile die **Überproduktion** oder die **Unterproduktion** dieses Artikels regelt. |
| Artikelart | Grenzt ein, für welche Artikel die Regel gilt: **Alle Artikel** (Regel wirkt allgemein) oder **Artikel** (Regel wirkt nur für die unter Artikelnr. genannte Nummer). |
| Artikelnr. | Wenn gesetzt, gilt die Einrichtungszeile genau für diesen Artikel; im FA-Arbeitsvorrat wird die Regel dann nur für Fertigungsaufträge dieses Artikels ausgewertet. |
| Artikelvariante | Wenn gesetzt, verengt die Regel zusätzlich auf die angegebene Variante des Artikels; ohne Angabe gilt sie für alle Varianten. |
| Referenzart | Bestimmt den Geltungsbereich hinsichtlich des Debitors. **Alle Debitoren:** Regel gilt unabhängig vom Kunden. **Debitor:** Regel gilt nur für den unter Referenz Nr. genannten Debitor des Fertigungsauftrags. |
| Referenz Nr. | Wenn die Referenzart **Debitor** ist, muss hier der Debitor eingetragen werden; nur dann greift die Regel kundenspezifisch. Bei **Alle Debitoren** bleibt das Feld leer. |
| Kontrollmethode | Wie in der globalen Einrichtung: **Vorgabe** (keine Wirkung dieser App), **Prozentsatz** (prozentuale Grenze) oder **Absoluter Wert** (feste Grenzmenge). |
| Warnung | Wenn **aktiviert**, ist die Grenze im FA-Arbeitsvorrat per Bestätigung übersteuerbar; wenn **deaktiviert**, blockiert eine Grenzüberschreitung den Abschluss. Bei Kontrollmethode **Vorgabe** ist das Feld nicht änderbar. |
| Wert | Wenn gesetzt, legt die zulässige Abweichung fest (Prozentanteil bzw. absolute Menge). Bei **Vorgabe** ohne Wirkung. |

### Über-/Unterproduktion Ausnahmeeinrichtung (Ausnahmen zu den Artikelregeln)

**Prozessintro.** Ausnahmen dienen dazu, einzelne Konstellationen von der Kontrolle **auszunehmen**. Trifft eine Ausnahme auf den Fertigungsauftrag zu, ignoriert diese App die betreffende Artikeleinrichtung und meldet die Konstellation als unzulässig zurück, statt eine Grenze zu berechnen. Der Administrator pflegt Ausnahmen ergänzend zur Artikeleinrichtung.

**Einstieg:** Öffnen Sie in der **Über-/Unterproduktionseinrichtung** die Funktion für die **Über-/Unterproduktion Ausnahmeeinrichtung**.

Zentrales Steuerfeld ist die **Ausnahmeart**. Sie bestimmt, worauf die Ausnahme angewendet wird. Die App wertet beim Abschluss der Meldung jede der folgenden Ausnahmearten aus:

| Einrichtung | Erläuterung |
|---|---|
| Kontrollart | Wenn gesetzt, gilt die Ausnahme entweder für **Überproduktion** oder für **Unterproduktion**. |
| Ausnahmeart | Bestimmt das Kriterium der Ausnahme (Werte siehe folgende Liste). Trifft der Wert auf den Fertigungsauftrag zu, wird die zugehörige Artikeleinrichtung übergangen und der Abschluss blockiert. |

Die **Ausnahmeart** kennt folgende Werte; alle werden von dieser App geprüft:

- **Alle Artikel:** Die Ausnahme gilt unabhängig vom konkreten Artikel; jede Über-/Unterproduktion dieser Kontrollart ist ausgenommen.
- **Artikel:** Die Ausnahme gilt nur für den im Ausnahmewert genannten Artikel des Fertigungsauftrags.
- **Artikelvariante:** Die Ausnahme gilt für die Kombination aus Artikel und der angegebenen Variante.
- **Artikelkategorie:** Die Ausnahme gilt für alle Artikel der angegebenen Artikelkategorie.
- **Produktbuchungsgruppe:** Die Ausnahme gilt für alle Artikel mit der angegebenen Produktbuchungsgruppe.
- **Lagerbuchungsgruppe:** Die Ausnahme gilt für alle Artikel mit der angegebenen Lagerbuchungsgruppe.
- **Beschaffungsmethode:** Die Ausnahme gilt für alle Artikel mit der angegebenen Beschaffungsmethode.
- **Debitor:** Die Ausnahme gilt für den angegebenen Debitor des Fertigungsauftrags.
- **Alle Debitoren:** Die Ausnahme gilt debitorenübergreifend.

> Wirkung im Prozess: Findet die App zu einem Fertigungsauftrag eine passende Ausnahme, erzeugt sie beim Abschluss eine Benachrichtigung und lässt den Abschluss nicht zu – unabhängig von den sonst berechneten Grenzen.

### Über-/Unterproduktionskontrolle im FA-Arbeitsvorrat einrichten

**Prozessintro.** Damit die Kontrolle beim Abschluss im FA-Arbeitsvorrat wirklich greift, müssen mehrere Einstellungen in Abhängigkeitsreihenfolge zusammenspielen: erst die Regelbasis, dann die Sollmenge je Auftrag, schließlich die Meldung im letzten Arbeitsgang. Diese Einrichtung betrifft **Administrator** (Regeln) und **Fertigungsplaner** (Ursprüngliche Menge); ausgelöst wird die Kontrolle später vom **operativen Anwender** in der täglichen Arbeit (siehe **Tägliche Arbeit im FA-Arbeitsvorrat**).

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Standardregel festlegen.** Pflegen Sie in der **Über-/Unterproduktionseinrichtung** je **Kontrollart** die **Kontrollmethode**, den **Wert** und die **Warnung**. Wenn Sie hier **Vorgabe** wählen, dann findet keine Kontrolle durch diese App statt; wählen Sie **Prozentsatz** oder **Absoluter Wert**, dann wird eine Grenze berechnet.
2. **Artikelabweichungen pflegen (optional).** Wenn ein Artikel oder Debitor abweichende Grenzen benötigt, dann erfassen Sie einen Eintrag in der **Über-/Unterproduktion Artikeleinrichtung**; dieser Eintrag hat Vorrang vor der Standardregel.
3. **Ausnahmen definieren (optional).** Wenn bestimmte Artikel, Kategorien, Buchungsgruppen, Beschaffungsmethoden oder Debitoren gar keine Abweichung erlauben sollen, dann hinterlegen Sie eine passende **Ausnahmeart** in der **Über-/Unterproduktion Ausnahmeeinrichtung**; die App blockiert dann den Abschluss dieser Konstellationen.
4. **Ursprüngliche Menge setzen.** Stellen Sie je Zeile des freigegebenen Fertigungsauftrags sicher, dass die **Ursprüngliche Menge** gesetzt ist (Aktion **Ursprüngliche Menge setzen**). Wenn dieser Wert fehlt, dann fehlt die Vergleichsbasis und die Kontrolle kann nicht korrekt rechnen.

**Operativer Abschluss der Kette.** Der Anwender schließt im **FA-Arbeitsvorrat** über die **FA-Arbeitsvorrat Buchung** die Charge-Erfassung des verantwortlichen Materials im letzten Arbeitsgang ab. Erst dieser Abschluss löst die von dieser App eingefügte Prüfung aus. Die operative Beschreibung finden Sie im Abschnitt **Tägliche Arbeit im FA-Arbeitsvorrat**.

## Tägliche Arbeit im FA-Arbeitsvorrat

Dieser Abschnitt beschreibt die transaktionale Arbeit, in der diese App wirkt. Steuernd sind die unter **Einrichtung** beschriebenen Seiten: die **Über-/Unterproduktionseinrichtung** (Standardregeln), die **Über-/Unterproduktion Artikeleinrichtung** (artikelspezifische Grenzen) und die **Über-/Unterproduktion Ausnahmeeinrichtung** (Ausnahmen) legen fest, ob und wie beim Abschluss geprüft wird; die **Ursprüngliche Menge** im Fertigungsauftrag liefert die Vergleichsbasis.

### Einstieg über den FA-Arbeitsvorrat

**Einstieg:** Öffnen Sie über **Suchen** den **FA-Arbeitsvorrat**.

1. Filtern Sie zuerst die **Arbeitsplatzgruppennr.**; es erscheinen die zugehörigen Fertigungsaufträge.
2. Grenzen Sie optional zusätzlich die **Arbeitsplatznr.** ein, wenn Sie nur einen bestimmten Arbeitsplatz sehen möchten.
3. Wählen Sie die Zeile des gestarteten Fertigungsauftrags, den Sie zurückmelden möchten.

### Charge-Erfassung des verantwortlichen Materials

Beim Abschluss eines gestarteten Fertigungsauftrags öffnet sich die **FA-Arbeitsvorrat Buchung**. Im Schritt für das verantwortliche Material erfassen Sie die verbrauchten bzw. gemeldeten Chargen. Die relevanten Felder:

| Feld | Erläuterung |
|---|---|
| Chargennr. | Identifiziert die gemeldete Charge; über die Chargennr. ordnet das System die Menge dem Arbeitsgang und den Artikelposten zu. |
| Lagerbestand | Zeigt den verfügbaren Bestand der Charge an; er hilft dem Anwender zu erkennen, welche Menge aus der Charge noch entnommen werden kann. Kein Eingabefeld. |
| Menge | Die für diese Charge gemeldete Menge. Diese Menge fließt in die Summe ein, die diese App beim Abschluss gegen die Über-/Unterproduktionsgrenze prüft. |
| Gebuchte Menge | Zeigt die bereits gebuchte Menge der Charge an. Bei einem nachfolgenden Arbeitsgang bzw. wenn zum letzten Arbeitsgang kein Artikelposten (Ausgang) existiert, addiert die App diese Menge zur Prüfsumme hinzu. |

**Restecharge abtrennen.** Bleibt aus dem gemeldeten Material eine Restmenge übrig, trennen Sie über die Aktion **Restecharge erstellen** eine **Restecharge** ab. In den Zeilen der Restecharge pflegen Sie insbesondere:

| Feld | Erläuterung |
|---|---|
| Chargennr. | Nummer der neu entstehenden Restecharge. |
| Menge | Restmenge, die als eigene Charge weitergeführt wird. |
| Neue FA-Zeilennr. | Verknüpft die Restecharge mit der Fertigungsauftragszeile, in der sie weiterverwendet wird. |

> Eine bereits gebuchte Zeile lässt keine Mengenänderung mehr zu; die **Menge** kann nach dem Buchen nicht mehr geändert werden.

### Prüfung beim Abschluss (letzter Arbeitsgang)

Wenn Sie die Charge-Erfassung des verantwortlichen Materials schließen, führt diese App die Über-/Unterproduktionsprüfung aus. Maßgeblich ist, dass es sich um den **letzten Arbeitsgang** handelt: Ist der Arbeitsgang bereits als abgeschlossen markiert, findet keine Prüfung statt. Andernfalls läuft folgender Ablauf – dieselben Schritte wie im Schnellstart:

1. Auf **FA-Arbeitsvorrat** die Zeile des gestarteten Fertigungsauftrags wählen.
2. Abschluss starten → **FA-Arbeitsvorrat Buchung** öffnet sich.
3. Chargen erfassen (**Chargennr.**, **Menge**), bei Bedarf **Restecharge erstellen**; Erfassung schließen.
4. Die App summiert die gemeldete **Menge** des Arbeitsgangs (zzgl. **Gebuchte Menge** gemäß Regel) und vergleicht sie mit der zulässigen Grenze aus **Ursprüngliche Menge** und Einrichtung.
5. Ergebnis:
   - **Innerhalb der Grenzen:** Abschluss ohne Rückfrage.
   - **Grenze überschritten, Warnung aktiv:** Bestätigungsabfrage „Sie überschreiten die erlaubten Werte … Wollen Sie fortfahren?“ – bei **Ja** wird abgeschlossen, bei **Nein** bleiben Sie in der Erfassung.
   - **Grenze überschritten, Warnung inaktiv:** Abschluss blockiert; Benachrichtigung verweist auf die Über-/Unterproduktionsregeln.
   - **Ausnahme greift:** Abschluss blockiert; Benachrichtigung, dass die Konstellation nicht zulässig ist.

## Über-/Unterproduktionsprüfung im Detail

Dieser Abschnitt erläutert die Logik, die diese App beim Abschluss ausführt, damit Anwender die Meldungen einordnen können. Alle Aussagen sind aus dem Verhalten der App abgeleitet.

### Wann geprüft wird

Die Prüfung wird nur ausgelöst, wenn der betroffene Arbeitsgang **nicht** bereits abgeschlossen ist. Für abgeschlossene Arbeitsgänge unterbleibt jede Kontrolle. Damit greift die Kontrolle wie vorgesehen im **letzten offenen Arbeitsgang** der Rückmeldung.

### Wie die Menge ermittelt wird

Die App bildet die Summe der gemeldeten **Menge** über alle verantwortlichen Chargen des Arbeitsgangs. Existiert ein nachfolgender Arbeitsgang, wird zusätzlich die bereits **Gebuchte Menge** der Chargen hinzugerechnet. Gibt es keinen nachfolgenden Arbeitsgang (letzter Arbeitsgang) und liegt für die Charge kein Artikelposten mit Ausgang vor, wird die **Gebuchte Menge** ebenfalls hinzugerechnet. Zu dieser Summe wird die bereits **Fertiggestellte Menge** der Zeile addiert und mit der **Ursprünglichen Menge** verglichen.

### Wie die Grenze berechnet wird

- Liegt die Summe **über** der Ursprünglichen Menge, greift die **Überproduktion**-Regel; liegt sie **darunter**, greift die **Unterproduktion**-Regel.
- Bei **Kontrollmethode = Vorgabe** greift die App nicht ein.
- Bei **Absoluter Wert** ist die Grenze die Ursprüngliche Menge plus bzw. minus dem eingerichteten **Wert**.
- Bei **Prozentsatz** ist die Grenze die Ursprüngliche Menge plus bzw. minus dem prozentualen Anteil des **Werts**.
- Für Artikel mit Seriennummernverfolgung wird die zulässige Grenze auf ganze Einheiten abgerundet.

### Bestätigung, Benachrichtigung und Protokoll

- Ist **Warnung** aktiv und die Grenze überschritten, erscheint die Bestätigungsabfrage. Bei Zustimmung wird die Aktion im **Über-/Unterproduktion Benutzeraktivitätsprotokoll** festgehalten.
- Ist **Warnung** inaktiv und die Grenze überschritten, erscheint statt der Rückfrage eine Benachrichtigung; der Abschluss wird nicht durchgeführt.
- Greift eine **Ausnahme**, erscheint eine Benachrichtigung, dass die Über-/Unterproduktion für diese Konstellation nicht zulässig ist.

Das **Über-/Unterproduktion Benutzeraktivitätsprotokoll** hält je Vorgang unter anderem folgende Angaben fest:

| Feld | Erläuterung |
|---|---|
| Definiert | Gibt an, ob der protokollierte Vorgang eine **Überproduktion** oder eine **Unterproduktion** betraf. |
| Ursprüngliche Menge | Die zum Zeitpunkt des Vorgangs gültige Sollmenge der Zeile. |
| Begrenzte Menge | Die aus Ursprünglicher Menge und Regel berechnete zulässige Grenze. |
| Finale Menge | Die tatsächlich gemeldete Menge, die den Vorgang ausgelöst hat. |
| Datum/Uhrzeit | Zeitpunkt des Vorgangs. |
| Benutzer | Anwender, der den Vorgang ausgelöst hat. |
| Artikelnr. | Betroffener Artikel des Fertigungsauftrags. |

## Berechtigungen

Die App liefert den zuweisbaren Berechtigungssatz **MuM STOP Perm** mit. Er legt fest, welche Aktionen Anwender im Rahmen dieser App ausführen dürfen, indem er die Ausführung der internen Prüf- und Protokolllogik gestattet. Ordnen Sie den Berechtigungssatz den Anwendern zu, die im FA-Arbeitsvorrat den letzten Arbeitsgang abschließen; ohne diese Berechtigung kann die Über-/Unterproduktionsprüfung nicht ausgeführt werden. Die Berechtigungen für die eigentlichen Einrichtungs- und Meldeseiten werden über die Berechtigungssätze der Module Über-/Unterproduktion und FA-Arbeitsvorrat bestimmt.

## FAQ und Troubleshooting

### Warum erscheint beim Abschluss keine Über-/Unterproduktionsabfrage, obwohl ich mehr melde als bestellt?
Prüfen Sie die **Kontrollmethode**. Steht sie auf **Vorgabe**, greift diese App nicht ein; erst **Prozentsatz** oder **Absoluter Wert** aktivieren die Kontrolle. Prüfen Sie außerdem, ob die **Ursprüngliche Menge** gesetzt ist, da ohne Vergleichsbasis nicht gerechnet werden kann.

### Warum wird die Prüfung nur im letzten Arbeitsgang ausgelöst?
Die App prüft bewusst beim Abschluss der Meldung des offenen Arbeitsgangs. Ist der Arbeitsgang bereits als abgeschlossen markiert, unterbleibt die Prüfung. Dadurch wird die Über-/Unterproduktion an der Stelle kontrolliert, an der die fertige Menge feststeht.

### Was bedeutet die Meldung „Sie überschreiten die erlaubten Werte … Wollen Sie fortfahren?“
Ihre gemeldete **Menge** liegt außerhalb der zulässigen Grenze, und für die Regel ist **Warnung** aktiv. Mit **Ja** übersteuern Sie die Grenze und schließen ab; mit **Nein** bleiben Sie in der Erfassung, ohne zu buchen. Ihre Zustimmung wird protokolliert.

### Warum kann ich den Abschluss gar nicht durchführen und sehe nur eine Benachrichtigung?
Für die geltende Regel ist **Warnung** deaktiviert, oder es greift eine **Ausnahme**. In beiden Fällen ist ein Übersteuern nicht vorgesehen; die Benachrichtigung verweist auf die Über-/Unterproduktionsregeln. Passen Sie die Menge an oder lassen Sie die Regel bzw. die Ausnahme durch den Administrator prüfen.

### Wo lege ich fest, wie stark eine Abweichung sein darf?
In der **Über-/Unterproduktionseinrichtung** über **Kontrollmethode** und **Wert**: **Absoluter Wert** definiert eine feste Zusatz-/Fehlmenge, **Prozentsatz** einen prozentualen Anteil der Ursprünglichen Menge. Für einzelne Artikel oder Debitoren verwenden Sie die **Über-/Unterproduktion Artikeleinrichtung**.

### Warum gilt für einen bestimmten Artikel eine andere Grenze als der Standard?
Weil in der **Über-/Unterproduktion Artikeleinrichtung** ein passender Eintrag existiert. Solche artikel- oder debitorenspezifischen Regeln haben Vorrang vor der globalen Standardregel.

### Warum wird für einen Artikel überhaupt keine Über-/Unterproduktion erlaubt?
Dann greift eine **Ausnahme** in der **Über-/Unterproduktion Ausnahmeeinrichtung**, deren **Ausnahmeart** auf den Fertigungsauftrag zutrifft (z. B. **Artikel**, **Artikelkategorie**, **Produktbuchungsgruppe**, **Lagerbuchungsgruppe**, **Beschaffungsmethode** oder **Debitor**). Die App übergeht in diesem Fall die Artikeleinrichtung und blockiert den Abschluss.

### Wozu dient die Aktion Restecharge erstellen?
Damit trennen Sie aus dem gemeldeten Material eine **Restecharge** ab und führen die Restmenge als eigene Charge weiter, verknüpft über die **Neue FA-Zeilennr.**. Die Aktion ändert nichts an der Über-/Unterproduktionsprüfung; die gemeldete **Menge** bleibt die Prüfbasis.

### Warum kann ich die Menge einer Charge nicht mehr ändern?
Sobald eine Zeile gebucht ist, ist die **Menge** gesperrt. Eine gebuchte Charge lässt keine nachträgliche Mengenänderung an dieser Stelle zu; korrigieren Sie über die dafür vorgesehenen Fertigungsprozesse.

### Wo sehe ich, dass eine Grenzüberschreitung genehmigt wurde?
Im **Über-/Unterproduktion Benutzeraktivitätsprotokoll**. Dort werden **Definiert** (Über-/Unterproduktion), **Ursprüngliche Menge**, **Begrenzte Menge**, **Finale Menge**, **Datum/Uhrzeit**, **Benutzer** und **Artikelnr.** festgehalten, sodass die Genehmigung später nachvollziehbar ist.

## Typische Anwendungsfälle

### Anwendungsfall 1 – Überproduktion mit Warnung im letzten Arbeitsgang

**Auslöser.** Ein Werker meldet am Ende der Fertigung mehr Gutstücke, als der Fertigungsauftrag vorsah, weil die letzte Charge ergiebiger war als kalkuliert.

**Einstieg in BC.** Der Werker öffnet über **Suchen** den **FA-Arbeitsvorrat**, filtert seine **Arbeitsplatzgruppennr.** und wählt die Zeile des gestarteten Fertigungsauftrags.

**Kernablauf.**
1. Abschluss starten → **FA-Arbeitsvorrat Buchung** öffnet sich.
2. Charge erfassen: **Chargennr.** und **Menge** – hier über der **Ursprünglichen Menge**.
3. Erfassung schließen. Diese App summiert die gemeldete **Menge** und stellt die **Überproduktion**-Grenze fest.
4. Da für den Artikel **Warnung** aktiv ist, erscheint die Abfrage „Sie überschreiten die erlaubten Werte … Wollen Sie fortfahren?“.

**Abschluss.** Der Werker bestätigt mit **Ja**; der Abschluss wird durchgeführt. Die Genehmigung erscheint anschließend im **Über-/Unterproduktion Benutzeraktivitätsprotokoll** mit **Finale Menge** und **Begrenzte Menge**. Voraussetzung ist die Einrichtung gemäß **Über-/Unterproduktionskontrolle im FA-Arbeitsvorrat einrichten**.

### Anwendungsfall 2 – Unterproduktion mit Restecharge

**Auslöser.** Aus dem eingesetzten Vormaterial verbleibt nach dem letzten Schnitt eine Restmenge; der Werker meldet weniger Gutmenge als bestellt und möchte den Rest als eigene Charge weiterführen.

**Einstieg in BC.** Öffnen über **Suchen** → **FA-Arbeitsvorrat** → **Arbeitsplatzgruppennr.** filtern → Zeile wählen.

**Kernablauf.**
1. Abschluss starten → **FA-Arbeitsvorrat Buchung**.
2. Charge erfassen: **Chargennr.**, **Menge** – hier unter der **Ursprünglichen Menge**.
3. Über **Restecharge erstellen** eine **Restecharge** abtrennen; in der Zeile **Menge** und **Neue FA-Zeilennr.** pflegen.
4. Erfassung schließen. Die App erkennt eine **Unterproduktion** und prüft die Grenze.

**Abschluss.** Ist die Unterschreitung durch die Regel mit **Warnung** gedeckt, bestätigt der Werker die Abfrage und schließt ab; ist **Warnung** inaktiv oder greift eine **Ausnahme**, wird der Abschluss blockiert und der Werker passt die Menge an oder klärt die Regel mit dem Administrator. Die abgetrennte **Restecharge** steht anschließend für den nächsten Fertigungsschritt bereit.
