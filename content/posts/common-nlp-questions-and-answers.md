---
title: Common NLP Questions and Answers
slug: common-nlp-questions-and-answers
published: true
date: 2026-05-22
featured: true
status: Published
excerpt: A study note answering common NLP questions about ABSA, tokenisation, Naive Bayes, vector semantics, logistic regression, RAG, fine-tuning, hallucinations, and ethics.
tags: [NLP, Machine Learning, Text Classification, LLMs, Study Notes]
coverImage: /blog-covers/common-nlp-questions-and-answers.png
mediaAltText: "Generated cover for Common NLP Questions and Answers"
---

# Common NLP Questions and Answers

This note collects short answers to common Natural Language Processing questions. I wrote it as a revision-style guide, so each answer focuses on the main idea, the reason it matters, and the terms I would use in an exam or interview.

## How did you justify your ABSA task?

ABSA stands for Aspect-Based Sentiment Analysis. I justified the task by explaining that normal sentiment analysis is often too broad. A whole review can be labelled as positive, negative, or neutral, but that label does not tell us what the person liked or disliked.

ABSA is useful because it separates the opinion target from the opinion itself. For example, in the sentence "The food was great, but the service was slow", document-level sentiment would struggle because the review is mixed. ABSA can identify that "food" has positive sentiment and "service" has negative sentiment.

The task is justified when the goal is to understand detailed feedback. It is especially useful for product reviews, restaurant reviews, customer support messages, app reviews, and survey responses because it helps answer questions like:

- Which parts of the service are people happy with?
- Which aspects are causing complaints?
- Are customers negative about the price, quality, delivery, usability, or support?

So the justification is that ABSA gives more actionable insight than a single overall sentiment label.

## Would you use logistic regression, a discriminative classifier, to classify your data into aspects?

Yes, logistic regression can be used as a discriminative classifier for aspect classification, especially as a strong baseline model. It learns the boundary between classes directly by estimating the probability of an aspect label given the input features.

For text classification, the text would normally be converted into numerical features first, such as bag-of-words, TF-IDF, n-grams, or embeddings. Logistic regression can then learn which words or features are associated with each aspect. For example, words like "battery", "charge", and "power" may be strong indicators of a battery aspect in product reviews.

I would use logistic regression when:

- the dataset is not extremely large
- interpretability matters
- I want a reliable baseline
- the aspects are reasonably separable from the text features

However, logistic regression may struggle when aspect meaning depends on deep context, long-distance dependencies, sarcasm, or complex wording. In those cases, transformer models such as BERT or another fine-tuned language model may perform better.

## What are some of the hyperparameters you can adjust in model training?

Hyperparameters are settings chosen before or during training that control how the model learns. Common hyperparameters include:

- learning rate, which controls how large each update step is
- batch size, which controls how many examples are processed before an update
- number of epochs, which controls how many times the model sees the training data
- regularisation strength, which helps reduce overfitting
- dropout rate, which randomly disables some neural network units during training
- maximum sequence length, which controls how much text is passed into the model
- vocabulary size or feature limit, especially for bag-of-words and TF-IDF models
- n-gram range, such as unigrams, bigrams, or trigrams
- number of hidden layers or hidden units in neural models
- optimiser choice, such as SGD, Adam, or AdamW

For logistic regression, important hyperparameters include the regularisation strength, penalty type, class weighting, solver, and maximum iterations.

For transformer models, important hyperparameters include learning rate, warmup steps, batch size, epochs, weight decay, maximum input length, and whether layers are frozen or fine-tuned.

## What are tokenisation, lemmatisation, and stemming, and how do they differ?

Tokenisation is the process of splitting text into smaller units called tokens. Tokens can be words, subwords, characters, or punctuation marks, depending on the tokenizer. For example, "I enjoyed the movie" can be tokenised into "I", "enjoyed", "the", and "movie".

Lemmatisation reduces a word to its dictionary form, called the lemma. It uses vocabulary and grammatical knowledge. For example, "running", "ran", and "runs" can be reduced to "run". Lemmatisation usually produces real words.

Stemming cuts words down to a root-like form using rules. It is faster and simpler than lemmatisation, but it can produce forms that are not real words. For example, "studies" might become "studi".

The main difference is:

- tokenisation splits text into units
- lemmatisation normalises words using linguistic knowledge
- stemming normalises words using crude rule-based trimming

Tokenisation is usually required before most NLP processing. Lemmatisation and stemming are optional preprocessing steps that can reduce vocabulary size and group related word forms.

## In finding probability of words in documents, how do we deal with word combinations not appearing in the test set? How is that same method used for Naive Bayes calculations of probability?

When a word or word combination has not appeared in the training data, its estimated probability can become zero. This is a problem because many probabilistic models multiply probabilities together. If one probability is zero, the whole calculation becomes zero.

The common solution is smoothing. The most common version is Laplace smoothing, also called add-one smoothing. Instead of giving unseen words a probability of zero, we add a small count to every possible word or n-gram.

For example, in Naive Bayes text classification, we estimate:

```text
P(word | class)
```

If a word never appeared in the training examples for a class, the unsmoothed probability would be zero. With smoothing, the formula becomes:

```text
P(word | class) = (count(word in class) + alpha) / (total words in class + alpha * vocabulary size)
```

Here, alpha is the smoothing value. If alpha is 1, it is Laplace smoothing. This gives unseen words a small non-zero probability and prevents the classifier from completely rejecting a class just because one word was unseen.

The same idea is used in n-gram language models. If a word combination such as a bigram or trigram has not appeared, smoothing or backoff methods assign it some probability rather than zero.

## Why was vector semantics introduced, and how does it replace edit distance to find word similarity?

Edit distance measures how many character-level changes are needed to turn one word into another. It is useful for spelling correction and string matching, but it does not understand meaning.

For example, "cat" and "bat" have a small edit distance, but they are not as semantically close as "cat" and "kitten". The words "car" and "automobile" have a large edit distance, but they can mean almost the same thing.

Vector semantics was introduced to represent meaning using numerical vectors. The core idea is distributional semantics: words that appear in similar contexts tend to have similar meanings. This is often summarised as "you shall know a word by the company it keeps."

In vector semantics, each word is represented as a point in a high-dimensional space. Similarity can be measured using cosine similarity or distance between vectors. Words with similar meanings should have vectors that point in similar directions.

Vector semantics improves on edit distance because it captures semantic similarity rather than just spelling similarity.

## How do we use logistic regression in classification of text?

To use logistic regression for text classification, we first convert text into numerical features. A common pipeline is:

1. Collect labelled text data.
2. Clean and preprocess the text if needed.
3. Tokenise the text.
4. Convert text into vectors using bag-of-words, n-grams, TF-IDF, or embeddings.
5. Train logistic regression on those vectors and labels.
6. Evaluate the model using accuracy, precision, recall, F1-score, or a confusion matrix.

Logistic regression estimates the probability that a text belongs to a class. For binary classification, it can estimate:

```text
P(class = positive | text)
```

For multi-class classification, it can estimate probabilities across several labels, such as positive, neutral, and negative.

In text classification, logistic regression works well because many tasks are strongly linked to word patterns. For example, in spam detection, words like "winner", "free", and "urgent" may increase the probability of the spam class.

## What is the different function required for a binomial comparison compared to a multinomial model?

For a binomial or binary classification problem, the model usually uses the sigmoid function. Sigmoid converts a score into a probability between 0 and 1:

```text
sigmoid(z) = 1 / (1 + e^-z)
```

This is used when there are two possible classes, such as spam or not spam.

For a multinomial or multi-class classification problem, the model usually uses the softmax function. Softmax converts multiple scores into a probability distribution across several classes:

```text
P(class i) = e^zi / sum(e^zj)
```

This is used when there are more than two mutually exclusive classes, such as positive, neutral, and negative.

So the key difference is:

- binary classification usually uses sigmoid
- multi-class classification usually uses softmax

## How were n-grams improved with LLMs?

Traditional n-gram models predict language using fixed-size word sequences. For example, a trigram model predicts the next word based on the previous two words. This is simple and useful, but it has major limits:

- it only sees a short context window
- it struggles with unseen word combinations
- it cannot deeply understand meaning
- it stores surface patterns rather than general language knowledge

LLMs improved on n-grams by using neural networks and attention mechanisms. Instead of relying only on fixed local word windows, transformer-based LLMs can consider much longer context and learn flexible representations of words, sentences, and documents.

LLMs also use embeddings, which allow similar words and phrases to have related representations. This means they can generalise better than n-gram models. If an LLM has learned a concept, it can often handle new wording that was not seen exactly during training.

In short, n-grams model local word sequence probabilities, while LLMs learn broader contextual and semantic patterns.

## How do you set up a RAG with a large set of documents?

RAG stands for Retrieval-Augmented Generation. It combines search with generation. Instead of asking a language model to rely only on its internal training data, we retrieve relevant documents and provide them as context.

A common setup is:

1. Collect the documents.
2. Clean and split the documents into chunks.
3. Create embeddings for each chunk.
4. Store the embeddings in a vector database or searchable index.
5. When a user asks a question, embed the question.
6. Retrieve the most relevant chunks using vector similarity.
7. Send the question and retrieved chunks to the language model.
8. Generate an answer grounded in the retrieved context.
9. Return citations or source links when possible.

For a large document set, chunking and metadata become very important. Each chunk should be small enough to retrieve accurately but large enough to preserve meaning. Metadata such as title, date, category, author, and source path helps filter retrieval results.

The system should also include evaluation. Good checks include whether retrieval finds the right source, whether the answer uses the source correctly, and whether the model admits when the answer is not in the documents.

## How do we fine-tune, and how is it a reduced form of training?

Fine-tuning means taking a pre-trained model and training it further on a smaller, task-specific dataset. The model already knows general language patterns from large-scale pretraining, so fine-tuning does not start from zero.

The process is usually:

1. Choose a pre-trained model.
2. Prepare a labelled dataset for the target task.
3. Format the data into the model's expected input and output structure.
4. Train the model for a smaller number of epochs with a lower learning rate.
5. Evaluate it on validation and test data.
6. Adjust hyperparameters if needed.

Fine-tuning is a reduced form of training because most of the expensive learning has already happened during pretraining. Instead of learning language from scratch, the model adapts its existing knowledge to a specific task, domain, tone, or output format.

Sometimes only part of the model is updated. For example, parameter-efficient fine-tuning methods such as LoRA update a small number of additional parameters rather than all model weights.

## How can discourse analysis improve a chatbot model?

Discourse analysis studies how meaning works across sentences and turns in a conversation. It looks at context, speaker intention, topic flow, references, and how earlier statements affect later ones.

For a chatbot, discourse analysis can improve:

- context tracking
- pronoun and reference resolution
- topic continuity
- turn-taking
- coherence across long conversations
- recognition of user intent
- handling of clarification questions

For example, if a user says "Tell me about BERT" and then asks "How is it different from GPT?", the chatbot needs to understand that "it" refers to BERT. Discourse analysis helps the system maintain that link.

It can also help the chatbot decide whether to answer directly, ask a clarifying question, summarise previous context, or correct a misunderstanding.

## What is the difference between a generative model and a discriminative model?

A discriminative model learns the boundary between classes. It models the probability of a label given the input:

```text
P(y | x)
```

For example, logistic regression and many classifiers are discriminative models. They are used to decide which class an input belongs to.

A generative model learns how the data itself is produced. It often models the joint probability:

```text
P(x, y)
```

or the probability of the input given a class:

```text
P(x | y)
```

Generative models can often create new examples, such as text, images, or speech. Naive Bayes is a classic generative classifier because it models how words are generated for each class. Modern LLMs are also generative because they generate text token by token.

The simple difference is:

- discriminative models classify
- generative models model or generate data

## What is the difference between a generative model and BERT for text-based models?

Many generative language models are trained to predict the next token from left to right. They are designed to produce text sequentially. GPT-style models are the common example.

BERT is different because it is an encoder-only transformer trained mainly with masked language modelling. During training, some words are hidden and BERT learns to predict the missing words using both left and right context.

This makes BERT very strong for understanding tasks, such as:

- text classification
- named entity recognition
- question answering
- semantic similarity
- sentiment analysis

Traditional BERT is not mainly designed for free-form text generation. It is better viewed as a text understanding model, while GPT-style models are better suited for generating fluent text.

So the difference is:

- GPT-style generative models predict and generate the next token
- BERT builds bidirectional representations for understanding text

## When training data is small, how can you improve your model?

When training data is small, the main risk is overfitting. The model may memorise the training examples instead of learning patterns that generalise.

Ways to improve the model include:

- use a simpler model as a baseline
- use transfer learning or a pre-trained model
- fine-tune carefully with a low learning rate
- use regularisation
- use dropout for neural models
- use data augmentation
- use cross-validation
- use class weighting if classes are imbalanced
- improve data quality and label consistency
- collect more representative examples if possible
- use semi-supervised learning or weak supervision
- freeze some model layers during fine-tuning

In NLP, pre-trained embeddings or transformer models can be especially useful because they bring general language knowledge from large datasets.

## Why do we get hallucinations when we seek creativity in LLMs?

LLMs generate text by predicting likely next tokens. They do not inherently know whether a statement is true unless the generation process is grounded in reliable context or checked against external sources.

When we ask for creativity, we often increase the model's freedom. Settings such as higher temperature can make outputs more varied and less predictable. This can be useful for brainstorming, storytelling, or idea generation, but it also increases the chance that the model will produce confident-sounding information that is not factual.

Hallucinations happen because the model is optimising for plausible language, not guaranteed truth. If the prompt asks for imaginative or open-ended output, the model may fill gaps with invented details.

Ways to reduce hallucinations include:

- provide source documents
- use RAG
- ask the model to cite evidence
- lower the temperature for factual tasks
- instruct the model to say when it does not know
- verify outputs with external tools or human review

The trade-off is that creativity benefits from freedom, while factual accuracy benefits from grounding and constraint.

## What ethical issues did you consider in your work?

Important ethical issues in NLP include privacy, bias, transparency, consent, and misuse.

For privacy, text data may contain personal information. It is important to remove or protect sensitive data, avoid exposing private messages, and follow data permissions.

For bias, NLP models can learn harmful patterns from training data. If a dataset contains stereotypes or unbalanced representation, the model may reproduce those patterns. Evaluation should check whether performance differs across groups.

For transparency, users should know when they are interacting with an AI system and what the model can or cannot do. The system should not pretend to be more certain than it is.

For consent and ownership, the data used for training or analysis should be used appropriately, especially if it comes from users, customers, or private communities.

For misuse, NLP systems can be used to generate spam, misinformation, impersonation, or manipulative content. Good design should include safeguards, monitoring, and clear boundaries.

In my own work, I would focus on using only appropriate data, avoiding private or sensitive content, checking for biased outputs, being honest about model limitations, and using the system for learning or helpful analysis rather than deception or harm.
