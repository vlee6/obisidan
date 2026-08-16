The goal is to have a data structure that can support the following operations quickly:
- **Updates:** `insert((K,V))` or `delete(K)` a key-value pair $(K,V)$ with $K \in [U]$ into a multiset
- **Queries:** `search(K)` returns a matching key-value pair $(K,V)$ from the multiset if it exists.

Given array $A$ of $n$ key-value pairs $((K_0,V_{0}),...(K_{n-1},V_{n-1}))$

The general idea is to have an array of $m$ linked lists. Hash function(s) take a element from universe $U$, the key, into universe $m$, the index of linked list. $[U] \rightarrow [m]$ A key-value pair gets placed into a certain linked list via a hash function, either randomized or deterministic.

Preprocessing: initialize an array $B$ of length $m$ with each entry being (pointers to) the start of an empty linked list. Choose a hash function (either random or deterministic), call it $h_\ell^{[U] \rightarrow [m]}$ only **ONCE** during the preprocessing step.

We choose which linked list a key value pair $(K,V)$ goes to via $B(h_\ell(K))$

- In order to initialize a hash table, we initialize an array of empty linked lists of length $m$, and thus initialization has a runtime of $O(m)$.
- `insert((K,V))` will insert into the head of the linked list and thus has a runtime of $O(n)$
- `delete(K)` will traverse through the linked list (from head to tail) and delete the **first** key-value pair with key $K$ if it exists. 
- `search(K)`will traverse through the linked list and return the **first** key-value pair with key $K$ if it exists. If it does not, return $\bot$.

| Step           | Runtime (for randomized hash table) | Runtime (for deterministic hash table) |
| -------------- | ----------------------------------- | -------------------------------------- |
| Initialization | $O(m)$                              | $O(m)$                                 |
| `insert`       | $O(1)$                              | $O(1)$                                 |
| `delete`       | $O\left( 1+\frac{n}{m} \right)$     | $O(n)$ worse case                      |
| `search`       | $O\left( 1+\frac{n}{m} \right)$     | $O(n)$ worse case                      |

### Deterministic Hash Table
A deterministic hash table utilizes a deterministic function to determine which key-value pairs go into each linked list. An example of this is for $m=10$ is $h_{\ell}(K)= K \text{ mod } 10$.

Since determinism means there exists a possible adversarial dataset, the runtime given input of size $n$ is:
- `insert` is $O(1)$ since it inserts at head of linked list
- `delete` and `search` is $O(n)$ since the worse case is we must traverse through a linked list containing all key-value pairs to find whatever specific key we are looking for.

### Randomized Hash Table
A randomized hash table utilizes a randomized function to determine which key-value pairs go into each linked list. Remember, we only chose our randomized function **ONCE** during the preprocessing step.

An common implementation of a randomized hash function is:
$$h_{a,b}(K)=((aK+b) \text{ \% } p) \text{ \% }m$$
Where $a,b$ are randomly chosen numbers such that $a\in\{1,...,p-1\}$, $b \in \{0,...,p-1\}$ where $p$ is a prime number from $U \leq p < 2U$.

The load of a randomized hash $\alpha = \frac{n}{m}$. We can imagine load as the average length of each linked list. Thus, the runtime of `delete` and `search` is $O\left( 1+ \frac{n}{m} \right)$ since on average we must traverse a linked list that is $\frac{n}{m}$ long. Ideally, $m$ should be as close to $n$ as possible to reduce **collisions**, or when more than one distinct key is mapped to the same linked list.

Runtime summary for **randomized** hash table:
- `insert` is still $O(1)$ since it inserts at head of linked list
- `delete` and `search` is $O\left( 1 + \frac{n}{m} \right)$ since the on average we must traverse through a linked list with length $\frac{n}{m}$ to find the specific key we are looking for.


Suppose we wanted to search for $x$. A Monte-Carlo hash table (quick runtime, but might not be correct) only checks whether $x$ is at the head of the bucket. A Las-Vegas hash table (variable runtime, but guaranteed to be correct) would search through even element in the bucket, looking for $x$.