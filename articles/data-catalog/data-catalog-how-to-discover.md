---
title: "如何探索 Azure 資料目錄中的資料資產 | Microsoft Docs"
description: "本文著重在說明如何探索已註冊 Azure 資料目錄的資料資產，包括搜尋、篩選 Azure 資料目錄入口網站，以及使用其結果醒目提示功能。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 9ff67dcb5ecb00440f73f979fd8d2b79a570c674
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-discover-data-sources-in-azure-data-catalog"></a><span data-ttu-id="267c3-103">如何探索 Azure 資料目錄中的資料資產</span><span class="sxs-lookup"><span data-stu-id="267c3-103">How to discover data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="267c3-104">簡介</span><span class="sxs-lookup"><span data-stu-id="267c3-104">Introduction</span></span>
<span data-ttu-id="267c3-105">Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料來源的註冊和探索系統。</span><span class="sxs-lookup"><span data-stu-id="267c3-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="267c3-106">換句話說，資料目錄可於協助人們探索、了解和使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="267c3-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="267c3-107">在資料目錄註冊資料來源之後，其中繼資料會由此服務編製索引，讓您可以輕鬆地搜尋以探索所需的資料。</span><span class="sxs-lookup"><span data-stu-id="267c3-107">After a data source is registered with Data Catalog, its metadata is indexed by the service, so that you can easily search to discover the data you need.</span></span>

## <a name="searching-and-filtering"></a><span data-ttu-id="267c3-108">搜尋和篩選</span><span class="sxs-lookup"><span data-stu-id="267c3-108">Searching and filtering</span></span>
<span data-ttu-id="267c3-109">在資料目錄進行探索會使用兩種主要機制：搜尋和篩選。</span><span class="sxs-lookup"><span data-stu-id="267c3-109">Discovery in Data Catalog uses two primary mechanisms: searching and filtering.</span></span>

<span data-ttu-id="267c3-110">搜尋的設計兼具直覺與強大的功能。</span><span class="sxs-lookup"><span data-stu-id="267c3-110">Searching is designed to be both intuitive and powerful.</span></span> <span data-ttu-id="267c3-111">根據預設，搜尋字詞會比對目錄中的所有內容，包括使用者提供的註解。</span><span class="sxs-lookup"><span data-stu-id="267c3-111">By default, search terms are matched against any property in the catalog, including user-provided annotations.</span></span>

<span data-ttu-id="267c3-112">篩選的設計則與搜尋互補。</span><span class="sxs-lookup"><span data-stu-id="267c3-112">Filtering is designed to complement searching.</span></span> <span data-ttu-id="267c3-113">您可以選取特定的特性，例如專家、資料來源類型、物件類型和標記。</span><span class="sxs-lookup"><span data-stu-id="267c3-113">You can select specific characteristics such as experts, data source type, object type, and tags.</span></span> <span data-ttu-id="267c3-114">您可以只檢視相符的資料資產，並將搜尋結果限制為相符的資產。</span><span class="sxs-lookup"><span data-stu-id="267c3-114">You can view only matching data assets, and constrain search results to matching assets.</span></span>

<span data-ttu-id="267c3-115">透過結合使用搜尋和篩選，您可以快速巡覽已經在資料目錄註冊的資料來源，以探索所需的資料來源。</span><span class="sxs-lookup"><span data-stu-id="267c3-115">By using a combination of searching and filtering, you can quickly navigate the data sources that have been registered with Data Catalog to discover the data sources you need.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="267c3-116">搜尋語法</span><span class="sxs-lookup"><span data-stu-id="267c3-116">Search syntax</span></span>
<span data-ttu-id="267c3-117">雖然預設的任意文字搜尋既簡單又直覺，但您也可以使用資料目錄搜尋語法，更充分地掌控搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="267c3-117">Although the default free text search is simple and intuitive, you can also use Data Catalog search syntax for greater control over the search results.</span></span> <span data-ttu-id="267c3-118">資料目錄搜尋支援下列技巧：</span><span class="sxs-lookup"><span data-stu-id="267c3-118">Data Catalog search supports the following techniques:</span></span>

| <span data-ttu-id="267c3-119">技巧</span><span class="sxs-lookup"><span data-stu-id="267c3-119">Technique</span></span> | <span data-ttu-id="267c3-120">使用</span><span class="sxs-lookup"><span data-stu-id="267c3-120">Use</span></span> | <span data-ttu-id="267c3-121">範例</span><span class="sxs-lookup"><span data-stu-id="267c3-121">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="267c3-122">基本搜尋</span><span class="sxs-lookup"><span data-stu-id="267c3-122">Basic search</span></span> |<span data-ttu-id="267c3-123">使用一或多個搜尋字詞的基本搜尋。</span><span class="sxs-lookup"><span data-stu-id="267c3-123">Basic search that uses one or more search terms.</span></span> <span data-ttu-id="267c3-124">結果包含了任何屬性與一或多個指定字詞相符的所有資產。</span><span class="sxs-lookup"><span data-stu-id="267c3-124">Results are any assets that match any property with one or more of the terms specified.</span></span> |`sales data` |
| <span data-ttu-id="267c3-125">屬性範圍</span><span class="sxs-lookup"><span data-stu-id="267c3-125">Property scoping</span></span> |<span data-ttu-id="267c3-126">只會傳回搜尋字詞與指定屬性相符的資料來源。</span><span class="sxs-lookup"><span data-stu-id="267c3-126">Return only data sources where the search term is matched with the specified property.</span></span> |`name:finance` |
| <span data-ttu-id="267c3-127">布林運算子</span><span class="sxs-lookup"><span data-stu-id="267c3-127">Boolean operators</span></span> |<span data-ttu-id="267c3-128">使用布林值作業擴大或縮小搜尋。</span><span class="sxs-lookup"><span data-stu-id="267c3-128">Broaden or narrow a search by using Boolean operations.</span></span> |`finance NOT corporate` |
| <span data-ttu-id="267c3-129">使用括弧分組</span><span class="sxs-lookup"><span data-stu-id="267c3-129">Grouping with parenthesis</span></span> |<span data-ttu-id="267c3-130">使用括弧將查詢部分分組，以達到邏輯隔離，尤其是與布林運算子結合時。</span><span class="sxs-lookup"><span data-stu-id="267c3-130">Use parentheses to group parts of the query to achieve logical isolation, especially in conjunction with Boolean operators.</span></span> |`name:finance AND (tags:Q1 OR tags:Q2)` |
| <span data-ttu-id="267c3-131">比較運算子</span><span class="sxs-lookup"><span data-stu-id="267c3-131">Comparison operators</span></span> |<span data-ttu-id="267c3-132">針對具有數值和日期資料類型的屬性使用比較而非相等。</span><span class="sxs-lookup"><span data-stu-id="267c3-132">Use comparisons other than equality for properties that have numeric and date data types.</span></span> |`modifiedTime > "11/05/2014"` |

<span data-ttu-id="267c3-133">如需資料目錄搜尋的詳細資訊，請參閱 [Azure 資料目錄](https://msdn.microsoft.com/library/azure/mt267594.aspx)一文。</span><span class="sxs-lookup"><span data-stu-id="267c3-133">For more information about Data Catalog search, see the [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) article.</span></span>

## <a name="hit-highlighting"></a><span data-ttu-id="267c3-134">搜尋結果醒目提示</span><span class="sxs-lookup"><span data-stu-id="267c3-134">Hit highlighting</span></span>
<span data-ttu-id="267c3-135">當您檢視搜尋結果時，會醒目顯示符合指定搜尋字詞的任何顯示屬性 (例如資料資產名稱、描述和標記)，讓您更輕鬆地找出指定搜尋傳回指定資料資產的原因。</span><span class="sxs-lookup"><span data-stu-id="267c3-135">When you view search results, any displayed properties that match the specified search terms (such as the data asset name, description, and tags) are highlighted to make it easier to identify why a given data asset was returned by a given search.</span></span>

> [!NOTE]
> <span data-ttu-id="267c3-136">若要關閉結果醒目提示，請使用 [醒目提示] 在資料目錄入口網站中進行切換。</span><span class="sxs-lookup"><span data-stu-id="267c3-136">To turn off hit highlighting, use the **Highlight** switch in the Data Catalog portal.</span></span>
>
>

<span data-ttu-id="267c3-137">當您檢視搜尋結果時，即使已啟用醒目提示，不一定能明顯看出為何某個資料資產會包含在其中。</span><span class="sxs-lookup"><span data-stu-id="267c3-137">When you view search results, it might not always be obvious why a data asset is included, even with hit highlighting enabled.</span></span> <span data-ttu-id="267c3-138">因為預設會搜尋所有屬性，某個資料資產可能因為符合資料行層級的屬性而被傳回。</span><span class="sxs-lookup"><span data-stu-id="267c3-138">Because all properties are searched by default, a data asset might be returned because of a match on a column-level property.</span></span> <span data-ttu-id="267c3-139">此外，多位使用者可以使用他們自己的標記和描述為已註冊的資料資產加上註解，因此並非所有的中繼資料都會顯示在搜尋結果清單中。</span><span class="sxs-lookup"><span data-stu-id="267c3-139">And because multiple users can annotate registered data assets with their own tags and descriptions, not all metadata might be displayed in the list of search results.</span></span>

<span data-ttu-id="267c3-140">在預設的並排顯示中，搜尋結果所顯示的每個磚，都含有**檢視搜尋字詞相符項目**圖示，讓您可以快速檢視相符項目的數目和位置，並在需要時移至該位置。</span><span class="sxs-lookup"><span data-stu-id="267c3-140">In the default tile view, each tile displayed in the search results includes a **View search term matches** icon, so that you can quickly view the number of matches and their location, and to jump to them if you want.</span></span>

 ![在 Azure 資料目錄入口網站顯示結果醒目提示並搜尋相符項目](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a><span data-ttu-id="267c3-142">摘要</span><span class="sxs-lookup"><span data-stu-id="267c3-142">Summary</span></span>
<span data-ttu-id="267c3-143">因為在資料目錄註冊資料來源，可讓您透過將結構化和描述性中繼資料從資料來源複製到目錄服務，所以更容易地探索及了解資料來源。</span><span class="sxs-lookup"><span data-stu-id="267c3-143">Because registering a data source with Data Catalog copies structural and descriptive metadata from the data source to the catalog service, the data source becomes easier to discover and understand.</span></span> <span data-ttu-id="267c3-144">註冊資料來源之後，您可以使用篩選來探索資料來源，並且在資料目錄入口網站搜尋。</span><span class="sxs-lookup"><span data-stu-id="267c3-144">After you've registered a data source, you can discover it by using filtering and search from within the Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="267c3-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="267c3-145">Next steps</span></span>
* <span data-ttu-id="267c3-146">如需如何探索資料來源的逐步詳細資料，請參閱[開始使用 Azure 資料目錄](data-catalog-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="267c3-146">For step-by-step details about how to discover data sources, see [Get Started with Azure Data Catalog](data-catalog-get-started.md).</span></span>
