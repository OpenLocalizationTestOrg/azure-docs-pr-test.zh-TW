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
# <a name="virtual-machine-extensions-and-features-for-windows"></a>適用於 Windows 的虛擬機器擴充功能和功能

「Azure 虛擬機器」擴充功能是小型的應用程式，可在「Azure 虛擬機器」上提供部署後設定及自動化工作。 例如，如果虛擬機器需要的軟體安裝、 防毒保護或 Docker 組態，VM 延伸模組可以是使用的 toocomplete 這些工作。 Azure VM 延伸模組可以執行使用 hello Azure CLI、 PowerShell、 Azure 資源管理員範本，與 hello Azure 入口網站。 擴充功能可以與新的虛擬機器部署搭配，或是在任何現有的系統上執行。

本文件概述的虛擬機器擴充功能，使用 toodetect，如何管理和移除虛擬機器擴充功能上的虛擬機器擴充功能和指引的必要條件。 本文件提供通用的資訊，因為有許多可用的 VM 擴充功能，每個都有唯一可能的組態。 在每個文件特定 toohello 個別擴充功能，可以找到延伸模組的特定詳細資料。

## <a name="use-cases-and-samples"></a>使用案例和範例

有許多不同的可用 Azure VM 擴充功能，各有特定使用案例。 部分範例使用案例包括︰

- 套用 hello DSC 延伸模組使用適用於 Windows PowerShell 預期狀態設定 tooa 虛擬機器。 如需詳細資訊，請參閱 [Azure 期望狀態組態擴充功能簡介](extensions-dsc-overview.md)。
- 設定虛擬機器使用 hello Microsoft 監視代理程式 VM 延伸模組進行監視。 如需詳細資訊，請參閱[連接 Azure 虛擬機器 tooLog 分析](../../log-analytics/log-analytics-azure-vm-extension.md)。
- 設定監視 Azure 基礎結構以 hello Datadog 延伸模組。 如需詳細資訊，請參閱 hello [Datadog 部落格](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/)。
- 使用 Chef 設定 Azure 虛擬機器。 如需詳細資訊，請參閱[使用 Chef 自動化 Azure 虛擬機器部署](chef-automation.md)。

此外 tooprocess 特定延伸項目，自訂指令碼延伸模組是適用於 Windows 和 Linux 虛擬機器。 hello 適用於 Windows 的自訂指令碼擴充功能可讓虛擬機器上執行任何 PowerShell 指令碼 toobe。 這對於設計需要超過原生 Azure 工具可提供之組態的 Azure 部署很有用。 如需詳細資訊，請參閱 [Windows VM 自訂指令碼擴充功能](extensions-customscript.md)。


## <a name="prerequisites"></a>必要條件

每個虛擬機器擴充功能可能有它自己的必要條件組。 比方說，hello Docker VM 擴充功能包含受支援的 Linux 散發套件的必要的元件。 Hello 延伸模組特定文件會詳細說明個別的擴充功能的需求。

### <a name="azure-vm-agent"></a>Azure VM 代理程式
hello Azure VM 代理程式管理的 Azure 虛擬機器與 hello Azure 網狀架構控制器之間的互動。 hello VM 代理程式會負責部署及管理 Azure 虛擬機器，包括執行 VM 擴充功能的許多功能層面。 hello Azure VM 代理程式會預先安裝在 Azure Marketplace 映像，並可以安裝在支援的作業系統。

如需有關支援的作業系統和安裝指示，請參閱 [Azure 虛擬機器代理程式](agent-user-guide.md)。

## <a name="discover-vm-extensions"></a>探索 VM 擴充功能
有許多不同的 VM 擴充功能可供與「Azure 虛擬機器」搭配使用。 完整的清單中，執行下列命令以 hello Azure 資源管理員 PowerShell 模組的 hello toosee。 如果您執行此命令，請確定 toospecify hello 預期位置。

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>執行 VM 延伸模組

Azure 虛擬機器擴充功能可以執行現有的虛擬機器上需要 toomake 組態變更，或復原已部署的 VM 上的連線時，會很有用。 VM 擴充功能也可以搭配 Azure Resource Manager 範本部署。 藉由使用資源管理員範本中的擴充功能，您可以啟用 Azure 虛擬機器 toobe 部署和設定而 hello 需要在部署後介入。

hello 下列方法可以是使用的 toorun 針對現有的虛擬機器擴充功能。

### <a name="powershell"></a>PowerShell

有數個 PowerShell 命令可用來執行個別的擴充功能。 清單中，執行下列 PowerShell 命令的 hello toosee。

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

這會提供類似 toohello 下列輸出：

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

hello 下列範例會使用從 GitHub 儲存機制 hello 目標虛擬機器上的 hello 自訂指令碼延伸 toodownload 指令碼，然後執行 hello 指令碼。 如需有關 hello 自訂指令碼擴充功能的詳細資訊，請參閱[自訂指令碼擴充概觀](extensions-customscript.md)。

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

在此範例中，hello VM 存取延伸模組是使用的 tooreset hello 系統管理密碼的 Windows 虛擬機器。 如需有關 hello VM 存取擴充功能的詳細資訊，請參閱[重設遠端桌面服務中 Windows VM](reset-rdp.md)。

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

hello`Set-AzureRmVMExtension`命令可以使用的 toostart 任何 VM 擴充功能。 如需詳細資訊，請參閱 hello[組 AzureRmVMExtension 參考](https://msdn.microsoft.com/en-us/library/mt603745.aspx)。


### <a name="azure-portal"></a>Azure 入口網站

VM 擴充功能可以透過 Azure 入口網站 hello 套用的 tooan 現有虛擬機器。 toodo，選取 hello 虛擬機器要 toouse，選擇**延伸**，然後按一下**新增**。 這會提供可用的擴充功能清單。 選取您想要並遵循 hello 精靈中的 hello 步驟 hello。

hello 下列影像顯示 hello hello Microsoft 反惡意程式碼擴充功能，從 hello Azure 入口網站安裝。

![安裝反惡意程式碼延伸模組](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Azure 資源管理員範本

VM 擴充功能與 hello hello 範本部署執行，而且可以加入的 tooan Azure Resource Manager 範本。 要建立完整設定的 Azure 部署時，使用範本來部署擴充功能很有用。 例如，hello 下列 JSON 取自 Resource Manager 範本將一組負載平衡虛擬機器和 Azure SQL database，部署，然後在每個 VM 上安裝.NET Core 應用程式。 hello VM 延伸模組會負責 hello 軟體安裝。

如需詳細資訊，請參閱 hello[完整 Resource Manager 範本](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。

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

如需詳細資訊，請參閱[使用 Windows VM 擴充功能編寫 Azure Resource Manager 範本](template-description.md#extensions)。

## <a name="secure-vm-extension-data"></a>安全的 VM 擴充功能資料

如果您執行的 VM 延伸模組，可能需要 tooinclude 機密資訊，例如認證、 儲存體帳戶名稱，以及儲存體帳戶存取金鑰。 許多 VM 擴充功能包含受保護的組態加密資料，並只將它解密 hello 目標虛擬機器內。 每個擴充功能都有特定受保護的組態結構描述，而且我們會在擴充功能特定文件中詳細說明。

hello 下列範例顯示 Windows hello 自訂指令碼延伸執行個體。 請注意該 hello 命令 tooexecute 包含一組認證。 在此範例中，將不會加密 hello 命令 tooexecute。


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

藉由移動 hello 安全 hello 執行字串**命令 tooexecute**屬性 toohello**保護**組態。

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

## <a name="troubleshoot-vm-extensions"></a>針對 VM 擴充功能進行疑難排解

每個 VM 擴充功能可能都會有特定的疑難排解步驟。 比方說，當您使用 hello 自訂指令碼擴充功能，指令碼執行詳細資料可以在本機上找 hello hello 延伸模組執行所在的虛擬機器。 所有擴充功能特定的疑難排解步驟都會在擴充功能特定文件中詳述。

下列疑難排解步驟的 hello 套用 tooall 虛擬機器擴充功能。

### <a name="view-extension-status"></a>檢視擴充功能狀態

已執行的虛擬機器的虛擬機器擴充功能之後，請使用下列 PowerShell 命令 tooreturn 延伸模組狀態的 hello。 請以您自己的值取代範例參數名稱。 hello`Name`參數會採用給定 toohello 延伸模組在執行階段的 hello 名稱。

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

hello 輸出看起來像下列 hello:

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

也可以在 hello Azure 入口網站中找到延伸模組的執行狀態。 tooview hello 狀態的延伸，選取 hello 虛擬機器，選擇**延伸**，並選取 hello 所需的擴充功能。

### <a name="rerun-vm-extensions"></a>執行 VM 擴充功能

可能是虛擬機器擴充功能必須 toobe 的情況下重新執行。 您可以移除 hello 延伸模組，然後重新執行您選擇的執行方法 hello 延伸模組。 擴充功能，執行下列命令以 hello Azure PowerShell 模組的 hello tooremove。 請以您自己的值取代範例參數名稱。

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

擴充功能也可以使用 hello Azure 入口網站來移除。 toodo 因此：

1. 選取虛擬機器。
2. 選取 [擴充功能]。
3. 選擇所需的 hello 擴充功能。
4. 選取 [解除安裝]。

## <a name="common-vm-extensions-reference"></a>常見的 VM 擴充功能參考
| 擴充功能名稱 | 說明 | 詳細資訊 |
| --- | --- | --- |
| Windows 的自訂指令碼延伸模組 |對「Azure 虛擬機器」執行指令碼 |[Windows 的自訂指令碼延伸模組](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Windows 的 DSC 延伸模組 |PowerShell DSC (預期狀態設定) 擴充功能 |[適用於 Windows 的 DSC 擴充功能](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure 診斷擴充功能 |管理「Azure 診斷」 |[Azure 診斷擴充功能](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Azure VM 存取擴充功能 |管理使用者和認證 |[適用於 Linux 的 VM 存取擴充功能](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
