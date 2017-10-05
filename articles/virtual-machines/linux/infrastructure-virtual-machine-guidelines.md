---
title: "Azure Linux 虛擬機器指導方針 | Microsoft Docs"
description: "了解將 Linux 虛擬機器部署到 Azure 中的關鍵設計和實作指導方針"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 2d886795b301ab79272cae10a53831fd44c18f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a><span data-ttu-id="c9fb2-103">適用於 Linux 的 Azure 虛擬機器指導方針</span><span class="sxs-lookup"><span data-stu-id="c9fb2-103">Azure virtual machines guidelines for Linux</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="c9fb2-104">本文著重於了解在 Azure 環境內建立及管理虛擬機器 (VM) 的必要計畫步驟。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-104">This article focuses on understanding the required planning steps for creating and managing virtual machines (VMs) within your Azure environment.</span></span>

## <a name="implementation-guidelines-for-vms"></a><span data-ttu-id="c9fb2-105">VM 的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="c9fb2-105">Implementation guidelines for VMs</span></span>
<span data-ttu-id="c9fb2-106">决策：</span><span class="sxs-lookup"><span data-stu-id="c9fb2-106">Decisions:</span></span>

* <span data-ttu-id="c9fb2-107">您針對各種應用程式層級和基礎結構元件將需要多少 VM？</span><span class="sxs-lookup"><span data-stu-id="c9fb2-107">How many VMs do you require for your various application tiers and components of your infrastructure?</span></span>
* <span data-ttu-id="c9fb2-108">每個 VM 需要什麼 CPU 和記憶體資源？而儲存體需求為何？</span><span class="sxs-lookup"><span data-stu-id="c9fb2-108">What CPU and memory resources does each VM need, and what are the storage requirements?</span></span>

<span data-ttu-id="c9fb2-109">工作：</span><span class="sxs-lookup"><span data-stu-id="c9fb2-109">Tasks:</span></span>

* <span data-ttu-id="c9fb2-110">定義應用程式的工作負載，以及 VM 所需的資源。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-110">Define the workloads for your application and the resources the VMs require.</span></span>
* <span data-ttu-id="c9fb2-111">以適當的 VM 大小和儲存體類型，對齊每個 VM 的資源需求。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-111">Align the resource demands for each VM with the appropriate VM size and storage type.</span></span>
* <span data-ttu-id="c9fb2-112">針對基礎結構的不同層級和元件定義您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-112">Define your resource groups for the different tiers and components of your infrastructure.</span></span>
* <span data-ttu-id="c9fb2-113">定義您的 VM 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-113">Define your VM naming convention.</span></span>
* <span data-ttu-id="c9fb2-114">使用 Azure CLI、入口網站，或 Resource Manager 範本建立 VM。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-114">Create your VMs using the Azure CLI, web portal, or with Resource Manager templates.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="c9fb2-115">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c9fb2-115">Virtual machines</span></span>
<span data-ttu-id="c9fb2-116">您 Azure 環境內的其中一個主要資源很可能是 VM。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-116">One of the main resources within your Azure environment is likely VMs.</span></span> <span data-ttu-id="c9fb2-117">這個資源是您執行應用程式、資料庫、驗證服務等項目的位置。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-117">This resource is where you run your applications, databases, authentication services, etc.</span></span>

<span data-ttu-id="c9fb2-118">請務必了解 [不同的 VM 大小](sizes.md) ，以根據效能和成本觀點正確評估您環境的大小。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-118">It is important to understand the [different VM sizes](sizes.md) to correctly size your environment from a performance and cost perspective.</span></span> <span data-ttu-id="c9fb2-119">如果您的 VM 沒有足夠的 CPU 核心數或記憶體，無論您的應用程式設計及開發得多好，它的效能都會受到影響。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-119">If your VMs do not have enough CPU cores or memory, performance of your application suffers regardless of how well it is designed and developed.</span></span> <span data-ttu-id="c9fb2-120">做為開始，請檢閱每個 VM 系列的建議工作負載，並決定在基礎結構中要用於每個元件的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-120">Review the suggested workloads for each VM series as a starting point as you decide which size VM to use for each component in your infrastructure.</span></span> <span data-ttu-id="c9fb2-121">您可以在部署後 [變更 VM 的大小](change-vm-size.md) 。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-121">You can [change the size of a VM](change-vm-size.md) after deployment.</span></span>

<span data-ttu-id="c9fb2-122">儲存體在 VM 效能中扮演重要的角色。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-122">Storage plays a key role in VM performance.</span></span> <span data-ttu-id="c9fb2-123">您可以選擇使用一般旋轉磁碟的標準儲存體，或是選擇使用 SSD 磁碟的進階儲存體，以取得高 I/O 工作負載和尖端效能。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-123">You can use Standard storage, that uses regular spinning disks, or Premium storage for high I/O workloads and peak performance, that use SSD disks.</span></span> <span data-ttu-id="c9fb2-124">針對 VM 大小，有一些選取儲存媒體的成本考量。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-124">As with the VM size, there are cost considerations to selecting the storage medium.</span></span> <span data-ttu-id="c9fb2-125">您可以閱讀 [storage infrastructure guidelines (儲存體基礎結構指導方針) 一文](infrastructure-storage-solutions-guidelines.md) ，以了解針對 VM 的最佳效能設計適當儲存體的方式。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-125">You can read the [storage infrastructure guidelines article](infrastructure-storage-solutions-guidelines.md) to understand how to design appropriate storage for optimum performance of your VMs.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="c9fb2-126">資源群組</span><span class="sxs-lookup"><span data-stu-id="c9fb2-126">Resource groups</span></span>
<span data-ttu-id="c9fb2-127">VM 之類的元件會以邏輯方式分組，以方便使用 [Azure 資源群組](../../azure-resource-manager/resource-group-overview.md)進行管理和維護。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-127">Components such as VMs are logically grouped for ease of management and maintenance using [Azure Resource Groups](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c9fb2-128">透過使用資源群組，您可以建立、管理並監視組成特定應用程式的所有資源。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-128">By using resource groups, you can create, manage, and monitor all the resources that make up a given application.</span></span> <span data-ttu-id="c9fb2-129">您也可以實作 [角色型存取控制](../../active-directory/role-based-access-control-what-is.md) ，以授與小組中的其他人員存取所需資源的權限。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-129">You can also implement [role-based access controls](../../active-directory/role-based-access-control-what-is.md) to grant access to others within your team to only the resources they require.</span></span> <span data-ttu-id="c9fb2-130">請花上一點時間計畫您的資源群組和角色指派。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-130">Take time to plan out your resource groups and role assignments.</span></span> <span data-ttu-id="c9fb2-131">實際設計並實作資源群組有數個不同的方式，因此請務必閱讀 [資源群組指導方針一文](infrastructure-resource-groups-guidelines.md) ，以了解建置 VM 的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-131">There are different approaches to actually design and implement resource groups, so be sure to read the [resource groups guidelines article](infrastructure-resource-groups-guidelines.md) to understand how best to build out your VMs.</span></span>

## <a name="templates"></a><span data-ttu-id="c9fb2-132">範本</span><span class="sxs-lookup"><span data-stu-id="c9fb2-132">Templates</span></span>
<span data-ttu-id="c9fb2-133">您可以建置範本 (由宣告式 JSON 檔案定義) 以建立您的 VM。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-133">You can build templates, defined by declarative JSON files, to create your VMs.</span></span> <span data-ttu-id="c9fb2-134">範本除了 VM 之外，通常也會建置必要的儲存體、網路、網路介面、IP 位址等。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-134">Templates typically also build the required storage, networking, network interfaces, IP addressing, etc. along with the VMs themselves.</span></span> <span data-ttu-id="c9fb2-135">您可以針對開發和測試目的使用範本來建立一致且可重現的環境，以輕鬆複寫生產環境，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-135">You can use templates to create consistent, reproducible environments for development and testing purposes to easily replicate production environments and vice versa.</span></span> <span data-ttu-id="c9fb2-136">您可以深入了解[建置並使用範本](../../azure-resource-manager/resource-group-overview.md#template-deployment)，以了解將它們用於建立及部署 VM 的方式。</span><span class="sxs-lookup"><span data-stu-id="c9fb2-136">You can read more about [building and using templates](../../azure-resource-manager/resource-group-overview.md#template-deployment) to understand how you can use them for creating and deploying your VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9fb2-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9fb2-137">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

