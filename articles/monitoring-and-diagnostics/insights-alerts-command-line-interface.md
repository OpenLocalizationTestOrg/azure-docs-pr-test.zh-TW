---
title: "建立 Azure 服務的警示 - 跨平台 CLI | Microsoft Docs"
description: "當符合您指定的條件時，觸發電子郵件、通知、呼叫網站 URL (Webhook) 或自動化。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="38fa8-103">在 Azure 監視器中為 Azure 服務建立計量警示 - 跨平台 CLI</span><span class="sxs-lookup"><span data-stu-id="38fa8-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38fa8-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="38fa8-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="38fa8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38fa8-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="38fa8-106">CLI</span><span class="sxs-lookup"><span data-stu-id="38fa8-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="38fa8-107">概觀</span><span class="sxs-lookup"><span data-stu-id="38fa8-107">Overview</span></span>
<span data-ttu-id="38fa8-108">此文章將說明如何使用跨平台命令列介面 (CLI) 設定 Azure 計量警示。</span><span class="sxs-lookup"><span data-stu-id="38fa8-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="38fa8-109">自 2016 年 9 月 25 日起，「Azure 監視器」是以前所謂「Azure Insights」的新名稱。</span><span class="sxs-lookup"><span data-stu-id="38fa8-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="38fa8-110">不過，命名空間和下列命令中仍有 "insights"。</span><span class="sxs-lookup"><span data-stu-id="38fa8-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="38fa8-111">您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="38fa8-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="38fa8-112">**計量值** - 當指定的計量值超出您在任一方向指派的臨界值時會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="38fa8-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="38fa8-113">也就是說，當先符合條件而之後該條件不再符合時，兩方面皆會觸發。</span><span class="sxs-lookup"><span data-stu-id="38fa8-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="38fa8-114">**活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。</span><span class="sxs-lookup"><span data-stu-id="38fa8-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="38fa8-115">若要深入了解活動記錄檔警示，請[按一下這裡](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="38fa8-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="38fa8-116">您可以設定當計量警示觸發時執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="38fa8-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="38fa8-117">傳送電子郵件給服務管理員和共同管理員</span><span class="sxs-lookup"><span data-stu-id="38fa8-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="38fa8-118">傳送電子郵件至您指定的其他電子郵件</span><span class="sxs-lookup"><span data-stu-id="38fa8-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="38fa8-119">呼叫 webhook</span><span class="sxs-lookup"><span data-stu-id="38fa8-119">call a webhook</span></span>
* <span data-ttu-id="38fa8-120">啟動執行 Azure Runbook (現階段只能從 Azure 入口網站啟動)</span><span class="sxs-lookup"><span data-stu-id="38fa8-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="38fa8-121">您可以透過下列方式設定和取得有關計量警示規則的資訊</span><span class="sxs-lookup"><span data-stu-id="38fa8-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="38fa8-122">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="38fa8-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="38fa8-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38fa8-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="38fa8-124">命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="38fa8-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="38fa8-125">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="38fa8-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="38fa8-126">輸入命令並在結尾加上 -help，可以收到命令的說明。</span><span class="sxs-lookup"><span data-stu-id="38fa8-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="38fa8-127">例如：</span><span class="sxs-lookup"><span data-stu-id="38fa8-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="38fa8-128">使用 CLI 建立警示規則</span><span class="sxs-lookup"><span data-stu-id="38fa8-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="38fa8-129">執行必要條件，然後登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="38fa8-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="38fa8-130">請參閱 [Azure 監視器 CLI 範例](insights-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="38fa8-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="38fa8-131">簡單地說，安裝 CLI，執行命令。</span><span class="sxs-lookup"><span data-stu-id="38fa8-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="38fa8-132">這些命令可讓您登入、顯示您正在使用的訂用帳戶、準備執行 Azure 監視器命令。</span><span class="sxs-lookup"><span data-stu-id="38fa8-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="38fa8-133">若要列出資源群組中的現有規則，使用 **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;* 格式</span><span class="sxs-lookup"><span data-stu-id="38fa8-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="38fa8-134">若要建立規則，您需要先取得幾項重要資訊：</span><span class="sxs-lookup"><span data-stu-id="38fa8-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="38fa8-135">您想要為其設定警示的 **資源識別碼**</span><span class="sxs-lookup"><span data-stu-id="38fa8-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="38fa8-136">該資源可使用的 **計量定義**</span><span class="sxs-lookup"><span data-stu-id="38fa8-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="38fa8-137">取得資源識別碼的方法之一，是使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="38fa8-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="38fa8-138">假設已建立資源，在入口網站中選取它。</span><span class="sxs-lookup"><span data-stu-id="38fa8-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="38fa8-139">然後在下一個刀鋒視窗中，選取 [設定] 區段下的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="38fa8-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="38fa8-140">[資源識別碼]  是下一個刀鋒視窗中的欄位。</span><span class="sxs-lookup"><span data-stu-id="38fa8-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="38fa8-141">另一種方法是使用 [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="38fa8-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="38fa8-142">以下是 Web 應用程式的範例資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="38fa8-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="38fa8-143">若要取得先前資源範例中那些計量的可用計量和單位的清單，使用下列的 CLI 命令︰</span><span class="sxs-lookup"><span data-stu-id="38fa8-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="38fa8-144">*PT1M* 是可用度量單位的資料粒度 (間隔 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="38fa8-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="38fa8-145">使用不同的資料粒度可提供您不同的計量選項。</span><span class="sxs-lookup"><span data-stu-id="38fa8-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="38fa8-146">若要建立以計量為基礎的警示規則，使用下列格式︰</span><span class="sxs-lookup"><span data-stu-id="38fa8-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="38fa8-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="38fa8-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="38fa8-148">下列範例會設定網站資源的警示。</span><span class="sxs-lookup"><span data-stu-id="38fa8-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="38fa8-149">只要持續 5 分鐘有收到任何流量，就會觸發警示，在這之後，5 分鐘沒收到任何流量也會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="38fa8-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="38fa8-150">若要在計量警示引發時建立 Webhook 或傳送電子郵件，請先建立電子郵件和/或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="38fa8-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="38fa8-151">然後立即建立規則。</span><span class="sxs-lookup"><span data-stu-id="38fa8-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="38fa8-152">您無法使用 CLI 將 webhook 或電子郵件與已建立的規則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="38fa8-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="38fa8-153">您可以藉由查看個別規則來確認您的警示已正確建立。</span><span class="sxs-lookup"><span data-stu-id="38fa8-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="38fa8-154">若要刪除規則，使用此格式︰</span><span class="sxs-lookup"><span data-stu-id="38fa8-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="38fa8-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="38fa8-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="38fa8-156">這些命令會刪除本文中先前建立的規則。</span><span class="sxs-lookup"><span data-stu-id="38fa8-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="38fa8-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38fa8-157">Next steps</span></span>
* <span data-ttu-id="38fa8-158">[取得 Azure 監視的概觀](monitoring-overview.md) 中說明您可以收集和監視的資訊類型。</span><span class="sxs-lookup"><span data-stu-id="38fa8-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="38fa8-159">深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="38fa8-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="38fa8-160">深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="38fa8-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="38fa8-161">深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="38fa8-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="38fa8-162">依照 [收集診斷記錄檔概觀](monitoring-overview-of-diagnostic-logs.md) 中的做法，收集您服務中詳細的高頻率計量。</span><span class="sxs-lookup"><span data-stu-id="38fa8-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="38fa8-163">依照 [計量集合概觀](insights-how-to-customize-monitoring.md) 中的做法，確保您的服務可使用且有回應。</span><span class="sxs-lookup"><span data-stu-id="38fa8-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
