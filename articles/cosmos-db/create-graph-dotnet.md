---
title: "Azure Cosmos DB.NET 應用程式使用 aaaBuild hello Graph API |Microsoft 文件"
description: "提供.NET 程式碼範例中，您可以使用 tooconnect tooand 查詢 Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB： 建置使用 hello Graph API 的.NET 應用程式

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 資料庫和圖形 （容器） 使用 hello Azure 入口網站。 然後建置並執行主控台應用程式根據 hello [Graph API](graph-sdk-dotnet.md) （預覽）。  

## <a name="prerequisites"></a>必要條件

如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>新增圖形

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們從 github，複製 Graph API 應用程式設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Visual Studio，並開啟 hello 方案檔，然後開啟。 

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello Program.cs 檔案，而且您會發現這行程式碼建立 hello Azure Cosmos DB 資源。 

* hello DocumentClient 會初始化。 在 hello 預覽中，我們可以加入圖形延伸模組 API hello Azure Cosmos DB 用戶端上。 我們會努力分開 hello Azure Cosmos DB 用戶端和資源，獨立圖形用戶端。

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* 已建立新資料庫。

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* 已建立新圖形。

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* 一系列的 Gremlin 步驟會執行使用 hello`CreateGremlinQuery`方法。

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 Visual Studio 2017，開啟 hello App.config 檔案。 

2. 在 hello Azure 入口網站，Azure Cosmos DB 帳戶中，按一下 **金鑰**在 hello 左瀏覽。 

    ![檢視及複製 hello hello 金鑰 頁面上的 Azure 入口網站中的主索引鍵](./media/create-graph-dotnet/keys.png)

3. 複製您**URI**值從 hello 入口網站，並將其 hello App.config 中的 hello 端點索引鍵的值。Hello 前面螢幕擷取畫面 toocopy hello 值中所示，您可以使用 hello [複製] 按鈕。

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. 複製您**主索引鍵**值從 hello 入口網站，並使其 hello App.config 中的 hello AuthKey 索引鍵的值，然後儲存您的變更。 

    `<add key="AuthKey" value="FILLME" />`

您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 

## <a name="run-hello-console-app"></a>執行 hello 主控台應用程式

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello **GraphGetStarted**專案中**方案總管 中**，然後按一下**管理 NuGet 封裝**。 

2. 在 hello NuGet**瀏覽**方塊中，輸入*Microsoft.Azure.Graphs*並檢查 hello**包含發行前版本**方塊。 

3. 從 hello 結果中，安裝 hello **Microsoft.Azure.Graphs**程式庫。 這會安裝 hello Azure Cosmos DB 圖形延伸模組程式庫封裝和所有相依性。

    如果您收到有關檢閱變更 toohello 方案，請按一下**確定**。 如果您收到關於接受授權的訊息，請按一下 [我接受]。

4. 按一下 CTRL + F5 toorun hello 應用程式。

   hello 主控台視窗會顯示 hello 頂點與所加入 toohello 圖形的邊緣。 Hello 指令碼完成時，按 ENTER 鍵兩次 tooclose hello 主控台視窗。 

## <a name="browse-using-hello-data-explorer"></a>瀏覽使用 hello 資料總管

您現在可以移回 tooData 總管 hello Azure 入口網站中的和瀏覽並查詢新的圖形資料。

1. 在 Data 總管 hello 新資料庫會出現在 hello 圖形窗格。 展開 graphdb、graphcollz，然後按一下圖形。

2. 按一下 hello**套用篩選**按鈕 toouse hello 預設查詢 tooview hello 圖形中的所有 hello verticies。 hello 圖形窗格中會顯示 hello hello 範例應用程式所產生的資料。

    您可以拉出 hello 圖形，您可以展開 hello 圖形的顯示空間、 新增其他 verticies，並移動 verticies hello 上的顯示的介面。

    ![在總管 中的資料在 hello Azure 入口網站中的檢視 hello 圖形](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟： 

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管 中，而圖形，並執行應用程式。 您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。 

> [!div class="nextstepaction"]
> [使用 Gremlin 進行查詢](tutorial-query-graph.md)

