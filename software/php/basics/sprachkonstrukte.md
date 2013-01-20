---
title: Sprachkonstrukte und Funktionen
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Sprachkonstrukte und Funktionen

# PHP Sprachkonstrukte und Funktionen

Sprachkonstrukte sind in PHP z. B. `if`, `else`, `elseif`, `for`, `do`,
`while`, `foreach`, `switch`, `include`, `include_once`, `require`,
`require_once`, `die`, `exit`, `echo`, `return`, `declare()`,
`unset()`, `list()` etc.

Im Gegensatz zu Funktionen haben Sprachkonstrukte keine Rückgabewerte, wodurch
man sie an einigen Stellen nicht benutzen kann.

{% highlight php %}
<?php
$var = true;
$var == true ? echo 'true' : echo 'false';      // Parse Error
$var == true ? print('true') : print('false');  // "true"

var_dump(echo 'foo');                           // Parse Error
var_dump(print('foo'));                         // "fooint(1)"
{% endhighlight %}
