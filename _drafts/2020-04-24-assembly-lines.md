---
layout: post
title: Software Assembly Line
---

We don't work on an assembly line that puts out web sites.
We don't work on an assembly line that puts out web-hosting systems.
We don't work on an assembly line that puts out systems for managing web hosting.
We don't work on an assembly line that puts out new features for systems for managing web hosting.
We work on an assembly line that puts out pull requests.

We might work on an assembly line that puts out microservices. But I don't think so.
Mostly because at BlueHost we're not talking about microservices.

What are the principles of the assembly line?

According to Wikipedia[Assembly Line], the defining characteristics of an assembly line are:
1. The work moves
2. The people stay put, specialization from the division of labor
3. Everything gets automated

Lean Manufacturing or the Toyota Production System take the assembly line as a given. They are not trying to re-model the process of work. Instead, they are optimizations of the existing model.

# Analogy
Let us compare a vehicle assembly line to software development.

The comparison makes more sense if we think about software the way it was sold when I was a kid. i.e. At Software Etc. at the mall.

1. Somehow the software got written.
2. Then, it was released to master, i.e. ready for duplication onto floppies or CD-ROMs.
3. Somewhere, a bunch of copies were made.
4. Those copies were sent to be packaged.
5. The CDs were put into some kind of envelope or jewel case to protect the optical surface.
6. The protected CDs are put in a box which had to be designed, printed, and assembled.
7. Like the softwrae and the box, a user manual had to be written, designed, printed, and brought to the assembly line.
8. Some other promotional material had to be written, designed, and printed.
9. Registration and warranty cards
10. Maybe an insert into the box to keep the CD and paperwork from rattling all around

All this had to be **"assembled"**, shrink wrapped, and then **distributed**.

Distribution had pricing, wholesale agreements, shipping and logistics.

So it's easy to see how software was thought of just like any other product. Even _cars!_

# But then, The Web
But then the internet happened. There were some false starts and missteps. But eventually we figured out that _Web Applications_ were a great way to distribute software. This usurred in the era of **Continuous Delivery**.

This has a lot of other things in common with **assembly lines**. Mostly that whole _"continuous"_ thing.

Assembly lines try to stay in motion. If they keep running smoothly, then cars keep pumping out the other end.

Every car that rolls off the assembly line represents a chunk of revenue and profit.

More cars, more cars, more cars.

Assembly lines are automation. Web servers represent automation.
Imagine the company running the assembly line pumping out shrink-wrapped copies of [Myst](https://en.wikipedia.org/wiki/Myst). Think of all the parts of their assembly line that they were able to automate out of existance:

1. The customer unwrapping the software and installing it. (Double click the installer)
2. The customer picking up the software at the store. (Just go to myst.com and download it)
3. That whole retail situation (Buy direct from the manufacturer)
4. The whole distribution network and logistics. (_Maybe_ a content delivery network. More likely just a big server in a data center somewhere.)
5. Physical packaging
6. The Golden Master (just copy the file to the web server)

That's a pretty good win. How much further up the supply chain can we push this automation thing?

And that brings us to:

# Continuous Delivery
Once we realized that we could avoid installing a release of software on the user's machine and just run everything as a web app, everything really started changing.

First to go was the heavy _Qality Assurance_ cycle. We were less worried about shipping a bug because it could be fixed and then we'd update the web app before most of the users even noticed. Back in shrink-wrap times it would take a whole new release cycle to fix a bug (new golden master, new boxes, new manuals, trucks, stores...).

But even that took too long. So we started releasing more often. More regularly. Until we arrived at this [_continuous delivery_](https://en.wikipedia.org/wiki/Continuous_delivery) concept. Release all the time. As soon as something is ready, release it!

Delivery. Continuous. Automation. It started feeling like an assembly line again.

And that's where the analogy starts letting us down.







What if we were selling shrink-wrapped software? How is this like a car? Let's compare the evolution of software delivery to that of automobile assembly.

## Hand-Crafted
Olden times software was purpose-built, at the site, on the computer.
This is like a group of specialists coming to the garage with a truck load of metal and wood and building a custom one-of-a-kind automobile in the garage of a Czar or something.




What does our end customer buy? In the old days it was a box containing a disk that would install the software on their machine.


Lean manufacturing is based on an assembly line churning out products. Cars. Toyota cars.
Software (lean or otherwise) is not an assembly line.[citation-needed]
So why are we trying to use assembly-line techniques to fix our software processes?

Let's stick with cars, Henry Ford is famous for bringing assembly-line techniques to car manufacturing[Assembly Line]. Reducing the price of automobiles to the point where they were affordable to the mass market.

Before that, car chassis were manufactured and then the bodies were hand-crafted by [coachbuilders](https://en.wikipedia.org/wiki/Coachbuilder).

Long after the Ford made the assembly line famous, small manufacturers were still building low-volume cars by hand. But this practice is so expensive that only expensive niches could be filled. Mostly ultra-luxe, royal-carriage, Rolls-Royce limousine type cars and ultra high-end performance cars.

Some snobs would say that these manufacturing techniques were used because only hand-built cars could meet their exacting standards of performance and luxury. But the real truth is, so few people would end up buying those cars, that building a modern manufacturing program would eat up all the profits. (According to Wikipedia[Coachbuilder], a single die can cost $40,000.)

So, die-making is an up-front capital expenditure. A barrier to entry. It's where the phrase "re-tooling" comes from.

...

Long story short: we _are_ an assembly line, but we're not churning out whole products. We're churning out features, or at least pull requests.


# Kaizen
At a car factory, workers might carry windshields from the place where they are stored to the assembly line when they are ready.
Noticing the wait, someone makes a little cart to take a batch of windshields between the storage area and the assembly line. Then there is only a wait every sixth windshield.

Other optimizations cause the wait every sixth windshield to become the new bottle neck. So they get a second cart and just before the sixth windshield is installed, the second cart arrives ready to be moved quickly into place. And the first cart is taken back to get refilled for next time.

And so on, and so on.

# See Also
[Assembly Line] https://en.wikipedia.org/wiki/Assembly_line
[Toyota Production System] https://en.wikipedia.org/wiki/Toyota_Production_System
[Coachbuilder] https://en.wikipedia.org/wiki/Coachbuilder#Unibody_construction
[Division of Labor] https://en.wikipedia.org/wiki/Division_of_labour
[_Kaizen_] https://en.wikipedia.org/wiki/Kaizen

# Links
## Software Etc.
https://www.flickr.com/photos/thecaldorrainbow/4943608625
https://www.reddit.com/r/nostalgia/comments/5quoav/richard_garriot_aka_lord_british_in_front_of/
