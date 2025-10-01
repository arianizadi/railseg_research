# 📅 MMSegmentation Installation & Inference Guide

A clear, beginner-friendly walkthrough to set up [MMSegmentation](https://github.com/open-mmlab/mmsegmentation) for semantic segmentation using a tested and stable configuration.

---

## 🧠 Why This Guide?
The official setup instructions often run into compatibility issues. This version has been tested and works on:

- **UNLV's AI SERVER** with CUDA 11.8 & 10 installed
- **My Local Machine** with CUDA 12.8 installed

If you're new to MMSeg or machine learning tooling, this guide will walk you through every step.

---

## 📦 Step-by-Step Installation

### 1. Create a Python Environment
This isolates your setup from other projects.
```bash
conda create -n openmmlab python=3.8 -y
conda activate openmmlab
```

### 2. Install PyTorch with CUDA Support
Choose the version that works with MMSegmentation and your GPU drivers.
```bash
pip install torch==2.1.0+cu121 torchvision==0.16.0+cu121 \
  -f https://download.pytorch.org/whl/torch_stable.html
```

### 3. Install MMCV (Core Dependency)
MMSeg depends on MMCV for ops and runtime support.
```bash
pip install mmcv==2.1.0 \
  -f https://download.openmmlab.com/mmcv/dist/cu121/torch2.1/index.html
```

### 4. Install MMSegmentation (Clone my mmseg repo or the official)
```bash
pip install -r requirements.txt
pip install -ve .
```

---

## 🔧 Verifying the Installation
We’ll run a pre-trained model on a sample image to ensure everything is working.

### Step 1: Download Model Files
Use `mim` (OpenMMLab installer) to grab a model config and pretrained weights.
```bash
pip install -U openmim
mim download mmsegmentation \
  --config pspnet_r50-d8_4xb2-40k_cityscapes-512x1024 \
  --dest .
```

This will download:
- `pspnet_r50-d8_4xb2-40k_cityscapes-512x1024.py` (model config)
- `pspnet_r50-d8_512x1024_40k_cityscapes_20200605_003338-2966598c.pth` (model weights)

### Step 2: Run Inference on a Sample Image
```bash
python demo/image_demo.py demo/demo.png \
  pspnet_r50-d8_4xb2-40k_cityscapes-512x1024.py \
  pspnet_r50-d8_512x1024_40k_cityscapes_20200605_003338-2966598c.pth \
  --device cuda:0 --out-file result.jpg
```

> 💡 Make sure your `demo/demo.png` file exists. You can use any image.

After the command runs, check the generated `result.jpg` — it will show the input image with predicted segmentation masks overlayed.

---
