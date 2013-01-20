---
title: Namensräume
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Namensräume

# PHP Namensräume oder Namespaces

- toc
{:toc}

PHP-Namespaces bieten eine Möglichkeit, um zusammengehörige Klassen, Funktionen
und Konstanten zusammenzufassen und Namenskollisionen zu vermeiden. Außerdem
werden dadurch Lange Funktions-, Klassen- und Konstantennamen vermieden, was
den Code lesbarer macht.

## Namespaces definieren

Namespaces werden mit dem Schlüsselwort `namespace` definiert.

- Der Namespace muss am Anfang der Datei stehen vor allem anderen Code stehen.
  Einzige Ausnahme ist `declare` welches die Ausführungsdirektive `encoding`
  für den Codeblock festlegt.
- Vor dem Namespace darf kein Nicht-PHP-Code stehen.
- Am besten nur einen Namespace je Datei definieren (Best Practice)
- Ist kein Namespace angegeben gilt der Globale-Namensraum
- Hierarchien können durch `\` im Namespace abgebildet werden, ähnlich wie man
  es von Dateisystemen kennt (ein einzelnes `\` kennzeichnet so den
  Globale-Namensraum).

{% highlight php %}
<?php
declare(encoding='UTF-8');
namespace de\domainname\package\subpackage;

const TESTMODE=1;
class Foo { }
function bar() { }
{% endhighlight %}

## Namespaces verwenden

{% highlight php %}
<?php
namespace Foo\Bar;

class foo { }

// Globale Funktion
\print('baz');

// Unqualifizierter Name
foo();                              // wird zu Foo\Bar\foo aufgelöst

// Qualifizierter Name
subnamespace\foo();                 // wird zu Foo\Bar\subnamespace\foo aufgelöst
                                  
// Vollständig qualifizierter Name
\Foo\Bar\foo();                     // wird zu Foo\Bar\foo aufgelöst

// Dynamische Verwendung
$className = 'subnamespace\foo';
$instance = new $className;
{% endhighlight %}

## Die Verwendung der Konstanten `__NAMESPACE__`

{% highlight php %}
<?php
// alternative Schreibweise und einzig Mögliche um den globalen Namespace in
// einer Datei mit anderen Namenspaces zu verwenden
namespace {
    // hier gilt der Namespace Global
    echo __NAMESPACE__;             // ""
}
namespace Foo\Bar {
    echo __NAMESPACE__;             // "Foo\Bar"

    $className = 'MyClass';
    $fullName  = __NAMESPACE__ . '//' . $className;
    $instance  = new $fullName;
}
{% endhighlight %}

## Importieren und Aliassen

PHP-Namespaces unterstützen drei Arten von Aliassen oder Importen:
- Alias für einen Klassennamen
- Alias für einen Interfacenamen
- Alias für einen Namespace

Das importieren einer Funktion oder Konstanten wird nicht unterstützt.

{% highlight php %}
<?php
namespace foo;
use Foo\Bar\ClassName as MyClass

// gleichbedeutend mit use Other\Full\NamespaceName as NamespaceName;
use Other\Full\NamespaceName;

// Objekt Foo\Bar\ClassName
$object = new MyClass();

// Objekt foo\ClassName
$object = new namespace\ClassName();

// Objekt Other\Full\NamespaceName\SubNamespace\Class
$object = new NamespaceName\SubNamespace\Class();
{% endhighlight %}

Importieren wird zur Kompilierungszeit ausgeführt und hat daher keinen
Einfluss auf dynamische Klassen-, Funktions- oder Konstantennamen.

{% highlight php %}
<?php
use My\Full\Classname as Another;

$a   = 'Another';
$obj = new Another; // Objekt der Klasse My\Full\Classname
$obj = new $a;      // Objekt der Klasse Another
{% endhighlight %}

Zusätzlich beeinflusst das Importieren nur unqualifizierte und qualifizierte
Namen. Vollständig qualifizierte Namen sind absolut und werden von Importen
nicht beeinflusst.

{% highlight php %}
<?php
use My\Full\Classname as Another;

$obj = new Another\thing;   // Objekt der Klasse My\Full\Classname\thing
$obj = new \Another\thing;  // Objekt der Klasse Another\thing
{% endhighlight %}

Importregeln sind auf Dateibasis gültig, das heißt eine eingebundene Datei
wird *nicht* die Importregeln der einbindenden Datei erben.

## Regeln für Namensauflösung

- Aufrufe von _vollständig qualifizierten Namen_ (Klassen, Funktionen und
  Konstanten) werden zur Kompilierungszeit aufgelöst.  `New \A\B` wird z. B.
  zur Klasse `A\B` aufgelöst.
- Alle nicht _vollständig qualifizierte Namen_ werden gemäß den aktuellen
  Importen zur Kompilierungszeit übersetzt.  Wenn zum Beispiel der Namespace
  `A\B\C` als `C` importiert wurde, so wird ein Aufruf von `C\D\e()` zu
  `A\B\C\D\e()` übersetzt.
- Innerhalb eines Namespace wird allen _qualifizierten Namen_, die noch nicht
  gemäß den Importregeln übersetzt wurden, der aktuelle Namespace
  vorangestellt.  Wenn z. B. `C\D\e()` innerhalb des Namespace `A\B`
  aufgerufen wird, so wird dies zu `A\B\C\D\e()` übersetzt.
- _Unqualifizierte Klassennamen_ werden zur Kompilierungszeit gemäß der
  aktuellen Importregeln (vollständige Namen ersetzt durch kurze Aliasnamen)
  übersetzt.  Z. B. wenn der Namespace `A\B\C` als `C` importiert wurde, so
  wird `new C()` zu `new A\B\C()` übersetzt.
- Innerhalb eines Namespace (z. B. `A\B`) werden Aufrufe von _unqualifizierten
  Funktionen_ zur Laufzeit aufgelöst. Der Aufruf der Funktion `foo()` wird wie
  folgt aufgelöst:
  - Zuerst wird nach der Funktion im aktuellen Namespace gesucht: `A\B\foo()`.
  - Es wird versucht, die Funktion `foo()` im globalen Namensraum zu finden.
- Innerhalb eines Namespace (z. B. `A\B`) werden Aufrufe von _nicht
  vollständig qualifizierte Klassennamen_ zur Laufzeit aufgelöst. Der Aufruf
  von `new C()` oder `new D\E()` wird wir folgt aufgelöst.
  - Für `new C()`:
    # Zuerst wird nach der Klasse im aktuellen Namespace gesucht: `A\B\C`.
    # Es wird versucht, die Klasse `A\B\C` mittels Autoload zu laden.
  - Für `new D\E()`:
    - Es wird nach der Klasse gesucht, indem der aktuelle Namespace
      vorangestellt wird: `A\B\D\E`.
    - Es wird versucht, die Klasse `A\B\D\E` mittels Autoload zu laden.
