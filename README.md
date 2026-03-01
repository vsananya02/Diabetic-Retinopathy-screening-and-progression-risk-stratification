# Diabetic Retinopathy Screening & Progression Risk Stratification

Multimodal deep learning system for diabetic retinopathy (DR) detection and personalized progression risk assessment. Integrates retinal fundus images with clinical HbA1c data using a **DenseNet121-based architecture**, achieving **79.93% validation accuracy** on 1,096 images. Provides DR severity classification, 6/12-month risk estimates, clinical recommendations, and **LIME visual explainability**.

## Project Overview

Diabetic retinopathy is a major cause of preventable blindness. Early detection and personalized risk stratification can significantly improve outcomes. This project develops a **multi-input neural network** that:
- Classifies DR into 5 severity levels: Mild, Moderate, No_DR, Proliferate_DR, Severe.
- Boosts accuracy by +6.39% over image-only baseline (73.54% -> 79.93%) via HbA1c integration.
- Uses a VTDR-inspired calculator for progression risks and screening intervals.
- Includes **LIME explainability** to show which retinal regions drive predictions.

## Key Features & Innovations

- **DR Severity Classification** - Predicts from fundus images (224×224×3) with 79.93% accuracy.
- **Multimodal Fusion** - Combines DenseNet121 image features (256) + HbA1c clinical features (16) for improved discrimination.
- **Personalized Risk Assessment** - Estimates 6- and 12-month progression risks using DR grade, HbA1c, age, diabetes duration, and systolic BP.
- **Clinical Recommendations** - Suggests next screening interval (1–12 months) and actions (e.g., "Immediate referral" for Very High Risk).
- **HbA1c Impact Comparison** - Shows how changing HbA1c (6.5%, 8.5%, 10.5%) affects risk for the **same retinal image** - demonstrates precision medicine.
- **LIME Explainability** - Generates visual heatmaps and overlays highlighting influential retinal regions (e.g., lesions, vessels, macula). 
- **Patient-Friendly Summaries** - Simple, non-technical notes for each DR grade.
- **Research Prototype Disclaimer** - For educational/research use only — not for clinical diagnosis.

## Technologies & Tools Used

- **Deep Learning Framework**: TensorFlow 2.17.0 + Keras 3.x
- **Backbone Architecture**: DenseNet121 (pretrained on ImageNet, frozen up to layer 100, fine-tuned 101–121)
- **Explainability**: LIME (Local Interpretable Model-agnostic Explanations) with 80–100 perturbations
- **Image Processing**: OpenCV (headless), Pillow, scikit-image
- **Evaluation & Visualization**: scikit-learn, matplotlib, seaborn
- **Other Libraries**: numpy, pandas, tqdm (progress bars)

## Dataset Details

Public diabetic retinopathy dataset of colored retinal fundus images (APTOS 2019).

- **Validation Set**: 1,096 images
- **Class Distribution (Validation)**:
  - Mild: 111
  - Moderate: 299
  - No_DR: 541 (~49%, majority)
  - Proliferate_DR: 88
  - Severe: 57 (~5%, minority)
- **Training Set** (approx.): ~2,566 images
- **Image Specs**: 224×224×3 RGB
- **HbA1c Data**: Synthetic, literature-based distributions:
  - No_DR: ~6.86%
  - Mild: ~7.85%
  - Moderate: ~8.65%
  - Severe: ~9.79%
  - Proliferate_DR: ~10.24%
  - Range: 4.0%–14.0% (clipped)

## Performance on Validation Set (1,096 images)

**Overall Accuracy**: 79.93%  
**Macro-averaged** (balanced across all classes):  
- Precision: 0.6371  
- Recall: 0.5826  
- F1-Score: **0.5962**  

**Weighted-averaged** (favors majority class):  
- F1-Score: 0.7851  

**Per-class Metrics**:

| Class            | Precision | Recall  | F1-Score | Support |
|------------------|-----------|---------|----------|---------|
| Mild             | 0.6126    | 0.6126  | 0.6126   | 111     |
| Moderate         | 0.6954    | 0.9894  | 0.7481   | 299     |
| No_DR            | 0.9480    | 0.9778  | 0.9627   | 541     |
| Proliferate_DR   | 0.5233    | 0.5320  | 0.5276   | 88      |
| Severe           | 0.4034    | 0.2632  | 0.3191   | 57      |

**Notes**:
- Excellent on No_DR and Moderate.
- Lower recall on rare classes due to imbalance.
- Macro F1 (0.5962) shows balanced performance - crucial for detecting vision-threatening DR.

**Improvement**: +6.39% accuracy over image-only DenseNet121 baseline (73.54%).

## Features to Highlight

1. **LIME + Overlay Visualization** - Shows red-highlighted regions (lesions/vessels) influencing prediction.
2. **HbA1c Sensitivity Analysis** - Proves same image + different HbA1c -> different urgency (precision medicine).
3. **VTDR-based Risk Calculator** - Personalized 6/12-month risks + category (Low -> Very High) + screening advice.
4. **Class Imbalance Handling** - Demonstrates macro F1 as honest metric for rare severe cases.
5. **End-to-End Pipeline** - From image upload -> prediction → explanation -> clinical recommendation.
