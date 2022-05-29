# Instruction on Installing the Paddle KUNLUN Generation 2 Version

The Paddle framework supports the Python training and original inference on the KUNLUN Generation 2 chips . The latest version is 2.3 rc and there are two installation methods: 

**1. Pre-compiled wheel package which supports the KUNLUN Generation 2 chips**

Currently the wheel package only supports one kind of environment:

Intel CPU+ KUNLUN Generation 2 chip +Linux Operating System

**2. Source-code compilation and installation**

If you want to use other environments, choose the source-code compilation and installation.

## Method 1：Use the wheel package for installation

### Download the installation package

**Environment 1：Intel CPU+ Kunlun Generation 2 Chip +Linux Operating System**

The release version of Linux should use the CentOS 7 system.

Python3.7

```
wget https://paddle-inference-lib.bj.bcebos.com/2.3.0-rc0/python/Linux/XPU2/x86-64_gcc8.2_py36_avx_mkl/paddlepaddle_xpu-2.3.0rc0-cp37-cp37m-linux_x86_64.whl
```

```
python3.7 -m pip install -U paddlepaddle_xpu-2.3.0rc0-cp37-cp37m-linux_x86_64.whl
```


### Verify installation 

After the installation, you can use python or python3 to enter into the python interpreter, and import

```
import paddle
```

And import

```
paddle.utils.run_check()
```

If there is a line "PaddlePaddle is installed successfully!"，it means that the installation is done. 

* Attention: For the support for the compiled whl package of the KUNLUN Generation 2 chips based on Kermel Primitive operators, please [click](https://www.kunlunxin.com.cn).

## Method 2：Compile the package which supports the KUNLUN XPU with the source code

### Environment Preparation

**Intel CPU+ KUNLUN Generation 2 chip +CentOS system**

- **Processor：Intel(R) Xeon(R) Gold 6148 CPU @2.40GHz**
- **Operating System：CentOS 7.8.2003（CentOS 7 is recommended）**
- **Python version： 3.7 (64 bit)**
- **pip/pip3：9.0.1+ (64 bit)**
- **cmake：3.15+**
- **gcc/g++：8.2+**


### Procedure of the souce-code compilation and installation:


（1）Paddle depends on cmake for creating compilation, and the cmake version should >=3.15. If the source provdied by the operating system contains an appropriate version of cmkae, you can perform installation directly. Otherwise, you need to 

```
wget https://github.com/Kitware/CMake/releases/download/v3.16.8/cmake-3.16.8.tar.gz
tar -xzf cmake-3.16.8.tar.gz && cd cmake-3.16.8
./bootstrap && make && sudo make install
```

（2）In Paddle, patchelf is used to modify the rpath of the dynamic repository. If the source offered by the operating system contains patchelf, you can perform installation directly, otherwise you need to use the source-code installation. You can refer to 

```
./bootstrap.sh
./configure
make
make check
sudo make install
```

（3）You can install Python dependency repositories according to [requirments.txt](https://github.com/PaddlePaddle/Paddle/blob/develop/python/requirements.txt).

（4）Clone the source code of Paddle into the Paddle folder in the current direcotry, and enter into the Paddle directory 

```
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle
```

Use stable versions for compilation, and it is recommended to release2.3 branch: 

```
git checkout release/2.3
```

（5）Compile the wheel package, and create and enter into a directory named build

```
mkdir build && cd build
```

For the meaning of compilation options, you can refer to [Compilation Option Table](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/install/Tables.html#Compile)

**Intel CPU+ KUNLUN Generation2 chip +CentOS system**

During the linkeage, there are many open files so that the system default limit may be exceeded and a compilation error may occur. You can set the maximum open files allowed in the process: 

```
ulimit -n 4096
```

Execute cmake，and finish the compilation

Python3.7

```
cmake .. -DPY_VERSION=3.7 \
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

make -j$(nproc)
```

（6）After the compilation is done, enter into the directory Paddle/build/python/dist and find the generated .whl package.

（7）Copy the .whl package to the target machine containing the KUNLUN XPU, and install Python dependency libraries on the target machine according to [requirments.txt](https://github.com/PaddlePaddle/Paddle/blob/develop/python/requirements.txt). (If the compiler contains a target machine with the KUNLUN XPU at the same time, skip the step) 

（8）Install the compiled .whl package on the target machine containing the KUNLUN XPU: pip install -U（name of the whl package） or pip3 install -U（name of the whl package）. Congratulations! You have finished all the steps of compilation and installation of PaddlePaddle on the KUNLUN XPU. 

**Verify installation**

After installation, you can use python or python3 to enter into the python interpreter and import

```
import paddle
```

Then import

```
paddle.utils.run_check()
```

If there is a line "PaddlePaddle is installed successfully!"，it means that you have finished the installation. 

### How to Uninstall 

Run the following command to uninstall PaddlePaddle：

```
pip uninstall paddlepaddle
```

or

```
pip3 uninstall paddlepaddle
```

* Attention：For the source-code compilation of the KUNLUN Generation 2 chip based on the Kermel Primitive operator，[click](https://www.kunlunxin.com.cn).
