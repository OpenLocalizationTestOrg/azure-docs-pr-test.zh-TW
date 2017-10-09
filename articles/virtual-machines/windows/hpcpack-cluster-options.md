---
title: "aaaWindows HPC Pack 叢集 hello 雲端中的選項 |Microsoft 文件"
description: "了解使用 Microsoft HPC Pack toocreate 選項及管理 Windows 高效能運算 (HPC) 叢集 hello Azure 雲端中"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="37d9a-103">使用 HPC Pack toocreate 選項和管理 Azure 中的 Windows HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="37d9a-104">本文著重在選項 toocreate HPC Pack 叢集 toorun Windows 工作負載。</span><span class="sxs-lookup"><span data-stu-id="37d9a-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="37d9a-105">也有一些選項如建立的 HPC Pack 叢集 toorun [Linux HPC 工作負載](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="37d9a-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="37d9a-106">在 Azure VM 中執行 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="37d9a-107">Azure 範本</span><span class="sxs-lookup"><span data-stu-id="37d9a-107">Azure templates</span></span>
* <span data-ttu-id="37d9a-108">(GitHub) [HPC Pack 2016 叢集範本](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="37d9a-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="37d9a-109">(Marketplace) [HPC Pack cluster for Windows workloads (適用於 Windows 工作負載的 HPC Pack 叢集)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="37d9a-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="37d9a-110">(Marketplace) [HPC Pack cluster for Excel workloads (適用於 Excel 工作負載的 HPC Pack 叢集)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="37d9a-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="37d9a-111">(快速入門) [Create an HPC cluster (建立 HPC 叢集)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="37d9a-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="37d9a-112">(快速入門) [Create an HPC cluster with custom compute node image (使用自訂的計算節點映像建立 HPC 叢集)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="37d9a-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="37d9a-113">Azure VM 映像</span><span class="sxs-lookup"><span data-stu-id="37d9a-113">Azure VM images</span></span>
* [<span data-ttu-id="37d9a-114">Windows Server 2016 上的 HPC Pack 2016 前端節點 (英文)</span><span class="sxs-lookup"><span data-stu-id="37d9a-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="37d9a-115">Windows Server 2016 上的 HPC Pack 2016 計算節點 (英文)</span><span class="sxs-lookup"><span data-stu-id="37d9a-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="37d9a-116">Windows Server 2012 R2 上的 HPC Pack 2016 前端節點 (英文)</span><span class="sxs-lookup"><span data-stu-id="37d9a-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="37d9a-117">Windows Server 2012 R2 上的 HPC Pack 2016 計算節點 (英文)</span><span class="sxs-lookup"><span data-stu-id="37d9a-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="37d9a-118">Windows Server 2012 R2 上的 HPC Pack 2012 R2 前端節點 (英文)</span><span class="sxs-lookup"><span data-stu-id="37d9a-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="37d9a-119">Windows Server 2012 R2 上的 HPC Pack 2012 R2 計算節點 (英文)</span><span class="sxs-lookup"><span data-stu-id="37d9a-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="37d9a-120">Windows Server 2012 R2 上含 Excel 的 HPC Pack 運算節點</span><span class="sxs-lookup"><span data-stu-id="37d9a-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="37d9a-121">PowerShell 部署指令碼</span><span class="sxs-lookup"><span data-stu-id="37d9a-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="37d9a-122">以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="37d9a-123">教學課程</span><span class="sxs-lookup"><span data-stu-id="37d9a-123">Tutorials</span></span>
* [<span data-ttu-id="37d9a-124">教學課程：在 Azure 中部署 HPC Pack 2016 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="37d9a-125">教學課程： 開始使用 Azure toorun Excel 中的 HPC Pack 叢集和 SOA 工作負載</span><span class="sxs-lookup"><span data-stu-id="37d9a-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="37d9a-126">手動部署以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="37d9a-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="37d9a-127">設定 hello Azure VM 中部署 HPC Pack 叢集的前端節點</span><span class="sxs-lookup"><span data-stu-id="37d9a-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="37d9a-128">叢集管理</span><span class="sxs-lookup"><span data-stu-id="37d9a-128">Cluster management</span></span>
* [<span data-ttu-id="37d9a-129">在 Azure 中管理 HPC Pack 叢集的運算節點</span><span class="sxs-lookup"><span data-stu-id="37d9a-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="37d9a-130">增加及縮減 HPC Pack 叢集中的 Azure 運算資源</span><span class="sxs-lookup"><span data-stu-id="37d9a-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="37d9a-131">提交 Azure 中的工作 tooan HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="37d9a-132">HPC Pack 中的作業管理</span><span class="sxs-lookup"><span data-stu-id="37d9a-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="37d9a-133">使用 Azure Active Directory 管理 Azure 中的 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="37d9a-134">新增背景工作角色節點 tooan HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="37d9a-135">TooAzure 背景工作執行個體使用 HPC Pack 高載</span><span class="sxs-lookup"><span data-stu-id="37d9a-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="37d9a-136">教學課程：在 Azure 中使用 HPC Pack 設定混合式叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="37d9a-137">在 Azure 中加入 Azure 「 高載 」 節點 tooan HPC Pack 前端節點</span><span class="sxs-lookup"><span data-stu-id="37d9a-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="37d9a-138">與 Azure Batch 整合</span><span class="sxs-lookup"><span data-stu-id="37d9a-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="37d9a-139">TooAzure 批次使用 HPC Pack 高載</span><span class="sxs-lookup"><span data-stu-id="37d9a-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="37d9a-140">建立 MPI 工作負載的 RDMA 叢集</span><span class="sxs-lookup"><span data-stu-id="37d9a-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="37d9a-141">設定 Windows RDMA 叢集與 HPC Pack toorun MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="37d9a-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

