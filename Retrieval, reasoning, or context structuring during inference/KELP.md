**KELP (Knowledge Graph-Enhanced Large Language Models via Path Selection)** is a three-stage framework designed to improve the factual accuracy of Large Language Models (LLMs) by incorporating external knowledge from Knowledge Graphs (KGs). It addresses two major limitations of existing prompt-engineering methods: the **lack of flexibility** in binary (yes/no) knowledge selection and the tendency of LLMs to ignore **indirectly related knowledge** that could still be impactful.

### **The Core Methodology**

KELP functions through a pipeline that identifies, encodes, and selects the most useful knowledge paths for a given question:

- **Knowledge Path Extraction:** The system identifies entities in the input question and extracts all **1-hop and 2-hop paths** originating from those entities within the background KG. These paths serve as the initial pool of candidate knowledge.
- **Sample Encoding:** KELP uses a specialized **path-text encoder** (based on DistilBert) fine-tuned on a latent semantic space. This encoder transforms both the question and the paths into embeddings to quantify their "usefulness" based on similarity scores.
- **Fine-Grained Path Selection:** To ensure the prompt remains concise and diverse, the framework applies **two coverage rules ($k1$ and $k2$)**. These rules allow for a flexible adjustment of the amount and variety of knowledge introduced, ensuring the selected paths are the most representative and least redundant.

### **Key Technical Innovations**

- **Potentially Impactful Knowledge:** A central contribution of KELP is its ability to capture knowledge that is **not directly semantically related** to the question but still helps the LLM generate a correct answer. The framework achieves this by training the encoder on a dataset of "positive" samples—paths that specifically corrected an LLM's previous factual error.
- **Relation-Only Ranking:** To handle massive, dense KGs where encoding every path would be too slow, KELP offers an alternative strategy that ranks paths based solely on their **relations**. This significantly improves efficiency by reducing the number of candidate sentences requiring full encoding.

### **Performance and Findings**

- **Superior Accuracy:** Experiments on **MetaQA** (strong semantic links) and **FACTKG** (weak semantic links) showed that KELP consistently outperformed standard LLM-based evidence methods like KG-GPT.
- **Robustness in Few-Shot Settings:** KELP proved to be highly stable across different numbers of "shots" (4, 8, and 12-shot configurations). It particularly excelled in scenarios with **limited examples**, where its ability to identify impactful knowledge provided a stronger performance boost than manual prompt engineering.
- **Correction of Hallucinations:** By providing grounded context, KELP effectively reduced the "hallucination problem" where LLMs generate plausible-sounding but factually incorrect information.

In summary, KELP transforms KG-augmented prompting from a rigid, binary selection process into a **flexible, scored alignment** that identifies hidden logical connections to improve LLM reasoning.