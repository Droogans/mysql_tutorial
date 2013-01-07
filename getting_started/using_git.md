
Git
===

The nice thing about git is that you can use it for so many things. The more you learn about it, the more likely you'll be to use it. The more you use it, the more likely it will save your future self some major headaches. You can also use git as a member of a team, and share many different versions of the same thing, and later merge them into a final product.

If you didn't already know this, you are currently reading this tutorial on github.com, which is a web interface for storing code that uses git version control.

What is version control?
------------------------

Version control is just what it sounds like: the ability to control *versions* of a document. 

I could go on and describe in detail what keeping a history of changes is all about, but other people have [already done this][Git_Intro] for me.
[Git_Intro]: http://git-scm.com/video/what-is-version-control

If you skipped that video, please go back and watch the whole thing, unless you've had experience working with version control. I promise, those five minutes will go faster than you think.

Now that you understand what git is, let's start using it. Head back to your PythonAnywhere consoles, and select a bash console (under "Others"). Before you can use git, you must understand some bash.

bash
====

Once your bash console has finished loading, you should see what's called a prompt. It'll look something like this:

    04:04 ~ $ 
	
It will have a blinking cursor at the end, taunting you with it's quiet, flashing presence. If you don't know what to do, this can be very intimidating. 

Here's a solid tip that works almost anywhere:

    04:04 ~ $ help
	GNU bash, version 4.1.5(1)-release (x86_64-pc-linux-gnu)
	These shell commands are defined internally.  Type `help' to see this list.
	Type `help name' to find out more about the function `name'.
	Use `info bash' to find out more about the shell in general.
	Use `man -k' or `info' to find out more about commands not in this list.
	
	[...more output below...]
	
Basically what this says is that we're using `bash`, which is an implementation of a program called a shell. There are many different [types of shell programs][Shell_List].
[Shell_List]: http://en.wikipedia.org/wiki/Unix_shell#Shell_categories

A shell is, simply, the black screen we're looking at, and is most often called a terminal. That big list at the bottom of the output is some of the more common commands you can use.

Let's try a few of them.

    04:04 ~ $ pwd
	/home/USERNAME
	
`pwd` stands for "print working directory". If you've used Windows before, you might know of directories as folders. If it helps, you could imagine this directory looking like this in Windows

    C:\Users\USERNAME\
	
Except Linux doesn't use the `C:` part. It replaces it with the *root directory*, which is where the first "folder" on a linux computer lives (similar to how `C:` is called "My Computer" in Windows).

Let's *change directories* (which is what the `cd` stands for) to the root folder.

    04:04 ~ $ cd /
	04:04 / $
	
Notice that the `~` sign in the prompt changed to a `/` sign. That `/` character is the name of the directory you're currently in. The directory you were just in was called `~` (this is a shortcut for `/home/USERNAME`, since it's used all the time. You can always go back to your home directory by using `cd ~`).

To see how this works, try printing out a *list* (`ls`) of all the directories in `/`.

    04:04 / $ ls
	bin  dev  etc  home  lib  lib64  proc  sbin  tmp  usr  var
	
See `home`? It's a directory in `/`, so to switch to that directory, you'd do this.

    04:04 / $ cd home
	04:04 /home $ 

To help you visualize what you just did, you more or less "double clicked" the Users folder in My Computer. 

Paths
-----

The `/` directory is an important concept in Linux filesystems, sometimes it can be frustrating at first. The key is to understand what an *absolute* filepath is, and what a *relative* filepath is. Once you get that down, you'll be ready to start using the command line with far less frustration.

An example:

    04:04 /home $ cd home/USERNAME
	bash: cd: home/USERNAME: No such file or directory
	
So we got an error message. The error line basically says 

> `bash` told me that the `cd` operation tried to use `home/USERNAME` and failed. Why? `No such file or directory`.

The problem with the above command was because we tried to go to a `home` directory while already inside `/home`. Which means we just tried to navigate to this:

    /home/home/USERNAME
	
Which doesn't exist. The trick is to start *from the root*, and go from there. Starting from the root directory is called using an *absolute* path, because it's absolutely specific.

    04:04 /home $ cd /home/USERNAME
	04:04 ~ $ 
	
But what happens when we are in the directory `/home/USERNAME/my_stuff/pictures/2012/October/halloween_party`, and we want to go back to all the pictures in the `2012` directory?

You could type out `cd /home/USERNAME/my_stuff/...` and so on, but after a while, this eats up a lot of time. That's where *relative* paths come in.

Let's try something new here:

    04:04 ~ $ cd /home
	04:04 /home $ ls
	USERNAME

After listing the directorie in `/home`, it appears that we have only one in there. But every directory has two additional directories, you just can't see them because they're hidden. Try looking at every directory in `/home` by using this

    04:04 /home $ ls --all
	.. . USERNAME
	
The `--all` part is called a *switch*, and switches modify commands. For more on switches, try and see if the command you're using has a built-in `--help` switch to print more info on them. I won't go into those topics just yet.

If you look closely at the output from `ls --all`, you'll notice that they added two new directories: `.` and `..`. These are *relative* directories. The `..` goes back one directory (imagine clicking the "Back" button in Windows when clicking through folders).

    04:04 /home $ cd ..
	04:04 / $ cd ~
	04:04 ~ $ cd ..
	04:04 /home $
	
Here's a little table showing you in a more graphical way what I just did:

    /home/.
	      ^ this means the current directory

	  
	cd ..
 
	/.
	 ^ the current directory is now "up" one from where we were before

	 
	cd ~
 
	/home/USERNAME/.
	               ^ you are here


	cd ..
 
	/home/.
	      ^ we are now back where we started
		  
In case you're wondering, there is a "Forward" button like in Windows too: `cd -`, but it can be confusing, so I'll leave that up to you to try out on your own.

When I said that the `.` means the current directory, I meant it literally. There is absolutely no difference between these two commands:

    04:04 /home $ cd USERNAME

and	

	04:04 /home $ cd ./USERNAME
	
Since `./` was used, it gets replaced with the *current directory*, or `/home`, which ends up being treated as `cd /home/USERNAME`.

If you're like me, you'll use `./` everywhere.


Finally, some Git...
--------------------

Now that you're able to get around a shell, you're ready to start using git. First, go to your home directory, copy and paste this line, then run it:

    git clone https://github.com/Droogans/mysql_tutorial.git
	
> Note: you have to use `ctrl + shift + v` to paste in PythonAnywhere
	
This will make a folder called `mysql_tutorial` in your home directory. Once it's finished, list the files inside of it. Except this time, when you type out the name of the `mysql_tutorial` folder, just type out the first part of the name: `my` or something. Then press `tab`. Bash can figure out the full name for you if there's nothing else with a similar name. This saves a lot of typing, especially for long directory or file names.

    04:04 ~ $ ls ./mysql_tutorial/
	README.md  getting_started  problems  solutions

You'll notice that it looks like a copy of everything on the you see here on github. Although it s technically a copy, it is much more than that. You also cloned all the changes I've ever made to this project, and all of that stuff lives in a hidden folder called `.git`.

    04:04 ~ $ ls -a ./mysql_tutorial/
	.  ..  .git  .gitignore  README.md  getting_started  problems  solutions

Notice that this time I used `ls -a`, instead of `ls --all`. They do exactly the same thing. One is easier to type out, while the other is easier to read.

Whatever you do, don't touch the `.git` folder. If you break it, I can't help you (likely, no one can).


Checking out git
----------------

If you change directories into this new `mysql_tutorial` directory, you should see that git adds a special bit of text to your prompt. It will look something like this:

    04:04 ~/mysql_tutorial (master)$ 
	
What this means is that git is using the *master* branch, or the default main branch. For now, just know that if you see that special colored text, you're looking at a git-versioned project.

Next, take a look at the `problems` directory, and read the file that's in there.

    04:04 ~/mysql_tutorial (master)$ cat ./problems/first_problem.txt
	
Once you've got an answer, use a text editor to write a response. We'll use Nano, because it's pretty similar to a lot of "normal" text editors, like Notepad.

    04:04 ~/mysql_tutorial $ nano ./solutions/first_solution.txt
	
Follow the instructions in the text file, and be sure to save your file once you're finished. If you need more help than what the tips in the editor provide, [Go here][Nano_Help] for some help.
[Nano_Help]: http://mintaka.sdsu.edu/reu/nano.html


Commiting your First Solution
-----------------------------

Now that you've got a solution to the first problem, let's see what git thinks of this:

    04:04 ~/mysql_tutorial (master)$ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#       modified:   solutions/first_solution.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")
	
This will display the changes that you've made to any files that git knows about. Obviously, `first_solution.txt` has been changed, so let's add those changes and make a new version of the project.

    04:04 ~/mysql_tutorial (master)$ git add ./solutions/first_solution.txt
	04:04 ~/mysql_tutorial (master)$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       modified:   solutions/first_solution.txt
	#
		
Notice that git added this file "to be committed". This is also known as "staged". This means that you have prepped it for a commit, but you haven't actually committed anything yet. This is nice becuase you may add a file that you don't actually want to commit, so you can get a second chance to look things over before committing.

Committing is pretty easy. You tell git to commit, and pass it a switch: `-m`, for *message*, or a note to yourself and others about what you did. Here's an example.

    04:04 ~/mysql_tutorial (master)$ git commit -m "solved the St. Ives riddle"
	
As a helpful tip from past experience, *always* describe what you did in a commit message, not what the goal was. A commit message of `"commit first_solution.txt"` isn't helpful. What did `first_solution.txt` need to have that made it worthy of a commit? What prompted the change? What does the change include? These are all more helpful than noting that a change has occured.

Also, always try to keep commit messages to under 80 characters. This is useful for going back and reading a list of changes over time and not having some commit messages be hard to read.

Let's see how we're doing. Ask git if there's any changes.

    04:04 ~/mysql_tutorial (master)$ git status
	# On branch master
	nothing to commit (working directory clean)
	
Good. We have commited everything that we've changed, and nothing needs to be done here.

Once you feel like moving on, go to [using branches][Using_Branches].

[Using_Branches]: https://github.com/Droogans/mysql_tutorial/blob/master/getting_started/using_branches.md