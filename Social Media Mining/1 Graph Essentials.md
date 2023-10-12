# Graph Essentials

## Basics

- **Nodes**: entities in the network.
  - Also called actors, points or vertices.
  - $V = \{v_1, v_2, ..., v_n\}$
- **Edges**: relationships between nodes.

  - Also called ties, links or lines.
  - Can be directed or undirected.
  - $E = \{e_1, e_2, ..., e_m\}$

- **Network**: a set of nodes and edges.

  - Also called a graph.
  - $G = (V, E)$

- **Cardinality**: number of nodes in a network.
  - $|V| = n$
- **Density**: number of edges in a network.

  - $|E| = m$

- **Neighborhood**: set of nodes adjacent to a node.

  - **Degree**: number of nodes in the neighborhood, i.e. number of edges connected to a node.
    - **In-degree**: number of incoming edges.
    - **Out-degree**: number of outgoing edges.
  - $N(v_i) = \{v_j \in V | (v_i, v_j) \in E\}$

- **Degree Distribution**: the probability distribution of the degrees over the entire network.

  - $P(k) = \frac{N_k}{N}$
  - **Degree Sequence**: $\pi(d) = \{d_1, d_2, ..., d_n\}$
  - **Degree Distribution Histogram**: x-axis is degree, y-axis is number of nodes with that degree.

- **Theorem 1**: the sum of the degrees of all nodes in a network is equal to twice the number of edges.

  - $\sum_{v_i \in V} deg(v_i) = 2|E|$

- **Lemma 1**: The number of nodes with odd degrees is even
- **Lemma 2**: In any directed graph, the sum of the in-degrees is equal to the sum of the out-degrees.
  - $\sum_i{d_i^{out}} = \sum_j{d_j^{in}}$

## Graph Representation

- Goal is to efficiently store and retrieve information

  - Do not lose information
  - Can be processed easily by computers
  - Can have mathematical methods to be applied easily

- **Null Graph**: Node set is empty. Edge set is empty.
- **Empty Graph**: Edge set is empty. Node set can be non-empty.
  - **Null Graph** is a special case of **Empty Graph**.

### Adjacency Matrix

- An `n x n` matrix used to represent a graph with `n` vertices.
  - A[i][j] = 1 (or edge weight) if there's an edge between vertex `i` and `j`.
  - A[i][j] = 0 otherwise.
- For undirected graphs: The matrix is symmetric (A[i][j] = A[j][i]).
- For directed graphs: The matrix need not be symmetric.
- For weighted graphs: The matrix contains the weights of the edges.

- **Single Graph**: Graph with one edge between any two nodes.
- **Multi Graph**: Graph with one or more edges between any two nodes.

#### Undirected Graph Example of Adjacency Matrix

|     | A   | B   | C   | D   |
| --- | --- | --- | --- | --- |
| A   | 0   | 1   | 0   | 1   |
| B   | 1   | 0   | 1   | 0   |
| C   | 0   | 1   | 0   | 1   |
| D   | 1   | 0   | 1   | 0   |

The above matrix represents the following graph:

```text
A -- B -- C -- D
|______________|
```

#### Directed Graph Example of Adjacency Matrix

|     | A   | B   | C   | D   |
| --- | --- | --- | --- | --- |
| A   | 0   | 1   | 0   | 1   |
| B   | 0   | 0   | 1   | 0   |
| C   | 0   | 0   | 0   | 1   |
| D   | 0   | 0   | 0   | 0   |

The above matrix represents the following graph:

```text
A --> B --> C --> D
|_________________^
```

- **Sparse Matrix**: most of the elements are zero.
  - Ex: social networks, web graphs, road networks.
- **Dense Matrix**: most of the elements are non-zero.
  - Ex: complete graphs, mesh networks, airline networks.

### Adjacency List

- A collection of unordered lists used to represent a graph.
  - Each list describes the set of neighbors of a vertex in the graph.

#### Undirected Graph Example of Adjacency List

| Vertex | Neighbors |
| ------ | --------- |
| A      | B, D      |
| B      | A, C      |
| C      | B, D      |
| D      | A, C      |

The above adjacency list represents the following graph:

```text
A -- B -- C -- D
|______________|
```

#### Directed Graph Example of Adjacency List

| Vertex | Neighbors |
| ------ | --------- |
| A      | B, D      |
| B      | C         |
| C      | D         |
| D      |           |

## Graph Connectivity

- **Adjacent nodes** are connected by an edge.
- **Incident edges** are connected to a node.

- **Walk** is a sequence of incident edges
  - **Open walk** does not end where it starts.
  - **Close walk** ends where it starts.
- **Walk Length** is the number of visited edges.
- **Path** is a walk with no repeated nodes and edges.
- **Cycle** is a closed path with no repeated nodes and edges.
- **Trail** is a walk with no repeated edges(covers all nodes).
  - **Closed trail** ends where it starts. Called a tour or circuit.
  - **Eulerian trail** is a trail that visits every edge exactly once.
  - **Hamiltonian cycle** is a closed trail that visits every node exactly once.


### Random Walk

Walk with the next step chosen randomly from the neighbors.

Edge weights can be used to bias the random walk.

  $\sum_x{W_{i,x}} = 1, \forall{i, j} w_{i,j} \geq 0$ 

### Connectivity

- **Node connectivity**: path exists between a pair of nodes.
- **Graph connectivity**: path exists between any pair of nodes.
  - **Connected Component**: a subgraph where all nodes have a path to each other.
  - **Strongly Connected**: path exists between any pair of nodes in a directed graph.
  - **Weakly Connected**: path exists between any pair of nodes without considering edge directions.
- **n-hop neighborhood**: set of nodes reachable within n steps.
- **Diameter**: longest shortest path between any pair of nodes.

### Special Graphs

- **Trees**: connected graph with no cycles.
	- |V| = |E| + 1
- **Forests**: disjoint set of trees (disconnected trees)


- **Spanning Tree**: subgraph that is a tree and contains all nodes of the original graph.
	- There can be multiple spanning trees for a graph.
	- Weight is the summation of all the edge weights
- **Minimum Spanning Tree (MST)** is a spanning tree with the minimum weight.
	- There can be multiple MSTs for a graph.
- **Prim's Algorithm**: Greedy algorithm to find MST.
	- Start with a node and add the edge with the minimum weight.
	- Add the next edge with the minimum weight that does not create a cycle.
	- Repeat until all nodes are connected.
- **Kruskal's Algorithm**: Greedy algorithm to find MST.
	- Start with the edge with the minimum weight.
	- Add the next edge with the minimum weight that does not create a cycle.
	- Repeat until all nodes are connected.


- **Steiner Tree**: weighted tree spanning all nodes with the minimum weight.
- **Complete Graph** is a graph where every pair of nodes is connected by an edge.
	- $|E| = \frac{|V|}{2}$
- **Bipartite Graph** is a graph where the nodes can be divided into two disjoint sets such that every edge connects a node in one set to a node in the other set.
	- $V = V_L \cup V_R$
	- $V_L \cap V_R = \emptyset$
	- $E \subseteq V_L \times V_R$ (the full edge set is the cartesian product)
- **Affiliate Network** is a bipartite graph where one set is the users and the other set is the products.
- **Social-Affiliation Network** is a combination of a social network and an affiliate network.

- **Regular Graph** is a graph where all nodes have the same degree (connected or disconnected).
	- *K-regular graph* is a graph where all nodes have degree k.
	- Complete graphs are examples of regular graphs
- **Egocentric Networks** contain a focal node (ego) and a set of alters that have ties.
	- There are conditions on the ties between alters.
	- Ex: Mother-children relations can only be from one mother to her children only.
- **Bridges** are edges whose removal will increase the number connected compoonents.
	- **Cut Vertices** are nodes whose removal will increase the number connected components.

## Graph Algorithms

- **Depth-First Search (DFS)**: Traverses the graph by going as deep as possible using a stack.
	- **Pre-order**: visit the node before visiting the children.
	- **Post-order**: visit the node after visiting the children.
- **Breadth-First Search (BFS)**: Traverses the graph by visiting all neighbors before going deeper using a queue.
	- **Level-order**: visit the nodes in the same level before going to the next level.


- **Dijkstra's Algorithm**: Finds the shortest path from a source node to all other nodes.
	- Designed for weighted graphs with non-negative weights.
	- Finds the shortest path from a source node to all other nodes.
	- Uses a priority queue to select the next node to visit.

- **Prim's Algorithm**: Finds the minimum spanning tree of a graph.
	- Select a random node and add the edge with the minimum weight.
	- Add the next edge with the minimum weight that does not create a cycle.

- **Bridge Detection Algorithm**: Finds the bridges in a graph using BFS to remove an edge and see if the # connected components increases.
