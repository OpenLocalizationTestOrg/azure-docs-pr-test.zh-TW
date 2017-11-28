---
title: "使用 hello Azure CDN 規則引擎 aaaOverride HTTP 行為 |Microsoft 文件"
description: "hello 規則引擎可讓您 toocustomize 如何 HTTP 要求會由 Azure CDN，例如封鎖 hello 傳遞某些類型的內容，定義快取的原則，並修改 HTTP 標頭。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="383f2-103">覆寫使用 hello Azure CDN 規則引擎的 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="383f2-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="383f2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="383f2-104">Overview</span></span>
<span data-ttu-id="383f2-105">hello 規則引擎可讓您 toocustomize 如何 HTTP 要求處理，例如封鎖 hello 傳遞某些類型的內容、 定義快取的原則，以及修改 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="383f2-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="383f2-106">本教學課程將示範建立規則，將會變更快取行為的 CDN 資產的 hello。</span><span class="sxs-lookup"><span data-stu-id="383f2-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="383f2-107">另外還有視訊內容用於 hello"[另請參閱](#see-also)」 一節。</span><span class="sxs-lookup"><span data-stu-id="383f2-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="383f2-108">如需詳細參考 toohello 語法，請參閱[規則引擎參考](cdn-rules-engine-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="383f2-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="383f2-109">教學課程</span><span class="sxs-lookup"><span data-stu-id="383f2-109">Tutorial</span></span>
1. <span data-ttu-id="383f2-110">從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="383f2-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="383f2-112">hello CDN 管理入口網站隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="383f2-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="383f2-113">按一下 hello **HTTP 大型** 索引標籤，後面接著**規則引擎**。</span><span class="sxs-lookup"><span data-stu-id="383f2-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="383f2-114">隨即顯示新規則的選項。</span><span class="sxs-lookup"><span data-stu-id="383f2-114">Options for a new rule are displayed.</span></span>
   
    ![CDN 新規則選項](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="383f2-116">多個規則列中的 hello 順序會影響處理的方式。</span><span class="sxs-lookup"><span data-stu-id="383f2-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="383f2-117">後續的規則可能會覆寫先前規則所指定的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="383f2-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="383f2-118">輸入的名稱在 hello**名稱 / 描述**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="383f2-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="383f2-119">識別 hello 的 hello 規則將套用到要求的類型。</span><span class="sxs-lookup"><span data-stu-id="383f2-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="383f2-120">根據預設，hello**永遠**已選取相符的條件。</span><span class="sxs-lookup"><span data-stu-id="383f2-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="383f2-121">本教學課程將使用 [永遠]  ，因此請維持選取。</span><span class="sxs-lookup"><span data-stu-id="383f2-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN 相符條件](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="383f2-123">有許多類型的相符項目可用在 hello 下拉式清單中的條件。</span><span class="sxs-lookup"><span data-stu-id="383f2-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="383f2-124">按一下 hello 藍色資訊圖示 toohello hello 符合條件的左將說明詳細資料中的 hello 目前選取的條件。</span><span class="sxs-lookup"><span data-stu-id="383f2-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="383f2-125">如需詳細資料中的條件式運算式 hello 完整清單，請參閱[規則引擎的條件運算式](cdn-rules-engine-reference-match-conditions.md)。</span><span class="sxs-lookup"><span data-stu-id="383f2-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="383f2-126">Hello 的詳細資料中的比對條件的完整清單，請參閱[規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)。</span><span class="sxs-lookup"><span data-stu-id="383f2-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="383f2-127">按一下 hello  **+** 太下一步按鈕**功能**tooadd 的新功能。</span><span class="sxs-lookup"><span data-stu-id="383f2-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="383f2-128">在左側 hello hello 下拉式清單中選取**強制內部 Max-age**。</span><span class="sxs-lookup"><span data-stu-id="383f2-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="383f2-129">在出現的 hello 文字方塊中，輸入**300**。</span><span class="sxs-lookup"><span data-stu-id="383f2-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="383f2-130">將保留 hello 剩餘預設值。</span><span class="sxs-lookup"><span data-stu-id="383f2-130">Leave hello remaining default values.</span></span>
   
   ![CDN 功能](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="383f2-132">因為與比對條件，按一下 hello 藍色資訊圖示 toohello hello 的新功能會顯示有關這項功能的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="383f2-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="383f2-133">Hello 案例**強制內部 Max-age**，我們會覆寫 hello 資產**Cache-control**和**Expires**標頭 toocontrol 時 hello CDN 邊緣節點將會重新整理 hello從 hello 原點的資產。</span><span class="sxs-lookup"><span data-stu-id="383f2-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="383f2-134">我們的範例 300 秒表示 hello CDN 邊緣節點就會快取 hello 資產 5 分鐘後再重新整理從其原來的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="383f2-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="383f2-135">Hello 的功能的詳細資料的完整清單，請參閱[規則引擎功能詳細資料](cdn-rules-engine-reference-features.md)。</span><span class="sxs-lookup"><span data-stu-id="383f2-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="383f2-136">按一下 hello**新增**按鈕 toosave hello 新規則。</span><span class="sxs-lookup"><span data-stu-id="383f2-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="383f2-137">hello 新規則現在正在等待核准。</span><span class="sxs-lookup"><span data-stu-id="383f2-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="383f2-138">一旦核准之後，將會變更 hello 狀態**暫止 XML**太**作用中的 XML**。</span><span class="sxs-lookup"><span data-stu-id="383f2-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="383f2-139">Too90 分鐘 toopropagate 透過 hello CDN 會在規則變更。</span><span class="sxs-lookup"><span data-stu-id="383f2-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="383f2-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="383f2-140">See also</span></span>
* [<span data-ttu-id="383f2-141">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="383f2-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="383f2-142">規則引擎參考</span><span class="sxs-lookup"><span data-stu-id="383f2-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="383f2-143">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="383f2-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="383f2-144">規則引擎條件運算式</span><span class="sxs-lookup"><span data-stu-id="383f2-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="383f2-145">規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="383f2-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="383f2-146">覆寫使用 hello 規則引擎的預設 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="383f2-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="383f2-147">[Azure Fridays: Azure CDN's powerful new Premium Features (影片：Azure 星期五：Azure CDN 強大的新高階功能)](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/)</span><span class="sxs-lookup"><span data-stu-id="383f2-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>