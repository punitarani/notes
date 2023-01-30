# Introduction

## What is a Programming Language?

- A way to communicate instructions to a computer
  - Communicate an algorithm
  - Describe a process
  - Communicate a system to another person

## How do we communicate instructions to a computer?

- Programs translate code into assembly language then machine code (binary)
- Compilers: Translate code into executable binary
- Interpreters: Translate and execute a program
- Transpilers: Translate code into another language

## What defines a programming language?

- **Syntax**: How the program should be written.
  - Set of rules that govern the structure and arrangement of the language's elements, such as keywords, operators, and expressions.
  - Defines how to write a correct program in a given language.
- **Semantics**: What the program should do.
  - The meaning of the language.
  - Defines the behavior of the program and how the language's elements are used to create that behavior.
  - Deals with the logical structure of the program and how the various.

## Lexer

- A program that reads a source file and breaks it into tokens.
  - This is the first step in the compilation process.
- A token is a sequence of characters that is meaningful to the compiler.
  - A token can be a keyword, an identifier, a literal, or a symbol.

## Grammar

- A grammar is a set of rules that describe the structure of a language.
- It specifies the valid combinations of tokens that make up a program.
- It is the foundation of a compiler and a programming language.

### Backus-Naur Form (BNF)

- BNF is a metalanguage and notation for describing the syntax of programming languages and other types of text.
- It defines a set of rules that specify the structure of a language.
- Each rule describes a different non-terminal symbol and the sequence of terminal symbols that can replace it.
- Terminal symbols are the actual characters of the language, such as keywords, operators, and punctuation.
- Non-terminal symbols represent the different syntactic elements of the language, such as statements, expressions, and declarations.
- BNF is widely used to specify the syntax of programming languages, and many programming languages have a BNF grammar that defines their syntax.

Example:

```text
<list> ::= <item> | <item> , <list>
<item> ::= [A-Za-z]+
<number> ::= [0-9]+

<expression> ::= <term> + <expression> | <term>
<term> ::= <factor> * <term> | <factor>
<factor> ::= <number> | ( <expression> )
```
