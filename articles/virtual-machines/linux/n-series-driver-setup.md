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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="4d16d-103">在執行 Linux 的 N 系列 VM 上安裝 NVIDIA GPU 驅動程式</span><span class="sxs-lookup"><span data-stu-id="4d16d-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="4d16d-104">tootake 利用 Azure N 數列的 hello GPU 功能執行 Linux Vm，安裝支援 NVIDIA 圖形驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="4d16d-105">本文提供您在部署 N 系列 VM 後的驅動程式安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="4d16d-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="4d16d-106">驅動程式設定資訊也適用於 [Windows VM](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4d16d-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="4d16d-107">如需 N 系列 VM 規格、儲存體容量與磁碟的詳細資料，請參閱 [GPU Linux VM 大小](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4d16d-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="4d16d-108">安裝 NV VM 的 GRID 驅動程式</span><span class="sxs-lookup"><span data-stu-id="4d16d-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="4d16d-109">tooinstall NVIDIA 方格驅動程式 NV Vm 上的進行 SSH 連線 tooeach VM，並遵循您的 Linux 散發 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="4d16d-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="4d16d-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4d16d-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="4d16d-111">執行 hello`lspci`命令。</span><span class="sxs-lookup"><span data-stu-id="4d16d-111">Run hello `lspci` command.</span></span> <span data-ttu-id="4d16d-112">請確認 hello NVIDIA M60 卡可以顯示為 PCI 裝置。</span><span class="sxs-lookup"><span data-stu-id="4d16d-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="4d16d-113">安裝更新。</span><span class="sxs-lookup"><span data-stu-id="4d16d-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="4d16d-114">停用 hello Nouveau 核心驅動程式，也就是與 hello NVIDIA 驅動程式不相容。</span><span class="sxs-lookup"><span data-stu-id="4d16d-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="4d16d-115">（僅使用 hello NVIDIA 驅動程式 NV Vm 上）。toodo，建立一個檔案中的`/etc/modprobe.d `名為`nouveau.conf`以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="4d16d-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="4d16d-116">重新啟動 hello VM，並重新連線。</span><span class="sxs-lookup"><span data-stu-id="4d16d-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="4d16d-117">結束 X 伺服器：</span><span class="sxs-lookup"><span data-stu-id="4d16d-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="4d16d-118">下載並安裝 hello 方格驅動程式：</span><span class="sxs-lookup"><span data-stu-id="4d16d-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="4d16d-119">當詢問您是否想 toorun hello nvidia xconfig 公用程式 tooupdate X 組態檔時，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="4d16d-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="4d16d-120">安裝完成之後，請複製 /etc/nvidia/gridd.conf.template tooa 新檔案 gridd.conf 在位置 /etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="4d16d-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="4d16d-121">Hello 太之後加入`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="4d16d-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="4d16d-122">Hello VM 重新開機，然後繼續 tooverify hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="4d16d-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="4d16d-123">以 CentOS 作為基礎的 7.3 或 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="4d16d-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="4d16d-124">更新 hello 核心和 DKMS。</span><span class="sxs-lookup"><span data-stu-id="4d16d-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="4d16d-125">停用 hello Nouveau 核心驅動程式，也就是與 hello NVIDIA 驅動程式不相容。</span><span class="sxs-lookup"><span data-stu-id="4d16d-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="4d16d-126">（僅使用 hello NVIDIA 驅動程式 NV Vm 上）。toodo，建立一個檔案中的`/etc/modprobe.d `名為`nouveau.conf`以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="4d16d-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="4d16d-127">Hello VM 重新開機，請重新連線，並安裝 hello Hyper-v： 最新的 Linux Integration Services</span><span class="sxs-lookup"><span data-stu-id="4d16d-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="4d16d-128">重新連線 toohello VM 以及執行 hello`lspci`命令。</span><span class="sxs-lookup"><span data-stu-id="4d16d-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="4d16d-129">請確認 hello NVIDIA M60 卡可以顯示為 PCI 裝置。</span><span class="sxs-lookup"><span data-stu-id="4d16d-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="4d16d-130">下載並安裝 hello 方格驅動程式：</span><span class="sxs-lookup"><span data-stu-id="4d16d-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="4d16d-131">當詢問您是否想 toorun hello nvidia xconfig 公用程式 tooupdate X 組態檔時，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="4d16d-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="4d16d-132">安裝完成之後，請複製 /etc/nvidia/gridd.conf.template tooa 新檔案 gridd.conf 在位置 /etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="4d16d-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="4d16d-133">Hello 太之後加入`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="4d16d-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="4d16d-134">Hello VM 重新開機，然後繼續 tooverify hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="4d16d-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="4d16d-135">確認驅動程式安裝</span><span class="sxs-lookup"><span data-stu-id="4d16d-135">Verify driver installation</span></span>


<span data-ttu-id="4d16d-136">tooquery hello GPU 裝置狀態、 SSH toohello VM 和執行的 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface)與 hello 驅動程式一起安裝的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="4d16d-137">此時會出現類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="4d16d-137">Output similar toohello following appears:</span></span>

![NVIDIA 裝置狀態](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="4d16d-139">X11 伺服器</span><span class="sxs-lookup"><span data-stu-id="4d16d-139">X11 server</span></span>
<span data-ttu-id="4d16d-140">如果您需要 X11 伺服器進行遠端連線 tooan NV VM [x11vnc](http://www.karlrunge.com/x11vnc/)建議使用，因為它可讓硬體加速的圖形。</span><span class="sxs-lookup"><span data-stu-id="4d16d-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="4d16d-141">hello BusID 的 hello M60 裝置必須手動新增 toohello xconfig 檔案 (`etc/X11/xorg.conf`上 Ubuntu 16.04 LTS、 `/etc/X11/XF86config` CentOS 7.3 或 Red Hat Enterprise Server 7.3 上)。</span><span class="sxs-lookup"><span data-stu-id="4d16d-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="4d16d-142">新增`"Device"`區段類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="4d16d-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="4d16d-143">此外，更新您`"Screen"`區段 toouse 此裝置。</span><span class="sxs-lookup"><span data-stu-id="4d16d-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="4d16d-144">可以找到 hello BusID 執行</span><span class="sxs-lookup"><span data-stu-id="4d16d-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="4d16d-145">取得重新配置 VM，或重新啟動時，可以變更 hello BusID。</span><span class="sxs-lookup"><span data-stu-id="4d16d-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="4d16d-146">因此，您可能想 toouse hello X11 組態指令碼 tooupdate hello BusID 時重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="4d16d-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="4d16d-147">例如：</span><span class="sxs-lookup"><span data-stu-id="4d16d-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="4d16d-148">可以叫用這個檔案作為開機時的根目錄，方法是在 `/etc/rc.d/rc3.d` 中為其建立項目。</span><span class="sxs-lookup"><span data-stu-id="4d16d-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="4d16d-149">安裝適用於 NC VM 的 CUDA 驅動程式</span><span class="sxs-lookup"><span data-stu-id="4d16d-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="4d16d-150">以下是 Linux NC Vm 從 hello NVIDIA CUDA Toolkit 8.0 步驟 tooinstall NVIDIA 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="4d16d-151">C 和 c + + 開發人員可以選擇性地安裝 hello 完整 Toolkit toobuild GPU 加速應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="4d16d-152">如需詳細資訊，請參閱 hello [CUDA 安裝指南](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)。</span><span class="sxs-lookup"><span data-stu-id="4d16d-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="4d16d-153">這裡所提供的 CUDA 驅動程式下載連結，為發行當時的最新驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="4d16d-154">Hello 最新 CUDA 驅動程式，請造訪 hello [NVIDIA](http://www.nvidia.com/)網站。</span><span class="sxs-lookup"><span data-stu-id="4d16d-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="4d16d-155">tooinstall CUDA Toolkit 進行的 SSH 連線 tooeach VM。</span><span class="sxs-lookup"><span data-stu-id="4d16d-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="4d16d-156">hello 系統的 tooverify 具有 CUDA 能夠 GPU，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4d16d-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="4d16d-157">您會看到下列範例 （顯示 NVIDIA Tesla K80 卡） 的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="4d16d-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![lspci 命令輸出](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="4d16d-159">然後執行您的配送映像特有的安裝命令。</span><span class="sxs-lookup"><span data-stu-id="4d16d-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="4d16d-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4d16d-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="4d16d-161">下載並安裝 hello CUDA 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="4d16d-162">hello 安裝可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4d16d-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="4d16d-163">toooptionally 安裝 hello 完成 CUDA 工具組，類型：</span><span class="sxs-lookup"><span data-stu-id="4d16d-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="4d16d-164">Hello VM 重新開機，然後繼續 tooverify hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="4d16d-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="4d16d-165">以 CentOS 作為基礎的 7.3 或 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="4d16d-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="4d16d-166">取得更新。</span><span class="sxs-lookup"><span data-stu-id="4d16d-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="4d16d-167">重新連線 toohello VM，然後安裝 hello 最新的 HYPER-V 的 Linux Integration Services。</span><span class="sxs-lookup"><span data-stu-id="4d16d-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4d16d-168">如果您 NC24r VM 上安裝的 CentOS 架構 HPC 映像，請略過 tooStep 3。</span><span class="sxs-lookup"><span data-stu-id="4d16d-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="4d16d-169">因為 hello 映像中預先安裝 Azure RDMA 驅動程式及 Linux Integration Services，LIS 應該不會進行升級，並依預設會停用核心更新。</span><span class="sxs-lookup"><span data-stu-id="4d16d-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="4d16d-170">重新連線 toohello VM 並繼續安裝以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4d16d-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

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

  <span data-ttu-id="4d16d-171">hello 安裝可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4d16d-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="4d16d-172">toooptionally 安裝 hello 完成 CUDA 工具組，類型：</span><span class="sxs-lookup"><span data-stu-id="4d16d-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="4d16d-173">Hello VM 重新開機，然後繼續 tooverify hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="4d16d-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="4d16d-174">確認驅動程式安裝</span><span class="sxs-lookup"><span data-stu-id="4d16d-174">Verify driver installation</span></span>


<span data-ttu-id="4d16d-175">tooquery hello GPU 裝置狀態、 SSH toohello VM 和執行的 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface)與 hello 驅動程式一起安裝的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="4d16d-176">此時會出現類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="4d16d-176">Output similar toohello following appears:</span></span>

![NVIDIA 裝置狀態](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="4d16d-178">CUDA 驅動程式更新</span><span class="sxs-lookup"><span data-stu-id="4d16d-178">CUDA driver updates</span></span>

<span data-ttu-id="4d16d-179">我們建議您在部署後定期更新 CUDA 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4d16d-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="4d16d-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4d16d-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="4d16d-181">以 CentOS 作為基礎的 7.3 或 Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="4d16d-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="4d16d-182">疑難排解</span><span class="sxs-lookup"><span data-stu-id="4d16d-182">Troubleshooting</span></span>

* <span data-ttu-id="4d16d-183">沒有 CUDA Ubuntu 16.04 LTS 上執行 hello 4.4.0-75 Linux 核心 Azure N 系列 Vm 上的驅動程式的已知的問題。</span><span class="sxs-lookup"><span data-stu-id="4d16d-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="4d16d-184">如果您要從較早的核心版本升級，升級 tooat 最低核心版本 4.4.0-77。</span><span class="sxs-lookup"><span data-stu-id="4d16d-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="4d16d-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d16d-185">Next steps</span></span>

* <span data-ttu-id="4d16d-186">在 hello N 系列 Vm 上 hello NVIDIA Gpu 的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="4d16d-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="4d16d-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (適用於 Azure NC VM)</span><span class="sxs-lookup"><span data-stu-id="4d16d-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="4d16d-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (適用於 Azure NV VM)</span><span class="sxs-lookup"><span data-stu-id="4d16d-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="4d16d-189">toocapture Linux VM 映像與安裝的 NVIDIA 驅動程式，請參閱[如何 toogeneralize 和擷取 Linux 虛擬機器](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4d16d-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
