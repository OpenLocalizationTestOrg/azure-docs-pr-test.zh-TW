---
title: "了解 Azure 消費限制 | Microsoft Docs"
description: "說明 Azure 消費限制的運作方式及如何移除此限制"
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
ms.openlocfilehash: a2743ef34bde0faabb3afd2ace27acddd59d3d70
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="understand-azure-spending-limit-and-how-to-remove-it"></a><span data-ttu-id="77ab1-103">了解 Azure 消費限制及如何移除此限制</span><span class="sxs-lookup"><span data-stu-id="77ab1-103">Understand Azure spending limit and how to remove it</span></span>

<span data-ttu-id="77ab1-104">Azure 消費限制是對您 Azure 訂用帳戶消費額度的限制。</span><span class="sxs-lookup"><span data-stu-id="77ab1-104">Azure spending limit is a limit on how much your Azure subscription can spend.</span></span> <span data-ttu-id="77ab1-105">所有新客戶只要註冊試用方案或包含多月點數的方案，預設都會開啟消費限制。</span><span class="sxs-lookup"><span data-stu-id="77ab1-105">All new customers who sign up for the trial offer or offers that includes credits over multiple months have the spending limit turned on by default.</span></span> <span data-ttu-id="77ab1-106">消費限制是 $0。</span><span class="sxs-lookup"><span data-stu-id="77ab1-106">The spending limit is $0.</span></span> <span data-ttu-id="77ab1-107">此限制無法變更。</span><span class="sxs-lookup"><span data-stu-id="77ab1-107">It can’t be changed.</span></span> <span data-ttu-id="77ab1-108">隨用隨付訂用帳戶和承諾方案之類的訂用帳戶類型無法使用消費限制。</span><span class="sxs-lookup"><span data-stu-id="77ab1-108">The spending limit isn’t available for subscription types such as Pay-As-You-Go subscriptions and commitment plans.</span></span> <span data-ttu-id="77ab1-109">請參閱[完整的 Azure 優惠及消費限制可用性清單](https://azure.microsoft.com/support/legal/offer-details/)。</span><span class="sxs-lookup"><span data-stu-id="77ab1-109">See the [full list of Azure offers and the availability of the spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

## <a name="what-happens-when-i-reach-the-spending-limit"></a><span data-ttu-id="77ab1-110">達到消費限制時會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="77ab1-110">What happens when I reach the spending limit?</span></span>

<span data-ttu-id="77ab1-111">當您因使用而產生的費用用罄優惠中所包含的每月金額時，您部署的服務將在該計費月份的剩餘天數中停用。</span><span class="sxs-lookup"><span data-stu-id="77ab1-111">When your usage results in charges that exhaust the monthly amounts included in your offer, the services that you deployed are disabled for the rest of that billing month.</span></span> <span data-ttu-id="77ab1-112">舉例來說，您部署的「雲端服務」會從生產環境中移除，而 Azure 虛擬機器則會停止並解除配置。</span><span class="sxs-lookup"><span data-stu-id="77ab1-112">For example, Cloud Services that you deployed are removed from production and your Azure virtual machines are stopped and de-allocated.</span></span> <span data-ttu-id="77ab1-113">若要避免服務遭到停用，您可以選擇移除消費限制。</span><span class="sxs-lookup"><span data-stu-id="77ab1-113">To prevent your services from being disabled, you can choose to remove your spending limit.</span></span> <span data-ttu-id="77ab1-114">當您的服務遭到停用時，您儲存體帳戶及資料庫中的資料仍然可供系統管理員以唯讀方式使用。</span><span class="sxs-lookup"><span data-stu-id="77ab1-114">When your services are disabled, the data in your storage accounts and databases are available in a read-only manner for administrators.</span></span> <span data-ttu-id="77ab1-115">在下一個計費月份開始時，若您的優惠包含多月點數，您的訂用帳戶將會重新啟用。</span><span class="sxs-lookup"><span data-stu-id="77ab1-115">At the beginning of the next billing month, if your offer includes credits over multiple months, your subscription will be re-enabled.</span></span> <span data-ttu-id="77ab1-116">接著，您便可以重新部署「雲端服務」，並完整存取您的儲存體帳戶和資料庫。</span><span class="sxs-lookup"><span data-stu-id="77ab1-116">Then you can redeploy your Cloud Services and have full access to your storage accounts and databases.</span></span>

<span data-ttu-id="77ab1-117">在免費試用訂用帳戶達到消費限制後，您可以在 90 天內重新啟用訂用帳戶，並讓它自動[升級到標準隨用隨付優惠](billing-upgrade-azure-subscription.md)。</span><span class="sxs-lookup"><span data-stu-id="77ab1-117">After the free trial subscription reaches the spending limit, you can re-enable the subscription and have it automatically [upgrade to our standard Pay-As-You-Go offer](billing-upgrade-azure-subscription.md) within 90 days.</span></span>

<span data-ttu-id="77ab1-118">當您達到所用優惠的消費限制時，將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="77ab1-118">You receive notifications when you hit the spending limit for your offer.</span></span> <span data-ttu-id="77ab1-119">請登入 [Azure 帳戶中心](https://account.windowsazure.com)，選取 [帳戶]，然後選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="77ab1-119">Log on to the [Azure Account Center](https://account.windowsazure.com), select **ACCOUNT**, and then select **subscriptions**.</span></span> <span data-ttu-id="77ab1-120">您會看到已達到消費限制之訂用帳戶的相關通知。</span><span class="sxs-lookup"><span data-stu-id="77ab1-120">You see notifications about subscriptions that have reached the spending limit.</span></span>

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a><span data-ttu-id="77ab1-121">即使已啟用消費限制也需要付費的項目</span><span class="sxs-lookup"><span data-stu-id="77ab1-121">Things you are charged for even if you have a spending limit enabled</span></span>

<span data-ttu-id="77ab1-122">即使已設定消費限制，有些 Azure 服務及 [Marketplace 購買](https://azure.microsoft.com/marketplace/)仍可能因付款方式 (CC) 而產生費用。</span><span class="sxs-lookup"><span data-stu-id="77ab1-122">Some Azure services and [Marketplace purchases](https://azure.microsoft.com/marketplace/) can incur charges under the payment method (CC) even if a spending limit is set.</span></span> <span data-ttu-id="77ab1-123">例如 Visual Studio 授權、Azure Active Directory Premium、支援方案以及透過 Marketplace 銷售的大多數協力廠商品牌服務。</span><span class="sxs-lookup"><span data-stu-id="77ab1-123">Examples are Visual studio licenses, Azure Active Directory premium, support plans, and most third-party branded services sold through the Marketplace.</span></span>


## <a name="when-not-to-use-the-spending-limit"></a><span data-ttu-id="77ab1-124">何時不要使用消費限制</span><span class="sxs-lookup"><span data-stu-id="77ab1-124">When not to use the spending limit</span></span>

<span data-ttu-id="77ab1-125">消費限制會防止您部署或使用特定的市集及 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="77ab1-125">The spending limit could prevent you from deploying or using certain marketplace and Microsoft services.</span></span> <span data-ttu-id="77ab1-126">以下是您應該移除訂用帳戶消費限制的情況。</span><span class="sxs-lookup"><span data-stu-id="77ab1-126">Here are the scenarios where you should remove the spending limit on your subscription.</span></span>

- <span data-ttu-id="77ab1-127">您打算部署第一方映像 (例如 Oracle) 或第一方服務 (例如 Visual Studio Team Services)。</span><span class="sxs-lookup"><span data-stu-id="77ab1-127">You plan to deploy first party images like Oracle and services such as Visual Studio Team Services.</span></span> <span data-ttu-id="77ab1-128">此情況會讓您幾乎立即超過消費限制，而導致訂用帳戶遭停用。</span><span class="sxs-lookup"><span data-stu-id="77ab1-128">This scenario causes you to exceed your spending limit almost immediately and causes your subscription to be disabled.</span></span>

- <span data-ttu-id="77ab1-129">您有不可中斷的服務。</span><span class="sxs-lookup"><span data-stu-id="77ab1-129">You have services that cannot be disrupted.</span></span>

- <span data-ttu-id="77ab1-130">您的服務及資源有您不想遺失的設定 (例如虛擬 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="77ab1-130">You have services and resources with settings like virtual IP addresses that you don't want to lose.</span></span> <span data-ttu-id="77ab1-131">將服務及資源解除配置時，將會遺失這些設定。</span><span class="sxs-lookup"><span data-stu-id="77ab1-131">These settings are lost when the services and resources are deallocated.</span></span>


## <a name="remove-the-spending-limit"></a><span data-ttu-id="77ab1-132">移除消費限制</span><span class="sxs-lookup"><span data-stu-id="77ab1-132">Remove the spending limit</span></span>

<span data-ttu-id="77ab1-133">只要您的訂用帳戶所關聯的付款方式有效，您就可以隨時移除消費限制。</span><span class="sxs-lookup"><span data-stu-id="77ab1-133">You can remove the spending limit at any time as long as there's a valid payment method associated with your subscription.</span></span> <span data-ttu-id="77ab1-134">針對具有多月點數的優惠，您也可以在下一個計費週期開始時重新啟用消費限制。</span><span class="sxs-lookup"><span data-stu-id="77ab1-134">For offers that have credit over multiple months, you can also re-enable the spending limit at the beginning of your next billing cycle.</span></span>

<span data-ttu-id="77ab1-135">若要移除您的消費限制，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="77ab1-135">To remove your spending limit, follow these steps:</span></span>

1. <span data-ttu-id="77ab1-136">登入 [Azure 帳戶中心](https://account.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="77ab1-136">Log on to the [Azure Account Center](https://account.windowsazure.com).</span></span>

2. <span data-ttu-id="77ab1-137">選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77ab1-137">Select a subscription.</span></span>

3. <span data-ttu-id="77ab1-138">如果訂用帳戶因為達到「消費限制」而被停用，請按一下此通知：[訂用帳戶已達消費限制，並已停用，以避免收費。]</span><span class="sxs-lookup"><span data-stu-id="77ab1-138">If the subscription is disabled due to the Spending Limit being reached, click this notification: "Subscription reached the Spending Limit and has been disabled to prevent charges."</span></span> <span data-ttu-id="77ab1-139">否則，請按一下 [訂用帳戶狀態] 區域中的 [移除消費限制]。</span><span class="sxs-lookup"><span data-stu-id="77ab1-139">Otherwise, click **Remove spending limit** in the **SUBSCRIPTION STATUS** area.</span></span>

4. <span data-ttu-id="77ab1-140">選取適合您的選項。</span><span class="sxs-lookup"><span data-stu-id="77ab1-140">Select an option that is appropriate for you.</span></span>

|<span data-ttu-id="77ab1-141">選項</span><span class="sxs-lookup"><span data-stu-id="77ab1-141">Option</span></span>|<span data-ttu-id="77ab1-142">效果</span><span class="sxs-lookup"><span data-stu-id="77ab1-142">Effect</span></span>|
|-------|-----|
|<span data-ttu-id="77ab1-143">無限期移除消費限制</span><span class="sxs-lookup"><span data-stu-id="77ab1-143">Remove spending limit indefinitely</span></span>|<span data-ttu-id="77ab1-144">移除消費限制，不在下一個計費週期開始時自動開啟。</span><span class="sxs-lookup"><span data-stu-id="77ab1-144">Removes the spending limit without turning it on automatically at the start of the next billing period.</span></span>|
|<span data-ttu-id="77ab1-145">移除目前計費週期的消費限制</span><span class="sxs-lookup"><span data-stu-id="77ab1-145">Remove spending limit for the current billing period</span></span>|<span data-ttu-id="77ab1-146">移除消費限制，讓它在下一個計費週期開始時自動開啟。</span><span class="sxs-lookup"><span data-stu-id="77ab1-146">Removes the spending limit so that it turns back on automatically at the start of the next billing period.</span></span>|

## <a name="need-help-contact-support"></a><span data-ttu-id="77ab1-147">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="77ab1-147">Need help?</span></span> <span data-ttu-id="77ab1-148">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="77ab1-148">Contact support.</span></span>
<span data-ttu-id="77ab1-149">如果仍需要協助，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="77ab1-149">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
