---
title: Anwenderhandbuch m+m Test Certificate Management
---

# Anwenderhandbuch m+m Test Certificate Management

Dieses Handbuch beschreibt die Bedienung des Moduls **m+m Test Certificate Management** (Prüfdaten) in Microsoft Dynamics 365 Business Central. Es richtet sich an Anwenderinnen und Anwender, die im Tagesgeschäft mit Prüfungen, Proben, Prüfzeugnissen und den zugehörigen Belegen arbeiten, sowie an Key-User und Administratoren, die das Modul einrichten. Alle Feld-, Seiten- und Aktionsbezeichnungen entsprechen der deutschen Oberfläche von Business Central.

---

## 1. Einleitung

### Zweck des Moduls

Mit dem Modul **Prüfdaten** erfassen und dokumentieren Sie Qualitätsprüfungen zu Artikeln, Arbeitsplätzen und Arbeitsplatzgruppen sowie zu Belegen aus Einkauf, Verkauf, Lager und Fertigung. Für jede Prüfung legen Sie eine oder mehrere **Proben** an, erfassen zu jeder Probe die **Probenwerte** einzelner Prüfeigenschaften und geben die Prüfung anschließend frei. Aus freigegebenen Prüfungen erzeugen Sie ein druck- und versandfähiges **Prüfzeugnis**.

Das Modul steuert darüber hinaus den **Prüfstatus** auf den Belegzeilen (z. B. Verkaufs-, Einkaufs- und Lagerbelege), sperrt bei Bedarf Bestände über einen **Quarantäne**-Lagerort und erzeugt Prüfungen bei bestimmten Ereignissen automatisch über **Prüfregeln**.

### Zielgruppe

Primäre Zielgruppe sind **operative Anwender** in Wareneingang, Qualitätssicherung, Fertigung und Verkauf, die täglich Proben erfassen, Prüfwerte eingeben, Prüfungen freigeben und Prüfzeugnisse drucken oder versenden. Sekundär richtet sich das Handbuch an **Administratoren und Key-User**, die die **Prüfdaten Einrichtung**, die Stammdaten (Normen, Prüfeigenschaften, Prüfgruppen, Prüfvorlagen) und die **Prüfregeln** pflegen.

### Kurzer Prozessüberblick

Der typische Ablauf im Modul verläuft in folgender Reihenfolge:

1. **Einrichtung** – Ein Administrator hinterlegt in der **Prüfdaten Einrichtung** die Nummernserien, die Quarantäne-Einstellungen und die Berichtsoptionen und legt die Prüfdatenbenutzer und -benutzergruppen an.
2. **Stammdaten** – Key-User pflegen **Normen**, **Prüfeigenschaften**, **Prüfgruppen** und **Prüfvorlagen** (die Vorlagen bestimmen, welche Eigenschaften eine Prüfung enthält).
3. **Regeln (optional)** – Über **Prüfregeln** wird festgelegt, bei welchem Ereignis (z. B. Freigabe eines Auftrags) automatisch eine Prüfung nach einer Prüfvorlage erzeugt wird.
4. **Tägliche Arbeit** – Der Anwender erstellt eine **Prüfung** (manuell oder automatisch), legt **Proben** an, erfasst die **Probenwerte** und gibt die Proben sowie die Prüfung frei.
5. **Ausgabe** – Aus der freigegebenen Prüfung entsteht ein **Prüfzeugnis**, das gedruckt oder per **E-Mail** versendet wird. Benachrichtigungen und Historienlisten dokumentieren den Ablauf.

### Navigation und Einstieg

Alle Prüfdaten-Funktionen sind in jedem Rollencenter über das Menüband unter der Gruppe **Prüfdatenverwaltung** erreichbar. Diese Gruppe enthält die Untergruppe **Verwaltung** (Einrichtung und Stammdaten), die Listen **Prüfungen**, **Prüfregeln** und **Prüfdaten Regelfilterliste** sowie die Gruppe **Berichte und Aufgaben** mit **Prüfzeugnisse**, **Prüfdaten Benachrichtigungsposten** und **Prüfdaten Benachrichtigungsverlauf**. Verwaltungsseiten sind zusätzlich über die **Suche** auffindbar; im Tagesgeschäft ist jedoch der Weg über das Menüband **Prüfdatenverwaltung** der vorgesehene Einstieg.

---

## 2. Schnellstart für Anwender

Der Schnellstart zeigt den kürzesten Weg vom eingerichteten System bis zum fertigen Prüfzeugnis. Die Einrichtung (Schritt A) erfolgt einmalig durch einen Administrator, bevor Anwender produktiv arbeiten.

**A. Einrichtung (einmalig, Administrator).**
1. Öffnen Sie über **Prüfdatenverwaltung → Verwaltung → Prüfdaten Einrichtung** die Einrichtungskarte und wählen Sie **Erstanlage ausführen**. Dadurch werden die Basisdaten des Moduls angelegt.
2. Hinterlegen Sie unter **Nummerierung** die Nummernserien für Prüfvorlagen, Prüfungen, Proben und Regeln.
3. Legen Sie unter **Prüfdatenverwaltung → Prüfdaten Benutzer** die Prüfdatenbenutzer an und markieren Sie in den **Prüfdatenbenutzergruppen** mindestens einen Benutzer als Benutzer mit Qualitätssicherungsrecht.

**B. Stammdaten (Key-User).**
4. Pflegen Sie **Normen**, **Prüfeigenschaften** und **Prüfgruppen**.
5. Legen Sie eine **Prüfvorlage** an, übernehmen Sie mit **Prüfgruppeneigenschaften übernehmen** die Eigenschaften einer Prüfgruppe, setzen Sie **Gültig von**/**Gültig bis** und aktivieren Sie die Vorlage mit **Vorlagen aktivieren**.

**C. Tägliche Arbeit (Anwender).**
6. Erstellen Sie eine **Prüfung** – entweder automatisch über eine aktive **Prüfregel**, oder manuell über die Aktion **Prüfung für Artikel erstellen** auf der Artikelkarte bzw. **Testzertifikat-Muster öffnen** auf einer Belegzeile, oder direkt über **Prüfungen → Neu** und Auswahl einer Prüfvorlage.
7. Wählen Sie auf der **Prüfungskarte** die Aktion **Neue Probe** (eine Probe) oder **Mehrere Proben erstellen** (mehrere Proben).
8. Öffnen Sie die **Probenkarte**, holen Sie mit **Serien/Chargen-Nr. vom Beleg holen** die Chargennr./Seriennr. und erfassen Sie im Wertegitter die **Probenwerte** je Prüfeigenschaft.
9. Wählen Sie auf der Probe **Freigeben** (bzw. auf der Probenliste **Alle Proben freigeben**). Die Probe erhält den Status **Freigegeben**.
10. Wählen Sie auf der **Prüfungskarte** **Freigeben**. Sind noch offene Proben vorhanden, meldet Business Central, dass zuerst alle Proben freigegeben werden müssen. Nach der Freigabe wird – abhängig von der Einrichtung – automatisch ein **Prüfzeugnis** erzeugt.
11. Öffnen Sie das **Prüfzeugnis**, wählen Sie bei Bedarf **Probenwerte auswählen** und anschließend **Beleg drucken** oder **E-Mail senden**.

Wird eine Prüfung noch einmal geändert, setzen Sie sie mit **Status zurücksetzen** wieder auf **Offen** (bei entsprechender Einrichtung nur durch einen Benutzer mit Qualitätssicherungsrecht möglich).

---

## 3. Berechtigungen und Prüfdatenbenutzer

Das Modul unterscheidet Anwender anhand eines **Qualitätssicherungsrechts**. Viele steuernde Aktionen (Regeln aktivieren, Vorlagen und Mailvorlagen bearbeiten, Prüfzeugnisse erneut drucken oder löschen, gesperrte Quarantänebestände buchen, Prüfungen wieder öffnen) sind ausschließlich Benutzern mit diesem Recht vorbehalten. Legen Sie daher die Prüfdatenbenutzer und -benutzergruppen ein, bevor Anwender produktiv arbeiten.

### 3.1 Prüfdatenbenutzer

**Einstieg:** Öffnen Sie über **Prüfdatenverwaltung → Prüfdaten Benutzer** die Liste **Prüfdatenbenutzer**.

Wer pflegt dies: der Administrator, vor der ersten Nutzung. Jeder Anwender, der Benachrichtigungen erhalten soll oder als Prüfer geführt wird, wird hier hinterlegt.

| Feld | Erläuterung |
|---|---|
| Benutzer-ID | Wenn Sie hier einen Business-Central-Benutzer auswählen, dann wird dieser Benutzer als Prüfdatenbenutzer geführt und kann Benachrichtigungen empfangen sowie in Prüfregeln und Prüfzeugnissen als Empfänger bzw. Prüfer verwendet werden. |
| Benachrichtigungsmethode | Legt fest, auf welchem Weg der Benutzer über Prüfdatenereignisse informiert wird. **Email:** Der Benutzer erhält eine E-Mail (über den Bericht Notification Email). **Benachrichtigung:** Der Benutzer erhält eine interne Business-Central-Benachrichtigung als Benachrichtigungsposten. |

Über die Aktion **Benachrichtigungsplan** öffnen Sie zu einem markierten Benutzer den zugehörigen **Benachrichtigungsplan** (siehe Kapitel 9), in dem Sie Rhythmus und Uhrzeit der Benachrichtigungen festlegen.

### 3.2 Prüfdatenbenutzergruppen und Qualitätssicherungsrecht

**Einstieg:** Öffnen Sie über **Prüfdatenverwaltung → Prüfdaten Benutzergruppe** die Liste **Prüfdatenbenutzergruppen** und öffnen Sie eine Gruppe per Zeile, um zur Karte zu gelangen.

Prozess: Der Administrator gruppiert die Prüfdatenbenutzer und bestimmt je Gruppenmitglied, ob es das Qualitätssicherungsrecht besitzt. Das Recht bestimmt die Berechtigungen für alle steuernden Aktionen des Moduls.

| Feld | Erläuterung |
|---|---|
| Benutzergruppencode | Eindeutiger Code der Prüfdatenbenutzergruppe. Wenn Sie eine Gruppe anlegen, dann können Sie ihr anschließend Mitglieder zuordnen und über die Prüfgruppenzuordnung steuern, welche Prüfgruppen die Mitglieder sehen. |
| Beschreibung | Klartextbezeichnung der Gruppe für die Auswahl in Listen. |

Auf der Karte pflegen Sie im Unterformular **Prüfdatenbenutzergruppenmitglieder** die Mitglieder:

| Feld | Erläuterung |
|---|---|
| Benutzer-ID | Ordnet einen Prüfdatenbenutzer der Gruppe zu. Wenn ein Benutzer Mitglied ist, dann werden ihm über die Gruppe Prüfgruppen-Sichten und – bei gesetztem Kennzeichen – Qualitätssicherungsrechte zugewiesen. |
| Qualitätssicherung | Wenn dieses Kennzeichen gesetzt ist, dann darf der Benutzer die steuernden Aktionen des Moduls ausführen: Prüfregeln aktivieren/deaktivieren/kopieren, Prüfvorlagen und Mailvorlagen bearbeiten, Benutzergruppen pflegen, bereits gedruckte Prüfzeugnisse löschen sowie Buchungen auf Quarantäne-Lagerorten und -Lagerplätzen durchführen. Ist das Kennzeichen bei keinem Mitglied gesetzt, behandelt das Modul die Gruppe als frei bearbeitbar und ergänzt beim Anlegen automatisch mindestens einen Benutzer mit Qualitätssicherungsrecht, damit stets ein Verantwortlicher existiert. |

Hinweis zur Berechtigung: Das Modul liefert den Berechtigungssatz **MuM TC Permission** mit, der die Datenzugriffsrechte auf die Prüfdatenobjekte umfasst. Das Qualitätssicherungsrecht aus der Benutzergruppe steuert zusätzlich – unabhängig vom Berechtigungssatz – die oben genannten fachlichen Aktionen.

---

## 4. Einrichtung

Die **Prüfdaten Einrichtung** ist die zentrale, unternehmensweite Einrichtungskarte des Moduls (ein Datensatz je Mandant). Sie ist das umfangreichste Konfigurationsobjekt und sollte vollständig gepflegt werden, bevor Anwender arbeiten.

**Einstieg:** **Prüfdatenverwaltung → Verwaltung → Prüfdaten Einrichtung**. Die Karte ist zusätzlich über die **Suche** auffindbar. Die Felder sind nur für Benutzer mit Qualitätssicherungsrecht bearbeitbar.

Vor der ersten Nutzung führen Sie die Aktion **Erstanlage ausführen** aus; sie legt die notwendigen Basisdaten des Moduls an. Mit **Quarantäne-Lagerplatz einrichten** werden die Quarantäne-Lagerplätze angelegt und anschließend die Lagerplätze angezeigt.

### 4.1 Allgemeine Einstellungen

Diese Einstellungen steuern das grundsätzliche Verhalten von Prüfungen und Proben im Tagesgeschäft.

| Einrichtung | Erläuterung |
|---|---|
| Zertifikat kann nur von QS-Benutzer wieder geöffnet werden | Wenn aktiviert, dann kann eine bereits freigegebene Prüfung nur von einem Benutzer mit Qualitätssicherungsrecht über **Status zurücksetzen** wieder geöffnet werden; andere Benutzer erhalten eine Fehlermeldung. So bleibt die Freigabe kontrolliert. |
| Regel ignorieren bei manueller Erstellung | Wenn aktiviert, dann werden beim manuellen Anlegen einer Prüfung die Prüfregeln nicht angewendet; der Anwender wählt Vorlage und Zuordnung selbst. Ohne das Kennzeichen greifen auch bei manueller Erstellung die Regelvorgaben. |
| Automatische Probenerstellung | Wenn aktiviert, dann erzeugt das Modul beim Anlegen einer Prüfung automatisch die vorgesehene Anzahl Proben, sodass der Anwender direkt mit der Werteerfassung beginnen kann. |
| Warnung vor Änderung des Fertigungsstatus | Wenn aktiviert, dann warnt Business Central, bevor der Status eines Fertigungsauftrags geändert wird, zu dem eine Prüfung existiert – so gehen keine Prüfbezüge unbemerkt verloren. |
| Beschriftung Vorgabewert 1 | Legt die Spaltenüberschrift fest, unter der der erste Vorgabewert einer Prüfeigenschaft in Vorlagen, Prüfungen und Proben angezeigt wird. Wenn Sie hier einen Text hinterlegen, dann erscheint dieser überall statt der Standardbezeichnung „Vorgabewert 1". |
| Beschriftung Vorgabewert 2 | Legt analog die Spaltenüberschrift für den zweiten Vorgabewert fest. |
| Chargennr. sperren | Wenn aktiviert, dann wird die zu einer Prüfung gehörende Charge im Bestand gesperrt, solange die Prüfung nicht freigegeben ist; die Charge kann dann erst nach erfolgreicher Prüfung weiterverwendet werden. |
| Wiedereröffnen verarbeiteter Proben zulassen | Wenn aktiviert, dann darf eine bereits als „verarbeitet" markierte Probe wieder geöffnet werden. Ohne das Kennzeichen ist das Wiederöffnen verarbeiteter Proben blockiert und Business Central meldet dies beim Versuch. |
| Verarbeitete Probe bearbeitbar | Wenn aktiviert, dann bleiben die Felder einer als verarbeitet markierten Probe editierbar. Ohne das Kennzeichen sperrt das Modul verarbeitete Proben gegen Änderungen und setzt das Verarbeitet-Kennzeichen automatisch bei Freigabe bzw. Wiedereröffnung. |
| Aktivierungskennzeichen per Stapelverarbeitung aktualisieren | Wenn aktiviert, dann wird die zeitgesteuerte Aktivierung/Deaktivierung von Prüfvorlagen und Regeln über die Aufgabenwarteschlange aktualisiert, statt nur beim Öffnen der Listen. So bleiben Gültigkeiten auch ohne manuelles Öffnen aktuell. |

### 4.2 Quarantäne-Einrichtung

Die Quarantäne sperrt geprüfte, aber noch nicht freigegebene Bestände. Sie benötigen einen Quarantäne-Lagerort bzw. -Lagerplatz sowie – je nach Lagerkomplexität – die Buchungs- und Lagerplatzart-Einstellungen. Diese Konfiguration greift im Tagesgeschäft in Kapitel 8 (Belegintegration und Lager).

**Einstieg für die Lagerplatzanlage:** Aktion **Quarantäne-Lagerplatz einrichten** auf dieser Karte.

| Einrichtung | Erläuterung |
|---|---|
| Quarantäne-Lagerort | Wenn Sie einen Lagerort hinterlegen, dann werden geprüfte Bestände dorthin umgebucht und für die weitere Verwendung gesperrt, bis die Prüfung freigegeben ist. Auswählbar sind nur Lagerorte ohne organisierte Lagerhaltung und ohne Lagerplatzpflicht. |
| Quarantäne Lagerplatzcode | Legt den konkreten Lagerplatz innerhalb des Quarantäne-Lagerorts fest, auf den gesperrte Bestände gebucht werden. |

**Buchen.** Diese Optionen steuern, ob und wie Bestände automatisch in die Quarantäne gebucht werden.

| Einrichtung | Erläuterung |
|---|---|
| Artikel automatisch in Quarantäne buchen | Wenn aktiviert, dann bucht das Modul den zu prüfenden Bestand automatisch auf den Quarantäne-Lagerplatz, sobald die Prüfung angelegt wird; der Anwender muss die Sperrung nicht manuell auslösen. |
| Vor Buchung in Quarantäne nachfragen | Wenn aktiviert, dann erscheint vor der automatischen Quarantänebuchung eine Rückfrage, sodass der Anwender die Umlagerung bestätigen kann. |
| Quarantäne-Buchungszeilen sperren | Wenn aktiviert, dann können Belegzeilen mit Quarantänebestand nicht regulär gebucht werden, solange die Prüfung nicht freigegeben ist – der Bestand ist damit gegen versehentliche Verwendung geschützt. |
| Quarantänewarnung vor Validierung des Probenwerts aktivieren | Wenn aktiviert, dann weist Business Central vor dem Bestätigen eines Probenwerts darauf hin, dass sich der Bestand in Quarantäne befindet, sodass der Prüfer die Sperrung berücksichtigt. |

**Erweiterte Lagerhaltung.** Diese Codes werden benötigt, wenn der Quarantäne-Lagerort mit organisierter Lagerhaltung (Zonen und Lagerplatzarten) betrieben wird.

| Einrichtung | Erläuterung |
|---|---|
| Quarantäne Zonencode | Legt die Zone fest, in der die Quarantäne-Lagerplätze eines Lagerorts mit organisierter Lagerhaltung liegen. |
| Quarantäne Lagerplatzartencode | Bestimmt die allgemeine Lagerplatzart, die beim Anlegen der Quarantäne-Lagerplätze verwendet wird. |
| Quarantäne Lagerplatzartencode Wareneingang | Bestimmt die Lagerplatzart, die für den Wareneingang in die Quarantäne genutzt wird. |
| Quarantäne Lagerplatzartencode Warenausgang | Bestimmt die Lagerplatzart für den Warenausgang aus der Quarantäne. |
| Quarantäne Lagerplatzartencode Einlagerung | Bestimmt die Lagerplatzart für die Einlagerung in die Quarantäne. |
| Quarantäne Lagerplatzartencode Kommissionierung | Bestimmt die Lagerplatzart für die Kommissionierung aus der Quarantäne. |

### 4.3 Nummerierung

Ohne Nummernserien lassen sich Vorlagen, Prüfungen, Proben und Regeln nicht anlegen. Legen Sie die Serien vor der ersten Nutzung an.

| Einrichtung | Erläuterung |
|---|---|
| Nummernserie Prüfvorlagen | Wenn Sie hier eine Nummernserie hinterlegen, dann erhalten neue Prüfvorlagen automatisch eine fortlaufende Nummer aus dieser Serie. |
| Nummernserie Prüfungen | Bestimmt die Nummernserie für neue Prüfungen. Ohne diese Serie kann keine Prüfung angelegt werden (Business Central prüft das Feld beim Anlegen). |
| Nummernserie Proben | Bestimmt die Nummernserie für neue Proben. |
| Nummernserie Prüfregeln | Bestimmt die Nummernserie für neue Prüfregeln. |

### 4.4 Bericht

Diese Einstellungen steuern das Layout und die automatische Erstellung des Prüfzeugnisses (siehe Kapitel 9).

| Einrichtung | Erläuterung |
|---|---|
| Nummernserie Prüfzeugnis | Bestimmt die Nummernserie für neue Prüfzeugnisse. |
| Logoposition auf Belegen | Legt fest, wo das Firmenlogo auf dem gedruckten Prüfzeugnis erscheint. **Kein Logo:** ohne Logo. **Links / Mitte / Rechts:** Das Logo wird an der gewählten Position im Belegkopf ausgegeben. |
| Bildreferenzsymbol | Legt das Zeichen fest, mit dem im Zeugnis auf ein hinterlegtes Bild einer Prüfeigenschaft verwiesen wird. Wenn Sie hier ein Symbol setzen, dann erscheint es an den Wertstellen mit Medienbezug. |
| Prüfzeugnis automatisch erstellen | Wenn aktiviert, dann erzeugt das Modul bei der Freigabe einer Prüfung automatisch das zugehörige Prüfzeugnis; ohne das Kennzeichen legt der Anwender das Prüfzeugnis manuell an. |

### 4.5 Stapelverarbeitung (Aufgabenwarteschlange)

| Einrichtung | Erläuterung |
|---|---|
| Aufgabenwarteschlange bei Fehler neu starten | Wenn aktiviert, dann startet das Modul einen fehlgeschlagenen Aufgabenwarteschlangenposten der regelbasierten Verarbeitung nach der eingestellten Wartezeit automatisch neu. Beim Aktivieren wird die Wartezeit auf 60 Minuten vorbelegt, falls sie noch 0 beträgt. |
| Aufgabenwarteschlange nach Anzahl Minuten neu starten | Legt die Wartezeit (in Minuten) bis zum automatischen Neustart fest. Das Feld ist nur bearbeitbar, wenn der Neustart bei Fehler aktiviert ist. |

---

## 5. Stammdaten

Die Stammdaten definieren, **was** geprüft wird. Sie werden von Key-Usern mit Qualitätssicherungsrecht gepflegt. Reihenfolge in der Praxis: zuerst **Normen**, **Prüfeigenschaften** und ggf. **Lookups**, dann **Prüfgruppen** (Bündel von Eigenschaften), schließlich **Prüfvorlagen** (die konkrete Zusammenstellung, die eine Prüfung erhält). Die Prüfvorlage ist das Bindeglied zur täglichen Arbeit (Kapitel 7) und zu den Regeln (Kapitel 6).

### 5.1 Normen

**Einstieg:** **Prüfdatenverwaltung → Verwaltung → Normen**.

Prozess: Der Key-User hinterlegt die Prüfnormen, die später einer Prüfvorlage über die **Normzuweisung** zugeordnet und auf dem Prüfzeugnis ausgewiesen werden.

| Feld | Erläuterung |
|---|---|
| Code | Eindeutiger Code der Norm. Wenn Sie eine Norm anlegen, dann steht sie in Prüfvorlagen und Prüfungen zur Auswahl und kann auf dem Prüfzeugnis gedruckt werden. |
| Beschreibung | Klartextbezeichnung der Norm. Über die Aktion **Übersetzung** hinterlegen Sie sprachabhängige Bezeichnungen, sodass das Prüfzeugnis in der Sprache des Empfängers ausgegeben werden kann. |

### 5.2 Prüfeigenschaften

**Einstieg:** **Prüfdatenverwaltung → Verwaltung → Prüfeigenschaften**.

Prozess: Eine **Prüfeigenschaft** ist ein einzelnes Merkmal, das später in einer Probe bewertet wird (z. B. ein Messwert). Der Key-User legt die Eigenschaften an; über Prüfgruppen und Prüfvorlagen fließen sie in die Prüfungen ein.

| Feld | Erläuterung |
|---|---|
| Nr. | Fortlaufende Nummer der Prüfeigenschaft. |
| Beschreibung | Bezeichnung der Eigenschaft; sie darf nicht leer sein und erscheint als Zeilenbezeichnung in Vorlagen, Prüfungen und Proben. Über die Aktion **Übersetzung** pflegen Sie sprachabhängige Bezeichnungen. |
| Datenart | Legt fest, welche Art von Wert für diese Eigenschaft erfasst wird. **Text:** freier Text. **Ganzzahl:** ganzzahliger Wert. **Dezimal:** Dezimalzahl (numerische Prüfung). **Medium:** ein Bild/Medienobjekt. Wenn bereits Werte zu dieser Eigenschaft existieren, kann die Datenart nicht mehr geändert werden. |
| Referenzart | Bestimmt, ob der Eingabewert gegen eine hinterlegte Werteliste geprüft wird. **(leer):** freie Eingabe gemäß Datenart. **Tabelle:** Der Wert muss ein gültiger Eintrag aus einem Lookup sein. |
| Referenzwert | Verweist bei Referenzart **Tabelle** auf den zugehörigen Lookup (siehe 5.3). Wenn Sie hier einen Lookup wählen, dann sind bei der Werteerfassung nur die dort definierten Werte zulässig. |
| Medium | Nimmt ein Standardbild zur Eigenschaft auf. Über **Medien importieren** laden Sie ein Bild, über **Medien anzeigen** öffnen Sie es. |
| Medium vorhanden | Zeigt an, ob zur Eigenschaft ein Bild hinterlegt ist. |

### 5.3 Lookups für Prüfeigenschaften

**Einstieg:** **Prüfdatenverwaltung → Verwaltung → Lookups für Prüfeigenschaften**. Die zugehörigen Werte öffnen Sie über die Aktion **Wert** in der Zeile.

Prozess: Ein Lookup ist eine geschlossene Werteliste, die einer Prüfeigenschaft mit Referenzart **Tabelle** zugeordnet wird. So stellen Sie sicher, dass Prüfer nur zulässige Werte erfassen.

| Feld | Erläuterung |
|---|---|
| Code | Eindeutiger Code der Lookup-Art. Wenn Sie eine Lookup-Art anlegen, dann kann sie als Referenzwert einer Prüfeigenschaft dienen. |
| Beschreibung | Bezeichnung der Lookup-Art. |

Zu jeder Lookup-Art pflegen Sie die zulässigen Werte (Seite **Prüfdaten Look-Up-Werte**):

| Feld | Erläuterung |
|---|---|
| Lookup-Wert | Ein zulässiger Wert der Lookup-Art. Wenn Sie Werte hinterlegen, dann kann der Prüfer bei der Werteerfassung nur aus dieser Liste wählen. |
| Beschreibung | Erläuterung des Werts. Über die Aktion **Übersetzung** hinterlegen Sie sprachabhängige Bezeichnungen. |

### 5.4 Prüfgruppen

**Einstieg:** **Prüfdatenverwaltung → Verwaltung → Prüfgruppen**. Die zugeordneten Eigenschaften öffnen Sie über die Aktion **Eigenschaftszuweisung**.

Prozess: Eine **Prüfgruppe** bündelt mehrere Prüfeigenschaften und bestimmt deren Druckform. Prüfgruppen werden anschließend in Prüfvorlagen übernommen (siehe 5.5) und steuern zugleich, welche Prüfgruppen ein Benutzer über seine Benutzergruppe sehen darf.

| Feld | Erläuterung |
|---|---|
| Code | Eindeutiger Code der Prüfgruppe. Wenn Sie eine Prüfgruppe anlegen, dann kann sie einer Prüfvorlage zugeordnet und ihren Mitgliedern über die Benutzergruppe zugewiesen werden. Ein Code, der bereits in Prüfungs- oder Vorlagenzeilen verwendet wird, kann nicht gelöscht werden. |
| Beschreibung | Bezeichnung der Prüfgruppe. Über die Aktion **Übersetzung** pflegen Sie sprachabhängige Bezeichnungen. |
| Druckart | Legt fest, wie die Eigenschaften der Gruppe auf dem Prüfzeugnis erscheinen. **(leer):** keine besondere Druckform. **Zeilen:** je Eigenschaft eine Zeile. **Spalten:** die Eigenschaften nebeneinander in Spalten. **Textblock:** ein zusammenhängender Textblock (Inhalt aus dem Feld Textblocktext). |
| Textblocktext | Nimmt bei Druckart **Textblock** den auszugebenden Text auf. |

Über **Eigenschaften kopieren von** übernehmen Sie die Eigenschaftszuweisung einer bestehenden Prüfgruppe in die aktuelle, um vergleichbare Gruppen schnell aufzubauen.

### 5.5 Prüfvorlagen

**Einstieg:** **Prüfdatenverwaltung → Verwaltung → Prüfvorlagen** (Liste), Öffnen einer Zeile führt zur **Prüfvorlage Karte**.

Prozess: Die **Prüfvorlage** ist die konkrete Zusammenstellung von Prüfgruppen und -eigenschaften mit ihren Vorgabewerten, die eine Prüfung erhält. Vorlagen sind **versioniert** und über **Gültig von**/**Gültig bis** zeitlich gesteuert. Eine Prüfung, ein Artikel oder eine Regel verweist stets auf eine Vorlage; die tägliche Arbeit (Kapitel 7) und die Regeln (Kapitel 6) konsumieren die Vorlage.

**Kopf der Prüfvorlage:**

| Feld | Erläuterung |
|---|---|
| Nr. | Nummer der Prüfvorlage aus der Nummernserie. Mehrere Versionen teilen sich dieselbe Nr. und unterscheiden sich über den Versionscode. |
| Versionscode | Code der Vorlagenversion. Wenn Sie mehrere Versionen führen, dann ist stets die Version aktiv, deren Gültigkeitszeitraum das Arbeitsdatum umfasst. |
| Beschreibung | Bezeichnung der Vorlage. |
| Erstellungsdatum | Anlagedatum der Version (wird automatisch gesetzt). |
| Gültig von | Beginn des Gültigkeitszeitraums (Pflichtfeld). Wenn das Arbeitsdatum in den Zeitraum fällt, dann kann die Version aktiviert werden. |
| Gültig bis | Ende des Gültigkeitszeitraums (Pflichtfeld). Das Modul verhindert überlappende Gültigkeitszeiträume mehrerer Versionen derselben Vorlage und meldet ein Datum, das vor „Gültig von" liegt. |
| Aktiv | Zeigt an, ob die Version aktiv ist. Wenn eine Version aktiv wird, dann werden andere Versionen derselben Nr. deaktiviert und die verknüpften Prüfregeln übernehmen den Gültigkeitszeitraum. Wird die Vorlage inaktiv, so deaktiviert das Modul die zugehörige Regel und vermerkt dies in deren Beschreibung. |
| Probendatenbefüllung | Legt fest, wie neue Proben mit Werten vorbelegt werden (Übernahme der Vorgabewerte bzw. der zuletzt erfassten Probenwerte). |
| Standardwerte anzeigen | Wenn aktiviert, dann werden im Wertegitter der Probe die Vorgabewerte (Vorgabewert 1/2) als eigene Spalten eingeblendet, damit der Prüfer den Sollwert sieht. |
| Anzahl Proben | Legt fest, wie viele Proben beim Anlegen einer Prüfung standardmäßig erzeugt werden. |

**Zeilen der Prüfvorlage** (Unterformular **Prüfvorlagen SubPage**):

| Feld | Erläuterung |
|---|---|
| Prüfgruppencode | Ordnet die Zeile einer Prüfgruppe zu. |
| Charakteristik-Nr. | Verweist auf die Prüfeigenschaft innerhalb der Prüfgruppe. |
| Prüfgruppenbeschreibung | Bezeichnung der Prüfgruppe (Anzeige). |
| Charakteristikbeschreibung | Bezeichnung der Prüfeigenschaft (Anzeige). |
| Vorgabewert 1 | Sollwert bzw. Standardwert 1 der Eigenschaft. Wenn Sie einen Vorgabewert setzen, dann wird er bei der Probenerstellung vorbelegt; bei Referenzart Tabelle wird er gegen den Lookup geprüft, bei numerischer Datenart als Zahl ausgewertet. Die Spaltenüberschrift entspricht der Beschriftung aus der Einrichtung (4.1). |
| Vorgabewert 2 | Sollwert 2 der Eigenschaft (z. B. oberer Grenzwert), analog zu Vorgabewert 1. |
| Datenart | Zeigt die Datenart der Eigenschaft (Text, Ganzzahl, Dezimal, Medium). |
| Drucken | Wenn aktiviert, dann wird die Zeile auf dem Prüfzeugnis gedruckt. |
| Prüfung | Wenn aktiviert, dann wird die Zeile beim Erzeugen einer Prüfung aus der Vorlage übernommen. Nur Zeilen mit gesetztem Kennzeichen fließen in die Prüfung ein. |

**Prozessschritte Prüfvorlage einrichten:**
1. Zuerst legen Sie den Vorlagenkopf mit **Nr.**, **Versionscode**, **Gültig von**/**Gültig bis** an.
2. Danach übernehmen Sie mit **Prüfgruppeneigenschaften übernehmen** die Eigenschaften einer Prüfgruppe in die Vorlagenzeilen und passen die **Vorgabewerte** an.
3. Über **Normzuweisung** ordnen Sie der Vorlage die zu druckenden Normen zu (Feld **Norm im Unterschriftsbereich drucken** je Zuordnung).
4. Schließlich aktivieren Sie die Version über **Vorlagen aktivieren** (in der Vorlagenliste). Erst eine aktive Vorlage kann von Prüfungen und Regeln verwendet werden.

Über **Bemerkung** hinterlegen Sie Kopf- und Zeilenbemerkungen zur Vorlage.

### 5.6 Prüfdaten-Mailvorlagen

**Einstieg:** **Prüfdatenverwaltung → Prüfdaten Mailvorlagen** (Liste), Öffnen einer Zeile führt zur **Prüfdaten Mailvorlagenkarte**.

Prozess: Eine **Mailvorlage** definiert Betreff und Text der E-Mail, die bei einer Prüfdatenantwort (Regel-Response) versendet wird. Der Text enthält Platzhalter, die beim Versand mit den konkreten Prüf- und Belegdaten gefüllt werden. Mailvorlagen werden je Prüfdatenantwort und Kategorie angelegt und im Regel-/Benachrichtigungsprozess (Kapitel 6/9) konsumiert.

| Feld | Erläuterung |
|---|---|
| Betreffcode | Verweist auf die Prüfdatenantwort, zu der die Mailvorlage gilt. Wenn Sie den Code wählen, dann werden Kategorie, Beschreibung und Betreff übernommen. |
| Betrefftext | Betreffzeile der E-Mail, mit optionalen Platzhaltern. |
| Kategorie | Prüfdatenkategorie, für die die Vorlage gilt (Anzeige). |
| Beschreibung | Bezeichnung der Mailvorlage (Anzeige). |

Im Unterformular **Prüfdaten Mailvorlage** erfassen Sie die Textzeilen mit Platzhaltern (**Zeilentext** sowie **Wert 1** bis **Wert 10**). Die zulässigen Platzhalter werden in der **Prüfdaten Mailvorlagenwertliste** verwaltet und beim Versand z. B. durch Prüfungsnummer, Belegnummer, Benutzer, Objekt, Charge, Menge ersetzt.

### 5.7 Prüfdaten-Systemtabellen (Referenz)

Die folgenden Seiten enthalten Referenzdaten, die die Regelverarbeitung (Kapitel 6) steuern. Sie werden überwiegend durch die App vorgegeben und nur bei Bedarf ergänzt.

- **Prüfdatenkategorie** – Fachbereiche (z. B. Einkauf, Verkauf, Artikel), unter denen Ereignisse, Antworten und Regeln zusammengefasst werden. Felder: **Benutzergruppencode** (Code) und **Beschreibung**.
- **Prüfdatenentität** – Ordnet ein Tabellen-/Tabellenpaar (mit optionaler verknüpfter Tabelle) einer Prüfdatenkategorie zu. Damit erkennt das Modul aus einem Beleg die zuständige Kategorie. Felder u. a.: **Tabellen-ID**, **Verknüpfte Tabellen-ID**, **Kategorie**.
- **Prüfdatenereignisse** – Auslösepunkte („Wann"), an denen Regeln verarbeitet werden (Feld **Wann** je Ereignis). 
- **Prüfdatenantworten** – Reaktionen („Dann"), die eine Regel ausführt, z. B. Prüfung erstellen, Artikel sperren, Benutzer benachrichtigen (Feld **Dann** je Antwort).
- **Prüfdatenmerkmal** – Definiert ein **Spezielles Merkmal**, d. h. eine über eine verknüpfte Tabelle erreichbare Feldreferenz (z. B. Debitor am Fertigungsauftrag), die als zusätzliches Regelkriterium dient. Felder u. a.: **Tabellen-ID**, **Feld-ID**, **Merkmal Tabellen-ID**, **Spezielles Merkmal**.

---

## 6. Regeln und automatische Prüfungserstellung

Prüfregeln erzeugen Prüfungen automatisch, sobald ein bestimmtes Ereignis in Business Central eintritt (z. B. Freigabe eines Auftrags, Validierung eines Probenwerts, zeitgesteuerter Lauf). Eine Regel verbindet drei Bausteine: eine **Prüfdatenkategorie** (Fachbereich), eine **Prüfvorlage** (was geprüft wird) sowie **Regelfilter** (auf welche Datensätze die Regel zutrifft) und **Ereignisantworten** (bei welchem Ereignis welche Reaktion erfolgt).

### 6.1 Regelstammdaten und Regelverarbeitung

Die Verarbeitung läuft so ab: Tritt ein Ereignis ein, ermittelt das Modul über die **Prüfdatenentität** die Kategorie, sammelt alle aktiven Regeln zu Ereignis und Kategorie, behält in Prioritätenreihenfolge nur die Regeln, deren **Regelfilter** sämtlich zutreffen, und führt je Regel die hinterlegten **Ereignisantworten** aus – die Antwort erstellt dann z. B. die Prüfung.

**Einstieg:** **Prüfdatenverwaltung → Prüfregeln** (Liste), Öffnen einer Zeile führt zur Regelkarte **Prüfdatenregel**. Die Karte ist nur bearbeitbar, solange die Regel inaktiv ist und der Benutzer Qualitätssicherungsrecht besitzt.

| Feld | Erläuterung |
|---|---|
| Kategorie | Ordnet die Regel einem Fachbereich zu. Wenn Sie die Kategorie ändern, dann werden die vorhandenen Regelfilter und Ereignisantworten der Regel entfernt, da sie kategoriespezifisch sind. |
| Nr. | Nummer der Regel aus der Nummernserie. |
| Aktiv | Zeigt an, ob die Regel wirksam ist. Nur aktive Regeln werden bei einem Ereignis ausgeführt. |
| Priorität | Legt die Reihenfolge fest, in der konkurrierende Regeln geprüft werden. |
| Beschreibung | Bezeichnung der Regel. |
| Prüfvorlagennr. | Verweist auf die Prüfvorlage, nach der die Prüfung erzeugt wird. Wenn Sie eine Vorlage wählen, dann werden Gültig von/bis übernommen; eine inaktive Vorlage wird abgewiesen. |
| Prüfvorlagen-Versionscode | Version der zugeordneten Prüfvorlage. |
| Gültig von / Gültig bis | Gültigkeitszeitraum der Regel (aus der Vorlage übernommen). |
| Regelart | Legt fest, wie die Regel auslöst. **Standard:** Die Regel greift bei jedem passenden Ereignis. **Interval:** Die Regel greift erst, wenn ein Zähler oder eine kumulierte Menge einen Schwellwert erreicht (Intervallsteuerung über die Regelfilter). |
| Ausführungsdatum letzter Lauf / Ausführungszeitintervall / Ausführung je Menge | Nur bei zeitgesteuerten Regeln sichtbar: steuern den nächsten Lauf über die Aufgabenwarteschlange und die je Objekt kumulierte Menge. |

**Regelfilter** (Unterformular): Jede Filterzeile prüft ein Feld eines Belegs, einer Zeile oder einer verknüpften Tabelle.

| Feld | Erläuterung |
|---|---|
| Tabellen-ID / Tabellenbezeichnung | Legt die zu prüfende Tabelle fest. |
| Feld-ID / Feldbezeichnung | Legt das zu prüfende Feld fest. |
| Feldfilter | Legt den Wert/Filter fest, der zutreffen muss, damit die Regel greift. **Wenn gesetzt, dann** wird die Regel nur auf Datensätze angewendet, die diesen Filter erfüllen. |
| Feldart | Zeigt die Art des Feldwerts: **Andere**, **Boolean** oder **Option** – danach wird der Filter interpretiert. |
| Verknüpfte Tabellen-ID / -bezeichnung | Verweist bei Filtern über eine verknüpfte Tabelle (spezielles Merkmal) auf diese. |
| Intervall zählen / Ausführungsintervall / Intervallfeld / Intervallzähler | Nur bei Regelart **Interval**: legen fest, ob nach Anzahl (Zähler) oder nach kumulierter Feldmenge ausgelöst wird und bei welchem Schwellwert. Über **Intervallzähler bearbeiten** setzen Sie den Zähler zurück. |

**Ereignisantwort** (Unterformular): verbindet je Zeile ein **Ereignis** mit einer **Antwort** derselben Kategorie; über **Benutzer benachrichtigen** wird zusätzlich eine Benachrichtigung ausgelöst.

Aktionen auf der Regel: **Regel aktivieren** (setzt Aktiv; verlangt eine gültige, aktive Vorlage und fragt bei leerem Zeitintervall nach), **Regel deaktivieren**, sowie in der Regelliste **Regel kopieren** (dupliziert Regel samt Filtern und Ereignisantworten).

### 6.2 Automatische Prüfungserstellung einrichten

Diese dedizierte Einrichtung verbindet Stammdaten und Regel bis zur automatischen Prüfung im Tagesablauf. Konfiguriert wird sie durch einen Administrator/Key-User mit Qualitätssicherungsrecht, bevor die automatische Erstellung erstmals genutzt wird; sie wird in der täglichen Arbeit an den Belegen (Kapitel 7/8) wirksam.

1. **Zuerst** stellen Sie sicher, dass eine **aktive Prüfvorlage** existiert (Kapitel 5.5): Vorlage mit gültigem Zeitraum und **Vorlagen aktivieren**. *Wenn keine aktive Vorlage vorliegt, dann kann die Regel nicht aktiviert werden.*
2. **Danach** prüfen Sie die **Prüfdatenkategorie** und die **Prüfdatenentität** (Kapitel 5.7): Die Entität ordnet die relevante Tabelle der Kategorie zu. *Wenn die Zuordnung fehlt, dann erkennt das Modul aus dem Beleg keine Kategorie und die Regel greift nicht.*
3. **Danach** legen Sie über **Prüfregeln → Neu** die **Prüfdatenregel** an, wählen Kategorie und Prüfvorlagennr. und setzen die **Priorität**.
4. **Danach** erfassen Sie die **Regelfilter** (welche Datensätze) und die **Ereignisantwort** (welches Ereignis löst welche Antwort aus, z. B. „Prüfung erstellen"). *Wenn ein Filter nicht zutrifft, dann wird die Regel für diesen Datensatz übersprungen.*
5. **Schließlich** wählen Sie **Regel aktivieren**. Ab jetzt erstellt Business Central beim passenden Ereignis automatisch eine Prüfung nach der Vorlage. Der Anwender findet die Prüfung anschließend über den **Prüfstatus** der Belegzeile bzw. über **Prüfungen** (Kapitel 7/8).

### 6.3 Einrichtungsassistent für Prüfregeln

Der **Prüfdatenregeleinrichtungsassistent** führt einen Administrator schrittweise durch die Vorbereitung der Regeln. Über die Schritte **Kategorie → Entität → Merkmal → Ereignis → Antwort** öffnet der Assistent jeweils die zugehörige Einrichtungsseite (Aktion **Öffnen …**), sodass die Grunddaten vorhanden sind, bevor eine Regel angelegt wird. Mit **Zurück**, **Weiter** und **Fertigstellen** navigieren Sie durch den Assistenten.

---

## 7. Tägliche Arbeit: Prüfung, Proben und Probenwerte

Dieses Kapitel beschreibt den Kern der täglichen Arbeit: das Erstellen einer Prüfung, das Anlegen von Proben, das Erfassen der Probenwerte und die Freigabe.

Die tägliche Arbeit wird durch die **Prüfdaten Einrichtung** (Kapitel 4: automatische Probenerstellung, Quarantäne, Chargensperre, verarbeitete Proben) sowie durch die **Prüfvorlagen** (Kapitel 5.5: welche Eigenschaften und Vorgabewerte, Anzahl Proben) gesteuert. Prüfungen können zusätzlich durch **Prüfregeln** (Kapitel 6) automatisch entstehen.

### 7.1 Die Prüfungskarte

**Einstieg:** **Prüfdatenverwaltung → Prüfungen** öffnet die Liste **Prüfungen**; über eine Zeile gelangen Sie zur **Prüfungskarte**. Alternativ wird die Karte direkt beim Erstellen einer Prüfung geöffnet (Aktionen in 7.4) oder über die Detailinformation einer Belegzeile (Kapitel 8).

**Allgemein:**

| Feld | Erläuterung |
|---|---|
| Nr. | Nummer der Prüfung aus der Nummernserie (nicht editierbar). |
| Status | **Offen:** Die Prüfung ist in Bearbeitung; Zeilen und Proben können geändert werden. **Freigegeben:** Die Prüfung ist abgeschlossen; die Zeilen sind gesperrt und das Prüfzeugnis kann erzeugt werden. |
| Abweichung zum Vorgabewert vorhanden | Wenn dieses (hervorgehobene) Kennzeichen gesetzt ist, dann weicht mindestens ein erfasster Probenwert vom Vorgabewert der Vorlage ab – ein Hinweis für die Qualitätsbewertung. |
| Beschreibung | Freitextbezeichnung der Prüfung. |
| Erstellungsdatum | Anlagedatum (automatisch gesetzt). |
| Prüfnorm | Ordnet der Prüfung eine Norm zu (Auswahl aus **Normen**); wird im Prüfzeugnis ausgewiesen. |
| Belegart | Legt fest, worauf sich die Prüfung bezieht. Zur Auswahl stehen die belegbezogenen Arten (Einkaufsbestellung, Verkaufsauftrag, Wareneingang, Warenausgang, Einlagerung/Kommissionierung, Fertigungsauftrag, Artikel Buch.-Blatt) sowie der objektbezogene Fall (leer). Wenn Sie die Belegart ändern, dann werden die abhängigen Bezugsfelder zurückgesetzt (nur zulässig, solange keine Probe existiert). |

Je nach Belegart blendet die Karte weitere Gruppen ein, deren Felder ausschließlich den gewählten Bezug betreffen (aus Gründen der Übersichtlichkeit ist jeweils nur die passende Gruppe sichtbar):

- **Lagerort** (bei objektbezogener Prüfung, Belegart leer): **Lagerortcode** des zu prüfenden Objekts.
- **Vorlage:** **Prüfvorlagennr.** (Pflichtangabe; die Auswahl überträgt Version, Anzahl Proben und Probendatenbefüllung) und **Prüfvorlagen-Versionscode**.
- **Probenprozess:** **Anzahl Proben**.
- **Objekt:** **Objektart** – **(leer)**, **Artikel**, **Arbeitsplatz** oder **Arbeitsplatzgruppe** –, **Objektnr.**, **Variantencode** und die Beschreibungen. Die Objektart bestimmt, welche Stammdaten geprüft werden.
- **Beleg** bzw. **Herkunft** (bei belegbezogener Prüfung): **Belegnr.**, **Belegzeilennr.**, **Herkunftsart** (**(leer)**, **Debitor**, **Kreditor**), **Herkunftsnr.** und **Herkunftsname** sowie bei Artikel-Buch.-Blatt die Buchblattfelder.
- **Fertigungsauftrag** (bei Belegart Fertigungsauftrag): **FA-Status**, **FA-Nr.** und **Belegzeilenart** – **(leer)**, **Fertigungauftragszeile**, **FA-Komponente** oder **FA-Arbeitsgangzeile** – mit den jeweils passenden Bezugsfeldern.

**Zeilen (Unterformular Prüfdaten Subpage):** Die Prüfungszeilen entstehen aus der Vorlage und enthalten je Prüfeigenschaft **Prüfgruppencode**, **Charakteristik-Nr.**, Beschreibungen, **Datenart**, **Vorgabewert 1/2** und das Kennzeichen **Drucken**.

**Faktenkästen** rechts: **Probenliste** und **Probenwerte** (Übersicht der Proben und Werte), die Kopf- und Zeilenbemerkungen sowie die **Prüfzeugnisliste** zur Prüfung.

**Aktionen der Prüfungskarte:** **Proben** (öffnet die Probenliste), **Neue Probe**, **Mehrere Proben erstellen**, **Freigeben**, **Status zurücksetzen**, **Prüfungszeilen aktualisieren** (übernimmt die Zeilen erneut aus der Vorlage), **Herkunftsbeleg öffnen** (springt zum Ursprungsbeleg bzw. -objekt) und **Bemerkung**.

### 7.2 Die Probenkarte und die Werteerfassung

**Einstieg:** Aktion **Proben** oder **Neue Probe** auf der Prüfungskarte; alternativ **Testzertifikat-Muster öffnen** auf einer Belegzeile (Kapitel 8). Aus der Probenliste öffnet eine Zeile die **Probenkarte**.

**Allgemein (Probenkarte):**

| Feld | Erläuterung |
|---|---|
| Verarbeitet | Wenn gesetzt, dann gilt die Probe als abgeschlossen; ihre Felder sind – abhängig von der Einrichtung „Verarbeitete Probe bearbeitbar" – gegen Änderungen gesperrt. |
| Probennr. | Nummer der Probe aus der Nummernserie (bei verarbeiteter Probe nicht editierbar). |
| Status | **Offen:** Werteerfassung möglich. **Freigegeben:** Werte gesperrt; die Prüfung kann erst freigegeben werden, wenn alle Proben freigegeben sind. |
| Beschreibung | Freitextbezeichnung der Probe. |
| Erstellungsdatum | Anlagedatum. |
| Belegart | Bezug der Probe (Anzeige). |
| Abweichung zum Vorgabewert | Zeigt an, ob ein Probenwert vom Vorgabewert abweicht. |
| Probe drucken | Wenn aktiviert, dann werden die Werte dieser Probe in das Prüfzeugnis aufgenommen. |
| Schlüsselwert | Wenn aktiviert, dann werden die Zeilen dieser Probe als Schlüsselwerte behandelt und beim Erzeugen des Prüfzeugnisses vorrangig berücksichtigt. |
| Quarantäne | Wenn aktiviert, dann ist der zugehörige Bestand als Quarantäne gekennzeichnet; das Kennzeichen wird auf Proben mit gleicher Charge/Seriennr. übertragen. |
| Prüfvorlagennr. | Verweist auf die zugrunde liegende Prüfvorlage (Absprung zur Vorlage per Detailinformation). |

**Artikelverfolgung:** In der Gruppe für die Artikelverfolgung erfassen Sie **Artikelnr.**, **Variantencode**, **Seriennr.** und **Chargennr.**. Über **Serien/Chargen-Nr. vom Beleg holen** übernehmen Sie die im Herkunftsbeleg vorhandenen Werte; die zugehörige Menge und die Verfolgungsbezeichnung werden automatisch ermittelt.

**Werteerfassung (Unterformular Prüfdaten Proben-Subpage):** Hier tragen Sie je Prüfeigenschaft den gemessenen Wert ein.

| Feld | Erläuterung |
|---|---|
| Prüfgruppencode | Prüfgruppe der Zeile (Anzeige). |
| Charakteristik-Nr. | Prüfeigenschaft der Zeile (Anzeige). |
| Charakteristikbeschreibung | Bezeichnung der Prüfeigenschaft. |
| Datenart | Datenart der Eigenschaft (Text, Ganzzahl, Dezimal, Medium). |
| Probenwert | Der erfasste Messwert. Wenn Sie einen Wert eingeben, dann wird er gegen die Datenart bzw. den Lookup geprüft und – bei Abweichung vom Vorgabewert – als Abweichung markiert. |
| Vorgabewert 1 / Vorgabewert 2 | Sollwerte aus der Vorlage; nur sichtbar, wenn in der Vorlage **Standardwerte anzeigen** aktiviert ist. |
| Abweichung zum Vorgabewert | Zeigt an, ob der erfasste Wert vom Vorgabewert abweicht. |
| Schlüsselwert | Kennzeichnet die Zeile als Schlüsselwert. |
| Medium vorhanden | Zeigt an, ob zur Eigenschaft ein Bild hinterlegt ist; über **Medien importieren**/**Medien anzeigen** verwalten Sie das Bild. |
| Verarbeitet | Zeigt an, ob die Zeile verarbeitet ist (Anzeige). |

Das Wertegitter zeigt nur die Prüfgruppen, für die der angemeldete Benutzer über seine Prüfdatenbenutzergruppe berechtigt ist. So sehen Prüfer nur die für sie relevanten Eigenschaften.

**Aktionen der Probenkarte:** **Freigeben**, **Status zurücksetzen** (nicht möglich, solange die Prüfung freigegeben ist) und **Serien/Chargen-Nr. vom Beleg holen**.

### 7.3 Freigabe von Proben und Prüfung

Der Abschlussprozess folgt einer festen Reihenfolge (Details siehe auch Schnellstart, Kapitel 2):

1. **Probenwerte** je Probe im Wertegitter erfassen.
2. Auf jeder Probe **Freigeben** wählen (oder in der Probenliste **Alle Proben freigeben**). Die Probe erhält Status **Freigegeben**; abhängig von der Einrichtung wird sie zugleich als verarbeitet markiert.
3. Auf der **Prüfungskarte** **Freigeben** wählen. Sind noch offene Proben vorhanden, verlangt Business Central zunächst deren Freigabe. Danach erhält die Prüfung Status **Freigegeben**, die Proben werden als verarbeitet gesetzt und – bei aktivierter Einrichtung **Prüfzeugnis automatisch erstellen** – wird das Prüfzeugnis erzeugt.
4. Bei Bedarf **Status zurücksetzen** auf der Prüfung (bei Einrichtung **Zertifikat kann nur von QS-Benutzer wieder geöffnet werden** nur durch Benutzer mit Qualitätssicherungsrecht). Das Wiederöffnen setzt den **Prüfstatus** der Belegzeile zurück.

### 7.4 Prüfung erstellen – Einstiegspunkte

Eine Prüfung entsteht auf einem der folgenden Wege:

- **Aus den Stammdaten:** Auf der **Artikelkarte** oder in der Artikelübersicht die Aktion **Prüfung für Artikel erstellen**; auf der Arbeitsplatzgruppen- bzw. Arbeitsplatzkarte **Prüfung für Arbeitsplatzgruppe erstellen** bzw. **Prüfung für Arbeitsplatz erstellen**. Sie wählen eine Prüfvorlage; die Prüfungskarte öffnet sich anschließend.
- **Aus einem Beleg:** Auf einer Belegzeile die Aktion **Testzertifikat-Muster öffnen** bzw. **Prüfung erstellen** (siehe Kapitel 8).
- **Direkt:** Über **Prüfungen → Neu**, Auswahl der Prüfvorlage und Erfassung des Bezugs (Objekt/Beleg).
- **Automatisch:** Über eine aktive **Prüfregel** beim passenden Ereignis (Kapitel 6).

---

## 8. Belegintegration, Prüfstatus, Quarantäne und Lager

Das Modul ergänzt die Standardbelege von Business Central um einen **Prüfstatus** und um Aktionen, mit denen Sie zu einer Belegzeile die zugehörige Prüfung bzw. deren Proben öffnen oder eine Prüfung erstellen. Betroffen sind insbesondere die Verkaufsauftrags- und Einkaufsbestellzeilen, die Lagerbelege (Wareneingang, Warenausgang, Kommissionierung, Einlagerung, jeweils auch Lager-/Bestandsvarianten), die Fertigungsbelege (**FA-Arbeitsplan**, **FA-Komponenten**, freigegebene/beendete Fertigungsauftragszeilen) sowie die Buch.-Blätter (Artikel Buch.-Blatt, Verbrauchs-, Istmeldungs- und Produktions-Buch.-Blatt) und die Artikelverfolgungszeilen.

### 8.1 Der Prüfstatus auf Belegzeilen

Auf den genannten Belegzeilen ergänzt das Modul die Spalte **Prüfstatus**. Sie wird farblich hervorgehoben und ist nicht direkt editierbar; sie wird durch die zugehörige Prüfung gesetzt.

| Wert | Erläuterung |
|---|---|
| **(leer)** | Zur Zeile existiert keine Prüfung; es besteht keine Prüfpflicht bzw. sie wurde noch nicht ausgelöst. |
| **Prüfung** | Zur Zeile besteht eine offene Prüfung; die Prüfung ist angelegt, aber noch nicht freigegeben. |
| **Bestanden** | Die zugehörige Prüfung wurde freigegeben und die Zeile ist geprüft/freigegeben. |
| **Gesperrt** | Die Zeile ist gesperrt; eine Weiterverarbeitung ist nicht zulässig, bis die Prüfung abgeschlossen ist. |
| **Quarantäne** | Der Bestand der Zeile befindet sich in Quarantäne (gesperrter Prüfbestand). |

Hinweis: Auf **FA-Arbeitsgangzeilen** kennt der Prüfstatus die Ausprägung **Quarantäne** nicht; dort sind nur **(leer)**, **Prüfung**, **Bestanden** und **Gesperrt** möglich.

Per Detailinformation auf der Spalte **Prüfstatus** springen Sie direkt zur zugehörigen **Prüfungskarte**.

### 8.2 Aktionen auf der Belegzeile

Je Beleg stehen in der Zeilengruppe folgende Aktionen bereit:

- **Testzertifikat-Muster öffnen** – öffnet zu der Belegzeile die zugehörige Probe (bei einer Probe die **Probenkarte**, bei mehreren die Probenliste). Verfügbar u. a. auf Verkaufs- und Einkaufszeilen, Lagerzeilen, Fertigungszeilen und Buch.-Blattzeilen.
- **Prüfung erstellen** / **Prüfung für Artikel erstellen** / **Neues Prüfzeugnis** – legt zu der Zeile eine Prüfung bzw. ein Prüfzeugnis an (verfügbar u. a. auf **FA-Arbeitsplan**, **FA-Komponenten**, Artikel-/Verbrauchs-/Istmeldungs-Buch.-Blatt sowie beendeten/freigegebenen Fertigungsauftragszeilen).
- **Testzertifikat öffnen** – auf der **Chargennr.-Informationskarte** öffnet die zur Charge gehörende Prüfung.

### 8.3 Quarantäne und Bestandssperre

Ist in der **Prüfdaten Einrichtung** ein **Quarantäne-Lagerort** bzw. -Lagerplatz hinterlegt und die automatische Quarantänebuchung aktiviert, so wird zu prüfender Bestand automatisch auf den Quarantäne-Lagerplatz gebucht und dort gesperrt, bis die Prüfung freigegeben ist. Optional erfolgt vorher eine Rückfrage (**Vor Buchung in Quarantäne nachfragen**), und Belegzeilen mit Quarantänebestand lassen sich sperren (**Quarantäne-Buchungszeilen sperren**).

Zusätzlich gilt eine Buchungssperre: Enthält ein Lager- oder Verkaufsbeleg eine Zeile, die den **Quarantäne-Lagerort** oder einen als Quarantäne gekennzeichneten Lagerplatz betrifft, so kann der Beleg nur von einem Benutzer mit Qualitätssicherungsrecht gebucht werden; andere Benutzer erhalten eine Fehlermeldung. So wird verhindert, dass gesperrte Prüfbestände unkontrolliert das Lager verlassen.

Die Quarantäne-Lagerplätze legen Sie über die Aktion **Quarantäne-Lagerplatz einrichten** in der Einrichtung an; anschließend werden die betroffenen Lagerplätze angezeigt.

---

## 9. Prüfzeugnis, Druck und E-Mail

Aus einer freigegebenen Prüfung entsteht das **Prüfzeugnis** – der druck- und versandfähige Nachweis der Prüfergebnisse.

**Einstieg:** **Prüfdatenverwaltung → Berichte und Aufgaben → Prüfzeugnisse** öffnet die **Prüfzeugnisliste**; eine Zeile öffnet das **Prüfzeugnis**. Bei aktivierter Einrichtung **Prüfzeugnis automatisch erstellen** wird das Prüfzeugnis bereits bei der Freigabe der Prüfung angelegt.

### 9.1 Das Prüfzeugnis

Der Prüfzeugniskopf übernimmt die Daten der Prüfung (Herkunft, Beleg, Objekt, Norm, Menge). Wesentliche Felder:

| Feld | Erläuterung |
|---|---|
| Nr. | Nummer des Prüfzeugnisses aus der Nummernserie. |
| Beschreibung | Freitextbezeichnung; wird im E-Mail-Versand als Nachrichtentext verwendet. |
| Prüfungsnr. | Verweist auf die zugrunde liegende Prüfung. Wenn Sie die Prüfung setzen, dann werden die Zeugniszeilen aus den Schlüssel-Probenwerten übernommen und die Kopfdaten (Herkunft, Objekt, Beleg, Norm) gefüllt. |
| Prüfungserstellungsdatum | Anlagedatum der zugrunde liegenden Prüfung (Anzeige). |
| Benutzer mit Qualitätssicherung | Führt die Prüfdatenbenutzer mit Qualitätssicherungsrecht auf, die zu den gedruckten Prüfgruppen gehören; sie erscheinen im Unterschriftsbereich des Zeugnisses. |
| Prüfdatenbenutzer | Der für das Zeugnis verantwortliche Prüfdatenbenutzer. |
| Druckzähler | Zählt die Ausdrucke des Zeugnisses. Ein bereits gedrucktes Zeugnis kann nur von einem Benutzer mit Qualitätssicherungsrecht gelöscht werden. |

In den Gruppen **Objekt**, **Herkunft/Beleg** und **Norm** werden die zugehörigen Daten (Objektart/-nr., Belegart/-nr., Herkunftsart, Norm) schreibgeschützt gespiegelt. Die Zeugniszeilen (Unterformular **Prüfzeugnis-Subpage**) enthalten je Wert die Prüfeigenschaft, den **Probenwert**, die **Druckart** (Zeilen/Spalten/Textblock) sowie Chargennr./Seriennr.

### 9.2 Drucken und Versenden

Auf dem Prüfzeugnis stehen bereit:

- **Probenwerte auswählen** – öffnet die Probenwerte und übernimmt die gewählten Werte als Zeugniszeilen.
- **Beleg drucken** – erzeugt das gedruckte Prüfzeugnis (Bericht) mit Firmenlogo (Position gemäß Einrichtung), Kopfdaten und den Ergebnissen in der jeweiligen Druckart sowie hinterlegten Bildern; der Druckzähler wird erhöht.
- **E-Mail senden** – erzeugt das Prüfzeugnis als PDF und öffnet eine E-Mail an die hinterlegte Adresse des angemeldeten Benutzers mit dem PDF im Anhang (Betreff = Prüfungsnr., Text = Beschreibung).

### 9.3 Benachrichtigungen und Mailvorlagen

Prüfdatenantworten aus Regeln können Benutzer benachrichtigen. Je Prüfdatenbenutzer bestimmt die **Benachrichtigungsmethode** (Email oder Benachrichtigung), wie er informiert wird. Der **Benachrichtigungsplan** legt den Rhythmus fest.

**Einstieg Benachrichtigungsplan:** Aktion **Benachrichtigungsplan** auf der Liste **Prüfdatenbenutzer** (je Benutzer).

| Feld | Erläuterung |
|---|---|
| Wiederholung | Legt fest, wann angesammelte Benachrichtigungen versendet werden. **Sofort:** unmittelbar. **Täglich / Wöchentlich / Monatlich:** gebündelt zum eingestellten Zeitpunkt. |
| Zeit | Uhrzeit des Versands (außer bei Sofort). |
| Tägliche Häufigkeit | **Werktag:** nur an Werktagen. **Täglich:** an allen Tagen. |
| Montag … Sonntag | Bei wöchentlicher Wiederholung: die Wochentage des Versands. |
| Tag des Monats / Monatliches Benachrichtigungsdatum | Bei monatlicher Wiederholung: **Erster Werktag**, **Letzter Werktag** oder **Benutzerdefiniert** (dann konkreter Tag im Feld „Tag des Monats"). |

Der Text der E-Mail wird aus einer **Prüfdaten-Mailvorlage** (Kapitel 5.6) erzeugt, deren Platzhalter durch die konkreten Prüf- und Belegdaten ersetzt werden. Interne Benachrichtigungen erscheinen als **Prüfdatenbenachrichtigungsposten**.

---

## 10. Historie und Nachverfolgung

Das Modul dokumentiert seine Aktivitäten in mehreren Listen, die Sie unter **Prüfdatenverwaltung → Berichte und Aufgaben** bzw. **→ Verwaltung** erreichen:

- **Prüfungen** – alle Prüfungen mit Status; Einstieg in die Prüfungskarte und Ausgangspunkt für Auswertungen. Über **Ausgewählte löschen** entfernen Sie markierte Prüfungen (mit den zugehörigen Proben und Bemerkungen).
- **Prüfzeugnisliste** – alle erzeugten Prüfzeugnisse mit Prüfungsnr., Beschreibung und **Druckzähler**.
- **Prüfdaten Benachrichtigungsposten** – die je Empfänger angelegten Benachrichtigungen mit Typ (**Neuer Datensatz**, **Genehmigung**, **Überfällig**), auslösendem Datensatz, Ziel-Seite und Fehlermeldung.
- **Prüfdaten Benachrichtigungsverlauf** – die tatsächlich versendeten Benachrichtigungen mit Empfänger, E-Mail-Adresse, Sendezeitpunkt sowie Betreff und Text.
- **Prüfdaten Regelfilterliste** – ein Überblick aller Regelfilter über alle Regeln hinweg, jeweils mit Kenn­zeichnung, ob die zugehörige Regel aktiv ist.

Über die Detailinformation der Prüfstatus-Spalte auf den Belegzeilen (Kapitel 8) und über **Herkunftsbeleg öffnen** auf der Prüfungskarte navigieren Sie zwischen Prüfung, Zeugnis und Ursprungsbeleg.

---

## 11. FAQ und Troubleshooting

### 1. Warum lässt sich meine Prüfung nicht freigeben?
Weil noch mindestens eine Probe den Status **Offen** hat. Beim Freigeben der Prüfung meldet Business Central, dass zuerst alle vorhandenen Proben freigegeben werden müssen. Geben Sie die Proben einzeln über **Freigeben** oder gesammelt über **Alle Proben freigeben** frei und wiederholen Sie dann die Freigabe der Prüfung.

### 2. Warum kann ich eine freigegebene Prüfung nicht wieder öffnen?
Wenn in der **Prüfdaten Einrichtung** die Option **Zertifikat kann nur von QS-Benutzer wieder geöffnet werden** aktiviert ist, darf nur ein Benutzer mit Qualitätssicherungsrecht die Aktion **Status zurücksetzen** ausführen. Lassen Sie sich das Recht in einer Prüfdatenbenutzergruppe zuweisen oder bitten Sie einen QS-Benutzer.

### 3. Warum kann ich einen Wareneingang/Verkauf nicht buchen?
Weil eine Belegzeile den **Quarantäne-Lagerort** oder einen als Quarantäne gekennzeichneten Lagerplatz betrifft. Solche Belege dürfen nur von Benutzern mit Qualitätssicherungsrecht gebucht werden. Schließen Sie die Prüfung ab bzw. lassen Sie einen QS-Benutzer buchen.

### 4. Warum wird keine Prüfung automatisch erzeugt, obwohl eine Regel existiert?
Prüfen Sie drei Punkte: Die **Prüfregel** muss **aktiv** sein, die zugeordnete **Prüfvorlage** muss aktiv und im Gültigkeitszeitraum sein, und die **Regelfilter** müssen auf den konkreten Datensatz zutreffen. Trifft ein Filter nicht zu oder ist die Vorlage inaktiv, überspringt das Modul die Regel.

### 5. Warum lässt sich eine Prüfregel nicht aktivieren?
Weil ihr keine gültige, aktive **Prüfvorlage** zugeordnet ist. Ordnen Sie eine aktive Vorlage zu (Gültigkeitszeitraum umfasst das Arbeitsdatum, **Vorlagen aktivieren** ausgeführt). Bei zeitgesteuerten Regeln mit leerem Ausführungszeitintervall erscheint zusätzlich eine Rückfrage.

### 6. Warum kann ich in einer Prüfeigenschaft die Datenart oder Referenzart nicht mehr ändern?
Weil zu der Prüfeigenschaft bereits Werte bzw. Verwendungen bestehen. Sind bereits Eigenschaften/Werte vorhanden, sind Änderungen an Datenart und Referenzart gesperrt, um bestehende Prüfergebnisse konsistent zu halten.

### 7. Warum sehe ich im Probenwertegitter nicht alle Prüfgruppen?
Weil das Gitter nur die Prüfgruppen anzeigt, für die Sie über Ihre **Prüfdatenbenutzergruppe** berechtigt sind. Fehlt eine Gruppe, lassen Sie sich über die Prüfgruppenzuordnung Ihrer Benutzergruppe berechtigen.

### 8. Warum kann ich eine verarbeitete Probe nicht mehr bearbeiten oder wieder öffnen?
Ist die Einrichtung **Verarbeitete Probe bearbeitbar** deaktiviert, sperrt das Modul verarbeitete Proben gegen Änderungen. Das Wiederöffnen einer verarbeiteten Probe setzt zusätzlich die Einrichtung **Wiedereröffnen verarbeiteter Proben zulassen** voraus.

### 9. Warum steht auf meiner Prüfungskarte „Abweichung zum Vorgabewert vorhanden"?
Weil mindestens ein erfasster **Probenwert** vom **Vorgabewert** der Prüfvorlage abweicht. Prüfen Sie die betroffenen Werte im Wertegitter; die Abweichung ist ein Hinweis für die Qualitätsbewertung, kein technischer Fehler.

### 10. Warum kann ich ein bereits gedrucktes Prüfzeugnis nicht löschen?
Weil ein Prüfzeugnis mit einem **Druckzähler** größer null nur von einem Benutzer mit Qualitätssicherungsrecht gelöscht werden darf. So bleibt nachvollziehbar, welche Zeugnisse bereits ausgegeben wurden.

---

## 12. Typische Anwendungsfälle

Die folgenden Beispiele zeigen den Ablauf von einem realen Auslöser bis zum Abschluss. Alle Seiten und Aktionen entsprechen dem tatsächlichen Verhalten des Moduls.

### 12.1 Wareneingang mit Prüfung (Lieferantencharge)

**Auslöser:** Eine Lieferung trifft ein; zu einer Einkaufsbestellung ist eine Wareneingangsprüfung erforderlich, bevor der Bestand frei verwendet werden darf.

**Einstieg in BC:** Der Anwender öffnet den **Wareneingang** zur Bestellung. In der Wareneingangszeile zeigt die Spalte **Prüfstatus** den Wert **Prüfung** (die Prüfung wurde per Regel erzeugt) bzw. der Anwender wählt in der Zeile **Testzertifikat-Muster öffnen**. Über die Detailinformation der Prüfstatus-Spalte gelangt er zur **Prüfungskarte**.

**Kernablauf:**
1. Auf der **Prüfungskarte** die Belegdaten prüfen (Belegart Wareneingang, Herkunftsart **Kreditor**, Objekt Artikel).
2. **Neue Probe** wählen; auf der **Probenkarte** über **Serien/Chargen-Nr. vom Beleg holen** die **Chargennr.** übernehmen.
3. Im Wertegitter die **Probenwerte** je Prüfeigenschaft erfassen.
4. Die Probe **Freigeben**, anschließend auf der Prüfungskarte **Freigeben**.

**Abschluss:** Nach der Freigabe ist der **Prüfstatus** der Wareneingangszeile **Bestanden**; ggf. entsperrt sich der Quarantänebestand. Bei aktivierter Einrichtung entsteht automatisch ein **Prüfzeugnis**, das über **Beleg drucken** ausgegeben werden kann.

### 12.2 Verkaufsauftrag mit Prüfzeugnis-Ausdruck

**Auslöser:** Ein Kunde verlangt zur Lieferung ein Prüfzeugnis.

**Einstieg in BC:** Der Anwender öffnet den **Verkaufsauftrag**. In der Verkaufszeile steht die Spalte **Prüfstatus**; über **Testzertifikat-Muster öffnen** in der Zeile öffnet er die zugehörige Probe bzw. Prüfung.

**Kernablauf:**
1. Auf der **Prüfungskarte** die Proben anlegen (**Neue Probe** / **Mehrere Proben erstellen**) und die **Probenwerte** erfassen.
2. Proben **Freigeben** und Prüfung **Freigeben**.
3. Das erzeugte **Prüfzeugnis** öffnen (**Prüfdatenverwaltung → Berichte und Aufgaben → Prüfzeugnisse**), bei Bedarf **Probenwerte auswählen**.

**Abschluss:** Über **Beleg drucken** wird das Prüfzeugnis gedruckt; über **E-Mail senden** wird es als PDF an den Kunden bzw. den Sachbearbeiter versendet.

### 12.3 Automatische Prüfungserstellung per Regel

**Auslöser:** Der Qualitätsverantwortliche möchte, dass bei einem bestimmten Ereignis (z. B. Freigabe eines Belegs) automatisch eine Prüfung entsteht.

**Einstieg in BC:** Der Administrator öffnet **Prüfregeln** und legt eine **Prüfdatenregel** an.

**Kernablauf:**
1. Kategorie und **Prüfvorlagennr.** (aktive Vorlage) wählen, **Priorität** setzen.
2. **Regelfilter** erfassen (welche Datensätze betroffen sind).
3. In der **Ereignisantwort** das Ereignis mit der Antwort „Prüfung erstellen" verbinden, ggf. **Benutzer benachrichtigen** setzen.
4. **Regel aktivieren**.

**Abschluss:** Tritt das Ereignis ein, erzeugt Business Central automatisch die Prüfung; der Anwender findet sie über den **Prüfstatus** der Belegzeile bzw. unter **Prüfungen** und arbeitet sie wie in Kapitel 7 ab.

### 12.4 Prüfung für einen Artikel aus den Stammdaten

**Auslöser:** Für eine bestimmte Charge eines Artikels ist eine Qualitätsprüfung durchzuführen, ohne dass ein Beleg vorliegt.

**Einstieg in BC:** Der Anwender öffnet die **Artikelkarte** des betreffenden Artikels und wählt **Prüfung für Artikel erstellen**.

**Kernablauf:**
1. Im Auswahldialog die passende **Prüfvorlage** wählen; die **Prüfungskarte** öffnet sich mit Objektart **Artikel**.
2. **Neue Probe** anlegen, **Chargennr.**/**Seriennr.** erfassen und die **Probenwerte** eingeben.
3. Probe und Prüfung **Freigeben**.

**Abschluss:** Die Prüfung ist **Freigegeben**; bei Bedarf wird über das **Prüfzeugnis** ein Nachweis gedruckt oder versendet. Die Prüfung ist anschließend in der Liste **Prüfungen** und in der Historie nachvollziehbar.
