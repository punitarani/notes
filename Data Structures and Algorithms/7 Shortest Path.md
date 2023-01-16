# Shortest Path

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
  - The total running time is $O(|V| \log |V| + |E|)
