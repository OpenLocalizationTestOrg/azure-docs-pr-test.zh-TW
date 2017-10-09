---
title: "aaaHow toomanage 並行寫入 tooresources 在 Azure 搜尋"
description: "使用開放式並行存取 tooavoid 中間空中衝突上的更新或刪除 tooAzure 搜尋索引、 索引子、 資料來源。"
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
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="7b58f-103">如何在 Azure 搜尋 toomanage 並行</span><span class="sxs-lookup"><span data-stu-id="7b58f-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="7b58f-104">管理 Azure 搜尋的資源，例如索引和資料來源時，重要 tooupdate 資源安全，特別是如果資源同時存取您的應用程式的不同元件。</span><span class="sxs-lookup"><span data-stu-id="7b58f-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="7b58f-105">當兩個用戶端在未經協調的情況下同時更新資源時，便可能發生競爭情形。</span><span class="sxs-lookup"><span data-stu-id="7b58f-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="7b58f-106">tooprevent，Azure 搜尋優惠*開放式並行存取模型*。</span><span class="sxs-lookup"><span data-stu-id="7b58f-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="7b58f-107">資源上不會有鎖定的情形。</span><span class="sxs-lookup"><span data-stu-id="7b58f-107">There are no locks on a resource.</span></span> <span data-ttu-id="7b58f-108">相反地，沒有 ETag 的覆寫識別 hello 資源版本，如此您就可以避免發生意外的要求建立每個資源。</span><span class="sxs-lookup"><span data-stu-id="7b58f-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="7b58f-109">[範例 C# 解決方案](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) \(英文\) 中的概念程式碼能說明 Azure 搜尋服務中並行控制的運作方式。</span><span class="sxs-lookup"><span data-stu-id="7b58f-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="7b58f-110">hello 程式碼會建立叫用並行控制的條件。</span><span class="sxs-lookup"><span data-stu-id="7b58f-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="7b58f-111">讀取 hello[下方的程式碼片段](#samplecode)就可能足以應付大部分的開發人員，但如果您想 toorun、 編輯 appsettings.json tooadd hello 服務名稱和管理員 api 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7b58f-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="7b58f-112">指定的服務 URL `http://myservice.search.windows.net`，hello 服務名稱是`myservice`。</span><span class="sxs-lookup"><span data-stu-id="7b58f-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="7b58f-113">運作方式</span><span class="sxs-lookup"><span data-stu-id="7b58f-113">How it works</span></span>

<span data-ttu-id="7b58f-114">開放式並行存取實作透過存取條件會檢查在撰寫 tooindexes、 索引子、 資料來源及 synonymMap 資源的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7b58f-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="7b58f-115">所有資源都有能提供物件版本資訊的[*實體標記 (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag)。</span><span class="sxs-lookup"><span data-stu-id="7b58f-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="7b58f-116">您可以藉由先檢查 hello ETag，避免並行更新的一般工作流程中取得、 在本機修改 (更新） 透過確保 hello 資源的 ETag 符合您的本機複本。</span><span class="sxs-lookup"><span data-stu-id="7b58f-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="7b58f-117">hello REST API 會使用[ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello 要求標頭上。</span><span class="sxs-lookup"><span data-stu-id="7b58f-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="7b58f-118">hello.NET SDK 設定透過 accessCondition 物件，並設定 hello hello ETag [If-match |如果-比對-無標頭](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)hello 資源上。</span><span class="sxs-lookup"><span data-stu-id="7b58f-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="7b58f-119">繼承自 [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) \(英文\) 的任何物件都具有 accessCondition 物件。</span><span class="sxs-lookup"><span data-stu-id="7b58f-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="7b58f-120">每次更新資源時，該資源的 ETag 都會自動變更。</span><span class="sxs-lookup"><span data-stu-id="7b58f-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="7b58f-121">當您實作並行管理時，您所做的所有放在前置條件需要 hello 遠端資源的 hello 更新要求 toohave hello hello hello 用戶端上修改過的 hello 資源複本為相同的 ETag。</span><span class="sxs-lookup"><span data-stu-id="7b58f-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="7b58f-122">如果並行處理序已變更 hello 遠端資源，hello ETag 不符 hello 前置條件和 HTTP 412 hello 要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="7b58f-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="7b58f-123">如果您使用 hello.NET SDK，這卻`CloudException`其中 hello`IsAccessConditionFailed()`擴充方法會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="7b58f-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="7b58f-124">並行只有一種機制。</span><span class="sxs-lookup"><span data-stu-id="7b58f-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="7b58f-125">無論資源更新是使用哪一種 API，都只會使用這個機制。</span><span class="sxs-lookup"><span data-stu-id="7b58f-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="7b58f-126">使用案例和範例程式碼</span><span class="sxs-lookup"><span data-stu-id="7b58f-126">Use cases and sample code</span></span>

<span data-ttu-id="7b58f-127">下列程式碼的 hello 示範 accessCondition 檢查索引鍵更新作業：</span><span class="sxs-lookup"><span data-stu-id="7b58f-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="7b58f-128">如果 hello 資源不存在，無法更新</span><span class="sxs-lookup"><span data-stu-id="7b58f-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="7b58f-129">如果 hello 資源版本變更，失敗的更新</span><span class="sxs-lookup"><span data-stu-id="7b58f-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="7b58f-130">[DotNetETagsExplainer 程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) \(英文\) 的範例程式碼</span><span class="sxs-lookup"><span data-stu-id="7b58f-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

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
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
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
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
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

## <a name="design-pattern"></a><span data-ttu-id="7b58f-131">設計模式</span><span class="sxs-lookup"><span data-stu-id="7b58f-131">Design pattern</span></span>

<span data-ttu-id="7b58f-132">實作開放式並行存取的設計模式應該包含迴圈，重試 hello 存取條件檢查，測試 hello 存取條件，並選擇性地擷取更新的資源嘗試 toore-套用 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="7b58f-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="7b58f-133">此程式碼片段說明 synonymMap tooan 索引已經存在的 hello 加法。</span><span class="sxs-lookup"><span data-stu-id="7b58f-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="7b58f-134">此程式碼取自 hello [Azure 搜尋的同義字 （預覽） C# 教學課程](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk)。</span><span class="sxs-lookup"><span data-stu-id="7b58f-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="7b58f-135">hello 片段取得 hello 「 旅館"索引、 檢查 hello 物件版本更新作業，如果 hello 條件失敗時，並再重試 hello 從索引擷取的 hello 伺服器 tooget hello 最新的作業 （向上 toothree 時間），會擲回例外狀況版本。</span><span class="sxs-lookup"><span data-stu-id="7b58f-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
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


## <a name="next-steps"></a><span data-ttu-id="7b58f-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b58f-136">Next steps</span></span>

<span data-ttu-id="7b58f-137">檢閱 hello[同義字 C# 範例](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms)toosafely 如何更新現有索引上的多個內容。</span><span class="sxs-lookup"><span data-stu-id="7b58f-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="7b58f-138">請嘗試修改 hello 下列任一取樣 tooinclude Etag 或 AccessCondition 物件。</span><span class="sxs-lookup"><span data-stu-id="7b58f-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ <span data-ttu-id="7b58f-139">[Github 上的 REST API 範例](https://github.com/Azure-Samples/search-rest-api-getting-started) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="7b58f-139">[REST API sample on Github](https://github.com/Azure-Samples/search-rest-api-getting-started)</span></span> 
+ <span data-ttu-id="7b58f-140">[Github 上的 .NET SDK 範例](https://github.com/Azure-Samples/search-dotnet-getting-started) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7b58f-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="7b58f-141">此解決方案包括包含 hello 本文章中呈現的程式碼的 hello"DotNetEtagsExplainer 」 專案。</span><span class="sxs-lookup"><span data-stu-id="7b58f-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="7b58f-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7b58f-142">See also</span></span>

  <span data-ttu-id="7b58f-143">[常見 HTTP 要求與回應標頭](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   \(英文\)</span><span class="sxs-lookup"><span data-stu-id="7b58f-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="7b58f-144">[HTTP 狀態碼](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) \(英文\) [索引作業 (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="7b58f-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>