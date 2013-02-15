# Objekt-Orientierte Programmierung
## Klassen, Attribute, Methoden und Instanzen

> Diese Lesson führt die letzten Elemente im Basiskurs zur Programmierung mit Processing ein - Objekte und deren Verwendung. Nach einer Einführung zum Konzept der Objekt-Orientierten Programmierung werden die grundlegenden Bausteine von zusammengesetzten Datentypen (Klassen) erklärt und beispielhaft ihr Einsatz bei der Programmierung erläutert.

---

### Grundgedanketest
Ein modulares Programm besteht aus einzelnen Modulen, von den jedes eine bestimmte Aufgabe erfüllen soll. Von der Lesson [[lesson:11]] kennen wir den Ansatz der Wiederverwendbarkeit. Sie ermöglichen es einem einzelnen Wert mehrfach in einem Programm aufzutauchen, so dass dieser einfach geändert werden kann. Funktionen<<lesson:20>> abstrahieren eine bestimmte Aufgabe und ermöglichen ebenfalls eine Wiederverwendbarkeit dieser Aufgabe. Dabei ist immer entscheidend, was eine [[lesson:20|Funktion]] tut und nicht wie sie im Detail funktioniert (Abstraktion). Diese Herangehensweise ermöglicht es, sich auf die Ziele eines Programms zu kümmern anstelle sich in Details zu verlieren.

Der **OOP-Ansatz** erweitert diese Modularität, in dem Variablen und Funktionen zu Objekten gruppiert werden.\\ 
Das Ziel dabei ist das Gestalten von regelbasiertem Verhalten in Form von Objekten. Die Verhaltensweisen eines Objektes sind formulierte Prozesse, die auf einen bestimmten Input einen bestimmten Output liefern. Man spricht bei diesen speziellen Funktionen von **Methoden**.
Ein Objekt kann weiterhin erst definiert werden, wenn wir seine Eigenschaften kennen. Durch diese Eigenschaften wird das Objekt unterscheid- und vergleichbar mit anderen Objekten. \\ 
\\ 
Dabei ist es durchaus möglich Analogien zwischen Software-Objekten und realen Objekten zu bilden.
[[image:51|center]]
         
### Begriffe
Im Texteditor wurde der Code des Sketches bis dato nur in einem Tab formuliert. Dieser Tab trägt den Namen unter welchem der Sketch abgelegt wurde - bzw. einen temporären, kryptischen wenn dies noch nicht passiert ist. Wie bereits angesprochen ist ein Vorteil von oop die Weiterführung des Modularisierungsansatzes von Programmen.\\ 
Jede sog. Klasse, die als Grundlage für die Objektgenerierung dient, wird in einem neuen Tab geschrieben. Um einen neuen Tab anzulegen, Klickt man im rechten Teil der Tableiste auf den quadratischen Button (->) und wählt 'New Tab'. Über der Konsole erscheint ein Eingabefeld in dem Processing der Name der Klasse mitgeteilt werden muss. Nach dem Bestätigen der Eingabe mit 'Ok' erhält man ein neues Tab und kann mit der Ausformulierung der Klasse beginnen.

#### Klasse
Basis für eine OOP-Konstruktion ist die Klasse. Ihr Inhalt dient als Bauplan für das spätere Erstellen von Objekten - auch Instanzen oder Klasseninstanzen genannt. Der Begriff *class* leitet die Formulierung ein, worauf der Klassenname folgt. Dieser muss mit einem Großbuchstaben beginnen((&laquo;muss&raquo; ist hier ein wenig übertrieben. Technisch gesehen kann der Klassenname auch mit einem kleinen Buchstaben oder gar einem Unterstrich beginnen. Es hat sich jedoch über die Jahre der Entwicklung mit Programmiersprachen zur allgemeine Konvention entwickelt, Klassennamen - und nur diese - mit einem grossen Buchstaben beginnen zu lassen um beim Lesen sofort zu wissen, dass es sich um eine Klasse handelt. Diese Konvention wollen wir beibehalten.)) und taucht beim Arbeiten als [[lesson:11|Datentyp]] bzw. direkt hinter dem Wort *new* auf. Innerhalb der geschweiften Klammern folgen die Attribute und Methoden der Klasse. Alles was außerhalb des Klassenblocks steht, gehört nicht zur Klasse.

```processing
class Butterfly {

  // Der Klassenblock

}
```

#### Attribut
Attribute sind die Eigenschaften die eine Klasse aufweist. Sie geben den Objekten die Möglichkeit sich voneinander zu unterscheiden, bzw. eine Vergleichbarkeit untereinander herzustellen. In der Formulierung der Klasse tauchen die Attribute an erster Stelle auf. Da es sich bei ihnen um [[lesson:11|Variablen]] handelt, folgt nach der Angabe des Datentyps (String, int, float, â€¦) der bezeichnende Name. Neben dem Datentyp können weitere OOP-spezifische Kriterien vergeben werden. Da es sich dabei aber um keine Notwendigkeit handelt, belassen wir es in diesem Abschnitt bei der kompakten Version.

```processing
class Butterfly {

  String species;
  String gender;

}
```

#### Methode
Die als Fähigkeiten aufgeführten Methoden werden ebenfalls im Klassenkörper platziert. Direkt unter den Attributen formulieren sie Prozesse in von [[lesson:20|Funktionen]] bekannter Schreibweise. Das Zurückgeben von Variablen als Result des Aufrufs (siehe Rückgabewerte in der Lesson zu Funktionen<<lesson:20>>) und die Angabe von [[lesson:20|Parametern]] ist wie bei normalen Funktionen möglich. Durch Einsatz dieser Bausteine kann eine hohe Varianz in das Verhalten unterschiedlicher Objekte gelegt werden.

```processing
class Butterfly {
   
   void fly () {
     // Prozess 'fliegen'
   }

   void land () {
     // Prozess 'landen'
   }
}
```

#### Konstruktor
Beim Arbeiten mit *Capture* wurden Ausdrücke wie ''Capture c = new Capture (â€¦);'' verwendet (siehe Kapitel über [[lesson:27|Video in Processing]]). Da Informationen wie Bildgröße, Bilder pro Sekunde und Kameranamen für Processing notwendig sind, mussten dafür Werte zwischen den Klammern ''(â€¦)'' angegeben werden. Beim Anlegen einer Klasse, in dem Fall *Capture*, können solche Daten mit der Festlegung eines sog. Konstruktors erzwungen werden.\\ 
Der Konstruktor ist eine spezielle Funktion einer Klasse und hat keinen [[lesson:20|Rückgabewert]]. Im Klassenaufbau findet er zwischen den Attributen und Methoden Platz. Durch Parameter im Funktionskopf wird definiert, welche Informationen beim Ausdruck ''new KlassenName (â€¦)'' zwischen den Klammern angegeben werden müssen. Innerhalb des Konstruktors erfolgt eine Zuweisung, wobei jeder Parameter seinem Attribut zugeordnet wird.

```processing
class Butterfly {

  String species;
  String gender;

  Butterfly (String theSpezies, String theGender) {
    species = theSpezies;
    gender = theGender;
  }
}
```

### Arbeiten mit Klassen
#### Instanzen/Objekte erzeugen
Mit einer Klasse haben wir gleichzeitig einen [[lesson:11|Datentyp]] erstellt. Beim Anlegen von Instanzen der Klasse taucht der Klassenname vor dem Instanznamen zum ersten Mal auf. Diese Schreibweise ist bereits vom Erzeugen von Variablen bekannt. Nach dem //=// folgte bei Variablen die Zuweisung des Wertes, z.B. "Text" oder Zahlen. Da es sich bei Klassen automatisch um komplexe Datentypen handelt, muss eine Instanz der Klasse mit dem Wörtchen *new* erstellt werden. Dadurch nimmt sich Processing den 'Objektbauplan' und strickt uns ein Abbild der Klasse - eine Instanz.

```processing
KlassenName InstanzName = new KlassenName (Parameter des Konstruktors);
```

Bezogen auf unser Schmetterlingsklasse sieht das Erstellen von Instanzen wie folgt aus:

```processing
Butterfly bfW = new Butterfly ("Zitronenfalter", "weiblich");
Butterfly bfM = new Butterfly ("Zitronenfalter", "männlich");
```

Die Instanzen tragen die Bezeichnungen ''bfW'' und ''bfM''. Beide sind von der Gattung 'Zitronenfalter' - unterscheiden sich jedoch im Geschlecht. Die Anzahl und Reihenfolge der übergebenen Parameter beim Erzeugen muss mit Definition im Konstruktor übereinstimmen.

#### Arbeiten mit Instanzen/Objekten
Der Zugriff und das Ansprechen von Instanzen funktioniert über die Punktnotation. Instanz- und Attributs- bzw. Methodenname werden dabei durch einen Punkt voneinander getrennt.

##### Attribute
Wo bei der Wertzuweisung von Variablen nur der Variablenname links neben dem //=// stand, taucht bei Attributen eine Kombination aus Instanz- und Attributsname auf. Das gleiche Prinzip gilt für das Auslesen von Attributen (siehe println() im Beispiel).

```processing
InstanzName.AttributName = "WERT";
println (InstanzName.AttributName);
```

##### Methoden
Genau wie Attribute spricht man die Fähigkeiten von Klasseninstanzen durch eine Kombination aus Instanz- und Methodenname an. In der zweiten Zeile des Pseudocodes gibt die Methode der Instanz einen *float* Wert zurück, welcher in der Variable ''val'' abgelegt wird. Der Aufruf gestaltet sich demnach wie bei Funktionen, nur das vor dem Methodennamen explizit eine Instanz angegeben werden muss, auf welche diese ausgeführt werden soll.

```processing
InstanzName.MethodenName (Parameter der Methode);
float val = InstanzName.MethodenName (Parameter der Methode);
```

Die Schmetterlingsinstanz ''btW'' kann also auf diese Weise fliegen und landen:

```processing
bfW.fly ();
bfW.land ();
```

Da die Methoden in der Klasse keinen Rückgabewert haben und keine Parameterangaben zulassen, kann der Aufruf nur in dieser Form erfolgen.

### Beispiele
#### Die Klasse »Ball«
###### Bsp.: Anlegen der Klasse
{{ /files/documents/b15_ball_1.jpg}}
Im ersten Beispiel legen wir die Klasse Ball in einem neuen Tab an. Dieses hält neben dem Klassenkörper die Attribute ''x'', ''y'' und ''diameter'' für Position und Durchmesser. Im Sketch (L15_01_oop_ball1) legen wir die Instanz ''b'' global fest. Nachdem wir im [[lesson:10#vorbereitung_fortlaufende_programme|setup()]]-Block das Sketchfenster eingerichtet haben, Erzeugen wir die Ballinstanz mit //b = new Ball();// und füllen die Attribute mit Werten. Das weitere Programm macht nichts anderes, als uns eine [[lesson:9#ellipse|Ellipse]] mit der Position und Größe des Balls abzubilden.

```processing

[tab|Ball-example-01]
// Instanz 'b' der Klasse 'Ball'
Ball b;

void setup () {
  size (320, 240);
  smooth ();
  
  // Erzeugen der Instanz
  b = new Ball ();
  // Füllen der Attribute
  b.x = 120;
  b.y = 140;
  b.diameter = 90;
}

void draw () {
  background (0);
  // Zeichnen des Balls durch Auslesen
  // der Instanzeigenschaften
  ellipse (b.x, b.y, b.diameter, b.diameter);
}
[/tab]

[tab|Ball]
class Ball {
  // Attribute der Klasse
  float x;
  float y;
  float diameter;
}
[/tab]

```

###### Bsp.: Anlegen mittels Konstruktor
{{ /files/documents/b15_ball_2.jpg}}
Da das 'manuelle' Befüllen der Instanz mit Werten eine relativ umständliche Angelegenheit ist, legen wir in der Klasse einen Konstruktor dafür an. Dieser wird automatisch bei der Erzeugung der Instanz von uns abgefragt. Visuell bestehen keine unterschiede zwischen diesem und dem ersten Beispiel.

```processing

[tab|Ball-example-02]
// Instanz 'b' der Klasse 'Ball'
Ball b;

void setup () {
  size (320, 240);
  smooth ();
  // Erzeugen der Instanz und gleichzeitiges 
  // Füllen der Attribute durch den Konstruktor
  b = new Ball (120, 140, 90);
}

void draw () {
  background (0);
  ellipse (b.x, b.y, b.diameter, b.diameter);
}
[/tab]

[tab|Ball]
class Ball {
  // Attribute der Klasse
  float x;
  float y;
  float diameter;
  
  // Konstruktor der Klasse 'Ball'
  Ball (float theX, float theY, float theDiameter) {
    x = theX;
    y = theY;
    diameter = theDiameter;
  }
}
[/tab]

```

###### Bsp.: Bewegen durch die Methode »move«
{{ /files/documents/b15_ball_3.jpg}}
Momentan besteht die Klasse nur aus Eigenschaftsdefinitionen. Sie ist nur brauchbar um Werte/Charakteristika abzulegen bzw. auszulesen. In diesem Schritt wird eine Methode (Fähigkeit) zum Bewegen des Balls festgelegt. Platziert im Klassenkörper hat sie den Namen 'move' und besitzt keinen Rückgabewert und keine Parameter<<lesson:20>>. Innerhalb dieser Methode wird der Wert von ''x'' um 1 erhöht und wenn notwendig auf 0 zurückgesetzt. Bei jedem [[lesson:10#vorbereitung_fortlaufende_programme|draw()]] Durchlauf wird //b.move();// aufgerufen, was eine Bewegung des Ball von links nach rechts zur Folge hat.

```processing

[tab|Ball-example-03]
Ball b;

void setup () {
  size (320, 240);
  smooth ();
  b = new Ball (120, 140, 90);
}

void draw () {
  background (0);
  b.move ();
  ellipse (b.x, b.y, b.diameter, b.diameter);
}
[/tab]

[tab|Ball]
class Ball {
  float x;
  float y;
  float diameter;
  
  Ball (float theX, float theY, float theDiameter) {
    x = theX;
    y = theY;
    diameter = theDiameter;
  }
  
  void move () {
    x = x + 1;
    if (x > width) {
      x = 0;
    }
  }
}

[/tab]

```

###### Bsp.: Array von Bällen{{ /files/documents/b15_ball_5.jpg}}
Beispiel Nummer vier demonstriert die Klasse Ball unter Verwendung eines Arrays<<lesson:19>>. Zwei //[[lesson:11|for]]//-Schleifen dienen dabei das Array im //setup()// zu füllen und [[lesson:10#vorbereitung_fortlaufende_programme|draw()]] auszulesen. Innerhalb der ersten Schleife ändert die Zählvariable ''i'' die Startpositionen der einzelnen Bälle.

```processing

[tab|Ball-example-04]
// Anlegen des Ball-Arrays
Ball b[] = new Ball[20];

void setup () {
  size (320, 240);
  smooth ();
  // Erzeugen aller Ballinstanzen
  for (int i=0; i < b.length; i++) {
    b[i] = new Ball (i * 15, 20 + i * 10, 10);
  }
}

void draw () {
  background (0);
  // für jede Ballinstanz
  for (int i=0; i < b.length; i++) {
    // Bewegen des Balls
    b[i].move ();
    // Darstellen im Sketchfenster
    ellipse(b[i].x, b[i].y, b[i].diameter, b[i].diameter);
  }
}
[/tab]

[tab|Ball]
class Ball {
  float x;
  float y;
  float diameter;
  
  Ball (float theX, float theY, float theDiameter) {
    x = theX;
    y = theY;
    diameter = theDiameter;
  }
  
  void move () {
    x = x + 1;
    if (x > width) {
      x = 0;
    }
  }
}
[/tab]
```

#### Gizmo Tierchen
Der folgende Beispielkomlex soll die schrittweise Entwicklung von simulierten &laquo;Lebewesen&raquo; verdeutlichen. Generell gibt es mehrere Prinzipien für die Simulation selbstständig anmutender &laquo;Lebewesen&raquo;. Die beiden bekanntesten sind die [[http://www.red3d.com/cwr/steer/|Steering Behaviors for Autonomous Vehicles]] von Craig W. Reynolds und die [[http://en.wikipedia.org/wiki/Braitenberg_vehicle|Braitenberg Vehicles]] von Valentino Braitenberg. Letztere gehen aber schnell über die reine Bewegung hinaus, in dem Braitenberg Konstruktionsprinzipien, z.B. für die Simulation von Gedächtnisfunktionen beschreibt. Sein Buch<<book:19>> empfehlen wir jedem, der sich ein wenig für Biologie interessiert!.\\ 
Unter Hinzunahme der [Vektor](http://de.wikipedia.org/wiki/Vektor) Klasse [PVector](http://processing.org/reference/PVector.html) werden Bewegungen im Sketchfenster simuliert, ohne das die Objekte dabei die Zeichenfläche verlassen. Im ersten Schritt folgen die Gizmos einem selbstgesetzten Ziel. Kurz vor dem Erreichen wird dieses verschoben - sie bleiben in ständiger Bewegung. Da die erzielte geradlinige Positionsänderung unnatürlich wirkt, verwirft die zweite Version den Gedanken des festen Ziels. Stattdessen werden die Gizmos mit jeweils einer Richtung ausgestattet. Ebenfalls ein Vektor, variieren wir *x* und *y* Wert von Bild zu Bild, um ein konfuses Verhalten zu erzeugen.

[[example:24]]

[[example:25]]

[[example:26]]

[[example:27]]