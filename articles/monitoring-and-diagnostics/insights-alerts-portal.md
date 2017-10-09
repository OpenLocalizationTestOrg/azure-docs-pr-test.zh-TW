---
title: "Azure 服務-aaaCreate 警示 Azure 入口網站 |Microsoft 文件"
description: "符合您指定的 hello 條件時，觸發程序的電子郵件，通知，便會呼叫網站 Url (webhook) 或自動化。"
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
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="6fc32-103">在 Azure 監視器中為 Azure 服務建立計量警示 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6fc32-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6fc32-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="6fc32-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="6fc32-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fc32-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="6fc32-106">CLI</span><span class="sxs-lookup"><span data-stu-id="6fc32-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="6fc32-107">概觀</span><span class="sxs-lookup"><span data-stu-id="6fc32-107">Overview</span></span>
<span data-ttu-id="6fc32-108">本文章將示範如何使用 Azure 的度量警示 tooset hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fc32-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="6fc32-109">您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="6fc32-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="6fc32-110">**度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6fc32-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="6fc32-111">也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。</span><span class="sxs-lookup"><span data-stu-id="6fc32-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="6fc32-112">**活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。</span><span class="sxs-lookup"><span data-stu-id="6fc32-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="6fc32-113">深入了解活動記錄檔警示 toolearn[按一下這裡](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6fc32-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="6fc32-114">您可以設定警示的度量 toodo hello 時，下列觸發：</span><span class="sxs-lookup"><span data-stu-id="6fc32-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="6fc32-115">傳送電子郵件通知 toohello 服務管理員和共同管理員</span><span class="sxs-lookup"><span data-stu-id="6fc32-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="6fc32-116">您指定的 tooadditional 電子郵件傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="6fc32-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="6fc32-117">呼叫 webhook</span><span class="sxs-lookup"><span data-stu-id="6fc32-117">call a webhook</span></span>
* <span data-ttu-id="6fc32-118">開始執行的 Azure runbook （只能從 hello Azure 入口網站)</span><span class="sxs-lookup"><span data-stu-id="6fc32-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="6fc32-119">您可以透過下列方式設定和取得有關計量警示規則的資訊</span><span class="sxs-lookup"><span data-stu-id="6fc32-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="6fc32-120">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6fc32-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="6fc32-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fc32-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="6fc32-122">命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="6fc32-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="6fc32-123">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="6fc32-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="6fc32-124">建立警示規則上 hello Azure 入口網站的度量</span><span class="sxs-lookup"><span data-stu-id="6fc32-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="6fc32-125">在 hello[入口網站](https://portal.azure.com/)，找出您感興趣監視 hello 資源並加以選取。</span><span class="sxs-lookup"><span data-stu-id="6fc32-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="6fc32-126">選取**警示**或**警示規則**hello [監視] 區段底下。</span><span class="sxs-lookup"><span data-stu-id="6fc32-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="6fc32-127">hello 文字和圖示可能各不相同稍有不同的資源。</span><span class="sxs-lookup"><span data-stu-id="6fc32-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![監視](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="6fc32-129">選取 hello**新增警示**命令，並填寫 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="6fc32-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![新增警示](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="6fc32-131">為您的警示規則命名 ([名稱])，選擇將會顯示在電子郵件通知中的 [描述]。</span><span class="sxs-lookup"><span data-stu-id="6fc32-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="6fc32-132">選取 hello**度量**toomonitor，然後選擇 **條件**和**閾值**hello 公制值。</span><span class="sxs-lookup"><span data-stu-id="6fc32-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="6fc32-133">同時選擇 hello**期間**的 hello 度量的時間必須符合規則之前 hello 警示觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6fc32-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="6fc32-134">例如，如果您使用 hello 期間 」 PT5M 」 警示會尋找 CPU 高於 80%，hello 警示時，觸發 hello CPU 已經一致上述 80 %5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6fc32-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="6fc32-135">一旦發生 hello 第一個觸發程序，一次觸發時 hello CPU 會保持低於 80 %5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6fc32-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="6fc32-136">hello CPU 度量，就會發生每隔 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6fc32-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="6fc32-137">請檢查**電子郵件擁有者...**如果您想要以電子郵件傳送的系統管理員和共同管理員 toobe 當 hello 引發警示。</span><span class="sxs-lookup"><span data-stu-id="6fc32-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="6fc32-138">如果您想要其他的電子郵件 tooreceive 通知時 hello 警示引發，增益 hello**其他的系統管理員 email(s)**欄位。</span><span class="sxs-lookup"><span data-stu-id="6fc32-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="6fc32-139">以分號分隔多個電子郵件 - *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="6fc32-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="6fc32-140">將放在有效的 URI，在 hello **Webhook**欄位若要呼叫它時 hello 引發警示。</span><span class="sxs-lookup"><span data-stu-id="6fc32-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="6fc32-141">如果您使用 Azure 自動化，您可以選取 Runbook toobe hello 警示觸發時執行。</span><span class="sxs-lookup"><span data-stu-id="6fc32-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="6fc32-142">選取**確定**時完成的 toocreate hello 警示。</span><span class="sxs-lookup"><span data-stu-id="6fc32-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="6fc32-143">在幾分鐘的時間內 hello 警示為作用中，且觸發程序，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="6fc32-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="6fc32-144">管理警示</span><span class="sxs-lookup"><span data-stu-id="6fc32-144">Managing your alerts</span></span>
<span data-ttu-id="6fc32-145">一旦建立警示，您可以選取警示，並且︰</span><span class="sxs-lookup"><span data-stu-id="6fc32-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="6fc32-146">檢視圖表顯示 hello 度量的閾值，從 hello 的 hello 實際值的前一天。</span><span class="sxs-lookup"><span data-stu-id="6fc32-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="6fc32-147">編輯或刪除警示。</span><span class="sxs-lookup"><span data-stu-id="6fc32-147">Edit or delete it.</span></span>
* <span data-ttu-id="6fc32-148">**停用**或**啟用**它，如果您想要 tootemporarily 停止或繼續接收該警示的通知。</span><span class="sxs-lookup"><span data-stu-id="6fc32-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fc32-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fc32-149">Next steps</span></span>
* <span data-ttu-id="6fc32-150">[取得的 Azure 監視概觀](monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。</span><span class="sxs-lookup"><span data-stu-id="6fc32-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="6fc32-151">深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc32-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="6fc32-152">深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc32-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="6fc32-153">深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc32-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="6fc32-154">依照 [診斷記錄檔概觀](monitoring-overview-of-diagnostic-logs.md) 中的做法，收集您服務中詳細的高頻率計量。</span><span class="sxs-lookup"><span data-stu-id="6fc32-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="6fc32-155">取得[概觀度量收集](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="6fc32-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
