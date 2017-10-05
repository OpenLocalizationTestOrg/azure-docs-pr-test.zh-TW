---
title: "將您的供應項目部署至 Azure Marketplace | Microsoft Docs"
description: "了解並逐步依照指示執行，將您的供應項目 (虛擬機器映像、開發人員服務、資料服務等) 部署至 Azure Marketplace。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: 12dc81642905cd9449a1032c7ab57298e6b69ba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-offer-to-the-azure-marketplace"></a><span data-ttu-id="843dd-103">將您的供應項目部署至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="843dd-103">Deploy your offer to the Azure Marketplace</span></span>
<span data-ttu-id="843dd-104">當您對供應項目感到滿意 (意即經過測試的客戶案例、行銷內容等) 並準備推出時，請在 [發佈] 索引標籤中要求 [推送至生產環境]。</span><span class="sxs-lookup"><span data-stu-id="843dd-104">When you are satisfied with your offer (that is, you have tested customer scenarios, marketing content, etc.) and you are ready to launch, request **Push to production** on the **Publish** tab.</span></span>  

1. <span data-ttu-id="843dd-105">發佈入口網站的 [逐步解說] 頁面中的四個步驟應是完成和綠色的狀態。</span><span class="sxs-lookup"><span data-stu-id="843dd-105">The four steps under the WALKTHROUGH page in the Publishing portal should be completed and green.</span></span> <span data-ttu-id="843dd-106">對於虛擬機器供應項目，請務必遵循下列指導方針。</span><span class="sxs-lookup"><span data-stu-id="843dd-106">For Virtual Machine offers, ensure that the following guidelines are followed.</span></span>
   
    ![繪圖][img-pubportal-walkthru-checked]
2. <span data-ttu-id="843dd-108">從左側清單中選取 [ **發佈** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="843dd-108">Select the **Publish** tab from the list on the left side.</span></span>
   
    ![繪圖][img-pubportal-menu-publish]
3. <span data-ttu-id="843dd-110">按一下 [要求核准推送到生產環境] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="843dd-110">Click the button **Request approval to push to production**.</span></span> <span data-ttu-id="843dd-111">提出要求後，核准小組會執行最後檢閱，然後您的供應項目即可在 Azure Marketplace 中公開發行。</span><span class="sxs-lookup"><span data-stu-id="843dd-111">Once the request is made, the approval team executes a final review, and then your offer will be available in the Azure Marketplace.</span></span>
   
    ![繪圖][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> <span data-ttu-id="843dd-113">如果是「虛擬機器」，當您按一下 [要求核准推送到生產環境] 按鈕時，會在場景後方執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="843dd-113">In case of Virtual Machines, when you click on the button Request approval to push to production, the following steps are performed behind the scene.</span></span> <span data-ttu-id="843dd-114">您可以在發佈入口網站的 [發佈] 索引標籤下檢視每個步驟的進度。</span><span class="sxs-lookup"><span data-stu-id="843dd-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="843dd-115">您必須定期查看此頁面是否有需要您更正的任何失敗資訊 (直到狀態顯示「已列出」為止) 。</span><span class="sxs-lookup"><span data-stu-id="843dd-115">You must check this page at regular interval (until the status shows "Listed") for any failure information which need correction from your end.</span></span>
> 
> * <span data-ttu-id="843dd-116">一開始，您的生產環境要求會送到驗證 VHD 的憑證小組。</span><span class="sxs-lookup"><span data-stu-id="843dd-116">At first your production request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="843dd-117">不過，如果您是要更新已列出的供應項目或您的要求只有行銷變更，則會略過憑證步驟。</span><span class="sxs-lookup"><span data-stu-id="843dd-117">However, if you are updating your already listed offer and the request has got only marketing change, then the certification step is skipped.</span></span>
> * <span data-ttu-id="843dd-118">在下一個步驟中，要求會送交驗證供應項目行銷內容的內容驗證小組。</span><span class="sxs-lookup"><span data-stu-id="843dd-118">At the next step, the request come to the content validation team who verify the marketing content of the offer.</span></span>
> * <span data-ttu-id="843dd-119">如果上述步驟都成功，便核准供應項目進入生產環境。</span><span class="sxs-lookup"><span data-stu-id="843dd-119">If the above steps are successful, then the offer is approved in production.</span></span> <span data-ttu-id="843dd-120">此時在發佈入口網站中的狀態會變成「已列出」。</span><span class="sxs-lookup"><span data-stu-id="843dd-120">At this time, the status become "Listed" in the publishing portal.</span></span> <span data-ttu-id="843dd-121">不過，這個「已列出」狀態不代表程序已完成。</span><span class="sxs-lookup"><span data-stu-id="843dd-121">However, this “Listed” status does not imply that the process is complete.</span></span> <span data-ttu-id="843dd-122">在可於 Azure Marketplace 公開發行供應項目之前，必須先完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="843dd-122">The following steps need to be complete before the offer is available in the Azure Marketplace.</span></span>
> * <span data-ttu-id="843dd-123">一旦供應項目於上述步驟中經核准進入生產環境，就會開始跨所有 Azure 資料中心複寫供應項目。</span><span class="sxs-lookup"><span data-stu-id="843dd-123">Once the offer is approved in production in the step above, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="843dd-124">複寫通常需要 24-48 小時才能完成，但依據 VHD 大小而定，最長可能需要一週的時間。</span><span class="sxs-lookup"><span data-stu-id="843dd-124">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="843dd-125">不過，如果您是要更新已列出的供應項目或您的要求只有行銷變更，則複寫會更快速。</span><span class="sxs-lookup"><span data-stu-id="843dd-125">However, if you are updating your already listed offer and it has got only marketing change, then the replication is faster.</span></span>
> * <span data-ttu-id="843dd-126">當複寫完成後，供應項目就會在 Azure Marketplace 公開發行。</span><span class="sxs-lookup"><span data-stu-id="843dd-126">When the replication is complete, then the offer will be available in the Azure Marketplace.</span></span>
> 
> <span data-ttu-id="843dd-127">當供應項目的狀態為 [草稿] 時 (也就是永遠不會 [推送至預備環境] 或 [推送至生產環境])，您可隨時將其刪除。</span><span class="sxs-lookup"><span data-stu-id="843dd-127">You can always delete the offer while it is in a **Draft** status (i.e., never **Push to staging** or **Push to production**).</span></span> <span data-ttu-id="843dd-128">在 [歷程記錄] 索引標籤中，按一下頁面底部的 [捨棄草稿] 按鈕以刪除草稿。</span><span class="sxs-lookup"><span data-stu-id="843dd-128">On the **History** tab, click the **Discard draft** button at the bottom of the page to delete a draft.</span></span>
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a><span data-ttu-id="843dd-129">適用於所有虛擬機器供應項目的生產環境檢查清單</span><span class="sxs-lookup"><span data-stu-id="843dd-129">Production checklist for all Virtual Machine offers</span></span>
* <span data-ttu-id="843dd-130">請確定您是 Microsoft Azure 認證合作夥伴</span><span class="sxs-lookup"><span data-stu-id="843dd-130">Ensure that you are a Microsoft Azure Certified partner</span></span>
* <span data-ttu-id="843dd-131">在 [SKU] 索引標籤下，只有當 SKU 是方案範本的一部分時，[從 Marketplace 隱藏此 SKU，因為應該永遠透過方案範本購買它] 選項才應該標示為 [是]。</span><span class="sxs-lookup"><span data-stu-id="843dd-131">Under the SKUs tab, the option "Hide this SKU from the Marketplace because it should always be bought via a solution template" should be marked as YES only if the SKU is a part of a Solution Template.</span></span> <span data-ttu-id="843dd-132">否則，這個選項應該永遠標示為 [否]。</span><span class="sxs-lookup"><span data-stu-id="843dd-132">In all the other cases, this option should always be marked as NO.</span></span>
* <span data-ttu-id="843dd-133">請記住︰您不應在 SKU 列出後變更 SKU 可見性設定。</span><span class="sxs-lookup"><span data-stu-id="843dd-133">Remember: You should not change the SKU visibility setting once the SKU is listed.</span></span> <span data-ttu-id="843dd-134">我們不支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="843dd-134">We do not support this functionality.</span></span>
* <span data-ttu-id="843dd-135">請確定標誌遵循以下的 Azure Marketplace 標誌指導方針。</span><span class="sxs-lookup"><span data-stu-id="843dd-135">Ensure that the logos adhere to the Azure Marketplace logo guidelines given below.</span></span>
* <span data-ttu-id="843dd-136">供應項目和 SKU 描述不應相同。</span><span class="sxs-lookup"><span data-stu-id="843dd-136">Offer and SKU description shouldn’t be same.</span></span>
* <span data-ttu-id="843dd-137">SKU 的標題和供應項目完整摘要不應相同。</span><span class="sxs-lookup"><span data-stu-id="843dd-137">SKU’s Title and Offer Long summary shouldn’t be same.</span></span>
* <span data-ttu-id="843dd-138">SKU 標題和供應項目摘要不應相同。</span><span class="sxs-lookup"><span data-stu-id="843dd-138">SKU Title and Offer Summary shouldn’t be same.</span></span>
* <span data-ttu-id="843dd-139">對於含多個 SKU 的供應項目，其 SKU 標題不應相同。</span><span class="sxs-lookup"><span data-stu-id="843dd-139">SKU Titles should not be identical for an offer with multiple SKUs.</span></span>

<span data-ttu-id="843dd-140">**Azure Marketplace 標誌指導方針**</span><span class="sxs-lookup"><span data-stu-id="843dd-140">**Azure Marketplace logo guidelines**</span></span>

* <span data-ttu-id="843dd-141">Azure 設計具有簡單的調色盤。</span><span class="sxs-lookup"><span data-stu-id="843dd-141">The Azure design has a simple color palette.</span></span> <span data-ttu-id="843dd-142">請保持標誌上具有最少的主要和次要色彩數目。</span><span class="sxs-lookup"><span data-stu-id="843dd-142">Keep the number of primary and secondary colors on your logo low.</span></span>
* <span data-ttu-id="843dd-143">Azure 入口網站的佈景主題色彩是白色與黑色。</span><span class="sxs-lookup"><span data-stu-id="843dd-143">The theme colors of the Azure portal are white and black.</span></span> <span data-ttu-id="843dd-144">因此請避免使用這些色彩做為您標誌的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="843dd-144">Hence avoid using these colors as the background color of your logos.</span></span> <span data-ttu-id="843dd-145">請使用會讓您的標誌在 Azure 入口網站顯得突出的某些色彩。</span><span class="sxs-lookup"><span data-stu-id="843dd-145">Use some color that would make your logos prominent in the Azure portal.</span></span> <span data-ttu-id="843dd-146">建議您使用簡單的主要色彩。</span><span class="sxs-lookup"><span data-stu-id="843dd-146">We recommend simple primary colors.</span></span> <span data-ttu-id="843dd-147">如果您使用透明背景，請確定標誌/文字不是白色或黑色。</span><span class="sxs-lookup"><span data-stu-id="843dd-147">If you are using transparent background, then make sure that the logo/text is not white or black.</span></span>
* <span data-ttu-id="843dd-148">請不要在標誌上使用漸層背景。</span><span class="sxs-lookup"><span data-stu-id="843dd-148">Do not use a gradient background on the logo.</span></span>
* <span data-ttu-id="843dd-149">避免在標誌上放置文字 (甚至是公司或品牌名稱)。</span><span class="sxs-lookup"><span data-stu-id="843dd-149">Avoid placing text, even your company or brand name, on the logo.</span></span>
* <span data-ttu-id="843dd-150">您標誌的外觀與風格應該是「一般」，而且應該避免漸層。</span><span class="sxs-lookup"><span data-stu-id="843dd-150">The look and feel of your logo should be 'flat' and should avoid gradients.</span></span>
* <span data-ttu-id="843dd-151">標誌不應該自動進行縮放。</span><span class="sxs-lookup"><span data-stu-id="843dd-151">The logo should not be stretched.</span></span>

<span data-ttu-id="843dd-152">**主圖標誌的其他指導方針：**</span><span class="sxs-lookup"><span data-stu-id="843dd-152">**Additional guidelines for the Hero logo:**</span></span>

* <span data-ttu-id="843dd-153">主圖標誌為選用項。</span><span class="sxs-lookup"><span data-stu-id="843dd-153">The Hero logo is optional.</span></span> <span data-ttu-id="843dd-154">發行者可以選擇不上傳主圖標誌。</span><span class="sxs-lookup"><span data-stu-id="843dd-154">The publisher can choose not to upload a Hero logo.</span></span> <span data-ttu-id="843dd-155">**但主圖圖示一旦上傳，即無法從發佈入口網站中刪除。屆時合作夥伴必須遵循主圖圖示的 Azure Marketplace 指導方針，否則供應項目將無法核准進入生產環境。**</span><span class="sxs-lookup"><span data-stu-id="843dd-155">**However once uploaded the hero icon cannot be deleted from the Publishing portal. At that time, the partner must follow the Azure Marketplace guidelines for Hero icons else the offer will not be approved to production.**</span></span>
* <span data-ttu-id="843dd-156">發行者顯示名稱、SKU 標題和供應項目完整細摘要會以白色字型色彩顯示。</span><span class="sxs-lookup"><span data-stu-id="843dd-156">The Publisher Display Name, SKU title and the offer long summary are displayed in white font color.</span></span> <span data-ttu-id="843dd-157">因此，您應避免在主圖圖示的背景使用淺色系。</span><span class="sxs-lookup"><span data-stu-id="843dd-157">Hence you should avoid keeping any light color in the background of the Hero Icon.</span></span> <span data-ttu-id="843dd-158">主圖圖示不允許使用黑色、白色和透明背景。</span><span class="sxs-lookup"><span data-stu-id="843dd-158">Black, white and transparent background is not allowed for Hero icons.</span></span>
* <span data-ttu-id="843dd-159">供應項目列出之後，會以程式設計方式將發行者顯示名稱、SKU 標題、供應項目完整摘要和 [建立] 按鈕內嵌在主圖標誌內。</span><span class="sxs-lookup"><span data-stu-id="843dd-159">The publisher display name, SKU title, the offer long summary and the create button are embedded programmatically inside the Hero logo once the offer goes listed.</span></span> <span data-ttu-id="843dd-160">因此您在設計主圖標誌時不應輸入任何文字。</span><span class="sxs-lookup"><span data-stu-id="843dd-160">So you should not enter any text while you are designing the Hero logo.</span></span> <span data-ttu-id="843dd-161">您只需在右邊留下空白空間，因為我們會以程式設計方式於該處內嵌文字 (也就是</span><span class="sxs-lookup"><span data-stu-id="843dd-161">Just leave empty space on the right because the text (i.e.</span></span> <span data-ttu-id="843dd-162">發行者顯示名稱、SKU 標題、供應項目完整摘要)。</span><span class="sxs-lookup"><span data-stu-id="843dd-162">publisher display name, SKU title, the offer long summary) will be included programmatically by us over there.</span></span> <span data-ttu-id="843dd-163">文字右側的空白空間應為 415 x 100 (從左邊開始位移 370px)。</span><span class="sxs-lookup"><span data-stu-id="843dd-163">The empty space for the text should be 415x100 on the right (and it is offset by 370px from the left).</span></span>

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a><span data-ttu-id="843dd-164">適用於已列出的虛擬機器供應項目的其他生產環境檢查清單</span><span class="sxs-lookup"><span data-stu-id="843dd-164">Additional production checklist for already listed Virtual Machine offers</span></span>
* <span data-ttu-id="843dd-165">請檢查是否已經有任何供應項目包含您公司所提供的同一供應項目。</span><span class="sxs-lookup"><span data-stu-id="843dd-165">Check if there is already an offer with the same offer name from your company.</span></span> <span data-ttu-id="843dd-166">如果有，您應在現有的供應項目加入新版 SKU，而不是新建重複的供應項目。</span><span class="sxs-lookup"><span data-stu-id="843dd-166">If yes, then you should add a new version of the SKU in the existing offer instead of creating a new duplicate offer.</span></span>
* <span data-ttu-id="843dd-167">請勿變更同一個 SKU 的兩個版本之間的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="843dd-167">Data disk should not change between two versions of the same SKU.</span></span>
* <span data-ttu-id="843dd-168">Azure Marketplace 不支援變更已列出 SKU 的價格，因為它會影響現有客戶的帳單。</span><span class="sxs-lookup"><span data-stu-id="843dd-168">The Azure Marketplace does not support pricing change of the listed SKUS as it impacts the billing of the existing customers.</span></span> <span data-ttu-id="843dd-169">請務必不要變更 SKU 公開發行區域已列出的 SKU 價格。</span><span class="sxs-lookup"><span data-stu-id="843dd-169">Ensure that you do not change the pricing of the listed SKUs in the regions where the SKU is available.</span></span> <span data-ttu-id="843dd-170">但是您可以在現有的 SKU 中加入新的 SKU 或新區域。</span><span class="sxs-lookup"><span data-stu-id="843dd-170">However, you can add new SKUs or add new regions to an existing SKU.</span></span>

## <a name="next-steps"></a><span data-ttu-id="843dd-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="843dd-171">Next steps</span></span>
<span data-ttu-id="843dd-172">一旦供應項目上線，請測試客戶案例，如同在預備環境中進行測試和驗證一樣，驗證在生產環境中的所有合約和功能都運作正常。</span><span class="sxs-lookup"><span data-stu-id="843dd-172">Once the offer goes live, test the customer scenarios to validate that all the contracts and functionality work properly in the production environment as tested and validated in the staging environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="843dd-173">另請參閱</span><span class="sxs-lookup"><span data-stu-id="843dd-173">See also</span></span>
* [<span data-ttu-id="843dd-174">使用者入門：如何將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="843dd-174">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
