# Example of Training on the Paddle ROCm Version

There is no much differnce training with the Hygon CPU/DCU or with the Intel CPU/Nvidia GPU. The Paddle ROCm version can fully support APIs of the Paddle CUDA version, and you can use the same commands and parameters of the GPU training.

#### Example of Training ResNet50

**Step 1**：Download the code of ResNet50, and prepare the ImageNet1k dataset

```bash
cd path_to_clone_PaddleClas
git clone https://github.com/PaddlePaddle/PaddleClas.git
```
You can also access [Github Repo] of PaddleClas(https://github.com/PaddlePaddle/PaddleClas) and dowload the source code. Plase prepare the ImageNet1k dataset by following the guide in the [Data Tutorial](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.0/docs/zh_CN/tutorials/data.md).

**Step 2**：Perform the Training

```bash
export HIP_VISIBLE_DEVICES=0,1,2,3

cd PaddleClas/
python -m paddle.distributed.launch --gpus="0,1,2,3" tools/train.py -c ./ppcls/configs/ImageNet/ResNet/ResNet50.yaml
```

**Step 3**: The Best Top1 Accuracy got from the four-card training is:

```bash
# The result of CUDA is CUDA 10.1 + 4-card V100 training
2021-03-24 01:16:08,548 - INFO - The best top1 acc 0.76332, in epoch: 118

# The result of ROCm is ROCm 4.0.1 + 4-card DCU training
2021-04-07 10:26:31,651 - INFO - The best top1 acc 0.76308, in epoch: 109
```

#### Example of Training YoloV3

**Step 1**：Download the code of YoloV3

```bash
cd path_to_clone_PaddleDetection
git clone https://github.com/PaddlePaddle/PaddleDetection.git
```
You can also access PaddleDetection's [Github Repo](https://github.com/PaddlePaddle/PaddleDetection) and download the source code. 

**Step 2**：Prepare the VOC dataset

```bash
cd PaddleDetection/dataset/voc
python download_voc.py
python create_list.py
```

**Step 3**：Modify parameters of the configuration file

The parameters of the configuration file `configs/yolov3/yolov3_darknet53_270e_voc.yml` is of eight-card design by default. If it is a single-computer four-card training with DCU, you need to modify parameters like: 

```bash
# Modify configs/yolov3/_base_/optimizer_270e.yml
base_lr: 0.0005

# Modify configs/yolov3/_base_/yolov3_reader.yml
worker_num: 1
```

**Step 4**：Perform the training

```bash
export HIP_VISIBLE_DEVICES=0,1,2,3

cd PaddleDetection/
python -m paddle.distributed.launch --gpus 0,1,2,3 tools/train.py -c configs/yolov3/yolov3_darknet53_270e_voc.yml --eval
```

**Step 5**：The mAP acquired in the four-card training is: 

```bash
# The result of CUDA is CUDA 10.1 + 4-card V100 training
[03/23 05:26:17] ppdet.metrics.metrics INFO: mAP(0.50, 11point) = 82.59%

# The result of ROCm is ROCm 4.0.1 + 4-card DCU training
[03/28 16:02:52] ppdet.metrics.metrics INFO: mAP(0.50, 11point) = 83.02%
```
