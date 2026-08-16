Given a set of variables $x_1,x_2,...,x_{n} \in [0,1]$, we construct a boolean formula $\varphi$ with the following operations:
- $\neg$ (not)
- $\wedge$ (and)
- $\vee$ (or)

For example:
$$\varphi_{palindrome}(x_0,x_1,x_2,x_3) = (
(x_{0} \wedge x_{3}) \vee
(x_{0} \wedge \neg x_{3}) \vee
((x_{1}\wedge x_{2)}) \vee
(\neg x_{1}\wedge x_2)
)$$
Which equals 1 if input is palindrome (ie. $x_0=0,x_1=1,x_2=1,x_3=0$)

### Terminology
**Literals**
Variables or negations of variables $(x_i, \neg x_i)$

|             | Description     | Example                  | Example 2                                                  |
| ----------- | --------------- | ------------------------ | ---------------------------------------------------------- |
| **Terms**   | AND of literals | Literal $\wedge$ Literal |                                                            |
| **Clauses** | OR of literals  | Literal $\vee$ Literal   |                                                            |
| **DNF**     | OR of terms     | Term $\vee$ Term         |                                                            |
| **CNF**     | AND of clauses  | Clause $\wedge$ Clause   | (Literal $\vee$ Literal) $\wedge$ (Literal $\vee$ Literal) |

Given any function that takes in bits as input and outputs a bit, it can be represented by a CNF or DNF.