Vectors for which the majority of values are 0.

Can often be stored and processed more efficiently than [[Dense Vectors]] (think of bitmaps).

In general, relevant for tasks/phenomena where there is a large number of potential features (high dimensionality), but each data point only uses a few of the available features.

Specifically, sparse vectors are common in NLP tasks because many popular ways of representing documents as embeddings are variations on the same principle: use a high-dimensional vector where each dimension represents a unique term (word) in the input vocabulary (variation on [one-hot](https://en.wikipedia.org/wiki/One-hot) technique). Since natural languages have large vocabularies, and most documents use only a tiny fraction of words in the vocabulary, the resulting document embeddings are sparse vectors.