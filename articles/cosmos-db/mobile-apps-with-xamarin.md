---
title: "使用 Xamarin 和 Azure Cosmos DB aaaBuild 行動裝置的應用程式 |Microsoft 文件"
description: "使用 Azure Cosmos DB 建立 Xamarin iOS、Android 或 Forms 應用程式的教學課程。 Azure Cosmos DB 是快速的全球級行動應用程式雲端資料庫。"
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式
大部分的行動應用程式需要 toostore hello 雲端中的資料，而且 Azure Cosmos DB 行動裝置應用程式的雲端資料庫。 行動應用程式開發人員所需的一切盡在其中。 它是完全受管理的資料庫即服務，可依需求進行調整。 以透明的方式，不論您的使用者位於周圍 hello 地球的何處，它可以使 tooyour 應用程式資料。 使用 hello [Azure Cosmos DB.NET Core SDK](documentdb-sdk-dotnet-core.md)，您可以啟用 Xamarin 的行動裝置應用程式 toointeract 直接與 Azure Cosmos DB 沒有中介層。

本文提供的教學課程可讓您了解如何使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式。 您可以在 hello 教學課程找到 hello 完整原始程式碼[Xamarin 和 GitHub 上的 Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin)，包括如何 toomanage 使用者和權限。

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>適用於行動應用程式的 Azure Cosmos DB 功能
Azure 的 Cosmos DB 會提供下列主要功能適用於行動裝置應用程式開發人員的 hello:

![適用於行動應用程式的 Azure Cosmos DB 功能](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* 豐富的無結構描述資料查詢。 Azure Cosmos DB 會將資料以無結構描述 JSON 文件的形式儲存在異質集合中。 它提供[豐富且快速的查詢](documentdb-sql-query.md)hello 不需要結構描述或索引的相關 tooworry。
* 快速的輸送量。 它會採用只有幾毫秒 Azure Cosmos DB tooread 和寫入的文件。 開發人員可以指定它們需要 hello 輸送量和 Azure Cosmos DB 可接受它 99.99 %sla。
* 規模無限制。 您的 Azure Cosmos DB 集合可[隨著應用程式成長](partition-data.md)。 您可以從小型資料大小和每秒數百個要求的輸送量著手。 您的集合可以成長 toopetabytes 資料以及任意大的輸送量數百萬的每秒要求數。
* 散布世界各地。 行動裝置應用程式，使用者會在 hello 移，通常 hello 世界各地。 Azure Cosmos DB 是[分散在世界各地的資料庫](distribute-data-globally.md)。 按一下 hello 對應 toomake 資料存取 tooyour 使用者。
* 內建豐富授權。 使用 Azure Cosmos DB 就能輕鬆實作熱門模式，例如[每位使用者的資料](https://aka.ms/documentdb-xamarin-todouser)或多位使用者共用的資料，而不需要複雜的自訂授權程式碼。
* 地理空間查詢。 許多行動應用程式目前都有提供地理情境體驗。 第一級支援[地理空間類型](geospatial.md)、 Azure Cosmos DB 會建立這些經驗輕鬆 tooaccomplish。
* 二進位附件。 您的應用程式資料通常包含二進位 Blob。 附件的原生支援可讓您更輕鬆 toouse Azure Cosmos DB 為一次滿足您的應用程式資料。

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Azure Cosmos DB 和 Xamarin 教學課程
hello 遵循教學課程顯示如何 toobuild 使用 Xamarin 及 Azure Cosmos DB 行動應用程式。 您可以在 hello 教學課程找到 hello 完整原始程式碼[Xamarin 和 GitHub 上的 Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin)。

### <a name="get-started"></a>開始使用
開始使用 Azure Cosmos DB 輕鬆 tooget 它。 請 toohello Azure 入口網站，並建立新的 Azure Cosmos DB 帳戶。 按一下 hello**快速入門** 索引標籤。下載 hello Xamarin Forms 待辦事項清單範例已連接 tooyour Azure Cosmos DB 帳戶。 

![適用於行動應用程式的 Azure Cosmos DB 快速入門](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

如果您有現有的 Xamarin 應用程式，您可以新增 hello 或者[Azure Cosmos DB NuGet 封裝](documentdb-sdk-dotnet-core.md)。 Azure Cosmos DB 支援 Xamarin.IOS、Xamarin.Android 和 Xamarin Forms 共用程式庫。

### <a name="work-with-data"></a>使用資料
您的資料記錄會以無結構描述 JSON 文件的形式儲存在 Azure Cosmos DB 的異質集合中。 您可以使用不同結構的文件儲存在 hello 相同的集合：

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

在您的 Xamarin 專案中，您可以使用語言整合式的無結構描述資料查詢︰

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>新增使用者
像許多取得已啟動的範例，您所下載的 hello Azure Cosmos DB 範例驗證 toohello 服務 hello 應用程式程式碼中使用主要金鑰的硬式編碼。 此預設值不是最好的作法是您想 toorun 以外的位置，您的本機模擬器上的應用程式。 如果未經授權的使用者取得 hello 主要金鑰，可能會有所有的 hello 資料跨 Azure Cosmos DB 帳戶。 相反地，您的應用程式 tooaccess 只 hello hello 登入的使用者記錄。 Azure Cosmos DB 可讓開發人員 toogrant 應用程式讀取或讀取/寫入權限 tooa 集合時，分組資料分割索引鍵的文件或特定的文件的集合。 

請遵循這些步驟 toomodify hello 待辦事項清單應用程式 tooa 多使用者的待辦事項清單應用程式： 

  1. 使用 Facebook、 Active Directory 或任何其他提供者，以新增登入 tooyour 應用程式。

  2. 建立與 Azure Cosmos DB UserItems 集合**/userId** hello 資料分割索引鍵。 指定 hello 資料分割索引鍵集合可讓 Azure Cosmos DB tooscale 無限做為您的應用程式使用者的 hello 數增加時，同時繼續 toooffer 快速的查詢。

  3. 新增 Azure Cosmos DB 資源權杖訊息代理程式。 這個簡單的 Web API 驗證使用者，並發出存留較短的語彙基元 toosigned 的使用者存取其資料分割內的唯一 toohello 文件。 在此範例中，資源權杖訊息代理程式裝載於 App Service 中。

  4. 修改 hello 應用程式 tooauthenticate tooResource 語彙基元 Broker 與 Facebook 和要求 hello 登入的 Facebook 使用者的 hello 資源權杖。 然後，您可以存取他們 hello UserItems 集合中的資料。  

您可以在 [GitHub 上的資源權杖訊息代理程式](http://aka.ms/documentdb-xamarin-todouser)中找到此模式的完整程式碼範例。 此圖說明 hello 方案：

![Azure Cosmos DB 使用者和權限訊息代理程式](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

如果您想要的兩個使用者 toohave 存取 toohello 相同待辦事項清單中，資源權杖 Broker 中，您可以加入額外的權限 toohello 存取權杖。

### <a name="scale-on-demand"></a>依需求進行調整
Azure Cosmos DB 是受管理的資料庫即服務。 隨著您使用者的基底時，您不需要 tooworry 有關佈建 Vm，或增加核心。 您只需要 Azure Cosmos DB tootell 是需要多少作業每秒 （輸送量） 您應用程式。 您可以指定透過 hello hello 輸送量**標尺**藉由呼叫要求單位 (Ru) 每秒的輸送量的量值的索引標籤。 例如，對 1-KB 文件進行的讀取作業需要 1 RU。 您也可以加入警示 toohello**輸送量**度量 toomonitor hello 流量成長，並以程式設計方式變更警示引發的 hello 輸送量。

![Azure Cosmos DB 依需求調整輸送量](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>進入全球級別
為您的應用程式提升熱門程度，您可能會瞭解使用者 hello 地球。 或者，您想 toobe 做好不可預見的事件。 連線 toohello Azure 入口網站，並開啟您的 Azure Cosmos DB 帳戶。 按一下您的區域的資料持續複寫 tooany 號碼 hello 對應 toomake hello 世界各地。 這項功能可讓您的使用者隨時隨地使用您的資料。 您也可以加入容錯移轉原則 toobe 做好偶發事件。

![跨地理區域的 Azure Cosmos DB 調整](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

恭喜！ 您已完成 hello 方案並且使用 Xamarin 和 Azure Cosmos DB 的行動裝置應用程式。 藉由使用 hello Azure Cosmos DB JavaScript SDK 和原生 iOS/Android 應用程式使用 Azure Cosmos DB REST Api，依照類似的步驟 toobuild Cordova 應用程式。

## <a name="next-steps"></a>後續步驟
* 檢視 hello 原始程式碼[Xamarin 和 GitHub 上的 Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin)。
* 下載 hello [Azure Cosmos DB.NET Core SDK](documentdb-sdk-dotnet-core.md)。
* 尋找更多 [.NET 應用程式](documentdb-dotnet-samples.md)的程式碼範例。
* 了解 [Azure Cosmos DB 豐富查詢功能](documentdb-sql-query.md)。
* 了解 [Azure Cosmos DB 中的地理空間支援](geospatial.md)。



