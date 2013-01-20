---
title: Versionskontrolle mit Git
layout: default
---
[Home](/) > [Software](/software/index.html) > Versionskontrolle mit Git

# Versionskontrolle mit Git

Git, Englisch für eine "blöde nichtsnutzige Person" oder eine neuere
Interpretation als "Global Information Tracker".

## Anforderungen an die Versionskontrolle

- Unterstützung verteilter Entwicklung
- Tausende Entwickler, die an verschiedenen Teilen Tätig sind
- Schnelle und Effiziente Ausführung (Update, Merge, Netzwerklatenz)
- Integrität und Vertrauen bewahren
- Verantwortlichkeit erzwingen (Nachvollziehbarkeit von Änderungen)
- Unveränderbarkeit (Datenobjekte und Historie können nicht mehr geändert
  werden) -> Vorteil: schnellere Vergleiche auf Objekten
- Atomare Transaktionen (Änderungen werden ganz oder gar nicht ausgeführt -
  durch Aufzeichnung diskreter Repository-Zustände)
- Unterstützung und Förderung der verzweigten Entwicklung (branches, schnelles
  und einfaches mergen)
- Vollständiges Repository (jedes Repository enthält zu jeder Datei eine
  vollständige Kopie aller vergangenen Revisionen)
- sauberes internes Design (schlichtes Objektmodell mit einer eindeutigen
  Identifizierungstechnik) - Git unterstützt auch große `Commits` z. B. 1. Git
  Commit für den Linux Kernel 2.6.12-rc2 mit 17291 Dateien und 6718755 Zeilen
  Code (vlg. Magento 1.5.1.0 besitzt ungefähr 1848434 Zeilen Code)
- Frei

## Erste Schritte

Einige kurze anwendungshinweise gibt es im [Git-Cheat-Sheet](git-cheat-sheet.html).

    $ git
    usage: git [--version] [--exec-path[=<path>]] [--html-path]
               [-p|--paginate|--no-pager] [--no-replace-objects]
               [--bare] [--git-dir=<path>] [--work-tree=<path>]
               [-c name=value] [--help]
               <command> [<args>]
    
    The most commonly used git commands are:
       add        Add file contents to the index
       bisect     Find by binary search the change that introduced a bug
       branch     List, create, or delete branches
       checkout   Checkout a branch or paths to the working tree
       clone      Clone a repository into a new directory
       commit     Record changes to the repository
       diff       Show changes between commits, commit and working tree, etc
       fetch      Download objects and refs from another repository
       grep       Print lines matching a pattern
       init       Create an empty git repository or reinitialize an existing one
       log        Show commit logs
       merge      Join two or more development histories together
       mv         Move or rename a file, a directory, or a symlink
       pull       Fetch from and merge with another repository or a local branch
       push       Update remote refs along with associated objects
       rebase     Forward-port local commits to the updated upstream head
       reset      Reset current HEAD to the specified state
       rm         Remove files from the working tree and from the index
       show       Show various types of objects
       status     Show the working tree status
       tag        Create, list, delete or verify a tag object signed with GPG
    
    See 'git help <command>' for more information on a specific command.

### Beispiel

    mkdir ~/public_html
    cd ~/public_html
    echo "Meine Website ist da!" > index.html

Anlegen eines Leeren Repositorys.

    git init
    git status

Eine Datei dem Repository hinzufügen.

    git add index.html
    git status

Den ersten Commit absetzten.

    git commit -m 'Initial Commit'
    git status

Den zweiten Commit tätigen.

    cd public_html
    # hack-hack
    git commit index.html

Das Commitlock anschauen.

    git log
