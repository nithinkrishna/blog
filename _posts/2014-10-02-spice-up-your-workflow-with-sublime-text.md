---
layout: post
title:  "Spice up your workflow with sublime-text"
categories: sublime-text
comments: true
description: Spice up your workflow with sublime-text
tags:
  - sublime-text
  - ruby
  - rails
  - productivity
author: Nithin Krishna
handle: "nithinkrishh"
---

I often find it distracting to have to switch workspaces, or switch between my text editor and the terminal. We are most productive within the realms of our text editors. It's important to establish a workflow which requires minimal context switching.

Over the course of this blog, I'm going to suggest some some user-settings and very useful sublime text plugins which will help you reduce context-switching and write better code.

---

## Setting up

Aesthetics of code is key. You code needs to be pleasing to look at. In addition to choosing the right theme, sublime offers loads of other settings that allow you to prettify you code.

```json
{
  "auto_complete_commit_on_tab": true,
  "bold_folder_labels": true,
  "dictionary": "Packages/Language - English/en_US.dic",
  "ensure_newline_at_eof_on_save": true,
  "font_size": 13,
  "highlight_line": true,
  "highlight_modified_tabs": true,
  "line_padding_bottom": 0.5,
  "line_padding_top": 0.5,
  "margin": 2,
  "rulers":
  [
    80
  ],
  "save_on_focus_lost": true,
  "spell_check": true,
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "trim_trailing_white_space_on_save": true
}
```

For example, I've set a ruler at 80. This ensures that, I have a sense of how long each line of code is. `trim_trailing_white_space_on_save` automatically removes all trailing white spaces and `ensure_newline_at_eof_on_save` adds a new line at the end of each line after save.

<img src="https://db.tt/hjFDouh0" />

It's important to to be aware of the modes and layouts on offer. Choose layouts to complement the work you are currently on.

<img src="https://db.tt/JfNWnuyq" />

---

## Packages

### The package manager

The most important of them all. Install/Remove packages with a few simple key-strokes.

<img src="https://db.tt/Hi5rfHio" />

### Git and GitGutter

Git is one of the major contributer to our need to context switch. The Git plugin, helps you perform all the git tasks from within sublime.

<img src="https://db.tt/ePNO6IQr" />

Every time before we commit we end up viewing the diff of all staged files at least once. GitGutter displays an in-line diff, real time.

<img src="https://db.tt/gXy8fwnh" />

### RubyTest

Another major contributer to context-switching are Tests. RubyTest helps you run your specs from within sublime. It even runs specific specs, based on your cursor location.

<img src="https://db.tt/ok7wKBjm" />


### Sublime-Spotify

This is my most favorite plugin. For all the music buffs out there like mem, Sublime spotify lets you control you music from inside sublime.

<img src="https://db.tt/arRn5vpC" />
