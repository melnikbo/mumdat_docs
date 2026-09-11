---
title: Anwenderhandbuch m+m Goods Receipt with Package Management
---

# Anwenderhandbuch m+m Goods Receipt with Package Management

## Einleitung

Die App **m+m Goods Receipt with Package Management** verbindet die m+m **Warenvereinnahmung** mit der m+m **Packmittelverwaltung**. Sie ermöglicht es, bereits während der Warenannahme im Lager die einzelnen Komponentenzeilen einem **Packmittel** zuzuordnen, neue Pakete direkt aus einer Komponente zu erstellen und Pakete aus einer **Packmittelreferenz** zu übernehmen. Beim Verarbeiten der Warenannahme werden die Packmittel automatisch in die verarbeitete Warenannahme sowie in einen daraus entstehenden Umlagerungseingang übergeben und können als Etiketten gedruckt werden.

Die Verarbeitung stützt sich vollständig auf die zugrunde liegenden Belege der Warenvereinnahmung. Die App fügt dort keine eigenen Belege hinzu, sondern erweitert die bestehende **Warenannahme**, den **Warenumlagerungseingang**, die **Packmittelposten** und die zugehörige **Warenvereinnahmung Einrichtung** um Packmittelfunktionen.

**Zielgruppe.** Primäre Anwender sind **operative Lagermitarbeiter** und Personen in der Warenannahme, die täglich Komponentenzeilen erfassen, Pakete zuweisen und Warenannahmen verarbeiten. Sekundär richtet sich das Kapitel **Einrichtung** an Administratoren bzw. Key-User, welche die Packmittelverarbeitung einmalig konfigurieren.

**Typischer Weg durch die App.** Der Anwender öffnet die **Warenannahme**, wählt eine Zeile bzw. deren Komponentenzeilen, weist über die Packmittelaktionen ein Paket zu (oder erstellt eines) und startet anschließend **Wareneingang verarbeiten und Packmittel drucken**. Die Packmittel erscheinen danach in der verarbeiteten Warenannahme, in den Folgebelegen der Umlagerung und in den **Packmittelposten**.

## Schnellstart für Anwender

Der schnellste Weg von der Einrichtung bis zum gedruckten Packmittel folgt der vom Code erzwungenen Reihenfolge (zuerst Einrichtung, dann Beleg, dann Verarbeitung):

1. **Einrichtung prüfen.** Öffnen Sie über **Suchen** die **Warenvereinnahmung Einrichtung** und legen Sie im Register **Verarbeitung** fest, ob und wie Packmittel gedruckt werden (**Packmittel drucken**), welcher Bericht dafür verwendet wird (**Packmittel Beleg-ID**) und ob Pakete automatisch an Komponenten zugewiesen werden (**Paket automatisch einer Komponente zuweisen**). Siehe Kapitel **Einrichtung**.
2. **Warenannahme öffnen.** Öffnen Sie über **Suchen** die **Warenannahme** und wählen Sie den zu bearbeitenden Beleg.
3. **Komponentenzeile wählen.** Öffnen Sie die Komponentenzeilen der Warenannahme. In der Spalte **Paketstatus** erkennen Sie farblich, ob eine Zeile noch keinem, teilweise oder vollständig einem Paket zugeordnet ist.
4. **Paket zuweisen oder erstellen.** Wählen Sie auf der Zeile eine der Aktionen **Packmittelzuweisung**, **Neues Paket erstellen** oder **Von Packmittelreferenz erstellen** (siehe **Tägliche Arbeit – Komponentenzeilen und Packmittel**).
5. **Verarbeiten und drucken.** Wählen Sie in der **Warenannahme** die Aktion **Wareneingang verarbeiten und Packmittel drucken**. Bestätigen Sie den Verarbeitungsdialog; danach werden die Packmittel des Berichts **Verarbeitete Warenannahme-Packmittel** gedruckt.
6. **Ergebnis prüfen.** Kontrollieren Sie die erzeugten Packmittel in der verarbeiteten Warenannahme, im **Warenumlagerungseingang** (Feld **Paketstatus**) und in den **Packmittelposten** (Felder **Warenannahmennr.** und **Warenannahmenzeilennr.**).

Der Packmittel-Etikettendruck lässt sich auch nachträglich aus der verarbeiteten Warenannahme über die Aktion **Packmittel drucken** anstoßen.

## Einrichtung

Die zentrale Einstellung dieser App liegt vollständig auf der bestehenden Seite **Warenvereinnahmung Einrichtung** der m+m Warenvereinnahmung. Es gibt keine eigene Setup-Seite dieser App; die drei Packmittelfelder werden in das bestehende Register **Verarbeitung** eingefügt. BC-Anwender sehen daher genau **eine** Einrichtungsseite, die im Folgenden bezogen auf die Packmittelverarbeitung vollständig beschrieben wird.

### Packmitteldruck und automatische Paketzuweisung einrichten

**Wer und wann.** Diese Einrichtung nimmt ein Administrator oder Key-User **einmalig vor der ersten Warenannahme mit Packmitteln** vor. Sie steuert, welcher Bericht beim Verarbeiten gedruckt wird, ob überhaupt gedruckt wird und ob Pakete beim Buchen automatisch an Fertigungskomponenten übergeben werden. Die Werte werden später in der **Warenannahme** (Aktion **Wareneingang verarbeiten und Packmittel drucken**) sowie bei der Zubuchung von Komponenten wirksam.

**Einstieg:** Öffnen Sie über **Suchen** die Seite **Warenvereinnahmung Einrichtung** und wechseln Sie in das Register **Verarbeitung**. Es handelt sich um eine unternehmensweite Einrichtung (ein Datensatz je Mandant).

Beim Öffnen der Seite trägt die App automatisch einen Standardbericht ein, sofern noch keiner hinterlegt ist (siehe **Packmittel Beleg-ID**).

| Einrichtung | Erläuterung |
|-------------|-------------|
| Packmittel drucken | Legt fest, ob und wie beim Verarbeiten der Warenannahme Packmitteletiketten gedruckt werden. **Kein Druck:** Beim Verarbeiten wird kein Packmittelbericht gedruckt; die Paketzuordnung bleibt rein datenseitig. **Pro Packmittel:** Für jedes einzelne Paket wird ein Etikett des hinterlegten Berichts erzeugt. **Pro Packmittelgruppe:** Der Druck erfolgt gebündelt je Packmittelgruppe; passend dazu wird auf der Warenannahmezeile die Verteilung **Pro Packmittelgruppe** verwendet, sodass die zuzuweisende Menge je Gruppe ermittelt wird. |
| Packmittel Beleg-ID | Bestimmt den Bericht, der für den Packmitteldruck ausgeführt wird. Wenn das Feld leer ist, setzt die App beim Öffnen der Einrichtung sowie beim Verarbeiten automatisch den mitgelieferten Bericht **Verarbeitete Warenannahme-Packmittel** ein; hinterlegen Sie hier einen abweichenden Bericht, wenn Sie ein eigenes Etikettenlayout nutzen. Der so hinterlegte Bericht wird sowohl bei **Wareneingang verarbeiten und Packmittel drucken** als auch bei der nachträglichen Aktion **Packmittel drucken** verwendet. |
| Paket automatisch einer Komponente zuweisen | Wenn aktiviert, werden beim Buchen des Warenannahme-Artikeljournals die vorhandenen physischen Pakete automatisch an die verknüpfte Fertigungsauftragskomponente übergeben; der Anwender muss die Pakete nicht manuell der Komponente zuordnen. Ohne Kennzeichen unterbleibt diese automatische Übergabe, und die Komponente bleibt ohne Paketbezug, bis eine Zuordnung manuell erfolgt. |

**Prozessschritte der Einrichtung.**

1. **Zuerst** entscheiden Sie unter **Packmittel drucken**, ob gedruckt werden soll und ob je Paket oder je Packmittelgruppe. Bei **Pro Packmittelgruppe** stellen Sie sicher, dass die betreffenden Warenannahmezeilen die Verteilung **Pro Packmittelgruppe** verwenden.
2. **Danach** prüfen bzw. hinterlegen Sie unter **Packmittel Beleg-ID** den gewünschten Bericht. Belassen Sie das Feld leer, wird der Standardbericht automatisch gesetzt.
3. **Schließlich** aktivieren Sie **Paket automatisch einer Komponente zuweisen**, wenn Pakete beim Buchen ohne Zusatzschritt an Fertigungskomponenten übergeben werden sollen.

Die Wirkung dieser Felder im Tagesablauf ist im Kapitel **Tägliche Arbeit – Komponentenzeilen und Packmittel** sowie in **Warenannahme verarbeiten und Packmittel drucken** beschrieben.

## Stammdaten und Verteilungssteuerung

Diese App führt keine eigenen Stammdatenkarten (keine Team-, Fehler- oder Profilstammdaten). Der einzige stammdatennahe Steuerungspunkt ist die **Verteilung** auf der Warenannahmezeile, die um einen Packmittelwert erweitert wird.

### Verteilung „Pro Packmittelgruppe“ auf der Warenannahmezeile

Auf der Warenannahmezeile der m+m Warenvereinnahmung steuert das Feld **Verteilung** (2. Verteilung, Feld **Allocation 2**), wie die Ausgabemenge auf die Komponenten verteilt wird. Diese App fügt dieser Auswahl den zusätzlichen Wert **Pro Packmittelgruppe** hinzu.

| Feld | Erläuterung |
|------|-------------|
| Verteilung → **Pro Packmittelgruppe** | Wenn auf der Warenannahmezeile die Verteilung **Pro Packmittelgruppe** gewählt ist, richtet sich die je Komponente zuzuweisende Menge nach der Menge der zugehörigen Packmittelgruppe (Feld **Zu bearbeitende Menge** des Pakets), und die Zahl der Verteilungen entspricht der **Gesamtanzahl Packmittel** der Komponente. So entsteht je Packmittelgruppe genau eine Verteilung. |

**Prüfregel (aus dem Code).** Bei Auswahl der Verteilung **Pro Packmittelgruppe** darf die Warenannahmezeile nur **eine** Komponentenzeile besitzen, die nicht den **Paketstatus** **Packmittel** trägt. Bestehen mehrere solche Komponentenzeilen, bricht das System die Auswahl mit einer Fehlermeldung ab. Legen Sie die Verteilung daher fest, solange die Zeile nur eine offene Komponente enthält, und bündeln Sie weitere Mengen über Pakete.

Der Zusammenhang zur Einrichtung: Der Wert **Pro Packmittelgruppe** wirkt zusammen mit der Einstellung **Packmittel drucken → Pro Packmittelgruppe** (Kapitel **Einrichtung**), sodass Verteilung und Etikettendruck auf derselben Gruppierung beruhen.

## Tägliche Arbeit – Komponentenzeilen und Packmittel

Die eigentliche Packmittelarbeit findet auf den **Komponentenzeilen der Warenannahme** statt. Diese Seite wird von den Einstellungen der **Warenvereinnahmung Einrichtung** (Register **Verarbeitung**) gesteuert: dort ist festgelegt, ob und wie gedruckt wird und ob Pakete automatisch an Komponenten übergehen. Die folgende Beschreibung setzt eine geöffnete **Warenannahme** und deren Komponentenzeilen voraus.

### Zusätzliche Spalten der Komponentenzeile

Die App ergänzt die Komponentenzeile um folgende Felder:

| Feld | Erläuterung |
|------|-------------|
| Paketstatus | Zeigt an, wie weit die Komponentenzeile bereits einem Paket zugeordnet ist. Das Feld ist nicht editierbar und wird beim Aufruf der Zeile aus der zugehörigen Artikeljournalzeile aktualisiert. Es ist farblich hervorgehoben (siehe Werte unten). **(leer):** Die Zeile ist noch keinem Paket zugewiesen — die Paketzuweisung ist erst noch vorzunehmen. **Voll:** Die Zeilenmenge ist vollständig einem Paket zugeordnet (grün, „günstig“). **Teilweise:** Nur ein Teil der Menge ist zugeordnet (gelb, „mehrdeutig“) — es verbleibt Restmenge. **Packmittel:** Die Zeile ist selbst eine Paketzeile (hervorgehoben); solche Zeilen sind gesperrt und können weder geändert noch als eigene Komponente zugewiesen werden. |
| Gesamtanzahl Packmittel | Zeigt die Anzahl der Pakete, die zu dieser Warenannahmezeile angelegt wurden (Anzahl der Paketzeilen in den Belegpaketen). Der Wert wird laufend berechnet; eine Null wird ausgeblendet. Er dient als Grundlage für die Verteilung **Pro Packmittelgruppe** (siehe **Stammdaten und Verteilungssteuerung**). |
| Packmittelreferenznr. | Verweist auf eine hinterlegte **Packmittelreferenz** (Verpackungsvorschrift) und füllt aus dieser die Paketstruktur vor. Beim Eintragen prüft und übernimmt die App die Referenz anhand von Artikel, Variante, Menge und Debitor der Warenannahme. Das Feld lässt sich nur auswählen, solange der **Paketstatus** **(leer)** ist und die Zeilenmenge größer als 0 ist; andernfalls meldet das System, dass die Referenz nicht gewählt werden kann, weil die Menge 0 ist oder der Artikel bereits einem Paket zugewiesen wurde. |

### Aktionen auf der Komponentenzeile

Die Zeilenaktionen im Menü **Zeile** decken die drei Wege ab, ein Paket zu einer Komponente zu bilden:

| Aktion | Erläuterung |
|--------|-------------|
| Packmittelzuweisung | Öffnet die Paketzuweisung der Packmittelverwaltung für die zur Zeile gehörende Artikeljournalzeile. Hier ordnet der Anwender die vorhandene Menge bestehenden Paketen zu. Die Aktion ist deaktiviert, wenn die Zeile bereits den **Paketstatus** **Packmittel** hat. |
| Neues Paket erstellen | Erstellt aus der Komponentenzeile ein neues Paket und verteilt die zuzuweisende Menge gleichmäßig auf die neu erzeugten Pakete; die Restmenge wird dem letzten Paket zugeschlagen. Bereits zuvor gebildete Pakete der Zeile bleiben erhalten und werden nicht erneut befüllt. |
| Von Packmittelreferenz erstellen | Erstellt die Pakete anhand der auf der Zeile eingetragenen **Packmittelreferenznr.**, also gemäß der hinterlegten Verpackungsvorschrift, und fasst gleichartige Paketkomponenten der Zeile anschließend zusammen. Die Aktion ist deaktiviert, wenn die Zeile bereits den **Paketstatus** **Packmittel** hat. |

**Schrittfolge zur Paketbildung.**

1. **Zuerst** wählen Sie die Komponentenzeile und prüfen den **Paketstatus**. Nur Zeilen mit Status **(leer)**, **Voll** oder **Teilweise** lassen sich bearbeiten; Zeilen mit Status **Packmittel** sind gesperrt.
2. **Danach** wählen Sie den passenden Weg: bestehende Pakete füllen (**Packmittelzuweisung**), ein neues Paket bilden (**Neues Paket erstellen**) oder nach Vorschrift erzeugen (**Von Packmittelreferenz erstellen** nach Eintrag der **Packmittelreferenznr.**).
3. **Schließlich** kontrollieren Sie den aktualisierten **Paketstatus** und die **Gesamtanzahl Packmittel** der Zeile, bevor Sie die Warenannahme verarbeiten.

**Sperrverhalten (aus dem Code).** Eine Komponentenzeile mit **Paketstatus** **Packmittel** kann nicht geändert werden; das System weist Änderungen mit einer Meldung ab. Wird der Paketstatus einer Zeile auf **(leer)** zurückgesetzt, entfernt die App zugleich die **Packmittelreferenznr.**.

## Warenannahme verarbeiten und Packmittel drucken

Der Abschluss der täglichen Arbeit ist das Verarbeiten der Warenannahme. Dieser Ablauf verbindet die Standardverarbeitung der Warenvereinnahmung mit dem Packmitteldruck aus der **Warenvereinnahmung Einrichtung**.

### Verarbeiten aus der Warenannahme

**Einstieg:** In der **Warenannahme** finden Sie im Menüband unter **Vorgang** die Aktion **Wareneingang verarbeiten und Packmittel drucken** (auch als hervorgehobene Aktion verfügbar).

Ablauf (aus dem Code):

1. Wählen Sie in der **Warenannahme** den Beleg und die Aktion **Wareneingang verarbeiten und Packmittel drucken**.
2. Bestätigen Sie den Verarbeitungsdialog der Warenannahme (Ja/Nein). Bei Bestätigung wird die Warenannahme verarbeitet.
3. Nach dem Verarbeiten ermittelt die App die zugehörige **verarbeitete Warenannahme** und startet für deren Belege den unter **Packmittel Beleg-ID** hinterlegten Bericht — standardmäßig **Verarbeitete Warenannahme-Packmittel**.
4. Der Bericht wird als Druckvorschau/Druck ausgegeben; je nach Einstellung **Packmittel drucken** erfolgt der Druck pro Paket oder pro Packmittelgruppe. Steht **Packmittel drucken** auf **Kein Druck**, wird die Warenannahme verarbeitet, aber kein Etikett gedruckt.

### Packmitteletiketten nachdrucken

**Einstieg:** In der **verarbeiteten Warenannahme** finden Sie unter **Berichte** die Aktion **Packmittel drucken** (auch als hervorgehobene Aktion).

Über diese Aktion drucken Sie die Packmitteletiketten für die markierten verarbeiteten Belege erneut, ohne die Warenannahme nochmals zu verarbeiten. Auch hier wird der unter **Packmittel Beleg-ID** hinterlegte Bericht verwendet.

### Bericht „Verarbeitete Warenannahme-Packmittel“

Der mitgelieferte Bericht **Verarbeitete Warenannahme-Packmittel** ist der Standard-Etikettenbericht. Er gibt die verarbeitete Warenannahme mit ihren Paketen aus und erzeugt je Paket einen Barcode (Code 128) aus Fertigungsauftrags- und Paketdaten.

| Feld im Bericht | Erläuterung |
|-----------------|-------------|
| Debitorennr. / Verk. an Name | Debitor der verarbeiteten Warenannahme, für den die Pakete bestimmt sind. |
| Externe Auftragsnr. | Externe Bestell-/Auftragsnummer des Debitors zum Beleg. |
| Externe Lieferscheinnr. | Externe Lieferscheinnummer des Debitors zum Beleg. |
| Verarbeitete Wareneingangsnr. | Nummer der verarbeiteten Warenannahme, aus der die Pakete stammen. |
| Wareneingangsdatum | Eingangsdatum der Warenannahme. |
| Artikelnr. | Artikel des jeweiligen Pakets bzw. der Paketposition. |
| Packmittelnr. | Nummer des gedruckten Pakets; zusammen mit dem übergeordneten Paket bildet sie die Etikettenstruktur. |
| Menge | Menge der Artikelposition im Paket. |

Der Bericht ist der Standardwert des Feldes **Packmittel Beleg-ID**; ein eigenes Layout hinterlegen Sie über dieses Feld (siehe **Einrichtung**).

## Umlagerung und Folgebelege

Die App überträgt die Paketzuordnung automatisch in die Folgeprozesse der Warenvereinnahmung, insbesondere in die Umlagerung, die aus einem verarbeiteten Warenannahmebeleg entsteht.

### Paketstatus im Warenumlagerungseingang

Der **Warenumlagerungseingang** der Warenvereinnahmung wird um den **Paketstatus** auf der Zeile erweitert. Die Zeile zeigt damit dieselbe Zuordnungslogik wie die Warenannahme.

| Feld | Erläuterung |
|------|-------------|
| Paketstatus | Übernimmt den Paketstatus aus der zugehörigen Umlagerungszeile und zeigt farblich, wie weit die Umlagerungszeile einem Paket zugeordnet ist. **(leer):** noch nicht zugeordnet. **Voll:** vollständig zugeordnet (grün). **Teilweise:** teilweise zugeordnet (gelb) — Restmenge offen. Das Feld ist nicht editierbar und wird beim Aufruf der Zeile aktualisiert. |

Zusätzlich zeigt der Warenumlagerungseingang eine Infobox **Komponenten Packmittelstruktur**, die die Paketstruktur zur ausgewählten Umlagerungszeile darstellt.

**Zeilenaktion.**

| Aktion | Erläuterung |
|--------|-------------|
| Paketzuordnung – Wareneingang | Öffnet die Paketzuweisung der Packmittelverwaltung für die zur Zeile gehörende Umlagerungszeile, sodass die eingehende Ware der Umlagerung einem Paket zugeordnet werden kann. |

**Automatische Übergabe (aus dem Code).** Wird aus einem verarbeiteten Warenannahmebeleg ein Umlagerungsauftrag für Rohmaterial erzeugt, überträgt die App die physischen Pakete des Ausgangsbelegs automatisch als Belegpakete des Umlagerungsversands. Ebenso wird beim Abrufen der Umlagerungszeilen der **Paketstatus** aus der Umlagerungszeile in die Zeile des Warenumlagerungseingangs übernommen. Der Anwender findet die Pakete dadurch ohne Zusatzschritt in der Umlagerung wieder.

### Warenannahme-Bezug in den Packmittelposten

Die **Packmittelposten** der Packmittelverwaltung werden um den Bezug zur Warenannahme erweitert, damit sich jedes gebuchte Paket bis zur Warenannahmezeile zurückverfolgen lässt.

| Feld | Erläuterung |
|------|-------------|
| Warenannahmennr. | Nummer der Warenannahme, aus der das Paket stammt. Ermöglicht die Rückverfolgung eines Packmittelpostens bis zum ursprünglichen Wareneingangsbeleg. |
| Warenannahmenzeilennr. | Zeilennummer der Warenannahme, aus der das Paket stammt. Ermöglicht zusammen mit der **Warenannahmennr.** die zeilengenaue Zuordnung des Packmittelpostens. |

## Historie und Nachverfolgung

Eigene Historien- oder Logseiten legt diese App nicht an. Die Nachverfolgung erfolgt über die bestehenden Belege und Posten:

- Die **verarbeitete Warenannahme** dokumentiert die abgeschlossenen Warenannahmen samt ihrer Pakete und erlaubt den Nachdruck über **Packmittel drucken**.
- Die **Packmittelposten** zeigen über **Warenannahmennr.** und **Warenannahmenzeilennr.**, aus welcher Warenannahme ein Paket hervorgegangen ist.
- Im **Warenumlagerungseingang** ist der **Paketstatus** je Zeile ersichtlich, sodass sich offene und abgeschlossene Paketzuordnungen der Umlagerung verfolgen lassen.

## FAQ und Troubleshooting

### 1. Warum kann ich auf einer Komponentenzeile keine Packmittelreferenz auswählen?
Die **Packmittelreferenznr.** lässt sich nur eintragen, solange die Zeile den **Paketstatus** **(leer)** hat und die Zeilenmenge größer als 0 ist. Ist die Menge 0 oder der Artikel bereits einem Paket zugewiesen, meldet das System, dass die Referenz nicht gewählt werden kann. Prüfen Sie Menge und Paketstatus der Zeile.

### 2. Warum kann ich eine Komponentenzeile nicht mehr ändern?
Zeilen mit **Paketstatus** **Packmittel** sind gesperrt. Das System weist Änderungen mit dem Hinweis ab, dass Zeilen mit diesem Paketstatus nicht geändert werden können. Bearbeiten Sie stattdessen das Paket selbst oder setzen Sie die Zuordnung zurück.

### 3. Was bedeuten die Farben in der Spalte „Paketstatus“?
Die Farbe spiegelt den Zuordnungsgrad: **Voll** wird grün („günstig“) dargestellt, **Teilweise** gelb („mehrdeutig“) und **Packmittel** hervorgehoben. Der leere Status bleibt ohne Hervorhebung und bedeutet: noch keine Zuordnung.

### 4. Warum wird beim Verarbeiten kein Packmitteletikett gedruckt?
Steht in der **Warenvereinnahmung Einrichtung** das Feld **Packmittel drucken** auf **Kein Druck**, verarbeitet die Aktion die Warenannahme, druckt aber kein Etikett. Setzen Sie den Wert auf **Pro Packmittel** oder **Pro Packmittelgruppe**, damit der Bericht ausgeführt wird.

### 5. Welcher Bericht wird für den Packmitteldruck verwendet?
Der unter **Packmittel Beleg-ID** hinterlegte Bericht. Ist das Feld leer, setzt die App automatisch den mitgelieferten Bericht **Verarbeitete Warenannahme-Packmittel** ein — sowohl beim Öffnen der Einrichtung als auch beim Verarbeiten. Für ein eigenes Layout hinterlegen Sie dort Ihren Bericht.

### 6. Wie drucke ich Packmittel nachträglich, ohne erneut zu verarbeiten?
Öffnen Sie die **verarbeitete Warenannahme** und wählen Sie unter **Berichte** die Aktion **Packmittel drucken**. Damit werden die Etiketten der markierten Belege erneut ausgegeben, ohne die Warenannahme nochmals zu verarbeiten.

### 7. Warum erhalte ich bei der Verteilung „Pro Packmittelgruppe“ eine Fehlermeldung?
Bei der Verteilung **Pro Packmittelgruppe** darf die Warenannahmezeile nur **eine** Komponentenzeile besitzen, die nicht den Paketstatus **Packmittel** trägt. Bestehen mehrere solche Komponentenzeilen, bricht das System die Auswahl ab. Reduzieren Sie die offenen Komponenten oder bündeln Sie Mengen über Pakete.

### 8. Wann werden Pakete automatisch an eine Fertigungskomponente übergeben?
Nur wenn in der **Warenvereinnahmung Einrichtung** das Feld **Paket automatisch einer Komponente zuweisen** aktiviert ist. Dann übergibt die App beim Buchen des Warenannahme-Artikeljournals die physischen Pakete an die verknüpfte Fertigungsauftragskomponente. Ohne Kennzeichen unterbleibt die Übergabe.

### 9. Wie finde ich heraus, aus welcher Warenannahme ein gebuchtes Paket stammt?
Öffnen Sie die **Packmittelposten**. Die Felder **Warenannahmennr.** und **Warenannahmenzeilennr.** verweisen zeilengenau auf die ursprüngliche Warenannahme.

### 10. Warum unterscheidet sich die Paketmenge zwischen den neu erstellten Paketen?
Beim **Neues Paket erstellen** verteilt die App die zuzuweisende Menge gleichmäßig auf die Pakete und schlägt die verbleibende Restmenge dem **letzten** Paket zu. Dadurch kann das letzte Paket eine geringfügig andere Menge enthalten als die übrigen.

## Typische Anwendungsfälle

### Anwendungsfall 1: Wareneingang mit neuer Paketbildung und Etikettendruck

**Auslöser.** Im Lager trifft eine angekündigte Lieferung ein, deren Komponenten für einen Kundenauftrag verpackt und etikettiert werden sollen.

**Einstieg in BC.** Der Anwender öffnet über **Suchen** die **Warenannahme** und wählt den betreffenden Beleg. Voraussetzung: In der **Warenvereinnahmung Einrichtung** ist **Packmittel drucken** auf **Pro Packmittel** gesetzt (siehe **Einrichtung**).

**Kernablauf.**
1. Der Anwender öffnet die Komponentenzeilen und prüft die Spalte **Paketstatus** — die Zeilen stehen auf **(leer)**.
2. Auf der Zeile wählt er **Neues Paket erstellen**; die App bildet die Pakete und verteilt die Menge. Der **Paketstatus** wechselt auf **Voll** oder **Teilweise**, die **Gesamtanzahl Packmittel** steigt entsprechend.
3. Zurück in der **Warenannahme** wählt der Anwender **Wareneingang verarbeiten und Packmittel drucken** und bestätigt den Dialog.

**Abschluss.** Nach dem Verarbeiten druckt die App den Bericht **Verarbeitete Warenannahme-Packmittel** je Paket. Die Pakete sind anschließend in der **verarbeiteten Warenannahme** und in den **Packmittelposten** (mit **Warenannahmennr.**) nachvollziehbar.

### Anwendungsfall 2: Verpacken nach hinterlegter Vorschrift (Packmittelreferenz)

**Auslöser.** Für einen Debitor gilt eine feste Verpackungsvorschrift; die eingehende Ware soll genau danach paketiert werden.

**Einstieg in BC.** Der Anwender öffnet die **Warenannahme** und deren Komponentenzeilen.

**Kernablauf.**
1. Er trägt in der Komponentenzeile die **Packmittelreferenznr.** ein (nur möglich bei Paketstatus **(leer)** und Menge > 0). Die App prüft die Referenz anhand von Artikel, Variante, Menge und Debitor.
2. Anschließend wählt er die Zeilenaktion **Von Packmittelreferenz erstellen**; die Pakete entstehen gemäß Vorschrift, gleichartige Paketkomponenten werden zusammengefasst.
3. Der Anwender verarbeitet den Beleg über **Wareneingang verarbeiten und Packmittel drucken**.

**Abschluss.** Die vorschriftsgemäß gebildeten Pakete werden gedruckt und stehen in der verarbeiteten Warenannahme sowie in den **Packmittelposten** zur Verfügung.

### Anwendungsfall 3: Umlagerung von Rohmaterial mit übernommenen Paketen

**Auslöser.** Aus einer verarbeiteten Warenannahme entsteht ein Umlagerungsauftrag, um Rohmaterial an einen anderen Lagerort zu bringen; die bereits gebildeten Pakete sollen erhalten bleiben.

**Einstieg in BC.** Der Anwender öffnet den **Warenumlagerungseingang** der Warenvereinnahmung.

**Kernablauf.**
1. Beim Erzeugen des Umlagerungsauftrags übergibt die App die physischen Pakete des Warenannahmebelegs automatisch als Belegpakete des Umlagerungsversands.
2. Der Anwender ruft die Umlagerungszeilen ab; der **Paketstatus** wird aus der Umlagerungszeile übernommen und je Zeile angezeigt. Über die Infobox **Komponenten Packmittelstruktur** prüft er die Paketstruktur.
3. Bei Bedarf ordnet er über die Zeilenaktion **Paketzuordnung – Wareneingang** eingehende Ware einem Paket zu.

**Abschluss.** Der Warenumlagerungseingang zeigt den korrekten **Paketstatus** je Zeile; die Pakete bleiben durchgängig zugeordnet und in den **Packmittelposten** nachverfolgbar.
