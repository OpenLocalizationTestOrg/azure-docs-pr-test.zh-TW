---
title: "適用於 Windows 的 aaaAzure N 序列驅動程式安裝 |Microsoft 文件"
description: "如何 tooset 向上 N 系列 Vm 在 Azure 中執行 Windows 的 NVIDIA GPU 驅動程式"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="29baa-103">為執行 Windows Server 的 N 系列 VM 設定 GPU 驅動程式</span><span class="sxs-lookup"><span data-stu-id="29baa-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="29baa-104">tootake 利用 hello GPU 功能的 Azure N 系列 Vm 執行 Windows Server 2016 或 Windows Server 2012 R2，安裝支援 NVIDIA 圖形驅動程式。</span><span class="sxs-lookup"><span data-stu-id="29baa-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="29baa-105">本文提供您在部署 N 系列 VM 後的驅動程式安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="29baa-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="29baa-106">驅動程式設定資訊也適用於 [ VM](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="29baa-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="29baa-107">如需基本規格、儲存體容量與磁碟的詳細資料，請參閱 [GPU Windows VM 大小](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="29baa-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="29baa-108">驅動程式安裝</span><span class="sxs-lookup"><span data-stu-id="29baa-108">Driver installation</span></span>

1. <span data-ttu-id="29baa-109">遠端桌面 tooeach N 系列 VM 的連線。</span><span class="sxs-lookup"><span data-stu-id="29baa-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="29baa-110">下載、 擷取，並安裝 Windows 作業系統的支援 hello 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="29baa-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="29baa-111">在 Azure NV VM 上，安裝驅動程式之後必須重新啟動。</span><span class="sxs-lookup"><span data-stu-id="29baa-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="29baa-112">在 NC VM 上，則不需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="29baa-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="29baa-113">確認驅動程式安裝</span><span class="sxs-lookup"><span data-stu-id="29baa-113">Verify driver installation</span></span>

<span data-ttu-id="29baa-114">您可以在 [裝置管理員] 中確認驅動程式安裝。</span><span class="sxs-lookup"><span data-stu-id="29baa-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="29baa-115">hello 下列範例顯示成功之組態 hello Tesla K80 卡 NC Azure VM 上。</span><span class="sxs-lookup"><span data-stu-id="29baa-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![GPU 驅動程式屬性](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="29baa-117">tooquery hello GPU 裝置狀態、 執行 hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface)與 hello 驅動程式一起安裝的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="29baa-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="29baa-118">開啟命令提示字元並變更 toohello **C:\Program Files\NVIDIA Corporation\NVSMI**目錄。</span><span class="sxs-lookup"><span data-stu-id="29baa-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="29baa-119">執行 **nvidia-smi**。</span><span class="sxs-lookup"><span data-stu-id="29baa-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="29baa-120">如果安裝 hello 驅動程式會輸出類似 toobelow。</span><span class="sxs-lookup"><span data-stu-id="29baa-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="29baa-121">請注意， **GPU Util**顯示**0%**除非 hello VM 上目前正在 GPU 工作負載。</span><span class="sxs-lookup"><span data-stu-id="29baa-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![NVIDIA 裝置狀態](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="29baa-123">適用於 NC24r VM 的 RDMA 網路</span><span class="sxs-lookup"><span data-stu-id="29baa-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="29baa-124">可以部署在 hello 的 NC24r Vm 上啟用 RDMA 網路連線相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="29baa-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="29baa-125">hello HpcVmDrivers 延伸模組必須先新增 tooinstall Windows 網路裝置驅動程式，啟用 RDMA 連接。</span><span class="sxs-lookup"><span data-stu-id="29baa-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="29baa-126">tooadd hello VM 延伸模組 tooan NC24r VM 使用[Azure PowerShell](/powershell/azure/overview) Azure 資源管理員的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="29baa-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="29baa-127">目前，只有 Windows Server 2012 R2 支援 hello RDMA 網路 NC24r Vm 上。</span><span class="sxs-lookup"><span data-stu-id="29baa-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="29baa-128">tooinstall hello 最新版本 1.1 HpcVMDrivers 延伸模組現有具備 RDMA 功能的 VM 上名為 myVM hello 美國西部區域中：</span><span class="sxs-lookup"><span data-stu-id="29baa-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="29baa-129">如需詳細資訊，請參閱[適用於 Windows 的虛擬機器擴充功能和功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="29baa-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="29baa-130">hello RDMA 網路以執行應用程式支援訊息傳遞介面 (MPI) 流量[Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx)或 Intel MPI 5.x。</span><span class="sxs-lookup"><span data-stu-id="29baa-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="29baa-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29baa-131">Next steps</span></span>

* <span data-ttu-id="29baa-132">在 hello N 系列 Vm 上 hello NVIDIA Gpu 的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="29baa-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="29baa-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (適用於 Azure NC VM)</span><span class="sxs-lookup"><span data-stu-id="29baa-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="29baa-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (適用於 Azure NV VM)</span><span class="sxs-lookup"><span data-stu-id="29baa-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="29baa-135">建置 hello NVIDIA Tesla Gpu 的 GPU 加速應用程式的開發人員同時下載及安裝 hello CUDA Toolkit 8 的[Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe)或[Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe)。</span><span class="sxs-lookup"><span data-stu-id="29baa-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="29baa-136">如需詳細資訊，請參閱 hello [CUDA 安裝指南](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi)。</span><span class="sxs-lookup"><span data-stu-id="29baa-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


