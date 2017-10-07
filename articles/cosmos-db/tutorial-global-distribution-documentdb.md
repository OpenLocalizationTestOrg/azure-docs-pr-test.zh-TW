---
title: "DocumentDB api aaaAzure Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello DocumentDB API。"
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
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="9ac51-104">如何使用全域發佈 toosetup Azure Cosmos DB hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="9ac51-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="9ac51-105">在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello DocumentDB API 連接。</span><span class="sxs-lookup"><span data-stu-id="9ac51-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="9ac51-106">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="9ac51-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="9ac51-107">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9ac51-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="9ac51-108">設定全域發佈使用 hello [DocumentDB Api](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="9ac51-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="9ac51-109">連接 tooa 慣用的區域使用 hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="9ac51-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="9ac51-110">中的順序 tootake 優點[全域發佈](distribute-data-globally.md)，用戶端應用程式可以指定 hello 排序喜好設定清單中的區域 toobe 用 tooperform 文件的作業。</span><span class="sxs-lookup"><span data-stu-id="9ac51-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="9ac51-111">設定 hello 連線原則可以完成此作業。</span><span class="sxs-lookup"><span data-stu-id="9ac51-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="9ac51-112">根據 hello Azure Cosmos DB 帳戶設定，目前區域的可用性和 hello 喜好設定清單中指定，hello 大部分最佳端點將會選擇的 hello DocumentDB SDK tooperform 寫入和讀取作業。</span><span class="sxs-lookup"><span data-stu-id="9ac51-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="9ac51-113">當使用 hello DocumentDB Sdk 初始化連線時，會指定此喜好設定清單。</span><span class="sxs-lookup"><span data-stu-id="9ac51-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="9ac51-114">hello Sdk 接受選擇性參數 」 PreferredLocations"也就是 Azure 區域的排序的清單。</span><span class="sxs-lookup"><span data-stu-id="9ac51-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="9ac51-115">hello SDK 都會自動傳送所有寫入 toohello 目前寫入的區域。</span><span class="sxs-lookup"><span data-stu-id="9ac51-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="9ac51-116">所有的讀取將會傳送 toohello 第一個可用的地區 hello PreferredLocations 清單中。</span><span class="sxs-lookup"><span data-stu-id="9ac51-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="9ac51-117">如果 hello 要求失敗，hello 用戶端會向 hello 清單 toohello 下一個區域，失敗等等。</span><span class="sxs-lookup"><span data-stu-id="9ac51-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="9ac51-118">hello Sdk 將只會嘗試 tooread hello PreferredLocations 中指定的區域。</span><span class="sxs-lookup"><span data-stu-id="9ac51-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="9ac51-119">因此，比方說，如果 hello 資料庫帳戶有三個區域，但是 hello 用戶端只會指定兩個 hello 非寫入區域的 PreferredLocations，然後讀取將會是由提供服務 hello 寫入區域，即使在 hello 的容錯移轉的情況下。</span><span class="sxs-lookup"><span data-stu-id="9ac51-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="9ac51-120">hello 應用程式可以確認 hello 目前寫入端點，以及讀取 hello SDK 所檢查的兩個屬性，WriteEndpoint 和 ReadEndpoint 可用 SDK 1.8 版和更新版本所選的端點。</span><span class="sxs-lookup"><span data-stu-id="9ac51-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="9ac51-121">如果未設定 hello PreferredLocations 屬性，將會 hello 目前寫入區域從服務的所有要求。</span><span class="sxs-lookup"><span data-stu-id="9ac51-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="9ac51-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="9ac51-122">.NET SDK</span></span>
<span data-ttu-id="9ac51-123">hello SDK 可以用不需要變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="9ac51-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="9ac51-124">在此情況下，hello SDK 會自動引導同時讀取和寫入 toohello 目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="9ac51-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="9ac51-125">在 1.8 及更新版本的 hello.NET SDK 版本，hello ConnectionPolicy hello DocumentClient 建構函式的參數會有稱為 Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations 的屬性。</span><span class="sxs-lookup"><span data-stu-id="9ac51-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="9ac51-126">這個屬性的類型是 Collection `<string>` ，而且應包含區域名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="9ac51-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="9ac51-127">會在每個 hello 區域名稱的資料行上 hello 格式化 hello 字串值[Azure 區域][ regions]頁面上，不含空格之前或之後 hello 第一次，並分別最後一個字元。</span><span class="sxs-lookup"><span data-stu-id="9ac51-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="9ac51-128">hello 目前寫入和讀取的端點中可用 DocumentClient.WriteEndpoint DocumentClient.ReadEndpoint 分別。</span><span class="sxs-lookup"><span data-stu-id="9ac51-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="9ac51-129">hello hello 端點的 Url 不應視為長時間執行的常數。</span><span class="sxs-lookup"><span data-stu-id="9ac51-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="9ac51-130">hello 服務可能會更新這些在任何時間點。</span><span class="sxs-lookup"><span data-stu-id="9ac51-130">hello service may update these at any point.</span></span> <span data-ttu-id="9ac51-131">hello SDK 自動處理這項變更。</span><span class="sxs-lookup"><span data-stu-id="9ac51-131">hello SDK handles this change automatically.</span></span>
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

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="9ac51-132">NodeJS、JavaScript 和 Python SDK</span><span class="sxs-lookup"><span data-stu-id="9ac51-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="9ac51-133">hello SDK 可以用不需要變更任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="9ac51-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="9ac51-134">在此情況下，SDK 會將自動導向的 hello 同時讀取和寫入 toohello 目前寫入區域。</span><span class="sxs-lookup"><span data-stu-id="9ac51-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="9ac51-135">版本 1.8 及更新版本的每一套 SDK，hello ConnectionPolicy 參數中的 hello DocumentClient 建構函式呼叫 DocumentClient.ConnectionPolicy.PreferredLocations 新屬性。</span><span class="sxs-lookup"><span data-stu-id="9ac51-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="9ac51-136">這個參數是取得區域名稱清單的字串陣列。</span><span class="sxs-lookup"><span data-stu-id="9ac51-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="9ac51-137">hello 名稱的每個在 hello hello 地區名稱資料行格式[Azure 區域][ regions]頁面。</span><span class="sxs-lookup"><span data-stu-id="9ac51-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="9ac51-138">您也可以使用預先定義的 hello 常數 hello 方便物件 AzureDocuments.Regions 中</span><span class="sxs-lookup"><span data-stu-id="9ac51-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="9ac51-139">hello 目前寫入和讀取的端點中可用 DocumentClient.getWriteEndpoint DocumentClient.getReadEndpoint 分別。</span><span class="sxs-lookup"><span data-stu-id="9ac51-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="9ac51-140">hello hello 端點的 Url 不應視為長時間執行的常數。</span><span class="sxs-lookup"><span data-stu-id="9ac51-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="9ac51-141">hello 服務可能會更新這些在任何時間點。</span><span class="sxs-lookup"><span data-stu-id="9ac51-141">hello service may update these at any point.</span></span> <span data-ttu-id="9ac51-142">hello SDK 會自動處理此變更。</span><span class="sxs-lookup"><span data-stu-id="9ac51-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="9ac51-143">以下是 NodeJS/Javascript 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="9ac51-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="9ac51-144">Python 和 Java，則會遵循 hello 相同的模式。</span><span class="sxs-lookup"><span data-stu-id="9ac51-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="9ac51-145">REST</span><span class="sxs-lookup"><span data-stu-id="9ac51-145">REST</span></span>
<span data-ttu-id="9ac51-146">一旦資料庫帳戶都可以使用多個區域中，用戶端可以查詢其可用性 hello 下列 URI 上執行 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="9ac51-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="9ac51-147">hello 服務會傳回一份區域的 hello 複本及其對應 Azure Cosmos DB 端點 Uri。</span><span class="sxs-lookup"><span data-stu-id="9ac51-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="9ac51-148">hello 回應 hello 目前寫入區域就會指出。</span><span class="sxs-lookup"><span data-stu-id="9ac51-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="9ac51-149">hello 用戶端可以再選取 hello 適當端點的未來所有 REST API 要求，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9ac51-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="9ac51-150">範例回應</span><span class="sxs-lookup"><span data-stu-id="9ac51-150">Example response</span></span>

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


* <span data-ttu-id="9ac51-151">所有 PUT、 POST 和 DELETE 要求必須一律指出 toohello 寫入 URI</span><span class="sxs-lookup"><span data-stu-id="9ac51-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="9ac51-152">取得所有及其他唯讀要求 （例如查詢） 可能會 tooany 端點的用戶端 hello 選擇</span><span class="sxs-lookup"><span data-stu-id="9ac51-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="9ac51-153">寫入要求僅限 tooread 區域將會失敗，HTTP 錯誤碼 403 （「 禁止 」）。</span><span class="sxs-lookup"><span data-stu-id="9ac51-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="9ac51-154">如果 hello 寫入區域變更之後用戶端 hello 初始探索階段中，後續寫入 toohello 先前寫入區域將會失敗，HTTP 錯誤碼 403 （「 禁止 」）。</span><span class="sxs-lookup"><span data-stu-id="9ac51-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="9ac51-155">hello 用戶端應該然後 hello 的區域清單再次取得 tooget hello 更新的寫入區域。</span><span class="sxs-lookup"><span data-stu-id="9ac51-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="9ac51-156">就這麼簡單，這樣便已完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="9ac51-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="9ac51-157">您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="9ac51-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="9ac51-158">如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="9ac51-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ac51-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ac51-159">Next steps</span></span>

<span data-ttu-id="9ac51-160">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9ac51-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ac51-161">設定全域發佈使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9ac51-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="9ac51-162">設定全域發佈使用 hello DocumentDB Api</span><span class="sxs-lookup"><span data-stu-id="9ac51-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="9ac51-163">您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。</span><span class="sxs-lookup"><span data-stu-id="9ac51-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ac51-164">與 hello 模擬器在本機開發</span><span class="sxs-lookup"><span data-stu-id="9ac51-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

