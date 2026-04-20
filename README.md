# AI Data Assistant (Hybrid RAG + Pandas)

## 🚀 Overview

This project explores the limitations of naive Retrieval-Augmented Generation (RAG) systems for analytical queries and proposes a hybrid architecture that separates deterministic computation from LLM-based reasoning.

The system allows users to ask natural language questions on structured datasets (CSV) and intelligently routes the query to:

* **Pandas** → for accurate numerical computations
* **LLM (Mistral via Ollama)** → for insights and reasoning
* **FAISS (Vector DB)** → for semantic retrieval

---

## ⚠️ Problem with Naive RAG

Traditional RAG systems fail for analytical queries due to:

* Limited context (top-k retrieval returns only a few rows)
* Hallucinated numerical outputs
* Inability of LLMs to reliably perform calculations
* Row-level embeddings leading to irrelevant context

Example failure:

> Query: *"Total sales by region"*
> ❌ LLM generates fabricated numbers based on incomplete context

---

## ✅ Proposed Solution

This project introduces a **hybrid architecture**:

* LLM is used only for **query understanding (intent extraction)**
* Pandas performs **deterministic computations**
* RAG is used only for **insight generation (non-numeric queries)**

---

## 🧠 Architecture

```
User Query
   ↓
LLM (Intent Extraction → JSON)
   ↓
IF calculation → Pandas (accurate result)
ELSE → FAISS (retrieve context) → LLM (generate insights)
```

---

## 🧪 Example Execution

### Query:

```
Total sales in East region
```

### Parsed Output (LLM):

```json
{
  "operation": "sum",
  "column": "Sales",
  "filters": {"Region": "East"}
}
```

### Pandas Execution:

```python
df[df["Region"] == "East"]["Sales"].sum()
```

### Output:

```
125000
```

---

### Insight Query:

```
Give sales insights
```

### Flow:

* FAISS retrieves relevant summary chunks
* LLM generates insights

### Output:

```
1. East region shows strong sales performance  
2. Technology category is growing rapidly  
3. Profit varies significantly across regions  
```

---

## ⚙️ Tech Stack

* Python
* Pandas
* FAISS (Vector Search)
* Sentence Transformers (Embeddings)
* Ollama (Local LLM Runtime)
* Mistral (LLM)

---

## 📂 Project Structure

```
ai-data-assistant-rag/
│
├── data/
│   └── sample_dataset.csv
│
├── src/
│   ├── main.py
│   ├── utils.py
│
├── README.md
├── requirements.txt
```

---

## ▶️ How to Run

1. Install dependencies:

```
pip install -r requirements.txt
```

2. Start Ollama:

```
ollama run mistral
```

3. Run the project:

```
python main.py
```

---

## 💡 Example Queries

* Total sales
* Average profit by category
* Sales in East region
* Give sales insights
* Top performing category

---

## ⚠️ Limitations

* Uses local LLM → limited reasoning quality
* Query parsing may fail for complex prompts
* No strict JSON validation (LLM output can be inconsistent)
* Not production-ready (prototype for learning and experimentation)

---

## 🔮 Future Improvements

* Replace local LLM with API-based models (GPT / Claude)
* Add structured output validation
* Improve query parsing reliability
* Add UI (Streamlit / Web app)
* Support SQL-based execution

---

## 💼 Key Learning

* Naive RAG is not suitable for analytical queries
* LLMs should not be trusted for numerical computation
* Hybrid systems (LLM + deterministic tools) are more reliable
* System design matters more than model choice

---

## 📌 Conclusion

This project demonstrates how combining LLMs with traditional data tools leads to more reliable and interpretable AI systems, especially for structured data analysis tasks.

---

## 👤 Author

Divyansh Pandey
