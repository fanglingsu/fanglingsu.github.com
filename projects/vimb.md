---
title: Vimb Browser
layout: default
---
[Home](/) > [Projekte](/projects/index.html) > Vimb Browser

# Vimb Browser

In Summer 2011 I found the [vimprobable](vimprobable.html) project and began
to make patches for it. This is a really nice project and a very powerful,
fast and easy to use browser. The only reason to implement a new (yet another
vim like browser) was the historic and monolithic code. This makes the hunting
for Bugs and memory leaks to a hard job. 

So I started to migrate the behaviour and look of vimprobable to a completely
new written [code base][vimb] that consequently uses the high-level functions provided
by the used libraries. Because I know the features I'd like to have and that
are known from vimprobable, I could implement the code to fit this features,
even if the features will be implemented in future.

My concerns goes mainly to the code-base. I do not think about features at the
moment, because the goal is to have a clean, easy to read and maintain code
base and to not have memory leaks. Second goal is performance, but not in such
a consequent way like it's know from [Suckless][].

## Features

- vim-like modal
- vim-like keybindings
- nearly every configuration can be changed on runtime with `:set varname=value`
  - allow to inspect the current set values of variables `:set varname?`
  - allow to toggle boolean variables with `:set varname!`
- keybindings for each browser mode assignable
- the center of `vimb` are the commands that can be called from inputbox or
  via keybinding
- history for
  - commands
  - search queries
  - urls
- completions for
  - commands
  - urls (visited and bookmarked)
  - variable names of settings
- hinting - marks links, form fields and other clickable elements to be
  clicked, opened or inspected
- webinspector that opens ad the bottom of the browser window like in some
  other fat browsers
- ssl validation against ca-certificate file
- custom configuration files
- embedding via xembed into other applications like [tabbed][]
- tagged url bookmarks

[suckless]: http://suckless.org/
[vimb]:     https://github.com/fanglingsu/vimb  "Vimb Browser"
[tabbed]:   http://tools.suckless.org/tabbed/
