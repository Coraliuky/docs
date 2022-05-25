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

**Step 1**：Prepare the runtime environment of CANN Community 5.0.2.alpha005. (The Paddle mirror is recommended.)

可以直接从Paddle的官方镜像库拉取预先装有 CANN 社区版 5.0.2.alpha005 的 docker 镜像，或者根据 [CANN社区版安装指南](https://support.huaweicloud.com/instg-cli-cann502-alpha005/atlasdeploy_03_0002.html) 来准备相应的开发与运行环境。

```bash
# 拉取镜像
docker pull paddlepaddle/paddle:latest-dev-cann5.0.2.alpha005-gcc82-aarch64

# 启动容器，注意这里的参数 --device，容器仅映射设备ID为4到7的4张NPU卡，如需映射其他卡相应增改设备ID号即可
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

# 检查容器中是否可以正确识别映射的昇腾DCU设备
npu-smi info

# 预期得到类似如下的结果
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

**第二步**：下载Paddle源码并编译，CMAKE编译选项含义请参见[编译选项表](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/install/Tables.html#Compile)

```bash
# 下载源码
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle

# 创建编译目录
mkdir build && cd build

# 执行cmake
cmake .. -DPY_VERSION=3.7 -DWITH_ASCEND=OFF -DWITH_ARM=ON -DWITH_ASCEND_CL=ON \
         -DWITH_ASCEND_INT64=ON -DWITH_DISTRIBUTE=ON -DWITH_TESTING=ON -DON_INFER=ON \
         -DCMAKE_BUILD_TYPE=Release -DCMAKE_EXPORT_COMPILE_COMMANDS=ON

# 使用以下命令来编译
make TARGET=ARMV8 -j$(nproc)
```

**第三步**：安装与验证编译生成的wheel包

编译完成之后进入`Paddle/build/python/dist`目录即可找到编译生成的.whl安装包，安装与验证命令如下：

```bash
# 安装命令
python -m pip install -U paddlepaddle_npu-0.0.0-cp37-cp37m-linux_aarch64.whl

# 验证命令
python -c "import paddle; paddle.utils.run_check()"

# 预期得到类似以下结果：
Running verify PaddlePaddle program ...
PaddlePaddle works well on 1 NPU.
PaddlePaddle works well on 4 NPUs.
PaddlePaddle is installed successfully! Let's start deep learning with PaddlePaddle now.
```

## 如何卸载

请使用以下命令卸载Paddle:

```bash
pip uninstall paddlepaddle-npu
```
