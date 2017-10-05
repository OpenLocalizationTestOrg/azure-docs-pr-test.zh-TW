---
title: "Azure DocumentDB .NET 變更摘要處理器 SDK 和資源 | Microsoft Docs"
description: "了解「變更摘要處理器 API 和 SDK」的所有相關資訊，包括發行日期、停用日期，以及「DocumentDB .NET 變更摘要處理器 SDK」每個版本之間的變更。"
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 40c796bc5af1220c46950a6fac062ffdd243e59f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="b03f6-103">DocumentDB .NET 變更摘要處理器 SDK：下載和版本資訊</span><span class="sxs-lookup"><span data-stu-id="b03f6-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b03f6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b03f6-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="b03f6-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="b03f6-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="b03f6-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b03f6-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="b03f6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="b03f6-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="b03f6-108">Java</span><span class="sxs-lookup"><span data-stu-id="b03f6-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="b03f6-109">Python</span><span class="sxs-lookup"><span data-stu-id="b03f6-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="b03f6-110">REST</span><span class="sxs-lookup"><span data-stu-id="b03f6-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="b03f6-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="b03f6-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="b03f6-112">SQL</span><span class="sxs-lookup"><span data-stu-id="b03f6-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="b03f6-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="b03f6-113">**SDK download**</span></span></td><td>[<span data-ttu-id="b03f6-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="b03f6-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="b03f6-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="b03f6-115">**API documentation**</span></span></td><td>[<span data-ttu-id="b03f6-116">變更摘要處理器程式庫 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="b03f6-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="b03f6-117">**開始使用**</span><span class="sxs-lookup"><span data-stu-id="b03f6-117">**Get started**</span></span></td><td>[<span data-ttu-id="b03f6-118">開始使用 DocumentDB 變更摘要處理器 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b03f6-118">Get started with the DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="b03f6-119">**目前支援的架構**</span><span class="sxs-lookup"><span data-stu-id="b03f6-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="b03f6-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="b03f6-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="b03f6-121">版本資訊</span><span class="sxs-lookup"><span data-stu-id="b03f6-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="b03f6-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="b03f6-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="b03f6-123">新增方法以取得要在變更摘要中處理之剩餘工作的估算。</span><span class="sxs-lookup"><span data-stu-id="b03f6-123">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span></span>
* <span data-ttu-id="b03f6-124">與 [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.13.2 或以上版本相容。</span><span class="sxs-lookup"><span data-stu-id="b03f6-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="b03f6-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="b03f6-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="b03f6-126">GA SDK</span><span class="sxs-lookup"><span data-stu-id="b03f6-126">GA SDK</span></span>
* <span data-ttu-id="b03f6-127">與 [DocumentDB.NET SDK](documentdb-sdk-dotnet.md) 1.14.1 或以下版本相容。</span><span class="sxs-lookup"><span data-stu-id="b03f6-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="b03f6-128">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="b03f6-128">Release & Retirement dates</span></span>
<span data-ttu-id="b03f6-129">Microsoft 至少會在停用 SDK 的 **12 個月** 之前提供通知，以供順利轉換至較新/支援的版本。</span><span class="sxs-lookup"><span data-stu-id="b03f6-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="b03f6-130">新的功能與最佳化項目只會新增至目前的 SDK，因此建議您一律盡早升級至最新的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="b03f6-130">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="b03f6-131">服務將會拒絕使用已停用 SDK 的任何 Cosmos DB 要求。</span><span class="sxs-lookup"><span data-stu-id="b03f6-131">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="b03f6-132">版本</span><span class="sxs-lookup"><span data-stu-id="b03f6-132">Version</span></span> | <span data-ttu-id="b03f6-133">發行日期</span><span class="sxs-lookup"><span data-stu-id="b03f6-133">Release Date</span></span> | <span data-ttu-id="b03f6-134">停用日期</span><span class="sxs-lookup"><span data-stu-id="b03f6-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b03f6-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b03f6-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="b03f6-136">2017 年 8 月 13 日</span><span class="sxs-lookup"><span data-stu-id="b03f6-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="b03f6-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b03f6-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="b03f6-138">2017 年 7 月 7 日</span><span class="sxs-lookup"><span data-stu-id="b03f6-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="b03f6-139">常見問題集</span><span class="sxs-lookup"><span data-stu-id="b03f6-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="b03f6-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b03f6-140">See also</span></span>
<span data-ttu-id="b03f6-141">若要深入了解 Cosmos DB，請參閱 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="b03f6-141">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

