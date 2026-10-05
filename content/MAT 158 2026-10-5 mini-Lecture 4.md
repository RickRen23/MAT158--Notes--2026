
# Sequence Multiplication in Metric & Normed Spaces: Bounding Techniques

## 1. Problem Formulation

Let $(V, \|\cdot\|)$ be a **normed vector space** (or $\mathbb{R}^k$ / $\mathbb{C}$ equipped with the standard metric $d(a, b) = \|a - b\|$). 

Let $(x_n)_{n \in \mathbb{N}}$ and $(y_n)_{n \in \mathbb{N}}$ be two sequences in $V$ such that:
$$ \lim_{n \to \infty} x_n = x \quad \text{and} \quad \lim_{n \to \infty} y_n = y $$

We want to prove that the product sequence converges to $x \cdot y$ (where $\cdot$ denotes a continuous bilinear operation such as scalar multiplication, vector multiplication, or standard real multiplication):
$$ \lim_{n \to \infty} (x_n \cdot y_n) = x \cdot y $$

### Core Inequality 
$$ \|x_n y_n - xy\| = \|x_n y_n - x_n y + x_n y - xy\| \le \|x_n\| \|y_n - y\| + \|y\| \|x_n - x\| $$

To make this term smaller than a given $\varepsilon > 0$, we need to bound $\|x_n\|$ by a constant so that $x_n$ cannot explode. Below are three distinct methods to achieve this.

---

## 2. Method 1: The Standard Textbook Proof (Fixed Delta Bound)

### Core Idea
Fix an arbitrary safety bound (typically $\varepsilon_0 = 1$ or $\varepsilon_0 = \|x\|$) to bound $\|x_n\|$ by a constant $K$, then split the error budget $\varepsilon$ evenly across both terms.

### Step-by-Step Construction
1. **Bound $\|x_n\|$**:
   Since $x_n \to x$, choose $N_1 \in \mathbb{N}$ such that for all $n > N_1$:
   $$ \|x_n - x\| < 1 \implies \|x_n\| < \|x\| + 1 $$
   Set $K = \|x\| + 1 > 0$.

2. **Budget Allocation**:
   * Choose $N_2 \in \mathbb{N}$ such that for all $n > N_2$:
     $$ \|y_n - y\| < \frac{\varepsilon}{2K} = \frac{\varepsilon}{2(\|x\| + 1)} $$
   * Choose $N_3 \in \mathbb{N}$ such that for all $n > N_3$:
     $$ \|x_n - x\| < \frac{\varepsilon}{2(\|y\| + 1)} $$

3. **Synthesis**:
   Let $N = \max(N_1, N_2, N_3)$. For all $n > N$:
   $$
   \begin{aligned}
   \|x_n y_n - xy\| &\le \|x_n\| \|y_n - y\| + \|y\| \|x_n - x\| \\
   &< (\|x\| + 1) \cdot \frac{\varepsilon}{2(\|x\| + 1)} + \|y\| \cdot \frac{\varepsilon}{2(\|y\| + 1)} \\
   &< \frac{\varepsilon}{2} + \frac{\varepsilon}{2} = \varepsilon
   \end{aligned}
   $$
$$\epsilon_1 < \min\left(1, \frac{\varepsilon}{2(|x|+1)}, \frac{\varepsilon}{2(|y|+1)}\right)$$
---

## 3. Method 2: The Linear Weighting Method ($2\|x\| + \|y\|$)

### Core Idea
Avoid arbitrary constants like $1$ by directly using $\|x\|$ to bound $\|x_n\| < 2\|x\|$, creating a single unified weight factor $(2\|x\| + \|y\|)$.

> **Assumption**: Assume $\|x\| > 0$ and $\|y\| > 0$. (The case where $\|x\|=0$ or $\|y\|=0$ is trivial).

### Step-by-Step Construction
1. **Bound $\|x_n\|$ using $\|x\|$**:
   Select $\varepsilon_1 < \|x\|$. By convergence of $x_n$, $\exists N_1$ such that $\forall n > N_1$:
   $$ \|x_n - x\| < \|x\| \implies \|x_n\| < 2\|x\| $$

2. **Unified Coefficient**:
   $$ \|x_n y_n - xy\| < 2\|x\| \|y_n - y\| + \|y\| \|x_n - x\| $$

3. **Budget Allocation**:
   Set target tolerance $\varepsilon_2 = \frac{\varepsilon}{2\|x\| + \|y\|}$.
   Choose $N_2, N_3$ such that $\forall n > \max(N_2, N_3)$:
   $$ \|x_n - x\| < \varepsilon_2 \quad \text{and} \quad \|y_n - y\| < \varepsilon_2 $$

4. **Synthesis**:
   Let $N = \max(N_1, N_2, N_3)$. For all $n > N$:
   $$
   \begin{aligned}
   \|x_n y_n - xy\| &< 2\|x\| \left( \frac{\varepsilon}{2\|x\| + \|y\|} \right) + \|y\| \left( \frac{\varepsilon}{2\|x\| + \|y\|} \right) \\
   &= (2\|x\| + \|y\|) \cdot \frac{\varepsilon}{2\|x\| + \|y\|} = \varepsilon
   \end{aligned}
   $$

$$\epsilon_1<\min\left(|x|, \frac{\varepsilon}{2|x| + |y|}\right)$$
---

## 4. Method 3: The Fully Symmetric $\max / \min$ Method

### Core Idea
Treat $x$ and $y$ symmetrically by letting $M = \max(\|x\|, \|y\|)$ and constraining the fluctuation within $M$. This eliminates directional bias in the proof.

### Step-by-Step Construction
1. **Symmetric Bound Setup**:
   Let $M = \max(\|x\|, \|y\|) > 0$.
   Set safety radius $\varepsilon_1 = M$.

2. **Bound Sequences**:
   Choose $N_1$ such that $\forall n > N_1$:
   $$ \|x_n - x\| < M \implies \|x_n\| < \|x\| + M \le 2M $$

3. **Symmetric Budget Allocation**:
   Set target tolerance $\varepsilon_2 = \frac{\varepsilon}{3M}$ 
   Choose $N_2, N_3$ such that $\forall n > \max(N_2, N_3)$:
   $$ \|x_n - x\| < \frac{\varepsilon}{3M} \quad \text{and} \quad \|y_n - y\| < \frac{\varepsilon}{3M} $$

4. **Synthesis**:
   Let $N = \max(N_1, N_2, N_3)$. For all $n > N$:
   $$
   \begin{aligned}
   \|x_n y_n - xy\| &\le \|x_n\| \|y_n - y\| + \|y\| \|x_n - x\| \\
   &< 2M \cdot \frac{\varepsilon}{3M} + M \cdot \frac{\varepsilon}{3M} \\
   &= 3M \cdot \frac{\varepsilon}{3M} = \varepsilon
   \end{aligned}
   $$
$$\epsilon_1<\min\left(\max(|x|, |y|), \frac{\varepsilon}{3 \max(|x|, |y|)}\right)$$
