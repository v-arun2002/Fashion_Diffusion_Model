# 🧵 Fashion Product Image Generation Using Diffusion Models  
*A comparative evaluation of Stable Diffusion v1.5 and Kandinsky v2.2 for fashion image synthesis.*

---

## 📌 Project Overview  
This project builds an end-to-end **text-to-image diffusion system** for generating fashion product images from textual descriptions.  
Using **Stable Diffusion v1.5** and **Kandinsky v2.2**, we evaluate model quality, prompt alignment, and parameter sensitivity across multiple settings.

The workflow includes:
- Data ingestion & preparation  
- Prompt cleaning + metadata extraction  
- Real image selection for FID reference  
- Parameter grid search  
- Image generation  
- Statistical evaluation using CLIP, FID, and Inception Score  

---

## 📦 Dataset  
- Link: https://huggingface.co/datasets/ashraq/fashion-product-images-small
<img width="1003" height="564" alt="1" src="https://github.com/user-attachments/assets/0270afcb-311e-48da-be96-1ef3107f8277" />



- Source: **Hugging Face Fashion Product Images Dataset** (ashraq/fashion-product-images-small)  
- ~4,000 samples with
 metadata including:  
  - gender  
  - product type  
  - color  
  - season  
  - product display name  
- Cleaned and stored as `fashion_cleaned.pkl`

This dataset offers a diverse mix of shirts, watches, shoes, handbags, and apparel categories.

---

## 🧩 Architecture Overview

<img width="859" height="510" alt="Screenshot 2025-12-05 at 5 24 44 AM" src="https://github.com/user-attachments/assets/3884c526-05dc-4cc8-900a-e6eda71c74ae" />

<img width="884" height="478" alt="Screenshot 2025-12-05 at 5 57 32 AM" src="https://github.com/user-attachments/assets/bcce3ce0-437b-4cda-a6c5-5d0b2fcf597d" />

### **Data Ingestion & Preparation**
- Load raw dataset  
- Extract metadata (gender, color, product type, etc.)  
- Clean text prompts  
- Prepare 500 real images (512×512) for FID evaluation  
- Run CLIP text embedding for prompt interpretation  

### **Model Testing**
Two diffusion architectures were compared:
1. **Stable Diffusion v1.5**
2. **Kandinsky v2.2**

### **Parameter Grid Search**
- **Guidance Scale:** 7.5, 9.0, 12.0  
- **Inference Steps:** 30, 50  
- **Schedulers:** Euler, DDIM, PNDM  

---

## 🖼️ Image Generation

<img width="1452" height="147" alt="Screenshot 2025-12-05 at 5 05 52 AM" src="https://github.com/user-attachments/assets/6045cff9-4fa6-43e2-bd8b-6a6de9144157" />

Both models were used to generate multiple variations of:
- Watches  
- Shirts  
- Sweatshirts  
- Handbags  
- Shoes  

Sample results show:
- Stable Diffusion → more consistent quality  
- Kandinsky → stronger contrast & sharpness in some prompts  

---

## 📊 Evaluation Metrics

We computed three core generative metrics:

### **1️⃣ CLIP Score (Alignment)**  
Measures similarity between prompt and generated image.  
- Avg range: **0.27 – 0.40**  
- Best images achieved **0.396–0.401**  

### **2️⃣ FID – Fréchet Inception Distance**  
Lower = closer to real image distribution.  
- Stable Diffusion: **185.22** (best)  
- Kandinsky: comparable but slightly slower  
  
### **3️⃣ Inception Score (Diversity)**  
- Consistently low (≈1.0) due to limited dataset + small generation batches  
<img width="750" height="333" alt="Screenshot 2025-12-05 at 5 37 13 AM" src="https://github.com/user-attachments/assets/16799905-3058-456b-9b2f-76d03492b82d" />


---

## 🏆 Final Best Configuration  

Based on CLIP, FID, and overall consistency:

**Guidance Scale:** 9.0  
**Steps:** 50  
**Scheduler:** Euler  
**Model:** Stable Diffusion v1.5  
<img width="762" height="553" alt="Screenshot 2025-12-05 at 5 32 46 AM" src="https://github.com/user-attachments/assets/f11cbae2-931a-41ed-b757-ef4d58a25f06" />



---

## 📁 Final Outputs  
- **50 large-scale generated images**  
- Saved under `/final_samples_large/`  
- Prompts include:  
  - “women red leather handbag”  
  - “black running shoes with white sole”  
  - “adidas mens fire grey t-shirt”  


<img width="485" height="535" alt="output" src="https://github.com/user-attachments/assets/f8149936-9946-4008-a4a4-30ccbc48d833" />


---

## 📈 Key Findings  
- Euler scheduler consistently outperformed DDIM/PNDM.  
- Guidance 9.0 provided the best balance of realism + fidelity.  
- Stable Diffusion generated **more stable & consistent** images.  
- Kandinsky achieved slightly higher CLIP scores on some apparel items.  
- FID indicates **room for improvement** in fine textures & realism.  

---

## 🔮 Future Work  
- Use **DreamBooth / LoRA** to fine-tune on specific product styles  
- Expand dataset for better diversity  
- Optimize schedulers for high-resolution outputs  
- Build a full **AI-powered product catalog generator**  

---

## 🛠️ Tech Stack  
- **Stable Diffusion v1.5 / Kandinsky v2.2**  
- **Hugging Face Diffusers**  
- **CLIP (OpenAI)**  
- **PyTorch**  
- **Python**  

---
## 🧪 Gradio UI for Interactive Image Generation (Final Code Block)

To make this project more accessible and visually interactive, we implemented a **Gradio-based web UI directly inside Google Colab**.  
This interface allows the user to:

- Enter a fashion-related text prompt  
- Adjust guidance scale, inference steps, and random seed  
- Generate high-quality diffusion images instantly  
- Clear results and input new prompts  
- View outputs inline without requiring external hosting  

### **Why Gradio?**
- **Runs inline inside Colab** → no ngrok, no Streamlit server, no external links  
- **Lightweight & fast** → ideal for demos and presentations  
- **Professional UI** → sliders, textboxes, buttons, real-time outputs  
- Perfect for class presentations, project reviews, or rapid experimentation  

### **Example of the Gradio UI**
<img width="1565" height="841" alt="Gradio_UI" src="https://github.com/user-attachments/assets/1853e2f0-212a-49ed-90df-0ac1bb6799e2" />



## 👥 Contributors  
- Nishanth Manoharan  
- Arun Solaiappan Valliappan  
- Preeti Purnimaa Kannan  
- Abhinav Aditya  

---

## 📜 License  
MIT License  
