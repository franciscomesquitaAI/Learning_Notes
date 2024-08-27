A new research called "*KAN: Kolmogorov–Arnold Network*" has created excitement in the machine learning (ML) community. It presents a new perspective on Neural Networks, being a possible alternative to Multi-Layer Perceptrons (MLP), a cornerstone of current ML \[1].

# Information

**Original paper (link):** [https://arxiv.org/abs/2404.19756](https://arxiv.org/abs/2404.19756) 

**Published date:** April 30th, 2024

**Authors:** [Ziming Liu](https://arxiv.org/search/cs?searchtype=author&query=Liu,+Z), [Yixuan Wang](https://arxiv.org/search/cs?searchtype=author&query=Wang,+Y), [Sachin Vaidya](https://arxiv.org/search/cs?searchtype=author&query=Vaidya,+S), [Fabian Ruehle](https://arxiv.org/search/cs?searchtype=author&query=Ruehle,+F), [James Halverson](https://arxiv.org/search/cs?searchtype=author&query=Halverson,+J), [Marin Soljačić](https://arxiv.org/search/cs?searchtype=author&query=Solja%C4%8Di%C4%87,+M), [Thomas Y. Hou](https://arxiv.org/search/cs?searchtype=author&query=Hou,+T+Y), [Max Tegmark](https://arxiv.org/search/cs?searchtype=author&query=Tegmark,+M)

---
# Scientific Breakthrough

Inspired by Kolmogorov-Arnold representation theorem \[2], KANs diverge from traditional MLPs by replacing fixed activation function with learnable functions, eliminating the need for linear weight matrices.

![KolmogorovArnold Networks (KAN) 1](https://i.imgur.com/Cb9Eo5x.png)

---
# MLP vs KAN

MLPs often struggle with high-dimensional data reducing the efficiency and accuracy of the ML system. This is known as the curse of dimensionality \[3]:

![KolmogorovArnold Networks (KAN) 3](https://i.imgur.com/cUSLA7t.png)
As the dimensionality increases, a larger percentage of the training data resides in the corners of the feature space \[4].

The Kolmogorov-Arnold theorem, however, provides a theoretical foundation for building networks (like KANs) that can overcome this challenge. Below is a full comparison between KAN e MLP:

![KolmogorovArnold Networks (KAN) 4](https://i.imgur.com/AzqBFor.png)

A more detailed and depth explanation can be seen here: [https://www.youtube.com/watch?v=7zpz_AlFW2w](https://www.youtube.com/watch?v=7zpz_AlFW2w)

**How can KAN help to avoid the curse of dimensionality?**

This theorem allows for the decomposition of complex high-dimensional functions into compositions of simpler one-dimensional functions. By focusing on optimizing these one-dimensional functions rather than the entire multivariate space, KANs reduce the complexity and the number of parameters needed to achieve accurate modeling. Furthermore, Because of working with simpler one-dimensional functions, KANs can be simple and interpretable models.

**KANs are not that different from MLPs:** KAN benefits the structure of MLP on the outside, and splines on the inside.
	As a result, KANs can not only learn features (thanks to their external similarity to MLPs), but can also optimize these learned features to great accuracy (thanks to their internal similarity to splines).

---
# What exactly are Kolmogorov–Arnold Networks (KAN)?

It is a type of neural network architecture inspired by the Kolmogorov-Arnold representation theorem. **Unlike traditional neural networks that use fixed activation functions, KANs employ learnable activation functions on the edges of the network**. This allows every weight parameter in a KAN to be replaced by a univariate function, typically parameterized as a **spline**, making them highly flexible and capable of modeling complex functions with potentially fewer parameters and enhanced interpretability.

![KolmogorovArnold Networks (KAN) 5](https://i.imgur.com/pw5BX18.png)

## Architecture

The architecture of Kolmogorov-Arnold Networks (KANs) revolves around a novel concept where traditional weight parameters are replaced by univariate function parameters on the edges of the network. Each node in a KAN sums up these function outputs without applying any nonlinear transformations, in contrast with MLPs that include linear transformations followed by nonlinear activation functions.

![KolmogorovArnold Networks (KAN) 6 1](https://i.imgur.com/iOl2Jog.png)

### B-Spline: The core of KAN

Splines are the backbone of KAN’s learning mechanism. They replace the traditional weight parameters typically found in neural networks. The flexibility of splines allows them to adaptively model complex relationships in the data by adjusting their shape to minimize approximation error, therefore, enhancing the network’s capability to learn subtle patterns from high-dimensional datasets.

![KolmogorovArnold Networks (KAN) 7](https://i.imgur.com/tObvjyl.png)

While KAN is based on the Kolmogorov-Arnold representation theorem, it is just as inspired by MLPs, _"leveraging their respective strengths and avoiding their respective weaknesses_". KAN benefits the structure of MLP on the outside, and splines on the inside.

**As a result, KANs can not only learn features (thanks to their external similarity to MLPs), but can also optimize these learned features to great accuracy (thanks to their internal similarity to splines).**

---
# Network overview

An overview of the network symbolification:

![Kolmogorov–Arnold Networks (KAN)](https://i.imgur.com/Yd3QkCV.png)

I will not get into too much technical detail because some of the steps are very hard to understand and for that, the original papel should be read!

Lets just talk two interesting concepts that we encounter when we talk about KANs:

- **Symbolification:** KAN is constructed by approximating functions using compositions of simpler, often interpretable functions. This results in their unique ability to hand over interpretable mathematical formulas, such as shown in the figure above.
- **Pruning:** This is about optimizing the network architecture by removing less important nodes or connections after the network has been trained. This process helps in reducing the complexity and size. Pruning focuses on identifying and eliminating those parts of the network that contribute minimally to the output. This makes the network lighter and potentially more interpretable. For those of you familiarised with the concept of tree pruning, this is exactly the same. The two figures below demonstrates this very well:

Tree pruning \[5]:

![Kolmogorov–Arnold Networks (KAN) 1](https://i.imgur.com/eDm7FcC.png)

Neural Networks / KANs prunning \[6]:

![Kolmogorov–Arnold Networks (KAN) 2](https://i.imgur.com/bPAAYkW.png)

---
# Are KANs a new concept?

No. The new paper highlights the following:
	Most work has stuck with the original depth-2 width-(2n + 1) representation, and did not have the chance to leverage more modern techniques (e.g., back propagation) to train the networks.

The novelty of the paper is to adapt this idea and apply it to the current landscape of ML. Using arbitrary network architecture (depth, width) and employing techniques such as backpropagation and pruning, KAN is closer to practical use cases than previous studies.

---
# Is the hype worth it? is this a major breakthrough?

Well, it depends on the perspective. It is a good approach that can help reach the "end goal" in AI but i do not see it as a major step or breakthrough in the ML field. Altough KANs are written with scientific application on mind, people are using it to mix various ML cocktails, including Multihead Attention.

The paper focuses mainly on the AI + Science applications of Kolmogorov-Arnold Networks due to their ability to model and discover complex scientific laws and patterns effectively. KANs are particularly suited for tasks that require the understanding and interpreting of underlying physical principles, as their structure allows for the decomposition of functions into symbolic mathematical expressions. This makes them ideal for scientific research where discovering such relationships is crucial, unlike in large language models (LLMs) where the primary goal often revolves around processing a mammoth corpus of data for natural language understanding and generation.

---
# References
\[1]: [https://towardsdatascience.com/kolmogorov-arnold-networks-kan-e317b1b4d075](https://towardsdatascience.com/kolmogorov-arnold-networks-kan-e317b1b4d075)

\[2]: [[2007.15884] The Kolmogorov-Arnold representation theorem revisited (arxiv.org)](https://arxiv.org/abs/2007.15884)

\[3]: [highdim.dvi (class-specific.com)](https://www.class-specific.com/csf/papers/hidim.pdf)

\[4]: [The Curse of Dimensionality in Classification (visiondummy.com)](https://www.visiondummy.com/2014/04/curse-dimensionality-affect-classification/)

\[5]: [Basic Principles of Pruning Woody Plants - UGA Cooperative Extension](https://extension.uga.edu/publications/detail.html?number=B949&title=basic-principles-of-pruning-woody-plants)

\[6]: [Algorithms - Free Full-Text - Activation-Based Pruning of Neural Networks (mdpi.com)](https://www.mdpi.com/1999-4893/17/1/48)
