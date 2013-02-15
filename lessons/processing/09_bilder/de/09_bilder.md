# Bilder
## Arbeiten mit Bildern zur Darstellung, Manipulation und als Grundlage zu Zeichnen weiterer Formen

> Nach einem weiterführenden Teil zu Farben in Processing, in dem u.a. die Extrahierung von Farben aus Pixeln erklärt wird, beschäftigt sich diese Lesson mit dem Laden, Darstellen und Verändern von Bildern in Processing. Anhand mehrerer, visueller Beispiele wird danach die Verwendung von Bildern als Datengrundlage für das Zeichnen anderer Formen eingeführt.

---

### Farben II
In der ersten Lesson<<lesson:9>> wurde das Festlegen von [[lesson:9#farben|Farbwerten]] für die Füllung und Umrandung von [[lesson:9#visuelle_grundelemente|Elementen]] vorgestellt. Mittels der Befehle fill() und stroke() definieren wir seither, in unterschiedlichen Parameterkombinationen, die Anteiligkeit des Rot-, Grün-, Blau- und Alphakanals. Die Angabe aller drei bis vier Werte in den oben genannten Befehlen limitiert unser Arbeiten, da wir immer alle drei (bzw. vier) kennen müssen. Stellen wir uns vor das wir von einer beliebigen Farbe den Rotanteil um 40 erhöhen möchten - fill() erlaubt dies aber nur wenn wir auch die beiden anderen Kanäle (grün und blau) nennen können.
Processing bietet für das Ablegen aller vier Werte den Datentyp color():

```processing
color rot = color (255, 0, 0);           // volles rot
color blau = color (0, 0, 255, 150);  // semitransparentes blau
```

Hinter den Variablen ''rot'' und ''blau'' befindet sich eine komplexe Zahlenkombination, welche mit folgenden Befehlen dekodiert werden kann:
  * **alpha()** auf die Farbe anzuwendende Transparenz zwischen 0-255. [[processing-reference:alpha()]]
  * **blue()** Blauanteil der Farbe zwischen 0-255. [[processing-reference:blue()]]
  * **brightness()** [[processing-reference:brightness()]]
  * **green()** Grünanteil der Farbe zwischen 0-255. [[processing-reference:green()]]
  * **red()** Rotanteil der Farbe zwischen 0-255. [[processing-reference:red()]]
  * **saturation()** Sättigung der Farbe zwischen 0-255. [[processing-reference:saturation()]]

Obacht ist geboten, denn all diese Befehle geben eine Gleitkommazahl zurück. Wenn das Resultat in einer Variable abgelegt werden soll, hat diese vom [[lesson:35#datentypen|Typ]] *float* zu sein. Den Versuch das Speichern auf eine *int* Variable vorzunehmen wird Processing mit einer Fehlermeldung vergelten.
Das oben angesprochene Problem können wir nun mittels der kennengelernten Befehle lösen:

```processing
// Erhöhen des Rotanteils einer beliebigen Farbe "c" um 40
float r = red (c) + 40;
float g = green (c);
float b = blue (c);
c = color (r, g, b);
```

Folgendes passiert bei der Durchführung dieser Zeile: Wir greifen auf die Variable vom Datentyp *color* zu und modifizieren den Anteil des Rotwertes - Grün und Blau bleiben gleich. Dabei wird mit [[processing-reference:color()]] eine neue Farbe generiert; ''c'' wird überschrieben. Als Parameter für das Erzeugen der neuen Farbe greifen wir aber auf die Originalwerte von ''c'' zurück; modifizieren dabei den Rotanteil.

###### Bsp.: Datentyp color
Auf [[lesson:10#mausinteraktion|Mausklick]] wird in diesem Beispiel die Anteiligkeit des Rot in der globalen Variable ''c'' verändert. Im [[lesson:10#vorbereitung_fortlaufende_programme|setup()]] werden zu Beginn alle drei Kanäle definiert, Rot in dem Fall 0. Während im draw() permanent der Hintergrund mit der Farbe ''c'' gefüllt wird, greift der Block mousePressed() in die Farbgebung ein.

```processing
// Globale Farbvariable "c" ist 
// überall im Programm erreichbar
color c;

void setup () {
  // einmaliges setzen der Anteile
  // für grün und blau
  c = color (0, 150, 255);
}

void draw () {
  // permanentes Zeichnen des Hinter-
  // grunds mit der aktuellen Farbe
  background (c);
}

// Führe einmalig pro Mausklick aus
void mousePressed () {
  // Auslesen der Farbkanäle
  // und Erhöhung des Rotanteils
  float r = red (c) + 40;
  float g = green (c);
  float b = blue (c);
  
  // Überprüfe ob der Rotanteil
  // nicht zu hoch wird
  if (r > 255) {
    r = 0;
  }
  // Setze die Anteile von "c" neu
  c = color (r, g, b);
  // Ausgabe zur Überprüfung
  println ("Rot: " + r);
}
```

### Pixelbilder in Processing verwenden
#### Abbilden
In Processing können Bilder geladen, dargestellt und auf komplexe Weise modifiziert werden.
Um ein Bild zu laden benötigen wir den Datentyp *PImage*. Genau wie Ganzzahlen in dem Variablentyp *int* und Flieskommazahlen im *float* abgespeichert werden, werden Bilder in dem Variablentyp *PImage* gespeichert. Bevor wir Bilder im Sketchfenster anzeigen können, müssen wir sie mittels der Funktion loadImage() laden. Dabei ist es Wichtig die Dateiendung (.jpg, .png. gif) mit einzubeziehen und das Ganze in Anführungszeichen zu setzen ("meinBild.jpg"). 
Um anschliessend Bilder im Sketchfenster anzuzeigen bedarf es des image() Aufrufs. Ihm wird das Bildobjekt und die x,y Koordinaten zur Positionierung mitgegeben. Ausgerichtet wird das Bild auf der Zeichenfläche wie ein mit rect() gezeichnetes Rechteck. Grundsätzlich befindet sich der Ursprung oben links, kann aber mittels imageMode() auf das Zentrum verschoben werden.

  * **image()** darstellen eines Pixelbildes an einer durch x und y Koordinate angegebenen Position. Zwei weitere optionale Parameter erlauben das Festlegen der Größenverhältnisse (wenn nicht angegeben werden die Originalwerte benutzt). [[processing-reference:image()]]```processing
PImage img;
...
image (img, 0, 0);
```
  * **imageMode()** legt den Punkt fest an welchem die Position ausgerichtet wird. Es besteht die Wahl zwischen CORNER, CORNERS und CENTER. [[processing-reference:imageMode()]]```processing
imageMode (CENTER); // Zentrum des Bildes
imageMode (CORNER); // obere linke Ecke des Bildes
```
  * **loadImage()** läd ein Bilddokument aus dem data-Ordner (dieser Ordner muss sich im Sketch-Ordner befinden). Das Resultat sollte immer einer PImage Variable zugewiesen werden. [[processing-reference:loadImage()]]```processing
PImage img = loadImage ("test.jpg");
image (img, 0, 0);
```

Alle Inhalten die in Processing verwendet werden sollen (z.B. Bilder) müssen sich in einem Ordner namens "data", im jeweiligen Sketchordner, befinden. Dieser Ordner wird nicht automatisch mit dem Erstellen eines neuen Sketches angelegt.
Navigiere über den Finder/Explorer oder *Apfel* + *k* in den Ordner des aktuellen Projektes und lege den Ordner "data" an. Alternativ kann eine Datei über den Menüpunkt "Sketch -> Add File..." zum Programm hinzugefügt werden. Hierbei legt Processing selbst den "data" Ordner im Projekt Ordner an.

###### Bsp.: Bild laden/darstellen
Dieses Beispiel beinhaltet zwei der drei oben aufgeführten Befehle. Wir erzeugen ein Objekt "img" und weisen ihm das Resultat unseres Aufrufs zum Bildladen zu ("img" beinhaltet nun alle Bilddaten). In der nächsten Zeile rufen wir den image() Befehl auf und teilen Processing mit das geladene Bild an der Position 0,0 im Sketchfenster abzubilden.
Da unser simples Programm keinen setup() oder draw() Block besitzt ist dies eine einmalige Sache.

```processing
// Zeichenfläche auf Größe des 
// zu ladenden Bildes festlegen
size (400, 375);

// Variable "img" zum halten des 
// Bildes festlegen. Bild hinein laden.
PImage img = loadImage ("lego.jpg");

// Bild mittels image() Befehl an der
// Position 0,0 (oben links) abbilden.
image (img, 0, 0);
```

#### Bilder modifizieren
Bilder werden mit der [[processing-reference:tint()]] Funktion eingefärbt. Diese funktioniert genauso wie wir es von fill() & stroke() kennen, bezieht sich aber nur auf Pixelbilder.

```processing
tint (Rot, Grün, Blau, Alpha);
```

Alle anschliessend dargestellten Bilder werden eingefärbt bis der Befehl [[processing-reference:noTint()]] ausgeführt wird.

###### Bsp.: Bilder einfärben
```processing
Pimage img;
img = loadImage ("meinBild.jpg");
tint (102);                       //grau einfärben
image (img, 0,0);
noTint ();                        //Einfärbung deaktivieren
image (img, 50, 0);
```

Um mehrere Farben zu benutzen können wir uns der Farbwert Variable [[processing-reference:color()]] bedienen und so mehrere Farbwerte abspeichern.

###### Bsp.: Bilder mittels color() einfärben
```processing
color yellow = color (220, 214, 41);
color green = color (110, 164, 32);
color red = color (255, 0, 0);

PImage img;
img = loadImage ("meinBild.jpg");

//gelb einfärben
tint (yellow);
image (img, 0, 0);

//grün einfärben
tint (green);
image (img, 33, 0);

//rot einfärben
tint (red);
image (img, 66, 0);
```

#### Auslesen
Die bekannte Vorgehensweise durch Angabe von x und y Koordinate bei der Positionierung und Skalierung von Elementen auf der Zeichenfläche liegt auch bei dem Auslesen von Bildern vor. Alle Bildpunkte (Pixel) sind in einem [[http://de.wikipedia.org/wiki/Kartesisches_Koordinatensystem|kartesischen]] Koordinatensystem angeordnet. Wie im Sketchfenster starten beide Achsen in der oberen linken Ecke an der Position 0,0. Jeder einzelne Pixel ist auf diese Weise eindeutig, durch die Angabe von x und y, identifizierbar.
Wenn wir von Bildpunkten bzw. Pixeln sprechen, beziehen wir uns immer auf den Farbwert an einer bestimmten Stelle. In Processings Funktionsumfang existiert der Befehl get() zum Erfragen von Farbwerten:

  * **get()** gibt den Farbwert eines Bildes oder Pixels zurück, bzw. Bildausschnitt. Das Ergebnis ist vom Datentyp *color*. [[processing-reference:get()]]```processing
PImage img = loadImage ("test.jpg");

// Farbmittelwert des gesamten Bildes
color bild = img.get ();

// Farbwert des Bildpunktes an der Position x:30, y:87
color pixel = img.get (30, 87);

// Bildabschnittes der sich von Position 
// x:10, y:10 um 20 Pixel nach rechts unten erstreckt
color bereich = img.get (10, 10, 20, 20);
```

Zwischen dem Namen des *PImage* Objekts und dem get() Befehl wird ein Punkt gesetzt. Dieser bedeutet wörtlich: Wende den Befehl get() auf das Bildobjekt ''img'' an.

###### Bsp.: Color picker
Unser Farbsucher tritt nur in Aktion, wenn sich der Mauszeiger über dem Bild befindet. Da wir dieses direkt in der oberen linken Ecke positioniert haben, überprüfen wir ob die Maus-x-Position kleiner als die Breite des Bildes ist. Innerhalb des *if* Blocks sucht der get() Aufruf nach dem Farbwert an der Mausposition im Bild und definiert damit eine Variable vom Datentyp *color*. Diese Variable ''c'' nutzen wir im letzten Schritt um die aktuelle Füllfarbe zu setzen.
Befindet sich die Maus nicht über dem Bild - wird der *if* Block nicht ausgeführt; kein [[lesson:9#rechteck|Rechteck]] wird gezeichnet.

```processing
// definiere die globale Variable 
// "img" damit sie überall im Programm 
// für uns verfügbar ist
PImage img;

void setup () {
  // Zeichenfläche auf Größe des
  // zu ladenden Bildes festlegen
  size (480, 375);
  // Kantenglättung aktivieren
  smooth ();
  // Outline deaktivieren
  noStroke ();
  // Variable "img" zum halten des
  // Bildes festlegen. Bild hinein laden.
  img = loadImage ("lego.jpg");
}

void draw () {
  // Hintergrund mit weiß füllen
  background (255);
  // Bild darstellen
  image (img, 0, 0);
  
  // Wenn sich die Maus über dem Bild befindet
  if (mouseX < img.width) {
    
    // lies Farbe an Mausposition aus
    color c = img.get (mouseX, mouseY);
    // setze Farbe als Füllfarbe
    fill (c);
    // zeichne ein Rechteck in den rechten Sketchpart
    rect (405, 5, 70, 365);
  }
}
```

[[example:11]]

[[example:12]]

[[example:13]]

#### Modifizieren
Umgekehrt lassen sich Farbwerte von Bildpunkten durch den Aufruf von set() ändern/modifizieren. Der Aufruf des Befehls muss immer die *x* und *y* Koordinaten, sowie ein Farbwert enthalten. Abwandlungen der Parameteranzahl, siehe get(), sind nicht möglich.

  * **set()** setzt den Farbwert eines Bildpunktes an einer bestimmten Position. [[processing-reference:set()]][code]
PImage img = loadImage ("test.jpg");
img.set (29, 18, color (255, 0, 0));
```

#### Sketch als Bild
Jeglicher grafischer Inhalt der von unseren Programmen im Sketchfenster erzeugt wurde und für uns sichtbar ist, stellt ein Bild (PImage) dar. Dadurch können Anweisungen wie get() und set() zum Auslesen und ändern der Zeichfläche dienen. 

###### Bsp.: Zeichenfläche einfärben
{{ /files/documents/b06_image_gradient.jpg}}
Alle oberhalb abgebildeten Verläufe wurden durch die unten stehenden Zeilen dieses Beispiels generiert. In der dritten Stunde schufen wir erstmals ähnliche Ergebnisse - griffen dabei aber auf Linien zurück, welche unterschiedlich eingefärbt wurden.
Nun definieren wir für jeden einzelnen Punkt auf unserer Zeichenfläche die mittels set() Farbe neu.

```processing
size(255, 255);

// für jede der 255 pixel spalten
for (int px = 0; px < width; px = px + 1) {
  // für jede der 255 pixel zeilen
  for (int py = 0; py < height; py = py + 1) {
    
    // setze den Farbwert für jeden Pixel 
    // auf der Zeichenfläche
    set (px, py, color (px, py, 0));
  }
}
```

#### SVG
**SVG** (Scaleable Vector Graphics) sind wie der Name schon sagt skalierbare Vektor Dateien, die wir im Adobe Illustrator oder Freehand erzeugen können. Der Vorteil dieser Grafiken ist, dass man im Gegensatz zu Pixelbildern ohne Qualitätsverlust skalieren kann.

Um eine eine SVG im Illustrator zu erzeugen, wählt man bei dem Menüpunkt //Speichern unter...// SVG(.svg).

Die selbige Datei muss sich, um sie in Processing laden zu können, ebenfalls im **data** Ordner unseres Sketches befinden.

Wie auch bei dem laden eines Bildes brauchen wir eine Globale Variable, in der die Grafik gespeichert wird. Der Datentyp dazu nennt sich [[processing-reference:PShape]] und der Befehl zum laden [[processing-reference:loadShape()]].

```processing
Pshape meineGrafik;
meineGrafik = loadShape("NameMeinerGrafik.svg");
```

In den beiden Zeilen wird die Variable *meineGrafik* des Typs *SVG* angelegt und anschliessend die .svg Datei geladen und in der Variable gespeichert.
Um die Grafik anschliessend auch darzustellen benötigen wir den Befehl shape(meineGrafik, xPosition, yPosition); 
Optional zur x- und yPosition kann auch die Weite und Höhe angegeben werden. Lässt man die Werte raus, werden die Ursprungswerte (Höhe & Weite) der Grafik übernommen.

###### Bsp.: Laden & darstellen von .svg
```processing
//Variable anlegen
Pshape meineGrafik;

//SVG laden
meineGrafik = loadShape("NameMeinerGrafik.svg");

//SVG darstellen
shape(meineGrafik, 10, 10, 80, 80);
```

Der zweite Vorteil an SVG ist, dass man diese mittels Processing im Nachhinein beeinflussen kann. So kann die Füllfarbe und die Strichfarbe wie gewohnt modifiziert werden.

Mittels dem Befehl [[processing.org/reference/PShape_getWidth_.html|getWidth()]] ist es möglich auf die Weite der geladenen SVG zuzugreifen und so z.B. die Ursprungsgrösse proportional zu vergrössern / zu verkleinern. Das gleiche gilt respektive für die Höhe mit [[http://www.processing.org/reference/PShape_getHeight_.html|getHeight()]]

###### Bsp.: SVG laden & modifizieren
```processing
// Die Datei "stifte.svg" muss sich im data Ordner
// des aktuellen Sketches befinden, um geladen zu werden

//Variable initalisieren
PShape s;

void setup(){

  size(400, 200);
  background(255);

  //SVG laden
  s = loadShape("stifte.svg");
  smooth();
}

void draw(){

  //Durch noLoop() wird der ganze block nur 1* ausgeführt
  noLoop();
  noFill();

  //SVG darstellen und die Ursprungsgröße um ein 4faches vergrössern
  shape(s, 50, 50, s.getWidth() *4, s.getHeight()*4);

  //Den Stil der SVG ausschalten â€¦
  s.disableStyle();

  //â€¦ und überschreiben
  strokeWeight(0.25);
  fill(242, 250, 34, 125);
  stroke(0,0,255);

  //SVG darstellen und die Ursprungsgröße um ein 5faches vergrössern
  shape(s, 200, 50, s.getWidth()*5, s.getHeight()*5);
}
```
Weiter Befehle findet ihr in der Referenz von [[http://www.processing.org/reference/PShape.html|PShape]]