---
title: "Azure 監視器 PowerShell 快速入門範例 | Microsoft Docs"
description: "使用 PowerShell 存取 Azure 監視器的功能，例如自動調整、警示、webhook 和搜尋活動記錄檔。"
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="99457-104">Azure 監視器 PowerShell 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="99457-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="99457-105">本文說明可協助您存取 Azure 監視器 功能的範例 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="99457-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="99457-106">Azure 監視器可讓您根據設定的遙測資料值、自動調整雲端服務、虛擬機器和 Web Apps，以及傳送警示通知，或呼叫 Web URL。</span><span class="sxs-lookup"><span data-stu-id="99457-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="99457-107">自 2016 年 9 月 25 日起，「Azure 監視器」是以前所謂「Azure Insights」的新名稱。</span><span class="sxs-lookup"><span data-stu-id="99457-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="99457-108">不過，命名空間和下列命令中仍包含 "insights"。</span><span class="sxs-lookup"><span data-stu-id="99457-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="99457-109">設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="99457-109">Set up PowerShell</span></span>
<span data-ttu-id="99457-110">設定要在電腦上執行的 PowerShell (如果您還未設定)。</span><span class="sxs-lookup"><span data-stu-id="99457-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="99457-111">如需詳細資訊，請參閱[如何安裝及設定 PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="99457-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="99457-112">本文中的範例</span><span class="sxs-lookup"><span data-stu-id="99457-112">Examples in this article</span></span>
<span data-ttu-id="99457-113">本文中的範例將說明如何使用Azure 監視器 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="99457-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="99457-114">您也可以在 [Azure 監視器 Cmdlet](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx) 檢閱整個 Azure 監視器 PowerShell Cmdlet 清單。</span><span class="sxs-lookup"><span data-stu-id="99457-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="99457-115">登入和使用訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="99457-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="99457-116">首先，登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99457-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="99457-117">這會要求您登入。</span><span class="sxs-lookup"><span data-stu-id="99457-117">This requires you to sign in.</span></span> <span data-ttu-id="99457-118">一旦登入之後，就會顯示您的帳戶、TenantID 和預設的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="99457-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="99457-119">所有 Azure Cmdlet 都會在您的預設訂用帳戶內容中運作。</span><span class="sxs-lookup"><span data-stu-id="99457-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="99457-120">若要檢視您具有存取權的訂用帳戶的清單，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="99457-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="99457-121">若要將使用中的內容變更為不同的訂用帳戶，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="99457-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="99457-122">擷取訂用帳戶的活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="99457-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="99457-123">使用 `Get-AzureRmLog` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="99457-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="99457-124">以下是一些常見的範例。</span><span class="sxs-lookup"><span data-stu-id="99457-124">The following are some common examples.</span></span>

<span data-ttu-id="99457-125">取得此時間/日期迄今的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="99457-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="99457-126">取得某個時間/日期範圍間的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="99457-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="99457-127">取得特定資源群組中的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="99457-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="99457-128">從特定的資源提供者取得某個時間/日期範圍間的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="99457-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="99457-129">取得包含特定呼叫者的所有記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="99457-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="99457-130">下列命令會擷取活動記錄檔中的最後 1000 個事件︰</span><span class="sxs-lookup"><span data-stu-id="99457-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="99457-131">`Get-AzureRmLog` 支援其他許多參數。</span><span class="sxs-lookup"><span data-stu-id="99457-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="99457-132">如需詳細資訊，請參閱 `Get-AzureRmLog` 參考。</span><span class="sxs-lookup"><span data-stu-id="99457-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="99457-133">`Get-AzureRmLog` 只提供 15 天的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="99457-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="99457-134">使用 **-MaxEvents** 參數可讓您查詢超過 15 天的前 N 個事件。</span><span class="sxs-lookup"><span data-stu-id="99457-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="99457-135">若要存取 15 天前的事件，請使用 REST API 或 SDK (使用 SDK 的 C# 範例)。</span><span class="sxs-lookup"><span data-stu-id="99457-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="99457-136">如果您未包含 **StartTime**，則預設值是 **EndTime** 減去一小時。</span><span class="sxs-lookup"><span data-stu-id="99457-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="99457-137">如果您未包含 **EndTime**，則預設值是目前的時間。</span><span class="sxs-lookup"><span data-stu-id="99457-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="99457-138">所有時間都是採用 UTC 格式。</span><span class="sxs-lookup"><span data-stu-id="99457-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="99457-139">擷取警示歷程記錄</span><span class="sxs-lookup"><span data-stu-id="99457-139">Retrieve alerts history</span></span>
<span data-ttu-id="99457-140">若要檢視所有警示事件，您可以使用下列範例查詢 Azure Resource Manager 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="99457-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="99457-141">若要檢視特定警示規則的歷程記錄，您可以使用 `Get-AzureRmAlertHistory` Cmdlet，傳入警示規則的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="99457-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="99457-142">`Get-AzureRmAlertHistory` Cmdlet 支援多各種參數。</span><span class="sxs-lookup"><span data-stu-id="99457-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="99457-143">如需詳細資訊，請參閱 [Get AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99457-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="99457-144">擷取警示規則的相關資訊</span><span class="sxs-lookup"><span data-stu-id="99457-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="99457-145">下列所有命令都會處理一個名為 "montest" 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="99457-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="99457-146">檢視警示規則的所有屬性︰</span><span class="sxs-lookup"><span data-stu-id="99457-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="99457-147">擷取資源群組上的所有警示︰</span><span class="sxs-lookup"><span data-stu-id="99457-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="99457-148">擷取針對目標資源設定的所有警示規則。</span><span class="sxs-lookup"><span data-stu-id="99457-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="99457-149">例如，在 VM 上設定的所有警示規則。</span><span class="sxs-lookup"><span data-stu-id="99457-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="99457-150">`Get-AzureRmAlertRule` 支援其他參數。</span><span class="sxs-lookup"><span data-stu-id="99457-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="99457-151">如需詳細資訊，請參閱 [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="99457-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="99457-152">建立計量警示</span><span class="sxs-lookup"><span data-stu-id="99457-152">Create metric alerts</span></span>
<span data-ttu-id="99457-153">您可以使用 `Add-AlertRule` Cmdlet 建立、更新或停用警示規則。</span><span class="sxs-lookup"><span data-stu-id="99457-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="99457-154">您可以分別使用 `New-AzureRmAlertRuleEmail` 和 `New-AzureRmAlertRuleWebhook` 建立電子郵件和 Webhook 屬性。</span><span class="sxs-lookup"><span data-stu-id="99457-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="99457-155">在警示規則 Cmdlet 中，將這些屬性當做動作，指派給警示規則的 [動作]  屬性。</span><span class="sxs-lookup"><span data-stu-id="99457-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="99457-156">下表描述使用計量建立警示所使用的參數和值。</span><span class="sxs-lookup"><span data-stu-id="99457-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="99457-157">參數</span><span class="sxs-lookup"><span data-stu-id="99457-157">parameter</span></span> | <span data-ttu-id="99457-158">value</span><span class="sxs-lookup"><span data-stu-id="99457-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="99457-159">名稱</span><span class="sxs-lookup"><span data-stu-id="99457-159">Name</span></span> |<span data-ttu-id="99457-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="99457-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="99457-161">此警示規則的位置</span><span class="sxs-lookup"><span data-stu-id="99457-161">Location of this alert rule</span></span> |<span data-ttu-id="99457-162">美國東部</span><span class="sxs-lookup"><span data-stu-id="99457-162">East US</span></span> |
| <span data-ttu-id="99457-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="99457-163">ResourceGroup</span></span> |<span data-ttu-id="99457-164">montest</span><span class="sxs-lookup"><span data-stu-id="99457-164">montest</span></span> |
| <span data-ttu-id="99457-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="99457-165">TargetResourceId</span></span> |<span data-ttu-id="99457-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="99457-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="99457-167">所建立警示的 MetricName</span><span class="sxs-lookup"><span data-stu-id="99457-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="99457-168">\PhysicalDisk (_Total) \Disk writes/sec。請參閱`Get-MetricDefinitions`cmdlet 有關如何擷取精確的衡量標準名稱</span><span class="sxs-lookup"><span data-stu-id="99457-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="99457-169">operator</span><span class="sxs-lookup"><span data-stu-id="99457-169">operator</span></span> |<span data-ttu-id="99457-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="99457-170">GreaterThan</span></span> |
| <span data-ttu-id="99457-171">臨界值 (此計量的計數/秒）</span><span class="sxs-lookup"><span data-stu-id="99457-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="99457-172">1</span><span class="sxs-lookup"><span data-stu-id="99457-172">1</span></span> |
| <span data-ttu-id="99457-173">WindowSize (hh:mm:ss 格式)</span><span class="sxs-lookup"><span data-stu-id="99457-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="99457-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="99457-174">00:05:00</span></span> |
| <span data-ttu-id="99457-175">彙總工具 (在此情況為計量的統計資料，其使用平均計數)</span><span class="sxs-lookup"><span data-stu-id="99457-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="99457-176">平均值</span><span class="sxs-lookup"><span data-stu-id="99457-176">Average</span></span> |
| <span data-ttu-id="99457-177">自訂電子郵件 (字串陣列)</span><span class="sxs-lookup"><span data-stu-id="99457-177">custom emails (string array)</span></span> |<span data-ttu-id="99457-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="99457-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="99457-179">傳送電子郵件給擁有者、參與者和讀者</span><span class="sxs-lookup"><span data-stu-id="99457-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="99457-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="99457-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="99457-181">建立電子郵件動作</span><span class="sxs-lookup"><span data-stu-id="99457-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="99457-182">建立 Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="99457-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="99457-183">在傳統 VM 上建立 CPU 百分比計量的警示規則</span><span class="sxs-lookup"><span data-stu-id="99457-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="99457-184">擷取警示規則</span><span class="sxs-lookup"><span data-stu-id="99457-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="99457-185">如果指定屬性的警示規則已存在，Add alert Cmdlet 也會更新規則。</span><span class="sxs-lookup"><span data-stu-id="99457-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="99457-186">若要停用警示規則，請加上參數 **-DisableRule**。</span><span class="sxs-lookup"><span data-stu-id="99457-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="99457-187">取得可用警示計量的清單</span><span class="sxs-lookup"><span data-stu-id="99457-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="99457-188">您可以使用 `Get-AzureRmMetricDefinition` Cmdlet 檢視特定資源的所有計量的清單。</span><span class="sxs-lookup"><span data-stu-id="99457-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="99457-189">下列範例會產生包含計量名稱及其單位的資料表。</span><span class="sxs-lookup"><span data-stu-id="99457-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="99457-190">`Get-AzureRmMetricDefinition` 的可用選項完整清單可在 [Get MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx)取得。</span><span class="sxs-lookup"><span data-stu-id="99457-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="99457-191">建立和管理自動調整設定</span><span class="sxs-lookup"><span data-stu-id="99457-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="99457-192">諸如 Web 應用程式、VM、雲端服務或虛擬機器擴展集之類的資源只能設定一個自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="99457-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="99457-193">不過，每個自動調整設定都可以有多個設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="99457-194">例如，一個用於以效能為基礎的調整設定檔，以及一個用於以排程為基礎的設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="99457-195">每個設定檔都可以設定多個規則。</span><span class="sxs-lookup"><span data-stu-id="99457-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="99457-196">如需有關自動調整的詳細資訊，請參閱 [如何自動調整應用程式](../cloud-services/cloud-services-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="99457-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="99457-197">以下是我們將使用的步驟：</span><span class="sxs-lookup"><span data-stu-id="99457-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="99457-198">建立規則。</span><span class="sxs-lookup"><span data-stu-id="99457-198">Create rule(s).</span></span>
2. <span data-ttu-id="99457-199">建立將您先前所建立的規則對應到設定檔的設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="99457-200">選擇性︰設定 Webhook 和電子郵件的屬性，以建立自動調整的通知。</span><span class="sxs-lookup"><span data-stu-id="99457-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="99457-201">藉由對應您在先前步驟中建立的設定檔和通知，使用目標資源上的名稱建立自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="99457-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="99457-202">下列範例將示範如何使用 CPU 使用率計量，為 Windows 作業系統的虛擬機器擴展集建立自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="99457-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="99457-203">首先，建立相應放大的規則，讓執行個體計數增加。</span><span class="sxs-lookup"><span data-stu-id="99457-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="99457-204">接著，建立相應縮小的規則，讓執行個體計數減少。</span><span class="sxs-lookup"><span data-stu-id="99457-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="99457-205">然後，建立規則的設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="99457-206">建立 Webhook 屬性。</span><span class="sxs-lookup"><span data-stu-id="99457-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="99457-207">建立自動調整設定的通知屬性，包括您先前建立的電子郵件與 Webhook。</span><span class="sxs-lookup"><span data-stu-id="99457-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="99457-208">最後，建立自動調整設定來新增您在以上建立的設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="99457-209">如需有關管理自動調整設定的詳細資訊，請參閱 [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99457-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="99457-210">自動調整歷程記錄</span><span class="sxs-lookup"><span data-stu-id="99457-210">Autoscale history</span></span>
<span data-ttu-id="99457-211">下列範例示範如何檢視最新的自動調整和警示的事件。</span><span class="sxs-lookup"><span data-stu-id="99457-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="99457-212">使用活動記錄檔搜尋檢視自動調整歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="99457-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="99457-213">您可以使用 `Get-AzureRmAutoScaleHistory` Cmdlet 擷取自動調整歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="99457-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="99457-214">如需詳細資訊，請參閱 [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99457-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="99457-215">檢視自動調整設定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="99457-215">View details for an autoscale setting</span></span>
<span data-ttu-id="99457-216">您可以使用 `Get-Autoscalesetting` Cmdlet 擷取有關自動調整設定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="99457-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="99457-217">下列範例會顯示資源群組 'myrg1' 中所有自動調整設定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="99457-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="99457-218">下列範例會顯示資源群組 'myrg1' 中所有自動調整設定的詳細資料，尤其是名為 'MyScaleVMSSSetting' 的自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="99457-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="99457-219">移除自動調整設定</span><span class="sxs-lookup"><span data-stu-id="99457-219">Remove an autoscale setting</span></span>
<span data-ttu-id="99457-220">您可以使用 `Remove-Autoscalesetting` Cmdlet 刪除自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="99457-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="99457-221">管理活動記錄檔的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="99457-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="99457-222">您可以建立*記錄檔設定檔*，並將資料從活動記錄檔匯出至儲存體帳戶，而且您可以為其設定資料保留期。</span><span class="sxs-lookup"><span data-stu-id="99457-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="99457-223">或者，您也可以將資料串流至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="99457-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="99457-224">請注意，此功能目前處於預覽狀態，而且每個訂用帳戶只能建立一個記錄檔設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="99457-225">您可以使用下列 Cmdlet 搭配您目前的訂用帳戶來建立和管理記錄檔設定檔。</span><span class="sxs-lookup"><span data-stu-id="99457-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="99457-226">您也可以選擇特定的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="99457-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="99457-227">PowerShell 預設為目前的訂用帳戶，但是您隨時可以使用 `Set-AzureRmContext`加以變更。</span><span class="sxs-lookup"><span data-stu-id="99457-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="99457-228">您可以設定活動記錄檔，將資料路由至任何儲存體帳戶或該訂用帳戶內的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="99457-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="99457-229">資料會以 JSON 格式的 Blob 檔案寫入。</span><span class="sxs-lookup"><span data-stu-id="99457-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="99457-230">取得記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="99457-230">Get a log profile</span></span>
<span data-ttu-id="99457-231">若要擷取現有的記錄檔設定檔，請使用 `Get-AzureRmLogProfile` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="99457-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="99457-232">新增沒有資料保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="99457-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="99457-233">移除記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="99457-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="99457-234">新增包含資料保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="99457-234">Add a log profile with data retention</span></span>
<span data-ttu-id="99457-235">您可以使用保留資料的天數，以正整數指定 **-RetentionInDays** 屬性。</span><span class="sxs-lookup"><span data-stu-id="99457-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="99457-236">新增包含保留期與 EventHub 的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="99457-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="99457-237">除了將資料路由至儲存體帳戶之外，您也可以將它串流到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="99457-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="99457-238">請注意，在此預覽版本中，儲存體帳戶設定是強制性的，但事件中樞設定則是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="99457-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="99457-239">設定診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="99457-239">Configure diagnostics logs</span></span>
<span data-ttu-id="99457-240">許多 Azure 服務都提供額外的記錄檔和遙測，並可設定為將資料儲存在 Azure 儲存體帳戶、傳送至事件中樞，和/或傳送到 OMS Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="99457-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="99457-241">該作業只能在資源層級執行，而且儲存體帳戶或事件中樞應該存在於進行診斷設定所在目標資源的相同區域中。</span><span class="sxs-lookup"><span data-stu-id="99457-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="99457-242">取得診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="99457-243">停用診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="99457-244">啟用不含保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="99457-245">啟用含保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="99457-246">針對特定的記錄檔類別，啟用含保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="99457-247">啟用事件中樞的診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="99457-248">啟用 OMS 的診斷設定</span><span class="sxs-lookup"><span data-stu-id="99457-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
