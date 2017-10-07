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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Azure web 應用程式中使用 PowerShell tooset 向上 Application Insights
[Microsoft Azure](https://azure.com)可以[設定 toosend Azure 診斷](app-insights-azure-diagnostics.md)太[Azure Application Insights](app-insights-overview.md)。 hello 診斷關聯 tooAzure 雲端服務和 Azure Vm。 搭配您從傳送 hello 應用程式使用 hello Application Insights SDK 中的 hello 遙測。 一部分的自動化 hello 程序在 Azure 中建立新的資源，您可以設定使用 PowerShell 的診斷。

## <a name="azure-template"></a>Azure 範本
如果是在 Azure 中的 hello web 應用程式，並建立您使用 Azure Resource Manager 範本的資源，您可以設定 Application Insights 加入此 toohello 資源節點：

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

* `nameOfAIAppResource`-hello Application Insights 資源名稱
* `myWebAppName`-hello hello web 應用程式識別碼

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>啟用診斷延伸模組做為部署雲端服務的一部分
hello `New-AzureDeployment` cmdlet 有一個參數`ExtensionConfiguration`，其可接受的診斷組態的陣列。 可以建立使用 hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet。 例如：

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>在現有的雲端服務上啟用診斷延伸模組
在現有的服務上，使用 `Set-AzureServiceDiagnosticsExtension`。

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

## <a name="get-current-diagnostics-extension-configuration"></a>取得目前的診斷延伸模組組態
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>移除診斷延伸模組
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

如果您啟用 hello 診斷延伸模組使用`Set-AzureServiceDiagnosticsExtension`或`New-AzureServiceDiagnosticsExtensionConfig`沒有 hello 角色參數，您就可以移除 hello 延伸模組使用`Remove-AzureServiceDiagnosticsExtension`沒有 hello 角色參數。 如果啟用 hello 延伸模組時，使用 hello 角色參數然後就必須也採用時移除 hello 延伸模組。

tooremove 每個個別的角色中的 hello 診斷延伸模組：

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>另請參閱
* [使用 Application Insights 監視 Azure 雲端服務應用程式](app-insights-cloudservices.md)
* [傳送 Azure 診斷 tooApplication Insights](app-insights-azure-diagnostics.md)
* [自動化設定警示](app-insights-powershell-alerts.md)

