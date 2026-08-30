# 🎲 Probability Fundamentals & LLM Settings

---

## 1. Generative vs. Discriminative — the "art studio" framing

- **Discriminative AI** → detective with a magnifying glass, sorting existing paintings into "real" vs. "fake" (**classification**, learns decision boundaries).
- **Generative AI** → the artist at the easel, learning the *style rules* well enough to paint an entirely new picture (**creation**, learns data distributions).

---

## 2. The Four Core Probability Concepts

| Concept | Definition | Key points |
|---|---|---|
| **Probability** | How likely an event is to occur | Range **0 → 1**; 0 = impossible, 1 = certain; used for prediction/decisions |
| **Likelihood** | How well *observed data* supports a hypothesis | Uses observed data; compares hypotheses; higher = better explanation |
| **Prior** | Belief **before** seeing new evidence | Based on past knowledge; independent of current observation; the "starting assumption" |
| **Posterior** | Updated belief **after** seeing new evidence | Combines prior + observed data → improved estimate |

### Real-world example (the restaurant)

```
PRIOR:      "It looks popular, maybe 50% chance it's good?"   (before eating)
                          │
                 [ New evidence: you eat the food ]
                          │
                          ▼
POSTERIOR:  "This is amazing — 95% good now!"                 (after eating)
```

### Real-world example (probability vs. likelihood)

- **Probability** = the general forecast: *"70% chance of rain tomorrow."*
- **Likelihood** = using evidence right now (dark clouds, dropping pressure) to judge how well that evidence supports *"it will rain."*

> 🔑 **Bayesian intuition:** `Posterior ∝ Likelihood × Prior` — you start with a belief (prior), weigh it against new evidence (likelihood), and land on an updated belief (posterior). This is the statistical backbone behind a lot of probabilistic ML.

---

## 3. Important LLM Generation Settings

| Setting | What it controls | Low value | High value |
|---|---|---|---|
| **Temperature** | Creativity / randomness of output | 0–0.5 → deterministic, focused | 1.5–2.0 → random, creative |
| **Top-P** (nucleus sampling) | Diversity — picks the smallest set of tokens whose cumulative probability ≥ `p` | Small p → narrow, safe word choices | Large p → wider pool of possible next words |
| **Knowledge Cutoff** | Date up to which the model was trained | — model has **no awareness** of anything after this date | — |
| **Max Output Length** | Max number of tokens the model can generate in one response | Shorter, capped responses | Longer, more complete responses (until cap) |

### Mental model

```
Temperature  → "How wild should my word choices be?"
Top-P        → "How big is the pool of words I'm allowed to pick from?"
Cutoff       → "What's the most recent thing I actually know about?"
Max length   → "When do I have to stop talking?"
```

---
*Source: SmartBridge/SkillWallet — "Overview of Generative AI and Probability Fundamentals"*
