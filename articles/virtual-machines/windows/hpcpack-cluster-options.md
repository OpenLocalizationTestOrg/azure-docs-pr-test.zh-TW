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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>使用 HPC Pack toocreate 選項和管理 Azure 中的 Windows HPC 叢集
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

本文著重在選項 toocreate HPC Pack 叢集 toorun Windows 工作負載。 也有一些選項如建立的 HPC Pack 叢集 toorun [Linux HPC 工作負載](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>在 Azure VM 中執行 HPC Pack 叢集
### <a name="azure-templates"></a>Azure 範本
* (GitHub) [HPC Pack 2016 叢集範本](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [HPC Pack cluster for Windows workloads (適用於 Windows 工作負載的 HPC Pack 叢集)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [HPC Pack cluster for Excel workloads (適用於 Excel 工作負載的 HPC Pack 叢集)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (快速入門) [Create an HPC cluster (建立 HPC 叢集)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (快速入門) [Create an HPC cluster with custom compute node image (使用自訂的計算節點映像建立 HPC 叢集)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Azure VM 映像
* [Windows Server 2016 上的 HPC Pack 2016 前端節點 (英文)](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2016 上的 HPC Pack 2016 計算節點 (英文)](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2012 R2 上的 HPC Pack 2016 前端節點 (英文)](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2 上的 HPC Pack 2016 計算節點 (英文)](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2 上的 HPC Pack 2012 R2 前端節點 (英文)](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Windows Server 2012 R2 上的 HPC Pack 2012 R2 計算節點 (英文)](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Windows Server 2012 R2 上含 Excel 的 HPC Pack 運算節點](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>PowerShell 部署指令碼
* [以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>教學課程
* [教學課程：在 Azure 中部署 HPC Pack 2016 叢集](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [教學課程： 開始使用 Azure toorun Excel 中的 HPC Pack 叢集和 SOA 工作負載](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>手動部署以 hello Azure 入口網站
* [設定 hello Azure VM 中部署 HPC Pack 叢集的前端節點](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>叢集管理
* [在 Azure 中管理 HPC Pack 叢集的運算節點](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [增加及縮減 HPC Pack 叢集中的 Azure 運算資源](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [提交 Azure 中的工作 tooan HPC Pack 叢集](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack 中的作業管理](https://technet.microsoft.com/library/jj899585.aspx)
* [使用 Azure Active Directory 管理 Azure 中的 HPC Pack 叢集](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>新增背景工作角色節點 tooan HPC Pack 叢集
* [TooAzure 背景工作執行個體使用 HPC Pack 高載](https://technet.microsoft.com/library/gg481749.aspx)
* [教學課程：在 Azure 中使用 HPC Pack 設定混合式叢集](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [在 Azure 中加入 Azure 「 高載 」 節點 tooan HPC Pack 前端節點](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>與 Azure Batch 整合
* [TooAzure 批次使用 HPC Pack 高載](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>建立 MPI 工作負載的 RDMA 叢集
* [設定 Windows RDMA 叢集與 HPC Pack toorun MPI 應用程式](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

