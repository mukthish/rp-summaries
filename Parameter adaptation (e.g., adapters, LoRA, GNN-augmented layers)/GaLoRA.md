The paper **"GaLoRA: Parameter-Efficient Graph-Aware LLMs for Node Classification"** introduces a modular framework designed to integrate structural information from **Text-Attributed Graphs (TAGs)** into Large Language Models (LLMs) efficiently.

### **The Core Problem**

Learning from TAGs requires representing both rich textual content and complex graph structures. While joint models (combining GNNs and LLMs) are effective, they are typically **computationally expensive and difficult to scale**. Previous methods like GLEM rely on noisy pseudo-labels, while others like GraphAdapter may limit the model's ability to adapt to specific semantic knowledge because the LLM remains entirely frozen.

### **The GaLoRA Framework**

GaLoRA (Graph-aware Low-Rank Adaptation) addresses these issues through a **two-phase, decoupled design**:

- **Phase 1: GNN Training:** A GNN (typically **GraphSAGE**) is trained on the TAG to extract structure-aware node embeddings. The model captures 1-hop neighborhood info (**Pass-1 embeddings**) and 2-hop info (**Pass-2 embeddings**) through successive message-passing layers.
- **Phase 2: LLM Fine-tuning with LoRA:** These structural embeddings are injected into a **frozen LLM** using **Low-Rank Adaptation (LoRA)**.
    - **Injection Strategy:** Pass-1 embeddings are injected into the **middle layers** of the LLM to help form context, while Pass-2 embeddings are injected into the **upper layers** to facilitate higher-level reasoning over a wider graph context.
    - **Learnable Gating:** A **learnable gate parameter ($\alpha$)** is used to balance the influence between the textual hidden states and the injected structural embeddings.

### **Efficiency and Performance**

- **Extreme Parameter Efficiency:** GaLoRA is highly efficient, requiring only **0.24% of the trainable parameters** compared to full LLM fine-tuning. It trains fewer than one million parameters even when using backbones like GPT-2.
- **Competitive Results:** Experiments on **ArXiv, Instagram, and Reddit** datasets show that GaLoRA performs on par with or better than state-of-the-art baselines like **GraphAdapter** and **GLEM**.
- **Resource Friendly:** Because it decouples GNN and LLM training, it significantly reduces training overhead, making it ideal for **resource-constrained settings**.

In summary, GaLoRA offers a scalable solution for node classification by allowing an LLM to "align" with both textual and structural information without the need for expensive joint backpropagation.