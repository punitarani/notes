# Heaps

An **array object** with a **tree view**, and **heap property**

- Tree view
  - The `n` elements are stored in `A[1], A[2], ..., A[n]`
  - Can be viewed as a nearly complete binary tree
- Heap Property
  - `A[parent(i)] >= A[i]`  some $∀ 2 \le i \le n$
  - `A[i] >= A[left(i)]`  if $left(i) \le n$
  - `A[i] >= A[right(i)]`  if $right(i) \le n$
  - Property is violated at node $i$ if:
  1. $left(i) \le n$, but $A[i] < A[left(i)]$
  2. $right(i) \le n$, but $A[i] < A[right(i)]$
- General notes
  - Array must be continuous with no space in between
  - Array doest not have to be sorted in descending order
