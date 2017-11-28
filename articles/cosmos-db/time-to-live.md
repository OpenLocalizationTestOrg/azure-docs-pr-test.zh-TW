---
title: "在 Azure Cosmos DB 時間 toolive aaaExpire 資料 |Microsoft 文件"
description: "Ttl，Microsoft Azure Cosmos DB 會提供自動清除從 hello 系統在一段時間之後的 hello 能力 toohave 文件。"
services: cosmos-db
documentationcenter: 
keywords: "toolive 時間"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="390ca-104">到期時間 toolive 使用自動 Azure Cosmos DB 集合中的資料</span><span class="sxs-lookup"><span data-stu-id="390ca-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="390ca-105">應用程式可以產生並儲存大量資料。</span><span class="sxs-lookup"><span data-stu-id="390ca-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="390ca-106">其中有些資料，例如電腦產生的事件資料、記錄檔和使用者工作階段資訊只能在有限的期間內使用。</span><span class="sxs-lookup"><span data-stu-id="390ca-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="390ca-107">一旦 hello 資料變得多餘 toohello hello 應用程式需要安全 toopurge 這項資料，並減少應用程式的 hello 儲存需求。</span><span class="sxs-lookup"><span data-stu-id="390ca-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="390ca-108">「 時間 toolive 」 或 TTL，Microsoft Azure Cosmos DB 會提供從 hello 資料庫中自動清除，在一段時間之後的 hello 能力 toohave 文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="390ca-109">hello 預設時間 toolive 可以 hello 集合層級設定，並覆寫個別文件為基礎。</span><span class="sxs-lookup"><span data-stu-id="390ca-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="390ca-110">設定 TTL (不論是作為集合預設值或是在文件層級設定) 之後，Cosmos DB 就會自動移除自上次修改後存在時間達該指定時間 (以秒為單位) 的文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="390ca-111">上次修改 hello 文件時，toolive Cosmos DB 中的時間就會使用針對位移。</span><span class="sxs-lookup"><span data-stu-id="390ca-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="390ca-112">toodo 此使用 hello`_ts`存在於每個文件的欄位。</span><span class="sxs-lookup"><span data-stu-id="390ca-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="390ca-113">hello _ts 欄位是 unix 樣式 epoch 時間戳記代表 hello 日期和時間。</span><span class="sxs-lookup"><span data-stu-id="390ca-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="390ca-114">hello`_ts`每次修改文件時，欄位會更新。</span><span class="sxs-lookup"><span data-stu-id="390ca-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="390ca-115">TTL 行為</span><span class="sxs-lookup"><span data-stu-id="390ca-115">TTL behavior</span></span>
<span data-ttu-id="390ca-116">hello TTL 功能是由兩個層級-hello 集合層級和 hello 文件層級的 TTL 屬性控制。</span><span class="sxs-lookup"><span data-stu-id="390ca-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="390ca-117">hello 值會設定以秒為單位，而會被視為 delta 從 hello`_ts`在上次修改該 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="390ca-118">DefaultTTL hello 集合</span><span class="sxs-lookup"><span data-stu-id="390ca-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="390ca-119">如果遺失 （或 set toonull） 文件不會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="390ca-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="390ca-120">如果有的話，hello 值為"-1"= 無限 – 依預設不會過期的文件</span><span class="sxs-lookup"><span data-stu-id="390ca-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="390ca-121">如果有的話，因此 hello 值是某個數字 ("n")-文件到期"n"秒之後在上次修改</span><span class="sxs-lookup"><span data-stu-id="390ca-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="390ca-122">TTL hello 文件：</span><span class="sxs-lookup"><span data-stu-id="390ca-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="390ca-123">屬性是 DefaultTTL 存在於 hello 父集合時，才適用。</span><span class="sxs-lookup"><span data-stu-id="390ca-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="390ca-124">覆寫 hello 父集合的 hello DefaultTTL 值。</span><span class="sxs-lookup"><span data-stu-id="390ca-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="390ca-125">只要 hello 文件已過期 (`ttl`  +  `_ts` > = 目前的伺服器時間)，hello 文件標示為 「 過期 」。</span><span class="sxs-lookup"><span data-stu-id="390ca-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="390ca-126">將這些文件上允許任何操作，在此時間之後，將排除 hello 執行任何查詢結果。</span><span class="sxs-lookup"><span data-stu-id="390ca-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="390ca-127">hello 文件會實際刪除 hello 系統中，並視情況在稍後刪除 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="390ca-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="390ca-128">這不會耗用任何[要求單位 (Ru)](request-units.md)從 hello 集合預算。</span><span class="sxs-lookup"><span data-stu-id="390ca-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="390ca-129">hello 遵循矩陣會顯示 hello 上方邏輯：</span><span class="sxs-lookup"><span data-stu-id="390ca-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="390ca-130">DefaultTTL 遺漏/不 hello 集合上設定</span><span class="sxs-lookup"><span data-stu-id="390ca-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="390ca-131">集合上的 DefaultTTL = -1</span><span class="sxs-lookup"><span data-stu-id="390ca-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="390ca-132">集合上的 DefaultTTL = "n"</span><span class="sxs-lookup"><span data-stu-id="390ca-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="390ca-133">集合上遺漏 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-133">TTL Missing on document</span></span> |<span data-ttu-id="390ca-134">執行任何動作 toooverride 由於 hello 文件和集合有沒有 TTL 的概念文件層級。</span><span class="sxs-lookup"><span data-stu-id="390ca-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="390ca-135">此集合中的所有文件都不會過期。</span><span class="sxs-lookup"><span data-stu-id="390ca-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="390ca-136">在此集合中的 hello 文件將到期間隔 n 耗盡時。</span><span class="sxs-lookup"><span data-stu-id="390ca-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="390ca-137">文件上的 TTL = -1</span><span class="sxs-lookup"><span data-stu-id="390ca-137">TTL = -1 on document</span></span> |<span data-ttu-id="390ca-138">不在 hello 文件層級不會定義 hello 集合，因為 toooverride hello DefaultTTL 屬性可以覆寫文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="390ca-139">文件上的 TTL 是 hello 系統未解譯的。</span><span class="sxs-lookup"><span data-stu-id="390ca-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="390ca-140">此集合中的所有文件都不會過期。</span><span class="sxs-lookup"><span data-stu-id="390ca-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="390ca-141">永遠不會過期 TTL = 1 這個集合中的 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="390ca-142">所有其他文件將在 "n" 間隔之後過期。</span><span class="sxs-lookup"><span data-stu-id="390ca-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="390ca-143">文件上的 TTL = n</span><span class="sxs-lookup"><span data-stu-id="390ca-143">TTL = n on document</span></span> |<span data-ttu-id="390ca-144">執行任何動作 toooverride hello 文件層級。</span><span class="sxs-lookup"><span data-stu-id="390ca-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="390ca-145">中的文件的 TTL hello 系統未解譯。</span><span class="sxs-lookup"><span data-stu-id="390ca-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="390ca-146">hello 文件，ttl = n 試用期間隔 n，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="390ca-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="390ca-147">其他文件會繼承間隔 -1 且永遠不會過期。</span><span class="sxs-lookup"><span data-stu-id="390ca-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="390ca-148">hello 文件，ttl = n 試用期間隔 n，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="390ca-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="390ca-149">其他文件會繼承 hello 集合"n"間隔。</span><span class="sxs-lookup"><span data-stu-id="390ca-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="390ca-150">設定 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-150">Configuring TTL</span></span>
<span data-ttu-id="390ca-151">根據預設，時間 toolive 已停用根據預設，所有的 Cosmos DB 集合中，並在所有文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="390ca-152">啟用 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-152">Enabling TTL</span></span>
<span data-ttu-id="390ca-153">tooenable TTL 集合或集合中的 hello 文件上，您需要 tooset hello DefaultTTL 集合 tooeither-1 或屬性的非零的正數值。</span><span class="sxs-lookup"><span data-stu-id="390ca-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="390ca-154">設定 hello DefaultTTL 太-1 表示預設 hello 集合中的所有文件永遠會存留，但 hello Cosmos DB 服務應該監視的文件已覆寫此預設值，這個集合。</span><span class="sxs-lookup"><span data-stu-id="390ca-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="390ca-155">在集合上設定預設 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="390ca-156">您有可以 tooconfigure 預設時間 toolive 集合層級。</span><span class="sxs-lookup"><span data-stu-id="390ca-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="390ca-157">tooset hello TTL 集合，您需要 tooprovide 非零的正數值，指出 hello 期間 （秒），tooexpire hello 集合中的所有文件之後 hello 上次修改時間戳記的 hello 文件 (`_ts`)。</span><span class="sxs-lookup"><span data-stu-id="390ca-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="390ca-158">或者，您可以設定 hello 預設太-1，這表示預設 live 插入 toohello 集合中的所有文件會無限期。</span><span class="sxs-lookup"><span data-stu-id="390ca-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="390ca-159">在文件上設定 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-159">Setting TTL on a document</span></span>
<span data-ttu-id="390ca-160">此外 toosetting 集合上的預設 TTL 您可以設定特定的 TTL 文件層級。</span><span class="sxs-lookup"><span data-stu-id="390ca-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="390ca-161">如此一來，將會覆寫 hello 預設值為 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="390ca-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="390ca-162">tooset hello TTL 文件中，您需要的 tooprovide 非零的正數值表示 hello 時間，以秒為單位，tooexpire hello 文件之後 hello 上次修改時間戳記的 hello 文件 (`_ts`)。</span><span class="sxs-lookup"><span data-stu-id="390ca-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="390ca-163">如果文件不有任何 [TTL] 欄位中，然後 hello hello 集合的預設會套用。</span><span class="sxs-lookup"><span data-stu-id="390ca-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="390ca-164">Hello 集合層級，TTL 已停用，直到 TTL hello 集合上再次啟用為止，將會忽略 hello 文件上的 hello TTL 欄位。</span><span class="sxs-lookup"><span data-stu-id="390ca-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="390ca-165">以下是程式碼片段顯示如何 tooset hello TTL 到期，文件上：</span><span class="sxs-lookup"><span data-stu-id="390ca-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="390ca-166">在現有文件上延長 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="390ca-167">您可以執行 hello 文件上的任何寫入作業，以重設文件上的 hello TTL。</span><span class="sxs-lookup"><span data-stu-id="390ca-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="390ca-168">執行此動作將設定 hello `_ts` toohello 目前的時間，hello 倒數計時 toohello 文件及到期時，所設定的 hello `ttl`，再重新開始。</span><span class="sxs-lookup"><span data-stu-id="390ca-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="390ca-169">如果您想 toochange hello`ttl`的文件，您可以更新 hello 欄位一樣可以與任何其他可設定的欄位。</span><span class="sxs-lookup"><span data-stu-id="390ca-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="390ca-170">從文件移除 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-170">Removing TTL from a document</span></span>
<span data-ttu-id="390ca-171">如果已設定的 TTL 文件上，您不再需要該文件 tooexpire，然後您可以擷取 hello 文件移除 hello TTL 欄位，取代 hello hello 伺服器上的文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="390ca-172">當從 hello 文件移除 hello TTL 欄位時，將會套用 hello 預設值為 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="390ca-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="390ca-173">toostop 文件不會過期，不會繼承 hello 集合則需要 tooset hello TTL 值太-1。</span><span class="sxs-lookup"><span data-stu-id="390ca-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="390ca-174">停用 TTL</span><span class="sxs-lookup"><span data-stu-id="390ca-174">Disabling TTL</span></span>
<span data-ttu-id="390ca-175">toodisable TTL 完全在集合，然後停止 hello 背景處理從尋找 hello DefaultTTL hello 集合屬性應該刪除過期的文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="390ca-176">刪除此屬性是不同於將它設定為太-1。</span><span class="sxs-lookup"><span data-stu-id="390ca-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="390ca-177">將新的文件設定太-1 表示新增 toohello 集合應永遠，但您可以在 hello 集合中特定文件上覆寫此。</span><span class="sxs-lookup"><span data-stu-id="390ca-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="390ca-178">Hello 集合中完全移除這個屬性表示的會到期的文件，即使已明確覆寫先前的預設值的文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="390ca-179">常見問題集</span><span class="sxs-lookup"><span data-stu-id="390ca-179">FAQ</span></span>
<span data-ttu-id="390ca-180">**TTL 的費用為何？**</span><span class="sxs-lookup"><span data-stu-id="390ca-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="390ca-181">沒有任何額外的成本 toosetting 文件上的 TTL。</span><span class="sxs-lookup"><span data-stu-id="390ca-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="390ca-182">**多久需要 toodelete 我的文件後已啟動的 hello TTL？**</span><span class="sxs-lookup"><span data-stu-id="390ca-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="390ca-183">hello TTL 已啟動，且將無法再存取透過 CRUD 或查詢 Api 之後，立即過期 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="390ca-184">**文件上的 TTL 是否會對 RU 費用造成任何影響？**</span><span class="sxs-lookup"><span data-stu-id="390ca-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="390ca-185">否，在 Cosmos DB 中透過 TTL 刪除過期的文件將不會影響 RU 費用。</span><span class="sxs-lookup"><span data-stu-id="390ca-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="390ca-186">**沒有 hello TTL 功能僅適用於 tooentire 文件，或可以後到期的個別文件屬性的值？**</span><span class="sxs-lookup"><span data-stu-id="390ca-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="390ca-187">TTL 適用於 toohello 整份文件。</span><span class="sxs-lookup"><span data-stu-id="390ca-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="390ca-188">如果您想要 tooexpire 部分文件，則建議您從 hello tooa 個別的 「 連結 」 文件中的主要文件擷取 hello 部分，，然後使用該擷取的文件上的 TTL。</span><span class="sxs-lookup"><span data-stu-id="390ca-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="390ca-189">**Hello TTL 功能是否有任何特定索引的需求？**</span><span class="sxs-lookup"><span data-stu-id="390ca-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="390ca-190">是。</span><span class="sxs-lookup"><span data-stu-id="390ca-190">Yes.</span></span> <span data-ttu-id="390ca-191">hello 集合必須有[編製索引原則集](indexing-policies.md)tooeither 一致或 Lazy。</span><span class="sxs-lookup"><span data-stu-id="390ca-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="390ca-192">嘗試 tooset DefaultTTL 集合具有索引組 tooNone 上的會發生錯誤時，將會嘗試 tooturn 關閉具有 DefaultTTL，已設定的集合上的索引。</span><span class="sxs-lookup"><span data-stu-id="390ca-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="390ca-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="390ca-193">Next steps</span></span>
<span data-ttu-id="390ca-194">深入了解 Azure Cosmos DB toolearn 參考 toohello 服務[*文件*](https://azure.microsoft.com/documentation/services/cosmos-db/)頁面。</span><span class="sxs-lookup"><span data-stu-id="390ca-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

