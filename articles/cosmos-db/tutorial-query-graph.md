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
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="db2d8-104">Azure Cosmos DB: Tooquery 與如何 hello Graph API （預覽）？</span><span class="sxs-lookup"><span data-stu-id="db2d8-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="db2d8-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) （預覽） 支援[Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/)查詢。</span><span class="sxs-lookup"><span data-stu-id="db2d8-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="db2d8-106">這篇文章會提供範例文件，並查詢的 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="db2d8-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="db2d8-107">Hello 中提供詳細的 Gremlin 參考[Gremlin 支援](gremlin-support.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="db2d8-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="db2d8-108">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="db2d8-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="db2d8-109">使用 Gremlin 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="db2d8-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db2d8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="db2d8-110">Prerequisites</span></span>

<span data-ttu-id="db2d8-111">這些查詢 toowork，您必須擁有 Azure Cosmos DB 帳戶，而且具有 hello 容器中的圖形資料。</span><span class="sxs-lookup"><span data-stu-id="db2d8-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="db2d8-112">不符合上述其中任何一項條件嗎？</span><span class="sxs-lookup"><span data-stu-id="db2d8-112">Don't have any of those?</span></span> <span data-ttu-id="db2d8-113">完整的 hello [5 分鐘快速入門](create-graph-dotnet.md)或 hello[開發人員教學課程](tutorial-query-graph.md)toocreate 帳戶，並填入您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="db2d8-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="db2d8-114">您可以執行下列查詢使用 hello hello [Azure Cosmos DB.NET 圖形庫](graph-sdk-dotnet.md)， [Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)，或您最愛的 Gremlin 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="db2d8-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="db2d8-115">Hello 圖形中的計數頂點</span><span class="sxs-lookup"><span data-stu-id="db2d8-115">Count vertices in hello graph</span></span>

<span data-ttu-id="db2d8-116">hello，下列程式碼片段顯示如何 toocount hello 的 hello 圖形中的頂點數目：</span><span class="sxs-lookup"><span data-stu-id="db2d8-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="db2d8-117">篩選器</span><span class="sxs-lookup"><span data-stu-id="db2d8-117">Filters</span></span>

<span data-ttu-id="db2d8-118">您可以執行使用 Gremlin 的篩選`has`和`hasLabel`步驟，並將它們結合使用`and`， `or`，和`not`toobuild 更複雜的篩選。</span><span class="sxs-lookup"><span data-stu-id="db2d8-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="db2d8-119">Azure Cosmos DB 可以對您頂點和角度內的所有屬性進行無從驗證綱要的索引編製，來加速查詢：</span><span class="sxs-lookup"><span data-stu-id="db2d8-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="db2d8-120">投射</span><span class="sxs-lookup"><span data-stu-id="db2d8-120">Projection</span></span>

<span data-ttu-id="db2d8-121">您可以投影中使用 hello hello 查詢結果的特定屬性`values`步驟：</span><span class="sxs-lookup"><span data-stu-id="db2d8-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="db2d8-122">尋找相關的邊緣和頂點</span><span class="sxs-lookup"><span data-stu-id="db2d8-122">Find related edges and vertices</span></span>

<span data-ttu-id="db2d8-123">到目前為止，我們只看到可在任何資料庫中運作的查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="db2d8-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="db2d8-124">您需要 toonavigate toorelated 邊緣和頂點圖形進行快速且有效率的周遊作業。</span><span class="sxs-lookup"><span data-stu-id="db2d8-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="db2d8-125">我們將尋找 Thomas 的所有朋友。</span><span class="sxs-lookup"><span data-stu-id="db2d8-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="db2d8-126">要執行此作業使用 Gremlin 的`outE`逐步的 toofind 所有 hello-都邊緣從 Thomas、，然後從使用 Gremlin 的那些都邊緣周遊 toohello 中-頂點`inV`步驟：</span><span class="sxs-lookup"><span data-stu-id="db2d8-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="db2d8-127">hello 下一個查詢會執行兩個躍點 toofind Thomas'"朋友的朋友 」，藉由呼叫的所有`outE`和`inV`兩次。</span><span class="sxs-lookup"><span data-stu-id="db2d8-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="db2d8-128">您可以建立更複雜的查詢，並實作功能強大的圖形周遊邏輯使用 Gremlin，包括混合的篩選運算式中，執行迴圈使用 hello`loop`步驟中，實作條件式使用巡覽及 hello`choose`步驟。</span><span class="sxs-lookup"><span data-stu-id="db2d8-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="db2d8-129">深入了解您可以透過 [Gremlin 支援](gremlin-support.md)來執行哪些操作！</span><span class="sxs-lookup"><span data-stu-id="db2d8-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="db2d8-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db2d8-130">Next steps</span></span>

<span data-ttu-id="db2d8-131">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="db2d8-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="db2d8-132">了解如何使用 Graph tooquery</span><span class="sxs-lookup"><span data-stu-id="db2d8-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="db2d8-133">您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。</span><span class="sxs-lookup"><span data-stu-id="db2d8-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db2d8-134">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="db2d8-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)