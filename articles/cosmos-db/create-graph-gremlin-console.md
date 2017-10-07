---
title: "Azure Cosmos DB 教學課程︰在Apache TinkerPops Gremlin 主控台中建立、查詢和周遊 | Microsoft Docs"
description: "Azure 宇宙資料庫快速入門 toocreates 頂點，邊緣，並使用 hello Azure Cosmos DB Graph API 查詢。"
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a>Azure Cosmos DB： 建立、 查詢和周遊 hello Gremlin 主控台中的圖形

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 資料庫和圖形 （容器） 使用 hello Azure 入口網站，然後使用 hello [Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)從[Apache TinkerPop](http://tinkerpop.apache.org) toowork 與圖形 API （預覽） 資料。 在本教學課程中，您建立及查詢頂點和邊緣、 更新頂點屬性，會查詢頂點、 周遊 hello 圖形，並卸除頂點。

![從 hello Apache Gremlin 主控台 azure Cosmos DB](./media/create-graph-gremlin-console/gremlin-console.png)

hello Gremlin 主控台是 Groovy/Java 型和 Linux、 Mac 和 Windows 上執行。 您可以從 hello [Apache TinkerPop 網站](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip)。

## <a name="prerequisites"></a>必要條件

您需要 Azure 訂用帳戶 toocreate Azure Cosmos DB 帳戶 toohave 本快速入門。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

您也需要 tooinstall hello [Gremlin 主控台](http://tinkerpop.apache.org/)。 使用 3.2.5 版或更高版本。

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>新增圖形

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a id="ConnectAppService"></a>連接 tooyour 應用程式服務
1. 開始之前 hello Gremlin 主控台、 建立或修改 hello apache-tinkerpop-gremlin-console-3.2.5/conf 目錄中的 hello 遠端 secure.yaml 組態檔。
2. 填入您的 host、port、username、password、connectionPool 和 serializer 組態︰

    設定|建議的值|說明
    ---|---|---
    主機|[***.graphs.azure.com]|請看下方的螢幕擷取畫面。 這是在 hello Azure 入口網站，以方括號，以 hello 尾端 hello 概觀 頁面上的 hello Gremlin URI 值： 443 / 已移除。<br><br>此值也可以擷取從 hello 金鑰 索引標籤，移除 https://、 變更文件 toographs 並移除尾端 hello 使用 hello URI 值： 443 /。
    連接埠|443|設定 too443。
    username|您的使用者名稱|hello hello 形式的資源`/dbs/<db>/colls/<coll>`其中`<db>`是您的資料庫名稱和`<coll>`集合名稱。
    password|您的主要金鑰| 請看下方的第二個螢幕擷取畫面。 這是 hello 的您可以擷取 hello 金鑰 頁面上 hello 主要金鑰 方塊中的 Azure 入口網站的主要金鑰。 在左側 hello toocopy hello 值 hello 使用 hello [複製] 按鈕。
    connectionPool|{enableSsl: true}|SSL 的連線集區設定。
    序列化程式|{ className: org.apache.tinkerpop.gremlin.<br>driver.ser.GraphSONMessageSerializerV1d0,<br> config: { serializeResultToString: true }}|設定 toothis 值，並刪除任何`\n`分行符號 hello 值中貼上時。

    Hello 主機值，複製 [hello **Gremlin URI**值從 hello**概觀**頁面： ![hello Azure 入口網站 hello 概觀] 頁面上的檢視與複製 hello Gremlin URI 值](./media/create-graph-gremlin-console/gremlin-uri.png)

    Hello 密碼值，複製 [hello**主索引鍵**從 hello**金鑰**頁面：![主索引鍵 hello Azure 入口網站中的檢視與複製金鑰] 頁面](./media/create-graph-gremlin-console/keys.png)


3. 在您的終端機中，執行`bin/gremlin.bat`或`bin/gremlin.sh`toostart hello [Gremlin 主控台](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/)。
4. 在您的終端機中，執行`:remote connect tinkerpop.server conf/remote-secure.yaml`tooconnect tooyour 應用程式服務。

    > [!TIP]
    > 如果您收到 hello 錯誤`No appenders could be found for logger`確定您在步驟 2 中所述更新 hello 遠端 secure.yaml 檔案中的 hello 序列化程式值。 

太棒了！ 既然我們完成 hello 安裝程式，讓我們開始執行某些主控台命令。

我們來試試簡單的 count() 命令。 Hello 主控台在 hello 提示字元中輸入 hello 下列：
```
:> g.V().count()
```

> [!TIP]
> 請注意 hello`:>`前面 hello`g.V().count()`文字嗎？ 
>
> 這是您需要 tootype hello 命令的一部分。 請務必 hello Gremlin 主控台中，使用 Azure Cosmos DB 時。  
>
> 省略此`:>`前置詞會指示 hello 主控台 tooexecute hello 命令在本機，通常針對在記憶體中的圖形。
> 使用此`:>`會告知 hello 主控台 tooexecute 遠端命令，在此情況下針對 Cosmos DB (任一 hello localhost 的模擬器，或 > Azure 執行個體)。


## <a name="create-vertices-and-edges"></a>建立頂點和邊緣

首先我們會新增五個人員頂點 Thomas、Mary Kay、Robin、Ben 和 Jack。

輸入 (Thomas)：

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

輸出：

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
輸入 (Mary Kay)：

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

輸出：

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

輸入 (Robin)：

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

輸出：

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

輸入 (Ben)：

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

輸出：

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

輸入 (Jack)：

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

輸出：

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


接下來，我們會新增人員之間關聯性的邊緣。

輸入 (Thomas -> Mary Kay)：

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

輸出：

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

輸入 (Thomas -> Robin)：

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

輸出：

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

輸入 (Robin -> Ben)：

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

輸出：

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a>更新頂點

讓我們更新 hello *Thomas*與新的存留期的頂點*45*。

輸入：
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
輸出：

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a>查詢圖形

現在，我們會對您的圖形執行各種查詢。

首先，我們再試一次查詢的篩選器 tooreturn 只有人超過 40 年。

輸入 (篩選查詢)︰

```
:> g.V().hasLabel('person').has('age', gt(40))
```

輸出：

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

接下來，讓我們專案 hello 名字人士 hello 超過 40 年。

輸入 (篩選 + 預測查詢)：

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

輸出：

```
==>Thomas
```

## <a name="traverse-your-graph"></a>查詢圖形

讓我們來周遊 hello 圖形 tooreturn 所有 Thomas 的朋友。

輸入 (Thomas 的朋友)：

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

輸出： 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

接下來，讓我們協助 hello 下一層的頂點。 周遊 hello 圖形 tooreturn 所有 hello 之朋友的朋友 Thomas 的。

輸入 (Thomas 朋友的朋友)：

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
輸出：

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a>刪除頂點

我們現在頂點從資料庫中刪除 hello 圖形。

輸入 (置放 Jack 頂點)：

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a>清除圖形

最後，讓我們來清除 hello 資料庫的所有頂點和邊緣。

輸入：

```
:> g.E().drop()
:> g.V().drop()
```

恭喜！ 您已經完成此 Azure Cosmos DB：圖形 API 教學課程！

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：  

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您已經學會 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管圖形、 建立頂點和邊緣、 以及周遊使用 hello Gremlin 主控台程式圖形的方式。 您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。 

> [!div class="nextstepaction"]
> [使用 Gremlin 進行查詢](tutorial-query-graph.md)
