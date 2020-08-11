# FedMD
FedMD: Heterogenous Federated Learning via Model Distillation. 
Preprint on https://arxiv.org/abs/1910.03581.

## Run scripts
Run the python script (in Colab). For instance 
``` 
python pretrain_CNN_on_public_dataset.py -conf conf/pretrain_MNIST_conf.json
python FEMNIST_Balanced.py
```

## 算法流程
![image-20200808190039493](https://i.loli.net/2020/08/08/bogR7OY2MX5DiPV.png)

### 初始化：
- 设置MNIST为公共数据集,在公共数据集上训练预定义的模型model_i,把各个模型保存到本地
- 设置EMNIST的一部分作为各个节点的私有数据集,每个工作节点选取同等规模的数据作为私有数据

### 通信多次:
- 各个节点的模型model_i在私有数据上训练,将acc和loss上传到central server
- server更新consensus(average)
- 各个节点根据最新的consensus在公共数据集再训练
- 各个节点再在私有数据上更新几个epoch
