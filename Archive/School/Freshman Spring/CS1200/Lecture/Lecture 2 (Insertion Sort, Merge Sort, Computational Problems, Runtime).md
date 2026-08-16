### Loop invariant
Any property that proves the final statement and keep track of how the loop modifies the data
### Insertion Sort
`for i = 0, 1, ... n-1`
- Find the smallest `J` such that `A[j][0] >= A[i][0]`
- Insert `A[i]` at j-th index
- Shift `A[J, ... i-1]` to `A[J+1, ... i]`

*Proof*
Insertion sort solves the sorting problem; for any input array A, `IS(A)` outputs a valid sort [^1] of A.

Notation
$A^{(0)}$ is the array right before the i-th iteration
$A^{(0)}$ is the input array, $A^{(n)}$ is the output

Loop invariant: $P(i)$ `A[0, ..., i-1]` is a valid sort of $A^{(0)}$`[0, ..., i-1]` and `A[i, ..., n-1] = ` $A^{(0)}$`[i, ..., n]`

1) Base case: `P(0) is true`

Since the $A^{(0)}$`[0, -1]` is an empty array, it's already sorted. $A^{(0)}$`[0, n]` is the same array, it's untouched as our loop invariant claims.

2) Inductive step: For all `i < n-1`, `P(i)` implies `P(i+1)`

P(1) says that $A^{(0)}$`[0, i-1]`

### Merge sort
Input is an array `A` of key-value pairs `((k0,v0), ..., (kn-1,vn-1))`

If `n <= 1` return A
else
- If `i = n/2`
	- B = `mergeSort((k0,V0), (ki-1,vi-1))`
	- B' = `mergeSort((ki,vi), (kn-1,vn-1)`
	- return `merge(B,B')`

Theorem MergeSort solved Sorting Problem.
- Proof by strong induction
	- P(k): "mergeSort correctly sorts all arrays of size k"
	- Base case P(0), P(1) by `n <= 1` statement
	- Strong induction: Show P(n) by assuming P(k) for **all** `k<n`

### Computational problem
A computational problem is a tuple ($I,O,f$)
- $I$ is a set of (usually infinite) possible inputs, $O$ is a set of possible outputs
- $f$ for all $x$ that is in $I$, $f(x) \subset O$. `f(x)` is the set of valid outputs for $x$.

For the sorting problem:
- $I$ is the set of all arrays of (key,value) pairs with the key being real
- $O$ is the set of all (sorted) arrays of (key,value) pairs with the key being real
- $f: x \in I$, set of valid sorts of $x$

### Algorithm
Informal definition: An algorithm is a well defined finite procedure for transforming input $x$ to outputs $A(x)$

- Algorithm A solves a computational problem ($I$, $O$, $f$) if...
	- for all $x \in I$ such that $f(x) \neq \emptyset$ , $A(x) \in F(x)$
	- for all $x \in I$ such that $f(x) = \emptyset$ , $A(x) = \bot$

### Measuring efficiency
- Which algorithm is faster
- Comparing computation problems
- Reductions

Size of $I -> n$
$T(n) max@$

![[Pasted image 20260202103708.png]]

[^1]: [[Lecture 1 (Introduction)#Valid Sort]]
