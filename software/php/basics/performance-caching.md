---
title: Performace und Bytecodecaching
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) >  Performace und Bytecodecaching

# PHP Performance und Bytecodecaching

## Speicherverbrauch reduzieren

Mit PHP 5.3 gibt es erstmals die Möglichkeit allokierten Speicher von zyklisch
referenzierten Objekten zur Laufzeit wieder freizugeben. Dabei wird der
Garage-Collector tätig wenn der Root-Puffer voll ist oder wenn die Funktion
[gc_collect_cycles()][gc] aufgerufen wird.

Allerdings verlangsamt sich die Scriptausführung wenn der Garage-Collector in
Aktion tritt um einige Prozent. Wenn er aber nicht gebraucht wird wirkt er
sich nicht auf die Performance aus.

Der neue Garbage-Collector ist daher vor allem für lange laufende Scripte,
Daemonscripte, Testsuiten und PHP-GTK Anwendungen sinnvoll.


## Links

- [Performancebetrachtungen PHP.net][perf]


[gc]:   http://www.php.net/manual/de/function.gc-collect-cycles.php
[perf]: http://php.net/manual/en/features.gc.performance-considerations.php
