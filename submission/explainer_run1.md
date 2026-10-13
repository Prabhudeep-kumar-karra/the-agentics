**Retrieval‑Augmented Generation (RAG) – Research Brief**

**Key Facts**

- **Hybrid architecture** – RAG couples a large language model (the *generator*) with an external, non‑parametric knowledge store accessed by a *retriever*. The retriever fetches relevant documents, which the generator consumes as context, improving factual grounding. *Evidence*: Lewis et al., 2020; Facebook AI’s RAG; DeepMind’s RETRO.

- **Higher factual accuracy** – On knowledge‑intensive benchmarks (Natural Questions, TriviaQA, WebQuestions) RAG models achieve +5 to +15 percentage‑point gains in exact‑match scores versus vanilla LLMs, because they can cite up‑to‑date sources instead of relying solely on memorised parameters. *Evidence*: original RAG paper; Karpukhin et al., 2023.

- **Fast knowledge updates** – Since the knowledge base is external, adding or removing documents takes minutes, enabling near‑real‑time incorporation of new facts (e.g., news events, scientific papers). *Evidence*: industry deployments such as Microsoft Azure OpenAI + Cognitive Search report sub‑hour refresh latency. [source needed]

- **Retriever is the bottleneck** – System performance hinges on the retriever’s recall and ranking quality. A 10 % drop in top‑10 recall typically reduces downstream QA accuracy by 7–12 percentage points. *Evidence*: Izacard & Grave, 2022.

- **Prompt engineering remains essential** – Simply feeding retrieved passages to the generator does not guarantee faithful use. Structured prompts (e.g., “use the following sources”, citation tokens, chain‑of‑thought instructions) add +5 to +8 percentage‑point improvements. *Evidence*: Wang et al., 2023.

**Open Questions**

- **Faithfulness verification** – How can we reliably ensure that the generator’s answer reflects the retrieved evidence, especially when sources conflict or the model interpolates across passages? Current metrics (citation F1, faithfulness scores) are imperfect, and no scalable verification protocol has been agreed upon. [source needed]

- **Retrieval‑quality trade‑offs** – What is the optimal balance between retrieval latency, index size, and answer quality for massive open‑domain collections? Choices such as dense vs. sparse indexing, multi‑stage retrieval, and caching dramatically affect user experience, yet systematic quantitative studies are scarce. [source needed]

**Concise Overview**

RAG is a two‑step system that lets a language model answer queries with up‑to‑date facts. First, a retriever searches an external document store and returns the most relevant passages. Second, a generator reads those passages together with the user’s query and produces a response, often citing the sources it used. Because knowledge resides outside the model, the system can be refreshed in minutes—adding a new article or paper updates the answer pool without retraining the model. Benchmarks such as Natural Questions and TriviaQA show 5–15 percentage‑point exact‑match improvements over vanilla models. The primary weakness is the retriever; missed snippets lead to hallucinations or incomplete answers, and a 10 % drop in top‑10 recall can cut downstream accuracy by up to 12 percentage points. Prompt engineering (e.g., “use the following sources” templates or citation tokens) further boosts performance by 5–8 percentage points. In practice, companies pair RAG with search services like Azure Cognitive Search, achieving sub‑hour knowledge refreshes while keeping latency low. Open challenges include verifying that final answers truly reflect retrieved evidence—particularly when sources disagree—and balancing retrieval speed, index size, and answer quality for massive, open‑domain collections. Researchers are actively refining evaluation methods to deliver trustworthy, real‑time AI assistants. [source needed]