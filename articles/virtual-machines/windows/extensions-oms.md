---
title: "aaaOMS 適用於 Windows Azure 虛擬機器擴充功能 |Microsoft 文件"
description: "部署 Windows 虛擬機器使用虛擬機器擴充功能上的 hello OMS 代理程式。"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>適用於 Windows 的 OMS 虛擬機器擴充功能

Operations Management Suite (OMS) 可提供雲端和內部部署資產的監視、警示和警示補救功能。 發行 hello OMS Agent for Windows 的虛擬機器擴充功能和 Microsoft 支援。 hello 延伸模組會安裝 Azure 的虛擬機器上的 hello OMS 代理程式，並註冊到現有的 OMS 工作區的虛擬機器。 此文件詳細資料 hello 支援平台、 組態和部署選項 hello OMS 虛擬機器擴充功能的 Windows。

## <a name="prerequisites"></a>必要條件

### <a name="operating-system"></a>作業系統
hello OMS Agent 擴充功能的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。

### <a name="internet-connectivity"></a>網際網路連線
hello 適用於 Windows 的 OMS 代理程式延伸模組需要該 hello 目標虛擬機器已連接的 toohello 網際網路。 

## <a name="extension-schema"></a>擴充功能結構描述

hello 下列 JSON 顯示 hello hello OMS 代理程式延伸結構描述。 hello 延伸模組需要 hello 工作區識別碼和工作區金鑰從 hello 目標 OMS 工作區，這些可以找到 hello OMS 入口網站中。 Hello 工作區金鑰應該視為機密資料，因為它應該儲存在受保護的設定。 Azure VM 延伸模組保護的設定資料加密，且只能解密 hello 目標虛擬機器上。 請注意，**workspaceId** 和 **workspaceKey** 區分大小寫。

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>屬性值

| 名稱 | 值 / 範例 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| 類型 | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| workspaceId (例如) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (例如) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |

## <a name="template-deployment"></a>範本部署

也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。 hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello OMS Agent 擴充功能，在 Azure 資源管理員範本部署期間。 包含 hello OMS 代理程式 VM 擴充功能的範例範本可以找到上 hello [Azure 快速入門圖庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm)。 

可以巢狀方式置於 hello 虛擬機器資源 hello JSON 的虛擬機器擴充功能，或將其放在 hello 根或資源管理員 JSON 範本的最上層。 hello JSON hello 位置會影響 hello hello 資源名稱和類型的值。 如需詳細資訊，請參閱[設定子資源的名稱和類型](../../azure-resource-manager/resource-manager-template-child-resource.md)。 

hello 下列範例假設 hello OMS 擴充功能位於 hello 虛擬機器資源。 巢狀 hello 延伸模組資源、 hello JSON 會放置於 hello `"resources": []` hello 虛擬機器的物件。


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

根目錄 hello hello 範本 hello 擴充 JSON 時，hello 資源名稱包含參考 toohello 父虛擬機器，並 hello 類型會反映 hello 巢狀的組態。 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>PowerShell 部署

hello`Set-AzureRmVMExtension`命令可以是使用的 toodeploy hello OMS 代理程式的虛擬機器擴充功能 tooan 現有的虛擬機器。 在執行之前 hello 命令，hello 公用和私用組態需要 toobe PowerShell 雜湊表中儲存。 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>疑難排解與支援

### <a name="troubleshoot"></a>疑難排解

從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。 toosee hello 部署狀態的延伸模組指定的 vm 時，執行下列命令所使用的 hello hello Azure PowerShell 模組。

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

延伸模組執行輸出 hello 中找到的記錄的 toofiles 之後，目錄：

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>支援

如果您需要更多說明，在本文中的任何時間點，您可以連絡 hello 上 hello Azure 專家[MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。 使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。
