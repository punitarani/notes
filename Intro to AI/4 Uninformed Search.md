# Uninformed Search

## Background and Terms

- Search Problem
  - States (configurations of the world)
  - Actions (changes from one state to another)
  - Costs (of actions)
  - Successor Function (world dynamics: state -> set of states)
  - Initial and Goal States
- Search Tree
  - Nodes: represent plans for reaching states
  - Plans have costs (sum of action costs)
- Search Algorithm

  - Systematically build a search tree
  - Chooses an order to expand fringe (unexplored nodes)
  - Optimal: finds the lowest-cost path

- Fringe: partial plans under consideration (set of leaf nodes)
- Node Expansion: generation of successors for a fringe node
- Exploration Strategy: which node from the fringe should be expanded

## Uninformed Search

- Use only the information available in the problem definition

  - Depth-First Search
  - Breadth-First Search
  - Depth-Limited Search
  - Iterative Deepening Search
  - Uniform-Cost Search

- Search Properties

  - **Completeness**: does it always find a solution if one exists?
  - **Optimality**: does it always find the least-cost solution?
  - **Time Complexity**: number of nodes generated and expanded
  - **Space Complexity**: maximum number of nodes in memory

- Time and space complexity are measured in termsof
  - b: maximum branching factor of the search tree
  - d: depth of the least-cost solution
  - m: maximum depth of the state space (may be infinite)

### Depth-First Search

- Expand a deepest unexpanded node first
- Fringe: LIFO (Last-In-First-Out) stack
- Time complexity: $O(b^m)$
- Space complexity: $O(bm)$ (only the siblings on path to the root)
- Complete: No, m could be infinite
- Optimal: No, it finds the "leftmost" solution regardless of cost and depth

### Breadth-First Search

- Expand the shallowest unexpanded node first
- Fringe: FIFO (First-In-First-Out) queue
- Time complexity: $O(b^d)$
- Space complexity: $O(b^d)$ (all nodes at depth d)
- Complete: Yes, as d is finite if a solution exists
- Optimal: Yes, it finds the least-cost solution

### Iterative Deepening Search

- Depth-Limited Search with increasing depth limits
  - DFS space advantage with BFS time and shallow-solution advantage
- Time complexity: $O(b^d)$
- Space complexity: $O(bd)$
- Complete: Yes, as d is finite if a solution exists
- Optimal: Yes, if all the costs are the same (1)

### Uniform-Cost Search

- Expand the least-cost unexpanded node first
- Fringe: priority queue ordered by path cost
- Time complexity: $O(b^{C^* / \epsilon})$
  - Process all nodes with cost less than optimal solution $C^* + \epsilon$
  - Let $C^*$ be the cost of the optimal solution and $\epsilon$ be the minimum cost of an action
- Space complexity: $O(b^{C^* / \epsilon})$
- Complete: Yes, as long as the cost of the actions $C^*$ and $\epsilon > 0$
- Optimal: Yes, it finds the least-cost solution by expanding in increasing order of path cost.

#### Problems with Uniform-Cost Search

- Note: Explores increasing cost contours
- Good: UCS is complete and optimal
- Bad:
  - Explores options in every direction
  - No information about distance and direction to goal

### Summary

| Criterion | Breadth-first | Uniform-cost      | Depth-first  | Depth-limited            | Iterative deepening |
| --------- | ------------- | ----------------- | ------------ | ------------------------ | ------------------- |
| Complete? | Yes           | Yes               | No           | No unless \( l \geq d \) | Yes                 |
| Optimal?  | Yes           | Yes               | No           | No                       | Yes                 |
| Time      | \( O(b^d) \)  | \( O(b^{c^\*}) \) | \( O(b^m) \) | \( O(b^l) \)             | \( O(b^d) \)        |
| Space     | \( O(b^d) \)  | \( O(b^{c^\*}) \) | \( O(bm) \)  | \( O(bl) \)              | \( O(bd) \)         |
