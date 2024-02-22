# Informed Search

- Issues with Uninformed Search
  - Explores options in every direction
  - No information about the goal

## Search Heuristics

- **Heuristic**: A function that estimates how close a state is to a goal
  - Example: Manhattan distance and Euclidean distance for pathfinding
  - **Admissible**: A heuristic that never overestimates the cost to reach the goal
  - **Consistent**: A heuristic that satisfies the triangle inequality
    - $h(A) - h(C) \leq cost(A to C)$

## Best-First Search

- Use a heuristic to identify the most promising node to expand
- Fringe is a priority queue sorted in decreasing order of heuristic value
- Special cases:
  - Greedy Best-First Search: Expand the node that appears to be closest to the goal
  - A\* Search: Expand the node that appears to be the best combination of cost and heuristic value

### Greedy Best-First Search

- Expand the node that appears to be closest to the goal
- **Problem**: May not find the optimal solution
- **Worst Case**: badly guided DFS with potential to miss the goal
- **Time** complexity: O(b^m), where b is the branching factor and m is the maximum depth of the search space
  - A good heuristic can improve the time complexity
- **Space** complexity: O(b^m)
- **Completeness**: No, may get stuck in a loop
- **Optimality**: No, may not find the optimal solution

### A\* Search

- Combining Uniform Cost Search and Greedy Best-First Search
  - **UCS**: Expand the node with the lowest path cost (g(n))
  - **Greedy**: Expand the node that appears to be closest to the goal (h(n))
  - **A**: Expand the node that appears to be the best combination of cost and heuristic value (f(n) = g(n) + h(n))
- Expand the node that appears to be the best combination of cost and heuristic value
