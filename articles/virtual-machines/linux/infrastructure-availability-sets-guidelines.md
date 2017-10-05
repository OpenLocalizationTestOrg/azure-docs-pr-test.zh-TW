---
title: "Azure 中 Linux VM 的可用性設定組 | Microsoft Docs"
description: "了解適合用來在 Azure 基礎結構服務中部署可用性設定組的關鍵設計和實作指導方針。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5fad478a8fbbdeef2fe72f0b8f2ebe32852bbc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a><span data-ttu-id="d43b6-103">適用於 Linux VM 的 Azure 可用性設定組指導方針</span><span class="sxs-lookup"><span data-stu-id="d43b6-103">Azure availability sets guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="d43b6-104">本文著重於了解可用性設定組的必要計畫步驟，以確保應用程式在計畫或非計畫的事件發生期間可以維持存取性。</span><span class="sxs-lookup"><span data-stu-id="d43b6-104">This article focuses on understanding the required planning steps for availability sets to ensure your applications remains accessible during planned or unplanned events.</span></span>

## <a name="implementation-guidelines-for-availability-sets"></a><span data-ttu-id="d43b6-105">可用性設定組的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="d43b6-105">Implementation guidelines for availability sets</span></span>
<span data-ttu-id="d43b6-106">决策：</span><span class="sxs-lookup"><span data-stu-id="d43b6-106">Decisions:</span></span>

* <span data-ttu-id="d43b6-107">在您的應用程式基礎結構中，需要針對各種角色和層級使用多少個可用性設定組？</span><span class="sxs-lookup"><span data-stu-id="d43b6-107">How many availability sets do you need for the various roles and tiers in your application infrastructure?</span></span>

<span data-ttu-id="d43b6-108">工作：</span><span class="sxs-lookup"><span data-stu-id="d43b6-108">Tasks:</span></span>

* <span data-ttu-id="d43b6-109">定義每個所需應用程式層級中的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="d43b6-109">Define the number of VMs in each application tier you require.</span></span>
* <span data-ttu-id="d43b6-110">決定您是否需要調整應用程式所使用的錯誤數目或更新網域。</span><span class="sxs-lookup"><span data-stu-id="d43b6-110">Determine if you need to adjust the number of fault or update domains to be used for your application.</span></span>
* <span data-ttu-id="d43b6-111">使用您的命名慣例，來定義必要的可用性設定組以及要置於其中的 VM。</span><span class="sxs-lookup"><span data-stu-id="d43b6-111">Define the required availability sets using your naming convention and what VMs reside in them.</span></span> <span data-ttu-id="d43b6-112">一個可用性設定組中只能放置一個 VM。</span><span class="sxs-lookup"><span data-stu-id="d43b6-112">A VM can only reside in one availability set.</span></span> 

## <a name="availability-sets"></a><span data-ttu-id="d43b6-113">可用性集合</span><span class="sxs-lookup"><span data-stu-id="d43b6-113">Availability sets</span></span>
<span data-ttu-id="d43b6-114">在 Azure 中，虛擬機器 (VM) 可以被放置在稱為可用性設定組的邏輯群組之中。</span><span class="sxs-lookup"><span data-stu-id="d43b6-114">In Azure, virtual machines (VMs) can be placed in to a logical grouping called an availability set.</span></span> <span data-ttu-id="d43b6-115">當您在可用性設定組中建立 VM 時，Azure 平台會將這些 VM 的位置散佈於基礎結構上。</span><span class="sxs-lookup"><span data-stu-id="d43b6-115">When you create VMs within an availability set, the Azure platform distributes the placement of those VMs across the underlying infrastructure.</span></span> <span data-ttu-id="d43b6-116">若 Azure 平台發生預計的維護事件，或是發生基礎硬體 / 基礎結構錯誤，使用可用性設定組將可確保至少有一個 VM 會保持執行。</span><span class="sxs-lookup"><span data-stu-id="d43b6-116">Should there be a planned maintenance event to the Azure platform or an underlying hardware / infrastructure fault, the use of availability sets ensures that at least one VM remains running.</span></span>

<span data-ttu-id="d43b6-117">最佳作法是不將應用程式放置在單一 VM 上。</span><span class="sxs-lookup"><span data-stu-id="d43b6-117">As a best practice, applications should not reside on a single VM.</span></span> <span data-ttu-id="d43b6-118">包含單一 VM 的可用性設定組將無法在 Azure 平台內針對計畫或非計畫的事件獲得保護。</span><span class="sxs-lookup"><span data-stu-id="d43b6-118">An availability set that contains a single VM doesn't gain any protection from planned or unplanned events within the Azure platform.</span></span> <span data-ttu-id="d43b6-119">[Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines) 需要可用性設定組內有兩個或以上的 VM，以允許將 VM 散佈於基礎結構上。</span><span class="sxs-lookup"><span data-stu-id="d43b6-119">The [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines) requires two or more VMs within an availability set to allow the distribution of VMs across the underlying infrastructure.</span></span> <span data-ttu-id="d43b6-120">如果您使用的是 [Azure 進階儲存體](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，Azure SLA 就會套用到單一 VM。</span><span class="sxs-lookup"><span data-stu-id="d43b6-120">If you are using [Azure Premium Storage](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the Azure SLA applies to a single VM.</span></span>

<span data-ttu-id="d43b6-121">Azure 中的基礎結構分為多個硬體叢集。</span><span class="sxs-lookup"><span data-stu-id="d43b6-121">The underlying infrastructure in Azure is divided in to multiple hardware clusters.</span></span> <span data-ttu-id="d43b6-122">每個硬體叢集皆可支援某個 VM 大小範圍。</span><span class="sxs-lookup"><span data-stu-id="d43b6-122">Each hardware cluster can support a range of VM sizes.</span></span> <span data-ttu-id="d43b6-123">不論何時，可用性設定組都只能裝載在單一硬體叢集上。</span><span class="sxs-lookup"><span data-stu-id="d43b6-123">An availability set can only be hosted on a single hardware cluster at any point in time.</span></span> <span data-ttu-id="d43b6-124">因此，能夠存在於單一可用性設定組中的 VM 大小範圍會限制在硬體叢集所支援的 VM 大小範圍。</span><span class="sxs-lookup"><span data-stu-id="d43b6-124">Therefore, the range of VM sizes that can exist in a single availability set is limited to the range of VM sizes supported by the hardware cluster.</span></span> <span data-ttu-id="d43b6-125">當部署可用性設定組中的第一個 VM，或啟動所有 VM 目前都處於「已停止-已解除配置」狀態之可用性設定組中的第一個 VM 時，就會選取該可用性設定組的硬體叢集。</span><span class="sxs-lookup"><span data-stu-id="d43b6-125">The hardware cluster for the availability set is selected when the first VM in the availability set is deployed or when starting the first VM in an availability set where all VMs are currently in the stopped-deallocated state.</span></span> <span data-ttu-id="d43b6-126">下列 CLI 命令可用來判斷可用性設定組可用的 VM 大小範圍：“az vm list-sizes --location \<string\>”</span><span class="sxs-lookup"><span data-stu-id="d43b6-126">The following CLI command can be used to determine the range of VM sizes available for an availability set: “az vm list-sizes --location \<string\>”</span></span>

<span data-ttu-id="d43b6-127">每個硬體叢集都分為多個更新網域和容錯網域。</span><span class="sxs-lookup"><span data-stu-id="d43b6-127">Each hardware cluster is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="d43b6-128">這些網域是會根據主機是共用一般更新週期，或共用類似的實體基礎結構 (例如電源和網路功能) 來定義。</span><span class="sxs-lookup"><span data-stu-id="d43b6-128">These domains are defined by what hosts share a common update cycle, or share similar physical infrastructure such as power and networking.</span></span> <span data-ttu-id="d43b6-129">Azure 會自動將您位於可用性設定組內的 VM 散佈於網域上，以維護可用性和容錯。</span><span class="sxs-lookup"><span data-stu-id="d43b6-129">Azure automatically distributes your VMs within an availability set across domains to maintain availability and fault tolerance.</span></span> <span data-ttu-id="d43b6-130">根據應用程式的大小，以及可用性設定組內的 VM 數目，您可以調整想要使用的網域數目。</span><span class="sxs-lookup"><span data-stu-id="d43b6-130">Depending on the size of your application and the number of VMs within an availability set, you can adjust the number of domains you wish to use.</span></span> <span data-ttu-id="d43b6-131">您可以深入了解[管理更新和容錯網域的可用性及使用](manage-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="d43b6-131">You can read more about [managing availability and use of update and fault domains](manage-availability.md).</span></span>

<span data-ttu-id="d43b6-132">設計應用程式基礎結構時，計畫要使用的應用程式層級。</span><span class="sxs-lookup"><span data-stu-id="d43b6-132">When designing your application infrastructure, plan out the application tiers to use.</span></span> <span data-ttu-id="d43b6-133">將用途相同的 VM 分組為可用性設定組，例如由執行 nginx 或 Apache 的前端 VM 所組成的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d43b6-133">Group VMs that serve the same purpose in to availability sets, such as an availability set for your front-end VMs running nginx or Apache.</span></span> <span data-ttu-id="d43b6-134">為執行 MongoDB 或 MySQL 的後端 VM 建立個別的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d43b6-134">Create a separate availability set for your back-end VMs running MongoDB or MySQL.</span></span> <span data-ttu-id="d43b6-135">我們的目標是要確保應用程式的每個元件都會受到某個可用性設定組所保護，且至少有一個執行個體總是保持執行。</span><span class="sxs-lookup"><span data-stu-id="d43b6-135">The goal is to ensure that each component of your application is protected by an availability set and at least once instance always remains running.</span></span>

<span data-ttu-id="d43b6-136">負載平衡器可以在每個應用程式層級之前運用，以和可用性設定組一起運作，並確保流量總是會被路由到正在執行中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d43b6-136">Load balancers can be utilized in front of each application tier to work alongside an availability set and ensure traffic can always be routed to a running instance.</span></span> <span data-ttu-id="d43b6-137">若沒有負載平衡器，您的 VM 可能會在規劃或未規劃的維護事件期間持續執行，但在主要 VM 無法使用的情況下，您的使用者可能無法解析它們。</span><span class="sxs-lookup"><span data-stu-id="d43b6-137">Without a load balancer, your VMs may continue running throughout planned and unplanned maintenance events, but your end user may not be able to resolve them if the primary VM is unavailable.</span></span>

<span data-ttu-id="d43b6-138">針對儲存層的高可用性設計應用程式。</span><span class="sxs-lookup"><span data-stu-id="d43b6-138">Design your application for high availability at storage layer.</span></span> <span data-ttu-id="d43b6-139">最佳作法是[對於可用性設定組中的 VM 使用受控磁碟](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)。</span><span class="sxs-lookup"><span data-stu-id="d43b6-139">The best practice is to [use Managed Disks for VMs in an Availability Set](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).</span></span> <span data-ttu-id="d43b6-140">如果您目前使用非受控磁碟，強烈建議您[將可用性設定組中的 VM 轉換為受控磁碟](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set)。</span><span class="sxs-lookup"><span data-stu-id="d43b6-140">If you are currently using unmanaged disks, we highly recommend you to [convert VMs in Availability Set to use Managed Disks](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43b6-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d43b6-141">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

