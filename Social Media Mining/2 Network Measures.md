# Network Measures

- **Centrality** is a measure of the importance of a node in a network.
  - **Degree Centrality**: number of edges connected to a node.
    - **In-degree Centrality**: number of incoming edges.
    - **Out-degree Centrality**: number of outgoing edges.
  - **Closeness Centrality**: how close a node is to all other nodes in the network.
  - **Betweenness Centrality**: how often a node appears on the shortest path between two other nodes.
  - **Eigenvector Centrality**: how well connected a node is to other well connected nodes.
  - **PageRank**: how important a node is based on the importance of its neighbors.

- **Reciprocity**: the probability that a link from node A to node B exists if a link from node B to node A exists.
- **Transitivity**: the probability that a link from node A to node B exists if a link from node A to node C and a link from node C to node B exist.
- **Similarity**: the probability that a link from node A to node B exists if node A and node B have a common neighbor.

## Centrality

- Who you're connected to?
  - Degree Centrality
  - Eigenvector Centrality
  - Katz Centrality
- How you connect others
  - Betweenness Centrality
- How fast you can reach them
  - Closeness Centrality

### Degree Centrality

- Ranks nodes with more connections higher
  - $C_d(v_i) = d_i = \sum_{j=1}^{n}A_{j,i}$
  - **In-degree Centrality**: ranks nodes with more incoming connections higher. Ex: Twitter followers.
  - **Out-degree Centrality**: ranks nodes with more outgoing connections higher. Ex: Twitter following.
  - **Normalized** by maximum possible degree (n - 1), maximum degree ($max_j d_j$), degree sum ($2|E|$ or $2m$)

### Eigenvector Centrality

- Generalizes degree centrality by accounting for the importance of a node's neighbors.
  - $C_e(v_i) = \frac{1}{\lambda}\sum_{j=1}^{n}A_{j,i}C_e(v_j)$ where $\lambda C_e = A^T C_e$
  - $\lambda$ is the largest eigenvalue of the adjacency matrix, which is used to normalize the centrality.

**Problem**: Centrality is 0 for nodes in a directed acyclic graph.

### Katz Centrality

$C_{katz}(v_i) = \alpha \sum_{j=1}^{n}A_{j,i}C_{katz}(v_j) + \beta$

where $\alpha$ is the controlling term and $\beta$ is the bias term.

**$\alpha < \frac{1}{\lambda}$** where $\lambda$ is the largest eigenvalue of the adjacency matrix.

$C_{katz} = \beta(I - \alpha A^T)^{-1} \cdot 1$

**Problem**: When a node becomes an authority, it passes all its centrality through its outgoing edges.
Not everyone known by a well-known person is well-known.

### Page Rank

Similar to Katz Centrality, but divide the centrality by the out-degree of the node.

$C_p(v_i) = \alpha \sum_{j=1}^{n}A_{j,i}\frac{C_p(v_j)}{d_j^{out}} + \beta$

$C_p = \beta(I - \alpha A^T D^{-1})^{-1} \cdot 1$

where $D$ is the diagonal matrix of out-degrees.

**$\alpha < \frac{1}{\lambda}$** where $\lambda$ is the largest eigenvalue of $A^T D^{-1}$.
In undirected graphs, $\lambda = 1$ so $\alpha < 1$.


### Betweenness Centrality

Consider how important a node is in connecting other nodes.

$C_b(v_i) = \sum_{s \neq t \neq v_i} \frac{\sigma_{st}(v_i)}{\sigma_{st}}$

where $\sigma_{st}$ is the number of shortest paths from node $s$ to node $t$ and $\sigma_{st}(v_i)$ is the number of shortest paths from node $s$ to node $t$ that pass through node $v_i$.

- If all the shortest paths from $s$ to $t$ pass through $v_i$, then $\sigma_{st}(v_i) = \sigma_{st}$ and $C_b(v_i) = 1$.

$C_b^{norm} (v_i) = \frac{C_b(v_i)}{n-1}$

where $n$ is the number of nodes in the graph.

- Trivial solution: compute all shortest paths between all pairs of nodes using Dijkstra's algorithm in $O(n^3)$
- Better solution: Brandes algorithm in $O(mn)$ for unweighted graphs and $O(mn + n^2 \log n)$ for weighted graphs.

### Closeness Centrality

Influential nodes can reach other nodes quickly.
These nodes should have a smaller average short path.

$C_c(v_i) = \frac{1}{\bar{l}_{v_i}}$

$\bar{l}_{v_i} = \frac{1}{n-1} \sum_{v_j \neq v_i} l_{i, j}$

where $l_{v_i, v_j}$ is the length of the shortest path from node $v_i$ to node $v_j$.

## Friendship Patterns

### Transitivity

- $aRb \land bRc \implies aRc$
- A friend of a friend is a friend.
- Can lead to a denser, more complete graph.
- Can help determine how close graphs are by measuring transitivity.

- **Clustering Coefficient** measures transitivity in an unidrected graphs.
  - Count paths of length two and check whether the third exists
  - $C = \frac{|Closed Paths of Length 2|}{|Paths of Length 2|}$
  - $C = \frac{6 \times \text{Number of Triangles}}{|Paths of Length 2|} = \frac{3 \times |Number of Triangles|}{Number of Connected Triples of Nodes}$
- **Local Clustering Coefficient** measures transitivity at the node level
  - $C(v_i) = \frac{Number of Pairs of Neights of v_i that are connected}{Number of pairs of neighbors of v_i}$
    - In an undirected graph, denominator is $\frac{d_i(d_i - 1)}{2}$

### Reciprocity

- $aRb \implies bRa$
- If you follow someone, they follow you back.

### Balance and Status

- **Balance Theory**: if the multiplication of edges in a cycle is positive, then the cycle is balanced.
- **Status**: if a node has more incoming edges than outgoing edges, then it has higher status.
- **Status Theory** if X has higher status than Y, Y has higher status than Z, then X has higher status than Z.

## Similarity

- **Structural Equivalence** two nodes are structurally equivalent if they have the same neighbors.

- **Vertex Similarity** two nodes are similar if they have many common neighbors.
  - $\sigma_{v_i, v_j} = |N(v_i) \cap N(v_j)|$
- **Jaccard Similarity** $\sigma_{jaccard}{v_i, v_j} = \frac{|N(v_i) \cap N(v_j)|}{|N(v_i) \cup N(v_j)|}$
- **Cosine Similarity** $\sigma_{cosine}{v_i, v_j} = \frac{|N(v_i) \cap N(v_j)|}{\sqrt{|N(v_i)||N(v_j)|}}$

- The neighborhood $N(v)$ often excludes itself
- **Problem**: Connected nodes not sharing a neighbor will have 0 similarity.
- **Solution**: For 0 similarity, include the connected nodes in the neighborhoods.

- **Measuring Similarity Significance** comapre the calculated similarity value with its expected value where the vertices pick their neighbors at random.
  - Rewrite the neighborhood overlap as $\sigma(v_i, v_j) = |N(v_i) \cap N(v_j)| = \sum_{v_k \in V} A_{i,k} A_{j,k}$

- **Pearson correlation coefficient**: $\sigma_{pearson}(v_i, v_j) = \frac{\sum_{v_k \in V} (A_{i,k} - \bar{A_i})(A_{j,k} - \bar{A_j})}{\sqrt{\sum_{v_k \in V} (A_{i,k} - \bar{A_i})^2 \sum_{v_k \in V} (A_{j,k} - \bar{A_j})^2}}$

- **Regular Equivalence**: we don't look at neighborhoods shared between individuals, but rather how neighborhoods are similar themselves.
  - Ex: Athletes are similar not because they know each other, but since they know similar individuals like coaches, teammates, etc.
  - $\sigma_{regular}(v_i, v_j) = \alpha \sigma_{k, l} A_{i, k} A_{j, l} \sigma_{regular}(v_k, v_l)$
  - $\sigma_{regular}(v_i, v_j) = \alpha \sum_{k} A_{i, k} \sigma_{regular}(v_k, v_l)$
  - $\sigma_{regular} = \alpha A \sigma_{regular}$
  - $\sigma_{regular} = (I - \alpha A)^{-1}$ where $\alpha < \frac{1}{\lambda_{max}}$
