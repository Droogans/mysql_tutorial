
About
=====

I am creating a simple database with a small subset of data to help teach my brother SQL.

I will do my best to ensure you can duplicate everything I show him with as little help as possible.

Before I Begin
==============

I would like to identify my target audience, who I will refer to as Matt. Matt works with Windows, in
a GUI-based development application writing logic for [PLCs][PLC_wiki], a very compact and fast method
of determining, among things, safety violations in machine-automated environments. These things run safety 
stops when light curtains are breached, saving folks the risk of death and dismemberment when accessing 
live running machines in the modern workplace. PLCs also, usually, are in charge of signaling your friendly
neighborhood stoplight!

More about PLCs, and their [importance to the world][Sutxnet].

Matt has heard a lot from his boss about stuff like Linux, databases, web sites and software code. These are things
that Matt uses everyday, but never directly. Hopefully, with the help of this tutorial, Matt can learn how
to use these things in the most efficient manner possible: from the command line.

It may seem daunting at first, but if you consider that at some point, all computers operated from the command line,
it's not such an obscure place to start learning about *actual* computers, and how to operate them.

What is the command line?
-------------------------

Basically, it's that place that Hollywood might convince you that "hackers" do all their work in. 
You know, the black screen with the blinking cursor. I know for a fact that this isn't the case, as I can assure
you, it couldn't be further from the truth. Unfortunately, the stereotype lives on, and I suppose that's how
hackers are still able to find jobs doing penetration tests for Fortune 500 companies three times a year at competetive salaries.
Some can easily get by on a good smile and a USB flash drive, and yet, a brilliant scientists might actually *use*
the command line to submit a patch on the new Mars rover hardware over at NASA. We'll focus on the second of these groups. 

As a wonderful essay has implied, cars can be used as an analogy to help demonstrate the subjective differences operating systems.

The description used to introduce the reader to Linux is as follows, and I feel is quite humorous:

> Linux ...[the dealership]... which is right next door, and which is not a business at all. It's a bunch of RVs, yurts, tepees, and 
> geodesic domes set up in a field and organized by consensus. The people who live there are making tanks. These are not old-fashioned, 
> cast-iron Soviet tanks; these are more like the M1 tanks of the U.S. Army, made of space-age materials and jammed with sophisticated 
> technology from one end to the other. But they are better than Army tanks. They've been modified in such a way that they never, ever 
> break down, are light and maneuverable enough to use on ordinary streets, and use no more fuel than a subcompact car. These tanks are 
> being cranked out, on the spot, at a terrific pace, and a vast number of them are lined up along the edge of the road with keys in the 
> ignition. Anyone who wants can simply climb into one and drive it away for free. 

> The group giving away the free tanks only stays alive because it is staffed by volunteers, who are lined up at the edge of the street with 
> bullhorns, trying to draw customers' attention to this incredible situation. A typical conversation goes something like this:

> Hacker with bullhorn: "Save your money! Accept one of our free tanks! It is invulnerable, and can drive across rocks and swamps at ninety 
> miles an hour while getting a hundred miles to the gallon!"

It may be a bit of an exaggeration to claim these things, but I intend to show you how you can climb into one of these tanks, with almost no
effort, and hopefully, learn some SQL in the process. 

Are you ready? It's easy, you just need a web browser.

[PLC_wiki]: http://en.wikipedia.org/wiki/Programmable_logic_controller "Wikipedia entry for PLCs"
[Stuxnet]: http://en.wikipedia.org/wiki/Stuxnet#PLC_infection

Getting Set Up
==============





*TODO*
-----
- Required:
 - Setting up PythonAnywhere
 - Using Bash (`.bashrc`, `export EDITOR=emacs`)
 - Using Emacs (`mysql> edit`)
 - Using git
- Optional:
 - Setting up dropbox
 
*META*
------
- Stop developing on master once the intial commit is finished
 - make a branch for every lesson; end the master branch on switching branches
