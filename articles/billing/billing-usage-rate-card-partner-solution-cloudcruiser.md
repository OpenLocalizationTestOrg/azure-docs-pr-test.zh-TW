---
title: "aaaCloud Cruiser 和 Microsoft Azure 計費 API 整合 |Microsoft 文件"
description: "從 Microsoft Azure 計費夥伴 Cloud Cruiser 他們將 hello Azure 計費 Api 整合至其產品的經驗提供唯一的檢視方塊。  這特別適用於有興趣使用/嘗試將 Cloud Cruiser 用於 Microsoft Azure Pack 的客戶。"
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a><span data-ttu-id="73c58-104">Cloud Cruiser 和 Microsoft Azure 計費 API 整合</span><span class="sxs-lookup"><span data-stu-id="73c58-104">Cloud Cruiser and Microsoft Azure Billing API Integration</span></span>
<span data-ttu-id="73c58-105">本文說明如何從新 Microsoft Azure 計費 Api 可以在 Cloud Cruiser 用於工作流程的 hello 收集的 hello 資訊成本模擬及分析。</span><span class="sxs-lookup"><span data-stu-id="73c58-105">This article describes how hello information collected from hello new Microsoft Azure Billing APIs can be used in Cloud Cruiser for workflow cost simulation and analysis.</span></span>

## <a name="azure-ratecard-api"></a><span data-ttu-id="73c58-106">Azure RateCard API</span><span class="sxs-lookup"><span data-stu-id="73c58-106">Azure RateCard API</span></span>
<span data-ttu-id="73c58-107">Azure 中的 hello RateCard API 提供匯率資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-107">hello RateCard API provides rate information from Azure.</span></span> <span data-ttu-id="73c58-108">驗證具有 hello 適當認證之後，您可以查詢 hello 服務可供使用在 Azure 上，與您提供的識別碼。 相關聯的 hello 率的 hello API toocollect 中繼資料</span><span class="sxs-lookup"><span data-stu-id="73c58-108">After authenticating with hello proper credentials, you can query hello API toocollect metadata about hello services available on Azure, along with hello rates associated with your Offer ID.</span></span>

<span data-ttu-id="73c58-109">hello 下列是範例回應顯示 hello 價格 hello A0 (Windows) 的 hello API 從執行個體：</span><span class="sxs-lookup"><span data-stu-id="73c58-109">hello following is a sample response from hello API showing hello prices for hello A0 (Windows) instance:</span></span>

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a><span data-ttu-id="73c58-110">雲端 Cruiser 的介面 tooAzure RateCard 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="73c58-110">Cloud Cruiser’s Interface tooAzure RateCard API</span></span>
<span data-ttu-id="73c58-111">Cloud Cruiser 可以利用 hello RateCard API 資訊，以不同的方式。</span><span class="sxs-lookup"><span data-stu-id="73c58-111">Cloud Cruiser can leverage hello RateCard API information in different ways.</span></span> <span data-ttu-id="73c58-112">如本文中，我們將示範如何它可以是使用的 toomake IaaS 工作負載成本模擬及分析。</span><span class="sxs-lookup"><span data-stu-id="73c58-112">For this article, we will show how it can be used toomake IaaS workload cost simulation and analysis.</span></span>

<span data-ttu-id="73c58-113">toodemonstrate 這個使用案例，想像執行 Microsoft Azure Pack (WAP) 上的數個執行個體的工作負載。</span><span class="sxs-lookup"><span data-stu-id="73c58-113">toodemonstrate this use case, imagine a workload of several instances running on Microsoft Azure Pack (WAP).</span></span> <span data-ttu-id="73c58-114">hello 目標是 toosimulate 這個相同的工作負載在 Azure 和評估 hello 成本進行這類移轉。</span><span class="sxs-lookup"><span data-stu-id="73c58-114">hello goal is toosimulate this same workload on Azure, and estimate hello costs of doing such migration.</span></span> <span data-ttu-id="73c58-115">若要 toocreate 這個模擬，有兩個主要工作 toobe 執行：</span><span class="sxs-lookup"><span data-stu-id="73c58-115">In order toocreate this simulation, there are two main tasks toobe performed:</span></span>

1. <span data-ttu-id="73c58-116">**匯入和處理序 hello 服務所收集的資訊從 hello RateCard API。**</span><span class="sxs-lookup"><span data-stu-id="73c58-116">**Import and process hello service information collected from hello RateCard API.**</span></span> <span data-ttu-id="73c58-117">Hello 活頁簿，其中 hello 擷取從 hello RateCard API 是轉換後，已發行的 tooa 新費率計劃也會執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="73c58-117">This task is also performed on hello workbooks, where hello extract from hello RateCard API is transformed and published tooa new rate plan.</span></span> <span data-ttu-id="73c58-118">這個新費率方案將會用於 hello 模擬 tooestimate hello Azure 價格。</span><span class="sxs-lookup"><span data-stu-id="73c58-118">This new rate plan will be used on hello simulations tooestimate hello Azure prices.</span></span>
2. <span data-ttu-id="73c58-119">**標準化 WAP 服務和 IaaS 的 Azure 服務。**</span><span class="sxs-lookup"><span data-stu-id="73c58-119">**Normalize WAP services and Azure services for IaaS.**</span></span> <span data-ttu-id="73c58-120">根據預設，WAP 服務以個別資源 (CPU、記憶體大小、磁碟大小等) 為基礎，而 Azure 服務以執行個體大小 (A0、A1、A2 等等) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="73c58-120">By default, WAP services are based on individual resources (CPU, Memory Size, Disk Size, etc.) while Azure services are based on instance size (A0, A1, A2, etc.).</span></span> <span data-ttu-id="73c58-121">第一個工作可以 Cloud Cruiser ETL 引擎所執行，稱為活頁簿，其中配套這些資源，以執行個體大小，類似 tooAzure 執行個體的服務。</span><span class="sxs-lookup"><span data-stu-id="73c58-121">This first task can be performed by Cloud Cruiser’s ETL engine, called workbooks, where these resources can be bundled on instance sizes, analogous tooAzure instance services.</span></span>

### <a name="import-data-from-hello-ratecard-api"></a><span data-ttu-id="73c58-122">Hello RateCard API 從匯入資料</span><span class="sxs-lookup"><span data-stu-id="73c58-122">Import data from hello RateCard API</span></span>
<span data-ttu-id="73c58-123">Cloud Cruiser 活頁簿提供 hello RateCard API 從自動化的方式 toocollect 和程序資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-123">Cloud Cruiser workbooks provide an automated way toocollect and process information from hello RateCard API.</span></span>  <span data-ttu-id="73c58-124">ETL （擷取-轉換-載入） 活頁簿可讓您 tooconfigure hello 集合、 轉換及發佈至 hello Cloud Cruiser 資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-124">ETL (extract-transform-load) workbooks allow you tooconfigure hello collection, transformation, and publishing of data into hello Cloud Cruiser database.</span></span>

<span data-ttu-id="73c58-125">每個活頁簿可以有一個或多個集合，可讓您從不同來源 toocomplement toocorrelate 資訊，或增加 hello 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-125">Each workbook can have one or multiple collections, allowing you toocorrelate information from different sources toocomplement or augment hello usage data.</span></span> <span data-ttu-id="73c58-126">下列兩個螢幕擷取畫面顯示如何 hello toocreate 新*集合*中現有的活頁簿，並將資訊匯入 hello*集合*從 hello RateCard API:</span><span class="sxs-lookup"><span data-stu-id="73c58-126">hello following two screenshots show how toocreate a new *collection* in an existing workbook, and importing information into hello *collection* from hello RateCard API:</span></span>

<span data-ttu-id="73c58-127">![圖 1 - 建立新的集合][1]</span><span class="sxs-lookup"><span data-stu-id="73c58-127">![Figure 1 - Creating a new collection][1]</span></span>

<span data-ttu-id="73c58-128">![圖 2-從 hello 新集合的匯入資料][2]</span><span class="sxs-lookup"><span data-stu-id="73c58-128">![Figure 2 - Import data from hello new collection][2]</span></span>

<span data-ttu-id="73c58-129">Hello 資料匯入 hello 活頁簿，之後可能 toocreate 多個步驟與轉換程序、 toomodify 及模型 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-129">After importing hello data into hello workbook, it’s possible toocreate multiple steps and transformation processes, toomodify and model hello data.</span></span> <span data-ttu-id="73c58-130">針對此範例中，我們只感興趣基礎結構做為服務 (IaaS) hello 轉換步驟 tooremove 不必要資料列或記錄，我們可以使用，因為相關 tooservices IaaS 以外。</span><span class="sxs-lookup"><span data-stu-id="73c58-130">For this example, since we are only interested in infrastructure-as-a-Service (IaaS) we can use hello transformation steps tooremove unnecessary rows, or records, related tooservices other than IaaS.</span></span>

<span data-ttu-id="73c58-131">hello 下列螢幕擷取畫面顯示 hello 轉換步驟使用 tooprocess hello 資料收集從 RateCard API:</span><span class="sxs-lookup"><span data-stu-id="73c58-131">hello following screenshot shows hello transformation steps used tooprocess hello data collected from RateCard API:</span></span>

<span data-ttu-id="73c58-132">![圖 3-轉換步驟從 RateCard API tooprocess 收集資料][3]</span><span class="sxs-lookup"><span data-stu-id="73c58-132">![Figure 3 - Transformation steps tooprocess collected data from RateCard API][3]</span></span>

### <a name="defining-new-services-and-rate-plans"></a><span data-ttu-id="73c58-133">定義新的服務和費率方案</span><span class="sxs-lookup"><span data-stu-id="73c58-133">Defining New Services and Rate Plans</span></span>
<span data-ttu-id="73c58-134">Cloud Cruiser 上有不同的方式 toodefine 服務。</span><span class="sxs-lookup"><span data-stu-id="73c58-134">There are different ways toodefine services on Cloud Cruiser.</span></span> <span data-ttu-id="73c58-135">Hello 選項的其中一個是 tooimport hello 服務從 hello 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-135">One of hello options is tooimport hello services from hello usage data.</span></span> <span data-ttu-id="73c58-136">這個方法通常用於使用公用雲端中，其中 hello 服務已經定義 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="73c58-136">This method is commonly used when working with public clouds, where hello services are already defined by hello provider.</span></span>

<span data-ttu-id="73c58-137">費率方案是一組速度或價格，其可以是有效的日期或一群客戶，其他選項為基礎的套用的 toodifferent 服務。</span><span class="sxs-lookup"><span data-stu-id="73c58-137">A Rate Plan is a set of rates or prices that can be applied toodifferent services, based on effective dates, or group of customers, among other options.</span></span> <span data-ttu-id="73c58-138">速率計劃也可用在 Cloud Cruiser toocreate 模擬或 「 假設 」 狀況，toounderstand services 中的變更如何影響工作負載的 hello 總成本。</span><span class="sxs-lookup"><span data-stu-id="73c58-138">Rate Plans can also be used on Cloud Cruiser toocreate simulation or “What-if” scenarios, toounderstand how changes in services can affect hello total cost of a workload.</span></span>

<span data-ttu-id="73c58-139">在此範例中，我們將使用 Cloud Cruiser 中的 hello hello RateCard API toodefine 新服務的服務資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-139">In this example, we will use hello service information from hello RateCard API toodefine new services in Cloud Cruiser.</span></span> <span data-ttu-id="73c58-140">在 hello 相同方式，我們可以使用相關聯的 hello 率 toohello services toocreate 新費率方案 Cloud Cruiser 上。</span><span class="sxs-lookup"><span data-stu-id="73c58-140">In hello same way, we can use hello rates associated toohello services toocreate a new Rate Plan on Cloud Cruiser.</span></span>

<span data-ttu-id="73c58-141">在 hello hello 轉換程序結尾，它可能 toocreate 新增步驟，而且發行為新的服務和速率 hello hello RateCard API 的資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-141">At hello end of hello transformation process, it is possible toocreate a new step and publish hello data from hello RateCard API as new services and rates.</span></span>

<span data-ttu-id="73c58-142">![圖 4： 將資料從 hello RateCard API 中的 hello 發行為新的服務和速率][4]</span><span class="sxs-lookup"><span data-stu-id="73c58-142">![Figure 4 - Publishing hello data from hello RateCard API as new Services and Rates][4]</span></span>

### <a name="verify-azure-services-and-rates"></a><span data-ttu-id="73c58-143">確認 Azure 服務和費率</span><span class="sxs-lookup"><span data-stu-id="73c58-143">Verify Azure Services and Rates</span></span>
<span data-ttu-id="73c58-144">發行之後 hello 服務和速度，您可以確認 hello 匯入中的服務清單 Cloud Cruiser*服務* 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="73c58-144">After publishing hello services and rates, you can verify hello list of imported services in Cloud Cruiser’s *Services* tab:</span></span>

<span data-ttu-id="73c58-145">![圖 5-正在驗證 hello 新服務][5]</span><span class="sxs-lookup"><span data-stu-id="73c58-145">![Figure 5 - Verifying hello new Services][5]</span></span>

<span data-ttu-id="73c58-146">在 hello*速率計劃*索引標籤上，您可以檢查 hello 稱為 「 AzureSimulation"hello 傳輸率 hello RateCard API 從匯入新費率方案。</span><span class="sxs-lookup"><span data-stu-id="73c58-146">On hello *Rate Plans* tab, you can check hello new rate plan called “AzureSimulation” with hello rates imported from hello RateCard API.</span></span>

<span data-ttu-id="73c58-147">![圖 6-正在驗證 hello 新費率方案和相關聯的速率][6]</span><span class="sxs-lookup"><span data-stu-id="73c58-147">![Figure 6 - Verifying hello new Rate Plan and associated rates][6]</span></span>

### <a name="normalize-wap-and-azure-services"></a><span data-ttu-id="73c58-148">標準化 WAP 和 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="73c58-148">Normalize WAP and Azure Services</span></span>
<span data-ttu-id="73c58-149">根據預設，WAP 會提供根據 hello 使用的運算、 記憶體和網路資源的使用方式資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-149">By default, WAP provides usage information based on hello use of compute, memory, and network resources.</span></span> <span data-ttu-id="73c58-150">Cloud Cruiser 中，您可以定義您的基礎服務直接依據 hello 配置或計量付費的這些資源的使用方式。</span><span class="sxs-lookup"><span data-stu-id="73c58-150">In Cloud Cruiser, you can define your services based directly on hello allocation or metered usage of these resources.</span></span> <span data-ttu-id="73c58-151">比方說，您可以設定每小時的 CPU 使用量或免費 hello GB 的記憶體配置 tooan 執行個體的基本的速率。</span><span class="sxs-lookup"><span data-stu-id="73c58-151">For example, you can set a basic rate for each hour of CPU usage, or charge hello GB of memory allocated tooan instance.</span></span>

<span data-ttu-id="73c58-152">WAP 和 Azure 之間的順序 toocompare 成本的這個範例中，我們需要 tooaggregate hello 的資源使用量 WAP 為組合，然後再將其對應的 tooAzure 服務。</span><span class="sxs-lookup"><span data-stu-id="73c58-152">For this example, in order toocompare costs between WAP and Azure, we need tooaggregate hello resource usage on WAP into bundles, which can then be mapped tooAzure services.</span></span> <span data-ttu-id="73c58-153">此轉換可以輕鬆地實作 hello 活頁簿中：</span><span class="sxs-lookup"><span data-stu-id="73c58-153">This transformation can be implemented easily in hello workbooks:</span></span>

<span data-ttu-id="73c58-154">![圖 7： 轉換 WAP 資料 toonormalize 服務][7]</span><span class="sxs-lookup"><span data-stu-id="73c58-154">![Figure 7 - Transforming WAP data toonormalize services][7]</span></span>

<span data-ttu-id="73c58-155">在 hello 活頁簿的 hello 最後一個步驟是 toopublish hello hello Cloud Cruiser 資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-155">hello last step at hello workbook is toopublish hello data into hello Cloud Cruiser database.</span></span> <span data-ttu-id="73c58-156">在此步驟中，hello 使用量資料現在會搭配服務 （的對應 toohello Azure 服務），並繫結 toodefault 率 toocreate hello 費用。</span><span class="sxs-lookup"><span data-stu-id="73c58-156">During this step, hello usage data is now bundled into services (that map toohello Azure Services) and tied toodefault rates toocreate hello charges.</span></span>

<span data-ttu-id="73c58-157">分頁裝訂 hello 活頁簿之後, 您可以自動化 hello 排程器上新增一項工作，並指定 hello 頻率和時間 hello 活頁簿 toorun hello hello 資料處理。</span><span class="sxs-lookup"><span data-stu-id="73c58-157">After finishing hello workbook, you can automate hello processing of hello data, by adding a task on hello scheduler and specifying hello frequency and time for hello workbook toorun.</span></span>

<span data-ttu-id="73c58-158">![圖 8 - 活頁簿排程][8]</span><span class="sxs-lookup"><span data-stu-id="73c58-158">![Figure 8 - Workbook scheduling][8]</span></span>

### <a name="create-reports-for-workload-cost-simulation-analysis"></a><span data-ttu-id="73c58-159">建立工作負載成本模擬分析的報告</span><span class="sxs-lookup"><span data-stu-id="73c58-159">Create Reports for Workload Cost Simulation Analysis</span></span>
<span data-ttu-id="73c58-160">Hello 使用量收集和費用會載入至 hello Cloud Cruiser 資料庫之後，我們可以利用 hello Cloud Cruiser Insights 模組 toocreate hello 工作負載成本模擬我們需要的。</span><span class="sxs-lookup"><span data-stu-id="73c58-160">After hello usage is collected and charges are loaded into hello Cloud Cruiser database, we can leverage hello Cloud Cruiser Insights module toocreate hello workload cost simulation that we desire.</span></span>

<span data-ttu-id="73c58-161">在訂單 toodemonstrate 此案例中，我們建立 hello 下列報表：</span><span class="sxs-lookup"><span data-stu-id="73c58-161">In order toodemonstrate this scenario, we created hello following report:</span></span>

<span data-ttu-id="73c58-162">![成本比較][9]</span><span class="sxs-lookup"><span data-stu-id="73c58-162">![Cost Comparison][9]</span></span>

<span data-ttu-id="73c58-163">hello 上圖形會顯示成本比較所比較 hello 價格 WAP （深藍色） 和 Azure （淺藍色） 之間的每個特定服務執行中 hello 工作負載的服務。</span><span class="sxs-lookup"><span data-stu-id="73c58-163">hello top graph shows a cost comparison by services, comparing hello price of running hello workload for each specific service between WAP (dark blue) and Azure (light blue).</span></span>

<span data-ttu-id="73c58-164">hello 下方圖表會顯示 hello 相同的資料，但依部門細分。</span><span class="sxs-lookup"><span data-stu-id="73c58-164">hello bottom graph shows hello same data but broken down by department.</span></span> <span data-ttu-id="73c58-165">這會顯示每個部門 toorun hello 成本其工作負載上 WAP 和 Azure，以及它們在 hello 節省列 （綠色） 之間的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="73c58-165">This shows hello costs for each department toorun their workload on WAP and Azure, along with hello difference between them in hello Savings bar (green).</span></span>

## <a name="azure-usage-api"></a><span data-ttu-id="73c58-166">Azure 使用情況 API</span><span class="sxs-lookup"><span data-stu-id="73c58-166">Azure Usage API</span></span>
### <a name="introduction"></a><span data-ttu-id="73c58-167">簡介</span><span class="sxs-lookup"><span data-stu-id="73c58-167">Introduction</span></span>
<span data-ttu-id="73c58-168">Microsoft 最近引進 hello Azure 使用量 API，允許訂閱者 tooprogrammatically 提取中使用量資料 toogain 深入了解依據耗用量。</span><span class="sxs-lookup"><span data-stu-id="73c58-168">Microsoft recently introduced hello Azure Usage API, allowing subscribers tooprogrammatically pull in usage data toogain insights into their consumption.</span></span> <span data-ttu-id="73c58-169">這是最棒的工具，可以利用 hello 更豐富資料集可透過此 API 的 Cloud Cruiser 客戶。</span><span class="sxs-lookup"><span data-stu-id="73c58-169">This is great news for Cloud Cruiser customers that can take advantage of hello richer dataset available through this API.</span></span>

<span data-ttu-id="73c58-170">Cloud Cruiser 可以利用 hello 整合，以數種方式的 hello 使用量 API。</span><span class="sxs-lookup"><span data-stu-id="73c58-170">Cloud Cruiser can leverage hello integration with hello Usage API in several ways.</span></span> <span data-ttu-id="73c58-171">hello 資料粒度 （每小時的使用量資訊） 和資源的中繼資料資訊可透過 API 提供的 hello hello 必要的資料集 toosupport 彈性回報或計費模型。</span><span class="sxs-lookup"><span data-stu-id="73c58-171">hello granularity (hourly usage information) and resource metadata information available through hello API provides hello necessary dataset toosupport flexible Showback or Chargeback models.</span></span> 

<span data-ttu-id="73c58-172">在此教學課程中，我們將提供如何 Cloud Cruiser 可受益於 hello 使用量 API 資訊的其中一個範例。</span><span class="sxs-lookup"><span data-stu-id="73c58-172">In this tutorial, we will present one example of how Cloud Cruiser can benefit from hello Usage API information.</span></span> <span data-ttu-id="73c58-173">更具體來說，我們將會在 Azure 上建立的資源群組、 關聯標記 hello 帳戶結構，然後說明提取和處理 hello 標記資訊到 Cloud Cruiser hello 程序。</span><span class="sxs-lookup"><span data-stu-id="73c58-173">More specifically, we will create a Resource Group on Azure, associate tags for hello account structure, then describe hello process of pulling and processing hello tag information into Cloud Cruiser.</span></span>

<span data-ttu-id="73c58-174">hello 最後的目標是 toobe 無法 toocreate 報表喜歡 hello 下列其中一個，而且無法 tooanalyze 成本及填入 hello 標記 hello 帳戶結構為基礎的耗用量。</span><span class="sxs-lookup"><span data-stu-id="73c58-174">hello final goal is toobe able toocreate reports like hello following one, and be able tooanalyze cost and consumption based on hello account structure populated by hello tags.</span></span>

<span data-ttu-id="73c58-175">![圖 10 - 含有使用標記之細項的報告][10]</span><span class="sxs-lookup"><span data-stu-id="73c58-175">![Figure 10 - Report with breakdowns using tags][10]</span></span>

### <a name="microsoft-azure-tags"></a><span data-ttu-id="73c58-176">Microsoft Azure 標記</span><span class="sxs-lookup"><span data-stu-id="73c58-176">Microsoft Azure Tags</span></span>
<span data-ttu-id="73c58-177">hello 資料可透過 hello Azure 使用量 API 不僅耗用量資訊包含同時也包含資源的中繼資料包含任何與其相關聯的標記。</span><span class="sxs-lookup"><span data-stu-id="73c58-177">hello data available through hello Azure Usage API includes not only consumption information, but also resource metadata including any tags associated with it.</span></span> <span data-ttu-id="73c58-178">標記提供簡單的方式 tooorganize 您的資源，但在順序 toobe 有效，您需要 tooensure 的：</span><span class="sxs-lookup"><span data-stu-id="73c58-178">Tags provide an easy way tooorganize your resources, but in order toobe effective, you need tooensure that:</span></span>

* <span data-ttu-id="73c58-179">標籤是正確套用的 toohello 資源在佈建階段</span><span class="sxs-lookup"><span data-stu-id="73c58-179">Tags are correctly applied toohello resources at provision time</span></span>
* <span data-ttu-id="73c58-180">標記會適當地用於 hello 回報/計費程序 tootie hello 使用量 toohello 組織的帳戶結構。</span><span class="sxs-lookup"><span data-stu-id="73c58-180">Tags are properly used on hello Showback/Chargeback process tootie hello usage toohello organization’s account structure.</span></span>

<span data-ttu-id="73c58-181">兩個需求可以是具挑戰性，特別是當 hello 佈建或充電側邊的手動程序。</span><span class="sxs-lookup"><span data-stu-id="73c58-181">Both of these requirements can be challenging, especially when there is a manual process on hello provision or charging side.</span></span> <span data-ttu-id="73c58-182">輸入錯誤、 不正確或遺失甚至標記時使用標籤及這些錯誤可以讓生活 hello 充電側邊很難上常見的抱怨客戶。</span><span class="sxs-lookup"><span data-stu-id="73c58-182">Mistyped, incorrect or even missing tags are common complaints from customers when using tags and these errors can make life on hello charging side very difficult.</span></span>

<span data-ttu-id="73c58-183">Hello 與新的 Azure 使用量 API、 Cloud Cruiser 可以提取資源標記的詳細資訊，，和透過複雜的 ETL 工具呼叫活頁簿，請修正這些常見的標記錯誤。</span><span class="sxs-lookup"><span data-stu-id="73c58-183">With hello new Azure Usage API, Cloud Cruiser can pull resource tagging information, and through a sophisticated ETL tool called workbooks, fix these common tagging errors.</span></span> <span data-ttu-id="73c58-184">透過使用規則運算式和資料相互關聯的轉換，Cloud Cruiser 可以識別不正確地加上標記的資源標記，然後將 hello 正確，確保 hello 正確關聯的 hello 資源 hello 取用者。</span><span class="sxs-lookup"><span data-stu-id="73c58-184">Through transformation using regular expressions and data correlation, Cloud Cruiser can identify incorrectly tagged resources and apply hello correct tags, ensuring hello correct association of hello resources with hello consumer.</span></span>

<span data-ttu-id="73c58-185">Hello 充電側邊，在 Cloud Cruiser hello 回報/計費程序，會自動執行，可以利用 hello 標記資訊 tootie hello 使用量 toohello 適當取用者 （部門、 部門、 專案等等）。</span><span class="sxs-lookup"><span data-stu-id="73c58-185">On hello charging side, Cloud Cruiser automates hello Showback/Chargeback process, and can leverage hello tag information tootie hello usage toohello appropriate consumer (Department, Division, Project, etc.).</span></span> <span data-ttu-id="73c58-186">這項自動化作業提供非常重大的改進，並且可以確保一致且可稽核的收費程序。</span><span class="sxs-lookup"><span data-stu-id="73c58-186">This automation provides a huge improvement and can ensure a consistent and auditable charging process.</span></span>

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a><span data-ttu-id="73c58-187">使用 Microsoft Azure 上的標記建立資源群組</span><span class="sxs-lookup"><span data-stu-id="73c58-187">Creating a Resource Group with tags on Microsoft Azure</span></span>
<span data-ttu-id="73c58-188">hello 在本教學課程的第一個步驟是 toocreate hello Azure 入口網站中的資源群組，然後建立新標記 tooassociate toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="73c58-188">hello first step in this tutorial is toocreate a Resource Group in hello Azure portal, then create new tags tooassociate toohello resources.</span></span> <span data-ttu-id="73c58-189">此範例中，我們將建立下列標記的 hello： 部門，環境中，擁有者，專案。</span><span class="sxs-lookup"><span data-stu-id="73c58-189">For this example, we will be creating hello following tags: Department, Environment, Owner, Project.</span></span>

<span data-ttu-id="73c58-190">hello 以下螢幕擷取畫面會顯示以 hello 的資源群組相關聯的標記範例。</span><span class="sxs-lookup"><span data-stu-id="73c58-190">hello screenshot below shows a sample Resource Group with hello associated tags.</span></span>

<span data-ttu-id="73c58-191">![圖 11 - 在 Azure 入口網站上具有相關標記的資源群組][11]</span><span class="sxs-lookup"><span data-stu-id="73c58-191">![Figure 11 - Resource Group with associated tags on Azure portal][11]</span></span>

<span data-ttu-id="73c58-192">hello 下一個步驟是 toopull hello 資訊 hello 使用量 API Cloud Cruiser 到。</span><span class="sxs-lookup"><span data-stu-id="73c58-192">hello next step is toopull hello information from hello Usage API into Cloud Cruiser.</span></span> <span data-ttu-id="73c58-193">hello 使用量 API 目前會提供以 JSON 格式的回應。</span><span class="sxs-lookup"><span data-stu-id="73c58-193">hello Usage API currently provides responses in JSON format.</span></span> <span data-ttu-id="73c58-194">Hello 擷取的資料的範例如下：</span><span class="sxs-lookup"><span data-stu-id="73c58-194">Here is a sample of hello data retrieved:</span></span>

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a><span data-ttu-id="73c58-195">將資料匯入從 hello 使用量 API Cloud Cruiser</span><span class="sxs-lookup"><span data-stu-id="73c58-195">Import data from hello Usage API into Cloud Cruiser</span></span>
<span data-ttu-id="73c58-196">Cloud Cruiser 活頁簿提供 hello 使用量 API 從自動化的方式 toocollect 和程序資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-196">Cloud Cruiser workbooks provide an automated way toocollect and process information from hello Usage API.</span></span> <span data-ttu-id="73c58-197">ETL （擷取-轉換-載入） 活頁簿可讓您 tooconfigure hello 集合、 轉換及發佈至 hello Cloud Cruiser 資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-197">An ETL (extract-transform-load) workbook allows you tooconfigure hello collection, transformation, and publishing of data into hello Cloud Cruiser database.</span></span>

<span data-ttu-id="73c58-198">每個活頁簿可以有一個或多個集合。</span><span class="sxs-lookup"><span data-stu-id="73c58-198">Each workbook can have one or multiple collections.</span></span> <span data-ttu-id="73c58-199">這可讓您從不同來源 toocomplement 或強化 hello 使用量資料 toocorrelate 資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-199">This allows you toocorrelate information from different sources toocomplement or augment hello usage data.</span></span> <span data-ttu-id="73c58-200">此範例中，我們將建立新的工作表 hello Azure 範本活頁簿中 (*UsageAPI)*並設定新*集合*tooimport 從 hello 使用量 API 的資訊。</span><span class="sxs-lookup"><span data-stu-id="73c58-200">For this example, we will create a new sheet in hello Azure template workbook (*UsageAPI)* and set a new *collection* tooimport information from hello Usage API.</span></span>

<span data-ttu-id="73c58-201">![圖 3: hello UsageAPI 工作表中的匯入的應用程式開發介面使用方式資料][12]</span><span class="sxs-lookup"><span data-stu-id="73c58-201">![Figure 3 - Usage API data imported into hello UsageAPI sheet][12]</span></span>

<span data-ttu-id="73c58-202">請注意，此活頁簿已有其他表 tooimport 服務從 Azure (*ImportServices*)，並處理從 hello 計費 API hello 耗用量資訊 (*PublishData*)。</span><span class="sxs-lookup"><span data-stu-id="73c58-202">Notice that this workbook already has other sheets tooimport services from Azure (*ImportServices*), and process hello consumption information from hello Billing API (*PublishData*).</span></span>

<span data-ttu-id="73c58-203">接下來，我們將使用 hello 使用量 API toopopulate hello *UsageAPI*工作表和相互關聯的 hello 資訊與 hello 耗用量 hello 計費 API 上 hello *PublishData*工作表。</span><span class="sxs-lookup"><span data-stu-id="73c58-203">Next we will use hello Usage API toopopulate hello *UsageAPI* sheet, and correlate hello information with hello consumption data from hello Billing API on hello *PublishData* sheet.</span></span>

### <a name="processing-hello-tag-information-from-hello-usage-api"></a><span data-ttu-id="73c58-204">處理 hello 標記資訊從 hello 使用量 API</span><span class="sxs-lookup"><span data-stu-id="73c58-204">Processing hello tag information from hello Usage API</span></span>
<span data-ttu-id="73c58-205">Hello 資料匯入 hello 活頁簿之後, 我們將建立轉換步驟，在 hello *UsageAPI* hello API 從訂單 tooprocess hello 資訊工作表。</span><span class="sxs-lookup"><span data-stu-id="73c58-205">After importing hello data into hello workbook, we will create transformation steps in hello *UsageAPI* sheet in order tooprocess hello information from hello API.</span></span> <span data-ttu-id="73c58-206">第一個步驟是的 toouse 「 JSON 分割 」 的處理器 tooextract hello 標記從單一欄位，然後建立它們 （部門、 專案、 擁有者，以及環境） 的每一個欄位。</span><span class="sxs-lookup"><span data-stu-id="73c58-206">First step is toouse a “JSON split” processor tooextract hello tags from a single field, then create fields for each one of them (Department, Project, Owner, and Environment).</span></span>

<span data-ttu-id="73c58-207">![圖 4-建立新的欄位，如 hello 標記資訊][13]</span><span class="sxs-lookup"><span data-stu-id="73c58-207">![Figure 4 - Create new fields for hello tag information][13]</span></span>

<span data-ttu-id="73c58-208">遺漏 hello 標記資訊 （黃色方塊），請注意 hello 「 網路功能 」 服務。 但我們可以確認它是否 hello 屬於相同的資源群組，藉由查看 hello *ResourceGroupName*欄位。</span><span class="sxs-lookup"><span data-stu-id="73c58-208">Notice hello “Networking” service is missing hello tag information (yellow box), but we can verify that it is part of hello same Resource Group by looking at hello *ResourceGroupName* field.</span></span> <span data-ttu-id="73c58-209">由於我們有 hello 的 hello 標記此資源群組的其他資源，我們可以使用此資訊 tooapply hello 遺漏標記 toothis 資源稍後在 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="73c58-209">Since we have hello tags for hello other resources from this Resource Group, we can use this information tooapply hello missing tags toothis resource later in hello process.</span></span>

<span data-ttu-id="73c58-210">hello 下一個步驟是 toocreate 查閱資料表產生關聯 hello 資訊從 hello 標記 toohello *ResourceGroupName*。</span><span class="sxs-lookup"><span data-stu-id="73c58-210">hello next step is toocreate a lookup table associating hello information from hello tags toohello *ResourceGroupName*.</span></span> <span data-ttu-id="73c58-211">Hello 下一個步驟 tooenrich hello 消耗資料，以標記資訊將使用此查閱資料表。</span><span class="sxs-lookup"><span data-stu-id="73c58-211">This lookup table will be used on hello next step tooenrich hello consumption data with tag information.</span></span>

### <a name="adding-hello-tag-information-toohello-consumption-data"></a><span data-ttu-id="73c58-212">加入 hello 標記資訊 toohello 耗用量資料</span><span class="sxs-lookup"><span data-stu-id="73c58-212">Adding hello tag information toohello consumption data</span></span>
<span data-ttu-id="73c58-213">現在我們可以跳 toohello *PublishData*工作表中，哪些處理程序 hello 耗用量資訊從 hello 計費應用程式開發介面，並加入 hello 與 hello 標記擷取的欄位。</span><span class="sxs-lookup"><span data-stu-id="73c58-213">Now we can jump toohello *PublishData* sheet, which processes hello consumption information from hello Billing API, and add hello fields extracted from hello tags.</span></span> <span data-ttu-id="73c58-214">藉由查看 hello hello 先前步驟中，使用 hello 上建立的查閱資料表執行此程序*ResourceGroupName* hello hello 查閱的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="73c58-214">This process is performed by looking at hello lookup table created on hello previous step, using hello *ResourceGroupName* as hello key for hello lookups.</span></span>

<span data-ttu-id="73c58-215">![圖 5-填入 hello 帳戶結構的 hello 查閱的 hello 資訊][14]</span><span class="sxs-lookup"><span data-stu-id="73c58-215">![Figure 5 - Populating hello account structure with hello information from hello lookups][14]</span></span>

<span data-ttu-id="73c58-216">請注意 hello 「 網路功能 」 服務的 hello 適當的帳戶結構欄位已套用的以 hello 遺漏標記修正 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="73c58-216">Notice that hello appropriate account structure fields for hello “Networking” service were applied, fixing hello issue with hello missing tags.</span></span> <span data-ttu-id="73c58-217">我們也擴展 hello 帳戶結構欄位資源我們的目標資源群組具有 「 其他 」 以外，在訂單 toodifferentiate hello 上進行報告。</span><span class="sxs-lookup"><span data-stu-id="73c58-217">We also populated hello account structure fields for resources other than our target Resource Group with “Other”, in order toodifferentiate them on hello reports.</span></span>

<span data-ttu-id="73c58-218">現在我們只需要 tooadd 步驟 toopublish hello 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="73c58-218">Now we just need tooadd a step toopublish hello usage data.</span></span> <span data-ttu-id="73c58-219">在此步驟中，我們費率方案上定義的每個服務的 hello 適當速度將會套用的 toohello 使用量資訊，與 hello 載入 hello 資料庫產生的費用。</span><span class="sxs-lookup"><span data-stu-id="73c58-219">During this step, hello appropriate rates for each service defined on our Rate Plan will be applied toohello usage information, with hello resulting charge loaded into hello database.</span></span>

<span data-ttu-id="73c58-220">hello 棒的是您只需要執行此程序 toogo 一次。</span><span class="sxs-lookup"><span data-stu-id="73c58-220">hello best part is that you only have toogo through this process once.</span></span> <span data-ttu-id="73c58-221">當完成 hello 活頁簿時，您只需要 tooadd 它 toohello 排程器，它會執行每小時或每天在 hello 排定的時間。</span><span class="sxs-lookup"><span data-stu-id="73c58-221">When hello workbook is completed, you just need tooadd it toohello scheduler and it will run hourly or daily at hello scheduled time.</span></span> <span data-ttu-id="73c58-222">然後它便只需建立新的報表，或自訂現有的順序 tooanalyze hello 資料 tooget 意義 insights 從您雲端的使用量。</span><span class="sxs-lookup"><span data-stu-id="73c58-222">Then it’s just a matter of creating new reports, or customizing existing ones, in order tooanalyze hello data tooget meaningful insights from your cloud usage.</span></span>

### <a name="next-steps"></a><span data-ttu-id="73c58-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73c58-223">Next Steps</span></span>
* <span data-ttu-id="73c58-224">如需建立 Cloud Cruiser 活頁簿和報表，詳細的指示，請參閱 tooCloud Cruiser 的線上[文件](http://docs.cloudcruiser.com/)（所需的有效登入）。</span><span class="sxs-lookup"><span data-stu-id="73c58-224">For detailed instructions on creating Cloud Cruiser workbooks and reports, please refer tooCloud Cruiser’s online [documentation](http://docs.cloudcruiser.com/) (valid login required).</span></span>  <span data-ttu-id="73c58-225">如需有關 Cloud Cruiser 的詳細資訊，請連絡 [info@cloudcruiser.com](mailto:info@cloudcruiser.com)。</span><span class="sxs-lookup"><span data-stu-id="73c58-225">For more information about Cloud Cruiser, please contact [info@cloudcruiser.com](mailto:info@cloudcruiser.com).</span></span>
* <span data-ttu-id="73c58-226">請參閱[深入了解您的 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md)hello Azure 資源使用量和 RateCard Api 的概觀。</span><span class="sxs-lookup"><span data-stu-id="73c58-226">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of hello Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="73c58-227">簽出 hello [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)如需有關這兩個 Api 的詳細資訊，這是 hello 組 hello Azure 資源管理員所提供的應用程式開發介面的一部分。</span><span class="sxs-lookup"><span data-stu-id="73c58-227">Check out hello [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of hello set of APIs provided by hello Azure Resource Manager.</span></span>
* <span data-ttu-id="73c58-228">如果您想要 toodive 右到 hello 範例程式碼，請參閱 Microsoft Azure 計費應用程式開發介面程式碼範例上[Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?term=billing)。</span><span class="sxs-lookup"><span data-stu-id="73c58-228">If you would like toodive right into hello sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

### <a name="learn-more"></a><span data-ttu-id="73c58-229">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="73c58-229">Learn More</span></span>
* <span data-ttu-id="73c58-230">請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)文章 toolearn 更多關於 hello Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="73c58-230">See hello [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article toolearn more about hello Azure Resource Manager.</span></span>

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "圖 1 - 建立新的集合"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "圖 2-從 hello 新集合的匯入資料"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "圖 3-轉換步驟從 RateCard API tooprocess 收集資料"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "圖 4： 將資料從 hello RateCard API 中的 hello 發行為新的服務和速率"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "圖 5-正在驗證 hello 新服務"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "圖 6-正在驗證 hello 新費率方案和相關聯的速率"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "圖 7： 轉換 WAP 資料 toonormalize 服務"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "圖 8 - 活頁簿排程"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "圖 9: hello 工作負載成本比較案例的範例報表"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "圖 10 - 含有使用標記之細項的報告"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "圖 11 - 在 Azure 入口網站上具有相關標記的資源群組"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "圖 12: hello UsageAPI 工作表中的匯入的應用程式開發介面使用方式資料"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "圖 13： 建立新的欄位，如 hello 標記資訊"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "圖 14-填入 hello 帳戶結構的 hello 查閱的 hello 資訊"
