---
title: "aaaAzure DocumentDB.NET 變更摘要處理器 SDK 與資源 |Microsoft 文件"
description: "變更摘要處理器 API 和 SDK 包括發行日期、 停用日期和 hello DocumentDB.NET 變更摘要處理器 SDK 的每個版本之間所做的變更，深入了解 hello。"
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
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="f9979-103">DocumentDB .NET 變更摘要處理器 SDK：下載和版本資訊</span><span class="sxs-lookup"><span data-stu-id="f9979-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9979-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f9979-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="f9979-105">.NET 變更摘要</span><span class="sxs-lookup"><span data-stu-id="f9979-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="f9979-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f9979-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="f9979-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f9979-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="f9979-108">Java</span><span class="sxs-lookup"><span data-stu-id="f9979-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="f9979-109">Python</span><span class="sxs-lookup"><span data-stu-id="f9979-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="f9979-110">REST</span><span class="sxs-lookup"><span data-stu-id="f9979-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="f9979-111">REST 資源提供者</span><span class="sxs-lookup"><span data-stu-id="f9979-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="f9979-112">SQL</span><span class="sxs-lookup"><span data-stu-id="f9979-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="f9979-113">**SDK 下載**</span><span class="sxs-lookup"><span data-stu-id="f9979-113">**SDK download**</span></span></td><td>[<span data-ttu-id="f9979-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="f9979-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="f9979-115">**API 文件**</span><span class="sxs-lookup"><span data-stu-id="f9979-115">**API documentation**</span></span></td><td>[<span data-ttu-id="f9979-116">變更摘要處理器程式庫 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="f9979-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="f9979-117">**快速入門**</span><span class="sxs-lookup"><span data-stu-id="f9979-117">**Get started**</span></span></td><td>[<span data-ttu-id="f9979-118">開始使用 DocumentDB 變更摘要處理器.NET SDK hello</span><span class="sxs-lookup"><span data-stu-id="f9979-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="f9979-119">**目前支援的架構**</span><span class="sxs-lookup"><span data-stu-id="f9979-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="f9979-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="f9979-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="f9979-121">版本資訊</span><span class="sxs-lookup"><span data-stu-id="f9979-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="f9979-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="f9979-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="f9979-123">加入方法 tooobtain 估計剩餘工作 toobe 處理 hello 變更摘要。</span><span class="sxs-lookup"><span data-stu-id="f9979-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="f9979-124">與 [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.13.2 或以上版本相容。</span><span class="sxs-lookup"><span data-stu-id="f9979-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="f9979-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="f9979-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="f9979-126">GA SDK</span><span class="sxs-lookup"><span data-stu-id="f9979-126">GA SDK</span></span>
* <span data-ttu-id="f9979-127">與 [DocumentDB.NET SDK](documentdb-sdk-dotnet.md) 1.14.1 或以下版本相容。</span><span class="sxs-lookup"><span data-stu-id="f9979-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="f9979-128">發行和停用日期</span><span class="sxs-lookup"><span data-stu-id="f9979-128">Release & Retirement dates</span></span>
<span data-ttu-id="f9979-129">Microsoft 提供通知的最少**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。</span><span class="sxs-lookup"><span data-stu-id="f9979-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="f9979-130">新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議您，您一律升級 toohello 最新版本 SDK 盡早。</span><span class="sxs-lookup"><span data-stu-id="f9979-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="f9979-131">Hello 服務，將會拒絕任何要求 tooCosmos 使用已停用的 SDK 的 DB。</span><span class="sxs-lookup"><span data-stu-id="f9979-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="f9979-132">版本</span><span class="sxs-lookup"><span data-stu-id="f9979-132">Version</span></span> | <span data-ttu-id="f9979-133">發行日期</span><span class="sxs-lookup"><span data-stu-id="f9979-133">Release Date</span></span> | <span data-ttu-id="f9979-134">停用日期</span><span class="sxs-lookup"><span data-stu-id="f9979-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="f9979-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="f9979-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="f9979-136">2017 年 8 月 13 日</span><span class="sxs-lookup"><span data-stu-id="f9979-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="f9979-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f9979-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="f9979-138">2017 年 7 月 7 日</span><span class="sxs-lookup"><span data-stu-id="f9979-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="f9979-139">常見問題集</span><span class="sxs-lookup"><span data-stu-id="f9979-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="f9979-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f9979-140">See also</span></span>
<span data-ttu-id="f9979-141">請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。</span><span class="sxs-lookup"><span data-stu-id="f9979-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

