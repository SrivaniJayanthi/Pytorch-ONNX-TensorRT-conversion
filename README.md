# Versions:
Python - 3.11.8 <br>
Cuda -  12.4 <br>
Pytorch - 2.5.1+cu124 (version 2.5.1 with compatibilty for 12.4 cuda version) <br>
ONNX - 1.13.0 (This version is compatible with python 3.11) <br>
TensorRT - 10.5.0 <br>
CMake - 3.31.0
Windows 11 64 bit architecture
VS Code - 1.96.2
# Installation:
## Cuda:
Installation link - [Cuda](https://developer.nvidia.com/cuda-12-4-0-download-archive?target_os=Windows&target_arch=x86_64&target_version=11&target_type=exe_local) <br>
Installation guide - [guide](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html)

## Pytorch:
Installation link - [Pytorch](https://pytorch.org/get-started/locally/)
Command - pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124

## CMake:
Use this video to install and integrate CMake with VS Code: [CMake with VS Code](https://www.youtube.com/watch?v=_BWU5mWqVA4&pp=ygUlY21ha2UgaW5zdGFsbCBpbiB3aW5kb3dzIHdpdGggdnMgY29kZQ%3D%3D)

## ONNX:
CMake is necessary for ONNX, so make sure you install CMake in your PC and integrate it with VS Code. <br>

To install ONNX: <br>
Step 1 - Clone the Protobuf repository: <br>
git clone https://github.com/protocolbuffers/protobuf.git <br>
cd protobuf <br>
git checkout v21.12 <br>

Step 2 - Build Protobuf: <br>
Navigate to the cmake directory in the protobuf repository - cd cmake <br>
Run CMake to configure the build system for Visual Studio - cmake -G "Visual Studio 16 2019" -A x64 -DCMAKE_INSTALL_PREFIX=<protobuf_install_dir> -Dprotobuf_MSVC_STATIC_RUNTIME=OFF -Dprotobuf_BUILD_SHARED_LIBS=OFF -Dprotobuf_BUILD_TESTS=OFF -Dprotobuf_BUILD_EXAMPLES=OFF . <br>
Replace <protobuf_install_dir> with the directory where you want to install Protobuf (e.g., C:\protobuf). <br>
Build the Protobuf library - msbuild protobuf.sln /m /p:Configuration=Release <br>
After the build completes, install Protobuf - msbuild INSTALL.vcxproj /p:Configuration=Release <br>
This installs Protobuf to the specified directory (<protobuf_install_dir>). Don't forget to add the bin directory (which contains protoc.exe) to your PATH. <br>

Step 3 - Update your PATH: <br>
To use protoc.exe globally, add the bin directory of your Protobuf installation to your PATH environment variable. You can do this with the following command - set CMAKE_PREFIX_PATH=<protobuf_install_dir>;%CMAKE_PREFIX_PATH% <br>

Step 4 - Clone the ONNX repository: <br>
git clone https://github.com/onnx/onnx.git <br>
cd onnx <br>
git checkout v1.13.0 <br>
git submodule update --init --recursive <br>
set CMAKE_ARGS=-DONNX_USE_LITE_PROTO=ON <br>
cmake -G "Visual Studio 16 2019" -A x64 -DCMAKE_PREFIX_PATH=<protobuf_install_dir> %CMAKE_ARGS% . <br>
pip install -e . -v <br>

Step 5 - Verify ONNX Installation: <br>
import onnx <br>
print(onnx.__version__) <br>














