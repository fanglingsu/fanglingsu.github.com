---
title: Variablen
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Variablen

# PHP Variablen

## Namensschema

Alle Variablen beginnen mit einem `$` gefolgt von Buchstaben, Zahlen und
Unterstrichen und sind Casesensitiv. Allerdings darf nach dem `$` nicht
direkt eine Zahl folgen!

Um Variable als Referenz zu übergeben oder zuzuweisen wird eine `&` der
Variablen vorangestellt.

{% highlight php %}
<?php
$a = 1;
$b = &$a;
$a = 7;
echo $b;    // 7
{% endhighlight %}

## Datentypen & Typumwandlungen

### Boolean

Werten, die beim der Umwandlung in Boolean zu `false` werden:
- integer 0
- float 0.0
- der Leerstring oder String "0"
- ein leeres Array
- `null`
- !SimpleXML Objekte die aus leeren Tags erzeugt wurden
- Alle Resourcen werden bei der Umwandlung zu Boolean `true`


### Integer

Die Größe von Integern ist Plattformabhängig und kann über die Konstanten
`PHP_INT_SIZE` und `PHP_INT_MAX` abgefragt werden. Auf 32 Systemen ist letztere
Konstante 2 147 483 647.

Integer können dezimal (100), oktal (0144) oder hexadezimal (0x64) notiert
werden. Wird ein Integer zu groß, so wird er automatisch nach Float gecastet.
- Leerstring, "0", "bla" casten zu 0, Strings die mit Zahlen beginnen werden
  zu diesen Zahlen konvertiert "24-Tage" wird zu 24, dagegen wird aus "Tag 24"
  0
- Float wird beim Integer Cast immer abgerundet, so wird aus 2.98 Float 2. Zu
  beachten ist, dass es keine Warnung oder Fehlermeldung gibt, wenn ein Float
  der außerhalb des Integer Bereiches liegt umgewandelt wird, so wir aus 20e57
  stillschweigend 0!
- Arrays werden zu 0 wenn sie leer sind und zu 1 wenn sie Elemente besitzen.
- Objekte können nicht nach Integer gecastet werden (`E_NOTICE`)
- `null` wird zu 0


### Float (Double)

Der Wertebereich für Fliesskommawertes ist plattformabhängig, allerdings ist ein
maximaler Wert von ca. 1.8e308 mit einer Genauigkeit von ca. 14
Nachkommastellen (entsprechend dem 64bit IEEE-Format) üblich.

- die Strings "", "0", "bla" werden zu Float `0` gecastet ansonsten gilt wie
  bei den Integern, dass führende Floats oder Integer aus Strings übernommen
  werden, das gilt auch wenn noch vor den Zahlen Whitespace ist. So wird aus
  "2.8" als auch aus "  2.8" Float `2.8`, dagegen aber aus "eine 2.1" Float
  `0`.
- alle anderen Datentypen werden zuerst nach Integer umgewandelt und von da
  aus weiter nach Float (siehe Integer).


### Strings

Strings sind beliebig lang und können auch Binärdaten beinhalten. Es gibt 4
Arten Strings zu deklarieren, Singelquoted, Doublequoted, Heredoc Syntax oder
Nowdoc Syntax (geht auch für Klassenvariablen).

Auf Zeichen eines Strings lässt sich auch mit der Arraynotation zugreifen.

{% highlight php %}
<?php
$a    = 'car';
$a[0] = 'b';
echo $a;        // "bar"
{% endhighlight %}

In Heredoc Syntax oder Doublequoted werden Variablen im String und
Backslashsequenzen ersetzt.

{% highlight php %}
<?php
echo "mail\100domain\x2ede" // "mail@domain.de"
{% endhighlight %}

### Array

Array Keys dürfen nur aus Strings oder Integern bestehen! Entspricht ein
String Key einem Integer so wird er als Integer verwendet (aus
`array("5" => "test")` wird `array(5 => "test")`).

- Strings, Integer und Floats werden beim Array-Cast zu einem Array mit dem
  entsprechendem Value, also aus 5.3 wird array(0 => 5.3), bei Objekten bleibt
  das Array aber leer!


### Objekt

Objekte werden in PHP seit Version 5 nicht mehr selbst in Variablen
gespeichert, sondern nur noch eine Objektbezeichner, der bei Objektzugriffen
die Identifizierung des Objekts ermöglicht. Bei der Übergabe werden keine
Aliase verwendet sondern die Objektbezeichner kopiert.

{% highlight php %}
<?php
$a = new A;
$copyA = $a;
$copyA = 3;     // $a ist noch immer eine Instanz von A

$b = new B;
$copyB = &$b;
$copyB = 3;     // 3 === $b
{% endhighlight %}

- Objekte, die nicht die `__toString()` Methode implementieren können nicht in
  skalare Werte umgewandelt werden (`Fatal Error`)
- Skalare Werte werden beim Typecast zu Objekten des Typs `stdClass`

{% highlight php %}
<?php
$string = 'foo';
$object = (object)$string;
echo $object->scalar;           // "foo"

var_dump($string == $object);   // "bool(false)"
{% endhighlight %}

### Ressource

Eine Resource ist eine spezielle Variable, die eine Referenz zu einer externen
Ressource wie geöffnete Dateien, Datenbankverbindungen, Grafikbereiche usw.
darstellt. Eine Typkonvertierung ist nicht sinnvoll.

Sind in PHP keine Referenzen auf eine Resource mehr vorhanden, so werden diese
automatisch vom Garbagecollector freigegeben, außer persistente
Datenbankverbindungen, welche *nicht* freigegeben werden.

### NULL

Die Groß- und Kleinschreibung dieses Wertes ist nicht wichtig. Null sind alle
Variable,
- denen Null zugewiesen wurden,
- die noch keinen Wert zugewiesen bekamen
- oder solche, welche mittels `unset()` gelöscht wurden.

Die Umwandlung einer Variable auf den Typ null entfernt die Variable und
löscht ihren Inhalt!

