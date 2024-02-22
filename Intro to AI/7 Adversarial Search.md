# Adversarial Search

## Multi Agents

- AI agents often interact with other agents in the world
- **Cooperative Agents**: agents that work together to achieve a common goal
  - Ex: AI tutors, self-driving cars, etc.
- **Competitive Agents**: agents that work against each other to achieve their own goals
  - Ex: Chess, Go, Poker, etc.

## Zero-Sum Games

- General games:
  - Agents have independent utilities (values on outcomes)
  - Cooperation, competition, or both
- Zero-sum games:
  - Agents have opposite utilities
  - One agent's gain is the other agent's loss
  - Adversarial and competitive

### Game Trees

- **Game Tree**: a tree that represents the possible moves and outcomes of a game
  - Each node represents a state of the game
  - Each edge represents a move
  - Each leaf represents a terminal state
  - Each path from the root to a leaf represents a sequence of moves
- **Adversarial game tree**: a game tree where the agents are adversarial
- **Maximizing agent**: the agent that tries to maximize its utility

## Minimax Algorithm

- **Minimax Algorithm**: a decision-making algorithm for adversarial games
  - **Maximizing agent**: tries to maximize its utility
  - **Minimizing agent**: tries to minimize the maximizing agent's utility
- Players take turns making moves
- **Complete**: only if the tree is finite
- **Time**: $O(b^m)$
  - $b$: branching factor
  - $m$: maximum depth of the tree
- **Space**: $O(bm)$

```text
def minimax-decision(state):
    return action a maximizing min-value(result(a, state))
```

```text
def mav-value(state):
    if terminal state:
        return utility(state)

    v = -inf
    for each successor in successors(state):
        v = max(v, min-value(successor))

    return v
```

```text
def min-value(state):
    if terminal state:
        return utility(state)

    v = +inf
    for each successor in successors(state):
        v = min(v, max-value(successor))

    return v
```

## Alpha-Beta Pruning

- General idea: prune the search tree to reduce the number of nodes to be evaluated
- **Alpha-Beta Pruning**: a pruning algorithm for the minimax algorithm
  - **Alpha**: the best value found so far for the maximizing agent
  - **Beta**: the best value found so far for the minimizing agent
- **Time**: $O(b^{m/2})$
  - $b$: branching factor
  - $m$: maximum depth of the tree
- **Space**: $O(bm)$

### Pseudocode

1. Start with alpha = -inf and beta = +inf
2. At each max node, update alpha with the maximum value found so far
3. At each min node, update beta with the minimum value found so far
4. If alpha >= beta, prune the subtree
5. Return the best action found so far
6. Continue until the search is complete

```text
def alpha-beta-search(state):
    v = max-value(state, -inf, +inf)
    return the action in successors(state) with value v
```

```text
def max-value(state, alpha, beta):
    if terminal state:
        return utility(state)

    v = -inf
    for each successor in successors(state):
        v = max(v, min-value(successor, alpha, beta))
        if v >= beta:
            return v
        alpha = max(alpha, v)

    return v
```

```text
def min-value(state, alpha, beta):
    if terminal state:
        return utility(state)

    v = +inf
    for each successor in successors(state):
        v = min(v, max-value(successor, alpha, beta))
        if v <= alpha:
            return v
        beta = min(beta, v)

    return v
```

### Properties

- Pruning does not affect minimax value computed for the root
- **Caveat** values of intermediate nodes might be wrong
- **Optimality**: alpha-beta pruning is optimal if the nodes are evaluated in the correct order]
  - With 'perfect-ordering', time complexity is $O(b^{m/2})$
  - Doubles the depth of search for the same computational cost
- **Branching factor**: the effective branching factor is the square root of the original branching factor
- **Resource Limits**: alpha-beta pruning can be stopped at any time and return the best move found so far
  - Useful for real-time games that don't have finite search trees
  - **Cutoff test**: a test to determine whether to stop the search and return the best move found so far
  - **Evaluation function**: a function to estimate the value of a state when the search is cut off
