# Instruction on Installing the Paddle ROCm Version

The Paddle ROCm Version supports the training and the original inference which are performed in Python based on the Hygon CPU and DCU. The compatible ROCm version is 4.0.1, and there are two ways to have it installed: 

- Use the pre-compiled wheel package 
- Use the source-code compilation

## Method 1: Use the pre-compiled wheel package 

**Attention**：Now there are only docker images bsed on CentOS 7.8 & ROCm 4.0.1 and wheel packages of Python 3.7.

**Step 1**：Prepare the runtime environment of ROCm 4.0.1 (The Paddle image is recommended)

Pull docker images where the ROCm 4.0.1 is pre-installed from the official image library of PaddlePaddle, or prepare the runtime environment according to the [ROCm Installationg Document](https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html#centos-rhel).

```bash
# Pull docker images
docker pull paddlepaddle/paddle:latest-dev-rocm4.0-miopen2.11

# Start the container, and pay attention to the parameters here. For example, shm-size and device are needed to be configured. 
docker run -it --name paddle-rocm-dev --shm-size=128G \
     --device=/dev/kfd --device=/dev/dri --group-add video \
     --cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
     paddlepaddle/paddle:latest-dev-rocm4.0-miopen2.11 /bin/bash

# Check whether the Hygon DCU can be recognized correctly. 
rocm-smi

# The result is expected to be like: 
======================= ROCm System Management Interface =======================
================================= Concise Info =================================
GPU  Temp   AvgPwr  SCLK     MCLK    Fan   Perf  PwrCap  VRAM%  GPU%  
0    50.0c  23.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
1    48.0c  25.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
2    48.0c  24.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
3    49.0c  27.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
================================================================================
============================= End of ROCm SMI Log ==============================
```

**Step 2**：Donwload the Python3.7 wheel installation package

```bash
pip install --pre paddlepaddle-rocm -f https://www.paddlepaddle.org.cn/whl/rocm/develop.html
```

**Step 3**：Verify the package

After the installation, run the following command. If there is a line of text "PaddlePaddle is installed successfully!", you should know the the installation has done. 

```bash
python -c "import paddle; paddle.utils.run_check()"
```

## Method 2: Use the source-code compilation

**Attention**：Now Paddle only supports the compilation environment of CentOS 7.8 & ROCm 4.0.1. And according to the requirement of ROCm 4.0.1, the supported compiler is devtoolset-7.

**Step 1**：Prepare the compilation environment of ROCm 4.0.1 (The Paddle image is recommended.)

Pull docker images where the ROCm 4.0.1 is pre-installed from the official image library of PaddlePaddle, or prepare the runtime environment according to the [ROCm Installationg Document](https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html#centos-rhel).

```bash
# Pull docker images
docker pull paddlepaddle/paddle:latest-dev-rocm4.0-miopen2.11

# Start the container, and pay attention to the parameters here. For example, shm-size and device are needed to be configured. 
docker run -it --name paddle-rocm-dev --shm-size=128G \
     --device=/dev/kfd --device=/dev/dri --group-add video \
     --cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
     paddlepaddle/paddle:latest-dev-rocm4.0-miopen2.11 /bin/bash

# Check whether the Hygon DCU can be recognized correctly. 
rocm-smi

# The result is expected to be like: 
======================= ROCm System Management Interface =======================
================================= Concise Info =================================
GPU  Temp   AvgPwr  SCLK     MCLK    Fan   Perf  PwrCap  VRAM%  GPU%  
0    50.0c  23.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
1    48.0c  25.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
2    48.0c  24.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
3    49.0c  27.0W   1319Mhz  800Mhz  0.0%  auto  300.0W    0%   0%  
================================================================================
============================= End of ROCm SMI Log ==============================
```

Before compilation, check whether the following environment variables are correct. If not, install matched dependencies and export correct variables. Take an official image of Paddle as an example. The variables are: 

```bash
# There is devtoolset-7 in PATH and LD_LIBRARY_PATH. If not, run the command:
source /opt/rh/devtoolset-7/enable

# There is cmake 3.16.0 in PATH.
export PATH=/opt/cmake-3.16/bin:${PATH}

# There is rocm 4.0.1 in PATH and LD_LIBRARY_PATH. 
export PATH=/opt/rocm/opencl/bin:/opt/rocm/bin:${PATH}
export LD_LIBRARY_PATH=/opt/rocm/lib:${LD_LIBRARY_PATH}

# There is Python 3.7 in PATH.
# Attention: Python 3.7 in the image is installed by miniconda. Load the Python 3.7 environment by using the command of conda activate base.
export PATH=/opt/conda/bin:${PATH}
```

**Step 2**：Donwload the source code of Paddle and have it compiled. For the meaning of CMAKE compilation options, refer to [Compilation Option Table](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/install/Tables.html#Compile).

```bash
# Download the source code to the develop branch by default
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle

# Build a compilation directory
mkdir build && cd build

# Execute cmake
cmake .. -DPY_VERSION=3.7 -DWITH_ROCM=ON -DWITH_TESTING=ON -DWITH_DISTRIBUTE=ON \
         -DWITH_MKL=ON -DCMAKE_BUILD_TYPE=Release

# Run the following command for compilation
make -j$(nproc)
```

**Step 3**：Install and verified the generated wheel package 

After compilation, enter into `Paddle/build/python/dist`and find the .whl installation package. The commands of installation and verification are: 

```bash
# Installation Command
python -m pip install -U paddlepaddle_rocm-0.0.0-cp37-cp37m-linux_x86_64.whl

# Verification Command
python -c "import paddle; paddle.utils.run_check()"
```

## How to Unintall

Run the following command to uninstall Paddle:

```bash
pip uninstall paddlepaddle-rocm
```
