---
title: User Guide m+m Material Properties
---

# User Guide m+m Material Properties

Öffnen Sie die Einrichtung, indem Sie im Webclient den Suchbegriff „Materialeigenschaften Einrichtung“ eingeben und den gleichlautenden Link anklicken.

[image]

Es öffnet sich die Seite „Materialeigenschaften Einrichtung“.

[image]

Erläuterungen zu den Feldern der „Materialeigenschaften Einrichtung“:

Feldname | Erläuterung | 
Fixe Werte nur am Basisartikel editierbar | Ändern von Eigenschaftswerten, die als Fix gekennzeichnet sind, können nur in einem Artikel geändert werden, der als „Basisartikel“ eingestellt ist. | 
Tausender Punkt für Beschreibung unterdrücken | Ist der Haken gesetzt, so wird der 1000er Punkt in der Beschreibung 1 und 2 nicht ausgegeben, andernfalls soll er angezeigt werden. | 
Optimierten Matchcodesuchparameter verwenden | Anstelle der Standard BC-Suche werden die Filterfunktionen für die Matchcodesuche aktiviert. | 
Erw. Matchcodesuche verwenden | Aktiviert die erweiterte Matchcodesuche in den Belegzeilen. | 
Tausender Punkt unterdrücken | Unterdrückt den Tausenderpunkt bei Dezimalzahlen bei der Erstellung des Matchcodes. Nur für den Matchcode und die Materialsuche zuständig. | 
Artikelvarianten Feature verwenden | Kann nur genutzt werden, wenn „Fixe Werte nur am Basisartikel editierbar“ aktiviert ist. Aktiviert die Materialeigenschaften und ihre Funktionen auf Artikelvariantenebene. | 
Verkaufsangebot | Aktiviert die Chargenreservierung im Verkaufsangebot | 
Verkaufsauftrag | Aktiviert die Chargenreservierung im Verkaufsauftrag | 
Logistischer Lagero

en auf Artikelvariantenebene. | 
Verkaufsangebot | Aktiviert die Chargenreservierung im Verkaufsangebot | 
Verkaufsauftrag | Aktiviert die Chargenreservierung im Verkaufsauftrag | 
Logistischer Lagerort | Ist diese Option aktiviert, werden in der erw. Matchcodesuche nur Bestände von Lagerorten berücksichtigt, die als logistischer Lagerort gekennzeichnet sind. | 
Komplette Menge zuordnen | Wenn die Erw. Matchcodesuche aktiviert ist, kann mit diesem Feld bestimmt werden, ob die komplette Menge dem Artikel oder der Artikelverfolgung zugeordnet werden soll.
[image] | 
Lagerort in der Wertefactbox berücksichtigen | Definiert, ob in der Infobox Werte der erw. Matchcodesuche die Werte Lagerort übergreifend oder für den Lagerort der ausgewählten Zeile berechnet werden sollen. | 
Artikelsuche | Definiert, ob die „Artikelsuche“ in der erw. Matchcodesuche standardmäßig aktiviert ist. | 
Chargensuche | Definiert, ob die „Chargensuche“ in der erw. Matchcodesuche standardmäßig aktiviert ist. Kann nicht zusammen mit „Alles anzeigen“ genutzt werden. | 
Alles anzeigen | Definiert, ob „Alles anzeigen“ in der erw. Matchcodesuche standardmäßig aktiviert ist. Kann nicht zusammen mit „Chargensuche“ genutzt werden. | 
In Bestellung | Definiert ob „In Bestellung” in der erw. Matchcodesuche standardmäßig aktiviert ist. Kann nur zusammen mit „Chargensuche“ verwendet werden. | 
Verteilungslogik | Gibt an, ob die erw. Matchcodesuche eine automatische Zuordnung des Suchergebnisses vornehmen soll.
Dem Use

aktiviert ist. Kann nur zusammen mit „Chargensuche“ verwendet werden. | 
Verteilungslogik | Gibt an, ob die erw. Matchcodesuche eine automatische Zuordnung des Suchergebnisses vornehmen soll.
Dem User stehen folgende Optionen zur Verfügung:
- Manuell
- FiFo
Durch FiFo werden die Chargen mit dem frühesten Eingangsdatum automatisch zugeordnet, wenn der User eine Erfassungsmenge in einem Artikel einträgt. Bei der Option „Manuell“ muss der User die Chargen manuell zuweisen. | 
Matchcode Materialart | Gibt die Standardmaterialart an, mit der in der erw. Matchcodesuche gesucht werden soll. | 
Standardwerte in erw. Suche ignorieren | Gibt an, ob in der erw. Matchcodesuche die Standardwerte der Sucheigenschaften ignoriert werden sollen. | 
Standard Materialsuche & -bestände Ansichtsart | Beeinflusst, wie die Ergebnisse der Materialsuche dargestellt werden. Die vorhandenen Optionen sind:
- Artikel & Lagerort
- Artikel
- Charge/Seriennummer |

Die „Eigenschaften“ stellen alle zur Verfügung stehenden Eigenschaften dar.

[image]

Eine Eigenschaft wird im Anschluss einer Materialart zugeordnet und kann dann in einem Artikel genutzt und mit Werten gefüllt werden.

[image]

Die Einrichtung einer Eigenschaft kann auf verschiedenen Wegen erfolgen:

Über ein Freitextfeld
Über eine Auswahl von Werten aus der hinterlegten vorgefertigten Tabelle
Durch Hinterlegung von Werten in einer eigenen Tabelle, die dann wiederum zur Einrichtung herangezogen wird

☞ Bitte beachten Sie, dass, sobald die Eigenschaft in Benutzung in einer Materialart und einem Artikel ist, die Eigenschaft nicht mehr geändert werden kann.

Erläuterungen zu den Feldern der Karte „Eigenschaft“:

Feldname | Erläuterung | 
Code | Der Code kann vom User selbst bestimmt werden, muss jedoch eindeutig sein. | 
Name | Name der Eigenschaft | 
Tabellennr. | Es kann eine beliebige Tabelle ausgewählt werden, aus der die User einen Wert auswählen möchten. | 
Feldnr. | Wird automatisch mit dem Primärschlüsselfeld der Tabelle hinterlegt. | 
Datentyp | Vorhandene Optionen:
- Text
- Ganzzahl
- Dezimal
- Datum. Wird automatisch gefüllt, wenn eine Tabelle genutzt wird. | 
Eigenschaftswerte verwenden | Aktiviert die Funktion der selbst einrichtbaren Eigenschaftswerte | 
Kategoriencode | Möglichkeit der Gruppierung von Eigenschaften außerhalb der Materialarten |

Aktionen innerhalb der Eigenschaftskarte

Erläuterungen zu den Aktionen der Karte „Eigenschaften“:

Feldname | Erläuterung | 
Eigenschaftswerte | Öffnet die hinterlegten Eigenschaftswerte zu der geöffneten Eigenschaftskarte. Kann nur genutzt werden, wenn Eigenschaftswerte verwenden auf True steht | 
Übersetzungen | Öffnet die Übersetzungen für den Eigenschaftsnamen. Hier können für verschiedene Sprachcodes verschiedene Namen hinterlegt werden. |

Eigenschaftswerte

Erläuterungen zu den Feldern der „Eigenschaftswerte“:

Feldname | Erläuterung | 
Wert | Eindeutiger Wert für die Eigenschaft | 
Name | Beschreibungstext für den Wert | 
Gruppencode | Möglichkeit der Gruppierung von Eigenschaftswerten |

[image]

In dem obigen Beispiel werden Eigenschaftswerte für die Eigenschaft

igenschaft | 
Name | Beschreibungstext für den Wert | 
Gruppencode | Möglichkeit der Gruppierung von Eigenschaftswerten |

[image]

In dem obigen Beispiel werden Eigenschaftswerte für die Eigenschaft „Typ“ angezeigt. Die Eigenschaft „Typ“ kann nun mit den gezeigten Werten näher definiert werden. Die Tabelle ist nachträglich erweiterbar.

Aktionen innerhalb der Eigenschaftswerte

Erläuterungen zu den Aktionen innerhalb der Eigenschaftswerte:

Feldname | Erläuterung | 
Neu | Legt einen neuen Eigenschaftswert an | 
Liste bearbeiten | Ändert den Modus zwischen Ansicht und Bearbeiten | 
Löschen | Löscht den oder die ausgewählten Eigenschaftswerte | 
Übersetzungen | Pro Eigenschaftswert kann für jeden Sprachcode eine Übersetzung eingerichtet werden |

Die „Materialarten“ stellen alle zur Verfügung stehenden Materialarten dar.

[image]

In der Übersicht der Materialarten steht den Usern die Möglichkeit zur Verfügung, alle Materialarten einzusehen. Sie können darüber hinaus die Anzahl der Artikel sehen, in denen diese Materialart genutzt wird. Über das Flowfield öffnet sich eine gefilterte Artikelliste zu dieser Materialart.

[image]

[image]

Erläuterungen zu den Feldern der Karte „Materialartenkarte“:

Feldname | Erläuterung | 
Code | Der Code kann von Usern selbst bestimmt werden, muss jedoch eindeutig sein. | 
Beschreibung | Name der Materialart | 
Duplikatsprüfung aktivieren | Aktiviert eine Prüfung, ob bereits Artikel mit denselben Materialeigenschaftswerten vorhanden ist und verhindert ggf. die Entsperrung des Artikels | 
Anzahl Artikel | Zeigt die Anzahl der Artikel an, die diese Materialart nutzen. | 
Formel für Artikelmatchcode | Anzeige der Formel für die Generierung des Artikelmatchcodes |

Materialarten Eigenschaftszuordnung

In der Materialarten Eigenschaftszuordnung können die User nun die vorher eingerichteten Eigenschaften einer Materialart zuordnen und ggfs. weitere Definitionen bestimmen.

[image]

Erläuterungen zu den Feldern der „Eigenschaftszuordnung“:

Feldname | Erläuterung | 
Code | Der Code der gewählten Eigenschaft | 
Eigenschaftsname | Name der Eigenschaft | 
Standardwert | Vorgabewert für Artikel dieser Materialart | 
Fix | In Kombination mit der Einstellung „Fixe Werte nur an Basisartikel editierbar“ verhindert diese Einstellung, dass ein Wert an Variantenartikeln bearbeitet werden kann. | 
Einkaufseigenschaft | Erlaubt das Editieren von Werten dieser Eigenschaft in Einkaufsdokumenten | 
Verkaufseigenschaft | Erlaubt das Editieren von Werten dieser Eigenschaft in Verkaufsdokumenten | 
Chargeneigenschaft | Erlaubt das Editieren von Werten dieser Eigenschaft pro Charge | 
Erford

nten | 
Verkaufseigenschaft | Erlaubt das Editieren von Werten dieser Eigenschaft in Verkaufsdokumenten | 
Chargeneigenschaft | Erlaubt das Editieren von Werten dieser Eigenschaft pro Charge | 
Erforderlich | Kennzeichnet die Eigenschaft als Pflichteigenschaft | 
Nicht editierbar | Verhindert das manuelle Editieren der Werte dieser Eigenschaft | 
Nicht sichtbar | Zeigt die Eigenschaft bei der Erfassung von Werten nicht an | 
Null ist Wert | Interpretiert eine Eingabe von 0 als Wert und nicht als Leer | 
Verwendung | Optionsfeld für die Nutzung in Verbindungsapps | 
Eigenschaftswertname | Ist ein Standardwert ausgewählt und besitzt dieser einen Eigenschaftswertnamen wird dieser angezeigt | 
Wert zulässig von | Schränkt die Erfassung von Werten dieser Eigenschaft mit einem „Von-Wert“ ein | 
Wert zulässig bis | Schränkt die Erfassung von Werten dieser Eigenschaften mit einem „Bis-Wert“ ein | 
Einheit | Gibt die Einheit der Eigenschaft an | 
Anzeigereihenfolge | Es kann eine numerische Reihenfolge festgelegt werden, in der die Eigenschaften dargestellt werden sollen | 
Kategoriencode | Eigenschaften in einer Materialart können Kategorien zugeordnet werden. | 
Kategorienbeschreibung | Zeigt die Beschreibung der zugeordneten Kategorie an | 
Wertfilter | Filter für Eigenschaftswerte bei der Editierung der Werte | 
Wertgruppenfilter | Filter für Eigenschaftswertgruppen bei der Editierung der Werte |

Aktionen in der Materialart

Erläuterungen zu den Aktionen der Karte „Materialart“:

der Editierung der Werte | 
Wertgruppenfilter | Filter für Eigenschaftswertgruppen bei der Editierung der Werte |

Aktionen in der Materialart

Erläuterungen zu den Aktionen der Karte „Materialart“:

Aktionsname | Erläuterung | 
Artikelmatchcodevorlage | Öffnet einen Dialog zur Erstellung einer Artikelmatchcodevorlage | 
Chargen/Serien Matchcode Vorlage | Öffnet einen Dialog zur Erstellung einer Chargen/Serien Matchcode Formel | 
Artikelmatchcodes aktualisieren | Aktualisiert alle Artikelmatchcodes der Artikel, die der Materialart zugeordnet sind, gemäß der Artikelmatchcodevorlage | 
Chargen/Serien Matchcodes aktualisieren | Aktualisiert alle Chargen/Serien Matchcodes der Artikel, die der Materialart zugeordnet sind, gemäß der Chargen/Serien Matchcodevorlage | 
Vorlage für Basisartikelkopie | Öffnet die Kopiervorlage für Basisartikel | 
Vorlage für Variantenartikel | Öffnet die Vorlage für Variantenartikel | 
Artikelbeschreibungsvorlage | Öffnet die Artikelbeschreibungsvorlagen | 
Chargen-/Seriennummernbeschreibungsvorlage | Öffnet die Chargen-/Seriennummernbeschreibungsvorlagen | 
Artikelbeschreibungen aktualisieren | Aktualisiert alle Artikelbeschreibungen der Artikel, die der Materialart zugeordnet sind, gemäß der Artikelbeschreibungsvorlage | 
Chargen-/Seriennummernbeschreibungen aktualisieren | Aktualisiert alle Chargen-/Seriennummernbeschreibungen der Artikel, die der Materialart zugeordnet sind, gemäß der Chargen-/Seriennummernbeschreibungsvorlage |

Artikelmatchcodev

ungen aktualisieren | Aktualisiert alle Chargen-/Seriennummernbeschreibungen der Artikel, die der Materialart zugeordnet sind, gemäß der Chargen-/Seriennummernbeschreibungsvorlage |

Artikelmatchcodevorlage

In der Artikelmatchcodevorlage können die User eine Vorlage für den im Artikel zu generierenden Matchcode erstellen. Dieser basiert auf Grundlage der in der Eigenschaftszuordnung ausgewählten Eigenschaften.

[image]

Erläuterung zu den Feldern in der Artikelmatchcodevorlage:

Feldname | Erläuterung | 
Eigenschaftscode | Auswahl einer Eigenschaft, die für die Aktionen der Artikelmatchcodevorlage genutzt werden soll. | 
Textwert | Freitextfeld, das für die Aktionen der Artikelmatchcodevorlage genutzt werden soll. | 
Formel für Artikelmatchcode | Formelausdruck für die Generierung des Artikelmatchcodes. | 
Artikelnr. Zum Testen auswählen | Auswahl einer Artikelnummer derselben Materialart zum Test der Formel für Artikelmatchcode | 
Testergebnis | Gibt den Matchcode an, der bei Nutzung der Formel als Artikelmatchcode generiert würde. |

Erläuterung der Aktionen in der Artikelmatchcodevorlage:

[image]

Aktionsname | Erläuterung | 
Ansicht/Bearbeiten | Stellt die Page in den Ansichtsmodus. | 
Eigenschaftswert einfügen | Fügt den Eigenschaftswert der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Artikelmatchcode ein.
Hierfür wird folgender Ausdruck genutzt:
VALUEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftsnamen einfügen | Fügt den Namen der Eigenschaf

chaftscode in die Formel für Artikelmatchcode ein.
Hierfür wird folgender Ausdruck genutzt:
VALUEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftsnamen einfügen | Fügt den Namen der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Artikelmatchcode ein.
Hierfür wird folgender Ausdruck genutzt:
NAMEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftswertnamen einfügen | Fügt den Namen des Eigenschaftswertes der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Artikelmatchcode ein. Zu beachten ist hierbei, dass Eigenschaftswerte für die Eigenschaft genutzt werden müssen, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
VALUENAMEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftseinheit einfügen | Fügt die Einheit der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Artikelmatchcode ein. Zu beachten ist hierbei, dass es sich um eine nummerische Eigenschaft inkl. gefülltem Eigenschaftscode handeln muss, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
UNITFROM (Wert aus dem Feld Eigenschaftscode) | 
Text einfügen | Fügt den Freitext aus dem Feld Textwert in die Formel für Artikelmatchcode ein.
Hierfür wird folgender Ausdruck genutzt:
TEXT (Wert aus dem Feld Textwert) | 
Rückgängig | Macht den letzten eingefügten Ausdruck rückgängig. |

Chargen/Serien Matchcode Vorlage

Mit der „Chargen/Serien Matchcode Vorlage“ können Sie für Chargen- und Seriennummern eigene Matchcode

ckgängig | Macht den letzten eingefügten Ausdruck rückgängig. |

Chargen/Serien Matchcode Vorlage

Mit der „Chargen/Serien Matchcode Vorlage“ können Sie für Chargen- und Seriennummern eigene Matchcode Vorlagen hinterlegen.

[image]

Erläuterung zu den Feldern in der Chargen/Serien Matchcode Vorlage:

Feldname | Erläuterung | 
Eigenschaftscode | Auswahl einer Eigenschaft, die für die Aktionen der Chargen/Serien Matchcode-Vorlage genutzt werden soll | 
Textwert | Freitextfeld, das für die Aktionen der Chargen/Serien Matchcode-Vorlage genutzt werden soll | 
Chargen/Serien Matchcode Formel | Formelausdruck für die Generierung des Chargen/Serien Matchcodes. | 
Artikelnr. zum Testen auswählen | Auswahl einer Artikelnr. derselben Materialart zum Test der Formel für den Chargen/Serien Matchcodes | 
Variante zum Testen auswählen | Auswahl einer Artikelvariante des Artikels aus dem Feld „Artikelnr. zum Testen auswählen“ zum Test der Formel für den Chargen/Serien Matchcode | 
Test Chargennr. Auswählen | Auswahl einer Chargennr. der Artikel Varianten Kombination aus den Feldern „Artikelnr. zum Testen auswählen“ und „Variante zum Testen auswählen“, zum Test der Formel für den Chargen/Serien Matchcode | 
Seriennr. Zum Testen auswählen | Auswahl einer Seriennr. der Artikel Varianten Kombination aus den Feldern „Artikelnr. zum Testen auswählen“ und „Variante zum Testen auswählen“, zum Test der Formel für den Chargen/Serien Matchcode | 
Chargen/Serien Matchcode-Ergebnis testen | Gibt den Matc

aus den Feldern „Artikelnr. zum Testen auswählen“ und „Variante zum Testen auswählen“, zum Test der Formel für den Chargen/Serien Matchcode | 
Chargen/Serien Matchcode-Ergebnis testen | Gibt den Matchcode an, der bei Nutzung der Formel für den Chargen/Serien Matchcode generiert werden würde. |

[image]

Erläuterung zu den Aktionen in der Chargen-/Serien Matchcodevorlage:

Aktionsname | Erläuterung | 
Ansicht/Bearbeiten | Stellt die Page in den Ansichtsmodus. | 
Eigenschaftswert einfügen | Fügt den Eigenschaftswert der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für den Chargen/Serien Matchcode ein.
Hierfür wird folgender Ausdruck genutzt:
VALUEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftsnamen einfügen | Fügt den Namen der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Chargen/Serien Matchcode ein.
Hierfür wird folgender Ausdruck genutzt:
NAMEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftswertnamen einfügen | Fügt den Namen des Eigenschaftswertes der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Chargen/Serien Matchcode ein. Zu beachten ist hierbei, dass Eigenschaftswerte für die Eigenschaft genutzt werden müssen, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
VALUENAMEFROM (Wert aus dem Feld Eigenschaftscode) | 
Eigenschaftseinheit einfügen | Fügt die Einheit der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Chargen/Serien Matchcode ein. Zu beachten ist hierbei, dass

m Feld Eigenschaftscode) | 
Eigenschaftseinheit einfügen | Fügt die Einheit der Eigenschaft aus dem Feld Eigenschaftscode in die Formel für Chargen/Serien Matchcode ein. Zu beachten ist hierbei, dass es sich um eine numerische Eigenschaft inkl. gefülltem Eigenschaftscode handeln muss, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
UNITFROM (Wert aus dem Feld Eigenschaftscode) | 
Text einfügen | Fügt den Freitext aus dem Feld Textwert in die Formel für Chargen/Serien Matchcode ein.
Hierfür wird folgender Ausdruck genutzt:
TEXT (Wert aus dem Feld Textwert) | 
Rückgängig | Macht den letzten eingefügten Ausdruck rückgängig. |

Vorlage für Basisartikelkopie

In der Vorlage für Basisartikelkopie können die User einstellen, welche Daten bei der Ausführung der „Aktion Basisartikel kopieren“ kopiert werden sollen.

[image]

[image]

Erläuterung zu den einzelnen Einstellungen in der Vorlage für Basisartikelkopie:

Feldname | Erläuterung | 
Allgemeine Artikelinformationen | Übernimmt Daten aus der Artikelkarte | 
Bild | Übernimmt das Artikelbild | 
Maßeinheiten | Übernimmt die Daten aus der Tabelle Artikeleinheiten | 
Bemerkungen | Übernimmt die Artikelbemerkungen aus der Tabelle Bemerkungen | 
Dimensionen | Übernimmt die Dimensionen aus der Tabelle Dimensionswerte | 
Verkaufspreise | Übernimmt die Verkaufspreise aus der Tabelle der Verkaufspreise | 
Verkaufszeilenrabatte | Übernimmt die Verkaufszeilenrabatte aus der Tabelle Verkaufszeilenrabatte | 
Eink

nswerte | 
Verkaufspreise | Übernimmt die Verkaufspreise aus der Tabelle der Verkaufspreise | 
Verkaufszeilenrabatte | Übernimmt die Verkaufszeilenrabatte aus der Tabelle Verkaufszeilenrabatte | 
Einkaufspreise | Übernimmt die Einkaufspreise aus der Tabelle der Einkaufspreise | 
Einkaufszeilenrabatte | Übernimmt die Einkaufszeilenrabatte aus der Tabelle der Einkaufszeilenrabatte | 
Problembehandlung | Übernimmt die Problembehandlungscodes aus der Tabelle der Problembehandlungen | 
Ressourcenqualifikationen | Übernimmt die Ressourcenqualifikationen aus der Tabelle der Ressourcenqualifikationen | 
Artikelvarianten | Übernimmt die Artikelvarianten aus der Tabelle der Artikelvarianten | 
Artikellieferanten | Übernimmt die Artikel Lieferanten Beziehungen aus der Artikel Lieferanten Tabelle | 
Übersetzungen | Übernimmt die Übersetzungen der Artikelbeschreibungen | 
Attribute | Übernimmt die Attribute des Artikels | 
Textbausteine | Übernimmt die Textbausteine des Artikels | 
Artikelreferenzen | Übernimmt die Artikelreferenzen des Artikels | 
Stücklistenkomponenten | Legt eine neue Fertigungsstückliste an und übernimmt die Stücklistenkomponenten des Artikels | 
Variantenartikel kopieren | Kopiert zusätzlich zum Basisartikel auch alle Variantenartikel des Artikels | 
Neuen Artikel entsperren | Entsperrt den neu erstellten Artikel automatisch |

Vorlage für Variantenartikel

In der Vorlage für Variantenartikel können die User einstellen, welche Daten bei der Ausführung der Aktion „Var

rren | Entsperrt den neu erstellten Artikel automatisch |

Vorlage für Variantenartikel

In der Vorlage für Variantenartikel können die User einstellen, welche Daten bei der Ausführung der Aktion „Variantenartikel erstellen“ vom Basisartikel kopiert werden sollen.

[image]

[image]

Erläuterung zu den einzelnen Einstellungen in der Vorlage für Variantenartikel:

Feldname | Erläuterung | 
Allgemeine Artikelinformationen | Übernimmt Daten aus der Artikelkarte | 
Bild | Übernimmt das Artikelbild | 
Maßeinheiten | Übernimmt die Daten aus der Tabelle Artikeleinheiten | 
Bemerkungen | Übernimmt die Artikelbemerkungen aus der Tabelle Bemerkungen | 
Dimensionen | Übernimmt die Dimensionen aus der Tabelle Dimensionswerte | 
Verkaufspreise | Übernimmt die Verkaufspreise aus der Tabelle der Verkaufspreise | 
Verkaufszeilenrabatte | Übernimmt die Verkaufszeilenrabatte aus der Tabelle Verkaufszeilenrabatte | 
Einkaufspreise | Übernimmt die Einkaufspreise aus der Tabelle der Einkaufspreise | 
Einkaufszeilenrabatte | Übernimmt die Einkaufszeilenrabatte aus der Tabelle der Einkaufszeilenrabatte | 
Problembehandlung | Übernimmt die Problembehandlungscodes aus der Tabelle der Problembehandlungen | 
Ressourcenqualifikationen | Übernimmt die Ressourcenqualifikationen aus der Tabelle der Ressourcenqualifikationen | 
Artikelvarianten | Übernimmt die Artikelvarianten aus der Tabelle der Artikelvarianten | 
Artikellieferanten | Übernimmt die Artikel Lieferanten Beziehungen aus der Artikel Lieferante

alifikationen | 
Artikelvarianten | Übernimmt die Artikelvarianten aus der Tabelle der Artikelvarianten | 
Artikellieferanten | Übernimmt die Artikel Lieferanten Beziehungen aus der Artikel Lieferanten Tabelle | 
Übersetzungen | Übernimmt die Übersetzungen der Artikelbeschreibungen | 
Attribute | Übernimmt die Attribute des Artikels | 
Textbausteine | Übernimmt die Textbausteine des Artikels | 
Artikelreferenzen | Übernimmt die Artikelreferenzen des Artikels | 
Stücklistenkomponenten | Legt eine neue Fertigungsstückliste an und übernimmt die Stücklistenkomponenten des Artikels | 
Neuen Artikel entsperren | Entsperrt den neu erstellten Artikel automatisch |

Artikelbeschreibungsvorlage

In der Artikelbeschreibungsvorlage können die User Eigenschaften mit Freitext kombinieren, um daraus für unterschiedliche Sprachcodes die Artikelbeschreibung 1 und 2 generieren zu lassen.

[image]

Erläuterung für die Felder in der Artikelbeschreibungsvorlage:

Feldname | Erläuterung | 
Sprachcode | Über unterschiedliche Sprachcodes können die User steuern, wie die Artikelbeschreibung für die unterschiedlichen Sprachen definiert wird. Diese werden dann z.B. beim Eintragen in eine Verkaufszeile generiert. | 
Artikelbeschreibungsformel | Gibt den Formelausdruck für die Beschreibung 1 des Artikels an. Über den Assis Edit Button gelangen die User in den Dialog zur Erfassung der Artikelbeschreibungsformel. | 
Formel für Artikelbeschreibung 2 | Gibt den Formelausdruck für die Beschreibung 2 des Artik

Über den Assis Edit Button gelangen die User in den Dialog zur Erfassung der Artikelbeschreibungsformel. | 
Formel für Artikelbeschreibung 2 | Gibt den Formelausdruck für die Beschreibung 2 des Artikels an. Über den Assis Edit Button gelangt der User in den Dialog zur Erfassung der Formel für Artikelbeschreibung 2. |

Dialog Artikelbeschreibungsformel & Formel Artikelbeschreibung 2

Der Dialog „Artikelbeschreibungsformel für die Artikelbeschreibung 2“ unterstützt Sie bei der Erstellung der Formel.

[image]

Erläuterung für die Felder im Dialog „Artikelbeschreibungsformel erstellen“:

Feldname | Erläuterung | 
Eigenschaftscode | Auswahl einer Eigenschaft, die für die Aktionen der Artikelbeschreibungsformel genutzt werden soll. | 
Textwert | Freitextfeld, das für die Aktionen der Artikelbeschreibungsformel genutzt werden soll. | 
Artikelbeschreibungsformel | Formelausdruck für die Generierung der Artikelbeschreibung. | 
Artikelnr. Zum Testen auswählen | Auswahl einer Artikelnr. derselben Materialart zum Testen der Artikelbeschreibungsformel. | 
Testergebnis | Gibt die Artikelbeschreibung an, die bei Nutzung der Artikelbeschreibungsformel generiert werden würde. |

[image]

Erläuterung für die Aktionen im Dialog „Artikelbeschreibungsformel erstellen“:

Aktionsname | Erläuterung | 
Ansicht/Bearbeiten | Stellt die Page in den Ansichtsmodus. | 
Eigenschaftswert einfügen | Fügt den Eigenschaftswert der Eigenschaft aus dem Feld Eigenschaftscode in die Artikelbeschreibungsformel ein.

Ansicht/Bearbeiten | Stellt die Page in den Ansichtsmodus. | 
Eigenschaftswert einfügen | Fügt den Eigenschaftswert der Eigenschaft aus dem Feld Eigenschaftscode in die Artikelbeschreibungsformel ein. Hierfür wird folgender Ausdruck genutzt: VALUEFROM (Wert aus dem Feld Eigenschaftscode). | 
Eigenschaftsnamen einfügen | Fügt den Namen der Eigenschaft aus dem Feld Eigenschaftscode in die Artikelbeschreibungsformel ein. Hierfür wird folgender Ausdruck genutzt: NAMEFROM (Wert aus dem Feld Eigenschaftscode). | 
Eigenschaftswertnamen einfügen | Fügt den Namen des Eigenschaftswertes der Eigenschaft aus dem Feld Eigenschaftscode in die Artikelbeschreibungsformel ein. Zu beachten ist hierbei, dass Eigenschaftswerte für die Eigenschaft genutzt werden müssen, um diese Aktion erfolgreich zu nutzen. Hierfür wird folgender Ausdruck genutzt: VALUENAMEFROM (Wert aus dem Feld Eigenschaftscode). | 
Eigenschaftseinheit einfügen | Fügt die Einheit der Eigenschaft aus dem Feld Eigenschaftscode in die Artikelbeschreibungsformel ein. Zu beachten ist hierbei, dass es sich um eine numerische Eigenschaft inkl. gefülltem Eigenschaftscode handeln muss, um diese Aktion erfolgreich zu nutzen. Hierfür wird folgender Ausdruck genutzt: UNITFROM (Wert aus dem Feld Eigenschaftscode). | 
Text einfügen | Fügt den Freitext aus dem Feld „Textwert“ in die Artikelbeschreibungsformel ein. Hierfür wird folgender Ausdruck genutzt: TEXT (Wert aus dem Feld Textwert). | 
Rückgängig | Macht den letzten eingefügten Ausdruc

reitext aus dem Feld „Textwert“ in die Artikelbeschreibungsformel ein. Hierfür wird folgender Ausdruck genutzt: TEXT (Wert aus dem Feld Textwert). | 
Rückgängig | Macht den letzten eingefügten Ausdruck rückgängig. |

Chargen-/Seriennummernbeschreibungsvorlagen

In der Chargen-/Seriennummernbeschreibungsvorlagen können die User Eigenschaften mit Freitext kombinieren. So hinterlegen sie einzigartige Beschreibungsvorlagen für Chargen- oder Seriennummern.

[image]

Erläuterung für die Felder in der Artikelbeschreibungsvorlage:

Feldname | Erläuterung | 
Art | Die User können über ein Optionswert entscheiden, ob die Beschreibungsvorlagen für Chargen- oder Seriennummern gelten sollen. | 
Beschreibungsformel | Gibt den Formelausdruck für die Beschreibung 1 der Chargen-/Seriennummer an. Über den Assis Edit Button gelangen die User in den Dialog zur Erfassung der Chargen-/Seriennummernbeschreibungsformeln. | 
Beschreibungsformel 2 | Gibt den Formelausdruck für die Beschreibung 2 der Chargen-/Seriennummer an. Über den Assis Edit Button gelangen die User in den Dialog zur Erfassung der Chargen-/Seriennummernbeschreibungsformeln. |

Dialog zur Erfassung der Chargen-/Seriennummernbeschreibungsformeln

Im Dialog „Chargen-/Seriennummernbeschreibungsformel erstellen“ können die User unterstützt die Formel für die Chargen-/Seriennummernbeschreibungen erstellen.

[image]

Erläuterung für die Felder im Dialog „Chargen-/Seriennummernbeschreibungsformel erstellen“:

Feldname | Erläuterung | 
Eige

die Formel für die Chargen-/Seriennummernbeschreibungen erstellen.

[image]

Erläuterung für die Felder im Dialog „Chargen-/Seriennummernbeschreibungsformel erstellen“:

Feldname | Erläuterung | 
Eigenschaftscode | Auswahl einer Eigenschaft, die für die Aktionen der Beschreibungsformel genutzt werden soll. | 
Textwert | Freitextfeld, das für die Aktionen der Beschreibungsformel genutzt werden soll. | 
Beschreibungsformel | Formelausdruck für die Generierung der Chargen-/Seriennummernbeschreibung. |

[image]

Erläuterung für die Aktionen im Dialog „Chargen-/Seriennummernbeschreibungsformel erstellen“:

Aktionsname | Erläuterung | 
Ansicht/Bearbeiten | Stellt die Page in den Ansichtsmodus. | 
Eigenschaftswert einfügen | Fügt den Eigenschaftswert der Eigenschaft aus dem Feld Eigenschaftscode in die Beschreibungsformel ein.
Hierfür wird folgender Ausdruck genutzt:
VALUEFROM (Wert aus dem Feld Eigenschaftscode). | 
Eigenschaftsnamen einfügen | Fügt den Namen der Eigenschaft aus dem Feld Eigenschaftscode in die Beschreibungsformel ein.
Hierfür wird folgender Ausdruck genutzt:
NAMEFROM (Wert aus dem Feld Eigenschaftscode). | 
Eigenschaftswertnamen einfügen | Fügt den Namen des Eigenschaftswertes der Eigenschaft aus dem Feld Eigenschaftscode in die Beschreibungsformel ein. Zu beachten ist hierbei, dass Eigenschaftswerte für die Eigenschaft genutzt werden müssen, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
VALUENAMEFROM (Wert aus dem Feld Eigenschaf

t hierbei, dass Eigenschaftswerte für die Eigenschaft genutzt werden müssen, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
VALUENAMEFROM (Wert aus dem Feld Eigenschaftscode). | 
Eigenschaftseinheit einfügen | Fügt die Einheit der Eigenschaft aus dem Feld Eigenschaftscode in die Beschreibungsformel ein. Zu beachten ist hierbei, dass es sich um eine numerische Eigenschaft inkl. gefülltem Eigenschaftscode handeln muss, um diese Aktion erfolgreich zu nutzen.
Hierfür wird folgender Ausdruck genutzt:
UNITFROM (Wert aus dem Feld Eigenschaftscode). | 
Text einfügen | Fügt den Freitext aus dem Feld Textwert in die Beschreibungsformel ein.
Hierfür wird folgender Ausdruck genutzt:
TEXT (Wert aus dem Feld Textwert). | 
Rückgängig | Macht den letzten eingefügten Ausdruck rückgängig. |

Den Usern steht an unterschiedlichen Stellen eine konfigurierbare Infobox für die Berechnung der Artikelverfügbarkeit zur Verfügung.

Die Einrichtung dieser Infobox erfolgt über die Werteeinrichtung.

[image]

Erläuterung zu den Feldern der Werteeinrichtung:

Feldname | Erläuterung | 
Lagerbestand berücksichtigen | Gibt an, ob der aktuelle Lagerbestand in der Verfügbarkeit berücksichtigt werden soll. Erhöht die Verfügbarkeit. | 
Verkaufsangebote einschließen | Gibt an, ob Verkaufsangebote in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Verkaufsaufträge einschließen | Gibt an, ob Verkaufsaufträge in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Verkaufsrahmenaufträge einschließen | Gibt an, ob Verkaufsaufträge in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Verkaufsreklamationen einschließen | Gibt an, ob Verkaufsreklamationen in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Einkaufsanfragen einschließen | Gibt an, ob Einkaufsanfragen in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Einkaufsbestellungen einschließen | Gibt an, ob Einkaufsbestellungen in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Einkaufsrahmenbestellungen einschließen | Gibt an, ob Einkaufsrahmenbestellungen in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Einkaufsreklamatione

Verfügbarkeit. | 
Einkaufsrahmenbestellungen einschließen | Gibt an, ob Einkaufsrahmenbestellungen in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Einkaufsreklamationen einschließen | Gibt an, ob Einkaufsreklamationen in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Fertigungsaufträge berücksichtigen | Gibt an, ob Fertigungsaufträge in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Fertigungskomponenten einschließen | Gibt an, ob Fertigungskomponenten in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Montageaufträge einschließen | Gibt an, ob Montageaufträge in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Montagekomponenten einschließen | Gibt an, ob Montagekomponenten in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Ausgeh. Umlagerungsaufträge einschließen | Gibt an, ob ausgehende Umlagerungsaufträge in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. | 
Eingeh. Umlagerungsaufträge einschließen | Gibt an, ob eingehende Umlagerungsaufträge in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
In-Transit einschließen | Gibt an, ob Bestände, die sich in einem In-Transit Lagerort befinden, in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Materialverfolgungsposten berücksichtigen | Gibt an, ob Einträ

Bestände, die sich in einem In-Transit Lagerort befinden, in der Verfügbarkeit berücksichtigt werden sollen. Erhöht die Verfügbarkeit. | 
Materialverfolgungsposten berücksichtigen | Gibt an, ob Einträge in den Materialverfolgungsposten in der Verfügbarkeit berücksichtigt werden sollen. Verringert die Verfügbarkeit. |

Auf der Artikelkarte stehen den Usern neue Felder und neue Aktionen zur Verfügung.

[image]

Erläuterung der Felder auf der Artikelkarte:

Feldname | Erläuterung | 
Materialartencode | Dient zur Bestimmung der Materialart des Artikels. Enthält einen LookUp auf die Materialartentabelle. Bei Auswahl der Materialart werden die Beschreibung und der Matchcode anhand deren Vorlagen erstellt. Außerdem wird der Artikel gesperrt. | 
Benutzerdefinierter Matchcode | Erlaubt die Erfassung eines Matchcode abweichend von der Matchcodevorlage der Materialart. | 
Matchcode | Gibt den Matchcode an. Das Feld kann nur manuell überschrieben werden, wenn Benutzerdefinierter Matchcode auf True eingestellt ist. | 
Basisartikel | Gibt an, ob es sich bei dem Artikel um einen Basisartikel handelt. | 
Basisartikelnr. | Gibt bei einem Variantenartikel die Nummer des Basisartikels an, aus dem der Variantenartikel erstellt wurde. | 
Kopiert von Artikelnr. | Gibt die Artikelnummer an, aus denen die Funktionen Basisartikel kopieren oder Variantenartikel erstellen, ausgeführt wurden. |

Erläuterung zu den Aktionen auf der Artikelkarte:

Aktionsname | Erläuterung | 
Materialliste | Öffnet die Materialliste gefiltert auf die Artikelnummer, aus der die Materialliste aufgerufen wurde. | 
Basisartikel kopieren | Ruft die an der Materialart hinterlegte Vorlage für Basisartikelkopie auf und kopiert anschließen den Artikel. Nur möglich, wenn es sich bei dem Artikel um einen Basisartikel handelt. | 
Variantenartikel

die an der Materialart hinterlegte Vorlage für Basisartikelkopie auf und kopiert anschließen den Artikel. Nur möglich, wenn es sich bei dem Artikel um einen Basisartikel handelt. | 
Variantenartikel erstellen | Öffnet die Page „Eigenschaften editieren“, in der die User die abweichenden Werte für den Variantenartikel hinterlegen können. | 
Materialfilter | Öffnet die Page „Artikel Materialfilter“, in der die User einen Filter für die Materialbestandssuche in den FA-Komponenten vordefinieren können. |

Hinterlegung der Eigenschaften am Artikel

Haben die User eine Materialart im Artikel ausgewählt, können sie über die Infobox „Eigenschaften“ im Artikel in die Erfassung der Eigenschaften springen.

[image]

Über „Bearbeiten“ erreichen die User die Page „Eigenschaften editieren“. Sie können nun die Werte der einzelnen Eigenschaften für den Artikel hinterlegen.

[image]

☞ Sind Werte von Eigenschaften als Fix gekennzeichnet, kann die Einrichtung nur am Basisartikel konfiguriert werden. Außerdem ist eine Anpassung der Werte nur möglich, wenn der Artikel gesperrt ist.

Die User können zusätzlich die Booleanfelder individuell für den Artikel einrichten.
Zu diesen Feldern zählen:

Fix
Einkaufseigenschaft
Verkaufseigenschaft
Chargeneigenschaft
Erforderlich
Nicht editierbar
Nicht sichtbar
Null ist Wert

[image]

☞ Bitte beachten Sie, dass die User keine Zeilen löschen oder hinzufügen können.

Verlassen die User die Page mit „Ok“, werden die Beschreibungen und der Matchcode anhand der V

Null ist Wert

[image]

☞ Bitte beachten Sie, dass die User keine Zeilen löschen oder hinzufügen können.

Verlassen die User die Page mit „Ok“, werden die Beschreibungen und der Matchcode anhand der Vorlagen neu generiert.

[image]

Bei der Entsperrung des Artikels wird abschließend die Duplikatsprüfung durchgeführt, solange diese an der Materialart aktiviert ist. Sollten diese bestimmten Eigenschaftswerte bereits bei einem anderen Artikel genutzt werden, erscheint eine Fehlermeldung.

[image]

Basisartikel kopieren

Führen die User die Aktion „Basisartikel kopieren“ aus, gelangen sie in die Page „Eigenschaften editieren“.

Hier können sie abweichende Werte für den neuen Basisartikel anlegen.

[image]

Verlassen sie die Page mit „Abbrechen“, wird die Kopie des Artikels abgebrochen.

Wird die Page mit „Ok“ verlassen, wird der neue Basisartikel angelegt.

Variantenartikel erstellen

Führen die User die Aktion „Variantenartikel erstellen“ aus, gelangen sie in die Page „Eigenschaften editieren“. Hier können sie abweichende Werte für den neuen Variantenartikel anlegen.

[image]

Verlassen die User die Page mit „Abbrechen“, wird die Anlage des neuen Variantenartikels abgebrochen.

Wird die Page mit „Ok“ verlassen, wird der neue Variantenartikel angelegt. Das Feld „Basisartikelnummer“ wird nun automatisch nach folgender Logik gefüllt:

Wurde der Variantenartikel aus einem Basisartikel erstellt, wird das Feld mit der Nummer des Basisartikels gefüllt.
Wurde der Variantenartikel aus ei

ird nun automatisch nach folgender Logik gefüllt:

Wurde der Variantenartikel aus einem Basisartikel erstellt, wird das Feld mit der Nummer des Basisartikels gefüllt.
Wurde der Variantenartikel aus einem anderen Variantenartikel erstellt, wird das Feld mit dem Wert des Feldes Basisartikel aus dem Artikel genommen, der als Kopiervorlage diente.

Die Aktion Materialfilter kann in der Artikelkarte unter folgendem Pfad im Menüband der Artikelkarte aufgerufen werden:

Zugehörig 🡪 Artikel 🡪 Materialfilter

[image]

[image]

Erläuterung der Felder des Materialfilters:

Feldname | Erläuterung | 
Art | Optionswertfeld in denen die User zwischen folgenden Werten wählen können:
- Materialart
- Eigenschaftsfilter
Je nach Auswahl stehen ihnen unterschiedliche Optionen im Feld „Code“ zur Verfügung. | 
Code | Je nach Auswahl im Feld „Art“ stehen den Usern im Feld „Code“ Lookups auf die Tabellen Materialart und Eigenschaften zur Verfügung.
Wählen sie eine Materialart aus, wird diese als Filterkriterium in der späteren Materialbestandssuche genutzt. Die Nutzung des Feldes Filterwert ist bei einer Zeile mit einer Materialart ausgeschlossen.
Bei einer Auswahl eines Eigenschaftscodes müssen die User den Filter für die Materialbestandssuche im Feld Filterwert definieren. | 
Filterwert | Haben die User eine Eigenschaft im Feld „Code“ gewählt, können sie in diesem Feld einen Filterwert für die Materialbestandssuche definieren.
Hierfür stehen ihnen die im nächsten Kapitel definierten Kriterien zur Verfügung. |

Filterwert definieren

Haben die User eine Eigenschaft mit Eigenschaftswert ausgewählt, öffnen sich die Eigenschaftswerte über den „Assist Edit“-Button. Hat die Eigenschaft keine Eigenschaftswerte, so öffnet sich eine Eingabehilfe für den Filterwert.

[image]

Durch Verlassen der Eingabehilfe mit „Ok“ füllt sich der Filterwert im Ma

sist Edit“-Button. Hat die Eigenschaft keine Eigenschaftswerte, so öffnet sich eine Eingabehilfe für den Filterwert.

[image]

Durch Verlassen der Eingabehilfe mit „Ok“ füllt sich der Filterwert im Materialfilter automatisch.

[image]

Materialbestandssuche in FA-Komponenten

In den FA-Komponenten von simulierten, geplanten, fest geplanten und freigegeben Fertigungsaufträgen steht den Usern die neue Aktion „Materialbestandssuche starten“ zur Verfügung.

[image]

Die Materialbestandssuche filtert die Bestände aller Artikel über einen Eigenschaftsfilter.

Wird die Materialbestandssuche gestartet, öffnet sich für die User ein Vorlauffilter. Hier können die User selbstständig einen Eigenschaftsfilter füllen, um die Ergebnisse der Materialbestandssuche einzugrenzen.

Ist der Materialfilter am Artikel der zugehörigen FA-Zeile gefüllt, wird die Materialbestandssuche bereits gefüllt und kann vom User angepasst werden.

[image]

Durch Verlassen der Page mit „Ok“ öffnet sich die Materialbestandssuche.
Durch Verlassen der Page mit „Abbrechen“ verlässt man die Materialbestandssuche.

Im Anschluss öffnet sich die Page Materialbestände.

[image]

Erläuterung der Felder der Materialbestände:

Feldname | Erläuterung | 
Artikelnr. | Feld zur Filterung einer bestimmten Artikelnr. beinhaltet eine LookUp auf die Artikeltabelle | 
Matchcode | Feld zur Filterung nach einem Matchcode oder einem Teil eines Matchcodes. | 
Chargennr. | Feld zur Filterung einer Chargennummer | 
Ansichtsart | Optionsfel

ookUp auf die Artikeltabelle | 
Matchcode | Feld zur Filterung nach einem Matchcode oder einem Teil eines Matchcodes. | 
Chargennr. | Feld zur Filterung einer Chargennummer | 
Ansichtsart | Optionsfeld zum Umstellen der Ansicht der Baumstruktur in den Zeilen der Materialbestände. Dem User stehen folgende Werte zur Auswahl:
- Artikel & Lagerort
- Artikel
- Charge/Seriennummer.
Je nach Auswahl werden der Baumstruktur Ebenen hinzugefügt oder abgezogen.
Für die weitere Dokumentation wird die Einstellung Artikel & Lagerort verwendet, da diese die komplexeste Baumstruktur darstellt. |

Erläuterung der Felder der Materialbestandszeilen:

Feldname | Erläuterung | 
Beschreibung | Stellt die Baumstruktur dar, die im Feld Ansichtsart ausgewählt wurde.
Die Stufen können in ihrer komplexesten Struktur wie folgt aussehen:
- Artikelnr.- Beschreibung
-> Lagerort - Lagerplätze
--> Lagerplatz
---> Charge – Beschreibung.
Jede Ebene kann auf- und zugeklappt werden. | 
Gesperrt | Zeigt an, ob eine Charge gesperrt ist. Die Information wird aus der Chargeninformationskarte übertragen | 
Erfassungsmenge | Die User können in dieses Feld eintragen, welche Menge der Basiseinheit einer Charge für die spätere Übertragung an die FA-Komponente genutzt werden soll. | 
Lagerbestand | Zeigt den Lagerbestand der Zeile an. Je nach Ebene der Baumstruktur wird der Wert von den unteren Ebenen aufsummiert. | 
Menge in Bestellung | Zeigt die Menge der Zeile an, die aktuell in Bestellzeilen vorhanden ist und somit vo

eile an. Je nach Ebene der Baumstruktur wird der Wert von den unteren Ebenen aufsummiert. | 
Menge in Bestellung | Zeigt die Menge der Zeile an, die aktuell in Bestellzeilen vorhanden ist und somit voraussichtlich dem Lager zugeht. | 
Menge in FA | Zeigt die Menge der Zeile an, die sich aktuell in einer Fertigungsauftragszeile befindet und somit voraussichtlich dem Lager zugeht. | 
Menge in Komponentenzeilen | Zeigt die Menge der Zeile an, die sich aktuell in einer FA-Komponentenzeile befindet und somit voraussichtlich vom Lager abgebucht wird. | 
Menge in Auftrag | Zeigt die Menge der Zeile an, die sich aktuell in einer Verkaufsauftragszeile befindet und somit voraussichtlich vom Lager abgebucht wird. |

Erläuterung zu den Aktionen der Materialbestände:

Aktionsname | Erläuterung | 
Liste bearbeiten | Ändert den Modus der Liste von „Bearbeiten“ auf Ansicht und umgekehrt. | 
Eigenschaftssuche | Öffnet den aktuell gültigen Eigenschaftsfilter. Die User können hier nachträglich Modifikationen vornehmen, um das Ergebnis der Materialbestände anzupassen. | 
Karte | Öffnet bei den Ebenen mit einer Artikelnr. oder einer Chargennr. entweder die Artikelkarte der Zeile oder die Chargeninformations-karte der Zeile. |

Erläuterung zu den Infoboxen in den Materialbeständen:

Infoboxname | Erläuterung | 
Verfügbarkeit | Zeigt die Verfügbarkeit der jeweiligen ausgewählten Zeile, die sich nach der Werte-Einrichtung richtet. | 
Eigenschaften | Zeigt die Eigenschaften der jeweiligen ausgewählte

uterung | 
Verfügbarkeit | Zeigt die Verfügbarkeit der jeweiligen ausgewählten Zeile, die sich nach der Werte-Einrichtung richtet. | 
Eigenschaften | Zeigt die Eigenschaften der jeweiligen ausgewählten Zeile. | 
Karte | Öffnet bei den Ebenen mit einer Artikelnr. oder einer Chargennr. entweder die Artikelkarte der Zeile oder die Chargeninformations-karte der Zeile. |

Tragen die User nun im Feld „Erfassungsmenge“ einen Wert bei einer Chargenzeile ein und verlassen die Materialbestände, können sie im Anschluss noch über eine Bestätigungsmeldung entscheiden, ob die eingetragenen Mengen übertragen werden sollen.

[image]

[image]

Wird die Bestätigungsmeldung mit „Ja“ bestätigt, wird automatisch eine FA-Komponentenzeile und die dazugehörige Artikelverfolgung angelegt.

[image]

[image]

In der Ansicht der Artikelverfolgungszeilen existiert eine Infobox „Eigenschaften“. Hierüber kann der User die Eigenschaften der Charge anpassen. In der Infobox können direkt über alle Chargen aus den Artikelverfolgungszeilen die Chargeneigenschaften geändert werden.

Beispielhaft werden die Materialeigenschaften im Zusammenhang mit einem Verkaufsauftrag gezeigt.

Belegeigenschaften abändern

Haben die User zuvor in der Einrichtung eine oder mehrere Eigenschaften als Verkaufs- oder Einkaufseigenschaft eingerichtet, können sie diese nun in den jeweiligen Belegarten abändern.

Hierfür müssen die User die jeweilige Zeile auswählen und in der Infobox die Aktion „Bearbeiten“ ausführen.

[image]

In der sich nun öffnenden Seite können die User nur die Eigenschaften ändern, die vorher als Belegeigenschaft gekennzeichnet waren.

Ändern sie eine Eigenschaft, wird diese hervorgehoben. Durch Klicken des Buttons „Ok“ können die User die Seite wieder verlassen. Die abgeänderten Werte sind nun für den jeweiligen Beleg gespeichert.

[image]

[image]

Werden nun Folgebelege erstellt, werden die abgeänderten Werte mit übernommen.

Folgebelege können zum Beispiel sein:

Wareneingänge
Warenausgänge
Fertigungsaufträge

[image]

Artikelbeschreibung im Beleg

Je nach Sprachcode des Debitors oder Kreditors und der Einrichtung der Materialart werden in den Belegen für Artikel unterschiedliche Beschreibungen generiert.

[image]

[image]

Anpassen von Chargeneigenschaften

Weicht eine Eigenschaft innerhalb einer Charge ab, können die User diese Eigenschaft innerhalb der Chargeninformationskarte abändern.

Hierfür öffnen sie die „Chargeninformationskarte“ und gelangen über die Aktion „Bearbeiten“ in der Infobox „Eigenschaften“ in die Seite „Eigenschaften editieren“.

r Chargeninformationskarte abändern.

Hierfür öffnen sie die „Chargeninformationskarte“ und gelangen über die Aktion „Bearbeiten“ in der Infobox „Eigenschaften“ in die Seite „Eigenschaften editieren“.

[image]

[image]

[image]

Artikelmatchcodesuche

Zusätzlich zu der normalen Erfassung von Artikeln in Belegen, steht den Usern noch die „Artikelmatchcodesuche“ zur Verfügung. Diese kann aufgerufen werden, indem man in einer Belegzeile den kompletten oder einen Teil des Matchcodes in das Feld „Matchcode“ eingibt.

[image]

[image]

Der User hat auch die Möglichkeit, wenn mehrere Zeilen vorgeschlagen werden, diese zu markieren und diese markierten Zeilen mit den entsprechenden Stückzahlen, Mengen, KG zu übernehmen.

Die Matchcodesuche wird beim Öffnen der Artikelsuche editierbar und es lassen sich Informationen filtern.

Wenn eine Filterung erfolgt ist, werden die entsprechenden Artikel übernommen.

Im Bereich „Allgemein“ wird im Matchcode-Filter die Eingabe aus der Belegzeile angezeigt.

Erläuterung der Felder des Suchergebnisses:

Feldname | Erläuterung | 
Artikelnr. | Zeigt alle Artikelnr. an, die innerhalb des Matchcode-Filters liegen. | 
Variantencode | Zeigt die Variantencodes an, die innerhalb des Matchcode-Filters liegen. | 
Lagerortcode | Zeigt den Lagerort der Belegzeile an. | 
Matchcode | Zeigt den Matchcode der Artikel-Varianten-Kombination an. | 
Beschreibung | Zeigt die Beschreibung der Artikel-Varianten-Kombination an. | 
Beschreibung 2 | Zeigt die Beschreibung 2

n. | 
Matchcode | Zeigt den Matchcode der Artikel-Varianten-Kombination an. | 
Beschreibung | Zeigt die Beschreibung der Artikel-Varianten-Kombination an. | 
Beschreibung 2 | Zeigt die Beschreibung 2 der Artikel-Varianten-Kombination an. | 
Einheitencode | Zeigt den Basiseinheitencode der Artikel-Varianten-Kombination an. | 
Erfassungsmenge | Hier kann der User die Menge in der Basiseinheit eintragen, die er für diesen Artikel in die Belegzeile übernehmen will. Trägt der User bei mehreren Suchergebniszeilen einen Wert ein, werden im Beleg auch mehrere Zeilen angelegt. | 
Verfügbare Menge | Zeigt die Menge der Artikel-Varianten-Kombination an, die auf dem Lagerortcode der Zeile zur Verfügung steht. |

Erläuterung der Felder des Artikelverfolgungssuchergebnisses:

Feldname | Erläuterung | 
Chargennr. | Zeigt die Chargennr. zur ausgewählten Suchergebniszeile an, die verfügbar sind. | 
Seriennr. | Zeigt die Seriennr. zur ausgewählten Suchergebniszeile an, die verfügbar sind. | 
Erfassungsmenge | Hier kann der User die Menge in der Basiseinheit eintragen, die er für diese Chargen- oder Seriennr. in die Belegzeile übernehmen will. Nutzen die User diese Art der Erfassung, werden die Chargen automatisch an die Artikelverfolgung der Belegzeile übertragen. | 
Verfügbare Menge | Zeigt die Menge der Chargen- oder Seriennr. an, die auf dem Lagerortcode der Suchergebniszeile zur Verfügung steht. |

Erläuterung zu den Infoboxen der Matchcodesuche:

Infobox | Erläuterung | 
Artikel - Eigensc

enge der Chargen- oder Seriennr. an, die auf dem Lagerortcode der Suchergebniszeile zur Verfügung steht. |

Erläuterung zu den Infoboxen der Matchcodesuche:

Infobox | Erläuterung | 
Artikel - Eigenschaften | Zeigt die Eigenschaften der Artikel-Varianten-Kombination an, die in den Suchergebniszeilen ausgewählt wurde. | 
Chargen - Eigenschaften | Zeigt die Eigenschaften der Charge an, die in den Artikelverfolgungssuchergebniszeilen ausgewählt wurde. |

Erweiterte Matchcodesuche

Haben die User in der Materialeigenschaftseinrichtung die Erw. Matchcodesuche aktiviert, ändert sich die Seite der Matchcodesuche.

[image]

[image]

Erläuterung der Felder des Registers Allgemein:

Feldname | Erläuterung | 
Matchcode | Gibt initial beim Öffnen der erw. Matchcodesuche den Filter aus der Belegzeile an. Die User können diesen - anders als in der normalen Matchcodesuche - nachträglich anpassen.
Nach dem hier eingegebenen Wert werden die Artikel- und Chargenzeilen nach ihrem Matchcode gefiltert. Auch Teileingaben eines Matchcodes sind möglich. | 
Materialart | Gibt initial beim Öffnen der erw. Matchcodesuche den Wert der Materialart aus der Materialeigenschaftseinrichtung an.
Geben die User eine Materialart an und führen anschließend die Aktion „Eigenschaftssuche“ aus, werden die Artikel- und Chargenzeilen nach dieser Materialart gefiltert. | 
Gewünschtes Lieferdatum | Gibt initial beim Öffnen der erw. Matchcodesuche den Wert des Feldes gewünschtes Lieferdatum des Beleges an.
Ist dieses Fe

Chargenzeilen nach dieser Materialart gefiltert. | 
Gewünschtes Lieferdatum | Gibt initial beim Öffnen der erw. Matchcodesuche den Wert des Feldes gewünschtes Lieferdatum des Beleges an.
Ist dieses Feld gefüllt, werden die verfügbaren Mengen in den Artikel- und Chargenzeilen auf den Wert dieses Feldes gefiltert. | 
Lagerort | Ist dieses Feld gefüllt, werden die verfügbaren Mengen in den Artikel- und Chargenzeilen auf den Wert dieses Feldes gefiltert. | 
Artikelsuche | Initialwert dieses Feldes wird durch die Materialeigenschaftseinrichtung bestimmt.
Ist diese Einstellung aktiviert, werden Suchergebnisse in den Artikelzeilen angezeigt, wenn diese auf Lager liegen. | 
Chargensuche | Initialwert dieses Feldes wird durch die Materialeigenschaftseinrichtung bestimmt.
Ist diese Einstellung aktiviert, werden Suchergebnisse in den Chargenzeilen angezeigt, wenn diese auf Lager liegen.
Ist nicht kompatibel mit „Alles anzeigen“. | 
Alles anzeigen | Initialwert dieses Feldes wird durch die Materialeigenschaftseinrichtung bestimmt.
Ist diese Einstellung aktiviert, werden in den Artikelzeilen alle möglichen Artikel-Lagerort-Kombinationen angezeigt, die zu den restlichen Filterkriterien passen.
Ist nicht kompatibel mit der Chargensuche und „In Bestellung“. | 
In Bestellung | Initialwert dieses Feldes wird durch die Materialeigenschaftseinrichtung bestimmt.
Ist diese Einstellung aktiviert, werden zusätzlich zu den auf Lager liegenden Artikel- und Chargenzeilen auch die angezeigt, die aktuell

Feldes wird durch die Materialeigenschaftseinrichtung bestimmt.
Ist diese Einstellung aktiviert, werden zusätzlich zu den auf Lager liegenden Artikel- und Chargenzeilen auch die angezeigt, die aktuell in Einkaufsbestellzeilen enthalten sind und innerhalb des gewünschten Lieferdatums liegen. |

[image]

Erläuterung zu den Aktionen der erw. Matchcodesuche:

Aktionsname | Erläuterung | 
Eigenschaftssuche | Filtert die Ergebnisse der Artikel- und Chargenzeilen nach den in den Eigenschaftsfiltern vorhandenen Filtern ein. | 
Filter entfernen | Löst den Eigenschaftsfilter auf. | 
Variantenartikel erstellen | Erstellt einen neuen Variantenartikel zu der ausgewählten Artikelzeile. Nach der Erstellung eines neuen Variantenartikels werden die User gefragt, ob nur nach diesem Variantenartikel gefiltert werden soll. | 
Basisartikel kopieren | Kopiert den Basisartikel der ausgewählten Artikelzeile. |

Die User können im Bereich des Eigenschaftsfilters nun ihren individuellen Filter für die ausgewählte Materialart hinterlegen und so die Artikel- und Chargenzeilen auf eine weitere Weise filtern. Haben sie Filterargumente eingegeben, können sie den Eigenschaftsfilter durch die Aktion „Eigenschaftssuche“ aktivieren.

Erläuterung zu den Feldern des Eigenschaftsfilters:

| Feldname | Erläuterung |
|--- |--- |
|Eigenschaftscode|Gibt den Eigenschaftscode der Eigenschaft an, die zu der Materialart zugeordnet ist, die im Feld Materialart ausgewählt wurde.|
|Eigenschaftsname|Gibt den Namen der Eigens

--- |--- |
|Eigenschaftscode|Gibt den Eigenschaftscode der Eigenschaft an, die zu der Materialart zugeordnet ist, die im Feld Materialart ausgewählt wurde.|
|Eigenschaftsname|Gibt den Namen der Eigenschaftscodes an.|
|Filterwert|Hier können die User den Filterwert mit den bekannten Microsoft Dynamics 365 Business Central Filterargumenten für den jeweiligen Eigenschaftscode angeben.
Über den Assis Edit Button stehen den Usern außerdem die Eigenschaftswerte zur Verfügung.|
Erläuterung zu den Feldern der Artikelzeilen:

Feldname | Erläuterung | 
Artikelnr. | Gibt die Artikelnr. an, die zu den eingegebenen Filterargumenten passen.
Ist kein Lagerort angegeben und es sind mehrere Lagerorte in der Auswahl möglich, werden Artikelnummern pro Lagerort dargestellt. | 
Matchcode | Gibt den Matchcode zur Artikelnr. an. | 
Beschreibung | Gibt die Beschreibung zur Artikelnr. an. | 
Beschreibung 2 | Gibt die Beschreibung 2 zur Artikelnr. an. | 
Variantencode | Gibt die Variantencodes an, die zu den eingegebenen Filterargumenten passen. | 
Lagerortcode | Gibt die Lagerorte zu den Artikelzeilen an. | 
Einheitencode | Gibt Basiseinheitencode zu der Artikelzeile an. | 
Verfügbare Menge (Artikelverfolgung) | Gibt die Menge an, die für alle definierten Artikelverfolgungen der Artikelzeile zur Verfügung stehen.
Wichtig:
Hierbei kann es sein, dass die verfügbare Menge (Artikelverfolgung) größer ist als die verfügbare Menge (Artikel). Dies ist der Fall, wenn es bereits weitere Verkaufszeilen gibt, in

g stehen.
Wichtig:
Hierbei kann es sein, dass die verfügbare Menge (Artikelverfolgung) größer ist als die verfügbare Menge (Artikel). Dies ist der Fall, wenn es bereits weitere Verkaufszeilen gibt, in denen diese Artikel-Lagerort-Kombination verwendet wird, jedoch noch keine Artikelverfolgung vorgenommen wurde. | 
Verfügbare Menge (Artikel) | Gibt die Menge an, die für die Artikelzeile zur Verfügung steht. | 
Erfasste Menge | Hier können die User eine Menge angeben, die später in die Verkaufszeile übertragen wird.
Ist die Verteilungslogik in der Materialeigenschaftseinrichtung auf FiFo gestellt, werden durch das manuelle Eintragen einer Menge auch automatisch die Chargenzeilen zugeordnet. | 
Komplette Menge zuordnen | Wird dieses Boolean-Feld aktiviert, so wird automatisch die komplette verfügbare Menge (Artikel) in das Feld erfasste Menge übertragen. | 
Lagerbestand | Flow-Field, das den aktuellen Lagerbestand des Artikels wiedergibt.
Wichtig:
Hierbei ist zu beachten, dass der Lagerbestand abweichend zu den verfügbaren Mengen-Feldern sein kann. Dies ist der Fall, wenn bereits z.B. Verkaufszeilen für diese Artikel-Lagerort-Kombination vorhanden sind, die noch nicht geliefert wurden. | 
Menge (Bestellung) | Zeigt die Menge der Artikelzeile an, die aktuell in Einkaufsbestellungen vorhanden sind, die noch nicht geliefert wurden. | 
Einstandspreis | Gibt den Einstandspreis der Artikelzeile an. | 
Gesperrt | Gibt an, ob der Artikel hinter der Artikelzeile gesperrt ist. | 
Warenaus

orhanden sind, die noch nicht geliefert wurden. | 
Einstandspreis | Gibt den Einstandspreis der Artikelzeile an. | 
Gesperrt | Gibt an, ob der Artikel hinter der Artikelzeile gesperrt ist. | 
Warenausgangsdatum | Hier können die User ein Warenausgangsdatum definieren, das an die Verkaufszeile übertragen wird. |
