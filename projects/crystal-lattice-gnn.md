---
layout: page
title: Crystal Lattice GNN Case Study
permalink: /projects/crystal-lattice-gnn/
---

# Crystal Lattice GNN: Physics-Informed Graph Neural Networks for Solid-State Systems

Predicting the thermodynamic stability and mechanical properties of crystalline materials traditionally requires computationally expensive Density Functional Theory (DFT) simulations. 

**Crystal Lattice GNN** is a deep learning pipeline that treats atoms as nodes and chemical bonds as edges, enforcing spatial constraints to predict material properties directly from crystal structures.

---

## 🔬 Modeling Periodic Boundary Conditions

Crystalline materials exist as infinite periodic structures repeating in three-dimensional space. Standard Graph Neural Networks fail here because they assume a localized, finite graph structure.

* **The Strategy:** The framework maps atomic coordinate tensors into fractional coordinates based on the system's unit cell lattice vectors. 
* **Edge Generation:** Edges are constructed using a dynamic radius-graph search that evaluates interactions across periodic boundaries. If an atom interacts with an image of another atom in an adjacent unit cell, a periodic boundary edge is generated, storing the directional offset vector ($R$).

---

## 🏗️ Message Passing Architecture

The network utilizes edge-conditioned convolutions where message vectors are regularized by atomic distances and spatial orientation:

* **Node Embeddings:** Initialized using discrete physical properties including atomic number, electronegativity, and valence electron configurations.
* **Continuous-Filter Convolution:** Distance vectors between nodes undergo a continuous filter generation step using Gaussian radial basis functions to capture continuous spatial variations.
* **Invariance:** The architecture explicitly enforces translational and rotational invariance to ensure that shifting or rotating the coordinates of a crystal lattice does not alter the predicted total energy.

---

*[View the source code, training logs, and dataset loaders on GitHub.](https://github.com/slam-wise/crystal-lattice-gnn)*