**fs1** (factual simple test-time scaling) is a framework designed to improve the **factuality** of Large Language Model (LLM) reasoning by grounding it in **Knowledge Graph (KG) paths**. While large reasoning models (like DeepSeek-R1) excel at complex tasks, their "thinking" traces are not guaranteed to be factually correct; fs1 addresses this by conditioning reasoning on verifiable facts.

### **The fs1 Methodology**

The framework follows a three-stage distillation and training process:

- **Trace Sourcing:** Researchers distilled approximately 3.4K raw reasoning traces (**rt**) by querying large models like **QwQ-32B** and **DeepSeek-R1** with complex multi-hop questions.
- **KG-Grounding:** To remove inaccuracies, these traces were enhanced by providing the models with **linearized KG paths** retrieved from Wikidata. This produced 3.9K factually grounded traces (**fs1**) which were typically shorter and more definitive than the raw versions.
- **Fine-Tuning:** The framework uses these traces to fine-tune smaller, non-reasoning instruction-tuned models (such as Qwen2.5 and SmolLM2) using standard **Supervised Fine-Tuning (SFT)**.

### **Key Performance and Findings**

- **Significant Accuracy Gains:** Across six complex open-domain benchmarks (totaling 23.9K questions), the fs1-tuned Qwen2.5-32B model improved factual accuracy by **6–14 absolute points** (measured at pass@16).
- **Superiority in Complexity:** The fs1 approach is particularly effective for **difficult questions** requiring three or more hops on a KG path, where it consistently outperforms standard Chain-of-Thought (CoT) and raw reasoning traces.
- **Impact of Model Scale:** Smaller LLMs (below 1.7B parameters) showed the **most profound improvements** in single-pass inference. Larger models (32B) also benefited, though they relied less on explicit KG guidance due to their stronger inherent parametric knowledge.
- **Domain Strengths:** Analysis showed that fs1-tuned models excel at **numerical answer types** (dates, numbers) and specific domains such as video games, geography, and politics.

### **Significance of Test-Time Scaling**

The framework highlights the effectiveness of **parallel sampling** (generating multiple answers and checking if at least one is correct). By improving the quality of individual reasoning traces through fine-tuning, fs1 directly boosts the **upper-bound potential** of what LLMs can achieve during inference without needing to scale the number of model parameters.

In summary, fs1 demonstrates that anchoring the "thinking" process of LLMs to factual KG paths is a critical step in transforming them into reliable tools for **knowledge-intensive tasks**.