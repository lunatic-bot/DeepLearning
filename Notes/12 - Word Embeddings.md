# What are Word Embeddings?

A **Word Embedding** is a dense numerical vector representation of words that captures their semantic meaning and relationships.

Instead of representing words as IDs or sparse vectors, embeddings map words into a continuous vector space.

Example:

```text
King   → [0.25, -0.61, 0.81, ...]
Queen  → [0.22, -0.58, 0.79, ...]
Apple  → [-0.72, 0.11, 0.05, ...]
```

Words with similar meanings have vectors that are close together.

---

# Why do we need Word Embeddings?

Computers cannot understand text directly.

Consider:

```text
Cat
Dog
Lion
```

If we assign IDs:

```text
Cat  = 1
Dog  = 2
Lion = 3
```

The model may incorrectly think:

```text
Lion > Dog > Cat
```

because IDs have no semantic meaning.

Embeddings solve this problem.

---

# Evolution of Word Representation

```text
Text
 ↓
Integer Encoding
 ↓
One-Hot Encoding
 ↓
Word Embeddings
 ↓
Contextual Embeddings (BERT)
```

---

# 1. One-Hot Encoding (Predecessor)

Vocabulary:

```text
[cat, dog, lion]
```

Representations:

```text
cat  = [1,0,0]
dog  = [0,1,0]
lion = [0,0,1]
```

### Problems

* Huge sparse vectors
* No semantic meaning
* Similar words appear unrelated

Example:

```text
cat × dog similarity = 0
```

---

# Traditional Word Embeddings

These generate **one fixed vector per word**.

---

# 2. Word2Vec

Developed by Google.

Most famous embedding technique.

---

## Idea

Words appearing in similar contexts have similar meanings.

Example:

```text
I drink coffee every morning.
I drink tea every morning.
```

The model learns:

```text
coffee ≈ tea
```

---

## Two Architectures

### CBOW (Continuous Bag of Words)

Predict center word from surrounding words.

Example:

```text
I ___ coffee every morning
```

Predict:

```text
drink
```

---

### Skip-Gram

Predict surrounding words from center word.

Example:

```text
drink
```

Predict:

```text
I, coffee, every, morning
```

---

## Advantages

✅ Captures semantic relationships

✅ Small and efficient

✅ Fast training

---

## Disadvantages

❌ One meaning per word

```text
bank (river)
bank (finance)
```

Same vector.

---

# 3. GloVe (Global Vectors)

Developed by Stanford University.

Combines:

* Global statistics
* Local context

---

## Idea

Uses word co-occurrence counts.

Example:

```text
ice and steam
```

co-occur differently with:

```text
solid
gas
water
```

The model learns relationships from these statistics.

---

## Advantages

✅ Captures global word relationships

✅ Strong semantic representation

---

## Disadvantages

❌ Fixed embeddings

❌ Cannot handle context

---

# 4. FastText

Developed by Meta.

Improvement over Word2Vec.

---

## Idea

Represent words using character n-grams.

Example:

```text
playing
```

Subwords:

```text
pla
lay
ayi
ying
```

---

## Advantage

Can understand unseen words.

Example:

```text
playing
played
player
```

share subword information.

---

## Advantages

✅ Handles rare words

✅ Handles misspellings

✅ Better morphology understanding

---

## Disadvantages

❌ Larger model size

❌ Slower than Word2Vec

---

# Contextual Word Embeddings

Traditional embeddings:

```text
bank → one vector
```

regardless of context.

Modern models fix this.

---

# 5. ELMo

Developed by Allen Institute for AI.

Uses Bi-LSTM.

Produces different vectors depending on context.

Example:

```text
river bank
```

and

```text
bank account
```

get different embeddings.

---

# 6. BERT Embeddings

Produced by BERT.

Current generation contextual embeddings.

Example:

```text
I sat on the bank.
```

vs

```text
I deposited money in the bank.
```

Different embeddings for "bank".

---

## Advantages

✅ Context-aware

✅ State-of-the-art performance

✅ Better semantic understanding

---

## Disadvantages

❌ Large models

❌ Computationally expensive

---

# How Embeddings are Used in Deep Learning

Deep learning models cannot process raw text.

Pipeline:

```text
Text
 ↓
Tokenization
 ↓
Word Embedding
 ↓
Neural Network
 ↓
Prediction
```

---

## Example

Sentence:

```text
I love AI
```

After embedding:

```text
I    → [0.1, 0.3, ...]
love → [0.7, 0.5, ...]
AI   → [0.9, 0.2, ...]
```

Matrix:

```text
[
 [0.1,0.3,...]
 [0.7,0.5,...]
 [0.9,0.2,...]
]
```

Input to:

* RNN
* LSTM
* GRU
* CNN for text
* Transformers

---

# Embedding Layer in Deep Learning

Example:

```python
Embedding(
    input_dim=vocab_size,
    output_dim=300
)
```

Meaning:

```text
Vocabulary Size = 50,000
Embedding Dimension = 300
```

Output:

```text
Each word → 300-dimensional vector
```

---

# Advantages of Word Embeddings

### Semantic Understanding

```text
King ≈ Queen
Car ≈ Vehicle
```

---

### Dense Representation

Instead of huge sparse vectors.

---

### Better Generalization

Similar words have similar vectors.

---

### Reduced Dimensionality

Much smaller than one-hot encoding.

---

### Transfer Learning

Pretrained embeddings can be reused.

---

# Disadvantages of Traditional Embeddings

### Polysemy Problem

```text
bank
```

Multiple meanings but one vector.

---

### Out-of-Vocabulary (OOV)

Unknown words not represented well.

---

### Static Meaning

Word meaning doesn't change with context.

---

# Traditional vs Contextual Embeddings

| Feature             | Word2Vec/GloVe | BERT |
| ------------------- | -------------- | ---- |
| One Vector Per Word | Yes            | No   |
| Context Aware       | No             | Yes  |
| Handles Polysemy    | No             | Yes  |
| Computational Cost  | Low            | High |

---

# Most Important Interview Questions

## Basic

### 1. What are word embeddings?

Dense vector representations of words that capture semantic meaning and relationships.

---

### 2. Why are embeddings better than one-hot encoding?

* Lower dimensionality
* Semantic similarity
* Better learning

---

### 3. What is the distributional hypothesis?

> Words appearing in similar contexts tend to have similar meanings.

This is the foundation of Word2Vec.

---

### 4. What is the embedding dimension?

The size of the vector used to represent each word.

Example:

```text
100, 200, 300 dimensions
```

---

## Intermediate

### 5. Difference between CBOW and Skip-Gram?

| CBOW                      | Skip-Gram             |
| ------------------------- | --------------------- |
| Context → Word            | Word → Context        |
| Faster                    | Slower                |
| Better for frequent words | Better for rare words |

---

### 6. Difference between Word2Vec and GloVe?

**Word2Vec**

* Local context-based

**GloVe**

* Global co-occurrence statistics

---

### 7. What problem does FastText solve?

Out-of-vocabulary and rare-word handling using subword information.

---

### 8. Why is BERT better than Word2Vec?

BERT generates context-dependent embeddings.

---

## Advanced

### 9. What is polysemy?

A word having multiple meanings.

Example:

```text
bank
```

---

### 10. Why are contextual embeddings important?

Because the meaning of words depends on surrounding words.

---

### 11. How are embeddings trained?

By learning vectors that minimize prediction error in tasks like:

* next-word prediction
* context prediction
* masked language modeling

---

### 12. Can embeddings capture analogies?

Yes.

Famous example:

```text
King - Man + Woman ≈ Queen
```

---

# Interview One-Liner

> Word embeddings are dense vector representations of words that capture semantic and syntactic relationships. Traditional methods like Word2Vec, GloVe, and FastText learn fixed embeddings, while modern approaches like BERT generate context-aware embeddings that significantly improve NLP performance.
