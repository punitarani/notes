# Search Uncertainty

- Minimax cannot handle uncertainty
  - **Uncertainty**: when the outcome of an action is not known
  - What if the opponent doesn't play optimally/adversarially and is random?

## Expectimax Algorithm

- **Expectimax Algorithm**: a decision-making algorithm for games with uncertainty
  - **Maximizing agent**: tries to maximize its utility
  - **Chance node**: a node that represents the average utility of its children
  - **Expectation**: the average utility of the children
  - **Complete**: only if the tree is finite
  - **Time**: $O(b^m)$
    - $b$: branching factor
    - $m$: maximum depth of the tree
  - **Space**: $O(bm)$
- ## We have a probabilistic model of how the opponent or environment will behave in any state

```text
def value(state):
    if terminal state:
        return utility(state)

    if next agent is max:
        return max-value(state)
    if next agent is min:
        return min-value(state)
    if next agent is exp:
        return exp-value(state)
```

```text
def max-value(state):
    if terminal state:
        return utility(state)

    v = -inf
    for each successor in successors(state):
        v = max(v, value(successor))

    return v
```

````text
def min-value(state):
    if terminal state:
        return utility(state)

    v = +inf
    for each successor in successors(state):
        v = min(v, value(successor))

    return v

```text
def exp-value(state):
    v = 0
    for each successor in successors(state):
        v += p(successor) * value(successor)
    return v
````

## Monte Carlo Tree Search (MCTS)

- **Evaluation by Rollouts**: estimate value of a state by playing many games (random actions or some fast policy) and count the wins/losses
- **Selective Search**: explore parts of the tree that will help improve the decision at root, regardless of depth
- **UCT (Upper Confidence Bound for Trees) Algorithm**: a decision-making algorithm for games with uncertainty
