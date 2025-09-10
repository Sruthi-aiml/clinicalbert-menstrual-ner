# ClinicalBERT Menstrual NER
This project fine-tunes [Bio_ClinicalBERT](https://huggingface.co/emilyalsentzer/Bio_ClinicalBERT) for Named Entity Recognition (NER) in a synthetic menstrual and IVF dataset. The goal is to extract medically relevant entities from clinical-style conversations. The model has been trained to recognize five main entity types: Symptoms, Hormones, Procedures, Medications, and Ultrasound findings.

## Project Overview
The workflow followed five main steps:  
1. Dataset Preparation: Synthetic menstrual/IVF conversations were converted into BIO format for training. Example:  
Patient irregular B-Symptoms  
periods I-Symptoms  
...  

2. Label Definition: Each entity type was mapped to a numerical ID for training. Example labels include B-Symptoms, I-Symptoms, B-Hormones, I-Hormones, B-Procedures, I-Procedures, B-Medications, I-Medications, B-Ultrasound, and I-Ultrasound.  

3. Tokenization: Text was tokenized using the ClinicalBERT tokenizer, with BIO tags aligned to subword tokens.  

4. Model Training: ClinicalBERT was fine-tuned using BertForTokenClassification for multiple epochs. Training progress was tracked with precision, recall, and F1 metrics.  

5. Prediction and Evaluation: The fine-tuned model can now recognize entities in unseen text. Example:  
Input: "Patient reports irregular periods and low estrogen."  
Output: [('irregular periods', 'Symptoms'), ('estrogen', 'Hormones')]  

## Project Structure
clinicalbert-menstrual-ner/  
│  
├── bio_dataset.txt                # BIO-formatted dataset  
├── train_clinicalbert_ner.py      # Training script  
├── predict_ner.py                 # Inference script  
├── eval_metrics.json              # Evaluation results (Precision, Recall, F1)  
├── README.md                      # Project documentation  
│  
└── clinicalbert_ner_out/          # Fine-tuned ClinicalBERT model  
    ├── config.json  
    ├── model.safetensors / pytorch_model.bin  
    ├── tokenizer.json  
    ├── vocab.txt  
    ├── training_args.bin  
    └── checkpoint-*/              # Saved checkpoints  

## Results
From eval_metrics.json:  
{  
  "eval_loss": 0.59,  
  "eval_precision": 0.72,  
  "eval_recall": 0.68,  
  "eval_f1": 0.70  
}  

These results show that the fine-tuned ClinicalBERT model is able to extract key medical entities with good accuracy.

## Next Steps
- Expand the dataset with more annotated IVF conversations.  
- Experiment with adding a CRF layer for improved entity boundary detection.  
- Deploy the trained model as a REST API for integration into EMR systems.  

Author: Sruthi M  
Repository: https://github.com/Sruthi-aiml/clinicalbert-menstrual-ner
