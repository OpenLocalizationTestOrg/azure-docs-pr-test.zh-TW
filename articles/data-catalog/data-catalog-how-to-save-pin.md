---
title: "aaaSave 搜尋和 pin 碼在 Azure 資料目錄中的資料資產 |Microsoft 文件"
description: "如何 tooarticle 反白顯示功能，在 Azure 資料目錄中儲存資料來源和資料資產，供日後使用。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="b6d1a-103">在 Azure 資料目錄中儲存搜尋和釘選資料資產</span><span class="sxs-lookup"><span data-stu-id="b6d1a-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="b6d1a-104">簡介</span><span class="sxs-lookup"><span data-stu-id="b6d1a-104">Introduction</span></span>
<span data-ttu-id="b6d1a-105">Azure 資料目錄提供用來探索資料來源的功能。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="b6d1a-106">您可以快速搜尋和篩選 hello 目錄 toolocate 資料來源和了解及其預期的用途，讓它更容易 toofind hello 右邊的資料手邊 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="b6d1a-107">但如果您需要 tooregularly 運作以 hello 相同的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="b6d1a-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="b6d1a-108">如果您與其他使用者定期未參與知識 toohello hello 目錄中的相同資料來源嗎？</span><span class="sxs-lookup"><span data-stu-id="b6d1a-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="b6d1a-109">在這些情況下，有 toorepeatedly 問題 hello 相同搜尋可能會沒有效率。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="b6d1a-110">這是已儲存的搜尋和已釘選的資料資產可發揮作用的地方。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="b6d1a-111">已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="b6d1a-111">Saved searches</span></span>
<span data-ttu-id="b6d1a-112">資料目錄中的已儲存搜尋是可重複使用的每個使用者搜尋定義。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="b6d1a-113">您可以定義搜尋，包括搜尋字詞、標籤及其他篩選條件，然後進行儲存。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="b6d1a-114">您可以重新執行 hello 儲存搜尋的定義更新 tooreturn 任何符合其搜尋條件的資料資產。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="b6d1a-115">建立已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="b6d1a-115">Create a saved search</span></span>
<span data-ttu-id="b6d1a-116">toocreate 儲存的搜尋，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="b6d1a-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="b6d1a-117">在 hello Azure 資料目錄入口網站中 hello**目前搜尋**視窗中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![目前搜尋設定的儲存連結](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="b6d1a-119">輸入您想 tooreuse，然後再按一下 hello 搜尋準則**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![目前搜尋設定的已儲存搜尋名稱](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="b6d1a-121">當系統提示您時，輸入 hello 儲存搜尋的名稱。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="b6d1a-122">選取有意義的名稱和描述 hello 將 hello 搜尋所傳回的資料資產。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="b6d1a-123">管理已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="b6d1a-123">Manage saved searches</span></span>
<span data-ttu-id="b6d1a-124">在您儲存一或多個搜尋後**已儲存的搜尋**hello 下方顯示選項**目前搜尋**方塊。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="b6d1a-125">當 hello 清單展開時，會顯示所有已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![已儲存的搜尋的清單](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="b6d1a-127">執行 hello 下列任何一項動作：</span><span class="sxs-lookup"><span data-stu-id="b6d1a-127">Do any of hello following:</span></span>

* <span data-ttu-id="b6d1a-128">tooexecute 搜尋，hello 清單中選取已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="b6d1a-129">tooview 一份管理選項，將已儲存的搜尋中，按一下向下箭號下一個 toohello 搜尋名稱的 hello。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![用於管理已儲存的搜尋的選項](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="b6d1a-131">tooenter hello 儲存搜尋的新名稱選取**重新命名**。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="b6d1a-132">hello 搜尋定義不會變更。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="b6d1a-133">tooremove hello 儲存搜尋清單，請選取**刪除**，然後確認 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="b6d1a-134">toomark hello 儲存搜尋，為您的預設搜尋，選取**儲存為預設**。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="b6d1a-135">如果 hello Azure 資料目錄首頁上，您可以執行"empty"的搜尋，則會執行預設的搜尋。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="b6d1a-136">此外，hello 標示為 hello 預設搜尋顯示在 hello hello 最上方的搜尋**已儲存的搜尋**清單。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="b6d1a-137">組織已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="b6d1a-137">Organizational saved searches</span></span>
<span data-ttu-id="b6d1a-138">您組織中的所有使用者都可以儲存搜尋供自己使用。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="b6d1a-139">資料目錄管理員也可以儲存搜尋 hello 組織內的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="b6d1a-140">當系統管理員儲存搜尋時，他們會看到與**hello 公司內共用**選項。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="b6d1a-141">選取此選項共用 hello 儲存 hello 組織中的 搜尋所有使用者。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![組織已儲存的搜尋](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="b6d1a-143">已釘選的資料資產</span><span class="sxs-lookup"><span data-stu-id="b6d1a-143">Pinned data assets</span></span>
<span data-ttu-id="b6d1a-144">利用已儲存的搜尋，您可以儲存並重複使用搜尋定義。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="b6d1a-145">經過一段時間，做為 hello 內容的 hello 目錄變更，可能會變更 hello hello 搜尋所傳回的資料資產。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="b6d1a-146">當您釘選的資料資產時，您可以明確地識別特定的資料資產 toomake 它們更容易 tooaccess 而不需要 toouse 搜尋。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="b6d1a-147">釘選資料資產相當簡單。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="b6d1a-148">tooadd hello 資料資產 tooyour 釘選清單中，您只是按一下 hello **pin**圖示。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="b6d1a-149">hello 資產磚在 hello 並排顯示檢視，和在 hello Azure 資料目錄入口網站中的 hello 清單檢視中的 hello 最左邊資料行中的 hello 角會顯示 hello 圖示。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![hello 資料資產釘選圖示](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="b6d1a-151">取消訂選資料資產相當簡單。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="b6d1a-152">只要按一下 hello**取消釘選**hello 選資產的圖示 tootoggle hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![hello 資料資產取消釘選圖示](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="b6d1a-154">hello 我資產區段</span><span class="sxs-lookup"><span data-stu-id="b6d1a-154">hello My Assets section</span></span>
<span data-ttu-id="b6d1a-155">hello 資料目錄入口網站首頁包括**我資產**顯示感興趣 toohello 目前使用者的資產的區段。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="b6d1a-156">此區段同時包含已釘選的資產和已儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-156">This section includes both pinned assets and saved searches.</span></span>

![hello hello 首頁上的 我的資產區段](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="b6d1a-158">摘要</span><span class="sxs-lookup"><span data-stu-id="b6d1a-158">Summary</span></span>
<span data-ttu-id="b6d1a-159">Azure 資料目錄提供功能，可讓您在需要時，更容易的 toodiscover hello 資料來源以便您和其他組織的成員可以花較少尋找資料和使用它的更多時間的時間。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="b6d1a-160">儲存的搜尋 和釘選的資料資產是以這些核心功能為基礎所建立，因此使用者可以輕鬆地識別所要重複使用的資料來源。</span><span class="sxs-lookup"><span data-stu-id="b6d1a-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
