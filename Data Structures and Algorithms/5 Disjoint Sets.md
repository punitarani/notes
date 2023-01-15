# Disjoint Sets

A Disjoint Set maintains a collection (set) of disjoint dynamic (sub) sets.
$S={S_1, S_2, \dots , S_k}$

- Each element could be a pointer to an object
- **Representative**: One element of a set that is used to identify the entire set.
  - Similar to root of a tree or head of a linked list

## Find

`Find-Set` is used to **find** the **representative** of a **set**.
It **returns** the **representative** of the **set** that contains $x$.

```text
Find-Set(A, x)
  if A[x] <= 0
      return x                  # x is the root
  else
      A[x] = find_set(A[x])     # Path compression
      return A[x]               # Recursively find the root
```

## Link

`Link` is used to **merge** two **sets** into a new set.

- Favor the **root** with the **larger rank**.
- Favor $y$ over $x$ if they have the same rank.

```text
Link(A, x, y)
    if (-A[x]) > (-A[y])        // * A[x] is larger
        A[y] = x
    elements                    // * A[y] is larger
        if (-A[x]) = (-A[y])    // * A[x] and A[y] are the same size
            A[y] --
        A[x] = y
```

## Union

- Worst case total running time of `Union()` is $\Theta(m\log n)$ and total running time is $O(m\log n)$.
- For $m$ disjoint set operations including $n$ `Make-Set()` operations, the complexity is $O(m \log n)$.
- The amortized time complexity of each disjoint set operation is $O (\log n)$.
- Use **Union by Rank** and **Path Compression** gives a worst-case running time of $O (m \alpha (n))$.

```text
Union(A, x, y)
    Link(A, Find-Set(A, x), Find-Set(A, y))
```

## Time Complexity

- Worst case total running time of `union()` is $\Theta(m\log n)$ and total running time is $O(m\log n)$.

  - $m$ is the number of operations and $n$ is the number of elements.
  - Need to show that the height of the tree is at most $\Theta (\log n)$.
  - The height of the tree is the upper bound on the number of recursive calls in `find_set(x)`.

- For $m$ disjoint set operations including $n$ `make_set()` operations, the time complexity is $O(m \log n)$.
- The amortized time complexity of each disjoint set operation is $O (\log n)$.

_Union by rank is used whenever applicable_.
