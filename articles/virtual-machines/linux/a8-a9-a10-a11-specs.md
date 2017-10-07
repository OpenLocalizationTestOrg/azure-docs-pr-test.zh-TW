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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>關於 Linux 的 H 系列和計算密集型 A 系列 VM
以下是背景資訊和使用的一些考量 hello 較新的 Azure H 數列也稱為 hello 較早的 A8、 A9、 A10 和 A11 大小*需要大量計算*執行個體。 本文將焦點放在使用這些 Linux VM 大小。 您也可以針對 [Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 使用它們。 

如需基本規格、儲存體容量與磁碟的詳細資料，請參閱[虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>存取 toohello RDMA 網路
您可以建立具備 RDMA 功能 hello 下列支援的 Linux HPC 分佈和 hello Azure RDMA 網路的支援的 MPI 實作 tootake 優點的其中一個執行的 Linux Vm 的叢集。 請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)部署選項和範例的組態步驟。

* **分佈**-您必須將 Vm 從具備 RDMA 功能 SUSE Linux Enterprise Server (SLES) 部署或 Rogue Wave 軟體 (先前稱為 OpenLogic) CentOS 架構 HPC 映像中的 hello Azure Marketplace。 hello 下列 Marketplace 映像支援 RDMA 連線能力：
  
    * SLES 12 SP1 for HPC、SLES 12 SP1 for HPC (Premium)
    
    * CentOS 型 7.1 HPC、CentOS 型 6.5 HPC  
 
        > [!NOTE]
        > 針對 H 系列 VM，建議使用 SLES 12 SP1 for HPC 映像或 CentOS 型 7.1 HPC。
        >
        > Hello CentOS 架構 HPC 映像，核心會停用更新中 hello **yum**組態檔。 這是因為 hello Linux RDMA 驅動程式散發作為 RPM 套件，而且如果 hello 核心會更新驅動程式的更新可能無法運作。
        > 
        > 
* **MPI** - Intel MPI Library 5.x
  
    根據 hello Marketplace 映像您選擇，個別的授權，安裝，或 Intel MPI 的組態可能需要，如下所示： 
  
  * **HPC 映像的 SLES 12 SP1** -Intel MPI 套件發佈 hello VM 上。 執行下列命令的 hello 來安裝：

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **CentOS 型 HPC 映像** - 已經安裝 Intel MPI 5.1。  
    
    其他系統設定為叢集 Vm 上的所需的 toorun MPI 工作。 例如，在叢集上的 Vm，您需要 tooestablish hello 之間信任計算節點。 一般設定，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

## <a name="considerations-for-hpc-pack-and-linux"></a>HPC Pack 和 Linux 的考量
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)，Microsoft 的免費 HPC 叢集和作業管理方案，提供您的第一個選項與 Linux toouse hello 大量計算執行個體。 hello 的 HPC Pack 的最新版本都支援數個 toorun 上的運算節點管理的 Windows Server 的前端節點的 Azure Vm 中部署的 Linux 散發套件。 具有 RDMA 功能的 Linux 運算節點執行 Intel MPI HPC Pack 可以排程，並執行 Linux MPI 應用程式存取 hello RDMA 網路。 tooget 啟動，請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

## <a name="network-topology-considerations"></a>網路拓撲考量
* 在 Azure 中具備 RDMA 功能的 Linux VM 上，Eth1 會保留給 RDMA 網路流量使用。 請勿變更任何 Eth1 設定或 hello 組態檔參考 toothis 網路中的任何資訊。 Eth0 會保留給一般 Azure 網路流量。
* 在 Azure 中，不支援透過 InfiniBand (IB) 的 IP。 僅支援透過 IB 的 RDMA。



## <a name="next-steps"></a>後續步驟
* 如需可用性和價格 hello 需要大量計算的大小的詳細資訊，請參閱[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)。
* 如需儲存體容量與磁碟詳細資訊，請參閱[虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* tooget 啟動部署與使用需要大量計算的大小與 RDMA on Linux，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

