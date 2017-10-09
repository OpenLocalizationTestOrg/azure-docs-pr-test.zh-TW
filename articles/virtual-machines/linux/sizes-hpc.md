---
title: "aaaAzure Linux VM 大小-HPC |Microsoft 文件"
description: "列出 hello 不同大小適用於 Linux 的高效能運算在 Azure 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="65c44-103">高效能運算 Linux VM 大小</span><span class="sxs-lookup"><span data-stu-id="65c44-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="65c44-104">支援 RDMA 的執行個體</span><span class="sxs-lookup"><span data-stu-id="65c44-104">RDMA-capable instances</span></span>
<span data-ttu-id="65c44-105">子集 hello 需要大量計算執行個體 （H16r、 H16mr、 A8、 A9） 功能的網路介面，遠端直接記憶體存取 (RDMA) 連線。</span><span class="sxs-lookup"><span data-stu-id="65c44-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="65c44-106">這個介面是另外 toohello 標準 Azure 網路介面可用 tooother VM 大小。</span><span class="sxs-lookup"><span data-stu-id="65c44-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="65c44-107">這個介面允許 hello 具備 RDMA 功能的執行個體 toocommunicate 透過 InfiniBand 網路，在 H16r 和 H16mr 虛擬機器的 FDR 率和 QDR 率的 A8 和 A9 虛擬機器上運作。</span><span class="sxs-lookup"><span data-stu-id="65c44-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="65c44-108">Hello 延展性和效能的訊息傳遞介面 (MPI) 應用程式，可以提高這些具備 RDMA 功能。</span><span class="sxs-lookup"><span data-stu-id="65c44-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="65c44-109">下列是具備 RDMA 功能的 Linux Vm tooaccess hello Azure RDMA 網路需求：</span><span class="sxs-lookup"><span data-stu-id="65c44-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="65c44-110">**分佈**-您必須將 Vm 從具備 RDMA 功能 SUSE Linux Enterprise Server (SLES) 部署或 Rogue Wave 軟體 (先前稱為 OpenLogic) CentOS 架構 HPC 映像中的 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="65c44-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="65c44-111">hello 下列 Marketplace 映像支援 RDMA 連線能力：</span><span class="sxs-lookup"><span data-stu-id="65c44-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="65c44-112">SLES 12 SP1 for HPC 或 SLES 12 SP1 for HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="65c44-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="65c44-113">CentOS 型 7.3 HPC、CentOS 型 7.1 HPC、CentOS 型 6.8 HPC 或 CentOS 型 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="65c44-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="65c44-114">針對 H 系列 VM，建議使用 SLES 12 SP1 for HPC 映像或 CentOS 型 7.1 或更新版本的 HPC。</span><span class="sxs-lookup"><span data-stu-id="65c44-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="65c44-115">Hello CentOS 架構 HPC 映像，核心會停用更新中 hello **yum**組態檔。</span><span class="sxs-lookup"><span data-stu-id="65c44-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="65c44-116">這是因為 hello Linux RDMA 驅動程式散發作為 RPM 套件，而且如果 hello 核心會更新驅動程式的更新可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="65c44-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="65c44-117">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="65c44-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="65c44-118">根據 hello Marketplace 映像您選擇，個別的授權，安裝，或 Intel MPI 的組態可能需要，如下所示：</span><span class="sxs-lookup"><span data-stu-id="65c44-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="65c44-119">**HPC 映像的 SLES 12 SP1** -Intel MPI 套件發佈 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="65c44-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="65c44-120">執行下列命令的 hello 來安裝：</span><span class="sxs-lookup"><span data-stu-id="65c44-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="65c44-121">**CentOS 型 HPC 映像** - 已經安裝 Intel MPI 5.1。</span><span class="sxs-lookup"><span data-stu-id="65c44-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="65c44-122">其他系統設定為叢集 Vm 上的所需的 toorun MPI 工作。</span><span class="sxs-lookup"><span data-stu-id="65c44-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="65c44-123">例如，在叢集上的 Vm，您需要 tooestablish hello 之間信任計算節點。</span><span class="sxs-lookup"><span data-stu-id="65c44-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="65c44-124">一般設定，請參閱[設定 Linux RDMA 叢集 toorun MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="65c44-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="65c44-125">網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="65c44-125">Network topology considerations</span></span>
* <span data-ttu-id="65c44-126">在 Azure 中具備 RDMA 功能的 Linux VM 上，Eth1 會保留給 RDMA 網路流量使用。</span><span class="sxs-lookup"><span data-stu-id="65c44-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="65c44-127">請勿變更任何 Eth1 設定或 hello 組態檔參考 toothis 網路中的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="65c44-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="65c44-128">Eth0 會保留給一般 Azure 網路流量。</span><span class="sxs-lookup"><span data-stu-id="65c44-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="65c44-129">在 Azure 中，不支援透過 InfiniBand (IB) 的 IP。</span><span class="sxs-lookup"><span data-stu-id="65c44-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="65c44-130">僅支援透過 IB 的 RDMA。</span><span class="sxs-lookup"><span data-stu-id="65c44-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="65c44-131">使用 HPC Pack</span><span class="sxs-lookup"><span data-stu-id="65c44-131">Using HPC Pack</span></span>
<span data-ttu-id="65c44-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)，Microsoft 的免費 HPC 叢集和作業管理方案，是為您的 Linux toouse hello 大量計算執行個體的其中一個選項。</span><span class="sxs-lookup"><span data-stu-id="65c44-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="65c44-133">hello 的 HPC Pack 的最新版本都支援數個 toorun 上的運算節點管理的 Windows Server 的前端節點的 Azure Vm 中部署的 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="65c44-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="65c44-134">具有 RDMA 功能的 Linux 運算節點執行 Intel MPI HPC Pack 可以排程，並執行 Linux MPI 應用程式存取 hello RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="65c44-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="65c44-135">請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="65c44-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="65c44-136">其他大小</span><span class="sxs-lookup"><span data-stu-id="65c44-136">Other sizes</span></span>
- [<span data-ttu-id="65c44-137">一般用途</span><span class="sxs-lookup"><span data-stu-id="65c44-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="65c44-138">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="65c44-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="65c44-139">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="65c44-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="65c44-140">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="65c44-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="65c44-141">GPU</span><span class="sxs-lookup"><span data-stu-id="65c44-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="65c44-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65c44-142">Next steps</span></span>

- <span data-ttu-id="65c44-143">tooget 啟動部署與使用需要大量計算的大小與 RDMA on Linux，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="65c44-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="65c44-144">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="65c44-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




