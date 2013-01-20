---
title: Operatoren
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Operatoren

# PHP Operatoren

- toc
{:toc}

Die folgende Tabelle zeigt die Rangfolge der Operatoren, oben steht der
Operator mit dem höchsten Rang. Ist die Rangfolge der Operatoren gleich, wird
links nach rechts Assoziativität benutzt.

## Operatoren Typen

### Arithmetische Operatoren

| Beispiel | Name           | Ergebnis                      |
|----------|----------------|-------------------------------|
| $a + $b  | Addition       | Summe von $a und $b           |
| $a - $b  | Subtraktion    | Differenz von $a und $b.      |
| $a * $b  | Multiplikation | Produkt von $a und $b.        |
| $a / $b  | Division       | Quotient von $a und $b.       |
| $a % $b  | Modulus        | Rest von $a geteilt durch $b. |

### Zuweisungs-Operator

Der `=` Zuweisung-Operator kopiert den Inhalt des Ausdrucks auf der rechten Seite
auf die Variable zur Linken.

### Bit-Operatoren

| Beispiel   | Name          | Ergebnis                                                                            |
|------------|---------------|-------------------------------------------------------------------------------------|
| $a & $b    | Und           | Bits, die in $a und $b gesetzt sind werden gesetzt.                                 |
| $a PIPE $b | Oder          | Bits, die in $a oder $b gesetzt sind werden gesetzt.                                |
| $a ^ $b    | Entweder oder | Bits, die entweder in $a oder $b gesetzt sind, werden gesetzt aber nicht in beiden. |
| ~ $a       | Nicht         | Die Bits, die in $a nicht gesetzt sind, werden gesetzt und umgekehrt.               |
| $a << $b   | Nach links    | Verschiebung der Bits von $a um $b Stellen nach links.                              |
| $a >> $b   | Nach rechts   | Verschiebt die Bits von $a um $b Stellen nach rechts.                               |

### Vergleich-Operatoren

| Beispiel  | Name            | Ergebnis                                                                        |
|-----------|-----------------|---------------------------------------------------------------------------------|
| $a == $b  | Gleich          | TRUE, wenn $a gleich $b ist.                                                    |
| $a === $b | Identisch       | TRUE, wenn $a gleich $b ist und beide vom gleichen Typ sind.                    |
| $a != $b  | Ungleich        | TRUE, wenn $a nicht gleich $b ist.                                              |
| $a <> $b  | Ungleich        | TRUE, wenn $a nicht gleich $b ist.                                              |
| $a !== $b | Nicht identisch | TRUE, wenn $a nicht gleich $b ist, oder wenn beide nicht vom gleichen Typ sind. |
| $a < $b   | Kleiner Als     | TRUE, wenn $a kleiner als $b ist.                                               |
| $a > $b   | Größer Als      | TRUE, wenn $a größer als $b ist.                                                |
| $a <= $b  | Kleiner Gleich  | TRUE, wenn $a kleiner oder gleich $b ist.                                       |
| $a >= $b  | Größer Gleich   | TRUE, wenn $a größer oder gleich $b ist.                                        |

### Fehlerkontroll-Operator

`@` Stellt man das @ in PHP vor einen Ausdruck werden alle Fehlermeldungen,
die von diesem Ausdruck erzeugt werden könnten, ignoriert.  Dies gilt nicht
für Parsingfehler.


### Operator zur Programmausführung

z. B. in `ls -l` entspricht `shell_exec('ls- l');`

### Increment- und Decrementopratoren

| Beispiel | Name           | Auswirkung                                                                                |
|----------|----------------|-------------------------------------------------------------------------------------------|
| ++$a     | Prä-Inkrement  | Erhöht den Wert von $a um eins und gibt anschließend den neuen Wert von $a zurück.        |
| $a++     | Post-Inkrement | Gibt zuerst den aktuellen Wert von $a zurück und erhöht dann den Wert von $a um eins.     |
| --$a     | Prä-Dekrement  | Vermindert den Wert von $a um eins und gibt anschließend den neuen Wert von $a zurück.    |
| $a--     | Post-Dekrement | Gibt zuerst den aktuellen Wert von $a zurück und erniedrigt dann den Wert von $a um eins. |

### Logische Operatoren

| Beispiel   | Name          | Ergebnis                                                  |
|------------|---------------|-----------------------------------------------------------|
| $a and $b  | Und           | TRUE wenn sowohl $a als auch $b TRUE ist.                 |
| $a or $b   | Oder          | TRUE wenn $a oder $b TRUE ist.                            |
| $a xor $b  | Entweder Oder | TRUE wenn entweder $a oder $b TRUE ist, aber nicht beide. |
| ! $a       | Nicht         | TRUE wenn $a nicht TRUE ist.                              |
| $a && $b   | Und           | TRUE wenn sowohl $a als auch $b TRUE ist.                 |
| $a PIPE $b | Oder          | TRUE wenn $a oder $b TRUE ist.                            |

### Zeichenketten-Operatoren

`.` Vereinigungsoperator; `.=` Vereinigungs-Zuweisungsoperator.

### Array-Operatoren

| Beispiel  | Name             | Ergebnis                                                                            |
|-----------|------------------|-------------------------------------------------------------------------------------|
| $a + $b   | Vereinigung      | Vereinigung von $a und $b.                                                          |
| $a == $b  | Gleichwertigkeit | TRUE für $a und $b mit gleichen Schlüssel- und Wert-Paaren.                         |
| $a === $b | Identität        | TRUE für $a und $b mit gleichen Schlüssel- und Wert-Paaren mit gleicher Reihenfolge |
| $a != $b  | Ungleichheit     | TRUE wenn $a nicht gleich $b ist.                                                   |
| $a <> $b  | Ungleichheit     | TRUE wenn $a nicht gleich $b ist.                                                   |
| $a !== $b | nicht identisch  | TRUE wenn $a nicht identisch zu $b ist.                                             |

### Typ-Operatoren

`instanceof` wird dazu verwendet um festzustellen, ob ein gegebenes Objekt
ein Objekt ist, das zu einer bestimmten Klasse oder Interface gehört.

## Operator-Rangfolge

| Assoziativität | Operator                                            |
|----------------|-----------------------------------------------------|
| keine          | new                                                 |
| rechts         | [                                                   |
| rechts         | ! ~ ++ -- (int) (float) (string) (array) (object) @ |
| links          | * / %                                               |
| links          | + - .                                               |
| links          | << >>                                               |
| keine Richtung | < <= > >=                                           |
| keine Richtung | == != === !==                                       |
| links          | &                                                   |
| links          | ^                                                   |
| links          | PIPE                                                |
| links          | &&                                                  |
| links          | PIPE                                                |
| links          | ? :                                                 |
| rechts         | = += -= *= /= .= %= &= ^= <<= >>=                   |
| rechts         | print                                               |
| links          | and                                                 |
| links          | xor                                                 |
| links          | or                                                  |
| links          | ,                                                   |

## Beispiele

{% highlight php %}
<?php
$a = 1;                         // int(1)
$b = null;                      // NULL
$c = isset($a) && isset($b);    // bool(false)
$d = (isset($a) and isset($b)); // bool(false)
$e = isset($a) and isset($b);   // bool(true) <- ($e = isset($a)) and isset($b)
                                //               ($e = true) and false
{% endhighlight %}

Vergleiche dazu auch [Logische Operatoren][lo].

{% highlight php %}
<?php
$a = 0;
$b = 'G';
$c = false;
echo $a == $b ? "true" : "false";   // true
echo $a == $c ? "true" : "false";   // true
echo $c == $b ? "true" : "false";   // false
{% endhighlight %}

{% highlight php %}
<?php
$a = 'y';
echo ++$a, ', ', ++$a, ', ', ++$a;  // z, aa, ab
{% endhighlight %}

Siehe dazu auch [Increment- Decrementoperatoren][io]

{% highlight php %}
<?php
echo "twe" . "lve";        // "twelve"
echo 1 . 2;                // "12"
echo 1.2;                  // 1.2
echo 1+2;                  // 3
{% endhighlight %}

[lo]: http://php.net/manual/de/language.operators.logical.php "Logische Operatoren"
[io]: http://www.php.net/manual/de/language.operators.increment.php "Increment- Decrementoperatoren"
