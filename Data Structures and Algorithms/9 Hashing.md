# Hashing

$O(1)$ insertion and searching in best case.
$O(n)$ insertion and searching in worst case.

- Chained-Hash-Insert(T, x): Insert $x$ at the head of the list $T[h(x.key)]$
- Chained-Hash-Search(T, x): Search for $x$ in the list $T[h(x.key)]$
- Chained-Hash-Delete(T, x): Delete $x$ from the list $T[h(x.key)]$
- Load Factor: $\alpha = \frac{n}{m} = \frac{elements}{slots}$
- $\Theta(1 + \alpha)$ average search and delete time.

```text
Hash-Insert(T, k)
    i = 0
    while true
        q = h(k, i)
        if T[q] == NIL or T[q] == DELETED
            T[q] = k
            return q
        i = i + 1
```

```text
Hash-Search
    i = 0
    while true
        q = h(k, i)
        if T[q] == k
            return q
        else if T[q] == NIL and T[q] != DELETED
            return NIL
        i = i + 1
```
