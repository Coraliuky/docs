# Support for the KUNLUN Generation 2 Chips Offered by PaddlePaddle

Paddle 2.3rc and its successive versions can all run on the KUNLUN generation 2 chips (R200，R300). Supports in the verified model training are: 

## Training Support

Models that can perform single-computer single-card/multi-card training are: 

| Model               | Field     | Coding Paradigm      | Available CPU           | Whether the single-computer single-card model training is supported   |  Whether the single-computer multi-card training is supported   |
| ------------------ | -------- |------------- | ----------------------- | -------------- | -------------- |
| ResNet50           | Image Classification | Dynamic Graph        | X86（Intel）            | Supported           |-           |
| MobileNet_v3       | Image Classification | Dynamic Graph        | X86（Intel）            | Supported           |-           |
| UNet               | Image Segmentation | Dynamic Graph        | X86（Intel）            | Supported           |-           |
| Yolov3-DarkNet53   | Object Detection | Dynamic Graph        | X86（Intel）            | Supported           |-           |
| SSD-ResNet34       | Object Detection | Dynamic Graph        | X86（Intel）            | Supported           |Supported         |
| OCR-DB             | Text Detection | Dynamic Graph        | X86（Intel）            | Supported           |-           |
| Bert-Base          | NLP     | Static Graph        | X86（Intel）            | Supported           |Supported         |
| Transformer        | NLP     | Static Graph        | X86（Intel）            | Supported           |Supported         |
| GPT-2              | NLP     | Dynamic Graph        | X86（Intel）            | Supported           |-           |
| DeepFM             | Recommendation    | Dynamic Graph        | X86（Intel）             | Supported           |-           |
| Wide&Deep          | Recommendation    | Dynamic Graph        | X86（Intel）             | Supported           |-           |



Models are stored in Paddle's model suites as independent repos in github.com/PaddlePaddle, and you can acquire what you need through git clone：

| Field     | Suite        | Branch/Version   |
| -------- | --------------- | ----------- |
| Image Classification | [PaddleClas](https://github.com/PaddlePaddle/PaddleClas)      | [develop](https://github.com/PaddlePaddle/PaddleClas/tree/develop) |
| Object Detection | [PaddleDetection](https://github.com/PaddlePaddle/PaddleDetection) | [develop](https://github.com/PaddlePaddle/PaddleDetection/tree/develop) |
| Image Segmentation | [PaddleSeg](https://github.com/PaddlePaddle/PaddleSeg)       | [develop](https://github.com/PaddlePaddle/PaddleSeg/tree/develop) |
| NLP     | [PaddleNLP](https://github.com/PaddlePaddle/PaddleNLP)       | [develop](https://github.com/PaddlePaddle/PaddleNLP/tree/develop) |
| OCR     | [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)       | [dygraph](https://github.com/PaddlePaddle/PaddleOCR/tree/dygraph) |
| Recommendation     | [PaddleREC](https://github.com/PaddlePaddle/PaddleRec)       | [master](https://github.com/PaddlePaddle/PaddleRec/tree/master) |

* Attention：For supports for KUNLUN Generation 2 chips based on the Kermel Primitive operator，[Click](https://www.paddlepaddle.org.cn/documentation/docs/zh/guides/07_new_op/kernel_primitive_api/index_cn.html).
