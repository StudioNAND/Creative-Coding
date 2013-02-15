# Events

---

### Mausinteraktion
Bisher haben wir um den Programmfluss zu steuern zwei Funktionsblöcke kennengelernt: **[[lesson:10#vorbereitung_fortlaufende_programme|void setup()]]** als statischen Modus der nur einmal ausgeführt wird und dem Befehle nacheinander einmal ausgeführt werden und **void draw()**, das solange wiederholt wird, bis der Benutzer das Programm unterbricht.

Um verschiedene Tastatureingaben oder [[lesson:10#mausinteraktion|Mausbefehle]] (man spricht auch von Tastatur oder Maus **Events**) abzufragen gibt es neben der der if() abfrage von Processing eigens zur Verfügung gestellte Funktionen.
Diese Funktionen werden nach dem draw() block geschrieben.
Den Abfrage ob die Maus gedrückt wurde haben wir bisher mit

```processing
if (mousePressed) {
  //tue etwas
}
```

kennengelernt. Um komplexere Programme zu schreiben und den Programmfluss sinnvoll und übersichtlich zu gestalten bedienen wir uns nun der Funktion:

```processing
void mousePressed () {
  //tue etwas
}
```

Wie alle Funktionen wird auch diese mit void eingeleitet und von geschweiften Klammern umrahmt.
Diese Funktion wird **einmal** aufgerufen, nachdem ein Mausknopf gedrückt wurde und unterscheidet sich dadurch durch die *if(mousePressed)* Abfrage, da diese, solange sie im draw() loop steht immer wieder durchlaufen wird.

###### Bsp. mousePressed ()
```processing
void setup () {
  //setze die größe der Zeichenfläche auf 100 *100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background(255);
  //antialiasing aktivieren
  smooth();
}

void draw () {
  // draw muss existieren damit unser 
  // programm am Leben bleibt
}

void mousePressed() {
  // Outline deaktivieren
  noStroke();

  // Füllfarbe auf schwarz & semitransparent setzen
  fill(0, 0, 0, 125);

  // Ellipse an der Mausposition zeichnen
  ellipse(mouseX, mouseY, 10, 10);
}
```

Man kann nicht nur abfragen, ob die Maus gedrückt wurde, sondern auch auf die anderen Stati können wir wie folgt zugreifen:
  * **mousePressed()** die Maustaste wurde gedrückt
  * **mouseReleased()** die Maustaste wurde losgelassen
  * **mouseMoved()** die Maus wird bewegt & es ist kein Knopf gedrückt
  * **mouseDragged()** der Mausknopf ist gedrückt und die Maus wird dabei bewegt
Auch für diese Stati müssen wir natürlich Funktionen festlegen:

###### Bsp. mousePressed() & mouseReleased()
```processing
void setup () {
  // setze die größe der Zeichenfläche auf 100x100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background (255);
  // Antialiasing aktivieren
  smooth ();
}

void draw() {
}

void mousePressed() {
  // Outline deaktivieren
  noStroke ();

  //Füllfarbe auf schwarz & semitransparent setzen
  fill (0, 0, 0, 125);

  //Ellipse an der Mausposition zeichnen
  ellipse (mouseX, mouseY, 10, 10);
}

void mouseReleased() {
  // Füllfarbe deaktivieren
  noFill ();

  // Strichfarbe auf rot & semitransparent setzen
  stroke (255, 0, 0, 125);

  // Rechteck von der Mitte aus zeichnen
  rectMode (CENTER);
  // Rechteck an der Mausposition zeichnen
  rect (mouseX, mouseY, 15, 15);
}
```

Nun soll noch ein Punkt an den Maus X 6 Maus Y Koordinaten gezeichnet werden, sobald die Maus bewegt wurde, aber keine Taste gedrückt ist

###### Bsp.: mousePressed() & mouseReleased() & mouseMoved()
```processing
void setup () {
  // setze die größe der Zeichenfläche auf 100x100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background (255);
  // Antialiasing aktivieren
  smooth ();
}

void draw () {
}

void mousePressed () {
  // Outline deaktivieren
  noStroke ();

  // Füllfarbe auf schwarz & semitransparent setzen
  fill (0, 0, 0, 125);

  //Ellipse an der Mausposition zeichnen
  ellipse (mouseX, mouseY, 10, 10);
}

void mouseReleased() {
  // Strichfarbe deaktivieren
  noFill ();

  // Strichfarbe auf schwarz & semitransparent setzen
  stroke (255, 0, 0, 125);

  // Rechteck vom Mittelpunkt aus zeichnen
  rectMode (CENTER);

  // Rechteck an der Mausposition zeichnen
  rect (mouseX, mouseY, 15, 15);
}

void mouseMoved() {
  // Strichfarbe auf schwarz & semitransparent setzen
  stroke (0, 0, 0, 125);

  //Punkt an der Mausposition zeichnen
  point (mouseX, mouseY);
}
```

Im nächsten Beispiel soll der Punkt nur dann gezeichnet werden, wenn der Mausknopf gedrückt und die Maus dabei bewegt wird. Dazu müssen wir lediglich den *mouseMoved()* Block in *mouseDragged()* umbenennen:

```processing
void setup(){
  // setze die größe der Zeichenfläche auf 100x100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background (255);
  // Antialiasing aktivieren
  smooth ();
}

void draw () {
}

void mousePressed () {
  // Outline deaktivieren
  noStroke ();

  // Füllfarbe auf schwarz & semitransparent setzen
  fill (0, 0, 0, 125);

  // Ellipse an der Mausposition zeichnen
  ellipse(mouseX, mouseY, 10, 10);
}

void mouseReleased () {
  // Strichfarbe deaktivieren
  noFill ();

  // Strichfarbe auf schwarz & semitransparent setzen
  stroke (255, 0, 0, 125);

  // Rechteck vom Mittelpunkt aus zeichnen
  rectMode (CENTER);

  // Rechteck an der Mausposition zeichnen
  rect (mouseX, mouseY, 15, 15);
}

void mouseDragged() {
  // Strichfarbe auf schwarz & semitransparent setzen
  stroke (0, 0, 0, 125);

  // Punkt an der Mausposition zeichnen
  point (mouseX, mouseY);
}
```

### Tastaturinteraktion
Genau wie mit der Maus können auch Tastatur Events abgefragt werden. Dabei wird jeder Tastendruck durch die Funktion keyPressed() (Taste wurde gedrückt) und keyReleased() (Taste wurde losgelassen) registriert.
Wie oben beschrieben wird der Code in dem keyPressed() Block einmal ausgeführt, wenn eine Taste gedrückt wurde.

###### Bsp.: keyPressed()
```processing
void setup () {
  // setze die größe der Zeichenfläche auf 100x100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background (255);
  // antialiasing aktivieren
  smooth();
}

void draw () {
}

void keyPressed () {
  // Outline deaktivieren
  noStroke();
  
  // Füllfarbe auf schwarz & semitransparent setzen
  fill(0, 0, 0, 125);

  // Ellipse an einer zufälligen Position in der Zeichenfläche zeichnen
  ellipse(random(height), random(width), 10, 10);
}
```

Im keyPressed() Block ist es zusätzlich möglich abzufragen, welche Taste gedrückt wurde:

###### Bsp.: keyPressed() 2
```processing
void setup () {
  // Setze die größe der Zeichenfläche auf 100x100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background(255);
  //antialiasing aktivieren
  smooth();
}

void draw() {
}

void keyPressed() {
  // Abfrage ob die Taste 'e' gedrückt wurde
  if (key == 'e') {
    // Outline deaktivieren
    noStroke ();
    // Füllfarbe auf schwarz & semitransparent setzen
    fill(0, 0, 0, 125);
    // Ellipse an der Mausposition zeichnen
    ellipse(random(height), random(width), 10, 10);
  }

  // Abfrage ob die Taste 'r' gedrückt wurde
  if (key == 'r') {
    // Füllfarbe deaktivieren
    noFill ();
    //Strichfarbe auf schwarz & semitransparent setzen
    stroke (255, 0, 0, 125);
    //Rechteck an einer zufälligen Position in der Zeichenfläche zeichnen
    rect (random (height), random (width), 10, 10);
  }
}
```

Neben den Buchstabentasten kennt Processing soggenannte Konstanten für die Abfrage spezieller Tasten: (BACKSPACE, TAB, ENTER, RETURN, ESC, DELETE, UP, DOWN, LEFT und RIGHT, â€¦)

###### Bsp.: keyPressed() 3
```processing
void setup() {
  // Setze die Größe der Zeichenfläche auf 100x100 Pixel
  size(100, 100);
  // lösche die Zeichenfläche und fülle sie mit weiss
  background(255);
  // Antialiasing aktivieren
  smooth();
}

void draw () {
}

void keyPressed () {
  // Abfrage ob die Taste 'e' gedrückt wurde
  if (key == 'e') {
    // Outline deaktivieren
    noStroke ();
    // Füllfarbe auf schwarz & semitransparent setzen
    fill (0, 0, 0, 125);
    //Ellipse an der Mausposition zeichnen
    ellipse(random (height), random (width), 10, 10);
  }

  // Abfrage ob die Taste 'r' gedrückt wurde
  if(key == 'r') {
    // Füllfarbe deaktivieren
    noFill ();
    // Strichfarbe auf schwarz & semitransparent setzen
    stroke (255, 0, 0, 125);
    //Rechteck an einer zufälligen Position in der Zeichenfläche zeichnen
    rect (random (height), random (width), 10, 10);
  }
  if (key == BACKSPACE) {
    // fülle die Zeichenfläche mit weiss
    background(255);
  }
}
```