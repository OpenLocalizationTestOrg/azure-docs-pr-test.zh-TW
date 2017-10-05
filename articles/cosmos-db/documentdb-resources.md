---
title: "Azure Cosmos DB 資源模型和概念 | Microsoft Docs"
description: "深入了解 Azure Cosmos DB 資料庫的階層式模型、集合、使用者定義函數 (UDF)、文件、權限，以便管理資源等。"
keywords: "階層式模型, Hierarchical model, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8051742c7c368d1ed84bcd90ab75b20f62105e2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a><span data-ttu-id="f869d-104">Azure Cosmos DB 階層式資源模型和核心概念</span><span class="sxs-lookup"><span data-stu-id="f869d-104">Azure Cosmos DB hierarchical resource model and core concepts</span></span>
<span data-ttu-id="f869d-105">Azure Cosmos DB 管理的資料庫實體稱為「資源」。</span><span class="sxs-lookup"><span data-stu-id="f869d-105">The database entities that Azure Cosmos DB manages are referred to as **resources**.</span></span> <span data-ttu-id="f869d-106">每個資源可透過邏輯 URI 唯一識別。</span><span class="sxs-lookup"><span data-stu-id="f869d-106">Each resource is uniquely identified by a logical URI.</span></span> <span data-ttu-id="f869d-107">您可以使用標準 HTTP 動詞命令、要求/回應標頭和狀態碼來與資源互動。</span><span class="sxs-lookup"><span data-stu-id="f869d-107">You can interact with the resources using standard HTTP verbs, request/response headers and status codes.</span></span> 

<span data-ttu-id="f869d-108">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="f869d-108">By reading this article, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="f869d-109">什麼是 Cosmos DB 的資源模型？</span><span class="sxs-lookup"><span data-stu-id="f869d-109">What is Cosmos DB's resource model?</span></span>
* <span data-ttu-id="f869d-110">什麼是系統定義的資源？與使用者定義的資源有何差異？</span><span class="sxs-lookup"><span data-stu-id="f869d-110">What are system defined resources as opposed to user defined resources?</span></span>
* <span data-ttu-id="f869d-111">如何處理資源？</span><span class="sxs-lookup"><span data-stu-id="f869d-111">How do I address a resource?</span></span>
* <span data-ttu-id="f869d-112">如何使用集合？</span><span class="sxs-lookup"><span data-stu-id="f869d-112">How do I work with collections?</span></span>
* <span data-ttu-id="f869d-113">如何使用預存程序、觸發程序和使用者定義函數 (UDF)？</span><span class="sxs-lookup"><span data-stu-id="f869d-113">How do I work with stored procedures, triggers and User Defined Functions (UDFs)?</span></span>

## <a name="hierarchical-resource-model"></a><span data-ttu-id="f869d-114">階層式資源模型</span><span class="sxs-lookup"><span data-stu-id="f869d-114">Hierarchical resource model</span></span>
<span data-ttu-id="f869d-115">如下圖所示，Cosmos DB 的階層式「資源模型」包含某個資料庫帳戶下的多組資源，而每組資源都可透過邏輯和穩定 URI 加以定址。</span><span class="sxs-lookup"><span data-stu-id="f869d-115">As the following diagram illustrates, the Cosmos DB hierarchical **resource model** consists of sets of resources under a database account, each addressable via a logical and stable URI.</span></span> <span data-ttu-id="f869d-116">在本文中，一組資源稱為 **摘要** 。</span><span class="sxs-lookup"><span data-stu-id="f869d-116">A set of resources will be referred to as a **feed** in this article.</span></span> 

> [!NOTE]
> <span data-ttu-id="f869d-117">Azure Cosmos DB 提供高效率的 TCP 通訊協定，此 TCP 通訊協定在通訊模型中也符合 REST 限制，並且可以透過 [DocumentDB .NET 用戶端 API](documentdb-sdk-dotnet.md) 取得。</span><span class="sxs-lookup"><span data-stu-id="f869d-117">Azure Cosmos DB offers a highly efficient TCP protocol which is also RESTful in its communication model, available through the [DocumentDB .NET client API](documentdb-sdk-dotnet.md).</span></span>
> 
> 

<span data-ttu-id="f869d-118">![Azure Cosmos DB 階層式資源模型][1]</span><span class="sxs-lookup"><span data-stu-id="f869d-118">![Azure Cosmos DB hierarchical resource model][1]</span></span>  
<span data-ttu-id="f869d-119">**階層式資源模型**</span><span class="sxs-lookup"><span data-stu-id="f869d-119">**Hierarchical resource model**</span></span>   

<span data-ttu-id="f869d-120">若要開始使用資源，您必須使用 Azure 訂用帳戶[建立資料庫帳戶](create-documentdb-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f869d-120">To start working with resources, you must [create a database account](create-documentdb-dotnet.md) using your Azure subscription.</span></span> <span data-ttu-id="f869d-121">資料庫帳戶包含一組「資料庫」，而每個資料庫都包含多個「集合」，且各集合因此包含「預存程序」、「觸發程序」、UDF、「文件」和相關「附件」。</span><span class="sxs-lookup"><span data-stu-id="f869d-121">A database account can consist of a set of **databases**, each containing multiple **collections**, each of which in turn contain **stored procedures, triggers, UDFs, documents** and related **attachments**.</span></span> <span data-ttu-id="f869d-122">資料庫也有相關聯的**使用者**，其中每位使用者都有一組可存取集合、預存程序、觸發程序、UDF、文件或附件的**權限**。</span><span class="sxs-lookup"><span data-stu-id="f869d-122">A database also has associated **users**, each with a set of **permissions** to access collections, stored procedures, triggers, UDFs, documents or attachments.</span></span> <span data-ttu-id="f869d-123">雖然資料庫、使用者、權限和集合都是具有已知結構描述的系統定義資源，但是文件和附件包含任意使用者定義 JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="f869d-123">While databases, users, permissions and collections are system-defined resources with well-known schemas, documents and attachments contain arbitrary, user defined JSON content.</span></span>  

| <span data-ttu-id="f869d-124">資源</span><span class="sxs-lookup"><span data-stu-id="f869d-124">Resource</span></span> | <span data-ttu-id="f869d-125">說明</span><span class="sxs-lookup"><span data-stu-id="f869d-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f869d-126">資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="f869d-126">Database account</span></span> |<span data-ttu-id="f869d-127">資料庫帳戶會與一組資料庫及附件之固定數目的 Blob 儲存體相關聯。</span><span class="sxs-lookup"><span data-stu-id="f869d-127">A database account is associated with a set of databases and a fixed amount of blob storage for attachments.</span></span> <span data-ttu-id="f869d-128">您可以使用 Azure 訂用帳戶建立一或多個資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="f869d-128">You can create one or more database accounts using your Azure subscription.</span></span> <span data-ttu-id="f869d-129">如需詳細資訊，請瀏覽我們的 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="f869d-129">For more information, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> |
| <span data-ttu-id="f869d-130">資料庫</span><span class="sxs-lookup"><span data-stu-id="f869d-130">Database</span></span> |<span data-ttu-id="f869d-131">資料庫是分割給多個集合之文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="f869d-131">A database is a logical container of document storage partitioned across collections.</span></span> <span data-ttu-id="f869d-132">同時也是使用者容器。</span><span class="sxs-lookup"><span data-stu-id="f869d-132">It is also a users container.</span></span> |
| <span data-ttu-id="f869d-133">User</span><span class="sxs-lookup"><span data-stu-id="f869d-133">User</span></span> |<span data-ttu-id="f869d-134">範圍權限的邏輯命名空間。</span><span class="sxs-lookup"><span data-stu-id="f869d-134">The logical namespace for scoping permissions.</span></span> |
| <span data-ttu-id="f869d-135">權限</span><span class="sxs-lookup"><span data-stu-id="f869d-135">Permission</span></span> |<span data-ttu-id="f869d-136">與使用者相關聯的授權權杖，可讓使用者用於存取特定資源。</span><span class="sxs-lookup"><span data-stu-id="f869d-136">An authorization token associated with a user for access to a specific resource.</span></span> |
| <span data-ttu-id="f869d-137">集合</span><span class="sxs-lookup"><span data-stu-id="f869d-137">Collection</span></span> |<span data-ttu-id="f869d-138">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="f869d-138">A collection is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="f869d-139">集合是計費實體，其中的 [成本](performance-levels.md) 是由與集合相關聯的效能層級所決定。</span><span class="sxs-lookup"><span data-stu-id="f869d-139">A collection is a billable entity, where the [cost](performance-levels.md) is determined by the performance level associated with the collection.</span></span> <span data-ttu-id="f869d-140">集合可以跨越一或多個資料分割/伺服器，也可以進行調整以處理幾乎無限量的儲存體或輸送量。</span><span class="sxs-lookup"><span data-stu-id="f869d-140">Collections can span one or more partitions/servers and can scale to handle practically unlimited volumes of storage or throughput.</span></span> |
| <span data-ttu-id="f869d-141">預存程序</span><span class="sxs-lookup"><span data-stu-id="f869d-141">Stored Procedure</span></span> |<span data-ttu-id="f869d-142">以 JavaScript 撰寫的應用程式邏輯，會向集合註冊並透過交易方式在資料庫引擎內執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-142">Application logic written in JavaScript which is registered with a collection and transactionally executed within the database engine.</span></span> |
| <span data-ttu-id="f869d-143">觸發程序</span><span class="sxs-lookup"><span data-stu-id="f869d-143">Trigger</span></span> |<span data-ttu-id="f869d-144">以 JavaScript 撰寫的應用程式邏輯，會在插入、取代或刪除作業之前或之後執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-144">Application logic written in JavaScript executed before or after either an insert, replace or delete operation.</span></span> |
| <span data-ttu-id="f869d-145">UDF</span><span class="sxs-lookup"><span data-stu-id="f869d-145">UDF</span></span> |<span data-ttu-id="f869d-146">以 JavaScript 撰寫的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="f869d-146">Application logic written in JavaScript.</span></span> <span data-ttu-id="f869d-147">UDF 可讓您建立自訂查詢運算子的模型，進而擴充核心 DocumentDB API 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="f869d-147">UDFs enable you to model a custom query operator and thereby extend the core DocumentDB API query language.</span></span> |
| <span data-ttu-id="f869d-148">文件</span><span class="sxs-lookup"><span data-stu-id="f869d-148">Document</span></span> |<span data-ttu-id="f869d-149">使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="f869d-149">User defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f869d-150">依照預設，不是不需要定義任何結構描述，就是需要提供所有新增至集合之文件的次要索引。</span><span class="sxs-lookup"><span data-stu-id="f869d-150">By default, no schema needs to be defined nor do secondary indices need to be provided for all the documents added to a collection.</span></span> |
| <span data-ttu-id="f869d-151">附件</span><span class="sxs-lookup"><span data-stu-id="f869d-151">Attachment</span></span> |<span data-ttu-id="f869d-152">附件是含有外部 Blob/媒體之參考資料和相關聯中繼資料的特殊文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-152">An attachment is a special document containing references and associated metadata for external blob/media.</span></span> <span data-ttu-id="f869d-153">開發人員可以選擇讓 Cosmos DB 管理 Blob，或使用外部 Blob 服務提供者 (例如 OneDrive、Dropbox 等) 儲存 Blob。</span><span class="sxs-lookup"><span data-stu-id="f869d-153">The developer can choose to have the blob managed by Cosmos DB or store it with an external blob service provider such as OneDrive, Dropbox, etc.</span></span> |

## <a name="system-vs-user-defined-resources"></a><span data-ttu-id="f869d-154">系統與使用者定義的資源</span><span class="sxs-lookup"><span data-stu-id="f869d-154">System vs. user defined resources</span></span>
<span data-ttu-id="f869d-155">資料庫帳戶、資料庫、集合、使用者、權限、預存程序、觸發程序和 UDF 等資源的結構描述都是固定不變的，因此稱為「系統資源」。</span><span class="sxs-lookup"><span data-stu-id="f869d-155">Resources such as database accounts, databases, collections, users, permissions, stored procedures, triggers, and UDFs - all have a fixed schema and are called system resources.</span></span> <span data-ttu-id="f869d-156">相反地，文件和附件等資源則是「使用者定義的資源」的範例，因為這些資源的結構描述沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="f869d-156">In contrast, resources such as documents and attachments have no restrictions on the schema and are examples of user defined resources.</span></span> <span data-ttu-id="f869d-157">在 Cosmos DB 中，系統和使用者定義資源都會呈現和管理為標準相符 JSON。</span><span class="sxs-lookup"><span data-stu-id="f869d-157">In Cosmos DB, both system and user defined resources are represented and managed as standard-compliant JSON.</span></span> <span data-ttu-id="f869d-158">所有資源 (不論是系統定義的還是使用者定義的) 都具有下列共同屬性。</span><span class="sxs-lookup"><span data-stu-id="f869d-158">All resources, system or user defined, have the following common properties.</span></span>

> [!NOTE]
> <span data-ttu-id="f869d-159">請注意，系統產生的資源屬性在以 JSON 形式表示時，前面都會加上底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="f869d-159">Note that all system generated properties in a resource are prefixed with an underscore (_) in their JSON representation.</span></span>
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-160"><strong>屬性</strong></span><span class="sxs-lookup"><span data-stu-id="f869d-160"><strong>Property</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-161"><strong>可由使用者設定或由系統產生？</strong></span><span class="sxs-lookup"><span data-stu-id="f869d-161"><strong>User settable or system generated?</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-162"><strong>用途</strong></span><span class="sxs-lookup"><span data-stu-id="f869d-162"><strong>Purpose</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-163">_rid</span><span class="sxs-lookup"><span data-stu-id="f869d-163">_rid</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-164">由系統產生</span><span class="sxs-lookup"><span data-stu-id="f869d-164">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-165">系統產生的唯一階層式資源識別碼</span><span class="sxs-lookup"><span data-stu-id="f869d-165">System generated, unique and hierarchical identifier of the resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-166">_etag</span><span class="sxs-lookup"><span data-stu-id="f869d-166">_etag</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-167">由系統產生</span><span class="sxs-lookup"><span data-stu-id="f869d-167">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-168">要控制開放式並行存取所需之資源的 etag</span><span class="sxs-lookup"><span data-stu-id="f869d-168">etag of the resource required for optimistic concurrency control</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-169">_ts</span><span class="sxs-lookup"><span data-stu-id="f869d-169">_ts</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-170">由系統產生</span><span class="sxs-lookup"><span data-stu-id="f869d-170">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-171">資源上次更新之時間的時間戳記</span><span class="sxs-lookup"><span data-stu-id="f869d-171">Last updated timestamp of the resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-172">_self</span><span class="sxs-lookup"><span data-stu-id="f869d-172">_self</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-173">由系統產生</span><span class="sxs-lookup"><span data-stu-id="f869d-173">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-174">資源的唯一可定址 URI</span><span class="sxs-lookup"><span data-stu-id="f869d-174">Unique addressable URI of the resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-175">id</span><span class="sxs-lookup"><span data-stu-id="f869d-175">id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-176">由系統產生</span><span class="sxs-lookup"><span data-stu-id="f869d-176">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-177">使用者定義的資源唯一名稱 (具有相同的分割索引鍵值)。</span><span class="sxs-lookup"><span data-stu-id="f869d-177">User defined unique name of the resource (with the same partition key value).</span></span> <span data-ttu-id="f869d-178">如果使用者未指定 id，系統產生將會 id</span><span class="sxs-lookup"><span data-stu-id="f869d-178">If the user does not specify an id, an id will be system generated</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a><span data-ttu-id="f869d-179">以線路表示資源</span><span class="sxs-lookup"><span data-stu-id="f869d-179">Wire representation of resources</span></span>
<span data-ttu-id="f869d-180">Cosmos DB 不會要求您提供用於 JSON 標準或特殊編碼的專屬延伸模組；Cosmos DB 本身就能處理符合 JSON 標準的文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-180">Cosmos DB does not mandate any proprietary extensions to the JSON standard or special encodings; it works with standard compliant JSON documents.</span></span>  

### <a name="addressing-a-resource"></a><span data-ttu-id="f869d-181">資源定址</span><span class="sxs-lookup"><span data-stu-id="f869d-181">Addressing a resource</span></span>
<span data-ttu-id="f869d-182">所有資源都能以 URI 定址。</span><span class="sxs-lookup"><span data-stu-id="f869d-182">All resources are URI addressable.</span></span> <span data-ttu-id="f869d-183">資源的 **_self** 屬性值代表資源的相對 URI。</span><span class="sxs-lookup"><span data-stu-id="f869d-183">The value of the **_self** property of a resource represents the relative URI of the resource.</span></span> <span data-ttu-id="f869d-184">URI 的格式是由 /\<feed\>/{_rid} 路徑片段所組成：</span><span class="sxs-lookup"><span data-stu-id="f869d-184">The format of the URI consists of the /\<feed\>/{_rid} path segments:</span></span>  

| <span data-ttu-id="f869d-185">_self 的值</span><span class="sxs-lookup"><span data-stu-id="f869d-185">Value of the _self</span></span> | <span data-ttu-id="f869d-186">說明</span><span class="sxs-lookup"><span data-stu-id="f869d-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f869d-187">/dbs</span><span class="sxs-lookup"><span data-stu-id="f869d-187">/dbs</span></span> |<span data-ttu-id="f869d-188">資料庫帳戶下的資料庫摘要</span><span class="sxs-lookup"><span data-stu-id="f869d-188">Feed of databases under a database account</span></span> |
| <span data-ttu-id="f869d-189">/dbs/{dbName}</span><span class="sxs-lookup"><span data-stu-id="f869d-189">/dbs/{dbName}</span></span> |<span data-ttu-id="f869d-190">具有符合值 {dbName} 的識別碼的資料庫</span><span class="sxs-lookup"><span data-stu-id="f869d-190">Database with an id matching the value {dbName}</span></span> |
| <span data-ttu-id="f869d-191">/dbs/{dbName}/colls/</span><span class="sxs-lookup"><span data-stu-id="f869d-191">/dbs/{dbName}/colls/</span></span> |<span data-ttu-id="f869d-192">在資料庫底下的集合摘要</span><span class="sxs-lookup"><span data-stu-id="f869d-192">Feed of collections under a database</span></span> |
| <span data-ttu-id="f869d-193">/dbs/{dbName}/colls/{collName}</span><span class="sxs-lookup"><span data-stu-id="f869d-193">/dbs/{dbName}/colls/{collName}</span></span> |<span data-ttu-id="f869d-194">具有符合值 {collName} 的識別碼的集合</span><span class="sxs-lookup"><span data-stu-id="f869d-194">Collection with an id matching the value {collName}</span></span> |
| <span data-ttu-id="f869d-195">/dbs/{dbName}/colls/{collName}/docs</span><span class="sxs-lookup"><span data-stu-id="f869d-195">/dbs/{dbName}/colls/{collName}/docs</span></span> |<span data-ttu-id="f869d-196">在集合底下的文件摘要</span><span class="sxs-lookup"><span data-stu-id="f869d-196">Feed of documents under a collection</span></span> |
| <span data-ttu-id="f869d-197">/dbs/{dbName}/colls/{collName}/docs/{docId}</span><span class="sxs-lookup"><span data-stu-id="f869d-197">/dbs/{dbName}/colls/{collName}/docs/{docId}</span></span> |<span data-ttu-id="f869d-198">具有符合值 {doc} 的識別碼的文件</span><span class="sxs-lookup"><span data-stu-id="f869d-198">Document with an id matching the value {doc}</span></span> |
| <span data-ttu-id="f869d-199">/dbs/{dbName}/users/</span><span class="sxs-lookup"><span data-stu-id="f869d-199">/dbs/{dbName}/users/</span></span> |<span data-ttu-id="f869d-200">在資料庫底下的使用者摘要</span><span class="sxs-lookup"><span data-stu-id="f869d-200">Feed of users under a database</span></span> |
| <span data-ttu-id="f869d-201">/dbs/{dbName}/users/{userId}</span><span class="sxs-lookup"><span data-stu-id="f869d-201">/dbs/{dbName}/users/{userId}</span></span> |<span data-ttu-id="f869d-202">具有符合值 {user} 的識別碼的使用者</span><span class="sxs-lookup"><span data-stu-id="f869d-202">User with an id matching the value {user}</span></span> |
| <span data-ttu-id="f869d-203">/dbs/{dbName}/users/{userId}/permissions</span><span class="sxs-lookup"><span data-stu-id="f869d-203">/dbs/{dbName}/users/{userId}/permissions</span></span> |<span data-ttu-id="f869d-204">在使用者底下的權限摘要</span><span class="sxs-lookup"><span data-stu-id="f869d-204">Feed of permissions under a user</span></span> |
| <span data-ttu-id="f869d-205">/dbs/{dbName}/users/{userId}/permissions/{permissionId}</span><span class="sxs-lookup"><span data-stu-id="f869d-205">/dbs/{dbName}/users/{userId}/permissions/{permissionId}</span></span> |<span data-ttu-id="f869d-206">具有符合值 {permission} 的識別碼的權限</span><span class="sxs-lookup"><span data-stu-id="f869d-206">Permission with an id matching the value {permission}</span></span> |

<span data-ttu-id="f869d-207">每項資源都具有一個使用者所定義的不重複名稱，並會透過 id 屬性公開。</span><span class="sxs-lookup"><span data-stu-id="f869d-207">Each resource has a unique user defined name exposed via the id property.</span></span> <span data-ttu-id="f869d-208">注意：就文件而言，如果使用者未指定識別碼，我們支援的 SDK 將會自動為文件產生唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f869d-208">Note: for documents, if the user does not specify an id, our supported SDKs will automatically generate a unique id for the document.</span></span> <span data-ttu-id="f869d-209">id 是使用者定義的字串，最多 256 個字元，且在特定父系資源的內容中會是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f869d-209">The id is a user defined string, of up to 256 characters that is unique within the context of a specific parent resource.</span></span> 

<span data-ttu-id="f869d-210">每個資源還會有系統產生的階層式資源識別碼 (也稱為 RID)，其可透過 _rid 屬性取得。</span><span class="sxs-lookup"><span data-stu-id="f869d-210">Each resource also has a system generated hierarchical resource identifier (also referred to as an RID), which is available via the _rid property.</span></span> <span data-ttu-id="f869d-211">RID 會對指定資源的整個階層進行編碼，此內部表示法十分方便，可透過分散方式強制執行參考完整性。</span><span class="sxs-lookup"><span data-stu-id="f869d-211">The RID encodes the entire hierarchy of a given resource and it is a convenient internal representation used to enforce referential integrity in a distributed manner.</span></span> <span data-ttu-id="f869d-212">RID 在資料庫帳戶內不會重複。Cosmos DB 會在內部使用 RID，完全無須跨資料分割進行查閱，就能有效率地進行路由。</span><span class="sxs-lookup"><span data-stu-id="f869d-212">The RID is unique within a database account and it is internally used by Cosmos DB for efficient routing without requiring cross partition lookups.</span></span> <span data-ttu-id="f869d-213">_self 和 _rid 屬性的值都是資源的替代及標準表示法。</span><span class="sxs-lookup"><span data-stu-id="f869d-213">The values of the _self and the  _rid properties are both alternate and canonical representations of a resource.</span></span> 

<span data-ttu-id="f869d-214">REST API 可透過識別碼與 _rid 屬性，支援資源的定址和要求的路由。</span><span class="sxs-lookup"><span data-stu-id="f869d-214">The REST APIs support addressing of resources and routing of requests by both the id and the _rid properties.</span></span>

## <a name="database-accounts"></a><span data-ttu-id="f869d-215">資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="f869d-215">Database accounts</span></span>
<span data-ttu-id="f869d-216">您可以使用 Azure 訂用帳戶佈建一或多個 Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="f869d-216">You can provision one or more Cosmos DB database accounts using your Azure subscription.</span></span>

<span data-ttu-id="f869d-217">您可以透過 Azure 入口網站 (網址 [http://portal.azure.com/](https://portal.azure.com/)) 建立和管理 Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="f869d-217">You can create and manage Cosmos DB database accounts via the Azure Portal at [http://portal.azure.com/](https://portal.azure.com/).</span></span> <span data-ttu-id="f869d-218">建立和管理資料庫帳戶都需要管理存取權，而且只有在 Azure 訂用帳戶下才能執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-218">Creating and managing a database account requires administrative access and can only be performed under your Azure subscription.</span></span> 

### <a name="database-account-properties"></a><span data-ttu-id="f869d-219">資料庫帳戶屬性</span><span class="sxs-lookup"><span data-stu-id="f869d-219">Database account properties</span></span>
<span data-ttu-id="f869d-220">在佈建和管理資料庫帳戶時，您可以設定和讀取下列屬性：</span><span class="sxs-lookup"><span data-stu-id="f869d-220">As part of provisioning and managing a database account you can configure and read the following properties:</span></span>  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-221"><strong>屬性名稱</strong></span><span class="sxs-lookup"><span data-stu-id="f869d-221"><strong>Property Name</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-222"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="f869d-222"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-223">一致性原則</span><span class="sxs-lookup"><span data-stu-id="f869d-223">Consistency Policy</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-224">設定此屬性，以設定您資料庫帳戶下所有集合的預設一致性層級。</span><span class="sxs-lookup"><span data-stu-id="f869d-224">Set this property to configure the default consistency level for all the collections under your database account.</span></span> <span data-ttu-id="f869d-225">您可以使用 [x-ms-consistency-level] 要求標頭，覆寫每個要求的一致性層級。</span><span class="sxs-lookup"><span data-stu-id="f869d-225">You can override the consistency level on a per request basis using the [x-ms-consistency-level] request header.</span></span> <p><p><span data-ttu-id="f869d-226">請注意，此屬性僅適用於「使用者定義的資源」<i></i>。</span><span class="sxs-lookup"><span data-stu-id="f869d-226">Note that this property only applies to the <i>user defined resources</i>.</span></span> <span data-ttu-id="f869d-227">所有系統定義資源都是設定成支援具有強式一致性的讀取/查詢。</span><span class="sxs-lookup"><span data-stu-id="f869d-227">All system defined resources are configured to support reads/queries with strong consistency.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f869d-228">授權金鑰</span><span class="sxs-lookup"><span data-stu-id="f869d-228">Authorization Keys</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f869d-229">這些是主要和次要且唯讀金鑰，提供資料庫帳戶下所有資源的管理存取權。</span><span class="sxs-lookup"><span data-stu-id="f869d-229">These are the primary and secondary master and readonly keys that provide administrative access to all of the resources under the database account.</span></span></p></td>
        </tr>
    </tbody>
</table>

<span data-ttu-id="f869d-230">請注意，除了從「Azure 入口網站」佈建、設定及管理資料庫帳戶之外，您也可以透過使用 [Azure Cosmos DB REST API (英文)](/rest/api/documentdb/) 以及[用戶端 SDK (英文)](documentdb-sdk-dotnet.md)，以程式設計方式建立和管理 Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="f869d-230">Note that in addition to provisioning, configuring and managing your database account from the Azure Portal, you can also programmatically create and manage Cosmos DB database accounts by using the [Azure Cosmos DB REST APIs](/rest/api/documentdb/) as well as [client SDKs](documentdb-sdk-dotnet.md).</span></span>  

## <a name="databases"></a><span data-ttu-id="f869d-231">資料庫</span><span class="sxs-lookup"><span data-stu-id="f869d-231">Databases</span></span>
<span data-ttu-id="f869d-232">Cosmos DB 資料庫是一個或多個集合和使用者的邏輯容器，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f869d-232">A Cosmos DB database is a logical container of one or more collections and users, as shown in the following diagram.</span></span> <span data-ttu-id="f869d-233">您可以在 Cosmos DB 資料庫帳戶下，根據供應項目限制建立任意數目的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f869d-233">You can create any number of databases under a Cosmos DB database account subject to offer limits.</span></span>  

<span data-ttu-id="f869d-234">![資料庫帳戶和集合階層式模型][2]</span><span class="sxs-lookup"><span data-stu-id="f869d-234">![Database account and collections hierarchical model][2]</span></span>  
<span data-ttu-id="f869d-235">**資料庫是使用者和集合的邏輯容器**</span><span class="sxs-lookup"><span data-stu-id="f869d-235">**A Database is a logical container of users and collections**</span></span>

<span data-ttu-id="f869d-236">資料庫可包含集合內分割的文件儲存體數量幾乎不受限制。</span><span class="sxs-lookup"><span data-stu-id="f869d-236">A database can contain virtually unlimited document storage partitioned within collections.</span></span>

### <a name="elastic-scale-of-a-cosmos-db-database"></a><span data-ttu-id="f869d-237">Cosmos DB 資料庫靈活的擴充能力</span><span class="sxs-lookup"><span data-stu-id="f869d-237">Elastic scale of a Cosmos DB database</span></span>
<span data-ttu-id="f869d-238">Cosmos DB 資料庫預設相當靈活，範圍從幾 GB 到數 PB 的 SSD 型式文件儲存體和佈建輸送量。</span><span class="sxs-lookup"><span data-stu-id="f869d-238">A Cosmos DB database is elastic by default – ranging from a few GB to petabytes of SSD backed document storage and provisioned throughput.</span></span> 

<span data-ttu-id="f869d-239">不同於傳統 RDBMS 中的資料庫，Cosmos DB 中的資料庫不會侷限在單一電腦中。</span><span class="sxs-lookup"><span data-stu-id="f869d-239">Unlike a database in traditional RDBMS, a database in Cosmos DB is not scoped to a single machine.</span></span> <span data-ttu-id="f869d-240">有了 Cosmos DB 之後，您就能隨著應用程式的規模而相應放大，並能建立更多的集合及 (或) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f869d-240">With Cosmos DB, as your application’s scale needs to grow, you can create more collections, databases, or both.</span></span> <span data-ttu-id="f869d-241">的確，Microsoft 中的各種第一方應用程式都是依消費者規模來使用 Cosmos DB，建立極大的 Cosmos DB 資料庫，每個資料庫各包含數千個具有好幾 TB 文件儲存體的集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-241">Indeed, various first party applications within Microsoft have been using Cosmos DB at a consumer scale by creating extremely large Cosmos DB databases each containing thousands of collections with terabytes of document storage.</span></span> <span data-ttu-id="f869d-242">您可以新增或移除集合來擴充或縮減資料庫，以配合您的應用程式規模需求。</span><span class="sxs-lookup"><span data-stu-id="f869d-242">You can grow or shrink a database by adding or removing collections to meet your application’s scale requirements.</span></span> 

<span data-ttu-id="f869d-243">您可以依據供應項目，在資料庫中建立任意數目的集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-243">You can create any number of collections within a database subject to the offer.</span></span> <span data-ttu-id="f869d-244">視選取的效能層而定，每個集合都有為您佈建的 SSD-backed 儲存體和輸出量。</span><span class="sxs-lookup"><span data-stu-id="f869d-244">Each collection has SSD backed storage and throughput provisioned for you depending on the selected performance tier.</span></span>

<span data-ttu-id="f869d-245">Cosmos DB 資料庫同時也是使用者的容器。</span><span class="sxs-lookup"><span data-stu-id="f869d-245">A Cosmos DB database is also a container of users.</span></span> <span data-ttu-id="f869d-246">使用者因此是一組權限的邏輯命名空間，可針對集合、文件和附件提供微調的授權和存取權。</span><span class="sxs-lookup"><span data-stu-id="f869d-246">A user, in-turn, is a logical namespace for a set of permissions that provides fine-grained authorization and access to collections, documents and attachments.</span></span>  

<span data-ttu-id="f869d-247">與 Cosmos DB 資源模型中的其他資源相同，不論是使用 [REST API](/rest/api/documentdb/) 還是任何[用戶端 SDK](documentdb-sdk-dotnet.md)，都可輕鬆地建立、取代、刪除、讀取或列舉資料庫。</span><span class="sxs-lookup"><span data-stu-id="f869d-247">As with other resources in the Cosmos DB resource model, databases can be created, replaced, deleted, read or enumerated easily using either the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="f869d-248">Cosmos DB 保證讀取或查詢資料庫資源之中繼資料的強式一致性。</span><span class="sxs-lookup"><span data-stu-id="f869d-248">Cosmos DB guarantees strong consistency for reading or querying the metadata of a database resource.</span></span> <span data-ttu-id="f869d-249">刪除資料庫會自動確定您無法存取其內所含的任何集合或使用者。</span><span class="sxs-lookup"><span data-stu-id="f869d-249">Deleting a database automatically ensures that you cannot access any of the collections or users contained within it.</span></span>   

## <a name="collections"></a><span data-ttu-id="f869d-250">集合</span><span class="sxs-lookup"><span data-stu-id="f869d-250">Collections</span></span>
<span data-ttu-id="f869d-251">Cosmos DB 集合是 JSON 文件的容器。</span><span class="sxs-lookup"><span data-stu-id="f869d-251">A Cosmos DB collection is a container for your JSON documents.</span></span> 

### <a name="elastic-ssd-backed-document-storage"></a><span data-ttu-id="f869d-252">彈性 SSD 支持文件儲存體</span><span class="sxs-lookup"><span data-stu-id="f869d-252">Elastic SSD backed document storage</span></span>
<span data-ttu-id="f869d-253">集合本質上是彈性的 - 它會隨著您新增或移除文件自動成長和縮減。</span><span class="sxs-lookup"><span data-stu-id="f869d-253">A collection is intrinsically elastic - it automatically grows and shrinks as you add or remove documents.</span></span> <span data-ttu-id="f869d-254">集合是邏輯資源，可以跨一或多個實體分割或伺服器。</span><span class="sxs-lookup"><span data-stu-id="f869d-254">Collections are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="f869d-255">集合中的分割數目是 Cosmos DB 根據集合的儲存體大小和佈建輸送量所決定。</span><span class="sxs-lookup"><span data-stu-id="f869d-255">The number of partitions within a collection is determined by Cosmos DB based on the storage size and the provisioned throughput of your collection.</span></span> <span data-ttu-id="f869d-256">Cosmos DB 中的每個分割都有其相關聯的固定 SSD 型式儲存體數量，並且複寫以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="f869d-256">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="f869d-257">資料分割管理完全透過 Azure Cosmos DB 來管理，您不需要撰寫複雜程式碼或管理資料分割。</span><span class="sxs-lookup"><span data-stu-id="f869d-257">Partition management is fully managed by Azure Cosmos DB, and you do not have to write complex code or manage your partitions.</span></span> <span data-ttu-id="f869d-258">從儲存體和輸送量的角度來看，Cosmos DB 集合「實際上並無限制」。</span><span class="sxs-lookup"><span data-stu-id="f869d-258">Cosmos DB collections are **practically unlimited** in terms of storage and throughput.</span></span> 

### <a name="automatic-indexing-of-collections"></a><span data-ttu-id="f869d-259">集合的自動編製索引</span><span class="sxs-lookup"><span data-stu-id="f869d-259">Automatic indexing of collections</span></span>
<span data-ttu-id="f869d-260">Cosmos DB 是真正不具結構描述的資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="f869d-260">Cosmos DB is a true schema-free database system.</span></span> <span data-ttu-id="f869d-261">它不會假設或不需要 JSON 文件的任何結構描述。</span><span class="sxs-lookup"><span data-stu-id="f869d-261">It does not assume or require any schema for the JSON documents.</span></span> <span data-ttu-id="f869d-262">將文件新增至集合時，Cosmos DB 會自動編製它們的索引，並且可供您進行查詢。</span><span class="sxs-lookup"><span data-stu-id="f869d-262">As you add documents to a collection, Cosmos DB automatically indexes them and they are available for you to query.</span></span> <span data-ttu-id="f869d-263">在不需要結構描述或次要索引的情況下自動編製文件索引是 Cosmos DB 的重要功能，並且會啟用以獲得寫入最佳化、無鎖定和記錄結構化索引維護技術。</span><span class="sxs-lookup"><span data-stu-id="f869d-263">Automatic indexing of documents without requiring schema or secondary indexes is a key capability of Cosmos DB and is enabled by write-optimized, lock-free and log-structured index maintenance techniques.</span></span> <span data-ttu-id="f869d-264">Cosmos DB 支援極快速持續寫入量，同時仍然提供一致的查詢。</span><span class="sxs-lookup"><span data-stu-id="f869d-264">Cosmos DB supports sustained volume of extremely fast writes while still serving consistent queries.</span></span> <span data-ttu-id="f869d-265">文件和索引儲存體都是用來計算每個集合所使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="f869d-265">Both document and index storage are used to calculate the storage consumed by each collection.</span></span> <span data-ttu-id="f869d-266">您可以設定集合的索引原則，以控制與索引相關聯的儲存體和效能取捨。</span><span class="sxs-lookup"><span data-stu-id="f869d-266">You can control the storage and performance trade-offs associated with indexing by configuring the indexing policy for a collection.</span></span> 

### <a name="configuring-the-indexing-policy-of-a-collection"></a><span data-ttu-id="f869d-267">設定集合的索引原則</span><span class="sxs-lookup"><span data-stu-id="f869d-267">Configuring the indexing policy of a collection</span></span>
<span data-ttu-id="f869d-268">每個集合的索引原則都可讓您進行與索引相關聯的效能和儲存體取捨。</span><span class="sxs-lookup"><span data-stu-id="f869d-268">The indexing policy of each collection allows you to make performance and storage trade-offs associated with indexing.</span></span> <span data-ttu-id="f869d-269">下列是可供您在進行索引組態時使用的選項：</span><span class="sxs-lookup"><span data-stu-id="f869d-269">The following options are available to you as part of indexing configuration:</span></span>  

* <span data-ttu-id="f869d-270">選擇集合是否自動編製所有文件的索引。</span><span class="sxs-lookup"><span data-stu-id="f869d-270">Choose whether the collection automatically indexes all of the documents or not.</span></span> <span data-ttu-id="f869d-271">預設會自動編製所有文件的索引。</span><span class="sxs-lookup"><span data-stu-id="f869d-271">By default, all documents are automatically indexed.</span></span> <span data-ttu-id="f869d-272">您可以選擇關閉自動編製索引，並選擇性地僅將特定文件新增至索引。</span><span class="sxs-lookup"><span data-stu-id="f869d-272">You can choose to turn off automatic indexing and selectively add only specific documents to the index.</span></span> <span data-ttu-id="f869d-273">相反地，您可以選擇性地選擇僅排除特定文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-273">Conversely, you can selectively choose to exclude only specific documents.</span></span> <span data-ttu-id="f869d-274">做法是在集合的 indexingPolicy 上將自動屬性設定為 true 或 false，以及在插入、取代或刪除文件時使用 [x-ms-indexingdirective] 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="f869d-274">You can achieve this by setting the automatic property to be true or false on the indexingPolicy of a collection and using the [x-ms-indexingdirective] request header while inserting, replacing or deleting a document.</span></span>  
* <span data-ttu-id="f869d-275">選擇在文件中包括還是排除索引中的特定路徑或模式。</span><span class="sxs-lookup"><span data-stu-id="f869d-275">Choose whether to include or exclude specific paths or patterns in your documents from the index.</span></span> <span data-ttu-id="f869d-276">做法是分別在集合的 indexingPolicy 上設定 includedPaths 和 excludedPaths。</span><span class="sxs-lookup"><span data-stu-id="f869d-276">You can achieve this by setting includedPaths and excludedPaths on the indexingPolicy of a collection respectively.</span></span> <span data-ttu-id="f869d-277">您也可以針對特定路徑模式的範圍和雜湊查詢，設定儲存體和效能取捨。</span><span class="sxs-lookup"><span data-stu-id="f869d-277">You can also configure the storage and performance trade-offs for range and hash queries for specific path patterns.</span></span> 
* <span data-ttu-id="f869d-278">選擇同步 (一致) 與非同步 (緩慢) 索引更新。</span><span class="sxs-lookup"><span data-stu-id="f869d-278">Choose between synchronous (consistent) and asynchronous (lazy) index updates.</span></span> <span data-ttu-id="f869d-279">每次在集合中插入、取代或刪除文件時，預設會同步更新索引。</span><span class="sxs-lookup"><span data-stu-id="f869d-279">By default, the index is updated synchronously on each insert, replace or delete of a document to the collection.</span></span> <span data-ttu-id="f869d-280">這個行為讓查詢能夠使用與文件的讀取相同的一致性層級。</span><span class="sxs-lookup"><span data-stu-id="f869d-280">This enables the queries to honor the same consistency level as that of the document reads.</span></span> <span data-ttu-id="f869d-281">雖然 Cosmos DB 的寫入已經過最佳化處理，並支援持續的文件寫入數量以及同步索引維護和提供一致的查詢，但是您還是可以設定特定集合，讓集合的索引更新速度變慢。</span><span class="sxs-lookup"><span data-stu-id="f869d-281">While Cosmos DB is write optimized and supports sustained volumes of document writes along with synchronous index maintenance and serving consistent queries, you can configure certain collections to update their index lazily.</span></span> <span data-ttu-id="f869d-282">緩慢索引會進一步地促進寫入效能，而且適合在主要進行大量讀取集合時大量擷取案例。</span><span class="sxs-lookup"><span data-stu-id="f869d-282">Lazy indexing boosts the write performance further and is ideal for bulk ingestion scenarios for primarily read-heavy collections.</span></span>

<span data-ttu-id="f869d-283">在集合上執行 PUT 即可變更索引原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-283">The indexing policy can be changed by executing a PUT on the collection.</span></span> <span data-ttu-id="f869d-284">不論是透過[用戶端 SDK](documentdb-sdk-dotnet.md)、[Azure 入口網站](https://portal.azure.com)還是 [REST API](/rest/api/documentdb/)，都可達到此目的。</span><span class="sxs-lookup"><span data-stu-id="f869d-284">This can be achieved either through the [client SDK](documentdb-sdk-dotnet.md), the [Azure Portal](https://portal.azure.com) or the [REST APIs](/rest/api/documentdb/).</span></span>

### <a name="querying-a-collection"></a><span data-ttu-id="f869d-285">查詢集合</span><span class="sxs-lookup"><span data-stu-id="f869d-285">Querying a collection</span></span>
<span data-ttu-id="f869d-286">集合內的文件可以有任意結構描述，而且您可以查詢集合內的文件，而不需要預先提供任何結構描述或次要索引。</span><span class="sxs-lookup"><span data-stu-id="f869d-286">The documents within a collection can have arbitrary schemas and you can query documents within a collection without providing any schema or secondary indices upfront.</span></span> <span data-ttu-id="f869d-287">您可以使用 [Azure Cosmos DB DocumentDB API：SQL 語法參考](https://msdn.microsoft.com/library/azure/dn782250.aspx)來查詢集合，這些語法透過 JavaScript 型 UDF 提供豐富階層式與關聯式的空間運算子及擴充性。</span><span class="sxs-lookup"><span data-stu-id="f869d-287">You can query the collection using the [Azure Cosmos DB DocumentDB API: SQL syntax reference](https://msdn.microsoft.com/library/azure/dn782250.aspx), which provides rich hierarchical, relational, and spatial operators and extensibility via JavaScript-based UDFs.</span></span> <span data-ttu-id="f869d-288">JSON 文法允許用於將 JSON 文件建模為標籤做為樹狀節點的樹狀目錄。</span><span class="sxs-lookup"><span data-stu-id="f869d-288">JSON grammar allows for modeling JSON documents as trees with labels as the tree nodes.</span></span> <span data-ttu-id="f869d-289">這會同時應用 DocumentDB API 的自動編製索引技術與 DocumentDB API 的 SQL 方言。</span><span class="sxs-lookup"><span data-stu-id="f869d-289">This is exploited both by DocumentDB API’s automatic indexing techniques as well as DocumentDB API's SQL dialect.</span></span> <span data-ttu-id="f869d-290">DocumentDB API 查詢語言包含三個主要部分：</span><span class="sxs-lookup"><span data-stu-id="f869d-290">The DocumetDB API query language consists of three main aspects:</span></span>   

1. <span data-ttu-id="f869d-291">本質上對應至樹狀結構的較小一組查詢作業 (包括階層式查詢和投射)。</span><span class="sxs-lookup"><span data-stu-id="f869d-291">A small set of query operations that map naturally to the tree structure including hierarchical queries and projections.</span></span> 
2. <span data-ttu-id="f869d-292">關聯式作業 (包括複合、篩選、投射、彙總和自我聯結) 的子集。</span><span class="sxs-lookup"><span data-stu-id="f869d-292">A subset of relational operations including composition, filter, projections, aggregates and self joins.</span></span> 
3. <span data-ttu-id="f869d-293">可與 (1) 和 (2) 搭配使用的純 JavaScript 型 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-293">Pure JavaScript based UDFs that work with (1) and (2).</span></span>  

<span data-ttu-id="f869d-294">Cosmos DB 查詢模型嘗試打破功能、效率和簡易性之間的平衡。</span><span class="sxs-lookup"><span data-stu-id="f869d-294">The Cosmos DB query model attempts to strike a balance between functionality, efficiency and simplicity.</span></span> <span data-ttu-id="f869d-295">Cosmos DB 資料庫引擎會原生編譯和執行 SQL 查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="f869d-295">The Cosmos DB database engine natively compiles and executes the SQL query statements.</span></span> <span data-ttu-id="f869d-296">您可以使用 [REST API](/rest/api/documentdb/) 或任何[用戶端 SDK](documentdb-sdk-dotnet.md) 來查詢集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-296">You can query a collection using the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="f869d-297">.NET SDK 隨附於 LINQ 提供者。</span><span class="sxs-lookup"><span data-stu-id="f869d-297">The .NET SDK comes with a LINQ provider.</span></span>

> [!TIP]
> <span data-ttu-id="f869d-298">您可以試試 DocumentDB API，並在[查詢園地](https://www.documentdb.com/sql/demo) (英文) 中針對我們的資料集執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="f869d-298">You can try out the DocumentDB API and run SQL queries against our dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
> 
> 

## <a name="multi-document-transactions"></a><span data-ttu-id="f869d-299">多文件交易</span><span class="sxs-lookup"><span data-stu-id="f869d-299">Multi-document transactions</span></span>
<span data-ttu-id="f869d-300">資料庫交易提供安全且可預測的程式設計模型來處理同時的資料變更。</span><span class="sxs-lookup"><span data-stu-id="f869d-300">Database transactions provide a safe and predictable programming model for dealing with concurrent changes to the data.</span></span> <span data-ttu-id="f869d-301">在 RDBMS 中，撰寫商務邏輯的傳統方式是撰寫「預存程序」和/或「觸發程序」，並將它傳送至資料庫伺服器以進行交易式執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-301">In RDBMS, the traditional way to write business logic is to write **stored-procedures** and/or **triggers** and ship it to the database server for transactional execution.</span></span> <span data-ttu-id="f869d-302">在 RDBMS 中，需要有應用程式設計人員，才能處理兩個不同的程式設計語言：</span><span class="sxs-lookup"><span data-stu-id="f869d-302">In RDBMS, the application programmer is required to deal with two disparate programming languages:</span></span> 

* <span data-ttu-id="f869d-303">(非交易式) 應用程式程式設計語言 (例如 JavaScript、Python、C#、Java 等等)</span><span class="sxs-lookup"><span data-stu-id="f869d-303">The (non-transactional) application programming language (e.g. JavaScript, Python, C#, Java, etc.)</span></span>
* <span data-ttu-id="f869d-304">T-SQL 是交易式程式設計語言，專門由資料庫執行</span><span class="sxs-lookup"><span data-stu-id="f869d-304">T-SQL, the transactional programming language which is natively executed by the database</span></span>

<span data-ttu-id="f869d-305">透過直接在資料庫引擎內深入承諾 JavaScript 和 JSON，Cosmos DB 提供直覺式程式設計模型，以透過預存程序和觸發程序直接在集合上執行 JavaScript 型應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="f869d-305">By virtue of its deep commitment to JavaScript and JSON directly within the database engine, Cosmos DB provides an intuitive programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="f869d-306">這會允許下列兩項動作：</span><span class="sxs-lookup"><span data-stu-id="f869d-306">This allows for both of the following:</span></span>

* <span data-ttu-id="f869d-307">直接在資料庫引擎中，有效率地實作 JSON 物件圖形的並行存取控制、復原、自動編製索引</span><span class="sxs-lookup"><span data-stu-id="f869d-307">Efficient implementation of concurrency control, recovery, automatic indexing of the JSON object graphs directly in the database engine</span></span>
* <span data-ttu-id="f869d-308">在 JavaScript 程式設計語言方面，直接自然表達資料庫交易的控制流程、變數範圍、指派和整合例外狀況處理基本項目</span><span class="sxs-lookup"><span data-stu-id="f869d-308">Naturally expressing control flow, variable scoping, assignment and integration of exception handling primitives with database transactions directly in terms of the JavaScript programming language</span></span>

<span data-ttu-id="f869d-309">在集合層級註冊的 JavaScript 邏輯接著可以對給定集合的文件發出資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="f869d-309">The JavaScript logic registered at a collection level can then issue database operations on the documents of the given collection.</span></span> <span data-ttu-id="f869d-310">Cosmos DB 可以跨集合內的文件，隱含地在具有快照隔離的環境 ACID 交易內包裝 JavaScript 型預存程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-310">Cosmos DB implicitly wraps the JavaScript based stored procedures and triggers within an ambient ACID transactions with snapshot isolation across documents within a collection.</span></span> <span data-ttu-id="f869d-311">在執行期間，如果 JavaScript 擲回例外狀況，則會中止整個交易。</span><span class="sxs-lookup"><span data-stu-id="f869d-311">During the course of its execution, if the JavaScript throws an exception, then the entire transaction is aborted.</span></span> <span data-ttu-id="f869d-312">產生的程式設計模型極為簡單，但功能強大。</span><span class="sxs-lookup"><span data-stu-id="f869d-312">The resulting programming model is a very simple yet powerful.</span></span> <span data-ttu-id="f869d-313">JavaScript 開發人員會取得「持續性」程式設計模型，同時仍然使用其熟悉的語言建構和程式庫基本。</span><span class="sxs-lookup"><span data-stu-id="f869d-313">JavaScript developers get a “durable” programming model while still using their familiar language constructs and library primitives.</span></span>   

<span data-ttu-id="f869d-314">直接在資料庫引擎 (與緩衝集區位於相同的位址空間) 內執行 JavaScript 的能力，可對集合的文件啟用資料庫作業的具效能和交易式執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-314">The ability to execute JavaScript directly within the database engine in the same address space as the buffer pool enables performant and transactional execution of database operations against the documents of a collection.</span></span> <span data-ttu-id="f869d-315">此外，Cosmos DB 資料庫引擎會進一步對 JSON 和 JavaScript 執行認可，以去除應用程式與資料庫之的類型系統間的阻抗不相符。</span><span class="sxs-lookup"><span data-stu-id="f869d-315">Furthermore, Cosmos DB database engine makes a deep commitment to the JSON and JavaScript eliminates any impedance mismatch between the type systems of application and the database.</span></span>   

<span data-ttu-id="f869d-316">建立集合之後，您即可使用 [REST API](/rest/api/documentdb/) 或任何[用戶端 SDK](documentdb-sdk-dotnet.md)，向集合註冊預存程序、觸發程序及 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-316">After creating a collection, you can register stored procedures, triggers and UDFs with a collection using the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="f869d-317">註冊之後，您就可以參考和執行它們。</span><span class="sxs-lookup"><span data-stu-id="f869d-317">After registration, you can reference and execute them.</span></span> <span data-ttu-id="f869d-318">您可以考慮使用下列完全以 JavaScript 撰寫的預存程序。下列程式碼採用兩個引數 (書籍名稱和作者名稱) 建立新文件，接著再查詢文件，然後加以更新。這些作業全都會在隱含的 ACID 交易中進行。</span><span class="sxs-lookup"><span data-stu-id="f869d-318">Consider the following stored procedure written entirely in JavaScript, the code below takes two arguments (book name and author name) and creates a new document, queries for a document and then updates it – all within an implicit ACID transaction.</span></span> <span data-ttu-id="f869d-319">在執行期間的任何時間點，如果擲回 JavaScript 例外狀況，整個交易便會中止。</span><span class="sxs-lookup"><span data-stu-id="f869d-319">At any point during the execution, if a JavaScript exception is thrown, the entire transaction aborts.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

<span data-ttu-id="f869d-320">用戶端可以將上面的 JavaScript 邏輯「傳送」至資料庫，以透過 HTTP POST 進行交易式執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-320">The client can “ship” the above JavaScript logic to the database for transactional execution via HTTP POST.</span></span> <span data-ttu-id="f869d-321">如需關於使用 HTTP 方法的詳細資訊，請參閱[與 Azure Cosmos DB 資源進行 RESTful 互動 (英文)](https://msdn.microsoft.com/library/azure/mt622086.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f869d-321">For more information about using HTTP methods, see [RESTful interactions with Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx).</span></span> 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


<span data-ttu-id="f869d-322">請注意，因為資料庫原本就了解 JSON 和 JavaScript，所以不會有類型系統不符、沒有「OR 對應」或不需要程式碼產生魔術。</span><span class="sxs-lookup"><span data-stu-id="f869d-322">Notice that because the database natively understands JSON and JavaScript, there is no type system mismatch, no “OR mapping” or code generation magic required.</span></span>   

<span data-ttu-id="f869d-323">預存程序和觸發程序會透過定義良好的物件模型 (可公開目前集合內容)，與集合及集合內的文件互動。</span><span class="sxs-lookup"><span data-stu-id="f869d-323">Stored procedures and triggers interact with a collection and the documents in a collection through a well-defined object model, which exposes the current collection context.</span></span>  

<span data-ttu-id="f869d-324">不論是使用 [REST API](/rest/api/documentdb/) 還是任何[用戶端 SDK](documentdb-sdk-dotnet.md)，都可輕鬆地建立、刪除、讀取或列舉 DocumentDB API 中的集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-324">Collections in the DocumentDB API can be created, deleted, read or enumerated easily using either the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="f869d-325">DocumentDB API 一律提供讀取或查詢集合中繼資料的強式一致性。</span><span class="sxs-lookup"><span data-stu-id="f869d-325">The DocumentDB API always provides strong consistency for reading or querying the metadata of a collection.</span></span> <span data-ttu-id="f869d-326">刪除集合會自動確定您無法存取其內所含的任何文件、附件、預存程序、觸發程序和 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-326">Deleting a collection automatically ensures that you cannot access any of the documents, attachments, stored procedures, triggers, and UDFs contained within it.</span></span>   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a><span data-ttu-id="f869d-327">預存程序、觸發程序和使用者定義函數 (UDF)</span><span class="sxs-lookup"><span data-stu-id="f869d-327">Stored procedures, triggers and User Defined Functions (UDF)</span></span>
<span data-ttu-id="f869d-328">如上一節所述，您可以撰寫直接在資料庫引擎的交易內執行的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="f869d-328">As described in the previous section, you can write application logic to run directly within a transaction inside of the database engine.</span></span> <span data-ttu-id="f869d-329">應用程式邏輯可以完全以 JavaScript 撰寫，也可以建模為預存程序、觸發程序或 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-329">The application logic can be written entirely in JavaScript and can be modeled as a stored procedure, trigger or a UDF.</span></span> <span data-ttu-id="f869d-330">預存程序或觸發程序內的 JavaScript 程式碼可以在集合內插入、取代、刪除、讀取或查詢文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-330">The JavaScript code within a stored procedure or a trigger can insert, replace, delete, read or query documents within a collection.</span></span> <span data-ttu-id="f869d-331">另一方面，UDF 內的 JavaScript 無法插入、取代或刪除文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-331">On the other hand, the JavaScript within a UDF cannot insert, replace, or delete documents.</span></span> <span data-ttu-id="f869d-332">UDF 會列舉查詢結果集的文件並產生另一個結果集。</span><span class="sxs-lookup"><span data-stu-id="f869d-332">UDFs enumerate the documents of a query's result set and produce another result set.</span></span> <span data-ttu-id="f869d-333">若是多重租用，Cosmos DB 會強制執行嚴謹的保留型資源管理。</span><span class="sxs-lookup"><span data-stu-id="f869d-333">For multi-tenancy, Cosmos DB enforces a strict reservation based resource governance.</span></span> <span data-ttu-id="f869d-334">每個預存程序、觸發程序或 UDF 都會取得固定配量的作業系統資源來執行工作。</span><span class="sxs-lookup"><span data-stu-id="f869d-334">Each stored procedure, trigger or a UDF gets a fixed quantum of operating system resources to do its work.</span></span> <span data-ttu-id="f869d-335">此外，預存程序、觸發程序或 UDF 無法連結外部 JavaScript 程式庫，因此，當這些項目超出配置的資源預算時，便會將其列入封鎖清單。</span><span class="sxs-lookup"><span data-stu-id="f869d-335">Furthermore, stored procedures, triggers or UDFs cannot link against external JavaScript libraries and are blacklisted if they exceed the resource budgets allocated to them.</span></span> <span data-ttu-id="f869d-336">您可以使用 REST API 向集合註冊、取消註冊預存程序、觸發程序或 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-336">You can register, unregister stored procedures, triggers or UDFs with a collection by using the REST APIs.</span></span>  <span data-ttu-id="f869d-337">註冊時，預存程序、觸發程序或 UDF 會預先編譯並儲存為位元組程式碼，以在稍後執行。</span><span class="sxs-lookup"><span data-stu-id="f869d-337">Upon registration a stored procedure, trigger, or a UDF is pre-compiled and stored as byte code which gets executed later.</span></span> <span data-ttu-id="f869d-338">下節說明如何使用 Cosmos DB JavaScript SDK 來註冊、執行和取消註冊預存程序、觸發程序和 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-338">The following section illustrate how you can use the Cosmos DB JavaScript SDK to register, execute, and unregister a stored procedure, trigger, and a UDF.</span></span> <span data-ttu-id="f869d-339">JavaScript SDK 是一種透過 [REST API](/rest/api/documentdb/) 的簡單包裝函式。</span><span class="sxs-lookup"><span data-stu-id="f869d-339">The JavaScript SDK is a simple wrapper over the [REST APIs](/rest/api/documentdb/).</span></span> 

### <a name="registering-a-stored-procedure"></a><span data-ttu-id="f869d-340">註冊預存程序</span><span class="sxs-lookup"><span data-stu-id="f869d-340">Registering a stored procedure</span></span>
<span data-ttu-id="f869d-341">透過 HTTP POST 在集合上建立新的預存程序資源，即可註冊預存程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-341">Registration of a stored procedure creates a new stored procedure resource on a collection via HTTP POST.</span></span>  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a><span data-ttu-id="f869d-342">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="f869d-342">Executing a stored procedure</span></span>
<span data-ttu-id="f869d-343">透過將參數傳遞給要求本文中的程序，以對現有預存程序資源發出 HTTP POST，即可執行預存程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-343">Execution of a stored procedure is done by issuing an HTTP POST against an existing stored procedure resource by passing parameters to the procedure in the request body.</span></span>

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a><span data-ttu-id="f869d-344">取消註冊預存程序</span><span class="sxs-lookup"><span data-stu-id="f869d-344">Unregistering a stored procedure</span></span>
<span data-ttu-id="f869d-345">只要對現有預存程序資源發出 HTTP DELETE，即可取消註冊預存程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-345">Unregistering a stored procedure is simply done by issuing an HTTP DELETE against an existing stored procedure resource.</span></span>   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a><span data-ttu-id="f869d-346">註冊預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="f869d-346">Registering a pre-trigger</span></span>
<span data-ttu-id="f869d-347">透過 HTTP POST 在集合上建立新的觸發程序資源，即可註冊觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-347">Registration of a trigger is done by creating a new trigger resource on a collection via HTTP POST.</span></span> <span data-ttu-id="f869d-348">您可以指定觸發程序是預先觸發程序還是後續觸發程序，以及可與之相關聯的作業類型 (例如，[建立]、[取代]、[刪除] 或 [全部])。</span><span class="sxs-lookup"><span data-stu-id="f869d-348">You can specify if the trigger is a pre or a post trigger and the type of operation it can be associated with (e.g. Create, Replace, Delete, or All).</span></span>   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a><span data-ttu-id="f869d-349">執行預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="f869d-349">Executing a pre-trigger</span></span>
<span data-ttu-id="f869d-350">透過要求標頭發出文件資源的 POST/PUT/DELETE 要求時指定現有觸發程序名稱，即可執行觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-350">Execution of a trigger is done by specifying the name of an existing trigger at the time of issuing the POST/PUT/DELETE request of a document resource via the request header.</span></span>  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in the Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a><span data-ttu-id="f869d-351">取消註冊預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="f869d-351">Unregistering a pre-trigger</span></span>
<span data-ttu-id="f869d-352">只要對現有觸發程序資源發出 HTTP DELETE，即可取消註冊觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f869d-352">Unregistering a trigger is simply done via issuing an HTTP DELETE against an existing trigger resource.</span></span>  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a><span data-ttu-id="f869d-353">註冊 UDF</span><span class="sxs-lookup"><span data-stu-id="f869d-353">Registering a UDF</span></span>
<span data-ttu-id="f869d-354">透過 HTTP POST 在集合上建立新的 UDF 資源，即可註冊 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-354">Registration of a UDF is done by creating a new UDF resource on a collection via HTTP POST.</span></span>  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-the-query"></a><span data-ttu-id="f869d-355">將 UDF 執行為查詢的一部分</span><span class="sxs-lookup"><span data-stu-id="f869d-355">Executing a UDF as part of the query</span></span>
<span data-ttu-id="f869d-356">UDF 可以指定為部分 SQL 查詢，也可做為一種擴充 [DocumentDB API 核心 SQL 查詢語言](https://msdn.microsoft.com/library/azure/dn782250.aspx) (英文) 的方法。</span><span class="sxs-lookup"><span data-stu-id="f869d-356">A UDF can be specified as part of the SQL query and is used as a way to extend the core [SQL query language for the DocumentDB API](https://msdn.microsoft.com/library/azure/dn782250.aspx).</span></span>

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a><span data-ttu-id="f869d-357">取消註冊 UDF</span><span class="sxs-lookup"><span data-stu-id="f869d-357">Unregistering a UDF</span></span>
<span data-ttu-id="f869d-358">只要對現有 UDF 資源發出 HTTP DELETE，即可取消註冊 UDF。</span><span class="sxs-lookup"><span data-stu-id="f869d-358">Unregistering a UDF is simply done by issuing an HTTP DELETE against an existing UDF resource.</span></span>  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

<span data-ttu-id="f869d-359">雖然以上程式碼片段顯示的是透過 [JavaScript SDK](https://github.com/Azure/azure-documentdb-js) 執行的註冊 (POST)、取消註冊 (PUT)、讀取/列出 (GET) 及執行 (POST)，但您也可以使用 [REST API](/rest/api/documentdb/) 或其他[用戶端 SDK](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f869d-359">Although the snippets above showed the registration (POST), unregistration (PUT), read/list (GET) and execution (POST) via the [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), you can also use the [REST APIs](/rest/api/documentdb/) or other [client SDKs](documentdb-sdk-dotnet.md).</span></span> 

## <a name="documents"></a><span data-ttu-id="f869d-360">文件</span><span class="sxs-lookup"><span data-stu-id="f869d-360">Documents</span></span>
<span data-ttu-id="f869d-361">您可以在集合中插入、取代、刪除、讀取、列舉和查詢任意 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-361">You can insert, replace, delete, read, enumerate and query arbitrary JSON documents in a collection.</span></span> <span data-ttu-id="f869d-362">Cosmos DB 不會託管任何結構描述，而且不需要次要索引，就支援逐一查詢集合中的文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-362">Cosmos DB does not mandate any schema and does not require secondary indexes in order to support querying over documents in a collection.</span></span> <span data-ttu-id="f869d-363">文件的大小上限為 2 MB。</span><span class="sxs-lookup"><span data-stu-id="f869d-363">The maximum size for a document is 2 MB.</span></span>   

<span data-ttu-id="f869d-364">Cosmos DB 是真正開放的資料庫服務，不會發明 JSON 文件的任何特殊資料類型 (例如日期時間) 或特定編碼。</span><span class="sxs-lookup"><span data-stu-id="f869d-364">Being a truly open database service, Cosmos DB does not invent any specialized data types (e.g. date time) or specific encodings for JSON documents.</span></span> <span data-ttu-id="f869d-365">請注意，Cosmos DB 無須遵循任何特殊 JSON 慣例，即可編寫各種文件之間的關聯性。Cosmos DB 的 SQL 語法提供有效率的階層式和關係查詢運算子，讓您可以用於查詢及保護文件，不僅無須任何特殊註釋，也無須使用不同的屬性來編寫文件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f869d-365">Note that Cosmos DB does not require any special JSON conventions to codify the relationships among various documents; the SQL syntax of Cosmos DB provides very powerful hierarchical and relational query operators to query and project documents without any special annotations or need to codify relationships among documents using distinguished properties.</span></span>  

<span data-ttu-id="f869d-366">與所有其他資源相同，使用 REST API 或任何 [用戶端 SDK](documentdb-sdk-dotnet.md)，即可輕鬆地建立、取代、刪除、讀取、列舉或查詢文件。</span><span class="sxs-lookup"><span data-stu-id="f869d-366">As with all other resources, documents can be created, replaced, deleted, read, enumerated and queried easily using either REST APIs or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="f869d-367">刪除文件時會立即清出對應至所有巢狀附件的配額。</span><span class="sxs-lookup"><span data-stu-id="f869d-367">Deleting a document instantly frees up the quota corresponding to all of the nested attachments.</span></span> <span data-ttu-id="f869d-368">文件的讀取一致性層級會遵循資料庫帳戶的一致性原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-368">The read consistency level of documents follows the consistency policy on the database account.</span></span> <span data-ttu-id="f869d-369">根據您應用程式的資料一致性需求，可以覆寫每個要求的這個原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-369">This policy can be overridden on a per-request basis depending on data consistency requirements of your application.</span></span> <span data-ttu-id="f869d-370">查詢文件時，讀取一致性會遵循集合上所設定的索引模式。</span><span class="sxs-lookup"><span data-stu-id="f869d-370">When querying documents, the read consistency follows the indexing mode set on the collection.</span></span> <span data-ttu-id="f869d-371">為求「一致」，這會遵循帳戶的一致性原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-371">For “consistent”, this follows the account’s consistency policy.</span></span> 

## <a name="attachments-and-media"></a><span data-ttu-id="f869d-372">附件和媒體</span><span class="sxs-lookup"><span data-stu-id="f869d-372">Attachments and media</span></span>
<span data-ttu-id="f869d-373">Cosmos DB 可讓您將二進位 Blob/媒體儲存至 Cosmos DB (每個帳戶最多 2 GB) 或您自己的遠端媒體存放區。</span><span class="sxs-lookup"><span data-stu-id="f869d-373">Cosmos DB allows you to store binary blobs/media either with Cosmos DB (maximum of 2 GB per account) or to your own remote media store.</span></span> <span data-ttu-id="f869d-374">它也可讓您透過特殊文件 (稱為附件) 來呈現媒體的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f869d-374">It also allows you to represent the metadata of a media in terms of a special document called attachment.</span></span> <span data-ttu-id="f869d-375">Cosmos DB 中的附件是一種特殊 (JSON) 文件，可參考儲存在其他位置的媒體/Blob。</span><span class="sxs-lookup"><span data-stu-id="f869d-375">An attachment in Cosmos DB is a special (JSON) document that references the media/blob stored elsewhere.</span></span> <span data-ttu-id="f869d-376">附件只是特殊文件，可擷取遠端媒體存放裝置中所儲存媒體的中繼資料 (例如位置、作者等)。</span><span class="sxs-lookup"><span data-stu-id="f869d-376">An attachment is simply a special document that captures the metadata (e.g. location, author etc.) of a media stored in a remote media storage.</span></span> 

<span data-ttu-id="f869d-377">請考慮使用社交閱讀應用程式，它會使用 Cosmos DB 儲存手寫註釋，以及與指定使用者電子書相關聯的中繼資料 (包括註解、醒目提示、書籤、評等、喜歡/不喜歡等)。</span><span class="sxs-lookup"><span data-stu-id="f869d-377">Consider a social reading application which uses Cosmos DB to store ink annotations, and metadata including comments, highlights, bookmarks, ratings, likes/dislikes etc. associated for an e-book of a given user.</span></span>   

* <span data-ttu-id="f869d-378">書籍本身的內容儲存在媒體存放裝置 (做為 Cosmos DB 資料庫帳戶的一部分) 或遠端媒體存放區中。</span><span class="sxs-lookup"><span data-stu-id="f869d-378">The content of the book itself is stored in the media storage either available as part of Cosmos DB database account or a remote media store.</span></span> 
* <span data-ttu-id="f869d-379">應用程式可能會將每個使用者的中繼資料儲存為不同的文件 (例如 Joe 的 book1 中繼資料儲存在 /colls/joe/docs/book1 所參考的文件中)。</span><span class="sxs-lookup"><span data-stu-id="f869d-379">An application may store each user’s metadata as a distinct document -- e.g. Joe’s metadata for book1 is stored in a document referenced by /colls/joe/docs/book1.</span></span> 
* <span data-ttu-id="f869d-380">指向使用者給定書籍之內容頁面的附件，儲存在對應的文件中 (例如 /colls/joe/docs/book1/chapter1、/colls/joe/docs/book1/chapter2 等)。</span><span class="sxs-lookup"><span data-stu-id="f869d-380">Attachments pointing to the content pages of a given book of a user are stored under the corresponding document e.g. /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 etc.</span></span> 

<span data-ttu-id="f869d-381">請注意，上述範例會使用易記 ID 來傳達資源階層。</span><span class="sxs-lookup"><span data-stu-id="f869d-381">Note that the examples listed above use friendly ids to convey the resource hierarchy.</span></span> <span data-ttu-id="f869d-382">資源是透過 REST API 以根據唯一資源 ID 進行存取。</span><span class="sxs-lookup"><span data-stu-id="f869d-382">Resources are accessed via the REST APIs through unique resource ids.</span></span> 

<span data-ttu-id="f869d-383">針對 Cosmos DB 所管理的媒體，附件的 _media 屬性將會依媒體的 URI 來參考媒體。</span><span class="sxs-lookup"><span data-stu-id="f869d-383">For the media that is managed by Cosmos DB, the _media property of the attachment will reference the media by its URI.</span></span> <span data-ttu-id="f869d-384">Cosmos DB 將會在捨棄所有未完成的參考時，確保回收媒體的記憶體。</span><span class="sxs-lookup"><span data-stu-id="f869d-384">Cosmos DB will ensure to garbage collect the media when all of the outstanding references are dropped.</span></span> <span data-ttu-id="f869d-385">如果您上傳新的媒體並填入 _media 以指向新增的媒體，則 Cosmos DB 會自動產生附件。</span><span class="sxs-lookup"><span data-stu-id="f869d-385">Cosmos DB automatically generates the attachment when you upload the new media and populates the _media to point to the newly added media.</span></span> <span data-ttu-id="f869d-386">如果您選擇將媒體儲存在您所管理的遠端 Blob 存放區中 (例如 OneDrive、Azure Storage、DropBox 等)，則還是可以使用附件來參考媒體。</span><span class="sxs-lookup"><span data-stu-id="f869d-386">If you choose to store the media in a remote blob store managed by you (e.g. OneDrive, Azure Storage, DropBox etc), you can still use attachments to reference the media.</span></span> <span data-ttu-id="f869d-387">在此情況下，您將自行建立附件，並填入其 _media 屬性中。</span><span class="sxs-lookup"><span data-stu-id="f869d-387">In this case, you will create the attachment yourself and populate its _media property.</span></span>   

<span data-ttu-id="f869d-388">與所有其他資源相同，使用 REST API 或任何用戶端 SDK，即可輕鬆地建立、取代、刪除、讀取或列舉附件。</span><span class="sxs-lookup"><span data-stu-id="f869d-388">As with all other resources, attachments can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of the client SDKs.</span></span> <span data-ttu-id="f869d-389">與文件相同，附件的讀取一致性層級會遵循資料庫帳戶的一致性原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-389">As with documents, the read consistency level of attachments follows the consistency policy on the database account.</span></span> <span data-ttu-id="f869d-390">根據您應用程式的資料一致性需求，可以覆寫每個要求的這個原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-390">This policy can be overridden on a per-request basis depending on data consistency requirements of your application.</span></span> <span data-ttu-id="f869d-391">查詢附件時，讀取一致性會遵循集合上所設定的索引模式。</span><span class="sxs-lookup"><span data-stu-id="f869d-391">When querying for attachments, the read consistency follows the indexing mode set on the collection.</span></span> <span data-ttu-id="f869d-392">為求「一致」，這會遵循帳戶的一致性原則。</span><span class="sxs-lookup"><span data-stu-id="f869d-392">For “consistent”, this follows the account’s consistency policy.</span></span> 
 

## <a name="users"></a><span data-ttu-id="f869d-393">使用者</span><span class="sxs-lookup"><span data-stu-id="f869d-393">Users</span></span>
<span data-ttu-id="f869d-394">Cosmos DB 使用者代表用於分組權限的邏輯命名空間。</span><span class="sxs-lookup"><span data-stu-id="f869d-394">A Cosmos DB user represents a logical namespace for grouping permissions.</span></span> <span data-ttu-id="f869d-395">Cosmos DB 使用者可能對應至身分識別管理系統或預先定義應用程式角色中的使用者。</span><span class="sxs-lookup"><span data-stu-id="f869d-395">A Cosmos DB user may correspond to a user in an identity management system or a predefined application role.</span></span> <span data-ttu-id="f869d-396">對於 Cosmos DB，使用者只代表將資料庫下的一組權限分組的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="f869d-396">For Cosmos DB, a user simply represents an abstraction to group a set of permissions under a database.</span></span>   

<span data-ttu-id="f869d-397">如需在您的應用程式中實作多重租用，您可以在 Cosmos DB 中建立對應至實際使用者或應用程式租用戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="f869d-397">For implementing multi-tenancy in your application, you can create users in Cosmos DB which corresponds to your actual users or the tenants of your application.</span></span> <span data-ttu-id="f869d-398">您接著可以建立給定使用者的權限，而權限透過各種集合、文件、附件等對應至存取控制。</span><span class="sxs-lookup"><span data-stu-id="f869d-398">You can then create permissions for a given user that correspond to the access control over various collections, documents, attachments, etc.</span></span>   

<span data-ttu-id="f869d-399">應用程式需要隨著使用者成長而調整時，您可以採用各種方式來共用資料。</span><span class="sxs-lookup"><span data-stu-id="f869d-399">As your applications need to scale with your user growth, you can adopt various ways to shard your data.</span></span> <span data-ttu-id="f869d-400">您可以建立每位使用者的模型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f869d-400">You can model each of your users as follows:</span></span>   

* <span data-ttu-id="f869d-401">每個使用者都對應至資料庫。</span><span class="sxs-lookup"><span data-stu-id="f869d-401">Each user maps to a database.</span></span>
* <span data-ttu-id="f869d-402">每個使用者都對應至集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-402">Each user maps to a collection.</span></span> 
* <span data-ttu-id="f869d-403">將對應至多位使用者的文件移至專用的集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-403">Documents corresponding to multiple users go to a dedicated collection.</span></span> 
* <span data-ttu-id="f869d-404">將對應至多位使用者的文件移至一組的集合。</span><span class="sxs-lookup"><span data-stu-id="f869d-404">Documents corresponding to multiple users go to a set of collections.</span></span>   

<span data-ttu-id="f869d-405">不論您選擇的特定分區化策略為何，您可以將實際使用者模型化為 Cosmos DB 資料庫中的使用者，並將微調後的權限關聯至每個使用者。</span><span class="sxs-lookup"><span data-stu-id="f869d-405">Regardless of the specific sharding strategy you choose, you can model your actual users as users in Cosmos DB database and associate fine grained permissions to each user.</span></span>  

<span data-ttu-id="f869d-406">![使用者集合][3]</span><span class="sxs-lookup"><span data-stu-id="f869d-406">![User collections][3]</span></span>  
<span data-ttu-id="f869d-407">**分區化策略和模型化使用者**</span><span class="sxs-lookup"><span data-stu-id="f869d-407">**Sharding strategies and modeling users**</span></span>

<span data-ttu-id="f869d-408">與所有其他資源相同，使用 REST API 或任何用戶端 SDK，即可輕鬆地在 Cosmos DB 中建立、取代、刪除、讀取或列舉使用者。</span><span class="sxs-lookup"><span data-stu-id="f869d-408">Like all other resources, users in Cosmos DB can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of the client SDKs.</span></span> <span data-ttu-id="f869d-409">Cosmos DB 一律提供讀取或查詢使用者資源之中繼資料的強式一致性。</span><span class="sxs-lookup"><span data-stu-id="f869d-409">Cosmos DB always provides strong consistency for reading or querying the metadata of a user resource.</span></span> <span data-ttu-id="f869d-410">這值得指出刪除使用者時會自動確保您無法存取其內所含的任何權限。</span><span class="sxs-lookup"><span data-stu-id="f869d-410">It is worth pointing out that deleting a user automatically ensures that you cannot access any of the permissions contained within it.</span></span> <span data-ttu-id="f869d-411">即使 Cosmos DB 在背景回收佈建為所刪除使用者一部分的權限配額，但是所刪除權限還是立即可以再度使用。</span><span class="sxs-lookup"><span data-stu-id="f869d-411">Even though the Cosmos DB reclaims the quota of the permissions as part of the deleted user in the background, the deleted permissions is available instantly again for you to use.</span></span>  

## <a name="permissions"></a><span data-ttu-id="f869d-412">權限</span><span class="sxs-lookup"><span data-stu-id="f869d-412">Permissions</span></span>
<span data-ttu-id="f869d-413">從存取控制觀點來看，系統會將資源 (例如資料庫帳戶、資料庫、使用者和權限) 視為「管理」  資源，因為這些都需要管理權限。</span><span class="sxs-lookup"><span data-stu-id="f869d-413">From an access control perspective, resources such as database accounts, databases, users and permission are considered *administrative* resources since these require administrative permissions.</span></span> <span data-ttu-id="f869d-414">另一方面，會將資源 (包括集合、文件、附件、預存程序、觸發程序和 UDF) 限制至給定資料庫，並將其視為「應用程式資源」 。</span><span class="sxs-lookup"><span data-stu-id="f869d-414">On the other hand, resources including the collections, documents, attachments, stored procedures, triggers, and UDFs are scoped under a given database and considered *application resources*.</span></span> <span data-ttu-id="f869d-415">授權模型定義兩種「存取金鑰」來對應兩種資源及可存取這些資源的角色 (即系統管理員和使用者)：「主要金鑰」和「資源金鑰」。</span><span class="sxs-lookup"><span data-stu-id="f869d-415">Corresponding to the two types of resources and the roles that access them (namely the administrator and user), the authorization model defines two types of *access keys*: *master key* and *resource key*.</span></span> <span data-ttu-id="f869d-416">主要金鑰是資料庫帳戶的一部分，並且提供給將佈建資料庫帳戶的開發人員 (或系統管理員)。</span><span class="sxs-lookup"><span data-stu-id="f869d-416">The master key is a part of the database account and is provided to the developer (or administrator) who is provisioning the database account.</span></span> <span data-ttu-id="f869d-417">此主要金鑰具有系統管理員語意，即它可以用來授權對管理和應用程式資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="f869d-417">This master key has administrator semantics, in that it can be used to authorize access to both administrative and application resources.</span></span> <span data-ttu-id="f869d-418">相較之下，資源金鑰是精細的存取金鑰，可允許存取「特定」  應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="f869d-418">In contrast, a resource key is a granular access key that allows access to a *specific* application resource.</span></span> <span data-ttu-id="f869d-419">因此，它會擷取資料庫使用者與使用者具有特定資源 (例如，集合、文件、附件、預存程序、觸發程序或 UDF) 的權限之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f869d-419">Thus, it captures the relationship between the user of a database and the permissions the user has for a specific resource (e.g. collection, document, attachment, stored procedure, trigger, or UDF).</span></span>   

<span data-ttu-id="f869d-420">取得資源金鑰的唯一方式是透過建立給定使用者的權限資源。</span><span class="sxs-lookup"><span data-stu-id="f869d-420">The only way to obtain a resource key is by creating a permission resource under a given user.</span></span> <span data-ttu-id="f869d-421">請注意，若要建立或擷取權限，授權標頭中必須要有主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="f869d-421">Note that In order to create or retrieve a permission, a master key must be presented in the authorization header.</span></span> <span data-ttu-id="f869d-422">權限資源會繫結資源、其存取權和使用者。</span><span class="sxs-lookup"><span data-stu-id="f869d-422">A permission resource ties the resource, its access and the user.</span></span> <span data-ttu-id="f869d-423">建立權限資源之後，使用者只需要具有相關聯的資源金鑰，就能存取相關資源。</span><span class="sxs-lookup"><span data-stu-id="f869d-423">After creating a permission resource, the user only needs to present the associated resource key in order to gain access to the relevant resource.</span></span> <span data-ttu-id="f869d-424">因此，可能會以權限資源的邏輯和壓縮呈現來檢視資源金鑰。</span><span class="sxs-lookup"><span data-stu-id="f869d-424">Hence, a resource key can be viewed as a logical and compact representation of the permission resource.</span></span>  

<span data-ttu-id="f869d-425">與所有其他資源相同，使用 REST API 或任何用戶端 SDK，即可輕鬆地在 Cosmos DB 中建立、取代、刪除、讀取或列舉權限。</span><span class="sxs-lookup"><span data-stu-id="f869d-425">As with all other resources, permissions in Cosmos DB can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of the client SDKs.</span></span> <span data-ttu-id="f869d-426">Cosmos DB 一律提供讀取或查詢權限之中繼資料的強式一致性。</span><span class="sxs-lookup"><span data-stu-id="f869d-426">Cosmos DB always provides strong consistency for reading or querying the metadata of a permission.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f869d-427">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f869d-427">Next steps</span></span>
<span data-ttu-id="f869d-428">深入了解如何使用 HTTP 命令來使用資源，請參閱[與 Cosmos DB 資源進行 RESTful 互動 (英文)](https://msdn.microsoft.com/library/azure/mt622086.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f869d-428">Learn more about working with resources by using HTTP commands in [RESTful interactions with Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx).</span></span>

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

