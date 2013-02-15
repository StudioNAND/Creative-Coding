# Funktionen
## Modularisierung, Parametrisierung und Wiederverwendbarkeit von Programm-Code

> Diese Lesson führt Funktionen, sowie deren Verwendung mit Hilfe von Parametern und Rückgabewerten als grundlegenden Bestandteil komplexerer Programme ein und zeigt anhand mehrerer Beispiele, wie sie dazu beitragen können ein Programm verständlicher und effektiver zu gestalten.

---

Bei der Einführung von sich endlos [[lesson:10|wiederholenden Programmen]] haben wir zwei Bestandteile kennengelernt, die wir bisher nicht weiter hinterfragt hatten.

[code|processing]
void setup() {
}

void draw() {
}
[/code]

Auch die Events für [[lesson:37#mausinteraktion|Mouseclicks]] und [[lesson:37#tastaturinteraktion|Tastatureingaben]] funktionierten nach dem selben Prinzip.

[code|processing]
void mousePressed() {
}

void keyPressed() {
}
[/code]

Mithilfe dieser Statements können wir unser Programm bisher in "Funktionsbereiche" unterteilen. Daher kommt auch der Name dieser Bestandteile: //Funktionen.// Jeder dieser Bereiche hat seine fest definierte Aufgabe, z.B.:
  * **setup()** - wird einmal zu Beginn des Programms ausgeführt
  * **void draw()** - wird, je nach [[processing-reference:frameRate()]] pro Sekunde ausgeführt (default 60 Frames pro Sekunde) - Hauptteil unseres Processing Programms.
  * **mousePressed()** - wird **einmal** ausgeführt, wenn die Maus gedrückt wird (Vergleiche dazu [[processing-reference:mousePressed]])
  * **keyPressed()** - wird **einmal** ausgeführt, wenn eine Taste auf der Tastatur gedrückt wird (Vergleiche dazu [[processing-reference:keyPressed]])
Neben den von Processing vordefinierten Funktionen (weitere können über die [[http://www.processing.org/reference/|Reference]] gefunden werden) haben wir auch die Möglichkeit eigene Funktionen zu schreiben und somit Programme gemäß unseren Anforderungen zu strukturieren. Dabei schreiben wir für jede Aufgabe die wir über unseren Code realisieren wollen eine //Funktion//. Diese können wir dann, wann immer wir sie brauchen, aufrufen. Das hat zwei große Vorteile:
  - Unser Code wird kürzer und übersichtlicher.
  - Wir brauchen Codeteile nicht immer und immer wieder zu schreiben, was die Fehlerquote senkt.
Dieses Prinzip, komplexe Aufgaben in ihre Grundbestandteile zu gliedern, um diese später einfach wiederverwenden zu können, bezeichnet man als //Modularität//.

=== Aufbau von Funktionen ===

Funktionen sind aus folgenden Bestandteilen zusammengesetzt: //Name//, //Parameter (auch mehrere)//, //Rückgabewert//. Diese werden im Code wiefolgt notiert:

[code|processing]
// ohne Parameter
Rückgabewert Name () {
}[/code]

[code|processing]
// mit einem Parameter
Rückgabewert Name (Parameter) {
}[/code]

[code|processing]
// mit mehreren Parametern
Rückgabewert Name (Parameter1, Parameter2) {
}[/code]

An der Stelle des Rückgabewertes haben wir bisher nur ''void'' (engl. leer) kennen gelernt - kein Rückgabewert.

==== Funktionen ohne Rückgabewert ====

In ihrer einfachsten Form erledigen Funktionen ihre Aufgaben (z.B. Zeichnen) und geben kein Ergebnis zurück. Bisher haben wir nur diese Art von Funktionen kennengelernt. Bei ihnen steht an Stelle der Rückgabewertes das Schlüsselwort //void//.

[code|processing]
void setup() {
}

void draw() {
  zeichneEllipse();
}

void zeichneEllipse() {
  ellipse(50, 50, 50, 50);
}
[/code]

==== Parameter ====

Um die auszuführende Aufgaben (hier das Zeichnen einer [[lesson:9#ellipse|Ellipse]]) flexibler zu definieren, sodass beim Aufruf z.B. angegeben werden kann wo, oder in welcher Größe die Ellipse gezeichnet werden soll, kann man sich beliebig vieler //Parameter// bedienen. Jede bekannte Variable kann ein Parameter sein. Die Parameter einer Funktion werden, durch Kommata getrennt, in den runden Klammern notiert.

[code|processing]
void setup() {
}

void draw() {
  // Funktionsaufruf mit zwei Parametern
  zeichneEllipse(25, 25);
  zeichneEllipse(75, 75);
}

// Funktion mit zwei float Parametern
void zeichneEllipse(float x, float y) {
  ellipse(x, y, 50, 50);
}
[/code]

==== Rückgabewerte ====

Abseits von Aufgaben, wie dem Zeichnen von zusammengesetzten Formen, die keine Ergebnisse für den weiteren Ablauf der Software erzeugen, gibt es oftmals Fälle in denen man ein Ergebnis von einer Funktion zurück erwartet (bspw. die kompliziertere Berechnung von Positionen oder Flächen uvm.). Die Art des erwarteten Ergebnisses wird durch den Rückgabewert bei der Definition der Funktion definiert. Statt //void// also z.B. //int, float, String, â€¦//.\\ 
Innerhalb der Funktion wird dann das Ergebnis nach Abschluss aller nötigen Schritte mit dem Schlüsselwort //return// zurück zu geben.

[code|processing]
void setup() {
  background(255);
  fill(0);
}

void draw() {
  background(255);
  float d = entfernungZumMittelpunkt(mouseX, mouseY);
  ellipse(50, 50, d, d);
}

// berechnet die Entfernung von einem Punkt (x, y Parameter)
// zum Mittelpunkt der Anwendung
float entfernungZumMittelpunkt(float x, float y) {
  float d = dist(x, y, width/2, height/2);
  // gebe das ergbenis zurück
  return d;
}
[/code]

=== Anwendungsbeispiele ===

====== Beispiel »Kreuze machen« ======

Exemplarisch dient uns als Ausgangspunkt eine Komposition bestehend aus drei auf der Zeichenfläche angeordneten X'en. Sie unterscheiden sich durch Position, Farbgebung und Strichstärke. Der Aufbau, die Proportion und Lage der beiden Linien zueinander, verhält sich bei allen X'en gleich.
**Original Sketch**
[[image:44|right]]

[code|processing]
void setup () {
  size (320, 240);
  background (0);
  smooth ();
  noLoop ();
}

void draw () {
  // draw thick, dark x
  stroke (80);
  strokeWeight (20);
  line (50, 40, 110, 105);
  line (110, 40, 50, 105);

  // draw medium, light gray x
  stroke (210);
  strokeWeight (10);
  line (150, 140, 210, 200);
  line (210, 140, 150, 200);

  // draw thin, white x
  stroke (255);
  strokeWeight (2);
  line (50, 140, 110, 200);
  line (110, 140, 50, 200);
}
[/code]

==== Modulare Version ====

Alle veränderbaren Eigenschaften müssen im Funktionskonstrukt variable formuliert werden. Der Inhalt des Funktionsblocks (zwischen den geschweiften Klammern ''{â€¦}'') dient zum Verfassen des Regelwerks. Die wechselnden Charakteristika werden mit Parametern belegt. Bis auf den Grauton der Strichstärke sind alle Angaben mit dem [[lesson:35|Datentyp]] //float// beschreibbar. Die Namen der im Kopf der Funktion erzeugten Variablen (Parameter) beginnen alle mit dem Wort ''the'', gefolgt von einem Großbuchstaben. Dabei handelt es sich nicht um eine durch Processing vorgegebene Notwendigkeit. Vielmehr soll dadurch die Zugehörigkeit der Variable ersichtlich sein. Alle mit diesem Begriff beginnenden Variablen sind Parameter einer Funktion, wurden nicht in der Funktion erzeugt bzw. sind nicht global verfügbar.\\ 
Mittels dieser Variablen werden im Funktionskörper die notwendigen Zeichenprozesse formuliert. Da der Inhalt der Variablen die unterschiedlichsten Werte enthalten kann, erzielt man durch variable Aufrufe der Funktion verschiedenartige Xe.

[code|processing]
void setup () {
  size (320, 240);
  background (0);
  smooth ();
  noLoop ();
}

void draw () {
  drawCross (50, 40, 60, 80, 20);
  drawCross (150, 140, 60, 210, 10);
  drawCross (50, 140, 60, 255, 2);
}

void drawCross (float theX, float theY, float theSize, int theGrey, float theWeight) {
  stroke (theGrey);
  strokeWeight (theWeight);
  line (theX, theY, theX+theSize, theY+theSize);
  line (theX+theSize, theY, theX, theY+theSize);  
}
[/code]

==== for-Kombination 1 ====

[[image:45|right]]
Nach dem 'manuellen' Aufruf folgt nun das Verpacken der Zeichenanweisung in einer //[[lesson:11#for_schleife|for]]//-Schleife. Genau 20 mal aufgerufen werden die Xe übereinander und leicht nach rechts gezeichnet. Neben der Position ändern sich alle weiteren Parameter durch das Einbeziehen der Zählvariable ''i''.\\ 
Die Funktionsdefinition und deren Aufruf wurden aus Gründen der Lesbarkeit umgebrochen. Bei einer großen Anzahl von Parametern bzw. bei Berechnungen innerhalb des Aufrufes kann dies von Vorteil sein.

[code|processing]
void setup () {
  size (320, 240);
  background (0);
  smooth ();
  noLoop ();
}

void draw () {
  for (int i=0; i < 20; i++) {
    drawCross (90 + i, 
               70 - i / 2, 
               100 + i, 
               70 + i * 4, 
               20 - i);
  } 
}

void drawCross (float theX, float theY, float theSize, 
                int theGrey, float theWeight) {
  stroke (theGrey);
  strokeWeight (theWeight);
  line (theX, theY, theX+theSize, theY+theSize);
  line (theX+theSize, theY, theX, theY+theSize);  
}
[/code]

==== for-Kombination 2 ====

[[image:46|center]]
[[lesson:11|Schleifenkombination]] zwei lässt alle möglichen Parameter der Funktion drawCross() zufällig variieren. Jeder Aufruf erzeugt eine andere Anordnung von 70 Kreuzen, welche sich durch Position, Größe, Stärke und Farbgebung unterscheiden. Da die Graustufe der Strichfarbe eine Ganzzahl (integer) ist, muss der durch [[lesson:13|random()]] generierte Wert mittels int() konvertiert werden. Anderenfalls erhält man beim Ausführen einen Fehler für unlautere Reihenfolge der Datentypen beim Funktionsaufruf.

[code|processing]
void setup () {
  size (320, 240);
  background (0);
  smooth ();
  noLoop ();
}

void draw () {
  for(int i=0; i < 70; i++) {
    drawCross  (random (width), 
                random (height), 
                random (10, 100), 
                int (random (40, 255)), 
                random (1, 18));
  }
}

void drawCross (float theX, float theY, float theSize, int theGrey, float theWeight) {
  stroke (theGrey);
  strokeWeight (theWeight);
  line (theX, theY, theX+theSize, theY+theSize);
  line (theX+theSize, theY, theX, theY+theSize);  
}
[/code]