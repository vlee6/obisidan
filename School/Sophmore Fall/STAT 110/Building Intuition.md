**How many ways are there to split a dozen people into 3 teams, where one team has 2 people, and the other two teams have 5 people each?**

Guess: There are $\binom{2}{12}\binom{5}{10}\binom{5}{5}$
Solution: There are $\frac{\binom{2}{12}\binom{5}{10}\binom{5}{5}}{2}$ since we overcount by a factor of 2 since the order of teams of 5 don't matter.

**How many ways are there to split a dozen people into 3 teams, where each team has 4 people?**

Guess: There are $\frac{\binom{12}{4})\binom{8}{4}\binom{4}{4}}{\binom{3}{1}\binom{2}{1}\binom{1}{1}} = 5775$

We overcount by the number of times its possible to arrange three groups.

**ELK**
In the denominator, we have all possible samples of elk of size $m$.
In the numerator, we want to find the number of samples of elk such that exactly $k$ of those elk were tagged.

$\binom{n}{k}$ k tagged from the n of tagged
$\binom{N-n}{m-k}$ the rest of them, selected from the untagged
$\binom{N-n}{n}$

$$
\frac{
\binom{n}{k}
\binom{N-n}{m-k}
}{
\binom{N}{m}
}
$$

Think about these things in the form of combinations. There are $N$ choose $m$ possible combinations of elk. There are $m$ choose $k$ possible combinations of $k$ tagged before. Etc.


**Time slots**
What is the probability of rolling a ten sided die 3 times and getting two or more of the same number.


$$
1- \frac{10*9*8}{10^3}
$$

**5 Card Poker Hands**

Royal flush
$$
\frac{
\binom{4}{1}\binom{13}{5}
}{\binom{52}{5}}
$$

Two pair
$$
\frac{
\binom{13}{1}\binom{4}{2}\binom{13}{1}\binom{4}{2}
}{\binom{52}{5}}
$$