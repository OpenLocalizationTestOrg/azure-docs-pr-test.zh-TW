---
title: "aaaCreate hello 入口網站中，在 Azure 搜尋服務 |Microsoft 文件"
description: "佈建 Azure 搜尋服務 hello 入口網站中。"
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
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a><span data-ttu-id="ce339-103">在 hello 入口網站中建立 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="ce339-103">Create an Azure Search service in hello portal</span></span>

<span data-ttu-id="ce339-104">本文說明如何 toocreate 或佈建 Azure 搜尋服務 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="ce339-104">This article explains how toocreate or provision an Azure Search service in hello portal.</span></span> <span data-ttu-id="ce339-105">如需 PowerShell 的指示，請參閱[使用 PowerShell 管理 Azure 搜尋服務](search-manage-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ce339-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="ce339-106">訂閱 (免費或付費)</span><span class="sxs-lookup"><span data-stu-id="ce339-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="ce339-107">[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)並使用免費信用額度 tootry 出支付 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits tootry out paid Azure services.</span></span> <span data-ttu-id="ce339-108">信用額度用完之後，保留 hello 帳戶，並繼續 toouse 免費的 Azure 服務，例如網站。</span><span class="sxs-lookup"><span data-stu-id="ce339-108">After credits are used up, keep hello account and continue toouse free Azure services, such as Websites.</span></span> <span data-ttu-id="ce339-109">除非您明確地變更您的設定，並詢問 toobe 收費，永遠不會收取您的信用卡。</span><span class="sxs-lookup"><span data-stu-id="ce339-109">Your credit card is never charged unless you explicitly change your settings and ask toobe charged.</span></span>

<span data-ttu-id="ce339-110">或者，請[啟用 MSDN 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="ce339-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="ce339-111">MSDN 訂用帳戶每月會提供您信用額度，讓您可以用於 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="ce339-112">尋找 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="ce339-112">Find Azure Search</span></span>
1. <span data-ttu-id="ce339-113">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ce339-113">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ce339-114">按一下 hello 加上正負號 （"+"） 中的 hello 左上角。</span><span class="sxs-lookup"><span data-stu-id="ce339-114">Click hello plus sign ("+") in hello top left corner.</span></span>
3. <span data-ttu-id="ce339-115">選取 [Web + 行動] > [Azure 搜尋服務]。</span><span class="sxs-lookup"><span data-stu-id="ce339-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a><span data-ttu-id="ce339-116">服務名稱的 hello 和 URL 端點</span><span class="sxs-lookup"><span data-stu-id="ce339-116">Name hello service and URL endpoint</span></span>

<span data-ttu-id="ce339-117">服務名稱是依據 API 呼叫所發出的 hello URL 端點的一部分。</span><span class="sxs-lookup"><span data-stu-id="ce339-117">A service name is part of hello URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="ce339-118">輸入您的服務名稱在 hello **URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="ce339-118">Type your service name in hello **URL** field.</span></span> 

<span data-ttu-id="ce339-119">服務名稱需求：</span><span class="sxs-lookup"><span data-stu-id="ce339-119">Service name requirements:</span></span>
   * <span data-ttu-id="ce339-120">長度為 2 到 60 個字元</span><span class="sxs-lookup"><span data-stu-id="ce339-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="ce339-121">小寫字母、數字或連字號 ("-")</span><span class="sxs-lookup"><span data-stu-id="ce339-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="ce339-122">沒有破折號 ("-") 為 hello 前 2 個或最後一個單一字元</span><span class="sxs-lookup"><span data-stu-id="ce339-122">no dash ("-") as hello first 2 characters or last single character</span></span>
   * <span data-ttu-id="ce339-123">不能是連續的破折號 ("-")</span><span class="sxs-lookup"><span data-stu-id="ce339-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="ce339-124">選取一個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ce339-124">Select a subscription</span></span>
<span data-ttu-id="ce339-125">如果您有一個以上的訂用帳戶，請選擇一個同樣具有資料或檔案儲存體服務的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce339-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="ce339-126">Azure 搜尋可以自動偵測 Azure 資料表和 Blob 儲存體、 SQL Database 和 Azure Cosmos DB 透過編製索引*索引子*，但只在 hello 服務相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce339-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in hello same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="ce339-127">選取資源群組</span><span class="sxs-lookup"><span data-stu-id="ce339-127">Select a resource group</span></span>
<span data-ttu-id="ce339-128">資源群組是一起使用之 Azure 服務和資源的集合。</span><span class="sxs-lookup"><span data-stu-id="ce339-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="ce339-129">比方說，如果您使用 Azure 搜尋 tooindex SQL 資料庫，則這兩項服務應該 hello 屬於相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ce339-129">For example, if you are using Azure Search tooindex a SQL database, then both services should be part of hello same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="ce339-130">刪除資源群組時，也會刪除 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-130">Deleting a resource group also deletes hello services within it.</span></span> <span data-ttu-id="ce339-131">利用多個服務，將它們全部放在 hello 原型專案相同的資源群組輕鬆清理之後 hello 專案是透過。</span><span class="sxs-lookup"><span data-stu-id="ce339-131">For prototype projects utilizing multiple services, putting all of them in hello same resource group makes cleanup easier after hello project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="ce339-132">選取裝載位置</span><span class="sxs-lookup"><span data-stu-id="ce339-132">Select a hosting location</span></span> 
<span data-ttu-id="ce339-133">作為 Azure 服務，可以在 hello 世界各地的資料中心裝載 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="ce339-133">As an Azure service, Azure Search can be hosted in datacenters around hello world.</span></span> <span data-ttu-id="ce339-134">請注意，各地理位置的[價格可能不同](https://azure.microsoft.com/pricing/details/search/) 。</span><span class="sxs-lookup"><span data-stu-id="ce339-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="ce339-135">選取定價層 (SKU)</span><span class="sxs-lookup"><span data-stu-id="ce339-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="ce339-136">[Azure 搜尋服務目前提供多個定價層](https://azure.microsoft.com/pricing/details/search/)︰免費、基本或標準。</span><span class="sxs-lookup"><span data-stu-id="ce339-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="ce339-137">每一層都有自己的[容量和限制](search-limits-quotas-capacity.md)。</span><span class="sxs-lookup"><span data-stu-id="ce339-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="ce339-138">請參閱[選擇定價層或 SKU](search-sku-tier.md) 以取得指導方針。</span><span class="sxs-lookup"><span data-stu-id="ce339-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="ce339-139">在本逐步解說中，我們選擇 hello 標準層針對我們的服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-139">In this walkthrough, we have chosen hello Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="ce339-140">建立您的服務</span><span class="sxs-lookup"><span data-stu-id="ce339-140">Create your service</span></span>

<span data-ttu-id="ce339-141">每當您登入記住 toopin 服務 toohello 儀表板，以方便存取。</span><span class="sxs-lookup"><span data-stu-id="ce339-141">Remember toopin your service toohello dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="ce339-142">調整您的服務</span><span class="sxs-lookup"><span data-stu-id="ce339-142">Scale your service</span></span>
<span data-ttu-id="ce339-143">它可能需要幾分鐘的時間 toocreate （15 分鐘或更多視 hello 層） 服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-143">It can take a few minutes toocreate a service (15 minutes or more depending on hello tier).</span></span> <span data-ttu-id="ce339-144">佈建您的服務之後，您可以調整它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="ce339-144">After your service is provisioned, you can scale it toomeet your needs.</span></span> <span data-ttu-id="ce339-145">因為您的 Azure 搜尋服務選擇 hello 標準層，您可以在兩個維度來調整您的服務： 複本和資料分割。</span><span class="sxs-lookup"><span data-stu-id="ce339-145">Because you chose hello Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="ce339-146">您已選擇 hello 基本層，您只能新增複本。</span><span class="sxs-lookup"><span data-stu-id="ce339-146">Had you chosen hello Basic tier, you can only add replicas.</span></span> <span data-ttu-id="ce339-147">如果您佈建 hello 免費服務，就無法使用小數位數。</span><span class="sxs-lookup"><span data-stu-id="ce339-147">If you provisioned hello free service, scale is not available.</span></span>

<span data-ttu-id="ce339-148">***資料分割***讓服務 toostore 和搜尋多個文件。</span><span class="sxs-lookup"><span data-stu-id="ce339-148">***Partitions*** allow your service toostore and search through more documents.</span></span>

<span data-ttu-id="ce339-149">***複本***允許服務 toohandle 的搜尋查詢更高的負載。</span><span class="sxs-lookup"><span data-stu-id="ce339-149">***Replicas*** allow your service toohandle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="ce339-150">服務必須具有 [2 個唯讀 SLA 的複本和 3 個讀/寫 SLA 的複本](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。</span><span class="sxs-lookup"><span data-stu-id="ce339-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="ce339-151">移 tooyour hello Azure 入口網站中的搜尋服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ce339-151">Go tooyour search service blade in hello Azure portal.</span></span>
2. <span data-ttu-id="ce339-152">在 hello 左瀏覽窗格中，選取 **設定** > **標尺**。</span><span class="sxs-lookup"><span data-stu-id="ce339-152">In hello left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="ce339-153">使用 hello slidebar tooadd 複本或資料分割。</span><span class="sxs-lookup"><span data-stu-id="ce339-153">Use hello slidebar tooadd Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="ce339-154">每個層次都有不同[限制](search-limits-quotas-capacity.md)hello 總數允許在單一服務中的搜尋單位 (複本 * 分割 = 總的搜尋單位)。</span><span class="sxs-lookup"><span data-stu-id="ce339-154">Each tier has different [limits](search-limits-quotas-capacity.md) on hello total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-tooadd-a-second-service"></a><span data-ttu-id="ce339-155">當 tooadd 第二個服務</span><span class="sxs-lookup"><span data-stu-id="ce339-155">When tooadd a second service</span></span>

<span data-ttu-id="ce339-156">大部分的客戶使用只有一個服務佈建於提供 hello 層[以滑鼠右鍵的資源平衡](search-sku-tier.md)。</span><span class="sxs-lookup"><span data-stu-id="ce339-156">A large majority of customers use just one service provisioned at a tier that provides hello [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="ce339-157">一項服務可以裝載多個索引、 主旨 toohello [hello 層您選取的最大限制](search-capacity-planning.md)，與從另一個隔離每個索引。</span><span class="sxs-lookup"><span data-stu-id="ce339-157">One service can host multiple indexes, subject toohello [maximum limits of hello tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="ce339-158">在 Azure 搜尋中，要求只能是導向的 tooone 索引，從其他意外或故意情況下的資料傳送的 hello 機會降到最低索引 hello 相同服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-158">In Azure Search, requests can only be directed tooone index, minimizing hello chance of accidental or intentional data retrieval from other indexes in hello same service.</span></span>

<span data-ttu-id="ce339-159">雖然大部分的客戶使用只有一個服務，服務備援可能需要如果操作需求 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="ce339-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include hello following:</span></span>

+ <span data-ttu-id="ce339-160">災害復原 (資料中心中斷)。</span><span class="sxs-lookup"><span data-stu-id="ce339-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="ce339-161">Azure 搜尋不提供立即中斷的 hello 事件中的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ce339-161">Azure Search does not provide instant failover in hello event of an outage.</span></span> <span data-ttu-id="ce339-162">如需建議和指導方針，請參閱[服務管理](search-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="ce339-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="ce339-163">將調查多租用戶模型的程式判定額外的服務為 hello 最佳設計。</span><span class="sxs-lookup"><span data-stu-id="ce339-163">Your investigation of multi-tenancy modeling has determined that additional services is hello optimal design.</span></span> <span data-ttu-id="ce339-164">如需詳細資訊，請參閱[針對多租用戶設計](search-modeling-multitenant-saas-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="ce339-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="ce339-165">針對全域部署的應用程式，您可能需要 Azure 搜尋的執行個體的多個區域 toominimize 延遲的應用程式的國際流量。</span><span class="sxs-lookup"><span data-stu-id="ce339-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions toominimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="ce339-166">在 Azure 搜尋服務中，您無法區隔索引和查詢工作負載，因此您永遠不會針對區隔的工作負載建立多重服務。</span><span class="sxs-lookup"><span data-stu-id="ce339-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="ce339-167">索引一律上查詢 hello 服務處於已建立 （您無法在一個服務中建立索引並將它複製 tooanother）。</span><span class="sxs-lookup"><span data-stu-id="ce339-167">An index is always queried on hello service in which it was created (you cannot create an index in one service and copy it tooanother).</span></span>
>

<span data-ttu-id="ce339-168">不需要第二個服務即可獲得高可用性。</span><span class="sxs-lookup"><span data-stu-id="ce339-168">A second service is not required for high availability.</span></span> <span data-ttu-id="ce339-169">使用 2 或多個複本中的 hello 相同的服務時，被達成高可用性的查詢。</span><span class="sxs-lookup"><span data-stu-id="ce339-169">High availability for queries is achieved when you use 2 or more replicas in hello same service.</span></span> <span data-ttu-id="ce339-170">複本更新是循序的，這表示當服務更新推出時，至少會有一個複本是可運作的。如需執行時間的詳細資訊，請參閱[服務等級協定](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。</span><span class="sxs-lookup"><span data-stu-id="ce339-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce339-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce339-171">Next steps</span></span>
<span data-ttu-id="ce339-172">之後佈建 Azure 搜尋服務，您就可以開始太[定義索引](search-what-is-an-index.md)讓您可以上傳，並搜尋您的資料。</span><span class="sxs-lookup"><span data-stu-id="ce339-172">After provisioning an Azure Search service, you are ready too[define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="ce339-173">從程式碼或指令碼，tooaccess hello 服務提供 hello URL (*服務名稱*。 search.windows.net) 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="ce339-173">tooaccess hello service from code or script, provide hello URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="ce339-174">系統管理金鑰授與完整存取權；查詢金鑰則授與唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="ce339-174">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="ce339-175">請參閱[如何 toouse Azure 搜尋.net](search-howto-dotnet-sdk.md) tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="ce339-175">See [How toouse Azure Search in .NET](search-howto-dotnet-sdk.md) tooget started.</span></span>

<span data-ttu-id="ce339-176">請參閱[建置及查詢您的第一個索引](search-get-started-portal.md)，來取得以入口網站為基礎的快速教學課程。</span><span class="sxs-lookup"><span data-stu-id="ce339-176">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

