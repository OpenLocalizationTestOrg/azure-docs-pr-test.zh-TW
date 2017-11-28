---
title: "升級至 Azure 搜尋服務 REST API 版本 2016-09-01 | Microsoft Docs"
description: "升級至 Azure 搜尋服務 REST API 版本 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="7fc83-103">升級至 Azure 搜尋服務 REST API 版本 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="7fc83-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="7fc83-104">如果您在使用版本 2015-02-28 or 2015-02-28-Preview 的 [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx)，本文章將協助您升級應用程式，以使用下一個正式推出的 API 版本 2016-09-01。</span><span class="sxs-lookup"><span data-stu-id="7fc83-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="7fc83-105">REST API 的版本 2016-09-01 包含一些較舊版本的變更。</span><span class="sxs-lookup"><span data-stu-id="7fc83-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="7fc83-106">這些是大部分具有回溯相容性，因此變更程式碼應該只需要最少的工作 (視您之前使用的版本而定)。</span><span class="sxs-lookup"><span data-stu-id="7fc83-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="7fc83-107">請參閱[升級步驟](#UpgradeSteps)以取得如何變更您的程式碼以使用新的 API 版本的指示。</span><span class="sxs-lookup"><span data-stu-id="7fc83-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="7fc83-108">您的「Azure 搜尋服務」執行個體支援數個 REST API 版本，包括最新版本。</span><span class="sxs-lookup"><span data-stu-id="7fc83-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="7fc83-109">當一個版本不再是最新版本時，您仍可繼續使用該版本，但建議您將程式碼移轉成使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="7fc83-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="7fc83-110">版本 2016-09-01 的新功能</span><span class="sxs-lookup"><span data-stu-id="7fc83-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="7fc83-111">版本 2016-09-01 是 Azure 搜尋服務 REST API 的第二個正式推出版本。</span><span class="sxs-lookup"><span data-stu-id="7fc83-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="7fc83-112">這個 API 版本的新功能包括︰</span><span class="sxs-lookup"><span data-stu-id="7fc83-112">New features in this API version include:</span></span>

* <span data-ttu-id="7fc83-113">[自訂分析器](https://aka.ms/customanalyzers)，可讓您充分控制將文字轉換成可檢索和可搜尋語彙基元的程序。</span><span class="sxs-lookup"><span data-stu-id="7fc83-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="7fc83-114">[Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)和 [Azure 表格儲存體](search-howto-indexing-azure-tables.md)索引子，可讓您根據排程或視需要將資料從 Azure 儲存體輕鬆地匯入至 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="7fc83-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="7fc83-115">[欄位對應](search-indexer-field-mappings.md)，可讓您自訂索引子如何將資料匯入至 Azure 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="7fc83-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="7fc83-116">Etag 可讓您透過安全並行方式來更新索引、索引子和資料來源的定義。</span><span class="sxs-lookup"><span data-stu-id="7fc83-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="7fc83-117">升級步驟</span><span class="sxs-lookup"><span data-stu-id="7fc83-117">Steps to upgrade</span></span>
<span data-ttu-id="7fc83-118">如果您從版本 2015-02-28 升級，則除了變更版本號碼之外，可能不需要對您的程式碼進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="7fc83-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="7fc83-119">您可能需要變更程式碼的唯一情況是︰</span><span class="sxs-lookup"><span data-stu-id="7fc83-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="7fc83-120">您的程式碼在 API 回應中傳回無法辨認的屬性時失敗。</span><span class="sxs-lookup"><span data-stu-id="7fc83-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="7fc83-121">您的應用程式預設應該會略過不了解的屬性。</span><span class="sxs-lookup"><span data-stu-id="7fc83-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="7fc83-122">您的程式碼仍然存在 API 要求，並嘗試將它們重新傳送給新的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="7fc83-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="7fc83-123">例如，發生原因可能是您的應用程式持續保存搜尋服務 API 所傳回的接續 Token (如需詳細資訊，請在[搜尋服務 API 參考](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)) 中查找 `@search.nextPageParameters`。</span><span class="sxs-lookup"><span data-stu-id="7fc83-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="7fc83-124">如果下列其中一種情況適用您的情況，您可能需要據此變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="7fc83-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="7fc83-125">否則，除非您想要開始使用版本 2016-09-01 的[新功能](#WhatsNew)，否則應該不需要進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="7fc83-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="7fc83-126">如果您要從版本 2015-02-28-Preview 升級，則也會套用上述作業，但也必須知道版本 2016-09-01 中未提供某些預覽功能︰</span><span class="sxs-lookup"><span data-stu-id="7fc83-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="7fc83-127">Azure Blob 儲存體索引子支援包含 JSON 陣列中的 CSV 檔案和 Blob。</span><span class="sxs-lookup"><span data-stu-id="7fc83-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="7fc83-128">同義字</span><span class="sxs-lookup"><span data-stu-id="7fc83-128">Synonyms</span></span>
* <span data-ttu-id="7fc83-129">"More like this" 查詢</span><span class="sxs-lookup"><span data-stu-id="7fc83-129">"More like this" queries</span></span>

<span data-ttu-id="7fc83-130">如果您的程式碼使用這些功能，則升級至 2016-09-01 時需要移除它們的使用。</span><span class="sxs-lookup"><span data-stu-id="7fc83-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fc83-131">請記住，預覽 API 是針對測試與評估，不應該用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="7fc83-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="7fc83-132">結論</span><span class="sxs-lookup"><span data-stu-id="7fc83-132">Conclusion</span></span>
<span data-ttu-id="7fc83-133">如果您需要使用 Azure 搜尋服務 REST API 的更多詳細資料，請參閱 MSDN 上最近更新的 [API 參考](https://msdn.microsoft.com/library/azure/dn798935.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7fc83-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="7fc83-134">歡迎您提供 Azure 搜尋服務的意見反應。</span><span class="sxs-lookup"><span data-stu-id="7fc83-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="7fc83-135">如果您遇到問題，歡迎在 [Azure 搜尋服務 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) 或 [StackOverflow](http://stackoverflow.com/)上尋求協助。</span><span class="sxs-lookup"><span data-stu-id="7fc83-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="7fc83-136">如果您要在 StackOverflow 上詢問 Azure 搜尋服務問題，請一定要將它標上 `azure-search`。</span><span class="sxs-lookup"><span data-stu-id="7fc83-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="7fc83-137">感謝您使用 Azure 搜尋服務！</span><span class="sxs-lookup"><span data-stu-id="7fc83-137">Thank you for using Azure Search!</span></span>

