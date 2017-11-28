---
title: "aaaAzure Cosmos DB 規模和效能測試 |Microsoft 文件"
description: "了解 tooperform 的調整規模和效能測試以 Azure Cosmos DB"
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
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="7791b-104">Azure Cosmos DB 的效能和規模測試</span><span class="sxs-lookup"><span data-stu-id="7791b-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="7791b-105">效能和規模測試是應用程式開發過程中的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="7791b-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="7791b-106">對於許多應用程式，hello 資料庫層次都有重大影響 hello 整體效能和延展性，且因此效能的重要元件測試。</span><span class="sxs-lookup"><span data-stu-id="7791b-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="7791b-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是為了能夠彈性延展及獲得可預測的效能而建置，因此非常適合需要高效能資料庫層的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7791b-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="7791b-108">這篇文章適合做為針對其 Cosmos DB 工作負載實作效能測試套件或針對高效能應用程式案例評估 Cosmos DB 之開發人員的參考。</span><span class="sxs-lookup"><span data-stu-id="7791b-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="7791b-109">其主要著重在隔離的效能測試的 hello 資料庫，但也包含 實際執行應用程式的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="7791b-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="7791b-110">閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="7791b-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="7791b-111">哪裡可以找到可供進行 Cosmos DB 效能測試的範例 .NET 用戶端應用程式？</span><span class="sxs-lookup"><span data-stu-id="7791b-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="7791b-112">如何藉由 Cosmos DB 從我的用戶端應用程式達到高輸送量層級？</span><span class="sxs-lookup"><span data-stu-id="7791b-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="7791b-113">tooget 啟動程式碼時，請下載 hello 專案從[Azure Cosmos DB 效能測試的範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)。</span><span class="sxs-lookup"><span data-stu-id="7791b-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="7791b-114">此應用程式的 hello 目標是 toodemonstrate 解壓縮從 Cosmos DB 更佳的效能較少的用戶端電腦的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="7791b-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="7791b-115">這是不會進行 hello 服務，可以調整 limitlessly toodemonstrate hello 尖峰容量。</span><span class="sxs-lookup"><span data-stu-id="7791b-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="7791b-116">如果您要尋找用戶端設定選項 tooimprove Cosmos DB 的效能，請參閱[Azure Cosmos DB 效能祕訣](performance-tips.md)。</span><span class="sxs-lookup"><span data-stu-id="7791b-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="7791b-117">執行 hello 效能測試應用程式</span><span class="sxs-lookup"><span data-stu-id="7791b-117">Run hello performance testing application</span></span>
<span data-ttu-id="7791b-118">hello 最快方式 tooget 啟動，而且 toocompile 執行的 hello.NET 範例下, 面 hello 步驟中所述。</span><span class="sxs-lookup"><span data-stu-id="7791b-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="7791b-119">您也可以檢閱 hello 原始程式碼，並實作類似組態 tooyour 自己的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7791b-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="7791b-120">**步驟 1:**下載 hello 專案從[Azure Cosmos DB 效能測試的範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)，或 「 分叉 」 hello GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7791b-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="7791b-121">**步驟 2:**修改的端點 Url、 AuthorizationKey、 CollectionThroughput 和 DocumentTemplate （選擇性） 在 App.config 中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="7791b-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="7791b-122">之前佈建具有高輸送量的集合，請參閱 toohello[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)tooestimate hello 成本，每個集合。</span><span class="sxs-lookup"><span data-stu-id="7791b-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="7791b-123">Azure 的 Cosmos db-storage 帳單和獨立每小時，因此您可以藉由刪除或降低 Azure Cosmos DB 集合 hello 輸送量測試後節省成本的輸送量。</span><span class="sxs-lookup"><span data-stu-id="7791b-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="7791b-124">**步驟 3:**編譯及執行 hello 主控台應用程式從 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="7791b-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="7791b-125">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7791b-125">You should see output like hello following:</span></span>

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


<span data-ttu-id="7791b-126">**步驟 4 （如有必要）：** hello 輸送量報告 （RU/秒） 從 hello 工具應該 hello 相同或高於 hello hello 集合的佈建的輸送量。</span><span class="sxs-lookup"><span data-stu-id="7791b-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="7791b-127">否則，請增加 hello DegreeOfParallelism 少量遞增的方式可協助您達到 hello。</span><span class="sxs-lookup"><span data-stu-id="7791b-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="7791b-128">如果您的用戶端應用程式中的 hello 輸送量會停滯不前，啟動 hello 應用程式的多個執行個體上 hello 相同或不同的電腦將協助您達到佈建的 hello hello 跨不同的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7791b-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="7791b-129">如果您需要這個步驟的說明，請撰寫一封電子郵件tooaskcosmosdb@microsoft.com或提出支援票證從 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7791b-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7791b-130">一旦您擁有 hello 應用程式執行時，您可以嘗試不同[編製索引原則](indexing-policies.md)和[一致性層級](consistency-levels.md)toounderstand 其對輸送量和延遲的影響。</span><span class="sxs-lookup"><span data-stu-id="7791b-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="7791b-131">您也可以檢閱 hello 原始程式碼，並實作類似的設定 tooyour 自己的測試套件或實際執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="7791b-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7791b-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7791b-132">Next steps</span></span>
<span data-ttu-id="7791b-133">在這篇文章中，我們探討了如何使用 .NET 主控台應用程式來執行 Cosmos DB 的相關效能和規模測試。</span><span class="sxs-lookup"><span data-stu-id="7791b-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="7791b-134">請如需使用 Azure Cosmos DB 的詳細資訊，參閱下列 toohello 連結。</span><span class="sxs-lookup"><span data-stu-id="7791b-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="7791b-135">Azure Cosmos DB 效能測試範例</span><span class="sxs-lookup"><span data-stu-id="7791b-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="7791b-136">用戶端設定選項 tooimprove Azure Cosmos DB 效能</span><span class="sxs-lookup"><span data-stu-id="7791b-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="7791b-137">Azure Cosmos DB 中的伺服器端資料分割</span><span class="sxs-lookup"><span data-stu-id="7791b-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


