
| Sorting algorithm     | Runtime       | Notes                                                          |
| --------------------- | ------------- | -------------------------------------------------------------- |
| Insertion sort        | $O(n^2)$      |                                                                |
| Selection sort        | $O(n^2)$      |                                                                |
| Merge sort            | $O(n \log n)$ | All comparison based algorithms have a runtime of $O(n\log n)$ |
| Singleton bucket sort | $O(n+U)$      | Requires keys to be from finite universe size $U$              |
| Radix sort            |               | Depends on sorting algorithm it reduces to                     |

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

![[Insertion-sort-example-300px.gif]]

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
	- Strong induction: Show P(n) by assuming P(k) for **all** `k<n

### Selection sort
![[Selection-sort.gif]]

### Radix sort
Essentially iterate through each base $b$ digit of each keys and order your keys based on sorting the base $b$ digits. Requires the use of a stable sorting algorithm to sort the base $b$ digits.