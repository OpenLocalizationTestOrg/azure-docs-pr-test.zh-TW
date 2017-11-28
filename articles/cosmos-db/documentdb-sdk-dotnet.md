---
title: "aaaAzure Cosmos DB.NET SDK 與資源 |Microsoft 文件"
description: ".NET API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB.NET SDK 的每個版本之間所做的變更，深入了解 hello。"
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
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a><span data-ttu-id="49f34-103">Azure Cosmos DB .NET SDK：下載和版本資訊</span><span class="sxs-lookup"><span data-stu-id="49f34-103">Azure Cosmos DB .NET SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49f34-104">.NET</span><span class="sxs-lookup"><span data-stu-id="49f34-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="49f34-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="49f34-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="49f34-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="49f34-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="49f34-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="49f34-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="49f34-108">Java</span><span class="sxs-lookup"><span data-stu-id="49f34-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="49f34-109">Python</span><span class="sxs-lookup"><span data-stu-id="49f34-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="49f34-110">REST</span><span class="sxs-lookup"><span data-stu-id="49f34-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="49f34-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="49f34-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="49f34-112">SQL</span><span class="sxs-lookup"><span data-stu-id="49f34-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="49f34-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="49f34-113">**SDK download**</span></span></td><td>[<span data-ttu-id="49f34-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="49f34-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td><span data-ttu-id="49f34-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="49f34-115">**API documentation**</span></span></td><td>[<span data-ttu-id="49f34-116">.NET API 參考文件</span><span class="sxs-lookup"><span data-stu-id="49f34-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="49f34-117">**範例**</span><span class="sxs-lookup"><span data-stu-id="49f34-117">**Samples**</span></span></td><td>[<span data-ttu-id="49f34-118">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="49f34-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="49f34-119">**快速入門**</span><span class="sxs-lookup"><span data-stu-id="49f34-119">**Get started**</span></span></td><td>[<span data-ttu-id="49f34-120">開始使用 hello Azure Cosmos DB.NET SDK</span><span class="sxs-lookup"><span data-stu-id="49f34-120">Get started with hello Azure Cosmos DB .NET SDK</span></span>](documentdb-get-started.md)</td></tr>

<tr><td><span data-ttu-id="49f34-121">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="49f34-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="49f34-122">使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="49f34-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="49f34-123">**目前支援的架構**</span><span class="sxs-lookup"><span data-stu-id="49f34-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="49f34-124">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="49f34-124">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="49f34-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="49f34-125">Release notes</span></span>

### <a name="a-name11701170"></a><span data-ttu-id="49f34-126"><a name="1.17.0"/>1.17.0</span><span class="sxs-lookup"><span data-stu-id="49f34-126"><a name="1.17.0"/>1.17.0</span></span> 

* <span data-ttu-id="49f34-127">PartitionKeyRangeId FeedOption 的查詢結果 tooa 特定的資料分割索引鍵的範圍值的範圍設定為已加入的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-127">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="49f34-128">StartTime 為 ChangeFeedOption toostart hello 變更尋找該時間之後所新增的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-128">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span>

### <a name="a-name11611161"></a><span data-ttu-id="49f34-129"><a name="1.16.1"/>1.16.1</span><span class="sxs-lookup"><span data-stu-id="49f34-129"><a name="1.16.1"/>1.16.1</span></span>
* <span data-ttu-id="49f34-130">Hello JsonSerializable 類別可能會造成堆疊溢位例外狀況中修正的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-130">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name11601160"></a><span data-ttu-id="49f34-131"><a name="1.16.0"/>1.16.0</span><span class="sxs-lookup"><span data-stu-id="49f34-131"><a name="1.16.0"/>1.16.0</span></span>
*   <span data-ttu-id="49f34-132">已修正的問題，需要重新編譯的 hello 應用程式到期的 JsonSerializerSettings toohello 簡介做 hello DocumentClient 建構函式中為選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="49f34-132">Fixed an issue that required recompiling of hello application due toohello introduction of JsonSerializerSettings as an optional parameter in hello DocumentClient constructor.</span></span>
* <span data-ttu-id="49f34-133">標示的 hello DocumentClient 建構函式已經過時 hello ConnectionPolicy 和 ConsistencyLevel 參數的預設值的最後一個參數 tooallow JsonSerializerSettings 參數中傳遞時需要 JsonSerializerSettings。</span><span class="sxs-lookup"><span data-stu-id="49f34-133">Marked hello DocumentClient constructor obsolete that required JsonSerializerSettings as hello last parameter tooallow for default values of ConnectionPolicy and ConsistencyLevel parameters when passing in JsonSerializerSettings parameter.</span></span>

### <a name="a-name11501150"></a><span data-ttu-id="49f34-134"><a name="1.15.0"/>1.15.0</span><span class="sxs-lookup"><span data-stu-id="49f34-134"><a name="1.15.0"/>1.15.0</span></span>
*   <span data-ttu-id="49f34-135">已新增對 [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 具現化時指定自訂 JsonSerializerSettings 的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-135">Added support for specifying custom JsonSerializerSettings while instantiating [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span></span>

### <a name="a-name11411141"></a><span data-ttu-id="49f34-136"><a name="1.14.1"/>1.14.1</span><span class="sxs-lookup"><span data-stu-id="49f34-136"><a name="1.14.1"/>1.14.1</span></span>
*   <span data-ttu-id="49f34-137">針對不支援 SSE4 指令的 x64 電腦，已修正執行 Azure Cosmos DB API 查詢時，這類電腦會擲回 SEHException 的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-137">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw an SEHException when running Azure Cosmos DB DocumentDB API queries.</span></span>

### <a name="a-name11401140"></a><span data-ttu-id="49f34-138"><a name="1.14.0"/>1.14.0</span><span class="sxs-lookup"><span data-stu-id="49f34-138"><a name="1.14.0"/>1.14.0</span></span>
*   <span data-ttu-id="49f34-139">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-139">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="49f34-140">已新增對個別資料分割之查詢計量的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-140">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="49f34-141">限制查詢的 hello 接續 token 的 hello 大小新增的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-141">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="49f34-142">已新增對失敗要求進行更詳細追蹤的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-142">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="49f34-143">Hello SDK 中進行一些效能改進。</span><span class="sxs-lookup"><span data-stu-id="49f34-143">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name11341134"></a><span data-ttu-id="49f34-144"><a name="1.13.4"/>1.13.4</span><span class="sxs-lookup"><span data-stu-id="49f34-144"><a name="1.13.4"/>1.13.4</span></span>
* <span data-ttu-id="49f34-145">在功能上與 1.13.3 相同。</span><span class="sxs-lookup"><span data-stu-id="49f34-145">Functionally same as 1.13.3.</span></span> <span data-ttu-id="49f34-146">已有一些內部變更。</span><span class="sxs-lookup"><span data-stu-id="49f34-146">Made some internal changes.</span></span>

### <a name="a-name11331133"></a><span data-ttu-id="49f34-147"><a name="1.13.3"/>1.13.3</span><span class="sxs-lookup"><span data-stu-id="49f34-147"><a name="1.13.3"/>1.13.3</span></span>
* <span data-ttu-id="49f34-148">在功能上與 1.13.2 相同。</span><span class="sxs-lookup"><span data-stu-id="49f34-148">Functionally same as 1.13.2.</span></span> <span data-ttu-id="49f34-149">已有一些內部變更。</span><span class="sxs-lookup"><span data-stu-id="49f34-149">Made some internal changes.</span></span>

### <a name="a-name11321132"></a><span data-ttu-id="49f34-150"><a name="1.13.2"/>1.13.2</span><span class="sxs-lookup"><span data-stu-id="49f34-150"><a name="1.13.2"/>1.13.2</span></span>
* <span data-ttu-id="49f34-151">修正忽略 hello PartitionKey 值的彙總查詢 FeedOptions 中提供的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-151">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="49f34-152">修正在執行移動途中跨資料分割 Order By 查詢期間，進行資料分割管理的透明處理時發生的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-152">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name11311131"></a><span data-ttu-id="49f34-153"><a name="1.13.1"/>1.13.1</span><span class="sxs-lookup"><span data-stu-id="49f34-153"><a name="1.13.1"/>1.13.1</span></span>
* <span data-ttu-id="49f34-154">修正造成死結的某些資料 hello 非同步 Api ASP.NET 內容中使用時的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-154">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name11301130"></a><span data-ttu-id="49f34-155"><a name="1.13.0"/>1.13.0</span><span class="sxs-lookup"><span data-stu-id="49f34-155"><a name="1.13.0"/>1.13.0</span></span>
* <span data-ttu-id="49f34-156">修正 toomake SDK 更多彈性 tooautomatic 容錯移轉，在某些情況下的。</span><span class="sxs-lookup"><span data-stu-id="49f34-156">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name11221122"></a><span data-ttu-id="49f34-157"><a name="1.12.2"/>1.12.2</span><span class="sxs-lookup"><span data-stu-id="49f34-157"><a name="1.12.2"/>1.12.2</span></span>
* <span data-ttu-id="49f34-158">偶爾會造成 WebException 可解決問題的修正： 無法解析 hello 遠端名稱。</span><span class="sxs-lookup"><span data-stu-id="49f34-158">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="49f34-159">加入的 hello 支援直接讀取藉由新增新的多載 tooReadDocumentAsync API 的具類型的文件。</span><span class="sxs-lookup"><span data-stu-id="49f34-159">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name11211121"></a><span data-ttu-id="49f34-160"><a name="1.12.1"/>1.12.1</span><span class="sxs-lookup"><span data-stu-id="49f34-160"><a name="1.12.1"/>1.12.1</span></span>
* <span data-ttu-id="49f34-161">新增彙總查詢的 LINQ 支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="49f34-161">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="49f34-162">為記憶體流失問題的事件處理常式的 hello 使用所造成的 hello ConnectionPolicy 物件解決問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-162">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="49f34-163">修正使用 ETag 時 UpsertAttachmentAsync 無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-163">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="49f34-164">修正根據字串欄位排序時交叉資料分割排序依據查詢接續無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-164">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="49f34-165"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="49f34-165"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="49f34-166">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="49f34-166">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="49f34-167">請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。</span><span class="sxs-lookup"><span data-stu-id="49f34-167">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="49f34-168">降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。</span><span class="sxs-lookup"><span data-stu-id="49f34-168">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name11141114"></a><span data-ttu-id="49f34-169"><a name="1.11.4"/>1.11.4</span><span class="sxs-lookup"><span data-stu-id="49f34-169"><a name="1.11.4"/>1.11.4</span></span>
* <span data-ttu-id="49f34-170">其中某些 hello 跨資料分割查詢在 hello 32 位元主控件程序失敗的問題的修正。</span><span class="sxs-lookup"><span data-stu-id="49f34-170">Fix for an issue wherein some of hello cross-partition queries were failing in hello 32-bit host process.</span></span>
* <span data-ttu-id="49f34-171">其中 hello 工作階段的容器不更新與 hello 閘道模式中的失敗要求的語彙基元可解決問題的修正。</span><span class="sxs-lookup"><span data-stu-id="49f34-171">Fix for an issue wherein hello session container was not being updated with hello token for failed requests in Gateway mode.</span></span>
* <span data-ttu-id="49f34-172">修正縱向選取中具有 UDF 呼叫的查詢在某些案例中失敗的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-172">Fix for an issue wherein a query with UDF calls in projection was failing in some cases.</span></span>
* <span data-ttu-id="49f34-173">用戶端端效能修正增加 hello 讀寫 hello 要求輸送量。</span><span class="sxs-lookup"><span data-stu-id="49f34-173">Client side performance fixes for increasing hello read and write throughput of hello requests.</span></span>

### <a name="a-name11131113"></a><span data-ttu-id="49f34-174"><a name="1.11.3"/>1.11.3</span><span class="sxs-lookup"><span data-stu-id="49f34-174"><a name="1.11.3"/>1.11.3</span></span>
* <span data-ttu-id="49f34-175">其中 hello 工作階段的容器不更新與 hello 語彙基元可解決問題的修正失敗的要求。</span><span class="sxs-lookup"><span data-stu-id="49f34-175">Fix for an issue wherein hello session container was not being updated with hello token for failed requests.</span></span>
* <span data-ttu-id="49f34-176">在 32 位元主控件程序中的 hello SDK toowork 加入的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-176">Added support for hello SDK toowork in a 32-bit host process.</span></span> <span data-ttu-id="49f34-177">請注意，若使用跨分割區查詢，建議您使用 64 位元主機處理以獲得改進的效能。</span><span class="sxs-lookup"><span data-stu-id="49f34-177">Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.</span></span>
* <span data-ttu-id="49f34-178">改進關於 IN 運算式中涉及大量分割區索引鍵值之查詢案例的效能。</span><span class="sxs-lookup"><span data-stu-id="49f34-178">Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.</span></span>
* <span data-ttu-id="49f34-179">文件集合讀取要求，當 PopulateQuotaInfo 要求選項設定，請填入 hello ResourceResponse 中的各種資源配額統計資料。</span><span class="sxs-lookup"><span data-stu-id="49f34-179">Populated various resource quota stats in hello ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.</span></span>

### <a name="a-name11111111"></a><span data-ttu-id="49f34-180"><a name="1.11.1"/>1.11.1</span><span class="sxs-lookup"><span data-stu-id="49f34-180"><a name="1.11.1"/>1.11.1</span></span>
* <span data-ttu-id="49f34-181">Hello CreateDocumentCollectionIfNotExistsAsync API 1.11.0 中導入的小效能修正程式。</span><span class="sxs-lookup"><span data-stu-id="49f34-181">Minor performance fix for hello CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.</span></span>
* <span data-ttu-id="49f34-182">效能修正在 hello SDK 涉及高度並行要求的情形。</span><span class="sxs-lookup"><span data-stu-id="49f34-182">Performance fix in hello SDK for scenarios that involve high degree of concurrent requests.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="49f34-183"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="49f34-183"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="49f34-184">支援新的類別和方法 tooprocess hello[變更摘要](change-feed.md)集合內的文件。</span><span class="sxs-lookup"><span data-stu-id="49f34-184">Support for new classes and methods tooprocess hello [change feed](change-feed.md) of documents within a collection.</span></span>
* <span data-ttu-id="49f34-185">支援跨資料分割繼續查詢和改善跨資料分割查詢的一些效能。</span><span class="sxs-lookup"><span data-stu-id="49f34-185">Support for cross-partition query continuation and some perf improvements for cross-partition queries.</span></span>
* <span data-ttu-id="49f34-186">新增 CreateDatabaseIfNotExistsAsync 和 CreateDocumentCollectionIfNotExistsAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="49f34-186">Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.</span></span>
* <span data-ttu-id="49f34-187">針對下列系統函式支援 LINQ︰IsDefined、IsNull 和 IsPrimitive。</span><span class="sxs-lookup"><span data-stu-id="49f34-187">LINQ support for system functions: IsDefined, IsNull and IsPrimitive.</span></span>
* <span data-ttu-id="49f34-188">搭配有 project.json 工具的專案使用 hello Nuget 封裝時，請修正自動 binplacing 的 Microsoft.Azure.Documents.ServiceInterop.dll 和 DocumentDB.Spatial.Sql.dll 組件 tooapplication 的 bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="49f34-188">Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies tooapplication’s bin folder when using hello Nuget package with projects that have project.json tooling.</span></span>
* <span data-ttu-id="49f34-189">支援發出用戶端 ETW 追蹤，其可在偵錯案例中幫上忙。</span><span class="sxs-lookup"><span data-stu-id="49f34-189">Support for emitting client side ETW traces which could be helpful in debugging scenarios.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="49f34-190"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="49f34-190"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="49f34-191">新增分割集合的直接連線支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-191">Added direct connectivity support for partitioned collections.</span></span>
* <span data-ttu-id="49f34-192">經改善 hello 繫結失效的一致性層級的效能。</span><span class="sxs-lookup"><span data-stu-id="49f34-192">Improved performance for hello Bounded Staleness consistency level.</span></span>
* <span data-ttu-id="49f34-193">新增為異地隔離空間查詢指定集合索引編製原則時的 Polygon 和 LineString 資料類型。</span><span class="sxs-lookup"><span data-stu-id="49f34-193">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="49f34-194">新增轉譯述詞時對 StringEnumConverter、IsoDateTimeConverter、UnixDateTimeConverter 的 LINQ 支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-194">Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.</span></span>
* <span data-ttu-id="49f34-195">多項 SDK 錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="49f34-195">Various SDK bug fixes.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="49f34-196"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="49f34-196"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="49f34-197">已修正的問題，造成的 hello 遵循 NotFoundException: hello 讀取工作階段不是供 hello 輸入工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="49f34-197">Fixed an issue that caused hello following NotFoundException: hello read session is not available for hello input session token.</span></span> <span data-ttu-id="49f34-198">查詢 hello 讀取地區之地理分散的帳戶時，在某些情況下發生此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="49f34-198">This exception occurred in some cases when querying for hello read-region of a geo-distributed account.</span></span>
* <span data-ttu-id="49f34-199">公開 hello ResourceResponse 類別，讓直接存取 toohello 基礎資料流從回應中的 hello ResponseStream 屬性。</span><span class="sxs-lookup"><span data-stu-id="49f34-199">Exposed hello ResponseStream property in hello ResourceResponse class, which enables direct access toohello underlying stream from a response.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="49f34-200"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="49f34-200"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="49f34-201">修改過的 hello ResourceResponse、 FeedResponse、 StoredProcedureResponse 和 MediaResponse 類別 tooimplement hello 對應公用介面，以便它們可以模仿的測試為導向的部署 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="49f34-201">Modified hello ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes tooimplement hello corresponding public interface so that they can be mocked for test driven deployment (TDD).</span></span>
* <span data-ttu-id="49f34-202">修正了使用自訂 JsonSerializerSettings 物件來序列化資料時，會造成資料分割索引鍵標頭格式不正確的問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-202">Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="49f34-203"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="49f34-203"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="49f34-204">已修正的問題造成長時間執行的查詢 toofail 發生錯誤： 授權權杖無效，無法在 hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="49f34-204">Fixed an issue that caused long running queries toofail with error: Authorization token is not valid at hello current time.</span></span>
* <span data-ttu-id="49f34-205">固定移除問題 hello 原始 SqlParameterCollection 從跨資料分割 top/排序依據查詢。</span><span class="sxs-lookup"><span data-stu-id="49f34-205">Fixed an issue that removed hello original SqlParameterCollection from cross partition top/order-by queries.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="49f34-206"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="49f34-206"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="49f34-207">已新增分割集合的平行查詢支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-207">Added support for parallel queries for partitioned collections.</span></span>
* <span data-ttu-id="49f34-208">已新增分割集合的跨資料分割 ORDER BY 和 TOP 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-208">Added support for cross partition ORDER BY and TOP queries for partitioned collections.</span></span>
* <span data-ttu-id="49f34-209">遺漏參考 tooDocumentDB.Spatial.Sql.dll 和 Microsoft.Azure.Documents.ServiceInterop.dll 參考參考 toohello Azure Cosmos DB Nuget 套件的 Azure Cosmos DB 專案時所需的固定的 hello。</span><span class="sxs-lookup"><span data-stu-id="49f34-209">Fixed hello missing references tooDocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing an Azure Cosmos DB project with a reference toohello Azure Cosmos DB Nuget package.</span></span>
* <span data-ttu-id="49f34-210">固定的 hello 能力 toouse LINQ 中使用使用者定義函數時的不同類型的參數。</span><span class="sxs-lookup"><span data-stu-id="49f34-210">Fixed hello ability toouse parameters of different types when using user-defined functions in LINQ.</span></span> 
* <span data-ttu-id="49f34-211">修正 bug 的全球複寫帳戶其中 Upsert 呼叫已導向的 tooread 位置，而非寫入位置。</span><span class="sxs-lookup"><span data-stu-id="49f34-211">Fixed a bug for globally replicated accounts where Upsert calls were being directed tooread locations instead of write locations.</span></span>
* <span data-ttu-id="49f34-212">遺漏了加入的方法 toohello IDocumentClient 介面：</span><span class="sxs-lookup"><span data-stu-id="49f34-212">Added methods toohello IDocumentClient interface that were missing:</span></span> 
  * <span data-ttu-id="49f34-213">UpsertAttachmentAsync 方法，會接受 mediaStream 及選項做為參數</span><span class="sxs-lookup"><span data-stu-id="49f34-213">UpsertAttachmentAsync method that takes mediaStream and options as parameters</span></span>
  * <span data-ttu-id="49f34-214">CreateAttachmentAsync 方法，會接受選項做為參數</span><span class="sxs-lookup"><span data-stu-id="49f34-214">CreateAttachmentAsync method that takes options as a parameter</span></span>
  * <span data-ttu-id="49f34-215">CreateOfferQuery 方法，會接受 querySpec 做為參數</span><span class="sxs-lookup"><span data-stu-id="49f34-215">CreateOfferQuery method that takes querySpec as a parameter.</span></span>
* <span data-ttu-id="49f34-216">非密封的 hello IDocumentClient 介面中公開的公用類別。</span><span class="sxs-lookup"><span data-stu-id="49f34-216">Unsealed public classes that are exposed in hello IDocumentClient interface.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="49f34-217"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="49f34-217"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="49f34-218">加入的 hello 支援多重地區資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="49f34-218">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="49f34-219">新增在已節流處理的要求上進行重試的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-219">Added support for retry on throttled requests.</span></span>  <span data-ttu-id="49f34-220">使用者可以自訂 hello 重試次數和 hello 最大等待時間藉由設定 hello ConnectionPolicy.RetryOptions 屬性。</span><span class="sxs-lookup"><span data-stu-id="49f34-220">User can customize hello number of retries and hello max wait time by configuring hello ConnectionPolicy.RetryOptions property.</span></span>
* <span data-ttu-id="49f34-221">加入新的 IDocumentClient 介面定義所有 DocumenClient 屬性及方法的 hello 簽章。</span><span class="sxs-lookup"><span data-stu-id="49f34-221">Added a new IDocumentClient interface that defines hello signatures of all DocumenClient properties and methods.</span></span>  <span data-ttu-id="49f34-222">這項變更的一部分，也變更 hello DocumentClient 類別本身建立 IQueryable 和 IOrderedQueryable toomethods 的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="49f34-222">As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable toomethods on hello DocumentClient class itself.</span></span>
* <span data-ttu-id="49f34-223">新增組態選項 tooset hello ServicePoint.ConnectionLimit 特定 Azure Cosmos DB 端點 Uri。</span><span class="sxs-lookup"><span data-stu-id="49f34-223">Added configuration option tooset hello ServicePoint.ConnectionLimit for a given Azure Cosmos DB endpoint Uri.</span></span>  <span data-ttu-id="49f34-224">使用 ConnectionPolicy.MaxConnectionLimit toochange hello 預設值，它會設定 too50。</span><span class="sxs-lookup"><span data-stu-id="49f34-224">Use ConnectionPolicy.MaxConnectionLimit toochange hello default value, which is set too50.</span></span>
* <span data-ttu-id="49f34-225">已淘汰 IPartitionResolver 及其實作。</span><span class="sxs-lookup"><span data-stu-id="49f34-225">Deprecated IPartitionResolver and its implementation.</span></span>  <span data-ttu-id="49f34-226">現在不支援 IPartitionResolver。</span><span class="sxs-lookup"><span data-stu-id="49f34-226">Support for IPartitionResolver is now obsolete.</span></span> <span data-ttu-id="49f34-227">建議您針對更高的儲存體和輸送量使用分割集合。</span><span class="sxs-lookup"><span data-stu-id="49f34-227">It's recommended that you use Partitioned Collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="49f34-228"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="49f34-228"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="49f34-229">加入多載 tooUri 型 ExecuteStoredProcedureAsync 方法採用 RequestOptions 做為參數。</span><span class="sxs-lookup"><span data-stu-id="49f34-229">Added an overload tooUri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="49f34-230"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="49f34-230"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="49f34-231">加入時間 toolive (TTL) 支援的文件。</span><span class="sxs-lookup"><span data-stu-id="49f34-231">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name163163"></a><span data-ttu-id="49f34-232"><a name="1.6.3"/>1.6.3</span><span class="sxs-lookup"><span data-stu-id="49f34-232"><a name="1.6.3"/>1.6.3</span></span>
* <span data-ttu-id="49f34-233">修正 .NET SDK 的 Nuget 封裝錯誤，可供封裝為 Azure 雲端服務解決方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="49f34-233">Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.</span></span>

### <a name="a-name162162"></a><span data-ttu-id="49f34-234"><a name="1.6.2"/>1.6.2</span><span class="sxs-lookup"><span data-stu-id="49f34-234"><a name="1.6.2"/>1.6.2</span></span>
* <span data-ttu-id="49f34-235">實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="49f34-235">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name153153"></a><span data-ttu-id="49f34-236"><a name="1.5.3"/>1.5.3</span><span class="sxs-lookup"><span data-stu-id="49f34-236"><a name="1.5.3"/>1.5.3</span></span>
* <span data-ttu-id="49f34-237">**[固定]**查詢 Azure DB Cosmos 端點就會擲回: ' System.Net.Http.HttpRequestException： 複製內容 tooa 資料流時發生錯誤 '。</span><span class="sxs-lookup"><span data-stu-id="49f34-237">**[Fixed]** Querying Azure Cosmos DB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content tooa stream'.</span></span>

### <a name="a-name152152"></a><span data-ttu-id="49f34-238"><a name="1.5.2"/>1.5.2</span><span class="sxs-lookup"><span data-stu-id="49f34-238"><a name="1.5.2"/>1.5.2</span></span>
* <span data-ttu-id="49f34-239">擴充的 LINQ 支援包括新的分頁、條件式運算式以及範圍比較的運算子。</span><span class="sxs-lookup"><span data-stu-id="49f34-239">Expanded LINQ support including new operators for paging, conditional expressions, and range comparison.</span></span>
  * <span data-ttu-id="49f34-240">進行 LINQ 運算子 tooenable 選取前行為</span><span class="sxs-lookup"><span data-stu-id="49f34-240">Take operator tooenable SELECT TOP behavior in LINQ</span></span>
  * <span data-ttu-id="49f34-241">CompareTo 運算子 tooenable 字串範圍比較</span><span class="sxs-lookup"><span data-stu-id="49f34-241">CompareTo operator tooenable string range comparisons</span></span>
  * <span data-ttu-id="49f34-242">條件式 (?) 與聯合運算子 (??)</span><span class="sxs-lookup"><span data-stu-id="49f34-242">Conditional (?) and coalesce operators (??)</span></span>
* <span data-ttu-id="49f34-243">**[已修正]** 將模型投射與 LINQ 查詢中的 Where-In 結合使用時發生 ArgumentOutOfRangeException。</span><span class="sxs-lookup"><span data-stu-id="49f34-243">**[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in a LINQ query.</span></span> [<span data-ttu-id="49f34-244">#81</span><span class="sxs-lookup"><span data-stu-id="49f34-244">#81</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><span data-ttu-id="49f34-245"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="49f34-245"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="49f34-246">**[固定]**如果選取不是最後一個運算式 hello hello LINQ 提供者假設投射，而且產生 SELECT * 不正確。</span><span class="sxs-lookup"><span data-stu-id="49f34-246">**[Fixed]** If Select is not hello last expression hello LINQ Provider assumed no projection and produced SELECT * incorrectly.</span></span>  [<span data-ttu-id="49f34-247">#58</span><span class="sxs-lookup"><span data-stu-id="49f34-247">#58</span></span>](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><span data-ttu-id="49f34-248"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="49f34-248"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="49f34-249">實作 Upsert、新增 UpsertXXXAsync 方法</span><span class="sxs-lookup"><span data-stu-id="49f34-249">Implemented Upsert, Added UpsertXXXAsync methods</span></span>
* <span data-ttu-id="49f34-250">所有要求的效能改進</span><span class="sxs-lookup"><span data-stu-id="49f34-250">Performance improvements for all requests</span></span>
* <span data-ttu-id="49f34-251">LINQ 提供者支援字串的條件式、聯合和 CompareTo 方法</span><span class="sxs-lookup"><span data-stu-id="49f34-251">LINQ Provider support for conditional, coalesce, and CompareTo methods for strings</span></span>
* <span data-ttu-id="49f34-252">**[固定]** LINQ 提供者--> 實作是否包含在清單 toogenerate 方法 hello 上 IEnumerable 和陣列相同的 SQL</span><span class="sxs-lookup"><span data-stu-id="49f34-252">**[Fixed]** LINQ provider --> Implement Contains method on List toogenerate hello same SQL as on IEnumerable and Array</span></span>
* <span data-ttu-id="49f34-253">**[固定]** BackoffRetryUtility 使用 hello 相同的 HttpRequestMessage，而不要建立新的重試</span><span class="sxs-lookup"><span data-stu-id="49f34-253">**[Fixed]** BackoffRetryUtility uses hello same HttpRequestMessage again instead of creating a new one on retry</span></span>
* <span data-ttu-id="49f34-254">**[已過時]** UriFactory.CreateCollection --> 現應使用 UriFactory.CreateDocumentCollection</span><span class="sxs-lookup"><span data-stu-id="49f34-254">**[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection</span></span>

### <a name="a-name141141"></a><span data-ttu-id="49f34-255"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="49f34-255"><a name="1.4.1"/>1.4.1</span></span>
* <span data-ttu-id="49f34-256">**[已修正]** 使用非 en 文化特性資訊時 (例如 nl-NL 等) 的當地語系化問題。</span><span class="sxs-lookup"><span data-stu-id="49f34-256">**[Fixed]** Localization issues when using non en culture info such as nl-NL, etc.</span></span> 

### <a name="a-name140140"></a><span data-ttu-id="49f34-257"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="49f34-257"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="49f34-258">已新增以識別碼為基礎的路由</span><span class="sxs-lookup"><span data-stu-id="49f34-258">Added ID-based routing</span></span>
  * <span data-ttu-id="49f34-259">新的 UriFactory helper tooassist 建構 ID 為基礎的資源連結</span><span class="sxs-lookup"><span data-stu-id="49f34-259">New UriFactory helper tooassist with constructing ID-based resource links</span></span>
  * <span data-ttu-id="49f34-260">在 URI 中 DocumentClient tootake 上的新多載</span><span class="sxs-lookup"><span data-stu-id="49f34-260">New overloads on DocumentClient tootake in URI</span></span>
* <span data-ttu-id="49f34-261">LINQ 中新增用於地理空間的 IsValid() 和 isvaliddetailed ()</span><span class="sxs-lookup"><span data-stu-id="49f34-261">Added IsValid() and IsValidDetailed() in LINQ for geospatial</span></span>
* <span data-ttu-id="49f34-262">增強的 LINQ 提供者支援：</span><span class="sxs-lookup"><span data-stu-id="49f34-262">LINQ Provider support enhanced:</span></span>
  * <span data-ttu-id="49f34-263">**算術** - Abs、Acos、Asin、Atan、Ceiling、Cos、Exp、Floor、Log、Log10、Pow、Round、Sign、Sin、Sqrt、Tan、Truncate</span><span class="sxs-lookup"><span data-stu-id="49f34-263">**Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate</span></span>
  * <span data-ttu-id="49f34-264">**字串** - Concat、Contains、EndsWith、IndexOf、Count、ToLower、TrimStart、Replace、Reverse、TrimEnd、StartsWith、SubString、ToUpper</span><span class="sxs-lookup"><span data-stu-id="49f34-264">**String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper</span></span>
  * <span data-ttu-id="49f34-265">**陣列** - Concat、Contains、Count</span><span class="sxs-lookup"><span data-stu-id="49f34-265">**Array** - Concat, Contains, Count</span></span>
  * <span data-ttu-id="49f34-266">**IN** 運算子</span><span class="sxs-lookup"><span data-stu-id="49f34-266">**IN** operator</span></span>

### <a name="a-name130130"></a><span data-ttu-id="49f34-267"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="49f34-267"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="49f34-268">新增修改索引編製原則的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-268">Added support for modifying indexing policies.</span></span>
  * <span data-ttu-id="49f34-269">DocumentClient 中新的 ReplaceDocumentCollectionAsync 方法</span><span class="sxs-lookup"><span data-stu-id="49f34-269">New ReplaceDocumentCollectionAsync method in DocumentClient</span></span>
  * <span data-ttu-id="49f34-270">ResourceResponse 中新的 IndexTransformationProgress 屬性<T>可追蹤索引原則變更的百分比進度</span><span class="sxs-lookup"><span data-stu-id="49f34-270">New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes</span></span>
  * <span data-ttu-id="49f34-271">DocumentCollection.IndexingPolicy 現在可變動</span><span class="sxs-lookup"><span data-stu-id="49f34-271">DocumentCollection.IndexingPolicy is now mutable</span></span>
* <span data-ttu-id="49f34-272">新增空間索引編製和查詢的支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-272">Added support for spatial indexing and query.</span></span>
  * <span data-ttu-id="49f34-273">新的 Microsoft.Azure.Documents.Spatial 命名空間，可序列化/還原序列化空間類型，例如 Point 和 Polygon</span><span class="sxs-lookup"><span data-stu-id="49f34-273">New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon</span></span>
  * <span data-ttu-id="49f34-274">新的 SpatialIndex 類別，可對儲存在 Cosmos DB 中的 GeoJSON 資料編製索引</span><span class="sxs-lookup"><span data-stu-id="49f34-274">New SpatialIndex class for indexing GeoJSON data stored in Cosmos DB</span></span>
* <span data-ttu-id="49f34-275">**[已修正]**：從 LINQ 運算式產生的 SQL 查詢不正確 [#38](https://github.com/Azure/azure-documentdb-net/issues/38) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="49f34-275">**[Fixed]** Incorrect SQL query generated from a LINQ expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38).</span></span>

### <a name="a-name120120"></a><span data-ttu-id="49f34-276"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="49f34-276"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="49f34-277">已新增對 Newtonsoft.Json v5.0.7 的相依性。</span><span class="sxs-lookup"><span data-stu-id="49f34-277">Added a dependency on Newtonsoft.Json v5.0.7.</span></span>
* <span data-ttu-id="49f34-278">Order By 做的變更 toosupport:</span><span class="sxs-lookup"><span data-stu-id="49f34-278">Made changes toosupport Order By:</span></span>
  
  * <span data-ttu-id="49f34-279">LINQ 提供者支援 OrderBy() 或 OrderByDescending()</span><span class="sxs-lookup"><span data-stu-id="49f34-279">LINQ provider support for OrderBy() or OrderByDescending()</span></span>
  * <span data-ttu-id="49f34-280">IndexingPolicy toosupport Order By</span><span class="sxs-lookup"><span data-stu-id="49f34-280">IndexingPolicy toosupport Order By</span></span> 
    
    <span data-ttu-id="49f34-281">**可能使得舊程式碼無法運作的變更**</span><span class="sxs-lookup"><span data-stu-id="49f34-281">**Possible breaking change**</span></span> 
    
    <span data-ttu-id="49f34-282">如果您有現有的程式碼以自訂的編製索引原則，會佈建集合，您現有的程式碼需要 toobe 更新 toosupport hello 新 IndexingPolicy 類別。</span><span class="sxs-lookup"><span data-stu-id="49f34-282">If you have existing code that provisions collections with a custom indexing policy, then your existing code needs toobe updated toosupport hello new IndexingPolicy class.</span></span> <span data-ttu-id="49f34-283">如果您沒有自訂的索引原則，這個變更不會影響到您。</span><span class="sxs-lookup"><span data-stu-id="49f34-283">If you have no custom indexing policy, then this change does not affect you.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="49f34-284"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="49f34-284"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="49f34-285">加入的資料分割使用 hello 新 HashPartitionResolver 和 RangePartitionResolver 類別和 hello ipartitionresolver 型支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-285">Added support for partitioning data by using hello new HashPartitionResolver and RangePartitionResolver classes and hello IPartitionResolver.</span></span>
* <span data-ttu-id="49f34-286">已新增 DataContract 序列化。</span><span class="sxs-lookup"><span data-stu-id="49f34-286">Added DataContract serialization.</span></span>
* <span data-ttu-id="49f34-287">已新增 LINQ 提供者中的 GUID 支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-287">Added GUID support in LINQ provider.</span></span>
* <span data-ttu-id="49f34-288">已新增 LINQ 中的 UDF 支援。</span><span class="sxs-lookup"><span data-stu-id="49f34-288">Added UDF support in LINQ.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="49f34-289"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="49f34-289"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="49f34-290">GA SDK</span><span class="sxs-lookup"><span data-stu-id="49f34-290">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="49f34-291">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="49f34-291">Release & Retirement dates</span></span>
<span data-ttu-id="49f34-292">Microsoft 至少提供通知**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。</span><span class="sxs-lookup"><span data-stu-id="49f34-292">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="49f34-293">新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議您，您一律升級 toohello 最新版本 SDK 盡早。</span><span class="sxs-lookup"><span data-stu-id="49f34-293">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="49f34-294">Hello 服務將會拒絕任何要求 tooAzure Cosmos DB 使用已淘汰的 SDK。</span><span class="sxs-lookup"><span data-stu-id="49f34-294">Any requests tooAzure Cosmos DB using a retired SDK are rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="49f34-295">版本</span><span class="sxs-lookup"><span data-stu-id="49f34-295">Version</span></span> | <span data-ttu-id="49f34-296">發行日期</span><span class="sxs-lookup"><span data-stu-id="49f34-296">Release Date</span></span> | <span data-ttu-id="49f34-297">停用日期</span><span class="sxs-lookup"><span data-stu-id="49f34-297">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="49f34-298">1.17.0</span><span class="sxs-lookup"><span data-stu-id="49f34-298">1.17.0</span></span>](#1.17.0) |<span data-ttu-id="49f34-299">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="49f34-299">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-300">1.16.1</span><span class="sxs-lookup"><span data-stu-id="49f34-300">1.16.1</span></span>](#1.16.1) |<span data-ttu-id="49f34-301">2017 年 8 月 7 日</span><span class="sxs-lookup"><span data-stu-id="49f34-301">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-302">1.16.0</span><span class="sxs-lookup"><span data-stu-id="49f34-302">1.16.0</span></span>](#1.16.0) |<span data-ttu-id="49f34-303">2017 年 8 月 2 日</span><span class="sxs-lookup"><span data-stu-id="49f34-303">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-304">1.15.0</span><span class="sxs-lookup"><span data-stu-id="49f34-304">1.15.0</span></span>](#1.15.0) |<span data-ttu-id="49f34-305">2017 年 6 月 30 日</span><span class="sxs-lookup"><span data-stu-id="49f34-305">June 30, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-306">1.14.1</span><span class="sxs-lookup"><span data-stu-id="49f34-306">1.14.1</span></span>](#1.14.1) |<span data-ttu-id="49f34-307">2017 年 5 月 23 日</span><span class="sxs-lookup"><span data-stu-id="49f34-307">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-308">1.14.0</span><span class="sxs-lookup"><span data-stu-id="49f34-308">1.14.0</span></span>](#1.14.0) |<span data-ttu-id="49f34-309">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="49f34-309">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-310">1.13.4</span><span class="sxs-lookup"><span data-stu-id="49f34-310">1.13.4</span></span>](#1.13.4) |<span data-ttu-id="49f34-311">2017 年 5 月 09 日</span><span class="sxs-lookup"><span data-stu-id="49f34-311">May 09, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-312">1.13.3</span><span class="sxs-lookup"><span data-stu-id="49f34-312">1.13.3</span></span>](#1.13.3) |<span data-ttu-id="49f34-313">2017 年 5 月 06 日</span><span class="sxs-lookup"><span data-stu-id="49f34-313">May 06, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-314">1.13.2</span><span class="sxs-lookup"><span data-stu-id="49f34-314">1.13.2</span></span>](#1.13.2) |<span data-ttu-id="49f34-315">2017 年 4 月 19 日</span><span class="sxs-lookup"><span data-stu-id="49f34-315">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-316">1.13.1</span><span class="sxs-lookup"><span data-stu-id="49f34-316">1.13.1</span></span>](#1.13.1) |<span data-ttu-id="49f34-317">2017 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="49f34-317">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-318">1.13.0</span><span class="sxs-lookup"><span data-stu-id="49f34-318">1.13.0</span></span>](#1.13.0) |<span data-ttu-id="49f34-319">2017 年 3 月 24 日</span><span class="sxs-lookup"><span data-stu-id="49f34-319">March 24, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-320">1.12.2</span><span class="sxs-lookup"><span data-stu-id="49f34-320">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="49f34-321">2017 年 3 月 20 日</span><span class="sxs-lookup"><span data-stu-id="49f34-321">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-322">1.12.1</span><span class="sxs-lookup"><span data-stu-id="49f34-322">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="49f34-323">2017 年 3 月 14 日</span><span class="sxs-lookup"><span data-stu-id="49f34-323">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-324">1.12.0</span><span class="sxs-lookup"><span data-stu-id="49f34-324">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="49f34-325">2017 年 2 月 15 日</span><span class="sxs-lookup"><span data-stu-id="49f34-325">February 15, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-326">1.11.4</span><span class="sxs-lookup"><span data-stu-id="49f34-326">1.11.4</span></span>](#1.11.4) |<span data-ttu-id="49f34-327">2017 年 2 月 6 日</span><span class="sxs-lookup"><span data-stu-id="49f34-327">February 06, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-328">1.11.3</span><span class="sxs-lookup"><span data-stu-id="49f34-328">1.11.3</span></span>](#1.11.3) |<span data-ttu-id="49f34-329">2017 年 1 月 26 日</span><span class="sxs-lookup"><span data-stu-id="49f34-329">January 26, 2017</span></span> |--- |
| [<span data-ttu-id="49f34-330">1.11.1</span><span class="sxs-lookup"><span data-stu-id="49f34-330">1.11.1</span></span>](#1.11.1) |<span data-ttu-id="49f34-331">2016 年 12 月 21 日</span><span class="sxs-lookup"><span data-stu-id="49f34-331">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-332">1.11.0</span><span class="sxs-lookup"><span data-stu-id="49f34-332">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="49f34-333">2016 年 12 月 8 日</span><span class="sxs-lookup"><span data-stu-id="49f34-333">December 08, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-334">1.10.0</span><span class="sxs-lookup"><span data-stu-id="49f34-334">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="49f34-335">2016 年 9 月 27 日</span><span class="sxs-lookup"><span data-stu-id="49f34-335">September 27, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-336">1.9.5</span><span class="sxs-lookup"><span data-stu-id="49f34-336">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="49f34-337">2016 年 9 月 1 日</span><span class="sxs-lookup"><span data-stu-id="49f34-337">September 01, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-338">1.9.4</span><span class="sxs-lookup"><span data-stu-id="49f34-338">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="49f34-339">2016 年 8 月 24 日</span><span class="sxs-lookup"><span data-stu-id="49f34-339">August 24, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-340">1.9.3</span><span class="sxs-lookup"><span data-stu-id="49f34-340">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="49f34-341">2016 年 8 月 15 日</span><span class="sxs-lookup"><span data-stu-id="49f34-341">August 15, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-342">1.9.2</span><span class="sxs-lookup"><span data-stu-id="49f34-342">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="49f34-343">2016 年 7 月 23 日</span><span class="sxs-lookup"><span data-stu-id="49f34-343">July 23, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-344">1.8.0</span><span class="sxs-lookup"><span data-stu-id="49f34-344">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="49f34-345">2016 年 6 月 14 日</span><span class="sxs-lookup"><span data-stu-id="49f34-345">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-346">1.7.1</span><span class="sxs-lookup"><span data-stu-id="49f34-346">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="49f34-347">2016 年 5 月 6 日</span><span class="sxs-lookup"><span data-stu-id="49f34-347">May 06, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-348">1.7.0</span><span class="sxs-lookup"><span data-stu-id="49f34-348">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="49f34-349">2016 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="49f34-349">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-350">1.6.3</span><span class="sxs-lookup"><span data-stu-id="49f34-350">1.6.3</span></span>](#1.6.3) |<span data-ttu-id="49f34-351">2016 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="49f34-351">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-352">1.6.2</span><span class="sxs-lookup"><span data-stu-id="49f34-352">1.6.2</span></span>](#1.6.2) |<span data-ttu-id="49f34-353">2016 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="49f34-353">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-354">1.5.3</span><span class="sxs-lookup"><span data-stu-id="49f34-354">1.5.3</span></span>](#1.5.3) |<span data-ttu-id="49f34-355">2016 年 2 月 19 日</span><span class="sxs-lookup"><span data-stu-id="49f34-355">February 19, 2016</span></span> |--- |
| [<span data-ttu-id="49f34-356">1.5.2</span><span class="sxs-lookup"><span data-stu-id="49f34-356">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="49f34-357">2015 年 12 月 14 日</span><span class="sxs-lookup"><span data-stu-id="49f34-357">December 14, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-358">1.5.1</span><span class="sxs-lookup"><span data-stu-id="49f34-358">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="49f34-359">2015 年 11 月 23 日</span><span class="sxs-lookup"><span data-stu-id="49f34-359">November 23, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-360">1.5.0</span><span class="sxs-lookup"><span data-stu-id="49f34-360">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="49f34-361">2015 年 10 月 5 日</span><span class="sxs-lookup"><span data-stu-id="49f34-361">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-362">1.4.1</span><span class="sxs-lookup"><span data-stu-id="49f34-362">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="49f34-363">2015 年 8 月 25 日</span><span class="sxs-lookup"><span data-stu-id="49f34-363">August 25, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-364">1.4.0</span><span class="sxs-lookup"><span data-stu-id="49f34-364">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="49f34-365">2015 年 8 月 13 日</span><span class="sxs-lookup"><span data-stu-id="49f34-365">August 13, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-366">1.3.0</span><span class="sxs-lookup"><span data-stu-id="49f34-366">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="49f34-367">2015 年 8 月 5 日</span><span class="sxs-lookup"><span data-stu-id="49f34-367">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-368">1.2.0</span><span class="sxs-lookup"><span data-stu-id="49f34-368">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="49f34-369">2015 年 7 月 6 日</span><span class="sxs-lookup"><span data-stu-id="49f34-369">July 06, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-370">1.1.0</span><span class="sxs-lookup"><span data-stu-id="49f34-370">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="49f34-371">2015 年 4 月 30 日</span><span class="sxs-lookup"><span data-stu-id="49f34-371">April 30, 2015</span></span> |--- |
| [<span data-ttu-id="49f34-372">1.0.0</span><span class="sxs-lookup"><span data-stu-id="49f34-372">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="49f34-373">2015 年 4 月 8 日</span><span class="sxs-lookup"><span data-stu-id="49f34-373">April 08, 2015</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="49f34-374">常見問題集</span><span class="sxs-lookup"><span data-stu-id="49f34-374">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="49f34-375">另請參閱</span><span class="sxs-lookup"><span data-stu-id="49f34-375">See also</span></span>
<span data-ttu-id="49f34-376">請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。</span><span class="sxs-lookup"><span data-stu-id="49f34-376">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

