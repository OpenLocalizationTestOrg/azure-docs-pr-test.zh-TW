---
title: "aaaUse PowerShell tooCreate 及設定記錄分析工作區 |Microsoft 文件"
description: "Log Analytics 會使用來自內部部署或雲端基礎結構中之伺服器的資料。 您可以在 Azure 診斷產生電腦資料時，從 Azure 儲存體加以收集。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="1b24d-104">使用 PowerShell 管理 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1b24d-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="1b24d-105">您可以使用 hello[記錄分析 PowerShell cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform 各種函式中記錄分析從命令列或指令碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="1b24d-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="1b24d-106">您可以使用 PowerShell 執行 hello 工作的範例包括：</span><span class="sxs-lookup"><span data-stu-id="1b24d-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="1b24d-107">建立工作區</span><span class="sxs-lookup"><span data-stu-id="1b24d-107">Create a workspace</span></span>
* <span data-ttu-id="1b24d-108">新增或移除方案</span><span class="sxs-lookup"><span data-stu-id="1b24d-108">Add or remove a solution</span></span>
* <span data-ttu-id="1b24d-109">匯入和匯出已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="1b24d-109">Import and export saved searches</span></span>
* <span data-ttu-id="1b24d-110">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="1b24d-110">Create a computer group</span></span>
* <span data-ttu-id="1b24d-111">啟用從電腦的 IIS 記錄檔收集 hello 已安裝的 Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="1b24d-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="1b24d-112">從 Linux 和 Windows 電腦收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="1b24d-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="1b24d-113">在 Linux 電腦上收集 syslog 事件</span><span class="sxs-lookup"><span data-stu-id="1b24d-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="1b24d-114">從 Windows 事件記錄檔收集事件</span><span class="sxs-lookup"><span data-stu-id="1b24d-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="1b24d-115">收集自訂事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b24d-115">Collect custom event logs</span></span>
* <span data-ttu-id="1b24d-116">新增 hello 記錄分析代理程式 tooan Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1b24d-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="1b24d-117">設定使用 Azure 診斷收集記錄檔分析 tooindex 資料</span><span class="sxs-lookup"><span data-stu-id="1b24d-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="1b24d-118">本文章提供兩個程式碼範例將示範一些您可以從 PowerShell 執行的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="1b24d-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="1b24d-119">您可以使用參照 toohello[記錄分析 PowerShell cmdlet 參考](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx)對其他函式。</span><span class="sxs-lookup"><span data-stu-id="1b24d-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="1b24d-120">記錄分析前稱為 Operational Insights，這也是為什麼 hello hello cmdlet 中使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="1b24d-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1b24d-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="1b24d-121">Prerequisites</span></span>
<span data-ttu-id="1b24d-122">這些範例處理 2.3.0 版本或更新版本的 hello AzureRm.OperationalInsights 模組。</span><span class="sxs-lookup"><span data-stu-id="1b24d-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="1b24d-123">建立及設定 Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="1b24d-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="1b24d-124">hello 下列指令碼範例說明如何：</span><span class="sxs-lookup"><span data-stu-id="1b24d-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="1b24d-125">建立工作區</span><span class="sxs-lookup"><span data-stu-id="1b24d-125">Create a workspace</span></span>
2. <span data-ttu-id="1b24d-126">清單 hello 可用的解決方案</span><span class="sxs-lookup"><span data-stu-id="1b24d-126">List hello available solutions</span></span>
3. <span data-ttu-id="1b24d-127">新增解決方案 toohello 工作區</span><span class="sxs-lookup"><span data-stu-id="1b24d-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="1b24d-128">匯入已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="1b24d-128">Import saved searches</span></span>
5. <span data-ttu-id="1b24d-129">匯出已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="1b24d-129">Export saved searches</span></span>
6. <span data-ttu-id="1b24d-130">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="1b24d-130">Create a computer group</span></span>
7. <span data-ttu-id="1b24d-131">啟用從電腦的 IIS 記錄檔收集 hello 已安裝的 Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="1b24d-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="1b24d-132">從 Linux 電腦收集邏輯磁碟效能計數器 (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span><span class="sxs-lookup"><span data-stu-id="1b24d-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="1b24d-133">從 Linux 電腦收集 syslog 事件</span><span class="sxs-lookup"><span data-stu-id="1b24d-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="1b24d-134">從 Windows 電腦的 hello 應用程式事件記錄檔收集錯誤和警告事件</span><span class="sxs-lookup"><span data-stu-id="1b24d-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="1b24d-135">從 Windows 電腦收集記憶體可用 Mb 效能計數器</span><span class="sxs-lookup"><span data-stu-id="1b24d-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="1b24d-136">收集自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b24d-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="1b24d-137">設定 Azure 診斷的記錄分析 tooindex</span><span class="sxs-lookup"><span data-stu-id="1b24d-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="1b24d-138">Azure 資源的無代理程式監視，hello 資源需要 toohave Azure 診斷已啟用且設定 toowrite tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="1b24d-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="1b24d-139">這個方法會將資料傳送直接 tooLog 分析，而且不需要資料 toobe 寫入 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b24d-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="1b24d-140">支援的資源包括：</span><span class="sxs-lookup"><span data-stu-id="1b24d-140">Supported resources include:</span></span>

| <span data-ttu-id="1b24d-141">資源類型</span><span class="sxs-lookup"><span data-stu-id="1b24d-141">Resource Type</span></span> | <span data-ttu-id="1b24d-142">記錄檔</span><span class="sxs-lookup"><span data-stu-id="1b24d-142">Logs</span></span> | <span data-ttu-id="1b24d-143">度量</span><span class="sxs-lookup"><span data-stu-id="1b24d-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b24d-144">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1b24d-144">Application Gateways</span></span>    | <span data-ttu-id="1b24d-145">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-145">Yes</span></span> | <span data-ttu-id="1b24d-146">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-146">Yes</span></span> |
| <span data-ttu-id="1b24d-147">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="1b24d-147">Automation accounts</span></span>     | <span data-ttu-id="1b24d-148">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-148">Yes</span></span> | |
| <span data-ttu-id="1b24d-149">Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="1b24d-149">Batch accounts</span></span>          | <span data-ttu-id="1b24d-150">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-150">Yes</span></span> | <span data-ttu-id="1b24d-151">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-151">Yes</span></span> |
| <span data-ttu-id="1b24d-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1b24d-152">Data Lake analytics</span></span>     | <span data-ttu-id="1b24d-153">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-153">Yes</span></span> | | 
| <span data-ttu-id="1b24d-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1b24d-154">Data Lake store</span></span>         | <span data-ttu-id="1b24d-155">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-155">Yes</span></span> | |
| <span data-ttu-id="1b24d-156">SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="1b24d-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="1b24d-157">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-157">Yes</span></span> |
| <span data-ttu-id="1b24d-158">事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="1b24d-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="1b24d-159">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-159">Yes</span></span> |
| <span data-ttu-id="1b24d-160">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="1b24d-160">IoT Hubs</span></span>                |     | <span data-ttu-id="1b24d-161">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-161">Yes</span></span> |
| <span data-ttu-id="1b24d-162">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="1b24d-162">Key Vault</span></span>               | <span data-ttu-id="1b24d-163">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-163">Yes</span></span> | |
| <span data-ttu-id="1b24d-164">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="1b24d-164">Load Balancers</span></span>          | <span data-ttu-id="1b24d-165">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-165">Yes</span></span> | |
| <span data-ttu-id="1b24d-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1b24d-166">Logic Apps</span></span>              | <span data-ttu-id="1b24d-167">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-167">Yes</span></span> | <span data-ttu-id="1b24d-168">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-168">Yes</span></span> |
| <span data-ttu-id="1b24d-169">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="1b24d-169">Network Security Groups</span></span> | <span data-ttu-id="1b24d-170">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-170">Yes</span></span> | |
| <span data-ttu-id="1b24d-171">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="1b24d-171">Redis Cache</span></span>             |     | <span data-ttu-id="1b24d-172">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-172">Yes</span></span> |
| <span data-ttu-id="1b24d-173">搜尋服務</span><span class="sxs-lookup"><span data-stu-id="1b24d-173">Search services</span></span>         | <span data-ttu-id="1b24d-174">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-174">Yes</span></span> | <span data-ttu-id="1b24d-175">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-175">Yes</span></span> |
| <span data-ttu-id="1b24d-176">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="1b24d-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="1b24d-177">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-177">Yes</span></span> |
| <span data-ttu-id="1b24d-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="1b24d-178">SQL (v12)</span></span>               |     | <span data-ttu-id="1b24d-179">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-179">Yes</span></span> |
| <span data-ttu-id="1b24d-180">網站</span><span class="sxs-lookup"><span data-stu-id="1b24d-180">Web Sites</span></span>               |     | <span data-ttu-id="1b24d-181">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-181">Yes</span></span> |
| <span data-ttu-id="1b24d-182">Web 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="1b24d-182">Web Server farms</span></span>        |     | <span data-ttu-id="1b24d-183">是</span><span class="sxs-lookup"><span data-stu-id="1b24d-183">Yes</span></span> |

<span data-ttu-id="1b24d-184">Hello hello 可用度量的詳細資訊，請參閱太[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="1b24d-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="1b24d-185">Hello 的 hello 可用的記錄檔的詳細資訊，請參閱太[支援診斷記錄檔的服務和結構描述](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="1b24d-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="1b24d-186">您也可以使用 hello 前面 cmdlet toocollect 記錄檔，從不同的訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="1b24d-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="1b24d-187">hello cmdlet 是無法 toowork 跨訂用帳戶，因為您提供建立記錄檔的這兩個 hello 資源 hello id，然後再 hello 工作區 hello 記錄會傳送到。</span><span class="sxs-lookup"><span data-stu-id="1b24d-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="1b24d-188">設定記錄分析 tooindex 從儲存體的 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="1b24d-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="1b24d-189">toocollect 記錄資料從 service fabric 叢集或傳統的雲端服務的執行個體中，您需要 toofirst 寫入 hello tooAzure 儲存資料。</span><span class="sxs-lookup"><span data-stu-id="1b24d-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="1b24d-190">記錄分析就設定 toocollect hello 記錄檔從 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b24d-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="1b24d-191">支援的資源包括：</span><span class="sxs-lookup"><span data-stu-id="1b24d-191">Supported resources include:</span></span>

* <span data-ttu-id="1b24d-192">傳統雲端服務 (Web 和背景工作角色)</span><span class="sxs-lookup"><span data-stu-id="1b24d-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="1b24d-193">Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="1b24d-193">Service fabric clusters</span></span>

<span data-ttu-id="1b24d-194">下列範例會示範如何 hello 至：</span><span class="sxs-lookup"><span data-stu-id="1b24d-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="1b24d-195">列出 hello 現有儲存體帳戶和記錄分析將索引資料的位置</span><span class="sxs-lookup"><span data-stu-id="1b24d-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="1b24d-196">從儲存體帳戶中建立組態 tooread</span><span class="sxs-lookup"><span data-stu-id="1b24d-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="1b24d-197">新建立的組態 tooindex 資料從其他位置更新 hello</span><span class="sxs-lookup"><span data-stu-id="1b24d-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="1b24d-198">刪除 hello 新建立的組態</span><span class="sxs-lookup"><span data-stu-id="1b24d-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="1b24d-199">您也可以使用上述指令碼 toocollect 記錄檔從儲存體帳戶不同的訂用帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1b24d-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="1b24d-200">hello 指令碼是無法 toowork 跨訂用帳戶，因為您可以提供 hello 儲存體帳戶資源識別碼和對應的便捷鍵。</span><span class="sxs-lookup"><span data-stu-id="1b24d-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="1b24d-201">當您變更 hello 便捷鍵時，您會需要 tooupdate hello 儲存深入了解 toohave hello 新金鑰。</span><span class="sxs-lookup"><span data-stu-id="1b24d-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b24d-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b24d-202">Next steps</span></span>
* <span data-ttu-id="1b24d-203">[檢閱 Log Analytics PowerShell Cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="1b24d-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

