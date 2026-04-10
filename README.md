# Fashion Product Image Generation Using Diffusion Models

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

## Project Overview

An end-to-end text-to-image generation system for fashion product synthesis using **Stable Diffusion v1.5** and **Kandinsky v2.2**. The project conducts a systematic comparative evaluation across model architectures, scheduler configurations, and inference parameters, measuring output quality using CLIP Score, FID, and Inception Score on a 4,000-sample fashion dataset.

**Best Configuration:** Stable Diffusion v1.5 | Guidance Scale 9.0 | 50 Steps | Euler Scheduler | FID: 185.22 | CLIP: 0.396–0.401

---

## Dataset

- **Source:** Hugging Face — `ashraq/fashion-product-images-small`
- **Size:** ~4,000 samples across shirts, watches, shoes, handbags, and apparel
- **Metadata:** Gender, product type, color, season, display name
- **Preprocessing:** Text prompt cleaning, metadata extraction, 500 real images (512×512) prepared for FID reference

---

## Architecture

The pipeline consists of four stages:

**1. Data Preparation** — Raw dataset ingestion, metadata extraction, prompt cleaning, and CLIP text embedding for semantic alignment scoring.

**2. Model Configuration** — Two diffusion architectures evaluated in parallel: Stable Diffusion v1.5 and Kandinsky v2.2, both loaded via Hugging Face Diffusers.

**3. Parameter Grid Search** — Systematic sweep across guidance scales (7.5, 9.0, 12.0), inference steps (30, 50), and schedulers (Euler, DDIM, PNDM) to identify optimal generation settings.

**4. Evaluation** — Generated images scored against three metrics: CLIP Score for prompt-image alignment, FID for distributional similarity to real images, and Inception Score for output diversity.

---

## Model Comparison

| Model | FID ↓ | CLIP Score ↑ | Strength |
|---|---|---|---|
| Stable Diffusion v1.5 | **185.22** | 0.396–0.401 | Consistency & realism |
| Kandinsky v2.2 | Comparable | Slightly higher on apparel | Contrast & sharpness |

---

## Evaluation Metrics

**CLIP Score** measures semantic alignment between text prompt and generated image. Achieved range of 0.27–0.40, with best images scoring 0.396–0.401.

**FID (Fréchet Inception Distance)** measures distributional similarity to real images — lower is better. Stable Diffusion achieved 185.22 as the best configuration.

**Inception Score** measures output diversity. Consistently ~1.0 due to limited dataset size and small generation batches — identified as an area for future improvement.

---

## Key Findings

- Euler scheduler consistently outperformed DDIM and PNDM across both models
- Guidance scale 9.0 provided the optimal balance of realism and prompt fidelity
- Stable Diffusion v1.5 produced more stable and consistent outputs at scale
- Kandinsky v2.2 achieved marginally higher CLIP scores on specific apparel categories
- FID scores indicate room for improvement in fine texture and high-frequency detail generation

---

## Interactive Demo

A **Gradio-based web UI** was implemented inside Google Colab allowing users to enter fashion prompts, adjust guidance scale, inference steps, and seed, and generate images in real time — no external hosting required.

---

## Tech Stack

| Category | Tools |
|---|---|
| Diffusion Models | Stable Diffusion v1.5, Kandinsky v2.2 |
| Model Library | Hugging Face Diffusers |
| Evaluation | CLIP (OpenAI), FID, Inception Score |
| Framework | PyTorch |
| UI | Gradio |
| Language | Python |

---

## Future Work

- Fine-tune on specific product styles using **DreamBooth / LoRA**
- Expand dataset for broader category diversity
- Optimize schedulers for high-resolution outputs
- Build a full AI-powered product catalog generator

---

## Project Structure

```
fashion-diffusion/
│
├── README.md
├── notebooks/
│   └── fashion_generation.ipynb
├── data/
│   └── fashion_cleaned.pkl
├── outputs/
│   └── final_samples_large/
└── assets/
    ├── architecture_diagram.png
    ├── gradio_ui.png
    └── sample_outputs.png
```


**Dataset:** Hugging Face Fashion Product Images | **Framework:** PyTorch | **License:** MIT
