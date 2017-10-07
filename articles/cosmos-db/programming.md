---
title: "Azure Cosmos DB 的 aaaServer 端 JavaScript 程式設計 |Microsoft 文件"
description: "了解如何 toouse Azure Cosmos DB toowrite 預存程序、 資料庫觸發程序，以及使用者定義函數 (Udf) 在 JavaScript 中。 取得資料庫程式設計秘訣等等。"
keywords: "資料庫觸發程序, 預存程序, 預存程序, 資料庫程式, sproc, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="5eb53-105">Azure Cosmos DB 伺服器端程式設計：預存程序、資料庫觸發程序和 UDF</span><span class="sxs-lookup"><span data-stu-id="5eb53-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="5eb53-106">了解 Azure Cosmos DB 的語言整合式、交易式 JavaScript 執行如何讓開發人員使用 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript 以原生方式撰寫**預存程序**、**觸發程序**及**使用者定義函數 (UDF)**。</span><span class="sxs-lookup"><span data-stu-id="5eb53-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="5eb53-107">這可讓您 toowrite 資料庫程式應用程式邏輯出貨並直接在 hello 資料庫儲存體磁碟分割上執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="5eb53-108">我們建議您取得啟動下列看 hello 視訊，Andrew Liu 其中提供簡單介紹 tooCosmos DB 的資料庫伺服器端程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="5eb53-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="5eb53-109">然後，傳回 toothis 發行項，您將在此學習 hello 答案 toohello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="5eb53-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="5eb53-110">如何使用 JavaScript 撰寫預存程序、觸發程序或 UDF？</span><span class="sxs-lookup"><span data-stu-id="5eb53-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="5eb53-111">Cosmos DB 如何提供 ACID 保證？</span><span class="sxs-lookup"><span data-stu-id="5eb53-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="5eb53-112">如何在 Cosmos DB 中執行交易工作？</span><span class="sxs-lookup"><span data-stu-id="5eb53-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="5eb53-113">什麼是預先觸發程序和後續觸發程序？其撰寫方法為何？</span><span class="sxs-lookup"><span data-stu-id="5eb53-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="5eb53-114">如何註冊及使用 HTTP 以 RESTful 方式執行預存程序、觸發程序或 UDF？</span><span class="sxs-lookup"><span data-stu-id="5eb53-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="5eb53-115">可以使用哪些 Cosmos DB Sdk 可用 toocreate 或執行預存程序、 觸發程序和 Udf？</span><span class="sxs-lookup"><span data-stu-id="5eb53-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="5eb53-116">簡介 tooStored 程序和 UDF 程式設計</span><span class="sxs-lookup"><span data-stu-id="5eb53-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="5eb53-117">這種方法的*"做為現代天 T-SQL JavaScript"* hello 變得複雜型別系統不符和物件關聯式對應之技術的應用程式開發人員會釋出。</span><span class="sxs-lookup"><span data-stu-id="5eb53-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="5eb53-118">它也有一些優點可以利用的 toobuild 豐富的應用程式的內建函式：</span><span class="sxs-lookup"><span data-stu-id="5eb53-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="5eb53-119">**程序的邏輯：** JavaScript 做為高層級的程式設計語言，提供豐富且熟悉的介面 tooexpress 商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="5eb53-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="5eb53-120">您可以執行複雜的作業更接近 toohello 資料的順序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="5eb53-121">**不可部分完成的交易**：Cosmos DB 可確保在單一預存程序或觸發程序內執行的資料庫作業成為不可部分完成的作業。</span><span class="sxs-lookup"><span data-stu-id="5eb53-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="5eb53-122">這可讓應用程式合併單一批次中的相關作業，讓所有作業不是一起成功就是一起失敗。</span><span class="sxs-lookup"><span data-stu-id="5eb53-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="5eb53-123">**效能：** hello 緩衝區中的 hello 事實 JSON 是在本質上對應的 toohello Javascript 語言類型系統，而且也可讓數個最佳化類似 JSON 的延遲具體化 hello Cosmos DB 中的儲存空間的基本單位文件集區，使其可以使用點播 toohello 執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="5eb53-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="5eb53-124">有多個傳送的商務邏輯 toohello 資料庫相關聯的效能優勢：</span><span class="sxs-lookup"><span data-stu-id="5eb53-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="5eb53-125">批次處理 - 開發人員可以群組多個作業 (例如插入)，大量進行提交。</span><span class="sxs-lookup"><span data-stu-id="5eb53-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="5eb53-126">hello 網路流量延遲成本，並大幅降低 hello 存放區負擔 toocreate 個別交易。</span><span class="sxs-lookup"><span data-stu-id="5eb53-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="5eb53-127">先行編譯-Cosmos DB 先行編譯預存程序、 觸發程序和使用者定義函數 (Udf) tooavoid 每次叫用 JavaScript 編譯成本。</span><span class="sxs-lookup"><span data-stu-id="5eb53-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="5eb53-128">hello hello 程序邏輯建置 hello 位元組的程式碼的額外負荷分期固定 tooa 最小值。</span><span class="sxs-lookup"><span data-stu-id="5eb53-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="5eb53-129">排序 - 許多作業都需要副作用 (「觸發程序」)，其可能涉及執行一項或多項次要儲存作業。</span><span class="sxs-lookup"><span data-stu-id="5eb53-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="5eb53-130">除了不可部份完成性，這是更好的效能時移動 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5eb53-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="5eb53-131">**封裝：**預存程序可能會在一個地方使用的 toogroup 商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="5eb53-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="5eb53-132">這有兩個優點：</span><span class="sxs-lookup"><span data-stu-id="5eb53-132">This has two advantages:</span></span>
  * <span data-ttu-id="5eb53-133">它會加入抽象層之上 hello 未經處理資料，可讓資料架構設計人員 tooevolve hello 資料獨立於其應用程式。</span><span class="sxs-lookup"><span data-stu-id="5eb53-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="5eb53-134">無結構描述，因為可能需要 toobe 本意 hello 應用程式，如果有與資料 toodeal 直接 toohello 脆弱假設 hello 資料時，這是特別有用。</span><span class="sxs-lookup"><span data-stu-id="5eb53-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="5eb53-135">這個抽象層可讓企業 hello 指令碼中的 hello 存取可簡化程序，確保資料安全。</span><span class="sxs-lookup"><span data-stu-id="5eb53-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="5eb53-136">hello 建立和執行資料庫觸發程序、 預存程序和自訂查詢運算子透過支援 hello [REST API](/rest/api/documentdb/)， [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases)，和[用戶端 Sdk](documentdb-sdk-dotnet.md)用於多種平台包括.NET、 Node.js 和 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="5eb53-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="5eb53-137">本教學課程使用 hello [Q 承諾 Node.js SDK](http://azure.github.io/azure-documentdb-node-q/) tooillustrate 語法和使用方式的預存程序、 觸發程序和 Udf。</span><span class="sxs-lookup"><span data-stu-id="5eb53-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="5eb53-138">預存程序</span><span class="sxs-lookup"><span data-stu-id="5eb53-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="5eb53-139">範例：撰寫簡易預存程序</span><span class="sxs-lookup"><span data-stu-id="5eb53-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="5eb53-140">我們先來看看簡單的預存程序，此程序會傳回 "Hello World" 回應。</span><span class="sxs-lookup"><span data-stu-id="5eb53-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="5eb53-141">預存程序是按照集合來註冊，而且可以作用於該集合中現有的文件和附件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="5eb53-142">hello 下列程式碼片段示範如何 tooregister hello helloWorld 預存程序集合。</span><span class="sxs-lookup"><span data-stu-id="5eb53-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="5eb53-143">Hello 預存程序註冊後，我們可以執行對 hello 集合，以了解回在 hello 用戶端的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="5eb53-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="5eb53-144">hello 內容物件提供存取 tooall 作業可對 Cosmos 資料庫儲存體，以及存取 toohello 要求和回應物件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="5eb53-145">在此情況下，我們使用 hello 回應物件 tooset hello 主體送出後 toohello 用戶端 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5eb53-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="5eb53-146">如需詳細資訊，請參閱 toohello [Azure Cosmos DB JavaScript 伺服器 SDK 文件](http://azure.github.io/azure-documentdb-js-server/)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="5eb53-147">讓我們延伸此範例，並加入多個資料庫相關的功能 toohello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="5eb53-148">預存程序可以建立、 更新、 讀取、 查詢及刪除文件與 hello 集合內的附件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="5eb53-149">範例： 撰寫預存程序 toocreate 文件</span><span class="sxs-lookup"><span data-stu-id="5eb53-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="5eb53-150">hello 的下一個程式碼片段顯示 toouse hello 內容物件 toointeract Cosmos DB 資源的方式。</span><span class="sxs-lookup"><span data-stu-id="5eb53-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="5eb53-151">這個預存程序會當做輸入 documentToCreate，hello 目前集合中建立文件 toobe hello 主體。</span><span class="sxs-lookup"><span data-stu-id="5eb53-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="5eb53-152">所有這類作業都是非同步的，而且需仰賴 JavaScript 函數回呼。</span><span class="sxs-lookup"><span data-stu-id="5eb53-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="5eb53-153">hello 作業失敗，而且建立物件的一個 hello 回呼函式會有兩個參數，一個用於 hello 物件時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5eb53-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="5eb53-154">在 hello 回呼的使用者可以處理 hello 例外狀況，或擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="5eb53-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="5eb53-155">假如未提供的回呼，但發生錯誤，hello Azure Cosmos DB 執行階段會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="5eb53-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="5eb53-156">Hello 上述範例中，在 hello 回呼擲回錯誤，如果 hello 作業失敗。</span><span class="sxs-lookup"><span data-stu-id="5eb53-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="5eb53-157">否則，它會設定 hello 識別碼 hello 做為 hello 回應 toohello 用戶端 hello 主體建立文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="5eb53-158">此預存程序與輸入參數搭配執行的方式如下。</span><span class="sxs-lookup"><span data-stu-id="5eb53-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="5eb53-159">請注意，這個預存程序可修改的 tootake 文件本文的陣列作為輸入及建立它們全都在 hello 相同預存程序執行，而不是多個網路要求 toocreate 每個個別。</span><span class="sxs-lookup"><span data-stu-id="5eb53-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="5eb53-160">這可以是使用的 tooimplement Cosmos 資料庫 （在本教學課程後面討論） 的有效率的大量匯入工具。</span><span class="sxs-lookup"><span data-stu-id="5eb53-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="5eb53-161">所述的 hello 範例示範如何 toouse 預存程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="5eb53-162">我們將稍後在 hello 教學課程涵蓋觸發程序和使用者定義函數 (Udf)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="5eb53-163">資料庫程式交易</span><span class="sxs-lookup"><span data-stu-id="5eb53-163">Database program transactions</span></span>
<span data-ttu-id="5eb53-164">一般資料庫中的交易可以定義為以單一工作邏輯單位執行的一連串作業。</span><span class="sxs-lookup"><span data-stu-id="5eb53-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="5eb53-165">每個交易都提供「ACID 保證」 。</span><span class="sxs-lookup"><span data-stu-id="5eb53-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="5eb53-166">ACID 是著名的縮寫，代表四個屬性：不可部分完成性 (Atomicity)、一致性 (Consistency)、隔離性 (Isolation) 及耐用性 (Durability)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="5eb53-167">簡言之，不可部分完成性保證完成交易內的所有 hello 工作會被都視為單一單位其中任一個全部都是認可或 none。</span><span class="sxs-lookup"><span data-stu-id="5eb53-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="5eb53-168">一致性可確保 hello 資料處於一律良好的內部狀態之間的交易。</span><span class="sxs-lookup"><span data-stu-id="5eb53-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="5eb53-169">隔離保證，任何兩個交易互相干擾 – 通常，大多數的商業系統提供多個可用的隔離層級根據 hello 應用程式需求。</span><span class="sxs-lookup"><span data-stu-id="5eb53-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="5eb53-170">持久性可確保一定會出現任何 hello 資料庫中認可的變更。</span><span class="sxs-lookup"><span data-stu-id="5eb53-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="5eb53-171">在 Cosmos DB 中，JavaScript 會裝載在 hello 與 hello 資料庫相同的記憶體空間。</span><span class="sxs-lookup"><span data-stu-id="5eb53-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="5eb53-172">因此，在預存程序和觸發程序所做的要求執行 hello 中相同的資料庫工作階段的範圍。</span><span class="sxs-lookup"><span data-stu-id="5eb53-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="5eb53-173">這可讓屬於單一預存程序/觸發程序的所有作業的 Cosmos DB tooguarantee ACID。</span><span class="sxs-lookup"><span data-stu-id="5eb53-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="5eb53-174">請考慮 hello 下列預存程序定義：</span><span class="sxs-lookup"><span data-stu-id="5eb53-174">Consider hello following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="5eb53-175">這個預存程序會使用兩個播放程式在單一作業中之間 tootrade 遊戲應用程式項目內的交易。</span><span class="sxs-lookup"><span data-stu-id="5eb53-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="5eb53-176">hello 預存程序嘗試 tooread 兩份文件中傳遞做為引數的每個對應的 toohello 播放程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="5eb53-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="5eb53-177">如果找不到這兩個播放程式文件，hello 預存程序會更新 hello 文件交換及其項目。</span><span class="sxs-lookup"><span data-stu-id="5eb53-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="5eb53-178">如果發生任何錯誤 hello 方式，就會擲回隱含中止 hello 交易的 JavaScript 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5eb53-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="5eb53-179">如果 hello 集合 hello 預存程序註冊針對單一資料分割集合，則 hello 交易是已設定領域的 tooall hello 集合中的 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="5eb53-180">如果已分割 hello 集合，預存程序會執行 hello 交易範圍中的單一資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5eb53-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="5eb53-181">每個預存程序執行必須再包含必須在對應的 toohello 範圍 hello 交易下執行的資料分割索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="5eb53-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="5eb53-182">如需詳細資訊，請參閱 [Azure Cosmos DB 資料分割](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="5eb53-183">認可和回復</span><span class="sxs-lookup"><span data-stu-id="5eb53-183">Commit and rollback</span></span>
<span data-ttu-id="5eb53-184">交易原本就深入整合至 Cosmos DB 的 JavaScript 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="5eb53-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="5eb53-185">在 JavaScript 函數內，會將所有作業自動包裝在單一交易內。</span><span class="sxs-lookup"><span data-stu-id="5eb53-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="5eb53-186">如果 hello JavaScript 完成而沒有任何例外狀況，就無法認可 hello operations toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5eb53-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="5eb53-187">作用中，關聯式資料庫中的 hello"BEGIN TRANSACTION"和"COMMIT TRANSACTION"陳述式是 Cosmos DB 中隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="5eb53-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="5eb53-188">如果沒有從 hello 指令碼會傳播任何例外狀況，Cosmos DB JavaScript 執行階段將會回復儲存 hello 整個交易。</span><span class="sxs-lookup"><span data-stu-id="5eb53-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="5eb53-189">如稍早所示 hello 範例中，擲回例外狀況是有效等同 tooa Cosmos DB 中的 「 復原交易 」。</span><span class="sxs-lookup"><span data-stu-id="5eb53-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="5eb53-190">資料一致性</span><span class="sxs-lookup"><span data-stu-id="5eb53-190">Data consistency</span></span>
<span data-ttu-id="5eb53-191">一律 hello Azure Cosmos DB 容器 hello 主要複本上執行預存程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="5eb53-192">這確保從預存程序讀取的資料有強式一致性。</span><span class="sxs-lookup"><span data-stu-id="5eb53-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="5eb53-193">使用使用者定義函數的查詢可以執行在 hello 主要或任何次要複本，但我們確定 toomeet hello 要求一致性層級選擇 hello 適當複本。</span><span class="sxs-lookup"><span data-stu-id="5eb53-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="5eb53-194">界限執行</span><span class="sxs-lookup"><span data-stu-id="5eb53-194">Bounded execution</span></span>
<span data-ttu-id="5eb53-195">所有 Cosmos DB 作業必須在指定的 hello 伺服器內都完成要求逾時持續期間。</span><span class="sxs-lookup"><span data-stu-id="5eb53-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="5eb53-196">這個條件約束也適用於 tooJavaScript 函式 （預存程序、 觸發程序和使用者定義函數）。</span><span class="sxs-lookup"><span data-stu-id="5eb53-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="5eb53-197">如果作業未完成的時間限制，hello 會復原交易。</span><span class="sxs-lookup"><span data-stu-id="5eb53-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="5eb53-198">JavaScript 函式必須在 hello 時間限制內完成，或實作基礎的接續模型 toobatch/繼續執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="5eb53-199">在訂單 toosimplify 開發中的預存程序和觸發程序 toohandle 時間限制，hello 集合物件 （適用於建立、 讀取、 取代型和刪除的文件和附件） 底下的所有函式會傳回布林值，表示是否，將會完成作業。</span><span class="sxs-lookup"><span data-stu-id="5eb53-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="5eb53-200">如果此值為 false，就表示 hello 時間限制是關於 tooexpire，和該 hello 程序必須結語執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="5eb53-201">作業排入佇列的先前 toohello 第一項不被接受的存放區作業一定 toocomplete 如果 hello 預存程序完成的時間，不佇列任何要求。</span><span class="sxs-lookup"><span data-stu-id="5eb53-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="5eb53-202">JavaScript 函數能使用的資源也受到限制。</span><span class="sxs-lookup"><span data-stu-id="5eb53-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="5eb53-203">Cosmos 資料庫會保留每個集合的資料庫帳戶的佈建的 hello 大小為基礎的輸送量。</span><span class="sxs-lookup"><span data-stu-id="5eb53-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="5eb53-204">輸送量是以 CPU、記憶體和 IO 使用量的標準單位 (稱為要求單位或 RU) 來表示。</span><span class="sxs-lookup"><span data-stu-id="5eb53-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="5eb53-205">JavaScript 函式可能可能佔用大量的俄文短的時間內，並可能會收到速率限制會在達到 hello 集合的限制時。</span><span class="sxs-lookup"><span data-stu-id="5eb53-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="5eb53-206">資源密集的預存程序可能也會隔離的 tooensure 可用性的基本資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="5eb53-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="5eb53-207">範例：將大量資料匯入資料庫程式</span><span class="sxs-lookup"><span data-stu-id="5eb53-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="5eb53-208">以下是集合中會寫入文件 toobulk 匯入的預存程序的範例。</span><span class="sxs-lookup"><span data-stu-id="5eb53-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="5eb53-209">注意如何 hello 儲存程序控制代碼繫結的執行方式是檢查 hello 布林值會傳回值 createDocument，以及使用然後 hello 的整個批次插入的 hello 預存程序 tootrack 並繼續進行的每個引動過程中的文件計數。</span><span class="sxs-lookup"><span data-stu-id="5eb53-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="5eb53-210"><a id="trigger"></a> 資料庫觸發程序</span><span class="sxs-lookup"><span data-stu-id="5eb53-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="5eb53-211">資料庫預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="5eb53-211">Database pre-triggers</span></span>
<span data-ttu-id="5eb53-212">Cosmos DB 提供作業在文件上執行或觸發的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="5eb53-213">比方說，您可以指定前的觸發程序，當您建立文件-這個前置觸發程序會在執行之前建立 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="5eb53-214">hello 以下是如何前置觸發程序可以是使用的 toovalidate hello 屬性所建立的文件的範例：</span><span class="sxs-lookup"><span data-stu-id="5eb53-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="5eb53-215">和 hello 對應 hello 觸發程序的 Node.js 註冊用戶端程式碼：</span><span class="sxs-lookup"><span data-stu-id="5eb53-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="5eb53-216">預先觸發程序不能有任何輸入參數。</span><span class="sxs-lookup"><span data-stu-id="5eb53-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="5eb53-217">hello 要求物件可以是使用的 toomanipulate hello 要求訊息與 hello 作業相關聯。</span><span class="sxs-lookup"><span data-stu-id="5eb53-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="5eb53-218">在這裡，hello 建立的文件，以執行 hello 前置觸發程序和 hello 要求訊息內文包含 hello 文件 toobe 以 JSON 格式來建立。</span><span class="sxs-lookup"><span data-stu-id="5eb53-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="5eb53-219">當觸發程序所註冊時，使用者可以指定執行時的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="5eb53-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="5eb53-220">這個觸發程序被建立 TriggerOperation.Create，這表示不允許下列 hello。</span><span class="sxs-lookup"><span data-stu-id="5eb53-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="5eb53-221">資料庫後續觸發程序</span><span class="sxs-lookup"><span data-stu-id="5eb53-221">Database post-triggers</span></span>
<span data-ttu-id="5eb53-222">後續觸發程序與預先觸發程序類以，都與文件上的作業相關聯，且未採用任何輸入參數。</span><span class="sxs-lookup"><span data-stu-id="5eb53-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="5eb53-223">您會看到執行**之後**hello 作業已完成，並具有存取 toohello 回應訊息傳送 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5eb53-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="5eb53-224">hello 下列範例會顯示作用中的後置觸發程序：</span><span class="sxs-lookup"><span data-stu-id="5eb53-224">hello following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="5eb53-225">hello 下列範例所示，您可以註冊 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="5eb53-226">這個觸發程序查詢 hello 中繼資料文件，並更新 hello 新建立的文件的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5eb53-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="5eb53-227">一件事，是很重要 toonote hello**異動**Cosmos DB 中的觸發程序執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="5eb53-228">這個後置觸發程序執行的 hello hello 建立 hello 原始文件相同的交易。</span><span class="sxs-lookup"><span data-stu-id="5eb53-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="5eb53-229">因此，我們會發生例外狀況擲回從 hello 後置觸發程序 （例如如果我們無法 tooupdate hello 中繼資料文件） 時，如果 hello 整筆交易將會失敗，而且會回復。</span><span class="sxs-lookup"><span data-stu-id="5eb53-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="5eb53-230">此時不會建立任何文件，並且會傳回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5eb53-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="5eb53-231"><a id="udf"></a>使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="5eb53-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="5eb53-232">使用者定義函數 (Udf) 包含使用的 tooextend hello DocumentDB API SQL 查詢語言文法，及實作自訂商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="5eb53-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="5eb53-233">UDF 只能從內部查詢進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="5eb53-233">They can only be called from inside queries.</span></span> <span data-ttu-id="5eb53-234">他們沒有存取 toohello 內容物件，而且為了 toobe 做為計算僅限 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="5eb53-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="5eb53-235">因此，Udf 可以 hello Cosmos DB 服務之次要複本上執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="5eb53-236">hello 下列範例會建立根據速率的各種收入方括號，UDF toocalculate 所得稅，然後使用它內查詢 toofind 支付 $ 20,000 名以上稅金中的所有人。</span><span class="sxs-lookup"><span data-stu-id="5eb53-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="5eb53-237">hello UDF 後續用於查詢在下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5eb53-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="5eb53-238">JavaScript Language Integrated Query API</span><span class="sxs-lookup"><span data-stu-id="5eb53-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="5eb53-239">除了使用 DocumentDB 的 SQL 文法 tooissuing 查詢，hello 伺服器端 SDK 可讓您使用 fluent 應用程式開發的 JavaScript 介面，而不知道任何 SQL tooperform 最佳化查詢。</span><span class="sxs-lookup"><span data-stu-id="5eb53-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="5eb53-240">hello JavaScript 查詢 API 可讓您 tooprogrammatically 建置查詢將述詞函式傳遞至可鏈結函式呼叫，與語法熟悉 tooECMAScript5 陣列內建像 lodash 受歡迎的 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="5eb53-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="5eb53-241">Hello 有效率地使用 Azure Cosmos DB 的索引執行的 JavaScript 執行階段 toobe 由剖析查詢。</span><span class="sxs-lookup"><span data-stu-id="5eb53-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="5eb53-242">`__`（雙底線） 太別名`getContext().getCollection()`。</span><span class="sxs-lookup"><span data-stu-id="5eb53-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="5eb53-243">換句話說，您可以使用`__`或`getContext().getCollection()`tooaccess hello JavaScript 查詢 API。</span><span class="sxs-lookup"><span data-stu-id="5eb53-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="5eb53-244">支援的函式包括︰</span><span class="sxs-lookup"><span data-stu-id="5eb53-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="5eb53-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-246">啟動鏈結的呼叫，必須以 value() 終止。</span><span class="sxs-lookup"><span data-stu-id="5eb53-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5eb53-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-248">篩選使用述詞的函式會傳回成 hello 結果集的順序 toofilter 輸入/輸出輸入文件中的 true/false 輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="5eb53-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="5eb53-249">這種行為與類似 tooa SQL 中的 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="5eb53-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5eb53-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-251">適用於投影，指定對應的每個輸入項目 tooa JavaScript 物件或值的轉換函式。</span><span class="sxs-lookup"><span data-stu-id="5eb53-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="5eb53-252">這種行為與類似的 tooa SELECT 子句中 SQL。</span><span class="sxs-lookup"><span data-stu-id="5eb53-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5eb53-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-254">這是從每個輸入項目擷取單一屬性的 hello 值對應的捷徑。</span><span class="sxs-lookup"><span data-stu-id="5eb53-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5eb53-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-256">結合，並將陣列 tooa 單一陣列中每個輸入項目。</span><span class="sxs-lookup"><span data-stu-id="5eb53-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="5eb53-257">這種行為與類似 tooSelectMany LINQ 中。</span><span class="sxs-lookup"><span data-stu-id="5eb53-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5eb53-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-259">透過排序 hello 文件，以遞增順序，使用指定的述詞的 hello hello 輸入文件資料流中會產生一組新的文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="5eb53-260">這種行為與類似 tooa ORDER BY 子句在 SQL 中。</span><span class="sxs-lookup"><span data-stu-id="5eb53-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5eb53-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="5eb53-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5eb53-262">透過排序 hello 文件，以遞減順序，使用指定的述詞的 hello hello 輸入文件資料流中會產生一組新的文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="5eb53-263">這種行為與 SQL 類似 tooa x DESC ORDER BY 子句。</span><span class="sxs-lookup"><span data-stu-id="5eb53-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="5eb53-264">包含述詞和 （或） 選取器函式內，hello 下列 JavaScript 建構自動最佳化的 toorun 直接在取得 Azure Cosmos DB 索引：</span><span class="sxs-lookup"><span data-stu-id="5eb53-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5eb53-265">簡單運算子：= + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="5eb53-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="5eb53-266">常值，包括 hello 物件常值: {}</span><span class="sxs-lookup"><span data-stu-id="5eb53-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="5eb53-267">var、return</span><span class="sxs-lookup"><span data-stu-id="5eb53-267">var, return</span></span>

<span data-ttu-id="5eb53-268">下列 JavaScript 建構的 hello 不會針對 Azure Cosmos DB 索引取得最佳化：</span><span class="sxs-lookup"><span data-stu-id="5eb53-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5eb53-269">控制流程 (例如 if、for、while)</span><span class="sxs-lookup"><span data-stu-id="5eb53-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="5eb53-270">函式呼叫</span><span class="sxs-lookup"><span data-stu-id="5eb53-270">Function calls</span></span>

<span data-ttu-id="5eb53-271">如需詳細資訊，請參閱我們的 [伺服器端 JSDocs](http://azure.github.io/azure-documentdb-js-server/)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="5eb53-272">範例： 撰寫預存程序使用 hello JavaScript 查詢 API</span><span class="sxs-lookup"><span data-stu-id="5eb53-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="5eb53-273">下列程式碼範例的 hello 是如何使用 hello JavaScript 查詢 API，hello 預存程序內容中的範例。</span><span class="sxs-lookup"><span data-stu-id="5eb53-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="5eb53-274">hello 預存程序插入文件中，所輸入的參數，指定並更新中繼資料文件中，使用 hello`__.filter()`方法，並有 minSize、 maxSize 和 totalSize 依據 hello 輸入文件的大小屬性。</span><span class="sxs-lookup"><span data-stu-id="5eb53-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="5eb53-275">SQL tooJavascript 祕技</span><span class="sxs-lookup"><span data-stu-id="5eb53-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="5eb53-276">hello 下表顯示各種 SQL 查詢和 hello 對應 JavaScript 的查詢。</span><span class="sxs-lookup"><span data-stu-id="5eb53-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="5eb53-277">使用 SQL 查詢時，文件屬性索引鍵 (例如 `doc.id`) 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5eb53-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="5eb53-278">SQL</span><span class="sxs-lookup"><span data-stu-id="5eb53-278">SQL</span></span>| <span data-ttu-id="5eb53-279">JavaScript 查詢 API</span><span class="sxs-lookup"><span data-stu-id="5eb53-279">JavaScript Query API</span></span>|<span data-ttu-id="5eb53-280">下列說明</span><span class="sxs-lookup"><span data-stu-id="5eb53-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="5eb53-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="5eb53-281">SELECT *</span></span><br><span data-ttu-id="5eb53-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5eb53-282">FROM docs</span></span>| <span data-ttu-id="5eb53-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="5eb53-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="5eb53-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="5eb53-285">});</span><span class="sxs-lookup"><span data-stu-id="5eb53-285">});</span></span>|<span data-ttu-id="5eb53-286">1</span><span class="sxs-lookup"><span data-stu-id="5eb53-286">1</span></span>|
|<span data-ttu-id="5eb53-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="5eb53-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="5eb53-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5eb53-288">FROM docs</span></span>|<span data-ttu-id="5eb53-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-289">__.map(function(doc) {</span></span><br><span data-ttu-id="5eb53-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="5eb53-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5eb53-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5eb53-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5eb53-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="5eb53-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="5eb53-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="5eb53-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="5eb53-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5eb53-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5eb53-295">});</span><span class="sxs-lookup"><span data-stu-id="5eb53-295">});</span></span>|<span data-ttu-id="5eb53-296">2</span><span class="sxs-lookup"><span data-stu-id="5eb53-296">2</span></span>|
|<span data-ttu-id="5eb53-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="5eb53-297">SELECT *</span></span><br><span data-ttu-id="5eb53-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5eb53-298">FROM docs</span></span><br><span data-ttu-id="5eb53-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="5eb53-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5eb53-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="5eb53-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="5eb53-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5eb53-302">});</span><span class="sxs-lookup"><span data-stu-id="5eb53-302">});</span></span>|<span data-ttu-id="5eb53-303">3</span><span class="sxs-lookup"><span data-stu-id="5eb53-303">3</span></span>|
|<span data-ttu-id="5eb53-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="5eb53-304">SELECT *</span></span><br><span data-ttu-id="5eb53-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5eb53-305">FROM docs</span></span><br><span data-ttu-id="5eb53-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="5eb53-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="5eb53-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-307">__.filter(function(x) {</span></span><br><span data-ttu-id="5eb53-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="5eb53-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="5eb53-309">});</span><span class="sxs-lookup"><span data-stu-id="5eb53-309">});</span></span>|<span data-ttu-id="5eb53-310">4</span><span class="sxs-lookup"><span data-stu-id="5eb53-310">4</span></span>|
|<span data-ttu-id="5eb53-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="5eb53-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="5eb53-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5eb53-312">FROM docs</span></span><br><span data-ttu-id="5eb53-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="5eb53-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5eb53-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5eb53-314">__.chain()</span></span><br><span data-ttu-id="5eb53-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5eb53-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="5eb53-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5eb53-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5eb53-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5eb53-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="5eb53-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="5eb53-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5eb53-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5eb53-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5eb53-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="5eb53-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="5eb53-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5eb53-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5eb53-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5eb53-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5eb53-324">.value();</span><span class="sxs-lookup"><span data-stu-id="5eb53-324">.value();</span></span>|<span data-ttu-id="5eb53-325">5</span><span class="sxs-lookup"><span data-stu-id="5eb53-325">5</span></span>|
|<span data-ttu-id="5eb53-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="5eb53-326">SELECT VALUE tag</span></span><br><span data-ttu-id="5eb53-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="5eb53-327">FROM docs</span></span><br><span data-ttu-id="5eb53-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="5eb53-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="5eb53-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="5eb53-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="5eb53-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5eb53-330">__.chain()</span></span><br><span data-ttu-id="5eb53-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5eb53-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="5eb53-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="5eb53-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5eb53-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5eb53-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5eb53-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="5eb53-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="5eb53-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="5eb53-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5eb53-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5eb53-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="5eb53-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="5eb53-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="5eb53-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="5eb53-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="5eb53-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="5eb53-340">6</span><span class="sxs-lookup"><span data-stu-id="5eb53-340">6</span></span>|

<span data-ttu-id="5eb53-341">hello 下列說明解釋 hello 上表中的每個查詢。</span><span class="sxs-lookup"><span data-stu-id="5eb53-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="5eb53-342">所有文件中的結果 (使用連續權杖分頁)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="5eb53-343">專案 hello 識別碼、 訊息 (別名 toomsg) 和所有文件中的動作。</span><span class="sxs-lookup"><span data-stu-id="5eb53-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="5eb53-344">文件以 hello 述詞的查詢： 識別碼 ="X998_Y998"。</span><span class="sxs-lookup"><span data-stu-id="5eb53-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="5eb53-345">查詢具有標記屬性和標記的文件是包含 hello 值 123 的陣列。</span><span class="sxs-lookup"><span data-stu-id="5eb53-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="5eb53-346">查詢述詞的文件識別碼 ="X998_Y998 」，而且然後專案 hello 識別碼和訊息 (別名 toomsg)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="5eb53-347">有一個陣列的屬性標記的文件會篩選和 hello _ts 時間戳記系統屬性，依排序 hello 產生文件，然後專案 + 簡維 hello 標記的陣列。</span><span class="sxs-lookup"><span data-stu-id="5eb53-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="5eb53-348">執行階段支援</span><span class="sxs-lookup"><span data-stu-id="5eb53-348">Runtime support</span></span>
<span data-ttu-id="5eb53-349">[DocumentDB JavaScript 伺服器端應用程式開發介面](http://azure.github.io/azure-documentdb-js-server/)hello 提供支援大部分的 hello 主流 JavaScript 語言功能，以標準化的[ecma-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="5eb53-350">安全性</span><span class="sxs-lookup"><span data-stu-id="5eb53-350">Security</span></span>
<span data-ttu-id="5eb53-351">JavaScript 預存程序和觸發程序是沙箱化，讓一個指令碼的 hello 效果不會流失 toohello 其他沒有經過 hello 資料庫層級的 hello 快照集交易隔離。</span><span class="sxs-lookup"><span data-stu-id="5eb53-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="5eb53-352">hello 執行階段環境管理的集區，但之後每次執行清除的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="5eb53-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="5eb53-353">因此，它們會保證 toobe 彼此安全的任何非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="5eb53-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="5eb53-354">預先編譯</span><span class="sxs-lookup"><span data-stu-id="5eb53-354">Pre-compilation</span></span>
<span data-ttu-id="5eb53-355">預存程序、 觸發程序和 Udf 於 hello 時間的每個指令碼引動過程順序 tooavoid 編譯成本隱含先行編譯的 toohello 位元組程式碼的格式。</span><span class="sxs-lookup"><span data-stu-id="5eb53-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="5eb53-356">這種作法可確保能夠快速叫用預存程序，且只需耗費少量資源。</span><span class="sxs-lookup"><span data-stu-id="5eb53-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="5eb53-357">用戶端 SDK 支援</span><span class="sxs-lookup"><span data-stu-id="5eb53-357">Client SDK support</span></span>
<span data-ttu-id="5eb53-358">中的加法 toohello DocumentDB API [Node.js](documentdb-sdk-node.md)用戶端，Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md)， [.NET Core](documentdb-sdk-dotnet-core.md)， [Java](documentdb-sdk-java.md)， [JavaScript](http://azure.github.io/azure-documentdb-js/)，和[Python Sdk](documentdb-sdk-python.md) hello DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="5eb53-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="5eb53-359">使用上述任何 SDK，也可以建立和執行預存程序、觸發程序和 UDF。</span><span class="sxs-lookup"><span data-stu-id="5eb53-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="5eb53-360">下列範例會示範如何 hello toocreate 和執行預存程序使用 hello.NET 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5eb53-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="5eb53-361">請注意 hello.NET 型別如何傳入 hello 預存程序，為 JSON，並讀回。</span><span class="sxs-lookup"><span data-stu-id="5eb53-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="5eb53-362">這個範例示範如何 toouse hello [DocumentDB.NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate 前置觸發程序和建立文件以 hello 觸發程序啟用。</span><span class="sxs-lookup"><span data-stu-id="5eb53-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="5eb53-363">和 hello 下列範例顯示如何 toocreate 使用者定義函數 (UDF)，並使用它在[DocumentDB API SQL 查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="5eb53-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="5eb53-364">REST API</span><span class="sxs-lookup"><span data-stu-id="5eb53-364">REST API</span></span>
<span data-ttu-id="5eb53-365">所有 Azure Cosmos DB 作業都可以用 RESTful 方式來執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="5eb53-366">使用 HTTP POST，就可以將預存程序、觸發程序和使用者定義函數註冊至某個集合下。</span><span class="sxs-lookup"><span data-stu-id="5eb53-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="5eb53-367">hello 以下是如何的範例 tooregister 預存程序：</span><span class="sxs-lookup"><span data-stu-id="5eb53-367">hello following is an example of how tooregister a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="5eb53-368">hello 預存程序註冊執行 POST 要求，針對 hello URI dbs/testdb/colls/testColl/sprocs hello 主體包含有 hello toocreate 預存程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="5eb53-369">觸發程序和 UDF可以透過分別發出 /triggers 和 /udfs 的 POST 要求，以類似方式進行註冊。</span><span class="sxs-lookup"><span data-stu-id="5eb53-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="5eb53-370">您可以接著對其資源連結發出 POST 要求來執行這個預存程序：</span><span class="sxs-lookup"><span data-stu-id="5eb53-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="5eb53-371">在這裡，hello 輸入的 toohello 預存程序會傳遞 hello 要求主體中。</span><span class="sxs-lookup"><span data-stu-id="5eb53-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="5eb53-372">請注意，hello 輸入被當做輸入參數的 JSON 陣列。</span><span class="sxs-lookup"><span data-stu-id="5eb53-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="5eb53-373">hello 預存程序會採用 hello 第一個輸入，是回應主體的文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="5eb53-374">我們收到 hello 回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="5eb53-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="5eb53-375">觸發程序與預存程序不同，無法直接執行，</span><span class="sxs-lookup"><span data-stu-id="5eb53-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="5eb53-376">而是在對文件執行作業時執行。</span><span class="sxs-lookup"><span data-stu-id="5eb53-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="5eb53-377">我們可以使用 HTTP 標頭，透過要求指定 hello 觸發程序 toorun。</span><span class="sxs-lookup"><span data-stu-id="5eb53-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="5eb53-378">hello 以下是要求 toocreate 文件。</span><span class="sxs-lookup"><span data-stu-id="5eb53-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="5eb53-379">這裡 hello 前置觸發程序 toobe 與 hello 要求執行 hello x-ms-documentdb-pre-trigger-include 標頭中指定。</span><span class="sxs-lookup"><span data-stu-id="5eb53-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="5eb53-380">相對的任何後續觸發程序可以在 hello x-ms-documentdb-post-trigger-include 標頭中。</span><span class="sxs-lookup"><span data-stu-id="5eb53-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="5eb53-381">請注意，您可以指定給定要求的預先和後續觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5eb53-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="5eb53-382">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="5eb53-382">Sample code</span></span>
<span data-ttu-id="5eb53-383">您可以在我們的 [GitHub 存放庫](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples)上找到更多的伺服器端程式碼範例 (包括 [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) 和 [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js))。</span><span class="sxs-lookup"><span data-stu-id="5eb53-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="5eb53-384">想 tooshare 實用的預存程序？</span><span class="sxs-lookup"><span data-stu-id="5eb53-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="5eb53-385">請傳送提取要求給我們！</span><span class="sxs-lookup"><span data-stu-id="5eb53-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5eb53-386">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5eb53-386">Next steps</span></span>
<span data-ttu-id="5eb53-387">一旦您擁有一個或多個預存程序、 觸發程序和使用者定義函式建立，您可以將它們載入並 hello Azure 入口網站使用的資料檔案總管中檢視這些檔案。</span><span class="sxs-lookup"><span data-stu-id="5eb53-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="5eb53-388">您也可能會發現 hello 下列參考與資源有助於您深入了解 Azure Cosmos dB 伺服器端程式設計的路徑 toolearn:</span><span class="sxs-lookup"><span data-stu-id="5eb53-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="5eb53-389">Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="5eb53-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="5eb53-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="5eb53-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="5eb53-391">JSON</span><span class="sxs-lookup"><span data-stu-id="5eb53-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="5eb53-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="5eb53-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="5eb53-393">安全和可攜式資料庫擴充性</span><span class="sxs-lookup"><span data-stu-id="5eb53-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="5eb53-394">服務導向資料庫架構</span><span class="sxs-lookup"><span data-stu-id="5eb53-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="5eb53-395">裝載 Microsoft SQL server 中的 hello.NET 執行階段</span><span class="sxs-lookup"><span data-stu-id="5eb53-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

