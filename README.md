# Hybrid Deep Learning Model for Tumor and Pulmonary Nodule Segmentation in Non-Small Cell Lung Cancer Using MedSAM

> **Oral Presentation** — 38th Annual Congress of the European Association of Nuclear Medicine (EANM), Barcelona, Spain, October 2025

---

## Authors

**H. Habchi¹**, B. Daoud², S. Mensi³·⁴, K. Chatti⁵

¹ Department of Biophysics and Medical Imaging, Higher Institute of Medical Technologies of Tunis, University of Tunis El Manar, Tunis, Tunisia  
² University of Texas, MD Anderson Cancer Center, Houston, TX, USA  
³ Nuclear Medicine Department, CHU Sahloul, Sousse, Tunisia  
⁴ Department of Biophysics, School of Medicine of Sousse, University of Sousse, Sousse, Tunisia  
⁵ School of Medicine of Monastir, University of Monastir, Monastir, Tunisia  

---

## Overview

Accurate segmentation of lung tumor lesions and pulmonary nodules in ¹⁸F-FDG PET/CT imaging is critical for treatment planning in Non-Small Cell Lung Cancer (NSCLC). This task is inherently challenging for two reasons:

- **Respiratory motion** causes visible shape and size discrepancies between PET and CT scans
- **Small pulmonary nodules** are frequently undetected, directly impacting the accuracy of treatment decisions and the differentiation of benign versus malignant lesions

To address these challenges, we developed a novel hybrid deep learning model that fuses PET/CT and CT modalities for automatic segmentation of lung tumors and pulmonary nodules, built on top of the [MedSAM](https://github.com/bowang-lab/MedSAM) foundation model.

---

## Key Results

| Model | DSC ↑ | sDSC (2mm) ↑ |
|---|---|---|
| **Hybrid-MedSAM (Ours)** | **0.80 ± 0.016** | **0.83 ± 0.021** |
| Hybrid-nnU-Net | 0.77 ± 0.047 | 0.81 ± 0.052 |
| Individual-MedSAM | 0.72 ± 0.018 | 0.76 ± 0.027 |
| Individual-nnU-Net | 0.71 ± 0.057 | 0.77 ± 0.013 |

**Our Hybrid-MedSAM model outperforms all four baselines on both DSC and surface DSC metrics.**

---

## Dataset

- **Total:** 188 ¹⁸F-FDG PET/CT scans of NSCLC patients
  - 168 cases from the public [AutoPET MICCAI 2022 Challenge](https://autopet.grand-challenge.org/)
  - 20 cases from our institution (CHU Sahloul, Sousse, Tunisia)
- **Annotation:** Manual segmentation of lung tumors and pulmonary nodules using the PET Tumor Segmentation extension in [3D Slicer](https://www.slicer.org/), confirmed by a nuclear medicine physician
- **Split:**
  - AutoPET data: 5-fold cross-validation → 100 training / 34 validation / 34 test PET/CT scans
  - Institutional data: used exclusively as external test set

> ⚠️ Institutional patient data cannot be shared publicly due to patient privacy regulations. The AutoPET subset is publicly available via the [AutoPET Challenge](https://autopet.grand-challenge.org/).

---

## Architecture & Methods

### Model Design
Each input modality (PET/CT and CT) is independently processed through a separate **MedSAM encoder** to extract modality-specific features. The extracted features are then merged using an **adaptively weighted ensemble approach**, producing a joint segmentation output. Two separate loss functions are used for joint learning, allowing the model to simultaneously optimize for both modality-specific and fused representations.

### Baselines
Four models were evaluated:

1. **Hybrid-MedSAM** — adaptively weighted ensemble of MedSAM encoders (PET/CT + CT)
2. **Hybrid-nnU-Net** — adaptively weighted ensemble of nnU-Net encoders (PET/CT + CT)
3. **Individual-MedSAM** — standard MedSAM trained on PET/CT only
4. **Individual-nnU-Net** — standard nnU-Net trained on PET/CT only

### Evaluation Metrics
- **Dice Similarity Coefficient (DSC)**
- **Surface Dice Similarity Coefficient at 2mm tolerance (sDSC₂ₘₘ)**

---

## Framework & Tools

```python
# Core frameworks
torch          # Deep learning
monai          # Medical image training framework
SimpleITK      # Image I/O and preprocessing
numpy
scipy

# Annotation
3D Slicer + PET Tumor Segmentation Extension
```

---

## Abstract & Citation

Full abstract available in the [EANM 2025 Abstract Book](./Abstract.pdf#page=12).

```
Habchi H, Daoud B, Mensi S, Chatti K. A Hybrid Deep Learning Model for Tumor 
and Pulmonary Nodule Segmentation in Non-Small Cell Lung Cancer Using MedSAM. 
38th Annual Congress of the European Association of Nuclear Medicine (EANM), 
Barcelona, Spain, October 2025. [Oral Presentation]
```

---

## Code Availability

Code will be made available upon publication of the full manuscript. For collaboration or data access inquiries, please contact the corresponding author.

---

## Corresponding Author

**Habiba Habchi, M.Sc.**  
Biophysicist & ML Researcher · Medical Image Analysis · PET/CT · Precision Oncology
Department of Nuclear Medicine, CHU Sahloul, Sousse, Tunisia  
[LinkedIn](https://www.linkedin.com/in/habiba-habchi-2b2a72257/) · [ORCID](https://orcid.org/0009-0000-1703-7406)
