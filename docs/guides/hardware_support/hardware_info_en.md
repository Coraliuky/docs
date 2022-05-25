# List of Hardware Supported by PaddlePaddle's Products

The information of the hardware supported by products of PaddlePaddle is as follows:

## PaddlePaddle

|  Class  | Architecture | Company | Product Model | Installation | Source-Code Compilation |  Whether the Training is Fully Supported | Whether Some Models are Supported |
|  ----  | ----  | ---- | ---- |---- | ---- |---- | ---- |
| Server-Side CPU | x86 | Intel | Common CPU models include Xeon and Core series| [Installation](https://www.paddlepaddle.org.cn/install/quick?docurl=/documentation/docs/zh/install/pip/linux-pip.html) | [Source-Code Compilation](https://www.paddlepaddle.org.cn/install/quick?docurl=/documentation/docs/zh/install/compile/linux-compile.html) | ✔️ |  |
| Server-Side GPU |  | NVIDIA | Common GPU models include V100 and T4| [Installation](https://www.paddlepaddle.org.cn/install/quick?docurl=/documentation/docs/zh/install/pip/linux-pip.html) | [Source-Code Compilation](https://www.paddlepaddle.org.cn/install/quick?docurl=/documentation/docs/zh/install/compile/linux-compile.html) | ✔️ |  |
| AI Acceleration Chip | DaVinci | Huawei | Ascend 910 | [Installation](./npu_docs/paddle_install_cn.html) | [Source-Code Compilation](./npu_docs/paddle_install_cn.html#anzhuangfangshi-tongguoyuanmabianyianzhuang) | | ✔️ |
| AI Acceleration Chip |  | Hygon | Hygon DCU | [Installation](./rocm_docs/paddle_install_cn.html#wheel) | [Source-Code Compilation](./rocm_docs/paddle_install_cn.html#anzhuangfangshier-tongguoyuanmabianyianzhuang) | ✔️ | [Supported Models](./rocm_docs/paddle_rocm_cn.html) |
| AI Acceleration Chip | XPU | Baidu | Kunlun K200, R200, and so on | [Installation](./xpu_docs/paddle_install_xpu2_cn.html#wheel) | [Source-Code Compilation](./xpu_docs/paddle_install_xpu2_cn.html#xpu) |  | [Supported Models](./xpu_docs/paddle_2.0_xpu2_cn.html) |
| AI Acceleration Chip | IPU | Graphcore | GC200 | | [Source-Code Compilation](./ipu_docs/paddle_install_cn.html) |  | |

## Paddle Inference

|  Class  | Architecture | Company | Product Model | Pre-Compiled Library | Source-Code Compilation |  Whether the Inference is fully supported | Whether Some Models are Supported |
|  ----  | ----  | ---- | ---- |---- | ---- |---- | ---- |
| Server-Side CPU | x86 | Intel | Common CPU models include Xeon and Core series | [Pre-Compiled Library](https://paddleinference.paddlepaddle.org.cn/user_guides/download_lib.html) | [Source-Code Compilation](https://paddleinference.paddlepaddle.org.cn/user_guides/source_compile.html) | ✔️ |   |
| Server-Side GPU |  | NVIDIA | Common GPU models include V100 and T4 | [Pre-Compiled Library](https://paddleinference.paddlepaddle.org.cn/user_guides/download_lib.html) | [Source-Code Compilation](https://paddleinference.paddlepaddle.org.cn/user_guides/source_compile.html) | ✔️ |   |
| Mobile GPU |  | NVIDIA | Jetson Series| [Pre-Compiled Library](https://paddleinference.paddlepaddle.org.cn/user_guides/download_lib.html) | [Source-Code Compilation](https://paddleinference.paddlepaddle.org.cn/user_guides/source_compile.html) | ✔️ |   |
| AI Acceleration Chip | DaVinci | Huawei | Ascend 910 | Available soon | | | |
| AI Acceleration Chip |  | Hygon | Hygon DCU | [Pre-Compiled Library](./rocm_docs/paddle_install_cn.html) | [Source-Code Compilation](./rocm_docs/paddle_install_cn.html) | ✔️ | [Supported Models](./rocm_docs/paddle_rocm_cn.html) |
| AI Acceleration Chip | XPU | Baidu | Kunlun K200, R200, and so on | [Pre-Compiled Library](./xpu_docs/inference_install_example_cn.html#wheel) | [Source-Code Compilation](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/guides/09_hardware_support/xpu_docs/paddle_install_cn.html#id2) |  | [Supported Models](./xpu_docs/paddle_2.0_xpu_cn.html#xunlianzhichi) |
| Server-Side CPU | ARM | Phytium | FT-2000+/64、S2500 |  |[Source-Code Compilation](../../install/compile/arm-compile.html#anchor-1) |  |  |
| Server-Side CPU | ARM | Huawei | Kunpeng 920 2426SK |  |[Source-Code Compilation](../../install/compile/arm-compile.html) |  |   |
| Server-Side CPU | MIPS | Loongson | Loongson 3A4000、3A5000、3C5000L |  |[Source-Code Compilation](../../install/compile/mips-compile.html#anchor-0) |  |  |
| Server-Side CPU | x86 | Zhaoxin | All CPUs |  |[Source-Code Compilation](../../install/compile/zhaoxin-compile.html#anchor-1) |  |  |

## Paddle Lite

|  Class  | Architecture | Company | Model | Pre-Compiled Library | Source-Code Compilation |  Whether the Inference is Fully Supported | Whether Some Models are Supported |
|  ----  | ----  | ---- | ---- |---- | ---- |---- | ---- |
| Mobile CPU | ARM | ARM | Cortex-A Series | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/quick_start/release_lib.html) | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/source_compile/compile_env.html) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/introduction/support_model_list.html) |
| Mobile GPU |  | ARM | Mali Series |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/opencl.html) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/introduction/support_model_list.html) |
| Mobile GPU |  | Qualcomm | Adreno Series |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/opencl.html) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/introduction/support_model_list.html) |
| AI Acceleration Chip |  | Huawei | Kirin 810/990/9000 |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/huawei_kirin_npu.html#id5) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/demo_guides/huawei_kirin_npu.html#id1) |
| AI Acceleration Chip |  | Huawei | Ascend 310 |  | Available Soon |  |  |
| AI Acceleration Chip |  | RockChip | RK1808 |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/rockchip_npu.html#id5) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/demo_guides/rockchip_npu.html#id1) |
| AI Acceleration Chip |  | MTK | NeuroPilot APU |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/mediatek_apu.html#id1) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/demo_guides/mediatek_apu.html#id1) |
| AI Acceleration Chip |  | Imagination | PowerVR 2NX |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/huawei_kirin_npu.html#id5) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/demo_guides/huawei_kirin_npu.html#id1) |
| AI Acceleration Chip |  | Baidu | Kunlun K200, R200, and so on |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/baidu_xpu.html#id4) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/demo_guides/baidu_xpu.html#id1) |
| AI Acceleration Chip |  | Cambricon | Siyuan 270 |  | Available Soon |   |   |
| AI Acceleration Chip |  | Bitmain | Sophon BM16 Series |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/bitmain.html#id5) |  | [Supported Models](https://paddlelite.paddlepaddle.org.cn/demo_guides/bitmain.html#id1) |
| FPGA |  | Baidu | Baidu Edgeboard |  | [Source-Code Compilation](https://paddlelite.paddlepaddle.org.cn/demo_guides/baidu_xpu.html#id4) |  | [Supported Models](https://ai.baidu.com/ai-doc/HWCE/Qkda68drw) |

**Attention:** If you want to know more about chip support, please contact us. And our e-mail address is Paddle-better@baidu.com.
