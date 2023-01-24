# Recurrence Relations and Master Method

## Reccurence

General form: $T(n) = aT(\frac{n}{b}) + f(n)$

### Examples

- **Binary Search**: $T(n) = T(\frac{n}{2}) + 1$. Where $a = 1$, $b = 2$, and $f(n) = 1$.
- **Merge and Quick Sort**: $T(n) = 2T(\frac{n}{2}) + cn$. Where $a = 2$, $b = 2$, and $f(n) = cn$.
- **Strassen Matrix Multiplication**: $T(n) = 7T(\frac{n}{2}) + cn^2$. Where $a = 7$, $b = 2$, and $f(n) = cn^2$.

---

## Master Method

- If $f(n) = O(n ^{\log _b a -\epsilon})$ for some $\epsilon > 0$, then $T(n) = \Theta(n ^{\log_b a})$.
- If $f(n) = \Omega(n ^{\log _b a + \epsilon})$ for some $\epsilon > 0$, then $T(n) = \Theta(f(n))$.
  - Iff $af(\frac{n}{b}) \le cf(n)$ for some $c < 1$ and large $n$.
- If $f(n) = \Theta(n ^{\log _b a })$, then $T(n) = \Theta(n ^{\log_b a} \log n)$.

**Compare the growth of 2 functions:** - $f(n)$ and $g(n) = n^{\log _b a}$

### The 3 disjoint cases

1. $f(n) = O(g(n) n^{- \epsilon})$ for some constant $\epsilon > 0$
2. $f(n) = \Theta (g(n))$
3. $f(n) = \Omega (g(n) n^{\epsilon})$ for some constant $\epsilon > 0$

### Usage

**Solve ${lim}_{n \to \infty} \frac{f(n)}{n^{\log_b a}}$**

**Case 2** - if ${lim} = c$ for some positive constant $c$.

- $f(n) = \Theta(n^{\log_b a})$
- $T(n) = \Theta ( \log(n) n ^ {\log _b a})$

**Case 1** - If ${lim} = 0$

- Find constant$\epsilon > 0$such that$f(n) = O(n ^{\log _b a -\epsilon})$
- $T(n) = \Theta (n ^ {\log _b a})$

**Case 3** - If ${lim} = \infty$

- Find constant $\epsilon > 0$ such that $f(n) = \Omega(n ^{\log _b a + \epsilon})$
- Find constant $c < 1$ such that $af(\frac{n}{b}) \le cf(n)$
- $T(n) = \Theta (f(n))$

**There are cases where the Master Method \*DOES NOT- work.**

---

### Master Method Examples

1. $T(n) = 8T(\frac{n}{2}) + n^2$

   We have $a=8$, $b=2$, and $f(n) = n^2$.

   - $\log _2 8 = 3$
   - $f(n) = n^2$ and $g(n) = n^3$

   **Find $\epsilon > 0$ such that $n^2$ is in $O(n^{3 - \epsilon})$.**

   - $T(n) = \Theta (n^3)$

2. $T(n) = T(\frac{n}{2} + 1)$

   We have $a=1$, $b=2$, and $f(n) = 1$.

   - $\log _2 1 = 0$
   - $f(n) = 1$ and $g(n) = 1$
   - $T(n) = \Theta (\log(n))$

3. $T(n) = 2T(\frac{n}{4}) + n^2$

   We have $a=2$, $b=4$, and $f(n) = n^2$.

   - $\log _4 2 = 0.5$
   - $f(n) = n^2$ and $g(n) = \sqrt{n}$
   - $af(\frac{n}{b}) \le cf(n)$ for $c \in [1/8, 1]$
     - $\frac{1}{8} n^2 \le cn^2$
   - $T(n) = \Theta (n^2)$

4. $T(n) = 4 T(\frac{n}{2}) + n^2 \log(n)$

   We have $a=4$, $b=2$, and $f(n) = n^2 \log(n)$.

   - $\log _2 4 = 2$
   - $f(n) = n^2 \log(n)$ and $g(n) = n^2$

   **Master method does not apply:**

   - $f(n)$ grows faster for Case 2.
   - Cannot find $\epsilon$ for and 3.
   - Case 1 does not apply as $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \log n \ne 0$.
