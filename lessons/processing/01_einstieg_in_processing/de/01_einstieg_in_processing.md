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
Die Größe der Zeichenfläche lässt sich mit dem Aufruf des Befehls size() festlegen. Processing passt die Ausgabefläche anderenfalls auf 100x100 Pixel an. Damit diese Einstellung funktioniert, braucht das Programm zwei Informationen von uns. Wie breit und wie hoch die gewünschte Zeichenfläche sein soll. Bei Positionen und Größen im 2d-Raum wird immer erst der Wert auf der *x*-Achse und danach der *y* Wert genannt (demnach erst die Breite, dann die Höhe). Beide Werte kommen als Parameter zwischen die beiden runden Klammern, die dem Begriff ''size'' folgen.
  * **size(width, height)** legt die Größe der sichtbaren Zeichenfläche (im Sketchfenster) fest. Das unten aufgeführte Beispiel legt einen Bereich von 800x600 Pixeln im Ausgabefenster an. [[processing-reference:size()]]```processing
size (800, 600);
```

### Visuelle Grundelemente
#### Punkt
{{ /files/documents/b01_point.jpg}}
Ein Punkt ist das simpelste Element der primitiven Grundformen. Nur mit einer *x* und einer *y*-Koordinate nimmt er, ohne spezielle Angaben, die Fläche eines Pixels auf dem Bildschirm ein. Die für die Füllung verwendete Farbe kann mit //[[lesson:9#flaechen_fuellen_raender_einfaerben|stroke()]]// festgelegt werden.
  * **point(x, y)** zeichnet einen Punkt auf die Zeichenfläche. Bestimmt wird dieser durch ''*x*'' & ''*y*''-Koordinate. [[processing-reference:point()]] ```processing
point (0, 0);   //obere-linke Ecke
point (43, 89); 
```

#### Linie
{{ /files/documents/b01_line.jpg}}
Als zweites Element lernen wir die Linie kennen. Als eine Reihe von Punkten erstreckt sie sich zwischen einem Anfangs- und einem Endpunkt. Um eine Linie zu zeichnen verwendet man den line() Befehl. Dieser hat genau vier Parameter, zwei Werte für den Anfangs- und zwei für den Endpunkt.
  * **line(x1, y1, x2, y2)** zeichnet eine Linie zwischen zwei Punkten. Punkt1 und Punkt2 werden jeweils durch eine *x* & *y*-Koordinate angegeben. [[processing-reference:line()]] ```processing
line (10, 20, 80, 60);
```

#### Rechteck
{{ /files/documents/b01_rect.jpg}}
Der Befehl rect() ermöglicht das Fällen bzw. Umranden einer rechteckigen Fläche. Bestimmt durch den oberen-linken Punkt dehnt dich diese nach rechts-unten aus. Dafür benötigt Processing neben der *x* und *y*-Koordinate zur Punktbestimmung die Breite und Höhe des Elements.
  * **rect(x, y, width, height)** zeichnet ein Rechteck mit einer definierten Breite und Höhe an eine bestimmte Position auf die Zeichenfläche des Sketchfensters. [[processing-reference:rect()]] ```processing
rect (20, 20, 60, 40);
```

Alle Außenkante des Vierecks bleiben beim Aufruf von rect() immer parallel zur *x* bzw. *y*-Achse. Um dies zu umgehen kann für das freie Zeichnen von viereckigen Flächen der [[lesson:9#viereck|quad()]] Befehl verwendet werden.

#### Ellipse
{{ /files/documents/b01_ellipse.jpg}}
  * **ellipse(x, y, width, height)** zeichnet eine Ellipse/Kreis in die Zeichenfläche. Grundsätzlich befindet sich der mit ''x'' und ''y'' angegebene Punkt im Zentrum der Ellipse. Die beiden weiteren Werte geben die Breite (''width'') auf der *x*-Achse und Höhe (''height'') auf der *y*-Achse des Elements an. Bei den Größenangaben handelt es sich demnach um den Durchmesser auf der jeweiligen Achse, nicht um den Radius. [[processing-reference:ellipse()]] ```processing
ellipse (50, 50, 45, 55);
```

#### Viereck
{{ /files/documents/b01_quad.jpg}}
Neben rect() erlaubt die erweiterte Möglichkeit quad() ebenfalls das Darstellen von Vierecken. Mittels vier ausformulierten Punkten können Formen gezeichnet werden, die keine Innenwinkel von 90° besitzen und parallele Seitenpaare haben.
  * **quad(x1, y1, x2, y2, x3, y3, x4, y4)** zeichnet ein Viereck in Zeichenfläche. Bestimmt durch 4 Punkte, jeweils eine *x* und *y* Koordinate, beschreiben die Lage der Fläche. [[processing-reference:quad()]]```processing
quad (12, 19, 31, 85, 67, 74, 80, 19);
```

### Graustufen
{{ /files/documents/b01_grey.jpg}}
Im [[http://de.wikipedia.org/wiki/RGB-Farbraum|RGB Farbraum]] mischen sich Graustufen aus gleichen Anteilen der drei Kanäle Rot, Grün und Blau. Durch die [additive](http://de.wikipedia.org/wiki/Additive_Farbsynthese) Zusammensetzung erhält man bei drei vollen Teilen die Farbe weiß, bei keinen Angaben für R,G,B schwarz. Processing bietet für diesen Fall eine Kurzschreibweise für die Festlegung von Füll- und Strichfarben. Statt drei gleicher Werte wird nur eine Wert zwischen den runden Klammern genannt. Die Zeile fill(38, 38, 38); hat die gleiche Aufgabe wie fill(38);.

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

Aufrufe von fill() und stroke() lassen sich wie folgt lesen:
  * **1 Wert** Grauton, deckend
  * **2 Werte** Grauton, mit Transparenzangabe
  * **3 Werte** RGB Farbtonangabe, deckend
  * **4 Werte** RGB Farbtonangabe, mit Transparenzangabe

### Farben
{{ /files/documents/b01_rgb_system.jpg}}
Standardmäßig arbeitet Processing mit dem [RGBA-Farbraum](http://de.wikipedia.org/wiki/RGB-Farbraum#RGBA-Farbmodell) (Rot, Grün, Blau, Alpha). Für jeden der sogenannten Kanäle steht ein Wertebereich von 256 Einheiten, beginnend bei 0, zur Verfügung um das Mischverhältnis zu bestimmen [additive Farbmischung](http://de.wikipedia.org/wiki/Additive_Farbsynthese). Ein Anteil von 0 bedeutet, daß kein Teil dieses Kanals in die Farbmischung eingeht - mit 255 der komplette Kanal.\\ 
Drei Befehlen bietet Processing um Farben für unterschiedliche Eigenschaften/Bereiche festzulegen: background() für das einfärben der gesamten Zeichenfläche, fill() für die Füllfarbe und stroke() für die Umrandung von visuellen Elemente.

#### Hintergrund einfärben
Processing färbt ohne unser Zutun den Hintergrund des Sketchfensters grau ein. Wenn wir die Fläche leeren wollten, sie mit einem Farbton füllen, müssten wir ein Rechteck im Fensterformat zeichnen. Diese Funktionalität bietet uns ebenfalls der Befehl background(). Ausgestattet mit Informationen über die Anteiligkeit der Farbkanäle überschreibt er den momentanen Inhalt der Zeichfläche (ohne das wie bei rect() Position oder Größe angegeben werden muss).
  * **background(r, g, b)** löscht den Inhalt der Zeichenfläche durch homogenes Füllen mit einer Farbe. Diese wird durch die drei Kanäle ''r'' Rot, ''g'' Grün und ''b'' Blau bestimmt. [[processing-reference:background()]]```processing
background (231, 0, 89);
```

#### Flächen füllen & Ränder einfärbenUm Flächen/Einschlüsse farblich zu füllen kann man dem grafischen Element keine konkreten Informationen mit auf den Weg geben. Innerhalb von Processing existiert für Füll- und Strichfarbe jeweils ein Farbeimer, bildlich gesprochen. Der Inhalt dieser beiden Eimer kann mit zwei Funktionen bestimmt werden: fill() für die Füllfarbe und stroke() für die Farbgebung der Umrandung. Wenn keine Farbe angewendet werden soll kommen noFill() und noStroke() ins Spiel. Diese Einstellungen bleiben solange aktiv, bis sie durch einen Aufruf von fill() bzw. noFill() für die Füllfarbe und stroke() bzw. noStroke() für die Umrandung geändert werden.
  * **fill(r, g, b)** setzt die Füllfarbe für alle im Anschluss gezeichneten Elemente. Die drei Werte stehen jeweils für einen Farbkanal: ''r'' Rot, ''g'' Grün und ''b'' Blau. Optional kann durch einen vierten Wert ''a'' die Transparenz bestimmt werden. Der Wertebereich liegt für alle vier Angaben zwischen 0 und 255. [[processing-reference:fill()]]```processing
fill (255, 0, 0); //volles Rot
fill (0, 255, 0); //volles Grün
fill (0, 0, 255); //volles Blau
```
  * **noFill()** deaktiviert die Füllfarbe für alle im Anschluss gezeichneten Elemente. [[processing-reference:noFill()]]```processing
noFill ();
```
  * **stroke(r, g, b)** setzt die Farbe für alle im Anschluss gezeichneten Elemente. Die drei Werte stehen jeweils für einen Farbkanal: ''r'' Rot, ''g'' Grün und ''b'' Blau. Optional kann durch einen vierten Wert ''a'' die Transparenz bestimmt werden. Der Wertebereich liegt für alle vier Angaben zwischen 0 und 255. [[processing-reference:stroke()]] ```processing
stroke (255, 0, 0); //volles Rot
stroke (0, 255, 0); //volles Grün
stroke (0, 0, 255); //volles Blau
```
  * **noStroke()** deaktiviert die Umrandungsfarbe für alle im Folgenden gezeichneten Elemente. [[processing-reference:noStroke()]]```processing
noStroke ();
```