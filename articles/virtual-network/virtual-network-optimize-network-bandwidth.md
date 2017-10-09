---
title: "aaaOptimize VM 網路輸送量 |Microsoft 文件"
description: "了解如何 toooptimize Azure 虛擬機器的網路輸送量。"
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="173e5-103">最佳化 Azure 虛擬機器的網路輸送量</span><span class="sxs-lookup"><span data-stu-id="173e5-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="173e5-104">Azure 虛擬機器 (VM) 有預設網路設定，可進一步針對網路輸送量進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="173e5-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="173e5-105">本文說明如何 toooptimize 適用於 Microsoft Azure Windows 和 Linux Vm，包括主要的分佈，例如 Ubuntu、 CentOS 和 Red Hat 的網路輸送量。</span><span class="sxs-lookup"><span data-stu-id="173e5-105">This article describes how toooptimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="173e5-106">Windows VM</span><span class="sxs-lookup"><span data-stu-id="173e5-106">Windows VM</span></span>

<span data-ttu-id="173e5-107">如果您的 Windows VM 支援[加速網路](virtual-network-create-vm-accelerated-networking.md)，啟用該功能會 hello 最佳輸送量設定。</span><span class="sxs-lookup"><span data-stu-id="173e5-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be hello optimal configuration for throughput.</span></span> <span data-ttu-id="173e5-108">針對所有其他的 Windows VM，相較於不使用接收端調整 (RSS) 的 VM，使用 RSS 的 VM 可達到更高的最大輸送量。</span><span class="sxs-lookup"><span data-stu-id="173e5-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="173e5-109">根據預設，Windows VM 中可能會停用 RSS。</span><span class="sxs-lookup"><span data-stu-id="173e5-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="173e5-110">完成下列步驟 toodetermine 是否已啟用 RSS hello 和 tooenable 它已停用。</span><span class="sxs-lookup"><span data-stu-id="173e5-110">Complete hello following steps toodetermine whether RSS is enabled and tooenable it if it's disabled.</span></span>

1. <span data-ttu-id="173e5-111">輸入 hello `Get-NetAdapterRss` PowerShell 命令 toosee 如果已啟用 RSS 的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="173e5-111">Enter hello `Get-NetAdapterRss` PowerShell command toosee if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="173e5-112">在 hello 下列範例輸出傳回的 hello `Get-NetAdapterRss`，RSS 不會啟用。</span><span class="sxs-lookup"><span data-stu-id="173e5-112">In hello following example output returned from hello `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="173e5-113">輸入下列命令 tooenable RSS hello:</span><span class="sxs-lookup"><span data-stu-id="173e5-113">Enter hello following command tooenable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="173e5-114">hello 前一個命令沒有輸出。</span><span class="sxs-lookup"><span data-stu-id="173e5-114">hello previous command does not have an output.</span></span> <span data-ttu-id="173e5-115">hello 命令變更 NIC 設定，造成連線暫時中斷約 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="173e5-115">hello command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="173e5-116">Reconnecting 對話方塊隨即出現在 hello 連線中斷。</span><span class="sxs-lookup"><span data-stu-id="173e5-116">A Reconnecting dialog box appears during hello connectivity loss.</span></span> <span data-ttu-id="173e5-117">連線通常是 hello 第三個嘗試之後還原。</span><span class="sxs-lookup"><span data-stu-id="173e5-117">Connectivity is typically restored after hello third attempt.</span></span>
3. <span data-ttu-id="173e5-118">確認 RSS 啟用 hello VM 中，輸入 hello`Get-NetAdapterRss`命令一次。</span><span class="sxs-lookup"><span data-stu-id="173e5-118">Confirm that RSS is enabled in hello VM by entering hello `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="173e5-119">如果成功，則會傳回 hello 下列範例輸出：</span><span class="sxs-lookup"><span data-stu-id="173e5-119">If successful, hello following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="173e5-120">Linux VM</span><span class="sxs-lookup"><span data-stu-id="173e5-120">Linux VM</span></span>

<span data-ttu-id="173e5-121">根據預設，Azure Linux VM 中一律會啟用 RSS。</span><span class="sxs-lookup"><span data-stu-id="173e5-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="173e5-122">Linux 核心發行之後 2017 年 1 月，包括新的網路最佳化選項，可讓 Linux VM tooachieve 更高的網路輸送量。</span><span class="sxs-lookup"><span data-stu-id="173e5-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM tooachieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="173e5-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="173e5-123">Ubuntu</span></span>

<span data-ttu-id="173e5-124">順序 tooget hello 最佳化，在第一次更新 toohello 最新支援版本，為準，年 6 月 2017，也就是：</span><span class="sxs-lookup"><span data-stu-id="173e5-124">In order tooget hello optimization, first update toohello latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="173e5-125">Hello 更新已完成之後，請輸入下列命令 tooget hello 最新的核心 hello:</span><span class="sxs-lookup"><span data-stu-id="173e5-125">After hello update is complete, enter hello following commands tooget hello latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="173e5-126">選擇性命令︰</span><span class="sxs-lookup"><span data-stu-id="173e5-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="173e5-127">Ubuntu 的 Azure 預覽版核心</span><span class="sxs-lookup"><span data-stu-id="173e5-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="173e5-128">核心可能沒有此 Azure Linux 預覽 hello 相同層級的可用性和可靠性 Marketplace 映像以及一般可用性版本的核心。</span><span class="sxs-lookup"><span data-stu-id="173e5-128">This Azure Linux Preview kernel may not have hello same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="173e5-129">hello 功能不支援，可能有限制功能，且可能無法 hello 預設核心的可靠。</span><span class="sxs-lookup"><span data-stu-id="173e5-129">hello feature is not supported, may have constrained capabilities, and may not be as reliable as hello default kernel.</span></span> <span data-ttu-id="173e5-130">請勿將此核心使用於生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="173e5-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="173e5-131">大幅輸送量效能可藉由安裝 hello 提議 Azure Linux 核心。</span><span class="sxs-lookup"><span data-stu-id="173e5-131">Significant throughput performance can be achieved by installing hello proposed Azure Linux kernel.</span></span> <span data-ttu-id="173e5-132">tootry 核心中，新增這行 too/etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="173e5-132">tootry this kernel, add this line too/etc/apt/sources.list</span></span>

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="173e5-133">然後以 root 身分執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="173e5-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="173e5-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="173e5-134">CentOS</span></span>

<span data-ttu-id="173e5-135">順序 tooget hello 最佳化，在第一次更新 toohello 最新支援版本，為準，年 7 月 2017，也就是：</span><span class="sxs-lookup"><span data-stu-id="173e5-135">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="173e5-136">Hello 更新已完成之後，安裝 hello 最新的 Linux Integration Services (LIS)。</span><span class="sxs-lookup"><span data-stu-id="173e5-136">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="173e5-137">hello 輸送量最佳化處於 LIS，從 4.2.2-2 開始。</span><span class="sxs-lookup"><span data-stu-id="173e5-137">hello throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="173e5-138">輸入下列命令 tooinstall LIS hello:</span><span class="sxs-lookup"><span data-stu-id="173e5-138">Enter hello following commands tooinstall LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="173e5-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="173e5-139">Red Hat</span></span>

<span data-ttu-id="173e5-140">順序 tooget hello 最佳化，在第一次更新 toohello 最新支援版本，為準，年 7 月 2017，也就是：</span><span class="sxs-lookup"><span data-stu-id="173e5-140">In order tooget hello optimization, first update toohello latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="173e5-141">Hello 更新已完成之後，安裝 hello 最新的 Linux Integration Services (LIS)。</span><span class="sxs-lookup"><span data-stu-id="173e5-141">After hello update is complete, install hello latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="173e5-142">hello 輸送量最佳化處於 LIS，從 4.2 開始。</span><span class="sxs-lookup"><span data-stu-id="173e5-142">hello throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="173e5-143">輸入下列命令 toodownload hello 和安裝 LIS:</span><span class="sxs-lookup"><span data-stu-id="173e5-143">Enter hello following commands toodownload and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="173e5-144">深入了解 Linux 整合服務版本 4.2 hyper-v 藉由檢視 hello[下載頁面](https://www.microsoft.com/download/details.aspx?id=55106)。</span><span class="sxs-lookup"><span data-stu-id="173e5-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing hello [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="173e5-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="173e5-145">Next steps</span></span>
* <span data-ttu-id="173e5-146">既然 hello VM 會經過最佳化，請參閱 hello 結果與[頻寬/輸送量測試 Azure VM](virtual-network-bandwidth-testing.md)您的案例。</span><span class="sxs-lookup"><span data-stu-id="173e5-146">Now that hello VM is optimized, see hello result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="173e5-147">深入了解 [Azure 虛擬網路常見問題集 (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="173e5-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
