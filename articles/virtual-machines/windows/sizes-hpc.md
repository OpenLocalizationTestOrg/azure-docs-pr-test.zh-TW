---
title: "Azure Windows VM 大小 - HPC | Microsoft Docs"
description: "列出 Azure 中可用的不同 Windows 高效能運算虛擬機器大小。"
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="8cc1a-103">高效能運算 VM 大小</span><span class="sxs-lookup"><span data-stu-id="8cc1a-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="8cc1a-104">支援 RDMA 的執行個體</span><span class="sxs-lookup"><span data-stu-id="8cc1a-104">RDMA-capable instances</span></span>
<span data-ttu-id="8cc1a-105">計算密集型執行個體 (H16r、H16mr、A8 與 A9) 的子集，包含用於遠端直接記憶體存取 (RDMA) 連線的網路介面。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="8cc1a-106">這是可供其他 VM 大小使用之標準 Azure 網路介面的額外界面。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="8cc1a-107">這個介面允許支援 RDMA 的執行個體透過 InfiniBand 網路進行通訊，針對 H16r 與 H16mr 虛擬機器以 FDR 速率運作，以及針對 A8 與 A9 虛擬機器以 QDR 速率運作。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="8cc1a-108">這些 RDMA 功能可以提高訊息傳遞介面 (MPI) 應用程式的延展性和效能。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="8cc1a-109">以下是支援 RDMA 的 Windows VM 存取 Azure RDMA 網路的需求：</span><span class="sxs-lookup"><span data-stu-id="8cc1a-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="8cc1a-110">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="8cc1a-110">**Operating system**</span></span>
  
  <span data-ttu-id="8cc1a-111">Windows Server 2012 R2、Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8cc1a-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8cc1a-112">Windows Server 2016 目前不支援 Azure 中的 RDMA 連線能力。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="8cc1a-113">**可用性設定組或雲端服務** – 在相同的可用性設定組 (如果您使用 Azure Resource Manager 部署模型) 或相同的雲端服務 (如果您使用傳統部署模型) 中部署支援 RDMA 的 VM。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="8cc1a-114">如果您是使用 Azure 批次，支援 RDMA 的 VM 必須在相同的集區中。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="8cc1a-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 或更新版本、Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="8cc1a-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="8cc1a-116">支援的 MPI 實作使用 Microsoft Network Direct 介面在執行個體之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="8cc1a-117">**RDMA 網路位址空間** - Azure 中的 RDMA 網路會保留位址空間 172.16.0.0/16。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="8cc1a-118">若要在 Azure 虛擬網路中已部署的執行個體上執行 MPI 應用程式，請確定虛擬網路位址空間不會與 RDMA 網路重疊。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="8cc1a-119">**HpcVmDrivers VM 擴充功能** - 在支援 RDMA 的 VM 上，必須新增 HpcVmDrivers 擴充功能，以便安裝 RDMA 連線的 Windows 網路裝置驅動程式。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="8cc1a-120">(在某些 A8 和 A9 執行個體部署中，會自動新增 HpcVmDrivers 擴充功能)。若要將 VM 擴充功能新增至 VM，您可以使用 [Azure PowerShell](/powershell/azure/overview) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="8cc1a-121">下列命令會在支援 RDMA 的虛擬機器 (名稱為 *myVM*，部署在*美國西部*區域中名稱為 *myResourceGroup* 的資源群組) 上安裝最新 1.1 版 HpcVMDrivers 擴充功能：</span><span class="sxs-lookup"><span data-stu-id="8cc1a-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="8cc1a-122">如需詳細資訊，請參閱[虛擬機器擴充功能和功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8cc1a-123">您也可以針對已在[傳統部署模型](classic/manage-extensions.md)中部署的 VM 使用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="8cc1a-124">使用 HPC Pack</span><span class="sxs-lookup"><span data-stu-id="8cc1a-124">Using HPC Pack</span></span>

<span data-ttu-id="8cc1a-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx) 是 Microsoft 的免費 HPC 叢集和作業管理解決方案，可為您提供一個選項，讓您能夠在 Azure 中建立計算叢集來執行 Windows 型 MPI 應用程式及其他 HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="8cc1a-126">HPC Pack 2012 R2 和更新版本包含 MS-MPI 的執行階段環境，此 MS-MPI 如果部署在支援 RDMA 的 VM 上，即可使用 Azure RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="8cc1a-127">其他大小</span><span class="sxs-lookup"><span data-stu-id="8cc1a-127">Other sizes</span></span>
- [<span data-ttu-id="8cc1a-128">一般用途</span><span class="sxs-lookup"><span data-stu-id="8cc1a-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="8cc1a-129">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="8cc1a-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="8cc1a-130">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="8cc1a-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="8cc1a-131">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="8cc1a-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="8cc1a-132">GPU 最佳化</span><span class="sxs-lookup"><span data-stu-id="8cc1a-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="8cc1a-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8cc1a-133">Next steps</span></span>

- <span data-ttu-id="8cc1a-134">如需在 Windows 伺服器上使用大量計算執行個體和 HPC Pack 的檢查清單，請參閱[使用 HPC Pack 設定 Windows RDMA 叢集以執行 MPI 應用程式](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="8cc1a-135">若要在以 Azure Batch 執行 MPI 應用程式時使用計算密集型執行個體，請參閱[在 Azure Batch 中使用多重執行個體工作來執行訊息傳遞介面 (MPI) 應用程式](../../batch/batch-mpi.md)。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="8cc1a-136">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="8cc1a-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




