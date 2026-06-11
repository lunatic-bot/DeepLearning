# What are Encoders and Decoders?

Encoders and Decoders are neural network components used in **Sequence-to-Sequence (Seq2Seq)** tasks where one sequence is converted into another sequence.

Examples:

```text
English → French Translation
Speech → Text
Text → Summary
Question → Answer
```

---

# Real-Life Example

Input:

```text
I love machine learning
```

Output:

```text
J'aime l'apprentissage automatique
```

Here:

* Encoder reads the English sentence
* Decoder generates the French sentence

---

# Encoder

The Encoder's job is:

```text
Input Sequence
      ↓
Understand Meaning
      ↓
Generate Context Vector
```

Example:

```text
I
love
machine
learning
```

Process:

```text
Word1 → h1
Word2 → h2
Word3 → h3
Word4 → h4
```

Final hidden state:

```text
h4
```

contains information about the entire sentence.

---

## Encoder Output

Traditionally:

```text
Sentence
↓
Encoder
↓
Context Vector
```

The context vector is a compressed representation of the input sequence.

---

# Decoder

The Decoder's job is:

```text
Context Vector
      ↓
Generate Output Sequence
```

Example:

```text
Context Vector
↓
J'
↓
aime
↓
l'apprentissage
↓
automatique
```

The decoder predicts one word at a time.

---

# Seq2Seq Architecture

```text
Input Sentence
      ↓
   Encoder
      ↓
Context Vector
      ↓
   Decoder
      ↓
Output Sentence
```

---

# Example of Translation

Input:

```text
I am happy
```

Encoder:

```text
I → h1
am → h2
happy → h3
```

Final state:

```text
Context Vector
```

Decoder:

```text
<sos>
↓
Je
↓
suis
↓
heureux
↓
<eos>
```

---

# Why were Encoder-Decoders Introduced?

Traditional RNNs:

```text
Input
↓
Output
```

could not easily handle:

```text
Variable Length Input
↓
Variable Length Output
```

Examples:

```text
English sentence length = 5
French sentence length = 8
```

Encoder-Decoders solve this.

---

# Encoder Types

### RNN Encoder

Uses vanilla RNN.

Problems:

* Vanishing gradients
* Poor long-term memory

---

### LSTM Encoder

Uses memory cells.

Advantages:

* Better long-term dependencies

---

### GRU Encoder

Simpler than LSTM.

Advantages:

* Faster training
* Fewer parameters

---

### Transformer Encoder

Used in modern NLP.

Examples:

* BERT
* T5

---

# Decoder Types

### RNN Decoder

Generates output sequentially.

---

### LSTM Decoder

Handles longer sequences better.

---

### Transformer Decoder

Used in:

* GPT
* BART

---

# Major Problem of Basic Encoder-Decoder

## Fixed-Length Context Vector Bottleneck

Traditional Seq2Seq compresses the entire sentence into a single vector.

```text
Long Sentence
↓
One Vector
↓
Decoder
```

Imagine:

```text
100-word paragraph
↓
One vector
```

Important information gets lost.

---

# Example

Input:

```text
The weather today in Bangalore is pleasant and suitable for outdoor activities...
```

Everything is compressed into one vector.

Result:

```text
Information Loss
```

---

# Attention Mechanism: The Solution

Instead of relying on one context vector:

```text
Decoder
↓
Looks at all encoder states
```

This is called **Attention**.

---

## Without Attention

```text
Encoder
↓
Single Context Vector
↓
Decoder
```

---

## With Attention

```text
Encoder States
h1 h2 h3 h4 h5
 ↓ ↓ ↓ ↓ ↓
Attention
 ↓
Decoder
```

Now the decoder can focus on relevant words.

---

# Example

Input:

```text
The cat sat on the mat
```

When generating:

```text
cat
```

Attention focuses on:

```text
The CAT sat on the mat
```

rather than the whole sentence equally.

---

# Problems with RNN Encoder-Decoders

## 1. Vanishing Gradient

Long sequences are hard to learn.

---

## 2. Sequential Processing

Cannot process words in parallel.

```text
Word1
↓
Word2
↓
Word3
```

Training is slow.

---

## 3. Long-Term Dependency Problem

Earlier words may be forgotten.

Example:

```text
The movie released in 1998...
...
...
What year?
```

The model may forget "1998".

---

## 4. Context Bottleneck

Entire sequence compressed into one vector.

---

# Transformer: The Modern Solution

Transformers remove recurrence.

Use:

```text
Self-Attention
```

Benefits:

* Parallel processing
* Better long-range dependencies
* Faster training
* Higher accuracy

---

# Encoder vs Decoder in Transformers

## Encoder-Only Models

Examples:

* BERT

Tasks:

* Classification
* Sentiment Analysis
* NER

---

## Decoder-Only Models

Examples:

* GPT

Tasks:

* Text Generation
* Chatbots

---

## Encoder-Decoder Models

Examples:

* T5
* BART

Tasks:

* Translation
* Summarization
* Question Answering

---

# Important Interview Questions

## Basic

### 1. What is an Encoder?

> A neural network component that reads an input sequence and converts it into a meaningful representation (context vector or hidden states).

---

### 2. What is a Decoder?

> A neural network component that generates an output sequence from the encoder's representation.

---

### 3. What is Seq2Seq?

> A sequence-to-sequence architecture where an encoder processes an input sequence and a decoder generates an output sequence.

---

### 4. Give applications of Encoder-Decoder models.

* Machine Translation
* Text Summarization
* Chatbots
* Speech Recognition

---

## Intermediate

### 5. What is the Context Vector?

> The compressed representation of the input sequence produced by the encoder.

---

### 6. Why is the Context Vector a bottleneck?

> Long sequences must be compressed into a single vector, causing information loss.

---

### 7. What is Attention?

> A mechanism that allows the decoder to focus on relevant encoder states instead of relying on a single context vector.

---

### 8. Why was Attention introduced?

> To overcome the fixed-length context vector bottleneck and improve performance on long sequences.

---

## Advanced

### 9. Difference between RNN Encoder-Decoder and Transformer?

| RNN Seq2Seq                    | Transformer         |
| ------------------------------ | ------------------- |
| Sequential                     | Parallel            |
| Slow                           | Fast                |
| Suffers long-term dependencies | Handles them better |
| Uses recurrence                | Uses self-attention |

---

### 10. Difference between Encoder-only, Decoder-only, and Encoder-Decoder models?

| Type            | Example | Usage          |
| --------------- | ------- | -------------- |
| Encoder-only    | BERT    | Understanding  |
| Decoder-only    | GPT     | Generation     |
| Encoder-Decoder | T5      | Transformation |

---

# Interview One-Liner

> An Encoder-Decoder architecture is a sequence-to-sequence framework where the encoder converts an input sequence into a learned representation and the decoder generates the target sequence from that representation. Traditional RNN-based encoder-decoders suffer from context bottlenecks and long-term dependency issues, which are largely solved by attention mechanisms and Transformer architectures.
