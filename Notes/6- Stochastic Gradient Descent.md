## Stochastic Gradient Descent (SGD)

**Stochastic Gradient Descent (SGD)** is an optimization algorithm used to train machine learning and deep learning models by updating weights to minimize the loss function.

It is a variation of **Gradient Descent**.

---

# Quick Recap: Gradient Descent

The goal is to find weights that minimize the loss.

Weight update rule:

W_{new}=W_{old}-\eta\frac{\partial L}{\partial W}

where:

* (W) = weight
* (L) = loss function
* (\eta) = learning rate

The gradient tells us the direction of steepest increase, so we move in the opposite direction.

---

# Types of Gradient Descent

Suppose you have **10,000 training samples**.

## 1. Batch Gradient Descent

Uses the entire dataset before one update.

```text
10000 samples → Compute gradient → Update weights
```

### Pros

* Stable updates

### Cons

* Slow
* High memory usage

---

## 2. Stochastic Gradient Descent (SGD)

Uses **one sample at a time**.

```text
1 sample → Compute gradient → Update weights
```

Example:

```text
Sample 1 → Update
Sample 2 → Update
Sample 3 → Update
...
```

---

## 3. Mini-Batch Gradient Descent

Most commonly used today.

Uses small batches:

```text
32 samples → Update
64 samples → Update
128 samples → Update
```

This combines the benefits of batch and SGD.

---

# Why "Stochastic"?

"Stochastic" means **random**.

At each step, SGD picks a training example (or a shuffled order of examples) and updates weights immediately.

Because updates are based on a single example, they are noisy.

---

# Example

Dataset:

```text
10000 samples
```

### Batch GD

```text
Process all 10000
→ Calculate gradient
→ 1 update
```

### SGD

```text
Sample 1 → update
Sample 2 → update
...
Sample 10000 → update
```

So SGD performs many more updates per epoch.

---

# Visualization Intuition

Imagine finding the lowest point in a valley.

### Batch GD

```text
Smooth, steady path
```

### SGD

```text
Zig-zag path
```

because each sample gives a slightly different estimate of the gradient.

Even though it's noisy, SGD often reaches a good solution faster.

---

# Advantages of SGD

### Faster updates

Weights are updated immediately.

### Lower memory usage

Only one sample needed at a time.

### Escapes local minima better

The noise in SGD can help move out of poor local optima.

### Works well for large datasets

Widely used in deep learning.

---

# Disadvantages

### Noisy updates

Loss fluctuates.

### May not converge smoothly

Can oscillate around the optimum.

### Sensitive to learning rate

Choosing the right learning rate is important.

---

# Learning Rate

The learning rate controls step size.

### Too small

```text
Slow training
```

### Too large

```text
Overshoots minimum
Training unstable
```

---

# Modern Improvements over SGD

Most deep learning today uses advanced optimizers built on SGD concepts:

* Momentum
* RMSProp
* Adam
* AdamW

These often converge faster than plain SGD.

---

# SGD with Momentum

Momentum helps smooth noisy updates.

Idea:

```text
Current update
+
Some fraction of previous update
```

This accelerates learning in the correct direction.

---

# Interview-Friendly Definition

> Stochastic Gradient Descent (SGD) is an optimization algorithm that updates model parameters using the gradient computed from a single training example at a time. Compared to batch gradient descent, it is faster and more memory-efficient for large datasets, though its updates are noisier and less stable.

---

# Interview Follow-up Question

### Why is Mini-Batch Gradient Descent preferred over pure SGD?

Because it:

* uses vectorized computation efficiently on GPUs
* reduces noise compared to SGD
* converges faster and more stably

Typical batch sizes:

```text
32, 64, 128, 256
```

which is why most modern deep learning frameworks train using mini-batches rather than pure SGD.
