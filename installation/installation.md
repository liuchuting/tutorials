# mindspore 安装指南

## 搭建ascend+mindspore开发环境需要四步
  1. 查ascend driver/firmware/cann与mindspore配套表
  2. 下载并安装ascend driver/firmware/cann toolkit
  3. 下载并安装mindspore
  4. 验证是否成功安装

### 第一步 查ascend driver/firmare/cann与mindspore配套表

| mindspore | ascend driver | firmware    | cann toolkit/kernel |
|:----------|:--------------|:------------|:--------------------|
| 2.3.1     | 24.1.RC2      | 7.3.0.1.231 | 8.0.RC2.beta1       |
| 2.3.0     | 24.1.RC2      | 7.3.0.1.231 | 8.0.RC2.beta1       |
| 2.2.10    | 23.0.3        | 7.1.0.5.220 | 7.0.0.beta1         |

- 温馨提示1: 请按照配套关系下载安装对应的版本，很多算法开发遇到的问题都来自于环境配置安装，请一定参考以上的配套关系表。
- 温馨提示2: 从硬件适配度和特性方面考虑，建议使用最新的2.3.0/2.3.1版本进行算法开发，有问题请到gitee提issue，https://gitee.com/mindspore/mindspore/issues

### 第二步 下载并安装ascend driver/firmware/cann toolkit

Ascend的driver/firmware与cann软件有两套版本系列，一个是商用版本，一个是社区版本。以下例子均来自于社区版本。

#### 下载

硬件以atlas 800T A2训练服务器 aarch64 架构为例，下面表格是对应的版本run包下载方式，请根据实际架构和 platform 选择对应的run包。

- mindspore 2.3.1 & mindspore 2.3.0

| ascend software          | platform  | version         | package name                                          | download                                                                                                                                                                                                        | release date  | 
|:-------------------------|:----------|:----------------|:------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------|
| ascend driver            | 910A      | 24.1.RC2        | Ascend-hdk-910-npu-driver_24.1.rc2_linux-aarch64.run  | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2024.1.RC2/Ascend-hdk-910-npu-driver_24.1.rc2_linux-aarch64.run?response-content-type=application/octet-stream)   | 2024-07-31    |
| ascend driver            | 910*      | 24.1.RC2        | Ascend-hdk-910b-npu-driver_24.1.rc2_linux-aarch64.run | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2024.1.RC2/Ascend-hdk-910b-npu-driver_24.1.rc2_linux-aarch64.run?response-content-type=application/octet-stream)  | 2024-07-31    |
| ascend firmware          | 910A      | 7.3.0.1.231     | Ascend-hdk-910-npu-firmware_7.3.0.1.231.run           | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2024.1.RC2/Ascend-hdk-910-npu-firmware_7.3.0.1.231.run?response-content-type=application/octet-stream)            | 2024-07-31    |
| ascend firmware          | 910*      | 7.3.0.1.231     | Ascend-hdk-910b-npu-firmware_7.3.0.1.231.run          | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2024.1.RC2/Ascend-hdk-910b-npu-firmware_7.3.0.1.231.run?response-content-type=application/octet-stream)           | 2024-07-31    |
| cann toolkit             | 910A/910* | 8.0.RC2.beta1   | Ascend-cann-toolkit_8.0.RC2_linux-aarch64.run         | [download page](https://www.hiascend.com/developer/download/community/result?module=cann&cann=8.0.RC2.beta1)                                                                                                    | 2024-07-17    |
| cann kernel              | 910A      | 8.0.RC2.beta1   | Ascend-cann-kernels-910_8.0.RC2_linux.run             | [download page](https://www.hiascend.com/developer/download/community/result?module=cann&cann=8.0.RC2.beta1)                                                                                                    | 2024-07-17    |
| cann kernel              | 910*      | 8.0.RC2.beta1   | Ascend-cann-kernels-910b_8.0.RC2_linux.run            | [download page](https://www.hiascend.com/developer/download/community/result?module=cann&cann=8.0.RC2.beta1)                                                                                                    | 2024-07-17    |

- mindspore 2.2.10

| ascend software          | platform  | version     | package name                                        | download                                                                                                                                                                                                   | release date | 
|:-------------------------|-----------|:------------|:----------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------|
| ascend driver            | 910A      | 23.0.3      | Ascend-hdk-910-npu-driver_23.0.3_linux-aarch64.run  | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2023.0.3/Ascend-hdk-910-npu-driver_23.0.3_linux-aarch64.run?response-content-type=application/octet-stream)  | 2024/03/11   |
| ascend driver            | 910*      | 23.0.3      | Ascend-hdk-910b-npu-driver_23.0.3_linux-aarch64.run | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2023.0.3/Ascend-hdk-910b-npu-driver_23.0.3_linux-aarch64.run?response-content-type=application/octet-stream) | 2024/03/11   |
| ascend firmware          | 910A      | 7.1.0.5.220 | Ascend-hdk-910-npu-firmware_7.1.0.5.220.run         | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2023.0.3/Ascend-hdk-910-npu-firmware_7.1.0.5.220.run?response-content-type=application/octet-stream )        | 2024/03/11   |
| ascend firmware          | 910*      | 7.1.0.5.220 | Ascend-hdk-910b-npu-firmware_7.1.0.5.220.run        | [download link](https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Ascend%20HDK/Ascend%20HDK%2023.0.3/Ascend-hdk-910b-npu-firmware_7.1.0.5.220.run?response-content-type=application/octet-stream)        | 2024/03/11   |
| cann toolkit             | 910A/910* | 7.0.0.beta1 | Ascend-cann-toolkit_7.0.0_linux-aarch64.run         | [download page](https://www.hiascend.com/developer/download/community/result?module=cann&cann=7.0.0.beta1)                                                                                                 | 2024/01/05   |
| cann kernel              | 910A      | 7.0.0.beta1 | Ascend-cann-kernels-910_7.0.0_linux.run             | [download page](https://www.hiascend.com/developer/download/community/result?module=cann&cann=7.0.0.beta1)                                                                                                 | 2024/01/05   |
| cann kernel              | 910*      | 7.0.0.beta1 | Ascend-cann-kernels-910b_7.0.0_linux.run            | [download page](https://www.hiascend.com/developer/download/community/result?module=cann&cann=7.0.0.beta1)                                                                                                 | 2024/01/05   |

> driver和firmware的download link放的是run包下载地址，点击即可下载，cann toolkit和 kernel放的是download page，需要进入页面后，注册登陆账号才可下载。
> 想了解更多ascend cann信息，请查看https://www.hiascend.com/developer/download/community/result

#### 安装

下面以 aarch64 架构 910* 服务器安装mindspore2.3.0版本配套run包为例：

1、安装driver和firmware

```bash
# 安装driver 
./Ascend-hdk-910b-npu-driver_24.1.rc2_linux-aarch64.run --full --install-for-all

# 查看NPU卡信息
npu-smi info

# 查看安装driver的版本号，显示24.1.rc2
cat /usr/local/Ascend/driver/version.info

# 安装NPU firmware
./Ascend-hdk-910b-npu-firmware_7.3.0.1.231.run --full

# 查看安装firmware的版本号，显示 7.3.0.1.231
cat /usr/local/Ascend/firmware/version.info


# 重启OS
reboot
```

2、安装cann

```bash

# 安装 cann toolkit
./Ascend-cann-toolkit_8.0.RC2_linux-aarch64.run --install --install-for-all --quiet

# 安装二进制算子包cann-kernel
./Ascend-cann-kernels-910b_8.0.RC2_linux.run --install --install-for-all --quiet

# 然后执行如下命令配置环境变量
source /usr/local/Ascend/ascend-toolkit/set_env.sh

# 查看cann 版本号
cat /usr/local/Ascend/ascend-toolkit/latest/version.cfg  
# 将会显示7.3.0.1.231:8.0.RC2 -> 7.3.0.1.231是firmware版本号, 8.0.RC2是cann tooklit版本号
```

3、安装sympy/hccl/te

```bash
pip install sympy
pip install /usr/local/Ascend/ascend-toolkit/latest/lib64/te-*-py3-none-any.whl
pip install /usr/local/Ascend/ascend-toolkit/latest/lib64/hccl-*-py3-none-any.whl
```

### 第三步 下载并安装mindspore

mindspore的whl包有两种安装方式：
1. 直接pip install mindspore==2.3.1 or pip install mindspore==2.3.0（自动根据系统python版本和cpu架构安装相应的whl包） 
2. 手动选择python版本和cpu架构相对应的whl包，下载和安装。

- mindspore 2.3.1 

| python |   os    |   cpu   | mindspore whl                                                                                                                                                                      | 
|:------:|:-------:|:-------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  3.8   |  linux  | aarch64 | [mindspore-2.3.1-cp38-cp38-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.1/MindSpore/unified/aarch64/mindspore-2.3.1-cp38-cp38-linux_aarch64.whl)     |
|  3.9   |  linux  | aarch64 | [mindspore-2.3.1-cp39-cp39-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.1/MindSpore/unified/aarch64/mindspore-2.3.1-cp39-cp39-linux_aarch64.whl)     |
|  3.10  |  linux  | aarch64 | [mindspore-2.3.1-cp310-cp310-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.1/MindSpore/unified/aarch64/mindspore-2.3.1-cp310-cp310-linux_aarch64.whl) |
|  3.8   |  linux  | x86_64  | [mindspore-2.3.1-cp38-cp38-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.1/MindSpore/unified/x86_64/mindspore-2.3.1-cp38-cp38-linux_x86_64.whl)        |
|  3.9   |  linux  | x86_64  | [mindspore-2.3.1-cp39-cp39-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.1/MindSpore/unified/x86_64/mindspore-2.3.1-cp39-cp39-linux_x86_64.whl)        |
|  3.10  |  linux  | x86_64  | [mindspore-2.3.1-cp310-cp310-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.1/MindSpore/unified/x86_64/mindspore-2.3.1-cp310-cp310-linux_x86_64.whl)    |

- mindspore 2.3.0 

| python |  os   |   cpu   | mindspore whl                                                                                                                                                                      | 
|:------:|:-----:|:-------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  3.8   | linux | aarch64 | [mindspore-2.3.0-cp38-cp38-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.0/MindSpore/unified/aarch64/mindspore-2.3.0-cp38-cp38-linux_aarch64.whl)     |
|  3.9   | linux | aarch64 | [mindspore-2.3.0-cp39-cp39-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.0/MindSpore/unified/aarch64/mindspore-2.3.0-cp39-cp39-linux_aarch64.whl)     |
|  3.10  | linux | aarch64 | [mindspore-2.3.0-cp310-cp310-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.0/MindSpore/unified/aarch64/mindspore-2.3.0-cp310-cp310-linux_aarch64.whl) |
|  3.8   | linux | x86_64  | [mindspore-2.3.0-cp38-cp38-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.0/MindSpore/unified/x86_64/mindspore-2.3.0-cp38-cp38-linux_x86_64.whl)        |
|  3.9   | linux | x86_64  | [mindspore-2.3.0-cp39-cp39-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.0/MindSpore/unified/x86_64/mindspore-2.3.0-cp39-cp39-linux_x86_64.whl)        |
|  3.10  | linux | x86_64  | [mindspore-2.3.0-cp310-cp310-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.3.0/MindSpore/unified/x86_64/mindspore-2.3.0-cp310-cp310-linux_x86_64.whl)    |

- mindspore 2.2.10

| python |  os   |   cpu   | mindspore whl                                                                                                                                                                       | 
|:------:|:-----:|:-------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  3.7   | linux | aarch64 | [mindspore-2.2.10-cp37-cp37m-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.10/MindSpore/unified/aarch64/mindspore-2.2.10-cp37-cp37m-linux_aarch64.whl) |
|  3.8   | linux | aarch64 | [mindspore-2.2.10-cp38-cp38-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.10/MindSpore/unified/aarch64/mindspore-2.2.10-cp38-cp38-linux_aarch64.whl)   |
|  3.9   | linux | aarch64 | [mindspore-2.2.10-cp39-cp39-linux_aarch64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.10/MindSpore/unified/aarch64/mindspore-2.2.10-cp39-cp39-linux_aarch64.whl)   |
|  3.7   | linux | x86_64  | [mindspore-2.2.10-cp37-cp37m-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.10/MindSpore/unified/x86_64/mindspore-2.2.10-cp37-cp37m-linux_x86_64.whl)    |
|  3.8   | linux | x86_64  | [mindspore-2.2.10-cp38-cp38-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.10/MindSpore/unified/x86_64/mindspore-2.2.10-cp38-cp38-linux_x86_64.whl)      |
|  3.9   | linux | x86_64  | [mindspore-2.2.10-cp39-cp39-linux_x86_64.whl](https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.10/MindSpore/unified/x86_64/mindspore-2.2.10-cp39-cp39-linux_x86_64.whl)      |

### 第四步 验证是否成功安装

```bash
python -c "import mindspore;mindspore.set_context(device_target='Ascend');mindspore.run_check()"
```

如果输出:

```shell
MindSpore version: 版本号
The result of multiplication calculation is correct, MindSpore has been installed on platform [Ascend] successfully!
```

说明MindSpore安装成功了。