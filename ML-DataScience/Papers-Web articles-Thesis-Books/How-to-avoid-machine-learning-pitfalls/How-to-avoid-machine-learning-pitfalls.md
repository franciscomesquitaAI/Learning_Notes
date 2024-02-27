---
share: true
path: ML-DataScience/Papers-Web articles-Thesis-Books/How-to-avoid-machine-learning-pitfalls
---
# Information

**Paper link:** https://arxiv.org/abs/2108.02497
**Author:** Michael A. Lones - https://scholar.google.com/citations?hl=pt-PT&user=MtauJIcAAAAJ&view_op=list_works&sortby=pubdate

---
# Purpose

It is a guide to avoid the most common mistakes when applying machine learning. It’s written by an academic, and focuses on lessons learned whilst doing ML research in academia.

---
# Content notes

## Before you start to build models

If you train your model using bad data, then you will most likely generate a bad model: a process known as **garbage in garbage out.**
![How to avoid machine learning pitfalls garbage|800](https://i.imgur.com/gn2CFTu.jpeg)

It’s important to do a literature review before you start work

---
## How to reliably build models

**Don’t allow test data to leak into the training process**
![How to avoid machine learning pitfalls train tes](https://i.imgur.com/nie4BLf.png)

No Free Lunch theorem shows that no ML approach is any better than any other when considering over every possible problem:
	More about this in [https://link.springer.com/chapter/10.1007/978-1-4471-0123-9_3](https://link.springer.com/chapter/10.1007/978-1-4471-0123-9_3)
![How to avoid machine learning pitfalls no free lunch](https://i.imgur.com/1hWxLLW.png)

When comparing models, Do optimize your model’s hyperparameters and Do evaluate a model multiple times to make sure you’re giving them all a fair chance, and Do correct for multiple comparisons when you publish your results.

Do not add unnecessary complexity. Don't assume deep learning will be the best approach.

Always keep up with recent developments (especially in DL):
![How to avoid machine learning pitfalls DL developments](https://i.imgur.com/ANumNiV.png)

You should take care when using either deep learning or explainable AI for models that are going to make high stakes or safety critical decisions

Do be careful where you optimise hyperparameters and select features:
- You should only use the training set to select the features which are used in both the training set and the test set.

- If you’re doing cross-validation, then it’s important to carry out feature selection and hyperparameter selection independently within each iteration, using just the training folds. The use of nested cross-validation (aka double cross-validation) uses an extra loop inside to give a more robust evaluation that involve processes such as hyperparameter optimisation or feature selection. Example

![How to avoid machine learning pitfalls hyperparameters|300](https://i.imgur.com/Ocelcx5.png)

- Representation of the ideia:

![How to avoid machine learning pitfalls idea representation|600](https://i.imgur.com/LI2JOCE.png)


**Do avoid learning spurious correlations:** Spurious correlations are features within data which are correlated with the target variable, but which have no semantic meaning. A classic example is the tank problem. Legend1 has it that the US military were looking to train an ML model that could recognize tanks. However, because the tank pictures used in training were taken during different weather conditions to the non-tank pictures, the model ended up discriminating based on features such as the number of blue pixels in the sky, rather than the presence of a tank.

---
## How to robustly evaluate models

First of all, always use a test set to measure the generality of an ML model. How well a model performs on the training set is almost meaningless, and a sufficiently complex model can entirely learn a training set yet capture no generalizable knowledge.

Test set should be representative of the wider population.

Don’t do data augmentation before splitting your data:
- One problem is that the model may overfit the characteristics of the augmented data, rather than the original samples, and you won’t be able to detect this if your test set also contains augmented data.
- A more critical problem occurs when data augmentation is applied to the entire data set before it is split into training and test sets. In this scenario, augmented versions of training samples may end up in the test set, which in the worst case can lead to a particularly nefarious form of data leakage in which the test samples are mostly variants of the training samples.

Do use a validation set! (Figure below is the perfect example for using validation test on the Deep models training like CNNs)

![How to avoid machine learning pitfalls validation set|600](https://i.imgur.com/swL34Yd.png)

Do evaluate a model multiple times:
- Many ML models are unstable. That is, if you train them multiple times, or if you make small changes to the training data, then their performance varies significantly. This means that a single evaluation of a model can be unreliable, and may either underestimate or overestimate the model’s true potential.
- Cross-validation is one of the best methods to do this.

Don’t ignore temporal dependencies in time series data:
- Most notably, time series data are subject to a particular kind of data leakage known as look ahead bias. More about this at https://bowtiedraptor.substack.com/p/look-ahead-bias-and-how-to-prevent. A good example of this bias:
![How to avoid machine learning pitfalls look ahead bias|600](https://i.imgur.com/KjmqsNn.png)

---
## How to compare models fairly

To really be sure of a fair comparison between two approaches, you should freshly implement all the models you’re comparing,
optimize each one to the same degree, carry out multiple evaluations, and then use statistical tests to determine whether the differences in performance are significant.

**Do use statistical tests when comparing models:**
- For example, McNemar’s test is a fairly common choice for comparing two classifiers, and works by comparing the classifiers’ output labels for each sample in the test set.

- The second category of tests are used to compare two models more generally, e.g. whether a decision tree or a neural network is a better fit for the data. These require multiple evaluations of each model, which you can get by using cross-validation or repeated resampling (or, if your training algorithm is stochastic, multiple repeats using the same data). The test then compares the two resulting distributions. Student’s T test is a common choice for this kind of comparison, but it’s only reliable when the distributions are normally distributed, which is often not the case. A safer bet is Mann-Whitney’s U test, since this does not assume that the distributions are normal.
	- [Gpt generated] A stochastic algorithm is a computational method that involves randomness or probability in its operation. It uses probabilistic models and statistical methods to solve problems that cannot be solved deterministically. 

- Things get a bit more complicated when you want to use statistical tests to compare more than two models, since doing multiple pairwise tests is a bit like using the test set multiple times — it can lead to overly-optimistic interpretations of significance.

- Basically, each time you carry out a comparison between two models using a statistical test, there’s a probability that it will discover significant differences where there aren’t any. This is represented by the confidence level of the test, usually set at 95%: meaning that 1 in 20 times it will give you a false positive. For a single comparison, this may be a level of uncertainty you can live with. However, it accumulates. That is, if you do 20 pairwise tests with a confidence level of 95%, one of them is likely to give you the wrong answer. This is known as the multiplicity effect, and is an example of a broader issue in data science known as data dredging or p-hacking.
	- To address this problem, you can apply a correction for multiple tests. The most common approach is the Bonferroni correction, a very simple method that lowers the significance threshold based on the number of tests that are being carried out. However, there are numerous other approaches, and there is also some debate about when and where these corrections should be applied; for an accessible overview, see https://www.sciencedirect.com/science/article/pii/S0002916523136963?via%3Dihub


**Do consider combinations of models:** Different ML models explore different trade-offs; by combining them, you can sometimes compensate for the weaknesses of one model by using the strengths of another model, and vice versa. Such composite models are known as ensembles.

---
## How to report your results

In order to effectively contribute to knowledge, you need to provide a complete picture of your work, covering both what worked and what didn’t. ML is often about trade-offs — it’s very rare that one model is better than another in every way that matters — and you should try to reflect this with a nuanced and considered approach to reporting results and conclusions.

Be transparent:
- For instance, if you used a script to implement all your experiments, then share the script when you publish the results. This means that other people can easily repeat your experiments, which adds confidence to your work.
- Knowing that you will be sharing your work also encourages you to be more careful, document your experiments well, and write clean code, which benefits you as much as anyone else.
- It’s also worth noting that issues surrounding reproducibility are gaining prominence in the ML community, so in the future you may not be able to publish work unless your workflow is adequately documented and shared.

Report performance in multiple ways:
- Use multiple datasets if possible
- Reports different metrics (because each one can present different perspective)

Don't generalize beyond data:
- We should just write what the experiment can show. Do not make statements not founded by the results of the work.
- One common issue is bias, or sampling error: that the data is not sufficiently representative of the real world.
- So, in short, don’t overplay your findings, and be aware of their limitations.

Be careful when reporting statistical significance:
- Statistical tests are not perfect. Some are conservative, and tend to under-estimate sig￾nificance; others are liberal, and tend to over-estimate significance. This means that a positive test doesn’t always indicate that something is significant, and a negative test doesn’t necessarily mean that something isn’t significant.
- If you have enough samples, you can always find significant differences, even when the actual difference in performance is minuscule. To give a better indication of whether something is important, you can measure effect size. There are a range of approaches used for this: Cohen’s d statistic is probably the most common, but more robust approaches, such as Kolmogorov-Smirnov, are preferable. You might also consider using Bayesian statistics; although there’s less guidance and tools support available, these theoretically have a lot going for them, and they avoid many of the pitfalls associated with traditional statistical tests.

Look at your model. Interpret how the model reach a decision. Look inside and use visualization and XAI techniques to extract knowledge. Metrics are important but a good model is much more than that!