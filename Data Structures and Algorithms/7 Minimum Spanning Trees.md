# Minimum Spanning Trees

## Shortest Paths

- The weight of a path is: $w(p) = \sum_{i=1}^{k} w(v_{i-1, i})$
- The shorted-path weight from vertex $u$ to vertex $v$ is
  - $w(u, v) = \min_{p \in P(u, v)} w(p)$
  - $\infty$ if no path exists

For each node $v$:

- $v_d$ is the distance from source $s$
- $v_p$ or $v_{\pi}$ is the predecessor of $v$ on a shortest path from $s$ to $v$
- Initially, $v_d = \infty$ and $v_p = \text{nil}$

**Relax** the distance at vertex $v$ if a shorter path has been found

```c
Relax(u, v, w)
  if (v.d > u.d + w(u, v))
    v.d = u.d + w(u, v)
    v.p = u
```

```text
Initialize-Single-Source(G, s)
    for each vertex v ∈ V[G]
        v.d = ∞
        v.π = NIL
    s.d = 0
```

```text
Relax(u, v, w)
    if v.d > u.d + w(u, v)
        v.d = u.d + w(u, v)
        v.π = u
        return true
    return false
```

```text
Dijkstra(G, w, s)
    Initialize-Single-Source(G, s)
    S = ∅
    Q = ∅
    for each vertex v ∈ V[G]
        Insert(Q, v)
    while Q ≠ ∅
        u = Extract-Min(Q)
        S = S ∪ {u}
        for each vertex v ∈ Adj[u]
            If Relax(u, v, w)
                Decrease-Key(Q, v, v.d)
```

The running time with binary heap for Q is $O((V + E) \log V)$.
The running time with Fibonacci heap for Q is $O(V \log V + E)$.

## Kruskal's Algorithm

Subset of G that includes all the vertices and has the minimum possible total weight.

```text
MST-Kruskal(G, w)
    A = ∅                               // A is the set of edges in the MST
    for each vertex v ∈ V[G]
        Make-Set(v)
    E = Sort(G.E) by increasing w
    for each edge (u, v) ∈ E
        if Find-Set(u) ≠ Find-Set(v)    // * u and v are in different trees
            A = A ∪ {(u, v)}            // add (u, v) to A
            Union(u, v)                 // merge u and v into one tree
```

## Prim's Algorithm

```text
MST-Prim(G, w, r)
    for each u ∈ V[G]
        u.key = ∞
        u.π = NIL
    r.key = 0
    Q = V[G]
    while Q ≠ ∅
        u = Extract-Min(Q)
        for each v ∈ Adj[u]
            if v ∈ Q and w(u, v) < v.key
                v.π = u
                v.key = w(u, v)
```

Time complexity of both are $O(E \log V)$.

## Dijkstra's Algorithm

The algorithm is a greedy algorithm that finds the shortest path from a source vertex to all other vertices in a weighted graph.

- It uses a priority queue with Breadth-First Search
- Key of vertex $v$ is the currently computed distance from $s$ to $v$
- Processed vertices are removed from Q and stored in a set $S$

### Dijkstra's Algorithm Pseudocode

```c
Dijkstra(G, s)
  initialize single-source(G, s)
  S = {}
  Q = {}

  for each vertex u in G.V
    Q.insert(u)

  while Q is not empty
    u = Q.extract_min()
    S.add(u)

    for each vertex v in G.Adj[u]
      Relax(u, v, w)
      if v in Q
        Q.decrease_key(v)
```

### Complexity

- The running time depends on the implementation of the priority queue
- $V$ is the number of vertices and $E$ is the number of edges.
- If we use a binary heap for Q:
  - Insertion takes $O(\log n)$ time
  - Extract-min takes $O(\log n)$ time
  - $v.d = u.d + w(u, v)$ in Relax decrease-key takes $O(\log n)$ time
  - Total running time is: $O((|E| + |V|) \log|V|)$
    - $O(|E| \log|V|)$ if the graph is connected
- If we use a fibonacci heap for Q:
  - The total running time is $O(|V| \log |V| + |E|)$
