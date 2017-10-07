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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>如何使用全域發佈 toosetup Azure Cosmos DB hello DocumentDB API

在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello DocumentDB API 連接。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello [DocumentDB Api](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>連接 tooa 慣用的區域使用 hello DocumentDB API

中的順序 tootake 優點[全域發佈](distribute-data-globally.md)，用戶端應用程式可以指定 hello 排序喜好設定清單中的區域 toobe 用 tooperform 文件的作業。 設定 hello 連線原則可以完成此作業。 根據 hello Azure Cosmos DB 帳戶設定，目前區域的可用性和 hello 喜好設定清單中指定，hello 大部分最佳端點將會選擇的 hello DocumentDB SDK tooperform 寫入和讀取作業。

當使用 hello DocumentDB Sdk 初始化連線時，會指定此喜好設定清單。 hello Sdk 接受選擇性參數 」 PreferredLocations"也就是 Azure 區域的排序的清單。

hello SDK 都會自動傳送所有寫入 toohello 目前寫入的區域。

所有的讀取將會傳送 toohello 第一個可用的地區 hello PreferredLocations 清單中。 如果 hello 要求失敗，hello 用戶端會向 hello 清單 toohello 下一個區域，失敗等等。

hello Sdk 將只會嘗試 tooread hello PreferredLocations 中指定的區域。 因此，比方說，如果 hello 資料庫帳戶有三個區域，但是 hello 用戶端只會指定兩個 hello 非寫入區域的 PreferredLocations，然後讀取將會是由提供服務 hello 寫入區域，即使在 hello 的容錯移轉的情況下。

hello 應用程式可以確認 hello 目前寫入端點，以及讀取 hello SDK 所檢查的兩個屬性，WriteEndpoint 和 ReadEndpoint 可用 SDK 1.8 版和更新版本所選的端點。

如果未設定 hello PreferredLocations 屬性，將會 hello 目前寫入區域從服務的所有要求。

## <a name="net-sdk"></a>.NET SDK
hello SDK 可以用不需要變更任何程式碼。 在此情況下，hello SDK 會自動引導同時讀取和寫入 toohello 目前寫入區域。

在 1.8 及更新版本的 hello.NET SDK 版本，hello ConnectionPolicy hello DocumentClient 建構函式的參數會有稱為 Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations 的屬性。 這個屬性的類型是 Collection `<string>` ，而且應包含區域名稱的清單。 會在每個 hello 區域名稱的資料行上 hello 格式化 hello 字串值[Azure 區域][ regions]頁面上，不含空格之前或之後 hello 第一次，並分別最後一個字元。

hello 目前寫入和讀取的端點中可用 DocumentClient.WriteEndpoint DocumentClient.ReadEndpoint 分別。

> [!NOTE]
> hello hello 端點的 Url 不應視為長時間執行的常數。 hello 服務可能會更新這些在任何時間點。 hello SDK 自動處理這項變更。
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

## <a name="nodejs-javascript-and-python-sdks"></a>NodeJS、JavaScript 和 Python SDK
hello SDK 可以用不需要變更任何程式碼。 在此情況下，SDK 會將自動導向的 hello 同時讀取和寫入 toohello 目前寫入區域。

版本 1.8 及更新版本的每一套 SDK，hello ConnectionPolicy 參數中的 hello DocumentClient 建構函式呼叫 DocumentClient.ConnectionPolicy.PreferredLocations 新屬性。 這個參數是取得區域名稱清單的字串陣列。 hello 名稱的每個在 hello hello 地區名稱資料行格式[Azure 區域][ regions]頁面。 您也可以使用預先定義的 hello 常數 hello 方便物件 AzureDocuments.Regions 中

hello 目前寫入和讀取的端點中可用 DocumentClient.getWriteEndpoint DocumentClient.getReadEndpoint 分別。

> [!NOTE]
> hello hello 端點的 Url 不應視為長時間執行的常數。 hello 服務可能會更新這些在任何時間點。 hello SDK 會自動處理此變更。
>
>

以下是 NodeJS/Javascript 程式碼範例。 Python 和 Java，則會遵循 hello 相同的模式。

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

## <a name="rest"></a>REST
一旦資料庫帳戶都可以使用多個區域中，用戶端可以查詢其可用性 hello 下列 URI 上執行 GET 要求。

    https://{databaseaccount}.documents.azure.com/

hello 服務會傳回一份區域的 hello 複本及其對應 Azure Cosmos DB 端點 Uri。 hello 回應 hello 目前寫入區域就會指出。 hello 用戶端可以再選取 hello 適當端點的未來所有 REST API 要求，如下所示。

範例回應

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


* 所有 PUT、 POST 和 DELETE 要求必須一律指出 toohello 寫入 URI
* 取得所有及其他唯讀要求 （例如查詢） 可能會 tooany 端點的用戶端 hello 選擇

寫入要求僅限 tooread 區域將會失敗，HTTP 錯誤碼 403 （「 禁止 」）。

如果 hello 寫入區域變更之後用戶端 hello 初始探索階段中，後續寫入 toohello 先前寫入區域將會失敗，HTTP 錯誤碼 403 （「 禁止 」）。 hello 用戶端應該然後 hello 的區域清單再次取得 tooget hello 更新的寫入區域。

就這麼簡單，這樣便已完成本教學課程。 您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。 如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello DocumentDB Api

您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。

> [!div class="nextstepaction"]
> [與 hello 模擬器在本機開發](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

