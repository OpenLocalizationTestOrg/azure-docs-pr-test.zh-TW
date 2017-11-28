---
title: "aaaAzure Cosmos DB Python 應用程式開發介面，SDK 與資源 |Microsoft 文件"
description: "了解 hello Python API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB Python SDK 的每個版本之間所做的變更。"
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="beac7-103">Azure Cosmos DB Python SDK︰版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="beac7-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="beac7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="beac7-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="beac7-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="beac7-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="beac7-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="beac7-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="beac7-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="beac7-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="beac7-108">Java</span><span class="sxs-lookup"><span data-stu-id="beac7-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="beac7-109">Python</span><span class="sxs-lookup"><span data-stu-id="beac7-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="beac7-110">REST</span><span class="sxs-lookup"><span data-stu-id="beac7-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="beac7-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="beac7-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="beac7-112">SQL</span><span class="sxs-lookup"><span data-stu-id="beac7-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="beac7-113">**下載 SDK**</span><span class="sxs-lookup"><span data-stu-id="beac7-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="beac7-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="beac7-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="beac7-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="beac7-115">**API documentation**</span></span></td><td>[<span data-ttu-id="beac7-116">Python API 參考文件</span><span class="sxs-lookup"><span data-stu-id="beac7-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="beac7-117">**SDK 安裝指示**</span><span class="sxs-lookup"><span data-stu-id="beac7-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="beac7-118">SDK 安裝指示</span><span class="sxs-lookup"><span data-stu-id="beac7-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="beac7-119">**參與 tooSDK**</span><span class="sxs-lookup"><span data-stu-id="beac7-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="beac7-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="beac7-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="beac7-121">**快速入門**</span><span class="sxs-lookup"><span data-stu-id="beac7-121">**Get started**</span></span></td><td>[<span data-ttu-id="beac7-122">開始使用 Python SDK hello</span><span class="sxs-lookup"><span data-stu-id="beac7-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="beac7-123">**目前支援的平台**</span><span class="sxs-lookup"><span data-stu-id="beac7-123">**Current supported platform**</span></span></td><td><span data-ttu-id="beac7-124">[Python 2.7](https://www.python.org/downloads/) 和 [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="beac7-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="beac7-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="beac7-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="beac7-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="beac7-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="beac7-127">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="beac7-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="beac7-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="beac7-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="beac7-129">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="beac7-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="beac7-130">新增針對 Cosmos DB 模擬器執行時停用 SSL 驗證的選項。</span><span class="sxs-lookup"><span data-stu-id="beac7-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="beac7-131">移除相依要求模組 toobe 完全 2.10.0 hello 限制。</span><span class="sxs-lookup"><span data-stu-id="beac7-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="beac7-132">降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。</span><span class="sxs-lookup"><span data-stu-id="beac7-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="beac7-133">在預存程序執行期間，加入支援指令碼記錄功能。</span><span class="sxs-lookup"><span data-stu-id="beac7-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="beac7-134">REST API 版本太當 ' 2017年-01-19' 在此版本。</span><span class="sxs-lookup"><span data-stu-id="beac7-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="beac7-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="beac7-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="beac7-136">變更幅度 toodocumentation 註解。</span><span class="sxs-lookup"><span data-stu-id="beac7-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="beac7-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="beac7-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="beac7-138">新增 Python 3.5 的支援。</span><span class="sxs-lookup"><span data-stu-id="beac7-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="beac7-139">新增使用要求模組的連接集區支援。</span><span class="sxs-lookup"><span data-stu-id="beac7-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="beac7-140">新增工作階段一致性的支援。</span><span class="sxs-lookup"><span data-stu-id="beac7-140">Added support for session consistency.</span></span>
* <span data-ttu-id="beac7-141">新增對已分割集合的 TOP/ORDERBY 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="beac7-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="beac7-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="beac7-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="beac7-143">新加入已節流處理要求的重試原則支援。</span><span class="sxs-lookup"><span data-stu-id="beac7-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="beac7-144">(已節流處理的要求會收到要求率太大的例外狀況，即錯誤碼 429。)根據預設，Azure Cosmos DB 重試 9 次針對每個要求時遇到錯誤碼 429，接受 hello 回應標頭中的 hello retryAfter 時間。</span><span class="sxs-lookup"><span data-stu-id="beac7-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="beac7-145">固定的重試間隔時間現在可以設定為 hello RetryOptions 屬性一部分 hello ConnectionPolicy 物件上如果您想要 tooignore hello retryAfter 時間伺服器傳回的 hello 重試之間。</span><span class="sxs-lookup"><span data-stu-id="beac7-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="beac7-146">Azure Cosmos DB 現在會等候 30 秒 （不論是重試計數） 正在進行節流，並傳回錯誤碼 429 hello 回應的每個要求的最大值。</span><span class="sxs-lookup"><span data-stu-id="beac7-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="beac7-147">此時也可以在 hello RetryOptions 屬性 ConnectionPolicy 物件上的已覆寫。</span><span class="sxs-lookup"><span data-stu-id="beac7-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="beac7-148">Cosmos DB 現在傳回 x ms-節流閥-重試的計數和 x-ms-throttle-retry-wait-time-ms hello 回應標頭中每個要求 toodenote hello 節流重試計數和 hello cummulative 時間 hello 要求 hello 重試之間等候。</span><span class="sxs-lookup"><span data-stu-id="beac7-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="beac7-149">移除的 hello RetryPolicy 類別和 hello 對應屬性 (retry_policy) hello document_client 類別上公開，並且改為引進公開 hello RetryOptions 屬性可以使用的 toooverride ConnectionPolicy 類別上 RetryOptions 類別某些 hello 預設重試選項。</span><span class="sxs-lookup"><span data-stu-id="beac7-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="beac7-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="beac7-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="beac7-151">加入的 hello 支援多重地區資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="beac7-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="beac7-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="beac7-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="beac7-153">加入的 hello 支援時間 tooLive(TTL) 功能的文件。</span><span class="sxs-lookup"><span data-stu-id="beac7-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="beac7-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="beac7-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="beac7-155">Bug 修正相關 tooserver 端分割 tooallow partitionkey 路徑中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="beac7-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="beac7-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="beac7-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="beac7-157">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="beac7-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="beac7-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="beac7-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="beac7-159">將雜湊和範圍加入資料分割的解析程式 tooassist 與跨多個資料分割的分區化應用程式。</span><span class="sxs-lookup"><span data-stu-id="beac7-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="beac7-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="beac7-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="beac7-161">實作 Upsert。</span><span class="sxs-lookup"><span data-stu-id="beac7-161">Implement Upsert.</span></span> <span data-ttu-id="beac7-162">新的 UpsertXXX 方法加入 toosupport Upsert 功能。</span><span class="sxs-lookup"><span data-stu-id="beac7-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="beac7-163">實作以識別碼為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="beac7-163">Implement ID Based Routing.</span></span> <span data-ttu-id="beac7-164">不需變更公用 API，所有變更皆為內部變更。</span><span class="sxs-lookup"><span data-stu-id="beac7-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="beac7-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="beac7-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="beac7-166">支援地理空間索引。</span><span class="sxs-lookup"><span data-stu-id="beac7-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="beac7-167">驗證所有資源的識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="beac7-167">Validates id property for all resources.</span></span> <span data-ttu-id="beac7-168">資源的識別碼不能包含 ?、/、#、\, 字元，或以空格作為結尾。</span><span class="sxs-lookup"><span data-stu-id="beac7-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="beac7-169">加入新的標頭 「 索引轉換進行 」 tooResourceResponse。</span><span class="sxs-lookup"><span data-stu-id="beac7-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="beac7-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="beac7-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="beac7-171">實作 V2 索引原則。</span><span class="sxs-lookup"><span data-stu-id="beac7-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="beac7-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="beac7-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="beac7-173">支援 Proxy 連線。</span><span class="sxs-lookup"><span data-stu-id="beac7-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="beac7-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="beac7-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="beac7-175">GA SDK。</span><span class="sxs-lookup"><span data-stu-id="beac7-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="beac7-176">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="beac7-176">Release & retirement dates</span></span>
<span data-ttu-id="beac7-177">Microsoft 提供通知的最少**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。</span><span class="sxs-lookup"><span data-stu-id="beac7-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="beac7-178">新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議，您一律升級 toohello 最新版本 SDK 盡早。</span><span class="sxs-lookup"><span data-stu-id="beac7-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="beac7-179">Hello 服務，將會拒絕任何要求 tooCosmos 使用已停用的 SDK 的 DB。</span><span class="sxs-lookup"><span data-stu-id="beac7-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="beac7-180">所有版本的 hello Azure DocumentDB SDK for Python 先前 tooversion **1.0.0**將會遭到淘汰**2016 年 2 月 29 日**。</span><span class="sxs-lookup"><span data-stu-id="beac7-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="beac7-181">版本</span><span class="sxs-lookup"><span data-stu-id="beac7-181">Version</span></span> | <span data-ttu-id="beac7-182">發行日期</span><span class="sxs-lookup"><span data-stu-id="beac7-182">Release Date</span></span> | <span data-ttu-id="beac7-183">停用日期</span><span class="sxs-lookup"><span data-stu-id="beac7-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="beac7-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="beac7-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="beac7-185">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="beac7-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="beac7-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="beac7-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="beac7-187">2017 年 5 月 1 日</span><span class="sxs-lookup"><span data-stu-id="beac7-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="beac7-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="beac7-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="beac7-189">2016 年 10 月 30 日</span><span class="sxs-lookup"><span data-stu-id="beac7-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="beac7-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="beac7-191">2016 年 9 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="beac7-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="beac7-193">2016 年 7 月 7 日</span><span class="sxs-lookup"><span data-stu-id="beac7-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="beac7-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="beac7-195">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="beac7-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="beac7-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="beac7-197">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="beac7-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="beac7-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="beac7-199">2016 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="beac7-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="beac7-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="beac7-201">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="beac7-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="beac7-203">2016 年 1 月 3 日</span><span class="sxs-lookup"><span data-stu-id="beac7-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="beac7-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="beac7-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="beac7-205">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="beac7-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="beac7-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="beac7-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="beac7-207">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="beac7-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="beac7-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="beac7-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="beac7-209">2015 年 8 月 6 日</span><span class="sxs-lookup"><span data-stu-id="beac7-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="beac7-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="beac7-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="beac7-211">2015 年 7 月 9 日</span><span class="sxs-lookup"><span data-stu-id="beac7-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="beac7-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="beac7-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="beac7-213">2015 年 5 月 25 日</span><span class="sxs-lookup"><span data-stu-id="beac7-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="beac7-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="beac7-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="beac7-215">2015 年 4 月 7 日</span><span class="sxs-lookup"><span data-stu-id="beac7-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="beac7-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="beac7-216">0.9.4-prelease</span></span> |<span data-ttu-id="beac7-217">2015 年 1 月 14 日</span><span class="sxs-lookup"><span data-stu-id="beac7-217">January 14, 2015</span></span> |<span data-ttu-id="beac7-218">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-218">February 29, 2016</span></span> |
| <span data-ttu-id="beac7-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="beac7-219">0.9.3-prelease</span></span> |<span data-ttu-id="beac7-220">2014 年 12 月 9 日</span><span class="sxs-lookup"><span data-stu-id="beac7-220">December 09, 2014</span></span> |<span data-ttu-id="beac7-221">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-221">February 29, 2016</span></span> |
| <span data-ttu-id="beac7-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="beac7-222">0.9.2-prelease</span></span> |<span data-ttu-id="beac7-223">2014 年 11 月 25 日</span><span class="sxs-lookup"><span data-stu-id="beac7-223">November 25, 2014</span></span> |<span data-ttu-id="beac7-224">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-224">February 29, 2016</span></span> |
| <span data-ttu-id="beac7-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="beac7-225">0.9.1-prelease</span></span> |<span data-ttu-id="beac7-226">2014 年 9 月 23 日</span><span class="sxs-lookup"><span data-stu-id="beac7-226">September 23, 2014</span></span> |<span data-ttu-id="beac7-227">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-227">February 29, 2016</span></span> |
| <span data-ttu-id="beac7-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="beac7-228">0.9.0-prelease</span></span> |<span data-ttu-id="beac7-229">2014 年 8 月 21 日</span><span class="sxs-lookup"><span data-stu-id="beac7-229">August 21, 2014</span></span> |<span data-ttu-id="beac7-230">2016 年 2 月 29 日</span><span class="sxs-lookup"><span data-stu-id="beac7-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="beac7-231">常見問題集</span><span class="sxs-lookup"><span data-stu-id="beac7-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="beac7-232">另請參閱</span><span class="sxs-lookup"><span data-stu-id="beac7-232">See also</span></span>
<span data-ttu-id="beac7-233">請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。</span><span class="sxs-lookup"><span data-stu-id="beac7-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

