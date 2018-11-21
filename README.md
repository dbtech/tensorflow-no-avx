

# Custom tensorflow build (Nov 21, 2018)

cat tensorflow* > tensorflow-1.12.0rc0.whl

**Motivation: [Request] Pre-build support old CPU #18689**

No custom build is available for my workstation which has a fairly recent GPU but an old CPU. According to the tensorflow project team a CPU without AVX will not be supported in the official tensorflow-gpu package any time in the future.

"Unfortunately we are unable to provide pre-built binaries without AVX. Unofficial third-party builds may be your best option."

I have built tensorflow from source without issues. It took about 3 hours. I have installed the wheel and tested the library in a keras framework. It works for me :)

**Target environment:**

Ubuntu 18.04.1 LTS (bionic)
Intel® Xeon(R) CPU W3520 @ 2.67GHz × 8
GeForce GTX 1050 Ti/PCIe/SSE2
CUDA 10.0
CUDNN 7.4.1

**Bazel build options:**

TF_NEED_OPENCL_SYCL="0"
TF_NEED_ROCM="0"
TF_NEED_CUDA="1"
CUDA_TOOLKIT_PATH="/usr/local/cuda"
TF_CUDA_VERSION="10.0"
CUDNN_INSTALL_PATH="/usr/lib/x86_64-linux-gnu"
TF_CUDNN_VERSION="7"
TF_NCCL_VERSION=""
TF_CUDA_COMPUTE_CAPABILITIES="6.1"
TF_CUDA_CLANG="0"
GCC_HOST_COMPILER_PATH="/usr/bin/x86_64-linux-gnu-gcc-6"
build --config=cuda
test --config=cuda
build:opt --copt=-march=native
build:opt --copt=-mssse3
build:opt --copt=-mcx16
build:opt --copt=-msse4.1
build:opt --copt=-msse4.2
build:opt --copt=-mpopcnt
build:opt --host_copt=-march=native
build:opt --define with_default_optimizations=true
build:v2 --define=tf_api_version=2
