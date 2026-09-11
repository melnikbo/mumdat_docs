---
title: Anwenderhandbuch m+m Wire Rope Configurator
---

# Anwenderhandbuch m+m Wire Rope Configurator

## Einleitung

Der **m+m Wire Rope Configurator** erweitert die Produktionsobjekte von Microsoft Dynamics 365 Business Central um eine Seilkonfiguration. Aus einer Seillänge im Verkauf entstehen ein simulierter Fertigungsauftrag, dessen **FA-Arbeitsplan** und dessen **FA-Komponenten**; die Modulrechnung ermittelt daraus die Anzahl der Spulen, die benötigte Einzellitzenlänge, die Einbauhäufigkeit, die Restmeter und die zu fertigenden Komponentenmengen.

Damit die Rechnung greift, hinterlegt die Verwaltung am **Arbeitsplan** das Kennzeichen **Ist Seil**, pflegt die Seilparameter (Litzen, Drähte, Faktoren) auf den **Arbeitsgangzeilen** und den **Fert.-Stücklistenzeilen** und trägt am **Arbeitsplatz** die **Rüstlänge in Meter** sowie das **Max. Spulengewicht** ein. Im Tagesgeschäft erfasst der Anwender am **Verkaufsauftrag** die **Passlängen** und startet den **Fertigungsassistent**.

**Zielgruppe.** Primäre Zielgruppe sind die **operativen Anwender**, die im Verkaufsauftrag Seillängen erfassen, den Fertigungsassistent ausführen und die Seilberechnung im Fertigungsauftrag anstoßen. Sekundär richtet sich das Handbuch an die **Fertigungsvorbereitung und Administration**, die Arbeitspläne, Fertigungsstücklisten, Arbeitsplätze und Produktionskampagnen als Seil einrichtet.

**Prozessüberblick.** Der Weg des Anwenders folgt dieser Kette: **Stammdaten und Einrichtung als Seil** (Arbeitsplatz, Arbeitsplan, Arbeitsgangzeilen, Fert.-Stücklistenzeilen) → **Verkaufsauftrag** mit Erfassung der **Passlängen** → **Fertigungsassistent** erzeugt den simulierten Fertigungsauftrag → **Drahtseil neu berechnen** ermittelt die Seilwerte → optionale Übernahme in den Herkunftsbeleg. Ergänzend verteilt die **Produktionskampagne** die **Seilrüstlänge** bei der Freigabe auf die enthaltenen Fertigungsaufträge.

## Schnellstart für Anwender

Der Schnellstart nennt die minimalen Schritte in Abhängigkeitsreihenfolge. Die Einrichtung steht vor der täglichen Arbeit, weil die Seilberechnung ohne die Seilkennzeichnung und die Rüstdaten nicht rechnet.

1. **Zuerst** den **Arbeitsplatz** öffnen und im Reiter Terminplanung die **Rüstlänge in Meter** und das **Max. Spulengewicht** eintragen (siehe *Einrichtung*).
2. **Danach** den **Arbeitsplan** öffnen, im Register **Allgemein** das Kennzeichen **Ist Seil** setzen und auf den **Arbeitsgangzeilen** die Seilparameter (u. a. **Anzahl Litzen**, **Helixfaktor für Seil**, **Sicherheitsfaktor**, **Sollmenge**) pflegen (siehe *Stammdaten*).
3. Auf den **Fert.-Stücklistenzeilen** die Komponentenparameter (**Anzahl Litzen**, **Anzahl Drähte**, **Mengenfaktor**, **Verschnittfaktor**, **Helixfaktor für Litze**) hinterlegen.
4. Im **Verkaufsauftrag** die betreffende Zeile markieren und über das Menü **Zeile** die Aktion **Passlängen** wählen; je Abschnitt **Reihenfolge**, **Meter** und **Nummer** erfassen. Der Kopf zeigt **Auftragsmeter**, **Gesamtmeter** und **Restmeter**.
5. **Schließlich** auf derselben Verkaufsauftragszeile die Aktion **Fertigungsassistent** wählen. Das Modul erzeugt je Passlänge eine Fertigungsauftragszeile, reserviert gegen die Verkaufszeile und öffnet den Fertigungsassistent. Dort **Drahtseil neu berechnen** ausführen, damit Spulen, Einzellitzenlänge, Einbauhäufigkeit und Komponentenmengen berechnet werden.

> Hinweis: Fehlen zu einer Verkaufszeile Passlängen, fragt das System **„Es existieren keine Passlängen. Wollen Sie fortfahren?“**. Bestätigen Sie nur, wenn der Auftrag ohne Passlängen weiterlaufen soll.

## Einrichtung

Die Einrichtung des Moduls verteilt sich auf wenige, klar getrennte Flächen: die **Rüstdaten am Arbeitsplatz**, die **Seilkennzeichnung des Arbeitsplans** und – bei kampagnengeführter Produktion – die **Seilrüstlänge der Produktionskampagne**. Die Seilparameter auf Arbeitsgang- und Stücklistenebene sind Stammdaten und im Kapitel *Stammdaten* beschrieben.

### Rüstdaten am Arbeitsplatz

**Einstieg:** Öffnen Sie den betreffenden **Arbeitsplatz** (Arbeitsplatzkarte) und wechseln Sie in den Bereich Terminplanung.

Prozessintro: Diese Felder pflegt die **Fertigungsvorbereitung** einmalig je Arbeitsplatz, bevor der erste Seilauftrag gerechnet wird. Die Werte sind die physikalische Grundlage der Spulen- und Rüstlängenrechnung: Das **Max. Spulengewicht** begrenzt, wie viel Seil pro Spule aufgewickelt werden darf, und die **Rüstlänge in Meter** fließt bei der Übernahme in die Arbeitsgangzeile als Vorbelegung ein. Die Werte werden später im **Fertigungsassistent** über **Drahtseil neu berechnen** ausgewertet.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Rüstlänge in Meter** | Wenn ein Wert gesetzt ist, wird dieser Meterwert beim Anlegen einer Arbeitsgangzeile mit diesem Arbeitsplatz automatisch als **Rüstlänge in Meter** der Zeile vorbelegt; dadurch muss die Rüstlänge nicht je Arbeitsgang manuell erfasst werden und geht konsistent in die Berechnung der zu fertigenden Menge und des Komponentenbedarfs ein. |
| **Max. Spulengewicht** | Wenn ein Gewicht gesetzt ist, verwendet die Seilberechnung diesen Grenzwert, um **Anzahl Längen je Spule** und **Anzahl Spulen** zu bestimmen; ist das Gewicht 0, greift ersatzweise das Max. Spulengewicht des Folgearbeitsplatzes, sodass die Spulenrechnung nicht ins Leere läuft. Ein höherer Grenzwert ergibt weniger, dafür schwerere Spulen. |

Die Übernahme der Rüstlänge in die Arbeitsgangzeile erfolgt automatisch, sobald in der Arbeitsgangzeile ein Arbeitsplatz gesetzt wird. Die weitere Verwendung ist im Abschnitt *Drahtseil neu berechnen* (Kapitel *Tägliche Arbeit*) beschrieben.

### Arbeitsplan als Seil einrichten

Prozessintro: Diese Einrichtungskette bereitet einen Artikel so vor, dass aus seinem Verkauf ein rechenbarer Seil-Fertigungsauftrag entsteht. Sie wird von der **Fertigungsvorbereitung** vor dem ersten Seilauftrag durchlaufen und in dieser Abhängigkeitsreihenfolge abgearbeitet. Die operative Schließung dieser Kette – die eigentliche Rechnung – erfolgt später im Tagesgeschäft über **Drahtseil neu berechnen** (siehe *Tägliche Arbeit*).

1. **Zuerst** am **Arbeitsplatz** die **Rüstlänge in Meter** und das **Max. Spulengewicht** setzen (siehe *Rüstdaten am Arbeitsplatz*). Wenn diese Werte fehlen, kann die Spulen- und Rüstlängenrechnung keine sinnvollen Mengen liefern.
2. **Danach** den **Arbeitsplan** öffnen und im Register **Allgemein** das Kennzeichen **Ist Seil** setzen. Wenn aktiviert, wird der Arbeitsplan als Seilarbeitsplan behandelt: Die Arbeitsgangzeilen werden nach der **Seil-Reihenfolge** sortiert, die Seilparameter werden pflegepflichtig und die Aktion **Drahtseil neu berechnen** rechnet für diesen Auftrag. Das Kennzeichen lässt sich nicht setzen, solange der Arbeitsplan den Status Zertifiziert hat; setzen Sie es vor der Zertifizierung.
3. **Danach** auf den **Arbeitsgangzeilen** die Seilparameter je Arbeitsgang pflegen (siehe *Stammdaten → Arbeitsgangzeilen*). Ohne gesetzte **Seil-Reihenfolge** lässt sich eine Seil-Arbeitsgangzeile nicht speichern.
4. **Danach** auf den **Fert.-Stücklistenzeilen** die Komponentenparameter pflegen (siehe *Stammdaten → Fert.-Stücklistenzeilen*), damit die Komponentenmengen berechnet werden können.
5. **Schließlich** erfolgt die operative Schließung im Verkaufsauftrag: **Passlängen** erfassen, **Fertigungsassistent** starten und **Drahtseil neu berechnen** ausführen (siehe *Tägliche Arbeit*).

### Seilrüstlänge in der Produktionskampagne einrichten

**Einstieg:** Öffnen Sie die betreffende **Produktionskampagne** (Karte) und arbeiten Sie im Register **Allgemein** sowie im Menüband.

Prozessintro: Diese Einrichtung betrifft Betriebe, die Seilfertigungsaufträge in einer **Produktionskampagne** bündeln. Sie wird von der Fertigungssteuerung vor der Kampagnenfreigabe gepflegt. Die operative Schließung ist die **Freigabe der Kampagne**: Dabei wird die zentral gepflegte **Seilrüstlänge** anteilig auf die Rüstlängen der beteiligten Fertigungsaufträge verteilt und die betroffenen Aufträge werden neu gerechnet.

| Einrichtung | Erläuterung |
|-------------|-------------|
| **Ist Drahtseil** | Wenn aktiviert, gilt die Kampagne als Seilkampagne; das Feld **Seilrüstlänge** wird editierbar und die anteilige Rüstlängenverteilung bei der Freigabe wird für diese Kampagne wirksam. Das Kennzeichen wird beim Verarbeiten der Kampagnenzeilen automatisch gesetzt, sobald ein Seilarbeitsplan mit Rüstlänge enthalten ist; es ist nicht manuell editierbar. Alle enthaltenen Fertigungsaufträge müssen dasselbe Seilkennzeichen tragen, sonst bricht die Verarbeitung mit Fehlermeldung ab. |
| **Seilrüstlänge** | Wenn ein Wert gesetzt ist, verteilt die Freigabe diese Gesamtrüstlänge anteilig auf die **Rüstlänge in Meter** der Arbeitsgänge aller Kampagnenaufträge und rechnet diese Aufträge anschließend neu; dadurch lässt sich die Rüstlänge zentral über die gesamte Kampagne steuern, statt sie je Auftrag einzeln zu pflegen. Das Feld ist nur editierbar, wenn **Ist Drahtseil** gesetzt ist, und darf nur im Status Offen geändert werden. |

Numerische Schritte der Einrichtung und Schließung:

1. **Zuerst** die Kampagne mit ihren Seilfertigungsaufträgen füllen und verarbeiten; dabei setzt das System **Ist Drahtseil** und summiert die Rüstlängen der enthaltenen Seilarbeitsgänge in die **Seilrüstlänge**.
2. **Danach** bei Bedarf über die Menübandaktion die aktuell summierte Gesamtrüstlänge der Kampagne neu ermitteln lassen (nur bei Status Offen möglich). Diese Aktion liest die Rüstlängen der Kampagnenaufträge erneut zusammen und schreibt sie in die **Seilrüstlänge**.
3. **Schließlich** die Kampagne **freigeben**. Weicht die neue **Seilrüstlänge** von der bisher verteilten Summe ab, verteilt das System die Differenz anteilig auf die Rüstlängen der beteiligten Arbeitsgänge und rechnet die betroffenen Fertigungsaufträge neu.

## Stammdaten

Die Seil-Stammdaten liegen auf drei Flächen: dem **Arbeitsplan** (Seilkennzeichen), den **Arbeitsgangzeilen** (Seilrechnung je Arbeitsgang) und den **Fert.-Stücklistenzeilen** (Komponentenparameter). Sie werden von der Fertigungsvorbereitung gepflegt und steuern unmittelbar, was der Fertigungsassistent im Tagesgeschäft berechnet.

### Arbeitsplan — Kennzeichen Ist Seil

**Einstieg:** Öffnen Sie **Arbeitspläne**, wählen Sie den Arbeitsplan und arbeiten Sie im Register **Allgemein**.

Prozessintro: Das Seilkennzeichen ist der zentrale Schalter des Moduls. Es entscheidet, ob ein Arbeitsplan als Seil gerechnet wird, und steuert die Sortierung und die Pflegepflichten der Arbeitsgangzeilen. Es wird vor der Zertifizierung gesetzt und im Verkaufsauftrag sowie im Fertigungsassistent ausgewertet.

| Feld | Erläuterung |
|------|-------------|
| **Ist Seil** | Wenn aktiviert, wird der Arbeitsplan als Seilarbeitsplan geführt: Die Arbeitsgangzeilen werden nach der **Seil-Reihenfolge** sortiert, die Seilparameter der Zeilen werden geprüft und pflegepflichtig, und die Aktion **Drahtseil neu berechnen** rechnet für Aufträge zu diesem Arbeitsplan. Ohne das Kennzeichen bleibt der Arbeitsplan ein Standard-Arbeitsplan ohne Seilrechnung. Das Kennzeichen kann nicht gesetzt werden, wenn der Arbeitsplan bereits zertifiziert ist. |

### Arbeitsgangzeilen — Seilparameter je Arbeitsgang

**Einstieg:** Öffnen Sie den **Arbeitsplan** und wechseln Sie in die **Zeilen** (Arbeitsgangzeilen).

Prozessintro: Auf den Arbeitsgangzeilen eines Seilarbeitsplans hinterlegt die Fertigungsvorbereitung die geometrischen und mengenmäßigen Kennwerte je Arbeitsgang. Diese Werte sind die Eingangsgrößen der Seilrechnung; mehrere Felder rechnen bereits bei der Eingabe abhängige Werte fort (z. B. **Zu fertigende Menge**, **Spulenlänge**, **Gesamtanzahl Drähte**). Die Sortierung der Zeilen erfolgt bei Seilarbeitsplänen nach der **Seil-Reihenfolge**. Jede Seil-Arbeitsgangzeile muss eine **Seil-Reihenfolge** besitzen, sonst kann sie nicht gespeichert werden.

| Feld | Erläuterung |
|------|-------------|
| **Seil-Reihenfolge** | Wenn gesetzt, bestimmt dieser Wert die Verarbeitungs- und Anzeigereihenfolge der Seilarbeitsgänge; bei einem Seilarbeitsplan ist die Eingabe Pflicht, weil die Zeilen nach diesem Schlüssel sortiert und die Folgearbeitsgänge daraus abgeleitet werden. |
| **Rüstlänge in Meter** | Wenn gesetzt, geht dieser Meterwert als fixer Rüstanteil in die **Zu fertigende Menge** und den **Komponentenbedarf Rüstlänge** ein; er wird beim Setzen des Arbeitsplatzes aus dessen Rüstlänge vorbelegt und kann je Arbeitsgang übersteuert werden. |
| **Helixfaktor für Seil** | Wenn gesetzt, multipliziert dieser Faktor die Auftragslänge zur benötigten Einzellitzenlänge und zur zu fertigenden Menge; er bildet die Schlagverlängerung des Seils ab. Ein höherer Faktor erhöht die berechnete Litzenlänge. |
| **Produktionsmengenfaktor** | Wenn gesetzt, gibt dieser Faktor das Verhältnis von zu fertigender Menge zur **Sollmenge** an; er wird aus **Zu fertigende Menge** und **Sollmenge** automatisch ermittelt und dient der Rückrechnung der Produktionsmenge. |
| **Komponentenbedarf Rüstlänge** | Wenn berechnet, weist dieses Feld die auf den Arbeitsgang entfallende Rüstlänge der Komponenten aus (Rüstlänge in Meter multipliziert mit der Spulenzahl); es macht den Rüstanteil des Materialbedarfs sichtbar. |
| **Theoretisches Gewicht pro Spule** | Wenn gesetzt, ist dies das rechnerische Gewicht einer Spule; die Spulenrechnung vergleicht es mit dem **Max. Spulengewicht** des Arbeitsplatzes, um die **Anzahl Spulen** zu bestimmen. |
| **Anzahl Spulen** | Wenn berechnet, gibt dieses Feld die Zahl der benötigten Spulen an; es ergibt sich aus theoretischem Spulengewicht, Litzenzahl und dem **Max. Spulengewicht** und steuert die **Spulenlänge**. |
| **Spulenlänge** | Wenn berechnet, ist dies die Länge je Spule (**Zu fertigende Menge** geteilt durch **Anzahl Spulen**); sie wird bei Änderung von Menge oder Spulenzahl automatisch fortgeschrieben. |
| **Anzahl Litzen** | Wenn gesetzt, ist dies die Zahl der Litzen des Seils; sie geht multiplikativ in die zu fertigende Menge und – zusammen mit **Anzahl Drähte pro Litze** – in die **Gesamtanzahl Drähte** ein. |
| **Anzahl Drähte pro Litze** | Wenn gesetzt, bestimmt dieser Wert zusammen mit **Anzahl Litzen** die **Gesamtanzahl Drähte**; er beschreibt den Litzenaufbau. |
| **Gesamtanzahl Drähte** | Wenn berechnet, ist dies das Produkt aus **Anzahl Litzen** und **Anzahl Drähte pro Litze**; das Feld ist nicht editierbar und dient als Kontrollwert des Drahtaufbaus. |
| **Zu fertigende Menge** | Wenn berechnet, ist dies die je Arbeitsgang zu produzierende Seilmenge; sie ergibt sich aus Spulenzahl, **Helixfaktor für Seil**, **Sollmenge** und Rüstanteil und ist nicht direkt editierbar. Sie ist die Bezugsgröße der Komponentenrückrechnung. |
| **Sollmenge** | Wenn gesetzt, ist dies die Zielmenge des Arbeitsgangs; ihre Eingabe stößt die Neuberechnung von **Produktionsmengenfaktor** und **Zu fertigende Menge** an. Sie ist das steuernde Mengenziel des Anwenders. |
| **Sicherheitsfaktor** | Wenn gesetzt, verringert dieser Faktor die zulässige Beladung je Spule in der Rechnung der **Anzahl Längen je Spule**; ein höherer Sicherheitsfaktor führt zu kürzeren Spulen und damit zu mehr Spulen und höherer Prozesssicherheit. |

> Berechnete Felder wie **Zu fertigende Menge**, **Spulenlänge** und **Gesamtanzahl Drähte** sind schreibgeschützt bzw. werden automatisch fortgeschrieben; sie werden hier dokumentiert, damit der Anwender die angezeigten Werte deuten kann.

### Fert.-Stücklistenzeilen — Komponentenparameter

**Einstieg:** Öffnen Sie die **Fertigungsstückliste** und wechseln Sie in die **Zeilen**.

Prozessintro: Auf den Fert.-Stücklistenzeilen beschreibt die Fertigungsvorbereitung, wie eine Komponente in das Seil eingeht. Diese Werte werden beim Aufbau des Fertigungsauftrags auf die **FA-Komponenten** übernommen und bestimmen dort über die Seilrechnung die **Menge pro** der Komponente. Der **Mengenfaktor** wird bei Auswahl eines Artikels aus dessen theoretischem Gewicht je Meter vorbelegt.

| Feld | Erläuterung |
|------|-------------|
| **Anzahl Litzen** | Wenn gesetzt, gibt dies an, mit wie vielen Litzen die Komponente in das Seil eingeht; der Wert wird auf die FA-Komponente übernommen und geht in das **Litzengewicht** und die Komponentenmenge ein. |
| **Anzahl Drähte** | Wenn gesetzt, beschreibt dies die Drahtzahl der Komponente; zusammen mit dem **Mengenfaktor** bestimmt sie das Litzengewicht des Arbeitsgangs und die berechnete Komponentenmenge. |
| **Mengenfaktor** | Wenn gesetzt, gewichtet dieser Faktor die Komponente in der Mengenrechnung; er wird bei Artikelauswahl aus dem theoretischen Gewicht je Meter des Artikels vorbelegt, sodass die Materialmenge ohne manuelle Eingabe konsistent ist. |
| **Verschnittfaktor** | Wenn gesetzt, berücksichtigt dieser Faktor den Materialverschnitt der Komponente; er erhöht den rechnerischen Materialbedarf entsprechend dem erwarteten Abfall. |
| **Helixfaktor für Litze** | Wenn gesetzt, bildet dieser Faktor die Schlagverlängerung der Litze ab und geht multiplikativ in die berechnete **Menge pro** der Komponente ein. Ein höherer Faktor erhöht den Materialbedarf je Meter Seil. |

## Tägliche Arbeit — Verkaufsauftrag, Passlängen und Fertigungsassistent

Diese Kapitel beschreiben den operativen Kern des Moduls. Die hier genutzten Aktionen setzen die im Kapitel *Einrichtung* und *Stammdaten* beschriebenen Seildaten voraus: Der Arbeitsplan muss **Ist Seil** tragen, die Arbeitsgang- und Stücklistenparameter müssen gepflegt sein und der Arbeitsplatz muss **Rüstlänge in Meter** und **Max. Spulengewicht** enthalten. Fehlen diese, liefert **Drahtseil neu berechnen** keine sinnvollen Mengen.

### Einstieg über den Verkaufsauftrag

**Einstieg:** Öffnen Sie den **Verkaufsauftrag**, markieren Sie die Auftragszeile und nutzen Sie im Zeilenmenü **Zeile** die Aktionen **Passlängen** und **Fertigungsassistent**.

Beide Aktionen sind an der Verkaufsauftragszeile verankert. Die Aktion **Passlängen** ist nur aktiv, solange die Zeile eine offene Restmenge besitzt. Die Seite **Passlängen** ist nicht über **Suchen** erreichbar; sie öffnet ausschließlich aus dieser Zeilenaktion.

### Passlängen erfassen

Prozessintro: In der **Passlängen**-Erfassung zerlegt der Anwender die Auftragslänge in einzelne Seilabschnitte. Jeder Abschnitt trägt eine **Reihenfolge**, eine Länge in **Meter** und eine **Nummer** (Anzahl gleicher Abschnitte). Der Kopf der Seite spiegelt laufend, wie viel der Auftragslänge bereits verplant ist.

| Feld | Erläuterung |
|------|-------------|
| **Auftragsmeter** | Zeigt die Gesamtmeter der Herkunftsbelegzeile; dient als Sollwert, gegen den die erfassten Passlängen abgeglichen werden. Das Feld ist nicht editierbar. |
| **Gesamtmeter** | Zeigt die Summe aus **Meter** × **Nummer** über alle erfassten Passlängen; steigt mit jeder erfassten Zeile und bildet die bereits verplante Länge ab. |
| **Restmeter** | Zeigt die Differenz **Auftragsmeter** − **Gesamtmeter**; ist der Wert 0, ist die Auftragslänge vollständig in Passlängen zerlegt. Ein positiver Wert bedeutet noch nicht verplante Länge, ein negativer eine Überplanung. |
| **Reihenfolge** | Wenn gesetzt, bestimmt dieser Wert die Reihenfolge der Passlänge; ein Absprung (Drilldown) auf dieses Feld öffnet – bei bereits erzeugtem Fertigungsauftrag – den Fertigungsassistent zur zugehörigen Auftragszeile und markiert die Passlänge nach Bearbeitung als **Fertigungsassistent bearbeitet**. |
| **Meter** | Wenn gesetzt, ist dies die Länge eines Abschnitts; bei Eingabe wird die Zeile gespeichert und **Gesamtmeter**/**Restmeter** werden neu berechnet. |
| **Nummer** | Wenn gesetzt, ist dies die Anzahl gleich langer Abschnitte; zusammen mit **Meter** ergibt sie die **Gesamtmeter** der Zeile. |
| **Fertigungsassistent bearbeitet** | Zeigt an, ob die Passlänge bereits über den Fertigungsassistent bearbeitet wurde; das Feld wird vom System gesetzt und ist nur in der geführten Assistentensicht sichtbar. |

Beim Schließen der Erfassung prüft das System offene Punkte:

- Wird die geführte Sicht mit OK bestätigt und existieren noch nicht bearbeitete Passlängen, erscheint **„Es existieren nicht bearbeitete Passlängenzeilen. Wollen Sie fortfahren?“**.
- Weicht die Summe der Passlängen von den **Auftragsmetern** ab, bietet das System an, den Herkunftsbeleg zu aktualisieren: **„Die Restmeter sind unterschiedlich von den Herkunftsbelegmetern. … Wollen Sie den Herkunftsbeleg aktualisieren?“**. Bestätigen Sie, wenn die Verkaufszeile auf die tatsächlich verplante Länge angepasst werden soll.

Eine Sicherung greift beim Ändern der Verkaufsmenge: Übersteigt die Summe der Passlängen die Menge der Verkaufszeile, meldet das System **„Die Passlänge kann nicht größer sein als die Menge … . Bitte aktualisieren Sie die Passlänge.“**. Passen Sie in diesem Fall zuerst die Passlängen an.

### Fertigungsassistent starten

Prozessintro: Die Aktion **Fertigungsassistent** überführt die Passlängen in einen simulierten Fertigungsauftrag. Der Anwender startet sie auf der Verkaufsauftragszeile; das Modul erzeugt je Passlänge mit Gesamtmetern größer 0 eine Fertigungsauftragszeile, reserviert die erzeugte Menge gegen die Verkaufszeile und öffnet anschließend den Fertigungsassistent zur weiteren Bearbeitung.

Ablauf beim Start:

1. Markieren Sie die **Verkaufsauftragszeile** und wählen Sie **Fertigungsassistent**.
2. Sind keine Passlängen vorhanden, fragt das System **„Es existieren keine Passlängen. Wollen Sie fortfahren?“**; bei Bestätigung wird der Standard-Fertigungsassistent ohne Passlängen aufgerufen.
3. Andernfalls legt das Modul den simulierten Fertigungsauftrag und je Passlänge eine Fertigungsauftragszeile an, überträgt **Konfektionsmeter** und **Passlängenreihenfolge** und reserviert gegen die Verkaufszeile.
4. Der **Fertigungsassistent** öffnet sich. Wird er ohne Übernahme abgebrochen, wird der erzeugte simulierte Fertigungsauftrag wieder gelöscht.

Im Fertigungsassistent steht das Feld **Konfektionsmeter** zur Verfügung; es hält die für den Seilabschnitt zu konfektionierende Länge und ist die Bezugsgröße der Seilrechnung. Über die Assistentenaktion lassen sich die **Passlängen** erneut aufrufen; die Sortierung des eingebetteten Arbeitsplans richtet sich nach der Seilkennzeichnung des gewählten Arbeitsplans.

### Drahtseil neu berechnen

Prozessintro: **Drahtseil neu berechnen** ist die zentrale Rechenaktion des Moduls. Sie steht im **Fertigungsassistent**, auf dem **FA-Arbeitsplan** (Arbeitsgänge des Fertigungsauftrags) und auf den **FA-Komponenten** zur Verfügung und rechnet über die gesamte Arbeitsgangkette hinweg.

Ablauf:

1. Öffnen Sie den Fertigungsassistent bzw. den **FA-Arbeitsplan** des Seilfertigungsauftrags.
2. Wählen Sie **Drahtseil neu berechnen**. Sind keine Passlängen definiert, meldet das System **„Keine Passlängen definiert. Wollen Sie fortfahren?“**.
3. Das Modul prüft, dass der Arbeitsplan **Ist Seil** trägt, und berechnet je Arbeitsgang: **Gesamtmeter je Litze für Gesamtauftragslänge aus Produktion**, **Benötigte Einzellitzenlänge für vorgegebene Seillänge (ohne Rüstlänge)**, **Anzahl Längen je Spule** (begrenzt durch **Max. Spulengewicht** und **Sicherheitsfaktor**), **Einbauhäufigkeit 1 (Rüsthäufigkeit)**, **Gesamtspulenanzahl**, **Restmeter** sowie die **Zu fertigende Menge** und **zu fertigende Menge (Komponente)**; anschließend wird die **Menge pro** der FA-Komponenten fortgeschrieben.

Die Ergebnisse erscheinen auf dem **FA-Arbeitsplan** in folgenden Feldern. Sie sind überwiegend Rechenergebnisse und werden bei erneuter Berechnung überschrieben.

| Feld | Erläuterung |
|------|-------------|
| **Gesamtmeter je Litze für Gesamtauftragslänge aus Produktion** | Zeigt die über die Auftragslänge benötigten Litzenmeter; Eingangsgröße für **Anzahl Längen je Spule** und **Restmeter**. |
| **Benötigte Einzellitzenlänge für vorgegebene Seillänge (ohne Rüstlänge)** | Zeigt die für eine Seillänge nötige Einzellitzenlänge ohne Rüstanteil; sie skaliert mit **Helixfaktor für Seil** und **Konfektionsmeter**. |
| **Anzahl Längen je Spule** | Zeigt, wie viele Einzellängen auf eine Spule passen; begrenzt durch **Max. Spulengewicht**, **Litzengewicht** und **Sicherheitsfaktor**, mindestens 1. |
| **Einbauhäufigkeit 1 (Rüsthäufigkeit)** | Zeigt, wie oft der Arbeitsgang gerüstet bzw. eingebaut wird, bis die Restmeter aufgebraucht sind; steuert zusammen mit der Spulenzahl die Gesamtspulenanzahl. |
| **Gesamtspulenanzahl** | Zeigt die Gesamtzahl der Spulen (Anzahl Spulen × Einbauhäufigkeit); Bezugsgröße des Rüstanteils in der zu fertigenden Menge. |
| **Restmeter** | Zeigt die nach Verteilung auf ganze Spulen verbleibenden Meter; die Rechnung wiederholt sich, bis dieser Wert 0 oder kleiner ist. |
| **Litzengewicht** | Zeigt das aus **Anzahl Drähte** und **Mengenfaktor** der Komponenten ermittelte Gewicht der Litze; geht in die Spulenrechnung ein. |

Auf den **FA-Komponenten** stehen dieselben Komponentenparameter wie auf den Fert.-Stücklistenzeilen (**Anzahl Litzen**, **Anzahl Drähte**, **Mengenfaktor**, **Verschnittfaktor**, **Helixfaktor für Litze**); die Aktion **Drahtseil neu berechnen** ist auch hier verfügbar und schreibt die **Menge pro** der Komponenten fort.

## Produktionskampagne und Seilrüstlänge

Werden mehrere Seilfertigungsaufträge gemeinsam gesteuert, bündelt die **Produktionskampagne** sie und verteilt die Rüstlänge. Die Einrichtung der Kampagnenfelder ist im Kapitel *Einrichtung → Seilrüstlänge in der Produktionskampagne einrichten* beschrieben; hier steht der operative Bezug.

Bei der **Freigabe** der Kampagne prüft das Modul, ob die Kampagne **Ist Drahtseil** trägt, und verteilt die zentral gepflegte **Seilrüstlänge** anteilig auf die **Rüstlänge in Meter** der Arbeitsgänge aller Kampagnenaufträge. Danach werden die betroffenen Fertigungsaufträge über dieselbe Logik wie **Drahtseil neu berechnen** neu gerechnet. Enthalten die Kampagnenzeilen Seil- und Nicht-Seil-Arbeitspläne gemischt, bricht die Verarbeitung mit einer Meldung ab, die den betroffenen Fertigungsauftrag und die abweichenden Seilkennzeichen nennt; stellen Sie in diesem Fall sicher, dass alle Kampagnenaufträge einheitlich als Seil gekennzeichnet sind.

In der Kampagnenübersicht ist das Kennzeichen **Ist Drahtseil** je Kampagne sichtbar, sodass Seilkampagnen ohne Öffnen der Karte erkennbar sind.

## Übersichtslisten

### Fertigungsstücklistenzeilen (Übersicht)

**Einstieg:** Diese eigenständige Liste ist über **Suchen** erreichbar (**Fertigungsstücklistenzeilen**).

Prozessintro: Die Liste zeigt Fertigungsstücklistenzeilen mit ihren Seilparametern in einer flachen Übersicht und dient der Kontrolle der gepflegten Komponentenwerte über mehrere Stücklisten hinweg. Sie ist schreibgeschützt zu verstehen; gepflegt werden die Werte auf der Fertigungsstückliste selbst.

Neben den Standardspalten der Fertigungsstücklistenzeile (u. a. **Nummer**, **Menge**, **Länge**) sind die Seilparameter der Komponente sichtbar:

| Feld | Erläuterung |
|------|-------------|
| **Anzahl Litzen** | Zeigt die Litzenzahl der Komponente je Zeile; zur Kontrolle der Seilparameter über mehrere Stücklisten. |
| **Anzahl Drähte** | Zeigt die Drahtzahl der Komponente je Zeile. |
| **Mengenfaktor** | Zeigt den Mengenfaktor der Komponente; auffällige Werte deuten auf eine fehlende Artikelvorbelegung hin. |
| **Verschnittfaktor** | Zeigt den Verschnittfaktor der Komponente. |
| **Helixfaktor für Litze** | Zeigt den Helixfaktor der Litze der Komponente. |

### Konfektionsmeter auf den Fertigungsauftragszeilen

Auf den Zeilenübersichten der simulierten, geplanten, fest geplanten und freigegebenen Fertigungsaufträge ergänzt das Modul jeweils die Spalte **Konfektionsmeter**. Sie zeigt die für den Seilabschnitt zu konfektionierende Länge der jeweiligen Fertigungsauftragszeile und wird beim Anlegen aus der Passlänge übernommen. Die Spalte ist auf allen vier Auftragsstatusstufen identisch und dient der schnellen Kontrolle der geplanten Seillänge je Zeile.

## Berechtigungen

Das Modul liefert einen eigenen, zuweisbaren Berechtigungssatz für den Seilkonfigurator. Er bündelt die Objekte des Moduls: die Passlängentabelle mit Lese-, Schreib-, Änderungs- und Löschrecht sowie die Ausführungsrechte der Modul-Codeunits und -Seiten. Der Berechtigungssatz legt fest, welche Aktionen die Anwender im Seilkonfigurator ausführen dürfen. Weisen Sie ihn den Anwendern zu, die Passlängen erfassen, den Fertigungsassistent nutzen und die Seilberechnung ausführen sollen.

## FAQ und Troubleshooting

### 1. Warum rechnet „Drahtseil neu berechnen“ keine Werte?
Der zugrunde liegende **Arbeitsplan** muss das Kennzeichen **Ist Seil** tragen. Ist es nicht gesetzt, bricht die Aktion ab, weil sie ausdrücklich prüft, dass der Arbeitsplan als Seil gekennzeichnet ist. Setzen Sie das Kennzeichen vor der Zertifizierung des Arbeitsplans.

### 2. Was passiert, wenn zu einer Verkaufszeile keine Passlängen erfasst sind?
Beim Start des **Fertigungsassistent** erscheint **„Es existieren keine Passlängen. Wollen Sie fortfahren?“**. Bestätigen Sie, läuft der Standard-Fertigungsassistent ohne Passlängen; brechen Sie ab, erfassen Sie zunächst die Passlängen über die Aktion **Passlängen**.

### 3. Warum meldet das System, dass die Passlänge größer als die Menge ist?
Wird die Menge der Verkaufszeile geändert und übersteigt die Summe der Passlängen die neue Menge, erscheint **„Die Passlänge kann nicht größer sein als die Menge … . Bitte aktualisieren Sie die Passlänge.“**. Reduzieren Sie zuerst die Passlängen auf die neue Auftragsmenge.

### 4. Wie stelle ich sicher, dass der Verkaufsauftrag die tatsächlich verplante Länge führt?
Beim Schließen der **Passlängen**-Erfassung mit abweichenden **Restmetern** fragt das System **„… Wollen Sie den Herkunftsbeleg aktualisieren?“**. Bestätigen Sie, passt das Modul die Meter- und Mengenwerte der Verkaufszeile an die Summe der Passlängen an.

### 5. Warum wird eine Passlänge als „Fertigungsassistent bearbeitet“ markiert?
Wird eine Passlänge über den Drilldown der **Reihenfolge** in den Fertigungsassistent geführt und dort bearbeitet, setzt das Modul das Kennzeichen **Fertigungsassistent bearbeitet**. Beim Schließen der geführten Sicht warnt das System, wenn noch unbearbeitete Passlängen bestehen.

### 6. Woher kommt die Rüstlänge in der Arbeitsgangzeile?
Sie wird beim Setzen des **Arbeitsplatzes** in der Arbeitsgangzeile aus dem Feld **Rüstlänge in Meter** des Arbeitsplatzes vorbelegt. Bei Maschinenzuordnungen wird der Wert des zugehörigen Arbeitsplatzes verwendet. Sie können den Wert je Arbeitsgang übersteuern.

### 7. Wie beeinflusst das „Max. Spulengewicht“ das Ergebnis?
Das **Max. Spulengewicht** des Arbeitsplatzes begrenzt, wie viel Seil pro Spule zulässig ist. Die Rechnung leitet daraus **Anzahl Längen je Spule** und **Anzahl Spulen** ab. Ist das Gewicht am Folgearbeitsplatz 0, greift ersatzweise das Gewicht des aktuellen Arbeitsplatzes, damit die Spulenrechnung nicht ausfällt.

### 8. Welche Rolle spielt der Sicherheitsfaktor?
Der **Sicherheitsfaktor** verringert die rechnerisch zulässige Beladung je Spule. Ein höherer Wert führt zu kürzeren Spulen, damit zu mehr Spulen und einer höheren Rüsthäufigkeit — er erhöht die Prozesssicherheit auf Kosten des Rüstaufwands.

### 9. Warum bricht die Kampagnenverarbeitung mit einer Seil-Meldung ab?
Enthält eine Produktionskampagne Fertigungsaufträge mit unterschiedlichen Seilkennzeichen, meldet das Modul den betroffenen Fertigungsauftrag und die abweichenden Werte und bricht ab. Sorgen Sie dafür, dass alle Aufträge einer Seilkampagne einheitlich als Seil geführt werden.

### 10. Wie wird die Seilrüstlänge über eine Kampagne verteilt?
Bei der **Freigabe** einer Kampagne mit **Ist Drahtseil** verteilt das Modul die zentral gepflegte **Seilrüstlänge** anteilig auf die **Rüstlänge in Meter** der Arbeitsgänge aller Kampagnenaufträge und rechnet die betroffenen Aufträge neu. Ändern Sie die **Seilrüstlänge** nur im Status Offen.

## Typische Anwendungsfälle

### Anwendungsfall 1 — Seilauftrag aus einem Kundenauftrag

**Auslöser.** Ein Kunde bestellt telefonisch ein Drahtseil einer bestimmten Gesamtlänge, das in mehreren Teilstücken zu fertigen ist.

**Einstieg in BC.** Der Anwender legt den **Verkaufsauftrag** an, markiert die Auftragszeile und wählt im Menü **Zeile** die Aktion **Passlängen**.

**Kernablauf.**
1. In der **Passlängen**-Erfassung trägt der Anwender je Teilstück **Reihenfolge**, **Meter** und **Nummer** ein und kontrolliert an **Auftragsmeter**, **Gesamtmeter** und **Restmeter**, dass die Auftragslänge vollständig zerlegt ist.
2. Auf derselben Verkaufsauftragszeile wählt er **Fertigungsassistent**. Das Modul erzeugt den simulierten Fertigungsauftrag mit einer Zeile je Passlänge, überträgt die **Konfektionsmeter** und reserviert gegen die Verkaufszeile.
3. Im Fertigungsassistent führt er **Drahtseil neu berechnen** aus; das Modul berechnet **Anzahl Längen je Spule**, **Gesamtspulenanzahl**, **Benötigte Einzellitzenlänge**, **Einbauhäufigkeit 1 (Rüsthäufigkeit)**, **Restmeter** und die Komponentenmengen.

**Abschluss.** Weicht die verplante Länge von den **Auftragsmetern** ab, bestätigt der Anwender beim Schließen die Rückfrage zur Aktualisierung des Herkunftsbelegs, sodass die Verkaufszeile die tatsächlich verplante Länge führt.

### Anwendungsfall 2 — Rüstlänge über eine Produktionskampagne steuern

**Auslöser.** Die Fertigungssteuerung bündelt mehrere Seilfertigungsaufträge in einer **Produktionskampagne**, um die Rüstlänge gemeinsam zu planen.

**Einstieg in BC.** Der Anwender öffnet die **Produktionskampagne** (Karte) und arbeitet im Register **Allgemein**.

**Kernablauf.**
1. Nach dem Verarbeiten der Kampagnenzeilen steht das Kennzeichen **Ist Drahtseil**; die Summe der Rüstlängen der enthaltenen Seilarbeitsgänge erscheint in der **Seilrüstlänge**.
2. Bei Bedarf lässt der Anwender die aktuelle Gesamtrüstlänge über die Menübandaktion neu ermitteln (nur im Status Offen).
3. Er gibt die Kampagne **frei**. Das Modul verteilt die **Seilrüstlänge** anteilig auf die **Rüstlänge in Meter** der Arbeitsgänge und rechnet die betroffenen Fertigungsaufträge neu.

**Abschluss.** Sind alle Kampagnenaufträge einheitlich als Seil gekennzeichnet, ist die Verteilung abgeschlossen; andernfalls weist die Abbruchmeldung auf den abweichenden Fertigungsauftrag hin und der Anwender vereinheitlicht die Seilkennzeichen.
