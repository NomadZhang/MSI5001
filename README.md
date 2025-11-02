MSI5001 Airline Sentiment Clustering
====================================

This project explores unsupervised clustering techniques on the Kaggle *Twitter US Airline Sentiment* dataset. The notebook `main.ipynb` walks through text cleaning, feature engineering (bag-of-words, spaCy embeddings, emoji & handle features, VADER sentiment scores) and evaluates both K-Means and DBSCAN clustering runs against the labelled sentiment ground truth.

Project Layout
--------------
- `main.ipynb` — primary analysis notebook; run cells top-to-bottom to reproduce plots and tables.
- `Airline Sentiment/` — contains the source dataset (`Tweets.csv`) expected by the notebook.
- `requirements.txt` — pinned dependencies (UTF-16 encoded).

Prerequisites
-------------
- Python 3.12
- `pip` for dependency installation.
- Ability to install large language resources (~800 MB for `en_core_web_lg`) and download NLTK corpora.

Environment Setup
-----------------
1. **Create and activate a virtual environment(if just use the local environment)**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate           # macOS/Linux
   # .venv\Scripts\activate            # Windows PowerShell
   ```
2. **Install dependencies**  
   `requirements.txt` is saved in UTF-16; modern `pip` handles this transparently.
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```
3. **Download the required spaCy model**
   ```bash
   python -m spacy download en_core_web_lg
   ```
4. **Pre-download NLTK resources (avoids interactive prompts mid-notebook)**
   ```bash
   python -m nltk.downloader stopwords punkt punkt_tab wordnet vader_lexicon
   ```

Running the Notebook
--------------------
1. From the project root, launch Jupyter:
   ```bash
   jupyter lab
   # or
   jupyter notebook
   ```
2. Open `main.ipynb`. Verify the dataset lives at `Airline Sentiment/Tweets.csv`; keep the relative path unchanged.
3. Run all cells sequentially (`Kernel → Restart & Run All`). The workflow is organised as:
   - **Data Ingestion & Cleaning** – removes URLs, handles, emojis; converts emojis/emoticons to text.
   - **Feature Engineering** – bag-of-words (CountVectorizer + TruncatedSVD), spaCy embeddings + PCA, custom emoji/handle/sentiment vectors, VADER sentiment scores.
   - **Clustering** – multiple K-Means experiments and DBSCAN with tuned `eps/min_samples`.
   - **Evaluation & Visualisation** – PCA scatter plots, word clouds, metric heatmaps (homogeneity, completeness, V-measure, ARI).

What to Expect
--------------
- The notebook caches nothing; each run recomputes feature matrices, PCA reductions, and clustering models. Expect ~15–25 minutes on a modern laptop due to spaCy + PCA passes.
- DBSCAN sections iterate over several `eps` settings until they achieve ≥3 clusters; progress prints in the cell output.

Troubleshooting
---------------
- **Missing resources**: If a cell errors about spaCy models or NLTK corpora, re-run the download commands above in the active virtual environment.
- **Unicode errors**: Ensure your terminal uses UTF-8; dataset and notebook assume UTF-8. The UTF-16 `requirements.txt` should still work with `pip`; if needed, re-save as UTF-8 before installing.
- **Matplotlib figures not showing**: When running headless, set `%matplotlib inline` or switch to Jupyter Notebook/Lab in a browser.

Verification Steps
------------------
- Confirm the notebook completes without errors.
- Review the generated evaluation tables (`clustering_metrics`, `clustering_metrics_high_confidence`, and their DBSCAN counterparts) to verify metric values.
- Inspect word cloud outputs for each clustering variant to ensure clusters align with qualitative expectations.

Next Steps (Optional)
---------------------
- Export cleaned feature tables for downstream modelling.
- Tune alternative clustering algorithms (e.g., Agglomerative, Gaussian Mixture).
- Package preprocessing into reusable Python modules for automation outside the notebook.
