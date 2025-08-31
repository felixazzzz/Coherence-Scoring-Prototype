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

## Methods

### Coherence Score Formula
We use a **linear combination** of HRV-based score ($S_{HRV}$) and text-based score ($S_{Text}$):

$$
S_{coherence} = w \cdot S_{HRV} + (1-w) \cdot S_{Text}
$$

where $w=0.8$ reflects stronger trust in physiological signals.

---

### HRV Score
- HRV is normalized relative to baseline.  
- To model tolerance for small deviations, a **power function** is applied: small differences give minor penalties, large differences accelerate toward zero.  
- Parameters $(\tau, p, q)$ control tolerance and penalty intensity. For example, $\tau=0.5$ (50% drift threshold), $p=q=2$.  

---

### Text Score
- Implemented via **VADER sentiment analysis** (compound score ∈ [-1,1] mapped to [0,100]).  
- Augmented with a **keyword dictionary** (confidence vs. uncertainty words). Each match adjusts score by ±2 points.  
- Lightweight and interpretable. In future, can be extended to BERT/LLM methods.

---

## Results

### Data Analysis
- Small dataset, HRV differences generally <20%.  
- Text snippets are short, supporting the lightweight approach.  
- Visualizations show HRV distribution, parameter sensitivity, and coherence score distributions.  

### Coherence Scoring
- Weighted fusion: $w=0.8$ for HRV, $0.2$ for text.  
- Demonstrated on example case: HRV 65 vs. baseline 75 + “nervous” → moderate coherence.  
- Applied to dataset with visualizations and explanations.  

---

## Discussion

- Current prototype is subjective due to limited dataset and lack of medical theory grounding.  
- Provides a **transparent baseline model**.  
- Future extensions:  
  - **BERT** sentence embeddings ([CLS] vector) for richer text features.  
  - **LLM few-shot prompting** for scoring with natural-language explanations.  

---

## Repository Structure
- `coherence_score.ipynb` — Core implementation of HRV + text scoring functions.  
- `data_analysis.ipynb` — Exploratory analysis, visualizations, sensitivity checks.  

---

## Usage

Clone the repo and run the notebooks:

```bash
git clone https://github.com/your-username/Coherence-Scoring-Prototype.git
cd Coherence-Scoring-Prototype
jupyter notebook
```

---

## Dependencies
- Python 3.9+  
- pandas, numpy  
- matplotlib, seaborn  
- scikit-learn  
- nltk / vaderSentiment  
- transformers (optional, for BERT extension)  

Install:
```bash
pip install -r requirements.txt
```

---

## Report
Full write-up: [Notion Report](https://www.notion.so/Trial-Task-Report-Coherence-Scoring-Prototype-23f252ec466e8026b7b6dbe1e8101a2a)

---

## License
MIT License. See `LICENSE` for details.
