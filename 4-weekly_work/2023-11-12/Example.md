# MMDetection
[链接](https://github.com/open-mmlab/mmdetection)

## 安装
[链接](https://mmdetection.readthedocs.io/zh-cn/latest/get_started.html)

1. **环境**
```
# 创建并激活一个 conda 环境
conda create --name openmmlab python=3.8 -y
conda activate openmmlab

# 在GPU平台上安装pytorch
conda install pytorch torchvision -c pytorch
```

2. **安装MMDetection**
```
# 步骤 0. 使用 MIM 安装 MMEngine 和 MMCV。
pip install -U openmim
mim install mmengine
mim install "mmcv>=2.0.0"

# 步骤 1. 安装 MMDetection。
方案 a：如果你开发并直接运行 mmdet，从源码安装它：
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -v -e .
# "-v" 指详细说明，或更多的输出
# "-e" 表示在可编辑模式下安装项目，因此对代码所做的任何本地修改都会生效，从而无需重新安装。
```
```
# 验证安装
# 步骤 1. 我们需要下载配置文件和模型权重文件。
mim download mmdet --config rtmdet_tiny_8xb32-300e_coco --dest .
# 步骤 2. 推理验证。
方案 a：如果你通过源码安装的 MMDetection，那么直接运行以下命令进行验证：
python demo/image_demo.py demo/demo.jpg rtmdet_tiny_8xb32-300e_coco.py --weights rtmdet_tiny_8xb32-300e_coco_20220902_112414-78e30dcc.pth --device cpu
``` 
