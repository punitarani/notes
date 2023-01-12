# Introduction to Theoretical Computer Science

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
