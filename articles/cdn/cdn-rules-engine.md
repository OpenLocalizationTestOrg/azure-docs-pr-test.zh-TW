---
title: "使用 Azure CDN 規則引擎覆寫 HTTP 行為 | Microsoft Docs"
description: "規則引擎可讓您自訂 Azure CDN 處理 HTTP 要求的方式，例如封鎖傳遞特定類型的內容、定義快取原則及修改 HTTP 標頭。"
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
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="c4717-103">使用 Azure CDN 規則引擎覆寫 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="c4717-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c4717-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c4717-104">Overview</span></span>
<span data-ttu-id="c4717-105">規則引擎可讓您自訂 HTTP 要求的處理方式，例如封鎖傳遞特定類型的內容、定義快取原則及修改 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="c4717-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="c4717-106">本教學課程將示範如何建立用以變更 CDN 資產之快取行為的規則。</span><span class="sxs-lookup"><span data-stu-id="c4717-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="c4717-107">「[另請參閱](#see-also)」一節中還有視訊內容。</span><span class="sxs-lookup"><span data-stu-id="c4717-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="c4717-108">如需詳細的語法參考，請參閱[規則引擎參考](cdn-rules-engine-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="c4717-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="c4717-109">教學課程</span><span class="sxs-lookup"><span data-stu-id="c4717-109">Tutorial</span></span>
1. <span data-ttu-id="c4717-110">在 [CDN 設定檔] 刀鋒視窗中，按一下 [管理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4717-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="c4717-112">隨即開啟 CDN 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="c4717-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="c4717-113">依序按一下 [HTTP 大型] 索引標籤和 [規則引擎]。</span><span class="sxs-lookup"><span data-stu-id="c4717-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="c4717-114">隨即顯示新規則的選項。</span><span class="sxs-lookup"><span data-stu-id="c4717-114">Options for a new rule are displayed.</span></span>
   
    ![CDN 新規則選項](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="c4717-116">多項規則的列出順序會影響規則的處理方式。</span><span class="sxs-lookup"><span data-stu-id="c4717-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="c4717-117">後一項規則可能會覆寫前一項規則所指定的動作。</span><span class="sxs-lookup"><span data-stu-id="c4717-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="c4717-118">在 [名稱/描述]  文字方塊中輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="c4717-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="c4717-119">識別將套用此規則的要求類型。</span><span class="sxs-lookup"><span data-stu-id="c4717-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="c4717-120">預設會選取 [永遠]  相符條件。</span><span class="sxs-lookup"><span data-stu-id="c4717-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="c4717-121">本教學課程將使用 [永遠]  ，因此請維持選取。</span><span class="sxs-lookup"><span data-stu-id="c4717-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN 相符條件](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="c4717-123">下拉式清單中提供許多類型的相符條件。</span><span class="sxs-lookup"><span data-stu-id="c4717-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="c4717-124">按一下相符條件左側的藍色資訊圖示，即會詳細說明目前選取的條件。</span><span class="sxs-lookup"><span data-stu-id="c4717-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="c4717-125">如需詳細的條件運算式完整清單，請參閱[規則引擎條件運算式](cdn-rules-engine-reference-match-conditions.md)。</span><span class="sxs-lookup"><span data-stu-id="c4717-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="c4717-126">如需完整比對條件清單的詳細資訊，請參閱[規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)。</span><span class="sxs-lookup"><span data-stu-id="c4717-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="c4717-127">按一下 [功能] 旁的 **+** 按鈕，以新增功能。</span><span class="sxs-lookup"><span data-stu-id="c4717-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="c4717-128">在左側下拉式清單中，選取 [強制執行內部最大壽命]。</span><span class="sxs-lookup"><span data-stu-id="c4717-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="c4717-129">在出現的文字方塊中，輸入 **300**。</span><span class="sxs-lookup"><span data-stu-id="c4717-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="c4717-130">保留其餘預設值。</span><span class="sxs-lookup"><span data-stu-id="c4717-130">Leave the remaining default values.</span></span>
   
   ![CDN 功能](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="c4717-132">如同相符條件，按一下新功能左側的藍色資訊圖示會顯示這項功能的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c4717-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="c4717-133">在 [強制執行內部最大壽命] 中，我們將覆寫資產的 **Cache-Control** 和 **Expires** 標頭，以控制 CDN 邊緣節點何時要從原始來源重新整理資產。</span><span class="sxs-lookup"><span data-stu-id="c4717-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="c4717-134">我們的範例為 300 秒，表示 CDN 邊緣節點會快取資產 5 分鐘，再從其原始來源重新整理資產。</span><span class="sxs-lookup"><span data-stu-id="c4717-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="c4717-135">如需完整功能清單的詳細資訊，請參閱[規則引擎功能詳細資訊](cdn-rules-engine-reference-features.md)。</span><span class="sxs-lookup"><span data-stu-id="c4717-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="c4717-136">按一下 [加入]  按鈕，以儲存新規則。</span><span class="sxs-lookup"><span data-stu-id="c4717-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="c4717-137">新規則現在正在等待核准。</span><span class="sxs-lookup"><span data-stu-id="c4717-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="c4717-138">核准後，狀態會從 [暫止 XML] 變更為 [使用中 XML]。</span><span class="sxs-lookup"><span data-stu-id="c4717-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c4717-139">規則變更可能需要最多 90 分鐘才能傳遍 CDN。</span><span class="sxs-lookup"><span data-stu-id="c4717-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="c4717-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c4717-140">See also</span></span>
* [<span data-ttu-id="c4717-141">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="c4717-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="c4717-142">規則引擎參考</span><span class="sxs-lookup"><span data-stu-id="c4717-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="c4717-143">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="c4717-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="c4717-144">規則引擎條件運算式</span><span class="sxs-lookup"><span data-stu-id="c4717-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="c4717-145">規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="c4717-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="c4717-146">使用規則引擎覆寫預設的 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="c4717-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="c4717-147">[Azure Fridays: Azure CDN's powerful new Premium Features (影片：Azure 星期五：Azure CDN 強大的新高階功能)](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/)</span><span class="sxs-lookup"><span data-stu-id="c4717-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>