# How to use the command line
### November 18, 2014
### by Greg Werbin, on behalf of QASR

## Intro

Today we're going to learn how to use the command line. The command line is a great tool for automating tasks, processing text streams, and just getting around your computer efficiently. I'm going to throw a lot of stuff at you today, but it really is worth taking the time to learn. It's an old school skill, but it's coming back in a big way. If nothing else, you will be more efficient and therefore productive once you're comfortable with it. But it's also becoming increasingly important as a component of basic computer literacy for anyone involved in statistics and other data-related work, because those fields are becoming increasingly dependent on computing and programming.

Hopefully you followed the instructions we sent out with the RSVP. If you're on a Mac there isn't much you had to do, but if you're on a Windows machine you will need to have Cygwin installed and ready to go in order to be able to do most what I'm going to show today.

Now, Windows does have its own command line, with its own commands and syntax, but the de facto standard is the Unix-style command line, and especially the Bash shell. I'll explain what I mean by all that in a second.

Let's start by opening Terminal, or Cygwin. You should see something similar to what I have, although it probably won't be exactly the same. Before we start typing anything, some context:

This screen is the command line, or the command prompt. "Command" because you use it to give commands to the computer, and "prompt" because it's prompting you for such a command.

The program we have open is called a "terminal" which is short for a "terminal emulator," and the terminal allows us to deliver commands to a "shell," which in turn delivers those commands to the operating system. It's an "emulator" because once upon a time a terminal was a physical device:

![A terminal. Source: http://commons.wikimedia.org/wiki/File:Televideo925Terminal.jpg](http://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Televideo925Terminal.jpg/579px-Televideo925Terminal.jpg)

So in an abstract sense the one on your screen is emulating the behavior of that device. The terminal on a Mac is just called Terminal. In Cygwin, the terminal is called MinTTY. On a Mac, the operating system is the Mac OS, which is a descendant of BSD, which is a variant of the Unix operating system. Linux is also based on Unix. That's why your Mac has this Unix-like environment inside it that's ready to go; because there actually _is_ Unix inside it. On a Windows, Cygwin programs are actually speaking to the Windows operating system, so even though they do a good job of looking and acting like Unix, it's not a perfect imitation.

The default shell on Macs, in Cygwin, and on a lot of Linux machines is called Bash. The shell is just a program that turns commands into actions, but it is also an interpreted scripting language with its own syntax. Different shells have different syntax, which is why using the built-in Windows shell, called CMD.EXE, can be a different experience from using Bash even when the programs are the same. That's not to mention that different operating systems have different programs available. On Unix systems, the other shell you might run into is the Z Shell, or "zsh," which has some additional nice features, but you'll rarely be forced to use it unless you want to.

## Getting around

So here we're being prompted for a command, but right now we have no idea what commands Bash will understand, let alone what we might even want to command it to do.

When using a shell, you are always working "inside" a folder on your computer, called the "working directory." This is like always having a Finder or Explorer window open in a particular folder, and, loosely, all of the commands you enter are assumed to act on that folder unless specified otherwise. I'll try to show you what we're doing in the shell with my Finder window, to try and tie it back to what we're used to doing.

In Finder/Explorer, we can usually see what folder we're in by looking at the title bar. In the shell, we're going to use a command to do this:

```
pwd
```

which stands for "`p`rint `w`working `d`irectory." Try it now; all it does is print the working directory to the terminal output, called the "standard output" or stdout. By default, the shell opens in what's known as the home directory, which on a Mac is /Users/your-user-name. The "/" directory is the "base" directory. In Cygwin, the file structure is going to be a little bit different, because it sets up a "mini Unix" file structure inside a folder somewhere in your computer and "pretends" there's nothing outside it, but in Windows the "/" is equivalent to "C:".

The default Mac prompt is made of a few components: the "host name," which is usually the name of your computer unless you're connected to a big network like the Columbia network, the working directory, your username, and a dollar sign to indicate where to type in commands. You'll see that the working directory here is `~` and not `/Users/hotdog2/`. The tilde is Unix shorthand for the home directory, whatever it might be. To see this, type

```
echo ~
```

Before it runs any command here, the shell first sees that there's a `~` and "expands" it to `/Users/hotdog2/`, and _then_ runs the command. That might not mean much right now, but it's a special kind of behavior and it will be important to understand once you start programming the shell, which you undoubtedly will at some point. The `echo` command just prints its argument to stdout, so all we did here was tell Bash to run the command `echo` on its "argument," which is programming-language jargon for "input to a function." In Bash, functions and arguments are separated by a space, and arguments are also separated from each other by a space. This makes it really easy to write commands without lots of punctuation, but it can also cause problems with, say, spaces in file names. You are allowed to have spaces in file names but you need to handle them the right way. We'll get to that a bit later. \< talk about Cygwin: http://stackoverflow.com/q/11089390/2954547 >.

So you might have noticed that you feel a little bit "blind" working in the shell versus working in the GUI. For instance, in Finder I can not only see all of the contents of my working directory but I also have a lot of other information available at once. In the shell, you have to ask for that information; it doesn't tell you anything you don't ask it for. We can see the contents of the working directory with the command

```
ls
```

which stands for "`l`i`s`t files." On my screen, folders are purple and regular files are white, but that's because I set those colors in a special file that I won't have time to discuss today; by default there isn't any color coding. On a Mac, like on my computer, there is going to be a lot of junk in here. \< talk about Cygwin >.

What's cool about `ls` is that it also takes arguments. That is, I can actually tell `ls` what folder to display without having to navigate to that folder (which I haven't told you how to do yet, anyway). Let's say we wanted to look at the contents of our system root directory, indicated by a plain `/` (this works differently from `~`; more on it later). Then we can type

```
ls /
```

which passes the argument `/` to the `ls` command. You can do this with any directory on your machine! There are also the "special" directories `.` and `..`. The first refers to the current directory, so `ls .` is equivalent to `ls` without any arguments, and the second refers to whatever directory is _above_ the current working directory. When I'm in my home directory, `..` refers to `/Users` so `ls ..` lists the contents thereof. Note that `..` works differently from `~`: it's a special file, unlike `~` which is a special _word_ understood by Bash, so Bash doesn't expand `.`. You can try `echo ..` to see what I mean.

Now what if we want to change directories? Let's say we wanted to move up one directory, i.e. move to `..`. Then we can type

```
cd ..
```

which stands for `c`hange `d`irectory, in this case to `..`. Now we can `pwd` and see that, in fact, I'm in `/Users/`, and we can use `ls` to see that, in fact, `hotdog2/` is an item the current directory. Or we can look at the contents of `hotdog2` with `ls hotdog2`. Then we can change directory back to our home directory with

```
cd hotdog2
```

or

```
cd hotdog2/
```

where the trailing slash is completely optional, but sometimes using the slashes can help you keep track of what you're doing.

We can also use `~` here. For instance, you can always `cd ~` to change back to your home directory.

## Keyboard interrupt: the "eject" switch

So just to see what happens, try typing the wrong thing:

```
cd hotdog
ls hotdog
```

which will give you an error. Or worse, you can type

```
cd hotdog`
```

which won't even give you an error. There are also plenty of "dangerous" things you can type, that I won't show you here, that can permanently damage your computer. To break out of a bad input, press `ctrl+c`. This "keyboard interrupt" will also stop a running program, which can be a life saver.

## Options

Most Unix programs have multiple options that can be used by passing `switches` or `flags` as arguments. For instance,

```
ls -l
```

shows files in "long" format, which includes more information.

```
ls -a
```

shows "all" files, including `.` and `..` as well as any other hidden files. You can also typically chain these together, so `ls -la` is equivalent to `ls -l -a`. "Short" options are prefixed by a single `-`, while "long" options, like a lot of options in Git, are prefixed by `--`. 

## Getting help

And where are all these options documented? There is a Unix program called `man`, short for `man`ual, that allows us to, unsurprisingly, read the manual. Try

```
man ls
```

`man` actually doesn't render the text output here; that's handled by a program called a "pager," which on a Mac and most other systems defaults to a program called `less`. Getting around `less` can be a bit confusing at first. For instance, you can always exit with the `Ctrl+C`, but that's like using the Windows task manager to exit MS Word. `less` has its own set of commands that are inspired by the 

As an aside: One of the obstacles to learning to work on the command line is that you have to remember not only a mini programming language just to get around and do things, but most programs on the command line have their _own_ set of commands to remember. There's a big learning curve here, but it comes naturally with some time and practice. One thing I'll encourage you to do, especially if you're going to be at Nick's workshop next week, is to make excuses to do small tasks on the command line. Knowing how to get around a `man` page is a particularly good way to learn how to do things faster, because it's easy to get help.

The first (and in a way, only) `less` command in you need to know is `h`, which unsurprisingly brings up the `h`elp page. Here you can see the other basic commands. Note that `^` means the `Ctrl` button. You can typically scroll around with the arrow keys, although you can also use the commands shown. The other all-important command is `q`, which quits the program (properly). Also vital is the command `/`, which searches forward, and `?` which searches backward. `n` repeats the previous search. `u` scrolls up an entire page, and `d` scrolls down a page.

One last note about moving around: Bash has several keyboard shortcuts other than `ctrl+c`. Other handy features are `ctrl+a`, which deletes everything from the cursor position to the beginning of the line, `ctrl+a` which jumps to the beginning of the line, `ctrl+e` which jumps to the end, and `ctrl+k` which deletes everything from your cursor to the end of the line. To see these, try

```
man bash
/commands for moving
```

to jump to the appropriate heading.

There are two different styles of keyboard commands being used here, originally created by two popular command-line text editors, Emacs and Vi. Bash uses Emacs-style commands, and `less` uses Vi-style commands.

## Managing files

Quick note about file names: spaces are allowed in file names on Mac OS and Windows, but as I mentioned before Bash uses spaces to delineate commands and arguments. This can be solved by quoting file names, such as `cd "class/data viz"` or `cd 'class/data viz'`. There is actually a difference between `"` and `'`, although it's not that important right now. You should, however, look it up online and make sure you understand it. Another way to solve the problem (although it's ugly) is with "escaping" the offending character by preceding it with a backlash. The backslash tells Bash to ignore the next character and treat it like regular text. You could do `cd class/data\ viz` but that's hideous. Escaping also allows me to type things like `echo \;`, since normally Bash uses `;` to indicate the end of a command without a line break.

So let's actually do something. Type `cd ~` just to make sure we're in our home directory. Then type:

```
mkdir shell-tutorial
```

to `m`a`k`e a `dir`ectory called "shell-tutorial." You can call it something different, but keep in mind what I said about spaces quoting. You're also allowed to use periods, digits, and underscores to your heart's content. Although you should know that starting a file name with a period signals to Bash (and also Finder) that the file is hidden, and it won't come up in Finder (unless you turn on the right setting) or `ls` unless you use `ls -a`. A lot of configuration files are stored in your home directory this way, which is why people often call them "dotfiles."

`ls` to see that you did indeed make a new folder, and `ls shell-tutorial` to see that it's empty. Now let's put a file in there. Write

```
touch shell-tutorial/stuff1
```

to create a new file, "stuff1" in the directory "shell-tutorial." and `ls shell-tutorial` to see that it in fact contains a file called "file1." Now, `cd shell-tutorial` to enter it. Confirm where you are with `pwd`, and confirm with `ls` that it contains `stuff1`.

Let's create two other directories:

```
mkdir my-files my-backups
```

and `ls` to see that we did in fact make them.

Let's say we wanted to move "stuff1" into "my-files". We use

```
mv stuff1 my-files/stuff1
```

to `m`o`v`e the file from the location in the first argument to the location in the second argument. This is actually what we use to rename files as well. Rename "file1" to "file1.txt" with

```
mv my-files/file1 my-files/stuff1.txt
```

Note that file extensions, including on Windows systems, are completely optional. They are just a way for the user and the operating system to know what's inside a file. But at the end of the day, _all files can be treated like text files_. I can open a PDF or Word file in a plain text editor like Notepad or Textedit, but I will get either a bunch of 1's and 0's or just plain garbage text. Those applications can't read the data inside, but it's all stored the same way.

Knowing this, let's give "stuff1.txt" a more descriptive name. Since typing paths is a pain, `cd my-files` first. Then

```
mv stuff1.txt regression_model_diagnostics.log
```

and `ls` to confirm what happened. Typing that long file name is going to be really obnoxious. Most terminals are equipped with "tab completion" that allows me to start typing `reg` and press `tab` to have it automatically fill in the full file name. This can save you a LOT of typing.

Now suppose we wanted to make a backup of our log file and put it in the other folder we made. Use

```
cp regression_model_diagnostics.log ../my-backups/regression_model_diagnostics.log
```

to `c`o`p`y the file named in the first argument to the location named in the second. `ls ../my-backups` to see what we did.

You might have noticed by now that file paths are relative. This includes the special directory `..`, which lets me do things like `ls ../my-backups`. Absolute paths start with `/`, which is why we say that `/` "is" the root directory. The one exception is for directories in the search path, which tells Bash where to look for executable files. Type `echo $PATH` to see your search path; it's a list of directories separated by a colon.

Now that we've made our backup, we can delete the original file:

```
rm regression_model_diagnostics.log
```

to `r`e`m`ove it.

Now `cd ~/shell-tutorial/` to return to where we started. Remember `cd ..`  would have done the same thing.

Let's remove an entire directory:

```
rmdir my-files
```

Note that this is equivalent to (but sometimes safer than) the `rm -d`.

### Text and viewing files

There are a few quick text handling tools we're going to run through but not explore in depth. First is the command `head`, which prints the first few lines (the "head") of a file to stdout. There's also `cat`, which prints entire files straight through. The name comes from con`cat`enate because it accepts multiple input files and prints them all end to end, i.e. conc`cat`enating them.

The `|` tool allows you to "pipe" the text output of one command to another. So you can write:

```
ls /bin | head -n2
```

to print only the first two lines of output from `ls`. Note that `ls` "knows" what is reading its output. If it's stdout, it will separate files with tabs. If it's anything else, like a pipe, it will write one file to each line: `ls /bin | echo`.

The `>` is a "redirect" in that it "redirects" the output of a command to a file. We can type `touch hello_world` and then `echo hello world > hello_world`. Then `cat hello_world` to see what we did. Then we can `echo goodbye world > hello_world` to overwrite the file with "goodbye world" and then `cat hello_world` to see the change.

You can also append, rather than redirect with `>>`. Try `echo just kidding >> hello_world` and `cat hello_world` to see what happened.

And just to show you what quoting can do, try:

```
echo "hello world" >> hello_world
echo \"hello world\" >> hello_world
echo 'hello world' >> hello_world
echo '"hello world"' >> hello_world
echo '\"hello world\"' >> hello_world
cat hello_world
```

You can also, of course, edit files with a regular text editor. You can do it in TextEdit or Notepad, or a more powerful editor like Sublime Text (highly recommended!!), or you can do it right on the command line with Emacs, Vim ("Vi iMproved"), or Nano. Nano is the simplest to use and I recommend it for beginners. Emacs and Vim are both extremely powerful but also have very steep learning curves. I'm not good with either of them, although I'm slowly learning to like Vim. Sublime Text and Notepad++ (which I haven't used much) strike a nice balance between horrible plain text editors and the full-powered command line editors.

### Package managers

One last thing: Linux pioneered a brilliant "package manager" system. For instance, on Ubutnu and Debian, I can type, say, `apt-get R` to automatically download, build, and install R. A few third-party package mangers exist for Macs, but I'm only going to recommend one: Homebrew. Google it to learn more. It's open source, it's written in Ruby and based on Git, and it's fairly self-contained, in that it doesn't spew garbage all over your system and typically doesn't break other programs. It can be a bit difficult to uninstall (there is no official uninstall tool and the one uninstall script people link to is horrible and dangerous).

On Cygwin, you don't have a command line package manager but it does have a package manager. Run the "setup.exe" file that you used to install Cygwin to access it. Cygwin comes with a very limited set of tools by default, but it has a good selection of available packages.

### One last thing:

In your home directory, there might be a file called `.bash_profile`. Type `ls -a ~` to see if it's there. If not, you can make one with `touch ~/.bash_profile`. This dotfile is run every time you log in to a Bash session, and it's where you can set options.

For instance, let's say you made a folder `~/bin` where you place all of your handy Bash scripts. You can run these scripts with `~/bin/my_script input_1 input_2`, or you can

```
echo 'export PATH="~/bin:$PATH"' >> ~/.bash_profile
```

to add `~/bin` to the search path. So then I could just type `my_script` from any folder and Bash will know to look there, and look there first (because it's first in the list), for an executable file called `my_script`. This is in fact how executable like `cp` are stored: `ls /bin`, and `echo $PATH` to note that `/bin` should be in there somewhere. 

The quoting here is defensive, just in case someone (foolishly) decided to put a directory with a space into `PATH`. Note that the `$` tells Bash to expand the variable `PATH`. Variables are expanded inside double quotes `""` but not inside single quotes `''`:

```
echo $PATH
echo "$PATH"
echo '$PATH'
```

### That's it!

Thank you! There are lots of resources online for getting help in Bash. Manpages, Google, and the various Stack Exchange sites (Unix & Linux most of all, but also SuperUser, Ubuntu, occasionally even Serverfault, and of course the venerable StackOverflow) are great resources for learning more. These notes will also be archived on the QASR website.

And last but not least, Nick Ursa of the CS department and the Columbia Data Science Society is teaching a tutorial on using the command line for data processing at the same time next week: Tuesday November 25 at 6 PM. See you there!
