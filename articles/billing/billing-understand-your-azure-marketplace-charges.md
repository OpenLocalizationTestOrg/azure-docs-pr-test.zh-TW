---
title: "了解您的 Azure 外部服務費用 | Microsoft Docs"
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
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="71a48-103">了解外部服務費用的 Azure 計費方式</span><span class="sxs-lookup"><span data-stu-id="71a48-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="71a48-104">外部服務先前稱為 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="71a48-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="71a48-105">一般而言，它們是由第三方發佈且適用於 Azure，但已完全整合於 Azure 內的服務。</span><span class="sxs-lookup"><span data-stu-id="71a48-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="71a48-106">例如，ClearDB 和 SendGrid 是可在 Azure 中購買的外部服務，然而它們並非由 Microsoft 所發行。</span><span class="sxs-lookup"><span data-stu-id="71a48-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="71a48-107">當您佈建新的外部服務或資源時，系統會顯示警告︰</span><span class="sxs-lookup"><span data-stu-id="71a48-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Marketplace 購買警告](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="71a48-109">外部服務乃是由 Microsoft 之外的公司所發佈，不過 Microsoft 產品有時候也會分類為外部服務。</span><span class="sxs-lookup"><span data-stu-id="71a48-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="71a48-110">如何對外部服務計費</span><span class="sxs-lookup"><span data-stu-id="71a48-110">How external services are billed</span></span>
- <span data-ttu-id="71a48-111">外部服務會分開計費。</span><span class="sxs-lookup"><span data-stu-id="71a48-111">External services are billed separately.</span></span> <span data-ttu-id="71a48-112">系統會將這類服務視為 Azure 訂用帳戶內的個別訂單。</span><span class="sxs-lookup"><span data-stu-id="71a48-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="71a48-113">當您購買服務時，會設定每項服務的計費期間。</span><span class="sxs-lookup"><span data-stu-id="71a48-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="71a48-114">這樣做可避免與購買服務之訂用帳戶的計費期間混淆。</span><span class="sxs-lookup"><span data-stu-id="71a48-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="71a48-115">您還會收到獨立的帳單，而信用卡收費也會分開進行。</span><span class="sxs-lookup"><span data-stu-id="71a48-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="71a48-116">每項外部服務都有各自的計費模式。</span><span class="sxs-lookup"><span data-stu-id="71a48-116">Each external service has a different billing model.</span></span> <span data-ttu-id="71a48-117">有些服務採用隨用隨付的方式計費，有些則使用按月付款模式。</span><span class="sxs-lookup"><span data-stu-id="71a48-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="71a48-118">您需要使用信用卡來支付 Azure 外部服務的費用，不能以發票付款的方式來購買。</span><span class="sxs-lookup"><span data-stu-id="71a48-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="71a48-119">外部服務不適用於每個月的免費信用額度。</span><span class="sxs-lookup"><span data-stu-id="71a48-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="71a48-120">如果您使用含有[免費信用額度](https://azure.microsoft.com/pricing/spending-limits/)的 Azure 訂用帳戶，該信用額度將無法套用至外部服務帳單。</span><span class="sxs-lookup"><span data-stu-id="71a48-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="71a48-121">請使用信用卡來購買外部服務。</span><span class="sxs-lookup"><span data-stu-id="71a48-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="71a48-122">在 Azure 入口網站檢視外部服務消費和歷程記錄</span><span class="sxs-lookup"><span data-stu-id="71a48-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="71a48-123">在 [Azure 入口網站](https://portal.azure.com/)內，您可以檢視每個訂用帳戶上的外部服務清單：</span><span class="sxs-lookup"><span data-stu-id="71a48-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="71a48-124">以帳戶管理員身分登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="71a48-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="71a48-125">在 [中樞] 功能表中，選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="71a48-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Select Subscriptions in the Hub menu](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="71a48-127">在 [訂用帳戶] 刀鋒視窗中，選取您想要檢視的訂用帳戶，然後選取 [外部服務]。</span><span class="sxs-lookup"><span data-stu-id="71a48-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![在計費刀鋒視窗中選取訂用帳戶](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="71a48-129">您應該會看到每項外部服務的訂單、發行者名稱、購買的服務層、資源的命名及目前的訂單狀態。</span><span class="sxs-lookup"><span data-stu-id="71a48-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="71a48-130">若要查看過去的帳單，請選取外部服務。</span><span class="sxs-lookup"><span data-stu-id="71a48-130">To see past bills, select an external service.</span></span>
   
    ![選取外部服務](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="71a48-132">在這裡，您可以檢視過去的帳單金額，包括稅額細目。</span><span class="sxs-lookup"><span data-stu-id="71a48-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![檢視外部服務帳單記錄](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="71a48-134">檢視 Enterprise 合約 (EA) 客戶的外部服務消費</span><span class="sxs-lookup"><span data-stu-id="71a48-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="71a48-135">EA 客戶可以在 EA 入口網站看到外部服務消費並下載報告。</span><span class="sxs-lookup"><span data-stu-id="71a48-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="71a48-136">請參閱 [EA 客戶的 Azure Marketplace](https://ea.azure.com/helpdocs/azureMarketplace) 以便開始使用。</span><span class="sxs-lookup"><span data-stu-id="71a48-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="71a48-137">管理外部服務訂單的付款方法</span><span class="sxs-lookup"><span data-stu-id="71a48-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="71a48-138">從[帳戶中心](https://account.windowsazure.com/)更新外部服務訂單的付款方法。</span><span class="sxs-lookup"><span data-stu-id="71a48-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="71a48-139">如果您使用公司或學校帳戶來購買訂用帳戶，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)來變更付款方法。</span><span class="sxs-lookup"><span data-stu-id="71a48-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="71a48-140">登入[帳戶中心](https://account.windowsazure.com/)並[瀏覽至 [Marketplace] 索引標籤](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="71a48-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![在帳戶中心內選取 Marketplace](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="71a48-142">選取要管理的外部服務</span><span class="sxs-lookup"><span data-stu-id="71a48-142">Select the external service you want to manage</span></span>
   
    ![選取要管理的外部服務](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="71a48-144">在頁面右側，按一下 [變更付款方式]。</span><span class="sxs-lookup"><span data-stu-id="71a48-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="71a48-145">此連結將帶您前往其他入口網站，以便您管理付款方法。</span><span class="sxs-lookup"><span data-stu-id="71a48-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![訂單摘要](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="71a48-147">按一下 [編輯資訊]，然後遵循指示更新付款資訊。</span><span class="sxs-lookup"><span data-stu-id="71a48-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![選取編輯資訊](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="71a48-149">取消外部服務訂單</span><span class="sxs-lookup"><span data-stu-id="71a48-149">Cancel an external service order</span></span>
<span data-ttu-id="71a48-150">如果想要取消外部服務訂單，請在 [Azure 入口網站](https://portal.azure.com)中刪除該資源。</span><span class="sxs-lookup"><span data-stu-id="71a48-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![刪除資源](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="71a48-152">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="71a48-152">Need help?</span></span> <span data-ttu-id="71a48-153">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="71a48-153">Contact support.</span></span>
<span data-ttu-id="71a48-154">如果您仍有問題，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="71a48-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

