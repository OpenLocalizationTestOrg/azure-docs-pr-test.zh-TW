---
title: "aaaUnderstand Azure 外部的服務費用 |Microsoft 文件"
description: "了解 Azure 中外部服務 (先前稱為 Marketplace) 費用的計費方式。"
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="7c2fd-103">了解外部服務費用的 Azure 計費方式</span><span class="sxs-lookup"><span data-stu-id="7c2fd-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="7c2fd-104">呼叫 Azure Marketplace toobe 使用外部的服務。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="7c2fd-105">一般而言，它們是由第三方發佈且適用於 Azure，但已完全整合於 Azure 內的服務。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="7c2fd-106">例如，ClearDB 和 SendGrid 是可在 Azure 中購買的外部服務，然而它們並非由 Microsoft 所發行。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="7c2fd-107">當您佈建新的外部服務或資源時，系統會顯示警告︰</span><span class="sxs-lookup"><span data-stu-id="7c2fd-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Marketplace 購買警告](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="7c2fd-109">外部服務乃是由 Microsoft 之外的公司所發佈，不過 Microsoft 產品有時候也會分類為外部服務。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="7c2fd-110">如何對外部服務計費</span><span class="sxs-lookup"><span data-stu-id="7c2fd-110">How external services are billed</span></span>
- <span data-ttu-id="7c2fd-111">外部服務會分開計費。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-111">External services are billed separately.</span></span> <span data-ttu-id="7c2fd-112">系統會將這類服務視為 Azure 訂用帳戶內的個別訂單。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="7c2fd-113">您購買 hello 服務時，會設定為每個服務的 hello 計費週期。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="7c2fd-114">不是 toobe hello hello 您購買它所在的訂用帳戶的計費期的問題感到困惑。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="7c2fd-115">您還會收到獨立的帳單，而信用卡收費也會分開進行。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="7c2fd-116">每項外部服務都有各自的計費模式。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-116">Each external service has a different billing model.</span></span> <span data-ttu-id="7c2fd-117">有些服務採用隨用隨付的方式計費，有些則使用按月付款模式。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="7c2fd-118">您需要使用信用卡來支付 Azure 外部服務的費用，不能以發票付款的方式來購買。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="7c2fd-119">外部服務不適用於每個月的免費信用額度。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="7c2fd-120">如果您使用 Azure 訂用帳戶包含[免費信用額度](https://azure.microsoft.com/pricing/spending-limits/)，它們不能套用的 tooexternal 服務帳單。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="7c2fd-121">使用信用卡 toopurchase 外部服務。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="7c2fd-122">檢視外部服務消費和 hello Azure 入口網站中的歷程記錄</span><span class="sxs-lookup"><span data-stu-id="7c2fd-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="7c2fd-123">您可以檢視一份 hello 外部服務的每個訂用帳戶內 hello [Azure 入口網站](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="7c2fd-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="7c2fd-124">登入 toohello [Azure 入口網站](https://portal.azure.com/)hello 帳戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="7c2fd-125">在 hello 中樞功能表中，選取 **訂閱**。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Hello 中樞功能表中選取訂用帳戶](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="7c2fd-127">在 hello**訂閱**刀鋒視窗中，選取 hello 訂閱您想 tooview，，然後選取**外部服務**。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![在 [hello 帳單] 刀鋒視窗中選取訂用帳戶](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="7c2fd-129">您應該會看到每個外部服務訂單、 hello 發行者名稱、 您購買的服務層、 hello 資源和 hello 目前的訂單狀態為您提供名稱。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="7c2fd-130">toosee 過去的帳單，選取 外部服務。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-130">toosee past bills, select an external service.</span></span>
   
    ![選取外部服務](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="7c2fd-132">從這裡，您可以檢視過去的包括 hello 稅分解的帳單金額。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![檢視外部服務帳單記錄](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="7c2fd-134">檢視 Enterprise 合約 (EA) 客戶的外部服務消費</span><span class="sxs-lookup"><span data-stu-id="7c2fd-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="7c2fd-135">EA 客戶可以查看消費外部服務，並下載 hello EA 入口網站中的報表。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="7c2fd-136">請參閱[Azure Marketplace 中的 EA 客戶](https://ea.azure.com/helpdocs/azureMarketplace)tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="7c2fd-137">管理外部服務訂單的付款方法</span><span class="sxs-lookup"><span data-stu-id="7c2fd-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="7c2fd-138">更新付款方式的外部服務訂單從 hello[帳戶中心](https://account.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="7c2fd-139">如果您購買訂用帳戶使用的公司或學校帳戶，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)toomake 變更 tooyour 付款方法。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="7c2fd-140">登入 toohello[帳戶中心](https://account.windowsazure.com/)和[瀏覽 toohello **marketplace**  索引標籤](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="7c2fd-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Hello 帳戶中心] 中選取 [marketplace](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="7c2fd-142">選取您想要 toomanage hello 外部服務</span><span class="sxs-lookup"><span data-stu-id="7c2fd-142">Select hello external service you want toomanage</span></span>
   
    ![選取您想要 toomanage hello 外部服務](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="7c2fd-144">按一下**變更付款方式**右邊 hello hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="7c2fd-145">此連結會帶您 tooa 不同入口 toomanage 付款方法。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![訂單摘要](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="7c2fd-147">按一下**編輯資訊**並遵循指示 tooupdate 付款資訊。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![選取編輯資訊](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="7c2fd-149">取消外部服務訂單</span><span class="sxs-lookup"><span data-stu-id="7c2fd-149">Cancel an external service order</span></span>
<span data-ttu-id="7c2fd-150">如果您想 toocancel 外部服務順序，刪除在 hello hello 資源[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![刪除資源](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="7c2fd-152">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="7c2fd-152">Need help?</span></span> <span data-ttu-id="7c2fd-153">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-153">Contact support.</span></span>
<span data-ttu-id="7c2fd-154">如果您仍有問題，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="7c2fd-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

