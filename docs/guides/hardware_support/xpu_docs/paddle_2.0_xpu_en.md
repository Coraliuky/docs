# Support for KUNLUN XPU Chips Offered by PaddlePaddle

Paddle 2.0 and its subsequent versions can all run on the KUNLUN XPU chips. Supports in the verified model training and inference are: 

## Training Support

Models that can perform single-computer single-card/multi-card training are: 

| Model               | Field     | Model readme                                                   | Coding Paradigm      | Available CPU           | Whether the single-computer multi-card training is supported   |
| ------------------ | -------- | ------------------------------------------------------------ | ------------- | ----------------------- | -------------- |
| VGG16/19           | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.1/docs/zh_CN/extension/train_on_xpu.md) | Static Graph        | X86（Intel）            | Supported           |
| ResNet50           | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.1/docs/zh_CN/extension/train_on_xpu.md) | Static Graph        | X86（Intel）ARM（Phytium） | Supported           |
| MobileNet_v3       | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.1/docs/zh_CN/extension/train_on_xpu.md) | Static Graph        | X86（Intel）            | Supported           |
| HRNet              | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.1/docs/zh_CN/extension/train_on_xpu.md) | Static Graph        | X86（Intel）            | Supported           |
| Yolov3-DarkNet53   | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/train_on_kunlun.md) | Static Graph        | X86（Intel）ARM（Phytium） | Supported           |
| Yolov3-MobileNetv1 | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/train_on_kunlun.md) | Static Graph        | X86（Intel）            | Supported           |
| PPYOLO             | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/train_on_kunlun.md) | Static Graph        | X86（Intel）            | Supported           |
| Mask_RCNN          | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.1/docs/tutorials/train_on_kunlun.md) | Static Graph        | X86（Intel）            | Supported           |
| Deeplab_v3         | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/blob/release/2.1/legacy/docs/train_on_xpu.md) | Static Graph        | X86（Intel）            | Supported           |
| Unet               | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/blob/release/2.1/legacy/docs/train_on_xpu.md) | Static Graph        | X86（Intel）            | Supported           |
| LSTM               | NLP      | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/release/2.0/examples/text_classification/rnn) | Static Graph/ Dynamic Graph | X86（Intel）            | Supported           |
| Bert-Base          | NLP      | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/blob/release/2.0/examples/language_model/bert/README.md) | Static Graph/ Dynamic Graph | X86（Intel）            | Supported (Static Graph) |
| Ernie-Base         | NLP      |                                                              | Static Graph/ Dynamic Graph | X86（Intel）            | Supported (Static Graph) |
| NAML               | Recommendation     | [Model Link](https://github.com/PaddlePaddle/PaddleRec/blob/release/2.1.0/models/rank/naml/train_on_kunlun.md) | Static Graph        | X86（Intel）            | Supported           |
| DQN                | Reinforcement Learning  | [Model Link](https://github.com/PaddlePaddle/PARL/blob/r1.4.3/examples/DQN/train_on_xpu.md) | Static Graph       | X86（Intel）            | Supported           |

Models are kept in PaddlePaddle model suites as independent repos in github.com/PaddlePaddle. You can get the models you needed through git clone:

| Field     | Suite        | Branch/Version   |
| -------- | --------------- | ----------- |
| Image Classification | PaddleClas      | release/2.1 |
| Object Detection | PaddleDetection | release/2.1 |
| Image Segmentation | PaddleSeg       | release/2.1 |
| NLP      | PaddleNLP       | release/2.0 |
| Recommendation     | PaddleRec       | release/2.1 |
| Reinforcement Learning | PARL            | >= r1.4     |



## Inference Support

The Paddle framework collects all the original inference functions in Python and you can use it out of the box. 
Besides the framework, there are also many high-performance inference libraries offered by PaddlePaddle, including Paddle Inference, Paddle Serving, and Paddle Lite. Deployment scenarios in different cloud, edge, and end environments are supported. Many hardware platforms, operating systems, and code languages are supported. At the same time, the service-oriented deployment capability is provided. Currently the models that can be verified by inference libraries include: 

| Model                     | Field     | Coding Paradigm | Available CPU           |
| ------------------------ | -------- | -------- | ----------------------- |
| VGG16/19                 | Image Classification | Static Graph   | X86（Intel）            |
| ResNet50                 | Image Classification | Static Graph   | X86（Intel）ARM（Phytium） |
| GoogleNet                | Image Classification | Static Graph   | X86（Intel）            |
| yolov3-darknet53         | Object Detection | Static Graph   | X86（Intel）ARM（Phytium） |
| yolov3-mobilenetv1       | Object Detection | Static Graph   | X86（Intel）            |
| ch_ppocr_mobile_v2.0_det | OCR      | Dynamic Graph   | X86（Intel）            |
| ch_ppocr_mobile_v2.0_rec | OCR      | Dynamic Graph   | X86（Intel）            |
| ch_ppocr_server_v2.0_det | OCR      | Dynamic Graph   | X86（Intel）            |
| ch_ppocr_server_v2.0_rec | OCR      | Dynamic Graph   | X86（Intel）            |
| LSTM                     | NLP      | Static Graph   | X86（Intel）            |
| Bert-Base                | NLP      | Static Graph   | X86（Intel）            |
| Ernie-Base               | NLP      | Static Graph   | X86（Intel）            |


As the ARM architecture has more advantages in performance, energy consumption, and costs, the ARM CPUs have been applied to more PCs and servers, and many cutting-edge domestic CPUs also adopt the ARM architecture. Under these circumstances, we have also tried running the Paddle framework on the ARM CPU+ KUNLUN XPU. Now we have tested the training and inference of ResNet50 and YOLOv3. Subsequent releases will test the KUNLUN XPUs on more model tasks. 
