---
layout: post
title: On Dependency Injection
---

# SOLID

## Single Responsibility

## Open-Closed
"Open" for extension, "Closed" for modification
In other words, it should be easy to add functionality to the system without modifying existing code.

## Liscov Substitution
All sub-types should be drop-in replacements.

## Interface Segregation
(Funny: I thought it was for Inversion of Control, which is basically the same as [Dependency Injection](#dependency-injection)).

Instead, interfaces should be small and compose-able.

and last, but not least:

## Dependency Injection
Instead of configuring and wiring up our **dependencies**, we allow them to be **injected**.

This is made much easier with the use of well-defined interfaces.

### An example: Panic Button
Instead of using a toggle switch to activate a blink circuit wired to a flashing light, we tell the boss: I need a panic button.

Then, the boss hands you a button.

It's up to the boss if the button:
- Flashes a light on a control panel
- Rings a bell at the fire station
- Pages the on-call team, or
- Sends a cell-phone call to ***The Wolf***."

(You're sending The Wolf? $#@!, Negro - that's all you had to _say!_)

We _depend_ on that button working. But we _invert_ who _controls_ it and let them _inject_ it into our system.

The part that confuses **me** is that when we are writing software, **we** are:
- The panickers who want to press the button,
- The boss who supplies the button,
- The on-call team responding to the button, and
- The technicians who install the button.

So it gets fuzzy if we can't imagine which part of our software represents which of the different roles.

(We are not, however, _The Wolf_; That's Harvey Keitel.)

![Harvey Keitel as Winston Wolfe]({{ site.url }}/assets/mrwolf-ls-coffee.jpg).

