---
title: Anwenderhandbuch m+m Ext. Text Module with Production Order Overview
---

# Anwenderhandbuch m+m Ext. Text Module with Production Order Overview

## Einleitung

Die App **m+m Ext. Text Module with Production Order Overview** verbindet zwei bestehende
m+m-Erweiterungen: das **Erweiterte Textmodul** und die **FA-Zeilenübersicht**
(Produktionsauftragsübersicht). Sie fügt der Seite **FA-Zeilenübersicht** zusätzliche
Informationsfenster (Infoboxen) und zwei Aktionen hinzu, mit denen erweiterte Texte eines
Fertigungsauftrags direkt aus der Zeilenübersicht gelesen und bearbeitet werden können.

Ohne diese App müssen Anwender die erweiterten Texte eines Fertigungsauftrags in dessen
eigener Seite öffnen. Mit der App sehen sie den **Fertigungstext** und den
**Fertigungszeilentext** unmittelbar neben der jeweiligen Fertigungsauftragszeile und
öffnen die vollständige Textbearbeitung über die Aktion **Erweiterter Fertigungstext**.

**Zielgruppe:** Primär richtet sich das Modul an **operativ tätige Anwender**, die täglich
mit der **FA-Zeilenübersicht** arbeiten — Fertigungssteuerung, Arbeitsvorbereitung und
Produktionsmitarbeitende, die auftrags- und zeilenbezogene Zusatztexte einsehen oder
pflegen. Administratoren sind nur nachrangig betroffen: Die App bringt **keine eigenen
Einrichtungsseiten** und **keine eigenen Stammdaten** mit; die eigentliche Textpflege und
deren Konfiguration erfolgen im **Erweiterten Textmodul** (siehe dessen separates Handbuch).

**Kurzer Prozessüberblick:**

1. Der Anwender öffnet die **FA-Zeilenübersicht**.
2. Zu jeder markierten Fertigungsauftragszeile zeigen die Infoboxen **Fertigungstext**
   (Kopftext des Fertigungsauftrags) und **Fertigungszeilentext** (Text der einzelnen
   Auftragszeile) den jeweils hinterlegten erweiterten Text an.
3. Über die Aktion **Erweiterter Fertigungstext** öffnet der Anwender die vollständige
   Textbearbeitung des Erweiterten Textmoduls, um Texte zu lesen oder zu ändern.

> **Voraussetzung:** Die App ist ein Verbindungsmodul. Sie setzt die installierten und
> eingerichteten Basismodule **m+m Cloud Base**, **m+m Ext. Text Module** (Erweitertes
> Textmodul) und **m+m Production Order Overview** (FA-Zeilenübersicht) voraus. Die App
> selbst erfordert keine zusätzliche Einrichtung.

## Schnellstart für Anwender

Der schnellste Weg zum erweiterten Fertigungstext einer Auftragszeile:

1. Öffnen Sie die Seite **FA-Zeilenübersicht** über die Suche (BC-Suchfunktion **Suchen**).
2. Markieren Sie die gewünschte Zeile. Die Infobox **Fertigungstext** und die Infobox
   **Fertigungszeilentext** auf der rechten Seite zeigen sofort den erweiterten Text zum
   Kopf des Fertigungsauftrags bzw. zur markierten Zeile an.
3. Wählen Sie in der Menüleiste die Aktion **Erweiterter Fertigungstext**, um die
   vollständige Textbearbeitung zu öffnen. Die geöffneten Texte richten sich automatisch
   nach dem **Status** des Fertigungsauftrags der markierten Zeile (siehe Abschnitt
   *Statusabhängige Textauswahl*).
4. Lesen oder ändern Sie den Text und schließen Sie die Bearbeitung. Die Infoboxen in der
   **FA-Zeilenübersicht** aktualisieren sich beim Wechsel der markierten Zeile.

> **Hinweis:** Die App bringt keine eigenen Einrichtungsschritte mit. Sind die Basismodule
> installiert und ist die **FA-Zeilenübersicht** aufrufbar, stehen die Infoboxen und die
> Aktion **Erweiterter Fertigungstext** ohne weitere Konfiguration zur Verfügung.

## Aufbau der FA-Zeilenübersicht mit erweiterten Texten

Die App erweitert ausschließlich die vorhandene Seite **FA-Zeilenübersicht** (aus dem Modul
FA-Zeilenübersicht). Für den Anwender erscheint die App nicht als eigene Seite, sondern als
zusätzliche Infoboxen und Aktionen innerhalb dieser bekannten Übersicht.

### Aktion: Erweiterter Fertigungstext

Die Aktion **Erweiterter Fertigungstext** ist in der Menüleiste der **FA-Zeilenübersicht**
angeordnet und zusätzlich als hervorgehobene Aktion im Menüband verfügbar. Sie öffnet die
Textbearbeitung des Erweiterten Textmoduls für den Fertigungsauftrag der aktuell markierten
Zeile.

**Bedienung:**

1. Markieren Sie in der **FA-Zeilenübersicht** die Zeile des Fertigungsauftrags, dessen
   Text Sie bearbeiten möchten.
2. Wählen Sie **Erweiterter Fertigungstext**.
3. Es öffnet sich die Textbearbeitung des Erweiterten Textmoduls. Welche Textvariante
   angezeigt wird, hängt vom **Status** des Fertigungsauftrags ab (siehe unten).

### Statusabhängige Textauswahl

Beim Öffnen über **Erweiterter Fertigungstext** ermittelt die App den **Status** des
Fertigungsauftrags der markierten Zeile und öffnet genau die dazu passende Textvariante.
Die erweiterten Texte werden im Erweiterten Textmodul je Belegtyp getrennt geführt; die App
bildet den Fertigungsauftragsstatus auf den entsprechenden Belegtyp ab. Der Anwender muss
den Belegtyp also nicht manuell auswählen — er ergibt sich aus dem Status der Zeile.

Die folgende Zuordnung ist im Programmablauf fest hinterlegt. Jeder Wert beschreibt, welche
Textvariante beim Aufruf geöffnet wird:

| Status des Fertigungsauftrags | Erläuterung (geöffnete Textvariante) |
|---|---|
| **Simuliert** | Wenn die markierte Zeile zu einem simulierten Fertigungsauftrag gehört, öffnet die Aktion den erweiterten Text der Variante **Simuliert**; damit lassen sich bereits in der Simulationsphase auftrags- und zeilenbezogene Texte hinterlegen. |
| **Geplant** | Wenn die Zeile zu einem geplanten Fertigungsauftrag gehört, öffnet die Aktion den Text der Variante **Geplant**; Texte aus der Planungsphase bleiben so getrennt von späteren Phasen. |
| **Fest geplant** | Wenn die Zeile zu einem fest geplanten Fertigungsauftrag gehört, öffnet die Aktion den Text der Variante **Fest geplant**. |
| **Freigegeben** | Wenn die Zeile zu einem freigegebenen Fertigungsauftrag gehört, öffnet die Aktion den Text der Variante **Freigegeben**; dies ist die für die laufende Fertigung maßgebliche Textvariante. |
| **Beendet** | Wenn die Zeile zu einem beendeten Fertigungsauftrag gehört, öffnet die Aktion den Text der Variante **Beendet**; abgeschlossene Aufträge behalten so ihren dokumentierten Textstand. |

> Die eigentliche Textpflege, das Zusammenführen von Standardtexten und die Regeln, nach
> denen Texte gebildet werden, sind im Handbuch des **Erweiterten Textmoduls** beschrieben.
> Diese App stellt lediglich den direkten Zugang aus der **FA-Zeilenübersicht** her und
> wählt die zum Status passende Variante aus.

### Infobox: Fertigungstext

Die Infobox **Fertigungstext** zeigt den erweiterten **Kopftext** des Fertigungsauftrags,
zu dem die markierte Zeile gehört. Sie wird beim Wechsel der markierten Zeile automatisch
aktualisiert und zeigt jeweils den Text passend zum Status des Auftrags an.

| Feld | Erläuterung |
|---|---|
| **Fertigungstext** (Infobox) | Wenn Sie eine Zeile in der **FA-Zeilenübersicht** markieren, zeigt diese Infobox den erweiterten Kopftext des zugehörigen Fertigungsauftrags an; so sehen Sie auftragsübergreifende Hinweise, ohne den Fertigungsauftrag selbst öffnen zu müssen. Der Inhalt wird nach Fertigungsauftragsnummer und Status gefiltert. |

### Infobox: Fertigungszeilentext

Die Infobox **Fertigungszeilentext** zeigt den erweiterten Text der **einzelnen
Fertigungsauftragszeile**, die aktuell markiert ist.

| Feld | Erläuterung |
|---|---|
| **Fertigungszeilentext** (Infobox) | Wenn Sie eine Zeile markieren, zeigt diese Infobox den erweiterten Text genau dieser Auftragszeile an; damit sind zeilenspezifische Fertigungshinweise sofort sichtbar. Der Inhalt wird nach Fertigungsauftragsnummer, Zeilennummer und Status gefiltert und beim Zeilenwechsel aktualisiert. |

## Verkaufstexte in der FA-Zeilenübersicht (optionaler Ausbaustand)

Die App enthält zusätzlich Elemente, mit denen zu einer Fertigungsauftragszeile auch der
erweiterte **Verkaufstext** der zugeordneten Verkaufszeile angezeigt und geöffnet werden
kann. Diese Elemente sind standardmäßig **ausgeblendet** und werden nur in Konstellationen
sichtbar, in denen die FA-Zeilenübersicht Verkaufszeilen bereitstellt. In der Standard­ansicht
sieht der Anwender sie nicht.

Wenn diese Elemente eingeblendet sind, stehen zur Verfügung:

- Aktion **Erweiterter Verkaufstext** — öffnet die Textbearbeitung des Erweiterten
  Textmoduls für die Verkaufszeile, die der markierten Fertigungsauftragszeile zugeordnet
  ist.
- Infobox **Verkaufstext** — zeigt den erweiterten Kopftext des zugehörigen Verkaufsbelegs.
- Infobox **Verkaufszeilentext** — zeigt den erweiterten Text der zugeordneten
  Verkaufszeile.

> Da diese Elemente standardmäßig ausgeblendet sind, ist für den überwiegenden Teil der
> Anwender allein der **Fertigungstext**-Zweig (Abschnitte oben) relevant.

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen, wie die App im Arbeitsalltag genutzt wird. Alle Schritte
verwenden ausschließlich Seiten und Aktionen, die die App tatsächlich bereitstellt.

### Fertigungshinweis zu einem freigegebenen Auftrag prüfen

**Auslöser:** Ein Mitarbeitender der Fertigung erhält telefonisch die Rückfrage, ob zu
einem laufenden Auftrag besondere Bearbeitungshinweise vorliegen.

**Einstieg in BC:** Der Mitarbeitende öffnet über **Suchen** die **FA-Zeilenübersicht** und
markiert die betreffende Auftragszeile.

**Kernablauf:** In der Infobox **Fertigungstext** liest er den Kopftext des Auftrags, in der
Infobox **Fertigungszeilentext** den zeilenspezifischen Text. Reicht die Vorschau nicht aus,
wählt er **Erweiterter Fertigungstext**; da der Auftrag den Status **Freigegeben** hat,
öffnet die App direkt die freigegebene Textvariante zur vollständigen Ansicht.

**Abschluss:** Die Rückfrage ist ohne Öffnen des Fertigungsauftrags beantwortet; die
markierte Zeile kann gewechselt werden, die Infoboxen aktualisieren sich automatisch.

### Zeilenbezogenen Text während der Planung ergänzen

**Auslöser:** In der Arbeitsvorbereitung soll zu einer geplanten Auftragszeile ein
zusätzlicher Hinweis erfasst werden, bevor der Auftrag fest geplant wird.

**Einstieg in BC:** Aufruf der **FA-Zeilenübersicht**, Markieren der geplanten Zeile.

**Kernablauf:** Der Anwender wählt **Erweiterter Fertigungstext**. Weil die Zeile zu einem
Auftrag mit Status **Geplant** gehört, öffnet die App die Textvariante **Geplant**. Der
Anwender erfasst bzw. ändert den Text in der Textbearbeitung des Erweiterten Textmoduls und
schließt die Seite.

**Abschluss:** Der ergänzte Text erscheint anschließend in der Infobox
**Fertigungszeilentext**, sobald die Zeile erneut markiert wird.

## FAQ und Troubleshooting

### Warum sehe ich in der FA-Zeilenübersicht plötzlich zwei zusätzliche Infoboxen?

Die App fügt die Infoboxen **Fertigungstext** und **Fertigungszeilentext** hinzu. Sie zeigen
den erweiterten Kopf- bzw. Zeilentext des Fertigungsauftrags zur markierten Zeile an.

### Wie öffne ich die vollständige Textbearbeitung eines Fertigungsauftrags?

Markieren Sie die Zeile in der **FA-Zeilenübersicht** und wählen Sie die Aktion
**Erweiterter Fertigungstext**. Die App öffnet die Textbearbeitung des Erweiterten Textmoduls.

### Warum wird beim Öffnen genau eine bestimmte Textvariante angezeigt?

Die App wertet den **Status** des Fertigungsauftrags der markierten Zeile aus und öffnet die
dazu passende Variante (**Simuliert**, **Geplant**, **Fest geplant**, **Freigegeben** oder
**Beendet**). Eine manuelle Auswahl des Belegtyps ist nicht erforderlich.

### Warum ändert sich der Inhalt der Infoboxen, wenn ich eine andere Zeile markiere?

Die Infoboxen sind an die jeweils markierte Zeile gebunden. Beim Zeilenwechsel filtern sie
neu nach Fertigungsauftragsnummer, Zeilennummer und Status und zeigen den passenden Text an.

### Muss ich für diese App etwas einrichten?

Nein. Die App bringt keine eigenen Einrichtungsseiten und keine Stammdaten mit. Sie
funktioniert, sobald die Basismodule installiert sind und die **FA-Zeilenübersicht**
aufrufbar ist.

### Warum ist die Aktion Erweiterter Fertigungstext leer oder zeigt keinen Text?

Zu dem Fertigungsauftrag ist in der aktuell relevanten Statusvariante noch kein erweiterter
Text hinterlegt. Das Anlegen und Zusammenführen von Texten erfolgt im Erweiterten Textmodul;
die App stellt nur den Zugang und die Vorschau bereit.

### Warum sehe ich keinen Verkaufstext, obwohl die App dies unterstützt?

Die Verkaufstext-Elemente (Aktion **Erweiterter Verkaufstext**, Infoboxen **Verkaufstext**
und **Verkaufszeilentext**) sind standardmäßig ausgeblendet und werden nur eingeblendet,
wenn die FA-Zeilenübersicht Verkaufszeilen bereitstellt.

### Wo pflege ich den eigentlichen Textinhalt?

Der Textinhalt wird in der Textbearbeitung des Erweiterten Textmoduls gepflegt, die Sie über
**Erweiterter Fertigungstext** erreichen. Die zugrunde liegenden Regeln beschreibt das
Handbuch des Erweiterten Textmoduls.

### Bezieht sich die Infobox Fertigungstext auf den Auftrag oder auf die Zeile?

Die Infobox **Fertigungstext** zeigt den **Kopftext** des Fertigungsauftrags; die Infobox
**Fertigungszeilentext** zeigt den Text der **einzelnen Auftragszeile**.

### Kann ich Texte eines bereits beendeten Auftrags noch einsehen?

Ja. Wählen Sie die Zeile eines Auftrags mit Status **Beendet** und öffnen Sie
**Erweiterter Fertigungstext**; die App öffnet die Textvariante **Beendet**, sodass der
dokumentierte Textstand abgeschlossener Aufträge erhalten bleibt und einsehbar ist.
