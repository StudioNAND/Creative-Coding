# Transformationen
## Verschieben, Drehen, Skalieren

> Transformationen beschreiben die Ã„nderung des Zustands (visueller) Elemente. Diese Lesson führt die drei Grundeigenschaften Translation, Rotation und Skalierung sowie deren Manipulation ein. Dabei steht die Ausrichtung visueller Elemente zueinander und zu ihrer Umgebung mit Hilfe der Befehle pushMatrix() und popMatrix() im Vordergrund.

---

Bisher haben wir in Processing lediglich die Möglichkeit kennengelernt, einfache [[lesson:9#visuelle_grundelemente|geometrisch Grundformen]] in der Sketch anhand der aufgerufenen Methoden zu positionieren. Auch bei [[lesson:15|Bildern]] und [[lesson:16|Texten]] funktionierte das nur nach diesem Prinzip:

```processing
// zeichne ein Rechteck an der Position x, y
rect(x, y, breite, höhe);
// zeichne ein Bild an der Position x, y
image(img, x, y);
// zeichne Text an der Position x, y
text("Creative Coding", x, y);
```

{{/files/documents/b09_00.png}}
Die Möglichkeiten bei der Positionierung visueller Elemente sind jedoch schnell erschöpft. So gibt es bisher z.B. keine Funktion mehrere, gezeichnete Elemente gleichzeitig zu verschieben, zu drehen oder gar zu skalieren. Im folgenden Kapitel dreht sich deshalb alles um die Funktionen translate(), rotate() und scale(). Diese Funktionen werden unter dem Begriff "Transformation" zusammengefasst. Eine Transformation eines graphischen Elements beschreibt demzufolge seine Verschiebung, Drehung und Skalierung im Raum.

### Verschieben
{{/files/documents/b09_01_translate.png}}
Der wichtigste Bestandteil einer Transformation ist das Versetzen des Ursprungs von dem aus das Element gezeichnet wird. Das kann über den Befehl translate erreicht werden:
  * **translate()** verschiebt das gesamte Koordinatensystem der Zeichenfläche um die Parameterangaben von *x* und *y*. [[processing-reference:translate()]]```processing
float x = 41;
float y = 95;
translate (x, y);
```

translate() verschiebt dabei nicht nur den Ursprung des nachfolgenden Objekts, sondern den Ursprung **aller** Objekte, die nachfolgend gezeichnet werden. Diese Funktionsweise ist u.a. einer der Vorteile von translate(), da gezielt Gruppen von graphischen Elementen verschoben werden können. Nach dem Aufruf von translate() verschiebt sich also das gesamte zu Grunde liegende Koordinatensystem. Durch die Parameter von translate() wird die zukünftige *x*- und *y*-Position des Koordinatenursprungs angegeben.

### Rotieren
{{/files/documents/b09_02_rotate.png}}
Über rotate() können alle gezeichneten Element gedreht werden. Dabei werden Elemente nicht um den Punkt gedreht an dem sie gezeichnet werden, sondern um den **Ursprung** von dem aus sie gezeichnet werden. Das heisst, dass der einfache Aufruf von rotate() das gesamte Koordinatensystem der Sketch rotiert. Der einzige Parameter von rotate() gibt den Grad der Drehung im [[http://de.wikipedia.org/wiki/Bogenmass|Bogenmaß]] an, wobei 2 PI einer vollen Drehung entsprechen. Um zwischen Bogenmaß und Gradmaß umzurechnen stellt Processing die Funktionen radians() und degrees() zu Verfügung.
  * **rotate()** dreht das gesamte Koordinatensystem um seinen Ursprung (x:0, y:0) nach dem im Bogenmaß gegebenen Winkel. Eine Drehung von 360 Grad entsprechen dabei 2 PI (6.2831855...). Processing bietet neben dem Ausdruck PI weiterhin HALF_PI und TWO_PI. [[processing-reference:rotate()]]```processing
rotate (1.349);
```
  * **radians()** gibt das Bogenmaß für einen Winkel in Grad zurück. [[processing-reference:radians()]]```processing
// 'rad' = Radiant für 45 Grad
float rad = radians (45);
```
  * **degrees()** stellt das Gegenteil von radians() dar - wandelt eine Winkelangabe vom Bogenmaß in Grad. [[processing-reference:degrees()]]```processing
// 'deg' = Grad für PIviertel
float deg = degrees (PI / 4);
```

###### Bsp.: Rotieren von Elementen
Es werden drei Dreiecke vom relativ nach unten-links verschobenen Sketchursprung (x:0, y:0) aus gezeichnet. Zwischen allen Dreiecken drehen wir die gesamte Zeichenfläche um den Wert von Winkel (genau zwei mal). Da der Winkel bei rotate() mit einem Minus übergeben wird, rotieren wir gegen den Uhrzeigersinn.

```processing
void setup () {
  // Sketchgröße definieren
  size(500, 230);
  // Kantenglättung aktivieren
  smooth ();
  // Outline deaktivieren
  noStroke ();
}

void draw () {
  background (255);

  // Winkeländerung zwischen allen Dreiecken 
  float winkel = PI * 0.09;

  // Koordinatenursprung (0,0) in den Mittel-
  // punkt der Zeichenfläche verschieben
  translate (width * 0.15, height * 0.8);

  // orangenes Dreieck
  fill (255, 125, 0);
  triangle (0, 40, 300, 0, 0, -40);
  
  // Zeichenfläche rotieren
  rotate (-winkel);

  // grünes Dreieck
  fill (125, 255, 0);
  triangle (0, 40, 300, 0, 0, -40);

  // Zeichenfläche rotieren
  rotate (-winkel);
  
  // blaues Dreieck
  fill (0, 125, 255);
  triangle (0, 40, 300, 0, 0, -40);
}
```

#### Rotieren um den relativen Mittelpunkt
Dadurch dass alle Elemente um den Koordinatenursprung gedreht werden, muss man vor dem Rotieren mittels translate() den Koordinatenursprung auf den gewünschten Mittelpunkt verschieben, um ein Objekt um die eigene Achse zu drehen.

###### Bsp.: Rotation um das Zentrum der Zeichenfläche
Schritt eins besteht aus dem Ã„ndern des Zeichenmodus für alle mit rect() gezeichneten Elemente. Wir setzen diesen auf CENTER - nun wir vom Zentrum aus gezeichnet, nicht von der oberen linken Ecke. Im zweiten Schritt setzen wir den Ursprung unseres Koordinatensystems mit translate() auf die Mitte der Zeichenfläche. Die sichtbare Fläche der *x*-Achse geht nun von -250 bis +250; vorher wurde uns der Bereich von 0 bis +500 dargestellt (Selbiges wird für die *y*-Achse durchgeführt). Wenn wir nun ein Quadrat an der Position x:0, y:0 zeichnen liegt dieses genau in der Mitte des Sketchfensters.\\ 
Mit diesen Voraussetzungen können wir beginnen den Teil der Abbildung zu verfassen. In einer Schleife positionieren wir jeweils zwei Quadrate (unterschiedlicher Größe) an x:0, y:0 und generieren jeweils einen Farbwert. Am Ende des draw() Blocks erhöhen wird den Winkel um im nächsten Bild eine weitere Verschiebung zu erhalten. Da eine ganze Umdrehung durch zwei PI (TWO_PI) repräsentiert wird, setzen wir ''winkel'' auf 0 zurück.

```processing
// Anzahl der Quadratpaare
int anzahl = 10;
// aktueller Winkel
float winkel = 0;

void setup () {
  // Sketchgröße definieren
  size(500, 270);
  // Kantenglättung aktivieren
  smooth ();
  // Rechtecke am Mittelpunkt positionieren
  rectMode (CENTER);
  noStroke ();
}

void draw () {
  background (255);
  // Koordinatenursprung (0,0) in den Mittel-
  // punkt der Zeichenfläche verschieben
  translate (width / 2, height / 2);
  
  // Winkel auf 0Â° setzen wenn 360Â° überschritten
  if (winkel > TWO_PI) {
    winkel = 0;
  }
  
  // für jeden Quadratpaar
  for (int i=0; i < anzahl; i = i + 1) {
    // Koordinatensystem um den Winkel drehen
    rotate (winkel);
    
    // großes Quadrat zeichnen (dunkel)
    fill (i * 20, i * 30, 130);
    rect (0, 0, 180 - i * 16, 180 - i * 16);
    // kleines Quadrat zeichnen (hell)
    fill (i * 23, i * 38, 140);
    rect (0, 0, 180 - i * 18, 180 - i * 18);
  }
  // Winkel erhöhen
  winkel = winkel + 0.004;
}
```

###### Bsp.: Rotieren um die X, Y & Z-Achse
Bisher haben wir Elemente im kartesischen Koordinatensystem immer auf zwei Achsen positioniert: der horizontalen *x*-Achse und der vertikalen *y*-Achse. In der dritten Dimension kommt die Z-Achse hinzu, auf der wir Objekte quasi zu uns hin- und wegbewegen können. Im folgenden Beispiel wird eine Linie um die *z*-Achse rotiert, wodurch man einen räumlichen Effekt erhält. Sobald man die *z*-Achse mit einbezieht, muss dem size(weite, höhe) Befehl neben der Weite und Höhe ein dritter Parameter namens **OPENGL** oder **P3D** hinzugefügt werden werden. Dieser bezeichnet einen extra Rendermodus den Processing für die 3D Darstellung benötigt. **OPENGL** muss über die Zeile ''import processing.opengl.*;'' importiert werden, bei P3D ist dies nicht nötig.

```processing
float winkel=0;
void setup(){

  //hinzufügen des P3D Rendermodus 
  size(600, 600, P3D);
  rectMode(CENTER);
  background(255);

}
void draw(){
 
  //Alle Elemente um 200% vergrössern 
  scale(2);

  if(mousePressed){
    winkel=winkel+0.007;
  }
  else{
    winkel=winkel;
  }

  //um die X-Achse rotieren
  rotateX(120);
  translate(146,175);
  for(int i=0;i<350;i=i+5){
    stroke(0,0,0, 18);

    //um die Z-Achse rotieren
    rotateZ(winkel);

    //um die Y-Achse rotieren
    rotateY(i+winkel);

    line(0, 22+winkel*3,-2, 22+winkel*3);
  }
}
```

#### Winkelberechnung zwischen zwei Punkten
Um den Winkel zwischen zwei Punkten zu berechnen, stellt Processing die Funktion zur Verfügung:
  * **atan2()** [[processing-reference:atan2()]]
Diese Funktion berechnet den Winkel eines Punktes (x, y) ausgehend vom Koordinatenursprung im Bereich von -PI bis PI. Um also den Winkel zwischen zwei Punkten zu berechnen, muss vor der Verwendung von atan2() der Koordinatenursprung mit translate() verschoben werden.

```processing
// globales Bildobjekt
PImage boid;

// globale Variablen zum Ablegen 
// der aktuellen Bildposition
float xpos = 0;
float ypos = 0;

void setup () {
  size (500, 266);
  smooth ();
  background (255);
  // Bilder zentriert positionieren
  imageMode (CENTER);
  // Bild in 'boid' ablegen
  boid = loadImage ("boid.png");
}

void draw () {
  background (255);
  
  // nonlineare Bewegung des Bildes zur Maus
  xpos = xpos + (mouseX - xpos) / 10.0;
  ypos = ypos + (mouseY - ypos) / 10.0;
  
  // Koordinatensystem verschieben
  translate (xpos, ypos);
  // Winkel zwischen Maus und Bild berechnen
  float angle = atan2 (mouseY - ypos, mouseX - xpos) + PI/2;
  // Koordinatensystem rotieren
  rotate (angle);
  // Bild darstellen
  image (boid, 0, 0);
}
```

### Skalieren
{{/files/documents/b09_03_scale.png}}
Genau wie translate() und rotate() wirkt sich scale() auf das gesamte Koordinatensystem aus.
  * **scale()** [[processing-reference:scale()]]```processing
scale (3.7);
```
Wie der Name vermuten lässt, wird dabei das Koordinatensystem skaliert, also vergrößert oder verkleinert. 

#### Lösen der Zeichenfläche
Da sich alle Funktionen für die Transformation immer auf das gesamte Koordinatensystem auswirken, gibt es in Processing die Möglichkeit mehrere Korrdinatensysteme von einander abzugrenzen, und so einzelne Transformation unabhängig voneinander anzuwenden. Die beiden Funktionen die dazu nötig heissen:
  * **pushMatrix()** erzeugt eine neue Ebene in der Zeichfläche. Diese übernimmt alle aktuellen Eigenschaften (wie Position und Rotation) vom Hintergrund. [[processing-reference:pushMatrix()]]```processing
// erzeugt eine neue Ebene
pushMatrix();
// verschiebt das Koordinatensystem 
// um 90 Pixel nach rechts
translate (90, 0);
// zeichnet ein Rechteck an x:90, y:0
rect (0, 0, 40, 40);
```

  * **popMatrix()** verbindet die mit pushMatrix() generierte Ebene (bzw. deren Inhalt) mit dem Hintergrund. Nach dem Aufruf von popMatrix() gelten die gleichen Bedingungen für Position und Rotation der Zeichenfläche wie vor dem Aufruf von pushMatrix(). [[processing-reference:popMatrix()]]```processing
// zeichnet ein Quadrat an x:0, y:0
rect (0, 0, 40, 40);

// erzeugt eine neue Ebene
pushMatrix ();
// verschiebt das Koordinatensystem 
// um 60 Pixel nach rechts
translate (60, 0);
// zeichnet ein Quadrat an x:60, y:0
rect (0, 0, 40, 40);
// fügt Ebene und Hintergrund zusammen
popMatrix ();

// zeichnet ein Quadrat an x:0, y:70
rect (0, 70, 40, 40);
```

Mithilfe dieser beiden Funktionen können Koordinatensysteme ([[http://de.wikipedia.org/wiki/Matrix_(Mathematik)|Matrizen]]) der Reihe nach gespeichert (*push*) und wieder abgerufen werden (*pop*). Dieses Konzept wird auch als //Stack (Stapel)// bezeichnet. Die Wirkungsweise von Stacks ist in ungefähr mit Ebenen in Bildbearbeitungsprogrammen (z.B. Adobe Photoshop) vergleichbar. pushMatrix() und popMatrix() grenzen also in Processing "Ebenen" ab, von denen jede ihren eigenen Ursprung, eine Ursprungsrotation und eine Skalierung hat, die mit den in dieser Lesson vorgestellten Funktionen definiert werden können (aber nicht müssen!)

###### Bsp.: Ebenen 1
In diesem Beispiel erzeugen wir nacheinander vier Ebenen. Gleichmäßig auf der Zeichenfläche verteilt und einheitlich rotiert werden sie jeweils, nach dem Zeichprozess, mit dem Hintergrund verbunden. Dabei verwenden wir wieder rectMode(CENTER); um die Quadrate um ihren Mittelpunkt (nicht die obere-linke Ecke) zu drehen. Da wir mit pushMatrix() und popMatrix() arbeiten, werden die Befehle zum Verschieben und Drehen immer auf den ursprünglichen Zustand des Koordinatensystems angewendet. Soll bedeuten - nach dem Aufruf von popMatrix() befindet sich der Ursprung der Sketchfläche wieder bei x:0, y:0 und ist nicht gedreht.

```processing
void setup () {
  // Sketchgröße definieren
  size(500, 140);
  // Kantenglättung aktivieren
  smooth ();
  // Rechteck-Zeichenursprung
  // auf den Mittelpunkt setzen
  rectMode (CENTER);
}

void draw () {
  // führe den 'draw' nur 1mal aus
  noLoop ();
  background (255);

  // Winkeländerung zwischen allen Quadraten 
  float winkel = 0.26;
  
  // QUADRAT 1
  // neue Ebene erstellen
  pushMatrix ();
  // Ebeneursprung nach x:90, y: 70 verschieben
  translate (90, height / 2);
  // Ebene um '0.26' rotieren
  rotate (winkel);
  // Quadrat in Ebene zeichnen
  rect (0, 0, 60, 60);
  // Ebene auf Hintergrund reduzieren
  popMatrix ();
  
  // QUADRAT 2
  pushMatrix ();
  translate (190, height / 2);
  rotate (winkel * 2);
  rect (0, 0, 60, 60);
  popMatrix ();
  
  // QUADRAT 3 ...
  pushMatrix ();
  translate (290, height / 2);
  rotate (winkel * 3);
  rect (0, 0, 60, 60);
  popMatrix ();
  
  pushMatrix ();
  translate (390, height / 2);
  rotate (winkel * 4);
  rect (0, 0, 60, 60);
  popMatrix ();
}
```

###### Bsp.: Ebenen 2
Eine Erweiterung von //Beispiel 1// stellt dieses Script dar. Zwei globale Variable (''anzahl'' und ''rand'') dienen zur Kontrolle des produzierten Ergebnisses und können nach Belieben modifiziert werden. Im [[lesson:10#vorbereitung_fortlaufende_programme|draw()]] Block werden für die Zustandsänderung zwischen den Quadraten die Schritte bei der *x*-Verschiebung und Winkeländerung berechnet und in ''xstep'' und ''astep'' abgelegt. Mittels einer *[[lesson:11#for_schleife|for]]*-Schleife wird der schon in //Beispiel 1// formulierte Zeichenablauf für jedes [[lesson:9#rechteck|Quadrat]] aufgerufen. Die Zählvariable ''i'' steuert dabei den Umfang der Verschiebung auf der *x*-Achse und der Rotation um das Zentrum der Elemente. Weiterhin wird die [[lesson:9#farben|Füllfarbe]] in jedem Durchlauf definiert - wir erhalten einen groben Farbverlauf.\\ 
Dieses Beispiel demonstriert auf anschauliche Weise die "Macht" von [[lesson:11|Schleifen]]. Mit deutlich weniger Aufwand erhalten wir ein komplexere Komposition.

```processing
// Menge der Quadrate
int anzahl = 80;
// Randbreite auf der x-Achse
float rand = 40;

void setup () {
  // Sketchgröße definieren
  size(500, 140);
  // Kantenglättung aktivieren
  smooth ();
  // Rechteck-Zeichenursprung
  // auf den Mittelpunkt setzen
  rectMode (CENTER);
}

void draw () {
  // führe den 'draw' nur 1mal aus
  noLoop ();
  background (255);
  
  // x-Verschiebung pro Quadrat
  float xstep = (width - rand * 2) / anzahl;
  // Winkel-Verschiebung pro Quadrat
  float astep = TWO_PI / (anzahl - 1);
  
  for (int i=0; i < anzahl; i = i + 1) {
    // neue Ebene erstellen
    pushMatrix ();
    // Ebeneursprung verschieben
    translate (rand + i * xstep, height / 2);
    // Ebene um '0.26' rotieren
    rotate (i * astep);
    // Füllfarbe mittels definieren
    fill (i * 13, i * 3, i * 4);
    // Quadrat in Ebene zeichnen
    rect (0, 0, 30, 30);
    // Ebene auf Hintergrund reduzieren
    popMatrix ();
  }
}
```

### Relative Positionierung
Größenverhältnisse und Positionen können auf Basis eines Faktors (Zoomstufe) in Verhältnisse gesetzt werden. Das Resultat ist eine Verkleiner- bzw. Vergrößerung eines existierenden Systems.\\ 
Im Beispiel zeichnen wir ein [[lesson:9#rechteck|Rechteck]] an die Position ''x'':80, ''y'':60 mit der Größe ''w'':100, ''h'':45. Die Position der [[lesson:10#mausposition|Maus]] im Sketch wird auf die Lage eines [[lesson:9#kreis|Kreises]] im von uns gezeichneten Rechteck übertragen. Wenn sich der Cursor im Fenster oben-links befindet, ist der Kreis ebenfalls in der oberen linken Ecke des Vierecks positioniert. In allen Fällen wir die Kreisposition relativ zur Mausposition im Programmfenster berechnet. Die Größenverhältnisse beider Flächen müssen nicht übereinstimmen.
```processing
float boxWidth  = 80;  // Ausschnittbreite
float boxHeight = 60;  // Ausschnitthöhe
float boxX      = 100; // Ausschnitt x-Position
float boxY      = 45;  // Ausschnitt y-Position

void setup () {
  size(320, 240);
  smooth ();
}

void draw () {
  background (255);
  
  // Zeichne Ausschnitt
  noFill ();
  stroke (100);
  rect (boxX, boxY, boxWidth, boxHeight);
  
  // Kreisposition im Ausschnitt
  float x = boxX + boxWidth * ((float) mouseX / width);
  float y = boxY + boxHeight * ((float) mouseY / height);
  
  // Zeichne Kreis
  fill (0);
  noStroke ();
  ellipse (x, y, 14, 14);
}
```