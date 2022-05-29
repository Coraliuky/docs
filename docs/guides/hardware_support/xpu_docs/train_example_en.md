# Demo of Training on the Paddle KUNLUN XPU Version

It is no much difference using XPU or CPU/GPU for training. It can mean that the training is executed on the KUNLUN device if there is a line "-o use_xpu=True" added.

#### Donwload ResNet50 and run the demo：

The command of downloading model files: 

```
cd path_to_clone_PaddleClas
git clone -b release/static https://github.com/PaddlePaddle/PaddleClas.git
```
You can access [github repo](https://github.com/PaddlePaddle/PaddleClas/tree/release/static) of PaddleClas and download the source code.

The command of configuring XPU for training is very simple: 
```
#FLAGS can designate single-card or multi-card training. The demo is the 2-card training:
export FLAGS_selected_xpus=0,1
#Start the training
python3.7 tools/static/train.py -c configs/quick_start/ResNet50_vd_finetune_kunlun.yaml -o use_gpu=False -o use_xpu=True -o is_distributed=False
```

If you want to designate more cards (such as eight cards)，you need to configure appropriate training parameters and can use the following command for automatic modification: 
```
export FLAGS_selected_xpus=0,1,2,3,4,5,6,7
python3.7 -m paddle.distributed.launch \
        --ips=${ips} \
        --xpus=${FLAGS_selected_xpus} \
        --log_dir log \
        tools/static/train.py \
        -c ${config_yaml} \
        -o is_distributed=False \
        -o epochs=${epochs} \
        -o TRAIN.batch_size=${total_batch_size} \
        -o LEARNING_RATE.params.lr=${lr} \
        -o use_gpu=False \
        -o use_xpu=True
```

For training demos of other models, you can refer to model links in the supported model table in [Support for the KUNLUN XPU offered by PaddlePaddle](https://www.paddlepaddle.org.cn/documentation/docs/zh/guides/xpu_docs/paddle_2.0_xpu_cn.html).
