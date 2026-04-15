**Graph of Thoughts (GoT)** is a pioneering prompting framework designed to bolster the **multi-step logical reasoning** capabilities of Large Language Models (LLMs) like GPT-4. It addresses the limitations of existing techniques by modeling the reasoning process as a **directed cognitive graph**, where individual "thoughts" are represented as nodes and their relationships as edges.

### **Core Innovations**

The GoT framework distinguishes itself through three primary technical contributions:

- **Graph-Based Structure:** Unlike hierarchical methods like Tree of Thoughts (ToT), GoT eliminates inherent hierarchy among intermediate nodes, allowing for **potential relationships between any pair of thoughts**. Notably, the prompting approach often **initiates from the desired outcome** rather than the initial conditions, emulating how humans reason backward to solve complex problems.
- **Inspection Mechanism:** To ensure accuracy, GoT utilizes a **`Checker` function** composed of multiple linked inspectors. This mechanism is more rigorous than traditional voting or scoring systems because it calculates the probability of correctness for a specific path; a node is only deemed "returnable" if every path leading to it is unobstructed and verified.
- **Iterative Graph Updating:** GoT facilitates **graph reuse and efficiency** by continuously adding verified intermediate thoughts to a "condition sequence". This allows the model to re-input updated conditions for complex problems that require multiple rounds of traversal, significantly reducing redundant reasoning.

### **Key Performance and Findings**

The framework was evaluated against three escalating mathematical and logical challenges, consistently outperforming state-of-the-art (SOTA) methods:

- **24-Point Game:** GoT achieved an **accuracy of 97%**, approaching the human baseline of 98.5%. This represented a **23 percentage point improvement** over the previous SOTA, Tree of Thoughts.
- **High-Degree Polynomial Equations:** The method improved GPT-4's accuracy by **86%**. While LLMs often struggle with algebraic calculations, the GoT `Checker` function served as an effective error-correction tool, and accuracy reached **89%** when the model was granted access to a calculator.
- **Recursive Sequences:** For tasks involving deriving formulas for sequences, GoT provided a **56% accuracy boost** over standard GPT-4. It proved particularly effective when multiple rounds of graph updates were used to supplement known conditions.

In summary, GoT transforms the LLM reasoning process into a **dynamic, non-linear exploration**. By allowing thoughts to be interconnected and rigorously verified, it enables models to achieve near-human performance on tasks that standard input-output or sequential prompting cannot solve.