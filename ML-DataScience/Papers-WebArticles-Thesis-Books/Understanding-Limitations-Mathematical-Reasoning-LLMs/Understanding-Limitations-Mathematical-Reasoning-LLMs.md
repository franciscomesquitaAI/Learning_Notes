---
share: true
path: ML-DataScience/Papers-WebArticles-Thesis-Books/Understanding-Limitations-Mathematical-Reasoning-LLMs
---

# Information

**Paper link:** [https://arxiv.org/abs/2410.05229]()
**First author:** Iman Mirzadeh - https://imirzadeh.me/ / https://scholar.google.com/citations?user=AjKbt44AAAAJ&hl=en

---

# Purpose
- Recent advancements in Large Language Models (LLMs) have sparked interest in their formal reasoning capabilities, particularly in mathematics. 
- To overcome the limitations of existing evaluations, authors introduce GSM-Symbolic, an improved benchmark created from symbolic templates that allow for the generation of a diverse set of questions.
- GSM-Symbolic enables more controllable evaluations, providing key insights and more reliable metrics for measuring the reasoning capabilities of models.
- Our findings reveal that LLMs exhibit noticeable variance when responding to different instantiations of the same question.
- Authors investigate the fragility of mathematical reasoning in these models and demonstrate that their performance significantly deteriorates as the number of clauses in a question increases.
- Authors hypothesize that this decline is due to the fact that current LLMs are not capable of genuine logical reasoning; instead, they attempt to replicate the reasoning steps observed in their training data.
- When we add a single clause that appears relevant to the question, we observe significant performance drops (up to 65%) across all state-of-the-art models, even though the added clause does not contribute to the reasoning chain needed to reach the final answer.

---
# Content notes

The question of whether current LLMs are genuinely capable of true logical reasoning is an important research focus. <ins>Literature suggests that the reasoning process in LLMs is probabilistic pattern-matching rather than formal reasoning.</ins> Although LLMs can match more abstract reasoning patterns, they fall short of true logical reasoning. Small changes in input tokens can drastically alter model outputs, indicating a strong token bias and suggesting that these models are highly sensitive and fragile.

Mathematical reasoning is a crucial cognitive skill that supports problem-solving in numerous scientific and practical applications. Consequently, <ins>the ability of large language models (LLMs) to effectively perform mathematical reasoning tasks is key to advancing artificial intelligence and its real- world applications.</ins>

The GSM8K (Grade School Math 8K) dataset \[1] is a popular benchmark for measure mathematical reasoning capabilities of LLMs. The authors present the following limitation to the data:
- It provides only a single metric on a fixed set of questions.
- The popularity and prevalence of GSM8K can increase the risk of inadvertent data contamination.
- The static nature of GSM8K does not allow for controllable experiments to understand model limitations, such as behavior under varied conditions or changes in question aspects and difficulty levels.

To solve those limitations, <ins>authors presented a more versatile and adaptive evaluation framework called GSM-Symbolic</ins>.


**Authors contributions:**

1. Introduction of GSM-Symbolic, an enhanced benchmark capable of generate different variations of GSM8K questions using symbolic templates. Look at the figure below to understand this better. Authors large-scale study on 25 state-of-the-art open and closed models provides significant insights into LLMs’ behavior in mathematical reasoning tasks.
2. Authors hint a possible data contamination on GSM8K, showing that performance of all models drops on GSM-Symbolic.
3. LLMs can deal better with names changes of variables but are very sensitive to changes in numerical values. They also show that LLMs reasoning capabilities struggle with increased complexity.
4. Authors questioned the LLM reasoning capabilites introducing the GSM-NoOp dataset. Performance dropped up to 65% on all SOTA models. This was probably because LLM reasoning is not formal in the common sense term and is mostly based on pattern matching.

Authors conclude with:
	Overall, our work provides a comprehensive understanding of the limitations of LLMs in mathematical reasoning. Our results emphasize the need for more reliable evaluation methodologies and further research into the reasoning capabilities of large language models.



![Understanding Limitations Mathematical Reasoning LLMs SymbolicTemplate](https://i.imgur.com/0LlN07s.png)

---

There is a considerable body of work suggesting that the reasoning process in LLMs is not formal, even though it appears that these models understand symbols and can work with them to some limited degree. Instead, LLMs likely perform a form of probabilistic pattern-matching and searching to find closest seen data during training without proper understanding of concepts.

While this process goes beyond naive memorization of words and the models are capable of searching and matching more abstract reasoning steps, <ins>it still falls short of true formal reasoning</ins>.

**Authors findings support the hypothesis that current LLMs are not capable of performing formal mathematical reasoning and pave the way for further research on this important topic.**

---
## GSM-Symbolic

The GSM8K dataset includes over 8000 grade school math questions and answers. The questions are relatively simple, requiring knowledge of only the four main arithmetic operations. However, GSM8K have a high risk of data contamination due to its popularity. This can lead to "wrong" performance variation and misleading results and conclusions.

Authors denote the following LLM limitation:
	LLMs struggle even when given multiple shots of the same question, indicating deeper challenges in problem-solving that cannot be resolved with few-shot prompting or fine-tuning on unseen distractions or variations of the same or different difficulty levels.

There some GSM8K dataset variations:
- GSM Plus \[2]: introduces variants of GSM8K questions but lacks symbolic templates and has a fixed size and difficulty.
- GSM1K \[3]: mirrors the style and complexity of GSM8K to identify systematic overfitting in existing models, but has a fixed number of examples, and is not publicly available for researchers.

<ins>Authors claim that the design of GSM-Symbolic makes it possible to generate numerous instances and allows finer control over questions difficulty. They claim that the approach contributes to the creation of a more robust and reliable evaluation framework that underscores the importance of generating multiple instances to assess LLMs’ mathematical capabilities. Also, their robustness to diverse problem difficulties and augmentations.</ins>

---
## Experimental setup

- More than 20 open models of different sizes (from 2B to 27B). They also included SOTA closed models like GPT-4o-mini, GPT-4o, o1-mini, and o1-preview.
- Authors conducted nearly 500 evaluations across various setups using a manageable dataset of 5,000 examples, with 8-shot Chain-of-Thought prompting as the default evaluation method, noting that performance was largely unaffected by the number of shots. 

---

## Results

By studying the distribution of performance on GSM-Symbolic and GSM8K, authors demonstrate notable performance variation. More importantly, they observe that the performance of models drops on GSM-Symbolic. That can be seen in the images below:

![Understanding Limitations Mathematical Reasoning LLMs   performance variations on both sets](https://i.imgur.com/JQMqOyt.png)

![Understanding Limitations Mathematical Reasoning LLMs   performance drop](https://i.imgur.com/2aw66mR.png)


On interesting result authors show is the performance variations between datasets when changing variables names vs changing values. When changing variables name the performance distribution on GSM8K is very close to the GSM-Symbolic but when changing values, performance drops significantly.

As no formal learning is involved on the way LLMs work, it can lead to high variance across different instances of the same question.

There is one amazing image that authors show that makes it possible to show **how fragile LLM knowledge is**:

![Understanding Limitations Mathematical Reasoning LLMs   fragile LLM knowledge](https://i.imgur.com/Fldw5fV.png)


Authors go even further and try to understand the impact that question difficulty have on LLM performance. To make this different level of difficult were used (more difficult = more clauses on the problem). The results are presented below, where red line is harder questions, yellow medium difficulty, blue the normal difficult of GSM8K and green the easy difficulty.

![Understanding Limitations Mathematical Reasoning LLMs   difficulty analysis](https://i.imgur.com/UjJWL7G.png)

<ins>Results here are "normal", as the difficulty increases, the performance decreases and the variance increases.</ins> Authors claim that this is in line with the hypothesis that models are not performing formal reasoning, as the number of required reasoning steps increases linearly, but the rate of drop seems to be faster. Moreover, considering the pattern-matching hypothesis, the increase in variance suggests that searching and pattern-matching become significantly harder for models as the difficulty increases.

LLMs are not capable of ignore irrelevant information, this also demonstrate that no formal reasoning are being done to get the result. Look at the below image which demonstrate the incapability of ignore non-relevant information.

![Understanding Limitations Mathematical Reasoning LLMs   cant ignore irrelevant info](https://i.imgur.com/uhM6Aw1.png)


Authors created a whole set with examples like the one showed in the image above. They called it GSM-NoOp (No Operation). This dataset has the math questions but with irrelevant information added, that should not interfere with the mathematical reasoning.

Results on the NoOp dataset have clearly shown the inability of LLMS to reason mathematically:
	NoOp-Symb uses 8 shots of the same GSM-Symbolic question, while NoOp-NoOp uses 8 random GSM-NoOp questions, showing consistent performance across models despite varying setups.

![Understanding Limitations Mathematical Reasoning LLMs   NoOp results](https://i.imgur.com/p603MzI.png)

---
## Conclusion

This work investigates the limitations of LLMs in mathematical reasoning, showing significant performance variability across different versions of the same question on GSM8K and GSM-Symbolic. 

It highlights that while LLMs are somewhat robust to changes in proper names, they are highly sensitive to numerical variations and irrelevant information. 

<ins>The introduction of GSM-NoOp exposes a critical flaw:</ins> adding inconsequential details can cause performance drops of up to 65%, even with few-shot learning. 

<ins>These findings suggest that LLMs rely more on pattern matching than genuine logical reasoning</ins>, struggling even with basic grade-school math, and underscore the need for further research to develop models capable of robust formal reasoning.


---
# References

\[1]: [https://paperswithcode.com/dataset/gsm8k](https://paperswithcode.com/dataset/gsm8k)
\[2]: [https://github.com/qtli/GSM-Plus](https://github.com/qtli/GSM-Plus)
\[3]: [https://arxiv.org/html/2405.00332v1](https://arxiv.org/html/2405.00332v1)



