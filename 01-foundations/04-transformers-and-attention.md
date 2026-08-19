# Chapter 4 – Transformers and Attention (Simplified)

## Learning Objectives
By the end of this chapter, you should be able to:
- Explain why attention-based architectures replaced recurrent networks for many language tasks.
- Describe queries, keys, values, attention scores, masks, and weighted combinations.
- Explain self-attention and distinguish it from cross-attention.
- Describe multi-head attention and why multiple heads are useful.
- Explain positional encodings and why order information must be added explicitly.
- Identify the major components of a transformer block.
- Compare encoder-only, decoder-only, and encoder-decoder architectures.
- Explain causal language modeling, masked language modeling, and sequence-to-sequence training.
- Describe how autoregressive generation and key-value caching work.
- Recognize transformer limitations involving context length, latency, memory, and data quality.

---

## 1. Why Transformers Matter
Earlier models like RNNs and LSTMs processed sequences step by step.  
This caused two problems:  
- Training was slow because it couldn’t be fully parallelized.  
- Long-range dependencies weakened as information passed through many steps.  

Transformers solved this by letting every token directly compare itself with all others using **attention**.  
This made training faster, scalable, and the foundation of modern LLMs. 

---

## 2. The Sequence-Modeling Problem
Language meaning depends on context.  
Example: *“The technician placed the sample in the freezer because it was unstable.”*  
The word *“it”* could mean technician, sample, or freezer.  

Attention lets the model compare *“it”* with all possible references and decide the most relevant one.  
This is more powerful than bag-of-words or simple recurrent models. 

---

## 3. From Tokens to Vectors
Transformers work with numbers, not raw text.  
Pipeline: Text → Tokenization → Token IDs → Embeddings → Transformer layers.  

Embeddings start static but become **contextual** after passing through transformer layers.  
Example: *“bank”* in *“river bank”* vs *“investment bank”* will have different contextual embeddings. 

---

## 4. Attention Intuition
Attention is like a search inside the model.  
- **Query:** what a token is looking for.  
- **Key:** what each token offers.  
- **Value:** the information each token contributes.  

The model learns which tokens are most relevant and combines their values. 

---

## 5. Scaled Dot-Product Attention
Formula:  
**Attention(Q, K, V) = softmax((QKᵀ) / √dₖ) V**  

- Dot product measures similarity.  
- Scaling prevents unstable optimization.  
- Softmax converts scores into weights that sum to 1.  
- Output is a weighted average of values.  

Important: Attention weights show internal mechanics but are not full explanations of reasoning. 

---

## 6. Queries, Keys, and Values
In self-attention:  
- Q, K, V all come from the same sequence.  
- Separate projections allow tokens to play different roles (matching vs contributing content).  

Cross-attention:  
- Queries come from one sequence (decoder).  
- Keys and values come from another (encoder).  
Used in translation and multimodal systems. 

---

## 7. Worked Example
A toy example shows how tokens compare via dot products, apply softmax, and combine values.  
Real models use larger dimensions, multiple heads, residuals, and masks. 

---

## 8. Multi-Head Attention
Multiple heads allow the model to capture different relationships at once.  
Outputs are concatenated and projected back.  
More heads increase capacity but don’t always improve quality. 

---

## 9. Positional Information
Self-attention alone doesn’t know order.  
Transformers add positional encodings:  
- **Absolute (sinusoidal).**  
- **Learned embeddings.**  
- **Relative/rotary methods.**  

This ensures word order affects meaning. 

---

## 10. Masks
Masks control visibility:  
- **Padding mask:** ignores filler tokens.  
- **Causal mask:** prevents future tokens from being seen during training.  
- **Other masks:** enforce boundaries, local windows, or modality restrictions. 

---

## 11. Transformer Block
A block includes:  
- Normalization  
- Self-attention  
- Residual connections  
- Feed-forward network  

Attention mixes information across tokens; feed-forward transforms each token individually. 

---

## 12. Transformer Families
- **Encoder-only:** bidirectional context (e.g., BERT).  
- **Decoder-only:** causal generation (e.g., GPT).  
- **Encoder-decoder:** input → output transformation (e.g., translation).  

Choose architecture based on task shape. 

---

## 13. Training Objectives
- **Causal LM:** predict next token.  
- **Masked LM:** predict hidden tokens.  
- **Seq2Seq:** transform source → target.  
- **Contrastive:** bring related items closer in embedding space. 

---

## 14. Autoregressive Generation
Decoder-only models generate one token at a time.  
Strategies: greedy, sampling, top-k, nucleus, beam search.  
Key-value caching speeds up generation by storing past states. 

---

## 15. Context Windows
Defines how much input/output the model can handle.  
Larger windows allow longer documents but increase cost and risk of irrelevant context.  
RAG helps filter and insert only relevant evidence. 

---

## 16. Computational Characteristics
- Attention cost grows quadratically with sequence length.  
- Memory includes parameters, activations, caches.  
- Optimizations: quantization, efficient kernels, retrieval, batching, speculative decoding. 

---

## 17. Production Transformer Stack
A transformer is only one part of a system.  
Other responsibilities: authentication, permissions, retrieval, validation, monitoring, escalation. 

---

## 18. Enterprise Example
Support assistant workflow:  
- Identity check → retrieval → ranking → prompt assembly → transformer generation → validation → response/escalation.  
Shows why transformers need surrounding system controls. 

---

## 19. Common Misconceptions
- Attention ≠ human attention.  
- Models don’t store documents.  
- Large context ≠ no need for retrieval.  
- More parameters ≠ guaranteed better quality.  
- Attention weights ≠ full explanation.  
- Transformers ≠ deterministic reasoning engines. 

---

## 20. Failure Modes
- Context contamination.  
- Hallucination.  
- Position/length sensitivity.  
- Tokenization surprises.  
- Repetition/degeneration.  
- Prompt-data confusion.  
- Unbounded generation. 

---

## 21. Best Practices
- Choose architecture by task.  
- Separate model capability from permissions.  
- Manage context budgets.  
- Retrieve and filter evidence.  
- Monitor latency and quality.  
- Validate structured outputs.  
- Log and monitor drift. 

---

## 22. Runnable Example
The repo includes a Python script for scaled dot-product attention.  
It demonstrates matrix multiplication, scaling, masking, softmax, and weighted value combination.  
This is educational; production uses optimized tensor libraries. 

---

## 23. Hands-on lab: inspect attention behavior

### Goal

Use the provided Python example to understand how queries, keys, values, and masks change the output.

### Tasks

1. Run the example without a causal mask.
2. Enable the causal mask and compare the attention matrix.
3. Modify one key vector so that it strongly matches the first query.
4. Observe how the first output vector changes.
5. Replace one value vector while keeping its key unchanged.
6. Explain why the attention weight remains similar while the retrieved content changes.
7. Increase the vector dimension and verify that scaling affects the softmax distribution.

### Extension

Create a padding mask for a four-token batch where the final position is padding. Confirm that no query assigns weight to that position.

### Expected learning

The lab should make the distinction clear:

- keys control matching;
- values control contributed content;
- queries define what is sought;
- masks define allowed information flow.

---

## 24. Architecture exercise

Design the model-facing portion of a document summarization service.

Requirements:

- accept documents up to 200 pages;
- produce an executive summary and a detailed summary;
- preserve section references;
- support confidential documents;
- detect unsupported claims;
- complete within an agreed latency budget.

Answer these questions:

1. Would you place the entire document in one context? Why or why not?
2. Which work should be performed by the transformer, and which by the application?
3. How would you chunk and hierarchically summarize the document?
4. How would you preserve source mapping?
5. How would you validate the final summary?
6. What telemetry would you collect?
7. What should happen when the document exceeds supported limits?

---

## 25. Knowledge check

1. What problem does self-attention solve in sequence modeling?
2. What are the different roles of queries, keys, and values?
3. Why are attention scores divided by the square root of the key dimension?
4. How does self-attention differ from cross-attention?
5. Why does a transformer need positional information?
6. What does a causal mask prevent?
7. What is the purpose of a residual connection?
8. How do encoder-only and decoder-only architectures differ?
9. Why is generation sequential even though training can be parallelized across positions?
10. What does a key-value cache store?
11. Why can a large context window still require retrieval?
12. Which parts of an enterprise AI product are not the transformer's responsibility?

---

## 26. Interview questions

### Beginner

1. Explain attention using a non-mathematical analogy.
2. What is self-attention?
3. Why are positional encodings needed?
4. What is the difference between encoder-only and decoder-only transformers?
5. What does a causal mask do?

### Intermediate

1. Walk through scaled dot-product attention step by step.
2. Why are query, key, and value projections learned separately?
3. What is multi-head attention, and what benefit does it provide?
4. Explain the roles of attention, feed-forward layers, normalization, and residual connections.
5. Compare masked language modeling and causal language modeling.
6. Explain the key-value cache and its memory trade-off.
7. Why does standard attention become expensive for long sequences?

### Advanced

1. Design an inference service for long-context document analysis with strict latency targets.
2. How would you distinguish model latency from retrieval, routing, and tool latency?
3. What failure modes arise when untrusted retrieved text is inserted into the model context?
4. How would you evaluate whether a longer context window actually improves a production task?
5. Compare full attention, local attention, and retrieval-based context selection.
6. What controls are required before allowing a decoder-only model to invoke write-capable tools?
7. Explain why attention weights are not a complete explanation method.

---

## 27. Chapter summary

Transformers are sequence models built around attention. They create contextual representations by allowing each token to compare itself with other permitted positions and combine relevant value information.

The core mechanism uses learned query, key, and value projections. Dot-product scores are scaled, optionally masked, normalized, and used to combine values. Multi-head attention repeats this process in multiple learned subspaces. Positional methods introduce order, while residual connections, normalization, and feed-forward networks make deep transformer stacks trainable and expressive.

Encoder-only models are commonly used for understanding and representation tasks. Decoder-only models use causal masking for autoregressive generation. Encoder-decoder models transform one sequence into another through source encoding and cross-attention.

In production, the transformer is only one layer. Authentication, retrieval, permissions, state, validation, monitoring, safety, and human escalation belong to the complete system. This distinction becomes essential in later chapters on LLM applications, RAG, and autonomous agents.

---

## 28. Next chapter

Chapter 5 builds on this architecture to explain large language models, including:

- pretraining and next-token prediction;
- tokenization and vocabulary design;
- scaling and emergent capability;
- instruction tuning and preference optimization;
- prompting and in-context learning;
- hallucination and uncertainty;
- model selection and deployment;
- the transition from an LLM to an agentic system.
