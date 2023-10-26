## Query context
If a query pattern in *query* context matches a document, the *relevance score* of that document is increased relative to its peers for the current query. Clauses should be executed in query context to answer the question 'how *well* does a document match compared to its peers?'.

## Filter context
If a query pattern in *filter* context matches a document, the document will be included in the search results (provided it is not excluded by another filter pattern), but the match does not contribute to the document's relevance score. Clauses should be executed in filter context to answer the question 'should this document be considered for further matching?'. Clauses in filter context can be cached from previous queries.

## Compound queries
Compound queries wrap atomic query clauses ('leaf queries') to combine their effects in some way. For example, a `must` and `should` clause nested under a `bool` query will cause the scores from both clauses to added together to get the final document score.

The most common compound query is `bool`, but there are [several others](https://www.elastic.co/guide/en/elasticsearch/reference/current/compound-queries.html). 

4 clauses can appear under a `bool` compound query:
1. `must`: returned documents must match the specified query, and meeting this condition will contribute to the document's score.
2. `filter`: returned documents must match the specified query, but the score is ignored, and the clause result for the document can be cached.
3. should: accepts a list of conditions that a document might match, but is not required to match. Each match increases the document's score. Useful to express optional criteria or preferences without excluding documents that don't meet them.
4. `must not`: essentially an 'exclude' clause. Executes in filter context, not query context. Use in cases when a single 'exclude' is simpler than multiple 'includes' via `filter`

## Text queries
Use to search fields of type `text`--these fields are automatically run through a [text analyzer](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis.html). The most common and basic clause is [match](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-match-query.html), which runs the provided query through the same text analyzer that was used on the field to be searched, and the resulting tokens are matched against the tokens in the analyzed field. Params like fuzziness are easily configurable. Note that the individual tokens are matched by default (not the whole phrase), and a boolean operator is applied to each token to get the entire token set to trigger a match. The default operator is OR, so the query 'Eddie Bauer' will match a text field that contains 'eddie' or 'bauer' or both. `match` operates as a `bool` clause, so each matched token contributes to the document's final score.

## Term queries
Use to find precise values in structured data. Term-level queries are *not* run through any analyzer, but will be run through the normalizer for fields of type `keyword` if one is specified on the field. The most common/simple term-level clauses are `term` and `terms`: match fields that contain one or at least one of the specified term or terms, respectively.

Do not use to search fields of type `text`: a `text` field is stored as analyzed and normalized tokens, but search `terms` are not analyzed. Since the term expects an exact match, it may find few or no results in the tokens stored in a `text` field, [even if one would be expected](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-term-query.html#avoid-term-query-text-fields).