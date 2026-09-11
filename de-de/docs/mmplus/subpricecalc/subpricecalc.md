---
title: Anwenderhandbuch m+m Subcontracting Prices with Price Calculation
---

# Anwenderhandbuch m+m Subcontracting Prices with Price Calculation

## Einleitung

Die App m+m „Subcontracting Prices with Price Calculation“ ist eine Verbindungs-App für Microsoft Dynamics 365 Business Central. Sie verbindet die beiden Grund-Apps m+m „Fremdarbeitenpreise“ und m+m „Preisfindung“ und ergänzt die Fremdarbeitenpreise um eine **Berechnungseinheit** und einen **Berechnungspreis**. Dadurch lässt sich ein hinterlegter Fremdarbeitspreis nicht nur je Grundeinheit, sondern zusätzlich je frei gewählter Berechnungseinheit (zum Beispiel je 100 Stück, je Liter oder je Kilogramm) führen und automatisch umrechnen.

Der fachliche Nutzen: Sobald ein Kreditor seine Fremdarbeitspreise in einer anderen Mengeneinheit kalkuliert als der Artikel geführt wird, rechnet die App den Preis zuverlässig auf die Grundeinheit um. In den Belegen der Fremdbearbeitung – im **FA-Arbeitsplan** des freigegebenen Fertigungsauftrags, in den **Fremdarbeitsarbeitsblättern** und in der daraus erzeugten **Einkaufsbestellung** – werden Berechnungseinheit und Preis pro Berechnungseinheit mitgeführt, und die Direktkosten je Einheit werden automatisch aus dem gefundenen Fremdarbeitspreis abgeleitet.

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwender**, die täglich mit Fremdbearbeitung arbeiten: Fertigungsplanung und Einkauf, die freigegebene Fertigungsaufträge bearbeiten, Fremdarbeitsarbeitsblätter verarbeiten und Einkaufsbestellungen für Lohnarbeit erzeugen. Sekundär angesprochen sind **Administratoren und Stammdatenverantwortliche**, welche die Voraussetzungen einrichten (Arbeitsplatzgruppe für Fremdarbeit kennzeichnen, Fremdarbeitenpreise mit Berechnungseinheit pflegen).

**Kurzer Prozessüberblick.** Der Ablauf folgt dieser Kette: Eine **Arbeitsplatzgruppe** wird für Fremdarbeit gekennzeichnet und einem **Kreditor** zugeordnet → in den **Fremdarbeitenpreisen** wird ein Preis mit **Berechnungseinheit** und **Berechnungspreis** hinterlegt → im **freigegebenen Fertigungsauftrag** setzt der Anwender diese Arbeitsplatzgruppe im **FA-Arbeitsplan** ein → das System zieht automatisch den passenden Fremdarbeitspreis, überträgt Berechnungseinheit und Preis pro Berechnungseinheit und errechnet die Direktkosten je Einheit → aus dem **Fremdarbeitsarbeitsblatt** entsteht die **Einkaufsbestellung** mit denselben Werten.

**Voraussetzung (Installation).** Diese Verbindungs-App benötigt als Grundinstallation die Apps m+m „Fremdarbeitenpreise“ und m+m „Preisfindung“ sowie m+m „Cloud Base“. Ohne diese Grund-Apps stehen die hier beschriebenen Felder und Prozesse nicht zur Verfügung.

## Schnellstart für Anwender

Der Schnellstart beschreibt den kürzesten Weg vom eingerichteten System bis zum automatisch ermittelten Fremdarbeitspreis. Die Einrichtungsschritte stehen bewusst vor der täglichen Arbeit, weil ohne sie kein Preis gezogen wird.

1. **Einrichtung prüfen (einmalig, durch den Administrator).** Öffnen Sie die **Arbeitsplatzgruppenkarte** der betreffenden Arbeitsplatzgruppe, hinterlegen Sie den zugehörigen **Kreditor** und kennzeichnen Sie die Arbeitsplatzgruppe für Fremdarbeit (Aktivierung des spezifischen Einstandspreises am Arbeitsplatz). Wenn die Arbeitsplatzgruppe so gekennzeichnet ist, dann verwendet das System bei der Preisermittlung nicht den normalen Einkaufspreis, sondern den in den Fremdarbeitenpreisen für diese Arbeitsplatzgruppe hinterlegten Preis.
2. **Fremdarbeitenpreis mit Berechnungseinheit pflegen.** Öffnen Sie über die **Kreditorenkarte** den Menüpunkt **Zugehörig** und dann **Fremdarbeitenpreise**. Erfassen Sie eine Zeile mit **Arbeitsplatzgruppennr.**, **Artikel**, **Einheit** und **Preis**. Wählen Sie zusätzlich die **Berechnungseinheit** aus; der **Berechnungspreis** wird daraufhin automatisch berechnet (siehe Kapitel *Stammdaten*).
3. **Freigegebenen Fertigungsauftrag öffnen.** Öffnen Sie den **freigegebenen Fertigungsauftrag** für den eingerichteten Artikel und rufen Sie über **Zeile** die Aktion **Arbeitsplan** auf. Damit öffnen Sie den **FA-Arbeitsplan**.
4. **Arbeitsplatzgruppe einsetzen.** Setzen Sie in der Arbeitsgangzeile die für Fremdarbeit gekennzeichnete Arbeitsplatzgruppe ein. Das System zieht automatisch den passenden Fremdarbeitspreis und füllt in der Zeile die Felder **Berechnungseinheit** und **Preis pro Berechnungseinheit**; die Direktkosten je Einheit werden aus dem gefundenen Preis abgeleitet.
5. **Fremdarbeit zur Bestellung führen.** Rufen Sie über die Suche die **Fremdarbeitsarbeitsblätter** auf. Lassen Sie zunächst den Fremdarbeitsbedarf berechnen und führen Sie anschließend die im Arbeitsblatt vorgeschlagene Aktionsmeldung aus. Es entsteht eine **Einkaufsbestellung**, in der **Berechnungseinheit** und **Preis pro Berechnungseinheit** aus der Bedarfszeile übernommen sind.

Weiterführende Schritte, alle Felder und die Umrechnungslogik finden Sie in den folgenden Kapiteln.

## Einrichtung

Diese App bringt **keine eigene Einrichtungsseite** mit. Sie erweitert vorhandene Seiten der Grund-Apps um zwei Felder und leitet den Preis über Ereignisse automatisch ab. Die Voraussetzungen für den automatischen Fremdarbeitspreis werden daher in den Grund-Apps eingerichtet. Damit die Berechnung je Berechnungseinheit greift, sind die nachfolgend beschriebenen Schritte in Abhängigkeitsreihenfolge zu durchlaufen.

### Berechnungseinheit für Fremdarbeitenpreise einrichten

**Prozessvorstellung.** Diese Einrichtung nimmt der **Administrator** bzw. ein Stammdatenverantwortlicher **vor der ersten Nutzung** vor. Sie aktiviert die zentrale Fähigkeit dieser App: die Führung und automatische Umrechnung eines Fremdarbeitspreises je Berechnungseinheit. Die eingerichteten Werte werden später im Kapitel *Tägliche Arbeit am FA-Arbeitsplan* durch die operativen Anwender verwendet. Die Schritte bauen aufeinander auf – zuerst die Arbeitsplatzgruppe, dann der Fremdarbeitenpreis, zuletzt die Wirkung im Beleg.

**Nummerierte Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Arbeitsplatzgruppe für Fremdarbeit kennzeichnen.** Öffnen Sie die **Arbeitsplatzgruppenkarte**, tragen Sie den zugehörigen **Kreditor** ein und kennzeichnen Sie die Arbeitsplatzgruppe für Fremdarbeit (spezifischer Einstandspreis am Arbeitsplatz). Wenn die Arbeitsplatzgruppe so gekennzeichnet ist, dann verwendet das System bei der Preisermittlung für diese Arbeitsplatzgruppe nicht den Standard-Einkaufspreis, sondern ausschließlich die in den Fremdarbeitenpreisen hinterlegten Preise – ohne diese Kennzeichnung bleibt der Fremdarbeitspreis unberücksichtigt und die Berechnungseinheit dieser App greift nicht.
2. **Berechnungseinheit in der Einkaufskalkulation vorbereiten.** Die auswählbaren Berechnungseinheiten stammen aus der **Einkaufspreisberechnung** der App m+m „Preisfindung“ (Tabelle der Einkaufspreisberechnung je Kreditor und Artikel). Wenn für die Kombination aus Kreditor und Artikel dort eine **Einkaufsberechnungseinheit** eingerichtet ist, dann steht diese in den Fremdarbeitenpreisen zur Auswahl; ohne diesen Eintrag ist im Feld **Berechnungseinheit** keine gültige Auswahl möglich.
3. **Fremdarbeitenpreis mit Berechnungseinheit und Berechnungspreis erfassen.** Öffnen Sie über die **Kreditorenkarte → Zugehörig → Fremdarbeitenpreise** die Fremdarbeitenpreise und erfassen Sie eine Preiszeile (siehe Feldtabelle im Kapitel *Stammdaten*). Wenn Sie eine **Berechnungseinheit** wählen und ein **Preis** gesetzt ist, dann berechnet das System den **Berechnungspreis** automatisch; wenn Sie umgekehrt den **Berechnungspreis** ändern, dann wird der **Preis** je Grundeinheit automatisch angepasst.

**Operativer Abschluss.** Die Einrichtung wird im Tagesgeschäft dadurch wirksam, dass der Anwender im **FA-Arbeitsplan** des freigegebenen Fertigungsauftrags die entsprechende Arbeitsplatzgruppe einsetzt (siehe Kapitel *Tägliche Arbeit am FA-Arbeitsplan*). Ab diesem Zeitpunkt zieht das System automatisch den passenden Fremdarbeitspreis samt Berechnungseinheit und errechnet die Direktkosten je Einheit.

## Stammdaten

Die Fremdarbeitenpreise sind die zentralen Stammdaten dieser App. Sie werden durch die Grund-App m+m „Fremdarbeitenpreise“ bereitgestellt; diese Verbindungs-App ergänzt sie um die Felder **Berechnungseinheit** und **Berechnungspreis** sowie um die automatische Umrechnung zwischen **Preis** und **Berechnungspreis**.

### Fremdarbeitenpreise

**Prozessvorstellung.** Die Fremdarbeitenpreise pflegt der **Stammdatenverantwortliche** je Kreditor. Sie legen fest, welcher Preis für die Kombination aus Arbeitsplatzgruppe, Standardkatalogcode, Artikel und Menge gilt. Der einfachste Zugang führt über die **Kreditorenkarte → Zugehörig → Fremdarbeitenpreise**. Die hier gepflegten Werte steuern die spätere automatische Preisermittlung im FA-Arbeitsplan und im Fremdarbeitsarbeitsblatt (siehe Kapitel *Tägliche Arbeit* und *Automatische Preisableitung*).

**Feldtabelle (Basisfelder der Grund-App und Zusatzfelder dieser App auf derselben Seite):**

| Feld | Erläuterung |
|---|---|
| Einkaufsart | Wenn „Alle Kreditoren“ gewählt ist, dann gilt die Preiszeile für sämtliche Kreditoren; wenn „Kreditor“ gewählt ist, dann gilt sie nur für den in der Zeile angegebenen Kreditor. Diese Auswahl steuert unmittelbar, welche Preiszeilen das System bei der automatischen Ermittlung im FA-Arbeitsplan berücksichtigt. |
| Kreditornr. | Wenn ein Kreditor eingetragen ist, dann bindet die Preiszeile an genau diesen Lohnfertiger; das System zieht sie nur, wenn die Arbeitsplatzgruppe demselben Kreditor zugeordnet ist. |
| Kreditorenname | Wird nach Auswahl der Kreditornr. automatisch gefüllt und dient der eindeutigen Zuordnung in der Liste; eine manuelle Pflege ist nicht erforderlich. |
| Arbeitsplatzgruppennr. | Bindet die Preiszeile an eine Arbeitsplatzgruppe. Wenn im FA-Arbeitsplan diese Arbeitsplatzgruppe eingesetzt wird, dann wird genau diese Preiszeile für die Preisermittlung herangezogen. |
| Referenz-Art | Wenn „Alle Standardkatalogcodes“ gewählt ist, dann gilt die Zeile für jeden Arbeitsgang; wenn „Standardkatalogcode“ gewählt ist, dann gilt sie nur für den in der Zeile angegebenen Code. Damit steuern Sie, ob der Preis pauschal oder je konkretem Arbeitsgang greift. |
| Standardkatalogcode | Wenn ein Standardkatalogcode eingetragen ist, dann wird die Zeile nur für Arbeitsgänge mit genau diesem Code gezogen; so lassen sich unterschiedliche Fremdarbeitsgänge unterschiedlich bepreisen. |
| Definitionsart | Wenn „Alle Artikel“ gewählt ist, dann gilt der Preis artikelunabhängig; wenn „Artikel“ gewählt ist, dann nur für den in der Zeile angegebenen Artikel. Damit trennen Sie allgemeine von artikelspezifischen Fremdarbeitspreisen. |
| Artikel | Wenn ein Artikel eingetragen ist, dann gilt die Preiszeile nur für Fertigungsaufträge dieses Artikels; leer bedeutet in Verbindung mit „Alle Artikel“, dass der Preis für jeden Artikel greift. |
| Einheit | Legt die Grundeinheit fest, auf die sich das Feld **Preis** bezieht. Diese Einheit ist der Bezugspunkt für die spätere Umrechnung in die Berechnungseinheit. |
| Mindestpreis | Wenn der aus Preis × Menge errechnete Betrag den Mindestpreis unterschreitet, dann wird pauschal der Mindestpreis angesetzt. So stellen Sie sicher, dass Kleinmengen nie unter einem vereinbarten Sockelbetrag abgerechnet werden. Je Arbeitsplatzgruppe und Standardkatalogcode ist der Mindestpreis nur einmal vergebbar. |
| Mindestmenge | Legt die Mindestmenge fest, ab der der Preis dieser Zeile gilt. Wenn Sie je Arbeitsplatzgruppe und Standardkatalogcode mehrere Zeilen mit unterschiedlicher Mindestmenge anlegen, dann bilden diese eine Preisstaffel, aus der das System den passenden Preis zur Fertigungsmenge wählt. |
| Preis | Legt den Preis je **Einheit** für die Kombination aus Arbeitsplatzgruppe, Standardkatalogcode und Menge fest. Wenn Sie den Preis ändern und eine Berechnungseinheit gesetzt ist, dann berechnet das System den **Berechnungspreis** automatisch neu. |
| Gültig ab | Wenn ein Datum gesetzt ist, dann gilt die Preiszeile erst ab diesem Datum; das System berücksichtigt bei der Ermittlung nur Zeilen, deren Gültigkeit das Arbeitsdatum einschließt. |
| Gültig bis | Wenn ein Datum gesetzt ist, dann verliert die Preiszeile danach ihre Gültigkeit; abgelaufene Zeilen werden bei der automatischen Ermittlung nicht mehr gezogen. |
| Berechnungseinheit | Legt fest, welche Artikelmaßeinheit für die Berechnung des Preises herangezogen wird. Wenn Sie eine Berechnungseinheit auswählen, dann errechnet das System aus dem **Preis** und den Mengenverhältnissen der Einheiten automatisch den **Berechnungspreis** und führt beide Werte in die Belege der Fremdbearbeitung mit. Die Auswahl erfolgt aus der Einkaufspreisberechnung der App m+m „Preisfindung“ für den Kreditor und Artikel. |
| Berechnungspreis | Zeigt den Preis je **Berechnungseinheit**. Wenn Sie diesen Wert manuell ändern, dann rechnet das System den **Preis** je Grundeinheit automatisch zurück, sodass beide Preisangaben stets konsistent bleiben. |

**Umrechnungslogik (Validierungshinweis).** Die Umrechnung zwischen **Preis** und **Berechnungspreis** erfolgt über das Verhältnis „Menge pro Einheit“ der beiden beteiligten Artikelmaßeinheiten (Einheit und Berechnungseinheit). Ist für eine der beiden Einheiten keine Artikelmaßeinheit hinterlegt, dann unterbleibt die Umrechnung und der Berechnungspreis bleibt bei 0. Voraussetzung ist außerdem, dass für die Kombination aus Kreditor und Artikel in der Einkaufspreisberechnung eine Berechnungseinheit eingerichtet ist.

### Infobox Fremdarbeitenpreise

**Prozessvorstellung.** Zur schnellen Sichtprüfung stellt die Grund-App im FA-Arbeitsplan eine Infobox mit den hinterlegten Fremdarbeitspreisen bereit. Diese Verbindungs-App ergänzt die Infobox um die **Berechnungseinheit**, damit der Anwender bereits in der Arbeitsgangzeile erkennt, auf welche Berechnungseinheit sich der angezeigte Preis bezieht.

| Feld | Erläuterung |
|---|---|
| Berechnungseinheit | Zeigt in der Infobox die Artikelmaßeinheit, auf die sich der Berechnungspreis der angezeigten Fremdarbeitspreiszeile bezieht. Wenn der Anwender die Infobox liest, dann erkennt er ohne Wechsel in die Fremdarbeitenpreise, in welcher Berechnungseinheit der Preis kalkuliert wurde. |

## Tägliche Arbeit am FA-Arbeitsplan

Die tägliche Arbeit setzt auf den in *Einrichtung* und *Stammdaten* gepflegten Werten auf: Sobald die Arbeitsplatzgruppe für Fremdarbeit gekennzeichnet ist und ein Fremdarbeitenpreis mit Berechnungseinheit vorliegt, füllt das System die Zusatzfelder automatisch. Der Anwender pflegt hier keine Preise, sondern setzt die vorbereitete Arbeitsplatzgruppe ein und prüft das Ergebnis.

### FA-Arbeitsplan (Arbeitsgangzeilen)

**Einstieg:** Öffnen Sie den **freigegebenen Fertigungsauftrag** und rufen Sie über **Zeile → Arbeitsplan** den **FA-Arbeitsplan** auf.

Wenn der Anwender in der Arbeitsgangzeile die für Fremdarbeit gekennzeichnete Arbeitsplatzgruppe einsetzt, dann ermittelt das System automatisch den passenden Fremdarbeitspreis und füllt die folgenden Felder:

| Feld | Erläuterung |
|---|---|
| Berechnungseinheit | Zeigt die aus dem gefundenen Fremdarbeitspreis übernommene Berechnungseinheit. Wenn das System einen passenden Preis findet, dann trägt es hier die kalkulatorische Einheit ein, sodass die Herkunft des Preises je Berechnungseinheit nachvollziehbar bleibt. |
| Preis pro Berechnungseinheit | Zeigt den je Berechnungseinheit kalkulierten Preis aus dem gefundenen Fremdarbeitspreis. Aus diesem Wert und der Fertigungsmenge leitet das System die Direktkosten je Einheit der Arbeitsgangzeile ab; dieser Betrag fließt in die Kalkulation des Fertigungsauftrags ein. |

**Hinweis zur automatischen Ermittlung.** Das System berücksichtigt nur Arbeitsgänge vom Typ Arbeitsplatzgruppe, deren Arbeitsplatzgruppe für Fremdarbeit gekennzeichnet ist (spezifischer Einstandspreis am Arbeitsplatz). Aus allen gültigen Preiszeilen (Gültigkeitszeitraum schließt das Arbeitsdatum ein, Mindestmenge kleiner oder gleich Fertigungsmenge) wählt das System die günstigste und berücksichtigt dabei den **Mindestpreis** als Untergrenze. Details siehe Kapitel *Automatische Preisableitung*.

### Fremdarbeitsarbeitsblätter

**Einstieg:** Rufen Sie über die Suche die **Fremdarbeitsarbeitsblätter** auf.

Die Fremdarbeitsarbeitsblätter überführen den Fremdarbeitsbedarf eines Fertigungsauftrags in eine Einkaufsbestellung. Diese Verbindungs-App ergänzt die Zeilen um dieselben Berechnungsfelder wie den FA-Arbeitsplan, damit die Berechnungseinheit durchgängig bis in die Bestellung erhalten bleibt.

| Feld | Erläuterung |
|---|---|
| Berechnungseinheit | Zeigt die aus dem Fremdarbeitspreis abgeleitete Berechnungseinheit für die Bedarfszeile. Wenn aus dieser Zeile später eine Einkaufsbestellung erzeugt wird, dann wird die Berechnungseinheit unverändert in die Bestellzeile übernommen. |
| Preis pro Berechnungseinheit | Zeigt den je Berechnungseinheit kalkulierten Preis der Bedarfszeile. Aus ihm werden die Direktkosten je Einheit der späteren Bestellzeile abgeleitet, sodass die Kalkulation von der Planung bis zur Bestellung konsistent bleibt. |

**Prozessschritte bis zur Einkaufsbestellung:**

1. Rufen Sie die **Fremdarbeitsarbeitsblätter** über die Suche auf.
2. Lassen Sie den zu verarbeitenden Fremdarbeitsbedarf berechnen; das System füllt die Bedarfszeilen und ermittelt dabei über die Fremdarbeitenpreise **Berechnungseinheit** und **Preis pro Berechnungseinheit**.
3. Setzen Sie bei Bedarf einen Filter auf den zu bearbeitenden Datensatz und führen Sie die vorgeschlagene Aktionsmeldung aus. Es wird eine **Einkaufsbestellung** erstellt; der Datensatz verschwindet danach aus dem Arbeitsblatt.
4. In der neuen **Einkaufsbestellung** sind **Berechnungseinheit** und **Preis pro Berechnungseinheit** aus der Bedarfszeile übernommen; die Direktkosten je Einheit ergeben sich aus dem gefundenen Fremdarbeitspreis geteilt durch die Menge.

## Automatische Preisableitung

Dieses Kapitel beschreibt die Kernlogik der App, damit Anwender das automatische Verhalten nachvollziehen und Abweichungen einordnen können. Der Anwender löst diese Logik nicht über eine eigene Schaltfläche aus; sie greift automatisch, sobald ein Fremdarbeitspreis benötigt wird.

**Preisermittlung (Fremdarbeitspreis finden).** Für einen Arbeitsgang vom Typ Arbeitsplatzgruppe prüft das System zunächst, ob die Arbeitsplatzgruppe für Fremdarbeit gekennzeichnet ist (spezifischer Einstandspreis am Arbeitsplatz). Anschließend werden aus den Fremdarbeitenpreisen alle Zeilen gesammelt, die auf die Arbeitsplatzgruppe passen, deren Gültigkeitszeitraum das Arbeitsdatum einschließt und deren **Mindestmenge** die Fertigungsmenge nicht übersteigt. Dabei werden die Kombinationen aus **Einkaufsart** (Alle Kreditoren / Kreditor) und **Referenz-Art** (Alle Standardkatalogcodes / Standardkatalogcode) berücksichtigt, sodass sowohl allgemeine als auch spezifische Preiszeilen einbezogen werden. Aus den passenden Zeilen wählt das System die günstigste; unterschreitet der aus Preis × Menge errechnete Betrag den **Mindestpreis**, dann wird der Mindestpreis angesetzt.

**Wirkung in den Belegen.** Der gefundene Preis wird an drei Stellen wirksam:

- Im **FA-Arbeitsplan** setzt das System **Berechnungseinheit**, **Preis pro Berechnungseinheit** und die Direktkosten je Einheit (gefundener Preis geteilt durch die Fertigungsmenge) in die Arbeitsgangzeile.
- In der aus dem Fremdarbeitsarbeitsblatt entstehenden **Einkaufsbestellung** werden Berechnungseinheit und Preis pro Berechnungseinheit übernommen und die Direktkosten je Einheit aus dem gefundenen Preis geteilt durch die Bestellmenge abgeleitet.
- In der **Bedarfszeile** des Fremdarbeitsarbeitsblatts werden dieselben Werte gesetzt, sodass sie beim Erzeugen der Bestellung unverändert weitergereicht werden.

**Reziproke Umrechnung Preis ⇄ Berechnungspreis.** In den Fremdarbeitenpreisen sind **Preis** (je Grundeinheit) und **Berechnungspreis** (je Berechnungseinheit) über das Mengenverhältnis der Artikelmaßeinheiten miteinander verknüpft. Wenn der Anwender den **Preis** oder die **Berechnungseinheit** ändert, dann wird der Berechnungspreis neu berechnet; ändert er den **Berechnungspreis**, dann wird der Preis je Grundeinheit zurückgerechnet. So bleiben beide Preisangaben jederzeit widerspruchsfrei.

## FAQ und Troubleshooting

### 1. Warum bleibt der Berechnungspreis in den Fremdarbeitenpreisen bei 0?

Weil für die **Einheit** oder die **Berechnungseinheit** keine Artikelmaßeinheit hinterlegt ist. Die Umrechnung nutzt das Verhältnis „Menge pro Einheit“ beider Einheiten; fehlt eine davon, bricht die Berechnung ab und der Berechnungspreis bleibt 0. Pflegen Sie beide Artikelmaßeinheiten am Artikel.

### 2. Warum kann ich im Feld Berechnungseinheit keine Einheit auswählen?

Weil für die Kombination aus **Kreditor** und **Artikel** in der Einkaufspreisberechnung der App m+m „Preisfindung“ keine Berechnungseinheit eingerichtet ist. Die Auswahlliste bezieht ihre Werte aus dieser Einkaufspreisberechnung; ohne passenden Eintrag ist keine Auswahl möglich.

### 3. Warum wird im FA-Arbeitsplan kein Fremdarbeitspreis gezogen?

Weil die betreffende **Arbeitsplatzgruppe** nicht für Fremdarbeit gekennzeichnet ist (spezifischer Einstandspreis am Arbeitsplatz nicht gesetzt). Ohne diese Kennzeichnung verwendet das System den Standard-Einkaufspreis und ignoriert die Fremdarbeitenpreise. Kennzeichnen Sie die Arbeitsplatzgruppe entsprechend auf der Arbeitsplatzgruppenkarte.

### 4. Was passiert, wenn die Fertigungsmenge kleiner als jede Mindestmenge ist?

Dann findet das System keine passende Preisstaffel und ermittelt keinen Fremdarbeitspreis für diese Zeile. Legen Sie eine Preiszeile mit einer **Mindestmenge** an, die kleiner oder gleich der geplanten Fertigungsmenge ist.

### 5. Warum wird ein höherer Betrag als Preis × Menge angesetzt?

Weil der errechnete Betrag den hinterlegten **Mindestpreis** unterschreitet. In diesem Fall setzt das System pauschal den Mindestpreis an, damit Kleinmengen nicht unter dem vereinbarten Sockelbetrag abgerechnet werden.

### 6. Nach welchem Kriterium wählt das System aus mehreren gültigen Preiszeilen?

Das System sammelt alle passenden Zeilen (Einkaufsart, Referenz-Art, Gültigkeit, Mindestmenge) und wählt daraus die **günstigste**. Der Mindestpreis wird anschließend als Untergrenze berücksichtigt.

### 7. Warum ändert sich beim Ändern des Berechnungspreises auch der Preis?

Weil **Preis** und **Berechnungspreis** über das Mengenverhältnis der Einheiten fest gekoppelt sind. Eine Änderung des Berechnungspreises rechnet den Preis je Grundeinheit automatisch zurück, damit beide Werte konsistent bleiben. Das ist beabsichtigt.

### 8. Werden Berechnungseinheit und Preis pro Berechnungseinheit in die Einkaufsbestellung übernommen?

Ja. Beim Erzeugen der Bestellung aus dem Fremdarbeitsarbeitsblatt überträgt das System **Berechnungseinheit** und **Preis pro Berechnungseinheit** aus der Bedarfszeile unverändert in die Bestellzeile; die Direktkosten je Einheit werden aus dem gefundenen Preis geteilt durch die Bestellmenge abgeleitet.

### 9. Warum steht in der Infobox eine andere Berechnungseinheit als erwartet?

Weil die Infobox die Berechnungseinheit der tatsächlich gezogenen Fremdarbeitspreiszeile anzeigt. Wenn mehrere Preisstaffeln existieren, kann eine andere als die vermutete Zeile die günstigste sein. Prüfen Sie die Preiszeilen in den Fremdarbeitenpreisen für die betreffende Arbeitsplatzgruppe.

### 10. Muss ich die Preise in der täglichen Arbeit manuell eintragen?

Nein. In der täglichen Arbeit setzen Sie lediglich die vorbereitete Arbeitsplatzgruppe ein; **Berechnungseinheit**, **Preis pro Berechnungseinheit** und die Direktkosten je Einheit füllt das System automatisch. Die Pflege der Preise erfolgt einmalig in den Fremdarbeitenpreisen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Neuen Fremdarbeitspreis je Berechnungseinheit hinterlegen und im Fertigungsauftrag einsetzen

**Auslöser.** Ein Lohnfertiger meldet telefonisch einen neuen Rahmenpreis für eine Fremdbearbeitung, den er je 100 Stück kalkuliert, während der Artikel im System in Stück geführt wird.

**Einstieg in BC.** Der Stammdatenverantwortliche öffnet die **Kreditorenkarte** des Lohnfertigers und ruft über **Zugehörig → Fremdarbeitenpreise** die Fremdarbeitenpreise auf.

**Kernablauf.** Er erfasst eine Preiszeile mit **Arbeitsplatzgruppennr.**, **Artikel**, **Einheit** (Stück) und **Preis**. Als **Berechnungseinheit** wählt er die 100-Stück-Einheit; das System errechnet daraufhin automatisch den **Berechnungspreis**. Bei Bedarf legt er weitere Zeilen mit unterschiedlicher **Mindestmenge** an, um eine Preisstaffel abzubilden, und hinterlegt einen **Mindestpreis** als Sockelbetrag. Voraussetzung ist, dass die Arbeitsplatzgruppe auf der **Arbeitsplatzgruppenkarte** dem Kreditor zugeordnet und für Fremdarbeit gekennzeichnet ist (spezifischer Einstandspreis am Arbeitsplatz; siehe Kapitel *Einrichtung*).

**Abschluss.** Anschließend öffnet die Fertigungsplanung den **freigegebenen Fertigungsauftrag**, ruft über **Zeile → Arbeitsplan** den **FA-Arbeitsplan** auf und setzt die Arbeitsplatzgruppe ein. Das System füllt **Berechnungseinheit** und **Preis pro Berechnungseinheit** und leitet die Direktkosten je Einheit ab. In der Infobox lässt sich der herangezogene Fremdarbeitspreis kontrollieren.

### Anwendungsfall 2: Fremdarbeit über das Arbeitsblatt zur Einkaufsbestellung führen

**Auslöser.** Für einen freigegebenen Fertigungsauftrag ist ein Fremdbearbeitungsschritt fällig, für den eine Einkaufsbestellung beim Lohnfertiger erzeugt werden soll.

**Einstieg in BC.** Der Einkauf ruft über die Suche die **Fremdarbeitsarbeitsblätter** auf.

**Kernablauf.** Über die Berechnung des Fremdarbeitsbedarfs zeigt das System die zu verarbeitende Fremdarbeit an. In den Bedarfszeilen sind **Berechnungseinheit** und **Preis pro Berechnungseinheit** aus dem zuvor gefundenen Fremdarbeitspreis bereits gefüllt. Der Anwender setzt bei Bedarf einen Filter auf den gewünschten Datensatz.

**Abschluss.** Mit dem Ausführen der vorgeschlagenen Aktionsmeldung erzeugt das System die **Einkaufsbestellung**; der verarbeitete Datensatz verschwindet aus dem Arbeitsblatt. In der Bestellung sind **Berechnungseinheit** und **Preis pro Berechnungseinheit** aus der Bedarfszeile übernommen, und die Direktkosten je Einheit ergeben sich aus dem gefundenen Preis geteilt durch die Bestellmenge. Damit ist die Fremdbearbeitung mit dem korrekt umgerechneten Preis bestellt.
