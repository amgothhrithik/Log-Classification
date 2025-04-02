## Goal: To Classify log messages 
We will first convert messages into embedding later we wil use 3 methods to classify the log messages.They are: 
- Regex Classification
  - DBSCAN Clustering + Regex => For simple-pattern and repetitive messages.
- Non-Regex Classification(for non-pattern messages).
  - Linear Regression with enough samples in the dataset.
  - Llama for less number of samples.

## Converting into Embedding.
- Embedding are dense vector used to capture semantic relationship between sentences.
- In vector space, sentences with similar meanings have embeddings closer to each other, i.e., smaller angular distance (higher cosine similarity) or smaller Euclidean distance between them.
- We are using Sentence Transformer for finding Embeddings as they are optimied for sentence similarly tasks.


## Regex Classification
- We will use DBSCAN which is density based clustering to find patterns for Regex Classification.
- ADVANTAGES of DBSCAN clustering:
  - Robust to Outliers.
  - No need to specify clusters.
  - Can also be used for arbitary shaped clusters.
- After Clustering, we will check if there are any patterns in each cluster with min 10 datapoints by printing few.
- Later we filter the Non-Regex classified data.

## Classification on filtered Dataset
- We will convert messages into embedding using Sentence Transformer on filtered Dataset.
- We will check if each category under source column has enough datapoint. If no we further filter the dataset.
- We will use `llama-3.3-70b-versatile` model to classify the log message with few no. of datapoints in source column.
- For the remaining dataset, we will train logistic regression for classification.
- While predicting with Logistic Regression, we will predict only if the probability of predicted label is higher than threshold to avoid labelling irrelavent log messages.
- I aslo tried with Random Forest which performed similar to Logistic regression but it was difficult to filter the irrelavent log messages as the probability of predicted label was similar for both genuine and irrelavent log messages.
