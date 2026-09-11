---
title: Anwenderhandbuch m+m Supplier Declaration
---

# Anwenderhandbuch m+m Supplier Declaration

## Einleitung

Das Modul **m+m Supplier Declaration** verwaltet **Lieferantendeklarationen** (Lieferantenerklärungen zur Präferenzursprungseigenschaft) in Microsoft Dynamics 365 Business Central. Es deckt sowohl **einstufige** als auch **langfristige Lieferantendeklarationen** ab, jeweils getrennt nach **Einkauf** und **Verkauf**, und verknüpft sie mit Chargen, Ländern und Belegen.

**Zielgruppe.** Primäre Anwender sind **operative Sachbearbeiter im Ein- und Verkauf** sowie in der Zoll-/Präferenzabwicklung: Sie legen Deklarationen an, bestätigen Länder, geben Deklarationen frei und arbeiten beim Buchen von Verkaufslieferungen und Einkaufslieferungen mit den daraus entstehenden Statusinformationen. **Administratoren und Key-User** richten das Modul ein (Einrichtung, Nummernserien, Berichte, Stammdaten) — sie sind die sekundäre Zielgruppe.

**Kurzer Prozessüberblick.** Der typische Weg durch das Modul:

1. Der Administrator aktiviert die **Lieferantendeklarationsfunktionen** und hinterlegt Nummernserien, Berichte sowie die Steuerung beim Buchen (Einrichtung).
2. Im Stammdatenteil wird festgelegt, **für welche Debitoren/Kreditoren und welche Materialarten/Artikel** eine Lieferantendeklaration erforderlich ist, und welche **Länder/Regionen** sowie **Länder-/Regionsgruppen** für die Deklaration relevant sind.
3. Der Anwender legt eine Deklaration über eine der vier Listen an, pflegt **Land/Region** und **Länder-/Regionsgruppe**, prüft die Gültigkeit (**Länder prüfen**) und gibt die Deklaration frei (**Freigeben**).
4. Beim Buchen von Verkaufslieferungen bzw. Einkaufslieferungen verknüpft das Modul automatisch Chargen und Belege mit den passenden Deklarationen und kann einstufige Deklarationen erzeugen und freigeben.
5. Über die **Chargennr.-Informationskarte**, die **Materialbestände** und die Chargenverfolgung lässt sich jederzeit nachvollziehen, ob für eine Charge eine Lieferantendeklaration vorhanden ist.

Der typische Einstieg ist: **Suchen** -> eine der vier Deklarationslisten -> Zeile auswählen -> Karte öffnen -> Aktionen ausführen.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zur freigegebenen Deklaration. Die Reihenfolge folgt der Abhängigkeit im Code (zuerst Einrichtung, dann Stammdaten, dann Tagesgeschäft).

1. **Einrichtung prüfen.** Öffnen Sie über **Suchen** die Seite **Lieferantendeklaration Einrichtung** und aktivieren Sie **Lieferantendeklarationsfunktionen aktiv**. Ohne dieses Kennzeichen sind alle Modulfunktionen inaktiv (siehe Einrichtung).
2. **Nummernserien und Berichte** auf derselben Seite hinterlegen (je Bereich und Typ eine Nummernserie; je Bereich und Typ eine Berichts-ID).
3. **Stammdaten festlegen.** Markieren Sie auf der Seite **Länder/Regionen** die für die Deklaration relevanten Länder über **Für Lieferantendeklaration**. Hinterlegen Sie bei Bedarf **Länder-/Regionsgruppen** und deren **Zuweisungen**. Setzen Sie auf der **Debitorenkarte** bzw. **Kreditorenkarte** das Kennzeichen **Lieferantendeklaration erforderlich** und pflegen Sie über **Lieferantendeklaration für Typen**, für welche Materialarten/Artikel eine Deklaration nötig ist.
4. **Deklaration anlegen.** Öffnen Sie über **Suchen** z. B. **Langfristige Lieferantendeklarationen - Einkauf**, legen Sie mit *Neu* eine Zeile an (Bereich und Typ werden automatisch gesetzt) und wählen Sie den Kreditor. Pflegen Sie **Gültigkeit ab/Gültig bis** und die enthaltenen Artikel/Materialarten (Register **Lieferantendeklaration enthalten**).
5. **Länder pflegen.** Bestätigen Sie in den Unterseiten **Lieferantendeklaration Land/Region** und **Lieferantendeklaration Länder-/Regionsgruppe** die zugesagten Länder über **Bestätigt**. Mit **Gültige Länder einfügen** füllen Sie die relevanten Länder automatisch ein.
6. **Gültigkeit prüfen.** Wählen Sie **Länder prüfen**. Liegen alle bestätigten Länder/Gruppen innerhalb des Gültigkeitszeitraums, wird der **Gültigkeitsstatus** auf *Geprüft* gesetzt.
7. **Freigeben.** Wählen Sie **Freigeben**. Der Status wechselt auf *Herausgegeben*; die Chargen werden in die Charge-Lieferantendeklaration übertragen. Mit **Öffnen** kehren Sie nach *Offen* zurück, mit **Abbrechen** stornieren Sie die Deklaration.

Beim Buchen von Verkaufslieferungen und Einkaufslieferungen läuft die Verknüpfung — je nach Einrichtung — automatisch (siehe **Beleg-Integration**).

## Einrichtung

Die Einrichtung ist der umfangreichste Konfigurationsteil des Moduls. Sie steuert, ob das Modul aktiv ist, mit welchen Nummernserien und Berichten gearbeitet wird und wie sich das Modul beim Buchen verhält.

### Lieferantendeklaration einrichten (zentrale Einrichtungsseite)

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Lieferantendeklaration Einrichtung**. Es handelt sich um eine unternehmensweite Einrichtungsseite (genau ein Datensatz je Mandant); sie wird beim ersten Öffnen automatisch angelegt.

**Prozess.** Der Administrator konfiguriert diese Seite **vor der ersten Nutzung** des Moduls. Sie aktiviert das Modul, legt die Nummernkreise fest, ordnet die Druck-/Versandberichte zu und bestimmt das Verhalten beim Buchen, das später im Tagesgeschäft (Beleg-Integration) wirksam wird.

**Register Allgemein**

| Einrichtung | Erläuterung |
|---|---|
| **Lieferantendeklarationsfunktionen aktiv** | Wenn aktiviert, sind sämtliche Funktionen des Moduls wirksam: Anlegen und Freigeben von Deklarationen, Prüfungen beim Buchen und das Setzen der Statusfelder in Beleg­zeilen. Ist das Kennzeichen nicht gesetzt, beenden alle Modulroutinen sofort, sodass das Tagesgeschäft im Standard ohne Lieferantendeklaration läuft. |
| **Ereignisherausgeber aktiviert** | Wenn aktiviert, reagiert das Modul zusätzlich auf das Einfügen/Ändern von Artikelposten und auf das Validieren von Verkaufs-/Einkaufszeilen: bei Umlagerung der Herkunft auf eine neue Charge (über die Zusatz-Chargeninformationen) wird die Lieferantendeklaration auf die neue Charge übertragen, und beim Erfassen einer Beleg­zeile wird **Lieferantendeklaration erforderlich** automatisch ermittelt. Ohne dieses Kennzeichen erfolgen diese automatischen Ermittlungen nicht. |

**Register Lieferantendeklaration**

| Einrichtung | Erläuterung |
|---|---|
| **Standardländer-/-regionscodes einfügen** | Wenn aktiviert, werden beim Anlegen einer Deklaration automatisch alle als **Für Lieferantendeklaration** markierten Länder als Land/Region-Zeilen vorbelegt; der Anwender muss sie dann nur noch bestätigen, statt sie einzeln einzutragen. |
| **Alle Anzahl-/Regionsgruppen einfügen** | Wenn aktiviert, werden beim Anlegen einer Deklaration zusätzlich alle vorhandenen Länder-/Regionsgruppen als Gruppenzeilen vorbelegt; ohne das Kennzeichen pflegt der Anwender die Gruppen manuell. |
| **Nicht relevante Länder-/Regionscodes löschen** | Wenn aktiviert, entfernt das Modul bei der Freigabe alle nicht bestätigten Land/Region-Zeilen aus der Deklaration; die freigegebene Deklaration enthält dann nur noch die tatsächlich zugesagten Länder. Ohne das Kennzeichen bleiben auch unbestätigte Zeilen erhalten. |

**Register Verkauf**

| Einrichtung | Erläuterung |
|---|---|
| **Lieferantendeklaration bei Verkaufslieferung erstellen** | Wenn aktiviert, erzeugt das Modul beim Buchen einer Verkaufslieferung für Zeilen, die eine Deklaration benötigen und für die noch keine existiert, automatisch eine einstufige Lieferantendeklaration inklusive Land, Beleg und Chargen. Ohne das Kennzeichen wird beim Buchen keine neue Deklaration angelegt. |
| **Lieferantendeklaration bei Verkaufslieferung freigeben** | Wenn aktiviert, wird die soeben automatisch erzeugte einstufige Deklaration unmittelbar nach dem Buchen freigegeben (Status *Herausgegeben*). Ohne das Kennzeichen bleibt sie im Status *Offen* zur manuellen Prüfung. Greift nur zusammen mit *Lieferantendeklaration bei Verkaufslieferung erstellen*. |
| **Auf fehlenden Lagerpl. decl. auf Verkaufsrechnungsbuchung prüfen** | Steuert die Buchungssperre bei der Verkaufsrechnung. **(leer):** keine Prüfung. **Warnung:** Wenn beim Buchen einer Verkaufsrechnung eine Zeile eine Deklaration benötigt, die zugehörige Lieferung aber keine besitzt, erscheint ein Hinweis, die Buchung läuft weiter. **Fehler:** In derselben Situation wird die Buchung mit einer Fehlermeldung abgebrochen, bis eine Deklaration vorliegt. |
| **Dekl. Drucken/Senden Mit** | Steuert die Prüfung beim Drucken/Versenden einer Verkaufs-Lieferantendeklaration. **(leer):** keine Prüfung. **Warnung:** fehlende Voraussetzungen werden als Hinweis gemeldet. **Fehler:** der Vorgang wird bei fehlenden Voraussetzungen abgebrochen. |

> Hinweis: Das Register **Einkauf** enthält in dieser Version keine eigenen Felder; die einkaufsseitige Steuerung erfolgt über die Nummernserien-, Berichts- und Allgemein-Einstellungen.

**Register Nummernserie**

| Einrichtung | Erläuterung |
|---|---|
| **Einkauf Lieferantendeklarationsnummern** | Wenn gesetzt, vergibt das Modul beim Anlegen einer **einstufigen** Einkaufs-Deklaration die Nummer aus dieser Serie. Ist die Serie auf manuelle Nummern eingestellt, kann der Anwender die Nummer auch selbst eingeben; andernfalls erhält jede neue Deklaration automatisch die nächste freie Nummer. |
| **Einkauf Langfristige Lieferantendeklarationsnummern** | Wenn gesetzt, liefert diese Serie die Nummern für **langfristige** Einkaufs-Deklarationen. |
| **Lieferantendeklarationsnummern** | Wenn gesetzt, liefert diese Serie die Nummern für **einstufige Verkaufs**-Deklarationen. |
| **Langfristige Lieferantendeklarationsnummern** | Wenn gesetzt, liefert diese Serie die Nummern für **langfristige Verkaufs**-Deklarationen. |

Ohne die jeweils passende Nummernserie wird das Anlegen einer Deklaration mit einer Testfeldmeldung abgebrochen — das Hinterlegen aller vier Serien ist daher Voraussetzung für das Tagesgeschäft.

**Register Berichte**

| Einrichtung | Erläuterung |
|---|---|
| **Berichts-ID der Lieferantendeklaration** (Einkauf) | Wenn gesetzt, verwendet die Druck-/Versandaktion für einstufige Einkaufs-Deklarationen diesen Bericht. Ohne Eintrag steht kein Ausdruck zur Verfügung. |
| **Einkauf Berichts-ID der langfristigen Lieferantendeklaration** | Wenn gesetzt, wird dieser Bericht für langfristige Einkaufs-Deklarationen gedruckt/versendet. |
| **Berichts-ID der Lieferantendeklaration** (Verkauf) | Wenn gesetzt, wird dieser Bericht für einstufige Verkaufs-Deklarationen verwendet (Aktion **Drucken** auf der Deklaration). |
| **Berichts-ID der langfristigen Lieferantendeklaration** (Verkauf) | Wenn gesetzt, wird dieser Bericht für langfristige Verkaufs-Deklarationen verwendet. |

Die Berichts-IDs verweisen auf Berichtsobjekte; das Hinterlegen ordnet dem jeweiligen Bereich/Typ das passende Druckformular zu. Die eigentlichen Berichtslayouts werden außerhalb dieses Moduls bereitgestellt.

> Ein weiteres Steuerfeld der Einrichtungstabelle, **Fehlende Vorauszahlungsrabatte - Ausl. in Mat.-Auswahl** (Optionswerte **(leer)**, **Warnung**, **Fehler**), steuert die Meldung bei fehlender Materialvoraussetzung in der Materialauswahl: **(leer)** = keine Prüfung, **Warnung** = Hinweis, **Fehler** = Abbruch. Es wird auf der Standard-Einrichtungsseite nicht angezeigt und ist nur für Spezialfälle der Materialauswahl relevant.

### Berechtigungen einrichten

Der Berechtigungssatz **MuM SDMuM All** fasst die Tabellen- und Objektrechte des Moduls zusammen. Weisen Sie ihn den Benutzern zu, die mit Lieferantendeklarationen arbeiten dürfen. Der Berechtigungssatz bestimmt die Berechtigungen für sämtliche Modultabellen und -seiten und legt fest, welche Aktionen die Anwender im Modul ausführen können; ohne Zuweisung sind die Modulseiten für den Benutzer nicht bedienbar.

### Lieferantendeklaration beim Buchen einrichten (Prozesskette)

Diese Einrichtungskette verbindet globale Einrichtung, Stammdaten und die operative Aktion beim Buchen. Sie wird vom Administrator vor der ersten Lieferung konfiguriert und im Tagesgeschäft beim Buchen wirksam (Querverweis: **Beleg-Integration**).

1. **Zuerst** auf der Seite **Lieferantendeklaration Einrichtung** das Kennzeichen **Lieferantendeklarationsfunktionen aktiv** setzen. Wenn aktiviert, sind die Buchungsprüfungen überhaupt erst wirksam.
2. **Danach** **Ereignisherausgeber aktiviert** setzen, damit beim Erfassen von Beleg­zeilen das Feld **Lieferantendeklaration erforderlich** automatisch ermittelt wird.
3. **Anschließend** in den Stammdaten festlegen, für welche Debitoren/Kreditoren (**Lieferantendeklaration erforderlich**) und welche Materialarten/Artikel (**Lieferantendeklaration für Typen**) eine Deklaration nötig ist (siehe Stammdaten).
4. **Danach** das Verkaufsverhalten wählen: **Lieferantendeklaration bei Verkaufslieferung erstellen** und optional **... freigeben**; zusätzlich **Auf fehlenden Lagerpl. decl. auf Verkaufsrechnungsbuchung prüfen** auf **Warnung** oder **Fehler** stellen.
5. **Im Tagesablauf** bucht der Anwender Verkaufslieferung/Einkaufslieferung; das Modul verknüpft Belege und Chargen, erzeugt bzw. gibt einstufige Deklarationen frei und prüft die Verkaufsrechnung gemäß der gewählten Stufe.

## Stammdaten

Die Stammdaten legen fest, **wann** eine Lieferantendeklaration verlangt wird und **welche Länder** als Ursprung in Frage kommen.

### Länder/Regionen für die Lieferantendeklaration kennzeichnen

**Einstieg:** Öffnen Sie über **Suchen** die Standardseite **Länder/Regionen**. Das Modul ergänzt die Liste um vier Felder.

**Prozess.** Der Key-User markiert vor der ersten Deklaration, welche Länder als Ursprung relevant sind. Diese Markierung steuert, welche Länder beim Anlegen einer Deklaration über **Standardländer-/-regionscodes einfügen** automatisch vorbelegt werden (Querverweis: Einrichtung) und in der Deklaration als Land/Region-Zeile bestätigt werden können.

| Feld | Erläuterung |
|---|---|
| **Für Lieferantendeklaration** | Wenn aktiviert, gilt dieses Land/diese Region als deklarationsrelevant: Es wird in neue Deklarationen als Land/Region-Zeile übernommen und kann dort bestätigt werden. Ohne das Kennzeichen erscheint das Land nicht in der automatischen Vorbelegung. |
| **Freitext** | Wenn gefüllt, steht für dieses Land ein erläuternder Text zur Verfügung, der in die Deklarationszeile übernommen werden kann. |
| **Gültigkeit ab** | Wenn gesetzt, gilt die Deklarationsrelevanz des Landes erst ab diesem Datum. |
| **Gültig bis** | Wenn gesetzt, endet die Deklarationsrelevanz des Landes mit diesem Datum. |

### Lieferantendeklaration für Typen je Debitor/Kreditor einrichten

**Einstieg (Verkauf):** Öffnen Sie in der **Debitorenkarte** die Aktion **Lieferantendeklaration für Typen**; alternativ in der **Debitorenübersicht** die Aktion **Lieferantendeklaration Materialarten**. **Einstieg (Einkauf):** Öffnen Sie in der **Kreditorenkarte** die Aktion **Lieferantendeklaration für Typen**. Die Seite ist zusätzlich über **Suchen** als Liste **Kontakt Lieferantendeklaration für Arten** erreichbar.

**Prozess.** Der Key-User hinterlegt je Debitor/Kreditor, für welche Materialart, welchen Artikel/Variante oder welche Zollposition eine Lieferantendeklaration verlangt wird. Setzen Sie zuvor auf der Debitoren-/Kreditorenkarte das Feld **Lieferantendeklaration erforderlich** (Aufruf der Detailseite über das Lookup desselben Feldes). Die Einträge werden beim Erfassen einer Beleg­zeile ausgewertet: Passt die Zeile zu einem Eintrag, wird **Lieferantendeklaration erforderlich** in der Beleg­zeile gesetzt (Querverweis: Beleg-Integration).

| Feld | Erläuterung |
|---|---|
| **Kreditorennr./Debitorennr.** | Ordnet den Eintrag dem Geschäftspartner zu, für den die Deklaration verlangt wird. |
| **Typ** | Bestimmt den Bezugspunkt der Regel. **Materialart:** Es zählt die Materialart des Artikels; das Feld **Materialart** wird bearbeitbar. **Artikel/Variante:** Es zählt der konkrete Artikel und ggf. die Variante; die Felder **Artikelnr.** und **Variantencode** werden bearbeitbar. **Zollpos.:** Es zählt die Zollposition des Artikels. |
| **Materialart** | Wenn Typ = Materialart: die Materialart, für die eine Deklaration verlangt wird. Nur bei diesem Typ bearbeitbar. |
| **Artikelnr.** | Wenn Typ = Artikel/Variante: der Artikel, für den eine Deklaration verlangt wird. Nur bei diesem Typ bearbeitbar. |
| **Variantencode** | Wenn Typ = Artikel/Variante: die Variante des Artikels. Nur bei diesem Typ bearbeitbar. |
| **Zollpos.** | Wenn Typ = Zollpos.: die Zollposition, für die eine Deklaration verlangt wird. |
| **Beschreibung** | Bezeichnung der Materialart/des Artikels zur Orientierung. |
| **Beschreibung 2** | Zusätzliche Bezeichnung zur Orientierung. |

Die zugehörigen Felder an Debitor/Kreditor:

| Feld | Erläuterung |
|---|---|
| **Lieferantendeklaration erforderlich** (Debitoren-/Kreditorenkarte) | Wenn aktiviert, wertet das Modul für diesen Geschäftspartner die Einträge unter *Lieferantendeklaration für Typen* aus. Wenn nicht gesetzt, wird für seine Beleg­zeilen keine Deklarationspflicht ermittelt. |
| **Anzahl der einzelnen Lieferantendeklarationen** / **Anzahl der langfristigen Lieferantendeklarationen** | Zeigen je Geschäftspartner, wie viele einstufige bzw. langfristige Deklarationen vorhanden sind; dienen der schnellen Übersicht in Karte und Infobox. |

### Länder-/Regionsgruppen und Zuweisungen einrichten

**Einstieg:** Die **Länder-/Regionsgruppe** und ihre **Zuweisungen** werden aus der Deklaration heraus bzw. über die zugehörigen Listen gepflegt; die Gruppe ist außerdem in den Deklarations-Unterseiten als Typ **Land/Region-Gruppe** verfügbar.

**Prozess.** Mehrere Länder, die gemeinsam zugesagt werden (z. B. eine Kumulierungszone), werden zu einer Gruppe zusammengefasst. In der Deklaration kann dann statt vieler Einzelländer die Gruppe bestätigt werden; das Modul prüft bei der Gültigkeitsprüfung, dass alle Länder der Gruppe innerhalb des Gültigkeitszeitraums liegen.

**Länder-/Regionsgruppe**

| Feld | Erläuterung |
|---|---|
| **Code** | Eindeutige Kennung der Gruppe. |
| **Namen** | Bezeichnung der Gruppe. |
| **Gültigkeit ab** / **Gültig bis** | Wenn gesetzt, gilt die Gruppe nur in diesem Zeitraum; außerhalb wird sie bei der Gültigkeitsprüfung als ungültig gemeldet. |
| **Länder/Regionen** | Zeigt die Anzahl bzw. die zugeordneten Länder der Gruppe. |

**Länder-/Regionszuweisung** (welche Länder gehören zur Gruppe)

| Feld | Erläuterung |
|---|---|
| **Länder-/Regionscode** | Ein der Gruppe zugeordnetes Land/Region. |
| **Namen** | Bezeichnung des Landes. |
| **Freitext** | Erläuternder Text zur Zuweisung. |
| **Gültigkeit ab** / **Gültig bis** | Wenn gesetzt, gilt die Zuordnung des Landes zur Gruppe nur in diesem Zeitraum. Liegt eine Zuweisung außerhalb des Deklarationszeitraums, schlägt die Gültigkeitsprüfung fehl. |

### Genehmigungen

Die Stammdatenliste **Genehmigung** verwaltet Genehmigungscodes (**Code**, **Beschreibung**), die einer Deklaration über das Feld **Genehmigungscode** zugeordnet werden können; die **Genehmigungsbeschreibung** wird dann nachgeschlagen. Sie dient der internen Kennzeichnung freigegebener bzw. genehmigter Deklarationen.

## Tägliche Arbeit: Lieferantendeklaration anlegen und freigeben

Die Deklaration ist der zentrale Beleg des Moduls. Es gibt vier Einstiegslisten, die sich nur in **Bereich** (Einkauf/Verkauf) und **Typ** (einstufig/langfristig) unterscheiden; die zugrunde liegende Karte ist identisch aufgebaut.

### Einstieg und Listen

**Einstieg:** Öffnen Sie über **Suchen** eine der vier Listen:

- **Einstufige Lieferantendeklarationen - Einkauf**
- **Langfristige Lieferantendeklarationen - Einkauf**
- **Verk. einzelner Lieferantendeklarationen** (einstufig, Verkauf)
- **Langfristige Lieferantendeklarationen - Verk.**

Jede Liste ist auf ihren Bereich und Typ vorgefiltert; beim Anlegen einer neuen Zeile werden **Bereich** und **Typ** automatisch vorbelegt. Die Liste ist nicht bearbeitbar; mit Auswahl einer Zeile öffnet sich die zugehörige Karte.

Spalten der Liste (Auszug, identisches Tabellenmodell wie die Karte): **Nr.**, **Bereich**, **Typ**, **Debitoren-/Kreditorennr.**, **Debitoren-/Kreditorenname**, **Deb./Kred. Länder-/Registrierungscode**, **Status**, **Gültigkeit ab/Gültig bis** (nur langfristig), **Kumulativ**, **Stornodatum**, **Unvollständig**, **Erstellt von/am**, **Geändert von/am**, **Kumulierte Länder/Regionen**.

### Kopfdaten der Lieferantendeklarationskarte

**Einstieg:** Wählen Sie in der Liste eine Zeile; die **Lieferantendeklarationskarte** öffnet sich. Beim Anlegen wird die Nummer aus der passenden Nummernserie vergeben.

| Feld | Erläuterung |
|---|---|
| **Nr.** | Eindeutige Nummer der Deklaration aus der Nummernserie. Umbenennen ist nicht zulässig. |
| **Bereich** | **Einkauf** oder **Verkauf**. Solange kein Debitor/Kreditor gesetzt ist, kann der Bereich gewählt werden; danach ist er fest. Steuert, ob die Deklaration gegen Kreditoren oder Debitoren läuft. |
| **Typ** | **Einstufige Lieferantendeklaration** oder **Langfristige Lieferantendeklaration**. Beim Wechsel werden bereits erfasste Länder gelöscht und der Gültigkeitsstatus auf *Scheck notwendig* zurückgesetzt, weil sich die Prüflogik unterscheidet. |
| **Debitoren-/Kreditorennr.** | Geschäftspartner der Deklaration. Bei der Eingabe prüft das Modul, ob der Partner nicht gesperrt ist und sein Land EU-Mitglied ist; andernfalls wird die Eingabe abgebrochen. Name, Adresse, PLZ, Ort und Länder-/Regionscode werden automatisch übernommen. |
| **Debitoren-/Kreditorenname**, **Name 2**, **Adresse**, **Adresse 2**, **PLZ-Code**, **Ort** | Anschrift des Geschäftspartners; aus dem Stammsatz vorbelegt, bei Bedarf überschreibbar. |
| **Deb./Kred. Länder-/Regionscode** | Land/Region des Geschäftspartners. Bei Änderung wird erneut auf EU-Mitgliedschaft geprüft; ein Nicht-EU-Land wird abgewiesen. |
| **Status** | Lebenszyklus der Deklaration (nicht direkt editierbar). **Offen:** in Bearbeitung; Änderungen erlaubt. **Herausgegeben:** freigegeben; die Chargen sind übertragen, Änderungen am Kopf sind gesperrt. **Abgebrochen:** storniert; die zugeordneten Charge-Deklarationen wurden entfernt und das Stornodatum gesetzt. |
| **Erstes Veröffentlichungsdatum** | Datum der ersten Freigabe (automatisch beim ersten **Freigeben**). |
| **Tatsächliches Freigabedatum** | Datum einer erneuten Freigabe nach Wiederöffnen. |
| **Gültigkeit ab** / **Gültig bis** | Gültigkeitszeitraum (vor allem für langfristige Deklarationen). Bei Eingabe wird geprüft, dass *ab* nicht nach *bis* liegt; jede Änderung setzt den Gültigkeitsstatus auf *Scheck notwendig* zurück. |
| **Gültigkeitsstatus** | Ergebnis der Länderprüfung (nicht editierbar). **Scheck notwendig:** Prüfung steht aus; eine Freigabe ist nicht möglich. **Geprüft:** alle bestätigten Länder/Gruppen liegen im Gültigkeitszeitraum. **Geprüft+Geändert:** zuvor geprüft, danach geändert. **Manuell geprüft:** durch den Anwender manuell als geprüft gesetzt. **Noch einmal prüfen:** eine zuvor geprüfte Deklaration wurde geändert und muss erneut geprüft werden. |
| **Unvollständig** | Wenn gesetzt, kennzeichnet das Modul die Deklaration als noch nicht vollständig (nicht editierbar). |
| **Kumulativ** | Wenn aktiviert, werden zusätzlich kumulierte Länder/Regionen berücksichtigt; das Kennzeichen wird automatisch gesetzt, sobald kumulierte Länder erfasst sind. Ohne kumulierte Länder ist eine Freigabe mit aktiviertem *Kumulativ* nicht möglich. |
| **Kumulierte Länder/Regionen** | Anzahl der kumulierten Länder; per Lookup öffnet sich die Pflegeseite **Kumuliertes Land/Region für Lieferantendeklaration**. |
| **Stornodatum** | Datum des Abbruchs (bei Status *Abgebrochen*). |
| **Erstellt von/am**, **Geändert von/am** | Protokollfelder; automatisch gepflegt. |
| **Genehmigungscode** / **Genehmigungsbeschreibung** | Optionaler Genehmigungsbezug aus der Stammdatenliste **Genehmigung**. |

> Hinweis zur Unterscheidung der Karten: Die **Lieferantendeklarationskarte** (langfristig) zeigt zusätzlich die Register **Lieferantendeklaration enthalten** und **Lieferantendeklarationsausnahme** sowie den Gültigkeitsstatus. Die **einstufigen** Verkaufs-/Einkaufsseiten zeigen diese Register nicht, dafür dieselben Kopf- und Länderbereiche.

### Worksheet-Bereiche der Deklaration

Die Karte fasst mehrere Unterseiten zusammen. Jeder Bereich pflegt einen Teil der Deklaration.

#### Lieferantendeklaration Land/Region

Pflegt die einzelnen zugesagten Länder.

| Feld | Erläuterung |
|---|---|
| **Code** | Land/Region, das in der Deklaration zugesagt wird. Bei Eingabe wird geprüft, ob das Land im gültigen Bereich liegt. |
| **Namen** | Bezeichnung des Landes. |
| **Freitext** | Erläuternder Text zur Länderzeile. |
| **Bestätigt** | Wenn aktiviert, gilt das Land als zugesagt und wird in die freigegebene Deklaration übernommen. Gehört das Land zu einer Gruppe, fragt das Modul, ob die gesamte Gruppe bestätigt werden soll. Ein Land, das in einer Gruppe enthalten ist, kann nicht einzeln auf „nicht bestätigt“ gesetzt werden. |
| **In Länder-/Regionsgruppe** | Zeigt, ob das Land Teil einer Gruppe ist. |
| **Länder-/Regionsgruppe** | Gruppe, der das Land zugeordnet ist. |
| **Gültigkeit ab** / **Gültig bis** | Optionaler Gültigkeitszeitraum der Länderzeile; muss innerhalb des Deklarationszeitraums liegen, sonst meldet die Prüfung das Land als ungültig. |

#### Lieferantendeklaration Länder-/Regionsgruppe

Pflegt die in der Deklaration bestätigten Gruppen.

| Feld | Erläuterung |
|---|---|
| **Code** | Bestätigte Länder-/Regionsgruppe. |
| **Namen** | Bezeichnung der Gruppe. |
| **Bestätigt** | Wenn aktiviert, werden bei langfristigen Deklarationen die zugehörigen Länder der Gruppe ebenfalls als bestätigt geführt; das Modul prüft dabei, dass der Zeitraum gesetzt und gültig ist. |
| **Gültigkeit ab** / **Gültig bis** | Optionaler Gültigkeitszeitraum der Gruppenzeile. |

#### Lieferantendeklaration enthalten (nur langfristig)

Legt fest, **welche** Artikel/Materialarten/Zollpositionen von der langfristigen Deklaration abgedeckt sind. Beim Buchen wird über diese Liste geprüft, ob eine Beleg­zeile durch eine vorhandene langfristige Deklaration gedeckt ist (Querverweis: Beleg-Integration).

| Feld | Erläuterung |
|---|---|
| **Typ** | **Artikel**, **Materialart** oder **Zollpos.**. Je nach Auswahl werden die zugehörigen Felder bearbeitbar; beim Wechsel werden die übrigen Felder geleert. |
| **Zollpos.** | Wenn Typ = Zollpos.: die abgedeckte Zollposition. |
| **Artikelnr.** / **Variantencode** | Wenn Typ = Artikel: der abgedeckte Artikel und ggf. die Variante. |
| **Matchcode** | Suchhilfe zur schnellen Artikelermittlung. |
| **Materialartcode** | Wenn Typ = Materialart: die abgedeckte Materialart. |
| **Beschreibung** / **Beschreibung 2** / **Referenznr.** | Beschreibende Felder; werden aus dem Artikel abgeleitet (nicht editierbar). |

#### Lieferantendeklarationsausnahme (nur langfristig)

Definiert Ausnahmen, die trotz Treffer in „enthalten“ **nicht** durch die langfristige Deklaration abgedeckt sind (dann ist eine einstufige Deklaration erforderlich).

| Feld | Erläuterung |
|---|---|
| **Typ** | **Materialart**, **Artikel**, **Artikelvariante** oder **Eigenschaft**. Die jeweils passenden Felder werden bearbeitbar. |
| **Materialartcode** | Wenn Typ = Materialart: ausgenommene Materialart. |
| **Artikelnr.** / **Variantencode** | Wenn Typ = Artikel/Artikelvariante: ausgenommener Artikel bzw. Variante. |
| **Matchcode** | Suchhilfe. |
| **Eigenschaftsnr.** / **Eigenschaftswertfilter** / **Eigenschaftsbeschreibung** | Wenn Typ = Eigenschaft: Ausnahme anhand einer Materialeigenschaft und deren Wertfilter. |
| **Beschreibung** / **Beschreibung 2** / **Referenznr.** | Beschreibende Felder. |

#### Zugewiesene Belege

Zeigt und pflegt die mit der Deklaration verknüpften Belege.

| Feld | Erläuterung |
|---|---|
| **Belegart** | **(leer)**, **Einkauf Bestellung**, **Einkauf Beleg**, **Einkauf Rechnung**, **Verkaufsauftrag**, **Verkaufslieferung** oder **Verkaufsrechnung**. Bestimmt, aus welchem Belegtyp die Zuordnung stammt; bei Auswahl wird die Debitoren-/Kreditornr. nachgeschlagen. |
| **Belegnr.** | Nummer des zugeordneten Belegs. |
| **Belegzeilennr.** | Zeilennummer des zugeordneten Belegs. |

> Eine nachträgliche Änderung zugewiesener Belege ist gesperrt; bei Bedarf die Zeile löschen und neu einfügen.

#### Infoboxen der Karte

- **Übers. Decl. Chargennr.** (Factbox): zeigt die zur Deklaration gehörenden Chargen je Charge an.
- **DropZone** (Factbox): Anhänge zur Deklaration per Drag-and-drop (über das m+m-Dropzone-Modul; als Quelle ist **Lieferantenerklärung** registriert).

### Aktionen der Deklaration (Freigabe- und Gültigkeitsablauf)

Die folgenden Schritte spiegeln den geprüften Ablauf wider. Sie erscheinen — je nach Karte — in den Gruppen **Freigeben** und **Weitere Aktionen**.

1. **Gültige Länder einfügen** — füllt die Land/Region-Zeilen (und bei langfristigen Deklarationen die Gruppen) automatisch aus den als deklarationsrelevant markierten Ländern. Sind bereits Länder erfasst, wird vor dem Neuaufbau nachgefragt.
2. **Kummulierung Land/Region** — öffnet **Kumuliertes Land/Region für Lieferantendeklaration** zur Pflege kumulierter Länder; setzt anschließend das Kennzeichen **Kumulativ**, wenn kumulierte Länder vorhanden sind.
3. **Länder mit Kumulierung aktualisieren** — aktualisiert die Länder aller Chargen der Deklaration anhand der Charge-Herkunft und der Gruppen.
4. **Länder prüfen** — prüft, ob alle bestätigten Länder, Gruppen und Gruppenländer im Gültigkeitszeitraum liegen. Erfolg: **Gültigkeitsstatus** = *Geprüft*. Andernfalls wird ein zuvor geprüfter Status auf *Noch einmal prüfen* gesetzt. Ohne erfassten Zeitraum erscheint ein Hinweis, dass keine Prüfung erfolgte.
5. **Manuelle Gültigkeit festlegen** / **Gültigkeit zurücksetzen** — setzt den Gültigkeitsstatus manuell auf *Manuell geprüft* bzw. zurück auf *Scheck notwendig*.
6. **Freigeben** — gibt die Deklaration frei: Ist der Gültigkeitsstatus noch *Scheck notwendig*, wird die Freigabe mit einem Hinweis verweigert. Andernfalls werden nicht relevante Länder entfernt, die Pflichtprüfung ausgeführt, das Freigabedatum gesetzt, je Charge ein Eintrag in **Chargennr. Lieferantendeklaration** geschrieben und der **Status** auf *Herausgegeben* gesetzt.
7. **Öffnen** — setzt eine freigegebene Deklaration auf *Offen* zurück und entfernt die Charge-Deklarationseinträge.
8. **Abbrechen** — storniert die Deklaration (Status *Abgebrochen*), entfernt die Charge-Deklarationseinträge und setzt das Stornodatum.
9. **Beleg hinzufügen** / **Verkaufslieferung hinzufügen** / **Einkaufslieferung hinzufügen** — ordnet gebuchte Verkaufslieferungs- bzw. Einkaufslieferungszeilen der Deklaration zu (Auswahl über **Gebuchte Verkaufslieferungszeilen** bzw. **Gebuchte Einkaufslieferungszeilen**) und übernimmt die zugehörigen Chargen.
10. **Drucken** — druckt/versendet die Deklaration über den in der Einrichtung hinterlegten Bericht.

## 8D-Report und E-Mail

Dieses Modul enthält keinen 8D-Report und keine modulspezifische E-Mail-Funktion. Der einzige Ausgabekanal ist der konfigurierbare **Bericht** zur Lieferantendeklaration (Aktion **Drucken**), dessen Berichts-ID je Bereich/Typ in der Einrichtung hinterlegt wird. Drucken/Versenden kann über **Dekl. Drucken/Senden Mit** abgesichert werden (Warnung/Fehler). Eine eigene Versandprotokollierung führt das Modul nicht.

## Beleg-Integration (Verkaufs- und Einkaufsbelege)

Das Modul erweitert die Standardbelege um Statusfelder und greift beim Freigeben und Buchen ein. Voraussetzung sind die Einrichtung (**Lieferantendeklarationsfunktionen aktiv**, **Ereignisherausgeber aktiviert**) und die Stammdaten (**Lieferantendeklaration erforderlich**, **Lieferantendeklaration für Typen**) — siehe **Einrichtung** und **Stammdaten**.

### Zusatzfelder in den Beleg­zeilen

Die Felder erscheinen in den Zeilen von **Verkaufsauftrag** und **Einkaufsbestellung** (sowie in Angebots-, Rahmen- und gebuchten Beleg-Unterseiten in gleicher Form):

| Feld | Erläuterung |
|---|---|
| **Lieferantendeklaration erforderlich** | Wenn gesetzt, verlangt die Zeile eine Lieferantendeklaration. Das Modul ermittelt das Kennzeichen beim Erfassen von **Artikelnr.** oder **Variantencode** aus dem Geschäftspartner (**Lieferantendeklaration erforderlich**) und den Einträgen **Lieferantendeklaration für Typen**. |
| **Verkaufslieferantendeklaration-Status** / **Einkauf Tor. Abschl.-Status** (Beleg­status) | Beim Freigeben des Belegs ermittelt: **(leer):** noch nicht ermittelt. **Langfristige Lieferantendeklaration vorhanden:** eine gültige, freigegebene langfristige Deklaration deckt die Zeile ab. **Einstufige Lieferantendeklaration erforderlich:** keine langfristige Deklaration deckt die Zeile ab; es wird eine einstufige benötigt. |
| **Einkaufspl.-Abgrenzungsstatus** (Bestandsbezug, Verkaufszeile, nicht editierbar) | Ergebnis der Bestandsprüfung der vorhandenen Chargen: **(leer):** nicht ermittelt. **Einstufige Lieferantendeklaration möglich:** alle offenen Chargen haben eine Einkaufs-Deklaration. **Einstufige Lieferantendeklaration nicht möglich:** keine Charge hat eine Deklaration. (Zwischenstufe „eingeschränkt möglich“: nur ein Teil der Chargen hat eine Deklaration.) Der Status wird farblich hervorgehoben (günstig/uneindeutig/ungünstig). |

### Status beim Freigeben des Belegs

Wird ein **Verkaufsauftrag** oder eine **Einkaufsbestellung** freigegeben, prüft das Modul je deklarationspflichtiger Zeile, ob eine gültige, freigegebene langfristige Deklaration den Artikel/die Variante einschließt (über **Lieferantendeklaration enthalten**) und keine **Ausnahme** greift. Ergebnis ist der oben beschriebene Beleg­status. Zusätzlich wird für Verkaufszeilen anhand der offenen Artikelposten geprüft, ob die vorhandenen Chargen über eine Einkaufs-Deklaration verfügen.

### Beim Buchen

1. **Verkaufslieferung buchen.** Für deklarationspflichtige Lieferzeilen ohne vorhandene Deklaration wird — falls **Lieferantendeklaration bei Verkaufslieferung erstellen** aktiv ist — eine einstufige Verkaufs-Deklaration inklusive Land, zugewiesenem Beleg und Chargen erzeugt; ist **Lieferantendeklaration bei Verkaufslieferung freigeben** aktiv, wird sie sofort freigegeben. Deckt eine langfristige Deklaration die Zeile, wird stattdessen nur der Beleg zugeordnet.
2. **Einkaufslieferung buchen.** Für deklarationspflichtige Bestellzeilen wird die gebuchte Einkaufslieferung einer passenden, gültigen, freigegebenen langfristigen Einkaufs-Deklaration zugeordnet und die Chargen werden übertragen.
3. **Verkaufsrechnung buchen.** Ist **Auf fehlenden Lagerpl. decl. auf Verkaufsrechnungsbuchung prüfen** auf **Warnung** oder **Fehler** gestellt und fehlt für eine deklarationspflichtige Zeile die Deklaration der zugehörigen Lieferung, erscheint ein Hinweis bzw. die Buchung wird abgebrochen.

### Folgebelegzeilen: einstufige Deklaration erzeugen

In den **Gebuchten Verkaufslieferungszeilen** und **Gebuchten Einkaufslieferungszeilen** steht die Aktion **Deklaration für einzelne Lieferanten erstellen** zur Verfügung. Damit erzeugt der Anwender nachträglich aus einer gebuchten Zeile eine einstufige Lieferantendeklaration, wenn beim Buchen keine erzeugt wurde.

## Chargenverfolgung, Historie und Nachweis

Ob eine Charge über eine Lieferantendeklaration verfügt, lässt sich an mehreren Stellen nachvollziehen.

### Chargennr.-Informationskarte

Das Modul ergänzt die **Chargennr.-Informationskarte** um zwei Felder:

| Feld | Erläuterung |
|---|---|
| **Lieferantendeklaration vorhanden** (Einkauf) | Wenn gesetzt, existiert für diese Charge eine Einkaufs-Lieferantendeklaration. Per Lookup öffnet das Modul die zugehörige Deklaration (bei genau einem Treffer die **Lieferantendeklarationskarte**, sonst die Chargenverfolgung). |
| **Lieferantendeklaration vorhanden** (Verkauf) | Wenn gesetzt, existiert für diese Charge eine Verkaufs-Lieferantendeklaration; Lookup wie oben für den Bereich Verkauf. |

### Materialbestände

In den **Materialbeständen** (m+m Material Properties) ergänzt das Modul je Chargenzeile das Feld **Lieferantendeklaration vorhanden**. Wenn gesetzt, besitzt die Charge eine Einkaufs-Deklaration; per Lookup gelangt der Anwender direkt zur Deklaration oder zur Chargenverfolgung.

### Chargenverfolgung der Lieferantendeklaration

Die Verfolgungsseite (Aufruf u. a. über die Lookups der Chargenfelder) zeigt die Herkunfts-/Verbrauchskette der Chargen mit Bezug zur Lieferantendeklaration.

**Filter**

| Filterfeld | Erläuterung |
|---|---|
| **Artikelfilter** | Wenn gesetzt, werden die Verfolgungszeilen auf diesen Artikel eingegrenzt. Ein Artikelfilter ist für die Verfolgung erforderlich. |
| **Variantenfilter** | Wenn gesetzt, Eingrenzung auf eine Variante. |
| **Chargennr. Filter** | Wenn gesetzt, Eingrenzung auf eine Charge. |
| **Seriennr. Filter** | Wenn gesetzt, Eingrenzung auf eine Seriennummer. |
| **Ablaufverfolgungsmethode** | Bestimmt die Richtung der Verfolgung. **Ursprung -> Verbrauch:** von der Quelle zur Verwendung. **Verbrauch -> Ursprung:** von der Verwendung zur Quelle. |
| **Komponenten anzeigen** | **Nein:** keine Komponenten. **Nur mit Artikelverfolgung:** nur chargen-/seriengeführte Komponenten. **Alle:** alle Komponenten. |

Aktionen der Verfolgung: **Ablaufverfolgung** (Verfolgung ausführen), **Filter mit Zeilenwerten festlegen**, **Umgekehrte Nachverfolgung - zeilenseitig**, **Nächstes/Vorhergehendes Ergebnis der Ablaufverfolgung**, **Beleg anzeigen**, **Artikel/Karte/Posten**, **Drucken** sowie der Sprung zur Historie **Gehe zu Historie 'Bereits nachverfolgt'**.

### Charge-Lieferantendeklaration

Beim Freigeben entstehen Einträge in **Chargennr. Lieferantendeklaration** je Charge (Felder u. a. **Chargennr.**, **Artikelnr.**, **Variantencode**, **Bereich**, **Typ**, **Lieferantendeklarationsnr.**, **Kreditoren-Chargennr.**). Diese Tabelle ist die Nachweisbasis dafür, welche Charge in welcher Deklaration zugesagt wurde; manuelle Änderungen sind hier gesperrt und müssen in der Deklaration erfolgen.

## FAQ und Troubleshooting

### Warum kann ich eine Deklaration nicht freigeben, obwohl Länder bestätigt sind?
Wenn der **Gültigkeitsstatus** noch *Scheck notwendig* ist, verweigert **Freigeben** den Vorgang mit einem Hinweis. Führen Sie zuerst **Länder prüfen** aus (oder **Manuelle Gültigkeit festlegen**), sodass der Status auf *Geprüft* bzw. *Manuell geprüft* wechselt.

### Warum meldet das System, dass das Land kein EU-Mitglied ist?
Beim Setzen von **Debitoren-/Kreditornr.** oder **Deb./Kred. Länder-/Regionscode** prüft das Modul die EU-Mitgliedschaft des Landes. Ist der EU-Ländercode am Land/Region nicht hinterlegt, wird das Einfügen abgebrochen. Pflegen Sie den EU-Ländercode am Land oder wählen Sie einen EU-Geschäftspartner.

### Warum werden meine Eingaben in der Deklaration nicht gespeichert?
Änderungen sind nur im **Status** *Offen* zulässig. Eine freigegebene oder abgebrochene Deklaration ist gegen Änderungen gesperrt. Setzen Sie sie zunächst über **Öffnen** zurück.

### Warum verlangt eine Beleg­zeile eine Lieferantendeklaration?
Das Feld **Lieferantendeklaration erforderlich** wird gesetzt, wenn am Geschäftspartner **Lieferantendeklaration erforderlich** aktiv ist und die Zeile zu einem Eintrag unter **Lieferantendeklaration für Typen** passt (nach Artikel/Variante, Materialart oder Zollposition). Voraussetzung ist zusätzlich **Ereignisherausgeber aktiviert** in der Einrichtung.

### Was bedeutet der Beleg­status „Einstufige Lieferantendeklaration erforderlich“?
Es gibt keine gültige, freigegebene **langfristige** Deklaration, die den Artikel/die Variante über **Lieferantendeklaration enthalten** abdeckt (oder eine **Ausnahme** greift). Für diese Zeile muss eine **einstufige** Deklaration erstellt werden.

### Was passiert beim Buchen einer Verkaufslieferung automatisch?
Für deklarationspflichtige Zeilen ohne Deckung erzeugt das Modul — bei aktivem **Lieferantendeklaration bei Verkaufslieferung erstellen** — eine einstufige Deklaration mit Land, zugewiesenem Beleg und Chargen und gibt sie bei aktivem **Lieferantendeklaration bei Verkaufslieferung freigeben** sofort frei. Andernfalls wird nur der Beleg einer vorhandenen langfristigen Deklaration zugeordnet.

### Warum wird meine Verkaufsrechnung beim Buchen abgewiesen?
Ist **Auf fehlenden Lagerpl. decl. auf Verkaufsrechnungsbuchung prüfen** auf **Fehler** gestellt und besitzt die zugrunde liegende Verkaufslieferung für eine deklarationspflichtige Zeile keine Deklaration, bricht die Buchung ab. Erstellen Sie die fehlende Deklaration oder stellen Sie die Prüfung auf **Warnung**.

### Warum kann ich „Kumulativ“ nicht freigeben?
Ist **Kumulativ** gesetzt, aber es wurden keine kumulierten Länder zugewiesen, ist die Freigabe nicht möglich. Pflegen Sie die kumulierten Länder über **Kummulierung Land/Region** oder deaktivieren Sie **Kumulativ**.

### Warum erscheint beim Bestätigen eines Landes die Frage nach der ganzen Gruppe?
Gehört das bestätigte Land zu einer Gruppe, fragt das Modul, ob die gesamte Gruppe bestätigt werden soll. Bestätigen Sie, werden alle Länder der Gruppe als bestätigt geführt; ein einzelnes Land einer Gruppe kann nicht separat auf „nicht bestätigt“ gesetzt werden.

### Wie finde ich heraus, ob eine Charge bereits eine Lieferantendeklaration hat?
Öffnen Sie die **Chargennr.-Informationskarte** oder die **Materialbestände** und prüfen Sie das Feld **Lieferantendeklaration vorhanden**. Per Lookup gelangen Sie zur Deklaration bzw. zur Chargenverfolgung.

## Typische Anwendungsfälle

### Langfristige Lieferantenerklärung eines Lieferanten erfassen
**Auslöser:** Ein Lieferant übersendet per E-Mail eine langfristige Lieferantenerklärung für mehrere Artikel.
**Einstieg in BC:** Über **Suchen** -> **Langfristige Lieferantendeklarationen - Einkauf** -> *Neu* (Bereich Einkauf, Typ langfristig werden vorbelegt) -> Karte.
**Kernablauf:** Kreditor auswählen (Anschrift wird übernommen, EU-Prüfung läuft). **Gültigkeit ab/Gültig bis** erfassen. Im Register **Lieferantendeklaration enthalten** die abgedeckten Artikel/Materialarten/Zollpositionen eintragen, bei Bedarf Ausnahmen pflegen. Mit **Gültige Länder einfügen** die Länder vorbelegen und in **Lieferantendeklaration Land/Region** über **Bestätigt** zusagen; ggf. Gruppen bestätigen. **Länder prüfen** -> Gültigkeitsstatus *Geprüft*. **Freigeben** -> Status *Herausgegeben*.
**Abschluss:** Optional **Drucken** für den Nachweis; die Deklaration deckt künftig passende Einkaufs- und Verkaufszeilen ab.

### Einstufige Verkaufs-Lieferantendeklaration für eine Lieferung
**Auslöser:** Ein Kunde fordert für eine bereits gebuchte Lieferung eine Lieferantenerklärung an.
**Einstieg in BC:** Über **Suchen** -> **Verk. einzelner Lieferantendeklarationen** -> *Neu* -> Karte (Bereich Verkauf, Typ einstufig vorbelegt).
**Kernablauf:** Debitor auswählen. Über **Beleg hinzufügen** die betreffenden Zeilen aus **Gebuchte Verkaufslieferungszeilen** zuordnen (das Modul übernimmt die Chargen). Land/Region bestätigen, **Freigeben**.
**Abschluss:** **Drucken** für den Kundennachweis. Alternativ entsteht diese Deklaration bei aktiver Einrichtung bereits **automatisch beim Buchen** der Verkaufslieferung und wird ggf. sofort freigegeben.

### Buchungsprüfung im Tagesgeschäft
**Auslöser:** Ein Sachbearbeiter bucht eine Verkaufsrechnung zu einer Lieferung mit deklarationspflichtigen Artikeln.
**Einstieg in BC:** Standard-Verkaufsrechnung; keine eigene Modulseite nötig.
**Kernablauf:** Beim Buchen prüft das Modul gemäß **Auf fehlenden Lagerpl. decl. auf Verkaufsrechnungsbuchung prüfen**, ob die Lieferung der deklarationspflichtigen Zeilen über eine Deklaration verfügt. Bei **Warnung** erscheint ein Hinweis und die Buchung läuft weiter; bei **Fehler** wird abgebrochen.
**Abschluss:** Fehlt eine Deklaration, erstellt der Anwender sie über **Deklaration für einzelne Lieferanten erstellen** in den gebuchten Lieferungszeilen und bucht erneut.
