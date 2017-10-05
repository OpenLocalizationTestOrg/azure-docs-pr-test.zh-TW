---
title: "關於與 Linux 搭配使用的計算密集型 VM | Microsoft Docs"
description: "取得針對 Linux VM 使用 H 系列及 A8、A9、A10 和 A11 計算密集型大小的背景資訊和考量"
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
ms.openlocfilehash: a2307f7055966ec7146b5da0b4daf1ad469abe2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="6a731-103">關於 Linux 的 H 系列和計算密集型 A 系列 VM</span><span class="sxs-lookup"><span data-stu-id="6a731-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="6a731-104">這裡提供使用較新的 Azure H 系列和較舊的 A8、A9、A10 及 A11 大小 (也稱為「計算密集型」  執行個體) 的背景資訊和一些考量。</span><span class="sxs-lookup"><span data-stu-id="6a731-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="6a731-105">本文將焦點放在使用這些 Linux VM 大小。</span><span class="sxs-lookup"><span data-stu-id="6a731-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="6a731-106">您也可以針對 [Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 使用它們。</span><span class="sxs-lookup"><span data-stu-id="6a731-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="6a731-107">如需基本規格、儲存體容量與磁碟的詳細資料，請參閱[虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6a731-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="6a731-108">存取 RDMA 網路</span><span class="sxs-lookup"><span data-stu-id="6a731-108">Access to the RDMA network</span></span>
<span data-ttu-id="6a731-109">您可以建立支援 RDMA 的 Linux VM 叢集來執行下列其中一個支援的 Linux HPC 散發套件及支援的 MPI 實作，以利用 Azure RDMA 網路。</span><span class="sxs-lookup"><span data-stu-id="6a731-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span></span> <span data-ttu-id="6a731-110">如需部署選項和範例組態步驟，請參閱[設定 Linux RDMA 叢集以執行 MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6a731-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="6a731-111">**散發套件** - 您必須從 Azure Marketplace 中支援 RDMA 的 SUSE Linux Enterprise Server (SLES) 或 Rogue Wave Software (先前為 OpenLogic) CentOS 型 HPC 映像部署 VM。</span><span class="sxs-lookup"><span data-stu-id="6a731-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="6a731-112">下列 Marketplace 映像支援 RDMA 連線能力：</span><span class="sxs-lookup"><span data-stu-id="6a731-112">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="6a731-113">SLES 12 SP1 for HPC、SLES 12 SP1 for HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="6a731-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="6a731-114">CentOS 型 7.1 HPC、CentOS 型 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="6a731-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="6a731-115">針對 H 系列 VM，建議使用 SLES 12 SP1 for HPC 映像或 CentOS 型 7.1 HPC。</span><span class="sxs-lookup"><span data-stu-id="6a731-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="6a731-116">在 CentOS 型 HPC 映像上， **yum** 組態檔中已停用核心更新。</span><span class="sxs-lookup"><span data-stu-id="6a731-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="6a731-117">這是因為 Linux RDMA 驅動程式以 RPM 封裝散發，如果更新核心，驅動程式更新可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="6a731-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="6a731-118">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="6a731-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="6a731-119">視您選擇的 Marketplace 映像而定，可能需要個別的 Intel MPI 授權、安裝或組態，如下︰</span><span class="sxs-lookup"><span data-stu-id="6a731-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="6a731-120">**SLES 12 SP1 for HPC 映像** - Intel MPI 封裝是在 VM 上散發。</span><span class="sxs-lookup"><span data-stu-id="6a731-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="6a731-121">執行下列命令進行安裝：</span><span class="sxs-lookup"><span data-stu-id="6a731-121">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="6a731-122">**CentOS 型 HPC 映像** - 已經安裝 Intel MPI 5.1。</span><span class="sxs-lookup"><span data-stu-id="6a731-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="6a731-123">必須進行額外的系統設定，才能在叢集 VM 上執行 MPI 作業。</span><span class="sxs-lookup"><span data-stu-id="6a731-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="6a731-124">例如，在 VM 叢集上，您必須在計算節點之間建立信任關係。</span><span class="sxs-lookup"><span data-stu-id="6a731-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="6a731-125">如需了解一般設定，請參閱[設定 Linux RDMA 叢集以執行 MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6a731-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="6a731-126">HPC Pack 和 Linux 的考量</span><span class="sxs-lookup"><span data-stu-id="6a731-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="6a731-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)是 Microsoft 的免費 HPC 叢集和作業管理解決方案，提供您一個搭配 Linux 使用計算密集型執行個體的選項。</span><span class="sxs-lookup"><span data-stu-id="6a731-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="6a731-128">HPC Pack 的最新版本支援讓數個 Linux 散發套件在部署於 Azure VM 中、由 Windows Server 前端節點管理的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="6a731-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="6a731-129">搭配支援 RDMA 且執行 Intel MPI 的 Linux 計算節點時，HPC Pack 可以排定及執行存取 RDMA 網路的 Linux MPI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a731-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="6a731-130">如需詳細資訊，請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6a731-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="6a731-131">網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="6a731-131">Network topology considerations</span></span>
* <span data-ttu-id="6a731-132">在 Azure 中具備 RDMA 功能的 Linux VM 上，Eth1 會保留給 RDMA 網路流量使用。</span><span class="sxs-lookup"><span data-stu-id="6a731-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="6a731-133">請勿變更任何 Eth1 設定或參考到此網路之組態檔中的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="6a731-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="6a731-134">Eth0 會保留給一般 Azure 網路流量。</span><span class="sxs-lookup"><span data-stu-id="6a731-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="6a731-135">在 Azure 中，不支援透過 InfiniBand (IB) 的 IP。</span><span class="sxs-lookup"><span data-stu-id="6a731-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="6a731-136">僅支援透過 IB 的 RDMA。</span><span class="sxs-lookup"><span data-stu-id="6a731-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6a731-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a731-137">Next steps</span></span>
* <span data-ttu-id="6a731-138">如需有關計算密集型大小的可用性和價格的詳細資料，請參閱 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)。</span><span class="sxs-lookup"><span data-stu-id="6a731-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="6a731-139">如需儲存體容量與磁碟詳細資訊，請參閱[虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6a731-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="6a731-140">若要開始在 Linux 上部署及使用具有 RDMA 的計算密集型大小，請參閱[設定 Linux RDMA 叢集以執行 MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6a731-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

