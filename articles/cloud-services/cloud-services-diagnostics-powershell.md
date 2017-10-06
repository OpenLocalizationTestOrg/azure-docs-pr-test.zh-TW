---
title: "使用 PowerShell 的 Azure 雲端服務中的 aaaEnable 診斷 |Microsoft 文件"
description: "了解如何 tooenable 診斷雲端服務以使用 PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>使用 PowerShell 在 Azure 雲端服務中啟用診斷
您可以收集診斷資料，例如應用程式記錄檔、 效能計數器等雲端服務使用 hello Azure 診斷擴充功能。 本文說明如何 tooenable hello 雲端服務，使用 PowerShell 的 Azure 診斷擴充功能。  請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) hello 這個發行項所需的必要條件。

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>啟用診斷延伸模組做為部署雲端服務的一部分
這個方法是適用的 toocontinuous 整合類型的情況下，可以啟用擴充功能，做為部署的一部分的 hello 診斷 hello 雲端服務的位置。 建立新的雲端服務部署時您還可以啟用 hello 診斷延伸模組，透過傳入 hello *ExtensionConfiguration*參數 toohello[新增 AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet。 hello *ExtensionConfiguration*參數會使用的診斷組態，您可以使用 hello 建立陣列[新增 AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet。

hello 下列範例顯示如何啟用 WebRole 和 WorkerRole，各具有不同的診斷組態的雲端服務的診斷功能。

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

如果 hello 診斷組態檔指定`StorageAccount`元素的儲存體帳戶名稱，然後 hello`New-AzureServiceDiagnosticsExtensionConfig`指令程式會自動使用該儲存體帳戶。 針對此 toowork，hello 必須儲存體帳戶中的 toobe hello 相同訂用帳戶，因為 hello 正在部署的雲端服務。

從 Azure SDK 2.6 向前 hello hello MSBuild 所產生的延伸模組組態檔發行目標的輸出將包括 hello hello hello 服務組態檔 (.cscfg) 中指定的診斷組態字串為基礎的儲存體帳戶名稱。 下列的 hello 指令碼會示範如何從 hello tooparse hello 延伸模組組態檔發行目標輸出，及部署 hello 雲端服務時，設定每個角色的診斷延伸模組。

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

Visual Studio Online 的自動部署雲端服務 hello 診斷延伸模組使用類似的方法。 請參閱 [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) 來取得完整的範例。

如果沒有`StorageAccount`中指定了 hello 診斷組態，則您需要在 hello toopass *StorageAccountName*參數 toohello cmdlet。 如果 hello *StorageAccountName*指定參數，則 hello 指令程式將一律使用 hello hello 參數中指定的儲存體帳戶和不 hello hello 診斷組態檔中指定的其中一個。

如果 hello 診斷儲存體帳戶位於不同的訂用帳戶，從 hello 雲端服務，則需要 tooexplicitly 傳入 hello *StorageAccountName*和*StorageAccountKey*參數toohello cmdlet。 hello *StorageAccountKey* hello 診斷儲存體帳戶位於 hello 相同的訂用帳戶，因為 hello 指令程式可自動查詢並設定 hello 機碼值，當啟用 hello 診斷延伸模組時，不需要參數。 不過，如果 hello 診斷儲存體帳戶位於不同的訂用帳戶，然後 hello cmdlet 可能不會自動無法 tooget hello 索引鍵是，您需要 tooexplicitly 指定 hello 金鑰透過 hello *StorageAccountKey*參數。

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>在現有的雲端服務上啟用診斷延伸模組
您可以使用 hello[組 AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0)已在執行中雲端服務上的 cmdlet tooenable 或更新診斷組態。

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>取得目前的診斷延伸模組組態
使用 hello [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello 目前診斷組態的雲端服務。

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>移除診斷延伸模組
tooturn 關閉診斷在雲端服務，您可以使用 hello[移除 AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet。

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

如果您啟用 hello 診斷延伸模組使用*組 AzureServiceDiagnosticsExtension*或 hello*新增 AzureServiceDiagnosticsExtensionConfig*沒有 hello*角色*參數，則您可以移除 hello 延伸模組使用*移除 AzureServiceDiagnosticsExtension*沒有 hello*角色*參數。 如果 hello*角色*啟用 hello 延伸模組，則必須同時使用時移除 hello 延伸模組時，使用參數。

tooremove 每個個別的角色中的 hello 診斷延伸模組：

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>後續步驟
* 如需使用 Azure 診斷和其他技術 tootroubleshoot 問題的其他指引，請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services-dotnet-diagnostics.md)。
* hello[診斷組態結構描述](https://msdn.microsoft.com/library/azure/dn782207.aspx)說明的 hello hello 診斷延伸模組的各種 xml 組態選項。
* 如何 tooenable hello 診斷擴充功能，針對虛擬機器，請參閱的 toolearn[使用監視和診斷使用 Azure Resource Manager 範本建立 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md)
