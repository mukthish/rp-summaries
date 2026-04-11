**AskGNN** is a novel framework designed to bridge the gap between sequential Large Language Models (LLMs) and complex **Textual Attributed Graphs (TAGs)** by leveraging **In-Context Learning (ICL)**.

### **The Core Problem: Structural Blindness**

The authors identify that while LLMs excel at processing unstructured text, they lack the innate ability to interpret the structural relationships (edges) fundamental to graphs. Current integration methods—such as text-based serialization (which misses long-range signals) or graph projection (which creates modality misalignment)—fail to fully capture the rich context inherent in TAGs.

### **The AskGNN Framework**

AskGNN addresses these gaps by transforming graph structural information into a small number of **document node-label pairs** that serve as ICL examples for the LLM. The framework consists of several key components:

- **Structure-Enhanced (SE) Retriever:** Unlike standard retrievers that rely solely on text similarity, the SE-Retriever uses a **Graph Neural Network (GNN)** to extract feature representations that incorporate both semantic and structural data. It identifies the most relevant labeled nodes for a query by calculating the cosine similarity of these GNN-extracted features.
- **Learning-to-Retrieve (L2R) with LLM Feedback:** This is a dynamic learning loop where the retriever is optimized based on the LLM's own performance.
    - The framework calculates a **"utility score"** for each example based on the **inverse of perplexity (PPL)**, quantifying how much an example helps the LLM reach a correct prediction.
    - The retriever is then fine-tuned using a loss function that combines this LLM feedback with traditional node classification objectives.

### **Key Findings and Results**

- **Consistent Superiority:** Across three major datasets (**ogbn-arxiv, ogbn-products, and arxiv2023**), AskGNN significantly outperformed bare GNNs, text-serialization methods, and standard ICL baselines like $k$-NN.
- **Data Efficiency:** The framework is highly effective in low-data scenarios, showing marked improvements even when training data is limited to 1% or 10% of labeled nodes.
- **Versatility Beyond Classification:** AskGNN demonstrated its flexibility by achieving state-of-the-art results in **link prediction** (predicting if two nodes are connected) and **conditional text generation** (generating missing text for a node).
- **Scaling Insights:** The study observed an "inverse scaling" phenomenon in some tasks, where very large models (e.g., 72B) were occasionally more prone to being misled by noisy ICL examples than mid-sized models (e.g., 32B).

### **Significance**

By using GNNs to select the "most insightful" examples for ICL, AskGNN allows LLMs to effectively utilize graph-structured data **without the need for extensive fine-tuning** or complex modality alignment. This establishes a new foundation for applying LLMs to sophisticated structured-data applications like social networks and recommendation engines.