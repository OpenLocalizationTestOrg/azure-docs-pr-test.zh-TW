---
title: "使用 PowerShell 在 Azure 雲端服務中啟用診斷 | Microsoft Docs"
description: "了解如何使用 PowerShell 啟用雲端服務的診斷"
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
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="8582c-103">使用 PowerShell 在 Azure 雲端服務中啟用診斷</span><span class="sxs-lookup"><span data-stu-id="8582c-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="8582c-104">您可以使用 Azure 診斷延伸模組，從雲端服務收集診斷資料 (例如應用程式記錄檔、效能計數器等)。</span><span class="sxs-lookup"><span data-stu-id="8582c-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="8582c-105">本文描述如何使用 PowerShell 啟用雲端服務的 Azure 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="8582c-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="8582c-106">如需這篇文章所需要的必要條件，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="8582c-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="8582c-107">啟用診斷延伸模組做為部署雲端服務的一部分</span><span class="sxs-lookup"><span data-stu-id="8582c-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="8582c-108">此方法適用於可以啟用診斷延伸模組做為雲端服務佈署一部分的連續整合類型案例。</span><span class="sxs-lookup"><span data-stu-id="8582c-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="8582c-109">當您建立新的雲端服務部署時，可以啟用診斷擴充，方法是將 *ExtensionConfiguration* 參數傳入 [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8582c-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="8582c-110">*ExtensionConfiguration* 參數接受以 [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) Cmdlet 建立的診斷組態陣列。</span><span class="sxs-lookup"><span data-stu-id="8582c-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="8582c-111">下列範例示範如何為某個雲端服務 (其中的 WebRole 和 WorkerRole 各自擁有不同的診斷組態) 啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="8582c-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="8582c-112">如果診斷組態檔以某個儲存體帳戶名稱指定 `StorageAccount` 元素，則 `New-AzureServiceDiagnosticsExtensionConfig` Cmdlet 將會自動使用該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8582c-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="8582c-113">但該儲存體帳戶所屬的訂用帳戶，必須與雲端服務部署時所屬的訂用帳戶相同，這個方法才有作用。</span><span class="sxs-lookup"><span data-stu-id="8582c-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="8582c-114">從 Azure SDK 2.6 開始，由 MSBuild 發佈目標輸出所產生的擴充設定檔，會包含以服務組態檔 (.cscfg) 中所指定的診斷組態字串為基礎的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="8582c-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="8582c-115">下列指令碼示範在部署雲端服務時，如何從發佈目標輸出來剖析擴充設定檔，以及如何設定每個角色的診斷擴充。</span><span class="sxs-lookup"><span data-stu-id="8582c-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="8582c-116">Visual Studio Online 使用類似的方法，自動部署具有診斷延伸模組的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8582c-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="8582c-117">請參閱 [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) 來取得完整的範例。</span><span class="sxs-lookup"><span data-stu-id="8582c-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="8582c-118">如果您未在診斷組態中指定 `StorageAccount`，則需要將 *StorageAccountName* 參數傳入 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8582c-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="8582c-119">如果已指定 *StorageAccountName* 參數，則 Cmdlet 一定會使用在此參數中指定的儲存體帳戶，而非在診斷組態檔中指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8582c-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="8582c-120">如果診斷儲存體帳戶和雲端服務分別屬於不同的訂用帳戶，您必須明確地將 *StorageAccountName* 和 *StorageAccountKey* 參數傳入 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8582c-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="8582c-121">當診斷儲存體帳戶位於同一個訂用帳戶中時，就不需要使用 *StorageAccountKey* 參數，因為 Cmdlet 會在啟用診斷擴充功能時自動查詢並設定金鑰值。</span><span class="sxs-lookup"><span data-stu-id="8582c-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="8582c-122">不過，如果診斷儲存體帳戶位於不同的訂用帳戶中，Cmdlet 可能就無法自動取得金鑰，您必須透過 *StorageAccountKey* 參數來明確指定金鑰。</span><span class="sxs-lookup"><span data-stu-id="8582c-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="8582c-123">在現有的雲端服務上啟用診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="8582c-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="8582c-124">您可以使用 [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) Cmdlet，在執行中的雲端服務上啟用或更新診斷組態。</span><span class="sxs-lookup"><span data-stu-id="8582c-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="8582c-125">取得目前的診斷延伸模組組態</span><span class="sxs-lookup"><span data-stu-id="8582c-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="8582c-126">使用 [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) Cmdlet 取得雲端服務目前的診斷組態。</span><span class="sxs-lookup"><span data-stu-id="8582c-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="8582c-127">移除診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="8582c-127">Remove diagnostics extension</span></span>
<span data-ttu-id="8582c-128">若要在雲端服務上關閉診斷，您可以使用 [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8582c-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="8582c-129">如果您在未使用 Role 參數的情況下使用 Set-AzureServiceDiagnosticsExtension 或 New-AzureServiceDiagnosticsExtensionConfig 啟用診斷擴充，則您可以在未使用 Role 參數的情況下使用 Remove-AzureServiceDiagnosticsExtension 來移除擴充。</span><span class="sxs-lookup"><span data-stu-id="8582c-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="8582c-130">如果啟用延伸模組時使用了 *Role* 參數，則移除延伸模組時也必須使用該參數。</span><span class="sxs-lookup"><span data-stu-id="8582c-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="8582c-131">若要從每個個別的角色移除診斷延伸模組：</span><span class="sxs-lookup"><span data-stu-id="8582c-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="8582c-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8582c-132">Next Steps</span></span>
* <span data-ttu-id="8582c-133">如需使用 Azure 診斷和其他技術疑難排解問題的詳細指引，請參閱 [在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="8582c-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="8582c-134">[診斷組態結構描述](https://msdn.microsoft.com/library/azure/dn782207.aspx) 說明診斷延伸模組的各種 XML 組態選項。</span><span class="sxs-lookup"><span data-stu-id="8582c-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="8582c-135">若要了解如何啟用虛擬機器的診斷延伸模組，請參閱 [使用 Azure 資源管理員範本建立具有監控和診斷功能的 Windows 虛擬機器](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="8582c-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
