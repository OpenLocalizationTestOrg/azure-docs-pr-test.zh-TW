---
title: "Graph API 的 aaaAzure Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello Graph API。"
services: cosmos-db
keywords: "全域散發, 圖形, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>如何使用全域發佈 toosetup Azure Cosmos DB hello Graph API

在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello Graph API （預覽） 連接。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello [Graph Api](graph-introduction.md) （預覽）

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>連接 tooa 慣用的區域使用 hello Graph API 使用 hello.NET SDK

hello Graph API 會公開為之上 hello DocumentDB SDK 延伸模組程式庫。

中的順序 tootake 優點[全域發佈](distribute-data-globally.md)，用戶端應用程式可以指定 hello 排序喜好設定清單中的區域 toobe 用 tooperform 文件的作業。 設定 hello 連線原則可以完成此作業。 根據 hello Azure Cosmos DB 帳戶設定，目前的地區可用性和 hello 喜好設定清單中指定，hello 會選擇 hello SDK tooperform 寫入和讀取作業大部分最佳端點。

當使用 hello Sdk 初始化連線時，會指定此喜好設定清單。 hello Sdk 接受選擇性參數 」 PreferredLocations"也就是 Azure 區域的排序的清單。

* **寫入**: hello SDK 將會自動傳送所有寫入 toohello 目前寫入區域。
* **讀取**： 所有讀取將會都傳送 toohello 第一個可用的地區 hello PreferredLocations 清單中。 如果 hello 要求失敗，hello 用戶端會向 hello 清單 toohello 下一個區域，失敗等等。 hello Sdk 將只會嘗試 tooread hello PreferredLocations 中指定的區域。 因此，比方說，如果 hello Cosmos DB 帳戶位在三個區域，但是 hello 用戶端只會指定兩個 hello 非寫入區域 PreferredLocations 的然後讀取會是由提供服務 hello 寫入區域，即使在 hello 的容錯移轉的情況下。

hello 應用程式可以確認 hello 目前寫入端點，以及讀取 hello SDK 所檢查的兩個屬性，WriteEndpoint 和 ReadEndpoint 可用 SDK 1.8 版和更新版本所選的端點。 如果未設定 hello PreferredLocations 屬性，將會 hello 目前寫入區域從服務的所有要求。

### <a name="using-hello-sdk"></a>使用 hello SDK

例如，在 hello.NET SDK，hello `ConnectionPolicy` hello 參數`DocumentClient`建構函式具有名`PreferredLocations`。 這個屬性可以設定區域名稱 tooa 的清單。 hello 顯示名稱[Azure 區域][ regions]可以指定一部分`PreferredLocations`。

> [!NOTE]
> hello hello 端點的 Url 不應視為長時間執行的常數。 hello 服務可能會更新這些在任何時間點。 hello SDK 自動處理這項變更。
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
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

[regions]: https://azure.microsoft.com/regions/

