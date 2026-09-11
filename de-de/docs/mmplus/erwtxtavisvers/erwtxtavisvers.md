---
title: Anwenderhandbuch m+m Ext. Text Module with Logistic Management
---

# Anwenderhandbuch m+m Ext. Text Module with Logistic Management

Dieses Handbuch beschreibt die Anwendung des Moduls **m+m Ext. Text Module with Logistic Management** in Microsoft Dynamics 365 Business Central. Das Modul verbindet die **Erweiterte Textzuordnung** (Textbausteinverwaltung aus dem m+m Textmodul) mit der Logistik-Planung – der **Avisierung** und der **Versandplanung**. So lassen sich vordefinierte Textvorlagen automatisch als Kopf- und Zeilentexte in Avisierungen, Versandplanungen und deren registrierte Belege übernehmen, auf Berichten drucken und in E-Mails einbetten.

Alle in diesem Handbuch genannten Seiten, Aktionen, Felder und Optionswerte entsprechen den deutschen Oberflächenbezeichnungen von Business Central.

---

## 1 Einleitung

### 1.1 Zweck des Moduls

Das Modul ist ein **Verbindungsmodul**: Es bringt die Funktionen der **Erweiterten Textzuordnung** in die logistischen Belege der Avisierung und Versandplanung. Ohne dieses Modul stehen erweiterte Textbausteine nur in den klassischen Verkaufs- und Einkaufsbelegen zur Verfügung. Mit dem Modul werden dieselben Textvorlagen auch für folgende Prozesse verfügbar:

- **Avisierung** und **Reg. Avisierung** (registrierte Avisierung),
- **Versandplanung** und **Reg. Versandplanung** (registrierte Versandplanung),
- den **Warenausgang** als Zielprozess der Versandplanung,
- die **Ladestelle** als zusätzliches Zuordnungskriterium.

Der Nutzen für den Anwender: Wiederkehrende Hinweistexte (z. B. Verlade-, Transport- oder Avisierungshinweise) werden nach einmaliger Einrichtung **automatisch** an die richtige Stelle des Belegs geschrieben – als reine Bildschirminformation, als Drucktext auf dem Bericht oder als E-Mail-Text.

### 1.2 Zielgruppe

Primäre Zielgruppe sind **operative Anwender in der Logistik**, die täglich Avisierungen und Versandplanungen erfassen, um Herkunftsbelege ergänzen, registrieren und versenden. Für diese Anwender erscheinen die Texte weitgehend automatisch; sie müssen die Belege lediglich normal bearbeiten.

Sekundäre Zielgruppe sind **Administratoren und Key-User**, die einmalig die Einrichtung vornehmen: die Prozesse aktivieren, Textvorlagen anlegen und die Zuordnung im **Arbeitsblatt erweiterte Textzuordnung** pflegen.

### 1.3 Kurzer Prozessüberblick

1. Der Administrator aktiviert die benötigten Prozesse in der **Avisierung Einrichtung**, der **Versandplanung Einrichtung** und – bei Bedarf – der **Ladestellen Einrichtung**.
2. Der Key-User legt in den **Erweiterten Textvorlagen** die Textbausteine an.
3. Im **Arbeitsblatt erweiterte Textzuordnung** ordnet der Key-User jede Vorlage einem **Prozess** (Avisierung oder Versandplanung) sowie einem **Typ** (Debitor/Kreditor …) und optional einem **Subtyp** (Artikel, Artikelkategorie, Ladestelle …) zu.
4. Der operative Anwender legt eine Avisierung oder Versandplanung an. Die passenden Texte werden automatisch in die Infoboxen übernommen.
5. Beim Registrieren des Belegs werden die Texte in den registrierten Beleg übertragen und stehen dort dauerhaft zur Verfügung.

---

## 2 Schnellstart für Anwender

Der Schnellstart folgt der technischen Abhängigkeitsreihenfolge: **zuerst die Einrichtung**, dann die Vorlagen, dann die tägliche Arbeit.

1. **Prozess aktivieren (Administrator).** Öffnen Sie über **Suchen** die **Versandplanung Einrichtung** bzw. **Avisierung Einrichtung** und setzen Sie den jeweiligen Aktivierungsschalter (**Versandplanung aktivieren** bzw. **Aktiviert**). Für ladestellenbezogene Texte aktivieren Sie zusätzlich in der **Ladestellen Einrichtung** den Schalter **Ladestellen aktiviert**.
2. **Textvorlage anlegen (Key-User).** Öffnen Sie über **Suchen** die **Erweiterten Textvorlagen** und legen Sie eine Vorlage mit **Vorlage Nr.**, **Drucktyp** und dem eigentlichen Textinhalt an.
3. **Vorlage zuordnen (Key-User).** Öffnen Sie über **Suchen** das **Arbeitsblatt erweiterte Textzuordnung**. Tragen Sie die **Vorlage Nr.** ein, wählen Sie im Feld **Prozess** den logistischen Prozess (**Versandplanung** oder **Avisierung**), setzen Sie **Typ**/**Typ Nr.** und – für Positionstexte – **Subtyp**/**Subtyp Nummer**.
4. **Beleg bearbeiten (Anwender).** Legen Sie eine **Versandplanung** bzw. **Avisierung** an. Die Kopftexte erscheinen automatisch in der Infobox **Versandplanungstexte** bzw. **Avisierungstexte**.
5. **Zeilen ergänzen (Anwender).** Holen Sie die Belegzeilen: In der Versandplanung über **Versandplanungszeilen holen**, in der Avisierung über **Herkunftsbelege holen**. Die Zeilentexte erscheinen dann in **Versandplanungszeilentexte** bzw. **Avisierungszeilentexte**.
6. **Prüfen und öffnen (Anwender).** Öffnen Sie bei Bedarf über die Aktion **Erweiterte Versandplanungstexte** bzw. **Erweiterte Avisierungstexte** die Vorschauseite, um die kombinierten Texte je Belegart zu kontrollieren oder neu zu erzeugen.
7. **Registrieren (Anwender).** Registrieren Sie den Beleg im gewohnten Ablauf der Avisierung/Versandplanung. Die Texte werden dabei in die **Registrierte Avisierung** bzw. **Registrierte Versandplanung** übernommen.

---

## 3 Einrichtung

Die Einrichtung ist der umfangreichste Teil dieses Moduls. Sie besteht aus drei Aktivierungsseiten (Prozessfreischaltung), der Vorlagenpflege und der eigentlichen Zuordnung im Arbeitsblatt. Die Aktivierungsseiten sind unternehmensweite Einrichtungsseiten (je ein Datensatz pro Mandant) und werden über **Suchen** aufgerufen.

### 3.1 Prozesse aktivieren

Bevor das Modul Texte erzeugt, muss der jeweilige logistische Prozess aktiviert sein. Ist der Prozess nicht aktiviert, erzeugt das Modul **keine** Texte – die Infoboxen bleiben leer.

**Einstieg:** Öffnen Sie über **Suchen** die jeweilige Einrichtungsseite.

| Einrichtung | Erläuterung |
|---|---|
| **Aktiviert** (in **Avisierung Einrichtung**) | Wenn aktiviert, erzeugt das Modul beim Anlegen und Ändern einer **Avisierung** automatisch die zugeordneten Avisierungstexte und stellt sie in den Infoboxen bereit; ist der Schalter nicht gesetzt, unterbleibt die Textübernahme für Avisierungen vollständig. |
| **Versandplanung aktivieren** (in **Versandplanung Einrichtung**) | Wenn aktiviert, erzeugt das Modul beim Anlegen und Ändern einer **Versandplanung** automatisch die zugeordneten Versandplanungstexte; ohne Aktivierung werden für Versandplanungen keine erweiterten Texte gebildet. |
| **Ladestellen aktiviert** (in **Ladestellen Einrichtung**) | Wenn aktiviert, dürfen im **Arbeitsblatt erweiterte Textzuordnung** die Subtypen **Ladestelle** und **Alle Ladestellen** verwendet werden, und ladestellenbezogene Texte werden je Ladestelle ermittelt; ist der Schalter nicht gesetzt, wird der Versuch, eine Ladestellen-Zuordnung zu speichern, mit dem Hinweis „Die Ladestellen sind nicht eingerichtet oder aktiviert.“ abgewiesen. |

> Hinweis: Die Aktivierungsschalter gehören zum Basismodul m+m Logistic Management; dieses Modul liest sie nur aus, um zu entscheiden, ob Texte gebildet werden. Die vollständige Einrichtung von Avisierung und Versandplanung selbst ist im Handbuch des Basismoduls beschrieben – für die Texterzeugung genügt der jeweils genannte Aktivierungsschalter.

### 3.2 Erweiterte Textvorlagen anlegen

Bevor Sie Texte zuordnen können, müssen die Textbausteine als **Erweiterte Textvorlagen** vorhanden sein.

**Prozess-Intro:** Diese Aufgabe erledigt der Key-User einmalig bzw. bei Bedarf. Die Vorlagen bilden die inhaltliche Grundlage; erst danach kann im Arbeitsblatt zugeordnet werden (siehe Abschnitt 3.3). Die Vorlagen werden später in der täglichen Arbeit (Kapitel 6) auf den Belegen wirksam.

**Einstieg:** Öffnen Sie über **Suchen** die **Erweiterten Textvorlagen**; legen Sie mit **+Neu** eine Vorlage an bzw. öffnen Sie eine bestehende zur Bearbeitung.

Die wichtigsten Felder der Vorlage:

| Feld | Erläuterung |
|---|---|
| **Vorlage Nr.** | Eindeutige Nummer der Textvorlage; wird beim Anlegen aus der Nummernserie vergeben. Über diese Nummer wird die Vorlage später im Arbeitsblatt referenziert. |
| **Beschreibung** | Frei wählbare interne Kurzbezeichnung der Vorlage; erleichtert dem Key-User das Wiederfinden, wird nicht auf Belegen gedruckt. |
| **Drucktyp** | Wenn gesetzt, bestimmt der Drucktyp, **wo** der Text erscheint. Werte siehe unten. |
| **Nebendruck Typ** | Wenn der Drucktyp **Bericht** gewählt ist, legt der Nebendruck Typ die Druckposition im Bericht fest; bei den Drucktypen **InfoBox** und **Mail** ist das Feld ohne Wirkung. Werte siehe unten. |

**Werte des Feldes Drucktyp** (jede Vorlage erhält genau einen Drucktyp):

- **InfoBox:** Der Text erscheint nur in der Infobox der jeweiligen Seite als interne Bildschirminformation und wird **nicht** gedruckt.
- **Bericht:** Der Text wird im Bericht des ausgewählten Prozesses ausgegeben und darf damit auf Belegen gedruckt werden. Nur bei diesem Drucktyp ist der **Nebendruck Typ** wählbar.
- **Mail:** Der Text wird in die E-Mail eingebettet, wenn zum Beleg eine E-Mail versendet wird.

**Werte des Feldes Nebendruck Typ** (nur bei Drucktyp **Bericht**):

- **Kopfzeile:** Druck des Textes im Kopfbereich des Berichts.
- **Fußzeile:** Druck des Textes im Fußbereich des Berichts.
- **Vor Position:** Druck des Textes vor der jeweiligen Belegposition.
- **Nach Position:** Druck des Textes nach der jeweiligen Belegposition.

### 3.3 Zuordnung im Arbeitsblatt erweiterte Textzuordnung

**Prozess-Intro:** Im **Arbeitsblatt erweiterte Textzuordnung** legt der Key-User fest, **welche** Textvorlage bei **welchem** Prozess und für **welchen** Geschäftspartner bzw. Artikel gilt. Diese Zuordnung ist die zentrale Steuerung des Moduls; sie wird in der täglichen Arbeit (Kapitel 6) automatisch ausgewertet. Voraussetzung sind angelegte Vorlagen (Abschnitt 3.2) und aktivierte Prozesse (Abschnitt 3.1).

**Einstieg:** Öffnen Sie über **Suchen** das **Arbeitsblatt erweiterte Textzuordnung**. Das Arbeitsblatt ist eine globale Seite ohne übergeordneten Stammbeleg.

| Einrichtung | Erläuterung |
|---|---|
| **Vorlage Nr.** | Verweist auf die zu verwendende Textvorlage. Über den LookUp wählen Sie eine bestehende Vorlage oder legen mit **+Neu** eine neue an. Wenn gefüllt, wird beim passenden Prozess der Inhalt dieser Vorlage übernommen. |
| **Drucktyp** | Wird aus der Vorlage geerbt und zeigt an, ob der zugeordnete Text als **InfoBox**, **Bericht** oder **Mail** wirkt (siehe Abschnitt 3.2). |
| **Typ** | Wenn gesetzt, schränkt der Typ die Zuordnung auf einen Geschäftspartner-Kontext auf Kopfebene ein. Werte siehe unten. |
| **Typ Nr.** | Wenn ein einzelbezogener Typ (Debitor, Kreditor, Debitorengruppe, Kreditorengruppe) gewählt ist, wird hier die konkrete Nummer bzw. Buchungsgruppe hinterlegt; nur für diesen Partner/diese Gruppe greift die Zuordnung. |
| **Subtyp** | Wenn gesetzt, macht der Subtyp aus der Zuordnung einen **Positionstext** (Zeilenebene). Bleibt der Subtyp **(leer)**, wirkt die Zuordnung als **Kopftext**. Werte siehe unten. |
| **Subtyp Nummer** | Konkretisiert den Subtyp (z. B. die Artikelnummer, die Artikelkategorie oder die Ladestellennummer), sofern der gewählte Subtyp eine Nummer erfordert. |
| **Prozess** | Wenn gesetzt, bestimmt der Prozess, für welchen logistischen Beleg die Vorlage gilt. Für dieses Modul sind insbesondere **Versandplanung**, **Avisierung** und **Warenausgang** relevant. Nur bei diesem Prozess wird der Text gebildet. |
| **Prozess-Objektname** | Zeigt den Namen des im Feld **Prozess** gewählten Objekts an; reine Anzeige zur Kontrolle. |

**Werte des Feldes Typ** (jede Zuordnung erhält höchstens einen Typ):

- **(leer):** Die Zuordnung ist nicht auf einen Geschäftspartner eingeschränkt und greift unabhängig vom Debitor/Kreditor des Belegs.
- **Debitor:** Zuordnung gilt für genau einen Debitor; der Debitor wird in **Typ Nr.** hinterlegt. In der Versandplanung wird der Debitor aus der Lieferung bzw. dem Fahrerkontakt ermittelt.
- **Alle Debitoren:** Zuordnung gilt einheitlich für alle Debitoren.
- **Debitorengruppe:** Zuordnung gilt für eine Debitorenbuchungsgruppe; die Gruppe wird in **Typ Nr.** hinterlegt.
- **Kreditor:** Zuordnung gilt für genau einen Kreditor (relevant für die Avisierung, die aus Einkaufsbelegen entsteht); der Kreditor wird in **Typ Nr.** hinterlegt.
- **Alle Kreditoren:** Zuordnung gilt einheitlich für alle Kreditoren.
- **Kreditorengruppe:** Zuordnung gilt für eine Kreditorenbuchungsgruppe; die Gruppe wird in **Typ Nr.** hinterlegt.

**Werte des Feldes Subtyp** (steuert den Positionstext; bleibt das Feld leer, entsteht ein Kopftext):

- **(leer):** Die Zuordnung ist ein **Kopftext** und wird nicht positionsbezogen ausgewertet.
- **Alle Artikel:** Positionstext gilt für alle Artikel der Zeilen.
- **Artikel:** Positionstext gilt nur für einen Artikel; die Artikelnummer steht in **Subtyp Nummer**.
- **Artikelkategorie:** Positionstext gilt für alle Artikel einer Artikelkategorie; die Kategorie steht in **Subtyp Nummer**.
- **Alle Ladestellen:** Positionstext gilt für alle Ladestellen (nur nutzbar, wenn **Ladestellen aktiviert** gesetzt ist).
- **Ladestelle:** Positionstext gilt nur für eine bestimmte Ladestelle; die Ladestellennummer steht in **Subtyp Nummer**. Beim Speichern wird geprüft, ob die Ladestellen aktiviert sind; andernfalls erscheint der Hinweis „Die Ladestellen sind nicht eingerichtet oder aktiviert.“.

> Merkregel: **Ist der Subtyp gefüllt, handelt es sich um einen Positionstext.** Für reine Kopftexte muss der Subtyp **(leer)** bleiben.

**Prozessschritte für eine Zuordnung:**

1. Zuerst wählen Sie die **Vorlage Nr.** (der **Drucktyp** wird angezeigt).
2. Danach setzen Sie den **Prozess** auf den gewünschten logistischen Beleg (Versandplanung, Avisierung oder Warenausgang).
3. Anschließend legen Sie über **Typ**/**Typ Nr.** den Geschäftspartner-Kontext fest.
4. Schließlich entscheiden Sie über den **Subtyp**: leer lassen für einen Kopftext, oder Artikel/Artikelkategorie/Ladestelle setzen für einen Positionstext.

### 3.4 Avisierungstexte einrichten (Prozesskette)

**Prozess-Intro:** Damit Avisierungen automatisch mit Texten versehen werden, sind mehrere Seiten in Abhängigkeitsreihenfolge zu konfigurieren. Diese Kette wird in der täglichen Arbeit an der Avisierung wirksam (Abschnitt 6.2).

1. **Avisierung aktivieren.** Setzen Sie in der **Avisierung Einrichtung** den Schalter **Aktiviert**. Wenn aktiviert, bildet das Modul beim Anlegen/Ändern einer Avisierung Texte; ohne diesen Schalter geschieht nichts.
2. **Textvorlage anlegen.** Legen Sie in den **Erweiterten Textvorlagen** die gewünschte Vorlage mit passendem **Drucktyp** an (Abschnitt 3.2).
3. **Zuordnung erfassen.** Ordnen Sie die Vorlage im **Arbeitsblatt erweiterte Textzuordnung** dem **Prozess Avisierung** zu. Für Kopftexte setzen Sie **Typ** (z. B. Kreditor/Alle Kreditoren), **Subtyp** bleibt **(leer)**. Für Positionstexte setzen Sie zusätzlich den **Subtyp** (Artikel, Artikelkategorie oder Ladestelle).
4. **Operativer Abschluss.** In der täglichen Arbeit legt der Anwender die Avisierung an und ergänzt Zeilen über **Herkunftsbelege holen**; die Texte erscheinen dann automatisch (siehe Abschnitt 6.2).

### 3.5 Versandplanungstexte einrichten (Prozesskette)

**Prozess-Intro:** Analog zur Avisierung, jedoch für die Versandplanung und den Debitorenkontext.

1. **Versandplanung aktivieren.** Setzen Sie in der **Versandplanung Einrichtung** den Schalter **Versandplanung aktivieren**. Wenn aktiviert, werden beim Anlegen/Ändern einer Versandplanung Texte gebildet – sowohl für den Prozess **Versandplanung** als auch für den nachgelagerten **Warenausgang**.
2. **Textvorlage anlegen** (Abschnitt 3.2).
3. **Zuordnung erfassen.** Ordnen Sie die Vorlage dem **Prozess Versandplanung** zu. Kopftexte über **Typ** (Debitor/Alle Debitoren/Debitorengruppe), Positionstexte zusätzlich über **Subtyp**.
4. **Operativer Abschluss.** Der Anwender legt die Versandplanung an und holt Zeilen über **Versandplanungszeilen holen**; die Texte erscheinen automatisch (siehe Abschnitt 6.1).

### 3.6 Ladestellenbezogene Texte einrichten (Prozesskette)

**Prozess-Intro:** Ladestellenbezogene Texte sind eine eigenständige Fähigkeit dieses Moduls: Sie erlauben Positionstexte, die nur für eine bestimmte **Ladestelle** gelten. Voraussetzung ist eine separate Aktivierung.

1. **Ladestellen aktivieren.** Setzen Sie in der **Ladestellen Einrichtung** den Schalter **Ladestellen aktiviert**. Wenn aktiviert, stehen die Subtypen **Ladestelle** und **Alle Ladestellen** zur Verfügung; ist er nicht gesetzt, wird jede Ladestellen-Zuordnung mit „Die Ladestellen sind nicht eingerichtet oder aktiviert.“ abgewiesen.
2. **Zuordnung mit Subtyp Ladestelle.** Erfassen Sie im **Arbeitsblatt erweiterte Textzuordnung** eine Positionszuordnung mit **Subtyp = Ladestelle** und der gewünschten Ladestellennummer in **Subtyp Nummer** (oder **Alle Ladestellen**).
3. **Operativer Abschluss.** Sobald in einer Avisierungs- oder Versandplanungszeile die **Ladestelle** gesetzt wird, ermittelt das Modul den passenden Text erneut und übernimmt ihn in die Zeilentexte (siehe Kapitel 6). Zusätzlich lässt sich die Zuordnung direkt von der Ladestelle aus pflegen (siehe Abschnitt 4.1).

### 3.7 Berechtigungen

Zur Nutzung des Moduls weisen Sie den Anwendern den mitgelieferten Berechtigungssatz **MuM ETAS All** zu. Er bestimmt die Berechtigungen für die Objekte dieses Moduls (Codeunits und Vorschauseiten) und legt damit fest, welche Anwender die Textkombination und die Vorschauseiten nutzen können.

---

## 4 Stammdaten

Dieses Modul erweitert nur eine klassische Stammdatenseite: die **Ladestelle**.

### 4.1 Ladestelle – erweiterte Texte pflegen

**Prozess-Intro:** Die **Ladestelle** ist eine logistische Stammdatenkarte des Basismoduls. Dieses Modul ergänzt dort die Aktion **Erweiterte Texte**, damit der Key-User die zu einer Ladestelle passenden Textzuordnungen unmittelbar von der Ladestelle aus einsehen und pflegen kann. Die dort gepflegten Zuordnungen wirken später in den Avisierungs- und Versandplanungszeilen mit der jeweiligen Ladestelle (Kapitel 6). Voraussetzung ist der Schalter **Ladestellen aktiviert** (Abschnitt 3.6).

**Einstieg:** Öffnen Sie die gewünschte **Ladestelle** und wählen Sie die Aktion **Erweiterte Texte**.

| Feld / Aktion | Erläuterung |
|---|---|
| **Erweiterte Texte** (Aktion) | Wenn gewählt, öffnet die Aktion das Arbeitsblatt der Textzuordnung gefiltert auf die aktuelle Ladestelle; angezeigt werden Zuordnungen mit **Subtyp = Ladestelle** (auf diese Ladestellennummer) sowie **Alle Ladestellen**. So sieht der Anwender genau die Texte, die für diese Ladestelle greifen, und kann sie ergänzen. |

Damit ist die Pflege ladestellenbezogener Texte ohne Umweg über die globale Suche möglich; sie ergänzt die Einrichtung aus Abschnitt 3.6.

---

## 5 Tägliche Arbeit

In der täglichen Arbeit ist das Modul weitgehend automatisch: Aufgrund der Einrichtung (Kapitel 3) erscheinen die Texte beim Bearbeiten der Belege selbstständig. Die folgenden Abschnitte beschreiben, an welchen Belegen welche Felder, Infoboxen und Aktionen dieses Moduls wirken.

Jeder logistische Beleg erhält im Bereich **Allgemein** zwei Steuerfelder dieses Moduls:

| Feld | Erläuterung |
|---|---|
| **Druckart** | Wenn gesetzt, steuert die Druckart, wie die zum Beleg gebildeten Texte behandelt werden (als InfoBox-, Bericht- oder Mail-Text); sie wird an die Infoboxen und die Vorschau weitergegeben, sodass dort genau die passende Textvariante angezeigt wird. |
| **Unterdruckart** | Wenn die Druckart **Bericht** ist, wählt die Unterdruckart die Druckposition (Kopfzeile, Fußzeile, Vor Position, Nach Position); bei anderen Druckarten ist das Feld gesperrt und ohne Wirkung. |

### 5.1 Versandplanung

**Steuernde Einrichtung:** Dieser Beleg wird durch die **Versandplanung Einrichtung** (Schalter **Versandplanung aktivieren**) und die im **Arbeitsblatt erweiterte Textzuordnung** hinterlegten Zuordnungen des Prozesses **Versandplanung** gesteuert (siehe Abschnitte 3.1, 3.3, 3.5).

**Einstieg:** Öffnen Sie die **Versandplanung** aus der Navigation des Logistikmoduls.

Ablauf:

1. **Versandplanung anlegen.** Beim Anlegen der Versandplanung bildet das Modul – sofern **Versandplanung aktivieren** gesetzt ist – automatisch die Kopftexte und stellt sie in der Infobox **Versandplanungstexte** dar.
2. **Zeilen holen.** Über die Aktion **Versandplanungszeilen holen** übernehmen Sie die zu liefernden Verkaufsauftragszeilen. Für jede übernommene Zeile bildet das Modul die Positionstexte und zeigt sie in der Infobox **Versandplanungszeilentexte**.
3. **Ladestelle setzen (optional).** Sobald in einer Zeile die Ladestelle geändert wird, ermittelt das Modul die ladestellenbezogenen Texte erneut.
4. **Vorschau öffnen (optional).** Über die Aktion **Erweiterte Versandplanungstexte** öffnen Sie die Vorschauseite (siehe Abschnitt 5.4), um die kombinierten Texte je Belegart zu prüfen oder neu zu erzeugen.

Die beiden Steuerfelder **Druckart** und **Unterdruckart** stehen im Kopf der Versandplanung zur Verfügung (siehe Tabelle oben).

### 5.2 Avisierung

**Steuernde Einrichtung:** Dieser Beleg wird durch die **Avisierung Einrichtung** (Schalter **Aktiviert**) und die Zuordnungen des Prozesses **Avisierung** gesteuert (siehe Abschnitte 3.1, 3.3, 3.4).

**Einstieg:** Öffnen Sie die **Avisierung** aus der Navigation des Logistikmoduls.

Ablauf:

1. **Avisierung anlegen.** Beim Anlegen der Avisierung bildet das Modul – sofern **Aktiviert** gesetzt ist – automatisch die Kopftexte und zeigt sie in der Infobox **Avisierungstexte**.
2. **Herkunftsbelege holen.** Über die Aktion **Herkunftsbelege holen** verknüpfen Sie z. B. eine Einkaufsbestellung mit der Avisierung. Für die dabei entstehenden Zeilen bildet das Modul die Positionstexte und zeigt sie in der Infobox **Avisierungszeilentexte**.
3. **Ladestelle setzen (optional).** Wie bei der Versandplanung werden die Zeilentexte bei Änderung der Ladestelle neu ermittelt.
4. **Vorschau öffnen (optional).** Über die Aktion **Erweiterte Avisierungstexte** öffnen Sie die Vorschauseite (siehe Abschnitt 5.4).

Auch hier stehen **Druckart** und **Unterdruckart** im Kopf zur Verfügung.

### 5.3 Versandplanungs-Zuordnung (Herkunft Verkauf/Einkauf)

**Steuernde Einrichtung:** Wie bei der Versandplanung; zusätzlich wird der Text aus dem Ursprungsbeleg (Verkaufs- bzw. Einkaufsbeleg) berücksichtigt.

Auf der Zuordnungsseite der Versandplanung (Zuordnung offener Belege) ergänzt das Modul zwei Infoboxen für Kopf- und Zeilentexte sowie die Aktion **Erweiterte Texte**.

| Aktion | Erläuterung |
|---|---|
| **Erweiterte Texte** | Wenn gewählt, öffnet die Aktion die erweiterten Texte des zugrunde liegenden Ursprungsbelegs: bei einer Verkaufsherkunft die Verkaufstexte, bei einer Einkaufsherkunft die Einkaufstexte. So kann der Anwender die Ausgangstexte einsehen, aus denen die Versandplanungstexte kombiniert werden. |

Die Infoboxen zeigen dabei automatisch die zum ausgewählten Ursprungsbeleg passenden Kopf- und Zeilentexte an.

### 5.4 Vorschauseiten „Erweiterte Avisierungstexte“ und „Erweiterte Versandplanungstexte“

**Prozess-Intro:** Beide Vorschauseiten sind gleich aufgebaut. Sie zeigen die kombinierten Texte eines Belegs, gruppiert nach **Belegart**, und erlauben das gezielte Neu-Erzeugen der Texte.

**Einstieg:** Öffnen Sie über die Aktion **Erweiterte Avisierungstexte** (an der Avisierung) bzw. **Erweiterte Versandplanungstexte** (an der Versandplanung) die jeweilige Vorschauseite.

| Feld / Bereich | Erläuterung |
|---|---|
| **Druckart** | Wenn gesetzt, filtert die Druckart, welche Textvariante in Vorschau und Infoboxen dargestellt wird (InfoBox, Bericht oder Mail). |
| **Unterdruckart** | Nur bei Druckart **Bericht** aktiv; bestimmt die betrachtete Druckposition (Kopfzeile, Fußzeile, Vor Position, Nach Position). |
| **Belegarten** (Liste) | Zeigt je Zeile eine **Belegart** und deren **Nr.**. Stimmt die Belegart mit der Herkunftsbelegart überein, wird die Zeile hervorgehoben. So erkennt der Anwender, welche Textquellen in den Beleg einfließen. |
| Bereich **Zeilen** (Unterseite) | Zeigt zur ausgewählten Belegart die Positionszeilen mit **Artikelnr.** und **Beschreibung** an, damit der Anwender die Zuordnung Text ↔ Position nachvollziehen kann. |

**Werte des Feldes Belegart** (welche Textquellen zusammengeführt werden):

- **Avisierung:** Texte, die dem Avisierungsprozess zugeordnet sind.
- **Reg. Avisierung:** Texte der bereits registrierten Avisierung.
- **Archivierte Avisierung:** Texte einer archivierten Avisierung.
- **Versandplanung:** Texte, die dem Versandplanungsprozess zugeordnet sind.
- **Reg. Versandplanung:** Texte der bereits registrierten Versandplanung.
- **Warenausgang:** Texte, die für den Warenausgang als Zielprozess der Versandplanung gebildet werden.

**Aktion auf der Vorschauseite:**

| Aktion | Erläuterung |
|---|---|
| **Erweiterte Texte für Belege erstellen** | Wenn gewählt, öffnet sich eine Auswahl mit zwei Möglichkeiten: (1) die erweiterten Texte **für das aktuelle Dokument und die aktuelle Belegart** neu erstellen bzw. aktualisieren, oder (2) **alle** Texte der Vorschau-Belegarten neu aufbauen und aktualisieren. So kann der Anwender die Texte nach einer geänderten Zuordnung gezielt neu erzeugen, ohne den Beleg neu anzulegen. |

---

## 6 E-Mail-Versand und Druck der Texte

Die zugeordneten Texte wirken nicht nur am Bildschirm, sondern auch beim Versand und Druck. Wie sie behandelt werden, steuert der **Drucktyp** der Vorlage:

- **InfoBox:** nur Bildschirmanzeige in den genannten Infoboxen; kein Druck, kein E-Mail-Text.
- **Bericht:** Der Text wird gemäß der **Unterdruckart** an der gewählten Position (Kopfzeile, Fußzeile, Vor Position, Nach Position) auf dem Bericht gedruckt.
- **Mail:** Beim E-Mail-Versand einer Avisierung wird der zugeordnete Text automatisch an den E-Mail-Text angehängt. Das Modul stellt dazu die passenden Kopf- und Zeilentexte zusammen; sind sowohl reine Infobox- als auch Mail-Texte vorhanden, wird der Mail-Text bevorzugt.

Auf diese Weise erhält der Empfänger genau die Hinweise, die der Key-User der jeweiligen Kombination aus Prozess, Geschäftspartner, Artikel bzw. Ladestelle zugeordnet hat.

---

## 7 Historie: Registrierte Belege

Beim **Registrieren** einer Avisierung oder Versandplanung werden die bis dahin am Arbeitsbeleg gebildeten erweiterten Texte in den registrierten Beleg übernommen und dort dauerhaft gespeichert; die Arbeitstexte des offenen Belegs werden dabei entfernt. So bleibt der gedruckte/versendete Textstand nachvollziehbar erhalten.

### 7.1 Registrierte Avisierung

**Einstieg:** Öffnen Sie die **Registrierte Avisierung**.

- Im Kopf werden die Felder **Druckart** und **Unterdruckart** schreibgeschützt angezeigt (Stand zum Zeitpunkt der Registrierung).
- Die Infoboxen **Avisierungstexte** und **Avisierungszeilentexte** zeigen die zum registrierten Beleg gehörenden Kopf- und Zeilentexte.

### 7.2 Registrierte Versandplanung

**Einstieg:** Öffnen Sie die **Registrierte Versandplanung**.

- Analog zur registrierten Avisierung werden **Druckart** und **Unterdruckart** schreibgeschützt angezeigt.
- Die Infoboxen **Versandplanungstexte** und **Versandplanungszeilentexte** zeigen die registrierten Kopf- und Zeilentexte.

Damit sind die Texte auch nach der Registrierung revisionssicher am Beleg abrufbar.

---

## 8 FAQ und Troubleshooting

### 8.1 Warum erscheinen in meiner Versandplanung keine Texte?

Prüfen Sie zuerst, ob in der **Versandplanung Einrichtung** der Schalter **Versandplanung aktivieren** gesetzt ist. Ist er nicht gesetzt, bildet das Modul keine Texte. Prüfen Sie anschließend, ob im **Arbeitsblatt erweiterte Textzuordnung** eine Zuordnung mit **Prozess = Versandplanung** existiert, die zum Debitor bzw. zur Debitorengruppe des Belegs passt.

### 8.2 Warum bleibt die Infobox „Avisierungstexte“ leer?

Die Avisierung muss über die **Avisierung Einrichtung** mit **Aktiviert** freigeschaltet sein, und es muss eine passende Zuordnung mit **Prozess = Avisierung** vorliegen. Ohne passenden **Typ** (z. B. der Kreditor der Avisierung oder **Alle Kreditoren**) findet das Modul keine Vorlage.

### 8.3 Warum bekomme ich beim Speichern die Meldung „Die Ladestellen sind nicht eingerichtet oder aktiviert.“?

Sie versuchen, eine Zuordnung mit **Subtyp = Ladestelle** oder **Alle Ladestellen** zu speichern, obwohl in der **Ladestellen Einrichtung** der Schalter **Ladestellen aktiviert** nicht gesetzt ist. Aktivieren Sie die Ladestellen zuerst (Abschnitt 3.6).

### 8.4 Was ist der Unterschied zwischen einem Kopftext und einem Positionstext?

Entscheidend ist das Feld **Subtyp**: Bleibt es **(leer)**, ist die Zuordnung ein **Kopftext** und erscheint in den Kopf-Infoboxen (**Avisierungstexte** / **Versandplanungstexte**). Ist der **Subtyp** gefüllt (Artikel, Artikelkategorie, Ladestelle …), ist es ein **Positionstext** und erscheint in den Zeilen-Infoboxen.

### 8.5 Warum kann ich die „Unterdruckart“ nicht auswählen?

Die **Unterdruckart** ist nur bei **Druckart = Bericht** aktiv. Bei **InfoBox** oder **Mail** ist das Feld gesperrt, weil die Druckposition nur für den Berichtsdruck eine Bedeutung hat.

### 8.6 Was passiert mit den Texten, wenn ich den Kreditor bzw. den Fahrerkontakt am Beleg ändere?

Das Modul erkennt die Änderung und baut die Kopftexte neu auf: Bei Änderung der Kreditornummer der Avisierung bzw. der externen Kontakt-Nr. (Fahrerkontakt) der Versandplanung werden die zugeordneten Texte neu ermittelt und ersetzt.

### 8.7 Warum ändern sich die Zeilentexte, nachdem ich die Artikelnummer oder die Ladestelle in der Zeile geändert habe?

Zeilentexte hängen von **Subtyp** (Artikel/Artikelkategorie/Ladestelle) ab. Ändern Sie in der Zeile die Artikelnummer oder die Ladestelle, ermittelt das Modul die passenden Positionstexte erneut, damit stets der richtige Text zur aktuellen Zeile angezeigt wird.

### 8.8 Muss ich eine Textvorlage vor der Zuordnung anlegen?

Ja. Im **Arbeitsblatt erweiterte Textzuordnung** verweist die **Vorlage Nr.** auf eine bestehende **Erweiterte Textvorlage**. Über den LookUp mit **+Neu** können Sie die Vorlage direkt anlegen, bevor Sie sie zuordnen.

### 8.9 Wo sehe ich, welche Texte tatsächlich in den Beleg einfließen?

Über die Aktion **Erweiterte Avisierungstexte** bzw. **Erweiterte Versandplanungstexte** öffnen Sie die Vorschauseite. Dort sind die kombinierten Texte nach **Belegart** gruppiert; mit **Erweiterte Texte für Belege erstellen** können Sie sie nach einer Zuordnungsänderung neu erzeugen.

### 8.10 Sind die Texte nach der Registrierung noch verfügbar?

Ja. Beim Registrieren werden die Texte in die **Registrierte Avisierung** bzw. **Registrierte Versandplanung** übernommen und bleiben dort abrufbar; die Arbeitstexte des offenen Belegs werden nach der Übernahme entfernt.

---

## 9 Typische Anwendungsfälle (Nutzungsbeispiele)

### 9.1 Standardhinweis auf jeder Versandplanung eines Kunden

**Auslöser:** Ein Debitor verlangt auf allen Lieferpapieren einen festen Verladehinweis. Die Anfrage kommt telefonisch beim Key-User an.

**Einstieg in BC:** Der Key-User öffnet über **Suchen** die **Erweiterten Textvorlagen** und legt eine Vorlage mit **Drucktyp = Bericht** und **Nebendruck Typ = Kopfzeile** an. Anschließend öffnet er das **Arbeitsblatt erweiterte Textzuordnung**.

**Kernablauf:**
1. Der Key-User trägt die **Vorlage Nr.** ein.
2. Er setzt **Prozess = Versandplanung**.
3. Er wählt **Typ = Debitor** und trägt in **Typ Nr.** den Kunden ein; **Subtyp** bleibt **(leer)** (Kopftext).
4. Der operative Anwender legt später eine **Versandplanung** für diesen Debitor an – der Hinweis erscheint automatisch in **Versandplanungstexte**.

**Abschluss:** Beim Registrieren wandert der Text in die **Registrierte Versandplanung**; beim Druck erscheint er in der Kopfzeile des Berichts.

### 9.2 Avisierungstext aus einer Einkaufsbestellung

**Auslöser:** Ein Kreditor kündigt eine Anlieferung an; die Ware soll avisiert werden.

**Einstieg in BC:** Der Anwender öffnet die **Avisierung** (Voraussetzung: **Aktiviert** in der **Avisierung Einrichtung**, Zuordnung mit **Prozess = Avisierung** und **Typ = Kreditor**/**Alle Kreditoren** vorhanden).

**Kernablauf:**
1. Der Anwender legt die Avisierung an – Kopftexte erscheinen in **Avisierungstexte**.
2. Über **Herkunftsbelege holen** verknüpft er die Einkaufsbestellung mit der Avisierung.
3. Für die übernommenen Zeilen erscheinen die Positionstexte in **Avisierungszeilentexte**.
4. Bei Bedarf prüft er das Ergebnis über **Erweiterte Avisierungstexte**.

**Abschluss:** Wird die Avisierung per E-Mail versendet und ist die Vorlage vom **Drucktyp Mail**, hängt das Modul den Text automatisch an die E-Mail an. Beim Registrieren bleibt der Textstand in der **Registrierten Avisierung** erhalten.

### 9.3 Text nur für eine bestimmte Ladestelle

**Auslöser:** Für eine bestimmte Ladestelle (Rampe) gilt eine besondere Anfahrtsregel, die auf den Positionen erscheinen soll.

**Einstieg in BC:** Der Key-User stellt sicher, dass in der **Ladestellen Einrichtung** der Schalter **Ladestellen aktiviert** gesetzt ist. Er öffnet die betreffende **Ladestelle** und wählt die Aktion **Erweiterte Texte**.

**Kernablauf:**
1. Der Key-User erfasst eine Zuordnung mit **Subtyp = Ladestelle** und der Ladestellennummer in **Subtyp Nummer** (Positionstext).
2. In der täglichen Arbeit setzt der Anwender in einer Versandplanungs- oder Avisierungszeile diese **Ladestelle**.
3. Das Modul ermittelt daraufhin den ladestellenbezogenen Text und zeigt ihn in **Versandplanungszeilentexte** bzw. **Avisierungszeilentexte**.

**Abschluss:** Der ladestellenbezogene Positionstext wird gemäß Drucktyp gedruckt, per E-Mail versendet oder nur angezeigt und beim Registrieren mit übernommen.
