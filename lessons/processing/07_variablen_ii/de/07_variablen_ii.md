# Variablen II
## Variablen und ihre Sichtbarkeit

> Erläutert den Unterschied zwischen lokalen und globalen Variablen und warum lokale Variablen dabei helfen, Fehler vorzubeugen.

---

=== Gültigkeit von Variablen ===

Um die Verwendung von Variablen zu strukturieren gelten diese stets nur für einen bestimmten Bereich des Programms - einem Block. Blöcke werden durch geschweifte Klammern gebildet. Das bedeutet, dass [[lesson:10#vorbereitung_fortlaufende_programme|setup(), draw()]], [[lesson:37#mausinteraktion|mousePressed()]], etc. als auch //if//-Abfragen und //[[lesson:11#for_schleife|for]]//-Schleifen eigene Blöcke bilden.\\ 
Das folgende Bild zeigt die Blockstruktur an einem Beispiel.

Variablen können in all diesen Blöcken deklariert und verwendet werden, und sind von dort an nur innerhalb des selben Blocks, sowie Blöcken eines niedrigeren Levels innerhalb dieses Blocks verfügbar. Dieses Konzept nennt man »Gültigkeit von Variablen«.

[code|processing]
int zahl = 20;

void setup() {
  size(200, 200);
  background(255);
  ellipse(100, 100, zahl, zahl);
}

void draw() {
}

void mousePressed() {
  ellipse(mouseX, mouseY, zahl, zahl);
}
[/code]

Hier ist ''zahl'' eine sogenannte Globale Variable, da sie im obersten Block initialisiert wurde und demzufolgen in allen unterliegenden Blöcken verfügbar ist. "Lokale" Variablen sind demzufolge alle Variablen, die nicht global und somit in einigen Teilen des Programms nicht verfügbar sind.

[code|processing]
void setup() {
  int zahl = 5;
  println(zahl); // â€˜5â€™
}

void draw() {
  println(zahl); // Fehler! zahl 
}
[/code]

Globale Variablen können also für alle Funktionen des gesamten Programms verwendet werden, z.B. um verschieden Parameter im Programmverlauf mitzuzählen.

[code|processing]
int count = 0;

void setup() {
  size(100, 100);
  background(0);
  stroke(255);
}

void draw() {
  background(0);
  count = count + 1;
  line(0, count, 100, count); 

  if (count == 100) {
    count = 0;
  }
}
[/code]

Lokale Variablen werden vorzugsweise bei allen Aufgaben verwendet, die nur in einem kleinen Teil des Programms stattfinden und demzufolge in anderen Teilen nicht benötigt werden. Die Verwendung von lokalen Variablen wann immer es möglich ist, gehört zu einem guten Programmierstil und hilft Fehler zu vermeiden. Desweiteren haben lokale Variablen den Vorteil, das Namen in unterschiedlichen Blöcken mehrfach verwendet werden können.

[code|processing]
void setup() {
  size(200, 200);
}

void draw() {
  int zahl = 4;
  ellipse(random(200), random(200), zahl, zahl);
}

void mousePressed() {
  int zahl = 20;
  ellipse(mouseX, mouseY, zahl, zahl);
}
[/code]