# Freiformen
## Zeichnen komplexer Formen

> Führt die Befehle vertex() und curveVertex() für das Zeichnen komplexerer Vektor-basierter Formen ein und erklärt die unterschiedlichen Zeichenmodi die beim Zeichnen von Pfaden und geschlossenen Formen in Processing zur Verfügung stehen.

---

### Vertex
Bereits aus Grafikprogrammen wie Photoshop und Illustrator ist uns das Zeichnen von Pfaden bekannt. Durch das Aneinanderreihen von Punkten legt man eine Abfolge von Linien fest, welche als Außenhaut der Form fungieren. In Processing werden diese Punkte durch den Aufruf von vertex() erzeugt. Begonnen und beendet wird das Zeichnen mit beginShape() und endShape():
  * **beginShape()** der Aufruf leitet das Zeichnen einer Freiform ein. Parameter benötigt dieser Befehlt nicht. Durch die Angabe von *POINTS*, *LINES*, *TRIANGLES*, *TRIANGLE_FAN*, *TRIANGLE_STRIP*, *QUADS* und *QUAD_STRIP* kann die resultierende Form eingeschränkt werden (keine vollwertige Freiform mehr). [[processing-reference:beginShape()]]```processing
// beginne eine Freiform
beginShape ();

// beginne nur Punkte zu zeichnen,
// die aber nicht zu verbinden
beginShape (POINTS);

// beginne nur Linien zu zeichnen,
// die resultierende Fläche aber nicht
// zu füllen
beginShape (LINES);
```
  * **endShape()** der Aufruf beendet das Zeichnen der Freiform. Diese setzt sich aus allen zwischen beginShape() und endShape() ausgeführten Zeichenbefehlen (z.B. vertex()) zusammen. Wenn bei beginShape() ein Parameter verwendet wurde, sollte dieser hier ebenfalls angegeben werden. [[processing-reference:endShape()]]```processing
// beendet das zeichnen einer Freiform
endShape ();
```
  * **vertex()** erweitert den formbeschreibenden Pfad um einen neuen Ankerpunkt. Da wir uns in einer zweidimensionalen Zeichenfläche bewegen geben wir die Position durch *x* und *y* Koordinate an. [[processing-reference:vertex()]]```processing
// vertex (x-koordinate, y-koordinate);
vertex (30, 40);
vertex (90, 20);
vertex (60, 70);
...
```

Processing teilt den Ablauf des Zeichnens von Freiformen demnach in drei Schritte:
  - **Einleiten:** Mittels beginShape() teilen dem Programm mit, das wir gleich eine Form zeichnen werden. Alle nun folgenden Punkte sollen zu einer Form bzw. Umrandung, abhänig vom angewendeten Modus, zusammengeführt werden. Modi wie *TRIANGLE_FAN*, *TRIANGLE_STRIP*, etc. stellen zu Beginn große Fehlerquellen dar. Jegliche Form kann auch ohne Angabe solcher Parameter erzeugt werden.
  - **Zeichnen:** In diesem Teil folgt die Formulierung der Freiform. Dies geschieht durch die Angabe der Ankerpunkte - Gestaltung der Outline. In diesem Abschnitt dürfen keine Aufrufe der bisherigen [[lesson:9#visuelle_grundelemente|Zeichenbefehle]] erfolgen! Erst nach dem Schließen der Form können [[lesson:9#ellipse|ellipse()]], [[lesson:9#rechteck|rect()]] wieder zur Verwendung kommen.
  - **Beenden:** Processing bekommt nun durch [[processing-reference:endShape()]] die Anweisung mit allen, seit beginShape() angegebenen Punkten, eine Umriss zu generieren. Je nach vorheriger Angabe von fill() und stroke() ist dieser gefüllt bzw. sichtbar. Der Einsatz von ellipse(), rect(), etc. ist nun wieder gestattet.

###### Bsp.: Freiform 1
In diesem Beispiel wird eine durch fünf Punkte beschriebene Form gezeichnet. Sie ist axial symmetrisch zur y-Achse (Spiegelachse befindet sich auf y=100, die Hälfte der Zeichenfläche) und weiß gefüllt.
Rechts, neben dem gerenderten Ergebnis, ist eine Grafik, welche die Lage der formbeschreibenden Punkte verdeutlicht. Wir beginnen oben-links mit dem Punkt (20, 40) und arbeiten uns Schritt für Schritt an der Outline entlang. Jeder Punkt wird dabei durch den Aufruf von vertex(x,y) definiert. 

```processing
// Größe der Zeichenfläche festlegen
size(220, 220);
// Kantenglättung aktivieren
smooth ();

// Zeichnen einleiten
beginShape ();
// Freiform durch Angabe der Vertexpunkte
// beschreiben (muss nicht geschlossen sein)
vertex (20, 40);
vertex (60, 150);
vertex (110, 190);
vertex (160, 150);
vertex (200, 40);
// Zeichnen beenden
endShape ();
```

###### Bsp.: Freiform 2
Mit dem im Vorherigen angesprochenen Parameter des beginShape() Befehls legt man die Art der Verbindungen zwischen den Vertexpunkten für den gesamten Zeichenprozess fest. Wenn die Initialisierung mit beginShape(LINES) durchgeführt wurde, werden immer zwei aufeinander folgende Punkte zu einer Linie verbunden. *TRIANGLES* erzeugt aus drei Punkten ein Dreieck - ignoriert jedoch in unserem Beispiel den vierten Punkt; *QUADS* generiert ein geschlossenen Viereck.
Alle oben abgebildeten Beispiele wurden auf Basis des unteren Scripts erstellt. Lediglich der Zeichenmodi (im Beispiel *LINES*) wurde ausgetauscht.

```processing
// Kantenglättung aktivieren
smooth ();

// Zeichnen Einleiten
beginShape (LINES);
// Zeichnen der vier Vertexpunkte
vertex (20, 20);  // Linie a, Punkt 1
vertex (40, 80);  // Linie a, Punkt 2
vertex (80, 80);  // Linie b, Punkt 1
vertex (60, 20);  // Linie b, Punkt 2
// Zeichnen Beenden
endShape ();
```

### Curve Vertex
Kurven werden wie die oben kennengelernte Vertexoutline durch eine Reihung von Punkten bestimmt. Jedoch werden die Punkte nicht geradlinig verbunden. Beeinflusst von allen Vertexelementen bewegt sich das "Zeichenwerkzeug" von Anfangs- zu Endpunkt und hinterlässt einen weichen, nicht kantigen, Pfad. Jeder Vertexpunkt wird dabei vom Pfad geschnitten.
Processing benötigt mindestens vier Punkte um eine Kurve abzubilden. Durch die Interpolation müssen Anfangs- und Endpunkt doppelt angegeben werden. Anderenfalls ist die Darstellung verschoben.

  * **curveVertex()** definiert mit *x* und *y*-Koordinate einen Kontrollpunkt der Kurve. Mindestens vier dieser Punkte müssen zwischen beginShape() und endShape() stehen. [[processing-reference:curveVertex()]]

###### Bsp.: Kurve
Bezogen auf das Beispiel "Freiform 1" sind nun die vertex() Aufrufe durch curveVertex() ersetzt worden. Ebenfalls haben wir Start- und Endpunkt dupliziert. Wir erhalten, wie in der bekannten Version, einen Fläche - mit einer abgerundeten Outline.

```processing
// Größe der Zeichenfläche festlegen
size(220, 220);
// Kantenglättung aktivieren
smooth ();

// Zeichnen einleiten
beginShape ();
// Freiform durch Angabe der Kurven-
// kontrollpunkte beschreiben
curveVertex (20, 40);
curveVertex (20, 40);
curveVertex (60, 150);
curveVertex (110, 190);
curveVertex (160, 150);
curveVertex (200, 40);
curveVertex (200, 40);
// Zeichnen beenden
endShape ();
```

###### Bsp.: Kurve modifizieren
Im folgenden Beispiel werden drei Punkte einer Kurve definiert. Um keine fehlerhafter Darstellung zu erhalten sind Punkt 1 (0,0) und Punkt 3 (100, 100) doppelt angegeben. Modifiziert wird der Verlauf der Kurve durch die Position der Maus im Sketchfenster. Auf Grundlage derer Koordinaten wird der mittlere Punkt gesetzt.

```processing
void setup() {
  // Kantenglättung aktivieren
  smooth ();
  // Füllung deaktivieren
  noFill();
}

void draw () {
  // Leere die Zeichenfläche
  background (255);
  
  // Zeichnen Einleiten
  beginShape ();
  curveVertex (0, 0);
  curveVertex (0, 0);
  curveVertex (mouseX, mouseY);
  curveVertex (100, 100);
  curveVertex (100, 100);
  // Zeichnen beenden
  endShape ();
}
```

###### Bsp.: dynamische Pfaderzeugung
Das zweite Beispiel veranschaulicht neben der Verwendung des Befehls curveVertex() die Einbindung einer [[lesson:11#for_schleife|for]]-Schleife, sowie der [[lesson:13#random|random()]] Funktion.
Im globalen Bereich werden zwei elementare Variablen unseres Programms festgelegt:

  * ''step'' repräsentiert den Abstand zwischen den einzelnen Kurvenkontrollpunkten auf der *x*-Achse - Weg welcher von Schleifendurchgang zu Schleifendurchgang durch Multiplikation mit der Zählvariable ''i'' variiert.
  * ''points'' steht für die Anzahl an Kontrollpunkten, welche die Kurve beschreiben. *int* da es nur eine ganze Menge an Punkten geben kann.
Nach der Initialisierung im [[lesson:10#vorbereitung_fortlaufende_programme|setup()]] Block setzen wir noch den Inhalt der Variable ''step''. Dazu teilen wir die Breite der Zeichenfläche durch die Anzahl an Punkten minus eins. Wir erhalte die nötige Distanz zwischen den Kontrollpunkten für eine gleichmäßige Verteilung.
Im draw() Block leeren wir das Sketchfenster zu Beginn. Anschließend weisen wir Processing mit dem Aufruf von beginShape() an aus alle folgenden Punkte ein grafisches Element zu erzeugen. Folgend werden die benötigten Punkte in einer *for*-Schleife generiert. Diese läuft beginnend von der linken Seite der Zeichenfläche bis zur Rechten - startet dann wieder von Neuem. Innerhalb wird jeweils die *x* und *y* Koordinate für den Punkt der aktuellen Position berechnet. Der *y*-Wert ist dabei zufällig (in den Grenzen der [[lesson:10#mausposition|Mausposition]]) beeinflusst. Um den Ersten und Letzten Punkt doppelt anzugeben gibt es für beide Fälle jeweils eine *if* Bedingung. Am Ende schließen wir das Erstellen unseres Elementes mit dem Befehl endShape() ab.

```processing
/* Lege die beiden globalen Variablen "step" und 
 * "points" fest. Sie stehen außerhalb von setup 
 * bzw. draw und sind deshalb überall im Programm 
 * erreichbar. Der Inhalt von step wird im setup-
 * Block gesetzt.
 * Bewege die Maus hoch und runter um die Amplitude 
 * der horizontalen Kurve zu ändern.
 */
float step;
int points = 15;

void setup () {
  // Größe der Zeichenfläche definieren
  size (500, 140);
  // Kantenglättung aktivieren
  smooth ();
  // Anzahl der Einzelbilder pro Sekunde
  // auf fünf beschränken
  frameRate (5);
  // Lege die Schrittweite pro for-Schleifen-
  // durchgang auf der x-Achse fest. Abstand 
  // der Kurvenkontrollpunkte auf der x-Achse.
  step = float (width) / (points - 1);
}

void draw () {
  // lösche den Inhalt der Zeichfläche
  background (255);
  
  // Zeichnen einleiten
  beginShape ();
  
  // führe diese Schleife für die Anzahl
  // von "points" aus (15 mal) - 
  // Kontrollpunkte der Kurve
  for (int i=0; i < points; i = i + 1) {
   
    // berechne die x-Position des Kurvenpunktes
    float posx = i * step;
    // berechne die y-Position des Kurvenpunktes
    float posy = height / 2 + random (-mouseY, mouseY);
    
    // füge den Punkt unserer Fläche hinzu
    curveVertex (posx, posy);
    
    // füge den ersten Punkt doppelt ein
    if (i == 0) {
      curveVertex (posx, posy);
    }
    // füge den letzten Punkt doppelt ein
    if (i == points - 1) {
      curveVertex (posx, posy);
    }
  }
  // Beende das Zeichnen der Freiform
  endShape ();
}
```