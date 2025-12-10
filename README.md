# cv5561-f25-team-diffusion
Title: Image generation using diffusion model  
member:  
Cheng-Fu Tseng,  tseng097@umn.edu  
Shilong Xiang,   xiang218@umn.edu  
Angel Gallegos,  galle289@morris.umn.edu  

The objective is to restore noisy medical images into
clear, high-quality, ones thereby improving the accuracy
of diagnosis and subsequent analyses.

Project code is in the project.ipynb. Result and the detail are in this notebook.
General speaking, we construct 2 model, which are a simple U-net diffusion and a denoising CNN. 
Finally, after training CNN on medical image and denosing them, 
we using transfer learning to denosing other type of images.

In this github folder, you will see several .pth files(storing trained model parameters in PyTorch.).
The "diffusion_ct.pth" use in diffusion model;
The "cnn_denoiser" use in CNN
The "cnn_cartoon_finetune" use in the transfer learing.
Other pth files are the toy examples, which does not have enough epoch and step in diffusion model.