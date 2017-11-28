---
title: "aaaHow toodocument 資料來源 |Microsoft 文件"
description: "如何 tooarticle 反白顯示如何在 Azure 資料目錄中的 toodocument 資料資產。"
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="09e2a-103">記載資料來源</span><span class="sxs-lookup"><span data-stu-id="09e2a-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="09e2a-104">簡介</span><span class="sxs-lookup"><span data-stu-id="09e2a-104">Introduction</span></span>
<span data-ttu-id="09e2a-105">**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="09e2a-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="09e2a-106">換句話說， **Azure 資料目錄**就是要協助大眾探索，*了解*，及使用資料來源，以及幫助組織 tooget 其現有的資料從多個值。</span><span class="sxs-lookup"><span data-stu-id="09e2a-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="09e2a-107">資料來源已向當**Azure 資料目錄**，它的中繼資料會複製，並以 hello 服務編製索引但 hello 劇本那里未結束。</span><span class="sxs-lookup"><span data-stu-id="09e2a-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="09e2a-108">**Azure 資料目錄**也可讓使用者 tooprovide 自己 hello 使用量和 hello 資料來源的常見案例可以說明的完整文件。</span><span class="sxs-lookup"><span data-stu-id="09e2a-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="09e2a-109">在[如何 tooannotate 資料來源](data-catalog-how-to-annotate.md)，您了解，知道 hello 資料來源的專家可以加上註解它使用標籤和描述。</span><span class="sxs-lookup"><span data-stu-id="09e2a-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="09e2a-110">hello **Azure 資料目錄**入口網站包含豐富的文字編輯器，讓使用者可以完整文件資料資產和容器。</span><span class="sxs-lookup"><span data-stu-id="09e2a-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="09e2a-111">hello 編輯器包含段落格式，例如標題、 文字格式設定、 項目符號清單中，編號的清單，以及資料表。</span><span class="sxs-lookup"><span data-stu-id="09e2a-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="09e2a-112">標記和描述非常適合用於簡單的註解。</span><span class="sxs-lookup"><span data-stu-id="09e2a-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="09e2a-113">不過，toohelp 資料取用者深入了解 hello 使用資料來源，而且資料來源，熟悉的商務案例可以提供完整的詳細文件。</span><span class="sxs-lookup"><span data-stu-id="09e2a-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="09e2a-114">它是簡單 toodocument 資料來源。</span><span class="sxs-lookup"><span data-stu-id="09e2a-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="09e2a-115">請選取資料資產或容器，然後選擇 [說明文件] 。</span><span class="sxs-lookup"><span data-stu-id="09e2a-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="09e2a-116">記載資料資產</span><span class="sxs-lookup"><span data-stu-id="09e2a-116">Documenting data assets</span></span>
<span data-ttu-id="09e2a-117">hello 優點**Azure 資料目錄**文件集可讓您 toouse 目錄做為內容儲存機制 toocreate 完成旁白資料資產的資料。</span><span class="sxs-lookup"><span data-stu-id="09e2a-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="09e2a-118">您可以探索說明容器和資料表的詳細內容。</span><span class="sxs-lookup"><span data-stu-id="09e2a-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="09e2a-119">如果您已經有內容中另一個內容的儲存機制，例如 SharePoint 或檔案共用，您可以加入 toohello 資產文件連結 tooreference 這個現有的內容。</span><span class="sxs-lookup"><span data-stu-id="09e2a-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="09e2a-120">此功能可讓您更容易找到現有的說明文件。</span><span class="sxs-lookup"><span data-stu-id="09e2a-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="09e2a-121">說明文件不會包含在搜尋索引中。</span><span class="sxs-lookup"><span data-stu-id="09e2a-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="09e2a-122">hello 的文件層級的範圍可從描述 hello 特性和值的資料資產容器 tooa 詳細的容器內的資料表結構描述的描述。</span><span class="sxs-lookup"><span data-stu-id="09e2a-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="09e2a-123">應該重點 hello 提供文件層級的業務需求。</span><span class="sxs-lookup"><span data-stu-id="09e2a-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="09e2a-124">但一般來說，記載資料資產的優缺點如下︰</span><span class="sxs-lookup"><span data-stu-id="09e2a-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="09e2a-125">文件只有容器： hello 的所有內容都位於同一個地方，但可能會缺少必要的詳細資料的使用者 toomake 做出明智的決策。</span><span class="sxs-lookup"><span data-stu-id="09e2a-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="09e2a-126">文件只 hello 資料表： 內容特定 toothat 物件，但是您的使用者有多個位置的文件。</span><span class="sxs-lookup"><span data-stu-id="09e2a-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="09e2a-127">文件容器和資料表： 最完整的方法，但可能會造成更多的維護的 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="09e2a-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="09e2a-128">摘要</span><span class="sxs-lookup"><span data-stu-id="09e2a-128">Summary</span></span>
<span data-ttu-id="09e2a-129">在 **Azure 資料目錄** 中記載資料來源可依所需詳細程度建立資料資產的相關敘述。</span><span class="sxs-lookup"><span data-stu-id="09e2a-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="09e2a-130">藉由使用連結，您可以連結 toocontent 儲存在現有內容儲存機制，它結合了您的現有文件和資料資產中。</span><span class="sxs-lookup"><span data-stu-id="09e2a-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="09e2a-131">一旦使用者找到合適的資料資產，就能取得一組完整的說明文件。</span><span class="sxs-lookup"><span data-stu-id="09e2a-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
