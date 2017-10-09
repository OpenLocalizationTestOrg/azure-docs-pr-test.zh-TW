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
# <a name="high-performance-compute-linux-vm-sizes"></a>高效能運算 Linux VM 大小

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>支援 RDMA 的執行個體
子集 hello 需要大量計算執行個體 （H16r、 H16mr、 A8、 A9） 功能的網路介面，遠端直接記憶體存取 (RDMA) 連線。 這個介面是另外 toohello 標準 Azure 網路介面可用 tooother VM 大小。 
  
這個介面允許 hello 具備 RDMA 功能的執行個體 toocommunicate 透過 InfiniBand 網路，在 H16r 和 H16mr 虛擬機器的 FDR 率和 QDR 率的 A8 和 A9 虛擬機器上運作。 Hello 延展性和效能的訊息傳遞介面 (MPI) 應用程式，可以提高這些具備 RDMA 功能。

下列是具備 RDMA 功能的 Linux Vm tooaccess hello Azure RDMA 網路需求：
 
* **分佈**-您必須將 Vm 從具備 RDMA 功能 SUSE Linux Enterprise Server (SLES) 部署或 Rogue Wave 軟體 (先前稱為 OpenLogic) CentOS 架構 HPC 映像中的 hello Azure Marketplace。 hello 下列 Marketplace 映像支援 RDMA 連線能力：
  
    * SLES 12 SP1 for HPC 或 SLES 12 SP1 for HPC (Premium)
    
    * CentOS 型 7.3 HPC、CentOS 型 7.1 HPC、CentOS 型 6.8 HPC 或 CentOS 型 6.5 HPC  
 
        > [!NOTE]
        > 針對 H 系列 VM，建議使用 SLES 12 SP1 for HPC 映像或 CentOS 型 7.1 或更新版本的 HPC。
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
    
    其他系統設定為叢集 Vm 上的所需的 toorun MPI 工作。 例如，在叢集上的 Vm，您需要 tooestablish hello 之間信任計算節點。 一般設定，請參閱[設定 Linux RDMA 叢集 toorun MPI 應用程式](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>網路拓撲考量
* 在 Azure 中具備 RDMA 功能的 Linux VM 上，Eth1 會保留給 RDMA 網路流量使用。 請勿變更任何 Eth1 設定或 hello 組態檔參考 toothis 網路中的任何資訊。 Eth0 會保留給一般 Azure 網路流量。

* 在 Azure 中，不支援透過 InfiniBand (IB) 的 IP。 僅支援透過 IB 的 RDMA。

## <a name="using-hpc-pack"></a>使用 HPC Pack
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)，Microsoft 的免費 HPC 叢集和作業管理方案，是為您的 Linux toouse hello 大量計算執行個體的其中一個選項。 hello 的 HPC Pack 的最新版本都支援數個 toorun 上的運算節點管理的 Windows Server 的前端節點的 Azure Vm 中部署的 Linux 散發套件。 具有 RDMA 功能的 Linux 運算節點執行 Intel MPI HPC Pack 可以排程，並執行 Linux MPI 應用程式存取 hello RDMA 網路。 請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

## <a name="other-sizes"></a>其他大小
- [一般用途](sizes-general.md)
- [計算最佳化](sizes-compute.md)
- [記憶體最佳化](sizes-memory.md)
- [儲存體最佳化](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>後續步驟

- tooget 啟動部署與使用需要大量計算的大小與 RDMA on Linux，請參閱[Linux RDMA 叢集 toorun MPI 應用程式設定](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

- 深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。




