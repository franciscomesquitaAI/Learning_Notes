---
share: true
path: 'ML & DataScience/Mitigating LLM Hallucinations with a metric-first evaluation'
attachment:
  send: true
  folder: 'ML & DataScience/Mitigating LLM Hallucinations with a metric-first evaluation/assets'
---

# Information

Workshop link: https://www.youtube.com/watch?v=u1pNrsR1txA
Apresentation slides: https://docs.google.com/presentation/d/1u_bTwp_WHLGop7ubOIKEO-tAtkdTKkCGJq3ElpaQxzA/edit#slide=id.g291a5494064_0_1261
Paper of the proposed method: [Paper - Galileo ChainPoll: A High Efficacy Method for LLM Hallucination Detection - Galileo (rungalileo.io)](https://www.rungalileo.io/blog/chainpoll)
Date: 26/10/2023

---
# Speakers
- Vikram Chatterji: https://www.linkedin.com/in/vikram-chatterji/ (Galileo CEO (https://www.rungalileo.io))
- Atindriyo Sanyal: https://www.linkedin.com/in/atinsanyal/  (Galileo CTO)
---
# Content

## What well be covered here
- The need of LLM experimentation and evaluation frameworks
- Evaluations methods
- Emerging hallucination detection methods
- Demo


When we work with LLMs we have a lot of possible inputs and outputs and complexity.

<ins>Input experimentation is highly iterative and manual.</ins>
![600](assets/Mitigating%20LLM%20Hallucinations%20with%20a%20metric-first%20evaluation%20Workshop%20-%20LLM%20complexities.png)

From a framework perspective there are essentialy three modules on LLM applications:
1. Prompt
2. Fine Tune
3. Monitor

<ins>Experimentation is meaningless without metrics!</ins>

There is essentially three types of metrics:
1. Output 'quality' metrics
	1. Tone of voice
	2. Toxicity
	3. Bias
	4. Hatefulness
	5. Sexism
	6. ... more
2. Custom metrics
	1. AI Policy adherence
	2. Compliance adherence
	3. Business metrics
	4. ... more
3. Output Hallucination metrics: <ins>Bottleneck Today!</ins> (How can we consistently and accurately measure the "correctness" of the LLM output?)

## LLM Output Hallucination metrics

In resume, Hallucination happens when the LLM response seems plausible but there are some incorrect, non-existent or problematic information.

There are 3 techniques to quantify LLM hallucinations:

### N-Gram matching 

<ins>Where there is ground truth information</ins>

For this can be used metrics like BLEU score METEOR.
> [!ai]+ AI
>
> BLEU (Bilingual Evaluation Understudy) is a metric used to measure the quality of machine-generated translations. It compares the machine-generated translation with one or more reference translations and assigns a score based on the similarity between them. BLEU calculates the precision of n-grams (sequences of n words) in the machine-generated translation compared to the reference translations. A higher BLEU score indicates a better quality translation.
> METEOR (Metric for Evaluation of Translation with Explicit ORdering) is another metric used to evaluate machine translation. It also compares the machine-generated translation with reference translations, but it takes into account not only word matches but also synonymy and paraphrasing. METEOR calculates a score based on various linguistic features like precision, recall, and alignment of words in the machine-generated translation compared to the reference translations. A higher METEOR score indicates a better quality translation.

Usually these metrics are used on:
	Translation quality estimation
	Summarization
	Image captioning

This has a lot of limitations:
	No semantic understanding
	Reliance on precise matching
	Novelty and style not considered
	Too granular

### Ask GPT

Metrics used:
- G-Eval: Ask an LLM to rate a response between 1 and 5
- SelfCheck or ChatProtect: Checking consistency between LLM response and a large number of other responses

Usually these metrics can be used on:
	Translation
	Summarization
	Q&A

Limitations:
	Black boxed techniques
	Prohibitively expensive (too much APIs requests!)
	Lack of explainability


### Probability Based

Metrics that use Probability based metrics...

Metrics used:
- GPT-Score
- Entropy: Measure $pLog(p)$ across normalize token probabilities
- Token confidence


Applications:
	All uses cases where models output token by token

Several limitations:
	Too granular
	Not always available
	Can only be model confusion and not an actual hallucination

---

<ins>We need a "new category" of LLM evaluation metrics that are:</ins>
1. More accurate
2. Scalable
3. Cost effective
4. Low latency

# ChainPoll

<ins>A new method for evaluating LLMs</ins>

There are essentially two steps on this method:

1. <ins>Chaining</ins>
Using a specialized prompt, the LLM is asked to judge if the original completion contained Hallucinations, justifying with a chain-of-thought explanation.

2. <ins>Polling or Ensembling</ins>
The above step is ensemble, i.e: the chaining step run multiple time, usually 5, in a batch inference fashion.

> [!ai]+ AI
>
> Batch inference refers to a process in which an artificial intelligence model makes predictions or performs computations on a large set of data at once, rather than processing each piece of data individually. It allows for the efficient processing of a large volume of information in a single operation.
> During batch inference, the model takes a batch or group of inputs and processes them together, analyzing patterns and making predictions based on the learned parameters. This approach is particularly useful when dealing with datasets that are too large to be processed individually or when there is a need for faster computation.
> By performing computations in batches, the model can take advantage of parallel processing or distributed computing resources, resulting in significant time savings. Additionally, batch inference can be more cost-effective compared to running individual predictions on each data point.
> Overall, batch inference simplifies and optimizes the process of making predictions or performing computations on large datasets by processing them collectively rather than one by one.

The algorithm:
![900](assets/Mitigating%20LLM%20Hallucinations%20with%20a%20metric-first%20evaluation%20-%20ChainPoll%20algorithm%20complete.png)

ChainPoll results:
![800](assets/Mitigating%20LLM%20Hallucinations%20with%20a%20metric-first%20evaluation%20-%20results%20obtained%20with%20chainpoll.png)

ChainPoll has several advantages:
- More accurate
- Provides human-understandable feedback
- Low latency
- Reduced cost (very few API calls)

Derived metrics:
![800](assets/Mitigating%20LLM%20Hallucinations%20with%20a%20metric-first%20evaluation%20-%20derived%20metrics.png)

### Correctness in action

<ins>Input</ins>: When and where was Abraham Lincoln born?

<ins>LLM Response</ins>: Abraham Lincoln was born on February 12, 1809 near Laron County, Kentucky.

<ins>Correctness</ins>: <mark class="hltr-red">0.24 (low)</mark>

<ins>Explanation</ins>: Abraham Lincoln was born in LaRue County, not LaRon County.


### Context adherence in action
![900](assets/Mitigating%20LLM%20Hallucinations%20with%20a%20metric-first%20evaluation%20-%20context%20adherence%20in%20action.png)


### Results on both Closed and Open domain datasets (both correctness and context adherence)

![800](assets/Mitigating%20LLM%20Hallucinations%20with%20a%20metric-first%20evaluation%20-%20result%20closed%20and%20open%20data.png)

---

# Practical Demonstration

## 1. Prompt: Building a Q&A app for kids

Resources used:
- Vector store with wikipedia articles
- Dataset of prompts
- LLMs

## 2. Fine tune: Generating headlines for news articles

Resources used:
- Corpus of news articles
- LLMs

<ins>These practical demonstrations where done on Galileo and for clear reasons not shared. The best i to see workshop to understand what they have done here!</ins>
