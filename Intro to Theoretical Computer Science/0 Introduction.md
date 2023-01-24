# Introduction to Theoretical Computer Science

## Mathematical Notions

- Universal Quantifier $\forall$: "For All" elements.
- Existential Quantifier $\exists$: "There Exists" an element.
- Conjunction $\land$: Logical $\text{and}$ operator $x \And y$
- Disjunction $\lor$: Logical $\text{or}$ operator $x | y$

## Sets

A set is a group of objects represented as a unit. The objects of a set S are called elements or members of S.

Example: $\{1, 2, 3\}$, $\{a, b, c\}$, $\{a, 1, \text{hello}\}$

Membership: $x \in S$ or $x \notin R$,
where $x$ is an element and $S$ is a set
and $x$ is not an element of $R$.

- Order of elements does not matter.
- Duplicate elements are not allowed.
- **Cardinality**: the number of elements in a set. $\mid S \mid$.
  - A set with no elements is called the **empty set** and is denoted by $\emptyset$.
- Sets can be defined by their properties. Example: $S = \{x \mid x = m^2 \land \exists m \in \N$.

### Subsets

A set $A \subseteq B$ is a **subset** of $B$ if every element of $A$ is also an element of $B$.

A set $A \subset B$ is a **proper subset** of $B$ if every element of $A$ is also an element of $B$ and $A \neq B$.

### K-Tuples (Ordered Sets)

A k-tuple is an ordered set.
Tuples with more than two members (k-members) are called k-tuples.

### Operations

- Union: $A \cup B = \{x \mid x \in A \lor x \in B\}$
- Intersection: $A \cap B = \{x \mid x \in A \land x \in B\}$
- Subtraction: $A - B = \{x \mid x \in A \land x \notin B\}$

### Cartesian Product

The Cartesian product of two sets $A$ and $B$ is the set of all ordered pairs $(a, b)$ where $a \in A$ and $b \in B$.
The order of the elements in the pair matters (non-commutative): $A \times B \neq B \times A$.

Example:

$A = \{1, 2, 3\}$ and $B = \{x, y\}$

$A \times B = \{(1, x), (1, y), (2, x), (2, y), (3, x), (3, y)\}$
$B \times A = \{(x, 1), (x, 2), (x, 3), (y, 1), (y, 2), (y, 3)\}$

---

## Fundamental Questions

- What are fundamental capabilities and limitations of computers?
- What makes some problems hard and others easy?
- Can we systematically build machines that have proven characteristics?

Goal: Answer these questions in an abstract and general manner that is independent of the actual physical hardware for computation.

## Theory of Computation

The theory of computation is the study of algorithms, their efficiency, and the limits of their power.
It includes the study of computability, which deals with the question of what problems can be solved by algorithms, and complexity theory, which deals with the question of how efficiently problems can be solved.
The theory of computation also encompasses the study of various models of computation, such as Turing machines and the lambda calculus, which provide a formal framework for understanding the properties of algorithms and the limits of their power.

The three main areas of theory of computation are:

- **Automata Theory**: building abstract machines.
- **Computability Theory**: Fundamental capabilities and limitations of abstract machines.
- **Complexity Theory**: Why certain problems are harder than others.

## Automata Theory

Automata theory is the study of abstract machines that can be used to model computation.

An abstract machine is essentially a mathematical model of computation.

### Finite Automata

An abstract machine that can capture systems with a finite number of states.

- Models simple tasks that need to be repeated.
- Easy to implement with limiter hardware and software.
- Easy to design and visualize.
- Easy to verify correctness.

Examples: Push Button and Elevator

### Pushdown Automata

An abstract machine that can capture systems with a finite  number of states and a stack (memory).

- Writes to stack.
- At each step, only the top symbol of stack can be accessed to perform read/write.
  - It can either be kept or removed.
  - or new symbol can be pushed.

Examples: Compiler and Calculator.

### Turing Machines

An abstract machine that can capture systems that can manipulate symbols on a strip of tape.

- The tape is infinite.
- Can both read and write to tape.
- The tape can move bidirectionally.
- Special states for rejecting and accepting take effect immediately.

While simple, Turing machines can model any given computer algorithm and its logic.

## Complexity Theory

Complexity theory is the study of the efficiency of algorithms and the limits of their power.
It is concerned with the question of how efficiently problems can be solved.

## Computability Theory

Computability theory is the study of the fundamental capabilities and limitations of abstract machines.
It is concerned with the question of what problems can be solved by algorithms.
Identify problems that can and can't be solved via reducibility.
