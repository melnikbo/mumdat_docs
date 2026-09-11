---
title: Anwenderhandbuch m+m Semifinished Items
---

# Anwenderhandbuch m+m Semifinished Items

## Einleitung

**m+m Semifinished Items** erweitert die Fertigungssteuerung von Microsoft Dynamics 365 Business Central um
die automatische Erzeugung von **Halbfertigartikeln** und die dazugehörige **Umlagerung** der Komponenten
zwischen den Lagerorten der beteiligten **Arbeitsplatzgruppen**. Das Modul teilt einen mehrstufigen
Fertigungsauftrag automatisch in mehrere Fertigungsauftragszeilen auf – je eine Zeile pro
Halbfertigstufe –, sucht oder erzeugt den passenden Halbfertigartikel anhand von **Materialeigenschaften**
und legt für den Materialfluss zwischen den Arbeitsplatzgruppen automatisch **Umlagerungsaufträge** an.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender in der Fertigung** –
Fertigungssteuerer und Werker, die Fertigungsaufträge freigeben, Arbeitsgänge zurückmelden, die Ausgabe
buchen und die Aufteilung (**FA Split**) auslösen. Sekundär angesprochen sind **Administratoren und
Arbeitsvorbereiter**, die die Arbeitsplatzgruppen, Arbeitspläne, Materialarten und Materialeigenschaften
einrichten (Kapitel *Einrichtung* und *Stammdaten*).

**Kurzer Prozessüberblick.** Der typische Weg durch das Modul:

1. Der Administrator kennzeichnet eine **Arbeitsplatzgruppe** als **Halbfertigartikel** und hinterlegt dort
   **Materialeigenschaften**.
2. Im **Arbeitsplan** wird der betreffende **Arbeitsgang** ebenfalls als **Halbfertigartikel** gekennzeichnet;
   je Arbeitsgang werden **Materialeigenschaftsänderungen** (Zielwerte des Halbfertigartikels) gepflegt und
   im Arbeitsplankopf die **Aufteilungsoption** gesetzt.
3. Ein **Festgeplanter Fertigungsauftrag** entsteht aus dem Verkaufsauftrag oder manuell.
4. Bei Verkaufsfreigabe, bei FA-Freigabe oder manuell über **FA Split** teilt das System den Auftrag auf,
   erzeugt bzw. findet die Halbfertigartikel und legt die **Umlagerungsaufträge** an.
5. Beim Buchen der Ausgabe werden die Umlagerungen automatisch verarbeitet; über den Umlagerungseingang wird
   der Arbeitsgang bei Bedarf auf **Fertig** gesetzt. Bei Bedarf erzeugt der Anwender den
   **Halbfertigartikel-Nachfolgeauftrag**.

Alle Feld-, Seiten- und Aktionsbezeichnungen in diesem Handbuch entsprechen der deutschen Oberfläche von
Business Central. Die BC-Suche wird durchgängig als **Suchen** bezeichnet.

---

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg zum Ergebnis. **Zuerst** die Einrichtung (nur einmalig durch
den Administrator), **danach** die tägliche Arbeit. Verwenden Sie die verlinkten Kapitel für die
vollständigen Feldtabellen.

**Einrichtung (einmalig, Administrator) – in Abhängigkeitsreihenfolge:**

1. **Zuerst** die **Materialart** öffnen (Materialarten-Liste → Karte) und im Feld
   **Halbfertigartikelvorlage** die Artikelvorlage hinterlegen, aus der neue Halbfertigartikel erzeugt
   werden. Siehe *Einrichtung → Halbfertigartikel-Aufteilung einrichten*.
2. **Danach** die **Arbeitsplatzgruppe** öffnen (Arbeitsplatzgruppen-Liste → Karte) und das Feld
   **Halbfertigartikel** aktivieren. Über die Aktion **Materialeigenschaften** die Zuordnung
   *Komponentenmaterialart → Halbfertigmaterialart → Eigenschaft* pflegen.
3. Im **Arbeitsplan** die betreffenden **Arbeitsgangzeilen** als **Halbfertigartikel** kennzeichnen, je
   Arbeitsgang über die Aktion **Materialeigenschaftsänderungen** die Zielwerte erfassen und im
   Arbeitsplankopf die **Aufteilungsoption** wählen.
4. Für den Materialfluss die **Lagerorte** der Arbeitsplatzgruppen, **Umlagerungsrouten** (mit
   **Transitcode**) und die Nummernserie für Umlagerungsaufträge bereitstellen. Siehe *Einrichtung →
   Umlagerung der Halbfertigkomponenten einrichten*.

**Tägliche Arbeit (operativer Anwender):**

1. **Festgeplanter Fertigungsauftrag** anlegen bzw. aus dem **Verkaufsauftrag** erzeugen und aktualisieren.
   Hinweis: Ein **Freigegebener Fertigungsauftrag** mit noch nicht aufgeteilten Halbfertig-Arbeitsgängen ist
   nicht zulässig – legen Sie zunächst einen festgeplanten Auftrag an.
2. **FA Split** ausführen – automatisch bei Verkaufsfreigabe bzw. FA-Freigabe (je nach Aufteilungsoption)
   oder manuell über die Aktion **FA Split** auf dem Fertigungsauftrag. Das System erzeugt die
   Halbfertig-Zeilen und die **Umlagerungsaufträge**.
3. Fertigungsauftrag **freigeben** und die Arbeitsgänge normal bearbeiten.
4. **Ausgabe buchen** (Produktionsbuchblatt/Fertigmeldung): Die zugehörige **Umlagerung** wird automatisch
   gebucht und die **FA-Komponente** in den Ziel-Lagerort bewegt.
5. Nach dem Umlagerungseingang setzt das System – sofern **Halbfertigteil letzter AG Option = Beim Buchen des
   Umlagerungseingangs** – den Arbeitsgang auf **Fertig**.
6. Bei Bedarf auf dem **Freigegebenen Fertigungsauftrag** die Aktion
   **Halbfertigartikel-Nachfolgeauftrag erstellen** ausführen.

---

## Einrichtung

Die Einrichtung ist der umfangreichste Teil dieses Moduls. Sie erfolgt in
**Microsoft Dynamics 365 Business Central** durch den Administrator bzw. Arbeitsvorbereiter, bevor die
operative Fertigung startet. Das Modul benötigt zwei aufeinander aufbauende Konfigurationsstrecken:
die **Halbfertigartikel-Aufteilung** (welche Arbeitsgänge Halbfertigartikel erzeugen und wie diese gefunden
werden) und die **Umlagerung der Halbfertigkomponenten** (wie das Material zwischen den Lagerorten fließt).

### Halbfertigartikel-Aufteilung einrichten

**Wer und wann.** Diese Strecke richtet der Administrator einmalig je Produktionsszenario ein, bevor der
erste Fertigungsauftrag aufgeteilt wird. Sie legt fest, welche Arbeitsgänge einen Halbfertigartikel erzeugen,
aus welcher Vorlage neue Halbfertigartikel entstehen und mit welchen Zielwerten. Konsumiert wird die
Einrichtung im Tagesablauf durch die Funktion **FA Split** (siehe *Tägliche Arbeit am Fertigungsauftrag*).

**Numerische Reihenfolge der Einrichtungsschritte (Abhängigkeitsreihenfolge aus dem Code):**

1. **Zuerst** je **Materialart** die Vorlage hinterlegen (Stammdaten → *Materialart als Halbfertigstufe*).
2. **Danach** die **Arbeitsplatzgruppe** als Halbfertigstation kennzeichnen und ihre
   **Materialeigenschaften** pflegen (Stammdaten → *Arbeitsplatzgruppe als Halbfertigstation*).
3. **Anschließend** je **Arbeitsgang** die Kennzeichnung und die **Materialeigenschaftsänderungen** setzen
   (Stammdaten → *Arbeitsgänge und Materialeigenschaftsänderungen*).
4. **Danach** im Arbeitsplankopf die **Aufteilungsoption** setzen (siehe *Arbeitsplan: Aufteilung steuern*).
5. **Optional** die **Optimierte Halbfertigteilsuche** aktivieren (siehe unten).
6. **Schließlich** löst der Anwender im Tagesablauf **FA Split** aus.

#### Arbeitsplan: Aufteilung steuern

**Einstieg:** Arbeitspläne (Liste) → **Arbeitsplan** (Karte) → Reiter **Allgemein**.

Der Arbeitsplankopf steuert, **wann** ein Fertigungsauftrag automatisch aufgeteilt wird, und dokumentiert, ob
ein Arbeitsplan aus einer Aufteilung entstanden ist.

| Feld | Erläuterung |
|---|---|
| **Aufteilungsoption** | Legt fest, wann die automatische Aufteilung des Fertigungsauftrags ausgelöst wird. Die Werte werden unten je Ausprägung erläutert. Nur setzbar, solange der Arbeitsplan **kein** aufgeteilter Arbeitsplan ist und **nicht** den Status *Zertifiziert* hat; ist keine als Halbfertigartikel gekennzeichnete Arbeitsgangzeile vorhanden, wird das Setzen mit der Meldung „Es kann keine Halbfertigteilarbeitsgangzeile gefunden werden." abgewiesen. |
| **Aufgeteilter Arbeitsgang** | Wenn aktiviert, handelt es sich bei diesem Arbeitsplan um ein durch die Aufteilung **automatisch erzeugtes** Duplikat; er wird vom System gesetzt und ist nicht manuell editierbar. So erkennen Sie generierte Arbeitspläne gegenüber den ursprünglich gepflegten. |
| **Urspr. Arbeitsplannr.** | Verweist bei einem aufgeteilten Arbeitsplan auf die **Nummer des Ausgangsarbeitsplans**, aus dem er kopiert wurde. Damit ist die Herkunft eines generierten Arbeitsplans nachvollziehbar; bei manuell gepflegten Arbeitsplänen bleibt das Feld leer. |

**Werte der Aufteilungsoption (vollständig):**

- **(leer):** Es findet **keine** automatische Aufteilung statt. Der Anwender kann die Aufteilung nur manuell
  über **FA Split** anstoßen.
- **Bei Verkaufsfreigabe:** Wenn gesetzt, teilt das System den aus einem Verkaufsauftrag erzeugten
  Fertigungsauftrag automatisch auf, **sobald der Verkaufsauftrag freigegeben** wird und Komponenten sowie
  Materialeigenschaftsänderungen vorliegen. Ideal, wenn die Halbfertigstruktur bereits mit der
  Verkaufsfreigabe feststehen soll.
- **Bei FA-Freigabe:** Wenn gesetzt, erfolgt die Aufteilung automatisch **beim Freigeben des
  Fertigungsauftrags** (Statuswechsel auf *Freigegeben*). Geeignet, wenn die Aufteilung erst zum Zeitpunkt
  der Fertigungsfreigabe erzeugt werden soll.

**Validierung/Abhängigkeit.** Ein aufgeteilter Arbeitsplan (**Aufgeteilter Arbeitsgang** = aktiv) kann keine
Aufteilungsoption erhalten (das System prüft, dass **Urspr. Arbeitsplannr.** leer ist). Solange keine
Halbfertig-Arbeitsgangzeile existiert, ist die Option nicht setzbar. Cross-Link: die Halbfertig-Kennzeichnung
der Arbeitsgänge pflegen Sie unter *Stammdaten → Arbeitsgänge und Materialeigenschaftsänderungen*.

#### Optimierte Halbfertigteilsuche

**Einstieg:** Materialeigenschaften-Einrichtung (Karte des Basismoduls *m+m Material Properties*) → Gruppe
**Halbfertigteil**.

Diese Einrichtung steuert das Verfahren, mit dem das Modul einen bereits vorhandenen Halbfertigartikel zu
den geforderten Eigenschaften findet.

| Einrichtung | Erläuterung |
|---|---|
| **Optimierte Halbfertigteilsuche verwenden** | Wenn aktiviert, verwendet die Aufteilung die interne, mengenoptimierte Eigenschaftssuche (Abfrage über die Eigenschaftswerte, sortiert nach Trefferzahl je Eigenschaft), um einen passenden Halbfertigartikel zu ermitteln; das reduziert bei großen Artikelbeständen die Suchzeit. Wenn deaktiviert, wird die Standard-Eigenschaftssuche des Basismoduls verwendet. In beiden Fällen gilt: Wird **genau ein** Artikel gefunden, wird er verwendet; werden **mehrere** gefunden, wählt der Anwender manuell aus; wird **keiner** gefunden, erzeugt das System einen neuen Halbfertigartikel aus der **Halbfertigartikelvorlage**. |

**Prozessbezug.** Die Suche wird während **FA Split** ausgeführt. Die Trefferermittlung stützt sich auf die
in den **Materialeigenschaftsänderungen** hinterlegten Zielwerte und die Materialeigenschaften der
Komponente. Cross-Link: *Tägliche Arbeit am Fertigungsauftrag*.

### Umlagerung der Halbfertigkomponenten einrichten

**Wer und wann.** Der Administrator richtet die Logistik einmalig ein, bevor der erste aufgeteilte
Fertigungsauftrag gebucht wird. Sie legt fest, **zwischen welchen Lagerorten** das Halbfertigmaterial bewegt
wird und wie die dazu automatisch erzeugten **Umlagerungsaufträge** gebucht werden. Konsumiert wird die
Einrichtung im Tagesablauf beim Buchen der Ausgabe und des Umlagerungseingangs.

**Numerische Reihenfolge der Einrichtungsschritte:**

1. **Zuerst** je Arbeitsplatzgruppe einen **Lagerort** (Feld **Lagerort** auf der Arbeitsplatzgruppe) sowie
   den Produktionslagerplatz (To-Production-Lagerplatz) hinterlegen. Wenn Ausgangs- und Ziel-Lagerort
   unterschiedlich sind, erzeugt das System eine Umlagerung; sind sie identisch, entfällt die Umlagerung und
   die **Halbfertigteil letzter AG Option** wird automatisch auf **(leer)** zurückgesetzt.
2. **Danach** für jede benötigte Lagerort-Kombination eine **Umlagerungsroute** mit **Transitcode**
   einrichten. Fehlt der Transitcode der Route, kann kein Umlagerungsauftrag angelegt werden.
3. **Anschließend** die Nummernserie für Umlagerungsaufträge in der Lagereinrichtung hinterlegen. Ohne diese
   Nummernserie bricht die automatische Erzeugung des Umlagerungsauftrags ab.
4. **Je Halbfertig-Arbeitsgang** die **Halbfertigteil letzter AG Option** setzen (siehe Tabelle unten), damit
   der Arbeitsgang beim Umlagerungseingang korrekt abgeschlossen wird.
5. **Schließlich** wird die Umlagerung im Tagesablauf automatisch beim Buchen der Ausgabe verarbeitet.

**Halbfertigteil letzter AG Option** (auf Arbeitsgang- bzw. FA-Arbeitsgangzeile):

| Feld | Erläuterung |
|---|---|
| **Halbfertigteil letzter AG Option** | Legt fest, wie der letzte Halbfertig-Arbeitsgang abgeschlossen wird, wenn das erzeugte Halbfertigmaterial per Umlagerung an den nächsten Lagerort geliefert wird. Nur editierbar, wenn die Zeile als **Halbfertigartikel** gekennzeichnet ist. Wird verlangt, dass sich der **Lagerort** des Arbeitsgangs vom Lagerort der Arbeitsplatzgruppe unterscheidet – andernfalls erscheint „Der Lagerort des Arbeitsgangs und der Arbeitsplatzgruppe muss unterschiedlich sein." |

**Werte (vollständig):**

- **(leer):** Der Arbeitsgang wird **nicht** durch den Umlagerungseingang abgeschlossen; der Status ergibt
  sich aus der normalen Rückmeldung. Wird automatisch gesetzt, wenn Arbeitsgang- und
  Arbeitsplatzgruppen-Lagerort identisch sind (keine Umlagerung nötig).
- **Beim Buchen des Umlagerungseingangs:** Wenn gesetzt, wird der Arbeitsgang automatisch auf **Fertig**
  gesetzt, sobald der **Umlagerungseingang** gebucht ist und die eingegangene Menge die Restmenge der
  **FA-Komponente** deckt. So schließt der physische Wareneingang am Ziel-Lagerort zugleich den Arbeitsgang
  ab.

**Validierung/Abhängigkeit.** Die Umlagerung wird nur für Komponenten erzeugt, deren Lagerort vom
Arbeitsplatzgruppen-Lagerort abweicht. Bei fremdvergebenen (Lohn-)Arbeitsgängen mit hinterlegter
Kreditorennummer steuert das Modul das Buchen der Umlagerung abweichend (kein automatisches Buchen, solange
der Folgearbeitsgang ebenfalls fremdvergeben ist). Cross-Link: *Umlagerung, Bestand und Folgeaufträge*.

### Berechtigungen

Für den Zugriff auf die Objekte dieses Moduls stellt die Erweiterung den Berechtigungssatz **MuM SF All**
(Bezeichnung „All permissions") bereit. Dieser Berechtigungssatz bestimmt die Lese-, Schreib-, Änderungs-
und Löschrechte für die Tabellen, Seiten und Codeunits des Halbfertigartikel-Moduls und legt fest, welche
Aktionen die Anwender im Modul ausführen dürfen. Er ist einer Rolle bzw. einem Benutzer zuzuweisen, bevor mit
der Halbfertigartikel-Aufteilung gearbeitet wird.

---

## Stammdaten

Die Stammdaten dieses Moduls bestehen aus Kennzeichnungen und Zuordnungen auf vorhandenen Fertigungs- und
Artikelstammdaten sowie aus zwei eigenen Pflegeseiten (**Materialeigenschaften** und
**Materialeigenschaftsänderungen**). Sie steuern, welche Objekte als Halbfertigstufe behandelt werden und mit
welchen Zielwerten Halbfertigartikel entstehen.

### Arbeitsplatzgruppe als Halbfertigstation

**Einstieg:** Arbeitsplatzgruppen (Liste) → **Arbeitsplatzgruppe** (Karte).

**Prozessbezug.** Der Administrator markiert diejenigen Arbeitsplatzgruppen, an denen Halbfertigartikel
entstehen. Diese Kennzeichnung ist die Grundlage dafür, dass die zugehörigen Arbeitsgänge im Arbeitsplan als
Halbfertigartikel behandelt und beim **FA Split** aufgeteilt werden. Die Kennzeichnung wird von der
Arbeitsplatzgruppe automatisch auf Arbeitsgang- und FA-Arbeitsgangzeilen übernommen.

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikel** | Wenn aktiviert, wird diese Arbeitsplatzgruppe als Halbfertigstation behandelt: Neue Arbeitsgangzeilen mit dieser Arbeitsplatzgruppe erhalten automatisch die Halbfertig-Kennzeichnung, und der zugehörige Fertigungsauftrag wird beim **FA Split** um eine eigene Halbfertigstufe erweitert. Ohne dieses Kennzeichen bleibt die Arbeitsplatzgruppe eine normale Kapazitätsstelle ohne automatische Halbfertigerzeugung. |

**Aktion auf der Karte:**

- **Materialeigenschaften** – öffnet die Pflegeliste der Materialeigenschaften für diese Arbeitsplatzgruppe
  (nur aktiv, wenn **Halbfertigartikel** gesetzt ist). Siehe *Materialeigenschaften pflegen*.

**Löschverhalten.** Wird eine Arbeitsplatzgruppe gelöscht, entfernt das System automatisch die zugehörigen
**Materialeigenschaften**.

#### Materialeigenschaften pflegen

**Einstieg:** Arbeitsplatzgruppenkarte → Aktion **Materialeigenschaften** (öffnet die Seite
**Materialeigenschaften**; die Seite ist nicht über **Suchen** erreichbar und wird ausschließlich über diese
Aktion aufgerufen).

**Prozessbezug.** Hier definiert der Administrator je Arbeitsplatzgruppe die Übersetzung von der
**Komponentenmaterialart** in die **Halbfertigmaterialart** und die dabei relevante **Eigenschaft**. Diese
Zuordnung steuert, welche Eigenschaften beim **FA Split** vom Vormaterial auf den Halbfertigartikel übertragen
werden.

| Feld | Erläuterung |
|---|---|
| **Komponentenmaterialart** | Legt die Materialart der eingehenden Komponente fest, für die diese Regel gilt. Beim **FA Split** wird anhand dieser Materialart bestimmt, welche Komponenteneigenschaften herangezogen werden. |
| **Halbfertigmaterialart** | Legt die Materialart des zu erzeugenden Halbfertigartikels fest. Beim Suchen bzw. Erzeugen des Halbfertigartikels wird diese Materialart verwendet; die Eigenschaftswerte werden gegen deren zulässige Grenzen geprüft. |
| **Eigenschaft** | Bestimmt die konkrete Eigenschaft (Eigenschaftscode), die von der Komponente auf den Halbfertigartikel abgebildet wird. Die Auswahl ist auf die Eigenschaften der gewählten **Halbfertigmaterialart** eingeschränkt. |

**Validierung.** Ändert der Administrator **Komponentenmaterialart**, **Halbfertigmaterialart** oder
**Eigenschaft** einer bereits verwendeten Zeile, löscht das System die abhängigen
**Materialeigenschaftsänderungen** automatisch, damit keine widersprüchlichen Zielwerte bestehen bleiben.

### Materialart als Halbfertigstufe

**Einstieg:** Materialarten (Liste) → **Materialart** (Karte) → Reiter **Allgemein**.

**Prozessbezug.** Je Materialart hinterlegt der Administrator die Artikelvorlage, aus der neue
Halbfertigartikel erzeugt werden, falls beim **FA Split** kein passender Artikel gefunden wird.

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikelvorlage** | Legt die Artikelvorlage (Konfigurationsvorlage für Artikel) fest, aus der ein neuer Halbfertigartikel erzeugt wird, wenn die Eigenschaftssuche keinen bestehenden Artikel liefert. Wenn hinterlegt, wird der neue Artikel mit der Nummernserie und den Vorgabewerten der Vorlage angelegt, als **Halbfertigartikel** gekennzeichnet und mit den ermittelten Eigenschaftswerten gefüllt. Ohne Vorlage kann kein neuer Halbfertigartikel automatisch entstehen. Zulässig sind nur aktivierte Artikelvorlagen. |

### Arbeitsgänge und Materialeigenschaftsänderungen

**Einstieg:** **Arbeitsplan** (Karte) → Unterseite **Arbeitsgangzeilen**.

**Prozessbezug.** Auf Arbeitsgangebene entscheidet der Administrator, welcher Arbeitsgang einen
Halbfertigartikel erzeugt, wie dieser beim Umlagerungseingang abgeschlossen wird und welche Zielwerte der
Halbfertigartikel erhalten soll.

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikel** | Wenn aktiviert, erzeugt dieser Arbeitsgang beim **FA Split** eine eigene Halbfertigstufe. Beim Aktivieren legt das System automatisch die zugehörigen **Materialeigenschaftsänderungen** (leere Zielwerte je Eigenschaft der Arbeitsplatzgruppe) an; beim Deaktivieren werden diese wieder entfernt. Der Wert wird beim Übernehmen der Arbeitsplatzgruppe automatisch aus deren Kennzeichnung gesetzt. |
| **Halbfertigteil letzter AG Option** | Steuert den Abschluss des Arbeitsgangs über den Umlagerungseingang (Werte siehe *Einrichtung → Umlagerung der Halbfertigkomponenten einrichten*). Nur editierbar, wenn **Halbfertigartikel** gesetzt ist. |

**Aktion auf der Arbeitsgangzeile:**

- **Materialeigenschaftsänderungen** – öffnet die Zielwertpflege für diesen Arbeitsgang (nur aktiv bei
  gesetztem **Halbfertigartikel**; die Seite ist nicht über **Suchen** erreichbar und wird ausschließlich
  über diese Aktion geöffnet).

**Löschverhalten.** Wird eine Arbeitsgangzeile gelöscht oder die Halbfertig-Kennzeichnung entfernt, löscht das
System die zugehörigen **Materialeigenschaftsänderungen**.

#### Materialeigenschaftsänderungen erfassen

**Einstieg:** Arbeitsgangzeile → Aktion **Materialeigenschaftsänderungen** (Seite
**Materialeigenschaftsänderungen**).

**Prozessbezug.** Hier legt der Administrator die konkreten **Zielwerte** je Eigenschaft fest, mit denen der
Halbfertigartikel gesucht oder erzeugt wird. Die Zeilen entstehen automatisch aus den Materialeigenschaften
der Arbeitsplatzgruppe; der Administrator ergänzt die Werte.

| Feld | Erläuterung |
|---|---|
| **Komponentenmaterialart** | Zeigt die Materialart der Komponente (nicht editierbar); dient der Zuordnung der Eigenschaft. |
| **Halbfertigmaterialart** | Zeigt die Materialart des Halbfertigartikels (nicht editierbar); bestimmt die zulässigen Eigenschaften und Wertegrenzen. |
| **Eigenschaft** | Zeigt die Eigenschaft (nicht editierbar), deren Zielwert erfasst wird. |
| **Wert** | Legt den Zielwert der Eigenschaft für den Halbfertigartikel fest. Bei Zahlen-Eigenschaften wird der Wert gegen **Wert erlaubt von/bis** geprüft und typgerecht formatiert; bei Eigenschaften mit Wertelisten (**Eigenschaftswerte verwenden**) muss der Wert in der Werteliste enthalten sein, sonst erscheint „Wert … ist nicht erlaubt/wurde nicht in den Eigenschaftswerten gefunden!". |
| **Eigenschaftswertname** | Zeigt den Klartextnamen zum eingegebenen Wert (aus der Werteliste; nicht editierbar). |
| **Einheit** | Zeigt die Maßeinheit der Eigenschaft (nicht editierbar). |
| **Wert erlaubt von** | Legt die Untergrenze für numerische Zielwerte fest. Wenn gesetzt, weist das System Werte unterhalb dieser Grenze ab. |
| **Wert erlaubt bis** | Legt die Obergrenze für numerische Zielwerte fest. Wenn gesetzt, weist das System Werte oberhalb dieser Grenze ab. |

**Werte nach Datentyp (Eigenschaft).** Der zugrunde liegende **Datentyp** der Eigenschaft bestimmt die
Prüfung des Feldes **Wert**:

- **Text:** Freitext; keine numerische Grenzprüfung. Bei aktivierten Eigenschaftswerten muss der Text in der
  Werteliste stehen.
- **Dezimal:** Der Wert muss eine gültige Dezimalzahl sein und innerhalb **Wert erlaubt von/bis** liegen;
  andernfalls Fehler „darf nicht weniger als …/größer sein als …".
- **Ganzzahl:** Wie Dezimal, jedoch wird auf eine ganze Zahl gerundet.
- **Datum:** Der Wert muss ein gültiges Datum sein („kann nicht zu … gewandelt werden.").

### Artikel als Halbfertigartikel

**Einstieg:** Artikel (Liste) → **Artikelkarte** → Infobereich **Artikel**.

**Prozessbezug.** Halbfertigartikel werden in der Regel automatisch beim **FA Split** erzeugt und dabei
gekennzeichnet. Auf der Artikelkarte ist die Kennzeichnung sichtbar und – bei manueller Stammdatenpflege –
setzbar.

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikel** | Wenn aktiviert, ist dieser Artikel als automatisch erzeugter bzw. gepflegter Halbfertigartikel gekennzeichnet. Die Kennzeichnung fließt in die Chargeninformation ein und wird bei der Eigenschaftssuche berücksichtigt. Beim automatischen Anlegen setzt das System das Kennzeichen und hebt die zwischenzeitliche Sperre (**Gesperrt**) des neuen Artikels nach Abschluss der Erzeugung wieder auf. |

### Charge als Halbfertigartikel

**Einstieg:** **Chargennr.-Informationskarte** → Reiter **Allgemein**.

**Prozessbezug.** Für die Nachverfolgung kennzeichnet das Modul auch Chargen als Halbfertigartikel.

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikel** | Wenn aktiviert, gehört diese Charge zu einem Halbfertigartikel. Das System setzt das Kennzeichen automatisch beim Entstehen des Artikelpostens: bei einer **Ausgabe** aus einem Halbfertig-Fertigungsauftrag anhand der FA-Zeile, sonst anhand des Artikelstamms. So lassen sich Halbfertigchargen in der Chargeninformation und in Auswertungen erkennen. |

---

## Tägliche Arbeit am Fertigungsauftrag

Die operative Arbeit findet am **Fertigungsauftrag** statt. Die relevanten Aktionen und Zusatzfelder dieses
Moduls sind gesteuert durch die zuvor beschriebene Einrichtung: Die **Halbfertig-Kennzeichnung** der
Arbeitsplatzgruppen und Arbeitsgänge, die **Materialeigenschaftsänderungen** je Arbeitsgang, die
**Aufteilungsoption** im Arbeitsplan sowie die **Umlagerungslogistik** (Lagerorte, Routen, Transitcode)
bestimmen, wann und wie das System aufteilt, sucht/erzeugt und umlagert. Cross-Link: *Einrichtung* und
*Stammdaten*.

### Fertigungsauftrag anlegen und aufteilen (FA Split)

**Einstieg:** **Festgeplanter Fertigungsauftrag** bzw. **Freigegebener Fertigungsauftrag** → Aktionsbereich
**Funktionen** → **FA Split**.

**Wichtige Regel.** Ein **Freigegebener Fertigungsauftrag** mit noch nicht aufgeteilten
Halbfertig-Arbeitsgängen ist nicht zulässig. Versucht das System, einen solchen Auftrag zu berechnen,
erscheint: „Sie sind nicht berechtigt einen freigegebenen Fertigungsauftrag mit Arbeitsgängen zu erstellen,
welche Arbeitsplatzgruppen ein Halbfertigartikel erzeugen. Bitte erstellen Sie einen festgeplanten
Fertigungsauftrag." Legen Sie daher zunächst einen **Festgeplanten Fertigungsauftrag** an.

**Ablauf der Aufteilung (was zuerst / was danach):**

1. **Zuerst** den Festgeplanten Fertigungsauftrag mit Artikel, Menge, Arbeitsplan und Komponenten anlegen
   bzw. aus dem Verkaufsauftrag erzeugen und aktualisieren.
2. **Danach** die Aufteilung auslösen:
   - **Automatisch** bei **Aufteilungsoption = Bei Verkaufsfreigabe**, sobald der Verkaufsauftrag
     freigegeben ist,
   - **automatisch** bei **Aufteilungsoption = Bei FA-Freigabe**, sobald der Fertigungsauftrag freigegeben
     wird,
   - **manuell** über die Aktion **FA Split**. Sind keine aufteilbaren Zeilen vorhanden, meldet das System
     „Es wurden keine Zeilen zum Splitten gefunden.".
3. **Ergebnis:** Das System legt je Halbfertigstufe eine eigene **Fertigungsauftragszeile** an, kopiert bzw.
   findet den passenden **Arbeitsplan**, sucht oder erzeugt den **Halbfertigartikel** (Eigenschaftssuche bzw.
   **Halbfertigartikelvorlage**), erstellt die **FA-Komponenten** der Folgestufen, legt die
   **Umlagerungsaufträge** an und setzt am Fertigungsauftrag das Kennzeichen **Aufgeteilte Zeilen**.

**Manuelle Artikelauswahl.** Liefert die Eigenschaftssuche **mehrere** Treffer, öffnet das System die
Artikelliste zur manuellen Auswahl des Halbfertigartikels; bei **einem** Treffer wird dieser automatisch
verwendet, bei **keinem** Treffer wird aus der Vorlage ein neuer Artikel erzeugt.

### Arbeitsgänge und Zusatzfelder im FA-Arbeitsplan

**Einstieg:** Fertigungsauftrag → Zeile → **Arbeitsgänge** (FA-Arbeitsplan).

Im FA-Arbeitsplan sind die Halbfertig-Zusatzfelder sichtbar und die Zielwertpflege erreichbar.

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikel** | Zeigt an (nicht editierbar), dass dieser Arbeitsgang einen Halbfertigartikel erzeugt. Ergibt sich aus der Arbeitsplatzgruppe bzw. dem Arbeitsplan. |
| **Halbfertigteil letzter AG Option** | Steuert den Abschluss des Arbeitsgangs über den Umlagerungseingang (Werte wie in der Einrichtung). Nur editierbar bei gesetztem **Halbfertigartikel**. |

**Aktion:** **Materialeigenschaftsänderungen** – öffnet die (auftragsbezogenen) Zielwerte des Arbeitsgangs
(Seite **Materialeigenschaftsänderungen**). Diese enthalten dieselben Felder wie in den Stammdaten
(Komponentenmaterialart, Halbfertigmaterialart, Eigenschaft, Wert, Eigenschaftswertname, Einheit, Wert
erlaubt von, Wert erlaubt bis) und werden beim **FA Split** aus den Stammdaten übernommen.

### Halbfertigartikel-Nachfolgeauftrag erstellen

**Einstieg:** **Freigegebener Fertigungsauftrag** → Aktionsbereich **Funktionen** →
**Halbfertigartikel-Nachfolgeauftrag erstellen**.

**Prozessbezug.** Wenn ein Halbfertig-Arbeitsgang abgeschlossen ist (letzter Arbeitsgang der Halbfertigzeile
mit Status **Fertig**) und noch Restmenge offen ist, öffnet diese Aktion die **FA-Zeilenübersicht** der
betroffenen Halbfertigzeilen, aus der der Folgeauftrag für die weitere Fertigung angestoßen bzw. ausgewählt
wird. So setzen Sie die Produktion der nächsten Stufe fort, ohne den Zusammenhang zum Ausgangsauftrag zu
verlieren.

---

## Umlagerung, Bestand und Folgeaufträge

Der Materialfluss zwischen den Arbeitsplatzgruppen erfolgt über automatisch erzeugte **Umlagerungsaufträge**.
Dieses Kapitel beschreibt, was beim Buchen geschieht und welche Zusatzfelder die Umlagerungszeilen mit dem
Fertigungsauftrag verknüpfen.

### Automatische Umlagerung beim Buchen der Ausgabe

**Ablauf (was zuerst / was danach):**

1. **Zuerst** bucht der Anwender die **Ausgabe** eines Halbfertig-Arbeitsgangs (Produktionsbuchblatt bzw.
   Fertigmeldung).
2. **Danach** ermittelt das Modul automatisch die zugehörigen **Umlagerungszeilen** (Verknüpfung über die
   Zusatzfelder, siehe unten), reserviert die Charge und bucht – je nach Lagerorteinstellung – entweder über
   **Lager-Warenausgang/-eingang** oder direkt den **Umlagerungsversand** und **Umlagerungseingang**.
3. **Anschließend** wird die **FA-Komponente** der Folgestufe in den Ziel-Lagerort (und Lagerplatz) bewegt;
   bei chargengeführten Artikeln wird die Charge über die Reservierung durchgereicht.
4. **Schließlich** setzt das System – bei **Halbfertigteil letzter AG Option = Beim Buchen des
   Umlagerungseingangs** und ausreichender Eingangsmenge – den Arbeitsgang auf **Fertig**.

**Teilmengen.** Teilausgaben und Teillieferungen sind zulässig; das Modul verarbeitet die jeweils gebuchte
Menge und schließt den Arbeitsgang erst, wenn die eingegangene Menge die Restmenge der Komponente deckt. Eine
künstliche Sperre „erst bei vollständigem Mengenausgleich abschließen" besteht nicht.

### Verknüpfungsfelder auf der Umlagerungszeile

Die folgenden Felder verbinden eine **Umlagerungszeile** mit dem auslösenden Fertigungsauftrag und werden vom
System gesetzt (nicht editierbar):

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikel FA-Nr.** | Zeigt den Fertigungsauftrag, aus dem diese Umlagerung entstanden ist. Damit ist die Umlagerung eindeutig dem Halbfertig-Prozess zugeordnet. |
| **Halbfertigartikel FA-Zeilennr.** | Zeigt die Fertigungsauftragszeile (Halbfertigstufe), zu der die Umlagerung gehört. |
| **Halbfertigartikel FA-Komponenten Zeilennr.** | Zeigt die FA-Komponente, die durch diese Umlagerung an den Ziel-Lagerort geliefert wird. |

### Interne Herkunfts- und Steuerfelder (Nachvollziehbarkeit)

Für die interne Verkettung der Halbfertigstufen führt das Modul auf den Fertigungsauftrags- und
Arbeitsgangzeilen zusätzliche, systemgesetzte Felder. Sie sind für die Nachvollziehbarkeit relevant und
werden nicht manuell gepflegt:

| Feld | Erläuterung |
|---|---|
| **Halbfertigartikelherkunftszeilennr.** (FA-Zeile) | Verweist auf die ursprüngliche Fertigungsauftragszeile, aus der die Halbfertigstufe abgeleitet wurde. |
| **Aufgeteilte Zeilen** (Fertigungsauftrag) | Wenn aktiviert, wurde dieser Fertigungsauftrag bereits aufgeteilt; ein erneutes automatisches Aufteilen unterbleibt. |
| **Halbfertigartikel Nächste AG Nr.** / **Halbfertigartikel vorherige AG Nr.** (FA-Arbeitsgang) | Verketten die Halbfertig-Arbeitsgänge in ihrer Reihenfolge und steuern, wann der letzte Arbeitsgang der Stufe erreicht ist. |
| **Halbfertigartikel Nächste FA-Zeilennr.** (FA-Arbeitsgang) | Verweist auf die Folge-Fertigungsauftragszeile, an die das Material umgelagert wird. |

---

## Historie, Nachverfolgung und Kennzeichnungen

Das Modul führt keine eigenen Historien- oder Protokollseiten. Die Nachverfolgung stützt sich auf
Kennzeichnungen an vorhandenen Stammdaten und Belegen:

- **Chargennr.-Informationskarte – Halbfertigartikel:** kennzeichnet Chargen, die aus Halbfertigartikeln
  stammen (automatisch beim Buchen des Artikelpostens gesetzt). So erkennen Sie Halbfertigchargen in der
  Chargenauswertung.
- **Arbeitsplankarte – Aufgeteilter Arbeitsgang / Urspr. Arbeitsplannr.:** kennzeichnet automatisch erzeugte
  (aufgeteilte) Arbeitspläne und deren Herkunft.
- **Fertigungsauftrag – Aufgeteilte Zeilen:** zeigt, dass ein Fertigungsauftrag bereits aufgeteilt wurde.
- **Umlagerungszeile – Halbfertigartikel FA-Nr./-Zeilennr./-Komponenten Zeilennr.:** verbinden jede
  Umlagerung mit ihrem Ursprung im Fertigungsauftrag.

Über diese Felder lässt sich der gesamte Weg vom Ausgangsauftrag über die erzeugten Halbfertigartikel und die
Umlagerungen bis zur Folgestufe nachvollziehen.

---

## FAQ und Troubleshooting

### Warum darf ich keinen freigegebenen Fertigungsauftrag mit Halbfertig-Arbeitsgängen erstellen?

Weil die Aufteilung an einem festgeplanten Auftrag erfolgen muss. Enthält ein zu berechnender freigegebener
Auftrag Arbeitsgänge mit Halbfertig-Arbeitsplatzgruppen, bricht das System mit einer entsprechenden Meldung
ab und fordert einen **Festgeplanten Fertigungsauftrag**. Legen Sie den Auftrag festgeplant an, teilen Sie ihn
auf und geben Sie ihn erst danach frei.

### Warum meldet FA Split „Es wurden keine Zeilen zum Splitten gefunden."?

Weil im Auftrag keine als **Halbfertigartikel** gekennzeichneten Arbeitsgänge (mit gültiger
Arbeitsplatzgruppe) vorhanden sind. Prüfen Sie, ob die Arbeitsplatzgruppe als **Halbfertigartikel**
gekennzeichnet ist und die betreffenden **Arbeitsgangzeilen** die Kennzeichnung übernommen haben.

### Wann teilt das System automatisch auf, und wann muss ich FA Split manuell auslösen?

Das hängt von der **Aufteilungsoption** im Arbeitsplankopf ab: **Bei Verkaufsfreigabe** teilt bei Freigabe des
Verkaufsauftrags auf, **Bei FA-Freigabe** bei Freigabe des Fertigungsauftrags. Ist die Option **(leer)**,
erfolgt keine automatische Aufteilung – dann lösen Sie **FA Split** manuell aus.

### Woher weiß das System, welchen Halbfertigartikel es verwenden soll?

Es sucht anhand der in den **Materialeigenschaftsänderungen** hinterlegten Zielwerte und der
Komponenteneigenschaften einen passenden Artikel. Bei **einem** Treffer wird dieser verwendet, bei
**mehreren** Treffern erscheint die Artikelliste zur Auswahl, bei **keinem** Treffer wird aus der
**Halbfertigartikelvorlage** der Materialart ein neuer Artikel erzeugt.

### Was passiert, wenn ich keine Halbfertigartikelvorlage hinterlegt habe?

Findet die Suche keinen bestehenden Artikel und ist keine **Halbfertigartikelvorlage** an der Materialart
hinterlegt, kann kein neuer Halbfertigartikel erzeugt werden – die Aufteilung liefert dann für diese Stufe
keinen Artikel. Hinterlegen Sie je Materialart eine aktivierte Artikelvorlage.

### Warum kann ich die Aufteilungsoption im Arbeitsplan nicht setzen?

Die Option ist nur setzbar, wenn der Arbeitsplan **nicht zertifiziert** ist, **kein** aufgeteilter Arbeitsplan
ist (leere **Urspr. Arbeitsplannr.**) und mindestens eine als **Halbfertigartikel** gekennzeichnete
Arbeitsgangzeile existiert. Andernfalls erscheint „Es kann keine Halbfertigteilarbeitsgangzeile gefunden
werden.".

### Warum erhalte ich „Der Lagerort des Arbeitsgangs und der Arbeitsplatzgruppe muss unterschiedlich sein."?

Weil die **Halbfertigteil letzter AG Option** nur sinnvoll ist, wenn Material tatsächlich umgelagert wird.
Sind Arbeitsgang-Lagerort und Arbeitsplatzgruppen-Lagerort identisch, ist keine Umlagerung nötig und die
Option wird nicht zugelassen bzw. auf **(leer)** zurückgesetzt.

### Wann wird ein Halbfertig-Arbeitsgang automatisch auf „Fertig" gesetzt?

Wenn die **Halbfertigteil letzter AG Option = Beim Buchen des Umlagerungseingangs** gesetzt ist und die
gebuchte Eingangsmenge der Umlagerung die Restmenge der **FA-Komponente** deckt. Dann setzt das System den
Arbeitsgang beim Buchen des Umlagerungseingangs auf **Fertig**.

### Warum wird der Wert einer Eigenschaft abgelehnt?

Bei numerischen Eigenschaften muss der **Wert** innerhalb **Wert erlaubt von/bis** liegen und in den korrekten
Datentyp wandelbar sein; bei Eigenschaften mit **Eigenschaftswerte verwenden** muss der Wert in der
hinterlegten Werteliste stehen. Andernfalls erscheinen Meldungen wie „darf nicht weniger als …", „größer sein
als …" oder „Wert … ist nicht erlaubt/wurde nicht in den Eigenschaftswerten gefunden!".

### Wie erkenne ich, welche Chargen und Arbeitspläne aus der Halbfertigerzeugung stammen?

Über die Kennzeichnungen: **Chargennr.-Informationskarte → Halbfertigartikel** für Halbfertigchargen sowie
**Arbeitsplankarte → Aufgeteilter Arbeitsgang / Urspr. Arbeitsplannr.** für automatisch erzeugte Arbeitspläne.
Am Fertigungsauftrag zeigt **Aufgeteilte Zeilen** an, dass die Aufteilung bereits erfolgt ist.

---

## Typische Anwendungsfälle

Die folgenden Szenarien zeigen den Ablauf aus Sicht der Anwender. Jeder Screen und jede Aktion ist im Code
des Moduls hinterlegt.

### Anwendungsfall 1: Kundenauftrag mit mehrstufigem Halbfertigartikel

**Auslöser.** Ein Kunde bestellt telefonisch einen Artikel, dessen Fertigung mehrere Halbfertigstufen an
verschiedenen Arbeitsplatzgruppen durchläuft.

**Einstieg in BC.** Der Vertrieb legt den **Verkaufsauftrag** an. Aus der Auftragszeile wird ein
**Fertigungsauftrag** erzeugt. Voraussetzung: Der Arbeitsplan des Artikels enthält Halbfertig-Arbeitsgänge,
die Arbeitsplatzgruppen sind als **Halbfertigartikel** gekennzeichnet und die **Materialeigenschaftsänderungen**
sind gepflegt (siehe *Einrichtung* / *Stammdaten*).

**Kernablauf.**
1. Der Arbeitsplankopf trägt **Aufteilungsoption = Bei Verkaufsfreigabe**.
2. Mit der **Verkaufsfreigabe** teilt das System den Fertigungsauftrag automatisch auf (**FA Split**): je
   Halbfertigstufe eine Fertigungsauftragszeile, passender Halbfertigartikel gesucht bzw. aus der
   **Halbfertigartikelvorlage** erzeugt, **FA-Komponenten** und **Umlagerungsaufträge** angelegt.
3. Der Fertigungssteuerer gibt den Auftrag frei und bucht die **Ausgabe** je Arbeitsgang.
4. Beim Buchen wird die **Umlagerung** automatisch verarbeitet; der letzte Halbfertig-Arbeitsgang wird beim
   **Umlagerungseingang** auf **Fertig** gesetzt (**Halbfertigteil letzter AG Option = Beim Buchen des
   Umlagerungseingangs**).

**Abschluss.** Bei Bedarf startet der Anwender über **Halbfertigartikel-Nachfolgeauftrag erstellen** die
Folgestufe. Die entstandenen Halbfertigchargen sind auf der **Chargennr.-Informationskarte** als
**Halbfertigartikel** erkennbar.

### Anwendungsfall 2: Manuelle Aufteilung eines festgeplanten Auftrags

**Auslöser.** Der Arbeitsvorbereiter legt für einen Lagerartikel proaktiv einen Fertigungsauftrag an, ohne
Bezug zu einem Verkaufsauftrag.

**Einstieg in BC.** **Festgeplanter Fertigungsauftrag** anlegen, Artikel/Menge/Arbeitsplan erfassen und
aktualisieren.

**Kernablauf.**
1. Der Arbeitsplan trägt **Aufteilungsoption = (leer)** oder **Bei FA-Freigabe**; der Anwender möchte die
   Aufteilung kontrolliert selbst anstoßen.
2. Über **Funktionen → FA Split** wird die Aufteilung ausgelöst. Sind keine Halbfertig-Arbeitsgänge
   vorhanden, meldet das System „Es wurden keine Zeilen zum Splitten gefunden.".
3. Liefert die Eigenschaftssuche mehrere passende Halbfertigartikel, wählt der Anwender in der Artikelliste
   den gewünschten aus.
4. Das System erzeugt Halbfertigzeilen, Komponenten und **Umlagerungsaufträge**; am Auftrag wird
   **Aufgeteilte Zeilen** gesetzt.

**Abschluss.** Der Auftrag wird freigegeben und wie in Anwendungsfall 1 gebucht.

### Anwendungsfall 3: Ausgabe buchen und Arbeitsgang über Umlagerungseingang abschließen

**Auslöser.** An einer Halbfertig-Arbeitsplatzgruppe ist eine Teilmenge fertig und soll an den nächsten
Lagerort weitergegeben werden.

**Einstieg in BC.** Der Werker bucht die **Ausgabe** des Halbfertig-Arbeitsgangs (Produktionsbuchblatt bzw.
Fertigmeldung am Freigegebenen Fertigungsauftrag).

**Kernablauf.**
1. Beim Buchen der Ausgabe ermittelt das Modul die zugehörige **Umlagerung** und bucht – abhängig von den
   Lagerorteinstellungen – Versand und Eingang automatisch.
2. Die **FA-Komponente** der Folgestufe wird in den Ziel-Lagerort bewegt; die Charge wird über die
   Reservierung durchgereicht.
3. Deckt die eingegangene Menge die Restmenge der Komponente und ist **Halbfertigteil letzter AG Option =
   Beim Buchen des Umlagerungseingangs** gesetzt, wird der Arbeitsgang auf **Fertig** gesetzt.

**Abschluss.** Teilmengen werden korrekt fortgeschrieben; der Arbeitsgang schließt erst, wenn die Restmenge
gedeckt ist. Über die Umlagerungszeilen (**Halbfertigartikel FA-Nr.** usw.) bleibt der Bezug zum
Fertigungsauftrag nachvollziehbar.
