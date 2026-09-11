---
title: m+m EDI mit Logistikmanagement
---

# m+m EDI mit Logistikmanagement

## Einleitung

Das Modul erweitert die bestehende Versandplanung in Microsoft Dynamics 365 Business Central um EDI-bezogene Informationen für Automotive-Vorgänge. Anwender arbeiten weiterhin in den bekannten Seiten der Versandplanung, sehen dort jedoch zusätzliche Kennzeichen für Automotive-Fälle und eine reservierte Versandnummer.

Die Zielgruppe sind Key User in Logistik, Versand und Auftragsabwicklung, die Versandplanungen anlegen, Auftragszeilen zuordnen, die weitere Lagerabwicklung vorbereiten und registrierte Versandplanungen nachverfolgen. Das Modul verändert keinen eigenen, vollständig getrennten Prozess, sondern ergänzt den vorhandenen Ablauf an den Stellen, an denen eine Versandplanung aus EDI-/Automotive-Sicht besonders gekennzeichnet werden muss.

Der typische Ablauf ist kurz gesagt wie folgt:

1. Voraussetzungen in der Versandplanung und den Filtervorlagen einrichten.
2. Auftrags- oder Reklamationszeilen in der Zuordnungsseite filtern und auswählen.
3. Versandplanung anlegen oder ergänzen.
4. Automotive-Zeilen in der Versandplanung prüfen.
5. Weitere Logistikschritte wie Warenausgang, Kommissionierung oder direkte Lieferung ausführen.
6. Versandplanung registrieren und später in den registrierten Versandplanungen erneut aufrufen.

## Schnellstart für Anwender

### Automotive-Versandplanung in wenigen Schritten

1. Öffnen Sie über **Suchen** die Seite **Versandplanung**.
2. Legen Sie einen neuen Vorgang an oder öffnen Sie eine vorhandene Versandplanung.
3. Rufen Sie die Zeilen auf und übernehmen Sie die gewünschten Belegzeilen in die Planung.
4. Prüfen Sie in den Zeilen das Feld **Automotive**. Nur für solche Zeilen wird eine reservierte Versandnummer vorgesehen.
5. Achten Sie darauf, dass die Zeile aus einem Verkaufsbeleg stammt, ein Debitor als Lieferempfänger eingetragen ist und noch keine tatsächliche Versandnummer vorhanden ist.
6. Ergänzen Sie die Versanddaten wie Tour, Versanddatum, Ladestelle und Mengen für die Zuweisung.
7. Geben Sie die Versandplanung frei.
8. Führen Sie anschließend den passenden Folgeprozess aus:
   - direkte Lieferung für Zeilen ohne Lagerprozess,
   - Warenausgang,
   - Kommissionierung,
   - oder Warenausgang mit Kommissionierung.
9. Registrieren Sie die Versandplanung, damit der Vorgang in den **Registrierten Versandplanungen** nachvollziehbar bleibt.

### Woran Sie einen EDI-/Automotive-Fall erkennen

Ein EDI-relevanter Vorgang ist in dieser Erweiterung an drei Stellen sichtbar:

- Im Kopf der Versandplanung über **Automotive vorhanden**.
- In der Zuordnungs- und Bestandskontrollseite über den Filter **Automotive**.
- In den Versandplanungszeilen über **Automotive** und **Reservierte Versandnummer**.

## Einrichtung

### Versandplanung einrichten

Die eigentliche Grundeinrichtung erfolgt weiterhin in der bestehenden Versandplanungseinrichtung des Basismoduls. Diese Seite steuert, ob Versandplanungen aktiv sind, welche Nummernserien verwendet werden und welche Standardwerte für Berichte oder Mengen vorbelegt werden.

Öffnen Sie über **Suchen** die Einrichtung der Versandplanung und prüfen Sie insbesondere die Nummerierung und die Standardvorgaben für den weiteren Prozess. Ohne diese Basisdaten kann die Versandplanung zwar geöffnet werden, der operative Ablauf bleibt jedoch unvollständig.

| Einrichtung | Erläuterung |
| --- | --- |
| Primärschlüssel | Technischer Hauptschlüssel des Einrichtungsdatensatzes. |
| Versandplanung aktivieren | Legt fest, ob die Versandplanung im Unternehmen verwendet wird. |
| Versandplanungsnummern | Nummernserie für neue Versandplanungen. |
| Registrierte Versandplanungsnummern | Nummernserie für registrierte Versandplanungen. |
| Vorgabeart für Transportbestellzeile | Steuert, ob für Transportbestellzeilen ein Sachkonto oder ein Zu-/Abschlag verwendet wird. |
| Vorgabenummer für Transportbestellzeile | Hinterlegt die konkrete Nummer passend zur gewählten Vorgabeart. |
| Inkrement Ladesequenznr. um | Bestimmt die automatische Schrittweite für die Ladereihenfolge. |
| Inkrement Versandreihenfolgenr. um | Bestimmt die automatische Schrittweite für die Versandreihenfolge. |
| Berichts-ID Versandplanung | Report für den Ausdruck der offenen Versandplanung. |
| Report registrierte Versandplanung | Report für den Ausdruck der registrierten Versandplanung. |
| Standardwert Menge für Zuweisung | Legt fest, ob standardmäßig die Restmenge oder die Fertigmenge für die Zuweisung verwendet wird. |
| Datumsfilter Versandplanungszuordnung und Bestandskontrolle | Steuert den Standard-Datumsfilter in der Zuordnungsseite. |
| Registrierung ohne Menge für Zuweisung zulassen | Erlaubt die Registrierung auch dann, wenn noch keine Zuweisungsmenge eingetragen ist. |

### Benutzerfiltervorlagen pflegen

Die Erweiterung ergänzt die Seite **Benutzerfiltervorlage Karte** um ein weiteres Kriterium für Automotive-Fälle. Diese Filtervorlagen sind in der Praxis wichtig, weil Anwender damit die Zuordnungsseite schneller auf die tatsächlich zu bearbeitenden Belege eingrenzen.

Pflegen Sie pro Benutzer oder Arbeitsbereich passende Vorlagen. Für EDI-/Automotive-Fälle empfiehlt sich mindestens eine eigene Vorlage, damit entsprechende Belege direkt sichtbar sind.

| Einrichtung | Erläuterung |
| --- | --- |
| Typ | Bestimmt, ob die Vorlage für Ladestellenkalendereinträge oder für die Versandplanung verwendet wird. |
| Benutzer-ID | Ordnet die Vorlage einem Benutzer zu. |
| Code | Kennung der Filtervorlage. |
| Standardfilter | Kennzeichnet die Vorlage als Standard für den Benutzer. |
| Gruppieren nach | Steuert, wie die Treffer in der Zuordnungsansicht zusammengefasst werden. Zulässige Werte sind Auftrag, Lieferadresse, Versanddatum, Artikelkategorie, Gewünschtes Lieferdatum, Zugesagtes Lieferdatum, Geplantes Lieferdatum und Geplantes Versanddatum. |
| Datumsformel | Hinterlegt einen relativen Zeitraum für die Vorauswahl. |
| Lagerortfilter | Begrenzt die Anzeige auf bestimmte Lagerorte. |
| Debitorenfilter | Begrenzt die Anzeige auf bestimmte Debitoren. |
| Versandtourfilter | Begrenzt die Anzeige auf bestimmte Touren. |
| Postleitzahlenfilter | Filtert nach Postleitzahl des Empfängers. |
| Länder-/Regionsfilter | Filtert nach Land oder Region des Empfängers. |
| Mengenfilter | Unterstützt die Auswahl nach Mengenstatus; verfügbar ist insbesondere Menge für Versandplanung > 0. |
| Verkaufsauftragsfilter | Grenzt die Anzeige auf bestimmte Verkaufsaufträge ein. |
| Einkaufsreklamationsfilter | Grenzt die Anzeige auf bestimmte Einkaufsreklamationen ein. |
| Artikelkategorienfilter | Filtert nach Artikelkategorie. |
| Ladestellenfilter | Filtert nach Ladestelle. |
| Lagerortfilter 2 | Zusätzlicher Lagerortfilter für erweiterte Vorauswahl. |
| Gesperrte Ladestellen einbeziehen | Bezieht auch gesperrte Ladestellen in die Trefferliste ein. |
| Nur ungenutzte Kapazitäten anzeigen | Zeigt nur freie Kapazitäten an. |
| Datumsformel 2 | Zweiter relativer Zeitraum für Zusatzfilter. |
| Offene Avisierungen anzeigen | Bezieht offene Avisierungen in die Sicht ein. |
| Einkaufsbestellzeilen anzeigen | Nimmt Einkaufsbestellzeilen in die Trefferliste auf. |
| Kreditorenfilter | Filtert nach Kreditoren. |
| Automotive | Kennzeichnet, ob nur Automotive-Fälle, keine Automotive-Fälle oder alle Fälle angezeigt werden. |

## Stammdaten und Filterlogik

### Automotive-Kennzeichnung in der Versandplanung

Die Erweiterung führt keine eigene Stammdatenseite ein. Der fachliche Kern liegt in zusätzlichen Feldern, die in vorhandene Versandplanungsdaten eingeblendet werden.

Im Kopf der Versandplanung wird **Automotive vorhanden** angezeigt. Das Feld ist eine reine Kennzeichnung. Es wird automatisch gesetzt, sobald mindestens eine Zeile der Versandplanung als Automotive markiert ist. Anwender pflegen dieses Feld nicht direkt.

In den Zeilen und in der Zuordnungsseite steht das Feld **Automotive** zur Verfügung. Es dient dazu, Automotive-Vorgänge sofort zu erkennen und gezielt zu filtern.

### Reservierte Versandnummer verstehen

Zusätzlich wird in den Versandplanungszeilen die **Reservierte Versandnummer** angezeigt. Dieses Feld ist nicht editierbar. Es wird nur dann gefüllt, wenn alle fachlichen Voraussetzungen erfüllt sind:

1. Die Zeile ist als **Automotive** gekennzeichnet.
2. Die Herkunft ist eine Verkaufszeile.
3. Der Lieferempfänger ist ein Debitor.
4. Es existiert noch keine echte Versandnummer.
5. Für vergleichbare Zeilen derselben Versandplanung ist noch keine tatsächliche Versandnummer verbraucht, aber eventuell bereits eine reservierte Nummer vorhanden.

Wenn bereits eine passende reservierte Versandnummer in vergleichbaren Zeilen gefunden wird, verwendet das System dieselbe Nummer erneut. Andernfalls wird die nächste Nummer aus der Versandnummernserie des zugehörigen Verkaufsauftrags reserviert.

## Profile und Zuordnungen

### Arbeiten mit der Zuordnungs- und Bestandskontrolle

Die Seite **Versandplanungszuordnung und Bestandskontrolle** ist der zentrale Einstieg, wenn Sie Zeilen für eine Versandplanung sammeln und vorselektieren möchten. Die Erweiterung fügt hier ein zusätzliches Filterfeld **Automotive** ein. Dadurch lassen sich EDI-relevante Zeilen gezielt ausblenden oder hervorheben.

Typischer Ablauf:

1. Öffnen Sie die Zuordnungsseite aus der Versandplanung heraus.
2. Setzen Sie die gewünschten Filter, insbesondere Datum, Lagerort, Debitor und bei Bedarf **Automotive**.
3. Prüfen Sie die Trefferliste im unteren Bereich.
4. Markieren Sie die gewünschten Zeilen.
5. Übernehmen Sie die markierten Zeilen in die Versandplanung.

| Feld | Erläuterung |
| --- | --- |
| Gruppierungsname | Zeigt die aktuelle Gruppierung der Treffer an. |
| Ausgewählt | Kennzeichnet, ob die Zeile für die Übernahme markiert ist. |
| Herkunftsnr. | Nummer des Ursprungsbelegs. |
| Artikelnr. | Artikel der zuzuordnenden Zeile. |
| Variantencode | Variante des Artikels. |
| Artikelkategoriecode | Artikelkategorie des Artikels. |
| Lagerortcode | Lagerort der Zeile. |
| Beschreibung | Beschreibung aus dem Ursprungsbeleg. |
| Beschreibung 2 | Zweite Beschreibung aus dem Ursprungsbeleg. |
| Menge | Ursprüngliche Belegmenge. |
| Restmenge | Noch offene Menge. |
| Einheitencode | Mengeneinheit der Zeile. |
| Artikelreferenznr. | Zusätzliche Referenz zum Artikel. |
| Bruttogewicht | Bruttogewicht der Zeile. |
| Nettogewicht | Nettogewicht der Zeile. |
| Versanddatum | Versanddatum des Ursprungsbelegs. |
| Geplantes Lieferdatum | Termin aus der Lieferplanung. |
| Geplantes Versanddatum | Geplanter Versandtermin. |
| Gewünschtes Lieferdatum | Vom Kunden gewünschter Liefertermin. |
| Zugesagtes Lieferdatum | Bestätigter Liefertermin. |
| Versandtourcode | Zugeordnete Versandtour. |
| Liefernach Typ | Typ des Empfängers; üblich sind Debitor oder Lagerort. |
| Liefernach Nr. | Nummer des Empfängers. |
| Name Lieferempfänger | Name des Empfängers. |
| Name 2 Lieferempfänger | Zusatzname des Empfängers. |
| Adresse Lieferempfänger | Adresse des Empfängers. |
| Adresse 2 Lieferempfänger | Zweite Adresszeile. |
| Ort Lieferempfänger | Ort des Empfängers. |
| Postleitzahl Lieferempfänger | Postleitzahl des Empfängers. |
| Länder-/Regionscode Lieferempfänger | Land oder Region des Empfängers. |
| Lagerprozess | Zeigt, ob kein Lagerprozess, Warenausgang, Kommissionierung oder Warenausgang und Kommissionierung vorgesehen sind. |
| Warenausgang erstellt | Kennzeichnet bereits erzeugte Warenausgänge. |
| Warenausgangsnummer | Nummer des zugehörigen Warenausgangs. |
| Warenausgangszeilennr. | Zeilennummer im Warenausgang. |
| Kommissionierung erstellt | Kennzeichnet bereits erzeugte Kommissionierungen. |
| Kommissioniernummer | Nummer der Kommissionierung. |
| Kommissionierzeilennr. | Zeilennummer in der Kommissionierung. |
| Fertigungsauftrag erstellt | Kennzeichnet einen bereits angelegten Fertigungsauftrag. |
| Fertigungsauftragsstatus | Zeigt den Status des Fertigungsauftrags. |
| Fertigungsauftragsnr. | Nummer des Fertigungsauftrags. |
| Fertigmenge | Bereits fertiggestellte Menge. |
| Menge für Versandplanung | Menge, die für die Versandplanung herangezogen werden kann. |
| Versandartencode | Versandart der Zeile. |
| Lagergruppe | Zusätzliche logistische Gruppierung. |
| Automotive | Kennzeichnet den Automotive-Fall in der Trefferliste. |

## Tägliche Arbeit in der Versandplanung

### Versandplanungskopf bearbeiten

Der Kopf der **Versandplanung** bündelt Status, Tour- und Fahrzeugdaten sowie Kennzahlen zum Fortschritt. Anwender starten hier, sobald die Zeilen einer Planung zusammengefasst werden sollen.

Arbeiten Sie in dieser Reihenfolge:

1. Öffnen oder erstellen Sie die Versandplanung.
2. Prüfen Sie zunächst Status und Datumsfelder.
3. Hinterlegen Sie Tour, Fahrzeug, Fahrer und Ladestelle.
4. Kontrollieren Sie, ob **Automotive vorhanden** gesetzt ist.
5. Wechseln Sie erst danach in die Zeilen, um Mengen, Termine und Folgeprozesse zu prüfen.

| Feld | Erläuterung |
| --- | --- |
| Nr. | Nummer der Versandplanung. |
| Status | Zeigt den Bearbeitungsstatus. Zulässige Werte sind Offen und Freigegeben. |
| Belegdatum | Dokumentdatum der Versandplanung. |
| Buchungsdatum | Datum für die weitere Verarbeitung. |
| Anzahl Gesamtzeilen | Zeigt die Gesamtzahl aller Zeilen. |
| Anzahl offene Zeilen | Zeigt die noch offenen Zeilen. |
| Anzahl offene Zeilen in Warenausgang | Anzahl Zeilen, die im Warenausgang noch offen sind. |
| Anzahl beendete Zeilen in Warenausgang | Anzahl Zeilen mit abgeschlossenem Warenausgang. |
| Anzahl offene Zeilen in Kommissionierung | Anzahl Zeilen, die sich noch in der Kommissionierung befinden. |
| Anzahl beendete Zeilen in Kommissionierung | Anzahl Zeilen mit abgeschlossener Kommissionierung. |
| Anzahl beendete Zeilen | Anzahl vollständig erledigter Zeilen. |
| Versandtourcode | Tour, auf der die Auslieferung erfolgen soll. |
| Interne Logistik | Kennzeichnet die Tour als internen Logistikvorgang. |
| Einkaufsreklamationen anzeigen | Bezieht Einkaufsreklamationen in die Planung mit ein. |
| Versandplanungsdatum | Datum der Planung. |
| Kreditorennr. | Kreditor, falls ein kreditorischer Zusammenhang besteht. |
| Einkaufsbelegnr. | Referenz auf einen Einkaufsbeleg. |
| Versandfahrzeugcode | Fahrzeug der Lieferung. |
| Kennzeichen | Freies Fahrzeugkennzeichen. |
| Mitarbeiternr. interner Fahrer | Interner Fahrer. |
| Kontaktnr. externer Fahrer | Externer Fahrer. |
| Ladestellen-Lagerortcode | Lagerort der Ladestelle. |
| Ladestelle | Zu verwendende Ladestelle. |
| Ladestellen-Kapazitätseinheitencode | Kapazitätseinheit der Ladestelle. |
| Automotive vorhanden | Kennzeichnet, dass mindestens eine Automotive-Zeile enthalten ist. |

### Versandplanungszeilen prüfen und ergänzen

Die Seite **Zeilen** ist der wichtigste Arbeitsbereich im Tagesgeschäft. Hier sehen Sie Herkunftsbeleg, Empfänger, Artikel, Mengen, Termine und den Fortschritt der Lagerabwicklung. Die Erweiterung ergänzt diese Zeilen um die Felder **Automotive** und **Reservierte Versandnummer**.

Für Automotive-Fälle empfiehlt sich die folgende Arbeitsreihenfolge:

1. Prüfen Sie Lieferempfänger, Herkunftsbeleg und Artikel.
2. Tragen Sie die **Menge für Zuweisung** ein.
3. Kontrollieren Sie Versand- und Liefertermine.
4. Ergänzen Sie Ladestelle, Ladezeit und Planungsstatus.
5. Prüfen Sie das Feld **Automotive**.
6. Lesen Sie die **Reservierte Versandnummer** nur als Ergebnis der Systemlogik; das Feld ist nicht manuell pflegbar.
7. Geben Sie die Versandplanung frei, bevor Sie Folgebelege anstoßen.

| Feld | Erläuterung |
| --- | --- |
| Ladereihenfolgenr. | Reihenfolge der Beladung innerhalb der Tour. |
| Versandreihenfolgenr. | Reihenfolge der Auslieferung. |
| Liefernach Typ | Typ des Empfängers; möglich sind leer, Debitor, Lagerort oder Kreditor. |
| Liefernach Nr. | Nummer des Empfängers. |
| Name Lieferempfänger | Name des Empfängers. |
| Name 2 Lieferempfänger | Zusatzname des Empfängers. |
| Adresse Lieferempfänger | Lieferadresse. |
| Adresse 2 Lieferempfänger | Zweite Zeile der Lieferadresse. |
| Ort Lieferempfänger | Ort des Empfängers. |
| Postleitzahl Lieferempfänger | Postleitzahl des Empfängers. |
| Länder-/Regionscode Lieferempfänger | Land oder Region des Empfängers. |
| Herkunftstyp | Interne Herkunft der Zeile. |
| Herkunftsuntertyp | Untertyp des Ursprungsbelegs. |
| Herkunftsbeleg | Art des Ursprungsbelegs; zulässig sind Verkaufsauftrag, Verkaufsreklamation, Bestellung, Einkaufsreklamation, ausgehende Umlagerung und Serviceauftrag. |
| Herkunftsnr. | Nummer des Ursprungsbelegs. |
| Herkunftszeilennr. | Ursprungszeile im Beleg. |
| Artikelnr. | Artikel der Zeile. |
| Variantencode | Variante des Artikels. |
| Artikelreferenznr. | Zusätzliche Referenz zum Artikel. |
| Beschreibung | Artikel- oder Zeilenbeschreibung. |
| Beschreibung 2 | Ergänzende Beschreibung. |
| Einheitencode | Mengeneinheit. |
| Lagerortcode | Lagerort der Zeile. |
| Menge für Zuweisung | Menge, die dieser Versandplanung zugeordnet wird. |
| Nettogewicht | Nettogewicht der Zeile. |
| Bruttogewicht | Bruttogewicht der Zeile. |
| Versandplanungsdatum | Planungsdatum der Zeile. |
| Startzeit Versandplanung | Geplanter Startzeitpunkt. |
| Endzeit Versandplanung | Geplanter Endzeitpunkt. |
| Versanddatum | Versandtermin. |
| Versandartencode | Versandart der Zeile. |
| Geplantes Lieferdatum | Geplanter Liefertermin. |
| Geplantes Versanddatum | Geplanter Versandtermin. |
| Gewünschtes Lieferdatum | Vom Empfänger gewünschter Termin. |
| Zugesagtes Lieferdatum | Bestätigter Termin. |
| Ladestelle | Geplante Ladestelle. |
| Ladezeit | Geplante Ladezeit. |
| Ladestellen-Kapazitätseinheitencode | Einheit für die Ladeplanung. |
| Planungsstatus Ladestelle | Zulässige Werte sind leer, Geplant, Freigegeben, In Bearbeitung und Abgeschlossen. |
| Offen | Kennzeichnet die noch offene Zeile. |
| Lagerprozess | Zulässige Werte sind leer, Warenausgang, Kommissionierung oder Warenausgang und Kommissionierung. |
| Warenausgang erstellt | Kennzeichnet die Erstellung eines Warenausgangs. |
| Warenausgangsnummer | Nummer des Warenausgangs. |
| Warenausgangszeilennr. | Zeilennummer des Warenausgangs. |
| Warenausgang beendet | Kennzeichnet den abgeschlossenen Warenausgang. |
| Kommissionierung erstellt | Kennzeichnet die Erstellung einer Kommissionierung. |
| Kommissioniernummer | Nummer der Kommissionierung. |
| Kommissionierzeilennr. | Zeilennummer der Kommissionierung. |
| Kommissionierung beendet | Kennzeichnet die abgeschlossene Kommissionierung. |
| Beendet | Kennzeichnet die vollständig bearbeitete Zeile. |
| Versandnummer | Tatsächlich gebuchte Versandnummer. |
| Automotive | Kennzeichnet die Zeile als Automotive-Fall. |
| Reservierte Versandnummer | Zeigt die automatisch reservierte Versandnummer für qualifizierte Automotive-Verkaufszeilen. |

### Wichtige Bearbeitungsregeln

Aus dem Code und den angrenzenden Seiten ergibt sich für Anwender insbesondere diese Reihenfolge:

1. Zeilen zuerst der Versandplanung zuordnen.
2. Mengen und Ladedaten vervollständigen.
3. Versandplanung freigeben.
4. Erst danach Warenausgang, Kommissionierung oder Direktlieferung auslösen.
5. Nach Abschluss der Logistikschritte die Versandplanung registrieren.

Wenn Sie eine Zeile manuell wieder öffnen oder die Versandnummer leeren, betrifft das nur den aktuellen Bearbeitungsstand in der Versandplanung. Folgebelege außerhalb der Versandplanung können trotzdem bereits existieren und müssen getrennt geprüft werden.

## Lager, Folgebelege und Abschluss

### Lagerprozess aus der Versandplanung anstoßen

Die Versandplanung arbeitet mit unterschiedlichen Lagerprozessen. Welche Schritte erforderlich sind, hängt vom Lagerort und der zugrunde liegenden Logistik ab.

Typische Varianten sind:

- Verkaufsauftrag direkt zur gebuchten Verkaufslieferung.
- Verkaufsauftrag über Warenausgang zur gebuchten Verkaufslieferung.
- Verkaufsauftrag über Warenausgang und Kommissionierung zur gebuchten Verkaufslieferung.
- Verkaufsauftrag über Versandplanung zur gebuchten Verkaufslieferung für Zeilen ohne Lagerprozess.

Für Anwender ist entscheidend, dass die Versandplanung selbst nicht jeden Schritt automatisch abschließt. Nach dem Freigeben müssen Sie den passenden Folgebeleg öffnen, prüfen und verbuchen.

### Registrieren und Nachverfolgen

Nach Abschluss der operativen Schritte registrieren Sie die Versandplanung. Dadurch wird sie in die **Registrierten Versandplanungen** überführt. Dort bleibt der Vorgang nachvollziehbar und kann bei Bedarf erneut geöffnet, gedruckt oder per E-Mail versendet werden.

Die Erweiterung sorgt dafür, dass die Felder **Automotive** und **Reservierte Versandnummer** auch in die registrierten Versandplanungszeilen übernommen werden. Dadurch bleibt die EDI-Kennzeichnung auch nach dem Tagesgeschäft erhalten.

## Historie und Nachverfolgung

### Registrierte Versandplanungen nutzen

Öffnen Sie über **Suchen** die **Registrierten Versandplanungen**, wenn ein bereits abgeschlossener Vorgang geprüft werden soll. Diese Ansicht eignet sich insbesondere für Rückfragen aus Versand, Vertrieb oder EDI-Abwicklung.

Prüfen Sie dort vor allem:

- ob der Vorgang als Automotive-Fall geführt wurde,
- welche reservierte Versandnummer verwendet wurde,
- ob die Zeilen vollständig abgeschlossen wurden,
- und ob ein erneuter Ausdruck oder Versand notwendig ist.

Die Historie dient damit nicht nur der Rückschau, sondern auch der Abstimmung zwischen Versandabteilung und EDI-Prozess.

## Typische Anwendungsfälle

### Ein Automotive-Kunde meldet einen kurzfristigen Versandtermin

**Auslöser:** Ein Debitor fordert kurzfristig die Auslieferung bestimmter Verkaufsauftragszeilen an.

**Einstieg in BC:** Der Anwender öffnet über **Suchen** die **Versandplanungszuordnung und Bestandskontrolle** oder direkt die **Versandplanung**.

**Kernablauf:** In der Zuordnungsseite setzt der Anwender Filter für Debitor, Datum und **Automotive**. Danach markiert er die passenden Zeilen und übernimmt sie in die Versandplanung. Im Kopf ergänzt er Tour, Fahrzeug und Ladestelle. In den Zeilen prüft er **Automotive** und liest die automatisch gesetzte **Reservierte Versandnummer**. Anschließend gibt er die Versandplanung frei und startet den passenden Lagerprozess.

**Abschluss:** Nach Warenausgang oder direkter Lieferung registriert der Anwender die Versandplanung.

### Mehrere Zeilen sollen gesammelt einer Tour zugeordnet werden

**Auslöser:** Die Versandabteilung plant eine gemeinsame Tour für mehrere offene Lieferungen.

**Einstieg in BC:** Der Anwender öffnet die **Benutzerfiltervorlage Karte** und wählt eine vorbereitete Filtervorlage oder pflegt eine neue Vorlage.

**Kernablauf:** Die Vorlage grenzt Lagerort, Debitoren, Termine und bei Bedarf **Automotive** ein. Danach öffnet der Anwender die Zuordnungsseite, übernimmt die Treffer und ergänzt im Versandplanungskopf Tour, Fahrer und Fahrzeug. In den Zeilen pflegt er Ladereihenfolge, Versandreihenfolge und Mengen für die Zuweisung.

**Abschluss:** Nach Freigabe und Ausführung der Folgeprozesse wird die Versandplanung registriert und später bei Bedarf erneut aufgerufen.

### Ein Anwender prüft, warum eine Zeile keine reservierte Versandnummer erhalten hat

**Auslöser:** In einer Automotive-Zeile bleibt das Feld **Reservierte Versandnummer** leer.

**Einstieg in BC:** Der Anwender öffnet die betreffende **Versandplanung** und wechselt in die **Zeilen**.

**Kernablauf:** Er prüft, ob die Zeile tatsächlich als **Automotive** gekennzeichnet ist, aus einem Verkaufsbeleg stammt, einen Debitor als Lieferempfänger hat und noch keine echte Versandnummer enthält. Außerdem kontrolliert er, ob die Verkaufsauftragsdaten vollständig sind. Erst wenn diese Voraussetzungen vorliegen, kann das System eine Nummer reservieren.

**Abschluss:** Nach der Korrektur wird die Zeile erneut geprüft und die weitere Lagerabwicklung fortgesetzt.

## FAQ und Troubleshooting

### 1. Warum erscheint das Feld Automotive vorhanden im Kopf, obwohl ich es nicht gepflegt habe?

Das Feld wird automatisch ermittelt. Es zeigt an, ob mindestens eine Zeile der Versandplanung als Automotive gekennzeichnet ist.

### 2. Warum bleibt die reservierte Versandnummer leer?

Die Nummer wird nur für Automotive-Zeilen reserviert, die aus einer Verkaufszeile stammen, einen Debitor als Lieferempfänger haben und noch keine tatsächliche Versandnummer besitzen.

### 3. Kann ich die reservierte Versandnummer manuell ändern?

Nein. Das Feld ist nicht editierbar und dient nur als systemseitige Reservierung.

### 4. Warum erhalten mehrere Zeilen dieselbe reservierte Versandnummer?

Das System verwendet für passende Zeilen derselben Versandplanung dieselbe bereits reservierte Nummer erneut, wenn die fachlichen Kriterien übereinstimmen.

### 5. Warum finde ich meine Automotive-Zeilen in der Zuordnungsseite nicht?

Prüfen Sie die verwendete Benutzerfiltervorlage und insbesondere den Filter **Automotive**. Möglicherweise ist nur „Nein“ oder eine zu enge Datums- oder Debitorenauswahl hinterlegt.

### 6. Muss ich die Versandplanung vor dem Warenausgang freigeben?

Ja. Die weitere Bearbeitung baut auf der freigegebenen Versandplanung auf. Ohne Freigabe bleiben Folgeaktionen eingeschränkt.

### 7. Warum ist eine Zeile in der Versandplanung beendet, obwohl ich noch Rückfragen habe?

Das Kennzeichen **Beendet** beschreibt den logistischen Bearbeitungsstand. Für fachliche Rückfragen können Sie den Vorgang trotzdem in der registrierten Versandplanung erneut aufrufen.

### 8. Wo sehe ich nachträglich, ob ein Vorgang ein Automotive-Fall war?

In den **Registrierten Versandplanungen** bleiben die Felder **Automotive** und **Reservierte Versandnummer** erhalten.

### 9. Warum wird im Kopf nur Automotive vorhanden angezeigt, nicht aber jede einzelne Nummer?

Der Kopf dient nur als schnelle Kennzeichnung. Die eigentliche Detailprüfung erfolgt in den Zeilen der Versandplanung.

### 10. Wann pflege ich den Automotive-Filter in der Benutzerfiltervorlage und wann direkt in der Zuordnungsseite?

Verwenden Sie die Benutzerfiltervorlage für wiederkehrende Arbeitssichten. Setzen Sie den Filter direkt in der Zuordnungsseite, wenn Sie nur ausnahmsweise einen besonderen Fall prüfen möchten.
