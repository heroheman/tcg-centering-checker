# TCG Centering Checker

Misst das Centering von Sammelkarten (Pokémon, One Piece, MTG, Lorcana, Yu-Gi-Oh! …) anhand eines Fotos und zeigt, welche Centering-Note bei den großen Gradern maximal drin ist.

**Live:** https://heroheman.github.io/tcg-centering-checker/

Eine einzige statische HTML-Datei, ohne Build, ohne Server, ohne Abhängigkeiten. Alle Daten bleiben im Browser.

## Funktionen

- **Foto laden** per Dateiauswahl, Drag & Drop oder aus der Zwischenablage (⌘/Strg + V).
- **Zwei Messarten**
  - *Linien:* je 4 Linien horizontal und vertikal (Kartenrand außen, Innenrahmen innen).
  - *Punkte:* je Achse 2 Messstrecken mit 4 Punkten. Das Ergebnis ist der Mittelwert; die Strecken dürfen leicht schräg liegen, und unterschiedliche Werte der beiden Strecken zeigen einen schief gedruckten Innenrahmen.
- **Feine Drehung** bis ±5° in Schritten bis 0,001°.
- **Entzerren:** bei schräg fotografierten Karten die 4 Ecken setzen; das Bild wird per Perspektivkorrektur auf das echte Kartenformat (63 × 88 mm oder 59 × 86 mm) gerechnet. Das Originalfoto bleibt erhalten.
- **Lupe** fest in der Ecke oder am Cursor, Zoom 1,5× bis 12×.
- **Mehrere Karten** mit Vorder- und Rückseite, gespeichert im Browser.
- **Noten** für PSA, CGC, BGS, SGC, TAG und EDGE (10 bis 7) sowie die Centering-Punkte von AOG.

## Bedienung

| Aktion | Eingabe |
| --- | --- |
| Linie / Punkt verschieben | ziehen; mit <kbd>Alt</kbd> 10× feiner |
| Ausgewählte Linie / Punkt nudgen | Pfeiltasten, mit <kbd>Shift</kbd> grob |
| Drehen | <kbd>Q</kbd> / <kbd>E</kbd> ±0,01°, mit <kbd>Shift</kbd> ±0,1°, mit <kbd>Alt</kbd> ±0,001° |
| Lupe umschalten | <kbd>L</kbd> (Aus, Ecke, Cursor) |
| Lupen-Zoom | Regler oder Mausrad über dem Bild |

Tipps für gute Messungen: Karte ohne Sleeve oder Toploader auf einfarbigem Untergrund fotografieren, möglichst senkrecht von oben und lieber mit etwas Abstand und Zoom als mit Weitwinkel. Perspektivische Schräglage korrigiert *Entzerren*; Linsenverzeichnung und gewölbte Karten nicht.

## Berechnung

Pro Achse gilt: Anteil links = linker Rand / (linker + rechter Rand), entsprechend oben/unten. Für die Note zählt die schlechtere Achse.

| Grader | Vorne 10 / 9 / 8 / 7 | Hinten 10 / 9 / 8 / 7 | Quelle |
| --- | --- | --- | --- |
| PSA | 55 / 60 / 65 / 70 | 75 / 90 / 90 / 90 | [edgegrading.com](https://edgegrading.com/centering/) (Standard ab 2025) |
| CGC | 55 / 60 / 65 / 70 | 75 / 90 / 90 / 90 | [cgccards.com](https://www.cgccards.com/card-grading/grading-scale/); Rückseite ab Note 8 nicht veröffentlicht, wie PSA angenommen |
| BGS | 50 / 55 / 60 / 65 | 50 / 70 / 80 / 90 | [edgegrading.com](https://edgegrading.com/centering/); die 10 ist „Pristine“ |
| SGC | 55 / 60 / 65 / 70 | 55 / 60 / 65 / 70 | [edgegrading.com](https://edgegrading.com/centering/) |
| TAG | 55 / 60 / 65 / 70 | 65 / 75 / 95 / 99 | [taggrading.com](https://taggrading.com/pages/scale) (Rückseite TCG) |
| EDGE | 55 / 60 / 70 / 75 | 70 / 80 / 90 / 90 | [edgegrading.com](https://edgegrading.com/centering/) |

**AOG** vergibt fürs Centering 0 bis 100 Punkte: je Achse sind 5 Prozentpunkte Unterschied zwischen beiden Seiten frei, jeder weitere kostet einen Punkt. Bei 50 Punkten oder weniger oder einem Verhältnis ab 2/3 zu 1/3 gilt die Karte als „Offcenter (OC)“. Die Gesamtwertung gewichtet die Vorderseite mit 100 % und die Rückseite mit 70 % ([AOG Beurteilungsskala](https://ao-grading.com/blogs/news/aog-beurteilungs-skala)).

Die Werte sind eine Orientierung, keine Garantie. Grader messen mit eigenen Verfahren und runden unterschiedlich.

## Daten

Kartennamen, Linien und Einstellungen liegen im `localStorage`, die Fotos in `IndexedDB` des Browsers. Nichts wird hochgeladen. Daten sind pro Browser und Gerät; wer die Website-Daten löscht, löscht auch die Karten.

## Entwicklung

Alles steckt in [`index.html`](index.html). Lokal reicht ein beliebiger statischer Server, zum Beispiel:

```bash
python3 -m http.server 8000
```

Danach http://localhost:8000 öffnen. Die Rechenlogik prüft sich beim Laden selbst per `console.assert` (Verhältnis, Notenschwellen, AOG-Beispiel, Perspektivkorrektur); Fehler erscheinen in der Browser-Konsole.

Deployment: GitHub Pages aus dem Branch `main`, Ordner `/`.
