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
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="2dbbe-103">Azure 中的 Linux 虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="2dbbe-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="2dbbe-104">這篇文章描述 hello 可用大小和選項 hello Azure 虛擬機器，您可以使用 toorun Linux 應用程式和工作負載。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="2dbbe-105">它也提供部署考量 toobe 留意，當您計劃 toouse 這些資源。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="2dbbe-106">本文也適用於 [Windows 虛擬機器](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="2dbbe-107">類型</span><span class="sxs-lookup"><span data-stu-id="2dbbe-107">Type</span></span>                     | <span data-ttu-id="2dbbe-108">大小</span><span class="sxs-lookup"><span data-stu-id="2dbbe-108">Sizes</span></span>           |    <span data-ttu-id="2dbbe-109">說明</span><span class="sxs-lookup"><span data-stu-id="2dbbe-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="2dbbe-110">一般用途</span><span class="sxs-lookup"><span data-stu-id="2dbbe-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="2dbbe-111">Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7,</span><span class="sxs-lookup"><span data-stu-id="2dbbe-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="2dbbe-112">CPU 與記憶體的比例平均。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="2dbbe-113">適用於測試和開發、 toomedium 小型資料庫，而且低 toomedium 流量的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="2dbbe-114">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="2dbbe-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="2dbbe-115">Fs、F</span><span class="sxs-lookup"><span data-stu-id="2dbbe-115">Fs, F</span></span>             | <span data-ttu-id="2dbbe-116">CPU 與記憶體的比例高。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="2dbbe-117">適用於中流量 Web 伺服器、網路設備、批次處理，以及應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="2dbbe-118">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="2dbbe-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="2dbbe-119">Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D</span><span class="sxs-lookup"><span data-stu-id="2dbbe-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="2dbbe-120">記憶體與 CPU 的比例高。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="2dbbe-121">太棒了關聯式資料庫伺服器、 中度 toolarge 快取，以及記憶體中分析。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="2dbbe-122">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="2dbbe-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="2dbbe-123">Ls</span><span class="sxs-lookup"><span data-stu-id="2dbbe-123">Ls</span></span>                | <span data-ttu-id="2dbbe-124">高磁碟輸送量及 IO。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-124">High disk throughput and IO.</span></span> <span data-ttu-id="2dbbe-125">適用於巨量資料、SQL 及 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="2dbbe-126">GPU</span><span class="sxs-lookup"><span data-stu-id="2dbbe-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="2dbbe-127">NV、NC</span><span class="sxs-lookup"><span data-stu-id="2dbbe-127">NV, NC</span></span>            | <span data-ttu-id="2dbbe-128">以大量圖形轉譯和視訊編輯為目標的特製化虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="2dbbe-129">有單一或多個 GPU 可供使用。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="2dbbe-130">高效能計算</span><span class="sxs-lookup"><span data-stu-id="2dbbe-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="2dbbe-131">H、A8-11</span><span class="sxs-lookup"><span data-stu-id="2dbbe-131">H, A8-11</span></span>          | <span data-ttu-id="2dbbe-132">速度最快、功能最強的 CPU 虛擬機器，搭載選配的高輸送量網路介面 (RDMA)。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="2dbbe-133">如需定價的 hello 各種大小資訊，請參閱[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="2dbbe-134">如需了解 Azure 區域中的 VM 大小可用性，請參閱 [依區域提供的產品](https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="2dbbe-135">請參閱 toosee Azure Vm 上的一般限制[Azure 訂用帳戶和服務限制、 配額和條件約束](../../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="2dbbe-136">深入了解 [Azure 計算單位 (ACU)](../windows/acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="2dbbe-137">Rest API</span><span class="sxs-lookup"><span data-stu-id="2dbbe-137">Rest API</span></span>

<span data-ttu-id="2dbbe-138">如需使用 hello REST API tooquery VM 大小的資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2dbbe-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="2dbbe-139">列出調整大小的可用虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="2dbbe-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="2dbbe-140">列出訂用帳戶的可用虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="2dbbe-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="2dbbe-141">列出可用性設定組中可用的虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="2dbbe-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="2dbbe-142">ACU</span><span class="sxs-lookup"><span data-stu-id="2dbbe-142">ACU</span></span>

<span data-ttu-id="2dbbe-143">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="2dbbe-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dbbe-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dbbe-144">Next steps</span></span>

<span data-ttu-id="2dbbe-145">進一步了解 hello 不同 VM 可使用大小：</span><span class="sxs-lookup"><span data-stu-id="2dbbe-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="2dbbe-146">一般用途</span><span class="sxs-lookup"><span data-stu-id="2dbbe-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="2dbbe-147">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="2dbbe-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="2dbbe-148">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="2dbbe-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="2dbbe-149">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="2dbbe-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="2dbbe-150">GPU</span><span class="sxs-lookup"><span data-stu-id="2dbbe-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="2dbbe-151">高效能計算</span><span class="sxs-lookup"><span data-stu-id="2dbbe-151">High performance compute</span></span>](sizes-hpc.md)



