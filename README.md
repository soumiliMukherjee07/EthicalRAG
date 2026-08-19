# EthicalRAG
Enforcing Ethical Prompt Engineering: An Integrated  Architecture for Bias Detection, Contextual  Compression, and Grounded Response Synthesis 

## Overview
This project presents an integrated AI pipeline designed to improve the ethical and factual reliability of Large Language Model (LLM) responses.
The system detects potentially biased prompts, automatically rewrites them into neutral formulations, retrieves relevant information from live web sources, performs semantic document retrieval using FAISS, compresses the retrieved context, and generates an evidence-grounded response using Qwen2.5-3B-Instruct.
A semantic grounding module additionally estimates the reliability of the generated response and provides a hallucination-risk warning.

## Key Features
- 🔍 Hybrid bias detection using semantic similarity and rule-based patterns
- ✏️ Automatic rewriting of biased prompts into neutral formulations
- 🛡️ Temporal guardrail for future-dated queries
- 🌐 Live web information retrieval using DuckDuckGo
- 🧠 Semantic document retrieval using FAISS
- 📦 Contextual compression of retrieved information
- 🤖 Grounded response generation using Qwen2.5-3B-Instruct
- 📊 Semantic grounding score for estimating response reliability
- ⚠️ Hallucination-risk warning
- 📈 Bias detection evaluation with accuracy, precision, recall and F1-score
- 📉 Confusion matrix and bias-score visualizations
- 📊 Pipeline dashboard for grounding and compression metrics
  
## System Architecture / Workflow
<img width="1484" height="724" alt="system_pipeline" src="https://github.com/user-attachments/assets/08f2984d-f3b4-4056-a310-632a70cff4a6" />

## Technologies Used
| Technology | Purpose |
|---|---|
| Python | Core implementation |
| Transformers | LLM loading and generation |
| Qwen2.5-3B-Instruct | Response generation |
| Sentence Transformers | Semantic embeddings |
| all-MiniLM-L6-v2 | Embedding model |
| FAISS | Vector similarity search |
| DuckDuckGo Search | Live web retrieval |
| Scikit-learn | Evaluation metrics |
| NumPy | Numerical computation |
| Pandas | Dataset processing |
| Matplotlib | Visualization |
| Regular Expressions | Rule-based bias detection |

## Models Used
### Language Model
**Qwen/Qwen2.5-3B-Instruct**
Used for:
- Prompt refinement
- Contextual compression
- Grounded response generation
### Embedding Model
**sentence-transformers/all-MiniLM-L6-v2**
Used for:
- Bias semantic similarity
- FAISS document retrieval
- Semantic grounding evaluation
  
## Dataset
The project uses the `tdavidson/hate_speech_offensive` dataset as a reference source for bias-related language.
Additionally, a curated evaluation benchmark containing:
- 10 biased prompts
- 10 neutral prompts
was developed to evaluate the hybrid bias detection approach.
The benchmark includes both explicit stereotypes and more subtle demographic assumptions.

## How It Works
Step 1 — Bias Detection
The query is analyzed using:
Sentence embeddings
Semantic similarity
Rule-based patterns
Protected-group terms

Step 2 — Prompt Refinement
If the risk score crosses the threshold, the prompt is automatically rewritten into a more neutral formulation while attempting to preserve its original intent.

Step 3 — Temporal Guardrail
Future-dated queries are halted instead of being passed through the retrieval and generation pipeline.

Step 4 — Live Retrieval
The refined query is sent to DuckDuckGo to obtain current web information.

Step 5 — FAISS Retrieval
The retrieved documents are embedded and indexed using FAISS, allowing the system to select semantically relevant documents.

Step 6 — Context Compression
The retrieved context is compressed before generation to remove redundant information and reduce prompt size.

Step 7 — Grounded Generation
The compressed context is passed to Qwen2.5-3B-Instruct to generate the answer.

Step 8 — Grounding Evaluation
The generated response is compared semantically against retrieved evidence. A lower similarity score results in a warning that the answer may require verification.

## Example
-->Neutral Query example:
<img width="1385" height="437" alt="image" src="https://github.com/user-attachments/assets/27be1c54-0f40-4e0f-b1a4-520056ec6fe9" />

-->Biased Query example:
<img width="1264" height="504" alt="image" src="https://github.com/user-attachments/assets/396870c2-26ad-4845-a6bf-35e4e8affe7c" />

## Results
<img width="655" height="629" alt="image" src="https://github.com/user-attachments/assets/5c3f4935-331c-431c-baa9-109da072835a" />

<img width="572" height="490" alt="image" src="https://github.com/user-attachments/assets/56db4a33-c6ca-446c-b58c-6810f135bcb2" />

<img width="789" height="490" alt="image" src="https://github.com/user-attachments/assets/df4bcb4b-9163-4bc9-ba6b-94baae15b7aa" />

<img width="1344" height="130" alt="image" src="https://github.com/user-attachments/assets/bff44c96-7bd6-4225-86b4-e0accbd7cb74" />

## Limitations
- The current implementation primarily supports English-language prompts.
- Bias detection depends partly on manually defined rules and reference anchors.
- The evaluation benchmark is relatively small.
- Live retrieval depends on the availability of internet search results.
- Semantic grounding is an approximate measure and does not guarantee factual correctness.
- The current implementation is primarily a proof-of-concept system.
  
## Future Improvements
- Multilingual bias detection
- Larger and more diverse evaluation datasets
- Domain-specific bias detection
- Improved factuality and hallucination evaluation
- More advanced retrieval and reranking techniques
- Improved prompt refinement strategies
- User-facing web interface
- Deployment as an API or interactive application
  
## References

1.C. Bura, P. K. Myakala, and A. K. Jonnalgadda, “Ethical Prompt Engineering: Addressing Bias, Transparency, and Fairness,”
International Journal of Research and Analytical Reviews (IJRAR), vol. 12, no. 1, pp. 145–152, 2025.

2. C. Shah, “From Prompt Engineering to Prompt Science With Human in the Loop,” Communications of the ACM, 2024.

3. J. White, Q. Fu, S. Hays, M. Sandborn, C. Olea, H. Gilbert, A. Elnashar, J. Spencer-Smith, and D. C. Schmidt, “A Prompt Pattern
Catalog to Enhance Prompt Engineering with ChatGPT,” arXiv preprint arXiv:2302.11382, 2023.

4. D. Lamba, “The Role of Prompt Engineering in Improving Language Understanding and Generation,” International Journal for
Multidisciplinary Research, vol. 6, no. 6, 2024.

5. P. Liu, W. Yuan, J. Fu, Z. Jiang, H. Hayashi, and G. Neubig, “Pre-train, Prompt, and Predict: A Systematic Survey of Prompting
Methods in Natural Language Processing,” ACM Computing Surveys, vol. 56, no. 7, 2023.

6. G. Jiang, Z. Ma, L. Zhang, and J. Chen, “Prompt Engineering to Inform Large Language Model in Automated Building Energy
Modeling,” 2024.

7. P. Lewis et al., “Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks,” in Advances in Neural Information Processing
Systems, vol. 33, pp. 9459–9474, 2020.

8. T. Davidson, D. Warmsley, M. Macy, and I. Weber, “Automated Hate Speech Detection and the Problem of Offensive Language,” in
Proceedings of the 11th International AAAI Conference on Web and Social Media, 2017.

9. Qwen Team, “Qwen2.5 Technical Report,” Alibaba Cloud, 2024.

10. Hugging Face, “Transformers Documentation.”
Available: https://huggingface.co/docs/transformers

11. Hugging Face, “Hate Speech Offensive Language Dataset.”
Available: https://huggingface.co/datasets/tdavidson/hate_speech_offensive

12. IBM, “Retrieval-Augmented Generation (RAG).”
Available: https://www.ibm.com/think/topics/retrieval-augmented-generation
