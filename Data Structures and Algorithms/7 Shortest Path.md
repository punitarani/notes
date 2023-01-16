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
