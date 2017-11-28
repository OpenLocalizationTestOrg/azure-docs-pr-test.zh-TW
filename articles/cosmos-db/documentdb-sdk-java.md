---
title: "Azure Cosmos DB：DocumentDB Java API、SDK 和資源 | Microsoft Docs"
description: "了解 hello Java API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB DocumentDB Java SDK 的每個版本之間所做的變更。"
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
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="f7276-103">Azure Cosmos DB：DocumentDB Java SDK 版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="f7276-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7276-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f7276-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="f7276-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="f7276-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="f7276-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f7276-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="f7276-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f7276-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="f7276-108">Java</span><span class="sxs-lookup"><span data-stu-id="f7276-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="f7276-109">Python</span><span class="sxs-lookup"><span data-stu-id="f7276-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="f7276-110">REST</span><span class="sxs-lookup"><span data-stu-id="f7276-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="f7276-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="f7276-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="f7276-112">SQL</span><span class="sxs-lookup"><span data-stu-id="f7276-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="f7276-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="f7276-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="f7276-114">Maven</span><span class="sxs-lookup"><span data-stu-id="f7276-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="f7276-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="f7276-115">**API documentation**</span></span></td><td>[<span data-ttu-id="f7276-116">Java API 參考文件</span><span class="sxs-lookup"><span data-stu-id="f7276-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="f7276-117">**參與 tooSDK**</span><span class="sxs-lookup"><span data-stu-id="f7276-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="f7276-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="f7276-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="f7276-119">**快速入門**</span><span class="sxs-lookup"><span data-stu-id="f7276-119">**Get started**</span></span></td><td>[<span data-ttu-id="f7276-120">開始使用 hello Java SDK</span><span class="sxs-lookup"><span data-stu-id="f7276-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="f7276-121">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="f7276-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="f7276-122">使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="f7276-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="f7276-123">**目前支援的執行階段**</span><span class="sxs-lookup"><span data-stu-id="f7276-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="f7276-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="f7276-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="f7276-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="f7276-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="f7276-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="f7276-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="f7276-127">在資料分割期間處理的重大錯誤修正 toorequest 分割。</span><span class="sxs-lookup"><span data-stu-id="f7276-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="f7276-128">已修正的問題，以強式 hello 和 BoundedStaleness 一致性層級。</span><span class="sxs-lookup"><span data-stu-id="f7276-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="f7276-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="f7276-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="f7276-130">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="f7276-131">已修正工作階段模式中讀取集合的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7276-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="f7276-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="f7276-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="f7276-133">已啟用對低至 2,500 RU/秒且以 100 RU/秒遞增量進行調整之資料分割集合的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="f7276-134">這可能導致 NullRef 例外狀況，在某些查詢中的 hello 原生組件中修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="f7276-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="f7276-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="f7276-136">在 hello 查詢引擎組態閘道模式可能會造成例外狀況的查詢中修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="f7276-137">修正 hello 可能會導致 「 找不到擁有者資源 」 的例外狀況要求在集合建立後立即的工作階段容器中的幾個 bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="f7276-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="f7276-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="f7276-139">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="f7276-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="f7276-140">請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。</span><span class="sxs-lookup"><span data-stu-id="f7276-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="f7276-141">新增變更摘要的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-141">Added support for change feed.</span></span>
* <span data-ttu-id="f7276-142">新增透過 RequestOptions.setPopulateQuotaInfo 收集配額資訊的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="f7276-143">新增透過 RequestOptions.setScriptLoggingEnabled 進行預存程序指令碼記錄的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="f7276-144">修正發生節流閥失敗時，DirectHttps 模式的查詢可能會停止回應的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7276-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="f7276-145">修正工作階段一致性模式中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7276-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="f7276-146">修正當要求率過高時，可能在 HttpContext 中造成 NullReferenceException 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7276-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="f7276-147">改善 DirectHttps 模式的效能。</span><span class="sxs-lookup"><span data-stu-id="f7276-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="f7276-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="f7276-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="f7276-149">在 ConnectionPolicy.setProxy() API 加入簡單的用戶端執行個體 Proxy 支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="f7276-150">加入的 DocumentClient.close() API tooproperly 關閉 DocumentClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7276-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="f7276-151">在直接連線模式，而不是 hello 閘道的 hello 原生組件從類別衍生 hello 查詢計劃中的改進的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="f7276-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="f7276-152">設定 FAIL_ON_UNKNOWN_PROPERTIES = false，因此使用者不需要在其 POJO JsonIgnoreProperties toodefine。</span><span class="sxs-lookup"><span data-stu-id="f7276-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="f7276-153">重構記錄 toouse SLF4J。</span><span class="sxs-lookup"><span data-stu-id="f7276-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="f7276-154">修正一致性讀取器中的其他幾個 Bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="f7276-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="f7276-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="f7276-156">Hello 連接管理 tooprevent 連接中的流失直接連線模式中修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="f7276-157">修正的 bug hello 最上層查詢中，它可能會擲回 「 NullReferenece 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f7276-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="f7276-158">藉由減少 hello hello 內部快取的網路呼叫數目的提升的效能。</span><span class="sxs-lookup"><span data-stu-id="f7276-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="f7276-159">在 DocumentClientException 中的 ActivityID 和要求 URI 中加入狀態碼以協助疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f7276-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="f7276-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="f7276-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="f7276-161">穩定性 hello 連線的管理中修正的問題。</span><span class="sxs-lookup"><span data-stu-id="f7276-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="f7276-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="f7276-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="f7276-163">新增對 BoundedStaleness 一致性層級的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="f7276-164">新增對已分割集合之 CRUD 作業的直接連線支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="f7276-165">修正以 SQL 查詢資料庫時發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7276-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="f7276-166">Hello，工作階段權杖可能未正確設定的工作階段快取中修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="f7276-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="f7276-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="f7276-168">新增對跨資料分割平行查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="f7276-169">新增對已分割集合的 TOP/ORDER BY 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="f7276-170">新增對強式一致性的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="f7276-171">新增對使用直接連線時之名稱型要求的支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="f7276-172">固定的 toomake ActivityId 保持一致所有要求重試次數。</span><span class="sxs-lookup"><span data-stu-id="f7276-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="f7276-173">修正的 bug 時重新建立 hello 與集合相關 toohello 工作階段快取相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="f7276-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="f7276-174">新增為異地隔離空間查詢指定集合索引編製原則時的 Polygon 和 LineString 資料類型。</span><span class="sxs-lookup"><span data-stu-id="f7276-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="f7276-175">修正適用於 Java 1.8 之 Java Doc 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f7276-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="f7276-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="f7276-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="f7276-177">PartitionKeyDefinitionMap 中修正的 bug toocache 單一分割區集合並不進行額外提取資料分割索引鍵的要求。</span><span class="sxs-lookup"><span data-stu-id="f7276-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="f7276-178">提供不正確的資料分割索引鍵值時，請修正 bug toonot 重試。</span><span class="sxs-lookup"><span data-stu-id="f7276-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="f7276-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="f7276-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="f7276-180">加入的 hello 支援多重地區資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7276-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="f7276-181">新增的支援選項 toocustomize hello max 節流的要求上的自動重試重試次數和最大值重試等候時間。</span><span class="sxs-lookup"><span data-stu-id="f7276-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="f7276-182">請參閱 RetryOptions 和 ConnectionPolicy.getRetryOptions()。</span><span class="sxs-lookup"><span data-stu-id="f7276-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="f7276-183">已淘汰以 IPartitionResolver 為基礎的自訂分割程式碼。</span><span class="sxs-lookup"><span data-stu-id="f7276-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="f7276-184">請針對更高的儲存體和輸送量使用分割集合。</span><span class="sxs-lookup"><span data-stu-id="f7276-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="f7276-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="f7276-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="f7276-186">新加入節流的重試原則支援。</span><span class="sxs-lookup"><span data-stu-id="f7276-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="f7276-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="f7276-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="f7276-188">加入時間 toolive (TTL) 支援的文件。</span><span class="sxs-lookup"><span data-stu-id="f7276-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="f7276-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="f7276-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="f7276-190">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="f7276-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="f7276-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="f7276-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="f7276-192">HashPartitionResolver toogenerate 雜湊值和其他 Sdk 一致由小到大 toobe 中修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="f7276-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="f7276-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="f7276-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="f7276-194">將雜湊和範圍加入資料分割的解析程式 tooassist 與跨多個資料分割的分區化應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7276-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="f7276-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="f7276-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="f7276-196">實作 Upsert。</span><span class="sxs-lookup"><span data-stu-id="f7276-196">Implement Upsert.</span></span> <span data-ttu-id="f7276-197">新的 upsertXXX 方法加入 toosupport Upsert 功能。</span><span class="sxs-lookup"><span data-stu-id="f7276-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="f7276-198">實作以識別碼為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="f7276-198">Implement ID Based Routing.</span></span> <span data-ttu-id="f7276-199">不需變更公用 API，所有變更皆為內部變更。</span><span class="sxs-lookup"><span data-stu-id="f7276-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="f7276-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="f7276-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="f7276-201">發行已略過 toobring 對齊方式，與其他 Sdk 版本號碼</span><span class="sxs-lookup"><span data-stu-id="f7276-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="f7276-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="f7276-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="f7276-203">支援地理空間索引</span><span class="sxs-lookup"><span data-stu-id="f7276-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="f7276-204">驗證所有資源的識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="f7276-204">Validates id property for all resources.</span></span> <span data-ttu-id="f7276-205">資源的識別碼不能包含 ?、/、#、\, 字元，或以空格作為結尾。</span><span class="sxs-lookup"><span data-stu-id="f7276-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="f7276-206">加入新的標頭 「 索引轉換進行 」 tooResourceResponse。</span><span class="sxs-lookup"><span data-stu-id="f7276-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="f7276-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="f7276-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="f7276-208">實作 V2 索引原則</span><span class="sxs-lookup"><span data-stu-id="f7276-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="f7276-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="f7276-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="f7276-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="f7276-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="f7276-211">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="f7276-211">Release & Retirement Dates</span></span>
<span data-ttu-id="f7276-212">Microsoft 提供通知的最少**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。</span><span class="sxs-lookup"><span data-stu-id="f7276-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="f7276-213">新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議，您一律升級 toohello 最新版本 SDK 盡早。</span><span class="sxs-lookup"><span data-stu-id="f7276-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="f7276-214">Hello 服務，將會拒絕任何要求 tooCosmos 使用已停用的 SDK 的 DB。</span><span class="sxs-lookup"><span data-stu-id="f7276-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="f7276-215">所有版本的 hello DocumentDB SDK for Java 先前 tooversion **1.0.0**將會遭到淘汰**2016 年 2 月 29 日**。</span><span class="sxs-lookup"><span data-stu-id="f7276-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="f7276-216">版本</span><span class="sxs-lookup"><span data-stu-id="f7276-216">Version</span></span> | <span data-ttu-id="f7276-217">發行日期</span><span class="sxs-lookup"><span data-stu-id="f7276-217">Release Date</span></span> | <span data-ttu-id="f7276-218">停用日期</span><span class="sxs-lookup"><span data-stu-id="f7276-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="f7276-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="f7276-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="f7276-220">2017 年 7 月 11 日</span><span class="sxs-lookup"><span data-stu-id="f7276-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="f7276-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="f7276-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="f7276-222">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="f7276-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="f7276-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="f7276-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="f7276-224">2017 年 3 月 11 日</span><span class="sxs-lookup"><span data-stu-id="f7276-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="f7276-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="f7276-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="f7276-226">2017 年 2 月 21 日</span><span class="sxs-lookup"><span data-stu-id="f7276-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="f7276-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="f7276-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="f7276-228">2017 年 1 月 31 日</span><span class="sxs-lookup"><span data-stu-id="f7276-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="f7276-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="f7276-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="f7276-230">2016 年 11 月24 日</span><span class="sxs-lookup"><span data-stu-id="f7276-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="f7276-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="f7276-232">2016 年 10 月 30 日</span><span class="sxs-lookup"><span data-stu-id="f7276-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="f7276-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="f7276-234">2016 年 10 月 28 日</span><span class="sxs-lookup"><span data-stu-id="f7276-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="f7276-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="f7276-236">2016 年 10 月 26 日</span><span class="sxs-lookup"><span data-stu-id="f7276-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="f7276-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="f7276-238">2016 年 10 月 3 日</span><span class="sxs-lookup"><span data-stu-id="f7276-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="f7276-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="f7276-240">2016 年 6 月 30 日</span><span class="sxs-lookup"><span data-stu-id="f7276-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="f7276-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="f7276-242">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="f7276-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="f7276-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="f7276-244">2016 年 4 月 30 日</span><span class="sxs-lookup"><span data-stu-id="f7276-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="f7276-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="f7276-246">2016 年 4 月 27 日</span><span class="sxs-lookup"><span data-stu-id="f7276-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="f7276-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="f7276-248">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="f7276-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="f7276-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="f7276-250">2015 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="f7276-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="f7276-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="f7276-252">2015 年 12 月 4 日</span><span class="sxs-lookup"><span data-stu-id="f7276-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="f7276-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="f7276-254">2015 年 10 月 5 日</span><span class="sxs-lookup"><span data-stu-id="f7276-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="f7276-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="f7276-256">2015 年 10 月 5 日</span><span class="sxs-lookup"><span data-stu-id="f7276-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="f7276-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="f7276-258">2015 年 8 月 5 日</span><span class="sxs-lookup"><span data-stu-id="f7276-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="f7276-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="f7276-260">2015 年 7 月 9 日</span><span class="sxs-lookup"><span data-stu-id="f7276-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="f7276-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="f7276-262">2015 年 5 月 12 日</span><span class="sxs-lookup"><span data-stu-id="f7276-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="f7276-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f7276-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="f7276-264">2015 年 4 月 7 日</span><span class="sxs-lookup"><span data-stu-id="f7276-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="f7276-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="f7276-265">0.9.5-prelease</span></span> |<span data-ttu-id="f7276-266">2015 年 3 月 9 日</span><span class="sxs-lookup"><span data-stu-id="f7276-266">Mar 09, 2015</span></span> |<span data-ttu-id="f7276-267">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-267">February 29, 2016</span></span> |
| <span data-ttu-id="f7276-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="f7276-268">0.9.4-prelease</span></span> |<span data-ttu-id="f7276-269">2015 年 2 月 17 日</span><span class="sxs-lookup"><span data-stu-id="f7276-269">February 17, 2015</span></span> |<span data-ttu-id="f7276-270">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-270">February 29, 2016</span></span> |
| <span data-ttu-id="f7276-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="f7276-271">0.9.3-prelease</span></span> |<span data-ttu-id="f7276-272">2015 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="f7276-272">January 13, 2015</span></span> |<span data-ttu-id="f7276-273">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-273">February 29, 2016</span></span> |
| <span data-ttu-id="f7276-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="f7276-274">0.9.2-prelease</span></span> |<span data-ttu-id="f7276-275">2014 年 12 月 19 日</span><span class="sxs-lookup"><span data-stu-id="f7276-275">December 19, 2014</span></span> |<span data-ttu-id="f7276-276">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-276">February 29, 2016</span></span> |
| <span data-ttu-id="f7276-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="f7276-277">0.9.1-prelease</span></span> |<span data-ttu-id="f7276-278">2014 年 12 月 19 日</span><span class="sxs-lookup"><span data-stu-id="f7276-278">December 19, 2014</span></span> |<span data-ttu-id="f7276-279">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-279">February 29, 2016</span></span> |
| <span data-ttu-id="f7276-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="f7276-280">0.9.0-prelease</span></span> |<span data-ttu-id="f7276-281">2014 年 12 月 10日</span><span class="sxs-lookup"><span data-stu-id="f7276-281">December 10, 2014</span></span> |<span data-ttu-id="f7276-282">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="f7276-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="f7276-283">常見問題集</span><span class="sxs-lookup"><span data-stu-id="f7276-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="f7276-284">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f7276-284">See Also</span></span>
<span data-ttu-id="f7276-285">請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。</span><span class="sxs-lookup"><span data-stu-id="f7276-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

