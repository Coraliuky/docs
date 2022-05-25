# Instruction on Installing the Ascend NPU Version of PaddlePaddle

The Paddle NPU version supports the training and original inference which are performed based on the Huawei Kunpeng CPU and its Ascend NPU in Python.

### Environment Preparation

Since the Ascend 910 NPU version of PaddlePaddle now supports the Huawei CANN Community 5.0.2.alpha005, first deploy and configure the runtime environment of the NPU according to the requirement of the Ascend 910 NPU. For this, you can refer to the official document of Huawei: [Guide to the Installation of CANN Community](https://support.huaweicloud.com/instg-cli-cann502-alpha005/atlasdeploy_03_0002.html).

The Ascend 910 NPU version of PaddlePaddle only supports the source-code compilation and installation, and requirements for the compilation and runtime environment are: 

- **CPU:** Kunpeng920
- **Operating System:** Ubuntu 18.04 / CentOS 7.6 / KylinV10SP1 / EulerOS 2.8
- **CANN Community:** 5.0.2.alpha005
- **Python Version:** 3.7
- **Cmake Version:** 3.15+
- **GCC/G++ Version:** 8.2+

## How to install：Use the source-code compilation

**Step 1**：Prepare the runtime environment of the CANN Community 5.0.2.alpha005. (The Paddle mirror is recommended.)

You can pull the docker image where the CANN Community 5.0.2.alpha005 has been installed beforehand from the official image library of PaddlePaddle, or you can prepare the developing and runtime environment by following the [Guide to Installing the CANN Community](https://support.huaweicloud.com/instg-cli-cann502-alpha005/atlasdeploy_03_0002.html) .
```bash
# Pull the docker image
docker pull paddlepaddle/paddle:latest-dev-cann5.0.2.alpha005-gcc82-aarch64

# Start the docker container and pay attention to a parameter --device. The container only maps four NPU cards whose device ID numbers are between 4 and 7. If you want it to map other cards, just modify their ID numbers.
docker run -it --name paddle-npu-dev -v /home/<user_name>:/workspace  \
            --pids-limit 409600 --network=host --shm-size=128G \
            --cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
            --device=/dev/davinci4 --device=/dev/davinci5 \
            --device=/dev/davinci6 --device=/dev/davinci7 \
            --device=/dev/davinci_manager \
            --device=/dev/devmm_svm \
            --device=/dev/hisi_hdc \
            -v /usr/local/Ascend/driver:/usr/local/Ascend/driver \
            -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
            -v /usr/local/dcmi:/usr/local/dcmi \
            paddlepaddle/paddle:latest-dev-cann5.0.2.alpha005-gcc82-aarch64 /bin/bash

# Check whether the container can recognize the mapped Ascend DCU correctly.
npu-smi info

# The result is expected to be like:
+------------------------------------------------------------------------------------+
| npu-smi 1.9.3                    Version: 21.0.rc1                                 |
+----------------------+---------------+---------------------------------------------+
| NPU   Name           | Health        | Power(W)   Temp(C)                          |
| Chip                 | Bus-Id        | AICore(%)  Memory-Usage(MB)  HBM-Usage(MB)  |
+======================+===============+=============================================+
| 4     910A           | OK            | 67.2       30                               |
| 0                    | 0000:C2:00.0  | 0          303  / 15171      0    / 32768   |
+======================+===============+=============================================+
| 5     910A           | OK            | 63.8       25                               |
| 0                    | 0000:82:00.0  | 0          2123 / 15171      0    / 32768   |
+======================+===============+=============================================+
| 6     910A           | OK            | 67.1       27                               |
| 0                    | 0000:42:00.0  | 0          1061 / 15171      0    / 32768   |
+======================+===============+=============================================+
| 7     910A           | OK            | 65.5       30                               |
| 0                    | 0000:02:00.0  | 0          2563 / 15078      0    / 32768   |
+======================+===============+=============================================+
```

**Step 2**：Download the source code of PaddlePaddle and have it compiled. To get the meaning of CMAKE compilation options, please refer to the [Compilation Option Table](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/install/Tables.html#Compile)

```bash
# Download the source code
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle

# Create the compilation directory
mkdir build && cd build

# Execute cmake
cmake .. -DPY_VERSION=3.7 -DWITH_ASCEND=OFF -DWITH_ARM=ON -DWITH_ASCEND_CL=ON \
         -DWITH_ASCEND_INT64=ON -DWITH_DISTRIBUTE=ON -DWITH_TESTING=ON -DON_INFER=ON \
         -DCMAKE_BUILD_TYPE=Release -DCMAKE_EXPORT_COMPILE_COMMANDS=ON

# Use the following command line for compilation
make TARGET=ARMV8 -j$(nproc)
```

**Step 3**：Install and verify the compiled wheel package

After compilation, enter into `Paddle/build/python/dist`and find the .whl installation package. Commands of installation and verification are:

```bash
# Installation command
python -m pip install -U paddlepaddle_npu-0.0.0-cp37-cp37m-linux_aarch64.whl

# Verification command
python -c "import paddle; paddle.utils.run_check()"

# The result is expected to be like: 
Running verify PaddlePaddle program ...
PaddlePaddle works well on 1 NPU.
PaddlePaddle works well on 4 NPUs.
PaddlePaddle is installed successfully! Let's start deep learning with PaddlePaddle now.
```

## Uninstallation

Run the following command to uninstall Paddle:

```bash
pip uninstall paddlepaddle-npu
```
