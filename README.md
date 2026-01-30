# Ecommerce-review-nlp
# E-commerce Review NLP: 1–5 Star Rating Prediction

## Overview
This project builds a multi-class NLP solution that converts free-form e-commerce review text into **1–5 star ratings**.  
It benchmarks **traditional ML baselines (TF-IDF)** against **deep learning models (CNN/LSTM with embeddings)** and summarizes results in a shareable HTML report.

## Dataset
- **59,621** reviews
- Key columns: **Score** (rating label) and **Text** (review content)

## Method
### Text preprocessing
- Basic cleaning (e.g., normalization, noise removal) and tokenization

### Text representations
- **TF-IDF**: n-gram range **(1,2)**, `min_df=2`, `max_features=20,000`
- **Embeddings (DL)**: vocabulary size **20,000**, embedding dim **128**, padding length **200 tokens**

### Models
- **Complement Naive Bayes (CNB)** + TF-IDF
- **KNN (best k=9)** + TF-IDF
- **CNN** + embeddings (conv layers + pooling)
- **LSTM** + embeddings (class weights + early stopping)

### Training & evaluation
- Metrics: **Accuracy / Precision / Recall / F1 (weighted)** + confusion matrix
- Optimizer (DL): **Adam**, loss: **categorical cross-entropy**
- Early stopping: **patience=2**

## Results (test set)
| Model | Accuracy | Weighted F1 | Notes |
|---|---:|---:|---|
| Naive Bayes | 0.685 | 0.672 | strong & lightweight baseline |
| KNN (k=9) | 0.635 | 0.589 | weakest; sensitive to sparse TF-IDF |
| CNN | **0.704** | **0.680** | best overall balance |
| LSTM | 0.648 | 0.660 | improved via class weights |

**Inference latency (same evaluation setting):** Naive Bayes (~0.25s) < CNN (~1.23s) < LSTM (~5.10s) < KNN (~7.83s)

## Key takeaways
- **CNN** achieves the best balance between accuracy and F1, especially for high-rated reviews.
- **Class imbalance** makes minority classes harder (models often confuse adjacent ratings).
- Naive Bayes is recommended for **fast, low-resource** scenarios; CNN/LSTM are better when **higher accuracy** is required.

## How to view the report
- HTML report: `E-commerce review NLP.html`

**Option A (recommended): Open locally**
1. Click `E-commerce review NLP.html`
2. Click **Download** (or **View raw**)
3. Open the downloaded file in a browser (Chrome/Safari)

**Option B (optional): Publish via GitHub Pages (web preview)**
If you want a shareable web link:
1. (Recommended) rename `E-commerce review NLP.html` → `index.html`
2. Repo → **Settings** → **Pages** → Deploy from branch (`main` / `root`)
3. Open the generated Pages URL

---

## Repository contents
- `E-commerce review NLP.html` — full report (exported notebook)
- `README.md` — project summary

---

## Use cases (how the results can be used)
- **Review coverage & normalization:** convert free-form reviews into structured 1–5 star ratings to standardize feedback at scale.
- **Product insight & prioritization:** surface recurring issues/topics behind low ratings to prioritize fixes and roadmap decisions.
- **Quality monitoring:** track shifts in predicted ratings over time to detect emerging problems after releases or policy changes.
- **Customer experience analytics:** summarize sentiment/rating signals to support marketing, service operations, and VoC reporting.

---

## Author
Shu-Yu Lin

