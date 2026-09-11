---
title: Anwenderhandbuch m+m Tool Management with Prod. Order Job Overview
---

# Anwenderhandbuch m+m Tool Management with Prod. Order Job Overview

## Einleitung

Die App m+m „Tool Management with Prod. Order Job Overview“ verbindet zwei bestehende m+m-Erweiterungen in „Microsoft Dynamics 365 Business Central“: die **Werkzeugverwaltung** (m+m Tool Management) und den **FA-Arbeitsvorrat** (m+m Production Order Job Overview). Sie fügt der Ansicht **FA-Arbeitsvorrat** Werkzeuginformationen hinzu und stellt zwei Planungsansichten bereit, mit denen die Reihenfolge der Werkzeugbelegung geplant und in den FA-Arbeitsvorrat übernommen werden kann.

Konkret ergänzt die App:

- im **FA-Arbeitsvorrat** eine Spalte **Werkzeug Status** sowie die Aktionen **Benötigte Werkzeuge** und **Installierte Werkzeuge**, und sie steuert, wann die Aktion **Starten** für einen Arbeitsgang zulässig ist;
- die Ansicht **Planungswerkzeug**, in der geplante Werkzeugbelegungen je Arbeitsplatzgruppe angezeigt und in eine Reihenfolge gebracht werden;
- in der Werkzeugplanung die Aktion **Reihenfolge übertragen**, mit der die geplante Reihenfolge in den FA-Arbeitsvorrat geschrieben wird.

**Zielgruppe.** Primär richtet sich die App an **operative Anwender in der Fertigung** – Werker und Einrichter, die am Arbeitsplatz Arbeitsgänge starten und rückmelden und dabei prüfen müssen, ob die benötigten Werkzeuge am Arbeitsplatz verfügbar sind. Sekundär unterstützt sie **Fertigungsplaner**, die die Reihenfolge der Werkzeugbelegung vorbereiten. Die App enthält keine eigenen Einrichtungs- oder Stammdatenseiten; die Werkzeugstammdaten (Werkzeugarten, Werkzeuge, Arbeitsplatz-Werkzeuge) werden in der Basis-App m+m Tool Management gepflegt.

**Prozessüberblick.** Der Anwender öffnet den **FA-Arbeitsvorrat**, wählt eine **Arbeitsplatzgruppennr.** (und optional eine **Arbeitsplatznr.**) und sieht die anstehenden Arbeitsgänge. Über die Spalte **Werkzeug Status** erkennt er sofort, ob die am Arbeitsgang benötigten Werkzeuge am Arbeitsplatz installiert sind. Ist dies nicht der Fall, bleibt die Aktion **Starten** gesperrt; über **Benötigte Werkzeuge** und **Installierte Werkzeuge** kann der Anwender die Differenz erkennen und Werkzeuge installieren. Parallel plant der Planer im **Planungswerkzeug** die Reihenfolge und überträgt sie mit **Reihenfolge übertragen** in den FA-Arbeitsvorrat.

## Voraussetzungen

Die App ist eine reine Integrationsschicht und setzt die drei abhängigen Apps sowie vorhandene Werkzeugstammdaten voraus. Vor der ersten Nutzung ist Folgendes sicherzustellen:

| Einrichtung | Erläuterung |
|---|---|
| Abhängige Apps | Wenn die Apps **m+m Cloud Base**, **m+m Tool Management** und **m+m Production Order Job Overview** installiert sind, stehen der **FA-Arbeitsvorrat**, die Werkzeugstammdaten und die hier beschriebenen Ergänzungen zur Verfügung; ohne diese Apps sind die Werkzeugaktionen und die Ansicht **Planungswerkzeug** nicht nutzbar. |
| Berechtigungssatz **MuM TMPJ PermSet** | Wenn dieser zuweisbare Berechtigungssatz einem Benutzer zugeordnet ist, bestimmt er die Berechtigungen für die Tabelle und die Seite **Planungswerkzeug** sowie die zugehörigen Objekte; ohne diesen Satz kann der Benutzer die Planungsansichten nicht öffnen. |
| Werkzeugstammdaten (Basis-App) | Wenn in der Werkzeugverwaltung Werkzeugarten, Werkzeuge und die Zuordnung von Werkzeugen zu Arbeitsplätzen/Arbeitsplatzgruppen gepflegt sind, kann die App den **Werkzeug Status** je Arbeitsgang ermitteln und die Listen **Benötigte Werkzeuge** und **Installierte Werkzeuge** füllen; fehlen diese Stammdaten, bleibt der Status leer bzw. **Nicht okay**. |
| Freigegebene Fertigungsaufträge mit Arbeitsplan | Wenn Fertigungsaufträge freigegeben sind und Arbeitsgänge mit Arbeitsplätzen sowie benötigten Werkzeugen im Arbeitsplan hinterlegt sind, erscheinen sie im FA-Arbeitsvorrat und im Planungswerkzeug; andernfalls bleiben die Ansichten leer. |

Die Pflege der Werkzeugstammdaten sowie sämtliche Einrichtungsschritte (Nummernserien, Werkzeugarten, Arbeitsplatz-Werkzeuge) erfolgen in der Basis-App m+m Tool Management und sind nicht Bestandteil dieser Erweiterung.

## Schnellstart für Anwender

**Werker/Einrichter – Arbeitsgang mit Werkzeugprüfung starten:**

1. Öffnen Sie über die **Suche** den **FA-Arbeitsvorrat**.
2. Tragen Sie im Filterbereich die **Arbeitsplatzgruppennr.** ein und optional die **Arbeitsplatznr.**; die anstehenden Arbeitsgänge werden angezeigt.
3. Prüfen Sie in der Zeile die Spalte **Werkzeug Status**: **Okay** bedeutet, dass alle benötigten Werkzeuge am Arbeitsplatz installiert sind, **Nicht okay**, dass mindestens ein benötigtes Werkzeug fehlt.
4. Bei **Nicht okay** öffnen Sie über die Aktion **Benötigte Werkzeuge** die Liste der geforderten Werkzeuge und über **Installierte Werkzeuge** die Liste der vorhandenen Werkzeuge; installieren Sie fehlende Werkzeuge über **Werkzeug installieren**.
5. Wählen Sie **Starten**, sobald der Status **Okay** ist (bei **Nicht okay** ist **Starten** gesperrt).
6. Melden Sie den Arbeitsgang wie gewohnt über **Teilbeenden** bzw. **Beenden** zurück.

**Planer – Werkzeugreihenfolge übertragen:**

1. Öffnen Sie über die **Suche** das **Planungswerkzeug**.
2. Grenzen Sie über die Filter **Arbeitsplatzgruppe** und ggf. **Arbeitsplatz**, **Werkzeugart** und **Startdatum** die Anzeige ein.
3. Vergeben Sie in den Zeilen die **Reihenfolge**.
4. Wählen Sie **Reihenfolge in FA-Arbeitsvorrat übertragen**; die Reihenfolge wird in die offenen Arbeitsgänge des FA-Arbeitsvorrats geschrieben.

Alternativ überträgt der Planer die Reihenfolge direkt aus der Ansicht **Erf.-Werkzeugplanung** über die Aktion **Reihenfolge übertragen**.

## Anwendung

Die nachfolgend beschriebene Anwendung erfolgt in „Microsoft Dynamics 365 Business Central“.

### FA-Arbeitsvorrat mit Werkzeuginformationen

Die Ansicht **FA-Arbeitsvorrat** ist über die **Suche** erreichbar. Wählt der Anwender im Kopfbereich eine **Arbeitsplatzgruppennr.** aus, erscheinen die zugehörigen Arbeitsgänge der freigegebenen Fertigungsaufträge. Diese App ergänzt die Ansicht um Werkzeuginformationen; die übrige Bedienung (Starten, Rüsten, Unterbrechen, Teilbeenden, Beenden) entspricht dem FA-Arbeitsvorrat der Basis-App.

#### Filter im FA-Arbeitsvorrat

Der Kopfbereich steuert, welche Arbeitsgänge angezeigt werden. Wenn ein Filter gesetzt ist, werden die Zeilen entsprechend eingegrenzt.

| Filterfeld | Erläuterung |
|---|---|
| Arbeitsplatzgruppennr. | Wenn gesetzt, werden ausschließlich Arbeitsgänge dieser Arbeitsplatzgruppe angezeigt; dies ist der übliche Einstieg des Werkers zu Beginn der Schicht. |
| Arbeitsplatzname | Wenn eine Arbeitsplatzgruppe gewählt ist, zeigt dieses Feld deren Bezeichnung zur Kontrolle an; es dient nur der Anzeige. |
| Arbeitsplatznr. | Wenn gesetzt, wird zusätzlich auf einen einzelnen Arbeitsplatz innerhalb der Arbeitsplatzgruppe eingegrenzt; die Angabe ist optional und wird für die Arbeit an einer bestimmten Maschine genutzt. |
| Arbeitsplatzname (Arbeitsplatz) | Wenn ein Arbeitsplatz gewählt ist, zeigt dieses Feld dessen Bezeichnung an; nur Anzeige. |
| FA-Nr. | Wenn gesetzt, werden nur die Arbeitsgänge des angegebenen freigegebenen Fertigungsauftrags angezeigt; hilfreich, wenn der Anwender gezielt einen Auftrag bearbeitet. |
| Datum | Wenn gesetzt, werden die Zeilen auf das gewählte Datum bezogen dargestellt; steuert die zeitliche Sicht auf die Arbeitsgänge. |
| Sortierung | Wenn eine Sortierung gewählt ist, werden die Zeilen entsprechend geordnet (z. B. nach Reihenfolge, Status oder Datum); dies bestimmt die Abarbeitungsreihenfolge in der Anzeige. |
| Beendete ausblenden | Wenn aktiviert, verschwinden bereits beendete Arbeitsgänge aus der Liste; der Anwender sieht nur noch offene Arbeit. |
| Offene ausblenden | Wenn aktiviert, werden offene Arbeitsgänge ausgeblendet; nützlich zur Kontrolle bereits erledigter Arbeit. |
| Rückmeldung in Vorarbeitsgang | Wenn aktiviert, werden nur Arbeitsgänge angezeigt, für die im vorherigen Arbeitsgang bereits Rückmeldungen vorliegen; so arbeitet der Anwender nur Gänge ab, deren Vorstufe bereit ist. |

#### Spalten im FA-Arbeitsvorrat

Diese App fügt der Zeile die Spalte **Werkzeug Status** hinzu. Die übrigen Spalten stammen aus dem FA-Arbeitsvorrat der Basis-App und werden hier zur Orientierung mit aufgeführt.

| Feld | Erläuterung |
|---|---|
| Werkzeug Status | Wenn alle für den Arbeitsgang benötigten Werkzeuge am Arbeitsplatz installiert sind, steht hier **Okay** und die Aktion **Starten** ist zulässig; fehlt mindestens ein Werkzeug, steht hier **Nicht okay** und **Starten** bleibt gesperrt, bis die Werkzeuge installiert sind. Die Spalte wird beim Blättern je Zeile automatisch neu ermittelt und farblich hervorgehoben. |
| FA-Status | Zeigt den Status des Fertigungsauftrags (z. B. Freigegeben). Über **Beleg anzeigen** wird abhängig von diesem Status der passende Fertigungsauftrag (simuliert, geplant, planfixiert, freigegeben, beendet) geöffnet. |
| FA-Nr. | Wenn gefüllt, verweist die Zeile auf den freigegebenen Fertigungsauftrag; dient als Sprung zum Beleg. |
| FA-Zeilennr. | Identifiziert die Fertigungsauftragszeile innerhalb des Auftrags; nur Anzeige. |
| Reihenfolge | Wenn gesetzt, bestimmt der Wert die Abarbeitungsreihenfolge des Arbeitsgangs am Arbeitsplatz; er wird durch **Reihenfolge übertragen** aus der Werkzeugplanung befüllt. |
| Status | Zeigt den Status des Arbeitsgangs (offen, gestartet, beendet usw.) und steuert, welche Aktionen zulässig sind. |
| Vorheriger Arbeitsgang Status | Zeigt den Status des vorangehenden Arbeitsgangs; hilft zu erkennen, ob die Vorstufe abgeschlossen ist. |
| Arbeitsgangnr. | Identifiziert den Arbeitsgang im Arbeitsplan; nur Anzeige. |
| Arbeitsplatzgruppennr. (Zeile) | Zeigt die Arbeitsplatzgruppe des Arbeitsgangs; nur Anzeige. |
| Personalnummer | Wenn gefüllt, ist der Arbeitsgang einem Mitarbeiter zugeordnet; das Feld ist nur editierbar, wenn die Personalzuordnung in der Basis-App aktiviert ist. |
| Arbeitsplatznr. | Zeigt den Arbeitsplatz (Maschine) des Arbeitsgangs; beim Ändern wird die Zeilendarstellung neu berechnet. |
| Unterbrechungsgrundcode / Unterbrechungsgrundbeschreibung | Wenn ein Arbeitsgang unterbrochen wurde, dokumentieren diese Felder den Grund; sie werden beim Unterbrechen gesetzt. |
| Startdatum / Startzeit | Wenn gefüllt, geben sie an, wann der Arbeitsgang gestartet wurde; nur Anzeige. |
| Fertiggestellte Menge | Zeigt die bereits rückgemeldete Menge des Arbeitsgangs; steigt mit jeder Teil- bzw. Endrückmeldung. |
| Einheitencode | Zeigt die Mengeneinheit der Rückmeldung; nur Anzeige. |
| FA-Artikelnr. / FA-Variantencode / FA-Artikelbeschreibung / FA-Artikelbeschreibung 2 | Beschreiben den zu fertigenden Artikel der Fertigungsauftragszeile; dienen der Identifikation der Arbeit. |
| Letzter Arbeitsgang | Wenn gesetzt, kennzeichnet der Wert den letzten Arbeitsgang der Fertigungsauftragszeile; relevant für den Abschluss. |
| Verkaufsauftragsnr. / Verk. an Deb.- Nr. / Verk. an Deb.- Name | Wenn gefüllt, verknüpfen sie den Arbeitsgang mit dem auslösenden Verkaufsauftrag und Debitor; helfen bei Rückfragen zur Priorität. |
| Sollzeit / Gemeldete Zeit / Offene Zeit / Zeit inkl. Rüsten | Stellen den Zeitfortschritt des Arbeitsgangs dar (geplante, gemeldete und noch offene Zeit einschließlich Rüsten); dienen der Fortschrittskontrolle. |
| Zusteller / Zustellertransportart | Wenn gefüllt, dokumentieren sie Versanddaten der Fertigungsauftragszeile; nur Anzeige. |
| Weitere Arbeitsgang-Kontextspalten (Beschreibung, Beschreibung 2, Vorh. Arbeitsgang Art/Beschr., Nächster Arbeitsgang Art/Beschr. sowie vorheriger/nächster Arbeitsgang und Produktionsmenge) | Diese zusätzlichen Kontextspalten des FA-Arbeitsvorrats beschreiben den Arbeitsgang und seine Nachbararbeitsgänge; sie unterstützen die Einordnung, ohne für die Werkzeugprüfung erforderlich zu sein. |

#### Werkzeugaktionen im FA-Arbeitsvorrat

| Aktion | Erläuterung |
|---|---|
| Benötigte Werkzeuge | Öffnen Sie über die Aktion **Benötigte Werkzeuge** die Liste der für den ausgewählten Arbeitsgang geforderten Werkzeuge (Werkzeugart, Werkzeugnummer, Beschreibung). Wenn der **Werkzeug Status** **Nicht okay** ist, erkennt der Anwender hier, welche Werkzeuge der Arbeitsgang laut Arbeitsplan verlangt. |
| Installierte Werkzeuge | Öffnen Sie über die Aktion **Installierte Werkzeuge** die Ansicht der aktuell am Arbeitsplatz bzw. an der Arbeitsplatzgruppe installierten Werkzeuge. Aus dieser Ansicht heraus lassen sich Werkzeuge über **Werkzeug installieren** ergänzen und über **Werkzeuge deinstallieren** entfernen, sodass sich der **Werkzeug Status** auf **Okay** ändert. |
| Starten (gesteuert durch diese App) | Wenn der **Werkzeug Status** **Nicht okay** ist, ist die Basis-Aktion **Starten** gesperrt; erst wenn die benötigten Werkzeuge installiert sind, lässt sich der Arbeitsgang starten. So verhindert die App den Start eines Arbeitsgangs ohne die erforderliche Werkzeugbestückung. |

Die weiteren Aktionen des FA-Arbeitsvorrats (**Rüsten**, **Unterbrechen**, **Teilbeenden**, **Beenden**, **Erneut öffnen**, **Beleg anzeigen**, **Daten aktualisieren**, **Ereignisverlauf**) stammen aus der Basis-App und werden durch diese Erweiterung nicht verändert.

### Installierte Werkzeuge verwalten (Planungswerkzeug-Liste)

Die Ansicht **Installierte Werkzeuge** (Seite Planungswerkzeug-Liste) wird ausschließlich modal aus dem FA-Arbeitsvorrat über die gleichnamige Aktion geöffnet; sie ist nicht über die Suche erreichbar. Sie zeigt die geplanten Werkzeugbelegungen zur gewählten Zeile und rechts eine Infobox **Installierte Werkzeuge** mit dem Abgleich zwischen benötigten und installierten Werkzeugen.

| Feld | Erläuterung |
|---|---|
| FA-Nr. | Zeigt den Fertigungsauftrag der Zeile; nur Anzeige. |
| FA-Zeilennummer | Identifiziert die Fertigungsauftragszeile; nur Anzeige. |
| Arbeitsgang Nr. | Zeigt den Arbeitsgang, für den die Werkzeuge geplant sind. |
| Arbeitsplatz (Arbeitsplatzgruppe der Zeile) | Zeigt die Arbeitsplatzgruppe des Arbeitsgangs; bestimmt zusammen mit dem Typ das Ziel des Installierens. |
| Arbeitsplatzname / Arbeitsplatzgruppenname | Zeigen die Bezeichnungen der Arbeitsplatzgruppe bzw. des Arbeitsplatzes zur Kontrolle; nur Anzeige. |
| Werkzeugart | Zeigt die Art des Werkzeugs; nur Anzeige. |
| Werkzeugnummer | Zeigt das konkrete Werkzeug; nur Anzeige. |
| WKZ-Zeilennummer | Identifiziert die Werkzeugzeile im Arbeitsplan; nur Anzeige. |
| Typ | **Arbeitsplatzgruppe:** Wenn der Typ Arbeitsplatzgruppe ist, wirken **Werkzeug installieren** / **Werkzeuge deinstallieren** auf die Arbeitsplatzgruppe. **Arbeitsplatz:** Wenn der Typ Arbeitsplatz ist, wirken diese Aktionen auf den einzelnen Arbeitsplatz. Der Typ bestimmt also, auf welcher Ebene das Werkzeug installiert oder entfernt wird. |

| Aktion | Erläuterung |
|---|---|
| Werkzeug installieren | Wenn Sie diese Aktion wählen, wird das ausgewählte Werkzeug je nach **Typ** der Arbeitsplatzgruppe oder dem Arbeitsplatz zugeordnet; anschließend zählt es beim Abgleich als installiert und der **Werkzeug Status** kann auf **Okay** wechseln. |
| Werkzeuge deinstallieren | Wenn Sie diese Aktion wählen, wird die Zuordnung des Werkzeugs zur Arbeitsplatzgruppe bzw. zum Arbeitsplatz entfernt; das Werkzeug gilt dann nicht mehr als installiert. |

Die beiden Aktionen sind unter der Schaltflächengruppe **Werkzeuge verwalten** zusammengefasst.

### Werkzeugreihenfolge im Planungswerkzeug planen

Die Ansicht **Planungswerkzeug** ist über die **Suche** erreichbar. Sie zeigt die geplanten Werkzeugbelegungen der Arbeitsgänge und dient dazu, deren **Reihenfolge** festzulegen und anschließend in den FA-Arbeitsvorrat zu übertragen.

#### Filter im Planungswerkzeug

Wenn ein Filter gesetzt ist, werden die Zeilen entsprechend eingegrenzt.

| Filterfeld | Erläuterung |
|---|---|
| Arbeitsplatzgruppe | Wenn gesetzt, werden nur Werkzeugbelegungen dieser Arbeitsplatzgruppe angezeigt; üblicher Einstieg des Planers. |
| Arbeitsplatz | Wenn gesetzt, wird zusätzlich auf einen einzelnen Arbeitsplatz eingegrenzt; optional. |
| Werkzeugart | Wenn gesetzt, werden nur Belegungen der gewählten Werkzeugart angezeigt; hilfreich, wenn eine bestimmte Werkzeuggruppe geplant wird. |
| Startdatum | Wenn gesetzt, werden nur Belegungen ab diesem Startzeitpunkt angezeigt; grenzt die Planung zeitlich ein. |

#### Spalten im Planungswerkzeug

| Feld | Erläuterung |
|---|---|
| FA-Nr. | Zeigt den Fertigungsauftrag der geplanten Belegung; nur Anzeige. |
| FA-Zeilennummer | Identifiziert die Fertigungsauftragszeile; nur Anzeige. |
| Arbeitsgang Nr. | Zeigt den Arbeitsgang, für den das Werkzeug benötigt wird. |
| Arbeitsplatz (Arbeitsplatzgruppe) | Zeigt die Arbeitsplatzgruppe des Arbeitsgangs; nur Anzeige. |
| Arbeitsplatz (Maschine) | Zeigt den Arbeitsplatz des Arbeitsgangs; nur Anzeige. |
| Werkzeugart | Zeigt die Art des benötigten Werkzeugs; nur Anzeige. |
| Werkzeugnummer | Zeigt das konkrete Werkzeug; nur Anzeige. |
| WKZ-Zeilennummer | Identifiziert die Werkzeugzeile; nur Anzeige. |
| Arbeitsgang Start / Arbeitsgang Ende | Zeigen den geplanten Start- und Endzeitpunkt des Arbeitsgangs; dienen der zeitlichen Einordnung der Reihenfolge. |
| Reihenfolge | Wenn Sie hier einen Wert eingeben, legen Sie die geplante Abarbeitungsreihenfolge der Werkzeugbelegung fest; dieser Wert wird beim Übertragen in den FA-Arbeitsvorrat geschrieben. |

#### Aktionen im Planungswerkzeug

Die Aktionen sind unter der Schaltflächengruppe **Prozess** zusammengefasst.

| Aktion | Erläuterung |
|---|---|
| Reihenfolge in FA-Arbeitsvorrat übertragen | Wenn Sie diese Aktion wählen, wird die im **Planungswerkzeug** vergebene **Reihenfolge** je Arbeitsplatzgruppe fortlaufend nummeriert und in die noch nicht beendeten Arbeitsgänge des FA-Arbeitsvorrats geschrieben; dort erscheint sie in der Spalte **Reihenfolge** und steuert die Abarbeitungsreihenfolge. |
| Installierte Werkzeuge | Wenn Sie diese Aktion wählen, wird die Liste der am Arbeitsplatz installierten Werkzeuge angezeigt, sodass Sie die Planung mit der tatsächlichen Bestückung abgleichen können. |
| Beleg anzeigen | Wenn Sie diese Aktion wählen, wird abhängig vom FA-Status der zugehörige Fertigungsauftrag geöffnet. |
| Arbeitsplan anzeigen | Wenn Sie diese Aktion wählen, wird der Arbeitsplan des Fertigungsauftrags zum gewählten Arbeitsgang geöffnet. |

### Reihenfolge aus der Erf.-Werkzeugplanung übertragen

Die App ergänzt die Ansicht **Erf.-Werkzeugplanung** (Erfassungsblatt der Werkzeugplanung) um die Aktion **Reihenfolge übertragen**. In dieser Ansicht filtert der Planer über **Arbeitsplatzgruppen/Arbeitsplatz Art**, **Arbeitsplatzgruppe / Arbeitsplatz Nummer**, **Werkzeugart** und **Startdatum** und vergibt in den Zeilen die **Reihenfolge**.

| Aktion | Erläuterung |
|---|---|
| Reihenfolge übertragen | Wenn Sie diese Aktion wählen, wird die in der Werkzeugplanung erfasste **Reihenfolge** in die passenden Arbeitsgänge des FA-Arbeitsvorrats übernommen; nach erfolgreicher Übernahme erscheint die Meldung „Die Übertragung der Reihenfolge in den FA-Arbeitsvorrat wurde erfolgreich abgeschlossen“. |

Diese Aktion ist in der Ansicht der Gruppe **Fertigungswerkzeuge** zugeordnet.

## FAQ und Troubleshooting

### 1. Warum steht in der Spalte Werkzeug Status „Nicht okay“?
**Nicht okay** bedeutet, dass mindestens ein für den Arbeitsgang benötigtes Werkzeug am Arbeitsplatz bzw. an der Arbeitsplatzgruppe nicht installiert ist. Vergleichen Sie über **Benötigte Werkzeuge** die Forderung mit den über **Installierte Werkzeuge** angezeigten vorhandenen Werkzeugen und installieren Sie die fehlenden.

### 2. Warum ist die Aktion Starten ausgegraut?
Die App sperrt **Starten**, solange der **Werkzeug Status** **Nicht okay** ist. Sobald alle benötigten Werkzeuge installiert sind und der Status auf **Okay** wechselt, ist **Starten** wieder verfügbar.

### 3. Wie wird der Werkzeug Status ermittelt?
Der Status wird beim Blättern je Zeile automatisch berechnet, indem die im Arbeitsplan des Arbeitsgangs geforderten Werkzeuge mit den am Arbeitsplatz installierten Werkzeugen abgeglichen werden. Stimmen sie überein, erscheint **Okay**, andernfalls **Nicht okay**.

### 4. Wo pflege ich die benötigten Werkzeuge eines Arbeitsgangs?
Die Zuordnung benötigter Werkzeuge zu Arbeitsgängen erfolgt im Arbeitsplan bzw. in der Werkzeugverwaltung der Basis-App m+m Tool Management. Diese Erweiterung zeigt die Forderung über **Benötigte Werkzeuge** nur an.

### 5. Wie installiere ich ein fehlendes Werkzeug am Arbeitsplatz?
Öffnen Sie im FA-Arbeitsvorrat die Aktion **Installierte Werkzeuge**, wählen Sie die Zeile und anschließend **Werkzeug installieren**. Je nach **Typ** wird das Werkzeug der Arbeitsplatzgruppe oder dem einzelnen Arbeitsplatz zugeordnet.

### 6. Was bewirkt „Reihenfolge in FA-Arbeitsvorrat übertragen“?
Die im **Planungswerkzeug** vergebene **Reihenfolge** wird je Arbeitsplatzgruppe fortlaufend nummeriert und in die noch nicht beendeten Arbeitsgänge des FA-Arbeitsvorrats geschrieben. Bereits beendete Arbeitsgänge werden dabei nicht verändert.

### 7. Warum finde ich die „Installierte Werkzeuge“-Liste nicht über die Suche?
Die Ansicht Planungswerkzeug-Liste ist bewusst nicht über die Suche erreichbar. Sie wird ausschließlich modal aus dem FA-Arbeitsvorrat über die Aktion **Installierte Werkzeuge** geöffnet.

### 8. Der FA-Arbeitsvorrat ist leer – woran liegt das?
Es sind keine passenden Arbeitsgänge vorhanden oder die Filter grenzen zu stark ein. Prüfen Sie die **Arbeitsplatzgruppennr.**, entfernen Sie ggf. den Filter **Arbeitsplatznr.** und stellen Sie sicher, dass freigegebene Fertigungsaufträge mit Arbeitsgängen an dieser Arbeitsplatzgruppe existieren.

### 9. Worin unterscheiden sich „Benötigte Werkzeuge“ und „Installierte Werkzeuge“?
**Benötigte Werkzeuge** zeigt, was der Arbeitsgang laut Arbeitsplan verlangt; **Installierte Werkzeuge** zeigt, was tatsächlich am Arbeitsplatz vorhanden ist. Die Differenz beider Listen erklärt einen Status **Nicht okay**.

### 10. Kann ich einen Arbeitsgang teilweise zurückmelden, obwohl noch Restmenge offen ist?
Ja. Die Rückmeldung erfolgt über die Basis-Aktionen **Teilbeenden** (Teilmenge) und **Beenden** (Abschluss). Die Werkzeugerweiterung schränkt dies nicht ein; sie steuert ausschließlich, ob **Starten** zulässig ist.

## Typische Anwendungsfälle (Nutzungsbeispiele)

### Anwendungsfall 1: Werkzeugprüfung vor dem Arbeitsgangstart

**Auslöser:** Der Werker beginnt seine Schicht und möchte den nächsten Arbeitsgang an seiner Arbeitsplatzgruppe starten.

**Einstieg in BC:** Er öffnet über die **Suche** den **FA-Arbeitsvorrat** und trägt seine **Arbeitsplatzgruppennr.** ein; die anstehenden Arbeitsgänge erscheinen.

**Kernablauf:** In der Zeile prüft er die Spalte **Werkzeug Status**. Steht dort **Nicht okay**, öffnet er **Benötigte Werkzeuge** und sieht, welches Werkzeug der Arbeitsgang verlangt. Über **Installierte Werkzeuge** stellt er fest, dass dieses Werkzeug am Arbeitsplatz fehlt, und ergänzt es mit **Werkzeug installieren**. Der Status wechselt auf **Okay**, und die Aktion **Starten** wird verfügbar. Er wählt **Starten** und arbeitet den Arbeitsgang ab.

**Abschluss:** Nach Fertigstellung meldet er den Arbeitsgang über **Teilbeenden** bzw. **Beenden** zurück; die **Fertiggestellte Menge** wird aktualisiert.

### Anwendungsfall 2: Werkzeugreihenfolge planen und übertragen

**Auslöser:** Der Fertigungsplaner möchte für eine Arbeitsplatzgruppe die Reihenfolge der Werkzeugbelegung für den kommenden Tag festlegen.

**Einstieg in BC:** Er öffnet über die **Suche** das **Planungswerkzeug** und filtert auf die **Arbeitsplatzgruppe**, ggf. auf **Arbeitsplatz**, **Werkzeugart** und **Startdatum**.

**Kernablauf:** In den Zeilen vergibt er in der Spalte **Reihenfolge** die gewünschte Abfolge. Anschließend wählt er **Reihenfolge in FA-Arbeitsvorrat übertragen**. Die App nummeriert die Reihenfolge je Arbeitsplatzgruppe fortlaufend und schreibt sie in die noch offenen Arbeitsgänge des FA-Arbeitsvorrats.

**Abschluss:** Im **FA-Arbeitsvorrat** erscheint die Spalte **Reihenfolge** gefüllt; die Werker können die Arbeitsgänge in der geplanten Abfolge abarbeiten.

### Anwendungsfall 3: Reihenfolge aus der Werkzeugplanung übernehmen

**Auslöser:** Der Planer pflegt die Werkzeugplanung in der Ansicht **Erf.-Werkzeugplanung** und möchte die dort festgelegte Reihenfolge direkt in den Arbeitsvorrat übernehmen.

**Einstieg in BC:** Er öffnet über die **Suche** die **Erf.-Werkzeugplanung** und grenzt über **Arbeitsplatzgruppen/Arbeitsplatz Art**, **Arbeitsplatzgruppe / Arbeitsplatz Nummer**, **Werkzeugart** und **Startdatum** ein.

**Kernablauf:** Nach dem Erfassen der **Reihenfolge** in den Zeilen wählt er in der Gruppe **Fertigungswerkzeuge** die Aktion **Reihenfolge übertragen**. Die App überträgt die Reihenfolge in die passenden Arbeitsgänge des FA-Arbeitsvorrats.

**Abschluss:** Es erscheint die Bestätigung „Die Übertragung der Reihenfolge in den FA-Arbeitsvorrat wurde erfolgreich abgeschlossen“. Die Reihenfolge steht anschließend im **FA-Arbeitsvorrat** zur Verfügung.
