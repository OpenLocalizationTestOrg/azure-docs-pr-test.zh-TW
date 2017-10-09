---
title: "hello 定域機組中的 aaaLinux HPC Pack 叢集選項 |Microsoft 文件"
description: "了解使用 Microsoft HPC Pack toocreate 選項和管理 Linux 高效能運算 (HPC) 叢集 hello Azure 雲端中"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="397db-103">使用 HPC Pack toocreate 選項和管理 Azure 中 Linux 工作負載的 HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="397db-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="397db-104">本文著重在選項 toouse HPC Pack toorun Linux 工作負載。</span><span class="sxs-lookup"><span data-stu-id="397db-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="397db-105">另有[使用 HPC Pack 執行 Windows HPC 工作負載](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)的選項。</span><span class="sxs-lookup"><span data-stu-id="397db-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="397db-106">在 Azure VM 中執行 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="397db-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="397db-107">Azure 範本</span><span class="sxs-lookup"><span data-stu-id="397db-107">Azure templates</span></span>
* <span data-ttu-id="397db-108">(GitHub) [HPC Pack 2016 叢集範本](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="397db-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="397db-109">(Marketplace) [HPC Pack cluster for Linux workloads (適用於 Linux 工作負載的 HPC Pack 叢集)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="397db-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="397db-110">(快速入門) [Create an HPC cluster with Linux compute nodes (使用 Linux 計算節點建立 HPC 叢集)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="397db-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="397db-111">PowerShell 部署指令碼</span><span class="sxs-lookup"><span data-stu-id="397db-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="397db-112">Hello HPC Pack IaaS 部署指令碼以建立 Linux HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="397db-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="397db-113">教學課程</span><span class="sxs-lookup"><span data-stu-id="397db-113">Tutorials</span></span>
* [<span data-ttu-id="397db-114">教學課程：開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點</span><span class="sxs-lookup"><span data-stu-id="397db-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="397db-115">教學課程：在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="397db-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="397db-116">教學課程：在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="397db-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="397db-117">教學課程：在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="397db-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="397db-118">叢集管理</span><span class="sxs-lookup"><span data-stu-id="397db-118">Cluster management</span></span>
* [<span data-ttu-id="397db-119">提交 Azure 中的工作 tooan HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="397db-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="397db-120">HPC Pack 中的作業管理</span><span class="sxs-lookup"><span data-stu-id="397db-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="397db-121">建立 MPI 工作負載的 RDMA 叢集</span><span class="sxs-lookup"><span data-stu-id="397db-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="397db-122">教學課程：在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="397db-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="397db-123">設定 Linux RDMA 叢集 toorun MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="397db-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

