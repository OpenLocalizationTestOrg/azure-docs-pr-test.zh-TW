---
title: "aaaAzure Linux VM 大小-GPU |Microsoft 文件"
description: "列出 hello 不同最佳化 GPU 可用的大小在 Azure 中 Linux 虛擬機器。"
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
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a>GPU Linux VM 大小

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

如需驅動程式安裝和驗證步驟，請參閱 [Linux 的 N 系列驅動程式安裝](n-series-driver-setup.md)。

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* 我們不建議您安裝伺服器或其他系統的 Ubuntu NC Vm 上使用 hello nouveau 驅動程式。 在安裝之前 NVIDIA GPU 驅動程式，您需要 toodisable hello nouveau 驅動程式。  

## <a name="other-sizes"></a>其他大小
- [一般用途](sizes-general.md)
- [計算最佳化](sizes-compute.md)
- [記憶體最佳化](sizes-memory.md)
- [儲存體最佳化](sizes-storage.md)
- [高效能計算](sizes-hpc.md)

## <a name="next-steps"></a>後續步驟
深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。