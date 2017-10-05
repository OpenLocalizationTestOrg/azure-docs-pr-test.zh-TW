---
title: "使用 PowerShell 以 Azure Log Analytics 評估 Service Fabric 應用程式 | Microsoft Docs"
description: "您可以在 Log Analytics 中使用 PowerShell，使用 Service Fabric 解決方案評估 Service Fabric 應用程式、微服務、節點和叢集的風險和健全狀況。"
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
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="3fbb7-103">使用 PowerShell 評估 Azure Service Fabric 應用程式和微服務</span><span class="sxs-lookup"><span data-stu-id="3fbb7-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fbb7-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3fbb7-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="3fbb7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fbb7-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Service Fabric 符號](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="3fbb7-107">這篇文章說明如何在 Log Analytics 中使用 Service Fabric 解決方案，協助識別整個 Service Fabric 叢集的問題並且進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="3fbb7-108">其可幫助您瞭解 Service Fabric 節點如何執行，以及您的應用程式與微服務的執行狀況。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="3fbb7-109">Service Fabric 解決方案會從 Service Fabric VM 使用 Azure 診斷資料，方法是從 Azure WAD 資料表收集此資料。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="3fbb7-110">接著 Log Analytics 會讀取下列 Service Fabric 架構事件：</span><span class="sxs-lookup"><span data-stu-id="3fbb7-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="3fbb7-111">**可靠服務事件**</span><span class="sxs-lookup"><span data-stu-id="3fbb7-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="3fbb7-112">**動作項目事件**</span><span class="sxs-lookup"><span data-stu-id="3fbb7-112">**Actor Events**</span></span>
- <span data-ttu-id="3fbb7-113">**運作事件**</span><span class="sxs-lookup"><span data-stu-id="3fbb7-113">**Operational Events**</span></span>
- <span data-ttu-id="3fbb7-114">**自訂 ETW 事件**</span><span class="sxs-lookup"><span data-stu-id="3fbb7-114">**Custom ETW events**</span></span>

<span data-ttu-id="3fbb7-115">Service Fabric 解決方案儀表板會向您顯示 Service Fabric 環境中值得注意的問題和相關事件。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="3fbb7-116">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="3fbb7-116">Installing and configuring the solution</span></span>
<span data-ttu-id="3fbb7-117">請遵循這三個簡單步驟以安裝及設定解決方案︰</span><span class="sxs-lookup"><span data-stu-id="3fbb7-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="3fbb7-118">請將您用來建立所有叢集資源 (包括儲存體帳戶) 的 Azure 訂用帳戶與您的工作區建立關聯。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="3fbb7-119">請參閱[開始使用 Log Analytics](log-analytics-get-started.md)，以取得建立 Log Analytics 工作區的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="3fbb7-120">設定 Log Analytics 以收集及檢視 Service Fabric 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="3fbb7-121">在您的工作區中啟用 Service Fabric 解決方案。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="3fbb7-122">設定 Log Analytics 以收集及檢視 Service Fabric 記錄檔</span><span class="sxs-lookup"><span data-stu-id="3fbb7-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="3fbb7-123">在本節中，您將學習如何設定 Log Analytics 以擷取 Service Fabric 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="3fbb7-124">記錄檔可讓您使用 OMS 入口網站，針對叢集或叢集中所執行的應用程式與服務，檢視、分析其中的問題，並且進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3fbb7-125">設定 Azure 診斷擴充功能，以上傳儲存體資料表的記錄。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="3fbb7-126">資料表必須符合 Log Analytics 尋找的項目。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="3fbb7-127">如需詳細資訊，請參閱[使用 Azure 診斷收集記錄](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md)。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="3fbb7-128">這份文章中的組態設定範例將顯示儲存體資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="3fbb7-129">在叢集上設定好診斷，並且將記錄檔上傳至儲存體帳戶之後，下一個步驟便是設定 Log Analytics 來收集這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="3fbb7-130">確定您更新 **template.json** 檔案中的 **EtwEventSourceProviderConfiguration** 區段，以在藉由執行 **deploy.ps1** EventSources 的項目。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="3fbb7-131">要上傳的資料表與 (ETWEventTable) 相同。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="3fbb7-132">目前，Log Analytics 只能從 *WADETWEventTable* 資料表中讀取應用程式 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="3fbb7-133">下列工具是用來執行此章節中的某些作業：</span><span class="sxs-lookup"><span data-stu-id="3fbb7-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="3fbb7-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fbb7-134">Azure PowerShell</span></span>
* [<span data-ttu-id="3fbb7-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3fbb7-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="3fbb7-136">設定 Log Analytics 工作區來顯示叢集記錄檔</span><span class="sxs-lookup"><span data-stu-id="3fbb7-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="3fbb7-137">建立 Log Analytics 工作區後，將該工作區設定為從 Azure 儲存體資料表提取記錄。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="3fbb7-138">接著請執行下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="3fbb7-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
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
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
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
                                # HTTP Not Found is returned if the storage insight doesn't exist
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
                                      # If any of the tables from the table list are not already monitored, then we add them
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

<span data-ttu-id="3fbb7-139">設定 Log Analytics 工作區以讀取儲存體帳戶的 Azure 資料表之後，接著請登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="3fbb7-140">選取 [所有資源] 中的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="3fbb7-141">系統會顯示連接到該工作區的儲存體帳戶記錄數目。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="3fbb7-142">選取 [儲存體帳戶記錄] 圖格。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="3fbb7-143">檢閱儲存體帳戶記錄，確認您的儲存體帳戶連接到正確的工作區。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![儲存體帳戶記錄檔](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="3fbb7-145">啟用 Service Fabric 解決方案</span><span class="sxs-lookup"><span data-stu-id="3fbb7-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="3fbb7-146">使用下列指令碼以將解決方案新增至 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="3fbb7-147">在 PowerShell 中執行指令碼，使用與您想要在其中啟用 Service Fabric 解決方案的 Log Analytics 工作區相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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

<span data-ttu-id="3fbb7-148">在您啟用解決方案後，Service Fabric 圖格會新增至 Log Analytics 的 [概觀] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="3fbb7-149">該頁面會顯示值得注意的問題，例如過去 24 小時內發生的 runAsync 失敗和取消作業。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Service Fabric 圖格](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="3fbb7-151">檢視 Service Fabric 事件</span><span class="sxs-lookup"><span data-stu-id="3fbb7-151">View Service Fabric events</span></span>
<span data-ttu-id="3fbb7-152">按一下 [Service Fabric] 圖格以開啟 Service Fabric 儀表板。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="3fbb7-153">儀表板中包含下表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="3fbb7-154">每個資料行依計數列出前 10 個事件，這幾個事件符合該資料行中指定時間範圍的準則。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="3fbb7-155">您可以按一下每個資料行右下角的 [查看全部] ，或按一下資料行標頭，以執行記錄搜尋來提供完整清單。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="3fbb7-156">**Service Fabric 事件**</span><span class="sxs-lookup"><span data-stu-id="3fbb7-156">**Service Fabric event**</span></span> | <span data-ttu-id="3fbb7-157">**description**</span><span class="sxs-lookup"><span data-stu-id="3fbb7-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="3fbb7-158">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="3fbb7-158">Notable Issues</span></span> | <span data-ttu-id="3fbb7-159">顯示問題，包括 RunAsyncFailures、RunAsynCancellations 及節點關閉。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="3fbb7-160">運作事件</span><span class="sxs-lookup"><span data-stu-id="3fbb7-160">Operational Events</span></span> | <span data-ttu-id="3fbb7-161">顯示值得注意的運作事件，包括應用程式升級和部署。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="3fbb7-162">可靠的服務事件</span><span class="sxs-lookup"><span data-stu-id="3fbb7-162">Reliable Service Events</span></span> | <span data-ttu-id="3fbb7-163">顯示值得注意的可靠服務事件，包括 Runasyncinvocations。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="3fbb7-164">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="3fbb7-164">Actor Events</span></span> | <span data-ttu-id="3fbb7-165">顯示微服務所產生值得注意的動作項目事件。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="3fbb7-166">事件包括動作項目方法擲回的例外狀況、動作項目啟用和停用等等等。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="3fbb7-167">應用程式事件</span><span class="sxs-lookup"><span data-stu-id="3fbb7-167">Application Events</span></span> | <span data-ttu-id="3fbb7-168">顯示您的應用程式產生的所有自訂 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-168">Displays all custom ETW events generated by your applications.</span></span> |

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="3fbb7-171">下表顯示 Service Fabric 的資料收集方法及如何收集資料的其他詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3fbb7-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="3fbb7-172">平台</span><span class="sxs-lookup"><span data-stu-id="3fbb7-172">platform</span></span> | <span data-ttu-id="3fbb7-173">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="3fbb7-173">Direct Agent</span></span> | <span data-ttu-id="3fbb7-174">Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="3fbb7-174">Operations Manager agent</span></span> | <span data-ttu-id="3fbb7-175">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="3fbb7-175">Azure Storage</span></span> | <span data-ttu-id="3fbb7-176">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="3fbb7-176">Operations Manager required?</span></span> | <span data-ttu-id="3fbb7-177">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="3fbb7-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="3fbb7-178">收集頻率</span><span class="sxs-lookup"><span data-stu-id="3fbb7-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3fbb7-179">Windows</span><span class="sxs-lookup"><span data-stu-id="3fbb7-179">Windows</span></span> |  |  | <span data-ttu-id="3fbb7-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="3fbb7-180">&#8226;</span></span> |  |  |<span data-ttu-id="3fbb7-181">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="3fbb7-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="3fbb7-182">透過儀表板頂端的 [Data based on last seven days]\(根據最近 7 天的資料\) 變更事件範圍。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="3fbb7-183">您也可以顯示過去七天、一天或六個小時內產生的事件。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="3fbb7-184">或者，也可以選取 [自訂]，以指定自訂日期範圍。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="3fbb7-185">針對 Service Fabric 和 Log Analytics 組態進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3fbb7-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="3fbb7-186">因為無法在 Log Analytics 中檢視事件資料，而需要確認 Log Analytics 設定時，請使用下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="3fbb7-187">其會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="3fbb7-187">It performs the following actions:</span></span>

1. <span data-ttu-id="3fbb7-188">讀取您的 Service Fabric 診斷設定</span><span class="sxs-lookup"><span data-stu-id="3fbb7-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="3fbb7-189">檢查寫入表格的資料</span><span class="sxs-lookup"><span data-stu-id="3fbb7-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="3fbb7-190">確認 Log Analytics 已設定成從表格讀取</span><span class="sxs-lookup"><span data-stu-id="3fbb7-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
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
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
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
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
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
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
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
    Check if ETW provider is configured to log events to the expected table storage
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
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
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


## <a name="next-steps"></a><span data-ttu-id="3fbb7-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fbb7-191">Next steps</span></span>
* <span data-ttu-id="3fbb7-192">使用 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md)，檢視詳細的 Service Fabric 事件資料。</span><span class="sxs-lookup"><span data-stu-id="3fbb7-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
