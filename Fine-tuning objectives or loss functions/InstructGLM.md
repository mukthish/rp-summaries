The provided text introduces **InstructGLM (Instruction-finetuned Graph Language Model)**, a novel framework designed to bridge the gap between generative large language models (LLMs) and graph machine learning, positioning LLMs as potential foundational models for graphs without needing Graph Neural Networks (GNNs).

**1. Core Challenges Addressed**

- **Limitations of GNNs:** Traditional GNNs suffer from issues like over-smoothing, and their architecture lacks compatibility with large-scale generative models, making it difficult to process non-numeric raw data (like text or images) directly or integrate them into unified AI systems.
- **Complexity in Existing LLM Approaches:** Prior attempts to use LLMs for graphs often require training multiple models (combining GNNs and LLMs) or designing computationally heavy, graph-specific attention mechanisms that restrict the model's receptive field to local 1-hop neighbors.

**2. Key Innovations of InstructGLM** To overcome these barriers, InstructGLM eliminates complex graph-tailored attention mechanisms and instead uses natural language as a highly flexible and scalable medium to describe graph topology.

- **Natural Language Graph Prompts:** The framework uses rule-based, scalable natural language prompts to explicitly describe the multi-hop geometric structure of a graph (up to 3 hops) centered around a target node. These prompts intuitively convey intermediate connecting paths as well as node and edge meta-features.
- **Vocabulary Expansion:** To embed structural data into the LLM, InstructGLM expands the model's vocabulary by creating a unique token for every node. The embeddings for these new tokens are initialized using the graph's inherent node feature vectors (e.g., Bag-of-Words, TF-IDF, or OGB features).
- **Multi-Task Instruction Tuning:** The model (utilizing backbones like Flan-T5 or LLaMA) is fine-tuned to perform graph tasks strictly via a generative language modeling objective. To further enhance the LLM's understanding of graph topology, the framework pairs the primary node classification task with an auxiliary **self-supervised link prediction** task.

**3. Experimental Results & Performance**

- **State-of-the-Art Dominance:** InstructGLM achieved single-model state-of-the-art performance, surpassing all top-ranked GNN baselines (like DRGAT and RevGAT) and powerful Transformer-based graph learners across the ogbn-arxiv, Cora, and PubMed datasets.
- **High Data Efficiency:** The model showcased remarkable robustness in low-label scenarios. When tested on the PubMed dataset with only 60 labeled training nodes (a 0.3% label ratio), InstructGLM outperformed the best GNN baseline by 5.8% and the best Graph Transformer by 9.3%.
- **Ablation Findings:** Studies confirmed that the core innovations—incorporating multi-hop structural information into the text prompts and running the auxiliary link prediction task—were vital, providing massive performance gains compared to simply tuning the LLM on the raw text of the nodes.