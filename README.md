# Li-Affine-Paraphrase-Geometry
Affine Lie group modeling of paraphrase transformations in sentence embedding space (PIT-2015, SBERT).
# Paraphrases as Local Lie Transformations in Sentence Embedding Space

This repository contains the official implementation of the paper:

"Paraphrases as Local Lie Transformations in Sentence Embedding Space"

## 🔬 Overview

We propose an affine Lie group formulation of paraphrase transformations in high-dimensional embedding spaces. 

Instead of treating semantic similarity as a scalar (cosine similarity), we model paraphrasing as a locally isometric affine transformation:

T(x) = A x + t

where:
- A ∈ GL(n) models structural transformation
- t ∈ ℝⁿ models contextual shift

We demonstrate that:
- Paraphrasing is locally near-isometric (Def → 0)
- There exists a stable geometric rotation constant (~28°)
- The affine model preserves ~91.7% of SBERT’s nonlinear classification capacity

Dataset: PIT-2015 (SemEval-2015 Task 1)  
Embedding model: all-mpnet-base-v2 (SBERT)

---

## 📁 Repository Structure

- `LiGroupsForTweetEmbeds_1 (2).ipynb` — Full experimental pipeline
- Grid search optimization
- Affine operator estimation
- Polar decomposition
- XAI descriptors (θ, Def, Shift, det(A))
- ROC-AUC evaluation
- 3D Affine Tube visualization

---

## ⚙️ Requirements

Python 3.9+

Main libraries:
- numpy
- scipy
- scikit-learn
- sentence-transformers
- matplotlib
- seaborn

Install via:

```bash
pip install -r requirements.txt
