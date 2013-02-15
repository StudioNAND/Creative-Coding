# Typografie
## Laden und Darstellen von Text

> Diese Lesson erläutert die Besonderheiten zu Processings Umgang mit Schrift und der Darstellung von Text. Darüber hinaus werden die Grundfunktionen wie Schriftgröße, Zeilenhöhe, Beschränkung des Textfelds, sowie dem Ausrichten und Einfärben von Text eingeführt. 

---

### Schriften in Processing
Innerhalb von Processing wird das Schriftformat vlw verwendet. Anders als bei Vektorschriften liegt dabei jedes Zeichen seperat als gerastertes Bild vor. Diese Bildinformationen beschränken sich pro Pixel auf die Angabe von schwarz (1) oder weiß (0) - wird das Pixel gefüllt oder nicht. Eine solche Schrift nennt man deshalb Bitmap-Font ([[http://de.wikipedia.org/wiki/Bit|Bit]]), da nur zwei Möglichkeiten existieren.
Grund für diese umständliche und qualitativ ungünstige Lösung ist die Funktion des Webexports. Da die Verfügbarkeit der Schriften im Betriebssystem von Betrachtern im Internet keine Vorraussetzung darstellen soll.

#### Laden von Schriften
Das laden von Schriften verhält sich ähnlich wie das Laden von [[lesson:15#pixelbilder_in_processing_verwenden|Bildern]]. Mussten wir bei Bildern, diese vorher manuell in den *data-Ordner* unserer Sketch kopieren (alternativ auch über das Menü "Sketch->Add File...") gibt es bei Schriften noch einen zusätzlichen Schritt vor dem Kopieren: das Erstellen der Bitmap-Font aus der auf dem Rechner installierten Schrift. Diese Aufgabe übernimmt komplett das Tool "Create Font" (im Menü "Tools->Create Font..."). Einmal geöffnet, wählt man die Schrift, die man verwenden möchte aus, woraufhin sie automatisch in den *data-Ordner* kopiert wird. Damit kann sie verwendet werden.

Wie Bilder werden auch Schriften in einem eigenen Datentypen gespeichert:

```processing
PFont myFont;
```
und können nach der Deklaration auch in die neu erstellte Variable geladen werden:
```processing
myFont = loadFont ("Name-of-my-Font.vlw");
```

#### Abbilden im Sketch
Nach dem Erfolgreichen Laden der Font kann diese endlich verwendet werden. Dazu muss Processing zu erst mitgeteilt werden welche Font verwendet werden soll. Das ist insbesondere deswegen nötig, da natürlich auch mehrere Schrift geladen und verwendet werden können.
In Processing wird die zu verwendende Schrift über den Befehl textFont(font, size); definiert. Diese Einstellung gilt dann bis zum erneuten Aufruf von textFont();. Beim festlegen der Schriftgröße sollte darauf geachtet werden, dass die Font vorher in einer bestimmten Größe gerastert (in Bitmap-Schrift umgewandelt) wurde, was dazu führen kann, dass die Pixel der Schrift sichtbar werden, wenn die Darstellungsgröße die Rastergröße übersteigt. Allgemein gilt: Schriften die klein gerastert wurden werden schneller dargestellt.\\ 
Als letzter Schritt ist lediglich die Verwendung von text("mein Text", xpos, ypos); nötig um Text in Processing darzustellen.
Die drei Parameter der text() Funktion bestimmem hierbei den darzustellenden Text als *String*, sowie die *x* und *y*-Position an der der Text dargestellt werden soll. Anders jedoch als bei rect() oder image() liegt der Orientierungspunkt für das Zeichnen von Text in der **linken, unteren Ecke**.

###### Bsp.: Darstellung
{{/files/documents/b07_00_loadfont.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size (500, 140);
// Hintergrund einfärben
background (45);

// Laden der Schrift in 
// die Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");

// Setze die Schrift 'font' als 
// Standardschrift für alle nun 
// folgenden 'text()' Aufrufe
textFont (font);

// Schreibe 'typo' an die Position
// x:40 und y:89
text ("typo!", 40, 89);
```

###### Bsp.: Darstellung im Block
{{/files/documents/b07_01_textblock.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size (500, 240);
// Hintergrund einfärben
background (45);

// Laden der Schrift in die Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");
// Setze die Schrift 'font' als Standardschrift
textFont (font);

// Schreibe 'typo' an die Position x:40 und y:89.
// Nutze dafür eine Fläche von 420x180 Pixel
text ("Zwei Boxkämpfer jagen Eva quer durch Sylt.", 40, 47, 420, 180);
```

#### Schriftgröße
Die Schriftgröße lässt sich auf zwei Wegen definieren:
  * **textFont(font, size)** setzt sowohl die zukünftig zu verwendende Schrift, sowie gleichzeitig die Schriftgröße. [[processing-reference:textFont()]]
  * **textSize(size)** diese Variante ist besser geeignet, wenn nur die Schriftgröße und nicht die Schrift geändert werden soll. [[processing-reference:textSize()]]

###### Bsp.: Schriftgröße
{{/files/documents/b07_02_textsize.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size (500, 140);
// Hintergrund einfärben
background (45);
// Aktiviere Kantenglättung
smooth ();

// Laden der Schrift in die Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");
// Setze die Schrift 'font' als Standardschrift
textFont (font);

// Setze Schriftgröße auf 28px
textSize (28);
// Schreibe 'creative' an x:40 y:67
text ("creative", 40, 67);

// Setze Schriftgröße auf 48px
textSize (48);
// Schreibe 'coding' an x:40 y:110
text ("coding", 40, 110);
```

#### Zeilenhöhe
Für die Darstellung von mehrzeiligem Text ist die Anpassung des Zeilenabstands unabdingbar um eine gute Lesbarkeit zu gewährleisten. Die Zeilenhöhe lässt sich über die Funktion textLeading() einstellen.

```processing
textLeading(distance);
```

###### Bsp.: Zeilenhöhe
{{/files/documents/b07_03_lineheight.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size(500, 180);
// Hintergrund einfärben
background (45);

// Laden der Schrift in ie Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");
// Setze die Schrift 'font' als Standardschrift
textFont (font);

// Setze die Zeilehöhe auf 29px
textLeading (29);

// Schreibe 'typo' an die Position x:40 und y:89.
// Nutze dafür eine Fläche von 420x180 Pixel
text ("Zwei Boxkämpfer jagen Eva quer durch Sylt.", 40, 47, 420, 180);
```

#### Einfärben
Das [[lesson:9#farben|Einfärben]] von Schrift funktioniert in Processing auf die selbe Art und Weise wie das auch bei den [[lesson:9#visuelle_grundelemente|Grundformen]] wie rect() oder ellipse() der Fall ist. Das heisst, ein Aufruf von fill(r, g, b); ändert die Füllfarbe für alle folgenden gezeichneten Texte (und Formen!). Auch die Verwendung von Transparenzen über fill(r, g, b, a); ist möglich.
Die Strichfarbe hingegen lässt sich bei Schriften nicht definieren, was mit dem Umstand zu tun hat, dass Texte in Processing generell Pixelbilder sind.

###### Bsp.: Text einfärben
{{/files/documents/b07_04_text_fill.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size(500, 140);
// Hintergrund einfärben
background (45);

// Laden der Schrift in die Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");
// Setze die Schrift 'font' als Standardschrift
textFont (font);

fill (255, 0, 102);
text ("creative", 40, 67);

fill (255, 20, 20);
text ("coding", 40, 110);
```

#### Ausrichtung
Texte können auf beiden Achsen, Horizontale und Vertikale, unter der Verwendung von textAlign() ausgerichtet werden. Die Vertikale (*y*-Achse) ist dabei nur ein optionaler Wert - die *x*-Achse muss jedoch immer angegeben werden.

  * **textAlign()** setzt die Ausrichtung alle danach folgenden mit text() dargestellte Texte. Diese Funktion kann mit einem oder zwei Parametern aufgerufen werden. Der erste definiert die *x*-Achse (Horizontale), optional kann mit dem Zweiten die y-Achse (Vertikale) angegeben werden. Als ersten Wert können folgende Angaben genutzt werden: LEFT, CENTER, RIGHT. Als Standard wird von Processing LEFT verwendet. Für die y-Achse finden folgende Werte Verwendung: TOP, CENTER, BOTTOM. [[processing-reference:textAlign()]]

```processing
// Ausrichtung rects
textAlign (RIGHT);
// Ausrichtung unten-rechts
textAlign (RIGHT, CENTER);
```

Die Begriffe zur Festlegung der Ausrichtung (LEFT, TOP, RIGHT, etc.) müssen in Versalien geschrieben werden.

###### Bsp.: Text horizontal ausrichten
Im unteren Beispiel legt die Variable ''xpos'' die *x*-Position beider Textschnippsel fest. Text 1 ("creative") wird links ausgerichtet - wie in Processing standardisiert. Der zweite Text ("coding") wird an selbiger Position platziert, aber mittels textAlign (RIGHT); rechts ausgerichtet. Text 2 endet deshalb an der Startposition von Text 1.

{{/files/documents/b07_05_text_align1.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size(500, 140);
// Hintergrund einfärben
background (45);

// Laden der Schrift in die Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");
// Setze die Schrift 'font' als Standardschrift
textFont (font);

// Variable für die x-Position des Textes
float xpos = 190;
// vertikale Linie an der Textposition
line (xpos, 0, xpos, height);

// Text links ausgerichtet
textAlign (LEFT);
text ("creative", xpos, 67);

// Text rechts ausgerichtet
textAlign (RIGHT);
text ("coding", xpos, 110);
```

#### Textbreite
Um Texte in Proportionen zur Zeichenfläche platzieren zu können, benötigen wir Informationen zur Breite. Processing gibt uns Antwort auf diese Frage mit dem Aufruf von textWidth(). Trotz der durch Pixel limitierten Darstellung auf dem Bildschirm erhalten wir eine Fließkommazahl (Datentyp *float*) der uns bei der Positionierung von Textschnippseln dient.
Bei der Berechnung dieses Wertes spielen die aktuellen Einstellungen wie textFont() (aktuelle Schriftart) und textSize() (Größe der Schrift) eine Rolle. Bei zwischenzeitlicher änderungen dieser Optionen, muss die Textbreite neu berechnet werden.

  * **textWidth()** gibt die Breite eines Textes für die aktuell mit textFont() gesetzte Schrift zurück - in Abhänigkeit von textSize(). Als einzigen Parameter wird der Text übergeben. [[processing-reference:textWidth()]]```processing
float breite = textWidth("Wie breit bin ich?");
```

###### Bsp.: Textbreite
Wir arbeiten in diesem Beispiel mit zwei Variablen (''xpos1'' und ''xpos2''), die jeweils die *x*-Position eines der beiden Textschnippsel beinhalten. ''xpos1'' wird von uns statisch ein Wert von 40 zugewiesen. Variable "xpos2" bekommt den Wert der Summe von ''xpos1'' (in diesem Fall 40) und der von Processing berechneten Breite unseres ersten Textes ("creative"). Beide Texte, bzw. Wörter, sind dadurch direkt aneinandergereiht.

{{/files/documents/b07_06_text_width.png}}

```processing
// Variable zum Ablegen 
// des Schriftschnittes
PFont font;

// Größe des Sketches
size(500, 140);
// Hintergrund einfärben
background (45);

// Laden der Schrift in 
// die Variable 'font'
font = loadFont ("HelveticaNeue-Bold-48.vlw");
// Setze die Schriftart
textFont (font);

// Variable für die x-Position der Texte
// 'xpos2' ist die Summe aus 'xpos1' + der 
// Breite des zweiten Textes in Pixel
float xpos1 = 40;
float xpos2 = xpos1 + textWidth ("creative");

// Text darstellen an den x-Positionen, die
// y-Position ist bei beiden die Selbe
text ("creative", xpos1, 97);
text ("coding", xpos2, 97);

// Linien zur Überprüfung der x-Positionen
line (xpos1, 0, xpos1, height);
line (xpos2, 0, xpos2, height);
```