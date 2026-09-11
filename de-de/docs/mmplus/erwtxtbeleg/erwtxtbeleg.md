---
title: Anwenderhandbuch m+m Ext. Text Module with Report Package
---

# Anwenderhandbuch m+m Ext. Text Module with Report Package

## Einleitung

Dieses Modul verbindet zwei bestehende m+m-Erweiterungen miteinander: die **m+m Ext. Text Module**-App, in der Sie erweiterte Texte (Textvorlagen sowie beleg- und zeilenbezogene Texte) pflegen, und das **m+m Belegpaket**, das die m+m-Berichte und -Belege druckt. Das Modul selbst besitzt **keine eigenen Seiten, Felder oder Aktionen**. Seine Aufgabe ist es, beim Druck eines m+m-Berichts die zuvor erfassten erweiterten Texte automatisch an den richtigen Stellen des Belegs einzufügen.

Konkret sorgt das Modul dafür, dass

- erweiterte **Kopf- und Belegtexte** (Positionen **Kopftext**, **Fußtext**, **Vor Position**, **Nach Position**) im Bericht an der jeweils gewählten Stelle erscheinen und
- erweiterte **Zeilentexte** unterhalb der zugehörigen Belegzeile gedruckt werden,

und zwar für Verkaufs- und Einkaufsbelege, offene wie gebuchte (Angebot, Auftrag, Rechnung, Gutschrift, Lieferung, Wareneingang, Rücksendung).

**Zielgruppe.** Primär richtet sich dieses Handbuch an **operative Anwenderinnen und Anwender** im Verkauf und Einkauf, die Belege bearbeiten, erweiterte Texte an Kopf, Fuß, vor oder nach einer Position hinterlegen und anschließend den m+m-Beleg **drucken**. Sekundär angesprochen sind **Administratorinnen und Administratoren**, die einmalig die Einrichtung in den **Erweiterte Texteinstellungen** vornehmen.

**Kurzer Prozessüberblick.** Zuerst legt eine Administratorin oder ein Administrator fest, aus welcher Textquelle die Zeilentexte gezogen werden (Einrichtung). Danach hinterlegt der Anwender die erweiterten Texte am Beleg — je Position (Kopftext, Fußtext, Vor Position, Nach Position) und je Zeile. Beim Druck des m+m-Berichts fügt dieses Modul die Texte automatisch in den Beleg ein; ein separater Buchungs- oder Freigabeschritt ist dafür nicht erforderlich.

## Schnellstart für Anwender

Voraussetzung: Die erweiterten Textvorlagen und die Zuordnung zu Belegen sind im Modul **m+m Ext. Text Module** angelegt (siehe Abschnitt *Voraussetzungen aus dem Modul m+m Ext. Text Module*).

1. **Einrichtung prüfen (einmalig, durch die Administration).** Öffnen Sie die Seite **Erweiterte Texteinstellungen** und entscheiden Sie über das Kennzeichen **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer**, aus welcher Quelle die **Zeilentexte** in den Bericht gelangen (siehe Kapitel *Einrichtung*).
2. **Beleg öffnen.** Öffnen Sie den betreffenden Verkaufs- oder Einkaufsbeleg (z. B. eine Verkaufsrechnung oder eine Einkaufsbestellung).
3. **Kopf-/Belegtext hinterlegen.** Erfassen Sie über die Aktion **Erweiterter Text** am Belegkopf den Text für die gewünschte Position — **Kopftext**, **Fußtext**, **Vor Position** oder **Nach Position**.
4. **Zeilentext hinterlegen (optional).** Erfassen Sie für einzelne Belegzeilen den zugehörigen erweiterten Zeilentext.
5. **Beleg drucken.** Lösen Sie den Druck des m+m-Berichts aus (Aktion **Drucken** bzw. **Berichte** am Beleg). Das Modul fügt die erfassten Texte automatisch an den konfigurierten Stellen ein.

Der Schnellstart entspricht dem Ablauf aus dem Kapitel *Wie die Texte in den Bericht gelangen*; die Reihenfolge (Einrichtung → Text erfassen → drucken) wird dort und in den *Nutzungsbeispielen* mit denselben Schritten wiederholt.

## Einrichtung

Die Einrichtung dieses Moduls ist bewusst schlank: Das Modul liest genau **ein** Steuerungskennzeichen aus der zentralen Setup-Karte des Moduls **m+m Ext. Text Module**. Alle übrigen Felder dieser Karte steuern andere Funktionen der Textmodul-App und sind dort dokumentiert; sie werden hier zur Orientierung genannt, damit Sie die eine relevante Einstellung sicher finden.

### Erweiterte Texteinstellungen — das steuernde Kennzeichen

**Wer richtet ein?** Eine Administratorin oder ein Administrator, **einmalig** vor der ersten Nutzung (Unternehmenseinrichtung).

**Einstieg:** Die **Erweiterte Texteinstellungen** sind eine unternehmensweite Einrichtungskarte (ein Datensatz je Mandant). Öffnen Sie die Seite über die Suche (**Suchen**) mit dem Begriff *Erweiterte Texteinstellungen*. Die Karte dient als Einrichtungspunkt des Moduls m+m Ext. Text Module; einen übergeordneten Stammdaten-Einstieg gibt es für diese Singleton-Einrichtung nicht.

**Welches Verhalten wird hier gesteuert?** Für dieses Modul ist ausschließlich das folgende Kennzeichen relevant. Es entscheidet, aus welcher Textquelle die **Zeilentexte** in den Bericht übernommen werden:

| Einrichtung | Erläuterung |
|---|---|
| erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer | Wenn **aktiviert**, werden als Zeilentext im Bericht die Texte vom **Drucktyp InfoBox** (mit leerem Nebendruck Typ) gedruckt; die Anwenderin bzw. der Anwender kann so den intern gepflegten Infobox-Text ohne separate Berichtsvorlage auf den Beleg bringen. Wenn **nicht aktiviert**, werden als Zeilentext die Texte vom **Drucktyp Bericht** (mit leerem Nebendruck Typ) gedruckt; dann greift ausschließlich der ausdrücklich für den Druck vorgesehene Text. Das Kennzeichen wirkt nur auf **Zeilentexte** — Kopf-, Fuß-, Vor- und Nach-Positionstexte am Belegkopf sind davon nicht betroffen. |

**Prozessschritt.** Setzen Sie das Kennzeichen entsprechend Ihrer Textstrategie **vor** der ersten Belegausgabe. Die Wirkung zeigt sich im Kapitel *Tägliche Arbeit* beim Druck der Zeilentexte (Querverweis dorthin).

### Übrige Felder der Einrichtungskarte (Orientierung)

Die Seite **Erweiterte Texteinstellungen** zeigt im Register *Allgemein* weitere Felder. Diese steuern **andere** Funktionen des Moduls m+m Ext. Text Module (Textkopie, Nummernserie der Vorlagen, Platzhalter, E-Mail-Texte, Hintergrundverarbeitung) und **nicht** das Drucken erweiterter Texte auf m+m-Berichten. Sie sind im Handbuch des Moduls m+m Ext. Text Module ausführlich beschrieben. Zur schnellen Zuordnung:

| Feld | Erläuterung |
|---|---|
| Vorlagennummern | Wenn gesetzt, vergibt BC neue Textvorlagen aus dieser Nummernserie; betrifft die Vorlagenpflege, nicht den Berichtsdruck. |
| Sprachcode | Wenn gesetzt, wird diese Sprache für die Textpflege vorbelegt; der Berichtsdruck selbst nutzt die Sprache des gedruckten Belegs. |
| Text kopieren | Wenn aktiviert, werden erweiterte Texte beim Kopieren von Belegen mit übernommen; betrifft die Belegkopie, nicht diesen Druckvorgang. |
| Überschreiben von Ext. Text | Wenn gesetzt, dürfen bestehende erweiterte Texte beim Übertragen überschrieben werden; steuert die Textübernahme, nicht den Druck. |

Für den Druck erweiterter Texte auf m+m-Berichten ist von diesen Feldern **kein** weiteres relevant; maßgeblich bleibt allein das oben beschriebene Kennzeichen.

### Belegtexte für den Druck einrichten

Damit erweiterte Texte tatsächlich auf einem m+m-Beleg erscheinen, ist eine mehrstufige Vorbereitung nötig. Diese Kette wird hier in Abhängigkeitsreihenfolge beschrieben; die eigentliche Erfassung der Vorlagen erfolgt im Modul m+m Ext. Text Module, das Andrucken erledigt dieses Modul.

**Prozesseinstieg.** Konfiguriert wird durch Administration bzw. Key-User, **bevor** der erste Beleg mit erweitertem Text gedruckt wird. Genutzt wird das Ergebnis in der *Täglichen Arbeit* beim Belegdruck.

**Einrichtungsschritte (in Abhängigkeitsreihenfolge):**

1. **Textvorlagen anlegen.** Legen Sie im Modul m+m Ext. Text Module die **Erweiterte Textvorlage** an (Seite **Erweiterte Textvorlage**/Vorlagenkarte). Wenn eine Vorlage mit **Drucktyp Bericht** angelegt wird, kann sie auf Belegen gedruckt werden; mit **Drucktyp InfoBox** dient sie der internen Anzeige, mit **Drucktyp Mail** dem E-Mail-Versand.
2. **Nebendruck Typ wählen (nur bei Drucktyp Bericht).** Wenn der Drucktyp **Bericht** ist, bestimmen Sie über den **Nebendruck Typ**, an welcher Stelle des Berichts der Text erscheint (siehe Werteübersicht unten). Bleibt der Nebendruck Typ **(leer)**, handelt es sich um einen **Zeilentext**.
3. **Vorlage dem Beleg/Prozess zuordnen.** Ordnen Sie die Vorlage über das **Zuweisungsarbeitsblatt** dem gewünschten Beleg bzw. der Position zu. Wenn die Zuordnung gesetzt ist, steht der Text beim Belegdruck zur Verfügung.
4. **Zeilentextquelle festlegen (optional).** Setzen Sie in den **Erweiterte Texteinstellungen** das Kennzeichen **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** entsprechend Ihrer Strategie (siehe oben). Wenn aktiviert, wird der Infobox-Text als Zeilentext gedruckt, andernfalls der Berichtstext.

**Operativer Abschluss.** Der Anwender öffnet den Beleg, erfasst über die Aktion **Erweiterter Text** die Positionstexte und druckt den m+m-Bericht (Kapitel *Tägliche Arbeit*). Damit ist die Kette geschlossen.

### Nebendruck Typ — Werteübersicht (Position im Bericht)

Der **Nebendruck Typ** ist dem **Drucktyp** untergeordnet und kann nur beim Drucktyp **Bericht** verwendet werden. Er legt die Druckstelle des Textes fest. Alle vom System vorgesehenen Werte:

| Nebendruck Typ | Erläuterung |
|---|---|
| Kopfzeile | Wenn ausgewählt, wird der Text im **Kopfbereich** des Berichts gedruckt (Belegposition **Kopftext**). |
| Fußzeile | Wenn ausgewählt, wird der Text im **Fußbereich** des Berichts gedruckt (Belegposition **Fußtext**). |
| Vor Position | Wenn ausgewählt, wird der Text **vor** der jeweiligen Belegposition gedruckt. |
| Nach Position | Wenn ausgewählt, wird der Text **nach** der jeweiligen Belegposition gedruckt. |
| (leer) | Wenn kein Nebendruck Typ gesetzt ist, gilt der Text als **Zeilentext** und wird unterhalb der zugehörigen Belegzeile gedruckt; die Quelle (InfoBox oder Bericht) steuert das Kennzeichen aus den Erweiterte Texteinstellungen. |

### Drucktyp — Werteübersicht

Der **Drucktyp** einer Textvorlage bestimmt, wozu der Text dient. Vom System vorgesehene Werte:

| Drucktyp | Erläuterung |
|---|---|
| Bericht | Wenn gewählt, ist der Text zum **Andruck auf Belegen** vorgesehen und wird von diesem Modul in den m+m-Bericht übernommen. Nur bei diesem Drucktyp ist ein **Nebendruck Typ** möglich. |
| InfoBox | Wenn gewählt, dient der Text der **internen Anzeige** in der Infobox am Beleg und wird normalerweise nicht gedruckt. Er wird nur dann als **Zeilentext** in den Bericht übernommen, wenn in den Erweiterte Texteinstellungen das Kennzeichen **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** aktiviert ist. |
| Mail | Wenn gewählt, ist der Text für den **E-Mail-Versand** vorgesehen; er wird von diesem Modul nicht in den Bericht gedruckt. |

## Tägliche Arbeit am Beleg

Dieser Abschnitt setzt die Einrichtung aus dem Kapitel *Einrichtung* voraus. Insbesondere steuert das Kennzeichen **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** aus den **Erweiterte Texteinstellungen**, aus welcher Quelle **Zeilentexte** gedruckt werden (Querverweis: Kapitel *Einrichtung*).

### Erweiterte Texte am Belegkopf erfassen

1. Öffnen Sie den Verkaufs- oder Einkaufsbeleg (offen oder — für Wiederdruck — den gebuchten Beleg).
2. Öffnen Sie über die Aktion **Erweiterter Text** die Texterfassung am Belegkopf.
3. Wählen Sie die gewünschte **Position** und erfassen Sie den Text:
   - **Kopftext** — erscheint im Kopfbereich des Berichts.
   - **Fußtext** — erscheint im Fußbereich des Berichts.
   - **Vor Position** — erscheint vor den Positionen.
   - **Nach Position** — erscheint nach den Positionen.
4. Formatieren Sie den Text bei Bedarf im Editor. Absätze (Umbrüche zwischen Absätzen) werden beim Druck automatisch in Zeilenumbrüche gewandelt, sodass der Text im Bericht sauber umbricht.

### Erweiterte Zeilentexte erfassen

1. Wählen Sie im Beleg die betreffende **Zeile**.
2. Erfassen Sie über **Erweiterter Text** den zeilenbezogenen Text.
3. Der Zeilentext wird beim Druck unterhalb der Belegzeile ausgegeben. Ob dabei der **InfoBox**- oder der **Bericht**-Text gezogen wird, hängt vom Einrichtungskennzeichen ab (siehe Einrichtung).

### Beleg mit erweiterten Texten drucken

1. Lösen Sie am Beleg den Druck des m+m-Berichts aus (Aktion **Drucken** bzw. **Berichte** / **m+m Belegpaket**).
2. Das Modul liest — passend zur Sprache des Belegs — die erfassten erweiterten Texte und fügt sie in den Bericht ein: Kopf-, Fuß-, Vor- und Nach-Positionstexte an den jeweiligen Stellen, Zeilentexte unter den Positionen.
3. Bilder, die in den Texten hinterlegt sind, werden ebenfalls an der jeweiligen Stelle mit ausgegeben.

Für **gebuchte** Belege (z. B. gebuchte Verkaufsrechnung, Lieferung, Wareneingang, Gutschrift, Rücksendung) werden die zum Buchungszeitpunkt gespeicherten erweiterten Texte gedruckt; das erneute Drucken eines gebuchten Belegs zeigt somit die dort gespeicherten Texte.

## Wie die Texte in den Bericht gelangen

Zum besseren Verständnis der Wirkzusammenhänge — vollständig aus dem Verhalten des Moduls abgeleitet:

- **Kopf-/Belegtexte.** Beim Aufbau der Berichtsdaten fragt das Belegpaket je Druckposition (Kopftext, Fußtext, Vor Position, Nach Position) beim Textmodul den passenden erweiterten Text des Belegs ab. Das Modul liefert diesen Text und schreibt ihn in den Berichtszeilenpuffer.
- **Zeilentexte.** Für jede Belegzeile liefert das Modul den erweiterten Zeilentext. Aus welcher Vorlagenquelle (Drucktyp **InfoBox** oder **Bericht**, jeweils mit leerem Nebendruck Typ) gelesen wird, entscheidet das Einrichtungskennzeichen.
- **Offene vs. gebuchte Belege.** Bei offenen Belegen stammen die Texte aus den belegbezogenen Texttabellen, bei gebuchten Belegen aus den gebuchten Texttabellen. So bleibt der Andruck bei Wiederholungsdrucken konsistent zum Buchungsstand.
- **Sprache.** Die Texte werden in der Sprache des gedruckten Belegs gelesen, damit fremdsprachige Belege die passenden Textfassungen andrucken.

## Voraussetzungen aus dem Modul m+m Ext. Text Module

Damit dieses Modul Texte drucken kann, müssen die Texte zuvor im Modul **m+m Ext. Text Module** existieren. Relevante Stammdaten dort (in diesem Modul nur referenziert, nicht selbst gepflegt):

- **Erweiterte Textvorlage** (Vorlagenkarte): mit **Vorlage Nr.**, **Textvorlage**, **Drucktyp**, **Startdatum**, **Enddatum**, **Zuweisungsarbeitsblatt** und — bei Drucktyp Bericht — **Nebendruck Typ**.
- **Zuweisungsarbeitsblatt**: verknüpft die Vorlage mit Belegen bzw. Positionen und dem gewünschten Prozess.

Die vollständige Pflege dieser Stammdaten ist im Handbuch des Moduls m+m Ext. Text Module beschrieben. Für den Berichtsdruck genügt es zu wissen, dass eine Vorlage mit **Drucktyp Bericht** und passendem **Nebendruck Typ** existieren und dem Beleg zugeordnet sein muss.

## FAQ und Troubleshooting

### 1. Warum erscheint mein erweiterter Text nicht auf dem Bericht?

Prüfen Sie den **Drucktyp** der Vorlage: Nur Texte vom Drucktyp **Bericht** werden regulär gedruckt. Ein Text vom Drucktyp **InfoBox** erscheint als Zeilentext nur, wenn in den **Erweiterte Texteinstellungen** das Kennzeichen **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** aktiviert ist. Texte vom Drucktyp **Mail** werden nicht gedruckt.

### 2. Was bewirkt das Kennzeichen „erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer“ genau?

Es steuert die Quelle der **Zeilentexte**: aktiviert wird der **InfoBox**-Text (mit leerem Nebendruck Typ) gedruckt, deaktiviert der **Bericht**-Text (mit leerem Nebendruck Typ). Auf Kopf-, Fuß-, Vor- und Nach-Positionstexte wirkt das Kennzeichen nicht.

### 3. Wie erreiche ich, dass ein Text im Briefkopf des Belegs steht?

Erfassen Sie den Text an der Position **Kopftext** (bzw. legen Sie die Vorlage mit Drucktyp **Bericht** und Nebendruck Typ **Kopfzeile** an). Für den Fußbereich nutzen Sie **Fußtext** bzw. Nebendruck Typ **Fußzeile**.

### 4. Wie bringe ich einen Hinweis direkt unter eine bestimmte Belegzeile?

Erfassen Sie einen **Zeilentext** an der betreffenden Zeile (Vorlage ohne Nebendruck Typ, also **(leer)**). Der Text wird unterhalb der Position gedruckt.

### 5. Wo liegt der Unterschied zwischen „Vor Position“ und „Nach Position“?

**Vor Position** druckt den Text oberhalb der jeweiligen Belegposition, **Nach Position** unterhalb. Beide gehören zu den Kopf-/Belegtexten am Belegkopf und werden je Position ausgewertet.

### 6. Warum werden meine Absätze im Bericht anders umgebrochen als im Editor?

Beim Druck wandelt das Modul Absatzwechsel automatisch in einfache Zeilenumbrüche um. Dadurch wird der Text im Bericht kompakt und ohne Leerabsätze dargestellt.

### 7. Kann ich Bilder in den erweiterten Texten drucken?

Ja. Enthält ein erweiterter Text ein Bild, wird es an derselben Stelle wie der Text in den Bericht übernommen und mitgedruckt.

### 8. Warum erscheinen auf dem fremdsprachigen Beleg die deutschen Texte nicht?

Die Texte werden in der **Sprache des Belegs** gelesen. Hinterlegen Sie die Übersetzung der Textvorlage in der benötigten Sprache; ohne passende Sprachfassung findet das Modul für diese Sprache keinen Text.

### 9. Ich habe die Vorlage geändert — warum zeigt der gebuchte Beleg den alten Text?

Für **gebuchte** Belege werden die zum Buchungszeitpunkt gespeicherten Texte gedruckt. Änderungen an der Vorlage wirken sich auf gebuchte Belege nicht rückwirkend aus.

### 10. Muss ich nach dem Erfassen der Texte etwas buchen oder freigeben, damit sie gedruckt werden?

Nein. Das Modul greift ausschließlich beim **Drucken** des m+m-Berichts. Ein zusätzlicher Buchungs- oder Freigabeschritt ist nicht nötig; es genügt, die Texte zu erfassen und den Beleg zu drucken.

## Typische Anwendungsfälle

### Anwendungsfall 1: Fester Kopftext auf jeder Verkaufsrechnung

**Auslöser.** Das Marketing bittet darum, auf jeder Verkaufsrechnung einen einheitlichen Einleitungstext im Kopfbereich zu drucken.

**Einstieg in BC.** Die Administration legt im Modul m+m Ext. Text Module eine **Erweiterte Textvorlage** mit **Drucktyp Bericht** und **Nebendruck Typ Kopfzeile** an und ordnet sie den Verkaufsrechnungen zu. Alternativ erfasst der Anwender am einzelnen Beleg über **Erweiterter Text** einen **Kopftext**.

**Kernablauf.**
1. Verkaufsrechnung öffnen.
2. Über **Erweiterter Text** den **Kopftext** erfassen bzw. die zugeordnete Vorlage nutzen.
3. Rechnung über die m+m-Berichtsausgabe **drucken**.

**Abschluss.** Der Kopftext erscheint im Kopfbereich der gedruckten Rechnung. Bei gebuchten Rechnungen wird der zum Buchungszeitpunkt gespeicherte Kopftext gedruckt.

### Anwendungsfall 2: Positionsbezogener Hinweis unter einer Auftragszeile

**Auslöser.** Eine Sachbearbeiterin muss zu einem bestimmten Artikel einen Hinweis (z. B. Pflegehinweis) direkt unter der Position drucken.

**Einstieg in BC.** Verkaufsauftrag öffnen, betreffende **Zeile** markieren.

**Kernablauf.**
1. Über **Erweiterter Text** den **Zeilentext** zur markierten Zeile erfassen (Vorlage ohne Nebendruck Typ, also **(leer)**).
2. Prüfen, ob die Zeilentextquelle korrekt eingerichtet ist: bei aktiviertem Kennzeichen **erweiterter Text Infobox Texte im Bericht mit Druck Untertyp leer** wird der InfoBox-Text gedruckt, sonst der Bericht-Text (Querverweis: *Einrichtung*).
3. Auftrag über den m+m-Bericht **drucken**.

**Abschluss.** Der Hinweis erscheint unmittelbar unter der betreffenden Auftragszeile.

### Anwendungsfall 3: Fußtext an den Lieferanten auf der Einkaufsbestellung

**Auslöser.** Der Einkauf möchte auf jeder Bestellung im Fußbereich ergänzende Bedingungen an den Lieferanten drucken.

**Einstieg in BC.** Einkaufsbestellung öffnen.

**Kernablauf.**
1. Über **Erweiterter Text** am Belegkopf den Text an der Position **Fußtext** erfassen.
2. Bestellung über die m+m-Berichtsausgabe **drucken**.

**Abschluss.** Der Fußtext erscheint im Fußbereich der gedruckten Bestellung; ebenso bei den zugehörigen gebuchten Einkaufsbelegen (Wareneingang, Einkaufsrechnung, Gutschrift, Rücksendung), sofern dort erfasst.
