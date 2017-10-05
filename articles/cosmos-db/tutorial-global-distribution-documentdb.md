---
title: "適用於 DocumentDB API 的 Azure Cosmos DB 全域散發教學課程 | Microsoft Docs"
description: "了解如何使用 DocumentDB API 來設定 Azure Cosmos DB 全域散發。"
services: cosmos-db
keywords: "全域散發, documentdb"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="d0d60-104">如何使用 DocumentDB API 來設定 Azure Cosmos DB 全域散發</span><span class="sxs-lookup"><span data-stu-id="d0d60-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="d0d60-105">在本文中，我們會說明如何使用 Azure 入口網站來設定 Azure Cosmos DB 全域散發，然後使用 DocumentDB API 來進行連線。</span><span class="sxs-lookup"><span data-stu-id="d0d60-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="d0d60-106">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="d0d60-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d0d60-107">使用 Azure 入口網站來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="d0d60-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="d0d60-108">使用 [DocumentDB API](documentdb-introduction.md) 來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="d0d60-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="d0d60-109">使用 DocumentDB API 來連線到慣用的區域</span><span class="sxs-lookup"><span data-stu-id="d0d60-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="d0d60-110">為了充分運用 [全球發佈](distribute-data-globally.md)，用戶端應用程式可以指定已排序的區域喜好設定清單，以用來執行文件作業。</span><span class="sxs-lookup"><span data-stu-id="d0d60-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="d0d60-111">這可透過設定連接原則來完成。</span><span class="sxs-lookup"><span data-stu-id="d0d60-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="d0d60-112">DocumentDB SDK 將會根據 Azure Cosmos DB 帳戶組態、目前的區域可用性及所指定的喜好設定清單，選擇最適合的端點來執行寫入和讀取作業。</span><span class="sxs-lookup"><span data-stu-id="d0d60-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="d0d60-113">這份喜好設定清單是在使用 DocumentDB SDK 將連線初始化時即已指定。</span><span class="sxs-lookup"><span data-stu-id="d0d60-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="d0d60-114">SDK 會接受選擇性參數 "PreferredLocations"，也就是已排序的 Azure 區域清單。</span><span class="sxs-lookup"><span data-stu-id="d0d60-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="d0d60-115">SDK 會自動將所有寫入傳送至目前的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d0d60-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="d0d60-116">所有讀取都將傳送至 PreferredLocations 清單中的第一個可用區域。</span><span class="sxs-lookup"><span data-stu-id="d0d60-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="d0d60-117">如果要求失敗，用戶端將無法往下到清單中的下一個區域，依此類推。</span><span class="sxs-lookup"><span data-stu-id="d0d60-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="d0d60-118">SDK 只會嘗試從 PreferredLocations 中指定的區域讀取。</span><span class="sxs-lookup"><span data-stu-id="d0d60-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="d0d60-119">因此，比方說，如果資料庫帳戶可供三個區域使用，但用戶端只針對 PreferredLocations 指定其中兩個非寫入區域，則將不會在該寫入區域以外的地方提供讀取服務，即使發生容錯移轉也一樣。</span><span class="sxs-lookup"><span data-stu-id="d0d60-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="d0d60-120">應用程式可以藉由檢查兩個屬性 (WriteEndpoint 和 ReadEndpoint，適用於 SDK 1.8 版和以上版本) 來確認 SDK 目前所選擇的寫入端點和讀取端點。</span><span class="sxs-lookup"><span data-stu-id="d0d60-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="d0d60-121">如果未設定 PreferredLocations 屬性，將會從目前的寫入區域為所有要求提供服務。</span><span class="sxs-lookup"><span data-stu-id="d0d60-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="d0d60-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="d0d60-122">.NET SDK</span></span>
<span data-ttu-id="d0d60-123">您不需變更任何程式碼即可使用 SDK。</span><span class="sxs-lookup"><span data-stu-id="d0d60-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="d0d60-124">在此情況下，SDK 會自動將讀取和寫入導向至目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d0d60-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="d0d60-125">在 .NET SDK 的 1.8 版和更新版本中，適用於 DocumentClient 建構函式的 ConnectionPolicy 參數會有一個名為 Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations 的屬性。</span><span class="sxs-lookup"><span data-stu-id="d0d60-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="d0d60-126">這個屬性的類型是 Collection `<string>` ，而且應包含區域名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="d0d60-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="d0d60-127">字串值已按照 [Azure 區域][regions]頁面的 [區域名稱] 欄而格式化，而且在第一個字元之前和最後一個字元之後沒有空格。</span><span class="sxs-lookup"><span data-stu-id="d0d60-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="d0d60-128">目前的寫入和讀取端點分別適用於 DocumentClient.WriteEndpoint 和 DocumentClient.ReadEndpoint。</span><span class="sxs-lookup"><span data-stu-id="d0d60-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="d0d60-129">不應將端點的 URI 視為長時間執行的常數。</span><span class="sxs-lookup"><span data-stu-id="d0d60-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="d0d60-130">服務可能會隨時更新這些項目。</span><span class="sxs-lookup"><span data-stu-id="d0d60-130">The service may update these at any point.</span></span> <span data-ttu-id="d0d60-131">SDK 會自動處理此變更。</span><span class="sxs-lookup"><span data-stu-id="d0d60-131">The SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="d0d60-132">NodeJS、JavaScript 和 Python SDK</span><span class="sxs-lookup"><span data-stu-id="d0d60-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="d0d60-133">您不需變更任何程式碼即可使用 SDK。</span><span class="sxs-lookup"><span data-stu-id="d0d60-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="d0d60-134">在此情況下，SDK 會自動將讀取和寫入導向至目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d0d60-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="d0d60-135">在每個 SDK 的 1.8 版和更新版本中，適用於 DocumentClient 建構函式的 ConnectionPolicy 參數會有一個名為 DocumentClient.ConnectionPolicy.PreferredLocations 的新屬性。</span><span class="sxs-lookup"><span data-stu-id="d0d60-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="d0d60-136">這個參數是取得區域名稱清單的字串陣列。</span><span class="sxs-lookup"><span data-stu-id="d0d60-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="d0d60-137">名稱已按照 [Azure 區域][regions]頁面的 [區域名稱] 欄而格式化。</span><span class="sxs-lookup"><span data-stu-id="d0d60-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="d0d60-138">您也可以在方便的物件 AzureDocuments.Regions 中使用預先定義的常數</span><span class="sxs-lookup"><span data-stu-id="d0d60-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="d0d60-139">目前的寫入和讀取端點分別適用於 DocumentClient.getWriteEndpoint 和 DocumentClient.getReadEndpoint。</span><span class="sxs-lookup"><span data-stu-id="d0d60-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="d0d60-140">不應將端點的 URI 視為長時間執行的常數。</span><span class="sxs-lookup"><span data-stu-id="d0d60-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="d0d60-141">服務可能會隨時更新這些項目。</span><span class="sxs-lookup"><span data-stu-id="d0d60-141">The service may update these at any point.</span></span> <span data-ttu-id="d0d60-142">SDK 將會自動處理此變更。</span><span class="sxs-lookup"><span data-stu-id="d0d60-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="d0d60-143">以下是 NodeJS/Javascript 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="d0d60-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="d0d60-144">Python 和 Java 都將遵循相同模式。</span><span class="sxs-lookup"><span data-stu-id="d0d60-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="d0d60-145">REST</span><span class="sxs-lookup"><span data-stu-id="d0d60-145">REST</span></span>
<span data-ttu-id="d0d60-146">一旦資料庫帳戶可供多個區域使用之後，用戶端就可藉由在下列 URI 上執行 GET 要求來查詢其可用性。</span><span class="sxs-lookup"><span data-stu-id="d0d60-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="d0d60-147">服務將會針對複本傳回區域清單及其對應的 Azure Cosmos DB 端點 URI。</span><span class="sxs-lookup"><span data-stu-id="d0d60-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="d0d60-148">回應中將會指出目前的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d0d60-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="d0d60-149">用戶端接著可針對所有未來的 REST API 要求選取適當的端點，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d0d60-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="d0d60-150">範例回應</span><span class="sxs-lookup"><span data-stu-id="d0d60-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="d0d60-151">所有的 PUT、POST 和 DELETE 要求都必須移至指定的寫入 URI</span><span class="sxs-lookup"><span data-stu-id="d0d60-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="d0d60-152">所有的 GET 和其他唯讀要求 (例如查詢) 可能會移至用戶端選擇的任何端點</span><span class="sxs-lookup"><span data-stu-id="d0d60-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="d0d60-153">將要求寫入至唯讀區域將會失敗，並產生 HTTP 錯誤碼 403 (「禁止」)。</span><span class="sxs-lookup"><span data-stu-id="d0d60-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="d0d60-154">如果寫入區域在用戶端初始探索階段之後變更，則寫入至上一個寫入區域的後續作業將會失敗，並產生 HTTP 錯誤碼 403 (「禁止」)。</span><span class="sxs-lookup"><span data-stu-id="d0d60-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="d0d60-155">用戶端接著應再次 GET 區域清單，以取得更新的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="d0d60-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="d0d60-156">就這麼簡單，這樣便已完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="d0d60-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="d0d60-157">您可以透過閱讀 [Azure Cosmos DB 中的一致性層級](consistency-levels.md)，來了解如何管理全域複寫帳戶的一致性。</span><span class="sxs-lookup"><span data-stu-id="d0d60-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="d0d60-158">如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="d0d60-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0d60-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0d60-159">Next steps</span></span>

<span data-ttu-id="d0d60-160">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="d0d60-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0d60-161">使用 Azure 入口網站來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="d0d60-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="d0d60-162">使用 DocumentDB API 來設定全域散發</span><span class="sxs-lookup"><span data-stu-id="d0d60-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="d0d60-163">您現在可以繼續進行到下一個教學課程，以了解如何使用 Azure Cosmos DB 本機模擬器在本機進行開發。</span><span class="sxs-lookup"><span data-stu-id="d0d60-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0d60-164">使用模擬器在本機進行開發</span><span class="sxs-lookup"><span data-stu-id="d0d60-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

