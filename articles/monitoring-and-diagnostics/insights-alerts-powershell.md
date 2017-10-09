---
title: "Azure 服務-PowerShell aaaCreate 警示 |Microsoft 文件"
description: "符合您指定的 hello 條件時，觸發程序的電子郵件，通知，便會呼叫網站 Url (webhook) 或自動化。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="f06ed-103">在 Azure 監視器中為 Azure 服務建立計量警示 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06ed-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f06ed-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="f06ed-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="f06ed-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06ed-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="f06ed-106">CLI</span><span class="sxs-lookup"><span data-stu-id="f06ed-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="f06ed-107">概觀</span><span class="sxs-lookup"><span data-stu-id="f06ed-107">Overview</span></span>
<span data-ttu-id="f06ed-108">本文將說明如何註冊 Azure 度量 tooset 警示使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f06ed-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="f06ed-109">您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="f06ed-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="f06ed-110">**度量值**-hello hello 值，指定的度量超出您在任一方向中指派的閾值時，警示觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f06ed-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="f06ed-111">也就是說，它會觸發兩者當第一次符合 hello 條件，並且再之後時，條件不再達成。</span><span class="sxs-lookup"><span data-stu-id="f06ed-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="f06ed-112">**活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。</span><span class="sxs-lookup"><span data-stu-id="f06ed-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="f06ed-113">深入了解活動記錄檔警示 toolearn[按一下這裡](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f06ed-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="f06ed-114">您可以設定警示的度量 toodo hello 時，下列觸發：</span><span class="sxs-lookup"><span data-stu-id="f06ed-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="f06ed-115">傳送電子郵件通知 toohello 服務管理員和共同管理員</span><span class="sxs-lookup"><span data-stu-id="f06ed-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="f06ed-116">您指定的 tooadditional 電子郵件傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f06ed-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="f06ed-117">呼叫 webhook</span><span class="sxs-lookup"><span data-stu-id="f06ed-117">call a webhook</span></span>
* <span data-ttu-id="f06ed-118">開始執行的 Azure runbook （只能從 hello Azure 入口網站)</span><span class="sxs-lookup"><span data-stu-id="f06ed-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="f06ed-119">您可以透過下列方式設定和取得有關警示規則的資訊</span><span class="sxs-lookup"><span data-stu-id="f06ed-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="f06ed-120">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f06ed-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="f06ed-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06ed-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="f06ed-122">命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="f06ed-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="f06ed-123">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="f06ed-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="f06ed-124">如需詳細資訊，您可以一律輸入```Get-Help```，然後 hello 您想要說明的 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="f06ed-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="f06ed-125">在 PowerShell 中建立警示規則</span><span class="sxs-lookup"><span data-stu-id="f06ed-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="f06ed-126">登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="f06ed-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="f06ed-127">取得清單的 hello 訂閱您可以使用。</span><span class="sxs-lookup"><span data-stu-id="f06ed-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="f06ed-128">請確認您使用與 hello 右訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f06ed-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="f06ed-129">如果沒有，請將它設定 toohello 右移一個使用 hello 輸出`Get-AzureRmSubscription`。</span><span class="sxs-lookup"><span data-stu-id="f06ed-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="f06ed-130">在資源群組中，下列命令使用 hello toolist 現有規則：</span><span class="sxs-lookup"><span data-stu-id="f06ed-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="f06ed-131">toocreate 規則，您需要 toohave 數個重要的資訊片段第一次。</span><span class="sxs-lookup"><span data-stu-id="f06ed-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="f06ed-132">hello**資源識別碼**hello 資源要 tooset 的警示</span><span class="sxs-lookup"><span data-stu-id="f06ed-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="f06ed-133">hello**度量定義**可用於該項資源</span><span class="sxs-lookup"><span data-stu-id="f06ed-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="f06ed-134">其中一種方式 tooget hello 資源識別碼為 toouse hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f06ed-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="f06ed-135">假設已經建立 hello 資源時，在 hello 入口網站中選取它。</span><span class="sxs-lookup"><span data-stu-id="f06ed-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="f06ed-136">然後在 [hello 下一步] 刀鋒視窗中，選取*屬性*下 hello*設定*> 一節。</span><span class="sxs-lookup"><span data-stu-id="f06ed-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="f06ed-137">**資源識別碼**是在 hello 下一步 刀鋒視窗中的欄位。</span><span class="sxs-lookup"><span data-stu-id="f06ed-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="f06ed-138">另一種方式為 toouse hello [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="f06ed-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="f06ed-139">以下是 Web 應用程式的範例資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="f06ed-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="f06ed-140">您可以使用`Get-AzureRmMetricDefinition`tooview hello 清單的特定資源的所有標準定義。</span><span class="sxs-lookup"><span data-stu-id="f06ed-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="f06ed-141">hello 下列範例會產生包含 hello 度量名稱的資料表和 hello 單位，該度量。</span><span class="sxs-lookup"><span data-stu-id="f06ed-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="f06ed-142">執行 Get-MetricDefinitions 可取得 Get-AzureRmMetricDefinition 的可用選項完整清單。</span><span class="sxs-lookup"><span data-stu-id="f06ed-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="f06ed-143">下列範例設定警示的網站資源上的 hello。</span><span class="sxs-lookup"><span data-stu-id="f06ed-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="f06ed-144">hello 警示觸發程序每當它以一致的方式接收任何流量 5 分鐘，一次當它收到沒有流量 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f06ed-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="f06ed-145">toocreate webhook 或傳送電子郵件時警示觸發時，會先建立 hello 電子郵件和/或 webhook。</span><span class="sxs-lookup"><span data-stu-id="f06ed-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="f06ed-146">立即建立 hello 規則之後 hello-動作標記和 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="f06ed-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="f06ed-147">您無法透過 PowerShell 將 webhook 或電子郵件與已建立的規則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="f06ed-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="f06ed-148">tooverify 警示有已正確建立藉由查看 hello 個別規則。</span><span class="sxs-lookup"><span data-stu-id="f06ed-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="f06ed-149">刪除您的警示。</span><span class="sxs-lookup"><span data-stu-id="f06ed-149">Delete your alerts.</span></span> <span data-ttu-id="f06ed-150">這些命令會刪除先前建立本文章中的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="f06ed-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="f06ed-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f06ed-151">Next steps</span></span>
* <span data-ttu-id="f06ed-152">[取得的 Azure 監視概觀](monitoring-overview.md)包括 hello 類型的資訊，您可以收集和監視。</span><span class="sxs-lookup"><span data-stu-id="f06ed-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="f06ed-153">深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="f06ed-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="f06ed-154">深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="f06ed-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="f06ed-155">深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="f06ed-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="f06ed-156">取得[收集診斷記錄檔的概觀](monitoring-overview-of-diagnostic-logs.md)toocollect 詳細高頻率度量，您的服務。</span><span class="sxs-lookup"><span data-stu-id="f06ed-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f06ed-157">取得[概觀度量收集](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="f06ed-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
