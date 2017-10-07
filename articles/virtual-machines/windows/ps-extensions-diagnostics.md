---
title: "在 Windows VM 上的 Azure PowerShell tooenable 診斷 aaaUse |Microsoft 文件"
services: virtual-machines-windows
documentationcenter: 
description: "深入了解如何在執行 Windows 的虛擬機器的 toouse PowerShell tooenable Azure 診斷"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="714e7-103">在執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="714e7-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="714e7-104">Azure 診斷是在啟用 hello 集合上部署的應用程式的診斷資料的 Azure 中的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="714e7-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="714e7-105">您可以使用 hello 診斷延伸模組 toocollect 診斷資料，例如應用程式記錄檔或從 Azure 虛擬機器 (VM) 執行 Windows 的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="714e7-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="714e7-106">本文說明如何 toouse Windows PowerShell tooenable hello vm 的診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="714e7-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="714e7-107">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) hello 這個發行項所需的必要條件。</span><span class="sxs-lookup"><span data-stu-id="714e7-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="714e7-108">啟用 hello 診斷延伸模組，如果您使用 hello Resource Manager 部署模型</span><span class="sxs-lookup"><span data-stu-id="714e7-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="714e7-109">您新增 hello 延伸模組組態 toohello Resource Manager 範本建立 Windows VM 透過 hello Azure Resource Manager 部署模型時，您可以啟用 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="714e7-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="714e7-110">請參閱[利用 hello Azure Resource Manager 範本建立的監視和診斷的 Windows 虛擬機器](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="714e7-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="714e7-111">tooenable hello 的診斷延伸模組透過 hello Resource Manager 部署模型所建立的現有 VM，您可以使用 hello[組 AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet，如下所示。</span><span class="sxs-lookup"><span data-stu-id="714e7-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="714e7-112">*$diagnosticsconfig_path* hello 路徑 toohello 檔案包含在 XML 中的 hello 診斷組態中所述 hello[範例](#sample-diagnostics-configuration)下方。</span><span class="sxs-lookup"><span data-stu-id="714e7-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="714e7-113">如果 hello 診斷組態檔指定**StorageAccount**元素的儲存體帳戶名稱，然後 hello*組 AzureRMVMDiagnosticsExtension*指令碼將會自動設定 hello診斷延伸模組 toosend 診斷資料 toothat 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="714e7-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="714e7-114">針對此 toowork，hello 必須儲存體帳戶中的 toobe hello 相同訂用帳戶，因為 hello VM。</span><span class="sxs-lookup"><span data-stu-id="714e7-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="714e7-115">如果沒有**StorageAccount**中指定了 hello 診斷組態，則您需要在 hello toopass *StorageAccountName*參數 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="714e7-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="714e7-116">如果 hello *StorageAccountName*指定參數，則 hello 指令程式將一律使用 hello hello 參數中指定的儲存體帳戶和不 hello hello 診斷組態檔中指定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="714e7-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="714e7-117">如果 hello 診斷儲存體帳戶位於不同的訂用帳戶，從 hello VM，則您需要 tooexplicitly 傳入 hello *StorageAccountName*和*StorageAccountKey*參數 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="714e7-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="714e7-118">hello *StorageAccountKey* hello 診斷儲存體帳戶位於 hello 相同的訂用帳戶，因為 hello 指令程式可自動查詢並設定 hello 機碼值，當啟用 hello 診斷延伸模組時，不需要參數。</span><span class="sxs-lookup"><span data-stu-id="714e7-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="714e7-119">不過，如果 hello 診斷儲存體帳戶位於不同的訂用帳戶，然後 hello cmdlet 可能不會自動無法 tooget hello 索引鍵是，您需要 tooexplicitly 指定 hello 金鑰透過 hello *StorageAccountKey*參數。</span><span class="sxs-lookup"><span data-stu-id="714e7-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="714e7-120">在 VM 上啟用 hello 診斷延伸模組後，您可以使用 hello 取得 hello 目前設定[Get AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="714e7-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="714e7-121">hello cmdlet 會傳回*PublicSettings*，其中包含 hello 診斷組態。</span><span class="sxs-lookup"><span data-stu-id="714e7-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="714e7-122">系統支援兩種設定，WadCfg 和 xmlCfg。</span><span class="sxs-lookup"><span data-stu-id="714e7-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="714e7-123">WadCfg 為 JSON 設定，xmlCfg 則是 Base64 編碼格式的 XML 設定。</span><span class="sxs-lookup"><span data-stu-id="714e7-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="714e7-124">tooread hello XML，您需要 toodecode 它。</span><span class="sxs-lookup"><span data-stu-id="714e7-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="714e7-125">hello[移除 AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension)指令程式可從 hello VM 使用的 tooremove hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="714e7-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="714e7-126">啟用 hello 診斷延伸模組，如果您使用 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="714e7-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="714e7-127">您可以使用 hello[組 AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable 您透過 hello 傳統部署模型所建立的 VM 的診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="714e7-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="714e7-128">hello 下列範例說明如何 toocreate 新的 VM，透過 hello 傳統部署模型具有 hello 診斷擴充功能啟用。</span><span class="sxs-lookup"><span data-stu-id="714e7-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="714e7-129">現有的 VM 建立透過 hello 傳統部署模型，第一個使用 hello 的 tooenable hello 診斷延伸模組[Get-azurevm](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM 組態。</span><span class="sxs-lookup"><span data-stu-id="714e7-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="714e7-130">然後使用 hello 更新 hello VM 組態 tooinclude hello 診斷延伸模組[組 AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="714e7-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="714e7-131">最後，藉由套用更新的 hello 組態 toohello VM [Update-azurevm](/powershell/module/azure/update-azurevm)。</span><span class="sxs-lookup"><span data-stu-id="714e7-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="714e7-132">範例診斷組態</span><span class="sxs-lookup"><span data-stu-id="714e7-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="714e7-133">下列 XML 可用於以上述指令碼的 hello hello 診斷公用組態的 hello。</span><span class="sxs-lookup"><span data-stu-id="714e7-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="714e7-134">此範例組態會從 hello 診斷傳輸各種效能計數器 toohello 診斷儲存體帳戶，以及從 hello 應用程式、 安全性和系統通道 hello Windows 事件記錄檔中的錯誤以及任何錯誤基礎結構記錄檔。</span><span class="sxs-lookup"><span data-stu-id="714e7-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="714e7-135">hello 組態需要 toobe 更新的 tooinclude hello 下列：</span><span class="sxs-lookup"><span data-stu-id="714e7-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="714e7-136">hello *resourceID*屬性 hello**度量**項目需要 toobe hello 資源識別碼 hello VM 已更新。</span><span class="sxs-lookup"><span data-stu-id="714e7-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="714e7-137">hello 識別碼可以使用下列模式的 hello 建構的資源:"/ 訂用帳戶 / {*hello VM hello 訂用帳戶的訂用帳戶 ID*} /resourceGroups/ {*hello VMhelloresourcegroup名稱*} / providers/Microsoft.Compute/virtualMachines/ {*hello VM 名稱*}"。</span><span class="sxs-lookup"><span data-stu-id="714e7-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="714e7-138">例如，如果 hello hello hello VM 執行所在的訂用帳戶的訂用帳戶 ID 是**11111111-1111-1111-1111-111111111111**，hello hello 資源群組的資源群組名稱是**MyResourceGroup**，且 hello VM 名稱是**MyWindowsVM**，然後 hello 值*resourceID*會是：</span><span class="sxs-lookup"><span data-stu-id="714e7-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="714e7-139">如需有關如何度量資訊會產生根據的 hello 效能計數器和計量組態的詳細資訊，請參閱[儲存體中的 Azure 診斷度量資料表](extensions-diagnostics-template.md#wadmetrics-tables-in-storage)。</span><span class="sxs-lookup"><span data-stu-id="714e7-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="714e7-140">hello **StorageAccount**項目需要 toobe 更新 hello hello 診斷儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="714e7-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="714e7-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="714e7-141">Next steps</span></span>
* <span data-ttu-id="714e7-142">如需使用 hello Azure 診斷功能和其他技術 tootroubleshoot 問題的其他指引，請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](../../cloud-services/cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="714e7-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="714e7-143">[診斷組態結構描述](https://msdn.microsoft.com/library/azure/mt634524.aspx)說明的 hello hello 診斷延伸模組的各種 XML 組態選項。</span><span class="sxs-lookup"><span data-stu-id="714e7-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

