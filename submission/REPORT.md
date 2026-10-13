# CrewAI Build Report

**Name:** Prabhudeep Kumar Karra
**Topic I used:** retrieval-augmented generation

## 1. What I changed

I changed the Writer agent's `backstory` in `main.py` from a general technical-writing description to a finance-director audience: "You write for a skeptical finance director who wants the bottom line, risks, and costs in plain language." I chose this change because the backstory is part of the context given to the agent, so it can influence tone and emphasis without changing the overall workflow.

I wanted to see whether changing the intended reader would make a difference that was easy to notice. The original output explains RAG in a general way, while the changed output adds an executive summary focused on costs, risks, and practical trade-offs. That distinction matters because a technical explanation and a decision-maker's summary serve different purposes. I left the agents' tasks and the order of the crew unchanged, so the main planned change was the audience described in the Writer's backstory. I expected a change in framing, not proof that the information was more accurate.

## 2. How CrewAI works

CrewAI organizes this program around agents, tasks, and a crew. An agent represents a role on the team; here, the Research Analyst gathers key facts and open questions, the Technical Writer explains the topic, and the Editor tightens the draft and marks claims that need sources. Each task says what its assigned agent should do and describes the expected output. The crew brings the agents and tasks together and uses a sequential process, so work moves from the research brief to the explainer and then to the edit. The program passes the topic into the tasks when it starts the crew.

The Writer's role, goal, and backstory give the model context for how to perform its task. I changed the backstory to describe a skeptical finance director as the audience. The Writer then emphasized practical concerns such as costs and risks in the second output. The overall task remained an explainer, but the audience context influenced what the writing highlighted. The two runs can still differ because the model does not produce identical text every time; the backstory steers the response rather than guaranteeing exact wording or correctness.

## 3. Evidence

Compare `explainer_run1.md` with `explainer_run2.md`. The first is a general explainer. The second includes an "Executive Summary for Finance Directors" with explicit cost, risk, retrieval-option, and bottom-line framing. The run logs are `run1_original.txt` and `run2_changed.txt`; both use the same topic, `retrieval-augmented generation`.

One thing that stood out was that the changed explainer made a specific claim that RAG reduces factual errors by roughly 15-30%, while the original included different benchmark percentages. Those figures are not established by this run, and the kit has no web access. I treated them as unverified claims that need checking against reliable sources, rather than assuming the more confident-sounding summary was correct. The two outputs also differ in wording and details, which is expected because model responses vary between runs.

## 4. Choosing a framework

For this assignment's research-to-explainer workflow, I would choose CrewAI because the work can be divided into clear roles and ordered tasks: research first, writing second, and editing last. The sequence is easy to understand, and the framework lets me describe each agent's responsibility without writing the control flow between every step myself. That makes it a reasonable fit for a content pipeline where each stage uses the previous stage's work.

The OpenAI Agents SDK would be a better fit for a lightweight assistant that decides which tool or specialist to use for a particular request. Its tools and hand-offs are useful for routing, but I would need to design the interaction differently for a fixed multi-stage writing pipeline. LangGraph would give me more explicit control over the steps, branches, and pauses for human approval, which would be valuable if the workflow needed review checkpoints or strict decision logic. In this small example, that extra control would mean more graph structure to define. My choice would depend on the project: CrewAI for a role-based sequence, the Agents SDK for routing and tools, and LangGraph when explicit control over the flow matters most.

## 5. Verification and AI use

The kit has no web access, so its factual claims come from the model rather than live research. In particular, check specific statistics and cost or accuracy claims in the explainers against reliable sources before relying on them.

I checked that the setup script completed with `CrewAI kit OK` and compared the two explainers to see whether the intended audience change was visible. That check shows a difference in framing, but it does not verify the factual claims. I have not independently confirmed the specific statistics in the generated text; those should be checked against reliable sources before being used as facts.

AI assistance used: GitHub Copilot helped with setup guidance, ran the provided setup check and both CrewAI runs, changed the Writer's backstory, and helped draft and organize this report. I reviewed the outputs and report draft. I will make sure the final wording reflects my own understanding and that any factual claims I keep are properly checked.
