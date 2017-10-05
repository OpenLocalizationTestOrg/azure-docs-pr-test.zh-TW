---
title: "Azure Cosmos DB .NET SDK 和資源 | Microsoft Docs"
description: "全面了解 .NET API 和 SDK，包括發行日期、停用日期及 Azure Cosmos DB .NET SDK 每個版本之間的變更。"
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 317792e04244a96cf8e47bc7e4a7f633f7a6d8c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a><span data-ttu-id="a8738-103">Azure Cosmos DB .NET SDK：下載和版本資訊</span><span class="sxs-lookup"><span data-stu-id="a8738-103">Azure Cosmos DB .NET SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8738-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a8738-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="a8738-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="a8738-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="a8738-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a8738-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="a8738-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8738-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="a8738-108">Java</span><span class="sxs-lookup"><span data-stu-id="a8738-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="a8738-109">Python</span><span class="sxs-lookup"><span data-stu-id="a8738-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="a8738-110">REST</span><span class="sxs-lookup"><span data-stu-id="a8738-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="a8738-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="a8738-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="a8738-112">SQL</span><span class="sxs-lookup"><span data-stu-id="a8738-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="a8738-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="a8738-113">**SDK download**</span></span></td><td>[<span data-ttu-id="a8738-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="a8738-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td><span data-ttu-id="a8738-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="a8738-115">**API documentation**</span></span></td><td>[<span data-ttu-id="a8738-116">.NET API 參考文件</span><span class="sxs-lookup"><span data-stu-id="a8738-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="a8738-117">**範例**</span><span class="sxs-lookup"><span data-stu-id="a8738-117">**Samples**</span></span></td><td>[<span data-ttu-id="a8738-118">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a8738-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="a8738-119">**開始使用**</span><span class="sxs-lookup"><span data-stu-id="a8738-119">**Get started**</span></span></td><td>[<span data-ttu-id="a8738-120">開始使用 Azure Cosmos DB .NET SDK 教學課程</span><span class="sxs-lookup"><span data-stu-id="a8738-120">Get started with the Azure Cosmos DB .NET SDK</span></span>](documentdb-get-started.md)</td></tr>

<tr><td><span data-ttu-id="a8738-121">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="a8738-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="a8738-122">使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="a8738-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="a8738-123">**目前支援的架構**</span><span class="sxs-lookup"><span data-stu-id="a8738-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="a8738-124">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="a8738-124">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="a8738-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="a8738-125">Release notes</span></span>

### <a name="a-name11701170"></a><span data-ttu-id="a8738-126"><a name="1.17.0"/>1.17.0</span><span class="sxs-lookup"><span data-stu-id="a8738-126"><a name="1.17.0"/>1.17.0</span></span> 

* <span data-ttu-id="a8738-127">已新增將 PartitionKeyRangeId 做為 FeedOption 的支援，以供對特定分割區索引鍵範圍值限制查詢結果範圍。</span><span class="sxs-lookup"><span data-stu-id="a8738-127">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="a8738-128">已新增將 StartTime 做為 ChangeFeedOption 的支援，以開始尋找該時間之後的變更。</span><span class="sxs-lookup"><span data-stu-id="a8738-128">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span>

### <a name="a-name11611161"></a><span data-ttu-id="a8738-129"><a name="1.16.1"/>1.16.1</span><span class="sxs-lookup"><span data-stu-id="a8738-129"><a name="1.16.1"/>1.16.1</span></span>
* <span data-ttu-id="a8738-130">修正 JsonSerializable 類別中可能會造成堆疊溢位例外狀況的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-130">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name11601160"></a><span data-ttu-id="a8738-131"><a name="1.16.0"/>1.16.0</span><span class="sxs-lookup"><span data-stu-id="a8738-131"><a name="1.16.0"/>1.16.0</span></span>
*   <span data-ttu-id="a8738-132">已修正需要重新編譯應用程式的問題，之所以有此問題，是因為在 DocumentClient 建構函式中導入 JsonSerializerSettings 來作為選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="a8738-132">Fixed an issue that required recompiling of the application due to the introduction of JsonSerializerSettings as an optional parameter in the DocumentClient constructor.</span></span>
* <span data-ttu-id="a8738-133">已將 DocumentClient 建構函式標記為過時，該建構函式需要 JsonSerializerSettings 來作為最後一個參數，以在傳遞 JsonSerializerSettings 參數時允許使用 ConnectionPolicy 和 ConsistencyLevel 參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="a8738-133">Marked the DocumentClient constructor obsolete that required JsonSerializerSettings as the last parameter to allow for default values of ConnectionPolicy and ConsistencyLevel parameters when passing in JsonSerializerSettings parameter.</span></span>

### <a name="a-name11501150"></a><span data-ttu-id="a8738-134"><a name="1.15.0"/>1.15.0</span><span class="sxs-lookup"><span data-stu-id="a8738-134"><a name="1.15.0"/>1.15.0</span></span>
*   <span data-ttu-id="a8738-135">已新增對 [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 具現化時指定自訂 JsonSerializerSettings 的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-135">Added support for specifying custom JsonSerializerSettings while instantiating [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span></span>

### <a name="a-name11411141"></a><span data-ttu-id="a8738-136"><a name="1.14.1"/>1.14.1</span><span class="sxs-lookup"><span data-stu-id="a8738-136"><a name="1.14.1"/>1.14.1</span></span>
*   <span data-ttu-id="a8738-137">針對不支援 SSE4 指令的 x64 電腦，已修正執行 Azure Cosmos DB API 查詢時，這類電腦會擲回 SEHException 的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-137">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw an SEHException when running Azure Cosmos DB DocumentDB API queries.</span></span>

### <a name="a-name11401140"></a><span data-ttu-id="a8738-138"><a name="1.14.0"/>1.14.0</span><span class="sxs-lookup"><span data-stu-id="a8738-138"><a name="1.14.0"/>1.14.0</span></span>
*   <span data-ttu-id="a8738-139">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-139">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="a8738-140">已新增對個別資料分割之查詢計量的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-140">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="a8738-141">已新增對限制查詢之接續權杖大小的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-141">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="a8738-142">已新增對失敗要求進行更詳細追蹤的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-142">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="a8738-143">SDK 中已有一些效能改進。</span><span class="sxs-lookup"><span data-stu-id="a8738-143">Made some performance improvements in the SDK.</span></span>

### <a name="a-name11341134"></a><span data-ttu-id="a8738-144"><a name="1.13.4"/>1.13.4</span><span class="sxs-lookup"><span data-stu-id="a8738-144"><a name="1.13.4"/>1.13.4</span></span>
* <span data-ttu-id="a8738-145">在功能上與 1.13.3 相同。</span><span class="sxs-lookup"><span data-stu-id="a8738-145">Functionally same as 1.13.3.</span></span> <span data-ttu-id="a8738-146">已有一些內部變更。</span><span class="sxs-lookup"><span data-stu-id="a8738-146">Made some internal changes.</span></span>

### <a name="a-name11331133"></a><span data-ttu-id="a8738-147"><a name="1.13.3"/>1.13.3</span><span class="sxs-lookup"><span data-stu-id="a8738-147"><a name="1.13.3"/>1.13.3</span></span>
* <span data-ttu-id="a8738-148">在功能上與 1.13.2 相同。</span><span class="sxs-lookup"><span data-stu-id="a8738-148">Functionally same as 1.13.2.</span></span> <span data-ttu-id="a8738-149">已有一些內部變更。</span><span class="sxs-lookup"><span data-stu-id="a8738-149">Made some internal changes.</span></span>

### <a name="a-name11321132"></a><span data-ttu-id="a8738-150"><a name="1.13.2"/>1.13.2</span><span class="sxs-lookup"><span data-stu-id="a8738-150"><a name="1.13.2"/>1.13.2</span></span>
* <span data-ttu-id="a8738-151">修正將在彙總查詢之 FeedOptions 中提供的 PartitionKey 值忽略的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-151">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="a8738-152">修正在執行移動途中跨資料分割 Order By 查詢期間，進行資料分割管理的透明處理時發生的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-152">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name11311131"></a><span data-ttu-id="a8738-153"><a name="1.13.1"/>1.13.1</span><span class="sxs-lookup"><span data-stu-id="a8738-153"><a name="1.13.1"/>1.13.1</span></span>
* <span data-ttu-id="a8738-154">已修正在 ASP.NET 內容內部使用時會在某些非同步 API 中造成死結的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-154">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="a8738-155"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="a8738-155"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="a8738-156">修正來讓 SDK 在某些情況下能夠更有彈性地進行自動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a8738-156">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name11221122"></a><span data-ttu-id="a8738-157"><a name="1.12.2"/>1.12.2</span><span class="sxs-lookup"><span data-stu-id="a8738-157"><a name="1.12.2"/>1.12.2</span></span>
* <span data-ttu-id="a8738-158">修正偶爾會造成「WebException: 無法解析遠端名稱」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a8738-158">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="a8738-159">透過針對 ReadDocumentAsync API 新增多載，以新增直接讀取具類型文件的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-159">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name11211121"></a><span data-ttu-id="a8738-160"><a name="1.12.1"/>1.12.1</span><span class="sxs-lookup"><span data-stu-id="a8738-160"><a name="1.12.1"/>1.12.1</span></span>
* <span data-ttu-id="a8738-161">新增彙總查詢的 LINQ 支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="a8738-161">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="a8738-162">針對使用事件處理常式所造成的 ConnectionPolicy 物件，修正記憶體流失問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-162">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="a8738-163">修正使用 ETag 時 UpsertAttachmentAsync 無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-163">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="a8738-164">修正根據字串欄位排序時交叉資料分割排序依據查詢接續無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-164">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="a8738-165"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="a8738-165"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="a8738-166">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="a8738-166">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="a8738-167">請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。</span><span class="sxs-lookup"><span data-stu-id="a8738-167">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="a8738-168">已將分割區集合的最小輸送量從 10,100 RU/s 降低為 2500 RU/s。</span><span class="sxs-lookup"><span data-stu-id="a8738-168">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name11141114"></a><span data-ttu-id="a8738-169"><a name="1.11.4"/>1.11.4</span><span class="sxs-lookup"><span data-stu-id="a8738-169"><a name="1.11.4"/>1.11.4</span></span>
* <span data-ttu-id="a8738-170">修正一個某些跨分割區查詢在 32 位元主機處理序中失敗的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-170">Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.</span></span>
* <span data-ttu-id="a8738-171">修正在閘道模式中未使用失敗要求的權杖來更新工作階段容器的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-171">Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.</span></span>
* <span data-ttu-id="a8738-172">修正縱向選取中具有 UDF 呼叫的查詢在某些案例中失敗的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-172">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span></span>
* <span data-ttu-id="a8738-173">已修正用戶端效能，以提高要求的讀取和寫入輸送量。</span><span class="sxs-lookup"><span data-stu-id="a8738-173">Client side performance fixes for increasing the read and write throughput of the requests.</span></span>

### <a name="a-name11131113"></a><span data-ttu-id="a8738-174"><a name="1.11.3"/>1.11.3</span><span class="sxs-lookup"><span data-stu-id="a8738-174"><a name="1.11.3"/>1.11.3</span></span>
* <span data-ttu-id="a8738-175">修正未使用失敗要求的權杖來更新工作階段容器的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-175">Fix for an issue wherein the session container was not being updated with the token for failed requests.</span></span>
* <span data-ttu-id="a8738-176">新增 SDK 支援，以在 32 位元主機處理序中運作。</span><span class="sxs-lookup"><span data-stu-id="a8738-176">Added support for the SDK to work in a 32-bit host process.</span></span> <span data-ttu-id="a8738-177">請注意，若使用跨分割區查詢，建議您使用 64 位元主機處理以獲得改進的效能。</span><span class="sxs-lookup"><span data-stu-id="a8738-177">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span></span>
* <span data-ttu-id="a8738-178">改進關於 IN 運算式中涉及大量分割區索引鍵值之查詢案例的效能。</span><span class="sxs-lookup"><span data-stu-id="a8738-178">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span></span>
* <span data-ttu-id="a8738-179">在設定 PopulateQuotaInfo 選項時，已在 ResourceResponse 中填入各種資源配額統計資料，以供文件集合讀取要求使用。</span><span class="sxs-lookup"><span data-stu-id="a8738-179">Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span></span>

### <a name="a-name11111111"></a><span data-ttu-id="a8738-180"><a name="1.11.1"/>1.11.1</span><span class="sxs-lookup"><span data-stu-id="a8738-180"><a name="1.11.1"/>1.11.1</span></span>
* <span data-ttu-id="a8738-181">針對在 1.11.0 推出的 CreateDocumentCollectionIfNotExistsAsync API 小幅修正效能。</span><span class="sxs-lookup"><span data-stu-id="a8738-181">Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span></span>
* <span data-ttu-id="a8738-182">針對和高比例並行要求有關的案例，修正 SDK 中的效能。</span><span class="sxs-lookup"><span data-stu-id="a8738-182">Performance fix in the SDK for scenarios that involve high degree of concurrent requests.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="a8738-183"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="a8738-183"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="a8738-184">支援新的類別和方法以在集合內處理文件的[變更摘要](change-feed.md)。</span><span class="sxs-lookup"><span data-stu-id="a8738-184">Support for new classes and methods to process the [change feed](change-feed.md) of documents within a collection.</span></span>
* <span data-ttu-id="a8738-185">支援跨資料分割繼續查詢和改善跨資料分割查詢的一些效能。</span><span class="sxs-lookup"><span data-stu-id="a8738-185">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span></span>
* <span data-ttu-id="a8738-186">新增 CreateDatabaseIfNotExistsAsync 和 CreateDocumentCollectionIfNotExistsAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="a8738-186">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span></span>
* <span data-ttu-id="a8738-187">針對下列系統函式支援 LINQ︰IsDefined、IsNull 和 IsPrimitive。</span><span class="sxs-lookup"><span data-stu-id="a8738-187">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span></span>
* <span data-ttu-id="a8738-188">修正在搭配使用 Nuget 套件和具有 project.json 工具的專案時，自動將 Microsoft.Azure.Documents.ServiceInterop.dll 和 DocumentDB.Spatial.Sql.dll 組件的 bin 放入應用程式的 bin 資料夾的動作。</span><span class="sxs-lookup"><span data-stu-id="a8738-188">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.</span></span>
* <span data-ttu-id="a8738-189">支援發出用戶端 ETW 追蹤，其可在偵錯案例中幫上忙。</span><span class="sxs-lookup"><span data-stu-id="a8738-189">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="a8738-190"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="a8738-190"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="a8738-191">新增分割集合的直接連線支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-191">Added direct connectivity support for partitioned collections.</span></span>
* <span data-ttu-id="a8738-192">改進「界限-陳舊」一致性層級的效能。</span><span class="sxs-lookup"><span data-stu-id="a8738-192">Improved performance for the Bounded Staleness consistency level.</span></span>
* <span data-ttu-id="a8738-193">新增為異地隔離空間查詢指定集合索引編製原則時的 Polygon 和 LineString 資料類型。</span><span class="sxs-lookup"><span data-stu-id="a8738-193">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="a8738-194">新增轉譯述詞時對 StringEnumConverter、IsoDateTimeConverter、UnixDateTimeConverter 的 LINQ 支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-194">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span></span>
* <span data-ttu-id="a8738-195">多項 SDK 錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="a8738-195">Various SDK bug fixes.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="a8738-196"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="a8738-196"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="a8738-197">將造成下列 NotFoundException 的問題修正︰讀取工作階段不適用於輸入工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="a8738-197">Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token.</span></span> <span data-ttu-id="a8738-198">查詢異地分散帳戶讀取區域時，在某些情況下發生此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8738-198">This exception occurred in some cases when querying for the read-region of a geo-distributed account.</span></span>
* <span data-ttu-id="a8738-199">公開 ResourceResponse 類別中的 ResponseStream 屬性，可讓您直接從回應存取基礎資料流。</span><span class="sxs-lookup"><span data-stu-id="a8738-199">Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="a8738-200"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="a8738-200"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="a8738-201">修改了 ResourceResponse、FeedResponse、StoredProcedureResponse 和 MediaResponse 類別以實作對應的公用介面，讓它們可以模擬用於測試導向部署 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="a8738-201">Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).</span></span>
* <span data-ttu-id="a8738-202">修正了使用自訂 JsonSerializerSettings 物件來序列化資料時，會造成資料分割索引鍵標頭格式不正確的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-202">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="a8738-203"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="a8738-203"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="a8738-204">已修正造成長時間執行的查詢失敗，並伴隨「授權權杖目前無效」錯誤的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-204">Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.</span></span>
* <span data-ttu-id="a8738-205">已修正會從跨資料分割的排名/排序依據查詢中移除原始 SqlParameterCollection 的問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-205">Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="a8738-206"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="a8738-206"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="a8738-207">已新增分割集合的平行查詢支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-207">Added support for parallel queries for partitioned collections.</span></span>
* <span data-ttu-id="a8738-208">已新增分割集合的跨資料分割 ORDER BY 和 TOP 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-208">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span></span>
* <span data-ttu-id="a8738-209">已修正使用 Azure Cosmos DB Nuget 套件參照來參考 Azure Cosmos DB 專案時，遺失所需的 DocumentDB.Spatial.Sql.dll 與 Microsoft.Azure.Documents.ServiceInterop.dll 參照。</span><span class="sxs-lookup"><span data-stu-id="a8738-209">Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing an Azure Cosmos DB project with a reference to the Azure Cosmos DB Nuget package.</span></span>
* <span data-ttu-id="a8738-210">已修正在 LINQ 中使用使用者定義的函式時，使用不同類型參數的能力。</span><span class="sxs-lookup"><span data-stu-id="a8738-210">Fixed the ability to use parameters of different types when using user-defined functions in LINQ.</span></span> 
* <span data-ttu-id="a8738-211">已修正廣域複寫帳戶中的的錯誤，此錯誤會使得 Upsert 呼叫導向讀取位置而非寫入位置。</span><span class="sxs-lookup"><span data-stu-id="a8738-211">Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.</span></span>
* <span data-ttu-id="a8738-212">已在遺失的 IDocumentClient 介面加入方法：</span><span class="sxs-lookup"><span data-stu-id="a8738-212">Added methods to the IDocumentClient interface that were missing:</span></span> 
  * <span data-ttu-id="a8738-213">UpsertAttachmentAsync 方法，會接受 mediaStream 及選項做為參數</span><span class="sxs-lookup"><span data-stu-id="a8738-213">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span></span>
  * <span data-ttu-id="a8738-214">CreateAttachmentAsync 方法，會接受選項做為參數</span><span class="sxs-lookup"><span data-stu-id="a8738-214">CreateAttachmentAsync method that takes options as a parameter</span></span>
  * <span data-ttu-id="a8738-215">CreateOfferQuery 方法，會接受 querySpec 做為參數</span><span class="sxs-lookup"><span data-stu-id="a8738-215">CreateOfferQuery method that takes querySpec as a parameter.</span></span>
* <span data-ttu-id="a8738-216">已解除密封 IDocumentClient 介面中公開的公用類別。</span><span class="sxs-lookup"><span data-stu-id="a8738-216">Unsealed public classes that are exposed in the IDocumentClient interface.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="a8738-217"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="a8738-217"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="a8738-218">新增對多重區域資料庫帳戶的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-218">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="a8738-219">新增在已節流處理的要求上進行重試的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-219">Added support for retry on throttled requests.</span></span>  <span data-ttu-id="a8738-220">使用者可以藉由設定 ConnectionPolicy.RetryOptions 屬性，來自訂重試次數和等待時間上限。</span><span class="sxs-lookup"><span data-stu-id="a8738-220">User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.</span></span>
* <span data-ttu-id="a8738-221">新增新的 IDocumentClient 介面，其中會定義所有 DocumenClient 屬性和方法的簽章。</span><span class="sxs-lookup"><span data-stu-id="a8738-221">Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.</span></span>  <span data-ttu-id="a8738-222">做為此變更的一部分，也將建立 IQueryable 和 IOrderedQueryable 的擴充方法變更為 DocumentClient 類別本身上的方法。</span><span class="sxs-lookup"><span data-stu-id="a8738-222">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.</span></span>
* <span data-ttu-id="a8738-223">新增組態選項，以針對指定的 Azure Cosmos DB 端點 URI 設定 ServicePoint.ConnectionLimit。</span><span class="sxs-lookup"><span data-stu-id="a8738-223">Added configuration option to set the ServicePoint.ConnectionLimit for a given Azure Cosmos DB endpoint Uri.</span></span>  <span data-ttu-id="a8738-224">使用 ConnectionPolicy.MaxConnectionLimit 來變更預設值 (已設為 50)。</span><span class="sxs-lookup"><span data-stu-id="a8738-224">Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.</span></span>
* <span data-ttu-id="a8738-225">已淘汰 IPartitionResolver 及其實作。</span><span class="sxs-lookup"><span data-stu-id="a8738-225">Deprecated IPartitionResolver and its implementation.</span></span>  <span data-ttu-id="a8738-226">現在不支援 IPartitionResolver。</span><span class="sxs-lookup"><span data-stu-id="a8738-226">Support for IPartitionResolver is now obsolete.</span></span> <span data-ttu-id="a8738-227">建議您針對更高的儲存體和輸送量使用分割集合。</span><span class="sxs-lookup"><span data-stu-id="a8738-227">It's recommended that you use Partitioned Collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="a8738-228"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="a8738-228"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="a8738-229">根據會接受 RequestOptions 做為參數的 ExecuteStoredProcedureAsync 方法，新加入 URI 多載。</span><span class="sxs-lookup"><span data-stu-id="a8738-229">Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="a8738-230"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="a8738-230"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="a8738-231">新加入文件的存留時間 (TTL) 支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-231">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name163163"></a><span data-ttu-id="a8738-232"><a name="1.6.3"/>1.6.3</span><span class="sxs-lookup"><span data-stu-id="a8738-232"><a name="1.6.3"/>1.6.3</span></span>
* <span data-ttu-id="a8738-233">修正 .NET SDK 的 Nuget 封裝錯誤，可供封裝為 Azure 雲端服務解決方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="a8738-233">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span></span>

### <a name="a-name162162"></a><span data-ttu-id="a8738-234"><a name="1.6.2"/>1.6.2</span><span class="sxs-lookup"><span data-stu-id="a8738-234"><a name="1.6.2"/>1.6.2</span></span>
* <span data-ttu-id="a8738-235">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="a8738-235">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name153153"></a><span data-ttu-id="a8738-236"><a name="1.5.3"/>1.5.3</span><span class="sxs-lookup"><span data-stu-id="a8738-236"><a name="1.5.3"/>1.5.3</span></span>
* <span data-ttu-id="a8738-237">**[已修正]** 查詢 Azure Cosmos DB 端點時擲回：「System.Net.Http.HttpRequestException：將內容複製到資料流時發生錯誤」。</span><span class="sxs-lookup"><span data-stu-id="a8738-237">**[Fixed]** Querying Azure Cosmos DB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.</span></span>

### <a name="a-name152152"></a><span data-ttu-id="a8738-238"><a name="1.5.2"/>1.5.2</span><span class="sxs-lookup"><span data-stu-id="a8738-238"><a name="1.5.2"/>1.5.2</span></span>
* <span data-ttu-id="a8738-239">擴充的 LINQ 支援包括新的分頁、條件式運算式以及範圍比較的運算子。</span><span class="sxs-lookup"><span data-stu-id="a8738-239">Expanded LINQ support including new operators for paging, conditional expressions, and range comparison.</span></span>
  * <span data-ttu-id="a8738-240">Take 運算子：可啟用 LINQ 中的 SELECT TOP 行為</span><span class="sxs-lookup"><span data-stu-id="a8738-240">Take operator to enable SELECT TOP behavior in LINQ</span></span>
  * <span data-ttu-id="a8738-241">CompareTo 運算子：可啟用字串範圍比較</span><span class="sxs-lookup"><span data-stu-id="a8738-241">CompareTo operator to enable string range comparisons</span></span>
  * <span data-ttu-id="a8738-242">條件式 (?) 與聯合運算子 (??)</span><span class="sxs-lookup"><span data-stu-id="a8738-242">Conditional (?) and coalesce operators (??)</span></span>
* <span data-ttu-id="a8738-243">**[已修正]** 將模型投射與 LINQ 查詢中的 Where-In 結合使用時發生 ArgumentOutOfRangeException。</span><span class="sxs-lookup"><span data-stu-id="a8738-243">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in a LINQ query.</span></span> [<span data-ttu-id="a8738-244">#81</span><span class="sxs-lookup"><span data-stu-id="a8738-244">#81</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><span data-ttu-id="a8738-245"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="a8738-245"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="a8738-246">**[已修正]** 如果 Select 不是最後一個運算式，LINQ 提供者會假設沒有任何預測，並會產生不正確的 SELECT *。</span><span class="sxs-lookup"><span data-stu-id="a8738-246">**[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT * incorrectly.</span></span>  [<span data-ttu-id="a8738-247">#58</span><span class="sxs-lookup"><span data-stu-id="a8738-247">#58</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><span data-ttu-id="a8738-248"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="a8738-248"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="a8738-249">實作 Upsert、新增 UpsertXXXAsync 方法</span><span class="sxs-lookup"><span data-stu-id="a8738-249">Implemented Upsert, Added UpsertXXXAsync methods</span></span>
* <span data-ttu-id="a8738-250">所有要求的效能改進</span><span class="sxs-lookup"><span data-stu-id="a8738-250">Performance improvements for all requests</span></span>
* <span data-ttu-id="a8738-251">LINQ 提供者支援字串的條件式、聯合和 CompareTo 方法</span><span class="sxs-lookup"><span data-stu-id="a8738-251">LINQ Provider support for conditional, coalesce, and CompareTo methods for strings</span></span>
* <span data-ttu-id="a8738-252">**[已修正]** LINQ 提供者 --> 在 List 上實作 Contains 方法，以產生與 IEnumerable 和 Array 上相同的 SQL</span><span class="sxs-lookup"><span data-stu-id="a8738-252">**[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array</span></span>
* <span data-ttu-id="a8738-253">**[已修正]** 重試時，BackoffRetryUtility 會再次使用相同的 HttpRequestMessage，而非建立新的</span><span class="sxs-lookup"><span data-stu-id="a8738-253">**[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry</span></span>
* <span data-ttu-id="a8738-254">**[已過時]** UriFactory.CreateCollection --> 現應使用 UriFactory.CreateDocumentCollection</span><span class="sxs-lookup"><span data-stu-id="a8738-254">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span></span>

### <a name="a-name141141"></a><span data-ttu-id="a8738-255"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="a8738-255"><a name="1.4.1"/>1.4.1</span></span>
* <span data-ttu-id="a8738-256">**[已修正]** 使用非 en 文化特性資訊時 (例如 nl-NL 等) 的當地語系化問題。</span><span class="sxs-lookup"><span data-stu-id="a8738-256">**[Fixed]** Localization issues when using non en culture info such as nl-NL, etc.</span></span> 

### <a name="a-name140140"></a><span data-ttu-id="a8738-257"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="a8738-257"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="a8738-258">已新增以識別碼為基礎的路由</span><span class="sxs-lookup"><span data-stu-id="a8738-258">Added ID-based routing</span></span>
  * <span data-ttu-id="a8738-259">新的 UriFactory 協助程式，可協助建構以識別碼為基礎的資源連結</span><span class="sxs-lookup"><span data-stu-id="a8738-259">New UriFactory helper to assist with constructing ID-based resource links</span></span>
  * <span data-ttu-id="a8738-260">DocumentClient 上新的多載可接受 URI</span><span class="sxs-lookup"><span data-stu-id="a8738-260">New overloads on DocumentClient to take in URI</span></span>
* <span data-ttu-id="a8738-261">LINQ 中新增用於地理空間的 IsValid() 和 isvaliddetailed ()</span><span class="sxs-lookup"><span data-stu-id="a8738-261">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span></span>
* <span data-ttu-id="a8738-262">增強的 LINQ 提供者支援：</span><span class="sxs-lookup"><span data-stu-id="a8738-262">LINQ Provider support enhanced:</span></span>
  * <span data-ttu-id="a8738-263">**算術** - Abs、Acos、Asin、Atan、Ceiling、Cos、Exp、Floor、Log、Log10、Pow、Round、Sign、Sin、Sqrt、Tan、Truncate</span><span class="sxs-lookup"><span data-stu-id="a8738-263">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span></span>
  * <span data-ttu-id="a8738-264">**字串** - Concat、Contains、EndsWith、IndexOf、Count、ToLower、TrimStart、Replace、Reverse、TrimEnd、StartsWith、SubString、ToUpper</span><span class="sxs-lookup"><span data-stu-id="a8738-264">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span></span>
  * <span data-ttu-id="a8738-265">**陣列** - Concat、Contains、Count</span><span class="sxs-lookup"><span data-stu-id="a8738-265">**Array** - Concat, Contains, Count</span></span>
  * <span data-ttu-id="a8738-266">**IN** 運算子</span><span class="sxs-lookup"><span data-stu-id="a8738-266">**IN** operator</span></span>

### <a name="a-name130130"></a><span data-ttu-id="a8738-267"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="a8738-267"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="a8738-268">新增修改索引編製原則的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-268">Added support for modifying indexing policies.</span></span>
  * <span data-ttu-id="a8738-269">DocumentClient 中新的 ReplaceDocumentCollectionAsync 方法</span><span class="sxs-lookup"><span data-stu-id="a8738-269">New ReplaceDocumentCollectionAsync method in DocumentClient</span></span>
  * <span data-ttu-id="a8738-270">ResourceResponse 中新的 IndexTransformationProgress 屬性<T>可追蹤索引原則變更的百分比進度</span><span class="sxs-lookup"><span data-stu-id="a8738-270">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span></span>
  * <span data-ttu-id="a8738-271">DocumentCollection.IndexingPolicy 現在可變動</span><span class="sxs-lookup"><span data-stu-id="a8738-271">DocumentCollection.IndexingPolicy is now mutable</span></span>
* <span data-ttu-id="a8738-272">新增空間索引編製和查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-272">Added support for spatial indexing and query.</span></span>
  * <span data-ttu-id="a8738-273">新的 Microsoft.Azure.Documents.Spatial 命名空間，可序列化/還原序列化空間類型，例如 Point 和 Polygon</span><span class="sxs-lookup"><span data-stu-id="a8738-273">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span></span>
  * <span data-ttu-id="a8738-274">新的 SpatialIndex 類別，可對儲存在 Cosmos DB 中的 GeoJSON 資料編製索引</span><span class="sxs-lookup"><span data-stu-id="a8738-274">New SpatialIndex class for indexing GeoJSON data stored in Cosmos DB</span></span>
* <span data-ttu-id="a8738-275">**[已修正]**：從 LINQ 運算式產生的 SQL 查詢不正確 [#38](https://github.com/Azure/azure-documentdb-net/issues/38) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a8738-275">**[Fixed]** Incorrect SQL query generated from a LINQ expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38).</span></span>

### <a name="a-name120120"></a><span data-ttu-id="a8738-276"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="a8738-276"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="a8738-277">已新增對 Newtonsoft.Json v5.0.7 的相依性。</span><span class="sxs-lookup"><span data-stu-id="a8738-277">Added a dependency on Newtonsoft.Json v5.0.7.</span></span>
* <span data-ttu-id="a8738-278">變更為支援 Order By：</span><span class="sxs-lookup"><span data-stu-id="a8738-278">Made changes to support Order By:</span></span>
  
  * <span data-ttu-id="a8738-279">LINQ 提供者支援 OrderBy() 或 OrderByDescending()</span><span class="sxs-lookup"><span data-stu-id="a8738-279">LINQ provider support for OrderBy() or OrderByDescending()</span></span>
  * <span data-ttu-id="a8738-280">IndexingPolicy 支援 Order By</span><span class="sxs-lookup"><span data-stu-id="a8738-280">IndexingPolicy to support Order By</span></span> 
    
    <span data-ttu-id="a8738-281">**可能使得舊程式碼無法運作的變更**</span><span class="sxs-lookup"><span data-stu-id="a8738-281">**Possible breaking change**</span></span> 
    
    <span data-ttu-id="a8738-282">如果現有程式碼以自訂索引原則來佈建集合，則需要更新現有的程式碼，才能支援新的 IndexingPolicy 類別。</span><span class="sxs-lookup"><span data-stu-id="a8738-282">If you have existing code that provisions collections with a custom indexing policy, then your existing code needs to be updated to support the new IndexingPolicy class.</span></span> <span data-ttu-id="a8738-283">如果您沒有自訂的索引原則，這個變更不會影響到您。</span><span class="sxs-lookup"><span data-stu-id="a8738-283">If you have no custom indexing policy, then this change does not affect you.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="a8738-284"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="a8738-284"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="a8738-285">使用新的 HashPartitionResolver 和 RangePartitionResolver 類別及 IPartitionResolver，以新增對資料分割的支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-285">Added support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver.</span></span>
* <span data-ttu-id="a8738-286">已新增 DataContract 序列化。</span><span class="sxs-lookup"><span data-stu-id="a8738-286">Added DataContract serialization.</span></span>
* <span data-ttu-id="a8738-287">已新增 LINQ 提供者中的 GUID 支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-287">Added GUID support in LINQ provider.</span></span>
* <span data-ttu-id="a8738-288">已新增 LINQ 中的 UDF 支援。</span><span class="sxs-lookup"><span data-stu-id="a8738-288">Added UDF support in LINQ.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="a8738-289"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="a8738-289"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="a8738-290">GA SDK</span><span class="sxs-lookup"><span data-stu-id="a8738-290">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="a8738-291">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="a8738-291">Release & Retirement dates</span></span>
<span data-ttu-id="a8738-292">Microsoft 至少會在停用 SDK 的 **12 個月** 之前提供通知，以供順利轉換至較新/支援的版本。</span><span class="sxs-lookup"><span data-stu-id="a8738-292">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="a8738-293">新的功能與最佳化項目只會新增至目前的 SDK，因此建議您一律盡早升級至最新的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="a8738-293">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="a8738-294">服務會拒絕使用已停用 SDK 的任何 Azure Cosmos DB 要求。</span><span class="sxs-lookup"><span data-stu-id="a8738-294">Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.</span></span>

<br/>

| <span data-ttu-id="a8738-295">版本</span><span class="sxs-lookup"><span data-stu-id="a8738-295">Version</span></span> | <span data-ttu-id="a8738-296">發行日期</span><span class="sxs-lookup"><span data-stu-id="a8738-296">Release Date</span></span> | <span data-ttu-id="a8738-297">停用日期</span><span class="sxs-lookup"><span data-stu-id="a8738-297">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="a8738-298">1.17.0</span><span class="sxs-lookup"><span data-stu-id="a8738-298">1.17.0</span></span>](#1.17.0) |<span data-ttu-id="a8738-299">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="a8738-299">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-300">1.16.1</span><span class="sxs-lookup"><span data-stu-id="a8738-300">1.16.1</span></span>](#1.16.1) |<span data-ttu-id="a8738-301">2017 年 8 月 7 日</span><span class="sxs-lookup"><span data-stu-id="a8738-301">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-302">1.16.0</span><span class="sxs-lookup"><span data-stu-id="a8738-302">1.16.0</span></span>](#1.16.0) |<span data-ttu-id="a8738-303">2017 年 8 月 2 日</span><span class="sxs-lookup"><span data-stu-id="a8738-303">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-304">1.15.0</span><span class="sxs-lookup"><span data-stu-id="a8738-304">1.15.0</span></span>](#1.15.0) |<span data-ttu-id="a8738-305">2017 年 6 月 30 日</span><span class="sxs-lookup"><span data-stu-id="a8738-305">June 30, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-306">1.14.1</span><span class="sxs-lookup"><span data-stu-id="a8738-306">1.14.1</span></span>](#1.14.1) |<span data-ttu-id="a8738-307">2017 年 5 月 23 日</span><span class="sxs-lookup"><span data-stu-id="a8738-307">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-308">1.14.0</span><span class="sxs-lookup"><span data-stu-id="a8738-308">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="a8738-309">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="a8738-309">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-310">1.13.4</span><span class="sxs-lookup"><span data-stu-id="a8738-310">1.13.4</span></span>](#1.13.4) |<span data-ttu-id="a8738-311">2017 年 5 月 09 日</span><span class="sxs-lookup"><span data-stu-id="a8738-311">May 09, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-312">1.13.3</span><span class="sxs-lookup"><span data-stu-id="a8738-312">1.13.3</span></span>](#1.13.3) |<span data-ttu-id="a8738-313">2017 年 5 月 06 日</span><span class="sxs-lookup"><span data-stu-id="a8738-313">May 06, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-314">1.13.2</span><span class="sxs-lookup"><span data-stu-id="a8738-314">1.13.2</span></span>](#1.13.2) |<span data-ttu-id="a8738-315">2017 年 4 月 19 日</span><span class="sxs-lookup"><span data-stu-id="a8738-315">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-316">1.13.1</span><span class="sxs-lookup"><span data-stu-id="a8738-316">1.13.1</span></span>](#1.13.1) |<span data-ttu-id="a8738-317">2017 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="a8738-317">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-318">1.13.0</span><span class="sxs-lookup"><span data-stu-id="a8738-318">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="a8738-319">2017 年 3 月 24 日</span><span class="sxs-lookup"><span data-stu-id="a8738-319">March 24, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-320">1.12.2</span><span class="sxs-lookup"><span data-stu-id="a8738-320">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="a8738-321">2017 年 3 月 20 日</span><span class="sxs-lookup"><span data-stu-id="a8738-321">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-322">1.12.1</span><span class="sxs-lookup"><span data-stu-id="a8738-322">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="a8738-323">2017 年 3 月 14 日</span><span class="sxs-lookup"><span data-stu-id="a8738-323">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-324">1.12.0</span><span class="sxs-lookup"><span data-stu-id="a8738-324">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="a8738-325">2017 年 2 月 15 日</span><span class="sxs-lookup"><span data-stu-id="a8738-325">February 15, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-326">1.11.4</span><span class="sxs-lookup"><span data-stu-id="a8738-326">1.11.4</span></span>](#1.11.4) |<span data-ttu-id="a8738-327">2017 年 2 月 6 日</span><span class="sxs-lookup"><span data-stu-id="a8738-327">February 06, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-328">1.11.3</span><span class="sxs-lookup"><span data-stu-id="a8738-328">1.11.3</span></span>](#1.11.3) |<span data-ttu-id="a8738-329">2017 年 1 月 26 日</span><span class="sxs-lookup"><span data-stu-id="a8738-329">January 26, 2017</span></span> |--- |
| [<span data-ttu-id="a8738-330">1.11.1</span><span class="sxs-lookup"><span data-stu-id="a8738-330">1.11.1</span></span>](#1.11.1) |<span data-ttu-id="a8738-331">2016 年 12 月 21 日</span><span class="sxs-lookup"><span data-stu-id="a8738-331">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-332">1.11.0</span><span class="sxs-lookup"><span data-stu-id="a8738-332">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="a8738-333">2016 年 12 月 8 日</span><span class="sxs-lookup"><span data-stu-id="a8738-333">December 08, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-334">1.10.0</span><span class="sxs-lookup"><span data-stu-id="a8738-334">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="a8738-335">2016 年 9 月 27 日</span><span class="sxs-lookup"><span data-stu-id="a8738-335">September 27, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-336">1.9.5</span><span class="sxs-lookup"><span data-stu-id="a8738-336">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="a8738-337">2016 年 9 月 1 日</span><span class="sxs-lookup"><span data-stu-id="a8738-337">September 01, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-338">1.9.4</span><span class="sxs-lookup"><span data-stu-id="a8738-338">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="a8738-339">2016 年 8 月 24 日</span><span class="sxs-lookup"><span data-stu-id="a8738-339">August 24, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-340">1.9.3</span><span class="sxs-lookup"><span data-stu-id="a8738-340">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="a8738-341">2016 年 8 月 15 日</span><span class="sxs-lookup"><span data-stu-id="a8738-341">August 15, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-342">1.9.2</span><span class="sxs-lookup"><span data-stu-id="a8738-342">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="a8738-343">2016 年 7 月 23 日</span><span class="sxs-lookup"><span data-stu-id="a8738-343">July 23, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-344">1.8.0</span><span class="sxs-lookup"><span data-stu-id="a8738-344">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="a8738-345">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="a8738-345">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-346">1.7.1</span><span class="sxs-lookup"><span data-stu-id="a8738-346">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="a8738-347">2016 年 5 月 6 日</span><span class="sxs-lookup"><span data-stu-id="a8738-347">May 06, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-348">1.7.0</span><span class="sxs-lookup"><span data-stu-id="a8738-348">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="a8738-349">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="a8738-349">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-350">1.6.3</span><span class="sxs-lookup"><span data-stu-id="a8738-350">1.6.3</span></span>](#1.6.3) |<span data-ttu-id="a8738-351">2016 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="a8738-351">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-352">1.6.2</span><span class="sxs-lookup"><span data-stu-id="a8738-352">1.6.2</span></span>](#1.6.2) |<span data-ttu-id="a8738-353">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="a8738-353">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-354">1.5.3</span><span class="sxs-lookup"><span data-stu-id="a8738-354">1.5.3</span></span>](#1.5.3) |<span data-ttu-id="a8738-355">2016 年 2 月 19 日</span><span class="sxs-lookup"><span data-stu-id="a8738-355">February 19, 2016</span></span> |--- |
| [<span data-ttu-id="a8738-356">1.5.2</span><span class="sxs-lookup"><span data-stu-id="a8738-356">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="a8738-357">2015 年 12 月 14 日</span><span class="sxs-lookup"><span data-stu-id="a8738-357">December 14, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-358">1.5.1</span><span class="sxs-lookup"><span data-stu-id="a8738-358">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="a8738-359">2015 年 11 月 23 日</span><span class="sxs-lookup"><span data-stu-id="a8738-359">November 23, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-360">1.5.0</span><span class="sxs-lookup"><span data-stu-id="a8738-360">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="a8738-361">2015 年 10 月 5 日</span><span class="sxs-lookup"><span data-stu-id="a8738-361">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-362">1.4.1</span><span class="sxs-lookup"><span data-stu-id="a8738-362">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="a8738-363">2015 年 8 月 25 日</span><span class="sxs-lookup"><span data-stu-id="a8738-363">August 25, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-364">1.4.0</span><span class="sxs-lookup"><span data-stu-id="a8738-364">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="a8738-365">2015 年 8 月 13 日</span><span class="sxs-lookup"><span data-stu-id="a8738-365">August 13, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-366">1.3.0</span><span class="sxs-lookup"><span data-stu-id="a8738-366">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="a8738-367">2015 年 8 月 5 日</span><span class="sxs-lookup"><span data-stu-id="a8738-367">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-368">1.2.0</span><span class="sxs-lookup"><span data-stu-id="a8738-368">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="a8738-369">2015 年 7 月 6 日</span><span class="sxs-lookup"><span data-stu-id="a8738-369">July 06, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-370">1.1.0</span><span class="sxs-lookup"><span data-stu-id="a8738-370">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="a8738-371">2015 年 4 月 30 日</span><span class="sxs-lookup"><span data-stu-id="a8738-371">April 30, 2015</span></span> |--- |
| [<span data-ttu-id="a8738-372">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a8738-372">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="a8738-373">2015 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="a8738-373">April 08, 2015</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="a8738-374">常見問題集</span><span class="sxs-lookup"><span data-stu-id="a8738-374">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="a8738-375">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8738-375">See also</span></span>
<span data-ttu-id="a8738-376">若要深入了解 Cosmos DB，請參閱 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="a8738-376">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

