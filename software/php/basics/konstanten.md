---
title: Konstanten
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Konstanten

# PHP Konstanten

Eine Konstante ist ein Bezeichner für einen einfachen Wert. Wie der Name
bereits nahelegt, kann der Wert einer Konstanten zur Laufzeit des Skripts
nicht verändert werden (ausgenommen die Magischen Konstanten, die aber keine
wirklichen Konstanten sind.)

Der Name einer Konstanten ist Casesensitiv und folgt den gleichen Regeln
wie alle anderen Bezeichner in PHP. Ein gültiger Name beginnt mit einem
Buchstaben oder einem Unterstrich, gefolgt von beliebig vielen Buchstaben,
Ziffern oder Unterstrichen. Als regulärer Ausdruck könnte das so beschrieben
werden: `[a-zA-Z_\x7f-\xff][a-zA-Z0-9_\x7f-\xff]*`

Der Gültigkeitsbereich von Konstanten die mit `define('NAME', 'value')`
definiert wurden ist `global`.

{% highlight php %}
<?php
if (!defined('CONST')) {
    define('CONST', 'bar');
}

echo CONST;                     // "bar"
echo constant('CONST');         // "bar"

interface Foo {
    const BAR = 'baz';
}

$const = 'BAR';
echo constant('Foo::'. $const); // "baz"
{% endhighlight %}

Neben diesen Konstanten gibt es noch sogenannte Magische-Konstanten der Form
`__XXX__`, die sich zur Laufzeit je nachdem wo sie benutzt werden verschieden
sind! Beispiele hierfür sind `__FILE__`, `__METHOD__`, `__LINE__` und so
weiter.
