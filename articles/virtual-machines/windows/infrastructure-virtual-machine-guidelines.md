---
title: "虛擬機器的指導方針 aaaAzure |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作指導方針將 Windows 虛擬機器部署至 Azure"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f932e65a-437b-48b0-8d70-f61ded8ce1c6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: d2c8043cd5829b54a5d57e56533122e42021797d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-windows"></a><span data-ttu-id="ba689-103">適用於 Windows 的 Azure 虛擬機器指導方針</span><span class="sxs-lookup"><span data-stu-id="ba689-103">Azure virtual machines guidelines for Windows</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="ba689-104">本文著重在所需的規劃步驟來建立及管理虛擬機器 (Vm) 的了解 hello Azure 環境內。</span><span class="sxs-lookup"><span data-stu-id="ba689-104">This article focuses on understanding hello required planning steps for creating and managing virtual machines (VMs) within your Azure environment.</span></span>

## <a name="implementation-guidelines-for-vms"></a><span data-ttu-id="ba689-105">VM 的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="ba689-105">Implementation guidelines for VMs</span></span>
<span data-ttu-id="ba689-106">决策：</span><span class="sxs-lookup"><span data-stu-id="ba689-106">Decisions:</span></span>

* <span data-ttu-id="ba689-107">您針對各種應用程式層級和基礎結構元件將需要多少 VM？</span><span class="sxs-lookup"><span data-stu-id="ba689-107">How many VMs do you require for your various application tiers and components of your infrastructure?</span></span>
* <span data-ttu-id="ba689-108">每個 VM 需要哪些 CPU 和記憶體資源，以及 hello 儲存體需求為何？</span><span class="sxs-lookup"><span data-stu-id="ba689-108">What CPU and memory resources does each VM need, and what are hello storage requirements?</span></span>

<span data-ttu-id="ba689-109">工作：</span><span class="sxs-lookup"><span data-stu-id="ba689-109">Tasks:</span></span>

* <span data-ttu-id="ba689-110">定義 Vm 需要您的應用程式和 hello 資源 hello 的 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="ba689-110">Define hello workloads for your application and hello resources hello VMs require.</span></span>
* <span data-ttu-id="ba689-111">對齊 hello 適當 VM 大小和儲存體類型具有每個 VM 的 hello 資源需求。</span><span class="sxs-lookup"><span data-stu-id="ba689-111">Align hello resource demands for each VM with hello appropriate VM size and storage type.</span></span>
* <span data-ttu-id="ba689-112">定義您的資源群組 hello 不同層和基礎結構的元件。</span><span class="sxs-lookup"><span data-stu-id="ba689-112">Define your resource groups for hello different tiers and components of your infrastructure.</span></span>
* <span data-ttu-id="ba689-113">定義您的 VM 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="ba689-113">Define your VM naming convention.</span></span>
* <span data-ttu-id="ba689-114">建立 Vm 使用 hello Azure PowerShell，web 入口網站，或使用資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="ba689-114">Create your VMs using hello Azure PowerShell, web portal, or with Resource Manager templates.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="ba689-115">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ba689-115">Virtual machines</span></span>
<span data-ttu-id="ba689-116">可能的 Vm hello Azure 環境內的主要資源的其中一個。</span><span class="sxs-lookup"><span data-stu-id="ba689-116">One of hello main resources within your Azure environment is likely VMs.</span></span> <span data-ttu-id="ba689-117">這個資源是您執行應用程式、資料庫、驗證服務等項目的位置。</span><span class="sxs-lookup"><span data-stu-id="ba689-117">This resource is where you run your applications, databases, authentication services, etc.</span></span>

<span data-ttu-id="ba689-118">它是重要的 toounderstand hello[不同的 VM 大小](sizes.md)toocorrectly 大小從效能及成本的觀點來看您的環境。</span><span class="sxs-lookup"><span data-stu-id="ba689-118">It is important toounderstand hello [different VM sizes](sizes.md) toocorrectly size your environment from a performance and cost perspective.</span></span> <span data-ttu-id="ba689-119">如果您的 VM 沒有足夠的 CPU 核心數或記憶體，無論您的應用程式設計及開發得多好，它的效能都會受到影響。</span><span class="sxs-lookup"><span data-stu-id="ba689-119">If your VMs do not have enough CPU cores or memory, performance of your application suffers regardless of how well it is designed and developed.</span></span> <span data-ttu-id="ba689-120">您決定為每個元件的大小 VM toouse 基礎結構中，檢閱 hello 建議針對每個 VM 序列，做為起點的工作負載。</span><span class="sxs-lookup"><span data-stu-id="ba689-120">Review hello suggested workloads for each VM series as a starting point as you decide which size VM toouse for each component in your infrastructure.</span></span> <span data-ttu-id="ba689-121">您可以[變更 VM 大小 hello](resize-vm.md)部署之後。</span><span class="sxs-lookup"><span data-stu-id="ba689-121">You can [change hello size of a VM](resize-vm.md) after deployment.</span></span>

<span data-ttu-id="ba689-122">儲存體在 VM 效能中扮演重要的角色。</span><span class="sxs-lookup"><span data-stu-id="ba689-122">Storage plays a key role in VM performance.</span></span> <span data-ttu-id="ba689-123">您可以選擇使用一般旋轉磁碟的標準儲存體，或是選擇使用 SSD 磁碟的進階儲存體，以取得高 I/O 工作負載和尖端效能。</span><span class="sxs-lookup"><span data-stu-id="ba689-123">You can use Standard storage, that uses regular spinning disks, or Premium storage for high I/O workloads and peak performance, that uses SSD disks.</span></span> <span data-ttu-id="ba689-124">做為以 hello VM 大小會增加成本考量 tooselecting hello 儲存媒體。</span><span class="sxs-lookup"><span data-stu-id="ba689-124">As with hello VM size, there are cost considerations tooselecting hello storage medium.</span></span> <span data-ttu-id="ba689-125">您可以閱讀 hello[儲存體基礎結構指導方針文件](infrastructure-storage-solutions-guidelines.md)toounderstand toodesign 適當 Vm 的最佳效能的存放裝置的方式。</span><span class="sxs-lookup"><span data-stu-id="ba689-125">You can read hello [storage infrastructure guidelines article](infrastructure-storage-solutions-guidelines.md) toounderstand how toodesign appropriate storage for optimum performance of your VMs.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="ba689-126">資源群組</span><span class="sxs-lookup"><span data-stu-id="ba689-126">Resource groups</span></span>
<span data-ttu-id="ba689-127">VM 之類的元件會以邏輯方式分組，以方便使用 [Azure 資源群組](../../azure-resource-manager/resource-group-overview.md)進行管理和維護。</span><span class="sxs-lookup"><span data-stu-id="ba689-127">Components such as VMs are logically grouped for ease of management and maintenance using [Azure Resource Groups](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ba689-128">藉由使用資源群組，您可以建立、 管理及監視所有的 hello 資源指定的應用程式所組成。</span><span class="sxs-lookup"><span data-stu-id="ba689-128">By using resource groups, you can create, manage, and monitor all hello resources that make up a given application.</span></span> <span data-ttu-id="ba689-129">您也可以實作[角色型存取控制](../../active-directory/role-based-access-control-what-is.md)toogrant 存取 tooothers 它們需要您小組 tooonly hello 資源內。</span><span class="sxs-lookup"><span data-stu-id="ba689-129">You can also implement [role-based access controls](../../active-directory/role-based-access-control-what-is.md) toogrant access tooothers within your team tooonly hello resources they require.</span></span> <span data-ttu-id="ba689-130">花費時間 tooplan 出您的資源群組和角色指派。</span><span class="sxs-lookup"><span data-stu-id="ba689-130">Take time tooplan out your resource groups and role assignments.</span></span> <span data-ttu-id="ba689-131">有不同的方法 tooactually 設計和實作的資源群組，所以請確定 tooread hello[資源群組的指導方針文件](infrastructure-resource-groups-guidelines.md)toounderstand 最佳 toobuild 出您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ba689-131">There are different approaches tooactually design and implement resource groups, so be sure tooread hello [resource groups guidelines article](infrastructure-resource-groups-guidelines.md) toounderstand how best toobuild out your VMs.</span></span>

## <a name="templates"></a><span data-ttu-id="ba689-132">範本</span><span class="sxs-lookup"><span data-stu-id="ba689-132">Templates</span></span>
<span data-ttu-id="ba689-133">您可以建立宣告式的 JSON 檔案，toocreate 所定義的範本，您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ba689-133">You can build templates, defined by declarative JSON files, toocreate your VMs.</span></span> <span data-ttu-id="ba689-134">範本通常也建置 hello 所需的儲存體、 網路功能、 網路介面、 IP 位址等以及 hello Vm 本身。</span><span class="sxs-lookup"><span data-stu-id="ba689-134">Templates typically also build hello required storage, networking, network interfaces, IP addressing, etc. along with hello VMs themselves.</span></span> <span data-ttu-id="ba689-135">您所使用的開發和測試用途 tooeasily 複寫實際執行環境範本 toocreate 一致、 可重現環境，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="ba689-135">You use templates toocreate consistent, reproducible environments for development and testing purposes tooeasily replicate production environments and vice versa.</span></span> <span data-ttu-id="ba689-136">您可以深入了解[建立和使用範本](../../azure-resource-manager/resource-group-overview.md#template-deployment)toounderstand 如何使用它們來建立和部署您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ba689-136">You can read more about [building and using templates](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand how you can use them for creating and deploying your VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba689-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba689-137">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

