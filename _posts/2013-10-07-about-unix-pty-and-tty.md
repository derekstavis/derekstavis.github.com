---
layout: post
title: "Serial ports, parsers and what ttys0 have to do with it."
category: posts
---

When you are messing with hardware, mostly with serial lines, it's common to need read data from a stream, buffer, and parse it (maybe on a separated thread, maybe no), then taking actions about the meaning of the communication.

In the process of writing a multi-threaded, real-time parser, together with a buffering core to a system, there's one thing you can't miss: Tests.

But tests with hardware are boring. You have to repeat the same task over and over again. Things like waving your hands on a sensor is tiresome. Sometimes you just don't have the hardware with you. 

What if you could simulate a serial port and then type or send commands by hand? Here's where UNIX filesystem-centric architechture really shines.


# Teletypes

If you issue a `ls /dev/tty*` you will see a lot of devices with repeated names like ttys0, ttys1, ttys2.

They are called teletypes, or TTYs. Teletypes are basically byte-oriented serial ports where you can attach a terminal. Try it! You can open it using `minicom -D /dev/ttys9` for example.

# Pseudo-Teletypes

Pseudo-Teletypes are pseudo serial ports. They are software tunnels inside the kernel to real teletypes. Every PTY has a corresponding TTY. Hope you haven't closed the last command. If you don't, try `minicom -D /dev/ptys9`. 

Type something and then switch to the other window and see what you've typed!

# Simulating Communication

When you need to simulate communication stream over serial port you can connect to a unused PTY and then write data to it in many ways:

* using `minicom` as the example
* `cat /dev/urandom > /dev/ttys9`
* `echo "asciitest" > /dev/ttys9`

You can, of course, open it programatically and exchange data.

