---
title: "在 Azure 中的 aaaWindows VM 大小 |Microsoft 文件"
description: "列出可用的 Windows Azure 中的虛擬機器 hello 不同大小。"
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Azure 中 Windows 虛擬機器的大小

這篇文章描述 hello 可用大小和選項 hello 程式的 Windows 應用程式和工作負載，您可以使用 toorun 的 Azure 虛擬機器。 它也提供部署考量 toobe 留意，當您計劃 toouse 這些資源。  本文也適用於 [Linux 虛擬機器](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。


| 類型                     | 大小           |    說明       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [一般用途](sizes-general.md)          | Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7 | CPU 與記憶體的比例平均。 適用於測試和開發、 toomedium 小型資料庫，而且低 toomedium 流量的網頁伺服器。 |
| [計算最佳化](sizes-compute.md)        | Fs、F             | CPU 與記憶體的比例高。 適用於中流量 Web 伺服器、網路設備、批次處理，以及應用程式伺服器。        |
| [記憶體最佳化](../virtual-machines-windows-sizes-memory.md)         | Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D   | 記憶體與 CPU 的比例高。 太棒了關聯式資料庫伺服器、 中度 toolarge 快取，以及記憶體中分析。                 |
| [儲存體最佳化](../virtual-machines-windows-sizes-storage.md)        | Ls                | 高磁碟輸送量及 IO。 適用於巨量資料、SQL 及 NoSQL 資料庫。                                                         |
| [GPU](sizes-gpu.md)            | NV、NC            | 以大量圖形轉譯和視訊編輯為目標的特製化虛擬機器。 有單一或多個 GPU 可供使用。       |
| [高效能計算](sizes-hpc.md) | H、A8-11          | 速度最快、功能最強的 CPU 虛擬機器，搭載選配的高輸送量網路介面 (RDMA)。 

<br> 

- 如需定價的 hello 各種大小資訊，請參閱[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)。 
- 請參閱 toosee Azure Vm 上的一般限制[Azure 訂用帳戶和服務限制、 配額和條件約束](../../azure-subscription-service-limits.md)。
- 儲存體成本是單獨根據 hello 儲存體帳戶中使用的頁面計算。 如需詳細資料，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。
- 深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。



## <a name="rest-api"></a>Rest API

如需使用 hello REST API tooquery VM 大小的資訊，請參閱 hello 下列：

- [列出調整大小的可用虛擬機器大小](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [列出訂用帳戶的可用虛擬機器大小](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [列出可用性設定組中可用的虛擬機器大小](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。

## <a name="next-steps"></a>後續步驟

進一步了解 hello 不同 VM 可使用大小：
- [一般用途](sizes-general.md)
- [計算最佳化](sizes-compute.md)
- [記憶體最佳化](../virtual-machines-windows-sizes-memory.md)
- [儲存體最佳化](../virtual-machines-windows-sizes-storage.md)
- [GPU 最佳化](sizes-gpu.md)
- [高效能計算](sizes-hpc.md)



