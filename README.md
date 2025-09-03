# PP-OCRv5_AMD-ROCm


## Introduction
PP-OCRv5-AMD-ROCm is a demo to show how to use the AMD GPU(whatever the iGPU or dGPU) to do Baidu Paddleocr model inference.(https://github.com/PaddlePaddle/PaddleOCR)


## Installation
The most necessary dependencies for deploying onnx model on AMD GPU are:
    ROCm
    ROCm-onnxruntime

1, Get the onnx model, please follow the steps in "How to export PP-OCRv5 model.md" to obtain the onnx models.

2, Please note the IR version of the onnx model, which will determine which verion of ROCm needs to be installed.
<div style="text-align: center">
    <image src = "./images/onnx-version.png">
</div>

3, For example, if the onnx IR version is 10, go to the link https://repo.radeon.com/rocm/manylinux/ . Will see all the ROCm versions.
<div style="text-align: center">
    <image src = "./images/rocm-rel-version.png">
</div>

4, When enter a link, can see the onnxruntime version supported by the ROCm. And the onnx model IR is 10, i select the rocm-rel-6.4.3 which can support onnxruntime_rocm-1.21.0, and onnxruntime 1.21.0 can support onnx IR 10.
<div style="text-align: center">
    <image src = "./images/onnx-runtime.png">
</div>

5, Now we know which ROCm and Onnxruntime-ROCm version should be installed.

6, Install ROCm, follow the link https://rocm.docs.amd.com/projects/install-on-linux/en/latest/install/quick-start.html to install the ROCm. We need to change the url https://repo.radeon.com/amdgpu-install/6.4.3/ubuntu/jammy/amdgpu-install_6.4.60403-1_all.deb to install the ROCm you want.
<div style="text-align: center">
    <image src = "./images/rocm-version.png">
</div>

7, If you are using AMD Ryzen CPU and want to use the iGPU to do inference, need to set a environment variable and the value of variable is based on the iGPU architecture. If you are using Ryzen 8000 or HX 300 series CPU, your iGPU architecture is RDNA3, you need to do "export HSA_OVERRIDE_GFX_VERISON=11.0.0". This step is important, you iGPU can support Pytorch and other AI framework by doing this.

<div style="text-align: center">
    <image src = "./images/HSA.png">
</div>

8, Install the onnxruntime-rocm. pip3 install onnxruntime-rocm -f https://repo.radeon.com/rocm/manylinux/rocm-rel-x.x.x/ Set the url based the ROCm verison installed. Please refer to this link https://rocm.docs.amd.com/projects/radeon/en/latest/docs/install/native_linux/install-onnx.html

9, Finally, you can inference the PaddleOCR models on your AMD iGPU or dGPU.
use GPU:
python main.py --image_dir images/paddleocr_structure.png --det_model_dir ../PP-OCRv5_server_det_infer/inference.onnx --det_model_device GPU --rec_model_dir ../PP-OCRv5_server_rec_infer/inference.onnx --rec_model_device GPU

use CPU:
python main.py --image_dir images/paddleocr_structure.png --det_model_dir ../PP-OCRv5_server_det_infer/inference.onnx --det_model_device CPU --rec_model_dir ../PP-OCRv5_server_rec_infer/inference.onnx --rec_model_device CPU
<div style="text-align: center">
    <image src = "./images/GPU-usage.png">
</div>
