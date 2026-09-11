---
title: Anwenderhandbuch m+m Logistic Differences
---

# Anwenderhandbuch m+m Logistic Differences

## Einleitung

Die Erweiterung **m+m Logistic Differences** steuert in Microsoft Dynamics 365 Business Central die **Über- und Unterlieferung** von Mengen. Für viele Unternehmen ist es entscheidend, kontrolliert zuzulassen oder zu verhindern, dass mehr oder weniger geliefert, empfangen, kommissioniert oder gebucht wird als ursprünglich vereinbart, weil solche Abweichungen weitreichende Folgen für Lieferkette, Bestand und Preisfindung haben.

Die App vergleicht bei jeder mengenrelevanten Aktion die aktuelle Menge mit einer hinterlegten **Ursprünglichen Menge** und wendet je Einrichtung eine der drei Reaktionen an: die Abweichung wird still zugelassen, sie löst eine **Warnung** mit Bestätigungsdialog aus, oder sie wird mit einer Fehlermeldung blockiert. Die Kontrollen greifen im **Einkauf**, **Verkauf**, in der **Umlagerung**, bei **Wareneingang** und **Warenausgang**, in den **Lageraktivitäten** (Kommissionierung, Einlagerung, Lagerbewegung), in den **Artikel Buch.-Blättern** sowie bei der **Kommissionierung Komponente** aus der Fertigung.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender**, die täglich Belege bearbeiten und buchen: Einkäufer, Vertriebsinnendienst, Lager- und Kommissionierpersonal. Sie geben Mengen in Auftrags-, Bestell-, Umlagerungs- und Lagerbelegen ein und entscheiden im Dialog über zulässige Abweichungen. Sekundär angesprochen sind **Administratoren und Key-User**, die die Toleranzregeln in der Einrichtung und in den Stammdaten hinterlegen.

**Prozessüberblick.** Der Administrator aktiviert je Prozess die Kontrolle und legt Kontrollmethode und -wert fest (**Über-/Unterlieferung Einrichtung**), verfeinert die Regeln optional artikel- oder partnerspezifisch (**Über-/Unterlieferungs Artikeleinrichtung**) und legt Vorgaben (**Über-/Unterlieferungsvorgaben**) an. Im Tagesablauf setzt der Anwender die **Ursprüngliche Menge**, ändert die zu liefernde/empfangende Menge und reagiert auf Warnung oder Fehler. Jede bestätigte Abweichung wird im **Über-/Unterlieferung Aktivitätsprotokoll** revisionssicher dokumentiert.

---

## Schnellstart für Anwender

Die folgenden Schritte führen vom leeren System zur ersten kontrollierten Überlieferung. Die Reihenfolge folgt der technischen Abhängigkeit: zuerst Einrichtung, dann Beleg.

1. **Einrichtung öffnen.** Rufen Sie über **Suchen** die Seite **Über-/Unterlieferung Einrichtung** auf. Sie ist eine unternehmensweite Einrichtungsseite (ein Datensatz je Mandant).
2. **Prozess aktivieren.** Setzen Sie im Inforegister **Allgemein** das gewünschte Kennzeichen, z. B. **VK-Überlieferungen aktiv** für den Verkauf. Ohne dieses Kennzeichen prüft die App den Prozess nicht.
3. **Vorgaben prüfen.** Kontrollieren Sie im Unterformular **Vorgaben** die Zeile für **Verkauf / Überlieferung**, wählen Sie eine **Kontrollmethode** (z. B. **Absoluter Wert**) und tragen Sie einen **Kontrollwert** (z. B. 10) ein. Setzen Sie **Warnung**, wenn der Anwender die Grenze bestätigen dürfen soll.
4. **(Optional) Spezifische Regel.** Legen Sie in der **Über-/Unterlieferungs Artikeleinrichtung** eine feinere Regel für einen bestimmten Debitor, Kreditor, Lagerort oder Artikel an.
5. **Beleg anlegen.** Öffnen Sie einen **Verkaufsauftrag** und erfassen Sie eine Zeile mit einer **Menge** (z. B. 10). Die App schreibt automatisch die **Ursprüngliche Menge**.
6. **Menge ändern.** Ändern Sie **Menge akt. Lieferung** über die Toleranz hinaus (z. B. 21). Es erscheint bei aktiver **Warnung** ein Bestätigungsdialog; bei **Warnung = Nein** eine Fehlermeldung. Bei Ablehnung wird auf die maximal erlaubte Menge zurückgesetzt, bei Bestätigung wird die Abweichung übernommen und protokolliert.
7. **(Unterlieferung) Beleg abschließen.** Möchten Sie eine Zeile trotz Restmenge beenden, setzen Sie in der Belegzeile das Kennzeichen **Beleg komplett** und bestätigen Sie die Rückfrage zur Mengenaktualisierung.

Für die reine Belegprüfung genügen die Schritte 5–7, sofern die Einrichtung bereits steht.

---

## Einrichtung

Die Einrichtung ist der umfangreichste Teil dieser App. Ein Administrator hinterlegt hier vor der ersten Nutzung, **welche** Prozesse geprüft werden, **wie** Abweichungen kontrolliert werden und **ob** der Anwender Grenzen per Bestätigung überschreiten darf.

### Über-/Unterlieferungskontrolle einrichten

**Wer/wann/wofür.** Diese zentrale Einrichtung nimmt der Administrator einmalig je Mandant vor der ersten Belegbearbeitung vor. Sie schaltet die Prüfung je Prozess frei und legt das Standardverhalten fest, auf das alle Belege im Kapitel **Tägliche Arbeit** zurückgreifen.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Über-/Unterlieferung Einrichtung**. Es handelt sich um eine unternehmensweite Einrichtungsseite; beim ersten Öffnen wird der Datensatz samt Vorgaben automatisch angelegt.

#### Prozess-Aktivierung (Inforegister Allgemein)

Jedes Kennzeichen schaltet die Kontrolle für einen Prozess vollständig ein oder aus.

| Einrichtung | Erläuterung |
|---|---|
| **EK-Überlieferungen aktiv** | Wenn aktiviert, prüft die App im Einkauf jede zu empfangende Menge, die über der Ursprünglichen Menge liegt; ohne Kennzeichen bleibt der Einkauf im Business-Central-Standard und Überlieferungen werden nicht kontrolliert. |
| **EK-Unterlieferungen aktiv** | Wenn aktiviert, greift die Kontrolle, sobald im Einkauf weniger empfangen wird als ursprünglich vereinbart; ermöglicht damit das kontrollierte Beenden von Restmengen über **Beleg komplett**. |
| **VK-Überlieferungen aktiv** | Wenn aktiviert, prüft die App im Verkauf jede Liefermenge oberhalb der Ursprünglichen Menge und löst je nach Regel Warnung oder Fehler aus. |
| **VK-Unterlieferungen aktiv** | Wenn aktiviert, kontrolliert die App Verkaufslieferungen unterhalb der Ursprünglichen Menge und erlaubt das gesteuerte Abschließen von Teillieferungen. |
| **Umlagerung - Überlieferung aktiv** | Wenn aktiviert, wird bei Umlagerungsaufträgen eine zu versendende Menge über der Ursprünglichen Menge kontrolliert. |
| **Umlagerung - Unterlieferung aktiv** | Wenn aktiviert, kontrolliert die App Umlagerungen unterhalb der Ursprünglichen Menge und ermöglicht das Beenden von Restmengen. |
| **Überlieferung aktivieren** (Artikel Buch.-Blatt) | Wenn aktiviert, prüft die App im Artikel Buch.-Blatt gebuchte Mengen oberhalb der Ursprünglichen Menge; ohne Kennzeichen wird die Buch.-Blattmenge nicht gegen eine Toleranz geprüft. |
| **Unterlieferung aktivieren** (Artikel Buch.-Blatt) | Wenn aktiviert, kontrolliert die App im Artikel Buch.-Blatt Mengen unterhalb der Ursprünglichen Menge. |
| **Kommiss. Komp. Überlieferung aktiv** | Wenn aktiviert, prüft die App bei der Kommissionierung von Fertigungskomponenten zu bearbeitende Mengen über der Ursprünglichen Menge; damit lässt sich mehr Material entnehmen, wenn es die Regel zulässt. |
| **Kommiss. Komp. Unterlieferung aktiv** | Wenn aktiviert, kontrolliert die App die Komponentenkommissionierung unterhalb der Ursprünglichen Menge und erlaubt das kontrollierte Beenden. |

#### Festpreis bei Über-/Unterlieferung

Diese vier Kennzeichen steuern, ob eine durch die Über-/Unterlieferung ausgelöste Mengenänderung die Preisneuberechnung im Beleg auslösen darf.

| Einrichtung | Erläuterung |
|---|---|
| **EK-Festpreis für Überlieferungen** | Wenn aktiviert, bleibt der Einkaufspreis bei einer Überlieferung unverändert; die App unterdrückt beim Zurückschreiben der gebuchten Menge auf die Bestellzeile die Neukalkulation, sodass der ursprünglich vereinbarte Preis erhalten bleibt. |
| **EK-Festpreis für Unterlieferungen** | Wenn aktiviert, bleibt der Einkaufspreis bei einer Unterlieferung unverändert; ohne Kennzeichen kann eine reduzierte Menge eine Preisstaffel neu auslösen. |
| **VK-Festpreis für Überlieferungen** | Wenn aktiviert, bleibt der Verkaufspreis bei einer Überlieferung fix; die App verhindert die Neuberechnung des Zeilenpreises bei der automatischen Mengenaktualisierung nach der Lagerbuchung. |
| **VK-Festpreis für Unterlieferungen** | Wenn aktiviert, bleibt der Verkaufspreis bei einer Unterlieferung fix, auch wenn die reduzierte Menge sonst eine andere Preisstaffel ergäbe. |

#### Menge aus Verfolgung aktualisieren

In der Gruppe **Menge aus Verfolgung aktualisieren** legt der Administrator je Bereich fest, wie sich die App verhält, wenn über die **Artikelverfolgungszeilen** eine von der Belegmenge abweichende Gesamtmenge erfasst wird. Jedes Feld ist eine Option mit den gleichen drei Werten.

| Einrichtung | Erläuterung |
|---|---|
| **Einkauf** | Steuert das Rückschreiben der aus der Artikelverfolgung erfassten Menge in die Einkaufszeile. |
| **Verkauf** | Steuert das Rückschreiben der Verfolgungsmenge in die Verkaufszeile. |
| **Umlagerung** | Steuert das Rückschreiben der Verfolgungsmenge in die Umlagerungszeile. |
| **Wareneingänge** | Steuert das Verhalten bei abweichender Verfolgungsmenge im Wareneingang. |
| **Warenausgänge** | Steuert das Verhalten bei abweichender Verfolgungsmenge im Warenausgang. |
| **Lageraktivitäten** | Steuert das Verhalten in Kommissionier- und Einlagerungsaktivitäten. |
| **Artikel Buch.-Blatt** | Steuert das Verhalten im Artikel Buch.-Blatt (Untergruppe **Buch.-Blätter**). |
| **Umlagerung Buch.-Blatt** | Steuert das Verhalten im Umlagerungs-Buch.-Blatt. |
| **Inventur Buch.-Blätter** | Steuert das Verhalten im Inventur-Buch.-Blatt. |
| **Neubewertungs Buch.-Blätter** | Steuert das Verhalten im Neubewertungs-Buch.-Blatt. |

Die Optionswerte je Feld bedeuten:

- **Standard:** Es gilt das Standardverhalten von Business Central; die App aktualisiert die Belegmenge nicht selbsttätig aus der Verfolgung.
- **Immer:** Weicht die in der Verfolgung erfasste Menge von der Belegmenge ab, wird die Belegmenge ohne Rückfrage auf die Verfolgungsmenge gesetzt.
- **Frage:** Bei Abweichung erscheint vor der Aktualisierung die Rückfrage *„Die zugewiesene Menge … unterscheidet sich von der Belegmenge … Wollen Sie die Menge im Beleg aktualisieren?“*; erst nach Bestätigung wird die Belegmenge angepasst.

#### Berechtigungen

Zur App gehört der Berechtigungssatz **MuM OS Permission**. Er legt fest, welche Aktionen Anwender in den Tabellen und Seiten der Über-/Unterlieferung ausführen dürfen, und bestimmt damit die Berechtigungen für Einrichtung, Artikeleinrichtung, Belegeinrichtung und Aktivitätsprotokoll. Weisen Sie diesen Berechtigungssatz den Rollen zu, die Toleranzregeln pflegen oder Abweichungen bestätigen sollen.

#### Über-/Unterlieferungsvorgaben

**Wer/wann/wofür.** Die **Vorgaben** definieren das Standardverhalten je Kombination aus **Ausgleich mit Art** und **Definiert**. Der Administrator pflegt sie direkt im Unterformular **Vorgaben** der Einrichtungsseite. Sie greifen immer dann, wenn keine spezifischere Artikeleinrichtung existiert, und werden beim Verarbeiten eines Belegs in die **Belegeinrichtung** kopiert.

**Einstieg:** Das Unterformular **Vorgaben** wird direkt in der **Über-/Unterlieferung Einrichtung** angezeigt. Fehlen Zeilen, erzeugt die Aktion **Standard erstellen** die zehn Standardzeilen (Alle Debitoren, Alle Kreditoren, Umlagerung, Artikel Buch.-Blatt, Kommissionierung Komponente – je Überlieferung und Unterlieferung).

| Einrichtung | Erläuterung |
|---|---|
| **Ausgleich mit Art** | Zeigt die Bezugsgröße der Vorgabezeile (z. B. Alle Debitoren, Alle Kreditoren, Umlagerung). Das Feld ist nicht editierbar, da die Vorgaben systemseitig angelegt werden. |
| **Definiert** | Gibt an, ob die Zeile die **Überlieferung** oder die **Unterlieferung** steuert; nicht editierbar. |
| **Kontrollmethode** | Legt fest, wie die Abweichung begrenzt wird (siehe Werte unten). |
| **Kontrollwert** | Wenn die Kontrollmethode Prozentsatz oder Absoluter Wert ist, ist hier der Grenzwert einzugeben (Pflichtfeld, sonst gesperrt). Bei Prozentsatz sind Werte zwischen 0 und 100 zulässig. |
| **Warnung** | Wenn aktiviert, darf der Anwender die Grenze über einen Bestätigungsdialog überschreiten (die Abweichung wird protokolliert); wenn nicht aktiviert, blockiert eine Überschreitung mit Fehler. Nur bei Prozentsatz/Absoluter Wert relevant. |

Werte der **Kontrollmethode**:

- **Vorgabe:** Bei Über- oder Unterlieferung gilt das Standardverhalten von Business Central; es wird kein eigener Grenzwert geprüft und kein Kontrollwert erwartet.
- **Prozentsatz:** Die zulässige Abweichung wird als Prozentsatz der Ursprünglichen Menge berechnet (bei Überlieferung Ursprüngliche Menge + Prozent, bei Unterlieferung Ursprüngliche Menge − Prozent).
- **Absoluter Wert:** Die zulässige Abweichung ist ein fester Mengenbetrag oberhalb bzw. unterhalb der Ursprünglichen Menge.

**Prozessschritte (Aktivierung end-to-end).** Zuerst legen Sie mit **Standard erstellen** die Vorgaben an und hinterlegen je Zeile Kontrollmethode/-wert und Warnung; danach setzen Sie im Inforegister **Allgemein** das Prozess-Kennzeichen (z. B. **VK-Überlieferungen aktiv**); schließlich greift die Regel im Tagesablauf, sobald der Anwender in einem **Verkaufsauftrag** die Menge außerhalb der Toleranz ändert (siehe **Tägliche Arbeit am Beleg**). Feinere Ausnahmen definieren Sie anschließend in der **Über-/Unterlieferungs Artikeleinrichtung**.

---

## Stammdaten

Die eigentlichen, vom Anwender gepflegten Toleranzregeln liegen in der **Über-/Unterlieferungs Artikeleinrichtung**. Von den Stammdatenkarten aus (Debitor, Kreditor, Artikel, Lagerort) gelangt der Anwender direkt in die gefilterte Sicht dieser Regeln.

### Spezifische Regeln in der Artikeleinrichtung einrichten

**Wer/wann/wofür.** Key-User pflegen hier vor bzw. während der laufenden Nutzung spezifischere Regeln als die Vorgaben – etwa „Kreditor X darf Artikel Y um absolut 5 Stück unterliefern“. Diese Regeln überschreiben die Vorgaben und werden beim Verarbeiten eines Belegs in die **Belegeinrichtung** kopiert. Konsumiert werden sie im Kapitel **Tägliche Arbeit am Beleg**.

**Einstieg:**
- Über die Stammdatenkarte oder -liste: Öffnen Sie z. B. die **Debitorenkarte** und wählen Sie die Aktion **Über-/Unterlieferung**. Business Central öffnet die **Über-/Unterlieferungs Artikeleinrichtung** gefiltert auf diesen Debitor. Dieselbe Aktion steht auf **Kreditor**, **Artikel** und **Lagerort** (jeweils Karte und Liste) zur Verfügung.
- Alternativ über **Suchen** oder über die Aktion **Über-/Unterlieferung Item Setup** auf der Einrichtungsseite (ungefilterte Gesamtliste).

| Feld | Erläuterung |
|---|---|
| **Definiert** | Wenn **Überlieferung** gewählt ist, gilt die Zeile für Mengen über der Ursprünglichen Menge; bei **Unterlieferung** für Mengen darunter. Pflichtfeld – ohne Auswahl lässt sich die Zeile nicht speichern. |
| **Ausgleich mit Art** | Legt die Bezugsgröße der Regel fest (Werte unten). Bei Wechsel wird die Ausgleichsnummer geleert. |
| **Ausgleich mit Nummer** | Wenn Ausgleich mit Art einen konkreten Kreditor, Debitor, Lagerort oder eine Buch.-Blattvorlage benennt, wird hier die zugehörige Nummer eingetragen (Pflichtfeld in diesem Fall); bei „Alle …“ bleibt das Feld leer. |
| **Artikelart** | Wenn **Artikel** gewählt ist, gilt die Regel nur für einen bestimmten Artikel; bei **Alle Artikel** für alle Artikel der Bezugsgröße. |
| **Artikel Nr.** | Nur editierbar, wenn Artikelart = Artikel. Bestimmt den Artikel, für den die Regel gilt. |
| **Beschreibung** | Zeigt den Beschreibungstext des gewählten Artikels an (nicht editierbar). |
| **Variantencode** | Wenn gesetzt, wird die Regel auf eine bestimmte Variante des Artikels eingeschränkt. |
| **Kontrollmethode** | Wie in den Vorgaben: **Vorgabe** (BC-Standard), **Prozentsatz** oder **Absoluter Wert**. |
| **Kontrollwert** | Grenzwert für Prozentsatz/Absoluter Wert; nur dann editierbar und dann Pflichtfeld. |
| **Einheitencode** | Wenn gesetzt, bezieht sich der absolute Kontrollwert auf diese Mengeneinheit; bei Artikelart = Artikel ist der Einheitencode Pflicht. |
| **Warnung** | Wenn aktiviert, kann der Anwender die Grenze per Bestätigung überschreiten (mit Protokolleintrag); wenn nicht aktiviert, blockiert die Überschreitung mit Fehler. |

Werte der **Ausgleich mit Art** in der Artikeleinrichtung:

- **Alle Kreditoren:** Regel gilt für Einkaufs- und Eingangsprozesse aller Kreditoren.
- **Kreditor:** Regel gilt nur für den in **Ausgleich mit Nummer** genannten Kreditor.
- **Alle Debitoren:** Regel gilt für Verkaufs-, Versand- und Kommissionierprozesse aller Debitoren.
- **Debitor:** Regel gilt nur für den genannten Debitor.
- **Umlagerung:** Regel gilt für Umlagerungsprozesse; die Nummer verweist auf einen Lagerort (Herkunft).
- **Artikel Buch.-Blatt:** Regel gilt für ein Artikel Buch.-Blatt; die Nummer verweist auf die Buch.-Blattvorlage.
- **Kommissionierung Komponente:** Regel gilt für die Kommissionierung von Fertigungskomponenten (keine Ausgleichsnummer).

Werte der **Artikelart**:

- **Alle Artikel:** Die Regel gilt für alle Artikel der gewählten Bezugsgröße.
- **Artikel:** Die Regel gilt nur für den in **Artikel Nr.** angegebenen Artikel (Einheitencode dann Pflicht).

**Prozessschritte.** Zuerst wählen Sie **Definiert** (Über-/Unterlieferung), danach **Ausgleich mit Art** und ggf. **Ausgleich mit Nummer**, dann optional Artikel/Variante/Einheit, schließlich **Kontrollmethode**, **Kontrollwert** und **Warnung**. Die Zeile wird beim Speichern geprüft (Ausgleichsnummer und Artikel-/Einheitenpflicht). Existiert keine passende Artikeleinrichtung, greifen die **Vorgaben**. Löschen Sie einen Debitor, Kreditor, Artikel, eine Variante oder einen Lagerort, entfernt die App die zugehörigen Artikeleinrichtungszeilen automatisch.

### Artikelverfolgung

**Wer/wann/wofür.** Wird ein Artikel mit **Artikelverfolgung** (Serien-/Chargennummern) geführt, erfasst der Anwender die Mengen in den **Artikelverfolgungszeilen**. Beim Schließen dieser Zeilen prüft die App, ob die dort erfasste Gesamtmenge die Über-/Unterlieferungsregel des Belegs verletzt.

**Einstieg:** In der Belegzeile über **Zeile → Artikelverfolgungszeilen**.

**Ablauf.** Ändert der Anwender die **Menge (Basis)** über die Toleranz hinaus und schließt die Seite, wird – abhängig von **Warnung** – eine Warnung oder ein Fehler ausgelöst. Wird die Warnung akzeptiert, übernimmt das System die Gesamtmenge in die Belegzeile und passt **Menge** und **Menge akt. Lieferung** an; die Rückfrage folgt dem in **Menge aus Verfolgung aktualisieren** eingestellten Wert (**Standard/Immer/Frage**).

---

## Tägliche Arbeit am Beleg

Die tägliche Prüfung findet direkt in den Standardbelegen statt. Das Verhalten wird durch die zuvor beschriebenen Seiten **Über-/Unterlieferung Einrichtung** (Prozess-Aktivierung, Kontrollmethode) und **Über-/Unterlieferungs Artikeleinrichtung** (spezifische Regeln) gesteuert; die konkret angewandte Regel wird pro Beleg in der **Über-/Unterlieferung Belegeinrichtung** festgehalten. Die Erweiterung ergänzt in allen unterstützten Belegen dieselben zwei Zeilenfelder und dieselbe Zeilenaktion.

### Zeilenfelder und -aktion (alle Belege)

Diese Felder ergänzt die App im Zeilen-Unterformular von **Verkaufsauftrag**, **Bestellung**, **Umlagerungsauftrag**, in den **Artikel Buch.-Blättern** sowie in allen Lagerbeleg-Zeilen (Wareneingang, Warenausgang, Kommissionierung, Einlagerung, Lagerbewegung).

| Feld | Erläuterung |
|---|---|
| **Ursprüngliche Menge** | Enthält die ursprünglich vereinbarte Menge, gegen die jede spätere Änderung geprüft wird. Wenn dieses Feld gesetzt ist und die aktuelle Menge abweicht, greift die Über-/Unterlieferungskontrolle; ist es 0, findet keine Prüfung statt. Das Feld ist nicht direkt editierbar. |
| **Beleg komplett** | Wenn aktiviert, erklärt der Anwender die Zeile trotz Restmenge für abgeschlossen, sodass keine weiteren Lieferungen/Eingänge erwartet werden. Nur für Unterlieferung und nur bei bereits gebuchter Menge > 0 setzbar; beim Setzen wird die Belegmenge nach Bestätigung auf die bereits gelieferte/empfangene Menge reduziert. Ändert der Anwender danach die Menge, wird das Kennzeichen automatisch entfernt. |

Zeilenaktion:

- **Ursprüngliche Menge setzen** (im Inforegister **Zeilen**): Ersetzt nach Rückfrage die **Ursprüngliche Menge** durch die aktuelle **Menge** und setzt **Beleg komplett** zurück. Nutzen Sie diese Aktion, wenn sich die vereinbarte Menge legitim geändert hat und künftige Prüfungen gegen den neuen Wert laufen sollen. Die Änderung wird protokolliert.

### Belegaktionen (Kopf)

Im Belegkopf (Menüband **Zugehörig/Navigation**) stellt die App die Gruppe **Über-/Unterlieferung** bereit:

- **Belegeinrichtung**: Öffnet die **Über-/Unterlieferung Belegeinrichtung** für den aktuellen Beleg. Hier sieht und ändert der Anwender die konkret für diesen Beleg ermittelte Regel.
- **Aktivitätsprotokoll**: Öffnet das **Über-/Unterlieferung Aktivitätsprotokoll** gefiltert auf den aktuellen Beleg.

### Über-/Unterlieferung Belegeinrichtung

**Wer/wann/wofür.** Die Belegeinrichtung ist die pro Beleg wirksame Kopie der Vorgabe- bzw. Artikelregel. Der Anwender öffnet sie über die Belegaktion **Belegeinrichtung**, um die für diesen Beleg geltende Regel zu prüfen oder den **Kontrollwert** anzupassen.

**Einstieg:** Im Beleg (z. B. **Verkaufsauftrag**) über **Über-/Unterlieferung → Belegeinrichtung**. Die Seite ist nicht über **Suchen** erreichbar, sondern ausschließlich aus dem Beleg heraus.

| Feld | Erläuterung |
|---|---|
| **Belegzeilennr.** | Verknüpft die Regel mit der Belegzeile (nicht editierbar). |
| **Definiert** | Zeigt, ob die Regel Über- oder Unterlieferung betrifft (nicht editierbar). |
| **Ausgleich mit Art** | Bezugsgröße der ermittelten Regel (nicht editierbar). |
| **Ausgleich mit Nummer** | Konkreter Kreditor/Debitor/Lagerort der Regel (nicht editierbar). |
| **Artikelart** | Alle Artikel oder Artikel (nicht editierbar). |
| **Artikel Nr.** | Betroffener Artikel (nicht editierbar). |
| **Beschreibung** | Artikelbeschreibung (nicht editierbar). |
| **Variantencode** | Betroffene Variante (nicht editierbar). |
| **Kontrollmethode** | Angewandte Methode: Vorgabe, Prozentsatz oder Absoluter Wert (nicht editierbar; aus Vorgabe/Artikeleinrichtung übernommen). |
| **Kontrollwert** | Nur editierbar, wenn die Kontrollmethode nicht Vorgabe ist; hier kann der Anwender die Grenze für genau diesen Beleg feinjustieren. |
| **Einheitencode** | Mengeneinheit des absoluten Kontrollwerts (nicht editierbar). |
| **Warnung** | Zeigt, ob die Grenze per Bestätigung überschreitbar ist (nicht editierbar). |

Aktion **Aktualisieren**: Ermittelt die Belegeinrichtungszeilen anhand der aktuellen Belegzeilen und Regeln neu. Nutzen Sie sie, wenn sich Zeilen oder Stammdatenregeln nach dem ersten Öffnen geändert haben.

### Ablauf bei Mengenänderung

Ändert der Anwender im Verkaufsauftrag die **Menge akt. Lieferung** (bzw. im Einkauf die zu empfangende Menge, in der Umlagerung die zu liefernde Menge) über die zulässige Grenze hinaus, läuft folgende Prüfung:

1. Zeile auf dem Beleg auswählen und **Menge akt. Lieferung** ändern.
2. Die App vergleicht die geplante Gesamtmenge (bereits geliefert + zu liefern) mit der aus **Kontrollmethode** und **Kontrollwert** berechneten Grenze.
3. **Innerhalb der Toleranz:** Die Menge wird ohne Meldung übernommen.
4. **Außerhalb + Warnung = Nein:** Es erscheint eine Fehlermeldung mit Angabe der aktuellen Beschränkungen und der maximal bzw. minimal erlaubten Menge; die Änderung wird zurückgewiesen.
5. **Außerhalb + Warnung = Ja:** Es erscheint der Bestätigungsdialog *„… würden Sie trotzdem fortfahren wollen?“*. Bei **Ja** wird die Menge übernommen und ein Eintrag im **Aktivitätsprotokoll** geschrieben; bei **Nein** wird auf die erlaubte Menge zurückgesetzt.
6. **Unterlieferung abschließen:** Ist weniger geliefert als vereinbart und soll der Rest entfallen, setzen Sie **Beleg komplett**. Die App erlaubt dies nur bei Unterlieferung und gebuchter Menge > 0, fragt *„Die zugewiesene Menge … Wollen Sie die Menge im Beleg aktualisieren?“* und setzt die Belegmenge auf die gelieferte Menge.

Bei **Direktlieferung** aktualisiert die App nach der Buchung sowohl die Einkaufs- als auch die Verkaufszeile gemäß der greifenden Über- oder Unterlieferungsregel.

---

## Lager, Kommissionierung und Folgebelege

Die Über-/Unterlieferungskontrolle greift auch in den Lagerprozessen. Voraussetzung ist, dass der jeweilige Prozess in der **Über-/Unterlieferung Einrichtung** aktiviert ist (**Wareneingänge**, **Warenausgänge**, **Lageraktivitäten**, **Kommiss. Komp. …**). Die Zeilenfelder **Ursprüngliche Menge** und **Beleg komplett** sowie die Aktion **Ursprüngliche Menge setzen** stehen wie im Kapitel **Tägliche Arbeit** beschrieben in allen Lagerbelegzeilen zur Verfügung.

### Wareneingang, Warenausgang und Kommissionierung

- **Wareneingang** (aus Bestellung oder eingehender Umlagerung): Beim Erfassen der zu empfangenden Menge prüft die App gegen die Einkaufs- bzw. Umlagerungsregel. Über die Kopfaktion **Über-/Unterlieferung → Belegeinrichtung** öffnen Sie die für den Herkunftsbeleg geltende Regel; über **Aktivitätsprotokoll** die dazugehörigen Bestätigungen.
- **Warenausgang** (aus Verkaufsauftrag oder ausgehender Umlagerung): Analog wird die zu liefernde Menge geprüft; die Belegaktionen öffnen die Belegeinrichtung bzw. das Protokoll des Herkunftsbelegs (Verkauf oder Umlagerung).
- **Kommissionierung** und **Einlagerung** (Lager- und Lagerkommissionierung/-einlagerung): Beim Ändern der zu bearbeitenden Menge greift die Kontrolle für Verkauf, Einkauf, Umlagerung oder Kommissionierung Komponente – je nach Herkunft der Zeile. Die Kopfaktionen der Kommissionierung und Einlagerung öffnen ebenfalls **Belegeinrichtung** und **Aktivitätsprotokoll**.

Nach der Lagerbuchung schreibt die App die tatsächlich bewegte Menge auf die Herkunftszeile (Verkauf/Einkauf/Umlagerung) zurück und setzt – bei gesetztem **Beleg komplett** – die Zeile als abgeschlossen. Ist der passende **Festpreis** aktiv, bleibt der Preis dabei unverändert.

### Kommissionierung Komponente (Fertigung)

Bei der Kommissionierung von Fertigungskomponenten prüft die App die zu entnehmende Menge gegen die Regel **Kommissionierung Komponente**. Innerhalb der absoluten Toleranz (bezogen auf bereits registrierte und offene Kommissionierzeilen) lässt die App die Menge zu und umgeht die Standardprüfung „zu bearbeitende Menge größer als offene Menge“; außerhalb greift wie üblich Warnung oder Fehler.

### Kommissionierzeilen ausgleichen (Nehmen/Ablegen)

Bei mengenverändernder Kommissionierung müssen **Nehmen**- und **Ablegen**-Zeilen mengengleich bleiben. Die Hilfsseite **Zeilen** (zu den Kommissionierzeilen) unterstützt den Anwender dabei: Sie zeigt die zusammengehörenden Aktivitätszeilen, erlaubt das Aufteilen einer Zeile über **Zeile teilen** und prüft beim Schließen, dass die Summe der zu bearbeitenden Mengen in Nehmen- und Ablegen-Zeilen übereinstimmt. Weicht sie ab, meldet die App *„Menge in Nehmen-Zeilen … muss gleich der Menge in Ablegen-Zeilen … sein“*. Bereits am Herkunftsbeleg geänderte Zeilen sind gesperrt.

---

## Historie und Nachverfolgung

### Über-/Unterlieferung Aktivitätsprotokoll

**Wer/wann/wofür.** Jede über eine **Warnung** bestätigte Abweichung sowie jede Änderung der **Ursprünglichen Menge** wird revisionssicher protokolliert. Das Protokoll hilft, später nachzuvollziehen, wer wann welche Über- oder Unterlieferung akzeptiert hat.

**Einstieg:** Über **Suchen** (Verlaufsliste), über die Aktion **Aktivitätsprotokoll** auf der **Über-/Unterlieferung Einrichtung** oder über die Gruppe **Über-/Unterlieferung → Aktivitätsprotokoll** in jedem unterstützten Beleg (dann gefiltert auf diesen Beleg). Die Liste ist nicht editierbar und nach **Datum/Uhrzeit** absteigend sortiert.

| Feld | Erläuterung |
|---|---|
| **Herkunftsbeleg** | Verweist auf den Beleg, in dem die Abweichung aufgetreten ist. |
| **Definiert** | Ob es sich um eine Über- oder eine Unterlieferung handelte; bei einer reinen Änderung der Ursprünglichen Menge bleibt der Wert leer. |
| **Ursprüngliche Menge** | Die Menge, gegen die geprüft wurde. |
| **Min./Max. erlaubte Menge** | Die aus Kontrollmethode/-wert berechnete Grenze (leer, wenn nicht relevant). |
| **Finale Menge** | Die tatsächlich übernommene Menge nach Bestätigung. |
| **Benutzer** | Der Anwender, der die Abweichung bestätigt hat. |
| **Datum/Uhrzeit** | Zeitpunkt der Bestätigung. |
| **Ursprüngliche Menge setzen** | Wenn aktiviert, dokumentiert die Zeile eine manuelle Neusetzung der Ursprünglichen Menge (nicht eine Über-/Unterlieferung). |

Aktion **Verknüpften Datensatz öffnen**: Springt aus der Protokollzeile in den zugehörigen Herkunftsbeleg. Existiert der Beleg nicht mehr, meldet die App *„Herkunftsbeleg existiert nicht mehr!“*.

---

## Typische Anwendungsfälle

### Anwendungsfall 1 — Verkaufsüberlieferung mit Warnung

**Auslöser.** Ein Kunde ruft an und möchte statt der bestellten 10 Stück kurzfristig 21 Stück geliefert bekommen.

**Einstieg in BC.** Der Vertriebsinnendienst öffnet den betreffenden **Verkaufsauftrag** und wechselt in die Zeile.

**Kernablauf.**
1. Voraussetzung: In der **Über-/Unterlieferung Einrichtung** ist **VK-Überlieferungen aktiv** gesetzt, und die Vorgabe für Verkauf/Überlieferung nutzt **Absoluter Wert** = 10 mit **Warnung** = Ja (siehe **Einrichtung**).
2. Die Zeile trägt bereits die **Ursprüngliche Menge** 10.
3. Der Anwender ändert **Menge akt. Lieferung** auf 21.
4. Die App erkennt die Überschreitung der Grenze (10 + 10 = 20) und zeigt die Bestätigung an.
5. Bei **Ja** wird 21 übernommen; bei **Nein** wird auf 20 zurückgesetzt.

**Abschluss.** Die akzeptierte Abweichung erscheint im **Über-/Unterlieferung Aktivitätsprotokoll** mit **Ursprüngliche Menge** 10, **Min./Max. erlaubte Menge** 20, **Finale Menge** 21 und dem Benutzernamen.

### Anwendungsfall 2 — Einkaufsunterlieferung abschließen

**Auslöser.** Ein Lieferant teilt per E-Mail mit, dass er die restlichen 3 von 10 Stück nicht mehr liefern wird.

**Einstieg in BC.** Der Einkäufer öffnet die betreffende **Bestellung**.

**Kernablauf.**
1. Voraussetzung: **EK-Unterlieferungen aktiv** ist gesetzt; für Einkauf/Unterlieferung ist eine Regel hinterlegt.
2. Es sind bereits 7 Stück empfangen (**Menge akt. Lieferung** der laufenden Eingänge = 0).
3. Der Einkäufer setzt in der Bestellzeile das Kennzeichen **Beleg komplett**.
4. Die App prüft, dass eine Unterlieferung zulässig und die empfangene Menge > 0 ist, und fragt *„Die zugewiesene Menge … Wollen Sie die Menge im Beleg aktualisieren?“*.
5. Bei **Ja** wird die Bestellmenge auf 7 reduziert; weitere Eingänge sind damit ausgeschlossen.

**Abschluss.** Die Bestellung ist mengenmäßig abgeschlossen; die Aktion **Aktivitätsprotokoll** in der Belegkopf-Gruppe **Über-/Unterlieferung** zeigt die vorgenommenen Bestätigungen.

### Anwendungsfall 3 — Mehrentnahme bei der Komponentenkommissionierung

**Auslöser.** In der Fertigung wird beim Kommissionieren einer Komponente festgestellt, dass geringfügig mehr Material entnommen werden muss als im Fertigungsauftrag geplant.

**Einstieg in BC.** Das Lagerpersonal öffnet die **Kommissionierung** zur Fertigungskomponente.

**Kernablauf.**
1. Voraussetzung: **Kommiss. Komp. Überlieferung aktiv** ist gesetzt; für **Kommissionierung Komponente** ist eine Regel mit **Absoluter Wert** und **Warnung** hinterlegt.
2. Der Anwender erhöht in der Kommissionierzeile die zu bearbeitende Menge über die geplante Menge hinaus.
3. Liegt die Mehrmenge innerhalb der absoluten Toleranz (bezogen auf bereits registrierte und offene Kommissionierzeilen), lässt die App sie ohne Standardfehler zu.
4. Liegt sie darüber, erscheint Warnung oder Fehler gemäß Regel.

**Abschluss.** Nach dem Buchen der Kommissionierung ist die Komponentenmenge entsprechend angepasst; bestätigte Abweichungen stehen im **Aktivitätsprotokoll**.

---

## FAQ und Troubleshooting

### 1. Warum wird eine Mengenänderung gar nicht geprüft?
Die Prüfung greift nur, wenn der Prozess in der **Über-/Unterlieferung Einrichtung** aktiviert ist (z. B. **VK-Überlieferungen aktiv**) und die Zeile eine **Ursprüngliche Menge** > 0 besitzt. Ist die Ursprüngliche Menge 0 oder das Prozess-Kennzeichen nicht gesetzt, verhält sich Business Central im Standard.

### 2. Warum erscheint ein Fehler statt eines Bestätigungsdialogs?
Weil in der greifenden Regel (Vorgabe, Artikeleinrichtung oder Belegeinrichtung) das Kennzeichen **Warnung** nicht gesetzt ist. Ohne Warnung blockiert eine Grenzüberschreitung mit Fehler; mit Warnung darf der Anwender per Bestätigung fortfahren.

### 3. Warum lässt sich **Beleg komplett** nicht setzen?
**Beleg komplett** ist nur für **Unterlieferung** vorgesehen und nur, wenn bereits eine Menge > 0 geliefert/empfangen wurde. Bei einer Überlieferung oder ohne gebuchte Menge weist die App mit einem Hinweis darauf hin.

### 4. Warum verschwindet mein Häkchen **Beleg komplett** wieder?
Sobald der Anwender die Menge der Zeile erneut ändert, entfernt die App das Kennzeichen automatisch, damit weitere Lieferungen/Eingänge wieder möglich sind. Setzen Sie es nach der letzten Änderung erneut.

### 5. Woher weiß die App, welche Regel für meinen Beleg gilt?
Beim Verarbeiten sucht die App die spezifischste Regel: zuerst die **Über-/Unterlieferungs Artikeleinrichtung** (Artikel/Variante/Partner/Einheit), sonst die **Vorgaben**. Das Ergebnis wird in die **Über-/Unterlieferung Belegeinrichtung** kopiert, die Sie über die Belegaktion **Belegeinrichtung** einsehen können.

### 6. Ich habe die Regel geändert – warum wirkt sie im Beleg nicht?
Öffnen Sie im Beleg **Über-/Unterlieferung → Belegeinrichtung** und wählen Sie **Aktualisieren**. Die Belegeinrichtung ist eine Kopie der Stammregel und wird dadurch neu ermittelt.

### 7. Was bedeutet der Kontrollwert bei Prozentsatz genau?
Bei **Prozentsatz** wird die Grenze relativ zur Ursprünglichen Menge berechnet: bei Überlieferung Ursprüngliche Menge zzgl. des Prozentsatzes, bei Unterlieferung abzüglich. Zulässig sind Werte zwischen 0 und 100; andernfalls meldet die App einen Bereichsfehler.

### 8. Warum bleibt der Preis trotz geänderter Menge gleich?
Weil der passende **Festpreis**-Parameter aktiv ist (z. B. **VK-Festpreis für Überlieferungen**). Dann unterdrückt die App beim automatischen Zurückschreiben der Menge die Preisneuberechnung, sodass der ursprüngliche Preis erhalten bleibt.

### 9. Wie wirken sich abweichende Mengen in den Artikelverfolgungszeilen aus?
Beim Schließen der **Artikelverfolgungszeilen** prüft die App die erfasste Gesamtmenge gegen die Regel. Ob die Belegmenge anschließend automatisch angepasst wird, steuert die Option **Menge aus Verfolgung aktualisieren** (**Standard/Immer/Frage**) für den jeweiligen Bereich.

### 10. Wo sehe ich, wer eine Überlieferung genehmigt hat?
Im **Über-/Unterlieferung Aktivitätsprotokoll**. Jede über eine Warnung bestätigte Abweichung wird mit **Herkunftsbeleg**, **Definiert**, **Ursprüngliche Menge**, **Min./Max. erlaubte Menge**, **Finale Menge**, **Benutzer** und **Datum/Uhrzeit** festgehalten; über **Verknüpften Datensatz öffnen** gelangen Sie zurück zum Beleg.
