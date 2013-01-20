---
title: Vimprobable
layout: default
---
[Home](/) > [Projekte](/projects/index.html) > Vimprobable

# Vimprobable

Vor ungefähr einem Jahr bin ich auf ein sehr interessantes Browser Projekt
gestoßen, Vimprobable.

[Vimprobable][] ist an an das Firefox Plugin `Vimperator` oder
`Pantadactyl` angelehnter Browser auf Webkit Basis. Vimprobable vereint die
Performance und Resourcensparsamkeit von Kommandozeilenbrowsern wie Lynx und
w3m mit den Fähigkeiten moderner grafischer Browser und der Bedienbarkeit des
beliebten Editors Vim.

Es gib zwei Versionen des Browsers, Vimprobable und Vimprobable2. Ersterer
lässt sich nur über die Einstellungen in der `config.h` konfigurieren und ist
deshalb etwas schlanker als sein umfangreicherer großer Bruder Vimprobable2.
Dieses kann über eigene Konfigurationsdateien (z. B.
`$XDG_CONFIG_HOME/vimprobable/vimprobablerc`) und zur Laufzeit über `:set` und
`:map` Kommandos angepasst werden.

Im Gegensatz zu manchen anderen auch sehr schlanken Browsern, unterstützt
Vimprobable kein Tabbing. Das ist aber kein Nachteil, sondern Teil der
Philosophie.

> Managing windows is a window manager's job. Vimprobable is not one. Any
> fullscreen or tiled WM will provide the features you are looking for
> natively.

Jedes Fenster is von den anderen unabhängig und kann unabhängig von diesen
konfiguriert werden. Tabbing kann man aber dennoch durch den Windowmanager
erreichen, oder durch ein kleines Programm wie
[Tabbed][] in dem man Vimprobable startet.
Dann wird jedes neue Fenster, dass man durch den Browser öffnet als neuer Tab
in tabbed angezeigt.

Eine Besonderheit beim browsen mit Vimprobable ist das sogenannte Hinting,
womit Links, und je nach Verwendung auch Bilder und Frames, mit Zahlen
gekennzeichnet werden. Anschließend kann man entweder mithilfe der Zahlen die
Links aktivieren oder weiter filtern, oder aber man aktiviert das Hinting und
Tippt dann ein Paar Buchstaben des Links, und schon wird dieser geöffnet.

![Vimprobale Hinting][img-hint]


## Keybindings

Keybindings für das Browsen mit Vimprobable.

| Kommando | Aktion                                                         |
|----------|----------------------------------------------------------------|
| o        | öffne URL in gleiches Fenster                                  |
| O        | öffne URL in gleiches Fenster - aktuelle URL ist vorausgefüllt |
| t        | öffne URL in neues Fenster                                     |
| T        | öffne URL in neues Fenster - aktuelle URL ist vorausgefüllt    |
| p        | öffne URL aus Zwischenablage                                   |
| P        | öffne URL aus Zwischenablage in neues Fenster                  |
| u        | öffne zuletzt geschlossene Seite                               |
| q{1-9}   | öffne Quickmark werden mit `:set qmark={1-9}` gesetzt          |
| <C-o>    | zurück                                                         |
| <C-p>    | vorwärts                                                       |
| gh       | öffne Startseite                                               |
| gH       | öffne Startseite in neuem Fenster                              |
| {num}gu  | gehe {num} Verzeichnisse höher                                 |
| gU       | gehe in das Root-Verzeichnis                                   |
| f        | folge Link                                                     |
| F        | folge Link in neues Fenster                                    |
| gi       | focusiere nächstes Inputfeld                                   |
| r        | lade Seite neu                                                 |
| R        | lade Seite neu - erzwungen                                     |
| <C-c>    | stoppt das laden der Seite                                     |
| d        | schließt das Fenster                                           |
| /        | suche                                                          |
| n        | nächster Suchtreffer                                           |
| N        | vorhergehender Suchtreffer                                     |

Bufferbezogen Keybindings.

| Kommando     | Aktion                     |
|--------------|----------------------------|
| h,j,k,l      | wie in vim                 |
| <C-e>, <C-y> | zeilenweise scrollen       |
| <C-f>,<C-b>  | eine Fensterhöhe scrollen  |
| <C-d>,<C-u>  | halbe Fensterhöhe scrollen |
| zi           | Text vergrößern            |
| zI           | alles vergrößern           |
| zo           | Text verkleinern           |
| zO           | alles verkleinern          |
| zz           | zurück zum Standartzoom    |
| y            | kopiere aktuelle URL       |
| Y            | kopiere markierten Text    |

[vimprobable]: http://sourceforge.net/apps/trac/vimprobable/
[tabbed]:      http://tools.suckless.org/tabbed
[img-hint]:    /media/vimprobable_hinting.png "Vimprobale Hinting"
