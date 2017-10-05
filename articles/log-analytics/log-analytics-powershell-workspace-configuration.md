---
title: "使用 PowerShell 建立和設定 Log Analytics 工作區 | Microsoft Docs"
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="87884-104">使用 PowerShell 管理 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="87884-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="87884-105">您可以從命令列或在指令碼中，使用 [Log Analytics PowerShell Cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 在 Log Analytics 中執行各種功能。</span><span class="sxs-lookup"><span data-stu-id="87884-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="87884-106">您可以使用 PowerShell 執行的工作範例包括︰</span><span class="sxs-lookup"><span data-stu-id="87884-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="87884-107">建立工作區</span><span class="sxs-lookup"><span data-stu-id="87884-107">Create a workspace</span></span>
* <span data-ttu-id="87884-108">新增或移除方案</span><span class="sxs-lookup"><span data-stu-id="87884-108">Add or remove a solution</span></span>
* <span data-ttu-id="87884-109">匯入和匯出已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="87884-109">Import and export saved searches</span></span>
* <span data-ttu-id="87884-110">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="87884-110">Create a computer group</span></span>
* <span data-ttu-id="87884-111">從已安裝 Windows 代理程式的電腦啟用 IIS 記錄檔收集功能</span><span class="sxs-lookup"><span data-stu-id="87884-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="87884-112">從 Linux 和 Windows 電腦收集效能計數器</span><span class="sxs-lookup"><span data-stu-id="87884-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="87884-113">在 Linux 電腦上收集 syslog 事件</span><span class="sxs-lookup"><span data-stu-id="87884-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="87884-114">從 Windows 事件記錄檔收集事件</span><span class="sxs-lookup"><span data-stu-id="87884-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="87884-115">收集自訂事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="87884-115">Collect custom event logs</span></span>
* <span data-ttu-id="87884-116">將 Log Analytics 代理程式加入至 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="87884-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="87884-117">設定 Log Analytics 將 Azure 診斷所收集的資料編製索引</span><span class="sxs-lookup"><span data-stu-id="87884-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="87884-118">本文提供兩個程式碼範例，示範您可以從 PowerShell 執行的一些功能。</span><span class="sxs-lookup"><span data-stu-id="87884-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="87884-119">關於其他功能，您可以參考 [Log Analytics PowerShell Cmdlet 參考文件](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="87884-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="87884-120">Log Analytics 在以前稱為 Operational Insights，這也是 Cmdlet 中使用此名稱的原因。</span><span class="sxs-lookup"><span data-stu-id="87884-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="87884-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="87884-121">Prerequisites</span></span>
<span data-ttu-id="87884-122">這些範例可與 AzureRm.OperationalInsights 模組的 2.3.0 版或更新版本搭配運作。</span><span class="sxs-lookup"><span data-stu-id="87884-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="87884-123">建立及設定 Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="87884-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="87884-124">下列指令碼範例說明如何：</span><span class="sxs-lookup"><span data-stu-id="87884-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="87884-125">建立工作區</span><span class="sxs-lookup"><span data-stu-id="87884-125">Create a workspace</span></span>
2. <span data-ttu-id="87884-126">列出可用的方案</span><span class="sxs-lookup"><span data-stu-id="87884-126">List the available solutions</span></span>
3. <span data-ttu-id="87884-127">將方案加入至工作區</span><span class="sxs-lookup"><span data-stu-id="87884-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="87884-128">匯入已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="87884-128">Import saved searches</span></span>
5. <span data-ttu-id="87884-129">匯出已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="87884-129">Export saved searches</span></span>
6. <span data-ttu-id="87884-130">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="87884-130">Create a computer group</span></span>
7. <span data-ttu-id="87884-131">從已安裝 Windows 代理程式的電腦啟用 IIS 記錄檔收集功能</span><span class="sxs-lookup"><span data-stu-id="87884-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="87884-132">從 Linux 電腦收集邏輯磁碟效能計數器 (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span><span class="sxs-lookup"><span data-stu-id="87884-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="87884-133">從 Linux 電腦收集 syslog 事件</span><span class="sxs-lookup"><span data-stu-id="87884-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="87884-134">從 Windows 電腦的應用程式事件記錄檔收集錯誤和警告事件</span><span class="sxs-lookup"><span data-stu-id="87884-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="87884-135">從 Windows 電腦收集記憶體可用 Mb 效能計數器</span><span class="sxs-lookup"><span data-stu-id="87884-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="87884-136">收集自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="87884-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="87884-137">設定 Log Analytics 來編製 Azure 診斷的索引</span><span class="sxs-lookup"><span data-stu-id="87884-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="87884-138">若要以無代理程式的方式監視 Azure 資源，資源需要啟用 Azure 診斷並將其設定為寫入至 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="87884-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="87884-139">此方法會將資料直接傳送到 Log Analytics，而且不需要將資料寫入儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="87884-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="87884-140">支援的資源包括：</span><span class="sxs-lookup"><span data-stu-id="87884-140">Supported resources include:</span></span>

| <span data-ttu-id="87884-141">資源類型</span><span class="sxs-lookup"><span data-stu-id="87884-141">Resource Type</span></span> | <span data-ttu-id="87884-142">記錄檔</span><span class="sxs-lookup"><span data-stu-id="87884-142">Logs</span></span> | <span data-ttu-id="87884-143">度量</span><span class="sxs-lookup"><span data-stu-id="87884-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87884-144">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="87884-144">Application Gateways</span></span>    | <span data-ttu-id="87884-145">是</span><span class="sxs-lookup"><span data-stu-id="87884-145">Yes</span></span> | <span data-ttu-id="87884-146">是</span><span class="sxs-lookup"><span data-stu-id="87884-146">Yes</span></span> |
| <span data-ttu-id="87884-147">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="87884-147">Automation accounts</span></span>     | <span data-ttu-id="87884-148">是</span><span class="sxs-lookup"><span data-stu-id="87884-148">Yes</span></span> | |
| <span data-ttu-id="87884-149">Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="87884-149">Batch accounts</span></span>          | <span data-ttu-id="87884-150">是</span><span class="sxs-lookup"><span data-stu-id="87884-150">Yes</span></span> | <span data-ttu-id="87884-151">是</span><span class="sxs-lookup"><span data-stu-id="87884-151">Yes</span></span> |
| <span data-ttu-id="87884-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="87884-152">Data Lake analytics</span></span>     | <span data-ttu-id="87884-153">是</span><span class="sxs-lookup"><span data-stu-id="87884-153">Yes</span></span> | | 
| <span data-ttu-id="87884-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="87884-154">Data Lake store</span></span>         | <span data-ttu-id="87884-155">是</span><span class="sxs-lookup"><span data-stu-id="87884-155">Yes</span></span> | |
| <span data-ttu-id="87884-156">SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="87884-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="87884-157">是</span><span class="sxs-lookup"><span data-stu-id="87884-157">Yes</span></span> |
| <span data-ttu-id="87884-158">事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="87884-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="87884-159">是</span><span class="sxs-lookup"><span data-stu-id="87884-159">Yes</span></span> |
| <span data-ttu-id="87884-160">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="87884-160">IoT Hubs</span></span>                |     | <span data-ttu-id="87884-161">是</span><span class="sxs-lookup"><span data-stu-id="87884-161">Yes</span></span> |
| <span data-ttu-id="87884-162">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="87884-162">Key Vault</span></span>               | <span data-ttu-id="87884-163">是</span><span class="sxs-lookup"><span data-stu-id="87884-163">Yes</span></span> | |
| <span data-ttu-id="87884-164">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="87884-164">Load Balancers</span></span>          | <span data-ttu-id="87884-165">是</span><span class="sxs-lookup"><span data-stu-id="87884-165">Yes</span></span> | |
| <span data-ttu-id="87884-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="87884-166">Logic Apps</span></span>              | <span data-ttu-id="87884-167">是</span><span class="sxs-lookup"><span data-stu-id="87884-167">Yes</span></span> | <span data-ttu-id="87884-168">是</span><span class="sxs-lookup"><span data-stu-id="87884-168">Yes</span></span> |
| <span data-ttu-id="87884-169">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="87884-169">Network Security Groups</span></span> | <span data-ttu-id="87884-170">是</span><span class="sxs-lookup"><span data-stu-id="87884-170">Yes</span></span> | |
| <span data-ttu-id="87884-171">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="87884-171">Redis Cache</span></span>             |     | <span data-ttu-id="87884-172">是</span><span class="sxs-lookup"><span data-stu-id="87884-172">Yes</span></span> |
| <span data-ttu-id="87884-173">搜尋服務</span><span class="sxs-lookup"><span data-stu-id="87884-173">Search services</span></span>         | <span data-ttu-id="87884-174">是</span><span class="sxs-lookup"><span data-stu-id="87884-174">Yes</span></span> | <span data-ttu-id="87884-175">是</span><span class="sxs-lookup"><span data-stu-id="87884-175">Yes</span></span> |
| <span data-ttu-id="87884-176">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="87884-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="87884-177">是</span><span class="sxs-lookup"><span data-stu-id="87884-177">Yes</span></span> |
| <span data-ttu-id="87884-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="87884-178">SQL (v12)</span></span>               |     | <span data-ttu-id="87884-179">是</span><span class="sxs-lookup"><span data-stu-id="87884-179">Yes</span></span> |
| <span data-ttu-id="87884-180">網站</span><span class="sxs-lookup"><span data-stu-id="87884-180">Web Sites</span></span>               |     | <span data-ttu-id="87884-181">是</span><span class="sxs-lookup"><span data-stu-id="87884-181">Yes</span></span> |
| <span data-ttu-id="87884-182">Web 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="87884-182">Web Server farms</span></span>        |     | <span data-ttu-id="87884-183">是</span><span class="sxs-lookup"><span data-stu-id="87884-183">Yes</span></span> |

<span data-ttu-id="87884-184">如需可用度量的詳細資訊，請參閱[支援 Azure 監視器的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="87884-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="87884-185">如需可用記錄檔的詳細資訊，請參閱[支援的服務以及診斷記錄檔的結構描述](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="87884-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="87884-186">您也可以使用前述 Cmdlet，來收集不同訂用帳戶中之資源的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87884-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="87884-187">因為您會提供建立記錄檔之資源和記錄檔所傳送至之工作區這兩個項目的識別碼，因此這個 Cmdlet 可跨訂用帳戶運作。</span><span class="sxs-lookup"><span data-stu-id="87884-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="87884-188">設定 Log Analytics 以對來自儲存體的 Azure 診斷編製索引</span><span class="sxs-lookup"><span data-stu-id="87884-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="87884-189">若要從傳統雲端服務或 Service Fabric 叢集的執行中執行個體內收集記錄檔資料，您必須先將資料寫入 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="87884-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="87884-190">然後，可將 Log Analytics 設定為從儲存體帳戶收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87884-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="87884-191">支援的資源包括：</span><span class="sxs-lookup"><span data-stu-id="87884-191">Supported resources include:</span></span>

* <span data-ttu-id="87884-192">傳統雲端服務 (Web 和背景工作角色)</span><span class="sxs-lookup"><span data-stu-id="87884-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="87884-193">Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="87884-193">Service fabric clusters</span></span>

<span data-ttu-id="87884-194">下列範例示範如何執行：</span><span class="sxs-lookup"><span data-stu-id="87884-194">The following example shows how to:</span></span>

1. <span data-ttu-id="87884-195">列出現有的儲存體帳戶和 Log Analytics 檢索的資源來源位置</span><span class="sxs-lookup"><span data-stu-id="87884-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="87884-196">建立組態以讀取儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="87884-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="87884-197">更新新建立的組態以檢索其他位置的資料</span><span class="sxs-lookup"><span data-stu-id="87884-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="87884-198">刪除新建立的組態</span><span class="sxs-lookup"><span data-stu-id="87884-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="87884-199">您也可以使用前述指令碼，來收集不同訂用帳戶中之儲存體帳戶的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="87884-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="87884-200">因為您會提供儲存體帳戶資源識別碼和對應的存取金鑰，因此指令碼可跨訂用帳戶運作。</span><span class="sxs-lookup"><span data-stu-id="87884-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="87884-201">當您變更存取金鑰時，您需要更新儲存體深入解析使其擁有新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="87884-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="87884-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87884-202">Next steps</span></span>
* <span data-ttu-id="87884-203">[檢閱 Log Analytics PowerShell Cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="87884-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

