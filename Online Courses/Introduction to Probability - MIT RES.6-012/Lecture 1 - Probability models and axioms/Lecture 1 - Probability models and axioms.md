---
share: true
path: 'Online Courses/Introduction to Probability - MIT RES.6-012/Lecture 1 - Probability models and axioms'
attachment:
  send: true
  folder: 'Online Courses/Introduction to Probability - MIT RES.6-012/Lecture 1 - Probability models and axioms/assets'
---
**Drawing file:** [Drawing 2023-09-20 15.27.10.excalidraw](Drawing%202023-09-20%2015.27.10.excalidraw.md)

**Probabilistic model:** quantitive description of a situation, a phenomenon, or an experiment whose outcome is uncertain.

**Sample space:** It defines the possible outcomes and describe beliefs about likelihood of outcomes.
> [!ai]+ AI
>
> Sample space refers to the set of all possible outcomes or results of a random experiment.

![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012%201.png)

- **Mutually exclusive:** At the end of experiment there can only be one of the outcomes.
- **Collectively exhaustive:**  At the end of the experiment, the outcome will be one of the possible outcomes presented in the set.
- **At the "right" granularity:** Depends on what type of question do we want to answer. We should not include 'irrelevant' information in sample space.

## Discrete/finite example

Taking as an example two rolls of a tetrahedral dice.
> [!ai]+ AI
>
> A tetrahedral dice is a four-sided geometric shape used in games and probability experiments.

These are two examples on the ways that we can present outcome possibilities:

![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-1%201.png)

The previous example involves a sample space that was discrete and finite. But, sample spaces can also be infinite and continuous.

If we consider the sample space a real point between x and y ( $0≤x,y≤1$ ). With infinite precision, this example is infinite and continuous...

## Probability axioms

In a infinite and continuous sample space, the probability of an outcome to occur with infinite precision should be 0!. To solve this, usually subsets are used:

![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-2.png)

**Event:** a subset of the sample space.

**Axioms:** rules that all probabilistic models should satisfy. The are:
- Nonnegativity: $P(A)≥0$
- Normalization: $P(Ω) = 1$
- (Finite) additivity: If $A∩B = Ø$, then $P(A∪B) = P(A) + P(B)$

![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012.-111.png)

### Some simple consequences of the axioms

- if $A \subset B$, then $P(A) \leq P(B)$
![500](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-dca.png)

- $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
![500](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-sdaxa.png)

- $P(A \cup B) < P(A) + P(B)$
This can be also called **union bound**

These three above axioms are explained in the course as following:
![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-axiomsconsequencevideo.png)

<ins>Note: In set theory, the complement of a set A, often denoted by **$A^C$ or $A'$**, is the set of elements not in A.</ins>

- $P(A \cup B \cup C) = P(A) + P(A^c \cap B) + P(A^c \cap B^c \cap C)$
![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-3subsetjoin.png)


## Discrete Uniform Law

**Probability calculation: discrete / finite example**:
![](assets/Introduction%20to%20Probability%20-%20MIT%20RES.6-012-examplediscreteuniformlaw.png)

The discrete uniform law assumes that all elements (n) have equal probability of happen.
	In the above example the combination (2,3) or (4,1) has the exact same probability of happen (1/16). And this happens with every event.

- Assume $\Omega$ consists of $n$ equally likely elements
- Assume $A$ consists of $k$ elements

$$P(A) = k \cdot \frac1n$$

> [!ai]+ AI
>
> The discrete uniform law, also known as the discrete uniform distribution, is a probability distribution that assigns equal probability to each possible outcome in a finite set. It is used when all outcomes are equally likely to occur and there is no bias towards any particular outcome. The discrete uniform law is commonly represented using a probability mass function (PMF) that assigns a probability of 1 divided by the number of possible outcomes to each outcome. This distribution is often used in situations such as rolling a fair die or flipping a fair coin, where all outcomes have the same likelihood of occurring.

