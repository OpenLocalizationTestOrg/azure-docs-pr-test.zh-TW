---
title: "aaaAzure 監視 PowerShell 快速入門範例。 | Microsoft Docs"
description: "使用 PowerShell tooaccess Azure 監視功能，例如自動調整規模、 警示、 webhook 和搜尋活動記錄檔。"
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="0942d-104">Azure 監視器 PowerShell 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="0942d-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="0942d-105">此發行項會顯示範例 PowerShell 命令 toohelp 您存取 Azure 監視功能。</span><span class="sxs-lookup"><span data-stu-id="0942d-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="0942d-106">Azure 監視器可讓您 tooAutoScale 雲端服務、 虛擬機器和 Web 應用程式和 toosend 警示通知或呼叫 web Url 根據設定的遙測資料的值。</span><span class="sxs-lookup"><span data-stu-id="0942d-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="0942d-107">Azure 的監視是 hello 所謂 「 Azure Insights"的新名稱，直到 2016 年 9 月 25 日。</span><span class="sxs-lookup"><span data-stu-id="0942d-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="0942d-108">不過，hello 命名空間，因此 hello 遵循命令仍包含 hello"見解"。</span><span class="sxs-lookup"><span data-stu-id="0942d-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="0942d-109">設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="0942d-109">Set up PowerShell</span></span>
<span data-ttu-id="0942d-110">如果您還沒有這麼做，設定您的電腦上的 PowerShell toorun。</span><span class="sxs-lookup"><span data-stu-id="0942d-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="0942d-111">如需詳細資訊，請參閱[如何 tooInstall 和設定 PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0942d-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="0942d-112">本文中的範例</span><span class="sxs-lookup"><span data-stu-id="0942d-112">Examples in this article</span></span>
<span data-ttu-id="0942d-113">hello 文件中的 hello 範例說明如何使用 Azure 監視器 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0942d-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="0942d-114">您也可以檢閱 hello Azure 監視 PowerShell cmdlet，在整個清單[Azure 監視器 （深入剖析） Cmdlet](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0942d-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="0942d-115">登入和使用訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0942d-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="0942d-116">首先，登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0942d-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="0942d-117">這需要您 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="0942d-117">This requires you toosign in.</span></span> <span data-ttu-id="0942d-118">一旦登入之後，就會顯示您的帳戶、TenantID 和預設的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="0942d-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="0942d-119">所有 hello Azure cmdlet hello 內容的預設訂用帳戶中的工作。</span><span class="sxs-lookup"><span data-stu-id="0942d-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="0942d-120">您擁有存取權的訂用帳戶 tooview hello 清單，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="0942d-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="0942d-121">toochange 您工作內容 tooa 不同訂用帳戶，下列命令使用 hello。</span><span class="sxs-lookup"><span data-stu-id="0942d-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="0942d-122">擷取訂用帳戶的活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="0942d-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="0942d-123">使用 hello `Get-AzureRmLog` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0942d-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="0942d-124">hello 以下是一些常見的範例。</span><span class="sxs-lookup"><span data-stu-id="0942d-124">hello following are some common examples.</span></span>

<span data-ttu-id="0942d-125">從這個日期/時間 toopresent 取得記錄項目：</span><span class="sxs-lookup"><span data-stu-id="0942d-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="0942d-126">取得某個時間/日期範圍間的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="0942d-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="0942d-127">取得特定資源群組中的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="0942d-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="0942d-128">從特定的資源提供者取得某個時間/日期範圍間的記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="0942d-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="0942d-129">取得包含特定呼叫者的所有記錄檔項目︰</span><span class="sxs-lookup"><span data-stu-id="0942d-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="0942d-130">下列命令擷取 hello hello 活動記錄檔中的最近 1000 則事件 hello:</span><span class="sxs-lookup"><span data-stu-id="0942d-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="0942d-131">`Get-AzureRmLog` 支援其他許多參數。</span><span class="sxs-lookup"><span data-stu-id="0942d-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="0942d-132">請參閱 hello`Get-AzureRmLog`參考，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0942d-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="0942d-133">`Get-AzureRmLog` 只提供 15 天的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0942d-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="0942d-134">使用 hello **-MaxEvents**參數可讓您 tooquery hello 最後 n 個事件，超過 15 天。</span><span class="sxs-lookup"><span data-stu-id="0942d-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="0942d-135">tooaccess 事件超過 15 天，都會使用 hello REST API 或 SDK （C# 範例使用 hello SDK）。</span><span class="sxs-lookup"><span data-stu-id="0942d-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="0942d-136">如果您未包含**StartTime**，hello 預設值為**EndTime**減一小時。</span><span class="sxs-lookup"><span data-stu-id="0942d-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="0942d-137">如果您未包含**EndTime**，hello 預設值為目前的時間。</span><span class="sxs-lookup"><span data-stu-id="0942d-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="0942d-138">所有時間都是採用 UTC 格式。</span><span class="sxs-lookup"><span data-stu-id="0942d-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="0942d-139">擷取警示歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0942d-139">Retrieve alerts history</span></span>
<span data-ttu-id="0942d-140">所有警示的事件，您可以查詢的 tooview hello Azure 資源管理員記錄檔使用 hello 遵循範例。</span><span class="sxs-lookup"><span data-stu-id="0942d-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="0942d-141">tooview hello 記錄特定警示的規則，您可以使用 hello `Get-AzureRmAlertHistory` cmdlet，傳入 hello hello 警示規則的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="0942d-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="0942d-142">hello`Get-AzureRmAlertHistory`指令程式支援各種不同的參數。</span><span class="sxs-lookup"><span data-stu-id="0942d-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="0942d-143">如需詳細資訊，請參閱 [Get AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0942d-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="0942d-144">擷取警示規則的相關資訊</span><span class="sxs-lookup"><span data-stu-id="0942d-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="0942d-145">所有的下列命令的 hello 作用於名為"montest"的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0942d-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="0942d-146">檢視所有 hello 屬性 hello 警示規則：</span><span class="sxs-lookup"><span data-stu-id="0942d-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="0942d-147">擷取資源群組上的所有警示︰</span><span class="sxs-lookup"><span data-stu-id="0942d-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="0942d-148">擷取針對目標資源設定的所有警示規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="0942d-149">例如，在 VM 上設定的所有警示規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="0942d-150">`Get-AzureRmAlertRule` 支援其他參數。</span><span class="sxs-lookup"><span data-stu-id="0942d-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="0942d-151">如需詳細資訊，請參閱 [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="0942d-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="0942d-152">建立計量警示</span><span class="sxs-lookup"><span data-stu-id="0942d-152">Create metric alerts</span></span>
<span data-ttu-id="0942d-153">您可以使用 hello `Add-AlertRule` cmdlet toocreate 更新或停用警示規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="0942d-154">您可以分別使用 `New-AzureRmAlertRuleEmail` 和 `New-AzureRmAlertRuleWebhook` 建立電子郵件和 Webhook 屬性。</span><span class="sxs-lookup"><span data-stu-id="0942d-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="0942d-155">在 hello 警示規則的 cmdlet，將指派為動作 toohello**動作**hello 警示規則的屬性。</span><span class="sxs-lookup"><span data-stu-id="0942d-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="0942d-156">hello 下表描述 hello 參數，以及值使用的 toocreate 使用度量的警示。</span><span class="sxs-lookup"><span data-stu-id="0942d-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="0942d-157">參數</span><span class="sxs-lookup"><span data-stu-id="0942d-157">parameter</span></span> | <span data-ttu-id="0942d-158">value</span><span class="sxs-lookup"><span data-stu-id="0942d-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="0942d-159">名稱</span><span class="sxs-lookup"><span data-stu-id="0942d-159">Name</span></span> |<span data-ttu-id="0942d-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="0942d-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="0942d-161">此警示規則的位置</span><span class="sxs-lookup"><span data-stu-id="0942d-161">Location of this alert rule</span></span> |<span data-ttu-id="0942d-162">美國東部</span><span class="sxs-lookup"><span data-stu-id="0942d-162">East US</span></span> |
| <span data-ttu-id="0942d-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0942d-163">ResourceGroup</span></span> |<span data-ttu-id="0942d-164">montest</span><span class="sxs-lookup"><span data-stu-id="0942d-164">montest</span></span> |
| <span data-ttu-id="0942d-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="0942d-165">TargetResourceId</span></span> |<span data-ttu-id="0942d-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="0942d-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="0942d-167">MetricName hello 警示所建立的</span><span class="sxs-lookup"><span data-stu-id="0942d-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="0942d-168">\PhysicalDisk (_Total) \Disk writes/sec。請參閱 hello `Get-MetricDefinitions` cmdlet 關於 tooretrieve hello 確切的度量名稱的方式</span><span class="sxs-lookup"><span data-stu-id="0942d-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="0942d-169">operator</span><span class="sxs-lookup"><span data-stu-id="0942d-169">operator</span></span> |<span data-ttu-id="0942d-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="0942d-170">GreaterThan</span></span> |
| <span data-ttu-id="0942d-171">臨界值 (此計量的計數/秒）</span><span class="sxs-lookup"><span data-stu-id="0942d-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="0942d-172">1</span><span class="sxs-lookup"><span data-stu-id="0942d-172">1</span></span> |
| <span data-ttu-id="0942d-173">WindowSize (hh:mm:ss 格式)</span><span class="sxs-lookup"><span data-stu-id="0942d-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="0942d-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="0942d-174">00:05:00</span></span> |
| <span data-ttu-id="0942d-175">彙總工具 （hello 標準，在此情況下使用平均計數的統計資料）</span><span class="sxs-lookup"><span data-stu-id="0942d-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="0942d-176">平均值</span><span class="sxs-lookup"><span data-stu-id="0942d-176">Average</span></span> |
| <span data-ttu-id="0942d-177">自訂電子郵件 (字串陣列)</span><span class="sxs-lookup"><span data-stu-id="0942d-177">custom emails (string array)</span></span> |<span data-ttu-id="0942d-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="0942d-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="0942d-179">傳送電子郵件 tooowners、 參與者與讀者</span><span class="sxs-lookup"><span data-stu-id="0942d-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="0942d-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="0942d-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="0942d-181">建立電子郵件動作</span><span class="sxs-lookup"><span data-stu-id="0942d-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="0942d-182">建立 Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="0942d-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="0942d-183">在傳統的 VM 上的 hello CPU %度量建立 hello 警示規則</span><span class="sxs-lookup"><span data-stu-id="0942d-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="0942d-184">擷取 hello 警示規則</span><span class="sxs-lookup"><span data-stu-id="0942d-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="0942d-185">如果警示規則已存在指定屬性的 hello hello 新增警示 cmdlet 也會更新 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="0942d-186">toodisable 警示規則，包括 hello 參數**-DisableRule**。</span><span class="sxs-lookup"><span data-stu-id="0942d-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="0942d-187">取得可用警示計量的清單</span><span class="sxs-lookup"><span data-stu-id="0942d-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="0942d-188">您可以使用 hello `Get-AzureRmMetricDefinition` cmdlet tooview hello 清單的特定資源的所有度量。</span><span class="sxs-lookup"><span data-stu-id="0942d-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="0942d-189">hello 下列範例會產生包含 hello 度量名稱的資料表和它 hello 單位。</span><span class="sxs-lookup"><span data-stu-id="0942d-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="0942d-190">`Get-AzureRmMetricDefinition` 的可用選項完整清單可在 [Get MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx)取得。</span><span class="sxs-lookup"><span data-stu-id="0942d-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="0942d-191">建立和管理自動調整設定</span><span class="sxs-lookup"><span data-stu-id="0942d-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="0942d-192">諸如 Web 應用程式、VM、雲端服務或虛擬機器擴展集之類的資源只能設定一個自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="0942d-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="0942d-193">不過，每個自動調整設定都可以有多個設定檔。</span><span class="sxs-lookup"><span data-stu-id="0942d-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="0942d-194">例如，一個用於以效能為基礎的調整設定檔，以及一個用於以排程為基礎的設定檔。</span><span class="sxs-lookup"><span data-stu-id="0942d-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="0942d-195">每個設定檔都可以設定多個規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="0942d-196">如需自動調整規模的詳細資訊，請參閱[如何 tooAutoscale 應用程式](../cloud-services/cloud-services-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="0942d-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="0942d-197">我們將使用的 hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="0942d-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="0942d-198">建立規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-198">Create rule(s).</span></span>
2. <span data-ttu-id="0942d-199">建立設定檔對應 hello 規則您先前建立 toohello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="0942d-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="0942d-200">選擇性︰設定 Webhook 和電子郵件的屬性，以建立自動調整的通知。</span><span class="sxs-lookup"><span data-stu-id="0942d-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="0942d-201">藉由對應 hello 設定檔和 hello 先前步驟中建立的通知 hello 目標資源的名稱建立的自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="0942d-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="0942d-202">hello 下列範例將示範如何建立自動調整規模設定的虛擬機器擴展集使用 hello CPU 使用量度量的 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="0942d-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="0942d-203">首先，建立規則 tooscale 外，執行個體計數增加。</span><span class="sxs-lookup"><span data-stu-id="0942d-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="0942d-204">與執行個體計數減少，接下來，tooscale 中建立的規則。</span><span class="sxs-lookup"><span data-stu-id="0942d-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="0942d-205">接著，建立 hello 規則的設定檔。</span><span class="sxs-lookup"><span data-stu-id="0942d-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="0942d-206">建立 Webhook 屬性。</span><span class="sxs-lookup"><span data-stu-id="0942d-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="0942d-207">建立 hello hello 自動調整設定，包括電子郵件通知屬性和 hello 您先前建立的 webhook。</span><span class="sxs-lookup"><span data-stu-id="0942d-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="0942d-208">最後，建立 hello 自動調整規模設定 tooadd hello 設定檔，您先前所建立。</span><span class="sxs-lookup"><span data-stu-id="0942d-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="0942d-209">如需有關管理自動調整設定的詳細資訊，請參閱 [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0942d-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="0942d-210">自動調整歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0942d-210">Autoscale history</span></span>
<span data-ttu-id="0942d-211">hello 下列範例示範您可以檢視新的自動調整規模及警示事件的方式。</span><span class="sxs-lookup"><span data-stu-id="0942d-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="0942d-212">使用 hello 活動記錄檔搜尋 tooview hello 自動調整歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0942d-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="0942d-213">您可以使用 hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve 自動調整歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0942d-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="0942d-214">如需詳細資訊，請參閱 [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0942d-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="0942d-215">檢視自動調整設定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="0942d-215">View details for an autoscale setting</span></span>
<span data-ttu-id="0942d-216">您可以使用 hello `Get-Autoscalesetting` cmdlet tooretrieve hello 自動調整規模設定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0942d-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="0942d-217">hello 下列範例顯示所有的自動調整規模設定的相關詳細資料中 hello 資源群組 'myrg1'。</span><span class="sxs-lookup"><span data-stu-id="0942d-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="0942d-218">hello 下列範例顯示 hello 資源群組 'myrg1' 中的所有自動調整規模設定的詳細，並特別 hello 名為 'MyScaleVMSSSetting' 的自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="0942d-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="0942d-219">移除自動調整設定</span><span class="sxs-lookup"><span data-stu-id="0942d-219">Remove an autoscale setting</span></span>
<span data-ttu-id="0942d-220">您可以使用 hello `Remove-Autoscalesetting` cmdlet toodelete 自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="0942d-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="0942d-221">管理活動記錄檔的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="0942d-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="0942d-222">您可以建立*記錄設定檔*和匯出資料，從 [活動記錄 tooa 儲存體帳戶，而且您可以為其設定資料保留。</span><span class="sxs-lookup"><span data-stu-id="0942d-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="0942d-223">（選擇性） 您也可以串流 hello 資料 tooyour 事件中心。</span><span class="sxs-lookup"><span data-stu-id="0942d-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="0942d-224">請注意，此功能目前處於預覽狀態，而且每個訂用帳戶只能建立一個記錄檔設定檔。</span><span class="sxs-lookup"><span data-stu-id="0942d-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="0942d-225">您可以使用下列指令程式，其目前的訂用帳戶 toocreate hello 和管理記錄檔設定檔。</span><span class="sxs-lookup"><span data-stu-id="0942d-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="0942d-226">您也可以選擇特定的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0942d-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="0942d-227">雖然 PowerShell 預設 toohello 目前訂用帳戶，您隨時可以變更該使用`Set-AzureRmContext`。</span><span class="sxs-lookup"><span data-stu-id="0942d-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="0942d-228">您可以設定活動記錄 tooroute 資料 tooany 儲存體帳戶或事件中心內該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0942d-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="0942d-229">資料會以 JSON 格式的 Blob 檔案寫入。</span><span class="sxs-lookup"><span data-stu-id="0942d-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="0942d-230">取得記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="0942d-230">Get a log profile</span></span>
<span data-ttu-id="0942d-231">toofetch 現有的記錄檔設定檔使用 hello `Get-AzureRmLogProfile` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0942d-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="0942d-232">新增沒有資料保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="0942d-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="0942d-233">移除記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="0942d-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="0942d-234">新增包含資料保留期的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="0942d-234">Add a log profile with data retention</span></span>
<span data-ttu-id="0942d-235">您可以指定 hello **-RetentionInDays** hello 數天內，為正整數，hello 資料會保留其中的內容。</span><span class="sxs-lookup"><span data-stu-id="0942d-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="0942d-236">新增包含保留期與 EventHub 的記錄檔設定檔</span><span class="sxs-lookup"><span data-stu-id="0942d-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="0942d-237">加法 toorouting 中您資料的 toostorage 帳戶，您可以也串流處理它 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="0942d-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="0942d-238">請注意，在此預覽版本和 hello 的儲存體帳戶設定是強制性事件中樞設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="0942d-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="0942d-239">設定診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="0942d-239">Configure diagnostics logs</span></span>
<span data-ttu-id="0942d-240">許多 Azure 服務提供額外的記錄檔，可以是 Azure 儲存體帳戶中，設定的 toosave 資料的遙測傳送 tooEvent 中樞和/或傳送 tooan OMS 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="0942d-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="0942d-241">在資源層級只能執行該作業和 hello 儲存體帳戶或事件中心應該會出現在 hello 其中 hello 診斷設定與 hello 目標資源相同的區域。</span><span class="sxs-lookup"><span data-stu-id="0942d-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="0942d-242">取得診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="0942d-243">停用診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="0942d-244">啟用不含保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="0942d-245">啟用含保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="0942d-246">針對特定的記錄檔類別，啟用含保留期的診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="0942d-247">啟用事件中樞的診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="0942d-248">啟用 OMS 的診斷設定</span><span class="sxs-lookup"><span data-stu-id="0942d-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
