# SicklePrenatal: Biometric-Guided Deep Learning for Early Sickle Cell Risk Detection from Fetal Ultrasound

## Abstract
Sickle Cell Disease (SCD) is one of the most prevalent inherited disorders in Sub-Saharan Africa, yet limited prenatal screening leads to high infant mortality. We present SicklePrenatal, an attention-based deep learning framework for early, non-invasive SCD risk prediction from fetal ultrasound in low-resource settings.

Our approach integrates two complementary streams: (1) a structure-preserving encoder enhanced with Sobel-Laplacian filters for vascular edge detection, and (2) a biometric encoder informed by gestational age and key fetal measurements (head circumference, femur length, abdominal diameter). A cross-attention module fuses both branches, capturing clinically relevant patterns under weak supervision.

To address the lack of labeled datasets, we design a proxy-based annotation pipeline grounded in clinical heuristics and literature-backed thresholds. We further pretrain with a contrastive self-supervised objective on grayscale ultrasound frames, and fine-tune on a dataset of 3,382 scans from a regional health clinic.

SicklePrenatal achieves 76.2% accuracy, surpassing baseline CNNs (63.7%) and ResNet classifiers (69.1%), while preserving interpretability through saliency maps localized around high-risk vascular zones. The model is optimized for edge deployment, enabling inference on low-compute devices.

This work contributes a scalable, low-cost framework for prenatal SCD screening, with potential to generalize to other hemoglobinopathies and fetal-risk disorders, advancing maternal-fetal healthcare in underserved populations.

---

## Baseline Comparison

| Model             | Accuracy | Macro F1 | Silhouette Score |
|-------------------|----------|----------|------------------|
| Metadata Only     | 61.4%    | 59.2%    | 0.41             |
| Image Only        | 64.8%    | 61.5%    | 0.46             |
| Multimodal (Ours) | 76.2%    | 73.9%    | 0.59             |
| Multimodal + SCL  | 76.2%    | 73.9%    | 0.65 (+12.3%)    |

---

## Method Overview (diagram)
```mermaid
flowchart LR
    US[Ultrasound frames] --> SE[Structure-preserving encoder\n+ Sobel/Laplacian]
    MD[Gestational age + HC + FL + AC] --> BE[Biometric encoder]
    SE --> CA[Cross-attention fusion]
    BE --> CA
    CA --> P[Risk prediction]
