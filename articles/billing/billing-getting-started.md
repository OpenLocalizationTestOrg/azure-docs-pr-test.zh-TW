---
title: "aaaPrevent 未預期的成本，管理帳單-Azure |Microsoft 文件"
description: "深入了解如何 tooavoid 未預期的費用，在 Azure 帳單上。 使用 Microsoft Azure 訂用帳戶的成本追蹤與管理功能。"
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
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a><span data-ttu-id="2d1f0-104">使用 Azure 計費與成本管理避免非預期的成本</span><span class="sxs-lookup"><span data-stu-id="2d1f0-104">Prevent unexpected costs with Azure billing and cost management</span></span>

<span data-ttu-id="2d1f0-105">當您註冊 Azure 」 時，有幾件事，您可以 tooget 了解您的消費效能。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-105">When you sign up for Azure, there are several things you can do tooget a better idea of your spend.</span></span> <span data-ttu-id="2d1f0-106">在 hello [Azure 入口網站](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)，當您選取 hello 訂用帳戶，您可以查看目前的成本明細和完工速率。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-106">In hello [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), when you select hello subscription, you can see your current cost breakdown and burn rate.</span></span> <span data-ttu-id="2d1f0-107">您也可以[下載之前的發票與詳細使用量檔案](billing-download-azure-invoice-daily-usage-date.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-107">You can also [download past invoices and detail usage files](billing-download-azure-invoice-daily-usage-date.md).</span></span> <span data-ttu-id="2d1f0-108">如果您想要使用不同的專案或小組資源 toogroup 成本，查看[資源標記](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-108">If you want toogroup costs for resources used for different projects or teams, look at [resource tagging](../azure-resource-manager/resource-group-using-tags.md).</span></span> <span data-ttu-id="2d1f0-109">如果您的組織有您喜歡 toouse 報告系統，請參閱 hello[計費 Api](billing-usage-rate-card-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-109">If your organization has a reporting system that you prefer toouse, check out hello [billing APIs](billing-usage-rate-card-overview.md).</span></span> 

<span data-ttu-id="2d1f0-110">如需每日使用量的詳細資訊，請參閱[了解 Microsoft Azure 帳單](billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-110">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

<span data-ttu-id="2d1f0-111">如果您的訂閱是透過 Enterprise 合約 (EA)、 雲端方案提供者 (CSP) 或 Azure 發起者，這篇文章中的許多功能不適用 tooyou。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-111">If your subscription is through an Enterprise Agreement (EA), Cloud Solution Provider (CSP), or Azure Sponsorship, then many features in this article don't apply tooyou.</span></span> <span data-ttu-id="2d1f0-112">反之，我們有不同的工具組，可供您用於成本管理。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-112">Instead, we have a different set of tools that you can use for cost management.</span></span> <span data-ttu-id="2d1f0-113">請參閱[適用於 EA、CSP 和贊助的其他資源](#other-offers)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-113">See [Additional resources for EA, CSP, and Sponsorship](#other-offers).</span></span>

<span data-ttu-id="2d1f0-114">如果您的訂閱是免費的試用版， [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，Azure 中開啟 (AIO) 或 BizSpark，深入了解[消費限制](#spending-limit)tooavoid 具有 unexpectantly 停用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-114">If your subscription is a Free Trial, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO), or BizSpark, then learn about [spending limits](#spending-limit) tooavoid having your subscription unexpectantly disabled.</span></span> 

## <a name="day-0-before-you-add-azure-services"></a><span data-ttu-id="2d1f0-115">第 0 天︰新增 Azure 服務之前</span><span class="sxs-lookup"><span data-stu-id="2d1f0-115">Day 0: Before you add Azure services</span></span>

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a><span data-ttu-id="2d1f0-116">估計成本線上使用 hello 定價計算機</span><span class="sxs-lookup"><span data-stu-id="2d1f0-116">Estimate cost online using hello pricing calculator</span></span>

<span data-ttu-id="2d1f0-117">簽出 hello[定價計算機](https://azure.microsoft.com/pricing/calculator/)和[總成本的擁有權 [小算盤]](https://aka.ms/azure-tco-calculator) tooget hello 服務您感興趣的估計 hello 每月成本。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-117">Check out hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/) and [total cost of ownership calculator](https://aka.ms/azure-tco-calculator) tooget an estimate hello monthly cost of hello service you're interested in.</span></span> <span data-ttu-id="2d1f0-118">例如，A1 Windows 虛擬機器 (VM) 會是估計的 toocost $66.96 美元/月中時數計算您讓它執行 hello 整個時間：</span><span class="sxs-lookup"><span data-stu-id="2d1f0-118">For example, an A1 Windows Virtual Machine (VM) is estimated toocost $66.96 USD/month in compute hours if you leave it running hello whole time:</span></span>

![顯示 A1 Windows VM 每個月的預估的 toocost $66.96 USD hello 定價計算機的螢幕擷取畫面](./media/billing-getting-started/pricing-calcVM.png)

<span data-ttu-id="2d1f0-120">如需詳細資訊，請參閱[ 購買常見問題集](https://azure.microsoft.com/pricing/faq/)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-120">For more information, see [pricing FAQ](https://azure.microsoft.com/pricing/faq/).</span></span> <span data-ttu-id="2d1f0-121">或如果您想 tootalk tooa 人員，請呼叫 1-800-867-1389。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-121">Or if you want tootalk tooa person, call 1-800-867-1389.</span></span>

### <a name="check-your-subscription-and-access"></a><span data-ttu-id="2d1f0-122">檢查訂用帳戶和存取權</span><span class="sxs-lookup"><span data-stu-id="2d1f0-122">Check your subscription and access</span></span>

<span data-ttu-id="2d1f0-123">需要檢視成本[訂用帳戶層級存取 toobilling 資訊](billing-manage-access.md)，但是 hello 帳戶管理員可以存取 hello[帳戶中心](https://account.windowsazure.com/Home/Index)、 變更計費資訊，以及管理訂閱。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-123">Viewing costs require [subscriptions-level access toobilling information](billing-manage-access.md), but only hello Account admin can access hello [Account Center](https://account.windowsazure.com/Home/Index), change billing info, and manage subscriptions.</span></span> <span data-ttu-id="2d1f0-124">hello 帳戶管理員 hello 的人物是誰從頭到尾 hello 註冊程序。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-124">hello Account admin is hello person who went through hello sign-up process.</span></span> <span data-ttu-id="2d1f0-125">如需詳細資訊，請參閱[hello 訂用帳戶或服務管理的新增或變更 Azure 系統管理員角色](billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-125">For more information, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="2d1f0-126">toosee 如果您正在 hello 帳戶系統管理員，請移至 toohello [hello Azure 入口網站中的訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)並查看 hello 您具有存取權的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-126">toosee if you're hello Account admin, go toohello [Subscriptions blade in hello Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and look at hello list of subscriptions you have access to.</span></span> <span data-ttu-id="2d1f0-127">查看 [我的角色] 底下。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-127">Look under **My Role**.</span></span> <span data-ttu-id="2d1f0-128">如果它顯示*帳戶管理員*，那麼您就是帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-128">If it says *Account admin*, then you're ok.</span></span> <span data-ttu-id="2d1f0-129">如果它顯示諸如*擁有者*之類的其他角色，則表示您沒有完整權限。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-129">If it says something else like *Owner*, then you don't have full privileges.</span></span>

![您的角色 hello hello Azure 入口網站中的訂閱檢視中的螢幕擷取畫面](./media/billing-getting-started/sub-blade-view.PNG)

<span data-ttu-id="2d1f0-131">如果您不是 hello 帳戶系統管理員，然後有人可能會讓您透過部分存取[Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)(RBAC)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-131">If you're not hello Account admin, then somebody probably gave you partial access via [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md) (RBAC).</span></span> <span data-ttu-id="2d1f0-132">toomanage 訂用帳戶和計費資訊，變更[尋找 hello 帳戶管理員](billing-subscription-transfer.md#whoisaa)並要求他們 tooperform hello 工作或[傳送嗨訂用帳戶 tooyou](billing-subscription-transfer.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-132">toomanage subscriptions and change billing info, [find hello Account admin](billing-subscription-transfer.md#whoisaa) and ask them tooperform hello tasks or [transfer hello subscription tooyou](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="2d1f0-133">如果您的帳戶管理員已不再與您的組織，您需要 toomanage 計費[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-133">If your Account admin is no longer with your organization and you need toomanage billing, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> 

### <span data-ttu-id="2d1f0-134"><a name="spending-limit"></a> 檢查您是否開啟消費限制</span><span class="sxs-lookup"><span data-stu-id="2d1f0-134"><a name="spending-limit"></a> Check if you have a spending limit on</span></span>

<span data-ttu-id="2d1f0-135">如果您有使用信用額度的訂閱，然後 hello 消費限制已為您預設。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-135">If you have a subscription that uses credits, then hello spending limit is turned on for you by default.</span></span> <span data-ttu-id="2d1f0-136">如此一來，當您花光您的信用額度時，就不會針對您的信用卡收費。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-136">This way, when you spend all your credits, your credit card doesn't get charged.</span></span> <span data-ttu-id="2d1f0-137">請參閱 hello [Azure 優惠和 hello 可用性的消費限制的完整清單](https://azure.microsoft.com/support/legal/offer-details/)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-137">See hello [full list of Azure offers and hello availability of spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

<span data-ttu-id="2d1f0-138">不過，如果您達到消費限制，就會停用您的服務。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-138">However, if you hit your spending limit, your services get disabled.</span></span> <span data-ttu-id="2d1f0-139">這表示您的 VM 會被解除配置。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-139">That means your VMs are deallocated.</span></span> <span data-ttu-id="2d1f0-140">tooavoid 服務停機時間，您必須關閉 hello 消費限制。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-140">tooavoid service downtime, you must turn off hello spending limit.</span></span> <span data-ttu-id="2d1f0-141">任何超額部分都會用您在檔案上的信用卡收費。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-141">Any overage gets charged onto your credit card on file.</span></span> 

<span data-ttu-id="2d1f0-142">如果您已經有消費限制，toosee 移 toohello [hello 帳戶中心中檢視訂閱](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-142">toosee if you've got spending limit on, go toohello [Subscriptions view in hello Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="2d1f0-143">如果您的消費限制是開啟的，則會出現橫幅︰</span><span class="sxs-lookup"><span data-stu-id="2d1f0-143">A banner appears if your spending limit is on:</span></span>

![顯示有關消費限制上處於 hello 帳戶中心的警告的螢幕擷取畫面](./media/billing-getting-started/spending-limit-banner.PNG)

<span data-ttu-id="2d1f0-145">按一下 hello 橫幅，並遵循提示 tooremove hello 消費限制。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-145">Click hello banner and follow prompts tooremove hello spending limit.</span></span> <span data-ttu-id="2d1f0-146">如果您註冊時，您未輸入信用卡資訊，您必須輸入 tooremove hello 消費限制。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-146">If you didn't enter credit card information when you signed up, you must enter it tooremove hello spending limit.</span></span> <span data-ttu-id="2d1f0-147">如需詳細資訊，請參閱[Azure 消費限制 – 如何運作以及如何 tooenable 或將它移除](https://azure.microsoft.com/pricing/spending-limits/)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-147">For more information, see [Azure spending limit – How it works and how tooenable or remove it](https://azure.microsoft.com/pricing/spending-limits/).</span></span>

### <a name="set-up-billing-alerts"></a><span data-ttu-id="2d1f0-148">設定帳務警示</span><span class="sxs-lookup"><span data-stu-id="2d1f0-148">Set up billing alerts</span></span>

<span data-ttu-id="2d1f0-149">設定計費警示 tooget 電子郵件時使用成本超過您指定的數量。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-149">Set up billing alerts tooget emails when your usage costs exceed an amount that you specify.</span></span> <span data-ttu-id="2d1f0-150">如果您有每月信用額度，請依照您設定指定金額時的額度設定警示。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-150">If you have monthly credits, set up alerts for when you use up a specified amount.</span></span> <span data-ttu-id="2d1f0-151">如需詳細資訊，請參閱[為您的 Microsoft Azure 訂用帳戶設定帳單通知](billing-set-up-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-151">For more information, see [Set up billing alerts for your Microsoft Azure subscriptions](billing-set-up-alerts.md).</span></span>

![帳務警示電子郵件的螢幕擷取畫面](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> <span data-ttu-id="2d1f0-153">這項功能是仍處於預覽狀態，因此您應該定期檢查您的使用量。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-153">This feature is still in preview so you should check your usage regularly.</span></span>

<span data-ttu-id="2d1f0-154">您可以從 hello 定價計算機為您的第一個警示的指導方針 toouse hello 成本預估值。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-154">You might want toouse hello cost estimate from hello pricing calculator as a guideline for your first alert.</span></span>

### <a name="understand-limits-and-quotas-for-your-subscription"></a><span data-ttu-id="2d1f0-155">了解您訂用帳戶的限制和配額</span><span class="sxs-lookup"><span data-stu-id="2d1f0-155">Understand limits and quotas for your subscription</span></span>

<span data-ttu-id="2d1f0-156">沒有預設限制針對 hello 的 CPU 核心數及 IP 位址等 tooeach 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-156">There are default limits tooeach subscription for things like hello number of CPU cores and IP addresses.</span></span> <span data-ttu-id="2d1f0-157">務必留意這些限制。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-157">Be mindful of these limits.</span></span> <span data-ttu-id="2d1f0-158">如需詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-158">For more information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="2d1f0-159">您可以要求增加 tooyour 限制或配額[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-159">You can request an increase tooyour limit or quota by [contacting support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="day-1-as-you-add-services"></a><span data-ttu-id="2d1f0-160">第 1 天：當您新增服務時</span><span class="sxs-lookup"><span data-stu-id="2d1f0-160">Day 1: As you add services</span></span>

### <a name="review-hello-estimated-cost-in-hello-portal"></a><span data-ttu-id="2d1f0-161">Hello 入口網站中檢閱 hello 估計成本</span><span class="sxs-lookup"><span data-stu-id="2d1f0-161">Review hello estimated cost in hello portal</span></span>

<span data-ttu-id="2d1f0-162">通常當您新增服務 hello Azure 入口網站中，是檢視，顯示類似的估計的成本，每個月。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-162">Typically when you add a service in hello Azure portal, there's a view that shows you a similar estimated cost per month.</span></span> <span data-ttu-id="2d1f0-163">例如，當您選擇的 Windows VM 的 hello 大小即 hello 預估每月成本 hello 運算時數：</span><span class="sxs-lookup"><span data-stu-id="2d1f0-163">For example, when you choose hello size of your Windows VM you see hello estimated monthly cost for hello compute hours:</span></span>

![範例： A1 Windows VM 是每個月的預估的 toocost $66.96 美元](./media/billing-getting-started/vm-size-cost.PNG)

### <span data-ttu-id="2d1f0-165"><a name="tags"></a>新增標記 tooyour 資源 toogroup 帳單資料</span><span class="sxs-lookup"><span data-stu-id="2d1f0-165"><a name="tags"></a> Add tags tooyour resources toogroup your billing data</span></span>

<span data-ttu-id="2d1f0-166">支援服務，您可以使用標記 toogroup 計費資料。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-166">You can use tags toogroup billing data for supported services.</span></span> <span data-ttu-id="2d1f0-167">例如，如果您執行數個 Vm 的不同小組，您可以使用標記 toocategorize 成本成本中心 (HR，行銷、 財務) 或環境 （生產環境中，進入生產階段前，測試）。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-167">For example, if you run several VMs for different teams, then you can use tags toocategorize costs by cost center (HR, marketing, finance) or environment (production, pre-production, test).</span></span> 

![設定標記會顯示 hello 入口網站中的螢幕擷取畫面](./media/billing-getting-started/tags.PNG)

<span data-ttu-id="2d1f0-169">hello 標記會顯示在不同的報告檢視的成本。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-169">hello tags show up throughout different cost reporting views.</span></span> <span data-ttu-id="2d1f0-170">例如，它們會立即顯示您的[成本分析檢視](#costs)，並在第一次計費期間之後，顯示[詳細使用量.csv](#invoice-and-usage)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-170">For example, they're visible in your [cost analysis view](#costs) right away and [detail usage .csv](#invoice-and-usage) after your first billing period.</span></span>

<span data-ttu-id="2d1f0-171">如需詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-171">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a><span data-ttu-id="2d1f0-172">請考慮啟用成本削減功能，例如 VM 自動關機</span><span class="sxs-lookup"><span data-stu-id="2d1f0-172">Consider enabling cost-cutting features like auto-shutdown for VMs</span></span>

<span data-ttu-id="2d1f0-173">根據您的案例中，您可以設定自動關機的 hello Azure 入口網站中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-173">Depending on your scenario, you could configure auto-shutdown for your VMs in hello Azure portal.</span></span> <span data-ttu-id="2d1f0-174">如需詳細資訊，請參閱[使用 Azure Resource Manager 的 VM 自動關機 (英文)](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-174">For more information, see [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![Hello 入口網站中的自動關閉選項的螢幕擷取畫面](./media/billing-getting-started/auto-shutdown.PNG)

<span data-ttu-id="2d1f0-176">自動關閉不 hello 與當您在關機時 hello VM 電源選項相同。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-176">Auto-shutdown isn't hello same as when you shut down within hello VM with power options.</span></span> <span data-ttu-id="2d1f0-177">自動關閉會停止並取消配置 Vm toostop 額外的使用費用。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-177">Auto-shutdown stops and deallocates your VMs toostop additional usage charges.</span></span> <span data-ttu-id="2d1f0-178">如需詳細資訊，請參閱 [Linux VM](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) 的定價常見問題，以及 [Windows VM](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)有關 VM 的狀態。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-178">For more information, see pricing FAQ for [Linux VMs](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) about VM states.</span></span>

<span data-ttu-id="2d1f0-179">如需更多針對開發和測試環境的成本削減功能，請參閱 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-179">For more cost-cutting features for your development and test environments, check out [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).</span></span>

## <span data-ttu-id="2d1f0-180"><a name="cost-reporting"></a> 第 2 天以後：使用服務之後，檢視使用量</span><span class="sxs-lookup"><span data-stu-id="2d1f0-180"><a name="cost-reporting"></a> Day 2+: After using services, view usage</span></span>

### <span data-ttu-id="2d1f0-181"><a name="costs"></a>定期檢查的成本明細 hello 入口網站和完工速率</span><span class="sxs-lookup"><span data-stu-id="2d1f0-181"><a name="costs"></a> Regularly check hello portal for cost breakdown and burn rate</span></span>

<span data-ttu-id="2d1f0-182">在您的服務開始執行之後，請定期檢查它們花了您多少錢。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-182">After you get your services running, regularly check how much they're costing you.</span></span> <span data-ttu-id="2d1f0-183">您可以看到 hello 目前支出和完工速率 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-183">You can see hello current spend and burn rate in Azure portal.</span></span> 

1. <span data-ttu-id="2d1f0-184">請瀏覽 hello [Azure 入口網站中的訂用帳戶 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-184">Visit hello [Subscriptions blade in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

2. <span data-ttu-id="2d1f0-185">選取您想要 toosee 您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-185">Select your subscription you want toosee.</span></span> <span data-ttu-id="2d1f0-186">您可能只有一個 tooselect。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-186">You might only have one tooselect.</span></span>

3. <span data-ttu-id="2d1f0-187">您應該看到 hello 成本分解和完工速率在 hello 快顯 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-187">You should see hello cost breakdown and burn rate in hello popup blade.</span></span> <span data-ttu-id="2d1f0-188">它可能不支援您的優惠 （靠近 hello 頂端會顯示一則警告）。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-188">It may not be supported for your offer (a warning would be displayed near hello top).</span></span> <span data-ttu-id="2d1f0-189">等候 24 小時之後新增 hello 資料 toopopulate 的服務。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-189">Wait 24 hours after you add a service for hello data toopopulate.</span></span>
    
    ![完工速率和分解 hello Azure 入口網站中的螢幕擷取畫面](./media/billing-getting-started/burn-rate.PNG)

4. <span data-ttu-id="2d1f0-191">您可能想 toopin hello view tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-191">You might want toopin hello view tooyour dashboard.</span></span>

    ![釘選 view toohello 儀表板的螢幕擷取畫面](./media/billing-getting-started/pin.PNG)

5. <span data-ttu-id="2d1f0-193">按一下**成本分析**hello 清單 toohello 左的 toosee hello 成本細目-依資源中。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-193">Click **Cost analysis** in hello list toohello left toosee hello cost breakdown by resource.</span></span>

    ![在 Azure 入口網站中的 hello 成本分析檢視的螢幕擷取畫面](./media/billing-getting-started/cost-analysis.PNG)

6. <span data-ttu-id="2d1f0-195">您可以依照不同屬性來篩選，例如[標記](#tags)資源群組和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-195">You can filter by different properties like [tags](#tags), resource group, and timespan.</span></span> <span data-ttu-id="2d1f0-196">按一下**套用**tooconfirm hello 篩選器和**下載**tooexport hello 檢視 tooa 逗號分隔值 (.csv) 檔案。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-196">Click **Apply** tooconfirm hello filters and **Download** tooexport hello view tooa Comma-Separated Values (.csv) file.</span></span>

7. <span data-ttu-id="2d1f0-197">按一下資源 toosee 花歷程記錄和多少它已成本您每一天。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-197">Click a resource toosee spend history and how much it was costing you each day.</span></span>

    ![花在 Azure 入口網站中的歷程記錄檢視的 hello 螢幕擷取畫面](./media/billing-getting-started/costhistory.PNG)

<span data-ttu-id="2d1f0-199">我們建議您檢查 hello 您會看到您已看到，當您選取 hello 服務的 hello 預估的成本。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-199">We recommend that you check hello costs you see with hello estimates you saw when you selected hello services.</span></span> <span data-ttu-id="2d1f0-200">如果 hello 成本末來而多半極不同估計值，請再次檢查 hello 定價方案 (A1 vs A0 VM，例如) 您已選取為您的資源。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-200">If hello costs wildly differ from estimates, double check hello pricing plan (A1 vs A0 VM, for example) that you've selected for your resources.</span></span> 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a><span data-ttu-id="2d1f0-201">檢視 hello 帳單 刀鋒視窗中所有訂用帳戶的成本</span><span class="sxs-lookup"><span data-stu-id="2d1f0-201">View costs for all your subscriptions in hello Billing blade</span></span>

<span data-ttu-id="2d1f0-202">如果因為 hello 帳戶管理員，您可以管理多個訂閱，您可以查看 hello 彙總的帳單金額和分解 hello 的全部訂閱[帳單 刀鋒視窗](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-202">If you manage multiple subscriptions as hello Account admin, you can see hello aggregate bill amount and breakdown for all your subscriptions in hello [Billing blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade).</span></span> 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a><span data-ttu-id="2d1f0-203">開啟並查看 Azure 建議程式的建議</span><span class="sxs-lookup"><span data-stu-id="2d1f0-203">Turn on and check out Azure Advisor recommendations</span></span>

<span data-ttu-id="2d1f0-204">[Azure 建議程式](../advisor/advisor-overview.md)是一項預覽功能，可協助您藉由找出低使用率的資源，來降低成本。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-204">[Azure Advisor](../advisor/advisor-overview.md) is a preview feature that helps you reduce costs by identifying resources with low usage.</span></span> <span data-ttu-id="2d1f0-205">在 hello Azure 入口網站中開啟：</span><span class="sxs-lookup"><span data-stu-id="2d1f0-205">Turn it on in hello Azure portal:</span></span>

![Azure 入口網站中 Azure 建議程式按鈕的螢幕擷取畫面](./media/billing-getting-started/advisor-button.PNG)

<span data-ttu-id="2d1f0-207">然後，您可以在 hello 取得可採取動作的建議**成本**hello Advisor 儀表板中的索引標籤：</span><span class="sxs-lookup"><span data-stu-id="2d1f0-207">Then, you can get actionable recommendations in hello **Cost** tab in hello Advisor dashboard:</span></span>

![建議程式的成本建議範例的螢幕擷取畫面](./media/billing-getting-started/advisor-action.PNG)

<span data-ttu-id="2d1f0-209">如需詳細資訊，請參閱[建議程式成本建議](../advisor/advisor-cost-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-209">For more information, see [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

### <span data-ttu-id="2d1f0-210"><a name="invoice-and-usage"></a>在您第一次計費期間之後取發票和詳細使用量</span><span class="sxs-lookup"><span data-stu-id="2d1f0-210"><a name="invoice-and-usage"></a> Get your invoice and detail usage after your first billing period</span></span>

<span data-ttu-id="2d1f0-211">在第一次計費期間之後，您可以下載您的可攜式文件格式 (.pdf) 發票和逗號分隔值 (.csv) 使用量詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-211">After your first billing period, you can download your Portable Document Format (.pdf) invoice and Comma-Separated Values (.csv) usage details.</span></span> <span data-ttu-id="2d1f0-212">您也可以選擇在 toohave 發票 tooyou 寄送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-212">You can also opt in toohave your invoice emailed tooyou.</span></span> <span data-ttu-id="2d1f0-213">這些檔案說明 toounderstand 什麼是最後使用票據的 tooyou 稅金、 折扣和信用額度之後。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-213">These files help toounderstand what is ultimately billed tooyou after tax, discounts, and credits.</span></span> <span data-ttu-id="2d1f0-214">如果您沒有付款方法附加 tooyour 訂用帳戶，這些檔案可能是您無法使用。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-214">If you didn't have a payment method attached tooyour subscription, these files might be unavailable for you.</span></span> <span data-ttu-id="2d1f0-215">如需詳細資訊，請參閱[如何 tooget 您 Azure 帳單寄送發票及每日使用量資料](billing-download-azure-invoice-daily-usage-date.md)和[Microsoft azure 了解您的帳單](billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-215">For more information, see [How tooget your Azure billing invoice and daily usage data](billing-download-azure-invoice-daily-usage-date.md) and [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

![.pdf 發票的螢幕擷取畫面](./media/billing-getting-started/invoice.png)

<span data-ttu-id="2d1f0-217">您先前設定的 hello 標記會顯示 hello 詳細使用狀況.csv 檔案中：</span><span class="sxs-lookup"><span data-stu-id="2d1f0-217">hello tags that you set earlier show up in hello detail usage .csv files:</span></span>

![顯示 hello 使用量.csv 中標記的螢幕擷取畫面](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a><span data-ttu-id="2d1f0-219">計費 API</span><span class="sxs-lookup"><span data-stu-id="2d1f0-219">Billing API</span></span>

<span data-ttu-id="2d1f0-220">使用我們計費 API tooprogrammatically get 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-220">Use our billing API tooprogrammatically get usage data.</span></span> <span data-ttu-id="2d1f0-221">使用 hello RateCard API 和 hello 使用量 API 一起 tooget 您計費的使用量。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-221">Use hello RateCard API and hello Usage API together tooget your billed usage.</span></span> <span data-ttu-id="2d1f0-222">如需詳細資訊，請參閱[深入瞭解 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-222">For more information, see [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md).</span></span>

## <span data-ttu-id="2d1f0-223"><a name="other-offers"></a> 適用於 EA、CSP 和贊助的其他資源</span><span class="sxs-lookup"><span data-stu-id="2d1f0-223"><a name="other-offers"></a> Additional resources for EA, CSP, and Sponsorship</span></span>

<span data-ttu-id="2d1f0-224">請連絡 tooyour 客戶經理或 Azure 合作夥伴 tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-224">Talk tooyour account manager or Azure partner tooget started.</span></span>

| <span data-ttu-id="2d1f0-225">提供項目</span><span class="sxs-lookup"><span data-stu-id="2d1f0-225">Offer</span></span> | <span data-ttu-id="2d1f0-226">資源</span><span class="sxs-lookup"><span data-stu-id="2d1f0-226">Resources</span></span> |
|-------------------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="2d1f0-227">Enterprise 合約 (EA)</span><span class="sxs-lookup"><span data-stu-id="2d1f0-227">Enterprise Agreement (EA)</span></span> | <span data-ttu-id="2d1f0-228">[EA 入口網站](https://ea.azure.com/)、[協助文件](https://ea.azure.com/helpdocs)和 [Power BI 報告](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span><span class="sxs-lookup"><span data-stu-id="2d1f0-228">[EA portal](https://ea.azure.com/), [help docs](https://ea.azure.com/helpdocs), and [Power BI report](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span></span> |
| <span data-ttu-id="2d1f0-229">雲端解決方案提供者 (CSP)</span><span class="sxs-lookup"><span data-stu-id="2d1f0-229">Cloud Solution Provider (CSP)</span></span> | <span data-ttu-id="2d1f0-230">Talk tooyour 提供者</span><span class="sxs-lookup"><span data-stu-id="2d1f0-230">Talk tooyour provider</span></span> |
| <span data-ttu-id="2d1f0-231">Azure 贊助</span><span class="sxs-lookup"><span data-stu-id="2d1f0-231">Azure Sponsorship</span></span> | [<span data-ttu-id="2d1f0-232">贊助入口網站 (英文)</span><span class="sxs-lookup"><span data-stu-id="2d1f0-232">Sponsorship portal</span></span>](https://www.microsoftazuresponsorships.com/) |

<span data-ttu-id="2d1f0-233">如果您管理 IT 的大型組織，建議您閱讀[Azure 企業版 scaffold](../azure-resource-manager/resource-manager-subscription-governance.md)和 hello[企業 IT 技術白皮書](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf)（.pdf 下載，僅限英文）。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-233">If you're managing IT for a large organization, we recommend reading [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) and hello [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf download, English only).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="2d1f0-234">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="2d1f0-234">Need help?</span></span> <span data-ttu-id="2d1f0-235">請連絡支援人員</span><span class="sxs-lookup"><span data-stu-id="2d1f0-235">Contact support</span></span>

<span data-ttu-id="2d1f0-236">如果您需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="2d1f0-236">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
