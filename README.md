# Large-scale Information Network Embedding Implementation

## Overview
This project implements a scalable information network embedding technique, with a particular emphasis on **first-order proximity**. Inspired by the [LINE (Large-scale Information Network Embedding) paper](https://arxiv.org/pdf/1503.03578.pdf), our aim is to efficiently capture direct connections between nodes in large-scale information networks. The goal is to generate embeddings that preserve both the structural and semantic properties of the network.

## Large-scale Information Network Embedding
LINE is designed to learn embeddings by preserving **first-order proximity** information within a network. In the context of LINE, first-order proximity refers to the relationships between a node and its immediate neighbors. The model optimizes an objective function that balances the likelihood of preserving the proximity of connected nodes and ensuring that unrelated nodes have distinct embeddings.

LINE’s focus on first-order proximity offers several advantages, particularly its scalability for handling large and complex networks (undirected, directed, and/or weighted). It efficiently captures the local structure of nodes, making it well-suited for tasks such as link prediction, node classification, and network visualization in large-scale information networks. The **edge sampling algorithm** used in LINE optimizes the objective function, overcoming the limitations of classical stochastic gradient descent (SGD), and significantly improving the effectiveness and efficiency of inference.

## Optimizations
To optimize the model, we initially employ a **batch alias sampler** for edge sampling, a technique widely used in graph-based machine learning tasks. The alias method is a probabilistic data structure that facilitates efficient random sampling. In the case of edge sampling, it is frequently used to select edges from a graph while preserving important structural properties.

Once a subset of edges is sampled, we iterate over them individually. For each edge, we draw **K negative samples** from the noise distribution $P_n(v) \propto d_v^{3/4}$ , where $d_v$ represents the degree of node $v$, as outlined in the original LINE paper. During each iteration, we update the embeddings for both the current node and the negative samples, optimizing the overall learning process.

