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
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>使用 HPC Pack toocreate 選項和管理 Azure 中 Linux 工作負載的 HPC 叢集
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

本文著重在選項 toouse HPC Pack toorun Linux 工作負載。 另有[使用 HPC Pack 執行 Windows HPC 工作負載](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)的選項。

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>在 Azure VM 中執行 HPC Pack 叢集
### <a name="azure-templates"></a>Azure 範本
* (GitHub) [HPC Pack 2016 叢集範本](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [HPC Pack cluster for Linux workloads (適用於 Linux 工作負載的 HPC Pack 叢集)](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (快速入門) [Create an HPC cluster with Linux compute nodes (使用 Linux 計算節點建立 HPC 叢集)](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>PowerShell 部署指令碼
* [Hello HPC Pack IaaS 部署指令碼以建立 Linux HPC 叢集](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>教學課程
* [教學課程：開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [教學課程：在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 NAMD](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [教學課程：在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [教學課程：在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 STAR-CCM+](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>叢集管理
* [提交 Azure 中的工作 tooan HPC Pack 叢集](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack 中的作業管理](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>建立 MPI 工作負載的 RDMA 叢集
* [教學課程：在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [設定 Linux RDMA 叢集 toorun MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

