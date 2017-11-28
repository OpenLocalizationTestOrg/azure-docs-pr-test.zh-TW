---
title: "aaaAzure Windows VM 大小 HPC |Microsoft 文件"
description: "列出 hello 不同大小適用於 Windows 的高效能運算在 Azure 虛擬機器。"
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
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="01b0f-103">高效能運算 VM 大小</span><span class="sxs-lookup"><span data-stu-id="01b0f-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="01b0f-104">支援 RDMA 的執行個體</span><span class="sxs-lookup"><span data-stu-id="01b0f-104">RDMA-capable instances</span></span>
<span data-ttu-id="01b0f-105">子集 hello 需要大量計算執行個體 （H16r、 H16mr、 A8、 A9） 功能的網路介面，遠端直接記憶體存取 (RDMA) 連線。</span><span class="sxs-lookup"><span data-stu-id="01b0f-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="01b0f-106">這個介面是另外 toohello 標準 Azure 網路介面可用 tooother VM 大小。</span><span class="sxs-lookup"><span data-stu-id="01b0f-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="01b0f-107">這個介面允許 hello 具備 RDMA 功能的執行個體 toocommunicate 透過 InfiniBand 網路，在 H16r 和 H16mr 虛擬機器的 FDR 率和 QDR 率的 A8 和 A9 虛擬機器上運作。</span><span class="sxs-lookup"><span data-stu-id="01b0f-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="01b0f-108">Hello 延展性和效能的訊息傳遞介面 (MPI) 應用程式，可以提高這些具備 RDMA 功能。</span><span class="sxs-lookup"><span data-stu-id="01b0f-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="01b0f-109">下列是具備 RDMA 功能的 Windows Vm tooaccess hello Azure RDMA 網路需求：</span><span class="sxs-lookup"><span data-stu-id="01b0f-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="01b0f-110">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="01b0f-110">**Operating system**</span></span>
  
  <span data-ttu-id="01b0f-111">Windows Server 2012 R2、Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="01b0f-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="01b0f-112">Windows Server 2016 目前不支援 Azure 中的 RDMA 連線能力。</span><span class="sxs-lookup"><span data-stu-id="01b0f-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="01b0f-113">**可用性設定組或雲端服務**– 中部署具備 RDMA 功能的 hello Vm hello 相同可用性設定組 （當您使用 hello Azure Resource Manager 部署模型時） 或 hello 相同雲端服務 （當您使用 hello 傳統部署模型）。</span><span class="sxs-lookup"><span data-stu-id="01b0f-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="01b0f-114">如果您使用 Azure 批次時，必須在 hello hello 具備 RDMA 功能的 Vm 相同的集區。</span><span class="sxs-lookup"><span data-stu-id="01b0f-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="01b0f-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 或更新版本、Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="01b0f-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="01b0f-116">支援的 MPI 實作使用 hello Microsoft Network Direct 介面 toocommunicate 執行個體之間。</span><span class="sxs-lookup"><span data-stu-id="01b0f-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="01b0f-117">**RDMA 網路位址空間**-在 Azure 中的 hello RDMA 網路保留 hello 位址空間 172.16.0.0/16。</span><span class="sxs-lookup"><span data-stu-id="01b0f-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="01b0f-118">toorun MPI 應用程式執行個體部署在 Azure 虛擬網路，請確定 hello 虛擬網路位址空間不會重疊 hello RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="01b0f-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="01b0f-119">**VM HpcVmDrivers 延伸模組**-上具備 RDMA 功能的 Vm，您必須新增 hello HpcVmDrivers 延伸模組 tooinstall Windows 網路裝置驅動程式的 RDMA 連線能力。</span><span class="sxs-lookup"><span data-stu-id="01b0f-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="01b0f-120">（在某些部署 A8 和 A9 執行個體中，hello HpcVmDrivers 延伸模組會自動加入。）tooadd hello VM 延伸模組 tooa VM，您可以使用[Azure PowerShell](/powershell/azure/overview) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="01b0f-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="01b0f-121">hello 下列命令安裝 hello 名為現有具備 RDMA 功能的 VM 上的最新版本 1.1 HpcVMDrivers 延伸模組*myVM*中名為 「 hello 資源群組部署*myResourceGroup* hello中*美國西部*區域：</span><span class="sxs-lookup"><span data-stu-id="01b0f-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="01b0f-122">如需詳細資訊，請參閱[虛擬機器擴充功能和功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="01b0f-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="01b0f-123">您也可以使用擴充功能的 Vm 部署在 hello[傳統部署模型](classic/manage-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="01b0f-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="01b0f-124">使用 HPC Pack</span><span class="sxs-lookup"><span data-stu-id="01b0f-124">Using HPC Pack</span></span>

<span data-ttu-id="01b0f-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)，Microsoft 的免費 HPC 叢集和作業管理方案，是 toocreate Azure toorun Windows 為基礎的 MPI 應用程式及其他 HPC 工作負載中的運算叢集的第一個選項。</span><span class="sxs-lookup"><span data-stu-id="01b0f-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="01b0f-126">HPC Pack 2012 R2 和更新版本包含執行階段環境的 hello Azure RDMA 網路部署時使用 RDMA 功能的 Vm 的 MS-MPI。</span><span class="sxs-lookup"><span data-stu-id="01b0f-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="01b0f-127">其他大小</span><span class="sxs-lookup"><span data-stu-id="01b0f-127">Other sizes</span></span>
- [<span data-ttu-id="01b0f-128">一般用途</span><span class="sxs-lookup"><span data-stu-id="01b0f-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="01b0f-129">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="01b0f-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="01b0f-130">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="01b0f-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="01b0f-131">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="01b0f-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="01b0f-132">GPU 最佳化</span><span class="sxs-lookup"><span data-stu-id="01b0f-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="01b0f-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01b0f-133">Next steps</span></span>

- <span data-ttu-id="01b0f-134">檢查清單 toouse hello 需要大量計算執行個體使用 Windows Server 上的 HPC Pack，請參閱[設定 HPC Pack toorun MPI 應用程式與 Windows RDMA 叢集](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="01b0f-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="01b0f-135">toouse 大量計算執行個體使用 Azure Batch 執行 MPI 應用程式時看到[使用多個執行個體工作 toorun Azure 批次中的訊息傳遞介面 (MPI) 應用程式](../../batch/batch-mpi.md)。</span><span class="sxs-lookup"><span data-stu-id="01b0f-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="01b0f-136">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="01b0f-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




