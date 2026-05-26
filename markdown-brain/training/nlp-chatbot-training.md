---
title: NLP Chatbot Training Knowledge Base
type: training-qa
status: active
memory_layer: training
approved: true
source: NLP_Chatbot.pdf
source_note: content/obsidian/Maxhoang.com.au/personal-chatbot-agent/nlp_chatbot_training.md
---

# NLP Chatbot Training Knowledge Base

Source: `NLP_Chatbot.pdf`

## Purpose

This file is designed to train a chatbot to answer common Natural Language Processing (NLP), machine learning, and chatbot-related questions in a more natural, human-style tone.

The chatbot should not sound like a textbook unless the user asks for a formal explanation. It should explain ideas simply, using friendly wording, short examples, and practical comparisons.

---

## Chatbot Answer Style Rules

Use these rules when answering questions from this knowledge base.

1. Answer in a natural, conversational way.
2. Keep the first answer short and easy to understand.
3. Use simple vocabulary before technical vocabulary.
4. Give a quick example when it helps.
5. Avoid sounding too academic unless the user asks for a formal definition.
6. If the user is a beginner, explain the concept like you are helping a friend.
7. Do not over-explain unless the user asks for more detail.
8. For technical terms, explain what it means and why it matters.
9. When comparing concepts, use simple contrasts such as “this creates new text” versus “this classifies text.”
10. If the user asks “what is X?”, start with a direct answer before adding details.

---

## Recommended Response Pattern

When answering, follow this structure:

```text
Simple answer first.
Then add one short example or practical use.
Add technical detail only if needed.
```

Example:

```text
Tokenisation is just breaking text into smaller pieces so a model can work with it. Usually that means splitting a sentence into words, but sometimes it splits words into smaller chunks too.
```

---

# Q&A Training Data

## Aspect-Based Sentiment Analysis

### Question
What is ABSA?

### Human-style answer
ABSA is basically sentiment analysis with more detail. Instead of just saying “this review is positive,” it figures out what the person liked and what they didn’t — like, the food was great but the service was awful.

### Formal answer
Aspect-Based Sentiment Analysis separates the opinion target from the opinion itself. Instead of labelling a whole review as positive or negative, it identifies which specific aspects, such as food or service, people liked or disliked.

### Keywords
ABSA, Aspect-Based Sentiment Analysis, sentiment analysis, review analysis, opinion mining

---

## Logistic Regression

### Question
What is logistic regression?

### Human-style answer
It’s a pretty simple classifier that gives you the probability of something belonging to a class. People use it a lot as a starting point before trying anything fancy.

### Formal answer
Logistic regression is a discriminative classifier that estimates the probability of a label given the input features. It is often used as a strong baseline for text classification with bag-of-words, TF-IDF, or embeddings.

### Keywords
logistic regression, classifier, baseline model, probability, text classification

---

## Hyperparameters

### Question
What are hyperparameters?

### Human-style answer
Think of them as the knobs you turn before training. Stuff like how fast the model learns or how many times it sees the data — you set them, the model doesn’t.

### Formal answer
Hyperparameters are settings chosen before or during training that control how a model learns, such as learning rate, batch size, epochs, dropout, and regularisation strength.

### Keywords
hyperparameters, learning rate, batch size, epochs, dropout, regularisation

---

## Tokenisation

### Question
What is tokenisation?

### Human-style answer
It’s just chopping text into pieces so the model can work with it. Usually into words, but sometimes into smaller chunks.

### Formal answer
Tokenisation is the process of splitting text into smaller units called tokens. Tokens can be words, subwords, characters, or punctuation marks.

### Keywords
tokenisation, tokens, text preprocessing, NLP preprocessing

---

## Lemmatisation

### Question
What is lemmatisation?

### Human-style answer
It turns different forms of a word back into the base form. So “ran,” “running,” and “runs” all become “run.”

### Formal answer
Lemmatisation reduces a word to its dictionary form using vocabulary and grammar. For example, “running,” “ran,” and “runs” all become “run.”

### Keywords
lemmatisation, lemma, base word, preprocessing, NLP

---

## Stemming

### Question
What is stemming?

### Human-style answer
Kind of a rough version of lemmatisation. It just chops off endings, so sometimes you get weird leftovers that aren’t real words.

### Formal answer
Stemming cuts words down to a root form using simple rules. It is faster than lemmatisation but may produce non-real words like “studi” from “studies.”

### Keywords
stemming, word root, preprocessing, NLP

---

## Smoothing

### Question
What is smoothing?

### Human-style answer
It’s a trick to stop your model freaking out when it sees a word it’s never seen before. You just give every word a tiny bit of probability so nothing’s ever zero.

### Formal answer
Smoothing gives unseen words or n-grams a small non-zero probability so probabilistic models do not collapse to zero when a word is missing from the training data.

### Keywords
smoothing, probability, unseen words, n-grams, Naive Bayes

---

## Laplace Smoothing

### Question
What is Laplace smoothing?

### Human-style answer
It’s the simplest type of smoothing — you just add 1 to every count. That way nothing has zero probability and your model doesn’t break on unseen words.

### Formal answer
Laplace smoothing, also called add-one smoothing, adds 1 to every word count so no word has zero probability. This prevents Naive Bayes from rejecting a class just because one word was unseen.

### Keywords
Laplace smoothing, add-one smoothing, Naive Bayes, probability

---

## Naive Bayes

### Question
What is Naive Bayes?

### Human-style answer
It’s an old-school classifier that just looks at how often words show up in each category. It assumes words don’t affect each other, which is naive but works surprisingly well.

### Formal answer
Naive Bayes is a generative classifier that uses Bayes’ theorem with the assumption that features are independent. It models how words are generated for each class.

### Keywords
Naive Bayes, Bayes theorem, classifier, text classification, generative model

---

## Vector Semantics

### Question
What is vector semantics?

### Human-style answer
Basically turning words into numbers so the computer can tell which words are similar. Words used in similar sentences end up close to each other.

### Formal answer
Vector semantics represents words as numerical vectors so meaning can be measured. Words used in similar contexts end up with similar vectors.

### Keywords
vector semantics, word vectors, embeddings, semantic similarity

---

## Cosine Similarity

### Question
What is cosine similarity?

### Human-style answer
It’s how you check if two word vectors point in the same direction. Closer to 1 means similar, closer to 0 means not really related.

### Formal answer
Cosine similarity measures similarity between two vectors based on the angle between them. It is commonly used to compare word or document embeddings.

### Keywords
cosine similarity, embeddings, vector comparison, similarity search

---

## Edit Distance

### Question
What is edit distance?

### Human-style answer
It’s how many letters you’d need to change to turn one word into another. Good for spellcheck, but it has no idea what the words actually mean.

### Formal answer
Edit distance is the number of character-level changes needed to turn one word into another. It is useful for spelling correction but does not capture meaning.

### Keywords
edit distance, spelling correction, character changes, NLP

---

## Bag-of-Words

### Question
What is bag-of-words?

### Human-style answer
You just count how many times each word shows up and ignore the order. Simple, but it loses a lot of context.

### Formal answer
Bag-of-words is a simple text representation that counts how often each word appears while ignoring grammar and word order.

### Keywords
bag-of-words, BoW, text representation, word count

---

## TF-IDF

### Question
What is TF-IDF?

### Human-style answer
It’s a way to figure out which words actually matter in a document. Common words like “the” get low scores, while rare meaningful ones get high scores.

### Formal answer
TF-IDF is a weighting scheme that scores words by how frequent they are in a document versus how rare they are across all documents. It helps highlight distinctive terms.

### Keywords
TF-IDF, term frequency, inverse document frequency, text features

---

## N-gram

### Question
What is an n-gram?

### Human-style answer
A chunk of n words in a row. Two-word chunks are bigrams, three-word chunks are trigrams — that’s pretty much it.

### Formal answer
An n-gram is a contiguous sequence of n words or tokens. For example, “natural language” is a bigram and “natural language processing” is a trigram.

### Keywords
n-gram, bigram, trigram, text sequence, tokens

---

## Sigmoid

### Question
What is sigmoid?

### Human-style answer
It squashes any number into a value between 0 and 1, so you can read it as a probability. Used when there are only two options.

### Formal answer
Sigmoid is a function that maps any number to a value between 0 and 1. It is used in binary classification to produce a probability.

### Keywords
sigmoid, binary classification, probability, activation function

---

## Softmax

### Question
What is softmax?

### Human-style answer
Like sigmoid but for more than two classes. It spreads probability across all the options so they add up to 1.

### Formal answer
Softmax converts multiple scores into a probability distribution across several classes. It is used for multi-class classification.

### Keywords
softmax, multi-class classification, probability distribution

---

## Large Language Model

### Question
What is an LLM?

### Human-style answer
It’s a really big AI model trained on tons of text. ChatGPT, Claude, and Gemini — those are all LLMs.

### Formal answer
A Large Language Model is a neural network trained on huge amounts of text that uses attention and embeddings to understand and generate language.

### Keywords
LLM, Large Language Model, ChatGPT, Claude, Gemini, language model

---

## Embedding

### Question
What is an embedding?

### Human-style answer
It’s a list of numbers that captures what a word or sentence means. Similar things end up with similar numbers.

### Formal answer
An embedding is a dense numerical vector that represents the meaning of a word, sentence, or document in a way models can compare and learn from.

### Keywords
embedding, vector, semantic meaning, sentence embedding, word embedding

---

## Attention

### Question
What is attention?

### Human-style answer
It’s how the model figures out which words in a sentence matter most when answering. Kind of like highlighting the important bits before responding.

### Formal answer
Attention is a mechanism that lets a model weigh the importance of different tokens in the input when producing an output. It helps the model understand long-range context.

### Keywords
attention, transformer, context, tokens, NLP

---

## Transformer

### Question
What is a transformer?

### Human-style answer
It’s the model design behind almost every modern AI you’ve heard of — GPT, BERT, Claude. It’s fast because it looks at all the words at once instead of one by one.

### Formal answer
A transformer is a neural network architecture built on attention that processes sequences in parallel and powers most modern LLMs like GPT and BERT.

### Keywords
transformer, attention, GPT, BERT, neural network

---

## RAG

### Question
What is RAG?

### Human-style answer
It’s when you let the AI search through your documents first, then answer based on what it found. Way better for company-specific or factual stuff.

### Formal answer
Retrieval-Augmented Generation combines search with generation. Relevant documents are retrieved and passed to an LLM as grounded context.

### Keywords
RAG, Retrieval-Augmented Generation, vector database, retrieval, chatbot

---

## Chunking

### Question
What is chunking?

### Human-style answer
Breaking up long documents into smaller pieces so the AI can search them properly. If chunks are too big or too small, RAG starts giving weird answers.

### Formal answer
Chunking splits documents into smaller pieces so they can be embedded and retrieved accurately in a RAG system.

### Keywords
chunking, RAG, document chunks, embeddings, retrieval

---

## Vector Database

### Question
What is a vector database?

### Human-style answer
It’s a database that’s good at finding stuff by meaning rather than exact keywords. RAG systems rely on these to pull up relevant content fast.

### Formal answer
A vector database stores embeddings and allows fast similarity search. It is used to retrieve relevant chunks in RAG pipelines.

### Keywords
vector database, embeddings, similarity search, RAG, semantic search

---

## Fine-Tuning

### Question
What is fine-tuning?

### Human-style answer
You take a model that already knows a lot and train it a bit more on your own data so it gets better at your specific task.

### Formal answer
Fine-tuning takes a pre-trained model and trains it further on a smaller task-specific dataset so it adapts to a specific task, domain, or tone.

### Keywords
fine-tuning, pre-trained model, training data, domain adaptation

---

## Pretraining

### Question
What is pretraining?

### Human-style answer
It’s the first big training round where the model learns language in general. After that, you can fine-tune it for whatever you actually need.

### Formal answer
Pretraining is the initial large-scale training phase where a model learns general language patterns from huge text datasets before being fine-tuned.

### Keywords
pretraining, language model, training, fine-tuning

---

## LoRA

### Question
What is LoRA?

### Human-style answer
A cheap way to fine-tune a model without retraining the whole thing. You only update a small extra layer, which saves heaps of time and money.

### Formal answer
LoRA is a parameter-efficient fine-tuning method that updates a small number of additional parameters instead of all the model’s weights.

### Keywords
LoRA, fine-tuning, parameter-efficient fine-tuning, adapters

---

## Transfer Learning

### Question
What is transfer learning?

### Human-style answer
It’s when you reuse a model that already learned something useful, instead of starting from scratch. Super handy when you don’t have much data.

### Formal answer
Transfer learning reuses a model trained on one task as the starting point for another. It is especially helpful when there is limited training data.

### Keywords
transfer learning, pre-trained model, fine-tuning, machine learning

---

## Discourse Analysis

### Question
What is discourse analysis?

### Human-style answer
It’s about understanding how a conversation flows — like knowing “it” refers to something said three messages ago. Helps chatbots not sound dumb.

### Formal answer
Discourse analysis studies how meaning works across sentences and turns in a conversation, including context, references, intent, and topic flow.

### Keywords
discourse analysis, conversation flow, context, references, chatbot

---

## Generative Model

### Question
What is a generative model?

### Human-style answer
It’s a model that can create new stuff — text, images, whatever. LLMs are generative because they actually write new sentences.

### Formal answer
A generative model learns how data is produced and can create new examples, such as LLMs generating text token by token.

### Keywords
generative model, LLM, text generation, AI generation

---

## Discriminative Model

### Question
What is a discriminative model?

### Human-style answer
It’s a model that just sorts things into categories. It doesn’t create new stuff, it just decides what something is.

### Formal answer
A discriminative model learns the boundary between classes by modelling P(y|x). It is used to decide which class an input belongs to.

### Keywords
discriminative model, classification, classifier, P(y|x)

---

## BERT

### Question
What is BERT?

### Human-style answer
It’s a model from Google that’s really good at understanding text. It reads in both directions, so it picks up context better than older models.

### Formal answer
BERT is an encoder-only transformer trained with masked language modelling. It uses both left and right context, making it strong for understanding tasks.

### Keywords
BERT, transformer, masked language modelling, encoder, NLP

---

## GPT

### Question
What is GPT?

### Human-style answer
It’s the model family from OpenAI. It predicts the next word, then the next, then the next — that’s how it writes.

### Formal answer
GPT is a generative transformer that predicts the next token from left to right and is designed for fluent text generation.

### Keywords
GPT, generative transformer, OpenAI, next-token prediction

---

## Masked Language Modelling

### Question
What is masked language modelling?

### Human-style answer
It’s like training the model with fill-in-the-blank exercises. You hide some words and make the model guess them.

### Formal answer
Masked language modelling is a training method where some words are hidden and the model learns to predict them from surrounding context. It is used to train BERT.

### Keywords
masked language modelling, BERT, fill-in-the-blank, training

---

## Overfitting

### Question
What is overfitting?

### Human-style answer
It’s when your model basically memorises the training data and then bombs on anything new. Like a student who only studies the practice test.

### Formal answer
Overfitting happens when a model memorises training examples instead of learning general patterns, causing it to perform poorly on new data.

### Keywords
overfitting, generalisation, training data, model performance

---

## Regularisation

### Question
What is regularisation?

### Human-style answer
It’s a way to stop your model from getting too obsessed with the training data. Keeps it simpler so it generalises better.

### Formal answer
Regularisation uses techniques that discourage overly complex models to reduce overfitting, such as L1/L2 penalties or weight decay.

### Keywords
regularisation, overfitting, L1, L2, weight decay

---

## Dropout

### Question
What is dropout?

### Human-style answer
During training you randomly switch off some parts of the network, which forces it to not rely too heavily on any one thing. Helps prevent overfitting.

### Formal answer
Dropout randomly disables some neural network units during training to prevent overfitting.

### Keywords
dropout, neural network, overfitting, regularisation

---

## Data Augmentation

### Question
What is data augmentation?

### Human-style answer
When you don’t have enough data, you make more by tweaking what you have. For text, that might mean swapping synonyms or rephrasing sentences.

### Formal answer
Data augmentation creates additional training examples by modifying existing ones. For text, this can include synonym swaps, back-translation, or paraphrasing.

### Keywords
data augmentation, training data, paraphrasing, synonym swap, back-translation

---

## Cross-Validation

### Question
What is cross-validation?

### Human-style answer
Instead of testing your model once, you split the data into chunks and test it multiple times. Gives you a much more honest score.

### Formal answer
Cross-validation splits data into multiple folds and trains/tests across them to get a more reliable estimate of model performance.

### Keywords
cross-validation, folds, model evaluation, testing

---

## Hallucination

### Question
What is a hallucination?

### Human-style answer
It’s when an AI just makes stuff up but says it really confidently. Happens a lot, which is why you should double-check important facts.

### Formal answer
A hallucination happens when an LLM produces confident-sounding output that is not factually true because it is optimising for plausible language rather than verified truth.

### Keywords
hallucination, LLM, AI error, factual accuracy

---

## Temperature

### Question
What is temperature?

### Human-style answer
It controls how creative or random the model gets. Low temp = boring and predictable, high temp = wild and weird.

### Formal answer
Temperature is a setting that controls randomness in LLM output. Higher values give more creative and varied responses, while lower values give more focused and factual ones.

### Keywords
temperature, LLM settings, randomness, creativity

---

## Memory in Chatbots

### Question
What is memory in chatbots?

### Human-style answer
It’s when the chatbot remembers things you said earlier — either in the same chat or across different sessions. Way more useful than starting fresh every time.

### Formal answer
Memory is the ability of a chatbot to retain information across turns or sessions so it can reference past context, user preferences, or earlier conversations.

### Keywords
chatbot memory, conversation memory, user preferences, context

---

## Intent

### Question
What is intent?

### Human-style answer
It’s what the user actually wants. Like if someone says “I’m hungry,” the intent might be “find food nearby,” not just stating a fact.

### Formal answer
Intent is what the user is actually trying to accomplish with a message. A chatbot tries to identify intent so it can give the right response.

### Keywords
intent, user intent, chatbot, NLU, natural language understanding

---

## Bias in NLP

### Question
What is bias in NLP?

### Human-style answer
It’s when the model picks up unfair or stereotyped patterns from its training data. Bad data in, biased outputs out.

### Formal answer
Bias in NLP happens when models learn and reproduce harmful patterns from training data, such as stereotypes or unequal performance across demographic groups.

### Keywords
bias, NLP ethics, stereotypes, unfairness, training data

---

## Privacy in NLP

### Question
What is privacy in NLP?

### Human-style answer
It’s about not exposing people’s personal info in your data. Things like names, emails, or private chats should be cleaned out before training.

### Formal answer
Privacy in NLP means protecting personal or sensitive information in text data through removal, anonymisation, and proper data permissions.

### Keywords
privacy, NLP ethics, personal information, anonymisation, data protection

---

# Chatbot Behaviour Examples

## Example 1

### User
What is RAG?

### Good chatbot answer
RAG is when the AI searches through your documents first, then answers based on what it found. It’s useful when you want the chatbot to answer from your own files instead of guessing from general knowledge.

---

## Example 2

### User
What is tokenisation?

### Good chatbot answer
Tokenisation means breaking text into smaller pieces so the model can process it. For example, a sentence can be split into words, punctuation, or smaller word parts.

---

## Example 3

### User
What is hallucination?

### Good chatbot answer
A hallucination is when an AI makes something up but says it confidently. That’s why important answers should be checked against reliable sources or your own documents.

---

# Extra Training Instructions for the Chatbot

When the chatbot does not know the answer:

```text
I’m not fully sure from the information I have, but here’s the closest explanation. You may want to check the source material if this is for an assignment or formal report.
```

When the user asks for a more academic answer:

```text
In formal terms, [concept] means...
```

When the user asks for a simple answer:

```text
Simple version: [plain explanation].
```

When the user asks for an example:

```text
For example, [short practical example].
```

---

# Suggested Metadata for RAG Systems

Use this format if storing the content in a vector database:

```json
{
  "source": "NLP_Chatbot.pdf",
  "category": "NLP chatbot Q&A",
  "tone": "human-style beginner-friendly explanation",
  "content_type": "training_qa",
  "language": "English"
}
```

---

# Notes for Implementation

For chatbot training or RAG embedding:

- Embed each Q&A section as a separate chunk.
- Keep the question, human-style answer, formal answer, and keywords together.
- Prioritise the human-style answer when the user asks casually.
- Use the formal answer when the user asks for academic wording.
- Use keywords to improve retrieval matching.
- Keep chunk sizes small so the chatbot retrieves the right concept accurately.
