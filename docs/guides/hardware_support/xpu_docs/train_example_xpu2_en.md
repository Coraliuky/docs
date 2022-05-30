# Demo of Training on the Paddle KUNLUN Generation 2 Version

There is no much difference using XPU or CPU/GPU for training. It can mean that the training is executed on the KUNLUN chip if you simply configure the XPU.

#### Download ResNet50 and run the demo：

1、 Install dependencies：
```
git clone https://github.com/PaddlePaddle/PaddleClas.git -b develop
cd PaddleClas
python -m pip install -r requirements.txt
```

2、Download the dataset：
Training on ResNet50 based on the CIFAR100 dataset
```
cd dataset
rm -rf ILSVRC2012
wget -nc https://paddle-imagenet-models-name.bj.bcebos.com/data/whole_chain/whole_chain_CIFAR100.tar
tar xf whole_chain_CIFAR100.tar
ln -s whole_chain_CIFAR100 ILSVRC2012
cd ILSVRC2012
mv train.txt train_list.txt
mv test.txt val_list.txt
```

3、The command of confgiuring XPU for training is simple:
```
cd ../..
#FLAGS can designate the single-card or multi-card training. In this demo, it is the single-card training.
export FLAGS_selected_xpus=2
export XPUSIM_DEVICE_MODEL=KUNLUN2
#Start the training
python tools/train.py \
-c ppcls/configs/ImageNet/ResNet/ResNet50.yaml \
-o Global.device=xpu
```

#### Download YOLOv3-DarkNet53 and run the demo：

1、Install dependencies：
```
git clone https://github.com/PaddlePaddle/PaddleDetection.git -b develop
cd PaddleDetection/
pip install -U pip Cython
pip install -r requirements.txt
```

2、Download the dataset:
```
cd dataset/voc/
python download_voc.py
python create_list.py
cd ../..
```

3、The command of configuring XPU for training is very simple: 
```
#FLAGS can designate single-card or multi-card training. In this demo, it is the single-card training. 
export FLAGS_selected_xpus=2
export XPUSIM_DEVICE_MODEL=KUNLUN2
#Start the training
python -u tools/train.py \
-c configs/yolov3/yolov3_darknet53_270e_voc.yml \
-o use_gpu=false use_xpu=true LearningRate.base_lr=0.000125 \
--eval
```
