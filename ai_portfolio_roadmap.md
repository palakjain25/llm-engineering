# AI Engineering Portfolio Roadmap

> A personal build plan — projects in the right order, honest gaps, and a prioritized fix list.
> The goal is not perfection. It's a credible, working base to start applying while continuing to improve.

---

## Part 1 — Project Build Order

### Why order matters
Evals first, everything else second. Without a measurement layer, no other project can make a
quantitative claim — and quantitative claims are what separate "I followed a tutorial" from
"I built something."

---

### 1. LLM Evals — Build First
**Source:** *How to Systematically Setup LLM Evals (Metrics, Unit Tests, LLM-as-a-Judge)*

**What it covers:** LLM-as-judge, unit tests for LLMs, precision/recall, A/B testing framing,
the analyze-measure-improve cycle.

**Why first:** This is the foundation. Every project that comes after needs a measurement layer.
Build this first so you can say "X improved by Y%" in every subsequent project — that's the
difference between a tutorial and a project.

**The one thing to add:** Build a small golden eval set on a domain you care about (healthcare QA,
clinical notes, anything). Even 50 question-answer pairs. Reference it in every project after this.

---

### 2. Hybrid Search RAG — Build Second
**Source:** *The Complete Guide to Hybrid Search in RAG (BM25 + Embeddings + Reranker)*

**What it covers:** BM25, dense embeddings, Reciprocal Rank Fusion (RRF), reranking, retrieval
evaluation.

**Why second:** RAG is the most asked-about topic in AI engineer interviews. Hybrid search
(BM25 + dense + reranker) is the right level of sophistication — not just "I called the
embeddings API." Because you now have evals, you can measure: BM25-only vs dense-only vs hybrid.
That comparison is the project.

**The one thing to add:** Use your own domain data. Even a small public healthcare or pharma
dataset makes this far more relevant to your background and more memorable to a hiring manager.

---

### 3. Agentic RAG from Scratch — Build Third
**Source:** *Building Agentic RAG From Scratch in Pure Python*

**What it covers:** Tool use, structured outputs, semantic vs agentic RAG distinction, agent
debugging, production considerations.

**Why third:** Natural progression from Project 2. You go from "retrieval pipeline" to "agent
that decides when and how to retrieve." Building it in pure Python (not LangChain) is a
deliberate signal — it shows you understand what's happening under the hood.

**Resume story:** "Built a RAG pipeline, then extended it into an agentic system with tool use
and structured outputs." That's a progression, not a list of disconnected things.

---

### 4. Self-Learning Agent with Memory — Build Fourth
**Source:** *How to Build Self-Learning AI Agents (Python Tutorial)*

**What it covers:** Mem0 framework, Qdrant for long-term memory, memory management challenges,
open-source vs cloud memory options.

**Why fourth:** Adds the memory dimension to your agent from Project 3. Mem0 is a fairly
high-level abstraction on its own — the way to make this stronger is to connect it to the
agentic RAG system. Now you have an agent that retrieves *and* remembers across sessions.
That's a coherent system, not two separate tutorials.

**Honest critique:** This is the weakest standalone project of the six. Its value is as an
extension of Project 3, not as an independent piece.

---

### 5. LLM Fine-Tuning — Build Fifth
**Source:** *End-to-End LLM Fine-tuning Tutorial (from data to model to live demo)*

**What it covers:** SFT (supervised fine-tuning), data formatting, training loop,
HuggingFace upload, Gradio demo, batch inference.

**Why fifth:** Fine-tuning is valuable on a resume but also the most commoditized tutorial
topic right now. What makes it credible: (a) your own task and data, and (b) a before/after
eval comparison using the eval set from Project 1.

**The one thing to add:** Fine-tune on something healthcare-adjacent — clinical notes, medical
QA, SOAP notes. You already have real background here (hallucination detection pipeline,
AZ oncology NLP). Generic fine-tuning on a standard dataset is forgettable. Domain-specific
fine-tuning with a measured improvement is not.

---

### 6. Document Review App — Build Last (or skip for now)
**Source:** *Build a Document Review App in 3 Hours (Python, React, Azure)*

**What it covers:** Azure Document Intelligence, FastAPI, SQLite, React frontend, Azure
Container Apps deployment.

**Why last:** Most "full-stack" of the six, but least differentiated for AI Engineer roles.
Closer to a solutions architect or MLOps project. Good engineering, but the signal-to-time
ratio is low if your target is Applied Scientist or AI Engineer. Move it up the list if
targeting ML platform or product-engineering roles.

**When to build it:** After the first five are done and on your resume. Treat it as a bonus
that shows deployment and system integration skills.

---

## Part 2 — What's Missing

These are topics not covered by the six projects above, ordered by how often they come up
in interviews and job descriptions for AI Engineer / Applied Scientist roles.

| # | Gap | Why It Matters |
|---|---|---|
| 1 | Prompt Engineering as a discipline | Comes up in every interview; none of the projects treat it systematically |
| 2 | Observability & Tracing | Production signal; shows you've thought about debugging in real systems |
| 3 | Chunking Strategy & Index Design | Upstream of retrieval; most RAG failures start here |
| 4 | RAG Failure Modes & Guardrails | Hallucination detection, faithfulness scoring — you have real experience here |
| 5 | Structured Outputs & Tool Calling at depth | Interviewers probe this hard; Project 5 only touches it |
| 6 | Vector Database internals | HNSW vs IVF, distance metrics, filtering — expected knowledge |
| 7 | Context Window Management | Long-context handling, summarization chains, what to do when context overflows |
| 8 | Multi-turn Conversation Handling | History compression, session state — Project 4 is close but too abstracted |
| 9 | Security & Safety basics | Prompt injection, PII handling — especially relevant given healthcare background |
| 10 | CI/CD for ML | Eval-gated deploys, experiment tracking, model versioning |

---

## Part 3 — Priority Fix List

The goal here is maximum resume impact for minimum new build work. Most of these are
additions to existing projects, not new projects from scratch.

---

### Priority 1 — Add Observability to RAG (one afternoon)
**Gap closed:** #2 Observability & Tracing

**What to do:** Add LangSmith or Langfuse tracing to your Hybrid RAG project (Project 2).
Log every retrieval call, every LLM call, latency, token counts.

**Why first:** Takes a few hours. Immediately upgrades an existing project. Shows production
mindset. Every AI Engineer job description mentions observability.

**Resume line:** "Instrumented RAG pipeline with LangSmith — traced retrieval latency,
token usage, and LLM call patterns across 200+ eval queries."

---

### Priority 2 — Add Chunking Comparison to RAG (half a day)
**Gap closed:** #3 Chunking Strategy & Index Design

**What to do:** Add a section to your RAG project that compares fixed-size vs semantic vs
hierarchical chunking. Run each against your golden eval set and report the numbers.

**Why second:** Chunking is where most RAG systems actually fail. Showing you thought about
it — and measured the tradeoffs — is a strong signal. The eval set from Project 1 makes
this possible.

**Resume line:** "Compared three chunking strategies (fixed 512-token, semantic, hierarchical)
against a 50-query golden set; hierarchical improved recall@5 by 14%."

---

### Priority 3 — Formalize Prompt Engineering (one focused session)
**Gap closed:** #1 Prompt Engineering as a discipline

**What to do:** Pick one project (the RAG system is a good candidate) and write a short
document or notebook that shows: (a) your baseline prompt, (b) two or three variations you
tested (chain-of-thought, few-shot, structured output prompting), (c) what your eval set
said about each.

**Why third:** This is not a new project — it's documentation of decisions you already made.
But it shows a hiring manager that you think about prompts the way an engineer thinks about
code: something to version, test, and improve.

---

### Priority 4 — Add Failure Mode Analysis to RAG or Fine-tuning (one day)
**Gap closed:** #4 RAG Failure Modes & Guardrails

**What to do:** Add a notebook to either your RAG or fine-tuning project that explicitly
tests for hallucination (faithfulness scoring), context relevance, and answer relevance.
RAGAS is a good library for this.

**Why fourth:** You have real professional experience here (SOAP notes hallucination detection
pipeline). This is the one gap where your actual work history gives you a head start.
Formalizing it in a portfolio project makes that experience visible to someone who hasn't
seen your LinkedIn.

---

### Priority 5 — Deepen Structured Outputs & Tool Calling (a few hours)
**Gap closed:** #5 Structured Outputs & Tool Calling at depth

**What to do:** Extend the Agentic RAG project (Project 3) to include explicit JSON schema
definition for tools, validation of model output against the schema, and error handling when
the model returns malformed output.

**Why fifth:** This is a common interview question and a common production failure mode.
Adding proper schema validation to an existing agent project is a small change with high
signal.

---

### Priority 6 — Add Vector DB Design Notes (documentation, not code)
**Gap closed:** #6 Vector Database Internals

**What to do:** Add a design section to your RAG project README that explains: why you chose
your distance metric, what index type you used (HNSW), and what tradeoffs you'd consider
at larger scale (IVF, quantization). This doesn't require building anything new — just
showing you know the concepts.

---

### Priority 7 — Context Window Management (add to fine-tuning or agentic RAG)
**Gap closed:** #7 Context Window Management

**What to do:** Add a section to your agentic RAG project that handles the case where
retrieved context exceeds the context limit. Implement a simple summarization fallback
or a sliding window approach.

---

### Priority 8 — Security & Safety section (one notebook)
**Gap closed:** #9 Security & Safety basics

**What to do:** Add a short notebook demonstrating prompt injection awareness and PII
detection/redaction before LLM calls. Given your healthcare background, PII handling
in clinical text is a natural fit and will be distinctive.

---

### Priorities 9 & 10 — Multi-turn Handling and CI/CD
**Gaps closed:** #8 and #10

These are real gaps but they require more effort and have lower immediate resume ROI than
the above. Build them after everything else is in place:

- **Multi-turn:** Extend the memory agent (Project 4) with explicit history compression
  and session state management, replacing the Mem0 abstraction with something you control.
- **CI/CD for ML:** Add a GitHub Actions workflow to your RAG project that runs your golden
  eval set on every commit and fails the build if recall@5 drops below a threshold.
  This is the "eval-gated deploy" pattern and it's a strong portfolio signal.

---

## Summary — The One-Page View

```
Build Order          Gap Priority (Fix Order)
────────────         ──────────────────────────────────────────────
1. Evals             P1. Add observability to RAG        (afternoon)
2. Hybrid RAG        P2. Add chunking comparison to RAG  (half day)
3. Agentic RAG       P3. Formalize prompt engineering    (one session)
4. Memory Agent      P4. Add failure mode analysis       (one day)
5. Fine-tuning       P5. Deepen structured outputs       (few hours)
6. Doc Review App    P6. Vector DB design notes          (documentation)
                     P7. Context window handling         (add to P3)
                     P8. Security & safety notebook      (one day)
                     P9. Multi-turn conversation         (after above)
                     P10. CI/CD eval gating              (after above)
```

> Remember: a one-paragraph README per project answering — *what problem, what approach,
> what tradeoff you made, what you measured* — matters more than the code itself.
> That paragraph is what gets read first.
