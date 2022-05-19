# Example of Paddle IPU inference

The Paddle IPU supports the original inference library of PaddlePaddle—Paddle Inference)，which is applicable to cloud inference.

## Example of C++ inference

**Step 1**：Compile the source code of a C++ inference library

Currently the Paddle IPU can only offer a C++ inference library through compiling the source code. To prepare the compilation environment, please refer to [instruction of the Paddle IPU installation](./paddle_install_cn.html)。

```
# Download the source code
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle

# Build the compilation directory
mkdir build && cd build

# Execute CMake，and open the inference optimization option ON_INFER
cmake .. -DWITH_IPU=ON -DWITH_PYTHON=ON -DPY_VERSION=3.7 -DWITH_MKL=ON -DON_INFER=ON \
         -DPOPLAR_DIR=/opt/poplar -DPOPART_DIR=/opt/popart -DCMAKE_BUILD_TYPE=Release

# Perform compilation
make -j$(nproc)
```

After the compilation is done, the C++ inference library will be stored in `build/paddle_inference_install_dir`.

**Step 2**：Acquire the demo code of inference, compile and run it

```
# Acquire the demo code
git clone https://github.com/PaddlePaddle/Paddle-Inference-Demo
```

Rename the C++ inference library and copy it to `Paddle-Inference-Demo/c++/lib/paddle_inference`.

```
cd Paddle-Inference-Demo/c++/paddle-ipu

# Peform compilation
bash ./compile.sh

# Perform execution
bash ./run.sh
```
