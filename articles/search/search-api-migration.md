---
title: "aaaUpgrading toohello Azure 搜尋服務 REST API 2016-09-01 版 |Microsoft 文件"
description: "升級 toohello Azure 搜尋服務 REST API 2016-09-01 版"
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
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="010dd-103">升級 toohello Azure 搜尋服務 REST API 2016-09-01 版</span><span class="sxs-lookup"><span data-stu-id="010dd-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="010dd-104">如果您使用版本 2015年-02-28 或 2015年-02-28-預覽的 hello [Azure 搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx)，本文將協助您升級您的應用程式 toouse hello 下一步正式推出的 API 版本，2016年-09-01。</span><span class="sxs-lookup"><span data-stu-id="010dd-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="010dd-105">版本 2016年-09-01 的 hello REST API 包含從舊版的某些變更。</span><span class="sxs-lookup"><span data-stu-id="010dd-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="010dd-106">這些是大部分具有回溯相容性，因此變更程式碼應該只需要最少的工作 (視您之前使用的版本而定)。</span><span class="sxs-lookup"><span data-stu-id="010dd-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="010dd-107">請參閱[步驟 tooupgrade](#UpgradeSteps)如需有關指示 toochange 您程式碼 toouse hello 新的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="010dd-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="010dd-108">您的 Azure 搜尋服務執行個體支援多個 REST API 版本，包括 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="010dd-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="010dd-109">您可以繼續 toouse 版本時，它不會再 hello 最新的其中一個，但我們建議您移轉您的程式碼 toouse hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="010dd-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="010dd-110">版本 2016-09-01 的新功能</span><span class="sxs-lookup"><span data-stu-id="010dd-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="010dd-111">版本 2016年-09-01 是 hello 的 hello 第二個版本 Azure 搜尋服務 REST API。</span><span class="sxs-lookup"><span data-stu-id="010dd-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="010dd-112">這個 API 版本的新功能包括︰</span><span class="sxs-lookup"><span data-stu-id="010dd-112">New features in this API version include:</span></span>

* <span data-ttu-id="010dd-113">[自訂分析器](https://aka.ms/customanalyzers)，可讓您 tootake hello 程序，將文字轉換為可編索引且可搜尋的語彙基元的控制。</span><span class="sxs-lookup"><span data-stu-id="010dd-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="010dd-114">[Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)和[Azure 資料表儲存體](search-howto-indexing-azure-tables.md)索引子，可讓您 tooeasily 資料匯入 Azure 儲存體從 Azure 搜尋根據排程或隨。</span><span class="sxs-lookup"><span data-stu-id="010dd-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="010dd-115">[欄位對應](search-indexer-field-mappings.md)，可讓您 toocustomize 如何索引子將資料匯入 Azure 搜尋。</span><span class="sxs-lookup"><span data-stu-id="010dd-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="010dd-116">Etag，可讓您的索引、 索引子和資料來源的 tooupdate hello 定義並行安全的方式。</span><span class="sxs-lookup"><span data-stu-id="010dd-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="010dd-117">步驟 tooupgrade</span><span class="sxs-lookup"><span data-stu-id="010dd-117">Steps tooupgrade</span></span>
<span data-ttu-id="010dd-118">如果您要升級版本 2015年-02-28，可能不會有 toomake 任何變更 tooyour 以外的程式碼，toochange hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="010dd-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="010dd-119">hello 唯一情況下，您可能需要 toochange 程式碼時，就：</span><span class="sxs-lookup"><span data-stu-id="010dd-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="010dd-120">您的程式碼在 API 回應中傳回無法辨認的屬性時失敗。</span><span class="sxs-lookup"><span data-stu-id="010dd-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="010dd-121">您的應用程式預設應該會略過不了解的屬性。</span><span class="sxs-lookup"><span data-stu-id="010dd-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="010dd-122">您的程式碼仍然存在 API 要求，而且會嘗試 tooresend 它們 toohello 新 API 版本。</span><span class="sxs-lookup"><span data-stu-id="010dd-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="010dd-123">比方說，這可能是因為您的應用程式保存 hello 搜尋 API 所傳回的接續 token (如需詳細資訊，請尋找`@search.nextPageParameters`在 hello[搜尋 API 參考](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1))。</span><span class="sxs-lookup"><span data-stu-id="010dd-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="010dd-124">若下列情況下套用 tooyou，則您可能需要 toochange 您的程式碼據此。</span><span class="sxs-lookup"><span data-stu-id="010dd-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="010dd-125">否則，除非您想使用 hello toostart 任何變更應該是必要[新功能](#WhatsNew)的 2016年-09-01 版。</span><span class="sxs-lookup"><span data-stu-id="010dd-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="010dd-126">如果您要升級的版本 2015年-02-28-預覽，也適用於上述 hello，但您也必須注意，某些預覽功能不是在 2016年-09-01 版可用：</span><span class="sxs-lookup"><span data-stu-id="010dd-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="010dd-127">Azure Blob 儲存體索引子支援包含 JSON 陣列中的 CSV 檔案和 Blob。</span><span class="sxs-lookup"><span data-stu-id="010dd-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="010dd-128">同義字</span><span class="sxs-lookup"><span data-stu-id="010dd-128">Synonyms</span></span>
* <span data-ttu-id="010dd-129">"More like this" 查詢</span><span class="sxs-lookup"><span data-stu-id="010dd-129">"More like this" queries</span></span>

<span data-ttu-id="010dd-130">如果您的程式碼會使用這些功能，就能 tooupgrade too2016-09-01，不會移除它們的使用方式。</span><span class="sxs-lookup"><span data-stu-id="010dd-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="010dd-131">請記住，預覽 API 是針對測試與評估，不應該用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="010dd-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="010dd-132">結論</span><span class="sxs-lookup"><span data-stu-id="010dd-132">Conclusion</span></span>
<span data-ttu-id="010dd-133">如果您需要更多詳細資料上使用 hello Azure 搜尋服務 REST API，請參閱 hello 最近更新[API 參考](https://msdn.microsoft.com/library/azure/dn798935.aspx)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="010dd-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="010dd-134">歡迎您提供 Azure 搜尋服務的意見反應。</span><span class="sxs-lookup"><span data-stu-id="010dd-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="010dd-135">如果您遇到問題，則可以免費 tooask 我們 hello 的說明[Azure 搜尋 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)或[StackOverflow](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="010dd-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="010dd-136">如果您正在詢問問題有關 Azure 搜尋 StackOverflow，請確定 tootag 它與`azure-search`。</span><span class="sxs-lookup"><span data-stu-id="010dd-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="010dd-137">感謝您使用 Azure 搜尋服務！</span><span class="sxs-lookup"><span data-stu-id="010dd-137">Thank you for using Azure Search!</span></span>

