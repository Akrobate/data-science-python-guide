# Natural langague processing - Preparing data

- [Natural langague processing - Preparing data](#natural-langague-processing---preparing-data)
  * [TfIdfVectorizer](#tfidfvectorizer)
  * [Langage detecting with langdetect package](#langage-detecting-with-langdetect-package)
  * [Lambda function to normalize text](#lambda-function-to-normalize-text)
  * [Lemmantize function](#lemmantize-function)
  * [Stemming function](#stemming-function)
  * [MNF Topics generation](#mnf-topics-generation)

## TfIdfVectorizer

```python
from sklearn.feature_extraction.text import TfidfVectorizer

stop_words = ["a", "an", "the"]

tfidf_vectorizer = TfidfVectorizer(
    strip_accents='unicode',
    stop_words=stop_words, 
    ngram_range=(1,1)
)

vecotrized_texts = tfidf_vectorizer.fit_transform(source_dataframe['text_column'])
```

## Langage detecting with langdetect package

```python
from langdetect import detect

text = "Bonjour le monde"

if (detect(text) == 'fr'):
    print("text is french")
else:
    print("text is not in french")
```

## Lambda function to normalize text

```python
import re
import pandas as pd

''' Example of simple function to normalize text '''
def pre_process_text(text):
    # lowercase
    text = text.lower()
    #remove tags
    text = re.sub("&lt;/?.*?&gt;"," &lt;&gt; ", text)
    # remove special characters and digits
    text = re.sub("(\\d|\\W)+"," ",text)
    return text

dataframe['text_column'] = dataframe['text_column'].apply(lambda value:pre_process_text(value))
```

## Lemmantize function

Lemmantize using spacy module. Be aware that you have to download the langague core that you need. Here "fr_core_news_md" whas downloaded

```python
import spacy
nlp = spacy.load('fr_core_news_md')

def lemmantize(text):
    result = []
    for token in nlp(text):
        result.append(token.lemma_)
    return ' '.join(result)

dataframe['text_column'] = dataframe['text_column'].apply(lambda value:lemmantize(value))
```

## MNF Topics generation

Show main topics of a collection of text documents

```python
from sklearn.decomposition import NMF
from sklearn.feature_extraction.text import TfidfVectorizer

def generate_topics(model, feature_names, n_top_words):
    for topic_idx, topic in enumerate(model.components_):
        message = "Topic #%d: " % topic_idx
        message += " ".join([feature_names[i]
                             for i in topic.argsort()[:-n_top_words - 1:-1]])
        print(message)
    print()

stop_words = ["a", "an", "the"]

# tfidf vectorize
tfidf_vectorizer = TfidfVectorizer(
    strip_accents='unicode',
    stop_words=stop_words, 
    ngram_range=(1,1)
)
vecotrized_texts = tfidf_vectorizer.fit_transform(source_dataframe['text_column'])
words_features_names = tfidf_vectorizer.get_feature_names()

# Create an NMF instance: model
model_nmf = NMF(n_components = 50, verbose=True)
model_nmf.fit(vecotrized_texts)

number_of_words_to_display_per_topic = 20
generate_topics(model_nmf, words_features_names, number_of_words_to_display_per_topic)

```

After this, it could be interresting to know how much each document belong to a topic or to another topic

```python
# Lets assume previous code has allready been evaluated

# This will return a dataset with score of each topic in document
nmf_features_topics = model_nmf.transform(vecotrized_texts)
```

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
print(similarities_cosine_score.nlargest(10))

```