# cv5561-f25-team-diffusion

**Title:** Image generation using diffusion model (Medical image denoising + transfer learning)  
**Members:**  
- Cheng-Fu Tseng — tseng097@umn.edu  
- Shilong Xiang — xiang218@umn.edu  
- Angel Gallegos — galle289@morris.umn.edu  

## Overview
This project restores noisy (low-dose) medical CT images into clearer, higher-quality images to support diagnosis and analysis. We implement and compare:
1) a **simple U-Net diffusion model** for denoising/reconstruction, and  
2) a **CNN denoiser** trained on medical images.  
We also demonstrate **transfer learning** by fine-tuning the CNN to denoise a different image domain.

All results and details are in **`project.ipynb`**.

## Environment Setup

### Option A: Conda (recommended)
```bash
conda create -n cv5561-diffusion python=3.10 -y
conda activate cv5561-diffusion
pip install -U pip
pip install jupyter numpy matplotlib pillow opencv-python
# PyTorch (choose ONE)
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121   # CUDA 12.1
# or CPU:
# pip install torch torchvision
```

### Option B: pip only
```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -U pip
pip install jupyter numpy matplotlib pillow opencv-python torch torchvision
```

## Dataset Setup

The notebook expects the CT dataset under this exact directory structure:

```text
./dataset/512/
  ├── Full Dose/1mm/Sharp Kernel (D45)/<PATIENT_ID>/*.png
  └── Quarter Dose/1mm/Sharp Kernel (D45)/<PATIENT_ID>/*.png
```

- Place your downloaded dataset files into `dataset/512/...` so the paths above exist.
- The notebook uses a Windows-style base path: `os.getcwd() + r"\dataset\512"`.
  - If you run on macOS/Linux, change it to `os.path.join(os.getcwd(), "dataset", "512")`.

(Optional) If you use the test loader in the notebook, it expects:
```text
./dataset/testing/
  ├── Full dose/*.png
  └── Quarter dose/*.png
```

## How to Run

Open and run the notebook top-to-bottom:

```bash
jupyter notebook project.ipynb
```

### What you will run inside `project.ipynb`
Please run in this order (cells are already organized this way):

1) **Load dataset & visualize samples**  
2) **Diffusion model (Simple U-Net)**  
   - Train (optional) and/or load weights `diffusion_ct.pth`
   - Run sampling (reverse diffusion) to denoise images
3) **CNN denoiser**
   - Train (optional) and/or load weights `cnn_denoiser.pth`
   - Evaluate PSNR/SSIM and compare with baselines
4) **Transfer learning demo**
   - Fine-tune the CNN on a single image with augmentation + synthetic noise  
   - Save/load weights `cnn_cartoon_finetune.pth` and run out-of-domain denoising

## Model Weights (.pth)

- `diffusion_ct.pth` — diffusion model weights (SimpleUNet)
- `cnn_denoiser.pth` — CNN denoiser weights (ResCNN)
- `cnn_cartoon_finetune.pth` — CNN after transfer learning fine-tuning
- Other `.pth` files are toy/partial runs
