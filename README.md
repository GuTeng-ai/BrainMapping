# BrainMapping: A Deep Learning Framework for Cross-Species Brain Functional Mapping

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📖 Introduction

**BrainMapping** is a deep learning framework designed to address a core challenge in neuroscience: establishing a principled, interpretable, and bidirectional functional mapping between evolutionarily distant brains (e.g., human and rodent).

While rodents are the most important model systems in biomedical research, a significant explanatory gap separates the cellular-level insights gained from them and the whole-brain data acquired from non-invasive human neuroimaging. Our framework bridges this gap with a novel, cascaded three-stage model that learns and aligns the functional organization of brains across species.

## ✨ Core Features

The framework's core is a cascaded three-stage model designed to progressively and robustly achieve the cross-species mapping:

1.  🧠 **Stage 1: Discriminative Feature Learning**
    * A **shared-weight Transformer encoder** processes both human and rat rs-fMRI data, forcing the model to learn a common feature language from the outset.
   
2.  🔧 **Stage 2: Feature Refinement**
    * With the encoder weights frozen, features are refined by jointly optimizing two objectives:
        * **Self-Supervision**: The model learns the internal biological structure of ROIs by reconstructing masked voxel information.
        * **Biological Prior Regularization**: A contrastive loss based on the principles of **Functional Segregation and Integration (FSI)** encourages intra-network similarity and inter-network dissimilarity.

3.  🗺️ **Stage 3: Graph Matching Based Alignment**
    * A **Graph Convolutional Network (GCN)** first enriches the features with network-topological context.
    * An **optimal transport solver** (Sinkhorn algorithm) then uses these topology-aware features to compute the final bidirectional probabilistic assignment matrix, $\mathbf{P}$.
    * This process **jointly optimizes** for both feature-level similarity and global graph-structural consistency.
    * 
## 🚀 Getting Started
We will open source our BrainMapping project code as soon as possible after the paper is published.


