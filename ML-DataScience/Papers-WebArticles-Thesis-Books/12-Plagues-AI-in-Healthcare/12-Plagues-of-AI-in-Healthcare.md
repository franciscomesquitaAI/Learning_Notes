The healthcare sector eagerly anticipates leveraging Artificial Intelligence (AI), particularly machine learning (ML), to enhance healthcare delivery. Despite significant investments from medical professionals, data scientists, and Big Tech, AI-based medical devices often fall short of their promised clinical impact, necessitating proactive management of common pitfalls to optimize their efficacy.

---

# Information

**Paper link**: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9110785/pdf/fdgth-04-765406.pdf
**First Author**:  Stephane Doyen - https://scholar.google.com/citations?user=btcExuEAAAAJ&hl=en

---
# Main topics and ideas

- Despite not being newly introduced, AI-based medical devices have more than often been limited in their true clinical impact that was originally promised or that which is likely capable.

- Google promises to detect 26 skin conditions with accuracy comparable to US board-certified dermatologists, yet recent work has already come under substantial controversy due to under performance based on underlying inter-individual differences in demographics, such as gender and skin color.

- The ability for human intuition alone to map the brain for instance, would take insurmountable amounts of time and effort compared to that which is now possible with AI-based technology.

- As with all emerging fields, further work is necessary to optimize the clinical applicability of these tools as we move forward to minimize unnecessary errors and harm.

- There is limited information available in the literature that presents a clear guide of the common problems that will be encountered with AI-based software, and more specifically how to overcome them moving forward in medical practices. Such a gap possibly reflects the separation of expertise and focus between medical professionals and data scientists all together.

---
# The 12 plagues in healthcare 

![image\|600](https://i.imgur.com/cSA5fNf.png)

---
# Problems in AI healthcare models

## Approach: what is the plan?

<u>Problem 1. Relevance: Cutting Cake With a Laser:</u>
-   Due to a rise in the amount of open-source and advanced statistical software, it has become increasingly easy to develop highly elegant and powered computational models.
-   When created with only technical solutions in mind, models can easily be created to solve an non-existent or irrelevant problem.
-   The ultimate users of the technology should be included at the very beginning of the development of the model.
-   Ultimately, it must be remembered that AI is a powerful tool that can be leveraged to answer a difficult questions, the usefulness of the tool is a function of the appropriateness of the question being asked.

<u>Problem 2. Practicality: Not Everyone Has a Cyclotron:</u>
- Refers to building a model which has limited practical applications in the environment of interest due to logistical constraints that were not considered outside of the environment that the model was originally created in, such as requiring more computation than necessary or that which can be feasibly run in a clinic.
- When just utilizing the limited available data obtained specifically from academic studies to train a model, illusory results may be obtained given these data are cleaner than that which would be obtained from the actual target field.
- A notable increase in recent efforts has been put forth by cloud providers and hardware manufactures to provide development frameworks which bridge the gap between an approach to a problem and the hardware to support it.

---
## Data: What are we using and for what purpose?

<u>Problem 3. Sample Size: Looking at the World Through a Keyhole:</u>
- Small sample size may cause a model to present results that are merely due to chance.
- When creating and training a model using a limited sample size, inflated results may be demonstrated when actually testing it against a control sample. Subsequently, when introduced into a different, clinical environment, the model’s accuracy can lessen, and it can fail.
- As in all aspects of medical research, newer ML models must be trained on a large and diverse dataset to provide reliable results.

<u>Problem 4. Discriminatory Biases: Rubbish in, Rubbish Out:</u>
- Developing models with historical data may perpetuate our historical biases on a variety of different patients in ways we have since improved from.
- Recent work has suggested one of the major sources of these inequalities stems from the lack of representation of race and skin tone in medical textbooks. Medical schools in recent years have immediately begun to address these concerns by updating textbook images for increased inclusivity, yet deep learning (DL) image-based classifier algorithms often continue to use low quality datasets for training, which commonly contain unidimensional data (e.g., mostly lighter skin images).

<u>Problem 5. Generalization to New Populations: From the Few, but Not the Many:</u>
- Problems with generalization may occur due to the expansion of global software markets. Aside from differences in gender and skin color alone, a model may fail based on datasets trained on individuals from a single population due to underestimating the differences in population driven variability.
- Most consider that using multi-centric data improves the external validity of a model’s results given that it tests samples of individuals from a variety of locations. However, if all the centers providing data are within a single country, such as in the United States for instance, how will these models perform in China where there are unique individual characteristics that are concomitantly shaped by differences in the environment?
- Surely, inter-individual factors must be considered during production to improve the robust ability of a model in different environments. Nonetheless, it is also likely that site-specific training should also be considered as an optimal avenue to tailor models based on the specific populations where a model is going to be implemented.

<u>Problem 6. Emergence of New Trends: Surfacing Creatures From the Depth:</u>
- Problems related to the emergence of new trends refers to when a new trend emerges in the data that the initial model was not built to account for, thus altering the new statistical comparisons being made between variables.
- ML tools can be applied to estimate which strains will be most common in upcoming seasons with high accuracy to be included in upcoming seasonal vaccines (46). However, unexpected changes can occur in the environment, such as a new pandemic, which drastically alters the environmental landscape and therefore changes the way two variables may be modeled based on new environmental parameters. If there is not an ongoing monitoring system in place, these models can lead to potential harm as results are no longer reliable.
- When utilizing brain mapping software on an individual patient with different scans, erroneous brain network anomalies may arise and can lead to inappropriate neurosurgical treatments just merely due to the inability of a model to account for differences in functional magnetic resonance imaging (fMRI) scanners utilized.
- Continual external validation testing with separate adequately sized datasets than which it was trained on provides a necessary avenue for improvement as the field of healthcare and the environment itself is continually changing.

---
## Method: How does the tech approach play out

<u>Problem 7. Reproducibility: Bad Copies:</u>
- Failure of a model to demonstrate the same results time and time again presents a profound risk of inconsistencies in the delivery and quality patient care, and therefore should be considered in future ML developments.
- To ensure an ML algorithm applied in the healthcare setting is fully reproducible, some have suggested that a study should produce the same results according to technically identical conditions (related to code and dataset release), statistically identical conditions (related to differences in sampled conditions still yielding the same statistical relationships), and conceptually identical conditions (related to how the results are reproduced in accordance with pre-defined descriptions of the model’s effects). When these methods of reproducibility are not met, the one who created the model would be unable to replicate its results on subsequent runs. Furthermore, when others are attempting to assess the model, possibly to improve its applicability, they too will be unable to obtain the reported effects by the original authors.

<u>Problem 8. Explainability: The Black Box Problem:</u>
- One of the largest concerns of AI-based devices in medicine concerns physicians’ lack of trust for model performance. Unfortunately, as ML models have increased in complexity, this improvement has often been met with a trade-off in explainability, in which there is increasing uncertainty regarding the way these models actually operate.
- Black box models could not tell almost nothing about why a model made a specific decision.
- A common example of this can be seen with a highly powered ML technique known as deep learning (DL). DL applications can maintain hundreds of stacked representations across hundreds of layers, a relationship that no human can truly accurately comprehend in full detail.
- Important improvements can be made in the field as we improve concerns of lack of explainability, to which a whole field has been dedicated known as Explainable Artificial Intelligence (XAI)
- However, if we could explain the various decisions being executed by a certain model and the specific features being analyzed to produce a certain outcome, physicians can better interpret these results based on logic and previous knowledge.
- Interpretable and explainable models may also unlock new insights in the scientific world that spur further improved ML developments in the future, creating a positive reinforcing cycle of innovation.
- Outside of the trust of a practicing healthcare provider, the patient themself, if diagnosed by a ML tool to have a malignant skin lesion, may too require an interpretable and justifiable reason why specific results were provided, such as why the tumor was diagnosed as malignant.
- Furthermore, if a model provides a piece of information that leads to a poor outcome for a patient, is it the machine’s fault or is it the healthcare provider’s medical error?
- For example, a number of recently developed practical approaches have been introduced using input vector permutation to better understand how specific inputs impact the predictions of a model and may be particularly useful to gain insight into how models make specific decisions.
- Explainable AI approaches, such as deconvolution methodology, can be applied to more complicated models, such as convolutional neural networks (CNNs) and ensembles, to improve the interpretability of the more complex models.
- However, further research is needed in the field of explainable AI to better understand model-specific techniques that can be leveraged to ultimately improve the transparency of these models in the healthcare setting.

<u>Problem 9. Accidental Fitting of Confounders: Guilt by Association:</u>
- ML tools are able to digest highly complex datasets by continually assessing and scanning different features until optimal performance is achieved. As such, concerns of accidentally fitting confounders can easily surface and a model that was thought to be capable of predicting an outcome is instead making a prediction based on factors unrelated to that outcome of interest. If so, these models can produce not only unreliable results in clinical practice, but can also present profound risks of patient harm, such as by under- or over-estimating specific diagnoses.
- First, an ML specialist must have a strong understanding of the data being modeled. Then, when actually developing the model, one should carefully explore and rule out any concerns for confounders. In addition to previous descriptions of “whitebox” models, improved understanding of the features being mapped may allow further appropriate critical evaluations of model performances and in turn lead to increased trust in the medical community.

---
## Operations: in the field

<u>Problem 10. Model Drift: Like a Rolling Stone:</u>
- For many of the reasons discussed above, over time a model will likely begin to make an accumulating number of errors. This could be due to issues with model drift, in which a model that was deployed into production many years ago would begin to show performance decay over time. Different than problems with the emergence of a new trend, model drift represents a multifactorial issue that likely reflects the relationship between two variables changing with time, ultimately causing a model to become increasingly unstable with predictions that are less reliable over time.
- Without considering the possibility of a model drifting, a model can begin to predict outcomes in an unexpected way, which in a healthcare setting could immediately represent incorrect diagnoses being made.
- To account for model drift, both active and passive methods have been proposed, of which the later represents the easiest solution to implement. Active methods refer to the methodology for detecting this drift and then self-adjusting its parameters to retrain the system to account for this shift, such as by forgetting old information and then updating based on new data. However, this methodology is more practical when data is available as a continual stream that will allow a model to continually adapt to recent data inputs. Differently, passive learning methods are reliable in that the performance of a model will be continually or periodically monitored by developers, such as through each release cycle, thus ensuring consistent and reliable results according to the model’s original results. As more data becomes available, passive methods could allow users to adapt the model and retrain it based on new data and updated scientific knowledge. Thus, this method could allow for more transparency over time concerning the model’s performance, avoiding scenarios where a model may make decisions on new relationships that are non-interpretable or even scientifically unsound.

<u>Problem 11. Practicality Over Hospital Context: Will the IT Department Say Yes?:</u>
- Systems should be developed according to the environment in which they will be deployed.
- There are a number of strict requirements that technology must follow in a healthcare setting that may not be accounted for, especially with cloud-based computing software. Thus, a system should be developed based on how hospitals are organized and specifically how healthcare providers will plan to use these models.
- If the system implemented is too computing heavy, the model itself may become impractical as it can take hours to run on a lesspowered healthcare provider’s laptop.

<u>Problem 12. Hacking: One Voxel Attack</u>
- Despite the novelty of advanced ML systems that are highly capable of managing complex data relationships, it must be remembered that ML systems are inherently IT systems which can be similarly fooled and hacked by outsider users.
- One particular well-known threat is described as the “onepixel attack,” referring to the ability to drastically fool a neural network by just changing a single pixel in the image being analyzed . In turn, this causes the model to classify the image as being of a different class than what is actually represented in the image. Ultimately, this single form of hacking merely suggests the vulnerable nature of ML systems, and also contributes to the truth that we do not always fully understand how a model may be working.
- A number of methods have been proposed to prevent the damage from these adversarial attacks. Re-training the model with robust optimization methodology can increase the resistance of a model to these attacks. Increase detection methods to identify attacks may also be appropriate. Other methods have also been similarly described, but it remains uncertain the degree to which these methods are better than others for a given scenario. Nonetheless, what is certain is that the integrity and robustness of an AI system must be rigorously examined against known attacks to achieve further safety and trust with applications in the medical field.

---
# Score: 9
-   Very relevant topic and clear contributions.
-   A good division was made in 4 different categories of the main problems when we work with AI and ML applied to health.
-   Extremely well organized and written article.
-   I liked and agree with all the problems presented. Each problem was explained in an almost perfect and succinct way, where I was able to learn a number of interesting terms and concepts.
-   The article is not very technical, but the concepts presented are a kind of brief explanation of the obstacles that exist to have better models and usable models in the health area.
-   Graphical representations of each type of problem could be shown more clearly, but what has been done is clear enough.
-   Overall a must-read for everyone working and exploring health-oriented AI / ML / DL
