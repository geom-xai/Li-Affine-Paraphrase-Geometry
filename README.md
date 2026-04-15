# LAG-XAI Notebook

This notebook reproduces the main computational pipeline for **LAG-XAI: A Lie-Inspired Affine Geometric Framework for Interpretable Paraphrasing in Transformer Latent Spaces**.

## What it does

- loads and preprocesses paraphrase data
- encodes texts with **Sentence-BERT (`all-mpnet-base-v2`)**
- estimates a global affine operator **(A, t)** from positive paraphrase pairs
- runs a manuscript-facing grid search over regularization parameters
- computes interpretable geometric descriptors:
  - **Theta_trace** (global operator angle)
  - **Deformation index**
  - **Determinant / chirality**
  - **Shift magnitude**
  - **Residual error**
- visualizes the **pairwise paraphrase corridor**
- supports qualitative transfer / anomaly checks on **TURL** and **HaluEval**

## Main angle mapping

Several angle-like quantities appear in the notebook. They are **not interchangeable**.

- **Theta_trace** → global operator angle used for the manuscript's **Table 2**
- **Theta_action** → auxiliary operator diagnostic used in notebook summaries
- **theta_pair** → direct pairwise angle between original and paraphrase embeddings, used for **Figure 5**
- **theta_local** → local case-study angle used only in qualitative XAI examples (**Table 3**)

## Manuscript-facing outputs

- **Table 2 branch**: manuscript-aligned grid-search results
- **Figure 5**: pairwise transformation angle histogram for Dev positives
- **Table 3**: qualitative local XAI audit
- **Table 5**: qualitative zero-shot TURL transfer audit
- **Table 6 / Figure 7 / Table 7**: HaluEval residual-error anomaly analysis

## Expected files

Typical saved outputs include:

- `tradeoff_analysis.png`
- `figure_pairwise_transformation_angle_distribution.png`
- `appendix_A6_bootstrap_stability_analysis.png`

Optional exploratory cells may also produce additional geometry diagnostics.

## Recommended execution order

1. setup and imports
2. dataset loading / preprocessing
3. SBERT embedding generation
4. core functions:
   - `algorithm_1_stable`
   - `algorithm_2_profile_stable`
   - `predict_hybrid_score`
5. manuscript-facing grid search / Table 2 branch
6. Figure 5 pairwise-angle cell
7. local qualitative XAI cases
8. TURL / HaluEval analysis
9. optional exploratory diagnostics

## Requirements

- Python 3.10+
- numpy
- pandas
- matplotlib
- seaborn
- scikit-learn
- scipy
- torch
- sentence-transformers

## Notes

- The **main manuscript angle** is **Theta_trace**, not **Theta_action**.
- **Figure 5** is based on **direct pairwise embedding angles**, not on the affine operator profile.
- **Table 3** is qualitative and illustrative, not the basis for the paper's main quantitative claims.
- If exploratory SO(n) / geodesic cells are kept in the notebook, treat them as auxiliary diagnostics unless the manuscript is rewritten around them.

## License

Add the repository license here if needed.
