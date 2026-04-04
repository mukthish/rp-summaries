The paper **"Graph-enhanced Large Language Models in Asynchronous Plan Reasoning"** investigates the ability of Large Language Models (LLMs) to handle complex **asynchronous planning**—tasks requiring the optimization of time costs through both sequential and parallel actions,.

### **The AsyncHow Benchmark**

Because existing datasets were insufficient for this specific reasoning task, the authors developed **AsyncHow**, a benchmark containing **1.6K high-quality instances** of real-life tasks,.

- **The Task:** Given a set of steps, their durations, and ordering constraints, the model must calculate the **shortest possible time** to complete the task,.
- **Mathematical Grounding:** This is formally defined as finding the **longest path on a Directed Acyclic Graph (DAG)**,.
- **Data Sources:** The benchmark was automatically generated using data from **WikiHow** and **ProScript**, with LLMs (GPT-3.5 and GPT-4) serving as data annotators for time and dependency constraints,.

### **The Proposed Method: Plan Like a Graph (PLaG)**

The researchers found that standard prompting techniques (Zero-shot, k-shot, CoT) resulted in poor performance, especially as task complexity increased,. To address this, they proposed **PLaG**, a prompting technique that instructs models to treat planning problems as graph problems,. PLaG has two primary variations:

- **Explicit Graph:** The prompt includes a structured graph representation (like an adjacency list or matrix) for the model to reason over,.
- **Build-a-Graph (BaG):** The model is instructed to **first generate its own internal graph representation** of the natural language task and then use that graph to calculate the answer,.

### **Key Findings and Results**

- **Performance Boost:** PLaG consistently improved the performance of all tested models, including GPT-4, GPT-3.5, LLaMA-2-70B, and Mistral-7B,.
- **BaG Superiority:** For the most capable models (GPT-4 and GPT-3.5), the **BaG** method often outperformed explicit graphs, likely because generating the graph as an intermediate step makes it harder for the model to ignore the structural constraints,,.
- **State-of-the-Art:** GPT-4 combined with PLaG (BaG) achieved new **state-of-the-art results** on the AsyncHow benchmark,.

### **Limitations and Complexity**

The study highlights a significant "limit" to using LLMs as digital agents: **model performance degrades drastically as task complexity ($|V| + |E|$) increases**,,.

- Tasks with a complexity score of 18 or higher remain challenging even for the best models.
- Common errors include **parallelism failures** (failing to schedule multiple steps at once) and **time unit conversion errors**.
- The authors conclude that while graph-enhancement helps, LLMs are not yet robust enough to be deployed as fully autonomous agents for complex scheduling and optimization,,.