# FavMovie — Movie Recommendation System

[![CI](https://img.shields.io/badge/CI-%20setup-lightgrey)](https://github.com/AnchalSR/FavMovie)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)

A lightweight, extensible movie recommendation project that demonstrates common recommendation techniques (collaborative filtering, content-based filtering, matrix factorization) and provides tools to preprocess data, train models, evaluate results, and run a small demo.

Key goals:
- Reproducible pipelines for training and evaluation
- Clear, modular code to add new models or datasets
- Simple demo to explore recommendations locally

Table of contents
- Project overview
- Quick start
- Data
- Scripts & usage
- Models
- Evaluation
- Project structure
- Development
- Contributing
- License & Contact

Project overview
This repository contains scripts and simple model implementations to build and evaluate movie recommenders. It is designed for experimentation with MovieLens-style datasets and to serve as a starting point for research or small demos.

What you get
- Data preprocessing utilities to convert raw CSVs into train/test splits and feature matrices
- Example model implementations (popularity baseline, item/user k-NN, matrix factorization)
- Training and evaluation scripts with standard recommendation metrics
- A minimal demo entrypoint (Flask/Streamlit) for quick local testing

Quick start
Prerequisites
- Python 3.8 or newer
- Git

1. Clone the repository
```bash
git clone https://github.com/AnchalSR/FavMovie.git
cd FavMovie
```

2. Create and activate a virtual environment
```bash
python -m venv .venv
source .venv/bin/activate   # macOS / Linux
.venv\Scripts\activate      # Windows
```

3. Install dependencies
If a requirements.txt exists:
```bash
pip install -r requirements.txt
```
Otherwise install the common packages:
```bash
pip install numpy pandas scikit-learn flask streamlit
```

Data
This project expects MovieLens-style CSV files. Recommended dataset: MovieLens (https://grouplens.org/datasets/movielens/). Place the files under the data/ directory:
- data/movies.csv
- data/ratings.csv
- data/tags.csv (optional)

Preprocessing
A preprocessing script converts raw CSVs into processed artifacts used for training and evaluation.
Example:
```bash
python scripts/preprocess.py --ratings data/ratings.csv --movies data/movies.csv --out data/processed/
```
If your file names or paths differ, pass the correct paths to the script.

Scripts & usage
- scripts/preprocess.py
  - Reads raw CSVs and produces processed datasets and train/test splits.
- scripts/train.py
  - Train a model and save artifacts to models/.
  Example:
  ```bash
  python scripts/train.py --data data/processed/ --model matrix_factorization --epochs 20 --out models/mf.pkl
  ```
- scripts/evaluate.py
  - Evaluate a saved model on held-out data.
  ```bash
  python scripts/evaluate.py --model models/mf.pkl --data data/processed/
  ```
- scripts/recommend.py
  - Produce top-K recommendations for a user from a saved model.
  ```bash
  python scripts/recommend.py --model models/mf.pkl --user-id 42 --k 10
  ```
- app.py
  - Minimal Flask or Streamlit demo to serve recommendations locally.
  Run with:
  ```bash
  export FLASK_APP=app.py
  flask run
  # or
  streamlit run app.py
  ```

Models (examples included)
- Baselines: popularity, random
- Collaborative filtering: user-based k-NN, item-based k-NN
- Matrix factorization: SVD / ALS style training
- Content-based: TF-IDF on genres/tags + cosine similarity
- Hybrid: simple score combination of CF + content

Evaluation
Supported offline metrics:
- Precision@k, Recall@k
- Mean Average Precision (MAP)
- Normalized Discounted Cumulative Gain (NDCG)
- RMSE/MAE (when predicting explicit ratings)

Use time-based or user-based holdout splits for realistic evaluation.

Project structure (recommended)
- README.md
- requirements.txt
- data/
  - raw/
  - processed/
- scripts/
  - preprocess.py
  - train.py
  - evaluate.py
  - recommend.py
- models/
- app.py
- notebooks/
- tests/

Development
- Run tests: pytest (if tests/ exist)
- Linting: flake8 / black

Contributing
Contributions are welcome — please follow these steps:
1. Fork the repository
2. Create a branch: git checkout -b feat/your-feature
3. Add tests and documentation for new functionality
4. Open a pull request describing your changes

License
This project is provided under the MIT License. See LICENSE for details.

Maintainer & Contact
- GitHub: https://github.com/AnchalSR
- Email: (add email if desired)

Acknowledgements
- MovieLens / GroupLens for dataset and inspiration

Notes & next steps
- Replace and/or adapt the script names and CLI flags above to match the implementation in this repository.
- If you want, I can inspect the repository and auto-fill exact commands, generate a requirements.txt from imports, or scaffold a demo app. If you want me to proceed, tell me which task to run next.
