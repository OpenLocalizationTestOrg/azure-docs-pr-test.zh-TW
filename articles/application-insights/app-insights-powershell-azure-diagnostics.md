---
title: "使用 PowerShell 在 Azure 中設定 Application Insights | Microsoft Docs"
description: "自動設定 Azure 診斷以透過管道傳送至 Application Insights。"
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="3fb6c-103">使用 PowerShell 為 Azure Web 應用程式設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3fb6c-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="3fb6c-104">[Microsoft Azure](https://azure.com) 可以[設定為傳送 Azure 診斷](app-insights-azure-diagnostics.md)至 [Azure Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="3fb6c-105">診斷與 Azure 雲端服務和 Azure VM 相關。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="3fb6c-106">可輔助您從應用程式使用 Application Insights SDK 傳送的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="3fb6c-107">在 Azure 中自動建立新資源的程序中，您可以使用 PowerShell 設定診斷。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="3fb6c-108">Azure 範本</span><span class="sxs-lookup"><span data-stu-id="3fb6c-108">Azure template</span></span>
<span data-ttu-id="3fb6c-109">如果 Web 應用程式位於 Azure 內，而且您使用 Azure Resource Manager 範本建立資源，您可以透過將以下內容新增到資源節點來設定 Application Insights：</span><span class="sxs-lookup"><span data-stu-id="3fb6c-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="3fb6c-110">`nameOfAIAppResource` - Application Insights 資源的名稱</span><span class="sxs-lookup"><span data-stu-id="3fb6c-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="3fb6c-111">`myWebAppName` - Web 應用程式的識別碼</span><span class="sxs-lookup"><span data-stu-id="3fb6c-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="3fb6c-112">啟用診斷延伸模組做為部署雲端服務的一部分</span><span class="sxs-lookup"><span data-stu-id="3fb6c-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="3fb6c-113">`New-AzureDeployment` Cmdlet 具有 `ExtensionConfiguration` 參數，其採用診斷組態的陣列。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="3fb6c-114">使用 `New-AzureServiceDiagnosticsExtensionConfig` Cmdlet 建立可以診斷組態。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="3fb6c-115">例如：</span><span class="sxs-lookup"><span data-stu-id="3fb6c-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="3fb6c-116">在現有的雲端服務上啟用診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="3fb6c-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="3fb6c-117">在現有的服務上，使用 `Set-AzureServiceDiagnosticsExtension`。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="3fb6c-118">取得目前的診斷延伸模組組態</span><span class="sxs-lookup"><span data-stu-id="3fb6c-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="3fb6c-119">移除診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="3fb6c-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="3fb6c-120">如果您在未使用 Role 參數的情況下使用 `Set-AzureServiceDiagnosticsExtension` 或 `New-AzureServiceDiagnosticsExtensionConfig` 啟用診斷延伸模組，則您可以在未使用 Role 參數的情況下使用 `Remove-AzureServiceDiagnosticsExtension` 移除延伸模組。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="3fb6c-121">如果啟用延伸模組時使用了 Role 參數，則移除延伸模組時也必須使用該參數。</span><span class="sxs-lookup"><span data-stu-id="3fb6c-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="3fb6c-122">若要從每個個別的角色移除診斷延伸模組：</span><span class="sxs-lookup"><span data-stu-id="3fb6c-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="3fb6c-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3fb6c-123">See also</span></span>
* [<span data-ttu-id="3fb6c-124">使用 Application Insights 監視 Azure 雲端服務應用程式</span><span class="sxs-lookup"><span data-stu-id="3fb6c-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="3fb6c-125">將 Azure 診斷傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3fb6c-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="3fb6c-126">自動化設定警示</span><span class="sxs-lookup"><span data-stu-id="3fb6c-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

