---
title: "aaaUsing PowerShell toosetup 在 Azure 中的 Application Insights |Microsoft 文件"
description: "設定 Azure 診斷 toopipe tooApplication Insights 會自動執行。"
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
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="f1b10-103">Azure web 應用程式中使用 PowerShell tooset 向上 Application Insights</span><span class="sxs-lookup"><span data-stu-id="f1b10-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="f1b10-104">[Microsoft Azure](https://azure.com)可以[設定 toosend Azure 診斷](app-insights-azure-diagnostics.md)太[Azure Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f1b10-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f1b10-105">hello 診斷關聯 tooAzure 雲端服務和 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="f1b10-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="f1b10-106">搭配您從傳送 hello 應用程式使用 hello Application Insights SDK 中的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="f1b10-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="f1b10-107">一部分的自動化 hello 程序在 Azure 中建立新的資源，您可以設定使用 PowerShell 的診斷。</span><span class="sxs-lookup"><span data-stu-id="f1b10-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="f1b10-108">Azure 範本</span><span class="sxs-lookup"><span data-stu-id="f1b10-108">Azure template</span></span>
<span data-ttu-id="f1b10-109">如果是在 Azure 中的 hello web 應用程式，並建立您使用 Azure Resource Manager 範本的資源，您可以設定 Application Insights 加入此 toohello 資源節點：</span><span class="sxs-lookup"><span data-stu-id="f1b10-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="f1b10-110">`nameOfAIAppResource`-hello Application Insights 資源名稱</span><span class="sxs-lookup"><span data-stu-id="f1b10-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="f1b10-111">`myWebAppName`-hello hello web 應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="f1b10-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="f1b10-112">啟用診斷延伸模組做為部署雲端服務的一部分</span><span class="sxs-lookup"><span data-stu-id="f1b10-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="f1b10-113">hello `New-AzureDeployment` cmdlet 有一個參數`ExtensionConfiguration`，其可接受的診斷組態的陣列。</span><span class="sxs-lookup"><span data-stu-id="f1b10-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="f1b10-114">可以建立使用 hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f1b10-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="f1b10-115">例如：</span><span class="sxs-lookup"><span data-stu-id="f1b10-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="f1b10-116">在現有的雲端服務上啟用診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="f1b10-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="f1b10-117">在現有的服務上，使用 `Set-AzureServiceDiagnosticsExtension`。</span><span class="sxs-lookup"><span data-stu-id="f1b10-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="f1b10-118">取得目前的診斷延伸模組組態</span><span class="sxs-lookup"><span data-stu-id="f1b10-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="f1b10-119">移除診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="f1b10-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="f1b10-120">如果您啟用 hello 診斷延伸模組使用`Set-AzureServiceDiagnosticsExtension`或`New-AzureServiceDiagnosticsExtensionConfig`沒有 hello 角色參數，您就可以移除 hello 延伸模組使用`Remove-AzureServiceDiagnosticsExtension`沒有 hello 角色參數。</span><span class="sxs-lookup"><span data-stu-id="f1b10-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="f1b10-121">如果啟用 hello 延伸模組時，使用 hello 角色參數然後就必須也採用時移除 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="f1b10-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="f1b10-122">tooremove 每個個別的角色中的 hello 診斷延伸模組：</span><span class="sxs-lookup"><span data-stu-id="f1b10-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="f1b10-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f1b10-123">See also</span></span>
* [<span data-ttu-id="f1b10-124">使用 Application Insights 監視 Azure 雲端服務應用程式</span><span class="sxs-lookup"><span data-stu-id="f1b10-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="f1b10-125">傳送 Azure 診斷 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="f1b10-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="f1b10-126">自動化設定警示</span><span class="sxs-lookup"><span data-stu-id="f1b10-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

