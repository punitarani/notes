# Logic Agents

## Knowlege-based Agents

- **Knowledge-based agents** use a knowledge base to reason and plan.
  - **Knowledge base**: domain-specific facts. Set of sentences in a formal language.
  - **Inference engine**: reasoning and planning.
  - Knowledge base is fixed with no ability to incorporate new knowledge.
- Agents acquire knowledge through perception, learning, and language
  - **Transition model**: knowledge of effects of actions.
  - **Sensor model**: knowledge of effects of perception.
  - **Learning model**: knowledge of how to learn from experience.

## Logic

- **Syntax**: what sentences are allowed?
- **Semantics**: what are the possible worlds? What sentences are true in which worlds?

### Entailment

- **Entailment** means that one thing follows from another.
  - $KB \models \alpha$ means that $\alpha$ is true in all worlds where KB is true.
- Models: formlly structured worlds to evaluate sentences.
  - $m$ is a model of $\alpha$ if $\alpha$ is true in $m$.
  - $M(\alpha)$ is the set of all models of $\alpha$.
  - $KB \models \alpha$ if $M(KB) \subseteq M(\alpha)$.

### Applications of Logic in AI

- Automated reasoning
  - Localization: using a map and sequence of sensor readings to determine the agent's location.
  - Mapping: given a sequence of sensor readings, determine the map of the environment.
- Automated planning
  - Given a description of the initial state, the possible actions, and the goal, find a sequence of actions to achieve the goal.

## Propositional Logic

- **Propositional logic** is a simple language for expressing facts.
  - **Atomic sentence**: a simple fact.
  - **Connectives**: $\neg$ (not), $\land$ (and), $\lor$ (or), $\Rightarrow$ (implies), $\Leftrightarrow$ (if and only if).
  - **Sentence**: a fact expressed in propositional logic.

### Propositional Logic Syntax

- Propositional symbols ${X_1, X_2, \ldots, X_n}$.
  - often add $True (T)$ and $False (F)$ for convenience.
- Grammar of Sentences
  - A variable (atom) $X_i$ is a sentence.
  - **Negation**: if $\alpha$ is a sentence, then $\neg \alpha$ is a sentence.
  - **Conjunction**: if $\alpha$ and $\beta$ are sentences, then $(\alpha \land \beta)$ is a sentence.
  - **Disjunction**: if $\alpha$ and $\beta$ are sentences, then $(\alpha \lor \beta)$ is a sentence.
  - **Implication**: if $\alpha$ and $\beta$ are sentences, then $(\alpha \Rightarrow \beta)$ is a sentence.
  - **Biconditional**: if $\alpha$ and $\beta$ are sentences, then $(\alpha \Leftrightarrow \beta)$ is a sentence.

### Propositional Logic Semantics

- Let $\omega$ be a truth assignment to ${X_1, X_2, \ldots, X_n}$.
  - If $\alpha$ is a symbol then its truth value is given in $\omega$.
- $\omega \models \alpha$ iff $\omega \not\models \neg \alpha$.
- $\omega \models \alpha \land \beta$ iff $\omega \models \alpha$ and $\omega \models \beta$.
- $\omega \models \alpha \lor \beta$ iff $\omega \models \alpha$ or $\omega \models \beta$.
- $\omega \models \alpha \Rightarrow \beta$ iff $\omega \models \alpha$ implies $\omega \models \beta$ (i.e. $\omega \not\models \alpha$ or $\omega \models \beta$).
- $\omega \models \alpha \Leftrightarrow \beta$ iff $\omega \models \alpha \Rightarrow \beta$ and $\omega \models \beta \Rightarrow \alpha$.

### Parse Tree

- A parse tree is a tree representation of the syntactic structure of a sentence.
- Precedence of operators: $\neg, \land, \lor, \Rightarrow, \Leftrightarrow$.
