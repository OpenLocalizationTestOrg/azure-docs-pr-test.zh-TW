---
title: "為 Azure 訂用帳戶設定計費或信用額度警示 | Microsoft Docs"
description: "描述如何設定您的 Azure 帳單上的警示，以避免計費出現意外的狀況。"
keywords: "信用額度警示, 計費警示"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="1fe5d-104">為您的 Microsoft Azure 訂用帳戶設定計費或信用額度警示</span><span class="sxs-lookup"><span data-stu-id="1fe5d-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="1fe5d-105">如果您是 Azure 訂用帳戶的帳戶管理員，您可以使用「Azure 計費警示服務」來建立自訂計費警示，以協助您監視和管理您 Azure 帳戶的計費活動。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="1fe5d-106">此服務為預覽狀態，因此您必須先在 [預覽功能] 頁面中加以啟用。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="1fe5d-107">設定警示閾值與電子郵件收件者</span><span class="sxs-lookup"><span data-stu-id="1fe5d-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="1fe5d-108">請瀏覽[預覽功能頁面](https://account.windowsazure.com/PreviewFeatures)並啟用**計費警示服務**。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="1fe5d-109">在收到已為您的訂用帳戶開啟計費服務的電子郵件確認之後，請瀏覽帳戶入口網站中的 [訂用帳戶頁面](https://account.windowsazure.com/Subscriptions) 。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="1fe5d-110">按一下您想要監視的訂用帳戶，然後按一下 [警示] 。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Azure 帳戶中心的訂用帳戶檢視螢幕擷取畫面，已醒目提示警示][Image1]

2. <span data-ttu-id="1fe5d-112">接著，按一下 [新增警示] 來建立您的第一個警示。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="1fe5d-113">每一訂用帳戶總計可以設定 5 個具有不同臨界值的警示，每個警示最多可以設定兩個電子郵件收件者。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![可供新增警示的警示檢視螢幕擷取畫面][Image2]

3. <span data-ttu-id="1fe5d-115">新增警示時，您將為它提供一個唯一的名稱、選擇消費臨界值，以及選擇要接收警示的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="1fe5d-116">設定臨界值時，您可以從 [警示對象] 清單中選擇 [計費總計] 或 [貨幣信用額度]。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="1fe5d-117">如果是計費總計，當訂用帳戶消費超過臨界值時，就會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="1fe5d-118">如果是貨幣信用額度，當貨幣信用額度低於限制時，就會傳送警示。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="1fe5d-119">貨幣信用額度通常適用於免費試用和 Visual Studio 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![可供設定收件者的警示新增檢視螢幕擷取畫面][Image3]

<span data-ttu-id="1fe5d-121">Azure 支援任何電子郵件地址，但不會驗證電子郵件地址是否有效，所以請仔細檢查是否有錯字。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="1fe5d-122">檢查您的通知</span><span class="sxs-lookup"><span data-stu-id="1fe5d-122">Check on your alerts</span></span>
<span data-ttu-id="1fe5d-123">設定警示之後，[帳戶中心] 會列出這些警示，並顯示您還可以設定多少個警示。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="1fe5d-124">針對每個警示，您會看到其傳送日期和時間 (不論是 [計費總計] 還是 [貨幣信用額度] 警示)，以及您所設定的限制。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="1fe5d-125">日期和時間格式是 24 小時制的世界標準時間 (UTC)，而日期為 yyyy-mm-dd 格式。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="1fe5d-126">您可以按一下清單中某個警示的加號來編輯該警示，或按一下資源回收筒圖示來將它刪除。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="1fe5d-127">Enterprise 合約 (EA) 客戶適用的計費警示</span><span class="sxs-lookup"><span data-stu-id="1fe5d-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="1fe5d-128">透過設定消費配額，EA 客戶可以取得註冊底下每個部門的警示。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="1fe5d-129">請參閱 EA 入口網站中的[部門消費配額](https://ea.azure.com/helpdocs/departmentSpendingQuotas)以便開始使用。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="1fe5d-130">深入了解 Azure 成本管理</span><span class="sxs-lookup"><span data-stu-id="1fe5d-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="1fe5d-131">使用[價格計算機](https://azure.microsoft.com/pricing/calculator/)、[擁有權總成本計算機](https://aka.ms/azure-tco-calculator)，以及新增服務的時間預估成本。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="1fe5d-132">[定期在 Azure 入口網站檢閱您的使用量和成本](billing-getting-started.md#costs)。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="1fe5d-133">開啟 [Azure Advisor 成本建議](../advisor/advisor-cost-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="1fe5d-134">若要深入了解，請參閱 [Azure 成本管理指導](billing-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1fe5d-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
