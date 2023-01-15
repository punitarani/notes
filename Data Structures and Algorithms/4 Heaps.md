# Heaps

An **array object** with a **tree view**, and **heap property**

- Tree view
  - The `n` elements are stored in `A[1], A[2], ..., A[n]`
  - Can be viewed as a nearly complete binary tree
- Heap Property
  - `A[parent(i)] >= A[i]` some $∀ 2 \le i \le n$
  - `A[i] >= A[left(i)]` if $left(i) \le n$
  - `A[i] >= A[right(i)]` if $right(i) \le n$
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

```text
Build-Max-Heap(A)
    heap-size[A] = length[A]
    for i = length[A]/2 downto 1
        Max-Heapify(A, i)
```

### Sort

`Max-Heapify` is used to **build** a **max-heap** from an **unsorted** array.
This could but likely won't be sorted in descending order.
`HeapSort` is used to **sort** the **max-heap** in **descending** order.

```text
HeapSort(A)
    Build-Max-Heap(A)
    for i = length[A] downto 2
        swap A[1] with A[i]
        heap-size[A] = heap-size[A] - 1
        Max-Heapify(A, 1)
```

### Extract

`Extract-Max` is used to **remove** the **largest** element from the **max-heap**.
It **returns** the **largest** element and **reduces** the **heap-size** by **one**.
It **assumes** that the **max-heap** property holds **before** the call.
It **maintains** the **max-heap** property **after** the call.

```text
Extract-Max(A)
    if heap-size[A] < 1
        error "heap underflow"
    max = A[1]
    A[1] = A[heap-size[A]]
    heap-size[A] = heap-size[A] - 1
    Max-Heapify(A, 1)
    return max
```

### Increase Key

`Increase-Key` is used to **increase** the **value** of an **element** in the **max-heap**.
It **assumes** that the **max-heap** property holds **before** the call.
It **maintains** the **max-heap** property **after** the call.

```text
Heap-Increase-Key(A, i, key)
    if key < A[i]
        error "new key is smaller than current key"
    A[i] = key
    while i > 1 and A[Parent(i)] < A[i]
        swap A[i] with A[Parent(i)]
        i = Parent(i)
```

Similarly, `Decrease-Key` is used to **decrease** the **value** of an **element** in the **min-heap**.

### Insert

`Max-Heap-Insert` is used to **insert** a **new** element into the **max-heap**.
It **assumes** that the **max-heap** property holds **before** the call.
It **maintains** the **max-heap** property **after** the call.

```text
Max-Heap-Insert(A, key)
    heap-size[A] ++
    i = heap-size[A]
    A[i] = -∞
    Heap-Increase-Key(A, i, key)
```

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
