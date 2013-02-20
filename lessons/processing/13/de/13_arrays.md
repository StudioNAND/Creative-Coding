# Arrays
## Datenreihen

> Thema der Lesson ist die Einführung in Arrays - Datenreihen. Nach einer kurzen Wiederholung zu Variablen und Datentypen werden der Aufbau und Umgang mit Arrays erläutert, sowie praktische Beispiele aus der Animation fortgeführt die die Verwendung von Arrays verdeutlichen.

---

### Wiederholung: Datentypen
Durch die Einführunf von Variablen ([[lesson:35]] & [[lesson:36]]) haben wir die Möglichkeit kennen gelernt unterschiedlich Formen von Daten zu speichern, auszulesen und zu verändern. Folgende [[lesson:35|Datentypen]] kennen wir bereits:
  * **Interger** - simple Ganzzahl, beispielsweise 0, 1, 8, -25, etc. [[processing-reference:int]]```processing
int number = 10;
```
  * **Float** - gebrochene Zahl (Fließkommazahl). Die Trennung erfolgt hierbei durch einen Punkt, nicht wie im Deutschen gewohnt durch ein Komma. [[processing-reference:float]]```processing
float number = 12.5819;
```
  * **Character** - speichert ein einzelnes Zeichen in der [Unicode](http://de.wikipedia.org/wiki/Unicode) - Codierung, z.B.: 'a', '?', 'ä'. Beachte die einzelnen Anführungszeichen um das Zeichen auf der rechten Seite des Istgleich! [[processing-reference:char]]```processing
char a = 'a';
```
  * **Boolean** - [[http://de.wikipedia.org/wiki/Boolesche_Algebra|Bool'scher Wert]] kann nur einer "wahr" - ''true'' oder "nicht wahr" - ''false'' beinhalten. Wir treffen diesen Datentyp meist bei *if*-Bedingungen an. [[processing-reference:boolean]]```processing
boolean nice = true;
```
  * **Color** - beinhaltet die Rot-, Grün- und Blauanteiligkeit (optional den Alphakanal) einer [[lesson:9#farben|Farbe]] (color(43, 31, 22), color(44, 199, 199), color(235, 223, 167), etc.) [[processing-reference:color_datatype]]```processing
color pink = color(255, 0, 255);
```

Diese [[lesson:35|Datentypen]] werden auch [primitiv](http://en.wikipedia.org/wiki/Primitive_type) genannt, da ihr Vorkommen, ihre Struktur und ihre Größe in der verwendeten Programmiersprache fest verankert sind. Beispielsweise kann eine Variable vom Typ *int* immer nur einen ganzzahligen Wert beinhalten. Dieser Fakt hat in unseren Programmen bisher kein Hindernis dargestellt - erlaubte uns aber, speziell im Bereich der [[lesson:17|Animation]], nur eine stark begrenzte Anzahl von Elementen zu bearbeiten.\\ 
Neben den *primitiven* Datentypen gibt es noch die sogenannten [zusammengesetzten](http://en.wikipedia.org/wiki/Composite_type) Datentypen. Ihre Größe und ihr Umfang ist nicht vorgegeben. Ihre Struktur kann in einigen Fällen  verändert werden, da sie im Grunde aus *primitiven* Datentypen zusammengesetzt sind.\\ 
Einen zusammengesetzten Datentypen haben wir bereits bei der Arbeit mit [[lesson:16|Text]] kennengelernt:
  * **String** - Kette aus Zeichen in [Unicode](http://de.wikipedia.org/wiki/Unicode) - Codierung ("Creative", "Coding", "Creative Coding", etc. Umschlossen von doppelten Anführungszeichen!) [[processing-reference:String]]```processing
String text = "too much!";
```

### Arrays
Variablen sind das Gedächtnis unserer Programme. Wir legen dort Informationen (Texte, Zahlen, Ja/Nein) ab um sie im weiteren Ablauf wiederverwenden zu können bzw. zu modifizieren. Die primitiven Variablen haben uns erlaubt eine Information pro deklarierte Variable zu speichern - dies ist gut, aber sehr wenig. Um Programme flexibel zu gestalten, beschäftigen wir uns nun mit dem Erstellen und Verarbeiten von sogenannten Arrays.\\ 
Arrays sind Listen, Reihen von Daten (Array = engl. Reihe). Ein Array besteht aus einer von uns bestimmten Anzahl von Feldern, welche alle einen Wert des gleichen Datentyps speichern können. Beispielsweise die Positionen von fünf [[lesson:9#rechteck|Quadraten]]:

```processing
// Sketchsettings
fill(0);
stroke(0);

// Erstellen und Befüllen der Variablen
float rSize = 20.0;
float pos1 = 0.0;
float pos2 = 20.0;
float pos3 = 40.0;
float pos4 = 60.0;
float pos5 = 80.0;

// Zeichnen der Rechtecke nach den
// Werten der Variablen
rect(pos1, pos1, rSize, rSize);
rect(pos2, pos2, rSize, rSize);
rect(pos3, pos3, rSize, rSize);
rect(pos4, pos4, rSize, rSize);
rect(pos5, pos5, rSize, rSize);
```
Diese Schreibweise mag für fünf Elemente noch erträglich sein, ist aber beispielsweise bei 100 Elementen unbrauchbar (erst recht wenn wir die Positionen über die Zeit hinweg verändern wollen!). Hier kommen Arrays ins Spiel und verkürzen den Code beachtlich.

#### Deklarieren und Initialisieren
Arrays werden in folgender Form notiert:

```processing
// deklariere ein float Array
float[] pos;
```

Die beiden eckigen Klammern hinter der Datentypbezeichnung markieren, dass es sich hierbei um ein Array von *float-Werten* handelt.
Als nächstes muss das Array initialisiert werden, d.h. wir bestimmen wie viele Werte das Array umfassen soll. Dies geschieht mithilfe eines neuen Begriffs in Processing, dem [[processing-reference:new]]. Mithilfe von *new* erzeugen wir ein 'neues' Array an *float*-Werten, in das wir ab sofort Werte speichern können. Als letztes geben wir noch die Anzahl an Werten an, die in dem Array gespeichert werden sollen. Die gesamte Zeile sieht dann wiefolgt aus:

```processing
// deklariere und erzeuge ein float-Array mit 5 Werten
float[] pos = new float[5];
```
Die '5' innerhalb der zweiten eckigen Klammern bezieht sich also auf die 5 *float*-Werte die ab sofort in dem Array gespeichert werden können.

#### Schreiben und Lesen
In einem so initialisierten Array können also ab sofort Werte gespeichert und ausgelesen werden. Dabei hat jeder Wert einen eigenen Index - beginnend bei 0 - über den auf den Wert an der jeweiligen Stelle zugegriffen werden kann.
Beim Zugriff auf das Array werden wieder die eckigen Klammern benutzt:

```processing
/* Deklarieren und Erzeugen eines float-Array mit 
 * der Möglichkeit 5 Werte ablegen zu können
 */
float[] pos = new float[5];

/* Befüllen des Arrays mit Werten. Beginnend bei 0. 
 * Das letzte Feld im Array sprechen wir deswegen 
 * mit Länge-1 an. Array mit 3 Feldern --> 3-1 = 2
 */
pos[0] = 1.2; // speichere den Wert '1.2' an der ersten Stelle
pos[1] = -2.5; // speichere den Wert '-2.5' an die zweite Stelle
pos[2] = 12.5; // speichere den Wert '12.5' an die dritte Stelle

// Auslesen des ersten Wertes, Ausgabe in der Konsole
println (pos[0]);
```

Ausserdem gibt es die Mölichkeit Arrays mit festen Werten zu erzeugen. Dazu werden sie nach der Deklaration in geschweiften Klammern, getrennt durch Kommata, geschrieben. Damit ersparen wir uns die Zeilen für das Befüllen des Arrays, können unseren Quelltext aber schlechter lesen:
```processing
/* Erstelle ein float-Array mit drei Feldern und befülle 
 * diese sofort mit den Werten '1.2', '-2.5' und '12.5'.
 */
float[] pos = {1.2, -2.5, 12.5};

// gibt '12.5' in der Konsole aus
println (pos[2]);
```

Unter Verwendung dieser Schreibweise sieht das obere Beispiel nun wiefolgt aus:

```processing
// Zeicheneinstellungen
fill (0);
stroke (0);

// Varaibel für die Quadratgröße
float rSize = 20.0;
// float-Array mit Position der Rechtecke
float[] pos = {0.0, 20.0, 40.0, 60.0, 80.0};

/* Zeichnen der Rechtecke, x- und y-Position 
 * wird dabei dem Array 'pos' entnommen und 
 * jeweils für beide Achsen eingesetzt.
 */
rect(pos[0], pos[0], rSize, rSize);
rect(pos[1], pos[1], rSize, rSize);
rect(pos[2], pos[2], rSize, rSize);
rect(pos[3], pos[3], rSize, rSize);
rect(pos[4], pos[4], rSize, rSize);
```

#### Größe
Jedes Array bietet die Möglichkeit über die Eigenschaft ''length'' seine Größe abzufragen. Die Schreibweise dazu sieht wiefolgt aus:

```processing
float[] pos = {0.0, 20.0, 40.0, 60.0, 80.0};
println (pos.length); // gibt '5' in der Konsole aus
```

Die Länge eines Arrays ist demnach eine Eigenschaft auf die mit der Punkt-Schreibweise zugegriffen werden kann (wie z.B. ''width'' oder ''height'' von Bildern, als ''img.width''). 

#### Rechenoperationen
Modifizieren und Neudefinieren von Werten erfolgt bei Werten innerhalb eines Arrays wie bei den uns bekannten einfachen Variablen. Links des Istgleich (=) befindet sich das Feld, wessen Wert wir ändern wollen. Bei einer Variable war dies die Nennung dieser durch den Variablennamen. Um ein Feld in einem Array anzusprechen, bedienen wir uns, wie oberhalb bereits erwähnt, der eckigen Klammern.

```processing
float[] pos = {0.0, 20.0, 40.0};

/* legt die Summe aus Feld zwei 
 * und drei in Feld eins ab.
 */
pos[0] = pos[1] + pos[2];

/* definiert den Wert des dritten Feldes 
 * mit dem Wert '91.41' neu
 */
pos[2] = 91.41;

/* definiert den Wert des zweiten Feldes 
 * mit einem Viertel des dritten Feldes neu
 */
pos[1] = pos[2] / 4; 
```

#### Arrays und for-Schleifen
Die häufigste Verwendung dieser Eigenschaft findet sich bei der Bearbeitung von Arrays mit Hilfe von *[[lesson:11#for_schleife|for]]*-Schleifen. Um ein Array, unabhänig vom Datentyp, einmal vollständig von Beginn bis Ende durchzulaufen sieht diese Schleife vom Aufbau immer gleich aus:
  - Da der Wert immer im null'ten Feld abgelegt wird, startet unsere Zählvariable ''i'' bei 0
  - Wir wollen bis zum letzten Wert vordringen, benötigen deswegen die Anzahl von [[lesson:11|Schleifendurchläufen]] wie unser Array Felder hat. Informatiker zählen, damit es nicht langweilg wird von 0 an - dem müssen wir uns beugen. Die Schleife läuft deshalb solange ''i'' kleiner als die Anzahl ist. Unseren letzten Wert erreichen wir mit Arraylänge - 1.
  - Die Zählvariable muss nach jedem Schleifendurchlauf um 1 erhöht werden um kein Feld des Arrays auszulassen.
Alle drei Regeln kombiniert ergeben folgende Vorlage:

```processing
int[] array = {"Alles", "aus", "der", "Liste"};

for (int i=0; i < array.length; i = i + 1) {
    print (array[i] + " ");
}
```

Im folgenden Beispiel wenden wir das Muster in zwei Formen an. Zuerst füllen wir jedes Feld des Arrays mit einem zufälligen Wert zwischen 0 und der Breite unseres Sketchfensters. Danach durchlaufen wir es ein zweites Mal und Positionieren unsere Quadrate an den durch [[lesson:13#random|random()]] festgelegten Positionen.

```processing
fill(0);
stroke(0);

float rSize = 20.0;
// deklariere und initialisiere das Array
float[] pos = new float[5];

/* Gehe mit Hilfe einer for-Schleife durch jede einzelne 
 * Position des Arrays. Das Ende der for-Schleife wird 
 * über die Länge-Eigenschaft des Arrays bestimmt.
 */
for (int i=0; i < pos.length; i++) {
  pos[i] = random(width);
}

// zeichne die Rechtecke nach dem selben Prinzip
for (int i=0; i < pos.length; i++) {
  rect(pos[i], pos[i], rSize, rSize);
}
```

#### Array Beispiele
[[example:21]]

[[example:22]]

[[example:23]]