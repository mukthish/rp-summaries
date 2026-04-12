**FiDeLiS** (Faithful Reasoning in Large Language Models for Knowledge Graph Question Answering) is a **unified, training-free framework** designed to improve the factual accuracy and efficiency of Large Language Models (LLMs) when answering complex questions using Knowledge Graphs (KGs),,. It addresses the common trade-off in KG-enhanced systems between **faithfulness** (avoiding hallucinations) and **efficiency** (reducing computational latency),.

### **The Core Components**

The framework consists of two primary modules that work together to anchor LLM responses in verifiable reasoning steps,:

- **1. Path-RAG (Reasoning Path Retrieval-Augmented Generation):** This module pre-selects a constrained set of candidate entities and relations for each reasoning step,. It uses an LLM to extract **exhaustive keywords** from the query to maximize retrieval coverage,. A unique **scoring function** then balances immediate semantic relevance with the **structural connectivity** of the graph, ensuring the model considers paths with long-term potential,.
- **2. Deductive-Verification Beam Search (DVBS):** This module builds reasoning paths step-by-step using a beam search strategy guided by **LLM-generated planning**,,. At every step, it performs **deductive verification** to ensure the reasoning logically follows from previous steps and supports the original query,,. The search is **halted early** as soon as the question can be logically deduced from the retrieved facts, preventing excessive reasoning,.

### **Key Performance and Findings**

- **Superior Accuracy and Efficiency:** FiDeLiS consistently outperformed strong training-free and fine-tuning baselines (such as ToG and RoG) across multiple benchmarks, including **WebQSP and CWQ**,. It reduced runtime costs by approximately **1.7x** compared to similar training-free methods like ToG,.
- **Handling Long-Tail Knowledge:** The framework was tested on **CR-LT-KGQA**, a benchmark specifically targeting obscure, long-tail entities,. FiDeLiS proved highly effective in these scenarios where LLMs typically fail due to a lack of internal parametric knowledge.
- **Improved Faithfulness:** Error analysis of existing models like RoG showed that 33% of their reasoning steps were invalid (containing format errors or non-existent facts),. By using **verifiable KG steps** and deductive logic, FiDeLiS ensures that each step in a reasoning chain actually exists in the KG,.
- **Enhanced Interpretability:** By anchoring every answer in a traceable, step-by-step reasoning path from the KG, the framework allows users to **verify and understand** the logic behind the LLM's output,,.

In summary, FiDeLiS provides a scalable and **training-free solution** that transforms the LLM into a more reliable reasoning agent by using KGs as a verifiable foundation for its logic,,.