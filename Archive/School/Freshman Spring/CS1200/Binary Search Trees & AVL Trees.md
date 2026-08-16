### BST Definition
A nonempty BST has finitely many vertices. Each vertex $v$ contains the following:
- A key $K_v$
- A value $V_v$
- A left subtree, which is either an empty BST or a BST rooted at vertex $v_L$, the left child
- A right subtree, which is either an empty BST or a BST rooted at vertex $v_R$, the right child

*The BST property:* If $v$ has a left child $v_L$, then the keys of $v_L$ and its descendants are no larger than $K_v$. Similarly, if $v$ has a right child $v_R$, the keys of $v_R$ and its descendants are no smaller than $K_v$.

The height of a BST $h$ is the length of the longest path from the root vertex to any leaf vertex.

### Rotations
Given a rotation around root node $A$
![[Pasted image 20260308174420.png]]

### AVL Tree Definition
An AVL tree is a BST that is:
- *Height-balanced:* Every pair of siblings (ie. a vertex that shares the same parent) has heights differing by at most 1 (including the case where on sibling is the empty tree and has height -1)
	- Any easy way to visualize that a tree is *height-balanced* is that leaf vertices don't differ in horizontal level by more than one.
- *Hight-augmented:* Every vertex has an additional attribute of the *height* of the tree rooted at that distance.

he height of an AVL tree with $O(n)$ vertices is $O(\log n)$ .

### Runtime

| Query           | Sorted Array           | Binary Search Tree                     | AVL Tree                | (Randomized) Hash table |
| --------------- | ---------------------- | -------------------------------------- | ----------------------- | ----------------------- |
| `search`        | $O(\log n)$            | $O(h)$                                 | $O(\log(n))$            | $O(1+\frac{n}{m})$      |
| `predecessor`   | $O(\log n)$            | $O(h)$                                 | $O(\log(n))$            |                         |
| `successor`     | $O(\log n)$            | $O(h)$                                 | $O(\log(n))$            |                         |
| `min`           | $O(1)$                 | $O(h)$                                 | $O(\log(n))$            |                         |
| `max`           | $O(1)$                 | $O(h)$                                 | $O(\log(n))$            |                         |
| `rank`/`select` | $O(\log n)$            | $O(n)$, $O(h)$ using size augmentation | $O(n)$,$O(\log(n))$<br> |                         |
| `insert`        | $O(n)$                 | $O(h)$                                 | $O(\log(n))$            | $O(1)$                  |
| `delete`        | $O(n)$                 | $O(h)$                                 | $O(\log(n))$            | $O(1+\frac{n}{m})$      |
| Initialization  | Sorting algo dependent |                                        |                         | $O(m)$                  |
