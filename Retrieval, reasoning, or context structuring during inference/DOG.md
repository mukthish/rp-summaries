**Decoding on Graphs (DOG)** is a training-free framework designed to enhance Knowledge Graph Question Answering (KGQA) by enabling Large Language Models (LLMs) to reason directly and faithfully on Knowledge Graphs (KGs). It addresses the limitations of existing methods—such as specialized retrievers that underutilize LLM reasoning or iterative prompting that is too complex for smaller models—by introducing a deep synergy between the LLM’s step-wise reasoning and the KG’s structural nature.

### **The Core Principle: Well-Formed Chains**

The foundation of DOG is the concept of a **"well-formed chain"**. A reasoning chain is considered well-formed if:

- **Factuality:** Every triplet in the chain exists in the actual KG.
- **Connectivity:** Each new triplet must grow from an entity that has already been visited or was mentioned in the original question.

These properties ensure that the reasoning trajectory is sound and grounded in the KG, which effectively eliminates hallucinations during the reasoning process.

### **Key Technical Components**

DOG achieves these well-formed chains through two primary mechanisms:

- **Graph-Aware Constrained Decoding:** Instead of relying on prompting alone, DOG imposes a hard constraint on the LLM's decoding process. It maintains a dynamic **query-centric subgraph ($G_q$)** that expands as reasoning progresses. By using a **trie** to track valid tokens, the system restricts the LLM's output vocabulary to only those tokens that can form a valid triplet within the current subgraph.
- **Beam Search Execution:** To prevent "error propagation"—where an irrelevant early step ruins the entire chain—DOG employs both token-level and **triplet-level beam search**. This allows the model to explore multiple plausible reasoning paths in parallel and retain the most confident chains based on their cumulative scores.

### **Performance and Advantages**

Experimental results across benchmarks like **WebQSP, CWQ, and 2Wikimultihop** demonstrate the framework's effectiveness:

- **State-of-the-Art Accuracy:** DOG consistently outperformed traditional retrieval-augmented baselines and even surpassed **StructLM**, a model specifically pre-trained on massive amounts of structured data.
- **Robustness Across KGs:** Unlike specialized retrievers that struggle when moved to a new KG (e.g., from Freebase to Wikidata), DOG utilizes the LLM's inherent textual understanding, making it highly adaptable to different graph taxonomies.
- **Compatibility with Compact LLMs:** While iterative prompting often requires massive models like GPT-4, DOG’s straightforward generation approach works exceptionally well with smaller, open-source models like **Llama-3.1-8B, Gemma-2-9B, and Qwen-2.5-7B**.
- **Mitigation of Logic Errors:** Detailed analysis showed that DOG's constrained decoding effectively "roots out" **ill triplets** (steps that break chain logic), leading to significantly higher-quality reasoning for complex, multi-hop questions.

In summary, DOG transforms the LLM into a graph-aware reasoner that "looks" at the topology of a KG to ensure every step of its logic is verifiable and connected, providing a more reliable and affordable alternative to specialized model training.