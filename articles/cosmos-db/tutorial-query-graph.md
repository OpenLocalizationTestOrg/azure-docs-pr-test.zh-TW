---
title: "如何在 Azure Cosmos DB 中查詢圖形資料？ | Microsoft Docs"
description: "了解如何在 Azure Cosmos DB 中查詢圖形資料"
services: cosmos-db
documentationcenter: 
author: luisbosquez
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 01/02/2018
ms.author: lbosq
ms.custom: mvc
ms.openlocfilehash: 5a635abfa9fa10cd8c8498e3c95a17af997cea3e
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api"></a>Azure Cosmos DB： 如何使用 Graph API 查詢？

Azure Cosmos DB [Graph API](graph-introduction.md)支援[Gremlin](https://github.com/tinkerpop/gremlin/wiki)查詢。 本文提供範例文件和查詢來協助您開始操作。 如需詳細的 Gremlin 參考資料，請參閱 [Gremlin 支援](gremlin-support.md)一文。

本文涵蓋下列工作： 

> [!div class="checklist"]
> * 使用 Gremlin 來查詢資料

## <a name="prerequisites"></a>必要條件

若要讓這些查詢能夠運作，您必須具備 Azure Cosmos DB 帳戶，並且在容器中有圖形資料。 不符合上述其中任何一項條件嗎？ 請完成 [5 分鐘快速入門](create-graph-dotnet.md)或[開發人員教學課程](tutorial-query-graph.md)，以建立帳戶並在資料庫中填入資料。 您可以使用 [Azure Cosmos DB .NET 圖形程式庫](graph-sdk-dotnet.md)、[Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)或慣用的 Gremlin 驅動程式，來執行下列查詢。

## <a name="count-vertices-in-the-graph"></a>計算圖形中的頂點

下列程式碼片段會示範如何計算圖形中的頂點數目：

```
g.V().count()
```

## <a name="filters"></a>篩選器

您可以使用 Gremlin 的 `has` 和 `hasLabel` 步驟，然後使用 `and`、`or` 及 `not` 來結合它們以建置更複雜的篩選。 Azure Cosmos DB 可以對您頂點和角度內的所有屬性進行無從驗證綱要的索引編製，來加速查詢：

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>投射

您可以使用 `values` 步驟來投射查詢結果中的某些屬性：

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>尋找相關的邊緣和頂點

到目前為止，我們只看到可在任何資料庫中運作的查詢運算子。 當您需要瀏覽至相關的邊緣和頂點時，圖形對周遊作業來說既快速又有效率。 我們將尋找 Thomas 的所有朋友。 我們的做法是使用 Gremlin 的 `outE` 步驟來尋找來自 Thomas 的外邊緣，然後使用 Gremlin 的 `inV` 步驟來周遊至來自這些邊緣的內頂點：

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

下一個查詢會透過呼叫 `outE` 和 `inV` 兩次來執行兩次跳躍，以找出 Thomas 的所有「朋友的朋友」。 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

您可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯，包括混合篩選條件運算式、使用 `loop` 步驟來執行迴圈，以及使用 `choose` 步驟來實作條件式瀏覽。 深入了解您可以透過 [Gremlin 支援](gremlin-support.md)來執行哪些操作！

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已完成下列操作：

> [!div class="checklist"]
> * 了解如何使用「圖形」來進行查詢 

您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。

> [!div class="nextstepaction"]
> [全域散發您的資料](tutorial-global-distribution-sql-api.md)
