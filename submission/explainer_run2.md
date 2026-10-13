**Retrieval‑Augmented Generation (RAG): Research Brief**

**Key Facts**

- **Hybrid architecture** – RAG pairs a large language model (the “generator”) with an external, non‑parametric knowledge store (the “retriever”). The retriever fetches relevant documents or passages, which the generator consumes as additional context.  
- **Improved factual accuracy** – Studies such as Lewis et al. (2020) and Izacard & Grave (2022) report higher precision on open‑domain QA and fact‑checking benchmarks (e.g., Natural Questions, TriviaQA) compared with vanilla LLMs of similar size, because the output can be grounded in up‑to‑date source material.  
- **Scalable knowledge updates** – Because the knowledge base is external, new information (e.g., recent news articles) can be added without retraining the language model, enabling near‑real‑time fact incorporation while keeping inference latency low.  
- **Retriever types** – Two dominant strategies are used: (1) **Sparse lexical retrieval** (e.g., BM25) for exact term matching, and (2) **Dense vector retrieval** (e.g., DPR, Contriever) for semantic similarity. Hybrid systems that fuse both often outperform either alone, especially on ambiguous queries.  
- **Training paradigms** – RAG can be trained end‑to‑end (joint fine‑tuning of retriever and generator) or in stages (pre‑train retriever, then fine‑tune generator). End‑to‑end training improves alignment between retrieved passages and generated text but is computationally expensive and sensitive to retrieval noise.

**Open Questions**

- **Mitigating retrieval‑induced hallucination** – Even with relevant documents, the generator may hallucinate or mis‑interpret content. Which training objectives, decoding constraints, or verification mechanisms can reliably ensure that the final output faithfully reflects the retrieved evidence?  
- **Optimal retrieval granularity and scaling** – The field lacks consensus on the ideal granularity of retrieved units (sentence vs. paragraph vs. whole document) and how this interacts with model size, latency budgets, and multimodal corpora. What principled methods can adapt granularity dynamically to balance relevance, cost, and answer quality?

---

**Executive Summary for Finance Directors**

Retrieval‑augmented generation (RAG) is a two‑step pipeline: a **retriever** searches an external document store (e.g., corporate wiki, news feed, regulatory database) and returns the most relevant passages; a **generator** reads those passages and produces the answer, using the retrieved text as evidence.

- **Higher factual accuracy** – Because answers are grounded in actual documents, RAG reduces factual errors by roughly 15‑30 % in open‑domain QA tests and catches outdated facts that pure generators miss. [source needed]  
- **Cost efficiency** – The language model remains static; only the knowledge base must be refreshed when regulations or market data change, eliminating costly retraining cycles. This separation saves compute dollars and time. [source needed]  
- **Retrieval options** – Cheap lexical methods (BM25) and more expensive dense vector search can be combined. Hybrid retrieval typically yields the best hit rate without inflating latency. [source needed]  
- **Risks** – The generator can still hallucinate, especially if the retriever returns irrelevant or low‑quality documents. Mitigation requires prompt engineering, verification layers, or end‑to‑end fine‑tuning, which adds engineering overhead.  

**Bottom line:** RAG offers a pragmatic way to keep AI‑generated answers current and reliable at modest compute cost, but it requires disciplined data curation and ongoing monitoring to keep hallucinations in check. [source needed]