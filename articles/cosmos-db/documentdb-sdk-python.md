---
title: "Azure Cosmos DB Python API、SDK 和資源 | Microsoft Docs"
description: "了解所有 Python API 和 SDK 相關資訊，包括 發行日期、停用日期及 Azure Cosmos DB Python SDK 每個版本之間所做的變更。"
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="c5b10-103">Azure Cosmos DB Python SDK︰版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="c5b10-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5b10-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c5b10-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="c5b10-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="c5b10-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="c5b10-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c5b10-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="c5b10-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c5b10-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="c5b10-108">Java</span><span class="sxs-lookup"><span data-stu-id="c5b10-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="c5b10-109">Python</span><span class="sxs-lookup"><span data-stu-id="c5b10-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="c5b10-110">REST</span><span class="sxs-lookup"><span data-stu-id="c5b10-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="c5b10-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="c5b10-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="c5b10-112">SQL</span><span class="sxs-lookup"><span data-stu-id="c5b10-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="c5b10-113">**下載 SDK**</span><span class="sxs-lookup"><span data-stu-id="c5b10-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="c5b10-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="c5b10-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="c5b10-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="c5b10-115">**API documentation**</span></span></td><td>[<span data-ttu-id="c5b10-116">Python API 參考文件</span><span class="sxs-lookup"><span data-stu-id="c5b10-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="c5b10-117">**SDK 安裝指示**</span><span class="sxs-lookup"><span data-stu-id="c5b10-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="c5b10-118">SDK 安裝指示</span><span class="sxs-lookup"><span data-stu-id="c5b10-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="c5b10-119">**參與 SDK**</span><span class="sxs-lookup"><span data-stu-id="c5b10-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="c5b10-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="c5b10-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="c5b10-121">**開始使用**</span><span class="sxs-lookup"><span data-stu-id="c5b10-121">**Get started**</span></span></td><td>[<span data-ttu-id="c5b10-122">開始使用 Python SDK</span><span class="sxs-lookup"><span data-stu-id="c5b10-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="c5b10-123">**目前支援的平台**</span><span class="sxs-lookup"><span data-stu-id="c5b10-123">**Current supported platform**</span></span></td><td><span data-ttu-id="c5b10-124">[Python 2.7](https://www.python.org/downloads/) 和 [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="c5b10-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="c5b10-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="c5b10-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="c5b10-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="c5b10-127">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="c5b10-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="c5b10-129">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="c5b10-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="c5b10-130">新增針對 Cosmos DB 模擬器執行時停用 SSL 驗證的選項。</span><span class="sxs-lookup"><span data-stu-id="c5b10-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="c5b10-131">移除相依要求模組必須為 2.10.0 的限制。</span><span class="sxs-lookup"><span data-stu-id="c5b10-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="c5b10-132">已將分割區集合的最小輸送量從 10,100 RU/s 降低為 2500 RU/s。</span><span class="sxs-lookup"><span data-stu-id="c5b10-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="c5b10-133">在預存程序執行期間，加入支援指令碼記錄功能。</span><span class="sxs-lookup"><span data-stu-id="c5b10-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="c5b10-134">REST API 版本在此版本中提升至 '2017-01-19'。</span><span class="sxs-lookup"><span data-stu-id="c5b10-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="c5b10-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="c5b10-136">對文件註解進行編輯性的變更。</span><span class="sxs-lookup"><span data-stu-id="c5b10-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="c5b10-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="c5b10-138">新增 Python 3.5 的支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="c5b10-139">新增使用要求模組的連接集區支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="c5b10-140">新增工作階段一致性的支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-140">Added support for session consistency.</span></span>
* <span data-ttu-id="c5b10-141">新增對已分割集合的 TOP/ORDERBY 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="c5b10-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="c5b10-143">新加入已節流處理要求的重試原則支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="c5b10-144">(已節流處理的要求會收到要求率太大的例外狀況，即錯誤碼 429。)根據預設，發生錯誤碼 429 時，Azure Cosmos DB 會遵守回應標頭中的 retryAfter 時間，並針對每個要求重試九次。</span><span class="sxs-lookup"><span data-stu-id="c5b10-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="c5b10-145">如果您想要忽略伺服器在多次重試之間傳回的 retryAfter 時間，現在可以在 ConnectionPolicy 物件上的 RetryOptions 屬性中設定固定的重試間隔時間。</span><span class="sxs-lookup"><span data-stu-id="c5b10-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="c5b10-146">Azure Cosmos DB 現在會針對每個要進行節流處理的要求等候最多 30 秒 (不論重試計數為何)，並傳回包含錯誤碼 429 的回應。</span><span class="sxs-lookup"><span data-stu-id="c5b10-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="c5b10-147">您也可以在 ConnectionPolicy 物件上的 RetryOptions 屬性中覆寫該時間。</span><span class="sxs-lookup"><span data-stu-id="c5b10-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="c5b10-148">Cosmos DB 現在會傳回 x-ms-throttle-retry-count 和 x-ms-throttle-retry-wait-time-ms 做為每個要求的回應標頭，其代表節流重試計數和要求歷經多次重試的累積時間。</span><span class="sxs-lookup"><span data-stu-id="c5b10-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="c5b10-149">移除 RetryPolicy 類別和 document_client 類別上公開的對應屬性 (retry_policy)，改為引進公開 ConnectionPolicy 類別上的 RetryOptions 屬性，它可以用來覆寫某些預設的重試選項。</span><span class="sxs-lookup"><span data-stu-id="c5b10-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="c5b10-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="c5b10-151">新增對多重區域資料庫帳戶的支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="c5b10-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="c5b10-153">新加入文件的存留時間 (TTL) 功能支援。</span><span class="sxs-lookup"><span data-stu-id="c5b10-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="c5b10-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="c5b10-155">伺服器端資料分割相關錯誤修正，允許在 partitionkey 路徑中使用特殊字元。</span><span class="sxs-lookup"><span data-stu-id="c5b10-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="c5b10-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="c5b10-157">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="c5b10-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="c5b10-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="c5b10-159">新增「雜湊和範圍」分割區解析程式來協助將應用程式跨多個分割區分區。</span><span class="sxs-lookup"><span data-stu-id="c5b10-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="c5b10-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="c5b10-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="c5b10-161">實作 Upsert。</span><span class="sxs-lookup"><span data-stu-id="c5b10-161">Implement Upsert.</span></span> <span data-ttu-id="c5b10-162">已新增新的 UpsertXXX 方法以支援 Upsert 功能。</span><span class="sxs-lookup"><span data-stu-id="c5b10-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="c5b10-163">實作以識別碼為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="c5b10-163">Implement ID Based Routing.</span></span> <span data-ttu-id="c5b10-164">不需變更公用 API，所有變更皆為內部變更。</span><span class="sxs-lookup"><span data-stu-id="c5b10-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="c5b10-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="c5b10-166">支援地理空間索引。</span><span class="sxs-lookup"><span data-stu-id="c5b10-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="c5b10-167">驗證所有資源的識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="c5b10-167">Validates id property for all resources.</span></span> <span data-ttu-id="c5b10-168">資源的識別碼不能包含 ?、/、#、\, 字元，或以空格作為結尾。</span><span class="sxs-lookup"><span data-stu-id="c5b10-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="c5b10-169">將新標頭「索引轉換進度」加至 ResourceResponse。</span><span class="sxs-lookup"><span data-stu-id="c5b10-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="c5b10-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="c5b10-171">實作 V2 索引原則。</span><span class="sxs-lookup"><span data-stu-id="c5b10-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="c5b10-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="c5b10-173">支援 Proxy 連線。</span><span class="sxs-lookup"><span data-stu-id="c5b10-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="c5b10-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="c5b10-175">GA SDK。</span><span class="sxs-lookup"><span data-stu-id="c5b10-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="c5b10-176">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="c5b10-176">Release & retirement dates</span></span>
<span data-ttu-id="c5b10-177">Microsoft 至少會在停用 SDK 的 **12 個月** 之前提供通知，以供順利轉換至較新/支援的版本。</span><span class="sxs-lookup"><span data-stu-id="c5b10-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="c5b10-178">新的功能與最佳化項目只會新增至目前的 SDK，因此建議您一律盡早升級至最新的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="c5b10-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="c5b10-179">服務將會拒絕使用已停用 SDK 的任何 Cosmos DB 要求。</span><span class="sxs-lookup"><span data-stu-id="c5b10-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="c5b10-180">適用於 Python 之所有 **1.0.0** 之前的 Azure DocumentDB SDK 版本都將於 **2016 年 2 月 29 日**停用。</span><span class="sxs-lookup"><span data-stu-id="c5b10-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="c5b10-181">版本</span><span class="sxs-lookup"><span data-stu-id="c5b10-181">Version</span></span> | <span data-ttu-id="c5b10-182">發行日期</span><span class="sxs-lookup"><span data-stu-id="c5b10-182">Release Date</span></span> | <span data-ttu-id="c5b10-183">停用日期</span><span class="sxs-lookup"><span data-stu-id="c5b10-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c5b10-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="c5b10-185">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="c5b10-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="c5b10-187">2017 年 5 月 1 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="c5b10-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="c5b10-189">2016 年 10 月 30 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="c5b10-191">2016 年 9 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="c5b10-193">2016 年 7 月 7 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="c5b10-195">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="c5b10-197">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="c5b10-199">2016 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="c5b10-201">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="c5b10-203">2016 年 1 月 3 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="c5b10-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="c5b10-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="c5b10-205">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="c5b10-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="c5b10-207">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="c5b10-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="c5b10-209">2015 年 8 月 6 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="c5b10-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="c5b10-211">2015 年 7 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="c5b10-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="c5b10-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="c5b10-213">2015 年 5 月 25 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="c5b10-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c5b10-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="c5b10-215">2015 年 4 月 7 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="c5b10-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="c5b10-216">0.9.4-prelease</span></span> |<span data-ttu-id="c5b10-217">2015 年 1 月 14 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-217">January 14, 2015</span></span> |<span data-ttu-id="c5b10-218">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-218">February 29, 2016</span></span> |
| <span data-ttu-id="c5b10-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="c5b10-219">0.9.3-prelease</span></span> |<span data-ttu-id="c5b10-220">2014 年 12 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-220">December 09, 2014</span></span> |<span data-ttu-id="c5b10-221">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-221">February 29, 2016</span></span> |
| <span data-ttu-id="c5b10-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="c5b10-222">0.9.2-prelease</span></span> |<span data-ttu-id="c5b10-223">2014 年 11 月 25 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-223">November 25, 2014</span></span> |<span data-ttu-id="c5b10-224">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-224">February 29, 2016</span></span> |
| <span data-ttu-id="c5b10-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="c5b10-225">0.9.1-prelease</span></span> |<span data-ttu-id="c5b10-226">2014 年 9 月 23 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-226">September 23, 2014</span></span> |<span data-ttu-id="c5b10-227">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-227">February 29, 2016</span></span> |
| <span data-ttu-id="c5b10-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="c5b10-228">0.9.0-prelease</span></span> |<span data-ttu-id="c5b10-229">2014 年 8 月 21 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-229">August 21, 2014</span></span> |<span data-ttu-id="c5b10-230">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c5b10-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="c5b10-231">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c5b10-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="c5b10-232">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c5b10-232">See also</span></span>
<span data-ttu-id="c5b10-233">若要深入了解 Cosmos DB，請參閱 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="c5b10-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

