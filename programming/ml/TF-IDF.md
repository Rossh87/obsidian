Term frequency-inverse document frequency is a family of mathematical formulae for quantifying the significance of a single term in the context of a text corpus, broken into documents. It is commonly used for search and ranked retrieval.

The idea is to count the occurrences of a term in a passage, and in the corpus as a whole. The frequency in the passage is used to decide the passage's relevance to a query term, weighted based on an inverse function that accounts for how often the term occurs in the corpus as a whole. If a searched-for term occurs often in a passage and rarely in the corpus as a whole, it is very likely the passage is relevant to the query term. As a word becomes more frequent in the corpus, the presence of a query term in a given passage becomes less useful for estimating the relevance of the passage.

TF-IDF is a *lexical*, not *semantic* search approach: it is a word-matching, not meaning-matching, algorithm.