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
