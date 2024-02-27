---
share: true
path: ML-DataScience/Techniques-Frameworks-Methods-Tools/Extreme-Machine-Learning-(ELM)
---

It is a feedforward neural network that uses Moore Penrose generalized inverse to set its weights. ELMs are able to produce acceptable predictive performance and it learn thousands of times more faster than other algorithm and their computational cost is much lower than networks trained by the back propagation algorithm.

---

**Sources:**
- AI content generated with gpt-3.5-turbo-0613 model
- https://medium.com/analytics-vidhya/a-gentle-introduction-to-extreme-learning-machines-elm-91bb793effa8
- https://towardsdatascience.com/introduction-to-extreme-learning-machines-c020020ff82b
- https://github.com/burnpiro/elm-pure
- https://link.springer.com/article/10.1007/s11042-021-11007-7
- https://www.extreme-learning-machines.org

---

> [!ai]+ AI
>
> Extreme Learning Machine (ELM) is a machine learning algorithm that belongs to the family of artificial neural networks. It was introduced by Huang et al. in 2006 as a fast and efficient learning algorithm for single-hidden-layer feedforward neural networks.
> ELM differs from traditional neural networks in its training process. Instead of iteratively adjusting the weights and biases through backpropagation, ELM randomly assigns the input-to-hidden layer weights and biases, and then calculates the output weights analytically using a least-squares approach. This random initialization of hidden layer parameters allows ELM to achieve faster training times compared to other neural network algorithms.
> One key advantage of ELM is its ability to handle large-scale datasets efficiently. Due to its simple and fast training process, ELM can quickly learn from massive amounts of data without requiring extensive computational resources. It has been successfully applied in various domains such as image classification, speech recognition, regression analysis, and time series prediction.
> ELM also has good generalization performance, often achieving comparable or even better accuracy than traditional neural networks with fewer hidden neurons. This makes it suitable for applications where real-time processing or resource-constrained environments are crucial.
> In summary, Extreme Learning Machine is a machine learning algorithm that offers fast training times, efficient handling of large-scale datasets, and good generalization performance.

---
## Why ELM is different from standard Neural Network

**ELM doesn’t require gradient-based backpropagation to work. It uses Moore-Penrose generalized inverse to set its weights.**

First, we look at standard SLFN (Single hidden Layer Feedforward Neural network):

![Extreme Machine Learning (ELM)   ELM model explanation](https://i.imgur.com/p1Sa9Eb.png)

It’s pretty straightforward:
1. multiply inputs by weights
2. add bias
3. apply the activation function
4. repeat steps 1–3 number of layers times
5. calculate output
6. backpropagate
7. repeat everything

ELM removes step 4 (because it’s always SLFN), replaces step 6 with matrix inverse, and does it only once, so step 7 goes away as well.

---
## But why we need ELM? What's so different about them in practice?

Back propagation(BP) based algorithms played dominant roles in training feedforward neural networks in the past few decades. On the other hand, they lack faster learning algorithm for neural networks. 

The traditional learning algorithm may takes several hours, several days and even more time to train neural networks. Many algorithm have been proposed to improve the single feedforward neural network operation rate and precision such as BP algorithm and its improved algorithms. With the limitation of BP algorithms, generalization ability of network is unsatisfactory and over learning easily occurs. 

In 2004, Huang G.B proposed Extreme learning machine(ELM), which has shown its efficiency in training feedforward neural networks and overcoming the limitations faced by the BP algorithm and its variants.

---
## Learning algorithm

Steps:
1. Randomly assign weights and bias
2. Calculate hidden layer output
3. Calculate output weight matrix
4. Use the previous calculated weight matrix to make predictions on new data

Figure 1:

![Extreme Machine Learning (ELM)   model explanation 2](https://i.imgur.com/OitGWw4.png)

Figure 1 is the ELM network structure which includes n input layer neurons, l hidden layer neurons and m output layer neurons. 

Matrix X (input) and matrix Y (output) can be expressed as:

![Extreme Machine Learning (ELM)   matrixes](https://i.imgur.com/iE62Lpy.png)

---
## Reliability and issues

The reliable application of machine learning methods is increasingly crucial in challenging engineering domains. Although ELMs can seem pretty interesting and with good potencial mainly because of it simplicity, they have several reliability downsides:
- ELM relies on single hidden-layer neural networks with randomly initialized and fixed input weights, making it inherently unreliable.
- The black-box nature of neural networks, including ELM, raises concerns, deterring engineers from using them in unsafe automation tasks.

Although a great number of achievements on high dimensional data applications have been presented in the past several years, the following three issues are worth considering:
- Tuning-free is one of the most important contributions to ELM. However, various approaches and applications have applied the iterative updating processing into the original ELM to produce good generalization performance, such as the usage of genetic algorithms, the boosting approaches, the pruning methods, and the evolutionary ensembles. Although the model regression accuracy and data classification performance are more or less improved by introducing such strategies, there is no doubt that the computational complexity is also increased. Thus, how to balance the performance and the processing time is an open issue, especially for applications in high dimensional data.
- How to choose the optimal number of hidden neurons for a certain application is not well addressed yet. In most of the existing works, few efforts have been paid to discussions on the selection of hidden neurons and almost all of them are chosen manually in a tentative way. Although some researchers claimed that the performance of ELM and its variants tend to be stable and acceptable when a large number of hidden neurons are used, redundancy and high computation burden would also occur.
- Designing real-time processing systems and devices for applications with ELM is highly desired. Although plentiful achievements have been reported in the past 10 years or so, most of them are still conducted in the laboratory via computer simulations. Real-world devices for different applications are always facing various challenges, which are more obvious for large data applications.

---
## Simple ELM implementation

Based on: https://github.com/burnpiro/elm-pure
Presented in the original ELM paper *Extreme learning machine: A new learning scheme of feedforward neural networks by Huang et al.* 


<ins>Code available on:</ins> 
	[https://drive.google.com/file/d/18d4EBrUFrVZAW5O8csQRMFdg4rd_H8NO/view?usp=sharing](https://colab.research.google.com/drive/10XJ9JoJheOWBoghWHWr4l8NeGR4wqB-p?usp=sharing)