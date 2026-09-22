# YadYar Lite — RAG and Hallucination Study

Course project for **T-05: Retrieval-Augmented Generation and the Study of Hallucination**.


- Run the notebook in order.

## Dataset


- Hugging Face dataset page: <https://huggingface.co/datasets/rajpurkar/squad_v2>
- Official SQuAD website: <https://rajpurkar.github.io/SQuAD-explorer/>
- Direct download — validation data used by this project: <https://rajpurkar.github.io/SQuAD-explorer/dataset/dev-v2.0.json>
- Direct download — training data: <https://rajpurkar.github.io/SQuAD-explorer/dataset/train-v2.0.json>
- Dataset name used in the notebook: `rajpurkar/squad_v2`
- Dataset split used in the notebook: `validation`

The notebook downloads the dataset automatically with:

```python
from datasets import load_dataset
dataset = load_dataset("rajpurkar/squad_v2")
```

The full dataset does not need to be downloaded manually. The direct links are provided for reference and reproducibility.

## Data used in the experiment

The notebook creates a small balanced sample from the SQuAD 2.0 validation split:

- 500 answerable questions;
- 500 unanswerable questions;
- 1,000 questions in total;
- 200 development questions;
- 800 test questions;
- random seed: `42`.

Repeated passages are removed when the retrieval corpus is created. Each unique passage receives a `context_id`.

## Baseline models

| Component | Model |
|---|---|
| Retriever | `sentence-transformers/multi-qa-MiniLM-L6-cos-v1` |
| Generator | `google/flan-t5-small` |
| Retrieval depth | Top 3 passages |

Both models are pretrained. The project does not train a model from scratch and does not fine-tune either model.

## Requirements


```
datasets
pandas
numpy
scikit-learn
sentence-transformers
transformers
accelerate
sentencepiece
torch
matplotlib
tqdm
```

## Google Drive folder

```
My Drive/RAG-Project
```

## Expected folders after execution

```text
RAG-Project/
├── RAG_Project.ipynb
├── README.md
├── report.pdf
├── report.docx
├── data/
│   ├── corpus.csv
│   ├── development.jsonl
│   └── test.jsonl
└── results/
    ├── development_retrieval.jsonl
    ├── test_retrieval.jsonl
    ├── development_generation.jsonl
    ├── test_generation.jsonl
    ├── metric CSV files
    ├── error-analysis CSV files
    └── result charts
```

## Reproducibility settings

- Random seed: `42`
- Balanced sample: 500 answerable + 500 unanswerable
- Development/test sizes: 200/800
- Retrieval depth: `top_k = 3`
- Generation sampling: disabled
- Batch checkpoints: enabled
