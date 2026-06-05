# Convolutional Neural Networks (CNN)

A **Convolutional Neural Network (CNN)** is a specialized type of neural network designed to process **grid-like data**, especially images.

CNNs automatically learn:

* edges
* shapes
* textures
* patterns
* objects

without requiring manual feature engineering.

CNNs are the backbone of modern:

* Computer Vision
* Object Detection
* Face Recognition
* Medical Imaging
* OCR
* Autonomous Driving

---

# Why not use a normal Neural Network for images?

Consider a color image:

```text
224 × 224 × 3
```

Total input features:

```text
224 × 224 × 3 = 150,528
```

Suppose first hidden layer has:

```text
1000 neurons
```

Parameters:

```text
150,528 × 1000
=
150 million+
```

Problems:

* Huge memory consumption
* Overfitting
* Slow training
* Ignores spatial relationships

CNN solves these issues.

---

# Core Idea of CNN

Instead of connecting every pixel to every neuron:

CNN learns small filters/kernels that scan the image.

Example:

```text
Image
┌───────────┐
│           │
│           │
│           │
└───────────┘

Kernel
┌───┐
│1 0│
│0 1│
└───┘
```

The filter slides over the image and extracts features.

---

# CNN Architecture

Typical CNN:

```text
Input Image
      ↓
Convolution Layer
      ↓
Activation (ReLU)
      ↓
Pooling Layer
      ↓
Convolution Layer
      ↓
Pooling Layer
      ↓
Flatten
      ↓
Fully Connected Layer
      ↓
Output
```

---

# 1. Convolution Layer

The most important layer.

Uses filters (kernels) to extract features.

Example filter:

```text
1  0 -1
1  0 -1
1  0 -1
```

This may detect vertical edges.

---

## How Convolution Works

Input:

```text
1 1 1
0 1 0
0 1 0
```

Kernel:

```text
1 0
0 1
```

Element-wise multiplication:

```text
(1×1)+(1×0)+(0×0)+(1×1)
=2
```

Produces one value in the feature map.

---

# Feature Maps

Output of convolution:

```text
Input Image
     ↓
Convolution
     ↓
Feature Map
```

Feature maps capture:

* edges
* corners
* textures
* object parts

---

# Hyperparameters in Convolution

## Filter Size

Examples:

```text
3×3
5×5
7×7
```

Most modern CNNs use:

```text
3×3
```

---

## Stride

Stride = movement of filter.

Stride 1:

```text
Move 1 pixel
```

Stride 2:

```text
Move 2 pixels
```

Larger stride:

* smaller output
* less computation

---

## Padding

Adds zeros around image.

Without padding:

```text
Image shrinks after convolution
```

With padding:

```text
Output size preserved
```

Types:

* Valid Padding
* Same Padding

---

# Output Size Formula

For convolution:

Output=\frac{N-F+2P}{S}+1

Where:

* N = input size
* F = filter size
* P = padding
* S = stride

---

# 2. Activation Function (ReLU)

After convolution:

```text
Negative → 0
Positive → keep
```

ReLU:

f(x)=\max(0,x)

Benefits:

* Non-linearity
* Faster training
* Reduces vanishing gradients

---

# 3. Pooling Layer

Reduces spatial dimensions.

Example:

```text
4×4
↓
2×2
```

---

## Max Pooling

Most common.

Example:

```text
1 3
2 4
```

Output:

```text
4
```

Takes maximum value.

---

## Why Pooling?

* Reduces computation
* Reduces overfitting
* Makes model robust to small shifts

---

# 4. Flatten Layer

Converts:

```text
Feature Maps
```

into

```text
1D Vector
```

Example:

```text
2×2×3
```

becomes

```text
12 values
```

---

# 5. Fully Connected Layer

Works like traditional neural network.

Combines extracted features for final prediction.

Example:

```text
Cat
Dog
Horse
```

---

# Training a CNN

Steps:

```text
Forward Pass
↓
Loss Calculation
↓
Backpropagation
↓
Weight Update
↓
Repeat
```

Optimizers:

* SGD
* RMSProp
* Adam

---

# Why CNNs Work So Well

## Local Connectivity

Nearby pixels are related.

CNN exploits this.

---

## Parameter Sharing

Same filter reused everywhere.

Huge reduction in parameters.

Example:

```text
Traditional NN:
Millions of weights

CNN:
Few thousand weights
```

---

## Hierarchical Learning

Layer 1:

```text
Edges
```

Layer 2:

```text
Corners
```

Layer 3:

```text
Shapes
```

Layer 4:

```text
Objects
```

---

# Famous CNN Architectures

### LeNet

First successful CNN.

---

### AlexNet

Won ImageNet 2012.

Introduced ReLU and Dropout.

---

### VGG16

Simple architecture using repeated 3×3 filters.

---

### ResNet

Introduced skip connections.

Solved deep network training problems.

---

### Inception

Multiple filter sizes in parallel.

---

# Advantages of CNN

✅ Automatic feature extraction

✅ Fewer parameters

✅ Translation invariance

✅ High accuracy

✅ Scalable

---

# Disadvantages

❌ Requires large datasets

❌ Computationally expensive

❌ Harder to interpret

---

# Most Important Interview Questions

### Basic

**1. What is CNN?**

A neural network specialized for image processing using convolution operations to automatically learn spatial features.

---

**2. Why CNN over ANN for images?**

CNN uses local connectivity and parameter sharing, drastically reducing parameters while preserving spatial information.

---

**3. What is a convolution operation?**

Applying a filter/kernel over an image to extract features such as edges and textures.

---

**4. What is a feature map?**

The output generated after applying a filter to an image.

---

### Intermediate

**5. What is stride?**

Number of pixels a filter moves during convolution.

---

**6. What is padding? Why is it used?**

Adding zeros around image boundaries to preserve dimensions and retain edge information.

---

**7. What is max pooling?**

A downsampling operation that keeps the maximum value in a region.

---

**8. Why ReLU is used in CNN?**

Introduces non-linearity and helps avoid vanishing gradients.

---

**9. What is parameter sharing?**

The same filter weights are reused across the entire image.

---

**10. What is flattening?**

Converting multi-dimensional feature maps into a 1D vector before dense layers.

---

### Advanced

**11. What are skip connections in ResNet?**

Direct connections that allow gradients to flow through deep networks more effectively.

---

**12. Why does CNN reduce overfitting compared to ANN?**

Fewer trainable parameters due to local connectivity and weight sharing.

---

**13. What is receptive field?**

The region of the input image that influences a neuron in a feature map.

---

**14. What is transfer learning?**

Using a pre-trained CNN and fine-tuning it for a new task.

---

**15. Explain CNN architecture from input to output.**

Input → Convolution → ReLU → Pooling → Convolution → Pooling → Flatten → Fully Connected → Output.

---

### Interview One-Liner

> CNNs are deep learning models designed for image data that use convolution filters, pooling, and parameter sharing to automatically learn hierarchical visual features while dramatically reducing the number of trainable parameters compared to fully connected neural networks.
