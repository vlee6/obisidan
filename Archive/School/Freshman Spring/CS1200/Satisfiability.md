*Satisfiability computational problem*
**Input:** A boolean formula $\varphi$
**Output:** An assignment $\alpha \in \{0,1\}^n$ such that $\varphi(\alpha)=1$, if such an assignment exists

*CNF Satisfiability computational problem*
**Input:** A CNF boolean formula $\varphi'$
**Output:** An assignment $\alpha \in \{0,1\}^n$ such that $\varphi'(\alpha)=1$, if such an assignment exists

### Resolution
Given literals $\{a,b,c,d\}$ and clause $(a \vee b \vee c \vee d)$
There is exists an equivalent CNF $(a \vee b \vee x) \wedge (\neg x \vee c \vee d)$ where $x$ is some variable. Essentially, the assignment satisfying $(a \vee b \vee c \vee d)$ will also satisfy $(a \vee b \vee x) \wedge (\neg x \vee c \vee d)$ for some $x$.

Given the two clauses $C$ which contains literal $\ell$ and $D$ which contains literal $\neg \ell$ , the **resolvent** between them is the new clause: $$((C-{\ell})\vee(D-{\neg \ell}))$$
### Algorithm to determine satisfiability
The algorithm to determine whether a satisfying assignment exists of a CNF  is as follows:
1. Repeatedly resolve pairs of clauses (ideally in a controlled order). 
2. If the empty clause is generate by a resolution $()$, return false.
3. Otherwise, return true.

![[Pasted image 20260510175324.png]]
### Algorithm to find satisfying assignment
The algorithm to actually find the satisfying assignment is as follows:
Given a set of clauses $C$ that is closed under resolution, meaning that it cannot be resolved further, and does not contain the empty clause $()$.

Construct satisfying assignment $\alpha$ one variable $v$ at a time.
1. If $C$ contains a singleton clause $(v)$, assign $v$ to 1.
2. If $C$ contains a singleton clause $(\neg v)$, assign $v$ to 0.
3. If $C$ contains neither $(v)$ or $(\neg v)$, assign it arbitrarily.

Simplify $C$ with the assignment of $v$ and continue to the next variable.