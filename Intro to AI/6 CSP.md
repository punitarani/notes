# Constraint Satisfaction Problems (CSPs)

- Standard Search Problem:
  - Atomic State Space: each state is a "black box" with arbitrary data structure
  - Goal Test: check if the state is a goal
- Constraint Satisfaction Problem (CSP):
  - State is defined by a set of variables $X = \{X_1, X_2, \ldots, X_n\}$ and values from domains $D = \{D_1, D_2, \ldots, D_n\}$
  - Goal Test: check if the state satisfies all the constraints $C$ that specify allowable combinations of values
- Simple example of a _formal language representation_
- Allows useful general-purpose algorithms with more power than standard search algorithms

## Constraint Graphs

- **Constraint Graph**: Graph where each node represents a variable and each edge represents a constraint
- **Binary CSP**: CSP where each constraint relates at most two variables
- **Binary Constraint Graph**: nodes represent variables and edges represent constraints

- Real-World CSPs
  - Assigment problems (e.g. who teaches what class)
  - Timetabling problems (e.g. which class is scheduled in which room at which time)
  - Scheduling problems (e.g. which tasks to do in which order)
  - Hardware and software configuration (e.g. which components to use in a computer)
  - Transportation and logistics (e.g. which delivery truck to send where)
  - Floorplanning (e.g. where to place furniture in a room)
  - Circuit layout (e.g. how to lay out components on a chip)

## Backtracking Search for CSPs

- The basic idea is to search for a solution by trying out different values for each variable
- **Backtracking Search**: a form of depth-first search where the search tree is a tree of assignments
- **Variable Assignments**: each node in the tree represents the assignment of a value to a variable
- **Constraint Propagation**: enforcing restrictions on the values that can be assigned to variables
- **Backtracking**: when a variable has no legal values left to assign, we backtrack to the most recent variable that has legal values to try
- **Idea 1**: one variable at a time
  - Variable orders are commutative, so the order in which we assign variables doesn't matter
  - Only consider the constraints when making assignments
  - **Minimum Remaining Values (MRV)**: choose the variable with the fewest legal values
- **Idea 2**: consider the constraints when making assignments
  - Choose the value that rules out the fewest values in the remaining variables
  - Incremental Goal Test
  - **Least Constraining Value (LCV)**: choose the value that rules out the fewest values in the remaining variables
- Backtracking = DFS + variable-ordering + fail-on-violation

```text
function Backtracking-Search(csp) returns solution/failure
    return Recursive-Backtracking({}, csp)

function Recursive-Backtracking(assignment, csp) returns solution/failure
    if assignment is complete then
        return assignment
    var ← Select-Unassigned-Variable(Variables[csp], assignment, csp)
    for each value in Order-Domain-Values(var, assignment, csp) do
        if value is consistent with assignment given Constraints[csp] then
            add {var = value} to assignment
            result ← Recursive-Backtracking(assignment, csp)
            if result ≠ failure then
                return result
            remove {var = value} from assignment
    return failure
```

### Improve Backtracking

- Ordering
  - Which variable should be assigned next?
  - In what order should its values be tried?
- Filtering
  - Can we detect inevitable failure early?
- Structure
  - Can we take advantage of problem structure?

### Minimum Remaining Values (MRV) Ordering

- **Minimum Remaining Values (MRV)**: choose the variable with the fewest legal values ("most constrained variable")
- Minimum instead of maximum because we want to fail as early as possible ("fail-fast ordering")

### Least Constraining Value (LCV) Ordering

- **Least Constraining Value (LCV)**: choose the value that rules out the fewest values in the remaining variables
- Choose the value that rules out the fewest values in the remaining variables
- Least instead of most because we want to keep as many options open as possible

### Forward Checking (FC) Filtering

- **Forward Checking (FC)**: keep track of remaining legal values for unassigned variables
- Cross off values that violate a constraint when added to existing assignments
- Terminate search when any variable has no legal values
- **Constraint Propagation**: enforcing restrictions on the values that can be assigned to variables
  - Forward checking propagates information from assigned to unassigned variables
  - It does not provide early detection of all failures

### Arc Consistency (AC) Filtering

- **Arc Consistency (AC)**: a variable $X_i$ is arc-consistent with another variable $X_j$ if for every value in the current domain of $X_i$, there is some consistent value of $X_j$
- Forward checking only enforces consistency of arcs pointing to each new assigmnet
- Arc consistency enforces consistency between every pair of variables
- Arc consistency detects failures earlier than forward checking
- It can be used as a preprocessing step to reduce the search space
- It can be more effective by combining MRV ehuristic with constraint propagation

#### K-Consistency

- Increasing degrees of consistency
  - 1-consistency: node consistency
    - Each node's domain has a value satisfying the node's unary constraints
  - 2-consistency: arc consistency
    - Each arc's domain has a value satisfying the arc's binary constraints
  - k-consistency: for each set of $k$ nodes, any consistent assignment to $k-1$ of them can be extended to a consistent assignment to the $k$th

### Tree-Structured CSPs

- **Tree-Structured CSP**: CSP where the constraint graph is a tree
- Theorem: if the constraint graph is a tree, the CSP can be solved in $O(n \cdot d^2)$ time
  - $n$: number of variables
  - $d$: size of the largest domain
  - For general CSPs, worst case is $O(d^n)$

#### Algorithm

1. Choose a variable as the root and order the variables such that parents come before children
2. (Remove backward) For each variable $X_i$ in the order, remove $X_i$ from the graph by making it a child of its parent $X_j$
3. (Assign forward) For each variable $X_i$ in the order, assign $X_i$ a value that is consistent with the values of its parent $X_j$

- **Claim 1**: after backward pass, all root-to-leaf arcs are consistent
- **Claim 2**: if root-to-leaf arcs are consistent, forward assignment will not backtrack

#### Nearly Tree-Structured CSPs

- **Conditioning**: instantiate a variable and remove it from the graph
- **Cutset Conditioning**: instantiate a set of variables and remove them from the graph
- **Cutset Size**: $C = \text{runtime} O(d^C(n - C) d^2)$
  - $n$: number of variables
  - $d$: size of the largest domain
  - $C$: size of the cutset

#### Cutset Conditioning

1. Choose a cutset of variables
2. Instantiate the cutset variables (all possible ways)
3. Compute residual CSP for each assignment
4. Solve the residual tree-structured CSPs

#### Iterative Algorithms for CSPs

- **Idea**: move between complete assignments until all constraints are satisfied
  - Allow states with unsatisfied constraints
  - Operators reassign variable values
- **Algorithm**:
  - Variable selection: randomly select a conflicted variable
  - Value selection (by min-conflicts heuristic): choose the value that violates the fewest constraints
