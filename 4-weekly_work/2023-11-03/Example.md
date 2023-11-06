# BIT Reproduction

## Reference Link
[github repos](https://github.com/justchenhao/BIT_CD)  
[csdn](https://blog.csdn.net/persist_ence/article/details/129687895?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169917089616777224410813%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=169917089616777224410813&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-129687895-null-null.142^v96^control&utm_term=BIT%E5%A4%8D%E7%8E%B0&spm=1018.2226.3001.4187)  

## Quick Start
``` python
python demo.py
```
We can find the prediction results in `samples/predict`.

## Data Preparation
### Data Download 
LEVIR-CD: [link](https://justchenhao.github.io/LEVIR/  )  
WHU-CD: [link](https://study.rsgis.whu.edu.cn/pages/download/building_dataset.html  )  
DSIFN-CD: [link](https://github.com/GeoZcx/A-deeply-supervised-image-fusion-network-for-change-detection-in-remote-sensing-images/tree/master/dataset  )  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/b8f0653b-b4d2-4cc4-8415-6ecfcf3396bb)    

### Data structure
```
"""
Change detection data set with pixel-level binary labels；
├─A
├─B
├─label
└─list
"""
```
`A`: images of t1 phase;  
`B`:images of t2 phase;  
`label`: label maps;  
`list`: contains `train.txt, val.txt and test.txt`, each file records the image names (XXX.png) in the change detection dataset.  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/a632a9f8-ec4a-4e34-aa75-a8f7df4a570a)
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/b36a7bf4-ece8-48e7-90fb-b5180dece9f3)  

To create the list, I utilized Python. The Python file is located at the provided link.
link

## Train
### `main_cd.py`
The file for training is `main_cd.py`, ang we need to modify certain parameters for the training process. Here are some key parameters.
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/daeae00c-4571-43fa-a100-b98138a69033)    
`project_name`: it will generate a file in the root of checkpoint_root, containing the relative log file for each training session.(need to change for each projection)  
`checkpoint_root`: it will generate a file int the root of this directory.  
`dataset` and `data_name` : These represent the name of the datasets, which we don't alter here.  

### `data_config.py`
We need to make modifications in the 'data_config.py' file. Here, we only need to change the 'root_dir' to the path of our own dataset.
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/5d5b5bca-95f6-446e-81e5-cacaa1e79271)  

### `dateset`
We will encounter an error when running this code in our server, and the error is found in this code:
'from Dataset.CD_dataset import CDDataset'.
**Solution:**
Since `Dataset` has the same name as a library, we will change the file name.

### ModuleNotFoundError
We encounter another error as ModuleNotFoundError: No module named ‘torchvision.models.utils.
Due to our Torch version being higher(above 1.6), errors are occurring. The error statements need to be modified.
**Solution:**
Modified `from torchvision.models.utils import load_state_dict_from_url` to `from torch.hub import load_state_dict_from_url`

### `run_cd.sh`
We can find the training script run_cd.sh in the folder scripts. We can run the script file by sh scripts/run_cd.sh in the command environment.

## Pretection
We utilize the `demo.py` for predictions. Please note that it's crucial to input the same `checkpoint_root` and `projection_name` as used in the `train.py`.
For the `dataset` and `data_name`, we keep them unchanged.
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/991c2340-717d-48da-b0bd-32e4230e8d23)  

## RuntimeError
RuntimeError: Error(s) in loading state_dict for BASE_Transformer**  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/ef7e31da-9774-4a81-aab6-cf4fb8f95a02)    
Due to the disparity between the model utilized for prediction and the one employed during training:  
This is the model we utilized for prediction.  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/916b61d2-5060-4b14-8e0c-02e659216da4)  

This is the model we utilized for training.  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/89bdaeae-91af-4d66-8b67-f4c0e3fa3a24)  

Therefore, adjustments are necessary to align them and ensure consistency.
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/9bc9706c-b051-4f4b-b587-ba06eff194df)  
