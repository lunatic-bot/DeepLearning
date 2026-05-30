## Weight Initialization in Neural Networks

**Weight initialization** is the process of assigning initial values to the weights of a neural network before training begins.

It is extremely important because poor initialization can lead to:

- Vanishing gradients
- Exploding gradients
- Slow convergence
- Failure to learn

---

# Why not initialize all weights to zero?

Suppose all neurons start with:

```text
W = 0
```

Then every neuron in a layer produces the same output and receives the same gradient update.

Result:

```text
All neurons learn identical features
```

This is called the **symmetry problem**.

Therefore:

✅ Random initialization is required.

---

# Goals of Good Weight Initialization

A good initialization should:

1. Break symmetry
2. Keep activations stable across layers
3. Prevent exploding gradients
4. Prevent vanishing gradients
5. Speed up convergence

---

# 1. Random Initialization

Initialize weights with small random values:

```python
W = np.random.randn(n, m) * 0.01
```

### Problem

For deep networks:

- Too small → vanishing gradients
- Too large → exploding gradients

Not ideal for modern deep learning.

---

# 2. Xavier (Glorot) Initialization

Designed for:

- Sigmoid
- Tanh

Idea:

Keep variance approximately constant across layers.

Formula:

Var(W)=\frac{1}{n\_{in}}

Common implementation:

W\sim U\left(-\sqrt{\frac{6}{n*{in}+n*{out}}},\sqrt{\frac{6}{n*{in}+n*{out}}}\right)

### Advantages

- Stable gradients
- Faster convergence
- Good for tanh/sigmoid networks

---

# 3. He Initialization (Kaiming Initialization)

Designed specifically for ReLU networks.

Most commonly used today.

Formula:

Var(W)=\frac{2}{n\_{in}}

Implementation:

```python
torch.nn.init.kaiming_normal_(layer.weight)
```

### Why it works

ReLU sets many activations to zero.

The factor of 2 compensates for this information loss.

### Best for

- ReLU
- Leaky ReLU

---

# 4. LeCun Initialization

Designed for:

- SELU activation

Formula:

Var(W)=\frac{1}{n\_{in}}

Used less frequently than Xavier or He.

---

# Comparison

| Initialization      | Best Activation   |
| ------------------- | ----------------- |
| Random Small Values | Rarely used today |
| Xavier/Glorot       | Sigmoid, Tanh     |
| He/Kaiming          | ReLU, Leaky ReLU  |
| LeCun               | SELU              |

---

# What happens with bad initialization?

### Too Small

```text
Weights = 0.00001
```

Result:

```text
Activations become tiny
→ Vanishing gradients
→ Slow learning
```

### Too Large

```text
Weights = 100
```

Result:

```text
Activations explode
→ Exploding gradients
→ Unstable training
```

---

# Interview Question

### Why is He initialization preferred for ReLU?

Because ReLU deactivates all negative inputs and effectively passes only about half the signals forward. He initialization compensates by using:

Var(W)=\frac{2}{n\_{in}}

which helps maintain stable activation and gradient magnitudes across deep networks.

---

# Practical Framework Defaults

### TensorFlow/Keras

```python
Dense(
    128,
    activation="relu",
    kernel_initializer="he_normal"
)
```

### PyTorch

```python
nn.init.kaiming_normal_(layer.weight)
```

---

# Interview-Friendly Summary

> Weight initialization is the process of assigning initial values to neural network weights before training. Proper initialization helps maintain stable activations and gradients, preventing vanishing and exploding gradients. Common techniques include Xavier initialization for sigmoid/tanh networks and He initialization for ReLU-based networks, with He initialization being the most widely used in modern deep learning.
