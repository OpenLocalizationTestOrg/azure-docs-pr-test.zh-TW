---
title: "測試將發佈到 Marketplace 的 VM 供應項目 | Microsoft Docs"
description: "了解如何測試您的 VM 供應項目在 Azure Marketplace 的表現。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="f2e64-103">在預備環境中測試您將發佈到 Azure Marketplace 的 VM 供應項目</span><span class="sxs-lookup"><span data-stu-id="f2e64-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="f2e64-104">預備環境代表將您的 SKU 部署在私人的「沙箱」中，您可以在部署到 Marketplace 之前在沙箱中測試與驗證其功能。</span><span class="sxs-lookup"><span data-stu-id="f2e64-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="f2e64-105">SKU 會出現在預備環境中，就如同客戶已部署該項目一樣。</span><span class="sxs-lookup"><span data-stu-id="f2e64-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="f2e64-106">您的 VM 映像必須經過認證才能推送至預備環境。</span><span class="sxs-lookup"><span data-stu-id="f2e64-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="f2e64-107">步驟 1：推送供應項目至預備環境</span><span class="sxs-lookup"><span data-stu-id="f2e64-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="f2e64-108">在 [發佈] 索引標籤上,按一下 [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="f2e64-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![繪圖](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="f2e64-110">如果發佈入口網站通知您任何錯誤，修正它們。</span><span class="sxs-lookup"><span data-stu-id="f2e64-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="f2e64-111">在 [ **誰可以存取您預備的供應項目？** ] 對話方塊中，輸入您要用來在 [Azure Preview 入口網站](https://portal.azure.com)中預覽供應項目的 Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="f2e64-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f2e64-112">如果是「虛擬機器」和「方案」範本，請 **不要** 將 CSP、DreamSpark 或 Azure in Open 類型的訂用帳戶加入允許清單。</span><span class="sxs-lookup"><span data-stu-id="f2e64-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="f2e64-113">如果是「虛擬機器」，當您按一下 [推送至預備環境] 按鈕時，會在場景後方執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f2e64-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="f2e64-114">您可以在發佈入口網站的 [發佈] 索引標籤下檢視每個步驟的進度。</span><span class="sxs-lookup"><span data-stu-id="f2e64-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="f2e64-115">您必須定期查看此頁面是否有需要您更正的任何失敗資訊 (直到狀態顯示「已預備」為止) 。</span><span class="sxs-lookup"><span data-stu-id="f2e64-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="f2e64-116">一開始，您的預備環境要求會送到驗證 VHD 的憑證小組。</span><span class="sxs-lookup"><span data-stu-id="f2e64-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="f2e64-117">不過，如果您的要求只有行銷變更，則會略過憑證步驟。</span><span class="sxs-lookup"><span data-stu-id="f2e64-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="f2e64-118">憑證完成後，就會開始跨所有 Azure 資料中心複寫供應項目。</span><span class="sxs-lookup"><span data-stu-id="f2e64-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="f2e64-119">複寫通常需要 24-48 小時才能完成，但依據 VHD 大小而定，最長可能需要一週的時間。</span><span class="sxs-lookup"><span data-stu-id="f2e64-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="f2e64-120">不過，如果您的要求只有行銷變更，複寫會更快速。</span><span class="sxs-lookup"><span data-stu-id="f2e64-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="f2e64-121">當複寫完成後，供應項目就會在 [Azure 入口網站](http:/portal.azure.com)公開發行。</span><span class="sxs-lookup"><span data-stu-id="f2e64-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="f2e64-122">屆時在發佈入口網站中的狀態會變成「已預備」。</span><span class="sxs-lookup"><span data-stu-id="f2e64-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="f2e64-123">只有當您使用與預備供應項目所用的訂用帳戶相關的電子郵件識別碼時，才能在 [Azure 入口網站](http:/portal.azure.com) 中看到已預備的供應項目。</span><span class="sxs-lookup"><span data-stu-id="f2e64-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="f2e64-124">使用上一個步驟中列出的其中一個 Azure 訂用帳戶登入 [Azure Preview 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="f2e64-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="f2e64-125">尋找您的供應項目，並驗證您的 VM 映像點：</span><span class="sxs-lookup"><span data-stu-id="f2e64-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="f2e64-126">請確定該行銷內容可在 MarketPlace 中正確顯示。</span><span class="sxs-lookup"><span data-stu-id="f2e64-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="f2e64-127">VM 映像的端對端部署</span><span class="sxs-lookup"><span data-stu-id="f2e64-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="f2e64-129">您的供應項目將留在預備環境中，直到您透過發佈入口網站 ([發佈] 索引標籤 > 按一下 [要求核准以推送至生產環境] 按鈕) 通知 Microsoft 您已準備好推送至生產環境為止。</span><span class="sxs-lookup"><span data-stu-id="f2e64-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="f2e64-130">這是所有團隊成員為您即將列出的供應項目做好萬全準備並徹底檢查的最佳時機。</span><span class="sxs-lookup"><span data-stu-id="f2e64-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="f2e64-131">預備平台是為了讓發行者在預覽模式下測試供應項目所設計。</span><span class="sxs-lookup"><span data-stu-id="f2e64-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="f2e64-132">我們強烈建議您勿將此平台使用於商業用途。</span><span class="sxs-lookup"><span data-stu-id="f2e64-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f2e64-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2e64-133">Next steps</span></span>
<span data-ttu-id="f2e64-134">現在您的供應項目「預備」好了，您已經測試過它的功能和行銷內容，您可以繼續進行最終的發佈階段，即 **步驟 4**： [將您的供應項目部署至 Marketplace](marketplace-publishing-push-to-production.md)。</span><span class="sxs-lookup"><span data-stu-id="f2e64-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f2e64-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f2e64-135">See also</span></span>
* [<span data-ttu-id="f2e64-136">使用者入門：如何將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f2e64-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

