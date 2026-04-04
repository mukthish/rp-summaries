### **Why in not LLM?**

LoRA is used to fine tune GNN

---

The paper **"GraphLoRA: Structure-Aware Contrastive Low-Rank Adaptation for Cross-Graph Transfer Learning"** introduces a parameter-efficient framework designed to adapt pre-trained Graph Neural Networks (GNNs) to new, diverse graph domains.

### **The Core Problem**

While GNNs are powerful, they face significant challenges in **transfer learning** due to discrepancies in node features and structural distributions between source and target graphs. Simply transferring a well-trained GNN often leads to **negative transfer** (suboptimal performance) or **catastrophic forgetting** of universal knowledge when fully fine-tuned on a new dataset. Furthermore, real-world target graphs often suffer from **label scarcity**.

### **The GraphLoRA Framework**

GraphLoRA addresses these issues by freezing the pre-trained GNN and injecting a small, tunable GNN alongside it, inspired by the **Low-Rank Adaptation (LoRA)** technique used in large language models. The framework consists of three primary modules:

- **Node Feature Adaptation Module:** This module aligns divergent node feature distributions using a novel **Structure-aware Maximum Mean Discrepancy (SMMD)**. Unlike standard MMD, SMMD utilizes **graph diffusion** (Personalized PageRank) to incorporate global structural information, ensuring that feature mapping preserves local homophily.
- **Structural Knowledge Transfer Learning Module:** To bridge structural gaps, the framework injects a low-rank GNN whose weight updates are decomposed into two smaller matrices ($A$ and $B$). This is coupled with a **graph contrastive loss** that maximizes mutual information between the frozen and tunable GNNs to facilitate smooth knowledge transfer.
- **Structure-aware Regularization:** To handle cases with very few labels, the authors introduce a regularization objective based on the **homophily principle** (the tendency of connected nodes to share labels). This allows the model to learn from the inherent structure of the target graph even when supervision is scarce.

### **Key Findings and Performance**

- **Theoretical Expressive Power:** The authors theoretically demonstrate that a low-rank adapted GNN can exactly approximate any target GNN under mild conditions, proving its robust representational capability.
- **Efficiency:** GraphLoRA is highly parameter-efficient, achieving state-of-the-art results by tuning only **7% to 20% of the total parameters**.
- **Superior Performance:** In extensive experiments across eight real-world datasets (including citation and co-purchase networks), GraphLoRA outperformed 14 baselines. It showed an average improvement of **10.12%** over direct transfer methods and was particularly effective in **10-shot settings**, where labels are extremely limited.
- **Mitigating Forgetting:** The method proved highly effective at retaining source-domain knowledge, showing significantly less performance decline than full fine-tuning when tested back on the original source graph.