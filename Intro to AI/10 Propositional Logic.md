# Propositional Logic

- **Propositional logic** is a simple language for expressing facts.

  - **Atomic sentence**: a simple fact.
  - **Connectives**: $\neg$ (not), $\land$ (and), $\lor$ (or), $\Rightarrow$ (implies), $\Leftrightarrow$ (if and only if).
  - **Sentence**: a fact expressed in propositional logic.

- **Negation** ($\neg$): $M(\neg \alpha) = \{m \mid m \not\models \alpha\}$.
- **Conjunction** ($\land$): $M(\alpha \land \beta) = M(\alpha) \cap M(\beta)$.
- **Disjunction** ($\lor$): $M(\alpha \lor \beta) = M(\alpha) \cup M(\beta)$.
- **Implication** ($\Rightarrow$): $M(\alpha \Rightarrow \beta) = \overline{M(\alpha)} \cup M(\beta) = \overline{M(\alpha) \backslash  M(\beta)}$.
- **Biconditional** ($\Leftrightarrow$): $M(\alpha \Leftrightarrow \beta) = \overline{M(\alpha) \backslash  M(\beta)} \cap \overline{M(\beta) \backslash  M(\alpha)} = (\overline{M(\alpha) \cap  M(\beta)}) \cup (M(\alpha) \cap M(\beta))$.

## Propositional Logic Semantics Truth Table

| p   | q   | $\neg p$ | $\neg q$ | $p \land q$ | $p \lor q$ | $p \Rightarrow q$ | $p \Leftrightarrow q$ |
| --- | --- | -------- | -------- | ----------- | ---------- | ----------------- | --------------------- |
| T   | T   | F        | F        | T           | T          | T                 | T                     |
| T   | F   | F        | T        | F           | T          | F                 | F                     |
| F   | T   | T        | F        | F           | T          | T                 | F                     |
| F   | F   | T        | T        | F           | F          | T                 | T                     |


## Inference

- How to determine if $KB$ entails $\alpha (KB \models \alpha)$?
  - Inference engine $i$ derives $\alpha$ from $KB$: $KB \vdash_i \alpha$. 
  - **Soundness**: everything it derives is in fact entailed (i.e. $KB \vdash_i \alpha \Rightarrow KB \models \alpha$).
  - **Completeness**: everything that is entailed can be derived (i.e. $KB \models \alpha \Rightarrow KB \vdash_i \alpha$).


1. **Model checking**: enumerate all models of $KB$ and check if $\alpha$ is true in all of them.
2. **Theorem proving**: use logical rules to determine if $\alpha$ is true in all models of $KB$.

### Inference by Enumeration

- **Model checking**: enumerate all models of $KB$ and check if $\alpha$ is true in all of them.
  - **Exhaustive**: check all possible worlds.
  - **Incomplete**: may not find a model if there are infinitely many.

### Inference by Theorem Proving

- **Theorem proving**: use logical rules to determine if $\alpha$ is true in all models of $KB$.
  - **Sound**: if $KB \vdash_i \alpha$ then $KB \models \alpha$.
  - **Complete**: if $KB \models \alpha$ then $KB \vdash_i \alpha$.

### Logical Equivalence

- **Logical equivalence**: two sentences are equivalent if they have the same truth value in all models.
  - $\alpha \equiv \beta$ if $M(\alpha) = M(\beta)$.
  - $\alpha \equiv \beta$ if $\alpha \Leftrightarrow \beta$ is a tautology.

### Theorem Proving by Deduction

- **Deduction**: derive new sentences from old ones.
  - **Modus Ponens**: if $\alpha$ and $\alpha \Rightarrow \beta$ are true, then $\beta$ is true.
  - **Resolution**: if $\alpha \lor \beta$ and $\neg \alpha \lor \gamma$ are true, then $\beta \lor \gamma$ is true.

### Theorem Proving by Refutation

- **Refutation**: show that $\neg \alpha$ is unsatisfiable.
  - **Resolution**: if $\alpha \land \beta$ is unsatisfiable, then $\neg \alpha \lor \neg \beta$ is true.
  - **Soundness**: if $KB \vdash_i \alpha$ then $KB \models \alpha$.
  - **Completeness**: if $KB \models \alpha$ then $KB \vdash_i \alpha$.
