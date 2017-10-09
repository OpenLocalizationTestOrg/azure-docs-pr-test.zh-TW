---
title: "aaaTesting 方案範本都提供 hello Marketplace |Microsoft 文件"
description: "了解如何 tootest 方案範本都提供 hello Azure Marketplace。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: 9c195c465d2fc6aa349e4bbcc348e5325f32850d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="35a12-103">在預備環境中測試您的解決方案範本供應項目</span><span class="sxs-lookup"><span data-stu-id="35a12-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="35a12-104">預備部署您的優惠，您可以在此測試並驗證其功能之前將它推送 tooproduction 「 沙箱 」 的私用的方法。</span><span class="sxs-lookup"><span data-stu-id="35a12-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="35a12-105">hello 供應項目會出現在暫存就像是 tooa 客戶已經部署。</span><span class="sxs-lookup"><span data-stu-id="35a12-105">hello offer appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="35a12-106">您提供的服務必須是推入的認證的 toobe toostaging。</span><span class="sxs-lookup"><span data-stu-id="35a12-106">Your offer must be certified toobe pushed toostaging.</span></span>

<span data-ttu-id="35a12-107">預備 hello 供應項目之後，您可以檢視及測試在 hello hello 優惠[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="35a12-107">After hello offer is staged, you can view and test hello offer in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="35a12-108">步驟 hello 下方 toopush 優惠 toostaging 及測試在 hello [Azure 入口網站](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="35a12-108">Follow hello steps below toopush your offer toostaging and test it in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="35a12-109">移 toohello[發佈入口網站](https://publish.windowsazure.com) > **解決方案範本** 索引標籤 > 您的優惠 >**發行** > **推送 tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="35a12-109">Go toohello [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push tooStaging**.</span></span>
2. <span data-ttu-id="35a12-110">您將使用 toopreview 並測試您的優惠，請提供 hello Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="35a12-110">Provide hello list of Azure subscriptions that you will use toopreview and test your offer.</span></span>
3. <span data-ttu-id="35a12-111">使用您在 hello 上一個步驟中使用的 hello 訂用帳戶 ID 登入 toohello Azure preview 入口網站。</span><span class="sxs-lookup"><span data-stu-id="35a12-111">Sign in toohello Azure preview portal by using hello subscription ID that you used in hello previous step.</span></span>
4. <span data-ttu-id="35a12-112">至少一個一回測試中 hello Azure preview 入口網站，如下所述的 hello 點上執行：</span><span class="sxs-lookup"><span data-stu-id="35a12-112">Carry out at least one round of testing in hello Azure preview portal on hello points mentioned below:</span></span>
   * <span data-ttu-id="35a12-113">請確定在行銷內容可正確顯示 hello Azure Marketplace 中。</span><span class="sxs-lookup"><span data-stu-id="35a12-113">Make sure that marketing content shows up correctly in hello Azure Marketplace.</span></span>
   * <span data-ttu-id="35a12-114">Hello 拓樸的端對端部署。</span><span class="sxs-lookup"><span data-stu-id="35a12-114">End-to-end deployment of hello topology.</span></span>
   * <span data-ttu-id="35a12-115">執行效能測試和壓力測試。</span><span class="sxs-lookup"><span data-stu-id="35a12-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="35a12-116">請確定您的拓撲，符合 toohello 最佳作法。</span><span class="sxs-lookup"><span data-stu-id="35a12-116">Ensure that your topology adheres toohello best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35a12-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35a12-117">Next steps</span></span>
<span data-ttu-id="35a12-118">如果您滿意 hello 結果，則您可以繼續發行階段中，toohello 最終優惠**步驟 4**:[部署您的優惠 toohello Marketplace](marketplace-publishing-push-to-production.md)。</span><span class="sxs-lookup"><span data-stu-id="35a12-118">If you are satisfied with hello results, then you can proceed toohello final offer publishing phase, **Step 4**:  [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="35a12-119">否則，請在您的供應項目中進行變更並再次要求憑證。</span><span class="sxs-lookup"><span data-stu-id="35a12-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="35a12-120">若為行銷內容變更，則不需要憑證。</span><span class="sxs-lookup"><span data-stu-id="35a12-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="35a12-121">請參閱[快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)指南 tooall 發行者工作。</span><span class="sxs-lookup"><span data-stu-id="35a12-121">See [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md) for a guide tooall publisher tasks.</span></span>

