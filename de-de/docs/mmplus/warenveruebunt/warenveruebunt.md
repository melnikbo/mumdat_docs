---
title: Anwenderhandbuch m+m Goods Receipt with Logistic Differences
---

# Anwenderhandbuch m+m Goods Receipt with Logistic Differences

## Einleitung

Dieses Handbuch richtet sich an die **operativen Anwenderinnen und Anwender in der Warenvereinnahmung und im Einkauf**, die eingehende Ware im Modul **m+m Warenvereinnahmung** erfassen und buchen. Sekundäre Zielgruppe sind Administratorinnen und Administratoren, die die Berechtigungen und die Regeln für Unterlieferungen einrichten.

Die Erweiterung **m+m Goods Receipt with Logistic Differences** verbindet zwei bestehende Module: die **m+m Warenvereinnahmung** (Erfassung und Buchung von Wareneingängen aus Warenbestellungen) und die **m+m Über-/Unterlieferung** (Regeln für Über- und Unterlieferungen). Sie fügt der Zeile einer **Warenbestellung** genau ein zusätzliches Kennzeichen hinzu: **Beleg komplett**.

Mit diesem Kennzeichen lösen Sie einen häufigen logistischen Fall: Ein Lieferant liefert **weniger** als bestellt und wird die Restmenge **nicht** mehr nachliefern. Ohne die Erweiterung bliebe die Bestellung mit einer offenen Restmenge stehen. Setzen Sie dagegen auf der betroffenen Zeile **Beleg komplett** und tragen Sie die tatsächlich gelieferte **Menge** ein, so wird beim Verarbeiten der **Warenbestellung** die Menge der zugrunde liegenden Einkaufsbestellzeile auf die gelieferte Menge reduziert und die Bestellung trotz der Differenz geschlossen. Die logistische Mengenlücke ist damit ausgeglichen.

**Kurzer Prozessüberblick**

1. Der Anwender öffnet die betroffene **Warenbestellung** und wählt die zu buchende Zeile.
2. Er trägt die tatsächlich gelieferte **Menge** ein und setzt bei einer endgültigen Unterlieferung das Kennzeichen **Beleg komplett**.
3. Er startet die Aktion **Warenbestellung verarbeiten**.
4. Die Erweiterung reduziert die Menge der Einkaufsbestellzeile auf die gelieferte Menge, überträgt das Kennzeichen **Beleg komplett** und der Wareneingang wird gebucht; die Bestellung ist geschlossen.

## Schnellstart für Anwender

Voraussetzung: In der Einrichtung **Über-/Unterlieferung** ist die **Unterlieferung** für den Einkauf zugelassen (siehe Kapitel *Einrichtung*), Sie besitzen die Berechtigung **MuM GROS All** und die zugehörige Einkaufsbestellung ist **Freigegeben**.

Endgültige Unterlieferung buchen (minimaler Weg):

1. Öffnen Sie über **Suchen** die Liste **Warenbestellungen** und öffnen Sie die betroffene **Warenbestellung** über die Zeile (Doppelklick).
2. Wählen Sie im Inforegister **Zeilen** die Zeile des unterlieferten Artikels.
3. Tragen Sie in **Menge** die tatsächlich gelieferte Menge ein (kleiner als die bestellte Menge).
4. Setzen Sie in derselben Zeile das Kennzeichen **Beleg komplett**.
5. Wählen Sie die Aktion **Warenbestellung verarbeiten**.

Nach dem Verarbeiten ist der Wareneingang mit der gelieferten Menge gebucht und die Einkaufsbestellzeile geschlossen. Für eine **vollständige** Lieferung lassen Sie **Beleg komplett** leer und verarbeiten die **Warenbestellung** wie gewohnt.

## Einrichtung

Die Erweiterung selbst bringt **keine eigene Einrichtungsseite** mit. Damit das Kennzeichen **Beleg komplett** wirkt, müssen jedoch drei Voraussetzungen aus den Basismodulen erfüllt sein. Diese werden hier in Abhängigkeitsreihenfolge beschrieben, damit eine Administratorin oder ein Administrator die Funktion vollständig aktivieren kann.

### Unterlieferung mit Belegabschluss einrichten

**Prozessintro.** Diese Einrichtung nimmt eine Administratorin oder ein Administrator **einmalig vor der ersten Nutzung** vor. Sie legt fest, ob im Einkauf eine Unterlieferung überhaupt zulässig ist. Erst dann kann ein Anwender in der täglichen Arbeit auf der Zeile der **Warenbestellung** das Kennzeichen **Beleg komplett** setzen. Das Ergebnis dieser Einrichtung wird im Kapitel *Tägliche Arbeit am Beleg Warenbestellung* angewendet.

**Ablauf in Abhängigkeitsreihenfolge**

1. **Zuerst** öffnen Sie über **Suchen** die Einrichtungsseite der **Über-/Unterlieferung** (Basismodul m+m Über-/Unterlieferung) und aktivieren Sie die Kontrolle für den **Einkauf**. Wenn der Einkauf aktiviert ist, dann greifen die Regeln für Über- und Unterlieferung in Wareneingangs- und Einkaufsprozessen; ohne diese Aktivierung ist keine kontrollierte Unterlieferung und damit auch kein Belegabschluss über **Beleg komplett** möglich.

2. **Danach** definieren Sie für die **Unterlieferung** die Kontrollmethode und den zulässigen Rahmen. Die folgenden Einstellungen stammen aus der Basiseinrichtung **Über-/Unterlieferung** und sind für das Kennzeichen **Beleg komplett** maßgeblich:

| Einrichtung | Erläuterung |
|-------------|-------------|
| Einkauf | Wenn aktiviert, dann werden Unterlieferungen im Einkauf kontrolliert und das Kennzeichen **Beleg komplett** kann auf der Zeile gesetzt werden; ist die Einstellung leer, bleibt jede Zeile bis zur vollständigen Lieferung offen und **Beleg komplett** greift nicht. |
| Kontrolltyp Unterlieferung | Wenn für die Unterlieferung ein Kontrolltyp gesetzt ist, dann prüft das System beim Setzen von **Beleg komplett**, ob die gelieferte Menge innerhalb des erlaubten Rahmens liegt; andernfalls wird der Vorgang abgewiesen oder gewarnt. |
| Kontrollmethode | Bestimmt, wie der zulässige Unterlieferungsrahmen berechnet wird. **Vorgabe:** Es gilt das Standardverhalten von Business Central. **Prozentsatz:** Der zulässige Rahmen ergibt sich aus einem Prozentsatz der ursprünglichen Menge. **Absoluter Wert:** Der zulässige Rahmen ergibt sich aus einem festen Mengenwert. |
| Kontrollwert | Wenn ein Kontrollwert hinterlegt ist, dann begrenzt dieser die zulässige Abweichung (als Prozentsatz oder als absoluter Wert je nach Kontrollmethode); erst innerhalb dieses Werts ist eine Unterlieferung mit **Beleg komplett** erlaubt. |
| Warnung | Wenn die Warnung aktiviert ist, dann kann der Anwender die Unterlieferung nach einer Rückfrage dennoch bestätigen und **Beleg komplett** auch außerhalb des sonst starren Rahmens setzen; ist die Warnung deaktiviert, wird eine unzulässige Unterlieferung mit einer Fehlermeldung verhindert. |

> Diese Seite gehört zum Basismodul **m+m Über-/Unterlieferung**. Weitere Felder dieser Einrichtung (z. B. artikelbezogene Regeln, Vorgaben je Kreditor) sind für den Belegabschluss über **Beleg komplett** nicht erforderlich und werden im Handbuch des Basismoduls beschrieben; für die vorliegende Erweiterung genügen die oben genannten Felder.

3. **Anschließend** stellen Sie sicher, dass die Anwender die Berechtigung **MuM GROS All** besitzen (siehe *Berechtigungen*) und dass eine gültige Lizenz vorliegt (siehe *Lizenz*).

**Operativer Abschluss.** Sind diese Schritte erfüllt, wird die Funktion in der täglichen Arbeit durch die Aktion **Warenbestellung verarbeiten** ausgelöst, sobald auf der Zeile **Beleg komplett** gesetzt und eine gegenüber der Bestellung geringere **Menge** eingetragen ist (Querverweis: *Tägliche Arbeit am Beleg Warenbestellung*).

### Berechtigungen

Die Erweiterung liefert den zuweisbaren Berechtigungssatz **MuM GROS All** aus. Er bestimmt die Berechtigungen für die Ausführung der zugehörigen Verarbeitungslogik.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Berechtigungssatz **MuM GROS All** | Wenn dieser Berechtigungssatz einem Benutzer oder einer Benutzergruppe zugewiesen ist, dann darf dieser Benutzer die Verarbeitung ausführen, bei der das Kennzeichen **Beleg komplett** beim Buchen ausgewertet wird; ohne diese Berechtigung wird die Zeilenmenge beim Verarbeiten nicht automatisch angepasst. Der Berechtigungssatz legt fest, welche Aktionen der Anwender im Rahmen dieser Erweiterung ausführen darf. |

### Lizenz

Beim Anmelden prüft die Erweiterung einmalig, ob für die installierte App eine gültige Lizenz vorliegt.

| Einrichtung | Erläuterung |
|-------------|-------------|
| Gültige Lizenz der App | Wenn eine gültige Lizenz vorliegt, dann steht die Funktion **Beleg komplett** beim Verarbeiten der **Warenbestellung** zur Verfügung; ohne gültige Lizenz kann die Verarbeitungslogik nicht ausgeführt werden. Diese Prüfung erfolgt automatisch im Hintergrund und erfordert keine Eingabe des Anwenders. |

## Tägliche Arbeit am Beleg Warenbestellung

Diese Erweiterung wird ausschließlich beim Bearbeiten des Belegs **Warenbestellung** wirksam. Das Verhalten wird durch die Einrichtung **Über-/Unterlieferung** gesteuert (Querverweis: *Unterlieferung mit Belegabschluss einrichten*): Nur wenn dort die Unterlieferung für den Einkauf zugelassen ist, kann das Kennzeichen **Beleg komplett** auf der Zeile gesetzt werden.

**Einstieg:** Öffnen Sie über **Suchen** die Liste **Warenbestellungen** und öffnen Sie über die gewünschte Zeile die einzelne **Warenbestellung**. Die Liste dient nur der Navigation; sie zeigt je Beleg die Spalten **Nr.**, **Status**, **Belegdatum** und das Eingangsdatum.

### Belegkopf der Warenbestellung

Der Kopf der **Warenbestellung** identifiziert Lieferant und Beleg. Für den Belegabschluss über **Beleg komplett** ist vor allem der **Status** entscheidend.

| Feld | Erläuterung |
|------|-------------|
| Nr. | Eindeutige Belegnummer der **Warenbestellung**; sie identifiziert den Beleg in Liste und Historie. |
| Eink. von Kred.-Nr. | Wenn hier der Kreditor eingetragen ist, dann bezieht das System Lieferant und zugehörige Vorgaben auf diesen Kreditor; ohne Kreditor kann keine Zeile verarbeitet werden. |
| Eink. von Name | Zeigt den Namen des unter **Eink. von Kred.-Nr.** gewählten Kreditors zur Kontrolle an. |
| Belegdatum | Belegdatum der **Warenbestellung**; es dient der Zuordnung und Auswertung des Belegs. |
| Status | Steuert, welche Aktionen möglich sind. **Offen:** Beleg in Bearbeitung, Zeilen können geändert werden, noch keine Verarbeitung. **In Bearbeitung:** Beleg befindet sich in einem Zwischenstand der Bearbeitung. **Freigegeben:** Beleg ist freigegeben und kann verarbeitet werden. Die zugrunde liegende Einkaufsbestellung muss beim Verarbeiten ebenfalls **Freigegeben** sein, sonst wird die Verarbeitung abgewiesen. |
| Wareneingangslagerortcode | Wenn ein Wareneingangslagerort hinterlegt ist, dann werden die Zeilen standardmäßig auf diesen Lagerort vereinnahmt; er bestimmt, wohin die gelieferte Menge gebucht wird. |

> Die weiteren Kopfbereiche (Lieferadresse, Anlage- und Änderungsinformationen, externe Lieferscheindaten) stammen aus dem Basismodul und beeinflussen das Kennzeichen **Beleg komplett** nicht; sie sind für den hier beschriebenen Ablauf nicht erforderlich.

### Zeilen der Warenbestellung

Auf dem Inforegister **Zeilen** erfassen Sie Artikel und Mengen des Wareneingangs. Diese Erweiterung ergänzt die Zeile um die letzte Spalte **Beleg komplett**. Der Anwender sieht Basisfelder und Erweiterungsfeld auf **einer** Maske; deshalb sind hier beide zusammen dokumentiert.

| Feld | Erläuterung |
|------|-------------|
| Artikelnr. | Wenn Sie hier den Artikel wählen, dann übernimmt das System Beschreibung und Einheit aus der Artikelkarte; die Zeile bezieht sich auf diesen Artikel. |
| Artikelreferenznr. | Wenn eine Artikelreferenz (z. B. Lieferantenartikelnummer) eingetragen ist, dann wird der zugehörige Artikel automatisch ermittelt; das erleichtert die Erfassung anhand der Belege des Lieferanten. |
| Beschreibung | Zeigt die Bezeichnung des Artikels an; sie kann zur Kontrolle angepasst werden. |
| Beschreibung 2 | Zusätzliche Bezeichnungszeile des Artikels für ergänzende Angaben. |
| Menge | Tragen Sie hier die tatsächlich gelieferte Menge ein. Wenn die eingetragene Menge kleiner ist als die bestellte Menge und **Beleg komplett** gesetzt ist, dann wird beim Verarbeiten die Menge der Einkaufsbestellzeile auf diese Menge reduziert und die Bestellung geschlossen. |
| Einheitencode | Bestimmt die Maßeinheit der eingetragenen **Menge**; ein Wechsel der Einheit rechnet die Basismenge entsprechend um. |
| Variantencode | Wenn der Artikel mit Varianten geführt wird, dann legt der Variantencode fest, welche Variante vereinnahmt wird. |
| Wareneingangslagerortcode | Wenn ein Wareneingangslagerort gesetzt ist, dann wird die Menge dieser Zeile auf diesen Lagerort vereinnahmt. |
| Wareneingangslagerplatzcode | Wenn der Lagerort lagerplatzpflichtig ist, dann bestimmt der Lagerplatzcode den genauen Lagerplatz der Vereinnahmung. |
| **Beleg komplett** | Setzen Sie dieses Kennzeichen, wenn die tatsächlich gelieferte **Menge** kleiner ist als die bestellte Menge und **keine** Restlieferung mehr erfolgt. Wenn das Kennzeichen gesetzt ist und die Menge unter der bestellten Menge liegt, dann reduziert das System beim Verarbeiten die Einkaufsbestellzeile auf die gelieferte Menge, überträgt das Kennzeichen auf die Einkaufsbestellzeile und schließt die Bestellung, sodass keine weiteren Wareneingänge mehr möglich sind. Ist das Kennzeichen **nicht** gesetzt (oder wurde die volle Menge geliefert), dann bleibt der Standardablauf unverändert und eine Restmenge bleibt offen. Das Kennzeichen kann nur im Rahmen der eingerichteten Unterlieferungsregeln gesetzt werden. |

> Die technischen Herkunftsspalten der Zeile (Herkunftsart, Herkunftsuntertyp, Herkunftsbeleg, Herkunftsnummer, Herkunftszeilennummer, Herkunftsunterzeilennummer) sind nicht editierbar und dienen nur der Rückverfolgung zur ursprünglichen Einkaufsbestellzeile. Sie werden vom System gefüllt und erfordern keine Eingabe.

### Zeilenaktion und Verarbeitung

Auf dem Beleg stehen die Statusaktionen der Gruppe **Status ändern** zur Verfügung (**Freigeben**, **Avisieren**, **In Bearbeitung**, **Status zurücksetzen**) sowie die Aktionen **Bestellzeilen abrufen** und **Warenbestellung verarbeiten**.

- **Bestellzeilen abrufen:** Öffnen Sie über die Aktion **Bestellzeilen abrufen** die Auswahl der offenen Einkaufsbestellzeilen, um Zeilen in die **Warenbestellung** zu übernehmen.
- **Warenbestellung verarbeiten:** Öffnen Sie über die Aktion **Warenbestellung verarbeiten** die Verarbeitung des Belegs. Dabei wird für jede Zeile geprüft, ob **Beleg komplett** gesetzt und die gelieferte **Menge** geringer ist als die bestellte Menge. Trifft dies zu, reduziert das System die Menge der Einkaufsbestellzeile auf die gelieferte Menge, überträgt **Beleg komplett** und bucht anschließend den Wareneingang.

**Buchungsablauf beim Belegabschluss**

1. Wählen Sie auf der **Warenbestellung** die unterlieferte Zeile.
2. Tragen Sie in **Menge** die gelieferte Menge ein und setzen Sie **Beleg komplett**.
3. Wählen Sie **Warenbestellung verarbeiten**.
4. Das System reduziert vor dem Buchen die Menge der Einkaufsbestellzeile auf die gelieferte Menge und setzt dort **Beleg komplett**.
5. Der Wareneingang wird gebucht; die Einkaufsbestellzeile ist geschlossen, es bleibt keine offene Restmenge.

## Typische Anwendungsfälle

### Anwendungsfall 1: Endgültige Unterlieferung abschließen

**Auslöser.** Ein Lieferant meldet telefonisch oder per E-Mail, dass er von 100 bestellten Stück nur 95 liefert und die restlichen 5 nicht mehr nachliefert.

**Einstieg in BC.** Der Anwender öffnet über **Suchen** die Liste **Warenbestellungen** und öffnet die betroffene **Warenbestellung**. Voraussetzung ist, dass die zugehörige Einkaufsbestellung den Status **Freigegeben** hat und die Unterlieferung im Einkauf eingerichtet ist.

**Kernablauf.**
1. Auf dem Inforegister **Zeilen** wählt der Anwender die Zeile des Artikels.
2. Er trägt in **Menge** die gelieferten 95 Stück ein.
3. Er setzt das Kennzeichen **Beleg komplett**, weil keine Restlieferung mehr erfolgt.
4. Er wählt die Aktion **Warenbestellung verarbeiten**.

**Abschluss.** Die Erweiterung reduziert die Einkaufsbestellzeile auf 95 Stück, überträgt **Beleg komplett** und der Wareneingang über 95 Stück wird gebucht. Die Bestellung ist geschlossen; es bleiben keine 5 Stück als offene Restmenge stehen.

### Anwendungsfall 2: Vollständige Lieferung ohne Kennzeichen

**Auslöser.** Eine Bestellung wird vollständig in der bestellten Menge geliefert.

**Einstieg in BC.** Der Anwender öffnet über **Suchen** die Liste **Warenbestellungen** und die betroffene **Warenbestellung**.

**Kernablauf.**
1. Der Anwender prüft auf dem Inforegister **Zeilen** die gelieferte **Menge**.
2. Er lässt **Beleg komplett** leer, da keine Unterlieferung vorliegt.
3. Er wählt **Warenbestellung verarbeiten**.

**Abschluss.** Da **Beleg komplett** nicht gesetzt ist, greift die Sonderlogik der Erweiterung nicht; der Wareneingang wird im Standardablauf über die volle Menge gebucht.

## FAQ und Troubleshooting

### 1. Wofür dient das Kennzeichen „Beleg komplett“?
Es schließt eine Bestellung trotz Unterlieferung ab. Wenn Sie es setzen und eine geringere **Menge** als bestellt buchen, reduziert das System die Einkaufsbestellzeile auf die gelieferte Menge und lässt keine weiteren Wareneingänge mehr zu.

### 2. Warum kann ich „Beleg komplett“ nicht setzen?
Das Kennzeichen ist nur im Rahmen der eingerichteten Unterlieferungsregeln zulässig. Prüfen Sie in der Einrichtung **Über-/Unterlieferung**, ob der **Einkauf** aktiviert und eine Unterlieferung zugelassen ist. Ohne diese Einrichtung greift das Kennzeichen nicht.

### 3. Was passiert, wenn ich „Beleg komplett“ setze, aber die volle Menge liefere?
Nichts Besonderes. Ist die gelieferte **Menge** nicht kleiner als die bestellte Menge, überspringt die Erweiterung ihre Sonderlogik und der Wareneingang wird im Standardablauf gebucht.

### 4. Was passiert, wenn ich „Beleg komplett“ nicht setze und weniger liefere?
Dann bleibt die Bestellung mit einer offenen Restmenge stehen. Es wird nur die gebuchte Teilmenge vereinnahmt; weitere Wareneingänge sind weiterhin möglich.

### 5. Muss die Einkaufsbestellung freigegeben sein?
Ja. Beim Verarbeiten prüft das System, dass die zugrunde liegende Einkaufsbestellung den Status **Freigegeben** hat. Ist sie nicht freigegeben, wird die Verarbeitung mit einer Fehlermeldung abgewiesen.

### 6. Wie starte ich die eigentliche Buchung?
Über die Aktion **Warenbestellung verarbeiten** auf dem Beleg. Diese Aktion prüft die Zeilen, wendet die Logik von **Beleg komplett** an und bucht den Wareneingang.

### 7. Wird meine erfasste Menge beim Abschluss verändert?
Die von Ihnen eingetragene **Menge** bleibt die gebuchte Wareneingangsmenge. Verändert wird die **Einkaufsbestellzeile**: Ihre Menge wird auf die gelieferte Menge reduziert, damit keine Restmenge offen bleibt.

### 8. Kann ich weiterhin in mehreren Teillieferungen vereinnahmen?
Ja. Solange Sie **Beleg komplett** nicht setzen, können Sie in mehreren Wareneingängen vereinnahmen. Erst wenn keine Restlieferung mehr kommt, setzen Sie beim letzten Eingang **Beleg komplett**.

### 9. Welche Berechtigung wird benötigt?
Der Berechtigungssatz **MuM GROS All** muss dem Anwender zugewiesen sein. Er bestimmt die Berechtigungen für die Ausführung der Verarbeitungslogik dieser Erweiterung.

### 10. Warum steht die Funktion nach der Installation nicht zur Verfügung?
Beim Anmelden wird eine gültige Lizenz der App geprüft. Fehlt eine gültige Lizenz, kann die Verarbeitungslogik nicht ausgeführt werden. Wenden Sie sich in diesem Fall an Ihre Administration.
