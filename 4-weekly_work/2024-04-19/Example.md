# Uncrtains--去云模型复现

# 模型实验结果  
模型 | RMSE | MAE | PSNR | SAM | SSIM 
--- | --- | --- | --- | --- | ---
Uncrtains MGNLL | 0.030638 | 0.022015 | 30.502849 | 4.43660 | 0.92405
MB_TaylorFormer l2 | **0.022929** | **0.016422** | **33.05454** | **4.22007** | **0.92842**
Swin_Transformer l2 | 0.031529 | 0.022521 | 30.28407 | 5.83186 | 0.86723
MB-Unet++(16-32-64-128)-SAR l2 | 0.025148 | 0.017571 | 32.22073 | 4.07692 | 0.92498
F001 l2 | 0.029336 | 0.020479 | 30.87077 | 4.77194 | 0.91125
F002 l2 | 0.026892 | 0.018900 | 31.67706 | 4.64615 | 0.89592
F003 l2 | 0.028785 | 0.020327 | 31.11134 | 4.91146 | 0.88973
G001 l2 | 0.025992 | 0.018477 | 32.03388 | 4.22486 | 0.90960
G002 l2 | 0.036035 | 0.026857 | 29.04113 | 7.45630 | 0.86437
H001 l2 | 0.026463 | 0.018167 | 31.88498 | 4.21242 | 0.91361

# 集群结果
模型 | RMSE | MAE | PSNR | SAM | SSIM 
--- | --- | --- | --- | --- | ---
Uncrtains MGNLL | 0.035703 | 0.022281 | 29.21935 | 6.51661 | 0.89306
MB-Unet++(16-32-64-128)-SAR l2 | **0.031613** | **0.021538** | **30.26417** | 6.67472 | 0.90519 
F001 l2 | 0.036905 | 0.024346 | 28.91412 | **5.38208** | **0.91226**