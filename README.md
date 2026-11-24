# CV/NLP – IMDB Opinion Mining

Dieses Projekt gehört zur Lehrveranstaltung *Computer Vision & Natural Language Processing* (CVNLP).  
Ziel ist es, Sentiment-Analyse auf dem **IMDB Large Movie Review Dataset (aclImdb)** zu machen und verschiedene Modelle zu vergleichen:

- Naive Bayes mit TF-IDF Features (Klassischer Algorithmus)
- Bidirectional LSTM (Deep Learning Algorithmus)

---

## Projektstruktur

```text
cvnlp-imdb-opinion-mining/
├─ notebooks/
│  ├─ 01_explore_dataset.ipynb      # Explorative Analyse des Datasets
│  ├─ 02_nb_tfidf_baseline.ipynb   # Naive Bayes + TF-IDF Baseline
│  ├─ 03_lstm_model.ipynb          # LSTM-Modell mit Keras
│  └─ 04_model_comparison.ipynb    # Modell-Vergleich und Interpretation
│
├─ src/
│  ├─ 01_explore_dataset.py         # Explorative Analyse (Python Script)
│  ├─ 02_nb_tfidf_baseline.py      # Naive Bayes + TF-IDF (Python Script)
│  ├─ 03_lstm_model.py              # LSTM-Modell (Python Script)
│  ├─ 04_mkae_results_table.py     # Ergebnisse-Tabelle generieren
│  ├─ utils_imdb.py                # Hilfsfunktionen (Daten laden, Preprocessing, etc.)
│  └─ __init__.py
│
├─ outputs/
│  ├─ preds_nb.csv                  # Vorhersagen des NB-Modells
│  ├─ preds_lstm.csv                # Vorhersagen des LSTM-Modells
│  ├─ models/                       # Gespeicherte Modelle
│  └─ *.png                         # Visualisierungen (Confusion Matrices, etc.)
│
├─ data/
│  └─ aclImdb/                      # IMDB-Dataset (liegt NICHT im Repo)
│
├─ requirements.txt                 # Python Dependencies
├─ PROJECT_REPORT.md                # Projektbericht-Vorlage
├─ Project -NLP.pdf                 # Projektbeschreibung / Angabe
└─ README.md                        # Diese Datei
```

---

## Installation

1. **Repository klonen oder herunterladen**

2. **Virtual Environment erstellen (empfohlen):**
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# oder
venv\Scripts\activate     # Windows
```

3. **Dependencies installieren:**
```bash
pip install -r requirements.txt
```

4. **IMDB Dataset herunterladen:**
   - Dataset von [IMDB Dataset](http://ai.stanford.edu/~amaas/data/sentiment/) herunterladen
   - In `data/aclImdb/` entpacken
   - Struktur sollte sein: `data/aclImdb/train/pos/`, `data/aclImdb/train/neg/`, etc.

---

## Verwendung

### 📖 Detaillierte Anleitung

**Siehe `ANLEITUNG.md` für eine Schritt-für-Schritt Anleitung!**

### Quick Start

1. **Dependencies installieren:**
   ```bash
   pip install -r requirements.txt
   ```

2. **IMDB Dataset herunterladen:**
   - Download von: http://ai.stanford.edu/~amaas/data/sentiment/
   - In `data/aclImdb/` entpacken

3. **Jupyter starten:**
   ```bash
   jupyter notebook
   ```

4. **Notebooks in Reihenfolge ausführen:**
   - `01_explore_dataset.ipynb` → Dataset-Exploration
   - `02_nb_tfidf_baseline.ipynb` → Naive Bayes Training
   - `03_lstm_model.ipynb` → LSTM Training (dauert länger!)
   - `04_model_comparison.ipynb` → Modell-Vergleich

### Python Scripts (Alternative)

Falls Sie die Python Scripts direkt ausführen möchten:

```bash
# Dataset Exploration
python src/01_explore_dataset.py

# Naive Bayes Training
python src/02_nb_tfidf_baseline.py

# LSTM Training
python src/03_lstm_model.py

# Ergebnisse vergleichen
python src/04_mkae_results_table.py
```

---

## Ergebnisse

Nach dem Ausführen der Notebooks/Scripts finden Sie:

- **Predictions**: `outputs/preds_nb.csv` und `outputs/preds_lstm.csv`
- **Modelle**: `outputs/models/`
- **Visualisierungen**: 
  - `outputs/dataset_balance.png`
  - `outputs/text_characteristics.png`
  - `outputs/confusion_matrix_nb.png`
  - `outputs/confusion_matrix_lstm.png`
  - `outputs/training_history_lstm.png`
  - `outputs/model_comparison_metrics.png`
  - `outputs/confusion_matrices_comparison.png`

---

## Projektbericht

Eine Vorlage für den Projektbericht finden Sie in `PROJECT_REPORT.md`.  
Bitte füllen Sie die Platzhalter mit Ihren Ergebnissen und Erkenntnissen aus.

---

## Anforderungen erfüllt

✅ Dataset Download und Preprocessing  
✅ Zwei Klassifikationsalgorithmen (Naive Bayes + LSTM)  
✅ Training beider Modelle  
✅ Performance-Vergleich und Interpretation  
✅ Jupyter Notebooks (Hauptanforderung)  
✅ Visualisierungen  
✅ Projektbericht-Vorlage
