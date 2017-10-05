---
title: "Azure Cosmos DB 的伺服器端 JavaScript 程式設計 | Microsoft Docs"
description: "了解如何使用 Azure Cosmos DB 來撰寫 JavaScript 預存程序、資料庫觸發程序和使用者定義函數 (UDF)。 取得資料庫程式設計秘訣等等。"
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
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="c8388-105">Azure Cosmos DB 伺服器端程式設計：預存程序、資料庫觸發程序和 UDF</span><span class="sxs-lookup"><span data-stu-id="c8388-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="c8388-106">了解 Azure Cosmos DB 的語言整合式、交易式 JavaScript 執行如何讓開發人員使用 [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript 以原生方式撰寫**預存程序**、**觸發程序**及**使用者定義函數 (UDF)**。</span><span class="sxs-lookup"><span data-stu-id="c8388-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="c8388-107">這一特點可讓您得以撰寫能直接在資料庫儲存體資料分割上傳送和執行的資料庫程式應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="c8388-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="c8388-108">我們建議使用者從觀看下列影片開始入門，Andrew Liu 在其中提供了 Cosmos DB 的伺服器端資料庫程式設計模型的簡介。</span><span class="sxs-lookup"><span data-stu-id="c8388-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="c8388-109">然後，回到這篇文章，您可在此找到下列問題的答案：</span><span class="sxs-lookup"><span data-stu-id="c8388-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="c8388-110">如何使用 JavaScript 撰寫預存程序、觸發程序或 UDF？</span><span class="sxs-lookup"><span data-stu-id="c8388-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="c8388-111">Cosmos DB 如何提供 ACID 保證？</span><span class="sxs-lookup"><span data-stu-id="c8388-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="c8388-112">如何在 Cosmos DB 中執行交易工作？</span><span class="sxs-lookup"><span data-stu-id="c8388-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="c8388-113">什麼是預先觸發程序和後續觸發程序？其撰寫方法為何？</span><span class="sxs-lookup"><span data-stu-id="c8388-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="c8388-114">如何註冊及使用 HTTP 以 RESTful 方式執行預存程序、觸發程序或 UDF？</span><span class="sxs-lookup"><span data-stu-id="c8388-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="c8388-115">哪些 Cosmos DB SDK 可用來建立及執行預存程序、觸發程序和 UDF？</span><span class="sxs-lookup"><span data-stu-id="c8388-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="c8388-116">預存程序和 UDF 程式設計簡介</span><span class="sxs-lookup"><span data-stu-id="c8388-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="c8388-117">這種「 *以 JavaScript 做為新式 T-SQL* 」的方式，可讓應用程式開發人員不必傷腦筋處理複雜的類型系統不符問題和物件關聯式對應技術。</span><span class="sxs-lookup"><span data-stu-id="c8388-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="c8388-118">此外，它本身還有一些可加以利用以便建置豐富應用程式的優勢：</span><span class="sxs-lookup"><span data-stu-id="c8388-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="c8388-119">**程序邏輯** ：以 JavaScript 做為高階程式設計語言，可提供豐富且常見的介面來表示商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="c8388-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="c8388-120">您可以用更接近資料的方式執行一連串的複雜作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="c8388-121">**不可部分完成的交易**：Cosmos DB 可確保在單一預存程序或觸發程序內執行的資料庫作業成為不可部分完成的作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="c8388-122">這可讓應用程式合併單一批次中的相關作業，讓所有作業不是一起成功就是一起失敗。</span><span class="sxs-lookup"><span data-stu-id="c8388-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="c8388-123">**效能**：由於 JSON 本身就對應至 Javascript 語言類型系統並同時是 Cosmos DB 中儲存體基本單位，因此可提供許多最佳化功能，例如在緩衝集區中對 JSON 文件執行滯後具體化，並讓執行中程式碼可以依需求使用這些文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="c8388-124">除此之外，還有其它與傳送商務邏輯至資料庫相關聯的效能優點：</span><span class="sxs-lookup"><span data-stu-id="c8388-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="c8388-125">批次處理 - 開發人員可以群組多個作業 (例如插入)，大量進行提交。</span><span class="sxs-lookup"><span data-stu-id="c8388-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="c8388-126">因此，網路流量延遲成本以及建立個別交易的額外儲存負荷得以大幅降低。</span><span class="sxs-lookup"><span data-stu-id="c8388-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="c8388-127">預先編譯 - Cosmos DB 會預先編譯預存程序、觸發程序和使用者定義函數 (UDF)，以避免每次叫用的 JavaScript 編譯成本。</span><span class="sxs-lookup"><span data-stu-id="c8388-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="c8388-128">因此，建置程序邏輯位元組程式碼的額外負荷已降到最低。</span><span class="sxs-lookup"><span data-stu-id="c8388-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="c8388-129">排序 - 許多作業都需要副作用 (「觸發程序」)，其可能涉及執行一項或多項次要儲存作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="c8388-130">除了不可部分完成的作業之外，這在移至伺服器時會有更好的效能。</span><span class="sxs-lookup"><span data-stu-id="c8388-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="c8388-131">**封裝** ：預存程序可以用來將商務邏輯群組在一個位置。</span><span class="sxs-lookup"><span data-stu-id="c8388-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="c8388-132">這有兩個優點：</span><span class="sxs-lookup"><span data-stu-id="c8388-132">This has two advantages:</span></span>
  * <span data-ttu-id="c8388-133">它會在未經處理的資料上方新增抽象層，讓資料架構設計人員發展其應用程式，而不會動到資料。</span><span class="sxs-lookup"><span data-stu-id="c8388-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="c8388-134">這在資料無結構描述時特別有用，因為暫時的假設是，如果它們需要直接處理資料，則可能需要編譯成應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8388-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="c8388-135">這個抽象層讓企業得以透過指令碼簡化存取來確保資料安全。</span><span class="sxs-lookup"><span data-stu-id="c8388-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="c8388-136">許多平台 (包括 .NET、Node.js 和 JavaScript) 都透過 [REST API](/rest/api/documentdb/)、[Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) 和 [用戶端 SDK](documentdb-sdk-dotnet.md) 來支援建立和執行資料庫觸發程序、預存程序及自訂查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="c8388-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="c8388-137">本教學課程使用 [Node.js SDK 搭配 Q Promises](http://azure.github.io/azure-documentdb-node-q/) 來說明預存程序、觸發程序及 UDF 的語法和用法。</span><span class="sxs-lookup"><span data-stu-id="c8388-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="c8388-138">預存程序</span><span class="sxs-lookup"><span data-stu-id="c8388-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="c8388-139">範例：撰寫簡易預存程序</span><span class="sxs-lookup"><span data-stu-id="c8388-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="c8388-140">我們先來看看簡單的預存程序，此程序會傳回 "Hello World" 回應。</span><span class="sxs-lookup"><span data-stu-id="c8388-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="c8388-141">預存程序是按照集合來註冊，而且可以作用於該集合中現有的文件和附件。</span><span class="sxs-lookup"><span data-stu-id="c8388-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="c8388-142">下列程式碼片段說明如何向集合註冊 helloWorld 預存程序。</span><span class="sxs-lookup"><span data-stu-id="c8388-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="c8388-143">註冊好預存程序後，即可針對集合執行，並將結果讀取回用戶端。</span><span class="sxs-lookup"><span data-stu-id="c8388-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="c8388-144">內容物件提供可對 Cosmos DB 儲存體執行之所有作業的存取權，以及要求和回應物件的存取權。</span><span class="sxs-lookup"><span data-stu-id="c8388-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="c8388-145">在此例中，我們使用回應物件來設定傳回給用戶端的回應本文。</span><span class="sxs-lookup"><span data-stu-id="c8388-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="c8388-146">如需詳細資料，請參閱 [Azure Cosmos DB JavaScript 伺服器 SDK 文件 (英文)](http://azure.github.io/azure-documentdb-js-server/)。</span><span class="sxs-lookup"><span data-stu-id="c8388-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="c8388-147">讓我們擴大這個範例，並對預存程序新增更多資料庫相關功能。</span><span class="sxs-lookup"><span data-stu-id="c8388-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="c8388-148">預存程序可以建立、更新、讀取、查詢與刪除集合內的文件和附件。</span><span class="sxs-lookup"><span data-stu-id="c8388-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="c8388-149">範例：撰寫建立文件的預存程序</span><span class="sxs-lookup"><span data-stu-id="c8388-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="c8388-150">下一個程式碼片段說明如何使用內容物件來與 Cosmos DB 資源互動。</span><span class="sxs-lookup"><span data-stu-id="c8388-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

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


<span data-ttu-id="c8388-151">此預存程序將 documentToCreate (要在目前集合中建立的文件本文) 做為輸入。</span><span class="sxs-lookup"><span data-stu-id="c8388-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="c8388-152">所有這類作業都是非同步的，而且需仰賴 JavaScript 函數回呼。</span><span class="sxs-lookup"><span data-stu-id="c8388-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="c8388-153">回呼函數有兩個參數，一個用於作業失敗時的錯誤物件，一個用於已建立的物件。</span><span class="sxs-lookup"><span data-stu-id="c8388-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="c8388-154">在回呼內，使用者可以處理例外狀況或擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="c8388-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="c8388-155">如果未提供回呼，而且發生錯誤，則 Azure Cosmos DB 執行階段會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="c8388-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="c8388-156">在上面的範例中，回呼會在作業失敗時擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="c8388-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="c8388-157">否則，會將已建立之文件的 ID 設定為用戶端回應的本文。</span><span class="sxs-lookup"><span data-stu-id="c8388-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="c8388-158">此預存程序與輸入參數搭配執行的方式如下。</span><span class="sxs-lookup"><span data-stu-id="c8388-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
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


<span data-ttu-id="c8388-159">請注意，您可以修改此預存程序，將一批文件本文做為輸入，並將這些本文全都建立在相同的預存程序執行內，而不是用多個網路要求個別建立這些本文。</span><span class="sxs-lookup"><span data-stu-id="c8388-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="c8388-160">您可以用這種方式來實作有效率的 Cosmos DB 大量匯入工具 (本教學課程稍後會有討論)。</span><span class="sxs-lookup"><span data-stu-id="c8388-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="c8388-161">上面描述的範例已示範如何使用預存程序。</span><span class="sxs-lookup"><span data-stu-id="c8388-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="c8388-162">本教學課程稍後會討論觸發程序和使用者定義函數 (UDF)。</span><span class="sxs-lookup"><span data-stu-id="c8388-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="c8388-163">資料庫程式交易</span><span class="sxs-lookup"><span data-stu-id="c8388-163">Database program transactions</span></span>
<span data-ttu-id="c8388-164">一般資料庫中的交易可以定義為以單一工作邏輯單位執行的一連串作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="c8388-165">每個交易都提供「ACID 保證」 。</span><span class="sxs-lookup"><span data-stu-id="c8388-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="c8388-166">ACID 是著名的縮寫，代表四個屬性：不可部分完成性 (Atomicity)、一致性 (Consistency)、隔離性 (Isolation) 及耐用性 (Durability)。</span><span class="sxs-lookup"><span data-stu-id="c8388-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="c8388-167">簡言之，不可部分完成的作業保證會將交易內完成的所有工作視為單一單位，所有工作不是全部認可就是一個都不認可。</span><span class="sxs-lookup"><span data-stu-id="c8388-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="c8388-168">「一致性」確保資料在交易中一律處於良好內部狀態。</span><span class="sxs-lookup"><span data-stu-id="c8388-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="c8388-169">「隔離」保證兩個交易不會彼此干擾；一般而言，大部分的商業系統都會提供多個可以根據應用程式的需要來使用的隔離等級。</span><span class="sxs-lookup"><span data-stu-id="c8388-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="c8388-170">「持久性」確保資料庫中所認可的任何變更一律會存在。</span><span class="sxs-lookup"><span data-stu-id="c8388-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="c8388-171">在 Cosmos DB 中，會在與資料庫相同的記憶體空間中裝載 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="c8388-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="c8388-172">因此，在預存程序和觸發程序內提出的要求會在資料庫工作階段的相同範圍中執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="c8388-173">這讓 Cosmos DB 能夠為屬於單一預存程序/觸發程序的所有作業提供 ACID 保證。</span><span class="sxs-lookup"><span data-stu-id="c8388-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="c8388-174">我們看一下下列預存程序定義：</span><span class="sxs-lookup"><span data-stu-id="c8388-174">Consider the following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="c8388-175">此預存程序使用遊戲應用程式內的交易，透過單一作業讓兩位玩家交易項目。</span><span class="sxs-lookup"><span data-stu-id="c8388-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="c8388-176">預存程序嘗試讀取兩份文件，這兩份文件各自對應到以引數形式傳入的玩家 ID。</span><span class="sxs-lookup"><span data-stu-id="c8388-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="c8388-177">如果有找到這兩份玩家文件，則預存程序會透過交換他們的項目來更新文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="c8388-178">如果過程中發生任何錯誤，則會擲回以隱含方式中止交易的 JavaScript 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c8388-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="c8388-179">如果預存程序註冊的集合是單一分割集合，則交易的範圍為集合中的所有文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="c8388-180">如果集合已分割，則預存程序會在單一分割索引鍵的交易範圍內執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="c8388-181">然後每個預存程序執行必須包含分割索引鍵值，該值對應至必須在其下執行交易的範圍。</span><span class="sxs-lookup"><span data-stu-id="c8388-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="c8388-182">如需詳細資訊，請參閱 [Azure Cosmos DB 資料分割](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="c8388-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="c8388-183">認可和回復</span><span class="sxs-lookup"><span data-stu-id="c8388-183">Commit and rollback</span></span>
<span data-ttu-id="c8388-184">交易原本就深入整合至 Cosmos DB 的 JavaScript 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="c8388-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="c8388-185">在 JavaScript 函數內，會將所有作業自動包裝在單一交易內。</span><span class="sxs-lookup"><span data-stu-id="c8388-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="c8388-186">如果 JavaScript 完成，而且沒有任何例外狀況，就會認可資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="c8388-187">在 Cosmos DB 中，關聯式資料庫中的 "BEGIN TRANSACTION" 和 "COMMIT TRANSACTION" 陳述式實際上是隱含的。</span><span class="sxs-lookup"><span data-stu-id="c8388-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="c8388-188">如果有任何透過指令碼傳播的例外狀況，則 Cosmos DB 的 JavaScript 執行階段將會復原整個交易。</span><span class="sxs-lookup"><span data-stu-id="c8388-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="c8388-189">如稍早的範例所示，擲回例外狀況的作用等同於 Cosmos DB 中的 "ROLLBACK TRANSACTION"。</span><span class="sxs-lookup"><span data-stu-id="c8388-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="c8388-190">資料一致性</span><span class="sxs-lookup"><span data-stu-id="c8388-190">Data consistency</span></span>
<span data-ttu-id="c8388-191">預存程序和觸發程序一律會在 Azure Cosmos DB 容器的主要複本上執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="c8388-192">這確保從預存程序讀取的資料有強式一致性。</span><span class="sxs-lookup"><span data-stu-id="c8388-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="c8388-193">使用「使用者定義函數」的查詢可以在主要或任何次要複本上執行，但是我們透過選擇適當的複本，確保符合所要求的一致性層級。</span><span class="sxs-lookup"><span data-stu-id="c8388-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="c8388-194">界限執行</span><span class="sxs-lookup"><span data-stu-id="c8388-194">Bounded execution</span></span>
<span data-ttu-id="c8388-195">所有 Cosmos DB 作業都必須在伺服器指定的要求逾時期間內完成。</span><span class="sxs-lookup"><span data-stu-id="c8388-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="c8388-196">此條件約束也適用於 JavaScript 函數 (預存程序、觸發程序和使用者定義函數)。</span><span class="sxs-lookup"><span data-stu-id="c8388-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="c8388-197">如果作業未在該時限內完成，則會回復交易。</span><span class="sxs-lookup"><span data-stu-id="c8388-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="c8388-198">JavaScript 函數必須在此時限內完成，或必須實作接續式模型來批次處理/繼續執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="c8388-199">若要簡化預存程序和觸發程序的開發流程以因應此時限，集合物件下的所有函數 (用於建立、讀取、取代與刪除文件和附件) 都會傳回布林值，以指出該作業是否會完成。</span><span class="sxs-lookup"><span data-stu-id="c8388-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="c8388-200">如果此值是 false，則表示即將到達時限，該程序必須包裝執行作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="c8388-201">如果預存程序及時完成，而且佇列中已無其他要求，則在第一個不被接受之儲存作業之前排入佇列的作業保證會完成。</span><span class="sxs-lookup"><span data-stu-id="c8388-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="c8388-202">JavaScript 函數能使用的資源也受到限制。</span><span class="sxs-lookup"><span data-stu-id="c8388-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="c8388-203">Cosmos DB 會根據所佈建的資料庫帳戶大小預留每個集合的輸送量。</span><span class="sxs-lookup"><span data-stu-id="c8388-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="c8388-204">輸送量是以 CPU、記憶體和 IO 使用量的標準單位 (稱為要求單位或 RU) 來表示。</span><span class="sxs-lookup"><span data-stu-id="c8388-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="c8388-205">JavaScript 函數有可能會在短時間內使用大量 RU，如果達到集合限制，速率便會受到限制。</span><span class="sxs-lookup"><span data-stu-id="c8388-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="c8388-206">需要使用大量資源的預存程序也可能會遭到隔離，以確保基本資料庫作業的可用性。</span><span class="sxs-lookup"><span data-stu-id="c8388-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="c8388-207">範例：將大量資料匯入資料庫程式</span><span class="sxs-lookup"><span data-stu-id="c8388-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="c8388-208">以下的預存程序範例，其撰寫目的是要將文件大量匯入集合之中。</span><span class="sxs-lookup"><span data-stu-id="c8388-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="c8388-209">請注意預存程序如何透過檢查 createDocument 所傳回的布林值處理界限執行，然後使用每次叫用預存程序時所插入的文件計數來追蹤和繼續各批次的進度。</span><span class="sxs-lookup"><span data-stu-id="c8388-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="c8388-210"><a id="trigger"></a> 資料庫觸發程序</span><span class="sxs-lookup"><span data-stu-id="c8388-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="c8388-211">資料庫預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="c8388-211">Database pre-triggers</span></span>
<span data-ttu-id="c8388-212">Cosmos DB 提供作業在文件上執行或觸發的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c8388-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="c8388-213">例如，您可以在建立文件時指定預先觸發程序；此預先觸發程序會在建立文件之前執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="c8388-214">下列範例說明如何使用預先觸發程序來驗證所建立文件的屬性：</span><span class="sxs-lookup"><span data-stu-id="c8388-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="c8388-215">以及觸發程序的對應 Node.js 用戶端註冊程式碼：</span><span class="sxs-lookup"><span data-stu-id="c8388-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

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


<span data-ttu-id="c8388-216">預先觸發程序不能有任何輸入參數。</span><span class="sxs-lookup"><span data-stu-id="c8388-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="c8388-217">要求物件可以用來操作與作業相關聯的要求訊息。</span><span class="sxs-lookup"><span data-stu-id="c8388-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="c8388-218">在這裡，預先觸發程序會在建立文件時執行，而且要求訊息本文包含要以 JSON 格式建立的文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="c8388-219">註冊觸發程序時，使用者可以指定與之搭配執行的作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="c8388-220">此觸發程序是使用 TriggerOperation.Create 所建立，這表示不允許下列作業。</span><span class="sxs-lookup"><span data-stu-id="c8388-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="c8388-221">資料庫後續觸發程序</span><span class="sxs-lookup"><span data-stu-id="c8388-221">Database post-triggers</span></span>
<span data-ttu-id="c8388-222">後續觸發程序與預先觸發程序類以，都與文件上的作業相關聯，且未採用任何輸入參數。</span><span class="sxs-lookup"><span data-stu-id="c8388-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="c8388-223">它們是在作業完成「之後」  執行，而且可以存取傳送給用戶端的回應訊息。</span><span class="sxs-lookup"><span data-stu-id="c8388-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="c8388-224">下列範例說明起作用的後續觸發程序：</span><span class="sxs-lookup"><span data-stu-id="c8388-224">The following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="c8388-225">觸發程序可以如下列範例所示進行註冊。</span><span class="sxs-lookup"><span data-stu-id="c8388-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
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


<span data-ttu-id="c8388-226">此觸發程序會查詢中繼資料文件，並使用新建立之文件的詳細資料加以更新。</span><span class="sxs-lookup"><span data-stu-id="c8388-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="c8388-227">有一點務必要注意，那就是在 Cosmos DB 中觸發程序的「交易式」執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="c8388-228">此後續觸發程序會在與建立原始文件時的相同交易過程中執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="c8388-229">因此，如果從後續觸發程序擲出例外狀況 (例如，如果我們無法更新中繼資料文件的話)，則整個交易會失敗並予以回復。</span><span class="sxs-lookup"><span data-stu-id="c8388-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="c8388-230">此時不會建立任何文件，並且會傳回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c8388-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="c8388-231"><a id="udf"></a>使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="c8388-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="c8388-232">使用者定義函數 (UDF) 可用來擴充 DocumentDB API SQL 查詢語言文法及實作自訂商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="c8388-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="c8388-233">UDF 只能從內部查詢進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="c8388-233">They can only be called from inside queries.</span></span> <span data-ttu-id="c8388-234">它們無法存取內容物件，只能做為計算用途的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="c8388-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="c8388-235">因此，UDF 可以在 Cosmos DB 服務的次要複本上執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="c8388-236">下列範例會建立 UDF，根據各種收入級距的稅率計算所得稅，然後在查詢內使用它來尋找繳稅超過 $20,000 的所有人員。</span><span class="sxs-lookup"><span data-stu-id="c8388-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="c8388-237">此 UDF 之後可以用於如下列範例所示的查詢中：</span><span class="sxs-lookup"><span data-stu-id="c8388-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="c8388-238">JavaScript Language Integrated Query API</span><span class="sxs-lookup"><span data-stu-id="c8388-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="c8388-239">除了使用 DocumentDB 的 SQL 文法發出查詢，伺服器端 SDK 可讓您使用流暢的 JavaScript 介面執行最佳化查詢，不需具備任何 SQL 的知識。</span><span class="sxs-lookup"><span data-stu-id="c8388-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="c8388-240">JavaScript 的查詢 API 使用 ECMAScript5 陣列內建和受歡迎的 JavaScript 程式庫如 lodash 所熟悉的語法，將述詞函式傳遞至可鏈結式函式呼叫，藉此以程式設計方式建立查詢。</span><span class="sxs-lookup"><span data-stu-id="c8388-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="c8388-241">JavaScript 執行階段會剖析查詢，以使用 Azure Cosmos DB 的索引有效地執行該查詢。</span><span class="sxs-lookup"><span data-stu-id="c8388-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="c8388-242">`__` (雙底線) 是 `getContext().getCollection()` 的別名。</span><span class="sxs-lookup"><span data-stu-id="c8388-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="c8388-243">換句話說，您可以使用 `__` 或 `getContext().getCollection()` 來存取 JavaScript 查詢 API。</span><span class="sxs-lookup"><span data-stu-id="c8388-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="c8388-244">支援的函式包括︰</span><span class="sxs-lookup"><span data-stu-id="c8388-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="c8388-245">
<b>chain() ... .value([callback] [, options])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-246">啟動鏈結的呼叫，必須以 value() 終止。</span><span class="sxs-lookup"><span data-stu-id="c8388-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="c8388-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-248">使用述詞函式篩選輸入，它會傳回 true/false 以將 in/out 輸入文件篩選至結果集。</span><span class="sxs-lookup"><span data-stu-id="c8388-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="c8388-249">此行為類似 SQL 中的 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="c8388-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="c8388-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-251">適用於所指定的轉換函式將每個輸入項目對應至 JavaScript 物件或值的投影。</span><span class="sxs-lookup"><span data-stu-id="c8388-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="c8388-252">此行為類似 SQL 中的 SELECT 子句。</span><span class="sxs-lookup"><span data-stu-id="c8388-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="c8388-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-254">這是從每個輸入項目擷取單一屬性值的對應捷徑。</span><span class="sxs-lookup"><span data-stu-id="c8388-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="c8388-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-256">合併並且壓平每個輸入項目的陣列成為單一陣列。</span><span class="sxs-lookup"><span data-stu-id="c8388-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="c8388-257">此行為類似 LINQ 中的 SelectMany。</span><span class="sxs-lookup"><span data-stu-id="c8388-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="c8388-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-259">使用指定述詞以遞增順序排序輸入文件串流中的文件，產生一組新的文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="c8388-260">此行為類似 SQL 中的 ORDER BY 子句。</span><span class="sxs-lookup"><span data-stu-id="c8388-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="c8388-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span><span class="sxs-lookup"><span data-stu-id="c8388-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="c8388-262">使用指定述詞以遞減順序排序輸入文件串流中的文件，產生一組新的文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="c8388-263">此行為類似 SQL 中的 ORDER BY x DESC 子句。</span><span class="sxs-lookup"><span data-stu-id="c8388-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="c8388-264">當裡面包含述詞和/或選取器函式時，下列 JavaScript 建構會自動取得最佳化，以便直接在 Azure Cosmos DB 索引上執行：</span><span class="sxs-lookup"><span data-stu-id="c8388-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="c8388-265">簡單運算子：= + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="c8388-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="c8388-266">常值，包括 literal: {} 物件</span><span class="sxs-lookup"><span data-stu-id="c8388-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="c8388-267">var、return</span><span class="sxs-lookup"><span data-stu-id="c8388-267">var, return</span></span>

<span data-ttu-id="c8388-268">下列 JavaScript 建構不會取得 Azure Cosmos DB 索引的最佳化：</span><span class="sxs-lookup"><span data-stu-id="c8388-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="c8388-269">控制流程 (例如 if、for、while)</span><span class="sxs-lookup"><span data-stu-id="c8388-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="c8388-270">函式呼叫</span><span class="sxs-lookup"><span data-stu-id="c8388-270">Function calls</span></span>

<span data-ttu-id="c8388-271">如需詳細資訊，請參閱我們的 [伺服器端 JSDocs](http://azure.github.io/azure-documentdb-js-server/)。</span><span class="sxs-lookup"><span data-stu-id="c8388-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="c8388-272">範例：使用 JavaScript 查詢 API 撰寫預存程序</span><span class="sxs-lookup"><span data-stu-id="c8388-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="c8388-273">下列程式碼範例示範 JavaScript 查詢 API 如何運用於預存程序的背景下。</span><span class="sxs-lookup"><span data-stu-id="c8388-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="c8388-274">預存程序會依照指定的輸入參數插入文件，然後使用 `__.filter()` 方法根據輸入文件的大小屬性，以 minSize、maxSize 和 totalSize 來更新中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="c8388-275">SQL 到 Javascript 的速查表</span><span class="sxs-lookup"><span data-stu-id="c8388-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="c8388-276">下列表格包含各種不同的 SQL 查詢和相對應的 JavaScript 查詢。</span><span class="sxs-lookup"><span data-stu-id="c8388-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="c8388-277">使用 SQL 查詢時，文件屬性索引鍵 (例如 `doc.id`) 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="c8388-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="c8388-278">SQL</span><span class="sxs-lookup"><span data-stu-id="c8388-278">SQL</span></span>| <span data-ttu-id="c8388-279">JavaScript 查詢 API</span><span class="sxs-lookup"><span data-stu-id="c8388-279">JavaScript Query API</span></span>|<span data-ttu-id="c8388-280">下列說明</span><span class="sxs-lookup"><span data-stu-id="c8388-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="c8388-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="c8388-281">SELECT *</span></span><br><span data-ttu-id="c8388-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="c8388-282">FROM docs</span></span>| <span data-ttu-id="c8388-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="c8388-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="c8388-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="c8388-285">});</span><span class="sxs-lookup"><span data-stu-id="c8388-285">});</span></span>|<span data-ttu-id="c8388-286">1</span><span class="sxs-lookup"><span data-stu-id="c8388-286">1</span></span>|
|<span data-ttu-id="c8388-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="c8388-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="c8388-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="c8388-288">FROM docs</span></span>|<span data-ttu-id="c8388-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-289">__.map(function(doc) {</span></span><br><span data-ttu-id="c8388-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="c8388-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="c8388-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="c8388-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="c8388-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="c8388-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="c8388-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="c8388-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="c8388-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="c8388-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="c8388-295">});</span><span class="sxs-lookup"><span data-stu-id="c8388-295">});</span></span>|<span data-ttu-id="c8388-296">2</span><span class="sxs-lookup"><span data-stu-id="c8388-296">2</span></span>|
|<span data-ttu-id="c8388-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="c8388-297">SELECT *</span></span><br><span data-ttu-id="c8388-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="c8388-298">FROM docs</span></span><br><span data-ttu-id="c8388-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="c8388-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="c8388-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="c8388-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="c8388-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="c8388-302">});</span><span class="sxs-lookup"><span data-stu-id="c8388-302">});</span></span>|<span data-ttu-id="c8388-303">3</span><span class="sxs-lookup"><span data-stu-id="c8388-303">3</span></span>|
|<span data-ttu-id="c8388-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="c8388-304">SELECT *</span></span><br><span data-ttu-id="c8388-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="c8388-305">FROM docs</span></span><br><span data-ttu-id="c8388-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="c8388-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="c8388-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="c8388-307">__.filter(function(x) {</span></span><br><span data-ttu-id="c8388-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="c8388-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="c8388-309">});</span><span class="sxs-lookup"><span data-stu-id="c8388-309">});</span></span>|<span data-ttu-id="c8388-310">4</span><span class="sxs-lookup"><span data-stu-id="c8388-310">4</span></span>|
|<span data-ttu-id="c8388-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="c8388-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="c8388-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="c8388-312">FROM docs</span></span><br><span data-ttu-id="c8388-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="c8388-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="c8388-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="c8388-314">__.chain()</span></span><br><span data-ttu-id="c8388-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="c8388-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="c8388-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="c8388-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="c8388-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="c8388-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="c8388-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="c8388-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="c8388-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="c8388-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="c8388-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="c8388-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="c8388-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="c8388-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="c8388-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="c8388-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="c8388-324">.value();</span><span class="sxs-lookup"><span data-stu-id="c8388-324">.value();</span></span>|<span data-ttu-id="c8388-325">5</span><span class="sxs-lookup"><span data-stu-id="c8388-325">5</span></span>|
|<span data-ttu-id="c8388-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="c8388-326">SELECT VALUE tag</span></span><br><span data-ttu-id="c8388-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="c8388-327">FROM docs</span></span><br><span data-ttu-id="c8388-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="c8388-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="c8388-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="c8388-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="c8388-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="c8388-330">__.chain()</span></span><br><span data-ttu-id="c8388-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="c8388-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="c8388-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="c8388-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="c8388-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="c8388-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="c8388-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="c8388-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="c8388-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="c8388-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="c8388-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="c8388-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="c8388-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="c8388-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="c8388-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="c8388-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="c8388-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="c8388-340">6</span><span class="sxs-lookup"><span data-stu-id="c8388-340">6</span></span>|

<span data-ttu-id="c8388-341">以下說明解說上表中的每個查詢。</span><span class="sxs-lookup"><span data-stu-id="c8388-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="c8388-342">所有文件中的結果 (使用連續權杖分頁)。</span><span class="sxs-lookup"><span data-stu-id="c8388-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="c8388-343">投射識別碼、訊息 (別名為 msg)，和所有文件中的動作。</span><span class="sxs-lookup"><span data-stu-id="c8388-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="c8388-344">使用 predicate: id = "X998_Y998" 查詢文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="c8388-345">查詢具有 Tags 屬性的文件，且 Tags 是包含值 123 的陣列。</span><span class="sxs-lookup"><span data-stu-id="c8388-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="c8388-346">使用 predicate, id = "X998_Y998" 查詢文件，然後投射識別碼和訊息 (別名為 msg)。</span><span class="sxs-lookup"><span data-stu-id="c8388-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="c8388-347">篩選具有陣列屬性 Tags 的文件，並且依據 _ts 時間戳記系統屬性排序結果文件，然後投射 + 壓平 Tags 陣列。</span><span class="sxs-lookup"><span data-stu-id="c8388-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="c8388-348">執行階段支援</span><span class="sxs-lookup"><span data-stu-id="c8388-348">Runtime support</span></span>
<span data-ttu-id="c8388-349">[DocumentDB JavaScript 伺服器端 API](http://azure.github.io/azure-documentdb-js-server/) 支援以 [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 作為標準的大部分主流 JavaScript 語言功能。</span><span class="sxs-lookup"><span data-stu-id="c8388-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="c8388-350">安全性</span><span class="sxs-lookup"><span data-stu-id="c8388-350">Security</span></span>
<span data-ttu-id="c8388-351">JavaScript 預存程序和觸發程序是在沙箱中執行，除非通過資料庫層級的快照交易隔離機制，否則某個指令碼的效果不會傳遞到另一個指令碼。</span><span class="sxs-lookup"><span data-stu-id="c8388-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="c8388-352">每次執行之後，都會對執行階段環境進行集區化處理，但會清除內容。</span><span class="sxs-lookup"><span data-stu-id="c8388-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="c8388-353">因此，環境與環境彼此之間絕對不會有任何未預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="c8388-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="c8388-354">預先編譯</span><span class="sxs-lookup"><span data-stu-id="c8388-354">Pre-compilation</span></span>
<span data-ttu-id="c8388-355">預存程序、觸發程序和 UDF 會隱含地預先編譯為位元組程式碼格式，以避免掉每次叫用指令碼時的編譯成本。</span><span class="sxs-lookup"><span data-stu-id="c8388-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="c8388-356">這種作法可確保能夠快速叫用預存程序，且只需耗費少量資源。</span><span class="sxs-lookup"><span data-stu-id="c8388-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="c8388-357">用戶端 SDK 支援</span><span class="sxs-lookup"><span data-stu-id="c8388-357">Client SDK support</span></span>
<span data-ttu-id="c8388-358">除了適用於 [Node.js](documentdb-sdk-node.md) 用戶端的 DocumentDB API 之外，Azure Cosmos DB 也具有適用於 DocumentDB API 的 [.NET](documentdb-sdk-dotnet.md)、[.NET Core](documentdb-sdk-dotnet-core.md)、[Java](documentdb-sdk-java.md)、[JavaScript](http://azure.github.io/azure-documentdb-js/) 和 [Python SDK](documentdb-sdk-python.md)。</span><span class="sxs-lookup"><span data-stu-id="c8388-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="c8388-359">使用上述任何 SDK，也可以建立和執行預存程序、觸發程序和 UDF。</span><span class="sxs-lookup"><span data-stu-id="c8388-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="c8388-360">下列範例說明如何使用 .NET 用戶端建立和執行預存程序。</span><span class="sxs-lookup"><span data-stu-id="c8388-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="c8388-361">請注意 .NET 類型是如何在預存程序中以 JSON 形式傳入及讀回。</span><span class="sxs-lookup"><span data-stu-id="c8388-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="c8388-362">此範例示範如何使用 [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) 建立預先觸發程序以及建立已啟用觸發程序的文件。</span><span class="sxs-lookup"><span data-stu-id="c8388-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

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


<span data-ttu-id="c8388-363">下列範例則說明如何建立使用者定義函數 (UDF) 並將它用於 [DocumentDB API SQL 查詢](documentdb-sql-query.md)中。</span><span class="sxs-lookup"><span data-stu-id="c8388-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="c8388-364">REST API</span><span class="sxs-lookup"><span data-stu-id="c8388-364">REST API</span></span>
<span data-ttu-id="c8388-365">所有 Azure Cosmos DB 作業都可以用 RESTful 方式來執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="c8388-366">使用 HTTP POST，就可以將預存程序、觸發程序和使用者定義函數註冊至某個集合下。</span><span class="sxs-lookup"><span data-stu-id="c8388-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="c8388-367">下列是如何註冊預存程序的範例：</span><span class="sxs-lookup"><span data-stu-id="c8388-367">The following is an example of how to register a stored procedure:</span></span>

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


<span data-ttu-id="c8388-368">預存程序的註冊方式是使用包含要建立的預存程序的本文，對 URI dbs/testdb/colls/testColl/sprocs 執行 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="c8388-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="c8388-369">觸發程序和 UDF可以透過分別發出 /triggers 和 /udfs 的 POST 要求，以類似方式進行註冊。</span><span class="sxs-lookup"><span data-stu-id="c8388-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="c8388-370">您可以接著對其資源連結發出 POST 要求來執行這個預存程序：</span><span class="sxs-lookup"><span data-stu-id="c8388-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="c8388-371">在這裡，預存程序的輸入會傳入要求本文中。</span><span class="sxs-lookup"><span data-stu-id="c8388-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="c8388-372">請注意，輸入會以 JSON 輸入參數陣列的形式傳遞。</span><span class="sxs-lookup"><span data-stu-id="c8388-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="c8388-373">預存程序會將第一個輸入做為文件 (即回應本文)。</span><span class="sxs-lookup"><span data-stu-id="c8388-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="c8388-374">我們收到的回應如下：</span><span class="sxs-lookup"><span data-stu-id="c8388-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="c8388-375">觸發程序與預存程序不同，無法直接執行，</span><span class="sxs-lookup"><span data-stu-id="c8388-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="c8388-376">而是在對文件執行作業時執行。</span><span class="sxs-lookup"><span data-stu-id="c8388-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="c8388-377">我們可以使用 HTTP 標頭指定要與要求搭配執行的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c8388-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="c8388-378">下列是建立文件的要求。</span><span class="sxs-lookup"><span data-stu-id="c8388-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="c8388-379">在這裏，要與要求搭配執行的預先觸發程序指定於 x-ms-documentdb-pre-trigger-include 標頭中。</span><span class="sxs-lookup"><span data-stu-id="c8388-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="c8388-380">相對應地，後續觸發程序則是指定於 x-ms-documentdb-post-trigger-include 標頭中。</span><span class="sxs-lookup"><span data-stu-id="c8388-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="c8388-381">請注意，您可以指定給定要求的預先和後續觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c8388-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="c8388-382">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="c8388-382">Sample code</span></span>
<span data-ttu-id="c8388-383">您可以在我們的 [GitHub 存放庫](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples)上找到更多的伺服器端程式碼範例 (包括 [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) 和 [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js))。</span><span class="sxs-lookup"><span data-stu-id="c8388-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="c8388-384">想要共用您絕佳的預存程序嗎？</span><span class="sxs-lookup"><span data-stu-id="c8388-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="c8388-385">請傳送提取要求給我們！</span><span class="sxs-lookup"><span data-stu-id="c8388-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c8388-386">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8388-386">Next steps</span></span>
<span data-ttu-id="c8388-387">一旦您建立一或多個預存程序、觸發程序和使用者定義函數，您可以使用資料總管在 Azure 入口網站中載入並檢視這些項目。</span><span class="sxs-lookup"><span data-stu-id="c8388-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="c8388-388">您還可以在您的路徑中找到下列有用的參考和資源，以深入了解 Azure Cosmos DB 伺服器端程式設計：</span><span class="sxs-lookup"><span data-stu-id="c8388-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="c8388-389">Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="c8388-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="c8388-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="c8388-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="c8388-391">JSON</span><span class="sxs-lookup"><span data-stu-id="c8388-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="c8388-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="c8388-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="c8388-393">安全和可攜式資料庫擴充性</span><span class="sxs-lookup"><span data-stu-id="c8388-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="c8388-394">服務導向資料庫架構</span><span class="sxs-lookup"><span data-stu-id="c8388-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="c8388-395">在 Microsoft SQL Server 中託管 .NET 執行階段</span><span class="sxs-lookup"><span data-stu-id="c8388-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

