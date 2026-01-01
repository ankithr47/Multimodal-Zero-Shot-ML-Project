# Zero-Shot EEG Classification via Orthogonal Procrustes Alignment

This repository implements a **multimodal zero-shot learning (ZSL) system** for EEG-based object recognition. The objective is to classify **previously unseen object categories** by aligning neural EEG signals with semantic text embeddings—**without requiring labelled EEG training data for new classes**.

The project reframes EEG decoding as a **cross-modal retrieval problem**, where EEG-derived embeddings are matched directly against semantic class prototypes. A simple baseline is established, followed by a principled linear alignment that corrects domain shift between neural and semantic spaces.

---

## Key Contributions

- **Zero-Shot EEG Classification**
  - Reformulates EEG object recognition as cross-modal matching between EEG signals and semantic embeddings.
  - Enables generalisation to unseen object categories without collecting new labelled EEG data.

- **Baseline Model**
  - PCA-based dimensionality reduction of high-dimensional EEG features.
  - ℓ2-normalisation and cosine similarity nearest-neighbour matching.
  - Provides a transparent reference point for analysing cross-modal misalignment.

- **Orthogonal Procrustes Alignment**
  - Introduces a closed-form, SVD-based orthogonal alignment between EEG and semantic spaces.
  - Corrects systematic domain shift while preserving geometric structure.
  - Learned exclusively on seen classes, maintaining the zero-shot constraint.

- **Empirical Improvements and Analysis**
  - The proposed alignment achieves an approximate **1.7× improvement in Top-1 and Top-5 accuracy** on unseen classes relative to the baseline.
  - Improvements are corroborated across multiple evaluation views, including ranking-based metrics, error structure analysis, and embedding visualisation.

---

## Evaluation and Analysis

Model behaviour is assessed using a set of complementary metrics designed for zero-shot and retrieval-based settings:

- **Top-k Accuracy**
  - Evaluates whether the correct unseen class appears within the top-k retrieved candidates.
  - The aligned model shows a consistent relative improvement in both Top-1 and Top-5 accuracy, indicating more reliable semantic matching.

- **Cumulative Match Characteristic (CMC) Curves**
  - Measure retrieval performance as a function of rank.
  - The Procrustes-aligned model dominates the baseline across ranks, demonstrating improved global ordering of candidate classes rather than isolated gains at a single cutoff.

- **Confusion Matrices**
  - Used to analyse the structure of misclassifications on unseen classes.
  - Alignment leads to more structured and semantically coherent error patterns, with reduced concentration of predictions on a small subset of classes.

- **Hubness Analysis**
  - Examines the frequency with which certain class prototypes dominate nearest-neighbour predictions.
  - The aligned model exhibits a flatter predicted-class distribution, indicating reduced hubness and improved utilisation of the semantic space.

- **t-SNE Visualisations**
  - Provide qualitative insight into the geometry of EEG embeddings after alignment.
  - Aligned embeddings show improved organisation and reduced overlap, supporting the quantitative ranking improvements.

Taken together, these metrics indicate that the proposed alignment improves not only point accuracy but also the **overall retrieval quality, error distribution, and semantic consistency** of zero-shot EEG classification.

---

## Summary of Findings

- Orthogonal Procrustes alignment yields a **~1.7× relative improvement** in zero-shot retrieval accuracy on unseen classes.
- Gains are consistent across ranking metrics rather than isolated to a single threshold.
- Error analysis and visualisation confirm reduced hubness and improved cross-modal alignment.
- Improvements are achieved with a simple, interpretable, and parameter-free linear transformation.

---

## Reproducibility

- Alignment is learned strictly on seen classes.
- No unseen-class EEG data is used during training or validation.
- The method is deterministic and requires no iterative optimisation.
- All evaluation protocols adhere to standard zero-shot learning practice.

