# Search

## Search Problem

- A **search problem** consists of
  - A **state space** (the set of all possible states)
  - A **start state** and **goal states**
  - A **set of actions** that can be taken to move from one state to another
  - A **successor function** that maps a state to a set of states that can be reached from that state by taking one of the available actions
- A **solution** to a search problem is a sequence of actions that leads from the start state to a goal state\

### Abstractions

- Real world is very complex
- Search problem formulas are models
  - State space must be asbstracted for the problem to be solvable
- Abstract state space
  - A state is a configuration of the world
  - A state is a node in a graph
- Abstract actions
  - An action is a change from one state to another
  - An action is an edge in a graph
  - Easier than the original problem
- Abstract solution

  - A solution is a path from the start state to a goal state
  - A solution is a sequence of edges in a graph

- The **World State** includes every detail of the environment
- The **Search State** includes only the relevant details for planning

#### Pacman Domain Example

- Problem: Path Finding
  - States: (x, y) position of Pacman and the food
  - Actions: (NSEW) movement of Pacman
  - Successor: (x, y) position of Pacman after the action
  - Goal test: (x, y) == END
- Problem: Eat all the food
  - States: (x, y) position of Pacman and the food (bool)
  - Actions: (NSEW) movement of Pacman
  - Successor: (x, y) position of Pacman after the action and the food (bool)
  - Goal test: no food left

#### Pacman Space Size Example

- World State:
  - Agent Positions: 12x10 = 120
  - Food Count: 30
  - Ghost Positions: 12
  - Agent facing: 4 (N, S, E, W)
- # World States: 120 _ 2\*\*30 _ 2\*_12 _ 4
  - This reflects the number of possible states in the world
- # States for path finding: 120
  - Number of possible positions for Pacman
- # States for eating all the food: 120 \* 2\*\*30
  - Number of possible positions for Pacman and the food

### State Space Graph

- A **state space graph** is a graph where
  - The nodes are states
  - The edges are successor as a result of actions
  - Goal test is a set of goal nodes
- The **state space graph** is a model of the search problem
  - It is a directed graph
- **Search Problem** is to find a minimum-cost path from the start to a goal states
  - The graphs are generated as needed, i.e. not all states are generated at once
  - In most cases, we can't build the entire graph

#### State Space Graph vs Search Trees

- Each node in the search tree is an entire path in the state space graph
- We construct both on demand and as little as possible

### Tree Search Algorithms (Sneak Peek)

- Expand tree nodes (potential plans)
- Maintain a fringe of partial plans under consideration
- Try to expand as few nodes as possible
