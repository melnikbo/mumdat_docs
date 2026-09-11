---
title: "Anwenderhandbuch m+m Metal & Tolling with Material Properties"
---

# Anwenderhandbuch m+m Metal & Tolling with Material Properties

## Einleitung

Dieses Handbuch beschreibt die App **m+m Metal & Tolling with Material Properties**. Die App verbindet zwei bestehende m+m-Module: die **Materialeigenschaften** (mit der Seite **Artikelvorlage erstellen**) und **Metall & Umarbeitung** (mit den Metall- und Umarbeitungsstammdaten am Artikel). Sie ergänzt an genau einer Stelle ein zusätzliches Kennzeichen — **Umarbeit** — und steuert damit, ob beim Anlegen bzw. Kopieren eines Artikels die kompletten Metall- und Umarbeitungsdaten des Ausgangsartikels auf den neuen Artikel übernommen oder bewusst zurückgesetzt werden.

**Zielgruppe.** Primäre Anwender sind **operative Anwender der Artikelverwaltung** — Personen, die im Tagesgeschäft neue Artikel aus einer Vorlage erzeugen oder bestehende Artikel kopieren (z. B. Stammdatenpflege, Arbeitsvorbereitung, Vertriebs- und Einkaufsstammdaten). Sekundäre Zielgruppe sind **Administratoren und Key-User**, die die Materialarten und die zugehörigen Metall- und Umarbeitungsstammdaten einrichten, damit das Kennzeichen **Umarbeit** überhaupt sinnvoll wirken kann.

**Kurzer Prozessüberblick.** Der typische Weg verläuft entlang der folgenden Kette: Sie öffnen zu einer **Materialart** die zugehörige **Artikelvorlage erstellen**, legen dort fest, welche Informationsbereiche beim Kopieren übernommen werden, und aktivieren bei Bedarf das Kennzeichen **Umarbeit**. Beim anschließenden Kopieren eines Artikels entscheidet dieses Kennzeichen, ob die Metall- und Umarbeitungsdaten mitgezogen werden. Es gibt in dieser App keine eigene Belegbuchung, keine eigenen Berichte und keine eigenen Listen; der Nutzen liegt in der korrekten Übernahme bzw. Bereinigung der Umarbeitungsdaten.

## Schnellstart für Anwender

Der schnellste Weg zum Ergebnis (Reihenfolge: zuerst Einrichtung/Vorlage, danach die eigentliche Tätigkeit):

1. **Voraussetzung prüfen:** Der Ausgangsartikel besitzt bereits gepflegte Metall- und Umarbeitungsstammdaten (Metallkonto usw.) aus dem Modul Metall & Umarbeitung. Ohne diese Stammdaten gibt es nichts zu übernehmen. Siehe **Voraussetzungen und abhängige Einrichtung**.
2. **Vorlage öffnen:** Öffnen Sie in der **Materialartenkarte** zur gewünschten Materialart die Aktion, die die Seite **Artikelvorlage erstellen** öffnet. Wählen Sie dabei die passende **Erstellungsart** (**Basisartikel** oder **Variantenartikel**).
3. **Kopierumfang festlegen:** Aktivieren Sie in der Gruppe **Allgemein** die Bereiche, die kopiert werden sollen, und setzen Sie das Kennzeichen **Umarbeit**, wenn die Metall- und Umarbeitungsdaten mit übernommen werden sollen.
4. **Artikel kopieren:** Kopieren Sie einen bestehenden Artikel über die Standardfunktion zum Kopieren von Artikeln. Der neue Artikel wird angelegt.
5. **Ergebnis prüfen:** Bei gesetztem **Umarbeit** trägt der neue Artikel die Metall- und Umarbeitungsdaten des Ausgangsartikels; bei nicht gesetztem **Umarbeit** sind diese Felder am neuen Artikel leer.

Mehr Kontext und die Auslöser aus der Praxis finden Sie unter **Typische Anwendungsfälle**.

## Voraussetzungen und abhängige Einrichtung

Diese App bringt **keine** eigene Einrichtungsseite, keine Nummernserien und keine Berichts- oder Mailparameter mit. Sie wirkt ausschließlich auf dem bereits vorhandenen Ablauf **Artikelvorlage erstellen / Artikel kopieren**. Damit das Kennzeichen **Umarbeit** eine Wirkung entfaltet, müssen die abhängigen Module korrekt eingerichtet sein. Diese Einrichtung nehmen Administratoren bzw. Key-User vor der ersten Nutzung vor.

### Umarbeit-Übernahme beim Artikel kopieren einrichten

**Prozesseinstieg.** Diese Einrichtung betrifft den Administrator bzw. Key-User der Stammdaten. Sie ist einmalig vor der ersten produktiven Nutzung sowie bei jeder neuen Materialart durchzuführen. Das Ergebnis wird später im Tagesgeschäft im Kapitel **Artikel mit Umarbeit-Daten kopieren** genutzt. Die Kette umfasst mehrere Seiten aus den abhängigen Modulen und endet mit der eigentlichen Anwenderaktion.

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Metall- und Umarbeitungsstammdaten am Ausgangsartikel pflegen.** Hinterlegen Sie am Artikel die Rolle und die Werte für Metall & Umarbeitung (z. B. **Metallkonto**, **Metallkonto 2. Ebene**, **Abfallschlüsselnr.**, **Schrottartikel**, **Rohmetall**, **Metallbehälter**) sowie die zugehörigen Untertabellen über die Seite **Artikel Metall & Umarbeitung Einrichtung**. *Wenn diese Daten vorhanden sind, dann existiert überhaupt ein übertragbarer Datenbestand;* fehlen sie, überträgt die App beim Kopieren nichts, weil es keine Quelldaten gibt.
2. **Materialart bereitstellen.** Sorgen Sie dafür, dass die betreffende **Materialart** in den **Materialarten** existiert und über die **Materialartenkarte** erreichbar ist. *Wenn die Materialart gepflegt ist, dann kann daraus eine Vorlage geöffnet werden;* ohne Materialart gibt es keinen Einstieg in die Vorlage.
3. **Umarbeit in der Vorlage setzen.** Öffnen Sie über die **Materialartenkarte** die Seite **Artikelvorlage erstellen** und aktivieren Sie das Kennzeichen **Umarbeit** (Details siehe Kapitel **Artikelvorlage erstellen und die Umarbeit-Kennung**). *Wenn Umarbeit in der Vorlage aktiviert ist, dann wird dieses Kennzeichen beim Kopieren automatisch in den Kopierpuffer übernommen* und steuert dort die Übernahme der Umarbeitungsdaten.

**Operativer Abschluss.** Die Kette wird im Tagesgeschäft abgeschlossen, indem der Anwender einen bestehenden Artikel kopiert (siehe Kapitel **Artikel mit Umarbeit-Daten kopieren**). Erst dieser Kopiervorgang löst die Übernahme bzw. Bereinigung der Metall- und Umarbeitungsdaten aus.

## Artikelvorlage erstellen und die Umarbeit-Kennung

**Prozesseinstieg.** Die Seite **Artikelvorlage erstellen** legt fest, welche Informationsbereiche eines Artikels beim Kopieren bzw. beim Anlegen aus der Vorlage übernommen werden. Sie ist keine über die Suche auffindbare Seite, sondern wird gezielt aus der **Materialartenkarte** heraus geöffnet.

**Einstieg:** Öffnen Sie in der **Materialartenkarte** zur gewünschten Materialart die Aktion, die die Seite **Artikelvorlage erstellen** öffnet. Beim Öffnen wird — falls noch nicht vorhanden — automatisch eine Vorlage zur gewählten **Erstellungsart** (**Basisartikel** oder **Variantenartikel**) angelegt. Die Vorlage ist damit fest an eine Materialart und eine Erstellungsart gebunden.

Die App ergänzt diese Seite in der Gruppe **Allgemein** um genau ein Feld: das Kennzeichen **Umarbeit**. Alle übrigen Felder stammen aus dem Basismodul, werden dem Anwender aber auf **einer** Seite angezeigt und sind deshalb hier vollständig beschrieben.

### Erstellungsart

Die **Erstellungsart** wird beim Öffnen der Vorlage aus der **Materialartenkarte** vorgegeben und bestimmt, für welchen Artikeltyp die Vorlage gilt. Sie ist ein Optionsfeld mit folgenden Werten:

- **Basisartikel:** Die Vorlage gilt für die Erstellung eines Basisartikels. In diesem Fall ist zusätzlich die Gruppe **Variantenartikel** mit dem Feld **Variantenartikel kopieren** sichtbar.
- **Variantenartikel:** Die Vorlage gilt für die Erstellung eines Variantenartikels. Die Gruppe **Variantenartikel** wird in diesem Fall nicht angezeigt.

### Felder der Gruppe „Allgemein"

Die Bereichskennzeichen legen fest, welche Informationen des Ausgangsartikels beim Kopieren mitgenommen werden. Ist ein Kennzeichen aktiviert, so wird der betreffende Bereich übernommen; ist es nicht aktiviert, bleibt der Bereich am neuen Artikel leer bzw. auf den Standardwerten.

| Feld | Erläuterung |
|---|---|
| **Allgemeine Artikelinformationen** | Wenn aktiviert, dann werden die allgemeinen Kopfdaten des Artikels (Beschreibung und weitere Grunddaten) in den neuen Artikel übernommen; ohne Aktivierung startet der neue Artikel ohne diese Grunddaten. |
| **Maßeinheiten** | Wenn aktiviert, dann werden die Maßeinheiten des Ausgangsartikels mitkopiert, sodass der neue Artikel sofort mit denselben Einheiten (z. B. Lager- und Verkaufseinheit) einsetzbar ist. |
| **Dimensionen** | Wenn aktiviert, dann übernimmt der neue Artikel die Dimensionswerte des Ausgangsartikels; die spätere Buchung auf Kostenstellen/-träger erfolgt damit ohne erneute Zuordnung. |
| **Bild** | Wenn aktiviert, dann wird das hinterlegte Artikelbild mitkopiert; ohne Aktivierung bleibt der neue Artikel ohne Bild. |
| **Bemerkungen** | Wenn aktiviert, dann werden die Bemerkungen des Ausgangsartikels übernommen. |
| **Planung** | Wenn aktiviert, dann werden die Planungs-/Dispositionsparameter des Ausgangsartikels mitkopiert, sodass die Beschaffungslogik für den neuen Artikel direkt greift. |
| **Umarbeit** | Wenn aktiviert, dann werden beim Kopieren die kompletten Metall- und Umarbeitungsdaten des Ausgangsartikels auf den neuen Artikel übernommen (Metallkonto und weitere Kopffelder sowie die Untertabellen wie Artikelmetallwerte, Artikelabschläge und Metallkontozuweisungen). Ist das Kennzeichen **nicht** aktiviert, so werden am neuen Artikel die Metall- und Umarbeitungs-Kopffelder (**Metallkonto**, **Metallkonto 2. Ebene**, **Abfallschlüsselnr.**, **Schrottartikel**, **Rohmetall**, **Metallbehälter**) bewusst zurückgesetzt — der neue Artikel startet damit ohne Umarbeitungsbezug. Dies ist das einzige von dieser App ergänzte Feld. |

### Felder der Gruppe „Verkauf"

| Feld | Erläuterung |
|---|---|
| **Verkaufspreise** | Wenn aktiviert, dann werden die Verkaufspreise des Ausgangsartikels mitkopiert; der neue Artikel ist damit sofort verkaufsfähig kalkuliert. |
| **Verkaufszeilenrabatte** | Wenn aktiviert, dann werden die Verkaufszeilenrabatte übernommen, sodass bestehende Rabattstaffeln für den neuen Artikel weiter gelten. |

### Felder der Gruppe „Einkauf"

| Feld | Erläuterung |
|---|---|
| **Einkaufspreise** | Wenn aktiviert, dann werden die Einkaufspreise des Ausgangsartikels übernommen; die Beschaffung des neuen Artikels ist damit bewertet. |
| **Einkaufszeilenrabatte** | Wenn aktiviert, dann werden die Einkaufszeilenrabatte mitkopiert. |

### Felder der Gruppe „Service"

| Feld | Erläuterung |
|---|---|
| **Problembehandlung** | Wenn aktiviert, dann wird die Problembehandlung des Ausgangsartikels übernommen. |
| **Ressourcenqualifikationen** | Wenn aktiviert, dann werden die Ressourcenqualifikationen mitkopiert. |

### Felder der Gruppe „Erweitert"

| Feld | Erläuterung |
|---|---|
| **Artikelvarianten** | Wenn aktiviert, dann werden die Artikelvarianten des Ausgangsartikels übernommen. |
| **Übersetzungen** | Wenn aktiviert, dann werden die Artikelübersetzungen mitkopiert, sodass fremdsprachige Beschreibungen erhalten bleiben. |
| **Textbausteine** | Wenn aktiviert, dann werden die Textbausteine des Ausgangsartikels übernommen. |
| **Stücklistenkomponenten** | Wenn aktiviert, dann werden die Stücklistenkomponenten mitkopiert. |
| **Artikellieferanten** | Wenn aktiviert, dann werden die zugeordneten Artikellieferanten übernommen. |
| **Attribute** | Wenn aktiviert, dann werden die Artikelattribute mitkopiert. |
| **Artikelreferenzen** | Wenn aktiviert, dann werden die Artikelreferenzen (z. B. Referenzen zu Lieferanten- oder Kundennummern) übernommen. |
| **Lagerhaltungsdaten** | Wenn aktiviert, dann werden die Lagerhaltungsdaten des Ausgangsartikels mitkopiert, sodass lagerspezifische Einstellungen erhalten bleiben. |

### Felder der Gruppe „Variantenartikel" (nur bei Erstellungsart Basisartikel)

| Feld | Erläuterung |
|---|---|
| **Variantenartikel kopieren** | Wenn aktiviert, dann werden bei der Erstellung eines Basisartikels auch die zugehörigen Variantenartikel mitkopiert. Die Gruppe ist nur sichtbar, wenn die **Erstellungsart** auf **Basisartikel** steht. |

### Felder der Gruppe „Optionen"

| Feld | Erläuterung |
|---|---|
| **Neuen Artikel entsperren** | Wenn aktiviert, dann wird der neu erstellte Artikel nach dem Kopieren automatisch entsperrt (das Kennzeichen **Gesperrt** wird entfernt) und ist sofort verwendbar. Ist die Option nicht aktiviert, bleibt der neue Artikel zunächst gesperrt und muss vor der Verwendung manuell freigegeben werden. |

**Validierung/Abhängigkeit.** Das Kennzeichen **Umarbeit** wirkt nur dann sinnvoll, wenn der Ausgangsartikel tatsächlich Metall- und Umarbeitungsdaten besitzt (siehe **Voraussetzungen und abhängige Einrichtung**). Die Übernahme bzw. Bereinigung erfolgt automatisch während des Kopiervorgangs; eine gesonderte Bestätigung ist nicht erforderlich.

## Artikel mit Umarbeit-Daten kopieren (Tägliche Arbeit)

**Steuerung durch vorgelagerte Seiten.** Dieser Tagesablauf wird durch zwei vorgelagerte Stellen gesteuert: durch die **Metall- und Umarbeitungsstammdaten** am Ausgangsartikel (gepflegt über **Artikel Metall & Umarbeitung Einrichtung**) und durch das Kennzeichen **Umarbeit** in der **Artikelvorlage erstellen**. Beide bestimmen, ob und welche Umarbeitungsdaten auf den neuen Artikel gelangen.

So läuft der Kopiervorgang ab:

1. Öffnen Sie einen bestehenden Artikel bzw. wählen Sie ihn in der Artikelübersicht aus.
2. Starten Sie die Standardfunktion zum Kopieren von Artikeln. Der Kopierumfang richtet sich nach den in der Vorlage gesetzten Kennzeichen, einschließlich **Umarbeit**.
3. Business Central legt den neuen Artikel an.
4. **Ist Umarbeit aktiviert**, so übernimmt die App zusätzlich die Metall- und Umarbeitungsdaten des Ausgangsartikels: die Kopffelder am Artikel sowie die zugehörigen Datensätze aus **Artikel Metall & Umarbeitung Einrichtung**, den **Artikel Metallwerten**, den **Artikelabschlägen**, den Metallkontozuweisungen und den Deckungsüberschuss-Salden.
5. **Ist Umarbeit nicht aktiviert**, so setzt die App die Metall- und Umarbeitungs-Kopffelder am neuen Artikel zurück (**Metallkonto**, **Metallkonto 2. Ebene**, **Abfallschlüsselnr.**, **Schrottartikel**, **Rohmetall**, **Metallbehälter**). Der neue Artikel ist damit ohne Umarbeitungsbezug.

**Hinweis.** Die App übernimmt nur solche Untertabellen, die am Ausgangsartikel tatsächlich Datensätze besitzen. Ist ein Bereich leer, wird er übersprungen. Es findet keine Buchung und keine Freigabe statt; der Vorgang ist mit dem Anlegen des neuen Artikels abgeschlossen.

## Berechtigungen

Für die Nutzung der App wird der Berechtigungssatz **MuM MTMP Permissions** ausgeliefert. Dieser Satz ist zuweisbar und bestimmt die Berechtigungen für die Ausführung der App-Logik: Er legt fest, welche Aktionen die Anwender im Rahmen der Umarbeit-Übernahme ausführen können, indem er die Ausführungsrechte für die beiden Codeunits der App (Kopier- und Ereignislogik) umfasst. Die Berechtigungen für die eigentlichen Metall-, Umarbeitungs- und Artikeldaten werden über die Berechtigungssätze der Basis- und abhängigen Module gesteuert.

## FAQ und Troubleshooting

### 1. Warum finde ich die Seite „Artikelvorlage erstellen" nicht über die Suche?
Die Seite ist bewusst nicht über die Suche auffindbar. Sie wird ausschließlich aus der **Materialartenkarte** über die zugehörige Aktion geöffnet, weil eine Vorlage immer an eine bestimmte **Materialart** und **Erstellungsart** gebunden ist.

### 2. Wo aktiviere ich, dass die Umarbeitungsdaten mitkopiert werden?
In der **Artikelvorlage erstellen** in der Gruppe **Allgemein** über das Kennzeichen **Umarbeit**. Dieses Kennzeichen wird beim Kopieren automatisch berücksichtigt.

### 3. Was passiert, wenn „Umarbeit" nicht gesetzt ist?
Der neue Artikel wird angelegt, seine Metall- und Umarbeitungs-Kopffelder (**Metallkonto**, **Metallkonto 2. Ebene**, **Abfallschlüsselnr.**, **Schrottartikel**, **Rohmetall**, **Metallbehälter**) werden jedoch zurückgesetzt. Der Artikel hat dann keinen Umarbeitungsbezug.

### 4. Welche Daten werden bei aktivem „Umarbeit" genau übernommen?
Die Kopffelder am Artikel sowie die Datensätze aus **Artikel Metall & Umarbeitung Einrichtung**, die **Artikel Metallwerte**, die **Artikelabschläge**, die Metallkontozuweisungen und die Deckungsüberschuss-Salden des Ausgangsartikels.

### 5. Warum wurden bei aktivem „Umarbeit" trotzdem keine Untertabellen kopiert?
Die App überträgt nur Untertabellen, die am Ausgangsartikel tatsächlich Datensätze enthalten. Sind am Ausgangsartikel z. B. keine Artikelabschläge gepflegt, gibt es nichts zu übernehmen.

### 6. Muss der Ausgangsartikel bestimmte Stammdaten haben, damit „Umarbeit" wirkt?
Ja. Der Ausgangsartikel muss die Metall- und Umarbeitungsstammdaten (z. B. **Metallkonto**) besitzen. Ohne diese Daten kann bei aktivem **Umarbeit** nichts übernommen werden.

### 7. Warum ist der neue Artikel nach dem Kopieren gesperrt?
Ob der neue Artikel entsperrt wird, steuert das Kennzeichen **Neuen Artikel entsperren** in der Vorlage. Ist es nicht aktiviert, bleibt der neue Artikel zunächst **Gesperrt** und muss manuell freigegeben werden.

### 8. Wann ist die Gruppe „Variantenartikel" sichtbar?
Nur, wenn die **Erstellungsart** der Vorlage auf **Basisartikel** steht. Bei **Variantenartikel** ist diese Gruppe ausgeblendet.

### 9. Erzeugt die App eigene Buchungen, Berichte oder Belege?
Nein. Die App ergänzt nur das Kopierverhalten um die Umarbeitungsdaten. Es gibt keine eigene Buchung, keinen eigenen Bericht und keinen eigenen Beleg.

### 10. Kann ich das Verhalten je Materialart unterschiedlich einstellen?
Ja. Da die Vorlage an **Materialart** und **Erstellungsart** gebunden ist, können Sie das Kennzeichen **Umarbeit** je Materialart und je Erstellungsart (Basis- bzw. Variantenartikel) unterschiedlich setzen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Neuen Umarbeitungsartikel aus einer Vorlage anlegen

**Auslöser.** Ein Kollege aus der Arbeitsvorbereitung meldet telefonisch, dass für eine bestehende Materialart eine weitere Artikelausprägung benötigt wird, die dieselben Metall- und Umarbeitungsbedingungen tragen soll wie ein vorhandener Artikel.

**Einstieg in BC.** Sie öffnen die **Materialartenkarte** zur betreffenden Materialart und rufen die Aktion auf, die die Seite **Artikelvorlage erstellen** für die **Erstellungsart Basisartikel** öffnet.

**Kernablauf.** In der Gruppe **Allgemein** aktivieren Sie die benötigten Bereiche und setzen das Kennzeichen **Umarbeit**. Anschließend kopieren Sie den vorhandenen Umarbeitungsartikel über die Standardfunktion zum Kopieren von Artikeln. Beim Anlegen des neuen Artikels übernimmt die App die Metall- und Umarbeitungsdaten des Ausgangsartikels vollständig, einschließlich der Untertabellen wie Artikelmetallwerte und Artikelabschläge.

**Abschluss.** Der neue Artikel trägt dieselben Umarbeitungsbedingungen wie der Ausgangsartikel. Ist in der Vorlage **Neuen Artikel entsperren** gesetzt, ist er sofort verwendbar; andernfalls geben Sie ihn manuell frei.

### Anwendungsfall 2: Artikel ohne Umarbeitungsbezug duplizieren

**Auslöser.** Per E-Mail geht die Aufgabe ein, einen bestehenden Artikel als reinen Handels- bzw. Standardartikel zu duplizieren — ausdrücklich **ohne** die Metall- und Umarbeitungsbindung des Originals.

**Einstieg in BC.** Sie öffnen zur passenden Materialart die **Artikelvorlage erstellen** und stellen sicher, dass das Kennzeichen **Umarbeit** **nicht** gesetzt ist.

**Kernablauf.** Sie kopieren den Ausgangsartikel über die Standardfunktion zum Kopieren von Artikeln. Da **Umarbeit** nicht gesetzt ist, setzt die App die Metall- und Umarbeitungs-Kopffelder am neuen Artikel zurück (**Metallkonto**, **Metallkonto 2. Ebene**, **Abfallschlüsselnr.**, **Schrottartikel**, **Rohmetall**, **Metallbehälter**).

**Abschluss.** Der neue Artikel entsteht ohne Umarbeitungsbezug und kann als eigenständiger Standardartikel weiterverwendet werden.
