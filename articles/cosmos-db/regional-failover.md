---
title: "Azure Cosmos DB 的區域性容錯移轉 | Microsoft Docs"
description: "了解 Azure Cosmos DB 的手動和自動容錯移轉如何運作。"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d8ba08bc9f99cb77c9f03949fc5db299eb222c8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a><span data-ttu-id="d887d-103">Azure Cosmos DB 中商務持續性的自動區域性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="d887d-103">Automatic regional failover for business continuity in Azure Cosmos DB</span></span>
<span data-ttu-id="d887d-104">Azure Cosmos DB 會簡化資料的全域散發作業，方法是提供多個可完全管理的[多重地區資料庫帳戶](distribute-data-globally.md)，在一致性、可用性和效能之間進行明確取捨，這一切全都倚靠相對應的保證來完成。</span><span class="sxs-lookup"><span data-stu-id="d887d-104">Azure Cosmos DB simplifies the global distribution of data by offering fully managed, [multi-region database accounts](distribute-data-globally.md) that provide clear tradeoffs between consistency, availability, and performance, all with corresponding guarantees.</span></span> <span data-ttu-id="d887d-105">Cosmos DB 帳戶具備下列優點：高可用性、個位數的毫秒延遲、[定義完善的一致性層級](consistency-levels.md)、利用多路連接 API 透明進行的區域性容錯移轉，以及全球輸送量及儲存體的靈活調整能力。</span><span class="sxs-lookup"><span data-stu-id="d887d-105">Cosmos DB accounts offer high availability, single digit ms latencies, [well-defined consistency levels](consistency-levels.md), transparent regional failover with multi-homing APIs, and the ability to elastically scale throughput and storage across the globe.</span></span> 

<span data-ttu-id="d887d-106">Cosmos DB 支援明確和原則導向的容錯移轉，可讓您控制在失敗發生時的端對端系統行為。</span><span class="sxs-lookup"><span data-stu-id="d887d-106">Cosmos DB supports both explicit and policy driven failovers that allow you to control the end-to-end system behavior in the event of failures.</span></span> <span data-ttu-id="d887d-107">我們將在本文中說明：</span><span class="sxs-lookup"><span data-stu-id="d887d-107">In this article, we look at:</span></span>

* <span data-ttu-id="d887d-108">Cosmos DB 的手動容錯移轉如何運作？</span><span class="sxs-lookup"><span data-stu-id="d887d-108">How do manual failovers work in Cosmos DB?</span></span>
* <span data-ttu-id="d887d-109">自動容錯移轉在 Cosmos DB 中如何運作，以及當資料中心當機時會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="d887d-109">How do automatic failovers work in Cosmos DB and what happens when a data center goes down?</span></span>
* <span data-ttu-id="d887d-110">如何在應用程式架構中使用手動容錯移轉？</span><span class="sxs-lookup"><span data-stu-id="d887d-110">How can you use manual failovers in application architectures?</span></span>

<span data-ttu-id="d887d-111">您也可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解區域容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d887d-111">You can also learn about regional failovers in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <span data-ttu-id="d887d-112"><a id="ConfigureMultiRegionApplications"></a>設定多區域應用程式</span><span class="sxs-lookup"><span data-stu-id="d887d-112"><a id="ConfigureMultiRegionApplications"></a>Configuring multi-region applications</span></span>
<span data-ttu-id="d887d-113">在深入探討容錯移轉模式之前，我們會探討如何設定應用程式以發揮多區域可用性，並在區域性容錯移轉中兼具彈性。</span><span class="sxs-lookup"><span data-stu-id="d887d-113">Before we dive into failover modes, we look at how you can configure an application to take advantage of multi-region availability and be resilient in the face of regional failovers.</span></span>

* <span data-ttu-id="d887d-114">首先，在多個區域中部署您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d887d-114">First, deploy your application in multiple regions</span></span>
* <span data-ttu-id="d887d-115">為了確保從您部署應用程式的每個區域能夠低延遲存取，使用支援的 SDK之一來設定每個區域的對應[慣用區域清單](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations)。</span><span class="sxs-lookup"><span data-stu-id="d887d-115">To ensure low latency access from every region your application is deployed, configure the corresponding [preferred regions list](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) for each region via one of the supported SDKs.</span></span>

<span data-ttu-id="d887d-116">下列程式碼片段示範如何初始化多區域的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d887d-116">The following snippet shows how to initialize a multi-region application.</span></span> <span data-ttu-id="d887d-117">在這裡，我們替 Cosmos DB 帳戶 `contoso.documents.azure.com` 設定兩個地區：美國西部和北歐。</span><span class="sxs-lookup"><span data-stu-id="d887d-117">Here, the Azure Cosmos DB account `contoso.documents.azure.com` is configured with two regions - West US and North Europe.</span></span> 

* <span data-ttu-id="d887d-118">應用程式是部署在美國西部區域 (舉例來說，使用 Azure App Service)</span><span class="sxs-lookup"><span data-stu-id="d887d-118">The application is deployed in the West US region (using Azure App Services for example)</span></span> 
* <span data-ttu-id="d887d-119">以 `West US` 設定為低延遲讀取的第一個慣用區域</span><span class="sxs-lookup"><span data-stu-id="d887d-119">Configured with `West US` as the first preferred region for low latency reads</span></span>
* <span data-ttu-id="d887d-120">以 `North Europe` 設定第二個慣用區域 (為了在區域失敗時有高可用性)</span><span class="sxs-lookup"><span data-stu-id="d887d-120">Configured with `North Europe` as the second preferred region (for high availability during regional failures)</span></span>

<span data-ttu-id="d887d-121">在 DocumentDB API 中，此設定看起來像下列程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="d887d-121">In the DocumentDB API, this configuration looks like the following snippet:</span></span>

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

應用程式也會部署在北歐區域，但是慣用區域順序相反。 也就是說，北歐是指定的第一個低延遲讀取區域。 <span data-ttu-id="d887d-124">然後，美國西部則指定為第二個慣用區域，以便在區域失敗時能有高可用性。</span><span class="sxs-lookup"><span data-stu-id="d887d-124">Then, the West US region is specified as the second preferred region for high availability during regional failures.</span></span>

<span data-ttu-id="d887d-125">以下架構圖中顯示多區域應用程式的部署，其中的 Cosmos DB 和應用程式設定為可在四個 Azure 地理區域使用。</span><span class="sxs-lookup"><span data-stu-id="d887d-125">The following architecture diagram shows a multi-region application deployment where Cosmos DB and the application are configured to be available in four Azure geographic regions.</span></span>  

![使用 Cosmos DB 部署全域分散式應用程式](./media/regional-failover/app-deployment.png)

<span data-ttu-id="d887d-127">現在，我們來看一下 Cosmos DB 服務如何透過自動容錯移轉處理區域性失敗。</span><span class="sxs-lookup"><span data-stu-id="d887d-127">Now, let's look at how the Cosmos DB service handles regional failures via automatic failovers.</span></span> 

## <span data-ttu-id="d887d-128"><a id="AutomaticFailovers"></a>自動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="d887d-128"><a id="AutomaticFailovers"></a>Automatic Failovers</span></span>
<span data-ttu-id="d887d-129">當發生 Azure 區域性中斷或資料中心中斷這類罕見事件時，Cosmos DB 會自動觸發存在於受影響區域中所有 Cosmos DB 帳戶的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d887d-129">In the rare event of an Azure regional outage or data center outage, Cosmos DB automatically triggers failovers of all Cosmos DB accounts with a presence in the affected region.</span></span> 

<span data-ttu-id="d887d-130">**如果讀取區域中斷會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="d887d-130">**What happens if a read region has an outage?**</span></span>

<span data-ttu-id="d887d-131">Cosmos DB 帳戶的讀取區域若在其中一個受影響區域中，會自動與其寫入區域中斷連線，並標示為離線。</span><span class="sxs-lookup"><span data-stu-id="d887d-131">Cosmos DB accounts with a read region in one of the affected regions are automatically disconnected from their write region and marked offline.</span></span> <span data-ttu-id="d887d-132">Cosmos DB SDK 實作區域探索通訊協定，當區域可供使用時它們會自動偵測，並將讀取呼叫重新導向至慣用區域清單中下一個可用的區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-132">The Cosmos DB SDKs implement a regional discovery protocol that allows them to automatically detect when a region is available and redirect read calls to the next available region in the preferred region list.</span></span> <span data-ttu-id="d887d-133">如果慣用區域清單中的區域都無法使用，呼叫會自動切換回目前的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-133">If none of the regions in the preferred region list is available, calls automatically fall back to the current write region.</span></span> <span data-ttu-id="d887d-134">不需要對應用程式的程式碼做任何變更來處理區域容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d887d-134">No changes are required in your application code to handle regional failovers.</span></span> <span data-ttu-id="d887d-135">整個過程中，絲毫無損 Cosmos DB 的一致性保證。</span><span class="sxs-lookup"><span data-stu-id="d887d-135">During this entire process, consistency guarantees continue to be honored by Cosmos DB.</span></span>

![Azure Cosmos DB 中的讀取區域失敗](./media/regional-failover/read-region-failures.png)

<span data-ttu-id="d887d-137">一旦受影響區域從中斷復原，服務會自動回復該區域中所有受影響的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d887d-137">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span></span> <span data-ttu-id="d887d-138">讀取區域在受影響區域中的 Cosmos DB 帳戶，則會自動與目前寫入區域同步，並開啟上線。</span><span class="sxs-lookup"><span data-stu-id="d887d-138">Cosmos DB accounts that had a read region in the affected region will then automatically sync with current write region and turn online.</span></span> <span data-ttu-id="d887d-139">Cosmos DB SDK 會探索新區域的可用性，並根據應用程式設定的慣用區域清單，評估是否應該選取該區域做為目前讀取區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-139">The Cosmos DB SDKs discover the availability of the new region and evaluate whether the region should be selected as the current read region based on the preferred region list configured by the application.</span></span> <span data-ttu-id="d887d-140">後續的讀取會被重新導向至復原的區域，不需要對應用程式的程式碼做任何變更。</span><span class="sxs-lookup"><span data-stu-id="d887d-140">Subsequent reads are redirected to the recovered region without requiring any changes to your application code.</span></span>

<span data-ttu-id="d887d-141">**如果寫入區域中斷會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="d887d-141">**What happens if a write region has an outage?**</span></span>

<span data-ttu-id="d887d-142">如果受影響的區域是 Cosmos DB 帳戶的目前寫入區域，則該區域會自動標示為離線。</span><span class="sxs-lookup"><span data-stu-id="d887d-142">If the affected region is the current write region for a given Cosmos DB account, then the region will be automatically marked as offline.</span></span> <span data-ttu-id="d887d-143">然後，每個受影響 Cosmos DB 帳戶的替代區域會升級為寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-143">Then, an alternative region is promoted as the write region each affected Cosmos DB account.</span></span> <span data-ttu-id="d887d-144">您可以透過 Azure 入口網站或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange)，完全控制 Cosmos DB 帳戶的區域選擇順序。</span><span class="sxs-lookup"><span data-stu-id="d887d-144">You can fully control the region selection order for your Cosmos DB accounts via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange).</span></span> 

![Azure Cosmos DB 的容錯移轉優先順序](./media/regional-failover/failover-priorities.png)

<span data-ttu-id="d887d-146">在自動容錯移轉期間，Cosmos DB 會根據 Azure Cosmos DB 帳戶指定的優先順序，自動選擇下一個寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-146">During automatic failovers, Cosmos DB automatically chooses the next write region for a given Cosmos DB account based on the specified priority order.</span></span> 

![Azure Cosmos DB 中的寫入區域失敗](./media/regional-failover/write-region-failures.png)

<span data-ttu-id="d887d-148">一旦受影響區域從中斷復原，服務會自動回復該區域中所有受影響的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d887d-148">Once the affected region recovers from the outage, all the affected Cosmos DB accounts in the region are automatically recovered by the service.</span></span> 

* <span data-ttu-id="d887d-149">原先寫入區域在受影響區域中的 Cosmos DB 帳戶，即使在區域復原後，仍會保持具可讀取性的離線模式。</span><span class="sxs-lookup"><span data-stu-id="d887d-149">Cosmos DB accounts with their previous write region in the affected region will stay in an offline mode with read availability even after the recovery of the region.</span></span> 
* <span data-ttu-id="d887d-150">在中斷期間，您可以與目前寫入區域中的可用資料比較，藉此查詢此區域來計算任何未複寫的寫入。</span><span class="sxs-lookup"><span data-stu-id="d887d-150">You can query this region to compute any unreplicated writes during the outage by comparing with the data available in the current write region.</span></span> <span data-ttu-id="d887d-151">根據您的應用程式需求，您可以執行合併和/或衝突解決，並將最後一組變更寫回目前的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-151">Based on the needs of your application, you can perform merge and/or conflict resolution and write the final set of changes back to the current write region.</span></span> 
* <span data-ttu-id="d887d-152">完成合併變更後，您可以在 Cosmos DB 帳戶中移除再重新新增區域，將受影響的區域帶回線上。</span><span class="sxs-lookup"><span data-stu-id="d887d-152">Once you've completed merging changes, you can bring the affected region back online by removing and readding the region to your Cosmos DB account.</span></span> <span data-ttu-id="d887d-153">一旦將區域新增回來，您就可以透過 Azure 入口網站或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)執行手動容錯移轉，將它設回寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-153">Once the region is added back, you can configure it back as the write region by performing a manual failover via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span>

## <span data-ttu-id="d887d-154"><a id="ManualFailovers"></a>手動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="d887d-154"><a id="ManualFailovers"></a>Manual Failovers</span></span>

<span data-ttu-id="d887d-155">除了自動容錯移轉，可以手動將指定 Cosmos DB 帳戶的目前寫入區域動態變更為現有讀取區域之一。</span><span class="sxs-lookup"><span data-stu-id="d887d-155">In addition to automatic failovers, the current write region of a given Cosmos DB account can be manually changed dynamically to one of the existing read regions.</span></span> <span data-ttu-id="d887d-156">手動容錯移轉可透過 Azure 入口網站或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)起始。</span><span class="sxs-lookup"><span data-stu-id="d887d-156">Manual failovers can be initiated via the Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span> 

<span data-ttu-id="d887d-157">手動容錯移轉可確保「資料零遺失」和「可用性零遺失」，並正常地將指定 Cosmos DB 帳戶的寫入狀態從舊的寫入區域傳輸到新的。</span><span class="sxs-lookup"><span data-stu-id="d887d-157">Manual failovers ensure **zero data loss** and **zero availability** loss and gracefully transfer write status from the old write region to the new one for the specified Cosmos DB account.</span></span> <span data-ttu-id="d887d-158">像自動容錯移轉一樣，Cosmos DB SDK 會在手動容錯移轉期間自動處理寫入區域的變更，並確保會自動將呼叫重新導向至新的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-158">Like in automatic failovers, the Cosmos DB SDK automatically handles write region changes during manual failovers and ensures that calls are automatically redirected to the new write region.</span></span> <span data-ttu-id="d887d-159">不需要對應用程式的程式碼或設定做任何變更來管理容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d887d-159">No code or configuration changes are required in your application to manage failovers.</span></span> 

![Azure Cosmos DB 中的手動容錯移轉](./media/regional-failover/manual-failovers.png)

<span data-ttu-id="d887d-161">手動容錯移轉很實用的常見案例有︰</span><span class="sxs-lookup"><span data-stu-id="d887d-161">Some of the common scenarios where manual failover can be useful are:</span></span>

<span data-ttu-id="d887d-162">**遵循時鐘模型**︰如果您的應用程式可根據一天中的時間預測流量模式，您可以根據當日的時間定期將寫入狀態變更為最常使用的地理區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-162">**Follow the clock model**: If your applications have predictable traffic patterns based on the time of the day, you can periodically change the write status to the most active geographic region based on time of the day.</span></span>

<span data-ttu-id="d887d-163">**服務更新**︰某些分散在世界各地的應用程式部署，可能會在其規劃的服務更新期間透過流量管理員將流量重新路由至其他區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-163">**Service update**: Certain globally distributed application deployment may involve rerouting traffic to different region via traffic manager during their planned service update.</span></span> <span data-ttu-id="d887d-164">現在，這類應用程式部署可以使用手動容錯移轉，將寫入狀態保持為在服務更新期間即將有活躍流量的區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-164">Such application deployment now can use manual failover to keep the write status to the region where there is going to be active traffic during the service update window.</span></span>

<span data-ttu-id="d887d-165">**商務持續性和災害復原 (BCDR) 及高可用性和災害復原 (HADR) 演練**︰大多數企業應用程式都會將商務持續性測試納入其開發和發行程序。</span><span class="sxs-lookup"><span data-stu-id="d887d-165">**Business Continuity and Disaster Recovery (BCDR) and High Availability and Disaster Recovery (HADR) drills**: Most enterprise applications include business continuity tests as part of their development and release process.</span></span> <span data-ttu-id="d887d-166">BCDR 和 HADR 測試通常是合規性認證及發生區域性中斷時保證服務可用性的重要步驟。</span><span class="sxs-lookup"><span data-stu-id="d887d-166">BCDR and HADR testing is often an important step in compliance certifications and guaranteeing service availability in the case of regional outages.</span></span> <span data-ttu-id="d887d-167">您可以針對使用 Cosmos DB 做為儲存體的應用程式測試 BCDR 完備性，做法是觸發 Cosmos DB 帳戶的手動容錯移轉，及/或動態新增並移除區域。</span><span class="sxs-lookup"><span data-stu-id="d887d-167">You can test the BCDR readiness of your applications that use Cosmos DB for storage by triggering a manual failover of your Cosmos DB account and/or adding and removing a region dynamically.</span></span>

<span data-ttu-id="d887d-168">在本文中，我們看了在 Azure Cosmos DB 中手動和自動容錯移轉如何運作，以及如何將 Cosmos DB 帳戶和應用程式設定為可全域使用。</span><span class="sxs-lookup"><span data-stu-id="d887d-168">In this article, we reviewed how manual and automatic failovers work in Cosmos DB, and how you can configure your Cosmos DB accounts and applications to be globally available.</span></span> <span data-ttu-id="d887d-169">使用 Cosmos DB 的全域複寫支援，可以改善端對端延遲，並確保其即使是在區域失敗時仍有高可用性。</span><span class="sxs-lookup"><span data-stu-id="d887d-169">By using Cosmos DB's global replication support, you can improve end-to-end latency and ensure that they are highly available even in the event of region failures.</span></span> 

## <span data-ttu-id="d887d-170"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="d887d-170"><a id="NextSteps"></a>Next Steps</span></span>
* <span data-ttu-id="d887d-171">了解 Cosmos DB 如何支援[全域散發](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="d887d-171">Learn about how Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="d887d-172">了解 [Azure Cosmos DB 的全域一致性](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="d887d-172">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="d887d-173">使用 Azure Cosmos DB 的 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md) 進行多區域開發</span><span class="sxs-lookup"><span data-stu-id="d887d-173">Develop with multiple regions using Azure Cosmos DB's [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="d887d-174">了解如何使用 Azure DocumentDB 建置[多區域寫入器架構](multi-region-writers.md)</span><span class="sxs-lookup"><span data-stu-id="d887d-174">Learn how to build [Multi-region writer architectures](multi-region-writers.md) with Azure DocumentDB</span></span>

