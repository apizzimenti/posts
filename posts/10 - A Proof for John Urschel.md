**September 29, 2016**

So there's a mathematics PhD student at MIT named John Urschel. For
anyone that seems to vaguely remember his name, he's also a guard
for the Baltimore Ravens.

He publishes to *The Player's Tribune*, a platform that gives 
a voice to athletes who are, oftentimes, judged only by their
performance in sport and their extracurricular endeavors.

In any case, Urschel posts weekly math challenges to try and
get readers of the *Tribune* to engage their math brains. I'm
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
the deck), the sample space $C$ shrinks by one outcome. Now, the
 $C$ only has 51 possible outcomes. The probability of
picking the King of Spades is $ \frac{1}{51} $.

This example illustrates *independent* and *mutually exclusive*
events. Since you can't pick a King of Hearts and then another
King of Hearts, the event outcomes don't intersect.

However, when flipping two coins, it's a bit different.

Even though each flip doesn't depend on the outcome of the other
flips, the outcomes are not mutually exclusive.

Let's explore the proof!

\newcommand{\cc}[1]{\begin{center}#1\end{center}}
\newcommand{\prob}[1]{\mathbf{P}(#1)}
\newcommand{\pp}[1]{#1^{\prime}}

\newtheorem{theorem}{Theorem}[section]
\newtheorem{corollary}{Corollary}[theorem]
\newtheorem{lemma}[theorem]{Lemma}

\begin{abstract}
		This document explores the inference behind the probability of two events occurring that are \textit{independent} but not \textit{mutually exclusive} (i.e. \textit{mutually inclusive}). For the examples of these proofs, we will use this prompt: \\
		\begin{addmargin}[10em]{10em}
			\textbf{If two coins are flipped, what is the probability that, if one coin turns up heads, that the other also turns up heads?} \\
		\end{addmargin}
		
This problem will be addressed and used to describe the reasoning behind the probability of two events that are independent but mutually inclusive.
\end{abstract}
    
    \section{Introduction}
        \cc{Define an sample space $E$ as the set of all possible outcomes for an event $E$. Also define the function $\prob{x}$ as the probability of a given event $x$.}
    
    \begin{lemma}
        \cc{Given an sample space $A$ and an sample space $B$ such that $ A \cap B \not= \emptyset $ and $ A \cup B \subset E$:}
        $$ \prob{A \cup B} = \prob{A} + \prob{B} - \prob {A \cap B} $$
    \end{lemma}
    
    \begin{lemma}
        \cc{Given an sample space $A$ and and event $B$ such that $ A \cap B \not= \emptyset $, $\pp{A} = A \setminus B$ and $ \pp{B} = B \setminus A $ (i.e. sets $\pp{A}$ and $\pp{B}$ are disjoint), and $ A \cup B \subset E $:}
        $$ \prob{A \cup B} = \prob{\pp{A}} + \prob{\pp{B}} + \prob{A \cap B} $$
    \end{lemma}
    
    \begin{lemma}
        \cc{The probability of any given outcome in $E$ is $1$ over the cardinality of $E$:}
        $$ P(x) = \left\{ \forall x \in E \ \big| \ \frac{1}{|E|} \right\} $$
    \end{lemma}
    
    \begin{lemma}
        \cc{The cardinality of a set $X$ is equal to the sum of the cardinalities of its disjoint subsets:}
        $$ X = \bigcup \left\{\forall x, \ y \in X : x \cap y = \emptyset \big| x \right\} \rightarrow |X| = \sum \left\{\forall x, \ y \in X : x \cap y = \emptyset \Big| |x| \right\} $$
    \end{lemma}
    
    \begin{lemma}
        \cc{The probability of an event $A$ given that an event $B$ has occurred can be defined as:}
        $$ \prob{A | B} = \frac{\prob{A \cap B}}{\prob{B}} $$
    \end{lemma}
    
    \section{Proof with Sets}
    
        \begin{proof}
            \cc{Let the set $E$ represent all possible outcomes of the two coin flips from the initially posed question:}
        
            $$ E = \text{\{HH, TH, HT, TT\}} $$
            
            \cc{Let $ A \cup B \subset E $ such that }
            $$ A = \{\text{HH}\} $$
            $$ B = \{\text{TH, HT, HH}\} $$
            \cc{$A$ represents the outcomes with only two heads and $B$ represents the outcomes with at least one head.}
            
            \cc{In order to effectively demonstrate probabilities, we will make these sets disjoint:}
            $$ \pp{A} = A \setminus B = \{\}, \ \pp{B} = B \setminus A = \{\text{TH, HT}\}$$
            
            \cc{By creating disjoint subsets, we can calculate $\prob{A \cup B}$ using Lemma 1.2:}
            $$ \prob{A \cup B} = \prob{\pp{A}} + \prob{\pp{B}} + \prob{A \cap B} $$
            
            \vspace{1mm}
            
            \cc{Let us build off of Lemma 1.1 with Lemma 1.4 in mind:}
            
            $$ \prob{A} = \prob{\pp{A}} + \prob{A \cap B} \rightarrow \prob{\pp{A}} = \prob{A} - \prob{A \cap B} $$
            $$ \prob{B} = \prob{\pp{B}} + \prob{A \cap B} \rightarrow \prob{\pp{B}} = \prob{B} - \prob{A \cap B} $$
            
            \vspace{2mm}
            
            \cc{Substituting into Lemma 1.2, we can derive Lemma 1.1:}
            \begin{align*}
                \prob{A \cup B} &= \prob{\pp{A}} + \prob{\pp{B}} + \prob{A \cap B} \\
                &= (\prob{A} - \prob{A \cap B}) + (\prob{B} - \prob{A \cap B}) + \prob {A \cap B} \\
                &= \prob{A} + \prob{B} - 2\prob{A \cap B} + \prob{A \cap B} \\
                \text{Lemma 1.1} &= \prob{A} + \prob{B} - \prob{A \cap B}
            \end{align*}
            
            \vspace{2mm}
            
            \cc{Using Lemma 1.3, we can say that the probability of any given outcome in $E$ is $ \frac1T$, where $ T = |E| $. From this, we can recall Lemma 1.4 and say that the probability of an event $X$  such that $ X \subset E $ is the sum of the probabilities of its disjoint subsets: i.e. $ \prob{X} = \frac{|X|}{T} $.}
            
            \cc{We can now substitute values into our original expression involving disjoint subsets to determine the probability that any given outcome will contain an H:}
            
            \begin{align*}
                \prob{A \cup B} &= \prob{\pp{A}} + \prob{\pp{B}} + \prob{A \cap B} \\
                &= \frac{|\pp{A}|}{T} + \frac{|\pp{B}|}{T} + \frac{|A \cap B|}{T} \\
                &= \frac04 + \frac24 + \frac 14 \\
                &= \frac34
            \end{align*}
            
            \cc{Now that the probability of a given outcome containing a head has been calculated, we can utilize Lemma 1.5 in calculating the probability that one coin flip is a head given that the other coin flip is a head. Let $H$ be the event that one head has occurred, and $HH$ be the event that two heads have occurred:}
            
            \begin{align*}
                \prob{HH | H} &= \frac{\prob{HH \cap H}}{\prob{H}} \\
                &= \frac{\prob{A \cap B}}{\prob{A \cup B}} \\
                &= \frac{\frac14}{\frac34} \\
                &= \frac13
            \end{align*}
            
        \end{proof}
        
        \section{Proof with Combinatorics}
        
            \begin{proof}
                
                \cc{We can begin by defining the total number of outcomes. For each of the two positions, there are two possible outcomes:}
                $$ 2 \cdot 2 = 2^2 = 4 $$
                
                \cc{From this, we can determine the probabilities of each outcome that contains a head:}
                $$ \pp{H} = \{HT, TH\} $$
                $$ HH = \{HH\} $$
                
                \begin{align*}
                    \prob{H} &= \prob{\pp{H}} + \prob{HH} \\
                    &= \frac{2 \cdot 1}{4} + \frac{1 \cdot 1}{4} \\
                    &= \frac34
                \end{align*}
                
                \cc{Knowing the probability of $HH$ is $\frac14$, we can leverage Lemma 1.5:}
                
                \begin{align*}
                    \prob{HH | H} &= \frac{\prob{HH \cap H}}{\prob{H}} \\
                    &= \frac{\frac14}{\frac34} \\
                    &= \frac13
                \end{align*}
                
                
            \end{proof}
