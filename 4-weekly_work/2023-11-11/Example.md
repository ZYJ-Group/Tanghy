# PaddleDetection

## 30分钟快速上手PaddleDetection  
[链接](https://gitee.com/paddlepaddle/PaddleDetection/blob/release/2.6/docs/tutorials/GETTING_STARTED_cn.md)


1. **安装**  
关于安装配置运行环境，请参考[安装指南](INSTALL_cn.md)
在本演示案例中，假定用户将PaddleDetection的代码克隆并放置在`/home/paddle`目录中。用户执行的命令操作均在`/home/paddle/PaddleDetection`目录下完成

2. **准备数据**  
数据集参考Kaggle数据集 ，包含877张图像，数据类别4类：crosswalk，speedlimit，stop，trafficlight。 将数据划分为训练集701张图和测试集176张图，下载链接.
 ```bash
python dataset/roadsign_voc/download_roadsign_voc.py
```
下载后的数据格式为
```
  ├── download_roadsign_voc.py
  ├── annotations
  │   ├── road0.xml
  │   ├── road1.xml
  │   |   ...
  ├── images
  │   ├── road0.png
  │   ├── road1.png
  │   |   ...
  ├── label_list.txt
  ├── train.txt
  ├── valid.txt
```

3. **配置文件改动和说明**  
<img width="1384" alt="2023-11-12-04" src="https://github.com/ZYJ-Group/Tanghy/assets/94824386/1a445485-370c-4ef2-8bd5-afe12139575c">   

4. **训练（GPU单卡训练）**  
```
python tools/train.py -c configs/yolov3/yolov3_mobilenet_v1_roadsign.yml  
```
5. **评估**  
默认将训练生成的模型保存在当前`output`文件夹下  
```
python tools/eval.py -c configs/yolov3/yolov3_mobilenet_v1_roadsign.yml -o weights=https://paddledet.bj.bcebos.com/models/yolov3_mobilenet_v1_roadsign.pdparams
```  
7. **预测**  
```
python tools/infer.py -c configs/yolov3/yolov3_mobilenet_v1_roadsign.yml --infer_img=demo/000000570688.jpg -o weights=https://paddledet.bj.bcebos.com/models/yolov3_mobilenet_v1_roadsign.pdparams
```  
![road554](https://github.com/ZYJ-Group/Tanghy/assets/94824386/3c90a109-2f54-46cc-8d3c-9d2bcaa458a2)

9. **训练可视化**  
当打开`use_vdl`开关后，为了方便用户实时查看训练过程中状态，PaddleDetection集成了VisualDL可视化工具，当打开`use_vdl`开关后，记录的数据包括：
1 loss变化趋势
2 mAP变化趋势

```bash
python tools/train.py -c configs/yolov3/yolov3_mobilenet_v1_roadsign.yml
                        --use_vdl=true \
                        --vdl_log_dir=vdl_dir/scalar \
```

使用如下命令启动VisualDL查看日志
```shell
# 下述命令会在127.0.0.1上启动一个服务，支持通过前端web页面查看，可以通过--host这个参数指定实际ip地址
visualdl --logdir vdl_dir/scalar/
```
![loss](https://github.com/ZYJ-Group/Tanghy/assets/94824386/cc45bacf-6e62-4eb4-a2bd-a1b8cf3943d4)

8. **模型导出**  
```
python tools/export_model.py -c configs/yolov3/yolov3_mobilenet_v1_roadsign.yml --output_dir=./inference_model -o weights=output/yolov3_mobilenet_v1_roadsign/best_model
```
10. **模型压缩**  
* 裁剪
* 量化
* 蒸馏
* 联合策略
10. **预测部署**  
