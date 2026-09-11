---
title: Anwenderhandbuch m+m Ext. Text Module with Production Order Job Overview
---

# Anwenderhandbuch m+m Ext. Text Module with Production Order Job Overview

## Einleitung

Die App **m+m Ext. Text Module with Production Order Job Overview** erweitert Microsoft Dynamics 365 Business Central um zusätzliche **InfoBoxen** (Factboxen) und eine Aktion in der Ansicht **FA-Arbeitsvorrat** (englischer Objektname *Prod. Order Job Overview*). Damit werden die im Modul **Erweitertes Textmodul** hinterlegten Texte einer Fertigung direkt am Arbeitsplatz sichtbar, ohne dass der Anwender in den Fertigungsauftrag oder in einzelne Belege wechseln muss.

Die App zeigt in drei InfoBoxen die erweiterten Texte

- der **Fertigung** (Kopftext des Fertigungsauftrags),
- der **Fertigungszeilen** (Zeilentext der Fertigungsauftragszeile) und
- der **Arbeitsgänge** (Text der Arbeitsgangzeile),

jeweils bezogen auf die im **FA-Arbeitsvorrat** markierte Arbeitsgangzeile eines **freigegebenen** Fertigungsauftrags. Zusätzlich öffnet die Aktion **Erweiteter Text Fertigung** die vollständige Textpflege zum ausgewählten Fertigungsauftrag.

**Zielgruppe:** Primär **operative Anwender** in der Fertigung — Werker, Arbeitsvorbereitung und Fertigungssteuerung, die im **FA-Arbeitsvorrat** täglich Arbeitsgänge abarbeiten und die hinterlegten Hinweise, Arbeitsanweisungen und Zusatzinformationen lesen müssen. Sekundär richtet sich das Handbuch an **Administratoren** und **Schlüsselanwender**, die die Voraussetzungen im Modul **Erweitertes Textmodul** und im Modul **FA-Arbeitsvorrat** einrichten.

**Kurzer Prozessüberblick:** Ein Schlüsselanwender pflegt die erweiterten Texte im Fertigungsauftrag (Kopf, Zeile, Arbeitsgang) über das **Erweiterte Textmodul**. Der operative Anwender öffnet anschließend den **FA-Arbeitsvorrat**, filtert auf seinen **Arbeitsplatz** bzw. seine **Arbeitsplatzgruppe**, markiert eine Arbeitsgangzeile und liest die Texte in den drei InfoBoxen. Bei Bedarf öffnet er über **Erweiteter Text Fertigung** die vollständige Textansicht.

> Diese App fügt der Ansicht **FA-Arbeitsvorrat** ausschließlich Anzeige- und Textpflegefunktionen hinzu. Sie enthält keine eigenen Buchungs-, Freigabe- oder Lagerprozesse. Die Erfassung der Texte selbst erfolgt über das abhängige Modul **Erweitertes Textmodul**.

## Schnellstart für Anwender

Der schnellste Weg zu den erweiterten Texten im **FA-Arbeitsvorrat**:

1. **Voraussetzung (Administrator/Schlüsselanwender):** Die erweiterten Texte müssen im Fertigungsauftrag vorhanden sein. Sie werden über das Modul **Erweitertes Textmodul** an Kopf, Zeile und Arbeitsgang erfasst (siehe Kapitel **Voraussetzungen und Einrichtung**).
2. **FA-Arbeitsvorrat öffnen:** Rufen Sie über **Suchen** die Ansicht **FA-Arbeitsvorrat** auf.
3. **Arbeitsplatzgruppe wählen:** Setzen Sie im Filter **Arbeitsplatzgruppennr.** die gewünschte Arbeitsplatzgruppe.
4. **Arbeitsplatz wählen (optional):** Grenzen Sie die Anzeige mit dem Filter **Arbeitsplatznr.** auf einen einzelnen Arbeitsplatz ein. Dieser Schritt ist optional.
5. **Arbeitsgangzeile markieren:** Wählen Sie in der Liste die abzuarbeitende Arbeitsgangzeile aus.
6. **Texte lesen:** Lesen Sie die zur markierten Zeile passenden Texte in den drei InfoBoxen **Fertigungstext**, **Fertigungszeilentext** und **Arbeitsgangtext**.
7. **Vollständige Textansicht (optional):** Öffnen Sie über die Aktion **Erweiteter Text Fertigung** die komplette Textpflege zum Fertigungsauftrag.

## Voraussetzungen und Einrichtung

Diese App besitzt **keine eigenen Einrichtungsseiten**. Sie zeigt Daten an, die in zwei vorausgesetzten Modulen entstehen. Die Einrichtung erfolgt daher in dieser Reihenfolge (Abhängigkeitsreihenfolge):

1. **Modul FA-Arbeitsvorrat bereitstellen** — Die Ansicht **FA-Arbeitsvorrat** stammt aus dem Modul **m+m Production Order Job Overview**. Ohne dieses Modul steht die erweiterte Ansicht nicht zur Verfügung. Der Administrator stellt sicher, dass das Modul installiert und für die betroffenen Anwender berechtigt ist. **Wenn** das Modul bereitgestellt ist, **dann** ist die Ansicht **FA-Arbeitsvorrat** über **Suchen** erreichbar und kann auf Arbeitsplatzgruppe und Arbeitsplatz gefiltert werden.
2. **Modul Erweitertes Textmodul bereitstellen** — Die erweiterten Texte und die drei InfoBoxen sowie die vollständige Textansicht stammen aus dem Modul **m+m Ext. Text Module**. **Wenn** dieses Modul bereitgestellt ist, **dann** stehen die Textpflege am Fertigungsauftrag sowie die Anzeige der Texte in den InfoBoxen zur Verfügung.
3. **Berechtigungen vergeben** — Der Administrator ordnet den Anwendern die passenden Berechtigungssätze zu (siehe **Berechtigungen**).

### Berechtigungen

Die App liefert den Berechtigungssatz **All Ext. Text Module with Production Order Job Overview permissions** (interner Berechtigungssatz der App) aus. Dieser legt fest, welche Aktionen Anwender im Rahmen dieser App ausführen dürfen; er umfasst ausschließlich die Ausführungsberechtigung für die interne Verarbeitung dieser App. **Wenn** der Berechtigungssatz einem Anwender zugeordnet ist, **dann** kann dieser die von der App bereitgestellten InfoBoxen und die Aktion **Erweiteter Text Fertigung** nutzen. Die Berechtigungen zum Lesen und Pflegen der eigentlichen Texte sowie zum Aufruf des **FA-Arbeitsvorrats** ergeben sich zusätzlich aus den vorausgesetzten Modulen **Erweitertes Textmodul** und **FA-Arbeitsvorrat**.

> **Hinweis zur Textpflege:** Das *Erfassen* der erweiterten Texte am Fertigungsauftrag ist Bestandteil des Moduls **Erweitertes Textmodul**. Dieses Handbuch beschreibt, **wie** und **wo** diese Texte im **FA-Arbeitsvorrat** angezeigt und geöffnet werden. Die Detaileinrichtung des Erweiterten Textmoduls (z. B. Textvorlagen, Sprachversionen, Druck- und Berichtsparameter) entnehmen Sie dem Handbuch des Moduls **Erweitertes Textmodul**.

## Der FA-Arbeitsvorrat als Einstiegspunkt

Der **FA-Arbeitsvorrat** ist die zentrale Arbeitsansicht, in der diese App wirkt. Der Anwender ruft die Ansicht über **Suchen** auf und schränkt sie über die Kopf-Filter ein, bevor er eine Arbeitsgangzeile markiert.

### Einstieg und Filter

**Einstieg:** Über **Suchen** die Ansicht **FA-Arbeitsvorrat** öffnen.

Die Ansicht ist über zwei zusammengehörige Filterebenen gegliedert. Setzen Sie die **Arbeitsplatzgruppe** zuerst und grenzen Sie danach bei Bedarf auf einen einzelnen **Arbeitsplatz** ein.

| Filterfeld | Erläuterung |
| --- | --- |
| **Arbeitsplatzgruppennr.** | Wenn gesetzt, dann werden die angezeigten Arbeitsgangzeilen auf die gewählte Arbeitsplatzgruppe gefiltert; der Anwender sieht nur die Arbeitsgänge seines Verantwortungsbereichs. Dies ist der übergeordnete Filter und wird zuerst gesetzt. |
| **Arbeitsplatznr.** | Wenn gesetzt, dann werden die Zeilen zusätzlich auf einen einzelnen Arbeitsplatz innerhalb der Arbeitsplatzgruppe eingegrenzt. Dieser Filter ist optional und wird nach der Arbeitsplatzgruppe gesetzt; ohne Eingabe bleiben alle Arbeitsplätze der gewählten Gruppe sichtbar. |

Nach dem Filtern markiert der Anwender die abzuarbeitende Arbeitsgangzeile. Sämtliche von dieser App ergänzten InfoBoxen und die Aktion **Erweiteter Text Fertigung** beziehen sich immer auf die aktuell markierte Zeile.

## InfoBoxen mit erweiterten Texten

Diese App fügt dem **FA-Arbeitsvorrat** drei InfoBoxen hinzu. Alle drei beziehen sich auf **freigegebene** Fertigungsaufträge und aktualisieren ihren Inhalt automatisch, sobald der Anwender eine andere Arbeitsgangzeile markiert. Die InfoBoxen zeigen die Texte im Anzeigemodus **InfoBox** (Drucktyp der Anzeige) — dieselben Texte können im Erweiterten Textmodul zusätzlich für **Bericht** vorgesehen sein.

### InfoBox „Fertigungstext"

**Prozessbezug:** Diese InfoBox zeigt den erweiterten **Kopftext** des freigegebenen Fertigungsauftrags. Sie wird vom Schlüsselanwender am Fertigungsauftragskopf gepflegt und dient dem operativen Anwender als auftragsbezogene Gesamtinformation (z. B. übergreifende Fertigungshinweise).

Die InfoBox ist an die Kopfdaten des Fertigungsauftrags gebunden. Maßgeblich sind:

| Feld | Erläuterung |
| --- | --- |
| **Fertigungstext** | Zeigt den erweiterten Kopftext des Fertigungsauftrags an. Wenn zur markierten Zeile ein freigegebener Fertigungsauftrag mit hinterlegtem Kopftext existiert, dann erscheint dieser Text hier; ohne hinterlegten Text bleibt die InfoBox leer. |
| **FA-Nr.** (Prod. Order No.) | Bestimmt, zu welchem Fertigungsauftrag der Kopftext geladen wird. Wenn der Anwender eine Zeile markiert, dann wird die Fertigungsauftragsnummer der Zeile zur Auswahl des Kopftexts herangezogen. |

**Bezug zur markierten Zeile:** Es wird immer der Fertigungsauftrag zur **FA-Nr.** der aktuell markierten Arbeitsgangzeile geladen; der Belegstatus ist auf **Freigegeben** festgelegt.

### InfoBox „Fertigungszeilentext"

**Prozessbezug:** Diese InfoBox zeigt den erweiterten **Zeilentext** der Fertigungsauftragszeile. Sie ergänzt den Kopftext um zeilenspezifische Hinweise (z. B. zum konkret zu fertigenden Artikel).

| Feld | Erläuterung |
| --- | --- |
| **Fertigungszeilentext** | Zeigt den erweiterten Text der Fertigungsauftragszeile an. Wenn zur markierten Arbeitsgangzeile eine Fertigungszeile mit hinterlegtem Text vorliegt, dann erscheint dieser hier; andernfalls bleibt die InfoBox leer. |
| **FA-Nr.** (Prod. Order No.) | Bestimmt zusammen mit der Zeilennummer, welche Fertigungszeile geladen wird. |
| **FA-Zeilennr.** (Prod. Order Line No.) | Bestimmt die konkrete Fertigungszeile innerhalb des Fertigungsauftrags. Wenn der Anwender eine Zeile markiert, dann wird über FA-Nr. und FA-Zeilennr. der passende Zeilentext ermittelt. |

**Bezug zur markierten Zeile:** Der Text wird über **FA-Nr.** und **FA-Zeilennr.** der markierten Arbeitsgangzeile ermittelt; der Belegstatus ist auf **Freigegeben** festgelegt.

### InfoBox „Arbeitsgangtext"

**Prozessbezug:** Diese InfoBox zeigt den erweiterten Text des **Arbeitsgangs** (Arbeitsplanzeile) und ist damit die für die tägliche Abarbeitung wichtigste InfoBox: Sie liefert die konkrete Arbeitsanweisung zum markierten Arbeitsgang. Die InfoBox wird bei jedem Zeilenwechsel neu aufgebaut und exakt auf den markierten Arbeitsgang eingegrenzt.

| Feld | Erläuterung |
| --- | --- |
| **Arbeitsgangtext** | Zeigt den erweiterten Text der Arbeitsgangzeile (Arbeitsplanzeile) an. Wenn zur markierten Zeile ein Arbeitsgangtext hinterlegt ist, dann erscheint dieser hier; andernfalls bleibt die InfoBox leer. |

Die Eingrenzung des Arbeitsgangtexts erfolgt automatisch über mehrere Kriterien der markierten Zeile:

| Feld | Erläuterung |
| --- | --- |
| **FA-Nr.** (Prod. Order No.) | Wenn gesetzt, dann wird der Arbeitsgangtext auf den Fertigungsauftrag der markierten Zeile eingegrenzt. |
| **Zeilennr.** (Line No.) | Wenn gesetzt, dann wird auf die zugehörige Fertigungszeile bzw. Arbeitsplan-Referenzzeile eingegrenzt. |
| **Arbeitsgangnr.** (Operation No.) | Wenn gesetzt, dann wird auf genau den markierten Arbeitsgang eingegrenzt; so sieht der Anwender nur den Text zu dem Arbeitsschritt, an dem er gerade arbeitet. |
| **Routing Nr.** (Routing No.) | Wenn gesetzt, dann wird der Text dem richtigen Arbeitsplan des Fertigungsauftrags zugeordnet. |
| **Zentrum Nr.** (Center No.) | Wenn gesetzt, dann wird der Text der Kapazitätsstelle (Arbeitsplatz bzw. Arbeitsplatzgruppe) des Arbeitsgangs zugeordnet, sodass die Anzeige zum tatsächlich ausführenden Zentrum passt. |

**Bezug zur markierten Zeile:** Der Arbeitsgangtext wird über die Arbeitsplanzeile des Fertigungsauftrags ermittelt und auf **FA-Nr.**, **Zeilennr.**, **Arbeitsgangnr.**, **Routing Nr.** und **Zentrum Nr.** der markierten Zeile eingegrenzt. Der Belegstatus (**FA-Status**) der markierten Zeile wird an die InfoBox übergeben, damit der Text zum richtigen Status geladen wird.

## Aktion „Erweiteter Text Fertigung"

Ergänzend zu den InfoBoxen stellt die App die Aktion **Erweiteter Text Fertigung** bereit. Sie ist im Menüband des **FA-Arbeitsvorrats** angeheftet (Kategorie Prozess) und öffnet die vollständige Textpflege des Erweiterten Textmoduls zum Fertigungsauftrag der markierten Zeile.

**Öffnen Sie über die Aktion Erweiteter Text Fertigung die vollständige Textansicht** des Fertigungsauftrags. Dabei gilt:

- Es wird der Fertigungsauftrag zur **FA-Nr.** der markierten Zeile herangezogen.
- Der Belegstatus ist fest auf **Freigegeben** gesetzt; die Aktion öffnet also die Texte des freigegebenen Fertigungsauftrags.

Während die InfoBoxen die Texte kompakt am Rand anzeigen, bietet die Aktion die vollständige Sicht auf die Dokumenttexte des Fertigungsauftrags und eignet sich zum Lesen längerer Texte oder für Anwender, die mehr Kontext benötigen als die InfoBox darstellt.

### Statuswerte des Belegtyps (Dokumenttyp)

Die zugrunde liegende Textzuordnung des Erweiterten Textmoduls unterscheidet mehrere Belegtypen (Dokumenttypen) eines Fertigungsauftrags. Diese App verwendet durchgängig den Wert **Freigegeben**. Der vollständige Wertevorrat des Dokumenttyps lautet:

- **Simuliert:** Texte eines simulierten Fertigungsauftrags. Von dieser App **nicht** verwendet — InfoBoxen und Aktion greifen nicht auf simulierte Aufträge zu.
- **Geplant:** Texte eines geplanten Fertigungsauftrags. Von dieser App **nicht** verwendet.
- **Fest geplant:** Texte eines fest geplanten Fertigungsauftrags. Von dieser App **nicht** verwendet.
- **Freigegeben:** Texte des freigegebenen Fertigungsauftrags. **Dieser Wert wird von der App verwendet:** InfoBoxen und die Aktion **Erweiteter Text Fertigung** greifen ausschließlich auf freigegebene Fertigungsaufträge zu, da nur diese im **FA-Arbeitsvorrat** abgearbeitet werden.
- **Beendet:** Texte eines beendeten Fertigungsauftrags. Von dieser App **nicht** verwendet.

### Anzeigemodus (Drucktyp der Anzeige)

Die InfoBoxen dieser App werden im Anzeigemodus **InfoBox** betrieben. Der zugehörige Wertevorrat im Erweiterten Textmodul lautet:

- **InfoBox:** Der Text wird als InfoBox neben der Liste angezeigt. **Dieser Modus wird von den drei InfoBoxen dieser App verwendet.**
- **Bericht:** Der Text ist für die Ausgabe in einem Bericht vorgesehen. Für die Anzeige im **FA-Arbeitsvorrat** durch diese App nicht relevant; die Berichtsausgabe der Texte steuert das Erweiterte Textmodul.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie operative Anwender die von dieser App bereitgestellten InfoBoxen und die Aktion im Tagesablauf nutzen. Alle beschriebenen Bildschirme, Filter und Aktionen sind im **FA-Arbeitsvorrat** und in den zugehörigen InfoBoxen verfügbar.

### Szenario 1: Arbeitsanweisung am Arbeitsplatz lesen

1. **Auslöser:** Ein Werker beginnt seine Schicht und möchte wissen, welche Besonderheiten für die anstehenden Arbeitsgänge gelten.
2. **Einstieg in BC:** Der Werker öffnet über **Suchen** den **FA-Arbeitsvorrat** und setzt im Filter **Arbeitsplatzgruppennr.** seine Arbeitsplatzgruppe; bei Bedarf grenzt er mit **Arbeitsplatznr.** auf seinen Arbeitsplatz ein.
3. **Kernablauf:** Er markiert die erste abzuarbeitende Arbeitsgangzeile. In der InfoBox **Arbeitsgangtext** liest er die konkrete Arbeitsanweisung zum markierten Arbeitsgang. In der InfoBox **Fertigungszeilentext** sieht er zeilenspezifische Hinweise zum Artikel, in der InfoBox **Fertigungstext** übergreifende Hinweise zum gesamten Fertigungsauftrag.
4. **Abschluss:** Beim Wechsel auf die nächste Zeile aktualisieren sich alle drei InfoBoxen automatisch. Es sind keine weiteren Schritte in dieser App nötig; die Abarbeitung der Arbeitsgänge selbst erfolgt über die Funktionen des Moduls **FA-Arbeitsvorrat**.

### Szenario 2: Vollständigen Fertigungstext einsehen

1. **Auslöser:** Der Text in der InfoBox **Fertigungstext** ist umfangreich, und der Anwender möchte den kompletten Kopftext des Fertigungsauftrags lesen.
2. **Einstieg in BC:** Im **FA-Arbeitsvorrat** markiert der Anwender eine Arbeitsgangzeile des betreffenden Fertigungsauftrags.
3. **Kernablauf:** Er wählt im Menüband die angeheftete Aktion **Erweiteter Text Fertigung**. Es öffnet sich die vollständige Textansicht des freigegebenen Fertigungsauftrags zur **FA-Nr.** der markierten Zeile.
4. **Abschluss:** Der Anwender liest den vollständigen Text und schließt die Ansicht wieder. Änderungen an den Texten selbst erfolgen über die Textpflege des Erweiterten Textmoduls.

### Szenario 3: Prüfen, warum keine Texte erscheinen

1. **Auslöser:** Ein Anwender meldet, dass die InfoBoxen leer bleiben.
2. **Einstieg in BC:** Im **FA-Arbeitsvorrat** markiert der Schlüsselanwender dieselbe Arbeitsgangzeile.
3. **Kernablauf:** Er prüft, ob der zugehörige Fertigungsauftrag **freigegeben** ist (nur freigegebene Aufträge werden angezeigt) und ob im Erweiterten Textmodul überhaupt Texte am Kopf, an der Zeile bzw. am Arbeitsgang hinterlegt sind.
4. **Abschluss:** Fehlen die Texte, werden sie über die Textpflege des Erweiterten Textmoduls ergänzt; danach erscheinen sie beim erneuten Markieren der Zeile automatisch in den InfoBoxen.

## FAQ und Troubleshooting

### 1. Warum sehe ich im FA-Arbeitsvorrat keine erweiterten Texte?

Die InfoBoxen greifen ausschließlich auf **freigegebene** Fertigungsaufträge zu und zeigen nur Texte an, die im Erweiterten Textmodul am Kopf, an der Zeile oder am Arbeitsgang hinterlegt wurden. Wenn kein freigegebener Auftrag zur markierten Zeile existiert oder keine Texte gepflegt sind, dann bleiben die InfoBoxen leer.

### 2. Wo pflege ich die Texte, die in den InfoBoxen erscheinen?

Die Texte werden nicht in dieser App, sondern über das vorausgesetzte Modul **Erweitertes Textmodul** am Fertigungsauftrag (Kopf, Zeile, Arbeitsgang) erfasst. Diese App zeigt diese Texte im **FA-Arbeitsvorrat** lediglich an.

### 3. Was zeigt die InfoBox „Fertigungstext" gegenüber „Fertigungszeilentext"?

**Fertigungstext** zeigt den Kopftext des gesamten Fertigungsauftrags (auftragsübergreifend). **Fertigungszeilentext** zeigt den Text der einzelnen Fertigungsauftragszeile (artikel- bzw. zeilenspezifisch). Beide beziehen sich auf die **FA-Nr.** der markierten Zeile.

### 4. Warum ändert sich der Arbeitsgangtext, wenn ich eine andere Zeile markiere?

Die InfoBox **Arbeitsgangtext** wird bei jedem Zeilenwechsel neu aufgebaut und exakt über **FA-Nr.**, **Zeilennr.**, **Arbeitsgangnr.**, **Routing Nr.** und **Zentrum Nr.** der markierten Zeile eingegrenzt. So sehen Sie immer nur den Text zu dem Arbeitsgang, den Sie gerade bearbeiten.

### 5. Wie öffne ich die vollständige Textansicht?

Markieren Sie im **FA-Arbeitsvorrat** eine Arbeitsgangzeile und wählen Sie im Menüband die Aktion **Erweiteter Text Fertigung**. Es öffnet sich die vollständige Textansicht des freigegebenen Fertigungsauftrags zur **FA-Nr.** der markierten Zeile.

### 6. Warum öffnet die Aktion nur freigegebene Aufträge?

Der **FA-Arbeitsvorrat** dient der Abarbeitung freigegebener Fertigungsaufträge. Die Aktion **Erweiteter Text Fertigung** ist daher fest auf den Dokumenttyp **Freigegeben** eingestellt und greift nicht auf simulierte, geplante, fest geplante oder beendete Aufträge zu.

### 7. Wie stelle ich sicher, dass ich nur die Arbeitsgänge meines Arbeitsplatzes sehe?

Setzen Sie im **FA-Arbeitsvorrat** zuerst den Filter **Arbeitsplatzgruppennr.** und danach optional **Arbeitsplatznr.**. Die InfoBoxen und die Aktion beziehen sich anschließend auf die von Ihnen markierte Zeile innerhalb dieser Filterung.

### 8. Muss ich den Filter Arbeitsplatznr. immer setzen?

Nein. Der Filter **Arbeitsplatznr.** ist optional. Ohne Eingabe sehen Sie alle Arbeitsplätze der gewählten **Arbeitsplatzgruppe**; mit Eingabe grenzen Sie auf einen einzelnen Arbeitsplatz ein.

### 9. Welche Berechtigungen brauche ich für diese App?

Für die Funktionen dieser App wird der Berechtigungssatz **All Ext. Text Module with Production Order Job Overview permissions** benötigt. Zusätzlich benötigen Sie die Berechtigungen der vorausgesetzten Module **FA-Arbeitsvorrat** (zum Öffnen der Ansicht) und **Erweitertes Textmodul** (zum Lesen und Pflegen der Texte).

### 10. Wird der Text automatisch aktualisiert oder muss ich neu laden?

Die InfoBoxen aktualisieren sich automatisch, sobald Sie eine andere Arbeitsgangzeile markieren. Ein manuelles Neuladen ist nicht erforderlich. Werden im Erweiterten Textmodul neue Texte gepflegt, erscheinen sie beim erneuten Markieren der Zeile.
