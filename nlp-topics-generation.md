
# NLP Topic generation and similarity score

- [NLP Topic generation and similarity score](#nlp-topic-generation-and-similarity-score)
  * [Topics generation](#topics-generation)
    + [Preparing data](#preparing-data)
    + [Training the model](#training-the-model)
    + [Appliyng trained model to the whole dataset](#appliyng-trained-model-to-the-whole-dataset)
  * [Similarity score generation](#similarity-score-generation)

## Topics generation

### Preparing data

Show main topics of a collection of text documents

```python
from sklearn.decomposition import NMF
from sklearn.feature_extraction.text import TfidfVectorizer

stop_words = ["a", "an", "the"]

# tfidf vectorize
tfidf_vectorizer = TfidfVectorizer(
    strip_accents='unicode',
    stop_words=stop_words, 
    ngram_range=(1,1)
)
vecotrized_texts = tfidf_vectorizer.fit_transform(source_dataframe['text_column'])
words_features_names = tfidf_vectorizer.get_feature_names()

```

### Training the model

```python
# Lets assume previous code has allready been evaluated

# Create an NMF instance: model
model_nmf = NMF(n_components = 50, verbose=True)
model_nmf.fit(vecotrized_texts)
```

### Visualize the topics

```python
# Lets assume previous code has allready been evaluated

def generate_topics(model, feature_names, n_top_words):
    for topic_idx, topic in enumerate(model.components_):
        message = "Topic #%d: " % topic_idx
        message += " ".join([feature_names[i]
                             for i in topic.argsort()[:-n_top_words - 1:-1]])
        print(message)
    print()

number_of_words_to_display_per_topic = 20
generate_topics(model_nmf, words_features_names, number_of_words_to_display_per_topic)
```

### Appliyng trained model to the whole dataset

After this, it could be interresting to know how much each document belong to a topic or to another topic

```python
# Lets assume previous code has allready been evaluated

# This will return a dataset with score of each topic in document
nmf_features_topics = model_nmf.transform(vecotrized_texts)
```

## Similarity score generation

Now we can try to find similarity of documents with consine distance calculation

```python
# Lets assume previous code has allready been evaluated
import pandas as pd
from sklearn.preprocessing import normalize

# Normalise nmf_features_topics dataset
normalized_nmf_features_topics = normalize(nmf_features_topics)

# Create dataframe to simplify work with dataset
normalized_nmf_features_topics_df = pd.DataFrame(normalized_nmf_features_topics)

# Lets assume we want to find similar entries to the first one
search_similar_entries_with = normalized_nmf_features_topics_df.loc[0]

# Apply cosine score calculation to whole document
similarities_cosine_score = normalized_nmf_features_topics_df.dot(search_similar_entries_with)

# Display those with the largest cosine similarity
number_of_entities_to_dispaly
print(similarities_cosine_score.nlargest(number_of_entities_to_dispaly))

```