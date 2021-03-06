**September 29, 2016**

So there's a mathematics PhD student at MIT named John Urschel. For any football fans,
he's also a guard for the Baltimore Ravens.

In any case, Urschel posts weekly math challenges to try and
get readers of *The Player's Tribune* to engage their math brains. I'm
specifically responding to the third question in
[this post.](http://www.theplayerstribune.com/john-urschel-morning-math-challenge-week-2/)

Initially, the answer seems counterintuitive and wrong. The
coin flips are independent, right? The probability of either flip
doesn't depend on the outcome of the other flip; this is true.
However, this doesn't mean that the
events are *mutually exclusive*. What do I mean by mutually exclusive?

> Mutually exclusive events are events that cannot happen at the
same time.

For any given event $E$, $E$ has what's called a [*sample space*](https://en.wikipedia.org/wiki/Sample_space).
A sample space is, at its simplest, a list of all the outcomes of $E$.
These sample spaces are expressed using [*sets*](https://en.wikipedia.org/wiki/Set_(mathematics)).
Sets are a way to group items (numbers, shapes, names, etc.) so
each element is unique.

So, if you consider the event $C$ picking a card out of a standard
52-card deck, then the sample space of $C$ is as such:

$$ C = \text{{Ace of Clubs, 2 of Clubs, 3 of Clubs, ... , King of Hearts}} $$

Now, what's the probability of picking, say, a 10 of Diamonds out of this
deck? Since the sample space $C$ contains 52 possible outcomes,
and there's only one 10 of Diamonds in the deck, the probability
is (you guessed it) $ \frac{1}{52} $.

After you've picked out the 10 of Diamonds, there are 51 cards left. Since
you've removed the possibility of picking another 10 of Diamonds
(since another one doesn't exist and you picked the only one from
the deck), the sample space $C$ shrinks by one outcome. Now,
 $C$ only has 51 possible outcomes. The probability of
picking any other card, say, the King of Spades, is $ \frac{1}{51} $.

This example illustrates *independent* and *mutually exclusive*
events. Since you can't pick a King of Hearts and then another
King of Hearts, the event outcomes don't intersect.

However, when flipping two coins, it's a bit different.

Even though each flip doesn't depend on the outcome of the other
flips, the outcomes are not mutually exclusive.

[Let's explore the proof!](https://www.dropbox.com/s/mnut8z7ffxkkz8e/Ind_Events_Pf.pdf?dl=0)
