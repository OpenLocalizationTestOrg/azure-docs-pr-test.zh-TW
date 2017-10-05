---
title: "取消 Azure 訂用帳戶 | Microsoft Docs"
description: "說明如何取消 Azure 訂用帳戶，例如免費試用訂用帳戶"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a><span data-ttu-id="45bd5-103">取消您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45bd5-103">Cancel your subscription for Azure</span></span>

<span data-ttu-id="45bd5-104">您可以用[帳戶管理員](billing-subscription-transfer.md#whoisaa)身分取消您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45bd5-104">You can cancel your Azure subscription as the [Account Administrator](billing-subscription-transfer.md#whoisaa).</span></span> <span data-ttu-id="45bd5-105">取消訂用帳戶之後，您將無法存取 Azure 服務和資源端點。</span><span class="sxs-lookup"><span data-stu-id="45bd5-105">After you cancel the subscription, your access to Azure services and resources ends.</span></span>

<span data-ttu-id="45bd5-106">取消訂用帳戶之前︰</span><span class="sxs-lookup"><span data-stu-id="45bd5-106">Before you cancel your subscription:</span></span>

* <span data-ttu-id="45bd5-107">備份您的資料。</span><span class="sxs-lookup"><span data-stu-id="45bd5-107">Back up your data.</span></span> <span data-ttu-id="45bd5-108">例如，如果您將資料儲存在 Azure 儲存體或 SQL，請下載複本。</span><span class="sxs-lookup"><span data-stu-id="45bd5-108">For example, if you're storing data in Azure storage or SQL, download a copy.</span></span> <span data-ttu-id="45bd5-109">如果您有虛擬機器，請將其映像儲存在本機。</span><span class="sxs-lookup"><span data-stu-id="45bd5-109">If you have a virtual machine, save an image of it locally.</span></span>
* <span data-ttu-id="45bd5-110">關閉您的服務。</span><span class="sxs-lookup"><span data-stu-id="45bd5-110">Shut down your services.</span></span> <span data-ttu-id="45bd5-111">移至[管理入口網站中的資源頁面](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources)，並**停止**任何執行中的虛擬機器、應用程式或其他服務。</span><span class="sxs-lookup"><span data-stu-id="45bd5-111">Go to the [resources page in the management portal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), and **Stop** any running virtual machines, applications, or other services.</span></span>
* <span data-ttu-id="45bd5-112">考慮移轉您的資料。</span><span class="sxs-lookup"><span data-stu-id="45bd5-112">Consider migrating your data.</span></span> <span data-ttu-id="45bd5-113">請參閱[將資源移動到新的資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="45bd5-113">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="45bd5-114">如果您取消付費 [Azure 支援方案](https://azure.microsoft.com/support/plans/)，6 個月期剩下的每個月仍會計費。</span><span class="sxs-lookup"><span data-stu-id="45bd5-114">If you cancel a paid [Azure Support plan](https://azure.microsoft.com/support/plans/), you are still billed monthly for the rest of the 6-months term.</span></span>

## <a name="cancel-subscription-using-the-azure-portal"></a><span data-ttu-id="45bd5-115">使用 Azure 入口網站取消訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45bd5-115">Cancel subscription using the Azure portal</span></span>

1. <span data-ttu-id="45bd5-116">在[訂用帳戶頁面](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)中，選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45bd5-116">Select your subscription from the [Subscriptions page](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

1. <span data-ttu-id="45bd5-117">選取您要取消的訂用帳戶，然後按一下 [取消訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="45bd5-117">Select the subscription that you want to cancel and click **Cancel subscription**.</span></span>

    ![顯示 [取消] 按鈕的螢幕擷取畫面](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. <span data-ttu-id="45bd5-119">遵循提示並完成取消作業。</span><span class="sxs-lookup"><span data-stu-id="45bd5-119">Follow prompts and finish cancellation.</span></span>

## <a name="cancel-subscription-using-the-azure-account-center"></a><span data-ttu-id="45bd5-120">使用 Azure 帳戶中心取消訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45bd5-120">Cancel subscription using the Azure Account Center</span></span>

1. <span data-ttu-id="45bd5-121">以帳戶管理員身分登入 [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="45bd5-121">Sign in to the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

1. <span data-ttu-id="45bd5-122">在 [按一下訂用帳戶即可檢視詳細資料及使用量] 下方，選取您要取消的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45bd5-122">Under **Click a subscription to view details and usage**, select the subscription that you want to cancel.</span></span>

    ![顯示已選取範例訂用帳戶的螢幕擷取畫面](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. <span data-ttu-id="45bd5-124">選取頁面右側的 [取消訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="45bd5-124">On the right side of the page, select **Cancel Subscription**.</span></span>

    ![顯示 [取消訂用帳戶] 按鈕的螢幕擷取畫面](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. <span data-ttu-id="45bd5-126">選取 [是，取消我的訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="45bd5-126">Select **Yes, cancel my subscription**.</span></span>

    ![顯示 [取消] 對話方塊的螢幕擷取畫面](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. <span data-ttu-id="45bd5-128">按一下 </span><span class="sxs-lookup"><span data-stu-id="45bd5-128">Click</span></span> ![[核取符號] 按鈕](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) <span data-ttu-id="45bd5-130">關閉對話視窗並返回您的訂用帳戶頁面。</span><span class="sxs-lookup"><span data-stu-id="45bd5-130">to close the dialog window and return to your subscription page.</span></span>

## <a name="what-happens-after-i-cancel-my-subscription"></a><span data-ttu-id="45bd5-131">取消訂用帳戶之後會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="45bd5-131">What happens after I cancel my subscription?</span></span>

<span data-ttu-id="45bd5-132">當您取消之後，計費會立即停止。</span><span class="sxs-lookup"><span data-stu-id="45bd5-132">Once you cancel, billing is stopped immediately.</span></span> <span data-ttu-id="45bd5-133">不過，可能需要最多 10 分鐘的時間，取消作業才會出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="45bd5-133">However, it can take up to 10 minutes for the cancellation show in the portal.</span></span>

<span data-ttu-id="45bd5-134">在這之後，您的服務將會停用。</span><span class="sxs-lookup"><span data-stu-id="45bd5-134">After that, your services are disabled.</span></span> <span data-ttu-id="45bd5-135">這表示您的虛擬機器將會解除配置、暫時 IP 位址將會釋出，且儲存體會變成唯讀。</span><span class="sxs-lookup"><span data-stu-id="45bd5-135">That means your virtual machines are deallocated, temporary IP addresses are freed, and storage is read-only.</span></span>

<span data-ttu-id="45bd5-136">除非您是處於免費試用期間或有可用的信用額度，否則您必須支付在最後一個結算週期與取消日期之間產生的所有未支付使用費用。</span><span class="sxs-lookup"><span data-stu-id="45bd5-136">Unless you’re on a Free Trial or have credits available, you’re billed for any outstanding usage charges generated between your last billing cycle and the cancellation date.</span></span> <span data-ttu-id="45bd5-137">您將在計費週期結束時取得最後一份帳單。</span><span class="sxs-lookup"><span data-stu-id="45bd5-137">You get your last bill at the end of the billing cycle.</span></span>

<span data-ttu-id="45bd5-138">取消訂用帳戶之後，我們會等 90 天之後才永久刪除您的資料，以防您需要存取它，或您改變心意。</span><span class="sxs-lookup"><span data-stu-id="45bd5-138">After you cancel your subscription, we wait 90 days before permanently deleting your data in case you need to access it or you change your mind.</span></span> <span data-ttu-id="45bd5-139">我們不會向您收取保留資料的費用。</span><span class="sxs-lookup"><span data-stu-id="45bd5-139">We don't charge you for retaining the data.</span></span> <span data-ttu-id="45bd5-140">若要深入了解，請參閱 [Microsoft 信任中心 - 我們如何管理您的資料](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="45bd5-140">To learn more, see [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span></span>

## <a name="reactivate-subscription"></a><span data-ttu-id="45bd5-141">重新啟動訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="45bd5-141">Reactivate subscription</span></span>

<span data-ttu-id="45bd5-142">如果您不小心取消隨用隨付訂用帳戶，您可以[在帳戶中心重新啟動它](billing-subscription-become-disable.md)。</span><span class="sxs-lookup"><span data-stu-id="45bd5-142">If you cancel your Pay-As-You-Go subscription accidentally, you can [reactivate it in the Accounts Center](billing-subscription-become-disable.md).</span></span>

<span data-ttu-id="45bd5-143">如果您的訂用帳戶不是隨用隨付類型，請在取消後 90 天內與支援服務連絡，以重新啟動您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45bd5-143">If your subscription is not Pay-As-You-Go, contact support within 90 days of cancellation to reactivate your subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="45bd5-144">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="45bd5-144">Need help?</span></span> <span data-ttu-id="45bd5-145">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="45bd5-145">Contact support.</span></span>

<span data-ttu-id="45bd5-146">如果您仍有問題，請[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="45bd5-146">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
