# Optimizing Patch Selection in HMAX Using Genetic Algorithms

This repository implements a biologically inspired HMAX model for visual object recognition, enhanced with a Genetic Algorithm to optimize patch selection. While traditional HMAX models rely on randomly extracting intermediate features, this approach evolves a compact and highly informative subset of patches. This method reduces feature space dimensionality while improving classification accuracy.

## Model Architecture
The network simulates the primate ventral visual pathway through four alternating layers of simple (S) and complex (C) units:

* **S1 Layer (V1 Simple Cells):** Applies a bank of Gabor filters across 8 scale bands and 4 canonical orientations ($0^\circ, 45^\circ, 90^\circ, 135^\circ$) to detect low-level features like edges and bar.
* **C1 Layer (Complex Cells):** Performs a two-stage local max-pooling over the S1 feature maps. This step introduces tolerance to position and scale variations. 
* **Patch Extraction:** Intermediate representations are formed by extracting multi-channel patches (ranging from $4\times4$ to $16\times16$ pixels) from the C1 layer.
* **S2 Layer:** Functions as a radial basis function (RBF) layer. It calculates the Euclidean distance between the input C1 features and the stored prototypes (patches), applying either Gaussian or ReLU activation.
* **C2 Layer:** Applies global pooling (min or max, depending on the S2 activation) to produce a final, highly compact, and shift-invariant feature vector for classification.

## Genetic Algorithm Optimization
To eliminate redundant or irrelevant patches extracted from C1, a Genetic Algorithm is employed:
* **Representation:** Subsets of patches are represented as binary chromosomes.
* **Fitness Function:** The fitness of each chromosome is evaluated based on the classification accuracy of a SVM trained on the selected features.
* **Evolution:** Through iterative selection, crossover, and mutation, the population evolves to identify the most discriminative patches for object recognition.
