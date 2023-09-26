---
share: true
path: 'Online Courses/GenerativeAI Short Courses - DeepLearningAI/Understanding and Applying Text Embeddings'
attachment:
  send: true
  folder: 'Online Courses/GenerativeAI Short Courses - DeepLearningAI/Understanding and Applying Text Embeddings/assets'
---

Here we will use Vertex AI to import a pretrained model.

> [!ai]+ AI
>
> Vertex AI is a machine learning (ML) platform provided by Google Cloud. It offers a unified and integrated environment for building, deploying, and managing ML models. With Vertex AI, developers and data scientists can access various tools and services to streamline the entire ML lifecycle, including data preparation, training, evaluation, deployment, and prediction.
> The platform provides AutoML capabilities that enable users to build ML models without extensive programming knowledge. It also supports custom model development using popular ML frameworks like TensorFlow and PyTorch. Vertex AI leverages Google's infrastructure for scalability and reliability, allowing users to train models on large datasets efficiently.
> Additionally, Vertex AI offers features like hyperparameter tuning, model monitoring, and explainability for better model performance and interpretability. It integrates with other Google Cloud services such as BigQuery for data storage and preprocessing and provides APIs for easy integration with applications.
> Overall, Vertex AI aims to simplify the process of developing ML models by providing a comprehensive set of tools and services in a unified platform.


<ins>Import pretrained model from vertexai:</ins>
```Python
embedding_model = TextEmbeddingModel.from_pretrained("textembedding-gecko@001")
```

<ins>Obtain embedding for one given sentence:  </ins>
```Python
embedding = embedding_model.get_embeddings(["What is the meaning of life?"])
```

<ins>Calculate the similarity between two sentences as a number between 0 and 1.</ins>
```python
from sklearn.metrics.pairwise import cosine_similarity
emb_1 = embedding_model.get_embeddings(["What is the meaning of life?"]) # 42!

emb_2 = embedding_model.get_embeddings(["How does one spend their time well on Earth?"])

emb_3 = embedding_model.get_embeddings(["Would you like a salad?"])

vec_1 = [emb_1[0].values]
vec_2 = [emb_2[0].values]
vec_3 = [emb_3[0].values]

print(cosine_similarity(vec_1,vec_2)) 
print(cosine_similarity(vec_2,vec_3))
print(cosine_similarity(vec_1,vec_3))
```


---

Sentence embeddings take into account words position, unlike words embedding:

![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings.png)
## What is an embedding?

Way of representing data as points in space where locations are semantically meaningful.

![center|700](assets/Understanding%20and%20Applying%20Text%20Embeddings_embeddingslogic.png)

## How are sentence embeddings computed?

- **Simple method:** Embed each word separately, and take a sum or mean of all the word embeddings
- **Modern embeddings:**  
	- Use a transformer neural network to compute a context-aware representation of each word.
	- Compute embeddings for each token (sub-word) rather than word. This enables the algorithm to work even for novel words and misspelt word ("unverse, bok, compter,...") - **This is how embeddings are usually prepared for LLMs**

**How are the transformer network trained? how we get the pairs of "similar" sentences?**
	Through "contrastive learning". NN is tuned to move similar sentences embeddings together, and dissimilar sentences embeddings apart.

> [!ai]+ AI
>
> Contrastive learning is a machine learning approach that aims to learn representations by contrasting similar and dissimilar samples. It involves training a model to maximize the similarity between positive pairs (samples that should be similar) and minimize the similarity between negative pairs (samples that should be dissimilar).
> In contrastive learning, two data augmentations are applied to an input sample, creating two augmented versions of the same sample. These two augmented samples form a positive pair. Simultaneously, another sample from a different class or category is chosen, and its augmented version forms a negative pair with the original sample.
> The objective is to train the model in such a way that it can discriminate between these positive and negative pairs. By doing so, the model learns to encode useful information about the underlying structure of the data and can generalize well to new, unseen samples.
> Contrastive learning has been particularly effective in self-supervised learning settings where labeled data is scarce or expensive to obtain. It has been successfully applied in various domains, including computer vision and natural language processing, leading to advancements in tasks such as image classification, object detection, and representation learning.

## Text embeddings application

![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_embeddingsapplications.png)

<ins>Anomaly / Outlier detection: </ins>
	We can add an anomalous piece of text and check if the outlier (anomaly) detection algorithm (Isolation Forest) can identify it as an outlier (anomaly), based on its embedding.

```Python
from sklearn.ensemble import IsolationForest

input_text = """I am making cookies but don't remember the correct ingredient proportions. 
                I have been unable to find anything on the web."""

emb = model.get_embeddings([input_text])[0].values
embeddings_l = question_embeddings.tolist()
embeddings_l.append(emb)

embeddings_array = np.array(embeddings_l)

# Add the outlier text to the end of the stack overflow dataframe
so_df = pd.read_csv('so_database_app.csv')
new_row = pd.Series([input_text, None, "baking"], index=so_df.columns)
so_df.loc[len(so_df)+1] = new_row


# Use Isolation Forest to identify potential outliers
	# IsolationForest` classifier will predict `-1` for potential outliers, and `1` for non-outliers.
	# You can inspect the rows that were predicted to be potential outliers and verify that the question about baking is predicted to be an outlier.

clf = IsolationForest(contamination=0.005, random_state = 2)

preds = clf.fit_predict(embeddings_array)
so_df.loc[preds == -1]

# Remove the outlier about baking
so_df = so_df.drop(so_df.index[-1])
```

## Multi-modal embeddings

Can relate multiple types of inputs:
![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_multi_modal_embeddings.png)

---

We can plot embeddings of some sentences and see how they are related (2d point plot or heatmap).
	To measure similarity we should use original vectors and not the compressed (after PCA one).

<ins>Cluster the embeddings of the Stack Overflow questions:</ins>
```python
from sklearn.cluster import KMeans
from sklearn.decomposition import PCA
from utils import clusters_2D
import matplotlib.pyplot as plt
import mplcursors
%matplotlib ipympl

clustering_dataset = question_embeddings[:1000]

n_clusters = 2
kmeans = KMeans(n_clusters=n_clusters, 
                random_state=0, 
                n_init = 'auto').fit(clustering_dataset)

kmeans_labels = kmeans.labels_

PCA_model = PCA(n_components=2)
PCA_model.fit(clustering_dataset)
new_values = PCA_model.transform(clustering_dataset)


clusters_2D(x_values = new_values[:,0], y_values = new_values[:,1], 
            labels = so_df[:1000], kmeans_labels = kmeans_labels)
```


![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_2dplot.png)

![center](assets/Understanding%20and%20Applying%20Text%20Embeddings_heatmap.png)

This visualization are not that precise and are just used to get an idea on how embeddings work.

---
## Using LLMs to generate text

<ins>Load pretrained LLM model from vertexai:</ins>
```python
generation_model = TextGenerationModel.from_pretrained("text-bison@001")
```

<ins>Asking something to the model:</ins>
```Python
prompt = "I'm an AI entusiast. \ Recommend me a programming activity to improve my skills."

print(generation_model.predict(prompt=prompt).text)
```

<ins>Making the model extract information and format it as a table:</ins>
```Python
prompt = """ A bright and promising wildlife biologist \ named Jesse Plank (Amara Patel) is determined to make her \
mark on the world. Jesse moves to Texas for what she believes is her dream job, 
only to discover a dark secret that will make \her question everything. 
In the new lab she quickly befriends the outgoing \lab tech named Maya Jones (Chloe Nguyen), 
and the lab director Sam Porter (Fredrik Johansson). Together the trio work long hours on their research \
in a hope to change the world for good. Along the way they meet the comical \
Brenna Ode (Eleanor Garcia) who is a marketing lead \ at the research institute, 
and marine biologist Siri Teller (Freya Johansson).

Extract the characters, their jobs \ and the actors who played them from the above message as a table
"""

response = generation_model.predict(prompt=prompt)

print(response.text)
```

When generating text input, the model creates an array with the probability of words that can be next. Look at the example:

![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_choosenextword.png)


But how should be the choosing (decoding) strategy?
- **Greedy decoding**: The one with the highest probability. It is good but can result in multiple equal sentences and always getting the same recommended word.
- **Random sample**: We might end up with some unusual tokens and very weird words for sentence.

We can controle this with the temperature parameter:
![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_temperatureparameter.png)

With temperature = 0, we have a deterministic choice (not creative but reliable):
![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_temperature0.png)


As temperature increases, randomness also increase:
![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_temperatureincrease.png)


We have two more parameters that we could set: Top P and Top K:
- **Top K**: select k samples with the most probabilities and random select one.

![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_TopK.png)

- **Top P:** select all samples with probability greater or equal to P (best solution?)
![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_topP.png)

<ins>Predicting next word using temperature, top_k and top_p parameters:</ins>
```Python
generation_model = TextGenerationModel.from_pretrained("text-bison@001")

prompt = "Complete the sentence: As I prepared the picture frame, I reached into my toolkit to fetch my:"

top_k = 20 # 20 samples with higher probabilities
top_p = 0.7 # Only select samples with probability greater or equal a 70%

response = generation_model.predict(
    prompt=prompt, 
    temperature=0.2, # Not too much creative in order to obtain reliable results
    top_k=top_k,
    top_p=top_p,
)

print(f"[top_p = {top_p}]")
print(response.text)
```


---

## Semantic Search, building a Q&A System

Out of the box LLMs aren't connected to the real world.

When we have a dataset comprising questions, answers, and their associated embeddings, if a user asks a particular question, we can seek out the most alike question from the dataset to the user's query and return the corresponding response:

![center|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_qeasimilarity.png)

### **Best way to measure similarity?**

Options:
![500|center](assets/Understanding%20and%20Applying%20Text%20Embeddings_optionsmeasuresimilarity.png)

There is no straight answer for the best method (?) but on the course it is used the cosine similarity.


Compare the computed embedding from user's input with the collection of embedding vectors is infeasible for large datasets and will almost certainly fail in production envionments.
- Instead, we can use algorithms that perform approximate matches like ScaNN. https://blog.research.google/2020/07/announcing-scann-efficient-vector.html?m=1

> [!ai]+ AI
>
> ScaNN (Scalable Nearest Neighbors) is an algorithm that allows for efficient approximate similarity search in large collections of vectors. It is designed to handle high-dimensional vector spaces commonly encountered in natural language processing tasks.
> The ScaNN algorithm constructs an index structure that partitions the vector space into smaller regions, allowing for faster search operations. This index structure is built using a combination of hierarchical clustering and graph-based partitioning techniques.
> During the search process, ScaNN performs an approximate nearest neighbor search by traversing the index structure to identify potential candidates. It then uses a more accurate distance metric, such as cosine similarity, to rank these candidates and retrieve the most similar vectors.
> One of the advantages of ScaNN is its ability to handle huge collections of vectors with millions or even billions of entries efficiently. It achieves this by utilizing techniques such as quantization and pruning to reduce the computational cost of similarity calculations.
> Overall, ScaNN provides a scalable and efficient solution for measuring similarity in large datasets, making it suitable for production environments where real-time or near-real-time response times are required.

![centert|500](assets/Understanding%20and%20Applying%20Text%20Embeddings_resume_all_q&a_system.png)

<ins>Q&A system with a scalable approach using ScaNN method and measure execution time:</ins>

```Python
import scann
import time
from utils import create_index


#Create index using scann
index = create_index(embedded_dataset = question_embeddings, 
                     num_leaves = 25,
                     num_leaves_to_search = 10,
                     training_sample_size = 2000)

query = "how to concat dataframes pandas"

start = time.time()
query_embedding = embedding_model.get_embeddings([query])[0].values
neighbors, distances = index.search(query_embedding, final_num_neighbors = 1)
end = time.time()

for id, dist in zip(neighbors, distances):
    print(f"[docid:{id}] [{dist}] -- {so_database.input_text[int(id)][:125]}...")

print("Latency (ms):", 1000 * (end - start))
```
