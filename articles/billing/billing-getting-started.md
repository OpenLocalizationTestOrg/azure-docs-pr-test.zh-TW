---
title: "避免意外的成本、管理計費 - Azure | Microsoft Docs"
description: "了解如何避免 Azure 帳單上的意外費用。 使用 Microsoft Azure 訂用帳戶的成本追蹤與管理功能。"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 5f9ae830da86a9d03f6d862d4adc7c99849d5014
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a><span data-ttu-id="01c38-104">使用 Azure 計費與成本管理避免非預期的成本</span><span class="sxs-lookup"><span data-stu-id="01c38-104">Prevent unexpected costs with Azure billing and cost management</span></span>

<span data-ttu-id="01c38-105">當您註冊 Azure 時，為了深入了解您的支出，有幾件事您可以做。</span><span class="sxs-lookup"><span data-stu-id="01c38-105">When you sign up for Azure, there are several things you can do to get a better idea of your spend.</span></span> <span data-ttu-id="01c38-106">在 [Azure 入口網站](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)中，選取訂用帳戶之後，您可以看到目前的成本細分和完工速率。</span><span class="sxs-lookup"><span data-stu-id="01c38-106">In the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), when you select the subscription, you can see your current cost breakdown and burn rate.</span></span> <span data-ttu-id="01c38-107">您也可以[下載之前的發票與詳細使用量檔案](billing-download-azure-invoice-daily-usage-date.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-107">You can also [download past invoices and detail usage files](billing-download-azure-invoice-daily-usage-date.md).</span></span> <span data-ttu-id="01c38-108">如果您想要將不同專案或小組所使用的資源成本分組，請查看[資源標記](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-108">If you want to group costs for resources used for different projects or teams, look at [resource tagging](../azure-resource-manager/resource-group-using-tags.md).</span></span> <span data-ttu-id="01c38-109">如果您的組織有您偏好使用的報告系統，請查看[計費 API](billing-usage-rate-card-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-109">If your organization has a reporting system that you prefer to use, check out the [billing APIs](billing-usage-rate-card-overview.md).</span></span> 

<span data-ttu-id="01c38-110">如需每日使用量的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-110">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

<span data-ttu-id="01c38-111">如果您的訂用帳戶是透過 Enterprise 合約 (EA)、雲端解決方案提供者 (CSP) 或 Azure 贊助取得，那麼此文章中所述的許多功能並不適用於您。</span><span class="sxs-lookup"><span data-stu-id="01c38-111">If your subscription is through an Enterprise Agreement (EA), Cloud Solution Provider (CSP), or Azure Sponsorship, then many features in this article don't apply to you.</span></span> <span data-ttu-id="01c38-112">反之，我們有不同的工具組，可供您用於成本管理。</span><span class="sxs-lookup"><span data-stu-id="01c38-112">Instead, we have a different set of tools that you can use for cost management.</span></span> <span data-ttu-id="01c38-113">請參閱[適用於 EA、CSP 和贊助的其他資源](#other-offers)。</span><span class="sxs-lookup"><span data-stu-id="01c38-113">See [Additional resources for EA, CSP, and Sponsorship](#other-offers).</span></span>

<span data-ttu-id="01c38-114">如果您的訂用帳戶是免費試用、[Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)、Azure in Open (AIO) 或 BizSpark，請了解[消費限制](#spending-limit)以避免您的訂用帳戶非預期地被停用。</span><span class="sxs-lookup"><span data-stu-id="01c38-114">If your subscription is a Free Trial, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO), or BizSpark, then learn about [spending limits](#spending-limit) to avoid having your subscription unexpectantly disabled.</span></span> 

## <a name="day-0-before-you-add-azure-services"></a><span data-ttu-id="01c38-115">第 0 天︰新增 Azure 服務之前</span><span class="sxs-lookup"><span data-stu-id="01c38-115">Day 0: Before you add Azure services</span></span>

### <a name="estimate-cost-online-using-the-pricing-calculator"></a><span data-ttu-id="01c38-116">使用價格計算機在線上評估成本</span><span class="sxs-lookup"><span data-stu-id="01c38-116">Estimate cost online using the pricing calculator</span></span>

<span data-ttu-id="01c38-117">查看[價格計算機](https://azure.microsoft.com/pricing/calculator/)和[擁有權總成本計算機 (英文)](https://aka.ms/azure-tco-calculator) 即可取得您感興趣的服務每月成本評估。</span><span class="sxs-lookup"><span data-stu-id="01c38-117">Check out the [pricing calculator](https://azure.microsoft.com/pricing/calculator/) and [total cost of ownership calculator](https://aka.ms/azure-tco-calculator) to get an estimate the monthly cost of the service you're interested in.</span></span> <span data-ttu-id="01c38-118">例如，如果您讓 A1 Windows 虛擬機器 (VM) 持續運作，則運算時間的預估成本為每月 $66.96 美元：</span><span class="sxs-lookup"><span data-stu-id="01c38-118">For example, an A1 Windows Virtual Machine (VM) is estimated to cost $66.96 USD/month in compute hours if you leave it running the whole time:</span></span>

![價格計算機的螢幕擷取畫面，顯示 A1 Windows 虛擬機器的每月預估成本為 $66.96 美元](./media/billing-getting-started/pricing-calcVM.png)

<span data-ttu-id="01c38-120">如需詳細資訊，請參閱[ 購買常見問題集](https://azure.microsoft.com/pricing/faq/)。</span><span class="sxs-lookup"><span data-stu-id="01c38-120">For more information, see [pricing FAQ](https://azure.microsoft.com/pricing/faq/).</span></span> <span data-ttu-id="01c38-121">或者，如果您想要與服務人員聯絡，請撥打 1-800-867-1389。</span><span class="sxs-lookup"><span data-stu-id="01c38-121">Or if you want to talk to a person, call 1-800-867-1389.</span></span>

### <a name="check-your-subscription-and-access"></a><span data-ttu-id="01c38-122">檢查訂用帳戶和存取權</span><span class="sxs-lookup"><span data-stu-id="01c38-122">Check your subscription and access</span></span>

<span data-ttu-id="01c38-123">檢視成本需要[訂用帳戶層級的計費資訊存取權](billing-manage-access.md)，但只有帳戶管理員可以存取[帳戶中心](https://account.windowsazure.com/Home/Index)、變更計費資訊，以及管理訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="01c38-123">Viewing costs require [subscriptions-level access to billing information](billing-manage-access.md), but only the Account admin can access the [Account Center](https://account.windowsazure.com/Home/Index), change billing info, and manage subscriptions.</span></span> <span data-ttu-id="01c38-124">帳戶管理員是完成註冊程序的人員。</span><span class="sxs-lookup"><span data-stu-id="01c38-124">The Account admin is the person who went through the sign-up process.</span></span> <span data-ttu-id="01c38-125">如需詳細資訊，請參閱[新增或變更管理訂用帳戶或服務的 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-125">For more information, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="01c38-126">若要查看您是否為帳戶管理員，請前往 [Azure 入口網站中的訂用帳戶刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)並查看您具有存取權的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="01c38-126">To see if you're the Account admin, go to the [Subscriptions blade in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and look at the list of subscriptions you have access to.</span></span> <span data-ttu-id="01c38-127">查看 [我的角色] 底下。</span><span class="sxs-lookup"><span data-stu-id="01c38-127">Look under **My Role**.</span></span> <span data-ttu-id="01c38-128">如果它顯示*帳戶管理員*，那麼您就是帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="01c38-128">If it says *Account admin*, then you're ok.</span></span> <span data-ttu-id="01c38-129">如果它顯示諸如*擁有者*之類的其他角色，則表示您沒有完整權限。</span><span class="sxs-lookup"><span data-stu-id="01c38-129">If it says something else like *Owner*, then you don't have full privileges.</span></span>

![Azure 入口網站的訂用帳戶檢視中您的角色的螢幕擷取畫面](./media/billing-getting-started/sub-blade-view.PNG)

<span data-ttu-id="01c38-131">如果您不是帳戶管理員，則表示有人可能透過 [Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md) (RBAC) 授與您部分存取權。</span><span class="sxs-lookup"><span data-stu-id="01c38-131">If you're not the Account admin, then somebody probably gave you partial access via [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md) (RBAC).</span></span> <span data-ttu-id="01c38-132">若要管理訂用帳戶及變更帳單資訊，請[找到帳戶管理員](billing-subscription-transfer.md#whoisaa)，並要求他們執行工作或[將訂用帳戶轉移給您](billing-subscription-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-132">To manage subscriptions and change billing info, [find the Account admin](billing-subscription-transfer.md#whoisaa) and ask them to perform the tasks or [transfer the subscription to you](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="01c38-133">如果您的帳戶系統管理員已不在您組織，而您需要管理帳單，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="01c38-133">If your Account admin is no longer with your organization and you need to manage billing, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> 

### <span data-ttu-id="01c38-134"><a name="spending-limit"></a> 檢查您是否開啟消費限制</span><span class="sxs-lookup"><span data-stu-id="01c38-134"><a name="spending-limit"></a> Check if you have a spending limit on</span></span>

<span data-ttu-id="01c38-135">如果您有使用信用額度的訂用帳戶，那麼您的消費限制依預設是開啟的。</span><span class="sxs-lookup"><span data-stu-id="01c38-135">If you have a subscription that uses credits, then the spending limit is turned on for you by default.</span></span> <span data-ttu-id="01c38-136">如此一來，當您花光您的信用額度時，就不會針對您的信用卡收費。</span><span class="sxs-lookup"><span data-stu-id="01c38-136">This way, when you spend all your credits, your credit card doesn't get charged.</span></span> <span data-ttu-id="01c38-137">請參閱 [Azure 優惠完整清單及消費限制可用性](https://azure.microsoft.com/support/legal/offer-details/)。</span><span class="sxs-lookup"><span data-stu-id="01c38-137">See the [full list of Azure offers and the availability of spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

<span data-ttu-id="01c38-138">不過，如果您達到消費限制，就會停用您的服務。</span><span class="sxs-lookup"><span data-stu-id="01c38-138">However, if you hit your spending limit, your services get disabled.</span></span> <span data-ttu-id="01c38-139">這表示您的 VM 會被解除配置。</span><span class="sxs-lookup"><span data-stu-id="01c38-139">That means your VMs are deallocated.</span></span> <span data-ttu-id="01c38-140">若要避免服務停機，您必須關閉消費限制。</span><span class="sxs-lookup"><span data-stu-id="01c38-140">To avoid service downtime, you must turn off the spending limit.</span></span> <span data-ttu-id="01c38-141">任何超額部分都會用您在檔案上的信用卡收費。</span><span class="sxs-lookup"><span data-stu-id="01c38-141">Any overage gets charged onto your credit card on file.</span></span> 

<span data-ttu-id="01c38-142">若要查看您是否已開啟消費限制，請移至[帳戶中心的訂用帳戶檢視](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="01c38-142">To see if you've got spending limit on, go to the [Subscriptions view in the Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="01c38-143">如果您的消費限制是開啟的，則會出現橫幅︰</span><span class="sxs-lookup"><span data-stu-id="01c38-143">A banner appears if your spending limit is on:</span></span>

![顯示帳戶中心已開啟消費限制的警告的螢幕擷取畫面](./media/billing-getting-started/spending-limit-banner.PNG)

<span data-ttu-id="01c38-145">按一下橫幅並遵循提示，即可移除消費限制。</span><span class="sxs-lookup"><span data-stu-id="01c38-145">Click the banner and follow prompts to remove the spending limit.</span></span> <span data-ttu-id="01c38-146">如果您在註冊時未輸入信用卡資訊，則必須輸入信用卡資訊，才能移除消費限制。</span><span class="sxs-lookup"><span data-stu-id="01c38-146">If you didn't enter credit card information when you signed up, you must enter it to remove the spending limit.</span></span> <span data-ttu-id="01c38-147">如需詳細資訊，請參閱 [Azure 消費限制 - 運作方式以及啟用或移除方法](https://azure.microsoft.com/pricing/spending-limits/)。</span><span class="sxs-lookup"><span data-stu-id="01c38-147">For more information, see [Azure spending limit – How it works and how to enable or remove it](https://azure.microsoft.com/pricing/spending-limits/).</span></span>

### <a name="set-up-billing-alerts"></a><span data-ttu-id="01c38-148">設定帳務警示</span><span class="sxs-lookup"><span data-stu-id="01c38-148">Set up billing alerts</span></span>

<span data-ttu-id="01c38-149">設定帳務警示，以便在使用成本超過您指定的金額時，收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="01c38-149">Set up billing alerts to get emails when your usage costs exceed an amount that you specify.</span></span> <span data-ttu-id="01c38-150">如果您有每月信用額度，請依照您設定指定金額時的額度設定警示。</span><span class="sxs-lookup"><span data-stu-id="01c38-150">If you have monthly credits, set up alerts for when you use up a specified amount.</span></span> <span data-ttu-id="01c38-151">如需詳細資訊，請參閱[為您的 Microsoft Azure 訂用帳戶設定帳單通知](billing-set-up-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-151">For more information, see [Set up billing alerts for your Microsoft Azure subscriptions](billing-set-up-alerts.md).</span></span>

![帳務警示電子郵件的螢幕擷取畫面](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> <span data-ttu-id="01c38-153">這項功能是仍處於預覽狀態，因此您應該定期檢查您的使用量。</span><span class="sxs-lookup"><span data-stu-id="01c38-153">This feature is still in preview so you should check your usage regularly.</span></span>

<span data-ttu-id="01c38-154">您可能需要使用價格計算機的成本估計當作您第一個警示的指導方針。</span><span class="sxs-lookup"><span data-stu-id="01c38-154">You might want to use the cost estimate from the pricing calculator as a guideline for your first alert.</span></span>

### <a name="understand-limits-and-quotas-for-your-subscription"></a><span data-ttu-id="01c38-155">了解您訂用帳戶的限制和配額</span><span class="sxs-lookup"><span data-stu-id="01c38-155">Understand limits and quotas for your subscription</span></span>

<span data-ttu-id="01c38-156">每個訂用帳戶都有針對各種項目 (例如 CPU 核心數目和 IP 位址) 的預設限制。</span><span class="sxs-lookup"><span data-stu-id="01c38-156">There are default limits to each subscription for things like the number of CPU cores and IP addresses.</span></span> <span data-ttu-id="01c38-157">務必留意這些限制。</span><span class="sxs-lookup"><span data-stu-id="01c38-157">Be mindful of these limits.</span></span> <span data-ttu-id="01c38-158">如需詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-158">For more information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="01c38-159">您可以 [連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)，要求提高您的限制或配額。</span><span class="sxs-lookup"><span data-stu-id="01c38-159">You can request an increase to your limit or quota by [contacting support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="day-1-as-you-add-services"></a><span data-ttu-id="01c38-160">第 1 天：當您新增服務時</span><span class="sxs-lookup"><span data-stu-id="01c38-160">Day 1: As you add services</span></span>

### <a name="review-the-estimated-cost-in-the-portal"></a><span data-ttu-id="01c38-161">在入口網站中檢閱預估成本</span><span class="sxs-lookup"><span data-stu-id="01c38-161">Review the estimated cost in the portal</span></span>

<span data-ttu-id="01c38-162">一般而言，當您在 Azure 入口網站中新增服務時，會有一個檢視向您顯示類似的每月預估成本。</span><span class="sxs-lookup"><span data-stu-id="01c38-162">Typically when you add a service in the Azure portal, there's a view that shows you a similar estimated cost per month.</span></span> <span data-ttu-id="01c38-163">例如，當您選擇 Windows VM 的大小時，會看到計算時數的預估每月成本：</span><span class="sxs-lookup"><span data-stu-id="01c38-163">For example, when you choose the size of your Windows VM you see the estimated monthly cost for the compute hours:</span></span>

![範例︰A1 Windows VM 預估每月成本為 $66.96 美元](./media/billing-getting-started/vm-size-cost.PNG)

### <span data-ttu-id="01c38-165"><a name="tags"></a> 將標記新增至您的資源以便將計費資料分組</span><span class="sxs-lookup"><span data-stu-id="01c38-165"><a name="tags"></a> Add tags to your resources to group your billing data</span></span>

<span data-ttu-id="01c38-166">針對支援的服務，您可以使用標記來將您的計費資料分組。</span><span class="sxs-lookup"><span data-stu-id="01c38-166">You can use tags to group billing data for supported services.</span></span> <span data-ttu-id="01c38-167">例如，如果您有不同小組執行數個 VM，您可以使用標記，依照成本中心 (HR、行銷、財務) 或環境 (生產環境、預先生產環境、測試) 來將成本分類。</span><span class="sxs-lookup"><span data-stu-id="01c38-167">For example, if you run several VMs for different teams, then you can use tags to categorize costs by cost center (HR, marketing, finance) or environment (production, pre-production, test).</span></span> 

![顯示在入口網站中設定標籤的螢幕擷取畫面](./media/billing-getting-started/tags.PNG)

<span data-ttu-id="01c38-169">這些標記會顯示在不同的成本報告檢視中。</span><span class="sxs-lookup"><span data-stu-id="01c38-169">The tags show up throughout different cost reporting views.</span></span> <span data-ttu-id="01c38-170">例如，它們會立即顯示您的[成本分析檢視](#costs)，並在第一次計費期間之後，顯示[詳細使用量.csv](#invoice-and-usage)。</span><span class="sxs-lookup"><span data-stu-id="01c38-170">For example, they're visible in your [cost analysis view](#costs) right away and [detail usage .csv](#invoice-and-usage) after your first billing period.</span></span>

<span data-ttu-id="01c38-171">如需詳細資訊，請參閱 [使用標記組織您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-171">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a><span data-ttu-id="01c38-172">請考慮啟用成本削減功能，例如 VM 自動關機</span><span class="sxs-lookup"><span data-stu-id="01c38-172">Consider enabling cost-cutting features like auto-shutdown for VMs</span></span>

<span data-ttu-id="01c38-173">根據您的案例，您可以在 Azure 入口網站中設定 VM 自動關機。</span><span class="sxs-lookup"><span data-stu-id="01c38-173">Depending on your scenario, you could configure auto-shutdown for your VMs in the Azure portal.</span></span> <span data-ttu-id="01c38-174">如需詳細資訊，請參閱[使用 Azure Resource Manager 的 VM 自動關機 (英文)](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)。</span><span class="sxs-lookup"><span data-stu-id="01c38-174">For more information, see [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![在入口網站的自動關機選項的螢幕擷取畫面](./media/billing-getting-started/auto-shutdown.PNG)

<span data-ttu-id="01c38-176">自動關機與您在 VM 中使用電源選項關閉不一樣。</span><span class="sxs-lookup"><span data-stu-id="01c38-176">Auto-shutdown isn't the same as when you shut down within the VM with power options.</span></span> <span data-ttu-id="01c38-177">自動關機會停止並解除配置您的 VM，以便停止額外的使用費用。</span><span class="sxs-lookup"><span data-stu-id="01c38-177">Auto-shutdown stops and deallocates your VMs to stop additional usage charges.</span></span> <span data-ttu-id="01c38-178">如需詳細資訊，請參閱 [Linux VM](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) 的定價常見問題，以及 [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)有關 VM 的狀態。</span><span class="sxs-lookup"><span data-stu-id="01c38-178">For more information, see pricing FAQ for [Linux VMs](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) about VM states.</span></span>

<span data-ttu-id="01c38-179">如需更多針對開發和測試環境的成本削減功能，請參閱 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/)。</span><span class="sxs-lookup"><span data-stu-id="01c38-179">For more cost-cutting features for your development and test environments, check out [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).</span></span>

## <span data-ttu-id="01c38-180"><a name="cost-reporting"></a> 第 2 天以後：使用服務之後，檢視使用量</span><span class="sxs-lookup"><span data-stu-id="01c38-180"><a name="cost-reporting"></a> Day 2+: After using services, view usage</span></span>

### <span data-ttu-id="01c38-181"><a name="costs"></a>定期查看入口網站以了解成本細分和完工速率</span><span class="sxs-lookup"><span data-stu-id="01c38-181"><a name="costs"></a> Regularly check the portal for cost breakdown and burn rate</span></span>

<span data-ttu-id="01c38-182">在您的服務開始執行之後，請定期檢查它們花了您多少錢。</span><span class="sxs-lookup"><span data-stu-id="01c38-182">After you get your services running, regularly check how much they're costing you.</span></span> <span data-ttu-id="01c38-183">您可以在 Azure 入口網站中看到目前的花費和完工速率。</span><span class="sxs-lookup"><span data-stu-id="01c38-183">You can see the current spend and burn rate in Azure portal.</span></span> 

1. <span data-ttu-id="01c38-184">請瀏覽 [Azure 入口網站中的訂用帳戶刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)。</span><span class="sxs-lookup"><span data-stu-id="01c38-184">Visit the [Subscriptions blade in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

2. <span data-ttu-id="01c38-185">選取您要檢視的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="01c38-185">Select your subscription you want to see.</span></span> <span data-ttu-id="01c38-186">您可能只有一個訂用帳戶可選取。</span><span class="sxs-lookup"><span data-stu-id="01c38-186">You might only have one to select.</span></span>

3. <span data-ttu-id="01c38-187">您應該會在快顯刀鋒視窗中看到成本細分和完工速率。</span><span class="sxs-lookup"><span data-stu-id="01c38-187">You should see the cost breakdown and burn rate in the popup blade.</span></span> <span data-ttu-id="01c38-188">您的優惠可能不受支援 (靠近頂端處會顯示警告)。</span><span class="sxs-lookup"><span data-stu-id="01c38-188">It may not be supported for your offer (a warning would be displayed near the top).</span></span> <span data-ttu-id="01c38-189">新增服務之後，請等候 24 小時以便資料填入。</span><span class="sxs-lookup"><span data-stu-id="01c38-189">Wait 24 hours after you add a service for the data to populate.</span></span>
    
    ![Azure 入口網站中完工速率和成本細分的螢幕擷取畫面](./media/billing-getting-started/burn-rate.PNG)

4. <span data-ttu-id="01c38-191">您可以將檢視釘選到您的儀表板。</span><span class="sxs-lookup"><span data-stu-id="01c38-191">You might want to pin the view to your dashboard.</span></span>

    ![將檢視釘選到儀表板的螢幕擷取畫面](./media/billing-getting-started/pin.PNG)

5. <span data-ttu-id="01c38-193">按一下左側清單中的 [成本分析]，可依照資源檢視成本細分。</span><span class="sxs-lookup"><span data-stu-id="01c38-193">Click **Cost analysis** in the list to the left to see the cost breakdown by resource.</span></span>

    ![Azure 入口網站中成本分析檢視的螢幕擷取畫面](./media/billing-getting-started/cost-analysis.PNG)

6. <span data-ttu-id="01c38-195">您可以依照不同屬性來篩選，例如[標記](#tags)資源群組和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="01c38-195">You can filter by different properties like [tags](#tags), resource group, and timespan.</span></span> <span data-ttu-id="01c38-196">按一下 [套用] 確認篩選器，按一下 [下載] 可將檢視匯出至逗號分隔值 (.csv) 檔案。</span><span class="sxs-lookup"><span data-stu-id="01c38-196">Click **Apply** to confirm the filters and **Download** to export the view to a Comma-Separated Values (.csv) file.</span></span>

7. <span data-ttu-id="01c38-197">按一下資源可查看消費歷程記錄，以及它每天花您多少錢。</span><span class="sxs-lookup"><span data-stu-id="01c38-197">Click a resource to see spend history and how much it was costing you each day.</span></span>

    ![Azure 入口網站中消費歷程記錄檢視的螢幕擷取畫面](./media/billing-getting-started/costhistory.PNG)

<span data-ttu-id="01c38-199">我們建議您將您看到的成本與您在選取服務時看到的預估進行核對。</span><span class="sxs-lookup"><span data-stu-id="01c38-199">We recommend that you check the costs you see with the estimates you saw when you selected the services.</span></span> <span data-ttu-id="01c38-200">如果成本和預估的差異很大，請再次檢查您為您的資源選取的定價方案 (例如 A1 與 A0 VM)。</span><span class="sxs-lookup"><span data-stu-id="01c38-200">If the costs wildly differ from estimates, double check the pricing plan (A1 vs A0 VM, for example) that you've selected for your resources.</span></span> 

#### <a name="view-costs-for-all-your-subscriptions-in-the-billing-blade"></a><span data-ttu-id="01c38-201">在帳單刀鋒視窗中檢視所有訂用帳戶的成本</span><span class="sxs-lookup"><span data-stu-id="01c38-201">View costs for all your subscriptions in the Billing blade</span></span>

<span data-ttu-id="01c38-202">如果您以帳戶系統管理員身分管理多個訂用帳戶，您可以在[帳單刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade)中看到您所有訂用帳戶的彙總帳單金額和細分。</span><span class="sxs-lookup"><span data-stu-id="01c38-202">If you manage multiple subscriptions as the Account admin, you can see the aggregate bill amount and breakdown for all your subscriptions in the [Billing blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade).</span></span> 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a><span data-ttu-id="01c38-203">開啟並查看 Azure 建議程式的建議</span><span class="sxs-lookup"><span data-stu-id="01c38-203">Turn on and check out Azure Advisor recommendations</span></span>

<span data-ttu-id="01c38-204">[Azure 建議程式](../advisor/advisor-overview.md)是一項預覽功能，可協助您藉由找出低使用率的資源，來降低成本。</span><span class="sxs-lookup"><span data-stu-id="01c38-204">[Azure Advisor](../advisor/advisor-overview.md) is a preview feature that helps you reduce costs by identifying resources with low usage.</span></span> <span data-ttu-id="01c38-205">在 Azure 入口網站中將它開啟：</span><span class="sxs-lookup"><span data-stu-id="01c38-205">Turn it on in the Azure portal:</span></span>

![Azure 入口網站中 Azure 建議程式按鈕的螢幕擷取畫面](./media/billing-getting-started/advisor-button.PNG)

<span data-ttu-id="01c38-207">然後，您可以從 [建議程式] 儀表板中的 [成本] 索引標籤取得可操作的建議：</span><span class="sxs-lookup"><span data-stu-id="01c38-207">Then, you can get actionable recommendations in the **Cost** tab in the Advisor dashboard:</span></span>

![建議程式的成本建議範例的螢幕擷取畫面](./media/billing-getting-started/advisor-action.PNG)

<span data-ttu-id="01c38-209">如需詳細資訊，請參閱[建議程式成本建議](../advisor/advisor-cost-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-209">For more information, see [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

### <span data-ttu-id="01c38-210"><a name="invoice-and-usage"></a>在您第一次計費期間之後取發票和詳細使用量</span><span class="sxs-lookup"><span data-stu-id="01c38-210"><a name="invoice-and-usage"></a> Get your invoice and detail usage after your first billing period</span></span>

<span data-ttu-id="01c38-211">在第一次計費期間之後，您可以下載您的可攜式文件格式 (.pdf) 發票和逗號分隔值 (.csv) 使用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="01c38-211">After your first billing period, you can download your Portable Document Format (.pdf) invoice and Comma-Separated Values (.csv) usage details.</span></span> <span data-ttu-id="01c38-212">您也可以選擇加入以便透過電子郵件收取發票。</span><span class="sxs-lookup"><span data-stu-id="01c38-212">You can also opt in to have your invoice emailed to you.</span></span> <span data-ttu-id="01c38-213">這些檔案可協助了解您在稅金、折扣和信用額度之後的最終計費是多少。</span><span class="sxs-lookup"><span data-stu-id="01c38-213">These files help to understand what is ultimately billed to you after tax, discounts, and credits.</span></span> <span data-ttu-id="01c38-214">如果您的訂用帳戶沒有連結付款方法，則您可能無法使用這些檔案。</span><span class="sxs-lookup"><span data-stu-id="01c38-214">If you didn't have a payment method attached to your subscription, these files might be unavailable for you.</span></span> <span data-ttu-id="01c38-215">如需詳細資訊，請參閱[如何取得您的 Azure 帳單寄送發票和每日使用量資料](billing-download-azure-invoice-daily-usage-date.md)和[了解 Microsoft Azure 帳單](billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-215">For more information, see [How to get your Azure billing invoice and daily usage data](billing-download-azure-invoice-daily-usage-date.md) and [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

![.pdf 發票的螢幕擷取畫面](./media/billing-getting-started/invoice.png)

<span data-ttu-id="01c38-217">您先前設定的標記會顯示在詳細使用量 .csv 檔案中︰</span><span class="sxs-lookup"><span data-stu-id="01c38-217">The tags that you set earlier show up in the detail usage .csv files:</span></span>

![在使用量 .csv 中顯示標記的螢幕擷取畫面](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a><span data-ttu-id="01c38-219">計費 API</span><span class="sxs-lookup"><span data-stu-id="01c38-219">Billing API</span></span>

<span data-ttu-id="01c38-220">使用我們的計費 API 可以用程式設計方式取得使用量資料。</span><span class="sxs-lookup"><span data-stu-id="01c38-220">Use our billing API to programmatically get usage data.</span></span> <span data-ttu-id="01c38-221">RateCard API 與使用情況 API 一起使用即可取得您的計費使用量。</span><span class="sxs-lookup"><span data-stu-id="01c38-221">Use the RateCard API and the Usage API together to get your billed usage.</span></span> <span data-ttu-id="01c38-222">如需詳細資訊，請參閱[深入瞭解 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="01c38-222">For more information, see [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md).</span></span>

## <span data-ttu-id="01c38-223"><a name="other-offers"></a> 適用於 EA、CSP 和贊助的其他資源</span><span class="sxs-lookup"><span data-stu-id="01c38-223"><a name="other-offers"></a> Additional resources for EA, CSP, and Sponsorship</span></span>

<span data-ttu-id="01c38-224">若要開始使用，請連絡帳戶管理員或 Azure 。</span><span class="sxs-lookup"><span data-stu-id="01c38-224">Talk to your account manager or Azure partner to get started.</span></span>

| <span data-ttu-id="01c38-225">提供項目</span><span class="sxs-lookup"><span data-stu-id="01c38-225">Offer</span></span> | <span data-ttu-id="01c38-226">資源</span><span class="sxs-lookup"><span data-stu-id="01c38-226">Resources</span></span> |
|-------------------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="01c38-227">Enterprise 合約 (EA)</span><span class="sxs-lookup"><span data-stu-id="01c38-227">Enterprise Agreement (EA)</span></span> | <span data-ttu-id="01c38-228">[EA 入口網站](https://ea.azure.com/)、[協助文件](https://ea.azure.com/helpdocs)和 [Power BI 報告](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span><span class="sxs-lookup"><span data-stu-id="01c38-228">[EA portal](https://ea.azure.com/), [help docs](https://ea.azure.com/helpdocs), and [Power BI report](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span></span> |
| <span data-ttu-id="01c38-229">雲端解決方案提供者 (CSP)</span><span class="sxs-lookup"><span data-stu-id="01c38-229">Cloud Solution Provider (CSP)</span></span> | <span data-ttu-id="01c38-230">與您的提供者討論</span><span class="sxs-lookup"><span data-stu-id="01c38-230">Talk to your provider</span></span> |
| <span data-ttu-id="01c38-231">Azure 贊助</span><span class="sxs-lookup"><span data-stu-id="01c38-231">Azure Sponsorship</span></span> | [<span data-ttu-id="01c38-232">贊助入口網站 (英文)</span><span class="sxs-lookup"><span data-stu-id="01c38-232">Sponsorship portal</span></span>](https://www.microsoftazuresponsorships.com/) |

<span data-ttu-id="01c38-233">如果您管理的是大型組織的 IT，我們建議您閱讀 [Azure 企業 Scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) 和[企業 IT 技術白皮書](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf 下載，僅提供英文版)。</span><span class="sxs-lookup"><span data-stu-id="01c38-233">If you're managing IT for a large organization, we recommend reading [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) and the [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf download, English only).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="01c38-234">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="01c38-234">Need help?</span></span> <span data-ttu-id="01c38-235">請連絡支援人員</span><span class="sxs-lookup"><span data-stu-id="01c38-235">Contact support</span></span>

<span data-ttu-id="01c38-236">如果需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="01c38-236">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
