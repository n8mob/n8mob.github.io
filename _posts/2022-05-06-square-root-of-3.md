---
layout: post
title: The Square Root of 3
categories: programming, mathematics, parenting
---

A few months ago learned from some blog post or article that you can refine an approximate square root by averaging a too-high guess with a too-low guess.

I tried it out with the square root of 2. I used a calculator to check the guesses and average them, but I tracked the process with pencil and paper. By the time that I reached the precision limit of my calculator, I was convinced that I could have done it as a student at the [Massachusetts Bay Colony Institute of Technological Arts](https://en.wikipedia.org/wiki/The_Baroque_Cycle).

My youngest son, Thomas, is obsessed with mathematics. His mom was a middle-school math teacher before she was a full-time mom, so he has all the tutoring he needs (for now).

Thomas will often say, “ask me a math question!” So I asked him, “what is the square root of 3?” He didn’t know that one, so we just hit the square root button on the calculator and saw “1.732050807568877”. Thomas started memorizing digits and got to “1.732050807” before I stopped him.

I had a feeling that the square root of three is irrational, so I tried multiplying it by itself on the calculator and of course it came out “3”. Which makes sense if the calculator is at the limit of its precision.

To test my hypothesis (that the square root of 3 is irrational) I thought about busting out the pencil and paper, but the calculator was already at the limit, so it wouldn't really help us with the verification calculation. So it was time to bust out the big gun: Python.

I’ve been writing software for almost twenty years, but I haven’t done much numerical analysis. I knew there were lots of scientific and numeric packages for Python. I found the “decimal” module (Batteries Included&trade;!) and it seemed like it would get us there.

I saw that you could set the precision, but I figured we would work with the default until we knew it wasn’t good enough.

I worked out this little script:

```python
decimal.getcontext().prec = 1000

representation = '1.732050807568877293527446341505872366942805253810380628055806979451'

previous_candidate = 0
for next_digit in range(10):
    r = representation + str(next_digit)
    candidate = decimal.Decimal(r)
    candidate_result = candidate * candidate

    print(f'{r} = {candidate * candidate}')

```

I would then hit "play" in [PyCharm](https://www.jetbrains.com/pycharm/) and see the next ten options and choose the largest one that didn't go over 3.0...

Of course it was not so smooth at the beginning, but we were getting in the groove and Thomas said, "this is cool!"

As the script got into its final form I stopped taking notes and just added the next digit to `representation`, hit play, note the next digit for which the result was less than 3.0, type it in, and hit play again.

At some point we ran out of digits on the print of the result so I looked up the default precision and learned that we were at exactly that many digits! So I added that line about `decimal.getcontext().prec = 1000`

By the time I got bored we had already gotten to, like 170 digits.

At that point I said, "I'm fairly certain that the square root of 3 is irrational." So we looked that up and someone had indeed proved it, but I didn't have the patience to read the proof. So we found [a million digits](https://apod.nasa.gov/htmltest/gifcity/sqrt3.1mil) and verified that our 170 matched!

```python
    representation = '1.73205080756887729352744634150587236694280525381038062805580697945193301690880003708114618675724857567562614141540670302996994509499895247881165551209437364852809323190230558'
```

I think my six-year-old son was right: this _is_ cool!
