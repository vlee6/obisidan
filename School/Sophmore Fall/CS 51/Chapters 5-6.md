### Variables
Ocaml syntax is sort of similar to Nix.

`let [varaible name] : [type] in [body of expression]`
```ocaml
let pi : float  = 3.1416 in
pi  *. 2. *. 2. ;;
```

The `let` expression is a binding construct since it binds a variable name to a value for use in the body of the expression.

Unlike other programming languages, you can't change the value of variables. It remains the same throughout the entire body of the expression.

We can also just let Ocaml infer the variable's type.

```ocaml
let pi  = 3.1416 in
pi  *. 2. *. 2. ;;
```

Let expressions, like all expressions in Ocaml, have values.

```ocaml
3.1416 * (let radius = 2. in radius *. radius) ;;
```

Variables also have scope, they can't exist outside of the body of the expression that they are binded to (ie. the think after `in`).

Note that the variable takes the value of nearest binding construct.

```ocaml
sqrt (let x = 3 in x *. x +. (let x = 4. in x *. x));;
```

The first two `x`'s take the value of 3 where the second two `x`'s take the vale of 4. We say that the outer variable is **shadowed** by the inner variable (meaning that the inner variable takes precedence).

If you omit the `in`, you've just created a global variable that exists to the end of the REPL section or to the end of the program. You can only create a global variable in the top level, not within an `in`.

```ocaml
let x = 3 ;;
let x = 4 ;;
x + x ;;
```
This isn't variable assignment: the first `x` still exists but is just inaccessible because it has been overshadowed by the second `x`.

### Functions
Functions in OCaml can only take one argument. ie. `sqrt 2.0`

If you want a function to take several arguments, we do something called currying the function. The function takes in each input one at a time and returns a function that takes the next input.

You can define an anonmyous function with the following syntax:
- `(fun x : int -> 2 * x) 21`

You can define a named function wit the following syntax:
- `let double = fun x -> 2 * x`
- `let double x = 2 * x`

Here's what a multivariable function looks like:

```ocaml
let hypotenuse a b = sqrt (a ** 2. +. b ** 2.)
```

Expands to:

```ocaml
let hypotenuse =
	fun a -> 
		fun b ->
		sqrt (a ** 2. +. b ** 2.)
```

Really just think of it as substitution.

```ocaml
let hypotenuse (a:float) (b:float) : float = 
	sqrt (a ** 2. +. b ** 2.)
```

Type hinting the arguments is intuitive, type hinting the output is just before the equals sign.

If you want to use your function inside the body (ie. a recursive function), you need the `rec` keyword.

```ocaml
let rec fact (n:int) : int =
	if n == 0 then 1
	else n * fact (n - 1)
```