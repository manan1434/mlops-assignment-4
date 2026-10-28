# Image Classification Pipeline — Documentation

**Name:** Manan  
**PRN:** 23070126070  
**GitHub Repository:** https://github.com/manan1434/mlops-assignment-4

---

## What This Project Does
Classifies flower images (daisy, dandelion, roses) using a Random Forest model.  
The pipeline is fully automated using DVC — one command runs all 5 stages.  
Data and models are stored on **AWS S3** using DVC remote storage.

---

## Tech Stack
- Python 3.x
- scikit-learn
- DVC + AWS S3
- Pillow
- NumPy, Matplotlib

---

## Pipeline Stages

| Stage | Script | What it does |
|-------|--------|--------------|
| data_collection | src/data_collection.py | Downloads flower images |
| data_processing | src/data_processing.py | Resizes to 64x64, splits train/val |
| feature_selection | src/feature_selection.py | Flattens and normalizes arrays |
| model_training | src/model_training.py | Trains Random Forest |
| model_evaluation | src/model_evaluation.py | Accuracy score + confusion matrix |

---

## Parameters (params.yaml)

| Parameter | Value | Why it matters |
|-----------|-------|----------------|
| image_size | 64 | All images become 64x64 |
| validation_split | 0.2 | 20% data for testing |
| n_estimators | 100 | Number of trees in forest |
| max_depth | 10 | How deep each tree grows |
| normalize | true | Pixels scaled 0-1 |
| flatten | true | Image to 1D for sklearn |
| max_images_per_class | 100 | Limits dataset size |
| random_state | 42 | Reproducible results |

---

## How to Run

```bash
pip install -r requirements.txt
git init && dvc init
dvc pull          # pulls data from AWS S3
dvc repro         # runs full pipeline
dvc metrics show  # shows accuracy