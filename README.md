
# Linear Transparency of Paraphrasing: Geometric Invariants in Transformer Embedding Spaces

Official code and experiments accompanying the paper:

**“The Linear Transparency of Paraphrasing: Discovering Geometric Invariants in Transformer Latent Spaces”**

This repository contains the full experimental pipeline used to demonstrate that paraphrase transformations in sentence embedding spaces can be approximated by **locally near‑isometric affine Lie transformations**.

---

# 🔬 Core Idea

Instead of modeling semantic similarity only with a scalar metric (e.g., cosine similarity), this work models paraphrasing as a **geometric transformation** in the embedding space.

A paraphrase transformation is approximated as an affine operator:

T(x) = A x + t

where:

- **A ∈ GL(n)** — structural transformation of the semantic basis  
- **t ∈ ℝⁿ** — contextual semantic shift

This formulation allows us to analyze paraphrasing using tools from:

- Lie groups
- geometric deep learning
- explainable AI (XAI)

The affine operator is interpreted as a **consensus linearization of local transformations** on the semantic manifold induced by a Transformer encoder.

---

# 📊 Key Results

Experiments on the **PIT‑2015 Twitter paraphrase dataset** using **Sentence‑BERT (all-mpnet-base-v2)** reveal a phenomenon we call:

## Linear Transparency of Transformer Embedding Spaces

| Model | ROC‑AUC |
|------|------|
| SBERT cosine similarity (baseline) | **0.8405** |
| Affine Lie model (Hybrid Cosine Score) | **0.7713** |

**Interpretation:**

The affine model reproduces **91.77% of the nonlinear classification capacity** of SBERT while remaining interpretable.

---

# 🧭 Discovered Geometric Invariants

The learned affine operator reveals stable geometric properties of paraphrasing:

| Descriptor | Value |
|-----------|------|
| Structural rotation angle | **27.84°** |
| Mean individual transformation angle | **≈44°** |
| Deformation index | **≈0.00025 (near‑isometric)** |
| Determinant of A | **≈ −0.836** |
| Shift magnitude ‖t‖₂ | **≈0.384** |

These results suggest that paraphrasing behaves as a **near‑isometric rotation with a small semantic drift** in the latent space.

---

# 📚 Datasets

The experiments use three datasets:

### PIT‑2015 (SemEval‑2015 Task 1)

Primary dataset used to estimate the affine transformation.

Contains paraphrase pairs from Twitter.

Used for:

- operator estimation (Train)
- evaluation (Dev)

---

### Twitter URL Corpus (TURL)

Used for **cross‑domain zero‑shot validation**.

Pairs of tweets linking to the same news article.

Used to verify that discovered geometric invariants generalize across domains.

---

### HaluEval

Used to evaluate the ability of the geometric model to detect **LLM hallucinations**.

The hypothesis is that hallucinations violate the **geometric corridor of legitimate semantic transformations**.

---

# 📁 Repository Structure

```
LiGroupsForTweetEmbeds.ipynb
```
Complete experimental pipeline including:

1. Embedding generation using SBERT
2. Stable affine operator estimation
3. Orthogonal + PCA regularization
4. Polar decomposition of the operator
5. XAI descriptor extraction
6. ROC‑AUC evaluation
7. Global vs Local transformation experiments
8. 3D visualization of the **Affine Tube**
9. Zero‑shot anomaly detection experiments

---

# ⚙️ Requirements

Python **3.9+**

Main libraries:

- numpy
- scipy
- scikit‑learn
- sentence‑transformers
- matplotlib
- seaborn
- pandas

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# 🧪 Experimental Pipeline

The notebook performs the following stages:

### 1. Embedding Generation
Tweets are encoded using:

Sentence‑BERT `all-mpnet-base-v2` (768‑dimensional embeddings).

All embeddings are **L2‑normalized** to place them on the unit hypersphere.

---

### 2. Affine Operator Estimation

A global affine operator

(A, t)

is estimated from paraphrase pairs using a **regularized least squares formulation** with:

- orthogonal Procrustes prior
- PCA‑based generator regularization
- truncated SVD stabilization

---

### 3. Geometric Decomposition

The learned operator is decomposed via **polar decomposition**:

A = R S

where

- **R** – rotation (structural transformation)
- **S** – deformation tensor

From this we derive interpretable **XAI descriptors**:

- rotation angle θ
- deformation index Def
- semantic chirality (det(A))
- shift magnitude ‖t‖

---

### 4. Hybrid Cosine Score

Paraphrase similarity is computed as

cos( normalize(Ax + t), y )

This metric allows comparison with the original SBERT cosine similarity.

---

### 5. Geometric Corridor Analysis

For each pair we compute a geometric profile:

(θ, Def, ‖t‖, det(A))

This defines a **semantic corridor** within which valid paraphrases lie.

---

### 6. Cross‑Domain Validation

The learned operator is evaluated on the **TURL dataset** without retraining.

This verifies that discovered geometric invariants are **model properties rather than dataset artifacts**.

---

### 7. Hallucination Detection

Using **HaluEval**, we test the hypothesis that hallucinations correspond to **out‑of‑manifold transformations**.

A simple geometric check detects **≈95% of hallucinated responses**.

---

# 📬 Contact

**Olexander Mazurets**  
Khmelnytskyi National University  

Email: mazuretso@khmnu.edu.ua
