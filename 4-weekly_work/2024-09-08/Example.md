# 8.20汇报

## 采集数据集
使用Google Earth Engine (GEE) 系统地采集并处理了浙江省杭州至舟山11个城市在2020年3月1日至5月31日间的光学与合成孔径雷达（SAR）图像。具体来说，针对每个城市的中心坐标，定义了2560米（约0.0231度）的缓冲区作为研究范围。采集数据包括Sentinel-2卫星的B4（红色）、B3（绿色）、B2（蓝色）光学波段，用于生成真彩色图像，以及Sentinel-1卫星的VV与VH波段，主要用于分析地表散射特性。最终，每张图像以256x256像素的分辨率输出并保存。  
![image](https://github.com/user-attachments/assets/65ea33ce-629f-47ea-86e1-00ee84d71130)  

目前部分数据集跑出的结果图  
![image](https://github.com/user-attachments/assets/b8ccdfc1-3107-46e7-b2b7-b052993851db)  


## 修改代码
主要调试新的去云的数据集的对应代码以及针对土地利用分类研究数据集(whu-opt-sar)进行熟悉和代码修改。

