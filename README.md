# AIRR PSF Analysis and AI-based Pre-restoration

This repository contains selected programming work from my research on **AIRR (Aerial Imaging by Retro-Reflection)**.

The main focus is on:

1. **AI-based pre-restoration for AIRR image blur**
2. **PSF inspection and pedestal subtraction for measured AIRR PSFs**

The notebooks are organized as a research portfolio. They include a cleaned AI pre-restoration notebook, an earlier research-process notebook, and a PSF inspection notebook that investigates measured PSF reliability.

---

## Overview

AIRR is an aerial display technology that forms real images in free space using a beam splitter and retro-reflectors. However, the formed aerial image can become blurred due to optical factors such as diffraction, geometrical ray shift, and retro-reflector related manufacturing defects.

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

#######################################################################
---

# 日本語概要

このリポジトリは、**AIRR (Aerial Imaging by Retro-Reflection)** に関する研究で作成したプログラミング成果物を整理したものです。

主な内容は以下の2点です。

1. **AIRR画像のぼけに対するAI事前復元**
2. **実測AIRR PSFの解析およびペデスタル成分の除去**

本リポジトリは研究ポートフォリオとして構成しており、整理済みのAI事前復元ノートブック、初期研究段階のノートブック、実測PSFの信頼性を検討するノートブックを含んでいます。

---

## 概要

AIRRは、ビームスプリッターと再帰反射素子を用いて、空中に実像を形成する空中表示技術です。一方で、形成される空中像には、回折、幾何学的な光線ずれ、再帰反射素子の製造誤差などの光学的要因により、点広がりが生じることがあります。

本研究では、まず合成PSFを用いて、CNNがAIRR画像のぼけを考慮した**事前復元**を学習できるかを検討しました。その後、実測PSFに含まれるペデスタル成分、ROI選択、実測PSFを畳み込みカーネルとして信頼して使用できるかについても検討しました。

---

## 推奨閲覧順

### 1. `01_ai_prerestoration_clean_portfolio.ipynb`

まずはこちらのノートブックをご覧ください。

これは、AI事前復元の内容をポートフォリオ用に整理したノートブックです。MSE損失を用いたシンプルな単一フェーズの学習と、PSNRを中心とした評価に焦点を当てています。

主な内容：

- 合成PSFの生成
- 畳み込みによるAIRRのぼけシミュレーション
- Residual U-Net型のCNNモデル
- MSEによる単一フェーズ学習
- PSNR / SSIMによる評価
- 元画像、ぼけ画像、事前補正画像、再ぼけ画像の比較

---

### 2. `02_ai_prerestoration_idw_research_process.ipynb`

このノートブックは、IDW段階の初期研究プロセスを残したものです。

異なるPSFモデル、学習方法の試行、評価セルなど、当時の実験過程が含まれています。1つ目のノートブックほど整理されてはいませんが、AI事前復元の考え方をどのように発展させたかを示すために残しています。

---

### 3. `03_psf_inspection_pedestal_subtraction.ipynb`

このノートブックでは、実測AIRR PSFデータを解析しています。

主な内容：

- 実測PSFの可視化
- ログスケールおよびdBスケールでの確認
- 明るい中心コアの中心推定
- 1/e²に基づくROI選択の検討
- 境界領域を用いたペデスタル成分の推定
- ペデスタル成分の減算とクリッピング
- 総和1への正規化
- プロファイル比較および診断用プロット

このノートブックでは、単純なROI選択ルールでは、実測PSFに含まれる低強度のテールやゴースト状の構造を十分に含められない可能性があることも確認しています。そのため、ROI選択は今後も検討が必要な研究課題として扱っています。

---

## リポジトリ構成

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

## 代表的な結果

整理済みのAI事前復元ノートブックでは、forward blur operatorを適用した後のMSEを用いてモデルを学習しています。主な評価指標としてPSNRを使用し、参考指標としてSSIMも表示しています。

あるテスト画像に対する代表例：

| Image | PSNR | SSIM |
|---|---:|---:|
| Baseline Blur | 24.01 dB | 0.8771 |
| Final Reblurred after AI Pre-restoration | 25.28 dB | 0.8891 |

これは、合成PSF条件下での代表的な結果です。

---

## 注意事項

### データとチェックポイントについて

本リポジトリには、完全な学習データセット、実測PSFの生データ、学習済みモデルのチェックポイントは含めていません。

公開可能な範囲で、ノートブック、代表的なスクリーンショット、短い研究ポートフォリオPDFのみを掲載しています。

### 再現性について

一部のノートブックには、元の研究環境で使用していたローカルパスが含まれています。

```text
C:\AI_research
```

これらは研究プロセスの記録として残しています。別の環境でノートブックを実行する場合は、パスやデータの配置を調整する必要があります。

### 結果の変動について

掲載しているPSNR / SSIMの値は代表的な研究結果です。以下の条件によって変動する可能性があります。

- 使用するテスト画像
- 選択するPSFモデル
- 学習条件
- ランダムシード
- ソフトウェアのバージョン
- ハードウェア環境

そのため、これらの値は固定されたベンチマークではなく、代表的な実験結果としてご覧ください。

### PSF可視化について

一部のPSF可視化では、見やすさを重視して `20log10` による振幅風のdB表示を使用しています。これは可視化のための処理であり、PSFデータ自体は強度データとして処理・正規化しています。

### ROI選択について

PSFノートブックでは、1/e²に基づくROI選択ルールを試しています。しかし、実測PSFでは低強度のテールやゴースト状の構造が中心コアに基づくROIの外側まで広がっていることが確認されました。そのため、実測AIRR PSFに対するROI選択は、今後さらに検討が必要な課題です。

### 研究プロセスを含むノートブックについて

本リポジトリには、最終的に整理されたコードだけでなく、研究の過程を示すノートブックも含まれています。一部のセルは、試行錯誤、デバッグ、評価確認の過程を示すために残しています。

---

## 使用技術

- Python
- NumPy
- Matplotlib
- OpenCV
- PyTorch
- CUDA
- Jupyter Notebook
- PSNR / SSIM評価
- PSFに基づく畳み込みシミュレーション

---

## 研究ポートフォリオ

短い日本語の研究ポートフォリオPDFを以下に含めています。

```text
dcs/研究Portfolio.pdf
```

研究背景、PSF解析、ペデスタル成分の除去、AI事前復元についてまとめています。
