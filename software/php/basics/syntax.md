---
title: Basics
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Syntax

# PHP Syntax

## Tags

In PHP 5.3 sind nur noch `<?php ?>` und `<script language="php"></script>`
erlaubt, allerdings kann in der _php.ini_ auch auf Short-Tags zurückgestellt
werden `<? ?>` oder `<?= ?>`, dies sollte aber vermieden werden, genauso
wie Tags im ASP Stil `<% %>`.

## Kommentare

PHP unterstützt `C/C++` und Unix-Shell-artige (Perl-artige) Kommentare.

{% highlight php %}
<?php
echo 'Test'; // einzeiliger Kommentar im C++-Stil
/*
  Dies ist ein mehrzeiliger Kommentar
  noch eine weitere Kommentar-Zeile
*/
echo 'Test'; # einzeiliger Shell-Kommentar
{% endhighlight %}
