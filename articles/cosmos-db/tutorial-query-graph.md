---
title: "在 Azure Cosmos DB aaaHow tooquery 圖形資料嗎？ | Microsoft Docs"
description: "了解在 Azure Cosmos DB tooquery 圖形資料"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB: Tooquery 與如何 hello Graph API （預覽）？

hello Azure Cosmos DB [Graph API](graph-introduction.md) （預覽） 支援[Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/)查詢。 這篇文章會提供範例文件，並查詢的 tooget 啟動。 Hello 中提供詳細的 Gremlin 參考[Gremlin 支援](gremlin-support.md)發行項。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 使用 Gremlin 來查詢資料

## <a name="prerequisites"></a>必要條件

這些查詢 toowork，您必須擁有 Azure Cosmos DB 帳戶，而且具有 hello 容器中的圖形資料。 不符合上述其中任何一項條件嗎？ 完整的 hello [5 分鐘快速入門](create-graph-dotnet.md)或 hello[開發人員教學課程](tutorial-query-graph.md)toocreate 帳戶，並填入您的資料庫。 您可以執行下列查詢使用 hello hello [Azure Cosmos DB.NET 圖形庫](graph-sdk-dotnet.md)， [Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)，或您最愛的 Gremlin 驅動程式。

## <a name="count-vertices-in-hello-graph"></a>Hello 圖形中的計數頂點

hello，下列程式碼片段顯示如何 toocount hello 的 hello 圖形中的頂點數目：

```
g.V().count()
```

## <a name="filters"></a>篩選器

您可以執行使用 Gremlin 的篩選`has`和`hasLabel`步驟，並將它們結合使用`and`， `or`，和`not`toobuild 更複雜的篩選。 Azure Cosmos DB 可以對您頂點和角度內的所有屬性進行無從驗證綱要的索引編製，來加速查詢：

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>投射

您可以投影中使用 hello hello 查詢結果的特定屬性`values`步驟：

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>尋找相關的邊緣和頂點

到目前為止，我們只看到可在任何資料庫中運作的查詢運算子。 您需要 toonavigate toorelated 邊緣和頂點圖形進行快速且有效率的周遊作業。 我們將尋找 Thomas 的所有朋友。 要執行此作業使用 Gremlin 的`outE`逐步的 toofind 所有 hello-都邊緣從 Thomas、，然後從使用 Gremlin 的那些都邊緣周遊 toohello 中-頂點`inV`步驟：

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

hello 下一個查詢會執行兩個躍點 toofind Thomas'"朋友的朋友 」，藉由呼叫的所有`outE`和`inV`兩次。 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

您可以建立更複雜的查詢，並實作功能強大的圖形周遊邏輯使用 Gremlin，包括混合的篩選運算式中，執行迴圈使用 hello`loop`步驟中，實作條件式使用巡覽及 hello`choose`步驟。 深入了解您可以透過 [Gremlin 支援](gremlin-support.md)來執行哪些操作！

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 了解如何使用 Graph tooquery 

您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。

> [!div class="nextstepaction"]
> [全域散發您的資料](tutorial-global-distribution-documentdb.md)