### **Why in not LLM?**

The paper focuses on Skill Graph construction. While the skill graph is used to pre train LLMs, it is not the focus of the paper.

---

The paper **"MASS: MAthematical Data Selection via Skill Graphs for Pretraining Large Language Models"** introduces a framework designed to significantly enhance the efficiency and effectiveness of pre-training Large Language Models (LLMs) specifically for **mathematical reasoning**,.

### **The Core Innovation: The Skill Graph**

Unlike traditional data selection methods that focus on surface-level linguistic quality (like grammar or noise reduction), MASS operates at a **deep semantic level** by focusing on the underlying "skills" (knowledge points) required to solve a problem. The framework constructs a **Skill Graph** where:

- **Nodes** represent specific mathematical skills (e.g., "Quadratic equations," "Integration by parts") extracted from a high-quality reference dataset (NuminaMath) using a strong LLM (Qwen2.5-72B),.
- **Edges** represent the **co-occurrence** of these skills in the same problem, capturing their compositional relationships,.

### **The Two-Step Methodology**

1. **Skill Graph Construction:** Skills are extracted via prompt engineering, merged for redundancy, and organized into a graph structure where each node's weight is determined by its frequency of occurrence,,.
2. **Data Scoring and Selection:**
    - **Similarity Computation:** The framework computes semantic similarities between the target text data and the skills in the graph.
    - **Graph Aggregation:** These similarity scores are aggregated through the graph's adjacency matrix. This ensures a data point gets a high score if it covers **important individual skills** and/or **rich compositional relationships** between skills,.
    - **Ranking:** The target dataset is ranked by these aggregated scores, and the top-performing subset is selected for training.

### **Key Findings and Performance**

- **Drastic Efficiency Gains:** Models trained on MASS-selected subsets can achieve the same performance as those trained on original datasets while using **50% to 70% fewer tokens**,.
- **Superior Accuracy:** When trained on the same amount of tokens, MASS-selected data improves model performance by **3.3% to 5.9%** across various mathematical benchmarks like GSM8K and MATH,.
- **Computational Efficiency:** The pre-processing steps (extraction, embedding, and graph construction) account for **less than 3%** of the total computational budget, making it highly practical for large-scale applications,.
- **Outperforming Baselines:** MASS consistently outperformed other state-of-the-art selection methods, including AutoDS, DSIR, and ProX, across different model sizes (1B and 7B),.

### **Why It Works**

The authors attribute the success of MASS to its ability to identify not just "clean" text, but **semantically effective** text. By using the graph to account for skill importance and complexity, the framework ensures the training corpus is dense with the specific reasoning patterns the model needs to master,.