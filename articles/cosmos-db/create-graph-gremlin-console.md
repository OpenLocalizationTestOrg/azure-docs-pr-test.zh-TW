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
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a><span data-ttu-id="d0304-103">Azure Cosmos DB： 建立、 查詢和周遊 hello Gremlin 主控台中的圖形</span><span class="sxs-lookup"><span data-stu-id="d0304-103">Azure Cosmos DB: Create, query, and traverse a graph in hello Gremlin console</span></span>

<span data-ttu-id="d0304-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="d0304-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d0304-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="d0304-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d0304-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 資料庫和圖形 （容器） 使用 hello Azure 入口網站，然後使用 hello [Gremlin 主控台](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console)從[Apache TinkerPop](http://tinkerpop.apache.org) toowork 與圖形 API （預覽） 資料。</span><span class="sxs-lookup"><span data-stu-id="d0304-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal and then use hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) toowork with Graph API (preview) data.</span></span> <span data-ttu-id="d0304-107">在本教學課程中，您建立及查詢頂點和邊緣、 更新頂點屬性，會查詢頂點、 周遊 hello 圖形，並卸除頂點。</span><span class="sxs-lookup"><span data-stu-id="d0304-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse hello graph, and drop a vertex.</span></span>

![從 hello Apache Gremlin 主控台 azure Cosmos DB](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="d0304-109">hello Gremlin 主控台是 Groovy/Java 型和 Linux、 Mac 和 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="d0304-109">hello Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="d0304-110">您可以從 hello [Apache TinkerPop 網站](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip)。</span><span class="sxs-lookup"><span data-stu-id="d0304-110">You can download it from hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0304-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d0304-111">Prerequisites</span></span>

<span data-ttu-id="d0304-112">您需要 Azure 訂用帳戶 toocreate Azure Cosmos DB 帳戶 toohave 本快速入門。</span><span class="sxs-lookup"><span data-stu-id="d0304-112">You need toohave an Azure subscription toocreate an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="d0304-113">您也需要 tooinstall hello [Gremlin 主控台](http://tinkerpop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="d0304-113">You also need tooinstall hello [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="d0304-114">使用 3.2.5 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="d0304-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="d0304-115">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="d0304-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="d0304-116">新增圖形</span><span class="sxs-lookup"><span data-stu-id="d0304-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="d0304-117"><a id="ConnectAppService"></a>連接 tooyour 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="d0304-117"><a id="ConnectAppService"></a>Connect tooyour app service</span></span>
1. <span data-ttu-id="d0304-118">開始之前 hello Gremlin 主控台、 建立或修改 hello apache-tinkerpop-gremlin-console-3.2.5/conf 目錄中的 hello 遠端 secure.yaml 組態檔。</span><span class="sxs-lookup"><span data-stu-id="d0304-118">Before starting hello Gremlin Console, create or modify hello remote-secure.yaml configuration file in hello apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="d0304-119">填入您的 host、port、username、password、connectionPool 和 serializer 組態︰</span><span class="sxs-lookup"><span data-stu-id="d0304-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="d0304-120">設定</span><span class="sxs-lookup"><span data-stu-id="d0304-120">Setting</span></span>|<span data-ttu-id="d0304-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="d0304-121">Suggested value</span></span>|<span data-ttu-id="d0304-122">說明</span><span class="sxs-lookup"><span data-stu-id="d0304-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="d0304-123">主機</span><span class="sxs-lookup"><span data-stu-id="d0304-123">hosts</span></span>|<span data-ttu-id="d0304-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="d0304-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="d0304-125">請看下方的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="d0304-125">See screenshot below.</span></span> <span data-ttu-id="d0304-126">這是在 hello Azure 入口網站，以方括號，以 hello 尾端 hello 概觀 頁面上的 hello Gremlin URI 值： 443 / 已移除。</span><span class="sxs-lookup"><span data-stu-id="d0304-126">This is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="d0304-127">此值也可以擷取從 hello 金鑰 索引標籤，移除 https://、 變更文件 toographs 並移除尾端 hello 使用 hello URI 值： 443 /。</span><span class="sxs-lookup"><span data-stu-id="d0304-127">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="d0304-128">連接埠</span><span class="sxs-lookup"><span data-stu-id="d0304-128">port</span></span>|<span data-ttu-id="d0304-129">443</span><span class="sxs-lookup"><span data-stu-id="d0304-129">443</span></span>|<span data-ttu-id="d0304-130">設定 too443。</span><span class="sxs-lookup"><span data-stu-id="d0304-130">Set too443.</span></span>
    <span data-ttu-id="d0304-131">username</span><span class="sxs-lookup"><span data-stu-id="d0304-131">username</span></span>|<span data-ttu-id="d0304-132">您的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d0304-132">*Your username*</span></span>|<span data-ttu-id="d0304-133">hello hello 形式的資源`/dbs/<db>/colls/<coll>`其中`<db>`是您的資料庫名稱和`<coll>`集合名稱。</span><span class="sxs-lookup"><span data-stu-id="d0304-133">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="d0304-134">password</span><span class="sxs-lookup"><span data-stu-id="d0304-134">password</span></span>|<span data-ttu-id="d0304-135">您的主要金鑰</span><span class="sxs-lookup"><span data-stu-id="d0304-135">*Your primary key*</span></span>| <span data-ttu-id="d0304-136">請看下方的第二個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="d0304-136">See second screenshot below.</span></span> <span data-ttu-id="d0304-137">這是 hello 的您可以擷取 hello 金鑰 頁面上 hello 主要金鑰 方塊中的 Azure 入口網站的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="d0304-137">This is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="d0304-138">在左側 hello toocopy hello 值 hello 使用 hello [複製] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d0304-138">Use hello copy button on hello left side of hello box toocopy hello value.</span></span>
    <span data-ttu-id="d0304-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="d0304-139">connectionPool</span></span>|<span data-ttu-id="d0304-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="d0304-140">{enableSsl: true}</span></span>|<span data-ttu-id="d0304-141">SSL 的連線集區設定。</span><span class="sxs-lookup"><span data-stu-id="d0304-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="d0304-142">序列化程式</span><span class="sxs-lookup"><span data-stu-id="d0304-142">serializer</span></span>|<span data-ttu-id="d0304-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="d0304-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="d0304-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="d0304-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="d0304-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="d0304-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="d0304-146">設定 toothis 值，並刪除任何`\n`分行符號 hello 值中貼上時。</span><span class="sxs-lookup"><span data-stu-id="d0304-146">Set toothis value and delete any `\n` line breaks when pasting in hello value.</span></span>

    <span data-ttu-id="d0304-147">Hello 主機值，複製 [hello **Gremlin URI**值從 hello**概觀**頁面： ![hello Azure 入口網站 hello 概觀] 頁面上的檢視與複製 hello Gremlin URI 值](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="d0304-147">For hello hosts value, copy hello **Gremlin URI** value from hello **Overview** page: ![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="d0304-148">Hello 密碼值，複製 [hello**主索引鍵**從 hello**金鑰**頁面：![主索引鍵 hello Azure 入口網站中的檢視與複製金鑰] 頁面](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="d0304-148">For hello password value, copy hello **Primary key** from hello **Keys** page: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="d0304-149">在您的終端機中，執行`bin/gremlin.bat`或`bin/gremlin.sh`toostart hello [Gremlin 主控台](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="d0304-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="d0304-150">在您的終端機中，執行`:remote connect tinkerpop.server conf/remote-secure.yaml`tooconnect tooyour 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="d0304-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="d0304-151">如果您收到 hello 錯誤`No appenders could be found for logger`確定您在步驟 2 中所述更新 hello 遠端 secure.yaml 檔案中的 hello 序列化程式值。</span><span class="sxs-lookup"><span data-stu-id="d0304-151">If you receive hello error `No appenders could be found for logger` ensure that you updated hello serializer value in hello remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="d0304-152">太棒了！</span><span class="sxs-lookup"><span data-stu-id="d0304-152">Great!</span></span> <span data-ttu-id="d0304-153">既然我們完成 hello 安裝程式，讓我們開始執行某些主控台命令。</span><span class="sxs-lookup"><span data-stu-id="d0304-153">Now that we finished hello setup, let's start running some console commands.</span></span>

<span data-ttu-id="d0304-154">我們來試試簡單的 count() 命令。</span><span class="sxs-lookup"><span data-stu-id="d0304-154">Let's try a simple count() command.</span></span> <span data-ttu-id="d0304-155">Hello 主控台在 hello 提示字元中輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d0304-155">Type hello following into hello console at hello prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="d0304-156">請注意 hello`:>`前面 hello`g.V().count()`文字嗎？</span><span class="sxs-lookup"><span data-stu-id="d0304-156">Notice hello `:>` that precedes hello `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="d0304-157">這是您需要 tootype hello 命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="d0304-157">This is part of hello command you need tootype.</span></span> <span data-ttu-id="d0304-158">請務必 hello Gremlin 主控台中，使用 Azure Cosmos DB 時。</span><span class="sxs-lookup"><span data-stu-id="d0304-158">It is important when using hello Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="d0304-159">省略此`:>`前置詞會指示 hello 主控台 tooexecute hello 命令在本機，通常針對在記憶體中的圖形。</span><span class="sxs-lookup"><span data-stu-id="d0304-159">Omitting this `:>` prefix instructs hello console tooexecute hello command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="d0304-160">使用此`:>`會告知 hello 主控台 tooexecute 遠端命令，在此情況下針對 Cosmos DB (任一 hello localhost 的模擬器，或 > Azure 執行個體)。</span><span class="sxs-lookup"><span data-stu-id="d0304-160">Using this `:>` tells hello console tooexecute a remote command, in this case against Cosmos DB (either hello localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="d0304-161">建立頂點和邊緣</span><span class="sxs-lookup"><span data-stu-id="d0304-161">Create vertices and edges</span></span>

<span data-ttu-id="d0304-162">首先我們會新增五個人員頂點 Thomas、Mary Kay、Robin、Ben 和 Jack。</span><span class="sxs-lookup"><span data-stu-id="d0304-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="d0304-163">輸入 (Thomas)：</span><span class="sxs-lookup"><span data-stu-id="d0304-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="d0304-164">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="d0304-165">輸入 (Mary Kay)：</span><span class="sxs-lookup"><span data-stu-id="d0304-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="d0304-166">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="d0304-167">輸入 (Robin)：</span><span class="sxs-lookup"><span data-stu-id="d0304-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="d0304-168">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="d0304-169">輸入 (Ben)：</span><span class="sxs-lookup"><span data-stu-id="d0304-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="d0304-170">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="d0304-171">輸入 (Jack)：</span><span class="sxs-lookup"><span data-stu-id="d0304-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="d0304-172">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="d0304-173">接下來，我們會新增人員之間關聯性的邊緣。</span><span class="sxs-lookup"><span data-stu-id="d0304-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="d0304-174">輸入 (Thomas -> Mary Kay)：</span><span class="sxs-lookup"><span data-stu-id="d0304-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="d0304-175">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="d0304-176">輸入 (Thomas -> Robin)：</span><span class="sxs-lookup"><span data-stu-id="d0304-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="d0304-177">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="d0304-178">輸入 (Robin -> Ben)：</span><span class="sxs-lookup"><span data-stu-id="d0304-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="d0304-179">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="d0304-180">更新頂點</span><span class="sxs-lookup"><span data-stu-id="d0304-180">Update a vertex</span></span>

<span data-ttu-id="d0304-181">讓我們更新 hello *Thomas*與新的存留期的頂點*45*。</span><span class="sxs-lookup"><span data-stu-id="d0304-181">Let's update hello *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="d0304-182">輸入：</span><span class="sxs-lookup"><span data-stu-id="d0304-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="d0304-183">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="d0304-184">查詢圖形</span><span class="sxs-lookup"><span data-stu-id="d0304-184">Query your graph</span></span>

<span data-ttu-id="d0304-185">現在，我們會對您的圖形執行各種查詢。</span><span class="sxs-lookup"><span data-stu-id="d0304-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="d0304-186">首先，我們再試一次查詢的篩選器 tooreturn 只有人超過 40 年。</span><span class="sxs-lookup"><span data-stu-id="d0304-186">First, let's try a query with a filter tooreturn only people who are older than 40 years old.</span></span>

<span data-ttu-id="d0304-187">輸入 (篩選查詢)︰</span><span class="sxs-lookup"><span data-stu-id="d0304-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="d0304-188">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="d0304-189">接下來，讓我們專案 hello 名字人士 hello 超過 40 年。</span><span class="sxs-lookup"><span data-stu-id="d0304-189">Next, let's project hello first name for hello people who are older than 40 years old.</span></span>

<span data-ttu-id="d0304-190">輸入 (篩選 + 預測查詢)：</span><span class="sxs-lookup"><span data-stu-id="d0304-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="d0304-191">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="d0304-192">查詢圖形</span><span class="sxs-lookup"><span data-stu-id="d0304-192">Traverse your graph</span></span>

<span data-ttu-id="d0304-193">讓我們來周遊 hello 圖形 tooreturn 所有 Thomas 的朋友。</span><span class="sxs-lookup"><span data-stu-id="d0304-193">Let's traverse hello graph tooreturn all of Thomas's friends.</span></span>

<span data-ttu-id="d0304-194">輸入 (Thomas 的朋友)：</span><span class="sxs-lookup"><span data-stu-id="d0304-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="d0304-195">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="d0304-196">接下來，讓我們協助 hello 下一層的頂點。</span><span class="sxs-lookup"><span data-stu-id="d0304-196">Next, let's get hello next layer of vertices.</span></span> <span data-ttu-id="d0304-197">周遊 hello 圖形 tooreturn 所有 hello 之朋友的朋友 Thomas 的。</span><span class="sxs-lookup"><span data-stu-id="d0304-197">Traverse hello graph tooreturn all hello friends of Thomas's friends.</span></span>

<span data-ttu-id="d0304-198">輸入 (Thomas 朋友的朋友)：</span><span class="sxs-lookup"><span data-stu-id="d0304-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="d0304-199">輸出：</span><span class="sxs-lookup"><span data-stu-id="d0304-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="d0304-200">刪除頂點</span><span class="sxs-lookup"><span data-stu-id="d0304-200">Drop a vertex</span></span>

<span data-ttu-id="d0304-201">我們現在頂點從資料庫中刪除 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="d0304-201">Let's now delete a vertex from hello graph database.</span></span>

<span data-ttu-id="d0304-202">輸入 (置放 Jack 頂點)：</span><span class="sxs-lookup"><span data-stu-id="d0304-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="d0304-203">清除圖形</span><span class="sxs-lookup"><span data-stu-id="d0304-203">Clear your graph</span></span>

<span data-ttu-id="d0304-204">最後，讓我們來清除 hello 資料庫的所有頂點和邊緣。</span><span class="sxs-lookup"><span data-stu-id="d0304-204">Finally, let's clear hello database of all vertices and edges.</span></span>

<span data-ttu-id="d0304-205">輸入：</span><span class="sxs-lookup"><span data-stu-id="d0304-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="d0304-206">恭喜！</span><span class="sxs-lookup"><span data-stu-id="d0304-206">Congratulations!</span></span> <span data-ttu-id="d0304-207">您已經完成此 Azure Cosmos DB：圖形 API 教學課程！</span><span class="sxs-lookup"><span data-stu-id="d0304-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="d0304-208">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="d0304-208">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="d0304-209">清除資源</span><span class="sxs-lookup"><span data-stu-id="d0304-209">Clean up resources</span></span>

<span data-ttu-id="d0304-210">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d0304-210">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>  

1. <span data-ttu-id="d0304-211">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d0304-211">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="d0304-212">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="d0304-212">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0304-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0304-213">Next steps</span></span>

<span data-ttu-id="d0304-214">本快速入門中，您已經學會 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管圖形、 建立頂點和邊緣、 以及周遊使用 hello Gremlin 主控台程式圖形的方式。</span><span class="sxs-lookup"><span data-stu-id="d0304-214">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, create vertices and edges, and traverse your graph using hello Gremlin console.</span></span> <span data-ttu-id="d0304-215">您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。</span><span class="sxs-lookup"><span data-stu-id="d0304-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0304-216">使用 Gremlin 進行查詢</span><span class="sxs-lookup"><span data-stu-id="d0304-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
