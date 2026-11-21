# Sharing Model Uncertainty — Part I

**Paper:** Hara, C., Mukerji, S., Riedel, F., & Tallon, J.-M. (2026). *Sharing Model Uncertainty*. *American Economic Journal: Microeconomics*, 18(2), 313–347. [DOI](https://doi.org/10.1257/mic.20240188).

These notes review the concepts I studied before the seminar, mainly for understanding Sections 1.1–1.2. They combine the paper's framework with supplementary examples and earlier material on expected utility.

## 1. Expected utility and risk aversion

### 1.1 Utility under a known probability distribution

Consider a gamble with a random consumption payoff $C$. In the expected-utility framework, an individual evaluates the gamble by

```math
\mathbb{E}[u(C)],
```
where $u(c)$ is a Bernoulli utility function. Assume that $u$ is twice differentiable and satisfies

```math
u'(c)>0, \qquad u''(c)<0.
```
The first inequality means that more consumption is preferred; the second means that marginal utility decreases with consumption. By **Jensen's inequality**,

```math
\boxed{u(\mathbb{E}[C])\geq\mathbb{E}[u(C)]}.
```
For a nondegenerate gamble and strictly concave $u$, the inequality is strict. A risk-averse individual prefers receiving the gamble's expected payoff with certainty to taking the gamble itself.

### 1.2 Certainty equivalent and risk premium

The **certainty equivalent (CE)** is the certain amount of consumption that yields the same utility as the gamble:

```math
\boxed{u(CE)=\mathbb{E}[u(C)]},
\qquad
CE=u^{-1}\!\left(\mathbb{E}[u(C)]\right).
```
The **risk premium (RP)** is the difference between the expected payoff and the certainty equivalent:

```math
\boxed{RP=\mathbb{E}[C]-CE}.
```
It measures the amount of expected consumption an individual would be willing to give up to avoid the gamble.

For a two-outcome gamble $g\in\{w_1,w_2\}$, the chord connecting $R$ and $S$ gives $\mathbb{E}[u(g)]$ at the expected payoff $\mathbb{E}[g]$ (point $T$). The concave utility curve lies above the chord, so $u(\mathbb{E}[g])>\mathbb{E}[u(g)]$. The certainty equivalent is the point where the utility curve reaches $\mathbb{E}[u(g)]$.

![Concave utility curve and the chord connecting R and S, with T, the certainty equivalent and the expected payoff](01-risk-aversion-certainty-equivalent-bw.png)

*Figure 1. A clean redraw of the diagram for Jensen's inequality, the certainty equivalent, and the risk premium. Points R, T, and S are collinear on the same straight chord.*

**Numerical example.** Suppose $C=100$ with probability $0.9$ and $C=0$ with probability $0.1$, with $u(c)=\sqrt{c}$:

```math
\begin{aligned}
\mathbb{E}[u(C)] &= 0.9\sqrt{100}+0.1\sqrt{0}=9,\\
CE &= u^{-1}(9)=81,\\
\mathbb{E}[C] &=90,\\
RP &=90-81=\boxed{9}.
\end{aligned}
```
The individual is indifferent between this gamble and receiving $81$ for certain. The square-root function is used here as a simple learning example; its derivative at zero is not finite.

### 1.3 Arrow–Pratt measure of risk aversion

The **coefficient of absolute risk aversion** is

```math
\boxed{A(c)=-\frac{u''(c)}{u'(c)}}.
```
It measures the local curvature of utility relative to its slope. For a strictly concave, increasing utility function, $A(c)>0$. Unlike the risk premium, which depends on the distribution of a particular gamble, the Arrow–Pratt coefficient is a local property of preferences.

Up to this point, the probability distribution of the gamble has been treated as known. The paper introduces a second source of uncertainty: the distribution itself may be uncertain.

## 2. From risk to model uncertainty

### 2.1 Different models may assign different probabilities to the same outcomes

A probability **model** $P$ describes a distribution of outcomes. Suppose that an economy may follow either a Boom model $P_B$ or a Bust model $P_b$:

```math
\mathcal{P}=\{P_B,P_b\}.
```
For an illustrative gamble (not the numerical example in the paper), suppose consumption can be either $100$ or $0$:

| Consumption | $P_B$ (Boom) | $P_b$ (Bust) |
|:--|--:|--:|
| $100$ | $90\%$ | $10\%$ |
| $0$ | $10\%$ | $90\%$ |

Within either model, the probabilities are specified. What is uncertain is **which model actually governs the outcome**.

With $u(c)=\sqrt{c}$, the expected utilities conditional on the two models are

```math
\begin{aligned}
\mathbb{E}_{P_B}[u(C)] &= 0.9\sqrt{100}+0.1\sqrt{0}=9,\\
\mathbb{E}_{P_b}[u(C)] &= 0.1\sqrt{100}+0.9\sqrt{0}=1.
\end{aligned}
```
The same gamble therefore has two different model-specific expected utility values.

### 2.2 Probabilities within models and a prior over models

Suppose both models are considered equally likely:

```math
\mu(\{P_B\})=\mu(\{P_b\})=\frac12.
```
Here, $\mu$ is a **prior distribution over models**, not a probability distribution over consumption outcomes within a model.

For example,

- $P_B(C=100)=0.9$ is the probability of the high outcome **conditional on Boom**.
- $\mu(\{P_B\})=0.5$ is the prior probability assigned to the **Boom model itself**.

The two-stage uncertainty can be expressed as

```math
\underbrace{\text{Model selection}}_{\mu}
\;\longrightarrow\;
\underbrace{\text{Outcome conditional on the model}}_{P}.
```
**Risk aversion** concerns variation in outcomes within a given model. **Ambiguity aversion**, in this framework, concerns variation in the expected utilities associated with different models. A person can have a prior over models and still be ambiguity-averse; ambiguity aversion does not require an absence of subjective probabilities.

## 3. Smooth ambiguity preferences

### 3.1 The two-layer utility representation

The paper represents consumer $i$'s preferences as

```math
\boxed{
U_i(X_i)=\int_{\mathcal{P}}
\phi_i\!\left(\mathbb{E}_{P}[u_i(X_i^{P})]\right)\,\mu(dP)
}.
```
The expression contains two levels of utility evaluation:

1. **Within a model:** $u_i$ evaluates the utility of consumption, and $\mathbb{E}_P[u_i(X_i^P)]$ is expected utility under model $P$.
2. **Across models:** $\phi_i$ transforms each model-specific expected utility, and $\mu$ determines how these transformed values are aggregated.

| Notation | Meaning |
|:--|:--|
| $X_i^P$ | Consumer $i$'s consumption plan conditional on model $P$ |
| $u_i$ | Bernoulli utility; attitudes toward risk |
| $\mathbb{E}_P$ | Expectation under the probability model $P$ |
| $\phi_i$ | Second-layer utility transformation; attitudes toward ambiguity |
| $\mathcal{P}$ | Set of possible probability models |
| $\mu$ | Prior distribution over models |

An **increasing, concave** $\phi_i$ captures ambiguity aversion: the consumer dislikes dispersion in expected utility across models. If $\phi_i$ is affine, the preferences reduce to expected utility under the mixture distribution (up to an affine transformation).

### 3.2 From the integral to the finite-model formula

When $\mathcal{P}$ is finite, the integral can be written as a sum:

```math
U_i(X_i)=\sum_{P\in\mathcal{P}}
\mu(\{P\})\,\phi_i\!\left(\mathbb{E}_P[u_i(X_i^P)]\right).
```
For two equally likely models,

```math
\boxed{
U_i(X_i)=
\frac12\phi_i\!\left(\mathbb{E}_{P_B}[u_i(X_i^{P_B})]\right)
+\frac12\phi_i\!\left(\mathbb{E}_{P_b}[u_i(X_i^{P_b})]\right)
}.
```
The integral and sum describe the same structure; the integral notation also accommodates a continuous collection of models.

### 3.3 Two consumers: same prior beliefs, different ambiguity attitudes

Consider **Amy** and **Mia**, who share the same prior over Boom and Bust and the same risk utility $u(c)=\sqrt{c}$. Their evaluations under the two models are therefore $9$ and $1$, respectively. However, they differ in their attitude toward ambiguity.

**Amy is ambiguity-averse.** Let $\phi_{\mathrm{Amy}}(v)=\sqrt{v}$. Then

```math
U_{\mathrm{Amy}}
=\frac12\sqrt{9}+\frac12\sqrt{1}
=\boxed{2}.
```
**Mia is ambiguity-neutral.** Let $\phi_{\mathrm{Mia}}(v)=v$. Then

```math
U_{\mathrm{Mia}}
=\frac12(9)+\frac12(1)
=\boxed{5}.
```
For Mia, the model uncertainty is evaluated in the same way as a compound lottery under expected utility. The mixture distribution assigns probability

```math
\frac12(0.9)+\frac12(0.1)=0.5
```
to the high payoff. Amy, by contrast, applies a concave transformation to the model-specific expected utilities before averaging.

The numbers $2$ and $5$ are calculated under different representations and **should not be interpreted as directly comparable welfare levels**. The example illustrates the difference in preferences, not a ranking of the two consumers' welfare.

### 3.4 Concavity and the ambiguity-related Jensen gap

Let

```math
V_P=\mathbb{E}_P[u(C)]
```
be expected utility conditional on model $P$. For concave $\phi$, Jensen's inequality gives

```math
\phi\!\left(\mathbb{E}_{\mu}[V_P]\right)
\geq\mathbb{E}_{\mu}[\phi(V_P)].
```
The difference

```math
\boxed{
\phi\!\left(\mathbb{E}_{\mu}[V_P]\right)
-\mathbb{E}_{\mu}[\phi(V_P)]\geq0
}
```
is a useful way to express the effect of concavity across models. In Amy's example,

```math
\sqrt{\tfrac12(9+1)}
-\left(\tfrac12\sqrt9+\tfrac12\sqrt1\right)
=\sqrt5-2\approx\boxed{0.236}.
```
This is an **ambiguity-related Jensen gap**, not an explicit penalty subtracted in the paper's preference formula. The curvature of $u$ captures aversion to risk within models; the curvature of $\phi$ captures aversion to dispersion in expected utility across models.

## 4. Why use an integral? A continuous-model example

A two-model economy requires only a summation, but some problems involve a continuum of plausible models.

Consider a simple GDP-growth process:

```math
g=\theta+\varepsilon,
```
where the uncertain mean-growth parameter satisfies

```math
\theta\in[0.01,0.03],
```
and the shock $\varepsilon$ takes values $+0.01$ and $-0.01$, each with probability $0.5$.

Each possible value of $\theta$ defines a probability model $P_\theta$:

| Model | Possible growth outcomes | Expected growth |
|:--|:--|--:|
| $P_{0.01}$ | 0% or 2%, each with probability 50% | 1% |
| $P_{0.02}$ | 1% or 3%, each with probability 50% | 2% |
| $P_{0.03}$ | 2% or 4%, each with probability 50% | 3% |

Thus,

```math
\mathcal P=\{P_\theta:\theta\in[0.01,0.03]\},
\qquad
\mathbb E_{P_\theta}[g]=\theta.
```
A prior $\mu$ now distributes probability across values of $\theta$. With the same two-layer structure,

```math
U_i(X_i)=\int_{0.01}^{0.03}
\phi_i\!\left(\mathbb E_{P_\theta}[u_i(X_i^{P_\theta})]\right)
\,\mu(d\theta).
```
The distinction remains: $P_\theta$ specifies the distribution of growth **given** $\theta$, whereas $\mu$ describes uncertainty **about** $\theta$.

This example is added to understand the integral notation. It is not the paper's original numerical example, and it does not by itself establish that $\theta$ is identifiable from a single observed growth rate.

## 5. Returning to the paper's setting

### 5.1 Identifiable models

The paper initially assumes **identifiable models**: after the relevant state is observed, the model generating it can be determined. This is important because a contingent consumption allocation may depend on both the realized outcome and the model.

In the simplified €100/€0 example, observing €100 alone would not distinguish Boom from Bust: both models permit that payoff. Formal identifiability requires additional information in the observed state that reveals the model. The paper illustrates this using economic-regime identification based on multiple observable indicators, with an eventual public announcement.

Consequently, observing an economic outcome and identifying the probability model that produced it are different tasks.

### 5.2 The paper's Boom/Bust running example

The paper's own example uses aggregate endowment $\bar X\in\{4,10\}$, with

```math
P_B(\bar X=10)=\frac34,
\qquad
P_b(\bar X=10)=\frac14.
```
With logarithmic Bernoulli utility $u_i(c)=\log c$, the expected utility of the **aggregate endowment itself** under each model is

```math
\begin{aligned}
\mathbb E_{P_B}[\log\bar X]
&=\frac34\log 10+\frac14\log4\approx2.074,\\
\mathbb E_{P_b}[\log\bar X]
&=\frac14\log10+\frac34\log4\approx1.615.
\end{aligned}
```
These are model-specific expected utility calculations, not the welfare of consumers under a proposed allocation. The paper's central question is how **multiple consumers** should divide the aggregate endowment when their ambiguity attitudes differ.

## 6. Further reading

The third page of my handwritten notes records seminar keywords rather than completed study. The next topics are **efficient allocations and the generalized Borch rule** (§1.3), **HARA/CMRT and the representative consumer** (§2.1), **heterogeneous relative ambiguity aversion** (§2.2), and **the pricing kernel / stochastic discount factor** (§3).

The immediate conceptual link is that the paper moves from an individual's evaluation of model uncertainty to the problem of sharing it across consumers. The mathematical derivations and asset-pricing implications remain for a later reading.

---

**Reference:** Hara, C., Mukerji, S., Riedel, F., & Tallon, J.-M. (2026). *Sharing Model Uncertainty*. *American Economic Journal: Microeconomics*, 18(2), 313–347. https://doi.org/10.1257/mic.20240188
