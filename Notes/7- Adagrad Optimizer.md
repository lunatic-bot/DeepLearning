## AdaGrad (Adaptive Gradient Optimizer)

**AdaGrad** stands for **Adaptive Gradient Algorithm**.

It is an optimization algorithm that adapts the learning rate for each parameter individually during training.

The key idea:

> Frequently updated parameters get smaller learning rates, while infrequently updated parameters get larger learning rates.

---

# Why was AdaGrad introduced?

In standard SGD:

```text
All parameters use the same learning rate.
```

Example:

```text
W1 → learning rate = 0.01
W2 → learning rate = 0.01
W3 → learning rate = 0.01
```

But some parameters may require:

* large updates
* small updates

AdaGrad automatically adjusts this.

---

# Core Idea

AdaGrad keeps track of the historical squared gradients.

For each parameter:

```text
Large past gradients
→ Smaller future learning rate

Small past gradients
→ Larger future learning rate
```

---

# Update Rule

First accumulate squared gradients:

G_t=G_{t-1}+g_t^2

where:

* (g_t) = current gradient
* (G_t) = accumulated squared gradients

Then update weights:

W_{t+1}=W_t-\frac{\eta}{\sqrt{G_t+\epsilon}}g_t

where:

* (\eta) = learning rate
* (\epsilon) = small number to avoid division by zero

---

# What happens over time?

Suppose a parameter receives large gradients repeatedly.

Then:

```text
Gt becomes very large
```

So:

```text
η / √Gt becomes smaller
```

Result:

```text
Smaller updates
```

For rarely updated parameters:

```text
Gt remains small
```

Result:

```text
Larger updates
```

---

# Why is this useful?

Consider NLP tasks.

Words like:

```text
the
is
and
```

appear frequently.

Words like:

```text
quantum
neural
transformer
```

appear less frequently.

AdaGrad naturally gives larger learning rates to rare features.

This made it popular for:

* NLP
* Sparse datasets
* Recommendation systems

---

# Advantages

### Adaptive learning rate

No need to manually tune learning rate heavily.

### Great for sparse data

Works well when some features appear rarely.

### Simple to implement

Built directly on SGD.

---

# Major Problem

The accumulated gradient:

G_t=\sum_{i=1}^{t}g_i^2

keeps growing forever.

Therefore:

```text
Learning rate keeps shrinking
```

Eventually:

```text
Learning rate ≈ 0
```

Training almost stops.

This is AdaGrad's biggest weakness.

---

# Example

Initially:

```text
Learning Rate = 0.01
```

After many updates:

```text
Effective Learning Rate = 0.00001
```

Then:

```text
Model learns extremely slowly
```

---

# How later optimizers fixed this

### RMSProp

Instead of storing all historical gradients:

```text
Uses moving average of recent gradients
```

### Adam

Combines:

* Momentum
* RMSProp

and became the most popular optimizer.

---

# Evolution of Optimizers

```text
SGD
 ↓
AdaGrad
 ↓
RMSProp
 ↓
Adam
 ↓
AdamW
```

---

# AdaGrad vs SGD

| Feature         | SGD    | AdaGrad                  |
| --------------- | ------ | ------------------------ |
| Learning Rate   | Fixed  | Adaptive                 |
| Sparse Features | Poor   | Excellent                |
| Tuning Required | More   | Less                     |
| Long Training   | Better | Learning rate may vanish |

---

# Interview-Friendly Definition

> AdaGrad (Adaptive Gradient Algorithm) is an optimization algorithm that adapts the learning rate for each parameter based on the history of its gradients. Frequently updated parameters receive smaller learning rates, while infrequently updated parameters receive larger learning rates. It works well for sparse data but suffers from continuously decreasing learning rates, which can eventually slow or stop learning.

---

### One-line interview answer

> AdaGrad improves SGD by using a separate adaptive learning rate for each parameter, making it particularly effective for sparse datasets, though its learning rate can become too small over time due to accumulated gradients.





## Why AdaDelta and RMSProp were introduced

The biggest problem with **AdaGrad** is:

```text
Accumulated squared gradients keep growing
↓
Learning rate keeps shrinking
↓
Training eventually becomes very slow
```

Both **AdaDelta** and **RMSProp** solve this by using only **recent gradients** instead of all historical gradients.

---

# 1. RMSProp (Root Mean Square Propagation)

Proposed by **Geoffrey Hinton**.

### Core Idea

Instead of storing all past gradients like AdaGrad:

```text
AdaGrad:
G = g₁² + g₂² + g₃² + ...
```

RMSProp keeps an **exponentially weighted moving average** of recent squared gradients.

### Formula

Moving average:

E[g^2]*t=\beta E[g^2]*{t-1}+(1-\beta)g_t^2

Weight update:

W_{t+1}=W_t-\frac{\eta}{\sqrt{E[g^2]_t+\epsilon}}g_t

---

## Intuition

Instead of remembering every gradient forever:

```text
Remember mostly recent gradients
Forget old gradients gradually
```

This prevents learning rates from shrinking to near zero.

---

## Advantages

* Solves AdaGrad's learning-rate decay problem
* Faster convergence
* Works well for deep neural networks
* Handles non-stationary objectives better

---

## Typical Hyperparameters

```text
Learning Rate = 0.001
Beta = 0.9
```

---

# 2. AdaDelta

AdaDelta is an improvement over AdaGrad proposed by Matthew Zeiler.

### Motivation

Even RMSProp still requires manually choosing:

```text
Learning Rate (η)
```

AdaDelta tries to reduce dependence on a manually chosen global learning rate.

---

## Core Idea

Instead of using:

```text
Gradient history only
```

AdaDelta tracks:

1. Past gradients
2. Past parameter updates

This helps determine an adaptive update size automatically.

---

### Gradient Moving Average

Similar to RMSProp:

E[g^2]*t=\rho E[g^2]*{t-1}+(1-\rho)g_t^2

---

### Update Calculation

AdaDelta computes updates using both gradient history and update history.

The exact equation is more involved, but the intuition is:

```text
Large recent updates
→ Smaller future updates

Small recent updates
→ Larger future updates
```

---

## Advantages

* No aggressive learning-rate decay
* Less sensitive to initial learning rate
* Automatic adaptation of update sizes

---

## Limitation

Although better than AdaGrad, it was eventually overshadowed by Adam.

Today you'll see Adam much more often than AdaDelta.

---

# AdaGrad vs RMSProp vs AdaDelta

| Feature                       | AdaGrad | RMSProp | AdaDelta       |
| ----------------------------- | ------- | ------- | -------------- |
| Adaptive Learning Rate        | ✅       | ✅       | ✅              |
| Uses All Past Gradients       | ✅       | ❌       | ❌              |
| Learning Rate Shrinks Forever | ✅       | ❌       | ❌              |
| Requires Manual LR            | ✅       | ✅       | Less sensitive |
| Deep Learning Usage Today     | Rare    | Common  | Less common    |

---

# Relationship Between Them

```text
SGD
 ↓
AdaGrad
 ↓
RMSProp
 ↓
Adam
```

AdaDelta was developed alongside this evolution as another attempt to fix AdaGrad's weaknesses.

---

# Interview-Friendly Definitions

### RMSProp

> RMSProp is an adaptive optimization algorithm that maintains an exponentially weighted moving average of squared gradients, preventing the learning rate from shrinking indefinitely as in AdaGrad. It is widely used for training deep neural networks.

### AdaDelta

> AdaDelta is an extension of AdaGrad that uses moving averages of both gradients and parameter updates to adapt learning rates automatically, reducing the need for manual learning-rate tuning.

---

# Quick Interview Comparison

If asked:

**"Why RMSProp is better than AdaGrad?"**

Answer:

> AdaGrad accumulates all past squared gradients, causing the effective learning rate to continuously decrease and eventually become too small. RMSProp fixes this by using an exponentially weighted moving average of recent gradients, allowing learning to continue effectively throughout training.

And if asked:

**"Why Adam became more popular?"**

Answer:

> Adam combines the advantages of Momentum and RMSProp, providing adaptive learning rates along with faster and more stable convergence, making it the default optimizer for many deep learning tasks.

