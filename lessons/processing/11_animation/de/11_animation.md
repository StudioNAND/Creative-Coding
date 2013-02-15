# Animation
## Programmierte Bewegung

> Kern dieser Lesson ist die Vermittlung der Grundprinzipien der Animation mit Processing. Ausgehend vom einfachsten Prinzip der Bildfolge, welches oft in der Spielprogrammierung angewendet wird, folgen Erklärungen zu linearer und non-linearer Animation. Dabei stehen eindimensionale Bewegungen ebenso im Mittelpunkt wie die Bewegung auf Kreisen, Ellipsen und Kreissegmenten mit Hilfe von trigonometrischen Funktionen (Sinus und Kosinus),

---

=== Bildanimation ===

Dieser erste Abschnitt steht für die digitale Form eines Daumenkinos. Durch die schnelle Abfolge von ähnlichen, aber nicht gleichen, [[lesson:15#pixelbilder_in_processing_verwenden|Bildern]] in ausreichend zügiger Geschwindigkeit kommt es zur Wahrnehmung einer Bewegung. Alle Bilder werden dafür im Teil des [[lesson:10#vorbereitung_fortlaufende_programme|setup()]] geladen und im [[lesson:10#vorbereitung_fortlaufende_programme|draw()]] je nach Bedarf abgebildet. Die Entscheidung welches der Einzelbilder auf der Zeichenfläche erscheint wird beim automatisierten Ablauf anhand einer Variable gefällt. [[lesson:36|Global instanziert]] bildet sie das Gedächtnis und gibt Aufschluss über die Abspielposition. Mögliche weitere Einflüsse können aber auch Eingaben durch [[lesson:37#tastaturinteraktion|Tastatur]] und [[lesson:37#mausinteraktion|Maus]] sein.

[[example:15]]

==== Lineare Animation ====

Da uns die Mittel gegeben sind durch diverse Zeichenfunktionen den Bildaufbau zu bestimmen, können wir grafische Element durch Modifikation der Position bewegen. Im [[lesson:36|vorherigen Kapitel]], zum Thema: Globale Variablen, haben wir bereits eine [[lesson:9#linie|Linie]] vom oberen Bildschirmrand nach unten fahren lassen. Diesen Fall der Animation nehmen wir nun genauer unter die Lupe.\\ 
Die Linie bewegte sich mit einer konstanten Geschwindigkeit auf der y-Achse. Zwischen allen Bildern wurde die selbe Distanz zurückgelegt - die Beschleunigung können wir deshalb mit 0 angeben. Dieser Fakt macht die Animation zu einer **linearen** Animation: »Konstante Zustandsänderung zwischen allen Einzelbildern.« Erhöhen wir den Weg der zwischen den Einzelbildern beschritten wird, erhalten wir eine schnellere Animation, sie bleibt aber linear.\\ 
Alle drei folgenden Beispielen wiederholen die angesprochene Animation aus Kapitel [[lesson:36]]. Beispiel zwei und drei bedienen sich weiterhin der //if//-Bedingung um Kollisionen mit den Außenseiten des Sketchfensters zu simulieren.

===== Bsp.: lineare Bewegung, eine Richtung =====

{{ /files/documents/b08_01_linear1.png}}
Gezeichnet wird die gleichförmige Ellipse am Wert der globalen Variable ''xpos'' und der Hälfte der Höhe. In jedem Durchlauf des draw()-Blocks erhöhen wir den Wert von ''xpos'' um 1, erhalten damit eine Bewegung des Kreises auf der //x//-Achse vom linken in den rechten Fensterabschnitt. Diese Vorgang findet bis zum Schließen des Fensters statt. Die Position des Kreises würde demnach innerhalb weniger Momente außerhalb des für uns sichtbaren Bereiches sein. Um dies zu lösen integrieren wir eine Bedingung nach dem Aktualisieren der Position (''xpos''). Wir fragen nach dem aktuellen Wert von ''xpos'' und schreiten ein, wenn sich der Kreis nicht mehr im Sketchfenster befindet. Die Intervention schlägt sich im Zurücksetzen des Wertes von ''xpos'' auf 0 nieder - die Animation beginnt wieder von vorn.
Um den Kreis auf beiden Seiten (links und rechts) komplett verschwinden zu lassen, testen wir auf //xpos < width + durchmesser// und setzen der Wert im //if//-Block auf //-durchmesser//.

[code|processing]
// gloable Variable für 
// die Ablage der Position
float xpos = 0;
// und den Kreisdurchmesser
float durchmesser = 30;

void setup () {
  // Größe des Sketches definieren
  size(320, 240);
  // aktiviere Kantenglättung
  smooth ();
}

void draw () {
  // Hintergrund leeren
  background (45);
  
  // Position modifiziere
  xpos = xpos + 1;
  
  // Zurücksetzen der Kreisposition auf die linke 
  // Bildschirmseite wenn die Position größer als 
  // Bildschrimbreite + Durchmesser ist
  if (xpos > width + durchmesser) {
    xpos = -durchmesser;
  }
  
  // Zeichnen des Kreises an die aktuelle Position
  ellipse (xpos, height / 2, durchmesser, durchmesser);
}
[/code]

====== Bsp.: lineare Bewegung, loop ======

{{ /files/documents/b08_02_linear21.png}}
Als zweiten Schritt geben wir uns die Auflage den Kreis auf der Horizontalen pendeln zu lassen. Zur Realisierung bedarf es der Information in welcher Richtung wir ihn momentan bewegen sollen. Dafür legen wir die Variable ''geschwindigkeit'' an, die ebenfalls den Weg beinhaltet, um welchen der Kreis zwischen den Einzelbilden verschoben wird. Im vorherigen Beispiel haben wir dies zu Beginn des draw() mit ''xpos + 1'' definiert.
Neben dieser änderung kommt eine zweite //if//-Bedingung hinzu. Wir müsse bei Beiden, der linken und rechten Fensterseite, intervenieren, wenn sich der Kreis aus unserer Fläche bewegen sollte. Diese Eingriffe bewirken eine Umkehrung der Richtung, festgelegt durch ''geschwindigkeit''. Wenn der Wert von ''geschwindigkeit'' positiv ist, bewegt sich der der Kreis von links nach rechts. Ist er negativ, von rechts nach links. Das Invertieren geschieht durch die Multiplikation mit -1.

[code|processing]
// gloable Variable für 
// die Ablage der Position
float xpos;
// Positionsänderung pro Einzelbild
float geschwindigkeit = 2;
// Kreisdurchmesser
float durchmesser = 30;

void setup () {
  // Größe des Sketches definieren
  size(320, 240);
  // aktiviere Kantenglättung
  smooth ();
  // Startposition
  xpos = width / 2;
}

void draw () {
  // Hintergrund leeren
  background (45);

  // Umkehr der Richtung wenn die Position 
  // des Kreises sich am rechten Fensterrand ist
  if (xpos > width - durchmesser / 2) {
    geschwindigkeit = geschwindigkeit * -1;
  }
  // Umkehr der Richtung wenn die Position 
  // des Kreises sich am linken Fensterrand ist
  if (xpos <  durchmesser / 2) {
    geschwindigkeit = geschwindigkeit * -1;
  }

  // Position modifizieren, 'geschwindigkeit' 
  // kann positiv oder negativ sein (siehe: * -1)
  xpos = xpos + geschwindigkeit;

  // Zeichnen des Kreises an die aktuelle Position
  ellipse (xpos, height / 2, durchmesser, durchmesser);
}
[/code]

Momentan wird die änderung der Richtung mit zwei //if//-Bedingungen kontrolliert. Innerhalb dieser Bedingungen tauschen wir das Vorzeichen unsers Wertes. Eine kompaktere Version ist die Kombination beider Bedingungen innerhalb einer //if//-Abfrage mit dem logischen || (ODER) Ausdruck. Im Block multiplizieren wir ''geschwindigkeit'' mit -1 und kehren dabei das Vorzeichen um - ohne den absoluten Wert zu modifizieren.

[code|processing]
if (xpos > width - durchmesser || xpos < durchmesser / 2) {
  geschwindigkeit = geschwindigkeit * -1;
}
[/code]

====== Bsp.: lineare Bewegung, frei ======

{{ /files/documents/b08_03_linear31.png}}
In Beispiel drei werden alle Elemente, welche die zur Animation der Kugel auf der //x//-Achse geführt haben, ebenfalls auf die //y//-Achse angewendet. D.h. wir benötigen eine weitere Variable ''yPos'' zur Ablage der Position und eine Variable ''yGeschwindigkeit'' um die Positionsänderung zu beschreiben. Weiterhin testen wir auf die Ober- und Unterseite des Sketchfensters.\\ 
Das Resultat ist ein sich frei bewegender Kreis der von allen Seiten reflektiert wird.

[code|processing]
// gloable Variable für 
// die Ablage der Position
float xpos;
float ypos;
// Positionsänderung pro Einzelbild
float xGeschwindigkeit = 2;
float yGeschwindigkeit = 2;
// Kreisdurchmesser
float durchmesser = 30;

void setup () {
  // Größe des Sketches definieren
  size(320, 240);
  // aktiviere Kantenglättung
  smooth ();
  // Startposition
  xpos = width / 2;
  ypos = height / 2;
}

void draw () {
  // Hintergrund leeren
  background (45);

  // rechter Fensterrand
  if (xpos > width - durchmesser / 2) {
    xGeschwindigkeit = xGeschwindigkeit * -1;
  }
  // linker Fensterrand
  if (xpos < durchmesser / 2) {
    xGeschwindigkeit = xGeschwindigkeit * -1;
  }
  // unterer Fensterrand
  if (ypos > height - durchmesser / 2) {
    yGeschwindigkeit = yGeschwindigkeit * -1;
  }
  // oberer Fensterrand
  if (ypos < durchmesser / 2) {
    yGeschwindigkeit = yGeschwindigkeit * -1;
  }
  
  // Position modifizieren, 'geschwindigkeit' 
  // kann positiv oder negativ sein (siehe: * -1)
  xpos = xpos + xGeschwindigkeit;
  ypos = ypos + yGeschwindigkeit;

  // Zeichnen des Kreises an die aktuelle Position
  ellipse (xpos, ypos, durchmesser, durchmesser);
}
[/code]

==== Non-lineare Animation ====

Im alltäglichen Leben treffen wir selten auf Bewegungsabläufe linearer Art. Im Normalfall haben wir es permanent mit beschleunigten bzw. gebremsten Abläufen zu tun. In diesem Gebiet findet eine positive oder negative Steigerung der Zustandänderungen statt - man bezeichnet dies auch als Beschleunigung.\\ 
Jegliches mobiles Gefährt steigert seine Geschwindigkeit aus der Ruhephase und fällt wiederum nicht sofort wieder in den Stillstand zurück. In dem folgenden Abschnitt beschäftigen wir uns mit der Simulierung dieser Prozesse und versuchen Lösungen für diese Art von profanen Vorgängen zu finden.

====== Bsp.: non-lineare Animation, zufällig ======

Um die Schrittweite innerhalb der Animation zu variieren bedienen wir uns im folgenden Beispiel des bekannten [[lesson:13#random|random()]]-Befehls. Das Resultat summiert auf die aktuelle Position verschiebt den Kreis von Bild zu Bild um unterschiedliche Distanzen.\\ 
Ausgeführt erhalten wir eine stockende Animation. Dies liegt nicht an der Geschwindigkeit unseres Computers, sondern an dem durch random() generierten Chaos in der Berechnung von ''xpos''. Es ist kann dazu kommen, dass die Position in Bild 14 sieben Pixel erhöht wurde, und in Bild 15 um zwei vermindert. Unsere Wahrnehmug erkennt darin keine wiederkehrende Merkmale (homogene Tendenz) - außer das sich der [[lesson:9#ellipse|Kreis]] scheinbar nach rechts bewegt. (Kommentare wurden zu übersichtlichkeit entfernt, siehe: lineare Bewegung - eine Richtung).

[code|processing]
float xpos = 0;
float durchmesser = 30;

void setup () {
  size(320, 240);
  smooth ();
}

void draw () {
  background (45);
  
  // addiere zufällige Schrittweite
  // auf die aktuelle Position, 
  // vorwiegend in positiv
  xpos = xpos + random (-3, 7);
  
  // Zurücksetzen der Kreisposition
  if (xpos > width + durchmesser) {
    xpos = -durchmesser;
  }
  
  // Zeichnen des Kreises an die aktuelle Position
  ellipse (xpos, height / 2, durchmesser, durchmesser);
}
[/code]

====== Bsp.: non-lineare Animation, gleichförmig ======

{{ /files/documents/b08_04_nonlinear1.png}}
Für den nächsten Schritt bedarf es einer weiteren Variable. In ihr legen wir die Zielposition unseres [[lesson:9#ellipse|Kreises]] ab und berechnen in jedem [[lesson:10#vorbereitung_fortlaufende_programme|draw()]]-Durchlauf die momentane Distanz zwischen beiden Punkten. Im Schritt der Positionsaktualisierung addieren wir keinen fixen oder zufälligen Wert, sondern immer ein 60tel des verbleibenden Weges. Demnach beginnt die Animation mit einer großen Schrittweite und schwacht mit dem Näherkommen ab. Da wir jedoch nie unsere Zielposition erreichen werden, muß das Ziel weiter entfernt sein als in der //if//-Bedingung zum Neustarten abgefragt.

[code|processing]
float xpos;
float ziel;
float durchmesser = 30;

void setup () {
  size(320, 240);
  smooth ();
  
  xpos = 0;
  // Zielposition muss größer sein 
  // als der in der 'if'-Abfrage 
  // getestete Wert, sonst Programmstopp 
  ziel = width + durchmesser * 2;
}

void draw () {
  background (45);
  
  // momentaner Abstand zwischen 
  // aktueller- und Zielposition
  float distanz = ziel - xpos;
  
  // addiere ein 60'tel der Distanz 
  // auf die aktuelle Position
  xpos = xpos + distanz / 60;
  
  // Zurücksetzen der Kreisposition
  if (xpos > width + durchmesser) {
    xpos = -durchmesser;
  }
  
  // Zeichnen des Kreises an die aktuelle Position
  ellipse (xpos, height / 2, durchmesser, durchmesser);
}
[/code]

====== Bsp.: non-lineare, gleichförmige Animation + Mausklick ======

In diesem Beispiel entfallen alle Bedingungen zur Positionskontrolle des [[lesson:9#ellipse|Kreises]]. Er kann sich nicht aus dem Sketchfensterbewegen - die Position wird immer mit dem Klicken durch die [[lesson:37#mausinteraktion|Maus]] definiert. Der Kreis folgt also unseren Anweisungen.

[code|processing]
// aktuelle Position
float xpos;
float ypos;
// aktuelles Ziel
float xZiel;
float yZiel;
float durchmesser = 30;

void setup () {
  size(320, 240);
  smooth ();
  
  // Startposition
  xpos = 0;
  ypos = 0;
  // erstes Ziel
  xZiel = width / 2;
  yZiel = height / 2;
}

void draw () {
  background (45);
  
  // Abstände zwischen 
  // aktueller- und Zielposition
  float xd = xZiel - xpos;
  float yd = yZiel - ypos;
  
  // addiere ein 20'tel der Distanz 
  // auf die aktuelle Position
  xpos = xpos + xd / 20;
  ypos = ypos + yd / 20;
  
  // Zeichnen des Kreises an die aktuelle Position
  ellipse (xpos, ypos, durchmesser, durchmesser);
}

// Wenn die Maus gedrückt wurde
void mousePressed () {
  // setze neue Zielposition
  xZiel = mouseX;
  yZiel = mouseY;
}
[/code]

====== Bsp.: non-lineare Animation, trigonometrische Basis ======

{{ /files/documents/b08_05_nonlinear2.png}}
Es existieren bereits einige mathematische Grundlagen um gleichförmige Animationsabläufe zu simulieren. Zwei pragmatische sind die aus dem Matheunterricht bekannten [[http://de.wikipedia.org/wiki/Sinus_und_Kosinus|Sinus & Kosinus]], zur Winkel- und Kreisberechnung.

  * **cos()** Kosinuswert für einen gegeben Winkel [[processing-reference:cos()]]
  * **sin()** Sinuswert für einen gegebenen Winkel [[processing-reference:sin()]]

Im Bereich von zwei [[http://de.wikipedia.org/wiki/Kreiszahl|PI]] (Kreiszahl) bewegt sich die Kurve einmal durch den kompletten Bereich von 0 zu 1 und wieder zurück. Diesen Wert sehen wir als relative Position auf unserer //x-Achse// - multiplizieren ihn demnach mit der Breite unserer Sketches. Der Kurvenverlauf der Sinuskurve auf der //y-Achse// spiegelt folglich die Position des Kreises wieder.\\ 
Führen wir die folgenden Zeilen aus, ähnelt das Resultat der Draufsicht eines Pendels. An der linken und rechten Fensterseite kommt es zu einem Abbremsen - in der Mitte besitzt der Kreis seine maximale Geschwindigkeit.
Die Variable ''pos'' wird zur Steuerung der Bewegung genutzt. Sie beinhaltet einen Wert zwische 0 und zwei [[http://de.wikipedia.org/wiki/Kreiszahl|PI]], ein vollständiger Kurvendurchlauf. Momentan addieren wir in jedem [[lesson:10#vorbereitung_fortlaufende_programme|draw()]]-Durchlauf 0.1 auf ''pos''. Je größer der Summand, so schneller der Ablauf der Animation.

[code|processing]
// dient zur Ablages des Animationsfortgangs 
// (beinhaltet aber nicht die exakte Position)
float pos = 0;

void setup () {
  size(320, 240);
  smooth ();
}

void draw () {
  background (45);
  
  // setze 'pos' auf 0 zurück wenn die 
  // Sinuskurve einmal durchlaufen ist
  if (pos > PI * 2) {
    pos = 0;
  }
  
  // erhöhe 'pos' pro Bild um 0.1 'pos' 
  // bewegt sich immer zwischen 0 und 2*PI
  pos = pos + 0.1;
 
  // Pendelzentrum, zwischen positivem und 
  // negativem Kurvenabschnitt
  float xZentrum    = width / 2;
  // momentaner Ausschlag des Pendels
  float xAmplitude  = width / 2 * sin (pos);
  // Summe ist die momentane Position
  float xpos        = xZentrum + xAmplitude;
  
  ellipse (xpos, height / 2, 30, 30);
}
[/code]

==== Kreisbewegung ====

Diese Art der Bewegung findet auf einem imaginären Kreis statt. Auf der Grundlage der Position, des Radius und der Winkelangabe kann die Koordinate auf der Kreisbahn bestimmt werden. Processing bietet die [[http://de.wikipedia.org/wiki/Trigonometrische_Funktion|trigonometrischen Funktionen]] [[processing-reference:sin()]] & [[processing-reference:cos()]] an, welche für gegebenen Winkel und Radius den Abstand zum Zentrum des Kreises berechnen lassen.

  * **cos()** gibt den Kosinuswert zwischen -1 und 1 für ein gegebenes [[http://de.wikipedia.org/wiki/Bogenmaß|Bogenmaß]] zurück. [[processing-reference:cos()]] [code|processing]
println (cos (PI / 3));  // 0.49999997
println (cos (PI));  // -1.0
[/code]
  * **sin()** gibt den Sinuswert zwischen -1 und 1 für ein gegebenes [[http://de.wikipedia.org/wiki/Bogenmaß|Bogenmaß]] zurück. [[processing-reference:sin()]] [code|processing]
println (sin (PI / 3));  // 0.86602545
[/code]

[[example:16]]

[[example:17]]

[[example:18]]

[[example:19]]

[[example:20]]