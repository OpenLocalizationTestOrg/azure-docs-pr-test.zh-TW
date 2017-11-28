---
title: "建立 Azure 服務的警示 - Azure 入口網站 | Microsoft Docs"
description: "當符合您指定的條件時，觸發電子郵件、通知、呼叫網站 URL (Webhook) 或自動化。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="787d1-103">在 Azure 監視器中為 Azure 服務建立計量警示 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="787d1-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="787d1-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="787d1-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="787d1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="787d1-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="787d1-106">CLI</span><span class="sxs-lookup"><span data-stu-id="787d1-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="787d1-107">概觀</span><span class="sxs-lookup"><span data-stu-id="787d1-107">Overview</span></span>
<span data-ttu-id="787d1-108">此文章說明如何使用 Azure 入口網站設定 Azure 計量警示。</span><span class="sxs-lookup"><span data-stu-id="787d1-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="787d1-109">您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="787d1-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="787d1-110">**計量值** - 當指定的計量值超出您在任一方向指派的臨界值時會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="787d1-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="787d1-111">也就是說，當先符合條件而之後該條件不再符合時，兩方面皆會觸發。</span><span class="sxs-lookup"><span data-stu-id="787d1-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="787d1-112">**活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。</span><span class="sxs-lookup"><span data-stu-id="787d1-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="787d1-113">若要深入了解活動記錄檔警示，請[按一下這裡](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="787d1-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="787d1-114">您可以設定當計量警示觸發時執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="787d1-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="787d1-115">傳送電子郵件給服務管理員和共同管理員</span><span class="sxs-lookup"><span data-stu-id="787d1-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="787d1-116">傳送電子郵件至您指定的其他電子郵件</span><span class="sxs-lookup"><span data-stu-id="787d1-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="787d1-117">呼叫 webhook</span><span class="sxs-lookup"><span data-stu-id="787d1-117">call a webhook</span></span>
* <span data-ttu-id="787d1-118">啟動執行 Azure Runbook (現階段只能從 Azure 入口網站啟動)</span><span class="sxs-lookup"><span data-stu-id="787d1-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="787d1-119">您可以透過下列方式設定和取得有關計量警示規則的資訊</span><span class="sxs-lookup"><span data-stu-id="787d1-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="787d1-120">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="787d1-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="787d1-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="787d1-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="787d1-122">命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="787d1-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="787d1-123">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="787d1-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="787d1-124">使用 Azure 入口網站建立計量的警示規則</span><span class="sxs-lookup"><span data-stu-id="787d1-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="787d1-125">在 [入口網站](https://portal.azure.com/)中，找到您要監視的資源並選取。</span><span class="sxs-lookup"><span data-stu-id="787d1-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="787d1-126">選取 [監視] 區段底下的 [警示] 或 [警示規則]。</span><span class="sxs-lookup"><span data-stu-id="787d1-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="787d1-127">不同資源的文字和圖示會有些許不同。</span><span class="sxs-lookup"><span data-stu-id="787d1-127">The text and icon may vary slightly for different resources.</span></span>  

    ![監視](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="787d1-129">選取 [新增警示]  命令，並填寫各欄位。</span><span class="sxs-lookup"><span data-stu-id="787d1-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![新增警示](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="787d1-131">為您的警示規則命名 ([名稱])，選擇將會顯示在電子郵件通知中的 [描述]。</span><span class="sxs-lookup"><span data-stu-id="787d1-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="787d1-132">選取您要監視的 [計量]，然後為計量選擇 [條件] 和 [臨界值]。</span><span class="sxs-lookup"><span data-stu-id="787d1-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="787d1-133">同時選擇警示觸發程序之前，計量規則必須滿足的 [期間]  。</span><span class="sxs-lookup"><span data-stu-id="787d1-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="787d1-134">例如，如果您使用「PT5M」期間，且您的警示會尋找高於 80% 的 CPU，當 CPU 已持續 5 分鐘高於 80%，警示就會觸發。</span><span class="sxs-lookup"><span data-stu-id="787d1-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="787d1-135">一旦發生第一次觸發，它會在 CPU 持續 5 分鐘低於 80 % 時再次觸發。</span><span class="sxs-lookup"><span data-stu-id="787d1-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="787d1-136">CPU 度量每隔 1 分鐘發生一次。</span><span class="sxs-lookup"><span data-stu-id="787d1-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="787d1-137">如果您想要在警示引發時傳送電子郵件給系統管理員和共同管理員，請勾選 [電子郵件的擁有者...]  。</span><span class="sxs-lookup"><span data-stu-id="787d1-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="787d1-138">如果您想要讓其他電子郵件信箱在警示引發時收到通知，在 [其他系統管理員電子郵件]  欄位新增它們。</span><span class="sxs-lookup"><span data-stu-id="787d1-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="787d1-139">以分號分隔多個電子郵件 - *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="787d1-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="787d1-140">如果您想在警示引發時呼叫webhook，在[webhook]  欄位中放入有效的 URI。</span><span class="sxs-lookup"><span data-stu-id="787d1-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="787d1-141">如果您使用 Azure 自動化，可以選取警示引發時執行的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="787d1-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="787d1-142">完成後選取 [確定]  建立警示。</span><span class="sxs-lookup"><span data-stu-id="787d1-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="787d1-143">在幾分鐘之內，警示會開始作用，且先前所述觸發。</span><span class="sxs-lookup"><span data-stu-id="787d1-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="787d1-144">管理警示</span><span class="sxs-lookup"><span data-stu-id="787d1-144">Managing your alerts</span></span>
<span data-ttu-id="787d1-145">一旦建立警示，您可以選取警示，並且︰</span><span class="sxs-lookup"><span data-stu-id="787d1-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="787d1-146">檢視圖表，其中顯示計量臨界值與前一天的實際值。</span><span class="sxs-lookup"><span data-stu-id="787d1-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="787d1-147">編輯或刪除警示。</span><span class="sxs-lookup"><span data-stu-id="787d1-147">Edit or delete it.</span></span>
* <span data-ttu-id="787d1-148">如果您想要暫時停止或恢復接收警示的通知，可以**停用**或**啟用**警示。</span><span class="sxs-lookup"><span data-stu-id="787d1-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="787d1-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="787d1-149">Next steps</span></span>
* <span data-ttu-id="787d1-150">[取得 Azure 監視的概觀](monitoring-overview.md) 中說明您可以收集和監視的資訊類型。</span><span class="sxs-lookup"><span data-stu-id="787d1-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="787d1-151">深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="787d1-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="787d1-152">深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="787d1-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="787d1-153">深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="787d1-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="787d1-154">依照 [診斷記錄檔概觀](monitoring-overview-of-diagnostic-logs.md) 中的做法，收集您服務中詳細的高頻率計量。</span><span class="sxs-lookup"><span data-stu-id="787d1-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="787d1-155">依照 [計量集合概觀](insights-how-to-customize-monitoring.md) 中的做法，確保您的服務可使用且有回應。</span><span class="sxs-lookup"><span data-stu-id="787d1-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
