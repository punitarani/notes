# The Computing Model and Asymptotic Notations

## Problems, Instances, and Algorithms

* A **problem P** is a binary relation on a **set I of problem instances** and a **set S of problem solutions**.
* An **algorithm A** is a deterministic **computational procedure to solve a P in finite time**.
* **Time Complexity is the number of steps** an algorithm takes to solve a problem instance.
* **Space Complexity is the amount of memory** an algorithm uses to solve a problem instance.

## Important Summations

| Problem                                             | Counting Technique                            |
| --------------------------------------------------- | --------------------------------------------- |
| $1 + 2 + 3 + ... + n = \sum_{1}^{n} x $             | $\frac{n(n+1)}{2}$                            |
| $1^2 + 2^2 + 3^2 + ... + n^2 = \sum_{1}^{n} x^2 $   | $\frac{n(n+1)(2n+1)}{6}$                      |
| $1 + x + x^2 + x^3 + ... + x^n = \sum_{1}^{n} x^n $ | $\frac{1-x^{n+1}}{1-x}$ for $\|x\| < 1$     |
| $1 + \frac{1}{2} + \frac{1}{3} + ... + \frac{1}{n}$ | $\epsilon (\ln n + \frac{1}{n}, \ln n + 1)$ |
| $\int \frac{1}{x} dx$                               | $\ln x$                                       |

## Asymptotic Notations

$n! > c^n > n^c > n^2 > nlogn > n > \sqrt n > \log n > 1$

* Big $O$ is the **upper bound** on the growth of a function.
* Big $\Omega$ is the **lower bound** on the growth of a function.
* Big $\Theta$ is the **tight bound** on the growth of a function.
  * $\Theta$ is the intersection of $O$ and $\Omega$.

* If $f(n) = O(n)$ and $f(n) = \Omega(n)$, then $f(n) = \Theta(n)$.
* If $f(n) = \Theta(n)$, then $f(n) = O(n)$ and $f(n) = \Omega(n)$.

* $lim _{n→ \infty} \frac {f(n)}{g(n)} = c > 0$, then $f(n) = \Theta (g(n))$.
* $lim _{n→ \infty} \frac {f(n)}{g(n)} < \infty$, then $f(n) = O (g(n))$.
* $lim _{n→ \infty} \frac {g(n)}{f(n)} < \infty$, then $f(n) = \Omega (g(n))$.

Following are true for all notations:

1. **Transitivity**: If $f(n) = O(g(n))$ and $g(n) = O(h(n))$, then $f(n) = O(h(n))$.
2. **Reflexivity**: If $f(n) = O(f(n))$.

* **Symmetry**: $f(n) = \Theta (g(n))$, **IFF** $g(n) = \Theta (f(n))$.
* **Transpose Symmetry**: $f(n) = O(g(n))$, **IFF** $g(n) = \Omega (f(n))$.

## Activation Records

Managed via a stack. **One activation record per function call.**
AR of callee is on top of caller. **AR is popped of once function returns.**
AR reserves space for variables and intermediate results.
