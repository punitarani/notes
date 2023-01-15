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
