
# YOLOv10 Adversarial Patch Attack Evaluation

Evaluation of YOLOv10 robustness against adversarial patch attacks in white-box settings, with transferability analysis and defense strategies.

## Quick Start

### Prerequisites
- Python 3.8+
- pip or conda
- Jupyter Notebook
- GPU (recommended) or CPU with 8GB+ RAM

### Installation

#### Step 1: Create Virtual Environment
```bash
cd YOLOv10-Adversarial-Patch-Project
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

#### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```

This installs:
- PyTorch & torchvision
- YOLOv10 (ultralytics)
- Faster R-CNN
- Jupyter, matplotlib, numpy, pandas, opencv-python

#### Step 3: Download Datasets

**MS COCO 2017:**
```bash
# Download val2017 from https://www.kaggle.com/datasets/bardiaardakanian/mmsample
# Extract to datasets/MSCOCO_subset_5k/val2017/
```

**APRICOT v1.0:**
```bash
# Download from https://apricot.mitre.org/download/
# Extract to datasets/APRICOTv1.0/
```

**YOLOv10 Weights:**
```bash
# Auto-downloads on first run, or manually download yolov10n.pt to project root
```

### Running the Project

#### Launch Jupyter
```bash
jupyter notebook adversarial_patch_yolov10_fixed.ipynb
```

#### Execution Flow
Run cells sequentially from top to bottom:

1. **Setup** — Imports, DEVICE configuration, path initialization
2. **Model Loading** — Load YOLOv10-n and Faster R-CNN-ResNet50
3. **Utilities** — Helper functions (patch generation, attack, defense)
4. **PGD Attack** — Generate adversarial patches via gradient optimization
5. **Baseline Evaluation** — Clean performance on COCO and APRICOT
6. **Attack Evaluation** — Apply patches, measure detection suppression
7. **Transferability** — Test cross-architecture transfer (YOLOv10 → Faster R-CNN)
8. **Defense Evaluation** — Bilateral filter recovery effectiveness
9. **Figure Generation** — Create Figure 2 (patches) and Figure 3 (metrics)
10. **Results Aggregation** — Save JSON results and statistics

**Expected Runtime:** 30–60 minutes (GPU), 2–3 hours (CPU)

### Output Files

Generated in `results/` directory:
- `fig1_digital_attacks.png` — Overview dashboard
- `fig2a_coco_patches.png` — COCO patch visualization
- `fig2b_apricot_patches.png` — APRICOT samples
- `fig3a_precision_recall_f1.png` — Patch size impact
- `fig3b_rotation_analysis.png` — Rotation robustness
- `attack_coco.json` — Attack results
- `baseline_coco.json` — Clean baseline metrics
- `defence_results.json` — Defense recovery metrics
- `transferability.json` — Cross-model transfer rates
- `map_results.json` — Aggregated mAP/F1 analysis

## Hardware Requirements

| Setup | Time | RAM | Notes |
|-------|------|-----|-------|
| **GPU (NVIDIA)** | 30–60 min | 8GB | Recommended |
| **CPU only** | 2–3 hours | 8GB+ | Slower but works |
| **Storage** | — | 20GB | Datasets + weights |

## Troubleshooting

**Out of Memory Error:**
```python
# In notebook, reduce:
ATTACK_N = 20  # was 50
```

**Dataset Not Found:**
```python
# Verify paths match your structure:
COCO_IMGS = DATASETS_DIR / 'MSCOCO_subset_5k' / 'val2017'
APRICOT_TEST = DATASETS_DIR / 'APRICOTv1.0' / 'Images' / 'test'
```

**GPU Not Detected:**
```python
# Code auto-falls back to CPU, or force:
DEVICE = 'cpu'
```

## Submission Contents

- `report.pdf` — IEEE-formatted report
- `project.ipynb` — Complete reproducible notebook
- `requirements.txt` — All dependencies
- `README.md` — This file

See Appendix A in the report for detailed setup and file structure instructions.