# AIRR PSF Analysis and AI-based Pre-restoration

This repository contains selected programming work from my research on **AIRR (Aerial Imaging by Retro-Reflection)**.

The main focus is on:

1. **AI-based pre-restoration for AIRR image blur**
2. **PSF inspection and pedestal subtraction for measured AIRR PSFs**

The notebooks are organized as a research portfolio. They include a cleaned AI pre-restoration notebook, an earlier research-process notebook, and a PSF inspection notebook that investigates measured PSF reliability.

---

## Overview

AIRR is an aerial display technology that forms real images in free space using a beam splitter and retro-reflectors. However, the formed aerial image can become blurred due to optical factors such as diffraction, geometrical ray shift, and retro-reflector related manufactoring defects.

In this research, I first investigated whether a CNN could learn **pre-restoration** using synthetic PSFs. After that, I also investigated measured PSF data, focusing on pedestal components, ROI selection, and whether the measured PSF can be used reliably as a convolution kernel.

---

## Recommended Reading Order

### 1. `01_ai_prerestoration_clean_portfolio.ipynb`

Please start from this notebook.

This is the cleaned portfolio version of the AI pre-restoration work. It focuses on a simple single-phase training flow using MSE loss and PSNR-based evaluation.

Main contents:

- Synthetic PSF generation
- AIRR blur simulation using convolution
- Residual U-Net style CNN model
- Single-phase MSE training
- PSNR / SSIM evaluation
- Visual comparison of original, blurred, pre-corrected, and reblurred images

---

### 2. `02_ai_prerestoration_idw_research_process.ipynb`

This notebook is kept as an earlier research-process notebook from the IDW-stage work.

It includes older experimental traces, different PSF models, training attempts, and evaluation cells. It is less clean than the first notebook, but it shows how the AI pre-restoration idea was developed during the research process.

---

### 3. `03_psf_inspection_pedestal_subtraction.ipynb`

This notebook investigates measured AIRR PSF data.

Main contents:

- Measured PSF visualization
- Log-scale and dB-scale inspection
- Bright core center estimation
- ROI selection investigation using a 1/e²-based rule
- Pedestal estimation from border regions
- Pedestal subtraction and clipping
- Unit-sum normalization
- Profile comparison and diagnostic plots

This notebook also shows that simple ROI rules may not fully capture low-intensity tails and ghost-like structures in measured PSFs. Therefore, ROI selection is treated as an ongoing research issue.

---

## Repository Structure

```text
notebooks/
  01_ai_prerestoration_clean_portfolio.ipynb
  02_ai_prerestoration_idw_research_process.ipynb
  03_psf_inspection_pedestal_subtraction.ipynb

dcs/
  研究Portfolio.pdf

sample outputs/
  ai_result.PNG
  psf_roi_decision.PNG
  03_psf_inspection_pedestal_subtraction.PNG
```

---

## Representative Result

In the cleaned AI pre-restoration notebook, the model is trained using MSE loss after applying the forward blur operator. PSNR is used as the main evaluation metric, while SSIM is also reported as a reference.

Example result from one test image:

| Image | PSNR | SSIM |
|---|---:|---:|
| Baseline Blur | 24.01 dB | 0.8771 |
| Final Reblurred after AI Pre-restoration | 25.28 dB | 0.8891 |

This is a representative result under a synthetic PSF condition.

---

## Important Notes

### Data and checkpoints

Full training datasets, raw measured PSF datasets, and trained model checkpoints are not included in this repository.

This repository only contains shareable notebooks, representative screenshots, and a short research portfolio PDF.

### Reproducibility

Some notebooks contain local file paths from the original research environment, such as:

```text
C:\AI_research
```

These paths are kept as part of the research-process record. To run the notebooks on another machine, the paths and data locations need to be adjusted.

### Result variation

The reported PSNR / SSIM values are representative research results. They may vary depending on:

- test image
- selected PSF model
- training condition
- random seed
- software versions
- hardware environment

Therefore, the values should be interpreted as representative experimental results rather than fixed benchmarks.

### PSF visualization note

Some PSF visualizations use an amplitude-style dB mapping using `20log10` for clearer visual contrast. This is used for visualization only. The PSF data itself is handled as intensity data during processing and normalization.

### ROI selection note

A 1/e²-based ROI selection rule was tested in the PSF notebook. However, in the measured PSF shown here, low-intensity tails and ghost-like structures extend outside the core-based ROI. This suggests that ROI selection for measured AIRR PSFs requires further investigation.

### Research-process notebooks

This repository includes notebooks that reflect the research process, not only final polished code. Some cells are kept to show exploratory trials, debugging decisions, and evaluation checks used during the study.

---

## Technologies Used

- Python
- NumPy
- Matplotlib
- OpenCV
- PyTorch
- CUDA
- Jupyter Notebook
- PSNR / SSIM evaluation
- PSF-based convolution simulation

---

## Research Portfolio

A short Japanese research portfolio is included in this repository:

```text
dcs/研究Portfolio.pdf
```

It summarizes the research background, PSF analysis, pedestal subtraction, and AI-based pre-restoration work.

---

## Author

Ahmad Aiman Mirza bin Ahmad Zamri  
Utsunomiya University
