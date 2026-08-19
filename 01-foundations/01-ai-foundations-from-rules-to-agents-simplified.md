# Chapter 1 – AI Foundations: From Rules to Agents (Simplified)

## Learning Objectives
By the end of this chapter, you should be able to:
- Explain the difference between rules-based programming, machine learning, deep learning, LLMs, and agentic systems.
- Understand where rules, models, prompts, retrieval, tools, and memory fit in an AI product.
- Know when to use an agent and when a simpler design is better.
- Map a business problem to the right technical approach (not everything needs an LLM).
- Identify the control layers needed before an AI system is ready for production.

---

## 1. Why This Chapter Matters
AI terms are often mixed up.
- A rules engine might be called “AI.”
- A chatbot might be called an “agent.”
- An LLM might be treated as a full product.

These shortcuts cause design mistakes because each technology has different strengths, weaknesses, costs, and risks.

**Key idea:**
- A **model** is just one component.
- An **AI application** is a system.
- An **agent** is a system that can choose and execute actions toward a goal.

---

## 2. What is Artificial Intelligence?
AI is about building systems that perform tasks we associate with intelligence, such as:
- Recognizing patterns
- Predicting outcomes
- Understanding language
- Generating text, images, or code
- Ranking options and recommending actions
- Planning steps
- Using tools and adapting with feedback

👉 Important: This doesn’t mean software “thinks” like humans. It’s about observable capabilities and system design.

---

## 2.1 AI is an Umbrella Term
Different approaches solve different problems:

| Approach | How it Works | Output | Example |
|----------|--------------|--------|---------|
| Rules | Explicit logic | Deterministic action | Tax calculation |
| Machine Learning | Learns patterns from data | Prediction/score | Fraud detection |
| Deep Learning | Multi-layer neural nets | Embeddings, generation | Image classification |
| LLMs | Prompt + context | Generated text | Document summarization |
| Agents | Model + tools + state | Multi-step workflow | Support ticket triage |

---

## 3. Evolution: From Rules to Agents
Newer methods don’t replace older ones — they add more design options.
Example: A support agent might use:
- Rules for permissions
- Classifier for routing
- Embedding model for retrieval
- LLM for drafting
- Agent loop for tool calls
- Rules again for human approval

---

## 4. Conventional Programming: Explicit Rules
Developers write the behavior directly.
**Flow:** Input → Rules → Output

**Strengths:** predictable, testable, cheap, safe.  
**Limitations:** hard to scale, brittle with exceptions, doesn’t learn.  
**Best use:** when logic is stable, exact, and explainability is required.

---

## 5. Machine Learning: Learned Behavior
Instead of coding rules, we train models from data.
**Flow:** Data + Labels → Training → Model → Prediction

**Strengths:** learns complex patterns, scales better.  
**Limitations:** needs good data, can inherit bias, harder to explain.  
**Best use:** prediction, classification, ranking tasks.

---

## 6. Deep Learning: Representations
Neural networks learn features automatically from large data.
- Early layers: simple patterns.
- Later layers: abstract features.
- Output: embeddings (vectors that capture meaning).

👉 Embeddings become central in RAG (retrieval-augmented generation).

---

## 7. Large Language Models (LLMs)
**Flow:** Prompt → LLM → Generated Output

LLMs can: summarize, classify, answer questions, generate code, etc.  
But prompts are not deterministic code — wording changes matter, outputs vary, and hallucinations happen.  
LLMs need external context (retrieval, tools) for reliable enterprise use.

---

## 8. From LLMs to Agents
An agent is more than a single LLM call. It has:
- Goal/task
- Instructions/policy
- Model
- Planner
- Tools
- Memory/state
- Evaluator/guardrails
- Stop conditions

👉 Autonomy is a spectrum: suggest → draft → approve → bounded autonomy → high autonomy. Most enterprise systems start with low autonomy.

---

## 9. Modern AI System Stack
A production AI product includes:
- Application & UX layer
- Identity & permissions
- Orchestration (classify, dispatch, execute, persist, return)
- Prompt/context assembly
- Retrieval & memory
- Tool gateway
- Evaluation & guardrails
- Observability (logs, metrics, costs, failures)

---

## 10. Four Approaches
- Symbolic: rules, facts, graphs.
- Statistical: ML patterns.
- Generative: new content.
- Agentic: models + workflows.
👉 Robust systems often combine all four.

---

## 11. Worked Example: Support Triage
- Stage 1: Rules-only (predictable but limited).
- Stage 2: ML classifier (learns from history).
- Stage 3: LLM-assisted (understands language, but needs policy grounding).
- Stage 4: RAG-grounded (retrieves current policies).
- Stage 5: Agentic triage (multi-step workflow with approvals).

---

## 12. Additional Examples
- Supplier recommendation: combines rules, models, LLM, and human approval.
- Project coordination: agent checks tickets/messages, must show sources.
- Agent evaluation: score on task completion, correctness, compliance, clarity, latency.

---

## 13. Choosing the Simplest Approach
- Use rules when logic is exact.
- Use ML when prediction/classification is needed.
- Use LLMs for language tasks.
- Use agents for multi-step workflows.
👉 Principle: **Use the least autonomous design that meets the business goal.**

---

## 14. Failure Modes
Each layer adds risks:
- Rules: missing edge cases.
- ML: biased data.
- Deep learning: opaque features.
- LLM: hallucinations.
- Retrieval: stale/missing chunks.
- Tools: invalid calls.
- Memory: wrong persistence.
- Orchestration: loops, lost state.
- Multi-agent: circular delegation.
- UX: overtrust.

---

## 15. Human Oversight
- Human-in-the-loop: review before execution.
- Human-on-the-loop: monitor and intervene.
- Human-out-of-the-loop: only for low-risk, well-controlled tasks.
👉 Controls: interrupt, reset, abort.

---

## 16. Mini-lab: design the right architecture

### Scenario

A procurement team wants a system that recommends a supplier for each purchase request.

Available data:

- supplier prices;
- promised delivery dates;
- quality history;
- approved-supplier policy;
- live inventory data;
- contract constraints.

### Step 1: separate deterministic constraints

Examples:

- supplier must be approved;
- quality score must exceed a threshold;
- contract region must match;
- restricted materials require compliance review.

These should be enforced with rules.

### Step 2: identify prediction or ranking needs

A model might estimate:

- probability of on-time delivery;
- expected quality risk;
- likelihood of price variance.

### Step 3: identify language needs

An LLM can:

- interpret a free-text purchase request;
- summarize supplier tradeoffs;
- explain the recommendation.

### Step 4: identify agentic needs

An agent is justified if the system must:

- query multiple systems;
- compare candidates;
- handle missing data;
- request clarification;
- run policy checks;
- prepare an approval package.

### Step 5: define control points

Before any order is placed:

- verify policy compliance;
- show sources used;
- display confidence or uncertainty;
- require human approval above a cost threshold;
- log the final decision and evidence.

### Exercise

Create your own architecture using this template:

```text
Business objective:
Users:
Required data:
Hard rules:
Predictions:
Generative tasks:
Tools:
State or memory:
Human approvals:
Stop conditions:
Evaluation metrics:
```

---

## 17. Knowledge check

### Question 1

A system applies a fixed tax rule to a transaction. Which approach is most appropriate?

A. Agentic workflow  
B. LLM generation  
C. Deterministic software  
D. Multi-agent debate

**Answer:** C. The logic is known and should be exact.

### Question 2

A system predicts whether a delivery will be late using years of labeled shipment history. Which approach is central?

A. Machine learning  
B. Prompt engineering  
C. Rule-only software  
D. Conversational memory

**Answer:** A.

### Question 3

A system summarizes an uploaded policy document. What is the minimum likely design?

A. Full multi-agent hierarchy  
B. LLM application with the document in context  
C. Reinforcement-learning environment  
D. Rules engine only

**Answer:** B.

### Question 4

A system must inspect three data sources, request missing information, compare alternatives, and create an approval draft. What additional design concept is likely needed?

**Answer:** A controlled agentic workflow with tools and persistent state.

### Question 5

Why is an LLM not a complete AI product?

**Answer:** Because production behavior also depends on data access, context assembly, permissions, tools, state, validation, UX, monitoring, and operational controls.

---

## 18. Interview questions

### Foundation level

1. What is the difference between AI, machine learning, and deep learning?
2. How does rule-based software differ from a trained model?
3. What is the difference between training and inference?
4. What does an LLM generate?
5. What is an embedding?

### Practitioner level

1. When would you prefer deterministic code over an LLM?
2. How would you combine rules, ML, and LLMs in one system?
3. What turns an LLM application into an agentic system?
4. Why must tool calls be validated outside the model?
5. How would you measure whether an agent is useful?

### Architecture level

1. Design a support-triage system with current policy grounding and human escalation.
2. Where should authorization be enforced in an agent architecture?
3. How would you prevent duplicate side effects during retries?
4. What evidence should be logged for an agent decision?
5. How would you decide whether a workflow needs one agent, multiple agents, or no agent?

---

## 19. Chapter summary

- Conventional programming expresses behavior through explicit rules.
- Machine learning learns predictive patterns from data.
- Deep learning learns internal representations from unstructured inputs.
- Large language models generate language or structured outputs from prompts and context.
- Agentic systems add controlled multi-step action, tools, state, and termination logic.
- A model is only one component of a production AI system.
- Production architecture must include identity, permissions, orchestration, context, retrieval, tool validation, evaluation, guardrails, UX, and observability.
- New capabilities introduce new failure modes.
- The safest architecture is usually the simplest design that satisfies the business objective.

---

## 20. Source map

| Board page | Material used in this chapter |
|---:|---|
| 1 | Supplier recommendation example, evidence, confidence, and human-review options |
| 2 | Agent evaluation dimensions |
| 3 | Support-triage role, plan, and output |
| 4 | Project-coordination workflow and source transparency |
| 5 | Course-level learning objectives |
| 6-7, 49 | RAG as external grounding |
| 10, 47 | Responsible-AI pipeline |
| 15-18 | Orchestration concepts |
| 23-26 | Guardrails, controls, and edge cases |
| 28 | Application-layer responsibilities |
| 34 | Business problem to agentic RAG and production architecture |
| 42 | Prompt components that influence model behavior |
| 51 | Rules, training, neural networks, and LLM comparison |

---

## 21. Next chapter

**Chapter 2 - Machine Learning Fundamentals** will expand the training branch of the board's comparison. It will cover problem framing, supervised and unsupervised learning, features, labels, train/validation/test splits, evaluation metrics, overfitting, drift, and the relationship between predictive models and generative systems.
concept is likely needed?

Answer: A controlled agentic workflow with tools and persistent state.

Question 5
Why is an LLM not a complete AI product?

Answer: Because production behavior also depends on data access, context assembly, permissions, tools, state, validation, UX, monitoring, and operational controls.
---

## Interview Questions
Foundation level
What is the difference between AI, machine learning, and deep learning?
How does rule-based software differ from a trained model?
What is the difference between training and inference?
What does an LLM generate?
What is an embedding?
Practitioner level
When would you prefer deterministic code over an LLM?
How would you combine rules, ML, and LLMs in one system?
What turns an LLM application into an agentic system?
Why must tool calls be validated outside the model?
How would you measure whether an agent is useful?
Architecture level
Design a support-triage system with current policy grounding and human escalation.
Where should authorization be enforced in an agent architecture?
How would you prevent duplicate side effects during retries?
What evidence should be logged for an agent decision?
How would you decide whether a workflow needs one agent, multiple agents, or no agent?
---

## Chapter Summary
Conventional programming expresses behavior through explicit rules.
Machine learning learns predictive patterns from data.
Deep learning learns internal representations from unstructured inputs.
Large language models generate language or structured outputs from prompts and context.
Agentic systems add controlled multi-step action, tools, state, and termination logic.
A model is only one component of a production AI system.
Production architecture must include identity, permissions, orchestration, context, retrieval, tool validation, evaluation, guardrails, UX, and observability.
New capabilities introduce new failure modes.
The safest architecture is usually the simplest design that satisfies the business objective.
---

## Source map
Board page	Material used in this chapter
1	Supplier recommendation example, evidence, confidence, and human-review options
2	Agent evaluation dimensions
3	Support-triage role, plan, and output
4	Project-coordination workflow and source transparency
5	Course-level learning objectives
6-7, 49	RAG as external grounding
10, 47	Responsible-AI pipeline
15-18	Orchestration concepts
23-26	Guardrails, controls, and edge cases
28	Application-layer responsibilities
34	Business problem to agentic RAG and production architecture
42	Prompt components that influence model behavior
51	Rules, training, neural networks, and LLM comparison
---

## Next chapter
Chapter 2 - Machine Learning Fundamentals will expand the training branch of the board's comparison. It will cover problem framing, supervised and unsupervised learning, features, labels, train/validation/test splits, evaluation metrics, overfitting, drift, and the relationship between predictive models and generative systems.
---

