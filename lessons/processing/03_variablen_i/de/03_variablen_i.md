# Variablen I
## Einführung in Variablen und Datentypen

> Vorgestellt werden die wichtigsten Datentypen für erste kleine Programme in Processing: boolean, int, float, String. Anhand dieser Datentypen wird die Verwendung von Variablen - deren Deklaration, Initialisierung, Abfrage und Zuweisung - eingeführt. Danach folgt ein Überblick über den Umgang mit Daten mit Hilfe von Operatoren. Dabei spielen Rechenoperationen ebenso eine Rolle, wie auch Vergleiche und logische Verknüpfungen.

---

### Datentypen
Kommunikation basiert auf dem Austausch von Daten. Entscheidungen werden mit ja - nein gefällt. Die Kühlschranktemperatur ist meist ein Wert zwischen 1 und 7 Grad Celsius. Einem Menschen werden Reihungen von Zeichen zur Identifikation zugewiesen. Diese Art der Beschreibung von Gegenständen und Individuen mit Informationen kann auch in Programmiersprachen verwendet werden. Hierbei sprechen wir immer von [Daten](http://de.wikipedia.org/wiki/Daten). Neben den [Algorithmen](http://de.wikipedia.org/wiki/Algorithmus) sind sie der Hauptbestandteil jeglicher Computer Software. Software besteht also aus Informationen (Daten) und Anweisungen zu ihrer Verarbeitung (Algorithmen). Im Bereich der Programmierung reden wir beim Umgang mit Daten oftmals von Variablen - einen Namen, den man sich gut darüber herleiten kann, dass Daten in Programmen prinzipiell *variabel* - also veränderbar - sind. Eine bewährte Metapher die beim Verständnis zum Umgang mit Variablen hilft ist die einer Schublade.\\ 
Variablen können wie Schubladen einen Wert haben (Inhalt) - müssen dies aber nicht (die Schublade existiert, ist jedoch leer). Jede Schublade hat jedoch unabhängig von ihrem Inhalt einen Namen (eine Beschriftung). Über diesen Namen können wir Werte von Variablen abfragen oder verändern. Die einzige Besonderheit von Variablen ist, dass sie jeweils beschränkt sind auf eine bestimmte Art von Inhalten. So gibt es Schubladen in denen man nur Ganzzahlen oder Kommazahlen speichern kann, sowie Schubladen die nur ein einfaches »Ja« oder »Nein« beinhalten können. Wir werden im Verlauf der weiteren Lessons noch weiteren speziellen Schubladen über den Weg laufen und auch lernen wie wir Schubladen speziell nach unseren Wünschen anlegen<<lesson:22>>.\\ 
In der Lesson zur [[lesson:10]] haben wir bereits vier solcher Variablen/Schubladen kennengelernt. Die Processing-Umgebung stellt uns z.B. die Koordinaten der Maus über die Ausdrücke mouseX und mouseY zur Verfügung. Da sich hinter diesen Begriffen keine einfachen Klammern befinden handelt es sich bei ihnen um Variablen. Processing ändert für uns vor jedem draw() Durchlauf den Wert dieser Variablen, sodass wir immer auf die aktuelle Lage der Maus zugreifen können.

Zum Einsteigen gebrauchen wir vier elementare Typen. Sie unterscheiden - wie oben beschrieben - sich in Ihrem Fassungsvermögen, also darin welche Art von Inhalten in ihnen gespeichert/abgelegt werden kann:

  * **boolean** speicher nur »Ja« oder »Nein« (*true* oder *false*, z.B. ist die Maustaste gedrückt, oder nicht?) [[processing-reference:boolean]]
  * **int** für ganzzahlige Werte (*integer*) 0, 1, 2, -3, ... bis zu zwei Billionen [[processing-reference:int]]
  * **float** für Gleitkommazahlen (//floating point number//). Die Notation wird wie im Englischen durch einen Punkt durchgeführt (falsch: *1,42* richtig: *1.42*) [[processing-reference:float]]
  * **String** Zeichenkette die in doppelten Anführungszeichen anzugeben ist, z.B. "Creative Coding" [[processing-reference:String]]

Bevor wir eine Variable nutzen können müssen wir sie ins Leben rufen; Processing mitteilen das wir vorhaben mit ihr im späteren Ablauf des Programms zu arbeiten. Dies geschieht immer mit der Angabe ihres Typs (z.B. *int*, *float*, etc. ) und einem Namen zur Identifikation.

###### Bsp.: Variablen definieren
```processing
boolean jaNein;
int ganzzahl;
float gleitzahl;
String textabschnitt;
```

Namen von Variablen dürfen nur Buchstaben, Zahlen, $ und _ enthalten und sollten immer mit einem Buchstaben beginnen. Die Vergaben von Leerzeichen ist nicht erlaubt. Um zusammengesetzte Name trotzdem lesbar abzubilden wird der erste Buchstabe eines folgenden Wortes großgeschrieben (z.B. *roteaepfel* wird zu *roteAepfel*). **Genau wie beim Aufruf von Befehlen ist Groß- und Kleinschreibung unbedingt zu beachten!**

Im oberen Beispiel haben wir zwar drei Variablen unterschiedliche Typs erstellt - jedoch können wir ohne Inhalt nicht mit ihnen arbeiten. Wir benötigen eine sogenannte Zuweisung eines Wertes. Dies geschieht mit einem = welches dem Variablennamen folgt. Rechts neben dem Istgleich erwartet Processing den Wert den es in hinter unserem Begriff (Variable) verstecken soll - gefolgt von einem Semikolon, um die Anweisung zu Beenden.

###### Bsp.: Werte zuweisen
```processing
// boolean Variable mit dem Wert 'ja' ('wahr')
boolean jaNein = true;

// ganzzahlige Variable mit dem Wert 40
int ganzzahl = 40;

// Variable mit dem gleitkomma Inhalt 36.9
float gleitzahl = 36.9;

// Variable die den Textschnipsel "Creative
// Coding" beinhaltet
String textabschnitt = "Creative Coding";
```

Beim Ausführen der beiden oberen Beispiele erhalten wir momentan keinerlei Feedback vom Programm. Das Sketchfenster öffnet sich und stellt uns den üblichen grauen Hintergrund dar. Das Einsehen des Wertes/Status der Variable könnte über eine textuelle Ausgabe in unserer Zeichenfäche geschehen, wäre aber vom Aufwand hoch einzustufen. In Processingprogramm existiert unter dem Texteditor, in welchem wir unseren Quellcode schreiben, eine schwarze Box. Bisher wurden uns hier im Ernstfall Fehlermedldungen abgebildet - zwei Befehlen erlauben uns aber auch sie selbst zu Befüllen:

  * **print()** gibt einen Inhalt bzw. Wert einer Variable in der Konsole aus. [[processing-reference:print()]]
  * **println()** gleiche Funktion wie print(), jedoch wird bei jedem Aufruf eine neue Zeile zur Ausgabe genutzt. [[processing-reference:println()]]

###### Bsp.: Werte modifizieren
```processing
// erstellt eine ganzzahlige Variable names 
// "zahl" und gibt ihr den Wert 39
int zahl = 39;

// Ausgabe in der Konsole
println (zahl);

// erhöhe den Wert von "zahl" um eins
zahl = zahl + 1;

// Ausgabe in der Konsole
println (zahl);
```

Die Angabe des Datentypen ist nur bei der Initialisierung nötig. Im weiteren Ablauf geschehen Abfragen und Zuweisungen ohne Angaben wie *int*, *float* oder *String*.

###### Bsp.: Verwendung von Variablen
```processing
void draw() {
  // lösche die Zeichenfläche und fülle sie mit weiss
  background (255, 255, 255);

  // erstelle eine Variable mit dem Namen "grenze"
  // und gib ihr den ganzzahligen Wert 50
  int grenze = 50;

  // wenn die Mausposition auf der x-Achse kleiner
  // ist als unsere definierte Grenze...
  if (mouseX < grenze) {
    // zeichne eine kleine ellipse an der Mausposition
    ellipse (mouseX, mouseY, 10, 10);
  }else{
    // zeichne eine große ellipse an der Mausposition
    ellipse (mouseX, mouseY, 50, 50);
  }

  // dieser Teil wird immer ausgeführt
  // (unabhängig vom Mauszustand)
  rect (90, 90, 10, 10);
}
```

### Operatoren
Operatoren kommen stets in Verbindung mit Variablen zum Einsatz und führen *Operationen* an ihnen durch. Die bekanntesten Operatoren sind die aus dem unbeliebten Mathekurs: +, -, * und / (geteilt). Mit ihnen haben wir vorher schon *Operationen* an Zahlen durchgeführt, also mit ihnen gerechnet. Andere Operatoren werden z.B. zur Formulierung von Fragen verwendet. Beispielsweise ob die Frucht ein Apfel ist und dieser die Farbe Grün besitzt.

#### Rechenoperationen
Der Titel dieses Abschnittes lässt Erinnerungen an vergangene Zeiten im unbeliebten Mathekurs aufkommen. Visuelle Eigenschaften wie Positionen und [[lesson:9#farben|Farbwerte]] werden von uns durch Zahlen angegeben - nun lernen wir diese Werte zu kontrollieren. Processing gibt uns dabei die vier grundlegenden Rechenoperationen, plus zwei Weitere die uns das Tippen ersparen.

  * **+** addiert zwei numerische Werte oder fügt zwei Zeichenketten (String) zusammen.
  * **-** subtrahiert zwei numerische Werte oder negiert einen Wert.
  * ** * ** multipliziert zwei numerische Werte.
  * **/** dividiert zwei numerische Werte.
  * **++** erhöht den Wert einer Variable um 1.
  * **--** verringert den Wert einer Variable um 1.

###### Bsp.: Strichrechnung
```processing
float a = 4.2;
float b = 1.3;

// Ausgabe: 5.5
println (a + b);

// Ausgabe: -2.8999999
println (b - a);

// Ausgabe: "Creative Coding 1"
println ("Creative " + "Coding " + 1);
```

###### Bsp.: Punktrechnung 1
```processing
int a = 5;
int b = 2;

// Ausgabe: 10
println (a * b);

// Ausgabe: 2
println (a / b);
```
Das Ergebniss der Multiplikation von 5 x 2 = 10 ist zu wie erwartet eingetreten. Aber bei der Division beider Werte fehlt einhalb. Dies liegt an dem von uns vergebenen Datentyp (bei beiden Variablen *int*, Ganzzahl). Wenn zwei Ganzzahlen durcheinander geteilt werden wird das Ergebniss von Processing immer auf die nächste Ganzzahl abgerundet - in unserem Fall 2.
Um dieses Problem zu umgehen muss mindestens eine der beiden Variablen eine Gleitkommazahl (*float*) sein:

###### Bsp.: Punktrechnung 2
```processing
float a = 5;
float b = 2;

// Ausgabe: 2.5
println (a / b);
```

###### Bsp.: Erhöhen
```processing
int zahl = 94;

// Ausgabe: 94
println (zahl);

// erhöht den Wert um 1
zahl++;

// Ausgabe: 95
println (zahl);
```

##### Bsp.: Verringern
```processing
int zahl = 94;

// Ausgabe: 94
println (zahl);

// verringert den Wert um 1
zahl--;

// Ausgabe: 93
println (zahl);
```

#### Vergleichsoperationen
  * **''==''** gleich
  * **''!=''** ungleich
  * **''> ''** größer als
  * **''>=''** größer gleich als
  * **''< ''** kleiner als
  * **''<=''** kleiner gleich als

Nach unserem Wissen müsste diese Abfrage folgende Struktur haben:

```processing
String fruchtSorte = "apfel";
String fruchtFarbe = "gruen";

if (fruchtSorte == "apfel") {
  if (fruchtFarbe == "gruen") {
    println ("greif zu!");
  }
}
```

#### Logische Operationen
Alle im Weiteren aufgeführten Elemente dienen zur Formulierung und Verknüpfung von Abfragen. Grundsätzlich muss das Resultat immer wahr oder falsch sein.

  * **''&&''** UND
  * **''! ''** NICHT
  * **''||''** ODER

```processing
String fruchtSorte = "apfel";
String fruchtFarbe = "gruen";

if (fruchtSorte == "apfel" && fruchtFarbe == "gruen") {
  println ("greif zu!");
}
```

Nun wurden beide Fragen innerhalb einer einzigen *if*-Abfrage gestellt. Beide müssen zutreffen damit "greif zu!" in der Konsole erscheint. Im nächsten Schritt lassen wir neben grünen Ã„pfeln alle roten Früchte zu:

```processing
String fruchtSorte = "apfel";
String fruchtFarbe = "gruen";

if (fruchtSorte == "apfel" && fruchtFarbe == "gruen" || fruchtFarbe == "rot") {
  println ("greif zu!");
}
```