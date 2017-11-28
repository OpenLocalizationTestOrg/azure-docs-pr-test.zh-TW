---
title: "建立 Azure 服務的警示 - PowerShell | Microsoft Docs"
description: "當符合您指定的條件時，觸發電子郵件、通知、呼叫網站 URL (Webhook) 或自動化。"
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
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="39366-103">在 Azure 監視器中為 Azure 服務建立計量警示 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="39366-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39366-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="39366-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="39366-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39366-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="39366-106">CLI</span><span class="sxs-lookup"><span data-stu-id="39366-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="39366-107">概觀</span><span class="sxs-lookup"><span data-stu-id="39366-107">Overview</span></span>
<span data-ttu-id="39366-108">此文章說明如何使用 PowerShell 設定 Azure 計量警示。</span><span class="sxs-lookup"><span data-stu-id="39366-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="39366-109">您可以收到以您 Azure 服務的監視計量或事件為基礎的警示。</span><span class="sxs-lookup"><span data-stu-id="39366-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="39366-110">**計量值** - 當指定的計量值超出您在任一方向指派的臨界值時會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="39366-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="39366-111">也就是說，當先符合條件而之後該條件不再符合時，兩方面皆會觸發。</span><span class="sxs-lookup"><span data-stu-id="39366-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="39366-112">**活動記錄檔事件** - 警示可在*每一個*事件上觸發，或是僅在發生特定事件時才觸發。</span><span class="sxs-lookup"><span data-stu-id="39366-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="39366-113">若要深入了解活動記錄檔警示，請[按一下這裡](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="39366-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="39366-114">您可以設定當計量警示觸發時執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="39366-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="39366-115">傳送電子郵件給服務管理員和共同管理員</span><span class="sxs-lookup"><span data-stu-id="39366-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="39366-116">傳送電子郵件至您指定的其他電子郵件</span><span class="sxs-lookup"><span data-stu-id="39366-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="39366-117">呼叫 webhook</span><span class="sxs-lookup"><span data-stu-id="39366-117">call a webhook</span></span>
* <span data-ttu-id="39366-118">啟動執行 Azure Runbook (現階段只能從 Azure 入口網站啟動)</span><span class="sxs-lookup"><span data-stu-id="39366-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="39366-119">您可以透過下列方式設定和取得有關警示規則的資訊</span><span class="sxs-lookup"><span data-stu-id="39366-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="39366-120">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="39366-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="39366-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39366-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="39366-122">命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="39366-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="39366-123">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="39366-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="39366-124">如需詳細資訊，您可以輸入 ```Get-Help``` ，即可得到所需 PowerShell 命令的說明。</span><span class="sxs-lookup"><span data-stu-id="39366-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="39366-125">在 PowerShell 中建立警示規則</span><span class="sxs-lookup"><span data-stu-id="39366-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="39366-126">登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="39366-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="39366-127">取得您可使用的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="39366-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="39366-128">確認您使用正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="39366-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="39366-129">若不是，使用 `Get-AzureRmSubscription`的輸出將它設為正確帳戶。</span><span class="sxs-lookup"><span data-stu-id="39366-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="39366-130">若要列出資源群組上的現有規則，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="39366-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="39366-131">若要建立規則，您需要先取得幾項重要資訊：</span><span class="sxs-lookup"><span data-stu-id="39366-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="39366-132">您想要為其設定警示的 **資源識別碼**</span><span class="sxs-lookup"><span data-stu-id="39366-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="39366-133">該資源可使用的 **計量定義**</span><span class="sxs-lookup"><span data-stu-id="39366-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="39366-134">取得資源識別碼的方法之一，是使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="39366-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="39366-135">假設已建立資源，在入口網站中選取它。</span><span class="sxs-lookup"><span data-stu-id="39366-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="39366-136">然後在下一個刀鋒視窗中，選取 [設定] 區段下的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="39366-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="39366-137">[資源識別碼] 是下一個刀鋒視窗中的欄位。</span><span class="sxs-lookup"><span data-stu-id="39366-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="39366-138">另一種方法是使用 [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="39366-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="39366-139">以下是 Web 應用程式的範例資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="39366-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="39366-140">您可以使用 `Get-AzureRmMetricDefinition` 檢視特定資源的所有計量定義的清單。</span><span class="sxs-lookup"><span data-stu-id="39366-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="39366-141">下列範例會產生資料表，其中有計量名稱及該計量的單位。</span><span class="sxs-lookup"><span data-stu-id="39366-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="39366-142">執行 Get-MetricDefinitions 可取得 Get-AzureRmMetricDefinition 的可用選項完整清單。</span><span class="sxs-lookup"><span data-stu-id="39366-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="39366-143">下列範例會設定網站資源的警示。</span><span class="sxs-lookup"><span data-stu-id="39366-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="39366-144">只要持續 5 分鐘有收到任何流量，就會觸發警示，在這之後，5 分鐘沒收到任何流量也會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="39366-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="39366-145">若要在警示觸發時建立 webhook 或傳送電子郵件，請先建立電子郵件和/或 webhook。</span><span class="sxs-lookup"><span data-stu-id="39366-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="39366-146">然後使用 -Actions 標籤立即建立規則，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="39366-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="39366-147">您無法透過 PowerShell 將 webhook 或電子郵件與已建立的規則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="39366-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="39366-148">查看個別規則，以確認您已正確建立警示。</span><span class="sxs-lookup"><span data-stu-id="39366-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="39366-149">刪除您的警示。</span><span class="sxs-lookup"><span data-stu-id="39366-149">Delete your alerts.</span></span> <span data-ttu-id="39366-150">這些命令會刪除本文中先前建立的規則。</span><span class="sxs-lookup"><span data-stu-id="39366-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="39366-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39366-151">Next steps</span></span>
* <span data-ttu-id="39366-152">[取得 Azure 監視的概觀](monitoring-overview.md) 中說明您可以收集和監視的資訊類型。</span><span class="sxs-lookup"><span data-stu-id="39366-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="39366-153">深入了解 [在警示中設定 webhook](insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="39366-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="39366-154">深入了解[在活動記錄檔事件上設定警示](monitoring-activity-log-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="39366-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="39366-155">深入了解 [Azure 自動化 Runbook](../automation/automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="39366-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="39366-156">依照 [收集診斷記錄檔概觀](monitoring-overview-of-diagnostic-logs.md) 中的做法，收集您服務中詳細的高頻率計量。</span><span class="sxs-lookup"><span data-stu-id="39366-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="39366-157">依照 [計量集合概觀](insights-how-to-customize-monitoring.md) 中的做法，確保您的服務可使用且有回應。</span><span class="sxs-lookup"><span data-stu-id="39366-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
