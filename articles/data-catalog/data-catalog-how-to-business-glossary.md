---
title: "在 Azure 資料目錄中設定控管標記的商務詞彙 | Microsoft Docs"
description: "強調 Azure 資料目錄中商務詞彙的操作說明文章，可定義和使用一般商務詞彙來標記註冊的資料資產。"
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
ms.openlocfilehash: 83ca3b2d89a335a5fd6dddeaca7c11f6d0492234
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-the-business-glossary-for-governed-tagging"></a><span data-ttu-id="294c8-103">設定控管標記的商務詞彙</span><span class="sxs-lookup"><span data-stu-id="294c8-103">Set up the business glossary for governed tagging</span></span>
## <a name="introduction"></a><span data-ttu-id="294c8-104">簡介</span><span class="sxs-lookup"><span data-stu-id="294c8-104">Introduction</span></span>
<span data-ttu-id="294c8-105">Azure 資料目錄啟用了資料來源探索功能，讓您能夠輕鬆地探索和了解要執行分析和做出決策所需的資料來源。</span><span class="sxs-lookup"><span data-stu-id="294c8-105">Azure Data Catalog enables data-source discovery, so you can easily discover and understand the data sources that you need to perform analysis and make decisions.</span></span> <span data-ttu-id="294c8-106">當您能找到並了解最大範圍的可用資料來源時，這些功能就能發揮最大效果。</span><span class="sxs-lookup"><span data-stu-id="294c8-106">These capabilities make the biggest impact when you can find and understand the broadest range of available data sources.</span></span>

<span data-ttu-id="294c8-107">正在標記一個資料目錄功能，可提升對資產資料的了解。</span><span class="sxs-lookup"><span data-stu-id="294c8-107">One Data Catalog feature that promotes greater understanding of assets data is tagging.</span></span> <span data-ttu-id="294c8-108">藉由使用標記，您可以建立關鍵字與資產或資料行的關聯，進而透過搜尋或瀏覽更輕鬆地探索資產。</span><span class="sxs-lookup"><span data-stu-id="294c8-108">By using tagging, you can associate keywords with an asset or a column, which in turn makes it easier to discover the asset via searching or browsing.</span></span> <span data-ttu-id="294c8-109">標記也可協助您更輕鬆地了解資產的內容和用途。</span><span class="sxs-lookup"><span data-stu-id="294c8-109">Tagging also helps you more easily understand the context and intent of the asset.</span></span>

<span data-ttu-id="294c8-110">不過，標記有時會造成自己的問題。</span><span class="sxs-lookup"><span data-stu-id="294c8-110">However, tagging can sometimes cause problems of its own.</span></span> <span data-ttu-id="294c8-111">標記可能會造成問題的部分範例如下：</span><span class="sxs-lookup"><span data-stu-id="294c8-111">Some examples of problems that tagging can introduce are:</span></span>

* <span data-ttu-id="294c8-112">對某些資產使用縮寫，但對其他資產使用展開的文字。</span><span class="sxs-lookup"><span data-stu-id="294c8-112">The use of abbreviations on some assets and expanded text on others.</span></span> <span data-ttu-id="294c8-113">雖然目的是要使用相同的標籤標記資產，但是這項不一致會防礙資產的探索。</span><span class="sxs-lookup"><span data-stu-id="294c8-113">This inconsistency hinders the discovery of assets, even though the intent was to tag the assets with the same tag.</span></span>
* <span data-ttu-id="294c8-114">意義的潛在變化取決於內容。</span><span class="sxs-lookup"><span data-stu-id="294c8-114">Potential variations in meaning, depending on context.</span></span> <span data-ttu-id="294c8-115">例如，稱為「營收」的標籤在客戶資料集上可能表示客戶的營收，但是相同的標籤在每季銷售資料集上可能表示公司的每季營收。</span><span class="sxs-lookup"><span data-stu-id="294c8-115">For example, a tag called *Revenue* on a customer data set might mean revenue by customer, but the same tag on a quarterly sales dataset might mean quarterly revenue for the company.</span></span>  

<span data-ttu-id="294c8-116">為了協助解決上述和其他類似的挑戰，資料目錄包含商務詞彙。</span><span class="sxs-lookup"><span data-stu-id="294c8-116">To help address these and other similar challenges, Data Catalog includes a business glossary.</span></span>

<span data-ttu-id="294c8-117">透過使用資料目錄商務詞彙，組織可記錄關鍵商務字詞及其定義，以建立常用的商務詞彙。</span><span class="sxs-lookup"><span data-stu-id="294c8-117">By using the Data Catalog business glossary, an organization can document key business terms and their definitions to create a common business vocabulary.</span></span> <span data-ttu-id="294c8-118">此控管可達成整個組織的資料使用一致性。</span><span class="sxs-lookup"><span data-stu-id="294c8-118">This governance enables consistency in data usage across the organization.</span></span> <span data-ttu-id="294c8-119">在商務詞彙中定義字詞之後，該字詞便可指派給目錄中的資料資產。</span><span class="sxs-lookup"><span data-stu-id="294c8-119">After a term is defined in the business glossary, it can be assigned to a data asset in the catalog.</span></span> <span data-ttu-id="294c8-120">「控管標記」這種方法與標記方法相同。</span><span class="sxs-lookup"><span data-stu-id="294c8-120">This approach, *governed tagging*, is the same approach as tagging.</span></span>

## <a name="glossary-availability-and-privileges"></a><span data-ttu-id="294c8-121">詞彙可用性和權限</span><span class="sxs-lookup"><span data-stu-id="294c8-121">Glossary availability and privileges</span></span>
<span data-ttu-id="294c8-122">商務詞彙只能在標準版 Azure 資料目錄中使用。</span><span class="sxs-lookup"><span data-stu-id="294c8-122">The business glossary is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="294c8-123">免費版的資料目錄不包含詞彙，而且不提供控管標記功能。</span><span class="sxs-lookup"><span data-stu-id="294c8-123">The Free Edition of Data Catalog does not include a glossary, and it does not provide capabilities for governed tagging.</span></span>

<span data-ttu-id="294c8-124">您可透過資料目錄入口網站之瀏覽功能表中的 [詞彙] 選項存取商務詞彙。</span><span class="sxs-lookup"><span data-stu-id="294c8-124">You can access the business glossary via the **Glossary** option in the Data Catalog portal's navigation menu.</span></span>  

![存取商務詞彙](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

<span data-ttu-id="294c8-126">資料目錄管理員和詞彙管理員角色的成員可以建立、編輯及刪除商務詞彙中的詞彙。</span><span class="sxs-lookup"><span data-stu-id="294c8-126">Data Catalog administrators and members of the glossary administrators role can create, edit, and delete glossary terms in the business glossary.</span></span> <span data-ttu-id="294c8-127">所有的資料目錄使用者都可以檢視字詞定義，而且可以利用詞彙標記資產。</span><span class="sxs-lookup"><span data-stu-id="294c8-127">All Data Catalog users can view the term definitions and tag assets with glossary terms.</span></span>

![新增字彙](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a><span data-ttu-id="294c8-129">建立詞彙</span><span class="sxs-lookup"><span data-stu-id="294c8-129">Creating glossary terms</span></span>
<span data-ttu-id="294c8-130">資料目錄管理員和詞彙管理員可以按一下 [新增詞彙] 按鈕來建立詞彙。</span><span class="sxs-lookup"><span data-stu-id="294c8-130">Data Catalog administrators and glossary administrators can create glossary terms by clicking the **New Term** button.</span></span> <span data-ttu-id="294c8-131">每個詞彙包含下列欄位：</span><span class="sxs-lookup"><span data-stu-id="294c8-131">Each glossary term contains the following fields:</span></span>

* <span data-ttu-id="294c8-132">詞彙的商務定義</span><span class="sxs-lookup"><span data-stu-id="294c8-132">A business definition for the term</span></span>
* <span data-ttu-id="294c8-133">會擷取資產/資料行之指定用途或商務規則的描述</span><span class="sxs-lookup"><span data-stu-id="294c8-133">A description that captures the intended use or business rules for the asset or column</span></span>
* <span data-ttu-id="294c8-134">最了解這個詞彙的專案關係人清單</span><span class="sxs-lookup"><span data-stu-id="294c8-134">A list of stakeholders who know the most about the term</span></span>
* <span data-ttu-id="294c8-135">定義詞彙在其中組織之階層的父詞彙</span><span class="sxs-lookup"><span data-stu-id="294c8-135">The parent term, which defines the hierarchy in which the term is organized</span></span>

## <a name="glossary-term-hierarchies"></a><span data-ttu-id="294c8-136">詞彙階層</span><span class="sxs-lookup"><span data-stu-id="294c8-136">Glossary term hierarchies</span></span>
<span data-ttu-id="294c8-137">藉由使用資料目錄商務詞彙，組織可以用詞彙階層的方式描述其商務詞彙，而且可以建立詞彙分類，以便更能代表其商務分類。</span><span class="sxs-lookup"><span data-stu-id="294c8-137">By using the Data Catalog business glossary, an organization can describe its business vocabulary as a hierarchy of terms, and it can create a classification of terms that better represents its business taxonomy.</span></span>

<span data-ttu-id="294c8-138">字詞在階層的給定層級中必須是唯一項目。</span><span class="sxs-lookup"><span data-stu-id="294c8-138">A term must be unique at a given level of hierarchy.</span></span> <span data-ttu-id="294c8-139">不允許使用重複的名稱。</span><span class="sxs-lookup"><span data-stu-id="294c8-139">Duplicate names are not allowed.</span></span> <span data-ttu-id="294c8-140">在單一階層中，層級數目沒有限制，但是三個層級以下的階層通常更容易了解。</span><span class="sxs-lookup"><span data-stu-id="294c8-140">There is no limit to the number of levels in a hierarchy, but a hierarchy is often more easily understood when there are three levels or fewer.</span></span>

<span data-ttu-id="294c8-141">商務詞彙中的階層使用是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="294c8-141">The use of hierarchies in the business glossary is optional.</span></span> <span data-ttu-id="294c8-142">讓詞彙的父字詞欄位保留空白會在詞彙中建立字詞的一般 (非階層式) 清單。</span><span class="sxs-lookup"><span data-stu-id="294c8-142">Leaving the parent term field blank for glossary terms creates a flat (non-hierarchical) list of terms in the glossary.</span></span>  

## <a name="tagging-assets-with-glossary-terms"></a><span data-ttu-id="294c8-143">利用詞彙標記資產</span><span class="sxs-lookup"><span data-stu-id="294c8-143">Tagging assets with glossary terms</span></span>
<span data-ttu-id="294c8-144">在目錄中定義詞彙之後，標記資產的體驗已最佳化，可在使用者輸入其標籤時搜尋詞彙。</span><span class="sxs-lookup"><span data-stu-id="294c8-144">After glossary terms have been defined within the catalog, the experience of tagging assets is optimized to search the glossary as a user types a tag.</span></span> <span data-ttu-id="294c8-145">資料目錄入口網站會顯示可以選擇的相符詞彙清單。</span><span class="sxs-lookup"><span data-stu-id="294c8-145">The Data Catalog portal displays a list of matching glossary terms to choose from.</span></span> <span data-ttu-id="294c8-146">如果使用者從清單中選取一個詞彙，該字詞會新增至資產作為標籤 (也稱為詞彙標籤)。</span><span class="sxs-lookup"><span data-stu-id="294c8-146">If the user selects a glossary term from the list, the term is added to the asset as a tag (also called a glossary tag).</span></span> <span data-ttu-id="294c8-147">使用者也可以選擇藉由鍵入不在詞彙中的字詞來建立新標籤 (也稱為使用者標籤)。</span><span class="sxs-lookup"><span data-stu-id="294c8-147">The user can also choose to create a new tag by typing a term that's not in the glossary (also called a user tag).</span></span>

![使用一個使用者標籤和兩個詞彙標籤標記的資料資產](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> <span data-ttu-id="294c8-149">使用者標籤是免費版資料目錄中唯一支援的標籤類型。</span><span class="sxs-lookup"><span data-stu-id="294c8-149">User tags are the only type of tag supported in the Free Edition of Data Catalog.</span></span>
>
>

### <a name="hover-behavior-on-tags"></a><span data-ttu-id="294c8-150">將滑鼠游標停留在標記上的行為</span><span class="sxs-lookup"><span data-stu-id="294c8-150">Hover behavior on tags</span></span>
<span data-ttu-id="294c8-151">在資料目錄入口網站中，標籤的兩種類型在視覺上有所不同，而且將滑鼠游標停留的行為也不相同。</span><span class="sxs-lookup"><span data-stu-id="294c8-151">In the Data Catalog portal, the two types of tags are visually distinct and present different hover behaviors.</span></span> <span data-ttu-id="294c8-152">當您將滑鼠游標停留在使用者標籤上時，就可以看見標籤文字或新增該標籤的使用者。</span><span class="sxs-lookup"><span data-stu-id="294c8-152">When you hover over a user tag, you can see the tag text and the user or users who have added the tag.</span></span> <span data-ttu-id="294c8-153">當您將滑鼠游標停留在詞彙標籤上時，也會看見詞彙的定義，以及可開啟商務詞彙以檢視字詞完整定義的連結。</span><span class="sxs-lookup"><span data-stu-id="294c8-153">When you hover over a glossary tag, you also see the definition of the glossary term and a link to open the business glossary to view the full definition of the term.</span></span>

### <a name="search-filters-for-tags"></a><span data-ttu-id="294c8-154">標籤的搜尋篩選</span><span class="sxs-lookup"><span data-stu-id="294c8-154">Search filters for tags</span></span>
<span data-ttu-id="294c8-155">詞彙標籤和使用者標籤都可供搜尋，您可以將它們套用到搜尋中作為篩選。</span><span class="sxs-lookup"><span data-stu-id="294c8-155">Glossary tags and user tags are both searchable, and you can apply them as filters in a search.</span></span>

## <a name="summary"></a><span data-ttu-id="294c8-156">摘要</span><span class="sxs-lookup"><span data-stu-id="294c8-156">Summary</span></span>
<span data-ttu-id="294c8-157">透過使用 Azure 資料目錄中的商務詞彙和它啟用的控管標記，您可以利用一致的方式識別、管理與探索資料資產。</span><span class="sxs-lookup"><span data-stu-id="294c8-157">By using the business glossary in Azure Data Catalog, and the governed tagging it enables, you can identify, manage, and discover data assets in a consistent manner.</span></span> <span data-ttu-id="294c8-158">商務詞彙可提升組織成員對商務詞彙的學習。</span><span class="sxs-lookup"><span data-stu-id="294c8-158">The business glossary can promote learning of the business vocabulary by organization members.</span></span> <span data-ttu-id="294c8-159">詞彙也支援擷取有意義的中繼資料，其可簡化資產探索及了解。</span><span class="sxs-lookup"><span data-stu-id="294c8-159">The glossary also supports capturing meaningful metadata, which simplifies asset discovery and understanding.</span></span>

## <a name="next-steps"></a><span data-ttu-id="294c8-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="294c8-160">Next steps</span></span>
* [<span data-ttu-id="294c8-161">商務詞彙作業的 REST API 文件</span><span class="sxs-lookup"><span data-stu-id="294c8-161">REST API documentation for business glossary operations</span></span>](https://msdn.microsoft.com/library/mt708855.aspx)
