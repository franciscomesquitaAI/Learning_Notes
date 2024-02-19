---
share: true
path: 'Online Courses/MITx: Probability - The Science of Uncertainty and Data'
attachment:
  send: true
  folder: 'Online Courses/MITx: Probability - The Science of Uncertainty and Data/assets'
---
_Part of the MITx MicroMasters program in Statistics and Data Science._

The world is full of uncertainty: accidents, storms, unruly financial markets, noisy communications. The world is also full of data. Probabilistic modeling and the related field of statistical inference are the keys to analyzing data and making scientifically sound predictions.

<ins>Most phenomena of interest involve significant randomness. The only reason we collect and manipulate data is because we want to fight this randomness as much as we can.</ins>

---
# Content overview

**Units 1-3:** Basic probability
**Unit 4**: Discrete random variables
**Unit 5**: Continuous random variables
**Unit 6**: Further topics
**Unit 7**: Bayesian inference
**Unit 8**: Limit theorems and statistics
**Unit 9**: Random arrival processes
**Unit 10**: Markov chains

---
# Course objectives

At a conceptual level:
- Master the basic concepts associated with probability models .
- Be able to translate models described in words to mathematical ones.
- Understand the main concepts and assumptions underlying Bayesian and classical inference .
- Obtain some familiarity with the range of applications of inference methods .

At a more technical level:
- Become familiar with basic and common probability distributions .
- Learn how to use conditioning to simplify the analysis of complicated models.
- Have facility manipulating probability mass functions , densities , and expectations .
- Develop a solid understanding of the concept of conditional expectation and its role in inference.
- Understand the power of laws of large numbers and be able to use them when appropriate.
- Become familiar with the basic inference methodologies (for both estimation and hypothesis testing ) and be able to apply them.
- Acquire a good understanding of two basic stochastic processes (Bernoulli and Poisson) and their use in modeling.
- Learn how to formulate simple dynamical models as Markov chains and analyze them.

---
# Standard notation

- **Symbols are case-sensitive:** **a** and **A** are different – make sure to use the correct case as specified in the problem
- **Parentheses:** make sure that your parentheses are properly balanced – each open parenthesis should have a matching close parenthesis!
- **Elementary arithmetic operations:** use the symbols **+** , **-** , ***** , **/** for addition, subtraction, multiplication, and division, respectively
- **For multiplication**, use * explicitly:
	- in the example above, enter b\*c ; do NOT enter bc
	- enter **2\*n\*(n+1)** ; do NOT enter **2n(n+1)**
	- although the "pretty" display underneath your answer looks correct if you do not include * s, your answer will be marked incorrect!
- **Exponents:** use the symbol ^ to denote exponentiation
	- 2 exponent n should be entered as **2^n**
	- x exponent n+1 should be entered as x^(n+1)
- **Square root:** use the string of letters sqrt , followed by enclosing what is under the square root in parentheses
	- should be entered as sqrt(-1)
- **Mathematical constants**: use the symbol **e** for the base of the natural logarithm; use the string of letters **pi** for pi symbol
	- ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20mathematical%20constants.png) - this should be written as **e^(i*(pi))+1**
- **Order of operations**: 1) parentheses, 2) exponents and roots, 3) multiplication and division, 4) addition and subtraction
	- ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20order%20of%20operations.png) - this should be written as **(1/sqrt(2*(pi)))*e^(-(x^2)/2)**
	- a/b*c is interpreted as ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20order%20of%20operations%202.png)
- a/(b\*c) is for  ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20order%20of%20operations%203.png)
- **Natural logarithm:** although in lectures and solved problems we will sometimes use the notation "log" (instead of "ln"), you should use the string of letters **ln** , followed by the argument enclosed in parentheses
	- ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20natural%20logarithm.png) - should be entered as **ln(2*x)**
- **Trigonometric functions:** use the usual 3-letter symbols to denote the standard trigonometric function (e.g: sin(x))
- **Greek letters:** use the Latin-character name to denote each Greek letter
	- ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20greek%20letters.png) - should be entered as **lambda*e^(-lambda*t)**
	- ![](assets/Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data%20-%20greek%20letters%202.png) - should be entered as **mu*alpha*theta**
- **Factorials, permutations, combinations:** you will not need enter these for any symbolic answers; do **NOT** use **!** in your answers as it will not be evaluated correctly!
---
# Notes

Some interesting discussions found while taken this course can be seen here: [(Discussion) Probability - The Science of Uncertainty and Data]((Discussion)%20Probability%20-%20The%20Science%20of%20Uncertainty%20and%20Data.md)

<ins>It's important to clarify that I'll only be posting here notes that I've taken from content that complements what is presented in the course or some very important information to remember later. If you want to consult the content of the course, I strongly advise you to check out the following link: https://www.edx.org/learn/probability/massachusetts-institute-of-technology-probability-the-science-of-uncertainty-and-data</ins>


## Lecture 1 - Probability models and axioms

On book:
- Sets: Section 1.1
- Probabilistic models: Section 1.2

---
## Lecture 2 - Conditioning and independence

**Finding The Sum of an Infinite Geometric Series**

- source at: https://www.youtube.com/watch?v=jxRqRLMliPc

let's say that we want to find the sum of the following infinite geometric series: $$8+4+2+1+1/2+1/4+...$$
There is a formula for this: $Sum = \frac{a1}{1-r}$ where $r$ is the common ratio and $|r| < 1$

But... <ins>What is the common ratio?</ins>

- To find the common ratio take the second term and divide by the first. To confirm it, take the third and divide by second.

So, the common ratio is $\frac{1}{2}$

As the common ration is less than 1, then we can use the formula $Sum = \frac{a1}{1-r}$

Making the calculations:
- $Sum = \frac{8}{1-\frac{1}{2}}$
- Sum = 16

Good and simple example for understanding the law of total probability: https://youtu.be/U3_783xznQI?t=222

---
## Lecture 4 - Counting

<ins>Why is 0! = 1 and why it is a convection?</ins>

This video helped me in understanding this: https://www.youtube.com/watch?v=X32dce7_D48



