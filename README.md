# BrainMapping: A Deep Learning Framework for Cross-Species Brain Functional Mapping

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📖 Introduction

**BrainMapping** is a deep learning framework designed to address a core challenge in neuroscience: establishing a principled, interpretable, and bidirectional functional mapping between evolutionarily distant brains (e.g., human and rodent).

While rodents are the most important model systems in biomedical research, a significant explanatory gap separates the cellular-level insights gained from them and the whole-brain data acquired from non-invasive human neuroimaging. Our framework bridges this gap with a novel, cascaded three-stage model that learns and aligns the functional organization of brains across species.

## ✨ Core Features

The framework's core is a cascaded three-stage model designed to progressively and robustly achieve the cross-species mapping:

1.  🧠 **Stage 1: Discriminative Feature Learning**
    * A **shared-weight BTEC encoder** (based on Transformers) processes both human and rat fMRI data, forcing the model to learn a common feature language from the outset.
    * Pre-training is performed via a **classification task** (using Additive Angular Margin Loss) to learn highly discriminable feature representations for each region of interest (ROI).

2.  🔧 **Stage 2: Feature Refinement**
    * With the encoder weights frozen, features are refined by jointly optimizing two objectives:
        * **Self-Supervision**: The model learns the internal biological structure of ROIs by reconstructing masked voxel information.
        * **Biological Prior Regularization**: A contrastive loss ($\mathcal{L}_{fsi}$) based on the principles of **Functional Segregation and Integration (FSI)** encourages intra-network similarity and inter-network dissimilarity.

3.  🗺️ **Stage 3: Graph-Based Alignment**
    * A graph model (KNN graph, with edges weighted by cosine similarity) is constructed for each species' feature space.
    * A **Graph Convolutional Network (GCN)** first enriches the features with network-topological context.
    * An **optimal transport solver** (Sinkhorn algorithm) then uses these topology-aware features to compute the final bidirectional probabilistic assignment matrix, $\mathbf{P}$.
    * This process **jointly optimizes** for both feature-level similarity and global graph-structural consistency.

## 🔬 Validation Highlights

Our framework was rigorously validated across multiple modalities and levels, demonstrating its efficacy, robustness, and biological plausibility.

### 1. Efficacy of Cross-Species Mapping
* **Functional Connectivity (FC) Pattern Preservation**: The mapping matrix $\mathbf{P}$ successfully preserves whole-brain and intra-network FC patterns bidirectionally.
* **Principal Functional Gradient Preservation**: The mapping preserves the macro-scale functional hierarchy (G1, G2), achieving a biologically meaningful alignment rather than a strict element-wise equivalence.
* **Network Topology Preservation**: The brain's essential "small-world" architecture is robustly maintained, preserving the balance of local segregation (high NC) and global integration (low NL).

### 2. Uncovering the Mapping Mechanism
* **A Balance of Alignment and Specificity**: Our core discovery is that before the final mapping with $\mathbf{P}$, the learned ROI features already achieve a key balance—they exhibit a **strong intrinsic alignment** (confirmed by low Wasserstein distance) while retaining **essential, macro-scale species-specificity** (confirmed by gradient-dependent correspondence and visualization).
* **Statistical Evidence**: The analysis of probability density functions (PDFs) for the shared gradients reveals that the distributional alignment strengthens for higher-order gradients, providing strong statistical evidence that our features align conserved functions while preserving macro-scale species-specificity.

### 3. Application: Decoding Functional Homology
* As a final functional test, a bidirectional, seed-based analysis confirmed that the whole-brain similarity map generated from a seed ROI accurately identifies its primary homologous region in the target species (e.g., human visual cortex to rat visual cortex), while also preserving the weaker, distributed connectivity patterns characteristic of brain-wide networks.



## 🚀 Getting Started

### Installation
```bash
# Clone this repository
git clone [https://github.com/your-username/BrainMapping.git](https://github.com/your-username/BrainMapping.git)
cd BrainMapping

# Install dependencies
pip install -r requirements.txt
```
## 📜 Citation
### If you use our framework or methods in your research, please cite our paper.
```
@article{YourLastName2025BrainMapping,
  title={BrainMapping: A Bidirectional Cross-Species Brain Mapping Framework},
  author={Your Name, et al.},
  journal={Journal of High-Impact Science},
  year={2025}
}
```

