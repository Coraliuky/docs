Training Demo of the Paddle KUNLUN XPU Version

There is no much difference using the XPU and CPU/GPU for training. It means that the training is performed on the KUNLUN chips if you add the line "-o use_xpu=True".

#### Demo of Downloading and Running ResNet50：

The command of downloading model files: 

```
cd path_to_clone_PaddleClas
git clone -b release/static https://github.com/PaddlePaddle/PaddleClas.git
```
You can also download the source code by accessing [github repo](https://github.com/PaddlePaddle/PaddleClas/tree/release/static) of PaddleClas.

The command of configuring the XPU for training is very simple: 
```
#FLAGS designate the training to be single-card or multi-card. In this demo, it is a two-card training
export FLAGS_selected_xpus=0,1
#Start the training
python3.7 tools/static/train.py -c configs/quick_start/ResNet50_vd_finetune_kunlun.yaml -o use_gpu=False -o use_xpu=True -o is_distributed=False
```

If you want to designate more cards (sucha eight cards), you need to configure proper trianing parameters and you can run the following command for automatic modification: 
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

Training demos of other models can be found in the models links of the supported model table in the document [Supports for KUNLUN XPU Chips offered by PaddlePaddle](https://www.paddlepaddle.org.cn/documentation/docs/zh/guides/xpu_docs/paddle_2.0_xpu_cn.html).
