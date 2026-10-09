# Autoencoders & Variational Autoencoders (VAEs)

> Personal study notes — understanding how autoencoders compress data and how VAEs enable structured sampling and generation from a latent space.

---

## 1. What is an Autoencoder?

An **autoencoder** is a neural network that learns a **compressed representation** of input data and then **reconstructs** the original data from that compressed form.

**Flow:** `Input → Encoder → Latent space → Decoder → Reconstructed output`

**Example:**
Imagine we feed a picture of a dog into the model. The encoder compresses it into a small set of numbers (the latent representation). The decoder then takes those numbers and tries to reconstruct the dog picture.
If the input has 1000 values, the encoder might compress it down to 50 values in the latent space, and the decoder expands it back to 1000 values.

## 2. Components: Encoder, Latent Space, Decoder

- **Encoder:** Converts the input into a compact representation. For example, it might turn an image into a vector like `[0.72, 0.31, -0.45, 0.81]`.
- **Latent Space:** The space where these compact representations live. It's a "compact information space."
  > **Analogy:** Think of compressing a large, detailed photograph into a short text summary that keeps only the most important features.
- **Decoder:** The reverse of the encoder. It takes the latent representation and turns it back into the reconstructed output. The goal is to make the output as close as possible to the original input.

## 3. Limitation of a Plain Autoencoder

A plain autoencoder does **not explicitly force the latent space to follow a smooth probability distribution**.

Because of this, the latent space can have regions with little or no meaningful representation (empty gaps). If you pick a random point from one of these empty regions and run it through the decoder, there is **no guarantee** that the output will look like anything meaningful. 
While it learns useful compressed representations, it is not organized as a continuous distribution suitable for **controlled sampling and generation**.

## 4. Variational Autoencoder (VAE)

A **Variational Autoencoder** fixes the gaps in the latent space by making the latent representation **probabilistic** rather than a single fixed point.

Instead of outputting fixed values, the encoder in a VAE outputs parameters for a **Gaussian (normal) distribution**: 
- **Mean (μ):** Controls the **center** of the distribution.
- **Standard Deviation (σ):** Controls the **spread**. A small σ gives a narrow curve, while a large σ gives a wide curve.
*(Note: σ² is the variance. In practice, implementations often output `log σ²`, known as `z_log_var`, for numerical stability.)*

Instead of saying "the latent representation is exactly this point," the VAE says "the latent representation can be **sampled** from this distribution." This forces the latent space to be continuous and structured, making it far better for generating new data.

### Autoencoder vs VAE

| Aspect | Autoencoder | VAE |
|---|---|---|
| Latent representation | Fixed | Probabilistic |
| Encoder output | Latent values | μ and σ |
| Latent space | Not explicitly modeled as a distribution | Modeled with a Gaussian |
| Sampling | Not naturally structured for it | Designed to support it |
| Main idea | Compress and reconstruct | Learn a structured probabilistic latent representation |

## 5. Reparameterization Trick

If we directly sample `z` from `N(μ, σ²)`, the randomness blocks the flow of gradients during backpropagation, so the network cannot learn.

**Reparameterization trick:** Instead of sampling directly from the distribution defined by μ and σ, we sample a random noise variable **ε** from a standard normal distribution `N(0,1)`. Then we calculate `z` as:
**`z = μ + σ·ε`**

Here, μ and σ come from the encoder, and ε supplies the randomness. Because the randomness is separated into ε, gradients can flow cleanly through μ and σ.

**Worked Example:**
If the encoder outputs μ = 2 and σ = 0.5, and we randomly sample ε = 1:
`z = 2 + 0.5 * 1 = 2.5`

## 6. Reconstruction Loss

**Reconstruction loss** measures how different the reconstructed output `x'` is from the original input `x`. Lower is better.
For a plain autoencoder, the total loss is simply the reconstruction loss.

**Worked Example:**
Suppose the input `x` is `[1.0, 0.8, 0.2, 0.5]`.
- Model A reconstructs `x'` as `[0.9, 0.7, 0.3, 0.6]`.
- Model B reconstructs `x'` as `[0.99, 0.79, 0.21, 0.51]`.
Model B has a much lower reconstruction loss because its values are much closer to the original input.

## 7. KL Divergence

**KL divergence** measures how different one probability distribution is from another.
In a VAE, it is used to measure how far the learned latent distribution `q(z|x) = N(μ, σ²)` is from the standard normal distribution `p(z) = N(0, I)`. 

It acts as a **regularizer** that pulls the latent distributions toward `N(0, I)`, ensuring the latent space stays organized and centered, preventing distributions from spreading out too far or becoming too narrow.

Closed form for a diagonal Gaussian vs `N(0, I)`:
`D_KL = -½ Σ ( 1 + log σ² − μ² − σ² )`

## 8. ELBO and VAE Loss

The objective that a VAE **maximizes** is called the **ELBO (Evidence Lower Bound)**. Since neural networks are trained by **minimizing** a loss, we define the VAE loss as the negative ELBO.

- **ELBO** = `E_q[ log p(x|z) ] − D_KL( q(z|x) || p(z) )` → **maximize**
- **VAE loss** = `-ELBO` = `Reconstruction loss + D_KL( q(z|x) || p(z) )` → **minimize**

*(Note: Some sources write ELBO as `L2(x, x') − D_KL`, but this mixes the sign convention because L2 is an error to be minimized, while ELBO is to be maximized.)*

## 9. Quick Revision

| Concept | Purpose |
|---|---|
| Encoder | Converts input into latent distribution parameters |
| μ | Center of the distribution |
| σ | Spread of the distribution |
| Reparameterization | Enables sampling while allowing gradient-based training |
| z | Sampled latent representation |
| Decoder | Reconstructs/generates output from z |
| KL divergence | Keeps the learned Gaussian close to N(0, I) |
| Reconstruction loss | Measures how well the input is reconstructed |
| ELBO | Objective maximized by the VAE |
| VAE loss | Negative ELBO, minimized during training |

**One-line recall:** A VAE uses μ and σ to define a Gaussian latent distribution, uses reparameterization to sample z, uses KL divergence to structure the latent space, and optimizes ELBO to balance reconstruction quality with latent-space regularization.

## 10. Next Steps and Comparisons

**Links:**
- Back to [Transformers and Autoregressive Models](07-transformers-and-autoregressive-models.md) and [Transformer Types and Image Generation](08-transformer-types-and-image-generation.md) for other ways to generate images.
- Forward to the hands-on notebook: [VAE MNIST Lab](../notebooks/vae-mnist.ipynb).

### VAE vs Autoregressive Models (Pixel RNN/CNN)

| Feature | VAE | Autoregressive (Pixel RNN/CNN) |
|---|---|---|
| Generation process | Samples the whole image at once from a latent vector in a single decoder pass | Generates the image pixel-by-pixel sequentially |
| Latent Space | Has a continuous latent space for structured interpolation | Typically has no global latent space |

---
*Source: Course notes — "Autoencoders and Variational Autoencoders"*
