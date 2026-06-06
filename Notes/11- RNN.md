# Recurrent Neural Networks (RNN)

A **Recurrent Neural Network (RNN)** is a type of neural network designed to work with **sequential data**, where the order of inputs matters.

Unlike traditional neural networks, RNNs have a **memory** that allows them to use information from previous inputs while processing the current input.

---

# Why do we need RNNs?

Consider a sentence:

```text
"I grew up in France and I speak fluent ____."
```

To predict the missing word, the model needs context from earlier words.

A traditional neural network treats each input independently and cannot remember previous words.

RNNs solve this by maintaining a hidden state (memory).

---

# Where are RNNs Used?

### Natural Language Processing (NLP)

* Language Translation
* Text Generation
* Sentiment Analysis
* Chatbots

Example:

```text
I love this movie.
```

Predict:

```text
Positive Sentiment
```

---

### Time Series Forecasting

* Stock Prices
* Weather Forecasting
* Sales Prediction

---

### Speech Recognition

Convert:

```text
Audio → Text
```

---

### Sequence Prediction

Examples:

* Next word prediction
* Auto-complete
* Machine Translation

---

# How RNN Works

Traditional Neural Network:

```text
Input → Output
```

RNN:

```text
Input_t
   ↓
Hidden State_t
   ↓
Output_t

Hidden State_t
   ↓
Hidden State_(t+1)
```

The hidden state carries information forward.

---

# Example

Sentence:

```text
I love deep learning
```

Processing:

```text
I      → hidden state h1
love   → hidden state h2
deep   → hidden state h3
learning → hidden state h4
```

Each word is processed using:

* Current input
* Previous hidden state

---

# RNN Architecture

At time step t:

Current hidden state:

h_t=f(W_hh_{t-1}+W_xx_t+b)

Output:

y_t=W_yh_t+b_y

Where:

* (x_t) = current input
* (h_t) = hidden state
* (y_t) = output

---

# Types of RNN Architectures

## 1. One-to-One

```text
Image → Label
```

Example:

```text
Cat Image → Cat
```

(Not typically called an RNN use case)

---

## 2. One-to-Many

```text
Image → Sentence
```

Example:

```text
Image Captioning
```

---

## 3. Many-to-One

```text
Words → Sentiment
```

Example:

```text
"This movie is amazing"
↓
Positive
```

---

## 4. Many-to-Many

```text
English Sentence
↓
French Sentence
```

Example:

Machine Translation

---

# Advantages of RNN

### Handles Sequential Data

Order matters.

```text
Dog bites man
```

vs

```text
Man bites dog
```

Different meanings.

---

### Memory of Previous Inputs

Can use past context.

---

### Variable Length Inputs

Works with:

* Short sentences
* Long documents

---

# Problems with Vanilla RNN

## 1. Vanishing Gradient Problem

During backpropagation:

```text
Gradients become very small
```

Earlier information gets forgotten.

Example:

```text
I grew up in France ...
...
...
I speak fluent French
```

The word "France" may be forgotten.

---

## 2. Exploding Gradient Problem

Gradients become extremely large.

Training becomes unstable.

---

# Solution: LSTM and GRU

Because vanilla RNNs struggle with long sequences, newer architectures were introduced:

### LSTM

Uses gates to remember important information.

---

### GRU

Simpler and faster version of LSTM.

---

# RNN vs CNN

| Feature                 | CNN                  | RNN               |
| ----------------------- | -------------------- | ----------------- |
| Best For                | Images               | Sequential Data   |
| Memory                  | No                   | Yes               |
| Handles Time Dependency | No                   | Yes               |
| Example                 | Image Classification | Language Modeling |

---

# RNN vs LSTM

| Feature                       | RNN        | LSTM      |
| ----------------------------- | ---------- | --------- |
| Memory                        | Short-Term | Long-Term |
| Vanishing Gradient            | Severe     | Reduced   |
| Performance on Long Sequences | Poor       | Good      |

---

# Real-World Examples

### Google Translate (older systems)

```text
English → French
```

Used encoder-decoder RNNs before Transformers became dominant.

---

### Next Word Prediction

Input:

```text
I love machine
```

Output:

```text
learning
```

---

### Stock Price Prediction

Use previous prices to predict future prices.

---

# Important Interview Questions

## Basic

### 1. What is RNN?

**Answer:**

An RNN is a neural network designed for sequential data that maintains a hidden state to capture information from previous inputs.

---

### 2. Why do we need RNNs?

Because traditional neural networks cannot capture dependencies between sequential inputs.

---

### 3. What is the hidden state?

The hidden state is the memory of the network that carries information from previous time steps.

---

### 4. Give applications of RNN.

* Language Translation
* Sentiment Analysis
* Speech Recognition
* Time-Series Forecasting
* Text Generation

---

## Intermediate

### 5. What is Backpropagation Through Time (BPTT)?

A variation of backpropagation used to train RNNs by unfolding the network across time steps.

---

### 6. Why do RNNs suffer from vanishing gradients?

Because gradients are repeatedly multiplied during backpropagation, causing them to shrink exponentially.

---

### 7. What is exploding gradient?

When gradients grow exponentially during backpropagation, leading to unstable training.

---

### 8. How can exploding gradients be handled?

Using gradient clipping.

---

### 9. What are the limitations of vanilla RNNs?

* Vanishing gradients
* Difficulty learning long-term dependencies
* Slow sequential computation

---

## Advanced

### 10. Why was LSTM introduced?

To solve the long-term dependency and vanishing gradient problems in RNNs.

---

### 11. Difference between RNN and LSTM?

RNN stores short-term information, while LSTM uses memory cells and gates to retain long-term information.

---

### 12. Difference between LSTM and GRU?

GRU is simpler, has fewer parameters, and trains faster; LSTM has separate memory cells and often captures complex dependencies better.

---

### 13. Why are Transformers replacing RNNs?

Because Transformers:

* Process sequences in parallel
* Handle long-range dependencies better
* Train faster on modern hardware

Examples include:

* BERT
* GPT

---

# Interview One-Liner

> RNNs are neural networks designed for sequential data that maintain a hidden state (memory) to capture information from previous inputs, making them suitable for tasks such as language modeling, speech recognition, and time-series forecasting. Their main limitation is difficulty learning long-term dependencies, which led to the development of LSTM and GRU architectures.



# Backpropagation Through Time (BPTT)

**Backpropagation Through Time (BPTT)** is the training algorithm used for **Recurrent Neural Networks (RNNs)**.

It is an extension of regular backpropagation that works on sequential data.

---

# Why do we need BPTT?

In a normal neural network:

```text
Input → Hidden → Output
```

We use backpropagation once to update weights.

But in an RNN:

```text
x1 → h1 → y1
      ↓
x2 → h2 → y2
      ↓
x3 → h3 → y3
```

The current hidden state depends on the previous hidden state.

So errors must be propagated not only through layers but also **through time steps**.

This is exactly what BPTT does.

---

# Key Idea

An RNN reuses the same weights at every time step.

Example sequence:

```text
"I love deep learning"
```

Unrolled RNN:

```text
x1 --> h1 --> y1
       |
x2 --> h2 --> y2
       |
x3 --> h3 --> y3
       |
x4 --> h4 --> y4
```

The same weight matrices are used repeatedly:

```text
Wx  → Input-to-hidden weights
Wh  → Hidden-to-hidden weights
Wy  → Hidden-to-output weights
```

---

# Step 1: Forward Pass

Process the sequence from left to right.

For each time step:

h_t=f(W_xx_t+W_hh_{t-1}+b)

Output:

y_t=W_yh_t+b_y

Compute total loss:

L=L_1+L_2+L_3+\cdots+L_T

---

# Step 2: Unroll the RNN

BPTT first converts the RNN into an equivalent deep network across time.

Example:

```text
Time 1      Time 2      Time 3

x1 → h1 → y1
      ↓
x2 → h2 → y2
      ↓
x3 → h3 → y3
```

becomes:

```text
x1 → h1 → h2 → h3
```

Now it looks like a deep neural network.

---

# Step 3: Backward Pass

Error is propagated backward:

```text
L3 → h3
     ↓
L2 → h2
     ↓
L1 → h1
```

The gradients flow backwards through all previous time steps.

---

# Why is it called "Through Time"?

Normal backpropagation:

```text
Backward through layers
```

BPTT:

```text
Backward through layers
+
Backward through time steps
```

Hence:

```text
Backpropagation Through Time
```

---

# Example

Sentence:

```text
I love machine learning
```

Suppose the model predicts the next word.

Forward:

```text
I       → hidden state
love    → hidden state
machine → hidden state
learning
```

Loss is calculated.

BPTT then propagates the error back through:

```text
learning
↓
machine
↓
love
↓
I
```

to update shared weights.

---

# Main Challenge: Vanishing Gradients

During BPTT:

Gradient computation involves repeated multiplication.

```text
0.1 × 0.1 × 0.1 × ...
```

becomes:

```text
0.000001
```

Result:

```text
Early time steps learn very slowly
```

This is the **vanishing gradient problem**.

---

# Exploding Gradients

Similarly:

```text
5 × 5 × 5 × ...
```

becomes enormous.

Result:

```text
Training becomes unstable
```

This is the **exploding gradient problem**.

---

# Solutions

### For Vanishing Gradients

Use:

* LSTM
* GRU

These preserve information across long sequences.

---

### For Exploding Gradients

Use:

```text
Gradient Clipping
```

to limit gradient magnitude.

---

# Truncated BPTT

For very long sequences:

```text
1000 time steps
```

full BPTT is expensive.

Instead:

```text
Backpropagate only last k steps
```

Example:

```text
k = 20
```

This is called:

```text
Truncated Backpropagation Through Time (TBPTT)
```

It reduces memory and computation requirements.

---

# Interview Questions

### 1. What is BPTT?

> BPTT is the training algorithm for RNNs that computes gradients by unrolling the network across time and propagating errors backward through all time steps.

---

### 2. Why can't we use ordinary backpropagation directly in RNNs?

> Because RNNs have temporal dependencies. The current hidden state depends on previous hidden states, so gradients must be propagated through time as well as layers.

---

### 3. What is meant by unrolling an RNN?

> Unrolling converts the recurrent network into a sequence of connected copies across time steps, allowing standard backpropagation to be applied.

---

### 4. What are the drawbacks of BPTT?

* Vanishing gradients
* Exploding gradients
* High computational cost
* Large memory consumption for long sequences

---

### 5. What is Truncated BPTT?

> A variation of BPTT where gradients are propagated back only a fixed number of time steps instead of the entire sequence.

---

# Interview One-Liner

> Backpropagation Through Time (BPTT) is the learning algorithm used to train RNNs, where the network is unrolled across time and gradients are propagated backward through all time steps to update shared weights. Its main challenges are vanishing and exploding gradients, which motivated architectures like LSTM and GRU.
