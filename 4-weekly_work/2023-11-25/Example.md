# open-cd
[链接](https://github.com/likyoo/open-cd)https://github.com/likyoo/open-cd

# 安装
#### simple usage
```
# Install OpenMMLab Toolkits as Python packages
pip install -U openmim
mim install mmengine
mim install "mmcv>=2.0.0"
mim install "mmpretrain>=1.0.0rc7"
pip install "mmsegmentation>=1.0.0"
pip install "mmdet>=3.0.0"
```
```
git clone https://github.com/likyoo/open-cd.git
cd open-cd
pip install -v -e .
```
train
```
python tools/train.py configs/changer/changer_ex_r18_512x512_40k_levircd.py --work-dir ./changer_r18_levir_workdir
```
infer
```
# get .png results
python tools/test.py configs/changer/changer_ex_r18_512x512_40k_levircd.py  changer_r18_levir_workdir/latest.pth --show-dir tmp_infer
# get metrics
python tools/test.py configs/changer/changer_ex_r18_512x512_40k_levircd.py  changer_r18_levir_workdir/latest.pth
```

### 修改mmcv版本问题
在'../open-cd-main/opencd/__init__.py'中，把
```python
# mmcv_minimum_version = '2.0.0rc4'
# mmcv_maximum_version = '2.1.0'
# 改成
mmcv_minimum_version = '2.0.0rc4'
mmcv_maximum_version = '2.1.1'
```
从而使用前面自动安装的mmcv==2.1.0版本

### 修改数据集位置
例：
```
python tools/train.py configs/changer/changer_ex_r18_512x512_40k_levircd.py --work-dir ./changer_r18_levir_workdir
```
从configs/changer/changer_ex_r18_512x512_40k_levircd.py
```python
_base_ = [
    '../_base_/models/changer_mit-b0.py', 
    '../common/standard_512x512_40k_levircd.py']
```
发现继承于'../common/standard_512x512_40k_levircd.py'
同理，从继承的文件中找到
```python
dataset_type = 'LEVIR_CD_Dataset'
data_root = '/home/wyc/Thy/Datasets/LEVIR'
```
从而修改data_root数据路径。

### 遇到不明错误
类似于
```
libpng error: IDAT: CRC error

AssertionError: The images in `img_path from` and `img_path to` are not one-to-one correspondence
```
考虑是数据集存在问题，或者代码与数据集不匹配

