---
title: "在 Azure 資料目錄中的 aaaHow toodiscover 資料來源 |Microsoft 文件"
description: "本文章重點說明 toodiscover Azure 資料目錄，包括搜尋和篩選所註冊的資料資產，並使用 hello 叫用的 hello Azure 資料目錄入口網站的反白顯示功能。"
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
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a><span data-ttu-id="9a9b9-103">在 Azure 資料目錄中 toodiscover 資料來源的方式</span><span class="sxs-lookup"><span data-stu-id="9a9b9-103">How toodiscover data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="9a9b9-104">簡介</span><span class="sxs-lookup"><span data-stu-id="9a9b9-104">Introduction</span></span>
<span data-ttu-id="9a9b9-105">Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料來源的註冊和探索系統。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="9a9b9-106">換句話說，資料目錄可於協助人們探索、了解和使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="9a9b9-107">資料來源以資料目錄註冊之後，它的中繼資料編製索引 hello 服務，您可以輕鬆地搜尋所需的 toodiscover hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-107">After a data source is registered with Data Catalog, its metadata is indexed by hello service, so that you can easily search toodiscover hello data you need.</span></span>

## <a name="searching-and-filtering"></a><span data-ttu-id="9a9b9-108">搜尋和篩選</span><span class="sxs-lookup"><span data-stu-id="9a9b9-108">Searching and filtering</span></span>
<span data-ttu-id="9a9b9-109">在資料目錄進行探索會使用兩種主要機制：搜尋和篩選。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-109">Discovery in Data Catalog uses two primary mechanisms: searching and filtering.</span></span>

<span data-ttu-id="9a9b9-110">搜尋是設計的 toobe 直覺式且功能強大。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-110">Searching is designed toobe both intuitive and powerful.</span></span> <span data-ttu-id="9a9b9-111">根據預設，搜尋詞彙會比對 hello 類別目錄，包括使用者提供的註解中的任何內容。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-111">By default, search terms are matched against any property in hello catalog, including user-provided annotations.</span></span>

<span data-ttu-id="9a9b9-112">篩選設計 toocomplement 搜尋。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-112">Filtering is designed toocomplement searching.</span></span> <span data-ttu-id="9a9b9-113">您可以選取特定的特性，例如專家、資料來源類型、物件類型和標記。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-113">You can select specific characteristics such as experts, data source type, object type, and tags.</span></span> <span data-ttu-id="9a9b9-114">您可以檢視只比對的資料資產，並限制搜尋結果 toomatching 資產。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-114">You can view only matching data assets, and constrain search results toomatching assets.</span></span>

<span data-ttu-id="9a9b9-115">藉由使用搜尋和篩選的組合，您可以快速瀏覽 hello 已經向您所需要的資料目錄 toodiscover hello 資料來源的資料來源。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-115">By using a combination of searching and filtering, you can quickly navigate hello data sources that have been registered with Data Catalog toodiscover hello data sources you need.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="9a9b9-116">搜尋語法</span><span class="sxs-lookup"><span data-stu-id="9a9b9-116">Search syntax</span></span>
<span data-ttu-id="9a9b9-117">雖然 hello 預設任意文字搜尋是既簡單又直接，但是您也可以使用資料目錄搜尋語法的 hello 搜尋結果中較大的控制權。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-117">Although hello default free text search is simple and intuitive, you can also use Data Catalog search syntax for greater control over hello search results.</span></span> <span data-ttu-id="9a9b9-118">下列技術資料類別目錄搜尋支援 hello:</span><span class="sxs-lookup"><span data-stu-id="9a9b9-118">Data Catalog search supports hello following techniques:</span></span>

| <span data-ttu-id="9a9b9-119">技巧</span><span class="sxs-lookup"><span data-stu-id="9a9b9-119">Technique</span></span> | <span data-ttu-id="9a9b9-120">使用</span><span class="sxs-lookup"><span data-stu-id="9a9b9-120">Use</span></span> | <span data-ttu-id="9a9b9-121">範例</span><span class="sxs-lookup"><span data-stu-id="9a9b9-121">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a9b9-122">基本搜尋</span><span class="sxs-lookup"><span data-stu-id="9a9b9-122">Basic search</span></span> |<span data-ttu-id="9a9b9-123">使用一或多個搜尋字詞的基本搜尋。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-123">Basic search that uses one or more search terms.</span></span> <span data-ttu-id="9a9b9-124">結果不符合任何屬性與一個或多個指定的 hello 詞彙任何資產。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-124">Results are any assets that match any property with one or more of hello terms specified.</span></span> |`sales data` |
| <span data-ttu-id="9a9b9-125">屬性範圍</span><span class="sxs-lookup"><span data-stu-id="9a9b9-125">Property scoping</span></span> |<span data-ttu-id="9a9b9-126">只會與 hello 比對 hello 搜尋詞彙的傳回資料來源指定的屬性。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-126">Return only data sources where hello search term is matched with hello specified property.</span></span> |`name:finance` |
| <span data-ttu-id="9a9b9-127">布林運算子</span><span class="sxs-lookup"><span data-stu-id="9a9b9-127">Boolean operators</span></span> |<span data-ttu-id="9a9b9-128">使用布林值作業擴大或縮小搜尋。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-128">Broaden or narrow a search by using Boolean operations.</span></span> |`finance NOT corporate` |
| <span data-ttu-id="9a9b9-129">使用括弧分組</span><span class="sxs-lookup"><span data-stu-id="9a9b9-129">Grouping with parenthesis</span></span> |<span data-ttu-id="9a9b9-130">使用括號 toogroup 組件的 hello 查詢 tooachieve 邏輯隔離，尤其是在配合布林運算子。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-130">Use parentheses toogroup parts of hello query tooachieve logical isolation, especially in conjunction with Boolean operators.</span></span> |`name:finance AND (tags:Q1 OR tags:Q2)` |
| <span data-ttu-id="9a9b9-131">比較運算子</span><span class="sxs-lookup"><span data-stu-id="9a9b9-131">Comparison operators</span></span> |<span data-ttu-id="9a9b9-132">針對具有數值和日期資料類型的屬性使用比較而非相等。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-132">Use comparisons other than equality for properties that have numeric and date data types.</span></span> |`modifiedTime > "11/05/2014"` |

<span data-ttu-id="9a9b9-133">如需有關資料類別目錄搜尋的詳細資訊，請參閱 hello [Azure 資料目錄](https://msdn.microsoft.com/library/azure/mt267594.aspx)發行項。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-133">For more information about Data Catalog search, see hello [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) article.</span></span>

## <a name="hit-highlighting"></a><span data-ttu-id="9a9b9-134">搜尋結果醒目提示</span><span class="sxs-lookup"><span data-stu-id="9a9b9-134">Hit highlighting</span></span>
<span data-ttu-id="9a9b9-135">當您檢視搜尋結果時，顯示任何符合指定的 hello 的屬性 （例如 hello 資料資產的名稱、 描述和標記） 的搜尋詞彙會反白顯示的 toomake 它更容易 tooidentify 為什麼給定的搜尋傳回指定的資料資產。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-135">When you view search results, any displayed properties that match hello specified search terms (such as hello data asset name, description, and tags) are highlighted toomake it easier tooidentify why a given data asset was returned by a given search.</span></span>

> [!NOTE]
> <span data-ttu-id="9a9b9-136">關閉反白顯示，使用 hello 叫用 tooturn**反白顯示**切換 hello 資料目錄入口網站中。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-136">tooturn off hit highlighting, use hello **Highlight** switch in hello Data Catalog portal.</span></span>
>
>

<span data-ttu-id="9a9b9-137">當您檢視搜尋結果時，即使已啟用醒目提示，不一定能明顯看出為何某個資料資產會包含在其中。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-137">When you view search results, it might not always be obvious why a data asset is included, even with hit highlighting enabled.</span></span> <span data-ttu-id="9a9b9-138">因為預設會搜尋所有屬性，某個資料資產可能因為符合資料行層級的屬性而被傳回。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-138">Because all properties are searched by default, a data asset might be returned because of a match on a column-level property.</span></span> <span data-ttu-id="9a9b9-139">與多個使用者可以使用他們自己的標籤和描述的已註冊的資料資產加上註解，因為並非所有的中繼資料可能會顯示 hello 搜尋結果清單中。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-139">And because multiple users can annotate registered data assets with their own tags and descriptions, not all metadata might be displayed in hello list of search results.</span></span>

<span data-ttu-id="9a9b9-140">在 hello 預設並排顯示檢視，包括在 hello 搜尋結果中顯示每個圖格**檢視搜尋術語符合**圖示，因此，如果您想要您可以快速檢視 hello 數目的相符項目和其位置，以及 toojump toothem。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-140">In hello default tile view, each tile displayed in hello search results includes a **View search term matches** icon, so that you can quickly view hello number of matches and their location, and toojump toothem if you want.</span></span>

 ![叫用反白顯示，而且在 hello Azure 資料目錄入口網站中的搜尋相符項目](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a><span data-ttu-id="9a9b9-142">摘要</span><span class="sxs-lookup"><span data-stu-id="9a9b9-142">Summary</span></span>
<span data-ttu-id="9a9b9-143">因為資料來源登錄至資料目錄複製結構，並將描述性中繼資料從 hello 資料來源 toohello 類別目錄服務，請 hello 資料來源變得更容易 toodiscover 並了解。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-143">Because registering a data source with Data Catalog copies structural and descriptive metadata from hello data source toohello catalog service, hello data source becomes easier toodiscover and understand.</span></span> <span data-ttu-id="9a9b9-144">您已註冊的資料來源之後，您可以探索使用篩選，並從 hello 資料目錄入口網站中進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-144">After you've registered a data source, you can discover it by using filtering and search from within hello Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a9b9-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a9b9-145">Next steps</span></span>
* <span data-ttu-id="9a9b9-146">如需如何逐步的詳細資訊 toodiscover 資料來源，請參閱[開始使用 Azure 資料目錄](data-catalog-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9a9b9-146">For step-by-step details about how toodiscover data sources, see [Get Started with Azure Data Catalog](data-catalog-get-started.md).</span></span>
