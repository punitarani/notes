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

## Functions

### Heapify

Max-Heapify is a **recursive** function that **assumes** that the **binary trees** rooted at `left(i)` and `right(i)` are **max-heaps**, but that `A[i]` might be smaller than its children, thus violating the **max-heap** property.
The function **corrects** this **violated** property by **traversing** the **tree** **bottom-up**.
It is used to **build** a **max-heap** from an **unsorted** array.

```text
Max-Heapify(A, i)
    l = left(i)
    r = right(i)
    largest = i
    if l ≤ heap-size[A] and A[l] > A[i]         // * A[l] is largest
        largest = l
    if r ≤ heap-size[A] and A[r] > A[largest]   // * A[r] is largest
        largest = r
    if largest ≠ i
        swap A[i] with A[largest]
        Max-Heapify(A, largest)
```

The recursive call is $T(\frac{2n}{3})$ and the constant time is $O(1)$.

## Time Complexities

|          | Best    | Average | Worst   |
| -------- | ------- | ------- | ------- |
| Heapify  | log(n)  | log(n)  | log(n)  |
| Build    | n       | nlog(n) | nlog(n) |
| Sort     | nlog(n) | nlog(n) | nlog(n) |
| Extract  | log(n)  | log(n)  | log(n)  |
| Increase | log(n)  | log(n)  | log(n)  |
| Insert   | log(n)  | log(n)  | log(n)  |
| Delete   | log(n)  | log(n)  | log(n)  |
| Search   | 1       | n       | n       |
