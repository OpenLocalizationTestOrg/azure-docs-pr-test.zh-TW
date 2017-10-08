---
title: "aaaAzure MongoDB api Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello MongoDB API。"
services: cosmos-db
keywords: "全域散發, MongoDB"
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>如何使用全域發佈 toosetup Azure Cosmos DB hello MongoDB 應用程式開發介面

在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello MongoDB API 連接。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello [MongoDB 應用程式開發介面](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>確認您的地區設定使用 hello MongoDB 應用程式開發介面
hello 雙 MongoDB 為 toorun hello 檢查您的全域組態 API 內的最簡單的方式*isMaster()* hello Mongo 殼層命令。

從您的 Mongo 殼層︰

   ```
      db.isMaster()
   ```
   
範例結果︰

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>連接 tooa 慣用的區域使用 hello MongoDB 應用程式開發介面

hello MongoDB API 可讓您 toospecify 集合的全域散發資料庫的讀取喜好設定。 針對兩者低延遲讀取和通用的高可用性，建議您設定集合的唯讀喜好設定太*接近*。 讀取的喜好設定的*接近*是設定的 tooread 從 hello 最接近的區域。

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

針對，主要的應用程式讀取/寫入區域與次要區域進行災害復原 (DR) 情況下，我們建議您設定您的集合讀取喜好設定太*慣用次要*。 讀取的喜好設定的*慣用次要*hello 主要區域無法使用時，會設定的 tooread 從 hello 次要區域。

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

最後，如果您將像是 toomanually 指定您讀取的區域。 您可以設定 hello 區域標記內讀取喜好設定。

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

就這麼簡單，這樣便已完成本教學課程。 您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。 如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello DocumentDB Api

您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。

> [!div class="nextstepaction"]
> [與 hello 模擬器在本機開發](local-emulator.md)
