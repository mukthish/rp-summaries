**Graph of Thoughts (GoT)** is a framework designed to advance the prompting capabilities of Large Language Models (LLMs) by modeling their reasoning process as an **arbitrary graph**. Unlike linear paradigms like Chain-of-Thought (CoT) or branching structures like Tree of Thoughts (ToT), GoT represents units of information ("LLM thoughts") as vertices and the dependencies between them as edges.

### **Core Methodology and Transformations**

The primary advantage of GoT is its ability to enable **non-linear reasoning** through specific graph-enabled transformations:

- **Aggregation:** Combining multiple arbitrary thoughts into a single synergistic outcome.
- **Refinement:** Iterating or looping over a specific thought to enhance and improve its content.
- **Generation:** Producing one or more new thoughts from an existing one, similar to previous schemes.
- **Backtracking:** Moving back from non-promising outcomes to explore new paths.

The framework is formally modeled as a tuple $(G, \mathcal{T}, \mathcal{E}, \mathcal{R})$, where $G$ is the reasoning process, $\mathcal{T}$ represents thought transformations, $\mathcal{E}$ is an evaluator function for scoring thoughts, and $\mathcal{R}$ is a ranking function to select the most relevant ones.

### **System Architecture**

GoT utilizes a modular architecture to coordinate the reasoning process:

- **Controller:** Coordinates the entire process using a **Graph of Operations (GoO)**, which defines the static execution plan, and a **Graph Reasoning State (GRS)**, which dynamically tracks the history and scores of all thoughts.
- **Prompter:** Encodes the graph structure and instructions into prompts for the LLM.
- **Parser:** Extracts information from the LLM's replies to update the reasoning state.
- **Scoring & Validation:** Assesses the quality of thoughts, sometimes consulting the LLM itself or human input.

### **The Latency-Volume Tradeoff**

Researchers propose a new metric, **thought volume**, which measures the number of preceding thoughts that could impact a given thought. GoT offers a superior tradeoff compared to other schemes, achieving **low latency** ($O(\log_k N)$) while maintaining **high volume** ($N$). This allows the model to incorporate a broader scope of information into a final solution without increasing the number of reasoning steps.

### **Key Performance and Findings**

GoT was evaluated across several use cases, including **sorting**, **set operations**, **keyword counting**, and **document merging**:

- **Accuracy and Quality:** On sorting tasks, GoT improved the quality of outcomes by approximately **62% over ToT** and ~70% over CoT.
- **Cost Efficiency:** Despite its complexity, GoT simultaneously reduced inference costs by **more than 31%** compared to ToT.
- **Problem Complexity:** The advantages of GoT become more pronounced as problem complexity and size increase.
- **Training-Free:** The framework requires **no model updates**, making it a resource-efficient approach compatible with various models like GPT-3.5, GPT-4, and Llama-2.