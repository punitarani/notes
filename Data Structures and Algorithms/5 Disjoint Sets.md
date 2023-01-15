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
