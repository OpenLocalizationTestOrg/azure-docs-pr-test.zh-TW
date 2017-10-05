---
title: "Azure VM 的災害復原案例 | Microsoft Docs"
description: "了解發生影響 Azure 虛擬機器的 Azure 服務中斷事件時該怎麼辦。"
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fb986a41e33501ee71c93a48457ac4114e33c671
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-to-do-in-the-event-that-an-azure-service-disruption-impacts-azure-vms"></a><span data-ttu-id="dc33d-103">發生影響 Azure VM 的 Azure 服務中斷事件時該怎麼辦</span><span class="sxs-lookup"><span data-stu-id="dc33d-103">What to do in the event that an Azure service disruption impacts Azure VMs</span></span>
<span data-ttu-id="dc33d-104">Microsoft 的同仁一向努力確保提供您需要的服務。</span><span class="sxs-lookup"><span data-stu-id="dc33d-104">At Microsoft, we work hard to make sure that our services are always available to you when you need them.</span></span> <span data-ttu-id="dc33d-105">有時候因為不可抗力之影響，造成服務意外中斷。</span><span class="sxs-lookup"><span data-stu-id="dc33d-105">Forces beyond our control sometimes impact us in ways that cause unplanned service disruptions.</span></span>

<span data-ttu-id="dc33d-106">Microsoft 為其服務提供服務等級協定 (SLA)，作為執行時間和連接承諾。</span><span class="sxs-lookup"><span data-stu-id="dc33d-106">Microsoft provides a Service Level Agreement (SLA) for its services as a commitment for uptime and connectivity.</span></span> <span data-ttu-id="dc33d-107">個別的 Azure 服務 SLA 位於 [Azure 服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="dc33d-107">The SLA for individual Azure services can be found at [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="dc33d-108">Azure 已經有許多支援高可用性應用程式的內建平台功能。</span><span class="sxs-lookup"><span data-stu-id="dc33d-108">Azure already has many built-in platform features that support highly available applications.</span></span> <span data-ttu-id="dc33d-109">如需這些服務的詳細資訊，請參閱 [Azure 應用程式的災害復原與高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="dc33d-109">For more about these services, read [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

<span data-ttu-id="dc33d-110">本文內含當整個地區因重大天災或大規模服務中斷而發生中斷的真實災害復原案例。</span><span class="sxs-lookup"><span data-stu-id="dc33d-110">This article covers a true disaster recovery scenario, when a whole region experiences an outage due to major natural disaster or widespread service interruption.</span></span> <span data-ttu-id="dc33d-111">這些都是極其罕見的情況，但您還是必須對整個區域發生中斷的可能性有所準備。</span><span class="sxs-lookup"><span data-stu-id="dc33d-111">These are rare occurrences, but you must prepare for the possibility that there is an outage of an entire region.</span></span> <span data-ttu-id="dc33d-112">如果整個區域的服務中斷，會暫時無法使用本機的備援資料複本。</span><span class="sxs-lookup"><span data-stu-id="dc33d-112">If an entire region experiences a service disruption, the locally redundant copies of your data would temporarily be unavailable.</span></span> <span data-ttu-id="dc33d-113">如果已啟用異地複寫，會在不同的區域儲存額外三份 Azure 儲存體 Blob 和資料表。</span><span class="sxs-lookup"><span data-stu-id="dc33d-113">If you have enabled geo-replication, three additional copies of your Azure Storage blobs and tables are stored in a different region.</span></span> <span data-ttu-id="dc33d-114">如果發生全面性區域中斷或嚴重損壞，且主要區域無法復原時，Azure 會重新對應異地複寫區域的所有 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="dc33d-114">In the event of a complete regional outage or a disaster in which the primary region is not recoverable, Azure remaps all of the DNS entries to the geo-replicated region.</span></span>

<span data-ttu-id="dc33d-115">為協助您處理這些罕見事件，我們提供以下 Azure 虛擬機器指引，以因應 Azure 虛擬機器應用程式部署所在的整個區域發生服務中斷的情況。</span><span class="sxs-lookup"><span data-stu-id="dc33d-115">To help you handle these rare occurrences, we provide the following guidance for Azure virtual machines in the case of a service disruption of the entire region where your Azure virtual machine application is deployed.</span></span>

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a><span data-ttu-id="dc33d-116">選項 1︰使用 Azure Site Recovery 起始容錯移轉</span><span class="sxs-lookup"><span data-stu-id="dc33d-116">Option 1: Initiate a failover by using Azure Site Recovery</span></span>
<span data-ttu-id="dc33d-117">您可以為 VM 設定 Azure Site Recovery，如此一來，只要按一下花幾分鐘就能復原應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc33d-117">You can configure Azure Site Recovery for your VMs so that you can recover your application with a single click in matter of minutes.</span></span> <span data-ttu-id="dc33d-118">您可以複寫至所選擇的 Azure 區域，而不限於配對的區域。</span><span class="sxs-lookup"><span data-stu-id="dc33d-118">You can replicate to Azure region of your choice and not restricted to paired regions.</span></span> <span data-ttu-id="dc33d-119">您可以[複寫虛擬機器](https://aka.ms/a2a-getting-started)來開始進行。</span><span class="sxs-lookup"><span data-stu-id="dc33d-119">You can get started by [replicating your virtual machines](https://aka.ms/a2a-getting-started).</span></span> <span data-ttu-id="dc33d-120">您可以[建立復原方案](../site-recovery/site-recovery-create-recovery-plans.md)，來將應用程式的整個容錯移轉程序自動化。</span><span class="sxs-lookup"><span data-stu-id="dc33d-120">You can [create a recovery plan](../site-recovery/site-recovery-create-recovery-plans.md) so that you can automate the entire failover process for your application.</span></span> <span data-ttu-id="dc33d-121">您可以事先[測試容錯移轉](../site-recovery/site-recovery-test-failover-to-azure.md)，而不影響實際執行應用程式或進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="dc33d-121">You can [test your failovers](../site-recovery/site-recovery-test-failover-to-azure.md) beforehand without impacting production application or the ongoing replication.</span></span> <span data-ttu-id="dc33d-122">如果主要區域發生中斷，只要[起始容錯移轉](../site-recovery/site-recovery-failover.md)並將您的應用程式帶到目標區域即可。</span><span class="sxs-lookup"><span data-stu-id="dc33d-122">In the event of a primary region disruption, you just [initiate a failover](../site-recovery/site-recovery-failover.md) and bring your application in target region.</span></span>


## <a name="option-2-wait-for-recovery"></a><span data-ttu-id="dc33d-123">選項 2︰等待復原</span><span class="sxs-lookup"><span data-stu-id="dc33d-123">Option 2: Wait for recovery</span></span>
<span data-ttu-id="dc33d-124">在此情況下，您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="dc33d-124">In this case, no action on your part is required.</span></span> <span data-ttu-id="dc33d-125">但您要知道，我們正在努力還原服務的可用性。</span><span class="sxs-lookup"><span data-stu-id="dc33d-125">Know that we are working diligently to restore service availability.</span></span> <span data-ttu-id="dc33d-126">您可以在 [Azure 服務健康狀態儀表板](https://azure.microsoft.com/status/)上看見目前的服務狀態。</span><span class="sxs-lookup"><span data-stu-id="dc33d-126">You can see the current service status on our [Azure Service Health Dashboard](https://azure.microsoft.com/status/).</span></span>

<span data-ttu-id="dc33d-127">如果發生中斷前尚未設定 Azure Site Recovery、讀取權限異地備援儲存體或異地備援儲存體，這便是您的最佳選項。</span><span class="sxs-lookup"><span data-stu-id="dc33d-127">This is the best option if you have not set up Azure Site Recovery, read-access geo-redundant storage, or geo-redundant storage prior to the disruption.</span></span> <span data-ttu-id="dc33d-128">如果儲存 VM 虛擬硬碟 (VHD) 的儲存體帳戶已設定異地備援儲存體或讀取權限異地備援儲存體，您可以指望復原基本映像 VHD，並嘗試用它佈建新的 VM。</span><span class="sxs-lookup"><span data-stu-id="dc33d-128">If you have set up geo-redundant storage or read-access geo-redundant storage for the storage account where your VM virtual hard drives (VHDs) are stored, you can look to recover the base image VHD and try to provision a new VM from it.</span></span> <span data-ttu-id="dc33d-129">因為不保證能夠同步處理資料，所以這不是慣用的選項。</span><span class="sxs-lookup"><span data-stu-id="dc33d-129">This is not a preferred option because there are no guarantees of synchronization of data.</span></span> <span data-ttu-id="dc33d-130">因此，不保證此選項可以運作。</span><span class="sxs-lookup"><span data-stu-id="dc33d-130">Consequently, this option is not guaranteed to work.</span></span>


> [!NOTE]
> <span data-ttu-id="dc33d-131">請注意，您完全無法控制這個程序，而且它只有在全區域服務中斷時才會發生。</span><span class="sxs-lookup"><span data-stu-id="dc33d-131">Be aware that you do not have any control over this process, and it will only occur for region-wide service disruptions.</span></span> <span data-ttu-id="dc33d-132">因此，您也必須依賴其他的應用程式特定備份策略，以達到最高層級的可用性。</span><span class="sxs-lookup"><span data-stu-id="dc33d-132">Because of this, you must also rely on other application-specific backup strategies to achieve the highest level of availability.</span></span> <span data-ttu-id="dc33d-133">如需詳細資訊，請參閱 [災害復原的資料策略](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery)一節。</span><span class="sxs-lookup"><span data-stu-id="dc33d-133">For more information, see the section on [Data strategies for disaster recovery](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="dc33d-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc33d-134">Next steps</span></span>

- <span data-ttu-id="dc33d-135">使用 Azure Site Recovery 開始[保護在 Azure 虛擬機器上執行的應用程式](https://aka.ms/a2a-getting-started)</span><span class="sxs-lookup"><span data-stu-id="dc33d-135">Start [protecting your applications running on Azure virtual machines](https://aka.ms/a2a-getting-started) using Azure Site Recovery</span></span>

- <span data-ttu-id="dc33d-136">若要深入了解如何實作災害復原和高可用性策略，請參閱 [Azure 應用程式的災害復原和高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="dc33d-136">To learn more about how to implement a disaster recovery and high availability strategy, see [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

- <span data-ttu-id="dc33d-137">若要開發雲端平台功能的詳細技術知識，請參閱 [Azure 復原技術指導](../resiliency/resiliency-technical-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="dc33d-137">To develop a detailed technical understanding of a cloud platform’s capabilities, see [Azure resiliency technical guidance](../resiliency/resiliency-technical-guidance.md).</span></span>


- <span data-ttu-id="dc33d-138">如果指示不清楚，或如果您希望 Microsoft 代您執行作業，請連絡 [客戶支援](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="dc33d-138">If the instructions are not clear, or if you would like Microsoft to do the operations on your behalf, contact [Customer Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
