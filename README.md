# Towards Generalizable Deepfake Detection by Primary Region Regularization

> Enhances deepfake detector generalizability by identifying and regularizing the primary (most discriminative) facial region via fused CAM-based heatmaps.

## Authors

**Harry Cheng**<sup>1</sup>, **Yangyang Guo**<sup>1</sup>\*, **Tianyi Wang**<sup>1</sup>, **Liqiang Nie**<sup>2</sup>\*, **Mohan Kankanhalli**<sup>1</sup>

<sup>1</sup> National University of Singapore
<sup>2</sup> Harbin Institute of Technology (Shenzhen)
\* Corresponding authors

## Links

- **Paper**: [ACM ToMM](https://dl.acm.org/doi/10.1145/3777474)
- **arXiv**: [2307.12534](https://arxiv.org/abs/2307.12534)
- **Checkpoint**: [Google Drive](https://drive.google.com/file/d/131TR01kyh1cmM7nMiBr4v3qWjUZ6uMDx/view?usp=drive_link)
- **Sample Heatmaps**: [Google Drive](https://drive.google.com/file/d/1PLGft4uwNpD3k4aEYJFxv_LgDxDIlzPA/view?usp=drive_link)
- **Code Repository**: [GitHub](https://github.com/iLearn-Lab/ToMM25-PRLE)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Method / Framework](#method--framework)
- [Project Structure](#project-structure)
- [Checkpoints / Models](#checkpoints--models)
- [Dataset / Benchmark](#dataset--benchmark)
- [Usage](#usage)
- [TODO](#todo)
- [Citation](#citation)
- [Acknowledgement](#acknowledgement)
- [License](#license)

---

## Updates

- [04/2026] Transfer repos to iLearn-Lab
- [2025] Paper accepted at ACM Transactions on Multimedia Computing, Communications and Applications (ToMM)

---

## Introduction

This repository is the official implementation of **Towards Generalizable Deepfake Detection by Primary Region Regularization**, published in **ACM ToMM**.

Deepfake detectors often overfit to forgery artifacts in non-discriminative facial regions, limiting cross-dataset generalization. This work introduces **PRLE** (Primary Region Localization and Exploitation), which identifies the most discriminative ("primary") facial region via fused Class Activation Maps (CAMs) and uses it as a regularization signal during training.

The method consists of two stages:
1. **Static localization**: Generate primary region maps by fusing CAM maps from a trained detector
2. **Dynamic exploitation**: Apply primary region masks during training to suppress reliance on non-discriminative regions

PRLE is **plug-and-play** — compatible with most existing deepfake detectors without enlarging dataset size. Experiments span five datasets (DFDC, DF-1.0, Celeb-DF, WildDF, FFIW) across seven backbones.

---

## Highlights

- **Plug-and-play**: compatible with most existing deepfake detection backbones
- Primary region discovery via **CAM fusion** — no additional human annotations
- Evaluated on **5 datasets** and **7 backbones** for comprehensive generalization benchmarks
- Does not enlarge dataset size, preserving training efficiency

---

## Method / Framework

### Pipeline

![Pipeline](./Pipeline.png)

**Figure 1.** PRLE pipeline. CAM maps are fused to produce primary region maps, which are applied during training to regularize the model.

---

## Project Structure

```text
.
├── config/
│   └── yaml/
│       └── efficient.yaml      # Main configuration file
├── dataset/                    # Dataset definitions
├── data_load_helper.py         # Data loading utilities
├── heatmap_finetune.py         # Heatmap fine-tuning
├── heatmap_fusion.py           # CAM fusion to generate primary region maps
├── landmark_detect.py          # Facial landmark detection
├── save_and_load_helper.py     # Checkpoint utilities
├── train_effcientnet.py        # Main training script (EfficientNet backbone)
├── train_helper.py             # Training utilities
├── utils/                      # General utilities
├── validation_helper.py        # Validation utilities
├── Pipeline.png                # Pipeline figure
└── README.md
```

---

## Checkpoints / Models

- **Pretrained checkpoint**: [Google Drive](https://drive.google.com/file/d/131TR01kyh1cmM7nMiBr4v3qWjUZ6uMDx/view?usp=drive_link)
- **Sample primary region heatmaps**: [Google Drive](https://drive.google.com/file/d/1PLGft4uwNpD3k4aEYJFxv_LgDxDIlzPA/view?usp=drive_link)

Download and update the checkpoint path in `./config/yaml/efficient.yaml`.

---

## Dataset / Benchmark

Update `./config/yaml/efficient.yaml` with your dataset path. The method supports standard deepfake detection datasets (DFDC, DF-1.0, Celeb-DF, WildDF, FFIW, etc.).

To train, primary region maps must be prepared first:
1. Download sample heatmaps from the link above, or
2. Generate your own via `heatmap_fusion.py` using CAM maps from a trained model

---

## Usage

### Training

Update `./config/yaml/efficient.yaml`, then run:

```bash
python train_effcientnet.py
```

### Inference

Download the pretrained checkpoint, update its path in `./config/yaml/efficient.yaml`, and run:

```bash
python train_effcientnet.py
```

---

## Citation

If you find our paper useful, please cite:

```bibtex
@article{cheng2026towards,
  title={Towards generalizable deepfake detection by primary region regularization},
  author={Cheng, Harry and Guo, Yangyang and Wang, Tianyi and Nie, Liqiang and Kankanhalli, Mohan},
  journal={ACM Transactions on Multimedia Computing, Communications and Applications},
  volume={22},
  number={2},
  pages={1--25},
  year={2026},
}
```

---

## Acknowledgement

- Thanks to our supervisors and collaborators for their valuable support.
- Thanks to the open-source deepfake detection community for providing useful baselines and datasets.

---

## License

This project is released under the Apache License 2.0.
