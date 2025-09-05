# Coherence Scoring Prototype

A lightweight prototype that combines **HRV biometric signals** and **text sentiment analysis** into a unified **coherence score (0–100)** with interactive visualizations and time series analysis.

## Overview

**Core Function:** Integrates HRV deviation from baseline with VADER sentiment analysis enhanced by domain-specific keywords to produce interpretable coherence scores.

**Key Features:**
- **HRV Component**: Uses quadratic penalty function with configurable tolerance (τ=0.5)
- **Text Component**: VADER sentiment + confidence/uncertainty keyword adjustments  
- **Weighted Fusion**: Default 80% HRV, 20% text (configurable)
- **Interactive Visualizations**: Time series charts and multi-view dashboards
- **JSON API Ready**: Structured output with all components and explanations

## Quick Start

```python
score_result = calculate_coherence_score(65, 75, "I feel nervous but ready.")
# Returns: {"coherence_score": 74.2, "explanation": "HRV is 13% below baseline; text contains uncertain language → moderate coherence."}
```

## Repository Structure
- `synthetic.ipynb` — Complete implementation with interactive visualizations
- `coherence_score.ipynb` — Original core function development  
- `data_analysis.ipynb` — Exploratory analysis and parameter tuning
- `synthetic_coherence_data.json` — Test dataset (50 samples)

## Visualizations

**Interactive Time Series**: Shows coherence score and component drift over time  
**Multi-View Dashboard**: Statistical analysis including distributions, correlations, and coherence level breakdown

## Dependencies
- Python 3.9+, pandas, numpy, plotly  
- matplotlib, seaborn, vaderSentiment
- textblob (optional for extended analysis)

## Results Summary
- **72% High Coherence** (≥80) across test samples
- **Strong HRV-Coherence Correlation** (0.917) validates weighting approach  
- **Robust Parameter Sensitivity** with configurable tolerance and penalties

## Report
Full write-up: [Notion Report](https://www.notion.so/Trial-Task-Report-Coherence-Scoring-Prototype-23f252ec466e8026b7b6dbe1e8101a2a)

---
