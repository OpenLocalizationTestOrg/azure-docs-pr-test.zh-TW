---
title: "aaaUnderstand Azure 消費限制 |Microsoft 文件"
description: "描述 Azure 消費限制的運作方式以及 tooremove 它"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a><span data-ttu-id="7f2a5-103">了解 Azure 消費限制以及如何 tooremove 它</span><span class="sxs-lookup"><span data-stu-id="7f2a5-103">Understand Azure spending limit and how tooremove it</span></span>

<span data-ttu-id="7f2a5-104">Azure 消費限制是對您 Azure 訂用帳戶消費額度的限制。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-104">Azure spending limit is a limit on how much your Azure subscription can spend.</span></span> <span data-ttu-id="7f2a5-105">所有新的客戶註冊 hello 試用供應項目或包含多個月內的信用額度的優惠擁有 hello 消費限制預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-105">All new customers who sign up for hello trial offer or offers that includes credits over multiple months have hello spending limit turned on by default.</span></span> <span data-ttu-id="7f2a5-106">hello 消費限制為 $0。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-106">hello spending limit is $0.</span></span> <span data-ttu-id="7f2a5-107">此限制無法變更。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-107">It can’t be changed.</span></span> <span data-ttu-id="7f2a5-108">hello 消費限制不適用於訂閱類型，例如隨用隨付訂用帳戶以及承諾計畫。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-108">hello spending limit isn’t available for subscription types such as Pay-As-You-Go subscriptions and commitment plans.</span></span> <span data-ttu-id="7f2a5-109">請參閱 hello [Azure 提供的消費限制的 hello hello 可用性的完整清單](https://azure.microsoft.com/support/legal/offer-details/)。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-109">See hello [full list of Azure offers and hello availability of hello spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

## <a name="what-happens-when-i-reach-hello-spending-limit"></a><span data-ttu-id="7f2a5-110">當我達到消費限制的 hello 發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="7f2a5-110">What happens when I reach hello spending limit?</span></span>

<span data-ttu-id="7f2a5-111">當您的使用方式導致耗盡 hello 每月量納入您的優惠的費用時，您部署的 hello 服務會停用該帳務月份 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-111">When your usage results in charges that exhaust hello monthly amounts included in your offer, hello services that you deployed are disabled for hello rest of that billing month.</span></span> <span data-ttu-id="7f2a5-112">舉例來說，您部署的「雲端服務」會從生產環境中移除，而 Azure 虛擬機器則會停止並解除配置。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-112">For example, Cloud Services that you deployed are removed from production and your Azure virtual machines are stopped and de-allocated.</span></span> <span data-ttu-id="7f2a5-113">tooprevent 無法停用您的服務，您可以選擇 tooremove 消費限制。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-113">tooprevent your services from being disabled, you can choose tooremove your spending limit.</span></span> <span data-ttu-id="7f2a5-114">您的服務停用時，您的儲存體帳戶和資料庫中的 hello 資料的使用。 系統管理員以唯讀方式</span><span class="sxs-lookup"><span data-stu-id="7f2a5-114">When your services are disabled, hello data in your storage accounts and databases are available in a read-only manner for administrators.</span></span> <span data-ttu-id="7f2a5-115">在 hello 開頭 hello 下一個計費月份，如果您的優惠包含透過數個月信用額度訂用帳戶將會重新啟用。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-115">At hello beginning of hello next billing month, if your offer includes credits over multiple months, your subscription will be re-enabled.</span></span> <span data-ttu-id="7f2a5-116">您可以重新部署您的雲端服務，並且具有完整存取 tooyour 儲存體帳戶和資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-116">Then you can redeploy your Cloud Services and have full access tooyour storage accounts and databases.</span></span>

<span data-ttu-id="7f2a5-117">Hello 免費的試用訂用帳戶達到消費限制的 hello 之後，您可以重新啟用 hello 訂用帳戶，並讓它自動[升級 tooour 標準隨用隨付優惠](billing-upgrade-azure-subscription.md)後 90 天內。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-117">After hello free trial subscription reaches hello spending limit, you can re-enable hello subscription and have it automatically [upgrade tooour standard Pay-As-You-Go offer](billing-upgrade-azure-subscription.md) within 90 days.</span></span>

<span data-ttu-id="7f2a5-118">當您遇到 hello 消費限制為您提供的服務時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-118">You receive notifications when you hit hello spending limit for your offer.</span></span> <span data-ttu-id="7f2a5-119">登入 toohello [Azure 帳戶中心](https://account.windowsazure.com)，選取**帳戶**，然後選取**訂閱**。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-119">Log on toohello [Azure Account Center](https://account.windowsazure.com), select **ACCOUNT**, and then select **subscriptions**.</span></span> <span data-ttu-id="7f2a5-120">您會看到有關訂用帳戶已達到消費限制的 hello 的通知。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-120">You see notifications about subscriptions that have reached hello spending limit.</span></span>

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a><span data-ttu-id="7f2a5-121">即使已啟用消費限制也需要付費的項目</span><span class="sxs-lookup"><span data-stu-id="7f2a5-121">Things you are charged for even if you have a spending limit enabled</span></span>

<span data-ttu-id="7f2a5-122">某些 Azure 服務和[Marketplace 購買](https://azure.microsoft.com/marketplace/)可以產生 hello 付款方式 (CC) 下的費用，即使已設定的消費限制。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-122">Some Azure services and [Marketplace purchases](https://azure.microsoft.com/marketplace/) can incur charges under hello payment method (CC) even if a spending limit is set.</span></span> <span data-ttu-id="7f2a5-123">範例包括 Visual studio 授權、 Azure Active Directory premium、 支援計劃和大部分第三方品牌銷售透過 hello Marketplace 的服務。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-123">Examples are Visual studio licenses, Azure Active Directory premium, support plans, and most third-party branded services sold through hello Marketplace.</span></span>


## <a name="when-not-toouse-hello-spending-limit"></a><span data-ttu-id="7f2a5-124">當不 toouse hello 消費限制</span><span class="sxs-lookup"><span data-stu-id="7f2a5-124">When not toouse hello spending limit</span></span>

<span data-ttu-id="7f2a5-125">hello 消費限制，無法讓您無法部署或使用特定的服務商場和 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-125">hello spending limit could prevent you from deploying or using certain marketplace and Microsoft services.</span></span> <span data-ttu-id="7f2a5-126">以下是您應該在此移除消費限制，您的訂用帳戶的 hello hello 案例。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-126">Here are hello scenarios where you should remove hello spending limit on your subscription.</span></span>

- <span data-ttu-id="7f2a5-127">您計劃 toodeploy 前的合作對象影像像 Oracle 和 Visual Studio Team Services 等服務。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-127">You plan toodeploy first party images like Oracle and services such as Visual Studio Team Services.</span></span> <span data-ttu-id="7f2a5-128">此案例會導致您 tooexceed 幾乎會立即您的消費限制，並會導致您的訂用帳戶 toobe 停用。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-128">This scenario causes you tooexceed your spending limit almost immediately and causes your subscription toobe disabled.</span></span>

- <span data-ttu-id="7f2a5-129">您有不可中斷的服務。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-129">You have services that cannot be disrupted.</span></span>

- <span data-ttu-id="7f2a5-130">您有服務和資源的設定，例如虛擬 IP 位址，您不想 toolose。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-130">You have services and resources with settings like virtual IP addresses that you don't want toolose.</span></span> <span data-ttu-id="7f2a5-131">當取消配置 hello 服務和資源，這些設定會遺失。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-131">These settings are lost when hello services and resources are deallocated.</span></span>


## <a name="remove-hello-spending-limit"></a><span data-ttu-id="7f2a5-132">移除消費限制的 hello</span><span class="sxs-lookup"><span data-stu-id="7f2a5-132">Remove hello spending limit</span></span>

<span data-ttu-id="7f2a5-133">您可以移除消費限制在任何時候，只要沒有有效的付款方式，與您訂用帳戶相關聯的 hello。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-133">You can remove hello spending limit at any time as long as there's a valid payment method associated with your subscription.</span></span> <span data-ttu-id="7f2a5-134">如有多個月內的信用額度的優惠，您也可以重新啟用 hello 消費限制，在您的下一個計費週期 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-134">For offers that have credit over multiple months, you can also re-enable hello spending limit at hello beginning of your next billing cycle.</span></span>

<span data-ttu-id="7f2a5-135">tooremove 您的消費限制，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7f2a5-135">tooremove your spending limit, follow these steps:</span></span>

1. <span data-ttu-id="7f2a5-136">登入 toohello [Azure 帳戶中心](https://account.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-136">Log on toohello [Azure Account Center](https://account.windowsazure.com).</span></span>

2. <span data-ttu-id="7f2a5-137">選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-137">Select a subscription.</span></span>

3. <span data-ttu-id="7f2a5-138">如果 hello 訂用帳戶已停用到期 toohello 正在達到消費限制，請按一下此通知: 「 訂用帳戶達到消費限制 hello 和已停用的 tooprevent 費用 」。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-138">If hello subscription is disabled due toohello Spending Limit being reached, click this notification: "Subscription reached hello Spending Limit and has been disabled tooprevent charges."</span></span> <span data-ttu-id="7f2a5-139">否則，請按一下**移除消費限制**在 hello**訂用帳戶狀態**區域。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-139">Otherwise, click **Remove spending limit** in hello **SUBSCRIPTION STATUS** area.</span></span>

4. <span data-ttu-id="7f2a5-140">選取適合您的選項。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-140">Select an option that is appropriate for you.</span></span>

|<span data-ttu-id="7f2a5-141">選項</span><span class="sxs-lookup"><span data-stu-id="7f2a5-141">Option</span></span>|<span data-ttu-id="7f2a5-142">效果</span><span class="sxs-lookup"><span data-stu-id="7f2a5-142">Effect</span></span>|
|-------|-----|
|<span data-ttu-id="7f2a5-143">無限期移除消費限制</span><span class="sxs-lookup"><span data-stu-id="7f2a5-143">Remove spending limit indefinitely</span></span>|<span data-ttu-id="7f2a5-144">移除 hello 時自動開啟在 hello hello 開始下一個計費週期沒有消費限制。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-144">Removes hello spending limit without turning it on automatically at hello start of hello next billing period.</span></span>|
|<span data-ttu-id="7f2a5-145">移除目前計費週期 hello 的消費限制</span><span class="sxs-lookup"><span data-stu-id="7f2a5-145">Remove spending limit for hello current billing period</span></span>|<span data-ttu-id="7f2a5-146">移除消費限制，使它傳回時自動開啟在 hello hello 開始下一個計費週期的 hello。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-146">Removes hello spending limit so that it turns back on automatically at hello start of hello next billing period.</span></span>|

## <a name="need-help-contact-support"></a><span data-ttu-id="7f2a5-147">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="7f2a5-147">Need help?</span></span> <span data-ttu-id="7f2a5-148">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-148">Contact support.</span></span>
<span data-ttu-id="7f2a5-149">如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="7f2a5-149">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
