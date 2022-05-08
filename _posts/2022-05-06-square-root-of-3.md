---
layout: post
title: The Square Root of 3
categories: programming, mathematics, parenting
published: false
---

My youngest son, Thomas, is obsessed with mathematics. His mom was a middle-school math teacher before she was a full-time mom, so he has all the tutoring he needs (for now).

A while back I learned from some blog post or article that you can refine an approximate square root by averaging a too-high guess with a too-low guess.

I tried it out a few months ago with the square root of 2. I used a calculator to check the guesses and average them, but I tracked the process with pencil and paper. I was satisfied when I reached the precision limit of my calculator.

Thomas will often say, “ask me a math question!” So I asked him, “what is the square root of 3?” He didn’t know that one, so we just hit the square root button on the calculator and saw “1.732050807568877”. Thomas started memorizing digits and got to “1.732050807” before I stopped him.

I had a feeling that the square root of three is irrational, so I tried multiplying it by itself on the calculator and of course it came out “3”. Which makes sense if the calculator is at the limit of its precision.

To test my hypothesis (that the square root of 3 is irrational) I thought about busting out the pencil and paper, but the calculator was already at the limit. So it was time to bust out the big guns: Python.

I’ve been writing software for almost twenty years, but I haven’t done much numerical analysis. I knew there were lots of scientific and numeric packages for Python. I found the “decimal” module (Batteries Included&trade;!) and it seemed like it would get us there.

I saw that you could set the precision, but I figured we would work with the default until we knew it wasn’t good enough.

I worked out this little script:

