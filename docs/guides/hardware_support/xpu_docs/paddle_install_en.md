# Instruction on Installing the Paddle KUNLUN XPU Version

The Paddle framework supports the Python training and original inference. The latest version is 2.1 and there are two installation methods: 

**1. Pre-compiled wheel package which supports the KUNLUN XPU**

There are only two environments supported by the wheel package: 

Intel CPU+ KUNLUN XPU +CentOS system

Phytium CPU+ KUNLUN XPU+ Kirin V10 system

**2. Source-code compilation and installation**

If you want to choose other environments, you can choose the source-code compilation and installation. 

## Installation Method 1：Use the wheel package

### Download the installation package

**Environment 1：Intel CPU+ KUNLUN XPU +CentOS system**

The Linux release version should choose the CentOS 7 system.

Python3.7

```
wget https://paddle-wheel.bj.bcebos.com/kunlun/paddlepaddle-2.1.0-cp37-cp37m-linux_x86_64.whl
```

```
python3.7 -m pip install -U paddlepaddle-2.1.0-cp37-cp37m-linux_x86_64.whl
```

Python3.6

```
wget https://paddle-wheel.bj.bcebos.com/kunlun/paddlepaddle-2.1.0-cp36-cp36m-linux_x86_64.whl
```

```
python3.6 -m pip install -U ``paddlepaddle-2.1.0-cp36-cp36m-linux_x86_64.whl
```

**Environment 2：Phytium CPU+ KUNLUN XPU+ Kirin V10 system**

If you want to use the pre-compiled wheel package that supports the KUNLUN XPU, please contact the PaddlePaddle official: Paddle-better@baidu.com.

### Verify installation

After installation, you can use python or python3 to enter into the python interpreter，import

```
import paddle
```

And import

```
paddle.utils.run_check()
```

If there is a line "PaddlePaddle is installed successfully!"，it means that the installation is done. 

## Method 2: Compile the package that supports the KUNLUN XPU with the source code

### Environment Preparation

**Intel CPU+ KUNLUN XPU+ CentOS system**

- **Processor：Intel(R) Xeon(R) Gold 6148 CPU @2.40GHz**
- **Operating system：CentOS 7.8.2003（CentOS 7 is recommended）**
- **Python： 3.6/3.7 (64 bit)**
- **pip or pip3：9.0.1+ (64 bit)**
- **cmake：3.15+**
- **gcc/g++：8.2+**

**Phytium CPU+ KUNLUN XPU+ Kirin V10 system**

- **Processor：Phytium,FT-2000+/64**
- **Operating system：Kylin release V10 (SP1)/(Tercel)-aarch64-Build04/20200711**
- **Python：3.6/3.7 (64 bit)**
- **pip or pip3： 9.0.1+ (64 bit)**
- **cmake：3.15+**
- **gcc/g++：8.2+**

### Procedure of the source-code compilation and installation：


（1）Paddle depends on cmake for building compilation, and the cmake version should >=3.15. If the source offered by the operating system contains an appropriate version of cmake，you can install directly. Otherwise, you need to

```
wget https://github.com/Kitware/CMake/releases/download/v3.16.8/cmake-3.16.8.tar.gz
tar -xzf cmake-3.16.8.tar.gz && cd cmake-3.16.8
./bootstrap && make && sudo make install
```

（2）In Paddle, patchelf is used to modify rpath of dynamic repositories. If the source offered by the operating system contains patchelf，you can perform installation directly. Otherwise, you need to use the source-code installation and you can refer to

```
./bootstrap.sh
./configure
make
make check
sudo make install
```

（3）You can install Python dependency libraries according to [requirments.txt](https://github.com/PaddlePaddle/Paddle/blob/develop/python/requirements.txt).

（4）Clone the source code of Paddle to the Paddle folder in the current directory and enter into the Paddle directory

```
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle
```

Use stable versions for compilation, and you should choose the release2.1 branch：

```
git checkout release/2.1
```

（5）Compile the wheel package, and create and enter into a directory named build

```
mkdir build && cd build
```

For the meaning of compilation meanings, refer to the document [Compilation Option Table](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/install/Tables.html#Compile).

**Intel CPU+ KUNLUN XPU+CentOS system**

In the linkage process, there are many open files so that the system default limit may be exceeded and a compilation error may occur. You should set the maximum files allowed in the process：

```
ulimit -n 2048
```

Execute cmake，and finish the compilation

Python3

```
cmake .. -DPY_VERSION=3.6 \
         -DCMAKE_BUILD_TYPE=Release \
         -DWITH_GPU=OFF \
         -DWITH_XPU=ON \
         -DON_INFER=ON \
         -DWITH_PYTHON=ON \
         -DWITH_AVX=ON \
         -DWITH_MKL=ON \
         -DWITH_MKLDNN=ON \
         -DWITH_XPU_BKCL=ON \
         -DWITH_DISTRIBUTE=ON \
         -DWITH_NCCL=OFF

make -j20
```

Python2

```
cmake .. -DPY_VERSION=2.7 \
         -DCMAKE_BUILD_TYPE=Release \
         -DWITH_GPU=OFF \
         -DWITH_XPU=ON \
         -DON_INFER=ON \
         -DWITH_PYTHON=ON \
         -DWITH_AVX=ON \
         -DWITH_MKL=ON \
         -DWITH_MKLDNN=ON \
         -DWITH_XPU_BKCL=ON \
         -DWITH_DISTRIBUTE=ON \
         -DWITH_NCCL=OFF

make -j20
```

**Phytium CPU+ KUNLUN XPU+ Kirin V10 system**

In the environment, you need to pull XPU SDK by hand before compilation，and you can use the following command: 

```
wget https://paddle-wheel.bj.bcebos.com/kunlun/xpu_sdk_v2.0.0.61.tar.gz
tar xvf xpu_sdk_v2.0.0.61.tar.gz
mv output xpu_sdk_v2.0.0.61 xpu_sdk
```

Execute cmake，and finish the compilation

```
ulimit -n 4096
python_exe="/usr/bin/python3.7"
export XPU_SDK_ROOT=$PWD/xpu_sdk

cmake .. -DPY_VERSION=3.7 \
         -DPYTHON_EXECUTABLE=$python_exe \
         -DWITH_ARM=ON \
         -DWITH_AARCH64=ON \
         -DWITH_TESTING=OFF \
         -DCMAKE_BUILD_TYPE=Release \
         -DON_INFER=ON \
         -DWITH_XBYAK=OFF \
         -DWITH_XPU=ON \
         -DWITH_GPU=OFF \
         -DWITH_LITE=ON \
         -DLITE_GIT_TAG=release/v2.9 \
         -DXPU_SDK_ROOT=${XPU_SDK_ROOT}

make VERBOSE=1 TARGET=ARMV8 -j32
```

（6）After compilation, enter into Paddle/build/python/dist and find the generated .whl package.

（7）Copy the .whl package to the target machine containing the KUNLUN XPU. Install Python dependency libraries on the target machine according to [requirments.txt](https://github.com/PaddlePaddle/Paddle/blob/develop/python/requirements.txt).（If the compiler contains the KUNLUN XPU, skip the step.) 

（8）Install the compiled the .whl package on the target machine containing the KUNLUN XPU：pip install -U（name of the whl package）or pip3 install -U（name of the whl package）. Congratulations! You have finished the compilation and installation of PaddlePaddle on the KUNLUN XPU.

**Verify installation**

After installation, you can use python or python3 to enter into the python interpreter and import

```
import paddle
```

And import

```
paddle.utils.run_check()
```

If there is a line "PaddlePaddle is installed successfully!"，it means that the installation is done.

### How to uninstall

Run the following command to uninstall PaddlePaddle：

```
pip uninstall paddlepaddle
```

or

```
pip3 uninstall paddlepaddle
```
