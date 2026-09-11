---
title: Anwenderhandbuch m+m Test Certificate Mgt. with Additional Lot Info.
---

# Anwenderhandbuch m+m Test Certificate Mgt. with Additional Lot Info.

## Einleitung

Die Erweiterung **m+m Test Certificate Mgt. with Additional Lot Info.** ergänzt das Prüfzeugniswesen von Business Central um zusätzliche Chargeninformationen. Sie steuert, **auf welcher Charge-Ebene** ein Prüfzeugnis erzeugt wird (Prüfung, Charge, Lieferantencharge oder Charge inklusive ursprünglicher Charge), überträgt Probenwerte automatisch von einer Lieferantenchargenvorlage auf gleichartige Proben und verdichtet Prüfmerkmalswerte im Beleg zu **Minimal-, Maximal- und Durchschnittswerten**. Zusätzlich legt sie je **Norm** ein eigenes Berichtslayout fest.

Die Erweiterung setzt auf den Modulen **m+m Test Certificate Management**, **m+m Additional Lot Information** und **m+m Cloud Base** auf. Die Grundfunktionen des Prüfzeugniswesens (Prüfungen, Proben, Prüfvorlagen, Nummernserien, Quarantäne) stammen aus dem Basismodul und werden dort dokumentiert; das vorliegende Handbuch beschreibt ausschließlich die Felder, Seiten und Aktionen, die **diese** Erweiterung ergänzt.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender der Qualitätssicherung**, die täglich Proben erfassen und freigeben sowie Prüfzeugnisse (Belege) erstellen, drucken und per E‑Mail versenden. Sekundäre Zielgruppe sind **Administratoren und QS‑Verantwortliche**, die die Einrichtung vornehmen (Zeugniserstellungsart, Berichtslayout je Norm, Prüfgruppen-Norm-Zuweisung).

### Kurzer Prozessüberblick

Der administrative Weg verläuft von der zentralen Seite **Prüfdaten Einrichtung** (globale Vorbelegung der Zeugniserstellungsart und der Führungscharge) über die **Prüfgruppen-Norm-Zuweisung** (Druckwertoption je Prüfgruppe und Norm) bis zur Berichtszuordnung je **Norm**. Der operative Weg verläuft von der **Probe** (Erfassung der Lieferantenchargen-Informationen und optional einer Vorlage) über das **Prüfzeugnis** (Auswahl der Proben und Verdichtung der Werte) bis zur **Ausgabe** per **Beleg drucken** oder **E-Mail senden**.

### Zentrale Begriffe

- **Charge / Chargennr.** – die verfolgte Charge eines Artikels.
- **Lieferantencharge / Lieferantenchargen-Nr.** – die vom Lieferanten vergebene Chargennummer, die als eigenständige Gruppierung für Prüfzeugnisse dienen kann.
- **Ursprüngliche Charge** – die vorgelagerte Charge, aus der die aktuelle Charge hervorgegangen ist.
- **Prüfung / Prüfungsnr.** – der Prüfdatensatz zu einem Objekt (Basismodul).
- **Probe / Probenwert** – die einzelne Messung eines Prüfmerkmals innerhalb einer Prüfung.
- **Prüfzeugnis** – der ausgebbare Beleg (Seite **Prüfzeugnis**).
- **Norm** – die dem Prüfzeugnis zugrunde liegende Norm; steuert Layout und Druckwertoption.
- **Zeugniserstellungsart** – bestimmt die Gruppierungsebene des Prüfzeugnisses.

## Schnellstart für Anwender

Der Schnellstart folgt der technisch erzwungenen Reihenfolge: **zuerst einrichten, dann Stammdaten pflegen, dann arbeiten und ausgeben.**

**A. Einrichtung (einmalig, durch Administrator/QS):**

1. Öffnen Sie über **Suchen** die Seite **Prüfdaten Einrichtung**. Setzen Sie in der Gruppe **Zertifikat** die Vorbelegung der **Zeugniserstellungsart** und – nur bei **Lieferantenchargenrein** – der **Führungscharge**. Aktivieren Sie bei Bedarf **Probenwerte von Lieferantenchargenvorlage übertragen**.
2. Öffnen Sie die **Norm**-Liste und hinterlegen Sie je Norm **Berichts-ID**, **Berichtsart** und **Berichtslayoutname** (Aktion siehe Kapitel Einrichtung).
3. Öffnen Sie in der **Norm**-Liste bzw. in der **Prüfgruppen**-Liste über die Aktion **Prüfgruppen-Norm-Zuweisung** die gleichnamige Seite und setzen Sie je Prüfgruppe und Norm die **Druckwertoption**.

**B. Stammdaten (laufend, durch QS):**

4. Erfassen Sie in der Liste **Proben** bzw. in der Proben-Karte die Lieferantenchargen-Informationen. Kennzeichnen Sie eine repräsentative Probe je Lieferantencharge mit **Ist Lieferantenchargenvorlage** = ja.

**C. Tägliche Arbeit und Ausgabe (durch QS):**

5. Öffnen Sie das **Prüfzeugnis**. Prüfen Sie die aus der Einrichtung vorbelegte **Zeugniserstellungsart** und wählen Sie die **Norm** (**Norm Code**); bestätigen Sie die Rückfrage *„Sollen die Zeilen aktualisiert werden?"* mit Ja.
6. Fügen Sie die Werte hinzu: über **Probenwerte auswählen** (Standardweg) oder – bei chargen- bzw. lieferantenchargenbezogener Zeugniserstellungsart – über **Mehrere Proben auswählen**.
7. Kontrollieren Sie im Register **Wertezusammenfassung** die verdichteten Werte (Min./Max./Durchschnitt) je Prüfmerkmal.
8. Geben Sie den Beleg aus: **Beleg drucken** oder **E-Mail senden**.

## Einrichtung

Die Einrichtung ist zweistufig: Ein globales, unternehmensweites Setup auf der Seite **Prüfdaten Einrichtung** legt Vorgaben fest, die pro Norm bzw. pro Prüfgruppe verfeinert werden. Alle folgenden Einstellungen werden im Kapitel **Tägliche Arbeit** wieder aufgegriffen.

### Prüfdaten Einrichtung — Gruppe Zertifikat

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Prüfdaten Einrichtung**. Es handelt sich um eine unternehmensweite Einrichtungsseite (ein Datensatz je Mandant); ein übergeordneter Beleg existiert nicht.

**Wer/wann:** Der Administrator oder ein QS‑Verantwortlicher pflegt diese Seite **einmalig vor der ersten Zeugniserstellung**. Die hier gesetzten Werte werden beim Anlegen jedes neuen **Prüfzeugnisses** als Vorbelegung übernommen (Kapitel Tägliche Arbeit).

Die Erweiterung ergänzt die Basis-Einrichtungsseite um die folgenden Felder (das übrige Setup – Nummernserien, Quarantäne, E‑Mail – gehört zum Basismodul und wird dort gepflegt):

| Einrichtung | Erläuterung |
|---|---|
| **Probenwerte von Lieferantenchargenvorlage übertragen** | Wenn aktiviert, werden bei der Freigabe aller Proben die Probenwerte der als Vorlage markierten Probe automatisch auf alle offenen Proben mit **derselben Lieferantencharge** übertragen und diese Proben anschließend freigegeben; die QS erfasst die Werte damit nur einmal je Lieferantencharge statt je Probe. Ohne dieses Kennzeichen bleibt die automatische Übertragung aus, und jede Probe wird einzeln erfasst. |
| **Zeugniserstellungsart** | Legt die Vorbelegung der Gruppierungsebene für neue Prüfzeugnisse fest. Wenn hier ein Wert gesetzt ist, übernimmt jedes neue **Prüfzeugnis** diesen Wert automatisch, und die Belegzeilen sowie die Ausgabe werden entsprechend gruppiert (siehe Werteübersicht unten). |
| **Führungscharge** | Legt fest, welche Chargennummer im Beleg als führende Charge angedruckt wird. Nur editierbar und wirksam, wenn **Zeugniserstellungsart** = **Lieferantenchargenrein** ist; andernfalls wird das Feld automatisch geleert. Wenn **Lieferantencharge** gewählt ist, erscheint im Beleg die Lieferantenchargen-Nr. anstelle der internen Charge. |

**Werte der Zeugniserstellungsart** (jeder Wert bestimmt, wonach die Prüfzeugniszeilen gruppiert und wie sie im Beleg zusammengefasst werden):

- **Prüfungsrein:** Das Prüfzeugnis bezieht sich genau auf **eine Prüfung** (Prüfungsnr.); es findet keine chargenübergreifende Zusammenfassung statt. Dies ist auch die erzwungene Einstellung, wenn im Basismodul die automatische Prüfzeugniserstellung aktiv ist.
- **Chargenrein:** Die Zeilen werden nach **Chargennr.** gruppiert; das Zeugnis fasst alle Proben derselben Charge zusammen. Die Aktion **Mehrere Proben auswählen** ist verfügbar.
- **Lieferantenchargenrein:** Die Zeilen werden nach **Lieferantenchargen-Nr.** gruppiert; das Zeugnis fasst alle Proben derselben Lieferantencharge zusammen (auch über mehrere interne Chargen hinweg). Nur bei dieser Art ist die **Führungscharge** wirksam. Die Aktion **Mehrere Proben auswählen** ist verfügbar.
- **Charge inkl. ursprüngliche Charge:** Die Zeilen werden anhand der **ursprünglichen Charge** gruppiert; liegt keine ursprüngliche Charge vor, wird die aktuelle Charge herangezogen. Damit werden vorgelagerte Chargen mit in das Zeugnis einbezogen. Die Aktion **Mehrere Proben auswählen** ist verfügbar.

**Abhängigkeit (aus dem Code):** Ist im Basismodul das automatische Erstellen des Prüfzeugnisbelegs aktiv, setzt das System **Zeugniserstellungsart** zwingend auf **Prüfungsrein** und leert die **Führungscharge**. Die manuelle Auswahl einer anderen Zeugniserstellungsart bei aktiver automatischer Erstellung wird abgelehnt. Umgekehrt lässt sich die Zeugniserstellungsart nur ändern, wenn die automatische Erstellung deaktiviert ist.

### Probenwert-Übertragung je Lieferantencharge einrichten

Diese Prozesskette verbindet die globale Einrichtung, die Stammdatenpflege der Proben und die Freigabe im Tagesablauf. Sie richtet sich an den Administrator/QS‑Verantwortlichen und wird **vor** der ersten Freigabe von Proben mit gemeinsamer Lieferantencharge eingerichtet.

1. **Zuerst** aktivieren Sie in der **Prüfdaten Einrichtung** das Kennzeichen **Probenwerte von Lieferantenchargenvorlage übertragen**. Wenn aktiviert, ist die automatische Übertragung mandantenweit freigeschaltet.
2. **Danach** pflegen die QS‑Anwender in den Stammdaten (Kapitel **Proben & Chargeninformationen**) je Lieferantencharge genau **eine** Probe mit **Ist Lieferantenchargenvorlage** = ja. Wenn gesetzt, dient diese Probe als Wertevorlage; das System lässt je Lieferantencharge nur eine Vorlage zu.
3. **Schließlich** löst der Anwender im Tagesablauf die Freigabe aller Proben aus. Wenn dabei mindestens eine Vorlage und mindestens eine offene Probe mit gleicher Lieferantencharge vorhanden sind, überträgt das System die Werte und zeigt die Rückfrage *„Möchten Sie die Probenwerte der Lieferantencharge auf alle Proben mit derselben Lieferantencharge übertragen?"*. Bestätigt der Anwender, werden die Werte kopiert und die betroffenen Proben freigegeben.

**Validierung:** Das Kennzeichen **Ist Lieferantenchargenvorlage** kann nur bei einer Probe im Status *Offen* gesetzt werden; es setzt eine gefüllte **Lieferantenchargen-Nr.** voraus. Ein zweiter Vorlagen-Datensatz für dieselbe Lieferantencharge wird mit der Meldung *„… kann nur einmal gesetzt werden."* abgelehnt.

Der operative Abschluss dieser Kette ist im Kapitel **Proben & Chargeninformationen** und im Nutzungsbeispiel *Probenwertvorlage je Lieferantencharge* beschrieben.

### Berichte und Layout je Norm einrichten

Die Erweiterung verknüpft jede **Norm** mit einem eigenen Bericht und Berichtslayout. Diese Zuordnung steuert, welcher Bericht bei **Beleg drucken** und **E-Mail senden** verwendet wird. Zuständig ist der Administrator/QS‑Verantwortliche; die Einrichtung erfolgt **vor** dem ersten Druck eines Prüfzeugnisses zu dieser Norm.

**Einstieg:** Öffnen Sie die **Norm**-Liste (Normen des Prüfzeugniswesens). Die Berichtsfelder werden dort je Normzeile gepflegt.

| Feld | Erläuterung |
|---|---|
| **Berichts-ID** | Legt fest, welcher Bericht für diese Norm gedruckt wird. Wenn ein Wert gesetzt ist, verwendet die Ausgabe genau diesen Bericht; beim Anlegen einer neuen Norm wird der Standard-Prüfzeugnisbericht vorbelegt. Wird die Berichts-ID auf 0 zurückgesetzt, wird der hinterlegte **Berichtslayoutname** geleert. |
| **Berichtsname** | Zeigt den Namen des unter **Berichts-ID** gewählten Berichts an (nicht editierbar). Dient der Kontrolle, dass die richtige Berichtsdefinition zugeordnet ist. |
| **Berichtsart** | Legt fest, aus welchem Layouttyp gedruckt wird. Wenn ein Typ gewählt wird, prüft das System, ob für den Bericht ein Layout dieses Typs existiert, und lehnt andernfalls mit einer Meldung ab (z. B. *„Bericht ‚…' hat kein Word-Layout."*). Bei **Benutzerdefiniert** öffnet sich die Layoutauswahl. |
| **Berichtslayoutname** | Zeigt das ausgewählte Layout an (nicht editierbar). Wenn **Benutzerdefiniert** gewählt wurde, steht hier das aus der Layoutliste bestätigte Layout; bei integrierten Layouts steht hier **(Standard)**. |

**Werte der Berichtsart** (OptionCaption **RDLC,Word,Benutzerdefiniert,Excel,Extern**):

- **RDLC:** Verwendet das integrierte RDLC‑Layout des Berichts; die Layoutauswahl wird geleert. Existiert kein RDLC‑Layout, wird die Auswahl abgelehnt.
- **Word:** Verwendet das integrierte Word‑Layout; Auswahl analog RDLC.
- **Benutzerdefiniert:** Öffnet die Liste **Berichtslayouts** zur Auswahl eines konkreten Layouts; der Name und die Anwendungs‑ID des Layouts werden übernommen. Wird nichts ausgewählt, erscheint *„Es wurde kein Berichtslayout ausgewählt."*.
- **Excel:** Verwendet ein Excel‑Layout; existiert keines, wird abgelehnt.
- **Extern:** Verwendet ein externes Layout; existiert keines, wird abgelehnt.

Zwei weitere Felder auf dieser Zeile sind für Anwender ausgeblendet und werden hier zusammengefasst: die technische **Berichtslayout-App-ID** (intern, nicht sichtbar) sowie der **Benutzerdefinierter Berichtslayout-Code** (veraltet, wird bei einem Upgrade automatisch auf den neuen **Berichtslayoutname** migriert). Beide erfordern keine manuelle Pflege.

### Prüfgruppen-Norm-Zuweisung einrichten

Die **Prüfgruppen-Norm-Zuweisung** legt je Kombination aus **Prüfgruppe** und **Norm** fest, wie die Werte dieser Prüfgruppe im Beleg angedruckt werden (einzeln oder verdichtet). Sie ist die Voraussetzung für die verdichteten Min./Max./Durchschnitt-Werte im Prüfzeugnis. Zuständig ist der QS‑Verantwortliche; die Zuordnung wird gepflegt, sobald neue Normen oder Prüfgruppen im Einsatz sind.

**Einstieg:** Öffnen Sie die **Norm**-Liste und wählen Sie in der Zeile der Norm die Aktion **Prüfgruppen-Norm-Zuweisung** (die Seite ist auf den **Normcode** vorgefiltert). Alternativ öffnen Sie die **Prüfgruppen**-Liste und wählen dort dieselbe Aktion **Prüfgruppen-Norm-Zuweisung** (vorgefiltert auf den Gruppencode). Beide Wege öffnen dieselbe Seite **Prüfgruppen-Norm-Zuweisung**.

| Feld | Erläuterung |
|---|---|
| **Gruppencode** | Verweist auf die Prüfgruppe, für die die Regel gilt. Wenn gesetzt, wird der **Prüfgruppenname** automatisch nachgezogen; nur Werte aus den vorhandenen Prüfgruppen sind zulässig. |
| **Prüfgruppenname** | Zeigt die Bezeichnung der Prüfgruppe an (nicht editierbar); dient der eindeutigen Erkennung der Gruppe. |
| **Norm Code** | Verweist auf die Norm, für die die Regel gilt. Wenn gesetzt, wird die **Norm Beschreibung** nachgezogen; nur vorhandene Normen sind zulässig. |
| **Norm Beschreibung** | Zeigt die Bezeichnung der Norm an (nicht editierbar). |
| **Druckwertoption** | Legt fest, wie die Werte dieser Prüfgruppe unter dieser Norm im Beleg erscheinen (siehe Werte unten). Wenn eine andere Option als **Standard** gewählt ist, berechnet das System zusätzliche Kennwerte und zeigt sie in der **Wertezusammenfassung** an. |

**Werte der Druckwertoption:**

- **Standard:** Es werden die einzelnen Probenwerte angedruckt; keine zusätzliche Verdichtung.
- **Min./Max. Wert:** Zusätzlich werden der kleinste und der größte Wert je Prüfmerkmal berechnet und angedruckt.
- **Durchschnittswert:** Zusätzlich wird der Durchschnitt je Prüfmerkmal berechnet und angedruckt.
- **Min./Max. Wert und Durchschnittswert:** Es werden Minimal-, Maximal- und Durchschnittswert je Prüfmerkmal berechnet und angedruckt.

**Validierung / Abhängigkeit:** Wird eine Prüfgruppe oder eine Norm gelöscht, für die noch Zuweisungen bestehen, verhindert das System die Löschung mit der Meldung *„Die Tabelle … hat Einträge. Löschen Sie diese zuerst."*. Für Prüfmerkmale vom Werttyp *Text* oder *Media* wird stets **Standard** verwendet, da für sie keine Kennwerte berechnet werden können.

## Stammdaten

### Prüfgruppen-Norm-Zuweisung (Stammliste)

Die Seite **Prüfgruppen-Norm-Zuweisung** ist zugleich die Stammliste der Regeln aus dem vorigen Abschnitt. Sie zeigt je Zeile **Gruppencode**, **Prüfgruppenname**, **Norm Code**, **Norm Beschreibung** und **Druckwertoption** (Feldbedeutungen siehe oben). Über sie erhalten QS‑Anwender einen Gesamtüberblick, welche Prüfgruppen unter welchen Normen verdichtet angedruckt werden. Die Werte fließen unmittelbar in die Belegerstellung ein: Beim Setzen des **Norm Code** im Prüfzeugnis werden die Zeilen anhand dieser Zuordnung mit der jeweiligen **Druckwertoption** versehen.

### Proben & Chargeninformationen

Die Erweiterung ergänzt die Proben um Lieferantenchargen-Informationen. Diese Angaben steuern, ob eine Probe als Wertevorlage dient und mit welcher Charge sie im Beleg erscheint. Zuständig sind die QS‑Anwender; die Pflege erfolgt laufend bei der Probenerfassung.

**Einstieg:** Öffnen Sie die Liste **Proben** und darüber die zugehörige Proben-Karte. Die folgenden Felder erscheinen im Chargen-/Probenbereich der Karte; in der Liste **Proben** werden zusätzlich **Lieferantenchargen-Nr.** und **Ist Lieferantenchargenvorlage** als Spalten angezeigt.

| Feld | Erläuterung |
|---|---|
| **Lieferantenchargen-Nr.** | Zeigt die dem Lieferanten zugeordnete Chargennummer der Probe an (aus der Chargeninformation abgeleitet, nicht editierbar). Wenn gefüllt, kann die Probe zu einer lieferantenchargenreinen Zusammenfassung herangezogen werden und ist Voraussetzung für die Kennzeichnung als Vorlage. |
| **Ist Lieferantenchargenvorlage** | Wenn aktiviert, dient diese Probe als **Wertevorlage** für alle offenen Proben mit derselben Lieferantencharge; bei der Freigabe aller Proben werden deren Werte übernommen (siehe *Probenwert-Übertragung je Lieferantencharge einrichten*). Setzbar nur im Status *Offen* und nur bei gefüllter Lieferantenchargen-Nr.; je Lieferantencharge ist nur eine Vorlage zulässig. |
| **Lief.-Interne-Chargennr.** | Zeigt die interne Chargennummer des Lieferanten an (aus der Chargeninformation abgeleitet, nicht editierbar). Dient der Nachverfolgung, wenn Lieferant und eigenes System unterschiedliche Chargennummern führen. |
| **Ursprüngliche Chargennr.** | Zeigt die vorgelagerte Charge an, aus der die aktuelle Charge hervorgegangen ist (aus der Chargeninformation abgeleitet, nicht editierbar). Wird bei der Zeugniserstellungsart **Charge inkl. ursprüngliche Charge** zur Gruppierung der Belegzeilen genutzt. |

**Probenwerteintrag (Basisfeld der Prüfung):** Die Erweiterung ergänzt das Basisfeld **Probenwerteintrag** um drei zusätzliche Verfahren, die festlegen, aus welcher vorhandenen Probe fehlende Werte automatisch übernommen werden, wenn keine passende Probe vorliegt:

- **Urspr. Charge gleiche Prüfung:** Es wird eine bereits erfasste Probe **derselben Prüfung** mit der ursprünglichen Charge herangezogen.
- **Urspr. Charge gleiche Prüfungsvorlage:** Es wird eine Probe zur ursprünglichen Charge herangezogen, deren Prüfung **dieselbe Prüfvorlage und Vorlagenversion** verwendet.
- **Urspr. Charge Gesamt (Letzte Prüfung):** Es wird die zuletzt vorhandene Probe zur ursprünglichen Charge herangezogen, unabhängig von Prüfung oder Vorlage.

In allen drei Fällen muss eine **ursprüngliche Charge** hinterlegt sein; fehlt sie, greift das Verfahren nicht.

## Tägliche Arbeit: Prüfzeugnis erstellen

Der zentrale Beleg dieser Erweiterung ist das **Prüfzeugnis**. Dieser Abschnitt setzt voraus, dass die im Kapitel **Einrichtung** beschriebenen Vorgaben gepflegt sind: die **Zeugniserstellungsart** und **Führungscharge** in der **Prüfdaten Einrichtung**, das Berichtslayout in der **Norm**-Liste und die **Druckwertoption** in der **Prüfgruppen-Norm-Zuweisung**.

### Kopf des Prüfzeugnisses

Beim Anlegen eines neuen Prüfzeugnisses übernimmt das System aus der **Prüfdaten Einrichtung** automatisch die **Zeugniserstellungsart** und die **Führungscharge** in den Belegkopf. Die Erweiterung ergänzt den Kopf um folgende Felder:

| Feld | Erläuterung |
|---|---|
| **Zeugniserstellungsart** | Bestimmt für diesen Beleg die Gruppierungsebene (Prüfungsrein, Chargenrein, Lieferantenchargenrein, Charge inkl. ursprüngliche Charge; Bedeutungen siehe Kapitel Einrichtung). Wenn der Wert geändert wird, aktiviert bzw. deaktiviert das System die Aktion **Mehrere Proben auswählen** entsprechend. Bei einem anderen Wert als **Lieferantenchargenrein** wird die **Führungscharge** automatisch geleert. |
| **Führungscharge** | Bestimmt, welche Charge im Beleg als führende Charge angedruckt wird. Nur bei **Lieferantenchargenrein** wirksam; bei Auswahl **Lieferantencharge** erscheint im Beleg die Lieferantenchargen-Nr. als führende Charge. |

### Werte auswählen

Zum Füllen der Belegzeilen stehen zwei Aktionen zur Verfügung:

- **Probenwerte auswählen** (Basisaktion): Öffnet die Probenwertauswahl zur aktuell im Kopf gesetzten Prüfung. Dieser Weg wird bei **Prüfungsrein** genutzt.
- **Mehrere Proben auswählen** (Aktion dieser Erweiterung): Nur aktiv, wenn die **Zeugniserstellungsart** **Chargenrein**, **Charge inkl. ursprüngliche Charge** oder **Lieferantenchargenrein** ist. Öffnen Sie über die Aktion **Mehrere Proben auswählen** die passende Auswahlliste:
  - bei **Chargenrein** und **Charge inkl. ursprüngliche Charge** die **Chargennr.-Information** (bei „inkl. ursprüngliche Charge" werden zusätzlich die verketteten ursprünglichen Chargen einbezogen),
  - bei **Lieferantenchargenrein** die Liste **Lieferantenchargen**.

  Nach Auswahl übernimmt das System alle Proben(werte) der gewählten Charge bzw. Lieferantencharge in die Belegzeilen und berechnet anschließend die verdichteten Werte neu.

**Norm setzen:** Setzen Sie im Register **Norm** den **Norm Code**. Bestehen bereits Zeilen, erscheint die Rückfrage *„Sollen die Zeilen aktualisiert werden?"*. Bei Bestätigung erhält jede Zeile die in der **Prüfgruppen-Norm-Zuweisung** hinterlegte **Druckwertoption**; für Text-/Media-Merkmale bleibt es bei **Standard**.

### Wertezusammenfassung

Die Erweiterung blendet im Prüfzeugnis das Register **Wertezusammenfassung** ein (nicht editierbar). Es zeigt die aus den Belegzeilen berechneten Kennwerte je Prüfmerkmal:

| Feld | Erläuterung |
|---|---|
| **Druckschlüssel** | Fasst die Zeilen zu einer Gruppierungseinheit zusammen (je nach Zeugniserstellungsart Prüfungsnr., Chargennr., ursprüngliche Charge oder Lieferantencharge). Dient als Ordnungsmerkmal der Verdichtung. |
| **Prüfgruppenname** | Zeigt die Prüfgruppe des Kennwerts an. |
| **Prüfmerkmalsbeschreibung** | Zeigt das Prüfmerkmal an, für das der Kennwert gilt. |
| **Wertoption** | Gibt an, um welchen Kennwert es sich handelt: **Min.**, **Max.** oder **Durchschnitt**. |
| **Wert** | Zeigt den berechneten Kennwert an (Minimum, Maximum bzw. auf drei Nachkommastellen gerundeter Durchschnitt). |

Die Verdichtung wird automatisch neu berechnet, sobald Belegzeilen hinzukommen oder gelöscht werden oder der **Norm Code** geändert wird. Welche Kennwerte tatsächlich erscheinen, hängt von der **Druckwertoption** der jeweiligen Prüfgruppe ab (siehe Prüfgruppen-Norm-Zuweisung).

## Ausgabe: Drucken und Versenden

Nachdem die Belegzeilen gefüllt und die Werte verdichtet sind, wird das Prüfzeugnis ausgegeben. Die Ausgabe verwendet den je **Norm** eingerichteten Bericht und das eingerichtete Layout (Kapitel *Berichte und Layout je Norm einrichten*).

1. **Beleg drucken:** Erzeugt den Ausdruck. Ist der Norm ein eigener Bericht zugeordnet, wird dieser verwendet; andernfalls der Standard-Prüfzeugnisbericht. Ohne hinterlegte Norm findet keine Ausgabe statt.
2. **E-Mail senden:** Erzeugt das Prüfzeugnis als PDF und übergibt es an den E‑Mail-Versand des Belegs.

**Andruck der Werte:** Für Prüfgruppen mit einer anderen **Druckwertoption** als **Standard** werden anstelle bzw. zusätzlich zu den Einzelwerten die Spalten **Min.**, **Max.** und/oder **Durchschnitt** aus der **Wertezusammenfassung** angedruckt. Bei der Führungscharge **Lieferantencharge** erscheint die Lieferantenchargen-Nr. als führende Chargenangabe im Beleg.

## FAQ und Troubleshooting

### Warum kann ich die Zeugniserstellungsart nicht ändern?
Ist im Basismodul das automatische Erstellen des Prüfzeugnisbelegs aktiv, erzwingt das System **Prüfungsrein** und leert die **Führungscharge**. Deaktivieren Sie zuerst die automatische Erstellung, um eine andere Zeugniserstellungsart wählen zu können.

### Warum ist das Feld Führungscharge ausgegraut?
Die **Führungscharge** ist nur bei der Zeugniserstellungsart **Lieferantenchargenrein** editierbar. Bei jeder anderen Art wird das Feld gesperrt und automatisch geleert.

### Warum ist die Aktion „Mehrere Proben auswählen" deaktiviert?
Die Aktion ist nur aktiv, wenn die **Zeugniserstellungsart** **Chargenrein**, **Charge inkl. ursprüngliche Charge** oder **Lieferantenchargenrein** ist. Bei **Prüfungsrein** verwenden Sie stattdessen **Probenwerte auswählen**.

### Warum werden die Probenwerte bei der Freigabe nicht übertragen?
Die automatische Übertragung setzt drei Bedingungen voraus: das Kennzeichen **Probenwerte von Lieferantenchargenvorlage übertragen** in der **Prüfdaten Einrichtung** ist aktiv, es existiert eine Probe mit **Ist Lieferantenchargenvorlage** = ja und gefüllter **Lieferantenchargen-Nr.**, und es gibt offene Proben mit derselben Lieferantencharge.

### Warum erhalte ich die Meldung „… kann nur einmal gesetzt werden."?
Je Lieferantencharge ist nur **eine** Vorlage zulässig. Es existiert bereits eine Probe mit **Ist Lieferantenchargenvorlage** = ja und derselben Lieferantenchargen-Nr. Entfernen Sie zuerst die bestehende Kennzeichnung.

### Warum kann ich „Ist Lieferantenchargenvorlage" nicht setzen?
Das Kennzeichen ist nur im Status *Offen* und nur bei gefüllter **Lieferantenchargen-Nr.** setzbar. Prüfen Sie den Status der Probe und ob eine Lieferantencharge hinterlegt ist.

### Warum erscheinen keine Min./Max.- oder Durchschnittswerte im Beleg?
Diese Kennwerte erscheinen nur, wenn in der **Prüfgruppen-Norm-Zuweisung** für die betreffende Prüfgruppe und Norm eine andere **Druckwertoption** als **Standard** gesetzt ist. Für Prüfmerkmale vom Typ *Text* oder *Media* bleibt es stets bei **Standard**.

### Warum lässt sich eine Prüfgruppe oder Norm nicht löschen?
Bestehen noch Einträge in der **Prüfgruppen-Norm-Zuweisung**, verhindert das System die Löschung mit *„Die Tabelle … hat Einträge. Löschen Sie diese zuerst."*. Entfernen Sie zunächst die zugehörigen Zuweisungen.

### Warum meldet das System „Bericht ‚…' hat kein Word-Layout." (o. ä.)?
Die gewählte **Berichtsart** erwartet ein Layout dieses Typs, das für den unter **Berichts-ID** hinterlegten Bericht nicht existiert. Wählen Sie eine passende Berichtsart oder hinterlegen Sie das entsprechende Layout.

### Warum wird beim Druck kein Beleg erzeugt?
Die Ausgabe setzt eine gesetzte **Norm** (Norm Code) sowie vorhandene Belegzeilen voraus. Ohne Norm oder ohne Zeilen bricht **Beleg drucken** bzw. **E-Mail senden** ohne Ausgabe ab.

## Typische Anwendungsfälle

### 1. Ein Prüfzeugnis je Lieferantencharge über mehrere interne Chargen

**Auslöser:** Ein Kunde fordert ein Prüfzeugnis, das sich auf die **Lieferantencharge** bezieht, obwohl die Ware im eigenen Lager auf mehrere interne Chargen aufgeteilt wurde.

**Einstieg in BC:** Der QS‑Anwender öffnet das **Prüfzeugnis**. Die Vorbelegung **Zeugniserstellungsart** = **Lieferantenchargenrein** stammt aus der **Prüfdaten Einrichtung**; ist sie dort nicht gesetzt, wählt der Anwender sie im Kopf und setzt die **Führungscharge** = **Lieferantencharge**.

**Kernablauf:** Über **Mehrere Proben auswählen** öffnet der Anwender die Liste **Lieferantenchargen** und wählt die betreffende Lieferantencharge. Das System übernimmt alle zugehörigen Proben – über alle internen Chargen hinweg – in die Belegzeilen. Anschließend setzt der Anwender den **Norm Code** und bestätigt *„Sollen die Zeilen aktualisiert werden?"*; die Zeilen erhalten die **Druckwertoption** aus der **Prüfgruppen-Norm-Zuweisung**. In der **Wertezusammenfassung** kontrolliert der Anwender die verdichteten Werte.

**Abschluss:** Der Anwender gibt den Beleg über **Beleg drucken** aus; im Beleg erscheint die Lieferantenchargen-Nr. als führende Charge.

### 2. Probenwertvorlage je Lieferantencharge

**Auslöser:** Für eine Lieferantencharge treffen mehrere Wareneingänge (interne Chargen) ein; die Werte sind laut Lieferantenzeugnis identisch und sollen nicht mehrfach erfasst werden.

**Einstieg in BC:** Der QS‑Anwender öffnet die Liste **Proben** und die zugehörige Proben-Karte. Voraussetzung ist das aktive Kennzeichen **Probenwerte von Lieferantenchargenvorlage übertragen** in der **Prüfdaten Einrichtung**.

**Kernablauf:** Der Anwender erfasst die Werte an **einer** Probe mit gefüllter **Lieferantenchargen-Nr.** und setzt dort **Ist Lieferantenchargenvorlage** = ja (nur im Status *Offen* möglich). Danach löst er die Freigabe aller Proben aus. Das System zeigt die Rückfrage *„Möchten Sie die Probenwerte der Lieferantencharge auf alle Proben mit derselben Lieferantencharge übertragen?"*.

**Abschluss:** Nach Bestätigung überträgt das System die Werte auf alle offenen Proben mit derselben Lieferantencharge und gibt diese frei. Die Proben stehen damit vollständig für die Zeugniserstellung bereit.

### 3. Verdichtete Kennwerte je Norm im Prüfzeugnis

**Auslöser:** Ein Prüfzeugnis soll je Prüfmerkmal nicht alle Einzelwerte, sondern **Minimum, Maximum und Durchschnitt** ausweisen, wie es die geforderte Norm verlangt.

**Einstieg in BC:** Der QS‑Verantwortliche öffnet über die Aktion **Prüfgruppen-Norm-Zuweisung** (aus der **Norm**- oder **Prüfgruppen**-Liste) die gleichnamige Seite.

**Kernablauf:** Für die betreffende Prüfgruppe und Norm setzt er die **Druckwertoption** = **Min./Max. Wert und Durchschnittswert**. Anschließend erstellt der Anwender das **Prüfzeugnis**, füllt die Zeilen (über **Probenwerte auswählen** bzw. **Mehrere Proben auswählen**) und setzt den **Norm Code**; die Zeilen erhalten automatisch die Druckwertoption. Die berechneten Kennwerte erscheinen in der **Wertezusammenfassung**.

**Abschluss:** Über **Beleg drucken** oder **E-Mail senden** wird der Beleg ausgegeben; für die betroffenen Prüfgruppen werden die Spalten **Min.**, **Max.** und **Durchschnitt** angedruckt.
