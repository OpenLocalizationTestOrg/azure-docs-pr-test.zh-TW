---
title: "aaaAzure 自訂指令碼延伸的視窗 |Microsoft 文件"
description: "使用 hello 自訂指令碼擴充自動化 Windows VM 組態工作"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Windows 的自訂指令碼延伸模組

hello 自訂指令碼擴充功能下載並在 Azure 虛擬機器上執行指令碼。 此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。 可以從 Azure 儲存體或 GitHub 下載指令碼，或提供 toohello 在執行階段的延伸模組的 Azure 入口網站。 hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。

這份文件詳細說明如何使用自訂指令碼擴充 toouse hello hello Azure PowerShell 模組、 Azure 資源管理員範本及疑難排解在 Windows 系統上的步驟的詳細資料。

## <a name="prerequisites"></a>必要條件

### <a name="operating-system"></a>作業系統

hello 自訂指令碼擴充的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。

### <a name="script-location"></a>指令碼位置

hello 指令碼需要 toobe 儲存在 Azure Blob 儲存體或可透過有效的 URL 存取的任何其他位置。

### <a name="internet-connectivity"></a>網際網路連線

hello 自訂指令碼擴充功能的 Windows 需要該 hello 目標虛擬機器已連接的 toohello 網際網路。 

## <a name="extension-schema"></a>擴充功能結構描述

hello 下列 JSON 顯示 hello hello 自訂指令碼擴充的結構描述。 hello 延伸模組需要的指令碼位置 （Azure 儲存體或其他位置，以有效的 URL） 和命令 tooexecute。 如果使用 Azure 儲存體做為 hello 指令碼來源，Azure 儲存體帳戶名稱和帳戶金鑰需要。 這些項目應該視為機密資料，並且在 hello 延伸的受保護的設定組態中指定。 Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>屬性值

| 名稱 | 值 / 範例 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| 類型 | 擴充功能 |
| typeHandlerVersion | 1.9 |
| fileUris (例如) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (例如) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName (例如) | examplestorageacct |
| storageAccountKey (例如) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**注意** - 屬性名稱會區分大小寫。 如上 tooavoid 部署問題，請使用 hello 名稱。

## <a name="template-deployment"></a>範本部署

也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。 hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 自訂指令碼擴充，在 Azure 資源管理員範本部署期間。 包含自訂指令碼擴充功能可以在這裡，找到的 hello 的範例範本[GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。

## <a name="powershell-deployment"></a>PowerShell 部署

hello`Set-AzureRmVMCustomScriptExtension`命令可以是使用的 tooadd hello 自訂指令碼延伸 tooan 現有的虛擬機器。 如需詳細資訊，請參閱 [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)。
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>疑難排解與支援

### <a name="troubleshoot"></a>疑難排解

從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。 擴充功能，針對指定的 VM，並執行下列命令的 hello toosee hello 部署狀態。

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

延伸模組執行輸出 hello 下找到的記錄的 toofiles 之後，目錄 hello 目標虛擬機器上。
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

hello 指定成 hello hello 目標虛擬機器上下列目錄下載檔案。
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
其中`<n>`是可能會改變 hello 延伸模組的執行之間的十進位整數。  hello`1.*`值符合 hello 實際目前`typeHandlerVersion`hello 延伸的值。  例如，可能是 hello 實際目錄`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`。  

當執行 hello`commandToExecute`命令 hello 延伸模組會將這個目錄 (例如`...\Downloads\2`) 為 hello 目前工作目錄。 這可讓 hello 使用的相對路徑 toolocate hello 檔案下載透過 hello`fileURIs`屬性。 請參閱 hello 表中的範例。

Hello 絕對下載路徑可能會隨著時間，因為它是較佳的相對的指令碼檔案路徑的 hello tooopt`commandToExecute`盡可能字串。 例如：
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

透過 hello 下載路徑資訊之後，檔案會保留第一個 URI 區段 hello`fileUris`屬性清單。  Hello 下表所示，將下載的檔案對應到下載子目錄 tooreflect hello 結構 hello`fileUris`值。  

#### <a name="examples-of-downloaded-files"></a>下載檔案的範例

| fileUris 中的 URI | 相對下載位置 | 絕對下載位置 * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*做為上述 hello 絕對目錄路徑將會變更 hello 存留期的 hello VM，但不是會在單一 hello CustomScript 延伸模組的執行。

### <a name="support"></a>支援

如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello hello [MSDN Azure 和堆疊溢位論壇] 上的 Azure 專家 (https://azure.microsoft.com/en-us/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。 使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。
