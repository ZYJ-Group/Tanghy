# GEE本地化
## 结果展示
范围：120，30，120.1，30.1  
日期：2022.01.01-2022.07.11  
数据集 | 波段 | 开发环境 | 结果图 | 耗时 | 代码链接
----  | --- | --- | --- | --- | ---
COPERNICUS/S1_GRD | 'VV', 'VH' | nodejs | ![2023-10-08-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/71c1d2b1-a412-4092-97cb-dd40a10b76d2) | 18.831 | [链接](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-10-08/2023-10-08-01.txt)
COPERNICUS/S1_GRD | 'VV', 'VH' | python | ![2023-10-08-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/fb72cd57-88b3-4eb8-8f20-4d05108cec42) | 17 | [链接](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-10-08/2023-10-08-03.txt)
COPERNICUS/S2_HARMONIZED | 'B4', 'B3', 'B2' | nodejs | ![2023-10-08-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/a074b7c2-9427-4d0d-abdc-02efcde4f4b4) | 34.668 | [链接](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-10-08/2023-10-08-02.txt)
COPERNICUS/S2_HARMONIZED | 'B4', 'B3', 'B2' | python | ![2023-10-08-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f068f740-870a-4817-9e0f-1ed96aefaab8) | 18 | [链接](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-10-08/2023-10-08-04.txt)

### COPERNICUS/S2_HARMONIZED 的 'B4', 'B3', 'B2'生成图像存在较大差异。   
数据集 | 开发环境 | 时间 | 结果图
----  | --- | --- | --- 
COPERNICUS/S2_HARMONIZED | python | 2020.1-2020.7 | ![2023-10-08-06](https://github.com/ZYJ-Group/Tanghy/assets/94824386/dab11f23-dbee-4a2a-a15d-e439bbb0e4fa)
COPERNICUS/S2_HARMONIZED | python | 2022.1-2022.7 | ![2023-10-08-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f068f740-870a-4817-9e0f-1ed96aefaab8) 
COPERNICUS/S2_HARMONIZED | nodejs | 2020.1-2020.7 | ![2023-10-08-05](https://github.com/ZYJ-Group/Tanghy/assets/94824386/c57542f7-b1f1-482d-94b6-a213552f4239) 
COPERNICUS/S2_HARMONIZED | nodejs | 2022.1-2022.7 | ![2023-10-08-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/ae82f207-cc21-4d91-82a4-bf2a8761b8ef) 
