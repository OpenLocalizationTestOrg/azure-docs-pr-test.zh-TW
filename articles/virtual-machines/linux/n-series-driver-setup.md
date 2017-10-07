---
title: "aaaAzure N 序列驅動程式安裝程式，適用於 Linux |Microsoft 文件"
description: "如何 tooset 向上 N 系列 Vm 在 Azure 中執行 Linux 的 NVIDIA GPU 驅動程式"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>在執行 Linux 的 N 系列 VM 上安裝 NVIDIA GPU 驅動程式

tootake 利用 Azure N 數列的 hello GPU 功能執行 Linux Vm，安裝支援 NVIDIA 圖形驅動程式。 本文提供您在部署 N 系列 VM 後的驅動程式安裝步驟。 驅動程式設定資訊也適用於 [Windows VM](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。


如需 N 系列 VM 規格、儲存體容量與磁碟的詳細資料，請參閱 [GPU Linux VM 大小](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>安裝 NV VM 的 GRID 驅動程式

tooinstall NVIDIA 方格驅動程式 NV Vm 上的進行 SSH 連線 tooeach VM，並遵循您的 Linux 散發 hello 步驟。 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. 執行 hello`lspci`命令。 請確認 hello NVIDIA M60 卡可以顯示為 PCI 裝置。

2. 安裝更新。

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. 停用 hello Nouveau 核心驅動程式，也就是與 hello NVIDIA 驅動程式不相容。 （僅使用 hello NVIDIA 驅動程式 NV Vm 上）。toodo，建立一個檔案中的`/etc/modprobe.d `名為`nouveau.conf`以 hello 下列內容：

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. 重新啟動 hello VM，並重新連線。 結束 X 伺服器：

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. 下載並安裝 hello 方格驅動程式：

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. 當詢問您是否想 toorun hello nvidia xconfig 公用程式 tooupdate X 組態檔時，選取**是**。

7. 安裝完成之後，請複製 /etc/nvidia/gridd.conf.template tooa 新檔案 gridd.conf 在位置 /etc/nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Hello 太之後加入`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Hello VM 重新開機，然後繼續 tooverify hello 安裝。


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>以 CentOS 作為基礎的 7.3 或 Red Hat Enterprise Linux 7.3


1. 更新 hello 核心和 DKMS。
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. 停用 hello Nouveau 核心驅動程式，也就是與 hello NVIDIA 驅動程式不相容。 （僅使用 hello NVIDIA 驅動程式 NV Vm 上）。toodo，建立一個檔案中的`/etc/modprobe.d `名為`nouveau.conf`以 hello 下列內容：

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Hello VM 重新開機，請重新連線，並安裝 hello Hyper-v： 最新的 Linux Integration Services
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. 重新連線 toohello VM 以及執行 hello`lspci`命令。 請確認 hello NVIDIA M60 卡可以顯示為 PCI 裝置。
 
5. 下載並安裝 hello 方格驅動程式：

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. 當詢問您是否想 toorun hello nvidia xconfig 公用程式 tooupdate X 組態檔時，選取**是**。

7. 安裝完成之後，請複製 /etc/nvidia/gridd.conf.template tooa 新檔案 gridd.conf 在位置 /etc/nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Hello 太之後加入`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Hello VM 重新開機，然後繼續 tooverify hello 安裝。

### <a name="verify-driver-installation"></a>確認驅動程式安裝


tooquery hello GPU 裝置狀態、 SSH toohello VM 和執行的 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface)與 hello 驅動程式一起安裝的命令列公用程式。 

此時會出現類似 toohello 下列輸出：

![NVIDIA 裝置狀態](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>X11 伺服器
如果您需要 X11 伺服器進行遠端連線 tooan NV VM [x11vnc](http://www.karlrunge.com/x11vnc/)建議使用，因為它可讓硬體加速的圖形。 hello BusID 的 hello M60 裝置必須手動新增 toohello xconfig 檔案 (`etc/X11/xorg.conf`上 Ubuntu 16.04 LTS、 `/etc/X11/XF86config` CentOS 7.3 或 Red Hat Enterprise Server 7.3 上)。 新增`"Device"`區段類似 toohello 下列：
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
此外，更新您`"Screen"`區段 toouse 此裝置。
 
可以找到 hello BusID 執行

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
取得重新配置 VM，或重新啟動時，可以變更 hello BusID。 因此，您可能想 toouse hello X11 組態指令碼 tooupdate hello BusID 時重新啟動 VM。 例如：

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

可以叫用這個檔案作為開機時的根目錄，方法是在 `/etc/rc.d/rc3.d` 中為其建立項目。


## <a name="install-cuda-drivers-for-nc-vms"></a>安裝適用於 NC VM 的 CUDA 驅動程式

以下是 Linux NC Vm 從 hello NVIDIA CUDA Toolkit 8.0 步驟 tooinstall NVIDIA 驅動程式。 

C 和 c + + 開發人員可以選擇性地安裝 hello 完整 Toolkit toobuild GPU 加速應用程式。 如需詳細資訊，請參閱 hello [CUDA 安裝指南](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)。


> [!NOTE]
> 這裡所提供的 CUDA 驅動程式下載連結，為發行當時的最新驅動程式。 Hello 最新 CUDA 驅動程式，請造訪 hello [NVIDIA](http://www.nvidia.com/)網站。
>

tooinstall CUDA Toolkit 進行的 SSH 連線 tooeach VM。 hello 系統的 tooverify 具有 CUDA 能夠 GPU，執行下列命令的 hello:

```bash
lspci | grep -i NVIDIA
```
您會看到下列範例 （顯示 NVIDIA Tesla K80 卡） 的輸出類似 toohello:

![lspci 命令輸出](./media/n-series-driver-setup/lspci.png)

然後執行您的配送映像特有的安裝命令。

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. 下載並安裝 hello CUDA 驅動程式。
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  hello 安裝可能需要幾分鐘的時間。

2. toooptionally 安裝 hello 完成 CUDA 工具組，類型：

  ```bash
  sudo apt-get install cuda
  ```

3. Hello VM 重新開機，然後繼續 tooverify hello 安裝。

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>以 CentOS 作為基礎的 7.3 或 Red Hat Enterprise Linux 7.3

1. 取得更新。 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. 重新連線 toohello VM，然後安裝 hello 最新的 HYPER-V 的 Linux Integration Services。

  > [!IMPORTANT]
  > 如果您 NC24r VM 上安裝的 CentOS 架構 HPC 映像，請略過 tooStep 3。 因為 hello 映像中預先安裝 Azure RDMA 驅動程式及 Linux Integration Services，LIS 應該不會進行升級，並依預設會停用核心更新。
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. 重新連線 toohello VM 並繼續安裝以 hello 下列命令：

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  hello 安裝可能需要幾分鐘的時間。 

4. toooptionally 安裝 hello 完成 CUDA 工具組，類型：

  ```bash
  sudo yum install cuda
  ```

5. Hello VM 重新開機，然後繼續 tooverify hello 安裝。


### <a name="verify-driver-installation"></a>確認驅動程式安裝


tooquery hello GPU 裝置狀態、 SSH toohello VM 和執行的 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface)與 hello 驅動程式一起安裝的命令列公用程式。 

此時會出現類似 toohello 下列輸出：

![NVIDIA 裝置狀態](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>CUDA 驅動程式更新

我們建議您在部署後定期更新 CUDA 驅動程式。

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>以 CentOS 作為基礎的 7.3 或 Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>疑難排解

* 沒有 CUDA Ubuntu 16.04 LTS 上執行 hello 4.4.0-75 Linux 核心 Azure N 系列 Vm 上的驅動程式的已知的問題。 如果您要從較早的核心版本升級，升級 tooat 最低核心版本 4.4.0-77。 



## <a name="next-steps"></a>後續步驟

* 在 hello N 系列 Vm 上 hello NVIDIA Gpu 的相關資訊，請參閱：
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (適用於 Azure NC VM)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (適用於 Azure NV VM)

* toocapture Linux VM 映像與安裝的 NVIDIA 驅動程式，請參閱[如何 toogeneralize 和擷取 Linux 虛擬機器](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
