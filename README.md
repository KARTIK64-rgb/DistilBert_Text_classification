# DistilBERT Text Classification

This project fine-tunes the [DistilBERT](https://huggingface.co/distilbert-base-uncased) model from Hugging Face Transformers for multi-class text classification. The goal is to classify text (combined from title and description) into one of four categories: World, Sports, Business, and Sci/Tech.

---

## 📚 Dataset

The dataset consists of: 
- `train.csv`
- `test.csv`
- "kaggle"

Each file contains:
- `Title`
- `Description`
- `Class Index` (values 1 to 4)

Preprocessing steps:
- Combine `Title` and `Description` into a single `text` field.
- Adjust `Class Index` to 0-based indexing (i.e., values 0 to 3).
- Keep only `text` and `label` columns for training.

---

## 🧠 Model Overview

- **Base Model**: DistilBERT (`distilbert-base-uncased`)
- **Classification Task**: 4-class classification
- **Transfer Learning**: The base DistilBERT layers are frozen
- **Head**: A classification layer trained on top of frozen embeddings

---

## 🚀 Training Configuration

Training is done using Hugging Face’s `Trainer` API with the following settings:

- Epochs: 3
- Train batch size: 16
- Eval batch size: 16
- Weight decay: 0.01
- Evaluation strategy: Per epoch
- Logging steps: 50

The model is trained on the training set and evaluated on the test set using the accuracy metric.

---

## 🔍 Evaluation

The model is evaluated using classification accuracy. The `evaluate` library is used to compute metrics after each epoch.

---

## 🧾 Inference Example

A simple inference function is provided:

```python
text = "Virat kohli won the ipl trophy"
print("Predicted class index:", predict(text))
