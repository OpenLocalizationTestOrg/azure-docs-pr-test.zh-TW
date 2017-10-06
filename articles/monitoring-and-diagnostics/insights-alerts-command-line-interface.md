---
title: "Azure 服務的跨平台 CLI aaaCreate 警示 |Microsoft 文件"
description: "符合您指定的 hello 條件時，觸發程序的電子郵件，通知，便會呼叫網站 Url (webhook) 或自動化。"
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
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="b0503-103">在 Azure 監視器中為 Azure 服務建立計量警示 - 跨平台 CLI</span><span class="sxs-lookup"><span data-stu-id="b0503-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0503-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="b0503-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="b0503-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0503-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="b0503-106">CLI</span><span class="sxs-lookup"><span data-stu-id="b0503-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="b0503-107">概觀</span><span class="sxs-lookup"><span data-stu-id="b0503-107">Overview</span></span>
<span data-ttu-id="b0503-108">本文章將示範如何使用 Azure 的度量警示 tooset hello 跨平台命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="b0503-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="b0503-109">Azure 的監視是 hello 所謂 「 Azure Insights"的新名稱，直到 2016 年 9 月 25 日。</span><span class="sxs-lookup"><span data-stu-id="b0503-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="b0503-110">不過，hello 命名空間，因此下列 hello 命令仍包含 hello"見解"。</span><span class="sxs-lookup"><span data-stu-id="b0503-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="b0503-111">您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="b0503-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="b0503-112">**度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。</span><span class="sxs-lookup"><span data-stu-id="b0503-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="b0503-113">也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。</span><span class="sxs-lookup"><span data-stu-id="b0503-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="b0503-114">**活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。</span><span class="sxs-lookup"><span data-stu-id="b0503-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="b0503-115">深入了解活動記錄檔警示 toolearn[按一下這裡](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="b0503-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="b0503-116">您可以設定警示的度量 toodo hello 時，下列觸發：</span><span class="sxs-lookup"><span data-stu-id="b0503-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="b0503-117">傳送電子郵件通知 toohello 服務管理員和共同管理員</span><span class="sxs-lookup"><span data-stu-id="b0503-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="b0503-118">您指定的 tooadditional 電子郵件傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b0503-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="b0503-119">呼叫 webhook</span><span class="sxs-lookup"><span data-stu-id="b0503-119">call a webhook</span></span>
* <span data-ttu-id="b0503-120">開始執行的 Azure runbook （只能從 hello Azure 入口網站在此階段)</span><span class="sxs-lookup"><span data-stu-id="b0503-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="b0503-121">您可以透過下列方式設定和取得有關計量警示規則的資訊</span><span class="sxs-lookup"><span data-stu-id="b0503-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="b0503-122">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b0503-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="b0503-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0503-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="b0503-124">命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="b0503-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="b0503-125">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="b0503-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="b0503-126">您一律可以收到的命令說明輸入命令，並將-協助 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="b0503-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="b0503-127">例如：</span><span class="sxs-lookup"><span data-stu-id="b0503-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="b0503-128">建立使用 hello CLI 的警示規則</span><span class="sxs-lookup"><span data-stu-id="b0503-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="b0503-129">執行 hello 必要條件和登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="b0503-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="b0503-130">請參閱 [Azure 監視器 CLI 範例](insights-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b0503-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="b0503-131">簡單地說，安裝 hello CLI，並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="b0503-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="b0503-132">它們可以獲得您登入，顯示您正在使用，並讓您準備 toorun Azure 監視器命令什麼訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0503-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="b0503-133">toolist 現有規則上的資源群組中，使用下列格式的 hello**警示規則清單的 azure insights** *[選項] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="b0503-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="b0503-134">toocreate 規則，您需要 toohave 數個重要的資訊片段第一次。</span><span class="sxs-lookup"><span data-stu-id="b0503-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="b0503-135">hello**資源識別碼**hello 資源要 tooset 的警示</span><span class="sxs-lookup"><span data-stu-id="b0503-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="b0503-136">hello**度量定義**可用於該項資源</span><span class="sxs-lookup"><span data-stu-id="b0503-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="b0503-137">其中一種方式 tooget hello 資源識別碼為 toouse hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b0503-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="b0503-138">假設已經建立 hello 資源時，在 hello 入口網站中選取它。</span><span class="sxs-lookup"><span data-stu-id="b0503-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="b0503-139">然後在 [hello 下一步] 刀鋒視窗中，選取*屬性*下 hello*設定*> 一節。</span><span class="sxs-lookup"><span data-stu-id="b0503-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="b0503-140">hello*資源識別碼*是在 hello 下一步 刀鋒視窗中的欄位。</span><span class="sxs-lookup"><span data-stu-id="b0503-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="b0503-141">另一種方式為 toouse hello [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b0503-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="b0503-142">以下是 Web 應用程式的範例資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="b0503-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="b0503-143">tooget hello 可用的度量和 hello 上述資源範例中，使用下列 CLI 命令的 hello 這些度量單位的清單：</span><span class="sxs-lookup"><span data-stu-id="b0503-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="b0503-144">*PT1M*是 hello 資料粒度的 hello 可用度量 （每隔 1 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="b0503-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="b0503-145">使用不同的資料粒度可提供您不同的計量選項。</span><span class="sxs-lookup"><span data-stu-id="b0503-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="b0503-146">toocreate 標準為基礎的警示規則，使用下列形式的 hello 的命令：</span><span class="sxs-lookup"><span data-stu-id="b0503-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="b0503-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="b0503-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="b0503-148">下列範例設定警示的網站資源上的 hello。</span><span class="sxs-lookup"><span data-stu-id="b0503-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="b0503-149">hello 警示觸發程序每當它以一致的方式接收任何流量 5 分鐘，一次當它收到沒有流量 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b0503-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="b0503-150">toocreate webhook 或傳送電子郵件時度量的警示引發時，會先建立 hello 電子郵件和/或 webhook。</span><span class="sxs-lookup"><span data-stu-id="b0503-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="b0503-151">然後立即建立 hello 規則之後。</span><span class="sxs-lookup"><span data-stu-id="b0503-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="b0503-152">您無法將 webhook 或電子郵件與已建立使用 hello CLI 規則。</span><span class="sxs-lookup"><span data-stu-id="b0503-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="b0503-153">您可以藉由查看個別規則來確認您的警示已正確建立。</span><span class="sxs-lookup"><span data-stu-id="b0503-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="b0503-154">toodelete 規則使用 hello 格式的命令：</span><span class="sxs-lookup"><span data-stu-id="b0503-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="b0503-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="b0503-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="b0503-156">這些命令會刪除先前建立的這篇文章中的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="b0503-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="b0503-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0503-157">Next steps</span></span>
* <span data-ttu-id="b0503-158">[取得的 Azure 監視概觀](monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。</span><span class="sxs-lookup"><span data-stu-id="b0503-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="b0503-159">深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="b0503-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="b0503-160">深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="b0503-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="b0503-161">深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="b0503-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b0503-162">取得[收集診斷記錄檔的概觀](monitoring-overview-of-diagnostic-logs.md)toocollect 詳細高頻率度量，您的服務。</span><span class="sxs-lookup"><span data-stu-id="b0503-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="b0503-163">取得[概觀度量收集](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="b0503-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
