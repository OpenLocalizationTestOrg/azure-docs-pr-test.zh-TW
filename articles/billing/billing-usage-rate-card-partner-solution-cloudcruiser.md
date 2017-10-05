---
title: "Cloud Cruiser 和 Microsoft Azure 計費 API 整合 | Microsoft Docs"
description: "提供 Microsoft Azure 計費合作夥伴 Cloud Cruiser 將 Azure 計費 API 整合至其產品的經驗所得來的獨特觀點。  這特別適用於有興趣使用/嘗試將 Cloud Cruiser 用於 Microsoft Azure Pack 的客戶。"
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
ms.openlocfilehash: a05fe5e610f1f0ce216a4b84bf2873b0d081875d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a><span data-ttu-id="308c6-104">Cloud Cruiser 和 Microsoft Azure 計費 API 整合</span><span class="sxs-lookup"><span data-stu-id="308c6-104">Cloud Cruiser and Microsoft Azure Billing API Integration</span></span>
<span data-ttu-id="308c6-105">本文描述從新的 Microsoft Azure 計費 API 所收集來的資訊如何用來在 Cloud Cruiser 中進行工作流程成本模擬與分析。</span><span class="sxs-lookup"><span data-stu-id="308c6-105">This article describes how the information collected from the new Microsoft Azure Billing APIs can be used in Cloud Cruiser for workflow cost simulation and analysis.</span></span>

## <a name="azure-ratecard-api"></a><span data-ttu-id="308c6-106">Azure RateCard API</span><span class="sxs-lookup"><span data-stu-id="308c6-106">Azure RateCard API</span></span>
<span data-ttu-id="308c6-107">RateCard API 提供來自 Azure 的費率資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-107">The RateCard API provides rate information from Azure.</span></span> <span data-ttu-id="308c6-108">以適當的認證進行驗證之後，您可以查詢 API 以收集 Azure 上可用服務的中繼資料，以及與優惠識別碼相關聯的費率。</span><span class="sxs-lookup"><span data-stu-id="308c6-108">After authenticating with the proper credentials, you can query the API to collect metadata about the services available on Azure, along with the rates associated with your Offer ID.</span></span>

<span data-ttu-id="308c6-109">以下是來自 API 的範例回應，顯示 A0 (Windows) 執行個體的價格：</span><span class="sxs-lookup"><span data-stu-id="308c6-109">The following is a sample response from the API showing the prices for the A0 (Windows) instance:</span></span>

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

### <a name="cloud-cruisers-interface-to-azure-ratecard-api"></a><span data-ttu-id="308c6-110">Azure RateCard API 的 Cloud Cruiser 介面</span><span class="sxs-lookup"><span data-stu-id="308c6-110">Cloud Cruiser’s Interface to Azure RateCard API</span></span>
<span data-ttu-id="308c6-111">Cloud Cruiser 可以用不同的方式運用 RateCard API 資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-111">Cloud Cruiser can leverage the RateCard API information in different ways.</span></span> <span data-ttu-id="308c6-112">在這篇文章中，我們將說明如何使用它進行 IaaS 工作負載成本模擬及分析。</span><span class="sxs-lookup"><span data-stu-id="308c6-112">For this article, we will show how it can be used to make IaaS workload cost simulation and analysis.</span></span>

<span data-ttu-id="308c6-113">為了示範這個使用案例，請想像執行於 Microsoft Azure Pack (WAP) 之數個執行個體的工作負載。</span><span class="sxs-lookup"><span data-stu-id="308c6-113">To demonstrate this use case, imagine a workload of several instances running on Microsoft Azure Pack (WAP).</span></span> <span data-ttu-id="308c6-114">目標是要在 Azure 上模擬相同的工作負載，並評估這類移轉的成本。</span><span class="sxs-lookup"><span data-stu-id="308c6-114">The goal is to simulate this same workload on Azure, and estimate the costs of doing such migration.</span></span> <span data-ttu-id="308c6-115">若要建立這個模擬，有兩個主要的工作要執行：</span><span class="sxs-lookup"><span data-stu-id="308c6-115">In order to create this simulation, there are two main tasks to be performed:</span></span>

1. <span data-ttu-id="308c6-116">**匯入和處理從 RateCard API 收集的服務資訊。**</span><span class="sxs-lookup"><span data-stu-id="308c6-116">**Import and process the service information collected from the RateCard API.**</span></span> <span data-ttu-id="308c6-117">這項工作也會在活頁簿上執行，其中從 RateCard API 擷取的內容會轉換並發佈為新的費率方案。</span><span class="sxs-lookup"><span data-stu-id="308c6-117">This task is also performed on the workbooks, where the extract from the RateCard API is transformed and published to a new rate plan.</span></span> <span data-ttu-id="308c6-118">新的費率方案將在模擬中用來評估 Azure 價格。</span><span class="sxs-lookup"><span data-stu-id="308c6-118">This new rate plan will be used on the simulations to estimate the Azure prices.</span></span>
2. <span data-ttu-id="308c6-119">**標準化 WAP 服務和 IaaS 的 Azure 服務。**</span><span class="sxs-lookup"><span data-stu-id="308c6-119">**Normalize WAP services and Azure services for IaaS.**</span></span> <span data-ttu-id="308c6-120">根據預設，WAP 服務以個別資源 (CPU、記憶體大小、磁碟大小等) 為基礎，而 Azure 服務以執行個體大小 (A0、A1、A2 等等) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="308c6-120">By default, WAP services are based on individual resources (CPU, Memory Size, Disk Size, etc.) while Azure services are based on instance size (A0, A1, A2, etc.).</span></span> <span data-ttu-id="308c6-121">第一個工作可以由 Cloud Cruiser 的 ETL 引擎執行，稱為活頁簿，其中資源整合為執行個體大小，類似 Azure 執行個體服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-121">This first task can be performed by Cloud Cruiser’s ETL engine, called workbooks, where these resources can be bundled on instance sizes, analogous to Azure instance services.</span></span>

### <a name="import-data-from-the-ratecard-api"></a><span data-ttu-id="308c6-122">從 RateCard API 匯入資料</span><span class="sxs-lookup"><span data-stu-id="308c6-122">Import data from the RateCard API</span></span>
<span data-ttu-id="308c6-123">Cloud Cruiser 活頁簿提供自動化的方式收集和處理來自 RateCard API 的資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-123">Cloud Cruiser workbooks provide an automated way to collect and process information from the RateCard API.</span></span>  <span data-ttu-id="308c6-124">ETL (擷取-轉換-載入) 活頁簿可讓您設定資料的集合、轉換和發佈至 Cloud Cruiser 資料庫。</span><span class="sxs-lookup"><span data-stu-id="308c6-124">ETL (extract-transform-load) workbooks allow you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span></span>

<span data-ttu-id="308c6-125">每個活頁簿可以有一個或多個集合，讓您將來自不同資源的資訊相互關聯，以補充或強化使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="308c6-125">Each workbook can have one or multiple collections, allowing you to correlate information from different sources to complement or augment the usage data.</span></span> <span data-ttu-id="308c6-126">以下兩個螢幕擷取畫面顯示如何在現有活頁簿中建立新的「集合」，並將資訊從 RateCard API 匯入到「集合」：</span><span class="sxs-lookup"><span data-stu-id="308c6-126">The following two screenshots show how to create a new *collection* in an existing workbook, and importing information into the *collection* from the RateCard API:</span></span>

<span data-ttu-id="308c6-127">![圖 1 - 建立新的集合][1]</span><span class="sxs-lookup"><span data-stu-id="308c6-127">![Figure 1 - Creating a new collection][1]</span></span>

<span data-ttu-id="308c6-128">![圖 2 - 從新集合匯入資料][2]</span><span class="sxs-lookup"><span data-stu-id="308c6-128">![Figure 2 - Import data from the new collection][2]</span></span>

<span data-ttu-id="308c6-129">將資料匯入活頁簿之後，就可以建立多個步驟及轉換程序，以修改資料與建立資料模型。</span><span class="sxs-lookup"><span data-stu-id="308c6-129">After importing the data into the workbook, it’s possible to create multiple steps and transformation processes, to modify and model the data.</span></span> <span data-ttu-id="308c6-130">以這個範例而言，因為我們只對基礎結構即為服務 (IaaS) 感興趣，所以我們可以使用轉換步驟移除不必要的資料列或記錄，它們和服務相關，而不是 IaaS。</span><span class="sxs-lookup"><span data-stu-id="308c6-130">For this example, since we are only interested in infrastructure-as-a-Service (IaaS) we can use the transformation steps to remove unnecessary rows, or records, related to services other than IaaS.</span></span>

<span data-ttu-id="308c6-131">以下螢幕擷取畫面顯示轉換步驟，用來處理從 RateCard API 所收集的資料：</span><span class="sxs-lookup"><span data-stu-id="308c6-131">The following screenshot shows the transformation steps used to process the data collected from RateCard API:</span></span>

<span data-ttu-id="308c6-132">![圖 3 - 可處理收集自 RateCard API 之資料的轉換步驟][3]</span><span class="sxs-lookup"><span data-stu-id="308c6-132">![Figure 3 - Transformation steps to process collected data from RateCard API][3]</span></span>

### <a name="defining-new-services-and-rate-plans"></a><span data-ttu-id="308c6-133">定義新的服務和費率方案</span><span class="sxs-lookup"><span data-stu-id="308c6-133">Defining New Services and Rate Plans</span></span>
<span data-ttu-id="308c6-134">有不同的方式可定義 Cloud Cruiser 上的服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-134">There are different ways to define services on Cloud Cruiser.</span></span> <span data-ttu-id="308c6-135">其中一個選項是從使用情況資料匯入服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-135">One of the options is to import the services from the usage data.</span></span> <span data-ttu-id="308c6-136">使用公用雲端，其中的服務已由提供者定義時，通常會使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="308c6-136">This method is commonly used when working with public clouds, where the services are already defined by the provider.</span></span>

<span data-ttu-id="308c6-137">費率方案是一組費率或價格，可根據生效日期、客戶群組或其他選項套用至不同服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-137">A Rate Plan is a set of rates or prices that can be applied to different services, based on effective dates, or group of customers, among other options.</span></span> <span data-ttu-id="308c6-138">費率方案也可以在 Cloud Cruiser 上用來建立模擬或「假設」案例，以了解服務中的變更如何影響工作負載的總成本。</span><span class="sxs-lookup"><span data-stu-id="308c6-138">Rate Plans can also be used on Cloud Cruiser to create simulation or “What-if” scenarios, to understand how changes in services can affect the total cost of a workload.</span></span>

<span data-ttu-id="308c6-139">在此範例中，我們將使用來自 RateCard API 的服務資訊定義 Cloud Cruiser 中的新服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-139">In this example, we will use the service information from the RateCard API to define new services in Cloud Cruiser.</span></span> <span data-ttu-id="308c6-140">同樣地，我們可以使用和服務相關聯的費率，在 Cloud Cruiser 上建立新的費率方案。</span><span class="sxs-lookup"><span data-stu-id="308c6-140">In the same way, we can use the rates associated to the services to create a new Rate Plan on Cloud Cruiser.</span></span>

<span data-ttu-id="308c6-141">在轉換程序結束時，就可以建立新的步驟，並將來自 RateCard API 的資料發佈做為新的服務和費率。</span><span class="sxs-lookup"><span data-stu-id="308c6-141">At the end of the transformation process, it is possible to create a new step and publish the data from the RateCard API as new services and rates.</span></span>

<span data-ttu-id="308c6-142">![圖 4- 將來自 RateCard API 的資料發佈為新的服務和費率][4]</span><span class="sxs-lookup"><span data-stu-id="308c6-142">![Figure 4 - Publishing the data from the RateCard API as new Services and Rates][4]</span></span>

### <a name="verify-azure-services-and-rates"></a><span data-ttu-id="308c6-143">確認 Azure 服務和費率</span><span class="sxs-lookup"><span data-stu-id="308c6-143">Verify Azure Services and Rates</span></span>
<span data-ttu-id="308c6-144">發佈服務及費率之後，您可以在 Cloud Cruiser 的 [ *服務* ] 索引標籤中確認匯入服務的清單：</span><span class="sxs-lookup"><span data-stu-id="308c6-144">After publishing the services and rates, you can verify the list of imported services in Cloud Cruiser’s *Services* tab:</span></span>

<span data-ttu-id="308c6-145">![圖 5- 驗證新的服務][5]</span><span class="sxs-lookup"><span data-stu-id="308c6-145">![Figure 5 - Verifying the new Services][5]</span></span>

<span data-ttu-id="308c6-146">在 [ *費率方案* ] 索引標籤上，您可以利用匯入自 RateCard API 的費率檢查名為 "AzureSimulation" 的費率方案。</span><span class="sxs-lookup"><span data-stu-id="308c6-146">On the *Rate Plans* tab, you can check the new rate plan called “AzureSimulation” with the rates imported from the RateCard API.</span></span>

<span data-ttu-id="308c6-147">![圖 6- 驗證新的費率方案及相關費率][6]</span><span class="sxs-lookup"><span data-stu-id="308c6-147">![Figure 6 - Verifying the new Rate Plan and associated rates][6]</span></span>

### <a name="normalize-wap-and-azure-services"></a><span data-ttu-id="308c6-148">標準化 WAP 和 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="308c6-148">Normalize WAP and Azure Services</span></span>
<span data-ttu-id="308c6-149">根據預設，WAP 會根據計算、記憶體和網路資源等使用情況提供使用情況資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-149">By default, WAP provides usage information based on the use of compute, memory, and network resources.</span></span> <span data-ttu-id="308c6-150">在 Cloud Cruiser 中，您可以直接根據這些資源的配置或計量使用情況來定義服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-150">In Cloud Cruiser, you can define your services based directly on the allocation or metered usage of these resources.</span></span> <span data-ttu-id="308c6-151">例如，您可以設定每小時 CPU 使用量的基本費率，或為配置給執行個體的 GB 記憶體收費。</span><span class="sxs-lookup"><span data-stu-id="308c6-151">For example, you can set a basic rate for each hour of CPU usage, or charge the GB of memory allocated to an instance.</span></span>

<span data-ttu-id="308c6-152">以這個範例而言，為了比較 WAP 和 Azure 之間的成本，我們必須將 WAP 上的資源使用情況彙總套組，進而將其對應至 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="308c6-152">For this example, in order to compare costs between WAP and Azure, we need to aggregate the resource usage on WAP into bundles, which can then be mapped to Azure services.</span></span> <span data-ttu-id="308c6-153">此轉換可以在活頁簿中輕鬆地實作：</span><span class="sxs-lookup"><span data-stu-id="308c6-153">This transformation can be implemented easily in the workbooks:</span></span>

<span data-ttu-id="308c6-154">![圖 7 - 轉換 WAP 資料以將服務標準化][7]</span><span class="sxs-lookup"><span data-stu-id="308c6-154">![Figure 7 - Transforming WAP data to normalize services][7]</span></span>

<span data-ttu-id="308c6-155">活頁簿的最後一個步驟是將資料發佈至 Cloud Cruiser 資料庫。</span><span class="sxs-lookup"><span data-stu-id="308c6-155">The last step at the workbook is to publish the data into the Cloud Cruiser database.</span></span> <span data-ttu-id="308c6-156">在此步驟期間，使用情況資料現在整合為服務 (進而對應至 Azure 服務)，並繫結至預設的費率來建立費用。</span><span class="sxs-lookup"><span data-stu-id="308c6-156">During this step, the usage data is now bundled into services (that map to the Azure Services) and tied to default rates to create the charges.</span></span>

<span data-ttu-id="308c6-157">完成活頁簿之後，您可以在排程器上加入工作，並指定活頁簿執行的頻率和時間，即可自動化資料的處理。</span><span class="sxs-lookup"><span data-stu-id="308c6-157">After finishing the workbook, you can automate the processing of the data, by adding a task on the scheduler and specifying the frequency and time for the workbook to run.</span></span>

<span data-ttu-id="308c6-158">![圖 8 - 活頁簿排程][8]</span><span class="sxs-lookup"><span data-stu-id="308c6-158">![Figure 8 - Workbook scheduling][8]</span></span>

### <a name="create-reports-for-workload-cost-simulation-analysis"></a><span data-ttu-id="308c6-159">建立工作負載成本模擬分析的報告</span><span class="sxs-lookup"><span data-stu-id="308c6-159">Create Reports for Workload Cost Simulation Analysis</span></span>
<span data-ttu-id="308c6-160">收集使用情況並將費用載入 Cloud Cruiser 資料庫之後，我們就可以利用 Cloud Cruiser Insights 模組來建立我們想要的工作負載成本模擬。</span><span class="sxs-lookup"><span data-stu-id="308c6-160">After the usage is collected and charges are loaded into the Cloud Cruiser database, we can leverage the Cloud Cruiser Insights module to create the workload cost simulation that we desire.</span></span>

<span data-ttu-id="308c6-161">為了示範這種案例，我們建立了下列報告：</span><span class="sxs-lookup"><span data-stu-id="308c6-161">In order to demonstrate this scenario, we created the following report:</span></span>

<span data-ttu-id="308c6-162">![成本比較][9]</span><span class="sxs-lookup"><span data-stu-id="308c6-162">![Cost Comparison][9]</span></span>

<span data-ttu-id="308c6-163">上圖顯示以服務為基準的成本比較，其比較在 WAP (深藍色) 與 Azure (淺藍色) 之間為每個特定服務執行工作負載的價格。</span><span class="sxs-lookup"><span data-stu-id="308c6-163">The top graph shows a cost comparison by services, comparing the price of running the workload for each specific service between WAP (dark blue) and Azure (light blue).</span></span>

<span data-ttu-id="308c6-164">下圖顯示依照部門細分的相同資料。</span><span class="sxs-lookup"><span data-stu-id="308c6-164">The bottom graph shows the same data but broken down by department.</span></span> <span data-ttu-id="308c6-165">該圖顯示每個部門在 WAP 和 Azure 上執行其工作負載的成本，以及以節約列 (綠色) 顯示兩者之間的成本差異。</span><span class="sxs-lookup"><span data-stu-id="308c6-165">This shows the costs for each department to run their workload on WAP and Azure, along with the difference between them in the Savings bar (green).</span></span>

## <a name="azure-usage-api"></a><span data-ttu-id="308c6-166">Azure 使用情況 API</span><span class="sxs-lookup"><span data-stu-id="308c6-166">Azure Usage API</span></span>
### <a name="introduction"></a><span data-ttu-id="308c6-167">簡介</span><span class="sxs-lookup"><span data-stu-id="308c6-167">Introduction</span></span>
<span data-ttu-id="308c6-168">Microsoft 最近推出 Azure Usage API，允許訂閱者以程式設計方式提取使用情況資料來洞悉其耗用量。</span><span class="sxs-lookup"><span data-stu-id="308c6-168">Microsoft recently introduced the Azure Usage API, allowing subscribers to programmatically pull in usage data to gain insights into their consumption.</span></span> <span data-ttu-id="308c6-169">這對Cloud Cruiser 客戶而言是好消息，他們可以透過此 API 利用更豐富的資料集。</span><span class="sxs-lookup"><span data-stu-id="308c6-169">This is great news for Cloud Cruiser customers that can take advantage of the richer dataset available through this API.</span></span>

<span data-ttu-id="308c6-170">Cloud Cruiser 可以數種方式運用和 Usage API 的整合。</span><span class="sxs-lookup"><span data-stu-id="308c6-170">Cloud Cruiser can leverage the integration with the Usage API in several ways.</span></span> <span data-ttu-id="308c6-171">可透過 API 使用的資料粒度 (每小時使用量資訊) 和資源中繼資料資訊可提供必要的資料集來支援彈性的回報或退款模型。</span><span class="sxs-lookup"><span data-stu-id="308c6-171">The granularity (hourly usage information) and resource metadata information available through the API provides the necessary dataset to support flexible Showback or Chargeback models.</span></span> 

<span data-ttu-id="308c6-172">在本教學課程中，我們將提供 Cloud Cruiser 如何使用 Usage API 資訊獲得好處的一個範例。</span><span class="sxs-lookup"><span data-stu-id="308c6-172">In this tutorial, we will present one example of how Cloud Cruiser can benefit from the Usage API information.</span></span> <span data-ttu-id="308c6-173">更具體來說，我們將在 Azure 上建立資源群組、將帳戶結構的標記相關聯，然後描述提取和處理標記資訊到 Cloud Cruiser 的程序。</span><span class="sxs-lookup"><span data-stu-id="308c6-173">More specifically, we will create a Resource Group on Azure, associate tags for the account structure, then describe the process of pulling and processing the tag information into Cloud Cruiser.</span></span>

<span data-ttu-id="308c6-174">最終的目標是要能夠建立和下方報告類似的報告，而且能夠根據標記填入的帳戶結構分析成本和耗用量。</span><span class="sxs-lookup"><span data-stu-id="308c6-174">The final goal is to be able to create reports like the following one, and be able to analyze cost and consumption based on the account structure populated by the tags.</span></span>

<span data-ttu-id="308c6-175">![圖 10 - 含有使用標記之細項的報告][10]</span><span class="sxs-lookup"><span data-stu-id="308c6-175">![Figure 10 - Report with breakdowns using tags][10]</span></span>

### <a name="microsoft-azure-tags"></a><span data-ttu-id="308c6-176">Microsoft Azure 標記</span><span class="sxs-lookup"><span data-stu-id="308c6-176">Microsoft Azure Tags</span></span>
<span data-ttu-id="308c6-177">可透過 Azure Usage API 使用的資料不僅包括耗用量資訊，還包括內含於其相關聯之任何標記的資源中繼資料。</span><span class="sxs-lookup"><span data-stu-id="308c6-177">The data available through the Azure Usage API includes not only consumption information, but also resource metadata including any tags associated with it.</span></span> <span data-ttu-id="308c6-178">標記可提供簡單的方式組織您的資源，但是為了有效率，您必須確認：</span><span class="sxs-lookup"><span data-stu-id="308c6-178">Tags provide an easy way to organize your resources, but in order to be effective, you need to ensure that:</span></span>

* <span data-ttu-id="308c6-179">標記在佈建階段正確套用至資源</span><span class="sxs-lookup"><span data-stu-id="308c6-179">Tags are correctly applied to the resources at provision time</span></span>
* <span data-ttu-id="308c6-180">標記正確用於回報/退款程序，以將使用情況繫結至組織的帳戶結構。</span><span class="sxs-lookup"><span data-stu-id="308c6-180">Tags are properly used on the Showback/Chargeback process to tie the usage to the organization’s account structure.</span></span>

<span data-ttu-id="308c6-181">兩個需求都頗具挑戰性，特別是當佈建或收費端上有手動程序時。</span><span class="sxs-lookup"><span data-stu-id="308c6-181">Both of these requirements can be challenging, especially when there is a manual process on the provision or charging side.</span></span> <span data-ttu-id="308c6-182">輸入錯誤、不正確或甚至是遺漏標記，都是客戶使用標籤時的常見抱怨，這些錯誤可能會使收費端的工作非常困難。</span><span class="sxs-lookup"><span data-stu-id="308c6-182">Mistyped, incorrect or even missing tags are common complaints from customers when using tags and these errors can make life on the charging side very difficult.</span></span>

<span data-ttu-id="308c6-183">使用新的 Azure Usage API，Cloud Cruiser 可以提取資源標記資訊，並透過複雜的 ETL 工具 (稱為活頁簿) 修正這些常見的標記錯誤。</span><span class="sxs-lookup"><span data-stu-id="308c6-183">With the new Azure Usage API, Cloud Cruiser can pull resource tagging information, and through a sophisticated ETL tool called workbooks, fix these common tagging errors.</span></span> <span data-ttu-id="308c6-184">透過運用規則運算式和資料相互關聯的轉換作業，Cloud Cruiser 能夠識別不正確標記的資源並套用正確的標記，確保資源和取用者之間有正確的關聯。</span><span class="sxs-lookup"><span data-stu-id="308c6-184">Through transformation using regular expressions and data correlation, Cloud Cruiser can identify incorrectly tagged resources and apply the correct tags, ensuring the correct association of the resources with the consumer.</span></span>

<span data-ttu-id="308c6-185">在收費端，Cloud Cruiser 可自動化回報/退款程序，並且可以運用標記資訊將使用情況繫結至適當的取用者 (部門、事業處、專案等)。</span><span class="sxs-lookup"><span data-stu-id="308c6-185">On the charging side, Cloud Cruiser automates the Showback/Chargeback process, and can leverage the tag information to tie the usage to the appropriate consumer (Department, Division, Project, etc.).</span></span> <span data-ttu-id="308c6-186">這項自動化作業提供非常重大的改進，並且可以確保一致且可稽核的收費程序。</span><span class="sxs-lookup"><span data-stu-id="308c6-186">This automation provides a huge improvement and can ensure a consistent and auditable charging process.</span></span>

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a><span data-ttu-id="308c6-187">使用 Microsoft Azure 上的標記建立資源群組</span><span class="sxs-lookup"><span data-stu-id="308c6-187">Creating a Resource Group with tags on Microsoft Azure</span></span>
<span data-ttu-id="308c6-188">本教學課程的第一個步驟是在 Azure 入口網站上建立資源群組，然後建立新的標記以產生和資源之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="308c6-188">The first step in this tutorial is to create a Resource Group in the Azure portal, then create new tags to associate to the resources.</span></span> <span data-ttu-id="308c6-189">為了這個範例，我們將建立下列標記：部門、環境、擁有者、專案。</span><span class="sxs-lookup"><span data-stu-id="308c6-189">For this example, we will be creating the following tags: Department, Environment, Owner, Project.</span></span>

<span data-ttu-id="308c6-190">以下螢幕擷取畫面顯示具有相關聯標記的範例資源群組。</span><span class="sxs-lookup"><span data-stu-id="308c6-190">The screenshot below shows a sample Resource Group with the associated tags.</span></span>

<span data-ttu-id="308c6-191">![圖 11 - 在 Azure 入口網站上具有相關標記的資源群組][11]</span><span class="sxs-lookup"><span data-stu-id="308c6-191">![Figure 11 - Resource Group with associated tags on Azure portal][11]</span></span>

<span data-ttu-id="308c6-192">下一步是將資訊從 Usage API 提取到 Cloud Cruiser。</span><span class="sxs-lookup"><span data-stu-id="308c6-192">The next step is to pull the information from the Usage API into Cloud Cruiser.</span></span> <span data-ttu-id="308c6-193">Usage API 目前提供 JSON 格式的回應。</span><span class="sxs-lookup"><span data-stu-id="308c6-193">The Usage API currently provides responses in JSON format.</span></span> <span data-ttu-id="308c6-194">擷取的資料範例如下：</span><span class="sxs-lookup"><span data-stu-id="308c6-194">Here is a sample of the data retrieved:</span></span>

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


### <a name="import-data-from-the-usage-api-into-cloud-cruiser"></a><span data-ttu-id="308c6-195">將資料從 Usage API 匯入到 Cloud Cruiser</span><span class="sxs-lookup"><span data-stu-id="308c6-195">Import data from the Usage API into Cloud Cruiser</span></span>
<span data-ttu-id="308c6-196">Cloud Cruiser 活頁簿提供自動化的方式收集和處理來自 Usage API 的資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-196">Cloud Cruiser workbooks provide an automated way to collect and process information from the Usage API.</span></span> <span data-ttu-id="308c6-197">ETL (擷取-轉換-載入) 活頁簿可讓您設定資料的集合、轉換和發佈至 Cloud Cruiser 資料庫。</span><span class="sxs-lookup"><span data-stu-id="308c6-197">An ETL (extract-transform-load) workbook allows you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span></span>

<span data-ttu-id="308c6-198">每個活頁簿可以有一個或多個集合。</span><span class="sxs-lookup"><span data-stu-id="308c6-198">Each workbook can have one or multiple collections.</span></span> <span data-ttu-id="308c6-199">這可讓您將來自不同資源的資訊相互關聯，以補充或強化使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="308c6-199">This allows you to correlate information from different sources to complement or augment the usage data.</span></span> <span data-ttu-id="308c6-200">在此範例中，我們將在 Azure 範本活頁簿中建立新的工作表 (*UsageAPI)* 並設定新的「集合」以從 Usage API 匯入資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-200">For this example, we will create a new sheet in the Azure template workbook (*UsageAPI)* and set a new *collection* to import information from the Usage API.</span></span>

<span data-ttu-id="308c6-201">![圖 3 - 匯入至 UsageAPI 工作表的 Usage API 資料][12]</span><span class="sxs-lookup"><span data-stu-id="308c6-201">![Figure 3 - Usage API data imported into the UsageAPI sheet][12]</span></span>

<span data-ttu-id="308c6-202">請注意，此活頁簿已有從 Azure 匯入服務的其他工作表 (*ImportServices*)，以及從 Billing API 處理耗用量資訊的工作表 (*PublishData*)。</span><span class="sxs-lookup"><span data-stu-id="308c6-202">Notice that this workbook already has other sheets to import services from Azure (*ImportServices*), and process the consumption information from the Billing API (*PublishData*).</span></span>

<span data-ttu-id="308c6-203">接下來，我們要使用 Usage API來填入 *UsageAPI* 工作表，然後在 *PublishData* 工作表上建立此資訊與來自 Billing API 之耗用量資料的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="308c6-203">Next we will use the Usage API to populate the *UsageAPI* sheet, and correlate the information with the consumption data from the Billing API on the *PublishData* sheet.</span></span>

### <a name="processing-the-tag-information-from-the-usage-api"></a><span data-ttu-id="308c6-204">處理來自 Usage API 的標記資訊</span><span class="sxs-lookup"><span data-stu-id="308c6-204">Processing the tag information from the Usage API</span></span>
<span data-ttu-id="308c6-205">將資料匯入活頁簿之後，我們將在 *UsageAPI* 工作表中建立轉換步驟以處理來自 API 的資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-205">After importing the data into the workbook, we will create transformation steps in the *UsageAPI* sheet in order to process the information from the API.</span></span> <span data-ttu-id="308c6-206">第一個步驟是使用「JSON 分割」處理器，從單一欄位擷取標記，再為每個標記建立欄位 (部門、專案、擁有者和環境)。</span><span class="sxs-lookup"><span data-stu-id="308c6-206">First step is to use a “JSON split” processor to extract the tags from a single field, then create fields for each one of them (Department, Project, Owner, and Environment).</span></span>

<span data-ttu-id="308c6-207">![圖 4 - 建立新的標記資訊欄位][13]</span><span class="sxs-lookup"><span data-stu-id="308c6-207">![Figure 4 - Create new fields for the tag information][13]</span></span>

<span data-ttu-id="308c6-208">請注意，「網路」服務遺漏了標記資訊 (黃色方塊)，但我們可以藉由查看 *ResourceGroupName* 欄位，確認這個服務屬於相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="308c6-208">Notice the “Networking” service is missing the tag information (yellow box), but we can verify that it is part of the same Resource Group by looking at the *ResourceGroupName* field.</span></span> <span data-ttu-id="308c6-209">由於我們已經擁有該資源群組中其他資源的標記，所以稍後我們可以在程序中使用這項資訊，將遺漏的標記套用至此資源。</span><span class="sxs-lookup"><span data-stu-id="308c6-209">Since we have the tags for the other resources from this Resource Group, we can use this information to apply the missing tags to this resource later in the process.</span></span>

<span data-ttu-id="308c6-210">下一步是建立查閱資料表，將來自標記的資訊關聯至 *ResourceGroupName*。</span><span class="sxs-lookup"><span data-stu-id="308c6-210">The next step is to create a lookup table associating the information from the tags to the *ResourceGroupName*.</span></span> <span data-ttu-id="308c6-211">下一個步驟將使用此查閱資料表，以利用標記資訊充實消耗量資料。</span><span class="sxs-lookup"><span data-stu-id="308c6-211">This lookup table will be used on the next step to enrich the consumption data with tag information.</span></span>

### <a name="adding-the-tag-information-to-the-consumption-data"></a><span data-ttu-id="308c6-212">將標記資訊加入至消耗量資料</span><span class="sxs-lookup"><span data-stu-id="308c6-212">Adding the tag information to the consumption data</span></span>
<span data-ttu-id="308c6-213">現在我們可以跳至處理來自 Billing API 之耗用量資訊的 *PublishData* 工作表，並新增從標記擷取的欄位。</span><span class="sxs-lookup"><span data-stu-id="308c6-213">Now we can jump to the *PublishData* sheet, which processes the consumption information from the Billing API, and add the fields extracted from the tags.</span></span> <span data-ttu-id="308c6-214">此程序的執行方式為查看上一個步驟中建立的查閱資料表，使用 *ResourceGroupName* 做為查閱的金鑰。</span><span class="sxs-lookup"><span data-stu-id="308c6-214">This process is performed by looking at the lookup table created on the previous step, using the *ResourceGroupName* as the key for the lookups.</span></span>

<span data-ttu-id="308c6-215">![圖 5 - 將來自查閱的資訊填入帳戶結構中][14]</span><span class="sxs-lookup"><span data-stu-id="308c6-215">![Figure 5 - Populating the account structure with the information from the lookups][14]</span></span>

<span data-ttu-id="308c6-216">請注意，已套用「網路」服務的適當帳戶結構欄位，利用遺漏標記修正問題。</span><span class="sxs-lookup"><span data-stu-id="308c6-216">Notice that the appropriate account structure fields for the “Networking” service were applied, fixing the issue with the missing tags.</span></span> <span data-ttu-id="308c6-217">我們也在目標資源群組已外的帳戶結構欄位中填入「其他」以在報告中區別它們。</span><span class="sxs-lookup"><span data-stu-id="308c6-217">We also populated the account structure fields for resources other than our target Resource Group with “Other”, in order to differentiate them on the reports.</span></span>

<span data-ttu-id="308c6-218">現在我們只需要加入發佈使用情況資料的步驟即可。</span><span class="sxs-lookup"><span data-stu-id="308c6-218">Now we just need to add a step to publish the usage data.</span></span> <span data-ttu-id="308c6-219">在這個步驟中，在費率方案上定義之每個服務的適當費率將套用至使用情況資訊，產生費用也會載入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="308c6-219">During this step, the appropriate rates for each service defined on our Rate Plan will be applied to the usage information, with the resulting charge loaded into the database.</span></span>

<span data-ttu-id="308c6-220">最棒的部分是您只需要完成此程序一次。</span><span class="sxs-lookup"><span data-stu-id="308c6-220">The best part is that you only have to go through this process once.</span></span> <span data-ttu-id="308c6-221">完成活頁簿之後，您只需要將它加入至排程器，它就會依照排程時間每小時或每日執行一次。</span><span class="sxs-lookup"><span data-stu-id="308c6-221">When the workbook is completed, you just need to add it to the scheduler and it will run hourly or daily at the scheduled time.</span></span> <span data-ttu-id="308c6-222">然後就只需建立新報告或自訂現有報告，進而藉由分析資料從雲端使用情況取得有意義的見解。</span><span class="sxs-lookup"><span data-stu-id="308c6-222">Then it’s just a matter of creating new reports, or customizing existing ones, in order to analyze the data to get meaningful insights from your cloud usage.</span></span>

### <a name="next-steps"></a><span data-ttu-id="308c6-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="308c6-223">Next Steps</span></span>
* <span data-ttu-id="308c6-224">如需建立 Cloud Cruiser 活頁簿和報告的詳細指示，請參閱 Cloud Cruiser 的線上 [文件](http://docs.cloudcruiser.com/) (需要有效的登入)。</span><span class="sxs-lookup"><span data-stu-id="308c6-224">For detailed instructions on creating Cloud Cruiser workbooks and reports, please refer to Cloud Cruiser’s online [documentation](http://docs.cloudcruiser.com/) (valid login required).</span></span>  <span data-ttu-id="308c6-225">如需有關 Cloud Cruiser 的詳細資訊，請連絡 [info@cloudcruiser.com](mailto:info@cloudcruiser.com)。</span><span class="sxs-lookup"><span data-stu-id="308c6-225">For more information about Cloud Cruiser, please contact [info@cloudcruiser.com](mailto:info@cloudcruiser.com).</span></span>
* <span data-ttu-id="308c6-226">請參閱 [深入了解 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md) 以取得 Azure 資源使用情況和 RateCard API 的概觀。</span><span class="sxs-lookup"><span data-stu-id="308c6-226">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of the Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="308c6-227">查看 [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) 以取得屬於 Azure 資源管理員所提供之 API 集合的兩個 API 之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="308c6-227">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of the set of APIs provided by the Azure Resource Manager.</span></span>
* <span data-ttu-id="308c6-228">如果您想要探究範例程式碼，請查看 [Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?term=billing)上的＜Microsoft Azure 計費 API 程式碼範例＞。</span><span class="sxs-lookup"><span data-stu-id="308c6-228">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

### <a name="learn-more"></a><span data-ttu-id="308c6-229">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="308c6-229">Learn More</span></span>
* <span data-ttu-id="308c6-230">請參閱 [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md) 一文，以深入了解 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="308c6-230">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article to learn more about the Azure Resource Manager.</span></span>

<!--Image references-->

<span data-ttu-id="308c6-231">[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "圖 1 - 建立新的集合"</span><span class="sxs-lookup"><span data-stu-id="308c6-231">[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Figure 1 - Creating a new collection"</span></span>
<span data-ttu-id="308c6-232">[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "圖 2 - 從新集合匯入資料"</span><span class="sxs-lookup"><span data-stu-id="308c6-232">[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figure 2 - Import data from the new collection"</span></span>
<span data-ttu-id="308c6-233">[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "圖 3 - 可處理收集自 RateCard API 之資料的轉換步驟"</span><span class="sxs-lookup"><span data-stu-id="308c6-233">[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figure 3 - Transformation steps to process collected data from RateCard API"</span></span>
<span data-ttu-id="308c6-234">[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "圖 4- 將來自 RateCard API 的資料發佈為新的服務和費率"</span><span class="sxs-lookup"><span data-stu-id="308c6-234">[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figure 4 - Publishing the data from the RateCard API as new Services and Rates"</span></span>
<span data-ttu-id="308c6-235">[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "圖 5- 驗證新的服務"</span><span class="sxs-lookup"><span data-stu-id="308c6-235">[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figure 5 - Verifying the new Services"</span></span>
<span data-ttu-id="308c6-236">[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "圖 6- 驗證新的費率方案及相關費率"</span><span class="sxs-lookup"><span data-stu-id="308c6-236">[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figure 6 - Verifying the new Rate Plan and associated rates"</span></span>
<span data-ttu-id="308c6-237">[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "圖 7 - 轉換 WAP 資料以將服務標準化"</span><span class="sxs-lookup"><span data-stu-id="308c6-237">[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figure 7 - Transforming WAP data to normalize services"</span></span>
<span data-ttu-id="308c6-238">[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "圖 8 - 活頁簿排程"</span><span class="sxs-lookup"><span data-stu-id="308c6-238">[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Figure 8 - Workbook scheduling"</span></span>
<span data-ttu-id="308c6-239">[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "圖 9 - 工作負載成本比較案例的範例報告"</span><span class="sxs-lookup"><span data-stu-id="308c6-239">[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figure 9 - Sample Report for the Workload cost comparison scenario"</span></span>
<span data-ttu-id="308c6-240">[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "圖 10 - 含有使用標記之細項的報告"</span><span class="sxs-lookup"><span data-stu-id="308c6-240">[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Figure 10 - Report with breakdowns using tags"</span></span>
<span data-ttu-id="308c6-241">[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "圖 11 - 在 Azure 入口網站上具有相關標記的資源群組"</span><span class="sxs-lookup"><span data-stu-id="308c6-241">[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Figure 11 - Resource Group with associated tags on Azure portal"</span></span>
<span data-ttu-id="308c6-242">[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "圖 12 - 匯入至 UsageAPI 工作表的 Usage API 資料"</span><span class="sxs-lookup"><span data-stu-id="308c6-242">[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figure 12 - Usage API data imported into the UsageAPI sheet"</span></span>
<span data-ttu-id="308c6-243">[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "圖 13 - 建立新的標記資訊欄位"</span><span class="sxs-lookup"><span data-stu-id="308c6-243">[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figure 13 - Create new fields for the tag information"</span></span>
<span data-ttu-id="308c6-244">[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "圖 14 - 將來自查閱的資訊填入帳戶結構中"</span><span class="sxs-lookup"><span data-stu-id="308c6-244">[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Figure 14 - Populating the account structure with the information from the lookups"</span></span>
