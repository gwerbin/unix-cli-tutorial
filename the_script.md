----
title: "How to use the command line"
author: "Greg Werbin and QASR"
output:
    html_document:
        fig_caption: true
----

### Intro

Today we're going to learn how to use the command line.

Hopefully you followed the instructions we sent out with the RSVP. If you're on a Mac there isn't much you had to do, but if you're on a Windows machine you will need to have Cygwin installed and ready to go in order to be able to do most what I'm going to show today.

Now, Windows does have its own command line, with its own commands and syntax, but the de facto standard is the Unix-style command line, and especially the Bash shell. I'll explain what I mean by all that in a second.

Let's start by opening Terminal, or Cygwin. You should see something similar to what I have, although it probably won't be exactly the same. Before we start typing anything, some context:

This screen is the command line, or the command prompt. "Command" because you use it to give commands to the computer, and "prompt" because it's prompting you for such a command.

The program we have open is called a "terminal" which is short for a "terminal emulator," and the terminal allows us to deliver commands to a "shell," which in turn delivers those commands to the operating system. It's an "emulator" because once upon a time a terminal was a physical device:

![A terminal. Source: http://commons.wikimedia.org/wiki/File:Televideo925Terminal.jpg](http://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Televideo925Terminal.jpg/579px-Televideo925Terminal.jpg)

So in an abstract sense the one on your screen is emulating the behavior of that device. The terminal on a Mac is just called Terminal. In Cygwin, the terminal is called MinTTY. On a Mac, the operating system is the Mac OS, which is a descendant of BSD, which is a variant of the Unix operating system. Linux is also based on Unix. That's why your Mac has this Unix-like environment inside it that's ready to go; because there actually _is_ Unix inside it. On a Windows, Cygwin programs are actually speaking to the Windows operating system, so even though they do a good job of looking and acting like Unix, it's not a perfect imitation.

The default shell on Macs, in Cygwin, and on a lot of Linux machines is called Bash. The shell is just a program that turns commands into actions, but it is also an interpreted scripting language with its own syntax. Different shells have different syntax, which is why using the built-in Windows shell, called CMD.EXE, can be a different experience from using Bash even when the programs are the same. That's not to mention that different operating systems have different programs available. On Unix systems, the other shell you might run into is the Z Shell, or "zsh," which has some additional nice features, but you'll rarely be forced to use it unless you want to.

### Getting started

So here we're being prompted for a command, but right now we have no idea what commands Bash will understand, let alone what we might even want to command it to do.

When using a shell, you are always working "inside" a folder on your computer, called the "working directory." This is like always having a Finder or Explorer window open in a particular folder, and, loosely, all of the commands you enter are assumed to act on that folder unless specified otherwise. I'll try to show you what we're doing in the shell with my Finder window, to try and tie it back to what we're used to doing.

In Finder/Explorer, we can usually see what folder we're in by looking at the title bar. In the shell, we're going to use a command to do this:

```
pwd
```

which stands for "`p`rint `w`working `d`irectory." Try it now; all it does is print the working directory to the terminal output, called the "standard output" or stdout. By default, the shell opens in what's known as the home directory, which on a Mac is /Users/your-user-name. The "/" directory is the "base" directory. In Cygwin, the file structure is going to be a little bit different, because it sets up a "mini Unix" file structure inside a folder somewhere in your computer and "pretends" there's nothing outside it, but in Windows the "/" is equivalent to "C:".

The default Mac prompt is made of a few components: the "host name," which is usually the name of your computer unless you're connected to a big network like the Columbia network, the working directory, your username, and a dollar sign to indicate where to type in commands. You'll see that the working directory here is `~` and not `/Users/hotdog2`. The tilde is Unix shorthand for the home directory, whatever it might be. To see this, type

```
echo ~
```

Before it runs any command here, the shell first sees that there's a `~` and "expands" it to `/Users/hotdog2`, and _then_ runs the command. That might not mean much right now, but it's a special kind of behavior and it will be important to understand once you start programming the shell, which you undoubtedly will at some point. The `echo` command just prints its argument to stdout, so all we did here was tell Bash to run the command `echo` on its "argument," which is programming-language jargon for "input to a function." In Bash, functions and arguments are separated by a space, and arguments are also separated from each other by a space. This makes it really easy to write commands without lots of punctuation, but it can also cause problems with, say, spaces in file names. You are allowed to have spaces in file names but you need to handle them the right way. We'll get to that a bit later.

So you might have noticed that you feel a little bit "blind" working in the shell versus working in the GUI. For instance, in Finder I can not only see all of the contents of my working directory but I also have a lot of other information available at once. In the shell, you have to ask for that information; it doesn't tell you anything you don't ask it for. We can see the contents of the working directory with the command

```
ls
```

which stands for "`l`i`s`t files." A

