---
title: "aaaAzure Cosmos DB Node.js 應用程式開發介面，SDK 與資源 |Microsoft 文件"
description: "了解 hello Node.js API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB Node.js SDK 的每個版本之間所做的變更。"
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="c7d50-103">Azure Cosmos DB Node.js SDK︰版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="c7d50-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7d50-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c7d50-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="c7d50-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="c7d50-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="c7d50-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c7d50-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="c7d50-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c7d50-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="c7d50-108">Java</span><span class="sxs-lookup"><span data-stu-id="c7d50-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="c7d50-109">Python</span><span class="sxs-lookup"><span data-stu-id="c7d50-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="c7d50-110">REST</span><span class="sxs-lookup"><span data-stu-id="c7d50-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="c7d50-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="c7d50-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="c7d50-112">SQL</span><span class="sxs-lookup"><span data-stu-id="c7d50-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="c7d50-113">**下載 SDK**</span><span class="sxs-lookup"><span data-stu-id="c7d50-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="c7d50-114">NPM</span><span class="sxs-lookup"><span data-stu-id="c7d50-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="c7d50-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="c7d50-115">**API documentation**</span></span></td><td>[<span data-ttu-id="c7d50-116">Node.js API 參考文件</span><span class="sxs-lookup"><span data-stu-id="c7d50-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="c7d50-117">**SDK 安裝指示**</span><span class="sxs-lookup"><span data-stu-id="c7d50-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="c7d50-118">安裝指示</span><span class="sxs-lookup"><span data-stu-id="c7d50-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="c7d50-119">**參與 tooSDK**</span><span class="sxs-lookup"><span data-stu-id="c7d50-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="c7d50-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="c7d50-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="c7d50-121">**範例**</span><span class="sxs-lookup"><span data-stu-id="c7d50-121">**Samples**</span></span></td><td>[<span data-ttu-id="c7d50-122">Node.js 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c7d50-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="c7d50-123">**開始使用教學課程**</span><span class="sxs-lookup"><span data-stu-id="c7d50-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="c7d50-124">開始使用 hello Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="c7d50-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="c7d50-125">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="c7d50-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="c7d50-126">使用 Azure Cosmos DB 來建置 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7d50-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="c7d50-127">**目前支援的平台**</span><span class="sxs-lookup"><span data-stu-id="c7d50-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="c7d50-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="c7d50-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="c7d50-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="c7d50-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="c7d50-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="c7d50-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="c7d50-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="c7d50-132">版本資訊</span><span class="sxs-lookup"><span data-stu-id="c7d50-132">Release notes</span></span>

### <span data-ttu-id="c7d50-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="c7d50-134">修正的 npm 文件。</span><span class="sxs-lookup"><span data-stu-id="c7d50-134">npm documentation fixed.</span></span>

### <span data-ttu-id="c7d50-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="c7d50-136">已修正 executeStoredProcedure 中的錯誤，其中涉及的文件有特殊 Unicode 字元 (LS、PS)。</span><span class="sxs-lookup"><span data-stu-id="c7d50-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="c7d50-137">修正的 bug，在處理文件以 hello 資料分割索引鍵中的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="c7d50-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="c7d50-138">支援固定的 hello 名稱媒體建立集合。</span><span class="sxs-lookup"><span data-stu-id="c7d50-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="c7d50-139">GitHub 問題 #114。</span><span class="sxs-lookup"><span data-stu-id="c7d50-139">Github issue #114.</span></span>
* <span data-ttu-id="c7d50-140">已修正權限授權權杖的支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="c7d50-141">GitHub 問題 #178。</span><span class="sxs-lookup"><span data-stu-id="c7d50-141">Github issue #178.</span></span>

### <span data-ttu-id="c7d50-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="c7d50-143">新增對新[一致性層級](consistency-levels.md) ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="c7d50-144">新增 UriFactory 的支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="c7d50-145">已修正 Unicode 支援錯誤。</span><span class="sxs-lookup"><span data-stu-id="c7d50-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="c7d50-146">GitHub 問題 #171。</span><span class="sxs-lookup"><span data-stu-id="c7d50-146">GitHub issue #171.</span></span>

### <span data-ttu-id="c7d50-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="c7d50-148">加入的 hello 支援彙總查詢 （計數、 MIN、 MAX、 SUM 和 AVG）。</span><span class="sxs-lookup"><span data-stu-id="c7d50-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="c7d50-149">加入的 hello 選項控制的跨資料分割的查詢平行處理原則程度。</span><span class="sxs-lookup"><span data-stu-id="c7d50-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="c7d50-150">停用 SSL 驗證對 Azure Cosmos DB 模擬器執行時加入的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="c7d50-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="c7d50-151">降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。</span><span class="sxs-lookup"><span data-stu-id="c7d50-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="c7d50-152">固定的 hello 接續 token 的 bug 單一資料分割集合。</span><span class="sxs-lookup"><span data-stu-id="c7d50-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="c7d50-153">GitHub 問題 #107。</span><span class="sxs-lookup"><span data-stu-id="c7d50-153">Github issue #107.</span></span>
* <span data-ttu-id="c7d50-154">在處理單一參數為 0 的固定的 hello executeStoredProcedure bug。</span><span class="sxs-lookup"><span data-stu-id="c7d50-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="c7d50-155">GitHub 問題 #155。</span><span class="sxs-lookup"><span data-stu-id="c7d50-155">Github issue #155.</span></span>

### <span data-ttu-id="c7d50-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="c7d50-157">固定的使用者代理程式標頭 tooinclude hello SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="c7d50-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="c7d50-158">次要程式碼清除。</span><span class="sxs-lookup"><span data-stu-id="c7d50-158">Minor code cleanup.</span></span>

### <span data-ttu-id="c7d50-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="c7d50-160">使用 hello SDK tootarget hello emulator(hostname=localhost) 時，請停用 SSL 驗證。</span><span class="sxs-lookup"><span data-stu-id="c7d50-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="c7d50-161">在預存程序執行期間，加入支援指令碼記錄功能。</span><span class="sxs-lookup"><span data-stu-id="c7d50-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="c7d50-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="c7d50-163">新增對跨資料分割平行查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="c7d50-164">新增對已分割集合的 TOP/ORDER BY 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="c7d50-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="c7d50-166">新加入已節流處理要求的重試原則支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="c7d50-167">(已節流處理的要求會收到要求率太大的例外狀況，即錯誤碼 429。)根據預設，Azure Cosmos DB 重試 9 次針對每個要求時遇到錯誤碼 429，接受 hello 回應標頭中的 hello retryAfter 時間。</span><span class="sxs-lookup"><span data-stu-id="c7d50-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="c7d50-168">固定的重試間隔時間現在可以設定為 hello RetryOptions 屬性一部分 hello ConnectionPolicy 物件上如果您想要 tooignore hello retryAfter 時間伺服器傳回的 hello 重試之間。</span><span class="sxs-lookup"><span data-stu-id="c7d50-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="c7d50-169">Azure Cosmos DB 現在會等候 30 秒 （不論是重試計數） 正在進行節流，並傳回錯誤碼 429 hello 回應的每個要求的最大值。</span><span class="sxs-lookup"><span data-stu-id="c7d50-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="c7d50-170">此時也會覆寫 hello RetryOptions ConnectionPolicy 物件上的屬性中。</span><span class="sxs-lookup"><span data-stu-id="c7d50-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="c7d50-171">Cosmos DB 現在傳回 x ms-節流閥-重試的計數和 x-ms-throttle-retry-wait-time-ms hello 回應標頭中每個要求 toodenote hello 節流重試計數和 hello 累計時間 hello 要求 hello 重試之間等候。</span><span class="sxs-lookup"><span data-stu-id="c7d50-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="c7d50-172">已新增 hello RetryOptions 類別，公開 hello RetryOptions 屬性可以使用的 toooverride hello ConnectionPolicy 類別上某些 hello 預設重試選項。</span><span class="sxs-lookup"><span data-stu-id="c7d50-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="c7d50-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="c7d50-174">加入的 hello 支援多重地區資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="c7d50-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="c7d50-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="c7d50-176">加入的 hello 支援時間 tooLive(TTL) 功能的文件。</span><span class="sxs-lookup"><span data-stu-id="c7d50-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="c7d50-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="c7d50-178">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="c7d50-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="c7d50-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="c7d50-180">修正的 RangePartitionResolver.resolveForRead bug 其中它未傳回 tooa 不正確的串連結果的到期的連結。</span><span class="sxs-lookup"><span data-stu-id="c7d50-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="c7d50-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="c7d50-182">修正 hashParitionResolver resolveForRead()：所提供的資料分割索引鍵都未擲回例外狀況時，而不會傳回所有已註冊連結的清單。</span><span class="sxs-lookup"><span data-stu-id="c7d50-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="c7d50-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="c7d50-184">修正問題[#100](https://github.com/Azure/azure-documentdb-node/issues/100) -專用 HTTPS 代理程式： 避免修改 Azure Cosmos DB 基於 hello 通用的代理程式。</span><span class="sxs-lookup"><span data-stu-id="c7d50-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="c7d50-185">所有的 hello lib 要求使用專用的代理程式。</span><span class="sxs-lookup"><span data-stu-id="c7d50-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="c7d50-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="c7d50-187">修正問題 [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - 正確處理媒體識別碼中的連字號。</span><span class="sxs-lookup"><span data-stu-id="c7d50-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="c7d50-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="c7d50-189">修正問題 [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter 接聽程式洩漏警告。</span><span class="sxs-lookup"><span data-stu-id="c7d50-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="c7d50-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="c7d50-191">修正問題[#92](https://github.com/Azure/azure-documentdb-node/issues/90) -重新命名資料夾雜湊 toohash 區分大小寫的系統。</span><span class="sxs-lookup"><span data-stu-id="c7d50-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="c7d50-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="c7d50-193">藉由新增雜湊和範圍分割解析程式來實作分區化支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="c7d50-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="c7d50-195">實作 Upsert。</span><span class="sxs-lookup"><span data-stu-id="c7d50-195">Implement Upsert.</span></span> <span data-ttu-id="c7d50-196">documentClient 上新的 upsertXXX 方法。</span><span class="sxs-lookup"><span data-stu-id="c7d50-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="c7d50-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="c7d50-198">略過 toobring 對齊方式，與其他 Sdk 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="c7d50-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="c7d50-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="c7d50-200">分割 Q 承諾包裝函式 toonew 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c7d50-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="c7d50-201">更新 toopackage npm 登錄檔案。</span><span class="sxs-lookup"><span data-stu-id="c7d50-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="c7d50-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="c7d50-203">實作以識別碼為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="c7d50-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="c7d50-204">修正問題 [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - 目前屬性與 current() 方法衝突。</span><span class="sxs-lookup"><span data-stu-id="c7d50-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="c7d50-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="c7d50-206">新增對地理空間索引的支援。</span><span class="sxs-lookup"><span data-stu-id="c7d50-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="c7d50-207">驗證所有資源的識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="c7d50-207">Validates id property for all resources.</span></span> <span data-ttu-id="c7d50-208">資源的識別碼不能包含 ?、/、#、&#47;&#47; 等字元，或在結尾處使用空格。</span><span class="sxs-lookup"><span data-stu-id="c7d50-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="c7d50-209">加入新的標頭 「 索引轉換進行 」 tooResourceResponse。</span><span class="sxs-lookup"><span data-stu-id="c7d50-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="c7d50-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="c7d50-211">實作 V2 索引原則。</span><span class="sxs-lookup"><span data-stu-id="c7d50-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="c7d50-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="c7d50-213">問題[#40](https://github.com/Azure/azure-documentdb-node/issues/40) -實作 eslint grunt hello 核心中的組態和保證 SDK。</span><span class="sxs-lookup"><span data-stu-id="c7d50-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="c7d50-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="c7d50-215">問題 [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promise 包裝函式不包括標頭並發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="c7d50-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="c7d50-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="c7d50-217">藉由加入 readConflicts、 readConflictAsync 和 queryConflicts 能力 tooquery 衝突。</span><span class="sxs-lookup"><span data-stu-id="c7d50-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="c7d50-218">已更新 API 文件。</span><span class="sxs-lookup"><span data-stu-id="c7d50-218">Updated API documentation.</span></span>
* <span data-ttu-id="c7d50-219">問題 [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync 錯誤。</span><span class="sxs-lookup"><span data-stu-id="c7d50-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="c7d50-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="c7d50-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="c7d50-221">GA SDK。</span><span class="sxs-lookup"><span data-stu-id="c7d50-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="c7d50-222">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="c7d50-222">Release & Retirement Dates</span></span>
<span data-ttu-id="c7d50-223">Microsoft 至少提供通知**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。</span><span class="sxs-lookup"><span data-stu-id="c7d50-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="c7d50-224">新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議您，您一律升級 toohello 最新版本 SDK 盡早。</span><span class="sxs-lookup"><span data-stu-id="c7d50-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="c7d50-225">使用已停用的 SDK 的 DB tooCosmos 是任何要求被拒絕 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="c7d50-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="c7d50-226">版本</span><span class="sxs-lookup"><span data-stu-id="c7d50-226">Version</span></span> | <span data-ttu-id="c7d50-227">發行日期</span><span class="sxs-lookup"><span data-stu-id="c7d50-227">Release Date</span></span> | <span data-ttu-id="c7d50-228">停用日期</span><span class="sxs-lookup"><span data-stu-id="c7d50-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c7d50-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="c7d50-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="c7d50-230">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="c7d50-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="c7d50-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="c7d50-232">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="c7d50-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="c7d50-234">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="c7d50-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="c7d50-236">2017 年 3 月 16 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="c7d50-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="c7d50-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="c7d50-238">2017 年 1 月 27 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="c7d50-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="c7d50-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="c7d50-240">2016 年 12 月 22 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="c7d50-242">2016 年 10 月 3 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="c7d50-244">2016 年 7 月 7 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="c7d50-246">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="c7d50-248">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="c7d50-250">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="c7d50-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="c7d50-252">2016 年 3 月 8 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="c7d50-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="c7d50-254">2016 年 2 月 2 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="c7d50-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="c7d50-256">2016 年 2 月 1 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="c7d50-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="c7d50-258">2016 年 1 月 26 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="c7d50-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="c7d50-260">2016 年 1 月 22 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="c7d50-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="c7d50-262">2016 年 1 月 4 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="c7d50-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="c7d50-264">2015 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="c7d50-266">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="c7d50-268">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="c7d50-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="c7d50-270">2015 年 9 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="c7d50-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="c7d50-272">2015 年 8 月 15 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="c7d50-274">2015 年 8 月 5 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="c7d50-276">2015 年 7 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="c7d50-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="c7d50-278">2015 年 6 月 4 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="c7d50-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="c7d50-280">2015 年 5 月 23 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="c7d50-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="c7d50-282">2015 年 5 月 15 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="c7d50-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c7d50-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="c7d50-284">2015 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="c7d50-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="c7d50-285">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c7d50-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="c7d50-286">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c7d50-286">See also</span></span>
<span data-ttu-id="c7d50-287">請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。</span><span class="sxs-lookup"><span data-stu-id="c7d50-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

