---
title: "aaaAzure Cosmos DB.NET Core API SDK 與資源 |Microsoft 文件"
description: ".NET Core API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB.NET Core SDK 的每個版本之間所做的變更，深入了解 hello。"
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="77b73-103">Azure Cosmos DB .NET Core SDK︰版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="77b73-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77b73-104">.NET</span><span class="sxs-lookup"><span data-stu-id="77b73-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="77b73-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="77b73-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="77b73-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="77b73-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="77b73-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="77b73-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="77b73-108">Java</span><span class="sxs-lookup"><span data-stu-id="77b73-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="77b73-109">Python</span><span class="sxs-lookup"><span data-stu-id="77b73-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="77b73-110">REST</span><span class="sxs-lookup"><span data-stu-id="77b73-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="77b73-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="77b73-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="77b73-112">SQL</span><span class="sxs-lookup"><span data-stu-id="77b73-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="77b73-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="77b73-113">**SDK download**</span></span></td><td>[<span data-ttu-id="77b73-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="77b73-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="77b73-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="77b73-115">**API documentation**</span></span></td><td>[<span data-ttu-id="77b73-116">.NET API 參考文件</span><span class="sxs-lookup"><span data-stu-id="77b73-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="77b73-117">**範例**</span><span class="sxs-lookup"><span data-stu-id="77b73-117">**Samples**</span></span></td><td>[<span data-ttu-id="77b73-118">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="77b73-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="77b73-119">**快速入門**</span><span class="sxs-lookup"><span data-stu-id="77b73-119">**Get started**</span></span></td><td>[<span data-ttu-id="77b73-120">開始使用 hello Azure Cosmos DB.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="77b73-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="77b73-121">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="77b73-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="77b73-122">使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="77b73-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="77b73-123">**目前支援的架構**</span><span class="sxs-lookup"><span data-stu-id="77b73-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="77b73-124">.NET Standard 1.6 和 .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="77b73-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="77b73-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="77b73-125">Release Notes</span></span>

<span data-ttu-id="77b73-126">hello Azure Cosmos DB.NET Core SDK 已與 hello hello 最新版本的功能同位檢查[Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="77b73-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="77b73-127">hello Azure Cosmos DB.NET Core SDK 不尚未與通用 Windows 平台 (UWP) 應用程式相容。</span><span class="sxs-lookup"><span data-stu-id="77b73-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="77b73-128">如果您有興趣 hello.NET Core SDK 支援 UWP 應用程式，請傳送電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="77b73-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="77b73-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="77b73-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="77b73-130">PartitionKeyRangeId FeedOption 的查詢結果 tooa 特定的資料分割索引鍵的範圍值的範圍設定為已加入的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="77b73-131">StartTime 為 ChangeFeedOption toostart hello 變更尋找該時間之後所新增的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="77b73-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="77b73-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="77b73-133">Hello JsonSerializable 類別可能會造成堆疊溢位例外狀況中修正的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="77b73-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="77b73-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="77b73-135">已新增對 [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 執行個體具現化時指定自訂 JsonSerializerSettings 的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="77b73-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="77b73-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="77b73-137">支援的.NET 標準 1.5 做為其中一個 hello 目標架構。</span><span class="sxs-lookup"><span data-stu-id="77b73-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="77b73-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="77b73-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="77b73-139">已修正當執行 Azure Cosmos DB 查詢時，受影響的 x64 機器不支援 SSE4 指令並且擲回 SEHException 的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="77b73-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="77b73-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="77b73-141">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="77b73-142">已新增對個別資料分割之查詢計量的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="77b73-143">限制查詢的 hello 接續 token 的 hello 大小新增的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="77b73-144">已新增對失敗要求進行更詳細追蹤的支援。</span><span class="sxs-lookup"><span data-stu-id="77b73-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="77b73-145">Hello SDK 中進行一些效能改進。</span><span class="sxs-lookup"><span data-stu-id="77b73-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="77b73-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="77b73-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="77b73-147">修正忽略 hello PartitionKey 值的彙總查詢 FeedOptions 中提供的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="77b73-148">修正在執行移動途中跨資料分割 Order By 查詢期間，進行資料分割管理的透明處理時發生的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="77b73-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="77b73-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="77b73-150">修正造成死結的某些資料 hello 非同步 Api ASP.NET 內容中使用時的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="77b73-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="77b73-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="77b73-152">修正 toomake SDK 更多彈性 tooautomatic 容錯移轉，在某些情況下的。</span><span class="sxs-lookup"><span data-stu-id="77b73-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="77b73-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="77b73-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="77b73-154">偶爾會造成 WebException 可解決問題的修正： 無法解析 hello 遠端名稱。</span><span class="sxs-lookup"><span data-stu-id="77b73-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="77b73-155">加入的 hello 支援直接讀取藉由新增新的多載 tooReadDocumentAsync API 的具類型的文件。</span><span class="sxs-lookup"><span data-stu-id="77b73-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="77b73-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="77b73-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="77b73-157">新增彙總查詢的 LINQ 支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="77b73-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="77b73-158">為記憶體流失問題的事件處理常式的 hello 使用所造成的 hello ConnectionPolicy 物件解決問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="77b73-159">修正使用 ETag 時 UpsertAttachmentAsync 無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="77b73-160">修正根據字串欄位排序時交叉資料分割排序依據查詢接續無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="77b73-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="77b73-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="77b73-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="77b73-162">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="77b73-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="77b73-163">請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。</span><span class="sxs-lookup"><span data-stu-id="77b73-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="77b73-164">降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。</span><span class="sxs-lookup"><span data-stu-id="77b73-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="77b73-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="77b73-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="77b73-166">hello Azure Cosmos DB.NET Core SDK 可讓您 toobuild 快，跨平台[ASP.NET Core](https://www.asp.net/core)和[.NET Core](https://www.microsoft.com/net/core#windows) Windows、 Mac 和 Linux 上的應用程式 toorun。</span><span class="sxs-lookup"><span data-stu-id="77b73-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="77b73-167">hello 最新版本的 hello Azure Cosmos DB.NET Core SDK 是完全[Xamarin](https://www.xamarin.com)相容，而且是使用的 toobuild 目標應用程式的 iOS、 Android 和單聲道 (Linux)。</span><span class="sxs-lookup"><span data-stu-id="77b73-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="77b73-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="77b73-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="77b73-169">hello Azure Cosmos DB.NET Core 預覽 SDK 可讓您 toobuild 快，跨平台[ASP.NET Core](https://www.asp.net/core)和[.NET Core](https://www.microsoft.com/net/core#windows) Windows、 Mac 和 Linux 上的應用程式 toorun。</span><span class="sxs-lookup"><span data-stu-id="77b73-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="77b73-170">hello Azure Cosmos DB.NET Core 預覽 SDK 已與 hello hello 最新版本的功能同位檢查[Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md)並支援下列 hello:</span><span class="sxs-lookup"><span data-stu-id="77b73-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="77b73-171">所有[連接模式](performance-tips.md#networking)︰閘道器模式、直接 TCP 和 Direct HTTPs。</span><span class="sxs-lookup"><span data-stu-id="77b73-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="77b73-172">所有[一致性層級](consistency-levels.md)︰強式、工作階段、限定過期和最終。</span><span class="sxs-lookup"><span data-stu-id="77b73-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="77b73-173">[資料分割的集合](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="77b73-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="77b73-174">[多重區域資料庫帳戶和異地複寫](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="77b73-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="77b73-175">如果您有問題相關的 toothis SDK，張貼太[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb)，hello 中提出問題或[github 儲存機制](https://github.com/Azure/azure-documentdb-dotnet/issues)。</span><span class="sxs-lookup"><span data-stu-id="77b73-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="77b73-176">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="77b73-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="77b73-177">版本</span><span class="sxs-lookup"><span data-stu-id="77b73-177">Version</span></span> | <span data-ttu-id="77b73-178">發行日期</span><span class="sxs-lookup"><span data-stu-id="77b73-178">Release Date</span></span> | <span data-ttu-id="77b73-179">停用日期</span><span class="sxs-lookup"><span data-stu-id="77b73-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="77b73-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="77b73-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="77b73-181">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="77b73-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="77b73-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="77b73-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="77b73-183">2017 年 8 月 7 日</span><span class="sxs-lookup"><span data-stu-id="77b73-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="77b73-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="77b73-185">2017 年 8 月 2 日</span><span class="sxs-lookup"><span data-stu-id="77b73-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="77b73-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="77b73-187">2017 年 6 月 12 日</span><span class="sxs-lookup"><span data-stu-id="77b73-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="77b73-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="77b73-189">2017 年 5 月 23 日</span><span class="sxs-lookup"><span data-stu-id="77b73-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="77b73-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="77b73-191">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="77b73-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="77b73-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="77b73-193">2017 年 4 月 19 日</span><span class="sxs-lookup"><span data-stu-id="77b73-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="77b73-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="77b73-195">2017 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="77b73-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="77b73-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="77b73-197">2017 年 3 月 25 日</span><span class="sxs-lookup"><span data-stu-id="77b73-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="77b73-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="77b73-199">2017 年 3 月 20 日</span><span class="sxs-lookup"><span data-stu-id="77b73-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="77b73-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="77b73-201">2017 年 3 月 14 日</span><span class="sxs-lookup"><span data-stu-id="77b73-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="77b73-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="77b73-203">2017 年 2 月 16 日</span><span class="sxs-lookup"><span data-stu-id="77b73-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="77b73-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="77b73-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="77b73-205">2016 年 12 月 21 日</span><span class="sxs-lookup"><span data-stu-id="77b73-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="77b73-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="77b73-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="77b73-207">2016 年 11 月 15 日</span><span class="sxs-lookup"><span data-stu-id="77b73-207">November 15, 2016</span></span> |<span data-ttu-id="77b73-208">2016 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="77b73-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="77b73-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="77b73-209">See Also</span></span>
<span data-ttu-id="77b73-210">請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。</span><span class="sxs-lookup"><span data-stu-id="77b73-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

