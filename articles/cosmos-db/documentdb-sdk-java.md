---
title: "Azure Cosmos DB：DocumentDB Java API、SDK 和資源 | Microsoft Docs"
description: "了解所有 Java API 和 SDK 相關資訊，包括發行日期、停用日期及 Azure Cosmos DB DocumentDB Java SDK 每個版本之間所做的變更。"
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="c37f2-103">Azure Cosmos DB：DocumentDB Java SDK 版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="c37f2-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c37f2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c37f2-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="c37f2-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="c37f2-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="c37f2-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c37f2-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="c37f2-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c37f2-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="c37f2-108">Java</span><span class="sxs-lookup"><span data-stu-id="c37f2-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="c37f2-109">Python</span><span class="sxs-lookup"><span data-stu-id="c37f2-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="c37f2-110">REST</span><span class="sxs-lookup"><span data-stu-id="c37f2-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="c37f2-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="c37f2-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="c37f2-112">SQL</span><span class="sxs-lookup"><span data-stu-id="c37f2-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="c37f2-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="c37f2-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="c37f2-114">Maven</span><span class="sxs-lookup"><span data-stu-id="c37f2-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="c37f2-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="c37f2-115">**API documentation**</span></span></td><td>[<span data-ttu-id="c37f2-116">Java API 參考文件</span><span class="sxs-lookup"><span data-stu-id="c37f2-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="c37f2-117">**參與 SDK**</span><span class="sxs-lookup"><span data-stu-id="c37f2-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="c37f2-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="c37f2-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="c37f2-119">**開始使用**</span><span class="sxs-lookup"><span data-stu-id="c37f2-119">**Get started**</span></span></td><td>[<span data-ttu-id="c37f2-120">開始使用 Java SDK</span><span class="sxs-lookup"><span data-stu-id="c37f2-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="c37f2-121">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="c37f2-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="c37f2-122">使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="c37f2-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="c37f2-123">**目前支援的執行階段**</span><span class="sxs-lookup"><span data-stu-id="c37f2-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="c37f2-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="c37f2-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="c37f2-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="c37f2-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="c37f2-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="c37f2-127">重大錯誤修正，要求在分割區分割期間處理。</span><span class="sxs-lookup"><span data-stu-id="c37f2-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="c37f2-128">已利用 Strong 和 BoundedStaleness 一致性層級修正問題。</span><span class="sxs-lookup"><span data-stu-id="c37f2-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="c37f2-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="c37f2-130">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="c37f2-131">已修正工作階段模式中讀取集合的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="c37f2-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="c37f2-133">已啟用對低至 2,500 RU/秒且以 100 RU/秒遞增量進行調整之資料分割集合的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="c37f2-134">已修正原生組件中的 Bug，這會在某些查詢中導致 NullRef 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c37f2-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="c37f2-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="c37f2-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="c37f2-136">修正查詢引擎組態中可能對閘道模式中的查詢造成例外狀況的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="c37f2-137">修正工作階段容器中可能在集合建立後立即對要求造成「找不到擁有者資源」例外狀況的幾個錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="c37f2-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="c37f2-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="c37f2-139">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="c37f2-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="c37f2-140">請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。</span><span class="sxs-lookup"><span data-stu-id="c37f2-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="c37f2-141">新增變更摘要的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-141">Added support for change feed.</span></span>
* <span data-ttu-id="c37f2-142">新增透過 RequestOptions.setPopulateQuotaInfo 收集配額資訊的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="c37f2-143">新增透過 RequestOptions.setScriptLoggingEnabled 進行預存程序指令碼記錄的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="c37f2-144">修正發生節流閥失敗時，DirectHttps 模式的查詢可能會停止回應的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="c37f2-145">修正工作階段一致性模式中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="c37f2-146">修正當要求率過高時，可能在 HttpContext 中造成 NullReferenceException 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="c37f2-147">改善 DirectHttps 模式的效能。</span><span class="sxs-lookup"><span data-stu-id="c37f2-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="c37f2-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="c37f2-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="c37f2-149">在 ConnectionPolicy.setProxy() API 加入簡單的用戶端執行個體 Proxy 支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="c37f2-150">加入的 DocumentClient.close() API 可正確關閉 DocumentClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c37f2-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="c37f2-151">從原生組件 (而不是從閘道) 衍生的查詢計劃利用直接連線模式改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="c37f2-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="c37f2-152">設定 FAIL_ON_UNKNOWN_PROPERTIES = false，讓使用者不需要在其 POJO 定義 JsonIgnoreProperties。</span><span class="sxs-lookup"><span data-stu-id="c37f2-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="c37f2-153">重新建構記錄使用 SLF4J。</span><span class="sxs-lookup"><span data-stu-id="c37f2-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="c37f2-154">修正一致性讀取器中的其他幾個 Bug。</span><span class="sxs-lookup"><span data-stu-id="c37f2-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="c37f2-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="c37f2-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="c37f2-156">修正連線管理中的 Bug，避免連線在直接連線模式中流失。</span><span class="sxs-lookup"><span data-stu-id="c37f2-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="c37f2-157">修正排名最前的查詢中可能會擲回 NullReferenece 例外狀況的 Bug。</span><span class="sxs-lookup"><span data-stu-id="c37f2-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="c37f2-158">透過減少內部快取的網路呼叫數來增進效能。</span><span class="sxs-lookup"><span data-stu-id="c37f2-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="c37f2-159">在 DocumentClientException 中的 ActivityID 和要求 URI 中加入狀態碼以協助疑難排解。</span><span class="sxs-lookup"><span data-stu-id="c37f2-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="c37f2-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="c37f2-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="c37f2-161">修正連線管理中的問題以提供穩定性。</span><span class="sxs-lookup"><span data-stu-id="c37f2-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="c37f2-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="c37f2-163">新增對 BoundedStaleness 一致性層級的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="c37f2-164">新增對已分割集合之 CRUD 作業的直接連線支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="c37f2-165">修正以 SQL 查詢資料庫時發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="c37f2-166">修正工作階段權杖設定不正確之工作階段快取中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="c37f2-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="c37f2-168">新增對跨資料分割平行查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="c37f2-169">新增對已分割集合的 TOP/ORDER BY 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="c37f2-170">新增對強式一致性的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="c37f2-171">新增對使用直接連線時之名稱型要求的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="c37f2-172">修正以使得 ActivityId 在所有要求重試之間保持一致。</span><span class="sxs-lookup"><span data-stu-id="c37f2-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="c37f2-173">修正與以相同名稱重新建立集合時之工作階段快取相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="c37f2-174">新增為異地隔離空間查詢指定集合索引編製原則時的 Polygon 和 LineString 資料類型。</span><span class="sxs-lookup"><span data-stu-id="c37f2-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="c37f2-175">修正適用於 Java 1.8 之 Java Doc 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="c37f2-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="c37f2-177">修正 PartitionKeyDefinitionMap 中將單一資料分割集合加入快取，而非提出額外擷取資料分割索引鍵要求的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="c37f2-178">修正在提供不正確的資料分割索引鍵時不重試的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c37f2-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="c37f2-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="c37f2-180">新增對多重區域資料庫帳戶的支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="c37f2-181">新增在已節流處理的要求上自動重試的支援，方法是提供選項來自訂重試次數上限和等待時間上限。</span><span class="sxs-lookup"><span data-stu-id="c37f2-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="c37f2-182">請參閱 RetryOptions 和 ConnectionPolicy.getRetryOptions()。</span><span class="sxs-lookup"><span data-stu-id="c37f2-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="c37f2-183">已淘汰以 IPartitionResolver 為基礎的自訂分割程式碼。</span><span class="sxs-lookup"><span data-stu-id="c37f2-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="c37f2-184">請針對更高的儲存體和輸送量使用分割集合。</span><span class="sxs-lookup"><span data-stu-id="c37f2-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="c37f2-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="c37f2-186">新加入節流的重試原則支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="c37f2-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="c37f2-188">新加入文件的存留時間 (TTL) 支援。</span><span class="sxs-lookup"><span data-stu-id="c37f2-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="c37f2-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="c37f2-190">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="c37f2-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="c37f2-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="c37f2-192">修正 HashPartitionResolver 中的錯誤以產生與其他 SDK 一致的 little-endian 雜湊值。</span><span class="sxs-lookup"><span data-stu-id="c37f2-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="c37f2-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="c37f2-194">新增「雜湊和範圍」分割區解析程式來協助將應用程式跨多個分割區分區。</span><span class="sxs-lookup"><span data-stu-id="c37f2-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="c37f2-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="c37f2-196">實作 Upsert。</span><span class="sxs-lookup"><span data-stu-id="c37f2-196">Implement Upsert.</span></span> <span data-ttu-id="c37f2-197">已新增新的 upsertXXX 方法以支援 Upsert 功能。</span><span class="sxs-lookup"><span data-stu-id="c37f2-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="c37f2-198">實作以識別碼為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="c37f2-198">Implement ID Based Routing.</span></span> <span data-ttu-id="c37f2-199">不需變更公用 API，所有變更皆為內部變更。</span><span class="sxs-lookup"><span data-stu-id="c37f2-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="c37f2-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="c37f2-201">已略過版本以配合其他 SDK 的版本號碼</span><span class="sxs-lookup"><span data-stu-id="c37f2-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="c37f2-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="c37f2-203">支援地理空間索引</span><span class="sxs-lookup"><span data-stu-id="c37f2-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="c37f2-204">驗證所有資源的識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="c37f2-204">Validates id property for all resources.</span></span> <span data-ttu-id="c37f2-205">資源的識別碼不能包含 ?、/、#、\, 字元，或以空格作為結尾。</span><span class="sxs-lookup"><span data-stu-id="c37f2-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="c37f2-206">將新標頭「索引轉換進度」加至 ResourceResponse。</span><span class="sxs-lookup"><span data-stu-id="c37f2-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="c37f2-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="c37f2-208">實作 V2 索引原則</span><span class="sxs-lookup"><span data-stu-id="c37f2-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="c37f2-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="c37f2-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="c37f2-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="c37f2-211">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="c37f2-211">Release & Retirement Dates</span></span>
<span data-ttu-id="c37f2-212">Microsoft 至少會在停用 SDK 的 **12 個月** 之前提供通知，以供順利轉換至較新/支援的版本。</span><span class="sxs-lookup"><span data-stu-id="c37f2-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="c37f2-213">新的功能與最佳化項目只會新增至目前的 SDK，因此建議您一律盡早升級至最新的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="c37f2-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="c37f2-214">服務將會拒絕使用已停用 SDK 的任何 Cosmos DB 要求。</span><span class="sxs-lookup"><span data-stu-id="c37f2-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="c37f2-215">所有 **1.0.0** 版之前的 DocumentDB SDK for Java 版本都將於 **2016 年 2 月 29 日**淘汰。</span><span class="sxs-lookup"><span data-stu-id="c37f2-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="c37f2-216">版本</span><span class="sxs-lookup"><span data-stu-id="c37f2-216">Version</span></span> | <span data-ttu-id="c37f2-217">發行日期</span><span class="sxs-lookup"><span data-stu-id="c37f2-217">Release Date</span></span> | <span data-ttu-id="c37f2-218">停用日期</span><span class="sxs-lookup"><span data-stu-id="c37f2-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c37f2-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="c37f2-220">2017 年 7 月 11 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="c37f2-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="c37f2-222">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="c37f2-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="c37f2-224">2017 年 3 月 11 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="c37f2-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="c37f2-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="c37f2-226">2017 年 2 月 21 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="c37f2-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="c37f2-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="c37f2-228">2017 年 1 月 31 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="c37f2-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="c37f2-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="c37f2-230">2016 年 11 月24 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="c37f2-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="c37f2-232">2016 年 10 月 30 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="c37f2-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="c37f2-234">2016 年 10 月 28 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="c37f2-236">2016 年 10 月 26 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="c37f2-238">2016 年 10 月 3 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="c37f2-240">2016 年 6 月 30 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="c37f2-242">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="c37f2-244">2016 年 4 月 30 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="c37f2-246">2016 年 4 月 27 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="c37f2-248">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="c37f2-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="c37f2-250">2015 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="c37f2-252">2015 年 12 月 4 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="c37f2-254">2015 年 10 月 5 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="c37f2-256">2015 年 10 月 5 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="c37f2-258">2015 年 8 月 5 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="c37f2-260">2015 年 7 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="c37f2-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="c37f2-262">2015 年 5 月 12 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="c37f2-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c37f2-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="c37f2-264">2015 年 4 月 7 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="c37f2-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="c37f2-265">0.9.5-prelease</span></span> |<span data-ttu-id="c37f2-266">2015 年 3 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-266">Mar 09, 2015</span></span> |<span data-ttu-id="c37f2-267">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-267">February 29, 2016</span></span> |
| <span data-ttu-id="c37f2-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="c37f2-268">0.9.4-prelease</span></span> |<span data-ttu-id="c37f2-269">2015 年 2 月 17 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-269">February 17, 2015</span></span> |<span data-ttu-id="c37f2-270">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-270">February 29, 2016</span></span> |
| <span data-ttu-id="c37f2-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="c37f2-271">0.9.3-prelease</span></span> |<span data-ttu-id="c37f2-272">2015 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-272">January 13, 2015</span></span> |<span data-ttu-id="c37f2-273">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-273">February 29, 2016</span></span> |
| <span data-ttu-id="c37f2-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="c37f2-274">0.9.2-prelease</span></span> |<span data-ttu-id="c37f2-275">2014 年 12 月 19 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-275">December 19, 2014</span></span> |<span data-ttu-id="c37f2-276">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-276">February 29, 2016</span></span> |
| <span data-ttu-id="c37f2-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="c37f2-277">0.9.1-prelease</span></span> |<span data-ttu-id="c37f2-278">2014 年 12 月 19 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-278">December 19, 2014</span></span> |<span data-ttu-id="c37f2-279">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-279">February 29, 2016</span></span> |
| <span data-ttu-id="c37f2-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="c37f2-280">0.9.0-prelease</span></span> |<span data-ttu-id="c37f2-281">2014 年 12 月 10日</span><span class="sxs-lookup"><span data-stu-id="c37f2-281">December 10, 2014</span></span> |<span data-ttu-id="c37f2-282">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c37f2-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="c37f2-283">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c37f2-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="c37f2-284">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c37f2-284">See Also</span></span>
<span data-ttu-id="c37f2-285">若要深入了解 Cosmos DB，請參閱 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="c37f2-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

