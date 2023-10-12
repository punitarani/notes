# Network Models

- Goal is to generate graphs that function like real-world networks.
  - Analyze simulated graphs instead of real networks (cost-efficient)
  - Better understand real-world networks with math explanations
  - Perform controlled experiments on synthetic networks when real networks are unavailable

## Properities of Real-World Networks

### Power-Law Degree Distribution

- When the frequency of an event changes as a power of an attribute. Frequency follows a power-law

$ p_d = ad^{-b}$

where $p_d$ is the fraction of users with degree $d$, $a$ is the power-law intercept, $d$ is the degree, and $b$ is the power-law exponent (typical range $[2, 3]$)

$\ln(p_d) = \ln(a) - b \ln(d)$

- Usually the very first $d$ values do not exhibit power-law distribution

Examples:

- Call networks: $\frac{1}{k^2}$
- Book sales: $\frac{1}{k^3}$
- Scientific citations: $\frac{1}{k^3}$
- Social networks: $\frac{1}{k^2}$

Elementary tests for power-law distribution:

1. Pick a popularity measure and compute it for the whole network
2. Compute $p_k$ for each value of $k$
3. Plot a log-log graph of $\ln{p_k}$ vs $\ln{k}$
4. If the graph is linear, then the distribution is power-law

**Scale-Free Networks**: networks with power-law degree distribution

### Clustering Coefficient

- The fraction of a node's neighbors that are also neighbors of each other.
- Friendships are usually highly transitive.

### Average Path Length

- In real world, any two members in a networks are connected by a short path.

- **Friendship Paradox**: most people have fewer friends than their friends have.
- **Core-Periphery Structure**: a small group of people have many friends, while most people have few friends.

## Network Models

### Random Graphs

- For a graph $G(n, p)$ with $n$ nodes, any of the edges $\binom{n}{2}$ can be formed with probability $p$.
- For a graph $G(n, m)$ with $n$ nodes and $m$ edges, $|\Omega| = \binom{\binom{n}{2}}{m}$.


- Similarities:
  - When $n$ is large, both $G(n, p)$ and $G(n, m)$ act similarly
  - The expected number of edges in $G(n, p)$ is $p \binom{n}{2} = \frac{1}{2} p n (n-1)$
  - We can set $\binom{n}{2} = m$ to get $p = \frac{2m}{n(n-1)}$
- Differences:
  - $G(n, m)$ has fixed number of edges, while $G(n, p)$ has none or all possible edges

- The expected number of edges connected to a node (expected degree) for $G(n, p)$ is $c = p(n-1)$.
- The expected number of edges in $G(n, p)$ is $\binom{n}{2} p = \frac{1}{2} p n (n-1)$.

- The probability of observing $m$ edges is $P(|E| = m) = \binom{\binom{n}{2}}{m} p^m (1-p)^{\binom{n}{2} - m}$
  - $m$ edges are selected from $\binom{n}{2}$ edges
  - Each edge is selected with probability $p$, so $m$ edges are selected with probability $p^m$
  - Other edges are not selected with probability $1-p$, so $\binom{n}{2} - m$ edges are not selected with probability $(1-p)^{\binom{n}{2} - m}$

## Evolution of Random Graphs

- In a random graph, as we increase $p$, a larger fraction of nodes will have a path, i.e. connected.
- **Giant Component** is the largest connected component in a graph. $p = 0 \rightarrow$ no giant component, $p = 1 \rightarrow$ one giant component.

### Properties of Random Graphs

- Do not have a power-law degree distribution
- Underestimates the clustering coefficient
- Models the average path lengths well

#### 1st Phase Transition
- Occurs when the diameter value starts to shrink.
  - When $p = \frac{1}{n}$, the expected degree is 1, and the graph is disconnected.
  - Giant component appears when $p = \frac{\ln{n}}{n}$ starts to grow
  - Diameter starts to shrink and is at its maximum value

- $c < 1$: small isolated clusters, small diameters, short path lengths.
- $c = 1$: giant component appears, diameter peaks and path lengths are long.
- $c > 1$: almost all nodes are connected, diameter shrinks, path lengths shorten.

- $P(d_v = d) = \binom{n-1}{d}p^d(1-p)^{n-1-d}$
- $p = \frac{1}{n-1} \ln n$
- This is a binomial distribution with mean $c = (n-1)p = \ln n$ and variance $\sigma^2 = (n-1)p(1-p) = \ln n - \ln^2 n$
- $e^{-c} \frac{c^d}{d!}$. This will turn into a Poisson distribution with mean $c$ and variance $c$ when $n \rightarrow \infty$.

#### 2nd Phase Transition

- When the graph is connected and there are no nodes with degree 0
- $P(d_v = 0) = e^{-c}$ should be less than $\frac{1}{n}$
- Connectivity Threshold: $p = \frac{1}{n-1} \ln n$

- Expected clustering coefficient $C = p$ for $G(n, p)$
- The average path length in a random graph is $l \approx \frac{\ln |V|}{\ln c}$

### Small-World Model

- Lattice with high but fixed clustering coefficient and high average path length
- Start with a regular lattice and rewire edges with probability $p$.
- Parameter $0 \le \beta \le 1$ controls randomness.
- Regular lattice has $C = \frac{3(c-2)}{4(c-1)} \approx \frac{3}{4}$ and $l = \frac{n}{2c}$.
- $C(p) = (1 - p)^3(C(0))$

### Preferential Attachment Model

- The probability of a new node connecting to an existing node is proportional to the degree of the existing node.
- $P(v_i) = \frac{d_i}{\sum_{j}d_j}$


- **Degree Distribution**: $P(d) = \frac{2m^2}{d^3}$
- **Clustering Coefficient**: $C = \frac{m_0 - 1}{8} \frac{(\ln t)^2}{t}$
- **Average Path Length**: $l = \frac{\ln |V|}{\ln \ln |V|}$
