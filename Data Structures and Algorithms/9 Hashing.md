# Hashing

$O(1)$ insertion and searching in best case.
$O(n)$ insertion and searching in worst case.

- Chained-Hash-Insert(T, x): Insert $x$ at the head of the list $T[h(x.key)]$
- Chained-Hash-Search(T, x): Search for $x$ in the list $T[h(x.key)]$
- Chained-Hash-Delete(T, x): Delete $x$ from the list $T[h(x.key)]$
- Load Factor: $\alpha = \frac{n}{m} = \frac{elements}{slots}$
- $\Theta(1 + \alpha)$ average search and delete time.

## Functions

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

## Time Complexity

- $O(m)$ worst case time to insert, delete, and search.
- Load factor $\alpha = \frac{n}{m} < 1$
- Unsuccessful search probability: $\frac{1}{1 - \alpha}$. Successful: $\frac{1}{\alpha} \ln (\frac{1}{1 - \alpha})$

## Hashing Functions

- Division Method: $h(k) = k \mod m$
- Multiplication Method: $h(k) = \lfloor m(kA \mod 1) \rfloor$ where $A \in (0, 1)$. Ex: $A = \frac{\sqrt{5} - 1}{2}$
