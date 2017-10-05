---
title: "Azure Cosmos DB Gremlin 支援 | Microsoft Docs"
description: "了解 Apache TinkerPop 的 Gremlin 語言，Azure Cosmos DB 中可用使用其功能和步驟"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: 1052a1a335dd1da15d845c2ba4ebbc3827d56bef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a><span data-ttu-id="1d42d-103">Azure Cosmos DB Gremlin graph 支援</span><span class="sxs-lookup"><span data-stu-id="1d42d-103">Azure Cosmos DB Gremlin graph support</span></span>
<span data-ttu-id="1d42d-104">Azure Cosmos DB 支援 [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps) \(英文\)，該圖形 API 是 [Apache Tinkerpop](http://tinkerpop.apache.org) \(英文\) 的圖形周遊語言，可用於建立圖表實體和執行圖表查詢作業。</span><span class="sxs-lookup"><span data-stu-id="1d42d-104">Azure Cosmos DB supports [Apache Tinkerpop's](http://tinkerpop.apache.org) graph traversal language, [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), which is a Graph API for creating graph entities, and performing graph query operations.</span></span> <span data-ttu-id="1d42d-105">您可以使用 Gremlin 語言建立圖表實體 (頂點和邊緣)、修改這些實體內的屬性、執行查詢和周遊，以及刪除實體。</span><span class="sxs-lookup"><span data-stu-id="1d42d-105">You can use the Gremlin language to create graph entities (vertices and edges), modify properties within those entities, perform queries and traversals, and delete entities.</span></span> 

<span data-ttu-id="1d42d-106">Azure Cosmos DB 在圖表資料庫中提供符合企業需求的功能。</span><span class="sxs-lookup"><span data-stu-id="1d42d-106">Azure Cosmos DB brings enterprise-ready features to graph databases.</span></span> <span data-ttu-id="1d42d-107">其中包括全域散發、獨立調整儲存體和輸送量、可預測的個位數毫秒延遲、自動編製索引，以及 99.99% 的 SLA。</span><span class="sxs-lookup"><span data-stu-id="1d42d-107">This includes global distribution, independent scaling of storage and throughput, predictable single-digit millisecond latencies, automatic indexing, and 99.99% SLAs.</span></span> <span data-ttu-id="1d42d-108">由於 Azure Cosmos DB 支援 TinkerPop/Gremlin，您可以輕鬆地移轉使用另一個圖表資料庫撰寫的應用程式，而不必變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d42d-108">Because Azure Cosmos DB supports TinkerPop/Gremlin, you can easily migrate applications written using another graph database without having to make code changes.</span></span> <span data-ttu-id="1d42d-109">此外，憑藉 Gremlin 支援，Azure Cosmos DB 與啟用 TinkerPop 的分析架構緊密整合，例如 [Apache Spark GraphX](http://spark.apache.org/graphx/)。</span><span class="sxs-lookup"><span data-stu-id="1d42d-109">Additionally, by virtue of Gremlin support, Azure Cosmos DB seamlessly integrates with TinkerPop-enabled analytics frameworks like [Apache Spark GraphX](http://spark.apache.org/graphx/).</span></span> 

<span data-ttu-id="1d42d-110">在本文中，我們提供 Gremlin 的快速逐步解說，並列舉圖形 API 支援預覽中所支援的 Gremlin 功能和步驟。</span><span class="sxs-lookup"><span data-stu-id="1d42d-110">In this article, we provide a quick walkthrough of Gremlin, and enumerate the Gremlin features and steps that are supported in the preview of Graph API support.</span></span>

## <a name="gremlin-by-example"></a><span data-ttu-id="1d42d-111">Gremlin 範例</span><span class="sxs-lookup"><span data-stu-id="1d42d-111">Gremlin by example</span></span>
<span data-ttu-id="1d42d-112">讓我們利用一個範例圖表了解如何以 Gremlin 表達查詢。</span><span class="sxs-lookup"><span data-stu-id="1d42d-112">Let's use a sample graph to understand how queries can be expressed in Gremlin.</span></span> <span data-ttu-id="1d42d-113">下圖顯示的商務應用程式以圖表形式管理使用者、興趣和裝置的相關資料。</span><span class="sxs-lookup"><span data-stu-id="1d42d-113">The following figure shows a business application that manages data about users, interests, and devices in the form of a graph.</span></span>  

![顯示人員、裝置和興趣的範例資料庫](./media/gremlin-support/sample-graph.png) 

<span data-ttu-id="1d42d-115">此圖表有下列頂點類型 (在 Gremlin 中稱為「標籤」)︰</span><span class="sxs-lookup"><span data-stu-id="1d42d-115">This graph has the following vertex types (called "label" in Gremlin):</span></span>

- <span data-ttu-id="1d42d-116">人員：圖表中有三個人：Robin、Thomas 和 Ben</span><span class="sxs-lookup"><span data-stu-id="1d42d-116">People: the graph has three people, Robin, Thomas, and Ben</span></span>
- <span data-ttu-id="1d42d-117">興趣︰他們的興趣，在此範例中是足球比賽</span><span class="sxs-lookup"><span data-stu-id="1d42d-117">Interests: their interests, in this example, the game of Football</span></span>
- <span data-ttu-id="1d42d-118">裝置：此人使用的裝置</span><span class="sxs-lookup"><span data-stu-id="1d42d-118">Devices: the devices that people use</span></span>
- <span data-ttu-id="1d42d-119">作業系統︰執行裝置的作業系統</span><span class="sxs-lookup"><span data-stu-id="1d42d-119">Operating Systems: the operating systems that the devices run on</span></span>

<span data-ttu-id="1d42d-120">我們透過下列邊緣類型/標籤，表達這些實體之間的關聯性︰</span><span class="sxs-lookup"><span data-stu-id="1d42d-120">We represent the relationships between these entities via the following edge types/labels:</span></span>

- <span data-ttu-id="1d42d-121">認識︰例如，「Thomas 認識 Robin」</span><span class="sxs-lookup"><span data-stu-id="1d42d-121">Knows: For example, "Thomas knows Robin"</span></span>
- <span data-ttu-id="1d42d-122">有興趣︰在圖表中表示人員的興趣，例如「Ben 對足球有興趣」</span><span class="sxs-lookup"><span data-stu-id="1d42d-122">Interested: To represent the interests of the people in our graph, for example, "Ben is interested in Football"</span></span>
- <span data-ttu-id="1d42d-123">執行 OS︰膝上型電腦執行 Windows OS</span><span class="sxs-lookup"><span data-stu-id="1d42d-123">RunsOS: Laptop runs the Windows OS</span></span>
- <span data-ttu-id="1d42d-124">使用︰代表某個人使用的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d42d-124">Uses: To represent which device a person uses.</span></span> <span data-ttu-id="1d42d-125">例如，Robin 使用序號 77 的 Motorola 手機</span><span class="sxs-lookup"><span data-stu-id="1d42d-125">For example, Robin uses a Motorola phone with serial number 77</span></span>

<span data-ttu-id="1d42d-126">讓我們使用 [Gremlin 主控台](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) (英文) 對此圖表執行一些作業。</span><span class="sxs-lookup"><span data-stu-id="1d42d-126">Let's run some operations against this graph using the [Gremlin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console).</span></span> <span data-ttu-id="1d42d-127">也可以在您選擇的平台 (Java、Node.js、Python 或 .NET) 使用 Gremlin 驅動程式執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="1d42d-127">You can also perform these operations using Gremlin drivers in the platform of your choice (Java, Node.js, Python, or .NET).</span></span>  <span data-ttu-id="1d42d-128">在了解 Azure Cosmos DB 中支援什麼功能之前，讓我們先看看幾個範例，以熟悉語法。</span><span class="sxs-lookup"><span data-stu-id="1d42d-128">Before we look at what's supported in Azure Cosmos DB, let's look at a few examples to get familiar with the syntax.</span></span>

<span data-ttu-id="1d42d-129">首先，讓我們看看 CRUD。</span><span class="sxs-lookup"><span data-stu-id="1d42d-129">First let's look at CRUD.</span></span> <span data-ttu-id="1d42d-130">下列 Gremlin 陳述式會將 "Thomas" 頂點插入圖表中︰</span><span class="sxs-lookup"><span data-stu-id="1d42d-130">The following Gremlin statement inserts the "Thomas" vertex into the graph:</span></span>

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

<span data-ttu-id="1d42d-131">接著，下列 Gremlin 陳述式會在 Thomas 和 Robin 之間插入 "knows" 邊緣。</span><span class="sxs-lookup"><span data-stu-id="1d42d-131">Next, the following Gremlin statement inserts a "knows" edge between Thomas and Robin.</span></span>

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

<span data-ttu-id="1d42d-132">下列查詢會依名字的遞減順序傳回 "person" 頂點：</span><span class="sxs-lookup"><span data-stu-id="1d42d-132">The following query returns the "person" vertices in descending order of their first names:</span></span>
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

<span data-ttu-id="1d42d-133">圖表的威力在於當您需要回答「Thomas 的朋友使用什麼作業系統？」這種問題時。</span><span class="sxs-lookup"><span data-stu-id="1d42d-133">Where graphs shine is when you need to answer questions like "What operating systems do friends of Thomas use?".</span></span> <span data-ttu-id="1d42d-134">您可以執行這個簡單的 Gremlin 周遊，從圖表中取得這項資訊︰</span><span class="sxs-lookup"><span data-stu-id="1d42d-134">You can run this simple Gremlin traversal to get that information from the graph:</span></span>

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
<span data-ttu-id="1d42d-135">現在，讓我們看看 Azure Cosmos DB 為 Gremlin 開發人員提供什麼功能。</span><span class="sxs-lookup"><span data-stu-id="1d42d-135">Now let's look at what Azure Cosmos DB provides for Gremlin developers.</span></span>

## <a name="gremlin-features"></a><span data-ttu-id="1d42d-136">Gremlin 功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-136">Gremlin features</span></span>
<span data-ttu-id="1d42d-137">TinkerPop 是一套涵蓋各種圖表技術的標準。</span><span class="sxs-lookup"><span data-stu-id="1d42d-137">TinkerPop is a standard that covers a wide range of graph technologies.</span></span> <span data-ttu-id="1d42d-138">因此，它採用標準術語來描述圖表提供者所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="1d42d-138">Therefore, it has standard terminology to describe what features are provided by a graph provider.</span></span> <span data-ttu-id="1d42d-139">Azure Cosmos DB 提供持續、高度並行、可寫入的圖表資料庫，可分割至多個伺服器或叢集。</span><span class="sxs-lookup"><span data-stu-id="1d42d-139">Azure Cosmos DB provides a persistent, high concurrency, writeable graph database that can be partitioned across multiple servers or clusters.</span></span> 

<span data-ttu-id="1d42d-140">下表列出 Azure Cosmos DB 所實作的 TinkerPop 功能︰</span><span class="sxs-lookup"><span data-stu-id="1d42d-140">The following table lists the TinkerPop features that are implemented by Azure Cosmos DB:</span></span> 

| <span data-ttu-id="1d42d-141">類別</span><span class="sxs-lookup"><span data-stu-id="1d42d-141">Category</span></span> | <span data-ttu-id="1d42d-142">Azure Cosmos DB 實作</span><span class="sxs-lookup"><span data-stu-id="1d42d-142">Azure Cosmos DB implementation</span></span> |  <span data-ttu-id="1d42d-143">注意事項</span><span class="sxs-lookup"><span data-stu-id="1d42d-143">Notes</span></span> | 
| --- | --- | --- |
| <span data-ttu-id="1d42d-144">Graph 功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-144">Graph features</span></span> | <span data-ttu-id="1d42d-145">在預覽中提供 Persistence 和 ConcurrentAccess。</span><span class="sxs-lookup"><span data-stu-id="1d42d-145">Provides Persistence and ConcurrentAccess in preview.</span></span> <span data-ttu-id="1d42d-146">設計為支援交易</span><span class="sxs-lookup"><span data-stu-id="1d42d-146">Designed to support Transactions</span></span> | <span data-ttu-id="1d42d-147">可以透過 Spark 連接器實作電腦方法。</span><span class="sxs-lookup"><span data-stu-id="1d42d-147">Computer methods can be implemented via the Spark connector.</span></span> |
| <span data-ttu-id="1d42d-148">變數功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-148">Variable features</span></span> | <span data-ttu-id="1d42d-149">支援布林值、整數、位元組、Double、Float、整數、Long、字串</span><span class="sxs-lookup"><span data-stu-id="1d42d-149">Supports Boolean, Integer, Byte, Double, Float, Integer, Long, String</span></span> | <span data-ttu-id="1d42d-150">支援基本類型、透過資料模型而與複雜類型相容</span><span class="sxs-lookup"><span data-stu-id="1d42d-150">Supports primitive types, is compatible with complex types via data model</span></span> |
| <span data-ttu-id="1d42d-151">頂點功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-151">Vertex features</span></span> | <span data-ttu-id="1d42d-152">支援 RemoveVertices、MetaProperties、AddVertices、MultiProperties、StringIds、UserSuppliedIds、AddProperty、RemoveProperty</span><span class="sxs-lookup"><span data-stu-id="1d42d-152">Supports RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty</span></span>  | <span data-ttu-id="1d42d-153">支援建立、修改和刪除端點</span><span class="sxs-lookup"><span data-stu-id="1d42d-153">Supports creating, modifying, and deleting vertices</span></span> |
| <span data-ttu-id="1d42d-154">頂點屬性功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-154">Vertex property features</span></span> | <span data-ttu-id="1d42d-155">StringIds、UserSuppliedIds、AddProperty、RemoveProperty、BooleanValues、ByteValues、DoubleValues、FloatValues、IntegerValues、LongValues、StringValues</span><span class="sxs-lookup"><span data-stu-id="1d42d-155">StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues</span></span> | <span data-ttu-id="1d42d-156">支援建立、修改和刪除頂點屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-156">Supports creating, modifying, and deleting vertex properties</span></span> |
| <span data-ttu-id="1d42d-157">邊緣功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-157">Edge features</span></span> | <span data-ttu-id="1d42d-158">AddEges、RemoveEdges、StringIds、UserSuppliedIds、AddProperty、RemoveProperty</span><span class="sxs-lookup"><span data-stu-id="1d42d-158">AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty</span></span> | <span data-ttu-id="1d42d-159">支援建立、修改和刪除邊緣</span><span class="sxs-lookup"><span data-stu-id="1d42d-159">Supports creating, modifying, and deleting edges</span></span> |
| <span data-ttu-id="1d42d-160">邊緣屬性功能</span><span class="sxs-lookup"><span data-stu-id="1d42d-160">Edge property features</span></span> | <span data-ttu-id="1d42d-161">Properties、BooleanValues、ByteValues、DoubleValues、FloatValues、IntegerValues、LongValues、StringValues</span><span class="sxs-lookup"><span data-stu-id="1d42d-161">Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues</span></span> | <span data-ttu-id="1d42d-162">支援建立、修改和刪除邊緣屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-162">Supports creating, modifying, and deleting edge properties</span></span> |

## <a name="gremlin-wire-format-graphson"></a><span data-ttu-id="1d42d-163">Gremlin 電傳格式︰GraphSON</span><span class="sxs-lookup"><span data-stu-id="1d42d-163">Gremlin wire format: GraphSON</span></span>

<span data-ttu-id="1d42d-164">從 Gremlin 作業傳回結果時，Azure Cosmos DB 會使用 [GraphSON 格式](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format)。</span><span class="sxs-lookup"><span data-stu-id="1d42d-164">Azure Cosmos DB uses the [GraphSON format](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) when returning results from Gremlin operations.</span></span> <span data-ttu-id="1d42d-165">GraphSON 是 Gremlin 使用 JSON 表示頂點、邊緣和屬性 (單一值和多重值屬性) 的標準格式。</span><span class="sxs-lookup"><span data-stu-id="1d42d-165">GraphSON is the Gremlin standard format for representing vertices, edges, and properties (single and multi-valued properties) using JSON.</span></span> 

<span data-ttu-id="1d42d-166">例如，下列程式碼片段顯示從 Azure Cosmos DB 傳回用戶端之頂點的 GraphSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="1d42d-166">For example, the following snippet shows a GraphSON representation of a vertex *returned to the client* from Azure Cosmos DB.</span></span> 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

<span data-ttu-id="1d42d-167">GraphSON 用於頂點的屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="1d42d-167">The properties used by GraphSON for vertices are the following:</span></span>

| <span data-ttu-id="1d42d-168">屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-168">Property</span></span> | <span data-ttu-id="1d42d-169">說明</span><span class="sxs-lookup"><span data-stu-id="1d42d-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1d42d-170">id</span><span class="sxs-lookup"><span data-stu-id="1d42d-170">id</span></span> | <span data-ttu-id="1d42d-171">頂點的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d42d-171">The ID for the vertex.</span></span> <span data-ttu-id="1d42d-172">必須是唯一的 (適合的話，與 _partition 的值結合)</span><span class="sxs-lookup"><span data-stu-id="1d42d-172">Must be unique (in combination with the value of _partition if applicable)</span></span> |
| <span data-ttu-id="1d42d-173">標籤</span><span class="sxs-lookup"><span data-stu-id="1d42d-173">label</span></span> | <span data-ttu-id="1d42d-174">頂點的標籤。</span><span class="sxs-lookup"><span data-stu-id="1d42d-174">The label of the vertex.</span></span> <span data-ttu-id="1d42d-175">這是選擇性，用來描述實體類型。</span><span class="sxs-lookup"><span data-stu-id="1d42d-175">This is optional, and used to describe the entity type.</span></span> |
| <span data-ttu-id="1d42d-176">類型</span><span class="sxs-lookup"><span data-stu-id="1d42d-176">type</span></span> | <span data-ttu-id="1d42d-177">用來區別頂端和非圖表文件</span><span class="sxs-lookup"><span data-stu-id="1d42d-177">Used to distinguish vertices from non-graph documents</span></span> |
| <span data-ttu-id="1d42d-178">屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-178">properties</span></span> | <span data-ttu-id="1d42d-179">與頂點相關聯的使用者定義屬性包。</span><span class="sxs-lookup"><span data-stu-id="1d42d-179">Bag of user-defined properties associated with the vertex.</span></span> <span data-ttu-id="1d42d-180">每個屬性可以有多個值。</span><span class="sxs-lookup"><span data-stu-id="1d42d-180">Each property can have multiple values.</span></span> |
| <span data-ttu-id="1d42d-181">_partition (可設定)</span><span class="sxs-lookup"><span data-stu-id="1d42d-181">_partition (configurable)</span></span> | <span data-ttu-id="1d42d-182">頂點的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1d42d-182">The partition key of the vertex.</span></span> <span data-ttu-id="1d42d-183">可用來將圖表相應放大至多部伺服器</span><span class="sxs-lookup"><span data-stu-id="1d42d-183">Can be used to scale out graphs to multiple servers</span></span> |
| <span data-ttu-id="1d42d-184">outE</span><span class="sxs-lookup"><span data-stu-id="1d42d-184">outE</span></span> | <span data-ttu-id="1d42d-185">這包含頂點的外邊緣清單。</span><span class="sxs-lookup"><span data-stu-id="1d42d-185">This contains a list of out edges from a vertex.</span></span> <span data-ttu-id="1d42d-186">儲存頂點的相鄰資訊可以加速周遊。</span><span class="sxs-lookup"><span data-stu-id="1d42d-186">Storing the adjacency information with vertex allows for fast execution of traversals.</span></span> <span data-ttu-id="1d42d-187">邊緣會根據標籤而分組。</span><span class="sxs-lookup"><span data-stu-id="1d42d-187">Edges are grouped based on their labels.</span></span> |

<span data-ttu-id="1d42d-188">邊緣還包含下列資訊，有助於瀏覽至圖表的其他部分。</span><span class="sxs-lookup"><span data-stu-id="1d42d-188">And the edge contains the following information to help with navigation to other parts of the graph.</span></span>

| <span data-ttu-id="1d42d-189">屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-189">Property</span></span> | <span data-ttu-id="1d42d-190">說明</span><span class="sxs-lookup"><span data-stu-id="1d42d-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1d42d-191">id</span><span class="sxs-lookup"><span data-stu-id="1d42d-191">id</span></span> | <span data-ttu-id="1d42d-192">邊緣的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d42d-192">The ID for the edge.</span></span> <span data-ttu-id="1d42d-193">必須是唯一的 (適合的話，與 _partition 的值結合)</span><span class="sxs-lookup"><span data-stu-id="1d42d-193">Must be unique (in combination with the value of _partition if applicable)</span></span> |
| <span data-ttu-id="1d42d-194">標籤</span><span class="sxs-lookup"><span data-stu-id="1d42d-194">label</span></span> | <span data-ttu-id="1d42d-195">邊緣的標籤。</span><span class="sxs-lookup"><span data-stu-id="1d42d-195">The label of the edge.</span></span> <span data-ttu-id="1d42d-196">這是選擇性屬性，用來描述關聯性類型。</span><span class="sxs-lookup"><span data-stu-id="1d42d-196">This property is optional, and used to describe the relationship type.</span></span> |
| <span data-ttu-id="1d42d-197">inV</span><span class="sxs-lookup"><span data-stu-id="1d42d-197">inV</span></span> | <span data-ttu-id="1d42d-198">這包含特定邊緣的頂點清單。</span><span class="sxs-lookup"><span data-stu-id="1d42d-198">This contains a list of in vertices for an edge.</span></span> <span data-ttu-id="1d42d-199">儲存邊緣的相鄰資訊可以加速周遊的執行。</span><span class="sxs-lookup"><span data-stu-id="1d42d-199">Storing the adjacency information with the edge allows for fast execution of traversals.</span></span> <span data-ttu-id="1d42d-200">頂點會根據標籤而分組。</span><span class="sxs-lookup"><span data-stu-id="1d42d-200">Vertices are grouped based on their labels.</span></span> |
| <span data-ttu-id="1d42d-201">屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-201">properties</span></span> | <span data-ttu-id="1d42d-202">與邊緣相關聯的使用者定義屬性包。</span><span class="sxs-lookup"><span data-stu-id="1d42d-202">Bag of user-defined properties associated with the edge.</span></span> <span data-ttu-id="1d42d-203">每個屬性可以有多個值。</span><span class="sxs-lookup"><span data-stu-id="1d42d-203">Each property can have multiple values.</span></span> |

<span data-ttu-id="1d42d-204">每個屬性可以將多個值儲存在陣列中。</span><span class="sxs-lookup"><span data-stu-id="1d42d-204">Each property can store multiple values within an array.</span></span> 

| <span data-ttu-id="1d42d-205">屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-205">Property</span></span> | <span data-ttu-id="1d42d-206">說明</span><span class="sxs-lookup"><span data-stu-id="1d42d-206">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1d42d-207">value</span><span class="sxs-lookup"><span data-stu-id="1d42d-207">value</span></span> | <span data-ttu-id="1d42d-208">屬性的值</span><span class="sxs-lookup"><span data-stu-id="1d42d-208">The value of the property</span></span>

## <a name="gremlin-partitioning"></a><span data-ttu-id="1d42d-209">Gremlin 分割</span><span class="sxs-lookup"><span data-stu-id="1d42d-209">Gremlin partitioning</span></span>

<span data-ttu-id="1d42d-210">在 Azure Cosmos DB 中，圖表儲存在容器內，而容器可根據儲存體和輸送量 (以一般化每秒要求數表示) 而獨立調整。</span><span class="sxs-lookup"><span data-stu-id="1d42d-210">In Azure Cosmos DB, graphs are stored within containers that can scale independently in terms of storage and throughput (expressed in normalized requests per second).</span></span> <span data-ttu-id="1d42d-211">每個容器必須定義一個選擇性但建議的資料分割索引鍵屬性，以決定相關資料的邏輯資料分割界限。</span><span class="sxs-lookup"><span data-stu-id="1d42d-211">Each container must define an optional, but recommended partition key property that determines a logical partition boundary for related data.</span></span> <span data-ttu-id="1d42d-212">每個頂點/邊緣都必須有一個 `id` 屬性，此屬性在該資料分割索引鍵值內的實體之間是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1d42d-212">Every vertex/edge must have an `id` property that is unique for entities within that partition key value.</span></span> <span data-ttu-id="1d42d-213">[Azure Cosmos DB 中的資料分割](partition-data.md)涵蓋詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1d42d-213">The details are covered in [Partitioning in Azure Cosmos DB](partition-data.md).</span></span>

<span data-ttu-id="1d42d-214">對於 Azure Cosmos DB 中跨越多個資料分割的圖形資料，Gremlin 作業可以順暢地運作。</span><span class="sxs-lookup"><span data-stu-id="1d42d-214">Gremlin operations work seamlessly across graph data that span multiple partitions in Azure Cosmos DB.</span></span> <span data-ttu-id="1d42d-215">不過，建議您為圖表選擇的資料分割索引鍵，最好是常用作查詢中的篩選條件、有許多不同的值，而且以類似的頻率存取這些值。</span><span class="sxs-lookup"><span data-stu-id="1d42d-215">However, it is recommended to choose a partition key for your graphs that is commonly used as a filter in queries, has many distinct values, and similar frequency of access these values.</span></span> 

## <a name="gremlin-steps"></a><span data-ttu-id="1d42d-216">Gremlin 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-216">Gremlin steps</span></span>
<span data-ttu-id="1d42d-217">現在，讓我們看看 Azure Cosmos DB 支援的 Gremlin 步驟。</span><span class="sxs-lookup"><span data-stu-id="1d42d-217">Now let's look at the Gremlin steps supported by Azure Cosmos DB.</span></span> <span data-ttu-id="1d42d-218">如需 Gremlin 的完整參考，請參閱 [TinkerPop 參考](http://tinkerpop.apache.org/docs/current/reference)。</span><span class="sxs-lookup"><span data-stu-id="1d42d-218">For a complete reference on Gremlin, see [TinkerPop reference](http://tinkerpop.apache.org/docs/current/reference).</span></span>

| <span data-ttu-id="1d42d-219">步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-219">step</span></span> | <span data-ttu-id="1d42d-220">說明</span><span class="sxs-lookup"><span data-stu-id="1d42d-220">Description</span></span> | <span data-ttu-id="1d42d-221">TinkerPop 3.2 文件</span><span class="sxs-lookup"><span data-stu-id="1d42d-221">TinkerPop 3.2 Documentation</span></span> | <span data-ttu-id="1d42d-222">注意事項</span><span class="sxs-lookup"><span data-stu-id="1d42d-222">Notes</span></span> |
| --- | --- | --- | --- |
| `addE` | <span data-ttu-id="1d42d-223">在兩個頂點之間新增邊緣</span><span class="sxs-lookup"><span data-stu-id="1d42d-223">Adds an edge between two vertices</span></span> | [<span data-ttu-id="1d42d-224">addE 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-224">addE step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | <span data-ttu-id="1d42d-225">將頂點新增至圖表</span><span class="sxs-lookup"><span data-stu-id="1d42d-225">Adds a vertex to the graph</span></span> | [<span data-ttu-id="1d42d-226">addV 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-226">addV step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | <span data-ttu-id="1d42d-227">確保所有周遊都會傳回值</span><span class="sxs-lookup"><span data-stu-id="1d42d-227">Ensurest that all the traversals return a value</span></span> | [<span data-ttu-id="1d42d-228">and 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-228">and step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | <span data-ttu-id="1d42d-229">將變數指派給步驟輸出的步驟調變器</span><span class="sxs-lookup"><span data-stu-id="1d42d-229">A step modulator to assign a variable to the output of a step</span></span> | [<span data-ttu-id="1d42d-230">as 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-230">as step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | <span data-ttu-id="1d42d-231">搭配 `group` 和 `order` 一起使用的步驟調變器</span><span class="sxs-lookup"><span data-stu-id="1d42d-231">A step modulator used with `group` and `order`</span></span> | [<span data-ttu-id="1d42d-232">by 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-232">by step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | <span data-ttu-id="1d42d-233">傳回第一次有傳回結果的周遊</span><span class="sxs-lookup"><span data-stu-id="1d42d-233">Returns the first traversal that returns a result</span></span> | [<span data-ttu-id="1d42d-234">coalesce 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-234">coalesce step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | <span data-ttu-id="1d42d-235">傳回常數值。</span><span class="sxs-lookup"><span data-stu-id="1d42d-235">Returns a constant value.</span></span> <span data-ttu-id="1d42d-236">搭配 `coalesce` 使用</span><span class="sxs-lookup"><span data-stu-id="1d42d-236">Used with `coalesce`</span></span>| [<span data-ttu-id="1d42d-237">constant 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-237">constant step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | <span data-ttu-id="1d42d-238">從周遊傳回計數</span><span class="sxs-lookup"><span data-stu-id="1d42d-238">Returns the count from the traversal</span></span> | [<span data-ttu-id="1d42d-239">count 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-239">count step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | <span data-ttu-id="1d42d-240">傳回已移除重複項的值</span><span class="sxs-lookup"><span data-stu-id="1d42d-240">Returns the values with the duplicates removed</span></span> | [<span data-ttu-id="1d42d-241">dedup 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-241">dedup step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | <span data-ttu-id="1d42d-242">捨棄值 (頂點/邊緣)</span><span class="sxs-lookup"><span data-stu-id="1d42d-242">Drops the values (vertex/edge)</span></span> | [<span data-ttu-id="1d42d-243">drop 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-243">drop step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | <span data-ttu-id="1d42d-244">作為屏障來計算結果的彙總</span><span class="sxs-lookup"><span data-stu-id="1d42d-244">Acts as a barrier that computes the aggregate of results</span></span>| [<span data-ttu-id="1d42d-245">fold 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-245">fold step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | <span data-ttu-id="1d42d-246">根據指定的標籤將值分組</span><span class="sxs-lookup"><span data-stu-id="1d42d-246">Groups the values based on the labels specified</span></span>| [<span data-ttu-id="1d42d-247">group 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-247">group step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | <span data-ttu-id="1d42d-248">用於篩選屬性、頂點和邊緣。</span><span class="sxs-lookup"><span data-stu-id="1d42d-248">Used to filter properties, vertices, and edges.</span></span> <span data-ttu-id="1d42d-249">支援 `hasLabel`、`hasId`、`hasNot` 和 `has` 變體。</span><span class="sxs-lookup"><span data-stu-id="1d42d-249">Supports `hasLabel`, `hasId`, `hasNot`, and `has` variants.</span></span> | [<span data-ttu-id="1d42d-250">has 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-250">has step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | <span data-ttu-id="1d42d-251">將值插入資料流</span><span class="sxs-lookup"><span data-stu-id="1d42d-251">Inject values into a stream</span></span>| [<span data-ttu-id="1d42d-252">inject 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-252">inject step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | <span data-ttu-id="1d42d-253">用來執行使用布林運算式的篩選條件</span><span class="sxs-lookup"><span data-stu-id="1d42d-253">Used to perform a filter using a boolean expression</span></span> | [<span data-ttu-id="1d42d-254">is 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-254">is step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | <span data-ttu-id="1d42d-255">用來限制周遊中的項目數</span><span class="sxs-lookup"><span data-stu-id="1d42d-255">Used to limit number of items in the traversal</span></span>| [<span data-ttu-id="1d42d-256">limit 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-256">limit step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | <span data-ttu-id="1d42d-257">局部包裝周遊的一個區段，類似於子查詢</span><span class="sxs-lookup"><span data-stu-id="1d42d-257">Local wraps a section of a traversal, similar to a subquery</span></span> | [<span data-ttu-id="1d42d-258">local 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-258">local step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | <span data-ttu-id="1d42d-259">用來否定篩選條件</span><span class="sxs-lookup"><span data-stu-id="1d42d-259">Used to produce the negation of a filter</span></span> | [<span data-ttu-id="1d42d-260">not 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-260">not step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | <span data-ttu-id="1d42d-261">如果指定的周遊產生結果，則傳回結果，否則傳回呼叫端元素</span><span class="sxs-lookup"><span data-stu-id="1d42d-261">Returns the result of the specified traversal if it yields a result else it returns the calling element</span></span> | [<span data-ttu-id="1d42d-262">optional 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-262">optional step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | <span data-ttu-id="1d42d-263">確保至少一個周遊會傳回值</span><span class="sxs-lookup"><span data-stu-id="1d42d-263">Ensures at least one of the traversals returns a value</span></span> | [<span data-ttu-id="1d42d-264">or 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-264">or step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | <span data-ttu-id="1d42d-265">依指定的排序次序傳回結果</span><span class="sxs-lookup"><span data-stu-id="1d42d-265">Returns results in the specified sort order</span></span> | [<span data-ttu-id="1d42d-266">order 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-266">order step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | <span data-ttu-id="1d42d-267">傳回周遊的完整路徑</span><span class="sxs-lookup"><span data-stu-id="1d42d-267">Returns the full path of the traversal</span></span> | [<span data-ttu-id="1d42d-268">path 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-268">path step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | <span data-ttu-id="1d42d-269">將屬性投射為 Map</span><span class="sxs-lookup"><span data-stu-id="1d42d-269">Projects the properties as a Map</span></span> | [<span data-ttu-id="1d42d-270">project 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-270">project step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | <span data-ttu-id="1d42d-271">傳回指定之標籤的屬性</span><span class="sxs-lookup"><span data-stu-id="1d42d-271">Returns the properties for the specified labels</span></span> | [<span data-ttu-id="1d42d-272">properties 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-272">properties step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | <span data-ttu-id="1d42d-273">篩選為指定的值範圍</span><span class="sxs-lookup"><span data-stu-id="1d42d-273">Filters to the specified range of values</span></span>| [<span data-ttu-id="1d42d-274">range 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-274">range step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | <span data-ttu-id="1d42d-275">將步驟重複執行指定的次數。</span><span class="sxs-lookup"><span data-stu-id="1d42d-275">Repeats the step for the specified number of times.</span></span> <span data-ttu-id="1d42d-276">用於迴圈處理</span><span class="sxs-lookup"><span data-stu-id="1d42d-276">Used for looping</span></span> | [<span data-ttu-id="1d42d-277">repeat 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-277">repeat step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | <span data-ttu-id="1d42d-278">用於取樣周遊的結果</span><span class="sxs-lookup"><span data-stu-id="1d42d-278">Used to sample results from the traversal</span></span> | [<span data-ttu-id="1d42d-279">sample 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-279">sample step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | <span data-ttu-id="1d42d-280">用於投射周遊的結果</span><span class="sxs-lookup"><span data-stu-id="1d42d-280">Used to project results from the traversal</span></span> |  [<span data-ttu-id="1d42d-281">select 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-281">select step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | <span data-ttu-id="1d42d-282">用於來自周遊的非封鎖彙總</span><span class="sxs-lookup"><span data-stu-id="1d42d-282">Used for non-blocking aggregates from the traversal</span></span> | [<span data-ttu-id="1d42d-283">store 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-283">store step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | <span data-ttu-id="1d42d-284">將頂點的路徑彙總至樹狀目錄</span><span class="sxs-lookup"><span data-stu-id="1d42d-284">Aggregate paths from a vertex into a tree</span></span> | [<span data-ttu-id="1d42d-285">tree 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-285">tree step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | <span data-ttu-id="1d42d-286">將迭代器展開為步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-286">Unroll an iterator as a step</span></span>| [<span data-ttu-id="1d42d-287">unfold 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-287">unfold step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | <span data-ttu-id="1d42d-288">合併來自多個周遊的結果</span><span class="sxs-lookup"><span data-stu-id="1d42d-288">Merge results from multiple traversals</span></span>| [<span data-ttu-id="1d42d-289">unfold 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-289">union step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | <span data-ttu-id="1d42d-290">包含頂點和邊緣之間周遊的必要步驟 `V`、`E`、`out`、`in`、`both`、`outE`、`inE`、`bothE`、`outV`、`inV`、`bothV` 和 `otherV`</span><span class="sxs-lookup"><span data-stu-id="1d42d-290">Includes the steps necessary for traversals between vertices and edges `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, and `otherV` for</span></span> | [<span data-ttu-id="1d42d-291">vertex 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-291">vertex steps</span></span>](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | <span data-ttu-id="1d42d-292">用於篩選周遊的結果。</span><span class="sxs-lookup"><span data-stu-id="1d42d-292">Used to filter results from the traversal.</span></span> <span data-ttu-id="1d42d-293">支援 `eq`、`neq`、`lt`、`lte`、`gt`、`gte` 和 `between` 運算子</span><span class="sxs-lookup"><span data-stu-id="1d42d-293">Supports `eq`, `neq`, `lt`, `lte`, `gt`, `gte`, and `between` operators</span></span>  | [<span data-ttu-id="1d42d-294">where 步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-294">where step</span></span>](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

<span data-ttu-id="1d42d-295">根據預設，Azure Cosmos DB 的寫入最佳化引擎支援自動編製頂點和邊緣內所有屬性的索引。</span><span class="sxs-lookup"><span data-stu-id="1d42d-295">Azure Cosmos DB's write-optimized engine supports automatic indexing of all properties within vertices and edges by default.</span></span> <span data-ttu-id="1d42d-296">因此，在任何屬性上執行附有篩選條件的查詢、範圍查詢、排序或彙總時，都是從索引來處理，而且有效率地提供。</span><span class="sxs-lookup"><span data-stu-id="1d42d-296">Therefore, queries with filters, range queries, sorting, or aggregates on any property are processed from the index, and served efficiently.</span></span> <span data-ttu-id="1d42d-297">如需 Azure Cosmos DB 中索引運作方式的詳細資訊，請參閱[無從驗證結構描述的索引編製](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)一文。</span><span class="sxs-lookup"><span data-stu-id="1d42d-297">For more information on how indexing works in Azure Cosmos DB, see our paper on [schema-agnostic indexing](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d42d-298">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d42d-298">Next Steps</span></span>
* <span data-ttu-id="1d42d-299">[使用我們的 SDK](create-graph-dotnet.md) 開始建置圖表應用程式</span><span class="sxs-lookup"><span data-stu-id="1d42d-299">Get started building a graph application [using our SDKs](create-graph-dotnet.md)</span></span> 
* <span data-ttu-id="1d42d-300">深入了解 [Azure Cosmos DB 的圖表支援](graph-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1d42d-300">Learn more about [Azure Cosmos DB's graph support](graph-introduction.md)</span></span>
