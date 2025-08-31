# Coherence Scoring Prototype

This repository contains a lightweight prototype function that fuses **biometric signals (HRV)** and **linguistic signals (text snippets)** into a single **coherence score (0–100)**. The goal is to design a simple, interpretable scoring mechanism that balances physiological reliability with textual heuristics.

---

## Problem Statement

**Goal:**  
Design a function that integrates HRV values and short text snippets into a coherence score between 0 and 100, accompanied by a one-line explanation.

**Inputs:**  
- HRV value (integer, e.g., `65`)  
- Baseline HRV value (integer, e.g., `75`)  
- Text snippet (short sentence, e.g., `"I think I can handle this, but I feel a little nervous."`)  

**Output (JSON):**
```json
{
  "coherence_score": 72,
  "explanation": "HRV is 13% below baseline; text contains nervous language → moderate coherence."
}
```

**Requirements:**  
- Normalize HRV relative to baseline (collapse >20% should reduce score).  
- Apply a text heuristic (e.g., “unsure/nervous” → lower score; “confident/clear” → higher score).  
- Fuse both signals with weights summing to 1.  
- Return a coherence score (0–100) and a concise explanation.  
- Lightweight, explainable, ~3–4 hours prototype.  

---

## Repository Structure
- `coherence_score.ipynb` — Core implementation of HRV + text scoring functions.  
- `data_analysis.ipynb` — Exploratory analysis, visualizations, sensitivity checks.  

---

## Dependencies
- Python 3.9+  
- pandas, numpy  
- matplotlib, seaborn  
- scikit-learn  
- nltk / vaderSentiment 

## Report
Full write-up: [Notion Report](https://www.notion.so/Trial-Task-Report-Coherence-Scoring-Prototype-23f252ec466e8026b7b6dbe1e8101a2a)

---
