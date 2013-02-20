# Mausinteraktion
## Grundlagen für die Gestaltung interaktiver Programme

> Nach einer kurzen Einführung in die Erstellung unendlich fortlaufender Programme werden die Grundlagen für die Interaktion mit der Maus in Processing vorgestellt. Dabei wird auf die Verwendung der Mausposition sowie auf die Abfrage der Maustasten eingegangen.

---

### Vorbereitung: Fortlaufende Programme
Grundsätzlich werden alle im Vorherigen geschriebenen Programme nach einmaligem Durchlaufen beendet. Das Resultat wird im definierten Fensterbereich abgebildet - weitere Modifikationen am Dargestellten durchzuführen ist jedoch nicht möglich. Um dies zu ermöglichen müssen im Programm spezielle Bereiche angelegt werden. Block eins setup() und zwei draw().

  * **setup()** wird direkt nach dem Programmstart einmalig ausgeführt.
  * **draw()** wird nach dem Ablauf von setup() ins Leben gerufen und läuft in einer Schleife bis das Fenster geschlossen wird.

Wenn beide Blöcke vorhanden sind und wir das Programm starten wird zuerst der Inhalt ( {â€¦} ) des setup() Blocks abgearbeitet. Nach Beendigung steigt die Applikation in den draw() Teil ein und führt diesen in einer Schleife aus. D.h. sobald die letzte Anweisung im draw() ausgeführt wurde springt sie zur ersten Zeile im draw() Block - bis das Sketchfenster geschlossen wird.

###### Bsp.: unendlich laufendes Programm
```processing
// Aufruf in einer Schleife
// bis zum Schließen des Fensters
void draw () {
  fill (255, 0, 0, 1);
  rect (10, 10, 80, 80);
}
```

Das Programm zeichnet 60 mal in der Sekunde ein fast nicht sichtbares rotes Quadrat in die Zeichenfläche. Durch die Überlagerungen der einzelnen Objekte addieren sich die Transparenzen und das Quadrat erhält eine bestechende Farbe.

###### Bsp.: Initialisierung & Fortlauf
```processing
// Aufruf einmal direkt nach
// dem Programmstart
void setup () {
  fill (0, 125, 0, 50);
  rect (40, 40, 20, 20);
}

// Aufruf in einer Schleife
// nach Beendigung des "setup" Blocks
// bis zum Schließen des Fensters
void draw () {
  fill (255, 0, 0, 4);
  rect (10, 10, 80, 80);
}
```

Im setup() Block wird nach dem Festlegen der Füllfarbe auf ein Grün ein Rechteck einmal gezeichnet. Nach Beendigung dieser Anweisungen wird der draw() Block bis zum Schließen des Fensters in einer Schleife ausgeführt. D.h. es wird permanent ein rotes, stark transparentes Rechteck in die Arbeitsfläche gezeichnet. Nach einer gewissen Zeit wurden genügend Rechtecke platziert um den grünen Farbton zu verdecken.

Diese Prozedur müsste ohne die Unterteilung in setup() und draw() nach dem folgenden Schema ablaufen:

```processing
// setup() direkt nach dem Programmstart
fill (0, 125, 0, 50);
rect (40, 40, 20, 20);
// draw() in einer unendlichen Schleife
// Durchlauf 1
fill (255, 0, 0, 4);
rect (10, 10, 80, 80);
// Durchlauf 2
fill (255, 0, 0, 4);
rect (10, 10, 80, 80);
// Durchlauf 3
// ...
```

Einen Durchlauf des draw() Abschnitts bezeichnet man als [Einzelbild](http://de.wikipedia.org/wiki/Einzelbild_(Film)) (ursprünglich aus dem Film). Processing versucht pro Sekunde 60 dieser Einzelbilder zu erzeugen und im Sketchfenster abzubilden. Diese Bildfrequenz wird im Bereich der Computergrafik als [[processing-reference:frameRate]] bezeichnet.

  * **frameRate** beinhaltet die aktuell angestrebte Anzahl von Einzelbildern (frames) der Processing Sketches.
  * **frameRate()** erlaubt das Steuern der Bildfrequnz (wie oft der draw() Block pro Sekunde abgearbeitet wird) durch Angabe einer Ganzzahl. Für Processing stellt es jedoch nur einen Richtwert dar - Abweichungen sind möglich.

###### Bsp.: Bildfrequnz
```processing
void setup () {
  // festlegung der Bildrate auf ein 
  // Bild pro Sekunde
  frameRate (1);
}

void draw () {
   fill (255, 0, 0, 15);
   rect (20, 20, 60, 60);
}
```

### Mausinteraktion
#### Mausposition
Die Kommunikation zwischen Benutzer und Programm kann auf vielfältige Weise geschehen. Im Folgenden wollen wir uns auf den Bereich der Maus - deren Position in der Zeichenfläche - beschäftigen. Die Processingumgebung bietet für diesen Zweck vier Ausdrücke: [[processing-reference:mouseX]], [[processing-reference:mouseY]] für die aktuelle Position der Maus und [[processing-reference:pmouseX]], [[processing-reference:pmouseY]] für die Position im vorherigen Bild.
Alle vier Angaben geben dabei die Distanz zum Koordinatenursprung (oben, links) in Pixeln auf der jeweiligen Achse an.

###### Bsp.: aktuelle Mausposition 1
```processing
void draw () {
  ellipse (mouseX, mouseY, 20, 20);
}
```

In jedem draw() Durchlauf wird ein Kreis an der aktuellen Mauskoordinaten positioniert. In der Vergangenheit gezeichnete Kreise befinden sich im Hintergrund und können bei Überlagerungen verdeckt werden.

###### Bsp.: aktuelle Mausposition 2
```processing
void draw () {
  background (255, 255, 255);
  ellipse (mouseX, mouseY, 20, 20);
}
```

Durch das Aufrufen des background() Befehls wird vor jedem Zeichnen eines Kreises die Arbeitsfläche vollflächig weiß gefüllt. Es scheint als würde sich ein und der selbe Kreis nach den Vorgaben der Maus bewegen.

###### Bsp.: aktuelle und vorherige Mausposition
```processing
void setup () {
    frameRate (5);
}

void draw () {
  background (255, 255, 255);
  line (pmouseX, pmouseY, mouseX, mouseY);
}
```

Bei schneller Bewegung der Maus wird eine schwarze Linie sichtbar. Diese wird zwischen der vorherigen und der aktuellen Mausposition gezeichnet und stellt die während eines Zeichenvorgangs zurückgelegte Distanz dar. Das "p" in pmouseX und pmouseY steht dabei für den englischen Begriff previous (dt.: früher, vorig).

#### Maustasten
Um in einem Processing Programm herauszufinden, ob die Maustaste gedrückt ist müssen wir lediglich den Zustand der Maustaste "abfragen". Genau eine solche Abfrage können wir mit einem neuen Befehl stellen:

  * **if (***Bedingung* **)** also "falls" eine von uns genannte Bedingung "wahr" ist (true), wird der darauf folgende Abschnitt in geschweiften Klammern ausgeführt ( {â€¦} )

Für unsere Abfrage, ob die Taste der Mausgedrückt ist, haben wir nun eine Eigenschaft in unserem Processing Programm ähnlich der *width* oder *height* Eigenschaft zur Verfügung:

  * **mousePressed** ist die Maustaste gedrückt, oder nicht.

Folgendes Beispiel demonstriert, wie man diese Abfrage richtig stellt.

###### Bsp.: Drücken der Maustaste I
```processing
// beim zeichnen kommt nun nichts weiter hinzu
// als die Abfrage, ob die Maus gedrückt ist mit Hilfe
// der "if" Abfrage (Statement)
void draw() {
  // lösche den Hintergrund und fülle ihn mit weiss
  background (255, 255, 255);

  // wenn die Maus gedrückt istâ€¦
  if (mousePressed) {
    // zeichne eine ellipse an der Mausposition
    ellipse (mouseX, mouseY, 10, 10);
  }

  // dieser Teil wird immer ausgeführt
  // (unabhängig vom Mauszustand)
  rect (90, 90, 10, 10);
}
```

Bei einer *if*-Abfrage wird immer zwischen Ja und Nein entschieden. Im oberen Beispiel haben wir den Status der Maustaste als Bedingung festgelegt - und zeichnen bei "Wahrheit" einen Kreis. Als Gegenstück zum Ja-Abschnitt können wir einen Bereich definieren der nur ausgeführt wird wenn die Maustaste nicht gedrückt wird.

  * **else** leitet einen Programmblock ein der bei Nichtzutreffen der *if*-Bedingung abgearbeitet wird. Dieser Block wird ebenfalls von zwei geschweiften Klammern umfasst ( {...} ).

###### Bsp.: Drücken der Maustaste II
```processing
void draw() {
  // lösche den Hintergrund und fülle ihn mit weiss
  background (255, 255, 255);

  // wenn die Maus gedrückt istâ€¦
  if (mousePressed) {
    // zeichne eine ellipse an der Mausposition
    // wenn die Maustaste gedrückt ist
    ellipse (mouseX, mouseY, 10, 10);
  }else{
    // zeichne ein Rechteck an der Mausposition
    // wenn die Maustaste nicht gedrückt ist
    rectMode (CENTER);
    rect (mouseX, mouseY, 30, 30);
  }
}
```

### Anwendungsbeispiele: Mausinteraktion
Elementar für die Interaktion mit der Maus sind Abfragen ob sich ein Punk in einem bestimmten Bereich befindet. Angefangen bei simplen Elementen wie beispielsweise rechteckigen Buttons bis hin zu komplexen Ansammlungen die einen Charakter eines Spiels darstellen funktioniert dies immer nach dem selben Prinzip.

[[example:9]]

[[example:10]]