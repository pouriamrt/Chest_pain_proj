# 🧠📊 Multimodal Diagnostic Prediction with Tabular and Text Data

This repository contains a comprehensive pipeline for building, training, and evaluating machine learning models that combine **tabular clinical data** and **free-text transcripts** for binary diagnostic classification. The project emphasizes **explainability**, **data augmentation**, and **modular design**, making it suitable for healthcare-related machine learning tasks.

---

## 🚀 Features

- 🔄 **Multimodal pipeline** combining tabular and textual data  
- 🧽 Custom **TextCleaner** for preprocessing unstructured text  
- 🧠 Choice of vectorizers: **TF-IDF** or **Doc2Vec**  
- 🧪 **Flexible pipeline** supporting different model types:
  - `RandomForestClassifier`
  - `BalancedRandomForestClassifier`
  - `EasyEnsembleClassifier`
  - `LogisticRegression`
  - `MultinomialNB`
- ⚖️ **SMOTE** for class imbalance handling (automatically bypassed for ensemble models)
- 🧠 **SHAP-based explainability** for both tree-based and linear models
- 📈 **Performance visualization**: confusion matrix, ROC curve
- 🔍 Scenario comparison:
  - Tabular only
  - Text only
  - Combined

---

## 📁 Project Structure

```bash
.
├── data/
│   ├── 00. Recordings/                     # Transcripts directory
│   ├── 01. OCI Chest pain study - CRF...   # Tabular data
│   └── 02. OCI Chest Pain - Patient...     # Patient input data
├── main.py                                 # Main training and evaluation script
├── README.md
└── requirements.txt
```

---

## 📊 Dataset Overview

The pipeline merges multiple sources:
- **Patient transcripts** (text files) are matched by Patient ID.
- **Self-reported data** like gender, age, and symptom questions.
- **Clinician-recorded final diagnoses** are used as binary targets:
  - Classes `[1,2,3]` → Non-critical
  - Classes `[4,5,6,7]` → Critical (target = 1)

---

## 🔧 How It Works

1. **Data Loading & Merging**:
   - Load tabular and patient input data from Excel sheets.
   - Merge them using patient identifiers.
   - Match transcripts from the file directory.

2. **Data Preprocessing**:
   - Categorical encoding, text cleaning, numerical scaling
   - Optional oversampling for class balancing

3. **Pipeline Building**:
   - Modular design via `sklearn.pipeline` and `FeatureUnion`
   - Easy to plug in different classifiers

4. **Model Evaluation**:
   - Classification report and confusion matrix
   - ROC curve + optimal threshold computation

5. **Model Explainability**:
   - SHAP summary plots for both tree-based and linear models
   - Support for interpreting text and tabular contributions

---

## 🧪 Experiments

You can compare performance across three scenarios:

- ✅ **Tabular + Text**
- 📄 **Text-only**
- 📊 **Tabular-only**

Each scenario can be configured with your model of choice using the `build_pipeline()` function.

---

## 🖼️ Visualizations

- Confusion Matrix
- ROC Curve with AUC
- SHAP Summary Plot for Feature Importance

**Optional**: UMAP + Doc2Vec visualization for transcript embeddings (commented in the script).

---

## 🛠️ Installation

```bash
pip install -r requirements.txt
```

Required packages include:
- `scikit-learn`
- `pandas`, `numpy`
- `imblearn`
- `shap`
- `matplotlib`, `seaborn`
- `nltk`, `gensim`, `umap-learn`

---

## 📌 Notes

- Make sure NLTK stopwords are downloaded before running:
  ```python
  import nltk
  nltk.download('stopwords')
  ```
- To avoid unnecessary errors, ensure all data files exist and are correctly named.

---

## 📍 Example Usage

```python
from your_module import build_pipeline, prepare_data_scenario

X, y = prepare_data_scenario(df, target_col='target')
pipeline = build_pipeline(use_text=True, use_tabular=True, model=LogisticRegression())
pipeline.fit(X_train, y_train)
```

---

## 📈 Output Metrics

```bash
Precision, Recall, F1-score
Confusion Matrix
ROC-AUC Score
SHAP Summary Plot
```

---

## 👨‍🔬 Author

**Pouria Mortezaagha**  
_Data Analyst | AI Researcher | Full Stack Developer_

Feel free to connect on [LinkedIn](https://www.linkedin.com/in/pouriamortezaagha/) or reach out if you're working on similar multimodal machine learning or healthcare AI projects!

---

## 📄 License

This project is licensed under the MIT License.
