---
title: "向上 hello 管標記，在 Azure 資料目錄中的商務詞彙 aaaSet |Microsoft 文件"
description: "如何 tooarticle 反白顯示 hello 商務字彙中定義及使用通用的商務詞彙 tootag Azure 資料目錄註冊的資料資產。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a><span data-ttu-id="6c9d4-103">設定決定標記 hello 商務字彙</span><span class="sxs-lookup"><span data-stu-id="6c9d4-103">Set up hello business glossary for governed tagging</span></span>
## <a name="introduction"></a><span data-ttu-id="6c9d4-104">簡介</span><span class="sxs-lookup"><span data-stu-id="6c9d4-104">Introduction</span></span>
<span data-ttu-id="6c9d4-105">Azure 資料目錄可讓資料來源探索，因此您可以輕鬆地找出並了解 hello 資料來源，您需要 tooperform 分析和做出決策。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-105">Azure Data Catalog enables data-source discovery, so you can easily discover and understand hello data sources that you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="6c9d4-106">時，您可以尋找並了解可用的資料來源的 hello 大範圍，這些功能會構成 hello 大影響。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-106">These capabilities make hello biggest impact when you can find and understand hello broadest range of available data sources.</span></span>

<span data-ttu-id="6c9d4-107">正在標記一個資料目錄功能，可提升對資產資料的了解。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-107">One Data Catalog feature that promotes greater understanding of assets data is tagging.</span></span> <span data-ttu-id="6c9d4-108">藉由使用標記，您可以與資產或資料行，接著使其更容易 toodiscover hello 資產透過搜尋或瀏覽關聯關鍵字。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-108">By using tagging, you can associate keywords with an asset or a column, which in turn makes it easier toodiscover hello asset via searching or browsing.</span></span> <span data-ttu-id="6c9d4-109">標記也可協助您更輕鬆地了解 hello 內容和 hello 資產的意圖。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-109">Tagging also helps you more easily understand hello context and intent of hello asset.</span></span>

<span data-ttu-id="6c9d4-110">不過，標記有時會造成自己的問題。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-110">However, tagging can sometimes cause problems of its own.</span></span> <span data-ttu-id="6c9d4-111">標記可能會造成問題的部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="6c9d4-111">Some examples of problems that tagging can introduce are:</span></span>

* <span data-ttu-id="6c9d4-112">hello 使用上的某些資產的縮寫與在其他的展開的文字。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-112">hello use of abbreviations on some assets and expanded text on others.</span></span> <span data-ttu-id="6c9d4-113">此不一致性所妨礙 hello 探索的資產，即使 hello 意圖是以 hello tootag hello 資產相同的標記。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-113">This inconsistency hinders hello discovery of assets, even though hello intent was tootag hello assets with hello same tag.</span></span>
* <span data-ttu-id="6c9d4-114">意義的潛在變化取決於內容。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-114">Potential variations in meaning, depending on context.</span></span> <span data-ttu-id="6c9d4-115">例如，標記稱為*營收*某個客戶的資料集可能表示營收的客戶，但 hello 每季的銷售資料集上的相同標記可能代表每季 hello 公司營收。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-115">For example, a tag called *Revenue* on a customer data set might mean revenue by customer, but hello same tag on a quarterly sales dataset might mean quarterly revenue for hello company.</span></span>  

<span data-ttu-id="6c9d4-116">toohelp 解決這些和其他類似的挑戰，資料目錄包含商務字彙。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-116">toohelp address these and other similar challenges, Data Catalog includes a business glossary.</span></span>

<span data-ttu-id="6c9d4-117">藉由使用 hello 資料目錄商務字彙，組織可以記錄關鍵商務字詞以及其定義 toocreate 通用的商務詞彙。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-117">By using hello Data Catalog business glossary, an organization can document key business terms and their definitions toocreate a common business vocabulary.</span></span> <span data-ttu-id="6c9d4-118">此控管 hello 組織內啟用使用量資料的一致性。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-118">This governance enables consistency in data usage across hello organization.</span></span> <span data-ttu-id="6c9d4-119">Hello 商務字彙中定義的詞彙之後，它可以指派 tooa hello 目錄中的資料資產。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-119">After a term is defined in hello business glossary, it can be assigned tooa data asset in hello catalog.</span></span> <span data-ttu-id="6c9d4-120">這種方式，*控管標記*，是 hello 一樣標記的方法。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-120">This approach, *governed tagging*, is hello same approach as tagging.</span></span>

## <a name="glossary-availability-and-privileges"></a><span data-ttu-id="6c9d4-121">詞彙可用性和權限</span><span class="sxs-lookup"><span data-stu-id="6c9d4-121">Glossary availability and privileges</span></span>
<span data-ttu-id="6c9d4-122">hello 商務字彙是只能在 hello 標準版本的 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-122">hello business glossary is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="6c9d4-123">hello 的資料目錄免費 Edition 不包括詞彙，且不提供功能來管標記。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-123">hello Free Edition of Data Catalog does not include a glossary, and it does not provide capabilities for governed tagging.</span></span>

<span data-ttu-id="6c9d4-124">您可以存取透過 hello hello 商務字彙**詞彙**hello 資料目錄入口網站的瀏覽功能表中的選項。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-124">You can access hello business glossary via hello **Glossary** option in hello Data Catalog portal's navigation menu.</span></span>  

![存取 hello 商務字彙](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

<span data-ttu-id="6c9d4-126">資料目錄管理員和系統管理員角色可以建立、 hello 詞彙的成員編輯和刪除在 hello 的商務詞彙的詞彙。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-126">Data Catalog administrators and members of hello glossary administrators role can create, edit, and delete glossary terms in hello business glossary.</span></span> <span data-ttu-id="6c9d4-127">所有的資料目錄使用者可以檢視 hello 詞彙定義和字彙字詞標籤資產。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-127">All Data Catalog users can view hello term definitions and tag assets with glossary terms.</span></span>

![新增字彙](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a><span data-ttu-id="6c9d4-129">建立詞彙</span><span class="sxs-lookup"><span data-stu-id="6c9d4-129">Creating glossary terms</span></span>
<span data-ttu-id="6c9d4-130">資料目錄管理員和詞彙的系統管理員可以建立詞彙即可 hello**新詞彙**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-130">Data Catalog administrators and glossary administrators can create glossary terms by clicking hello **New Term** button.</span></span> <span data-ttu-id="6c9d4-131">每個詞彙的詞彙包含下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c9d4-131">Each glossary term contains hello following fields:</span></span>

* <span data-ttu-id="6c9d4-132">Hello 詞彙的商務定義</span><span class="sxs-lookup"><span data-stu-id="6c9d4-132">A business definition for hello term</span></span>
* <span data-ttu-id="6c9d4-133">擷取預期的 hello 用途或商務規則 hello 資產或資料行的描述</span><span class="sxs-lookup"><span data-stu-id="6c9d4-133">A description that captures hello intended use or business rules for hello asset or column</span></span>
* <span data-ttu-id="6c9d4-134">專案關係人知道 hello hello 詞彙的最相關的清單</span><span class="sxs-lookup"><span data-stu-id="6c9d4-134">A list of stakeholders who know hello most about hello term</span></span>
* <span data-ttu-id="6c9d4-135">hello 父系字詞定義詞彙組織中的 hello hello 階層</span><span class="sxs-lookup"><span data-stu-id="6c9d4-135">hello parent term, which defines hello hierarchy in which hello term is organized</span></span>

## <a name="glossary-term-hierarchies"></a><span data-ttu-id="6c9d4-136">詞彙階層</span><span class="sxs-lookup"><span data-stu-id="6c9d4-136">Glossary term hierarchies</span></span>
<span data-ttu-id="6c9d4-137">藉由使用 hello 資料目錄商務字彙，組織可以為階層的詞彙，描述其商務詞彙，而且可以建立的詞彙更能代表其商務分類的分類。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-137">By using hello Data Catalog business glossary, an organization can describe its business vocabulary as a hierarchy of terms, and it can create a classification of terms that better represents its business taxonomy.</span></span>

<span data-ttu-id="6c9d4-138">字詞在階層的給定層級中必須是唯一項目。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-138">A term must be unique at a given level of hierarchy.</span></span> <span data-ttu-id="6c9d4-139">不允許使用重複的名稱。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-139">Duplicate names are not allowed.</span></span> <span data-ttu-id="6c9d4-140">在階層中，層級的數量沒有限制 toohello 但階層通常更容易了解時有三個層級或更少。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-140">There is no limit toohello number of levels in a hierarchy, but a hierarchy is often more easily understood when there are three levels or fewer.</span></span>

<span data-ttu-id="6c9d4-141">階層中 hello 商務字彙 hello 使用是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-141">hello use of hierarchies in hello business glossary is optional.</span></span> <span data-ttu-id="6c9d4-142">讓 hello 父詞彙欄位空白的字彙字詞 hello 詞彙中建立詞彙 （非階層式） 的一般的清單。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-142">Leaving hello parent term field blank for glossary terms creates a flat (non-hierarchical) list of terms in hello glossary.</span></span>  

## <a name="tagging-assets-with-glossary-terms"></a><span data-ttu-id="6c9d4-143">利用詞彙標記資產</span><span class="sxs-lookup"><span data-stu-id="6c9d4-143">Tagging assets with glossary terms</span></span>
<span data-ttu-id="6c9d4-144">詞彙定義 hello 目錄中之後，標記資產 hello 體驗為最佳化的 toosearch hello 詞彙使用者類型標記。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-144">After glossary terms have been defined within hello catalog, hello experience of tagging assets is optimized toosearch hello glossary as a user types a tag.</span></span> <span data-ttu-id="6c9d4-145">hello 資料目錄入口網站會顯示從相符詞彙條款 toochoose 的清單。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-145">hello Data Catalog portal displays a list of matching glossary terms toochoose from.</span></span> <span data-ttu-id="6c9d4-146">如果 hello 使用者從 hello 清單中選取的詞彙的詞彙，hello 詞彙加入 toohello 資產 （也稱為詞彙標記） 的標記。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-146">If hello user selects a glossary term from hello list, hello term is added toohello asset as a tag (also called a glossary tag).</span></span> <span data-ttu-id="6c9d4-147">hello 使用者也可以選擇 toocreate 新標記輸入不是處於 hello 的詞彙 （也稱為使用者標記） 的詞彙。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-147">hello user can also choose toocreate a new tag by typing a term that's not in hello glossary (also called a user tag).</span></span>

![使用一個使用者標籤和兩個詞彙標籤標記的資料資產](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> <span data-ttu-id="6c9d4-149">使用者標記的標記中支援的型別 hello 的資料目錄免費 Edition 只有在已經 hello。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-149">User tags are hello only type of tag supported in hello Free Edition of Data Catalog.</span></span>
>
>

### <a name="hover-behavior-on-tags"></a><span data-ttu-id="6c9d4-150">將滑鼠游標停留在標記上的行為</span><span class="sxs-lookup"><span data-stu-id="6c9d4-150">Hover behavior on tags</span></span>
<span data-ttu-id="6c9d4-151">在 hello 資料目錄入口網站 hello 兩種類型的標記都是以視覺化方式不同，且有不同的動態顯示行為。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-151">In hello Data Catalog portal, hello two types of tags are visually distinct and present different hover behaviors.</span></span> <span data-ttu-id="6c9d4-152">當您將滑鼠停留在使用者標記時，您可以看到 hello 標記文字和 hello 使用者或使用者已新增 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-152">When you hover over a user tag, you can see hello tag text and hello user or users who have added hello tag.</span></span> <span data-ttu-id="6c9d4-153">您將滑鼠停留在詞彙標記，您也看到 hello 字彙 hello 定義及連結 tooopen hello 商務字彙 tooview hello 完整定義 hello 詞彙。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-153">When you hover over a glossary tag, you also see hello definition of hello glossary term and a link tooopen hello business glossary tooview hello full definition of hello term.</span></span>

### <a name="search-filters-for-tags"></a><span data-ttu-id="6c9d4-154">標籤的搜尋篩選</span><span class="sxs-lookup"><span data-stu-id="6c9d4-154">Search filters for tags</span></span>
<span data-ttu-id="6c9d4-155">詞彙標籤和使用者標籤都可供搜尋，您可以將它們套用到搜尋中作為篩選。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-155">Glossary tags and user tags are both searchable, and you can apply them as filters in a search.</span></span>

## <a name="summary"></a><span data-ttu-id="6c9d4-156">摘要</span><span class="sxs-lookup"><span data-stu-id="6c9d4-156">Summary</span></span>
<span data-ttu-id="6c9d4-157">您可以藉由使用 Azure 資料目錄，和 hello 控管標記它可讓 hello 商務字彙，識別、 管理及探索資料資產以一致的方式。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-157">By using hello business glossary in Azure Data Catalog, and hello governed tagging it enables, you can identify, manage, and discover data assets in a consistent manner.</span></span> <span data-ttu-id="6c9d4-158">hello 商務字彙可以升級學習的組織成員 hello 的商務詞彙。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-158">hello business glossary can promote learning of hello business vocabulary by organization members.</span></span> <span data-ttu-id="6c9d4-159">hello 詞彙也支援擷取有意義的中繼資料，可簡化資產探索及了解。</span><span class="sxs-lookup"><span data-stu-id="6c9d4-159">hello glossary also supports capturing meaningful metadata, which simplifies asset discovery and understanding.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c9d4-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c9d4-160">Next steps</span></span>
* [<span data-ttu-id="6c9d4-161">商務詞彙作業的 REST API 文件</span><span class="sxs-lookup"><span data-stu-id="6c9d4-161">REST API documentation for business glossary operations</span></span>](https://msdn.microsoft.com/library/mt708855.aspx)
