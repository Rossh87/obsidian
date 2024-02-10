## Tasks

Elastic allows deploying [[BERT]] -like pretrained language models for various NLP tasks. The task type is part of the `inference_config` object. These tasks fall into 3 main buckets, each with a set of specific sub-tasks:
1. **Information Extraction**: models can be used to extract particular info from unstructured records or queries.
	1. **Named entity recognition**: extract entities (generally simple or compound nouns) from text and assign them a class.
	2. **Fill mask**: fill-in-the-blank. Texts with a placeholder string (e.g. 'MASK') are offered to the model and it is asked to predict the value of the placeholder.
	3. **Question answering**: A long input text is submitted along with a question to be answered based on the input context. The model tries to answer the submitted question.
2. **Classify text**: Exactly what it sounds like.
	1. **Language identification**: Return most probable language(s) of source text. NB Elastic comes with a trained language recognizer built-in (`lang_ident_model_1`) that can be [used in ingest pipelines](https://www.elastic.co/blog/multilingual-search-using-language-identification-in-elasticsearch)
	2. **Text classification**: Assign source texts to one-of-2 (binary) or one-of-many classes. An example is a sentiment analyzer, where classes are 'POSITIVE' and 'NEGATIVE'.
	3. **Zero-shot text classification**: Basically the same as 2, except that the model used is not trained with specific classification data. Instead, it uses a model trained on a large dataset to have general language understanding, and the labels are provided along with the source text.
3. **Search and Compare**: embed and search
	1. **Text embedding**: use a model to generate vectors for source content
	2. **Text similarity**: express the similarity of two pieces of text as a numeric value. For example, take an array of input texts and a fixed comparison text, and decide which input is most similar to the comparison text. Use-case for this is a bit fuzzy; potentially use a model trained to embed questions with their answers and filter input documents based on subject relevancy? Could be used to keep extraneous texts from being indexed.

## Model Selection

Model compatibility is described [here](https://www.elastic.co/guide/en/machine-learning/8.8/ml-nlp-model-ref.html). In general, models the use the [[BERT]] interface and WordPiece tokenization algorithm are likely compatible.