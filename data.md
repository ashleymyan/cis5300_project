# Data Overview

This project uses a combination of English and multilingual sentiment datasets to train and evaluate a cross-lingual sentiment classifier.  
The overall data is divided into **three main stages**, corresponding to different phases of training and evaluation:

| Stage | Dataset(s) | Purpose | Languages | Split |
|--------|-------------|----------|------------|--------|
| **Stage A** | IMDb + MARC (English only) | Binary sentiment classification (`positive` / `negative`) | English | train / dev / test |
| **Stage B** | MARC (English only) | 3-way sentiment classification (`positive` / `neutral` / `negative`) | English | train / dev / test |
| **Multilingual Evaluation** | LinCE-SA | Evaluation on code-switched text (`positive` / `neutral` / `negative`) | Spanish-English, Hindi-English | dev only |

All data is serialized in **JSON Lines (`.jsonl`)** format for ease of streaming during model training.  
Each record consists of the following fields:

```json
{
  "text": "This movie was fantastic!",
  "label": "positive",
  "source": "imdb",
  "lang_pair": "es-en"
}
```

### Data Sources and Collection

All datasets were downloaded directly from their Kaggle repositories and extracted locally for preprocessing.

- **IMDb Movie Reviews** – [Kaggle link](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)  
  → Loaded as a single CSV file for English-only sentiment classification.

- **MARC (Multilingual Amazon Reviews Corpus)** – [Kaggle link](https://www.kaggle.com/datasets/mexwell/amazon-reviews-multi)  
  → The English subset was filtered from the multilingual corpus after downloading all three split CSVs (`train`, `validation`, `test`).

- **LinCE-SA (Linguistic Code-switching Evaluation)** – [Kaggle link](https://www.kaggle.com/datasets/thedevastator/unlock-universal-language-with-the-lince-dataset)  
  → The sentiment analysis subset (`sa_spaeng_*.csv`) was extracted and combined into a unified validation set for multilingual evaluation.
