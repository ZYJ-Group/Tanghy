# GEE数据库
## 一、关键信息
了解一个常用的 Google Earth Engine（GEE）数据库，您需要掌握以下关键信息：

1. **数据库名称或数据集标识：** 每个数据集在 GEE 中都有一个唯一的名称或标识符，用于在代码中引用它。

2. **数据类型**：了解数据集的类型，是影像、矢量数据、栅格数据还是表格数据等。

3. **数据内容**：明确数据集包含的内容，例如卫星影像、气象数据、地形数据、土地覆盖分类等。

4. **时间范围**：数据集覆盖的时间范围，以便您确定可用于分析的时间段。

5. **地理范围**：数据集覆盖的地理区域，以便您选择感兴趣的区域。

6. **数据分辨率**：了解数据集的空间分辨率，这会影响分析的精度和计算成本。

7. **数据来源**：数据集的来源机构或卫星/传感器名称，以便您了解数据的可靠性和适用性。

8. **数据质量**：了解数据的质量和精度等级，有助于评估数据是否适合您的研究目的。

9. **数据访问方式**：了解如何通过 GEE 代码访问数据集，通常是使用 ee.Image() 或 ee.ImageCollection() 等函数加载数据。

10. **数据属性和波段**：了解数据集的属性信息，例如数据的波段数、波段名称和单位等。

11. **数据预处理要求**：有些数据集可能需要进行预处理，如亮度温度转换、辐射定标等，需要了解可能的预处理步骤。

12. **数据用途**：理解数据集适用的研究领域和应用，以便确定是否适合您的需求。

13. **数据更新频率**：了解数据集的更新频率，以便您选择适合时间分析的数据。

14. **数据许可和使用限制**：了解数据集的使用许可和任何限制，确保您的使用是符合法律和规定的。

15. **示例代码和用法**：查找使用该数据集的示例代码，以便您了解如何加载、处理和可视化数据。


## 二、六个常用的数据库
1. **Landsat 数据集**

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称 |	Landsat 数据集
数据类型	| 高分辨率卫星影像
数据内容	| 地表影像，可用于监测陆地变化、植被状况等
时间范围	| 1972 年至今
地理范围	| 全球范围
数据分辨率	| 通常为 30 米

2. **MODIS 数据集**

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| MODIS 数据集
数据类型	| 多光谱遥感数据
数据内容	| 气象观测、陆地表面温度、植被指数等
时间范围	| 2000 年至今
地理范围	| 全球范围
数据分辨率	| 不同产品分辨率不同，如 250 米、500 米、1 公里等

3. **Sentinel 数据集**（哨兵）

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| Sentinel 数据集
数据类型	| 各种多光谱和雷达数据
数据内容	| 地表影像、地形数据、海洋数据等
时间范围	| 根据不同卫星不同，覆盖多个年份
地理范围	| 全球范围
数据分辨率	| 不同传感器具有不同的分辨率，如 10 米到 60 米

4. **SRTM DEM 数据集**

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| SRTM 数字高程模型
数据类型	| 地表高程数据
数据内容	| 数字高程模型，用于地形分析、洪水模拟等
时间范围	| 单次测绘数据，如 SRTM1（2000 年）和 SRTM3（2004 年）
地理范围	| 全球范围
数据分辨率	| SRTM1 为 30 米，SRTM3 为 90 米

5. **Global Land Cover 数据集**（全球土地覆盖数据集）

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| 全球土地覆盖数据集
数据类型	| 土地覆盖分类数据
数据内容	| 土地利用、覆盖分类数据，用于分析土地变化等
时间范围	| 根据版本不同，覆盖不同的年份
地理范围	| 全球范围
数据分辨率	| 根据数据源和版本不同，分辨率也不同

6. **WorldPop 人口数据集**

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| WorldPop 人口数据集
数据类型	| 人口分布和人口密度数据
数据内容	| 全球范围内的人口分布信息，用于人口统计等
时间范围	| 根据数据源不同，覆盖不同的年份
地理范围	| 全球范围
数据分辨率	| 通常为 100 米到 1 公里


## 三、数据库示例
1. **Landsat 数据集**[（Landsat 9 OLI-2/TIRS-2）](https://developers.google.com/earth-engine/datasets/catalog/landsat-9)

| 数据库名称 |	内容 | 图像 |
|  ----  | ----  | --- |
地表反射率（Surface Reflectance） |	在这个数据库中，数据已经经过大气校正，以便更准确地表示地表的反射率。这意味着通过排除大气干扰，您可以获得更精确的地表信息。Tier 1提供了最高质量的数据，Tier 2则相对较低。| ![2023-08-29-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1467249b-9753-4a0f-832d-839e223ca4cc) |
大气顶部（Top of Atmosphere）| 这个数据库提供了校准后的大气顶部反射率数据。虽然没有进行大气校正，但这些数据仍然是原始数据的有用转换。Tier 1和Tier 2同样表示数据质量的级别，Tier 1的质量更高。| ![2023-08-29-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/9d594cb5-3c15-4762-a841-b448d60997a7) |
原始影像（Raw Images）	| 这个数据库包含原始的传感器辐射亮度（DN值）数据，这些数据可以用来进行各种类型的分析。这些数据没有进行校正，但可以通过一系列处理步骤来转换为更有用的数据。同样，Tier 1和Tier 2代表了数据的质量级别。| ![2023-08-29-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/ac614b7a-9a80-48c1-b56c-08b798ca0e38) |

2. [**MODIS 数据集**](https://developers.google.com/earth-engine/datasets/catalog/modis)

| 数据库名称 |	内容 | 图像 |
|  ----  | ----  | --- |
MOD13Q1.061 Terra 植被指数 16 天全球 250m |	这个数据集提供了植被指数（如归一化植被指数 NDVI 和增强植被指数 EVI），广泛用于监测植被覆盖和生长的变化，以及环境状况评估。 | ![2023-08-29-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/7e7632c9-1792-4843-b1fc-c6eb6e587feb) |
MOD11A1.061 Terra 陆地表面温度和发射率每日全球 1km | 这个数据集用于测量地表温度和发射率，对于研究地表能量平衡、城市热岛效应、气象变化等非常有用。 | ![2023-08-29-05](https://github.com/ZYJ-Group/Tanghy/assets/94824386/9f8a4fe7-9619-4728-a435-8a22223253b0) |
MCD43A4.061 MODIS 天底 BRDF 调整反射率 每日 500m | 经过调整的地表反射率数据，可以用来研究地表反射率特性、土地覆盖变化等。 | ![2023-08-29-06](https://github.com/ZYJ-Group/Tanghy/assets/94824386/4b3d23d3-bddd-4b9a-90c0-909200b2d0b8) |
MOD10A1.061 Terra Snow Cover 每日全球 500m | 用于监测积雪分布、融化和覆盖变化，对于高山地区、季节性变化研究等有重要作用。 | ![2023-08-29-07](https://github.com/ZYJ-Group/Tanghy/assets/94824386/4a1b97c8-55d2-4aa7-b2b5-798b37d306f0) |
MCD15A3H.061 MODIS 叶面积指数/FPAR 4 天全球 500m | 这这个数据集提供了叶面积指数（LAI）和光合有效辐射（FPAR）数据，对于植被生长监测和生态系统研究非常有用。 | ![2023-08-29-08](https://github.com/ZYJ-Group/Tanghy/assets/94824386/4f2300ad-ad8e-447b-ad48-832b1bf24846) |
MCD12Q1.061 MODIS 土地覆盖类型 年 全球 500m | 提供了年度土地覆盖分类数据，对于研究土地利用变化、生态系统分析等非常有用。 | ![2023-08-29-09](https://github.com/ZYJ-Group/Tanghy/assets/94824386/55302291-b22c-4417-acb8-4371af9abb56) |


3. **Sentinel 数据集**（哨兵）

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| Sentinel 数据集
数据类型	| 各种多光谱和雷达数据
数据内容	| 地表影像、地形数据、海洋数据等
时间范围	| 根据不同卫星不同，覆盖多个年份
地理范围	| 全球范围
数据分辨率	| 不同传感器具有不同的分辨率，如 10 米到 60 米

4. **SRTM DEM 数据集**

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| SRTM 数字高程模型
数据类型	| 地表高程数据
数据内容	| 数字高程模型，用于地形分析、洪水模拟等
时间范围	| 单次测绘数据，如 SRTM1（2000 年）和 SRTM3（2004 年）
地理范围	| 全球范围
数据分辨率	| SRTM1 为 30 米，SRTM3 为 90 米

5. **Global Land Cover 数据集**（全球土地覆盖数据集）

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| 全球土地覆盖数据集
数据类型	| 土地覆盖分类数据
数据内容	| 土地利用、覆盖分类数据，用于分析土地变化等
时间范围	| 根据版本不同，覆盖不同的年份
地理范围	| 全球范围
数据分辨率	| 根据数据源和版本不同，分辨率也不同

6. **WorldPop 人口数据集**

| 关键信息 |	内容 |
|  ----  | ----  |
数据库名称	| WorldPop 人口数据集
数据类型	| 人口分布和人口密度数据
数据内容	| 全球范围内的人口分布信息，用于人口统计等
时间范围	| 根据数据源不同，覆盖不同的年份
地理范围	| 全球范围
数据分辨率	| 通常为 100 米到 1 公里