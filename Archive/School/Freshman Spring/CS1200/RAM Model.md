### Program
A program in a ram model is a set of variables (registers) and commands (lines of code). Programs can access memory, an infinite array that stores natural numbers.

$P: (V, C_{0},\dots,C_{n-1})$

Variables store natural numbers such as `var = 0`.
Commands:
	- Assignment: `var = C` {`var` $\in V$, `C` $\in \mathbb{N}$}
	- Arithmetic: $var_{1} = var_{2} \text{ op } var_{3}$, where $\text{op}$ is either $+,-,\times,\div$
	- Read from memory: $var_{1}=M[var_{2}]$
	- Write to memory: $M[var_{1}]=var_{2}$
	- Conditional GOTO: `IF var == 0 GOTO k`, where`k` is some line number

There are some special variables that are automatically created upon initialization: `input-len`, `output-ptr`, `output-len`.

Output starts at memory location `M[output-ptr]` and ends at `M[output-prt + output-len - 1]`. Input starts at `M[0]` and ends at `M[input-len - 1]`

Commands are executed in order ($C_{0}, C_{1},C_{3},\dots$) with the exception of conditional GOTO commands.

Runtime of a RAM program $p$ on input $x$ ($T_p(x)$) is the # of lines of code/commands executed (**NOT** the number of lines of code) and could potentially be infinite.

- Notice that we can only only preform arithmetic operations between variables. If you want to use the value of a number, you must first define it as a variable (ie. `zero = 0`).
- Notice that there is no such thing as < or > in a RAM program.
- Whenever inserting new lines of code for a simulation-style proof, don't forget to update GOTOs accordingly.