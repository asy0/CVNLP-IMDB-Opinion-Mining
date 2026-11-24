# Anleitung: Projekt ausführen

Diese Anleitung erklärt Schritt für Schritt, wie Sie das IMDB Opinion Mining Projekt ausführen.

---

## Voraussetzungen

- **Python 3.8 oder höher** (empfohlen: Python 3.10+)
- **Jupyter Notebook** oder **JupyterLab** oder **VS Code** mit Jupyter Extension
- **IMDB Dataset** (siehe Schritt 2)

---

## Schritt 1: Virtual Environment erstellen (Empfohlen)

### Windows (PowerShell):
```powershell
# Virtual Environment erstellen
python -m venv venv

# Aktivieren
.\venv\Scripts\Activate.ps1

# Falls Fehler: Execution Policy ändern
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Windows (CMD):
```cmd
python -m venv venv
venv\Scripts\activate
```

### Linux/Mac:
```bash
python3 -m venv venv
source venv/bin/activate
```

---

## Schritt 2: Dependencies installieren

```bash
pip install -r requirements.txt
```

**Wichtig:** Falls es Fehler gibt, installieren Sie die Pakete einzeln:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow keras joblib tqdm wordcloud
```

---

## Schritt 3: IMDB Dataset herunterladen

1. **Dataset herunterladen:**
   - Gehen Sie zu: http://ai.stanford.edu/~amaas/data/sentiment/
   - Laden Sie `aclImdb_v1.tar.gz` herunter

2. **Dataset entpacken:**
   ```bash
   # Windows (PowerShell)
   tar -xzf aclImdb_v1.tar.gz
   
   # Oder mit 7-Zip/WinRAR entpacken
   ```

3. **Dataset-Struktur prüfen:**
   ```
   data/
   └── aclImdb/
       ├── train/
       │   ├── pos/     (12.500 positive Reviews)
       │   └── neg/     (12.500 negative Reviews)
       └── test/
           ├── pos/     (12.500 positive Reviews)
           └── neg/     (12.500 negative Reviews)
   ```

4. **Dataset ins Projekt-Verzeichnis verschieben:**
   - Verschieben Sie den `aclImdb` Ordner nach `data/aclImdb/`
   - Die Struktur sollte sein: `cvnlp-imdb-opinion-mining/data/aclImdb/`

---

## Schritt 4: Jupyter Notebook starten

### Option A: Jupyter Notebook (Browser)
```bash
jupyter notebook
```
Öffnet sich automatisch im Browser. Navigieren Sie zu den `.ipynb` Dateien.

### Option B: JupyterLab (Modernere UI)
```bash
jupyter lab
```

### Option C: VS Code
- Öffnen Sie VS Code
- Installieren Sie die "Jupyter" Extension (falls nicht vorhanden)
- Öffnen Sie eine `.ipynb` Datei
- Klicken Sie auf "Run All" oder führen Sie Zelle für Zelle aus

---

## Schritt 5: Notebooks in der richtigen Reihenfolge ausführen

### ⚠️ WICHTIG: Reihenfolge beachten!

Die Notebooks müssen **in dieser Reihenfolge** ausgeführt werden:

### 1️⃣ `01_explore_dataset.ipynb`
- **Zweck:** Dataset-Exploration und Analyse
- **Dauer:** ~1-2 Minuten
- **Output:** 
  - Dataset-Statistiken
  - Visualisierungen: `outputs/dataset_balance.png`, `outputs/text_characteristics.png`

**Ausführung:**
- Öffnen Sie das Notebook
- Klicken Sie auf **"Run All"** (oder führen Sie Zelle für Zelle aus mit `Shift + Enter`)

---

### 2️⃣ `02_nb_tfidf_baseline.ipynb`
- **Zweck:** Training des Naive Bayes Modells
- **Dauer:** ~2-5 Minuten (je nach Hardware)
- **Output:**
  - Modell: `outputs/models/nb_tfidf_imdb.joblib`
  - Predictions: `outputs/preds_nb.csv`
  - Confusion Matrix: `outputs/confusion_matrix_nb.png`

**Ausführung:**
- Öffnen Sie das Notebook
- Klicken Sie auf **"Run All"**
- ⚠️ **Warten Sie, bis das Training abgeschlossen ist!**

---

### 3️⃣ `03_lstm_model.ipynb`
- **Zweck:** Training des LSTM Modells
- **Dauer:** ~10-30 Minuten (je nach Hardware, GPU empfohlen)
- **Output:**
  - Modell: `outputs/models/lstm_imdb_savedmodel/`
  - Predictions: `outputs/preds_lstm.csv`
  - Training History: `outputs/training_history_lstm.png`
  - Confusion Matrix: `outputs/confusion_matrix_lstm.png`

**Ausführung:**
- Öffnen Sie das Notebook
- Klicken Sie auf **"Run All"**
- ⚠️ **Das Training kann lange dauern!** Seien Sie geduldig.
- 💡 **Tipp:** Für schnelleres Testen können Sie `MAX_DOCS_PER_CLASS = 1000` setzen (in Zelle 3)

---

### 4️⃣ `04_model_comparison.ipynb`
- **Zweck:** Vergleich der beiden Modelle
- **Dauer:** ~1 Minute
- **Voraussetzung:** Beide Modelle müssen trainiert sein (Notebooks 2 und 3)
- **Output:**
  - Vergleichsplots: `outputs/model_comparison_metrics.png`
  - Confusion Matrices Vergleich: `outputs/confusion_matrices_comparison.png`

**Ausführung:**
- Öffnen Sie das Notebook
- Klicken Sie auf **"Run All"**
- ⚠️ **Funktioniert nur, wenn Notebooks 2 und 3 bereits ausgeführt wurden!**

---

## Schritt 6: Ergebnisse prüfen

Nach dem Ausführen aller Notebooks finden Sie:

### Visualisierungen (`outputs/`):
- `dataset_balance.png` - Dataset-Balance
- `text_characteristics.png` - Text-Charakteristika
- `confusion_matrix_nb.png` - Naive Bayes Confusion Matrix
- `confusion_matrix_lstm.png` - LSTM Confusion Matrix
- `training_history_lstm.png` - LSTM Training History
- `model_comparison_metrics.png` - Metriken-Vergleich
- `confusion_matrices_comparison.png` - Confusion Matrices Vergleich

### Predictions (`outputs/`):
- `preds_nb.csv` - Naive Bayes Predictions
- `preds_lstm.csv` - LSTM Predictions

### Modelle (`outputs/models/`):
- `nb_tfidf_imdb.joblib` - Gespeichertes Naive Bayes Modell
- `lstm_imdb_savedmodel/` - Gespeichertes LSTM Modell

---

## Häufige Probleme und Lösungen

### Problem 1: "ModuleNotFoundError"
**Lösung:**
```bash
pip install [fehlendes-modul]
# Oder
pip install -r requirements.txt
```

### Problem 2: "FileNotFoundError: data/aclImdb"
**Lösung:**
- Stellen Sie sicher, dass das Dataset in `data/aclImdb/` liegt
- Prüfen Sie die Verzeichnisstruktur (siehe Schritt 3)

### Problem 3: LSTM Training zu langsam
**Lösung:**
- Reduzieren Sie die Datenmenge: In `03_lstm_model.ipynb`, Zelle 3, setzen Sie:
  ```python
  MAX_DOCS_PER_CLASS = 1000  # Statt None
  ```
- Verwenden Sie eine GPU (falls verfügbar)

### Problem 4: "Out of Memory" Fehler
**Lösung:**
- Reduzieren Sie `MAX_DOCS_PER_CLASS` in den Notebooks
- Schließen Sie andere Programme
- Verwenden Sie einen Computer mit mehr RAM

### Problem 5: Jupyter startet nicht
**Lösung:**
```bash
pip install jupyter
jupyter notebook
```

### Problem 6: Encoding-Fehler beim Laden der Daten
**Lösung:**
- Das sollte bereits im Code behoben sein (`errors="ignore"`)
- Falls weiterhin Probleme: Stellen Sie sicher, dass Sie UTF-8 Encoding verwenden

---

## Alternative: Python Scripts ausführen

Falls Sie die Python Scripts direkt ausführen möchten (ohne Jupyter):

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

**Hinweis:** Die Scripts erzeugen keine interaktiven Visualisierungen, aber speichern die Plots als PNG-Dateien.

---

## Projektbericht ausfüllen

Nach dem Ausführen aller Notebooks:

1. Öffnen Sie `PROJECT_REPORT.md`
2. Füllen Sie die Platzhalter mit Ihren Ergebnissen:
   - Metriken aus den Notebooks kopieren
   - Visualisierungen referenzieren
   - Probleme und Lösungen dokumentieren
   - Interpretationen hinzufügen

---

## Tipps für bessere Performance

1. **GPU für LSTM:** Falls Sie eine NVIDIA GPU haben, installieren Sie `tensorflow-gpu`
2. **Batch Size anpassen:** Bei Speicherproblemen reduzieren Sie `BATCH_SIZE` im LSTM Notebook
3. **Subset für Tests:** Verwenden Sie `MAX_DOCS_PER_CLASS = 1000` für schnelle Tests
4. **Parallel Processing:** Scikit-learn nutzt automatisch mehrere CPU-Kerne

---


**Viel Erfolg! 🚀**






