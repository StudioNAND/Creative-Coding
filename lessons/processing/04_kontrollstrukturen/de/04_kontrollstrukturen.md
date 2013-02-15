# Kontrollstrukturen
## Abfragen und Schleifen

> Einführung in Kontrollstrukturen zur Steuerung des Ablaufs eines Programms. Im Fokus dieser Lesson steht die Auseinandersetzung mit der while und for-Schleife, die durch Wiederholungen komplexere Prozesse effizient im Code abbilden können. Am Schluß folgt ein Beispiel zu verschachtelten for-Schleifen, die die Grundlage für die Anordnung visueller Elemente im Raster bzw. in einer Matrix bilden können.

---

=== Schleifen ===

Um visuelle Komplexität zu generieren muss eine Vielzahl von [[lesson:9#visuelle_grundelemente|Zeichenbefehlen]] aufgerufen werden. Viele Formen oder Formzusammenschlüsse weisen Ã„hnlichkeiten auf und unterscheiden sich im Quelltext nur durch unterschiedliche Angaben von Parametern (z.B. ''x1'', ''y1'', ''x2'', â€¦) die den Zeichenbefehlen folgen.
Im unteren Beispiel werden fünf Linien gleichmäßig mit einem Abstand von jeweils 20px auf der //y//-Achse verteilt.

[code|processing]
void draw () {
  background (255);
  
  line (0, 0, 320, 0);
  line (0, 20, 320, 20);
  line (0, 40, 320, 40);
  line (0, 60, 320, 60);
  line (0, 80, 320, 80);
}
[/code]

Die x-Position der Anfangs- und Endpunkte bleibt bei allen fünf Aufrufen bei 0px bzw. 320px. Nur die //y//-Position erhöht sich von line() zu line() Aufruf. Im Folgenden lernen wir nun eine Schreibform die uns Arbeit erspart und uns die Möglichkeit gibt die Anzahl der Linien zu steuern. Bisher haben wir in zwei Fällen von sogenannten "Blöcken" gesprochen. Blöcke die mittels geschweifter Klammern ( {â€¦} ) einen besonderen Bereich markieren. Im Fall von [[lesson:10#vorbereitung_fortlaufende_programme|draw()]] wird ein Einzelbild erstellt - bei //if// und //else// entscheidet eine Bedingung über die Ausführung des Programmabschnittes.\\ 
Nun lernen wir eine neue Art von Block kennen, die einen Bereich beschreibt der mehrfach ausgeführt werden kann. Das resultierende Konstrukt (Kontrollstruktur) wird als "Schleife" bezeichnet, von denen es mehrere Formen gibt.

==== while-Schleife ====

Die einfachste Form einer Schleife ist die sogenannte //while//-Schleife. Formuliert wird sie durch die Angabe einer Laufbedinung und den geschweiften Klammern ''{ }''. Eine Laufbedinung muss eine Frage stellen, die klar mit Ja (''[[lesson:35#datentypen|true]]'') oder Nein (''[[lesson:35#datentypen|false]]'') beantwortbar ist. Hat eine Variable einen bestimmten Wert; liegt ein Wert unter/über einer Grenze; Ist die Maustaste gedrückt?. Wenn aus dieser Bedingung ein ''true'' resultiert wird der Code innerhalb des Schleifenkörpers (zwischen den geschweiften Klammern) ausgeführt. Kommt es jedoch zu einem ''false'' - wird die gesamte Schleife übersprungen und das Programm läuft weiter.\\ 
Im Falle einer Bedingung die immer mit Ja (''true'') beantwortet wird erhält man eine Endlosschleife. In dieser speziellen Version hängt das Programm in der //while//-Schleife und es werden beispielsweise keine weiteren Einzelbilder gezeichnet, wenn die ''while''-Schleife im draw() Block platziert ist.

[code|processing]
while (Bedingung) {
  // repetiver Prozess
}
[/code]

Formuliert wird die //while//-Schleife durch den Begiff ''while'', gefolgt von der Bedingung in runden Klammern. Nachdem die Klammernkombination geschlossen wird beginnt die Defintion des Schleifenkörpers. Wie jeder weitere Block, z.B. setup() oder draw() wird dieser mit geschweiften Klammern umfasst. Wenn die Bedingung ein ''false'' als Resultat besitzt, läuft das Programm unterhalb des Schleifenkörpers, nach der zweiten geschweiften Klammer, weiter.

====== Bsp.: while-Schleife 1 ======

[code|processing]
void draw () {
  background (255);

  float y=0;
  
  while (y <= 100) {
    line (0, y, 320, y);
    y = y + 20;
  }
}
[/code]

Unsere erste //while//-Schleife liefert das oberhalb eingeführte Muster aus vier horizontalen Linien. Bevor die Schleife mit dem Begriff ''while'' ins Leben gerufen wird, legen wir die Variable ''y'' mit dem Wert 0 an. In ihr soll die //y//-Position der Linien gespeichert werden.\\ 
Bevor der Schleifenkörper abgearbeitet wird, stellt Processing die in der Bedinung formulierte Frage:"Ist y kleiner-gleich 100?". Da ''y'' zu Beginn den Wert 0 besitzt springt Processing in den Schleifenkörper und zeichnet eine Linie an der Position //x1=0//, //y1=0//, //x2=320// und //y2=0//. Damit liegt diese direkt an der oberen Bildschirmkante. Die zweite Zeile im Schleifenkörper erhöht den Wert von ''y'' um 20. Da die Bedingung der //while//-Schleife positiv war versucht Processing nun ein zweites Mal die Schleife auszuführen. Der aktuelle Wert von ''y'' ist nun 20 - eine weitere Linie wird im Sketchfenster 20 Pixel unter der Ersten gezeichnet.\\ 
Processing schafft es genau fünf Linien untereinander zu setzen. Dann hat ''y'' einen Wert von 120. Die Frage ob es "unter, bzw. gleich 100 ist" gibt ''false'' zurück. Dieses Beispiel zeigt die Struktur und Funktion von while-Schleifen. Da die Anzahl der Durchläufe relativ gering ist und innerhalb des Schleifenkörpers simple Prozesse ablaufen, ist der große Vorteil von Schleifen nicht unmittelbar kenntlich. Trifft jedoch einer der beiden Punkte zu, wird dieses Konstrukt unverzichtbar.

====== Bsp.: while-Schleife 2 ======

[code|processing]
void draw () {
  background (255);
 
  float y=0;
 
  while (y <= 100) {
    line (0, y, 320, y);
    y = y + 2;
  }
}
[/code]

Beide Beispiele unterscheide sich nur in der letzte Zeile des Blocks der //while//-Schleife. In der ersten Version erhöhen wir den Wert von ''y'' um 20, im zweiten Fall um 2. Das Resultat von Nummer zwei ist ein viel dichteres Muster aus Linien da wir 52 statt 5 Durchläufe der Schleife zählen.

==== for-Schleife ====

Als zweite Form einer Schleife lernen wir nun die //for//-Schleife kennen. Ebenso wie die //while// Version dient sie dazu einen Codeblock als repitiven Prozess zu formulieren. Der Kontrollmechanismus der //while//-Schleife bestand aus einer Frage die mit ''true'' zum Ausführen der Schleife führte. Bei ''false'' wurde die Schleife abgebrochen bzw. gar nicht erst ausgeführt. Im Beispiel nutzten wir die Variable ''y'' um die Anzahl der Durchgänge zu regulieren und einen Abbruch nach fünf gezeichneten [[lesson:9#linie|Linien]] zu erzwingen. Die //for//-Schleife ist neben der Abbruchbedingung mit zwei weiteren Bestandteilen ausgestattet, welche das Anlegen einer Variable zur Kontrolle (''y'' im //while// Beispiel) überflüssig macht. Diesen Typ von Variable, der sich auf die Anzahl der Durchläufe auswirkt, nennt man "Zählvariable". Beim Schleifenaufruf, der Initialisierung, wird diese angelegt und nach jedem Durchgang aktualisiert.
Neben der englischen Bezeichnung ist die //for//-Schleife unter dem Namen "Zählschleife" bekannt. Ausschlaggebend dafür ist die Zählvariable, welche diese Schleifenform von der //while//-Schleife unterscheidet. Aufgerufen wird die //for//-Schleife in Processing über die folgende Struktur:

[code|processing]
for (Initialisirung; Test; Aktualisierung) {
  // repetiver Prozess
}
[/code]

Der Begriff //for// leitet die Schleife ein, gefolgt von dem in runden Klammern umfassten "Initialisierung-Test-Aktualisierung" Block. Zur Formulierung des Schleifenblocks folgen nach der geschlossenen runden Klammer ein Paar geschweifte Klammern ''{ }''. Alles innerhalb dieses Blocks wird als Schleifenkörper bezeichnet und bei jedem Durchlauf von Processing abgearbeitet.
  * **Initialisierung** beschreibt die Festlegung der Zählvariable zur Steuerung der Zählschleife. Als Variable hat sich die Verwendung von einer Ganzzahl mit dem einfachen Namen //i//, für Iterator, durchgesetzt.
  * **Test**, Bedingung beinhaltet eine logische Abfrage die vor jedem Beginn eines Schleifendurchlaufs getestet wird. Bei Nichtzutreffen wird das Programm unterhalb des for-Blocks abgearbeitet.
  * **Aktualisierung** der Zählvariable nach Ablauf eines Schleifendurchgangs.
Wie bei der //while//-Schleife kann es zu einer Endlosschleifen kommen. Grundlage dafür sind Fehler beim Verfassen der "Initialisierung-Test-Aktualisierung"-Kombination. Beispielsweise wenn die Zählvariable bei 0 startet und nach jedem Durchlauf um 1 erhöht wird, wobei der Test die Schleife nur abbricht, wenn der Wert der Zählvariable unter 0 kommt (was nie der Fall ist).

====== Bsp.: for-Schleife 1 ======

[code|processing]
void draw () {
  background (255);
  
  for (int i=0; i < 5; i = i + 1) {
    line (0, i * 20, 320, i * 20);
  }
}
[/code]

Dies ist die mit einer //for//-Schleife vereinfachte Version des oberen Beispiels. Dabei ist die Zeilenanzahl zwar nur auf drei gesunken - es steht uns aber die Option offen den Teil //i < 5// durch //i < 50// zu ersetzen. Unsere Linie würde damit 50 mal abgebildet werden.

====== Bsp.: for-Schleife 2 ======

[code|processing]
void draw () {
  background (255);

  for (int i=0; i < mouseY; i++) {
    // weise der Linienfarbe einen Farbwert 
    // mittels der Zählvariable "i" zu
    stroke (i * 2, i, 0);

    // zeichne eine horizontale Linie 
    // verwende den Wert der 
    // Zählvariable als y-Position 
    line (0, i, width, i);
  }
}
[/code]

Wir haben mit dem oberen Beispiel unseren ersten dynamischen Farbverlauf erstellt. Die Schleife beginnt bei 0px auf der y-Achse und zeichnet solange eine Horizontale bis sie unsere Maus erreicht. Dabei wird von Linie zu Linie der Farbwert leicht variiert - ein Verlauf entsteht.

====== Bsp.: rückläufige for-Schleife ======

[code|processing]
size(300, 300);
background (255);
// aktiviere Kantenglättung
smooth ();
// deaktiviere outlines
noStroke ();

// führe die Schleife aus bis die Zählvariable "diameter" 
// einen Wert erreicht der kleiner als 0 ist. Verringere dabei 
// ihren Wert nach jedem Durchgang um 12.
for (int diameter=255; diameter > 0; diameter = diameter - 12) {
  // setze die Füllfarbe neu
  fill (diameter);
  // zeichne den Kreis mit variablem Durchmesser
  ellipse (width / 2, height / 2, diameter, diameter);
}
[/code]

====== Bsp.: verschachtelte for-Schleife ======

[code|processing]
void draw () {
  // fülle die gesamte Zeichenfläche mit weiß
  background (255);
  // deaktiviere Umrandungen
  noStroke ();
  
  // erstelle zwei Variablen zur späteren 
  // Ablage der Positionen
  float x;
  float y;
  
  // Schleife für die Matrix-Zeilen
  for (int i=0; i < 5; i = i + 1) {
    // Schleife für die Matrix-Spalten
    for (int j=0; j < 5; j = j + 1) {
      
      // DIESER TEIL WIRD FÜR JEDEN 
      // KREIS AUSGEFÜHRT!
      
      // Berechnung der Position
      x = i * 20;
      y = j * 20;
      
      // bestimme die Füllfarbe und zeichne 
      // anschließend die Ellipse
      fill (i * 50, 0, j * 50);
      ellipse (x, y, 27, 27);
    }
  }
}
[/code]

Bei der Verschachtlung von Zählschleifen muss nur auf die Namen der Zählvariablen geachtet werden. Doppelbelegungen sind hierbei nicht zulässig. Deshalb verwenden wir in der zweiten //for//-Schleife den Variablennamen j (i, j, k haben sich als Standard etabliert).