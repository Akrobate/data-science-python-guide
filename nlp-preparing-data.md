# Natural langague processing - Preparing data

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

## MNF Topics generation

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

## Lementize function

## Stemming function

