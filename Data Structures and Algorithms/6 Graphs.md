# Graphs

- **Vertex**: A node in a graph.
- **Edge**: A connection between two vertices.
- **Directed Graph**: A graph where each edge is directed from one vertex to another.
- **Undirected Graph**: A graph where each edge is bidirectional.
- **Weighted Graph**: A graph where each edge has a weight associated with it.

## Breadth First Search

**Applications**: Prim's minimum-spanning-tree algorithm and Dijkstra's shortest-path algorithm.

### BFS Color Codes

- **White**: Undiscovered Vertex
- **Gray**: Discovered but Unexplored Vertex
- **Black**: Discovered and Explored

All vertices are initially white, gray when enqueued and black after dequeued and explored.

### BFS Notes

- **Breadth First Search** is a **level-order traversal** of a graph.
- Adjacency list representation is used for graphs.
- Vertex consists of:
  1. u.d: Distance to the source vector
  2. u.color: {WHITE, GRAY, BLACK}
  3. u.pi: Parent of the vertex
- The algorithm is implemented using a **queue** with FIFO property.
- BFS is a **non-recursive** algorithm.
- BFS can be applied to **directed** and **undirected** graphs.
  - Directed: Edges are directed from one vertex to another.
  - Undirected: Edges are bidirectional.

### BFS Pseudocode

```c
BFS(G, s)
  // G is a graph, s is the source vertex
  for each vertex u in G.V - {s}
      u.color = WHITE
      u.d = INFINITY
      u.pi = NIL

  // Initialize source vertex
  s.color = GRAY
  s.d = 0
  s.pi = NIL

  // Initialize queue
  Q = Queue([])

  // Enqueue source vertex
  Q.enqueue(s)
  while (Q != empty)
    u = Q.dequeue()

    for each vertex v in G.Adj[u]
        if v.color == WHITE
            v.color = GRAY
            v.d = u.d + 1
            v.pi = u
            Q.enqueue(v)

    u.color = BLACK
```

### BFS Time Complexity

- The time complexity of BFS is $O(n + m)$.
  - n is the number of vertices
  - m is the number of edges
- Each vertex is enqueued and dequeued at most once.
- Each vertex is examined at most once.

### BFS Shortest Path

- The shortest path from $s$ to $v$ is the path of minimum number of edges.
- $\delta (s, v)$ is the length of the shortest path from $s$ to $v$.
  - If there is no path: $\delta (s, v) = \infty$.

- Lemma 1: For any edge $(u, v)$, $\delta (s, v) \le \delta (s, u) + 1$.
- Lemma 2: For G=(V, E) and s in V, $v.d \ge \delta (s, v)$ for all v in V.
- Lemma 3: For vertices $<v_1, v_2, \dots, v_n>$ in Queue and $i = 1, 2, \dots, r-1$:
  - $v_r \le v_{1}.d + 1$
  - $v_1.d \le v_2.d \le ... \le v_n.d$.
- Lemma 5: After BFS is complete, we have $\delta (s, v) = v.d$ for all v in V.
