---
title: "Azure Cosmos DB 規模和效能測試 | Microsoft Docs"
description: "了解使用 Azure Cosmos DB 來執行規模和效能測試"
keywords: "效能測試"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="aeced-104">Azure Cosmos DB 的效能和規模測試</span><span class="sxs-lookup"><span data-stu-id="aeced-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="aeced-105">效能和規模測試是應用程式開發過程中的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="aeced-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="aeced-106">對許多應用程式來說，資料庫層對整體效能和延展性具有相當重大的影響，因此是效能測試的重要元件。</span><span class="sxs-lookup"><span data-stu-id="aeced-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="aeced-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是為了能夠彈性延展及獲得可預測的效能而建置，因此非常適合需要高效能資料庫層的應用程式。</span><span class="sxs-lookup"><span data-stu-id="aeced-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="aeced-108">這篇文章適合做為針對其 Cosmos DB 工作負載實作效能測試套件或針對高效能應用程式案例評估 Cosmos DB 之開發人員的參考。</span><span class="sxs-lookup"><span data-stu-id="aeced-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="aeced-109">主要是著重在隔離的資料庫效能測試，但也包含適用於實際執行應用程式的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="aeced-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="aeced-110">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="aeced-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="aeced-111">哪裡可以找到可供進行 Cosmos DB 效能測試的範例 .NET 用戶端應用程式？</span><span class="sxs-lookup"><span data-stu-id="aeced-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="aeced-112">如何藉由 Cosmos DB 從我的用戶端應用程式達到高輸送量層級？</span><span class="sxs-lookup"><span data-stu-id="aeced-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="aeced-113">若要開始使用程式碼，請從 [Azure Cosmos DB 效能測試範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)下載專案。</span><span class="sxs-lookup"><span data-stu-id="aeced-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="aeced-114">此應用程式的目標，在於示範透過少數用戶端電腦發揮 Cosmos DB 更好效能的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="aeced-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="aeced-115">而不是要示範可以無限制調整的服務尖峰容量。</span><span class="sxs-lookup"><span data-stu-id="aeced-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="aeced-116">如果您要尋找用戶端設定選項，以改善 Cosmos DB 效能，請參閱 [Azure Cosmos DB 效能祕訣](performance-tips.md)。</span><span class="sxs-lookup"><span data-stu-id="aeced-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="aeced-117">執行效能測試應用程式</span><span class="sxs-lookup"><span data-stu-id="aeced-117">Run the performance testing application</span></span>
<span data-ttu-id="aeced-118">若要開始使用，最快的方法就是依以下步驟所述，編譯並執行下面的 .NET 範例。</span><span class="sxs-lookup"><span data-stu-id="aeced-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="aeced-119">您也可以檢閱原始程式碼，然後對自己的用戶端應用程式實作類似的組態。</span><span class="sxs-lookup"><span data-stu-id="aeced-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="aeced-120">**步驟 1：**從 [Azure Cosmos DB 效能測試範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark) 或 GitHub 存放庫的分支下載專案。</span><span class="sxs-lookup"><span data-stu-id="aeced-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="aeced-121">**步驟 2：** 修改 App.config 中 EndpointUrl、AuthorizationKey、CollectionThroughput 及 DocumentTemplate (選擇性) 的設定。</span><span class="sxs-lookup"><span data-stu-id="aeced-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="aeced-122">以高輸送量佈建集合之前，請參閱 [價格頁面](https://azure.microsoft.com/pricing/details/cosmos-db/) 以估算每個集合的成本。</span><span class="sxs-lookup"><span data-stu-id="aeced-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="aeced-123">Azure Cosmos DB 對儲存體和輸送量是以小時為基礎獨立計費，因此您可以藉由在測試後刪除或降低 Azure Cosmos DB 集合的輸送量來節省成本。</span><span class="sxs-lookup"><span data-stu-id="aeced-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="aeced-124">**步驟 3：** 從命令列編譯並執行主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="aeced-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="aeced-125">您應該會看到如以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="aeced-125">You should see output like the following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="aeced-126">**步驟 4 (如有必要)：** 從工具回報的輸送量 (RU/秒) 應該等於或大於佈建的集合輸送量。</span><span class="sxs-lookup"><span data-stu-id="aeced-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="aeced-127">如果情況並非如此，向上微調 DegreeOfParallelism 可協助您達到該限制。</span><span class="sxs-lookup"><span data-stu-id="aeced-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="aeced-128">如果來自用戶端應用程式的輸送量達持平狀態，在相同或不同機器上啟動多個應用程式執行個體將可協助您在各個不同的執行個體達到所佈建的限制。</span><span class="sxs-lookup"><span data-stu-id="aeced-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="aeced-129">如果您需要協助進行這個步驟，請撰寫電子郵件寄至 askcosmosdb@microsoft.com 或在 [Azure 入口網站](https://portal.azure.com)提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="aeced-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="aeced-130">讓應用程式處於執行狀態之後，您便可以嘗試不同的[索引編製原則](indexing-policies.md)和[一致性層級](consistency-levels.md)，以了解它們對輸送量和延遲的影響。</span><span class="sxs-lookup"><span data-stu-id="aeced-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="aeced-131">您也可以檢閱原始程式碼，然後對自己的測試套件或實際執行應用程式實作類似的組態。</span><span class="sxs-lookup"><span data-stu-id="aeced-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeced-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aeced-132">Next steps</span></span>
<span data-ttu-id="aeced-133">在這篇文章中，我們探討了如何使用 .NET 主控台應用程式來執行 Cosmos DB 的相關效能和規模測試。</span><span class="sxs-lookup"><span data-stu-id="aeced-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="aeced-134">如需有關使用 Azure Cosmos DB 的其他資訊，請參閱下面的連結。</span><span class="sxs-lookup"><span data-stu-id="aeced-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="aeced-135">Azure Cosmos DB 效能測試範例</span><span class="sxs-lookup"><span data-stu-id="aeced-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="aeced-136">改善 Azure Cosmos DB 效能的用戶端設定選項</span><span class="sxs-lookup"><span data-stu-id="aeced-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="aeced-137">Azure Cosmos DB 中的伺服器端資料分割</span><span class="sxs-lookup"><span data-stu-id="aeced-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


