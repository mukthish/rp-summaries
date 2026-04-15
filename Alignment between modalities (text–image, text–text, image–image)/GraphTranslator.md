**GraphTranslator** is a novel framework designed to bridge the gap between pre-trained **Graph Models (GMs)** and **Large Language Models (LLMs)** to handle both pre-defined tasks (like node classification) and open-ended, instruction-based tasks. While traditional GMs excel at structured data but are restricted to pre-defined formats, GraphTranslator leverages the emergent reasoning and interactive capabilities of LLMs to provide a flexible, open-ended interface for graph data.

### **Core Components**

The framework consists of four primary modules:

- **Frozen Graph Model (GM):** A pre-trained model (e.g., **GraphSAGE**) that encodes the graph's structural and feature information into high-dimensional node embeddings.
- **Frozen LLM:** A large-scale language model (e.g., **ChatGLM2-6B**) that serves as the reasoning engine and user interface. It remains frozen during training to preserve its vast knowledge and reduce computational costs.
- **Translator Module:** A lightweight, trainable module that converts node embeddings into **"soft prompts"**—sequences of tokens that the LLM can interpret. This module uses cross-attention layers to extract language-relevant features from the graph embeddings.
- **Producer Module:** An auxiliary module that utilizes an LLM to construct **alignment data** by generating textual descriptions of node attributes, neighbor information, and model commonalities. These (node embedding, text description) pairs are essential for training the Translator.

### **Training Methodology**

GraphTranslator follows a **two-stage training paradigm** to bridge the modality gap:

1. **GM-Text Alignment:** The Translator is trained to align node embeddings with textual descriptions using contrastive, generative, and matching objectives.
2. **GM-LLM Alignment:** The Translator is fine-tuned to ensure its output tokens can be understood by the LLM as valid semantic prompts, allowing the model to follow human instructions based on graph data.

### **Key Performance and Findings**

The framework was evaluated on industrial (**Taobao**) and benchmark (**ArXiv**) datasets, with the following results:

- **Zero-shot Capability:** GraphTranslator significantly outperforms vanilla LLM-based methods in zero-shot node classification. It is particularly effective at identifying implicit information (e.g., "cat owners" based on related products) that raw text-only methods often miss.
- **Graph Question Answering (GQA):** The model excels in open-ended reasoning tasks, such as summarizing user interests and analyzing friendships.
- **Superior to Raw Text Prompts:** Unlike "Vanilla LLM" approaches that feed raw, noisy text into the prompt, GraphTranslator uses a **compact soft prompt** derived from embeddings. This reduces noise, avoids the attention disturbances caused by lengthy text, and maintains consistency in multi-turn dialogues.

In summary, **GraphTranslator** provides a unified perspective for graph learning by allowing a single model to perform traditional graph tasks with high precision while simultaneously enabling **interactivity and explainability** through natural language instructions.