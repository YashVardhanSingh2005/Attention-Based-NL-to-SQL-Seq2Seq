
# 🧠 Attention-Based NL-to-SQL Translator

This project implements a powerful Natural Language to Structured Query Language (NL-to-SQL) translation pipeline designed to generate accurate, executable SQL queries from complex user questions.

The core technology is an **Attention-Based Sequence-to-Sequence (Seq2Seq) model** built using TensorFlow/Keras. The project emphasizes robust preprocessing, advanced decoding, and domain-aware post-processing to ensure high performance and semantic correctness.

## 🚀 Key Features

* **Attention-Based Seq2Seq Architecture:** Utilizes an LSTM Encoder-Decoder model to handle long-range dependencies in complex NL queries. 
* **Robust Preprocessing:** Implements schema canonicalization (mapping synonyms to database names) and dynamic number masking (`<NUM0>`) to maximize model generalization.
* **Advanced Decoding:** Employs **Beam Search** (beam width=5) during inference, significantly increasing the probability of generating the most accurate target sequence.
* **Domain-Specific Post-Processing:** Features a rule-based layer that enforces SQL syntax, restores original numeric values, and applies heuristic corrections (e.g., correcting 'AGE' filters that semantically belong to 'DISBURSEMENT\_AMOUNT') to guarantee executable output.
* **High Performance:** Achieves a **99.2%** validation accuracy and an excellent **~0.75 BLEU score** on the validation set.

## ⚙️ Project Pipeline Summary

1.  **Data Preprocessing:** NL/SQL pairs are tokenized, padded, and large numbers are masked.
2.  **Model Training:** The Seq2Seq model is trained using Teacher Forcing with the Adam optimizer and Sparse Categorical Cross-Entropy loss.
3.  **Inference:** The trained model is split into separate Encoder and Decoder inference models. 
4.  **Prediction:** The `predict_sql` wrapper manages the entire pipeline, from NL canonicalization to final SQL cleaning.

## 🛠️ Technologies & Dependencies

* Python 3.x
* TensorFlow / Keras (Core ML framework)
* NumPy (Numerical Operations)
* Matplotlib (Visualization of Training History)
* `re` (Regular Expressions for Canonicalization and Post-Processing)

## 📄 Example Usage

**Input NL Query:**
`Show all clients with loans above 500,000 who are female.`

**Predicted SQL Query:**
`SELECT * FROM loans WHERE DISBURSEMENT_AMOUNT > 500000 AND gender = 'Female';`

---
**To Run This Project:**

1. Clone the repository.
2. Install dependencies (`pip install -r requirements.txt`).
3. Load the notebook (`nl_sql_generator.ipynb`) and execute the cells.
