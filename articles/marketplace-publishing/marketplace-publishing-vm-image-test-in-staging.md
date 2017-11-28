---
title: "您的 VM 提供 hello Marketplace aaaTest |Microsoft 文件"
description: "了解如何 tootest VM 的映像 hello Azure Marketplace。"
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
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="9d569-103">在預備環境中測試您的 VM 優惠 hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9d569-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="9d569-104">預備部署您的 「 沙箱 」 可測試及驗證其功能，再將其部署 toohello Marketplace 的私用的 SKU 的方式。</span><span class="sxs-lookup"><span data-stu-id="9d569-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="9d569-105">hello SKU 會出現在暫存就像是 tooa 客戶已經部署。</span><span class="sxs-lookup"><span data-stu-id="9d569-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="9d569-106">您的 VM 映像必須是推入的認證的 toobe toostaging。</span><span class="sxs-lookup"><span data-stu-id="9d569-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="9d569-107">步驟 1： 推入的供應項目 toostaging</span><span class="sxs-lookup"><span data-stu-id="9d569-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="9d569-108">在 hello**發行**索引標籤上，按一下 **推送 tooStaging**。</span><span class="sxs-lookup"><span data-stu-id="9d569-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![繪圖](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="9d569-110">如果 hello 發佈入口網站會通知您的任何錯誤，更正它們。</span><span class="sxs-lookup"><span data-stu-id="9d569-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="9d569-111">在 hello**誰可以存取您提供執行的服務？**對話方塊方塊中，輸入 Azure 訂用帳戶，您將使用 toopreview 您提供的服務中 hello hello 清單[Azure preview 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9d569-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d569-112">如果是「虛擬機器」和「方案」範本，請 **不要** 將 CSP、DreamSpark 或 Azure in Open 類型的訂用帳戶加入允許清單。</span><span class="sxs-lookup"><span data-stu-id="9d569-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="9d569-113">發生虛擬機器，當您按一下 [hello] 5d; 按鈕**發送 tooSTAGING**，hello 步驟會執行背後 hello 場景。</span><span class="sxs-lookup"><span data-stu-id="9d569-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="9d569-114">您將會無法 tooview hello 進度 hello hello 發行 索引標籤底下的每個步驟的發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="9d569-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="9d569-115">您必須檢查這個頁面在定期間隔 （直到 hello 狀態顯示分段） 需要從您的 end 更正任何失敗資訊。</span><span class="sxs-lookup"><span data-stu-id="9d569-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="9d569-116">一開始您執行的要求會驗證 hello vhd toohello 憑證小組。</span><span class="sxs-lookup"><span data-stu-id="9d569-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="9d569-117">不過，如果您的要求有只有行銷變更，然後 hello 憑證會略過步驟。</span><span class="sxs-lookup"><span data-stu-id="9d569-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="9d569-118">Hello 憑證完成之後，複寫的 hello 供應項目開始，所有 hello Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="9d569-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="9d569-119">它通常會採用 24-48hours hello 複寫 toocomplete 的但可能佔用 tooa 週 hello hello vhd 大小而定。</span><span class="sxs-lookup"><span data-stu-id="9d569-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="9d569-120">不過，如果您的要求有只有行銷變更，hello 複寫會更快。</span><span class="sxs-lookup"><span data-stu-id="9d569-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="9d569-121">Hello 複寫完成時，則 hello 供應項目會提供在 hello [Azure 入口網站](http:/portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9d569-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="9d569-122">在該時間 hello 狀態變成暫置在 hello 中發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="9d569-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="9d569-123">階段式供應項目會顯示在 hello [Azure 入口網站](http:/portal.azure.com)只能使用 hello 與 hello 接移的 hello 與優惠的訂用帳戶相關聯的電子郵件識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d569-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="9d569-124">登入 toohello [Azure preview 入口網站](https://portal.azure.com)使用其中一種 hello Azure 訂用帳戶中所列 hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="9d569-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="9d569-125">尋找您的供應項目，並驗證您的 VM 映像點：</span><span class="sxs-lookup"><span data-stu-id="9d569-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="9d569-126">請確定在行銷內容可正確顯示 hello Marketplace 中。</span><span class="sxs-lookup"><span data-stu-id="9d569-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="9d569-127">端對端部署的 hello VM 映像。</span><span class="sxs-lookup"><span data-stu-id="9d569-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="9d569-129">您提供的服務將保留在暫存直到您通知 Microsoft hello 發佈入口網站透過 [**發行** 索引標籤 > hello 5d; 按鈕按一下**」 要求核准 tooPush tooProduction 」**] 您已準備好 toopushtooproduction。</span><span class="sxs-lookup"><span data-stu-id="9d569-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="9d569-130">這是小組的理想的時間 toohave，透過在您要列出的優惠準備的所有項目檢查您的所有成員。</span><span class="sxs-lookup"><span data-stu-id="9d569-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="9d569-131">hello 發行者在預覽模式中的測試 hello 供應項目的保護 hello 暫存平台。</span><span class="sxs-lookup"><span data-stu-id="9d569-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="9d569-132">我們強烈建議您勿將此平台使用於商業用途。</span><span class="sxs-lookup"><span data-stu-id="9d569-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9d569-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d569-133">Next steps</span></span>
<span data-ttu-id="9d569-134">既然您提供的服務 「 預備 」，且您已測試其功能與行銷內容，您可以繼續 toohello 最終發行階段中，**步驟 4**:[部署您的優惠 toohello Marketplace](marketplace-publishing-push-to-production.md)。</span><span class="sxs-lookup"><span data-stu-id="9d569-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9d569-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9d569-135">See also</span></span>
* [<span data-ttu-id="9d569-136">快速入門： 如何 toopublish 優惠 toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9d569-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

