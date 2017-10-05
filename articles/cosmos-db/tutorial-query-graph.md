---
title: "如何在 Azure Cosmos DB 中查詢圖形資料？ | Microsoft Docs"
description: "了解如何在 Azure Cosmos DB 中查詢圖形資料"
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
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="5c7e3-104">Azure Cosmos DB：如何使用圖形 API (預覽) 來進行查詢？</span><span class="sxs-lookup"><span data-stu-id="5c7e3-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="5c7e3-105">Azure Cosmos DB [圖形 API](graph-introduction.md) (預覽) 支援 [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) 查詢。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="5c7e3-106">本文提供範例文件和查詢來協助您開始操作。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="5c7e3-107">如需詳細的 Gremlin 參考資料，請參閱 [Gremlin 支援](gremlin-support.md)一文。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="5c7e3-108">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="5c7e3-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5c7e3-109">使用 Gremlin 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="5c7e3-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c7e3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c7e3-110">Prerequisites</span></span>

<span data-ttu-id="5c7e3-111">若要讓這些查詢能夠運作，您必須具備 Azure Cosmos DB 帳戶，並且在容器中有圖形資料。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="5c7e3-112">不符合上述其中任何一項條件嗎？</span><span class="sxs-lookup"><span data-stu-id="5c7e3-112">Don't have any of those?</span></span> <span data-ttu-id="5c7e3-113">請完成 [5 分鐘快速入門](create-graph-dotnet.md)或[開發人員教學課程](tutorial-query-graph.md)，以建立帳戶並在資料庫中填入資料。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="5c7e3-114">您可以使用 [Azure Cosmos DB .NET 圖形程式庫](graph-sdk-dotnet.md)、[Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)或慣用的 Gremlin 驅動程式，來執行下列查詢。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="5c7e3-115">計算圖形中的頂點</span><span class="sxs-lookup"><span data-stu-id="5c7e3-115">Count vertices in the graph</span></span>

<span data-ttu-id="5c7e3-116">下列程式碼片段會示範如何計算圖形中的頂點數目：</span><span class="sxs-lookup"><span data-stu-id="5c7e3-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="5c7e3-117">篩選器</span><span class="sxs-lookup"><span data-stu-id="5c7e3-117">Filters</span></span>

<span data-ttu-id="5c7e3-118">您可以使用 Gremlin 的 `has` 和 `hasLabel` 步驟，然後使用 `and`、`or` 及 `not` 來結合它們以建置更複雜的篩選。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="5c7e3-119">Azure Cosmos DB 可以對您頂點和角度內的所有屬性進行無從驗證綱要的索引編製，來加速查詢：</span><span class="sxs-lookup"><span data-stu-id="5c7e3-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="5c7e3-120">投射</span><span class="sxs-lookup"><span data-stu-id="5c7e3-120">Projection</span></span>

<span data-ttu-id="5c7e3-121">您可以使用 `values` 步驟來投射查詢結果中的某些屬性：</span><span class="sxs-lookup"><span data-stu-id="5c7e3-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="5c7e3-122">尋找相關的邊緣和頂點</span><span class="sxs-lookup"><span data-stu-id="5c7e3-122">Find related edges and vertices</span></span>

<span data-ttu-id="5c7e3-123">到目前為止，我們只看到可在任何資料庫中運作的查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="5c7e3-124">當您需要瀏覽至相關的邊緣和頂點時，圖形對周遊作業來說既快速又有效率。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="5c7e3-125">我們將尋找 Thomas 的所有朋友。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="5c7e3-126">我們的做法是使用 Gremlin 的 `outE` 步驟來尋找來自 Thomas 的外邊緣，然後使用 Gremlin 的 `inV` 步驟來周遊至來自這些邊緣的內頂點：</span><span class="sxs-lookup"><span data-stu-id="5c7e3-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="5c7e3-127">下一個查詢會透過呼叫 `outE` 和 `inV` 兩次來執行兩次跳躍，以找出 Thomas 的所有「朋友的朋友」。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="5c7e3-128">您可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯，包括混合篩選條件運算式、使用 `loop` 步驟來執行迴圈，以及使用 `choose` 步驟來實作條件式瀏覽。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="5c7e3-129">深入了解您可以透過 [Gremlin 支援](gremlin-support.md)來執行哪些操作！</span><span class="sxs-lookup"><span data-stu-id="5c7e3-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c7e3-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c7e3-130">Next steps</span></span>

<span data-ttu-id="5c7e3-131">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="5c7e3-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5c7e3-132">了解如何使用「圖形」來進行查詢</span><span class="sxs-lookup"><span data-stu-id="5c7e3-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="5c7e3-133">您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。</span><span class="sxs-lookup"><span data-stu-id="5c7e3-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c7e3-134">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="5c7e3-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)