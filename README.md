# A-Noob_GeoSnap_submission
Geo Snap - Land Use Classification &amp; Explainability from Space
# A-Noob_GeoSnap_submission
## Geo Snap — Land-Use Classification & Explainability from Space
**SOI × Cosmosoc | Data Science Competition**

---

## Team Details
- **Team Name:A Noob** YourTeamName
- **Event:** Geo Snap — SOI × Cosmosoc

---

## Project Overview
This project builds intelligent models to classify land-use from 
satellite imagery using the EuroSAT dataset (Sentinel-2) and explains 
why those predictions are made.

**Two models were built and compared:**
- RGB Model (3 bands) → 97.80% validation accuracy
- Multispectral Model (13 bands) → 98.44% validation accuracy

---

## Repository Structure
---

## Setup Instructions

### Requirements
- Python 3.10+
- Google Colab with T4 GPU
- Google Drive with dataset uploaded

### Dependencies
```bash
pip install torch torchvision
pip install lime
pip install rasterio
pip install seaborn scikit-learn
pip install matplotlib numpy pandas pillow
```

### Dataset Setup
1. Download EuroSAT_Dataset.zip from the provided link
2. Upload to Google Drive
3. Run the setup cell in each notebook to mount Drive and unzip

---

## How to Run

### Task 1A — RGB Classification
1. Open `Task1_RGB.ipynb` in Google Colab
2. Enable T4 GPU: `Runtime → Change runtime type → T4 GPU`
3. Run all cells: `Runtime → Run all`
4. Model saves to Drive as `best_efficientnet_rgb.pth`
5. Predictions save as `rgb_predictions.csv`

### Task 1B — Multispectral Classification
1. Open `Task1_Multispectral.ipynb` in Google Colab
2. Enable T4 GPU
3. Run all cells
4. Model saves to Drive as `best_efficientnet_ms.pth`
5. Predictions save as `ms_predictions.csv`

### Task 2 — Explainability
1. Open `Task2_Explainability.ipynb` in Google Colab
2. Enable T4 GPU
3. Requires both models already trained and saved to Drive
4. Run all cells

---

## Model Architecture
- **Base Model:** EfficientNet-B0 (pretrained on ImageNet)
- **RGB Model:** Standard EfficientNet-B0, final layer → 10 classes
- **Multispectral Model:** Modified first conv layer
  (3→13 input channels), final layer → 10 classes
- **Training:** 15 epochs, Adam optimizer,
  CosineAnnealingLR scheduler, batch size 32

---

## Results Summary

### Classification Performance
| Model | Val Accuracy | Parameters |
|---|---|---|
| RGB (EfficientNet-B0) | 97.80% | 4.0M |
| Multispectral (EfficientNet-B0) | 98.44% | 4.0M |

### Per Class F1 Scores
| Class | RGB F1 | MS F1 |
|---|---|---|
| AnnualCrop | 0.97 | 0.98 |
| Forest | 0.98 | 0.99 |
| HerbaceousVegetation | 0.94 | 0.98 |
| Highway | 0.95 | 0.98 |
| Industrial | 0.97 | 0.99 |
| Pasture | 0.94 | 0.97 |
| PermanentCrop | 0.90 | 0.97 |
| Residential | 0.99 | 0.99 |
| River | 0.96 | 0.99 |
| SeaLake | 0.99 | 1.00 |

### Key Findings
- Multispectral beats RGB by **+0.64%**
- **B8 NIR** is the most important band — 29.09% accuracy drop when removed
- **PermanentCrop** shows biggest improvement with spectral data (0.90→0.97)
- **SeaLake** achieves perfect 1.00 F1 score with multispectral data

---

## Explainability Highlights
- **LIME** used for visual explainability on RGB model
- **Band ablation** study identifies most important Sentinel-2 bands
- **NDVI:** Forest (0.68) and Pasture (0.65) have highest vegetation density
- **NDWI:** SeaLake (0.44) is the only class with positive water content

---

## Files in This Repository
| File | Description |
|---|---|
| `Task1_RGB.ipynb` | RGB model training and inference |
| `Task1_Multispectral.ipynb` | Multispectral model training and inference |
| `Task2_Explainability.ipynb` | All explainability analysis |
| `predictions/rgb_predictions.csv` | RGB test set predictions |
| `predictions/ms_predictions.csv` | Multispectral test set predictions |
| `report/technical_report.pdf` | Technical report |

---

