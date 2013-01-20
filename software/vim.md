---
title: Vim
layout: default
---
[Home](/) > Vim

# Vim

## Plugins

Für vim gibt es unzählige Plugin und Erweiterungen. Manche davon sind
nützlich und machen einem das Arbeiten mit vim angenehmer und schneller.

Für die, die noch nicht so viel Erfahrung im Umgang mit vim haben, empfehle
ich zuerst ohne Plugins zu starten und sich mit den Grundlagen der Navigation
und den Textobjekten vertraut zu machen. Wer zu schnell Plugins verwendet,
verpasst wahrscheinlich sich mit den unglaublichen Möglichkeiten zu befassen,
die vim schon bietet und erhöht sich die Lernkurve noch dadurch, dass er noch
das Plugin bedienen lernen muss.

Nebenbei bemerkt, ist es auch gut vim ohne Plugins zu beherrschen, falls man
mal auf einem Server oder einen anderen Fremden System einen nur nackten
vim zur Verfügung hat. Dann ist es gut, wenn man trotzdem zügig arbeiten kann.

Folgende Plugins verwendet ich zur Zeit:

[vim-pathogen][]
: vim-pathogen erlaubt es vim Plugins in eigene Verzeichnisse zu legen.
  Dadurch kann man sehr einfach Plugins hinzufügen und wieder entfernen.

[vim-fastwordcompleter][]
: vim-fastwordcompleter vervollständigt automatisch bereits verwendete Wörter
  beim schreiben. Es kann angegeben werden ab wie vielen Buchstaben je Wort die
  Vervollständigung gestartet wird.

[vimwiki][]
: vimwiki ist ein Wiki das man mit vim benutz welches die Seiten auch nach
  HTML exportieren kann. Ich verwende Vimwiki für diese Homepage und auch lokal
  um mir strukturiert Notizen und Dokumentationen zu machen.

[vimoutliner][]
: vimoutliner ist ein klassischer Outliner. Momentan verwende ich ihn um auf
  Arbeit meine Arbeitszeiten zu verwalten und meine Arbeitsstunden wochen,
  monats- und jahresweise auf zu summieren.

[snipmate][]
: snipmate verwaltet Filetypebasierte Textsnippets um oft gebrauchte
  Textfragmente einfach einzufügen zu können. Ist sehr nützlich beim
  Programmieren, weil man in kurzer Zeit eine Methode mit Dokumentation und
  Parametern skizziert hat.

[csv-vim][]
: csv-vim sehr nettes Plugin um mit CSV-Dateien zu arbeiten. Kann die Zellen
  schön untereinander ausrichten, in Spalten suchen und Spalten ausblenden und
  noch mehr. Ideal für diejenigen, die die Orientierung in CSV-Dateien
  verlieren, die viele hundert Spalten besitzen aber nicht auf die Nerven haben
  eine CSV mit einem Officprogramm zu editieren.

[vim-latex][]
: vim-latex habe ich erst seit kurzem und verwende noch nicht so viele
  Features von diesem Plugin, aber allein das kompilieren der Sourcen via `\ll`
  ist es Wert vim-latex zu verwenden.


Die hier folgenden Plugins wollte ich gerne benutzen, mach es aber nicht:

- buffexplorer
- drawit
- fuzzyfinder
- nerdtree
- surround
- taglist
- tasklist
- vim-fugitive


## Wichtige Befehle

Ich habe mich 2 Jahre damit gequält den Insert-Mode mit `<esc>` zu beenden,
bis ich in den Hilfeseiten entdeckt habe, dass man auch `CTRL-[` verwenden
kann, trotz der drei tasten besser zu erreichen ist. Jetzt weiß ich auch, dass
man auch `CTRL-c` verwenden kann (geht auch in der CLI). Bei `CTRL-c` werden
allerdings keine Abkürzungen "abbreviations" aufgelöst.

## Links

- [http://www.vim.org/][vim] die Offizielle Website des vim Projektes

[vim-pathogen]:          https://github.com/tpope/vim-pathogen
[vim-fastwordcompleter]: https://github.com/fanglingsu/vim-fastwordcompleter
[Vimwiki]:               http://code.google.com/p/vimwiki/
[vimoutliner]:           https://github.com/vimoutliner/vimoutliner
[snipmate]:              https://github.com/msanders/snipmate.vim
[csv-vim]:               https://github.com/chrisbra/csv.vim
[vim-latex]:             http://vim-latex.sourceforge.net/
[vim]:                   http://www.vim.org/    "Offizielle Website des vim Projektes"

