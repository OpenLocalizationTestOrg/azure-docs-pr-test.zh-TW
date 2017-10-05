---
title: "發生影響 Azure 雲端服務的 Azure 服務中斷事件時該怎麼辦 | Microsoft Docs"
description: "了解發生影響 Azure 雲端服務的 Azure 服務中斷事件時該怎麼辦。"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: db6a980b85ea5ef8cbbba4ba5a36f9d033739df1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="what-to-do-in-the-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a><span data-ttu-id="b8352-103">發生影響 Azure 雲端服務的 Azure 服務中斷事件時該怎麼辦</span><span class="sxs-lookup"><span data-stu-id="b8352-103">What to do in the event of an Azure service disruption that impacts Azure Cloud Services</span></span>
<span data-ttu-id="b8352-104">Microsoft 的同仁一向努力確保提供您需要的服務。</span><span class="sxs-lookup"><span data-stu-id="b8352-104">At Microsoft, we work hard to make sure that our services are always available to you when you need them.</span></span> <span data-ttu-id="b8352-105">有時候因為不可抗力之影響，造成服務意外中斷。</span><span class="sxs-lookup"><span data-stu-id="b8352-105">Forces beyond our control sometimes impact us in ways that cause unplanned service disruptions.</span></span>

<span data-ttu-id="b8352-106">Microsoft 為其服務提供服務等級協定 (SLA)，作為執行時間和連接承諾。</span><span class="sxs-lookup"><span data-stu-id="b8352-106">Microsoft provides a Service Level Agreement (SLA) for its services as a commitment for uptime and connectivity.</span></span> <span data-ttu-id="b8352-107">個別的 Azure 服務 SLA 位於 [Azure 服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="b8352-107">The SLA for individual Azure services can be found at [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="b8352-108">Azure 已經有許多支援高可用性應用程式的內建平台功能。</span><span class="sxs-lookup"><span data-stu-id="b8352-108">Azure already has many built-in platform features that support highly available applications.</span></span> <span data-ttu-id="b8352-109">如需這些服務的詳細資訊，請參閱 [Azure 應用程式的災害復原與高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="b8352-109">For more about these services, read [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

<span data-ttu-id="b8352-110">本文內含當整個地區因重大天災或大規模服務中斷而發生中斷的真實災害復原案例。</span><span class="sxs-lookup"><span data-stu-id="b8352-110">This article covers a true disaster recovery scenario, when a whole region experiences an outage due to major natural disaster or widespread service interruption.</span></span> <span data-ttu-id="b8352-111">這些都是極其罕見的情況，但您還是必須對整個區域發生中斷的可能性有所準備。</span><span class="sxs-lookup"><span data-stu-id="b8352-111">These are rare occurrences, but you must prepare for the possibility that there is an outage of an entire region.</span></span> <span data-ttu-id="b8352-112">如果整個區域的服務中斷，會暫時無法使用本機的備援資料複本。</span><span class="sxs-lookup"><span data-stu-id="b8352-112">If an entire region experiences a service disruption, the locally redundant copies of your data would temporarily be unavailable.</span></span> <span data-ttu-id="b8352-113">如果已啟用異地複寫，會在不同的區域儲存額外三份 Azure 儲存體 Blob 和資料表。</span><span class="sxs-lookup"><span data-stu-id="b8352-113">If you have enabled geo-replication, three additional copies of your Azure Storage blobs and tables are stored in a different region.</span></span> <span data-ttu-id="b8352-114">如果發生全面性區域中斷或嚴重損壞，且主要區域無法復原時，Azure 會重新對應異地複寫區域的所有 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="b8352-114">In the event of a complete regional outage or a disaster in which the primary region is not recoverable, Azure remaps all of the DNS entries to the geo-replicated region.</span></span>

> [!NOTE]
> <span data-ttu-id="b8352-115">請注意，您完全無法控制這個程序，而且它只有在整個資料中心服務中斷時才會發生。</span><span class="sxs-lookup"><span data-stu-id="b8352-115">Be aware that you do not have any control over this process, and it will only occur for datacenter-wide service disruptions.</span></span> <span data-ttu-id="b8352-116">因此，您也必須依賴其他的應用程式特定備份策略，以達到最高層級的可用性。</span><span class="sxs-lookup"><span data-stu-id="b8352-116">Because of this, you must also rely on other application-specific backup strategies to achieve the highest level of availability.</span></span> <span data-ttu-id="b8352-117">如需詳細資訊，請參閱[建置在 Microsoft Azure 上之應用程式的災害復原和高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="b8352-117">For more information, see [Disaster recovery and high availability for applications built on Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span> <span data-ttu-id="b8352-118">如果您希望能夠影響您自己的容錯移轉，就可能想要考慮使用 [讀取存取異地備援儲存體 (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)，在其他區域中建立資料的唯讀複本。</span><span class="sxs-lookup"><span data-stu-id="b8352-118">If you would like to be able to affect your own failover, you might want to consider the use of [read-access geo-redundant storage (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), which creates a read-only copy of your data in another region.</span></span>
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a><span data-ttu-id="b8352-119">選項 1︰透過 Azure 流量管理員使用備份部署</span><span class="sxs-lookup"><span data-stu-id="b8352-119">Option 1: Use a backup deployment through Azure Traffic Manager</span></span>
<span data-ttu-id="b8352-120">最強固的災害復原解決方案涉及維護您的應用程式在不同區域中的多個部署，然後使用 [Azure 流量管理員](../traffic-manager/traffic-manager-overview.md)導向其間的流量。</span><span class="sxs-lookup"><span data-stu-id="b8352-120">The most robust disaster recovery solution involves maintaining multiple deployments of your application in different regions, then using [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) to direct traffic between them.</span></span> <span data-ttu-id="b8352-121">Azure 流量管理員會提供多種[路由方式](../traffic-manager/traffic-manager-routing-methods.md)，因此您可以選擇使用主要/備份模型來管理您的部署，或分割其間的流量。</span><span class="sxs-lookup"><span data-stu-id="b8352-121">Azure Traffic Manager provides multiple [routing methods](../traffic-manager/traffic-manager-routing-methods.md), so you can choose whether to manage your deployments using a primary/backup model or to split traffic between them.</span></span>

![使用 Azure 流量管理員平衡區域間的 Azure 雲端服務](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

<span data-ttu-id="b8352-123">若要對遺失區域做出最快的回應，請務必設定流量管理員的[端點監視](../traffic-manager/traffic-manager-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="b8352-123">For the fastest response to the loss of a region, it is important that you configure Traffic Manager's [endpoint monitoring](../traffic-manager/traffic-manager-monitoring.md).</span></span>

## <a name="option-2-deploy-your-application-to-a-new-region"></a><span data-ttu-id="b8352-124">選項 2︰將應用程式部署至新的區域</span><span class="sxs-lookup"><span data-stu-id="b8352-124">Option 2: Deploy your application to a new region</span></span>
<span data-ttu-id="b8352-125">如前一個選項所述維護多個作用中的部署，會造成額外的成本。</span><span class="sxs-lookup"><span data-stu-id="b8352-125">Maintaining multiple active deployments as described in the previous option incurs additional ongoing costs.</span></span> <span data-ttu-id="b8352-126">如果您的復原時間目標 (RTO) 有足夠的彈性，且您具有原始程式碼或已編譯的雲端服務套件，您即可在其他區域中建立應用程式的新執行個體並更新您的 DNS 記錄，以指向新的部署。</span><span class="sxs-lookup"><span data-stu-id="b8352-126">If your recovery time objective (RTO) is flexible enough and you have the original code or compiled Cloud Services package, you can create a new instance of your application in another region and update your DNS records to point to the new deployment.</span></span>

<span data-ttu-id="b8352-127">如需如何建立和部署雲端服務應用程式的詳細資訊，請參閱[如何建立和部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b8352-127">For more detail about how to create and deploy a cloud service application, see [How to create and deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>

<span data-ttu-id="b8352-128">根據您的應用程式資料來源，您可能需要檢查應用程式資料來源的復原程序。</span><span class="sxs-lookup"><span data-stu-id="b8352-128">Depending on your application data sources, you may need to check the recovery procedures for your application data source.</span></span>

* <span data-ttu-id="b8352-129">如需 Azure 儲存體資料來源，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) ，以根據您針對應用程式所選擇的複寫模型來查看可用的選項。</span><span class="sxs-lookup"><span data-stu-id="b8352-129">For Azure Storage data sources, see [Azure Storage replication](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) to check on the options that are available based on the chose replication model for your application.</span></span>
* <span data-ttu-id="b8352-130">如需 SQL 資料庫來源，請閱讀 [概觀：雲端商務持續性和 SQL Database 的資料庫災害復原](../sql-database/sql-database-business-continuity.md) ，以根據您針對應用程式所選擇的複寫模型來查看可用的選項。</span><span class="sxs-lookup"><span data-stu-id="b8352-130">For SQL Database sources, read [Overview: Cloud business continuity and database disaster recovery with SQL Database](../sql-database/sql-database-business-continuity.md) to check on the options that are available based on the chosen replication model for your application.</span></span>


## <a name="option-3-wait-for-recovery"></a><span data-ttu-id="b8352-131">選項 3︰等待復原</span><span class="sxs-lookup"><span data-stu-id="b8352-131">Option 3: Wait for recovery</span></span>
<span data-ttu-id="b8352-132">在此情況下，您不需要採取任何動作，但是直到該區域還原，才可使用您的服務。</span><span class="sxs-lookup"><span data-stu-id="b8352-132">In this case, no action on your part is required, but your service will be unavailable until the region is restored.</span></span> <span data-ttu-id="b8352-133">您可以在 [Azure 服務健康狀態儀表板](https://azure.microsoft.com/status/)上看見目前的服務狀態。</span><span class="sxs-lookup"><span data-stu-id="b8352-133">You can see the current service status on the [Azure Service Health Dashboard](https://azure.microsoft.com/status/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8352-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8352-134">Next steps</span></span>
<span data-ttu-id="b8352-135">若要深入了解如何實作災害復原和高可用性策略，請參閱 [Azure 應用程式的災害復原和高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="b8352-135">To learn more about how to implement a disaster recovery and high availability strategy, see [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

<span data-ttu-id="b8352-136">若要開發雲端平台功能的詳細技術知識，請參閱 [Azure 復原技術指導](../resiliency/resiliency-technical-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="b8352-136">To develop a detailed technical understanding of a cloud platform’s capabilities, see [Azure resiliency technical guidance](../resiliency/resiliency-technical-guidance.md).</span></span>