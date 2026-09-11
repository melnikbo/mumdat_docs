---
title: Handbuch zur m+m Logistic Management mit Report Package
---

# Handbuch zur m+m Logistic Management mit Report Package

## Einleitung

Dieses Modul ergänzt die Versandplanung in Microsoft Dynamics 365 Business Central um ausgaberelevante Zusatzdaten für das m+m Report Package. Anwender arbeiten dabei weiterhin in den bekannten Seiten für Versandplanung und registrierte Versandplanung. Das Modul ergänzt diese Oberflächen insbesondere um ein Sachbearbeiterfeld und stellt zwei Berichte für die Ausgabe bereit.

Das Handbuch richtet sich an Key User in Logistik, Versand und Vertriebsinnendienst, die Versandplanungen bearbeiten, registrierte Versandplanungen prüfen und Versandunterlagen ausgeben.

Der Ablauf ist schlank:

1. Sie erfassen oder pflegen eine Versandplanung.
2. Sie ergänzen die reportrelevanten Angaben im Kopf der Versandplanung.
3. Sie prüfen die Zeilen, Termine und Ladeinformationen.
4. Sie registrieren die Versandplanung.
5. Sie drucken die Versandplanung oder die Avismeldung über die vorgesehenen Berichte.

## Schnellstart für Anwender

### Versandplanung mit reportrelevanten Angaben ergänzen

1. Öffnen Sie über **Suchen** die Seite **Versandplanung**.
2. Rufen Sie die gewünschte Versandplanung auf oder legen Sie sie nach Ihrem bestehenden Prozess an.
3. Prüfen Sie im Kopf Buchungsdatum, Versanddatum, Tour und Fahrzeug.
4. Füllen Sie das Feld **RPAS Sachbearbeitercode** aus.
5. Kontrollieren Sie in den Zeilen Mengen, Lieferadresse, Ladepunkt und Planungsstatus.
6. Registrieren Sie die Versandplanung gemäß Ihrem Standardprozess.
7. Öffnen Sie anschließend die **Registrierte Versandplanung**, wenn Sie die abgeschlossene Planung nachvollziehen oder erneut ausgeben möchten.

### Bericht ausgeben

1. Öffnen Sie die gewünschte Versandplanung oder registrierte Versandplanung.
2. Starten Sie den passenden Bericht für die Versandplanung oder die Avismeldung.
3. Setzen Sie auf der Anforderungsseite die benötigten Filter.
4. Prüfen Sie die Ausgabe vor dem endgültigen Druck oder Versand.

## Einrichtung

Das vorliegende Modul bringt keine eigene Einrichtungsseite, keine eigene Stammdatentabelle und keine eigene Profilseite mit. Die fachliche Einrichtung erfolgt deshalb in den vorhandenen Grundlagen der Versandplanung, die aus dem Basismodul bereitgestellt werden. Für den Einsatz dieses Report-Pakets sind insbesondere Nummernserien, Touren, Fahrzeuge, Ladepunkte und die allgemeine Organisation der Versandplanung relevant.

### Voraussetzungen für den Einsatz

Bevor Anwender mit dem Modul arbeiten, sollte die zugrunde liegende Versandplanung bereits betriebsbereit eingerichtet sein.

| Einrichtung | Erläuterung |
| --- | --- |
| Nummernserie der Versandplanung | Steuert die Vergabe der laufenden Nummern für Versandplanung und registrierte Versandplanung. |
| Liefertouren | Ordnen Versandplanungen einer Tour zu und bündeln Lieferungen für die weitere Abwicklung. |
| Versandfahrzeuge | Stellen die Fahrzeugdaten für Planung, Ausdruck und Nachverfolgung bereit. |
| Ladepunkte | Legen fest, an welchem Ladepunkt und mit welcher Kapazität die Verladung eingeplant wird. |
| Benutzer und Berechtigungen | Anwender benötigen Zugriff auf Versandplanung, registrierte Versandplanung und die zugehörigen Berichte. |

### Report-Package-spezifische Ergänzung

Das Modul ergänzt den Kopf der offenen und der registrierten Versandplanung um ein zusätzliches Feld für die sachbearbeitende Person. Dieses Feld sollte in Ihrem Unternehmen verbindlich gepflegt werden, wenn Berichte oder interne Abläufe danach ausgerichtet sind.

| Einrichtung | Erläuterung |
| --- | --- |
| RPAS Sachbearbeitercode | Kennzeichnet die zuständige Person für die Versandplanung. Der Wert steht auf der offenen und auf der registrierten Versandplanung zur Verfügung und kann in Ausgaben oder nachgelagerten Abläufen verwendet werden. |

## Stammdaten und Grundlagen der Versandplanung

Dieses Modul führt keine eigenen Stammdatenseiten ein. Für den Anwender relevant bleiben die Stammdaten der Versandplanung aus der zugrunde liegenden Lösung. Dazu gehören insbesondere Touren, Fahrzeuge, Kreditoren bei einkaufsbezogenen Vorgängen sowie Ladepunkte und Lagerorte.

### Relevante Grundlagen im Tagesgeschäft

| Stammdatum / Grundlage | Erläuterung |
| --- | --- |
| Liefertouren | Bündeln Versandplanungen nach Tour und helfen bei der Reihenfolge der Abarbeitung. |
| Versandfahrzeuge | Stellen Fahrzeugcode und Kennzeichen für Planung und Ausdruck bereit. |
| Kreditoren | Werden genutzt, wenn Versandplanungen im Einkaufskontext oder bei Rücklieferungen verwendet werden. |
| Ladepunkte | Steuern, wo und wann eine Zeile verladen wird. |
| Lagerorte | Bestimmen den logistischen Ursprung der Zeile. |
| Artikel und Varianten | Liefern die fachlichen Stammdaten für Position, Variante, Gewichte und Mengeneinheiten. |

## Tägliche Arbeit mit der Versandplanung

### Kopf der Versandplanung

Öffnen Sie die Seite **Versandplanung** über **Suchen**. Im Kopf pflegen Sie die organisatorischen und logistischen Angaben, bevor Sie die Zeilen im Detail bearbeiten. Arbeiten Sie dabei in dieser Reihenfolge: zuerst Identifikation und Termine, danach Tour und Logistik, anschließend Fahrzeug und Ansprechpartner.

| Feld | Erläuterung |
| --- | --- |
| Nr. | Eindeutige Nummer der Versandplanung. |
| Status | Zeigt den Bearbeitungsstand an. Verwendet werden mindestens die Werte **Offen** und **Freigegeben**. |
| Belegdatum | Datum des Belegs. |
| Buchungsdatum | Datum, mit dem die Versandplanung gebucht oder registriert wird. |
| Anzahl Gesamtzeilen | Zeigt die Gesamtzahl aller Zeilen der Versandplanung. |
| Anzahl offener Zeilen | Zeigt, wie viele Zeilen noch nicht abgeschlossen sind. |
| Anzahl offener Lagerausgangszeilen | Zeigt offene Zeilen mit Bezug zum Lagerausgang. |
| Anzahl fertiger Lagerausgangszeilen | Zeigt bereits fertig bearbeitete Lagerausgangszeilen. |
| Anzahl offener Kommissionierzeilen | Zeigt offene Zeilen mit Bezug zur Kommissionierung. |
| Anzahl fertiger Kommissionierzeilen | Zeigt bereits abgeschlossene Kommissionierzeilen. |
| Anzahl fertiger Zeilen | Zeigt die Zahl vollständig abgeschlossener Zeilen. |
| Liefertourcode | Ordnet die Versandplanung einer Tour zu. |
| Interne Logistik | Kennzeichnet, ob interne Logistikprozesse berücksichtigt werden. |
| Einkaufsreklamationen anzeigen | Blendet einkaufsbezogene Rücklieferungen in der Planung ein, sofern der zugrunde liegende Prozess dies nutzt. |
| Versanddatum | Legt den fachlichen Termin der Versandplanung fest. |
| Kreditorennr. | Verweist auf den betroffenen Kreditor. |
| Einkaufsbelegnr. | Zeigt den zugehörigen Einkaufsbeleg an. |
| Versandfahrzeugcode | Weist der Versandplanung ein Fahrzeug zu. |
| Amtliches Kennzeichen | Ergänzt oder bestätigt das Kennzeichen des Fahrzeugs. |
| Interne Fahrermitarbeiternr. | Verknüpft die Versandplanung mit einem internen Fahrer. |
| Externe Fahrerkontaktnr. | Verknüpft die Versandplanung mit einem externen Ansprechpartner. |
| Ladepunkt-Lagerortcode | Bestimmt den Lagerort des gewählten Ladepunkts. |
| Ladepunkt | Bestimmt den konkreten Ladepunkt. |
| Ladepunkt-Kapazitätseinheitencode | Zeigt die Kapazitätseinheit des Ladepunkts an. |
| RPAS Sachbearbeitercode | Kennzeichnet den zuständigen Sachbearbeiter für diese Versandplanung. |

### Zeilen der Versandplanung

Die Zeilen steuern die operative Abarbeitung. Prüfen Sie nach dem Öffnen der Versandplanung zuerst Empfänger und Ursprungsbeleg, danach Artikel und Mengen, anschließend Termine und Ladeinformationen. Der Planungsstatus des Ladepunkts zeigt, wie weit die einzelne Zeile in der Verladeplanung fortgeschritten ist.

| Feld | Erläuterung |
| --- | --- |
| Ladereihenfolge | Bestimmt die Reihenfolge beim Laden. |
| Lieferreihenfolge | Bestimmt die Reihenfolge der Auslieferung. |
| Lief.-an-Art | Zeigt, ob an **Debitor**, **Lagerort** oder **Kreditor** geliefert wird. |
| Lief.-an-Nr. | Nummer des Empfängers oder Zielorts. |
| Lief.-an-Name | Name des Empfängers. |
| Lief.-an-Name 2 | Zweite Namenszeile des Empfängers. |
| Lief.-an-Adresse | Erste Adresszeile des Empfängers. |
| Lief.-an-Adresse 2 | Zweite Adresszeile des Empfängers. |
| Lief.-an-Ort | Ort der Lieferadresse. |
| Lief.-an-PLZ-Code | Postleitzahl der Lieferadresse. |
| Lief.-an-Länder-/Regionscode | Land oder Region der Lieferadresse. |
| Herkunftsart | Technische Einordnung des Ursprungsdatensatzes. |
| Herkunftsunterart | Verfeinert die Herkunftsart innerhalb des Prozesses. |
| Herkunftsbeleg | Zeigt den Belegtyp, zum Beispiel **Verkaufsauftrag**, **Verkaufsreklamation**, **Bestellung**, **Einkaufsreklamation**, **Ausgehende Umlagerung** oder **Serviceauftrag**. |
| Herkunftsnr. | Nummer des Ursprungsbelegs. |
| Herkunftszeilennr. | Zeilennummer des Ursprungsbelegs. |
| Artikelnr. | Artikel der Versandzeile. |
| Variantencode | Variante des Artikels. |
| Referenznr. | Externe oder interne Referenz zum Artikel oder Beleg. |
| Beschreibung | Erste Beschreibung der Position. |
| Beschreibung 2 | Zweite Beschreibung der Position. |
| Einheitencode | Mengeneinheit der Position. |
| Lagerortcode | Lagerort der Zeile. |
| Zuzuweisende Menge | Menge, die in der Versandplanung berücksichtigt wird. |
| Nettogewicht | Nettogewicht der Zeile. |
| Bruttogewicht | Bruttogewicht der Zeile. |
| Versanddatum | Zeigt das fachliche Versanddatum der Zeile. |
| Startzeit Versandplanung | Geplanter Startzeitpunkt der Bearbeitung oder Verladung. |
| Endzeit Versandplanung | Geplantes Ende der Bearbeitung oder Verladung. |
| Lieferdatum | Termin der tatsächlichen Lieferung aus Sicht des Belegs. |
| Versandartencode | Definiert die Versandart. |
| Geplantes Lieferdatum | Geplanter Liefertermin. |
| Geplantes Versanddatum | Geplanter Versandtermin. |
| Gewünschtes Lieferdatum | Vom Geschäftsvorfall gewünschter Liefertermin. |
| Zugesagtes Lieferdatum | Verbindlich bestätigter Liefertermin. |
| Ladepunkt | Ladepunkt für die einzelne Zeile. |
| Ladezeit | Veranschlagte Zeit am Ladepunkt. |
| Ladepunkt-Kapazitätseinheitencode | Kapazitätseinheit für die Ladezeit. |
| Ladepunkt-Planungsstatus | Steuert den Fortschritt am Ladepunkt. Typische Werte sind **Leer**, **Geplant**, **Freigegeben**, **In Bearbeitung** und **Fertig**. |
| Offen | Kennzeichnet, ob die Zeile noch offen ist. |
| Lagerprozess | Zeigt den zugehörigen Lagerprozess. Typische Werte sind **Leer**, **Lagerausgang**, **Kommissionierung** oder **Lagerausgang und Kommissionierung**. |
| Lagerausgang erstellt | Zeigt an, ob bereits ein Lagerausgang erzeugt wurde. |
| Lagerausgangsnr. | Nummer des erzeugten Lagerausgangs. |
| Lagerausgangszeilennr. | Zeilennummer im Lagerausgang. |
| Lagerausgang abgeschlossen | Zeigt an, ob der Lagerausgang abgeschlossen ist. |
| Kommissionierung erstellt | Zeigt an, ob bereits eine Kommissionierung erzeugt wurde. |
| Kommissionierungsnr. | Nummer der Kommissionierung. |
| Kommissionierungszeilennr. | Zeilennummer der Kommissionierung. |
| Kommissionierung abgeschlossen | Zeigt an, ob die Kommissionierung abgeschlossen ist. |
| Fertig | Kennzeichnet die vollständig abgeschlossene Versandzeile. |
| Lieferungsnr. | Nummer der entstandenen Lieferung. |

### Arbeiten mit der Zeilensteuerung

In der täglichen Praxis ist folgende Reihenfolge sinnvoll:

1. Prüfen Sie, ob der richtige Ursprungsbeleg und die richtige Empfängeradresse gezogen wurden.
2. Kontrollieren Sie Artikel, Variante, Menge und Gewichte.
3. Stimmen Sie Versanddatum, Lieferdatum und weitere Terminangaben ab.
4. Legen Sie Ladepunkt, Ladezeit und gegebenenfalls die Reihenfolge fest.
5. Beobachten Sie den Ladepunkt-Planungsstatus sowie die Kennzeichen für Lagerausgang und Kommissionierung.
6. Registrieren Sie die Versandplanung erst, wenn die Zeilen fachlich vollständig geplant sind.

## Registrierte Versandplanung und Nachverfolgung

### Kopf der registrierten Versandplanung

Nach der Registrierung bleibt die Planung zur Nachverfolgung erhalten. Öffnen Sie dazu die Seite **Registrierte Versandplanung**. Die Daten sind grundsätzlich nicht mehr zur freien Bearbeitung gedacht, dienen aber der Kontrolle, dem Ausdruck und der Rückverfolgung.

| Feld | Erläuterung |
| --- | --- |
| Nr. | Eindeutige Nummer der registrierten Versandplanung. |
| Belegdatum | Ursprüngliches Belegdatum. |
| Buchungsdatum | Tatsächliches Buchungsdatum der Registrierung. |
| Versandplanungsnr. | Verweist auf die offene Versandplanung, aus der registriert wurde. |
| Liefertourcode | Übernommene Tour der Planung. |
| Interne Logistik | Übernommene Kennzeichnung aus der offenen Planung. |
| Versanddatum | Übernommener fachlicher Termin. |
| Kreditorennr. | Zugeordneter Kreditor. |
| Einkaufsbelegnr. | Zugehöriger Einkaufsbeleg. |
| Versandfahrzeugcode | Zugeordnetes Fahrzeug. |
| Amtliches Kennzeichen | Kennzeichen des Fahrzeugs. |
| Interne Fahrermitarbeiternr. | Interner Fahrer. |
| Externe Fahrerkontaktnr. | Externer Fahrer oder Ansprechpartner. |
| Name des Fahrers | Anzeigename des Fahrers. |
| RPAS Sachbearbeitercode | Übernommener Sachbearbeitercode aus der Planung. |

### Zeilen der registrierten Versandplanung

Die registrierten Zeilen dokumentieren den finalen Stand zum Zeitpunkt der Registrierung. Nutzen Sie die Seite für Rückfragen, Ausdrucke und die Kontrolle bereits bearbeiteter Versandvorgänge.

| Feld | Erläuterung |
| --- | --- |
| Ladereihenfolge | Gespeicherte Reihenfolge beim Laden. |
| Lieferreihenfolge | Gespeicherte Reihenfolge bei der Auslieferung. |
| Lief.-an-Art | Empfängerart der registrierten Zeile. |
| Lief.-an-Nr. | Nummer des Empfängers oder Zielorts. |
| Lief.-an-Name | Name des Empfängers. |
| Lief.-an-Name 2 | Zweite Namenszeile. |
| Lief.-an-Adresse | Erste Adresszeile. |
| Lief.-an-Adresse 2 | Zweite Adresszeile. |
| Lief.-an-Ort | Ort der Lieferadresse. |
| Lief.-an-PLZ-Code | Postleitzahl der Lieferadresse. |
| Lief.-an-Länder-/Regionscode | Land oder Region der Lieferadresse. |
| Herkunftsart | Ursprungsart des Vorgangs. |
| Herkunftsunterart | Weitere Differenzierung des Vorgangs. |
| Herkunftsbeleg | Ursprungsbelegtyp. |
| Herkunftsnr. | Nummer des Ursprungsbelegs. |
| Herkunftszeilennr. | Zeilennummer des Ursprungsbelegs. |
| Artikelnr. | Artikel der Zeile. |
| Variantencode | Artikelvariante. |
| Referenznr. | Referenz zum Artikel oder Beleg. |
| Beschreibung | Erste Positionsbeschreibung. |
| Beschreibung 2 | Zweite Positionsbeschreibung. |
| Einheitencode | Mengeneinheit. |
| Lagerortcode | Lagerort der registrierten Zeile. |
| Zugewiesene Menge | Registrierte Menge. |
| Nettogewicht | Registriertes Nettogewicht. |
| Bruttogewicht | Registriertes Bruttogewicht. |
| Versanddatum | Registriertes Versanddatum. |
| Startzeit Versandplanung | Registrierte Startzeit. |
| Endzeit Versandplanung | Registrierte Endzeit. |
| Lieferdatum | Registriertes Lieferdatum. |
| Ladepunkt | Registrierter Ladepunkt. |
| Ladezeit | Registrierte Ladezeit. |
| Ladepunkt-Kapazitätseinheitencode | Kapazitätseinheit für die Ladezeit. |
| Ladepunkt-Planungsstatus | Stand der Planung zum Registrierungszeitpunkt. |
| Lieferungsnr. | Nummer der erzeugten Lieferung. |

## Berichte und Ausgabe

Das Modul stellt zwei Berichte bereit. Beide bauen auf den Daten der Versandplanung auf und werden für die operative Ausgabe genutzt.

### Bericht Versandplanung

Der Bericht **MuM RPAS Shipment Planning** dient zur Ausgabe einer Versandplanung. Anwender nutzen ihn, wenn die aktuelle Planung als Arbeitsunterlage, Abstimmungsgrundlage oder Versanddokument benötigt wird.

Typische Verwendung:

1. Öffnen Sie die offene Versandplanung.
2. Prüfen Sie Tour, Fahrzeug, Termine und Sachbearbeitercode.
3. Starten Sie den Bericht für die Versandplanung.
4. Setzen Sie die benötigten Filter in der Anforderungsseite.
5. Kontrollieren Sie die Ausgabe vor dem Druck.

### Bericht Avismeldung

Der Bericht **MuM RPAS Advice Notification** dient zur Ausgabe einer Avismeldung. Er wird eingesetzt, wenn Empfänger oder interne Stellen über die bevorstehende oder erfolgte Lieferung informiert werden sollen.

Typische Verwendung:

1. Öffnen Sie die passende Versandplanung oder den zugehörigen Vorgang.
2. Prüfen Sie Empfänger, Lieferadresse, Fahrzeug und Termine.
3. Starten Sie den Bericht für die Avismeldung.
4. Filtern Sie die Ausgabe auf die benötigten Vorgänge.
5. Prüfen Sie die fertige Ausgabe vor der Weitergabe.

## Historie und Nachverfolgung

Das Modul liefert keine eigene Protokollseite, keine eigene Archivliste und keine eigene Versandhistorie. Die Nachverfolgung erfolgt daher vor allem über die **Registrierte Versandplanung** und über die Belegverweise in den Zeilen.

### Was Sie nachvollziehen können

| Bereich | Erläuterung |
| --- | --- |
| Registrierte Versandplanung | Zeigt den abgeschlossenen Stand der Planung im Kopf und in den Zeilen. |
| Ursprungsbeleg | Über Herkunftsbeleg, Herkunftsnr. und Herkunftszeilennr. kann der Ausgangsvorgang zurückverfolgt werden. |
| Lagerdokumente | Lagerausgang und Kommissionierung lassen sich über die gespeicherten Nummern prüfen. |
| Lieferung | Über die Lieferungsnr. sehen Sie, welche Lieferung aus der Zeile entstanden ist. |

## FAQ und Troubleshooting

### 1. Warum kann ich eine Versandplanung nicht vollständig abschließen?

Prüfen Sie zuerst die Zeilen. Solange Mengen, Termine, Ladepunkt oder logistische Folgeprozesse nicht sauber geplant sind, bleiben Zeilen offen oder stehen nicht auf **Fertig**.

### 2. Warum sehe ich in der Versandplanung keinen vollständigen Ausdruck?

Prüfen Sie, ob die kopf- und zeilenbezogenen Pflichtangaben gepflegt sind. Fehlende Angaben zu Tour, Fahrzeug, Empfänger oder Sachbearbeiter können die fachliche Aussagekraft des Ausdrucks mindern.

### 3. Was bedeutet der Status in der Versandplanung?

Der Kopfstatus steuert den allgemeinen Bearbeitungsstand. Üblicherweise arbeiten Sie mindestens mit **Offen** und **Freigegeben**. Bearbeiten Sie inhaltliche Daten, solange der Vorgang noch nicht endgültig abgeschlossen ist.

### 4. Wofür dient der RPAS Sachbearbeitercode?

Das Feld kennzeichnet die zuständige Person für die Versandplanung. Nutzen Sie es einheitlich, damit Ausdrucke und interne Rückfragen eindeutig zugeordnet werden können.

### 5. Warum erscheint keine Lagerdokumentnummer in der Zeile?

Die Felder für Lagerausgang und Kommissionierung werden erst gefüllt, wenn der zugehörige Lagerprozess tatsächlich angestoßen oder abgeschlossen wurde.

### 6. Warum ist eine Zeile noch offen, obwohl sie bereits eingeplant ist?

Die reine Termin- und Ladeplanung reicht nicht immer aus. Prüfen Sie, ob Lagerausgang, Kommissionierung oder weitere logistische Schritte noch ausstehen.

### 7. Was ist der Unterschied zwischen Versanddatum und Lieferdatum?

Das **Versanddatum** beschreibt den geplanten Versandvorgang. Das **Lieferdatum** bezieht sich auf den Termin beim Empfänger oder im zugrunde liegenden Beleg. Beide Felder sollten bewusst gepflegt werden.

### 8. Wann arbeite ich in der offenen und wann in der registrierten Versandplanung?

Die offene Versandplanung dient der Bearbeitung und Planung. Die registrierte Versandplanung dient der Nachverfolgung, Prüfung und erneuten Ausgabe abgeschlossener Vorgänge.

### 9. Warum wird ein Ladepunkt-Planungsstatus benötigt?

Der Status zeigt den Fortschritt am Ladepunkt. Damit erkennen Sie schnell, ob eine Zeile nur geplant, bereits freigegeben, in Bearbeitung oder fertig ist.

### 10. Warum finde ich eine Lieferung nur über die Zeile und nicht direkt im Kopf?

Die Lieferung entsteht fachlich aus der einzelnen Versandzeile. Deshalb wird die Lieferungsnummer zeilenbezogen geführt und sollte auch dort geprüft werden.

## Typische Anwendungsfälle

### Anwendungsfall 1: Speditionsabholung für mehrere Lieferungen vorbereiten

**Auslöser:** Die Logistik erhält eine Meldung, dass ein Fahrzeug mehrere Aufträge an einem festen Termin abholen soll.

**Einstieg in BC:** Der Anwender sucht nach **Versandplanung**.

**Kernablauf:**

1. Öffnen Sie die passende Versandplanung.
2. Tragen Sie Versanddatum, Liefertourcode und Versandfahrzeugcode ein.
3. Ergänzen Sie Kennzeichen sowie internen oder externen Fahrer.
4. Pflegen Sie den **RPAS Sachbearbeitercode**.
5. Prüfen Sie in den Zeilen Empfänger, Artikel, Menge, Ladepunkt und Ladezeit.
6. Setzen Sie den Ladepunkt-Planungsstatus je Zeile entsprechend dem Fortschritt.
7. Registrieren Sie die Versandplanung, sobald die Planung fachlich steht.

**Abschluss:** Drucken Sie anschließend den Bericht zur Versandplanung für Lager und Fahrer aus.

### Anwendungsfall 2: Avismeldung für einen geplanten Versand ausgeben

**Auslöser:** Ein Empfänger oder eine interne Stelle benötigt vorab eine Avismeldung zur bevorstehenden Lieferung.

**Einstieg in BC:** Der Anwender öffnet die passende **Versandplanung** oder arbeitet von der bekannten Nummer aus.

**Kernablauf:**

1. Prüfen Sie im Kopf Empfängerbezug, Fahrzeug, Tour und Termine.
2. Kontrollieren Sie in den Zeilen Lieferadresse, Versandart, geplantes Lieferdatum und Ladeinformationen.
3. Starten Sie den Bericht **MuM RPAS Advice Notification**.
4. Begrenzen Sie die Ausgabe mit den erforderlichen Filtern.
5. Prüfen Sie die fertige Avismeldung in der Vorschau.

**Abschluss:** Geben Sie die Avismeldung intern weiter oder drucken Sie sie für die weitere Kommunikation aus.

### Anwendungsfall 3: Registrierte Versandplanung bei Rückfragen nachvollziehen

**Auslöser:** Nach der Auslieferung gibt es eine Rückfrage zu Empfänger, Ladepunkt oder Ursprungsbeleg.

**Einstieg in BC:** Der Anwender sucht nach **Registrierte Versandplanung**.

**Kernablauf:**

1. Öffnen Sie die registrierte Versandplanung über die bekannte Nummer.
2. Prüfen Sie im Kopf Versanddatum, Tour, Fahrzeug und Sachbearbeiter.
3. Kontrollieren Sie in den Zeilen den Herkunftsbeleg, die Lieferadresse und die Lieferungsnr.
4. Nutzen Sie bei Bedarf Lagerausgangs- oder Kommissionierungsnummern zur weiteren Nachverfolgung.

**Abschluss:** Drucken Sie bei Bedarf den Bericht erneut oder geben Sie die Informationen an Vertrieb, Lager oder Empfänger weiter.
