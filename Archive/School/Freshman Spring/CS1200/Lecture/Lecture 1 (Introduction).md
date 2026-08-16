Our input:
`(k0,v0) (k1,v1) (k2,v2) ... (kn-1,vn-1)`

### Valid Sort
- Keys are in ascending order
	- `k0 <= k1 <= k2 <= ... <= kn-1` 
- The valid sort is a permutation of input

### Exhaustive search sort (ESS)
- For all permutations $\pi[n] \rightarrow [n]$ 
	- If keys are in ascending order, return it.
	- Otherwise, return $\perp$ (bot which means that the operation always returns false)
- Very slow sort.
- Proof:
	- THM: ESS outputs a valid sort of A (if it exists). 
	- ESS definitely returns before $\pi*$ is reached

### Insertion sort (IS)
- For all `i = 0, 1, ..., n-1`
	- Words:
		- Find the smallest J less than I for which the key at the j-th location is less than or equal to the key at the i-th position.
		- Then insert the i-th entry at position J, shift everything after J up one.
	- Math:
		- Find a the smallest `j <= i` such that `A[j][0] >= A[i][0]`
		- Insert `A[i]` at `j`th place and move `A[j]` and all entries after it up one slot
	- Example `(6,a), (2,b), (1,c), (4,d)`
		- `i = 0   (6,a), (2,b), (1,c), (4,d)`
		- `i = 1   (2,b), (6,a), (1,c), (4,d)`
		- `i = 2   (1,c), (2,b), (6,a), (4,d)`
		- `i = 3   (1,c), (2,b), (4,d), (6,a)`
Proof:
Let  $A^{(i)}$ be the array right before the $i$th step
Let $k^{(i)}[j]$ $j$ be the key of $A^{(i)}$ 

Induction shows a "loop invariant"

$P[1]$ "$A^{(i)}[0,i]$ is sorted and $A^{(0)}[n,n-1]$ is unchanged

Read textbook on sorting 1.1-1.5. Make comments.