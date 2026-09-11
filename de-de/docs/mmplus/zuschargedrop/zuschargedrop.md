---
title: Anwenderhandbuch m+m Additional Lot Information with Dropzone
---

# Anwenderhandbuch m+m Additional Lot Information with Dropzone

## Einleitung

Die Erweiterung **m+m Additional Lot Information with Dropzone** verbindet drei m+m-Module innerhalb von Microsoft Dynamics 365 Business Central: **m+m Additional Lot Information**, **m+m Dropzone** und **m+m Medienspeicher**. Sie sorgt dafür, dass Dokumente und Bilder, die per **DropZone** an einer Charge hinterlegt wurden, automatisch mit einer daraus abgeleiteten Charge mitwandern.

Der fachliche Hintergrund: In der **m+m Additional Lot Information** kann eine Charge auf eine **ursprüngliche Charge** verweisen (Felder **Ursprüngliche Artikel-Nr.**, **Ursprüngliche Chargennr.** und **Ursprünglicher Variantencode** auf der **Chargennr.-Informationskarte**). Legt der Anwender eine solche abgeleitete Charge an oder ändert er deren Ursprungsangaben, überträgt diese Erweiterung die per DropZone abgelegten **Anhänge** der Ursprungscharge auf die neue Charge – gesteuert über einen einzigen Schalter in der **Medienspeicher-Einrichtung**.

**Zielgruppe:** Primär **operative Anwender** in Lager, Qualität und Logistik, die im Tagesgeschäft Chargen anlegen bzw. Chargeninformationen pflegen und dabei die zugehörigen Dokumente sofort an der abgeleiteten Charge sehen möchten. **Sekundär** richtet sich das Kapitel **Einrichtung** an Administratoren bzw. Key-User, die die Funktion einmalig unternehmensweit aktivieren.

**Kurzer Prozessüberblick:**

1. Der Administrator aktiviert in der **Medienspeicher-Einrichtung** den Schalter **Anhang von der ursprünglichen Charge übertragen**.
2. Ein Anwender pflegt an einer Charge die **Ursprüngliche Chargennr.** (und **Ursprüngliche Artikel-Nr.**).
3. Beim Speichern der Charge kopiert die Erweiterung alle DropZone-Anhänge der Ursprungscharge automatisch auf die abgeleitete Charge, sofern dort noch nicht vorhanden.

Es gibt in dieser Erweiterung **keinen** eigenen Beleg, keine Buchung und keine manuelle Schaltfläche für die Übertragung – der Ablauf läuft **automatisch** im Hintergrund, sobald der Schalter gesetzt ist.

## Schnellstart für Anwender

Der schnellste Weg zum Ergebnis besteht aus einer einmaligen Einrichtung und dem laufenden Pflegen der Ursprungsangaben.

1. **Zuerst – Funktion aktivieren (einmalig, Administrator):** Öffnen Sie über **Suchen** die **Medienspeicher-Einrichtung** und aktivieren Sie im Bereich **Dropzone** den Schalter **Anhang von der ursprünglichen Charge übertragen**. Wenn dieser Schalter nicht gesetzt ist, findet keine Übertragung statt.
2. **Danach – Ursprungscharge hinterlegen (Anwender):** Öffnen Sie die **Chargennr.-Informationskarte** der abgeleiteten Charge und tragen Sie die **Ursprüngliche Artikel-Nr.** und die **Ursprüngliche Chargennr.** (sowie ggf. den **Ursprünglichen Variantencode**) ein.
3. **Ergebnis:** Beim Speichern werden die per **DropZone** an der Ursprungscharge abgelegten **Anhänge** automatisch auf die abgeleitete Charge übertragen und erscheinen dort in der DropZone-Faktenbox.

> Voraussetzung: An der Ursprungscharge müssen bereits Anhänge über die DropZone abgelegt sein, und der **Medienspeicher** muss – wie für die DropZone üblich – eingerichtet sein (siehe **Einrichtung**).

## Einrichtung

Die gesamte Einrichtung dieser Erweiterung findet auf **einer** Seite statt: der **Medienspeicher-Einrichtung**. Diese Seite gehört zum Modul **m+m Medienspeicher**; die vorliegende Erweiterung ergänzt sie um den Bereich **Dropzone** mit einem einzigen Schalter. Da Business Central dem Anwender **eine** zusammenhängende Seite anzeigt, dokumentiert dieses Handbuch die **komplette** Seite – Basisfelder des Medienspeichers und das Zusatzfeld dieser Erweiterung gemeinsam.

**Einstieg:** Öffnen Sie über **Suchen** die **Medienspeicher-Einrichtung**. Es handelt sich um eine unternehmensweite Einrichtungsseite (ein Datensatz pro Mandant); sie wird beim ersten Öffnen automatisch angelegt.

### Anhangübertragung einrichten

**Wer und wann:** Diese Einrichtung nimmt ein **Administrator** oder **Key-User** einmalig vor der ersten Nutzung vor. Sie steuert das gesamte Modulverhalten und wird im Tagesgeschäft von den Anwendern auf der **Chargennr.-Informationskarte** genutzt (siehe **Stammdaten** und **Automatischer Ablauf**).

**Ablauf (in Abhängigkeitsreihenfolge):**

1. **Zuerst – Speicherort festlegen:** Wählen Sie im Feld **Speicherungsart**, wo der **Medienspeicher** die Dateien ablegt (**Datenbank**, **Azure Blob Storage** oder **OneDrive**). Diese Einstellung ist die Grundlage dafür, dass DropZone-Anhänge überhaupt gespeichert und später kopiert werden können. Füllen Sie je nach Auswahl die zugehörigen Verbindungsfelder aus (siehe Feldtabelle) und prüfen Sie die Verbindung mit **Verbindung testen**.
2. **Danach – Übertragung aktivieren:** Aktivieren Sie im Bereich **Dropzone** den Schalter **Anhang von der ursprünglichen Charge übertragen**. Erst damit wird die automatische Kopie der Anhänge scharf geschaltet.
3. **Schließlich – operativer Abschluss im Tagesgeschäft:** Die Kette wird ohne weitere Schaltfläche abgeschlossen: Sobald ein Anwender an einer Charge die **Ursprüngliche Chargennr.** und **Ursprüngliche Artikel-Nr.** pflegt und speichert, werden die Anhänge automatisch übertragen (siehe **Automatischer Ablauf**).

**Feldtabelle – Medienspeicher-Einrichtung (Bereiche Speicherort, Azure Blob Storage, OneDrive, Dropzone):**

| Einrichtung | Erläuterung |
|---|---|
| **Speicherungsart** | Legt fest, wohin der Medienspeicher – und damit die DropZone-Anhänge – abgelegt wird. Die Auswahl steuert, welche Verbindungsfelder darunter aktiv sind. **Datenbank:** Wenn ausgewählt, werden Anhänge direkt in der Business-Central-Datenbank gespeichert; es sind keine externen Verbindungsdaten nötig. **Azure Blob Storage:** Wenn ausgewählt, werden Anhänge in einem Azure-Speicher abgelegt; die Felder **Access Key**, **Storage Account** und **Storage Container** werden bearbeitbar und müssen gefüllt sein. **OneDrive:** Wenn ausgewählt, werden Anhänge in OneDrive abgelegt; die OneDrive-Felder (**Anwendungs-ID (Client)**, **Geheimschlüssel**, **Verzeichnis-ID (Mandant)**, **Onedrive Email**, **Delegierte Genehmigungen**) werden bearbeitbar. |
| **Access Key** | Wenn die Speicherungsart **Azure Blob Storage** ist, hinterlegen Sie hier den Zugriffsschlüssel des Speicherkontos; ohne gültigen Schlüssel schlägt **Verbindung testen** fehl und es können keine Anhänge gespeichert oder kopiert werden. (Als Kennwortfeld maskiert.) |
| **Storage Account** | Wenn die Speicherungsart **Azure Blob Storage** ist, geben Sie hier den Namen des Azure-Speicherkontos an; er bestimmt, in welchem Konto die Dateien liegen. |
| **Storage Container** | Wenn die Speicherungsart **Azure Blob Storage** ist, legen Sie hier den Container fest, in dem die Dateien innerhalb des Speicherkontos abgelegt werden. |
| **Anwendungs-ID (Client)** | Wenn die Speicherungsart **OneDrive** ist, hinterlegen Sie hier die Client-ID der registrierten Azure-App; sie ermöglicht die Anmeldung von Business Central an OneDrive. Ohne diesen Wert ist keine OneDrive-Ablage möglich. |
| **Geheimschlüssel** | Wenn die Speicherungsart **OneDrive** ist, hinterlegen Sie hier das zugehörige Client-Geheimnis der Azure-App; zusammen mit der Anwendungs-ID authentifiziert es den Zugriff. (Als Kennwortfeld maskiert.) |
| **Verzeichnis-ID (Mandant)** | Wenn die Speicherungsart **OneDrive** ist, geben Sie hier die Verzeichnis-/Mandanten-ID (Tenant) an; sie bestimmt, in welchem Azure-AD-Mandanten die Anmeldung erfolgt. |
| **Onedrive Email** | Wenn die Speicherungsart **OneDrive** ist, hinterlegen Sie hier das OneDrive-Postfach bzw. den Benutzer, in dessen Ablage die Dateien gespeichert werden. |
| **Delegierte Genehmigungen** | Wenn die Speicherungsart **OneDrive** ist, steuert dieses Feld, ob der Zugriff mit delegierten Berechtigungen (im Namen eines angemeldeten Benutzers) erfolgt; damit bestimmen Sie das Berechtigungsmodell der OneDrive-Anbindung. |
| **Anhang von der ursprünglichen Charge übertragen** | Der zentrale Schalter dieser Erweiterung. **Wenn aktiviert**, kopiert Business Central beim Anlegen oder Ändern einer Charge mit hinterlegter Ursprungscharge automatisch alle DropZone-Anhänge der Ursprungscharge auf die abgeleitete Charge. **Wenn nicht aktiviert**, bleibt die Chargenpflege unverändert; es werden keine Anhänge übertragen und der Anwender müsste Dokumente an der neuen Charge manuell per DropZone ablegen. |

**Aktion auf dieser Seite:**

- **Verbindung testen** – prüft die Verbindung zum externen Speicher. **Wenn** die Speicherungsart **Azure Blob Storage** oder **OneDrive** ist, führen Sie diese Aktion nach dem Ausfüllen der Verbindungsfelder aus, um sicherzustellen, dass Anhänge tatsächlich gespeichert und später kopiert werden können. Bei der Speicherungsart **Datenbank** ist die Aktion nicht erforderlich.

**Validierung/Abhängigkeit:** Die Übertragung greift nur, wenn (a) der Schalter **Anhang von der ursprünglichen Charge übertragen** aktiv ist **und** (b) an der abgeleiteten Charge sowohl **Ursprüngliche Artikel-Nr.** als auch **Ursprüngliche Chargennr.** gefüllt sind. Fehlt eine dieser Angaben, unterbleibt die Kopie (siehe **Automatischer Ablauf**). Querverweis: die Pflege der Ursprungsangaben ist unter **Stammdaten** beschrieben.

## Stammdaten

Diese Erweiterung bringt **keine** eigenen Stammdatenseiten mit. Sie stützt sich auf die **Chargennr.-Information** aus dem Modul **m+m Additional Lot Information** und auf die per **DropZone** abgelegten **Anhänge**. Beide sind Voraussetzung für die automatische Übertragung und werden hier so weit beschrieben, wie es für die Nutzung dieser Erweiterung nötig ist.

### Ursprungscharge auf der Chargennr.-Informationskarte pflegen

**Wer und wann:** Anwender in Lager/Qualität pflegen diese Angaben, sobald feststeht, aus welcher Ursprungscharge eine Charge abgeleitet wurde. Die Angaben stammen aus dem Modul **m+m Additional Lot Information** und sind die Auslöser für die Anhangübertragung dieser Erweiterung.

**Relevante Felder (Chargennr.-Informationskarte):**

| Feld | Erläuterung |
|---|---|
| **Ursprüngliche Artikel-Nr.** | Verweist auf die Artikelnummer der Ursprungscharge. **Wenn gefüllt** (zusammen mit der Ursprünglichen Chargennr.), identifiziert dieses Feld gemeinsam die Ursprungscharge, von der die Anhänge kopiert werden. |
| **Ursprüngliche Chargennr.** | Verweist auf die Chargennummer der Ursprungscharge. **Wenn gefüllt**, sucht die Erweiterung deren DropZone-Anhänge und überträgt sie auf die aktuelle Charge. Ist das Feld leer, findet keine Übertragung statt. |
| **Ursprünglicher Variantencode** | Grenzt die Ursprungscharge zusätzlich auf eine bestimmte Variante ein. **Wenn gefüllt**, wird die Ursprungscharge exakt nach Artikel, Variante und Chargennr. bestimmt; bei variantengeführten Artikeln verhindert dies eine Verwechslung. |

**Prozessschritt:** Öffnen Sie die **Chargennr.-Informationskarte** der abgeleiteten Charge, tragen Sie zuerst die **Ursprüngliche Artikel-Nr.** und danach die **Ursprüngliche Chargennr.** ein und speichern Sie. Voraussetzung ist, dass der Schalter aus dem Kapitel **Einrichtung** gesetzt ist (Querverweis: **Anhangübertragung einrichten**).

### DropZone-Anhänge an der Charge

Die **DropZone** wird als separate Faktenbox auf der **Chargennr.-Informationskarte** angezeigt. Anwender legen dort Dokumente per Drag-and-drop ab; die Dateien werden im **Medienspeicher** gespeichert (Herkunft: Chargennr.-Information). Für diese Erweiterung sind diese Anhänge der **Quellbestand**: Genau die an der Ursprungscharge abgelegten Anhänge werden auf die abgeleitete Charge kopiert. Eine eigene Einrichtung der DropZone ist nicht erforderlich; maßgeblich ist allein die **Medienspeicher-Einrichtung** (siehe **Einrichtung**).

## Automatischer Ablauf (Übertragung der Anhänge)

Diese Erweiterung stellt dem Anwender **keine** Schaltfläche zum Übertragen bereit. Die Übertragung erfolgt **automatisch**, ausgelöst durch das Speichern einer Charge.

**Ablauf im Detail (aus dem Code abgeleitet):**

1. **Auslöser:** Ein Datensatz der **Chargennr.-Information** wird **angelegt** oder **geändert** (z. B. beim Erfassen der Ursprungsangaben). Beide Ereignisse lösen die Prüfung aus.
2. **Prüfung Ursprungsbezug:** Die Erweiterung prüft, ob an der Charge sowohl **Ursprüngliche Artikel-Nr.** als auch **Ursprüngliche Chargennr.** gefüllt sind. Ist eine Angabe leer, endet der Vorgang ohne Aktion.
3. **Prüfung Schalter:** Es wird geprüft, ob in der **Medienspeicher-Einrichtung** der Schalter **Anhang von der ursprünglichen Charge übertragen** aktiv ist. Ist er nicht gesetzt, endet der Vorgang.
4. **Ursprungscharge ermitteln:** Anhand von **Ursprüngliche Artikel-Nr.**, **Ursprünglicher Variantencode** und **Ursprünglicher Chargennr.** wird der passende Chargennr.-Informationssatz gesucht. Fehlt dort **Artikel-Nr.** oder **Chargennr.**, endet der Vorgang.
5. **Anhänge kopieren:** Alle **Medienspeicher**-Einträge der Ursprungscharge (Herkunft Chargennr.-Information) werden durchlaufen. Für jeden Eintrag wird geprüft, ob an der Zielcharge bereits ein Anhang mit **derselben Beschreibung** existiert. Nur wenn nicht, wird der Anhang – einschließlich des hinterlegten **Bilds**/der Datei – auf die Zielcharge kopiert und mit einer neuen laufenden Nummer angelegt.

**Was der Anwender sieht:** Nach dem Speichern erscheinen die kopierten Dokumente in der DropZone-Faktenbox der abgeleiteten Charge und können dort wie gewohnt geöffnet oder heruntergeladen werden. Vorhandene, gleichnamige Anhänge werden nicht doppelt angelegt.

## Berechtigungen

Die Erweiterung liefert die Berechtigungsgruppe **„All Permissions“** (Objektname **MuM ALDZ Permission**). Sie legt fest, welche Aktionen ein Anwender im Rahmen dieser Erweiterung ausführen darf, und umfasst die Ausführungsrechte für die beiden internen Codeunits (Verwaltung und Ereignisverarbeitung). Da die Übertragung automatisch beim Speichern der Charge läuft, benötigen Anwender darüber hinaus die üblichen Rechte an der **Chargennr.-Information** und am **Medienspeicher**. Weisen Sie die Berechtigungsgruppe den Benutzern bzw. Benutzergruppen zu, die mit Chargeninformationen und DropZone-Anhängen arbeiten.

## Typische Anwendungsfälle

Die folgenden Szenarien sind aus dem tatsächlichen, im Code verifizierten Verhalten abgeleitet.

### Anwendungsfall 1 – Abgeleitete Charge erhält die Dokumente der Ursprungscharge

1. **Auslöser:** Im Lager entsteht aus einer bestehenden Charge eine neue, abgeleitete Charge (z. B. durch Umpacken oder Aufteilen). Zur Ursprungscharge liegen bereits Prüfdokumente und Bilder in der DropZone vor.
2. **Einstieg in BC:** Der Anwender öffnet die **Chargennr.-Informationskarte** der neuen Charge.
3. **Kernablauf:** Er trägt die **Ursprüngliche Artikel-Nr.** und die **Ursprüngliche Chargennr.** (bei variantengeführten Artikeln zusätzlich den **Ursprünglichen Variantencode**) ein und speichert. Voraussetzung ist, dass der Administrator zuvor **Anhang von der ursprünglichen Charge übertragen** in der **Medienspeicher-Einrichtung** aktiviert hat.
4. **Abschluss:** Business Central kopiert automatisch alle DropZone-Anhänge der Ursprungscharge auf die neue Charge. Der Anwender findet sie sofort in der DropZone-Faktenbox der abgeleiteten Charge – ohne die Dateien erneut hochladen zu müssen.

### Anwendungsfall 2 – Ursprungscharge wird nachträglich ergänzt

1. **Auslöser:** Eine Charge wurde bereits angelegt, die zugehörige Ursprungscharge ist aber erst später bekannt.
2. **Einstieg in BC:** Der Anwender öffnet erneut die **Chargennr.-Informationskarte** der betroffenen Charge.
3. **Kernablauf:** Er ergänzt die **Ursprüngliche Chargennr.** und **Ursprüngliche Artikel-Nr.** und speichert die Änderung. Da auch das Ändern der Charge die Übertragung auslöst, ist kein weiterer Schritt nötig.
4. **Abschluss:** Die Anhänge der Ursprungscharge werden nachträglich übertragen. Bereits vorhandene, gleichnamige Anhänge bleiben unverändert und werden nicht doppelt angelegt.

## FAQ und Troubleshooting

### 1. Warum werden keine Anhänge auf die neue Charge übertragen?
Prüfen Sie zuerst, ob in der **Medienspeicher-Einrichtung** der Schalter **Anhang von der ursprünglichen Charge übertragen** aktiviert ist. Ohne diesen Schalter findet keine Übertragung statt.

### 2. Welche Angaben muss ich an der Charge pflegen, damit die Übertragung greift?
Es müssen **beide** Felder **Ursprüngliche Artikel-Nr.** und **Ursprüngliche Chargennr.** gefüllt sein. Fehlt eine der beiden Angaben, unterbleibt die Kopie.

### 3. Muss ich die Übertragung manuell starten?
Nein. Es gibt keine Schaltfläche. Die Übertragung läuft automatisch beim **Anlegen** oder **Ändern** der Chargennr.-Information.

### 4. Kann ich die Übertragung auch nachträglich auslösen?
Ja. Öffnen Sie die **Chargennr.-Informationskarte**, ergänzen oder ändern Sie die Ursprungsangaben und speichern Sie. Auch das Ändern der Charge stößt die Übertragung an.

### 5. Werden Anhänge doppelt angelegt, wenn ich die Charge mehrfach speichere?
Nein. Vor dem Kopieren wird geprüft, ob an der Zielcharge bereits ein Anhang mit **derselben Beschreibung** existiert. Nur fehlende Anhänge werden ergänzt.

### 6. Woher stammen die übertragenen Dokumente?
Aus den **Medienspeicher**-Einträgen der Ursprungscharge, also aus den per **DropZone** an der Ursprungscharge abgelegten Anhängen (Herkunft Chargennr.-Information).

### 7. Warum finde ich an der Ursprungscharge keine Anhänge zum Übertragen?
An der Ursprungscharge müssen zuvor Dokumente über die **DropZone** abgelegt worden sein. Ist die Ursprungscharge ohne Anhänge, gibt es nichts zu kopieren.

### 8. Welche Speicherungsart soll ich in der Medienspeicher-Einrichtung wählen?
Wählen Sie **Datenbank** für die Ablage direkt in Business Central, **Azure Blob Storage** oder **OneDrive** für eine externe Ablage. Bei den externen Varianten füllen Sie die zugehörigen Verbindungsfelder und prüfen die Verbindung mit **Verbindung testen**.

### 9. Was passiert, wenn die Ursprungscharge zu keiner gültigen Chargennr.-Information führt?
Kann die Ursprungscharge anhand von Artikel und Chargennr. nicht eindeutig ermittelt werden oder fehlt dort die Chargennr., bricht der Vorgang ohne Kopie und ohne Fehlermeldung ab.

### 10. Welche Berechtigungen benötigen die Anwender?
Weisen Sie die mitgelieferte Berechtigungsgruppe **„All Permissions“** (MuM ALDZ Permission) zu. Zusätzlich benötigen die Anwender die üblichen Rechte an der **Chargennr.-Information** und am **Medienspeicher**, da die Übertragung beim Speichern der Charge erfolgt.
