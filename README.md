# Comparative Study on Deep Learning for COVID-19 and Pneumonia Detection in Chest X-Rays

BSc Thesis in Computer Science (Data Analysis)  
Università degli Studi di Messina (2025–2026)  
Author: Aklesia Berihu Mekonnen | Supervisor: Prof. Ing. Armando Ruggeri

For the full academic summary, see [`8_Mekonnen_abstract.pdf`](./8_Mekonnen_abstract.pdf).

## What this repo is

Code and results from my bachelor's thesis comparing 9 deep learning setups (CNN, ResNet50, ResNet101, ResNet152, and DenseNet121, trained both from scratch and with transfer learning) on two 3-class chest X-ray classification tasks:

1. **Experiment 1:** COVID-19 vs. Normal vs. Pneumonia
2. **Experiment 2:** Normal vs. Viral Pneumonia vs. Bacterial Pneumonia

All models used the same classification head, augmentation pipeline, optimizer, and training budget. Only weight initialization and the learning rate schedule changed, so the comparison stays fair.

## Datasets

- **Internal (Train / Val / Test):** Mendeley Extensive COVID-19 X-Ray Dataset
- **External Validation:** Kaggle COVID-19 Radiography Dataset (15,153 images), used to test all 9 Experiment 1 models without retraining.

Raw images are not included in this repo.

## Main Results

- **Internal:** DenseNet121 (Scratch) and ResNet152 (Scratch) tied for the top Macro AUC (`0.9980`). Transfer learning did not show a reliable advantage over training from scratch internally.
- **External (15,153 images):** DenseNet121 (Transfer) generalized best (`0.8299` AUC) with the smallest drop, even though it ranked 5th internally.
- **Stats & Explainability:** After Bonferroni correction, only one model pair showed a statistically significant difference. Grad-CAM and Canny ROI overlays were used to check where the models focused.

## Visuals

### Grad-CAM (COVID-19)
![DenseNet121 Grad-CAM](densenet121_gradcam_covid.png)

### Class Distributions
| Experiment 1 (Internal) | Experiment 2 (Internal) | External Validation (Kaggle) |
| :---: | :---: | :---: |
| ![Exp 1 Distribution](class_distribution_exp1.png) | ![Exp 2 Distribution](class_distribution_exp2.png) | ![Kaggle Distribution](kaggle_class_distribution.png) |

## Files

Since all 9 models share the same training pipeline, I included a representative subset of scripts here:

- `01_dataset_setup_eda_split.py` - dataset setup, EDA, and splits
- `09_exp1_densenet121_scratch.py` - Experiment 1 top internal model
- `26_exp2_04_densenet121_transfer_fair_he...` - Experiment 2 training script *(update with full filename)*
- `20_kaggle_external_test_.py` - external evaluation on the Kaggle dataset
- `final_analysis.py` - metric comparisons and statistical tests
- `requirements.txt` - Python dependencies
- `8_Mekonnen_abstract.pdf` - 1-page thesis abstract
