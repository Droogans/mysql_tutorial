
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
neighborhood stoplight. They are controlled by ladder logic, a type of programming that looks less like this:

    if sensor.input.bias > daily_limit:
	    signal.send(signal.STOP)
		
And [more like this][ladder_logic]. I am here to introduce Matt to code that more closely resembles the above.

More about PLCs, and their [importance to the world][Stuxnet].

Matt has heard a lot from his boss about stuff like Linux, databases, web sites and software code. These are things
that Matt uses everyday, but never directly. Hopefully, with the help of this tutorial, Matt can learn how
to use these things in the most efficient manner possible; from the command line.

It may seem daunting at first, but if you consider that at some point, all computers operated from the command line,
it's not such an obscure place to start learning about using computers, and how to manage them.

What is the command line?
-------------------------

Basically, it's that place that Hollywood might convince you that "hackers" do all their work in. 
You know, the black screen with the blinking cursor. I know for a fact that this isn't the case, as I can assure
you, it couldn't be further from the truth. Unfortunately, the stereotype lives on, and I suppose that's how
hackers are still able to find jobs doing penetration tests for Fortune 500 companies three times a year at competetive salaries.
Some can easily get by on a good smile and a USB flash drive, and yet, a brilliant scientists might actually *use*
the command line to submit a patch on the new Mars rover hardware over at NASA. We'll focus on the second of these groups. 

As [a wonderful essay][commandline_essay] has implied, cars can be used as an 
analogy to help demonstrate the subjective differences between operating systems.

The description used to introduce the reader to Linux is as follows, and I feel it is quite humorous:

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

> Prospective station wagon buyer: "I know what you say is true...but...er...I don't know how to maintain a tank!"

> Bullhorn: "You don't know how to maintain a station wagon either!"

It may be a bit of an exaggeration to claim these things, but I intend to show you how you can climb into one of these tanks, with almost no
effort, and hopefully, learn some SQL in the process. From there, it'll be up to you to learn to maintain your station wagon and/or tank.

Are you ready? It's easy, you just need a web browser.

[PLC_wiki]: http://en.wikipedia.org/wiki/Programmable_logic_controller "Wikipedia entry for PLCs"
[Stuxnet]: http://en.wikipedia.org/wiki/Stuxnet#PLC_infection
[commandline_essay]: https://github.com/bibanon/bibanon/wiki/In-the-Beginning-There-was-the-Command-Line
[ladder_logic]: http://www.contactandcoil.com/wp-content/uploads/ladder-logic-for-cat.png

Getting Set Up
==============

There is an incredible website, developed by, [among others][Hansel], a rather...eccentric individual named [Harry Percival][HarryP].
This is a website which allows you to execute Python code in a browser. Certainly they will change name of the site in the future, as 
this entire tutorial uses a 'Python' service to execute SQL statements in a built-in MySQL environment, and also utilizes Bash. 
Eventually, Python will become just another environment they offer in their service. And what a wonderful service it is.

Note: For the beginner, MySQL is "the database", and Bash is "Linux". Neither of these statements are correct...just go with it for now.
Python is beyond the scope of this tutorial, but if they named a website after it, it certainly must be a [Good Thing][Python].

To get setup, make sure you have an email account that you're comfortable using for an online service. Done?

Ok, next thing you need to do: visit this website: https://www.pythonanywhere.com/registration/register/free/

Once you've registered, you should see something along the lines of [this][PythonAnywhereConsoles].

You're just about ready to begin.

[HarryP]: http://www.youtube.com/watch?v=e6NLAbgmRZ4&t=189
[Hansel]: http://www.aychedee.com/2012/04/19/browser-based-consoles-for-the-ipad/
[PythonAnywhereConsoles]: http://www.aychedee.com/static/pythonanywhere-console-nav.png
[Python]: http://docs.python.org/2/tutorial/



*TODO*
-----
- Required:
 - Setting up PythonAnywhere
 - Using Bash (`.bashrc`, `export EDITOR=emacs`)
 - Using an editor (`mysql> edit`)
 - Using git
- Optional:
 - Setting up dropbox
 
*META*
------
- Stop developing on master once the intial commit is finished
 - make a branch for every lesson; end the master branch on switching branches
