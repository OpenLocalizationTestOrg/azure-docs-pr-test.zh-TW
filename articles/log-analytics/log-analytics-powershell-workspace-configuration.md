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
# <a name="manage-log-analytics-using-powershell"></a>使用 PowerShell 管理 Log Analytics
您可以使用 hello[記錄分析 PowerShell cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform 各種函式中記錄分析從命令列或指令碼的一部分。  您可以使用 PowerShell 執行 hello 工作的範例包括：

* 建立工作區
* 新增或移除方案
* 匯入和匯出已儲存的搜尋
* 建立電腦群組
* 啟用從電腦的 IIS 記錄檔收集 hello 已安裝的 Windows 代理程式
* 從 Linux 和 Windows 電腦收集效能計數器
* 在 Linux 電腦上收集 syslog 事件 
* 從 Windows 事件記錄檔收集事件
* 收集自訂事件記錄檔
* 新增 hello 記錄分析代理程式 tooan Azure 虛擬機器
* 設定使用 Azure 診斷收集記錄檔分析 tooindex 資料

本文章提供兩個程式碼範例將示範一些您可以從 PowerShell 執行的 hello 函式。  您可以使用參照 toohello[記錄分析 PowerShell cmdlet 參考](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx)對其他函式。

> [!NOTE]
> 記錄分析前稱為 Operational Insights，這也是為什麼 hello hello cmdlet 中使用的名稱。
> 
> 

## <a name="prerequisites"></a>必要條件
這些範例處理 2.3.0 版本或更新版本的 hello AzureRm.OperationalInsights 模組。


## <a name="create-and-configure-a-log-analytics-workspace"></a>建立及設定 Log Analytics 工作區
hello 下列指令碼範例說明如何：

1. 建立工作區
2. 清單 hello 可用的解決方案
3. 新增解決方案 toohello 工作區
4. 匯入已儲存的搜尋
5. 匯出已儲存的搜尋
6. 建立電腦群組
7. 啟用從電腦的 IIS 記錄檔收集 hello 已安裝的 Windows 代理程式
8. 從 Linux 電腦收集邏輯磁碟效能計數器 (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)
9. 從 Linux 電腦收集 syslog 事件
10. 從 Windows 電腦的 hello 應用程式事件記錄檔收集錯誤和警告事件
11. 從 Windows 電腦收集記憶體可用 Mb 效能計數器
12. 收集自訂記錄檔 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>設定 Azure 診斷的記錄分析 tooindex
Azure 資源的無代理程式監視，hello 資源需要 toohave Azure 診斷已啟用且設定 toowrite tooa 記錄分析工作區。 這個方法會將資料傳送直接 tooLog 分析，而且不需要資料 toobe 寫入 tooa 儲存體帳戶。 支援的資源包括：

| 資源類型 | 記錄檔 | 度量 |
| --- | --- | --- |
| 應用程式閘道    | 是 | 是 |
| 自動化帳戶     | 是 | |
| Batch 帳戶          | 是 | 是 |
| Data Lake Analytics     | 是 | | 
| Data Lake Store         | 是 | |
| SQL 彈性集區        |     | 是 |
| 事件中樞命名空間     |     | 是 |
| IoT 中樞                |     | 是 |
| 金鑰保存庫               | 是 | |
| 負載平衡器          | 是 | |
| Logic Apps              | 是 | 是 |
| 網路安全性群組 | 是 | |
| Redis 快取             |     | 是 |
| 搜尋服務         | 是 | 是 |
| 服務匯流排命名空間   |     | 是 |
| SQL (v12)               |     | 是 |
| 網站               |     | 是 |
| Web 伺服器陣列        |     | 是 |

Hello hello 可用度量的詳細資訊，請參閱太[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。

Hello 的 hello 可用的記錄檔的詳細資訊，請參閱太[支援診斷記錄檔的服務和結構描述](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)。

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

您也可以使用 hello 前面 cmdlet toocollect 記錄檔，從不同的訂用帳戶中的資源。 hello cmdlet 是無法 toowork 跨訂用帳戶，因為您提供建立記錄檔的這兩個 hello 資源 hello id，然後再 hello 工作區 hello 記錄會傳送到。


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>設定記錄分析 tooindex 從儲存體的 Azure 診斷
toocollect 記錄資料從 service fabric 叢集或傳統的雲端服務的執行個體中，您需要 toofirst 寫入 hello tooAzure 儲存資料。 記錄分析就設定 toocollect hello 記錄檔從 hello 儲存體帳戶。 支援的資源包括：

* 傳統雲端服務 (Web 和背景工作角色)
* Service Fabric 叢集

下列範例會示範如何 hello 至：

1. 列出 hello 現有儲存體帳戶和記錄分析將索引資料的位置
2. 從儲存體帳戶中建立組態 tooread
3. 新建立的組態 tooindex 資料從其他位置更新 hello
4. 刪除 hello 新建立的組態

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

您也可以使用上述指令碼 toocollect 記錄檔從儲存體帳戶不同的訂用帳戶中的 hello。 hello 指令碼是無法 toowork 跨訂用帳戶，因為您可以提供 hello 儲存體帳戶資源識別碼和對應的便捷鍵。 當您變更 hello 便捷鍵時，您會需要 tooupdate hello 儲存深入了解 toohave hello 新金鑰。


## <a name="next-steps"></a>後續步驟
* [檢閱 Log Analytics PowerShell Cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 。

