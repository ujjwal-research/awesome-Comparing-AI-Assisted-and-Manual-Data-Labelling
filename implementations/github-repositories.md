# Open-Source GitHub Implementations

This document catalogues open-source repositories and codebases that implement key algorithms, annotation workflows, and model backends for data labeling and quality verification.

---

## GitHub Implementations

1. **cleanlab/cleanlab**
   - **Repository:** [https://github.com/cleanlab/cleanlab](https://github.com/cleanlab/cleanlab)
   - **What it implements:** Official codebase implementing Confident Learning algorithms to automatically identify label noise, dataset errors, and annotator disagreements.
   - **Why it is relevant:** Provides the standard algorithmic framework for auditing label quality and evaluating human vs. model annotation reliability on scientific and ML benchmarks.

2. **allenai/deepfigures-open**
   - **Repository:** [https://github.com/allenai/deepfigures-open](https://github.com/allenai/deepfigures-open)
   - **What it implements:** Deep learning pipeline for distantly supervised extraction and bounding box localization of figures, tables, and captions from scholarly PDFs.
   - **Why it is relevant:** Implements large-scale automated data labeling for scientific documents without requiring manual human annotation.

3. **HumanSignal/label-studio-ml-backend**
   - **Repository:** [https://github.com/HumanSignal/label-studio-ml-backend](https://github.com/HumanSignal/label-studio-ml-backend)
   - **What it implements:** Server framework integrating machine learning models (including LLMs and custom classifiers) into Label Studio workflows.
   - **Why it is relevant:** Enables human-in-the-loop (HITL) pipelines by serving automated pre-annotations and dynamically updating models via active learning.

4. **modAL-python/modAL**
   - **Repository:** [https://github.com/modAL-python/modAL](https://github.com/modAL-python/modAL)
   - **What it implements:** Modular active learning framework for Python built on top of Scikit-Learn, supporting uncertainty sampling and query-by-committee strategies.
   - **Why it is relevant:** Demonstrates algorithmic strategies that minimize human labeling volume while optimizing annotation accuracy on scientific datasets.

5. **facebookresearch/segment-anything**
   - **Repository:** [https://github.com/facebookresearch/segment-anything](https://github.com/facebookresearch/segment-anything)
   - **What it implements:** Official implementation and checkpoints for the Segment Anything Model (SAM), a foundation model for promptable visual mask generation.
   - **Why it is relevant:** Serves as the primary automated pre-labeling engine for interactive, AI-assisted medical and scientific image annotation pipelines.
