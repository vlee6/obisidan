Very similar to [[RAM Model]] but with the addition of word length $w$ and memory size $S$.
- $w$ is some fixed integer
- $S$ is a variable that can be incremented by one with `MALLOC`. Upon initialization $S=n$.

The value of a memory cell and variable must be $\leq 2^w-1$.
Memory is now an array of length $S$. Reads are writes from memory locations larger than $S$ have no effect.

For arithmetic operations $var_3=var_{2} \text{ op } var_3$, the result is capped at $2^w-1$.
Output is capped at $S$, as in if the program halts, output ends at $M[\min \{ \texttt{output-ptr} + \texttt{output-len} - 1, S-1 \}]$.

A Word-RAM program $P$ crashes on input $x$ and word length $w$ if any of the following occur:
1. One of the constants $c$ in the assignment commands (`var = c`) in $P$ is $\geq 2^w$
2. $x[i]$ $\geq 2^w$ for some $i \in [n]$
3. $S > 2^w$

The runtime of a Word-RAM program $P$ is the number of commands executed until $P$ halts or crashes.