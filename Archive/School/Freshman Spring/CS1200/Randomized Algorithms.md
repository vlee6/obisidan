When we see **expected runtime**, think of randomized algorithms

Randomized Algorithms use randomness in their computation. For example:
### `QuickSelect`

$$\text{Input: } A = ((K_0,V_0),...,(K_{n-1},V_{n-1})), i \in [n]$$
$$\text{Output: } (K_j,V_{j)} \text{ where } K_{j}\text{ is the (i+1)-th smallest key}.$$
$$\text{At most } i \text{ keys less than } K_{j} \text{ and at most } n-i-1 \text{ keys greater than } K_j $$

```
QuickSelect(A,i):
if n == 1 return (K0, V0)
p = random(n)
pivot = kp
A_small = array of (key,value) pairs with key < pivot
A_large = array of (key,value) pairs with key > pivot
A_equal = array of (key,value) pairs with key == pivot
n_small = size of A_small
n_large = size of A_large
n_equal = size of A_equal
if i >= n_small + n_equal, return QuickSelect(A_large, i - n_small - n_equal)
if i < n_small, return QuickSelect(A_small, i)
return anything in A_equal
```

*(Proof of correctness)* Strong induction on that fact that `QuickSelect` solves selection on a array with size $<$ k.

*(Runtime)* On average, the size of the large or small array is $\frac{3n}{4}$.
$$T(n) \leq T\left(\frac{3n}{4}\right)+cn$$
$$T(n) \leq cn + c \left(\frac{3n}{4}\right)+c \left(\frac{3n}{4}\right)^{2}+ ...$$
$$T(n)=4cn \text{ by infinite series }= O(n)$$

Only random pivot selection can guarantee the $\frac{3n}{4}$. If we didn't have random pivot selection, there could be adversarial datasets that have a worse case runtime of $O(n^2)$ if only one key-value pair is removed at a time.

### Rank
The rank of an entry in an array is the position that entry has if the array is sorted in order.

$A = {5,6,4,2}$
2 has rank 1
4 has rank 2
5 has rank 3
6 has rank 4

"Find the element of rank $I$" means "find the $i$-th smallest element."

To score on the $x$th percentile means that $x$ percent of people scored the same or lower than you.

### Las Vegas Algorithm
Algorithms that always solve the problem but may run for a very long time. We measure expected runtime.

### Monte Carlo Algorithm
Algorithms that solve the problem with high likelihood (but not always—can return incorrect answers), but with fixed runtime. We measure worst case runtime over randomness.

If you just stop an Las Vegas Algorithm once you get tired, it becomes a Monte Carlo Algorithm