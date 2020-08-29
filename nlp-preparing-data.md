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