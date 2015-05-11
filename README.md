# Terminator
by Chris Jones <cmsj@tenshu.net> and others.

## Please be informed that, this repo only works with Python 3.X!

## The repository was not fully converted to GTK3 +! Use it at your own risk!

## Intro

The goal of this project is to produce a useful tool for arranging terminals. 
It is inspired by programs such as gnome-multi-term, quadkonsole, etc. in that
the main focus is arranging terminals in grids (tabs is the most common default
method, which Terminator also supports).

When you run Terminator, you will get a terminal in a window, just like almost 
every other terminal emulator available. There is also a titlebar which will
update as shells/programs inside the terminal tell it to. Also on the titlebar
is a small button that opens the grouping menu. From here you can put terminals
into groups, which allows you to control multiple terminals simultaneously.

You can create more terminals by right clicking on one and choosing to split 
it vertically or horizontally. You can get rid of a terminal by right 
clicking on it and choosing Close. Ctrl-Shift-o and Ctrl-Shift-e will also 
effect the splitting.
Also from the right mouse menu you can access Terminator's preferences window.

Ctrl-Shift-n and Ctrl-Shift-p will Shift focus to the next/previous terminal 
respectively, and Ctrl-Shift-w will close the current terminal and 
Ctrl-Shift-q the current window.

For more keyboard shortcuts and also the command line options, please see the
manpage "terminator". For configuration options, see the manpage 
"terminator_config".

Ask questions at: https://answers.launchpad.net/terminator/
Please report all bugs to https://bugs.launchpad.net/terminator/+filebug

## History

Terminator began by shamelessly copying code from the vte-demo.py in the vte 
widget package, and the gedit terminal plugin (which was fantastically 
useful at figuring out vte's API).

vte-demo.py was not my code and is copyright its original author. While it 
does not contain any specific licensing information in it, the VTE package 
appears to be licenced under LGPL v2.

The gedit terminal plugin is part of the gedit-plugins package, which is 
licenced under GPL v2 or later.

I am thus licensing Terminator as GPL v2 only.

## Credits

Cristian Grada provided the old icon under the same licence.

Cory Kontros provided the new icon under the CC-by-SA licence.

For other authorship information, see debian/copyright

## Cloning notes

Since terminator is keep on bzr, updates to this mirror are done with

```
$ git fast-import
```

bzr clone is keep on a separate dir. Once updated

```
$ bzr pull
```

A new import is made after remove last one

```
$ rm -rf .git/ 
$ git init
$ bzr fast-export --plain . | git fast-import
```

That git clone is imported on real repo

```
$ git remote add local file://<path-to-git-import>
$ git fetch local
```

Then last common commit is detected using

```
$ git log --date-order
```

```
 * local/master <new-import>
 *
 *
 |* master <changes to default project>
 |*
 *| <common-new-commit>
 |* <common-old-commit>
 *|
 |*
```

and rebasing with

```
$ git rebase <commom-new-commit> local/master --onto <common-old-commit>
```

resulting

```
    * (HEAD)
    *
    *
 *  | local/master <new-import>
 *  |
 *  |
 |* | master <changes to default project>
 |* |
 *|/ <common-new-commit>
 |* <common-old-commit>
 *|
 |*
```

but there's a problem with launchpad workflow. There are some commits for 
releases that have no email author and that's problematic on git. So this 
script must be applied to detect and fix that commits.

```
. res/replace-authors-without-email.sh
```
