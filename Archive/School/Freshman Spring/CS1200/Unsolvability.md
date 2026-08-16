Unsolvable problems
1. Halting Problem, given $(P,x)$ `yes` if $P$ halts on $x$, `no` otherwise
2. Halts on Empty
3. HaltingProblem RAM/WRAM

If $A \leq B$ (A reduces to B)
Since $A$ is a known unsolvable problem, $B$ must also be an unsolvable problem. Otherwise, we could solve $A$ with the oracle solving $B$.

A common template is:
1. Construct some program $Q$
	- $Q$ must run $P/P'$ on $x/\epsilon$
	- Do something
2. Run $B$ on program $Q$
3. Convert $B's$ output to `yes` and `no`

The idea is that $B$ does something if and only if $P$ halts. So if $B$ does something, then we know that $P$ must halt.