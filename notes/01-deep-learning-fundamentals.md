# 📘 Deep Learning & Neural Network Fundamentals

> Personal study notes — Deep Learning basics, perceptrons, training loop, and the ANN/CNN/RNN family.

---

## 1. What is Deep Learning?

**Deep Learning** = a branch of Machine Learning that uses **multi-layer neural networks** to learn complex patterns straight from raw data.

> 🧠 **Analogy:** Teaching a computer to recognize a face by showing it thousands of examples — instead of manually telling it "look for eyes, nose, jawline."

### Why do we need it? — Limits of classic ML

| Limitation of traditional ML | Deep Learning's answer |
|---|---|
| Needs **manual feature engineering** (shape, color, texture, edges…) | Learns useful representations **automatically** from raw data |
| Struggles with **complex/unstructured data** (images, audio, video, text) | Excels at exactly this kind of data |

---

## 2. The Perceptron — the atomic unit

A **Perceptron** is the simplest neural network: it takes inputs, multiplies by weights, adds a bias, and passes the result through an activation function.

```
x1 ──(w1)──┐
x2 ──(w2)──┼──► Σ (weighted sum + bias) ──► Activation ──► y (output)
xn ──(wn)──┘
              ▲
              b (bias)
```

## 3. Neuron — the computational unit

```
Inputs → Weights → Bias → Activation Function → Output
```

- A **single neuron** = simple computation.
- **Many neurons across many layers** = ability to model very complex relationships.

## 4. Dense (Fully Connected) Layers

A **Dense Layer**: every neuron connects to every neuron of the previous layer.

A basic network = **Input Layer → Hidden Layer(s) → Output Layer**

| Layer | Role |
|---|---|
| Input | Receives the raw data |
| Hidden | Learns different, increasingly abstract representations |
| Output | Produces the final prediction |

## 5. Core building blocks

| Concept | One-liner |
|---|---|
| **Weight** | Importance score for an input — higher weight → more influence |
| **Bias** | Baseline adjustment that shifts a neuron's output, adding flexibility |
| **Activation Function** | Decides how strongly a neuron "fires"; introduces **non-linearity** |
| **Forward Propagation** | Passing data from input → output through the network |
| **Loss Function** | Measures how wrong the prediction is (`Loss = expected − predicted`, conceptually) |
| **Backward Propagation** | Sends the error backward to see which weights caused it |
| **Optimizer** | Uses the backprop signal to actually update the weights (e.g., gradient descent style) |

### Common Activation Functions

| Function | Range | Typical use |
|---|---|---|
| **Sigmoid** | (0, 1) | Output layer, binary classification |
| **ReLU** | [0, ∞) | Hidden layers (efficient, avoids vanishing gradients) |
| **Leaky ReLU** | (−∞, ∞), small slope for negatives | Hidden layers, prevents "dead neurons" |
| **Softmax** | Probabilities summing to 1 | Output layer, multi-class classification |

### The full training loop

```
Input → Forward Propagation → Prediction → Loss Calculation
      → Backpropagation → Optimizer → Weight Update → (repeat)
```

> 🧠 **Analogy:** Like getting an exam back with a 60% score, figuring out *which* questions were wrong and *why*, then studying differently before the next attempt.

---

## 6. Types of Deep Learning Architectures

| Model | Best suited for | Example use cases |
|---|---|---|
| **ANN** (Artificial Neural Network) | Structured / tabular data | Churn prediction, credit risk, fraud detection, sales forecasting |
| **CNN** (Convolutional Neural Network) | Images & visual/grid data | Image classification, face recognition, object detection |
| **RNN** (Recurrent Neural Network) | Sequential data (order matters) | Language processing, speech recognition, time-series/demand forecasting |

**Quick mnemonic:**
```
ANN → General patterns
CNN → Visual patterns
RNN → Sequential patterns
```

---

## ✅ Quick Revision Cheat Sheet

- Deep Learning = ML + multi-layer neural nets → learns representations, not just labels.
- Neuron pipeline: **Inputs → Weights → Bias → Activation → Output**
- Training pipeline: **Forward Prop → Loss → Backprop → Optimizer → repeat**
- ANN = tabular, CNN = images, RNN = sequences.

---
*Source: SmartBridge/SkillWallet — "Introduction to Deep Learning, Neural Networks, and Core Concepts"*
