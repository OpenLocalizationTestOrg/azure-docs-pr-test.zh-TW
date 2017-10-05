---
title: "管理 Azure Marketplace 上的虛擬機器映像 | Microsoft Docs"
description: "如何在初始發佈後管理 Azure Marketplace 上的虛擬機器映像的詳細指南"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: e1f90650e71345957c2d353774cb8bef62c1868b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-the-azure-marketplace"></a><span data-ttu-id="a915e-103">關於 Azure Marketplace 中的虛擬機器優惠的後期製作指南</span><span class="sxs-lookup"><span data-stu-id="a915e-103">Post-production guide for virtual machine offers in the Azure Marketplace</span></span>
<span data-ttu-id="a915e-104">本文說明如何更新 Azure Marketplace 中已上線的虛擬機器供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-104">This article explains how you can update a live virtual machine offer in the Azure Marketplace.</span></span> <span data-ttu-id="a915e-105">它會引導您進行將一或多個新 SKU 新增至現有供應項目的程序。</span><span class="sxs-lookup"><span data-stu-id="a915e-105">It guides you through the process of adding one or more new SKUs to an existing offer.</span></span> <span data-ttu-id="a915e-106">同時引導您進行從 Marketplace 移除上線虛擬機器供應項目或 SKU 的程序。</span><span class="sxs-lookup"><span data-stu-id="a915e-106">It also guides you through the process of removing a live virtual machine offer or SKU from the Marketplace.</span></span>

<span data-ttu-id="a915e-107">供應項目/SKU 在 [Azure 入口網站](http://portal.azure.com)預備完成後，您就無法變更下列文字方塊：</span><span class="sxs-lookup"><span data-stu-id="a915e-107">After an offer/SKU is staged in the [Azure portal](http://portal.azure.com), you can't change the following text boxes:</span></span>

* <span data-ttu-id="a915e-108">**供應項目識別碼**︰在發佈入口網站中，移至 [虛擬機器] 並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-108">**Offer Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="a915e-109">然後按一下 [VM 映像] > [供應項目識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a915e-109">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="a915e-110">**SKU 識別碼**︰在發佈入口網站中，移至 [虛擬機器] 並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-110">**SKU Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="a915e-111">然後按一下 [SKU] > [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="a915e-111">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="a915e-112">**發行者命名空間**︰在發佈入口網站中，移至 **[虛擬機器]** > **[逐步解說]** > **[告知我們您的公司]** (請見「步驟 2：註冊您的公司」) > **[發行者命名空間]** > **[命名空間** ]。</span><span class="sxs-lookup"><span data-stu-id="a915e-112">**Publisher Namespace**: In the Publishing portal, go to **virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under “Step 2 Register Your Company”) > **Publisher Namespace** > **Namespace**.</span></span>

<span data-ttu-id="a915e-113">供應項目/SKU 列在 [Marketplace](http://azure.microsoft.com/marketplace) 後，您就無法變更下列文字方塊：</span><span class="sxs-lookup"><span data-stu-id="a915e-113">After the offer/SKU is listed in the [Marketplace](http://azure.microsoft.com/marketplace), you can't change the following text boxes:</span></span>

* <span data-ttu-id="a915e-114">**供應項目識別碼**︰在發佈入口網站中，移至 [虛擬機器] 並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-114">**Offer Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="a915e-115">然後按一下 [VM 映像] > [供應項目識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a915e-115">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="a915e-116">**SKU 識別碼**︰在發佈入口網站中，移至 [虛擬機器] 並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-116">**SKU Identifier**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="a915e-117">然後按一下 [SKU] > [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="a915e-117">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="a915e-118">**發行者命名空間**︰在發佈入口網站中，移至 **[虛擬機器]** > **[逐步解說]** > **[告知我們您的公司]** (請見「步驟 2 註冊」) > **[發行者命名空間]** > **[命名空間]** 。</span><span class="sxs-lookup"><span data-stu-id="a915e-118">**Publisher Namespace**: In the Publishing portal, go to **virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under "Step 2 Register") **Publisher Namespace** > **Namespace**.</span></span>
* <span data-ttu-id="a915e-119">**連接埠**︰在發佈入口網站中，移至 [虛擬機器] 並選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-119">**Ports**: In the Publishing portal, go to **virtual machines** and select your offer.</span></span> <span data-ttu-id="a915e-120">然後按一下 [VM 映像] > [開啟連接埠]。</span><span class="sxs-lookup"><span data-stu-id="a915e-120">Then click **VM IMAGES** > **Open Ports**.</span></span>
* <span data-ttu-id="a915e-121">**已列出 SKU 的價格變更**</span><span class="sxs-lookup"><span data-stu-id="a915e-121">**Pricing change of listed SKU(s)**</span></span>
* <span data-ttu-id="a915e-122">**已列出 SKU 的計費模式變更**</span><span class="sxs-lookup"><span data-stu-id="a915e-122">**Billing model change of listed SKU(s)**</span></span>
* <span data-ttu-id="a915e-123">**移除已列出 SKU 的計費區域**</span><span class="sxs-lookup"><span data-stu-id="a915e-123">**Removal of billing regions of listed SKU(s)**</span></span>
* <span data-ttu-id="a915e-124">**變更已列出 SKU 的資料磁碟計數**</span><span class="sxs-lookup"><span data-stu-id="a915e-124">**Changing the data disk count of listed SKU(s)**</span></span>

## <a name="update-the-technical-details-of-a-sku"></a><span data-ttu-id="a915e-125">更新 SKU 的技術詳細資料</span><span class="sxs-lookup"><span data-stu-id="a915e-125">Update the technical details of a SKU</span></span>
<span data-ttu-id="a915e-126">若要將新版本新增到已列出的 SKU，然後重新發佈供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-126">To add a new version to the listed SKU and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-127">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-127">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-128">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-128">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-129">在左側功能表中，按一下 [VM 映像] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-129">In the menu on the left, click the **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="a915e-130">在 [SKU] 區段中，找出您想要更新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-130">In the **SKUs** section, locate the SKU that you want to update.</span></span>
5. <span data-ttu-id="a915e-131">新增新的 SKU 版本號碼，然後按一下 **+** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-131">Add a new version number for the SKU, and click the **+** button.</span></span> <span data-ttu-id="a915e-132">新版本應該是 X.Y.Z 格式，其中 X、Y 和 Z 是整數。</span><span class="sxs-lookup"><span data-stu-id="a915e-132">The new version should be in an X.Y.Z format, where X, Y, and Z are integers.</span></span> <span data-ttu-id="a915e-133">只能以累加方式變更版本。</span><span class="sxs-lookup"><span data-stu-id="a915e-133">Version changes should only be incremental.</span></span>
6. <span data-ttu-id="a915e-134">在 [OS VHD URL]  方塊中，輸入針對作業系統 VHD 所建立的共用存取簽章 URI，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-134">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD and save the changes.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a915e-135">您不能增加/減少已列出的 SKU 的資料磁碟計數。</span><span class="sxs-lookup"><span data-stu-id="a915e-135">You can't increment/decrement the data disk count of a listed SKU.</span></span> <span data-ttu-id="a915e-136">在此案例中，您需要建立新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-136">You need to create a new SKU in this case.</span></span> <span data-ttu-id="a915e-137">如需詳細指引，請參閱[在已列出的供應項目下新增 SKU](#add-a-new-sku-under-a-listed-offer)一節。</span><span class="sxs-lookup"><span data-stu-id="a915e-137">For detailed guidance, refer to the section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>
   >
   >
7. <span data-ttu-id="a915e-138">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-138">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-139">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-139">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="a915e-140">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-140">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-141">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-141">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![VM 映像](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-the-nontechnical-details-of-an-offer-or-a-sku"></a><span data-ttu-id="a915e-143">更新供應項目或 SKU 的技術性詳細資料</span><span class="sxs-lookup"><span data-stu-id="a915e-143">Update the nontechnical details of an offer or a SKU</span></span>
<span data-ttu-id="a915e-144">您可以更新 Marketplace 中已上線的供應項目或 SKU 的非技術性 (行銷、法律、支援、類別) 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a915e-144">You can update the nontechnical (marketing, legal, support, categories) details of your live offer or SKU in the Marketplace.</span></span>

### <a name="update-the-offer-description-and-logos"></a><span data-ttu-id="a915e-145">更新供應項目描述和標誌</span><span class="sxs-lookup"><span data-stu-id="a915e-145">Update the offer description and logos</span></span>
<span data-ttu-id="a915e-146">若要更新供應項目詳細資訊並重新發佈您的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-146">To update the offer details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-147">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-147">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-148">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-148">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-149">在左側功能表中，按一下 [行銷] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-149">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="a915e-150">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="a915e-150">Click **English (US)**.</span></span>
5. <span data-ttu-id="a915e-151">按一下 [詳細資料] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-151">Click the **DETAILS** tab.</span></span> <span data-ttu-id="a915e-152">在 [描述] 區段中，更新供應項目的 [標題]、[摘要] 和 [完整摘要]，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-152">In the **Description** section, update the offer **TITLE**, **SUMMARY**, and **LONG SUMMARY** and save the changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-153">當您更新 SKU 詳細資料時，請注意下列限制︰</span><span class="sxs-lookup"><span data-stu-id="a915e-153">When you update the SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="a915e-154">請不要對供應項目描述和 SKU 描述輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="a915e-154">Do not enter duplicate text for the offer description and the SKU description.</span></span>
   * <span data-ttu-id="a915e-155">請不要對 SKU 標題和供應項目完整摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="a915e-155">Do not enter duplicate text for the SKU title and the offer long summary.</span></span> 
   * <span data-ttu-id="a915e-156">請不要對 SKU 標題和供應項目摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="a915e-156">Do not enter duplicate text for the SKU title and the offer summary.</span></span>
   >
   >

    ![詳細資料](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. <span data-ttu-id="a915e-158">在 [詳細資料] 索引標籤的 [標誌] 區段中，更新標誌。</span><span class="sxs-lookup"><span data-stu-id="a915e-158">In the **LOGOS** section of the **DETAILS** tab, update the logos.</span></span> <span data-ttu-id="a915e-159">請確定標誌遵循 [Azure Marketplace 指導方針](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。</span><span class="sxs-lookup"><span data-stu-id="a915e-159">Ensure that the logos follow the [Azure Marketplace guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-160">主圖圖示是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="a915e-160">A hero icon is optional.</span></span> <span data-ttu-id="a915e-161">您可以選擇不上傳主圖圖示。</span><span class="sxs-lookup"><span data-stu-id="a915e-161">You can choose not to upload a hero icon.</span></span> <span data-ttu-id="a915e-162">然而，上傳主圖圖示後，就無法從發佈入口網站中刪除。</span><span class="sxs-lookup"><span data-stu-id="a915e-162">However, after a hero icon is uploaded, there is no provision to delete it from the Publishing portal.</span></span> <span data-ttu-id="a915e-163">請遵循[主圖圖示指導方針](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。</span><span class="sxs-lookup"><span data-stu-id="a915e-163">Follow the [hero icon guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
   >
   >
7. <span data-ttu-id="a915e-164">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-164">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-165">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-165">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="a915e-166">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-166">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-167">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-167">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![標誌](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-the-sku-description"></a><span data-ttu-id="a915e-169">更新 SKU 描述</span><span class="sxs-lookup"><span data-stu-id="a915e-169">Update the SKU description</span></span>
<span data-ttu-id="a915e-170">若要更新 SKU 詳細資訊並重新發佈您的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-170">To update the SKU details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-171">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-171">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-172">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-172">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-173">在左側功能表中，按一下 [行銷] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-173">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="a915e-174">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="a915e-174">Click **English (US)**.</span></span>
5. <span data-ttu-id="a915e-175">按一下 [方案] 。</span><span class="sxs-lookup"><span data-stu-id="a915e-175">Click the **PLANS** tab.</span></span> <span data-ttu-id="a915e-176">在 [SKU] 區段中，更新 SKU 的 [標題]、[摘要] 和 [描述]，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-176">In the **SKUs** section, update the SKU **TITLE**, **SUMMARY**, and **DESCRIPTION** and save the changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-177">當您更新 SKU 詳細資料時，請注意下列限制︰</span><span class="sxs-lookup"><span data-stu-id="a915e-177">When you update the SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="a915e-178">請不要對供應項目描述和 SKU 描述輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="a915e-178">Do not enter duplicate text for the offer description and the SKU description.</span></span> 
   * <span data-ttu-id="a915e-179">請不要對 SKU 標題和供應項目完整摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="a915e-179">Do not enter duplicate text for the SKU title and the offer long summary.</span></span> 
   * <span data-ttu-id="a915e-180">請不要對 SKU 標題和供應項目摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="a915e-180">Do not enter duplicate text for the SKU title and the offer summary.</span></span>
   >
   >
6. <span data-ttu-id="a915e-181">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-181">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-182">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-182">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="a915e-183">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-183">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-184">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-184">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![方案](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a><span data-ttu-id="a915e-186">變更現有連結或新增連結</span><span class="sxs-lookup"><span data-stu-id="a915e-186">Change existing links or add new links</span></span>
<span data-ttu-id="a915e-187">若要變更現有連結或新增連結，然後重新發佈您的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-187">To change existing links or add new links and then republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-188">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-188">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-189">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-189">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-190">在左側功能表中，按一下 [行銷] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-190">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="a915e-191">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="a915e-191">Click **English (US)**.</span></span>
5. <span data-ttu-id="a915e-192">按一下 [連結] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-192">Click the **LINKS** tab.</span></span>
6. <span data-ttu-id="a915e-193">若要新增連結，請在 [連結] 區段中，按一下 [+ 新增連結]。</span><span class="sxs-lookup"><span data-stu-id="a915e-193">To add a new link, in the **Links** section, click **+ ADD LINK**.</span></span> <span data-ttu-id="a915e-194">在 [新增連結] 對話方塊中，輸入連結的 [標題] 和 [URL]，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-194">In the **Add Link** dialog box, enter the link **TITLE** and **URL** and save the changes.</span></span> <span data-ttu-id="a915e-195">您可以輸入任何包含資訊來協助客戶的連結。</span><span class="sxs-lookup"><span data-stu-id="a915e-195">You can enter any link that contains information that might help customers.</span></span>
7. <span data-ttu-id="a915e-196">若要更新或刪除現有的連結，請選取連結，然後按一下 [編輯] 按鈕或 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-196">To update or delete an existing link, select the link and click the **Edit** button or the **Delete** button.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-197">確保您在此區段中輸入的連結可正常運作，因為在生產環境要求處理期間會驗證這些連結。</span><span class="sxs-lookup"><span data-stu-id="a915e-197">Ensure that the links that you've entered in this section are working properly, because these links get validated during your production request process.</span></span>
   >
   >
8. <span data-ttu-id="a915e-198">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-198">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-199">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-199">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="a915e-200">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-200">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-201">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-201">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![連結](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![新增連結](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a><span data-ttu-id="a915e-204">變更現有範例映像或新增範例映像</span><span class="sxs-lookup"><span data-stu-id="a915e-204">Change an existing sample image or add a new sample image</span></span>
<span data-ttu-id="a915e-205">若要變更現有範例映像或新增範例映像，然後重新發佈您的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-205">To change an existing sample image or add new sample images and then republish your offer, follow these steps:</span></span>

> [!NOTE]
> <span data-ttu-id="a915e-206">只有一個範例映像會顯示在 [Azure 入口網站](https://portal.azure.com)中。</span><span class="sxs-lookup"><span data-stu-id="a915e-206">Only one sample image is displayed in the [Azure portal](https://portal.azure.com).</span></span>
>
>

1. <span data-ttu-id="a915e-207">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-207">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-208">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-208">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-209">在左側功能表中，按一下 [行銷] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-209">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="a915e-210">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="a915e-210">Click **English (US)**.</span></span>
5. <span data-ttu-id="a915e-211">按一下 [範例映像] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-211">Click the **SAMPLE IMAGES** tab.</span></span>
6. <span data-ttu-id="a915e-212">若要新增範例映像，請在 [範例映像] 區段中，按一下 [上傳新映像] ，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-212">To add a new sample image, in the **Sample Images** section, click **UPLOAD A NEW IMAGE** and save the changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-213">包含範例映像是選擇性作業。</span><span class="sxs-lookup"><span data-stu-id="a915e-213">Including a sample image is optional.</span></span>
   >
7. <span data-ttu-id="a915e-214">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-214">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-215">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-215">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="a915e-216">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-216">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-217">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-217">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![範例映像](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-the-legal-content"></a><span data-ttu-id="a915e-219">更新法律聲明內容</span><span class="sxs-lookup"><span data-stu-id="a915e-219">Update the legal content</span></span>
<span data-ttu-id="a915e-220">若要更新法律聲明內容並重新發佈您的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-220">To update the legal content and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-221">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-221">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-222">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-222">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-223">在左側功能表中，按一下 [行銷] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-223">In the menu on the left, click the **MARKETING** tab.</span></span>
4. <span data-ttu-id="a915e-224">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="a915e-224">Click **English (US)**.</span></span>
5. <span data-ttu-id="a915e-225">按一下 [法律聲明] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-225">Click the **LEGAL** tab.</span></span> <span data-ttu-id="a915e-226">在 [法律聲明] 索引標籤中，更新使用原則/條款。</span><span class="sxs-lookup"><span data-stu-id="a915e-226">In the **Legal** section, update your policies/terms of use.</span></span> <span data-ttu-id="a915e-227">在 [使用條款] 方塊中輸入或貼上原則/條款，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-227">Enter or paste the policies/terms in the **TERMS OF USE** box and save the changes.</span></span>
6. <span data-ttu-id="a915e-228">法律使用條款的字元限制為 1 百萬個字元。</span><span class="sxs-lookup"><span data-stu-id="a915e-228">The character limit for the legal terms of use is 1 million characters.</span></span>
7. <span data-ttu-id="a915e-229">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-229">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-230">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-230">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="a915e-231">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-231">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-232">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-232">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![法律](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-the-support-information"></a><span data-ttu-id="a915e-234">更新支援資訊</span><span class="sxs-lookup"><span data-stu-id="a915e-234">Update the support information</span></span>
<span data-ttu-id="a915e-235">若要更新支援資訊並重新發佈您的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-235">To update the support information and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-236">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-236">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-237">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-237">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-238">在左側功能表中，按一下 [支援] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-238">In the menu on the left, click the **SUPPORT** tab.</span></span>
4. <span data-ttu-id="a915e-239">在 [工程連絡人] 區段中，更新工程連絡人詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a915e-239">In the **Engineering Contact** section, update the engineering contact details.</span></span> <span data-ttu-id="a915e-240">這些詳細資料僅用於合作夥伴與 Microsoft 之間的內部通訊。</span><span class="sxs-lookup"><span data-stu-id="a915e-240">These details are used for internal communication between the partner and Microsoft only.</span></span>
5. <span data-ttu-id="a915e-241">在 [客戶支援] 區段中，更新支援連絡人詳細資料和 [支援 URL]。</span><span class="sxs-lookup"><span data-stu-id="a915e-241">In the **Customer Support** section, update the support contact details and the **SUPPORT URL**.</span></span> <span data-ttu-id="a915e-242">這些詳細資料僅用於合作夥伴與 Microsoft 之間的內部通訊。</span><span class="sxs-lookup"><span data-stu-id="a915e-242">These details are used for internal communication between the partner and Microsoft only.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-243">如果您只想要提供電子郵件支援，請在 [客戶支援] 區段中輸入虛設的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="a915e-243">If you want to provide only email support, enter a dummy phone number in the **Customer Support** section.</span></span> <span data-ttu-id="a915e-244">在此情況下，會改用您提供的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a915e-244">In this case, the email you provided is used instead.</span></span>
   >
   >
6. <span data-ttu-id="a915e-245">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-245">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-246">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-246">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="a915e-247">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-247">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-248">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-248">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![支援](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-the-categories"></a><span data-ttu-id="a915e-250">更新類別</span><span class="sxs-lookup"><span data-stu-id="a915e-250">Update the categories</span></span>
<span data-ttu-id="a915e-251">若要更新供應項目的類別區段，然後重新發佈供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-251">To update the categories section for your offer and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-252">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-252">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-253">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-253">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-254">在左側功能表中，按一下 [類別] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-254">In the menu on the left, click the **CATEGORIES** tab.</span></span>
4. <span data-ttu-id="a915e-255">在 [類別]  區段中，更新供應項目的類別，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a915e-255">In the **Categories** section, update the categories for your offer and save the changes.</span></span> <span data-ttu-id="a915e-256">您最多可以為 Azure Marketplace 資源庫選擇五個類別。</span><span class="sxs-lookup"><span data-stu-id="a915e-256">You can choose up to five categories for the Azure Marketplace gallery.</span></span>
5. <span data-ttu-id="a915e-257">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-257">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-258">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-258">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
6. <span data-ttu-id="a915e-259">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-259">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-260">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-260">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![類別](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a><span data-ttu-id="a915e-262">在已列出的供應項目下新增 SKU</span><span class="sxs-lookup"><span data-stu-id="a915e-262">Add a new SKU under a listed offer</span></span>
<span data-ttu-id="a915e-263">若要在上線的供應項目中新增 SKU，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-263">To add a new SKU in your live offer, follow these steps:</span></span>

1. <span data-ttu-id="a915e-264">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-264">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-265">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-265">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-266">在左側功能表中，按一下 [SKU] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-266">In the menu on the left, click the **SKUS** tab.</span></span> <span data-ttu-id="a915e-267">然後按一下 [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="a915e-267">Then click **Add a SKU**.</span></span> 
4. <span data-ttu-id="a915e-268">在對話方塊中，輸入小寫的 [SKU 識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a915e-268">In the dialog box, enter a **SKU Identifier** in lowercase.</span></span> <span data-ttu-id="a915e-269">如果您想要以 BYOL 計費模式發佈新的 SKU，請選取 [自備授權 (BYOL) 計費模式] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a915e-269">Select the **Bring your own license (BYOL) billing model** check box if you want to publish the new SKU with a BYOL billing model.</span></span> <span data-ttu-id="a915e-270">否則，清除此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a915e-270">Otherwise, clear the check box.</span></span> <span data-ttu-id="a915e-271">按一下核取記號以建立新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-271">Click the tick mark to create a new SKU.</span></span> <span data-ttu-id="a915e-272">如果您並未選取 BYOL 計費模式，則計費模式會自動設為「每小時」。</span><span class="sxs-lookup"><span data-stu-id="a915e-272">If you didn't choose the BYOL billing model, the billing model is automatically set to hourly.</span></span> <span data-ttu-id="a915e-273">如果您想要「每小時」計費模式的 30 天免費試用，請選取 [有免費試用可用嗎?] 的 [一個月]。</span><span class="sxs-lookup"><span data-stu-id="a915e-273">If you want the 30-day free trial for the hourly billing model, select **One Month** for **Is a free trial available?**</span></span> <span data-ttu-id="a915e-274">否則，請選取 [無試用]。</span><span class="sxs-lookup"><span data-stu-id="a915e-274">Otherwise, select **No Trial**.</span></span> <span data-ttu-id="a915e-275">(只有在建立新的 SKU 時尚未選取 BYOL，[有免費試用可用嗎?] 才會出現。)</span><span class="sxs-lookup"><span data-stu-id="a915e-275">(**Is a free trial available?** appears only if you haven't selected BYOL while creating the new SKU.)</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a915e-276">「只有」當您獲准發佈方案範本時，[從 Marketplace 隱藏此 SKU，因為應該永遠透過方案範本購買它] 才會為 [是]。</span><span class="sxs-lookup"><span data-stu-id="a915e-276">**Hide this SKU from the Marketplace because it should always be bought via a solution template** should be **Yes** *only* if you're approved for publishing a solution template.</span></span> <span data-ttu-id="a915e-277">否則，這個選項應該永遠都是 [否]。</span><span class="sxs-lookup"><span data-stu-id="a915e-277">Otherwise, this option should always be **No**.</span></span>
   >
   >
4. <span data-ttu-id="a915e-278">在左側功能表中，按一下 [VM 映像] 索引標籤並找出您已建立的新 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-278">In the menu on the left, click the **VM IMAGES** tab and find out the new SKU that you've created.</span></span>
5. <span data-ttu-id="a915e-279">若要設定新的 SKU，請參閱[取得 VM 映像的憑證](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image)中的指引。</span><span class="sxs-lookup"><span data-stu-id="a915e-279">To set up the new SKU, see [Obtain certification for your VM image](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) for guidance.</span></span>
6. <span data-ttu-id="a915e-280">若要為新的 SKU 新增行銷資料，請參閱[提供 Marketplace 行銷內容](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。</span><span class="sxs-lookup"><span data-stu-id="a915e-280">To add marketing material for the new SKU, see [Provide Marketplace marketing content](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
7. <span data-ttu-id="a915e-281">若要為新的 SKU 新增價格資訊，請參閱[設定價格](marketplace-publishing-push-to-staging.md#step-2-set-your-prices)。</span><span class="sxs-lookup"><span data-stu-id="a915e-281">To add pricing information for the new SKU, see [Set your prices](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).</span></span>
8. <span data-ttu-id="a915e-282">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-282">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-283">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-283">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="a915e-284">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-284">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-285">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-285">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![新增 SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-the-data-disk-count-for-a-listed-sku"></a><span data-ttu-id="a915e-288">變更已列出 SKU 的資料磁碟計數</span><span class="sxs-lookup"><span data-stu-id="a915e-288">Change the data disk count for a listed SKU</span></span>
<span data-ttu-id="a915e-289">您不能增加/減少已列出的 SKU 的資料磁碟計數。</span><span class="sxs-lookup"><span data-stu-id="a915e-289">You can't increment/decrement the data disk count of a listed SKU.</span></span> <span data-ttu-id="a915e-290">在此案例中，您需要建立新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-290">You need to create a new SKU in this case.</span></span> <span data-ttu-id="a915e-291">如需詳細指引，請參閱[在已列出的供應項目下新增 SKU](#add-a-new-sku-under-a-listed-offer)一節。</span><span class="sxs-lookup"><span data-stu-id="a915e-291">For detailed guidance, refer to the section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>

## <a name="delete-a-listed-offer-from-the-marketplace"></a><span data-ttu-id="a915e-292">從 Marketplace 刪除已列出的供應項目</span><span class="sxs-lookup"><span data-stu-id="a915e-292">Delete a listed offer from the Marketplace</span></span>
<span data-ttu-id="a915e-293">要求移除上線供應項目時，需要注意幾個層面。</span><span class="sxs-lookup"><span data-stu-id="a915e-293">Various aspects need to be taken care of in the case of a request to remove a live offer.</span></span> <span data-ttu-id="a915e-294">若要取得支援小組的指引，以從 Marketplace 移除已列出的供應項目，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-294">To get guidance from the support team to remove a listed offer from the Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="a915e-295">在[建立事件](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681)頁面上引發支援票證。</span><span class="sxs-lookup"><span data-stu-id="a915e-295">Raise a support ticket on the [Create an incident](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) page.</span></span>

2. <span data-ttu-id="a915e-296">選取 [管理供應項目] 作為 [問題類型]，然後選取 [修改已在生產中的供應項目和/或 SKU] 作為 [類別]。</span><span class="sxs-lookup"><span data-stu-id="a915e-296">Select **Problem type** as **Managing offers**, and select **Category** as **Modifying an offer and/or SKU already in production**.</span></span>
3. <span data-ttu-id="a915e-297">提交要求。</span><span class="sxs-lookup"><span data-stu-id="a915e-297">Submit the request.</span></span>

<span data-ttu-id="a915e-298">支援小組會引導您完成供應項目/SKU 刪除程序。</span><span class="sxs-lookup"><span data-stu-id="a915e-298">The support team guides you through the offer/SKU deletion process.</span></span>

> [!NOTE]
> <span data-ttu-id="a915e-299">當供應項目的狀態為 [草稿] \(但不是 [預備] 或 [生產]) 時，您可隨時將其刪除。</span><span class="sxs-lookup"><span data-stu-id="a915e-299">You can always delete the offer while it is in Draft status (but not Staging or Production).</span></span> <span data-ttu-id="a915e-300">在 [歷程記錄] 索引標籤上，按一下 [捨棄草稿]。</span><span class="sxs-lookup"><span data-stu-id="a915e-300">On the **HISTORY** tab, click **DISCARD DRAFT**.</span></span>
>
>

## <a name="delete-a-listed-sku-from-the-marketplace"></a><span data-ttu-id="a915e-301">從 Marketplace 刪除已列出的 SKU</span><span class="sxs-lookup"><span data-stu-id="a915e-301">Delete a listed SKU from the Marketplace</span></span>
<span data-ttu-id="a915e-302">若要從 Marketplace 刪除已列出的 SKU，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-302">To delete a listed SKU from the Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="a915e-303">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-303">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="a915e-304">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-304">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-305">在左側窗格中，按一下 [SKU] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-305">In the pane on the left, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="a915e-306">選取您要刪除的 SKU，然後按一下 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-306">Select the SKU that you want to delete, and click the **Delete** button.</span></span>
5. <span data-ttu-id="a915e-307">移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-307">Go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-308">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-308">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish the offer in the Marketplace.</span></span>
6. <span data-ttu-id="a915e-309">在 Marketplace 中重新發佈供應項目之後，會從 Marketplace 和 Azure 入口網站刪除 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-309">After the offer is republished in the Marketplace, the SKU is deleted from the Marketplace and the Azure portal.</span></span>

## <a name="delete-the-current-version-of-a-listed-sku-from-the-marketplace"></a><span data-ttu-id="a915e-310">從 Marketplace 刪除已列出 SKU 的目前版本</span><span class="sxs-lookup"><span data-stu-id="a915e-310">Delete the current version of a listed SKU from the Marketplace</span></span>
<span data-ttu-id="a915e-311">若要從 Marketplace 刪除已列出 SKU 的目前版本，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="a915e-311">To delete the current version of a listed SKU from the Marketplace, follow these steps:</span></span> 

1. <span data-ttu-id="a915e-312">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-312">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="a915e-313">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-313">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-314">在左側功能表中，按一下 [VM 映像] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-314">In the menu on the left, click the **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="a915e-315">選取您要刪除其目前版本的 SKU，然後按一下 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-315">Select the SKU whose current version you want to delete, and click the **Delete** button.</span></span>
5. <span data-ttu-id="a915e-316">移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-316">Go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-317">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-317">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish the offer in the Marketplace.</span></span>
6. <span data-ttu-id="a915e-318">在 Marketplace 中重新發佈供應項目之後，會從 Marketplace 和 Azure 入口網站刪除已列出 SKU 的目前版本。</span><span class="sxs-lookup"><span data-stu-id="a915e-318">After the offer gets republished in the Marketplace, the current version of the listed SKU is deleted from the Marketplace and the Azure portal.</span></span> <span data-ttu-id="a915e-319">SKU 會接著回復為先前的版本。</span><span class="sxs-lookup"><span data-stu-id="a915e-319">The SKU is then rolled back to its previous version.</span></span>

## <a name="revert-the-listing-price-to-production-values"></a><span data-ttu-id="a915e-320">將列出價格還原成生產環境值</span><span class="sxs-lookup"><span data-stu-id="a915e-320">Revert the listing price to production values</span></span>
<span data-ttu-id="a915e-321">若要將列出價格還原成生產環境值，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a915e-321">To revert the listing price to production values, follow these steps:</span></span>

1. <span data-ttu-id="a915e-322">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-322">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="a915e-323">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-323">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-324">在左側功能表中，按一下 [價格] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-324">In the menu on the left, click the **PRICING** tab.</span></span>
4. <span data-ttu-id="a915e-325">選取您想要重設其價格的區域。</span><span class="sxs-lookup"><span data-stu-id="a915e-325">Select a region whose pricing you want to reset.</span></span>

    ![價格區域](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. <span data-ttu-id="a915e-327">對於每小時計費模式的 SKU，請重設所有核心的價格，因為它們處於所選區域的生產環境。</span><span class="sxs-lookup"><span data-stu-id="a915e-327">For SKUs with an hourly billing model, reset the prices for all the cores as they are in production for the selected region.</span></span> <span data-ttu-id="a915e-328">對於 BYOL 計費模式的 SKU，請在 [外部授權的 (BYOL) SKU 可用性] 區段中核取該 SKU 的核取方塊，以在該區域提供 SKU。</span><span class="sxs-lookup"><span data-stu-id="a915e-328">For SKUs with a BYOL billing model, make the SKU available in the region by selecting the check box for the SKU in the **EXTERNALLY-LICENSED (BYOL) SKU AVAILABILITY** section.</span></span>

    ![定價模式](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. <span data-ttu-id="a915e-330">按一下 [依據美國價格自動訂定其他市場價格] 。</span><span class="sxs-lookup"><span data-stu-id="a915e-330">Click **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a915e-331">視選取的區域而定，按鈕的標籤可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="a915e-331">The button’s label might be different depending on the region that you select.</span></span> <span data-ttu-id="a915e-332">因為我們選取了美國，所以此按鈕會標示為 [依據美國價格自動訂定其他市場價格]。</span><span class="sxs-lookup"><span data-stu-id="a915e-332">Because we selected United States, the button is labeled **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>
   >
   >

    ![自動定價](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. <span data-ttu-id="a915e-334">在自動定價精靈的第 1 頁，選擇基底市場並按一下**箭號**按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-334">On page 1 of the Autoprice wizard, choose the base market and click the **arrow** button.</span></span>

    ![基底市場](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. <span data-ttu-id="a915e-336">在第 2 頁，選擇服務方案和計量 (核心)，然後按一下**箭號**按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-336">On page 2, choose service plans and meters (cores), and click the **arrow** button.</span></span>

    ![服務方案和計量](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. <span data-ttu-id="a915e-338">在第 3 頁，按一下 [全部切換] 以選取所有區域。</span><span class="sxs-lookup"><span data-stu-id="a915e-338">On page 3, click **Toggle All** to select all regions.</span></span> <span data-ttu-id="a915e-339">或者，您可以手動選取特定區域的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a915e-339">Or you can manually select check boxes for specific regions.</span></span> <span data-ttu-id="a915e-340">按一下**箭號**按鈕。</span><span class="sxs-lookup"><span data-stu-id="a915e-340">Click the **arrow** button.</span></span>

    ![選擇市場](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. <span data-ttu-id="a915e-342">在第 4 頁，檢閱匯率，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="a915e-342">On page 4, review the exchange rates and click **Finish**.</span></span> <span data-ttu-id="a915e-343">精靈會根據您的選擇重設價格。</span><span class="sxs-lookup"><span data-stu-id="a915e-343">The wizard resets the pricing according to your selections.</span></span>

11. <span data-ttu-id="a915e-344">在 [價格] 索引標籤上，按一下 [檢視摘要和變更]。</span><span class="sxs-lookup"><span data-stu-id="a915e-344">On the **PRICING** tab, click **VIEW SUMMARY AND CHANGES**.</span></span>
    <span data-ttu-id="a915e-345">對於 [檢視版本]，選取 [草稿]，以及針對 [比較項目]，選取 [生產]。</span><span class="sxs-lookup"><span data-stu-id="a915e-345">For **View Version**, select **Draft**, and for **Compare with**, select **Production**.</span></span> <span data-ttu-id="a915e-346">如果看不出價格差異，即表示價格已順利還原成生產環境值。</span><span class="sxs-lookup"><span data-stu-id="a915e-346">If you see no pricing difference, the pricing reverted to the production values successfully.</span></span>

    ![摘要檢視和變更](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. <span data-ttu-id="a915e-348">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-348">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-349">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-349">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
13. <span data-ttu-id="a915e-350">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-350">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-351">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-351">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

## <a name="revert-the-billing-model-to-production-values"></a><span data-ttu-id="a915e-352">將計費模式還原成生產環境值</span><span class="sxs-lookup"><span data-stu-id="a915e-352">Revert the billing model to production values</span></span>
<span data-ttu-id="a915e-353">若要將計費模式還原成生產環境值，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a915e-353">To revert the billing model to production values, follow these steps:</span></span>

1. <span data-ttu-id="a915e-354">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-354">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="a915e-355">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-355">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-356">在左側功能表中，按一下 [SKU] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-356">In the menu on the left, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="a915e-357">按一下 [編輯] 按鈕以還原計費模式。</span><span class="sxs-lookup"><span data-stu-id="a915e-357">Click the **Edit** button to revert the billing model.</span></span> <span data-ttu-id="a915e-358">在開啟的視窗中，選取或清除 [計費與授權於 Azure 外部進行 (亦即自備授權)] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a915e-358">In the window that opens, select or clear the **Billing and licensing is done externally from Azure (aka Bring Your Own License)** check box.</span></span>

    ![編輯計費](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. <span data-ttu-id="a915e-360">請本文「將列出價格還原成生產環境值」中的步驟。</span><span class="sxs-lookup"><span data-stu-id="a915e-360">Follow the steps in "Revert the listing price to production values" in this article.</span></span>
6. <span data-ttu-id="a915e-361">移至 [發佈] 索引標籤，然後按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="a915e-361">Go to the **PUBLISH** tab, and click **PUSH TO STAGING**.</span></span> <span data-ttu-id="a915e-362">如需在預備環境中測試供應項目的詳細指引，請參閱[針對 Marketplace 測試您的 VM 供應項目](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="a915e-362">For detailed guidance on testing your offer in the staging environment, see [Test your VM offer for the Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="a915e-363">在預備環境中測試您的供應項目之後，請移至發佈入口網站中的 [發佈] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-363">After you've tested your offer in staging, go to the **PUBLISH** tab in the Publishing portal.</span></span> <span data-ttu-id="a915e-364">按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-364">Click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

## <a name="revert-the-visibility-setting-of-a-listed-sku-to-the-production-value"></a><span data-ttu-id="a915e-365">將已列出 SKU 的可見性設定還原成生產環境值</span><span class="sxs-lookup"><span data-stu-id="a915e-365">Revert the visibility setting of a listed SKU to the production value</span></span>
<span data-ttu-id="a915e-366">若要將已列出 SKU 的可見性設定還原成生產環境值，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a915e-366">To revert the visibility setting of a listed SKU to the production value, follow these steps:</span></span>

1. <span data-ttu-id="a915e-367">登入[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="a915e-367">Sign in to the [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="a915e-368">移至 [虛擬機器] 索引標籤，然後選取您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-368">Go to the **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="a915e-369">在左側功能表中，按一下 [SKU] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a915e-369">In the menu on the left, click the **SKUS** tab.</span></span>
4. <span data-ttu-id="a915e-370">選取您的 SKU，將 SKU 的可見性設定還原成生產環境值。</span><span class="sxs-lookup"><span data-stu-id="a915e-370">Select your SKU, and revert the visibility setting of the SKU to the production value.</span></span>

    ![可見性](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. <span data-ttu-id="a915e-372">在變更完成後，按一下 [要求核准以推送至生產環境]，以在 Marketplace 中重新發佈您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="a915e-372">After you're done with the changes, click **REQUEST APPROVAL TO PUSH TO PRODUCTION** to republish your offer in the Marketplace.</span></span>

## <a name="see-also"></a><span data-ttu-id="a915e-373">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a915e-373">See also</span></span>
* [<span data-ttu-id="a915e-374">使用者入門：將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a915e-374">Get Started: Publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="a915e-375">了解付款報告</span><span class="sxs-lookup"><span data-stu-id="a915e-375">Understand payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="a915e-376">變更雲端解決方案提供者轉售商獎勵</span><span class="sxs-lookup"><span data-stu-id="a915e-376">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="a915e-377">針對 Marketplace 中常見的發佈問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a915e-377">Troubleshoot common publishing problems in the Marketplace</span></span>](marketplace-publishing-support-common-issues.md)
* [<span data-ttu-id="a915e-378">以發佈者身分取得支援</span><span class="sxs-lookup"><span data-stu-id="a915e-378">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)
* [<span data-ttu-id="a915e-379">建立內部部署 VM 映像</span><span class="sxs-lookup"><span data-stu-id="a915e-379">Create a VM image on-premises</span></span>](marketplace-publishing-vm-image-creation-on-premise.md)
* [<span data-ttu-id="a915e-380">在 Azure Preview 入口網站中建立執行 Windows 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a915e-380">Create a virtual machine running Windows in the Azure preview portal</span></span>](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
