# 🖼️ Convolutional Neural Networks (CNN) — Deep Dive

> CNNs are the deep-learning architecture specialized for **visual / grid-structured data**, inspired loosely by the biological visual cortex.

---

## 1. Why CNNs?

Regular dense networks flatten an image into a long vector and lose **spatial structure** (which pixels are neighbors). CNNs preserve this structure and learn **hierarchical visual features**:

```
Edges & lines → Shapes & textures → Object parts → Full objects
```

## 2. The CNN Pipeline (Simple Architecture)

```
Input Image (H×W×C)
     │
     ▼
[Convolutional Layer] → learn filters (edges, colors...) ─┐
     │                                                     │  Feature
     ▼                                                     │  Extraction
[Pooling Layer]        → shrink & keep strongest signals ──┘
     │
     (repeat Conv → Pool blocks, each stage learns more complex features)
     │
     ▼
[Flatten Layer]        → turn 2D feature maps into 1D vector
     │
     ▼
[Fully Connected/Dense]→ combine features for the decision
     │
     ▼
[Output Layer]         → class probabilities (Softmax)
```

### Example sizing (128×128×3 input)

| Stage | Filters | Kernel | Pool | Output size |
|---|---|---|---|---|
| Conv1 + Pool1 | 32 | 3×3 | 2×2 | 126×126×32 → 63×63×32 |
| Conv2 + Pool2 | 64 | 3×3 | 2×2 | 61×61×64 → 30×30×64 |
| Conv3 + Pool3 | 128 | 3×3 | 2×2 | 28×28×128 → 14×14×128 |
| Flatten → Dense | — | — | — | → N classes |

## 3. Core explanation, in plain English

| Stage | What it does | Kid-friendly analogy |
|---|---|---|
| **Input Layer** | Converts a picture into a grid of numbers (pixels) | Handing the computer a picture |
| **Convolutional Layer** | Slides small filters ("magnifying glasses") over the image to detect patterns | Looking for clues: lines → shapes → textures |
| **Pooling Layer** | Shrinks the feature map, keeping only the strongest signals | Keeping only the loudest clues, discarding the rest |
| **Flatten Layer** | Reshapes 2D feature maps into a single 1D vector | Lining up all the clues in a row |
| **Output Layer (Dense + Softmax)** | Produces a probability per class | "95% dog, 4% cat, 1% car" |

## 4. Real-World Applications

- **Content moderation & tagging** — Facebook/Instagram auto-tagging faces & objects
- **Medical imaging** — detecting tumors/fractures in X-rays, CT, MRI
- **Autonomous vehicles** — real-time pedestrian/vehicle/traffic-light detection
- **Facial recognition** — phone unlock, airport security
- **Retail/e-commerce** — visual product search, automated checkout recognition

---

## 5. Hands-on: MNIST Digit Classifier (Lab)

Practical notebook: [`notebooks/mnist-cnn-classification.ipynb`](../notebooks/mnist-cnn-classification.ipynb)

**Goal:** classify handwritten digits 0–9, visualize what the model sees, evaluate carefully, and even predict a digit you draw/upload yourself.

### Model architecture used

```python
model = keras.Sequential([
    layers.Input(shape=(28, 28, 1)),

    layers.Conv2D(32, (3, 3), activation="relu", name="conv1"),
    layers.MaxPooling2D((2, 2), name="pool1"),

    layers.Conv2D(64, (3, 3), activation="relu", name="conv2"),
    layers.MaxPooling2D((2, 2), name="pool2"),

    layers.Flatten(),
    layers.Dense(128, activation="relu", name="dense1"),
    layers.Dropout(0.30),
    layers.Dense(10, activation="softmax", name="output")
])

model.compile(optimizer="adam",
              loss="sparse_categorical_crossentropy",
              metrics=["accuracy"])
```

### Workflow covered in the notebook

1. Load & inspect MNIST-style data (CSV/NPZ auto-loader)
2. Visualize samples as images **and** as raw pixel-intensity heatmaps
3. Check class balance (bar chart of digit counts)
4. Reshape images to `(N, 28, 28, 1)` — add the channel dimension CNNs expect
5. Build & train the CNN (`validation_split=0.20`, 10 epochs)
6. Evaluate on the held-out test set: accuracy, confusion matrix, classification report
7. **Bonus:** upload your own handwritten digit → the notebook crops, centers, resizes to 28×28, and predicts it with a confidence score
8. Save the trained model (`.keras` format) for reuse without retraining

### Key practical takeaways

- CNNs expect a **channel dimension**, even for grayscale images: `(28, 28)` → `(28, 28, 1)`.
- `validation_split` gives an *honest* read on generalization — it's never used to update weights.
- `Dropout` (here 30%) randomly disables neurons during training to reduce overfitting.
- The final `Softmax` layer turns raw scores into a probability distribution over the 10 digit classes.

---
*Source: SmartBridge/SkillWallet — "Understanding of Convolutional Neural Network" + Lab02 MNIST CNN notebook*
