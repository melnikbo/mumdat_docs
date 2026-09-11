---
title: "m+m Base: Anwenderhandbuch"
---

# m+m Base: Anwenderhandbuch

## Einleitung

m+m Base erweitert Microsoft Dynamics 365 Business Central in mehreren Grundbereichen, die in anderen Fachmodulen wiederverwendet werden. Im Mittelpunkt stehen drei Anwenderpfade:

1. Einrichtung fuer Kreditlimitpruefung und Belegstatus.
2. Pflege zentraler Stammdaten wie Kreditversicherer, Terminarten und Statusereignisse.
3. Taegliche Arbeit direkt in Standardbelegen wie Verkaufsangebot, Verkaufsauftrag, Einkaufsangebot, Einkaufsauftrag sowie Rahmenverkaufs- und Rahmeneinkaufsauftrag.

Das Modul wirkt daher nicht nur ueber eigene Listen und Karten, sondern auch direkt in Standardseiten. Anwender arbeiten typischerweise ueber **Kreditlimit Einrichtung**, **Kreditversicherer**, **Terminarten**, **Belegstatus**, **Status**, **Statusereigniszuweisung** sowie ueber die erweiterten Verkaufs- und Einkaufsbelege.

## Schnellstart fuer Anwender

### Kreditlimitpruefung vorbereiten

1. Oeffnen Sie ueber **Tell Me** die Seite **Kreditlimit Einrichtung**.
2. Hinterlegen Sie die fuer Ihr Unternehmen benoetigten Parameter fuer die Kreditlimitpruefung.
3. Pflegen Sie anschliessend in **Kreditversicherer** die zulaessigen Versicherer.
4. Oeffnen Sie bei Bedarf **Benutzer Einrichtung** und pruefen Sie, welche Benutzer Kreditlimitwerte aendern duerfen.
5. Kontrollieren Sie auf der **Debitorkarte**, ob die fuer die Kreditlimitsteuerung benoetigten Stammdaten vorhanden sind.

### Stammdaten fuer Statussteuerung vorbereiten

1. Oeffnen Sie **Belegstatus** und legen Sie die benoetigten Statusdefinitionen an.
2. Oeffnen Sie **Status** und pflegen Sie die zulaessigen Stati.
3. Oeffnen Sie **Statusereignis** und erfassen Sie die Ereignisse, die zu Statuswechseln fuehren.
4. Verbinden Sie anschliessend Status und Ereignisse ueber **Statusereigniszuweisung**.
5. Pruefen Sie Aenderungen spaeter in **Belegstatus Aenderungsprotokoll**.

### Erweiterte Belegarbeit starten

1. Oeffnen Sie einen Verkaufs- oder Einkaufsbeleg, zum Beispiel **Verkaufsauftrag**, **Verkaufsangebot**, **Einkaufsauftrag** oder **Einkaufsangebot**.
2. Erfassen Sie zuerst die Kopfdaten wie gewohnt im Standard.
3. Bearbeiten Sie danach die durch m+m Base erweiterten Kopf- und Zeileninformationen.
4. Nutzen Sie die von der Erweiterung eingeblendeten Status-, Kreditlimit- oder Zusatzinformationen waehrend der Bearbeitung.
5. Kontrollieren Sie nach Statuswechseln oder Kreditlimitpruefungen die zugehoerigen Listen und Protokolle.

## Einrichtung

### Kreditlimit Einrichtung

Die Seite **Kreditlimit Einrichtung** ist die zentrale Einstiegsseite fuer die kreditlimitbezogenen Funktionen der Erweiterung. Rufen Sie die Seite zuerst auf, bevor Sie Kreditversicherer, benutzerspezifische Berechtigungen oder kundenbezogene Kreditlimitdaten pflegen.

Gehen Sie in dieser Reihenfolge vor:

1. Oeffnen Sie **Kreditlimit Einrichtung**.
2. Hinterlegen Sie die Grundparameter fuer die Pruefung und Verarbeitung von Kreditlimitvorgaengen.
3. Stimmen Sie die Einrichtung mit den Benutzerrechten in **Benutzer Einrichtung** ab.
4. Pflegen Sie danach die benoetigten Kreditversicherer.
5. Testen Sie die Wirkung anschliessend an einem Debitor und in einem Verkaufsbeleg.

Hinweis: Die genaue Feldliste der Seite konnte in diesem Lauf nicht automatisiert aus `get_page_field_catalog` gelesen werden, weil der MCP-Dienst fuer Seitenkataloge serverseitig nicht verfuegbar war. Fuer die fachliche Reihenfolge wurde die verifizierte Existenz der Seite und ihrer zugehoerigen Tabellen verwendet.

### Verkauf und Einkauf vorbereiten

m+m Base erweitert sowohl **Verkauf & Forderungen Einrichtung** als auch **Einkauf & Verbindlichkeiten Einrichtung**. Dadurch werden Grundparameter nicht in einer isolierten Modulkarte gepflegt, sondern in den vorhandenen Standard-Einrichtungsseiten.

Empfohlene Reihenfolge:

1. Oeffnen Sie **Verkauf & Forderungen Einrichtung**.
2. Pruefen Sie die durch m+m Base ergaenzten Einstellungen fuer Verkaufsprozesse.
3. Oeffnen Sie danach **Einkauf & Verbindlichkeiten Einrichtung**.
4. Pflegen Sie die fuer Einkaufsbelege benoetigten Zusatzparameter.
5. Testen Sie die Wirkung anschliessend in Verkaufs- und Einkaufsangeboten sowie in Auftraegen.

### Benutzer Einrichtung

Die Erweiterung fuegt der **Benutzer Einrichtung** eigene Einstellungen hinzu. Diese Seite ist wichtig, wenn Kreditlimitwerte nicht von jedem Benutzer geaendert oder uebersteuert werden duerfen.

Gehen Sie wie folgt vor:

1. Oeffnen Sie **Benutzer Einrichtung**.
2. Rufen Sie den betreffenden Benutzer auf.
3. Pflegen Sie die fuer m+m Base zusaetzlich eingeblendeten Felder.
4. Dokumentieren Sie interne Freigaberegeln ausserhalb der Seite, wenn nicht jeder Benutzer Kreditlimite oder Statusdaten aendern darf.
5. Fuehren Sie anschliessend einen Praxistest mit dem betroffenen Benutzer durch.

## Stammdaten

### Kreditversicherer

Die Seite **Kreditversicherer** dient zur Pflege der verfuegbaren Versicherer. Diese Stammdaten werden benoetigt, bevor kundenbezogene Kreditlimitinformationen sauber gepflegt und ausgewertet werden koennen.

Typischer Ablauf:

1. Oeffnen Sie **Kreditversicherer**.
2. Legen Sie fuer jeden Versicherer einen eigenen Datensatz an.
3. Pflegen Sie die fachlich benoetigten Identifikations- und Steuerungsdaten.
4. Verwenden Sie anschliessend die Datensaetze in den kreditlimitbezogenen Kundeninformationen.

### Terminarten

Mit **Terminarten** pflegen Sie die Basis fuer datums- oder fristbezogene Logik, die in angeschlossenen Prozessen genutzt wird.

Empfohlene Pflege:

1. Oeffnen Sie **Terminarten**.
2. Legen Sie die benoetigten Terminarten an.
3. Stimmen Sie die Definitionen mit den Fachbereichen ab, damit dieselben Begriffe in Verkauf und Einkauf verwendet werden.
4. Testen Sie die Auswirkungen in den erweiterten Belegen.

### Belegstatus

Die Seite **Belegstatus** enthaelt die Definition der verfügbaren Belegstatussaetze. Diese Pflege ist die Grundlage fuer spaetere Statussteuerung in Belegen und Protokollen.

Gehen Sie in dieser Reihenfolge vor:

1. Oeffnen Sie **Belegstatus**.
2. Legen Sie die fachlich benoetigten Statusdefinitionen an.
3. Stimmen Sie ab, welche Stati nur informativ sind und welche Prozesse steuern.
4. Verknuepfen Sie die Definitionen anschliessend mit Ereignissen und Zuweisungen.

### Status und Statusereignisse

Die Seiten **Status**, **Statusereignis** und **Statusereigniszuweisung** gehoeren fachlich zusammen. Pflegen Sie diese Bereiche immer als zusammenhaengenden Ablauf.

Empfohlene Reihenfolge:

1. Legen Sie auf **Status** die moeglichen Stati an.
2. Definieren Sie auf **Statusereignis** die ausloesenden Ereignisse.
3. Verbinden Sie beides auf **Statusereigniszuweisung**.
4. Testen Sie die Kombination anschliessend in einem echten Verkaufs- oder Einkaufsbeleg.
5. Kontrollieren Sie die Aenderungspaare spaeter in den Protokollseiten.

### Dokumenttexte und Uebersetzungen

Die Seite **Dokumenttext Uebersetzungen** ist fuer Texte relevant, die in unterschiedlichen Sprach- oder Ausgabekontexten benoetigt werden. Pflegen Sie diese Daten fruehzeitig, wenn in Verkauf oder Einkauf mehrsprachige oder standardisierte Texte ausgegeben werden sollen.

## Profile und Zuordnungen

m+m Base enthaelt keine eigenstaendige Profilkarte im Sinne einer separaten Profilverwaltung, wie sie in anderen m+m Modulen vorkommt. Die Rolle dieses Kapitels wird hier durch Zuordnungen zwischen Status, Ereignissen, Benutzern, Debitoren und Belegen erfuellt.

Wichtige Zuordnungsstellen sind:

1. **Statusereigniszuweisung** fuer die fachliche Verkettung von Ereignis und Status.
2. **Benutzer Einrichtung** fuer benutzerbezogene Steuerung.
3. **Debitorkarte** fuer kundenbezogene Informationen.
4. Erweiterte Verkaufs- und Einkaufsbelege fuer die operative Nutzung dieser Zuordnungen.

## Taegliche Arbeit in Verkaufs- und Einkaufsbelegen

### Verkauf: Angebote und Auftraege

m+m Base erweitert mindestens folgende Standardseiten im Verkauf:

1. **Verkaufsangebot**
2. **Verkaufsangebot Zeilen**
3. **Verkaufsauftrag**
4. **Verkaufsauftrag Zeilen**
5. **Rahmenverkaufsauftrag**
6. **Rahmenverkaufsauftrag Zeilen**
7. **Rahmenverkaufsauftraege**

Arbeiten Sie in Belegen in folgender Reihenfolge:

1. Erfassen oder oeffnen Sie den Belegkopf.
2. Pruefen Sie die durch m+m Base ergaenzten Kopfinformationen.
3. Erfassen Sie danach die Zeilen.
4. Pruefen Sie die durch m+m Base ergaenzten Zeileninformationen.
5. Reagieren Sie auf Hinweise aus Kreditlimit- oder Statuslogik, bevor Sie den Beleg weiterverarbeiten.

Da sowohl Kopf- als auch Zeilenseiten erweitert werden, ist die Trennung zwischen Kopfdaten und Positionsdaten fachlich wichtig. Pflegen Sie daher steuernde Informationen zuerst im Kopf und pruefen Sie anschliessend die Wirkung in den Zeilen.

### Einkauf: Angebote und Auftraege

Das gleiche Muster gilt im Einkauf. m+m Base erweitert mindestens folgende Standardseiten:

1. **Einkaufsangebot**
2. **Einkaufsangebot Zeilen**
3. **Einkaufsauftrag**
4. **Einkaufsauftrag Zeilen**
5. **Rahmeneinkaufsauftrag**
6. **Rahmeneinkaufsauftrag Zeilen**
7. **Rahmeneinkaufsauftraege**

Empfohlener Ablauf:

1. Oeffnen Sie zuerst den Kopf des Einkaufsbelegs.
2. Pflegen Sie die durch die Erweiterung benoetigten Zusatzangaben.
3. Erfassen Sie danach die Zeilen.
4. Kontrollieren Sie, ob Status- oder andere Zusatzinformationen konsistent sind.
5. Fuehren Sie erst danach die naechsten Standardprozesse wie Freigabe, Bestellung oder weitere Bearbeitung aus.

### Kreditlimit am Debitor pruefen

Fuer die operative Arbeit mit Kreditlimiten stehen zusaetzliche Seiten wie **Kreditlimit** und **Kreditlimit bearbeiten** zur Verfuegung. Nutzen Sie diese Seiten, wenn ein Debitor gesondert geprueft oder angepasst werden muss.

Typischer Ablauf:

1. Oeffnen Sie die **Debitorkarte**.
2. Wechseln Sie bei Bedarf in die kreditlimitbezogenen Detailseiten.
3. Pruefen Sie vorhandene Werte, Versichererzuordnung und Protokolle.
4. Aendern Sie Werte nur, wenn Ihre Rolle dies erlaubt.
5. Kontrollieren Sie anschliessend die Auswirkungen in offenen Verkaufsbelegen.

## Historie und Nachverfolgung

### Kreditlimitueberschreitungen

Die Seite **Kreditlimitueberschreitungen** dient der Nachverfolgung von kreditlimitbezogenen Vorgaengen. Nutzen Sie diese Liste, wenn Sie nachvollziehen wollen, wann ein Grenzwert ueberschritten wurde oder welche Bearbeitung anschliessend erfolgt ist.

### Belegstatus Aenderungsprotokoll

Mit **Belegstatus Aenderungsprotokoll** pruefen Sie, wann ein Status gewechselt wurde. Diese Seite ist besonders hilfreich, wenn der Fachbereich nachvollziehen muss, weshalb ein Beleg in seinem aktuellen Zustand steht.

Empfohlene Anwendung:

1. Oeffnen Sie den betroffenen Beleg oder die betroffene Statusdefinition.
2. Wechseln Sie in das **Belegstatus Aenderungsprotokoll**.
3. Pruefen Sie die Reihenfolge der Aenderungen.
4. Vergleichen Sie die Aenderung mit der zugrunde liegenden Ereigniszuweisung.

## Graphische und technische Hilfsseiten

Das Modul enthaelt zusaetzlich Seiten wie **Graph**, **Nodeflow Editor**, **Node Subform**, **Edge Subform**, **Package Subform**, **Packaging Viewer**, **Report Preview**, **Signature** und **PDF Viewer Part**. Diese Seiten deuten auf technische oder komponentenbasierte Unterstuetzung fuer andere Module hin.

Aus Anwendersicht gilt:

1. Nutzen Sie diese Seiten nur dann direkt, wenn Ihr Fachprozess oder ein angebundenes Modul Sie dorthin fuehrt.
2. Richten Sie Stammdaten und operative Belege zuerst in den fachlichen Hauptseiten ein.
3. Stimmen Sie den Einsatz dieser Spezialseiten mit Key Usern oder dem internen Modulverantwortlichen ab.

## FAQ und Troubleshooting

### Warum greift die Kreditlimitlogik nicht wie erwartet?

Pruefen Sie zuerst die **Kreditlimit Einrichtung**, dann die Stammdaten in **Kreditversicherer**, danach die Berechtigung in **Benutzer Einrichtung** und zuletzt die Debitorendaten.

### Warum ist ein Statuswechsel im Beleg nicht nachvollziehbar?

Oeffnen Sie **Belegstatus**, **Statusereigniszuweisung** und anschliessend das **Belegstatus Aenderungsprotokoll**. Meist fehlt entweder eine Zuweisung oder die Reihenfolge der Pflege ist nicht konsistent.

### Warum erscheinen zusaetzliche Felder in manchen Belegen, in anderen aber nicht?

m+m Base erweitert mehrere Standardbelegarten getrennt. Pruefen Sie daher, ob Sie im richtigen Belegtyp arbeiten, zum Beispiel in **Verkaufsauftrag** statt **Verkaufsangebot** oder in **Rahmeneinkaufsauftrag** statt **Einkaufsauftrag**.

### Wo pruefe ich, welche Stammdaten zuerst gepflegt werden muessen?

Beginnen Sie immer mit **Kreditlimit Einrichtung**, **Belegstatus**, **Status**, **Statusereignis** und **Statusereigniszuweisung**. Danach folgen Benutzer-, Debitoren- und Belegdaten.

## Typische Anwendungsfaelle

### Verkaufsauftrag mit Kreditlimitpruefung

**Ausloeser:** Ein Vertriebsmitarbeiter erfasst einen neuen Auftrag fuer einen bestehenden Debitor.

**Einstieg in BC:** Der Anwender oeffnet ueber **Tell Me** den **Verkaufsauftrag** oder wechselt aus der Debitorensicht in einen neuen Auftrag.

**Kernablauf:**

1. Der Anwender erfasst zuerst den Belegkopf.
2. Danach werden die Auftragszeilen gepflegt.
3. Waerend der Bearbeitung wirken die durch m+m Base erweiterten Kopf- und Zeileninformationen.
4. Bei kreditlimitbezogenen Auffaelligkeiten prueft der Anwender die Debitorensicht und bei Bedarf die Seiten **Kreditlimit** oder **Kreditlimit bearbeiten**.
5. Falls eine Ueberschreitung vorliegt, wird die Entscheidung anhand der internen Berechtigungen und der Einrichtung getroffen.

**Abschluss:** Der Anwender kontrolliert spaeter die Liste **Kreditlimitueberschreitungen**, wenn der Vorgang nachverfolgt werden muss.

### Statussteuerung fuer einen Einkaufsauftrag

**Ausloeser:** Ein Einkaeufer muss einen vorhandenen Beleg in einen definierten Bearbeitungszustand ueberfuehren.

**Einstieg in BC:** Der Anwender oeffnet ueber **Tell Me** den **Einkaufsauftrag**.

**Kernablauf:**

1. Der Belegkopf wird geoeffnet.
2. Die von m+m Base eingeblendeten Zusatzinformationen werden geprueft.
3. Der Anwender bearbeitet die Zeilen nur dann weiter, wenn der benoetigte Status oder das zugehoerige Ereignis korrekt eingerichtet ist.
4. Falls ein Status nicht erreichbar ist, prueft der Anwender zuerst **Status**, dann **Statusereignis** und zuletzt **Statusereigniszuweisung**.

**Abschluss:** Die Nachverfolgung erfolgt ueber **Belegstatus Aenderungsprotokoll**.

### Pflege neuer Statuslogik durch einen Key User

**Ausloeser:** Der Fachbereich fuehrt einen neuen Bearbeitungszustand fuer Belege ein.

**Einstieg in BC:** Der Key User startet mit **Belegstatus**, **Status** und **Statusereignis**.

**Kernablauf:**

1. Neue Statusdefinition anlegen.
2. Passende Stati pflegen.
3. Ausloesende Ereignisse erfassen.
4. Die Kombination in **Statusereigniszuweisung** verbinden.
5. Den Ablauf in einem Testbeleg pruefen.

**Abschluss:** Aenderungen und Testergebnisse werden spaeter ueber die Protokollseite kontrolliert.

### Terminarten fuer operative Belege vorbereiten

**Ausloeser:** Im Unternehmen werden neue Fristen oder Terminlogiken benoetigt.

**Einstieg in BC:** Der Anwender oeffnet **Terminarten**.

**Kernablauf:**

1. Neue Terminart anlegen.
2. Definition mit dem Fachbereich abstimmen.
3. In einem Verkaufs- oder Einkaufsbeleg pruefen, ob die Terminlogik wie erwartet verfuegbar ist.
4. Bei Bedarf die Grundparameter in den Einrichtungsseiten nachziehen.

**Abschluss:** Die neue Terminart steht danach fuer die operative Belegbearbeitung zur Verfuegung.
