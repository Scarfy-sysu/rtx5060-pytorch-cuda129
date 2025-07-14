# rtx5060-pytorch-cuda129
Run PyTorch with CUDA 12.9 on RTX 50 series (e.g. RTX 5060)
#  ⭐RTX 5060 成功运行 PyTorch Nightly + CUDA 12.9 的完整配置教程

本项目记录了在 Windows 系统中，使用 **NVIDIA GeForce RTX 5060 显卡** 成功运行 PyTorch 并开启 GPU 加速的过程。由于 RTX 50 系列显卡使用了 `sm_120` 架构，目前尚未被 PyTorch 稳定版支持，因此我们采用 **Nightly 开发版 + CUDA 12.9 运行库** 方式实现。

---

## 背景说明
### 为什么要用 Nightly
目前 PyTorch 稳定版（截至 2025 年 7 月）尚未支持 RTX 50 系列的 sm_120 架构，
导致用户即使拥有高性能显卡也无法正常启用 GPU 加速。

通过使用官方提供的 Nightly 版 + CUDA 12.9 的 pip 安装包，可以绕过稳定版限制，
在不安装 CUDA Toolkit、不编译源码的前提下，一行命令启用 RTX 5060 的 GPU 加速能力。



## 系统与环境信息


| 项目         | 配置                                  |
|--------------|---------------------------------------|
| 显卡         | NVIDIA GeForce RTX 5060               |
| 操作系统     | Windows 10 / 11                       |
| Anaconda 版本| Anaconda3 2025.06-0 (Windows x86_64)  |
| Python 版本  | 3.10（通过 Anaconda 安装）           |
| PyTorch 版本 | Nightly 版（2.9.0.dev + cu129）       |
| CUDA         | 使用 PyTorch 内置 CUDA 12.9 运行库，无需单独安装 CUDA Toolkit |

---

## 安装步骤

### 1️ 创建 Conda 虚拟环境

```bash
conda create -n torch5060 python=3.10 -y
conda activate torch5060
```

### 2 安装 PyTorch（Nightly + CUDA 12.9）

```bash
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu129
```

## 检验GPU是否可用

### 创建python脚本，使用以下代码：

```bash
import torch

print("PyTorch 版本:", torch.__version__)
print("CUDA 版本:", torch.version.cuda)
print("CUDA 是否可用:", torch.cuda.is_available())
if torch.cuda.is_available():
    print("GPU 名称:", torch.cuda.get_device_name(0))
else:
    print("GPU 不可用")
```

### 使用jupyter检测如下：

![jupyter检测截图](https://github.com/Scarfy-sysu/rtx5060-pytorch-cuda129/blob/main/5060jupyter.png?raw=true)
