# Uncrtains--去云模型复现

# 模型实验结果  
模型 | RMSE | MAE | PSNR | SAM | SSIM 
--- | --- | --- | --- | --- | ---
Uncrtains MGNLL | 0.030638 | 0.022015 | 30.502849 | 4.43660 | 0.92405
Uncrtains l2 | 0.029236 | 0.021148 | 30.93103 | 4.97689 | 0.91461
MB_TaylorFormer l2 | **0.022929** | **0.016422** | **33.05454** | **4.22007** | **0.92842**
Swin_Transformer l2 | 0.031529 | 0.022521 | 30.28407 | 5.83186 | 0.86723
MB-Unet(64-128-256-512-1024) l2 | 0.033119 | 0.023700 | 29.76443 | 5.35992 | 0.83499 
MB-Unet(16-32-64-128-256) l2 | 0.032504 | 0.022475 | 29.95579 | 5.69498 | 0.85839 


# 模型图展示
**Uncrtains**
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/4c5ea776-4858-4f85-bfce-17913968d064)  


**MB_TaylorFormer**
<img width="1428" alt="pipeline" src="https://github.com/ZYJ-Group/Tanghy/assets/94824386/a62e793e-88c2-4452-8f3f-71d411baa22b">  
