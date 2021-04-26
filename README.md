# Regenwasser Anlage "2020"
Hier ein “kleines Bastelprojekt” das mich schon eine Weile lang beschäftigt.

## Aufgabe und Anforderungen
Aufgabe ist die Steuerung einer Regenwasser-Anlage.

In einem unterirdischen Tank wird das Regenwasser vom Dach des Hauses und was sonst noch so verfügbar ist, also Garage, Gartenhäuschen, etc., gesammelt. Eine fest installierte, druckgesteuerte Tauchpumpe versorgt die Toiletten im Haus und dient der Gartenbewässerung.

Nach anfänglichen Problemen wurde die Anlage Stück für Stück erweitert. So z.B. das automatische Nachfüllen mit Frischwasser falls der Tank leer wird um ein Trockenlaufen des Ansaugtraktes der Pumpe zu verhindern. Dazu sind im unteren Bereich des Tanks zwei Schwimmerschalter installiert. Fällt der Wasserspiegel unter den unteren Schwimmer (“kritischer” Pegel) wird über ein Magnetventil bis über den oberen Schwimmer (“Normaler” Pegel) Frischwasser nachgefüllt. Dies soll eine gewisse Hysterese sicherstellen.

Von diversen “lesson learned” aus Fehlfunktionen in der Vergangenheit haben sich Stand heute folgende funktionale Anforderungen ergeben:

Automatischer Nachlauf bei unterschreiten des “kritischen” Pegels und auffüllen mit Frischwasser bis zum “normalen” Pegel
Im Falle ungültiger Werte für die Wasserstands-Ermittlung (instabiles Signal, Wasser über oberem aber unter unterem Schwimmer), 
z.B. durch defektes Kabel oder Schwimmerschalter, soll die Automatik abgeschaltet werden.
Bei überschreiten der einstellbaren, maximalen Nachlaufzeit wird das Ventil automatisch geschlossen
(z.B. bei Versagen der Frischwasser-Versorgung oder defektem Schlauch)
Die Laufzeit der Pumpe soll überwacht werden und bei Überschreiten eines einstellbaren Maximum abgeschaltet werden.
Sowohl für die Pumpe als auch das Nachlaufventil ist jeweils 3 Modi benötigt
- Manuell EIN
- Manuell AUS
- Automatik

Tritt in einer der 3 Funktionsblöcke (Wasserstands-Ermittlung, Pumpensteuerung, Ventilsteuerung) ein Fehler auf, werden sowohl die Pumpe als auch das Ventil in den “Manuell AUS” Modus versetzt

## Umsetzung
Ein paar Details zur Umsetzung

Um "Nebenfunktionen" wie Logging, remote control, u.s.w. zu erleichtern habe ich mich f. einen Raspberry Pi als "zentrale Intelligenz" entschieden.

Im Regenwasser-Tank sind zwei Schwimmer-Schalter die einen pull-up gegen Masse ziehen.
- "niedrig" 
    - ca. 30cm über dem Tankboden verbaut
    - Offen bei höherem Wasserstand
- "kritisch" 
    - ca. 15cm über dem Tankboden verbaut
    - Offen bei niedrigerem Wasserstand
Durch die "antiparallele" Anordung kann auch eventueller Kabelbruch diagnostiziert werden.

Die eingesetzte Tauchpumpe ist druckgesteuert. D.h. fällt der Druck im Leitungsnetz z.B. durch einen geöffneten Wasserhahn schaltet sich die Pumpe automatisch ein. Beim Erreichen normalen Leitungsdrucks, schaltet die Pumpe ab.
Die Aktivierung wird anhand des Pumpenstroms mit Hilfe eines Stromwandlers detektiert.

Pumpe und Ventil werden jeweils durch ein Relais gesteuert (Pumpe "normal closed", Ventil "normal open"). Um ein längerfristigeres Anziehen der Relais (und damit Wärmeentwicklung) zu vermeiden kommen Bi-stabile Relais zum Einsatz. 
