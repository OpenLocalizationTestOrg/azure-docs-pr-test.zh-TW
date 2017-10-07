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
# <a name="high-performance-compute-vm-sizes"></a>高效能運算 VM 大小

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>支援 RDMA 的執行個體
子集 hello 需要大量計算執行個體 （H16r、 H16mr、 A8、 A9） 功能的網路介面，遠端直接記憶體存取 (RDMA) 連線。 這個介面是另外 toohello 標準 Azure 網路介面可用 tooother VM 大小。 
  
這個介面允許 hello 具備 RDMA 功能的執行個體 toocommunicate 透過 InfiniBand 網路，在 H16r 和 H16mr 虛擬機器的 FDR 率和 QDR 率的 A8 和 A9 虛擬機器上運作。 Hello 延展性和效能的訊息傳遞介面 (MPI) 應用程式，可以提高這些具備 RDMA 功能。

下列是具備 RDMA 功能的 Windows Vm tooaccess hello Azure RDMA 網路需求： 

* **作業系統**
  
  Windows Server 2012 R2、Windows Server 2012
  
  > [!NOTE]
  > Windows Server 2016 目前不支援 Azure 中的 RDMA 連線能力。
  >

* **可用性設定組或雲端服務**– 中部署具備 RDMA 功能的 hello Vm hello 相同可用性設定組 （當您使用 hello Azure Resource Manager 部署模型時） 或 hello 相同雲端服務 （當您使用 hello 傳統部署模型）。 如果您使用 Azure 批次時，必須在 hello hello 具備 RDMA 功能的 Vm 相同的集區。

* **MPI** - Microsoft MPI (MS-MPI) 2012 R2 或更新版本、Intel MPI Library 5.x

  支援的 MPI 實作使用 hello Microsoft Network Direct 介面 toocommunicate 執行個體之間。 

* **RDMA 網路位址空間**-在 Azure 中的 hello RDMA 網路保留 hello 位址空間 172.16.0.0/16。 toorun MPI 應用程式執行個體部署在 Azure 虛擬網路，請確定 hello 虛擬網路位址空間不會重疊 hello RDMA 網路。

* **VM HpcVmDrivers 延伸模組**-上具備 RDMA 功能的 Vm，您必須新增 hello HpcVmDrivers 延伸模組 tooinstall Windows 網路裝置驅動程式的 RDMA 連線能力。 （在某些部署 A8 和 A9 執行個體中，hello HpcVmDrivers 延伸模組會自動加入。）tooadd hello VM 延伸模組 tooa VM，您可以使用[Azure PowerShell](/powershell/azure/overview) cmdlet。 

  
  hello 下列命令安裝 hello 名為現有具備 RDMA 功能的 VM 上的最新版本 1.1 HpcVMDrivers 延伸模組*myVM*中名為 「 hello 資源群組部署*myResourceGroup* hello中*美國西部*區域：

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  如需詳細資訊，請參閱[虛擬機器擴充功能和功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 您也可以使用擴充功能的 Vm 部署在 hello[傳統部署模型](classic/manage-extensions.md)。


## <a name="using-hpc-pack"></a>使用 HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)，Microsoft 的免費 HPC 叢集和作業管理方案，是 toocreate Azure toorun Windows 為基礎的 MPI 應用程式及其他 HPC 工作負載中的運算叢集的第一個選項。 HPC Pack 2012 R2 和更新版本包含執行階段環境的 hello Azure RDMA 網路部署時使用 RDMA 功能的 Vm 的 MS-MPI。




## <a name="other-sizes"></a>其他大小
- [一般用途](sizes-general.md)
- [計算最佳化](sizes-compute.md)
- [記憶體最佳化](../virtual-machines-windows-sizes-memory.md)
- [儲存體最佳化](../virtual-machines-windows-sizes-storage.md)
- [GPU 最佳化](sizes-gpu.md)

## <a name="next-steps"></a>後續步驟

- 檢查清單 toouse hello 需要大量計算執行個體使用 Windows Server 上的 HPC Pack，請參閱[設定 HPC Pack toorun MPI 應用程式與 Windows RDMA 叢集](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

- toouse 大量計算執行個體使用 Azure Batch 執行 MPI 應用程式時看到[使用多個執行個體工作 toorun Azure 批次中的訊息傳遞介面 (MPI) 應用程式](../../batch/batch-mpi.md)。

- 深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。




