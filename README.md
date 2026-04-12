Large language models frequently generate hallucinated content—fluent but factually incorrect outputs—which is especially problematic in medical contexts. Detecting such hallucinations is essential for safe deployment.

This project formulates hallucination detection as a supervised classification task: given a question, context, and answer, predict whether the answer is hallucinated. The model is trained on MedHallu [https://huggingface.co/datasets/UTAustin-AIHealth/MedHallu], a dataset with fine-grained hallucination annotations, and evaluated on Med-HALT[https://huggingface.co/datasets/openlifescienceai/Med-HALT], which introduces diverse reasoning-based tasks.

A key objective of this work is to determine whether domain-specific pretraining improves hallucination detection, particularly under distribution shift. To address this, BERT and BioBERT are compared under identical training conditions.

Refer to the project report for more details https://github.com/ashamatthews/hallucination_project/blob/main/hallucination_classification_biobert.ipynb
