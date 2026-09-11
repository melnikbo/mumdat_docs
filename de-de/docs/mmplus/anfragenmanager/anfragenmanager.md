---
title: Anwenderhandbuch m+m Purchase Quote Manager
---

# Anwenderhandbuch m+m Purchase Quote Manager

## Einleitung
Der Einkaufsanfragenmanager unterstützt Sie dabei, aus Bedarfen und bestehenden Belegen strukturierte Einkaufsanfragenkampagnen aufzubauen, Lieferanten zu bündeln und daraus Einkaufsanfragen sowie später Einkaufsbestellungen zu erzeugen.

Das Modul richtet sich an Mitarbeitende im Einkauf sowie an Key User, die Einkaufsanfragen aus Verkaufsbelegen, Bestellungen oder dem Bestellungsarbeitsblatt vorbereiten, vergleichen und nachverfolgen. Der typische Ablauf beginnt mit einer Einkaufsanfragenkampagne, führt über Kreditoren- und Artikelzeilen zu Einkaufsanfragen und endet mit Einkaufsbestellungen oder dem Abschluss der Kampagne.

## Schnellstart für Anwender
### Neue Kampagne manuell anlegen
1. Öffnen Sie über **Einkaufsanfragenkampagne** die Kampagnenliste.
2. Wählen Sie **Neu**.
3. Tragen Sie in der Karte mindestens Beschreibung, Lagerortcode und Einkäufercode ein.
4. Erfassen Sie im Bereich **Kreditoren** mindestens eine Kreditorenzeile.
5. Erfassen Sie im Bereich **Artikel** die anzufragenden Artikel und Mengen.
6. Führen Sie die Aktion **Einkaufsanfrage erstellen** aus, um die Einkaufsanfragen zu erzeugen.
7. Öffnen Sie die erzeugten Einkaufsanfragen über die Beleg-Nr. in den Kreditoren- oder Artikelzeilen.

### Kampagne aus vorhandenem Beleg erzeugen
1. Öffnen Sie einen unterstützten Beleg, zum Beispiel **Verkaufsangebot**, **Verkaufsauftrag**, **Rahmenauftrag**, eine Einkaufsbestellung oder eine Zeile im **Bestellungsarbeitsblatt**.
2. Starten Sie dort die Aktion **Einkaufskampagne erstellen**.
3. Öffnen Sie die verknüpfte Kampagne über die **Einkaufskampagne Nr.** im Beleg.
4. Prüfen Sie die übernommenen Kreditoren- und Artikelzeilen.
5. Erstellen Sie anschließend die Einkaufsanfragen.

## Einrichtung
### Nummernserie in Einkaufs- & Kreditoren-Einrichtung
Bevor Sie Kampagnen anlegen, muss in der Seite **Einkaufs- & Kreditoren Einrichtung** im Bereich **Einkaufsanfragenkampagne** eine Nummernserie hinterlegt sein. Ohne diese Vorgabe meldet das Modul beim Anlegen einer Kampagne einen Fehler, weil die Kampagnennummer nicht vergeben werden kann.

| Einrichtung | Erläuterung |
| --- | --- |
| Einkaufsanfragenkampagnen Nummernserie | Wenn Sie hier eine Nummernserie hinterlegen, vergibt Business Central beim Anlegen einer neuen Kampagne automatisch eine Nummer aus dieser Serie; fehlt der Eintrag, lässt sich keine Kampagne speichern. |

Die Kampagnennummer wird beim Einfügen einer neuen Kampagne aus genau dieser Nummernserie gelesen. Wenn zu der Nummernserie verwandte Serien existieren, kann Business Central die passende Serie auswählen.

### Voraussetzungen für den täglichen Einsatz
Für die spätere Verarbeitung sollten folgende Stammdaten und Standardvorgaben vorhanden sein:

| Einrichtung | Erläuterung |
| --- | --- |
| Lagerortcode | Wenn Sie auf der Kampagne einen Lagerortcode setzen, wird er beim Erzeugen der Einkaufsanfragen in deren Kopf übernommen und auf die Artikelzeilen verteilt; so steuern Sie, für welchen Lagerort der Bedarf angefragt wird. |
| Einkäufercode | Wenn Sie einen Einkäufercode hinterlegen, wird er auf die erzeugten Einkaufsanfragen übertragen und kennzeichnet dort den verantwortlichen Einkäufer. |
| Kreditoren | Müssen vor dem Anlegen von Kreditorenzeilen vorhanden sein, sonst kann keine Einkaufsanfrage entstehen. |
| Artikel | Müssen vor dem Anlegen von Artikelzeilen vorhanden sein; bei Auswahl eines Artikels werden Beschreibung, EK-Preis und Einheit vorbelegt. |

### Lizenzprüfung beim Anmelden
Das Modul baut auf **m+m Cloud Base** auf. Bei der Anmeldung prüft der Einkaufsanfragenmanager die Lizenz über das Bezahlmodul. Ist keine gültige Lizenz vorhanden, weist Business Central darauf hin; die Kampagnenfunktionen stehen dann nicht uneingeschränkt zur Verfügung.

## Stammdaten und Grundlagen der Kampagne
### Kampagnenliste
Die Seite **Einkaufsanfragenkampagne** (Liste) dient als Einstieg in alle vorhandenen Kampagnen. Sie ist absteigend nach Nummer sortiert und bietet die Ansichten **Offen**, **Freigegeben** und **Beendet**. Von hier aus öffnen Sie einzelne Kampagnenkarten und prüfen den Bearbeitungsstand. Die Liste selbst ist nicht bearbeitbar; Änderungen nehmen Sie in der Karte vor.

| Feld | Erläuterung |
| --- | --- |
| Nr. | Eindeutige Kennung der Kampagne. |
| Beschreibung | Freitext zur Benennung des Beschaffungsvorhabens. |
| Status | Zeigt, ob die Kampagne offen, freigegeben oder beendet ist, und steuert damit, ob die Kampagne noch bearbeitet werden darf. |
| Verknüpfte Belegart | Zeigt, aus welchem Ursprung die Kampagne stammt, zum Beispiel Verkaufsangebot, Verkaufsauftrag, Rahmenauftrag, Einkaufsbestellung oder Bestellungsarbeitsblatt. |
| Verknüpfte Beleg-Nr. | Nummer des Ursprungsbelegs. Über die Drilldown-Funktion springen Sie direkt auf die zugehörige Belegkarte. |
| Verknüpfter Arbeitsblattvorlagenname | Bei Bezug zum Bestellungsarbeitsblatt der Name der Arbeitsblattvorlage. |
| Verknüpfter Artikelbuchblattname | Bei Bezug zum Bestellungsarbeitsblatt der Name des Buch.-Blatts. |

### Kampagnenkarte
Die Karte **Einkaufsanfragenkampagne** steuert den gesamten Prozess. Hier pflegen Sie die Kopfdaten und arbeiten mit den Kreditoren- und Artikelzeilen. Der Bereich mit den verknüpften Belegdaten wird nur eingeblendet, wenn die Kampagne aus einem Beleg entstanden ist.

| Feld | Erläuterung |
| --- | --- |
| Nr. | Wird beim Einfügen automatisch aus der Nummernserie vergeben; ist keine automatische Serie eingerichtet, müssen Sie die Nummer manuell holen. |
| Beschreibung | Wenn Sie hier den Zweck der Kampagne eintragen, wird dieser Text beim Kopieren der Kampagne in die neue Kampagne übernommen. |
| Status | Wird vom Prozess gesteuert. Nur im Status Offen sind Kopf und Zeilen bearbeitbar; in anderen Status sperrt das Modul Änderungen. |
| Lagerortcode | Wenn Sie den Lagerortcode ändern, bietet das Modul an, den neuen Code auf alle vorhandenen Artikelzeilen zu übertragen, und übergibt ihn später an die erzeugten Einkaufsanfragen. |
| Einkäufercode | Wenn Sie einen Einkäufercode setzen, wird er beim Erzeugen der Einkaufsanfragen in deren Kopf geschrieben. |
| Verknüpfte Belegart | Kennzeichnet, ob die Kampagne aus einem Verkaufsbeleg, einer Einkaufsbestellung oder dem Bestellungsarbeitsblatt entstanden ist; das Feld ist nicht editierbar. |
| Verknüpfte Beleg-Nr. | Speichert die Nummer des Ursprungsbelegs; per Drilldown öffnen Sie den Ursprungsbeleg. |
| Verknüpfter Arbeitsblattvorlagenname | Speichert bei Bezug zum Bestellungsarbeitsblatt die verwendete Vorlage. |
| Verknüpfter Artikelbuchblattname | Speichert bei Bezug zum Bestellungsarbeitsblatt den Namen des Buch.-Blatts. |
| Verknüpfte Zeilennr. | Speichert bei Bezug zum Bestellungsarbeitsblatt die Zeile; nach dem Erzeugen der Einkaufsanfragen wird sie zurückgesetzt, damit dieselbe Zeile erneut verwendet werden kann. |

### Kreditorenzeilen
Im Bereich **Kreditoren** hinterlegen Sie, welche Kreditoren die Kampagne anfragen soll. Für jede Zeile kann später eine Einkaufsanfrage oder Einkaufsbestellung entstehen. Das Kreditorenfeld ist als Pflichtangabe gekennzeichnet.

| Feld | Erläuterung |
| --- | --- |
| Kreditor Nr. | Der anzufragende Lieferant. Ohne Kreditor Nr. wird beim Erstellen keine Einkaufsanfrage erzeugt, sondern eine Meldung protokolliert. |
| Name | Wird aus dem Kreditor übernommen und dient der Kontrolle. |
| Adresse | Wird aus dem Kreditor übernommen und dient der Übersicht. |
| Belegart | Zeigt, ob für diese Zeile bereits eine Einkaufsanfrage oder Einkaufsbestellung existiert; solange leer, ist die Zeile noch unverarbeitet. |
| Beleg-Nr. | Verweist auf die erzeugte Einkaufsanfrage oder Einkaufsbestellung; per Drilldown öffnen Sie den jeweiligen Beleg. |
| Anfragenstatus | Zeigt den Status der erzeugten Einkaufsanfrage (zum Beispiel Offen oder Freigegeben) und steuert, ob die Freigabe-Aktionen der Zeile verfügbar sind. |

### Artikelzeilen
Im Bereich **Artikel** definieren Sie, welche Artikel je Kreditorenzeile angefragt werden. Wenn Sie eine zusätzliche Kreditorenzeile anlegen, übernimmt das Modul die bereits erfassten Artikel als neue Artikelzeilen für diesen Kreditor.

| Feld | Erläuterung |
| --- | --- |
| Artikelnummer | Der anzufragende Artikel. Bei Auswahl werden Beschreibung, EK-Preis und Einheit aus dem Artikel vorbelegt. |
| Beschreibung | Bezeichnung des Artikels; kann je Zeile angepasst werden. |
| Variantencode | Wenn der Artikel Varianten führt, legen Sie hier die anzufragende Variante fest. |
| Menge | Bedarf für diese Zeile. Zeilen mit Menge 0 werden beim Erstellen der Einkaufsanfragen nicht verarbeitet, sondern als Fehler protokolliert. |
| Lagerortcode | Lagerort der angefragten Menge; wird beim Einfügen aus dem Kopf der Kampagne vorbelegt. |
| Einheit | Maßeinheit der Menge; wird in die Einkaufsanfragezeile übernommen. |
| EK-Preis Ohne MwSt. | Angefragter oder erwarteter Einkaufspreis. Eine Änderung berechnet den Zeilenbetrag neu. |
| Zeilenbetrag | Wird aus Menge und EK-Preis berechnet und ist nicht direkt editierbar. |
| Wareneingangsdatum | Geplantes Wareneingangsdatum; wird beim Erzeugen der Einkaufsanfrage in die Wareneingangs- und Bedarfstermine der Einkaufszeile übernommen. |
| Belegart | Zeigt, ob die Zeile bereits an eine Einkaufsanfrage oder Einkaufsbestellung gebunden ist. |
| Beleg-Nr. | Nummer der zugehörigen Einkaufsanfrage oder Einkaufsbestellung; per Drilldown öffnen Sie den Beleg. |
| Belegzeilennr. | Zeilennummer in der erzeugten Einkaufsanfrage oder Einkaufsbestellung. |

## Tägliche Arbeit mit der Einkaufsanfragenkampagne
### Kampagne anlegen und pflegen
Legen Sie zuerst die Kampagne an oder lassen Sie sie aus einem Ursprungsbeleg erzeugen. Prüfen Sie danach die Kopfdaten. Wenn die Kampagne aus einem Verkaufsbeleg, einer Einkaufsbestellung oder dem Bestellungsarbeitsblatt stammt, werden die Artikelzeilen anhand der verknüpften Belegart und Belegnummer aufgebaut. Übernommen werden dabei jeweils nur Zeilen vom Typ Artikel.

Das Modul kennt folgende Ursprünge:

| Feldwert | Bedeutung |
| --- | --- |
| Verkaufsangebot | Die Kampagne wurde aus einem Verkaufsangebot erzeugt. Die Artikelzeilen werden aus den Artikelzeilen des Angebots übernommen. |
| Verkaufsauftrag | Die Kampagne wurde aus einem Verkaufsauftrag erzeugt; die Artikelzeilen stammen aus dem Auftrag. |
| Rahmenauftrag | Die Kampagne wurde aus einem Verkaufsrahmenauftrag erzeugt. |
| Einkaufsbestellung | Die Kampagne wurde aus einer Einkaufsbestellung erzeugt; deren Artikelzeilen bilden die Kampagnenartikel. |
| Bestellungsarbeitsblatt | Die Kampagne wurde aus einer oder mehreren Zeilen des Bestellungsarbeitsblatts erzeugt. |

Wenn Sie eine Kampagne aus einem bereits verknüpften Beleg erneut anstoßen, erkennt das Modul die vorhandene Kampagne und bietet stattdessen an, die bestehende Karte zu öffnen.

### Einkaufsanfragen erzeugen
Nachdem Kreditoren- und Artikelzeilen vollständig gepflegt sind, erzeugen Sie über die Aktion **Einkaufsanfrage erstellen** auf der Kampagnenkarte die Einkaufsanfragen für alle Kreditorenzeilen. Das Modul fragt zur Sicherheit nach und meldet anschließend den Erfolg.

Die Verarbeitung erfolgt in dieser Reihenfolge:
1. Pro Kreditorenzeile wird geprüft, ob eine Kreditor Nr. vorhanden ist.
2. Zu jeder Kreditorenzeile müssen noch unverarbeitete Artikelzeilen vorhanden sein.
3. Für jede gültige Kreditorenzeile wird eine Einkaufsanfrage angelegt.
4. Die Kopfdaten Lagerortcode, Einkäufercode und Kampagnennummer werden in die Einkaufsanfrage übernommen.
5. Anschließend werden die Artikelzeilen mit Artikel, Variante, Menge, Wareneingangsdatum, Einheit und Lagerort in die Einkaufsanfrage geschrieben.
6. Kreditoren- und Artikelzeilen erhalten danach die Belegart **Einkaufsanfrage** und die passende Beleg-Nr.

Alternativ erstellen Sie Einkaufsanfragen gezielt für einzelne Kreditoren: Markieren Sie im Bereich **Kreditoren** die gewünschten Zeilen und führen Sie die Aktion **Einkaufsanfragen erstellen** aus. Dann verarbeitet das Modul nur die markierten Kreditorenzeilen.

Typische Gründe, warum keine Einkaufsanfrage erzeugt wird:

| Frage | Antwort |
| --- | --- |
| Warum wird für eine Kreditorenzeile keine Einkaufsanfrage erzeugt? | Weil die Kreditor Nr. leer ist oder für diese Kreditorenzeile keine unverarbeiteten Artikelzeilen vorhanden sind. |
| Warum bleibt eine Artikelzeile ohne Einkaufsanfrage? | Weil die Menge 0 ist oder die Zeile bereits verarbeitet wurde. |

### Änderungen nach der Erzeugung von Einkaufsanfragen
Solange eine Artikelzeile an eine Einkaufsanfrage gebunden ist, werden Änderungen an der Kampagnenartikelzeile mit der Einkaufsanfrage synchronisiert. Besonders Mengen-, Preis- und Terminänderungen werden in die bestehende Einkaufsanfragezeile zurückgeschrieben.

Umgekehrt kann das Modul neue Artikelzeilen, die direkt auf der Einkaufsanfrage erfasst werden, wieder als Kampagnenartikelzeilen anlegen, sofern die Einkaufsanfrage mit einer Kampagne und einer Kreditorenzeile verknüpft ist und die Kampagne den Status Offen hat.

Bei verknüpften Einkaufsanfragen sperrt das Modul zudem bestimmte Felder gegen Direktänderung. Versuchen Sie etwa, im Kopf oder in der Zeile der Einkaufsanfrage Kreditor, Artikel, Menge, Einheit, Variante oder Lagerortcode zu ändern, weist das Modul mit einer Meldung darauf hin, dass das Feld aus der Kampagne stammt. Pflegen Sie diese Werte stattdessen in der Kampagne.

### Aus Einkaufsanfragen Einkaufsbestellungen erzeugen
Nach der Lieferantenauswahl oder nach der Prüfung einzelner Artikelzeilen können Sie Einkaufsbestellungen erzeugen.

Es gibt zwei fachliche Wege:
1. Über markierte Kreditorenzeilen mit der Aktion **Einkaufsbestellung(en) erstellen**. Dabei werden alle passenden Artikelzeilen des jeweiligen Kreditors in Einkaufsbestellungen übertragen.
2. Über markierte Artikelzeilen mit der Aktion **Einkaufsbestellung erstellen**. Dabei werden nur die ausgewählten Positionen weitergeführt; nicht markierte Positionen derselben Einkaufsanfrage werden vor der Umwandlung entfernt.

Voraussetzung ist immer, dass den Zeilen bereits Einkaufsanfragen zugeordnet sind. Sind keine gültigen Zeilen mit Einkaufsanfrage vorhanden, meldet das Modul einen Fehler.

Bei der Umwandlung geschieht Folgendes:
1. Das Modul liest alle betroffenen Einkaufsanfragen.
2. Die Standardfunktion zur Umwandlung von Einkaufsanfrage in Bestellung wird aufgerufen.
3. Danach werden Kreditoren- und Artikelzeilen von **Einkaufsanfrage** auf **Einkaufsbestellung** umgestellt.
4. Anschließend prüft das Modul, ob die Kampagne abgeschlossen werden kann, sofern keine offenen Restzeilen verbleiben.

### Einkaufsanfragen freigeben und zurücksetzen
Im Bereich **Kreditoren** können Sie die zu einer Zeile erzeugte Einkaufsanfrage direkt freigeben oder wieder öffnen, ohne die Anfrage einzeln aufrufen zu müssen.

| Aktion | Erläuterung |
| --- | --- |
| Freigeben | Verfügbar, wenn die Zeile auf eine Einkaufsanfrage im Status Offen verweist. Setzt die Einkaufsanfrage über die Standardfreigabe auf Freigegeben. |
| Status zurücksetzen | Verfügbar, wenn die verknüpfte Einkaufsanfrage freigegeben ist. Öffnet sie wieder zur Bearbeitung. |

### Kampagne kopieren
Wenn Sie auf Basis einer bestehenden Kampagne erneut anfragen möchten, kopieren Sie die Kampagne über die Aktion **Kampagne kopieren**. Dabei werden Beschreibung, Lagerortcode, Einkäufercode und die vorhandene Kreditoren- und Artikelstruktur in eine neue Kampagne übernommen, jedoch ohne die Belegverknüpfungen. Die neue Kampagne erhält eine eigene Nummer; auf Wunsch öffnet das Modul die neue Karte direkt.

### Status steuern
Der Status einer Kampagne wird über die Aktionen **Freigeben**, **Status zurücksetzen** und **Abschließen** geführt.

| Status | Bedeutung |
| --- | --- |
| Offen | Die Kampagne ist bearbeitbar. In diesem Status können Zeilen gepflegt und Einkaufsanfragen erzeugt werden. Über **Freigeben** wechseln Sie in den Status Freigegeben. |
| Freigegeben | Die Kampagne ist für die weitere Bearbeitung freigegeben. Über **Status zurücksetzen** gelangen Sie zurück nach Offen, um Änderungen vorzunehmen; aus diesem Status heraus kann die Kampagne über **Abschließen** beendet werden. |
| Beendet | Die Kampagne ist abgeschlossen und dient nur noch der Nachverfolgung. |

Die Aktion **Freigeben** ist nur im Status Offen aktiv, **Status zurücksetzen** und **Abschließen** nur im Status Freigegeben. Eine Kampagne kann nur beendet werden, wenn alle erforderlichen Kreditoren- und Artikelzeilen bereits in Einkaufsanfragen oder Einkaufsbestellungen überführt wurden. Verbleiben unverarbeitete Zeilen, lässt das Modul den Abschluss nicht zu und meldet einen Fehler.

## Arbeiten in verbundenen Belegen
### Verkaufsangebot, Verkaufsauftrag und Rahmenauftrag
Auf Verkaufsangeboten, Verkaufsaufträgen und Rahmenaufträgen ergänzt das Modul im Inforegister **Allgemein** das Feld **Einkaufskampagne Nr.** sowie das Infobox-Element mit den zugehörigen Einkaufsanfragen. Über die Aktion **Einkaufskampagne erstellen** legen Sie direkt eine neue Kampagne an.

Der Ablauf ist dabei immer gleich:
1. Öffnen Sie den Verkaufsbeleg.
2. Starten Sie die Aktion **Einkaufskampagne erstellen**.
3. Das Modul prüft, ob bereits eine Kampagne vorhanden ist, und öffnet auf Wunsch die bestehende.
4. Falls noch keine Kampagne existiert, wird eine neue Kampagne angelegt und mit dem Beleg verknüpft.
5. Die Artikelzeilen des Belegs werden als Kampagnenartikel übernommen.

Über das Feld **Einkaufskampagne Nr.** springen Sie per Drilldown jederzeit auf die zugehörige Kampagnenkarte.

### Einkaufsbestellung
Auch auf Einkaufsbestellungen stehen das Feld **Einkaufskampagne Nr.**, die Infobox und die Aktion **Einkaufskampagne erstellen** zur Verfügung. In diesem Fall dient die Einkaufsbestellung als Quelle der Artikelzeilen. Wird die Bestellung später gelöscht, löst das Modul die Kampagnenverknüpfung wieder aus dem Beleg.

### Einkaufsanfrage
Die Karte **Einkaufsanfrage** zeigt im Inforegister **Allgemein** das Feld **Einkaufskampagne Nr.**, in der Zeile (Unterseite) zusätzlich die **Kampagnen Nr.**. Über den Drilldown gelangen Sie auf die Kampagnenkarte. So erkennen Sie auf der Anfrage sofort, aus welcher Kampagne sie stammt.

### Bestellungsarbeitsblatt
Im **Bestellungsarbeitsblatt** kann eine Kampagne zu einer einzelnen Zeile oder zu mehreren markierten Zeilen entstehen. Die Kampagne speichert dazu Arbeitsblattvorlage, Artikelbuchblattname und Zeilennummer; das eingeblendete Feld **Kampagnen Nr.** zeigt die bereits verknüpfte Kampagne der aktuellen Zeile an.

Das Arbeitsblatt stellt dafür mehrere Aktionen bereit:

| Aktion | Erläuterung |
| --- | --- |
| Einkaufskampagne erstellen | Erzeugt aus den markierten Zeilen eine Einkaufsanfragenkampagne und übernimmt die Artikelzeilen. |
| zu Einkaufsanfrage hinzufügen | Fügt die markierten Zeilen (mit akzeptierter Aktionsmeldung) zu einer vorhandenen, offenen Einkaufsanfrage desselben Kreditors hinzu. |
| zu Einkaufsbestellung hinzufügen | Fügt die markierten Zeilen zu einer vorhandenen, offenen Einkaufsbestellung desselben Kreditors hinzu. |
| neue Anfrage erzeugen | Erstellt aus den markierten Zeilen eine neue Einkaufsanfrage und bietet an, sie direkt zu öffnen. |
| neue Bestellung erzeugen | Erstellt aus den markierten Zeilen eine neue Einkaufsbestellung und bietet an, sie direkt zu öffnen. |

Bei den Aktionen zum Hinzufügen oder Erzeugen von Belegen müssen alle markierten Arbeitsblattzeilen denselben Kreditor tragen; andernfalls meldet das Modul, dass die Kreditorennummer in allen Zeilen gleich sein muss.

Damit eignet sich das Modul besonders für folgende Situation:
1. Bedarf wird zuerst im Bestellungsarbeitsblatt gesammelt.
2. Daraus entsteht eine Einkaufsanfragenkampagne.
3. Die Artikelzeilen der ausgewählten Arbeitsblattzeilen werden in die Kampagne übernommen.
4. Danach erzeugen Sie aus der Kampagne die Einkaufsanfragen.

## Einkaufsanfragen, Bestellungen, Druck und E-Mail
### Belege öffnen
Sobald für eine Kreditoren- oder Artikelzeile eine Beleg-Nr. vorhanden ist, öffnen Sie darüber per Drilldown direkt die zugehörige Einkaufsanfrage oder Einkaufsbestellung. Das Modul führt je nach Belegart auf die passende Karte.

### Drucken
Aus einer Kampagne heraus drucken Sie über die Aktion **Drucken** alle zugeordneten Einkaufsanfragen gesammelt. Dafür markiert das Modul alle Einkaufsanfragen der Kampagne und startet den in Business Central über die Berichtsauswahl für Kreditorenbelege hinterlegten Druck. Sind keine Einkaufsanfragen vorhanden, meldet das Modul dies.

### E-Mail senden
Ebenso versenden Sie die zugeordneten Einkaufsanfragen über die Aktion **E-Mail senden** gesammelt per E-Mail. Das Modul markiert die Einkaufsanfragen der Kampagne und verwendet die Standardfunktion zum Senden der Belege.

### Verhalten nach dem Buchen einer Einkaufsbestellung
Wenn eine aus der Kampagne entstandene Einkaufsbestellung gebucht wird, entfernt das Modul die Belegverknüpfungen auf Kreditoren- und Artikelzeilen wieder. Die Kampagne bleibt zur Nachverfolgung erhalten, aber die konkrete Bestellverbindung der Zeilen wird geleert.

## Historie und Nachverfolgung
Die Nachverfolgung erfolgt vor allem über die Kampagnenkarte und die darin gespeicherten Beleginformationen.

| Bereich | Nutzen |
| --- | --- |
| Kampagnenliste | Überblick über alle Kampagnen und ihren Status, mit den Ansichten Offen, Freigegeben und Beendet. |
| Kreditorenzeilen | Nachweis, zu welchem Kreditor bereits eine Einkaufsanfrage oder Einkaufsbestellung besteht, inklusive Anfragenstatus. |
| Artikelzeilen | Nachweis, welche Position an welche Einkaufsanfrage- oder Bestellzeile gebunden war. |
| Verknüpfter Beleg | Rücksprung auf den Ursprungsbeleg, aus dem die Kampagne entstanden ist. |
| Infobox am Verkaufs-/Einkaufsbeleg | Zeigt die zur Kampagne gehörenden Einkaufsanfragen mit Nummer und Kreditor an. |

Eine eigene Archiv- oder Protokollseite ist im Modul nicht erkennbar. Die Nachverfolgung läuft daher über Status, Belegverknüpfungen und die Standardhistorie der erzeugten Einkaufs- und Verkaufsbelege.

## FAQ und Troubleshooting
### 1. Warum kann ich keine neue Kampagne speichern?
Weil in der Einkaufs- & Kreditoren Einrichtung keine Nummernserie für Einkaufsanfragenkampagnen hinterlegt ist.

### 2. Warum wird beim Ursprungsbeleg keine neue Kampagne erzeugt?
Weil für diesen Beleg bereits eine Kampagne existiert. Das Modul erkennt die vorhandene Verknüpfung und öffnet auf Wunsch die bestehende Kampagne.

### 3. Warum fehlt bei einer Kreditorenzeile die Einkaufsanfrage?
Weil die Kreditor Nr. leer ist oder keine unverarbeiteten Artikelzeilen zu dieser Kreditorenzeile existieren.

### 4. Warum erscheint beim Erstellen der Einkaufsanfragen eine Fehlermeldung zu Artikelzeilen?
Weil mindestens eine Artikelzeile eine Menge von 0 hat; solche Zeilen werden nicht in die Einkaufsanfrage übernommen.

### 5. Warum kann ich die Kampagne nicht beenden?
Weil noch Kreditoren- oder Artikelzeilen vorhanden sind, die nicht vollständig in Einkaufsanfragen oder Einkaufsbestellungen überführt wurden, oder weil die Kampagne nicht im Status Freigegeben ist.

### 6. Warum springt die Beleg-Nr. auf eine Einkaufsanfrage und nicht auf eine Einkaufsbestellung?
Weil die Zeile bislang nur bis zur Einkaufsanfrage verarbeitet wurde. Erst nach der Umwandlung wird die Belegart auf Einkaufsbestellung umgestellt.

### 7. Warum ändern sich Werte in der Einkaufsanfrage, wenn ich die Kampagnenzeile ändere?
Weil das Modul Änderungen an bereits verknüpften Kampagnenartikelzeilen zurück in die Einkaufsanfrage synchronisiert.

### 8. Warum kann ich bestimmte Felder in der Einkaufsanfrage nicht mehr ändern?
Weil die Einkaufsanfrage mit einer Kampagne verknüpft ist. Das Modul sperrt Änderungen an Feldern wie Kreditor, Artikel, Menge, Einheit, Variante und Lagerortcode, damit Kampagne und Beleg konsistent bleiben.

### 9. Warum ist die Verknüpfung zu einer Einkaufsbestellung nach dem Buchen leer?
Weil das Modul die Belegverknüpfungen nach dem Buchen einer Einkaufsbestellung bewusst aus den Kampagnenzeilen entfernt.

### 10. Warum steht im Bestellungsarbeitsblatt bereits eine Kampagnen Nr.?
Weil das Modul eine Kampagne zu genau dieser Arbeitsblattzeile anhand von Arbeitsblattvorlage, Artikelbuchblattname und Zeilennummer gefunden hat.

## Typische Anwendungsfälle
### Verkaufsangebot in Lieferantenanfragen überführen
**Auslöser:** Der Vertrieb hat ein Verkaufsangebot mit mehreren Artikelpositionen angelegt, für die aktuelle Einkaufspreise benötigt werden.

**Einstieg in BC:** Öffnen Sie das **Verkaufsangebot** und starten Sie dort die Aktion **Einkaufskampagne erstellen**.

**Kernablauf:**
1. Das Modul erzeugt eine neue Kampagne und verknüpft sie mit dem Verkaufsangebot.
2. Die Artikelzeilen des Angebots werden in die Kampagne übernommen.
3. Ergänzen Sie auf der Kampagnenkarte im Bereich **Kreditoren** die gewünschten Lieferanten.
4. Führen Sie die Aktion **Einkaufsanfrage erstellen** aus.
5. Öffnen Sie die erzeugten Einkaufsanfragen über die Beleg-Nr. und prüfen Sie EK-Preise, Mengen und Wareneingangsdaten.

**Abschluss:** Drucken oder versenden Sie die Einkaufsanfragen direkt aus der Kampagne über **Drucken** oder **E-Mail senden**.

### Bedarf aus dem Bestellungsarbeitsblatt bündeln
**Auslöser:** Die Disposition hat im Bestellungsarbeitsblatt mehrere Bedarfszeilen aufgebaut, die gemeinsam am Markt angefragt werden sollen.

**Einstieg in BC:** Öffnen Sie das **Bestellungsarbeitsblatt**.

**Kernablauf:**
1. Markieren Sie die gewünschten Zeilen und führen Sie **Einkaufskampagne erstellen** aus.
2. Das Modul speichert Arbeitsblattvorlage, Artikelbuchblattname und Zeilenbezug in der Kampagne.
3. Prüfen Sie die automatisch übernommenen Artikelzeilen.
4. Ergänzen Sie im Bereich **Kreditoren** die anzufragenden Lieferanten.
5. Führen Sie **Einkaufsanfrage erstellen** aus.

**Abschluss:** Über das Feld **Kampagnen Nr.** im Bestellungsarbeitsblatt wechseln Sie später jederzeit wieder auf die Kampagne.

### Vorliegende Einkaufsanfragen in Einkaufsbestellungen umwandeln
**Auslöser:** Ein oder mehrere Lieferanten haben auf die Einkaufsanfrage reagiert und die Anfrage soll in eine Einkaufsbestellung überführt werden.

**Einstieg in BC:** Öffnen Sie die **Einkaufsanfragenkampagne**.

**Kernablauf:**
1. Markieren Sie im Bereich **Kreditoren** die betroffenen Zeilen oder im Bereich **Artikel** gezielt einzelne Positionen.
2. Starten Sie **Einkaufsbestellung(en) erstellen** (Kreditorenzeilen) bzw. **Einkaufsbestellung erstellen** (Artikelzeilen).
3. Das Modul wandelt die zugehörigen Einkaufsanfragen in Einkaufsbestellungen um.
4. Kreditoren- und Artikelzeilen werden auf die Belegart Einkaufsbestellung umgestellt.
5. Prüfen Sie die erzeugten Einkaufsbestellungen über die Beleg-Nr.

**Abschluss:** Beenden Sie anschließend die Kampagne über **Abschließen**, sofern keine offenen Restzeilen mehr vorhanden sind.

### Bestehende Kampagne für eine Folgeanfrage wiederverwenden
**Auslöser:** Eine bereits abgewickelte Anfragesituation soll mit ähnlichen Daten erneut durchgeführt werden.

**Einstieg in BC:** Öffnen Sie die bestehende **Einkaufsanfragenkampagne**.

**Kernablauf:**
1. Nutzen Sie die Aktion **Kampagne kopieren**.
2. Öffnen Sie auf Wunsch direkt die neu angelegte Kampagne.
3. Passen Sie Lieferanten, Mengen, EK-Preise oder Termine an.
4. Führen Sie **Einkaufsanfrage erstellen** aus.

**Abschluss:** Die alte Kampagne bleibt erhalten, die neue Kampagne besitzt eine eigene Nummer und eigene Belegverknüpfungen.
