Refer to the [project report](https://github.com/UC-Berkeley-I-School/hallucination_detection_in_medical_QA_bert_vs_biobert/blob/main/hallucination_detection_in_medical_QA_bert_vs_biobert.pdf) for more details.

# Detecting Hallucinations in Medical Question Answering: A Comparative Study of BERT and BioBERT


This project investigates hallucination detection in medical question answering systems using transformer-based models. I compare a general-purpose language model (**BERT**) with a biomedical domain-specific model (**BioBERT**) to evaluate their effectiveness in detecting hallucinated medical responses.

---

## Project Overview

Large Language Models (LLMs) can generate fluent but factually incorrect outputs (hallucinations), especially in high-stakes domains like healthcare. Detecting such hallucinations is essential for safe deployment.

This project formulates hallucination detection as a **binary classification problem**:

> Given a medical question, context, and answer: predict whether the answer is **grounded (0)** or **hallucinated (1)**.

Evaluate both in-domain and out-of-domain generalization.

---

## Datasets

### MedHallu (Training + In-domain Evaluation)
Source: https://arxiv.org/abs/2502.14302

Dataset: https://huggingface.co/datasets/UTAustin-AIHealth/MedHallu

MedHallu is a medical hallucination detection benchmark with fine-grained annotations.

I use it to construct a binary classification dataset:

- (Question + Context, Ground Truth Answer) → Label 0 (non-hallucinated)
- (Question + Context, Hallucinated Answer) → Label 1 (hallucinated)

**Categories include:**
- Misinterpretation of Question
- Incomplete Information
- Mechanism and Pathway Misattribution
- Methodological and Evidence Fabrication

---

### Med-HALT (Out-of-domain Evaluation)
Source: https://arxiv.org/abs/2307.15343

Dataset: https://huggingface.co/datasets/openlifescienceai/Med-HALT

Med-HALT is used to evaluate robustness under distribution shift and reasoning stress tests.

It includes three sub-tasks:

- **FCT (False Confidence Test)**  
- **NOTA (None of the Above Test)**  
- **FQT (Fake Questions Test)**  

---

## Models

I compare two transformer-based sequence classification models:

- **BERT-base-uncased**
- **BioBERT-base-cased (biomedical pretraining)**

Both models are fine-tuned using HuggingFace Transformers for binary classification.

---

## Methodology

### Input Representation

Each training example is constructed as: Question + Answer → Candidate Answer

---

### Task Formulation

Binary classification:

- **0 → Grounded / correct answer**
- **1 → Hallucinated / incorrect answer**

---

### Training Setup

- Framework: HuggingFace Transformers
- Loss Function: Cross-Entropy Loss
- Optimizer: AdamW
- Epochs: 5
- Batch Size: 8
- Max Sequence Length: 256

---

## Results

### In-Domain Performance (MedHallu)

| Model    | Accuracy | F1 Score |
|----------|----------|----------|
| BERT     | ~0.94–0.95 | ~0.94 |
| BioBERT  | ~0.95–0.96 | ~0.96 |

BioBERT consistently outperforms BERT in the medical domain.

---

### Out-of-Domain Performance (Med-HALT)

| Model    | Accuracy | F1 Score |
|----------|----------|----------|
| BERT     | ~0.43 | ~0.33 |
| BioBERT  | ~0.56 | ~0.59 |

BioBERT shows significantly better generalization under distribution shift.

---

### Med-HALT Task Breakdown

| Task  | BERT F1 | BioBERT F1 |
|------|--------|------------|
| FCT  | ~0.30  | ~0.49 |
| NOTA | ~0.35  | ~0.65 |
| FQT  | 0.00   | 0.00 |

---

## Key Findings

- Domain-specific pretraining (BioBERT) improves hallucination detection performance.
- Strong in-domain results do not guarantee out-of-domain robustness.
- Both models struggle significantly with Fake Question (FQT) tasks.
- Hallucination detection remains challenging under reasoning shifts and adversarial inputs.

---

## Repository Structure

```bash
.
├── hallucination_classification_bert.ipynb
├── hallucination_classification_biobert.ipynb
├── hallucination_detection_in_medical_QA_biobert_vs_bert.pdf
└── README.md
```

