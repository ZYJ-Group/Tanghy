# Uncrtains--去云模型复写

## Dataload and Model definition

### 文件格式
- data
  - dataLoader.py
- model
  - src
    - backbones
      - base_model.py
      - uncrtaints.py
      - utae.py
    - learning
      - metrics.py
      - weight_init.py
    - losses.py
    - model_utils.py
    - utils.py
  - parse_args.py
  - test.py
  - train.py
- util
  - pytorch_ssim
    - __init__.py
  - detect_cloudshadow.py
 
### 按流程梳理
  以train.py文件的main文件为主流程进行梳理

main(config):
  config---parse_args.py/
  dataload---dataLoader.py,SEN12MSCR/seed_worker,generator/
  model definition---model_utils.py,get_model,get_generator/base_model.py/losses.py,get_losses
                                                          /uncrtaints.py
                                                          
