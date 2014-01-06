---
layout: post
title: "Creating a installer using Inno Setup on Linux and Mac OS X"
category: posts
---

The best way to create installers for Windows is using Inno Setup. 
But then you face that same scary situation: It's Windows only.
For our delight Inno works smoothly over Wine.

As I needed it to work in both OS X and Linux and itegrate into Ant, 
I wrote a simple wrapper that runs ISCC, the Inno Compiler, from wine 
prefix. It's really simple to integrate it in whatever build system you use.

Dependencies
------------

The first thing you need is Wine, of course. And you need at least version 1.6.
Go to [Inno Setup Page](http://www.jrsoftware.org/isdl.php) and download
Quick Start installer. If you want an IDE for editing scripts, you can download 
Studio instead. It's important that you install it on standard folder, as script
will locate the compiler into `%PROGRAMFILES%\Inno Setup 5` path.

Get the script
--------------

The script is hosted on a [Gist](https://gist.github.com/derekstavis/8288379). 

If you want a raw link to script get it [here](https://gist.github.com/derekstavis/8288379/raw/678c72b66e14dbedff4a5b7786a5235aea18e983/iscc).

Running
-------

1. Place `iscc` script into `/usr/bin` or any directory included in your `PATH`.
2. Give execution permissions using `chmod +x iscc`
3. To invoke the compiler use `iscc script_file.iss`

