**February 14, 2016**

First of all, happy Valentine's Day! It was a great day to spend with friends and family, and I enjoyed it.

Anyway, I was on the bus to a hockey game yesterday when I started writing out the way I'd use to figure the probability of a team winning a game against another.

Here's my method:

$gf_i = $ goals for/game for team i

$ga_i = $ goals against/game for team i

$gf_i + ga_i = ag_i = $ average number of goals in a game team i plays

$\frac{gf_i}{ag_i} = $ probability that team i will score $gf_i$ goals in a game where $ag_i$ goals are scored

So we have our basic parameters. Let's go with teams a and b, where $P(A)$ is the probability that team a wins, given $gf_a \ge gf_b$:

$$P(A) = \frac{gf_a}{ag_a} - \frac{gf_b}{ag_b} + \frac12 $$

So for a practical (but very simple) example, suppose:

$$ gf_a = 3, \ ga_a = 2 \rightarrow ag_a = 5 $$
$$ gf_b = 2, \ ga_b = 3 \rightarrow ag_b = 5 $$

The fact that both teams score the same amount of goals per game could lead one to believe that the matchup will be even, but we are overlooking the fact that team b has more goals scored *on them* per game than team a does. We have to make the each fraction proportional by setting the denominators to be equal; this way, we can correctly figure the probability.

$$ \frac{gf_a}{ag_a} - \frac{gf_b}{ag_b} + \frac12 = \frac35 - \frac25 + \frac12 = \frac{7}{10} $$

From here, we choose a random number $n$ in the range $0 \ ... \ 10 $, and if $ 0 \leq n \leq 7 $, team a is the winner of the game. Otherwise, team b wins.
