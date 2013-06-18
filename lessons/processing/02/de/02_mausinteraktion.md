# Mausinteraktion
## Grundlagen für die Gestaltung interaktiver Programme

> Nach einer kurzen Einführung in die Erstellung unendlich fortlaufender Programme werden die Grundlagen für die Interaktion mit der Maus in Processing vorgestellt. Dabei wird auf die Verwendung der Mausposition sowie auf die Abfrage der Maustasten eingegangen.

---

### Vorbereitung: Fortlaufende Programme

Processing unterscheidet grundsätzlich zwei Programm-Modi: _statisch_ und _aktiv_. Im bisherigen Verlauf haben wir nur im _statischen_ Modus gearbeitet, weshalb alle geschriebenen Programme nach einmaligem Durchlaufen beendet wurden. Das Resultat wird im definierten Fensterbereich abgebildet, weitere Modifikationen am Dargestellten durchzuführen ist jedoch nicht möglich. Um dies zu ermöglichen müssen im Programm spezielle Bereiche angelegt werden, die _Blöcke_ genannt werden:

  * Block 1: **setup()** wird direkt nach dem Programmstart einmalig ausgeführt.
  * Block 2: **draw()** wird nach dem Ablauf von **setup()** ausgeführt und läuft in einer Schleife bis das Fenster geschlossen wird.

Beide Blöcke müssen im Programm vorhanden sein, damit es in den _aktiven_ Modus wechselt. Hat ein Programm also nur den **setup()** oder den **draw()** Block, führt das zu Problemen.

Wenn beide Blöcke vorhanden sind und wir das Programm starten, wird zuerst der Inhalt – also alles zwischen den beiden geschweiften Klammern – des **setup()** Blocks abgearbeitet. Nach Beendigung des **setup()** Blocks springt das Programm in den **draw()** Teil und führt diesen in einer Schleife aus. D.h. sobald die letzte Anweisung im **draw()** Block ausgeführt wurde, springt sie zur ersten Zeile - bis das Sketchfenster geschlossen wird.

###### Bsp.: unendlich laufendes Programm
```processing
// wird bis zum Beenden des Programms
// in einer Schleife aufgerufen
void draw() {
  fill(255, 0, 0, 1);
  rect(10, 10, 80, 80);
}
```

Das Programm zeichnet 60 mal in der Sekunde ein fast nicht sichtbares rotes Quadrat in die Zeichenfläche. Durch die Überlagerungen der einzelnen Objekte addieren sich die transparenten Rechtecke zu einer opaken Form.

###### Bsp.: Initialisierung & Fortlauf
```processing
// wird einmalig beim Start des
// Programms aufgerufen
void setup() {
  fill(0, 125, 0, 50);
  rect(40, 40, 20, 20);
}

// wird bis zum Beenden des Programms
// in einer Schleife aufgerufen
void draw () {
  fill(255, 0, 0, 4);
  rect(10, 10, 80, 80);
}
```

Im **setup()** Block wird zuerst die Füllfarbe auf ein Grün festgelegt in der dann ein Rechteck einmal gezeichnet wird. Nach Beendigung dieser Anweisung wird der **draw()** Block bis zum Schließen des Fensters in einer Schleife ausgeführt. D.h. es wird permanent ein rotes, stark transparentes Rechteck in die Arbeitsfläche gezeichnet. Nach einer gewissen Zeit wurden genügend Rechtecke platziert um das grüne Rechteck fast vollständig zu verdecken.

Diese Prozedur müsste ohne die Unterteilung in **setup()** und **draw()** nach dem folgenden Schema ablaufen:

```processing
// alle Befehle aus dem setup() Block
fill(0, 125, 0, 50);
rect(40, 40, 20, 20);
// alle draw() Durchgänge wiederholt hintereinander
// Durchlauf 1
fill(255, 0, 0, 4);
rect(10, 10, 80, 80);
// Durchlauf 2
fill(255, 0, 0, 4);
rect(10, 10, 80, 80);
// Durchlauf 3
// ...
```

Einen Durchlauf des draw() Abschnitts bezeichnet man als [Einzelbild](http://de.wikipedia.org/wiki/Einzelbild_(Film)) (engl. [frame](https://en.wikipedia.org/wiki/Film_frame), ursprünglich aus dem Film). Processing versucht pro Sekunde 60 dieser Einzelbilder zu erzeugen und im Sketchfenster abzubilden. Diese Bildfrequenz wird im Englischen, und somit auch in Processing, als [frameRate](http://processing.org/reference/frameRate_.html) bezeichnet.

  * **frameRate** beinhaltet die aktuell dargestellte Anzahl von Einzelbildern pro Sekund (frames per second) des Processing Sketches.
  * **frameRate()** erlaubt das Festlegen der Bildfrequnz (wie oft der draw() Block pro Sekunde abgearbeitet wird) durch Angabe einer Ganzzahl. Für Processing stellt es jedoch nur einen Richtwert dar - Abweichungen sind möglich.

###### Bsp.: Bildfrequnz
```processing
void setup() {
  // festlegung der Bildrate auf ein 
  // Bild pro Sekunde
  frameRate(1);
}

void draw() {
   fill(255, 0, 0, 15);
   rect(20, 20, 60, 60);
}
```

### Mausinteraktion
#### Mausposition
Die Kommunikation zwischen Benutzer und Programm kann auf vielfältige Weise geschehen. Im Folgenden wollen wir uns auf die Maus, genauer mit deren Position in der Zeichenfläche, beschäftigen. Die Processingumgebung bietet für diesen Zweck vier Ausdrücke: [mouseX](http://processing.org/reference/mouseX.html), [mouseY](http://processing.org/reference/mouseY.html) für die aktuelle Position der Maus und [pmouseX](http://processing.org/reference/pmouseX.html), [pmouseY](http://processing.org/reference/pmouseY.html) für die Position im vorherigen Bild.
Alle vier Angaben geben dabei die Distanz zum Koordinatenursprung (oben, links) in Pixeln auf der jeweiligen Achse an.

###### Bsp.: aktuelle Mausposition 1
```processing
void draw() {
  ellipse(mouseX, mouseY, 20, 20);
}
```

In jedem **draw()** Durchlauf wird ein Kreis an den aktuellen Mauskoordinaten positioniert. Neu gezeichnete Kreise überlagern die bereits gezeichneten.

###### Bsp.: aktuelle Mausposition 2
```processing
void draw() {
  background(255, 255, 255);
  ellipse(mouseX, mouseY, 20, 20);
}
```

Durch das Aufrufen des background() Befehls wird vor jedem Zeichnen eines Kreises die Arbeitsfläche vollflächig weiß gefüllt. Es scheint als würde sich ein und der selbe Kreis nach den Vorgaben der Maus bewegen.

###### Bsp.: aktuelle und vorherige Mausposition
```processing
void setup() {
    frameRate(5);
}

void draw() {
  background (255, 255, 255);
  line(pmouseX, pmouseY, mouseX, mouseY);
}
```

Bei schneller Bewegung der Maus wird eine schwarze Linie sichtbar. Diese wird zwischen der vorherigen und der aktuellen Mausposition gezeichnet und stellt die zwischen zwei Einzelbildern zurückgelegte Distanz dar. Das "p" in pmouseX und pmouseY steht dabei für den englischen Begriff *previous* (dt.: früher, vorig).

#### Maustasten
Um in einem Processing Programm herauszufinden, ob die Maustaste gedrückt ist, müssen wir lediglich den Zustand der Maustaste "abfragen". Genau eine solche Abfrage können wir mit einem neuen Befehl stellen:

  * **[if](http://processing.org/reference/if.html) (** *Bedingung* **) {...}** also "falls" eine von uns genannte Bedingung "wahr" ist (true), wird der darauf folgende Abschnitt in geschweiften Klammern ausgeführt

Für unsere Abfrage, ob die Taste der Maus gedrückt ist, haben wir nun eine Eigenschaft in unserem Processing Programm ähnlich der [width](http://processing.org/reference/width.html) oder [height](http://processing.org/reference/height.html) Eigenschaft zur Verfügung:

  * **[mousePressed](http://processing.org/reference/mousePressed.html)** ist die Maustaste gedrückt, oder nicht.

Folgendes Beispiel demonstriert, wie man diese Abfrage richtig stellt:

###### Bsp.: Drücken der Maustaste I
```processing
// beim zeichnen kommt nun nichts weiter hinzu
// als die Abfrage, ob die Maus gedrückt ist mit Hilfe
// der "if" Abfrage (Statement)
void draw() {
  // lösche den Hintergrund und fülle ihn mit weiss
  background(255, 255, 255);

  // wenn die Maus gedrückt istâ€¦
  if (mousePressed) {
    // zeichne eine ellipse an der Mausposition
    ellipse(mouseX, mouseY, 10, 10);
  }

  // dieser Teil wird immer ausgeführt
  // (unabhängig vom Mauszustand)
  rect(90, 90, 10, 10);
}
```

Bei einer [if](http://processing.org/reference/if.html)-Abfrage wird immer zwischen Ja und Nein entschieden. Im oberen Beispiel haben wir den Status der Maustaste als Bedingung festgelegt - und zeichnen für den Fall "wahr" einen Kreis. Als Gegenstück zum Ja-Abschnitt können wir einen Bereich definieren der nur ausgeführt wird wenn die Maustaste nicht gedrückt wird ("falsch").

  * **[else](http://processing.org/reference/else.html) {...}** leitet einen Programmblock ein der bei Nichtzutreffen der [if](http://processing.org/reference/if.html)-Bedingung abgearbeitet wird. Dieser Block wird ebenfalls von zwei geschweiften Klammern umfasst.

###### Bsp.: Drücken der Maustaste II
```processing
void draw() {
  // lösche den Hintergrund und fülle ihn mit weiss
  background(255, 255, 255);

  // wenn die Maus gedrückt ist:
  if (mousePressed) {
    // zeichne eine ellipse an der Mausposition
    ellipse(mouseX, mouseY, 10, 10);
  // wenn nicht:
  }else{
    // zeichne ein Rechteck an der Mausposition
    rectMode(CENTER);
    rect(mouseX, mouseY, 30, 30);
  }
}
```

### Anwendungsbeispiele: Mausinteraktion
Elementar für die Interaktion mit der Maus sind Abfragen ob sich ein Punk in einem bestimmten Bereich befindet. Dabei ist es egal, ob es sich um einfache Elemente handelt, wie beispielsweise einer runden Schaltfläche, oder um komplexe Formen die eine Figur in einem Computerspiel darstellen. Das Grundprinzip der Abfrage funktioniert immer nach dem selben Prinzip.

*MISSING EXAMPLE LINKS (9) (10)*