---
title: "Service Fabric 應用程式以使用 PowerShell 的 Azure Log Analytics aaaAssess |Microsoft 文件"
description: "您可以使用 hello Service Fabric 方案中使用 PowerShell tooassess hello 風險和健全狀況服務的網狀架構應用程式、 微服務、 節點和叢集的記錄分析。"
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a>使用 PowerShell 評估 Azure Service Fabric 應用程式和微服務
> [!div class="op_single_selector"]
> * [Resource Manager](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>


![Service Fabric 符號](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

本文說明如何 toouse hello Service Fabric 方案中記錄分析 toohelp 識別及疑難排解問題跨 Service Fabric 叢集。 其可幫助您瞭解 Service Fabric 節點如何執行，以及您的應用程式與微服務的執行狀況。

hello Service Fabric 解決方案會使用從您服務網狀架構的 Vm，Azure 診斷資料收集這項資料從 Azure WAD 資料表。 記錄分析會接著讀取 hello 遵循 Service Fabric 架構事件：

- **可靠服務事件**
- **動作項目事件**
- **運作事件**
- **自訂 ETW 事件**

hello Service Fabric 方案儀表板會顯示 Service Fabric 環境中您值得注意的問題和相關的事件。

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
請依照下列三個簡易步驟 tooinstall，並設定 hello 方案：

1. 建立 hello 您使用 toocreate 所有的叢集資源，包括使用的工作區的儲存體帳戶的 Azure 訂用帳戶的關聯。 請參閱[開始使用 Log Analytics](log-analytics-get-started.md)，以取得建立 Log Analytics 工作區的詳細資訊。
2. 設定記錄分析 toocollect，並檢視 Service Fabric 記錄檔。
3. 啟用工作區中的 hello Service Fabric 解決方案。

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a>設定記錄分析 toocollect 並檢視 Service Fabric 記錄檔
在本節中，您學會 tooconfigure 記錄分析 tooretrieve Service Fabric 記錄的方式。 hello 記錄 tooview 可讓您、 分析和疑難排解問題，在您的叢集或 hello 應用程式和服務在該叢集中，使用 hello OMS 入口網站中執行。

> [!NOTE]
> 設定 hello Azure 診斷擴充功能 tooupload hello 記錄的儲存體資料表。 hello 資料表必須符合記錄分析外觀。 如需詳細資訊，請參閱[toocollect 使用 Azure 診斷的記錄方式](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md)。 本文中的 hello 組態設定範例會顯示 hello 儲存體資料表應該是何種 hello 名稱。 一旦診斷 hello 叢集上設定，並為上傳記錄檔 tooa 儲存體帳戶，hello 下一個步驟是 tooconfigure 記錄分析 toocollect 這些記錄檔。
>
>

請務必更新 hello **EtwEventSourceProviderConfiguration** > 一節中 hello **template.json**檔 tooadd hello 新 EventSources 套用 hello 組態之前更新的項目執行**deploy.ps1**。 hello 資料表上傳為 hello 相同為 (ETWEventTable)。 在 hello 的時刻，記錄分析只能讀取應用程式的 ETW 事件從 hello *WADETWEventTable*資料表。

hello 下列工具將使用的 tooperform 一些在這一節中的 hello 作業：

* Azure PowerShell
* [Operations Management Suite](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a>設定記錄分析工作區 tooshow hello 叢集記錄檔

建立記錄分析工作區之後，設定 hello Azure 儲存體資料表中的 hello 工作區 toopull 記錄檔。 然後，執行下列 PowerShell 指令碼的 hello:

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

設定從 hello Azure hello 記錄分析工作區 tooread 之後登入 toohello Azure 入口網站的儲存體帳戶中的資料表。 選取從 hello 記錄分析工作區**所有資源**。 儲存體帳戶連接的記錄檔 toohello 工作區的 hello 號碼會顯示。 選取 hello**儲存體帳戶記錄**磚。 檢閱您的儲存體帳戶會連線的 toohello 正確的工作區的儲存體帳戶記錄 tooverify hello 清單。

![儲存體帳戶記錄檔](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a>啟用 hello Service Fabric 解決方案
使用下列指令碼 tooadd hello 方案 tooyour 記錄分析工作區的 hello。 在 PowerShell 中，使用 hello 與您想 tooenable hello Service Fabric 方案中的 hello 記錄分析工作區相關聯的 Azure 訂用帳戶執行 hello 指令碼。

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

Hello Service Fabric 磚啟用 hello 方案之後，加入記錄分析 tooyour*概觀*頁面。 hello 頁面會顯示值得注意的問題，例如 runAsync 失敗和取消作業發生在 hello 過去 24 小時內的檢視。

![Service Fabric 圖格](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a>檢視 Service Fabric 事件
按一下 hello **Service Fabric**磚 tooopen hello Service Fabric 儀表板。 hello 儀表板包括 hello 表中的 hello 資料行。 每個資料行計數對應資料行的準則 hello 指定時間範圍列出 hello 前 10 個事件。 您可以執行，即可提供 hello 整個清單的記錄搜尋**查看所有**在 hello 右下的每個資料行，或按一下 hello 資料行標頭。

| **Service Fabric 事件** | **description** |
| --- | --- |
| 值得注意的問題 | 顯示問題，包括 RunAsyncFailures、RunAsynCancellations 及節點關閉。 |
| 運作事件 | 顯示值得注意的運作事件，包括應用程式升級和部署。 |
| 可靠的服務事件 | 顯示值得注意的可靠服務事件，包括 Runasyncinvocations。 |
| 動作項目事件 | 顯示微服務所產生值得注意的動作項目事件。 事件包括動作項目方法擲回的例外狀況、動作項目啟用和停用等等等。 |
| 應用程式事件 | 顯示您的應用程式產生的所有自訂 ETW 事件。 |

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf4.png)

hello 下表顯示資料收集方法，以及適用於 Service Fabric 如何收集資料的其他詳細資料：

| 平台 | 直接代理程式 | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 分鐘 |

> [!NOTE]
> 變更的事件與 hello 領域**資料根據過去七天**在 hello hello 儀表板的頂端。 您也可以顯示 hello 內產生過去七天一天或六個小時的事件。 或者，您可以選取**自訂**toospecify 自訂日期範圍。
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a>針對 Service Fabric 和 Log Analytics 組態進行疑難排解
如果您需要 tooverify 記錄分析設定因為您無法 tooview 中記錄分析的事件資料，請使用下列指令碼的 hello。 它會執行下列動作的 hello:

1. 讀取您的 Service Fabric 診斷設定
2. 將資料寫入至 hello 資料表的檢查
3. 確認記錄分析設定的 tooread hello 資料表

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a>後續步驟
* 使用[中記錄分析記錄搜尋](log-analytics-log-searches.md)tooview 詳細 Service Fabric 事件資料。
