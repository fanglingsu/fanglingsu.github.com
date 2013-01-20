---
title: Git Cheat-Sheet
layout: default
---
[Home](/) > [Software](/software/index.html) > Git Cheat-Sheet

# Git Cheat-Sheet

## Reference Clone

    git-clone --reference ./vimprobable \
        https://github.com/fanglingsu/vimprobable.git \
        new_vimprobable

## New Project

    mkdir project
    cd project

    git init
    // Dateien anlegen und Code schreiben
    git add .
    git commit -m "Initial commit"

## Merges

Typischer Workflow.

    git checkout -b topic-branch
    vim hack.c
    git commit

    # mergen
    git checkout master
    git merge topic-branch
    git branch -d topic-branch

    # oder alles in einem Commit mergen
    git checkout master
    git merge --squash --no-commit topic branch
    git commit
    git branch -d topic-branch

## Rebase

    git rebase master topic-branch-2

    # rebase conflicts
    git rebase {--continue | --abort | --skip}

    # helpful
    git rebase -i

## Diff

    git diff HEAD

## Log

    # anzeigen was sich in den letzten zwei Tagen geändert hat
    git log --since='2 days ago'

    # zeige die Logeinträge zwischen dem aktuellen stand und dem master Zweig
    git log master..HEAD

    # eine Überblick über die Coder und ihre Änderung erhalten
    git log --no-merges v2.6.18.. drivers/usb | git shortlog | less -S

## Patches generieren und versenden

Patch für alle Commits zwischen dem master Branch und dem aktuellen
generieren.

    git format-patch -M -n --cover-letter -o patchdir master
    // Covermail bearbeiten
    $EDITOR patchdir/0000*
    git send-email --compose --to <email-address> patchdir

## Ein Patch anwenden

    git am <path-to-patchfiles>

## Remove Remote Commits

Den letzten Commit von einem Remoterepository entfernen:

    git push -f origin HEAD^:master

Ein Remote-Branch löschen geht auf folgende Art, im Grund das pushen von
Nichts auf den angegebenen Branch.

    git push origin :fls/new-hint-modes

Das funktioniert auch für Tags:

    git tag -d tag_name
    git push origin :refs/tags/tag_name
