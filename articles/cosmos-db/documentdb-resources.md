---
title: "aaaAzure Cosmos DB 資源模型和概念 |Microsoft 文件"
description: "深入了解的資料庫、 集合、 使用者定義函數 (UDF)、 文件、 權限 toomanage 資源和多個 Azure Cosmos DB 的階層式模型。"
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
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a><span data-ttu-id="2fef4-104">Azure Cosmos DB 階層式資源模型和核心概念</span><span class="sxs-lookup"><span data-stu-id="2fef4-104">Azure Cosmos DB hierarchical resource model and core concepts</span></span>
<span data-ttu-id="2fef4-105">hello Azure Cosmos DB 管理的資料庫實體會參照的 tooas**資源**。</span><span class="sxs-lookup"><span data-stu-id="2fef4-105">hello database entities that Azure Cosmos DB manages are referred tooas **resources**.</span></span> <span data-ttu-id="2fef4-106">每個資源可透過邏輯 URI 唯一識別。</span><span class="sxs-lookup"><span data-stu-id="2fef4-106">Each resource is uniquely identified by a logical URI.</span></span> <span data-ttu-id="2fef4-107">您可以使用標準 HTTP 動詞命令、 要求/回應標頭和狀態碼的 hello 資源互動。</span><span class="sxs-lookup"><span data-stu-id="2fef4-107">You can interact with hello resources using standard HTTP verbs, request/response headers and status codes.</span></span> 

<span data-ttu-id="2fef4-108">讀取這份文件，您將會無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="2fef4-108">By reading this article, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="2fef4-109">什麼是 Cosmos DB 的資源模型？</span><span class="sxs-lookup"><span data-stu-id="2fef4-109">What is Cosmos DB's resource model?</span></span>
* <span data-ttu-id="2fef4-110">什麼是系統為相對於的 toouser 定義資源定義的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="2fef4-110">What are system defined resources as opposed toouser defined resources?</span></span>
* <span data-ttu-id="2fef4-111">如何處理資源？</span><span class="sxs-lookup"><span data-stu-id="2fef4-111">How do I address a resource?</span></span>
* <span data-ttu-id="2fef4-112">如何使用集合？</span><span class="sxs-lookup"><span data-stu-id="2fef4-112">How do I work with collections?</span></span>
* <span data-ttu-id="2fef4-113">如何使用預存程序、觸發程序和使用者定義函數 (UDF)？</span><span class="sxs-lookup"><span data-stu-id="2fef4-113">How do I work with stored procedures, triggers and User Defined Functions (UDFs)?</span></span>

## <a name="hierarchical-resource-model"></a><span data-ttu-id="2fef4-114">階層式資源模型</span><span class="sxs-lookup"><span data-stu-id="2fef4-114">Hierarchical resource model</span></span>
<span data-ttu-id="2fef4-115">如 hello 如下圖所示，hello Cosmos DB 階層式**資源模型**帳戶資料庫，每個透過邏輯且穩定 URI 定址的資源集合所組成。</span><span class="sxs-lookup"><span data-stu-id="2fef4-115">As hello following diagram illustrates, hello Cosmos DB hierarchical **resource model** consists of sets of resources under a database account, each addressable via a logical and stable URI.</span></span> <span data-ttu-id="2fef4-116">一組資源將會參考的 tooas**摘要**本文中。</span><span class="sxs-lookup"><span data-stu-id="2fef4-116">A set of resources will be referred tooas a **feed** in this article.</span></span> 

> [!NOTE]
> <span data-ttu-id="2fef4-117">Azure Cosmos 資料庫提供高效率的 TCP 通訊協定也是在其通訊模型中，可透過 hello RESTful [DocumentDB.NET 用戶端應用程式開發介面](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-117">Azure Cosmos DB offers a highly efficient TCP protocol which is also RESTful in its communication model, available through hello [DocumentDB .NET client API](documentdb-sdk-dotnet.md).</span></span>
> 
> 

<span data-ttu-id="2fef4-118">![Azure Cosmos DB 階層式資源模型][1]</span><span class="sxs-lookup"><span data-stu-id="2fef4-118">![Azure Cosmos DB hierarchical resource model][1]</span></span>  
<span data-ttu-id="2fef4-119">**階層式資源模型**</span><span class="sxs-lookup"><span data-stu-id="2fef4-119">**Hierarchical resource model**</span></span>   

<span data-ttu-id="2fef4-120">toostart 使用資源，您必須[建立資料庫帳戶](create-documentdb-dotnet.md)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fef4-120">toostart working with resources, you must [create a database account](create-documentdb-dotnet.md) using your Azure subscription.</span></span> <span data-ttu-id="2fef4-121">資料庫帳戶包含一組「資料庫」，而每個資料庫都包含多個「集合」，且各集合因此包含「預存程序」、「觸發程序」、UDF、「文件」和相關「附件」。</span><span class="sxs-lookup"><span data-stu-id="2fef4-121">A database account can consist of a set of **databases**, each containing multiple **collections**, each of which in turn contain **stored procedures, triggers, UDFs, documents** and related **attachments**.</span></span> <span data-ttu-id="2fef4-122">資料庫也有相關聯的**使用者**，每個都有一組**權限**tooaccess 集合，預存程序、 觸發程序，Udf、 文件或附件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-122">A database also has associated **users**, each with a set of **permissions** tooaccess collections, stored procedures, triggers, UDFs, documents or attachments.</span></span> <span data-ttu-id="2fef4-123">雖然資料庫、使用者、權限和集合都是具有已知結構描述的系統定義資源，但是文件和附件包含任意使用者定義 JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="2fef4-123">While databases, users, permissions and collections are system-defined resources with well-known schemas, documents and attachments contain arbitrary, user defined JSON content.</span></span>  

| <span data-ttu-id="2fef4-124">資源</span><span class="sxs-lookup"><span data-stu-id="2fef4-124">Resource</span></span> | <span data-ttu-id="2fef4-125">說明</span><span class="sxs-lookup"><span data-stu-id="2fef4-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2fef4-126">資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="2fef4-126">Database account</span></span> |<span data-ttu-id="2fef4-127">資料庫帳戶會與一組資料庫及附件之固定數目的 Blob 儲存體相關聯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-127">A database account is associated with a set of databases and a fixed amount of blob storage for attachments.</span></span> <span data-ttu-id="2fef4-128">您可以使用 Azure 訂用帳戶建立一或多個資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fef4-128">You can create one or more database accounts using your Azure subscription.</span></span> <span data-ttu-id="2fef4-129">如需詳細資訊，請瀏覽我們的 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-129">For more information, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> |
| <span data-ttu-id="2fef4-130">資料庫</span><span class="sxs-lookup"><span data-stu-id="2fef4-130">Database</span></span> |<span data-ttu-id="2fef4-131">資料庫是分割給多個集合之文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-131">A database is a logical container of document storage partitioned across collections.</span></span> <span data-ttu-id="2fef4-132">同時也是使用者容器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-132">It is also a users container.</span></span> |
| <span data-ttu-id="2fef4-133">User</span><span class="sxs-lookup"><span data-stu-id="2fef4-133">User</span></span> |<span data-ttu-id="2fef4-134">hello 邏輯命名空間範圍的權限。</span><span class="sxs-lookup"><span data-stu-id="2fef4-134">hello logical namespace for scoping permissions.</span></span> |
| <span data-ttu-id="2fef4-135">權限</span><span class="sxs-lookup"><span data-stu-id="2fef4-135">Permission</span></span> |<span data-ttu-id="2fef4-136">授權權杖存取 tooa 特定資源的使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-136">An authorization token associated with a user for access tooa specific resource.</span></span> |
| <span data-ttu-id="2fef4-137">集合</span><span class="sxs-lookup"><span data-stu-id="2fef4-137">Collection</span></span> |<span data-ttu-id="2fef4-138">集合是 JSON 文件的容器與 hello JavaScript 應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-138">A collection is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="2fef4-139">集合是一個可計費的實體，其中 hello[成本](performance-levels.md)取決於 hello 與 hello 集合相關聯的效能層級。</span><span class="sxs-lookup"><span data-stu-id="2fef4-139">A collection is a billable entity, where hello [cost](performance-levels.md) is determined by hello performance level associated with hello collection.</span></span> <span data-ttu-id="2fef4-140">集合可以跨一個或多個資料分割/伺服器，而且可以延展 toohandle 幾乎沒有限制的磁碟區的儲存體或輸送量。</span><span class="sxs-lookup"><span data-stu-id="2fef4-140">Collections can span one or more partitions/servers and can scale toohandle practically unlimited volumes of storage or throughput.</span></span> |
| <span data-ttu-id="2fef4-141">預存程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-141">Stored Procedure</span></span> |<span data-ttu-id="2fef4-142">這是向集合註冊，且 hello 資料庫引擎內以交易方式執行的 JavaScript 撰寫的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-142">Application logic written in JavaScript which is registered with a collection and transactionally executed within hello database engine.</span></span> |
| <span data-ttu-id="2fef4-143">觸發程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-143">Trigger</span></span> |<span data-ttu-id="2fef4-144">以 JavaScript 撰寫的應用程式邏輯，會在插入、取代或刪除作業之前或之後執行。</span><span class="sxs-lookup"><span data-stu-id="2fef4-144">Application logic written in JavaScript executed before or after either an insert, replace or delete operation.</span></span> |
| <span data-ttu-id="2fef4-145">UDF</span><span class="sxs-lookup"><span data-stu-id="2fef4-145">UDF</span></span> |<span data-ttu-id="2fef4-146">以 JavaScript 撰寫的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-146">Application logic written in JavaScript.</span></span> <span data-ttu-id="2fef4-147">Udf 啟用 toomodel 自訂查詢運算子，並藉此擴充 hello 核心 DocumentDB API 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="2fef4-147">UDFs enable you toomodel a custom query operator and thereby extend hello core DocumentDB API query language.</span></span> |
| <span data-ttu-id="2fef4-148">文件</span><span class="sxs-lookup"><span data-stu-id="2fef4-148">Document</span></span> |<span data-ttu-id="2fef4-149">使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="2fef4-149">User defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2fef4-150">根據預設，沒有結構描述需要 toobe 定義也沒有次要索引 toobe 提供所有 hello 文件加入 tooa 集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-150">By default, no schema needs toobe defined nor do secondary indices need toobe provided for all hello documents added tooa collection.</span></span> |
| <span data-ttu-id="2fef4-151">附件</span><span class="sxs-lookup"><span data-stu-id="2fef4-151">Attachment</span></span> |<span data-ttu-id="2fef4-152">附件是含有外部 Blob/媒體之參考資料和相關聯中繼資料的特殊文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-152">An attachment is a special document containing references and associated metadata for external blob/media.</span></span> <span data-ttu-id="2fef4-153">hello 開發人員可以選擇管理 Cosmos DB toohave hello blob，或將它儲存例如 OneDrive、 Dropbox 等外部 blob 服務提供者。</span><span class="sxs-lookup"><span data-stu-id="2fef4-153">hello developer can choose toohave hello blob managed by Cosmos DB or store it with an external blob service provider such as OneDrive, Dropbox, etc.</span></span> |

## <a name="system-vs-user-defined-resources"></a><span data-ttu-id="2fef4-154">系統與使用者定義的資源</span><span class="sxs-lookup"><span data-stu-id="2fef4-154">System vs. user defined resources</span></span>
<span data-ttu-id="2fef4-155">資料庫帳戶、資料庫、集合、使用者、權限、預存程序、觸發程序和 UDF 等資源的結構描述都是固定不變的，因此稱為「系統資源」。</span><span class="sxs-lookup"><span data-stu-id="2fef4-155">Resources such as database accounts, databases, collections, users, permissions, stored procedures, triggers, and UDFs - all have a fixed schema and are called system resources.</span></span> <span data-ttu-id="2fef4-156">相反地，例如文件和附件資源沒有任何限制 hello 結構描述，是使用者定義資源的範例。</span><span class="sxs-lookup"><span data-stu-id="2fef4-156">In contrast, resources such as documents and attachments have no restrictions on hello schema and are examples of user defined resources.</span></span> <span data-ttu-id="2fef4-157">在 Cosmos DB 中，系統和使用者定義資源都會呈現和管理為標準相符 JSON。</span><span class="sxs-lookup"><span data-stu-id="2fef4-157">In Cosmos DB, both system and user defined resources are represented and managed as standard-compliant JSON.</span></span> <span data-ttu-id="2fef4-158">系統或使用者定義的所有資源都有 hello 下列常見的屬性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-158">All resources, system or user defined, have hello following common properties.</span></span>

> [!NOTE]
> <span data-ttu-id="2fef4-159">請注意，系統產生的資源屬性在以 JSON 形式表示時，前面都會加上底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-159">Note that all system generated properties in a resource are prefixed with an underscore (_) in their JSON representation.</span></span>
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-160"><strong>屬性</strong></span><span class="sxs-lookup"><span data-stu-id="2fef4-160"><strong>Property</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-161"><strong>可由使用者設定或由系統產生？</strong></span><span class="sxs-lookup"><span data-stu-id="2fef4-161"><strong>User settable or system generated?</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-162"><strong>用途</strong></span><span class="sxs-lookup"><span data-stu-id="2fef4-162"><strong>Purpose</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-163">_rid</span><span class="sxs-lookup"><span data-stu-id="2fef4-163">_rid</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-164">由系統產生</span><span class="sxs-lookup"><span data-stu-id="2fef4-164">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-165">系統產生，hello 資源的唯一且階層式識別項</span><span class="sxs-lookup"><span data-stu-id="2fef4-165">System generated, unique and hierarchical identifier of hello resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-166">_etag</span><span class="sxs-lookup"><span data-stu-id="2fef4-166">_etag</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-167">由系統產生</span><span class="sxs-lookup"><span data-stu-id="2fef4-167">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-168">開放式並行存取控制所需的 hello 資源的 etag</span><span class="sxs-lookup"><span data-stu-id="2fef4-168">etag of hello resource required for optimistic concurrency control</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-169">_ts</span><span class="sxs-lookup"><span data-stu-id="2fef4-169">_ts</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-170">由系統產生</span><span class="sxs-lookup"><span data-stu-id="2fef4-170">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-171">Hello 資源上次更新時間戳記</span><span class="sxs-lookup"><span data-stu-id="2fef4-171">Last updated timestamp of hello resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-172">_self</span><span class="sxs-lookup"><span data-stu-id="2fef4-172">_self</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-173">由系統產生</span><span class="sxs-lookup"><span data-stu-id="2fef4-173">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-174">Hello 資源的唯一可定址 URI</span><span class="sxs-lookup"><span data-stu-id="2fef4-174">Unique addressable URI of hello resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-175">id</span><span class="sxs-lookup"><span data-stu-id="2fef4-175">id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-176">由系統產生</span><span class="sxs-lookup"><span data-stu-id="2fef4-176">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-177">使用者定義的 hello 資源的唯一名稱 （hello 與相同資料分割索引鍵的值）。</span><span class="sxs-lookup"><span data-stu-id="2fef4-177">User defined unique name of hello resource (with hello same partition key value).</span></span> <span data-ttu-id="2fef4-178">如果 hello 使用者未指定的識別碼，識別碼會是系統產生</span><span class="sxs-lookup"><span data-stu-id="2fef4-178">If hello user does not specify an id, an id will be system generated</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a><span data-ttu-id="2fef4-179">以線路表示資源</span><span class="sxs-lookup"><span data-stu-id="2fef4-179">Wire representation of resources</span></span>
<span data-ttu-id="2fef4-180">Cosmos DB 不會要求任何專屬延伸模組 toohello JSON 標準或特殊編碼。它可搭配標準相容的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-180">Cosmos DB does not mandate any proprietary extensions toohello JSON standard or special encodings; it works with standard compliant JSON documents.</span></span>  

### <a name="addressing-a-resource"></a><span data-ttu-id="2fef4-181">資源定址</span><span class="sxs-lookup"><span data-stu-id="2fef4-181">Addressing a resource</span></span>
<span data-ttu-id="2fef4-182">所有資源都能以 URI 定址。</span><span class="sxs-lookup"><span data-stu-id="2fef4-182">All resources are URI addressable.</span></span> <span data-ttu-id="2fef4-183">hello 值 hello **_self**屬性的資源代表 hello hello 資源的相對 URI。</span><span class="sxs-lookup"><span data-stu-id="2fef4-183">hello value of hello **_self** property of a resource represents hello relative URI of hello resource.</span></span> <span data-ttu-id="2fef4-184">hello hello URI 的格式包含 hello /\<摘要\>/ {_rid} 路徑片段：</span><span class="sxs-lookup"><span data-stu-id="2fef4-184">hello format of hello URI consists of hello /\<feed\>/{_rid} path segments:</span></span>  

| <span data-ttu-id="2fef4-185">值為 hello （_s）</span><span class="sxs-lookup"><span data-stu-id="2fef4-185">Value of hello _self</span></span> | <span data-ttu-id="2fef4-186">說明</span><span class="sxs-lookup"><span data-stu-id="2fef4-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2fef4-187">/dbs</span><span class="sxs-lookup"><span data-stu-id="2fef4-187">/dbs</span></span> |<span data-ttu-id="2fef4-188">資料庫帳戶下的資料庫摘要</span><span class="sxs-lookup"><span data-stu-id="2fef4-188">Feed of databases under a database account</span></span> |
| <span data-ttu-id="2fef4-189">/dbs/{dbName}</span><span class="sxs-lookup"><span data-stu-id="2fef4-189">/dbs/{dbName}</span></span> |<span data-ttu-id="2fef4-190">資料庫識別碼的事件符合 hello 值 {dbName}</span><span class="sxs-lookup"><span data-stu-id="2fef4-190">Database with an id matching hello value {dbName}</span></span> |
| <span data-ttu-id="2fef4-191">/dbs/{dbName}/colls/</span><span class="sxs-lookup"><span data-stu-id="2fef4-191">/dbs/{dbName}/colls/</span></span> |<span data-ttu-id="2fef4-192">在資料庫底下的集合摘要</span><span class="sxs-lookup"><span data-stu-id="2fef4-192">Feed of collections under a database</span></span> |
| <span data-ttu-id="2fef4-193">/dbs/{dbName}/colls/{collName}</span><span class="sxs-lookup"><span data-stu-id="2fef4-193">/dbs/{dbName}/colls/{collName}</span></span> |<span data-ttu-id="2fef4-194">集合識別碼的事件符合 hello 值 {collName}</span><span class="sxs-lookup"><span data-stu-id="2fef4-194">Collection with an id matching hello value {collName}</span></span> |
| <span data-ttu-id="2fef4-195">/dbs/{dbName}/colls/{collName}/docs</span><span class="sxs-lookup"><span data-stu-id="2fef4-195">/dbs/{dbName}/colls/{collName}/docs</span></span> |<span data-ttu-id="2fef4-196">在集合底下的文件摘要</span><span class="sxs-lookup"><span data-stu-id="2fef4-196">Feed of documents under a collection</span></span> |
| <span data-ttu-id="2fef4-197">/dbs/{dbName}/colls/{collName}/docs/{docId}</span><span class="sxs-lookup"><span data-stu-id="2fef4-197">/dbs/{dbName}/colls/{collName}/docs/{docId}</span></span> |<span data-ttu-id="2fef4-198">使用識別碼 hello 值 {文件} 比對文件</span><span class="sxs-lookup"><span data-stu-id="2fef4-198">Document with an id matching hello value {doc}</span></span> |
| <span data-ttu-id="2fef4-199">/dbs/{dbName}/users/</span><span class="sxs-lookup"><span data-stu-id="2fef4-199">/dbs/{dbName}/users/</span></span> |<span data-ttu-id="2fef4-200">在資料庫底下的使用者摘要</span><span class="sxs-lookup"><span data-stu-id="2fef4-200">Feed of users under a database</span></span> |
| <span data-ttu-id="2fef4-201">/dbs/{dbName}/users/{userId}</span><span class="sxs-lookup"><span data-stu-id="2fef4-201">/dbs/{dbName}/users/{userId}</span></span> |<span data-ttu-id="2fef4-202">使用者識別碼的事件符合 hello 值 {user}</span><span class="sxs-lookup"><span data-stu-id="2fef4-202">User with an id matching hello value {user}</span></span> |
| <span data-ttu-id="2fef4-203">/dbs/{dbName}/users/{userId}/permissions</span><span class="sxs-lookup"><span data-stu-id="2fef4-203">/dbs/{dbName}/users/{userId}/permissions</span></span> |<span data-ttu-id="2fef4-204">在使用者底下的權限摘要</span><span class="sxs-lookup"><span data-stu-id="2fef4-204">Feed of permissions under a user</span></span> |
| <span data-ttu-id="2fef4-205">/dbs/{dbName}/users/{userId}/permissions/{permissionId}</span><span class="sxs-lookup"><span data-stu-id="2fef4-205">/dbs/{dbName}/users/{userId}/permissions/{permissionId}</span></span> |<span data-ttu-id="2fef4-206">權限識別碼的事件符合 hello 值 {權限。</span><span class="sxs-lookup"><span data-stu-id="2fef4-206">Permission with an id matching hello value {permission}</span></span> |

<span data-ttu-id="2fef4-207">每個資源都有唯一的使用者定義名稱透過 hello id 屬性公開。</span><span class="sxs-lookup"><span data-stu-id="2fef4-207">Each resource has a unique user defined name exposed via hello id property.</span></span> <span data-ttu-id="2fef4-208">注意： 對於文件，如果 hello 使用者未指定的識別碼，我們支援的 Sdk 會自動產生 hello 文件的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2fef4-208">Note: for documents, if hello user does not specify an id, our supported SDKs will automatically generate a unique id for hello document.</span></span> <span data-ttu-id="2fef4-209">hello 識別碼是使用者定義字串，向上 too256 hello 特定父系資源內容內是唯一的字元。</span><span class="sxs-lookup"><span data-stu-id="2fef4-209">hello id is a user defined string, of up too256 characters that is unique within hello context of a specific parent resource.</span></span> 

<span data-ttu-id="2fef4-210">每個資源也有系統產生的階層式的資源識別碼 (也參考 tooas RID)，並透過 hello _rid 屬性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-210">Each resource also has a system generated hierarchical resource identifier (also referred tooas an RID), which is available via hello _rid property.</span></span> <span data-ttu-id="2fef4-211">hello RID 編碼 hello 整個階層的特定資源，而且很方便的內部表示法的分散式方式使用 tooenforce 參考完整性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-211">hello RID encodes hello entire hierarchy of a given resource and it is a convenient internal representation used tooenforce referential integrity in a distributed manner.</span></span> <span data-ttu-id="2fef4-212">hello RID 內是唯一的資料庫帳戶，它會在內部用於 Cosmos db 有效率的路由，而不需要跨磁碟分割查閱。</span><span class="sxs-lookup"><span data-stu-id="2fef4-212">hello RID is unique within a database account and it is internally used by Cosmos DB for efficient routing without requiring cross partition lookups.</span></span> <span data-ttu-id="2fef4-213">hello hello （_s） 及 hello _rid 屬性值會替代與標準格式的資源的表示法。</span><span class="sxs-lookup"><span data-stu-id="2fef4-213">hello values of hello _self and hello  _rid properties are both alternate and canonical representations of a resource.</span></span> 

<span data-ttu-id="2fef4-214">hello REST Api 支援的資源定址及路由的要求識別碼 hello 和 hello _rid 屬性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-214">hello REST APIs support addressing of resources and routing of requests by both hello id and hello _rid properties.</span></span>

## <a name="database-accounts"></a><span data-ttu-id="2fef4-215">資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="2fef4-215">Database accounts</span></span>
<span data-ttu-id="2fef4-216">您可以使用 Azure 訂用帳戶佈建一或多個 Cosmos DB 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fef4-216">You can provision one or more Cosmos DB database accounts using your Azure subscription.</span></span>

<span data-ttu-id="2fef4-217">您可以建立及管理透過 hello Azure 入口網站的 Cosmos DB 資料庫帳戶在[http://portal.azure.com/](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-217">You can create and manage Cosmos DB database accounts via hello Azure Portal at [http://portal.azure.com/](https://portal.azure.com/).</span></span> <span data-ttu-id="2fef4-218">建立和管理資料庫帳戶都需要管理存取權，而且只有在 Azure 訂用帳戶下才能執行。</span><span class="sxs-lookup"><span data-stu-id="2fef4-218">Creating and managing a database account requires administrative access and can only be performed under your Azure subscription.</span></span> 

### <a name="database-account-properties"></a><span data-ttu-id="2fef4-219">資料庫帳戶屬性</span><span class="sxs-lookup"><span data-stu-id="2fef4-219">Database account properties</span></span>
<span data-ttu-id="2fef4-220">佈建和管理資料庫帳戶的過程中，您可以設定和讀取 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="2fef4-220">As part of provisioning and managing a database account you can configure and read hello following properties:</span></span>  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-221"><strong>屬性名稱</strong></span><span class="sxs-lookup"><span data-stu-id="2fef4-221"><strong>Property Name</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-222"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="2fef4-222"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-223">一致性原則</span><span class="sxs-lookup"><span data-stu-id="2fef4-223">Consistency Policy</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-224">設定此屬性 tooconfigure hello 預設一致性層級的資料庫帳戶下的所有 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-224">Set this property tooconfigure hello default consistency level for all hello collections under your database account.</span></span> <span data-ttu-id="2fef4-225">您可以覆寫 hello 依每個要求來使用 hello [x 層 ms-一致性層級] 要求標頭的一致性層級。</span><span class="sxs-lookup"><span data-stu-id="2fef4-225">You can override hello consistency level on a per request basis using hello [x-ms-consistency-level] request header.</span></span> <p><p><span data-ttu-id="2fef4-226">請注意，這個屬性只適用於 toohello<i>使用者定義資源</i>。</span><span class="sxs-lookup"><span data-stu-id="2fef4-226">Note that this property only applies toohello <i>user defined resources</i>.</span></span> <span data-ttu-id="2fef4-227">系統定義的所有資源都是設定的 toosupport 讀取/查詢具有強式一致性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-227">All system defined resources are configured toosupport reads/queries with strong consistency.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="2fef4-228">授權金鑰</span><span class="sxs-lookup"><span data-stu-id="2fef4-228">Authorization Keys</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="2fef4-229">這些是 hello 主要和次要 master 和 readonly 金鑰提供系統管理存取 tooall hello 資料庫帳戶下的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-229">These are hello primary and secondary master and readonly keys that provide administrative access tooall of hello resources under hello database account.</span></span></p></td>
        </tr>
    </tbody>
</table>

<span data-ttu-id="2fef4-230">請注意，在加法 tooprovisioning，設定和管理您的資料庫帳戶從 hello Azure 入口網站中，您可以也以程式設計方式建立及管理 Cosmos DB 資料庫帳戶使用 hello [Azure Cosmos DB REST Api](/rest/api/documentdb/)為以及[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-230">Note that in addition tooprovisioning, configuring and managing your database account from hello Azure Portal, you can also programmatically create and manage Cosmos DB database accounts by using hello [Azure Cosmos DB REST APIs](/rest/api/documentdb/) as well as [client SDKs](documentdb-sdk-dotnet.md).</span></span>  

## <a name="databases"></a><span data-ttu-id="2fef4-231">資料庫</span><span class="sxs-lookup"><span data-stu-id="2fef4-231">Databases</span></span>
<span data-ttu-id="2fef4-232">Cosmos DB 資料庫是一個或多個集合和使用者的邏輯容器 hello 下列圖表所示。</span><span class="sxs-lookup"><span data-stu-id="2fef4-232">A Cosmos DB database is a logical container of one or more collections and users, as shown in hello following diagram.</span></span> <span data-ttu-id="2fef4-233">您可以建立任意數目的資料庫下 Cosmos DB 資料庫帳戶主體 toooffer 限制。</span><span class="sxs-lookup"><span data-stu-id="2fef4-233">You can create any number of databases under a Cosmos DB database account subject toooffer limits.</span></span>  

<span data-ttu-id="2fef4-234">![資料庫帳戶和集合階層式模型][2]</span><span class="sxs-lookup"><span data-stu-id="2fef4-234">![Database account and collections hierarchical model][2]</span></span>  
<span data-ttu-id="2fef4-235">**資料庫是使用者和集合的邏輯容器**</span><span class="sxs-lookup"><span data-stu-id="2fef4-235">**A Database is a logical container of users and collections**</span></span>

<span data-ttu-id="2fef4-236">資料庫可包含集合內分割的文件儲存體數量幾乎不受限制。</span><span class="sxs-lookup"><span data-stu-id="2fef4-236">A database can contain virtually unlimited document storage partitioned within collections.</span></span>

### <a name="elastic-scale-of-a-cosmos-db-database"></a><span data-ttu-id="2fef4-237">Cosmos DB 資料庫靈活的擴充能力</span><span class="sxs-lookup"><span data-stu-id="2fef4-237">Elastic scale of a Cosmos DB database</span></span>
<span data-ttu-id="2fef4-238">依預設 – 範圍從幾 GB toopetabytes SSD 支援文件儲存體和佈建的輸送量彈性 Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2fef4-238">A Cosmos DB database is elastic by default – ranging from a few GB toopetabytes of SSD backed document storage and provisioned throughput.</span></span> 

<span data-ttu-id="2fef4-239">不同於傳統的 RDBMS 中的資料庫，Cosmos DB 中的資料庫不是已設定領域的 tooa 單一機器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-239">Unlike a database in traditional RDBMS, a database in Cosmos DB is not scoped tooa single machine.</span></span> <span data-ttu-id="2fef4-240">以 Cosmos DB 應用程式的小數位數必須 toogrow，您可以建立更多的集合、 資料庫或兩者。</span><span class="sxs-lookup"><span data-stu-id="2fef4-240">With Cosmos DB, as your application’s scale needs toogrow, you can create more collections, databases, or both.</span></span> <span data-ttu-id="2fef4-241">的確，Microsoft 中的各種第一方應用程式都是依消費者規模來使用 Cosmos DB，建立極大的 Cosmos DB 資料庫，每個資料庫各包含數千個具有好幾 TB 文件儲存體的集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-241">Indeed, various first party applications within Microsoft have been using Cosmos DB at a consumer scale by creating extremely large Cosmos DB databases each containing thousands of collections with terabytes of document storage.</span></span> <span data-ttu-id="2fef4-242">您可以成長或壓縮資料庫，藉由新增或移除集合 toomeet 應用程式的小數位數的需求。</span><span class="sxs-lookup"><span data-stu-id="2fef4-242">You can grow or shrink a database by adding or removing collections toomeet your application’s scale requirements.</span></span> 

<span data-ttu-id="2fef4-243">您可以建立任意數目的資料庫主體 toohello 優惠中的集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-243">You can create any number of collections within a database subject toohello offer.</span></span> <span data-ttu-id="2fef4-244">每個集合有支援的 SSD 儲存體和佈建以供您根據 hello 選的效能層的輸送量。</span><span class="sxs-lookup"><span data-stu-id="2fef4-244">Each collection has SSD backed storage and throughput provisioned for you depending on hello selected performance tier.</span></span>

<span data-ttu-id="2fef4-245">Cosmos DB 資料庫同時也是使用者的容器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-245">A Cosmos DB database is also a container of users.</span></span> <span data-ttu-id="2fef4-246">使用者，在 [開啟] 是一組權限提供更細緻的授權和存取 toocollections、 文件和附加檔案的邏輯命名空間。</span><span class="sxs-lookup"><span data-stu-id="2fef4-246">A user, in-turn, is a logical namespace for a set of permissions that provides fine-grained authorization and access toocollections, documents and attachments.</span></span>  

<span data-ttu-id="2fef4-247">與 hello Cosmos DB 資源模型中的其他資源，可以建立資料庫，取代、 刪除、 讀取或列舉輕鬆地使用任一 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-247">As with other resources in hello Cosmos DB resource model, databases can be created, replaced, deleted, read or enumerated easily using either hello [REST APIs](/rest/api/documentdb/) or any of hello [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2fef4-248">Cosmos DB 保證讀取或查詢 hello 中繼資料的資料庫資源的強式一致性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-248">Cosmos DB guarantees strong consistency for reading or querying hello metadata of a database resource.</span></span> <span data-ttu-id="2fef4-249">自動刪除資料庫，可確保您無法存取任何 hello 集合或其中包含的使用者。</span><span class="sxs-lookup"><span data-stu-id="2fef4-249">Deleting a database automatically ensures that you cannot access any of hello collections or users contained within it.</span></span>   

## <a name="collections"></a><span data-ttu-id="2fef4-250">集合</span><span class="sxs-lookup"><span data-stu-id="2fef4-250">Collections</span></span>
<span data-ttu-id="2fef4-251">Cosmos DB 集合是 JSON 文件的容器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-251">A Cosmos DB collection is a container for your JSON documents.</span></span> 

### <a name="elastic-ssd-backed-document-storage"></a><span data-ttu-id="2fef4-252">彈性 SSD 支持文件儲存體</span><span class="sxs-lookup"><span data-stu-id="2fef4-252">Elastic SSD backed document storage</span></span>
<span data-ttu-id="2fef4-253">集合本質上是彈性的 - 它會隨著您新增或移除文件自動成長和縮減。</span><span class="sxs-lookup"><span data-stu-id="2fef4-253">A collection is intrinsically elastic - it automatically grows and shrinks as you add or remove documents.</span></span> <span data-ttu-id="2fef4-254">集合是邏輯資源，可以跨一或多個實體分割或伺服器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-254">Collections are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="2fef4-255">在集合中的資料分割的 hello 數目取決於 Cosmos DB 根據 hello 儲存大小和 hello 佈建的輸送量的集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-255">hello number of partitions within a collection is determined by Cosmos DB based on hello storage size and hello provisioned throughput of your collection.</span></span> <span data-ttu-id="2fef4-256">Cosmos DB 中的每個分割都有其相關聯的固定 SSD 支援儲存體數量，並且複寫以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-256">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="2fef4-257">資料分割管理完全受 Azure Cosmos DB，且您沒有 toowrite 複雜的程式碼或管理您的資料分割。</span><span class="sxs-lookup"><span data-stu-id="2fef4-257">Partition management is fully managed by Azure Cosmos DB, and you do not have toowrite complex code or manage your partitions.</span></span> <span data-ttu-id="2fef4-258">從儲存體和輸送量的角度來看，Cosmos DB 集合「實際上並無限制」。</span><span class="sxs-lookup"><span data-stu-id="2fef4-258">Cosmos DB collections are **practically unlimited** in terms of storage and throughput.</span></span> 

### <a name="automatic-indexing-of-collections"></a><span data-ttu-id="2fef4-259">集合的自動編製索引</span><span class="sxs-lookup"><span data-stu-id="2fef4-259">Automatic indexing of collections</span></span>
<span data-ttu-id="2fef4-260">Cosmos DB 是真正不具結構描述的資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="2fef4-260">Cosmos DB is a true schema-free database system.</span></span> <span data-ttu-id="2fef4-261">它不會假設或 hello JSON 文件所需的任何結構描述。</span><span class="sxs-lookup"><span data-stu-id="2fef4-261">It does not assume or require any schema for hello JSON documents.</span></span> <span data-ttu-id="2fef4-262">當您加入文件 tooa 集合，Cosmos DB 自動建立它們的索引，而且它們可供您 tooquery。</span><span class="sxs-lookup"><span data-stu-id="2fef4-262">As you add documents tooa collection, Cosmos DB automatically indexes them and they are available for you tooquery.</span></span> <span data-ttu-id="2fef4-263">在不需要結構描述或次要索引的情況下自動編製文件索引是 Cosmos DB 的重要功能，並且會啟用以獲得寫入最佳化、無鎖定和記錄結構化索引維護技術。</span><span class="sxs-lookup"><span data-stu-id="2fef4-263">Automatic indexing of documents without requiring schema or secondary indexes is a key capability of Cosmos DB and is enabled by write-optimized, lock-free and log-structured index maintenance techniques.</span></span> <span data-ttu-id="2fef4-264">Cosmos DB 支援極快速持續寫入量，同時仍然提供一致的查詢。</span><span class="sxs-lookup"><span data-stu-id="2fef4-264">Cosmos DB supports sustained volume of extremely fast writes while still serving consistent queries.</span></span> <span data-ttu-id="2fef4-265">文件和索引的儲存體是使用每個集合所耗用的 toocalculate hello 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="2fef4-265">Both document and index storage are used toocalculate hello storage consumed by each collection.</span></span> <span data-ttu-id="2fef4-266">您可以控制 hello 儲存和效能取捨相關聯索引所設定之集合的 hello 編製索引原則。</span><span class="sxs-lookup"><span data-stu-id="2fef4-266">You can control hello storage and performance trade-offs associated with indexing by configuring hello indexing policy for a collection.</span></span> 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a><span data-ttu-id="2fef4-267">設定集合中的 hello 編製索引原則</span><span class="sxs-lookup"><span data-stu-id="2fef4-267">Configuring hello indexing policy of a collection</span></span>
<span data-ttu-id="2fef4-268">檢索原則的每個集合的 hello 可讓您 toomake 效能和儲存體的利弊得失與索引相關聯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-268">hello indexing policy of each collection allows you toomake performance and storage trade-offs associated with indexing.</span></span> <span data-ttu-id="2fef4-269">hello 下列選項可使用 tooyou 索引組態的一部分：</span><span class="sxs-lookup"><span data-stu-id="2fef4-269">hello following options are available tooyou as part of indexing configuration:</span></span>  

* <span data-ttu-id="2fef4-270">選擇是否 hello 集合會自動索引 hello 文件的所有與否。</span><span class="sxs-lookup"><span data-stu-id="2fef4-270">Choose whether hello collection automatically indexes all of hello documents or not.</span></span> <span data-ttu-id="2fef4-271">預設會自動編製所有文件的索引。</span><span class="sxs-lookup"><span data-stu-id="2fef4-271">By default, all documents are automatically indexed.</span></span> <span data-ttu-id="2fef4-272">您可以選擇關閉自動檢索 tooturn，並選擇性地新增特定的文件 toohello 索引。</span><span class="sxs-lookup"><span data-stu-id="2fef4-272">You can choose tooturn off automatic indexing and selectively add only specific documents toohello index.</span></span> <span data-ttu-id="2fef4-273">相反地，您可以選擇性地選擇 tooexclude 只有特定的文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-273">Conversely, you can selectively choose tooexclude only specific documents.</span></span> <span data-ttu-id="2fef4-274">您可以藉由設定在集合中的 hello indexingPolicy hello 自動屬性 toobe true 或 false，並使用 hello [x-ms-indexingdirective] 要求標頭時插入、 取代或刪除文件來達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="2fef4-274">You can achieve this by setting hello automatic property toobe true or false on hello indexingPolicy of a collection and using hello [x-ms-indexingdirective] request header while inserting, replacing or deleting a document.</span></span>  
* <span data-ttu-id="2fef4-275">選擇 tooinclude 或排除特定的路徑或從您的文件中的模式 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="2fef4-275">Choose whether tooinclude or exclude specific paths or patterns in your documents from hello index.</span></span> <span data-ttu-id="2fef4-276">您可以達到此目的設定 includedPaths 並在集合中的 hello indexingPolicy excludedPaths 分別。</span><span class="sxs-lookup"><span data-stu-id="2fef4-276">You can achieve this by setting includedPaths and excludedPaths on hello indexingPolicy of a collection respectively.</span></span> <span data-ttu-id="2fef4-277">您也可以設定 hello 儲存和效能取捨範圍，再雜湊的特定路徑模式的查詢。</span><span class="sxs-lookup"><span data-stu-id="2fef4-277">You can also configure hello storage and performance trade-offs for range and hash queries for specific path patterns.</span></span> 
* <span data-ttu-id="2fef4-278">選擇同步 (一致) 與非同步 (緩慢) 索引更新。</span><span class="sxs-lookup"><span data-stu-id="2fef4-278">Choose between synchronous (consistent) and asynchronous (lazy) index updates.</span></span> <span data-ttu-id="2fef4-279">根據預設，hello 索引會以同步方式在每個插入、 取代或刪除文件 toohello 集合中的更新。</span><span class="sxs-lookup"><span data-stu-id="2fef4-279">By default, hello index is updated synchronously on each insert, replace or delete of a document toohello collection.</span></span> <span data-ttu-id="2fef4-280">這可讓 hello 查詢 toohonor hello 相同一致性層級的 hello 文件讀取。</span><span class="sxs-lookup"><span data-stu-id="2fef4-280">This enables hello queries toohonor hello same consistency level as that of hello document reads.</span></span> <span data-ttu-id="2fef4-281">雖然 Cosmos DB 有防寫最佳化，並支援持續性磁碟區的文件寫入，以及同步索引維護和服務一致的查詢，您可以設定特定集合 tooupdate 其索引延遲的方式。</span><span class="sxs-lookup"><span data-stu-id="2fef4-281">While Cosmos DB is write optimized and supports sustained volumes of document writes along with synchronous index maintenance and serving consistent queries, you can configure certain collections tooupdate their index lazily.</span></span> <span data-ttu-id="2fef4-282">延遲索引進一步 hello 寫入效能的提升，且適合用來大量擷取案例主要是大量讀取的集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-282">Lazy indexing boosts hello write performance further and is ideal for bulk ingestion scenarios for primarily read-heavy collections.</span></span>

<span data-ttu-id="2fef4-283">hello 集合上執行 PUT 可以變更 hello 編製索引原則。</span><span class="sxs-lookup"><span data-stu-id="2fef4-283">hello indexing policy can be changed by executing a PUT on hello collection.</span></span> <span data-ttu-id="2fef4-284">這可能是達成方式是透過 hello[用戶端 SDK](documentdb-sdk-dotnet.md)，hello [Azure 入口網站](https://portal.azure.com)或 hello [REST Api](/rest/api/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-284">This can be achieved either through hello [client SDK](documentdb-sdk-dotnet.md), hello [Azure Portal](https://portal.azure.com) or hello [REST APIs](/rest/api/documentdb/).</span></span>

### <a name="querying-a-collection"></a><span data-ttu-id="2fef4-285">查詢集合</span><span class="sxs-lookup"><span data-stu-id="2fef4-285">Querying a collection</span></span>
<span data-ttu-id="2fef4-286">在集合中的 hello 文件可以有任意的結構描述，您可以查詢集合中的文件，但未提供任何結構描述或預先次要索引。</span><span class="sxs-lookup"><span data-stu-id="2fef4-286">hello documents within a collection can have arbitrary schemas and you can query documents within a collection without providing any schema or secondary indices upfront.</span></span> <span data-ttu-id="2fef4-287">您可以查詢使用 hello hello 集合[Azure Cosmos DB DocumentDB API: SQL 語法參考](https://msdn.microsoft.com/library/azure/dn782250.aspx)，這樣會提供豐富的階層式、 關聯式及空間運算子，並透過 JavaScript 為基礎的 Udf 的擴充性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-287">You can query hello collection using hello [Azure Cosmos DB DocumentDB API: SQL syntax reference](https://msdn.microsoft.com/library/azure/dn782250.aspx), which provides rich hierarchical, relational, and spatial operators and extensibility via JavaScript-based UDFs.</span></span> <span data-ttu-id="2fef4-288">JSON 的文法，可讓模型 JSON 文件以 hello 樹狀目錄節點的標籤與樹狀目錄。</span><span class="sxs-lookup"><span data-stu-id="2fef4-288">JSON grammar allows for modeling JSON documents as trees with labels as hello tree nodes.</span></span> <span data-ttu-id="2fef4-289">這會同時應用 DocumentDB API 的自動編製索引技術與 DocumentDB API 的 SQL 方言。</span><span class="sxs-lookup"><span data-stu-id="2fef4-289">This is exploited both by DocumentDB API’s automatic indexing techniques as well as DocumentDB API's SQL dialect.</span></span> <span data-ttu-id="2fef4-290">hello DocumetDB API 查詢語言包含三個主要層面：</span><span class="sxs-lookup"><span data-stu-id="2fef4-290">hello DocumetDB API query language consists of three main aspects:</span></span>   

1. <span data-ttu-id="2fef4-291">較少的自然對應 toohello 樹狀結構，包括階層式查詢和預測的查詢作業。</span><span class="sxs-lookup"><span data-stu-id="2fef4-291">A small set of query operations that map naturally toohello tree structure including hierarchical queries and projections.</span></span> 
2. <span data-ttu-id="2fef4-292">關聯式作業 (包括複合、篩選、投射、彙總和自我聯結) 的子集。</span><span class="sxs-lookup"><span data-stu-id="2fef4-292">A subset of relational operations including composition, filter, projections, aggregates and self joins.</span></span> 
3. <span data-ttu-id="2fef4-293">可與 (1) 和 (2) 搭配使用的純 JavaScript 型 UDF。</span><span class="sxs-lookup"><span data-stu-id="2fef4-293">Pure JavaScript based UDFs that work with (1) and (2).</span></span>  

<span data-ttu-id="2fef4-294">hello Cosmos DB 查詢模型嘗試 toostrike 功能、 效率和簡化之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="2fef4-294">hello Cosmos DB query model attempts toostrike a balance between functionality, efficiency and simplicity.</span></span> <span data-ttu-id="2fef4-295">hello Cosmos DB 資料庫引擎原生會編譯並執行 hello SQL 查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="2fef4-295">hello Cosmos DB database engine natively compiles and executes hello SQL query statements.</span></span> <span data-ttu-id="2fef4-296">您可以查詢集合，使用 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-296">You can query a collection using hello [REST APIs](/rest/api/documentdb/) or any of hello [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2fef4-297">hello.NET SDK 隨附 LINQ 提供者。</span><span class="sxs-lookup"><span data-stu-id="2fef4-297">hello .NET SDK comes with a LINQ provider.</span></span>

> [!TIP]
> <span data-ttu-id="2fef4-298">您可以試用 hello DocumentDB API，並對我們 hello 中的資料集執行 SQL 查詢[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-298">You can try out hello DocumentDB API and run SQL queries against our dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
> 
> 

## <a name="multi-document-transactions"></a><span data-ttu-id="2fef4-299">多文件交易</span><span class="sxs-lookup"><span data-stu-id="2fef4-299">Multi-document transactions</span></span>
<span data-ttu-id="2fef4-300">資料庫交易提供安全且可預測的程式設計模型處理並行的變更 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="2fef4-300">Database transactions provide a safe and predictable programming model for dealing with concurrent changes toohello data.</span></span> <span data-ttu-id="2fef4-301">在 RDBMS，hello 傳統方式 toowrite 商務邏輯是 toowrite**預存程序**及/或**觸發程序**和出貨它 toohello 交易執行的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="2fef4-301">In RDBMS, hello traditional way toowrite business logic is toowrite **stored-procedures** and/or **triggers** and ship it toohello database server for transactional execution.</span></span> <span data-ttu-id="2fef4-302">RDBMS，在 hello 應用程式設計人員會是與兩個不同的程式設計語言的必要的 toodeal:</span><span class="sxs-lookup"><span data-stu-id="2fef4-302">In RDBMS, hello application programmer is required toodeal with two disparate programming languages:</span></span> 

* <span data-ttu-id="2fef4-303">hello （非交易式） 應用程式的程式語言 （例如 JavaScript、 Python、 C#、 Java 等）</span><span class="sxs-lookup"><span data-stu-id="2fef4-303">hello (non-transactional) application programming language (e.g. JavaScript, Python, C#, Java, etc.)</span></span>
* <span data-ttu-id="2fef4-304">T-SQL、 hello 異動程式設計語言的原生執行方式是 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="2fef4-304">T-SQL, hello transactional programming language which is natively executed by hello database</span></span>

<span data-ttu-id="2fef4-305">由於其深層承諾 tooJavaScript 和 JSON 直接在 hello 資料庫引擎內，Cosmos DB 會提供直覺式的程式設計模型執行的 JavaScript hello 集合以預存程序中直接根據應用程式邏輯和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2fef4-305">By virtue of its deep commitment tooJavaScript and JSON directly within hello database engine, Cosmos DB provides an intuitive programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="2fef4-306">這可讓這兩個 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2fef4-306">This allows for both of hello following:</span></span>

* <span data-ttu-id="2fef4-307">有效率的並行實作控制項，復原時，自動編製索引的直接在 hello 資料庫引擎中的 hello JSON 物件圖形</span><span class="sxs-lookup"><span data-stu-id="2fef4-307">Efficient implementation of concurrency control, recovery, automatic indexing of hello JSON object graphs directly in hello database engine</span></span>
* <span data-ttu-id="2fef4-308">自然表達 控制流程、 變數範圍，指派和例外狀況處理基本類型與直接以 hello JavaScript 的程式設計語言的資料庫交易的整合</span><span class="sxs-lookup"><span data-stu-id="2fef4-308">Naturally expressing control flow, variable scoping, assignment and integration of exception handling primitives with database transactions directly in terms of hello JavaScript programming language</span></span>

<span data-ttu-id="2fef4-309">hello JavaScript 邏輯在集合層級註冊可以再發出 hello 文件上的資料庫作業的指定集合的 hello。</span><span class="sxs-lookup"><span data-stu-id="2fef4-309">hello JavaScript logic registered at a collection level can then issue database operations on hello documents of hello given collection.</span></span> <span data-ttu-id="2fef4-310">Cosmos DB 隱含包裝 hello JavaScript 基礎預存程序和觸發程序與跨快照集隔離的環境 ACID 交易內文件集合內。</span><span class="sxs-lookup"><span data-stu-id="2fef4-310">Cosmos DB implicitly wraps hello JavaScript based stored procedures and triggers within an ambient ACID transactions with snapshot isolation across documents within a collection.</span></span> <span data-ttu-id="2fef4-311">在其執行中，hello 過程期間如果 hello JavaScript 會擲回的例外狀況，然後 hello 整筆交易便會中止。</span><span class="sxs-lookup"><span data-stu-id="2fef4-311">During hello course of its execution, if hello JavaScript throws an exception, then hello entire transaction is aborted.</span></span> <span data-ttu-id="2fef4-312">hello 產生的程式設計模型是非常簡單但強大。</span><span class="sxs-lookup"><span data-stu-id="2fef4-312">hello resulting programming model is a very simple yet powerful.</span></span> <span data-ttu-id="2fef4-313">JavaScript 開發人員會取得「持續性」程式設計模型，同時仍然使用其熟悉的語言建構和程式庫基本。</span><span class="sxs-lookup"><span data-stu-id="2fef4-313">JavaScript developers get a “durable” programming model while still using their familiar language constructs and library primitives.</span></span>   

<span data-ttu-id="2fef4-314">hello 直接 hello 資料庫內的能力 tooexecute JavaScript 引擎在 hello 相同位址空間，因為如此 hello 緩衝集區可以高效能和交易式資料庫對 hello 文件中的作業集合的執行。</span><span class="sxs-lookup"><span data-stu-id="2fef4-314">hello ability tooexecute JavaScript directly within hello database engine in hello same address space as hello buffer pool enables performant and transactional execution of database operations against hello documents of a collection.</span></span> <span data-ttu-id="2fef4-315">此外，Cosmos DB 資料庫引擎進行深層承諾 toohello JSON 及 JavaScript 排除任何 hello 的型別系統的應用程式與 hello 資料庫之間的阻抗不相符。</span><span class="sxs-lookup"><span data-stu-id="2fef4-315">Furthermore, Cosmos DB database engine makes a deep commitment toohello JSON and JavaScript eliminates any impedance mismatch between hello type systems of application and hello database.</span></span>   

<span data-ttu-id="2fef4-316">建立集合之後, 您可以向預存程序、 觸發程序和 Udf 集合使用 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-316">After creating a collection, you can register stored procedures, triggers and UDFs with a collection using hello [REST APIs](/rest/api/documentdb/) or any of hello [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2fef4-317">註冊之後，您就可以參考和執行它們。</span><span class="sxs-lookup"><span data-stu-id="2fef4-317">After registration, you can reference and execute them.</span></span> <span data-ttu-id="2fef4-318">請考慮 hello 下列預存程序完全以 JavaScript 撰寫 hello 的下列程式碼會採用兩個引數 （書籍名稱和作者名稱） 和建立新的文件、 文件的查詢，然後更新它 – 所有隱含的 ACID 交易中。</span><span class="sxs-lookup"><span data-stu-id="2fef4-318">Consider hello following stored procedure written entirely in JavaScript, hello code below takes two arguments (book name and author name) and creates a new document, queries for a document and then updates it – all within an implicit ACID transaction.</span></span> <span data-ttu-id="2fef4-319">在任何時間點 hello 執行期間，如果擲回 JavaScript 例外狀況，hello 整個交易中止。</span><span class="sxs-lookup"><span data-stu-id="2fef4-319">At any point during hello execution, if a JavaScript exception is thrown, hello entire transaction aborts.</span></span>

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

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

<span data-ttu-id="2fef4-320">hello 用戶端可以"ship"hello 上方 JavaScript 邏輯 toohello 資料庫進行透過 HTTP POST 的交易式執行。</span><span class="sxs-lookup"><span data-stu-id="2fef4-320">hello client can “ship” hello above JavaScript logic toohello database for transactional execution via HTTP POST.</span></span> <span data-ttu-id="2fef4-321">如需關於使用 HTTP 方法的詳細資訊，請參閱[與 Azure Cosmos DB 資源進行 RESTful 互動 (英文)](https://msdn.microsoft.com/library/azure/mt622086.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-321">For more information about using HTTP methods, see [RESTful interactions with Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx).</span></span> 

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


<span data-ttu-id="2fef4-322">請注意，JSON 及 JavaScript，原本即了解 hello 資料庫，因為沒有任何型別系統不符，「 OR 對應 」 或所需的程式碼產生識別常數。</span><span class="sxs-lookup"><span data-stu-id="2fef4-322">Notice that because hello database natively understands JSON and JavaScript, there is no type system mismatch, no “OR mapping” or code generation magic required.</span></span>   

<span data-ttu-id="2fef4-323">預存程序和觸發程序互動集合和 hello 文件集合透過妥善定義的物件模型，公開 hello 目前集合的內容中。</span><span class="sxs-lookup"><span data-stu-id="2fef4-323">Stored procedures and triggers interact with a collection and hello documents in a collection through a well-defined object model, which exposes hello current collection context.</span></span>  

<span data-ttu-id="2fef4-324">集合中 hello DocumentDB API 建立、 刪除、 讀取或列舉輕鬆地使用任一 hello [REST Api](/rest/api/documentdb/)或任何 hello[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-324">Collections in hello DocumentDB API can be created, deleted, read or enumerated easily using either hello [REST APIs](/rest/api/documentdb/) or any of hello [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2fef4-325">hello DocumentDB API 一律會提供強式一致性的讀取或查詢集合中的 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2fef4-325">hello DocumentDB API always provides strong consistency for reading or querying hello metadata of a collection.</span></span> <span data-ttu-id="2fef4-326">刪除集合時，會自動以確保您無法存取任何 hello 文件、 附件、 預存程序、 觸發程序和 Udf 包含在其中。</span><span class="sxs-lookup"><span data-stu-id="2fef4-326">Deleting a collection automatically ensures that you cannot access any of hello documents, attachments, stored procedures, triggers, and UDFs contained within it.</span></span>   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a><span data-ttu-id="2fef4-327">預存程序、觸發程序和使用者定義函數 (UDF)</span><span class="sxs-lookup"><span data-stu-id="2fef4-327">Stored procedures, triggers and User Defined Functions (UDF)</span></span>
<span data-ttu-id="2fef4-328">Hello 上一節所述，您可以撰寫應用程式邏輯 toorun 直接在交易內 hello 資料庫引擎內。</span><span class="sxs-lookup"><span data-stu-id="2fef4-328">As described in hello previous section, you can write application logic toorun directly within a transaction inside of hello database engine.</span></span> <span data-ttu-id="2fef4-329">hello 應用程式邏輯可以完全以 JavaScript 撰寫並為預存程序、 觸發程序或 UDF 可以模式化。</span><span class="sxs-lookup"><span data-stu-id="2fef4-329">hello application logic can be written entirely in JavaScript and can be modeled as a stored procedure, trigger or a UDF.</span></span> <span data-ttu-id="2fef4-330">hello 預存程序或觸發程序中的 JavaScript 程式碼可以插入、 取代、 刪除集合中的讀取或查詢文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-330">hello JavaScript code within a stored procedure or a trigger can insert, replace, delete, read or query documents within a collection.</span></span> <span data-ttu-id="2fef4-331">在 hello 另一方面，hello JavaScript UDF 內無法插入、 取代或刪除文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-331">On hello other hand, hello JavaScript within a UDF cannot insert, replace, or delete documents.</span></span> <span data-ttu-id="2fef4-332">Udf 列舉查詢的結果集的 hello 文件，並會產生另一個結果集。</span><span class="sxs-lookup"><span data-stu-id="2fef4-332">UDFs enumerate hello documents of a query's result set and produce another result set.</span></span> <span data-ttu-id="2fef4-333">若是多重租用，Cosmos DB 會強制執行嚴謹的保留型資源管理。</span><span class="sxs-lookup"><span data-stu-id="2fef4-333">For multi-tenancy, Cosmos DB enforces a strict reservation based resource governance.</span></span> <span data-ttu-id="2fef4-334">每個預存程序、 觸發程序或 UDF 取得固定的配量的作業系統資源 toodo 其工作。</span><span class="sxs-lookup"><span data-stu-id="2fef4-334">Each stored procedure, trigger or a UDF gets a fixed quantum of operating system resources toodo its work.</span></span> <span data-ttu-id="2fef4-335">此外，預存程序、 觸發程序或 Udf 無法針對外部的 JavaScript 程式庫連結，並會列入黑名單中而如果超過配置 toothem hello 資源預算。</span><span class="sxs-lookup"><span data-stu-id="2fef4-335">Furthermore, stored procedures, triggers or UDFs cannot link against external JavaScript libraries and are blacklisted if they exceed hello resource budgets allocated toothem.</span></span> <span data-ttu-id="2fef4-336">您可以註冊、 取消註冊預存程序、 觸發程序或 Udf，使用集合與 hello REST Api。</span><span class="sxs-lookup"><span data-stu-id="2fef4-336">You can register, unregister stored procedures, triggers or UDFs with a collection by using hello REST APIs.</span></span>  <span data-ttu-id="2fef4-337">註冊時，預存程序、觸發程序或 UDF 會預先編譯並儲存為位元組程式碼，以在稍後執行。</span><span class="sxs-lookup"><span data-stu-id="2fef4-337">Upon registration a stored procedure, trigger, or a UDF is pre-compiled and stored as byte code which gets executed later.</span></span> <span data-ttu-id="2fef4-338">hello 下列章節說明如何使用 hello Cosmos DB JavaScript SDK tooregister、 執行和取消註冊預存程序、 觸發程序和 UDF。</span><span class="sxs-lookup"><span data-stu-id="2fef4-338">hello following section illustrate how you can use hello Cosmos DB JavaScript SDK tooregister, execute, and unregister a stored procedure, trigger, and a UDF.</span></span> <span data-ttu-id="2fef4-339">hello JavaScript SDK 是簡單的包裝函式透過 hello [REST Api](/rest/api/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-339">hello JavaScript SDK is a simple wrapper over hello [REST APIs](/rest/api/documentdb/).</span></span> 

### <a name="registering-a-stored-procedure"></a><span data-ttu-id="2fef4-340">註冊預存程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-340">Registering a stored procedure</span></span>
<span data-ttu-id="2fef4-341">透過 HTTP POST 在集合上建立新的預存程序資源，即可註冊預存程序。</span><span class="sxs-lookup"><span data-stu-id="2fef4-341">Registration of a stored procedure creates a new stored procedure resource on a collection via HTTP POST.</span></span>  

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

### <a name="executing-a-stored-procedure"></a><span data-ttu-id="2fef4-342">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-342">Executing a stored procedure</span></span>
<span data-ttu-id="2fef4-343">預存程序的執行方式是藉由 hello 要求主體中傳遞參數 toohello 程序發出 HTTP POST 對現有的預存程序資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-343">Execution of a stored procedure is done by issuing an HTTP POST against an existing stored procedure resource by passing parameters toohello procedure in hello request body.</span></span>

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a><span data-ttu-id="2fef4-344">取消註冊預存程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-344">Unregistering a stored procedure</span></span>
<span data-ttu-id="2fef4-345">只要對現有預存程序資源發出 HTTP DELETE，即可取消註冊預存程序。</span><span class="sxs-lookup"><span data-stu-id="2fef4-345">Unregistering a stored procedure is simply done by issuing an HTTP DELETE against an existing stored procedure resource.</span></span>   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a><span data-ttu-id="2fef4-346">註冊預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-346">Registering a pre-trigger</span></span>
<span data-ttu-id="2fef4-347">透過 HTTP POST 在集合上建立新的觸發程序資源，即可註冊觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2fef4-347">Registration of a trigger is done by creating a new trigger resource on a collection via HTTP POST.</span></span> <span data-ttu-id="2fef4-348">您可以指定是否 hello 觸發程序會預先或是張貼觸發程序和 hello 類型的作業 （例如建立、 取代、 刪除或所有） 相關聯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-348">You can specify if hello trigger is a pre or a post trigger and hello type of operation it can be associated with (e.g. Create, Replace, Delete, or All).</span></span>   

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

### <a name="executing-a-pre-trigger"></a><span data-ttu-id="2fef4-349">執行預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-349">Executing a pre-trigger</span></span>
<span data-ttu-id="2fef4-350">觸發程序的執行方式是在 hello 時間發出 hello 透過 hello 要求標頭的文件資源的 POST/PUT/DEKETE 要求指定 hello 現有觸發程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="2fef4-350">Execution of a trigger is done by specifying hello name of an existing trigger at hello time of issuing hello POST/PUT/DELETE request of a document resource via hello request header.</span></span>  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a><span data-ttu-id="2fef4-351">取消註冊預先觸發程序</span><span class="sxs-lookup"><span data-stu-id="2fef4-351">Unregistering a pre-trigger</span></span>
<span data-ttu-id="2fef4-352">只要對現有觸發程序資源發出 HTTP DELETE，即可取消註冊觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2fef4-352">Unregistering a trigger is simply done via issuing an HTTP DELETE against an existing trigger resource.</span></span>  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a><span data-ttu-id="2fef4-353">註冊 UDF</span><span class="sxs-lookup"><span data-stu-id="2fef4-353">Registering a UDF</span></span>
<span data-ttu-id="2fef4-354">透過 HTTP POST 在集合上建立新的 UDF 資源，即可註冊 UDF。</span><span class="sxs-lookup"><span data-stu-id="2fef4-354">Registration of a UDF is done by creating a new UDF resource on a collection via HTTP POST.</span></span>  

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

### <a name="executing-a-udf-as-part-of-hello-query"></a><span data-ttu-id="2fef4-355">執行 hello 查詢 UDF</span><span class="sxs-lookup"><span data-stu-id="2fef4-355">Executing a UDF as part of hello query</span></span>
<span data-ttu-id="2fef4-356">UDF 可以指定為 hello SQL 查詢的一部份，並做為方法 tooextend hello 核心[hello DocumentDB API 的 SQL 查詢語言](https://msdn.microsoft.com/library/azure/dn782250.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-356">A UDF can be specified as part of hello SQL query and is used as a way tooextend hello core [SQL query language for hello DocumentDB API](https://msdn.microsoft.com/library/azure/dn782250.aspx).</span></span>

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a><span data-ttu-id="2fef4-357">取消註冊 UDF</span><span class="sxs-lookup"><span data-stu-id="2fef4-357">Unregistering a UDF</span></span>
<span data-ttu-id="2fef4-358">只要對現有 UDF 資源發出 HTTP DELETE，即可取消註冊 UDF。</span><span class="sxs-lookup"><span data-stu-id="2fef4-358">Unregistering a UDF is simply done by issuing an HTTP DELETE against an existing UDF resource.</span></span>  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

<span data-ttu-id="2fef4-359">雖然上述 hello 片段顯示 hello 註冊 (POST)、 取消註冊 (PUT)、 讀取/列出 (GET) 和執行 (POST) 透過 hello [JavaScript SDK](https://github.com/Azure/azure-documentdb-js)，您也可以使用 hello [REST Api](/rest/api/documentdb/)或其他[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-359">Although hello snippets above showed hello registration (POST), unregistration (PUT), read/list (GET) and execution (POST) via hello [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), you can also use hello [REST APIs](/rest/api/documentdb/) or other [client SDKs](documentdb-sdk-dotnet.md).</span></span> 

## <a name="documents"></a><span data-ttu-id="2fef4-360">文件</span><span class="sxs-lookup"><span data-stu-id="2fef4-360">Documents</span></span>
<span data-ttu-id="2fef4-361">您可以在集合中插入、取代、刪除、讀取、列舉和查詢任意 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-361">You can insert, replace, delete, read, enumerate and query arbitrary JSON documents in a collection.</span></span> <span data-ttu-id="2fef4-362">Cosmos DB 不會要求任何結構描述，而且不需要在順序 toosupport 查詢集合中的文件上的次要索引。</span><span class="sxs-lookup"><span data-stu-id="2fef4-362">Cosmos DB does not mandate any schema and does not require secondary indexes in order toosupport querying over documents in a collection.</span></span> <span data-ttu-id="2fef4-363">hello 文件的大小上限為 2 MB。</span><span class="sxs-lookup"><span data-stu-id="2fef4-363">hello maximum size for a document is 2 MB.</span></span>   

<span data-ttu-id="2fef4-364">Cosmos DB 是真正開放的資料庫服務，不會發明 JSON 文件的任何特殊資料類型 (例如日期時間) 或特定編碼。</span><span class="sxs-lookup"><span data-stu-id="2fef4-364">Being a truly open database service, Cosmos DB does not invent any specialized data types (e.g. date time) or specific encodings for JSON documents.</span></span> <span data-ttu-id="2fef4-365">請注意 Cosmos DB 不需要任何特殊 JSON 慣例 toocodify hello 之間的關聯性各種文件。hello Cosmos DB SQL 語法提供強大的階層式和關聯式查詢運算子 tooquery 和專案的文件，而不需要任何特殊的註解或文件使用辨別的屬性之間需要 toocodify 關聯性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-365">Note that Cosmos DB does not require any special JSON conventions toocodify hello relationships among various documents; hello SQL syntax of Cosmos DB provides very powerful hierarchical and relational query operators tooquery and project documents without any special annotations or need toocodify relationships among documents using distinguished properties.</span></span>  

<span data-ttu-id="2fef4-366">與所有其他資源，可以建立文件，取代、 刪除、 讀取、 列舉和輕鬆地使用 REST Api 或任何 hello 查詢[用戶端 Sdk](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-366">As with all other resources, documents can be created, replaced, deleted, read, enumerated and queried easily using either REST APIs or any of hello [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2fef4-367">刪除文件會立即釋出 hello 配額對應 tooall 的巢狀的 hello 附件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-367">Deleting a document instantly frees up hello quota corresponding tooall of hello nested attachments.</span></span> <span data-ttu-id="2fef4-368">hello 讀取的文件的一致性層級會遵循 hello 一致性原則的 hello 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fef4-368">hello read consistency level of documents follows hello consistency policy on hello database account.</span></span> <span data-ttu-id="2fef4-369">根據您應用程式的資料一致性需求，可以覆寫每個要求的這個原則。</span><span class="sxs-lookup"><span data-stu-id="2fef4-369">This policy can be overridden on a per-request basis depending on data consistency requirements of your application.</span></span> <span data-ttu-id="2fef4-370">當查詢文件，hello 讀取一致性如下所示 hello 索引 hello 集合上設定的模式。</span><span class="sxs-lookup"><span data-stu-id="2fef4-370">When querying documents, hello read consistency follows hello indexing mode set on hello collection.</span></span> <span data-ttu-id="2fef4-371">對於 「 一致性 」，這會遵循 hello 帳戶一致性原則。</span><span class="sxs-lookup"><span data-stu-id="2fef4-371">For “consistent”, this follows hello account’s consistency policy.</span></span> 

## <a name="attachments-and-media"></a><span data-ttu-id="2fef4-372">附件和媒體</span><span class="sxs-lookup"><span data-stu-id="2fef4-372">Attachments and media</span></span>
<span data-ttu-id="2fef4-373">Cosmos DB 可讓您 toostore 二進位 blob/媒體 Cosmos DB （每個帳戶最多 2 gb） 或 tooyour 自己的遠端媒體存放區。</span><span class="sxs-lookup"><span data-stu-id="2fef4-373">Cosmos DB allows you toostore binary blobs/media either with Cosmos DB (maximum of 2 GB per account) or tooyour own remote media store.</span></span> <span data-ttu-id="2fef4-374">它也可讓您的媒體稱為附件的特殊文件方面的 toorepresent hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2fef4-374">It also allows you toorepresent hello metadata of a media in terms of a special document called attachment.</span></span> <span data-ttu-id="2fef4-375">附件 Cosmos DB 中的參考 hello 媒體 /blob 儲存其他地方的特殊 (JSON) 文件。</span><span class="sxs-lookup"><span data-stu-id="2fef4-375">An attachment in Cosmos DB is a special (JSON) document that references hello media/blob stored elsewhere.</span></span> <span data-ttu-id="2fef4-376">附件的只是特殊文件，擷取 hello 中繼資料 （例如位置、 作者等） 的遠端媒體儲存體中儲存媒體。</span><span class="sxs-lookup"><span data-stu-id="2fef4-376">An attachment is simply a special document that captures hello metadata (e.g. location, author etc.) of a media stored in a remote media storage.</span></span> 

<span data-ttu-id="2fef4-377">請考慮使用 Cosmos DB toostore 筆跡註釋，社交讀取應用程式和中繼資料包括註解，反白顯示，書籤、 分級、 類似 dislikes 等相關聯的特定使用者的電子書。</span><span class="sxs-lookup"><span data-stu-id="2fef4-377">Consider a social reading application which uses Cosmos DB toostore ink annotations, and metadata including comments, highlights, bookmarks, ratings, likes/dislikes etc. associated for an e-book of a given user.</span></span>   

* <span data-ttu-id="2fef4-378">hello hello 活頁簿本身的內容會儲存在 hello 媒體儲存體是可從 Cosmos DB 資料庫帳戶的一部分或遠端媒體存放區。</span><span class="sxs-lookup"><span data-stu-id="2fef4-378">hello content of hello book itself is stored in hello media storage either available as part of Cosmos DB database account or a remote media store.</span></span> 
* <span data-ttu-id="2fef4-379">應用程式可能會將每個使用者的中繼資料儲存為不同的文件 (例如 Joe 的 book1 中繼資料儲存在 /colls/joe/docs/book1 所參考的文件中)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-379">An application may store each user’s metadata as a distinct document -- e.g. Joe’s metadata for book1 is stored in a document referenced by /colls/joe/docs/book1.</span></span> 
* <span data-ttu-id="2fef4-380">指向 toohello 內容頁面的使用者指定書籍的附件儲存在 hello 對應文件例如 /colls/joe/docs/book1/chapter1 /colls/joe/docs/book1/chapter2 等等。</span><span class="sxs-lookup"><span data-stu-id="2fef4-380">Attachments pointing toohello content pages of a given book of a user are stored under hello corresponding document e.g. /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 etc.</span></span> 

<span data-ttu-id="2fef4-381">請注意，上面所列的 hello 範例會使用易記識別碼 tooconvey hello 資源階層。</span><span class="sxs-lookup"><span data-stu-id="2fef4-381">Note that hello examples listed above use friendly ids tooconvey hello resource hierarchy.</span></span> <span data-ttu-id="2fef4-382">透過 hello REST Api，透過唯一的資源 id 所存取的資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-382">Resources are accessed via hello REST APIs through unique resource ids.</span></span> 

<span data-ttu-id="2fef4-383">Hello Cosmos DB 受的媒體，hello 附件 hello _media 屬性會參考 hello 媒體依其 URI。</span><span class="sxs-lookup"><span data-stu-id="2fef4-383">For hello media that is managed by Cosmos DB, hello _media property of hello attachment will reference hello media by its URI.</span></span> <span data-ttu-id="2fef4-384">Cosmos DB 將可確保 toogarbage 收集 hello 媒體時卸除所有 hello 未完成的參考。</span><span class="sxs-lookup"><span data-stu-id="2fef4-384">Cosmos DB will ensure toogarbage collect hello media when all of hello outstanding references are dropped.</span></span> <span data-ttu-id="2fef4-385">Cosmos DB 自動上傳 hello 新的媒體時，會產生 hello 附件，並於其中填入 hello _media toopoint toohello 新增的媒體。</span><span class="sxs-lookup"><span data-stu-id="2fef4-385">Cosmos DB automatically generates hello attachment when you upload hello new media and populates hello _media toopoint toohello newly added media.</span></span> <span data-ttu-id="2fef4-386">如果您選擇 toostore hello 媒體受您 （例如 OneDrive，Azure 儲存體、 DropBox 等） 的遠端 blob 存放區中，您仍然可以使用 附件 tooreference hello 媒體。</span><span class="sxs-lookup"><span data-stu-id="2fef4-386">If you choose toostore hello media in a remote blob store managed by you (e.g. OneDrive, Azure Storage, DropBox etc), you can still use attachments tooreference hello media.</span></span> <span data-ttu-id="2fef4-387">在此情況下，您會自行建立 hello 附件，並擴展其 _media 屬性。</span><span class="sxs-lookup"><span data-stu-id="2fef4-387">In this case, you will create hello attachment yourself and populate its _media property.</span></span>   

<span data-ttu-id="2fef4-388">如同所有其他資源，附件可以建立、 取代、 刪除、 讀取或列舉輕鬆地使用 REST Api 或任何 hello 用戶端 Sdk。</span><span class="sxs-lookup"><span data-stu-id="2fef4-388">As with all other resources, attachments can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of hello client SDKs.</span></span> <span data-ttu-id="2fef4-389">文件，與 hello 讀取附件的一致性層級會遵循 hello 一致性原則的 hello 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fef4-389">As with documents, hello read consistency level of attachments follows hello consistency policy on hello database account.</span></span> <span data-ttu-id="2fef4-390">根據您應用程式的資料一致性需求，可以覆寫每個要求的這個原則。</span><span class="sxs-lookup"><span data-stu-id="2fef4-390">This policy can be overridden on a per-request basis depending on data consistency requirements of your application.</span></span> <span data-ttu-id="2fef4-391">查詢時的附件，hello 讀取一致性如下所示 hello 索引 hello 集合上設定的模式。</span><span class="sxs-lookup"><span data-stu-id="2fef4-391">When querying for attachments, hello read consistency follows hello indexing mode set on hello collection.</span></span> <span data-ttu-id="2fef4-392">對於 「 一致性 」，這會遵循 hello 帳戶一致性原則。</span><span class="sxs-lookup"><span data-stu-id="2fef4-392">For “consistent”, this follows hello account’s consistency policy.</span></span> 
 

## <a name="users"></a><span data-ttu-id="2fef4-393">使用者</span><span class="sxs-lookup"><span data-stu-id="2fef4-393">Users</span></span>
<span data-ttu-id="2fef4-394">Cosmos DB 使用者代表用於分組權限的邏輯命名空間。</span><span class="sxs-lookup"><span data-stu-id="2fef4-394">A Cosmos DB user represents a logical namespace for grouping permissions.</span></span> <span data-ttu-id="2fef4-395">Cosmos DB 使用者可能對應 tooa 使用者的身分識別管理系統或預先定義的應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="2fef4-395">A Cosmos DB user may correspond tooa user in an identity management system or a predefined application role.</span></span> <span data-ttu-id="2fef4-396">Cosmos DB 使用者只代表抽象 toogroup 資料庫下的權限集。</span><span class="sxs-lookup"><span data-stu-id="2fef4-396">For Cosmos DB, a user simply represents an abstraction toogroup a set of permissions under a database.</span></span>   

<span data-ttu-id="2fef4-397">實作多租用戶應用程式中，您可以在 Cosmos DB 對應 tooyour 實際使用者或應用程式的 hello 租用戶中建立使用者。</span><span class="sxs-lookup"><span data-stu-id="2fef4-397">For implementing multi-tenancy in your application, you can create users in Cosmos DB which corresponds tooyour actual users or hello tenants of your application.</span></span> <span data-ttu-id="2fef4-398">然後，您可以建立針對指定的使用者對應 toohello 各種集合、 文件、 附件和其他內容的存取控制的權限。</span><span class="sxs-lookup"><span data-stu-id="2fef4-398">You can then create permissions for a given user that correspond toohello access control over various collections, documents, attachments, etc.</span></span>   

<span data-ttu-id="2fef4-399">為您的應用程式需要與使用者成長 tooscale，可以採用不同的方式 tooshard 您的資料。</span><span class="sxs-lookup"><span data-stu-id="2fef4-399">As your applications need tooscale with your user growth, you can adopt various ways tooshard your data.</span></span> <span data-ttu-id="2fef4-400">您可以建立每位使用者的模型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2fef4-400">You can model each of your users as follows:</span></span>   

* <span data-ttu-id="2fef4-401">每個使用者對應 tooa 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2fef4-401">Each user maps tooa database.</span></span>
* <span data-ttu-id="2fef4-402">每個使用者對應 tooa 集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-402">Each user maps tooa collection.</span></span> 
* <span data-ttu-id="2fef4-403">文件對應 toomultiple 使用者移 tooa 專用的集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-403">Documents corresponding toomultiple users go tooa dedicated collection.</span></span> 
* <span data-ttu-id="2fef4-404">文件對應 toomultiple 使用者移 tooa 組集合。</span><span class="sxs-lookup"><span data-stu-id="2fef4-404">Documents corresponding toomultiple users go tooa set of collections.</span></span>   

<span data-ttu-id="2fef4-405">不論您選擇的 hello 特定分區化策略，您可以建立實際使用者模型為 Cosmos DB 資料庫中的使用者，並沒問題的更細緻權限 tooeach 使用者建立關聯。</span><span class="sxs-lookup"><span data-stu-id="2fef4-405">Regardless of hello specific sharding strategy you choose, you can model your actual users as users in Cosmos DB database and associate fine grained permissions tooeach user.</span></span>  

<span data-ttu-id="2fef4-406">![使用者集合][3]</span><span class="sxs-lookup"><span data-stu-id="2fef4-406">![User collections][3]</span></span>  
<span data-ttu-id="2fef4-407">**分區化策略和模型化使用者**</span><span class="sxs-lookup"><span data-stu-id="2fef4-407">**Sharding strategies and modeling users**</span></span>

<span data-ttu-id="2fef4-408">如同其他資源，Cosmos DB 中的使用者可以建立、 取代、 刪除、 讀取或列舉輕鬆地使用 REST Api 或任何 hello 用戶端 Sdk。</span><span class="sxs-lookup"><span data-stu-id="2fef4-408">Like all other resources, users in Cosmos DB can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of hello client SDKs.</span></span> <span data-ttu-id="2fef4-409">Cosmos DB 一定會提供強式一致性的讀取或查詢 hello 中繼資料的使用者資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-409">Cosmos DB always provides strong consistency for reading or querying hello metadata of a user resource.</span></span> <span data-ttu-id="2fef4-410">很值得，自動刪除使用者可確保您無法存取任何內含的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="2fef4-410">It is worth pointing out that deleting a user automatically ensures that you cannot access any of hello permissions contained within it.</span></span> <span data-ttu-id="2fef4-411">即使 hello Cosmos DB 一部分 hello 刪除使用者 hello 背景回收 hello hello 使用權限配額，hello 刪除權限為可用立即再次您 toouse。</span><span class="sxs-lookup"><span data-stu-id="2fef4-411">Even though hello Cosmos DB reclaims hello quota of hello permissions as part of hello deleted user in hello background, hello deleted permissions is available instantly again for you toouse.</span></span>  

## <a name="permissions"></a><span data-ttu-id="2fef4-412">權限</span><span class="sxs-lookup"><span data-stu-id="2fef4-412">Permissions</span></span>
<span data-ttu-id="2fef4-413">從存取控制觀點來看，系統會將資源 (例如資料庫帳戶、資料庫、使用者和權限) 視為「管理」  資源，因為這些都需要管理權限。</span><span class="sxs-lookup"><span data-stu-id="2fef4-413">From an access control perspective, resources such as database accounts, databases, users and permission are considered *administrative* resources since these require administrative permissions.</span></span> <span data-ttu-id="2fef4-414">在 hello 另一方面資源包括 hello 集合、 文件、 附件、 預存程序、 觸發程序和 Udf 為範圍下指定的資料庫，並視為*應用程式資源*。</span><span class="sxs-lookup"><span data-stu-id="2fef4-414">On hello other hand, resources including hello collections, documents, attachments, stored procedures, triggers, and UDFs are scoped under a given database and considered *application resources*.</span></span> <span data-ttu-id="2fef4-415">對應的資源與 hello 角色存取它們 （也就是 hello 系統管理員和使用者） 的 toohello 兩種類型的 hello 授權模型會定義兩種類型的*存取金鑰*:*主要金鑰*和*資源索引鍵*。</span><span class="sxs-lookup"><span data-stu-id="2fef4-415">Corresponding toohello two types of resources and hello roles that access them (namely hello administrator and user), hello authorization model defines two types of *access keys*: *master key* and *resource key*.</span></span> <span data-ttu-id="2fef4-416">hello 主要金鑰屬於 hello 資料庫帳戶和 toohello 開發人員 （或管理員） 提供者佈建 hello 資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="2fef4-416">hello master key is a part of hello database account and is provided toohello developer (or administrator) who is provisioning hello database account.</span></span> <span data-ttu-id="2fef4-417">此主要金鑰具有系統管理員語意，可以使用的 tooauthorize 存取 tooboth 系統管理和應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-417">This master key has administrator semantics, in that it can be used tooauthorize access tooboth administrative and application resources.</span></span> <span data-ttu-id="2fef4-418">資源索引鍵相較之下，會允許存取 tooa 細微的存取金鑰*特定*應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-418">In contrast, a resource key is a granular access key that allows access tooa *specific* application resource.</span></span> <span data-ttu-id="2fef4-419">因此，它會擷取 hello hello 使用者的資料庫之間的關聯性，hello 權限 hello 使用者擁有特定資源 （例如集合、 文件、 附件、 預存程序、 觸發程序或 UDF）。</span><span class="sxs-lookup"><span data-stu-id="2fef4-419">Thus, it captures hello relationship between hello user of a database and hello permissions hello user has for a specific resource (e.g. collection, document, attachment, stored procedure, trigger, or UDF).</span></span>   

<span data-ttu-id="2fef4-420">hello 唯一方式 tooobtain 資源索引鍵是建立在指定的使用者權限資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-420">hello only way tooobtain a resource key is by creating a permission resource under a given user.</span></span> <span data-ttu-id="2fef4-421">請注意，在訂單 toocreate 或擷取權限、 主要金鑰必須呈現 hello 授權標頭中。</span><span class="sxs-lookup"><span data-stu-id="2fef4-421">Note that In order toocreate or retrieve a permission, a master key must be presented in hello authorization header.</span></span> <span data-ttu-id="2fef4-422">權限資源繫結合作對 hello 資源、 存取和 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2fef4-422">A permission resource ties hello resource, its access and hello user.</span></span> <span data-ttu-id="2fef4-423">建立權限資源之後, hello 使用者只需要 toopresent hello 相關聯的資源索引鍵順序 toogain 存取 toohello 相關資源。</span><span class="sxs-lookup"><span data-stu-id="2fef4-423">After creating a permission resource, hello user only needs toopresent hello associated resource key in order toogain access toohello relevant resource.</span></span> <span data-ttu-id="2fef4-424">因此，資源索引鍵可視為邏輯和 compact hello 權限資源的表示方式。</span><span class="sxs-lookup"><span data-stu-id="2fef4-424">Hence, a resource key can be viewed as a logical and compact representation of hello permission resource.</span></span>  

<span data-ttu-id="2fef4-425">如同所有其他資源，Cosmos DB 中的權限可以建立、 取代、 刪除、 讀取或列舉輕鬆地使用 REST Api 或任何 hello 用戶端 Sdk。</span><span class="sxs-lookup"><span data-stu-id="2fef4-425">As with all other resources, permissions in Cosmos DB can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of hello client SDKs.</span></span> <span data-ttu-id="2fef4-426">Cosmos DB 一定會提供強式一致性的讀取或查詢 hello 中繼資料的權限。</span><span class="sxs-lookup"><span data-stu-id="2fef4-426">Cosmos DB always provides strong consistency for reading or querying hello metadata of a permission.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2fef4-427">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2fef4-427">Next steps</span></span>
<span data-ttu-id="2fef4-428">深入了解如何使用 HTTP 命令來使用資源，請參閱[與 Cosmos DB 資源進行 RESTful 互動 (英文)](https://msdn.microsoft.com/library/azure/mt622086.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2fef4-428">Learn more about working with resources by using HTTP commands in [RESTful interactions with Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx).</span></span>

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

