# PaddleDetection

## 安装
[链接](https://gitee.com/paddlepaddle/PaddleDetection/blob/release/2.6/docs/tutorials/INSTALL_cn.md)  

1. **安装PaddlePaddle**
```
# CUDA10.2
python -m pip install paddlepaddle-gpu==2.3.2 -i https://mirror.baidu.com/pypi/simple
```
2. **安装PaddleDetection**
```
# 克隆PaddleDetection仓库
cd <path/to/clone/PaddleDetection>
git clone https://github.com/PaddlePaddle/PaddleDetection.git

# 安装其他依赖
cd PaddleDetection
pip install -r requirements.txt

# 编译安装paddledet
python setup.py install
```
安装后确认测试通过：
`python ppdet/modeling/tests/test_architectures.py`
测试通过后会提示如下信息：
```
.......
----------------------------------------------------------------------
Ran 7 tests in 12.816s
OK
```
3. **快速体验**
```
python tools/infer.py -c configs/ppyolo/ppyolo_r50vd_dcn_1x_coco.yml -o use_gpu=true weights=https://paddledet.bj.bcebos.com/models/ppyolo_r50vd_dcn_1x_coco.pdparams --infer_img=demo/000000014439.jpg

```

4. **结果图**  
![000000014439](https://github.com/ZYJ-Group/Tanghy/assets/94824386/b2c28758-744c-4307-bde3-c1eb16ca1dcc)  

