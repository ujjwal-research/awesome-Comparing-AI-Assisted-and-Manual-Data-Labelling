# Benchmark Datasets for Data Labelling and Quality Auditing

This document catalogues key benchmark datasets used for evaluating AI-assisted pre-labelling accuracy, label error detection, distant supervision, and manual expert annotation quality across scientific and machine learning domains[cite: 1, 2].

---

## Datasets

1. **AbdomenAtlas 1.0 (Multi-Organ CT Segmentation)**
   - **Source:** [GitHub - MrGiovanni/AbdomenAtlas](https://github.com/MrGiovanni/AbdomenAtlas) | [Hugging Face Repository](https://huggingface.co/datasets/AbdomenAtlas/AbdomenAtlas1.0MiniBeta)
   - **Description:** A large-scale medical dataset featuring 5,195 abdominal CT scans (over 3.2 million slices) with voxel-level multi-organ annotations constructed through automated AI pre-labeling and human expert quality assurance[cite: 2].
   - **Application:** Used for benchmarking AI-assisted medical segmentation, active learning pipelines, and label-error estimation models (such as Quality Sentinel)[cite: 2].

2. **DeepFigures Benchmark (Scientific Document Parsing)**
   - **Source:** [GitHub - allenai/deepfigures-open](https://github.com/allenai/deepfigures-open)
   - **Description:** A large-scale scholarly corpus containing over 5.5 million distantly-supervised figure, table, and caption bounding box annotations induced automatically from open-access arXiv and PubMed PDF articles[cite: 2].
   - **Application:** Used for evaluating automated distant supervision accuracy against manual layout labeling in scientific document analysis[cite: 2].

3. **LabelErrors Benchmark Datasets (ML Test-Set Label Noise)**
   - **Source:** [GitHub - cleanlab/label-errors](https://github.com/cleanlab/label-errors) | [LabelErrors.com](https://labelerrors.com/)
   - **Description:** A curated verification benchmark tracking pervasive label errors and annotator noise across 10 standard ML test sets (including ImageNet, CIFAR, QuickDraw, and Amazon Reviews) validated via crowdsourced consensus[cite: 2].
   - **Application:** Evaluates algorithmic label-checking performance, confident learning formulations, and downstream model sensitivity to noisy human annotations[cite: 2].
