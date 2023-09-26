# 月总结（2023-08 && 2023-09）
- [**北京洪水变化时序分析**](#北京洪水变化时序分析)
  - [注册](#注册)
  - [代码_简易](#代码_简易)
  - [代码_最终](#代码_最终)
  - [结果图](#结果图)
- [**GEE本地化**](#GEE本地化)
  - [Nodejs与GEE集成](#Nodejs与GEE集成)
  - [任务要求](#任务要求)
  - [遇到的问题](#遇到的问题)
  - [结果图](#结果图)
  - [GEEmap](#GEEmap)
  - [结果图](#结果图)
  - [python和GEE的集成](#python和GEE的集成)
  - [结果图](#结果图)
- [**UNet复现**](#UNet复现)
  - [pytorch的安装和配置](#pytorch的安装和配置)
  - [准备工作](#准备工作)
  - [模型下载和测试](#模型下载和测试)
  - [结果图](#结果图)
- [**计划安排**](#计划安排)
  - [注册](#注册)
  - [注册](#注册)


### 北京洪水变化时序分析
#### 注册  
1. 注册Google账号。  
2. 注册GEE账号。  
3. 登录GEE Code Editor  
参考网站：[链接](https://zhuanlan.zhihu.com/p/426365317)  

#### [代码_简易](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-08-14/Code)  
1. 区域范围  
```javascript
var roiCoordinates = [
  [112.65931859449563, 37.74922317697311],
  [120.63539281324563, 37.74922317697311],
  [120.63539281324563, 42.15954015334511],
  [112.65931859449563, 42.15954015334511],
  [112.65931859449563, 37.74922317697311]
];
var roiPolygon = ee.Geometry.Polygon(roiCoordinates);
```
2. 日期范围  
```javascript
var dateList = ['2023-08-01', '2023-08-02', '2023-08-03', '2023-08-04', '2023-08-05', '2023-08-06', '2023-08-07', '2023-08-08'];
```
3. 导出图像  
```javascript
  var collection = ee.ImageCollection('COPERNICUS/S5P/NRTI/L3_CLOUD')
    .select('cloud_fraction')
    .filterDate(currentDate, currentDate.advance(1, 'day'))
    .filterBounds(roiPolygon);
```
4. 图像可视化  
```javascript
  var band_viz = {
    min: 0,
    max: 0.95,
    palette: ['black', 'blue', 'purple', 'cyan', 'green', 'yellow', 'red']
  };
```
5. 计算平均值像素  
```javascript
  var meanImage = collection.mean();

  var visualization = meanImage.visualize(band_viz);
```

#### [代码_最终](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-08-21/%E6%B4%AA%E6%B0%B4%E5%89%8D%E5%90%8E.txt)  
1. 几何形状和时间范围设置：
   - 代码开始通过地理坐标定义了研究区域的多边形几何形状。
   - 它使用变量`before_start`、`before_end`、`after_start`和`after_end`指定了“洪水前”和“洪水后”的影像日期范围。
```javascript
var geometry = 
    /* color: #d63000 */
    /* displayProperties: [
      {
        "type": "rectangle"
      }
    ] */
    ee.Geometry.Polygon(
        [[[116.0313889986048, 40.08473253369342],
          [116.0313889986048, 39.71810936483123],
          [116.7235276704798, 39.71810936483123],
          [116.7235276704798, 40.08473253369342]]], null, false);

var before_start= '2023-06-01';
var before_end='2023-07-9';
 
// 洪水发生后的影像时间段
var after_start='2023-07-10';
var after_end='2023-08-13';
```
2. SAR影像集筛选：
   - 代码根据多个条件对Sentinel-1影像集进行了筛选：仪器模式、极化方式、通过方向（上行）、分辨率和地理范围。
   - 它选择了特定的极化方式（VH或VV），并相应地对影像集进行了筛选。
```javascript
// Sentinel - 1 SAR极化方式设置, 这里选用 VH ，也可以使用 VV
var polarization = "VH";
 
// 设置轨道方式，有上轨道和下轨道，根据研究区的数据有无选择
// 这里选择ASCENDING, 在有数据的情况下也可选择DESCENDING
var pass_direction = "ASCENDING"; // ASCENDING
 
// 设置变化的阈值，由于基本原理是利用SAR数据在洪水变化前后的差异，因此
// 要得到洪水的范围需要设置阈值j进行分割，这里选择 1.25， 也可以自己设置
var difference_threshold = 1.25;


// 选择研究区，可以手动画矢量范围，也可以使用资产中的研究去边界
// 为方便运行，这里以代码的形式展现, 范围如下图所示

var aoi = ee.FeatureCollection(geometry);
 
// 选择SAR影像
var collection= ee.ImageCollection('COPERNICUS/S1_GRD')
  .filter(ee.Filter.eq('instrumentMode','IW'))
  .filter(ee.Filter.listContains('transmitterReceiverPolarisation', polarization))
  .filter(ee.Filter.eq('orbitProperties_pass',pass_direction)) 
  .filter(ee.Filter.eq('resolution_meters',10))
  .filterBounds(aoi)
  .select(polarization);
```
3. 筛选洪水前后的影像：
   - 代码通过使用之前定义的日期范围，对影像集进行筛选，以获取洪水前后的SAR影像。
   - 它将筛选后的影像集的大小打印到控制台。
```javascript
 // 筛选洪水前后的SAR数据
 // 洪水发生前
var before_collection = collection.filterDate(before_start, before_end);
print(before_collection.size())
// 洪水发生后
var after_collection = collection.filterDate(after_start,after_end);
print(after_collection.size())
// 获取 after_collection 中的图像数量
var afterImageCount = after_collection.size().getInfo();
```
4. 导出洪水后的影像：
   - 代码遍历洪水后的影像集，并将每个影像分别导出到Google Drive。
   - 它为每个影像构建名称，并指定导出参数，如影像、描述、文件夹、分辨率和区域。
```javascript
// 循环保存每个图像
for (var i = 0; i < afterImageCount; i++) {
  var image = ee.Image(after_collection.toList(afterImageCount).get(i));
  var imageIndex = (i + 1).toString();
  var paddedIndex = imageIndex.length < 2 ? '0' + imageIndex : imageIndex; // 补零，如 01、02
  var imageId = "After_" + paddedIndex; // 生成图像名称，如 after_01、after_02

  // 定义导出任务的参数
  var exportParams = {
    image: image,
    description:imageId,
    folder: 'Your_Google_Drive_Folder_Name', // 替换为你的Google Drive文件夹名
    fileNamePrefix: imageId,
    scale: 10, // 设置导出的分辨率
    region: aoi.geometry() // 设置导出的区域
  };
  
  // 启动导出任务
  Export.image.toDrive(exportParams);
```
5. 影像镶嵌和平滑处理：
   - 代码对洪水前后的影像集进行镶嵌，并将其剪裁为研究区域。
   - 它使用`focal_mean`函数和指定的平滑半径对两个影像应用了均值滤波，以减少噪声。
```javascript
// 对筛选的数据进行镶嵌和裁减
var before = before_collection.mosaic().clip(aoi);
var after = after_collection.mosaic().clip(aoi);
 
// 对数据进行滤波
// 设置滤波半径
var smoothing_radius = 50;
// 应用滤波
var before_filtered = before.focal_mean(smoothing_radius, 'circle', 'meters');
var after_filtered = after.focal_mean(smoothing_radius, 'circle', 'meters');
 
// 显示影像
Map.centerObject(aoi,8);
Map.addLayer(before_filtered, {min:-25,max:0}, 'Before Flood',0);
Map.addLayer(after_filtered, {min:-25,max:0}, 'After Flood',1);

```
6. 计算影像差异和阈值处理：
   - 代码计算了洪水后影像相对于洪水前影像的强度比（差异）。
   - 它应用阈值来创建二进制洪水范围掩膜。
   - 进一步通过应用像素连接分析来细化掩膜，以去除孤立像素。
```javascript
// 利用洪水发生时的影像减去洪水发生前的影像
var difference = after_filtered.divide(before_filtered);
 
// 应用预定义的差分阈值并创建泛滥范围掩膜
var threshold = difference_threshold;
var difference_binary = difference.gt(threshold);
var difference_binary = difference_binary.updateMask(difference_binary.eq(1))
// 计算像素的连通性，以消除那些连接到8个或更少邻居的像素
// 这一操作降低了洪水范围的噪音(椒盐现象-小碎点)
var connections = difference_binary.connectedPixelCount()//.reproject(difference.projection(), null, 10);    
var flooded = difference_binary.updateMask(connections.gte(8));
```
7. 根据坡度过滤淹没区域：
   - 代码计算了数字高程模型（DEM）的坡度，并使用它来过滤掉坡度大于5度的淹没区域。
```javascript
//  去除上述洪水淹没范围中坡度大于5度的区域
// 计算坡度
var DEM = ee.Image('WWF/HydroSHEDS/03VFDEM');
var terrain = ee.Algorithms.Terrain(DEM);
var slope = terrain.select('slope');
 
// 最终的洪水淹没范围
var flooded = flooded.updateMask(slope.lt(5));
Map.addLayer(flooded,{palette:"0000FF"},'Flooded areas');
```
8. 计算淹没面积：
   - 代码通过将二进制掩膜与像元面积相乘，并对结果进行求和，计算出淹没的面积。
   - 最后，将计算结果从平方米转换为公顷。
```javascript
// 计算洪水面积
// 将每个像素转化为像元面积
var flood_pixelarea = flooded.select(polarization)
                            .multiply(ee.Image.pixelArea());
 
// 统计所有像元的和，默认的面积是 ㎡
var flood_stats = flood_pixelarea.reduceRegion({
  reducer: ee.Reducer.sum(),              
  geometry: aoi,
  scale: 10, 
  bestEffort: true // 为true时可以减少计算时间
  });
  
// 将 平方米转化为 公顷
var flood_area_ha = flood_stats
  .getNumber(polarization)
  .divide(10000)
  .round();// 四舍五入
  
  // 显示淹没范围面积结果
  print('area/ha', flood_area_ha);
```
9. 导出结果：
   - 代码以栅格（TIFF）格式导出二进制洪水范围掩膜。
   - 还使用`reduceToVectors`将二进制掩膜转换为矢量格式（多边形），并以形状文件（SHP）格式导出。
```javascript
  // 导出栅格格式 tif
Export.image.toDrive({
  image: flooded, 
  description: 'Flood_extent_raster',
  fileNamePrefix: 'flooded',
  region: aoi, 
  maxPixels: 1e10
});
 
// 导出shp格式
// 栅格转矢量
var flooded_vec = flooded.reduceToVectors({
  scale: 10,
  geometryType:'polygon',
  geometry: aoi,
  eightConnected: false,
  bestEffort:true,
  tileScale:2,
});
 
// 导出shp结果
Export.table.toDrive({
  collection:flooded_vec,
  description:'Flood_extent_vector',
  fileFormat:'SHP',
  fileNamePrefix:'flooded_vec'
```

#### 结果图
- 北京市区地形图
![Beijing](https://github.com/Axianlatiao/Test/assets/94824386/bac01b2e-b732-488b-84ca-9a3767fd50cd)

- 北京洪水前图像
![Before_flood](https://github.com/Axianlatiao/Test/assets/94824386/b682ca8e-6ea9-4d04-ad7d-1ddc82dc83a5)

- 北京洪水后图像
![After_flood](https://github.com/Axianlatiao/Test/assets/94824386/76d362f2-d39d-43e0-b36c-872b18f19727)

- 可能的洪水影响区域
![Area_flood](https://github.com/Axianlatiao/Test/assets/94824386/1d9c13c5-0769-4cde-8f51-e1c8e43830fc)

### GEE本地化
#### Nodejs与GEE集成
1. 安装Node.js环境。  
2. 安装与GEE的API集成的Node.js库，'@google/earthengine'。  
3. 认证。使用GEE提供的认证机制，此处使用服务账号方式。  
4. 初始化GEE，提供认证凭据。  
5. 使用GEE API。  
参考网站：[链接](https://developers.google.com/earth-engine/guides/npm_install)  
#### 任务要求
1. 数据库要求，至少满足一个SAR图像，一个RGB图像。
2. 传入数据格式如图所示。
![2023-09-06-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/18b1f86b-3718-47b9-b04f-95bed7bd5b69)
3. RGB图像需要至少加载B2、B3和B4的波段，SAR图像需要至少加载VV和VH的波段。
4. 要将图像保存到本地。
#### 遇到的问题
1. 生成图像一团黑或者一团白。
解决办法：minPixelValue和maxPixelValue的值不对，  查询像素值范围：[代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-07/2023-09-07-02.txt)  
2. 默认保存为zip格式。
解决办法：加入format下载的文件格式。
```
      const url = rgbImage.getDownloadURL({
        name: 'RGB_Image', // 更新导出文件名为 'RGB_Image'
        scale: scale,
        crs: crs, // 使用获取的CRS
        region: region,
        format: 'GeoTIFF', // 下载的文件格式
      });
```
3. 导出图片的时间过长。
4. 过大范围无法导出。
且尚无办法解决问题3和4。

#### 结果图
数据库 | 波段 | 现在的代码 | 现在的时间 |现在的图像
--- | --- | --- | --- | --- 
COPERNICUS/S2_HARMONIZED | 'B4', 'B3', 'B2' | [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-17/2023-09-17-03.txt) | 70.442 seconds | ![2023-09-17-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/2662bf9e-ee1a-4391-ac1f-ffdf839c536a)  
COPERNICUS/S1_GRD | 'VV', 'VH' | [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-17/2023-09-17-04.txt) | 60.905 seconds | ![2023-09-17-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/49e424c3-864b-4628-b540-1422a6ba6fe0)  

#### GEEmap
1. [安装GEEmap](https://github.com/ZYJ-Group/Tanghy/edit/main/4-weekly_work/2023-09-20/Example.md)    
2. [登录账号](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-21/Example.md)  

#### 结果图
1. [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-23/%E6%96%B0%E5%BB%BA%20%E6%96%87%E6%9C%AC%E6%96%87%E6%A1%A3%20(5).txt)    
结果图：  
![2023-09-23-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/a999acfe-54ae-4f67-abe1-3e4ce17dde7c)  

2. [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-23/%E6%96%B0%E5%BB%BA%20%E6%96%87%E6%9C%AC%E6%96%87%E6%A1%A3%20(5).txt)     
结果图：  
![2023-09-23-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/e92e1fa1-acb6-46c4-83ed-2740a0f99f0d)  

#### python和GEE的集成
1. 配置 python API：
- 安装gcloud CLI [网站](https://cloud.google.com/sdk/docs/install?hl=zh-cn)  
- 遇到网络问题，无法正常认证。  
2. 解决办法：
[链接](https://zhuanlan.zhihu.com/p/259377035)
3. 解决重复验证
![2023-09-24-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/e1b98ad5-8aef-4cee-8e9a-b67231a93e76)  
参考网站：[geemap代码](https://book.geemap.org/chapters/06_data_analysis.html)  
[python API](https://developers.google.com/earth-engine/tutorials/community/intro-to-python-api)

#### 结果图
1. [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-24/%E6%96%B0%E5%BB%BA%20%E6%96%87%E6%9C%AC%E6%96%87%E6%A1%A3%20(2).txt)  
结果图：
![2023-09-24-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/de805320-ef1a-4730-aea3-244d99f41019)  

2. [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-24/%E6%96%B0%E5%BB%BA%20%E6%96%87%E6%9C%AC%E6%96%87%E6%A1%A3%20(3).txt)  
结果图：
![2023-09-24-03](https://github.com/ZYJ-Group/Tanghy/assets/94824386/5107ec87-2a74-4433-8858-7f1c2da62fa9)  

3. [代码](https://github.com/ZYJ-Group/Tanghy/blob/main/4-weekly_work/2023-09-24/%E6%96%B0%E5%BB%BA%20%E6%96%87%E6%9C%AC%E6%96%87%E6%A1%A3%20(4).txt)  
结果图：
![2023-09-24-04](https://github.com/ZYJ-Group/Tanghy/assets/94824386/aea52715-81cd-4fe9-92b4-3eb8daf09c74)  
![2023-09-24-05](https://github.com/ZYJ-Group/Tanghy/assets/94824386/933625ba-cf73-4e43-b584-0556b5cc46f3)  

### UNet复现
#### pytorch的安装和配置
1. 安装anaconda
2. 在anaconda配置一个pytorch虚拟环境
3. 在pytorch虚拟环境中安装相关的库。（AMD显卡使用CPU版本）
4. 安装pycharm
5. 在pycharm中使用conda（pytorch环境）的编译器。

主要参考视频：[链接](https://www.bilibili.com/video/BV1S5411X7FY/?spm_id_from=333.999.0.0&vd_source=6714df959b40fdf22d5fa47201de3d2c)  

#### 准备工作
1. pycharm安装  
2. mobaXterm安装  
3. 连接服务器  
编辑配置    
![2023-09-18-01](https://github.com/ZYJ-Group/Tanghy/assets/94824386/32a20fa1-94d5-4d43-a04c-082230a3ce19)  
配置路径映射    
![2023-09-18-02](https://github.com/ZYJ-Group/Tanghy/assets/94824386/b6d76c23-1a9f-40d6-a20d-9091ab2e8f7e)   
4. github找到示例代码  

#### 模型下载和测试
1. 注册wandb。
2. 服务器连接网络。
3. 从kaggle上下载数据集。

#### 结果图
1. wandb云端数据结果  
![2023-09-19-11](https://github.com/ZYJ-Group/Tanghy/assets/94824386/18095f1b-ce14-4cad-a4ba-dadc3c67e90b)  
2. predict结果  
![2023-09-19-10](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1fbc2e7e-df03-4345-bfa9-39c8ba72d697)  

### 计划安排
