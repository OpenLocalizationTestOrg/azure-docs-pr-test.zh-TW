---
title: "Azure Cosmos DB: 使用 Graph API 在.NET 中的 hello 開發 |Microsoft 文件"
description: "深入了解如何使用適用於.NET 的 Azure Cosmos DB 的 DocumentDB api toodevelop"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>使用 Graph API 在.NET 中的 hello 開發 azure Cosmos DB:
Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本教學課程示範如何使用您建立 Azure Cosmos DB 帳戶 toocreate hello Azure 入口網站以及如何 toocreate 圖形資料庫和容器。 然後 hello 應用程式與使用 hello 的四個人員建立簡單的社交網路[Graph API](graph-sdk-dotnet.md) （預覽），則會周遊和查詢使用 Gremlin hello 圖形。

本教學課程涵蓋 hello 下列工作：

> [!div class="checklist"]
> * 建立 Azure Cosmos DB 帳戶 
> * 建立圖形資料庫和容器
> * 將頂點和邊緣 too.NET 物件序列化
> * 新增頂點和邊緣
> * 使用 Gremlin 查詢 hello 圖形

## <a name="graphs-in-azure-cosmos-db"></a>Azure Cosmos DB 中的圖形
您可以使用 Azure Cosmos DB toocreate、 更新和查詢圖形使用 hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md)程式庫。 hello Microsoft.Azure.Graph 程式庫提供單一的擴充方法`CreateGremlinQuery<T>`之上 hello`DocumentClient`類別 tooexecute Gremlin 查詢。

Gremlin 是一個函式程式設計語言，可支援寫入作業 (DML) 及查詢和周遊作業。 我們將討論幾個範例在這個發行項 tooget Gremlin 與您開始使用。 如需 Azure Cosmos DB 中可用之 Gremlin 功能的詳細逐步解說，請參閱 [Gremlin 查詢](gremlin-support.md)。 

## <a name="prerequisites"></a>必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。 
    * 或者，您可以使用 hello [Azure DocumentDB 模擬器](local-emulator.md)本教學課程。
* [Visual Studio](http://www.visualstudio.com/)。

## <a name="create-database-account"></a>建立資料庫帳戶

首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。  

> [!TIP]
> * 已經有 Azure Cosmos DB 帳戶？ 如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)
> * 您是否已有 Azure DocumentDB 帳戶？ 如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。  
> * 如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>設定您的 Visual Studio 方案
1. 在電腦上開啟 **Visual Studio**。
2. 在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。
3. 在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **主控台應用程式 (.NET Framework)**，命名您的專案，然後按一下**確定**。
4. 在 [hello**方案總管] 中**，新主控台應用程式，也就是在您的 Visual Studio 方案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝...**
5. 在 hello **NuGet**索引標籤上，按一下 **瀏覽**，和型別**Microsoft.Azure.Graphs** hello 搜尋方塊中，核取 hello 中**包含發行前版本**.
6. 在 hello 結果中尋找**Microsoft.Azure.Graphs**按一下**安裝**。
   
   如果您收到有關檢閱變更 toohello 方案，請按一下**確定**。 如果您收到關於接受授權的訊息，請按一下 [我接受]。
   
    hello`Microsoft.Azure.Graphs`程式庫提供單一的擴充方法`CreateGremlinQuery<T>`執行 Gremlin 作業。 Gremlin 是一個函式程式設計語言，可支援寫入作業 (DML) 及查詢和周遊作業。 我們將討論幾個範例在這個發行項 tooget Gremlin 與您開始使用。 如需 Azure Cosmos DB 中 Gremlin 功能的詳細逐步解說，請參閱 [Gremlin 查詢](gremlin-support.md)。

## <a id="add-references"></a>連接您的應用程式

在應用程式中新增下列兩個常數和您的「用戶端」變數。 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
接下來，head 回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點 URL 和主索引鍵。 hello 端點 URL 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。 

在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，按一下 **金鑰**，然後按一下**讀寫金鑰**。 

從 hello 入口網站複製 hello URI，並將它貼入`Endpoint`上述的 hello 端點屬性中。 然後複本 hello 從 hello 入口網站的主索引鍵，並將它貼到 hello`AuthKey`上述的屬性。 

![Hello Azure 入口網站的螢幕擷取畫面使用 hello 教學課程 toocreate C# 應用程式。 金鑰] 按鈕上反白顯示 hello Azure Cosmos DB 導覽和 hello URI 與主索引鍵的值上反白顯示 hello 金鑰刀鋒視窗會顯示 Azure Cosmos DB 帳戶 hello] [金鑰] 
 
## <a id="instantiate"></a>具現化 hello DocumentClient 
接下來，建立新的執行個體的 hello **DocumentClient**。  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>建立資料庫 

現在，建立 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)使用 hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx)方法或[CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx)方法 hello **DocumentClient**類別從 hello [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)。  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>建立圖形 

接下來，建立的圖形容器，藉由使用 hello hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)方法或[CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx)方法 hello **DocumentClient**類別。 集合是圖形實體的容器。 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>將頂點和邊緣 too.NET 物件序列化
Azure 的 Cosmos DB 使用 hello [GraphSON 電傳格式](gremlin-support.md)，其定義所在的頂點，邊緣、 和屬性的 JSON 結構描述。 hello Azure Cosmos DB.NET SDK 包含 JSON.NET 做為相依性，而這讓我們 tooserialize/還原序列化 GraphSON 我們可以在程式碼中使用的.NET 物件。

我們將使用一個包含 4 個人的簡單社交網路來作為範例。 我們會審視如何 toocreate`Person`頂點，新增`Knows`之間關聯性，則查詢和周遊 hello 圖形 toofind"朋友的朋友叫什麼 」 關聯性。 

hello`Microsoft.Azure.Graphs.Elements`命名空間提供`Vertex`， `Edge`，`Property`和`VertexProperty`GraphSON 回應 toowell 定義.NET 物件還原序列化的類別。

## <a name="run-gremlin-using-creategremlinquery"></a>使用 CreateGremlinQuery 來執行 Gremlin
Gremlin (例如 SQL) 支援讀取、寫入及查詢作業。 例如，hello 下列程式碼片段示範如何 toocreate 頂點，邊緣、 執行使用的某些查詢範例`CreateGremlinQuery<T>`，並以非同步方式逐一查看使用這些結果`ExecuteNextAsync`和 ' HasMoreResults。

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>新增頂點和邊緣

讓我們看看顯示的 hello 前面一節更詳細的 hello Gremlin 陳述式。 首先，我們會使用 Gremlin 的 `addV` 方法來新增一些頂點。 比方說，hello 下列程式碼片段會建立類型"Person"，"Thomas Andersen"頂點具有屬性的名字、 姓氏和年齡。

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

然後，我們會使用 Gremlin 的 `addE` 方法在這些頂點之間建立一些邊緣。 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

我們可以使用 Gremlin 中的 `properties` 步驟來更新現有的頂點。 我們會略過 hello 呼叫 tooexecute hello 查詢透過`HasMoreResults`和`ExecuteNextAsync`hello 範例 hello 其餘部分。

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

您可以使用 Gremlin 的 `drop` 步驟來卸除邊緣和頂點。 以下是程式碼片段顯示如何 toodelete 的頂點和邊緣。 請注意，卸除頂點執行 hello 串聯刪除相關聯的邊緣。

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>查詢 hello 圖形

您也可以使用 Gremlin 來執行查詢和周遊。 例如，下列程式碼片段的 hello 顯示如何 toocount hello 的 hello 圖形中的頂點數目：

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
您可以執行使用 Gremlin 的篩選`has`和`hasLabel`步驟，並將它們結合使用`and`， `or`，和`not`toobuild 更複雜的篩選：

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

您可以投影中使用 hello hello 查詢結果的特定屬性`values`步驟：

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

到目前為止，我們只看到可在任何資料庫中運作的查詢運算子。 您需要 toonavigate toorelated 邊緣和頂點圖形進行快速且有效率的周遊作業。 我們將尋找 Thomas 的所有朋友。 要執行此作業使用 Gremlin 的`outE`逐步的 toofind 所有 hello-都邊緣從 Thomas、，然後從使用 Gremlin 的那些都邊緣周遊 toohello 中-頂點`inV`步驟：

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

hello 下一個查詢會執行兩個躍點 toofind Thomas'"朋友的朋友 」，藉由呼叫的所有`outE`和`inV`兩次。 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

您可以建立更複雜的查詢，並實作功能強大的圖形周遊邏輯使用 Gremlin，包括混合的篩選運算式中，執行迴圈使用 hello`loop`步驟中，實作條件式使用巡覽及 hello`choose`步驟。 深入了解您可以透過 [Gremlin 支援](gremlin-support.md)來執行哪些操作！

這樣就大功告成了，您已完成此 Azure Cosmos DB 教學課程！ 

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，使用下列步驟 toodelete hello Azure 入口網站在此教學課程所建立的所有資源的 hello。  

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 建立 Azure Cosmos DB 帳戶 
> * 建立圖形資料庫和容器
> * 序列化的頂點和邊緣 too.NET 物件
> * 新增頂點和邊緣
> * 使用 Gremlin 查詢的 hello 圖形

您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。 

> [!div class="nextstepaction"]
> [使用 Gremlin 進行查詢](tutorial-query-graph.md)
