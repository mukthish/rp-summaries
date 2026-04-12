The paper **"Graph Reasoning Paradigm: Structured and Symbolic Reasoning with Topology-Aware Reinforcement Learning for Large Language Models"** introduces a novel framework to improve the reasoning capabilities of Large Language Models (LLMs) by shifting from unstructured plain-text reasoning to a **structured, graph-based format**.

### **The Core Problem: Limitations of Textual Reasoning**

Current LLMs typically use **Long Chain-of-Thought (LCoT)** reasoning, which is primarily unstructured plain text. This creates several issues:

- **Evaluation Bottleneck:** Semantic evaluation of unstructured text is computationally expensive and difficult to control.
- **Inconsistent Reasoning:** Operations like "reflection" or "refinement" can occur randomly and inconsistently.
- **Reward Hacking:** During reinforcement learning, models may over-optimize for process-based rewards at the expense of final answer accuracy.

### **1. The Graph Reasoning Paradigm (GRP)**

GRP transforms the reasoning process into a **directed graph** where each step is explicitly defined and annotated.

- **Step-level Cognitive Labels:** Each reasoning node is assigned a specific cognitive operation, including **known** (problem conditions), **generate** (moving forward), **aggregate** (merging steps), **reflect** (reviewing), **refine** (improving), **reverse** (backward reasoning), and **associate** (analogies).
- **Node-based Representation:** Each node is a tuple containing a unique ID, parent IDs (dependency relations), and content.
- **Training:** The researchers constructed over **52k graph-structured reasoning chains** for mathematical and coding tasks and used **Supervised Fine-Tuning (SFT)** to help models internalize this paradigm.

### **2. PASC-GRPO: Topology-Aware Reinforcement Learning**

To further optimize the reasoning process, the authors propose **Process-Aware Stratified Clipping Group Relative Policy Optimization (PASC-GRPO)**.

- **Process-Aware Graph Rewards:** Instead of relying on expensive semantic evaluation, the system uses **topology-based rewards** to evaluate the reasoning graph:
    - **Structure Format:** Ensures the graph is well-formed (e.g., "known" nodes have no parents).
    - **Efficiency:** Uses **Connectivity** and **Effective Reasoning Subgraph (ERS)** rewards to discourage redundant "chatter" and fragmented reasoning.
    - **Quality:** Employs **Reachability** and **Reverse Search Consistency** (traversing backward from the answer to see if steps actually contributed) to ensure the logic leads to the goal.
- **Stratified Clipping Advantage Estimation (SCAE):** This mechanism prioritizes **task accuracy** over structural signals to prevent reward hacking. It treats structural rewards as **bonuses** for correct answers and **penalties** for incorrect ones, ensuring correctness remains the dominant objective.

### **Key Findings and Results**

The framework was tested on mathematical reasoning (e.g., GSM8K, MATH500, AIME) and code generation benchmarks (e.g., HumanEval, MBPP, LiveCodeBench).

- **Significant Gains:** The method consistently outperformed strong baselines, including LLaMA-3.1 and Gemma-3, especially on competition-level tasks.
- **Inference Efficiency:** PASC-GRPO effectively **reduced reasoning length** while simultaneously improving accuracy, demonstrating that more focused, structured thinking is more effective than long-winded text.
- **Generalization:** The paradigm showed strong effectiveness across both math and code domains, indicating its potential for diverse logic-intensive tasks.