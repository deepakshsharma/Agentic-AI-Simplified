# Chapter 5 – Large Language Models (Simplified)

## Learning Objectives
By the end of this chapter, you should be able to:
- Explain what large language models (LLMs) are and how they work.
- Understand tokenization, embeddings, and autoregressive generation.
- Describe prompting, context windows, and retrieval-augmented generation (RAG).
- Recognize strengths and limitations of LLMs.
- Identify common risks like hallucination, bias, and misuse.
- Explain how LLMs fit into enterprise AI systems and agent workflows.

---

## 1. What Are LLMs?
Large language models are neural networks trained on massive amounts of text.  
They predict the next token in a sequence, which allows them to generate text, answer questions, and summarize documents.  

---

## 2. Tokenization
Text is broken into tokens (words, subwords, or characters).  
Each token is mapped to an embedding vector.  
The model processes sequences of these embeddings.  

---

## 3. Autoregressive Generation
LLMs generate text one token at a time.  
Each new token depends on the previous ones.  
This allows coherent sentences but also means outputs can vary.  

---

## 4. Context Windows
LLMs can only handle a fixed number of tokens at once.  
This is called the **context window**.  
Longer documents require summarization or retrieval to fit within the window.  

---

## 5. Prompting
Prompts are instructions given to the model.  
The wording of a prompt affects the output.  
Example: “Summarize this report in 3 bullet points” vs “Write a detailed summary.”  

---

## 6. Embeddings
LLMs use embeddings to represent meaning.  
Similar words or phrases have embeddings close together in vector space.  
Embeddings are useful for search, clustering, and retrieval.  

---

## 7. Retrieval-Augmented Generation (RAG)
LLMs don’t store facts reliably.  
RAG improves accuracy by retrieving relevant documents and inserting them into the prompt.  
This grounds the model’s output in real data.  

---

## 8. Strengths of LLMs
- Can handle many language tasks without retraining.  
- Flexible: summarization, classification, translation, generation.  
- Adaptable: can be guided with prompts.  

---

## 9. Limitations of LLMs
- Hallucinations: generating false but confident-sounding text.  
- Bias: reflecting patterns in training data.  
- Sensitivity: small prompt changes can alter outputs.  
- Cost: large models require significant compute.  

---

## 10. Hallucination
LLMs may invent facts when they lack information.  
This is why grounding with retrieval or rules is essential in enterprise use.  

---

## 11. Bias
Training data may contain stereotypes or skewed information.  
LLMs can reproduce these biases unless mitigated.  

---

## 12. Misuse Risks
- Generating harmful or misleading content.  
- Automating tasks without oversight.  
- Overtrusting outputs without validation.  

---

## 13. Fine-Tuning
LLMs can be fine-tuned for specific domains.  
Example: legal documents, medical notes, customer support.  
This improves relevance but requires careful data handling.  

---

## 14. Prompt Engineering
Designing effective prompts is a skill.  
Techniques:  
- Clear instructions.  
- Examples (few-shot learning).  
- Constraints (e.g., “answer in JSON”).  

---

## 15. Evaluation
LLM outputs are evaluated with:  
- Accuracy (does it match ground truth?).  
- Relevance (is it useful?).  
- Fluency (is it readable?).  
- Safety (is it appropriate?).  

---

## 16. Enterprise Integration
LLMs are not standalone products.  
They need:  
- Retrieval systems.  
- Tool integration.  
- Guardrails and monitoring.  
- Human oversight.  

---

## 17. Agents vs LLMs
An LLM is a model.  
An agent is a system that uses LLMs plus tools, memory, and workflows.  
Agents can plan and act, not just generate text.  

---

## 18. Common Failure Modes
- Context overflow.  
- Wrong retrieval.  
- Misuse of tools.  
- Poor prompt design.  
- Lack of monitoring.  

---

## 19. Human Oversight
Humans should:  
- Approve high-risk outputs.  
- Monitor dashboards.  
- Validate structured responses.  
- Provide feedback for retraining.  

---

## 20. Mini Case Study
Example: Customer support assistant.  
- Retrieval finds policy documents.  
- LLM drafts response.  
- Agent validates with rules.  
- Human approves final message.  

---

## 21. Scaling Laws
LLM performance improves with more parameters, data, and compute.  
But costs rise quickly, so balance is needed.  

---

## 22. Key Takeaways
- LLMs predict tokens to generate text.  
- Prompts and context shape outputs.  
- Retrieval improves reliability.  
- Risks include hallucination, bias, and misuse.  
- LLMs are building blocks, not complete systems.  


---

## 23. Hands-on lab: decoding behavior

### Goal

Explore how decoding settings affect a next-token model.

### Tasks

1. Run the example with greedy decoding.
2. Generate five outputs with temperature `0.7`.
3. Generate five outputs with temperature `1.4`.
4. Set `top_k=2` and compare diversity.
5. Add a new sentence to the corpus and retrain.
6. Observe how one local data change affects continuation probabilities.
7. Evaluate a held-out sentence using perplexity.
8. Explain why lower perplexity on a tiny corpus does not imply general intelligence.

### Extension

Modify the tokenizer so punctuation becomes separate tokens. Compare vocabulary size and generated text.

### Expected learning

You should be able to explain:

- why generation is sequential;
- how local token probabilities produce complete text;
- how temperature changes sampling;
- how data distribution shapes output;
- why probability does not guarantee truth.

---

## 24. Architecture exercise: enterprise policy assistant

Design an employee policy assistant with these requirements:

- answer only from approved policy documents;
- show sources;
- respect employee permissions;
- support multiple languages;
- never change payroll or employment status;
- escalate legal or ambiguous questions;
- record an audit trail;
- meet a defined latency target.

Answer the following:

1. What belongs in the system prompt?
2. Which information should be retrieved rather than memorized?
3. How will retrieval enforce authorization?
4. What output schema will the model return?
5. Which questions require deterministic policy logic?
6. When must the assistant abstain?
7. How will the system detect prompt injection in retrieved text?
8. Which metrics will be monitored?
9. What information should never be logged?
10. What is the human escalation path?

---

## 25. Knowledge check

1. What does an autoregressive language model predict?
2. Why is tokenization required?
3. How does instruction tuning differ from pretraining?
4. What is in-context learning?
5. How do zero-shot and few-shot prompting differ?
6. What does temperature change during decoding?
7. Why is low temperature not a factuality guarantee?
8. What is the role of a context window?
9. Why should context be treated as a scarce workspace?
10. When should retrieval be used instead of fine-tuning?
11. Why can valid JSON still be operationally wrong?
12. What is prompt injection?
13. Why must permissions be enforced outside the model?
14. What is the difference between faithfulness and correctness?
15. Which capabilities turn an LLM application into an agentic system?

---

## 26. Interview questions

### Beginner

1. Explain an LLM in simple terms.
2. What is a token?
3. What is next-token prediction?
4. What is the difference between a base model and an instruction-tuned model?
5. What is a context window?
6. What is temperature?
7. Why do LLMs hallucinate?
8. What is few-shot prompting?

### Intermediate

1. Walk through the inference pipeline from text to generated token.
2. Compare prompting, retrieval, tool use, and fine-tuning.
3. Explain top-k and top-p sampling.
4. How would you design a structured-output workflow with validation?
5. What should be logged for an LLM request?
6. How would you evaluate a support-triage LLM?
7. Why can longer context reduce quality?
8. How would you mitigate prompt injection from retrieved documents?
9. Explain the difference between an LLM and an agent.

### Advanced

1. Design a model-routing layer for mixed low-risk and high-risk requests.
2. How would you evaluate whether a model upgrade is safe to release?
3. Design a multilingual, permission-aware enterprise knowledge assistant.
4. How would you separate model uncertainty from retrieval uncertainty?
5. What controls are needed before an LLM can call write-capable tools?
6. How would you manage context for a long-running agent workflow?
7. Explain how streaming affects safety and validation design.
8. How would you reduce cost without degrading critical-case recall?
9. Design an observability model that supports debugging without logging sensitive content.
10. When would you choose self-hosting over a managed model API?

---

## 27. Chapter summary

A large language model is a transformer-based model trained to predict and generate token sequences at scale. Its broad capabilities emerge from learning statistical structure across large datasets, then being adapted through instruction tuning, preference optimization, prompts, retrieval, tools, or fine-tuning.

The core generation loop is autoregressive: tokenize the input, compute a probability distribution, select the next token, append it, and repeat. Decoding controls such as temperature, top-k, and top-p influence diversity but do not guarantee truth. The context window supplies temporary working information, yet it must be actively managed for relevance, cost, latency, and security.

Prompting changes behavior in the current request. Retrieval supplies external knowledge. Fine-tuning changes model parameters for stable repeated patterns. These are complementary interventions, not substitutes for one another.

LLMs can produce fluent unsupported output because their objective is plausible continuation rather than verified truth. Reliable products therefore combine the model with authoritative sources, deterministic tools, structured validation, permissions, evaluation, monitoring, and human escalation.

Finally, an LLM is not automatically an agent. Agentic systems add goals, planning, tools, state, evaluation loops, termination conditions, and control mechanisms around the model. The next part of the handbook focuses on the first of those application layers: prompt engineering.

---

## 28. Next chapter

Chapter 6 begins Part II with prompt engineering. It will cover:

- role, task, context, constraints, output format, and quality checks;
- zero-shot, one-shot, and few-shot prompting;
- structured outputs;
- prompt debugging;
- reasoning and action patterns;
- prompt injection boundaries;
- evaluation and iterative refinement;
- reusable prompt templates for product and engineering workflows.
