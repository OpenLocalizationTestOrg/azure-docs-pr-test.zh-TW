---
title: "在入口網站中建立 Azure 搜尋服務 | Microsoft Docs"
description: "在入口網站中佈建 Azure 搜尋服務。"
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 58f4eab190e40e16ed261c165ffdfc8155eeb434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-search-service-in-the-portal"></a><span data-ttu-id="ddaf7-103">在入口網站中建立 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="ddaf7-103">Create an Azure Search service in the portal</span></span>

<span data-ttu-id="ddaf7-104">本文說明如何在入口網站中建立或佈建 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-104">This article explains how to create or provision an Azure Search service in the portal.</span></span> <span data-ttu-id="ddaf7-105">如需 PowerShell 的指示，請參閱[使用 PowerShell 管理 Azure 搜尋服務](search-manage-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="ddaf7-106">訂閱 (免費或付費)</span><span class="sxs-lookup"><span data-stu-id="ddaf7-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="ddaf7-107">[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，並使用免費信用額度來試用付費的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits to try out paid Azure services.</span></span> <span data-ttu-id="ddaf7-108">當您用完信用額度之後，請保留帳戶，並繼續使用免費的 Azure 服務，例如網站。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-108">After credits are used up, keep the account and continue to use free Azure services, such as Websites.</span></span> <span data-ttu-id="ddaf7-109">除非您明確變更您的設定且同意付費，否則我們絕對不會從您的信用卡收取任何費用。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-109">Your credit card is never charged unless you explicitly change your settings and ask to be charged.</span></span>

<span data-ttu-id="ddaf7-110">或者，請[啟用 MSDN 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="ddaf7-111">MSDN 訂用帳戶每月會提供您信用額度，讓您可以用於 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="ddaf7-112">尋找 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="ddaf7-112">Find Azure Search</span></span>
1. <span data-ttu-id="ddaf7-113">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-113">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ddaf7-114">按一下左上角的加號 ("+")。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-114">Click the plus sign ("+") in the top left corner.</span></span>
3. <span data-ttu-id="ddaf7-115">選取 [Web + 行動] > [Azure 搜尋服務]。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-the-service-and-url-endpoint"></a><span data-ttu-id="ddaf7-116">為服務和 URL 端點命名</span><span class="sxs-lookup"><span data-stu-id="ddaf7-116">Name the service and URL endpoint</span></span>

<span data-ttu-id="ddaf7-117">服務名稱是 URL 端點的一部分，API 呼叫是根據此端點所發出。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-117">A service name is part of the URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="ddaf7-118">在 [URL] 欄位中輸入您的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-118">Type your service name in the **URL** field.</span></span> 

<span data-ttu-id="ddaf7-119">服務名稱需求：</span><span class="sxs-lookup"><span data-stu-id="ddaf7-119">Service name requirements:</span></span>
   * <span data-ttu-id="ddaf7-120">長度為 2 到 60 個字元</span><span class="sxs-lookup"><span data-stu-id="ddaf7-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="ddaf7-121">小寫字母、數字或連字號 ("-")</span><span class="sxs-lookup"><span data-stu-id="ddaf7-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="ddaf7-122">不能使用連字號 ("-") 作為前 2 個字元或最後一個字元</span><span class="sxs-lookup"><span data-stu-id="ddaf7-122">no dash ("-") as the first 2 characters or last single character</span></span>
   * <span data-ttu-id="ddaf7-123">不能是連續的破折號 ("-")</span><span class="sxs-lookup"><span data-stu-id="ddaf7-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="ddaf7-124">選取一個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ddaf7-124">Select a subscription</span></span>
<span data-ttu-id="ddaf7-125">如果您有一個以上的訂用帳戶，請選擇一個同樣具有資料或檔案儲存體服務的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="ddaf7-126">Azure 搜尋服務可以透過「索引子」自動偵測 Azure 資料表和 Blob 儲存體、SQL Database 和 Azure Cosmos DB 以進行索引編製，但只會針對相同訂用帳戶中的服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in the same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="ddaf7-127">選取資源群組</span><span class="sxs-lookup"><span data-stu-id="ddaf7-127">Select a resource group</span></span>
<span data-ttu-id="ddaf7-128">資源群組是一起使用之 Azure 服務和資源的集合。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="ddaf7-129">例如，如果您使用 Azure 搜尋服務來編製 SQL 資料庫的索引，則這兩個服務應該屬於同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-129">For example, if you are using Azure Search to index a SQL database, then both services should be part of the same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="ddaf7-130">刪除資源群組也會刪除其中的服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-130">Deleting a resource group also deletes the services within it.</span></span> <span data-ttu-id="ddaf7-131">針對使用多個服務的原型專案，將它們全部放入同一個資源群組，在專案結束之後就能更容易清除。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-131">For prototype projects utilizing multiple services, putting all of them in the same resource group makes cleanup easier after the project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="ddaf7-132">選取裝載位置</span><span class="sxs-lookup"><span data-stu-id="ddaf7-132">Select a hosting location</span></span> 
<span data-ttu-id="ddaf7-133">做為 Azure 服務，Azure 搜尋服務可以裝載於世界各地的資料中心。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-133">As an Azure service, Azure Search can be hosted in datacenters around the world.</span></span> <span data-ttu-id="ddaf7-134">請注意，各地理位置的[價格可能不同](https://azure.microsoft.com/pricing/details/search/) 。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="ddaf7-135">選取定價層 (SKU)</span><span class="sxs-lookup"><span data-stu-id="ddaf7-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="ddaf7-136">[Azure 搜尋服務目前提供多個定價層](https://azure.microsoft.com/pricing/details/search/)︰免費、基本或標準。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="ddaf7-137">每一層都有自己的[容量和限制](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="ddaf7-138">請參閱[選擇定價層或 SKU](search-sku-tier.md) 以取得指導方針。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="ddaf7-139">在此逐步解說中，我們已為服務選擇標準層。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-139">In this walkthrough, we have chosen the Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="ddaf7-140">建立您的服務</span><span class="sxs-lookup"><span data-stu-id="ddaf7-140">Create your service</span></span>

<span data-ttu-id="ddaf7-141">請記得將您的服務釘選到儀表板，以方便在登入時存取。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-141">Remember to pin your service to the dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="ddaf7-142">調整您的服務</span><span class="sxs-lookup"><span data-stu-id="ddaf7-142">Scale your service</span></span>
<span data-ttu-id="ddaf7-143">可能需要幾分鐘的時間來建立服務 (視層級而定，15 分鐘或更多)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-143">It can take a few minutes to create a service (15 minutes or more depending on the tier).</span></span> <span data-ttu-id="ddaf7-144">佈建完您的服務之後，您可以調整它以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-144">After your service is provisioned, you can scale it to meet your needs.</span></span> <span data-ttu-id="ddaf7-145">由於您為「Azure 搜尋服務」選擇了「標準」層，因此您可以在兩個維度調整服務︰複本和資料分割。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-145">Because you chose the Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="ddaf7-146">如果您選擇的是「基本」層，則只能新增複本。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-146">Had you chosen the Basic tier, you can only add replicas.</span></span> <span data-ttu-id="ddaf7-147">如果您佈建的是免費服務，則無法進行調整。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-147">If you provisioned the free service, scale is not available.</span></span>

<span data-ttu-id="ddaf7-148">「資料分割」允許您的服務儲存及搜尋更多文件。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-148">***Partitions*** allow your service to store and search through more documents.</span></span>

<span data-ttu-id="ddaf7-149">「複本」允許服務來處理更高的搜尋查詢負載。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-149">***Replicas*** allow your service to handle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="ddaf7-150">服務必須具有 [2 個唯讀 SLA 的複本和 3 個讀/寫 SLA 的複本](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="ddaf7-151">在 Azure 入口網站中移至您的搜尋服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-151">Go to your search service blade in the Azure portal.</span></span>
2. <span data-ttu-id="ddaf7-152">在左導覽窗格中，選取 [設定] > [調整]。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-152">In the left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="ddaf7-153">使用滑桿來新增複本或分割區。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-153">Use the slidebar to add Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="ddaf7-154">關於單一服務中允許的搜尋單位總數 (複本 * 分割區 = 搜尋單位總數)，每一層各有不同的[限制](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-154">Each tier has different [limits](search-limits-quotas-capacity.md) on the total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-to-add-a-second-service"></a><span data-ttu-id="ddaf7-155">新增第二個服務的時機</span><span class="sxs-lookup"><span data-stu-id="ddaf7-155">When to add a second service</span></span>

<span data-ttu-id="ddaf7-156">大部分的客戶都是使用在提供[正確資源平衡](search-sku-tier.md)的層上佈建的單一服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-156">A large majority of customers use just one service provisioned at a tier that provides the [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="ddaf7-157">單一服務可以裝載多個索引 (數量受限於[所選層的最大限制](search-capacity-planning.md))，且每個索引都互相隔離。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-157">One service can host multiple indexes, subject to the [maximum limits of the tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="ddaf7-158">在 Azure 搜尋服務中，要求只能導向到單一索引，以降低意外或刻意從相同服務的其他索引中擷取資料的機會。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-158">In Azure Search, requests can only be directed to one index, minimizing the chance of accidental or intentional data retrieval from other indexes in the same service.</span></span>

<span data-ttu-id="ddaf7-159">雖然大部分的客戶只使用單一服務，但如果操作需求包含下列項目，則可能需要服務備援：</span><span class="sxs-lookup"><span data-stu-id="ddaf7-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include the following:</span></span>

+ <span data-ttu-id="ddaf7-160">災害復原 (資料中心中斷)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="ddaf7-161">Azure 搜尋服務在中斷時不會提供即時容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-161">Azure Search does not provide instant failover in the event of an outage.</span></span> <span data-ttu-id="ddaf7-162">如需建議和指導方針，請參閱[服務管理](search-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="ddaf7-163">您的多租用戶模型調查判斷額外服務為最佳化設計。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-163">Your investigation of multi-tenancy modeling has determined that additional services is the optimal design.</span></span> <span data-ttu-id="ddaf7-164">如需詳細資訊，請參閱[針對多租用戶設計](search-modeling-multitenant-saas-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="ddaf7-165">針對全球部署的應用程式，您在多個區域可能都需要 Azure 搜尋服務執行個體，以降低應用程式國際流量的延遲。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions to minimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="ddaf7-166">在 Azure 搜尋服務中，您無法區隔索引和查詢工作負載，因此您永遠不會針對區隔的工作負載建立多重服務。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="ddaf7-167">一律是在建立索引的服務上查詢該索引 (您無法在某個服務中建立索引，並將它複製到另一個服務)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-167">An index is always queried on the service in which it was created (you cannot create an index in one service and copy it to another).</span></span>
>

<span data-ttu-id="ddaf7-168">不需要第二個服務即可獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-168">A second service is not required for high availability.</span></span> <span data-ttu-id="ddaf7-169">當您在同一個服務中使用 2 個或更多的複本，查詢就會達到高可用性。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-169">High availability for queries is achieved when you use 2 or more replicas in the same service.</span></span> <span data-ttu-id="ddaf7-170">複本更新是循序的，這表示當服務更新推出時，至少會有一個複本是可運作的。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out.</span></span> <span data-ttu-id="ddaf7-171">如需執行時間的詳細資訊，請參閱[服務等級協定](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-171">For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddaf7-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddaf7-172">Next steps</span></span>
<span data-ttu-id="ddaf7-173">佈建 Azure 搜尋服務之後，您就可以[定義索引](search-what-is-an-index.md)，以便上傳和搜尋您的資料。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-173">After provisioning an Azure Search service, you are ready to [define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="ddaf7-174">若要從程式碼或指令碼存取服務，請提供 URL (*service-name*.search.windows.net) 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-174">To access the service from code or script, provide the URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="ddaf7-175">系統管理金鑰授與完整存取權；查詢金鑰則授與唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-175">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="ddaf7-176">請參閱[如何在 .NET 中使用 Azure 搜尋服務](search-howto-dotnet-sdk.md)以便開始使用。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-176">See [How to use Azure Search in .NET](search-howto-dotnet-sdk.md) to get started.</span></span>

<span data-ttu-id="ddaf7-177">請參閱[建置及查詢您的第一個索引](search-get-started-portal.md)，來取得以入口網站為基礎的快速教學課程。</span><span class="sxs-lookup"><span data-stu-id="ddaf7-177">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

