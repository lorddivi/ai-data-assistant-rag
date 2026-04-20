# AI Data Assistant (Hybrid RAG + Pandas)

# 1. What this project does
This project demonstrates a hybrid approach to building an AI-powered data assistant that can answer natural language queries over structured datasets by combining:

a. LLM-based query understanding

b. Pandas for deterministic computation

c. FAISS for semantic retrieval

# 2. Key Insights
Naive RAG approaches fail for analytical queries (e.g., totals, averages) due to limited context and hallucination.
This project addresses that by separating computation from reasoning.

# 3. Architecture
User Query --> LLM (Intent Extraction) --> Pandas (if calculation) --> RAG + LLM (if insights)

# 4. Limitations

a. Uses local LLM (Mistral) → limited reasoning quality

b. Query parsing may fail for complex prompts

c. Not production-ready (prototype for learning)

# 5. Future Improvements

a. Replace local LLM with stronger API models

b. Add structured output validation

c. Improve query parsing reliability

d. Add UI layer
