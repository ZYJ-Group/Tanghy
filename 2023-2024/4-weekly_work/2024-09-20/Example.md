# 9.18 周报
## 数据集采集（已完成）  
数据集大小约为960组有云、无云和雷达图像。  

## 自建数据集实验结果  
### 消融实验（已完成）
Method | PSNR↑ | SSIM↑  | MAE↓ | SAM↓ | 
--- | --- | --- | --- | ---
base | 23.233 | 65.854 | 5.601 | 7.269
base + SG-BAFM | 23.301 | 69.731 | 5.605 | 6.831
base + DFIN | 23.769 | 70.795 | 5.266 | 5.919
base + SG-BAFM + DFIN | **23.930** | **71.361** | **4.983** | **5.575**

### 对比实验（待完成）
Method | PSNR↑ | SSIM↑  | MAE↓ | SAM↓ | 
--- | --- | --- | --- | ---
McGAN | 21.365 | 62.360 | 6.753 | 7.537
SpA GAN | 19.891 | 53.375 | 8.271 | 11.289
DSen2-CR | 22.389 | 65.896 | 6.129 | 6.975
UnCRtainTS | 22.684 | 66.261 | 5.876 | 6.647
ours | **23.930** | **71.361** | **4.983** | **5.575**
