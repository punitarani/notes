# Decision Trees

Binary tree representing comparisons between elements of an algorithm.
We annotate each node by the comparison made at the corresponding step of the algorithm.
We annotate each leaf node by a permutation: $< \pi(1), \pi(2), \dots, \pi(n) >$.

- Insertion Sort: $A[j] > A[i]$. The key and the elements to the left are compared.
- Merge Sort: $A[i] \leq A[j]$. The elements of the two halves are compared.
- Quick Sort: $A[j] \leq A[r]$. The elements of the two halves are compared.

- There are $\Theta(n!)$ internal nodes and $O(n^2)$ possible comparisons.
- A binary tree of height $h$ has $2^h - 1$ nodes.
- A binary tree with $n$ nodes has height $\log(n)$.
- $log(n!) \in \Omega(n \log(n))$ is the lower bound of the height.
