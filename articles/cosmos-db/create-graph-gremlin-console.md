---
title: "Azure Cosmos DB 教學課程︰在Apache TinkerPops Gremlin 主控台中建立、查詢和周遊 | Microsoft Docs"
description: "Azure Cosmos DB 快速入門，說明如何使用 Azure Cosmos DB 圖形 API建立頂點、邊緣和查詢。"
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
ms.openlocfilehash: fd5cc93ce1ed2a8c7da090666ef539b338ac61c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-the-gremlin-console"></a><span data-ttu-id="b76c0-103">Azure Cosmos DB︰在 Gremlin 主控台中建立、查詢和周遊圖形</span><span class="sxs-lookup"><span data-stu-id="b76c0-103">Azure Cosmos DB: Create, query, and traverse a graph in the Gremlin console</span></span>

<span data-ttu-id="b76c0-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="b76c0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b76c0-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="b76c0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b76c0-106">本快速入門會示範如何使用 Azure 入口網站建立 Azure Cosmos DB 帳戶、資料庫和圖形 (容器)，然後從 [Apache TinkerPop](http://tinkerpop.apache.org) 使用 [Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)來處理圖形 API (預覽) 資料。</span><span class="sxs-lookup"><span data-stu-id="b76c0-106">This quick start demonstrates how to create an Azure Cosmos DB account, database, and graph (container) using the Azure portal and then use the [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) to work with Graph API (preview) data.</span></span> <span data-ttu-id="b76c0-107">在本教學課程中，您將建立和查詢頂點和邊緣、更新頂點屬性、查詢頂點、周遊該圖形，以及刪除頂點。</span><span class="sxs-lookup"><span data-stu-id="b76c0-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse the graph, and drop a vertex.</span></span>

![Apache Gremlin 主控台中的 Azure Cosmos DB](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="b76c0-109">Gremlin 主控台是以 Groovy/Java 為基礎並且在 Linux、Mac 和 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="b76c0-109">The Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="b76c0-110">您可以從 [Apache TinkerPop 網站](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip)進行下載。</span><span class="sxs-lookup"><span data-stu-id="b76c0-110">You can download it from the [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b76c0-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="b76c0-111">Prerequisites</span></span>

<span data-ttu-id="b76c0-112">您必須擁有 Azure 訂用帳戶，才能針對本快速入門建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b76c0-112">You need to have an Azure subscription to create an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="b76c0-113">您也需要安裝 [Gremlin 主控台](http://tinkerpop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="b76c0-113">You also need to install the [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="b76c0-114">使用 3.2.5 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="b76c0-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="b76c0-115">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="b76c0-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="b76c0-116">新增圖形</span><span class="sxs-lookup"><span data-stu-id="b76c0-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="b76c0-117"><a id="ConnectAppService"></a>連線到您的應用程式服務</span><span class="sxs-lookup"><span data-stu-id="b76c0-117"><a id="ConnectAppService"></a>Connect to your app service</span></span>
1. <span data-ttu-id="b76c0-118">啟動 Gremlin 主控台之前，請建立或修改 apache-tinkerpop-gremlin-console-3.2.5/conf 目錄中的 remote-secure.yaml 組態檔。</span><span class="sxs-lookup"><span data-stu-id="b76c0-118">Before starting the Gremlin Console, create or modify the remote-secure.yaml configuration file in the apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="b76c0-119">填入您的 host、port、username、password、connectionPool 和 serializer 組態︰</span><span class="sxs-lookup"><span data-stu-id="b76c0-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="b76c0-120">設定</span><span class="sxs-lookup"><span data-stu-id="b76c0-120">Setting</span></span>|<span data-ttu-id="b76c0-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="b76c0-121">Suggested value</span></span>|<span data-ttu-id="b76c0-122">說明</span><span class="sxs-lookup"><span data-stu-id="b76c0-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="b76c0-123">主機</span><span class="sxs-lookup"><span data-stu-id="b76c0-123">hosts</span></span>|<span data-ttu-id="b76c0-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="b76c0-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="b76c0-125">請看下方的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="b76c0-125">See screenshot below.</span></span> <span data-ttu-id="b76c0-126">這是 Azure 入口網站的 [概觀] 頁面上的 Gremlin URI 值，其以方括號括住並已移除尾端的 :443/。</span><span class="sxs-lookup"><span data-stu-id="b76c0-126">This is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="b76c0-127">此值也可以從 [金鑰] 索引標籤擷取，方法是移除 https://、將文件變更為圖形，並移除尾端的 :443/ 來使用 URI 值。</span><span class="sxs-lookup"><span data-stu-id="b76c0-127">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="b76c0-128">連接埠</span><span class="sxs-lookup"><span data-stu-id="b76c0-128">port</span></span>|<span data-ttu-id="b76c0-129">443</span><span class="sxs-lookup"><span data-stu-id="b76c0-129">443</span></span>|<span data-ttu-id="b76c0-130">設為 443。</span><span class="sxs-lookup"><span data-stu-id="b76c0-130">Set to 443.</span></span>
    <span data-ttu-id="b76c0-131">username</span><span class="sxs-lookup"><span data-stu-id="b76c0-131">username</span></span>|<span data-ttu-id="b76c0-132">您的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b76c0-132">*Your username*</span></span>|<span data-ttu-id="b76c0-133">`/dbs/<db>/colls/<coll>` 表單的資源，其中 `<db>` 是您的資料庫名稱，而 `<coll>` 是您的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="b76c0-133">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="b76c0-134">password</span><span class="sxs-lookup"><span data-stu-id="b76c0-134">password</span></span>|<span data-ttu-id="b76c0-135">您的主要金鑰</span><span class="sxs-lookup"><span data-stu-id="b76c0-135">*Your primary key*</span></span>| <span data-ttu-id="b76c0-136">請看下方的第二個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="b76c0-136">See second screenshot below.</span></span> <span data-ttu-id="b76c0-137">這是您的主要金鑰，可以從 Azure 入口網站 [金鑰] 頁面的 [主鑰金鑰] 方塊中擷取。</span><span class="sxs-lookup"><span data-stu-id="b76c0-137">This is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="b76c0-138">使用方塊左側的 [複製] 按鈕來複製此值。</span><span class="sxs-lookup"><span data-stu-id="b76c0-138">Use the copy button on the left side of the box to copy the value.</span></span>
    <span data-ttu-id="b76c0-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="b76c0-139">connectionPool</span></span>|<span data-ttu-id="b76c0-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="b76c0-140">{enableSsl: true}</span></span>|<span data-ttu-id="b76c0-141">SSL 的連線集區設定。</span><span class="sxs-lookup"><span data-stu-id="b76c0-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="b76c0-142">序列化程式</span><span class="sxs-lookup"><span data-stu-id="b76c0-142">serializer</span></span>|<span data-ttu-id="b76c0-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="b76c0-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="b76c0-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="b76c0-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="b76c0-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="b76c0-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="b76c0-146">設定此值，並在貼入此值時刪除任何 `\n` 分行符號。</span><span class="sxs-lookup"><span data-stu-id="b76c0-146">Set to this value and delete any `\n` line breaks when pasting in the value.</span></span>

    <span data-ttu-id="b76c0-147">對於主機值，從 [概觀] 頁面複製 [Gremlin URI] 值：![在 Azure 入口網站的 [概觀] 頁面上檢視和複製 Gremlin URI 值](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="b76c0-147">For the hosts value, copy the **Gremlin URI** value from the **Overview** page: ![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="b76c0-148">對於密碼值，從 [金鑰] 頁面複製 [主要金鑰]：![在 Azure 入口網站的 [金鑰] 頁面上檢視和複製主要金鑰](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="b76c0-148">For the password value, copy the **Primary key** from the **Keys** page: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="b76c0-149">在您的終端機執行 `bin/gremlin.bat` 或 `bin/gremlin.sh`，以啟動 [Gremlin 主控台](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="b76c0-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` to start the [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="b76c0-150">在您的終端機執行 `:remote connect tinkerpop.server conf/remote-secure.yaml`，以連線到您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="b76c0-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` to connect to your app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="b76c0-151">如果您收到 `No appenders could be found for logger` 錯誤，確定您如步驟 2 所述更新了 remote-secure.yaml 檔案中的序列化程式值。</span><span class="sxs-lookup"><span data-stu-id="b76c0-151">If you receive the error `No appenders could be found for logger` ensure that you updated the serializer value in the remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="b76c0-152">太棒了！</span><span class="sxs-lookup"><span data-stu-id="b76c0-152">Great!</span></span> <span data-ttu-id="b76c0-153">現在已完成安裝程式，讓我們開始執行一些主控台命令。</span><span class="sxs-lookup"><span data-stu-id="b76c0-153">Now that we finished the setup, let's start running some console commands.</span></span>

<span data-ttu-id="b76c0-154">我們來試試簡單的 count() 命令。</span><span class="sxs-lookup"><span data-stu-id="b76c0-154">Let's try a simple count() command.</span></span> <span data-ttu-id="b76c0-155">在提示字元中，將下列內容輸入到主控台：</span><span class="sxs-lookup"><span data-stu-id="b76c0-155">Type the following into the console at the prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="b76c0-156">請注意，`:>` 位於 `g.V().count()` 文字前面？</span><span class="sxs-lookup"><span data-stu-id="b76c0-156">Notice the `:>` that precedes the `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="b76c0-157">這是您需要輸入之命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="b76c0-157">This is part of the command you need to type.</span></span> <span data-ttu-id="b76c0-158">使用 Gremlin 主控台時請務必搭配 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="b76c0-158">It is important when using the Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="b76c0-159">省略此 `:>` 前置詞會指示主控台在本機執行命令，通常是針對記憶體中的圖形。</span><span class="sxs-lookup"><span data-stu-id="b76c0-159">Omitting this `:>` prefix instructs the console to execute the command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="b76c0-160">使用此 `:>` 會告訴主控台要執行遠端命令，在此案例中是針對 Cosmos DB (localhost 模擬器或是 > Azure 執行個體)。</span><span class="sxs-lookup"><span data-stu-id="b76c0-160">Using this `:>` tells the console to execute a remote command, in this case against Cosmos DB (either the localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="b76c0-161">建立頂點和邊緣</span><span class="sxs-lookup"><span data-stu-id="b76c0-161">Create vertices and edges</span></span>

<span data-ttu-id="b76c0-162">首先我們會新增五個人員頂點 Thomas、Mary Kay、Robin、Ben 和 Jack。</span><span class="sxs-lookup"><span data-stu-id="b76c0-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="b76c0-163">輸入 (Thomas)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="b76c0-164">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="b76c0-165">輸入 (Mary Kay)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="b76c0-166">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="b76c0-167">輸入 (Robin)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="b76c0-168">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="b76c0-169">輸入 (Ben)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="b76c0-170">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="b76c0-171">輸入 (Jack)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="b76c0-172">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="b76c0-173">接下來，我們會新增人員之間關聯性的邊緣。</span><span class="sxs-lookup"><span data-stu-id="b76c0-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="b76c0-174">輸入 (Thomas -> Mary Kay)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="b76c0-175">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="b76c0-176">輸入 (Thomas -> Robin)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="b76c0-177">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="b76c0-178">輸入 (Robin -> Ben)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="b76c0-179">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="b76c0-180">更新頂點</span><span class="sxs-lookup"><span data-stu-id="b76c0-180">Update a vertex</span></span>

<span data-ttu-id="b76c0-181">我們會以新的年齡 45 更新 Thomas 頂點。</span><span class="sxs-lookup"><span data-stu-id="b76c0-181">Let's update the *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="b76c0-182">輸入：</span><span class="sxs-lookup"><span data-stu-id="b76c0-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="b76c0-183">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="b76c0-184">查詢圖形</span><span class="sxs-lookup"><span data-stu-id="b76c0-184">Query your graph</span></span>

<span data-ttu-id="b76c0-185">現在，我們會對您的圖形執行各種查詢。</span><span class="sxs-lookup"><span data-stu-id="b76c0-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="b76c0-186">首先，我們會使用篩選條件嘗試查詢，只傳回超過 40 歲的人員。</span><span class="sxs-lookup"><span data-stu-id="b76c0-186">First, let's try a query with a filter to return only people who are older than 40 years old.</span></span>

<span data-ttu-id="b76c0-187">輸入 (篩選查詢)︰</span><span class="sxs-lookup"><span data-stu-id="b76c0-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="b76c0-188">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="b76c0-189">接下來，我們會預測超過 40 歲的第一個人員名稱。</span><span class="sxs-lookup"><span data-stu-id="b76c0-189">Next, let's project the first name for the people who are older than 40 years old.</span></span>

<span data-ttu-id="b76c0-190">輸入 (篩選 + 預測查詢)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="b76c0-191">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="b76c0-192">查詢圖形</span><span class="sxs-lookup"><span data-stu-id="b76c0-192">Traverse your graph</span></span>

<span data-ttu-id="b76c0-193">我們會周遊圖形，以傳回 Thomas 的所有朋友。</span><span class="sxs-lookup"><span data-stu-id="b76c0-193">Let's traverse the graph to return all of Thomas's friends.</span></span>

<span data-ttu-id="b76c0-194">輸入 (Thomas 的朋友)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="b76c0-195">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="b76c0-196">接下來，我們會取得下一層的頂點。</span><span class="sxs-lookup"><span data-stu-id="b76c0-196">Next, let's get the next layer of vertices.</span></span> <span data-ttu-id="b76c0-197">周遊圖形，以傳回 Thomas 朋友的所有朋友。</span><span class="sxs-lookup"><span data-stu-id="b76c0-197">Traverse the graph to return all the friends of Thomas's friends.</span></span>

<span data-ttu-id="b76c0-198">輸入 (Thomas 朋友的朋友)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="b76c0-199">輸出：</span><span class="sxs-lookup"><span data-stu-id="b76c0-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="b76c0-200">刪除頂點</span><span class="sxs-lookup"><span data-stu-id="b76c0-200">Drop a vertex</span></span>

<span data-ttu-id="b76c0-201">我們現在會從圖形資料庫中刪除頂點。</span><span class="sxs-lookup"><span data-stu-id="b76c0-201">Let's now delete a vertex from the graph database.</span></span>

<span data-ttu-id="b76c0-202">輸入 (置放 Jack 頂點)：</span><span class="sxs-lookup"><span data-stu-id="b76c0-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="b76c0-203">清除圖形</span><span class="sxs-lookup"><span data-stu-id="b76c0-203">Clear your graph</span></span>

<span data-ttu-id="b76c0-204">最後，我們會清除所有頂點和邊緣的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b76c0-204">Finally, let's clear the database of all vertices and edges.</span></span>

<span data-ttu-id="b76c0-205">輸入：</span><span class="sxs-lookup"><span data-stu-id="b76c0-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="b76c0-206">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b76c0-206">Congratulations!</span></span> <span data-ttu-id="b76c0-207">您已經完成此 Azure Cosmos DB：圖形 API 教學課程！</span><span class="sxs-lookup"><span data-stu-id="b76c0-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="b76c0-208">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="b76c0-208">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b76c0-209">清除資源</span><span class="sxs-lookup"><span data-stu-id="b76c0-209">Clean up resources</span></span>

<span data-ttu-id="b76c0-210">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="b76c0-210">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>  

1. <span data-ttu-id="b76c0-211">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="b76c0-211">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="b76c0-212">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="b76c0-212">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b76c0-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b76c0-213">Next steps</span></span>

<span data-ttu-id="b76c0-214">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶、如何使用 [資料總管] 來建立圖形、如何建立頂點和邊緣，以及如何使用 Gremlin 主控台來周遊圖形。</span><span class="sxs-lookup"><span data-stu-id="b76c0-214">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, create vertices and edges, and traverse your graph using the Gremlin console.</span></span> <span data-ttu-id="b76c0-215">您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。</span><span class="sxs-lookup"><span data-stu-id="b76c0-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b76c0-216">使用 Gremlin 進行查詢</span><span class="sxs-lookup"><span data-stu-id="b76c0-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
