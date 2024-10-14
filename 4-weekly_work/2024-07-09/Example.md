# 网络模型框架图
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/0d92f378-bfe6-421b-83a8-cd449ff5e662)  


# 实验结果 
## 消融实验  
Method | PSNR↑ | SSIM↑  | MAE↓ | SAM↓ | 
--- | --- | --- | --- | --- |
base | 29.403 | 89.029 | 2.415 | 6.725
base + SG-BAFM | 30.604 | 90.600 | 2.051 | 5.136
base + DFIN | 30.555 | 90.282 | 2.031 | 5.005
base + SG-BAFM + DFIN | **31.050** | **90.618** | **1.929** | **4.912** 


## 对比实验  
Method | PSNR↑ | SSIM↑  | MAE↓ | SAM↓ | 
--- | --- | --- | --- | --- |
McGAN | 26.368 | 76.853 | 3.408 | 13.851
SpA GAN | 26.084 | 81.107 | 3.373 | 12.863
DSen2-CR | 29.862 | 88.056 | 2.216 | 5.165
UnCRtainTS | 29.373 | 89.745 | 2.166 | 6.445
ours |  **31.050** | **90.618** | **1.929** | **4.912** 

![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/7330d4d8-1171-48d6-a928-90579a298c38)
