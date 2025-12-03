# Multilingual Harmful / Non-Harmful Meme Classification  
### Dataset Curation & Multimodal Baseline Development

This repository presents the first large-scale effort to curate **Indic-language harmful meme datasets** and build a **multimodal baseline model** for harmful meme classification across **Hindi, Telugu, Tamil, and Kannada**.  
Our work extends the MOMENTA architecture with **IndicBERT**, **ConceptNet background knowledge**, and **multimodal attention fusion**.

---

## 🔍 Overview

Memes are a powerful communication medium, but many contain harmful content such as stereotypes, hate, misinformation, or targeted harassment.  
Despite progress in English harmful meme detection, **Indic languages remain almost unexplored**.

This project aims to close that gap by:

- Curating high-quality datasets across four Indic languages  
- Using a **hybrid annotation strategy** (LLMs + manual verification)  
- Developing a **multimodal harmfulness classifier**  
- Evaluating with **Macro-F1** to address class imbalance  
- Releasing datasets & code for reproducibility  

---

## ✨ Key Contributions

### **1. First curated multilingual Indic meme datasets**

Languages supported:

- Hindi  
- Telugu  
- Tamil  
- Kannada  

Telugu and Kannada datasets are **first-of-their-kind handcrafted datasets** for harmful meme detection.

### **2. Multimodal Baseline Model**

Our baseline integrates:

- **CLIP** — global image embeddings  
- **VGG-19** — local region-based cues  
- **IndicBERT** — text embeddings tuned for Indic languages  
- **ConceptNet** — background knowledge reasoning  
- **MOMENTA-style attention fusion** — integrates all modalities  

### **3. Full End-to-End Pipeline**

Includes:

- OCR-based text extraction  
- Text cleaning and Indic tokenization  
- Region-based vision feature extraction  
- External knowledge retrieval  
- Attention-based fusion  
- Supervised training and evaluation  

---

## 📚 Dataset Details

| Language | Harmful | Harmless | Ratio |
|----------|---------|----------|--------|
| Telugu   | 965     | 1970     | 1 : 2  |
| Kannada  | 573     | 1064     | 1 : 2  |
| Tamil    | 1282    | 1018     | 1.26 : 1 |
| Hindi    | 3776    | 3070     | 1.23 : 1 |

**Dataset link (SharePoint):**  
https://iitgnacin-my.sharepoint.com/my?id=%2Fpersonal%2F23110168_iitgn_ac_in%2FDocuments%2FMemes%20Dataset

---

## 🧠 Model Architecture

The model uses four parallel encoders:

- **CLIP** for global image-level embeddings  
- **VGG-19** for local region features  
- **IndicBERT** for meme text  
- **ConceptNet** for retrieving contextual background concepts  

These representations are fused using **self-attention** and **cross-attention layers** inspired by MOMENTA.

**Trainable parameters:** ~3.74M  

---

## ⚙️ Training Configuration

- **Optimizer:** Adam  
- **Learning Rate:** 1e-5  
- **Batch Size:** 32  
- **Epochs:** 40  
- **Training Platform:** Kaggle T4 GPUs  
- **Split:** 80% training, 20% testing  
- **Evaluation:** Accuracy + Macro-F1  

Identity-based stratification was used to avoid leakage when the same person appears in multiple memes.

---

## 📊 Results

### **Accuracy (Validation)**

| Language | Full Model | Without ConceptNet |
|----------|------------|--------------------|
| Hindi    | 0.40       | 0.35 |
| Tamil    | 0.37       | 0.31 |
| Telugu   | 0.36       | 0.34 |
| Kannada  | 0.32       | 0.29 |

### **Macro-F1 (Validation)**

| Language | Full Model | Without ConceptNet |
|----------|------------|--------------------|
| Hindi    | 0.41       | 0.38 |
| Tamil    | 0.39       | 0.36 |
| Telugu   | 0.34       | 0.30 |
| Kannada  | 0.33       | 0.29 |

ConceptNet consistently improved performance, especially for context-heavy memes.

---

## 🧪 Qualitative Error Analysis

### **1. False Positive**
A harmless meme predicted as harmful due to:

- Noisy OCR  
- Misinterpreted facial cues  
- Incorrect background concept retrieval  

### **2. False Negative**
A harmful meme predicted harmless due to:

- Indic slang poorly handled by IndicBERT  
- Missing culturally relevant ConceptNet connections  

### **3. Correct Complex Meme**
Success due to:

- Clean OCR extraction  
- Strong textual signal  
- Helpful background knowledge  
- Good multimodal feature alignment  

---

## 🚧 Limitations

- Lower performance compared to English models  
- Weak handling of slang & code-mixed text  
- OCR struggles with stylized meme fonts  
- ConceptNet lacks Indic cultural references  
- No large-scale vision encoders (ViT/CLIP-L) used  

---

## 🔮 Future Work

- Use advanced knowledge graphs (ATOMIC, Wikidata)  
- Fine-tune OCR on Indic meme datasets  
- Expand datasets to more Indic languages  
- Explore LLaVA, Qwen-VL, or other VLMs for zero-shot  
- Introduce fine-grained harmfulness categories  
- Improve handling of code-mixed text (Hinglish, Tenglish)  
- Build real-time inference pipeline  

---

## 🔗 Code, Checkpoints & Web App

**Model Code:**  
https://github.com/Akhilesh348/Multilingual-Memes-Classification-Harmful-Non-Harmful-.git

**Web Application:**  
https://github.com/Praveennayak22/Meme_Classifier_Web_App

**Model Checkpoint:**  
https://drive.google.com/file/d/1_gywN0IEiFIppZGsIw2Frhbo_XtxZx0q/view

---

