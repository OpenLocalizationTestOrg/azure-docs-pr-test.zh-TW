---
title: "在 Azure Cosmos DB aaaRegional 容錯移轉 |Microsoft 文件"
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
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a><span data-ttu-id="5ff8d-103">Azure Cosmos DB 中商務持續性的自動區域性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5ff8d-103">Automatic regional failover for business continuity in Azure Cosmos DB</span></span>
<span data-ttu-id="5ff8d-104">Azure Cosmos DB hello 全域發佈的資料，藉以簡化供應項目完整進行管理，[多區域資料庫帳戶](distribute-data-globally.md)提供清楚的權衡取捨完全之間的一致性、 可用性和效能，所有的對應保證。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-104">Azure Cosmos DB simplifies hello global distribution of data by offering fully managed, [multi-region database accounts](distribute-data-globally.md) that provide clear tradeoffs between consistency, availability, and performance, all with corresponding guarantees.</span></span> <span data-ttu-id="5ff8d-105">Cosmos DB 帳戶提供高可用性，單一位數毫秒的延遲，[妥善定義的一致性層級](consistency-levels.md)，透明區域的容錯移轉多路連接的應用程式開發介面，和 hello 能力 tooelastically 標尺輸送量與儲存體跨 hello 地球。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-105">Cosmos DB accounts offer high availability, single digit ms latencies, [well-defined consistency levels](consistency-levels.md), transparent regional failover with multi-homing APIs, and hello ability tooelastically scale throughput and storage across hello globe.</span></span> 

<span data-ttu-id="5ff8d-106">Cosmos DB 明確同時支援和原則導向的容錯移轉可讓您 toocontrol hello 端對端的系統行為在 hello 事件中的失敗。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-106">Cosmos DB supports both explicit and policy driven failovers that allow you toocontrol hello end-to-end system behavior in hello event of failures.</span></span> <span data-ttu-id="5ff8d-107">我們將在本文中說明：</span><span class="sxs-lookup"><span data-stu-id="5ff8d-107">In this article, we look at:</span></span>

* <span data-ttu-id="5ff8d-108">Cosmos DB 的手動容錯移轉如何運作？</span><span class="sxs-lookup"><span data-stu-id="5ff8d-108">How do manual failovers work in Cosmos DB?</span></span>
* <span data-ttu-id="5ff8d-109">自動容錯移轉在 Cosmos DB 中如何運作，以及當資料中心當機時會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="5ff8d-109">How do automatic failovers work in Cosmos DB and what happens when a data center goes down?</span></span>
* <span data-ttu-id="5ff8d-110">如何在應用程式架構中使用手動容錯移轉？</span><span class="sxs-lookup"><span data-stu-id="5ff8d-110">How can you use manual failovers in application architectures?</span></span>

<span data-ttu-id="5ff8d-111">您也可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解區域容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-111">You can also learn about regional failovers in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <span data-ttu-id="5ff8d-112"><a id="ConfigureMultiRegionApplications"></a>設定多區域應用程式</span><span class="sxs-lookup"><span data-stu-id="5ff8d-112"><a id="ConfigureMultiRegionApplications"></a>Configuring multi-region applications</span></span>
<span data-ttu-id="5ff8d-113">我們深入了解容錯移轉模式之前，我們探討您可以設定應用程式的多重區域可用性 tootake 優點和 hello 表面區域的容錯移轉中有彈性的方式。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-113">Before we dive into failover modes, we look at how you can configure an application tootake advantage of multi-region availability and be resilient in hello face of regional failovers.</span></span>

* <span data-ttu-id="5ff8d-114">首先，在多個區域中部署您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5ff8d-114">First, deploy your application in multiple regions</span></span>
* <span data-ttu-id="5ff8d-115">從您的應用程式部署時，每個區域 tooensure 低延遲存取設定 hello 對應[慣用的區域清單](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations)透過其中一個 hello 各地區支援的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-115">tooensure low latency access from every region your application is deployed, configure hello corresponding [preferred regions list](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) for each region via one of hello supported SDKs.</span></span>

<span data-ttu-id="5ff8d-116">下列程式碼片段說明如何 hello tooinitialize 多區域應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-116">hello following snippet shows how tooinitialize a multi-region application.</span></span> <span data-ttu-id="5ff8d-117">在這裡，hello Azure Cosmos DB 帳戶`contoso.documents.azure.com`設有兩個區域-美國西部和北歐。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-117">Here, hello Azure Cosmos DB account `contoso.documents.azure.com` is configured with two regions - West US and North Europe.</span></span> 

* <span data-ttu-id="5ff8d-118">hello 應用程式被部署在 hello 美國西部地區 （例如，使用 Azure 應用程式服務）</span><span class="sxs-lookup"><span data-stu-id="5ff8d-118">hello application is deployed in hello West US region (using Azure App Services for example)</span></span> 
* <span data-ttu-id="5ff8d-119">設定`West US`為 hello 第一個慣用的區域為低延遲讀取</span><span class="sxs-lookup"><span data-stu-id="5ff8d-119">Configured with `West US` as hello first preferred region for low latency reads</span></span>
* <span data-ttu-id="5ff8d-120">設定`North Europe`為 hello 第二個慣用的區域 （適用於在地區失敗時的高可用性）</span><span class="sxs-lookup"><span data-stu-id="5ff8d-120">Configured with `North Europe` as hello second preferred region (for high availability during regional failures)</span></span>

<span data-ttu-id="5ff8d-121">Hello DocumentDB API，在此組態看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ff8d-121">In hello DocumentDB API, this configuration looks like hello following snippet:</span></span>

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

hello 應用程式也部署在 hello 北歐 hello 順序反轉的慣用區域的區域中。 也就是針對低度延遲讀取時先指定 hello 北歐區域。 <span data-ttu-id="5ff8d-124">然後，hello 美國西部地區 hello 第二個慣用的地區高可用性為期間指定地區的失敗。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-124">Then, hello West US region is specified as hello second preferred region for high availability during regional failures.</span></span>

<span data-ttu-id="5ff8d-125">hello 架構圖顯示多區域應用程式部署 Cosmos DB 與 hello 應用程式會設定的 toobe 可用在四個 Azure 地理區域中。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-125">hello following architecture diagram shows a multi-region application deployment where Cosmos DB and hello application are configured toobe available in four Azure geographic regions.</span></span>  

![使用 Cosmos DB 部署全域分散式應用程式](./media/regional-failover/app-deployment.png)

<span data-ttu-id="5ff8d-127">現在，讓我們看看如何 hello Cosmos DB 服務處理地區透過自動容錯移轉失敗。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-127">Now, let's look at how hello Cosmos DB service handles regional failures via automatic failovers.</span></span> 

## <span data-ttu-id="5ff8d-128"><a id="AutomaticFailovers"></a>自動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5ff8d-128"><a id="AutomaticFailovers"></a>Automatic Failovers</span></span>
<span data-ttu-id="5ff8d-129">在 hello 罕見事件中的 Azure 地區中斷或資料中心完全停止運作，Cosmos DB 都會自動觸發容錯移轉的 hello 受影響區域中出現的所有 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-129">In hello rare event of an Azure regional outage or data center outage, Cosmos DB automatically triggers failovers of all Cosmos DB accounts with a presence in hello affected region.</span></span> 

<span data-ttu-id="5ff8d-130">**如果讀取區域中斷會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="5ff8d-130">**What happens if a read region has an outage?**</span></span>

<span data-ttu-id="5ff8d-131">與唯讀區域中的其中一個受影響的 hello 區域 cosmos DB 帳戶自動中斷其寫入區域並標示為離線。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-131">Cosmos DB accounts with a read region in one of hello affected regions are automatically disconnected from their write region and marked offline.</span></span> <span data-ttu-id="5ff8d-132">區域是使用重新導向讀取呼叫 toohello 下一個可用的地區 hello 慣用的地區清單中，偵測到 hello Cosmos DB Sdk 實作外面 tooautomatically 地區的探索通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-132">hello Cosmos DB SDKs implement a regional discovery protocol that allows them tooautomatically detect when a region is available and redirect read calls toohello next available region in hello preferred region list.</span></span> <span data-ttu-id="5ff8d-133">如果無 hello 中的 hello 區域偏好的地區清單為可用，呼叫會自動切換回 toohello 目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-133">If none of hello regions in hello preferred region list is available, calls automatically fall back toohello current write region.</span></span> <span data-ttu-id="5ff8d-134">您的應用程式程式碼 toohandle 地區容錯移轉，不需要任何變更。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-134">No changes are required in your application code toohandle regional failovers.</span></span> <span data-ttu-id="5ff8d-135">在整個過程中，一致性保證會繼續接受 Cosmos DB toobe。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-135">During this entire process, consistency guarantees continue toobe honored by Cosmos DB.</span></span>

![Azure Cosmos DB 中的讀取區域失敗](./media/regional-failover/read-region-failures.png)

<span data-ttu-id="5ff8d-137">一旦從 hello 中斷復原受影響的 hello 區域，hello 區域中的所有受影響的 hello Cosmos DB 帳戶會自動回復 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-137">Once hello affected region recovers from hello outage, all hello affected Cosmos DB accounts in hello region are automatically recovered by hello service.</span></span> <span data-ttu-id="5ff8d-138">Cosmos DB 帳戶 hello 受影響區域中已讀取的區域會自動同步目前寫入區域然後開啟線上。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-138">Cosmos DB accounts that had a read region in hello affected region will then automatically sync with current write region and turn online.</span></span> <span data-ttu-id="5ff8d-139">hello Cosmos DB Sdk 探索 hello 的 hello 新區域的可用性，並評估是否應該為 hello 目前讀取區域 hello 應用程式所設定的 hello 慣用的地區清單為基礎選取 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-139">hello Cosmos DB SDKs discover hello availability of hello new region and evaluate whether hello region should be selected as hello current read region based on hello preferred region list configured by hello application.</span></span> <span data-ttu-id="5ff8d-140">後續的讀取會重新導向的 toohello 復原的區域，而不需要任何變更 tooyour 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-140">Subsequent reads are redirected toohello recovered region without requiring any changes tooyour application code.</span></span>

<span data-ttu-id="5ff8d-141">**如果寫入區域中斷會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="5ff8d-141">**What happens if a write region has an outage?**</span></span>

<span data-ttu-id="5ff8d-142">如果指定的 Cosmos DB 帳戶 hello 目前寫入區域 hello 受影響的區域，然後 hello 區域將會自動標示為離線。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-142">If hello affected region is hello current write region for a given Cosmos DB account, then hello region will be automatically marked as offline.</span></span> <span data-ttu-id="5ff8d-143">然後，hello 撰寫區域每個受影響的 Cosmos DB 帳戶時，會升級替代地區。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-143">Then, an alternative region is promoted as hello write region each affected Cosmos DB account.</span></span> <span data-ttu-id="5ff8d-144">您可以完全掌控 hello 地區選取項目順序的 Cosmos DB 帳戶透過 hello Azure 入口網站或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange)。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-144">You can fully control hello region selection order for your Cosmos DB accounts via hello Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange).</span></span> 

![Azure Cosmos DB 的容錯移轉優先順序](./media/regional-failover/failover-priorities.png)

<span data-ttu-id="5ff8d-146">自動的容錯移轉期間 Cosmos DB 自動選擇下一個寫入區域 hello 指定的 Cosmos db 指定優先順序根據 hello 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-146">During automatic failovers, Cosmos DB automatically chooses hello next write region for a given Cosmos DB account based on hello specified priority order.</span></span> 

![Azure Cosmos DB 中的寫入區域失敗](./media/regional-failover/write-region-failures.png)

<span data-ttu-id="5ff8d-148">一旦從 hello 中斷復原受影響的 hello 區域，hello 區域中的所有受影響的 hello Cosmos DB 帳戶會自動回復 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-148">Once hello affected region recovers from hello outage, all hello affected Cosmos DB accounts in hello region are automatically recovered by hello service.</span></span> 

* <span data-ttu-id="5ff8d-149">Cosmos DB 帳戶與他們 hello 受影響區域中的先前寫入區域停留在離線模式中讀取的可用性與 hello 區域 hello 復原後，即使。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-149">Cosmos DB accounts with their previous write region in hello affected region will stay in an offline mode with read availability even after hello recovery of hello region.</span></span> 
* <span data-ttu-id="5ff8d-150">您可以查詢此區域 toocompute 任何未複寫的寫入 hello 中斷期間藉由比較與 hello hello 目前寫入區域中可用的資料。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-150">You can query this region toocompute any unreplicated writes during hello outage by comparing with hello data available in hello current write region.</span></span> <span data-ttu-id="5ff8d-151">根據應用程式的 hello 需求，您可以執行合併和/或衝突解析並撰寫 hello 最終組的變更回復 toohello 目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-151">Based on hello needs of your application, you can perform merge and/or conflict resolution and write hello final set of changes back toohello current write region.</span></span> 
* <span data-ttu-id="5ff8d-152">當您完成變更之後時，您可以讓受影響的 hello 區域重新上線藉由移除 hello 區域 tooyour Cosmos DB 帳戶正在重新加入。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-152">Once you've completed merging changes, you can bring hello affected region back online by removing and readding hello region tooyour Cosmos DB account.</span></span> <span data-ttu-id="5ff8d-153">一旦 hello 區域就會重新加入，您可以設定回為 hello 寫入區域執行透過 hello Azure 入口網站的手動容錯移轉或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-153">Once hello region is added back, you can configure it back as hello write region by performing a manual failover via hello Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span>

## <span data-ttu-id="5ff8d-154"><a id="ManualFailovers"></a>手動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5ff8d-154"><a id="ManualFailovers"></a>Manual Failovers</span></span>

<span data-ttu-id="5ff8d-155">此外 tooautomatic 容錯移轉，目前的 hello 寫入指定的 Cosmos DB 帳戶的區域中，您可以手動變更動態 tooone 的 hello 現有唯讀區域。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-155">In addition tooautomatic failovers, hello current write region of a given Cosmos DB account can be manually changed dynamically tooone of hello existing read regions.</span></span> <span data-ttu-id="5ff8d-156">可透過 hello Azure 入口網站起始手動容錯移轉或[以程式設計方式](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate)。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-156">Manual failovers can be initiated via hello Azure portal or [programmatically](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).</span></span> 

<span data-ttu-id="5ff8d-157">手動容錯移轉確保**零資料遺失**和**零可用性**遺失而且依正常程序從舊的 hello 傳輸寫入狀態撰寫區域 toohello 新 hello 指定 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-157">Manual failovers ensure **zero data loss** and **zero availability** loss and gracefully transfer write status from hello old write region toohello new one for hello specified Cosmos DB account.</span></span> <span data-ttu-id="5ff8d-158">像是自動容錯移轉，hello Cosmos DB SDK 自動控制代碼會寫入區域手動容錯移轉期間變更，並確保呼叫不會自動重新導向的 toohello 新寫入的區域。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-158">Like in automatic failovers, hello Cosmos DB SDK automatically handles write region changes during manual failovers and ensures that calls are automatically redirected toohello new write region.</span></span> <span data-ttu-id="5ff8d-159">程式碼或組態不需要任何變更您的應用程式 toomanage 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-159">No code or configuration changes are required in your application toomanage failovers.</span></span> 

![Azure Cosmos DB 中的手動容錯移轉](./media/regional-failover/manual-failovers.png)

<span data-ttu-id="5ff8d-161">Hello 很有用的手動容錯移轉的常見案例包括：</span><span class="sxs-lookup"><span data-stu-id="5ff8d-161">Some of hello common scenarios where manual failover can be useful are:</span></span>

<span data-ttu-id="5ff8d-162">**遵循 hello 時鐘模型**： 如果您的應用程式有 hello hello 一天的時間為基礎的可預測的流量模式，您可以定期變更 hello 寫入狀態 toohello 最常使用地理區域的 hello 當日時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-162">**Follow hello clock model**: If your applications have predictable traffic patterns based on hello time of hello day, you can periodically change hello write status toohello most active geographic region based on time of hello day.</span></span>

<span data-ttu-id="5ff8d-163">**服務更新**： 特定全域散發的應用程式部署可能會重設透過流量管理員流量 toodifferent 區域路徑在其計劃的服務更新。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-163">**Service update**: Certain globally distributed application deployment may involve rerouting traffic toodifferent region via traffic manager during their planned service update.</span></span> <span data-ttu-id="5ff8d-164">這類應用程式部署現在可以使用手動容錯移轉 tookeep hello 寫入狀態 toohello 區域其中那里即將 toobe active 流量期間 hello 服務更新。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-164">Such application deployment now can use manual failover tookeep hello write status toohello region where there is going toobe active traffic during hello service update window.</span></span>

<span data-ttu-id="5ff8d-165">**商務持續性和災害復原 (BCDR) 及高可用性和災害復原 (HADR) 演練**︰大多數企業應用程式都會將商務持續性測試納入其開發和發行程序。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-165">**Business Continuity and Disaster Recovery (BCDR) and High Availability and Disaster Recovery (HADR) drills**: Most enterprise applications include business continuity tests as part of their development and release process.</span></span> <span data-ttu-id="5ff8d-166">BCDR 和 HADR 測試通常是在相容性認證中的一個重要步驟和地區的中斷的 hello 萬一保證服務可用性。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-166">BCDR and HADR testing is often an important step in compliance certifications and guaranteeing service availability in hello case of regional outages.</span></span> <span data-ttu-id="5ff8d-167">您可以測試 hello BCDR 整備觸發 Cosmos DB 帳戶的手動容錯移轉和/或新增及移除區域以動態方式透過使用儲存體 Cosmos DB 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-167">You can test hello BCDR readiness of your applications that use Cosmos DB for storage by triggering a manual failover of your Cosmos DB account and/or adding and removing a region dynamically.</span></span>

<span data-ttu-id="5ff8d-168">在本文中，我們已檢閱 Cosmos DB 中的方式手動和自動容錯移轉工作，您可以設定您 Cosmos DB 帳戶與應用程式 toobe 全域可用的方式。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-168">In this article, we reviewed how manual and automatic failovers work in Cosmos DB, and how you can configure your Cosmos DB accounts and applications toobe globally available.</span></span> <span data-ttu-id="5ff8d-169">使用 Cosmos DB 全域複寫支援，可以改進端對端延遲，並確保其高可用性，即使在 hello 的區域失敗的事件。</span><span class="sxs-lookup"><span data-stu-id="5ff8d-169">By using Cosmos DB's global replication support, you can improve end-to-end latency and ensure that they are highly available even in hello event of region failures.</span></span> 

## <span data-ttu-id="5ff8d-170"><a id="NextSteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ff8d-170"><a id="NextSteps"></a>Next Steps</span></span>
* <span data-ttu-id="5ff8d-171">了解 Cosmos DB 如何支援[全域散發](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="5ff8d-171">Learn about how Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="5ff8d-172">了解 [Azure Cosmos DB 的全域一致性](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="5ff8d-172">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="5ff8d-173">使用 Azure Cosmos DB 的 [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md) 進行多區域開發</span><span class="sxs-lookup"><span data-stu-id="5ff8d-173">Develop with multiple regions using Azure Cosmos DB's [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="5ff8d-174">深入了解如何 toobuild[多區域寫入器架構](multi-region-writers.md)與 Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="5ff8d-174">Learn how toobuild [Multi-region writer architectures](multi-region-writers.md) with Azure DocumentDB</span></span>

