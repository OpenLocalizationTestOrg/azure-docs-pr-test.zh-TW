---
title: "Azure Cosmos DB .NET Core API、SDK 和資源 | Microsoft Docs"
description: "全面了解 .NET Core API 和 SDK，包括發行日期、停用日期及 Azure Cosmos DB .NET Core SDK 每個版本之間的變更。"
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
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="23be6-103">Azure Cosmos DB .NET Core SDK︰版本資訊與資源</span><span class="sxs-lookup"><span data-stu-id="23be6-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23be6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="23be6-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="23be6-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="23be6-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="23be6-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="23be6-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="23be6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="23be6-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="23be6-108">Java</span><span class="sxs-lookup"><span data-stu-id="23be6-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="23be6-109">Python</span><span class="sxs-lookup"><span data-stu-id="23be6-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="23be6-110">REST</span><span class="sxs-lookup"><span data-stu-id="23be6-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="23be6-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="23be6-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="23be6-112">SQL</span><span class="sxs-lookup"><span data-stu-id="23be6-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="23be6-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="23be6-113">**SDK download**</span></span></td><td>[<span data-ttu-id="23be6-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="23be6-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="23be6-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="23be6-115">**API documentation**</span></span></td><td>[<span data-ttu-id="23be6-116">.NET API 參考文件</span><span class="sxs-lookup"><span data-stu-id="23be6-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="23be6-117">**範例**</span><span class="sxs-lookup"><span data-stu-id="23be6-117">**Samples**</span></span></td><td>[<span data-ttu-id="23be6-118">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="23be6-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="23be6-119">**開始使用**</span><span class="sxs-lookup"><span data-stu-id="23be6-119">**Get started**</span></span></td><td>[<span data-ttu-id="23be6-120">開始使用 Azure Cosmos DB .NET Core SDK 教學課程</span><span class="sxs-lookup"><span data-stu-id="23be6-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="23be6-121">**Web 應用程式教學課程**</span><span class="sxs-lookup"><span data-stu-id="23be6-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="23be6-122">使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="23be6-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="23be6-123">**目前支援的架構**</span><span class="sxs-lookup"><span data-stu-id="23be6-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="23be6-124">.NET Standard 1.6 和 .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="23be6-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="23be6-125">版本資訊</span><span class="sxs-lookup"><span data-stu-id="23be6-125">Release Notes</span></span>

<span data-ttu-id="23be6-126">Azure Cosmos DB .NET Core SDK 有與最新版 [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) 類似的功能。</span><span class="sxs-lookup"><span data-stu-id="23be6-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="23be6-127">Azure Cosmos DB .NET Core SDK 與「通用 Windows 平台」(UWP) 應用程式尚未相容。</span><span class="sxs-lookup"><span data-stu-id="23be6-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="23be6-128">如果您有興趣了解可支援 UWP 應用程式的 .NET Core SDK，請傳送電子郵件至 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="23be6-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="23be6-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="23be6-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="23be6-130">已新增將 PartitionKeyRangeId 做為 FeedOption 的支援，以供對特定分割區索引鍵範圍值限制查詢結果範圍。</span><span class="sxs-lookup"><span data-stu-id="23be6-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="23be6-131">已新增將 StartTime 做為 ChangeFeedOption 的支援，以開始尋找該時間之後的變更。</span><span class="sxs-lookup"><span data-stu-id="23be6-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="23be6-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="23be6-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="23be6-133">修正 JsonSerializable 類別中可能會造成堆疊溢位例外狀況的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="23be6-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="23be6-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="23be6-135">已新增對 [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 執行個體具現化時指定自訂 JsonSerializerSettings 的支援。</span><span class="sxs-lookup"><span data-stu-id="23be6-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="23be6-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="23be6-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="23be6-137">支援 .NET Standard 1.5 作為其中一個目標架構。</span><span class="sxs-lookup"><span data-stu-id="23be6-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="23be6-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="23be6-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="23be6-139">已修正當執行 Azure Cosmos DB 查詢時，受影響的 x64 機器不支援 SSE4 指令並且擲回 SEHException 的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="23be6-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="23be6-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="23be6-141">已新增對新一致性層級 ConsistentPrefix 的支援。</span><span class="sxs-lookup"><span data-stu-id="23be6-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="23be6-142">已新增對個別資料分割之查詢計量的支援。</span><span class="sxs-lookup"><span data-stu-id="23be6-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="23be6-143">已新增對限制查詢之接續權杖大小的支援。</span><span class="sxs-lookup"><span data-stu-id="23be6-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="23be6-144">已新增對失敗要求進行更詳細追蹤的支援。</span><span class="sxs-lookup"><span data-stu-id="23be6-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="23be6-145">SDK 中已有一些效能改進。</span><span class="sxs-lookup"><span data-stu-id="23be6-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="23be6-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="23be6-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="23be6-147">修正將在彙總查詢之 FeedOptions 中提供的 PartitionKey 值忽略的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="23be6-148">修正在執行移動途中跨資料分割 Order By 查詢期間，進行資料分割管理的透明處理時發生的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="23be6-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="23be6-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="23be6-150">已修正在 ASP.NET 內容內部使用時會在某些非同步 API 中造成死結的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="23be6-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="23be6-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="23be6-152">修正來讓 SDK 在某些情況下能夠更有彈性地進行自動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="23be6-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="23be6-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="23be6-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="23be6-154">修正偶爾會造成「WebException: 無法解析遠端名稱」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="23be6-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="23be6-155">透過針對 ReadDocumentAsync API 新增多載，以新增直接讀取具類型文件的支援。</span><span class="sxs-lookup"><span data-stu-id="23be6-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="23be6-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="23be6-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="23be6-157">新增彙總查詢的 LINQ 支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="23be6-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="23be6-158">針對使用事件處理常式所造成的 ConnectionPolicy 物件，修正記憶體流失問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="23be6-159">修正使用 ETag 時 UpsertAttachmentAsync 無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="23be6-160">修正根據字串欄位排序時交叉資料分割排序依據查詢接續無法運作的問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="23be6-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="23be6-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="23be6-162">新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。</span><span class="sxs-lookup"><span data-stu-id="23be6-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="23be6-163">請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。</span><span class="sxs-lookup"><span data-stu-id="23be6-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="23be6-164">已將分割區集合的最小輸送量從 10,100 RU/s 降低為 2500 RU/s。</span><span class="sxs-lookup"><span data-stu-id="23be6-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="23be6-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="23be6-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="23be6-166">Azure Cosmos DB .NET Core SDK 可讓您建置快速、跨平台的 [ASP.NET Core](https://www.asp.net/core) 和 [.NET Core](https://www.microsoft.com/net/core#windows) 應用程式，以在 Windows、Mac 和 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="23be6-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="23be6-167">最新版 Azure Cosmos DB .NET Core SDK 與 [Xamarin](https://www.xamarin.com) 完全相容，可用來建置以 iOS、Android 及 Mono (Linux) 為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="23be6-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="23be6-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="23be6-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="23be6-169">Azure Cosmos DB .NET Core Preview SDK 可讓您建置快速、跨平台的 [ASP.NET Core](https://www.asp.net/core) 和 [.NET Core](https://www.microsoft.com/net/core#windows) 應用程式，以在 Windows、Mac 和 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="23be6-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="23be6-170">Azure Cosmos DB .NET Core Preview SDK 有與最新版本 [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) 的功能類似的功能，並且支援下列項目︰</span><span class="sxs-lookup"><span data-stu-id="23be6-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="23be6-171">所有[連接模式](performance-tips.md#networking)︰閘道器模式、直接 TCP 和 Direct HTTPs。</span><span class="sxs-lookup"><span data-stu-id="23be6-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="23be6-172">所有[一致性層級](consistency-levels.md)︰強式、工作階段、限定過期和最終。</span><span class="sxs-lookup"><span data-stu-id="23be6-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="23be6-173">[資料分割的集合](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="23be6-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="23be6-174">[多重區域資料庫帳戶和異地複寫](distribute-data-globally.md)。</span><span class="sxs-lookup"><span data-stu-id="23be6-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="23be6-175">如果您有與此 SDK 相關的問題，請張貼至 [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb)，或是在 [Github 儲存機制](https://github.com/Azure/azure-documentdb-dotnet/issues)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="23be6-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="23be6-176">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="23be6-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="23be6-177">版本</span><span class="sxs-lookup"><span data-stu-id="23be6-177">Version</span></span> | <span data-ttu-id="23be6-178">發行日期</span><span class="sxs-lookup"><span data-stu-id="23be6-178">Release Date</span></span> | <span data-ttu-id="23be6-179">停用日期</span><span class="sxs-lookup"><span data-stu-id="23be6-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="23be6-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="23be6-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="23be6-181">2017 年 8 月 10 日</span><span class="sxs-lookup"><span data-stu-id="23be6-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="23be6-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="23be6-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="23be6-183">2017 年 8 月 7 日</span><span class="sxs-lookup"><span data-stu-id="23be6-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="23be6-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="23be6-185">2017 年 8 月 2 日</span><span class="sxs-lookup"><span data-stu-id="23be6-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="23be6-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="23be6-187">2017 年 6 月 12 日</span><span class="sxs-lookup"><span data-stu-id="23be6-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="23be6-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="23be6-189">2017 年 5 月 23 日</span><span class="sxs-lookup"><span data-stu-id="23be6-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="23be6-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="23be6-191">2017 年 5 月 10 日</span><span class="sxs-lookup"><span data-stu-id="23be6-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="23be6-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="23be6-193">2017 年 4 月 19 日</span><span class="sxs-lookup"><span data-stu-id="23be6-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="23be6-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="23be6-195">2017 年 3 月 29 日</span><span class="sxs-lookup"><span data-stu-id="23be6-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="23be6-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="23be6-197">2017 年 3 月 25 日</span><span class="sxs-lookup"><span data-stu-id="23be6-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="23be6-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="23be6-199">2017 年 3 月 20 日</span><span class="sxs-lookup"><span data-stu-id="23be6-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="23be6-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="23be6-201">2017 年 3 月 14 日</span><span class="sxs-lookup"><span data-stu-id="23be6-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="23be6-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="23be6-203">2017 年 2 月 16 日</span><span class="sxs-lookup"><span data-stu-id="23be6-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="23be6-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="23be6-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="23be6-205">2016 年 12 月 21 日</span><span class="sxs-lookup"><span data-stu-id="23be6-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="23be6-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="23be6-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="23be6-207">2016 年 11 月 15 日</span><span class="sxs-lookup"><span data-stu-id="23be6-207">November 15, 2016</span></span> |<span data-ttu-id="23be6-208">2016 年 12 月 31 日</span><span class="sxs-lookup"><span data-stu-id="23be6-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="23be6-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="23be6-209">See Also</span></span>
<span data-ttu-id="23be6-210">若要深入了解 Cosmos DB，請參閱 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="23be6-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

