# Lexical Analysis

## Language Syntax

- A language's syntax is the set of rules that govern the structure and arrangement of the language's elements, such as keywords, operators, and expressions.
  - Programmers know what is and isn't valid syntax.
  - Compilers can read programs and enforce syntax rules.
- Tokens are abstractions on top of the low-level alphabet of characters.
  - Words, sentences, paragraphs, etc.

### Strings

- Strings are combinations of alphabet symbols.
  - $\Sigma$ is the alphabet of symbols.
  - $\epsilon$ is the empty string.
  - $\epsilon + s = s \epsilon$ represents the concatenation of strings.
- Enclosed in "double quotes" or [_italics with dark blue_](#strings).

### Languages

- $\Sigma$ represents the set of all symbols in an alphabet.
- $\Sigma^*$ represents the set of all strings over $\Sigma$.
  - Contains all strings that can be constructed from $\Sigma$.
- A language $L$ over $\Sigma$ is a set of strings over $\Sigma$.
  - $L \subseteq \Sigma^*$.

## Regular Expressions

- Regular expressions are a way to describe languages.
  - They are compact, expressive, precise, and easy to parse.
- Tokens are typically described using regex.
- Usually represented by $R$

- A regular expression is either
  1. $\phi$
  2. $\epsilon$
  3. $a$, where $a \in \Sigma$
  4. $R_1 | R_2$
  5. $R_1 \cdot R_2$
  6. $(R)$
  7. $R^*$

- The Language $L(R)$ is given by:
  1. $L(\phi) = \phi$
  2. $L(\epsilon) = \{\epsilon\}$
  3. $L(a) = \{a\}$
  4. $L(R_1 | R_2) = L(R_1) \cup L(R_2)$
  5. $L(R_1 \cdot R_2) = L(R_1) \cdot L(R_2)$
