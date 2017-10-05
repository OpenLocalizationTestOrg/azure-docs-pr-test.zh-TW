---
title: "如何從 .NET 應用程式使用 Azure 搜尋服務 | Microsoft Docs"
description: "如何從 .NET 應用程式使用 Azure 搜尋服務"
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
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="02ce1-103">如何從 .NET 應用程式使用 Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="02ce1-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="02ce1-104">本文會逐步指引您學會如何使用 [Azure 搜尋服務 .NET SDK](https://aka.ms/search-sdk)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="02ce1-105">您可以透過 .NET SDK，利用 Azure 搜尋服務在應用程式中實作豐富的搜尋經驗。</span><span class="sxs-lookup"><span data-stu-id="02ce1-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="02ce1-106">Azure 搜尋服務 SDK 中有哪些內容</span><span class="sxs-lookup"><span data-stu-id="02ce1-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="02ce1-107">SDK 包含用戶端程式庫 `Microsoft.Azure.Search`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="02ce1-108">該程式庫可讓您管理索引、資料來源及索引子，以及更新和管理文件，還可以執行查詢，而且一律不需要處理 HTTP 和 JSON 的細節。</span><span class="sxs-lookup"><span data-stu-id="02ce1-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="02ce1-109">用戶端程式庫會定義類別，例如 `Index`、`Field` 及 `Document`，以及定義作業，例如 `SearchServiceClient` 和 `SearchIndexClient` 類別上的 `Indexes.Create` 和 `Documents.Search`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="02ce1-110">這些類別可編成以下命名空間：</span><span class="sxs-lookup"><span data-stu-id="02ce1-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="02ce1-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="02ce1-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="02ce1-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="02ce1-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="02ce1-113">目前的 Azure 搜尋服務 .NET SDK 版本現在正式推出。</span><span class="sxs-lookup"><span data-stu-id="02ce1-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="02ce1-114">如果您想提供意見反應給我們，讓我們可以將您的意見併入下一個版本中，請瀏覽我們的 [意見回應頁面](https://feedback.azure.com/forums/263029-azure-search/)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="02ce1-115">.NET SDK 支援 `2016-09-01` 版的 [Azure 搜尋服務 REST API](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="02ce1-116">此版本現在包含自訂分析器支援及 Azure Blob 和 Azure 資料表索引子支援。</span><span class="sxs-lookup"><span data-stu-id="02ce1-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="02ce1-117">「不」屬於此版本的預覽功能 (例如 JSON 和 CSV 檔案編製索引支援) 處於[預覽](search-api-2015-02-28-preview.md)狀態，並可透過較舊的 [2.0 預覽版 .NET SDK](https://aka.ms/search-sdk-preview) 取得。</span><span class="sxs-lookup"><span data-stu-id="02ce1-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="02ce1-118">此 SDK 不支援[管理作業](https://docs.microsoft.com/rest/api/searchmanagement/)，例如建立及調整搜尋服務和管理 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="02ce1-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="02ce1-119">如果您需要從 .NET 應用程式管理搜尋資源，您可以使用 [Azure 搜尋服務 .NET 管理 SDK](https://aka.ms/search-mgmt-sdk)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="02ce1-120">升級到最新版本的 SDK</span><span class="sxs-lookup"><span data-stu-id="02ce1-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="02ce1-121">如果您已經在使用舊版的 Azure 搜尋服務 .NET SDK，而您想要升級至新的正式推出版本， [這篇文章](search-dotnet-sdk-migration.md) 會說明如何進行。</span><span class="sxs-lookup"><span data-stu-id="02ce1-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="02ce1-122">SDK 的需求</span><span class="sxs-lookup"><span data-stu-id="02ce1-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="02ce1-123">Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="02ce1-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="02ce1-124">擁有 Azure Search 服務。</span><span class="sxs-lookup"><span data-stu-id="02ce1-124">Your own Azure Search service.</span></span> <span data-ttu-id="02ce1-125">為了使用 SDK，您需要為服務命名，還需要一或多個 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="02ce1-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="02ce1-126">[在入口網站建立服務](search-create-service-portal.md) 可協助您執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="02ce1-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="02ce1-127">使用 Visual Studio 中的 [管理 NuGet 封裝] 下載 Azure 搜尋服務 .NET SDK [NuGet 封裝](http://www.nuget.org/packages/Microsoft.Azure.Search) 。</span><span class="sxs-lookup"><span data-stu-id="02ce1-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="02ce1-128">只要在 NuGet.org 上搜尋封裝名稱 `Microsoft.Azure.Search` 即可。</span><span class="sxs-lookup"><span data-stu-id="02ce1-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="02ce1-129">Azure 搜尋服務 .NET SDK 支援以 .NET Framework 4.6 和 .NET Core 為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="02ce1-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="02ce1-130">核心案例</span><span class="sxs-lookup"><span data-stu-id="02ce1-130">Core scenarios</span></span>
<span data-ttu-id="02ce1-131">您必須在搜尋應用程式中執行一些作業。</span><span class="sxs-lookup"><span data-stu-id="02ce1-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="02ce1-132">本教學課程中涵蓋了這些主要情節：</span><span class="sxs-lookup"><span data-stu-id="02ce1-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="02ce1-133">建立索引</span><span class="sxs-lookup"><span data-stu-id="02ce1-133">Creating an index</span></span>
* <span data-ttu-id="02ce1-134">透過文件填入索引</span><span class="sxs-lookup"><span data-stu-id="02ce1-134">Populating the index with documents</span></span>
* <span data-ttu-id="02ce1-135">使用全文檢索搜尋和篩選來搜尋文件</span><span class="sxs-lookup"><span data-stu-id="02ce1-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="02ce1-136">這些情節的說明都隨附範例程式碼，</span><span class="sxs-lookup"><span data-stu-id="02ce1-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="02ce1-137">歡迎在您的應用程式中使用這些程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="02ce1-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="02ce1-138">Overview</span><span class="sxs-lookup"><span data-stu-id="02ce1-138">Overview</span></span>
<span data-ttu-id="02ce1-139">我們將探索的範例應用程式，會建立名為 "hotels" 的新索引，並透過一些文件填入索引，然後執行一些搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="02ce1-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="02ce1-140">以下是主要程式，該程式顯示了整體流程：</span><span class="sxs-lookup"><span data-stu-id="02ce1-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="02ce1-141">您可以在 [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo) 上尋找本逐步解說中所用範例應用程式的完整原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="02ce1-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="02ce1-142">我們會逐步說明，</span><span class="sxs-lookup"><span data-stu-id="02ce1-142">We'll walk through this step by step.</span></span> <span data-ttu-id="02ce1-143">首先必須建立新的 `SearchServiceClient`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="02ce1-144">此物件可讓您管理索引。</span><span class="sxs-lookup"><span data-stu-id="02ce1-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="02ce1-145">若要建構此物件，必須提供 Azure Search 服務名稱和系統管理 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="02ce1-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="02ce1-146">您可以在[範例應用程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)的 `appsettings.json` 檔案中輸入這項資訊。</span><span class="sxs-lookup"><span data-stu-id="02ce1-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="02ce1-147">如果提供不正確的金鑰 (例如，需要系統管理金鑰卻提供查詢金鑰)，則 `SearchServiceClient` 會在您第一次用它呼叫作業方法時 (例如 `Indexes.Create`) 擲回 `CloudException`，並附上「禁止」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="02ce1-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="02ce1-148">如果遇到此情況，請按兩下我們的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="02ce1-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="02ce1-149">以下幾行程式碼會呼叫建立名為 "hotels" 索引的方法，如果索引已存在，請加以刪除。</span><span class="sxs-lookup"><span data-stu-id="02ce1-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="02ce1-150">稍後我們會逐項執行這些方法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="02ce1-151">接著必須填入索引。</span><span class="sxs-lookup"><span data-stu-id="02ce1-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="02ce1-152">若要這麼做，必須要有 `SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="02ce1-153">取得的方式有兩種：建構該項目，或用 `SearchServiceClient` 呼叫 `Indexes.GetClient`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="02ce1-154">為方便起見，我們使用後者。</span><span class="sxs-lookup"><span data-stu-id="02ce1-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="02ce1-155">在一般搜尋應用程式中，索引的管理和填入是由搜尋查詢的個別元件所處理。</span><span class="sxs-lookup"><span data-stu-id="02ce1-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="02ce1-156">`Indexes.GetClient` 可以很輕易填入索引，因為它可以節省提供其他 `SearchCredentials` 的麻煩。</span><span class="sxs-lookup"><span data-stu-id="02ce1-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="02ce1-157">執行方法是將用於建立 `SearchServiceClient` 的系統管理金鑰傳遞至新的 `SearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="02ce1-158">但在執行查詢的應用程式中，最好直接建立 `SearchIndexClient` ，如此一來就可以傳遞查詢金鑰，而非系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="02ce1-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="02ce1-159">這不但符合最低權限的準則，也可以讓您的應用程式更安全。</span><span class="sxs-lookup"><span data-stu-id="02ce1-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="02ce1-160">您可以 [在這裡](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization)深入了解系統管理金鑰和查詢金鑰。</span><span class="sxs-lookup"><span data-stu-id="02ce1-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="02ce1-161">現在我們有 `SearchIndexClient`，可以開始填入索引。</span><span class="sxs-lookup"><span data-stu-id="02ce1-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="02ce1-162">這要使用另一個方法來執行，稍後我們會逐項說明。</span><span class="sxs-lookup"><span data-stu-id="02ce1-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="02ce1-163">最後，我們會執行一些搜尋查詢並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="02ce1-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="02ce1-164">這次我們使用不同的 `SearchIndexClient`：</span><span class="sxs-lookup"><span data-stu-id="02ce1-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="02ce1-165">我們稍後會仔細查看 `RunQueries` 方法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="02ce1-166">以下是可建立新 `SearchIndexClient` 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="02ce1-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="02ce1-167">這次我們使用查詢金鑰，因為我們不需要索引的寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="02ce1-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="02ce1-168">您可以在[範例應用程式](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)的 `appsettings.json` 檔案中輸入這項資訊。</span><span class="sxs-lookup"><span data-stu-id="02ce1-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="02ce1-169">如果使用有效的服務名稱和 API 金鑰執行此應用程式，則輸出應該會看起來如下：</span><span class="sxs-lookup"><span data-stu-id="02ce1-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="02ce1-170">本文結尾會提供完整的應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="02ce1-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="02ce1-171">接著，我們要進一步了解 `Main`所呼叫的每個方法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="02ce1-172">建立索引</span><span class="sxs-lookup"><span data-stu-id="02ce1-172">Creating an index</span></span>
<span data-ttu-id="02ce1-173">建立 `SearchServiceClient`後，`Main` 會接著刪除 "hotels" 索引 (如果已經存在)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="02ce1-174">刪除方法如下：</span><span class="sxs-lookup"><span data-stu-id="02ce1-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="02ce1-175">此方法使用指定的 `SearchServiceClient` 查看索引是否存在，如果存在，就加以刪除。</span><span class="sxs-lookup"><span data-stu-id="02ce1-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-176">為簡單起見，本文的範例程式碼使用 Azure 搜尋服務 .NET SDK 的同步方法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="02ce1-177">我們建議您在應用程式中使用非同步方法，讓應用程式保有可擴充性且回應靈敏。</span><span class="sxs-lookup"><span data-stu-id="02ce1-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="02ce1-178">例如，您可以在以上方法中使用 `ExistsAsync` 和 `DeleteAsync`，而非 `Exists` 和 `Delete`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="02ce1-179">接著，`Main` 會呼叫此方法建立新的 "hotels" 索引：</span><span class="sxs-lookup"><span data-stu-id="02ce1-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="02ce1-180">此方法會以定義新索引結構描述的 `Field` 物件清單，建立新的 `Index` 物件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="02ce1-181">每個欄位均有一個名稱、資料類型和一些屬性，以用於定義欄位的搜尋行為。</span><span class="sxs-lookup"><span data-stu-id="02ce1-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="02ce1-182">`FieldBuilder` 類別會檢查指定 `Hotel` 模型類別的公用屬性 (property) 和屬性 (attribute)，進而使用反映來建立索引的 `Field` 物件清單。</span><span class="sxs-lookup"><span data-stu-id="02ce1-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="02ce1-183">我們稍後會仔細查看 `Hotel` 類別。</span><span class="sxs-lookup"><span data-stu-id="02ce1-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-184">如有需要，您永遠可以直接建立 `Field` 物件清單，而不是使用`FieldBuilder`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="02ce1-185">例如，您可能不想使用模型類別，或您可能需要使用不想藉由新增屬性來修改的現有模型類別。</span><span class="sxs-lookup"><span data-stu-id="02ce1-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="02ce1-186">除了欄位之外，您還可以新增評分設定檔、建議工具或 CORS 選項到 Index (基於簡化目的，範例已省略這些選項)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="02ce1-187">如需 Index 物件以及其組成部分的詳細資訊，請參閱 [SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index)和 [Azure 搜尋服務 REST API 參考](https://docs.microsoft.com/rest/api/searchservice/)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="02ce1-188">填入索引</span><span class="sxs-lookup"><span data-stu-id="02ce1-188">Populating the index</span></span>
<span data-ttu-id="02ce1-189">`Main` 的下一步是填入新建立的索引。</span><span class="sxs-lookup"><span data-stu-id="02ce1-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="02ce1-190">執行方法如下：</span><span class="sxs-lookup"><span data-stu-id="02ce1-190">This is done in the following method:</span></span>

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
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="02ce1-191">此方法分四個部分。</span><span class="sxs-lookup"><span data-stu-id="02ce1-191">This method has four parts.</span></span> <span data-ttu-id="02ce1-192">第一個部分會建立 `Hotel` 物件的陣列，做為我們上傳到索引的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="02ce1-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="02ce1-193">為簡單起見，此資料採硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="02ce1-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="02ce1-194">在您的應用程式中，資料可能會來自像是 SQL 資料庫的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="02ce1-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="02ce1-195">第二個部分會建立包含文件的 `IndexBatch` 。</span><span class="sxs-lookup"><span data-stu-id="02ce1-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="02ce1-196">您在建立批次時 (在此案例中，是藉由呼叫 `IndexBatch.Upload`)，指定要套用至該批次的作業。</span><span class="sxs-lookup"><span data-stu-id="02ce1-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="02ce1-197">接著以 `Documents.Index` 方法將該 Batch 上傳至 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="02ce1-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-198">在此範例中，我們只上傳文件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="02ce1-199">如果您想要將變更合併至現有的文件，或是刪除文件，您可以改為呼叫 `IndexBatch.Merge`、`IndexBatch.MergeOrUpload` 或 `IndexBatch.Delete` 來建立批次。</span><span class="sxs-lookup"><span data-stu-id="02ce1-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="02ce1-200">您也可以在單一批次中混合不同的作業，方法是呼叫 `IndexBatch.New`，它會採用一組 `IndexAction` 物件，其中每個物件都會要求 Azure 搜尋服務針對文件執行特定的作業。</span><span class="sxs-lookup"><span data-stu-id="02ce1-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="02ce1-201">您可以建立每個擁有自己作業的 `IndexAction`，方法是呼叫對應的方法，例如 `IndexAction.Merge`、`IndexAction.Upload` 等等。</span><span class="sxs-lookup"><span data-stu-id="02ce1-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="02ce1-202">此方法的第三部分是擷取區塊，該區塊會為編制索引處理重要錯誤情況。</span><span class="sxs-lookup"><span data-stu-id="02ce1-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="02ce1-203">如果您的 Azure Search 服務無法將 Batch 中的一些文件編制索引，則 `Documents.Index` 會擲回 `IndexBatchException`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="02ce1-204">如果您在服務負載過重時編制文件的索引，就會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="02ce1-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="02ce1-205">**我們強烈建議您在程式碼中明確處理此情況。**</span><span class="sxs-lookup"><span data-stu-id="02ce1-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="02ce1-206">您可以延遲，然後重新嘗試將失敗的文件編制索引，或像範例一樣加以記錄並繼續，或是根據您應用程式的資料一致性需求執行其他操作。</span><span class="sxs-lookup"><span data-stu-id="02ce1-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-207">您可以使用 `FindFailedActionsToRetry` 方法來建構新的批次，該批次僅包含先前呼叫 `Index` 時失敗的動作。</span><span class="sxs-lookup"><span data-stu-id="02ce1-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="02ce1-208">此方法記載於[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_)，而且有如何[在 StackOverflow 上](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry)正確使用它的討論。</span><span class="sxs-lookup"><span data-stu-id="02ce1-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="02ce1-209">最後，`UploadDocuments` 方法會延遲兩秒。</span><span class="sxs-lookup"><span data-stu-id="02ce1-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="02ce1-210">您的 Azure 搜尋服務中會發生非同步索引編製，因此範例應用程式必須稍待一會，才能確定文件已準備好可供搜尋。</span><span class="sxs-lookup"><span data-stu-id="02ce1-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="02ce1-211">通常只有在示範、測試和範例應用程式中，才需要這類延遲。</span><span class="sxs-lookup"><span data-stu-id="02ce1-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="02ce1-212">.NET SDK 如何處理文件</span><span class="sxs-lookup"><span data-stu-id="02ce1-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="02ce1-213">您可能想知道 Azure 搜尋服務 .NET SDK 如何能夠將使用者定義的類別執行個體 (例如 `Hotel` 上傳至索引。</span><span class="sxs-lookup"><span data-stu-id="02ce1-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="02ce1-214">為了回答這問題，我們來看一下 `Hotel` 類別：</span><span class="sxs-lookup"><span data-stu-id="02ce1-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
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

<span data-ttu-id="02ce1-215">首先要注意的是，每個 `Hotel` 的公用屬性會對應索引定義中的欄位，但這之中有一項關鍵的差異：每個欄位的名稱會以小寫字母 (「駝峰式命名法」) 為開頭，而每個 `Hotel` 的公用屬性名稱會以大小字母 (「巴斯卡命名法」) 為開頭。</span><span class="sxs-lookup"><span data-stu-id="02ce1-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="02ce1-216">這在執行資料繫結、而目標結構描述在應用程式開發人員控制範圍之外的 .NET 應用程式中很常見。</span><span class="sxs-lookup"><span data-stu-id="02ce1-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="02ce1-217">與其違反 .NET 命名方針，使屬性名稱為駝峰式命名法，您可以改用 `[SerializePropertyNamesAsCamelCase]` 屬性，告訴 SDK 自動將屬性名稱對應至駝峰式命名法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-218">Azure 搜尋服務 .NET SDK 使用 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 程式庫來將您的自訂模型物件序列化到 JSON 中，以及將您在 JSON 中的自訂模型物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="02ce1-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="02ce1-219">如有需要，您可以自訂這個序列化的過程。</span><span class="sxs-lookup"><span data-stu-id="02ce1-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="02ce1-220">如需詳細資訊，請參閱[使用 JSON.NET 自訂序列化](#JsonDotNet)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="02ce1-221">第二個要注意的是裝飾每個公用屬性 (property) 的屬性 (attribute)，例如 `IsFilterable`、`IsSearchable`、`Key` 和 `Analyzer`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="02ce1-222">這些屬性直接對應至 [Azure 搜尋服務索引的對應屬性](https://docs.microsoft.com/rest/api/searchservice/create-index#request)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="02ce1-223">`FieldBuilder` 類別會使用這些屬性來建構索引的欄位定義。</span><span class="sxs-lookup"><span data-stu-id="02ce1-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="02ce1-224">第三個要注意的是，`Hotel` 類別為公用屬性的資料類型。</span><span class="sxs-lookup"><span data-stu-id="02ce1-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="02ce1-225">這些屬性的 .NET 類型會對應至索引定義中，與其相當的欄位類型。</span><span class="sxs-lookup"><span data-stu-id="02ce1-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="02ce1-226">例如，`Category` 字串屬性會對應至 `category` 欄位 (此欄位屬於 `Edm.String` 類型)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="02ce1-227">`bool?` 與 `Edm.Boolean`、`DateTimeOffset?` 與 `Edm.DateTimeOffset` 等，它們之間也有類似的類型對應。類型對應的特定規則和 `Documents.Get` 方法已一起記載於 [Azure 搜尋服務 .NET SDK 參考](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="02ce1-228">`FieldBuilder` 類別會為您處理這項對應，但它仍有助您了解您需要對任何序列化問題進行疑難排解的情況。</span><span class="sxs-lookup"><span data-stu-id="02ce1-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="02ce1-229">這讓使用您的類別做為文件可雙向有效；您也可以擷取搜尋結果，然後讓 SDK 將結果自動還原序列化為您選擇的類型，我們會在下一節中看到這部分。</span><span class="sxs-lookup"><span data-stu-id="02ce1-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-230">Azure 搜尋服務 .NET SDK 還支援使用 `Document` 類別的動態類型文件，也就是欄位名稱與欄位值的索引鍵/值對應。</span><span class="sxs-lookup"><span data-stu-id="02ce1-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="02ce1-231">當您在設計階段卻不知道索引的結構描述時，這很實用，否則要繫結到特定模型類別會很麻煩。</span><span class="sxs-lookup"><span data-stu-id="02ce1-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="02ce1-232">SDK 中所有處理文件的方法，都有可搭配 `Document` 類別使用的多載，以及使用泛型類型參數的強類型多載。</span><span class="sxs-lookup"><span data-stu-id="02ce1-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="02ce1-233">本教學課程的範例程式碼只使用了後者。</span><span class="sxs-lookup"><span data-stu-id="02ce1-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="02ce1-234">`Document` 類別繼承自 `Dictionary<string, object>`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="02ce1-235">如需其他詳細資訊，請前往[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="02ce1-236">**為什麼您應該使用 Nullable 資料類型**</span><span class="sxs-lookup"><span data-stu-id="02ce1-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="02ce1-237">當您將自己的模型類別設計為可對應至 Azure 搜尋服務索引時，建議您將 `bool` 和 `int` 等的值類型屬性宣告為可為 Null (例如宣告為 `bool?`，而不是 `bool`)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="02ce1-238">如果您使用不可為 Null 的屬性，則必須保證  索引中沒有任何文件的對應欄位包含 Null 值。</span><span class="sxs-lookup"><span data-stu-id="02ce1-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="02ce1-239">SDK 和 Azure 搜尋服務都不會協助您強制執行這項規定。</span><span class="sxs-lookup"><span data-stu-id="02ce1-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="02ce1-240">這不只是假設性的問題：如果您在類型為 `Edm.Int32` 的現有索引中新增欄位，</span><span class="sxs-lookup"><span data-stu-id="02ce1-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="02ce1-241">更新索引定義之後，所有文件對於該新的欄位具有 null 值 (因為所有類型在 Azure 搜尋服務中都可為 null)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="02ce1-242">如果您接著對該欄位使用 `int` 屬性不可為 Null 的模型類別，就會在嘗試擷取文件時得到類似這樣的 `JsonSerializationException`：</span><span class="sxs-lookup"><span data-stu-id="02ce1-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="02ce1-243">因此，我們建議您在模型類別中使用可為 Null 的類型，來做為最佳作法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="02ce1-244">使用 JSON.NET 自訂序列化</span><span class="sxs-lookup"><span data-stu-id="02ce1-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="02ce1-245">SDK 會使用 JSON.NET 序列化和還原序列化文件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="02ce1-246">您可以視需要定義您自己的 `JsonConverter` 或 `IContractResolver` 來自訂序列化和還原序列化 (如需詳細資訊，請參閱 [JSON.NET 文件](http://www.newtonsoft.com/json/help/html/Introduction.htm))。</span><span class="sxs-lookup"><span data-stu-id="02ce1-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="02ce1-247">當您想要調整您的應用程式的現有模型類別以搭配使用 Azure 搜尋服務以及其他更進階的案例時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="02ce1-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="02ce1-248">例如，使用自訂序列化，您可以：</span><span class="sxs-lookup"><span data-stu-id="02ce1-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="02ce1-249">包含或排除模型類別的特定屬性儲存為文件欄位。</span><span class="sxs-lookup"><span data-stu-id="02ce1-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="02ce1-250">在程式碼的屬性名稱和索引的欄位名稱之間進行對應。</span><span class="sxs-lookup"><span data-stu-id="02ce1-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="02ce1-251">建立可用來將屬性對應至文件欄位的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="02ce1-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="02ce1-252">您可以在 GitHub 上的 Azure 搜尋服務 .NET SDK 的單元測試中找到實作自訂序列化的範例。</span><span class="sxs-lookup"><span data-stu-id="02ce1-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="02ce1-253">[這個資料夾](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models)是好的起點。</span><span class="sxs-lookup"><span data-stu-id="02ce1-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="02ce1-254">它包含自訂序列化測試使用的類別。</span><span class="sxs-lookup"><span data-stu-id="02ce1-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="02ce1-255">搜尋索引中的文件</span><span class="sxs-lookup"><span data-stu-id="02ce1-255">Searching for documents in the index</span></span>
<span data-ttu-id="02ce1-256">此範例應用程式的最後一個步驟是搜尋索引中的一些文件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="02ce1-257">執行方法如下：</span><span class="sxs-lookup"><span data-stu-id="02ce1-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
    Console.WriteLine("and return the hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

    Console.WriteLine("Search the entire index for the term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="02ce1-258">每次執行查詢時，這個方法都會先建立新的 `SearchParameters` 物件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="02ce1-259">該物件用於指定查詢的其他選項，例如排序、篩選、分頁及 Facet。</span><span class="sxs-lookup"><span data-stu-id="02ce1-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="02ce1-260">在此方法中，我們會針對不同查詢設定 `Filter`、`Select`、`OrderBy` 和 `Top` 屬性。</span><span class="sxs-lookup"><span data-stu-id="02ce1-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="02ce1-261">所有 `SearchParameters` 屬性都記載於[這裡](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="02ce1-262">下一步是實際執行搜尋查詢，</span><span class="sxs-lookup"><span data-stu-id="02ce1-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="02ce1-263">我們透過 `Documents.Search` 方法完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="02ce1-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="02ce1-264">針對每次查詢，我們會傳遞搜尋文字做為字串 (如果沒有搜尋文字，則傳遞 `"*"`)，並再加上先前建立的搜尋參數。</span><span class="sxs-lookup"><span data-stu-id="02ce1-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="02ce1-265">我們也指定了 `Hotel` 做為 `Documents.Search` 的類型參數，藉此告訴 SDK 將搜尋結果中的文件還原序列化為 `Hotel` 類型的物件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="02ce1-266">如需搜尋查詢運算式語法的詳細資訊，請參閱 [這裡](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)。</span><span class="sxs-lookup"><span data-stu-id="02ce1-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="02ce1-267">最後，在每次查詢之後，此方法會反覆查詢搜尋結果中的所有相符項，然後將每個文件列印至主控台：</span><span class="sxs-lookup"><span data-stu-id="02ce1-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="02ce1-268">讓我們依序仔細查看每個查詢。</span><span class="sxs-lookup"><span data-stu-id="02ce1-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="02ce1-269">以下是執行第一個查詢的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="02ce1-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="02ce1-270">在此情況下，我們會搜尋符合 "budget" 這個字的旅館，而且我們只想要傳回 `Select` 參數所指定的旅館名稱。</span><span class="sxs-lookup"><span data-stu-id="02ce1-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="02ce1-271">結果如下︰</span><span class="sxs-lookup"><span data-stu-id="02ce1-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="02ce1-272">接下來，我們想要尋找每晚費率小於 $150 的旅館，並且只傳回旅館識別碼和描述︰</span><span class="sxs-lookup"><span data-stu-id="02ce1-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

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

<span data-ttu-id="02ce1-273">此查詢會使用 OData `$filter` 運算式 (`baseRate lt 150`)，以篩選索引中的文件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="02ce1-274">您可以在 [這裡](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)找到更多 Azure 搜尋服務支援的 OData 語法。</span><span class="sxs-lookup"><span data-stu-id="02ce1-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="02ce1-275">查詢的結果如下：</span><span class="sxs-lookup"><span data-stu-id="02ce1-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="02ce1-276">接下來，我們要尋找最近重新裝修的前兩間旅館，並顯示旅館名稱和上次重新裝修日期。</span><span class="sxs-lookup"><span data-stu-id="02ce1-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="02ce1-277">程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="02ce1-277">Here is the code:</span></span> 

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

<span data-ttu-id="02ce1-278">在此情況下，我們再次使用 OData 語法，將 `OrderBy` 參數指定為 `lastRenovationDate desc`。</span><span class="sxs-lookup"><span data-stu-id="02ce1-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="02ce1-279">我們也會將 `Top` 設定為 2，以確保只取得前兩份文件。</span><span class="sxs-lookup"><span data-stu-id="02ce1-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="02ce1-280">如同前面，我們會設定 `Select` 來指定應傳回哪些欄位。</span><span class="sxs-lookup"><span data-stu-id="02ce1-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="02ce1-281">結果如下︰</span><span class="sxs-lookup"><span data-stu-id="02ce1-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="02ce1-282">最後，我們想要尋找符合 "motel" 這個字的所有旅館︰</span><span class="sxs-lookup"><span data-stu-id="02ce1-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="02ce1-283">結果如下，其中包含所有欄位，因為我們並未指定 `Select` 屬性︰</span><span class="sxs-lookup"><span data-stu-id="02ce1-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="02ce1-284">此步驟已完成本教學課程，但別就此結束。</span><span class="sxs-lookup"><span data-stu-id="02ce1-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="02ce1-285">**後續步驟** 會提供可深入了解 Azure 搜尋服務的其他資源。</span><span class="sxs-lookup"><span data-stu-id="02ce1-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02ce1-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02ce1-286">Next steps</span></span>
* <span data-ttu-id="02ce1-287">瀏覽 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) 及 [REST API](https://docs.microsoft.com/rest/api/searchservice/) 參考文章。</span><span class="sxs-lookup"><span data-stu-id="02ce1-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="02ce1-288">使用 [影片與其他範例和教學課程](search-video-demo-tutorial-list.md)加深知識。</span><span class="sxs-lookup"><span data-stu-id="02ce1-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="02ce1-289">檢閱 [命名規則](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) ，了解命名各種物件的規則。</span><span class="sxs-lookup"><span data-stu-id="02ce1-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="02ce1-290">檢閱 Azure 搜尋服務 [支援的資料類型](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 。</span><span class="sxs-lookup"><span data-stu-id="02ce1-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
