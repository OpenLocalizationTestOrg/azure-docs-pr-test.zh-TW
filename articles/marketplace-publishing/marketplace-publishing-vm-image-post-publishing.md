---
title: "您的虛擬機器映像中 hello Azure Marketplace aaaManaging |Microsoft 文件"
description: "上如何 toomanage 您的虛擬機器映像 hello Azure Marketplace 中之後初始發行集的詳細的指引"
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
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a><span data-ttu-id="3c4c1-103">虛擬機器後製指南所提供的 hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3c4c1-103">Post-production guide for virtual machine offers in hello Azure Marketplace</span></span>
<span data-ttu-id="3c4c1-104">本文說明如何更新 hello Azure Marketplace 中的即時虛擬機器提供項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-104">This article explains how you can update a live virtual machine offer in hello Azure Marketplace.</span></span> <span data-ttu-id="3c4c1-105">它會引導您完成新增一或多個新的 Sku tooan 現有的優惠的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-105">It guides you through hello process of adding one or more new SKUs tooan existing offer.</span></span> <span data-ttu-id="3c4c1-106">它也會引導您 hello 程序的即時虛擬機器提供項目或 SKU 移除 hello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-106">It also guides you through hello process of removing a live virtual machine offer or SKU from hello Marketplace.</span></span>

<span data-ttu-id="3c4c1-107">供應項目/SKU 已經暫置在 hello 之後[Azure 入口網站](http://portal.azure.com)，您無法變更下列文字方塊中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c4c1-107">After an offer/SKU is staged in hello [Azure portal](http://portal.azure.com), you can't change hello following text boxes:</span></span>

* <span data-ttu-id="3c4c1-108">**提供的識別項**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-108">**Offer Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="3c4c1-109">然後按一下 [VM 映像] > [供應項目識別碼]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-109">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="3c4c1-110">**SKU 識別碼**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-110">**SKU Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="3c4c1-111">然後按一下 [SKU] > [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-111">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="3c4c1-112">**發行者命名空間**: hello 在發行入口網站，太移**虛擬機器** > **逐步解說** > **告訴我們有關您公司**（在 「 步驟 2 註冊您公司 」 下找到） >**發行者命名空間** > **命名空間**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-112">**Publisher Namespace**: In hello Publishing portal, go too**virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under “Step 2 Register Your Company”) > **Publisher Namespace** > **Namespace**.</span></span>

<span data-ttu-id="3c4c1-113">Hello 優惠/SKU 會列在 hello 之後[Marketplace](http://azure.microsoft.com/marketplace)，您無法變更下列文字方塊中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c4c1-113">After hello offer/SKU is listed in hello [Marketplace](http://azure.microsoft.com/marketplace), you can't change hello following text boxes:</span></span>

* <span data-ttu-id="3c4c1-114">**提供的識別項**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-114">**Offer Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="3c4c1-115">然後按一下 [VM 映像] > [供應項目識別碼]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-115">Then click **VM IMAGES** > **Offer Identifier**.</span></span>
* <span data-ttu-id="3c4c1-116">**SKU 識別碼**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-116">**SKU Identifier**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="3c4c1-117">然後按一下 [SKU] > [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-117">Then click **SKUS** > **Add a SKU**.</span></span>
* <span data-ttu-id="3c4c1-118">**發行者命名空間**: hello 在發行入口網站，太移**虛擬機器** > **逐步解說** > **告訴我們有關您公司**（找到在 「 步驟 2 註冊 」）**發行者命名空間** > **命名空間**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-118">**Publisher Namespace**: In hello Publishing portal, go too**virtual machines** > **Walkthrough** > **Tell Us About Your Company** (found under "Step 2 Register") **Publisher Namespace** > **Namespace**.</span></span>
* <span data-ttu-id="3c4c1-119">**連接埠**: hello 在發行入口網站，太移**虛擬機器**並選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-119">**Ports**: In hello Publishing portal, go too**virtual machines** and select your offer.</span></span> <span data-ttu-id="3c4c1-120">然後按一下 [VM 映像] > [開啟連接埠]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-120">Then click **VM IMAGES** > **Open Ports**.</span></span>
* <span data-ttu-id="3c4c1-121">**已列出 SKU 的價格變更**</span><span class="sxs-lookup"><span data-stu-id="3c4c1-121">**Pricing change of listed SKU(s)**</span></span>
* <span data-ttu-id="3c4c1-122">**已列出 SKU 的計費模式變更**</span><span class="sxs-lookup"><span data-stu-id="3c4c1-122">**Billing model change of listed SKU(s)**</span></span>
* <span data-ttu-id="3c4c1-123">**移除已列出 SKU 的計費區域**</span><span class="sxs-lookup"><span data-stu-id="3c4c1-123">**Removal of billing regions of listed SKU(s)**</span></span>
* <span data-ttu-id="3c4c1-124">**變更的 hello 資料磁碟計數列出 SKU(s)**</span><span class="sxs-lookup"><span data-stu-id="3c4c1-124">**Changing hello data disk count of listed SKU(s)**</span></span>

## <a name="update-hello-technical-details-of-a-sku"></a><span data-ttu-id="3c4c1-125">更新 hello SKU 的技術詳細資料</span><span class="sxs-lookup"><span data-stu-id="3c4c1-125">Update hello technical details of a SKU</span></span>
<span data-ttu-id="3c4c1-126">新的版本 toohello tooadd 列 SKU 和重新發行您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-126">tooadd a new version toohello listed SKU and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-127">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-127">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-128">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-128">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-129">在左側 hello hello 功能表上，按一下 [hello **VM 映像**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-129">In hello menu on hello left, click hello **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="3c4c1-130">在 hello **Sku**區段中，找出您想 tooupdate SKU hello。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-130">In hello **SKUs** section, locate hello SKU that you want tooupdate.</span></span>
5. <span data-ttu-id="3c4c1-131">加入新的版本號碼的 hello SKU，然後按一下 hello  **+**   按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-131">Add a new version number for hello SKU, and click hello **+** button.</span></span> <span data-ttu-id="3c4c1-132">hello 新的版本應該採用 X.Y.Z 格式，X、 Y 和 Z 都是整數。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-132">hello new version should be in an X.Y.Z format, where X, Y, and Z are integers.</span></span> <span data-ttu-id="3c4c1-133">只能以累加方式變更版本。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-133">Version changes should only be incremental.</span></span>
6. <span data-ttu-id="3c4c1-134">在 hello **OS VHD URL**方塊、 輸入 hello 共用的存取簽章 URI 建立 hello 作業系統 VHD 和儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-134">In hello **OS VHD URL** box, enter hello shared access signature URI created for hello operating system VHD and save hello changes.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3c4c1-135">您無法遞增/遞減 hello 資料磁碟計數列出的 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-135">You can't increment/decrement hello data disk count of a listed SKU.</span></span> <span data-ttu-id="3c4c1-136">在此情況下，您需要 toocreate 新 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-136">You need toocreate a new SKU in this case.</span></span> <span data-ttu-id="3c4c1-137">如需詳細指引，請參閱 toohello 區段[加入列出的供應項目底下的新 SKU](#add-a-new-sku-under-a-listed-offer)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-137">For detailed guidance, refer toohello section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>
   >
   >
7. <span data-ttu-id="3c4c1-138">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-138">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-139">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-139">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="3c4c1-140">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-140">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-141">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-141">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![VM 映像](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a><span data-ttu-id="3c4c1-143">更新優惠或 SKU 的 hello 非技術性的詳細資料</span><span class="sxs-lookup"><span data-stu-id="3c4c1-143">Update hello nontechnical details of an offer or a SKU</span></span>
<span data-ttu-id="3c4c1-144">您可以更新 hello 非技術性 (行銷、 legal 支援類別目錄) 即時優惠或 SKU 的 hello Marketplace 中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-144">You can update hello nontechnical (marketing, legal, support, categories) details of your live offer or SKU in hello Marketplace.</span></span>

### <a name="update-hello-offer-description-and-logos"></a><span data-ttu-id="3c4c1-145">更新 hello 供應項目描述和標誌</span><span class="sxs-lookup"><span data-stu-id="3c4c1-145">Update hello offer description and logos</span></span>
<span data-ttu-id="3c4c1-146">tooupdate hello 優惠詳細資料和重新發行您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-146">tooupdate hello offer details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-147">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-147">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-148">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-148">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-149">在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-149">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="3c4c1-150">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-150">Click **English (US)**.</span></span>
5. <span data-ttu-id="3c4c1-151">按一下 hello**詳細資料** 索引標籤。在 hello**描述**區段中，更新 hello 優惠**標題**，**摘要**，和**長摘要**儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-151">Click hello **DETAILS** tab. In hello **Description** section, update hello offer **TITLE**, **SUMMARY**, and **LONG SUMMARY** and save hello changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-152">當您更新 hello SKU 詳細資料時，請注意這些限制：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-152">When you update hello SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="3c4c1-153">請勿將重複的文字輸入 hello 供應項目描述和 hello SKU 描述。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-153">Do not enter duplicate text for hello offer description and hello SKU description.</span></span>
   * <span data-ttu-id="3c4c1-154">請勿 hello SKU 標題和 hello 供應項目完整摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-154">Do not enter duplicate text for hello SKU title and hello offer long summary.</span></span> 
   * <span data-ttu-id="3c4c1-155">請勿為 hello SKU 標題和 hello 供給摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-155">Do not enter duplicate text for hello SKU title and hello offer summary.</span></span>
   >
   >

    ![詳細資料](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. <span data-ttu-id="3c4c1-157">在 hello**標誌**區段 hello**詳細資料**索引標籤上，更新 hello 標誌。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-157">In hello **LOGOS** section of hello **DETAILS** tab, update hello logos.</span></span> <span data-ttu-id="3c4c1-158">請確定 hello 標誌遵循 hello [Azure Marketplace 的指導方針](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-158">Ensure that hello logos follow hello [Azure Marketplace guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-159">主圖圖示是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-159">A hero icon is optional.</span></span> <span data-ttu-id="3c4c1-160">您可以選擇不 tooupload 英雄圖示。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-160">You can choose not tooupload a hero icon.</span></span> <span data-ttu-id="3c4c1-161">不過上, 傳英雄圖示之後，沒有任何佈建 toodelete 從 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-161">However, after a hero icon is uploaded, there is no provision toodelete it from hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-162">請遵循 hello[英雄圖示指導方針](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-162">Follow hello [hero icon guidelines](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
   >
   >
7. <span data-ttu-id="3c4c1-163">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-163">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-164">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-164">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="3c4c1-165">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-165">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-166">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-166">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![標誌](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a><span data-ttu-id="3c4c1-168">更新 hello SKU 描述</span><span class="sxs-lookup"><span data-stu-id="3c4c1-168">Update hello SKU description</span></span>
<span data-ttu-id="3c4c1-169">tooupdate hello SKU 詳細資料，並重新發行您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-169">tooupdate hello SKU details and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-170">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-170">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-171">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-171">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-172">在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-172">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="3c4c1-173">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-173">Click **English (US)**.</span></span>
5. <span data-ttu-id="3c4c1-174">按一下 hello**計劃**] 索引標籤。在 [hello **Sku**區段中，更新 hello SKU**標題**，**摘要**，和**描述**儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-174">Click hello **PLANS** tab. In hello **SKUs** section, update hello SKU **TITLE**, **SUMMARY**, and **DESCRIPTION** and save hello changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-175">當您更新 hello SKU 詳細資料時，請注意這些限制：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-175">When you update hello SKU details, be aware of these restrictions:</span></span> 
   * <span data-ttu-id="3c4c1-176">請勿將重複的文字輸入 hello 供應項目描述和 hello SKU 描述。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-176">Do not enter duplicate text for hello offer description and hello SKU description.</span></span> 
   * <span data-ttu-id="3c4c1-177">請勿 hello SKU 標題和 hello 供應項目完整摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-177">Do not enter duplicate text for hello SKU title and hello offer long summary.</span></span> 
   * <span data-ttu-id="3c4c1-178">請勿為 hello SKU 標題和 hello 供給摘要輸入重複的文字。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-178">Do not enter duplicate text for hello SKU title and hello offer summary.</span></span>
   >
   >
6. <span data-ttu-id="3c4c1-179">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-179">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-180">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-180">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="3c4c1-181">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-181">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-182">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-182">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![方案](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a><span data-ttu-id="3c4c1-184">變更現有連結或新增連結</span><span class="sxs-lookup"><span data-stu-id="3c4c1-184">Change existing links or add new links</span></span>
<span data-ttu-id="3c4c1-185">toochange 現有連結或加入新的連結，然後重新發佈您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-185">toochange existing links or add new links and then republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-186">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-186">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-187">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-187">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-188">在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-188">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="3c4c1-189">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-189">Click **English (US)**.</span></span>
5. <span data-ttu-id="3c4c1-190">按一下 hello**連結** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-190">Click hello **LINKS** tab.</span></span>
6. <span data-ttu-id="3c4c1-191">新的連結，在 hello tooadd**連結**區段中，按一下**+ 加入連結**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-191">tooadd a new link, in hello **Links** section, click **+ ADD LINK**.</span></span> <span data-ttu-id="3c4c1-192">在 hello**加入連結**對話方塊方塊中，輸入 hello 連結**標題**和**URL**儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-192">In hello **Add Link** dialog box, enter hello link **TITLE** and **URL** and save hello changes.</span></span> <span data-ttu-id="3c4c1-193">您可以輸入任何包含資訊來協助客戶的連結。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-193">You can enter any link that contains information that might help customers.</span></span>
7. <span data-ttu-id="3c4c1-194">tooupdate 或刪除現有連結，請選取 hello 連結，然後按一下 hello**編輯**按鈕或 hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-194">tooupdate or delete an existing link, select hello link and click hello **Edit** button or hello **Delete** button.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-195">請確定您已輸入本節中的 hello 連結正常運作，因為這些連結取得驗證您在實際執行要求程序。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-195">Ensure that hello links that you've entered in this section are working properly, because these links get validated during your production request process.</span></span>
   >
   >
8. <span data-ttu-id="3c4c1-196">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-196">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-197">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-197">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="3c4c1-198">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-198">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-199">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-199">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![連結](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![新增連結](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a><span data-ttu-id="3c4c1-202">變更現有範例映像或新增範例映像</span><span class="sxs-lookup"><span data-stu-id="3c4c1-202">Change an existing sample image or add a new sample image</span></span>
<span data-ttu-id="3c4c1-203">現有的範例 toochange 映像或加入新的範例映像，然後重新發佈您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-203">toochange an existing sample image or add new sample images and then republish your offer, follow these steps:</span></span>

> [!NOTE]
> <span data-ttu-id="3c4c1-204">只有一個範例影像會顯示在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-204">Only one sample image is displayed in hello [Azure portal](https://portal.azure.com).</span></span>
>
>

1. <span data-ttu-id="3c4c1-205">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-205">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-206">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-206">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-207">在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-207">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="3c4c1-208">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-208">Click **English (US)**.</span></span>
5. <span data-ttu-id="3c4c1-209">按一下 hello**範例影像** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-209">Click hello **SAMPLE IMAGES** tab.</span></span>
6. <span data-ttu-id="3c4c1-210">新範例映像，在 hello tooadd**範例影像**區段中，按一下**上傳新的映像**儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-210">tooadd a new sample image, in hello **Sample Images** section, click **UPLOAD A NEW IMAGE** and save hello changes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-211">包含範例映像是選擇性作業。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-211">Including a sample image is optional.</span></span>
   >
7. <span data-ttu-id="3c4c1-212">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-212">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-213">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-213">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="3c4c1-214">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-214">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-215">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-215">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![範例映像](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a><span data-ttu-id="3c4c1-217">更新 hello 合法的內容</span><span class="sxs-lookup"><span data-stu-id="3c4c1-217">Update hello legal content</span></span>
<span data-ttu-id="3c4c1-218">tooupdate hello 合法的內容重新發佈您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-218">tooupdate hello legal content and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-219">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-219">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-220">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-220">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-221">在左側 hello hello 功能表上，按一下 [hello**行銷**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-221">In hello menu on hello left, click hello **MARKETING** tab.</span></span>
4. <span data-ttu-id="3c4c1-222">按一下 [英文 (美國)]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-222">Click **English (US)**.</span></span>
5. <span data-ttu-id="3c4c1-223">按一下 hello**合法**] 索引標籤。在 [hello**合法**區段中，更新使用您原則/詞彙。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-223">Click hello **LEGAL** tab. In hello **Legal** section, update your policies/terms of use.</span></span> <span data-ttu-id="3c4c1-224">輸入或貼上 hello hello 原則/詞彙**使用條款**方塊，並儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-224">Enter or paste hello policies/terms in hello **TERMS OF USE** box and save hello changes.</span></span>
6. <span data-ttu-id="3c4c1-225">使用 hello 法律規定 hello 字元限制為 1 百萬個字元。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-225">hello character limit for hello legal terms of use is 1 million characters.</span></span>
7. <span data-ttu-id="3c4c1-226">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-226">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-227">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-227">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
8. <span data-ttu-id="3c4c1-228">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-228">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-229">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-229">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![法律](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a><span data-ttu-id="3c4c1-231">更新 hello 支援資訊</span><span class="sxs-lookup"><span data-stu-id="3c4c1-231">Update hello support information</span></span>
<span data-ttu-id="3c4c1-232">tooupdate hello 支援資訊並重新發行您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-232">tooupdate hello support information and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-233">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-233">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-234">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-234">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-235">在左側 hello hello 功能表上，按一下 [hello**支援**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-235">In hello menu on hello left, click hello **SUPPORT** tab.</span></span>
4. <span data-ttu-id="3c4c1-236">在 hello**工程連絡**區段中，更新 hello 工程連絡人詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-236">In hello **Engineering Contact** section, update hello engineering contact details.</span></span> <span data-ttu-id="3c4c1-237">這些詳細資料會用於內部通訊 hello 夥伴與 Microsoft 之間只。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-237">These details are used for internal communication between hello partner and Microsoft only.</span></span>
5. <span data-ttu-id="3c4c1-238">在 hello**客戶支援部門**區段中，更新 hello 支援連絡人詳細資料和 hello**支援 URL**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-238">In hello **Customer Support** section, update hello support contact details and hello **SUPPORT URL**.</span></span> <span data-ttu-id="3c4c1-239">這些詳細資料會用於內部通訊 hello 夥伴與 Microsoft 之間只。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-239">These details are used for internal communication between hello partner and Microsoft only.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-240">如果您想 tooprovide 唯一的電子郵件支援，請輸入空的電話號碼中 hello**客戶支援部門**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-240">If you want tooprovide only email support, enter a dummy phone number in hello **Customer Support** section.</span></span> <span data-ttu-id="3c4c1-241">在此情況下，您提供的 hello 電子郵件改為使用。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-241">In this case, hello email you provided is used instead.</span></span>
   >
   >
6. <span data-ttu-id="3c4c1-242">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-242">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-243">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-243">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="3c4c1-244">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-244">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-245">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-245">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![支援](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a><span data-ttu-id="3c4c1-247">更新 hello 類別</span><span class="sxs-lookup"><span data-stu-id="3c4c1-247">Update hello categories</span></span>
<span data-ttu-id="3c4c1-248">tooupdate hello 類別為您提供的服務區段，然後重新發佈您的優惠，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-248">tooupdate hello categories section for your offer and republish your offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-249">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-249">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-250">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-250">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-251">在左側 hello hello 功能表上，按一下 [hello**類別**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-251">In hello menu on hello left, click hello **CATEGORIES** tab.</span></span>
4. <span data-ttu-id="3c4c1-252">在 hello**類別**區段中，更新您的優惠的 hello 分類然後儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-252">In hello **Categories** section, update hello categories for your offer and save hello changes.</span></span> <span data-ttu-id="3c4c1-253">您可以選擇 toofive hello Azure Marketplace 的組件庫的類別。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-253">You can choose up toofive categories for hello Azure Marketplace gallery.</span></span>
5. <span data-ttu-id="3c4c1-254">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-254">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-255">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-255">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
6. <span data-ttu-id="3c4c1-256">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-256">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-257">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-257">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![類別](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a><span data-ttu-id="3c4c1-259">在已列出的供應項目下新增 SKU</span><span class="sxs-lookup"><span data-stu-id="3c4c1-259">Add a new SKU under a listed offer</span></span>
<span data-ttu-id="3c4c1-260">tooadd 新 SKU 中您的提供即時服務，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-260">tooadd a new SKU in your live offer, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-261">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-261">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-262">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-262">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-263">在左側 hello hello 功能表上，按一下 [hello **SKU** ] 索引標籤。然後按一下 [新增 SKU]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-263">In hello menu on hello left, click hello **SKUS** tab. Then click **Add a SKU**.</span></span> 
4. <span data-ttu-id="3c4c1-264">在 [hello] 對話方塊中，輸入**SKU 識別碼**小寫。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-264">In hello dialog box, enter a **SKU Identifier** in lowercase.</span></span> <span data-ttu-id="3c4c1-265">選取 hello**攜帶您自己的授權 (BYOL) 計費模型**核取方塊，如果您想 toopublish hello BYOL 計費的模型使用新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-265">Select hello **Bring your own license (BYOL) billing model** check box if you want toopublish hello new SKU with a BYOL billing model.</span></span> <span data-ttu-id="3c4c1-266">否則，請清除 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-266">Otherwise, clear hello check box.</span></span> <span data-ttu-id="3c4c1-267">按一下 hello 刻度記號 toocreate 新 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-267">Click hello tick mark toocreate a new SKU.</span></span> <span data-ttu-id="3c4c1-268">如果您未選擇 hello BYOL 計費模型，hello 計費模型會自動設定 toohourly。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-268">If you didn't choose hello BYOL billing model, hello billing model is automatically set toohourly.</span></span> <span data-ttu-id="3c4c1-269">如果您想 hello 每小時的計費模型的 hello 30 天免費試用版，請選取**一個月**如**可免費試用版嗎？**</span><span class="sxs-lookup"><span data-stu-id="3c4c1-269">If you want hello 30-day free trial for hello hourly billing model, select **One Month** for **Is a free trial available?**</span></span> <span data-ttu-id="3c4c1-270">否則，請選取 [無試用]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-270">Otherwise, select **No Trial**.</span></span> <span data-ttu-id="3c4c1-271">(**可免費試用版嗎？**時建立 hello 新 SKU 您尚未選取 BYOL 時，才會出現。)</span><span class="sxs-lookup"><span data-stu-id="3c4c1-271">(**Is a free trial available?** appears only if you haven't selected BYOL while creating hello new SKU.)</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3c4c1-272">**因為永遠應該購買方案範本透過隱藏 hello Marketplace 從這個 SKU**應該**是***只*如果核准以發佈方案範本。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-272">**Hide this SKU from hello Marketplace because it should always be bought via a solution template** should be **Yes** *only* if you're approved for publishing a solution template.</span></span> <span data-ttu-id="3c4c1-273">否則，這個選項應該永遠都是 [否]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-273">Otherwise, this option should always be **No**.</span></span>
   >
   >
4. <span data-ttu-id="3c4c1-274">在左側 hello hello 功能表上，按一下 [hello **VM 映像**] 索引標籤，找出 hello 您已建立的新 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-274">In hello menu on hello left, click hello **VM IMAGES** tab and find out hello new SKU that you've created.</span></span>
5. <span data-ttu-id="3c4c1-275">tooset 最多 hello 新 SKU，請參閱[取得憑證的 VM 映像](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image)指導方針。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-275">tooset up hello new SKU, see [Obtain certification for your VM image](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) for guidance.</span></span>
6. <span data-ttu-id="3c4c1-276">行銷資料 tooadd hello 新 SKU，請參閱[行銷內容提供 Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-276">tooadd marketing material for hello new SKU, see [Provide Marketplace marketing content](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).</span></span>
7. <span data-ttu-id="3c4c1-277">定價資訊的 tooadd hello 新 SKU，請參閱[設定價格](marketplace-publishing-push-to-staging.md#step-2-set-your-prices)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-277">tooadd pricing information for hello new SKU, see [Set your prices](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).</span></span>
8. <span data-ttu-id="3c4c1-278">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-278">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-279">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-279">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
9. <span data-ttu-id="3c4c1-280">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-280">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-281">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-281">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

    ![SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![新增 SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a><span data-ttu-id="3c4c1-284">變更所列的 SKU hello 資料磁碟計數</span><span class="sxs-lookup"><span data-stu-id="3c4c1-284">Change hello data disk count for a listed SKU</span></span>
<span data-ttu-id="3c4c1-285">您無法遞增/遞減 hello 資料磁碟計數列出的 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-285">You can't increment/decrement hello data disk count of a listed SKU.</span></span> <span data-ttu-id="3c4c1-286">在此情況下，您需要 toocreate 新 SKU。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-286">You need toocreate a new SKU in this case.</span></span> <span data-ttu-id="3c4c1-287">如需詳細指引，請參閱 toohello 區段[加入列出的供應項目底下的新 SKU](#add-a-new-sku-under-a-listed-offer)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-287">For detailed guidance, refer toohello section [Add a new SKU under a listed offer](#add-a-new-sku-under-a-listed-offer).</span></span>

## <a name="delete-a-listed-offer-from-hello-marketplace"></a><span data-ttu-id="3c4c1-288">列出的優惠刪除 hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="3c4c1-288">Delete a listed offer from hello Marketplace</span></span>
<span data-ttu-id="3c4c1-289">各個層面需要 toobe 要求 tooremove 即時優惠 hello 案例處理。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-289">Various aspects need toobe taken care of in hello case of a request tooremove a live offer.</span></span> <span data-ttu-id="3c4c1-290">hello 支援小組 tooremove hello Marketplace，列出提供項目從 tooget 指引，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-290">tooget guidance from hello support team tooremove a listed offer from hello Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-291">引發支援票證上 hello[建立事件](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681)頁面。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-291">Raise a support ticket on hello [Create an incident](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) page.</span></span>

2. <span data-ttu-id="3c4c1-292">選取 [管理供應項目] 作為 [問題類型]，然後選取 [修改已在生產中的供應項目和/或 SKU] 作為 [類別]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-292">Select **Problem type** as **Managing offers**, and select **Category** as **Modifying an offer and/or SKU already in production**.</span></span>
3. <span data-ttu-id="3c4c1-293">送出 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-293">Submit hello request.</span></span>

<span data-ttu-id="3c4c1-294">hello 支援小組會引導您完成 hello 優惠/SKU 刪除程序。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-294">hello support team guides you through hello offer/SKU deletion process.</span></span>

> [!NOTE]
> <span data-ttu-id="3c4c1-295">在 [草稿] 狀態 （但不是預備或生產） 時，隨時都可以刪除 hello 供應項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-295">You can always delete hello offer while it is in Draft status (but not Staging or Production).</span></span> <span data-ttu-id="3c4c1-296">在 hello**記錄**索引標籤上，按一下 **捨棄草稿**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-296">On hello **HISTORY** tab, click **DISCARD DRAFT**.</span></span>
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a><span data-ttu-id="3c4c1-297">從 hello Marketplace 刪除列出的 SKU</span><span class="sxs-lookup"><span data-stu-id="3c4c1-297">Delete a listed SKU from hello Marketplace</span></span>
<span data-ttu-id="3c4c1-298">toodelete 列出 SKU 從 hello 服務商場，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-298">toodelete a listed SKU from hello Marketplace, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-299">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-299">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="3c4c1-300">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-300">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-301">在 hello hello 左側窗格，按一下 hello **SKU**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-301">In hello pane on hello left, click hello **SKUS** tab.</span></span>
4. <span data-ttu-id="3c4c1-302">選取 hello SKU toodelete，並按一下 hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-302">Select hello SKU that you want toodelete, and click hello **Delete** button.</span></span>
5. <span data-ttu-id="3c4c1-303">移 toohello**發行** 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-303">Go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-304">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello hello Marketplace 中的供應項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-304">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish hello offer in hello Marketplace.</span></span>
6. <span data-ttu-id="3c4c1-305">Hello 供應項目會重新發行在 hello Marketplace 之後，會刪除 hello SKU hello Marketplace 和 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-305">After hello offer is republished in hello Marketplace, hello SKU is deleted from hello Marketplace and hello Azure portal.</span></span>

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a><span data-ttu-id="3c4c1-306">從 hello Marketplace 刪除 hello 目前版本列出的 SKU</span><span class="sxs-lookup"><span data-stu-id="3c4c1-306">Delete hello current version of a listed SKU from hello Marketplace</span></span>
<span data-ttu-id="3c4c1-307">toodelete hello 目前版本列出 SKU 從 hello 服務商場，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-307">toodelete hello current version of a listed SKU from hello Marketplace, follow these steps:</span></span> 

1. <span data-ttu-id="3c4c1-308">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-308">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="3c4c1-309">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-309">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-310">在左側 hello hello 功能表上，按一下 [hello **VM 映像**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-310">In hello menu on hello left, click hello **VM IMAGES** tab.</span></span>
4. <span data-ttu-id="3c4c1-311">選取 hello SKU 的目前版本 toodelete，然後按一下 hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-311">Select hello SKU whose current version you want toodelete, and click hello **Delete** button.</span></span>
5. <span data-ttu-id="3c4c1-312">移 toohello**發行** 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-312">Go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-313">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello hello Marketplace 中的供應項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-313">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish hello offer in hello Marketplace.</span></span>
6. <span data-ttu-id="3c4c1-314">Hello 供應項目取得 hello Marketplace 中發佈之後，hello 的 hello 列出的 SKU 從中 hello Marketplace 和 hello Azure 入口網站的目前版本。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-314">After hello offer gets republished in hello Marketplace, hello current version of hello listed SKU is deleted from hello Marketplace and hello Azure portal.</span></span> <span data-ttu-id="3c4c1-315">hello SKU 將會回復 tooits 先前的版本。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-315">hello SKU is then rolled back tooits previous version.</span></span>

## <a name="revert-hello-listing-price-tooproduction-values"></a><span data-ttu-id="3c4c1-316">還原 hello 列出價格 tooproduction 值</span><span class="sxs-lookup"><span data-stu-id="3c4c1-316">Revert hello listing price tooproduction values</span></span>
<span data-ttu-id="3c4c1-317">toorevert hello 清單價格 tooproduction 值，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-317">toorevert hello listing price tooproduction values, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-318">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-318">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>
2. <span data-ttu-id="3c4c1-319">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-319">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-320">在左側 hello hello 功能表上，按一下 [hello**定價**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-320">In hello menu on hello left, click hello **PRICING** tab.</span></span>
4. <span data-ttu-id="3c4c1-321">選取您想要其價格的地區 tooreset。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-321">Select a region whose pricing you want tooreset.</span></span>

    ![價格區域](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. <span data-ttu-id="3c4c1-323">對於每小時的計費模型的 Sku，重設所有 hello 核心的 hello 價格和它們在 hello 所選區域的生產環境中。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-323">For SKUs with an hourly billing model, reset hello prices for all hello cores as they are in production for hello selected region.</span></span> <span data-ttu-id="3c4c1-324">Sku BYOL 計費的模型，請選取 hello SKU 的 hello 核取方塊在 hello hello hello 區域中可用的 SKU **EXTERNALLY-LICENSED (BYOL) SKU 可用性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-324">For SKUs with a BYOL billing model, make hello SKU available in hello region by selecting hello check box for hello SKU in hello **EXTERNALLY-LICENSED (BYOL) SKU AVAILABILITY** section.</span></span>

    ![定價模式](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. <span data-ttu-id="3c4c1-326">按一下 [依據美國價格自動訂定其他市場價格] 。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-326">Click **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c4c1-327">hello 按鈕的標籤可能會不同，視您選取的 hello 地區而定。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-327">hello button’s label might be different depending on hello region that you select.</span></span> <span data-ttu-id="3c4c1-328">因為我們選取 美國，所以 hello 按鈕的標籤為**AUTOPRICE 其他市場基礎 ON 價格在美國的狀態**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-328">Because we selected United States, hello button is labeled **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES**.</span></span>
   >
   >

    ![自動定價](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. <span data-ttu-id="3c4c1-330">在 hello Autoprice 精靈的第 1 頁，選擇 hello 基底的市場，然後按 hello**箭號** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-330">On page 1 of hello Autoprice wizard, choose hello base market and click hello **arrow** button.</span></span>

    ![基底市場](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. <span data-ttu-id="3c4c1-332">在第 2 頁，選擇服務計劃和公尺 （核心），然後按 hello**箭號** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-332">On page 2, choose service plans and meters (cores), and click hello **arrow** button.</span></span>

    ![服務方案和計量](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. <span data-ttu-id="3c4c1-334">在第 3 頁，按一下 **切換所有**tooselect 所有區域。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-334">On page 3, click **Toggle All** tooselect all regions.</span></span> <span data-ttu-id="3c4c1-335">或者，您可以手動選取特定區域的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-335">Or you can manually select check boxes for specific regions.</span></span> <span data-ttu-id="3c4c1-336">按一下 hello**箭號** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-336">Click hello **arrow** button.</span></span>

    ![選擇市場](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. <span data-ttu-id="3c4c1-338">在頁面 4 檢閱 hello 匯率，並按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-338">On page 4, review hello exchange rates and click **Finish**.</span></span> <span data-ttu-id="3c4c1-339">hello 精靈會重設 hello 定價相應 tooyour 選取項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-339">hello wizard resets hello pricing according tooyour selections.</span></span>

11. <span data-ttu-id="3c4c1-340">在 hello**定價**索引標籤上，按一下 **檢視和變更摘要**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-340">On hello **PRICING** tab, click **VIEW SUMMARY AND CHANGES**.</span></span>
    <span data-ttu-id="3c4c1-341">對於 [檢視版本]，選取 [草稿]，以及針對 [比較項目]，選取 [生產]。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-341">For **View Version**, select **Draft**, and for **Compare with**, select **Production**.</span></span> <span data-ttu-id="3c4c1-342">如果您不看到任何價格差異，hello 定價 toohello 生產環境值成功還原。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-342">If you see no pricing difference, hello pricing reverted toohello production values successfully.</span></span>

    ![摘要檢視和變更](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. <span data-ttu-id="3c4c1-344">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-344">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-345">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-345">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
13. <span data-ttu-id="3c4c1-346">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-346">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-347">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-347">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

## <a name="revert-hello-billing-model-tooproduction-values"></a><span data-ttu-id="3c4c1-348">還原 hello 計費模型 tooproduction 值</span><span class="sxs-lookup"><span data-stu-id="3c4c1-348">Revert hello billing model tooproduction values</span></span>
<span data-ttu-id="3c4c1-349">toorevert hello 計費模型 tooproduction 值，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-349">toorevert hello billing model tooproduction values, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-350">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-350">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="3c4c1-351">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-351">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-352">在左側 hello hello 功能表上，按一下 [hello **SKU** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-352">In hello menu on hello left, click hello **SKUS** tab.</span></span>
4. <span data-ttu-id="3c4c1-353">按一下 hello**編輯**按鈕 toorevert hello 計費模型。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-353">Click hello **Edit** button toorevert hello billing model.</span></span> <span data-ttu-id="3c4c1-354">在 hello 開啟視窗中，選取或清除 hello**計費和授權由外部 Azure （又稱 「 攜帶您自己授權）**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-354">In hello window that opens, select or clear hello **Billing and licensing is done externally from Azure (aka Bring Your Own License)** check box.</span></span>

    ![編輯計費](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. <span data-ttu-id="3c4c1-356">遵循本文章中的"Revert hello 列出價格 tooproduction 值"hello 步驟進行。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-356">Follow hello steps in "Revert hello listing price tooproduction values" in this article.</span></span>
6. <span data-ttu-id="3c4c1-357">移 toohello**發行**索引標籤，然後按一下**發送 tooSTAGING**。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-357">Go toohello **PUBLISH** tab, and click **PUSH tooSTAGING**.</span></span> <span data-ttu-id="3c4c1-358">如需詳細指引 hello 預備環境中測試您的優惠的詳細資訊，請參閱[測試 VM 提供 hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-358">For detailed guidance on testing your offer in hello staging environment, see [Test your VM offer for hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).</span></span>
7. <span data-ttu-id="3c4c1-359">測試過您的優惠之後在接移移 [toohello**發行**] 索引標籤中 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-359">After you've tested your offer in staging, go toohello **PUBLISH** tab in hello Publishing portal.</span></span> <span data-ttu-id="3c4c1-360">按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-360">Click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a><span data-ttu-id="3c4c1-361">還原列出的 SKU toohello 生產環境值 hello 可見性設定</span><span class="sxs-lookup"><span data-stu-id="3c4c1-361">Revert hello visibility setting of a listed SKU toohello production value</span></span>
<span data-ttu-id="3c4c1-362">列出 SKU toohello 實際值，toorevert hello 可見性設定，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3c4c1-362">toorevert hello visibility setting of a listed SKU toohello production value, follow these steps:</span></span>

1. <span data-ttu-id="3c4c1-363">登入 toohello[發佈入口網站](https://publish.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-363">Sign in toohello [Publishing portal](https://publish.windowsazure.com).</span></span>

2. <span data-ttu-id="3c4c1-364">移 toohello**虛擬機器**索引標籤，然後選取您的優惠。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-364">Go toohello **virtual machines** tab, and select your offer.</span></span>
3. <span data-ttu-id="3c4c1-365">在左側 hello hello 功能表上，按一下 [hello **SKU** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-365">In hello menu on hello left, click hello **SKUS** tab.</span></span>
4. <span data-ttu-id="3c4c1-366">選取您的 SKU，並還原 hello 的 hello SKU toohello 生產環境值的可見性設定。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-366">Select your SKU, and revert hello visibility setting of hello SKU toohello production value.</span></span>

    ![可見性](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. <span data-ttu-id="3c4c1-368">您已完成 hello 變更之後，請按一下**要求核准 tooPUSH tooPRODUCTION** toorepublish hello Marketplace 中的服務項目。</span><span class="sxs-lookup"><span data-stu-id="3c4c1-368">After you're done with hello changes, click **REQUEST APPROVAL tooPUSH tooPRODUCTION** toorepublish your offer in hello Marketplace.</span></span>

## <a name="see-also"></a><span data-ttu-id="3c4c1-369">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3c4c1-369">See also</span></span>
* [<span data-ttu-id="3c4c1-370">開始： 發佈供應項目 toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3c4c1-370">Get Started: Publish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="3c4c1-371">了解付款報告</span><span class="sxs-lookup"><span data-stu-id="3c4c1-371">Understand payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="3c4c1-372">變更雲端解決方案提供者轉售商獎勵</span><span class="sxs-lookup"><span data-stu-id="3c4c1-372">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="3c4c1-373">疑難排解 hello Marketplace 中的一般發佈問題</span><span class="sxs-lookup"><span data-stu-id="3c4c1-373">Troubleshoot common publishing problems in hello Marketplace</span></span>](marketplace-publishing-support-common-issues.md)
* [<span data-ttu-id="3c4c1-374">以發佈者身分取得支援</span><span class="sxs-lookup"><span data-stu-id="3c4c1-374">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)
* [<span data-ttu-id="3c4c1-375">建立內部部署 VM 映像</span><span class="sxs-lookup"><span data-stu-id="3c4c1-375">Create a VM image on-premises</span></span>](marketplace-publishing-vm-image-creation-on-premise.md)
* [<span data-ttu-id="3c4c1-376">建立執行 Windows hello Azure preview 入口網站中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="3c4c1-376">Create a virtual machine running Windows in hello Azure preview portal</span></span>](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
