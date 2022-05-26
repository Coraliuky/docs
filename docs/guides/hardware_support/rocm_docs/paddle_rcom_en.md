
# Models Supported by the Paddle ROCm Version

Currently the Paddle ROCm version based on the Hygon CPU(X86) and DCU supports the single-computer single-card/multi-card model training and inference. 

## Image Classification

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| ResNet50  | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/ResNet/ResNet50.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| ResNet101  | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/ResNet/ResNet101.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| SE_ResNet50_vd  | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/SENet/SE_ResNet50_vd.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| VGG16 | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/VGG/VGG16.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| InceptionV4 | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/Inception/InceptionV4.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| GoogleNet | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/Inception/GoogLeNet.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| MobileNetV3 | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/MobileNetV3/MobileNetV3_large_x1_0.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| AlexNet | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/AlexNet/AlexNet.yaml) |  Dynamic Graph  | Supported | Supported | Supported |
| DenseNet121 | Image Classification | [Model Link](https://github.com/PaddlePaddle/PaddleClas/blob/release/2.3/ppcls/configs/ImageNet/DenseNet/DenseNet121.yaml) |  Dynamic Graph  | Supported | Supported | Supported |


## Object Detection

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| YOLOv3  | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/yolov3) |  Dynamic Graph  | Supported | Supported | Supported |
| PP-YOLO | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/ppyolo) |  Dynamic Graph  | Supported | Supported | Supported |
| SSD | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/ssd) |  Dynamic Graph  | Supported | Supported | Supported |
| RetinaNet | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/static/configs/retinanet_r50_fpn_1x.yml) |  Static Graph   | Supported | Supported | Supported |
| Faster R-CNN  | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/faster_rcnn) |  Dynamic Graph  | Supported | Supported | Supported |
| Faster R-CNN + FPN | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/faster_rcnn) |  Dynamic Graph  | Supported | Supported | Supported |
| Cascade Faster R-CNN | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/cascade_rcnn) |  Dynamic Graph  | Supported | Supported | Supported |
| Libra R-CNN | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/static/configs/libra_rcnn/README_cn.md) |  Static Graph   | Supported | Supported | Supported |
| Mask R-CNN  | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/mask_rcnn) |  Dynamic Graph  | Supported | Supported | Supported |
| Mask R-CNN + FPN  | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/mask_rcnn) |  Dynamic Graph  | Supported | Supported | Supported |
| Cascade Mask R-CNN | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/cascade_rcnn) |  Dynamic Graph  | Supported | Supported | Supported |
| SOLOv2 | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/solov2) |  Dynamic Graph  | Supported | Supported | Supported |
| FCOS | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/fcos) |  Dynamic Graph  | Supported | Supported | Supported |
| TTFNet | Object Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/ttfnet) |  Dynamic Graph  | Supported | Supported | Supported |
| BlazeFace | Face Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/configs/face_detection) |  Dynamic Graph  | Supported | Supported | Supported |
| FaceBoxes | Face Detection | [Model Link](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.2/static/docs/featured_model/FACE_DETECTION.md) |  Static Graph  | Supported | Supported | Supported |

## 图像分割

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| ANN | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/ann) |  Dynamic Graph  | Supported | Not Supported | Supported |
| BiSeNetV2 | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/bisenet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| DANet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/danet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| DeepLabV3+ | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/deeplabv3p) |  Dynamic Graph  | Supported | Not Supported | Supported |
| Fast-SCNN | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/fastscnn) |  Dynamic Graph  | Supported | Not Supported | Supported |
| FCN | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/fcn) |  Dynamic Graph  | Supported | Not Supported | Supported |
| GCNet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/gcnet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| GSCNN | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/gscnn) |  Dynamic Graph  | Supported | Not Supported | Supported |
| HarDNet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/hardnet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| OCRNet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/ocrnet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| U-Net | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/unet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| DecoupledSegNet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/decoupled_segnet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| EMANet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/emanet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| ISANet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/isanet) |  Dynamic Graph  | Supported | Not Supported | Supported |
| DNLNet | Image Segmentation | [Model Link](https://github.com/PaddlePaddle/PaddleSeg/tree/release/v2.0/configs/dnlnet) |  Dynamic Graph  | Supported | Not Supported | Supported |

## Natural Language Processing

| Model               | Field     | Model Link                                                   | Coding Paradigm      | Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| BERT | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/language_model/bert) |  Dynamic Graph  | Supported | Supported | Supported |
| XLNet | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/language_model/xlnet) |  Dynamic Graph  | Supported | Supported | Supported |
| ELECTRA | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/language_model/electra) |  Dynamic Graph  | Supported | Supported | Supported |
| Transformer | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/machine_translation/transformer) |  Dynamic Graph  | Supported | Supported | Supported |
| Seq2Seq | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/machine_translation/seq2seq) |  Dynamic Graph  | Supported | Supported | Supported |
| TextCNN | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/text_classification/rnn) |  Dynamic Graph  | Supported | Supported | Supported |
| Bi-LSTM | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/text_classification/rnn) |  Dynamic Graph  | Supported | Supported | Supported |
| LAC | NLP | [Model Link](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/lexical_analysis) |  Dynamic Graph  | Supported | Supported | Supported |

## Character Recognition

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| OCR-DB | Text Detection | [Model Link ](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.3/doc/doc_ch/detection.md) |   Dynamic Graph  | Supported | Supported | Supported |
| CRNN-CTC | Text Recognition | [Model Link ](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.3/doc/doc_ch/recognition.md) |   Dynamic Graph  | Supported | Supported | Supported |
| OCR-Clas | Angle Classification | [Model Link ](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.3/doc/doc_ch/angle_class.md) |  Dynamic Graph  | Supported | Supported | Supported |
| OCR-E2E | Character Recognition | [Model Link ](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.3/doc/doc_ch/pgnet.md) |  Dynamic Graph  | Supported | Supported | Supported |

## Recommendation System

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| DeepFM | Recommendation System | [Model Link](https://github.com/PaddlePaddle/PaddleRec/tree/release/2.1.0/models/rank/deepfm) |  Dynamic Graph  | Supported | Not Supported | Supported |
| Wide&Deep | Recommendation System | [Model Link](https://github.com/PaddlePaddle/PaddleRec/tree/release/2.1.0/models/rank/wide_deep) |  Dynamic Graph  | Supported | Not Supported | Supported |
| Word2Vec | Recommendation System | [Model Link](https://github.com/PaddlePaddle/PaddleRec/tree/release/2.1.0/models/recall/word2vec) |  Dynamic Graph  | Supported | Not Supported | Supported |
| NCF | Recommendation System | [Model Link](https://github.com/PaddlePaddle/PaddleRec/tree/release/2.1.0/models/recall/ncf) |  Dynamic Graph  | Supported | Not Supported | Supported |

## Video Classification

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| SlowFast | Video Classification | [Model Link](https://github.com/PaddlePaddle/PaddleVideo/blob/develop/docs/zh-CN/model_zoo/recognition/slowfast.md) |  Dynamic Graph  | Supported | Supported | Supported |
| TSM | Video Classification | [Model Link](https://github.com/PaddlePaddle/PaddleVideo/blob/develop/docs/zh-CN/model_zoo/recognition/tsm.md) |  Dynamic Graph  | Supported | Supported | Supported |
| TSN | Video Classification | [Model Link](https://github.com/PaddlePaddle/PaddleVideo/blob/develop/docs/zh-CN/model_zoo/recognition/tsn.md) |  Dynamic Graph  | Supported | Supported | Supported |
| Attention-LSTM | Video Classification| [Model Link](https://github.com/PaddlePaddle/PaddleVideo/blob/develop/docs/zh-CN/model_zoo/recognition/attention_lstm.md) |  Dynamic Graph  | Supported | Supported | Supported |
| BMN | Video Classification | [Model Link](https://github.com/PaddlePaddle/PaddleVideo/blob/develop/docs/zh-CN/model_zoo/localization/bmn.md) |  Dynamic Graph  | Supported | Supported | Supported |
| StNet | Video Classification | [Model Link](https://github.com/PaddlePaddle/models/tree/develop/PaddleCV/video/models/stnet) |  Dynamic Graph  | Supported | Supported | Supported |

## Speech Synthesis

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| Transformer TTS | Speech Synthesis | [Model Link ](https://github.com/PaddlePaddle/Parakeet/tree/develop/examples/transformer_tts) |  Dynamic Graph  | Supported | Supported | Supported |
| WaveFlow | Speech Synthesis | [Model Link ](https://github.com/PaddlePaddle/Parakeet/tree/develop/examples/waveflow) |  Dynamic Graph  | Supported | Supported | Supported |

## Generative Adversarial Network

| Model               | Field     | Model Link                                                   | Coding Paradigm      |  Whether the Single-Computer Multi-Card Training is Supported  | Whether the Multi-Computer Multi-Card Training is Supported  | Whether Inference is Supported |
| ----------------- | -------- | ------------------------------------------------------------ | ------------- | -------------- | -------------- | -------------- |
| Pix2Pix | Style Transfer | [Model Link](https://github.com/PaddlePaddle/PaddleGAN/blob/develop/docs/zh_CN/tutorials/pix2pix_cyclegan.md) |  Dynamic Graph  | Supported | Supported | Supported |
| CycleGAN | Style Transfer | [Model Link](https://github.com/PaddlePaddle/PaddleGAN/blob/develop/docs/zh_CN/tutorials/pix2pix_cyclegan.md) |  Dynamic Graph  | Supported | Supported | Supported |
| StyleGAN V2 | Face Generation | [Model Link](https://github.com/PaddlePaddle/PaddleGAN/blob/develop/docs/zh_CN/tutorials/styleganv2.md) |  Dynamic Graph  | Supported | Supported | Supported |
| Wav2Lip | Lip Synthesis | [Model Link](https://github.com/PaddlePaddle/PaddleGAN/blob/develop/docs/zh_CN/tutorials/wav2lip.md) |  Dynamic Graph  | Supported | Supported | Supported |
| ESRGAN | Image Super-Resolution | [Model Link](https://github.com/PaddlePaddle/PaddleGAN/blob/develop/docs/zh_CN/tutorials/single_image_super_resolution.md) |  Dynamic Graph  | Supported | Supported | Supported |
| EDVR | Video Super-Resolution | [Model Link](https://github.com/PaddlePaddle/PaddleGAN/blob/develop/docs/zh_CN/tutorials/video_super_resolution.md) |  Dynamic Graph  | Supported | Supported | Supported |

## Model Suite

Models are stored in the model suites of PaddlePaddle, which are independent repositories under github.com/PaddlePaddle , git clone and get the needed model files：

| Field      | Suite        | Branch/Version        |
| ----------- | --------------- | ---------------- |
| Image Classification     | PaddleClas      | release/2.3      |
| Object Detection     | PaddleDetection | release/2.2      |
| Image Segmentation     | PaddleSeg       | release/v2.0     |
| Natural Language Processing  | PaddleNLP       | develop          |
| Character Recognition     | PaddleOCR       | release/2.3      |
| Recommendation System     | PaddleRec       | release/2.1.0    |
| Video Classification     | PaddleVideo     | develop          |
| Speech Synthesis     | Parakeet        | develop          |
| Generative Adversarial Network  | PaddleGAN       | develop          |
