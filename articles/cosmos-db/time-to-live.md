---
title: "利用存留時間讓 Azure Cosmos DB 中的資料過期 | Microsoft Docs"
description: "Microsoft Azure Cosmos DB 可讓您利用 TTL 在一段時間後自動從系統清除文件。"
services: cosmos-db
documentationcenter: 
keywords: "存留時間"
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
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="fe1c7-104">利用存留時間讓 Azure Cosmos DB 集合中的資料自動過期</span><span class="sxs-lookup"><span data-stu-id="fe1c7-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="fe1c7-105">應用程式可以產生並儲存大量資料。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="fe1c7-106">其中有些資料，例如電腦產生的事件資料、記錄檔和使用者工作階段資訊只能在有限的期間內使用。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="fe1c7-107">一旦資料超過應用程式的需求，即可放心清除此資料並減少應用程式的儲存體需求。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="fe1c7-108">Microsoft Azure Cosmos DB 可讓您利用「存留時間」(或稱 TTL) 在一段時間後自動從資料庫清除文件。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="fe1c7-109">預設存留時間可以在集合層級設定，並且在每份文件上覆寫。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="fe1c7-110">設定 TTL (不論是作為集合預設值或是在文件層級設定) 之後，Cosmos DB 就會自動移除自上次修改後存在時間達該指定時間 (以秒為單位) 的文件。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="fe1c7-111">Cosmos DB 中的存留時間會使用上次修改文件時的對照時間位移。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="fe1c7-112">為了這麼做，它會使用每份文件上都有的 `_ts` 欄位。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="fe1c7-113">_ts 欄位是 unix 樣式的 Epoch 時間戳記，表示日期和時間。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="fe1c7-114">每次修改文件時都會更新 `_ts` 欄位。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="fe1c7-115">TTL 行為</span><span class="sxs-lookup"><span data-stu-id="fe1c7-115">TTL behavior</span></span>
<span data-ttu-id="fe1c7-116">TTL 功能是由兩個層級 (集合層級和文件層級) 的 TTL 屬性所控制。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="fe1c7-117">這些值會以秒為單位來設定，而且會視為與上次修改文件時的 `_ts` 的差異。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="fe1c7-118">集合的 DefaultTTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="fe1c7-119">如果遺失 (或設為 null)，便不會自動刪除文件。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="fe1c7-120">如果存在且值為 "-1" = 無限 – 文件預設不會過期</span><span class="sxs-lookup"><span data-stu-id="fe1c7-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="fe1c7-121">如果存在且值是某個數字 ("n") – 文件會在上次修改後的 "n" 秒到期</span><span class="sxs-lookup"><span data-stu-id="fe1c7-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="fe1c7-122">文件的 TTL︰</span><span class="sxs-lookup"><span data-stu-id="fe1c7-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="fe1c7-123">僅在父集合有 DefaultTTL 時，才適用屬性。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="fe1c7-124">覆寫父集合的 DefaultTTL 值。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="fe1c7-125">文件一過期 (`ttl` + `_ts` >= 目前的伺服器時間)，就會標示為「已過期」。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="fe1c7-126">在此時間之後，不允許在這些文件上執行任何作業，而且將會從任何執行的查詢結果中排除。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="fe1c7-127">這些文件會在系統中遭到實體刪除，而稍後在背景中伺機刪除。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="fe1c7-128">這不會耗用集合預算中的任何 [要求單位 (RU)](request-units.md) 。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="fe1c7-129">上述邏輯可以顯示在下列矩陣中︰</span><span class="sxs-lookup"><span data-stu-id="fe1c7-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="fe1c7-130">集合上遺漏/未設定 DefaultTTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="fe1c7-131">集合上的 DefaultTTL = -1</span><span class="sxs-lookup"><span data-stu-id="fe1c7-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="fe1c7-132">集合上的 DefaultTTL = "n"</span><span class="sxs-lookup"><span data-stu-id="fe1c7-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="fe1c7-133">集合上遺漏 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-133">TTL Missing on document</span></span> |<span data-ttu-id="fe1c7-134">文件層級沒有可覆寫的項目，因為文件和集合沒有 TTL 的概念。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="fe1c7-135">此集合中的所有文件都不會過期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="fe1c7-136">此集合中的文件將會在間隔 n 過去時到期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="fe1c7-137">文件上的 TTL = -1</span><span class="sxs-lookup"><span data-stu-id="fe1c7-137">TTL = -1 on document</span></span> |<span data-ttu-id="fe1c7-138">文件層級沒有可覆寫的項目，因為集合未定義文件可以覆寫的 DefaultTTL 屬性。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="fe1c7-139">系統無法解譯文件上的 TTL。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="fe1c7-140">此集合中的所有文件都不會過期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="fe1c7-141">此集合中 TTL=-1 的文件永遠不會過期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="fe1c7-142">所有其他文件將在 "n" 間隔之後過期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="fe1c7-143">文件上的 TTL = n</span><span class="sxs-lookup"><span data-stu-id="fe1c7-143">TTL = n on document</span></span> |<span data-ttu-id="fe1c7-144">文件層級沒有可覆寫的項目。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-144">Nothing to override at the document level.</span></span> <span data-ttu-id="fe1c7-145">系統無法解譯文件上的 TTL。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="fe1c7-146">TTL = n 的文件將在間隔 n (以秒為單位) 之後到期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="fe1c7-147">其他文件會繼承間隔 -1 且永遠不會過期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="fe1c7-148">TTL = n 的文件將在間隔 n (以秒為單位) 之後到期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="fe1c7-149">其他文件會繼承集合的間隔 "n"。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="fe1c7-150">設定 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-150">Configuring TTL</span></span>
<span data-ttu-id="fe1c7-151">根據預設，在所有 Cosmos DB 集合中及所有文件上都會停用存留時間。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="fe1c7-152">啟用 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-152">Enabling TTL</span></span>
<span data-ttu-id="fe1c7-153">若要在集合上或集合內的文件上啟用 TTL，您需要將集合的 DefaultTTL 屬性設定為 -1 或非零的正數。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="fe1c7-154">將 DefaultTTL 設定為 -1，表示集合中的所有文件都預設為永遠存留，但 Cosmos DB 服務應監視此集合中已覆寫這個預設值的文件。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="fe1c7-155">在集合上設定預設 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="fe1c7-156">您可以在集合層級設定預設存留時間。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="fe1c7-157">若要在集合上設定 TTL，您必須提供一個非零的正數，指出集合中的所有文件在上次修改的時間戳記 (`_ts`) 之後要到期的期間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="fe1c7-158">或者，您可以將預設值設定為 -1，表示插入集合中的所有文件預設會無限期存留。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="fe1c7-159">在文件上設定 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-159">Setting TTL on a document</span></span>
<span data-ttu-id="fe1c7-160">除了在集合上設定預設 TTL，您可以在文件層級設定特定的 TTL。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="fe1c7-161">這麼做將會覆寫集合的預設值。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="fe1c7-162">若要在文件上設定 TTL，您必須提供一個非零的正數，指出文件在上次修改的時間戳記 (`_ts`) 之後要到期的期間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="fe1c7-163">如果文件沒有 TTL 欄位，則會套用集合的預設值。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="fe1c7-164">如果已在集合層級停用 TTL，則會忽略文件上的 TTL 欄位，直到在集合上重新啟用 TTL 為止。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="fe1c7-165">以下是說明如何在文件上設定 TTL 到期時間的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="fe1c7-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="fe1c7-166">在現有文件上延長 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="fe1c7-167">您可以在文件上進行任何寫入作業，以重設文件上的 TTL。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="fe1c7-168">這麼做會將 `_ts` 設定為目前的時間，並重新開始倒數文件的到期時間 (如 `ttl` 所設定)。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="fe1c7-169">如果您想要變更文件的 `ttl`，您可以如同處理任何其他可設定的欄位一樣更新此欄位。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="fe1c7-170">從文件移除 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-170">Removing TTL from a document</span></span>
<span data-ttu-id="fe1c7-171">如果文件上已設定 TTL，而您不再希望文件會到期，您可以擷取此文件、移除 TTL 欄位，然後取代伺服器上的文件。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="fe1c7-172">移除文件的 TTL 欄位後，將會套用集合的預設值。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="fe1c7-173">若要阻止文件到期且不要繼承集合的值，您必須將 TTL 值設定為 -1。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="fe1c7-174">停用 TTL</span><span class="sxs-lookup"><span data-stu-id="fe1c7-174">Disabling TTL</span></span>
<span data-ttu-id="fe1c7-175">若要在集合上完全停用 TTL 並阻止背景處理程序尋找過期的文件，則應刪除集合上的 DefaultTTL 屬性。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="fe1c7-176">刪除此屬性與將它設定為 -1 不同。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="fe1c7-177">設定為 -1，表示加入至集合的新文件會永遠存留，但是您可以在集合中的特定文件上覆寫此值。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="fe1c7-178">從集合中完全移除此屬性，表示即使有已明確覆寫先前預設值的文件，所有文件也都不會過期。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="fe1c7-179">常見問題集</span><span class="sxs-lookup"><span data-stu-id="fe1c7-179">FAQ</span></span>
<span data-ttu-id="fe1c7-180">**TTL 的費用為何？**</span><span class="sxs-lookup"><span data-stu-id="fe1c7-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="fe1c7-181">在文件上設定 TTL 不會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="fe1c7-182">**TTL 一旦到了，刪除我的文件要花多少時間？**</span><span class="sxs-lookup"><span data-stu-id="fe1c7-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="fe1c7-183">TTL 一旦到了，文件會立即到期，並將無法透過 CRUD 或查詢 API 存取。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="fe1c7-184">**文件上的 TTL 是否會對 RU 費用造成任何影響？**</span><span class="sxs-lookup"><span data-stu-id="fe1c7-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="fe1c7-185">否，在 Cosmos DB 中透過 TTL 刪除過期的文件將不會影響 RU 費用。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="fe1c7-186">**TTL 功能只會套用至整個文件，或者我可以讓個別的文件屬性值過期？**</span><span class="sxs-lookup"><span data-stu-id="fe1c7-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="fe1c7-187">TTL 會套用到整份文件。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-187">TTL applies to the entire document.</span></span> <span data-ttu-id="fe1c7-188">如果您只想要讓文件的一部分過期，建議您從主要文件中將該部分擷取到個別的「已連結」文件，然後在該擷取文件上使用 TTL。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="fe1c7-189">**TTL 功能是否有任何特定的編製索索引需求？**</span><span class="sxs-lookup"><span data-stu-id="fe1c7-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="fe1c7-190">是。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-190">Yes.</span></span> <span data-ttu-id="fe1c7-191">集合的[編製索引原則](indexing-policies.md)必須設定為 [延遲] 或 [一致]。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="fe1c7-192">嘗試在編製索引設為 [無] 的集合上設定 DefaultTTL 會造成錯誤，而嘗試在已設定 DefaultTTL 的集合上關閉索引編製也會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe1c7-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe1c7-193">Next steps</span></span>
<span data-ttu-id="fe1c7-194">若要深入了解 Azure Cosmos DB，請參閱服務的[*文件 (英文)*](https://azure.microsoft.com/documentation/services/cosmos-db/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="fe1c7-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

