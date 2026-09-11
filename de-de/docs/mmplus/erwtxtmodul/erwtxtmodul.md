---
title: Anwenderhandbuch m+m Erweiterte Texte
---

# Anwenderhandbuch m+m Erweiterte Texte

## Einleitung
Die App m+m Erweiterte Texte erweitert Microsoft Dynamics 365 Business Central um gepflegte Zusatztexte fuer Belege, Buchungen, Mailtexte, Arbeitsplaene und Vorschauansichten. Anwender arbeiten dabei nicht in AL-Objekten, sondern in klaren BC-Oberflaechen wie **Erweiterte Texteinstellungen**, **Erweiterte Textvorlagen**, **Arbeitsblatt erweiterte Textzuordnung** und den erweiterten Feldern bzw. Infoboxen direkt in Verkaufs-, Einkaufs-, Umlagerungs-, Lager- und Produktionsbelegen.

Das Modul deckt drei typische Aufgaben ab:

1. Vorlagen, Prozesse und Platzhalter einrichten.
2. Vorlagen einzelnen Geschaeftsfaellen, Partnern oder Prozessen zuordnen.
3. Zusatztexte in Belegen, gebuchten Belegen, Mails und Berichten anzeigen, pruefen und bei Bedarf aktualisieren.

Der fachliche Schwerpunkt liegt auf dem geordneten Zusammenspiel von Vorlagen, Zuordnung und Ausgabeart. Ein Text kann als InfoBox, als Berichtstext, als Mailtext oder als Mailbetreff genutzt werden. Bei Berichtstexten kommt zusaetzlich die Position des Textes hinzu, zum Beispiel Kopfzeile, Fusszeile, Vor Position oder Nach Position.

## Schnellstart fuer Anwender
### Schnellstart fuer Administratoren
1. Oeffnen Sie ueber **Tell Me** die Seite **Erweiterte Texteinstellungen**.
2. Hinterlegen Sie mindestens die Nummernserie fuer Vorlagen und pruefen Sie Sprache, Platzhaltergrenzen und Mailverhalten.
3. Oeffnen Sie danach **Erweiterte Textvorlagen** und legen Sie die benoetigten Textvorlagen an.
4. Pflegen Sie die eigentlichen Texte direkt in der Vorlagenkarte in der FactBox **Erweiterter Text**.
5. Falls mehrsprachige Texte noetig sind, oeffnen Sie pro Vorlage die Aktion **Uebersetzung** und erfassen Sie Sprachvarianten.
6. Wechseln Sie in das **Arbeitsblatt erweiterte Textzuordnung** und ordnen Sie die Vorlage einem Typ, einem Typcode sowie optional Subtyp, Prozessgruppe oder Prozess zu.
7. Pruefen Sie anschliessend einen Beleg, zum Beispiel einen Verkaufsauftrag oder eine Verkaufsgutschrift. Das Modul zeigt die Zusatztexte in den eingeblendeten FactBoxen oder im Aufruf **Erweiterter Text**.

### Schnellstart fuer Fachanwender im Tagesgeschaeft
1. Oeffnen Sie den gewuenschten Beleg, zum Beispiel Verkaufsauftrag, Verkaufsgutschrift, Rahmenauftrag, Einkaufsbestellung oder Umlagerungsauftrag.
2. Pruefen Sie das Feld fuer den Drucktyp und bei Berichtsausgabe den Nebendrucktyp.
3. Oeffnen Sie bei Bedarf die Aktion **Erweiterter Text**, um die zugeordneten Kopf- und Zeilentexte zu sehen.
4. Nutzen Sie in gebuchten Belegen oder Versandbelegen die eingeblendeten Text-FactBoxen, um die ausgegebene Version zu kontrollieren.
5. Nutzen Sie die Aktion **E-Mail**, wenn der Beleg per Mail versendet wird und der Mailtext aus den erweiterten Texten stammen soll.

## Einrichtung
### Erweiterte Texteinstellungen
Die zentrale Administration erfolgt auf der Seite **Erweiterte Texteinstellungen**.

| Einrichtung | Erlaeuterung |
| --- | --- |
| Template Nos. | Nummernserie fuer neue Textvorlagen. Ohne Nummernserie laesst sich die Vorlagenkarte nicht komfortabel per AssistEdit anlegen. |
| Language Code | Standardsprache fuer die Textaufbereitung. Die Sprache wirkt sich auf Vorlagen und Uebersetzungen aus. |
| Placeholder Start | Startzeichen fuer Platzhalter in Texten. |
| Placeholder End | Endzeichen fuer Platzhalter in Texten. |
| Email Placeholders | Steuert, ob Platzhalter nur beim Senden ersetzt werden oder ob der ersetzte Inhalt gespeichert wird. Werte: leer, Ersetzung nur beim Senden, Ersetzung beim Senden und Speichern. |
| Preferred Email Text | Legt fest, ob Mailtexte bevorzugt aus Mailvorlagen oder aus InfoBox-Texten gezogen werden. Werte: Mailtext verwenden, stattdessen InfoBox-Text verwenden. |
| Preview texts in source docs. | Aktiviert die Vorschau direkt im Ursprungsbeleg. |
| FactBox Texts to Report | Uebergibt FactBox-Texte in die Berichtsausgabe. |
| Copy Text | Uebernimmt Zusatztexte beim Kopieren von Belegen. |
| Auto. Ext. Text Posting | Uebertraegt bzw. erzeugt Zusatztexte beim Buchen automatisch. |
| Trans. Rout. Text to P. Order | Uebernimmt Arbeitsplantexte in Produktionsauftraege. |
| Trans. Prod. Text Chg. Status | Beruecksichtigt Produktionsstatuswechsel fuer Textuebernahmen. |
| Create Purch Hdr Text Backg | Aktiviert Hintergrundverarbeitung fuer Einkaufskopftexte. |
| Create Purch Line Text Backg | Aktiviert Hintergrundverarbeitung fuer Einkaufszeilentexte. |
| Create Sales Hdr Text Backg | Aktiviert Hintergrundverarbeitung fuer Verkaufskopftexte. |
| Create Sales Line Text Backg | Aktiviert Hintergrundverarbeitung fuer Verkaufszeilentexte. |
| MuM MPET Use PO Item Mat.Prop. | Zusatzfeld aus einer Erweiterung fuer Materialeigenschaften auf Einkaufsartikeln. Nur relevant, wenn die zugehoerige Erweiterung im Einsatz ist. |
| MuM MPET Formula Start/End | Zusatzfeld fuer Formelumrahmung in Verbindung mit Materialeigenschaftstexten. |
| MuM MPET Sub Formula Start | Zusatzfeld fuer Unterformeln in Verbindung mit Materialeigenschaftstexten. |
| MuM MPET Sub Formula End | Zusatzfeld fuer Unterformeln in Verbindung mit Materialeigenschaftstexten. |
| MuM MPET Auto Update Ext. Text | Aktualisiert erweiterte Texte automatisch fuer die Materialeigenschaftserweiterung. |

Zusatzaktionen in den **Erweiterten Texteinstellungen**:

| Aktion | Erlaeuterung |
| --- | --- |
| Prozesse erstellen | Erstellt bzw. initialisiert Prozessdaten fuer die FactBox- und Ausgabesteuerung. |
| Prozesse | Oeffnet die Prozessliste. |
| Platzhalter | Oeffnet die Platzhalterverwaltung. |

### Vorlagen anlegen und pflegen
Die eigentliche Textpflege beginnt auf den Seiten **Erweiterte Textvorlagen** und **Erweiterte Textvorlagenkarte**.

| Feld | Erlaeuterung |
| --- | --- |
| Template No. | Eindeutige Vorlagennummer. Sie wird ueber die Nummernserie vergeben oder manuell gepflegt. |
| Template Text | Kurzbezeichnung bzw. Textschluessel der Vorlage. |
| Description | Fachliche Beschreibung der Vorlage. |
| Printing Type | Bestimmt die Ausgabeart. Werte: InfoBox, Bericht, Mail, Mail Subject. |
| Starting Date | Startdatum der Gueltigkeit. |
| Ending Date | Enddatum der Gueltigkeit. |
| Assignment Worksheet | Kennzeichen, ob die Vorlage bereits einer Zuordnung dient. |
| Translation Exists | Zeigt an, ob Uebersetzungen vorhanden sind. |
| Legacy Data | Kennzeichnet Altdaten. |
| Sub-Printing Type | Nur bei Drucktyp Bericht sichtbar. Werte: leer, Kopfzeile, Fusszeile, Vor Position, Nach Position. |

Vorgehen in der Vorlagenkarte:

1. Legen Sie die Vorlage an.
2. Waehlen Sie zuerst den Drucktyp.
3. Pflegen Sie bei Berichtsausgabe anschliessend den Nebendrucktyp.
4. Erfassen Sie den eigentlichen Inhalt in der FactBox **Erweiterter Text**.
5. Nutzen Sie bei Bedarf die Aktion **Vorlage kopieren**, wenn eine bestehende Vorlage als Ausgangspunkt dienen soll.
6. Nutzen Sie die Aktion **Uebersetzung**, wenn derselbe Inhalt in mehreren Sprachen benoetigt wird.

### Uebersetzungen pflegen
Mehrsprachige Vorlagen werden ueber **Erweiterte Textuebersetzungen** gepflegt.

| Feld | Erlaeuterung |
| --- | --- |
| Language Code | Sprachcode der Uebersetzung. |
| Template Text | Anzeige der zugehoerigen Vorlage. |
| Language Name | Bezeichnung der Sprache. |

In der Praxis gehen Sie so vor:

1. Oeffnen Sie die Vorlage.
2. Rufen Sie **Uebersetzung** auf.
3. Erfassen Sie eine Zeile je Sprache.
4. Pflegen Sie den eigentlichen Text in der zugehoerigen Text-FactBox.

### Platzhalter vorbereiten
Die Seite **Liste der Platzhalter** steuert, welche Platzhalter in Texten verwendet werden duerfen.

| Feld | Erlaeuterung |
| --- | --- |
| Placeholder | Technischer Platzhalter, der im Text eingefuegt wird. |
| System Procedures | Vordefinierter Systemwert. Moegliche Werte: leer, User ID, Work Date, Today Date, Current Time. |
| Table ID | Quelltabelle fuer den Platzhalter, wenn kein Systemwert verwendet wird. |
| Table Name | Anzeigename der Quelltabelle. |
| Field No. | Quellfeld fuer die Ausgabe. |
| Field Name | Anzeigename des Quellfelds. |
| Related Table | Zugehoerige Beziehungstabelle fuer indirekte Werte. |
| Related Table Field | Beziehungsfeld in der verknuepften Tabelle. |
| Related Field Name | Anzeigename des verknuepften Felds. |
| Free Text | Freitext fuer spezielle Platzhalterlogik. |
| Picture | Bildinhalt fuer bildbasierte Platzhalter. |
| Resize % | Groessenanpassung in Prozent. |
| Height | Feste Hoehe fuer Bildplatzhalter. |
| Width | Feste Breite fuer Bildplatzhalter. |

Nutzen Sie Platzhalter vor allem dann, wenn sich Inhalte je Beleg, Partner, Datum oder Benutzer aendern sollen.

## Stammdaten und Zuordnungen
### Prozesse
Auf der Seite **Erweiterte Textprozesse** wird festgelegt, an welches Objekt ein Textprozess gebunden ist.

| Feld | Erlaeuterung |
| --- | --- |
| Code | Kennung des Prozesses. |
| Print Type | Ausgabeart des Prozesses: InfoBox, Bericht, Mail oder Mail Subject. |
| Description | Fachliche Beschreibung des Prozesses. |
| Object Type | Art des Zielobjekts. Im Modul sind insbesondere Seite und Bericht vorgesehen. |
| Object No. | Objekt-ID der Seite oder des Berichts. |
| Object Name | Anzeigename des Objekts. |
| Process Assignements | Kennzeichen bzw. Anzahl bestehender Zuweisungen. |

Die Aktion **Process Report Assignement** ist nur fuer Prozesse mit Ausgabeart **Bericht** verfuegbar. Damit pruefen Sie, an welche Berichtsausgabe ein Prozess gekoppelt ist.

### Prozessgruppen
Wenn mehrere Prozesse zusammengefasst werden sollen, nutzen Sie **Erweiterte Textprozessgruppen**.

| Feld | Erlaeuterung |
| --- | --- |
| Code | Kennung der Prozessgruppe. |
| Description | Beschreibung der Gruppe. |
| Synchronization Type | Ausgabeart der Gruppe. Sie muss zur Ausgabeart der enthaltenen Prozesse passen. |

In den Zeilen der Prozessgruppe pflegen Sie mindestens:

| Feld | Erlaeuterung |
| --- | --- |
| Process Code | Verknuepfter Prozess. Die Lookup-Auswahl ist auf passende Prozesse der gleichen Ausgabeart begrenzt. |

### Arbeitsblatt erweiterte Textzuordnung
Die eigentliche fachliche Zuordnung erfolgt im **Arbeitsblatt erweiterte Textzuordnung**.

| Feld | Erlaeuterung |
| --- | --- |
| Template No. | Verweist auf die Textvorlage. |
| Template Print Type | Ausgabeart der Vorlage. Wird bei leerer Vorlagennummer direkt gepflegt. |
| Type | Oberkategorie der Zuordnung. Moegliche Werte sind unter anderem Debitor, Kreditor, Alle Debitoren, Alle Kreditoren, Debitorengruppe, Kreditorengruppe, Lagerort, Alle Lagerorte, Arbeitsplaene und Alle Arbeitsplaene. |
| Type No. | Nummer innerhalb des gewaehlten Typs, zum Beispiel Debitorennummer, Kreditorennummer oder Lagerortcode. |
| Sub Type | Unterkategorie. Moegliche Werte sind unter anderem Alle Artikel, Artikelkategorie, Artikel, Alle Maschinenplaetze, Maschinenplatz, Alle Arbeitsplaetze, Arbeitsplatz und Lieferadresse. |
| Sub Type No. | Nummer bzw. Code zum gewaehlten Subtyp. |
| Process Group Code | Optionale Prozessgruppe fuer die Ausgabe. |
| Process Code | Optionale direkte Prozesssteuerung. |
| Process Object Name | Anzeigename des hinterlegten Prozessobjekts. |
| Legacy Data | Kennzeichen fuer Altdaten. |

Reihenfolge fuer eine saubere Zuordnung:

1. Vorlage auswaehlen.
2. Typ und Typnummer festlegen.
3. Falls noetig Subtyp und Subtypnummer ergaenzen.
4. Danach Prozessgruppe oder einzelnen Prozess zuordnen.
5. Ueber die Text- und Uebersetzungs-FactBox kontrollieren, ob die richtigen Inhalte hinterlegt sind.

Die Seite enthaelt zudem wichtige Aktionen fuer den laufenden Betrieb:

| Aktion | Erlaeuterung |
| --- | --- |
| Vorlagenkarte | Oeffnet die zugehoerige Vorlagenkarte. |
| Uebersetzung | Oeffnet die Uebersetzungen der markierten Vorlage. |
| Zugehoerige Zeilen anzeigen | Fuehrt die Kombination der erweiterten Texte zusammen und zeigt die Wirkung der Zuordnung. |
| Platzhalter | Oeffnet die Platzhalterliste. |
| Excel-Vorlage exportieren | Stellt eine Importvorlage fuer den Massenimport bereit. |
| Excel Erweiterte Texte exportieren | Exportiert markierte Zuordnungen in Excel. |
| Excel-Vorlage importieren | Importiert Texte aus Excel. |
| Alte erweiterte Texte loeschen | Entfernt Legacy-Daten. |
| Alle Belegtexte aktualisieren | Startet eine Hintergrundaktualisierung aller Belegtexte. |
| Benachrichtigungen in allen Belegen aktualisieren | Prueft, ob geaenderte Vorlagen in vorhandenen Belegen als aktualisierungsrelevant markiert werden muessen. |

## Taegliche Arbeit in Belegen
### Grundprinzip in Verkaufs-, Einkaufs-, Umlagerungs- und Produktionsbelegen
Direkt in den Fachbelegen erweitert das Modul die Standardseiten um zwei Arten von Bedienung:

1. zusaetzliche Felder fuer **Drucktyp** und bei Berichten den **Nebendrucktyp**,
2. Text-FactBoxen fuer Kopf- und Zeilenebene sowie teils eine Aktion **Erweiterter Text**.

Die Felder folgen immer demselben Muster:

| Feld | Erlaeuterung |
| --- | --- |
| Drucktyp | Steuert, ob der Zusatztext als InfoBox, Bericht oder Mail verwendet wird. |
| Nebendrucktyp | Nur bei Drucktyp Bericht sichtbar. Steuert die Position des Berichtstexts: Kopfzeile, Fusszeile, Vor Position oder Nach Position. |

In offenen Belegen wird zusaetzlich meist eine Aktion **Erweiterter Text** angeboten. Damit oeffnen Sie die Vorschauliste des jeweiligen Belegbereichs und sehen, fuer welche Belegart und welche Folgebelege Texte erzeugt werden.

### Verkauf
Auf Verkaufsbelegen nutzt das Modul die Erweiterung unter anderem in Verkaufsgutschriften und Rahmenauftraegen. Zusaetzlich sind viele weitere Verkaufsseiten laut Objektinventar erweitert, insbesondere fuer Auftraege, Rechnungen, Lieferungen, Archive und Ruecksendungen.

Typischer Ablauf im Verkauf:

1. Oeffnen Sie den Verkaufsbeleg.
2. Pruefen Sie im Kopf den **Drucktyp**.
3. Falls der Text im Bericht erscheinen soll, waehlen Sie den **Nebendrucktyp**.
4. Oeffnen Sie **Erweiterter Text**, wenn Sie die kombinierte Belegvorschau brauchen.
5. Kontrollieren Sie in den Kopf- und Zeilen-FactBoxen, welche Texte aktuell aktiv sind.
6. Nutzen Sie **E-Mail**, wenn der Versand direkt aus dem Beleg erfolgen soll.

Wichtige Verkaufsoberflaechen:

| BC-Oberflaeche | Erlaeuterung |
| --- | --- |
| Verkaufsgutschrift | Offener Verkaufsbeleg mit Feldern fuer Drucktyp und Nebendrucktyp, Aktion **Erweiterter Text** sowie Aktion **E-Mail**. |
| Verkaufsrahmenauftrag | Nutzt dieselbe Logik fuer Textanzeige, Folgebelege und Mailversand. |
| Gebuchte Verkaufsrechnung | Bietet einen Aktionsblock **Erweiterter Text** mit Umschaltung zwischen InfoBox, Bericht und Mail. |
| Gebuchte Verkaufslieferung | Bietet **E-Mail** und die Umschaltung der Textausgabe fuer bereits gebuchte Daten. |
| Gebuchte Verkaufsgutschrift | Bietet dieselbe Umschaltlogik fuer InfoBox, Bericht, Kopfzeile, Fusszeile, Vor Position, Nach Position und Mail. |
| Verkaufsarchivseiten | Anzeigen und Archivversionen koennen die archivierten Textstaende ueber spezielle Archiv-FactBoxen zeigen. |

### Einkauf
Im Einkauf ist das Muster weitgehend identisch. Das Modul erweitert offene und gebuchte Einkaufsbelege sowie Archivseiten.

Typischer Ablauf im Einkauf:

1. Oeffnen Sie Bestellung, Rahmenbestellung, Rechnung oder Gutschrift.
2. Setzen Sie Drucktyp und bei Bedarf den Nebendrucktyp.
3. Oeffnen Sie **Erweiterter Text**, um die Vorschau fuer den Beleg zu erzeugen oder zu pruefen.
4. Kontrollieren Sie Kopf- und Zeilentexte in den FactBoxen.
5. Nutzen Sie auf gebuchten Belegen oder Eingangsbelegen die Aktion **E-Mail**, wenn Dokumente mit Mailtext versendet werden sollen.

Wichtige Einkaufsoberflaechen:

| BC-Oberflaeche | Erlaeuterung |
| --- | --- |
| Einkaufsrahmenbestellung | Erweiterte Felder, Textvorschau und Mailversand. |
| Gebuchte Einkaufsrechnung | Aktionsgruppe **Erweiterter Text** zum Wechsel der Ausgabeart. |
| Gebuchte Einkaufslieferung | Anzeige der erzeugten Kopf- und Zeilentexte in FactBoxen. |
| Einkaufsarchivseiten | Archivierte Texte fuer historische Stände ueber Archiv-FactBoxen. |

### Umlagerung und Lager
Das Modul deckt auch Umlagerungsauftraege, Lagerbelege und gebuchte Lagerbelege ab.

| BC-Oberflaeche | Erlaeuterung |
| --- | --- |
| Umlagerungsauftrag | Erweiterte Texte auf Kopf und Zeile sowie Vorschau auf Folgebelege **Gebuchte Umlagerungslieferung** und **Gebuchte Umlagerungsannahme**. |
| Wareneingang Lager | FactBoxen fuer Kopf- und Zeilentexte im Lagerbeleg. |
| Gebuchter Lagerwareneingang | Anzeige bereits gebuchter Texte einschliesslich Drucktyp und Nebendrucktyp. |
| Gebuchter Lagerwarenausgang | Anzeige bereits gebuchter Texte einschliesslich Drucktyp und Nebendrucktyp. |

Die Lagerseiten sind besonders wichtig, wenn Textinformationen mit physischen Warenbewegungen zusammenlaufen, zum Beispiel bei begleitenden Hinweisen fuer den Wareneingang oder Versand.

### Produktion und Arbeitsplaene
In der Produktion verknuepft das Modul Arbeitsplantexte, Produktionsauftragsstatus und Folgebelege.

| BC-Oberflaeche | Erlaeuterung |
| --- | --- |
| Fertigungsauftrag fertig | Kopf- und Zeilentexte fuer den Status **Fertig**. |
| Produktionsauftrags-Arbeitsplan | Text-FactBox fuer Arbeitsgangtexte an der Routing-Zeile. |
| Produktion Erweiterter Text | Vorschauseite fuer Produktionsauftraege und Folgezustände wie Simuliert, Geplant, Fest geplant, Freigegeben und Fertig. |

Das Modul erzeugt laut Logik nicht nur den Text fuer den aktuellen Status. Bei bestimmten Ausgangsbelegen werden auch Folgebelege bzw. Folgestaende vorbereitet, zum Beispiel von **Freigegeben** nach **Fertig** oder von Verkaufs- und Einkaufsbelegen in gebuchte Stufen.

## Vorschau, Import und Massenpflege
### Belegvorschau fuer offene Dokumente
Die Seiten **Verkaufsbelege Erweiterter Text**, **Einkaufsbelege erweiterter Text**, **Dokumente uebertragen Erweiterter Text** und **Produktion Erweiterter Text** sind keine normale Stammdatenpflege, sondern Arbeitsseiten fuer die Textvorschau.

Je Seite sehen Sie mindestens:

| Feld | Erlaeuterung |
| --- | --- |
| Belegart | Zeigt, fuer welche Stufe der Text gerade angezeigt wird. |
| Nr. | Dokumentnummer. |
| Zeilennr. | In den Unterseiten die konkrete Belegzeile. |

Diese Vorschauseiten erzeugen je nach Ausgangsbeleg nicht nur den aktuellen Text, sondern auch Texte fuer Folgedokumente. Beispiele aus der Programmlogik:

| Ausgangsbeleg | Miterzeugte Folgestufen |
| --- | --- |
| Verkaufsauftrag | Gebuchte Verkaufsrechnung, gebuchte Verkaufslieferung, produktionsnahe Folgestufen und Lagerausgang, soweit die Logik greift. |
| Verkaufsgutschrift | Gebuchte Verkaufsgutschrift. |
| Einkaufsbestellung | Gebuchte Einkaufsrechnung, gebuchte Ruecklieferung, Lagerwareneingang. |
| Umlagerungsauftrag | Gebuchte Umlagerungslieferung und gebuchte Umlagerungsannahme. |
| Produktionsauftrag | Je nach Status weitere Produktionsstatus. |

Nutzen Sie die Aktion **Erweiterte Texte fuer Belege erstellen**, wenn Sie die Texte neu aufbauen oder aktualisieren wollen.

### Import/Export fuer Arbeitsplaene
Die Seite **Erweiterte Texte Import/Export - Routings** dient dem Massenimport und der Massenverarbeitung fuer Arbeitsplantexte.

| Feld | Erlaeuterung |
| --- | --- |
| Processed | Kennzeichnet bereits verarbeitete Zeilen. |
| Routing No. | Arbeitsplannummer. |
| Version Code | Versionscode des Arbeitsplans. |
| Operation No. | Vorgangsnummer. |
| Language Code | Sprache der importierten Texte. |
| Has Text Factbox | Zeigt, ob ein InfoBox-Text vorhanden ist. |
| Has Text Report | Zeigt, ob ein Berichtstext vorhanden ist. |
| Has Text Mail | Zeigt, ob ein Mailtext vorhanden ist. |
| Has Report Text Header | Zeigt Kopfzeilentexte fuer Berichte. |
| Has Report Text Footer | Zeigt Fusszeilentexte fuer Berichte. |
| Has Report Text Before | Zeigt Texte vor Position. |
| Has Report Text After | Zeigt Texte nach Position. |

Wichtige Aktionen:

| Aktion | Erlaeuterung |
| --- | --- |
| Ausgewählte Daten verarbeiten | Verarbeitet nur markierte Zeilen. |
| Alle Daten verarbeiten | Verarbeitet den gesamten Puffer. |
| Verarbeitete entfernen - Auswahl | Loescht den Verarbeitungskennzeichen fuer markierte Zeilen. |
| Verarbeitete entfernen - Alle | Bereinigt alle verarbeiteten Eintraege. |
| Excel-Vorlage exportieren | Stellt eine Importvorlage bereit. |
| Excel-Daten exportieren | Exportiert Arbeitsplandaten. |
| Excel-Daten importieren | Importiert Arbeitsplantexte. |

### Import/Export fuer Belege
Die Seite **Erweiterte Texte Import/Export - Documents** arbeitet nach demselben Prinzip fuer offene Belege.

| Feld | Erlaeuterung |
| --- | --- |
| Processed | Kennzeichnet verarbeitete Pufferzeilen. |
| Table ID | Quelltabelle des Belegs oder der Zeile. |
| Table Name | Anzeigename der Quelltabelle. |
| Source Document Type | Ausgangsbelegart. |
| No. | Belegnummer. |
| Line No. | Zeilennummer. |
| Has Text Factbox | InfoBox-Text vorhanden. |
| Has Text Report | Berichtstext vorhanden. |
| Has Text Mail | Mailtext vorhanden. |
| Has Report Text Header | Kopfzeilentext vorhanden. |
| Has Report Text Footer | Fusszeilentext vorhanden. |
| Has Report Text Before | Text vor Position vorhanden. |
| Has Report Text After | Text nach Position vorhanden. |

Das Feld **Overwrite Ext. Text** entscheidet dabei, ob bestehende Texte bei der Verarbeitung ueberschrieben werden.

## Mail und Berichtsausgabe
### Drucktyp und Nebendrucktyp fachlich nutzen
Der Drucktyp bestimmt, wo der Anwender den Text erwartet:

| Wert | Nutzung |
| --- | --- |
| InfoBox | Text erscheint in der eingeblendeten FactBox am Beleg. |
| Bericht | Text wird fuer den Druck bzw. die Berichtsausgabe vorbereitet. |
| Mail | Text wird fuer den Mailtext genutzt. |
| Mail Subject | Text wird fuer die Mailbetrefflogik genutzt. |

Der Nebendrucktyp ist nur bei **Bericht** relevant:

| Wert | Nutzung |
| --- | --- |
| leer | Standardposition fuer Berichtstext. |
| Kopfzeile | Text erscheint im Kopfbereich. |
| Fusszeile | Text erscheint im Fussbereich. |
| Vor Position | Text wird vor der Belegzeile ausgegeben. |
| Nach Position | Text wird nach der Belegzeile ausgegeben. |

### Gebuchte Belege nachtraeglich umstellen
Auf gebuchten Verkaufs-, Einkaufs-, Umlagerungs- und Lagerbelegen stehen Aktionsgruppen zur Verfuegung, mit denen Sie die Ausgabeart nachtraeglich aendern koennen. Typische Optionen sind:

1. InfoBox
2. Bericht Standard
3. Bericht Kopfzeile
4. Bericht Fusszeile
5. Bericht Vor Position
6. Bericht Nach Position
7. Mail

Das ist besonders hilfreich, wenn ein Beleg bereits gebucht ist, der Zusatztext aber fachlich anders dargestellt werden soll.

### E-Mail-Versand
Auf offenen und gebuchten Belegen ist an mehreren Stellen eine Aktion **E-Mail** vorhanden. Die Programmlogik ruft dabei den Standard-Mailversand fuer die markierten Datensaetze auf. Voraussetzung ist, dass die Mailtexte, Mailbetreffe und Platzhalter in den Vorlagen und Einstellungen vorbereitet sind.

## Historie, Archiv und Nachverfolgung
Das Modul fuehrt keine eigene allgemeine Historienliste fuer Anwender, stellt aber mehrere historische Oberflaechen bereit:

| Bereich | Nachverfolgung |
| --- | --- |
| Belegarchive Verkauf und Einkauf | Archiv-FactBoxen zeigen archivierte Kopf- und Zeilentexte pro Version und Vorkommnis. |
| Gebuchte Belege | Die gebuchten Text-FactBoxen zeigen den tatsaechlich uebernommenen Textstand. |
| Hintergrundaktualisierung | Ueber die Aktionen zum Aktualisieren aller Belegtexte bzw. Benachrichtigungen lassen sich geaenderte Vorlagen systemweit nachziehen. |
| Import/Export-Puffer | Felder wie **Processed** zeigen den Bearbeitungsstand fuer Massenverarbeitung. |

## FAQ und Troubleshooting
### Warum erscheint im Beleg kein Text?
Pruefen Sie zuerst die Zuordnung im **Arbeitsblatt erweiterte Textzuordnung**. Ohne passende Kombination aus Vorlage, Typ, Typnummer und gegebenenfalls Subtyp wird kein Text gezogen.

### Warum erscheint der Text nur in der InfoBox, aber nicht im Bericht?
Pruefen Sie in der Vorlage den **Drucktyp**. Fuer Berichtsausgaben muss der Drucktyp **Bericht** sein. Falls die Position im Druck nicht stimmt, pruefen Sie auch den **Nebendrucktyp**.

### Warum sehe ich auf einem gebuchten Beleg noch den alten Text?
Gebuchte Belege halten den uebernommenen Stand. Wenn Aenderungen nachgezogen werden sollen, pruefen Sie die Funktionen zur Aktualisierung aller Belegtexte bzw. die Umstellung der Ausgabeart auf dem gebuchten Beleg.

### Warum wird der Mailtext nicht wie erwartet gefuellt?
Pruefen Sie in den **Erweiterten Texteinstellungen** die Felder **Email Placeholders** und **Preferred Email Text**. Kontrollieren Sie anschliessend die verwendeten Platzhalter in der Vorlage.

### Warum ist der Nebendrucktyp nicht sichtbar?
Der Nebendrucktyp wird nur gezeigt, wenn der Drucktyp **Bericht** ist.

### Warum kann ich einen Prozess nicht auswaehlen?
Prozessgruppe und Prozess werden nach Ausgabeart gefiltert. Wenn Vorlage oder Zuordnung auf **Mail** stehen, werden keine reinen **Bericht**-Prozesse angeboten.

## Typische Anwendungsfaelle
### Verkaufsbeleg mit Zusatztext und Mailversand
**Ausloeser:** Ein Sachbearbeiter erstellt eine Verkaufsgutschrift und moechte den Hinweistext fuer den Kunden im Dokument und in der E-Mail mitgeben.

**Einstieg in BC:** Ueber **Tell Me** oder direkt ueber die Belegliste die **Verkaufsgutschrift** oeffnen.

**Kernablauf:**
1. Im Beleg den **Drucktyp** auf die gewuenschte Ausgabeart setzen.
2. Falls der Text im Bericht vor oder nach der Position erscheinen soll, den **Nebendrucktyp** auswaehlen.
3. Ueber **Erweiterter Text** die Vorschau in **Verkaufsbelege Erweiterter Text** oeffnen.
4. In der Kopf- und Zeilen-FactBox pruefen, ob die richtige Vorlage gezogen wurde.
5. Ueber **E-Mail** den Versand starten.

**Abschluss:** In gebuchten Belegen kann spaeter geprueft werden, welcher Textstand tatsaechlich uebernommen wurde.

### Neue Vorlage fuer einen Debitor und einen Artikelbereich bereitstellen
**Ausloeser:** Der Vertrieb benoetigt einen standardisierten Zusatztext fuer eine bestimmte Debitorengruppe und eine bestimmte Artikelkategorie.

**Einstieg in BC:** **Erweiterte Textvorlagen** und danach **Arbeitsblatt erweiterte Textzuordnung**.

**Kernablauf:**
1. In **Erweiterte Textvorlagen** eine neue Vorlage anlegen.
2. Drucktyp und bei Bedarf Nebendrucktyp festlegen.
3. Textinhalt in der Vorlagen-FactBox pflegen.
4. In **Arbeitsblatt erweiterte Textzuordnung** die Vorlage auswaehlen.
5. Bei **Typ** die gewuenschte Debitor- oder Gruppenzuordnung festlegen.
6. Bei **Subtyp** zum Beispiel **Artikelkategorie** oder **Artikel** auswaehlen.
7. Danach im Testbeleg pruefen, ob die Zuordnung greift.

**Abschluss:** Falls der Text mehrsprachig benoetigt wird, direkt die Uebersetzungen pflegen.

### Arbeitsplantexte per Excel importieren
**Ausloeser:** Die Fertigungsplanung erhaelt viele neue Arbeitsplanhinweise aus einer externen Datei.

**Einstieg in BC:** **Erweiterte Texte Import/Export - Routings**.

**Kernablauf:**
1. Zunaechst die **Excel-Vorlage exportieren**.
2. Daten in der Vorlage vorbereiten.
3. Ueber **Excel-Daten importieren** die Datei einlesen.
4. In der Pufferliste pruefen, welche Zeilen bereits Texte fuer InfoBox, Bericht oder Mail enthalten.
5. Mit **Ausgewaehlte Daten verarbeiten** oder **Alle Daten verarbeiten** die Texte in das System uebernehmen.

**Abschluss:** Ueber den Verarbeitungsstatus und die Arbeitsplan-FactBox kontrollieren, ob die Texte angekommen sind.

### Belegtexte systemweit nach Aenderung einer Vorlage aktualisieren
**Ausloeser:** Ein bestehender Hinweistext wurde geaendert und soll moeglichst breit nachgezogen werden.

**Einstieg in BC:** **Arbeitsblatt erweiterte Textzuordnung**.

**Kernablauf:**
1. Die betroffene Vorlage und Zuordnung pruefen.
2. Je nach Bedarf **Alle Belegtexte aktualisieren** oder **Benachrichtigungen in allen Belegen aktualisieren** starten.
3. Die Hintergrundverarbeitung abwarten.
4. Stichprobenartig offene Belege, gebuchte Belege und Archivseiten pruefen.

**Abschluss:** Falls manuell geaenderte Texte in Belegen nicht ueberschrieben werden sollen, die fachliche Wirkung vor dem Massenlauf abstimmen.
