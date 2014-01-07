---
layout: post
title: "Creating a installer using Inno Setup on Linux and Mac OS X"
category: posts
---

The best way to create installers for Windows is using Inno Setup. 
But then you face that scary situation: It's Windows only. To your surprise, 
Inno works smoothly over Wine. Even Inno Studio works without any quirks.

As I needed it to work in both OS X and Linux and integrate into Ant, 
I wrote a simple wrapper that runs ISCC, the Inno Compiler, from the available 
wine prefix. It's really simple to integrate it in whatever build system you use.

The Dependencies
----------------

The first thing you need is Wine, of course. And you need at least version 1.6.

Go to [Inno Setup Page](http://www.jrsoftware.org/isdl.php) and download
Quick Start installer. If you want an IDE for editing scripts, you can download 
Studio too.

It's important that you install it on standard folder, as script will locate the 
compiler in `%PROGRAMFILES%/Inno Setup 5` directory by default.

If you already installed Inno Studio or Quick Start into a different path, 
edit the script and point INNO_BIN variable to your ISCC.exe binary. 
This path is relative to Program Files directory.

The Script
----------

The script is availabe in a [Gist](https://gist.github.com/derekstavis/8288379).
For command line fans, get a raw link [here](https://gist.github.com/derekstavis/8288379/raw/678c72b66e14dbedff4a5b7786a5235aea18e983/iscc).

Compiling
---------

1. Place `iscc` script into `/usr/bin` or any directory included in your `PATH`.
2. Give exec permissions using `chmod +x iscc`
3. To invoke the compiler use `iscc script_file.iss`

