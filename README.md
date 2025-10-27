# Data Mining Methodologies: CRISP-DM, KDD, SEMMA

This repository contains three end-to-end data science / data mining projects.  
Each project uses a different industry-standard methodology:

1. **CRISP-DM (Cross-Industry Standard Process for Data Mining)**  
   - Dataset: Retail / Walmart-style weekly store sales forecasting  
   - Task: Predict next week's sales to help inventory and staffing  
   - Model type: Regression  
   - Notebook: `CRISP_DM/notebooks/crispdm_pipeline.ipynb`

2. **KDD (Knowledge Discovery in Databases)**  
   - Dataset: Telco Customer Churn  
   - Task: Predict if a telecom customer will churn (leave)  
   - Model type: Binary classification  
   - Notebook: `KDD/notebooks/kdd_pipeline.ipynb`

3. **SEMMA (Sample, Explore, Modify, Model, Assess)**  
   - Dataset: Student Performance / At-Risk Student Prediction  
   - Task: Predict if a student is at academic risk  
   - Model type: Binary classification  
   - Notebook: `SEMMA/notebooks/semma_pipeline.ipynb`

## Deliverables per methodology

For each methodology, this repo includes:
- A runnable Google Colab notebook
- A `reports/` folder with one Markdown file per phase of the methodology
- `critique_sessions.md`, which shows AI critique loops:
  - We ask GPT-5 / Claude to act like a "world-renowned expert" in that methodology
  - It reviews each phase and points out gaps
  - We revise based on that feedback
- `medium_article_draft.md`: Medium-style article telling the story of that project
- `video_script.md`: spoken walkthrough script for the YouTube-style video demo

## Reproducibility / Environment

See `environment/`:
- `docker/requirements.txt` and `docker/Dockerfile` document the Python environment
- `open_interpreter_notes.md`: using open-interpreter and a local GPT-5-style workflow to iterate safely
- `metagpt_notes.md`: using agent-style planning (MetaGPT) to structure tasks and documentation

Note: Some datasets (e.g. Kaggle) may require you to agree to terms. If raw data cannot be committed, a `README` in `data/raw/` will include download instructions.

## Academic Integrity

All AI-generated code, analysis, and text was:
1. Executed and verified manually by the student in Colab
2. Iterated through multiple critique loops with an AI persona modeled as a senior industry expert in CRISP-DM / KDD / SEMMA
3. Documented in `critique_sessions.md` for transparency
