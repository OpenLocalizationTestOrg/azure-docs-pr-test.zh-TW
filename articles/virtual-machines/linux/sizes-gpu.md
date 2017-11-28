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
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="89213-103">GPU Linux VM 大小</span><span class="sxs-lookup"><span data-stu-id="89213-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="89213-104">如需驅動程式安裝和驗證步驟，請參閱 [Linux 的 N 系列驅動程式安裝](n-series-driver-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="89213-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="89213-105">我們不建議您安裝伺服器或其他系統的 Ubuntu NC Vm 上使用 hello nouveau 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="89213-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="89213-106">在安裝之前 NVIDIA GPU 驅動程式，您需要 toodisable hello nouveau 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="89213-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="89213-107">其他大小</span><span class="sxs-lookup"><span data-stu-id="89213-107">Other sizes</span></span>
- [<span data-ttu-id="89213-108">一般用途</span><span class="sxs-lookup"><span data-stu-id="89213-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="89213-109">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="89213-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="89213-110">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="89213-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="89213-111">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="89213-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="89213-112">高效能計算</span><span class="sxs-lookup"><span data-stu-id="89213-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="89213-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89213-113">Next steps</span></span>
<span data-ttu-id="89213-114">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="89213-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>