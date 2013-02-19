# Einstieg in Processing
## Geschichte, Kontext und die ersten Zeilen Code

> Diese Lesson führt Processing als Programmiersprache und Umgebung ein. Nach einem kurzen Überblick über die Enstehung und Wurzeln des Projekts am MIT Media Lab wird die Processing Software mit ihren grundlegenden Funktionen vorgestellt. Danach folgt der unmittelbare Einstieg in die Programmierumgebung, indem das Koordinatensystem, die visuellen Grundelemente und die Verwendung von Farben eingeführt werden.

---

In dieser Lesson dreht sich alles um das Gestalten von generativen und interaktiven Systemen mittels der Open-Source Umgebung [Processing](http://www.processing.org). Sie ermöglicht Interessierten ohne Programmiererhintergrund einen schnellen und einfachen Einstieg in das kreative Arbeiten mit Code. Ohne aufwendige Vorbereitung erlaubt Processing das Zeichnen von grafischen Elementen, die Manipulation von digitalen Bildern oder die Verwendung von Mouse und Tastatur in eigenen Programmen sowie vielem mehr.

Das Projekt wurde von [Ben Fry](http://www.benfry.com) und [Casey Reas](http://www.reas.com) 2001 am [MIT](http://media.mit.edu) ins Leben gerufen. Inspiriert von [John Maeda’s](http://www..com) 1999 entstandenem Projekt [Design by Numbers](http://www..com) sollte es als Werkzeug für Designer und Künstler dienen, das einen flexibleren Umgang mit Software und Technologie ermöglicht. Schnell wurde die Umgebung von vielen Künstlern nicht nur im Entwurfsprozess, sondern auch für Installationen und Ausstellungen genutzt.

Processing basiert auf der Programmiersprache [Java](https://de.wikipedia.org/wiki/Java_(Programmiersprache)), vereinfacht deren Schreibweise und minimiert so den Schreibaufwand beim Programmieren beachtlich. Es handelt sich streng genommen bei Processing also eher um einen Dialekt von Java, als um eine eigenständige Programmiersprache. Der Vorteil dieses Umstands liegt dabei auf der Hand. Möchte (oder muss) man später einmal über den Tellerrand von Processing hinausschauen, so fällt der Einstieg in Java sehr leicht. Auch das spätere Erlernen von Java-ähnlichen Programmiersprachen wie [ActionScript](https://de.wikipedia.org/wiki/ActionScript) oder [JavaScript](https://de.wikipedia.org/wiki/Javascript) fällt durch Processing leichter. In den letzten Jahren hat sich Processing zusätzlich von der Java-Platform auch auf andere Umgebungen ausgebreitet. Der bekannteste Vertreter dieser Entwicklung ist [ProcessingJS](http://processingjs.org), das in Processing seit den neuesten Versionen automatisch unterstützt wird. ProcessingJS basiert auf JavaScript und lässt sich dadurch sehr leicht in umfangreiche Webseiten integrieren.

Der Schlüssel für das Verständnis von Programmierung liegt im Erlernen der Forumulierung von Programmanweisungen – der sogenannten Syntax – und der logischen Strukturierung von Programmabläufen, also dem Gestalten von [Algorithmen](https://de.wikipedia.org/wiki/Algorithmus). Viele aktuellen Programmiersprachen ähneln sich in diesen Punkten stark und können deshalb mit Grundkenntnissen in Processing leicht erlernt werden. Deshalb - und natürlich wegen der starken visuellen Ausrichtung – ist Processing unser Werkzeug der Wahl, wenn es um die Einführung in die Programmierung für Künstler und Designer geht.

### Das Programm
Processing besteht aus zwei Teilen: Der eigentlichen Programmiersprache, sowie der Anwendung die die Verwendung dieser so einfach wie möglich machen möchte.

Die Processing Anwendung ist im Grunde ein Texteditor mit kleinen Zusatzfunktionen die grundlegende, programmierspezifische Aufgaben erfüllen. Im Vergleich zu [Entwicklungsumgebungen](https://de.wikipedia.org/wiki/Integrierte_Entwicklungsumgebung) wie [Eclipse](http://www.eclipse.org) oder [Netbeans](http://www..com) bedarf es keiner aufwendigen Projekteinrichtung und Konfiguration bevor die ersten Schritte gemacht werden können. Kostenlos verfügbar für Mac, Linux und Windows kann es im [Downloadbereich](http://www.progcessing.org/download) der Processingseite heruntergeladen werden. Vorraussetzungen sind eine aktuelle Java- und QuickTime-Version, die jedoch häufig bereits installiert sind oder im Download dabei sind. Teilweise benötigen Plugins (sog. [Libraries](http://www.processing.org/learning/libraries)) systemspezifische Zusatzdateien, die jedoch fast immer mitgeliefert werden.

*An dieser Stelle möchten wir gern darauf hinweisen, dass Processing momentan grundlegend weiterentwickelt und verändert wird. Die momentane Version wird zwar als **Beta** bezeichnet – eine Äquivalent zu ‘Testen’ in der Software Entwicklung – wir betrachten diese Version jedoch als stabil genug um sie mit allen Lessons auf Creative Coding benutzen zu können.*

Der Großteil des Programmfensters wird durch den Texteditor eingenommen. Alle Bestandteile der hier geschriebenen Anweisungen werden zu besseren Lesbarkeit eingefärbt. Über dem Editor befindet sich die Menüleiste mit den gewohnten Optionen wie ‘Öffnen’ oder ‘Speichern’, bis hin zu Plugin-Verwaltung und Ausgabe des geschriebenen Programms. Programme werden in Processing ‘Sketches’ genannt und dadurch wird der Fokus auf das skizzenhafte Entwickeln eines Programms bereits deutlich. Einige der essentiellen Funktionen, z.B. das Ausführen des Programms, sind zwischen Menüleiste und Texteditor als Icons angesiedelt. Beim Starten des Sketches springt ein zweites Fenster auf in dem das laufende Programm abgebildet wird. Alternativ kann das Programmauch mit der Tastenkombination Cmd (Ctrl) + r ausgeführt werden. Im späteren Verlauf kann es dazu kommen, dass ein Programm aus mehreren Textdokumenten besteht. Direkt über dem Texteditor befindet sich zu diesem Zweck eine Tab-Leiste um diese aufzulisten.

### Zeichenfläche
Als Basis zum Zeichnen in Processing ist das Sketchfenster in ein [kartesisches Koordinatensystem](http://de.wikipedia.org/wiki/Kartesisches_Koordinatensystem) unterteilt. Die *x*-Achse befindet sich horizontal am oberen Fensterrand, die *y*-Achse vertikal am linken Fensterran. In der **oberen, linken Ecke** befindet sich der **Koordinatenursprung** mit den (x,y)-Werten **(0,0)**. Von dort aus breitet sich das Koordinatensystem auf der *x*-Achse nach *rechts* und auf der *y*-Achse nach *unten* aus. Positions- und Größenangaben werden in der Einheit ’Pixel‘ (ein Bildschirmpunkt) vorgenommen - demnach ist der *x-Wert* für den Punkt in der oberen-rechten Ecke gleich der Breite des Fensters in Pixel. Beide Achsen dehnen sich ebenfalls in den negativen Wertebereich nach *links* bzw. *oben* aus. So würde sich bspw. der Punkt mit den (x,y)-Werten (-10, -10) jeweils 10 Pixel ausserhalb der Zeichenfläche in der linken, oberen Ecke befinden. Auch diese Koordinaten können beim Positionieren also angegeben werden, und man sollte immer bedenken, das gezeichnete Objekte aus der sichtbaren Fläche ‘herausrutschen’ können und somit nicht dargestellt werden.

Neben dem zweidimensionalem Raum können unter Hinzunahme der *z*-Achse **dreidimensionale** Abbildungen erzeugt werden. Die dritte Achse verläuft ebenfalls durch die **obere, linke** Ecke, jedoch *orthogonal* (in einem rechten Winkel) zum Bildschrim. Positive Werte auf der *z*-Achse befinden vor dem Bildschirm, negative Werte dahinter. In den folgenden Lessons konzentrieren wir uns jedoch auf das Gestalten mit Code in 2D.

#### Größe des Sketchfensters
Die Größe der Zeichenfläche lässt sich mit dem Aufruf des Befehls `size()` festlegen. Falls die Sketch diesen Befehl nicht beinhaltet, passt Processing die Ausgabefläche selbstständig auf 100x100 Pixel an. Damit diese Einstellung funktioniert, braucht das Programm zwei Informationen von uns: wie breit und wie hoch die gewünschte Zeichenfläche sein soll. Bei Positionen und Größen im 2d-Raum wird immer erst der Wert auf der *x*-Achse und danach der *y* Wert genannt (demnach erst die Breite, dann die Höhe). Beide Werte können als *Parameter* zwischen die beiden runden Klammern geschrieben werden, die dem Begriff `‘size’` folgen.

*	**`size(width, height)`** legt die Größe der sichtbaren Zeichenfläche (im Sketchfenster) fest. Das unten aufgeführte Beispiel setzt die Größe des Sketchfensters auf 800x600 Pixel:
```processing
size (800, 600);
```

### Visuelle Grundelemente
#### Punkt
![Punkt](/files/documents/b01_point.jpg "Punkt")
Der Punkt ist das einfachste Element der primitiven Grundformen. Nur mit einer *x* und einer *y*-Koordinate nimmt er, ohne spezielle Angaben, die Fläche eines Pixels auf dem Bildschirm ein. Die für die Füllung verwendete Farbe kann mit dem [`stroke()`](lesson9#flaechen_fuellen_raender_einfaerben)-Befehl festgelegt werden.

*	**`point(x, y)`** zeichnet einen Punkt auf die Zeichenfläche. Bestimmt wird dieser durch die *x* & *y*-Koordinate.
```processing
point (0, 0);   // obere, linke Ecke
point (43, 89); // x = 43 & y = 89
```

#### Linie
![Linie](/files/documents/b01_line.jpg "Linie")
Als zweites Element lernen wir die Linie kennen. Sie verbindet einen Anfangs- und einem Endpunkt. Um eine Linie zu zeichnen verwendet man den `line()` Befehl. Dieser hat genau vier Parameter, die *x* und die *y*-Koordinate für den Anfangs- und für den Endpunkt.

*	**`line(x1, y1, x2, y2)`** zeichnet eine Linie zwischen zwei Punkten. Punkt1 und Punkt2 werden jeweils durch eine *x* & *y*-Koordinate angegeben.
```processing
line (10, 20, 80, 60);
```

#### Rechteck
![Rechteck](/files/documents/b01_rect.jpg "Rechteck")
Der Befehl `rect()` (vom engl. *rectangle* für *Rechteck*) ermöglicht das Zeichnen einer rechteckigen Fläche. Die Position orientiert sich am oberen, linken Punkt. Die Größe an der Ausdehnung nach rechts und unten von diesem. Processing benötigt also neben der *x* und *y*-Koordinate zur Positionsbestimmung auch noch die Breite und Höhe des Rechtecks.

*	**`rect(x, y, width, height)`** zeichnet ein Rechteck mit einer definierten Breite (*width*) und Höhe (*height*) an die Position (*x*,*y*) auf die Zeichenfläche der Sketch.
```processing
rect (20, 20, 60, 40);
```

Für das Zeichnen von Vierecken, bei denen die Innenwinkel nicht auf 90° beschränkt sind, steht ausserdem der [`quad()`](lesson1#viereck)-Befehl zur Verfügung.

#### Ellipse
![Ellipse](/files/documents/b01_ellipse.jpg "Ellipse")
Der Befehl `ellipse()` ermöglicht das Zeichnen einer Ellipse/eines Kreises in die Zeichenfläche. Grundsätzlich befindet sich der mittels *x* und *y*-Koordinaten angegebene Punkt im Zentrum der Ellipse. Das zweite Wertepaar gibt, wie beim `rect()` Befehl, die Breite und Höhe der Ellipse an. Sind beide Werte hier gleich, erhalten wir einen Kreis. Durch die Breiten- und Höhenangaben handelt es sich also hierbei um die *Durchmesser* und nicht die Radien der gezeichneten Ellipsen und Kreise!

* **`ellipse(x, y, width, height)`** zeichnet eine Ellipse mit einer definierten Breite (*width*) und Höhe (*height*) an die Position (*x*,*y*) auf die Zeichenfläche der Sketch.
```processing
ellipse (50, 50, 45, 55);
```

#### Viereck
![Viereck](/files/documents/b01_quad.jpg "Viereck")
Der `quad()` Befehl erlaubt das Zeichnen von beliebigen Vierecken, also auch von [Parallelogrammen](https://de.wikipedia.org/wiki/Parallelogramm), [Trapezen](https://de.wikipedia.org/wiki/Trapez_(Geometrie)) und unregelmäßigen Vierecken. Diese Formen können durch die Angabe von vier Eckpunkten gezeichnet werden:

* **`quad(x1, y1, x2, y2, x3, y3, x4, y4)`** zeichnet ein Viereck auf die Zeichenfläche der Sketch. Bestimmt durch 4 Punkte, jeweils eine *x* und *y*-Koordinate, beschreiben die Lage der Fläche.
```processing
quad (12, 19, 31, 85, 67, 74, 80, 19);
```

### Graustufen
![Graustufen](/files/documents/b01_grey.jpg "Graustufen")
Im [RGB Farbraum](http://de.wikipedia.org/wiki/RGB-Farbraum) mischen sich Graustufen aus gleichen Anteilen der drei Kanäle *R*ot, *G*rün und *B*lau. Der Anteil jedes Farbkanals wird dabei durch eine Zahl von 0 und 255 angegeben. Durch die [additive](http://de.wikipedia.org/wiki/Additive_Farbsynthese) Zusammensetzung erhält man somit bei drei vollen Teilen die Farbe weiß, bei keinen Angaben für R,G,B schwarz. Processing bietet für diesen Fall eine Kurzschreibweise für die Festlegung von Füll- und Strichfarben. Statt drei gleicher Werte wird nur ein Wert zwischen den runden Klammern angegeben. Die Zeile `fill(38, 38, 38);` führt also zum gleichen Ergebnis wie `fill(38);`.

```processing
background (110);  // grau
fill (0);          // schwarz
stroke (255);      // weiß
```

Neben dem Grauwert kann als zweiter Wert die Transparenz für den Grauton angageben werden, ebenfalls von 0 bis 255.

```processing
background (110);  // grau
fill (0, 90);      // schwarz, transparent
stroke (255, 200); // weiß, transparent
```

Aufrufe von `fill()` und `stroke()` lassen sich wiefolgt lesen:

* **1 Wert** Grauton, deckend
* **2 Werte** Grauton, mit Transparenzangabe
* **3 Werte** RGB Farbtonangabe, deckend
* **4 Werte** RGB Farbtonangabe, mit Transparenzangabe

### Farben
![RGB Farbsystem](/files/documents/b01_rgb_system.jpg "RGB Farbsystem")
Standardmäßig arbeitet Processing mit dem [RGBA-Farbraum](http://de.wikipedia.org/wiki/RGB-Farbraum#RGBA-Farbmodell) (*R*ot, *G*rün, *B*lau, *A*lpha). Für jeden der sogenannten Farbkanäle steht ein Wertebereich von 256 Einheiten (beginnend bei ‘0’) zur Verfügung um ihr Mischverhältnis zu bestimmen. Diese Farbmischverfahren wird als [additive Farbmischung](http://de.wikipedia.org/wiki/Additive_Farbsynthese) bezeichnet. Ein Anteil von 0 bedeutet, dass kein Teil dieses Kanals in die Farbmischung eingeht, ein Anteil von 255 steht für den kompletten Kanal.

Drei Befehle bietet Processing um Farben für unterschiedliche Eigenschaften/Bereiche festzulegen: `background()` für das einfärben der gesamten Zeichenfläche, `fill()` für die Füllfarbe und `stroke()` für die Umrandung von visuellen Elementen.

#### Hintergrund einfärben
Processing färbt ohne unser Zutun den Hintergrund des Sketchfensters grau ein. Wir können den Hintergrund mit einer beliebigen Farbe füllen und somit die Zeichenfläche leeren, bevor wir neue Elemente zeichnen. Diese Funktionalität bietet uns der Befehl `background()`. Ausgestattet mit Informationen über die Anteile der Farbkanäle überschreibt er den momentanen Inhalt der Zeichfläche.

* **`background(r, g, b)`** löscht den Inhalt der Zeichenfläche durch homogenes Füllen mit einer Farbe. Die Farbe wird entweder durch einen Grauton-Wert oder durch drei Kanäle **R**ot, **G**rün und **B**lau bestimmt.
```processing
background(231, 0, 89);
```

#### Flächen füllen & Ränder einfärben
Bisher haben wir keine Möglichkeit kennengelernt beim Zeichnen von grafischen Elementen deren Füll- und Strichfarben zu bestimmen um diese einfärben zu können. Innerhalb von Processing existiert dazu für Füll- und Strichfarbe jeweils ein – bildlich gesprochen – ‘Farbeimer’. Der Inhalt dieser beiden Eimer kann mit zwei Funktionen bestimmt werden: `fill()` für die Füllfarbe und `stroke()` für die Farbgebung der Linien, Umrandungen eingeschlossen. Wenn keine Farbe angewendet werden soll kommen `noFill()` und `noStroke()` ins Spiel. Diese Einstellungen bleiben solange aktiv, bis sie durch einen Aufruf von `fill()` bzw. `noFill()` für die Füllfarbe und `stroke()` bzw. `noStroke()` für die Umrandung geändert werden.

* **`fill(r, g, b)`** setzt die Füllfarbe für alle im Anschluss gezeichneten Elemente. Die Farbe wird durch drei Kanäle **R**ot, **G**rün und **B**lau bestimmt. Optional kann durch einen vierten **A**lpha-Wert die Transparenz bestimmt werden. Der Wertebereich liegt für alle vier Angaben zwischen 0 und 255.
```processing
fill (255, 0, 0); // volles Rot
fill (0, 255, 0); // volles Grün
fill (0, 0, 255); // volles Blau
```
* **`noFill()`** deaktiviert die Füllfarbe für alle im Anschluss gezeichneten Elemente.
```processing
noFill();
```
* **`stroke(r, g, b)`** setzt die Strichfarbe für alle im Anschluss gezeichneten Elemente. Die Farbe wird durch drei Kanäle **R**ot, **G**rün und **B**lau bestimmt. Optional kann durch einen vierten **A**lpha-Wert die Transparenz bestimmt werden. Der Wertebereich liegt für alle vier Angaben zwischen 0 und 255.
```processing
stroke (255, 0, 0); //volles Rot
stroke (0, 255, 0); //volles Grün
stroke (0, 0, 255); //volles Blau
```
* **`noStroke()`** deaktiviert die Strichfarbe für alle im Folgenden gezeichneten Elemente. **ACHTUNG:** Wenn diese Einstellung aktiv ist, werden Punkte und Linien nicht gezeichnet!
```processing
noStroke();
```