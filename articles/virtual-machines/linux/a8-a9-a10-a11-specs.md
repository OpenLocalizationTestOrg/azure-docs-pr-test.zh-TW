---
title: "aaaAbout 需要大量計算的 Linux Vm |Microsoft 文件"
description: "取得背景資訊和使用 hello H 數列和 A8、 A9、 A10 和 A11 大量計算的大小適用於 Linux Vm 的考量"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="1d7a3-103">關於 Linux 的 H 系列和計算密集型 A 系列 VM</span><span class="sxs-lookup"><span data-stu-id="1d7a3-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="1d7a3-104">以下是背景資訊和使用的一些考量 hello 較新的 Azure H 數列也稱為 hello 較早的 A8、 A9、 A10 和 A11 大小*需要大量計算*執行個體。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="1d7a3-105">本文將焦點放在使用這些 Linux VM 大小。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="1d7a3-106">您也可以針對 [Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 使用它們。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1d7a3-107">如需基本規格、儲存體容量與磁碟的詳細資料，請參閱[虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="1d7a3-108">存取 toohello RDMA 網路</span><span class="sxs-lookup"><span data-stu-id="1d7a3-108">Access toohello RDMA network</span></span>
<span data-ttu-id="1d7a3-109">您可以建立具備 RDMA 功能 hello 下列支援的 Linux HPC 分佈和 hello Azure RDMA 網路的支援的 MPI 實作 tootake 優點的其中一個執行的 Linux Vm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="1d7a3-110">請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)部署選項和範例的組態步驟。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="1d7a3-111">**分佈**-您必須將 Vm 從具備 RDMA 功能 SUSE Linux Enterprise Server (SLES) 部署或 Rogue Wave 軟體 (先前稱為 OpenLogic) CentOS 架構 HPC 映像中的 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="1d7a3-112">hello 下列 Marketplace 映像支援 RDMA 連線能力：</span><span class="sxs-lookup"><span data-stu-id="1d7a3-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="1d7a3-113">SLES 12 SP1 for HPC、SLES 12 SP1 for HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="1d7a3-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="1d7a3-114">CentOS 型 7.1 HPC、CentOS 型 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="1d7a3-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="1d7a3-115">針對 H 系列 VM，建議使用 SLES 12 SP1 for HPC 映像或 CentOS 型 7.1 HPC。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="1d7a3-116">Hello CentOS 架構 HPC 映像，核心會停用更新中 hello **yum**組態檔。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="1d7a3-117">這是因為 hello Linux RDMA 驅動程式散發作為 RPM 套件，而且如果 hello 核心會更新驅動程式的更新可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="1d7a3-118">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="1d7a3-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="1d7a3-119">根據 hello Marketplace 映像您選擇，個別的授權，安裝，或 Intel MPI 的組態可能需要，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d7a3-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="1d7a3-120">**HPC 映像的 SLES 12 SP1** -Intel MPI 套件發佈 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="1d7a3-121">執行下列命令的 hello 來安裝：</span><span class="sxs-lookup"><span data-stu-id="1d7a3-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="1d7a3-122">**CentOS 型 HPC 映像** - 已經安裝 Intel MPI 5.1。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="1d7a3-123">其他系統設定為叢集 Vm 上的所需的 toorun MPI 工作。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="1d7a3-124">例如，在叢集上的 Vm，您需要 tooestablish hello 之間信任計算節點。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="1d7a3-125">一般設定，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="1d7a3-126">HPC Pack 和 Linux 的考量</span><span class="sxs-lookup"><span data-stu-id="1d7a3-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="1d7a3-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)，Microsoft 的免費 HPC 叢集和作業管理方案，提供您的第一個選項與 Linux toouse hello 大量計算執行個體。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="1d7a3-128">hello 的 HPC Pack 的最新版本都支援數個 toorun 上的運算節點管理的 Windows Server 的前端節點的 Azure Vm 中部署的 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="1d7a3-129">具有 RDMA 功能的 Linux 運算節點執行 Intel MPI HPC Pack 可以排程，並執行 Linux MPI 應用程式存取 hello RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="1d7a3-130">tooget 啟動，請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="1d7a3-131">網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="1d7a3-131">Network topology considerations</span></span>
* <span data-ttu-id="1d7a3-132">在 Azure 中具備 RDMA 功能的 Linux VM 上，Eth1 會保留給 RDMA 網路流量使用。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="1d7a3-133">請勿變更任何 Eth1 設定或 hello 組態檔參考 toothis 網路中的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="1d7a3-134">Eth0 會保留給一般 Azure 網路流量。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="1d7a3-135">在 Azure 中，不支援透過 InfiniBand (IB) 的 IP。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="1d7a3-136">僅支援透過 IB 的 RDMA。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1d7a3-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d7a3-137">Next steps</span></span>
* <span data-ttu-id="1d7a3-138">如需可用性和價格 hello 需要大量計算的大小的詳細資訊，請參閱[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="1d7a3-139">如需儲存體容量與磁碟詳細資訊，請參閱[虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1d7a3-140">tooget 啟動部署與使用需要大量計算的大小與 RDMA on Linux，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1d7a3-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

