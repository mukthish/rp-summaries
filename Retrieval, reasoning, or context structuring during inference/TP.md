**Thought Propagation (TP)** is a training-free, "plug-and-play" prompting framework designed to enhance the complex reasoning abilities of Large Language Models (LLMs). The method addresses a critical limitation of existing approaches like Chain-of-Thought (CoT) and Tree-of-Thought (ToT): they **"reason from scratch,"** meaning they cannot reuse insights from similar problems and are prone to accumulated errors in multi-step reasoning.

### **The Three-Module Framework**

Inspired by human analogical reasoning, TP guides an LLM to explore related problems and apply their solutions to the current task through three modules:

1. **LLM Propose:** Given an input problem, the LLM generates a set of **analogous problems** that share similar characteristics. These problems are designed to provide reusable strategies or knowledge-intensive plans.
2. **LLM Solve:** The LLM solves both the original input problem and the newly proposed analogous problems using existing prompting methods (e.g., CoT).
3. **LLM Aggregate:** This module combines the results in two ways: it either reuses solutions from analogous problems to directly generate a **new solution** for the input task or derives a **high-level plan** to rectify errors in the initial reasoning steps.

### **Key Technical Features**

- **Multi-Layer Implementation:** TP can be stacked into $K$ layers, where the model leverages solutions from **$K$-hop analogous problems**. While 2-layer TP achieves the best performance, 1-layer TP is often preferred for balancing efficiency and token costs.
- **No External Knowledge Required:** Unlike other analogical methods that rely on large-scale databases or knowledge graphs, TP generates and solves analogies **internally** using the LLM's own parametric knowledge.
- **Compatibility:** TP is highly versatile and can be integrated with various LLM backends (GPT-3.5, GPT-4, PaLM-2) and specialized prompting methods like **ReAct** for autonomous planning.

### **Experimental Results and Use Cases**

The researchers tested TP across three challenging tasks, demonstrating significant improvements over standard baselines:

- **Shortest-path Reasoning:** In finding the optimal path through weighted undirected graphs, TP achieved an average **12% absolute increase** in finding optimal solutions. It proved much more effective than ToT, which often suffered from "searching backward" or hallucinations in dense graphs.
- **Creative Writing:** For generating coherent messages from random sentences, TP improved **human preference by 13%** and achieved the highest coherence scores on both GPT-3.5 and GPT-4 backends.
- **LLM-Agent Planning (ALFWorld):** TP enhanced task completion rates by **15%**. By reflecting on successful trials of similar tasks rather than just its own failures, TP proved superior to methods like **Reflexion**.

### **Conclusion**

Thought Propagation transforms the LLM reasoning process from a linear, error-prone search into an **analogical exploration**. By leveraging the "prior knowledge" of similar problem-solving experiences, it enables LLMs to refine sub-optimal results and maintain focus during long-trial planning tasks.