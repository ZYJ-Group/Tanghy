# GEE本地化（大方向/篇数）
[代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-06/2023-09-06-01.txt)

## 存在问题
**采集样本**  
  需要至少满足以下数据库的要求
- RGB 
cloud landset
- SAR
sentinel

**最大数据量**
**crs: 'EPSG:4326'**

**传入的数据格式**  
![2023-09-06-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/18b1f86b-3718-47b9-b04f-95bed7bd5b69)  

## 解决办法
[代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-07/2023-09-07-01.txt)
- 面对图像一团黑或者一团白 原因可能是minPixelValue和maxPixelValue的值不对  
  查询像素值范围：[代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-07/2023-09-07-02.txt)

**实验结果**
数据集 | 波段 | 图像
--- | --- | ---
COPERNICUS/S2_SR | B4 | ![2023-09-07-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/4e6b03af-827d-4082-a8e2-19ca79da9f80)  
LANDSAT/LC09/C02/T1_L2 | SR_B4 | ![2023-09-07-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/de8317fb-f3c0-434f-9e89-cd8b80bb6009)  
COPERNICUS/S5P/OFFL/L3_CLOUD | cloud_fraction | ![2023-09-07-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/6950861a-1b27-456a-b03a-630aaf8e0414)  
