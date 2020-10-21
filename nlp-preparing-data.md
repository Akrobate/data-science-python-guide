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
