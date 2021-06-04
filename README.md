# Ancient Texts - Identifying Authorship of Ancient Hebrew Texts
# By Rowana Ahmed, Sun Kim, Jie Sun, and Nellie Ponarul
Hebrew biblical texts are considered composite documents. Scholars have various views towards the authorship of each book, and the construction of compositional layers.
In this project, we aim to explore methods to determine whether a word, a verse or a chapter belongs to a particular author. We face several challenges: 

- (1) Because this is unsupervised text classification, there is no labeled training data. 
- (2) The exact number of authors is unknown, although scholars have theories which we will leverage in our validation process. 
- (3) The hebrew texts were ‘old’ hebrew without any vowels. Embeddings thus need to be trained without access to powerful pre-trained models such as GPT-2.

We aim to answer the following questions:

- What type of embedding best captures the style of each Biblical verse? Can an automated approach perform as well as manual methods used in previous research?
- How many authors wrote each of the first five books of the Bible?

View project presentation here: https://youtu.be/yFZDVMM_TH8

## Embeddings
Skip-gram, LSTM, BERT

An example of the BERT embeddings under tSNE is below:

![image](https://user-images.githubusercontent.com/58132970/120743939-82e1c880-c52c-11eb-80c5-82046176511e.png)


## Clustering methods
Spectral clustering, agglomerative clustering

An example of the spectral and agglomerative clustering below:
![image](https://user-images.githubusercontent.com/58132970/120744125-eb30aa00-c52c-11eb-8d3e-9b39ea1c7d54.png)

![image](https://user-images.githubusercontent.com/58132970/120744111-e1a74200-c52c-11eb-9e1e-17da2dfb6ce4.png)


## Model evaluation
- Supervised label prediction
- Artificial text generation

Results were compared with the biblical references by scholars:
![image](https://user-images.githubusercontent.com/58132970/120744239-203cfc80-c52d-11eb-994e-d4abef9f794a.png)
 
# Discussions

## Strengths

Our study has extensive exploration on three types of word embeddings, generated from both the Hebrew and the English bible. In addition, we adopted both spectral and agglomerative clustering for the unsupervised classification, which is unseen in previous publications.

We validated our models using an approach similar to Koppel and Akiva, in which a supervised model is built based on the result of the unsupervised classification. We also tested the robustness of the result on a randomly mixed text.

At the end, we also provided snippets of the generated clusters to compare with the biblical sources. This can provide reference for future studies.

## Limitations

The limitations of the embedding models from Skip-Gram is that it is originally designed to predict synonyms for a given word, rather than a given sentence. While we made appropriate aggregations of the embedding vectors to try to predict similarity between verses, the model is not actually designed to predict verse similarity. Additionally, in the absence of labeled data, we were forced to create couplets for each verse separately; if labeled data was available, we could have trained over multiple verses and used a wider window for broader context.

For the LSTM embeddings, we would expect the embedding to capture verse structure well, however it performed similarly enough to the skip-gram model that it may not have actually been doing a great job of capturing verse structure in its layer. This may have been improved upon with a deeper autoencoder, as the one we created for this task only had one layer.

For BERT embeddings, since the model process one verse at the time, it is possible that the context-based embeddings obtained are based on the verses, not the whole bible corpus. Although we have seen excellent performance of the BERT embeddings in the evaluation, this limitation may have hindered us in producing an even better representation of the text features.

A greater limitation comes from the way embeddings are used. While our objective is to determine the authorship of the text, we assume that each author will have their own distinct style. The embeddings however, capture not only the stylistic differences, but also the content differences. We are not able to control what aspects the embeddings can extract, as they are meant to represent overall features of the verses.

Another limitation includes the fact that there is no inherent right answer for the unsupervised text classification. It is also difficult to understand why certain sentences are attributed to one author, but not the other. This is also the limitation that we have observed in many previous published work on this topic. We are relying on the heuristics of the embeddings or other feature extraction methods, without being able to make linguistic or lexical interpretations.

## How to improve

Common to most NLP problems, enlarging the corpus may provide more meaningful contextual information, especially for the skip-gram model. Future studies could also focus on building a connection between the word embeddings and their linguistic characteristics, so that we can understand what features lead to the classification. For example, an RNN model can be built, in which we can visualize which word or phrases are activated for the classification. Additionally, lower level character embeddings could provide meaningful information on punctuation usage and part of speech identification could be used to analyze sentence structures. Richer ensemble methods considering the various facets of linguistic characteristics could improve overall performance.
