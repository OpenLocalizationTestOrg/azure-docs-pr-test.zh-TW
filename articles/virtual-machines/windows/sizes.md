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
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="83b2f-103">Azure 中 Windows 虛擬機器的大小</span><span class="sxs-lookup"><span data-stu-id="83b2f-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="83b2f-104">這篇文章描述 hello 可用大小和選項 hello 程式的 Windows 應用程式和工作負載，您可以使用 toorun 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="83b2f-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="83b2f-105">它也提供部署考量 toobe 留意，當您計劃 toouse 這些資源。</span><span class="sxs-lookup"><span data-stu-id="83b2f-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="83b2f-106">本文也適用於 [Linux 虛擬機器](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="83b2f-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="83b2f-107">類型</span><span class="sxs-lookup"><span data-stu-id="83b2f-107">Type</span></span>                     | <span data-ttu-id="83b2f-108">大小</span><span class="sxs-lookup"><span data-stu-id="83b2f-108">Sizes</span></span>           |    <span data-ttu-id="83b2f-109">說明</span><span class="sxs-lookup"><span data-stu-id="83b2f-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="83b2f-110">一般用途</span><span class="sxs-lookup"><span data-stu-id="83b2f-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="83b2f-111">Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7</span><span class="sxs-lookup"><span data-stu-id="83b2f-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="83b2f-112">CPU 與記憶體的比例平均。</span><span class="sxs-lookup"><span data-stu-id="83b2f-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="83b2f-113">適用於測試和開發、 toomedium 小型資料庫，而且低 toomedium 流量的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="83b2f-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="83b2f-114">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="83b2f-115">Fs、F</span><span class="sxs-lookup"><span data-stu-id="83b2f-115">Fs, F</span></span>             | <span data-ttu-id="83b2f-116">CPU 與記憶體的比例高。</span><span class="sxs-lookup"><span data-stu-id="83b2f-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="83b2f-117">適用於中流量 Web 伺服器、網路設備、批次處理，以及應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="83b2f-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="83b2f-118">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="83b2f-119">Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D</span><span class="sxs-lookup"><span data-stu-id="83b2f-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="83b2f-120">記憶體與 CPU 的比例高。</span><span class="sxs-lookup"><span data-stu-id="83b2f-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="83b2f-121">太棒了關聯式資料庫伺服器、 中度 toolarge 快取，以及記憶體中分析。</span><span class="sxs-lookup"><span data-stu-id="83b2f-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="83b2f-122">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="83b2f-123">Ls</span><span class="sxs-lookup"><span data-stu-id="83b2f-123">Ls</span></span>                | <span data-ttu-id="83b2f-124">高磁碟輸送量及 IO。</span><span class="sxs-lookup"><span data-stu-id="83b2f-124">High disk throughput and IO.</span></span> <span data-ttu-id="83b2f-125">適用於巨量資料、SQL 及 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="83b2f-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="83b2f-126">GPU</span><span class="sxs-lookup"><span data-stu-id="83b2f-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="83b2f-127">NV、NC</span><span class="sxs-lookup"><span data-stu-id="83b2f-127">NV, NC</span></span>            | <span data-ttu-id="83b2f-128">以大量圖形轉譯和視訊編輯為目標的特製化虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="83b2f-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="83b2f-129">有單一或多個 GPU 可供使用。</span><span class="sxs-lookup"><span data-stu-id="83b2f-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="83b2f-130">高效能計算</span><span class="sxs-lookup"><span data-stu-id="83b2f-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="83b2f-131">H、A8-11</span><span class="sxs-lookup"><span data-stu-id="83b2f-131">H, A8-11</span></span>          | <span data-ttu-id="83b2f-132">速度最快、功能最強的 CPU 虛擬機器，搭載選配的高輸送量網路介面 (RDMA)。</span><span class="sxs-lookup"><span data-stu-id="83b2f-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="83b2f-133">如需定價的 hello 各種大小資訊，請參閱[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)。</span><span class="sxs-lookup"><span data-stu-id="83b2f-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="83b2f-134">請參閱 toosee Azure Vm 上的一般限制[Azure 訂用帳戶和服務限制、 配額和條件約束](../../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="83b2f-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="83b2f-135">儲存體成本是單獨根據 hello 儲存體帳戶中使用的頁面計算。</span><span class="sxs-lookup"><span data-stu-id="83b2f-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="83b2f-136">如需詳細資料，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="83b2f-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="83b2f-137">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="83b2f-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="83b2f-138">Rest API</span><span class="sxs-lookup"><span data-stu-id="83b2f-138">Rest API</span></span>

<span data-ttu-id="83b2f-139">如需使用 hello REST API tooquery VM 大小的資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="83b2f-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="83b2f-140">列出調整大小的可用虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="83b2f-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="83b2f-141">列出訂用帳戶的可用虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="83b2f-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="83b2f-142">列出可用性設定組中可用的虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="83b2f-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="83b2f-143">ACU</span><span class="sxs-lookup"><span data-stu-id="83b2f-143">ACU</span></span>

<span data-ttu-id="83b2f-144">深入了解 [Azure 計算單位 (ACU)](acu.md) 如何協助您比較各個 Azure SKU 的計算效能。</span><span class="sxs-lookup"><span data-stu-id="83b2f-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83b2f-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83b2f-145">Next steps</span></span>

<span data-ttu-id="83b2f-146">進一步了解 hello 不同 VM 可使用大小：</span><span class="sxs-lookup"><span data-stu-id="83b2f-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="83b2f-147">一般用途</span><span class="sxs-lookup"><span data-stu-id="83b2f-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="83b2f-148">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="83b2f-149">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="83b2f-150">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="83b2f-151">GPU 最佳化</span><span class="sxs-lookup"><span data-stu-id="83b2f-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="83b2f-152">高效能計算</span><span class="sxs-lookup"><span data-stu-id="83b2f-152">High performance compute</span></span>](sizes-hpc.md)



