---
title: Anwenderhandbuch m+m Master Data Management
---

# Anwenderhandbuch m+m Master Data Management

## Einleitung

Die Erweiterung **m+m Master Data Management** (Zentralmandant) ermöglicht es, ausgewählte Stammdaten **zwischen mehreren Mandanten** in Microsoft Dynamics 365 Business Central automatisch synchron zu halten. Ändert ein Anwender beispielsweise den Namen eines **Debitors** in einem Mandanten, wird diese Änderung in einen oder mehrere andere Mandanten übernommen – ohne dass der Datensatz dort erneut manuell bearbeitet werden muss.

Der Abgleich erfolgt **feldgenau**: Sie legen fest, welche Felder welcher Tabellen zwischen welchen Mandanten übertragen werden. Der Austausch kann **bidirektional** (alle beteiligten Mandanten werden auf demselben Stand gehalten) oder **von oben nach unten** (ein führender Mastermandant verteilt seine Daten an die übrigen Mandanten) erfolgen. Ziel- und Quellmandanten sind frei kombinierbar; die Zielmandanten können sich in derselben oder in einer anderen Business-Central-Datenbank befinden. Nach der einmaligen Einrichtung läuft der Datenabgleich vollautomatisch.

### Zielgruppe

Primäre Zielgruppe sind **operative Key-User und Administratoren**, die in mehreren Mandanten arbeiten und den täglichen Datenstand konsistent halten müssen – etwa die Debitoren-, Kreditoren- oder Artikelverwaltung, die eine Änderung in einem Mandanten pflegt und erwartet, dass sie in den übrigen Mandanten ankommt. Sekundär richtet sich das Handbuch an die **Systemadministration**, die die einmalige Einrichtung (Zentralmandanteinrichtung, Übertragungsdienst, Berechtigungen) vornimmt.

### Kurzer Prozessüberblick

1. **Zentralmandanteinrichtung** einmalig aktivieren und die Verbindungsdaten (Autorisierung) hinterlegen; über die Aktion **Initialisieren** die freigegebenen Tabellen bereitstellen.
2. **Übertragungsdienst** anlegen, der die Zieldatenbank und die Authentifizierung beschreibt.
3. Eine **Zentralmandantübertragung** definieren: Synchronisierungsart, beteiligte Mandanten (**Zentralmandantzuweisung**), zu übertragende **Übertragungsfelder** und optionale **Mandantenfilter**.
4. Optional bestehende Bestandsdaten über die **Mandanten-Initialisierung** in neue Mandanten kopieren.
5. Laufenden Betrieb über **Asynchrones Protokoll** und **Zentralmandantübertragungsfehlerprotokoll** überwachen und Fehler nachziehen.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg von der Einrichtung bis zur ersten laufenden Synchronisation. Die Schritte folgen der technischen Abhängigkeitsreihenfolge (zuerst Einrichtung, dann Konfiguration, dann Betrieb).

1. **Zentralmandanteinrichtung öffnen.** Öffnen Sie über die **Suche** die Seite **Zentralmandanteinrichtung**. Setzen Sie **Aktiv** auf „Ja“, wählen Sie unter **Autorisierung** die Anmeldeart (**Basic** oder **OAuth**) und hinterlegen Sie die zugehörigen Anmeldedaten.
2. **Initialisieren.** Wählen Sie in der Zentralmandanteinrichtung die Aktion **Initialisieren**. Danach stehen die freigegebenen Tabellen für die Auswahl in den Übertragungen zur Verfügung. Diese Aktion ist nur einmalig auszuführen.
3. **Übertragungsdienst anlegen.** Öffnen Sie über die **Suche** die **Übertragungsdienstliste**, legen Sie einen Datensatz an, hinterlegen Sie **Code**, **ODataV4 Adresse** und die **Autorisierung**. Prüfen Sie die Verbindung mit **Verbindung testen**.
4. **Zentralmandantübertragung anlegen.** Öffnen Sie über die **Suche** die **Zentralmandantübertragungen** und legen Sie einen neuen Datensatz an. Öffnen Sie die Zeile, um die **Zentralmandantübertragungskarte** zu bearbeiten. Erfassen Sie **Code**, **Beschreibung**, **Übertragungsdienstcode** und die **Synchronisierungsart**.
5. **Mandanten zuweisen.** Fügen Sie im Bereich **Zentralmandantzuweisung** die beteiligten Mandanten hinzu. Bei der Synchronisierungsart **Von Oben nach unten** aktivieren Sie bei genau einem Mandanten das Kennzeichen **Master**.
6. **Felder wählen.** Wählen Sie im Bereich **Übertragungsfelder** die Tabellen und Felder aus. Mit **Alle Felder einfügen** übernehmen Sie alle Felder einer Tabelle auf einmal.
7. **Aktiv setzen.** Setzen Sie die Übertragung im Kopf auf **Aktiv**. Ab jetzt werden Änderungen an den gewählten Feldern automatisch übertragen.
8. **Optional – Bestandsdaten kopieren.** Wählen Sie in den **Zentralmandantübertragungen** die Aktion **Mandanten-Initialisierung**, legen Sie eine **Mandantenerstellung** an, definieren Sie **Herkunfts-** und **Zielmandant** je Zeile und starten Sie mit **Asynchrone Verarbeitung**.
9. **Überwachen.** Prüfen Sie bei Bedarf das **Zentralmandantübertragungsfehlerprotokoll**; korrigieren Sie fehlgeschlagene Zeilen und stoßen Sie sie mit **Erneut versuchen** bzw. **Daten Senden** neu an.

☞ Sämtliche Zentralmandanteinrichtungen sind **mandantenübergreifend** und nur einmalig vorzunehmen.

## Einrichtung

Die Einrichtung ist die Grundlage des Moduls und wird von der **Systemadministration** vor der ersten Nutzung durchgeführt. Sie umfasst die globale **Zentralmandanteinrichtung**, mindestens einen **Übertragungsdienst**, die Festlegung der **Verantwortlichen** für Benachrichtigungen sowie die **Berechtigungen**.

### Zentralmandanteinrichtung

**Prozess.** Die Zentralmandanteinrichtung ist eine **mandantenübergreifende Einzelkarte** (ein Datensatz für alle Mandanten). Der Administrator hinterlegt hier, ob das Modul aktiv ist, mit welcher Autorisierung Daten zwischen den Mandanten ausgetauscht werden und ob der Austausch asynchron über Aufgabenwarteschlangen erfolgen soll. Erst wenn **Aktiv** gesetzt ist, werden Änderungen tatsächlich übertragen; die konkrete Nutzung erfolgt später in den **Zentralmandantübertragungen** (siehe Kapitel *Zentralmandantübertragungen einrichten*).

**Einstieg:** Öffnen Sie über die **Suche** die Seite **Zentralmandanteinrichtung**.

Erläuterungen zu den Feldern der Karte **Zentralmandanteinrichtung**:

| Einrichtung | Erläuterung |
|---|---|
| **Aktiv** | Wenn aktiviert, führt das Modul den Datenaustausch tatsächlich aus; ohne dieses Kennzeichen werden Änderungen an freigegebenen Feldern **nicht** an andere Mandanten gesendet. Dies ist der zentrale Ein-/Ausschalter des gesamten Moduls. |
| **Erfolgsmeldung protokollieren** | Wenn aktiviert, wird zusätzlich zu Fehlern **auch jede erfolgreiche Übertragung** im Fehlerprotokoll vermerkt. Nutzen Sie dies zur Nachvollziehbarkeit in der Einführungsphase; im Dauerbetrieb erzeugt es viele Einträge und bleibt in der Regel deaktiviert. |
| **Autorisierung** | Legt fest, wie sich das Modul an der Zieldatenbank anmeldet. Wählen Sie den Wert je Anmeldeart (siehe folgende Werteliste). Die Auswahl blendet die passenden Anmeldefelder ein. |
| **Übertragungsbenutzer** | Wenn gesetzt, meldet sich das Modul bei **Basic**-Autorisierung mit diesem Benutzerkonto an. Der Benutzer muss in **allen** Mandanten SUPER-Rechte besitzen; andernfalls wird die Eingabe abgewiesen. |
| **Passwort** | Wenn gesetzt, dient dieses Kennwort zusammen mit dem Übertragungsbenutzer der **Basic**-Anmeldung. Ohne Übertragungsbenutzer ist keine Eingabe möglich. |
| **Abweichende ODataV4 Adresse** | Wenn gesetzt, verwendet das Modul diese Serverport-/Endpunktadresse für die Web-Service-Aufrufe, statt der Standardadresse der Umgebung. Nutzen Sie dies, wenn die Zieldatenbank über eine abweichende OData-Adresse erreichbar ist. |
| **Asynchroner Betrieb** | Wenn aktiviert, werden Datenänderungen nicht sofort synchron gesendet, sondern für eine spätere Verarbeitung vorgemerkt. In Kombination mit der Asynchronen Option steuert dies, wie Übertragungen zeitversetzt ausgeführt werden. |
| **Asynchrone Option** | Legt das Verfahren des zeitversetzten Versands fest (siehe folgende Werteliste). Bei Auswahl **Aufgabenwarteschlange** erscheint ein Hinweis, dass in jedem beteiligten Mandanten eine Aufgabenwarteschlange eingerichtet werden muss. |
| **Startdatum/-uhrzeit Asynchroner Option** | Wenn gesetzt, starten die asynchronen Aufgabenwarteschlangen ab diesem Zeitpunkt. Das Feld ist nur bei der Asynchronen Option **Aufgabenwarteschlange** aktiv; der Zeitpunkt muss in der Zukunft liegen. |
| **Client-ID** | Wenn **OAuth** gewählt ist: die Anwendungs-ID (Client-ID) der registrierten Azure-App, mit der sich das Modul anmeldet. Pflichtfeld für OAuth. |
| **Geheimer Clientschlüssel** | Wenn **OAuth** gewählt ist: das Client-Geheimnis der App. Pflichtfeld für OAuth; wird maskiert gespeichert. |
| **Autorisierungs-URL** | Wenn **OAuth** gewählt ist: die Endpunktadresse, unter der das Zugriffstoken angefordert wird. Pflichtfeld für OAuth. |

**Werte der Option Autorisierung** (Task-relevante Bedeutung je Wert):

- **Basic:** Anmeldung mit **Übertragungsbenutzer** und **Passwort**. Es werden die Basic-Felder eingeblendet; OAuth-Felder werden geleert.
- **OAuth:** Anmeldung über **Client-ID**, **Geheimer Clientschlüssel** und **Autorisierungs-URL**. Es werden die OAuth-Felder eingeblendet; die Basic-Felder werden geleert.

**Werte der Asynchronen Option:**

- **Standard:** Vorgemerkte Änderungen werden über eine einmalige Hintergrundaufgabe versendet, sobald sie anfallen. Es ist keine dauerhafte Aufgabenwarteschlange je Mandant nötig.
- **Aufgabenwarteschlange:** Der Versand erfolgt über wiederkehrende Aufgabenwarteschlangen, die **in jedem beteiligten Mandanten** eingerichtet werden müssen. Beachten Sie: Vergibt in der Zwischenzeit ein anderer Mandant denselben Wert, können die Daten auseinanderlaufen – diese Option ist mit Bedacht zu wählen.

Erläuterungen zu den Aktionen der Karte **Zentralmandanteinrichtung**:

| Aktion | Erläuterung |
|---|---|
| **Initialisieren** | Wenn ausgeführt, werden alle für das Modul zugelassenen Tabellen eingefügt und der interne Web-Service registriert; bei aktivem asynchronem Betrieb werden zusätzlich die Aufgabenwarteschlangen in den beteiligten Mandanten vorbereitet. Diese Aktion ist einmalig auszuführen, damit anschließend in den Übertragungen Tabellen ausgewählt werden können. |

**Ablauf der Erstaktivierung (in Abhängigkeitsreihenfolge):**
1. **Zuerst** **Aktiv** setzen und **Autorisierung** samt Anmeldedaten hinterlegen. Wenn dies fehlt, findet trotz definierter Übertragungen keine Datenübertragung statt.
2. **Danach** die Aktion **Initialisieren** ausführen, damit die zugelassenen Tabellen bereitstehen.
3. **Schließlich** – bei gewünschtem zeitversetztem Betrieb – **Asynchroner Betrieb** und **Asynchrone Option** setzen und ggf. die **Startdatum/-uhrzeit Asynchroner Option** festlegen.

☞ Zulassungsregel: Nicht jede Tabelle darf synchronisiert werden. Die Aktion **Initialisieren** stellt die zulässigen Tabellen bereit (z. B. **Debitor**, **Kreditor**, **Artikel**, **Kontakt**, **Sachkonto** sowie zugehörige Stammtabellen); andere Tabellen sind zur Wahrung der Datenkonsistenz ausgenommen.

### Übertragungsdienst einrichten

**Prozess.** Ein **Übertragungsdienst** beschreibt **eine Zieldatenbank** samt Authentifizierung. Er wird vom Administrator vor der ersten Übertragung angelegt und später in der **Zentralmandantübertragungskarte** (Feld **Übertragungsdienstcode**) sowie je Mandant in der **Zentralmandantzuweisung** referenziert. Für Übertragungen innerhalb derselben Datenbank kann der Dienst als **Gleiche Datenbank** gekennzeichnet werden; für eine getrennte Ziel-Umgebung hinterlegen Sie deren OData-Adresse und Anmeldung.

**Einstieg:** Öffnen Sie über die **Suche** die **Übertragungsdienstliste** und öffnen Sie mit „Neu“ die **Übertragungsdienstkarte**.

Erläuterungen zu den Feldern der **Übertragungsdienstkarte**:

| Einrichtung | Erläuterung |
|---|---|
| **Code** | Wenn gesetzt, identifiziert dieser eindeutige Code den Dienst; unter diesem Code wird er in Übertragungen und Zuweisungen ausgewählt. Pflichtfeld. |
| **Beschreibung** | Wenn gesetzt, erleichtert der erläuternde Text die Auswahl des richtigen Dienstes in Listen. |
| **ODataV4 Adresse** | Wenn gesetzt, sendet das Modul die Übertragungen an diese OData-V4-Endpunktadresse der Zieldatenbank. |
| **Standard** | Wenn aktiviert, gilt dieser Dienst als voreingestellter Dienst und wird herangezogen, wenn an anderer Stelle kein abweichender Dienst gewählt ist. Es ist nur **ein** Standarddienst zulässig; ein zweiter wird abgewiesen. |
| **Gleiche Datenbank** | Wenn aktiviert, zeigt der Dienst auf **dieselbe** Datenbank; Protokolleinträge werden dann nur einmal erstellt, um Duplikate zu vermeiden. Nutzen Sie dies bei mandantenübergreifender Synchronisation innerhalb einer Umgebung. |
| **Autorisierung** | Legt die Anmeldeart fest (**Basic** oder **OAuth**); die Auswahl blendet die passende Feldgruppe ein und leert die jeweils andere. |
| **Übertragungsbenutzer** | Wenn **Basic** gewählt ist: Benutzername für die Anmeldung an der Zieldatenbank. Der Benutzer muss SUPER-Rechte in allen Mandanten besitzen. |
| **Passwort** | Wenn **Basic** gewählt ist: zugehöriges Kennwort; nur zusammen mit dem Übertragungsbenutzer erfassbar. |
| **Client-ID** | Wenn **OAuth** gewählt ist: Anwendungs-ID (Client-ID) für die OAuth-Anmeldung. |
| **Geheimer Clientschlüssel** | Wenn **OAuth** gewählt ist: Client-Geheimnis; wird maskiert gespeichert und nur zusammen mit der Client-ID erfasst. |
| **Autorisierungs-URL** | Wenn **OAuth** gewählt ist: Autoritäts-URL, unter der das Token angefordert wird (z. B. der Microsoft-Anmeldeendpunkt des Mandanten). |
| **Bereich** | Wenn **OAuth** gewählt ist: der angeforderte OAuth-Bereich (Scope) für den Zugriff auf die Business-Central-API. |

**Werte der Feldgruppen Basisauthentifizierung / OAuth:** Die Gruppe **Basisauthentifizierung** ist nur sichtbar, wenn **Autorisierung = Basic**; die Gruppe **OAuth** nur, wenn **Autorisierung = OAuth**. Es wird stets genau eine Gruppe angezeigt.

Aktion der **Übertragungsdienstkarte**:

| Aktion | Erläuterung |
|---|---|
| **Verbindung testen** | Wenn ausgeführt, prüft das Modul zunächst die Vollständigkeit der Anmeldedaten und stellt anschließend eine Testverbindung zur Zieldatenbank her. Bei Erfolg erscheint eine Bestätigung, andernfalls ein Fehlertext mit Ursache. Führen Sie den Test aus, bevor Sie den Dienst produktiv einsetzen. |

Die **Übertragungsdienstliste** zeigt die Dienste im Überblick:

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger Code des Dienstes. |
| **Beschreibung** | Erläuternder Text zur schnellen Auswahl. |
| **ODataV4 Adresse** | Zieladresse der Übertragung. |
| **Autorisierung** | Anmeldeart (Basic/OAuth) des Dienstes. |
| **Standard** | Kennzeichnet den voreingestellten Dienst. |

☞ Ein Übertragungsdienst kann nicht gelöscht werden, solange er von einer oder mehreren Zentralmandantübertragungen verwendet wird.

**Beziehung zur Zentralmandanteinrichtung:** Sind in der Zentralmandanteinrichtung Autorisierung und Anmeldedaten vollständig gepflegt, erzeugt bzw. aktualisiert das Modul automatisch einen Standard-Übertragungsdienst mit dem Code **DEFAULT**. Übertragungen ohne eigenen Übertragungsdienstcode verwenden diesen Standarddienst.

### Verantwortliche und Benachrichtigungen (Benutzer Einrichtung)

**Prozess.** Damit die richtigen Personen über fehlgeschlagene Übertragungen und über abgekündigte Felder informiert werden, kennzeichnet der Administrator zuständige Benutzer in der **Benutzer Einrichtung**. Die Kennzeichen steuern den E-Mail-Versand aus dem laufenden Betrieb (siehe Kapitel *Asynchroner Betrieb und Protokolle*).

**Einstieg:** Öffnen Sie über die **Suche** die **Benutzer Einrichtung** und wählen Sie die Zeile des zuständigen Benutzers.

| Einrichtung | Erläuterung |
|---|---|
| **Zentralmandant Verantwortlicher** | Wenn aktiviert, erhält dieser Benutzer eine E-Mail, sobald eine Übertragung fehlschlägt und ein Eintrag im Fehlerprotokoll entsteht. Voraussetzung ist eine hinterlegte **E-Mail**-Adresse in der Benutzerzeile; ohne E-Mail wird das Setzen des Kennzeichens abgewiesen. |
| **Zentralmandant Empfänger obsolete Felder** | Wenn aktiviert, erhält dieser Benutzer eine regelmäßige E-Mail über Tabellen und Felder, die abgekündigt wurden oder nicht mehr in der Datenbank existieren. Beim Aktivieren wird automatisch eine wiederkehrende Aufgabenwarteschlange für den Versand angelegt. Auch hier ist eine E-Mail-Adresse Voraussetzung. |

**Ablauf:** **Zuerst** in der Benutzerzeile eine **E-Mail**-Adresse hinterlegen, **danach** das jeweilige Kennzeichen aktivieren. Ohne E-Mail-Adresse ist die Aktivierung nicht möglich.

### Berechtigungen

Für die Nutzung des Moduls steht ein Berechtigungssatz zur Verfügung, der den Zugriff auf die Tabellen, Seiten und Verarbeitungen des Moduls bündelt. Der Berechtigungssatz **legt fest, welche Aktionen die Anwender im Modul ausführen können** – vom Lesen der Übertragungen bis zum Anlegen und Ändern der Konfiguration. Weisen Sie ihn den Benutzern zu, die Zentralmandantübertragungen einrichten oder überwachen.

☞ Unabhängig vom Berechtigungssatz muss der in der Einrichtung bzw. im Übertragungsdienst hinterlegte **Übertragungsbenutzer** in **allen** beteiligten Mandanten SUPER-Rechte besitzen, da er den mandantenübergreifenden Datenaustausch technisch ausführt.

## Zentralmandantübertragungen einrichten

Eine **Zentralmandantübertragung** ist die eigentliche Konfiguration einer Synchronisation. Sie bündelt in einer Karte drei Bereiche: den **Kopf** (Grundangaben und Synchronisierungsart), die **Zentralmandantzuweisung** (welche Mandanten teilnehmen) und die **Übertragungsfelder** (welche Felder welcher Tabellen übertragen werden). Zusätzlich lässt sich je Mandant ein **Mandantenfilter** hinterlegen.

**Steuernde Vorbedingungen.** Diese Konfiguration wird durch die **Zentralmandanteinrichtung** (Aktivierung, Autorisierung, asynchroner Betrieb) und den gewählten **Übertragungsdienst** (Zieldatenbank, Authentifizierung) gesteuert. Ist das Modul nicht **Aktiv** oder fehlen Anmeldedaten, werden trotz vollständiger Übertragung keine Daten gesendet. Richten Sie daher zuerst die Einrichtung und den Übertragungsdienst ein (siehe Kapitel *Einrichtung*).

**Einstieg:** Öffnen Sie über die **Suche** die **Zentralmandantübertragungen**. Legen Sie eine neue Zeile an und öffnen Sie sie, um die **Zentralmandantübertragungskarte** zu bearbeiten.

Die Übersicht **Zentralmandantübertragungen** zeigt:

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutiger Name der Übertragung; darüber wird sie in allen weiteren Schritten referenziert. |
| **Beschreibung** | Erläuternder Text zur Übertragung. |
| **Synchronisierungsart** | Zeigt, ob bidirektional oder von oben nach unten synchronisiert wird (Details siehe Kopf). |

### Kopf der Übertragung (Bereich Allgemein)

| Feld | Erläuterung |
|---|---|
| **Code** | Wenn gesetzt, dient dieser eindeutige Code als Schlüssel der Übertragung; auf ihn beziehen sich Zuweisungen, Felder und Filter. |
| **Beschreibung** | Wenn gesetzt, erleichtert die Beschreibung die Wiedererkennung der Übertragung in Listen und in der Mandantenerstellung. |
| **Übertragungsdienstcode** | Wenn gesetzt, wird über diesen Übertragungsdienst (Zieldatenbank + Anmeldung) synchronisiert. Beim Ändern prüft das Modul, dass dieselbe Tabelle desselben Mandanten nicht bereits in einer anderen Übertragung mit demselben Dienst konfiguriert ist – so werden doppelte, widersprüchliche Übertragungen verhindert. |
| **Synchronisierungsart** | Legt die Übertragungsrichtung fest (siehe Werteliste). Die Auswahl bestimmt, ob ein Mastermandant erforderlich ist. |
| **Initialisierungsreihenfolge** | Wenn gesetzt (Wert ungleich 0), nimmt diese Übertragung an der **Mandanten-Initialisierung** teil und wird in dieser Reihenfolge abgearbeitet. Der Wert muss eindeutig sein; ein doppelter Wert wird abgewiesen. Bleibt das Feld 0, wird die Übertragung bei der Initialisierung übersprungen. |
| **Aktiv** | Wenn aktiviert, ist die Übertragung scharf geschaltet und Feldänderungen werden übertragen; beim Aktivieren wird der Zeitpunkt in **Aktiv ab** festgehalten. Ohne dieses Kennzeichen bleibt die Konfiguration wirkungslos. |
| **Aktiv ab** | Zeigt automatisch den Zeitpunkt, ab dem die Übertragung aktiv gesetzt wurde (nicht editierbar). |

**Werte der Synchronisierungsart:**

- **Bidirektional:** Die Daten werden in **allen** beteiligten Mandanten auf demselben Stand gehalten. Eine Änderung in einem beliebigen Mandanten wird an die übrigen verteilt. Geeignet, wenn alle Mandanten denselben Datenbestand führen sollen. Bei dieser Art darf **kein** Mastermandant gesetzt sein; ist noch einer vorhanden, ist er zu entfernen.
- **Von Oben nach unten:** Nur die Änderungen des **Mastermandanten** werden in die übrigen (Ziel-)Mandanten kopiert. Änderungen in den untergeordneten Mandanten werden **nicht** weiterverteilt. Geeignet, wenn es einen führenden Mandanten gibt und die übrigen Mandanten Feldinhalte individuell anpassen dürfen. Bei dieser Art ist genau **ein** Mastermandant zu definieren.

☞ Es werden ausschließlich die in den **Übertragungsfeldern** hinterlegten Felder übertragen.

### Zentralmandantzuweisung

**Prozess.** In der Zentralmandantzuweisung legt der Administrator fest, **welche Mandanten** an dieser Übertragung teilnehmen und – bei „Von Oben nach unten“ – welcher Mandant der Quell-/Mastermandant ist. Je Mandant kann ein abweichender Übertragungsdienst und ein Mandantenfilter hinterlegt werden.

| Feld | Erläuterung |
|---|---|
| **Mandantenname** | Wenn gesetzt, nimmt dieser Mandant an der Übertragung teil. Über den Lookup wählen Sie einen lokalen Mandanten oder – bei hinterlegtem Übertragungsdienst – einen Mandanten der Zieldatenbank. Mandantennamen mit Sonderzeichen werden abgewiesen. |
| **Master** | Wenn aktiviert, ist dieser Mandant der **Quellmandant**, aus dem bei „Von Oben nach unten“ die Daten verteilt werden; alle übrigen Mandanten sind automatisch Zielmandanten. Das Kennzeichen ist nur bei der Synchronisierungsart **Von Oben nach unten** zulässig, und es darf immer nur **einen** Mastermandanten geben. Soll der Master später gewechselt werden, ist die gesamte Übertragung neu anzulegen. |
| **Übertragungsdienstcode** | Wenn gesetzt, verwendet dieser Mandant einen **abweichenden** Übertragungsdienst; ist das Feld leer, gilt der Dienst aus dem Kopf bzw. es werden eigene (lokale) Mandanten angezeigt. Nutzen Sie dies, wenn einzelne Zielmandanten in einer anderen Datenbank liegen. |
| **Filter vorhanden** | Zeigt an, ob für diesen Mandanten über die Aktion **Mandantenfilter** bereits ein Filter eingerichtet wurde (nicht editierbar). |
| **Aufgabenwarteschlange - Status** | Zeigt bei asynchronem Betrieb den aktuellen Status der zugehörigen Aufgabenwarteschlange des Mandanten (siehe Werteliste); dient der Überwachung, ob der Versand läuft. |

**Werte des Aufgabenwarteschlange-Status:** **Bereit** (Aufgabe kann starten), **In Bearbeitung** (Versand läuft), **Fehler** (Ausführung fehlgeschlagen), **Abwarten** (angehalten – z. B. bis zur Freigabe), **Beendet** (abgeschlossen), **Abwarten mit Leerlaufzeitlimit** (angehalten wegen Zeitlimit bei Inaktivität).

Aktion der Zentralmandantzuweisung:

| Aktion | Erläuterung |
|---|---|
| **Mandantenfilter** | Wenn ausgeführt, öffnet sich der **Zentralmandanttabellenfilter** für den markierten Mandanten dieser Übertragung. Dort schränken Sie ein, welche Datensätze vor der Übertragung berücksichtigt werden (siehe Abschnitt *Mandantenfilter*). |

**Einstieg für den Mandantenfilter:** Öffnen Sie in der **Zentralmandantzuweisung** die gewünschte Zeile und wählen Sie die Aktion **Mandantenfilter**.

### Übertragungsfelder

**Prozess.** Hier definiert der Administrator **feldgenau**, welche Felder welcher Tabellen synchronisiert werden. Erst nach der Aktion **Initialisieren** (Zentralmandanteinrichtung) stehen die zulässigen Tabellen zur Auswahl.

| Feld | Erläuterung |
|---|---|
| **Tabellen-Nr.** | Wenn gesetzt, wird aus dieser Tabelle das gewählte Feld übertragen. Eine Tabelle darf innerhalb einer Übertragung nur **einmal** verwendet werden; so werden Endlosschleifen und Inkonsistenzen vermieden. |
| **Tabellenbezeichnung** | Zeigt den Namen der gewählten Tabelle (nicht editierbar). |
| **Feld-Nr.** | Wenn gesetzt, wird dieses Feld zwischen den Mandanten synchronisiert. Über den Drilldown wählen Sie das Feld aus der Tabelle; es stehen normale, nicht abgekündigte Felder zur Verfügung. |
| **Feldbezeichnung** | Zeigt den Namen des gewählten Feldes (nicht editierbar). |
| **Primärschlüsselfeld** | Zeigt an, ob das Feld Teil des Primärschlüssels der Tabelle ist. Diese Felder identifizieren den Datensatz und werden zur Zuordnung im Zielmandanten benötigt. |
| **Wert validieren** | Wenn aktiviert, wird beim Übertragen des Wertes im Zielmandanten die zum Feld hinterlegte Prüf-/Validierungslogik ausgeführt (z. B. Prüfung auf Zulässigkeit). Ohne dieses Kennzeichen wird der Wert ohne Zusatzprüfung geschrieben. Aktivieren Sie es, um Inkonsistenzen zu vermeiden. |
| **Abkündigungsstatus** | Zeigt an, ob das Feld in der Datenbank abgekündigt („Pending“) oder entfernt („Removed“) wurde. Ein Wert weist darauf hin, dass die Übertragung dieses Feldes zu prüfen ist. *(Hinweis: Die Statuswerte „Pending“/„Removed“ werden in der aktuellen Auslieferung in englischer Form angezeigt.)* |

Aktionen der Übertragungsfelder:

| Aktion | Erläuterung |
|---|---|
| **Alle Felder einfügen** | Wenn ausgeführt, übernimmt das Modul alle normalen, aktiven und nicht abgekündigten Nicht-Schlüsselfelder der Tabelle auf einmal in die Übertragungsfelder. Nutzen Sie dies, wenn nahezu die gesamte Tabelle synchronisiert werden soll, statt jedes Feld einzeln zu wählen. |
| **Verbundene Tabellen und Felder anzeigen/einfügen** | Wenn ausgeführt, zeigt das Modul in einer Baumdarstellung die mit der gewählten Tabelle über Tabellenrelationen verbundenen Tabellen und Felder an und ermöglicht deren Übernahme. So stellen Sie sicher, dass abhängige Stammtabellen (z. B. verknüpfte Codes) ebenfalls synchronisiert werden. |

Die Seite **Verbundene Tabellenfilter** (Baumansicht) hebt farblich hervor, welche verbundenen Einträge bereits in der Übertragung enthalten sind und welche fehlen; mit **Alle Felder anzeigen** heben Sie eine gesetzte Filterung wieder auf. Die Hilfsseiten **Felder** und **Tabellen** dienen ausschließlich der Auswahl bzw. Prüfung abgekündigter Objekte über die Drilldowns.

**Ablauf der Feldauswahl (in Reihenfolge):**
1. **Zuerst** die Tabelle über **Tabellen-Nr.** wählen (nur zugelassene Tabellen).
2. **Danach** je Feld die **Feld-Nr.** wählen oder mit **Alle Felder einfügen** übernehmen.
3. Optional **Verbundene Tabellen und Felder anzeigen/einfügen** nutzen, um abhängige Tabellen zu ergänzen.
4. Für sensible Felder **Wert validieren** aktivieren.

### Mandantenfilter (Zentralmandanttabellenfilter)

**Prozess.** Für jeden in der Zentralmandantzuweisung hinterlegten Mandanten kann festgelegt werden, **welche Datensätze** vor der Übertragung berücksichtigt werden. So werden z. B. nur Debitoren eines bestimmten Ortes synchronisiert.

**Einstieg:** Öffnen Sie in der **Zentralmandantzuweisung** die Zeile des Mandanten und wählen Sie die Aktion **Mandantenfilter**. Es öffnet sich der **Zentralmandanttabellenfilter**.

| Feld | Erläuterung |
|---|---|
| **Tabellen-Nr.** | Wenn gesetzt, wird der Filter auf Datensätze dieser Tabelle vor der Synchronisation angewendet. Es stehen die in den Übertragungsfeldern verwendeten Tabellen zur Auswahl. |
| **Tabellenbezeichnung** | Zeigt den Namen der Tabelle (nicht editierbar). |
| **Feld-Nr.** | Wenn gesetzt, wird der Filter auf dieses Feld angewendet. Über den Drilldown wählen Sie das Feld. |
| **Feldbezeichnung** | Zeigt den Namen des Feldes (nicht editierbar). |
| **Filterausdruck** | Legt die Vergleichsart fest, mit der der Filterwert geprüft wird (siehe Werteliste). Für Vergleiche wie „kleiner“/„größer“ sind nur numerische, Datums- oder Zeitfelder zulässig; andernfalls wird die Eingabe abgewiesen. |
| **Filterwert** | Wenn gesetzt, werden nur Datensätze übertragen, deren Feldwert der Bedingung entspricht. Für Felder mit Tabellenbezug, Ja/Nein- oder Optionsfeldern bietet der Lookup die zulässigen Werte an. |

**Werte des Filterausdrucks:** **=** (gleich), **<** (kleiner), **>** (größer), **=<** (kleiner oder gleich), **>=** (größer oder gleich), **<>** (ungleich).

☞ Je Tabelle kann jedes Feld nur **einmal** als Filter verwendet werden; mehrere Filterbedingungen über verschiedene Felder sind möglich.

## Mandanten-Initialisierung

**Prozess.** Beim Aufbau eines **neuen** Mandanten sind zunächst keine Stammdaten vorhanden. Die Mandanten-Initialisierung kopiert die in den Übertragungen definierten Bestandsdaten **einmalig** vom Herkunfts- in den Zielmandanten – in einer definierten Reihenfolge (z. B. zuerst Debitoren, dann abhängige Tabellen). Sie ergänzt die laufende Synchronisation um den erstmaligen Grunddatenbestand.

**Voraussetzung.** Es teilnehmen nur Übertragungen mit einer **Initialisierungsreihenfolge** ungleich 0 (siehe Kopf der Übertragung). Der Herkunftsmandant entspricht bei „Von Oben nach unten“ dem Mastermandanten.

**Einstieg:** Öffnen Sie über die **Suche** die **Zentralmandantübertragungen** und wählen Sie die Aktion **Mandanten-Initialisierung**. Es öffnet sich die **Mandantenerstellung Liste**; öffnen Sie eine Zeile für die **Mandantenerstellung Karte**.

Felder der **Mandantenerstellung** (Kopf):

| Feld | Erläuterung |
|---|---|
| **Reihenfolge** | Zeigt die automatisch vergebene, fortlaufende Nummer des Initialisierungslaufs (nicht editierbar). |
| **Beschreibung** | Wenn gesetzt, benennt der Text den Zweck des Laufs und erscheint in den erzeugten Aufgabenwarteschlangen. |
| **Startdatum/-uhrzeit** | Wenn gesetzt, startet die Verarbeitung ab diesem Zeitpunkt; der Wert muss in der Zukunft liegen. Liegt er beim Start in der Vergangenheit, bietet das Modul an, ihn auf eine Minute nach der aktuellen Zeit zu setzen. |
| **Status** | Zeigt den Fortschritt des Laufs (siehe Werteliste; nicht editierbar). Änderungen an Kopf und Zeilen sind nur im Status **Neu** möglich. |

Felder der **Mandantenerstellung** (Zeilen):

| Feld | Erläuterung |
|---|---|
| **Übertragungscode** | Wenn gesetzt, wird diese Zeile über die gewählte Zentralmandantübertragung initialisiert; auswählbar sind nur Übertragungen mit gesetzter Initialisierungsreihenfolge. Bei Auswahl wird der Herkunftsmandant automatisch aus dem Mastermandanten vorbelegt. |
| **Übertragungsbeschreibung** | Zeigt die Beschreibung der gewählten Übertragung (nicht editierbar). |
| **Herkunftsmandant** | Wenn gesetzt, ist dies der Mandant, aus dem die Bestandsdaten kopiert werden. Er muss dem in der Zuweisung hinterlegten Mastermandanten entsprechen; Sonderzeichen sind unzulässig. |
| **Zielmandant** | Wenn gesetzt, ist dies der Mandant, in den die Daten kopiert werden. Herkunfts- und Zielmandant müssen **unterschiedlich** sein. |
| **Status** | Zeigt den Zeilenstatus des Laufs (analog zum Kopf). |
| **Anzahl Aufgabenwarteschlangen** | Zeigt die Anzahl der für diese Zeile erzeugten Aufgabenwarteschlangen des Herkunftsmandanten; per Drilldown gelangen Sie zu den Aufgabenwarteschlangenposten (bei lokalen Mandanten). |

**Werte des Status (Mandantenerstellung):**

- **Neu:** Lauf angelegt, noch nicht gestartet. Nur in diesem Status sind Kopf und Zeilen änderbar.
- **Terminiert:** Aufgabenwarteschlangen wurden in den Herkunftsmandanten erstellt; die Verarbeitung ist eingeplant. Änderungen sind nicht mehr möglich.
- **In Bearbeitung:** Die Initialisierung läuft.
- **Abgeschlossen:** Der Lauf wurde vollständig und fehlerfrei beendet.
- **Abgeschlossen mit Fehler:** Der Lauf wurde beendet, es traten jedoch Fehler auf (siehe Fehlerprotokoll).

Aktionen der **Mandantenerstellung Karte**:

| Aktion | Erläuterung |
|---|---|
| **Asynchrone Verarbeitung** | Wenn ausgeführt, prüft das Modul die Zeilen, legt in jedem Herkunftsmandanten Aufgabenwarteschlangen an und setzt Kopf und Zeilen auf **Terminiert**. Ab dem Startzeitpunkt kopieren diese Aufgaben die Bestandsdaten in die Zielmandanten. Pro Erstellungsübertragung ist nur ein Herkunftsmandant zulässig. |
| **Setze Status auf Neu** | Wenn ausgeführt, werden die zugehörigen Aufgabenwarteschlangen entfernt und Kopf und Zeilen auf **Neu** zurückgesetzt, sodass der Lauf wieder bearbeitet werden kann. Nur in den Status **Terminiert**, **Abgeschlossen** oder **Abgeschlossen mit Fehler** möglich. |

**Ablauf (in Abhängigkeitsreihenfolge):**
1. **Zuerst** in den Übertragungen die **Initialisierungsreihenfolge** setzen (Kapitel *Zentralmandantübertragungen einrichten*).
2. **Danach** über **Mandanten-Initialisierung** eine **Mandantenerstellung** anlegen, **Beschreibung** und **Startdatum/-uhrzeit** erfassen.
3. Je Zeile **Übertragungscode**, **Herkunftsmandant** und **Zielmandant** festlegen.
4. **Schließlich** mit **Asynchrone Verarbeitung** starten; den Fortschritt über **Status** und **Anzahl Aufgabenwarteschlangen** überwachen.

## Asynchroner Betrieb und Protokolle

Nach der Einrichtung läuft die Synchronisation automatisch. Zur Überwachung und Fehlerbehandlung stehen zwei Protokolle bereit: das **Asynchrone Protokoll** für vorgemerkte, noch zu sendende Änderungen und das **Zentralmandantübertragungsfehlerprotokoll** für fehlgeschlagene Übertragungen.

### Asynchrones Protokoll

**Einstieg:** Öffnen Sie über die **Suche** das **Zentralmandant Daten übertragen Asynchrones Protokoll**.

Bei asynchronem Betrieb werden Datenänderungen zunächst hier vorgemerkt und dann gesammelt versendet.

| Feld | Erläuterung |
|---|---|
| **Von Mandant** | Zeigt den Mandanten, aus dem die Änderung stammt. |
| **Tabellen-Nr.** | Zeigt die Tabelle der geänderten Daten. |
| **Tabellenbezeichnung** | Name der Tabelle. |
| **Datensatz-Info.** | Kurzinformation zum betroffenen Datensatz. |
| **Aktion** | Zeigt die vorgemerkte Aktion (siehe Werteliste). |
| **Datensatz-ID** | Interne Kennung des betroffenen Datensatzes. |
| **Statustext** | Zeigt eine ergänzende Status-/Fehlermeldung zur Vormerkung. |
| **Ausstehende Übertragung** | Wenn aktiviert, ist der Eintrag zum Versand vorgemerkt und noch nicht gesendet. |

**Werte der Aktion:** **Einfügen** (neuer Datensatz), **Modifizieren** (Änderung), **Löschen** (Löschung), **Umbenennen** (Schlüsseländerung).

Aktionen des Asynchronen Protokolls:

| Aktion | Erläuterung |
|---|---|
| **Daten senden** | Wenn ausgeführt, werden die markierten Einträge zum Versand vorgemerkt und der asynchrone Versand angestoßen; erfolgreich gesendete Einträge werden anschließend entfernt. |
| **Als gesendet markieren** | Wenn ausgeführt, werden die markierten Einträge als versendet gekennzeichnet (Kennzeichen **Ausstehende Übertragung** entfällt), ohne dass ein erneuter Versand erfolgt. Nutzen Sie dies, um bereits anderweitig übernommene Änderungen aus der Warteschlange zu nehmen. |
| **Daten anzeigen** | Wenn ausgeführt, wird der zugehörige Dateninhalt (JSON) des Eintrags angezeigt – nützlich zur Analyse. |

### Zentralmandantübertragungsfehlerprotokoll

**Einstieg:** Öffnen Sie über die **Suche** das **Zentralmandantübertragungsfehlerprotokoll**.

Schlägt eine Übertragung fehl, wird dies hier vermerkt. Ist zusätzlich **Erfolgsmeldung protokollieren** in der Einrichtung aktiv, erscheinen auch erfolgreiche Übertragungen.

| Feld | Erläuterung |
|---|---|
| **Lfd. Nr.** | Automatisch erzeugte interne Zählnummer des Eintrags. |
| **Von Mandant** | Mandant, aus dem die Daten übertragen werden sollten. |
| **Nach Mandant** | Mandant, an den die Daten übertragen werden sollten. |
| **Übertragungsdienstcode** | Zeigt den verwendeten Übertragungsdienst des Eintrags. |
| **Tabellen-Nr.** | ID der Tabelle, bei der der Vorgang aufgetreten ist. |
| **Tabellenbezeichnung** | Name der betreffenden Tabelle. |
| **Datensatz-ID** | Kennung des betroffenen Datensatzes, sofern vorhanden. |
| **Aktion** | Zuletzt für diese Tabelle ausgeführte Aktion (siehe Werteliste). |
| **Status** | Ergebnis der Übertragung (siehe Werteliste). |
| **Statustext** | Ergänzender Fehler- oder Statustext zur Analyse. |

**Werte des Status:** **(leer)** (noch kein Ergebnis), **Erledigt** (erfolgreich übertragen), **Fehler** (Übertragung fehlgeschlagen), **Überarbeitet** (Eintrag wurde nach Korrektur erneut bearbeitet).

Aktionen des Fehlerprotokolls:

| Aktion | Erläuterung |
|---|---|
| **Daten anzeigen** | Wenn ausgeführt, wird der zur Übertragung anstehende Dateninhalt (JSON) angezeigt – hilfreich zur Fehleranalyse. |
| **Erneut versuchen** | Wenn ausgeführt, wird die Übertragung der aktiven Zeile erneut angestoßen. Voraussetzung: Der **Nach Mandant** ist der aktuell geöffnete Mandant. Es werden nur Zeilen bearbeitet, deren Zielmandant dem aktuellen Mandanten entspricht (Rückfrage zur Bestätigung). |
| **Daten Senden** | Wenn ausgeführt, werden die markierten Einträge (erneut) an den Zielmandanten gesendet; anschließend werden ungültige Fehlereinträge bereinigt. Es werden nur Zeilen bearbeitet, deren Herkunftsmandant der aktuelle Mandant ist (Rückfrage zur Bestätigung). |
| **Sende Daten. als Bearbeitet** | Wie **Daten Senden**, jedoch werden die Daten als Änderung (Modifizieren) statt als Neuanlage übertragen. Nutzen Sie dies, wenn der Datensatz im Zielmandanten bereits existiert. |

☞ Benachrichtigung: Ist in der **Benutzer Einrichtung** ein **Zentralmandant Verantwortlicher** mit E-Mail hinterlegt, erhält dieser bei jedem neuen Fehlereintrag automatisch eine Hinweis-E-Mail mit der laufenden Nummer.

## Typische Anwendungsfälle

Die folgenden Beispiele zeigen realistische Auslöser und den Ablauf in Business Central. Alle genannten Seiten und Aktionen sind im Modul vorhanden.

### 1. Debitoren-Namensänderung in allen Mandanten übernehmen

- **Auslöser:** Die Buchhaltung meldet, dass ein Debitor umfirmiert hat; der neue Name soll in allen Mandanten gelten.
- **Einstieg in BC:** Die einmalige Einrichtung ist erfolgt: In den **Zentralmandantübertragungen** existiert eine Übertragung mit **Synchronisierungsart = Bidirektional**, in der **Zentralmandantzuweisung** sind die beteiligten Mandanten hinterlegt und in den **Übertragungsfeldern** ist für den Debitor das Feld **Name** aufgenommen.
- **Kernablauf:** Der Anwender öffnet im führenden Mandanten den Debitor und ändert den Namen. Da die Tabelle und das Feld freigegeben sind und das Modul **Aktiv** ist, wird die Änderung automatisch an die übrigen Mandanten übertragen. Bei bidirektionaler Art ist es unerheblich, in welchem Mandanten die Änderung erfolgt.
- **Abschluss:** Ist **Erfolgsmeldung protokollieren** aktiv, erscheint im **Zentralmandantübertragungsfehlerprotokoll** ein Eintrag mit Status **Erledigt**. Andernfalls bleibt das Protokoll leer, solange kein Fehler auftritt.

### 2. Neuen Mandanten mit Stammdaten befüllen

- **Auslöser:** Es wurde eine neue Gesellschaft gegründet; der neue Mandant soll die bestehenden Debitoren und abhängigen Stammdaten des Hauptmandanten erhalten.
- **Einstieg in BC:** Der Administrator öffnet über die **Suche** die **Zentralmandantübertragungen** und wählt **Mandanten-Initialisierung**.
- **Kernablauf:** In der **Mandantenerstellung** legt er einen Lauf an, erfasst **Beschreibung** und **Startdatum/-uhrzeit**. Je Zeile wählt er den **Übertragungscode** (die Übertragung muss eine **Initialisierungsreihenfolge** besitzen); **Herkunftsmandant** wird aus dem Master vorbelegt, als **Zielmandant** wird die neue Gesellschaft gewählt. Mit **Asynchrone Verarbeitung** startet er den Lauf; Kopf und Zeilen wechseln auf **Terminiert**.
- **Abschluss:** Der Fortschritt ist am **Status** und an der **Anzahl Aufgabenwarteschlangen** ablesbar. Nach vollständiger Verarbeitung steht **Abgeschlossen** (bzw. **Abgeschlossen mit Fehler**, falls einzelne Datensätze scheiterten – dann Fehlerprotokoll prüfen).

### 3. Fehlgeschlagene Übertragung nachziehen

- **Auslöser:** Ein **Zentralmandant Verantwortlicher** erhält eine Hinweis-E-Mail über einen neuen Fehlereintrag.
- **Einstieg in BC:** Er öffnet über die **Suche** das **Zentralmandantübertragungsfehlerprotokoll** und markiert den Eintrag mit Status **Fehler**.
- **Kernablauf:** Über **Daten anzeigen** prüft er den Dateninhalt und die Ursache im **Statustext** (z. B. ein fehlender abhängiger Datensatz). Nach Behebung wechselt er in den betroffenen **Nach Mandant** und wählt **Erneut versuchen**; existiert der Datensatz im Ziel bereits, nutzt er **Sende Daten. als Bearbeitet**.
- **Abschluss:** Der Eintrag erhält den Status **Überarbeitet** bzw. **Erledigt**; ungültige Fehlereinträge werden dabei bereinigt.

### 4. Übertragung in eine andere Datenbank einrichten

- **Auslöser:** Der Konzern betreibt zwei getrennte Business-Central-Umgebungen; Stammdaten sollen von der einen in die andere synchronisiert werden.
- **Einstieg in BC:** Der Administrator öffnet über die **Suche** die **Übertragungsdienstliste** und legt einen neuen **Übertragungsdienst** an.
- **Kernablauf:** Er hinterlegt die **ODataV4 Adresse** der Zielumgebung und die **Autorisierung** (bei **OAuth**: **Client-ID**, **Geheimer Clientschlüssel**, **Autorisierungs-URL**, **Bereich**). Mit **Verbindung testen** prüft er die Erreichbarkeit. Anschließend trägt er den **Übertragungsdienstcode** im Kopf der Zentralmandantübertragung bzw. je Mandant in der **Zentralmandantzuweisung** ein.
- **Abschluss:** Nach erfolgreichem Verbindungstest laufen die Übertragungen über den Dienst in die Zieldatenbank; Fehler erscheinen mit dem jeweiligen **Übertragungsdienstcode** im Fehlerprotokoll.

## FAQ und Troubleshooting

### Warum werden meine Änderungen nicht in die anderen Mandanten übertragen?
In der **Zentralmandanteinrichtung** ist das Kennzeichen **Aktiv** nicht gesetzt, oder die Übertragung selbst ist nicht **Aktiv**. Ohne diese Kennzeichen sendet das Modul keine Daten. Prüfen Sie außerdem, ob das geänderte Feld tatsächlich in den **Übertragungsfeldern** enthalten ist.

### Warum kann ich keinen Mastermandanten setzen?
Das Kennzeichen **Master** ist nur bei der **Synchronisierungsart „Von Oben nach unten“** zulässig. Bei **Bidirektional** darf kein Master gesetzt sein; ist noch einer vorhanden, entfernen Sie ihn zuerst. Zudem kann es je Übertragung immer nur **einen** Mastermandanten geben.

### Warum meldet das System „Es existiert eine Masterzuordnung“ beim Wechsel auf Bidirektional?
Sie haben die Synchronisierungsart von „Von Oben nach unten“ auf **Bidirektional** geändert, es ist aber noch ein Mandant als **Master** markiert. Entfernen Sie das Master-Kennzeichen, danach ist der Wechsel möglich.

### Warum wird der Übertragungsbenutzer abgewiesen?
Der in **Zentralmandanteinrichtung** bzw. **Übertragungsdienst** hinterlegte **Übertragungsbenutzer** muss in **allen** Mandanten SUPER-Rechte besitzen. Fehlen diese, meldet das System, dass der Benutzer SUPER-Rechte in allen Mandanten haben muss.

### Warum lässt sich eine Tabelle nicht in den Übertragungsfeldern auswählen?
Es stehen nur die durch die Aktion **Initialisieren** freigegebenen Tabellen zur Verfügung. Führen Sie **Initialisieren** in der **Zentralmandanteinrichtung** aus. Zur Wahrung der Datenkonsistenz sind viele Tabellen bewusst ausgenommen.

### Warum kann ich eine Zeile in den Übertragungstabellen nicht löschen oder ändern?
Zu der Tabelle sind bereits **Übertragungsfelder** hinterlegt. Entfernen Sie zuerst die zugehörigen Felder; danach lässt sich die Tabellenzeile löschen bzw. ändern.

### Warum erhalte ich „Tabelle ist bereits konfiguriert“?
Dieselbe Tabelle desselben Mandanten ist bereits in einer **anderen** Zentralmandantübertragung mit **demselben Übertragungsdienst** konfiguriert. Diese Prüfung verhindert doppelte, widersprüchliche Übertragungen. Verwenden Sie die vorhandene Übertragung oder einen anderen Dienst.

### Warum kann ich die Mandantenerstellung nicht mehr bearbeiten?
Änderungen an Kopf und Zeilen der **Mandantenerstellung** sind nur im Status **Neu** möglich. Setzen Sie den Lauf mit **Setze Status auf Neu** zurück (aus den Status **Terminiert**, **Abgeschlossen** oder **Abgeschlossen mit Fehler**), um ihn erneut zu bearbeiten.

### Warum lässt sich „Erneut versuchen“ im Fehlerprotokoll nicht ausführen?
Die Aktion **Erneut versuchen** wirkt nur für Zeilen, deren **Nach Mandant** der aktuell geöffnete Mandant ist. Wechseln Sie in den Zielmandanten und wiederholen Sie die Aktion. Für den Versand aus dem Herkunftsmandant nutzen Sie **Daten Senden**.

### Warum verlangt die Benutzer Einrichtung eine E-Mail-Adresse?
Die Kennzeichen **Zentralmandant Verantwortlicher** und **Zentralmandant Empfänger obsolete Felder** lösen E-Mail-Benachrichtigungen aus. Ohne hinterlegte **E-Mail**-Adresse in der Benutzerzeile kann das jeweilige Kennzeichen nicht aktiviert werden. Tragen Sie zuerst die E-Mail-Adresse ein.
