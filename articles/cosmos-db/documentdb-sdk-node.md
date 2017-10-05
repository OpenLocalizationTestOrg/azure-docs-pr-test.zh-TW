---
title: "Azure Cosmos DB Node.js API、SDK 和資源 | Microsoft Docs"
description: "了解所有 Node.js API 和 SDK 相關資訊，包括 發行日期、停用日期及 Azure Cosmos DB Node.js SDK 每個版本之間所做的變更。"
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
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="275c5-103">Azure Cosmos DB Node.js SDK︰版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="275c5-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="275c5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="275c5-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="275c5-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="275c5-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="275c5-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="275c5-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="275c5-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="275c5-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="275c5-108">Java</span><span class="sxs-lookup"><span data-stu-id="275c5-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="275c5-109">Python</span><span class="sxs-lookup"><span data-stu-id="275c5-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="275c5-110">REST</span><span class="sxs-lookup"><span data-stu-id="275c5-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="275c5-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="275c5-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="275c5-112">SQL</span><span class="sxs-lookup"><span data-stu-id="275c5-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="275c5-113">**下載 SDK**</span><span class="sxs-lookup"><span data-stu-id="275c5-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="275c5-114">NPM</span><span class="sxs-lookup"><span data-stu-id="275c5-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="275c5-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="275c5-115">**API documentation**</span></span></td><td>[<span data-ttu-id="275c5-116">Node.js API 參考文件</span><span class="sxs-lookup"><span data-stu-id="275c5-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="275c5-117">**SDK 安裝指示**</span><span class="sxs-lookup"><span data-stu-id="275c5-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="275c5-118">安裝指示</span><span class="sxs-lookup"><span data-stu-id="275c5-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="275c5-119">**參與 SDK**</span><span class="sxs-lookup"><span data-stu-id="275c5-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="275c5-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="275c5-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="275c5-121">**範例**</span><span class="sxs-lookup"><span data-stu-id="275c5-121">**Samples**</span></span></td><td>[<span data-ttu-id="275c5-122">Node.js 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="275c5-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="275c5-123">**開始使用教學課程**</span><span class="sxs-lookup"><span data-stu-id="275c5-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="275c5-124">開始使用 Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="275c5-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="275c5-125">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="275c5-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="275c5-126">使用 Azure Cosmos DB 來建置 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="275c5-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="275c5-127">**目前支援的平台**</span><span class="sxs-lookup"><span data-stu-id="275c5-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="275c5-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="275c5-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="275c5-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="275c5-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="275c5-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="275c5-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="275c5-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="275c5-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="275c5-132">版本資訊</span><span class="sxs-lookup"><span data-stu-id="275c5-132">Release notes</span></span>

### <span data-ttu-id="275c5-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="275c5-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="275c5-134">修正的 npm 文件。</span><span class="sxs-lookup"><span data-stu-id="275c5-134">npm documentation fixed.</span></span>

### <span data-ttu-id="275c5-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="275c5-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="275c5-136">已修正 executeStoredProcedure 中的錯誤，其中涉及的文件有特殊 Unicode 字元 (LS、PS)。</span><span class="sxs-lookup"><span data-stu-id="275c5-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="275c5-137">已修正在分割區索引鍵中使用 Unicode 字元處理文件的錯誤。</span><span class="sxs-lookup"><span data-stu-id="275c5-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="275c5-138">已修正使用名稱媒體建立集合的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="275c5-139">GitHub 問題 #114。</span><span class="sxs-lookup"><span data-stu-id="275c5-139">Github issue #114.</span></span>
* <span data-ttu-id="275c5-140">已修正權限授權權杖的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="275c5-141">GitHub 問題 #178。</span><span class="sxs-lookup"><span data-stu-id="275c5-141">Github issue #178.</span></span>

### <span data-ttu-id="275c5-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="275c5-143">新增對新[一致性層級](consistency-levels.md) ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="275c5-144">新增 UriFactory 的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="275c5-145">已修正 Unicode 支援錯誤。</span><span class="sxs-lookup"><span data-stu-id="275c5-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="275c5-146">GitHub 問題 #171。</span><span class="sxs-lookup"><span data-stu-id="275c5-146">GitHub issue #171.</span></span>

### <span data-ttu-id="275c5-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="275c5-148">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="275c5-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="275c5-149">新增控制跨分割區查詢平行處理程度的選項。</span><span class="sxs-lookup"><span data-stu-id="275c5-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="275c5-150">新增針對 Azure Cosmos DB 模擬器執行時停用 SSL 驗證的選項。</span><span class="sxs-lookup"><span data-stu-id="275c5-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="275c5-151">已將分割區集合的最小輸送量從 10,100 RU/s 降低為 2500 RU/s。</span><span class="sxs-lookup"><span data-stu-id="275c5-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="275c5-152">已修正單一資料分割集合的接續權杖錯誤。</span><span class="sxs-lookup"><span data-stu-id="275c5-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="275c5-153">GitHub 問題 #107。</span><span class="sxs-lookup"><span data-stu-id="275c5-153">Github issue #107.</span></span>
* <span data-ttu-id="275c5-154">已修正將 0 做為單一參數處理的 executeStoredProcedure 錯誤。</span><span class="sxs-lookup"><span data-stu-id="275c5-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="275c5-155">GitHub 問題 #155。</span><span class="sxs-lookup"><span data-stu-id="275c5-155">Github issue #155.</span></span>

### <span data-ttu-id="275c5-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="275c5-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="275c5-157">修正使用者-代理程式標頭以包含 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="275c5-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="275c5-158">次要程式碼清除。</span><span class="sxs-lookup"><span data-stu-id="275c5-158">Minor code cleanup.</span></span>

### <span data-ttu-id="275c5-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="275c5-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="275c5-160">當使用 SDK 以模擬器 (hostname=localhost) 為目標時，停用 SSL 驗證。</span><span class="sxs-lookup"><span data-stu-id="275c5-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="275c5-161">在預存程序執行期間，加入支援指令碼記錄功能。</span><span class="sxs-lookup"><span data-stu-id="275c5-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="275c5-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="275c5-163">新增對跨資料分割平行查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="275c5-164">新增對已分割集合的 TOP/ORDER BY 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="275c5-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="275c5-166">新加入已節流處理要求的重試原則支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="275c5-167">(已節流處理的要求會收到要求率太大的例外狀況，即錯誤碼 429。)根據預設，發生錯誤碼 429 時，Azure Cosmos DB 會遵守回應標頭中的 retryAfter 時間，並針對每個要求重試九次。</span><span class="sxs-lookup"><span data-stu-id="275c5-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="275c5-168">如果您想要忽略伺服器在多次重試之間傳回的 retryAfter 時間，現在可以在 ConnectionPolicy 物件上的 RetryOptions 屬性中設定固定的重試間隔時間。</span><span class="sxs-lookup"><span data-stu-id="275c5-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="275c5-169">Azure Cosmos DB 現在會針對每個要進行節流處理的要求等候最多 30 秒 (不論重試計數為何)，並傳回包含錯誤碼 429 的回應。</span><span class="sxs-lookup"><span data-stu-id="275c5-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="275c5-170">您也可以在 ConnectionPolicy 物件上的 RetryOptions 屬性中覆寫該時間。</span><span class="sxs-lookup"><span data-stu-id="275c5-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="275c5-171">Cosmos DB 現在會傳回 x-ms-throttle-retry-count 和 x-ms-throttle-retry-wait-time-ms 做為每個要求的回應標頭，其代表節流重試計數和要求歷經多次重試的累積時間。</span><span class="sxs-lookup"><span data-stu-id="275c5-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="275c5-172">新增 RetryOptions 類別，以及公開 ConnectionPolicy 類別上的 RetryOptions 屬性，使其能用來覆寫某些預設的重試選項。</span><span class="sxs-lookup"><span data-stu-id="275c5-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="275c5-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="275c5-174">新增對多重區域資料庫帳戶的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="275c5-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="275c5-176">新加入文件的存留時間 (TTL) 功能支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="275c5-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="275c5-178">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="275c5-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="275c5-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="275c5-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="275c5-180">已修正 RangePartitionResolver.resolveForRead 錯誤，其因錯誤的結果 CONCAT 而無法傳回連結。</span><span class="sxs-lookup"><span data-stu-id="275c5-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="275c5-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="275c5-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="275c5-182">修正 hashParitionResolver resolveForRead()：所提供的資料分割索引鍵都未擲回例外狀況時，而不會傳回所有已註冊連結的清單。</span><span class="sxs-lookup"><span data-stu-id="275c5-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="275c5-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="275c5-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="275c5-184">修正問題 [#100](https://github.com/Azure/azure-documentdb-node/issues/100)- HTTPS 專用代理程式：避免基於 Azure Cosmos DB 用途而修改全域代理程式。</span><span class="sxs-lookup"><span data-stu-id="275c5-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="275c5-185">針對所有 lib 要求使用專用的代理程式。</span><span class="sxs-lookup"><span data-stu-id="275c5-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="275c5-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="275c5-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="275c5-187">修正問題 [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - 正確處理媒體識別碼中的連字號。</span><span class="sxs-lookup"><span data-stu-id="275c5-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="275c5-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="275c5-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="275c5-189">修正問題 [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter 接聽程式洩漏警告。</span><span class="sxs-lookup"><span data-stu-id="275c5-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="275c5-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="275c5-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="275c5-191">修正問題 [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - 針對區分大小寫的系統，將資料夾 Hash 重新命名為 hash。</span><span class="sxs-lookup"><span data-stu-id="275c5-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="275c5-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="275c5-193">藉由新增雜湊和範圍分割解析程式來實作分區化支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="275c5-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="275c5-195">實作 Upsert。</span><span class="sxs-lookup"><span data-stu-id="275c5-195">Implement Upsert.</span></span> <span data-ttu-id="275c5-196">documentClient 上新的 upsertXXX 方法。</span><span class="sxs-lookup"><span data-stu-id="275c5-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="275c5-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="275c5-198">已略過以配合其他 SDK 的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="275c5-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="275c5-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="275c5-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="275c5-200">將 Q Pomise 包裝函式分割至新的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="275c5-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="275c5-201">更新至 npm 登錄的封裝檔案。</span><span class="sxs-lookup"><span data-stu-id="275c5-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="275c5-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="275c5-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="275c5-203">實作以識別碼為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="275c5-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="275c5-204">修正問題 [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - 目前屬性與 current() 方法衝突。</span><span class="sxs-lookup"><span data-stu-id="275c5-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="275c5-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="275c5-206">新增對地理空間索引的支援。</span><span class="sxs-lookup"><span data-stu-id="275c5-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="275c5-207">驗證所有資源的識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="275c5-207">Validates id property for all resources.</span></span> <span data-ttu-id="275c5-208">資源的識別碼不能包含 ?、/、#、&#47;&#47; 等字元，或在結尾處使用空格。</span><span class="sxs-lookup"><span data-stu-id="275c5-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="275c5-209">將新標頭「索引轉換進度」加至 ResourceResponse。</span><span class="sxs-lookup"><span data-stu-id="275c5-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="275c5-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="275c5-211">實作 V2 索引原則。</span><span class="sxs-lookup"><span data-stu-id="275c5-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="275c5-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="275c5-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="275c5-213">問題 [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - 核心與 Promise SDK 中實作的 eslint 和 grunt 組態。</span><span class="sxs-lookup"><span data-stu-id="275c5-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="275c5-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="275c5-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="275c5-215">問題 [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promise 包裝函式不包括標頭並發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="275c5-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="275c5-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="275c5-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="275c5-217">已實作透過新增 readConflicts、readConflictAsync 及 queryConflicts 來查詢衝突的功能。</span><span class="sxs-lookup"><span data-stu-id="275c5-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="275c5-218">已更新 API 文件。</span><span class="sxs-lookup"><span data-stu-id="275c5-218">Updated API documentation.</span></span>
* <span data-ttu-id="275c5-219">問題 [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync 錯誤。</span><span class="sxs-lookup"><span data-stu-id="275c5-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="275c5-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="275c5-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="275c5-221">GA SDK。</span><span class="sxs-lookup"><span data-stu-id="275c5-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="275c5-222">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="275c5-222">Release & Retirement Dates</span></span>
<span data-ttu-id="275c5-223">Microsoft 至少會在停用 SDK 的 **12 個月** 之前提供通知，以供順利轉換至較新/支援的版本。</span><span class="sxs-lookup"><span data-stu-id="275c5-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="275c5-224">新的功能與最佳化項目只會新增至目前的 SDK，因此建議您一律盡早升級至最新的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="275c5-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="275c5-225">服務會拒絕使用已停用 SDK 的任何 Cosmos DB 要求。</span><span class="sxs-lookup"><span data-stu-id="275c5-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="275c5-226">版本</span><span class="sxs-lookup"><span data-stu-id="275c5-226">Version</span></span> | <span data-ttu-id="275c5-227">發行日期</span><span class="sxs-lookup"><span data-stu-id="275c5-227">Release Date</span></span> | <span data-ttu-id="275c5-228">停用日期</span><span class="sxs-lookup"><span data-stu-id="275c5-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="275c5-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="275c5-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="275c5-230">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="275c5-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="275c5-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="275c5-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="275c5-232">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="275c5-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="275c5-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="275c5-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="275c5-234">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="275c5-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="275c5-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="275c5-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="275c5-236">2017 年 3 月 16 日</span><span class="sxs-lookup"><span data-stu-id="275c5-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="275c5-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="275c5-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="275c5-238">2017 年 1 月 27 日</span><span class="sxs-lookup"><span data-stu-id="275c5-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="275c5-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="275c5-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="275c5-240">2016 年 12 月 22 日</span><span class="sxs-lookup"><span data-stu-id="275c5-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="275c5-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="275c5-242">2016 年 10 月 3 日</span><span class="sxs-lookup"><span data-stu-id="275c5-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="275c5-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="275c5-244">2016 年 7 月 7 日</span><span class="sxs-lookup"><span data-stu-id="275c5-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="275c5-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="275c5-246">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="275c5-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="275c5-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="275c5-248">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="275c5-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="275c5-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="275c5-250">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="275c5-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="275c5-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="275c5-252">2016 年 3 月 8 日</span><span class="sxs-lookup"><span data-stu-id="275c5-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="275c5-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="275c5-254">2016 年 2 月 2 日</span><span class="sxs-lookup"><span data-stu-id="275c5-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="275c5-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="275c5-256">2016 年 2 月 1 日</span><span class="sxs-lookup"><span data-stu-id="275c5-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="275c5-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="275c5-258">2016 年 1 月 26 日</span><span class="sxs-lookup"><span data-stu-id="275c5-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="275c5-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="275c5-260">2016 年 1 月 22 日</span><span class="sxs-lookup"><span data-stu-id="275c5-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="275c5-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="275c5-262">2016 年 1 月 4 日</span><span class="sxs-lookup"><span data-stu-id="275c5-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="275c5-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="275c5-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="275c5-264">2015 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="275c5-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="275c5-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="275c5-266">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="275c5-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="275c5-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="275c5-268">2015 年 10 月 6 日</span><span class="sxs-lookup"><span data-stu-id="275c5-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="275c5-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="275c5-270">2015 年 9 月 10 日</span><span class="sxs-lookup"><span data-stu-id="275c5-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="275c5-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="275c5-272">2015 年 8 月 15 日</span><span class="sxs-lookup"><span data-stu-id="275c5-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="275c5-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="275c5-274">2015 年 8 月 5 日</span><span class="sxs-lookup"><span data-stu-id="275c5-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="275c5-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="275c5-276">2015 年 7 月 9 日</span><span class="sxs-lookup"><span data-stu-id="275c5-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="275c5-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="275c5-278">2015 年 6 月 4 日</span><span class="sxs-lookup"><span data-stu-id="275c5-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="275c5-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="275c5-280">2015 年 5 月 23 日</span><span class="sxs-lookup"><span data-stu-id="275c5-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="275c5-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="275c5-282">2015 年 5 月 15 日</span><span class="sxs-lookup"><span data-stu-id="275c5-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="275c5-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="275c5-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="275c5-284">2015 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="275c5-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="275c5-285">常見問題集</span><span class="sxs-lookup"><span data-stu-id="275c5-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="275c5-286">另請參閱</span><span class="sxs-lookup"><span data-stu-id="275c5-286">See also</span></span>
<span data-ttu-id="275c5-287">若要深入了解 Cosmos DB，請參閱 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="275c5-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

