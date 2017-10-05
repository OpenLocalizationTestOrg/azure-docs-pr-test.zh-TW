---
title: "如何在 Azure 搜尋服務中管理對於資源的並行寫入"
description: "使用開放式同步存取來避免在針對 Azure 搜尋服務索引、索引子及資料來源的更新或刪除過程中發生衝突。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: aee1b7376d4829e3e2f5a232525e3c3cb4df9d8e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-manage-concurrency-in-azure-search"></a><span data-ttu-id="bf6fc-103">如何管理 Azure 搜尋服務中的並行</span><span class="sxs-lookup"><span data-stu-id="bf6fc-103">How to manage concurrency in Azure Search</span></span>

<span data-ttu-id="bf6fc-104">管理如索引及資料來源的 Azure 搜尋服務資源時，能夠安全地更新資源是一件很重要的事，尤其是在應用程式中有不同的元件正在同時存取資源時。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-104">When managing Azure Search resources such as indexes and data sources, it's important to update resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="bf6fc-105">當兩個用戶端在未經協調的情況下同時更新資源時，便可能發生競爭情形。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="bf6fc-106">為了避免這個問題，Azure 搜尋服務提供了「開放式同步存取模型」。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-106">To prevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="bf6fc-107">資源上不會有鎖定的情形。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-107">There are no locks on a resource.</span></span> <span data-ttu-id="bf6fc-108">每個資源都會有一個能識別資源版本的 ETag，使您可以製作能避免意外覆寫的要求。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-108">Instead, there is an ETag for every resource that identifies the resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="bf6fc-109">[範例 C# 解決方案](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) \(英文\) 中的概念程式碼能說明 Azure 搜尋服務中並行控制的運作方式。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="bf6fc-110">該程式碼會建立能叫用並行控制的條件。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-110">The code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="bf6fc-111">對於大多數開發人員而言，閱讀[下方的程式碼片段](#samplecode)應該就已經足夠，但如果您想要執行該程式碼片段，請編輯 appsettings.json 以新增服務名稱和系統管理員 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-111">Reading the [code fragment below](#samplecode) is probably sufficient for most developers, but if you want to run it, edit appsettings.json to add the service name and an admin api-key.</span></span> <span data-ttu-id="bf6fc-112">若服務 URL 為 `http://myservice.search.windows.net`，服務名稱將會是 `myservice`。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-112">Given a service URL of `http://myservice.search.windows.net`, the service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="bf6fc-113">運作方式</span><span class="sxs-lookup"><span data-stu-id="bf6fc-113">How it works</span></span>

<span data-ttu-id="bf6fc-114">開放式同步存取的實作方式，是透過對寫入索引、索引子、資料來源及 synonymMap 資源的 API 呼叫進行存取條件檢查。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-114">Optimistic concurrency is implemented through access condition checks in API calls writing to indexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="bf6fc-115">所有資源都有能提供物件版本資訊的[*實體標記 (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag)。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="bf6fc-116">透過先檢查 ETag 並確保資源的 ETag 符合您的本機複本，將可以避免在一般工作流程 (取得，於本機修改，更新) 中發生同時更新。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-116">By checking the ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring the resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="bf6fc-117">REST API 會在要求標頭上使用 [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-117">The REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the request header.</span></span>
+ <span data-ttu-id="bf6fc-118">.NET SDK 透過 accessCondition 物件設定 ETag，並在資源上設定 [If-Match | If-Match-None 標頭](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-118">The .NET SDK sets the ETag through an accessCondition object, setting the [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the resource.</span></span> <span data-ttu-id="bf6fc-119">繼承自 [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) \(英文\) 的任何物件都具有 accessCondition 物件。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="bf6fc-120">每次更新資源時，該資源的 ETag 都會自動變更。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="bf6fc-121">當您實作並行管理時，所做的就是為更新要求設置前置條件，要求遠端資源的 ETag 必須與您在用戶端上所修改之資源複本的 ETag 相同。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-121">When you implement concurrency management, all you're doing is putting a precondition on the update request that requires the remote resource to have the same ETag as the copy of the resource that you modified on the client.</span></span> <span data-ttu-id="bf6fc-122">如果並行處理程序已變更遠端資源，其 ETag 將會與前置條件不符，且該要求將會失敗並顯示 HTTP 412。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-122">If a concurrent process has changed the remote resource already, the ETag will not match the precondition and the request will fail with HTTP 412.</span></span> <span data-ttu-id="bf6fc-123">如果您是使用 .NET SDK，這會顯示為 `CloudException`，其中 `IsAccessConditionFailed()` 擴充方法會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-123">If you're using the .NET SDK, this manifests as a `CloudException` where the `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="bf6fc-124">並行只有一種機制。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="bf6fc-125">無論資源更新是使用哪一種 API，都只會使用這個機制。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="bf6fc-126">使用案例和範例程式碼</span><span class="sxs-lookup"><span data-stu-id="bf6fc-126">Use cases and sample code</span></span>

<span data-ttu-id="bf6fc-127">下列程式碼示範金鑰更新作業的 accessCondition 檢查：</span><span class="sxs-lookup"><span data-stu-id="bf6fc-127">The following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="bf6fc-128">如果資源已不存在，則更新失敗</span><span class="sxs-lookup"><span data-stu-id="bf6fc-128">Fail an update if the resource no longer exists</span></span>
+ <span data-ttu-id="bf6fc-129">如果資源版本變更，則更新失敗</span><span class="sxs-lookup"><span data-stu-id="bf6fc-129">Fail an update if the resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="bf6fc-130">[DotNetETagsExplainer 程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) \(英文\) 的範例程式碼</span><span class="sxs-lookup"><span data-stu-id="bf6fc-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of the resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once the resource exists in Azure Search, its ETag will be populated. Make sure to use the object
            // returned by the SearchServiceClient! Otherwise, you will still have the old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that the update will only
            // succeed if the index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates to the same resource. If another
            // client tries to update the resource, it will fail as long as all clients are using the right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. To start, both clients see the same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates the index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries to update the index, but fails, thanks to the ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed to update the index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of the DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using the Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // the resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key to end application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="bf6fc-131">設計模式</span><span class="sxs-lookup"><span data-stu-id="bf6fc-131">Design pattern</span></span>

<span data-ttu-id="bf6fc-132">實作開放式同步存取的設計模式應包含重複嘗試存取條件檢查、測試存取條件，並選擇性擷取更新資源，然後再嘗試重新套用變更的迴圈。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-132">A design pattern for implementing optimistic concurrency should include a loop that retries the access condition check, a test for the access condition, and optionally retrieves an updated resource before attempting to re-apply the changes.</span></span> 

<span data-ttu-id="bf6fc-133">此程式碼片段說明如何將 synonymMap 新增至已存在的索引。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-133">This code snippet illustrates the addition of a synonymMap to an index that already exists.</span></span> <span data-ttu-id="bf6fc-134">此程式碼來自 [Azure 搜尋服務的同義字 (預覽) C# 教學課程](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk)。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-134">This code is from the [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="bf6fc-135">該程式碼片段會取得 "hotels" 索引，檢查更新作業的物件版本，在條件失敗的情況下擲回例外狀況，然後重試該作業 (最多三次)，並從自伺服器擷取索引以取得最新版本開始。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-135">The snippet gets the "hotels" index, checks the object version on an update operation, throws an exception if the condition fails, and then retries the operation (up to three times), starting with index retrieval from the server to get the latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // The IfNotChanged condition ensures that the index is updated only if the ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated the index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="bf6fc-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf6fc-136">Next steps</span></span>

<span data-ttu-id="bf6fc-137">如需如何安全地更新現有索引的詳細內容，請檢閱[同義字 C# 範例](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-137">Review the [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how to safely update an existing index.</span></span>

<span data-ttu-id="bf6fc-138">嘗試修改下列任一範例以包含 ETag 或 AccessCondition 物件。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-138">Try modifying either of the following samples to include ETags or AccessCondition objects.</span></span>

+ <span data-ttu-id="bf6fc-139">[Github 上的 REST API 範例](https://github.com/Azure-Samples/search-rest-api-getting-started) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="bf6fc-139">[REST API sample on Github](https://github.com/Azure-Samples/search-rest-api-getting-started)</span></span> 
+ <span data-ttu-id="bf6fc-140">[Github 上的 .NET SDK 範例](https://github.com/Azure-Samples/search-dotnet-getting-started) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="bf6fc-141">此解決方案包括「DotNetEtagsExplainer」專案，其中包含本文所提供的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bf6fc-141">This solution includes the "DotNetEtagsExplainer" project containing the code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="bf6fc-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bf6fc-142">See also</span></span>

  <span data-ttu-id="bf6fc-143">[常見 HTTP 要求與回應標頭](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   \(英文\)</span><span class="sxs-lookup"><span data-stu-id="bf6fc-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="bf6fc-144">[HTTP 狀態碼](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) \(英文\) [索引作業 (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="bf6fc-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>