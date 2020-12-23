---
layout: post
title:  "Rolling Your Own"
date:   2019-06-13 10:22:00 -0600
categories: code coding MAGiE
---

stackoverflow-driven development strikes (me) again.

I copy-pasted some code from a library, perhaps this will look familiar:


{% highlight c# %}

public static IEnumerable<IEnumerable<T>> Batch<T>(
        this IEnumerable<T> source, int size)
{
    T[] bucket = null;
    var count = 0;

    foreach (var item in source)
    {
       if (bucket == null)
           bucket = new T[size];

       bucket[count++] = item;

       if (count != size)                
          continue;

       yield return bucket.Select(x => x);

       bucket = null;
       count = 0;
    }

    // Return the last bucket with all remaining elements
    if (bucket != null && count > 0)            
        yield return bucket.Take(count);            
}
{% endhighlight %}

It worked like a charm.
But I was having slow performance precisely where this code was running.
So I did a [`.ToList()` to force the execution](https://stackoverflow.com/questions/1064043/force-linq-to-not-delay-execution) and put a [System.Diagnostics.Stopwatch](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.stopwatch?view=netframework-4.8) on it.

In my case, I was batching about 450 items into groups of 5 (plus some trim and spacing objects).
The above code took about **80ms**.
Clearly not my performance bottleneck: I was (still am, rarely) seeing many seconds of latency in the UI.
But, now that I had the stopwatch all set up I thought I'd try a straight [LINQ](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/) implementation:

{% highlight c# %}

private IEnumerable<IEnumerable<char>> Batch(IEnumerable<char> bits)
{
    return bits
        .Select((v, i) => new {Index = i, Value = v})
        .GroupBy(x => x.Index / EncodingWidth)
        .Select(g => g.Select(x => x.Value));
}

{% endhighlight %}

This only took **5ms**. Only a savings of **75ms**. But, really, an improvement of ***1,600 %***

This is in game programming, so I'm thinking in frames. The worst case I've yet seen is 16ms of processing per frame. But with a much longer puzzle it would continue climbing.

The best fix I've come up with yet is to put each row of puzzle elements into their own horizontal group. Then add each horizontal group (all at once) to a vertical group. This still has the slow-down to 16ms/frame, but it lasts about 1/13 of the time. (13 elements per row.)

That improvement, combined with the truth that a 90-character-long puzzle is too long and tedious for early levels of the game, will keep our performance playable until we can (and need to) implement the real fix: recycling the a limited number of UI list objects and re-populating them with separate, raw data.

I've been avoiding that because it will be a lot of work that someone has probably already done. So, you can see that I've learned my lesson: I won't be rolling my own scroll-list item recycling code!
