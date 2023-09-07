# GEE本地化（大方向/篇数）
[代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-06/2023-09-06-01.txt)

## 存在问题
- RGB图像的输出
- 保存地址的更改

## 解决办法
[代码（RGB)](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-08/2023-09-08-01.txt)  
[代码（SAR）](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-08/2023-09-08-02.txt)  
- 修改对应的Image函数
- 修改关于波段的函数

**实验结果**
数据集 | 波段 | 图像
--- | --- | ---
COPERNICUS/S2_SR | B4 | ![2023-09-08-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/5b85e758-0779-4ed1-8bee-721f67405c45)  
LANDSAT/LC09/C02/T1_L2 | SR_B4 | ![2023-09-08-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/6946fd1a-0211-4d4d-98fb-5c22ea1be029)  
COPERNICUS/S1_GRD | VH |  ![2023-09-08-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/7e7d42ec-a38e-459e-888c-934deb661903)  
COPERNICUS/S1_GRD | VV |  ![2023-09-08-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/2ed49dc4-924b-4dda-82fc-13d7ba9bdfc6)  
