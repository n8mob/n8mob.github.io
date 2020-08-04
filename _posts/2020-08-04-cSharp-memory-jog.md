---
layout: post
title: Jogging my C# Memories
---

I've been writing Python at work lately - a web service using Django. Before that, I was doing Java for a few years. Java and Python will both let you reference a class member through an instance variable. In C# that's a compile error.

# An Example
```c#
using System;

class Foo {
  public static string bar = "baz";
}

class MainClass {
  public static void Main (string[] args) {
    Foo f = new Foo();
    try
    {
      Console.WriteLine(f.bar);
    } catch {
      Console.WriteLine("Actually, this is a compile error and can't be caught.");
    }
  }
}
```

