**June 6, 2017**

This is the definitive guide to setting up Python on a Macintosh. The bold sections are the ones that contain just the bare essentials, but the other stuff is pretty interesting as well (feel free to skim).

##Table of Contents
1. [Prerequisites](#1)
	- [Reading](#1.0)
	- [UNIX-flavored](#1.1)
	- [macOS Root Folders](#1.2)
	- [Bash and Environment Variables](#1.3)
	- [**Run All the Checks!**](#1.4)
2. [Homebrew](#2)
	- [**Installation**](#2.1)
	- [Housekeeping](#2.2)
3. [**Python**](#3)
	- [**Warnings**](#3.0)
	- [Python 2](#3.1)
	- [Python 3](#3.2)
	- [Pip](#3.3)

## <a name="1">Prerequisites</a>
Running a few checks prior to diving into setup will make things run more smoothly, and can help prevent problems later on. The goals of the prerequisite section are to find out which tools the computer already has, which ones need installing, and how they relate to Python itself.

### <a name="1.0">Reading</a>
In this instruction manual, there's a lot of explanation. For sanity's sake, I've linked all the sections in the manual to their spot in the table of contents.

We'll be using Terminal a lot, so make sure that you always have that window open. If you don't know how to find it, there are two ways to get there:

1. Open a new Finder window and go to the `Applications` folder. In `Applications`, there is a folder called `Utilities`. Open that, and the Terminal application is in there.
2. Use the `⌘ + <spacebar>` command to open Spotlight, and type in "Terminal". It'll find Terminal, and then just hit enter (or double-click, whichever you prefer).

The notation I use for describing a Terminal command is like this:

`$ <command> [option 1] ... [option n]`

The `$` is just a separator, and it's used to denote that you've opened a new shell. The `<command>` and `[option 1] ...` parts are to show the command and options we'll be using with the shell. In short, you don't have to type the `$`.

Essentially any computer text will be formatted `like this`, so it can be differentiated from regular post text.


### <a name="1.1">UNIX-flavored</a>
macOS is based on UNIX, an operating system architecture developed at Bell Labs in the 70s. UNIX, as one of its main principles, allows shell scripting so that users can interact with the operating system. Because of this, macOS is quite modular - users can quickly and easily import third-party software and use it right out of the box with no configuration. We are going to be installing third-party software (namely Python), and a tool included with Python allows you to install even *more* third-party packages for Python to use.

### <a name="1.2">macOS Root Folders</a>
In most UNIX filesystems, there is a folder called `/`. This is the root directory, and every single file that your computer uses is inside that folder. It makes sense, then, that some of those folders are restricted so that inexperienced users ("haxors", the computer-illiterate, pets, etc.) can't write or delete from them and potentially cause harm. This is where the `/usr/` folder comes in.

`/usr/` is the directory that stores the majority of a computer's programs that interface with the operating system, but are still operable to the user. Many of these are stored in subdirectories of user, namely `/usr/bin/`, `/usr/lib/`, and `/usr/local/`.

`/usr/bin/` is mainly used to store binaries. Typically commands like `ssh`, `which`, and the like are stored there. `/usr/lib/` contains libraries for programming languages like PHP, Ruby, the system itself, and default installations for Python (in macOS Sierra, Python 2.6 and 2.7 are installed). `/usr/local/`, however, is our sandbox. This is the folder dedicated to local or third-party programs, and is managed by the system's administrator.

Additionally, many of the tools baked into a macOS installation are written by **GNU**'s **N**ot **U**nix (or just GNU). This group of hackers provides multiple suites of useful tools, namely `gcc`, a set of compilers, `coreutils`, `screen`, and the **B**ourne-**a**gain **sh**ell, or Bash - the default shell for macOS.

### <a name="1.3">Bash and Environment Variables</a>
Bash (commonly referred to as a Bash shell, which doesn't make much sense because, expanded, that's just "bash shell shell") is the default shell for macOS. When a user begins to use Terminal, they are "logged in" to the default login shell. While this user is logging in, Bash reads from three files -  `~/.bash_profile`, `~/.bash_login`, and `~/.profile` in that order. This allows any user to set preferences for Bash itself - how the prompt looks, special-use variables, sourcing other files, running background tasks, etc. We will be modifying some of these files later on, but we'll be doing it responsibly. Hopefully you'll become familiar enough to modify any of those three files later on and work some cool Bash magic.

Bash keeps track of a set of global presets called environment variables. These values are available in all new shells and open to all languages that interface with the OS once they have been set (or changed). They have universal read access, and are used by countless programs to find installations of software, packages, and other necessary programs.

When a command is run in Bash, it uses the `PATH` environment variable to search for the executable file the command is tied to. You can look at what's stored in `PATH` by running

`$ echo $PATH`. Mine returns a huge list of directories where the commands I run *could* be located.

### <a name="1.4">Run All the Checks!</a>
In order to install Python, we're going to install a package manager called [Homebrew](https://brew.sh). Homebrew manages the versions and installations of all packages. It's written in Ruby, so we're going to check that your pre-packged Ruby installation is still there.

Run

`$ which ruby`

which should return `/usr/bin/ruby/`. Next, we're going to check that you have git installed.

Git is a version control system, which is basically a tiny internal database that tracks all the changes made to a file (or set of files, or directory). Nearly every single minor or major collection of programs uses git to track changes and manage different versions of files (even Homebrew uses git to track itself). macOS comes with a pre-installed version of git, but it's old(er) and isn't as useful as newer versions. To check that git is installed, run

`$ which git`,

which should return `/usr/bin/git/`. Running

`$ git --version`

should return `git version 2.11.0 (Apple Git-81)`. Since we have those, we can now move on to installing Homebrew.

## <a name="2">Homebrew</a>
Homebrew is the a package manager that should be in every developer's toolbox. From here you can effectively manage hundreds of packages, each of which is useful for development. Many major languages and runtimes have their packages registered with Homebrew (think Python, Node.js, etc.) as well as countless other useful programs.

### <a name="2.1">Installation</a>
To install Homebrew, copy this command and paste it into Terminal. 

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

You can also go [here](https://brew.sh/) and read the instructions from the Homebrew people.

### <a name="2.2">Housekeeping</a>
It's important to keep your formulae (Homebrew-installed packages) and Homebrew itself up to date. You can run a few commands to help with maintaining your packages and keeping the number of extra packages small.

[**Here**](http://docs.brew.sh/Manpage.html) is the man page for Homebrew if you want to look at these commands in more detail.

1. `$ brew update` fetches the newest version of Homebrew from Github.
2. `$ brew upgrade` checks all formulae for updates, and if any exist, install those updates. Check the man page for more options
3. `$ brew doctor` returns potential issues with any of your formulae or Homebrew itself.
4. `$ brew prune` removes all dead symlinks from `/usr/local/bin/` so you don't have any broken links.

Make sure to take a look at the man page and find some other commands that could be useful. StackOverflow also has a pretty extensive set of questions about Homebrew, so any questions you have can be answered there better than here.

## <a name="3">Python</a>
This is the section we've all been waiting for - installing Python. It's actually quite simple, and there shouldn't be too many hiccups. We'll go over how to install both versions of Python (2.7.x and 3.x.x) as well as any errors you may encounter.

### <a name="3.0">Warnings</a>
- Do *not* use `sudo` when installing any Homebrew, Pip, NPM, or any other third-party packages. `/usr/local/` is for locally installed or third-party software, and the use of `sudo` can affect the read/write permissions of `/usr/local` by changing its owner. When installing Homebrew, it asked for your password. This is for *write permissions* to `/usr/local/`. After it's installed, Homebrew takes care of this for you by installing packages in `/usr/local/Cellar/` and then creating symlinks to executable files and placing them in `/usr/local/`, whose permissions are managed by Homebrew.

- There is a difference between `python`, `python3`, `pip`, and `pip3`. `python` and `pip` run scripts and install packages for Python 2.x respectively, while `python3` and `pip3` run scripts and install packages for Python 3.x.x respectively.

### <a name="3.1">Python 2</a>
Python 2.7 comes preinstalled on all Macs. However, it usually isn't the most current version, and Python's package manager, Pip, isn't installed.

To install Python 2, run

`$ brew install python`.

That's it! If you have errors, **GO TO THIS SECTION RIGHT HERE**.

### <a name="3.2">Python 3</a>
Many new applications and frameworks are written with Python 3, as it is considered the standard Python implementation. Support for Python 2.7 will end in 2020 (per Guido van Rossum, Python's creator).

To install Python 3, run

`$ brew install python3`. Again, for any errors, check the next section.

### <a name"3.3>Pip</a>
Pip is the package management ecosystem for Python. The Python Software Foundation keeps a registry of useful third-party Python addons that are typically open-source and publicly available.

When using 

### <a name="3.4">Errors</a>

If `$ brew install python` or `$brew install python3` gives you an error saying that:

- The bottle can't be compiled because `gcc` is not installed, run `$ xcode-select --install` to install Apple Command Line Tools (which includes `gcc`, the GNU Compiler Collection). Then, run `$ brew install python3`.
- `/usr/local/bin` may not be writable, change the permissions of the directory by running ``$ sudo chown -R `whoami` /usr/local/``.

If `$ which python` or `$ which python3` don't return `/usr/local/bin/python/` or `/usr/local/bin/python3` respectively, or when you run `$ python` or `$ python3` you get a `command not found` error, there may be a linking issue. Follow these instructions in order, and stop when the problem is fixed.

1. Run `$ brew doctor` to find any problems, and then run `$ brew unlink python && brew link python` (or `python3`) to try and rewrite the existing symlinks.
2. Run `$ brew link --dry-run --overwrite python` (or `python3`) to check if a `python3` already exists in `/usr/local/bin/`. If it does, you can overwrite it by running `$ brew link --overwrite python`.
3. If none of the above have worked, run `$ echo $PATH`. If the directory `/usr/local/bin` doesn't appear there, you'll have to modify your `PATH` environment variable. You can do this by editing `~/.bash_profile` or `~/.profile` using the [Vim editor.](https://www.linux.com/learn/vim-101-beginners-guide-vim) Add `export PATH=/usr/local/bin/:$PATH` and save the file. This adds `/usr/local/bin/` to the list of locations Bash looks for executable programs.