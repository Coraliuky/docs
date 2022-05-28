# Example of Inference on the Paddle ROCm Version

There is no much difference using the Hygon CPU/DCU or Intel CPU/Nvidia GPU for model inference. The original inference library of PaddlePaddle, Paddle Inference is supported, and it is applicable to high-performance server-side inference and cloud inference. The Paddle ROCm version is fully compatible with the C++/Python API of the Paddle CUDA version. You can use the original inference commands and parameters without any refinement. 

## C++ Inference and Deployment

**Attention**：For more about how to use APIs in C++ inference, please refer to [Paddle Inference - C++ API](https://paddleinference.paddlepaddle.org.cn/api_reference/cxx_api_index.html).

**Step 1**：Compile the C++ inference library with source code

Now the Paddle ROCm version only supports offering the C++ inference library through the source-code compilation. For the preparation of the runtime environment, please refer to [Instruction on Installing the Paddle ROCm Version: Use the Source-Code Compilation](./paddle_install_cn.html).

```bash
# Download the source code, and choose the branch of release/2.1
git clone -b release/2.1 https://github.com/PaddlePaddle/Paddle.git
cd Paddle

# Build a compilation directory
mkdir build && cd build

# Execute cmake，and you should set the option of inference optimization to ON_INFER
cmake .. -DPY_VERSION=3.7 -DWITH_ROCM=ON -DWITH_TESTING=OFF -DON_INFER=ON \
         -DWITH_MKL=ON -DCMAKE_BUILD_TYPE=Release -DCMAKE_EXPORT_COMPILE_COMMANDS=ON

# Run the following command for compilation 
make -j$(nproc)
```

After the compilation, `paddle_inference_install_dir` under the `build` is the C++ inference library. Its directory is like: 

```bash
build/paddle_inference_install_dir
├── CMakeCache.txt
├── paddle
│   ├── include                                    Directory of the header of the C++ inference library
│   │   ├── crypto
│   │   ├── experimental
│   │   ├── internal
│   │   ├── paddle_analysis_config.h
│   │   ├── paddle_api.h
│   │   ├── paddle_infer_declare.h
│   │   ├── paddle_inference_api.h                 header of the C++ inference library
│   │   ├── paddle_mkldnn_quantizer_config.h
│   │   ├── paddle_pass_builder.h
│   │   └── paddle_tensor.h
│   └── lib
│       ├── libpaddle_inference.a                  static file of the C++ inference library
│       └── libpaddle_inference.so                 dynamic file of the C++ inference library 
├── third_party
│   ├── install                                    Third-party library and its header
│   │   ├── cryptopp
│   │   ├── gflags
│   │   ├── glog
│   │   ├── mkldnn
│   │   ├── mklml
│   │   ├── protobuf
│   │   └── xxhash
│   └── threadpool
│       └── ThreadPool.h
└── version.txt
```

The file `version.txt` contains the version information about that inference library, such as Git Commit ID, the use of OpenBlas or MKL mathematic library, and the ROCm/MIOPEN version number. For example:

```bash
GIT COMMIT ID: e75412099f97a49701324788b468d80391293ea9
WITH_MKL: ON
WITH_MKLDNN: ON
WITH_GPU: OFF
WITH_ROCM: ON
HIP version: 4.0.20496-4f163c68
MIOpen version: v2.11
CXX compiler version: 7.3.1
```

**Step 2**：Prepare a model of inference and deployment

Download [ResNet50](https://paddle-inference-dist.bj.bcebos.com/Paddle-Inference-Demo/resnet50.tgz) and have it comprssed. Then you will get a model which is of the Paddle format and stored in the ResNet50 folder. If you want to check its structure, use the model visualization tool [Netron](https://netron.app/) to open the inference.pdmodel file. 

```bash
wget https://paddle-inference-dist.bj.bcebos.com/Paddle-Inference-Demo/resnet50.tgz
tar zxf resnet50.tgz

# You will get a model directory which is a file: 
resnet50/
├── inference.pdmodel
├── inference.pdiparams.info
└── inference.pdiparams
```

**Step 3**：Get the demo code of inference, compile and run it.  

**Prerequisite**：

In this chapter, the demo code of C++ inference is in [Paddle-Inference-Demo/c++/resnet50](https://github.com/PaddlePaddle/Paddle-Inference-Demo/tree/master/c++/resnet50).

Download the demo code and rename the folder `paddle_inference_install_dir` which has been compiled in the step 1 as `paddle_inference`, and move it to the directory `Paddle-Inference-Demo/c++/lib` of the code.  Here are the files needed. 

```bash
-rw-r--r-- 1 root root 3479 Jun  2 03:14 README.md                 README
-rw-r--r-- 1 root root 3051 Jun  2 03:14 resnet50_test.cc          Source code of C++ inference
drwxr-xr-x 2 root root 4096 Mar  5 07:43 resnet50                  Folder of the model of inference and deployment which has been prepared in step 2
-rw-r--r-- 1 root root  387 Jun  2 03:14 run.sh                    Run the script
-rwxr-xr-x 1 root root 1077 Jun  2 03:14 compile.sh                Compile the script
-rw-r--r-- 1 root root 9032 Jun  2 07:26 ../lib/CMakeLists.txt     CMAKE file
drwxr-xr-x 1 root root 9032 Jun  2 07:26 ../lib/paddle_inference   the folder of Paddle Infernece which has been compiled in step 1
```

Before compiling and running the inference demo, compile the script `compile.sh` according to the runtime environment configuration.

```bash
# Confirm whether the following labels should be turned on according to the version.txt in the pre-compiled library
WITH_MKL=ON  
WITH_GPU=OFF # You should turn off WITH_GPU
USE_TENSORRT=OFF

WITH_ROCM=ON # You should turn on WITH_ROCM
ROCM_LIB=/opt/rocm/lib
```

Run the script `run.sh` for compilation and operation of the demo code. You'll get the final inference result:

```bash
bash run.sh

# After the execution, the expected result is like: 
... ...
I0602 04:12:03.708333 52627 analysis_predictor.cc:595] ======= optimize end =======
I0602 04:12:03.709321 52627 naive_executor.cc:98] ---  skip [feed], feed -> inputs
I0602 04:12:03.710139 52627 naive_executor.cc:98] ---  skip [save_infer_model/scale_0.tmp_1], fetch -> fetch
I0602 04:12:03.711813 52627 device_context.cc:624] oneDNN v2.2.1
WARNING: Logging before InitGoogleLogging() is written to STDERR
I0602 04:12:04.106405 52627 resnet50_test.cc:73] run avg time is 394.801 ms
I0602 04:12:04.106503 52627 resnet50_test.cc:88] 0 : 0
I0602 04:12:04.106525 52627 resnet50_test.cc:88] 100 : 2.04163e-37
I0602 04:12:04.106552 52627 resnet50_test.cc:88] 200 : 2.1238e-33
I0602 04:12:04.106573 52627 resnet50_test.cc:88] 300 : 0
I0602 04:12:04.106591 52627 resnet50_test.cc:88] 400 : 1.6849e-35
I0602 04:12:04.106603 52627 resnet50_test.cc:88] 500 : 0
I0602 04:12:04.106618 52627 resnet50_test.cc:88] 600 : 1.05767e-19
I0602 04:12:04.106643 52627 resnet50_test.cc:88] 700 : 2.04094e-23
I0602 04:12:04.106670 52627 resnet50_test.cc:88] 800 : 3.85254e-25
I0602 04:12:04.106683 52627 resnet50_test.cc:88] 900 : 1.52391e-30
```

## Demo of Python Inference and Deployment

**Attention**：For more about APIs of Python inference, please refer to [Paddle Inference - Python API](https://paddleinference.paddlepaddle.org.cn/api_reference/python_api_index.html).

**Step 1**：Install the Python inference library

You can install or compile its Python inference library by following the [Instruction on Installing the Paddle ROCm Version](./paddle_install_cn.html).

**Step 2**：Prepare the model of inference and deployment

Download [ResNet50](https://paddle-inference-dist.bj.bcebos.com/Paddle-Inference-Demo/resnet50.tgz) and have it compiled, and you'll get a model which is of the Paddle inference format and stored in the ResNet50 folder. If you want it check its structure, you can open the inference.pdmodel file by using the model visualization tool [Netron](https://netron.app/).

```bash
wget https://paddle-inference-dist.bj.bcebos.com/Paddle-Inference-Demo/resnet50.tgz
tar zxf resnet50.tgz

# Get the model directory, which is a file:
resnet50/
├── inference.pdmodel
├── inference.pdiparams.info
└── inference.pdiparams
```

**Step 3**：Prepare the programme of inference and deployment

Store the following code into one file and name it as `python_demo.py`：

```bash
import argparse
import numpy as np

# Cite the paddle inference library
import paddle.inference as paddle_infer

def main():
    args = parse_args()

    # Create config
    config = paddle_infer.Config(args.model_file, args.params_file)

    # Create predictor according to config
    predictor = paddle_infer.create_predictor(config)

    # Get the input name
    input_names = predictor.get_input_names()
    input_handle = predictor.get_input_handle(input_names[0])

    # Set the input
    fake_input = np.random.randn(args.batch_size, 3, 318, 318).astype("float32")
    input_handle.reshape([args.batch_size, 3, 318, 318])
    input_handle.copy_from_cpu(fake_input)

    # Run the predictor
    predictor.run()

    # Get the output
    output_names = predictor.get_output_names()
    output_handle = predictor.get_output_handle(output_names[0])
    output_data = output_handle.copy_to_cpu() # numpy.ndarray类型
    print("Output data size is {}".format(output_data.size))
    print("Output data shape is {}".format(output_data.shape))

def parse_args():
    parser = argparse.ArgumentParser()
    parser.add_argument("--model_file", type=str, help="model filename")
    parser.add_argument("--params_file", type=str, help="parameter filename")
    parser.add_argument("--batch_size", type=int, default=1, help="batch size")
    return parser.parse_args()

if __name__ == "__main__":
    main()
```

**Step 4**：Execute the inference programme

```bash
# The input file is the same as the ResNet50 in the step 2
python python_demo.py --model_file ./resnet50/inference.pdmodel \
                      --params_file ./resnet50/inference.pdiparams \
                      --batch_size 2

# After the execution, the expected output result is like:
... ...
I0602 04:14:13.455812 52741 analysis_predictor.cc:595] ======= optimize end =======
I0602 04:14:13.456934 52741 naive_executor.cc:98] ---  skip [feed], feed -> inputs
I0602 04:14:13.458562 52741 naive_executor.cc:98] ---  skip [save_infer_model/scale_0.tmp_1], fetch -> fetch
Output data size is 2000
Output data shape is (2, 1000)
```
