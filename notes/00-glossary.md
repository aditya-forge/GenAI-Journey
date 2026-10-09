# Glossary of Deep Learning and Generative AI Terms

An alphabetical reference for all key terms across the study notes. Each entry links to the note where it is explained in more detail.

---

**Activation function** — A function applied to a neuron's output that introduces non-linearity, enabling the network to learn complex patterns. Common types: Sigmoid, ReLU, Softmax. [Notes 01](01-deep-learning-fundamentals.md)

**Attention** — A mechanism in Transformers that lets the model directly connect and weigh the importance of any two positions in a sequence, regardless of distance. [Notes 07](07-transformers-and-autoregressive-models.md)

**Autoencoder** — A neural network trained to compress input data into a latent representation (encoder) and then reconstruct the original (decoder). [Notes 09](09-autoencoders-and-vaes.md)

**Autoregressive** — A modeling approach where the next value in a sequence is predicted from previous values. Used in language models and image generation (Pixel RNN/CNN). [Notes 07](07-transformers-and-autoregressive-models.md), [Notes 08](08-transformer-types-and-image-generation.md)

**Bias** — A learnable offset added to a neuron's weighted sum, giving the model flexibility to shift its output independent of the inputs. [Notes 01](01-deep-learning-fundamentals.md)

**ELBO (Evidence Lower Bound)** — The objective a VAE maximizes during training. ELBO = Expected log-likelihood of reconstruction − KL divergence. VAE loss = −ELBO. [Notes 09](09-autoencoders-and-vaes.md)

**Encoder** — The part of an autoencoder or VAE that maps input data to a compact latent representation (or to distribution parameters μ and σ in a VAE). [Notes 09](09-autoencoders-and-vaes.md)

**Decoder** — The part of an autoencoder or VAE that maps from the latent space back to the original data space to produce a reconstruction or generated sample. [Notes 09](09-autoencoders-and-vaes.md)

**KL divergence (Kullback-Leibler divergence)** — A measure of how different one probability distribution is from another. In VAEs, it regularizes the latent space by keeping learned distributions close to N(0, I). [Notes 09](09-autoencoders-and-vaes.md)

**Latent space** — The compressed, lower-dimensional space where an autoencoder or VAE stores its learned representations. [Notes 09](09-autoencoders-and-vaes.md)

**Likelihood** — The probability of observing the data given a particular model and parameters. Distinct from probability in that the data is fixed and the model parameters vary. [Notes 04](04-probability-fundamentals-and-llm-settings.md)

**LSTM (Long Short-Term Memory)** — A type of RNN with gated memory cells that can learn to remember or forget information over long sequences. [Notes 06](06-lstm-and-sequence-models.md)

**Masked convolution** — A convolution where the kernel is masked so a pixel can only depend on previously generated pixels, enabling autoregressive image generation. [Notes 08](08-transformer-types-and-image-generation.md)

**Posterior** — The updated probability of a hypothesis after observing data. In Bayesian terms: P(hypothesis | data). [Notes 04](04-probability-fundamentals-and-llm-settings.md)

**Prior** — The initial probability of a hypothesis before observing any data. In Bayesian terms: P(hypothesis). [Notes 04](04-probability-fundamentals-and-llm-settings.md)

**Reparameterization** — A trick used in VAEs to enable gradient flow through a sampling step. Instead of sampling z directly, sample ε ~ N(0,1) and compute z = μ + σ·ε. [Notes 09](09-autoencoders-and-vaes.md)

**Self-supervised learning** — A learning paradigm where labels are automatically derived from the input data itself (e.g. predicting the next word in a sentence). [Notes 03](03-generative-ai-and-machine-learning.md)

**Temperature** — A parameter that controls the randomness of a language model's output distribution. Low temperature → more deterministic; high temperature → more random. [Notes 04](04-probability-fundamentals-and-llm-settings.md)

**Top-P (nucleus sampling)** — A sampling strategy where the model selects from the smallest set of tokens whose cumulative probability exceeds P. Controls output diversity. [Notes 04](04-probability-fundamentals-and-llm-settings.md)

---
*Generated from notes 01–09. Update when new notes are added.*
