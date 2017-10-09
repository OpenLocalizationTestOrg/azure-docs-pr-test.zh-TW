---
title: "aaaCustom Windows VM 上的指令碼延伸 |Microsoft 文件"
description: "在遠端 Windows VM 上使用 hello 自訂指令碼延伸 toorun PowerShell 指令碼自動化 Azure VM 組態工作"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>自訂指令碼擴充功能的 Windows hello 傳統部署模型

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

hello 自訂指令碼擴充功能下載並在 Azure 虛擬機器上執行指令碼。 此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。 可以從 Azure 儲存體或 GitHub 下載指令碼，或提供 toohello 在執行階段的延伸模組的 Azure 入口網站。 hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。

這份文件詳細說明如何使用自訂指令碼擴充 toouse hello hello Azure PowerShell 模組、 Azure 資源管理員範本及疑難排解在 Windows 系統上的步驟的詳細資料。

## <a name="prerequisites"></a>必要條件

### <a name="operating-system"></a>作業系統

hello 自訂指令碼擴充的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。

### <a name="script-location"></a>指令碼位置

hello 指令碼需要 toobe 儲存在 Azure 儲存體或可透過有效的 URL 存取的任何其他位置。

### <a name="internet-connectivity"></a>網際網路連線

hello 自訂指令碼擴充功能的 Windows 需要該 hello 目標虛擬機器已連接的 toohello 網際網路。 

## <a name="extension-schema"></a>擴充功能結構描述

hello 下列 JSON 顯示 hello hello 自訂指令碼擴充的結構描述。 hello 延伸模組需要的指令碼位置 （Azure 儲存體或其他位置，以有效的 URL） 和命令 tooexecute。 如果使用 Azure 儲存體做為 hello 指令碼來源，Azure 儲存體帳戶名稱和帳戶金鑰需要。 這些項目應該視為機密資料，並且在 hello 延伸的受保護的設定組態中指定。 Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a>屬性值

| 名稱 | 值 / 範例 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| 擴充功能 | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (例如) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (例如) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |

## <a name="template-deployment"></a>範本部署

也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。 hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 自訂指令碼擴充，在 Azure 資源管理員範本部署期間。 包含自訂指令碼擴充功能可以在這裡，找到的 hello 的範例範本[GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。

## <a name="powershell-deployment"></a>PowerShell 部署

hello`Set-AzureVMCustomScriptExtension`命令可以是使用的 tooadd hello 自訂指令碼延伸 tooan 現有的虛擬機器。 如需詳細資訊，請參閱 [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension)。

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>疑難排解與支援

### <a name="troubleshoot"></a>疑難排解

從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。 擴充功能，針對指定的 VM，並執行下列命令的 hello toosee hello 部署狀態。

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

延伸模組執行輸出我們記錄 toofiles hello hello 目標虛擬機器上下列目錄中找到。

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

hello 指令碼本身會下載到 hello hello 目標虛擬機器上下列目錄。

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>支援

如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello 上 hello Azure 專家[MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。 使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。
