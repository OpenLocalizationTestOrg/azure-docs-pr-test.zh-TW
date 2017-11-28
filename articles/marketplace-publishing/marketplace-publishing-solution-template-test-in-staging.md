---
title: "針對 Marketplace 測試您的解決方案範本供應項目 | Microsoft Docs"
description: "了解如何針對 Azure Marketplace 測試您的解決方案範本供應項目。"
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
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="0fddb-103">在預備環境中測試您的解決方案範本供應項目</span><span class="sxs-lookup"><span data-stu-id="0fddb-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="0fddb-104">預備環境代表將您的供應項目部署在私人的「沙箱」中，您可以在推送到生產環境之前在沙箱中測試與驗證其功能。</span><span class="sxs-lookup"><span data-stu-id="0fddb-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="0fddb-105">供應項目會出現在預備環境中，就如同客戶已部署該項目一樣。</span><span class="sxs-lookup"><span data-stu-id="0fddb-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="0fddb-106">您的供應項目必須經過認證才能推送至預備環境。</span><span class="sxs-lookup"><span data-stu-id="0fddb-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="0fddb-107">預備供應項目之後，您可以在 [Azure 入口網站](https://portal.azure.com/)中檢視並測試供應項目。</span><span class="sxs-lookup"><span data-stu-id="0fddb-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="0fddb-108">請遵循下列步驟，將您的供應項目推送至預備環境並在 [Azure 入口網站](https://portal.azure.com/)中進行測試：</span><span class="sxs-lookup"><span data-stu-id="0fddb-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="0fddb-109">瀏覽至[發佈入口網站](https://publish.windowsazure.com) > [解決方案範本] 索引標籤 > 您的供應項目 > [發佈] > [推送至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="0fddb-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="0fddb-110">提供您將用來預覽和測試供應項目的 Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="0fddb-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="0fddb-111">使用上一個步驟中使用的訂用帳戶 ID，登入 Azure Preview 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0fddb-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="0fddb-112">在 Azure Preview 入口網站中，將以下提到的重點至少執行一回合測試：</span><span class="sxs-lookup"><span data-stu-id="0fddb-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="0fddb-113">請確定該行銷內容可在 Azure Marketplace 中正確顯示。</span><span class="sxs-lookup"><span data-stu-id="0fddb-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="0fddb-114">拓撲的端對端部署。</span><span class="sxs-lookup"><span data-stu-id="0fddb-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="0fddb-115">執行效能測試和壓力測試。</span><span class="sxs-lookup"><span data-stu-id="0fddb-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="0fddb-116">確定您的拓撲遵守最佳作法。</span><span class="sxs-lookup"><span data-stu-id="0fddb-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fddb-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fddb-117">Next steps</span></span>
<span data-ttu-id="0fddb-118">如果您很滿意結果，則可以繼續進行最後的供應項目發佈階段，也就是 **步驟 4**：[將您的供應項目部署至 Marketplace](marketplace-publishing-push-to-production.md)。</span><span class="sxs-lookup"><span data-stu-id="0fddb-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="0fddb-119">否則，請在您的供應項目中進行變更並再次要求憑證。</span><span class="sxs-lookup"><span data-stu-id="0fddb-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="0fddb-120">若為行銷內容變更，則不需要憑證。</span><span class="sxs-lookup"><span data-stu-id="0fddb-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="0fddb-121">如需所有發行者工作的指南，請參閱 [快速入門：如何將供應項目發佈至 Azure Marketplace](marketplace-publishing-getting-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="0fddb-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

