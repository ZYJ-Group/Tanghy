# GEE平台开发（大方向/篇数）
## 需要改进的地方
1. 导出图片的时间过长
2. 过大的范围无法导出  
![2023-09-17-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/5f41ab13-4566-440b-94cb-e05c9f354794)  
3. 导出的图片保留云  
4. 固定最大最小像素值  
(ps.原先的代码:[RGB](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-17/2023-09-17-02.txt)  [SAR](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-17/2023-09-17-01.txt))  
 
## 改进之后  
数据库 | 波段 | 现在的代码 | 现在的时间 |现在的图像
--- | --- | --- | --- | --- 
COPERNICUS/S2_HARMONIZED | 'B4', 'B3', 'B2' | [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-17/2023-09-17-03.txt) | 70.442 seconds | ![2023-09-17-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/2662bf9e-ee1a-4391-ac1f-ffdf839c536a)  
COPERNICUS/S1_GRD | 'VV', 'VH' | [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-17/2023-09-17-04.txt) | 60.905 seconds | ![2023-09-17-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/49e424c3-864b-4628-b540-1422a6ba6fe0)  


