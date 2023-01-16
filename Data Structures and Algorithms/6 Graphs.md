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

## Depth First Search

**Applications**: Topological sort, strongly connected components, and finding bridges and articulation points.

- **Depth First Search** is a **pre-order traversal** of a graph.
  - Pre-order traversal: Visit the root node, then recursively traverse the left subtree, then recursively traverse the right subtree.
- Vertex consists of:
  1. u.d: Discovery time
  2. u.f: Finish time
  3. u.color: {WHITE, GRAY, BLACK}
  4. u.pi: Parent of the vertex
- The algorithm is implemented using a **stack** with LIFO property.
- The predecessor sub-graph of G as $G_{\pi} = (V_{\pi}, E_{\pi})$, where:
  - $V_{\pi} = \{v \in V | v.pi \ne nil\}$. This is the set of vertices with a parent.
  - $E_{\pi} = \{<v.\pi, v>: v \in V|{\pi} - \{s\}\}$. This is the set of edges from the parent to the child.

### DFS Pseudocode

```c
DFS(G)
  for each vertex u in G.V
      u.color = WHITE
      u.pi = NIL

  time = 0

  for each vertex u in G.V
      if u.color == WHITE
          DFS_VISIT(G, u)
```

```c
DFS_VISIT(G, u)
  time = time + 1
  u.d = time
  u.color = GRAY

  for each vertex v in G.Adj[u]
      if v.color == WHITE
          v.pi = u
          DFS_VISIT(G, v)

  u.color = BLACK
  time = time + 1
  u.f = time
```

### DFS Time Complexity

- The time complexity of DFS is $\Theta(n + m)$.
  - n is the number of vertices
  - m is the number of edges
- Each vertex is pushed and popped at most once.
- Each vertex is traversed at most once.

### DFS Theorems

#### Nesting of Descendant's Intervals

Vertex $v$ is a descendant of vertex $u$ in the DFS forest iff $u.d \le v.d \le v.f \le u.f$.

#### White-path Theorem

In a DFS forest fo a graph $G=(V, E)$, vertex $v$ is a descendant of vertex $u$ iff there is a white path from $u$ to $v$.

#### Parenthesis Theorem

In a DFS forest of a graph $G=(V, E)$, for any two vertices $u$ and $v$, the following conditions hold:

- Intervals ([u.d, u.f], [v.d, v.f]) are disjoint: neither $u$ nor $v$ is a descendant of the other.

- Interval [u.d, u.f] is contained entirely within the interval [v.d, v.f], and u is a descendant of v
  OR
- Interval [v.d, v.f] is contained entirely within the interval [u.d, u.f], and v is a descendant of u.

## Classification of Edges

In the case of an undirected DFS forest, every edge is either a tree edge or a back edge.

- **Tree Edge**: An edge $(u, v)$ is in a tree edge if v is first discovered by exploring edge $(u, v)$.
- **Back Edge**: An edge $(u, v)$ connecting a vertex $u$ to an ancestor $v$ in the DFS tree. This is a cycle or self-loop edge.
- **Forward Edge**: An edge $(u, v)$ connecting a vertex $u$ to a descendant $v$ in the DFS tree.
- **Cross Edge**: All other edges.

### Cycle

- A **cycle** is a path of length at least 2 that starts and ends at the same vertex.
  - A **self-loop** is considered a cycle.
  - Can be detected in $\Theta (n + m)$ time using DFS.

### Directed Acyclic Graph (DAG)

- A **directed acyclic graph** (DAG) is a directed graph with no cycles.
  - Can be detected in $\Theta (n + m)$ time using DFS.

### Topological Sort

- A **topological sort** of a DAG is a linear ordering of its vertices such that if G contains an edge $(u, v)$, then $u$ appears before $v$ in the ordering.
  - A topological sort is not unique.
  - Time complexity: $\Theta(n + m)$

#### Topological Sort Pseudocode

```c
TOPOLOGICAL_SORT(G)
  DFS(G)
  return vertices of G in order of decreasing u.f
```

### Strongly Connected Components

1. DFS to compute $u.f$ for each vertex $u$.
2. Construct $G^t$ by reversing all the edges of $G$ in opposite direction.
3. Run DFS on $G^t$ but in the main loop of DFS, consider the vertices in order of decreasing $u.f$.

The order of $DFS(G^t)$ is important. but the order of $DFS(G)$ is not important.
The running time is $O(V + E)$.
