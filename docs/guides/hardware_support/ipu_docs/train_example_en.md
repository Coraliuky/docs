# Example of Paddle IPU training 

## Training the BERT-Base Model

In the example, it is assumed that users have installed the Paddle IPU, and configurated the required runtime environment (It is suggested use the Paddle IPU in the docker environment). 

The example code is in [Paddle-BERT with Graphcore IPUs](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/examples/language_model/bert/static_ipu)

**Step 1**：Download the source code and install dependencies
```
# Download the source code 
git clone https://github.com/PaddlePaddle/PaddleNLP.git
cd paddlenlp/examples/language_model/bert/static_ipu

# Install dependencies
pip install -r requirements.txt
```

**Step 2**：Prepare the dataset

Prepare the dataset for pre-training by following the guide in `README.md`.

**Step 3**：Execute model training

With the guidance of `README.md`, start to pre-train the BERT-Base model and fine-tune the model on the SQuAD v1.1 dataset.
