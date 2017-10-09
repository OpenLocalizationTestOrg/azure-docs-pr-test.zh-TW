---
title: "在 Azure 中的 aaaLinux VM 大小 |Microsoft 文件"
description: "列出 hello 不同大小適用於 Azure 中 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a>Azure 中的 Linux 虛擬機器大小
這篇文章描述 hello 可用大小和選項 hello Azure 虛擬機器，您可以使用 toorun Linux 應用程式和工作負載。 它也提供部署考量 toobe 留意，當您計劃 toouse 這些資源。 本文也適用於 [Windows 虛擬機器](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。


| 類型                     | 大小           |    說明       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [一般用途](sizes-general.md)          | Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7,  | CPU 與記憶體的比例平均。 適用於測試和開發、 toomedium 小型資料庫，而且低 toomedium 流量的網頁伺服器。 |
| [計算最佳化](sizes-compute.md)        | Fs、F             | CPU 與記憶體的比例高。 適用於中流量 Web 伺服器、網路設備、批次處理，以及應用程式伺服器。        |
| [記憶體最佳化](sizes-memory.md)         | Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D   | 記憶體與 CPU 的比例高。 太棒了關聯式資料庫伺服器、 中度 toolarge 快取，以及記憶體中分析。                 |
| [儲存體最佳化](sizes-storage.md)        | Ls                | 高磁碟輸送量及 IO。 適用於巨量資料、SQL 及 NoSQL 資料庫。                                                         |
| [GPU](sizes-gpu.md)            | NV、NC            | 以大量圖形轉譯和視訊編輯為目標的特製化虛擬機器。 有單一或多個 GPU 可供使用。       |
| [高效能計算](sizes-hpc.md) | H、A8-11          | 速度最快、功能最強的 CPU 虛擬機器，搭載選配的高輸送量網路介面 (RDMA)。 

<br>

- 如需定價的 hello 各種大小資訊，請參閱[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)。 
- 如需了解 Azure 區域中的 VM 大小可用性，請參閱 [依區域提供的產品](https://azure.microsoft.com/regions/services/)。
- 請參閱 toosee Azure Vm 上的一般限制[Azure 訂用帳戶和服務限制、 配額和條件約束](../../azure-subscription-service-limits.md)。
- 深入了解 [Azure 計算單位 (ACU)](../windows/acu.md) 如何協助您比較各個 Azure SKU 的計算效能。


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
- [記憶體最佳化](sizes-memory.md)
- [儲存體最佳化](sizes-storage.md)
- [GPU](sizes-gpu.md)
- [高效能計算](sizes-hpc.md)



