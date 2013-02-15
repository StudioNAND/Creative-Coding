# Zufall und Rauschen
## random & noise

> Stellt die Befehle random() und noise() vor und erläutert anhand einfacher Beispiele ihre Unterschiede.

---

=== random ===

Für Anzahl, Farbe, Form und Position die Würfel fliegen lassen.

  * **random(a)** erzeugt eine Zufallszahl zwischen 0 und //a//, wobei //a// eine rationale oder gebrochen rationale Zahl sein kann. Bei dieser Parameteranzahl legen wir demnach nur die Obergrenze des möglichen Wertebereiches fest. Die Untergrenze ist durch Processing auf 0 gesetzt.

[code|processing]
// z.B.: 0.8751683
println (random (1));
[/code]

  * **random(a, b)** erzeugt eine Zufallszahl zwischen //a// und //b//, wobei //a// und //b// rationale oder gebrochenrationale Zahlen seien können. Beide, Unter- und Obergrenze, werden von uns festgelegt.

[code|processing]
// z.B.: 3.9300842
println (random (1, 10);
[/code]

Als Ergebnis liefert uns die [[processing-reference:random()]] Funktion immer einen gebrochen rationalen Wert. Das Befüllen eines //int// mit dem Resultat ist uns demnach nicht gestattet - wir müssen den Datentyp //float// verwenden.

====== Bsp.: random 1 ======

[code|processing]
void setup () {
  size(200, 200);
}

void draw () {
  ellipse (100, 100, random (200), random (200));
}
[/code]

In jedem Einzelbild (einem [[lesson:10#vorbereitung_fortlaufende_programme|draw()]] Durchlauf) wird eine [[lesson:9#ellipse|Ellipse]] gezeichnet. Breite und Höhe werden jedes Mal zufällig bestimmt - zwischen 0 und 200 Pixel. Eine Variable zur Zwischenablage der Zufallszahlen wird dabei nicht benötigt. Das Resultat der random() Funktion wird direkt als Parameter an die ellipse() Funktion weitergereicht.

====== Bsp.: random 2 ======

[code|processing]
void setup () {
  size(200, 200);
}

void draw () {
  // erstelle eine Variable "durchmesser"
  // und lege in ihr einen zufälligen Wert
  // zwischen 0 und 200 ab
  float durchmesser = random (200);

  // zeichne einen Kreis in die Mitte der
  // Zeichenfläche - verwende für Breite
  // und Höhe den Wert der Variable "durchmesser"
  ellipse (100, 100, durchmesser, durchmesser);
}
[/code]

Im zweiten Beispiel erzeugen wir gleichförmige Kreise deren Durchmesser ebenfalls zufällig ist. Dies geht nur mittels Zuhilfenahme von einer [[lesson:35#datentypen|Variable]] deren Wert bei der Breite und Höhe der Ellipse verwendet wird. Beachte das sie vom Datentyp //float// zu sein hat. Da das Resultat des random() Aufrufs eine gebrochen rationale Zahl zurück gibt - //int// kann nur mit Ganzzahlen gefüllt werden.

====== Bsp.: random 3 ======

[code|processing]
void setup () {
  size(200, 200);
  // aktiviert Kantenglättung
  smooth ();
  // begrenzung der Einzelbilder pro
  // Sekunde auf 5 (besser für die augen)
  frameRate (5);
}

void draw () {
  background (255);

  // bestimmung der Kreisanzahl für
  // dieses Einzelbild (Maxima ist 40)
  float anzahl = random (40);

  // für jeden Kreis werden position
  // und Farbe neubestimmt
  for (int i=0; i < anzahl; i = i + 1) {
    // random Position auf der x-Achse
    float posX = random (width);
    // random Position auf der y-Achse
    float posY = random (height);

    // random Werte für alle drei Farbkanäle RGB
    fill (random (255), random (255), random (255));
    // zeichnen des Kreises an den vorher
    // ermittelten Koordinaten
    ellipse (posX, posY, 20, 20);
  }
}
[/code]

Bis auf die Abmaße haben wir im dritten Beispiel mit Anzahl, Position und Farbe fast alle möglichen Attribute in unserer simplen Darstellung vom Zufall bestimmt. Die Verwendung von random() ist also nicht automatisch ein Rezept für die Erstellung von hochwertigen Grafiken. Setze es mit Bedacht ein um geringe Abweichungen in deinem Arrangement zu generieren oder die Verteilung im Aufbau deines Programmes zu organisieren - für abwechslungsreiche Resultate.

=== noise ===

Im Gegensatz zu random() ist [[processing-reference:noise()]] eine kontrollierbarere Methode um Zufall zu erzeugen. Sie basiert auf der Theorie des [[http://en.wikipedia.org/wiki/Perlin_noise|Perlin Noise]], 1982 von Ken Perlin für den legendären Film [[http://en.wikipedia.org/wiki/Tron_(film)|Tron]] entwickelt.
random() führt die Bestimmung des Zufallswertest jedes Mal auf neue aus - unabhänig von vorherigen Ergebnissen. Dieser Aspekt unterscheidet beide Funktionen. noise() bezieht sich auf das Resultat des letzten Aufrufes und fügt ihm eine leichte Varianz hinzu. Auf dieser Grundlage werden in der Computergrafik natürlich wirkende [[http://toxi.co.uk/p5/noiseDetail/|Texturen]], [[http://toxi.co.uk/p5/perlin/|Gelände]] und [[http://toxi.co.uk/p5/perlin/filteredClouds/|Wolken]] generiert. Die Varianz verteilt sich auf eine bestimmte Anzahl von Funktionen die unterschiedliche Frequenzen und Amplituden besitzen. Durch Addition all dieser Wellen erhählt man ein harmonisches/gleichmäßiges Rauschen. [[http://freespace.virgin.net/hugo.elias/models/m_perlin.htm|Weiterführend]]

  * **noise(x)** Zufallszahl in eindimensionaler Abfolge.
  * **noise(x, y)** Zufallszahl in zweidimensionaler Abfolge, z.B. für eine 2d Textur.
  * **noise(x, y, z)** Zufallszahl in dreidimensionaler Abfolge, z.B. für eine räumlichen Wolke.
  * **noiseDetail(octaves)** definiert die Anzahl an Wellen die addiert das Rauschen ergeben. Je größer die Anzahl - umso feiner die Varianz. Processing arbeitet standardmäßig mit vier Oktaven.

====== Bsp.: random() vs. noise() ======

[code|processing]
size(600, 170);
background (255);
noStroke ();
fill (0);

float v = 0;
for (int i=0; i < width; i += 3) {
  float n = 90 + noise (v) * 40;
  rect (i, n, 2, 20);
  v = v + 0.15;
}

for (int i=0; i < width; i += 3) {
  float r = random (10, 30);
  rect (i, r, 2, 20);
}
[/code]