---
title: "aaaHow toouse Azure 搜尋.NET 應用程式 |Microsoft 文件"
description: "如何從.NET 應用程式的 toouse Azure 搜尋"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="e36da-103">如何從.NET 應用程式的 toouse Azure 搜尋</span><span class="sxs-lookup"><span data-stu-id="e36da-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="e36da-104">這篇文章會逐步解說 tooget 您啟動並執行以 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)。</span><span class="sxs-lookup"><span data-stu-id="e36da-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="e36da-105">您可以使用 hello.NET SDK tooimplement 豐富您的應用程式使用 Azure Search 中搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="e36da-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="e36da-106">什麼是在 hello Azure 搜尋 SDK</span><span class="sxs-lookup"><span data-stu-id="e36da-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="e36da-107">hello SDK 包含用戶端程式庫`Microsoft.Azure.Search`。</span><span class="sxs-lookup"><span data-stu-id="e36da-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="e36da-108">您的索引、 資料來源和索引子，可讓您 toomanage，以及上傳和管理文件，並執行查詢，完全不需要包含 hello 細節的 HTTP 和 JSON toodeal。</span><span class="sxs-lookup"><span data-stu-id="e36da-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="e36da-109">hello 用戶端程式庫定義類別，例如`Index`， `Field`，和`Document`，以及等作業`Indexes.Create`和`Documents.Search`上 hello`SearchServiceClient`和`SearchIndexClient`類別。</span><span class="sxs-lookup"><span data-stu-id="e36da-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="e36da-110">這些類別會組織成下列命名空間的 hello:</span><span class="sxs-lookup"><span data-stu-id="e36da-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="e36da-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="e36da-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="e36da-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="e36da-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="e36da-113">現在上市 hello hello Azure 搜尋.NET SDK 目前版本。</span><span class="sxs-lookup"><span data-stu-id="e36da-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="e36da-114">如果您想要 tooprovide 意見反應對我們 tooincorporate hello 未來的版本，請造訪我們[意見反應頁面](https://feedback.azure.com/forums/263029-azure-search/)。</span><span class="sxs-lookup"><span data-stu-id="e36da-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="e36da-115">hello.NET SDK 支援的版本為`2016-09-01`的 hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="e36da-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="e36da-116">此版本現在包含自訂分析器支援及 Azure Blob 和 Azure 資料表索引子支援。</span><span class="sxs-lookup"><span data-stu-id="e36da-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="e36da-117">預覽功能*不*此版本中，例如支援 JSON 和 CSV 檔案編製索引的一部分位於[預覽](search-api-2015-02-28-preview.md)，而且可透過較舊的 hello [hello.NET SDK 2.0 preview 版本](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="e36da-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="e36da-118">此 SDK 不支援[管理作業](https://docs.microsoft.com/rest/api/searchmanagement/)，例如建立及調整搜尋服務和管理 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e36da-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="e36da-119">如果您需要 toomanage.NET 應用程式從您搜尋的資源，您可以使用 hello [Azure 搜尋.NET 管理 SDK](https://aka.ms/search-mgmt-sdk)。</span><span class="sxs-lookup"><span data-stu-id="e36da-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="e36da-120">Toohello hello SDK 最新版本升級</span><span class="sxs-lookup"><span data-stu-id="e36da-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="e36da-121">如果您已經使用較舊版本的 hello Azure 搜尋.NET SDK，而且您想要 tooupgrade toohello 正式推出新版、[本文](search-dotnet-sdk-migration.md)說明如何。</span><span class="sxs-lookup"><span data-stu-id="e36da-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="e36da-122">Hello SDK 的需求</span><span class="sxs-lookup"><span data-stu-id="e36da-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="e36da-123">Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="e36da-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="e36da-124">擁有 Azure Search 服務。</span><span class="sxs-lookup"><span data-stu-id="e36da-124">Your own Azure Search service.</span></span> <span data-ttu-id="e36da-125">在順序 toouse hello SDK，您將需要 hello 您的服務名稱和一或多個 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e36da-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="e36da-126">[Hello 入口網站中建立服務](search-create-service-portal.md)將協助您完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="e36da-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="e36da-127">下載 hello Azure 搜尋.NET SDK [NuGet 封裝](http://www.nuget.org/packages/Microsoft.Azure.Search)使用 Visual Studio 中的 管理 NuGet 封裝 」。</span><span class="sxs-lookup"><span data-stu-id="e36da-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="e36da-128">只要搜尋 hello 封裝名稱`Microsoft.Azure.Search`NuGet.org 上。</span><span class="sxs-lookup"><span data-stu-id="e36da-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="e36da-129">hello Azure 搜尋.NET SDK 支援以.NET Framework 4.6 hello 和.NET Core 為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e36da-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="e36da-130">核心案例</span><span class="sxs-lookup"><span data-stu-id="e36da-130">Core scenarios</span></span>
<span data-ttu-id="e36da-131">有幾件事，您將需要 toodo 搜尋應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e36da-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="e36da-132">本教學課程中涵蓋了這些主要情節：</span><span class="sxs-lookup"><span data-stu-id="e36da-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="e36da-133">建立索引</span><span class="sxs-lookup"><span data-stu-id="e36da-133">Creating an index</span></span>
* <span data-ttu-id="e36da-134">擴展文件以 hello 索引</span><span class="sxs-lookup"><span data-stu-id="e36da-134">Populating hello index with documents</span></span>
* <span data-ttu-id="e36da-135">使用全文檢索搜尋和篩選來搜尋文件</span><span class="sxs-lookup"><span data-stu-id="e36da-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="e36da-136">後面的 hello 範例程式碼將說明其中每一項。</span><span class="sxs-lookup"><span data-stu-id="e36da-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="e36da-137">您自己的應用程式中的可用 toouse hello 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e36da-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="e36da-138">概觀</span><span class="sxs-lookup"><span data-stu-id="e36da-138">Overview</span></span>
<span data-ttu-id="e36da-139">hello 會瀏覽我們的範例應用程式會建立新的名為 「 旅館"，索引填入幾個文件，則會執行一些搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="e36da-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="e36da-140">以下是 hello 主程式，顯示 hello 整體流程：</span><span class="sxs-lookup"><span data-stu-id="e36da-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="e36da-141">您可以找到 hello 範例應用程式上使用此逐步解說中的 hello 完整原始碼[GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)。</span><span class="sxs-lookup"><span data-stu-id="e36da-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="e36da-142">我們會逐步說明，</span><span class="sxs-lookup"><span data-stu-id="e36da-142">We'll walk through this step by step.</span></span> <span data-ttu-id="e36da-143">我們第一次需要新 toocreate `SearchServiceClient`。</span><span class="sxs-lookup"><span data-stu-id="e36da-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="e36da-144">此物件可讓您 toomanage 索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="e36da-145">其中一個順序 tooconstruct，您需要 tooprovide 您的 Azure 搜尋服務名稱，以及管理 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e36da-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="e36da-146">您可以輸入此資訊在 hello`appsettings.json`檔案的 hello[範例應用程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)。</span><span class="sxs-lookup"><span data-stu-id="e36da-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="e36da-147">如果您提供正確的索引鍵 （例如，查詢索引鍵管理金鑰所需的位置），hello`SearchServiceClient`將會擲回`CloudException`hello 錯誤訊息 「 禁止 」 hello 與第一次您呼叫作業方法，例如`Indexes.Create`。</span><span class="sxs-lookup"><span data-stu-id="e36da-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="e36da-148">如果發生這種情況 tooyou，請仔細檢查我們的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e36da-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="e36da-149">hello 接下來的幾個幾行呼叫方法 toocreate 名為 「 旅館 」，必須先刪除它，如果已經存在的索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="e36da-150">稍後我們會逐項執行這些方法。</span><span class="sxs-lookup"><span data-stu-id="e36da-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="e36da-151">接下來，hello 索引需要 toobe 填入。</span><span class="sxs-lookup"><span data-stu-id="e36da-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="e36da-152">toodo，我們需要`SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="e36da-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="e36da-153">有兩種方式 tooobtain 其中一個： 建構，或呼叫`Indexes.GetClient`上 hello `SearchServiceClient`。</span><span class="sxs-lookup"><span data-stu-id="e36da-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="e36da-154">我們為了方便起見使用後者 hello。</span><span class="sxs-lookup"><span data-stu-id="e36da-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="e36da-155">在一般搜尋應用程式中，索引的管理和填入是由搜尋查詢的個別元件所處理。</span><span class="sxs-lookup"><span data-stu-id="e36da-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="e36da-156">`Indexes.GetClient`填入索引，因為它會將儲存您的方便 hello 提供另一個問題`SearchCredentials`。</span><span class="sxs-lookup"><span data-stu-id="e36da-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="e36da-157">其做法是傳遞 hello 管理金鑰，您使用的 toocreate hello `SearchServiceClient` toohello 新`SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="e36da-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="e36da-158">不過，在 hello 部分中執行查詢的應用程式，它是較佳的 toocreate hello`SearchIndexClient`直接，讓您可以傳入的查詢索引鍵，而不是管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="e36da-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="e36da-159">這是與 hello 最低權限原則一致，而且可協助您更安全的應用程式 toomake。</span><span class="sxs-lookup"><span data-stu-id="e36da-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="e36da-160">您可以 [在這裡](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization)深入了解系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="e36da-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="e36da-161">現在，我們已經`SearchIndexClient`，我們可以擴展 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="e36da-162">這要使用另一個方法來執行，稍後我們會逐項說明。</span><span class="sxs-lookup"><span data-stu-id="e36da-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="e36da-163">最後，我們會執行幾個搜尋查詢，並顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e36da-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="e36da-164">這次我們使用不同的 `SearchIndexClient`：</span><span class="sxs-lookup"><span data-stu-id="e36da-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="e36da-165">我們要探討 hello`RunQueries`稍後方法。</span><span class="sxs-lookup"><span data-stu-id="e36da-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="e36da-166">以下是新 hello 程式碼 toocreate hello `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="e36da-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="e36da-167">這次我們使用的查詢索引鍵，因為我們不需要寫入權限 toohello 索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="e36da-168">您可以輸入此資訊在 hello`appsettings.json`檔案的 hello[範例應用程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)。</span><span class="sxs-lookup"><span data-stu-id="e36da-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="e36da-169">如果您執行此應用程式具有有效的服務名稱和 API 金鑰，hello 輸出看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="e36da-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="e36da-170">這篇文章的 hello 結尾會提供 hello 完整 hello 應用程式的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="e36da-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="e36da-171">接下來，我們將接受 hello 所呼叫的方法進一步檢視`Main`。</span><span class="sxs-lookup"><span data-stu-id="e36da-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="e36da-172">建立索引</span><span class="sxs-lookup"><span data-stu-id="e36da-172">Creating an index</span></span>
<span data-ttu-id="e36da-173">在建立之後`SearchServiceClient`下, 一步 hello`Main`未是刪除 hello 「 旅館"的索引，如果已經存在。</span><span class="sxs-lookup"><span data-stu-id="e36da-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="e36da-174">是由下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="e36da-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="e36da-175">這個方法會使用指定的 hello `SearchServiceClient` toocheck 如果 hello 索引存在，而且如果是，刪除它。</span><span class="sxs-lookup"><span data-stu-id="e36da-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-176">這篇文章中的 hello 範例程式碼為了簡單起見使用 hello Azure 搜尋.NET SDK 的 hello 同步方法。</span><span class="sxs-lookup"><span data-stu-id="e36da-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="e36da-177">我們建議您在自己的應用程式 tookeep 使用 hello 非同步方法加以擴充且回應迅速。</span><span class="sxs-lookup"><span data-stu-id="e36da-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="e36da-178">例如，在 hello 方法，您可以使用`ExistsAsync`和`DeleteAsync`而不是`Exists`和`Delete`。</span><span class="sxs-lookup"><span data-stu-id="e36da-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="e36da-179">接著，`Main` 會呼叫此方法建立新的 "hotels" 索引：</span><span class="sxs-lookup"><span data-stu-id="e36da-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="e36da-180">這個方法會建立新`Index`物件及一串`Field`定義 hello hello 新索引的結構描述的物件。</span><span class="sxs-lookup"><span data-stu-id="e36da-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="e36da-181">每個欄位均有一個名稱、資料類型和一些屬性，以用於定義欄位的搜尋行為。</span><span class="sxs-lookup"><span data-stu-id="e36da-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="e36da-182">hello`FieldBuilder`類別會使用反映 toocreate 一份`Field`hello 索引藉由檢查物件 hello 公用屬性和屬性的指定 hello`Hotel`模型類別。</span><span class="sxs-lookup"><span data-stu-id="e36da-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="e36da-183">我們將探討 hello`Hotel`稍後類別。</span><span class="sxs-lookup"><span data-stu-id="e36da-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-184">您一律可以建立 hello 清單`Field`物件，而使用非直接`FieldBuilder`視。</span><span class="sxs-lookup"><span data-stu-id="e36da-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="e36da-185">例如，您可能不想 toouse 模型類別，或您可能需要 toouse 現有的模型類別，您不想 toomodify 藉由加入屬性。</span><span class="sxs-lookup"><span data-stu-id="e36da-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="e36da-186">此外 toofields，您也可以新增評分設定檔、 建議工具或 CORS 選項 toohello （省略來自 hello 範例為求簡潔） 的索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="e36da-187">您可以找到 hello Index 物件和毛利的構成部分的詳細資訊，在 hello [SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index)，同時也 hello [Azure 搜尋 REST API 參考](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="e36da-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="e36da-188">擴展 hello 索引</span><span class="sxs-lookup"><span data-stu-id="e36da-188">Populating hello index</span></span>
<span data-ttu-id="e36da-189">中的下一個步驟 hello `Main` toopopulate hello 新建的索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="e36da-190">這是 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="e36da-190">This is done in hello following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="e36da-191">此方法分四個部分。</span><span class="sxs-lookup"><span data-stu-id="e36da-191">This method has four parts.</span></span> <span data-ttu-id="e36da-192">hello 會先建立的陣列`Hotel`將做為輸入的資料 tooupload toohello 索引的物件。</span><span class="sxs-lookup"><span data-stu-id="e36da-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="e36da-193">為簡單起見，此資料採硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="e36da-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="e36da-194">在您的應用程式中，資料可能會來自像是 SQL 資料庫的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="e36da-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="e36da-195">hello 第二個部分會建立`IndexBatch`包含 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="e36da-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="e36da-196">您指定要在您建立，在此情況下所呼叫的 hello 階段 tooapply toohello 批次的 hello 作業`IndexBatch.Upload`。</span><span class="sxs-lookup"><span data-stu-id="e36da-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="e36da-197">hello 批次則上傳的 toohello Azure 搜尋索引 hello`Documents.Index`方法。</span><span class="sxs-lookup"><span data-stu-id="e36da-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-198">在此範例中，我們只上傳文件。</span><span class="sxs-lookup"><span data-stu-id="e36da-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="e36da-199">如果您想 toomerge 變更為現有的文件或刪除文件，您可以藉由呼叫來建立批次`IndexBatch.Merge`， `IndexBatch.MergeOrUpload`，或`IndexBatch.Delete`改為。</span><span class="sxs-lookup"><span data-stu-id="e36da-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="e36da-200">您也可以藉由呼叫混合不同的作業，以單一批次`IndexBatch.New`，其可接受的集合`IndexAction`物件，其中每個會告訴 Azure 搜尋 tooperform 文件上的特定作業。</span><span class="sxs-lookup"><span data-stu-id="e36da-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="e36da-201">您可以建立每個`IndexAction`與它自己的作業，透過呼叫 hello 對應的方法，例如`IndexAction.Merge`， `IndexAction.Upload`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="e36da-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="e36da-202">hello 第三個部分，這個方法是處理編製索引的重要的錯誤案例的 catch 區塊。</span><span class="sxs-lookup"><span data-stu-id="e36da-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="e36da-203">如果您的 Azure 搜尋服務失敗的 tooindex hello 的批次中的 hello 某些文件`IndexBatchException`，所擲回`Documents.Index`。</span><span class="sxs-lookup"><span data-stu-id="e36da-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="e36da-204">如果您在服務負載過重時編制文件的索引，就會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="e36da-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="e36da-205">**我們強烈建議您在程式碼中明確處理此情況。**</span><span class="sxs-lookup"><span data-stu-id="e36da-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="e36da-206">您可以延遲，然後重試失敗，索引 hello 文件或您可以記錄並繼續像 hello 範例會執行，或者，您可以執行根據您的應用程式資料的一致性需求的其他項目。</span><span class="sxs-lookup"><span data-stu-id="e36da-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-207">您可以使用 hello`FindFailedActionsToRetry`方法 tooconstruct 新批次包含只 hello 過先前的呼叫失敗的動作`Index`。</span><span class="sxs-lookup"><span data-stu-id="e36da-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="e36da-208">已記錄 hello 方法[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_)，而且沒有 tooproperly 如何使用它的討論[在 StackOverflow 上](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry)。</span><span class="sxs-lookup"><span data-stu-id="e36da-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="e36da-209">最後，hello`UploadDocuments`方法兩秒鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="e36da-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="e36da-210">索引會發生以非同步方式在 Azure 搜尋服務中，所以 hello 範例應用程式需要 toowait hello 文件可供搜尋簡短時間 tooensure。</span><span class="sxs-lookup"><span data-stu-id="e36da-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="e36da-211">通常只有在示範、測試和範例應用程式中，才需要這類延遲。</span><span class="sxs-lookup"><span data-stu-id="e36da-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="e36da-212">Hello.NET SDK 的文件的處理方式</span><span class="sxs-lookup"><span data-stu-id="e36da-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="e36da-213">您可能想知道 hello Azure 搜尋.NET SDK 無法 tooupload 之類的使用者定義的類別執行個體的方式`Hotel`toohello 索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="e36da-214">toohelp 回答這個問題，讓我們看看 hello`Hotel`類別：</span><span class="sxs-lookup"><span data-stu-id="e36da-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="e36da-215">hello 首先 toonotice 在於每一個公用屬性的`Hotel`對應 tooa 欄位在 hello 索引定義中，但有一點很重要： hello 名稱的每個公開時 hello 每個欄位的名稱會以小寫字母 （「 camel 命名法的情況"），啟動屬性`Hotel`開頭的大寫字母 （「 Pascal 大小寫 」）。</span><span class="sxs-lookup"><span data-stu-id="e36da-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="e36da-216">這是常見的案例中執行資料繫結其中 hello 目標結構描述是控制外部 hello hello 應用程式開發人員的.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e36da-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="e36da-217">而不是讓 tooviolate hello.NET 命名指導方針進行屬性名稱依照 camel 命名法的情況下，您可以告訴 hello SDK toomap hello 屬性名稱 toocamel 案例會自動以 hello`[SerializePropertyNamesAsCamelCase]`屬性。</span><span class="sxs-lookup"><span data-stu-id="e36da-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-218">hello Azure 搜尋.NET SDK 會使用 hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize 程式庫和您自訂的模型物件 tooand，從 JSON 還原序列化。</span><span class="sxs-lookup"><span data-stu-id="e36da-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="e36da-219">如有需要，您可以自訂這個序列化的過程。</span><span class="sxs-lookup"><span data-stu-id="e36da-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="e36da-220">如需詳細資訊，請參閱[使用 JSON.NET 自訂序列化](#JsonDotNet)。</span><span class="sxs-lookup"><span data-stu-id="e36da-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="e36da-221">hello 第二個東西 toonotice 是 hello 屬性例如`IsFilterable`， `IsSearchable`， `Key`，和`Analyzer`，裝飾每個公用屬性。</span><span class="sxs-lookup"><span data-stu-id="e36da-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="e36da-222">這些屬性都會直接對應 toohello [hello Azure 搜尋索引的對應屬性](https://docs.microsoft.com/rest/api/searchservice/create-index#request)。</span><span class="sxs-lookup"><span data-stu-id="e36da-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="e36da-223">hello`FieldBuilder`類別會使用這些 tooconstruct 欄位定義 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="e36da-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="e36da-224">hello 第三個重要的是有關 hello`Hotel`類別是 hello hello 公用屬性資料類型。</span><span class="sxs-lookup"><span data-stu-id="e36da-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="e36da-225">這些屬性的 hello.NET 型別對應 tootheir hello 索引定義中的對等的欄位類型。</span><span class="sxs-lookup"><span data-stu-id="e36da-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="e36da-226">例如，hello`Category`字串屬性會對應 toohello`category`欄位的型別`Edm.String`。</span><span class="sxs-lookup"><span data-stu-id="e36da-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="e36da-227">有類似的型別對應之間`bool?`和`Edm.Boolean`，`DateTimeOffset?`和`Edm.DateTimeOffset`，等 hello 特定規則的 hello 型別對應都會記錄以 hello`Documents.Get`方法在 hello [Azure 搜尋.NET SDK參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)。</span><span class="sxs-lookup"><span data-stu-id="e36da-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="e36da-228">hello`FieldBuilder`類別會負責這項對應，但仍然可以很有幫助 toounderstand 以防您需要 tootroubleshoot 序列化的任何問題。</span><span class="sxs-lookup"><span data-stu-id="e36da-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="e36da-229">此功能 toouse 雙向; 運作自己的類別為文件您也可以擷取搜尋結果，且擁有 hello SDK 自動還原序列化它們 tooa 類型的您的選擇，我們將會看到 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="e36da-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-230">hello Azure 搜尋.NET SDK 也支援動態具類型的文件使用 hello`Document`類別，這是索引鍵/值對應的欄位名稱 toofield 值。</span><span class="sxs-lookup"><span data-stu-id="e36da-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="e36da-231">您不知道 hello 索引結構描述在設計階段，或者它會是很不方便 toobind toospecific 模型類別，這是非常實用。</span><span class="sxs-lookup"><span data-stu-id="e36da-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="e36da-232">中的所有 hello 方法 hello SDK 文件處理都具有多載，搭配 hello`Document`類別，以及接受泛型型別參數的強型別多載。</span><span class="sxs-lookup"><span data-stu-id="e36da-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="e36da-233">只有 hello 後者可用在 hello 範例程式碼在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="e36da-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="e36da-234">hello`Document`類別繼承自`Dictionary<string, object>`。</span><span class="sxs-lookup"><span data-stu-id="e36da-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="e36da-235">如需其他詳細資訊，請前往[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document)。</span><span class="sxs-lookup"><span data-stu-id="e36da-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="e36da-236">**為什麼您應該使用 Nullable 資料類型**</span><span class="sxs-lookup"><span data-stu-id="e36da-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="e36da-237">當設計您的模型類別 toomap tooan Azure 搜尋索引，我們建議您宣告實值類型的屬性，例如`bool`和`int`toobe 可為 null (例如，`bool?`而不是`bool`)。</span><span class="sxs-lookup"><span data-stu-id="e36da-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="e36da-238">如果您使用非 null 的屬性，您有太**保證**沒有文件索引中的包含 hello 對應欄位的 null 值。</span><span class="sxs-lookup"><span data-stu-id="e36da-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="e36da-239">Hello SDK 都 hello Azure 搜尋服務可協助您 tooenforce 這。</span><span class="sxs-lookup"><span data-stu-id="e36da-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="e36da-240">這不只是假設性的問題： 想像一下，讓您加入新欄位 tooan 現有索引型別的`Edm.Int32`。</span><span class="sxs-lookup"><span data-stu-id="e36da-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="e36da-241">在更新之後 hello 索引定義，所有文件必須針對該新欄位的 null 值 （因為所有類型都是可為 null 的 Azure 搜尋）。</span><span class="sxs-lookup"><span data-stu-id="e36da-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="e36da-242">若您搭配不可為 null，然後使用模型類別`int`該欄位的屬性，您會收到`JsonSerializationException`tooretrieve 文件時，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="e36da-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="e36da-243">因此，我們建議您在模型類別中使用可為 Null 的類型，來做為最佳作法。</span><span class="sxs-lookup"><span data-stu-id="e36da-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="e36da-244">使用 JSON.NET 自訂序列化</span><span class="sxs-lookup"><span data-stu-id="e36da-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="e36da-245">hello SDK 會使用 JSON.NET 進行序列化和還原序列化文件。</span><span class="sxs-lookup"><span data-stu-id="e36da-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="e36da-246">您可以自訂序列化和還原序列化如有需要定義您自己`JsonConverter`或`IContractResolver`(請參閱 hello [JSON.NET 文件](http://www.newtonsoft.com/json/help/html/Introduction.htm)如需詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="e36da-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="e36da-247">當您想 tooadapt 現有的模型類別，從您的應用程式與 Azure 搜尋中，以及其他更進階的案例搭配使用時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="e36da-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="e36da-248">例如，使用自訂序列化，您可以：</span><span class="sxs-lookup"><span data-stu-id="e36da-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="e36da-249">包含或排除模型類別的特定屬性儲存為文件欄位。</span><span class="sxs-lookup"><span data-stu-id="e36da-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="e36da-250">在程式碼的屬性名稱和索引的欄位名稱之間進行對應。</span><span class="sxs-lookup"><span data-stu-id="e36da-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="e36da-251">建立可用於將屬性 toodocument 欄位對應的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="e36da-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="e36da-252">您可以找到 hello GitHub 上的 Azure 搜尋.NET SDK 的 hello 單元測試中實作自訂序列化的範例。</span><span class="sxs-lookup"><span data-stu-id="e36da-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="e36da-253">[這個資料夾](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models)是好的起點。</span><span class="sxs-lookup"><span data-stu-id="e36da-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="e36da-254">它包含 hello 自訂序列化測試所使用的類別。</span><span class="sxs-lookup"><span data-stu-id="e36da-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="e36da-255">搜尋文件以 hello 索引</span><span class="sxs-lookup"><span data-stu-id="e36da-255">Searching for documents in hello index</span></span>
<span data-ttu-id="e36da-256">hello hello 範例應用程式中的最後一個步驟是 toosearch hello 索引中的某些文件。</span><span class="sxs-lookup"><span data-stu-id="e36da-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="e36da-257">hello 下列方法會執行此動作：</span><span class="sxs-lookup"><span data-stu-id="e36da-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="e36da-258">每次執行查詢時，這個方法都會先建立新的 `SearchParameters` 物件。</span><span class="sxs-lookup"><span data-stu-id="e36da-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="e36da-259">這是使用的 toospecify hello 查詢，例如排序、 篩選、 分頁和 faceting 的其他選項。</span><span class="sxs-lookup"><span data-stu-id="e36da-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="e36da-260">在此方法中，我們正在設定 hello `Filter`， `Select`， `OrderBy`，和`Top`不同查詢的屬性。</span><span class="sxs-lookup"><span data-stu-id="e36da-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="e36da-261">所有的 hello`SearchParameters`屬性會記載[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters)。</span><span class="sxs-lookup"><span data-stu-id="e36da-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="e36da-262">hello 下一個步驟是 tooactually 執行 hello 搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="e36da-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="e36da-263">這是使用 hello`Documents.Search`方法。</span><span class="sxs-lookup"><span data-stu-id="e36da-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="e36da-264">針對每個查詢中，我們傳遞為字串 hello 搜尋文字 toouse (或`"*"`如果沒有任何搜尋文字)，再加上 hello 搜尋稍早建立的參數。</span><span class="sxs-lookup"><span data-stu-id="e36da-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="e36da-265">我們也指定`Hotel`hello 型別參數為`Documents.Search`，hello 搜尋結果中向 hello SDK toodeserialize 文件類型的物件至`Hotel`。</span><span class="sxs-lookup"><span data-stu-id="e36da-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="e36da-266">您可以找到有關 hello 搜尋查詢運算式語法的詳細資訊[這裡](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)。</span><span class="sxs-lookup"><span data-stu-id="e36da-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="e36da-267">最後，在每個查詢之後這個方法逐一查看所有 hello 相符項目在 hello 搜尋結果中，列印每個文件 toohello 主控台：</span><span class="sxs-lookup"><span data-stu-id="e36da-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="e36da-268">接著我們探討每個 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="e36da-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="e36da-269">以下是 hello 程式碼 tooexecute hello 第一個查詢：</span><span class="sxs-lookup"><span data-stu-id="e36da-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="e36da-270">在此情況下，我們要搜尋飯店符合 hello word"budget"，而且我們想 tooget 只傳回 hello 飯店名稱，為指定的 hello`Select`參數。</span><span class="sxs-lookup"><span data-stu-id="e36da-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="e36da-271">Hello 結果如下：</span><span class="sxs-lookup"><span data-stu-id="e36da-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="e36da-272">接下來，我們想要每晚率小於 $150 toofind hello 旅館，只能傳回 hello 旅館識別碼和描述：</span><span class="sxs-lookup"><span data-stu-id="e36da-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="e36da-273">此查詢會使用 OData`$filter`運算式`baseRate lt 150`，toofilter hello hello 索引文件。</span><span class="sxs-lookup"><span data-stu-id="e36da-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="e36da-274">您可以進一步了解 Azure 搜尋支援的 OData 語法 hello[這裡](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)。</span><span class="sxs-lookup"><span data-stu-id="e36da-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="e36da-275">以下是 hello hello 查詢結果：</span><span class="sxs-lookup"><span data-stu-id="e36da-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="e36da-276">接下來，我們想 toofind hello 前兩個旅館，最近重新裝修，並顯示 hello 飯店名稱和最後一個 renovation 日期。</span><span class="sxs-lookup"><span data-stu-id="e36da-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="e36da-277">Hello 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="e36da-277">Here is hello code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="e36da-278">在此情況下，我們一次使用 OData 語法 toospecify hello`OrderBy`參數做為`lastRenovationDate desc`。</span><span class="sxs-lookup"><span data-stu-id="e36da-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="e36da-279">我們也將設定`Top`too2 tooensure 我們只能取得 hello 前兩個文件。</span><span class="sxs-lookup"><span data-stu-id="e36da-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="e36da-280">之前，我們設定`Select`toospecify 應傳回哪些欄位。</span><span class="sxs-lookup"><span data-stu-id="e36da-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="e36da-281">Hello 結果如下：</span><span class="sxs-lookup"><span data-stu-id="e36da-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="e36da-282">最後，我們想 toofind hello 字"motel"相符的所有旅館：</span><span class="sxs-lookup"><span data-stu-id="e36da-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="e36da-283">以下是 hello 結果，包含所有欄位，因為我們並未指定 hello 和`Select`屬性：</span><span class="sxs-lookup"><span data-stu-id="e36da-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="e36da-284">這個步驟會完成 hello 教學課程中，但不在此停止。</span><span class="sxs-lookup"><span data-stu-id="e36da-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="e36da-285">**後續步驟** 會提供可深入了解 Azure 搜尋服務的其他資源。</span><span class="sxs-lookup"><span data-stu-id="e36da-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e36da-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e36da-286">Next steps</span></span>
* <span data-ttu-id="e36da-287">瀏覽 hello 的 hello 參考[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)和[REST API](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="e36da-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="e36da-288">使用 [影片與其他範例和教學課程](search-video-demo-tutorial-list.md)加深知識。</span><span class="sxs-lookup"><span data-stu-id="e36da-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="e36da-289">檢閱[命名慣例](https://docs.microsoft.com/rest/api/searchservice/Naming-rules)toolearn hello 規則命名各種物件。</span><span class="sxs-lookup"><span data-stu-id="e36da-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="e36da-290">檢閱 Azure 搜尋服務 [支援的資料類型](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 。</span><span class="sxs-lookup"><span data-stu-id="e36da-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
