**March 1, 2017**

In the latest homework for my Algorithms class, we had a series of questions dealing with the [Minimum Vertex Cover](https://en.m.wikipedia.org/wiki/Vertex_cover) (or "MVC") problem. It's an [NP-complete](https://en.m.wikipedia.org/wiki/NP-completeness) problem, which means there exists no algorithm which finds an optimal solution in polynomial time.

**Remark.** *Polynomial Time.* Refers to some function $f$ such that $f(n) = \mathbf O (n^c)$ where $c \in \mathbb{R}$ as $n \rightarrow \infty$.

In the context of the homework, we were supposed to test out two other algorithms' solutions and compare them to an optimal solution. This, of course, involves computing an optimal solution. We weren't asked to test them on graphs $G = (V, E)$ where $|V| \leq 10$ - the first graph we computed was a randomized algorithm-generated graph where $|V| \leq 2^{20}$. Bear in mind that the largest storable integer is $2^{31} - 1$. For the sake of context, let's see the number in both base-10 and base-2.

$$ (2^{31} - 1)_{(10)} =  2147483647 $$

$$ (2^{31} - 1)_{(2)} = 1111111111111111111111111111111 $$

That's right... 31 ones. Hold onto this concept, as it'll come in handy later.

Anyway, it's easy-ish for humans to correctly identify a minimum vertex covering, especially when we have a picture of a graph in front of us. However, when the number of vertices is huge, we want to use a computer. When we use computers, though, we have to figure out an algorithmic or "generic" way to generate a solution for *all* instances of the problem. With MVC, it's been proven that there is **no** algorithm that can produce the optimal solution in polynomial time (which makes this problem NP-complete). We have some approximate algorithms, but testing them involves finding the actual optimal solution.

An optimal solution $ S \subseteq V $ to the MVC is bound by two constraints:

1. The set is a vertex covering.
2. The set is of smallest size.

The first constraint is easily verifiable. If we have a set $ K \subseteq E $ such that $\forall (u, v) \in K \ \big| \ u \in S \ \lor v \in S$, then $K$ is a vertex covering. However, (2) is much harder. To verify this constraint, we actually have to *create* all the individual subsets of $E$ and then check to see which vertices we can pick out to make a minimum vertex cover.

This is easier said than done, however. What we're generating is called a [Power Set](https://en.m.wikipedia.org/wiki/Power_set). If we have a set $S$, the power set of $S$ is the set of all subsets of $S$. For all sets, the size of the power set is $2^n$, where $n$ is the size of the set (think about it - each member of the set can either be in or not in any given subset).

For example, if we have a set $ Q =\{A, B, C\} $, $ |Q| = 3 $ the power set is:

$$ \wp(Q) = \big\{ \{\emptyset\}, \{A\}, \{B\}, \{C\}, \{A, B\}, \{A, C\}, \{B, C\}, \{A, B, C\} \big\} $$

$$ | \wp (Q) | = 8 = 2^3$$

And since we know that there are $2^n$ subsets, is there some connection we can make between the representation of subsets and numbers themselves?

Yes, there is. And to find it, we look to binary.

Think about numbers themselves. $\forall n \in \mathbb{N}$, $n$ is represented uniquely. And since base-2 is just a different base, the same holds for all base-2 representations of the natural (and, as it turns out, all) numbers.

Take a look at the numbers 0 - 7:

$$ 0_{(2)} = 000 $$

$$ 1_{(2)} = 001 $$

$$ 2_{(2)} = 010 $$

$$ 3_{(2)} = 011 $$

$$ 4_{(2)} = 100 $$

$$ 5_{(2)} = 101 $$

$$ 6_{(2)} = 110 $$

$$ 7_{(2)} = 111 $$

Can you see the connection from $ \wp (Q) $ to these binary numbers? There is actually a one-to-one correspondence between the power set and these numbers. A $1$ indicates the presence of an element and a $0$ indicates the absence of an element. Since each number (or subset) is unique, and there are the same number of subsets in $ \wp (Q) $ and the numbers $[0, 2^n - 1]$, and each subset is of the same size as its morphism, we can establish an isomorphism.

$$ M: \wp (Q) \twoheadrightarrow [0, 2^n - 1]$$

We can find all the subsets pretty easily! Turns out that it's computationally simple, but it still takes $\textbf O (2^n)$ time. We also want to provide some lower bound of the subsets we need to check. The idea behind this is that if some set $K \subseteq V$ is not a vertex cover, no set $k \subseteq K$ can be a cover, either.

For this algorithm, we have an input set of vertices $V$.

```
bruteForceBinary(V):

	covers := set of vertex covers
	k := 0
	
	for a := 2^n - 1 to 2^{n - 1} - 1:
	
		if a > k:								// (1)
			i := a
			
			while i > k:
				bits := binary(i)
				set	:= make subset out of bits
				
				if set is a cover:
					sets.add(set)
				else:
					k := i						// (2)
				
				i := ceil(i / 2) - 1			// (3)
		
		else:
			break
			
	sort(sets)
	return sets[0] 	// returns smallest vertex cover	
```

We start out by iterating backwards from $2^n - 1$, which will always be a string of ones that has $n$ ones in it ($7_{(2)} = 111, \ n = 3$), which represents the largest subset of $V$ (which is, incidentally, $V$). in `(2)`, we progressively remove one element from the set by dividing by two ($ \lfloor \frac 72 \rfloor = 3, \ 3_{(2)} = 011)$. We can do this until we run into a set where the set is *not* a cover, where we then set the lower bound to $i$, so that we don't search any subsets below it.

This holds for all iterations $i \in [2^{n - 1} - 1, 2^n - 1]$. Additionally, resetting this bound guarantees that we will find the minimal subset. On the average case, we will only take $\log_2 n $ steps per iteration $i$, which leads to:

$$ \textbf O (n \cdot \log_2 n) = \textbf O (\log_2 n^n)$$

This helps greatly with efficiency; the average runtime of this algorithm on a graph of size $2^{20}$ was just over a second.

#end