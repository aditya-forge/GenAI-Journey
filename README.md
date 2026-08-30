# 🧠 Deep Learning & Generative AI — Study Notes

Personal study notes from a Deep Learning / Generative AI / Machine Learning course, expanded with my own deeper research, diagrams, and a hands-on CNN lab. Kept here so I can revise quickly and share with others.

> 📓 These notes started from course handbooks and were extended with extra explanations, tables, and analogies while studying — including handwritten notes (scanned into [`handwritten-notes/`](./handwritten-notes)).

---

## 📂 Structure

```
.
├── notes/
│   ├── 01-deep-learning-fundamentals.md         # Perceptron, neurons, weights, bias, backprop, ANN/CNN/RNN
│   ├── 02-convolutional-neural-networks.md      # CNN architecture deep-dive + MNIST lab walkthrough
│   ├── 03-generative-ai-and-machine-learning.md # GenAI, discriminative vs generative, 4 learning types, ML tasks
│   ├── 04-probability-fundamentals-and-llm-settings.md # Probability, likelihood, prior/posterior, temperature/top-p
│   └── 05-ml-practical-and-eda.md               # ML lifecycle, Python libraries, 8-step EDA framework
├── notebooks/
│   └── mnist-cnn-classification.ipynb           # Hands-on CNN digit classifier (TensorFlow/Keras)
├── handwritten-notes/                           # (add your scanned/handwritten notes here)
└── README.md
```

## 📖 Topics Covered

| Notes file | Key concepts |
|---|---|
| [Deep Learning Fundamentals](notes/01-deep-learning-fundamentals.md) | Perceptron · Neuron · Weights & Bias · Activation Functions · Forward/Backward Propagation · Optimizers · ANN vs CNN vs RNN |
| [Convolutional Neural Networks](notes/02-convolutional-neural-networks.md) | Conv layers · Pooling · Flatten · Feature hierarchy · Real-world CV applications · Full MNIST CNN walkthrough |
| [Generative AI & ML](notes/03-generative-ai-and-machine-learning.md) | Generative vs Discriminative models · Supervised/Unsupervised/Reinforcement/Self-Supervised Learning · Regression/Classification/Clustering |
| [Probability & LLM Settings](notes/04-probability-fundamentals-and-llm-settings.md) | Probability vs Likelihood · Prior vs Posterior (Bayesian intuition) · Temperature · Top-P · Knowledge cutoff |
| [ML Practical & EDA](notes/05-ml-practical-and-eda.md) | Standard ML lifecycle · pandas/NumPy/Matplotlib/Seaborn/Pickle · 8-step EDA framework |

## 🚀 Hands-on Lab

[`notebooks/mnist-cnn-classification.ipynb`](notebooks/mnist-cnn-classification.ipynb) — a small CNN (Conv→Pool→Conv→Pool→Dense→Softmax) trained on MNIST, with visualizations of the raw data, training curves, a confusion matrix, and a fun step where you can upload your own handwritten digit for live prediction.

## 🗺️ How to read this repo

If you're new to the topic, read in this order:
1. **Deep Learning Fundamentals** → the building blocks (neuron, weights, training loop)
2. **Generative AI & ML** → the bigger picture (learning paradigms, ML task types)
3. **Convolutional Neural Networks** → the image-specific architecture
4. **Probability Fundamentals** → the math intuition behind "confidence" and generation settings
5. **ML Practical & EDA** → how this actually gets built in code

## 🙌 Credits

Course material basis: SmartBridge / SkillWallet handbooks. Notes, diagrams-in-text, and explanations reorganized/expanded by me while studying.

## 📄 License

Feel free to use these notes for your own learning. Attribution appreciated but not required.
