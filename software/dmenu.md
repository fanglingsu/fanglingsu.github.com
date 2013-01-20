---
title: Dmenu
layout: default
---
[Home](/) > [Software](/software/index.html) > Dmenu


# Dmenu

Dmenu ist ein kleiner flinker Programmstarter aus dem
[Suckless](http://suckless.org) Projekt. Eigentlich ist es nicht nur ein
Programmstarter, sondern ein Tool um aus beliebigen Textinput `stdin` ein Menü
zu erzeugen. Dieses Menü kann man durch weitere Texteingaben filtern und
Einträge mit den Cursor-Tasten auswählen, die dann nach `stdout` geschrieben
werden. Mit den aus gegebenen Text kann man dann verschiedene Aktionen
antriggern und so auch Programme starten.

Für das Starten von Programmen wird auch gleich ein Wrapper-Script
mitgeliefert (`dmenu_run`). Dieses Script generiert ein Cache-File mit allen
in `$PATH` befindlichen Programmen, und schickt dieses über `stdin` in dmenu.
Die Ausgabe, die von dmenu durch filtern auf `stdout` geschrieben wird, wird
einfach in die Shell gepiped und ausgeführt.

So sieht das Standard `dmenu_run` Wrapperscript aus.

{% highlight sh %}
#!/bin/sh
cachedir=${XDG_CACHE_HOME:-"$HOME/.cache"}
if [ -d "$cachedir" ]; then
    cache=$cachedir/dmenu_run
else
    cache=$HOME/.dmenu_cache # if no xdg dir, fall back to dotfile in ~
fi
(
    IFS=:
    if stest -dqr -n "$cache" $PATH; then
        stest -flx $PATH | sort -u | tee "$cache" | dmenu "$@"
    else
        dmenu "$@" < "$cache"
    fi
) | ${SHELL:-"/bin/sh"} &
{% endhighlight %}


## Sortiere nach Häufigkeit

![Menü mit dmenu_run_recent erzeugt](/media/dmenu_run_recent.png)

Standardmäßig sortiert `dmenu_run` die Programme rein alphabetisch. Hat man
viele Programme, deren Name mit vim beginnt, dann muss man relativ viel
filtern, bis man das gewünschte Programm ausgewählt hat. Deshalb habe ich mich
entschlossen, diejenigen Programme, die ich häufiger verwende gleich oben an zu
listen.

Zusätzlich dazu kann man noch Programme mit anschliessendem ";" aufrufen, dies
führt dazu, dass das Programm in einem Terminal Fenster gestartet wird.
Das ist besonders dann hilfreich, wenn `dmenu` nicht von einem Terminal
gestartet wird und sich so CLI-Programme nicht richtig starten liessen. Das is
zum Beispiel der Fall wenn dmenu per Shortcut des Windowmanagers gestartet
wird (META-p bei [xmonad](http://xmonad.org/)).

Mein Script `dmenu_run_recent`.

{% highlight sh %}
#!/bin/bash
TERM="urxvtc -e"

cachedir=${XDG_CACHE_HOME:-"$HOME/.cache"}
if [ -d "$cachedir" ]; then
    mostused=$cachedir/dmenu_cache_recent
    cache=$cachedir/dmenu_cache
else
    # if no xdg dir, fall back to dotfile in ~
    mostused=$HOME/.dmenu_cache_recent
    cache=$HOME/.dmenu_cache
fi

IFS=:
if stest -dqr -n "$cache" $PATH; then
    stest -flx $PATH | sort -u > "$cache"
fi

touch $mostused
mostused_data=$(sort $mostused | uniq -c | sort -nr | colrm 1 8)
run=$((echo "$mostused_data"; cat $cache | grep -vxF "$mostused_data") | dmenu ${1+"$@"}) \
    && (echo "$run"; head -n 99 "$mostused") > $mostused.$$ \
    && mv $mostused.$$ $mostused

IFS=$" "
case $run in
    *\;) exec $(echo $TERM ${run/;/}) ;;
    *)   exec $run ;;
esac
{% endhighlight %}

Durch das `dmenu ${1+"$@"})` werden die übergebenen Optionen direkt an `dmenu`
weitergegeben, so dass man das Menü direkt anpassen kann.

Mit folgender Zeile kann man dann ein Menü wie es im obigen Bild zu sehen ist
generieren.

`~/bin/dmenu_run_recent -f -l 7 -nb '#000' -nf '#ccc' -sb '#070' -sf '#fff' &`


## Links

Wer auf den Geschmack gekommen ist sollte sich unbedingt den
[Dmenu-Hacking-Thread](https://bbs.archlinux.org/viewtopic.php?id=80145) auf
archlinux.org ansehen. Da sieht man mal wider wie flexible man Tools
kombinieren kann, die der Unix-Philosophie folgen.

> Write programs that do one thing and do it well. Write programs to work
> together. Write programs to handle text streams, because that is a
> universal interface.
