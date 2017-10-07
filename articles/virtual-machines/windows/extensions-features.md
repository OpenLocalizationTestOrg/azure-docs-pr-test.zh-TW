---
title: "aaaVirtual 機器適用於 Windows Azure 中的擴充功能和功能 |Microsoft 文件"
description: "了解哪些擴充功能適用於 Azure 虛擬機器，並依它們提供或改善的內容來分組。"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="29c65-103">適用於 Windows 的虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="29c65-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="29c65-104">「Azure 虛擬機器」擴充功能是小型的應用程式，可在「Azure 虛擬機器」上提供部署後設定及自動化工作。</span><span class="sxs-lookup"><span data-stu-id="29c65-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="29c65-105">例如，如果虛擬機器需要的軟體安裝、 防毒保護或 Docker 組態，VM 延伸模組可以是使用的 toocomplete 這些工作。</span><span class="sxs-lookup"><span data-stu-id="29c65-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="29c65-106">Azure VM 延伸模組可以執行使用 hello Azure CLI、 PowerShell、 Azure 資源管理員範本，與 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="29c65-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="29c65-107">擴充功能可以與新的虛擬機器部署搭配，或是在任何現有的系統上執行。</span><span class="sxs-lookup"><span data-stu-id="29c65-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="29c65-108">本文件概述的虛擬機器擴充功能，使用 toodetect，如何管理和移除虛擬機器擴充功能上的虛擬機器擴充功能和指引的必要條件。</span><span class="sxs-lookup"><span data-stu-id="29c65-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="29c65-109">本文件提供通用的資訊，因為有許多可用的 VM 擴充功能，每個都有唯一可能的組態。</span><span class="sxs-lookup"><span data-stu-id="29c65-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="29c65-110">在每個文件特定 toohello 個別擴充功能，可以找到延伸模組的特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="29c65-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="29c65-111">使用案例和範例</span><span class="sxs-lookup"><span data-stu-id="29c65-111">Use cases and samples</span></span>

<span data-ttu-id="29c65-112">有許多不同的可用 Azure VM 擴充功能，各有特定使用案例。</span><span class="sxs-lookup"><span data-stu-id="29c65-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="29c65-113">部分範例使用案例包括︰</span><span class="sxs-lookup"><span data-stu-id="29c65-113">Some example use cases are:</span></span>

- <span data-ttu-id="29c65-114">套用 hello DSC 延伸模組使用適用於 Windows PowerShell 預期狀態設定 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="29c65-115">如需詳細資訊，請參閱 [Azure 期望狀態組態擴充功能簡介](extensions-dsc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="29c65-116">設定虛擬機器使用 hello Microsoft 監視代理程式 VM 延伸模組進行監視。</span><span class="sxs-lookup"><span data-stu-id="29c65-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="29c65-117">如需詳細資訊，請參閱[連接 Azure 虛擬機器 tooLog 分析](../../log-analytics/log-analytics-azure-vm-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="29c65-118">設定監視 Azure 基礎結構以 hello Datadog 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="29c65-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="29c65-119">如需詳細資訊，請參閱 hello [Datadog 部落格](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)。</span><span class="sxs-lookup"><span data-stu-id="29c65-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="29c65-120">使用 Chef 設定 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="29c65-121">如需詳細資訊，請參閱[使用 Chef 自動化 Azure 虛擬機器部署](chef-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="29c65-122">此外 tooprocess 特定延伸項目，自訂指令碼延伸模組是適用於 Windows 和 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="29c65-123">hello 適用於 Windows 的自訂指令碼擴充功能可讓虛擬機器上執行任何 PowerShell 指令碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="29c65-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="29c65-124">這對於設計需要超過原生 Azure 工具可提供之組態的 Azure 部署很有用。</span><span class="sxs-lookup"><span data-stu-id="29c65-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="29c65-125">如需詳細資訊，請參閱 [Windows VM 自訂指令碼擴充功能](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="29c65-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="29c65-126">Prerequisites</span></span>

<span data-ttu-id="29c65-127">每個虛擬機器擴充功能可能有它自己的必要條件組。</span><span class="sxs-lookup"><span data-stu-id="29c65-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="29c65-128">比方說，hello Docker VM 擴充功能包含受支援的 Linux 散發套件的必要的元件。</span><span class="sxs-lookup"><span data-stu-id="29c65-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="29c65-129">Hello 延伸模組特定文件會詳細說明個別的擴充功能的需求。</span><span class="sxs-lookup"><span data-stu-id="29c65-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="29c65-130">Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="29c65-130">Azure VM agent</span></span>
<span data-ttu-id="29c65-131">hello Azure VM 代理程式管理的 Azure 虛擬機器與 hello Azure 網狀架構控制器之間的互動。</span><span class="sxs-lookup"><span data-stu-id="29c65-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="29c65-132">hello VM 代理程式會負責部署及管理 Azure 虛擬機器，包括執行 VM 擴充功能的許多功能層面。</span><span class="sxs-lookup"><span data-stu-id="29c65-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="29c65-133">hello Azure VM 代理程式會預先安裝在 Azure Marketplace 映像，並可以安裝在支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="29c65-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="29c65-134">如需有關支援的作業系統和安裝指示，請參閱 [Azure 虛擬機器代理程式](agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="29c65-135">探索 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-135">Discover VM extensions</span></span>
<span data-ttu-id="29c65-136">有許多不同的 VM 擴充功能可供與「Azure 虛擬機器」搭配使用。</span><span class="sxs-lookup"><span data-stu-id="29c65-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="29c65-137">完整的清單中，執行下列命令以 hello Azure 資源管理員 PowerShell 模組的 hello toosee。</span><span class="sxs-lookup"><span data-stu-id="29c65-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="29c65-138">如果您執行此命令，請確定 toospecify hello 預期位置。</span><span class="sxs-lookup"><span data-stu-id="29c65-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="29c65-139">執行 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="29c65-139">Run VM extensions</span></span>

<span data-ttu-id="29c65-140">Azure 虛擬機器擴充功能可以執行現有的虛擬機器上需要 toomake 組態變更，或復原已部署的 VM 上的連線時，會很有用。</span><span class="sxs-lookup"><span data-stu-id="29c65-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="29c65-141">VM 擴充功能也可以搭配 Azure Resource Manager 範本部署。</span><span class="sxs-lookup"><span data-stu-id="29c65-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="29c65-142">藉由使用資源管理員範本中的擴充功能，您可以啟用 Azure 虛擬機器 toobe 部署和設定而 hello 需要在部署後介入。</span><span class="sxs-lookup"><span data-stu-id="29c65-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="29c65-143">hello 下列方法可以是使用的 toorun 針對現有的虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="29c65-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="29c65-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29c65-144">PowerShell</span></span>

<span data-ttu-id="29c65-145">有數個 PowerShell 命令可用來執行個別的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="29c65-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="29c65-146">清單中，執行下列 PowerShell 命令的 hello toosee。</span><span class="sxs-lookup"><span data-stu-id="29c65-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="29c65-147">這會提供類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="29c65-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="29c65-148">hello 下列範例會使用從 GitHub 儲存機制 hello 目標虛擬機器上的 hello 自訂指令碼延伸 toodownload 指令碼，然後執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="29c65-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="29c65-149">如需有關 hello 自訂指令碼擴充功能的詳細資訊，請參閱[自訂指令碼擴充概觀](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="29c65-150">在此範例中，hello VM 存取延伸模組是使用的 tooreset hello 系統管理密碼的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="29c65-151">如需有關 hello VM 存取擴充功能的詳細資訊，請參閱[重設遠端桌面服務中 Windows VM](reset-rdp.md)。</span><span class="sxs-lookup"><span data-stu-id="29c65-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="29c65-152">hello`Set-AzureRmVMExtension`命令可以使用的 toostart 任何 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="29c65-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="29c65-153">如需詳細資訊，請參閱 hello[組 AzureRmVMExtension 參考](https://msdn.microsoft.com/en-us/library/mt603745.aspx)。</span><span class="sxs-lookup"><span data-stu-id="29c65-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="29c65-154">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="29c65-154">Azure portal</span></span>

<span data-ttu-id="29c65-155">VM 擴充功能可以透過 Azure 入口網站 hello 套用的 tooan 現有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="29c65-156">toodo，選取 hello 虛擬機器要 toouse，選擇**延伸**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="29c65-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="29c65-157">這會提供可用的擴充功能清單。</span><span class="sxs-lookup"><span data-stu-id="29c65-157">This provides a list of available extensions.</span></span> <span data-ttu-id="29c65-158">選取您想要並遵循 hello 精靈中的 hello 步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="29c65-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="29c65-159">hello 下列影像顯示 hello hello Microsoft 反惡意程式碼擴充功能，從 hello Azure 入口網站安裝。</span><span class="sxs-lookup"><span data-stu-id="29c65-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![安裝反惡意程式碼延伸模組](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="29c65-161">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="29c65-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="29c65-162">VM 擴充功能與 hello hello 範本部署執行，而且可以加入的 tooan Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="29c65-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="29c65-163">要建立完整設定的 Azure 部署時，使用範本來部署擴充功能很有用。</span><span class="sxs-lookup"><span data-stu-id="29c65-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="29c65-164">例如，hello 下列 JSON 取自 Resource Manager 範本將一組負載平衡虛擬機器和 Azure SQL database，部署，然後在每個 VM 上安裝.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29c65-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="29c65-165">hello VM 延伸模組會負責 hello 軟體安裝。</span><span class="sxs-lookup"><span data-stu-id="29c65-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="29c65-166">如需詳細資訊，請參閱 hello[完整 Resource Manager 範本](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。</span><span class="sxs-lookup"><span data-stu-id="29c65-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="29c65-167">如需詳細資訊，請參閱[使用 Windows VM 擴充功能編寫 Azure Resource Manager 範本](template-description.md#extensions)。</span><span class="sxs-lookup"><span data-stu-id="29c65-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="29c65-168">安全的 VM 擴充功能資料</span><span class="sxs-lookup"><span data-stu-id="29c65-168">Secure VM extension data</span></span>

<span data-ttu-id="29c65-169">如果您執行的 VM 延伸模組，可能需要 tooinclude 機密資訊，例如認證、 儲存體帳戶名稱，以及儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="29c65-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="29c65-170">許多 VM 擴充功能包含受保護的組態加密資料，並只將它解密 hello 目標虛擬機器內。</span><span class="sxs-lookup"><span data-stu-id="29c65-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="29c65-171">每個擴充功能都有特定受保護的組態結構描述，而且我們會在擴充功能特定文件中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="29c65-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="29c65-172">hello 下列範例顯示 Windows hello 自訂指令碼延伸執行個體。</span><span class="sxs-lookup"><span data-stu-id="29c65-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="29c65-173">請注意該 hello 命令 tooexecute 包含一組認證。</span><span class="sxs-lookup"><span data-stu-id="29c65-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="29c65-174">在此範例中，將不會加密 hello 命令 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="29c65-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="29c65-175">藉由移動 hello 安全 hello 執行字串**命令 tooexecute**屬性 toohello**保護**組態。</span><span class="sxs-lookup"><span data-stu-id="29c65-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="29c65-176">針對 VM 擴充功能進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="29c65-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="29c65-177">每個 VM 擴充功能可能都會有特定的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="29c65-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="29c65-178">比方說，當您使用 hello 自訂指令碼擴充功能，指令碼執行詳細資料可以在本機上找 hello hello 延伸模組執行所在的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="29c65-179">所有擴充功能特定的疑難排解步驟都會在擴充功能特定文件中詳述。</span><span class="sxs-lookup"><span data-stu-id="29c65-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="29c65-180">下列疑難排解步驟的 hello 套用 tooall 虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="29c65-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="29c65-181">檢視擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="29c65-181">View extension status</span></span>

<span data-ttu-id="29c65-182">已執行的虛擬機器的虛擬機器擴充功能之後，請使用下列 PowerShell 命令 tooreturn 延伸模組狀態的 hello。</span><span class="sxs-lookup"><span data-stu-id="29c65-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="29c65-183">請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="29c65-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="29c65-184">hello`Name`參數會採用給定 toohello 延伸模組在執行階段的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="29c65-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="29c65-185">hello 輸出看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="29c65-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="29c65-186">也可以在 hello Azure 入口網站中找到延伸模組的執行狀態。</span><span class="sxs-lookup"><span data-stu-id="29c65-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="29c65-187">tooview hello 狀態的延伸，選取 hello 虛擬機器，選擇**延伸**，並選取 hello 所需的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="29c65-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="29c65-188">執行 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-188">Rerun VM extensions</span></span>

<span data-ttu-id="29c65-189">可能是虛擬機器擴充功能必須 toobe 的情況下重新執行。</span><span class="sxs-lookup"><span data-stu-id="29c65-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="29c65-190">您可以移除 hello 延伸模組，然後重新執行您選擇的執行方法 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="29c65-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="29c65-191">擴充功能，執行下列命令以 hello Azure PowerShell 模組的 hello tooremove。</span><span class="sxs-lookup"><span data-stu-id="29c65-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="29c65-192">請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="29c65-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="29c65-193">擴充功能也可以使用 hello Azure 入口網站來移除。</span><span class="sxs-lookup"><span data-stu-id="29c65-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="29c65-194">toodo 因此：</span><span class="sxs-lookup"><span data-stu-id="29c65-194">toodo so:</span></span>

1. <span data-ttu-id="29c65-195">選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="29c65-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="29c65-196">選取 [擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="29c65-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="29c65-197">選擇所需的 hello 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="29c65-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="29c65-198">選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="29c65-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="29c65-199">常見的 VM 擴充功能參考</span><span class="sxs-lookup"><span data-stu-id="29c65-199">Common VM extensions reference</span></span>
| <span data-ttu-id="29c65-200">擴充功能名稱</span><span class="sxs-lookup"><span data-stu-id="29c65-200">Extension name</span></span> | <span data-ttu-id="29c65-201">說明</span><span class="sxs-lookup"><span data-stu-id="29c65-201">Description</span></span> | <span data-ttu-id="29c65-202">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="29c65-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29c65-203">Windows 的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="29c65-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="29c65-204">對「Azure 虛擬機器」執行指令碼</span><span class="sxs-lookup"><span data-stu-id="29c65-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="29c65-205">Windows 的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="29c65-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="29c65-206">Windows 的 DSC 延伸模組</span><span class="sxs-lookup"><span data-stu-id="29c65-206">DSC Extension for Windows</span></span> |<span data-ttu-id="29c65-207">PowerShell DSC (預期狀態設定) 擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="29c65-208">適用於 Windows 的 DSC 擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="29c65-209">Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="29c65-210">管理「Azure 診斷」</span><span class="sxs-lookup"><span data-stu-id="29c65-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="29c65-211">Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="29c65-212">Azure VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-212">Azure VM Access Extension</span></span> |<span data-ttu-id="29c65-213">管理使用者和認證</span><span class="sxs-lookup"><span data-stu-id="29c65-213">Manage users and credentials</span></span> |[<span data-ttu-id="29c65-214">適用於 Linux 的 VM 存取擴充功能</span><span class="sxs-lookup"><span data-stu-id="29c65-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
