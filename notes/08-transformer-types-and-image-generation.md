# 🖼️ Transformer Types & Autoregressive Image Generation

> Personal study notes — encoder/decoder variants, Pixel RNN, Pixel CNN, masked convolutions, and how it all connects.

---

## 1. Types of Transformers

Transformers can be built using different combos of encoders and decoders. Three main types:

### 1.1 Encoder-only

The encoder processes input and creates a **meaningful representation** of it.

**Example:** Input: "The movie was excellent." → The encoder processes and captures its meaning for tasks like classification.

> 🧠 **Analogy:** Like a student reading and understanding a paragraph — *Read → Understand*

### 1.2 Decoder-only (Autoregressive)

A decoder **generates** output. In an autoregressive decoder, the model predicts the next token using tokens already available.

```
Artificial → Artificial Intelligence → Artificial Intelligence is → Artificial Intelligence is powerful
```

Each step generates another token.

### 1.3 Encoder-Decoder

Contains both. The **encoder understands** the input, the **decoder generates** the output.

**Example (Translation):**
```
Input: "I love India."
  → Encoder understands the input
  → Decoder generates the translated output
```

> 🧠 **Analogy:** Like a translator — one person reads and understands the original, another person produces it in a new language.

### Comparison Table

| Type | Primary Function | Best For |
|---|---|---|
| **Encoder-only** | Understands input, creates representations | Classification, sentiment analysis, NER |
| **Decoder-only** | Generates output one token at a time | Text generation, chatbots, creative writing |
| **Encoder-Decoder** | Understands input + generates output | Translation, summarization, complex reasoning |

**Memory hook:**
```
Encoder-only    → "Reader"
Decoder-only    → "Writer"
Encoder-Decoder → "Translator"
```

---

## 2. Pixel RNN — Image Generation

### 2.1 What is Pixel RNN?

A **Pixel RNN** is an autoregressive model that generates images **pixel by pixel** using recurrent processing. It learns relationships between pixels and predicts new ones based on previously generated pixels.

```
For text:      Previous words  → Next word
For Pixel RNN: Previous pixels → Next pixel
```

**Simple Example** — imagine generating a small image step by step:
```
□ □ □
□ □ □    →    Fill in pixel by pixel until complete
□ □ □
□ □ □
```

### 2.2 Generation Order

Pixel RNN generates pixels in a fixed order — commonly **left to right, top to bottom**:

```
P1 → P2 → P3 → P4 → P5 → P6 → P7 → P8 → P9
```

The key rule: the model must **not** use info from pixels that haven't been generated yet.

### 2.3 Pixel RNN Architectures

Two important architectures:

#### Row LSTM

Processes the image **row by row**. Information from earlier rows influences predictions in later rows.

```
Row 1 → Row 2 → Row 3 → Row 4
         ↓ info carries downward
```

**Why useful:** captures row-to-row dependencies, can process positions within a row more efficiently than fully sequential pixel-by-pixel approach.

#### Diagonal BiLSTM

Uses **diagonal** recurrent processing instead of just horizontal rows. Two directional recurrent paths capture info from different spatial directions.

```
P1
P2  P3
P4  P5  P6
P7  P8  P9  P10
```

**Why useful:** captures dependencies across diagonal directions, uses a wider spatial context, models relationships between pixels that aren't directly adjacent.

#### Row LSTM vs Diagonal BiLSTM

| Feature | Row LSTM | Diagonal BiLSTM |
|---|---|---|
| Processing pattern | Row-based | Diagonal-based |
| Main idea | Carries info between rows | Captures info along diagonals |
| Spatial context | Strong row-to-row dependency | Broader directional dependency |
| Think of it as | "Row by Row" | "Across Diagonals" |

---

## 3. Pixel CNN — Convolutional Image Generation

### 3.1 What is Pixel CNN?

A **Pixel CNN** uses convolutional neural network mechanics for autoregressive image generation. Since CNNs are great at recognizing spatial patterns (edges, shapes, textures, objects), they're a natural fit for image data.

```
Prior pixels → Pixel CNN → Next pixel
```

> 🧠 **Analogy:** Like looking at an artwork through a small window — you study the surrounding details and use those cues to predict what comes next.

### 3.2 Why Masked Convolution?

A normal convolution looks at a **full local neighborhood** around a pixel. But in autoregressive generation, we have a strict rule: **the prediction must not use future pixels.**

When predicting P5 in this grid:
```
P1  P2  P3
P4  P5  P6
P7  P8  P9
```

We CAN use: `P1, P2, P3, P4` (already generated)
We CANNOT use: `P6, P7, P8, P9` (future pixels)

A normal convolution would accidentally look at future pixels. So Pixel CNN uses **masked convolution** to block them.

### 3.3 Mask A vs Mask B

**Mask A** — used in the **first** masked conv layer:
```
1 1 1
1 0 0    (center pixel BLOCKED — we're trying to predict it!)
0 0 0
```

**Mask B** — used in **later** layers:
```
1 1 1
1 1 0    (center position ALLOWED — info already processed by Mask A)
0 0 0
```

The difference: Mask A blocks the current pixel entirely (prevents info leakage in the first layer). Mask B lets already-processed info flow through deeper layers while still blocking future positions.

```
Mask A = Strict first layer (no peeking at the answer)
Mask B = Continue processing (but still block future info)
```

### 3.4 Generation Process

```
Previous Pixels → Masked Convolution → Learn Spatial Features
  → Predict Next Pixel → Add to Image → Repeat
```

**Important:** During *training*, masked convolutions allow processing many positions in parallel (the mask enforces the dependency structure). During *generation*, pixels still have to be generated one by one following the autoregressive order.

### 3.5 Receptive Field

The **receptive field** = the region of the image that influences a pixel's prediction.

```
Layer 1 → Small context
Layer 2 → Larger context
Layer 3 → Even larger context
```

By stacking more masked conv layers, the model can "see" progressively larger parts of the image → better understanding of overall structure.

---

## 4. Pixel RNN vs Pixel CNN

| | Pixel RNN | Pixel CNN |
|---|---|---|
| Processing | Recurrent-style | Convolutional-style |
| Focus | Sequential dependencies | Localized spatial patterns |
| Generation | One pixel at a time | One pixel at a time |
| Built for | Image generation | Image generation |

Both are autoregressive — the core difference is whether they use recurrent or convolutional processing to model pixel dependencies.

---

## 5. The Big Picture — Evolution Summary

```
Basic RNN
  ↓
LSTM (better memory)
  ↓
Challenges with long sequences
  ↓
Transformer (attention mechanism)
  ↓
Autoregressive Modeling
  ↓
Next-Token Prediction
  ↓
Text Generation / Image Generation (Pixel RNN, Pixel CNN)
```

---

## ✅ Quick Revision

- Encoder = Reader, Decoder = Writer, Encoder-Decoder = Translator
- Pixel RNN = generate images pixel by pixel using recurrent processing
- Row LSTM processes rows, Diagonal BiLSTM processes diagonals
- Pixel CNN = generate images using masked convolutions
- Mask A (first layer, strict) vs Mask B (later layers, allows processed info)
- Receptive field grows with more conv layers
- Everything connects: RNN → LSTM → Transformer → Autoregressive → Generation

---
*Source: Course notes — "Understanding Autoregressive Models and Next-Token Generation"*
